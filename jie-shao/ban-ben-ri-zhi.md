# 版本日志

### 2023.3.21&#x20;

{% hint style="info" %}
**V1.9.15版本镜像已更新**
{% endhint %}

### 1、新增功能🏅

* 支持引入第三方JS库

{% hint style="info" %}
1、可以将你需要工具库的URL 粘贴到Pageplug中来使用

2、可以在资源管理器中查看所有已安装的库。
{% endhint %}

<figure><img src="../.gitbook/assets/image (10) (5).png" alt=""><figcaption></figcaption></figure>

* #### &#x20;新增iframe嵌入选项

{% hint style="info" %}
1、添加用于嵌入 iframe 的代码片段

2、`ssoTrigger`结合使用查询参数对程序借用信任`embed=true`

`3、`登录嵌入应用程序的用户现在可以自动看到PagePlug 应用程序
{% endhint %}

<figure><img src="../.gitbook/assets/image (4) (1) (1).png" alt=""><figcaption></figcaption></figure>

* **新增数据查看层**

{% hint style="info" %}
目前仅适用于api.data
{% endhint %}

<figure><img src="../.gitbook/assets/image (10) (2).png" alt=""><figcaption></figcaption></figure>

* **新增值查看窗口**

{% hint style="info" %}
1、只有在组件中有代码或输入存在验证错误时，它才会显示

2、窗口支持拖拽，放在你喜欢的任意位置

3、窗格的默认状态更加清晰，带有扩展部分的选项
{% endhint %}

<figure><img src="../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### 2、功能优化💪

* 底层升级：

mongo 4.4 -> 5.0.14

&#x20;jdk 11 -> 17&#x20;

Spring Boot 2.7 -> 3.0.1 3



* ANTD5升级，让 formily 支持设置主题，整体样式方案更统一✅
* 嵌入个人的应用程序中提供 SSO，自动高度改进等
* `storeValue`操作现在被批处理以获得更好的性能
* 容器现在会随着其中组件的大小自动增长和收缩。当你拖动其他组件上下移动时，容器还会实时更改大小
* 查询字段、输入和数字输入可以响应了
* 引用一个类似实体`selectedTab`或在 JavaScript 函数中声明的另一个属性，其名称是计算的，而不是静态的，不会再抛出错误的 linting 错误
* 商业版ODIC功能优化，修复 OIDC 对 Spring、AWS Cognito 的依赖性



### 3、修复已知bug🐮

* 对gitee、github上的issue问题进行优化处理，欢迎继续在社区提交issue
* 修复用户的浏览器导航问题，可以使用浏览器后退/前进按钮在 PagePlug上穿越旧环境
* 修复表格在添加绑定到列名称时中断的问题
* 修复列表组件嵌套限制为最多 3 层
* 修复在 API 标头中包含与换行符的绑定
* 修复在任何 JS 对象中引用其中任何一个时，会自动完成现在会显示所有 JS 对象的所有函数。
* 修复商业版用户现在将在注册并激活他们的实例后看到他们应该看到的应用程序，而不必从主屏幕上找出他们想要的应用程序
* 将 Nginx 限制增加到 150 MB 以允许 100 MB Base 64 编码文件
* 修复允许 MsSQL 插件连接 ssl 加密



### 4、提醒❗️

1、因为appsmith新版升级了MongoDB版本，所以PagePlug从V1.8版本升级到V1.9前，需要将实例镜像升级到处理数据兼容性的中间版本，可以进行如下操作：



* 1、关停PagePlug实例，在Docker -compose.yml所在目录下输入docker -compose down
* 2、修改docker -compose.yml镜像为appsmith兼容版本appsmith/appsmith-ce:v1.9.2（PagePlug和appsmith是兼容的），然后docker -compose up -d启动容器

<figure><img src="../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>

* 3、在容器启动成功后，再次关停，将镜像替换回cloudtogouser/pageplug-ce ，然后启动

<figure><img src="../.gitbook/assets/image (2) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

2、迁移教程

旧版本迁移到新版本的教程，可以查看：[迁移教程](../xue-xi-wen-dang/ban-ben-qian-yi-jiao-cheng.md)



欢迎社区的同学们在gitee及github上对pageplug的使用给我们提issue哈🥳
