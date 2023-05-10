---
description: storeValue()函数将数据保存在浏览器中作为键值对，浏览器的localstorage里可以访问到，以后可以在应用程序中的任何地方访问。
---

# 存储/修改/清除数据(storeValue/removeValue/clearstore)的使用

## 1、格式

* 存储数据

```javascript
storeValue(key: string, value: any, persist? = true)
```

* 修改数据

```
```

* 清除数据

```javascript
```

## 2、参数

* **key：key的名称**
* **value：您想保存的数据**

## **3、PagePlug内的动作事件**

<figure><img src="../../.gitbook/assets/image (95) (2).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (137).png" alt=""><figcaption><p>storeValue—存储数据</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (14) (1).png" alt=""><figcaption><p>removeValue—修改数据</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (18).png" alt=""><figcaption><p>ClearStore—清除数据</p></figcaption></figure>

## **4、案例**

### **案例一：将input组件的内容存起来**

1.1 在input的**onTextChanged**事件里选择**保存数据（**其他事件同理哦**）**

<figure><img src="../../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

1.2 假如键名input，键值用**\{{input1.text\}}**

<figure><img src="../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

1.3 当我在input输入内容时，触发了它的**onTextChanged**事件，**input1.text**会被存储在**localstorage**中

在浏览器的localstorage中可查

<figure><img src="../../.gitbook/assets/image (94) (2).png" alt=""><figcaption></figcaption></figure>

> 如何获取它?

```
{{global.store.input}}
```

<figure><img src="../../.gitbook/assets/image (98).png" alt=""><figcaption></figcaption></figure>

### 案例二：使用JSObject中的函数存储员某些需要全局的共享数据

1.创建个JS对象JSObject1, 使用以下代码

```javascript
export default {
    writeToStore: () => {
        storeValue("isActive", true). // Boolean
        storeValue("name", "Robert") // String 
        storeValue("pin", 9929) // Number
}

```

在按钮的onClick事件中选执行JS函数-->JSobject1-->writeToStore

<figure><img src="../../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

点击保存数据，可以在localstorage里看到已保存

<figure><img src="../../.gitbook/assets/image (107) (2).png" alt=""><figcaption></figcaption></figure>
