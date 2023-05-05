# 源码本地化部署（Mac版）未更新完

## 1、前置准备

PagePlug 后端启动需要 Jdk11、Maven3、一个Mongo实例和一个Redis实例，请检查下电脑是否已经部署好，如果还没有的话，可以查看下面教程安装

### 1.1 配置Java—OpenJSDK11

#### 1.1.1下载JDK11

* 下载地址[https://www.oracle.com/java/technologies/downloads/#jdk20-mac](https://www.oracle.com/java/technologies/downloads/#jdk20-mac)
* 如果是M1及以上的选择ARM，如果是inter的，选择X64。

<figure><img src="../../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

#### 1.1.2对JDK进行安装

* 将下载好的文件，点击运行

<figure><img src="../../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

* 一路点击继续

<figure><img src="../../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

* 可以在终端输入**`java -version`**，查看是否安装成功

```
java -version
```

<figure><img src="../../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

#### 1.1.3配置环境变量

* 点击苹果快捷键

```
commadn+shift+G
```

* 一般安装都在这个默认路径

```
/Library/Java/JavaVirtualMachines/
```

<figure><img src="../../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

* 点击JDK文件，进入/Contents/Home

<figure><img src="../../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

* 切换权限，或者给指令添加sudo

```
sudo chmod 773 /etc/profile
```

<figure><img src="../../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

* 编辑/ect/profile文件：

```
vim /etc/profile
```

<figure><img src="../../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

* 添加以下内容

```
JAVA_HOME="/Library/Java/JavaVirtualMachines/jdk-11.jdk/Contents/Home"
export JAVA_HOME
CLASS_PATH="$JAVA_HOME/lib"
PATH=".$PATH:$JAVA_HOME/bin"

```

```
JAVA_HOME="/Library/Java/JavaVirtualMachines/jdk-11.jdk/Contents/Home"
export JAVA_HOME
CLASS_PATH="$JAVA_HOME/lib"
PATH=".$PATH:$JAVA_HOME/bin"

```

<figure><img src="../../../.gitbook/assets/image (175).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (191).png" alt=""><figcaption></figcaption></figure>

按ESC，进入保存。

之后按住shfit+:(冒号)，输入 :wq! 保存【一定记得是：shfiti+冒号进入，冒号+wq(小写)+叹号】，之后回车保存

<figure><img src="../../../.gitbook/assets/image (172).png" alt=""><figcaption></figcaption></figure>

保存成功之后会回到终端

{% hint style="danger" %}
如果出现了这个报错，点击回车之后再输入上述内容
{% endhint %}

<figure><img src="../../../.gitbook/assets/image (181).png" alt=""><figcaption></figcaption></figure>

* 输入source /etc/profile，JAVA环境变量配置生效

```
source /etc/profile
```

