# console对象

控制台[对象](https://developer.mozilla.org/en-US/docs/Web/API/Console\_API)提供了一种简单的方法，可以将日志消息从浏览器发送到开发控制台，或者在发生错误时在浏览器中显示消息。默认情况下，控制台输出会出现在浏览器的控制台选项卡中，您可以通过调用浏览器的开发人员工具来查看。

控制台是任何开发人员工具包中不可或缺的一部分——它允许您通过在消息、错误和警告发生时记录它们来监控您的程序正在做什么。这些信息丰富的日志可以更轻松地调试您的代码并找到错误和意外行为的来源。

Appsmith 提供全局控制台对象，用于在 JavaScript 代码中记录有关[API](https://docs.appsmith.com/core-concepts/connecting-to-data-sources/authentication)、[Queries](https://docs.appsmith.com/core-concepts/data-access-and-binding/querying-a-database)和[Widgets 属性的信息。](https://docs.appsmith.com/reference/widgets)使用 mustache 登录`{{}}`小部件属性或[直接在您的代码中](https://docs.appsmith.com/core-concepts/writing-code/javascript-editor-beta#use-case)调用控制台对象。

笔记

控制台日志**不会被**保存，并且**仅**可用于**当前会话。**

### [方法](https://docs.appsmith.com/reference/appsmith-framework/console-object#methods) <a href="#methods" id="methods"></a>

控制台方法是在记录不同类型消息的控制台对象上执行的函数。您可以使用以下方法记录消息：

* 日志
* 错误
* 警告

信息

控制台对象**仅**支持**log**、**error**和**warn**方法。您还可以使用**信息**和**调试**方法。**但是，这些方法提供与日志**方法相同的功能。

例如，您正在构建一个应用程序并集成外部 API 以获取输入。您的应用程序代码的行为因 API 生成的响应类型而异。

[这是JS 对象](https://docs.appsmith.com/core-concepts/writing-code/javascript-editor-beta#code-workflow)的代码片段，您在其中调用外部 API( `getTaskList`)，并根据生成的响应返回所需的输出。您要么发送电子邮件通知用户，要么提醒管理员无需执行任何操作。

```
export default {
    notifyUserIfTaskIsIncomplete: async () => {
        let isTaskIncomplete = false;
        const taskList = getTaskList.data.record;
        for (const task of taskList) {
            if(task.ownerId == Table1.selectedRow.ownerId && task.endDate < Date() && task.status != "Completed") {
                isTaskIncomplete = true;
                break;
            }
        }
        if (isTaskIncomplete){
            sendEmailToNotifyUser.sendEmail();
            return;
        } 
        showAlert("No action is needed");
}
```

API 在独立执行时生成正确的响应，并且您的应用程序代码按预期工作。但是，代码在集成期间失败，因为 API 响应未生成或不符合预期。

要排除错误，您可能需要记录一些消息：在 API 调用开始时、您正在[构建并传递给 API 的](https://docs.appsmith.com/core-concepts/connecting-to-data-sources/authentication/connect-to-apis#passing-data-parameters-to-api-calls)参数、您从 API 获得的响应以及结果。在这里，控制台对象就派上用场了。您可以使用不同的方法，例如[`log`](https://docs.appsmith.com/reference/appsmith-framework/console-object#log)记录方法的开始、参数和结果，[`error`](https://docs.appsmith.com/reference/appsmith-framework/console-object#error)记录 API 返回的错误消息，以及[`warn`](https://docs.appsmith.com/reference/appsmith-framework/console-object#warn)记录 API 返回的警告。

#### [日志](https://docs.appsmith.com/reference/appsmith-framework/console-object#log) <a href="#log" id="log"></a>

该`console.log()`方法向日志选项卡输出一条消息。消息可以是单个字符串值、多个字符串值或 JavaScript 对象。

笔记

控制台方法**不**支持**字符串替换**。

为了输出入门级消息、参数值和最终结果，您可以添加 console.log 消息，如下所示：

```
export default {
    notifyUserIfTaskIsIncomplete: async () => {
        console.log("Entered method- notifyUserIfTaskIsCompleted");
        let isTaskIncomplete = false;
        console.log("Selected Owner Id: " + Table1.selectedRow.ownerId);
        const taskList = getTaskList.data.record;
        for (const task of taskList) {
            if(task.ownerId == Table1.selectedRow.ownerId && task.endDate < Date() && task.status != "Completed") {
                isTaskIncomplete = true;
                break;
            }
        }
        if (isTaskIncomplete){
            sendEmailToNotifyUser.sendEmail();
            return;
        } 
        showAlert("No action is needed");
        console.log("Exitted method- notifyUserIfTaskIsCompleted");
    }
}
```

[可以在日志选项卡](https://docs.appsmith.com/core-concepts/writing-code/javascript-editor-beta#logs-tab)中记录和查看提供给方法的方法入口、出口和参数。

![](https://docs.appsmith.com/assets/images/Appsmith\_Framework\_\_Console\_Object\_\_Console.log\_messages-ce783dc37a8855503d336ea84da6fbc5.png)

要记录单个字符串、多个字符串或 JavaScript 对象，请使用 for 循环中的代码片段打印任务对象，如下所示：

```
console.log("Current from the tasklist response: " , task);
```

您可以检查作为响应一部分的任务对象及其属性，以评估条件并在必要时修复代码。

#### [错误](https://docs.appsmith.com/reference/appsmith-framework/console-object#error) <a href="#error" id="error"></a>

该方法向[日志选项卡](https://docs.appsmith.com/core-concepts/writing-code/javascript-editor-beta#logs-tab)`console.error()`输出一条错误消息。它可以记录一个字符串，按原样编写 - 使用自定义错误对象 - 或者使用返回字符串或打印自定义对象的函数。

笔记

控制台方法**不**支持**字符串替换。**

查看日志选项卡中打印的条目、参数和退出消息后，您不确定是什么破坏了代码。要进一步排除故障，您应该将 API 调用和方法逻辑包含在一个`try-catch`块中。您可以有一个自定义函数来评估 API 可能抛出的所有类型的错误，输出适当的消息，并可以使用 console.error() 方法打印返回的消息。

```
printErrorMessages: (errorCode) => {
    if (errorCode == "403 Forbidden") {
        return "Access Denied!";
    } else if (errorCode == "503 Service Unavailable") {
        return "The server is either not available or shut down.";
    }
}
```

使用`console.error()`方法中的catch块中的`notifyUserIfTaskIsIncomplete`方法打印方法返回的错误信息`printErrorMessages`。

```
export default {
    notifyUserIfTaskIsIncomplete: async () => {
        console.log("Entered method- notifyUserIfTaskIsCompleted");
        let isTaskIncomplete = false;
        console.log("Selected Owner Id: " + Table1.selectedRow.ownerId);
        try{
                const taskList = getTaskList.data.record;
                for (const task of taskList) {
                console.log("iterableTask from the tasklist response: " , task);
                if(task.ownerId == Table1.selectedRow.ownerId && task.endDate < Date() && task.status != "Completed") {
                    isTaskIncomplete = true;
                    break;
                }
            }
                if (isTaskIncomplete){
                    sendEmailToNotifyUser.sendEmail();
                    return;
                } 
                showAlert("No action is needed");
                console.log("Exitted method- notifyUserIfTaskIsCompleted");
        }catch (err) {
            console.error(this.printErrorMessages(err.name));
        }
    },
    printErrorMessages: (errorCode) => {
        if (errorCode == "401 Unauthorized") {
            return "Access Denied!";
        }
    }
}
```

可以在日志选项卡中记录和查看错误消息。

![](https://docs.appsmith.com/assets/images/Appsmith\_Framework\_\_Console\_Object\_\_Console.error\_messages-535ef3c38389cc0993aea2f958cd7c5b.png)

查看错误消息并更正代码后，您希望确保代码不应该引发任何可能停止处理的警告。为此，请使用该`console.warn()`方法。

#### [警告](https://docs.appsmith.com/reference/appsmith-framework/console-object#warn) <a href="#warn" id="warn"></a>

该方法在[日志选项卡](https://docs.appsmith.com/core-concepts/writing-code/javascript-editor-beta#logs-tab)`console.warn()`中记录一条警告消息。与和一样，您可以将字符串和 JavaScript 对象记录为警告消息。`console.log()console.error()`

笔记

控制台方法**不**支持**字符串替换**。

警告表示在运行时可能出现问题的情况，因此不应忽略它们，并且可以使用该`console.warn()`方法进行记录。

```
console.warn(this.printWarningMessages()); 
```

该`printWarningMessages`方法是一种自定义方法，它返回警告消息并将它们记录在[日志选项卡](https://docs.appsmith.com/core-concepts/writing-code/javascript-editor-beta#logs-tab)中。

![](https://docs.appsmith.com/assets/images/Appsmith\_Framework\_\_Console\_Object\_\_Console.warn\_messages-4f1596a248c31e471eb202878477dce1.png)

您可以查看警告消息，`API.errorCode(Number1) is deprecated.`并根据需要修复代码。

使用控制台方法时：`log`、`error`和`warn`，您可以调试复杂的执行逻辑并修复问题。

### 使用[控制台](https://docs.appsmith.com/reference/appsmith-framework/console-object#benefits-of-using-console) <a href="#benefits-of-using-console" id="benefits-of-using-console"></a>

控制台对象有助于快速调试并定位问题的根本原因。它易于使用，不需要开发人员工具。

* **Ease**：控制台对象对于记录应用程序的运行时上下文很有用。您可以使用`console.log()`、`console.error()`或记录特定上下文中的消息`console.warn()`。
* **在 Appsmith 编辑器中可用**：消息记录在日志选项卡中，无需调用浏览器的开发人员工具即可在 Appsmith 编辑器中访问。

### 查看记录的[消息](https://docs.appsmith.com/reference/appsmith-framework/console-object#viewing-the-logged-messages) <a href="#viewing-the-logged-messages" id="viewing-the-logged-messages"></a>

日志选项[卡](https://docs.appsmith.com/core-concepts/writing-code/javascript-editor-beta#logs-tab)显示记录的消息。它显示系统和用户生成的消息（控制台对象的日志、错误和警告方法用于记录用户生成的消息）。用户可以使用以时间戳为前缀的图标来区分它们。系统生成的消息有一个桌面图标，而用户生成的消息有一个用户图标前缀。

它还显示消息源（[JS 对象](https://docs.appsmith.com/core-concepts/writing-code/javascript-editor-beta)/[小部件](https://docs.appsmith.com/reference/widgets)），因此您可以导航到[小部件](https://docs.appsmith.com/reference/widgets)或[JS 对象](https://docs.appsmith.com/core-concepts/writing-code/javascript-editor-beta)。

![](https://docs.appsmith.com/assets/images/Appsmith\_Framework\_\_Console\_Object\_\_Viewing\_logged\_messages-13ee44cc82cf219de3a24cab1b34b3fd.png)

信息

当您在日志选项卡中时，您可以通过控制台日志过滤它们，这些日志是用户生成的消息。

![](https://docs.appsmith.com/assets/images/Appsmith\_Framework\_\_Console\_Object\_\_Viewing\_logged\_messages\_Filter-1a1cb34c72de1da4873ec0e24e55e642.png)

使用控制台对象进行调试比直接在 Appsmith 编辑器中使用调试器更高效、更快速、更容易。[如果您有复杂的 API 逻辑、多个JS 对象](https://docs.appsmith.com/core-concepts/writing-code/javascript-editor-beta)或需要调试的复杂查询，则无需担心。

信息

如果您遇到问题，请阅读[JS 错误](https://docs.appsmith.com/help-and-support/troubleshooting-guide/js-errors)/[操作错误](https://docs.appsmith.com/help-and-support/troubleshooting-guide/action-errors) [故障排除指南或通过](https://docs.appsmith.com/help-and-support/troubleshooting-guide)[Discord](https://discord.com/invite/rBTTVJp)或社区论坛提出您的疑问[。](https://community.appsmith.com/)
