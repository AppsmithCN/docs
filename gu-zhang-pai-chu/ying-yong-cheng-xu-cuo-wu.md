# 应用程序错误

<figure><img src="../.gitbook/assets/image (8) (1).png" alt=""><figcaption></figcaption></figure>

### 1、无效/空名称错误 <a href="#invalid--empty-name-error" id="invalid--empty-name-error"></a>

&#x20;**错误原因：**

{% hint style="info" %}
Application name can't be empty.
{% endhint %}

&#x20; **导致的原因：**

此错误表明应用程序名称字段已留空。



&#x20;**解决方案：**

可以通过编辑应用程序名称字段并提供非空字符串作为应用程序名称来修复此错误。



### 2、重名错误

&#x20; **错误原因：**

{% hint style="info" %}
Entity name: is already being used.
{% endhint %}

&#x20; **导致的原因：**

此错误表明分配给实体的名称之前已被使用。

&#x20;   **解决方案：**

JavaScript 保留关键字和窗口对象方法和属性不能用作实体名称。您可以通过为实体分配一个新的唯一名称来修复错误。



### 3、登录/注册错误

<figure><img src="../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

&#x20; **3.1账号已注册**

&#x20;       **错误原因：**

{% hint style="info" %}
There is already an account registered with this email. Please sign in instead.
{% endhint %}

&#x20;       **导致的原因：**

此错误表明用于注册的电子邮件之前已被使用过。\


&#x20;       **解决方案：**

这个错误可以通过使用不同的电子邮件注册或做`login`而不是`signup`

&#x20;  **3.2重置密码**

&#x20;       **错误原因：**

{% hint style="info" %}
It looks like you may have entered incorrect/invalid credentials. Please try again or reset password using the button below.
{% endhint %}

&#x20;       **导致的原因：**

当您尝试使用无效的电子邮件和/或密码登录 PagePlug 平台时，会出现此错误。



&#x20;   **解决方案：**

如果您因忘记凭据而无法登录，建议您重置您的帐户密码。这可以通过 PagePlug 登录页面上的“忘记密码”按钮来完成；该页面会提示您输入与您的帐户关联的电子邮件地址，然后 PagePlug 会向该地址发送一封电子邮件，其中包含用于创建新密码的链接。

或者，您可以使用 Google 或 GitHub 等 SSO 方法访问您的帐户。如果您使用 SSO 的帐户与您通常用于通过电子邮件和密码登录的帐户具有相同的电子邮件地址，则您应该可以成功登录。

如果您在使用 PagePlug 的自托管实例时需要重置密码，则必须先将实例配置为发送电子邮件通知。

****

### 4、没有用户

&#x20;   **错误原因：**

{% hint style="info" %}
Unable to find user .
{% endhint %}

&#x20;   **导致的原因：**

该错误表明提供用于重置密码的电子邮件未在 PagePlug 注册。



&#x20;**解决方案：**

您可以通过提供之前用于注册 PagePlug 的电子邮件来修复错误。或者，任何新的未注册电子邮件都可用于使用注册选项创建新帐户。



### 5、页面访问

&#x20; **错误原因：**

{% hint style="info" %}
Either this page does not exist, or you don't have access to this page.
{% endhint %}

&#x20; **导致的原因：**

* 页面 URL 无效。
* 用户无权访问该页面。

&#x20;   **解决方案：**

您可以通过从 请求页面的访问权限来修复错误`admin/developer`
