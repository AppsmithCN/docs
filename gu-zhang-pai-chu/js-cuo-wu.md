# JS错误

使用JS 对象或编写JS 函数时可能会遇到错误。它们可能是由代码中的语法错误、数据类型不匹配或尝试访问不存在的属性或函数引起的。

本节帮助您解决Pageplug平台上常见的 JS 错误。

### 1、数据类型评估 <a href="#data-type-evaluation-errors" id="data-type-evaluation-errors"></a>

当小部件属性中的值与属性所需的数据类型不匹配时，会发生此错误。

&#x20;   **错误信息1:**

{% hint style="info" %}
This value does not evaluate to type Array\[Object]
{% endhint %}

&#x20;   **导致的原因：**

在使用Tables或Lists时，您可能会遇到此错误，因为数据属性需要一个可能与API响应的数据类型不匹配的对象数组。



&#x20;   **解决方案：**

解决方案是在响应对象中绑定数组或使用 JavaScript 转换响应对象。下面以 fetch users API的响应为例。将其直接绑定到表会导致错误。

```
{
 "next": "https://mock-api.appsmith.com/users?page=2&pageSize=10",
 "previous": null,
 "users": [
   {
     "id": 1,
     "name": "Barty Crouch",
     "status": "APPROVED",
     "avatar": "https://robohash.org/sednecessitatibuset.png?size=100x100&set=set1",
     "email": "barty.crouch@gmail.com",
   },
   {
     "id": 2,
     "name": "Jenelle Kibbys",
     "status": "APPROVED",
     "avatar": "https://robohash.org/quiaasperiorespariatur.bmp?size=100x100&set=set1",
     "email": "jkibby1@hp.com",
   }
 ]
}
```

为了克服这个问题，您可以使用 JavaScript 绑定用户的响应数组而不是整个响应对象：

```
{{ fetch_users.data.users }}
```



&#x20; **错误信息2：**

{% hint style="info" %}
This value does not evaluate to type Array\[{`label: string, value: string`}]
{% endhint %}

&#x20;   **导致的原因：**

在向单选或多选下拉列表添加选项时，您可能会遇到数据不匹配错误。在这种情况下，请确保`options`属性是包含标签和值作为字符串的对象数组。

&#x20;**解决方案：**

如果响应不包含如下所示的标签和值键，您可以映射响应以使用 JavaScript 对其进行转换。

```
// invalid response of fetchColors API
[
 'Blue',
 'Green',
 'Red'
]
```

```
// Transform Response
{{
   fetchColors.data.map((color) =>{
       return {
           label: color,
           value: color
       }
   })
}}
```

****

&#x20;   **错误信息3:**

{% hint style="info" %}
The value does not evaluate to type Array \[{x: string, y: number}]
{% endhint %}

&#x20;   **导致的原因：**

下图显示图表`Chart Data field`小部件中存在错误。这里的Evaluated Value表示该字段的当前值，在下面的截图中可以看到当前值是一个数组，而错误提示它必须是一个数组\\\<x, y>。

