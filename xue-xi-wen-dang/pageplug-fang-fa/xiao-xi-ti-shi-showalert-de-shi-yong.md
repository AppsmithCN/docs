---
description: 向用户显示一个临时的消息提示，持续5秒。警报消息的持续时间不能修改。
---

# 消息提示(showAlert)的使用

## 1、格式

```javascript
showAlert(message: string, style: string)
```

## 2、参数说明

| 参数名            | 描述                             |
| -------------- | ------------------------------ |
| Message        | 您希望传输到的页面名称或URL，PageName区分大小写。 |
| **params(可选)** | 通过URL传递的查询参数，用于与目标页共享信息。       |
| **target(可选)** | 配置在哪里打开URL，默认当前窗口。             |

* **Message：**显示给用户的消息。
* **Style：**警报消息的样式。可以是“info”、“success”、“error”或“warning”之一。

## 3、PagePlug内对应的动作事件

<figure><img src="../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (100) (2).png" alt=""><figcaption></figcaption></figure>

## 4、案例

* 在button的**onClick**事件选**消息提示**

<figure><img src="../../.gitbook/assets/image (145) (1).png" alt=""><figcaption></figcaption></figure>

* 消息、成功、错误、警告类型提示分别如下图所示

<figure><img src="../../.gitbook/assets/image (111) (2).png" alt=""><figcaption></figcaption></figure>
