# 安全

## 1、PagePlug会存储我的数据吗 <a href="#does-appsmith-store-my-data" id="does-appsmith-store-my-data"></a>

PagePlug不会存储从 API 端点或数据库查询返回的任何数据，PagePlug仅充当代理层。当您查询数据库/API端点时，PagePlug服务器仅在将请求转发到后端之前附加敏感凭据。它不会向浏览器公开敏感凭据，因为这可能会导致安全漏洞，路由可确保您的系统和数据的安全。



## 2、PagePlug所做的安全措施

PagePlug应用程序是安全的，我们对此做了相关的安全措施：

* 所有敏感凭据（例如数据库凭据）均使用[AES-256 加密](https://en.wikipedia.org/wiki/Advanced\_Encryption\_Standard)进行加密。私有化部署PagePlug的应用都通过配置唯一的**salt**和密码值来确保[静态数据的](https://en.wikipedia.org/wiki/Data\_at\_rest)安全性。
* [对于私有化部署的，我们支持在安装过程中通过LetsEncrypt](https://letsencrypt.org/)设置[SSL](https://en.wikipedia.org/wiki/Public\_key\_certificate)证书的功能。
* PagePlug在企业内部的访问可以通过[双因素身份验证系统](https://en.wikipedia.org/wiki/Help:Two-factor\_authentication)、单点登录、权限管理、审计日志进行控制；对于系统登录安全，支持更好的防暴力破解

{% hint style="info" %}
"salt"是指在加密密码时添加的一段随机字符串。这个随机字符串会在加密过程中被与原始密码组合后进行哈希运算，从而增加密码的强度和安全性，使得相同的密码在加密后得到的哈希值也会因为salt的不同而产生差异，增加了破解密码的难度。
{% endhint %}

{% hint style="info" %}
防暴力破解、单点登录、权限管理、审计日志功能仅在商业版中支持
{% endhint %}

## 3、安全地使用查询和调用API

PagePlug的后端系统在响应API调用或执行任何查询时不存储任何数据。我们对此做了相关的安全措施：

* PagePlug的后端系统不会存储有关查询响应或用户输入的任何信息。PagePlug**仅**充当代理，绝不会在 PagePlug的数据存储中记录或存储私人/机密数据。
* 为了保护应用程序，使用户无法推断执行的查询 - PagePlug存储查询配置并确保 SQL 查询正文或自定义 API的URL 永远不会在`view`模式下暴露给客户端。
* 为了避免 SQL 注入，所有 SQL 查询都默认启用预处理语句。



## 4、安全的执行JavaScript

PagePlug中编写的 JavaScript 代码仅在客户端上执行，用户可以检查站点并在浏览器中查看代码。

该代码会存储在 MongoDB 数据库中，PagePlug使用该数据库来存储所有其他应用程序配置。为确保所有数据安全，请仔细阅读以下内容：

{% hint style="danger" %}
我们建议你**不要以**纯文本形式对 JavaScript 对象中的敏感密钥、凭据或其他敏感信息进行硬编码。
{% endhint %}

{% hint style="info" %}
你可以向**API**或**数据源配置**添加**机密信息**，因为它们**不会在视图模式**下公开。您可以在**编辑模式**下更新**机密信息**，但在**查看**或**编辑**配置时**无法**查看现有**机密信息。**
{% endhint %}

* 当您将应用程序同步到 git 仓库时，JavaScript 代码也会同步并作为 JavaScript 文件存储在仓库中。因此，我们建议在处理 PagePlug上编写的 JavaScript 代码时遵循标准最佳实践。
* 在编写 JavaScript 代码时，我们**不会**直接向用户公开 DOM API，但我们通过PagePlug上提供的`setInterval()、clearInterval()`全局操作支持一些功能。
* PagePlug不允许某些操作，例如`Fetch`. 您无法直接从 JavaScript 代码调用外部 API。但是，您可以在  PagePlug上添加 API 并使用它来请求、读取数据或操作来自外部 API 的响应。
* 不推荐使用`storeValue`函数存储敏感信息，因为数据存储在浏览器的本地存储中并且可以读取。
