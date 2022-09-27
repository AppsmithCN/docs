# 更新本地文件路径

Appsmith 克隆本地文件系统中的 git 存储库，附加到 docker 容器中的持久卷。为了维护 git 存储库，我们需要一个指向 docker 容器中的卷的文件路径。我们只需更新相关的环境变量就可以快速实现这一点。

> 如果文件路径不存在，将克隆 git 存储库，但这不会是持久的，Appsmith 将尝试克隆存储库，以防它们被 docker restart 等删除。

#### 自定义 Git 根目录

要指向将保留 git 存储库的自定义 Git 根目录，请更新名为 <mark style="color:orange;">APPSMITH\_GIT\_ROOT</mark> 指向您的自定义文件路径。

```
// APPSMITH_GIT_ROOT=./path/to/repo/directory 
```

请记住重新启动容器以应用更改。
