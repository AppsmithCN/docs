# 配置邮箱服务

PagePlug集成了邮箱服务，你可以在PagePlug上通过邮件的方式：

* 邀请用户加入到PagePlug团队中
* 有重要的事情和批准请求通知管理员
* 处理团队用户的电子邮件，例如密码重置



### 1、前置条件

PagePlug邮件需要配置以下环境变量：

| 字段                                     | 描述                                                                                                    |
| -------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| **APPSMITH\_MAIL\_ENABLED**            | 设置为 true 以启用电子邮件服务。                                                                                   |
| **APPSMITH\_MAIL\_FROM**               | 设置为发件人经过验证的电子邮件。                                                                                      |
| **APPSMITH\_REPLY\_TO**                | 设置为默认应接收回复的电子邮件。                                                                                      |
| **APPSMITH\_MAIL\_HOST**               | 设置邮件服务提供商的**SMTP 主机。**                                                                                |
| **APPSMITH\_MAIL\_PORT**               | 将其设置为电子邮件服务提供商可用的**SMTP 端口。**                                                                         |
| **APPSMITH\_MAIL\_SMTP\_TLS\_ENABLED** | 如果设置为**true，则启用传输层安全性。**                                                                              |
| **APPSMITH\_MAIL\_SMTP\_AUTH**         | 将其设置为**true**以共享凭据 (`APPSMITH_MAIL_USERNAME`\* **\* 和 \*\*** `APPSMITH_MAIL_PASSWORD`**)**与 SMTP 服务器。 |
| **APPSMITH\_MAIL\_USERNAME**           | 设置为访问SMTP服务商的用户名。                                                                                     |
| **APPSMITH\_MAIL\_PASSWORD**           | 将其设置为 SMTP 用户的密码。您也可以将其设置为电子邮件服务提供商为 SMTP 用户生成的 API 密钥。                                               |

或者可以在管理员设置这里进行配置：

<figure><img src="../.gitbook/assets/image (186).png" alt=""><figcaption></figcaption></figure>

接下来将分享该如何在PagePlug上配置邮箱服务～～

### 2、配置邮箱

#### &#x20;       2.1登录进来后点击管理员设置

<figure><img src="../.gitbook/assets/image (189).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
稍后配置邮箱服务的时候，在管理员邮箱这里，要确保这里出现你登陆的邮箱，不然权限不够会配置失败哟
{% endhint %}

<figure><img src="../.gitbook/assets/image (187).png" alt=""><figcaption></figcaption></figure>

#### &#x20;       2.2填写信息

接下来点击左侧**邮箱，**我们需要分别填写**smtp主机**、**smtp端口**、**发件地址**、**回复地址**、**开启TLS安全连接**、**smtp用户名**、**smtp用户密码**

<figure><img src="../.gitbook/assets/image (174).png" alt=""><figcaption></figcaption></figure>

| 字段        | 描述                            |
| --------- | ----------------------------- |
| SMTP主机    | 填写你的邮件服务提供商的 SMTP 主机          |
| SMTP端口    | 填写你的邮件服务提供商的 SMTP 端口          |
| 发件地址      | 需要填写一个内部的邮箱地址，地址最终将显示在邮件发送的地方 |
| 回复地址      | 需要填写一个内部的邮箱地址，地址最终将显示在邮件回复的地方 |
| 开启TLS安全连接 | 默认启用，切换回禁用                    |
| SMTP用户名   | 添加你的邮件地址名称                    |
| SMTP用户密码  | 添加你的邮件地址密码（可以在邮件设置里面生成第三方密码）  |

### 3、例子示范（以阿里云邮箱为例子）

* 以**阿里云邮箱**为例，**stmp主机**在右上角的设置-->邮箱设置-->POP和IMAP 可以找到

<figure><img src="../.gitbook/assets/image (177).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (185).png" alt=""><figcaption></figcaption></figure>

* 查找stmp端口，可以在官网查询，选常规的即可

<figure><img src="../.gitbook/assets/image (190).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (184).png" alt=""><figcaption></figcaption></figure>

* 配置发件地址、回复地址和用户名

**发件地址**、**回复地址**用你邮箱地址就好，**smtp用户名**一般也是你邮箱

<figure><img src="../.gitbook/assets/image (188).png" alt=""><figcaption></figcaption></figure>

* **smtp密码**

获取方式如下：在设置-->账户与安全-->账户安全中，开启三方客户端安全密码，然后生成新密码，记得复制下来哦

<figure><img src="../.gitbook/assets/image (192).png" alt=""><figcaption></figcaption></figure>

* 点击左下角保存，重启服务，之后点击发送测试邮件，会有收到一个这样的提示

<figure><img src="../.gitbook/assets/image (180).png" alt=""><figcaption></figcaption></figure>

你的邮箱应该会收到电子邮件收件箱中收到一封测试电子邮件。

* 可以退出登录，测试下忘记密码的邮件服务

<figure><img src="../.gitbook/assets/image (182).png" alt=""><figcaption></figcaption></figure>

* 填写邮箱，点击重置

<figure><img src="../.gitbook/assets/image (178).png" alt=""><figcaption></figcaption></figure>

* 之后页面会提示重置成功，你提供的邮箱也会收到重置消息

<figure><img src="../.gitbook/assets/image (196).png" alt=""><figcaption></figcaption></figure>
