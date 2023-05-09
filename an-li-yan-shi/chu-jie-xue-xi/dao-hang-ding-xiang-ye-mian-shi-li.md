# 导航定向页面示例

PagePlug支持多样的能力开发，满足研发的使用需求。例如我们会需要对系统进行很多的页面切换及展示，如果能通过一个导航功能，定向跳转到指定的页面，系统的功能又将会充满无限的可能。

### 1、仓存系统的页面导航

例如下面的，仓存管理系统除了能够完成数据的可视化展示外，我们也可以完成页面的切换，实现对应的增删改查功能

<figure><img src="../../.gitbook/assets/2023-04-22 171028.gif" alt=""><figcaption><p>组件跟</p></figcaption></figure>

### 2、案例示范：

* 需要用到的组件：按钮组和标签页组件

<figure><img src="../../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

* 1、把标签页的数据用global存起来，可以自定义一个activeTab变量

```
{{global.store.activeTab}}
```

<figure><img src="../../.gitbook/assets/image (141).png" alt=""><figcaption></figcaption></figure>

**2、在按钮组中，对按钮设置【保存数据】事件，以仓库按钮为例：**

* 进入按钮设置页面：

<figure><img src="../../.gitbook/assets/image (137) (2) (1).png" alt=""><figcaption></figcaption></figure>

* 在按钮设置中，事件选择【保存数据】

<figure><img src="../../.gitbook/assets/image (138) (2).png" alt=""><figcaption></figcaption></figure>

* 键输入上面填写的变量【activeTab】，值选择标签页的【名称】，例如仓库

<figure><img src="../../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>

这样设置，当你点击按钮的时候，就可以对标签页的页面进行切换，其他页面和按钮组件也是同样的设置

<figure><img src="../../.gitbook/assets/2023-04-22 184551.gif" alt=""><figcaption></figcaption></figure>

### 3、功能延伸

或者我们可以将按钮切换成【菜单按键】，或者使用【菜单按钮】

<figure><img src="../../.gitbook/assets/image (126) (2).png" alt=""><figcaption></figcaption></figure>

* 设置3个菜单选项，例如【仓库库存】、【供应商】、【产品】

<figure><img src="../../.gitbook/assets/image (121).png" alt=""><figcaption></figcaption></figure>

* 同样的，我们对菜单里的选项设置一个【保存数据】事件

<figure><img src="../../.gitbook/assets/image (116).png" alt=""><figcaption></figcaption></figure>

* 这样设置，当你点击菜单内的选项时，会联动页面的切换，其他选项也是如此

<figure><img src="../../.gitbook/assets/2023-04-23 101056.gif" alt=""><figcaption></figcaption></figure>

🤩除了应用系统、内部小工具这样的开发，网站页面的联动切换及跳转，事件设置中选择【跳转到】，可以指定跳转url或者是搭建的内部页面

<figure><img src="../../.gitbook/assets/image (84).png" alt=""><figcaption></figcaption></figure>

### 4、灵感工厂

不仅仅是按钮组，我们也可以通过下拉选项组件及任何组件来进行控制切换，社区的同学们自己拓展延伸下吧，期待你们的作品

<figure><img src="../../.gitbook/assets/321.gif" alt=""><figcaption></figcaption></figure>
