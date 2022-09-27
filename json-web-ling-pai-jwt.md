# JSON Web 令牌 (JWT)

JSON Web Token (JWT) 是一种开放标准 ([RFC 7519](https://datatracker.ietf.org/doc/html/rfc7519)) 用于以 JSON 对象的形式在各​​方之间安全地传输信息。

**JSON Web 令牌** (JWT) 可以作为 OpenID Connect (OIDC)的一部分访问，仅在自托管实例的 \*\*\*\* **企业版** 中可用

## 何时使用 JSON Web 令牌？

以下是使用 JSON Web 令牌的一些常见场景：

> 如果您了解 JSON Web 令牌，请直接转到 [如何在 Appsmith 中使用 JSON?](https://docs.appsmith.com/getting-started/setup/instance-configuration/authentication/json-web-tokens-jwt#how-to-use-json-web-tokens-in-appsmith)

### 验证

对于经过身份验证的用户，每当用户请求访问资源或服务或路由时，应用程序都会以遵循 JWT 格式的访问令牌的形式传递信息。单点登录 (SSO) 通常使用 JWT 与位于相似域或其他域的不同系统进行通信。

### 信息交流

JSON Web 令牌是在不同应用程序之间传输信息的一种安全方式。JWT 也可以签名。令牌可以有一个与之关联的时间戳，一旦时间戳过期，您可以阻止过期令牌的信息交换。您还可以验证令牌的内容是否未被篡改。例如，使用公钥/私钥对，您可以确保发件人是授权的发件人。这为数据或信息交换提供了额外的安全层。

## JSON Web 令牌如何工作？

例如，您正在对用户进行身份验证。您的 SSO 提供者在成功验证时共享一个 JSON Web 令牌 (JWT)。

> 作为最佳实践，您应该只在需要的时候存储令牌。

每当用户请求访问资源时，用户代理应发送 JWT，通常在 Authorization 标头中使用 Bearer。

```
 Authorization: Bearer <followed by the token value>
```

服务器的验证机制将验证`Authorization`标头中的令牌并授予对资源的访问权限或允许用户执行操作。

> 发送令牌作为授权标头的一部分消除了通过 cookie 共享时通常面临的跨域资源共享 (CORS)。

## JSON Web 令牌结构

JSON Web Token 包含三个主要部分，用点 (.) 分隔 - 标头、有效负载和签名。

比如你的header是HEADER1，Payload是PAYLOAD1，Signature是SIGNATURE1，那么JWT结构就是：`HEADER1.PAYLOAD1.SIGNATURE1`

### 标题

JWT 标头存储有关 JWT 令牌类型和用于签名的算法（如 SHA256 或 RSA 等）的信息。

因此，标头表示为：

```
{

   “alg”:”HS256”,

   “typ”:”JWT”

}
```

这里 alg 代表用于签名的算法，typ 代表令牌类型。然后将 JSON 编码为 Base64Url 以形成 JSON Web 令牌的第一部分，即标头。

### 有效载荷

令牌的第二部分，有效负载，包括声明。声明是关于通常与用户和元数据相关联的实体的信息。有三种类型的声明 - 公开的、私有的和保留的。

#### 上市

如果您创建[公共声明](https://datatracker.ietf.org/doc/html/rfc7519#section-4.2)，则必须在 IANA JSON Web 令牌注册表中定义它们或将它们定义为具有抗冲突命名空间的 URI。

> 公开声明应得到发行人和消费​​者的验证和同意。

#### 私人的

相互通信的各方可能希望识别一些自定义声明。您可以在私有声明下定义这些自定义声明。这些声明既没有注册也没有公开。

> 公共/私有声明不应具有与保留声明相似的名称，因为它会破坏交换信息的系统之间的互操作性。

#### 注册的

一组非强制性但被视为推荐的预定义声明被定义为[已注册声明](https://datatracker.ietf.org/doc/html/rfc7519#section-4.1)。此类声明提供有用的信息，例如到期时间、发行人详细信息、目标受众等。

> 声明名称只有三个字符长，以确保 JWT 紧凑。

样本有效载荷可以是：

```
{

  “sub”: “SSOProvider”,

  “email_verified”: true,

  “updated_at”: 1646310160264

}
```

然后对有效负载进行编码以形成 Base64Url 并形成令牌的第二部分。

#### 签名

要创建签名，您必须对标头、有效负载、秘密进行编码，使用标头中定义的算法并对其进行签名。

例如，您正在使用 HMAC SHA-256(HS256) 算法。那么生成的签名如下：

```
 ​​HMACSHA256(

  base64UrlEncode(header) + "." +

  base64UrlEncode(payload),

  secret)
```

您可以使用签名来验证发送者的真实性，检查消息是否被篡改，并且可以使用私钥进行签名。

签名被编码为 Base64Url 并附加以形成完整的 JSON Web Token。

例如，带有标头、有效负载和签名的编码 JWT 可能如下所示：

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9**.**eyJzdWIiOiJTU09Qcm92aWRlciIsImVtYWlsX3ZlcmlmaWVkIjp0cnVlLCJ1cGRhdGVkX2F0IjoxNjQ2MzEwMTYwMjY0fQ**.**qUwYZqYbtfCjhODEEF9M6B3JFN4WtUSg37MixYVN1h0
```

您可以看到 JWT 的三个部分用点 (.) 分隔。

> 您可以使用 JWT 调试器对生成的 JWT 进行编码、解码或验证。

## 为什么使用 JSON Web 令牌？

使用 JWT 的主要好处是它更紧凑，因此尺寸更小。它是安全的，可以使用发行者和消费者之间的共享秘密。它使用 JSON 格式；几乎每种编程语言都有 JSON 解析器，因此您不必重新发明轮子。

## 如何在 Appsmith 中使用 JSON Web 令牌？

让我们举个例子。您已使用OpenID Connect 将单点登录 (SSO) 提供商与 Appsmith 集成。您正在使用 Appsmith 登录并使用您的 SSO 提供商来验证请求。

让我们仔细看看 Appsmith 的这种交互是如何发生的。

![](<.gitbook/assets/JSON Web 令牌（JWT）-图1.png>)

在上图中，您可以看到：

* 用户使用 Appsmith 请求登录。
* 在幕后，Appsmith 与 SSO 提供程序集成。
* SSO 提供者授权请求。
* SSO 提供程序为经过身份验证的用户生成令牌并与 Appsmith 共享。
* Appsmith 拥有可在平台上访问的令牌。您可以在 API 中传递它以提供对资源的访问或执行所需的操作。

### 代币类型

Appsmith 提供了两种类型的 JSON Web 令牌，您的应用程序可以与之集成：ID 令牌和访问令牌。

#### 身份令牌

ID 令牌是用户身份的签名保证，包含姓名、图片、电子邮件地址等基本信息。当用户成功登录时，会根据 Open ID Connect (OIDC) 规范共享一个 ID 令牌。

#### 如何在 Appsmith 上读取 ID 令牌？

一旦 SSO 提供商成功验证用户身份，ID 令牌就可以在 Appsmith 平台上使用。

> Appsmith`idToken`在客户端公开参数。因此，它可以嵌入到您希望在 JavaScript 函数、API 或查询中执行的任何操作中。

您可以使用小胡子符号 \{{\}} 在 API/查询中读取 id 令牌的值。

```
{{appsmith.user.idToken}}
```

#### 访问令牌

访问令牌是以声明的形式存储有关实体的信息的对象。当您想使用基于令牌的身份验证时，访问令牌会派上用场。访问令牌是自包含的。您不必调用服务器来验证令牌。

#### 如何在 Appsmith 上读取访问令牌？

通过 SSO 提供者成功进行用户身份验证后，您可以在 Appsmith 上使用访问令牌。访问令牌可作为环境变量使用。

> 根据安全规范，客户端无法访问环境变量。

环境变量`APPSMITH_USER_OAUTH2_ACCESS_TOKEN`存储访问令牌。您可以通过在尖括号之间使用访问令牌来读取它的值`<<>>.`

`<<APPSMITH_USER_OAUTH2_ACCESS_TOKEN >>`

借助 Appsmith 上可用的 JSON Web 令牌，您可以在 Appsmith 与您的应用程序或 API 之间安全地交换数据或信息。