![](https://docs.appsmith.com/assets/images/chart\_error-6d1cd8e5122d283d8dda7bd2f2f2b4e8.png)

&#x20;   **解决方案：**

在这些情况下，您可以使用 JavaScript 将数据转换为正确的数据类型或访问对象内的正确数据。下面的代码减少了fetch\_orders.data数组，以根据日期将订单聚合到数组 \\\<x, y> 中，其中 x 是订单日期，y 是订单金额

```
{{
   _.values(fetch_orders.data.reduce((accumulator, order) => {
       if(accumulator[order.date]) {
           accumulator[order.date].y += order.orderAmount
       } else {
           accumulator[order.date] = { x:order.date, y: order.orderAmount  };
       }
       return acc;
   }, {}))
}}
```

&#x20;   ****   &#x20;

&#x20;   **错误信息4:**

{% hint style="info" %}
Value does not match ISO 8601 standard date string
{% endhint %}

&#x20;   **导致的原因：**

日期选择器需要标准ISO 格式的默认日期。如果您提供的日期与此不匹配，您将看到此错误。



&#x20;   **解决方案：**

要解决此问题，您可以使用 moment.js 转换日期字符串。

```
// Moment can be used to set the default date to the current date
{{moment()}}
```

```
// Moment can parse your date format
{{ moment("2021-07-26", "YYYY-MM-DD") }}
```

****

&#x20; **错误信息5:**

{% hint style="info" %}
This value does not evaluate to type \`boolean
{% endhint %}

&#x20; **导致的原因：**

此错误通常发生在`isVisible`和`isDisabled`属性中，表示属性中的值与类型不匹配`boolean`。



&#x20;   **解决方案：**

您可以使用比较运算符解决此问题。

```
{{ Dropdown1.selectedOptionValue === "RED" }}
```



&#x20; **错误信息6:**

{% hint style="info" %}
This value does not evaluate to type string
{% endhint %}

&#x20;  **导致的原因：**

使用小部件时，您可能会遇到错误，其中数据属性需要一个与查询响应的数据类型不匹配的字符串值。



&#x20;   **解决方案：**

该问题的解决方案是将 API 响应的数据类型转换为字符串。这可以使用 JavaScript 方法来完成。此外，确保传递给小部件的数据格式正确。例如：

```
To get text,
{{Text1.text}}


To get image,
{{Image1.image}}
```

如果前面的方法不起作用，您还可以检查 EVALUATED VALUE 部分以确保它返回的是字符串值而不是对象或其他数据类型。



&#x20;   **错误信息7:**

{% hint style="info" %}
This value must be number
{% endhint %}

&#x20;   **导致的原因：**

您可能会遇到一个错误，其中数据属性需要一个与 API 响应的数据类型不匹配的数值。



&#x20;   **解决方案：**

确保传递给小部件的数据属性的数据与预期的数据类型相匹配很重要。此问题的一种解决方案是使用 JavaScript 将 API 响应转换为正确的数据类型，或者从 API 响应访问正确的数据类型。

您还可以检查 EVALUATED VALUE 部分以确保它返回的是数值而不是对象或其他数据类型。



### 2、语法错误 <a href="#syntax-error" id="syntax-error"></a>

当 handlebars 中存在无效的 JavaScript 时，会发生此错误`{{ }}`。在这种情况下，字段的评估值显示为未定义。验证代码中大括号的数量，并考虑将JS 重写为多行代码。

在下面的示例中，应用程序中的任何地方都没有定义 fetch

![](https://docs.appsmith.com/assets/images/syntax\_error-54ac606aa1209e4b16172160ec5daddf.png)

### 3、循环依赖错误 <a href="#cyclic-dependency-error" id="cyclic-dependency-error"></a>

当节点直接或间接依赖于自身时，应用程序会出现循环依赖错误。

&#x20;   **反应性和依赖性地图**

在 Pageplug 中，所有用户可编辑的字段都被定义为节点，并且为了提供反应性，在这些节点之间创建了一个依赖映射，以找到这些节点的最佳评估顺序。例如，当您`{{Api1.data}}`在 Table1 的字段中引用时，会在和`tableData`之间创建依赖关系。所以每次更新，都需要更新。`Api1.dataTable1.tableDataApi1.dataTable1.tableData`

```
// Table1.tableData depends on Api1.data
Api1.data -> Table1.tableData
```

类似地，所有父节点都隐式依赖于子节点以确保更新向上传播到实体对象。更直接的理解方式是，如果子节点更新，则父节点及其依赖项也应更新。

```
// Implicit. Parent depends on children
Api1.data -> Api1
Table1.tableData -> Table1


// Explicit. Table1.tableData depends on Api1.data
Api1.data -> Table1.tableData
```

发生循环的最常见情况是当您尝试将节点绑定到其父节点时。由于无法评估具有循环依赖性的应用程序，因此您必须退出并处于错误状态，直到循环得到解决。

```
// A cycle is formed
Table1 -> Table1.tableData
Table1.isVisible -> Table1
```

### &#x20;<a href="#infinite-loop-error" id="infinite-loop-error"></a>

### 4、死循环错误 <a href="#infinite-loop-error" id="infinite-loop-error"></a>

当函数或代码块无限重复时会发生无限循环错误，导致应用程序或函数变得无响应，甚至会阻止用户访问应用程序的某些功能。

&#x20;   **导致的原因：**

问题可能是由于页面加载函数卡在了循环中。如果您添加了使用该`navigateTo`函数并在 上执行的代码，就会发生这种情况`onPageLoad`，这可能会导致页面无法访问或导致应用程序陷入循环并不断路由到目标页面。

&#x20; **解决方案：**

要解决此问题，您可以在 Pageplug 中使用调试器语句来停止代码的执行并确定无限循环的来源。以下是执行此操作的步骤：

1. 在 Pageplug 中打开应用程序并转到发生死循环的页面。
2. 找到导致无限循环的函数或代码块。
3. 在暂停代码执行并允许您检查其状态的函数或代码块的开头插入调试器语句。有关详细信息，请参阅调试语句及其使用方法。
4. 使用浏览器的调试器控制台单步执行代码并确定无限循环的原因。
5. 确定问题后，对代码进行必要的更改以修复它。
6. 保存更改并再次测试应用程序以确保无限循环问题已得到解决。
