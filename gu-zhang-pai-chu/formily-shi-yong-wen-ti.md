---
description: 目前formliy组件未跟pageplug打通，因此一些使用上提供一些临时解决方法，欢迎在群里，或者私聊静静反馈相关问题，一起完善帮助文档
---

# Formily使用问题

### 1.**select 下拉框数据**

> 🔍我想把外面<mark style="color:purple;">jsObject</mark>的内容，放到里面select组件的可选项中，怎么办？

可以试试下面这个处理方案

* 在fomliy初始化数据表单项中传入，自定义的option

<figure><img src="../.gitbook/assets/image (2) (3) (2).png" alt=""><figcaption></figcaption></figure>

* 在Select组件自定义的<mark style="color:blue;">响应器配置</mark>中，给dataSource赋值

<figure><img src="../.gitbook/assets/image (16) (2).png" alt=""><figcaption></figcaption></figure>

> 🔍我想通过<mark style="color:purple;">调用接口</mark>，初始化select可选项，怎么办？

<figure><img src="../.gitbook/assets/image (6) (4).png" alt=""><figcaption></figcaption></figure>

### 2.只要包含<mark style="color:yellow;">上传文件</mark>的组件，提交就报错

<figure><img src="../.gitbook/assets/image (17) (2).png" alt=""><figcaption></figcaption></figure>

使用 自定义请求<mark style="color:blue;">customRequest</mark> 替代默认的上传事件

```javascript
$props({
  customRequest(options) {
    let params = new FormData()
    // post 参数
    params.append("files", options.file) // binary
    $request("http://upload_server/upload", {
      data: params,
      method: "post",
    }).then(response) {
        const res = JSON.parse(response)
        options.onSuccess(res[0], options.file)
        $self.loading = false
        // 设置form表单的file字段，为接口返回的url
        $form.setValuesIn("file", file[0].response.data)
      }
  },
})
```
