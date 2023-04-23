# PagePlug的JS库

你可以在PagePlug的任何地方编写 JavaScript 代码，包括小部件属性、事件侦听器、查询和其他设置。借助 JavaScript 编辑器和调试工具，编写复杂的可重用代码并构建可扩展的应用程序。同时你可以直接使用PagePlug内置的 JavaScript 库，可用于处理`{{ }}`绑定或 JSObject 中的数据。从而提升开发效率；



## 1、支持代码的编写

您可以在**mustache 语法`{{ }}`**中编写 JS 代码。您可以引用实体（小部件、查询、JS 对象）及其相关数据和属性作为 JavaScript 变量，并使用内置函数对它们执行操作。



目前PagePlug支持两种形式的动态评估属性的 JavaScript 代码：

* PagePlug 支持在代码器里编写单行代码，`{{ }}`并将括号内的任何内容解释为 JavaScript 表达式。JS 表达式的输出绑定到相应的属性。您可以为诸如对数组执行转换或对条件表达式使用三元运算符等情况编写单行代码。

例子：

```
/*Filter the data array received from a query*/
{{ QueryName.data.filter((row) => row.id > 5 ) }}

/*Ternary condition*/
{{SelectWidgetName.selectedOptionValue === "1" ? "Option 1" : "Option 2" }} 
```

* 有时，您可能必须在一行中链接多个操作，例如运行查询、调用函数/方法、使用条件表达式等，以实现所需的结果。

例子：显示如何在成功执行查询时运行多个`updateData`操作

```
{{updateData.run(() => {getData.run(), closeModal('ModalName')}, () => {})}}
```

#### 如果您的表达式变得过于复杂或具有挑战性而无法放在一行中，使用[**立即调用函数表达式 (IIFE)**](https://developer.mozilla.org/en-US/docs/Glossary/IIFE)编写带有返回语句的函数或代码块。



例子：此示例显示如何编写按钮的`onClick`事件侦听器以执行一组操作。

```
{{
  storeValue("userID", 42);  
  console.log(appsmith.store.userID); 
  showAlert("userID saved");
}}
```

下面的示例显示了如何使用**IIFE**重组无效的代码内容

* 错误代码

```
/*Call a query to fetch the results and filter the data*/
{{ 
   const array = QueryName.data;
   const filterArray = array.filter((row) => row.id > 5);
   return filterArray;
}}

/* Check the selected option and return the value*/
{{ 
  if (Dropdown.selectedOptionValue === "1") {
      return "Option 1";
  } else {
      return "Option 2";
  }
}}
```

* 正确代码

```
/* Call a query and then manipulate its result */
{{ 
  (function() {
      const array = QueryName.data;
      const filterArray = array.filter((row) => row.id > 5);
      return filterArray;
   })()
}}

/* Verify the selected option and return the value*/

{{ 
  (function() {
      if (Dropdown.selectedOptionValue === "1") {
        return "Option 1";
      } else {
        return "Option 2";
      }
   })()
}}
```



## 2、内置的 JS 库介绍：

<figure><img src="../../.gitbook/assets/image (135).png" alt=""><figcaption></figcaption></figure>

内置的 JavaScript 库为数据操作、数字运算、日期和时间处理等常见任务提供了一系列全面的功能。无需任何额外安装或设置即可访问和使用这些库。

| 库名称       | 介绍                                                                       | 文档地址                                                                                                             |   版本号   |
| --------- | ------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------- | :-----: |
| lodash    | <p></p><p>Lodash为常见的编程任务提供函数，例如格式化数据、遍历集合以及操作数组和对象。</p>                  | [https://lodash.com/docs/](https://lodash.com/docs/)                                                             | 4.17.21 |
| moment    | Moment通过提供用于解析、验证、操作和显示日期和时间的函数，简化了在 JavaScript 中使用日期和时间的工作。             | [https://momentjs.com/docs/](https://momentjs.com/docs/)                                                         |  2.29.4 |
| xmlParser | xmlParser可用于在 JavaScript 中解析和操作 XML 数据。                                  | [https://naturalintelligence.github.io/fast-xml-parser/](https://naturalintelligence.github.io/fast-xml-parser/) |  3.17.5 |
| forge     | forge是TLS协议在 JavaScript 中的完全原生实现，一组加密实用程序，以及一组用于开发利用许多网络资源的 Web 应用程序的工具。 | [https://github.com/digitalbazaar/forge#introduction](https://github.com/digitalbazaar/forge#introduction)       |  1.3.0  |

