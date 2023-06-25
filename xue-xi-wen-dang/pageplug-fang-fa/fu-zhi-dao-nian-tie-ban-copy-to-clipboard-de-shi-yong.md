---
description: 此函数用于将文本复制到剪贴板。
---

# 复制到粘贴板(Copy to clipboard)的使用

## 1、格式

```javascript
copyToClipboard(data: string, options: object)
```

## 2、参数介绍

| 参数名                | 描述                |
| ------------------ | ----------------- |
| **data**           | 要复制的数据            |
| **options.debug**  | 布尔值，可选的，启用控制台输出   |
| **options.format** | 字符串，可选的，设置要复制文本类型 |

## 3、PagePlug内对应的动作事件

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (3) (1) (2) (2).png" alt=""><figcaption></figcaption></figure>

## 4、案例

例如：在按钮组件中选择复制输入框（input）组件的内容

<figure><img src="../../.gitbook/assets/image (151).png" alt=""><figcaption></figcaption></figure>

