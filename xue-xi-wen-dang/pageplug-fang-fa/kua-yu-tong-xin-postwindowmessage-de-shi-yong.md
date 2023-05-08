---
description: >-
  pageplug提供了一种在pageplug应用程序和Iframe小部件之间实现安全跨域通信的方法。假设您正在构建一个应用程序，其中包含一个嵌入外部页面的Iframe组件，并希望在外部页面和pageplug应用程序之间发布消息。
---

# 跨域通信(postWindowMessage)的使用

### 1、相关参数

**postWindowMessage()**可用于在应用程序或父窗口与iframe之间发送消息。

```
postWindowMessage(message, targetIframe, targetOrigin)
```

| 参数名              | 介绍                                                                                                             |
| ---------------- | -------------------------------------------------------------------------------------------------------------- |
| **message**      | 这是要发送到目标iframe或窗口的消息。大多数JavaScript值在这里都是可以接受的，除了null和undefined。(默认:“”)                                         |
| **targetIframe** | 这是要向其发送消息的窗口。如果它的值是"window"，那么你正在向父应用程序的窗口global应用被嵌入其中)发送消息。如果要向global中的iframe发送消息，请在此处输入iframe的名称。(默认值是“窗口”) |
| **targetOrigin** | 这是您可以向其发送消息的URL。默认值“\*”表示消息可以发送到任何URL。如果您想限制只向父应用程序(其中嵌入global)发送消息，请在这里输入父应用程序的URL。(默认值是“\*”)                 |

### 2、PagePlug内的动作事件

<figure><img src="../../.gitbook/assets/image (199).png" alt=""><figcaption><p>postWindowMessage方法对应的动作是——发消息</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (197).png" alt=""><figcaption></figcaption></figure>

### 3、给iframe小组件发消息案例

首先演示一个简单案例

#### &#x20;       2.1将一个名为inputMessage的Input组件和一个Button组件拖放到画布上。

![](<../../.gitbook/assets/image (14).png>)

#### &#x20;       2.2在画布上放置一个名为iframeExample的Iframe组件。在html属性中，插入以下代码：

```
<div id="target"></div>

<script>
window.addEventListener('message', (event) => {
    const tgt = document.querySelector("#target")
        tgt.textContent = event.data
    });
</script>
```

* 这段代码监听从pageplug中的Input组件发送的消息，并在Iframe中的HTML元素中显示文本。

<figure><img src="../../.gitbook/assets/image (19) (3).png" alt=""><figcaption></figcaption></figure>

#### &#x20;       2.3在按钮的**onClick**事件中，选择**发消息**选项。

* 将消息的内容设置为**\{{inputMessage.text\}}**。然后目标iframe 填入 **iframeExample**。

<figure><img src="../../.gitbook/assets/image (197) (1).png" alt=""><figcaption></figcaption></figure>

#### &#x20;       2.4 输入“你好呀”，点击**发送**

<figure><img src="../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

#### &#x20;       2.5iframe收到消息

<figure><img src="../../.gitbook/assets/image (17) (2).png" alt=""><figcaption></figcaption></figure>

