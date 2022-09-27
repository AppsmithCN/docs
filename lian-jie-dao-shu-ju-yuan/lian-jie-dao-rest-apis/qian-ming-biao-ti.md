# 签名标题

这是一个可以在 REST 数据源上启用的选项.启用后,我们还需要用户输入签名机密（至少 32 个字符的字符串）.启用此选项的效果是,对该数据源进行的每个 API 调用都将包含一个附加标头 `X-Appsmith-Signature`, 其值是使用用户提供的机密签名的 JWT.以下是此签名的构造方式、JWT 包含的内容以及此标头对用户的意义的详细信息.

### 启用标题 <a href="#e5-90-af-e7-94-a8-e6-a0-87-e9-a2-98" id="e5-90-af-e7-94-a8-e6-a0-87-e9-a2-98"></a>

为特定 REST 数据源启用签名标头有两个步骤:

1. 设置 `Send Appsmith signature header` 为 `Yes`.
2. 设置 `Session Details Signature Key` 为至少 32 个字符长的随机字符串.

现在保存数据源,在此数据源之上构建的任何操作现在应该有一个 `X-Appsmith-Signature` 带有 JWT（如下所述）的标头作为它的值.

### Contents of the JWT <a href="#contents-of-the-jwt" id="contents-of-the-jwt"></a>

JWT 由三部分组成.标头、有效负载和签名.标头和有效负载本质上是 base64 编码的 JSON 对象.

典型的标头 JSON 对象如下所示:

```javascript
{
  "alg": "HS256",
  "typ": "JWT"
}
```

典型的有效负载 JSON 对象如下所示:

```javascript
{
  "iss": "Appsmith",
  "exp": 1516239022
}
```

### 构建令牌和签名 <a href="#e6-9e-84-e5-bb-ba-e4-bb-a4-e7-89-8c-e5-92-8c-e7-ad-be-e5-90-8d" id="e6-9e-84-e5-bb-ba-e4-bb-a4-e7-89-8c-e5-92-8c-e7-ad-be-e5-90-8d"></a>

现在,这两个被用来构造以下字符串（我们称之为主体）:

```javascript
base64Encode(JSON.stringify(header)) + "." + base64Encode(JSON.stringify(payload))
```

`alg` 然后使用标头密钥中指定的算法对该正文进行签名.用于制作此签名的秘密是用户在数据源中配置的秘密.然后将此签名附加到上面的正文 `"."` 中.

### 签名的意义 <a href="#e7-ad-be-e5-90-8d-e7-9a-84-e6-84-8f-e4-b9-89" id="e7-ad-be-e5-90-8d-e7-9a-84-e6-84-8f-e4-b9-89"></a>

签名将确保此 JWT 的真实性和完整性.

**真实性**: 真实性是令牌的属性,证明令牌来自 Appsmith.

如果没有访问用于创建签名的秘密,则无法重新创建签名.秘密签名仅对 Appsmith 和用户可用这一事实证明了签名和令牌的真实性.

**完整性**: 完整性是令牌不可篡改的属性.

除了秘密之外,签名是使用主体构造的.因此,如果标头或有效负载的内容或发生变化（导致令牌正文部分发生变化）,则签名将不匹配.但是,篡改者无法重新创建签名,因为他们无法获得秘密.因此,只要秘密仍然是秘密,就可以确保完整性.

在[https://jwt.io/introduction/](https://jwt.io/introduction/)了解有关 JWT 的更多信息.
