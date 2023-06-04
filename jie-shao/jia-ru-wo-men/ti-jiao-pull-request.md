# 💡 提交Pull Request

## 🧑🏻‍💻提PR步骤

### 1、Fork源码：

* 进入项目页面, 点击右上角的Fork按钮

<figure><img src="../../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

* 之后会进入这个页面，填写一些简介信息（我已填写），点击create

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

* 创建成功之后，你会在repositories中看到刚刚fork的项目

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

* 此时，你需要在本地clone刚刚fork的项目，在命令行终端执行命令：

```
git clone https://github.com/zsf1482451437/pageplug.git
```



### 2、获取原项目代码

* 进入pageplug文件夹, 添加远程地址

```
git remote add origin https://github.com/zsf1482451437/pageplug.git
```

* 获取最新代码

```
git pull origin open-v1.8
```

{% hint style="info" %}
现在我们在 fork 来的 open-v1.8分支上, 这个 open-v1.8留作跟踪origin的远程代码...（一般是项目的主分支是master，这项目主分支命名为open-v1.8）
{% endhint %}



### 3、创建分支

好了, 现在可以开始贡献我们的代码了&#x20;

按照国际惯例, 我们一般不在 master 上提交新代码, 而需要为新增的功能或者fixbug建立新分支, 再合并到 master 上, 使用以下代码创建分支

```
git checkout -b branch1
```

现在我们可以在分支上更改代码了&#x20;

假设我们已经添加了一些代码, 使用命令提交到本地仓库

```
git commit -a -m "new commit"
```

{% hint style="info" %}
（选项 "-a" 表示自动将所有已修改和已删除的文件添加到暂存区，这样就不必使用 "git add" 命令来逐个添加文件了。）
{% endhint %}

### 4、合并修改

一个常见的问题是远程的 origin1 有了新的更新, 从而会导致我们提交的 Pull Request 时会导致冲突, 因此我们可以在提交前先把远程其他开发者的commit和我们的commit合并

* 使用以下命令切换到本地仓库的 master 分支:

```
git checkout master
```

* 使用以下命令拉取别人远程仓库origin1的最新代码到本地：

```
git pull origin master
```

* 切换回 branch1：

```
git checkout branch1
```

* 如果忘记自己之前建的分支名可以用 `git branch` 查看，把 master 的 commit 合并到 本地仓库branch1分支:

```
git rebase master
```

* 把更新代码提交到自己远程的 branch1分支 中:（相当于留个副本）

```
git push <你的远程仓库地址> branch1
```



### 5、发起Pull Request

* 完成代码的修改，在本地自测完成后便可发起 `pull request` 了，不要大意，这里还得有一个地方需要注意，那就是代码换行符的问题。

{% hint style="info" %}
一旦换行符与源仓库的不一致时，`git` 会认为这次修改是删除后重来的，这样会给 **`code review`** 带来巨大的麻烦。
{% endhint %}

* 最简单的方法就是设置自己 `git` 的全局配置，可以参考[这里](http://kuanghy.github.io/2017/03/19/git-lf-or-crlf)。

```
# 提交时转换为LF，检出时转换为CRLF
git config --global core.autocrlf true

# 提交时转换为LF，检出时不转换
git config --global core.autocrlf input

# 提交检出均不转换
git config --global core.autocrlf false
```

确认没问题后便可点击这里发起 pull request，后面按照引导执行即可。

### 6、Code Review <a href="#code-review" id="code-review"></a>

`PR` 发起后便可等待社区审核了。在这过程中我们会和你发起沟通交流，分享一些我们的想法，同时将你的想法和idea与PagePlug的进行深度融合，一同参与头脑风暴，有更好的code review过程。

沟通完后我们会将这次pr合并进master中



