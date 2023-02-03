# 部署错误

### 1、端口不可用 <a href="#ports-unavailable" id="ports-unavailable"></a>

如果遇到`ports 80 & 443`未打开的错误，建议您停止这些端口上的所有进程并重新启动。如果无法停止这些端口上的进程，您可以在另一个端口上运行 PagePlug。

1.  在文件`docker-compose.yml`中，将Nginx容器的端口更改为自定义端口，如下例所示。

    ```
        ports:
          - "80:80"
          - "443:443"
          - "9001:9001"
    ```

    改成

    ```
        ports:
          - "3000:80"
          - "8443:443"
          - "9801:9001"
    ```
2. 跑步`docker-compose up -d`

{% hint style="danger" %}
提示

要停止在这些端口上运行的先前版本的 appsmith，请运行以下命令：

* `sudo su`
* `docker container kill $(docker ps -q)`
{% endhint %}



### 2、容器启动 <a href="#containers-failed-to-start" id="containers-failed-to-start"></a>

如果您选择初始化新数据库并看到此错误，则可能是由于在安装期间获取依赖项时出错。删除当前安装方向，杀死 docker 容器，然后重新启动安装应该可以。如果没有，请联系PagePlug静静

如果您尝试连接到现有的MongoDB而容器无法启动，则可能是由于以下原因之一：

1. **不正确的 MongoDB凭据**
2. **用于加密的空盐/密码**

使用有效值重新启动安装过程。



### 3、无法访问PagePlug <a href="#unable-to-access-appsmith" id="unable-to-access-appsmith"></a>

* 确保您的安全组配置为允许流量流向安装实例上的端口 80 和 443。
* 您可以在任何浏览器或您机器上访问本地主机上正在运行的应用程序。`public IP`
* 您可能需要等待几分钟才能访问应用程序以允许Nginx启动。

### &#x20;<a href="#oauth-sign-up-not-working" id="oauth-sign-up-not-working"></a>

### 4、OAuth 注册无效 <a href="#oauth-sign-up-not-working" id="oauth-sign-up-not-working"></a>

如果您的部署位于 ELB/代理之后，则必须更新部署的Nginx配置。在文件中`data/nginx/nginx.app.conf.template`修改行：

```
proxy_set_header X-Forwarded-Proto $scheme;
```

和

```
proxy_set_header X-Forwarded-Proto $http_x_forwarded_proto;
```

这确保重定向 URL 在OAuth2登录期间是正确的。即使 ELB 配置为在自定义端口上运行，这仍然有效。



### 5、服务器因MongoCommandException <a href="#server-not-booting-because-of-mongocommandexception" id="server-not-booting-because-of-mongocommandexception"></a>

在发布`v1.6.4`中，PagePlug 升级了它的库和Spring 框架。这导致了 PagePlug 中使用的库与之前发布的MongoDB版本之间的兼容性问题。这并没有出现在测试中，因为所有测试都是针对具有副本集的MongoDB集群进行的，而问题并未浮出水面。

如果您看到如下错误，则您的实例受到在`v1.6.4`.

```
Caused by: com.mongodb.MongoCommandException: Command failed with error 17 (ProtocolError): 'Attempt to switch database target during SASL authentication.' on server mongo:27017. The full response is {"ok": 0.0, "errmsg": "Attempt to switch database target during SASL authentication.", "code": 17, "codeName": "ProtocolError"}
```

请按照下面提到的步骤修复您的 PagePlug 安装。

&#x20;   **第 1 步：编辑 MongoDB URI**

添加`&authSource=admin`到文件`APPSMITH_MONGODB_URI`中变量值的`docker.env`末尾。例如，在您的`docker.env`文件中，如果您有以下行：

```
# Old config
APPSMITH_MONGODB_URI=mongodb://<your_username>:<your_password>@mongo/appsmith?retryWrites=true
```

将其更改为以下内容（注意唯一的变化是`&authSource=admin`。请不要粘贴整行。仅将`&authSource=admin`部分添加到您的当前值。

```
# New config
APPSMITH_MONGODB_URI=mongodb://<your_username>:<your_password>@mongo/appsmith?retryWrites=true&authSource=admin
```

保存文件。



&#x20;   **第 2 步：重启服务器**

现在使用以下命令重新启动容器：

```
sudo docker-compose up -d --force-recreate appsmith-internal-server
```

一两分钟后，服务器现在应该启动并准备就绪。

### &#x20;<a href="#unable-to-send-emails" id="unable-to-send-emails"></a>

### 5、无法发送电子邮件 <a href="#unable-to-send-emails" id="unable-to-send-emails"></a>

如果您遇到无法发送邀请电子邮件的问题，即使**管理员电子邮件设置**能够发送测试电子邮件，也可能是由于电子邮件参数的配置问题。

如果您没有收到邀请电子邮件，请检查`APPSMITH_REPLY_TO`配置文件中的值。如果此值为空，请将其设置为您使用的相同电子邮件地址`APPSMITH_MAIL_FROM`并**重新启动应用程序**。

这应该可以解决收不到邀请电子邮件的问题。此外，验证正在使用的电子邮件服务器是否正常工作以及网络或其他组件是否存在阻止电子邮件发送的问题可能会有所帮助。

但是，如果您遇到任何问题，可以在Github上提问或者在PagePlug开源社区提问。

### &#x20;<a href="#server-shuts-down-with-schema-mismatch-error" id="server-shuts-down-with-schema-mismatch-error"></a>

### &#x20;<a href="#server-shuts-down-with-schema-mismatch-error" id="server-shuts-down-with-schema-mismatch-error"></a>
