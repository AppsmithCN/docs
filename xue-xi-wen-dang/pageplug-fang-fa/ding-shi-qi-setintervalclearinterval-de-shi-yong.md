---
description: 定时事件(JavaScript中的计时函数)允许用户定期运行API和DB查询。您可以使用setInterval和clearInterval函数来配置这些。
---

# 定时器(setInterval/clearInterval)的使用

## setInterval() <a href="#setinterval" id="setinterval"></a>

setInterval()在以固定的时间间隔执行回调函数。

### 1、格式

```javascript
setInterval(callbackFunction: Function, interval: number, id?: string, args?: any)
```

### 2、参数介绍

| 参数名                  | 描述                                   |
| -------------------- | ------------------------------------ |
| **callbackFunction** | 每隔特定时间间隔重复调用的函数。                     |
| **interval**         | 调用callbackFunction之间等待的毫秒数，也就是时间间隔。  |
| **id**               | 定时器的唯一标识，使用clearInterval清除定时器就是传这个id |

### 3、PagePlug内对应的动作事件

<figure><img src="../../.gitbook/assets/image (2) (1) (4).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (4) (1) (5).png" alt=""><figcaption></figcaption></figure>

### 4、案例

```javascript
setInterval(() => { Query1.run() }, 10000, "myTimer");j
```

这个定时器会每隔10秒执行Query1.run()

## 二、clearInterval() <a href="#clearinterval" id="clearinterval"></a>

该函数可以清除定时器，避免定时器占用内存。

### 1、格式

```javascript
clearInterval(id: string)
```

### 2、参数介绍

| 参数名    | 描述         |
| ------ | ---------- |
| **id** | 需要清除的定时器id |

### **3、**PagePlug内对应的动作事件

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (7) (1).png" alt=""><figcaption></figcaption></figure>

### 4、案例

```javascript
clearInterval("myTimer");
```
