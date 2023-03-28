# 按钮组件

按钮组件是一个可点击的实体，可以触发附加到它的任何事件。

<figure><img src="../../../../.gitbook/assets/image (71) (1).png" alt=""><figcaption></figcaption></figure>

### 1、属性

| 字段      | 描述                                                                          |
| ------- | --------------------------------------------------------------------------- |
| 标签      | 可设置按钮内的文案                                                                   |
| onclick | 设置单击此组件时要发生的操作。可以从常见操作的 GUI 列表中设置（请参阅下方动作列表。），或者可以定义一个自定义 JavaScript 函数来调用。 |

<figure><img src="../../../../.gitbook/assets/image (72) (1).png" alt=""><figcaption></figcaption></figure>

### 2、消息属性

| 字段      | 描述                                               |
| ------- | ------------------------------------------------ |
| 提示      | 鼠标移至按钮时触发消息提醒                                    |
| 是否显示    | 控制组件在页面上的可见性。关闭时：当应用程序发布时，组件将不可见。在编辑模式下它看起来是半透明的 |
| 禁用      | 使该组件不可点击或不可用。该组件对用户保持可见，但不允许用户交互。                |
| 加载时显示动画 | 您可以使用拨动开关将其打开/关闭。您还可以使用 JavaScript 关闭/打开它        |

<figure><img src="../../../../.gitbook/assets/image (57) (1).png" alt=""><figcaption></figcaption></figure>

### 3、校验

| 字段                       | 描述                                                                                                                                                                                                                                                                     |
| ------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Google reCAPTCHA Key     | 这里提供 Google reCAPTCHA[站点密钥](https://cloud.google.com/recaptcha-enterprise/docs/create-key)，会向按钮添加[Google reCAPTCHA](https://www.google.com/recaptcha/about/)检查。`recaptchaToken`可以使用密钥从 API 窗格访问令牌（请参阅我们的[Google reCAPTCHA](https://www.google.com/recaptcha/about/)文档） |
| Google reCAPTCHA Version | 设置用于按钮的Google reCAPTCHA版本                                                                                                                                                                                                                                              |

<figure><img src="../../../../.gitbook/assets/image (83) (1).png" alt=""><figcaption></figcaption></figure>

### 4、表单设置

| 字段         | 描述                                                                          |
| ---------- | --------------------------------------------------------------------------- |
| 表单校验不成功时禁用 | 如果按钮组件在表单组件内，表单必须校验成功才能点击此按钮                                                |
| 提交成功后重置表单  | 设置单击此组件时要发生的操作。可以从常见操作的 GUI 列表中设置（请参阅下方动作列表。），或者可以定义一个自定义 JavaScript 函数来调用。 |

<figure><img src="../../../../.gitbook/assets/image (74) (1).png" alt=""><figcaption></figcaption></figure>

### 5、动作







### 6、样式

| 字段   | 描述                                 |
| ---- | ---------------------------------- |
| 按钮类型 | 有三种类型样式选择，“主按钮”、“次级按钮”、“文本按钮”      |
| 选择图标 | 可以在文案旁新增图标，丰富样式                    |
| 位置   | 调整图标的位置，可设置在文案的“左侧”或“右侧”           |
| 排列方式 | 调整文案及图标的位置，分别是“向前对齐”、“两边对齐”、“居中对齐” |
| 按钮颜色 | 对按钮底色背景进行修改                        |
| 边框圆角 | 对按钮边框样式进行修改                        |
| 阴影   | 对按钮样式调整阴影大小                        |

<figure><img src="../../../../.gitbook/assets/image (73) (1).png" alt=""><figcaption></figcaption></figure>

### 7、JS代码



<figure><img src="../../../../.gitbook/assets/image (66) (1).png" alt=""><figcaption></figcaption></figure>

