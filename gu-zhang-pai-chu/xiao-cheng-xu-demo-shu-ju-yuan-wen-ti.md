# 小程序demo数据源问题

## 一、行云严选的小程序demo ，为什么导入之后接口报错

目前的demo的后台采用的是开源小商城项目，详情参考[商城项目地址](https://github.com/linlinjava/litemall)&#x20;

{% hint style="info" %}
目前访问失败，大概率是由于demo数据中配置的数据源是很早的，之前部署的那套litemall应用已经被回收了，所以下面介绍，**如何重新搭建一套可访问的litemall**
{% endhint %}

### ⭐介绍

整个后台应用，包含一个java和一个mysql，这里我们使用了[<mark style="color:blue;">**Methodot在线开发平台**</mark>](https://methodot.com/)搭建并部署一个商城后台，最后拿到新的**接口访问地址**，更换”行云严选“低代码应用中，旧的数据源地址。

> 基本流程：
>
> \-> 新建架构图，其中新建组件，包含两个镜像组件，一个配置java镜像，一个mysql镜像
>
> \-> 使用配置好的架构图，发布应用，发布成功后，会得到java服务的访问地址

### ⭐开始

1. 登录[<mark style="color:blue;">Methodot</mark>](https://methodot.com/)，进入应用工厂，点击“创建新项目”，选择“微服务”类型

<figure><img src="../.gitbook/assets/image (14) (1) (2).png" alt=""><figcaption></figcaption></figure>

2. 填写项目名称和描述，点击“创建”

<figure><img src="../.gitbook/assets/image (13) (3) (1).png" alt=""><figcaption></figcaption></figure>

3. 进入到架构图编排页面，需要从左侧，拖拽两个“镜像”类型组件

✔️ 第一步，选择组件：修改为更直观的命名

* java组件
  * 名称：litemall-java
* mysql组件
  * 名称：litemall-mysql

✔️ 第二步，发现镜像：镜像地址在“<mark style="color:purple;">行云趣码本地集群</mark>”，输入框中搜索关键字`litemall`，会查到两个镜像地

* java 的镜像tag选择：20220822
* mysql的镜像tag选择：8.0.27

> registry.local/appsmith/litemall:20220822
>
> registry.local/appsmith/litemall-mysql:8.0.27

✔️ 第三步，配置组件：

*   **网络服务**

    * java组件：配置8080端口
    * mysql组件：配置3306端口


* **高级配置 -> 环境变量**
  * mysql组件：环境变量<mark style="color:blue;">MYSQL\_ROOT\_PASSWORD</mark> 设置为 `123456`
  * java组件：后面步骤中配置

✔️ 第四步，连接mysql和java组件,会弹窗提示新增一个组件参数，名称修改为`mysql`

<figure><img src="../.gitbook/assets/image (3) (3) (1).png" alt=""><figcaption></figcaption></figure>

✔️ 第五步，双击 “litemall-java”组件，设置环境变量

* **高级配置 -> 环境变量**

环境变量<mark style="color:blue;">SPRING\_DATASOURCE\_DRUID\_URL</mark> 设置为

<pre class="language-bash" data-overflow="wrap"><code class="lang-bash">jdbc:mysql://<a data-footnote-ref href="#user-content-fn-1">mysql</a>:3306/litemall?useUnicode=true&#x26;characterEncoding=UTF-8&#x26;serverTimezone=Asia/Shanghai&#x26;allowPublicKeyRetrieval=true&#x26;verifyServerCertificate=false&#x26;useSSL=false
</code></pre>

{% hint style="warning" %}
其中👆第二个mysql字符串，替换成上面“**组件参数**”部分的mysql参数引用（输入<mark style="color:purple;">@</mark>字符可自动关联选项），展示效果如下
{% endhint %}

<figure><img src="../.gitbook/assets/image (9) (1) (2).png" alt=""><figcaption></figcaption></figure>

✔️ 最终保证两个组件的配置信息如下👇

* java组件

<figure><img src="../.gitbook/assets/image (11) (1).png" alt=""><figcaption></figcaption></figure>

* mysql组件

<figure><img src="../.gitbook/assets/image (1) (4).png" alt=""><figcaption></figcaption></figure>



4. 右上角“保存”架构图，自动刷新页面后，点击右上角“发布”按钮，进入发布配置页面

直接使用默认的配置，不需要做任何修改，直接拖到页面最下方，<mark style="color:purple;">点击左下角的“发布”按钮</mark>

5. 提示发布成功之后，进入应用配置，查看接口地址

<figure><img src="../.gitbook/assets/image (5) (1) (1) (2).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (8) (2).png" alt=""><figcaption></figcaption></figure>

拿到已经部署好的服务地址，可以替换您的“行云严选”小程序demo中的数据源前缀了

<figure><img src="../.gitbook/assets/image (12) (2).png" alt=""><figcaption></figcaption></figure>

数据源只需要修改保存一次，使用了本数据源的api接口会自动同步修改，接口运行成功，预览试试吧👻

<figure><img src="../.gitbook/assets/image (2) (1) (2).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
有更多改造需求，可自行拉取 litemall开源项目深度改造

另外，平台上的搭建或者发布过程有什么问题，可以联系[Methodot](https://methodot.com/) 的nina反馈👇
{% endhint %}

<figure><img src="../.gitbook/assets/image (10) (1) (1).png" alt=""><figcaption></figcaption></figure>

[^1]: 这里需要替换成引用参数
