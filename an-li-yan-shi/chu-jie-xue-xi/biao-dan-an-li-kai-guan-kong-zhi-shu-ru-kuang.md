# 表单案例—开关控制输入框

PagePlug支持多样的能力开发，满足研发的使用需求。例如我们在表单或者系统中，需要通过开关按钮去控制是否能输入或者是选择，本次案例将展示开关按钮对输入框的控制

<figure><img src="../../.gitbook/assets/2023-04-28 173720 (1).gif" alt=""><figcaption></figcaption></figure>

### 1、案例示范

本次案例用到<mark style="color:red;">**开关按钮组件**</mark>和<mark style="color:red;">**输入框组件**</mark>

<figure><img src="../../.gitbook/assets/image (183).png" alt=""><figcaption></figcaption></figure>

* 我们可以先对输入框的文本进行修改，本次案例填写的是【是否填写】，也可以对文本和开关的位置进行调整

<figure><img src="../../.gitbook/assets/image (195).png" alt=""><figcaption></figcaption></figure>

* 之后我们可以调整下输入框的文本内容，例如案例的展示【家属信息】、【联系方式】、【家庭地址】，可以增添其他功能，例如校验等

<figure><img src="../../.gitbook/assets/image (194).png" alt=""><figcaption></figcaption></figure>

* 开关（Switch）组件自带有三个属性变量isDisabled，isSwitchedOn，isVisible，我们使用isSwitchedON

<figure><img src="../../.gitbook/assets/image (179).png" alt=""><figcaption></figcaption></figure>

可以将下列内容复制到输入框的禁用功能中

```
{{Switch1.isSwitchedOn}}
```

<figure><img src="../../.gitbook/assets/image (173).png" alt=""><figcaption></figcaption></figure>

* 另外的2个输入组件也是这样添加，就实现开关按钮控制输入框的输入

<figure><img src="../../.gitbook/assets/2023-04-28 173720.gif" alt=""><figcaption></figcaption></figure>

### 2、技巧延伸

我们可以把相关的组件，快速封装成一个模块，更方便界面的展示及使用。例如，我们框选我们所需要的组件，之后选择组合

<figure><img src="../../.gitbook/assets/2023-04-28 181010.gif" alt=""><figcaption></figcaption></figure>



