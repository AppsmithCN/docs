# 动作错误

### 1、超时

如果您的 API / DB 查询超时，可能是由于以下原因之一

* 您的 API / 数据库位于无法从 appsmith 实例访问的 VPC 后面。这可以通过将数据库或 VPC 中的 PagePlug实例列入白名单来解决。
* 您的 API / 查询响应时间过长。这可以通过使用获取较小的数据集来解决

服务器端分页或在设置部分增加API /查询的超时

### 2、配置

```
getUsers failed to execute. Please check its configuration code
```

此消息指示操作配置中的错误。您可以导航到此状态下的API /查询并查看它遇到的错误。如果错误间歇性发生，可能是由于配置中的某个值在运行 API / 查询时不可用。

### 3、强制参数空

```
Mandatory parameters 'Action' and 'Bucket Name' are missing
```

```
Required parameter 'File Path' is missing
```

```
Missing action name (like `ListTables`, `GetItem` etc.)
```

```
Document/Collection path cannot be empty
```

```
Missing Firestore method code
```

这种类型的消息意味着查询编辑器表单中至少有一个必填/必填字段丢失。

可以通过编辑查询编辑器表单并提供错误消息中提到的参数来修复此错误。

### 4、缺少查询

```
Missing required parameter: Query
```

```
needs a non-empty body to work code
```

```
Body is null or empty code
```

这些消息中的任何一条都表明查询正文已留空。

可以通过编辑查询表单并提供查询正文来修复此错误。

### 5、无效查询

```
Not a valid Redis command code
```

```
Query preparation failed while inserting value code
```

这种类型的消息表示查询主体的语法无效。

可以通过在查询编辑器表单中提供有效语法来修复此错误。

### 6、编码

```
File content is not base64 encoded code
```

此消息表示查询期望base64 编码值作为内容主体，但传递给它的实际值不是 base64 编码的。

可以通过将 base64 编码值作为查询中的文件内容参数传递来修复此错误。

### &#x20;7、无效号码

```
Parameter 'Expiry Duration of Signed URL' is NOT a number
```

此消息表示消息中提到的查询参数需要一个数字，但在查询表单中提供了一个非数字值。

可以通过编辑查询表单并提供有效数字作为上述参数的输入来修复此错误。

### 8、JSON解析

```
Error parsing the JSON body
```

```
Error converting array to ND-JSON
```

```
Unable to parse condition value as a JSON list
```

此消息表示作为参数传递给查询的JSON字符串不是有效的 JSON 字符串。

可以通过编辑查询表单并将有效的 JSON 字符串作为参数传递来修复此错误。
