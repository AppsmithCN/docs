# 图片组件

图片组件可以显示应用程序中的图像。图片格式必须是 URL 或有效的 base64。

<figure><img src="../../../.gitbook/assets/image (104) (1) (1).png" alt=""><figcaption></figcaption></figure>

### 1、数据

| 字段   | 描述                                                |
| ---- | ------------------------------------------------- |
| 图片   | 设置图像的来源。支持图像 URL、数据 URI 或 base64 编码图像数据           |
| 默认图片 | 当图片加载不出来时，将显示该图像。接受图像 URL、数据 URI 或 base64 编码图像数据。 |

<figure><img src="../../../.gitbook/assets/image (130).png" alt=""><figcaption></figcaption></figure>

### 2、属性

| 字段      | 描述                                                                                                                               |
| ------- | -------------------------------------------------------------------------------------------------------------------------------- |
| 图片填充方式  | 设置图片填充父容器方式，支持“包含”、“封面”、“自动”三种形式，如有其他形式的疑惑，可以参阅 CSS[`object-fit`](https://developer.mozilla.org/en-US/docs/Web/CSS/object-fit)文档 |
| 最大缩放倍数  | 设置图像最大允许缩放倍数。启用 JS 后，接受数字值。                                                                                                      |
| 是否显示    | 控制组件在页面上的可见性。关闭时：当应用程序发布时，组件将不可见。在编辑模式下它看起来是半透明的                                                                                 |
| 加载时显示动画 | 关闭时，该组件加载时不会有任何动画。您可以使用拨动开关将其打开/关闭。您还可以通过启用旁边的 JS 标签使用 javascript 将其关闭/打开。                                                       |
| 允许旋转    | 组件上会新增允许旋转图像的按钮                                                                                                                  |
| 允许下载    | 组件上会新增允许下载图像的按钮                                                                                                                  |

<figure><img src="../../../.gitbook/assets/image (93) (1).png" alt=""><figcaption></figcaption></figure>

### 3、事件

| 字段      | 描述            |
| ------- | ------------- |
| onClick | 点击图片组件时候触发的动作 |

<figure><img src="../../../.gitbook/assets/image (134).png" alt=""><figcaption></figcaption></figure>

### 4、动作





### 5、样式

| 字段   | 描述             |
| ---- | -------------- |
| 边框圆角 | 对图片组件的边框样式进行修改 |
| 阴影   | 对图片组件调整阴影大小    |

<figure><img src="../../../.gitbook/assets/image (94) (1).png" alt=""><figcaption></figcaption></figure>

### 6、例子说明

PagePlug 支持几乎所有主要图像格式，包括：

* 图片
* PNG
* SVG
* WebP
* GIF

你可以将下列地址输入到图片组件中体验查看

```
//png:
 https://assets.appsmith.com/widgets/default.png

//jpg:
https://jpeg.org/images/jpegsystems-home.jpg

//gif:
https://mir-s3-cdn-cf.behance.net/project_modules/max_1200/5eeea355389655.59822ff824b72.gif

//webp:
https://www.gstatic.com/webp/gallery/4.sm.webp

//svg:
https://assets.codepen.io/3/kiwi.svg
```



**内嵌说明**

内联 SVG 是指包含在网页标记中的 SVG 标记。要显示内联 SVG，可以试下以下步骤操作：

* 将图像小部件拖放到画布中
* 现在在图像部分，将下面提到的 URL 与您的 SVG 代码粘贴在一起：

```
data:image/svg+xml;charset=UTF-8,{{encodeURI('<svg..<your-svg>.. ></svg>')}}
```

您甚至可以使用这样的编码 URL：

```
example 1:
data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg'%3E%3Ccircle r='50' cx='50' cy='50' fill='tomato'/%3E%3Ccircle r='41' cx='47' cy='50' fill='orange'/%3E%3Ccircle r='33' cx='48' cy='53' fill='gold'/%3E%3Ccircle r='25' cx='49' cy='51' fill='yellowgreen'/%3E%3Ccircle r='17' cx='52' cy='50' fill='lightseagreen'/%3E%3Ccircle r='9' cx='55' cy='48' fill='teal'/%3E%3C/svg%3E

example 2:
data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='100' height='100'%3E%3Ccircle cx='50' cy='50' r='40' stroke='green' stroke-width='4' fill='yellow' /%3E%3C/svg%3E
```

### 7、JS代码



<figure><img src="../../../.gitbook/assets/image (98) (1).png" alt=""><figcaption></figcaption></figure>
