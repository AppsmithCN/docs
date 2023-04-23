---
description: HTMLPagePlugPagePlug
---

# 嵌入到网站HTML

在本指南中，您将了解如何将 PagePlug的应用或页面嵌入任何网站。



### 1、创建HTML页面

首先，让我们创建一个 HTML 页面并将其命名为\` `dashboard.html`\` 。现在，添加基本的 HTML 结构使其成为 HTML 页面：

```
<!DOCTYPE html>
<html>
<head>
    <title> Customer Dashboard </title>
</head>
<body>

</body>
</html>
```

在嵌入前，必须确保您的应用是公开的，才能嵌入到其他应用程序中。您可以在右上角【分享】侧，选择公开应用，将应用可公开访问

<figure><img src="../.gitbook/assets/image (129).png" alt=""><figcaption></figcaption></figure>





接下来，创建一个`iframe`标签并将共享选项中的可共享链接添加到`src`高度和宽度分别设置为`500`和 的属性`100%`。

在 head 中包含元标记以确保嵌入式应用程序在不同的屏幕尺寸上响应地呈现：

```
<!DOCTYPE html>
<html> 
<head>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title> Customer Support Dashboard </title>
</head>
<body>
    <iframe src="<LINK_OF_APP>" height="700" width="100%"></iframe>
</body>
</html>
```



### 2、打开HTML

{% hint style="info" %}
如果您以file的形式打开 HTML页面，浏览器将不允许您这样做。HTML 文件需要来自服务器。
{% endhint %}

创建 HTML 页面后，将其另存为`dashboard.html`并让 HTTP 服务器为其提供服务。有几种方法可以做到这一点，如下所述：

#### 1、使用Node.js提供HTML文件

创建 HTML 文件后，创建一个新的` app.js`` ` **\`\`**文件。粘贴下面提到的代码并编辑您的 HTML 文件名。

```
const http = require('http');
const fs = require('fs');

http.createServer(function(req, res) {
    res.writeHead(200, { 'content-type': 'text/html' });
    const html = fs.readFileSync('./dashboard.html');
    res.end(html);
}).listen(3000, () => {
    console.log('running on 3000');
});
```

现在，在终端中运行`node app.js`

这将提示一条`running on 3000`消息。接下来，转到您的浏览器并打开[http://localhost:3000/](http://localhost:3000/)

这将打开您的 HTML 文件。

<figure><img src="../.gitbook/assets/image (118).png" alt=""><figcaption></figcaption></figure>

#### 3、运行npx http服务器

这是打开 HTML 文件的另一种方法。

现在，如果您安装了_Node JS_，请转到命令终端并运行：

```
npx http-server
```

接下来，打开[http://localhost:8080/dashboard.html](http://localhost:8080/dashboard.html)，它应该会打开 HTML 文件。

### 3、修改布局小Tips

1、

您可以直接在 PagePlug应用程序中修改嵌入式代码的布局，并控制在网站或外部应用程序上显示时的外观。

* 要更改布局，请打开`app settings`.
* 点击`Share & Embed`。
* 根据需要更新嵌入大小。
* 复制更新的嵌入代码。

如果你想让你的应用在你的浏览器中使用整个页面，你可以改变你的高度和宽度参数，如下所示：

```
<!DOCTYPE html>
<html>
<head>
    <meta name="viewport" content="width=device-width, initial-scale=1"
    <title></title>
</head>
<body>
    <iframe src="<LINK_OF_APP>" scrolling="yes" seamless="seamless" style="display:block; width:100%; height:100vh;"></iframe>
</body>
</html>
```

#### 2、调整侧边栏

**`?embed=true`**您可以通过附加到共享 URL来删除带有页面选项卡的 Appsmith 顶部栏。或者，您可以从`App Settings`画布上获取准备好的 URL，如下所示。

![删除 Appsmith 顶部栏](https://docs.appsmith.com/assets/images/embed\_apps-ca688d32e01f82b6b1f8059b3c604242.png)

* 单击`App settings`画布属性。
* 点击`Share & Embed`。
* 切换`Show navigation bar`。
* 复制更新的嵌入代码。

```
<!DOCTYPE html>
<html>
<head>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title> Customer Support Dashboard </title>
</head>
<body>
    <iframe src="<LINK_OF_APP>" height="700" width="100%"></iframe>
</body>
</html>
```

![Appsmith 嵌入 ?embed=true 属性](https://docs.appsmith.com/assets/images/embed=true-d5f1018fc39c139b06ef270a07f17fcf.png)

### 4、SSO单点登录（商业版支持）

您可以在您的网站或外部应用程序中嵌入私有 PagePlug的应用或页面，并通过 SSO 无缝地验证用户身份。

#### ⚠️前提条件：

* PagePlug应用程序和父应用程序应位于同一域的子域下。例如。`Pageplug.company.com`和`internal.company.com`。
* 您必须在PagePlug和父应用程序上配置相同的 SSO 身份提供程序 (IDP)。

要将 PagePlug 配置为使用 SSO，您可以将以下参数（基于您的 SSO 类型）附加到您嵌入的应用程序的 URL 路径。

* `ssoTrigger=oidc`对于 OIDC SSO。
* `ssoTrigger=saml`用于基于 SAML 2.0 的 SSO。
* `ssoTrigger=google`适用于 Google OAuth 2.0 单点登录

#### ⚠️注意事项：

* 该功能可能不适用于`HTTP`URL。用于`HTTPS Pageplug` 实例和父应用程序。
* Firefox 有额外的第三方 cookie 限制，可能会导致私人嵌入出现问题。
* 在浏览器上启用严格的第三方 cookie 共享限制时，用户可能会遇到问题。
* GitHub OAuth 2.0 不支持私有嵌入中的 SSO。
* 对于Google OAuth 2.0 配置，父子可以是同一个项目下的两个OAuth 2.0 客户端。

\
