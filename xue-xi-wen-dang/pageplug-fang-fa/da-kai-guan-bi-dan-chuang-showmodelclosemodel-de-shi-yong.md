---
description: 这个函数用于在触发时打开一个弹窗。
---

# 打开/关闭弹窗(showModel/closeModel)的使用

## 1、格式

* 打开弹窗

```javascript
showModal(modalName: string)
```

* 关闭弹窗

```javascript
closeModal(modalName: string)
```

## 2、参数介绍

| 参数名            | 描述       |
| -------------- | -------- |
| **Modal Name** | 要显示的弹窗名称 |

## 3、PagePlug内对应的动作事件

<figure><img src="../../.gitbook/assets/image (147).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (110).png" alt=""><figcaption><p>showModal——打开弹窗</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (148).png" alt=""><figcaption><p>closeModal——关闭弹窗</p></figcaption></figure>

## 4、案例

{% hint style="info" %}
想打开弹窗之前记得先创建弹窗哦
{% endhint %}

* 在**button**按钮的**onClick**事件选择**打开弹窗**

<figure><img src="../../.gitbook/assets/image (102) (3).png" alt=""><figcaption></figcaption></figure>

* 新建弹窗

![](<../../.gitbook/assets/image (108).png>)

* 点击按钮之后就可以显示弹窗啦

<figure><img src="../../.gitbook/assets/image (93).png" alt=""><figcaption></figcaption></figure>

* 关闭弹窗

在弹窗的**关闭按钮**的**onClick**事件选择**关闭弹窗**

<figure><img src="../../.gitbook/assets/image (17) (1) (1).png" alt=""><figcaption></figcaption></figure>

* 选择弹窗名称，点击关闭弹窗就消失啦

<figure><img src="../../.gitbook/assets/image (15) (1) (1).png" alt=""><figcaption></figcaption></figure>



