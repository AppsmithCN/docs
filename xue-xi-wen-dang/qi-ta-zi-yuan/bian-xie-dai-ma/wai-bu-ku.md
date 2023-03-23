---
description: Appsmith 平台包括 JavaScript 实用程序库,可用于处理 `{{ }}` 绑定中的数据.
---

# 外部库

### JavaScript 库参考 <a href="#javascript-e5-ba-93-e5-8f-82-e8-80-83" id="javascript-e5-ba-93-e5-8f-82-e8-80-83"></a>

* [lodash](https://lodash.com/docs/4.17.15)
* [moment](https://momentjs.com/docs/)
* [btoa](https://github.com/dankogai/js-base64#readme)
* [atob](https://github.com/dankogai/js-base64#readme)
* [xmlParser](https://github.com/NaturalIntelligence/fast-xml-parser#readme)

### 使用 JavaScript 库 <a href="#e4-bd-bf-e7-94-a8-javascript-e5-ba-93" id="e4-bd-bf-e7-94-a8-javascript-e5-ba-93"></a>

外部库可以在内部任何地方\{{ \}}使用,就像在应用程序的其余部分使用 JavaScript 一样.JavaScript 库的签名与其文档中提到的完全相同

#### 示例: Lodash <a href="#e7-a4-ba-e4-be-8b-lodash" id="e7-a4-ba-e4-be-8b-lodash"></a>

以下是Lodash `_.map` 工具的使用实例. fetchFruits是API/查询的名称

```javascript
{{
  _.map(fetchFruits.data, (fruit) => { 
    return { label: fruit.name, value: fruit.id } 
    })
}}
```

#### Example: moment <a href="#example-moment" id="example-moment"></a>

在查询中使用的 moment.js 实用程序示例 `format`

```sql
insert into users (name, email, createdDate) values 
('John', 'john@appsmith.com', {{moment().format("YYYY-MM-DD")}})
```
