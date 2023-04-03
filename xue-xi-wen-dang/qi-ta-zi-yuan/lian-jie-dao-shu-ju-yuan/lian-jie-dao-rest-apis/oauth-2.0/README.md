# OAuth 2.0

开放式身份验证 (OAuth) 是一种开放式标准授权协议,允许您在服务之间共享信息,而无需解除或交换您的密码.它是开发人员广泛使用的安全交换信息的标准,因此提供对应用程序的**安全指定访问** .例如,您可以告诉 GitHub 授予 Appsmith 以您的名义合并或创建拉取请求的权限,而无需共享您的密码.因此,您可以灵活地在不暴露密码的情况下允许应用程序之间的交互.

通过使用 OAuth,您可以最大程度地降低安全风险.它确保即使关联的应用程序被破坏,您的密码也是安全的,因为它从未被暴露.

### OAuth 2.0 是如何工作的? <a href="#oauth-20-e6-98-af-e5-a6-82-e4-bd-95-e5-b7-a5-e4-bd-9c-e7-9a-84" id="oauth-20-e6-98-af-e5-a6-82-e4-bd-95-e5-b7-a5-e4-bd-9c-e7-9a-84"></a>

OAuth 2.0 是关于授权的,它要求管理访问的权限. [OAuth2.0](https://oauth.net/2/) 是 OAuth 1.0 的简化重新设计版本. `OAuth 2.0` 更快、更容易实施和使用.

OAuth 2.0 工作流程中有四个主要参与者：资源所有者、客户端、授权服务器和资源服务器.使用 OAuth 2.0 工作流程,作为**用户**或**系统的资源所有者**希望授权**客户端**访问可使用访问令牌访问的受保护资源.客户端向\*\*授权服务器请求访问令牌.\*\*客户端使用访问令牌并从资源服务器请求访问.资源服务器验证访问令牌并返回请求的资源.

例如,John（**资源所有者**）希望 Notion（**客户端**）代表他在 Twitter 上发布推文.Twitter（**授权和资源服务器**）为 Notion 生成一个密钥和一个秘密来完成这项工作.Notion 使用密钥和秘密来创建令牌并代表 John 发布推文.

> OAuth 2.0 不向后兼容.如果您的应用是 OAuth 1.0 或 1.1,您将无法使用 OAuth 2.0 进行集成.

### 身份验证类型 - OAuth 2.0 <a href="#e8-ba-ab-e4-bb-bd-e9-aa-8c-e8-af-81-e7-b1-bb-e5-9e-8b-oauth-20" id="e8-ba-ab-e4-bb-bd-e9-aa-8c-e8-af-81-e7-b1-bb-e5-9e-8b-oauth-20"></a>

对于 OAuth 2.0 集成, `OAuth 2.0` 请从可用选项中进行选择.

![](<../../../../../.gitbook/assets/OAuth 2.0 图1.png>)

### 认证类型 <a href="#e8-ae-a4-e8-af-81-e7-b1-bb-e5-9e-8b" id="e8-ae-a4-e8-af-81-e7-b1-bb-e5-9e-8b"></a>

您可以使用 Appsmith 上的 Authenticated API 连接到您的 OAuth 2.0 API.您选择身份验证类型为 OAuth 2.0.您可以在下面的屏幕截图中看到,您有以下可用的授权类型可供选择.

![](<../../../../../.gitbook/assets/OAuth 2.0 图2.png>)

#### 资助类型 <a href="#e8-b5-84-e5-8a-a9-e7-b1-bb-e5-9e-8b" id="e8-b5-84-e5-8a-a9-e7-b1-bb-e5-9e-8b"></a>

授权授予类型是所有者授权的安全表示,以换取访问令牌.

{% embed url="https://youtu.be/NOpmWnQuwwQ" %}

对于 Appsmith 上的 OAuth 2.0,您可以使用以下授权类型与您的 API 进行通信.导航到以下授权类型以了解其特定配置.

[授权码](shou-quan-ma.md)

[客户凭证](ke-hu-ping-zheng.md)