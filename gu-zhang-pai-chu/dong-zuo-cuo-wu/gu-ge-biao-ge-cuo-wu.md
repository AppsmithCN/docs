# 谷歌表格错误

在 Pageplug 上使用Google 表格插件是将 Google 表格用作构建应用程序的数据源的最便捷方式。但有时，我们在编辑和删除 Google 表格上的数据时，经常会在特定查询时遇到小错误。在本指南中，我们将了解人们在使用 Google 表格时经常遇到的一些错误。



### 1、预期行

当将无效格式传递给插入或更新工作表操作时，会发生此错误。请求正文必须是一个对象，其键与 Google 表格的标题匹配。标题行由 google 表格的索引确定。下面是一个示例行对象

```
{
    "rowIndex":{{Table1.selectedRow.rowIndex}},
    "Name Input": "{{editFund.text}}",
    "Designation": "{{editDesignation.text}}",
    "Location": "{{editLocation.text}}"
}
```

### 2、缺少必填字段行

**在 Google 表格上**编辑数据：要在 Google 表格上编辑数据，我们必须使用插件中的**编辑表格行**查询。这样做时，我们可能会遇到**Missing required field row index error**。当我们错过**Row Object**属性`rowIndex`中的键时，就会发生这种情况。

例如，您正在使用表 ( `Table1`) 中具有以下名称的输入小部件编辑三个字段：

* 名称输入：`nameInput`
* 电子邮件输入：`emailInput`
* 位置输入：`locationInput`

要编辑这些，您`Row Object`应该设置为以下内容：

```
{
    "rowIndex":{{Table1.selectedRow.rowIndex}},
    "Name Input": "{{editFund.text}}",
    "Designation": "{{editDesignation.text}}",
    "Location": "{{editLocation.text}}"
}
```

正如我们在`Edit Sheet Row`查询中看到的那样，我们必须传递一个`rowIndex`，否则它会抛出**Missing required field row index**错误。

### 3、插件无法解析 JSON <a href="#plugin-failed-to-parse-json-error" id="plugin-failed-to-parse-json-error"></a>

从 Pageplug 创建或编辑 Google 表格上的数据时，我们应该在 Row Object 属性中传递需要编辑的对象。在这里，我们在将数据解析为JSON对象时可能会遇到错误。下面是一个示例，作为在 Pageplug 的 Google 表格上编辑/创建新行对象的参考。

在这里，我们的目标是在 Google 表格上创建一个新行，为此我们将使用**插入表格行**查询。在此示例中，我们将使用以下行对象：

```
{
  "Investment Fund": "{{addFund.text}}",
  "Location": "{{addLocation.text}}",
  "Name of Investor": "{{addInvestorInput.text}}",
  "Designation": "{{addDesignation.text}}",
  "Interesting Portfolio Companies": "{{addPortifolio.text}}"
}
```

在这里，键通常是 Google 表格中的列名，对应的值是使用 mustache运算符从输入小部件`{{}}`计算的值。

{% hint style="danger" %}
提示

确保删除JSON末尾不必要的逗号
{% endhint %}

