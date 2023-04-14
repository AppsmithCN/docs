# MongoDB

本文档介绍如何将MongoDB 数据库和 PagePlug 之间建立连接，应用可以读取跟写入数据。



### 1、创建MongoDB数据库

要添加 MongoDB 数据源，**请点击左下角数据源旁边的( + ) 号，** 在数据库页面中选择MongoDB

<figure><img src="../../../.gitbook/assets/image (114).png" alt=""><figcaption></figcaption></figure>

### 2、连接MongoDB

MongoDB支持URL或者主机地址的方式连接

<figure><img src="../../../.gitbook/assets/image (103).png" alt=""><figcaption></figcaption></figure>

#### 2.1 URL的方式

* 标准连接字符串的格式

你可以通过标准方式使用 Mongo 的URL地址来选择连接

<figure><img src="../../../.gitbook/assets/image (115).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
标准格式：

mongodb://username:password@host:port/databaseName/
{% endhint %}

{% hint style="info" %}
示例：

mongodb://21c342e1eeee.c.methodot.com:34108/test
{% endhint %}

映射URL字段解释：

* **`mongodb://`** 标准连接格式的前缀
* **`username ：`** 连接MongoDB数据库的用户名
* **`password：`** 连接的MongoDB数据库的密码
* **`host ：`**连接MongoDB数据库的主机地址
* **`port：`**运行 MongoDB数据库的端口号
* **`databaseName：`**需要连接的MongoDB数据库的库名

{% hint style="danger" %}
提示

* 你可以在连接字符串中添加以逗号分隔的多个主机和端口详细信息，以同一用户的方式进行连接。
* 如果用户名或密码包含使用[百分比编码](https://www.rfc-editor.org/rfc/rfc3986#section-2.1)**`(: /? # [ ] @)`**`,需要`转换这些字符。
* 必须为DatabaseName字段提供一个值，查询将针对它执行。
{% endhint %}

* 域名服务种子列表格式

DNS 种子列表格式是另一种连接到 MongoDB 的方式，PagePlug支持这种方式。

它涉及使用域名服务 (DNS) 种子列表的标准格式，这需要连接字符串以 `mongodb+srv://` 为前缀。`+srv` 前缀用于指示主机名与 DNS SRV 相关联。

下面是 DNS 种子列表格式如何表示的示例：

{% hint style="info" %}
标准格式：

mongodb+srv://username:password@host:port/databaseName
{% endhint %}

{% hint style="danger" %}
提示

* 使用`+srv`自动将 TLS 或 SSL 选项设置为 true。如果您希望关闭 TLS 或 SSL 选项，`tls/ssl=false`请添加在查询字符串中。
* 如果用户名或密码包含使用[百分比编码](https://www.rfc-editor.org/rfc/rfc3986#section-2.1)**`(: /? # [ ] @)`**`,需要`转换这些字符。
{% endhint %}

#### 2.2主机地址的方式连接

<figure><img src="../../../.gitbook/assets/image (55).png" alt=""><figcaption></figcaption></figure>

* **连接模式**：选择在建立与数据库的连接时授予PagePlug的权限。两种可用模式是：只读模式、读取/写入模式
* **主机地址**：提供数据库服务器的主机名或 IP 地址。
* **端口**：提供连接到数据库的端口。如果不指定端口的情况下，PagePlug会尝试连接到端口**`27017`**。
* **数据库名称：**提供数据库的名称
* **身份认证**：填写连接你数据库的用户名和密码（如果无需用户名和密码验证，这里请留空且你的数据库必须接受这样的方式连接）
* **SSL模式：**支持默认、已启用、已禁用模式来设置您的查询是否使用 SSL 连接

{% hint style="info" %}
如果你想连接自己本地的数据库，你可以用ngrok来穿透。有关详细信息，请参阅如何连接到 PagePlug 上的本地数据库。
{% endhint %}
