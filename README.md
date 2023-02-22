---
description: >-
  PagePlug
  是一款帮助企业应用开发更便捷的软件，可快速创建内部应用程序。使用我们基于JavaScript的可视化开发平台，构建CRUD应用程序、仪表板、管理面板等的速度提高10倍。
  您可以使用我们预先构建的UI小部件，将它们连接到您的API和数据库，以构建动态应用程序和复杂的工作流程。旨在为企业提供一套成本更低、人效更佳的开发方式。
---

# 核心介绍



<figure><img src=".gitbook/assets/image (6) (1) (1).png" alt=""><figcaption><p>pageplug.cn</p></figcaption></figure>

## 1、​您可以使用PagePlug做什么？​ <a href="#nin-ke-yi-shi-yong-appsmith-zuo-shen-me" id="nin-ke-yi-shi-yong-appsmith-zuo-shen-me"></a>

以下是Pageplug的前五个用例：

* **连接任何数据源**: 与数据库或 API 等数据源集成。PagePlug 对许多数据库和 RESTful API 接口提供即插即用支持，可与大多数工具无缝连接。
* **构建 UI**：使用可自定义的内置小部件来构建应用程序布局。
* **访问数据**：通过编写查询并将数据绑定到小部件，将 UI 连接到数据源。用 JavaScript 控制一切。
* **协作、部署、共享：**PagePlug还支持使用 Git 进行版本控制，以跟踪更改、创建回滚并使用 git 分支进行协作。部署应用程序并与其他用户共享。

数据库是每个应用程序的重要组成部分，用于存储和管理数据。在 PagePlug 上，您可以直接连接到支持的数据库并运行查询以在PagePlug查询编辑器上读取和写入数据。





