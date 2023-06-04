---
description: storeValue()函数将数据保存在浏览器中作为键值对，浏览器的localstorage里可以访问到，以后可以在应用程序中的任何地方访问。
---

# 全局数据的管理(storeValue/removeValue/clearstore)的使用

## 1、格式

* **存储数据**

```javascript
storeValue(key: string, value: any, persist? = true)
```

如果希望存储输入框组件的文本，可以使用storeValue()

```javascript
{{storeValue('email',input1.text)}}
```

* **读取数据**

可以通过引用存储对象中的键来访问存储中的值。

```javascript
{{ global.store.key }}
```

比如，存储了 input1.text 的值。可以通过引用键 emai l在应用程序中的任何位置访问此值

```javascript
{{global.store.email}}
```

* **修改数据**

可以通过使用其键覆盖数据来更新存储中保存的值。

比如，可以使用键isActive将布尔值从True更新为False，如下所示

```javascript
export default {
    updateStore: () => {
        if(global.store.isActive === true)
            storeValue("isActive", false) 
    }
}
```

如果需要存储许多值，而不是多次调用storeValue函数，建议使用对象形式来存储值。所有的值都可以在一个storeValue()函数中分配，如下所示

```javascript
storeValue("user", { "name": "Bar Crouch", "email": "bar@appsmith.com", "pin": "9984"}) 
```

* **清除数据**

removeValue()函数清除存储库中指定键的值。

```javascript
{{Value(key)}}
```

参考下面的代码，使用JSObject删除键为isActive的值

```javascript
export default {
    deleteStore: () => {
        // Delete value for a particular key
        removeValue("isActive")
            }
}
```

* **清空数据**

clearStore()函数清除应用中所有数据。

```javascript
{{clearStore()}}
```



## **2、PagePlug内对应的动作事件**

<figure><img src="../../.gitbook/assets/image (95) (2).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (137).png" alt=""><figcaption><p>storeValue—存储数据</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (14) (1).png" alt=""><figcaption><p>removeValue—修改数据</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (18) (1) (1).png" alt=""><figcaption><p>ClearStore—清除数据</p></figcaption></figure>

## **3、异步的storeValue**

storeValue是异步的，要保证你想在它执行之后再执行某些操作，必须使用async/await来控制执行

举个例子，假设有一个JS函数调用返回唯一标识符的API，并且您希望使用storeValue()保存返回的值。

```javascript
export default {
    getUniqueValue: () => {
        GetUniqueNameAPI.run()
        storeValue("uniqueEmail", GetUniqueNameAPI.data.uniqueName);
        showAlert("Success! Store value set: " + global.store.uniqueEmail);
    }
}
```

当您运行该函数时，您期望收到一条成功警报消息，其值存储在键uniqueEmail中，但它显示未定义。由于storeValue()是异步的，它可能在API调用正在进行时执行，并且值没有保存在存储中，从而导致未定义的值。

为了处理这种情况，您可以使用async/await，以确保StoreValue()函数等待API调用以完成执行。示例：修改代码以使用async/await，如下所示：

```javascript
export default {
     getUniqueValue: async () => {
         await GetUniqueNameAPI.run()
         await storeValue("uniqueEmail", GetUniqueNameAPI.data.uniqueName);
         showAlert("Success, Store value set: " + appsmith.store.uniqueEmail);
    }
}
```

getUniqueValue函数调用GetUniqueNameAPI.run()从API获取数据;

GetUniqueNameAPI调用的前缀await确保等待API执行完成，然后移动到下一行;

storeValue()的前缀await确保在下一行执行showAlert之前将给定键的值添加到存储中。



## **4、案例**

### **案例一：将input组件的内容存起来**

1.1 在input的**onTextChanged**事件里选择**保存数据（**其他事件同理哦**）**

<figure><img src="../../.gitbook/assets/image (25) (1).png" alt=""><figcaption></figcaption></figure>

1.2 假如键名input，键值用**\{{input1.text\}}**

<figure><img src="../../.gitbook/assets/image (20) (1).png" alt=""><figcaption></figcaption></figure>

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

<figure><img src="../../.gitbook/assets/image (32) (1).png" alt=""><figcaption></figcaption></figure>

点击保存数据，可以在localstorage里看到已保存

<figure><img src="../../.gitbook/assets/image (107) (2).png" alt=""><figcaption></figcaption></figure>
