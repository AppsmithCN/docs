# MySQL

本页介绍如何在PagePlug中连接到 MySQL 数据库并使用它来执行查询。

{% hint style="info" %}
小tips

PagePlug 支持 MySQL 版本 5.5、5.6、5.7 和 8.0。
{% endhint %}



### 1、创建MySQL

要添加 MySQL 数据源，请单击**数据源旁边的 ( + )** 号。在下一个屏幕上，选择**MySQL**按钮。

<figure><img src="../../../.gitbook/assets/image (38) (1) (2).png" alt=""><figcaption></figcaption></figure>

### 2、连接MySQL

<figure><img src="../../../.gitbook/assets/image (59) (2).png" alt=""><figcaption><p>mysql连接页面</p></figcaption></figure>

{% hint style="info" %}
如果你想连接自己本地的数据库，你可以用ngrok来穿透。有关详细信息，请参阅如何连接到 PagePlug 上的本地数据库。
{% endhint %}

要连接到您的数据库，PagePlug需要以下参数。所有必填字段均以星号 ( \* ) 为后缀。

* <mark style="color:red;">**Conneciton Mode**</mark>：选择在建立与数据库的连接时授予PagePlug的权限。两种可用模式是：只读模式、读取/写入模式
* <mark style="color:red;">**Host Address**</mark>：提供数据库服务器的主机名或 IP 地址。
* <mark style="color:red;">**Port**</mark>：提供连接到数据库的端口。默认情况下，PagePlug会尝试连接到端口`5432`。
* Database Name：提供数据库的名称
* Authentication：填写连接你数据库的用户名和密码
* SSL：支持Default、Required、Disabled的模式来设置您的查询是否使用 SSL 连接
* MySQL Specific Parameters：\
  服务器时区覆盖，提供一个有效的时区（例如：“UTC”）以用于您的查询。如果 plugpage不自动识别 MySQL 服务器的时区，请使用此选项。

### 3、创建Mysql查询

你可以通过选择 MySQL数据源下的表来<mark style="color:red;">**新建查询，**</mark>支持Select、INSERT、UPDATE、DELETE四种方式

<figure><img src="../../../.gitbook/assets/image (34) (3).png" alt=""><figcaption></figcaption></figure>

或者可以点击对应的数据源，点击新建查询，方便后续编写查询以获取数据或将数据写入 MySQL 数据库。

<figure><img src="../../../.gitbook/assets/image (4) (4).png" alt=""><figcaption></figcaption></figure>

#### 1、SELECT方式

使用`SELECT`语句从表中检索数据。例如，要从表中获取记录`users`：

```
SELECT * FROM users ORDER BY id LIMIT 10;
```

<figure><img src="../../../.gitbook/assets/image (5) (2) (1) (2).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
强烈建议像示例一样使用`LIMIT`运算符，以防止一次查询大量数据。您还可以阅读有关如何对[数据进行分页的信息](https://docs.appsmith.com/reference/widgets/table#server-side-pagination)。
{% endhint %}

获取数据后，您可以通过将其绑定到组件的属性来将值显示出来，如下所示。

```
{{ query_name.data }}
```

<figure><img src="../../../.gitbook/assets/image (69) (1).png" alt=""><figcaption></figcaption></figure>

#### 2、INSERT方式

使用`INSERT`语句向数据库表中添加行。

例如，假设您有一个名为 users 的表，其中包含`name`、`gender`和的列`phone`，并且您想要创建一条新记录。要收集记录数据，您可以构建一个名为“NewUserForm”的表单，其中包含：

* 一个名为“NameInput”的输入小部件，用于名称，
* 用于性别的名为“GenderSelect”的选择小部件。
* 一个名为“EmailInput”的电子邮件输入小部件，

填写完这些表单字段后，您可以将它们的值提取到您的查询中，如下所示：

```
INSERT INTO users
  (name, gender, email)
VALUES
  (
    {{ NewUserForm.data.NameInput }},
    {{ NewUserForm.data.GenderSelect }},
    {{ NewUserForm.data.EmailInput }}
  );

```

然后，通过Button 小部件的**onClick**事件运行此查询以将数据插入到您的数据库中。请务必添加一个回调来重新运行提取查询以刷新表格小部件中的数据。`onSuccess`

#### 3、UPDATE方式

使用`UPDATE`语句更改数据库中现有记录的值。

例如，假设您想更改表`email`中一条记录的值`users`。在您的 Table 小部件中，将`email`列设置为[**Editable**](https://docs.appsmith.com/reference/widgets/table/inline-editing#editable)。表格中应该会出现一个新的**保存/放弃按钮列。**

在表的属性窗格中，打开保存/放弃按钮列的列设置并设置按钮的**onClick**以运行`UPDATE`查询。请务必添加一个`onSuccess`回调，该回调会重新运行获取查询以在执行后刷新 Table 小部件中的数据。

如下所示配置您的查询，以将现有`email`条目设置为表中的更新值。

```
UPDATE users
  SET email = '{{Table1.updatedRow.email}}'
  WHERE id = {{ Table1.selectedRow.id}};
```

现在您可以编辑`email`Table 小部件中任何行的单元格，然后单击**Save**将您的更新发送到数据库。



#### 4、DELETE方式

使用`DELETE`语句从数据库中删除记录。

例如，要从表格小部件中删除现有行，请将按钮列添加到表格小部件并将其标记为“删除”。设置该按钮的**onClick**事件以运行`DELETE`如下查询：

```
DELETE FROM users WHERE id = {{ Table1.selectedRow.id }};
```

当用户单击该按钮时，该记录将从数据库表中删除。请务必`onSuccess`向删除查询添加一个回调，该回调会重新运行您的获取查询以刷新您的表小部件中的数据。

为避免意外删除记录，请考虑在[查询设置](https://docs.appsmith.com/core-concepts/data-access-and-binding/querying-a-database/query-settings)中启用“运行查询前请求确认”设置。



### 4、故障排除

如果遇到困难，可以参考[动作错误](../../../gu-zhang-pai-chu/dong-zuo-cuo-wu/)或者[MySQL错误](../../../gu-zhang-pai-chu/dong-zuo-cuo-wu/mysql-cuo-wu.md)寻求帮助。
