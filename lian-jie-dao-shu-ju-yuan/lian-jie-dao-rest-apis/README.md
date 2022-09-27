# 连接到 REST APIs

如果您的 API 受到身份验证机制的保护,这需要一组标准的标头或参数,这些标头或参数需要随每个请求一起发送,您可以将它们保存在一个公共数据源中,以便在每个请求中重用,称为 Authenticated API.

### 创建经过身份验证的 API <a href="#e5-88-9b-e5-bb-ba-e7-bb-8f-e8-bf-87-e8-ba-ab-e4-bb-bd-e9-aa-8c-e8-af-81-e7-9a-84-api" id="e5-88-9b-e5-bb-ba-e7-bb-8f-e8-bf-87-e8-ba-ab-e4-bb-bd-e9-aa-8c-e8-af-81-e7-9a-84-api"></a>

导航到 **Explorer** → 向下滚动到 **Datasources** → 单击 **(+)** 符号 → 单击 **Authenticated API**.

{% embed url="https://youtu.be/Uy7ZDviGbtM" %}

您将被重定向到创建数据源页面,如下所示:

![](<../../.gitbook/assets/连接到REST API.png>)

### 配置 <a href="#e9-85-8d-e7-bd-ae" id="e9-85-8d-e7-bd-ae"></a>

您可以按如下方式配置数据源:

#### 姓名 <a href="#e5-a7-93-e5-90-8d" id="e5-a7-93-e5-90-8d"></a>

默认情况下,Appsmith 为创建的数据源提供运行序列.您可以单击它旁边的铅笔图标来编辑数据源的名称.

> 建议您为 Authenticated API 数据源指定一个有意义的名称.

#### 网址 <a href="#e7-bd-91-e5-9d-80" id="e7-bd-91-e5-9d-80"></a>

使用此字段添加您要访问的 API URL.例如,我想访问 Appsmith 的模拟 API,为此,我将提供 URL 为 [https://mock-api.appsmith.com](https://mock-api.appsmith.com/)&#x20;

#### 标头 <a href="#e6-a0-87-e5-a4-b4" id="e6-a0-87-e5-a4-b4"></a>

您可以添加一个或多个您希望随请求一起发送的标头详细信息,以访问您已集成的 API.

#### 查询参数 <a href="#e6-9f-a5-e8-af-a2-e5-8f-82-e6-95-b0" id="e6-9f-a5-e8-af-a2-e5-8f-82-e6-95-b0"></a>

您可以将一个或多个查询参数添加到您集成的 API 作为请求的一部分.

#### 发送 Appsmith 签名标头 <a href="#e5-8f-91-e9-80-81-appsmith-e7-ad-be-e5-90-8d-e6-a0-87-e5-a4-b4" id="e5-8f-91-e9-80-81-appsmith-e7-ad-be-e5-90-8d-e6-a0-87-e5-a4-b4"></a>

当您想要确保传入请求来自 Appsmith 时,您可以 `Send Appsmith Signature Header` 通过选择 **Yes** 来启用. 您将看到一个新字段 - **Session Details Signature Key** 以提供签名密钥.

![](<../../.gitbook/assets/连接到 REST API 图2.png>)

#### 认证类型 <a href="#e8-ae-a4-e8-af-81-e7-b1-bb-e5-9e-8b" id="e8-ae-a4-e8-af-81-e7-b1-bb-e5-9e-8b"></a>

您可以使用 Appsmith 上提供的协议为[ REST API](https://docs.appsmith.com/core-concepts/connecting-to-data-sources/authentication/authentication-type) 定义身份验证类型

### 安全 <a href="#e5-ae-89-e5-85-a8" id="e5-ae-89-e5-85-a8"></a>

Appsmith 安全地加密您的所有身份验证凭据并安全地存储它们.Appsmith 也不存储从您的数据源返回的任何数据,仅充当代理层来编排 API/查询调用.由于 Appsmith 是一个开源框架,您可以 [将其部署到本地](https://docs.appsmith.com/getting-started/setup), 并对其进行审核以确保您的所有数据都不会离开您的 VPC.

### 智能 JSON 替换 <a href="#e6-99-ba-e8-83-bd-json-e6-9b-bf-e6-8d-a2" id="e6-99-ba-e8-83-bd-json-e6-9b-bf-e6-8d-a2"></a>

智能 JSON 替换功能允许 Appsmith 对请求正文中的字段值动态执行类型转换.下面的视频说明了如何使用此功能:

{% embed url="https://youtu.be/-Z3y-pdNhXc" %}
