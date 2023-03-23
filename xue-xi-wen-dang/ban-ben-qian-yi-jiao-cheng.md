# 版本迁移教程

假设您当前的 PagePlug 实例位于文件夹中`~/pageplug-old`，而您希望新设置位于`~/pageplug-new`. （这只是示例文件夹名称，请使用您喜欢的名称。）

然后我们可以看到这样一个粗略的文件夹结构`~/pageplug-old`：

```
~/pageplug-old
├── data
│   ├── certbot
│   │   ├── conf
│   │   └── www
│   ├── mongo
│   │   ├── db
│   │   └── init.js
│   └── nginx
│       └── app.conf.template
├── docker-compose.yml
├── docker.env
└── encryption.env
```

像这样`~/pageplug -new`（在本文档中的步骤完成后）：

```
~/pageplug-new
├── docker-compose.yml
└── stacks
    ├── configuration
    │   ├── docker.env
    │   └── mongo-init.js
    ├── data
    │   ├── backup
    │   ├── certificate
    │   ├── mongodb
    │   └── restore
    └── letsencrypt
        ├── accounts
        ├── archive
        ├── conf
        ├── csr
        ├── keys
        ├── live
        ├── options-ssl-nginx.conf
        ├── renewal
        ├── renewal-hooks
        ├── ssl-dhparams.pem
        └── www
```

现在让我们回顾一下要执行的步骤。

### 1.关闭旧版本pageplug实例 <a href="#1-shutdown-old-appsmith-instance" id="1-shutdown-old-appsmith-instance"></a>

🚨 在开始前，请先了解下面4个通知：

* 整个迁移应该在 25-30 分钟内完成，通常比这要短。
* 当前登录的所有用户都将被注销。一旦新实例启动并正常运行，他们就可以重新登录。
* 根据您的配置，下面的任何`docker-compose`和`docker`命令可能需要`sudo`在开始时运行。
* 请检查命令的输出，看看是否有任何错误，运行命令后，然后再继续下一步。

让我们首先定义几个在我们的迁移过程中有用的变量。请使用适当的路径代替`~/pageplug-old`和`~/pageplug-new`。

```
old_path=~/pageplug-old
new_path=~/pageplug-new
```

在开始迁移之前，请使用以下命令停止旧服务器：

```
cd "$old_path"
docker-compose stop appsmith-internal-server
```

### 2.导出[数据库](https://docs.appsmith.com/getting-started/setup/installation-guides/docker/migrate#2-export-database) <a href="#2-export-database" id="2-export-database"></a>

要从正在运行的`MongoDB`数据库中导出数据，我们使用`mongodump`命令，这将创建一个`gzip`包含所有数据的存档。然后该文件将被复制到新设置并导入。

创建备份文件夹以存储转储文件：

```
cd "$old_path"
docker-compose exec mongo mkdir -pv /data/db/backup
```

转储 MongoDB 数据并压缩成 gzip 文件：

```
docker-compose exec mongo sh -c 'mongodump --uri="$APPSMITH_MONGODB_URI" --archive=/data/db/backup/appsmith-data.archive --gzip'
```

### 3.迁移[配置](https://docs.appsmith.com/getting-started/setup/installation-guides/docker/migrate#3-migrate-configuration) <a href="#3-migrate-configuration" id="3-migrate-configuration"></a>

新设置`docker.env`对所有环境变量配置使用单个文件。

让我们创建所需的文件夹结构：

```
mkdir -pv "$new_path"/stacks/configuration
```

从旧位置迁移配置：

```
cat "$old_path"/docker.env "$old_path"/encryption.env >> "$new_path"/stacks/configuration/docker.env
```

现在，在文件中`"$new_path"/stacks/configuration/docker.env`：

