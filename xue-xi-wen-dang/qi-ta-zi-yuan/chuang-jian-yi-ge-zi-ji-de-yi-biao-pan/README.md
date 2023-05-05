# 创建一个自己的仪表盘

{% hint style="info" %}
Type\
⌘/\
for commands,\
/\
for inline commands.\
P
{% endhint %}



### 1、创建应用





### 2、绑定数据源

* 首先，单击`+`旁边的图标`Datasources`。
* 接下来，您将看到可以连接到的数据源选项列表，选择`PostgreSQL`

<figure><img src="../../../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>



* 选择**Postgres**并将数据源重命名为`Postgres Mock DB`.
* 接下来，使用以下详细信息连接数据源。

{% hint style="info" %}
**连接模式:** Read / Write

**主机地址:** mockdb.internal.appsmith.com

**端口:** 5432

**数据库名称:** yelp

**用户名:** yelp&#x20;

**密码:** that-annoying-yelper
{% endhint %}

<figure><img src="../../../.gitbook/assets/image (24) (1).png" alt=""><figcaption></figcaption></figure>

### 3、新建查询

* 我们可以对数据库新建一个查询，后续在页面中使用它

<figure><img src="../../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (26) (1).png" alt=""><figcaption></figcaption></figure>

* 可以将此查询命名为`getBusinessData`并单击选择。
* 输入以下查询，获取所有业务数据

{% hint style="info" %}
SELECT \* FROM yelp\_business;
{% endhint %}

<figure><img src="../../../.gitbook/assets/image (29) (1).png" alt=""><figcaption></figcaption></figure>

* 我们可以从右边选择一些组件，把数据自动导入展示，例如表单table

<figure><img src="../../../.gitbook/assets/image (18) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (2) (4).png" alt=""><figcaption><p>数据就自动导入到表单组件了</p></figcaption></figure>

* 或者我们可以怎么用呢？例如自己拖入一个表单组件，在数据这里添加下面内容

{% hint style="info" %}
\{{ getBusinessData.data \}}
{% endhint %}

<figure><img src="../../../.gitbook/assets/image (31) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
PagePlug任意地方，都可以写JS，让很多事情都变得简单便捷
{% endhint %}

### 4、拖拉组件构建UI

* 将表单拖入容器组件里面

<figure><img src="../../../.gitbook/assets/image (27) (2).png" alt=""><figcaption><p>容器的大小，可以在右侧高度那里调整</p></figcaption></figure>

* 在容器内拖入地图组件

{% hint style="info" %}
{ "lat": \{{Table1.selectedRow.latitude\}}, "long": \{{Table1.selectedRow.longitude\}} }
{% endhint %}



{% hint style="info" %}
\[ { "lat": \{{Table1.selectedRow.latitude\}}, "long": \{{Table1.selectedRow.longitude\}}, "title": \{{Table1.selectedRow.name\}} } ]
{% endhint %}
