# 编写代码

JavaScript 可以 `{{ }}` 在 Appsmith 的任何地方使用.Appsmith 中的每个实体都可以作为 JavaScript 变量引用,并且可以对它们执行所有 JavaScript 函数和操作.这意味着所有小部件、API、查询以及它们相关的数据和属性都可以在应用程序中的任何位置在车把中引用 `{{ }}`.

Appsmith 目前支持两种形式的 JavaScript 代码来动态评估属性值:

1. 单行代码或函数,例如三元条件

```javascript
{{ QueryName.data.filter((row) => row.id > 5 ) }}
```

1. 立即调用的函数表达式 [IIFE](https://developer.mozilla.org/en-US/docs/Glossary/IIFE)

```javascript
{{ 
  (function() {
      const array = QueryName.data;
      const filterArray = array.filter((row) => row.id > 5);
      return filterArray;
   })()
}}
```

您还可以为事件侦听器编写 JavaScript 代码.对于事件侦听器中的 JavaScript 代码,您可以编写多行 JavaScript,如下所示.

```javascript
{{
  storeValue("userID", 42);  
  console.log(appsmith.store.userID); 
  showAlert("userID saved");
}}
```

## 反应性 <a href="#e5-8f-8d-e5-ba-94-e6-80-a7" id="e5-8f-8d-e5-ba-94-e6-80-a7"></a>

Appsmith 是\[反应性]的([https://en.wikipedia.org/wiki/Reactive\_programming](https://en.wikipedia.org/wiki/Reactive\_programming)) 因此 Appsmith 中的代码本质上是声明性的,并描述了属性的最终状态. 为了更新小部件的属性,与命令式编程不同,程序员将语句编写为

```javascript
// Imperative Style incompatible with appsmith
if (Dropdown1.selectedOption === "John")
    nameInput.setText("John Doe");
```

在 Appsmith 中,程序员在属性窗格中声明 text 属性的状态如下,并且每当 Dropdown1 的值发生变化时,小部件的属性都会响应更新

```javascript
{{ Dropdown1.selectedOption === "John" ? "John Doe" : "" }}
```

这样，只要 Dropdown1 的值发生变化，nameInput 小部件的属性就会进行响应式更新。当用户更改 Dropdown1 值时，nameInput 小部件的文本将根据我们的表达式自动更新。

一般来说，画布上的任何给定小部件都会在其基础值更改或 API / Query 返回新数据时自动更新。

## 单行 JavaScript <a href="#e5-8d-95-e8-a1-8c-javascript" id="e5-8d-95-e8-a1-8c-javascript"></a>

这意味着每当其基础数据更改或 API / 查询返回数据时,小部件都会自动更新.

Appsmith 主要支持在其间编写单行 javascript, `{{ }}` 因为 JavaScript 表达式的值在字段中被替换.这需要我们在一行中链接多个操作以实现结果.

### 有效的 JavaScript <a href="#e6-9c-89-e6-95-88-e7-9a-84-javascript" id="e6-9c-89-e6-95-88-e7-9a-84-javascript"></a>

以下是用于属性值的 JavaScript 的有效示例.

```javascript
{{ QueryName.data.filter((row) => row.id > 5 ) }}
```

```javascript
{{ Dropdown.selectedOptionValue === "1" ? "Option 1" : "Option 2" }}
```

**无效的 JavaScript**

以下是属性值的无效 JavaScript 示例.在这里,我们应该使用立即调用的函数表达式 [IIFE](https://developer.mozilla.org/en-US/docs/Glossary/IIFE)

```javascript
{{ 
   const array = QueryName.data;
   const filterArray = array.filter((row) => row.id > 5);
   return filterArray;
}}
```

```javascript
{{ 
  if (Dropdown.selectedOptionValue === "1") {
      return "Option 1";
  } else {
      return "Option 2";
  }
}}
```

## 多行 JavaScript <a href="#e5-a4-9a-e8-a1-8c-javascript" id="e5-a4-9a-e8-a1-8c-javascript"></a>

如果是 [IIFE](https://developer.mozilla.org/en-US/docs/Glossary/IIFE),Appsmith 确实支持多行 JS .上述无效示例如果按以下方式使用,则变为有效.

```javascript
{{ 
  (function() {
      const array = QueryName.data;
      const filterArray = array.filter((row) => row.id > 5);
      return filterArray;
   })()
}}
```

```javascript
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

> **在里面写评论 ：**
>
> 请注意,您可以使用 JavaScript 的多行注释语法在内部编写注释,但内部不支持 `/* */`, 单行注释. `//`
