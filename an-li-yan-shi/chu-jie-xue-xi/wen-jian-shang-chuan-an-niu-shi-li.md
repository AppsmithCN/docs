# 文件上传按钮示例

本次案例需要使用到如下组件：

1、PagePlug的文件上传组件

2、自己的文件服务器（如果没有的话，可以使用methodot的http文件服务器）

本次案例演示将使用的是methodot的http文件服务器



### 1、部署一个http服务器

在methodot的应用商店部署一个http服务器商品

<figure><img src="../../.gitbook/assets/image (14) (3).png" alt=""><figcaption></figcaption></figure>

部署成功后会有一个url地址

<figure><img src="../../.gitbook/assets/image (5) (1) (2).png" alt=""><figcaption></figcaption></figure>

### 2、在Pageplug画布中拖入一个文件上传组件

<figure><img src="../../.gitbook/assets/image (2) (2).png" alt=""><figcaption></figcaption></figure>

### 3、在PagePlug新建一个api

<figure><img src="../../.gitbook/assets/image (16) (1).png" alt=""><figcaption></figcaption></figure>

### 4、编辑api

将在methodot上创建的url地址复制到输入框内，并修改类型。在请求体内输入对应的健、值

<figure><img src="../../.gitbook/assets/image (15) (3).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
1、get换成post请求

2、在请求体中，选择Multipart\_form\_data

3、键：file

4、选择File

5、值：\{{FilePicker1.files\[0]\}}
{% endhint %}



### 5、对组件进行绑定

<figure><img src="../../.gitbook/assets/image (9) (4).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
1、支持文件类型：选择任意文件类型

2、数据格式：Binary

3、事件：执行查询——选择“http\_file”api——消息提醒——提示消息：yes——提示类型：成功（后续动作可自行发挥～～）
{% endhint %}

<figure><img src="../../.gitbook/assets/image (7) (2).png" alt=""><figcaption></figcaption></figure>

### 6、可以在http服务器上查看下自己上传的文件

<figure><img src="../../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>
