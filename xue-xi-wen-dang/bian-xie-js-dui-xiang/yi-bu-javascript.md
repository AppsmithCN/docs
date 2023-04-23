# 异步JavaScript

本文档会给你解释如何在 PagePlug中编写异步 Javascript 代码。



## JavaScript promises

JavaScript Promises有助于实现使用回调时难以管理的异步工作流。PagePlug为 JavaScript 提供原生支持，Promises让异步操作更容易，且PagePlug的框架函数，如[showAlert()](https://docs.appsmith.com/reference/appsmith-framework/widget-actions/show-alert)、[showModal()](https://docs.appsmith.com/reference/appsmith-framework/widget-actions/show-modal)、[storeValue()](https://docs.appsmith.com/reference/appsmith-framework/widget-actions/store-value)和其他函数都返回一个Promises，使异步工作流的实现更容易和可读。

### 1、Callbacks vs promises <a href="#callbacks-vs-promises" id="callbacks-vs-promises"></a>

要了解Callbacks和 promise 实现之间的区别，请考虑一个依次执行三个 API 查询并在所有 API 成功运行完成时显示一条消息的示例，例如：

<pre><code><strong>// Using Callbacks
</strong>{{
    MockApi.run(() => {
        MockApi1.run(() => {
            MockApi2.run(() => {
                showAlert('done') 
                })
        })   
    }) 
}}
</code></pre>

对同一个示例使用promise可以让实现更易于管理和可读。

```
{{
    MockApi.run()
        .then(() => MockApi1.run())
        .then(() => MockApi2.run())
        .then(() => showAlert('done'))
 }}
```

### 2、Promise方法 <a href="#promise-methods" id="promise-methods"></a>

JavaScript Promise有几个内置方法。

{% hint style="info" %}
小tips：

传递函数给`.then()`or的时候`.catch()`一定要记得把它作为[回调](https://developer.mozilla.org/en-US/docs/Glossary/Callback\_function)函数传递，如下图：
{% endhint %}

❌错误方法：

```
{{
  (function() {
    MockApi.run().then(showAlert(`Success`))      
   })()
}}
```

✅正确方法：

```
{{
  (function() {
     return MockApi.run().then(() => showAlert(`Success`))
   })()
}}
```

**方法一：Promise.any()**

[Promise.any()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Promise/any)将可迭代的Promise作为输入并返回单个Promise。当其中一个Promise首次履行时，它会返回一个Promise，该Promise解决了已履行Promise的价值。如果你只想完成一个action/Promise以进一步执行，你可以使用`Promise.any()`方法。

例子：

```
{{
(function(){
    
  return Promise.any([
        MockApi.run({ name: 1 }), // if name:1 finished early
        MockApi.run({ name: 2 })
  ]).then((res) => {
    showAlert(`Winner: ${res.args.name}`) // Alert Message showns as "Winner: 1" 
  });
})()
}}
```

在这个例子中：

1. 该函数调用多个 API 查询传递和参数到每个 API 调用。`Promise.any()`收到退回的Promise。
2. 当任何 API 调用首先完成并返回已履行的Promise时，将显示一条警报消息。该消息包含发送到 API 的参数，API 完成执行并在 API 调用中首先返回Promise。

**方法二：Promise.race()**

它等待第一个已确定的Promise、fulfilled或rejected，以获得结果。`Promise.race()`当您只需要一个动作/承诺来完成执行时，您可以使用。

例子：

```
{{
(function(){
    return  Promise.race([
            MockApi.run({ name: 1 }),
            MockApi.run({ name: 2 })
    ]).then((res) => {
        showAlert(`Winner: ${res.args.name}`)
    });
})()
}}
```

在示例中：

1. 该函数调用多个 API 查询传递和参数到每个 API 调用。
2. 返回的 Promise 传递给`Promise.race()`
3. 当任何 API 调用首先完成并返回已履行的Promise时，将显示一条警报消息。该消息包含发送到 API 的参数，该参数在 API 调用中首先完成并返回Promise。

**方法三：Promise.all**

它接受一组Promise（从技术上讲是任何可迭代的，但通常是一个数组）并返回一个新的Promise。Promise 的结果数组成为新 Promise 的结果。如果其中一个 promise 失败（拒绝状态），新的 Promise 会立即拒绝并返回相同的错误。您可以`Promise.all()`在希望所有操作成功完成执行时使用。

例子：

```
{{
(function(){
    let employeeNames = ["Employee 1","Employee 2"];
    // Start a bunch of calls running in parallel and store returned promise
    const calls = employeeNames.map(employeeName => MockApi.run({ name: employeeName }));
    
    // Wait for all to finish (or any to reject).
    return Promise.all(calls)
            .then(() => showAlert('Promise.all - All successful'))
            .catch(() => showAlert('Promise.all - Something went wrong'))
            .finally(() => showAlert('Promise.all - finished'))
})()
}}
```

在示例中：

1. 该函数使用作为参数传递的员工姓名运行 API。
2. 该`calls`数组存储每个 API 调用的返回Promise。
3. 根据中的成功或失败案例显示一条警告消息`Promise.all()`。

**方法三：Promise.allSettled()**

它等待所有 promise 解决，不管结果如何（resolved 或 rejected）。`Promise.allSettled()`当您希望所有操作首先完成时，您可以使用。

例子：

```
{{
(function(){
  let employeeNames = ["Employee 1","Employee 2"];
  // Start a bunch of calls running in parallel and store returned promise
  const calls = employeeNames.map(employeeName => MockApi.run({ name: employeeName }));
  
  // Wait for all to resolve / reject.
  return Promise.allSettled(calls)
        .then(() => showAlert('Promise.allSettled - All successful'))
        .catch(() => showAlert('Promise.allSettled - Something went wrong'))
        .finally(() => showAlert('Promise.allSettled - finished'))
})()
}}
```

在示例中：

1. 该函数使用作为参数传递的员工姓名运行 API。
2. 该`calls`数组存储每个 API 调用的返回Promise。
3. 根据中的成功或失败案例显示一条警告消息`Promise.allSettled()`。

### 3、通用指南

以下是在PagePlug 中使用 Promise 的一些通用指南：

* PagePlug 中的大多数操作触发器都会返回Promise，因此您可以在继续之前附加一个`.then()`或`await`等待操作。
* 所有触发器都包含在Promise中，因此任何遗漏的错误都会导致未捕获的Promise错误。
* 附有返回承诺`.then()`，如下所示：

```
{{
  (function() {
        // the .then only runs if a promise is returned
        return MockApi.run()
            .then(() => showAlert('success'))
    })()
}}
```

* 参数不再在`.then()`的参数中传递`action.run()`。只传递response，如下图：

```
{{
  (function() {
        // define params on top so that you can use them in the later calls
        const params = { name: "PagePlug" }
        return MockApi.run(params)
            .then((response) => {
                showAlert(`${response.length} users found in `${params.name}`)
            })
    })()
}}


```

### 4、async和await

async和await关键字可以让异步工作流能够以更干净的风格编写，从而避免了显式配置promise链的需要。

* asynv

`async`在函数前添加关键字总是返回一个promise。其他值自动包装在已解决的promise中

* await

该关键字`await`使 JavaScript 等待，直到 Promise 完成并返回其结果。

例子：

```
{{
    (async function(){ 
        const response = await MockApi.run({ name: 'PagePlug' }); 
        await storeValue( "name", response.args.name ); 
        await showAlert(global.store.name); 
    })() 
}}
```

在前面的示例中：

1. `MockApi`使用参数作为“PagePlug”运行查询`name`并等待响应。
2. `storeValue()`当您收到响应时，将响应存储在 global.store中。
3. 成功执行后`storeValue()`，显示一条警告消息，其中包含保存在global的数据。
