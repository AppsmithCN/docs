# Kubernetes

## 使用 Helm Charts 安装 Appsmith

此图表使用[Helm包管理器](https://helm.sh/)在[Kubernetes](https://github.com/appsmithorg/appsmith/blob/release/deploy/helm/kubernetes.io)集群上引导Appsmith部署

### 先决条件

* 安装 [Helm包管理器](https://helm.sh/docs/intro/install/).
* 确保 `kubectl` 已安装并配置为连接到您的集群
  * 安装 [kubectl](https://kubernetes.io/vi/docs/tasks/tools/install-kubectl/)
  * Minikube: [设置 Kubectl](https://minikube.sigs.k8s.io/docs/handbook/kubectl/)
  * Google Cloud Kubernetes: [为kubectl配置集群访问](https://cloud.google.com/kubernetes-engine/docs/how-to/cluster-access-for-kubectl)
  * AWS EKS: [为Amazon EKS创建kubeconfig](https://docs.aws.amazon.com/eks/latest/userguide/create-kubeconfig.html)
  * Microk8s: [使用kubectl](https://microk8s.io/docs/working-with-kubectl)
* 请确保您在集群上运行了默认存储类.请按照以下指南之一启用您的默认存储类 -
  * Minikube: [启用插件默认存储类](https://kubernetes.io/docs/tutorials/hello-minikube/#enable-addons)
  * Google Cloud Kubernetes: [在GKE上设置默认存储类](https://cloud.google.com/anthos/clusters/docs/on-prem/1.3/how-to/default-storage-class)
  * AWS EKS: [创建默认存储类](https://docs.aws.amazon.com/eks/latest/userguide/storage-classes.html)
  * Microk8s: [启用存储](https://microk8s.io/docs/command-reference#heading--microk8s-enable)
* 默认情况下，应在集群上启用 Kubernetes NGINX Ingress Controller.请确保为您的集群安装正确的版本
  * Minikube: [使用 NGINX Ingress Controller在 Minikube上设置Ingress](https://kubernetes.io/docs/tasks/access-application-cluster/ingress-minikube/)
  * Google Cloud Kubernetes: [在Google Kubernetes Engine上使用NGINX控制器的Ingress](https://kubernetes.github.io/ingress-nginx/deploy/#gce-gke)
  * AWS EKS: [为 AWS EKS 安装 NGINX 控制器](https://kubernetes.github.io/ingress-nginx/deploy/#network-load-balancer-nlb)
  * Microk8s: [添加：入口](https://microk8s.io/docs/addon-ingress)

### 安装图表

1. 使用 Helm 将 Appsmith 添加到您的存储库中.

```
helm repo add appsmith https://helm.appsmith.com

helm repo update
```

2\. 安装 <mark style="color:orange;">`appsmith`</mark> 发行版的图表.

```
helm install appsmith/appsmith --generate-name
```

该命令以默认配置在 Kubernetes 集群上部署 Appsmith 应用程序。参数部分列出了安装期间的可配置参数.

### 卸载图表

要卸载该 <mark style="color:orange;">`appsmith`</mark> 版本:

```
helm list
NAME                       NAMESPACE       REVISION        UPDATED                                 STATUS          CHART           APP VERSION
appsmith-1631069261        default         1               2021-09-09 11:24:40.152766 +0700 +07    deployed        appsmith-1.3.0  1.16.0

helm uninstall appsmith-1631069261
```

该命令卸载版本并删除与图表关联的所有 Kubernetes 资源.

### 参数

#### 全局参数

| 姓名                         | 描述             | 价值   |
| -------------------------- | -------------- | ---- |
| `global.namespaceOverride` | 覆盖图表部署的资源的命名空间 | `""` |
| `global.storageClass`      | 持久卷的全局存储类      | `""` |

#### 常用参数

| 姓名                  | 描述                          | 价值           |
| ------------------- | --------------------------- | ------------ |
| `fullnameOverride`  | 完全覆盖 `appsmith.name` 模板的字符串 | `""`         |
| `containerName`     | 指定在 pod 中运行的容器名称            | `"appsmith"` |
| `commonLabels`      | 要添加到所有已部署对象的标签              | `{}`         |
| `commonAnnotations` | 添加到所有已部署对象的注释               | `{}`         |

#### Appsmith 图像参数

| 姓名                 | 描述              | 价值                         |
| ------------------ | --------------- | -------------------------- |
| `image.registry`   | Appsmith 镜像注册表  | `index.docker.io`          |
| `image.repository` | Appsmith 图像存储库  | `appsmith/appsmith-editor` |
| `image.tag`        | Appsmith 图像标签   | `latest`                   |
| `image.pullPolicy` | Appsmith 图像拉取策略 | `IfNotPresent`             |

#### Appsmith 部署参数

| 姓名                   | 描述                  | 价值              |
| -------------------- | ------------------- | --------------- |
| `strategyType`       | Appsmith 部署策略类型     | `RollingUpdate` |
| `schedulerName`      | 备用调度程序              | `""`            |
| `podAnnotations`     | Appsmith pod 的注解    | `{}`            |
| `podSecurityContext` | Appsmith pods 安全上下文 | `{}`            |
| `securityContext`    | 设置安全上下文             | `{}`            |
| `resources.limits`   | Appsmith 容器的资源限制    | `{}`            |
| `resources.requests` | Appsmith 容器请求的资源    | `{}`            |
| `nodeSelector`       | pod 分配的节点标签         | `{}`            |
| `tolerations`        | pod 分配的容差           | `[]`            |
| `affinity`           | 亲和 fod pod 分配       | `{}`            |

#### Appsmith 命名空间参数

| 姓名                 | 描述               | 价值     |
| ------------------ | ---------------- | ------ |
| `namespace.create` | 启用创建 `Namespace` | `true` |

#### 服务帐户参数

| 姓名                           | 描述                                                           | 价值     |
| ---------------------------- | ------------------------------------------------------------ | ------ |
| `serviceAccount.create`      | 为 Appsmith pod启用创建 `ServiceAccount`                          | `true` |
| `serviceAccount.name`        | 创建的名称 `ServiceAccount` . I如果未设置，则使用 appsmith.fullname 模板生成名称 | `""`   |
| `serviceAccount.annotations` | 其他服务帐号注释                                                     | `{}`   |

#### 交通曝光参数

| 姓名                                 | 描述                                 | 价值          |
| ---------------------------------- | ---------------------------------- | ----------- |
| `service.type`                     | Appsmith 服务类型                      | `ClusterIP` |
| `service.port`                     | Appsmith 服务端口                      | `80`        |
| `service.portName`                 | Appsmith 服务端口名称                    | `appsmith`  |
| `service.nodePort`                 | Appsmith 服务节点端口要暴露要暴露              | `8000`      |
| `service.clusterIP`                | Appsmith 服务集群                      | `""`        |
| `service.loadBalancerIP`           | Appsmith 服务负载均衡器 IP                | `""`        |
| `service.loadBalancerSourceRanges` | Appsmith 服务负载均衡器来源                 | `[]`        |
| `service.annotations`              | Additional 服务的附加自定义注释              | `{}`        |
| `ingress.enabled`                  | 为 Appsmith 启用入口记录生成                | `false`     |
| `ingress.hosts`                    | 要被入口记录覆盖的主机数组                      | `[]`        |
| `ingress.tls`                      | 为参数中定义的主机启用 TLS 配置 `ingress.hosts` | `false`     |
| `ingress.secrets`                  | 自定义 TLS 证书作为机密                     | `[]`        |
| `ingress.certManager`              | 启用入口以使用 Cert Manager 提供的 TLS 证书    | `false`     |
| `ingress.certManagerTls`           | 指定证书管理器创建的 TLS 机密资源                | `[]`        |
| `ingress.className`                | 配置在入口资源中使用的入口类                     | `""`        |

#### 持久性参数

| 姓名                                  | 描述                                | 价值                 |
| ----------------------------------- | --------------------------------- | ------------------ |
| `persistence.enabled`               | 使用 Persistent Volume Claims 启用持久性 | `true`             |
| `persistence.storageClass`          | 持久卷存储类                            | `""`               |
| `persistence.annotations`           | PVC 的附加自定义注释                      | `{}`               |
| `persistence.localStorage`          | 使用本地存储启用持久卷                       | `false`            |
| `persistence.storagePath`           | 本地存储路径                            | `/tmp/hostpath_pv` |
| `persistence.localCluster`          | 本地运行集群提供存储空间                      | `[minikube]`       |
| `persistence.accessModes`           | 持久卷访问模式                           | `[ReadWriteOnce]`  |
| `persistence.size`                  | 持久卷大小                             | `10Gi`             |
| `storageClass.enabled`              | 启用存储类配置                           | `false`            |
| `storageClass.defaultClass`         | 创建默认存储类                           | `false`            |
| `storageClass.bindingMode`          | 使用存储类的持久卷声明的绑定模式                  | `Immediate`        |
| `storageClass.allowVolumeExpansion` | 允许使用存储类扩展持久卷声明                    | `true`             |
| `storageClass.reclaimPolicy`        | 配置动态创建的持久卷的保留                     | `Delete`           |
| `storageClass.provisioner`          | 存储类供应商                            | `""`               |
| `storageClass.annotations`          | 其他存储类注释                           | `{}`               |
| `storageClass.mountOptions`         | 持久卷使用的挂载选项                        | `{}`               |
| `storageClass.parameters`           | 存储类参数                             | `{}`               |

#### 自动更新图表的图像

| 姓名                     | 描述                  | 价值            |
| ---------------------- | ------------------- | ------------- |
| `autoupdate.enabled`   | 启用自动更新 Helm 图表的图像   | `true`        |
| `autoupdate.scheduler` | 安排时间运行 cron 作业以更新映像 | `"0 * * * *"` |

使用helm install 的参数指定每个参数. `--set key=value[,key=value]` 例如:

```
helm install \
--set persistence.storageClass=appsmith-pv \
  stable-appsmith/appsmith --generate-name
```

上述命令部署 Appsmith 应用程序并将应用程序配置为使用存储类名称`appsmith-pv`

或者，可以在安装图表时提供指定参数值的 YAML 文件。例如：

```
helm install -f values.yaml stable-appsmith/appsmith --generate-name
```

_**提示**: 您可以使用默认值_ [_values.yaml_](https://github.com/appsmithorg/appsmith/blob/release/deploy/helm/values.yaml) _作为配置这种方式的起点._

#### 应用程序配置

要更改 Appsmith 配置，您可以更新 `values.yaml` 文件（可用配置如下所列）.

| 姓名                                                       | 价值   |
| -------------------------------------------------------- | ---- |
| `applicationConfig.APPSMITH_OAUTH2_GOOGLE_CLIENT_ID`     | `""` |
| `applicationConfig.APPSMITH_OAUTH2_GOOGLE_CLIENT_SECRET` | `""` |
| `applicationConfig.APPSMITH_OAUTH2_GITHUB_CLIENT_ID`     | `""` |
| `applicationConfig.APPSMITH_OAUTH2_GITHUB_CLIENT_SECRET` | `""` |
| `applicationConfig.APPSMITH_CLIENT_LOG_LEVEL`            | `""` |
| `applicationConfig.APPSMITH_GOOGLE_MAPS_API_KEY`         | `""` |
| `applicationConfig.APPSMITH_MAIL_ENABLED`                | `""` |
| `applicationConfig.APPSMITH_MAIL_HOST`                   | `""` |
| `applicationConfig.APPSMITH_MAIL_PORT`                   | `""` |
| `applicationConfig.APPSMITH_MAIL_USERNAME`               | `""` |
| `applicationConfig.APPSMITH_MAIL_PASSWORD`               | `""` |
| `applicationConfig.APPSMITH_MAIL_FROM`                   | `""` |
| `applicationConfig.APPSMITH_REPLY_TO`                    | `""` |
| `applicationConfig.APPSMITH_MAIL_SMTP_AUTH`              | `""` |
| `applicationConfig.APPSMITH_MAIL_SMTP_TLS_ENABLED`       | `""` |
| `applicationConfig.APPSMITH_DISABLE_TELEMETRY`           | `""` |
| `applicationConfig.APPSMITH_RECAPTCHA_SITE_KEY`          | `""` |
| `applicationConfig.APPSMITH_RECAPTCHA_SECRET_KEY`        | `""` |
| `applicationConfig.APPSMITH_RECAPTCHA_ENABLED`           | `""` |
| `applicationConfig.APPSMITH_MONGODB_URI`                 | `""` |
| `applicationConfig.APPSMITH_REDIS_URL`                   | `""` |
| `applicationConfig.APPSMITH_ENCRYPTION_PASSWORD`         | `""` |
| `applicationConfig.APPSMITH_ENCRYPTION_SALT`             | `""` |
| `applicationConfig.APPSMITH_CUSTOM_DOMAIN`               | `""` |

例如，要更改加密盐配置，您可以运行以下命令:

```
helm install \
--set applicationConfig.APPSMITH_ENCRYPTION_SALT=123 \
  stable-appsmith/appsmith --generate-name
```

## 揭秘 Appsmith

* 如果您希望通过 Internet 将您的 Appsmith 发布到全世界，您需要首先设置 Ingress 控制器。请参阅 [先决条件](broken-reference)中的 **Kubernetes NGINX Ingress Controller** 部分.
*   如果你还没有安装 Helm chart，你可以运行下面的命令来安装它并暴露 Appsmith:

    ```
    helm install appsmith/appsmith --generate-name \
      --set ingress.enabled=true \
      --set ingress.annotations."kubernetes\.io/ingress\.class"=nginx \
      --set service.type=ClusterIP
    ```
*   如果您已经安装了 Appsmith Helm chart，请运行 `helm upgrade` 命令升级现有安装

    ```
    helm upgrade --set ingress.enabled=true appsmith appsmith/appsmith

    # Or this command if you are using values.yaml file
    helm upgrade --values values.yaml appsmith appsmith/appsmith
    ```

## 更新 Appsmith

### 自动更新

*   在默认的 Appsmith helm 安装中，自动更新被禁用（推荐）. 您可以选择通过以下任一方式为 Appsmith helm 部署启用自动更新:

    * 如果您使用的是值文件，请在文件中设置 `autoupdate.enabled` 为 `true` `values.yaml` .

    ```
     helm upgrade --values values.yaml appsmith appsmith/appsmith
    ```

    * 通过将参数传递 `--set autoupdate.enabled=true` t给 helm install/upgrade 命令.

    ```
      helm install appsmith/appsmith --generate-name \
        --set ingress.enabled=true \
        --set ingress.annotations."kubernetes\.io/ingress\.class"=nginx \
        --set service.type=ClusterIP \
        --set autoupdate.enabled=true
    ```

### 手动更新

* 要将 Appsmith 容器映像手动更新到最新版本，请运行以下命令: `kubectl rollout restart statefulset appsmith`

## 故障排除

如果您在此过程中遇到任何错误，请查看我们的调试部署错误指南。如果您仍然遇到任何问题，可以加入我们技术交流群，直接与Appsmith中国社区联系！
