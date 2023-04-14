# PostgreSQL

本文档介绍如何将PostgreSQL 数据库和 PagePlug 之间建立连接，应用可以读取跟写入数据。



### 1、创建PostgreSQL

要添加 PostgreSQL 数据源，**请点击左下角数据源旁边的( + ) 号，** 在数据库页面中选择PostgreSQL

<figure><img src="../../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

### 2、连接PostgreSQL

<figure><img src="../../../.gitbook/assets/image (113).png" alt=""><figcaption></figcaption></figure>

* **连接模式**：选择在建立与数据库的连接时授予PagePlug的权限。两种可用模式是：只读模式、读取/写入模式
* **主机地址**：提供数据库服务器的主机名或 IP 地址。
* **端口**：提供连接到数据库的端口。默认情况下，PagePlug会尝试连接到端口`5432`。
* **数据库名称：**提供数据库的名称
* **身份认证**：填写连接你数据库的用户名和密码
* **SSL模式：**支持Default、Require、Disable、Prefer、Allow的模式来设置您的查询是否使用 SSL 连接

{% hint style="info" %}
如果你想连接自己本地的数据库，你可以用ngrok来穿透。有关详细信息，请参阅如何连接到 PagePlug 上的本地数据库。
{% endhint %}

### 3、创建PostgreSQL查询

你可以通过选择PostgreSQL数据源下的表来<mark style="color:red;">**新建查询，**</mark>支持Select、INSERT、UPDATE、DELETE四种方式



<figure><img src="../../../.gitbook/assets/image (104).png" alt=""><figcaption></figcaption></figure>

[可以使用标准SQL 语法](https://www.postgresql.org/docs/12/index.html)查询 PostgreSQL 数据库。所有 PostgreSQL 查询都返回一个对象数组，其中每个对象都是查询返回的一行，对象中的每个属性都是一列。



#### 1、INSERT方式

insert 子句用于将一行或多行插入到数据库表中。

例如，您有一个名为 users 的表，其中包含`name`、`email`和 的列`phone`。如果您想直接从 UI 将数据插入数据库表，您可以使用输入或选择小部件，如下所示：

```
INSERT INTO users
  (name, gender, email)
VALUES
  (
    {{ nameInput.text }},
    {{ genderDropdown.selectedOptionValue }},
    {{ emailInput.text }}
  );

```

**然后，您可以在“提交”按钮的onClick**事件上调用此查询，以将数据插入到数据库表中。

#### 2、UPDATE方式 <a href="#update-data" id="update-data"></a>

使用更新查询，您可以过滤或删除属于某个类型的任何字段。例如，如果您想更改用户表中的电子邮件 ID，您可以向表小部件添加一个更新列并将其列类型更改为按钮。

设置确认按钮的 onClick 事件以执行更新查询，并更改记录部分以使用输入小部件的文本更新所选行的字段。

```
UPDATE users
  SET email = '{{emailInput.text}}'
  WHERE id = {{ Table1.selectedRow.id}};
```

**在“更新”按钮的onClick**事件上运行此查询，以使用在小部件中输入的新值修改所选行的字段。

#### 3、DELETE方式 <a href="#delete-data" id="delete-data"></a>

删除记录命令从数据库中删除特定记录。

例如，假设您有一个名为 users 的表，其中包含 id、name、email 和 phone 列。如果要从此表中删除特定行，

* 您可以将“删除”列添加到表属性并将其类型设置为按钮。
* 然后，您可以设置删除按钮的 onClick 属性来执行删除查询，从数据库表中删除选定的行。

您可以将查询更改为：

```
DELETE FROM users WHERE id = {{Table1.selectedRow.id}};
```

