# 扫码器组件

扫描器组件允许您扫描各种条形码和 QR 码

<figure><img src="../../../.gitbook/assets/image (1) (2) (1).png" alt=""><figcaption></figcaption></figure>

### 1、支持类型

| 1D product | 1D industrial | 2D          |
| ---------- | ------------- | ----------- |
| UPC-A      | Code 39       | QR Code     |
| UPC-E      | Code 128      | Data Matrix |
| EAN-8      | ITF           | Aztec       |
| EAN-13     | RSS-14        | PDF 417     |



### 2、标签

| 字段 | 描述          |
| -- | ----------- |
| 文本 | 可设置组件内展示的文本 |

<figure><img src="../../../.gitbook/assets/image (40) (1).png" alt=""><figcaption></figcaption></figure>

### 3、属性

| 字段      | 描述                                                                         |
| ------- | -------------------------------------------------------------------------- |
| 是否显示    | 控制组件在页面上的可见性。关闭时：当应用程序发布时，组件将不可见。在编辑模式下它看起来是半透明的                           |
| 禁用      | 使该组件不可点击或不可用。该组件对用户保持可见，但不允许用户交互。                                          |
| 加载时显示动画 | 关闭时，该组件加载时不会有任何动画。您可以使用拨动开关将其打开/关闭。您还可以通过启用旁边的 JS 标签使用 javascript 将其关闭/打开。 |
| 提示消息    | 鼠标移至按钮的时候，触发消息提醒，可配置消息提醒的文本                                                |



### 4、事件



<figure><img src="../../../.gitbook/assets/image (32) (1).png" alt=""><figcaption></figcaption></figure>

### 5、样式

| 字段   | 描述                                         |
| ---- | ------------------------------------------ |
| 选择图标 | 可对按钮组件配置一个图标logo                           |
| 位置   | 设置logo的位置在文本的左侧或右侧                         |
| 对齐   | 可以设置logo与文本的位置组件内的位置，支持“左对齐”、“两端对齐”、“居中对齐” |
| 按钮颜色 |  设置扫码器按钮的底色                                |
| 边框圆角 | 对扫码器组件的边框样式进行修改                            |
| 阴影   | 对按钮样式调整阴影大小                                |

<figure><img src="../../../.gitbook/assets/image (39) (1).png" alt=""><figcaption></figcaption></figure>

### 6、JS代码



<figure><img src="../../../.gitbook/assets/image (10) (2) (1) (1).png" alt=""><figcaption></figcaption></figure>

### 7、例子演示

如果想从扫描的代码中获取响应，我们可以将扫码器组件的值绑定到另外一个小组件中，在小组件的值中添加如下代码

```
{{<your_widget>.value}}
```

例如，我们使用扫码器组件（CodeScanner1），并将其值绑定到文本组件上。我们可以给文本组件添加以下代码：

```
{{CodeScanner1.value}}
```

<figure><img src="../../../.gitbook/assets/image (44) (1).png" alt=""><figcaption></figcaption></figure>
