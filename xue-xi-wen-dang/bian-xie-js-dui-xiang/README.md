# 编写JS对象

在PagePlug中的 JavaScript 编辑器允许您创建一个可重用的 JavaScript 函数，你可以在组件内调用这些函数，从而实现对应的功能。在 PagePlug 中，处处皆可JS。

<figure><img src="../../.gitbook/assets/image (35) (1).png" alt=""><figcaption><p>在PagePlug中处处皆可JS </p></figcaption></figure>

### 1、如何创建JS对象

JS 对象是由多个函数和变量组成的实体。它是一个可以在其他 JS 对象中引用的可重用组件，允许您创建一组有组织的层次结构。

* 您可以从左侧菜单栏的【查询/JS】中新增JS对象

<figure><img src="../../.gitbook/assets/image (73).png" alt=""><figcaption></figcaption></figure>

### 2、如何调用JS对象

你可以在PagePlug任何的输入框中，来调用JS对象中定义的函数，例如：

<figure><img src="../../.gitbook/assets/image (106).png" alt=""><figcaption></figcaption></figure>

**1、可以修改js对象的名称**

**2、代码编辑选项，可以在里面编写JS代码**

**3、支持设置异步函数**

**4、可以定义变量**

**5、可以定义函数**

**6、这里可以支持多种内容，举几个例子：**

* **编写代码**
* **调用内置或用户定义的函数**
* **API调用**
* **数据库执行查询**

**7、向JS对象添加多个函数**

**8、可以选择要执行的函数名称**

**9、点击执行**

{% hint style="info" %}
定义的 JS 对象可跨 API、查询或为**特定页面定义的其他 JS 对象使用，**并且具有**页面级访问权限**，**不能跨页面**访问。
{% endhint %}

### 3、调用JS函数

例如我们刚刚在上面创建了一个`JSObject1`对象，我们可以在任意组件中调用`JSObject1`对象中定义的函数，例如在输入框组件里面：

<figure><img src="../../.gitbook/assets/image (122).png" alt=""><figcaption><p>组件的属性框都支持编写JS</p></figcaption></figure>

### 4、使用Synchronous或Asynchronous的JS对象编写函数

* #### Synchronous <a href="#synchronous" id="synchronous"></a>

例如，下面的代码片段显示了一个数据过滤器：

```javascript
Api.data.filter(() => {}); // filtering data 
```

这里的数据过滤是选择您要选择用于查看或分析的数据子集的过程。要过滤数据，您必须一个接一个地遍历整个数据集，如果符合过滤条件，则将其隔离。因此，您需要同步执行

* ### Asynchronous

在PagePlug中，例如使用**`Promises`**，**`Api.run()，Query.Run()`**（例如。showModal）。它基本上可以让您延迟执行嵌入在异步函数中的代码，并在需要时执行。



您可以[为异步功能配置其他设置](yi-bu-javascript-han-shu-she-zhi.md)并增强用户体验。

### 5、JS代码编辑器介绍

JavaScript 编辑器是一个功能广泛的编辑器，可在编写代码时提供额外的功能，你可以用它做很多事情。

* 功能介绍

&#x20;       **1、返回结果选项**

在开发时执行每个功能，都可以在返回结果选项中查看输出

<figure><img src="../../.gitbook/assets/image (114).png" alt=""><figcaption></figcaption></figure>

&#x20;       **2、编码错误检查**

JavaScript 编辑器会自动检查您的源代码是否存在编程错误。如果代码在编程上不正确，它会在错误代码下方使用<mark style="color:red;">**红色波浪线**</mark>突出显示错误。例如，`return`被拼错为 ret 的语法错误也会被 linting 捕获。

<figure><img src="../../.gitbook/assets/image (120).png" alt=""><figcaption></figcaption></figure>

&#x20;       **3、错误选项**

错误选项卡显示代码执行产生的所有类型的错误。这些错误可能包括**语法错误**、**运行时错误**（如**解析错误）**等。\


<figure><img src="../../.gitbook/assets/image (69).png" alt=""><figcaption></figcaption></figure>

&#x20;      **4、日志选项**

日志选项显示能看到执行的时间情况，你也可以通过单击控制台右下角的调试图标来打开“日志”选项（如下面的屏幕截图所示）。在**日志选项中，使您可以通过在过滤器框中**输入关键字或从**下拉列表**中选择**日志类型**来灵活地过滤日志。

<figure><img src="../../.gitbook/assets/image (55).png" alt=""><figcaption></figcaption></figure>

* 例子介绍

可以添加以下代码片段

```javascript
export default {
   hello: () => {
      return “Hello World”;
   }
}
```

<figure><img src="../../.gitbook/assets/image (130).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
您可以点击右上角的**运行可用来执行JS 函数。**如果你的 JS 对象只定义了一个函数，编辑器会默认函数名。但如果您的 JS 对象定义了多个函数，您可以选择要执行的函数，然后单击**运行**。
{% endhint %}

### 6、debugger和console功能

你可以使用`debugger`或`console.log()`调试您的代码并分别在浏览器控制台中检查它，这样可以检查代码的情况，并逐行检查它以帮助识别和修复任何错误

* console.log()用法

你可以使用`console.log()`将有关代码的信息打印到浏览器的控制台，帮你查看代码执行的不同点检查变量值或应用程序的状态。

用法：

```
console.log(<VARIABLE_NAME>);
```

当你运行你的代码时，`<VARIABLE_NAME>` 的值将打印到浏览器的控制台，查看它是否符合您的预期

#### &#x20;   6.1案例演示

* 首先创建一个get\_users的api

```
https://mock-api.appsmith.com/users
```

<figure><img src="../../.gitbook/assets/image (59).png" alt=""><figcaption></figcaption></figure>

* 创建一个js对象，打印接口数据

把下列代码输入到代码器中

```javascript
export default {
    getUser: async () => {
			const res = await get_users.run();
			console.log(res);
    }
}
```

<figure><img src="../../.gitbook/assets/image (104).png" alt=""><figcaption></figcaption></figure>

之后点击右上角运行，之后就看到打印的接口的返回数据

<figure><img src="../../.gitbook/assets/image (38) (1).png" alt=""><figcaption></figcaption></figure>

* 延伸，我们再试下打印一个变量值

```javascript
export default {
    getUser: async () => {
        const {users} = await get_users.run();
        console.log(users);
        users[0].id = 5;
        console.log(users[0]);	
    }
}
```

<figure><img src="../../.gitbook/assets/image (124).png" alt=""><figcaption></figcaption></figure>



* debugger功能

我们可以在代码中要暂停的地方插入一个`debugger`，然后运行你的应用程序。当到达调试器语句时，代码的执行将暂停，它的工作方式类似于`breakpoint`. 然后，您可以使用调试器工具单步执行代码、检查变量并查看代码的执行情况。

例子：

插入了之后我们可以在控制台里面查看详情

<figure><img src="../../.gitbook/assets/image (17) (2) (1).png" alt=""><figcaption></figcaption></figure>
