---
description: >-
  PagePlug
  是一款帮助企业应用开发更便捷的软件，可快速创建内部应用程序。使用我们基于JavaScript的可视化开发平台，构建CRUD应用程序、仪表板、管理面板等的速度提高10倍。
  您可以使用我们预先构建的UI小部件，将它们连接到您的API和数据库，以构建动态应用程序和复杂的工作流程。旨在为企业提供一套成本更低、人效更佳的开发方式。
---

# 介绍

<figure><img src=".gitbook/assets/image (6).png" alt=""><figcaption><p>pageplug.cn</p></figcaption></figure>

### 1、​您可以使用PagePlug做什么？​ <a href="#nin-ke-yi-shi-yong-appsmith-zuo-shen-me" id="nin-ke-yi-shi-yong-appsmith-zuo-shen-me"></a>

以下是Pageplug的前五个用例：

* **连接任何数据源**: 与数据库或 API 等数据源集成。PagePlug 对许多数据库和 RESTful API 接口提供即插即用支持，可与大多数工具无缝连接。
* **构建 UI**：使用可自定义的内置小部件来构建应用程序布局。
* **访问数据**：通过编写查询并将数据绑定到小部件，将 UI 连接到数据源。用 JavaScript 控制一切。
* **协作、部署、共享：**PagePlug还支持使用 Git 进行版本控制，以跟踪更改、创建回滚并使用 git 分支进行协作。部署应用程序并与其他用户共享。

通过这些简单的步骤，您可以为复杂的多步骤工作流创建简单的 CRUD 应用程序。PagePlug 可以轻松构建与任何数据源对话的 UI。观看这个5分钟的视频，了解如何使用 PagePlug。[去bilibili观看中文字幕版](https://www.bilibili.com/video/BV1dg411Q7PG?zw\&vd\_source=1a6805ecebcf8f2c6ac95a3bc7c11495)​入门教程**（可以点个赞和收藏多支持下哟）**

{% embed url="https://www.bilibili.com/video/BV1dg411Q7PG?t=0.0" %}

### 2、Demo项目体验： <a href="#chuang-jian-zhang-hu" id="chuang-jian-zhang-hu"></a>

&#x20;   **2.1工程管理系统demo**

{% embed url="https://lowcode.methodot.com/applications/6322a1453892ca140cb874d5/pages/6322a1453892ca140cb874e3" %}

&#x20; **2.2企业CRM系统demo**

{% embed url="https://lowcode.methodot.com/applications/6322a6d63892ca140cb87551/pages/6322a6d63892ca140cb87555?embed=1" %}



### 3、快速开始 <a href="#chuang-jian-zhang-hu" id="chuang-jian-zhang-hu"></a>

[🌈 线上稳定SaaS版本，**Methodot（推荐）**](she-zhi-pageplug/saas-ban-pageplug.md)****

<figure><img src=".gitbook/assets/image (11).png" alt=""><figcaption><p>methodot.com</p></figcaption></figure>

🌱 私有部署【Docker】（推荐）

> **最低服务器配置：4G内存 + 2核CPU**

```
// 获取安装脚本
curl -O https://raw.githubusercontent.com/cloudtogo/pageplug/open/install.sh

// 赋予运行权限
chmod +x install.sh

// 执行安装脚本
./install.sh
```

#### 🎈 本地开发

PagePlug 代码位于 /app 目录下，主要目录分别是：

* /client -- React 前端项目，使用 create-react-app 脚手架生成，负责低代码的编辑器和 web 端展示
* /server -- Java 后端项目，使用 Spring WebFlux 框架，负责低代码的后端服务、各种数据源的代理
* /taro -- Taro 移动端项目，使用 Taro 跨平台方案实现移动端对低代码 DSL 的解析和展示

**PagePlug 前端启动**

PagePlug 前端项目使用 Nginx 作为网关，并且 Nginx 使用 Docker 运行，所以在运行之前请确保已安装 [Docker](https://www.docker.com/get-started/) ，下面的启动命令仅针对 **Windows** 环境，非Windows环境请参考[官方指南](https://github.com/AppsmithCN/pageplug/blob/open/contributions/ClientSetup.md)。

```
// 配置 host
127.0.0.1 dev.appsmith.com

// 环境变量
cp .env.example .env

// 启动本地 nginx docker
cd app/client
yarn start-proxy

// 启动前端服务
yarn
yarn start-win
```

顺利启动后，访问 [https://dev.appsmith.com](https://dev.appsmith.com/) 预览效果。



**PagePlug 后端启动**

PagePlug 后端启动需要 Jdk11、Maven3、一个Mongo实例和一个Redis实例，具体操作请参考[官方指南](https://github.com/AppsmithCN/pageplug/blob/open/contributions/ServerSetup.md)。下面的启动命令仅针对 **Windows** 环境，Windows环境运行脚本需要借助 bash 命令，非 Windows 环境下直接运行脚本即可。

> **注意**：build.sh 脚本中用到了 rsync 工具，启动前请确保系统中已经安装了 rsync，Windows环境安装 rsync 请看[这里](https://xindot.com/2019/08/13/add-rsync-to-git-bash-for-windows/)。

```
// 使用 IDEA 打开工程
app/server

// 创建环境变量文件
cp envs/dev.env.example .env

// 打开.env，配置环境变量
APPSMITH_MONGODB_URI="你的Mongo实例地址"
APPSMITH_REDIS_URL="你的Redis实例地址"

// 构建 java 服务
mvn clean compile
bash ./build.sh -DskipTests

// 启动 java 服务
bash ./scripts/start-dev-server.sh
```

**PagePlug 移动端启动**

PagePlug 移动端是一个 [Taro](https://github.com/NervJS/taro) 项目，天然地支持多端小程序、H5和React Native，但是，目前 PagePlug 仅支持微信小程序，微信小程序的预览和发布需要使用微信开发者工具、小程序账号，开发前请先查看[微信小程序官方指南](https://developers.weixin.qq.com/miniprogram/dev/framework/quickstart/getstart.html)。\
PagePlug 移动端组件采用 [Taroify](https://github.com/mallfoundry/taroify) UI组件库打造。

```
cd app/taro

打开 config/dev.js 配置开发参数

// PagePlug 后端接口地址，本地开发时需要填写本机IP地址
API_BASE_URL: '"http://192.168.xxx.xxx:8080/api/"'

// 小程序默认展示的应用ID，你可以从应用的url中找到应用ID：/app/[应用ID]/page/[页面ID]
DEFAULT_APP: '"应用ID"'

// 启动 Taro 项目
yarn
yarn dev:weapp
```

### ​[帮助中心](https://appsmith-fans.cn/docs/introduction?id=%e5%b8%ae%e5%8a%a9%e4%b8%ad%e5%bf%83)​ <a href="#bang-zhu-zhong-xin" id="bang-zhu-zhong-xin"></a>

* 查看我们的[常见问题解答](https://docs.appsmith.com/faq)，您可能会在此处找到问题的解答；
* 寻找具体信息？试试[小部件参考](https://docs.appsmith.com/reference/widgets)，[框架参考](https://docs.appsmith.com/reference/appsmith-framework)或[数据源参考](https://docs.appsmith.com/core-concepts/connecting-to-data-sources/connecting-to-databases#supported-databases) ；
* 在B站上查看我们的指南和教程；
* ​[通过Github 问题](https://github.com/appsmithorg/appsmith/issues)向PagePlug报告错误

**如果您仍然遇到任何问题，可以加入我们技术交流群，直接与PagePlug产品静静联系!**

<figure><img src=".gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>
