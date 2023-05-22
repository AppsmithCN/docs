# 提交Pull Request

## 🧑🏻‍💻提PR步骤

### 1、Fork源码、本地开发：

* 进入项目页面, 点击右上角的Fork按钮

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

* 之后会进入这个页面，填写一些简介信息（我已填写），点击create

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>



### 2、完成自测：





### 3、发起Pull Request

* 自测完成后便可发起 `pull request` 了，不要大意，这里还得有一个地方需要注意，那就是代码换行符的问题。一旦换行符与源仓库的不一致时，`git` 会认为这次修改是删除后重来的，这样会给 `code review` 带来巨大的麻烦。



最简单的方法就是设置自己 `git` 的全局配置，可以参考[这里](http://kuanghy.github.io/2017/03/19/git-lf-or-crlf)。

```
# 提交时转换为LF，检出时转换为CRLF
git config --global core.autocrlf true

# 提交时转换为LF，检出时不转换
git config --global core.autocrlf input

# 提交检出均不转换
git config --global core.autocrlf false
```

确认没问题后便可点击这里发起 pull request，后面按照引导执行即可。



### 4、Code Review <a href="#code-review" id="code-review"></a>

`pr` 发起后便可等待社区审核了。



期待你为PagePlug提交的第一个Pull Request
