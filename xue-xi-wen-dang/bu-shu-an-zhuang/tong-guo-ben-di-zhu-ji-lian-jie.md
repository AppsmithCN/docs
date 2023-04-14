# 通过本地主机连接

当您的本地PagePlug在同一系统上运行时，您可以使用[`host.docker.internal` ](https://docs.appsmith.com/advanced-concepts/more/how-to-work-with-local-apis-on-appsmith#using-docker-internal)ngrok连接到在本地主机上或作为其他 docker 容器运行的数据库、API 和服务



### 方法一：使用`host.docker.internal`

您可以使用它[`host.docker.internal`](https://docs.docker.com/desktop/networking/#i-want-to-connect-from-a-container-to-a-service-on-the-host)来连接数据库/API/其他运行在`localhost`

{% hint style="info" %}


[您还可以访问 docker 文档以阅读host.docker.internal](https://docs.docker.com/desktop/networking/#use-cases-and-workarounds-for-all-platforms)用法的用例和解决方法。
{% endhint %}

* 对于 Linux 系统，您需要提供一个运行标志 `add-host`。

```
--add-host=host.docker.internal:host-gateway
```

{% hint style="info" %}
只有较新版本的 Docker 才支持 host-gateway，它被转换为 Docker 默认桥接网络 IP（或主机的虚拟 IP）。
{% endhint %}

* 运行以下命令来测试并确保显示主机文件中的 IP 地址。

```
run —-rm -—add-host=host.docker.internal:host-gateway
```

* 对于 Linux 上的 Docker Compose，您需要手动将其添加到`docker-compose.yaml`文件中。用于`extra hosts`添加条目如下：

```
extra_hosts: 
     - "host.docker.internal:host-gateway"
```



### 方法二：使用ngrok

> PagePlug 允许您`localhost`在**`ngrok`**. 但是必须进行`ngrok`相同的设置。

#### 1）设置Ngrok

要设置“ngrok”——前提必须在[ngrok](https://dashboard.ngrok.com/get-started/setup)上注册（它是免费的！）。按照说明连接您的帐户。

* 下载`ngrok`安装文件并解压
* 添加[`auth-token`](https://ngrok.com/docs/ngrok-agent#install-your-authtoken)

#### 2）连接本地主机

按照以下步骤连接到 MongoDB 实例：

* `ngrok`使用命令公开本地 MongoDB 实例

```
ngrok <PROTOCOL> <LOCAL_PORT> 
```

MongoDB 使用一种`tcp`协议来创建连接，并且`27017`是默认端口。如果您不使用默认端口，请提供它代替`27017`.

```
ngrok tcp 27017
```

![使用在本地主机上运行的 ngrok MongoDB 进行连接](https://docs.appsmith.com/assets/images/connect-localhost-mongodb-using-ngrok-dbf728e4f58fa53f639ee6389f807866.png)

使用主机地址`0.tcp.in.ngrok.io`和端口号`17392`将 MongoDB 数据源添加到您的应用程序。

![通过连接到本地 MongoDB 使用 ngrok 创建 MongoDB 数据源](https://docs.appsmith.com/assets/images/Appsmith-connect-localhost-mongodb-using-ngrok-0713f6237e0e7b146623cc6847bd86c3.png)

您可以对新添加的 MongoDB 数据源的本地主机实例创建查询`LocalMongoDBUsingNgrok`。

#### 3）本地托管API

要在本地托管 API，您可以使用[Python FastAPI](https://realpython.com/fastapi-python-web-apis/#what-is-fastapi)服务器。您可以使用`pip`.

```
$ python3 -m pip install fastapi uvicorn
```

您可以使用以下代码片段来处理 API 请求：

```
from fastapi import FastAPI

app = FastAPI()

items = [{     
       "name": "Counter-Strike",
       "appid": 10,
       "average_playtime": 17612,
       "genres": "Action",
       "price": 7.2
     },
     {
       "name": "Team Fortress Classic",
       "appid": 20,
       "average_playtime": 277,
       "genres": "Action",
       "price": 3.99
     }]


@app.get("/")
async def root():
   return items
```

在代码片段中 - 你有：

* 导入 FastAPI 库并使用该类启动应用`FastAPI`程序
* 定义了一组 Steam 游戏对象
* 声明了可以访问项目（游戏对象）的路径“/”

您可以使用以下命令运行服务器：

```
$ uvicorn main:app --reload
```

{% hint style="info" %}
命令 uvicorn main:app 指的是：

* `main`：文件 main.py（Python“模块”）。
* `app`：在 main.py 中使用 app = FastAPI() 行创建的对象。
* `--reload`: 代码更改后重新启动服务器。仅用于开发环境
{% endhint %}

当应用程序启动并且 API 准备好使用时，您会看到下面的屏幕。

![使用 FastAPI 运行本地主机 API](https://docs.appsmith.com/assets/images/start-localhost-api-using-fastapi-c42821b4b51d522d49beb5486cd1ee3d.png)

启动`ngrok`并公开本地端口8000

```
ngrok <PROTOCOL> <LOCAL_PORT> 
```

要访问 API，您必须使用`HTTP`协议和端口`8000`。

```
ngrok http 8000
```

`ngrok`创建 HTTP 隧道，将外部可访问地址转发到本地地址，并允许通过 Internet 访问本地 API。

![使用 ngrok 连接本地 api](https://docs.appsmith.com/assets/images/connect-localhost-api-using-ngrok-595f34bacf761612286cfa6ea7d2a872.png)
