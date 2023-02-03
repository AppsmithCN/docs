# 迁移 (k8s)

现在 Helm 支持 Appsmith，本指南将帮助您将在旧堆栈（多个 pod/容器）上运行的 Kubernetes 上的部署迁移到 Helm 图表（使用单个容器）.

本指南将在具有以下资源的默认 Kubernetes 安装上正常工作:

```
➜ kubectl get all
NAME                                           READY   STATUS      RESTARTS   AGE
pod/appsmith-editor-995c974df-njtdh            1/1     Running     0          3d12h
pod/appsmith-internal-server-dfd68b55b-8p5w8   1/1     Running     1          3d12h
pod/imago-27473940-kwslt                       0/1     Completed   0          12m
pod/mongo-statefulset-0                        1/1     Running     0          3d12h
pod/redis-statefulset-0                        1/1     Running     0          3d12h

NAME                               TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)           AGE
service/appsmith-backend-service   NodePort    10.100.247.245   <none>        8080:32694/TCP    3d12h
service/appsmith-editor            ClusterIP   10.100.236.17    <none>        80/TCP            3d12h
service/kubernetes                 ClusterIP   10.100.0.1       <none>        443/TCP           3d12h
service/mongo-service              NodePort    10.100.2.162     <none>        27017:31766/TCP   3d12h
service/redis-service              NodePort    10.100.7.184     <none>        6379:30834/TCP    3d12h

NAME                                       READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/appsmith-editor            1/1     1            1           3d12h
deployment.apps/appsmith-internal-server   1/1     1            1           3d12h

NAME                                                  DESIRED   CURRENT   READY   AGE
replicaset.apps/appsmith-editor-995c974df             1         1         1       3d12h
replicaset.apps/appsmith-internal-server-dfd68b55b    1         1         1       3d12h

NAME                                 READY   AGE
statefulset.apps/mongo-statefulset   1/1     3d12h
statefulset.apps/redis-statefulset   1/1     3d12h

NAME                  SCHEDULE    SUSPEND   ACTIVE   LAST SCHEDULE   AGE
cronjob.batch/imago   0 * * * *   False     0        12m             3d12h

NAME                       COMPLETIONS   DURATION   AGE
job.batch/imago-27473940   1/1           16s        12m
```

## 迁移钱

### 1. 先决条件

