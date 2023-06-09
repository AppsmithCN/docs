# 玩转表格（Table）组件

{% hint style="info" %}
&#x20;文档来源社区成员平头哥的编写，感谢社区成员平头哥的贡献
{% endhint %}

### 1、案例前提

看完这个案例，你可以学会：

* 数据源的使用（本次案例使用的是mysql为例）
* 表格数据的增加（行更新模式）
* 表格数据的修改（行更新模式）
* 表格数据的删除（行更新模式）
* 表格数据的查询（当然啦）
* 表格数据的分页（亮点🌟）



### 2、连接数据源

#### 2.1 新增数据源

在PagePlug中创建一个新的应用后，在左侧工具栏的数据源中选择新增，选择mysql

<figure><img src="https://picx.zhimg.com/80/v2-72bef3c97b73dc14d4dcfb1d93df6171_720w.png" alt=""><figcaption></figcaption></figure>



#### 2.2 填写数据源信息

* 分别填写Mysql数据源的主机、端口、数据库名、用户名和密码（本次案使用的是[methodot](http://methodot.com/)的云数据库）

<figure><img src="https://pic1.zhimg.com/80/v2-ffaf60847df6c10650a2790f156cbcf8_720w.png" alt=""><figcaption></figcaption></figure>

* sql文件可以点击下方自己上传

{% file src="../../.gitbook/assets/pageplug—社区8群平头哥.sql" %}

* 之后点击右下角的测试，测试无误后，点击保存

<figure><img src="https://picx.zhimg.com/80/v2-4cc826723ef9bb24cfd31ecac40b9843_720w.png" alt=""><figcaption></figcaption></figure>

### 3、表格数据的展示

#### 3.1 新增查询，编写查询语句

* 我们可以根据绑定的MySQl数据源，新增一个JS查询

<figure><img src="https://pic1.zhimg.com/80/v2-3b385e8d34c22814dfc38c55fcc38091_720w.png" alt=""><figcaption></figcaption></figure>

* 编写查询语句，并运行测试

```
SELECT * FROM user;
```

<figure><img src="https://picx.zhimg.com/80/v2-188440c6d7d02231d85a439034cce5b7_720w.png" alt=""><figcaption></figcaption></figure>

#### 3.2 使用表格组件

* 在左侧的菜单栏中，拖入一个表格组件

<figure><img src="https://pic1.zhimg.com/80/v2-4f6785d3904d4d00bb92834ac9f33757_720w.png" alt=""><figcaption></figcaption></figure>

* 并在右侧的数据栏中输入下列代码

```
{{ getAllUsers.data }}
```

<figure><img src="https://picx.zhimg.com/80/v2-f14596c16614b51eee9fe55723ab1136_720w.png" alt=""><figcaption></figcaption></figure>

#### 3.3 同步数据源与表格列名

* 分别检查每列的属性名与数据的属性名是否一致（一般当你替换数据时就自动同步了）

<figure><img src="https://picx.zhimg.com/80/v2-24669435d99df3a43e88eabef07403d4_720w.png" alt=""><figcaption></figcaption></figure>

<figure><img src="https://picx.zhimg.com/80/v2-ac9c40b095fb779ede9bd98c8f988cd1_720w.png" alt=""><figcaption></figcaption></figure>

<figure><img src="https://picx.zhimg.com/80/v2-e56a4185426f9d6b28d07e846a09fb9c_720w.png" alt=""><figcaption></figcaption></figure>

### 4、表格的数据新增

#### 4.1 新增查询，编写新增语句

<figure><img src="https://picx.zhimg.com/80/v2-3b385e8d34c22814dfc38c55fcc38091_720w.png" alt=""><figcaption></figcaption></figure>

输入下列代码

```
NSERT INTO user  (username, power)VALUES  (    {{ Table1.newRow.username || '' }},                {{ Table1.newRow.power || 0 }}  );
```

<figure><img src="https://picx.zhimg.com/80/v2-831c68607caff7fe04f9f7741f436480_720w.png" alt=""><figcaption></figcaption></figure>

#### 4.2 表格配置新增一行，保存事件绑定js函数

* 在表格配置中，打开“新增一行”

<figure><img src="https://pica.zhimg.com/80/v2-4ad333c932314e1d763cb60e4e177357_720w.png" alt=""><figcaption></figcaption></figure>

* 保存事件绑定js函数（记得提前新建个js对象哦）

<figure><img src="https://pic1.zhimg.com/80/v2-9a5693301aab31def71101c0f6ed3821_720w.png" alt=""><figcaption></figcaption></figure>

* pageHandler的addUser逻辑如下

```
addUser: () => {                //write code here                addUser.run().then(() => {                        showAlert('添加成功', 'success')                        getAllUsers.run()                }).catch(() => {                        showAlert('添加失败', 'error')                })                        }
```

<figure><img src="https://picx.zhimg.com/80/v2-85f0ca0915850a878f953138185ceb85_720w.png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
小Tips：

当你新增成功之后还要重新运行getAllUsers查询，刷新表格数据；当你想使用对表格数据进行增删改时，记得配置可以编辑，并选择行更新模式
{% endhint %}

<figure><img src="https://picx.zhimg.com/80/v2-639cbdbe97843760aef8440179319b90_720w.png" alt=""><figcaption></figcaption></figure>

#### 4.3 点击新增一行选项，进行测试

* 可以点击表格组件的【新增一行】

<figure><img src="https://pica.zhimg.com/80/v2-991ecc493f5f11b4a3c1a37342a7bce3_720w.png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
1、部分id自增，可以不用写&#x20;

2、例如填写用户名和潜力之后，可以点击保存按钮；&#x20;

3、成功时表格数据刷新，可以倒序查看新增数据；&#x20;

4、也可以放弃此次新增，点击【丢弃】按钮即可
{% endhint %}

<figure><img src="https://picx.zhimg.com/80/v2-a8ff5e2d0272c2fcd9acad9440d52595_720w.png" alt=""><figcaption></figcaption></figure>

### 5、表格数据的修改与删除

#### 5.1 新增查询，编写修改语句

<figure><img src="https://picx.zhimg.com/80/v2-3b385e8d34c22814dfc38c55fcc38091_720w.png" alt=""><figcaption></figcaption></figure>

编写修改语句的代码如下：

```
UPDATE user  SET username = {{ Table1.selectedRow.username  }}, power = {{ Table1.selectedRow.power }}  WHERE id = {{ Table1.selectedRow.id }};
```

<figure><img src="https://pic1.zhimg.com/80/v2-ecd2e7e9192ba423b3a4b86e223a8c84_720w.png" alt=""><figcaption></figcaption></figure>

* 在行更新操作列中配置保存和丢弃事件

<figure><img src="https://picx.zhimg.com/80/v2-ca1cc399a3b5d989d4adc22b7a41bd78_720w.png" alt=""><figcaption></figcaption></figure>

#### 5.2 配置保存和丢弃事件

* 在右侧的行更新中点击设置，我们在onSave中这样配置

<figure><img src="https://picx.zhimg.com/80/v2-3972edc7c68230a7aa3f2f597370fb4b_720w.png" alt=""><figcaption></figcaption></figure>

* pageHandler的updateUser逻辑如下，同理，修改之后重新请求数据，刷新表格

```
updateUser: () => {                updateUser.run().then(() => {                        showAlert('修改成功', 'success')                        getAllUsers.run()                }).catch(() => {                        showAlert('修改失败', 'error')                })        }
```

<figure><img src="https://picx.zhimg.com/80/v2-02bf38970c2382eca3041e3f94d84bea_720w.png" alt=""><figcaption></figcaption></figure>

#### 5.3 测试下

* 回到表格组件中，点击这个图标

<figure><img src="https://picx.zhimg.com/80/v2-23f80e99e9e852d47f5ed1f654ff60de_720w.png" alt=""><figcaption></figcaption></figure>

* 在输入框输入值了后，回车保存

<figure><img src="https://picx.zhimg.com/80/v2-4d51eb89a43596fa7b8a3f8204e08288_720w.png" alt=""><figcaption></figcaption></figure>

* 可以点击右侧的行更新操作，会发现数据表格刷新保存

<figure><img src="https://picx.zhimg.com/80/v2-92e47d42b3ffb165dfd0811a054d9afc_720w.png" alt=""><figcaption></figcaption></figure>

#### 5.4 删除同理，以下直接提供代码，可自行操作

* 丢弃事件绑定pageHandler的deleteUser

）

<figure><img src="https://picx.zhimg.com/80/v2-5330facc974fa8a0cb450aa7f8ec5883_720w.png" alt=""><figcaption></figcaption></figure>

​编辑切换为居中添加图片注释，不超过 140 字（可选）

* pageHandler的deleteUser逻辑如下

```
deleteUser: () => {                deleteUser.run().then(() => {                        showAlert('删除成功', 'success')                        getAllUsers.run()                }).catch(() => {                        showAlert('删除失败', 'error')                })        }
```

<figure><img src="https://picx.zhimg.com/80/v2-1299c930d8ade9df305482fd57431aa9_720w.png" alt=""><figcaption></figcaption></figure>

> 删除有点不够优雅，你得选中一行，然后编辑一下，才能点丢弃；
>
> 当然，你也可以另外使用一个按钮，绑定pageHandler的deleteUser哈，也欢迎有新的想法功能尝试

### 6、表格数据的份分页

重点重点，接下来说下有点复杂的分页，演示分页之前，先注意两个概念

* 当前页数（pageNo）
* 每页大小（pageSize）

#### 6.1 分享下PagePlug这里的分页逻辑

* 先看个简单的例子

```
SELECT * FROM orders LIMIT 10, 10;
```

上述查询中，LIMIT 10, 10 表示跳过前 10 条记录，然后返回接下来的 10 条记录，即第 11 到 20 条记录。 用我们的中文理解就是

```
SELECT * FROM orders LIMIT 跳过行数, 接下来行数
```

这是简单的分页查询语句。你可能会想，那我这样写：

```
SELECT * FROM user LIMIT {{ (Table1.pageNo - 1) * Table1.pageSize }}, {{ Table1.pageSize }};
```

当你想看某一页的数据时，取决于两个值，当前页数（pageNo），每页大小（pageSize），比如每页大小为4，你想看第4\~8条数据，你的当前页数（pageNo）为2，即第二页。那语句是:

```
SELECT * FROM user LIMIT ((2-1) *4), 4;
```

* 那pageNo为什么要减去1？

当你想看第一页时，其实就是：

```
SELECT * FROM user LIMIT ((0-1) *4), 4;
```

这里大家都会忽略了一个边界情况，现在假设数据总条数（getAllUsers.data.length）有16条，每页大小为7，那会分成3页：7 7 2，但是如果你使用：

```
SELECT * FROM user LIMIT {{ (Table1.pageNo - 1) * Table1.pageSize }}, {{ Table1.pageSize }};
```

当你在第2页，你想翻页时，也就是pageNo变成3时，他就是

```
SELECT * FROM user LIMIT 14, 7;
```

也就是想看14条后面的7条数据，但是后面并没有7条数据（只有2条），这样会报错！也就是说，我们需要做个判断:

{% hint style="info" %}
* 当pageSize >= 剩余条数 时（也就是刚刚的情况，pageSize为7，剩余条数为2），那LIMIT的第二个参数就是 剩余条数；
* 当pageSize < 剩余条数 时（比如pageSize为7，剩余条数为9），那LIMIT的第二个参数就是 pageSize；
{% endhint %}

总结一下，我们用个三元表达式判断，也就是：

```
SELECT * FROM user LIMIT 跳过行数, (pageSize >= (总数-跳过行数)) ? (总数-跳过行数) : pageSize ;
```

剩余行数 = 总数-跳过行数 所以，接下来写法你应该就更懂了，只是长而已，逻辑并不复杂\~

```
SELECT * FROM user LIMIT {{ (Table1.pageNo - 1) * Table1.pageSize }}, {{ Table1.pageSize >= (getAllUsers.data.length - ((Table1.pageNo - 1) * Table1.pageSize))  ?   getAllUsers.data.length - ((Table1.pageNo - 1) * Table1.pageSize) : Table1.pageSize }};
```

<mark style="color:red;">**当然，有问题欢迎继续在社区社群里面补充**</mark>

#### 6.2 查看分页查询

* 先新建个分页查询

<figure><img src="https://pic1.zhimg.com/80/v2-bbdec05dae78667aa8e785e7457f47e5_720w.png" alt=""><figcaption></figcaption></figure>

分页查询的代码如下：

```
SELECT * FROM user LIMIT {{ (Table1.pageNo - 1) * Table1.pageSize }}, {{ Table1.pageSize >= (getAllUsers.data.length - ((Table1.pageNo - 1) * Table1.pageSize))  ?   getAllUsers.data.length - ((Table1.pageNo - 1) * Table1.pageSize) : Table1.pageSize }};
```

#### 6.3 实战演示

{% hint style="info" %}
小tips：

* 表格数据用分页查询的数据
* 表格配置开启服务端分页
* 总行数使用数据总条数
* 翻页事件（onPageChange）和改变每页大小事件（onPageSizeChange）需要绑定js函数（执行getPagingData查询
{% endhint %}

<figure><img src="https://pic1.zhimg.com/80/v2-871eba292110cf24fdbfe7ba60e18e83_720w.png" alt=""><figcaption></figcaption></figure>

* 修改下表格数据

```
{{ getPagingData.data }}
```

<figure><img src="https://pica.zhimg.com/80/v2-6f636f36e5c0c3e9f43d571eefa1a6cc_720w.png" alt=""><figcaption></figcaption></figure>

<figure><img src="https://pic1.zhimg.com/80/v2-5d3072c040bf015b8aeb4e5877393141_720w.png" alt=""><figcaption></figcaption></figure>

* 当你对表格数据进行增删改时，都得执行getPagingData查询，刷新表格数据\~

<figure><img src="https://picx.zhimg.com/80/v2-97d69c78df808bd01c44db47564eb832_720w.png" alt=""><figcaption></figcaption></figure>

做完上述操作以后，当你拉动表格高度或者翻页时，你就会看到自己的杰作啦\~

PagePlug低代码里的表格组件你就玩转啦
