---
description: 此操作的目的是将任何数据下载为文件。该功能是通过使用downloadjs库实现的。
---

# 下载(download)的使用

## 1、格式

```javascript
download(data: any, fileName: string, fileType?: string)
```



## 2、参数介绍

| 参数名          | 描述         |
| ------------ | ---------- |
| **data**     | 要下载的数据或URL |
| **fileName** | 待下载的文件名    |
| **fileType** | 要下载的文件类型   |

## **3、PagePlug内对应的动作事件**

<figure><img src="../../.gitbook/assets/image (10) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (9) (1) (1).png" alt=""><figcaption></figcaption></figure>

## 4、支持的文件类型

Pageplug为下载各种格式的文件提供了广泛的支持，包括：

* Plain text
* HTML
* CSV
* JSON
* JPEG
* PNG
* SVG

{% hint style="info" %}
Download操作不会将文件转换为特定类型，而是以原始格式下载。如果需要更改文件类型，则需要在下载之前使用JavaScript将数据转换为特定格式。
{% endhint %}

## 5、案例

### **1、下载纯文本**

要下载纯文本文档，传递给下载操作的数据应该是要下载的文本内容的字符串表示形式。此外，应该为下载函数提供一个filename和一个可选的fileType参数。

* 在按钮的onclick事件中选择下载

<figure><img src="../../.gitbook/assets/image (105).png" alt=""><figcaption></figcaption></figure>

* 填写**下载数据**、**完整文件名**、**文件类型**

<figure><img src="../../.gitbook/assets/image (144).png" alt=""><figcaption></figcaption></figure>

* 在输入框中输入内容，点击**下载**

<figure><img src="../../.gitbook/assets/image (5) (1) (3).png" alt=""><figcaption></figcaption></figure>

* 该内容会被下载成txt文件，你打开会看到：

<figure><img src="../../.gitbook/assets/image (101).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
此功能对于保存笔记、日志或任何其他类型的纯文本信息非常有用，以便以后参考或与他人共享。
{% endhint %}

如果想导出excel的文件，可以参考[添加第三方js库](../pageplug-de-js-ku/zhi-chi-tian-jia-di-san-fang-js-ku.md)[(ExcelJS)](../pageplug-de-js-ku/zhi-chi-tian-jia-di-san-fang-js-ku.md)的案例

### 2、下载图像

{% hint style="info" %}
要下载图像，传递给下载操作的数据应该是图像的URL或图像的Base64字符串表示形式。



另外，一个fileName和一个可选的fileType应该作为参数提供给下载函数。
{% endhint %}

* 用一个图片组件，默认图片地址放一张图片的地址，例如

```
https://th.bing.com/th/id/R.987f582c510be58755c4933cda68d525?rik=C0D21hJDYvXosw&riu=http%3a%2f%2fimg.pconline.com.cn%2fimages%2fupload%2fupc%2ftx%2fwallpaper%2f1305%2f16%2fc4%2f20990657_1368686545122.jpg&ehk=netN2qzcCVS4ALUQfDOwxAwFcy41oxC%2b0xTFvOYy5ds%3d&risl=&pid=ImgRaw&r=0
```

<figure><img src="../../.gitbook/assets/image (92).png" alt=""><figcaption></figcaption></figure>

* 下载事件配置：
  * **下载数据，**\{{Image1.defaultImage\}}
  * 文件名，sample
  * 文件类型，png或JPEG

<figure><img src="../../.gitbook/assets/image (97).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
对于图片文件类型，文件名无需提供后缀
{% endhint %}

{% hint style="info" %}
为了成功下载文件，它们的内容必须通过HTTPS提供，以防止请求被阻止。为了防止跨域资源共享(Cross-Origin Resource Sharing, CORS)错误，请确保获取文件的服务器启用了CORS，并在响应中返回所需的标头。
{% endhint %}
