---
description: 使用resetWidget方法将组件恢复到其默认状态。任何用户输入的更改都将被恢复，并应用默认属性中的值。
---

# 重置(resetWidet)的使用

## 1、格式

```javascript
resetWidget(widgetName: string, resetChildren?: boolean = true)
```

## 2、参数介绍

| 参数名                            | 描述                  |
| ------------------------------ | ------------------- |
| **widgetName**                 | 需要重置的组件的名称          |
| **`resetChildren`** (optional) | 所有的子组件也会被重置，默认为true |

## 3、PagePlug内对应的动作事件

<figure><img src="../../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (8) (1).png" alt=""><figcaption></figcaption></figure>

## 4、案例

onClick事件配置如下

例如：可以先在输入框中输入点内容，之后点击重置，你会发现表单回到初识状态了，也就是重置了

<figure><img src="../../.gitbook/assets/image (155).png" alt=""><figcaption></figcaption></figure>
