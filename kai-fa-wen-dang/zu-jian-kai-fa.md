# 组件开发

{% hint style="info" %}
文档源自PagePlug社区8群的茂行整理
{% endhint %}



## 1、在 PagePlug 中配置组件

* 开发人员在构建 PagePlug 应用程序时可以配置组件属性 和 事件处理程序。
* 组件 开发人员可以决定向 PagePlug 平台暴露属性和事件

### 1.1 组件属性

这些是定义 组件 状态的值。如果PagePlug 开发人员希望使用来自其他实体的数据更新 组件的状态，则他们需要 bind其他实体作为 组件的属性。

例如，Text 组件有一个属性text。这定义了Text Widget 中显示的文本。如果 PagePlug 开发人员希望 Input widget 的值显示在Text组件中，则 Input widget 的文本属性必须与Text组件的text属性绑定在一起。

```
{{ Input1.text }}
```

这里，Input1是 Input 组件 的名称。text是 Input 组件的属性，它包含我们想要在 Text 组件中显示的值。平台会<mark style="color:red;">**evaluate \{{ \}}**</mark>括号内的内容。这意味着如果我们想要操作实体属性，我们可以在\{{ \}}其中编写 JS 代码。

例如：

```
{{ Input1.text.toLowerCase() }} 
```



### 1.2 组件动作触发器

{% hint style="info" %}
许多 组件 是交互式的。这些 组件 交互可用于触发 Web 应用中的工作流。这就是静态网页与 Web 应用的区别。
{% endhint %}

例如，Button 组件具有点击交互。因此，onClick操作触发器被暴露出来，其处理程序可以由PagePlug 开发人员配置。

例如，假设我们想在单击按钮小部件时显示一条消息。我们可以这样配置它：

```
{{ showAlert("My message", "info") }}
```

这里，**`showAlert`**是 PagePlug 平台提供的一个[操作方法](../xue-xi-wen-dang/pageplug-fang-fa/)。**`“My message”`**，是将显示在警报中的字符串。**`“info”`**是一个showAlert特定的参数，它描述了消息的类型。

我们也可以，将实体属性绑定到 showAlert里。例如：

```
{{ showAlert(Text1.text, "info") }}
```

在这里，Text1.text是名为 Text1 组件的 text 属性。我们这里也可以使用JS。

```
{{ showAlert(Text1.text.toLowerCase(), "info") }}
```



## 2、组件开发流程



### 2.1 组件文件夹结构

<figure><img src="../.gitbook/assets/image (6) (6).png" alt=""><figcaption></figcaption></figure>

* index.ts: 该文件包含组件的配置。
* constants.tsx: 该文件包含将组件及其组件中使用的常量。
* icon.svg: 这是代表组件的图标的 SVG 文件。
* widget/index.tsx: 这包含组件代码，它利用组件开发 API 并让PagePlug平台知道如何呈现组件。
* component/index.tsx: 这包含在主画布上呈现的核心组件。

**画布：**画布是 PagePlug 平台中的一种特殊类型的组件，PagePlug开发人员可以在其中放置widget。例如，一个 Container组件 包含一个 Canvas 组件，这允许我们将其他 widget 放置在一个容器 widget 中。

我们可以使用下面的CLI 命令生成Widget文件夹结构：

```
cd app/client && yarn generate:widget
```



### 2.2 组件注册

一个组件要在 PagePlug 应用程序展示出来，首先要在 PagePlug 平台上进行注册。