* `kubectl` 必须安装和配置以连接您的集群:
  * 安装 kubectl: [kubernetes.io/vi/docs/tasks/tools/install-kubectl/](https://kubernetes.io/vi/docs/tasks/tools/install-kubectl/)
  * Minikube: [设置 Kubectl](https://minikube.sigs.k8s.io/docs/handbook/kubectl/)
  * Google Cloud Kubernetes: [Configuring cluster access for kubectl](https://cloud.google.com/kubernetes-engine/docs/how-to/cluster-access-for-kubectl)
  * Aws EKS: [Create a kubeconfig for Amazon EKS](https://docs.aws.amazon.com/eks/latest/userguide/create-kubeconfig.html)
* 在本指南中，我们将使用包将资源中的 `yq` 数据格式化为文件，作为迁移配置的参考 `ConfigMap` `.yaml` :
  * 安装 `yq` 包: [https://github.com/mikefarah/yq#install](https://github.com/mikefarah/yq#install)

### 2. 不包含在本文档中

基于 Kubernetes 的上下文，本指南将不涉及两个部分:

* 迁移现有 SSL 证书:
  * 在旧 Kubernetes 堆栈和新 Helm 图表的上下文中，Kubernetes 集群将使用 `cert-manager` ([https://cert-manager.io/](https://cert-manager.io/)) 来配置 SSL 证书.根据定义, `cert-manager` 它 `Automate certificate manager` 本身提供和管理证书=>如果将证书从一个迁移 `cert-manager` 到另一个,则向后不兼容.
    * 建议: 我们建议迁移到 Helm 图表后，您可以按照此文档则向后不兼容 ([https://github.com/appsmithorg/appsmith/blob/release/deploy/helm/Setup-https.md](https://github.com/appsmithorg/appsmith/blob/release/deploy/helm/Setup-https.md)) 来设置新的 `cert-manager` 和配置新的证书.
* 移除旧的 Kubernetes 堆栈:
  * 在本指南中，我们不会提及删除旧的 Kubernetes 堆栈，因为这不是迁移中的必需步骤，您可以将其保留为备用计划，以防在迁移到新的 Helm 图表时遇到问题.

## 迁移步骤

### 1. 从旧 K8S 导出数据库和配置

目标: 从现有的 `MongoDB` pod 中导出数据,并将归档文件下载到本地.

* 步骤
  * 在pod中创建 `backup` 目录 `MongoDB` .
  * 执行 `mongodump` 命令以从正在运行的 MongoDB pod 中导出数据.
  * 将存档文件从 MongoDB pod 复制到本地.
* 命令
  *   创建 `backup` 目录:

      ```
      kubectl exec mongo-statefulset-0 -- mkdir -pv /data/db/backup
      ```

      * 导出 `MongoDB` 数据:

      ```
      kubectl exec mongo-statefulset-0 o-statefulset-0 -- sh -c 'mongodump --uri="mongodb://$MONGO_INITDB_ROOT_USERNAME:$MONGO_INITDB_ROOT_PASSWORD@localhost/$MONGO_INITDB_DATABASE" --authenticationDatabase admin --archive=/data/db/backup/appsmith-data.archive --gzip'
      ```

      * 将存档文件复制到本地:

      ```
      kubectl cp mongo-statefulset-0:data/db/backup/appsmith-data.archive appsmith-data.archive
      ```
* 核实
  *   此步骤的输出应该是一个本地文件,该文件存储了 Kubernetes `archive` 中现有服务的所有数据. `MongoDB` 我们可以通过列出本地目录来验证 `archive` 文件是否已存储在本地.

      ```
      ls | grep appsmith-data.archive

      appsmith-data.archive
      ```

### 2. 从旧K8S导出配置文件是否已存储在本地

目标: `ConfigMap` 从正在运行的 Kubernetes 系统中导出所有现有配置,并将它们迁移到 `values.yaml` Helm 图表的模板中.

* 步骤
  * 从格式为 ( )的文件中检索所有配置数据 `ConfigMap` 并将其写入文件 `yaml` (`configuration.yaml`).
    * 下载 `values.yaml` Helm 图表的模板.
    * 手动将数据 `configuration.yaml` 从 `applicationConfig` `values.yaml`.
* 命令
  *   运行以下命令以获取数据并将其写入 `configuration.yaml` 文件:

      ```
      kubectl get cm application-config -o "jsonpath={.data}" | yq e -P -I 2 >> configuration.yaml \
      && kubectl get cm mongo-config -o "jsonpath={.data}" | yq e -P -I 2 >> configuration.yaml \
      && kubectl get cm encryption-config -o "jsonpath={.data}" | yq e -P -I 2 >> configuration.yaml
      ```
  *   Helm图表下载 `values.yaml` 模板:

      ```
      curl -o values.yaml https://raw.githubusercontent.com/appsmithorg/appsmith/release/deploy/helm/values.yaml
      ```

      * 手动将值复制到（强烈建议 `values.yaml` 将值放在报价中）:
* 核实
  *   手动迁移配置后,该 `applicationConfig` 部分 `values.yaml` s应如下所示:

      ```
      applicationConfig:
        APPSMITH_OAUTH2_GOOGLE_CLIENT_ID: ""
        APPSMITH_OAUTH2_GOOGLE_CLIENT_SECRET: ""
        APPSMITH_OAUTH2_GITHUB_CLIENT_ID: ""
        APPSMITH_OAUTH2_GITHUB_CLIENT_SECRET: ""
        APPSMITH_FORM_LOGIN_DISABLED: "false"
        APPSMITH_SIGNUP_DISABLED: "true"
        APPSMITH_CLIENT_LOG_LEVEL: ""
        APPSMITH_GOOGLE_MAPS_API_KEY: "false"
        APPSMITH_MAIL_ENABLED: ""
        APPSMITH_MAIL_HOST: ""
        APPSMITH_MAIL_PORT: ""
        APPSMITH_MAIL_USERNAME: ""
        APPSMITH_MAIL_PASSWORD: ""
        APPSMITH_MAIL_FROM: ""
        APPSMITH_REPLY_TO: ""
        APPSMITH_MAIL_SMTP_AUTH: ""
        APPSMITH_MAIL_SMTP_TLS_ENABLED: ""
        APPSMITH_DISABLE_TELEMETRY: "false"
        APPSMITH_RECAPTCHA_SITE_KEY: ""
        APPSMITH_RECAPTCHA_SECRET_KEY: ""
        APPSMITH_RECAPTCHA_ENABLED: "false"
        APPSMITH_MONGODB_URI: "mongodb://root:root@mongo-service/appsmith"
        APPSMITH_REDIS_URL: "redis://redis-service:6379"
        APPSMITH_ENCRYPTION_PASSWORD: "rmEOM1TxTRxit"
        APPSMITH_ENCRYPTION_SALT: "Jhj1IyFcpKYUK"
        APPSMITH_CUSTOM_DOMAIN: ""
      ```

### 3. 更改 Helm 上下文的配置

目标: 从第 2 步迁移后更改配置 `values.yaml` ,这将确保 Helm 图表可以与内部 `Redis` 和 `MongoDB` 服务一起正常运行.

* 步骤
  * 随内部主机更改 `MongoDB URI` .
    * 为初始凭证添加附加配置 `MongoDB`
    * 替换 `Redis URL` 为本地 URL
* 行动
  * 随内部主机变化 `MongoDB URI` :在旧的 Kubernetes 堆栈中, `MongoDB` 已作为单独的资源部署在集群中.在新的 Helm 图表中,我们使用内部 `MongoDB` 服务并将其配置为 `ReplicaSet`. 因此, 我们需要对 Helm 上下文执行以下操作:
    * 将主机 `APPSMITH_MONGODB_URI` 从更改 `mongo-service` 为 `localhost`.
    * 如果存在，则删除 URI 中的查询参数.
  * 为初始凭据添加附加配置 `MongoDB`: 您将需要添加 2 个新变量,它们是 `APPSMITH_MONGODB_USER` & `APPSMITH_MONGODB_PASSWORD` 其值为 `MongoDB` .
  * 替换 `Redis URL` 为本地 URL:同 `MongoDB`, 在新的 Helm 图表中，我们也使用内部 `Redis` 服务. 因此，将主机从更改 `redis-service` 为 `localhost` (或 `127.0.0.1`) 是必要的操作.
* 核实
  *   以第 2 节中的步骤为例 `Verify` ,更改配置后，我们将获得具有 `applicationConfig` 以下值的部分:

      ```
      applicationConfig:
        APPSMITH_OAUTH2_GOOGLE_CLIENT_ID: ""
        APPSMITH_OAUTH2_GOOGLE_CLIENT_SECRET: ""
        APPSMITH_OAUTH2_GITHUB_CLIENT_ID: ""
        APPSMITH_OAUTH2_GITHUB_CLIENT_SECRET: ""
        APPSMITH_FORM_LOGIN_DISABLED: "false"
        APPSMITH_SIGNUP_DISABLED: "true"
        APPSMITH_CLIENT_LOG_LEVEL: ""
        APPSMITH_GOOGLE_MAPS_API_KEY: "false"
        APPSMITH_MAIL_ENABLED: ""
        APPSMITH_MAIL_HOST: ""
        APPSMITH_MAIL_PORT: ""
        APPSMITH_MAIL_USERNAME: ""
        APPSMITH_MAIL_PASSWORD: ""
        APPSMITH_MAIL_FROM: ""
        APPSMITH_REPLY_TO: ""
        APPSMITH_MAIL_SMTP_AUTH: ""
        APPSMITH_MAIL_SMTP_TLS_ENABLED: ""
        APPSMITH_DISABLE_TELEMETRY: "false"
        APPSMITH_RECAPTCHA_SITE_KEY: ""
        APPSMITH_RECAPTCHA_SECRET_KEY: ""
        APPSMITH_RECAPTCHA_ENABLED: "false"
        APPSMITH_MONGODB_URI: "mongodb://root:root@localhost/appsmith"
        APPSMITH_REDIS_URL: "redis://127.0.0.1:6379"
        APPSMITH_ENCRYPTION_PASSWORD: "rmEOM1TxTRxit"
        APPSMITH_ENCRYPTION_SALT: "Jhj1IyFcpKYUK"
        APPSMITH_CUSTOM_DOMAIN: ""
        APPSMITH_MONGODB_USER: "root"
        APPSMITH_MONGODB_PASSWORD: "root"
      ```

### 4. 安装Helm图表

* 目标: 使用旧配置安装新 Helm 图表的指南
* 步骤
  * 添加 Helm 存储库.
    * 更新存储库.
    * 删除 `Imago` 资源.
    * 安装 Appsmith Helm 图表.
* 命令
  *   添加 Helm 存储库:

      ```
      helm repo add appsmith https://helm.appsmith.com
      ```

      * 更新存储库:

      ```
      helm repo update
      ```

      * 删除 `Imago` 资源: `Imago` 是 Kubernetes 的自动更新工具,该工具在旧 Kubernetes 堆栈和 Helm 图表的上下文中设置.因此,在部署 Helm chart 与现有服务帐户和 cronjob时可能会发生冲突.`Imago` 从旧的 Kubernetes 上下文中删除它是必要的:

      ```
      kubectl delete sa,cronjob imago
      ```

      * 安装 Appsmith Helm 图表:

      ```
      helm install appsmith appsmith/appsmith --values values.yaml
      ```
* 核实
  *   安装后，您可以使用以下命令检查正在运行的 pod,应该会看到由 Helm 图表创建的新 pod:

      ```
      kubectl get pods
      NAME                                        READY   STATUS    RESTARTS   AGE
      appsmith-0                                  1/1     Running   0          2m48s
      appsmith-editor-566f7b547f-lb9n8            1/1     Running   0          55m
      appsmith-internal-server-5c78944b64-fs7jm   1/1     Running   0          44m
      mongo-statefulset-0                         1/1     Running   0          55m
      redis-statefulset-0                         1/1     Running   0          55m
      ```

### 5. 导入数据库

目标: 将存档文件中的数据导入新的 Helm 图表

* 步骤
  * 在新 pod 中创建目录 `restore` .
  * 将存档文件从本地复制到新 pod.
    * 运行 `import_db` 命令.
* 命令
  *   在新 pod 中创建目录 `restore`

      ```
      kubectl exec appsmith-0 -- mkdir -p /appsmith-stacks/data/restore
      ```
  *   将归档文件从本地复制到新 pod:

      ```
      kubectl cp appsmith-data.archive appsmith-0:/appsmith-stacks/data/restore
      ```

      * 运行 `import_db` 命令:

      ```
      kubectl exec -it appsmith-0 -- appsmithctl import_db
      ```

      请注意，这会询问您 `Importing this DB will erase this data. Are you sure you want to proceed`, 您可以在哪里回复 `y`. 在这种情况下是安全的，因为新设置中的新数据库仅包含初始数据并且应该可以安全地被覆盖.
* 核实
  * 此步骤的预期输出是 Helm 图表在导入后仍然可以正常工作，并且来自旧 Kubernetes 堆栈的数据也出现在 Helm 图表中
