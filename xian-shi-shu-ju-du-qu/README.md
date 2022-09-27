# 显示数据 (读取)

本文档假定您已成功 [链接到数据源](https://docs.appsmith.com/core-concepts/connecting-to-data-sources) 并具有获取数据的查询.

### 在小部件中显示数据 <a href="#e5-b0-8f-e9-83-a8-e4-bb-b6" id="e5-b0-8f-e9-83-a8-e4-bb-b6"></a>

> Appsmith 是反应式的，因此只要查询中的数据发生变化，小部件就会自动更新。

例如，您可以将查询的结果绑定如下

```
//{{ fetch_users.data.users }}
```

![](../.gitbook/assets/111.gif)

{% hint style="warning" %}
每个小部件属性都有一个特定的数据类型，用于验证其值。如果数据类型不匹配，则会抛出错误。这可以使用 javascript 来转换属性的值来解决。
{% endhint %}

### 转换数据 <a href="#e8-bd-ac-e6-8d-a2-e6-95-b0-e6-8d-ae" id="e8-bd-ac-e6-8d-a2-e6-95-b0-e6-8d-ae"></a>

将查询数据绑定到属性时,您可以在内部使用 Javascript 来转换查询数据.让我们举一个 Query 的例子,它返回一个需要在下拉列表中填充的对象数组.直接绑定数据会报错如下图

下拉菜单在其选项字段中需要一个Array\<label, value> 因此要将此数据连接到下拉菜单,我们需要转换下拉选项属性中的数据.

**示例查询数据**

```javascript
[
  {
    "id": 1,
    "name": "test",
    "status": "APPROVED",
    "gender": "",
    "avatar": "https://robohash.org/sednecessitatibuset.png?size=100x100&set=set1",
    "email": "barty.crouch@gmail.com",
    "address": "St Petersberg #911 4th main",
    "createdAt": "2020-03-16T18:00:05.000Z",
    "updatedAt": "2020-08-12T17:29:31.980Z"
  },
  {
    "id": 2,
    "name": "Jenelle Kibbys",
    "status": "APPROVED",
    "gender": "Female",
    "avatar": "https://robohash.org/quiaasperiorespariatur.bmp?size=100x100&set=set1",
    "email": "jkibby1@hp.com",
    "address": "85 Tennessee Plaza",
    "createdAt": "2019-10-04T03:22:23.000Z",
    "updatedAt": "2019-09-11T20:18:38.000Z"
  },
  {
    "id": 3,
    "name": "Demetre",
    "status": "APPROVED",
    "gender": "Male",
    "avatar": "https://robohash.org/iustooptiocum.jpg?size=100x100&set=set1",
    "email": "aaaa@bbb.com",
    "address": "262 Saint Paul Park",
    "createdAt": "2020-05-01T17:30:50.000Z",
    "updatedAt": "2019-10-08T14:55:53.000Z"
  }
]
```

**转换代码**

以下示例遍历数据集并以某种 `Array<label, value>` 格式返回数据

```javascript
{{
  QueryName.data.map((row) => {
      return { label: row.name, value: row.id };
  });
}}
```
