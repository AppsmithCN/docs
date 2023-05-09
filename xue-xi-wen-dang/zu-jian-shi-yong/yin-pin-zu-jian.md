# 音频组件

音频组件允许您播放各种 URL，包括文件路径、YouTube、Facebook、Twitch、SoundCloud、Streamable、优酷、B站等等

<figure><img src="../../../.gitbook/assets/image (92) (1) (1).png" alt=""><figcaption></figcaption></figure>

## 1、组件介绍

### 1、属性

你可以在所有可以编写JS的地方，通过该组件的名称来访问该组件的属性，从而读取该组件相关的信息。

| 属性名称          | 类型      | 描述                | 示例                    |
| ------------- | ------- | ----------------- | --------------------- |
| **autoPlay**  | Boolean | 这个属性表示是否启用自动播放功能。 | \{{Video.autoPlay\}}  |
| **playState** | String  | 这个属性显示当前是否正在播放视频  | \{{Video.playState\}} |

### 2、方法

你可以通过组件的方法来跟组件进行交互，可以在所有可以写 JavaScript 的地方通过组件的名称来调用它

| 方法          | 描述             |   |
| ----------- | -------------- | - |
| **onPlay**  | 设置视频播放时要运行的操作。 |   |
| **onPause** | 设置视频暂停时要运行的操作。 |   |
| **onEnd**   | 设置视频结束时要运行的操作。 |   |

## 2、界面使用介绍

### 1、数据

| 字段  | 描述            |
| --- | ------------- |
| URL | 要播放的音频源的 URL。 |

<figure><img src="../../../.gitbook/assets/image (52) (1).png" alt=""><figcaption></figcaption></figure>

### 2、属性

| 字段      | 描述                                                                            |
| ------- | ----------------------------------------------------------------------------- |
| 自动播放    | 在页面加载时自动播放音频，无需进行任何操作                                                         |
| 是否显示    | 控制组件在页面上的可见性。关闭时：当应用程序发布时，组件将不可见。在编辑模式下它看起来是半透明的                              |
| 加载时显示动画 | 您可以使用拨动开关将其打开/关闭。您还可以使用 JavaScript 关闭/打开它，方法是单击它旁边的 JS 标签并编写计算结果为_boolean_的代码 |

<figure><img src="../../../.gitbook/assets/image (82) (1).png" alt=""><figcaption></figcaption></figure>

### 3、事件

| 字段      | 描述         |
| ------- | ---------- |
| onPlay  | 开始播放时触发该动作 |
| OnPause | 暂停播放时触发该动作 |
| onEnd   | 播放结束时触发该动作 |

<figure><img src="../../../.gitbook/assets/image (50) (1).png" alt=""><figcaption></figcaption></figure>



### 4、动作

| 字段      | 描述    |
| ------- | ----- |
| 无动作     | 无任何行为 |
| 执行查询    |       |
| 执行JS函数  |       |
| 跳转到     |       |
| 消息提示    |       |
| 打开弹窗    |       |
| 关闭弹窗    |       |
| 保存数据    |       |
| 下载      |       |
| 复制      |       |
| 重置组件    |       |
| 设置定时器   |       |
| 清除定时器   |       |
| 获取定位    |       |
| 实时定位    |       |
| 停止实时定位  |       |
| 发消息     |       |

<figure><img src="../../../.gitbook/assets/image (61) (1).png" alt=""><figcaption></figcaption></figure>

### 6、JS代码



<figure><img src="../../../.gitbook/assets/image (91) (1).png" alt=""><figcaption></figcaption></figure>



📣动作的案例使用教程，点击跳转查看