这是通过 [registerWidget ](https://github.com/cloudtogo/pageplug/blob/open-v1.8/app/client/src/utils/WidgetRegistry.tsx)函数来实现的。

```
registerWidget(Widget, config)
// Widget: 扩展的类BaseWidget
// config: 小部件配置（CONFIG如下所述）

```

### 2.3组件配置index.ts

这会将组件配置导出为通常名为 的对象CONFIG。默认导出必须是组件本身。此处显示了一个示例:

<figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

**配置选项**

* type（必填）：Widget.getWidgetType()，Widget默认从widget/index.tsx导入 ；
* name（必需）：此小部件的显示名称。这可以包含空格；
* iconSVG（必填）：IconSVG，IconSVG从./icon.svg导入；
* needsMeta（可选）：true，如果此小部件存储临时值。例如，用户输入值或状态。
* isCanvas（可选）：true，如果此小部件本身包含一个 Canvas，则允许将小部件放置在其中。
* properties（必需的）：

```
derived: Widget.getDerivedPropertiesMap(),
default: Widget.getDefaultPropertiesMap(),
meta: Widget.getMetaPropertiesMap(),
config: Widget.getPropertyPaneConfig(),
```

* defaults（必需）：Widget的默认属性。该平台提供了通用配置：

\- rows（必填）：放置在画布上时此Widget默认占用的行数。

\- columns（必填）：放置在画布上时此Widget默认占用的列数。

\- widgetName（必需）：自动生成的Widget名称前缀，用于此类Widget。这不能有空格或特殊字符。

\- version（必需）：此类Widget的版本号。

\-  blueprint（可选）：Widget的[蓝图](https://github.com/cloudtogo/pageplug/blob/open-v1.8/contributions/AppsmithWidgetDevelopmentGuide.md)。

\- enhancements（可选）：可以应用于Widget的增强功能[。](https://github.com/appsmithorg/appsmith/blob/release/contributions/AppsmithWidgetDevelopmentGuide.md#widget-enhancements)

{% hint style="info" %}
要考虑的要点：
{% endhint %}

* 所有配置都会影响 组件的行为方式。错误配置会导致错误。
* PagePlug平台提供了一些常量和类型。这些可以从src/widgets/constants.[ 查看更多](https://github.com/cloudtogo/pageplug/blob/open-v1.8/app/client/src/widgets/constants.ts)
* blueprint 和 enhancements是可用于创建复杂组件的强大功能。

### 2.4 Widget

组件代码必须在widget文件夹中全部可用。

```
class RadioButtonWidgetWidget extends BaseWidget<RadioButtonWidgetWidgetProps, WidgetState> {
  static getPropertyPaneContentConfig() {
    return [];
  }

  static getPropertyPaneStyleConfig() {
    return [];
  }

  static getDerivedPropertiesMap(): DerivedPropertiesMap {
    return {};
  }

  static getDefaultPropertiesMap(): Record<string, string> {
    return {};
  }

  static getMetaPropertiesMap(): Record<string, any> {
    return {};
  }

  getPageView() {
    return <RadioButtonWidgetComponent />;
  }

  static getWidgetType(): string {
    return "RADIOBUTTONWIDGET_WIDGET";
  }
}

export default RadioButtonWidgetWidget;
```



#### 静态方法：

* getPropertyPaneConfig （必需），返回[窗格属性](zu-jian-kai-fa.md#2.8-shu-xing-chuang-ge-pei-zhi)配置
* getDerivedPropertiesMap （可选，[DerivedPropertiesMap](zu-jian-kai-fa.md#2.5-pai-sheng-shu-xing-pei-zhi)）：返回可以从其他属性派生的属性映射。
* getDefaultPropertiesMap（可选，对象）：返回默认情况下采用[默认属性值](zu-jian-kai-fa.md#2.6-mo-ren-shu-xing-pei-zhi)的属性列表
* getMetaPropertiesMap（可选，对象）：返回将被视为和存储为[元属性](zu-jian-kai-fa.md#2.7-yuan-shu-xing-pei-zhi)的属性。
* getWidgetType（必需，字符串）：返回小部件的唯一类型。

#### 继承方法：

* executeAction(void): 执行一个动作。通常，用于调用配置的操作触发器。参数：
  * triggerPayload[ ExecuteTriggerPayload ](https://github.com/cloudtogo/pageplug/blob/open-v1.8/app/client/src/constants/AppsmithActionConstants/ActionConstants.tsx)注意：undefined或者null动作会抛出错误。
* disableDrag(void)：防止小部件在画布中被拖动。例如，当使用标题拖动对列重新排序时，表格小部件会禁用小部件拖动。这允许小部件在不与平台功能冲突的情况下实现功能。
  * disable 当参数为true时禁用拖动，当 false 时启用。
* updateWidgetProperty(void)：更新单个小部件属性
  * propertyPath: 要更新的属性的路径
  * propertyValue：要设置的值
* deleteWidgetProperty(void): 删除特定的小部件属性
* batchUpdateProperty(void)：批量更新属性。参数：
  * updates: 参数类型BatchUpdatePropertyPayload
  * shouldReplay(boolean): 如果为false, 则无法通过undo(cmd+z 或ctrl+z )命令返回原来的状态。默认为true。
* resetChildMetaProperty(void)：重置此小部件的子项的所有元属性。参数：
  * widgetId： 当前的widgetId
* updateWidgetMetaProperty(void)：与 <mark style="color:red;">updateWidgetProperty</mark> 不同，这些更新不会在刷新后保留。元属性是瞬态属性，通常是用户输入。参数：
  * propertyPath（任何，必需）：要更新的属性路径
  * propertyValue(any, required): 属性的value。
  * actionExecution（[DebouncedExecuteActionPayload](https://github.com/cloudtogo/pageplug/blob/open-v1.8/app/client/src/widgets/MetaHOC.tsx)，可选）：如果有与属性更新一起执行的操作，
* getPageView (ReactNode, required ): React.render 的加强版。这应该返回需要在画布上呈现的 React 组件。

### 2.5 派生属性配置

派生属性是从widget的其他属性计算而来的。

例如，富文本编辑器widget的 <mark style="color:red;">isValid</mark>属性 可以使用<mark style="color:red;">isRequired</mark>和<mark style="color:red;">text</mark>属性计算得到。如果widget被配置必填，但是文本为空，则该小部件的文本应该是无效的。一个简单的 JS 条件语句可以帮助我们为<mark style="color:red;">isValid</mark>属性赋值。

```
{{ this.isRequired ? this.text && this.text.length : true }}
```

在此示例中，我们从两个（ isRequired、text）现有属性派生了一个新属性。

注意：<mark style="color:red;">this</mark>关键字是小部件的上下文。在这里，指代富文本编辑器widget。

使用所描述的机制，<mark style="color:red;">getDerivedPropertiesMap</mark>应该返回一个对象，其中键是派生属性名称，值是带有 JS 绑定的字符串以计算派生属性值。

### 2.6 默认属性配置

默认属性是定义其他属性的默认值（在属性窗格中配置）的映射。

例如，在 Rich Text Editor Widget 中，该text属性包含用户输入的内容。但是，它也可以配置为窗体属性的默认起始值​​。在窗格属性中配置的属性称为defaultText。通过使用getDefaultPropertiesMapAPI，小部件开发人员可以定义如何text获取其默认值。

```
static getDefaultPropertiesMap(): Record<string, string> {
    return {
      text: "defaultText",
    };
  }
  
```

注意：当defaultText提供新值时，它将覆盖该text值。

### 2.7 元属性配置

元属性是其值是暂时的并且不会在应用程序中持久存在的属性。例如，富文本编辑器小部件中用户提供的内容（text属性）不会持久化。但是，此内容存储在内存中，可以在绑定中使用。我们可以使用 getMetaPropertiesMap 配置这些。

```
 static getMetaPropertiesMap(): Record<string, any> {
    return {
      text: undefined,
    };
  }

```

注意：如果此属性也用于其他 API（例如getDerivedPropertiesMap），那么value必须为 undefined。



### 2.8 属性窗格配置

属性窗格配置 定义属性控件的顺序、属性控件的验证、分组和类型等。类型是\`[数组](https://github.com/cloudtogo/pageplug/blob/open-v1.8/app/client/src/constants/PropertyControlConstants.tsx)\`\`。

<figure><img src="../.gitbook/assets/image (33) (1).png" alt=""><figcaption></figcaption></figure>

**PropertyPaneSectionConfig**

该对象定义属性窗体中的部分。

* sectionName（必需，字符串）：区段的显示名称
* children（必需，PropertyPaneConfig\[]）：通常是要在此部分中显示的属性控件列表。请参阅下方PropertyPaneControlConfig
* hidden（可选，布尔值）：函数，定义此部分是否隐藏。参数： - props：当前小部件属性
* propertyPath：相对于此区段的小部件的路径。如果不在面板中，这通常是小部件本身。

**PropertyPaneControlConfig**

该对象定义属性控件的配置

* label（必需，字符串）：显示给 PagePlug 开发人员的属性名称 - propertyName（必需，字符串）：与值关联的属性键。
* helpText（可选，字符串）：帮助 PagePlug 开发人员更好地理解属性的描述。将鼠标悬停在标签上时显示在工具提示中。
* isJSconvertible（可选，布尔值）：是否允许 PagePlug 开发人员使用 JS 按钮允许绑定此属性。
* controlType（必需，[ControlType](https://github.com/cloudtogo/pageplug/blob/open-v1.8/app/client/src/components/propertyControls/index.ts)）：控件的类型。
* panelConfig: (optional, [PanelConfig](zu-jian-kai-fa.md#2.9-mian-ban-pei-zhi) : 此属性是否打开面板？如果是，则必须在此处定义面板配置。
* isBindProperty（必需，布尔值）：此属性的值是否可以由 PagePlug 开发人员使用绑定来定义
* isTriggerProperty（必需，布尔值）：true ,如果这是一个可以触发操作的事件处理程序
* updateHook: （可选，Array<{propertyPath: string; propertyValue: any}> | undefined）

此函数用于定义更新此属性时，需要更新的其他属性。此函数在存储和评估新属性值之前执行。从此函数返回的所有属性更新将与原始属性更新同时应用。

参数

* props（任何）：小部件的属性。
* propertyName（字符串）：小部件属性的路径
* propertyValue（任意）：PagePlug 开发人员尝试应用的属性的新值。- 返回值应该是对象数组或undefined. 对象的键描述在下面。

返回

* 类型：Array<{propertyPath: string; propertyValue: any}> | undefined
* propertyPath: 需要更新的属性的路径
* propertyValue：需要更新的属性值。
* hidden （可选, 返回boolean值）：如果应隐藏此属性，则该函数应该返回 true。

参数：

* props：当前小部件属性
* propertyPath：相对于此属性的小部件的路径。
* additionalAutoComplete（可选，嵌套对象）：一个函数，返回此属性中自动完成的附加条目。

参数：

* props：当前小部件属性

返回：

* 类型：Record>
* 这将返回一个以关键字作为键的对象和一个作为值的对象，其键将用于自动完成。

其他：

* dependencies（对于updateHookand , string\[] 是必需的）：这列出了在and函数hidden中进行计算所需的属性路径。这是一种优化，允许将一小部分小部件属性用于计算。hiddenupdateHook
* validation（必需，[ValidationConfig](https://github.com/appsmithorg/appsmith/blob/release/contributions/AppsmithWidgetDevelopmentGuide.md#property-validation-configuration)）：定义如何验证此属性的配置。
* customJSControl（可选，ControlType）：如果我们有一个特殊的控件，我们想显示它来代替标准INPUT控件。

### 2.9 面板配置

此配置有助于定义面板中显示的属性的详细信息。

* editableTitle（必需，布尔值）：它定义面板的标题是否可编辑。
* titlePropertyName（必需，字符串）：它定义面板内属性的根路径。
* children（必需，[PropertyPaneConfig\[\]](https://github.com/appsmithorg/appsmith/blob/release/contributions/AppsmithWidgetDevelopmentGuide.md#property-pane-configuration)）：它配置面板中显示的部分和控件。
* \[updateHook]\(#propertypanecontrolconfig) [例子](https://github.com/appsmithorg/appsmith/blob/e772fd4ff96accfb94818fa9f0b58dc6851a1cf0/app/client/src/widgets/TableWidget/widget/propertyConfig.ts#L305)

### 2.10 属性验证配置

当允许 PagePlug 开发人员使用绑定时，可能需要验证属性。它有助于维护小部件的完整性。当提供验证时，小部件开发人员可以期望经过验证的属性。

* type（必需，[ValidationTypes](https://github.com/appsmithorg/appsmith/blob/e772fd4ff96accfb94818fa9f0b58dc6851a1cf0/app/client/src/constants/WidgetValidation.ts#L5)）：要执行的验证类型。
* params（某些验证类型需要[ValidationConfigParams](https://github.com/appsmithorg/appsmith/blob/e772fd4ff96accfb94818fa9f0b58dc6851a1cf0/app/client/src/constants/PropertyControlConstants.tsx#L67)）：提供的参数用于帮助验证。
  * \-min（可选，数字）：用于指定最小值 ValidationTypes.NUMBER
  * max（可选，数字）：用于指定最大值 alidationTypes.NUMBER
  * natural（可选，数字）：用于将数字验证为自然数。搭配使用 ValidationTypes.NUMBER
  * default（可选，未知）：用于为无效值或属性值提供默认值undefined。
  * unique（可选，boolean | string\[]）：用于指定属性中需要唯一的路径。请参见[示例](https://github.com/appsmithorg/appsmith/blob/e772fd4ff96accfb94818fa9f0b58dc6851a1cf0/app/client/src/widgets/DropdownWidget/widget/index.tsx#L44)。
  * required（可选，布尔值）：指定此属性的值是否是小部件正常运行所必需的。
  * regex（可选，RegExp）：匹配文本值的正则表达式ValidationTypes.TEXT
  * allowedKeys(optional, Array>): 中允许键的配置数组ValidationTypes.OBJECT。
    * name（必填，字符串）：密钥的名称
    * type(required, ValidationTypes): 这个键值的验证类型
    * params（可选，ValidationConfigParams）：提供的参数用于帮助验证
* allowedValues (optional, unknown\[]): 包含允许值集的数组ValidationTypes.ARRAY
* children（可选，ValidationConfig）：条目的验证配置ValidationTypes.OBJECT\_ARRAY
* fn（可选，(value: unknown, props: any, \_?: any, moment?: any) => ValidationResponse）：用于验证的函数ValidationTypes.FUNCTION
  * 参数
    * value（未知）：要验证的属性的当前值
    * props(any): 当前widget的属性
    * \_: [lodash](https://lodash.com/docs/4.17.15)库实用程序
    * moment: [momentjs](https://momentjs.com/docs/#/use-it/)库实用程序
  * 返回值
    * ValidationResponse：PagePlug 平台用来理解验证结果的特定格式。
      * isValid（必需，布尔值）：指定属性值是否有效
      * parsed（必填，未知）：验证后的值。这可以是默认值或原始值或原始值的格式化版本。
      * messages（可选，字符串\[]）：一组消息，用于描述验证失败的原因。这有助于 PagePlug 开发人员识别和修复属性配置中的问题
* expected（对于ValidationTypes.FUNCTION, [CodeEditorExpected](https://github.com/appsmithorg/appsmith/blob/e772fd4ff96accfb94818fa9f0b58dc6851a1cf0/app/client/src/components/editorComponents/CodeEditor/index.tsx#L107)是必需的）：描述预期类型、示例和自动完成数据类型的结构。
  * type（必需，字符串）：要向 PagePlug 开发人员显示的属性类型
  * example（必需，[ExpectedValueExample](https://github.com/appsmithorg/appsmith/blob/e772fd4ff96accfb94818fa9f0b58dc6851a1cf0/app/client/src/utils/validation/common.ts#L16)）：属性预期值的示例。
  * autocompleteDataType（必需，[AutocompleteDataType](https://github.com/appsmithorg/appsmith/blob/e772fd4ff96accfb94818fa9f0b58dc6851a1cf0/app/client/src/utils/autocomplete/CodemirrorTernService.ts#L64)）：描述此属性的自动完成功能应如何工作。
* strict（可选，布尔值）：如果设置为，则在验证之前不会将 , 中的true值转换为字符串。ValidationTypes.TEXT
* ignoreCase（可选，布尔值）：如果设置为true，则将匹配键，同时allowedKeys忽略ValidationTypes.OBJECT
* validationTypes.FUNCTION应谨慎使用，并在另一个ValidationTypes不符合验证要求时用作逃生舱口。&#x20;
* 所有验证都返回一个ValidationResponse。



### 2.11 组件蓝图

组件蓝图是一种配置，可以让组件开发人员描述组件的子结构及其属性的任何修改。这个结构将与 PagePlug 开发人员放置在画布上的此类小部件一起应用。

例如，默认情况下，表单widget包含一个画布，其中有一个文本小部件和按钮小部件。参考表单组件的[ 配置细节](https://github.com/cloudtogo/pageplug/blob/open-v1.8/app/client/src/widgets/FormWidget/index.ts)。

{% hint style="info" %}
组件蓝图配置包含两个部分。view和operations。
{% endhint %}

#### view

view: (optional, Array<{ type, size, position, props }>) 这描述了 children 和他们的结构

* type（ 必填，WidgetType）：子部件的类型。
* size ( required,  { rows: number, cols: number }): 子控件要占用的行数和列数。
* position (required,  { top: number, left: number }): 子控件的行（上）列（左）偏移量
* props（可选，Record）：默认应用于子部件的属性列表。

{% hint style="info" %}
注意：如果子部件需要同时创建属于自己的子部件，那么同样需要在props提供 blueprint属性作为自己的子部件的蓝图。
{% endhint %}

{% hint style="info" %}
注意：如前所述，只有 type 为CANVAS\_WIDGET的小部件才可以有children。因此，在大多数情况下，蓝图的配置会以 CANVAS\_WIDGET 开头，其他嵌套的子项将在CANVAS\_WIDGET的 prop中进行配置。[请参考Form Widget 示例](https://github.com/cloudtogo/pageplug/blob/open-v1.8/app/client/src/widgets/FormWidget/index.ts)。
{% endhint %}

{% hint style="info" %}
注意：不需要定义 CANVAS\_WIDGET的 size属性 ，因为这种类型的小部件独立工作并占据父级的所有大小。因此，position的值也将是{top: 0, left:0}
{% endhint %}

#### operation

soperations: (optional, BlueprintOperation\[]) 在画布上显示widget 之前要执行的一组修改widget 属性的操作。

BlueprintOperation的类型：{ type: BlueprintOperationType, fn: BlueprintOperationFunction }

BlueprintOperationType：这些操作可以分为三种类型：

* 修改属性的操作 BlueprintOperationTypes.MODIFY\_PROPS
* 添加动作触发器处理程序的操作 BlueprintOperationTypes.ADD\_ACTION
* 将子控件 添加到当前widget时候，将要执行的操作。BlueprintOperationTypes.CHILD\_OPERATIONS

### 2.12 组件增强

**derived.js 和 parseDerivedProperties.ts**

* 一些小部件，如表格小部件，具有复杂的派生属性，因此为派生属性的函数使用单独的文件。[parseDerivedProperties.ts](https://github.com/cloudtogo/pageplug/blob/open-v1.8/app/client/src/widgets/ListWidget/widget/parseDerivedProperties.ts)

从关联的[derived.js](https://github.com/cloudtogo/pageplug/blob/open-v1.8/app/client/src/widgets/ListWidget/widget/derived.js)中加载函数用于以字符串的形式绑定派生属性。

**组件常量**

* 一些常量可通过 PagePlug 平台获得，供小部件开发人员在构建小部件时使用，这些小部件使用一些标准组件。[查看代码](https://github.com/cloudtogo/pageplug/blob/open-v1.8/app/client/src/components/constants.ts)

**独立组件常量**

* 与组件常量类似，组件常量是组件开发人员可以使用的独立常量集。
* [查看文档1](https://github.com/cloudtogo/pageplug/blob/open-v1.8/app/taro/src/constants/WidgetConstants.tsx)
* [查看文档2](https://github.com/cloudtogo/pageplug/blob/open-v1.8/app/client/src/widgets/constants.ts)

**组件工具**

* PagePlug 平台还提供实用功能来帮助开发小部件。[查看代码](https://github.com/cloudtogo/pageplug/blob/open-v1.8/app/client/src/widgets/WidgetUtils.ts)

**如何评估\{{\}}绑定原理？**

* 来自 Appsmith 团队的 Hetu 的一篇不错的[帖子](https://dev.to/appsmith/evaluating-js-in-the-browser-for-a-low-code-product-56ld)详细描述了评估逻辑。

**性能考虑**

* 创建小部件时，不鼓励使用componentDidMount和componentDidUpdate生命周期方法。其他方法getDerivedPropertiesMap可以帮助在渲染之前导出相关值。
* 在许多情况下，延迟加载小部件的组件是一个好主意，尤其是在使用新库创建此组件的情况下。

