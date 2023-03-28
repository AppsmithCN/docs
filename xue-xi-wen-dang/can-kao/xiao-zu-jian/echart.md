# echart



{% hint style="info" %}
若没有及时回复，欢迎来gitee: [https://gitee.com/cloudtogo/pageplug/issues](https://gitee.com/cloudtogo/pageplug/issues) 和 github: [https://github.com/cloudtogo/pageplug/issues](https://github.com/cloudtogo/pageplug/issues)

提issue，记得描述清楚使用版本，组件及背景，方便成员复现
{% endhint %}

#### 1. 自定义图表报错

自定义图表的数据，解析到key没有双引号，如果您是直接从echart官网复制过来的，请在外面包裹一层`{{}}`

#### 2. 该怎么调用echart实例的方法？

提供了callFunc 方法，调用echart实例的方法

```javascript
// widgetName组件名称，funcName调用方法名称， option参数（可选）
callFunc(widgetName:string, funcName:string, option?:any) => Promise()
```

![](../../../.gitbook/assets/image.png)

```javascript
global.echartInstance
.callFunc("Echarts1", "getHeight")
.then(res => {
   console.log(res);
 })
```

#### 3.支持其他的监听事件吗？

支持自定义添加监听事件

```javascript
{{
     (data) => {
     console.log("回调数据", data)
     }
}}
```

下图示范调用: 点击图表是调用 实例的 getHeight方法&#x20;

![](<../../../.gitbook/assets/image (19).png>)

