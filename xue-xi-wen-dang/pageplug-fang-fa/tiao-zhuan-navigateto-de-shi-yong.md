---
description: >-
  该事件允许用户在应用程序的内部页面或外部URL之间导航。它可以在任何小部件操作上触发，如Button的onClick,
  Dropdown的onOptionChange等。在navigateTo函数中输入页面名称或外部URL(在onClick等触发操作下)，如果需要，输入Query参数，并为新页面(新窗口或相同窗口)选择目的地。
---

# 跳转(navigateTo)的使用

## 1、格式

```javascript
navigateTo(pageName | Url: string, params?: {}, target: "SAME_WINDOW" | "NEW_WINDOW") -> Promise
```

## 2、参数介绍

| 参数名              | 描述                             |
| ---------------- | ------------------------------ |
| **pageName或Url** | 您希望传输到的页面名称或URL，PageName区分大小写。 |
| **params(可选)**   | 通过URL传递的查询参数，用于与目标页共享信息。       |
| **target(可选)**   | 配置在哪里打开URL，默认当前窗口。             |

## 3、PagePlug内对应的动作事件

<figure><img src="../../.gitbook/assets/image (200).png" alt=""><figcaption><p>navigateTo方法对应的动作是——跳转到</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (136).png" alt=""><figcaption></figcaption></figure>

## 4、案例介绍

例如Page1想给Page2共享某个数据

* 在**button**组件的**onClick**事件选择跳转到

<figure><img src="../../.gitbook/assets/image (198).png" alt=""><figcaption></figcaption></figure>

* 选择**Page2**

<figure><img src="../../.gitbook/assets/image (19) (1) (2).png" alt=""><figcaption></figcaption></figure>

* 在**查询参数**填入一下代码

```
{{{
	"test": "123"
}}}
```

<figure><img src="../../.gitbook/assets/image (17) (1) (3).png" alt=""><figcaption></figcaption></figure>

* 点击**提交**，在**Page2**，通过 **global.URL.queryParams** 可以取到该数据

<figure><img src="../../.gitbook/assets/image (138).png" alt=""><figcaption></figcaption></figure>

* 同理，给外部URL传递数据类似

<figure><img src="../../.gitbook/assets/image (137) (1).png" alt=""><figcaption></figcaption></figure>

* 点击**提交**，你会在新窗口看到传递的数据

<figure><img src="../../.gitbook/assets/image (126).png" alt=""><figcaption></figcaption></figure>

