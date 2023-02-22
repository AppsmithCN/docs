# 数据源错误

<figure><img src="../../.gitbook/assets/image (9) (1) (1).png" alt=""><figcaption><p>Pageplug支持各类主流数据源</p></figcaption></figure>

以下是用户在Pageplug创建新数据源时经常看到的错误列表：

* 缺少端点
* 缺少端点
* 缺少端点主机
* 缺少端点和 URL
* 缺少主机名
* 没有配置端点

这些消息表明数据源创建表单`Host address`中的字段已留空。可以通过编辑数据源创建表单并输入数据源的主机地址来修复此错误。



### 1、无效主机

```
Invalid host provided. It should be of the form http(s)://your-es-url.com
```

### 2、缺少端口

```
Missing port for endpoint
```

此消息表明数据源创建表单`Port`中的字段已留空。

可以通过编辑数据源创建表单并输入数据源的端口地址来修复此错误。

### 3、缺少用户名

```
Missing username for authentication
```

此消息表明数据源创建表单`Username`中的字段已留空。该字段通常嵌套在子部分内。`UsernameAuthentication`

可以通过编辑数据源创建表单`Username`中的字段来修复此错误。

### 4、缺少密码

```
Missing password for authentication
```

此消息表明数据源创建表单`Password`中的字段已留空。该字段通常嵌套在子部分内。`PasswordAuthentication`

可以通过编辑数据源创建表单`Password`中的字段来修复此错误。

### 5、必填参数/字段空

```
The mandatory parameter 'Access Key' is empty.
```

```
At least one of the mandatory fields in the plugin's datasource creation form is empty
```

此消息表明其中一个必填字段（例如 ）在数据源创建表单`Access Key`中留空。

可以通过在数据源创建表单中填写上述必填字段来修复此错误。

### 6、无法删除数据源

```
Cannot delete datasource since it has 1 action(s) using it.
```

此消息表明试图删除的数据源配置了一些查询操作。

可以通过在尝试删除数据源之前删除依赖于该数据源的任何查询来修复此错误。

### 7、连接到本地数据库或API

如果您尝试从 Pageplug连接到本地数据库并看到如下错误消息：

> Connection refused

> Server logs - 'io.netty.channel.AbstractChannel$AnnotatedConnectException: finishConnect(..) failed: Connection refused: /172.17.0.1:3306'



在 Docker 容器内运行 Pageplug 时，它可能有自己的网络命名空间，并且无法使用`localhost`或`127.0.0.1`地址访问主机上运行的服务。这是因为这些地址指向容器的本地网络，与宿主机的本地网络不同。

相反，您可以使用`host.docker.internal`Windows 和 macOS 主机以及`172.17.0.1`Linux 主机上的主机名，从容器内访问主机上运行的服务。这允许容器访问主机上运行的 MySQL 服务器。

特别是，如果您要连接到 MySQL 服务器（或类似的 SQL 服务器），请确保它已配置为绑定到`0.0.0.0`. 这允许来自任何主机的连接，包括同一网络上的其他设备。根据您的安全要求，这可能是可取的，也可能不是可取的。

如果您在 Pageplug 中构建时仍然遇到问题，最好从`stacks/logs/backend/backend.log`文件中检查后端日志以获取任何错误消息或其他可能有助于解决问题的信息。

详细了解如何连接到本地主机数据库/API







