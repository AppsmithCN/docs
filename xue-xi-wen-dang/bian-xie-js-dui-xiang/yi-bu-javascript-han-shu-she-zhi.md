# 异步 JavaScript 函数设置

异步函数允许您选择何时执行代码。例如，您可能希望延迟查询执行或按需获取数据。



## 1、异步函数介绍

在 PagePlug中，如果您正在执行以下操作之一，则函数被称为**异步：**

* 你有一个关键字 (async) 来标记函数的异步执行

```
export default{
    functionName: async() => {
       //use async-await or promises
    }
}
```

* 您在功能块中添加了PagePlug内置组件的功能，例如`showModal(), showAlert()`等。
* 您想要在运行时执行查询或调用 API。例如，你有一个 API `GetUsersList,`，你想在运行时调用这个 API，也就是每当`callAPI()`执行 JS Object 函数时。您的功能可能如下所示：

```
export default {
   callAPI: () => {
      GetUsersList.run();
   }
 }
```

这行代码`GetUsersList.run()`标记了异步执行的函数`callAPI()`，因此`callAPI`函数被认为是异步的。

PagePlug 中的 JavaScript 编辑器为异步函数提供了一些附加设置，可帮助您添加更多配置。

## 2、如何在PagePlug中定义异步函数

* **你可以在代码选项旁边的设置选项，进行异步函数的设置**

<figure><img src="../../.gitbook/assets/image (131).png" alt=""><figcaption></figcaption></figure>

* **页面加载后执行：**你可以设置这个函数是否在加载页面时候执行。例如，您有一个页面并添加了一个 JS 对象，该对象具有获取用户角色的功能。你希望在页面加载时执行查询，以便登录用户能够看到用户列表。要使其正常工作。
* **执行函数前确认：**在执行函数前，会有弹窗提醒，确认是否执行

<figure><img src="../../.gitbook/assets/image (134).png" alt=""><figcaption></figcaption></figure>
