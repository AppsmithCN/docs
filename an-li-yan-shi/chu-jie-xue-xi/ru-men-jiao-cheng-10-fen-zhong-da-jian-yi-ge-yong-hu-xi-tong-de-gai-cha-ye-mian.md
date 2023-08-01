# 入门教程—10分钟搭建一个用户系统的改查页面

通过本次教程，能够先初步了解PagePlug的使用流程，后端可以通过直接连接数据源（API、DB），将任何的后端数据都变成了 JS 变量，并随意转换、并配置到前端任意的视图组件



## 1、创建新的应用

* 我们可以在工作区中，先创建一个桌面应用

<figure><img src="../../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

* 修改下本次应用的名称，例如：**运营部门用户管理系统**

<figure><img src="../../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>



## 2、连接数据库

* 在左下角数据源中，点击左侧的+号，新增一个数据源，本次案例演示用的是**PostgreSQL**

<figure><img src="../../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

* 填写相应的端口信息

{% hint style="info" %}
**主机地址**:`mockdb.internal.appsmith.com`\
**端口**:`5432`\
**数据库名称**:`users`\
**用户名**:`users`\
**密码**:`new-users-db-pass`
{% endhint %}

填写完后，我们可以点右下角的测试，看下填写信息是否有误（无误的话会提示连接成功）

<figure><img src="../../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

数据库连接成功后，点击保存，数据源就创建成功了

<figure><img src="../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

## 3、新建查询

* 点击新建查询按钮内，我们选择Select选项，用默认的语句

<figure><img src="../../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

* 点击运行，查询的内容生成出来了

<figure><img src="../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

我们可以在右侧选择通过什么组件展示数据，本次案例选择表格（Table）组件

<figure><img src="../../.gitbook/assets/image (23).png" alt=""><figcaption><p>数据内容就自动生成表格了</p></figcaption></figure>

{% hint style="warning" %}
数据是怎么来的？
{% endhint %}

在右侧数据那里，我们会发现通过\{{ \}}的形式，将查询Query1的数据，连接到了表格Table中

<figure><img src="../../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

## 4、搭建用户信息的查询窗口



* 我们可以在左侧组件栏中，拖入一个表单组件

<figure><img src="../../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

* 我们可以在表单组件里面，将文本（Text1）组件，并改名为：用户详细信息

<figure><img src="../../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

* 之后我们可以拖入一个输入框（input1）组件，用来获取表格内的信息

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

* 我们可以对input组件的布局做下调整（例如文本与输入框的位置、宽度大小等），并修改下文本的内容，例如修改为Name

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

* 我们可以在默认值那里，通过组件的方法，拿到表格当前的值，例如

```
{{Table1.selectedRow}}

//拿到Table组件当前行的值
```

<figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

那比如说，我想拿name的信息，就可以这样

```
{{Table1.selectedRow.name}}
```

<figure><img src="../../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

* 同样的，比如说我们想拿到Email的值，可以拖入一个input组件，同理处理

```
{{Table1.selectedRow.email}}
```

<figure><img src="../../.gitbook/assets/image (5) (2).png" alt=""><figcaption></figcaption></figure>

* 再比如说，我们想拿到用户图片的信息，我们可以拖入一个图片（Image）组件，同样的方法

```
{{Table1.selectedRow.image}}
```

<figure><img src="../../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

简单的查询页面就完成了

<figure><img src="../../.gitbook/assets/2023-07-18 115459.gif" alt=""><figcaption></figcaption></figure>



## 5、更改用户详细信息

* 我们可以对绑定的数据源，新建一个更新查询

<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

* 可以将下面SQL的更新命令复制到编辑器里面

```sql
UPDATE users 
SET name = {{Input1.text}}, 
email = {{Input2.text}}
WHERE id = {{Table1.selectedRow.id}}
```

{% hint style="danger" %}
注意：复制这段sql执行的时候，需要修改将\{{\}}内的组件名称与画布上的组件名称对应上
{% endhint %}

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

* 回到画布上，我们对表单组件内的提交按钮设置事件

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

* 修改按钮的文本为：更新；在事件中，我们选择执行查询Query2

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

可以对执行成功和执行失败配置对应的动作事件，如成功后，执行消息提醒

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

* 如果想对修改后的表格内容展示出来，我们可以重新执行下Query1，点击右上角的JS

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption><p>PagePlug处处皆可编写JS</p></figcaption></figure>

```javascript
{{Query2.run(() => {showAlert('成功','success'),Query1.run()} ,() => {})}}
```

<figure><img src="../../.gitbook/assets/image (1) (2).png" alt=""><figcaption></figcaption></figure>

10分钟的时间，其实就能快速完成一个用户系统的改查页面，快速满足业务的需要上线





## 6、演示拓展：通过数据库生成页面

{% hint style="info" %}
这是PagePlug的特点，可以通过数据库直接生成页面
{% endhint %}

* 点击左下角的查看所有数据源，可以看到我们刚刚绑定的数据库<mark style="color:red;">Untitled Datasource 1</mark>，点击生成新页面

<figure><img src="../../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

* 用户系统的查改系统就快速生成交付了

<figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>