* 除非您使用的是外部 MongoDB 数据库，否则`APPSMITH_MONGODB_URI`请将 中的部分更改`@mongo`为`@localhost`，并删除查询参数（the`?`及其后的所有内容）。例如，如果当前值为`mongodb://root:rootpass@mongo/appsmith?retryWrites=true&authSource=admin`，则将其更改为 just `mongodb://root:rootpass@localhost/appsmith`。
* 除非您使用的是外部 Redis 实例，否则`APPSMITH_REDIS_URL`请将 中的 更改`redis://redis:6379`为`redis://localhost:6379`. 也就是说，将主机从更改`redis`为`localhost.`

在此文件的末尾`docker.env`，让我们添加以下新环境变量：

```
APPSMITH_MONGODB_USER=<Your MongoDB User>
APPSMITH_MONGODB_PASSWORD=<Your MongoDB Password>
APPSMITH_API_BASE_URL=http://localhost:8080
```

在这里，请使用上面提供的相同用户名和密码代替`<Your MongoDB User>`和。在上面的示例值中，这些将用于用户和密码。`<Your MongoDB Password>APPSMITH_MONGODB_URIrootrootpass`

### 4.导出https配置和证书（可选[）](https://docs.appsmith.com/getting-started/setup/installation-guides/docker/migrate#4-export-https-config--certificate-optional) <a href="#4-export-https-config--certificate-optional" id="4-export-https-config--certificate-optional"></a>

{% hint style="info" %}
如果您的 `pageplug` 实例未使用自定义域，请跳过此步骤
{% endhint %}

如果您还没有`APPSMITH_CUSTOM_DOMAIN`配置`docker.env`，请添加如下一行

```
echo APPSMITH_CUSTOM_DOMAIN=appsmith.mycustomdomain.com >> "$new_path"/stacks/configuration/docker.env
```

您还可以通过运行以下命令将证书移动到新容器：

```
mkdir -pv "$new_path"/stacks/letsencrypt
sudo cp -rfv "$old_path"/data/certbot/conf/* "$new_path"/stacks/letsencrypt
```

### 5. 使用 Fat[容器](https://docs.appsmith.com/getting-started/setup/installation-guides/docker/migrate#5-setup-new-appsmith-with-fat-container) <a href="#5-setup-new-appsmith-with-fat-container" id="5-setup-new-appsmith-with-fat-container"></a>

现在让我们完全关闭旧实例：

```
docker-compose --file "$old_path"/docker-compose.yml down
```

[按照官方指南在Docker Compose Configuration](bu-shu-an-zhuang/si-you-hua-bu-shu-han-docker-an-zhuang-jiao-cheng.md)开始新的 Pageplug 部署，此处也简要显示以供参考：

```
cd "$new_path"
curl -L https://bit.ly/32jBNin -o docker-compose.yml
docker-compose up -d
```

_请注意，您必须创建一个新的`docker-compose.yml`文件`"$new_path"`夹，就像上面的命令一样`curl`。不要从`"$old_path"`._

### 6.导入[数据库](https://docs.appsmith.com/getting-started/setup/installation-guides/docker/migrate#6-import-database) <a href="#6-import-database" id="6-import-database"></a>

在您的新部署出现后（通常需要30 秒左右），我们将导入从旧实例导出的数据：

创建文件夹以复制存档文件：

```
mkdir -pv "$new_path"/stacks/data/restore
```

复制存档文件：

```
cp "$old_path"/data/mongo/db/backup/appsmith-data.archive "$new_path"/stacks/data/restore/
```

从此存档导入数据：

```
docker-compose exec appsmith appsmithctl import_db
```

请注意，这将询问您`Importing this DB will erase this data. Are you sure you want to proceed`，您可以在那里回复`y`。在这种情况下是安全的，因为新设置中的新数据库只包含初始数据，应该可以安全覆盖。

一旦成功，我们就可以启动我们的新实例了！

### 7. 验证迁移 <a href="#7-verify-migration" id="7-verify-migration"></a>

导航到您的 PagePlug 实例，无论是使用 IP 地址还是自定义域，使用与旧实例相同的方式，并验证您的 PagePlug 实例是否运行良好，并且您的所有数据都完好无损。

在此之后，请指定一个用户作为超级用户，让他们访问管理设置页面。diff --git a/setting-up/migrate.md b/setting-up/migrate.md

\
