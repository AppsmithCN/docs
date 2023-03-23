# context 对象

PagePlug中的context对象提供有关应用程序当前状态的信息

### [属性](https://docs.appsmith.com/reference/appsmith-framework/context-object#properties) <a href="#properties" id="properties"></a>

Appsmith 上下文对象包含以下属性：

```
{
   store: object,
   URL: object,
   user: object,
   geolocation: object,
   mode: enum
}
```

#### [商店](https://docs.appsmith.com/reference/appsmith-framework/context-object#store) <a href="#store" id="store"></a>

该对象包含应用程序本地存储的键值对。[可以使用storeValue 函数](https://docs.appsmith.com/reference/appsmith-framework/widget-actions/store-value)更新存储的值。可以使用它们的键访问存储中的值。

```
{{ appsmith.store.key }}
```

#### [网址](https://docs.appsmith.com/reference/appsmith-framework/context-object#url) <a href="#url" id="url"></a>

该对象包含与用户所在的当前 URL 关联的所有值。该字段的 queryParams 对象可用于读取使用[navigateTo 函数](https://docs.appsmith.com/reference/appsmith-framework/widget-actions/navigate-to)从其他页面发送到该页面的数据。可以使用以下方法访问 URL 中的值：

```
{{ appsmith.URL }}
```

```
{
  host: string,
  hostName: string,
  fullPath: string,
  pathName: string,
  port: string,
  protocol: string,
  hash: string,
  queryParams: object
}
```

[**主机**](https://docs.appsmith.com/reference/appsmith-framework/context-object#host)

URL 接口的主机属性是一个字符串，其中包括主机名，然后是 ，`:`后跟 URL 的端口（如果[端口](https://docs.appsmith.com/reference/appsmith-framework/context-object#port)可用）。

例子：

```
//{{appsmith.URL.host}}
host:"app.appsmith.com:111"
```

[**主机名**](https://docs.appsmith.com/reference/appsmith-framework/context-object#hostname)

URL 的主机名属性是一个包含**URL 域的**字符串。简单来说，hostname 就是[主机](https://docs.appsmith.com/reference/appsmith-framework/context-object#host)名（不含端口号）。

例子：

```
//{{appsmith.URL.hostname}}
hostName:"app.appsmith.com"
```

[**全路径**](https://docs.appsmith.com/reference/appsmith-framework/context-object#fullpath)

完整路径 URL 指定一个确切的位置（例如页面、应用程序、文件等）。除了域和顶级域 (TLD) 之外，完整路径 URL 还需要包括协议、子域（例如“app”、“support”等）、路径/目标以及可能的文件扩展名以及查询参数。完整路径可以包括：

* 协议
* 子域名
* 域名
* 顶级域 (TLD)
* 小路
* 参数

例子：

```
//{{appsmith.URL.fullPath}}
fullPath:"https://app.appsmith.com/app/demo-app/page1-6324031aa"
```

信息

在前面的示例中，`6324031aa`表示名为 的页面的**ID**`page1`。URL 中的当前页面 slug 是通过组合创建的`$pageName-$pageId`。每个页面都有一个分配给它的唯一页面 ID。

[**路径名**](https://docs.appsmith.com/reference/appsmith-framework/context-object#pathname)

它是由一组路径段组成的字符串，每个路径段都有`/`前缀字符。如果 URL 没有路径段，则空字符串将是路径名属性的值。

例子：

```
//{{appsmith.URL.pathname}}
pathName:"/app/demo-app/page1-6324031aa"
```

[**端口**](https://docs.appsmith.com/reference/appsmith-framework/context-object#port)

URL 的端口属性是一个字符串，其中包含 URL 的端口号。

例子：

```
//{{appsmith.URL.port}}
port:"3000"
```

[**协议**](https://docs.appsmith.com/reference/appsmith-framework/context-object#protocol)

URL 的协议属性是一个字符串，表示 URL 的协议方案，包括`:`.

> 资源名称和协议标识由一个冒号和两个正斜杠彼此分隔。

例子：

```
//{{appsmith.URL.protocol}}
protocol:"https:"
```

[**哈希**](https://docs.appsmith.com/reference/appsmith-framework/context-object#hash)

该值是主题标签（**包括**`appsmith.URL.hash`）之后的字符串。URL 片段标识后跟一个哈希符号（#），这是 URL 接口的哈希属性。**`#`**

例子：

```
//{{appsmith.URL.hash}}
hash:"#n912xhego"
```

[**查询参数**](https://docs.appsmith.com/reference/appsmith-framework/context-object#queryparams)

查询参数是一组预定义的参数，这些参数根据传递的数据定义特定的内容或操作。URL 的所有查询参数都附加在末尾，并以 a`?`作为分隔符。

例子：

```
//{{appsmith.URL.queryParams}}
queryParams:"?name=value&variable=value"
```

#### [用户](https://docs.appsmith.com/reference/appsmith-framework/context-object#user) <a href="#user" id="user"></a>

该对象包含当前经过身份验证的用户的数据。

```
{
  email: string
  username: string
  name: string
  isEnabled: boolean
  accountNonExpired: boolean
  accountNonLocked: boolean
  credentialsNonExpired: boolean
  isAnonymous: boolean
}
```

#### [地理位置](https://docs.appsmith.com/reference/appsmith-framework/context-object#geolocation) <a href="#geolocation" id="geolocation"></a>

该对象包含请求当前用户位置和从此请求接收的坐标的函数[https://developer.mozilla.org/en-US/docs/Web/API/Geolocation\\\_API](https://developer.mozilla.org/en-US/docs/Web/API/Geolocation/\_API)。

```
{
 canBeRequested: boolean,
 getCurrentPosition: Function,
 watchPosition: Function,
 clearWatch: Function,
 currentPosition: {
   coords: {
      accuracy: number,
      altitude: number | null,
      altitudeAccuracy: number | null,
      heading: number | null,
      latitude: number,
      longitude: number,
      speed: number | mull,
   },
   timestamp: number,
 }
}
```

**获取当前位置**

签名：

```
(
 onSuccessCallback?,
 onErrorCallback?,
 options?: { maximumAge?: number, timeout?: number, enableHighAccuracy?: boolean } 
) -> void
```

与原始浏览器 API 几乎相似，除了不需要传递成功回调之外。成功后，该位置将自动存储在`appsmith.geolocation.currentPosition.coords`。如果传递了 onSuccessCallback，则会使用收到的位置信息调用它。

**观看位置**

签名：

```
(
  onSuccessCallback?,
  onErrorCallback?,
  options?: { maximumAge?: number, timeout?: number, enableHighAccuracy?: boolean } 
) -> void
```

与原始浏览器 API 几乎相似，除了不需要传递成功回调之外。成功后，该位置将自动存储在上次更新位置时的更新位置`appsmith.geolocation.currentPosition.coords`。`appsmith.geolocation.currentPosition.timestamp`回调（如果提供）会在位置更改时自动执行。没有 watchId 被返回以及平台只允许一个`watchPosition`

**清晰的手表**

签名：`() -> Promise`

与原始浏览器 API 几乎相似，除了您不必传递 watchId。如果手表处于活动状态，则必须在开始新手表之前将其清除。

#### [模式](https://docs.appsmith.com/reference/appsmith-framework/context-object#mode) <a href="#mode" id="mode"></a>

该字段是一个枚举，其中包含应用程序当前是在查看模式还是编辑模式下运行。它采用值 VIEW|EDIT
