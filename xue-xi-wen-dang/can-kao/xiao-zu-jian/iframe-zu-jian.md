# Iframe组件

<figure><img src="../../../.gitbook/assets/image (114).png" alt=""><figcaption></figcaption></figure>



### 1、数据

| 字段   | 描述                                                                            |
| ---- | ----------------------------------------------------------------------------- |
| URL  | 设置要在 iframe组件中加载页面的URL                                                        |
| HTML | 提供 HTML（和`<style>`标签内的 CSS）以在 iframe 中呈现，而不是使用 URL。当此属性有值时，小部件的**URL**属性将被忽略。 |

<figure><img src="../../../.gitbook/assets/image (108) (1).png" alt=""><figcaption></figcaption></figure>

### 2、属性

| 字段      | 描述                                                                                                   |
| ------- | ---------------------------------------------------------------------------------------------------- |
| 标题      | 为 iframe 内容设置标题。此标题出现在 iframe 的 HTML 标记 ( `<iframe ... title="MyTitle">`) 和小部件的内部`IFrame1.title`属性中。 |
| 加载时显示动画 | 您可以使用拨动开关将其打开/关闭。您还可以使用 JavaScript 关闭/打开它                                                            |

<figure><img src="../../../.gitbook/assets/image (132).png" alt=""><figcaption></figcaption></figure>

### 3、事件

| 字段                | 描述                                              |
| ----------------- | ----------------------------------------------- |
| onURLChanged      | 设置更改URL时触发的动作，或者您可以定义一个自定义 JavaScript 函数来调用     |
| onSrcDocChanged   | 设置内嵌HTML变化时触发的动作，或者您可以定义一个自定义 JavaScript 函数来调用  |
| onMessageReceived | 设置嵌入页面接收到事件时触发的动作，或者您可以定义一个自定义 JavaScript 函数来调用 |

<figure><img src="../../../.gitbook/assets/image (118).png" alt=""><figcaption></figcaption></figure>

### 4、样式

| 字段    | 描述                    |
| ----- | --------------------- |
| 边框颜色  | 对Iframe组件的边框颜色设置调整    |
| 边框宽度  | 设置Iframe组件内画布与容器边框的宽度 |
| 边框透明度 | 设置Iframe组件底下画布颜色的透明度  |
| 边框圆角  | 对Iframe组件的边框样式进行修改    |
| 阴影    | 调整Iframe组件整体阴影大小      |

<figure><img src="../../../.gitbook/assets/image (137).png" alt=""><figcaption></figcaption></figure>



### 5、动作







### 6、案例演示



**用PagePlug的Iframe组件开发一个视频网站门户**

<figure><img src="../../../.gitbook/assets/image (123).png" alt=""><figcaption></figcaption></figure>



### 7、JS代码

<figure><img src="../../../.gitbook/assets/image (101) (1).png" alt=""><figcaption></figcaption></figure>
