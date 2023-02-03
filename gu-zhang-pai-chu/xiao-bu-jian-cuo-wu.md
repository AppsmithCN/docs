# 小部件错误

本节帮助您解决 PagePlug 平台上的常见小部件错误。



### 1、绑定错误 <a href="#binding-errors" id="binding-errors"></a>

从API、查询、JS 对象将数据绑定到小部件时，您可能会看到以下错误。

### 2、同步字段错误 <a href="#sync-field-error" id="sync-field-error"></a>

在需要数据但不能用于触发操作的小部件属性中执行 API、查询、JS 对象时，您可能会看到此错误。

![无法触发错误操作](https://docs.appsmith.com/assets/images/Troubleshooting-Widget-errors-action-cannot-be-triggered-8c55e8cd976a5527cbbd3fd3a1b5160b.png)

&#x20;   **错误信息：**

{% hint style="info" %}
Found a reference to \{{action\}} during evaluation. Sync fields cannot execute async framework actions. Please remove any direct/indirect references to \{{action\}} and try again.
{% endhint %}

or

{% hint style="info" %}
Found a Promise() during evaluation. Sync fields cannot execute asynchronous code.
{% endhint %}

&#x20; **导致的原因：**

Action 是指 API、Query 或 JS 对象的执行。您只能通过将其绑定到异步字段来执行操作。当您将操作绑定到只需要数据的同步字段时，它会抛出错误。

示例：如果您正在表的属性中执行`storeValue()`函数。`TableData`该`TableData`属性需要数据但无法执行函数，并导致错误。同样，如果您尝试`<JSOBJECT_NAME.FUNCTION_NAME>`在`TableData`属性中执行 JS 对象函数，它会抛出错误。



&#x20; **解决方案：**

调用 API、查询或 JS 对象的数据属性。

例如，你有一个 JS 对象`getLoggedInUserInfo`，它有一个函数`getFullNameOfLoggedInUser`。该函数返回登录用户的全名。您希望添加全名并创建欢迎文本，`Welcome! <LOGGED_IN_USER_NAME>`. `getFullNameOfLoggedInUser`通过调用`.data`属性将函数的响应绑定到文本小部件。`{{}}`要绑定响应，请在小胡子 ( ) 符号中添加以下代码片段。

```
 getLoggedInUserInfo.getFullNameOfLoggedInUser.data
```

### 3、JSON 格式错误 <a href="#json-form-errors" id="json-form-errors"></a>

使用JSON 表单小部件时，您可能会看到以下错误。

#### &#x20;   3.1源数据超过 50 个字段 <a href="#source-data-exceeds-50-fields" id="source-data-exceeds-50-fields"></a>

当您尝试将大型查询/API 响应绑定到JSON 表单小部件的源数据属性时，您可能会看到一条错误消息。

&#x20;       **错误信息：**

{% hint style="info" %}
Source data exceeds 50 fields. Please update the source data.
{% endhint %}

&#x20;     **导致的原因：**

当您尝试绑定时可能会导致问题：

* 大量的多个 JSON 对象
* 一个巨大的 JSON 对象，它有很多字段
* 整个查询数据而不是表中的选定行或触发行

![当数据超过 50 个字段时](https://docs.appsmith.com/assets/images/Troubleshooting\_\_Widget\_Errors\_\_JSON\_Form\_Errors\_\_Source\_Exceeds\_50\_Fields-59d788e3ed8536545bdb9e5616ee0654.png)

&#x20;    **解决方案：**

确定问题是否由以下原因引起：

* **大型数组或大型 JSON 对象**- 您可以重新查看数据并评估是否需要在 UI 上显示所有数据，因为导航超过 50 个字段会让您的用户感到痛苦。
* **您绑定到源数据的整个查询响应**- 您重新检查您尝试绑定的源数据字段并选择要绑定的选定行/触发行。

确定数据的新结构后，前往源数据字段进行更改。

{% hint style="danger" %}
如果您找不到您要找的东西并且需要帮助调试错误，请在github上提问或者是在开源社区请教PagePlug静静
{% endhint %}
