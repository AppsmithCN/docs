---
description: >-
  Docker 是一个开源的容器化平台。 它使开发人员能够将应用程序打包到容器中——将应用程序源代码与在任何环境中运行该代码所需的操作系统 (OS)
  库和依赖项相结合的标准化 可执行组件。 Appsmith可以在本地部署，也可以使用Docker部署在你的私有实例上。
---

# Docker

## 先决条件

> Docker(20.10.7或更高版本)\
> Docker-Compose(1.29.2或更高版本)

* 创建一个名为appsmith的安装文件夹，您可以将Appsmith安装和数据存储在其中。
* cd 进入安装文件夹。

## 快速入门（使用Docker-Compose）

Appsmith Docker 镜像由在单个 Docker 容器中运行所需的所有组件构建。 所有这些多个进程都由一个 Supervisord 实例管理，该实例是一个轻量级进程管理器。

> 使用 docker-compose ps 命令时，您开始运行一个容器,就像是：
>
> \#Container appsmith Running

### Docker-compose配置

> 目前，在docker-compose文件上禁用了自动更新。如果您想为Appsmith启用自动更新，请取消注释docker-compose文件中的所有注释行。

将以下 docker-compose.yml 文件下载到appsmith安装文件夹中

filename

或者你是在远程机器上，运行下面的curl

```bash
curl -L https://bit.ly/32jBNin -o $PWD/docker-compose.yml
```

此配置运行Appsmith实例和Watchtower实例以使Appsmith自动保持最新状态。

通过运行以下命令启动 docker 容器。（您可能需要像sudo您的用户无法访问 docker 和 docker-compose 一样运行）

```bash
docker-compose up -d
```

如果本地不可用，上面的命令将下载 Docker 镜像并启动服务。您可以使用以下命令跟踪日志：

```bash
docker logs -f appsmith
```

容器准备就绪后，您会看到这样一条消息。`Appsmith is Running!`如果这是您第一次使用docker，您应该会看到类似于下面的欢迎页面。

> 恭喜！您的 Appsmith 服务器现在应该已启动并正在运行。您可以通过[http://localhost](http://localhost)访问它。

### 更新 Appsmith（使用 docker-compose）

要手动更新 Appsmith（使用 docker-compose 配置），请转到设置的根目录并运行以下命令：

```bash
docker-compose pull
docker-compose rm -fsv appsmith
docker-compose up -d
```

***

## 探索 Appsmith（没有docker-compose）

要快速启动并运行 Appsmith，请在您的计算机上运行以下命令：

```bash
docker run -d --name appsmith -p 80:80 -v "$PWD/stacks:/appsmith-stacks" appsmith/appsmith-ce
```

此命令将下载映像并启动 Appsmith。下载完成后，服务器应该会在一分钟内启动。您可以使用以下命令跟踪日志：

```bash
docker logs -f appsmith
```

`Appsmith is Running!`容器准备就绪后，您应该会看到该消息

![](https://s3.bmp.ovh/imgs/2022/06/29/6173eeb59d1fa70a.png)

## 重启容器

如果您的容器无法重新启动，您可以执行以下脚本来启动它们：

{% file src="broken-reference" %}

### 更新 Appsmith（没有 docker-compose）

要手动更新 Appsmith，请转到设置的根目录并运行以下命令：

```bash
docker rmi appsmith/appsmith-ce -f
docker pull appsmith/appsmith-ce
docker rm -f appsmith
docker run -d --name appsmith -p 80:80 -v "$PWD/stacks:/appsmith-stacks" appsmith/appsmith-ce
```

## 故障排除

如果您在此过程中遇到任何错误，请查看我们的调试部署错误指南。如果您仍然遇到任何问题，可以加入我们技术交流群，直接与Appsmith中国社区联系！
