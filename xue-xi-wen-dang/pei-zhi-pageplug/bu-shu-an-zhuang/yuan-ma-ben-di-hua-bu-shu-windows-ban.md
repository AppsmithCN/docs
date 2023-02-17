# 源码本地化部署（windows版）



## 1、前置准备

PagePlug 后端启动需要 Jdk11、Maven3、一个Mongo实例和一个Redis实例，请检查下电脑是否已经部署好，如果还没有的话，可以查看下面教程安装

### &#x20;   1.1 配置Java—OpenJSDK11

#### &#x20;       1.1.1下载JDK11

* 官网地址[https://jdk.java.net/archive/](https://jdk.java.net/archive/)
* 下载地址[https://download.java.net/java/GA/jdk11/9/GPL/openjdk-11.0.2\_windows-x64\_bin.zip](https://download.java.net/java/GA/jdk11/9/GPL/openjdk-11.0.2\_windows-x64\_bin.zip)

<figure><img src="../../../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>



#### &#x20;       1.1.2创建文件夹解压

* 在自己本地的磁盘，创建一个文件夹，例如叫java

<figure><img src="../../../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

* 将下载好的jdk-11.0.2解压到文件夹下

<figure><img src="../../../.gitbook/assets/image (77).png" alt=""><figcaption></figcaption></figure>

#### &#x20;       1.1.3配置环境变量

* 打开电脑设置，左下角菜单选择<mark style="color:red;">**关于**</mark>，右侧选择<mark style="color:red;">**高级系统配置**</mark>，系统属性中选择<mark style="color:red;">**高级系统设置**</mark>

<figure><img src="../../../.gitbook/assets/image (67).png" alt=""><figcaption></figcaption></figure>

* 在系统变量中，选择<mark style="color:red;">**新建**</mark>

<figure><img src="../../../.gitbook/assets/image (62).png" alt=""><figcaption></figcaption></figure>

* 之后编辑变量名和变量值

变量名可以填写：JAVA\_HOME

变量值填写jdk的安装目录（可以通过浏览目录，找到jdk的文件夹）

<figure><img src="../../../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>

* 配置好后，点击确定，再系统变量中找到Path，点击编辑

<figure><img src="../../../.gitbook/assets/image (91).png" alt=""><figcaption></figcaption></figure>

* 点击新建，将下面命令输入进Path值

```
%JAVA_HOME%\bin
```

<figure><img src="../../../.gitbook/assets/image (81).png" alt=""><figcaption></figcaption></figure>

之后点击确定，变量就配置好了



#### &#x20;       1.1.4 测试JDK是否安装成功

* 打开命令行窗口即CMD命令，输入java或者javac都可以

```
java
```

```
javac
```

<figure><img src="../../../.gitbook/assets/image (69).png" alt=""><figcaption></figcaption></figure>

出现这样一堆东西，环境已经配置好了



### &#x20;   1.2配置Maven版本在3以上（最好是3.6）

#### &#x20;       1.2.1下载

* 官网地址：[https://maven.apache.org/download.cgi](https://maven.apache.org/download.cgi)

根据不同的版本，选择对应的文件，windows选择zip的压缩包

<figure><img src="../../../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

#### &#x20;         1.2.2创建文件夹解压

* 在自己本地的磁盘，创建一个文件夹，例如叫java

<figure><img src="../../../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

* 将下载好的apache-maven-3.9.0解压到java文件夹下

<figure><img src="../../../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>

#### &#x20;       1.2.3配置环境变量



* 打开电脑设置，左下角菜单选择<mark style="color:red;">**关于**</mark>，右侧选择<mark style="color:red;">**高级系统配置**</mark>，系统属性中选择<mark style="color:red;">**高级系统设置**</mark>

<figure><img src="../../../.gitbook/assets/image (67).png" alt=""><figcaption></figcaption></figure>

* 在系统变量中，选择<mark style="color:red;">**新建**</mark>

<figure><img src="../../../.gitbook/assets/image (62).png" alt=""><figcaption></figcaption></figure>

* 之后编辑变量名和变量值

变量名可以填写：MAVEN\_HOME

变量值填写maven的安装目录（可以通过浏览目录，找到maven的文件夹）

<figure><img src="../../../.gitbook/assets/image (71).png" alt=""><figcaption></figcaption></figure>

* 配置好后，点击确定，再系统变量中找到Path，点击编辑

<figure><img src="../../../.gitbook/assets/image (91).png" alt=""><figcaption></figcaption></figure>

* 点击新建，将下面命令输入进Path值

```
%MAVEN_HOME%\bin
```

<figure><img src="../../../.gitbook/assets/image (54).png" alt=""><figcaption></figcaption></figure>

之后点击确定，变量就配置好了

#### &#x20;       1.2.4 测试MAVEN是否安装成功

* 打开命令行窗口即CMD命令，输入

```
mvn -v
```

<figure><img src="../../../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

显示版本号证明环境已经配置好了

### &#x20;   1.3配置mongoDB数据库(自身已有redis数据库，可忽略此步骤)

{% hint style="info" %}
PagePlug的数据结构对Mongo会有一些要求，Methodot部署的Mongo建议是空数据内容或者自行优化适配Pageplug的数据结构
{% endhint %}



### &#x20;   1.4配置redis数据库（自身已有redis数据库，可忽略此步骤）

* 打开Methodot官网，从工作台中进入到应用商店，找到redis商品

```
www.methodot.com
```

<figure><img src="../../../.gitbook/assets/image (75).png" alt=""><figcaption></figcaption></figure>

* 选择部署

<figure><img src="../../../.gitbook/assets/image (79).png" alt=""><figcaption></figcaption></figure>

* 配置redis，支持自定义域名，选择立即部署

<figure><img src="../../../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

* 部署成功，可以使用

<figure><img src="../../../.gitbook/assets/image (87).png" alt=""><figcaption></figcaption></figure>

### &#x20;   1.5git安装（如果已经有了，可忽略此步骤）

* 点击下方链接下载git

> [ https://github.com/git-for-windows/git/releases/download/v2.38.1.windows.1/Git-2.38.1-\
> 64-bit.exe](https://github.com/git-for-windows/git/releases/download/v2.38.1.windows.1/Git-2.38.1-64-bit.exe)

* 安装在电脑的磁盘，配置可以根据个人使用喜好选择，仅供参考

<figure><img src="../../../.gitbook/assets/image (158).png" alt=""><figcaption></figcaption></figure>

* 安装成功

<figure><img src="../../../.gitbook/assets/image (168).png" alt=""><figcaption></figcaption></figure>

### 1.6配置Rsync工具

build.sh 脚本中用到了 rsync 工具，启动前请确保系统中已经安装了 rsync，Windows环境配置sync请看

* 可以点击下方链接下载usr文件

{% hint style="info" %}
链接：https://pan.baidu.com/s/1gKAps-7bLYGFfxiJJ5ANUw&#x20;

提取码：dwfs
{% endhint %}

<figure><img src="../../../.gitbook/assets/image (161).png" alt=""><figcaption></figcaption></figure>

* usr文件夹里面可能包含 `bin`、`lib`、`share` ，将 `usr` 文件拷贝到 Git 安装目录下即可

例如我的在C盘，/Program Files/Git

<figure><img src="../../../.gitbook/assets/image (153).png" alt=""><figcaption></figcaption></figure>

## 2、源码拉取下载

{% hint style="danger" %}
避免因权限问题导致下载失败或拉取失败，在使用git拉取的时候，<mark style="color:red;">**以管理员身份来运行使用**</mark>
{% endhint %}

### 2.1创建源码文件夹



* 我们可以在任意磁盘创建一个文件夹，例如在D盘创建一个work

<figure><img src="../../../.gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>

### 2.2打开git bash下载

* 打开git bash，进入源码文件夹所在的D盘，输入以下命令

```
cd d:
```

<figure><img src="../../../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>

* 之后我们可以再进入D盘下的work文件夹，输入以下命令

```
cd work
```

<figure><img src="../../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

* 之后我们可以输入这个命令，查下文件夹下有无其他文件

```
ll
```

<figure><img src="../../../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

* 复制git或者是github的地址下载

```
https://gitee.com/cloudtogo/pageplug.git
```

<figure><img src="../../../.gitbook/assets/image (50).png" alt=""><figcaption><p>gitee的地址</p></figcaption></figure>

```
https://github.com/cloudtogo/pageplug.git
```

<figure><img src="../../../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

输入以下的命令，下载源码（以gitee为例）

```
git clone https://gitee.com/cloudtogo/pageplug.git
```

<figure><img src="../../../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

* 显示下面内容的时候，源码拉取成功

<figure><img src="../../../.gitbook/assets/image (59).png" alt=""><figcaption></figcaption></figure>

## 3、后端部署

### &#x20;   3.1检查maven在编译器的配置

* 点击左上角File—settings

<figure><img src="../../../.gitbook/assets/image (80).png" alt=""><figcaption></figcaption></figure>

* 左上角搜索框搜索maven，检查下Maven home path、User settings file、Local repository是否配置有误

Maven home Path中填写Maven安装目录的位置

<figure><img src="../../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

User settings file的文件在maven目录中，/conf/logging

<figure><img src="../../../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

Local repository可以修改或者不修改，默认在C盘，如果担心C盘存量不够，建议更换目录（我在D盘创建了一个空的local文件夹）

<figure><img src="../../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

配置没啥问题后，我们按照从IDEA中打开源文件

### &#x20; 3.2打开Pageplug文件

* 进入IDEA，我们将下载的源码从文件夹中打开

<figure><img src="../../../.gitbook/assets/image (78).png" alt=""><figcaption></figcaption></figure>

* 等待几分钟加载，之后点击下方Terminal，进入Git Bash

<figure><img src="../../../.gitbook/assets/image (58).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (65).png" alt=""><figcaption></figcaption></figure>

我们将开始按照教程依次操作

### &#x20;   3.3打开及配置工程文件

<figure><img src="../../../.gitbook/assets/image (56).png" alt=""><figcaption></figcaption></figure>

* 首先进入到app文档，输入以下命令

```
cd app
```

<figure><img src="../../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

* 再进入到server文档，输入以下命令

```
cd server
```

<figure><img src="../../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

* 按照步骤提示，我们需要创造一个步骤文件，输入以下命令

```Plaintext
cp envs/dev.env.example .env
```

<figure><img src="../../../.gitbook/assets/image (72).png" alt=""><figcaption></figcaption></figure>

* 接下来我们打开env，配置环境变量，文件路径/app/server/scripts/.env

&#x20;     对mongo和redis的地址进行修改

<figure><img src="../../../.gitbook/assets/image (64).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
<pre><code><strong>如果需要小程序预览功能，可以在这里，需要配置你的小程序信息
</strong>CLOUDOS_WECHAT_APPID=""
CLOUDOS_WECHAT_SECRET=""
</code></pre>
{% endhint %}

* 按照模版格式替换地址

<figure><img src="../../../.gitbook/assets/image (82).png" alt=""><figcaption></figcaption></figure>

如果没有[**mongo**](yuan-ma-ben-di-hua-bu-shu-windows-ban.md#1.3-pei-zhi-mongodb-shu-ju-ku)和[**redis**](yuan-ma-ben-di-hua-bu-shu-windows-ban.md#1.4-pei-zhi-redis-shu-ju-ku)，可以在methodot上部署生成使用，教程可以往上看

<figure><img src="../../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

### &#x20;   3.4构建Java服务

* 我们在git bash下，输入以下命令

```Python
mvn clean compile
```

<figure><img src="../../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

等待一会时间，成功后有提示

<figure><img src="../../../.gitbook/assets/image (55).png" alt=""><figcaption></figcaption></figure>

* **build.sh 脚本中用到了 rsync 工具，启动前请确保系统中已经安装了 rsync，否则执行命令会有提醒**

<figure><img src="../../../.gitbook/assets/image (48).png" alt=""><figcaption></figcaption></figure>

Windows环境安装 rsync ，可以点击下方链接

```
http://mysoft.6h5.cn/win/rsync.64.zip
```

下载完成后，解压压缩包，找到<mark style="color:red;">**`rsync.exe`**</mark>，把这个文件拷贝到Git Bash目录<mark style="color:red;">**`C:\Program Files\Git\usr\bin`**</mark>即可在Git Bash上使用了。

<figure><img src="../../../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>

* 继续操作，输入第二个命令

```
bash ./build.sh -DskipTests
```

<figure><img src="../../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

安装成功之后会有下面的提醒

<figure><img src="../../../.gitbook/assets/image (17) (1).png" alt=""><figcaption></figcaption></figure>

* 检查是否有了dist文件夹

<figure><img src="../../../.gitbook/assets/image (150).png" alt=""><figcaption></figcaption></figure>

### 3.5启动java服务

* 输入第三个命令

```Bash
bash ./scripts/start-dev-server.sh
```

<figure><img src="../../../.gitbook/assets/image (63).png" alt=""><figcaption></figcaption></figure>

看到appsmith is running就是成功了

<figure><img src="../../../.gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>





## 4、前端部署

### &#x20;    4.1启动本地 nginx docker

* 我们新建一个git bash，输入以下命令，进入pageplug文件夹

```
cd pageplug
```

<figure><img src="../../../.gitbook/assets/image (145).png" alt=""><figcaption></figcaption></figure>

* 输入以下命令，进入app文件夹

```
cd app
```

<figure><img src="../../../.gitbook/assets/image (170).png" alt=""><figcaption></figcaption></figure>

* 输入以下命令，进入client文件夹

```
cd client
```

<figure><img src="../../../.gitbook/assets/image (169).png" alt=""><figcaption></figcaption></figure>

* 输入以下命令，启动nginx

```
yarn start-proxy
```

<figure><img src="../../../.gitbook/assets/image (154).png" alt=""><figcaption></figcaption></figure>

{% hint style="danger" %}
如果原来电脑没有拉取过nginx，首先会拉取nginx image；同时也需要保证你本地的443端口没有被占有
{% endhint %}

<figure><img src="../../../.gitbook/assets/image (148).png" alt=""><figcaption></figcaption></figure>

* 显示Done的时候，已经顺利启动

<figure><img src="../../../.gitbook/assets/image (164).png" alt=""><figcaption></figcaption></figure>

👇Docker里面的nginx容器启动成功👇

<figure><img src="../../../.gitbook/assets/image (171).png" alt=""><figcaption></figcaption></figure>

### &#x20;   4.2安装依赖

* 输入以下命令

```
yarn
```

<figure><img src="../../../.gitbook/assets/image (144).png" alt=""><figcaption></figcaption></figure>

* 等待几分钟，最终显示如下

<figure><img src="../../../.gitbook/assets/image (152).png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
yarn 安装依赖，有可能会遇到网络问题，可以参考[https://segmentfault.com/a/1190000017419993](https://segmentfault.com/a/1190000017419993)

设置npm源
{% endhint %}

{% hint style="success" %}
yarn 安装依赖， 提示报错 “cross-env找不到”，可以将package.json 的脚本里面的<mark style="color:purple;">cross-env</mark>替换成 <mark style="color:purple;">set</mark>
{% endhint %}

{% hint style="danger" %}
安装过程中，如果遇到@sentry/cli或者node-sass依赖找不到的

可以参照这个地址[https://blog.csdn.net/qq\_31201781/article/details/106147842'](https://blog.csdn.net/qq\_31201781/article/details/106147842')

单独设置镜像地址
{% endhint %}

{% hint style="danger" %}
如果遇到@shared/ast找不到问题，其实就是本地包的之前，需要 yarn link 建立软链接
{% endhint %}

<figure><img src="../../../.gitbook/assets/image (151).png" alt=""><figcaption></figcaption></figure>

可以参考如下操作

```
cd shared/ast 
yarn run link-package
cd client
yarn link @shared/ast
```



### &#x20;   4.3启动前端服务

* 输入以下命令，启动前端服务

```
yarn start-win
```

<figure><img src="../../../.gitbook/assets/image (166).png" alt=""><figcaption></figcaption></figure>

* 等待几分钟，最终显示如下，出现warings可以忽略

<figure><img src="../../../.gitbook/assets/image (163).png" alt=""><figcaption></figcaption></figure>

### 4.检查是否成功

* 访问下面的地址，页面会显示如下

```
dev.appsmith.com
```

{% hint style="info" %}
确保你的机器的host，已经配置了映射关系

127.0.0.1  dev.appsmith.com
{% endhint %}
