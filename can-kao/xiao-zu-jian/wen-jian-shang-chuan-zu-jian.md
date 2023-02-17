# 文件上传组件

文件上传组件允许通过 API 将文件从本地计算机上传到任何云存储。Cloudinary 和 Amazon S3 具有用于云存储上传的简单 API

<figure><img src="../../.gitbook/assets/image (96).png" alt=""><figcaption></figcaption></figure>

**小Tips：**

您可以通过创建帖子API 并在帖子正文中引用文件的 base64 或二进制版本来上传文件。数据格式由属性窗格中的数据类型属性确定

```
{{ Filepicker1.files[0].data }}
```

{% hint style="info" %}
信息

如果你尝试记录数据时，它会以 blob 格式出现。但是，如果在 API/查询中使用它，它实际上会上传 base64/二进制数据。
{% endhint %}

{% hint style="info" %}
如果你尝试上传大文件，请记得增加 API 配置中的超时时间。只要文件大于 5mb，它就会存储为 blob。
{% endhint %}

### 1、属性

| 字段     | 描述                                                                    |
| ------ | --------------------------------------------------------------------- |
| 支持文件类型 | 设置允许上传的文件类型，支持多选。支持“任意文件类型”、“图片”、“视频”、“音频”、“文本”、“word文档”、“JPEG”、“PNG” |
| 数据格式   | 设置上传文件的数据格式。支持Base64、二进制、文本（纯文本）和数组 (CSV)                             |
| 最大上传数量 | 可以设置一次上传多少个文件                                                         |

<figure><img src="../../.gitbook/assets/image (95).png" alt=""><figcaption></figcaption></figure>

### 2、标签

| 字段 | 描述        |
| -- | --------- |
| 文本 | 设置按钮展示的文本 |

<figure><img src="../../.gitbook/assets/image (138).png" alt=""><figcaption></figcaption></figure>

### 3、校验

| 字段     | 描述            |
| ------ | ------------- |
| 必填     | 可以设置按钮是否为必选选项 |
| 最大上传大小 | 配置每个上传文件最大上限  |

<figure><img src="../../.gitbook/assets/image (119).png" alt=""><figcaption></figcaption></figure>

### 4、属性

| 字段      | 描述                                               |
| ------- | ------------------------------------------------ |
| 是否显示    | 控制组件在页面上的可见性。关闭时：当应用程序发布时，组件将不可见。在编辑模式下它看起来是半透明的 |
| 禁用      | 使该组件不可点击或不可用。该组件对用户保持可见，但不允许用户交互。                |
| 加载时显示动画 | 您可以使用拨动开关将其打开/关闭。您还可以使用 JavaScript 关闭/打开它        |

<figure><img src="../../.gitbook/assets/image (112).png" alt=""><figcaption></figcaption></figure>

### 5、事件





### 6、样式

| 字段   | 描述               |
| ---- | ---------------- |
| 按钮颜色 | 设置按钮的颜色          |
| 边框圆角 | 对文件上传组件的边框样式进行修改 |
| 阴影   | 调文件上传组件整体阴影大小    |

<figure><img src="../../.gitbook/assets/image (110).png" alt=""><figcaption></figcaption></figure>

### 7、JS代码

<figure><img src="../../.gitbook/assets/image (140).png" alt=""><figcaption></figcaption></figure>
