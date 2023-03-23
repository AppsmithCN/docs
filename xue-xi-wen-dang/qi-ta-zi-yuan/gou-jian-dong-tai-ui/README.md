---
description: 小部件是 Appsmith 的 UI 构建块.小部件使您能够通过简单的配置和零 HTML/CSS 来可视化、捕获和组织数据.
---

# 构建动态 UI

本文档假定您了解显示数据和捕获数据的基础知识,并扩展了构建对用户输入和系统数据作出反应的动态 UI 的概念

{% embed url="https://youtu.be/vlx8TEuep5I" %}

## 动态属性 <a href="#e5-8a-a8-e6-80-81-e5-b1-9e-e6-80-a7" id="e5-8a-a8-e6-80-81-e5-b1-9e-e6-80-a7"></a>

小部件的每个属性都可以使用 handlebars 中的 javascript 动态描述 `{{}}` . 没有输入来编写 javascript 的属性可以通过单击它们旁边的 JS 按钮来动态化.这会将属性转换为可用于编写代码的输入字段.

![](<../../../.gitbook/assets/构建动态 UI - 图1.gif>)

## 更新小部件数据 <a href="#e6-9b-b4-e6-96-b0-e5-b0-8f-e9-83-a8-e4-bb-b6-e6-95-b0-e6-8d-ae" id="e6-9b-b4-e6-96-b0-e5-b0-8f-e9-83-a8-e4-bb-b6-e6-95-b0-e6-8d-ae"></a>

让我们以显示产品列表的表格为例.当用户在表中选择了一个产品时,我们可能希望更新一个表单中的产品信息,以便用户可以更新产品.

![](../../../.gitbook/assets/构建动态UI-图2.gif)

为了实现这一点,我们可以使用表格中选择的相应值填充每个表单小部件的默认值.我们可以使用它的名称来引用 Tables selectedRow 属性 **`{{ }}`**

获取产品名称输入 (Default Text property)

```javascript
{{ Table1.selectedRow.productName }}
```

获取 MRP 输入 (Default Text property)

```javascript
{{ Table1.selectedRow.mrp }}
```

获取类别下拉列表 (Default Option property)

```javascript
{{ Table1.selectedRow.category }}
```

这里 Table1 是小部件的名称

![](<../../../.gitbook/assets/构建动态UI -图3.gif>)
