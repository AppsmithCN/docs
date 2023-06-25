---
description: 接下来演示如何连接mysql数据库并执行查询
---

# formily案例（登陆demo-mysql数据库）

## 1、demo收获（看完你就会）

* formily组件的简单使用
* 获取表单数据
* 连接mysql数据库
* mysql查询
* JS对象方法的调用

## 2、formily表单组件简单使用



<figure><img src="../../.gitbook/assets/image (10) (5).png" alt=""><figcaption><p>做一个登录demo</p></figcaption></figure>

### 2.1 设计表单

* 拉一个formily表单组件

<figure><img src="../../.gitbook/assets/image (3) (5).png" alt=""><figcaption></figcaption></figure>

* 选中它，在它右边点击**设计表单**

<figure><img src="../../.gitbook/assets/image (7) (4).png" alt=""><figcaption></figcaption></figure>

* 分别拖**输入框**和**密码框**进去

<figure><img src="../../.gitbook/assets/image (28) (3).png" alt=""><figcaption></figcaption></figure>

* 分别设置一下这两组件的**字段标识**、**标题**、**默认值**、**是否必填，**这里的字段标识很关键，设置成英文，后续获取该表单项的值时会用到

<figure><img src="../../.gitbook/assets/image (21) (1) (2).png" alt=""><figcaption></figcaption></figure>

* 配置好这两个组件后，点击保存

<figure><img src="../../.gitbook/assets/image (4) (1) (1).png" alt=""><figcaption></figcaption></figure>

然后你就可以看到

<figure><img src="../../.gitbook/assets/image (12) (1).png" alt=""><figcaption></figcaption></figure>

### 2.2获取表单数据

<figure><img src="../../.gitbook/assets/image (6) (5).png" alt=""><figcaption></figcaption></figure>

注意这个名字，我们可以通过 **formily1.formData.username** 获取到 用户名的值，密码同理，比如你给密码的字段标识是password，那么你就可以通过 **formily1.formData.password** 获取到密码的值

### 2.3连接mysql数据库

* 在**数据源**那点击 + ，然后选择**mysql**

<figure><img src="../../.gitbook/assets/image (26) (3) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
connect mode用默认的就行，可读可写
{% endhint %}

* 填写服务器主机，端口号、数据库名称、用户名、密码

其它选项暂时不用写

<figure><img src="../../.gitbook/assets/image (9) (1) (1) (2).png" alt=""><figcaption></figcaption></figure>

* 填完信息之后，点击**测试**，页面显示连接成功后，点击**保存**

<figure><img src="../../.gitbook/assets/image (5) (1) (1).png" alt=""><figcaption></figcaption></figure>

* 保存之后你可以看到

<figure><img src="../../.gitbook/assets/image (11) (2).png" alt=""><figcaption></figcaption></figure>

### 2.4 账号查询

* 选择表单后，在表单的提交事件上选择**执行查询**，当执行查询成功后，需要在查询的onSucces事件上绑定JS对象的函数，通知配置失败的**消息提示**

<figure><img src="../../.gitbook/assets/image (22) (1).png" alt=""><figcaption></figcaption></figure>

* **JS对象的代码如下**

{% hint style="info" %}
**js对象**中可以通过**Query1.data**去获取查询的结果
{% endhint %}

```javascript
export default {
	myFun1: () => {
		//write code here
		if(Query1.data.length > 0){
			showAlert('登陆成功', 'success')
    } else {
			showAlert('无此账户，请确认账户密码是否正确', 'error')
		}
	}
}
```

* 查询语句如下

```sql
SELECT * FROM admin WHERE username = {{formily1.formData.username}} AND password = {{formily1.formDaqa.password}}
```

<figure><img src="../../.gitbook/assets/image (13) (4).png" alt=""><figcaption></figcaption></figure>

这个开关要打开，打开可以使您的查询对SQL注入等不良事件具有弹性。但是，如果您的动态绑定包含任何SQL关键字，如“SELECT”，“WHERE”，“AND”等，则需要关闭。

* 点击提交，登陆成功（数据库有这个账户）

<figure><img src="../../.gitbook/assets/image (2) (3).png" alt=""><figcaption></figcaption></figure>
