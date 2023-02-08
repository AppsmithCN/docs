# 相机组件

相机组件可以在应用程序中捕获图像和视频，并共享数据以供进一步使用。

<figure><img src="../../.gitbook/assets/image (84).png" alt=""><figcaption></figcaption></figure>

### 1、属性

| 字段   | 描述                                               |
| ---- | ------------------------------------------------ |
| 模式   | 相机组件支持“拍照”或“录像”的方式                               |
| 是否可见 | 控制组件在页面上的可见性。关闭时：当应用程序发布时，组件将不可见。在编辑模式下它看起来是半透明的 |
| 禁用   | 使该组件不可点击或不可用。该组件对用户保持可见，但不允许用户交互。                |
| 显示镜像 | 应用会展示正在捕获的图像，默认情况下打开。                            |

<figure><img src="../../.gitbook/assets/image (75).png" alt=""><figcaption></figcaption></figure>



### 2、事件



<figure><img src="../../.gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>



### 3、样式

| 字段   | 描述            |
| ---- | ------------- |
| 边框圆角 | 对相机组件边框样式进行修改 |
| 阴影   | 对相机组件样式调整阴影大小 |

<figure><img src="../../.gitbook/assets/image (55).png" alt=""><figcaption></figcaption></figure>



### 4、绑定

这些属性允许您将相机小部件与查询或 JS 对象中的任何其他小部件绑定。下表列出了所有绑定属性。

| **imageBlobURL** | 图像的 Blob URL，用于存储图像以供将来使用。     | `{{<camerawidget_name>.imageBlobURL}}`   |
| ---------------- | ------------------------------ | ---------------------------------------- |
| **图像数据URL**      | 图像的数据 URL 格式，以将其内联嵌入到不同的应用程序中。 | `{{<camerawidget_name>.`图像数据URL`}}`      |
| **图像原始二进制文件**    | 图像的二进制文件格式，用于存储图像以备将来使用。       | `{{<camerawidget_name>.`图像原始二进制文件`}}`    |
| **videoBlobURL** | 视频的 Blob URL，用于存储图像以供将来使用。     | `{{<camerawidget_name>.`videoBlobURL`}}` |
| **视频数据URL**      | 视频的数据 URL 格式，以将其内联嵌入到不同的应用程序中。 | `{{<camerawidget_name>.`视频数据URL`}}`      |
| **视频原始二进制文件**    | 图像的二进制文件格式，用于存储图像以备将来使用。       | `{{<camerawidget_name>.`视频原始二进制文件`}}`    |

