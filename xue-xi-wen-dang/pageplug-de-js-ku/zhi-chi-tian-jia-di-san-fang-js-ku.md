# 支持添加第三方JS库

PagePlug支持自定义 Javascript 库了！！！能为 PDF 生成、CSV 解析、分析、身份验证、错误记录等复杂用例提供了更高级的功能，还能支持您通过自定义库来操作或转换数据，这些外部库提供了额外的方法来帮助您构建复杂的应用程序和业务逻辑。

<figure><img src="../../.gitbook/assets/image (5) (2) (2).png" alt=""><figcaption></figcaption></figure>

### 1、库的兼容性

PagePlug 仅与支持 [**UMD**](https://github.com/umdjs/umd) 构建的库兼容。如果库支持 UMD 构建格式，则库索引文件的源代码应符合此 [基本模式](https://github.com/umdjs/umd/blob/master/templates/commonjsStrict.js)。`root`大多数兼容库的索引文件可以在, `/umd` 或 文件夹下找到 `/browser` ，并具有`.min.js`文件扩展名。如果您希望使用的库不支持 UMD 构建，您可以使用 [browserify](https://browserify.org/) 生成一个并将其托管在您选择的 CDN 中。

* 有效网址：

&#x20;`https://cdn.jsdelivr.net/npm/exceljs@4.3.0/dist/exceljs.min.js`

* 有效网址，但不支持的构建格式：&#x20;

`https://cdn.jsdelivr.net/npm/uuid@9.0.0/dist/index.js`

* &#x20;网址无效。不指向索引文件：

&#x20;`https://www.jsdelivr.com/package/npm/datejs`



### 2、安装外部JS库

PagePlug在安装JS库的时候，菜单栏会有一些推荐的库可供选择，您只需单击安装图标即可进行安装。但是，如果您想使用 URL 安装特定的库，过程也很简单。要安装其他库：

* [在jsDelivr](https://www.jsdelivr.com/) 或 [UNPKG](https://unpkg.com/)等流行的 CDN 服务上 查找[兼容的](https://docs.appsmith.com/core-concepts/writing-code/ext-libraries#library-compatibility)库。
* 将 URL 复制到其索引文件并将其粘贴到 PagePlug 上以开始安装。
* 导航到资源管理器选项卡
* 单击`+`旁边的标志`Libraries`。
* 将 URL 粘贴到指定字段中。例如：

```
https://cdn.jsdelivr.net/npm/exceljs@4.3.0/dist/exceljs.min.js
```

<figure><img src="../../.gitbook/assets/image (119).png" alt=""><figcaption></figcaption></figure>

* 之后点击安装

<figure><img src="../../.gitbook/assets/image (123).png" alt=""><figcaption></figcaption></figure>

### 3、案例演示

可以像在应用内通过`{{ }}`的方式使用 JavaScript 一样在内部使用外部库，提供一些示例：

<figure><img src="../../.gitbook/assets/image (132).png" alt=""><figcaption></figcaption></figure>

<pre class="language-javascript"><code class="lang-javascript">export default {
  myVar1: [],
  myVar2: {},
  myFun1 () {
		//	write code here
		//	this.myVar1 = [1,2,3]
	},
  createWorkbook: async () => {
    const workbook = new ExcelJS.Workbook();
<strong>    console.log(workbook, "66666")
</strong>    workbook.creator = "Tomato";
    workbook.lastModifiedBy = "Tomato";
    workbook.created = new Date();
    workbook.modified = new Date();
    workbook.calcProperties.fullCalcOnLoad = true;
  
    const worksheet = workbook.addWorksheet("Tomato page 1", {
      properties: { tabColor: { argb: "#FF0000" } },
      pageSetup: { paperSize: 9, orientation: "landscape" },
    });
  
    worksheet.getCell("A1").value = "Hello, World!";
    worksheet.getCell("B1").value = "What time is it?";javaja
    worksheet.getCell("A2").value = 7;
    worksheet.getCell("B2").value = "12pm";
  
    const buf = await workbook.xlsx.writeBuffer();
    const blob = new Blob([buf], {
      type: "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet",
    });
    const url = URL.createObjectURL(blob);
  
    await download(url, "test.xls");
  }
}
</code></pre>



### 4、注意事项

由于平台限制，您可能无法安装或使用某些库的方法：

* [DOM](https://developer.mozilla.org/en-US/docs/Web/API/Document\_Object\_Model/Introduction)访问：试图操纵文档对象的库将无法工作。示例： https: [//d3js.org/](https://d3js.org/)
* [XHR](https://developer.mozilla.org/en-US/docs/Glossary/XMLHttpRequest)：仅依赖 XHR 的库将无法工作。
* 其他 API：在后台使用以下 API 的库方法将不起作用：[setInterval](https://developer.mozilla.org/en-US/docs/Web/API/setInterval)、[clearInterval](https://developer.mozilla.org/en-US/docs/Web/API/clearInterval)、[setImmediate](https://developer.mozilla.org/en-US/docs/Web/API/Window/setImmediate)、[localStorage](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage)和[Navigator](https://developer.mozilla.org/en-US/docs/Web/API/Navigator)。
* [DOM](https://developer.mozilla.org/en-US/docs/Web/API/Document\_Object\_Model/Introduction)访问：试图操纵文档对象的库将无法工作。示例： https: [//d3js.org/](https://d3js.org/)
* [XHR](https://www.notion.so/Custom-JS-Libraries-82c03d95918b4eaa8f3e0dd811f3cd00)：仅依赖 XHR 的库将无法工作。
* 其他 API：在后台使用以下 API 的库方法将不起作用：[setInterval](https://developer.mozilla.org/en-US/docs/Web/API/setInterval)、[clearInterval](https://developer.mozilla.org/en-US/docs/Web/API/clearInterval)、[setImmediate](https://developer.mozilla.org/en-US/docs/Web/API/Window/setImmediate)、[localStorage](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage)和[Navigator](https://developer.mozilla.org/en-US/docs/Web/API/Navigator)。



如果您在连接外部库时遇到困难，可以参考[JavaScript 错误故障排除指南](../../gu-zhang-pai-chu/js-cuo-wu.md)

