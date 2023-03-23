# JavaScript 承诺

以前,在 Appsmith 中实现异步工作流的唯一方法是通过回调,处理回调并不容易.Appsmith 现在支持原生 JavaScript 承诺,使处理异步工作流更容易.

JavaScript Promise 的新手？在[这里](https://javascript.info/promise-basics)检查 Promise 的基础知识这里.

{% embed url="https://youtu.be/VuBycqPJVug" %}

所有 Appsmith API,例如 [`showAlert()`](https://file+.vscode-resource.vscode-cdn.net/Users/fengqiong/Desktop/framework-reference/show-alert.md), [`showModal()`](https://file+.vscode-resource.vscode-cdn.net/Users/fengqiong/Desktop/framework-reference/show-modal.md), [`storeValue()`](https://file+.vscode-resource.vscode-cdn.net/Users/fengqiong/Desktop/framework-reference/store-value.md), [`navigateTo()`](https://file+.vscode-resource.vscode-cdn.net/Users/fengqiong/Desktop/framework-reference/navigateto.md) 等,将返回一个承诺,使异步工作流的实现更容易和可读.

为了理解回调和 Promise 实现之间的区别,让我们尝试实现在前一个成功后分别运行三个 API 并最终显示带有“完成”消息的警报的逻辑.

> MockApi 是在 Appsmith 内部创建的查询,它以名称作为参数..

旧的回调实现如下所示：

```
{{ 	 
MockApi.run(() => {
 	MockApi1.run(() => {
 		MockApi2.run(() => {
 			showAlert('done') 
			})
 	 }) 	 
}) 
}}
```

然而,对同样的问题使用 Promise 会使实现更容易和可读.

```
{{
 	MockApi.run()
 		.then(() => MockApi1.run())
 		.then(() => MockApi2.run())
 		.then(() => showAlert('done'))
 }}
```

### 异步/等待 <a href="#e5-bc-82-e6-ad-a5-e7-ad-89-e5-be-85" id="e5-bc-82-e6-ad-a5-e7-ad-89-e5-be-85"></a>

`async` 和 `await` 关键字使异步工作流能够以更简洁的风格编写,避免了显式配置承诺链的需要.

**异步**

在函数之前添加 `async` 关键字意味着一件简单的事情：函数总是返回一个承诺.其他值自动包装在已解决的承诺中.

**等待**

该关键字 `await` 使 JavaScript 等待,直到 Promise 完成并返回其结果.

让我们举个例子来理解这些关键字.参考下面的代码：

```
{{ 
(async function(){ 
    const response = await MockApi.run({ name: 'Appsmith' }); 
    await storeValue( "name", response.args.name ); 
    await showAlert(appsmith.store.name); 
    })() 
}}
```

在上面的例子中:

1. 我们运行 `MockApi` 参数名称为“Appsmith”并等待响应.
2. 当我们得到响应时,我们使用 `storeValue` 将响应存储在Appsmith商店中.
3. 在完成 `storeValue` 后, 我们显示一个带有信息的警报.

### 承诺方法 <a href="#e6-89-bf-e8-af-ba-e6-96-b9-e6-b3-95" id="e6-89-bf-e8-af-ba-e6-96-b9-e6-b3-95"></a>

如果您只想完成一个动作/承诺以进一步执行,您可以使用 `Promise.any()` 或 `Promise.race()` 方法.

> Please remember to always return the promise for <mark style="color:red;">`.then`</mark>`or`<mark style="color:red;">`.catch`</mark>`blocks` to work as expected.

```
{{
  (function() {
      ❌   MockApi.run().then(() => showAlert(`Success`))	
      ✅   return MockApi.run().then(() => showAlert(`Success`)) 
   })()
}}
```

\{% endhint %\}

**Promise.any()**

它需要一个可迭代的 Promise 对象.当其中一个 promise 实现时,它会返回一个用该 Promise 的值解析的 promise..

例如,参考下面的代码:

```
{{
(function(){
    
  return Promise.any([
		MockApi.run({ name: 1 }), // if name:1 finished early
		MockApi.run({ name: 2 })
  ]).then((res) => {
    showAlert(`Winner: ${res.args.name}`) // Alert Message will be "Winner: 1" 
  });
})()
}}
```

在这里,我们 `MockApi` 使用参数名称作为唯一数字（例如,1、2）运行多个,并将返回的 Promise 传递给 `Promise.any()`. 当执行任何操作时,我们会显示一条警报消息,其中包含发送到 API 的参数,从而更快地完成.

**Promise.race()**

它只是等待第一个已解决的 Promise（已完成或已拒绝）来获得结果.

让我们举个例子来理解 `Promise.race()`. 参考下面的代码:

```
{{
(function(){
    
 return	Promise.race([
		MockApi.run({ name: 1 }),
		MockApi.run({ name: 2 })
  ]).then((res) => {
    showAlert(`Winner: ${res.args.name}`)
  });

})()
}}
```

在上面的例子中:

1. 我们 `MockApi` 以参数名称作为唯一编号运行多个（例如,1、2）;
2. 我们将返回的 Promise 传递给 `Promise.race()`;
3. 我们显示一条警报消息,其中包含发送到 API 的参数,它完成得更快.

如果您希望所有操作首先完成,您可以使用 `Promise.all()` 或 `Promise.allSettled()` 来处理这种情况.

**Promise.all()**

它 \*\*\*\* 接受一组承诺（技术上是任何可迭代的,但通常是一个数组）并返回一个新的承诺.Promise 的结果数组成为新 Promise 的结果.如果任何 Promise 失败（拒绝状态）,新的 Promise 会立即拒绝并返回相同的错误.

例如,参考下面的代码:

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

在上面的例子中:

1. 我们有一个员工姓名列表,我们 `MockApi` 使用参数名称作为每个员工姓名运行;
2. 我们将每个返回的 Promise 存储 `MockApi.run()` 在调用数组中;
3. 然后,我们根据中的成功或失败情况显示警报消息 `Promise.all()`.

**Promise.allSettled()**

它只是等待所有的承诺解决,不管结果如何（解决或拒绝）.

例如,参考下面的代码:

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

在上面的例子中:

1. 我们有一个员工姓名列表,我们 `MockApi` 使用参数名称作为每个员工姓名运行;
2. 我们将每个返回的 Promise 存储 `MockApi.run()` 在调用数组中;
3. 然后,我们根据中的成功或失败情况显示警报消息 `Promise.allSettled()`.

### **在 Appsmith 中使用 Promise** <a href="#e5-9c-a8-appsmith-e4-b8-ad-e4-bd-bf-e7-94-a8-promise" id="e5-9c-a8-appsmith-e4-b8-ad-e4-bd-bf-e7-94-a8-promise"></a>

以下是在 Appsmith 中使用 Promises 的一些一般准则:

* Appsmith 中的大多数动作触发器现在都返回承诺,因此您可以附加 a `.then / await` 以在继续之前等待动作.
* 所有触发器都包装在一个 Promise 中,因此任何错过的错误都会导致未捕获的 Promise 错误.
* 返回带有 `.then` 的承诺.

```
{{
  (function() {
		// the .then will not run if the promise is not returned
		return MockApi.run()
			.then(() => showAlert('success'))
	})()
}}
```

* 在 `action.run` 的 `.then()` 参数中不再传递参数.只有响应被传递.

```
{{
  (function() {
		// define params on top so that you can use them in the later calls
		const params = { name: "Appsmith" }
		return MockApi.run(params)
			.then((response) => {
				showAlert(`${response.length} users found in `${params.name}`)
			})
	})()
}}
```

* 在action.run的.then()参数中不再传递参数.只有响应被传递.将函数传递给 `.then()` 或 `.catch()` 始终记住将其作为 回调函数 传递 .

```
{{
  (function() {
	MockApi.run().then(showAlert(`Success`))❌	
	return MockApi.run().then(() => showAlert(`Success`)) ✅
      
   })()
}}
```
