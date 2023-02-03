# 查询错误

该部分说明了常见的查询错误以及如何在 PagePlug 上解决这些错误。

### 1、查询/API 响应错误 <a href="#queryapi-response-errors" id="queryapi-response-errors"></a>

使用API或查询响应时，您可能会看到以下错误。

#### &#x20;   1.1执行失败，状态为5009 <a href="#execution-failed-with-status-5009" id="execution-failed-with-status-5009"></a>

您会看到查询/API 执行失败并生成错误响应：

{% hint style="info" %}
\<QUERY\_OR\_API\_NAME> action returned an error response. Response size exceeded the maximum supported size of \<SIZE\_SPECIFIED\_IN\_FILE> MB. Please use LIMIT to reduce the amount of data fetched.
{% endhint %}

&#x20;       **错误信息：**

{% hint style="info" %}
Response size exceeded the maximum supported size of \<SIZE\_SPECIFIED\_IN\_FILE> MB. Please use LIMIT to reduce the amount of data fetched.
{% endhint %}

&#x20;     **导致的原因：**

当 API/查询响应大小超过允许的最大限制**5 MB**或大小设置时，可能会导致错误响应。

![响应大于支持的大小](https://docs.appsmith.com/assets/images/Query-errors-response-size-larger-than-5MB-7f81fcc53bf43f787198a4dbc5ae6156.png)

![响应大于错误选项卡中显示的支持大小错误](https://docs.appsmith.com/assets/images/Query-errors-response-size-larger-than-5MB-errors-tab-847cba551b0ccb1f01a8a5b01661f63f.png)

&#x20;    **解决的方案：**

您可以通过执行以下操作之一来解决错误响应：

* 通过在查询中使用限制或为表启用分页来限制作为查询响应的一部分返回的数据。
* 要限制 API 的数据，您必须向其添加服务器端分页功能。
* 要更新最大允许限制，您可以仅为 Appsmith 的自托管实例修改环境变量。例如，要修改基于 docker 的安装的限制，请导航到该`docker.env`文件并将`APPSMITH_PLUGIN_MAX_RESPONSE_SIZE_MB`环境变量修改为所需的响应大小 (10 MB)。

```
APPSMITH_PLUGIN_MAX_RESPONSE_SIZE_MB=10
```

{% hint style="danger" %}
如果您找不到您要找的东西并且需要帮助调试错误，请在github上提问或者是在开源社区请教PagePlug静静
{% endhint %}



### 2、MongoDB名称不能为空 <a href="#mongodb-name-can-not-be-null" id="mongodb-name-can-not-be-null"></a>

尝试对 MongoDB 数据源运行查询时，您可能会遇到此错误。

&#x20;   **错误信息：**

错误消息可能以几种不同的方式出现。例如：

* 作为控制台中的错误响应：

{% hint style="info" %}
{ message: 'name can not be null', type: 'PLUGIN\_EXECUTION', subType: undefined }
{% endhint %}

* 作为文本通知：

{% hint style="info" %}
* Mongo is not correctly configured. Please fix the following and then re-run: \[Missing default database name.]
{% endhint %}

* 或者

{% hint style="info" %}
Missing default database name.
{% endhint %}

&#x20;  **导致的原因：**

此错误可能是由于**连接字符串 URI**字段中省略了数据库名称引起的。

&#x20;  &#x20;

&#x20;**解决方案：**

在数据源设置中找到您的**连接字符串 URI**，并验证数据库名称是否在主机名后面的字符串中。例如，如果您的数据库名称是`Movies`，它应该如下所示：

```
// Connection String URI

mongodb+srv://mockdb-admin:****@mockdb.kce5o.mongodb.net/movies?w=majority&retrywrites=true&authsource=admin&minpoolsize=0
```

在代码片段中，`mockdb.kce5o.mongodb.net/`是主机，`movies`是数据库名称，后面的项目`?`是可选参数。

![](https://docs.appsmith.com/assets/images/mongoerr\_dbname-d4c620a546103b082435e21d227c96d7.png)

{% hint style="danger" %}
如果您找不到您要找的东西并且需要帮助调试错误，请在github上提问或者是在开源社区请教PagePlug静静
{% endhint %}
