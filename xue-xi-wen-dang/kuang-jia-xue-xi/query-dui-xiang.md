---
description: 本页介绍如何使用 Query 对象运行查询并访问响应中的数据。
---

# Query 对象

## run()

调用查询的 **run()** 函数执行该查询。 run() 是**异步的**并返回一个 **promise**，所以你可以使用 .then() 链式调用 和 async/await 这样的异步语法。

### 格式

```javascript
run(params: Object): Promise
```

| 参数     | 描述                                              |
| ------ | ----------------------------------------------- |
| params | 包含要传递到查询中的键值对的对象。使用 \{{ this.params.key \}} 访问。 |

```javascript
// 使用promise语法按顺序链式调用
{{
    Query1.run(params)
        .then(() => {...}) // 成功后执行的回调函数
        .catch(() => {...}) // 遇到错误后执行的回调函数
}}

```



### 参数传递到查询

大多数查询直接从组件实体读取值作为全局变量。在某些情况下，例如在循环内运行查询，可能需要将参数传递给查询，并使用与执行相关的值。

为此，使用 `params` 参数将键值对对象传递到查询中。你可以使用 `{{ this.params.key }}` 在查询中访问这些值。

**示例**

假设需要根据 id 值从数据库中获取特定用户。在此示例中，你将了解如何配置查询和辅助函数以获取 ID 数组并为每个 ID 运行查询。

1.在画布上，你应该有一个 **Table** 组件和一个 **Button** 组件；

<figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

2.使用 pageplug 的模拟 Postgres  数据库(`users`)创建一个名为 **`GetUserById`** 的查询。

<figure><img src="../../.gitbook/assets/image (50).png" alt=""><figcaption></figcaption></figure>

3.将以下 SQL 语句添加到查询中：

```sql
SELECT * FROM users WHERE id = {{ this.params.id }};
```

4.创建一个 JS 对象并将其命名为 `utils` ,编写调用查询并处理其响应的辅助函数

{% tabs %}
{% tab title="promise写法" %}
```javascript
export default {
	myVar1: [],
	myVar2: {},
	test: () => {
		this.getByIds([[1, 4, 8, 34, 16]])
	},
	getByIds: async (ids) => {
		const queries = ids.map(id => {
			return GetUserById.run({"id": id})
		})

		Promise.allSettled(queries)
			.then(queryResponses => queryResponses.map(res => res.value[0]))
			.then(records => storeValue("records", records))
	}
}
```
{% endtab %}

{% tab title="async/await写法" %}
<pre class="language-javascript"><code class="lang-javascript">export default {
	myVar1: [],
	myVar2: {},
	test: () => {
		this.getByIds([[1, 4, 8, 34, 16]])
	},
	getByIds: async (ids) => {
          const queries = ids.map(id => {
            return GetUserById.run({"id": id})
          })
    
    	  const responses = await Promise.allSettled(queries)
    	  const records = await responses.map(promise => promise.value[0])
    	  await storeValue("records", records)
<strong>	}
</strong>}
</code></pre>
{% endtab %}
{% endtabs %}

以上代码片段为其 `ids` 数组中的每个 `id` 运行一次查询，等待数据库的响应，并将生成的表记录存储在 **global.store** 中。

5.现在，当 `utils.getByIds()` 函数使用一组 id 运行时，您将在 **global.store** 中获得结果记录。将此值绑定到 Table 组件的 属性：

```javascript
{{ global.store.records }}
```

<figure><img src="../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>



6.最后，要执行查询，请设置 **Button** 组件的 **onClick** 事件以执行您的辅助函数：

```javascript
{{ utils.test() }}
```

<figure><img src="../../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>



当你单击该按钮时，它会运行你的辅助函数，该函数会在数据库中查询你指定的每个用户信息。

## 属性

| 属性               | 描述                                                 |
| ---------------- | -------------------------------------------------- |
| **data**         | 包含上次成功执行此查询的响应正文。如果在组件的属性字段中引用了此属性，则查询会在页面加载时自动运行。 |
| **responseMeta** | 包含对此查询执行上次响应的元数据。                                  |
| **clear()**      | 清空查询的 `data` 属性中的所有数据。                             |
| **run()**        | 调用时执行查询。不能在同步字段中调用                                 |
