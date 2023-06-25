# \{{\}}绑定原理

{% hint style="info" %}
文档源自PagePlug社区8群的茂行整理
{% endhint %}

PagePlug是一款开源的为开发者而设计的构建内部应用的低代码平台。

在PagePlug中，我们的开发者可以在应用内编写js代码来定义业务逻辑，这个代码需要写在\{{\}}里面，js代码可以用来创建sql查询，引用API，或者触发操作。

此功能可让您以最少的配置控制您的应用程序的行为方式。本质上，该平台将以优化的方式评估所有这些代码，以确保该应用程序保持高性能和响应性。

让我们举一个将查询响应绑定到表格小部件的示例。&#x20;

这一切都从绑定括号 \{{\}} 开始 。当平台在小部件或操作配置中看到这些括号和其中的一些代码时，它会将字段标记为动态字段，以便我们的评估者稍后可以选择它。在我们的示例中，让我们将 usersQuery 绑定到 usersTable

<figure><img src="../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>

由于我们在 tableData 字段中添加了此绑定，我们将标记此字段并将其存储在我们的小部件配置中

```
// usersTable config
{
  "usersTable": {
        ...
        "tableData": "{{
            usersQuery.data
                .map(row => ({
                    name: row.name,
                    email: row.email
                }))
            }}",
        "dynaminBindingPathList": [
            {"key": "tableData"}
            ...
        ]
    }
}
```

在后台，我们的评估侦听器始终留意此类需要评估的事件。对于我们的示例，这是一个绝对需要评估的场景，因此它启动了我们的评估程序。 我们将当前构建的应用程序数据列表(又叫DataTree)传递给评估线程，并耐心等待它的回音。

```
// DataTree
{
    "usersQuery": {
        "config": {...},
        "data": [...]
    },
    "usersTable": {
        "tableData": "{{
            usersQuery.data
                .map(row => ({
                    name: row.name,
                    email: row.email
                }))
            }}",
        "dynaminBindingPathList": [{"key": "tableData"}]
    }
}

```

出于性能原因，我们使用 [web workers](https://developer.mozilla.org/en-US/docs/Web/API/Web\_Workers\_API)，在单独的后台线程中运行我们的评估过程。这可确保运行时间超过 16 毫秒的评估周期不会挂断主线程，从而使应用始终能响应用户事件。



在线程内部，事件侦听器收到唤醒呼叫并开始工作。

* 获取差异：首先它将计算和上次DataTree的差异。这将确保我们只处理更改而不是整棵树。在我们的示例中，我们会看到usersTable.tableData已经更改并且usersTable.dynamicBindingPathList有一个新条目。它接受每个差异，过滤任何不重要的更改，然后处理其余的。
* 使用依赖关系图获取评估顺序：它还维护各种实体属性之间的DependencyMap关系。评估器将关注是否有绑定已更改并相应地重新创建排序顺序。对于我们的示例，我们推断usersTable.tableDatanow 取决于usersQuery.data。这意味着在我们评估表数据之前应该始终评估查询响应，并且每当我们看到查询响应发生变化时，我们也需要重新评估表数据。

```
// DependencyMap
{
    ...
    "usersTable.tableData": ["usersQuery.data"]
}

// Evaluation order
[
    "usersQuery.data",
    "usersTable.tableData"
]

```

* 评估：创建优化的评估顺序后，我们将按照所述顺序评估树的更新。评估通过封闭的 eval 函数进行，整个 DataTree 充当其作用域。这就是为什么我们可以在我们的代码中直接引用我们DataTree的任何对象。

```
// Evaluator

const code = `
  usersQuery.data.map(row => ({
    name: row.name,
    email: row.email
  }))
`;

const scriptToEvaluate = `
  function closedFunction () {
    const result = ${code};
    return result
  }
  closedFunction()
`;

const result = eval(scriptToEvaluate);

```

* 验证和解析：我们期望评估后返回的值是小部件期望的数据类型，这样就算代码返回了一些错误，也能确保小部件始终获得可预测的数据。这对于评估顺序中的任何函数也是需要的，如果它引用这个字段，将始终获得一个合理的数据类型来使用。

这就是评估的整个过程。最后，我们将得到一个全面评估的DataTree，然后我们可以将其发送回主线程并开始侦听任何新事件以再次执行整个过程。

```
// Evaluated DataTree
{
    "usersQuery": {
        "data": [...] 
    }
    "usersTable": {
        "tableData": [...]
    }
}

```

我们的主线程会收到一个事件，表示评估已完成，新的评估DataTree 将会存储在 app redux 状态中。小部件将从redux中获取数据并展示。

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

### 总结我们的理念

* Pull vs push：

在为不同的开发人员构建低代码应用程序时，我们认真考虑了编写的代码如何与平台的其余部分一起工作。我们希望配置易于启动，又能保持功能强大。出于这个原因，我们选择了基于拉的架构而不是推。这意味着在大多数地方，您不必考虑将数据绑定到到特定的字段。您编写的代码将从全局中提取DataTree的所有内容，并将其设置到您编写它的字段中。这样，当底层数据发生变化时，它就会传递给所有依赖于它的字段，而作为开发人员的您不必编排 ui 。

* 单向数据流：

由于我们的应用是建立在 React.js 和 Redux 之上，我们强烈支持单向数据流模型。这意味着您不能从应用程序的其他部分直接将表的数据设置到表字段中。如果确实需要更新表，则必须触发查询运行，这将导致表使用新数据重新呈现。这有助于您编写的代码易于推理并易于查找错误。它还将每个小部件和操作的逻辑封装在自身中，以实现良好的关注点分离。
