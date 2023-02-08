# Airtable

在 PagePlug 上，与任何数据源（包括 Airtable）建立连接都非常简单。通过此集成，您可以使用基于 PagePlug 构建的自定义 UI 执行不同的操作，只需最少的配置。

### 1、创建

<figure><img src="../../.gitbook/assets/image (67).png" alt=""><figcaption><p>点击+号，在API下选择Airtable</p></figcaption></figure>

### 2、连接

如下图所示配置 Airtable 数据源，Papgplug 允许您从可用的身份验证类型中进行选择，以与 Airtable 数据库集成：：

<figure><img src="../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

* **API KEY：**[Airtable API](https://support.airtable.com/hc/en-us/articles/219046777-How-do-I-get-my-API-key-)密钥允许您使用公共 API 在您在 Airtable 中有权访问的[基础](https://support.airtable.com/hc/en-us/articles/202576419-Introduction-to-Airtable-bases)上创建、获取、更新和删除记录。
* **Bearer Token：**是 OAuth 2.0 使用的主要Token

{% hint style="info" %}
API 限制为每秒 5 个请求。如果超过此速率，您将收到 429 状态代码，并且需要等待 30 秒，后续请求才会成功。
{% endhint %}

### **3、API**

<figure><img src="../../.gitbook/assets/image (63).png" alt=""><figcaption></figcaption></figure>
