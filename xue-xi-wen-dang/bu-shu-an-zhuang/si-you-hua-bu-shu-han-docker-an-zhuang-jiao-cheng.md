# 私有化部署（含docker安装教程）

## 1、Windows版

Docker Desktop for Windows 支持 64 位版本的 Windows 10 Pro，且必须开启 Hyper-V（若版本为 v1903 及以上则无需开启 Hyper-V），或者 64 位版本的 Windows 10 Home v1903 及以上版本。



* 检查下自己的Hyper-v是否开启

打开Windows设置—搜索“hyper”，点击启用或关闭windows功能

<figure><img src="../../.gitbook/assets/image (165).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (156).png" alt=""><figcaption></figcaption></figure>

* 检查下虚拟化是否开启

打开任务管理器——选择性能tab

<figure><img src="../../.gitbook/assets/image (167).png" alt=""><figcaption></figcaption></figure>

### &#x20;   1.1 docker安装

* 下载docker

可以点击该👉 [链接](https://desktop.docker.com/win/main/amd64/Docker%20Desktop%20Installer.exe) 下载 Docker Desktop for Windows，下载好之后双击 `Docker Desktop Installer.exe` 开始安装。

<figure><img src="../../.gitbook/assets/image (160).png" alt=""><figcaption></figcaption></figure>

* 如果遇到WSL的报错，需要对WSL做个升级

<figure><img src="../../.gitbook/assets/image (149) (1).png" alt=""><figcaption></figcaption></figure>

打开cmd，输入以下命令：

```
wsl --install
```

<figure><img src="../../.gitbook/assets/image (155).png" alt=""><figcaption></figcaption></figure>

* 更多wsl的问题，可查阅官方文档处理：

{% hint style="info" %}
[https://learn.microsoft.com/zh-cn/windows/wsl/install](https://learn.microsoft.com/zh-cn/windows/wsl/install)
{% endhint %}



* 安装完成（避免运行限制，请以管理员的身份运行docker）

<figure><img src="../../.gitbook/assets/image (146).png" alt=""><figcaption></figcaption></figure>

* 或者可以运行下面命令，看docker是否能正常工作

```
docker version
```

<figure><img src="../../.gitbook/assets/image (162).png" alt=""><figcaption></figcaption></figure>

* 配置国内加速器，可以添加在Docker Engine下

```
"registry-mirrors": ["https://docker.mirrors.ustc.edu.cn"]
```

<figure><img src="../../.gitbook/assets/image (159).png" alt=""><figcaption></figcaption></figure>

### &#x20;   1.2部署启动应用

{% hint style="info" %}
**小Tips：**

当前部署方法使用docker和docker-compose

在运行前请确保你已正确安装了docker环境，并且确保当前环境<mark style="color:red;">**80端口和443端口**</mark>没有被其他应用占用
{% endhint %}



Docker安装完后，之后我们点击下方链接，点击下载**docker-compose.yml**



{% embed url="https://lowcode.methodot.com/app/pageplug/page1-63160074cb370d532de7f2af?embed=1" %}

<figure><img src="../../.gitbook/assets/image (135) (1).png" alt=""><figcaption></figcaption></figure>

1、首先我们现在D盘（或者任意一个磁盘）创建一个PagePlug的文件夹

<figure><img src="../../.gitbook/assets/image (106) (1) (1).png" alt=""><figcaption></figcaption></figure>

2、将下载的**docker-compose.yml**文件放入到pageplug文件夹中

<figure><img src="../../.gitbook/assets/image (121) (1).png" alt=""><figcaption></figcaption></figure>

3、按WIN+R进入运行窗口，打开cmd窗口

<figure><img src="../../.gitbook/assets/image (128).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (133).png" alt=""><figcaption></figcaption></figure>

4、在CMD窗口中，我们先进入到D盘，再进入到pageplug文件夹中（如果在其他盘，演示操作相同），输入如下：

```
d:
```

<figure><img src="../../.gitbook/assets/image (143).png" alt=""><figcaption></figcaption></figure>

5、之后我们进入到pageplug文件夹，目录下输入如下：

```
cd pageplug
```

<figure><img src="../../.gitbook/assets/image (105) (1).png" alt=""><figcaption></figcaption></figure>

6、之后我们将下列命令拷贝输入，回车

```
docker-compose up -d
```

<figure><img src="../../.gitbook/assets/image (129) (1).png" alt=""><figcaption></figcaption></figure>

7、会进入下载状态，耐心稍等几分钟

<figure><img src="../../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>

8、下载成功后，会看到如下提示，代表已经部署成功

<figure><img src="../../.gitbook/assets/image (3) (1) (2).png" alt=""><figcaption></figcaption></figure>

{% hint style="danger" %}
如果在部署的时候看到<mark style="color:red;">**Access is denied**</mark>提醒，是文件夹的权限不够，需求修改下
{% endhint %}

<figure><img src="../../.gitbook/assets/image (76).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
点击文件夹右键——属性——安全，对组和对象权限进行修改
{% endhint %}

<figure><img src="../../.gitbook/assets/image (73) (1).png" alt=""><figcaption></figcaption></figure>

9、之后打开浏览器输入<mark style="color:red;">**localhost**</mark>，就会看到下面的页面，PagePlug启动成功了

<figure><img src="../../.gitbook/assets/image (46).png" alt=""><figcaption></figcaption></figure>

10、点击开始吧，之后填写邮箱密码资料创建

<figure><img src="../../.gitbook/assets/image (24) (2).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (83).png" alt=""><figcaption></figcaption></figure>



点击创建你的第一个应用，开始对PagePlug操作吧～～

<figure><img src="../../.gitbook/assets/image (74).png" alt=""><figcaption></figcaption></figure>



## 2、Mac版



### 2.1docker安装



确认下自己电脑的配置是英特尔芯片或者是M1及以上的，选择不同对应的版本，[点击下载](https://docs.docker.com/desktop/install/mac-install/)

<figure><img src="../../.gitbook/assets/image (52).png" alt=""><figcaption></figcaption></figure>

如同 macOS 其它软件一样，安装也非常简单，双击下载的 `.dmg` 文件，然后将那个鲸鱼图标拖拽到 `Application` 文件夹即可（其间需要输入用户密码）

<figure><img src="../../.gitbook/assets/image (89).png" alt=""><figcaption></figcaption></figure>

之后在应用中找到Docker图标并点击运行

<figure><img src="../../.gitbook/assets/image (5) (3).png" alt=""><figcaption></figcaption></figure>

之后，你可以在终端通过命令检查安装后的 Docker 版本

```
docker --version
```

如果 `docker version`、`docker info` 都正常的话，可以尝试运行一个 Nginx 服务器：

```
docker run -d -p 80:80 --name webserver nginx
```

<figure><img src="../../.gitbook/assets/image (60).png" alt=""><figcaption></figcaption></figure>

服务运行后，可以访问 [http://localhost](http://localhost)，如果看到了 "Welcome to nginx!"，就说明 Docker Desktop for Mac 安装成功了。

<figure><img src="../../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>

小提示：可以配置下镜像加速器，复制如下代码到<mark style="color:red;">**Docker Engine**</mark>

```

  "registry-mirrors": ["https://docker.mirrors.ustc.edu.cn"]

```

<figure><img src="../../.gitbook/assets/image (85).png" alt=""><figcaption></figcaption></figure>

将代码复制进Docker Engine中

```
// Some code
```

<figure><img src="../../.gitbook/assets/image (10) (3) (1).png" alt=""><figcaption></figcaption></figure>

左下角显示绿色的时候，就证明配置好了，接下来我们将准备启动应用



### 2.2部署启动应用



Docker安装完后，之后我们点击下方链接，点击下载**docker-compose.yml**

{% embed url="https://lowcode.methodot.com/app/pageplug/page1-63160074cb370d532de7f2af?embed=1" %}

<figure><img src="../../.gitbook/assets/image (135) (1).png" alt=""><figcaption></figcaption></figure>

**1、我们可以先在桌面端创建一个pageplug文件夹**

![](<../../.gitbook/assets/image (88).png>)



**2、将下载的docker-compose.yml文件放入到pageplug文件夹中**

<figure><img src="../../.gitbook/assets/image (70).png" alt=""><figcaption></figcaption></figure>

**3、在pageplug文件中，右键点击**<mark style="color:red;">**“新建位于文件夹位置的终端窗口”**</mark>

<figure><img src="../../.gitbook/assets/image (25) (1) (2).png" alt=""><figcaption></figcaption></figure>

**4、在终端输入以下命令，回车，就会开始进入下载**

```
docker-compose up -d
```

<figure><img src="../../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

**过程中可能会要授权访问文件夹的文件，点击“好”**

<figure><img src="../../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

**5、最终出现Pageplug started的时候，Pageplug部署成功**

<figure><img src="../../.gitbook/assets/image (2) (3) (1).png" alt=""><figcaption></figcaption></figure>



**6、之后打开浏览器输入**<mark style="color:red;">**localhost**</mark>**，就会看到下面的页面，PagePlug启动成功了**

<figure><img src="../../.gitbook/assets/image (61).png" alt=""><figcaption></figcaption></figure>

**7、点击开始吧，之后填写邮箱密码资料创建**

<figure><img src="../../.gitbook/assets/image (24) (2).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (83).png" alt=""><figcaption></figcaption></figure>



**点击创建你的第一个应用，开始你的低代码之旅吧～～**

<figure><img src="../../.gitbook/assets/image (74).png" alt=""><figcaption></figcaption></figure>