通过这些简单的步骤，您可以为复杂的多步骤工作流创建简单的 CRUD 应用程序。PagePlug 可以轻松构建与任何数据源对话的 UI。观看这个5分钟的视频，了解如何使用 PagePlug。[去bilibili观看中文字幕版](https://www.bilibili.com/video/BV1dg411Q7PG?zw\&vd\_source=1a6805ecebcf8f2c6ac95a3bc7c11495)​入门教程**（可以点个赞和收藏多支持下哟）**

{% embed url="https://www.bilibili.com/video/BV1dg411Q7PG?t=0.0" %}

## 2、Demo项目体验： <a href="#chuang-jian-zhang-hu" id="chuang-jian-zhang-hu"></a>

&#x20;   **2.1工程管理系统demo**

{% embed url="https://lowcode.methodot.com/applications/6322a1453892ca140cb874d5/pages/6322a1453892ca140cb874e3" %}

&#x20; **2.2企业CRM系统demo**

{% embed url="https://lowcode.methodot.com/applications/6322a6d63892ca140cb87551/pages/6322a6d63892ca140cb87555?embed=1" %}

* 在右侧菜单中选择导入即可体验

<figure><img src=".gitbook/assets/image (1) (3).png" alt=""><figcaption></figcaption></figure>



## 3、快速开始 <a href="#chuang-jian-zhang-hu" id="chuang-jian-zhang-hu"></a>

### 🌱3.1 线上稳定SaaS版本，**Methodot（推荐）**

<figure><img src=".gitbook/assets/image (11) (1) (1).png" alt=""><figcaption><p>methodot.com</p></figcaption></figure>

<figure><img src=".gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
使用教程，请点击这里：[**线上PagePlug体验**](xue-xi-wen-dang/bu-shu-an-zhuang/xian-shang-pageplugsaas-ban.md)****
{% endhint %}

### 🌱3.2私有部署【Docker】



> **最低服务器配置：4G内存 + 2核CPU**

```
// 获取安装脚本
curl -O https://raw.githubusercontent.com/cloudtogo/pageplug/open/install.sh

// 赋予运行权限
chmod +x install.sh

// 执行安装脚本
./install.sh
```

{% hint style="info" %}
详细安装教程，请点击这里：[**私有化部署（含docker安装教程）**](xue-xi-wen-dang/bu-shu-an-zhuang/si-you-hua-bu-shu-han-docker-an-zhuang-jiao-cheng.md)****
{% endhint %}

### &#x20;  🌱 3.3本地开发

PagePlug 代码位于 /app 目录下，主要目录分别是：

* /client -- React 前端项目，使用 create-react-app 脚手架生成，负责低代码的编辑器和 web 端展示
* /server -- Java 后端项目，使用 Spring WebFlux 框架，负责低代码的后端服务、各种数据源的代理
* /taro -- Taro 移动端项目，使用 Taro 跨平台方案实现移动端对低代码 DSL 的解析和展示

&#x20;       **😎 PagePlug 前端启动**

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



&#x20;       **😎PagePlug 后端启动**

PagePlug 后端启动需要 Jdk11、Maven3、一个Mongo实例和一个Redis实例，具体操作请参考[官方指南](https://github.com/AppsmithCN/pageplug/blob/open/contributions/ServerSetup.md)。下面的启动命令仅针对 **Windows** 环境，Windows环境运行脚本需要借助 bash 命令，非 Windows 环境下直接运行脚本即可。

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

****

&#x20;       **😎PagePlug 移动端启动**

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

{% hint style="info" %}
详细安装教程，请点击这里：[**源码本地化部署（windows版）**](xue-xi-wen-dang/bu-shu-an-zhuang/yuan-ma-ben-di-hua-bu-shu-windows-ban.md)****
{% endhint %}



## 4、参与PagePlug开源

{% hint style="info" %}
💪🏻PagePlug的发展进步，离不开社区、开源小组每一位成员的努力及付出

我们始终保持初心，希望能够通过更便捷跟快速的工具，提升应用的开发效率

<mark style="color:red;">**“应用的开发，本该那么高效及简单”**</mark>



💡如果你曾经有过这样的想法：

* 想提升自身个人代码质量，更加简洁、干净、规范
* 有开源项目傍身，获得更广阔的职业机会及职业发展空间
* 成为某方面领域的KOL，建立个人品牌



PagePlug愿与你一同前行，欢迎加入：[**PagePlug开源团队**](jie-shao/jia-ru-wo-men/)****
{% endhint %}

### 4.1开源小分队



如果您想与组织一同<mark style="color:red;">**有节奏**</mark>、<mark style="color:red;">**有计划**</mark>的对PagePlug项目深度发展（例如积极参与社区管理的管理和答疑解惑、撰写和改进项目的文档、参与PagePlug的功能开发、提交补丁优化代码等等），欢迎加入我们的开源小分队🤩（目前在不断的壮大ing）



**🧑🏻‍💻Owenr：王昆QC**



**1、开源分队之狂飙队（排名不分先后）**

👩🏻‍💻扛把子：DD

🙋🏻‍♂️成员：Chris



**2、开源分队之漫威队（排名不分先后）**

🧑🏻‍💻美队：克力

🙋🏻‍♂️成员：xiaolu、kate、Bob、Nina、洪涛、马哥（很有爱和氛围的一群人🥰）



{% hint style="info" %}
近期会启动开源项目共建计划的招募，具体的流程及加入方式后续可以留意群消息或者查看这篇文章：[**加入开源小分队**](jie-shao/jia-ru-wo-men/)****
{% endhint %}



### 4.2个人尝试

PagePlug非常需要你的发现及自荐feature，我们接纳任何可行有益的建议，相信都会有助于提升整个项目的质量，哪怕是一个标点符号都会值得肯定👍🏻



如果你想自己先初步尝试，也欢迎在Github或者gitee上提交Issue或者Pull Request，社区的同学们将和您一起探讨，共同进步！

👇点击下方链接查看提交步骤👇

{% hint style="info" %}
提交你的Issue，可以查看：[**给PagePlug提Issue**](jie-shao/jia-ru-wo-men/ti-jiao-issue.md)****
{% endhint %}

{% hint style="info" %}
提交你的Pull Request，可以查看：[**给PagePlug提Pull Reque**](jie-shao/jia-ru-wo-men/ti-jiao-pull-request.md)****
{% endhint %}

🏅我们将会在此展示优秀伙伴的贡献及付出（展示顺序不分先后）

| 贡献内容 | Github名称 | 所在社区的名称 | 所在社区的群 | 提交时间 |
| ---- | -------- | ------- | ------ | ---- |
|      |          |         |        |      |
|      |          |         |        |      |
|      |          |         |        |      |



## 5、社区优质作品

我们非常欢迎社区的同学们多分享一些PagePlug的使用想法及心得，我们也会通过我们的平台，对大家沉淀的内容进行宣传及分享，如果有好的想法及idea，非常欢迎来社区分享你的内容及作品



随着PagePlug项目的发展，您所做出的分享也会被更多行业及领域的同行们所了解认识

{% hint style="info" %}
PagePlug有无限的可能性，能够满足更多的使用场景，”创新“时刻都在发生，点击查看：[**社区成员们优秀的作品案例**](jie-shao/he-xin-jie-shao/she-qu-zuo-pin-ji.md)****
{% endhint %}



**如果您仍然遇到问题，可以加入我们技术交流群，直接与PagePlug产品静静联系!**

<figure><img src=".gitbook/assets/image (3) (1) (1).png" alt=""><figcaption></figcaption></figure>
