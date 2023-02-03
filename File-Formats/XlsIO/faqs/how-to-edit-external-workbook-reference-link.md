---
title: How to edit external workbook reference link | XlsIO | Syncfusion
description: Code example to edit external workbook reference link using Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# How to edit external workbook reference link?

Existing external workbook reference link can be modified through [URL](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.Implementation.ExternWorkbookImpl.html#Syncfusion_XlsIO_Implementation_ExternWorkbookImpl_URL) property of [ExternWorkbookImpl](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.Implementation.ExternWorkbookImpl.html) class. Please find the code snippet below.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
string DataPathBase = System.Environment.CurrentDirectory + @"\";
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Open("../../Sample.xlsx");
  string filepath = (workbook as WorkbookImpl).ExternWorkbooks[0].URL;

  (workbook as WorkbookImpl).ExternWorkbooks[0].URL = DataPathBase + "Template.xlsx";

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}
{% endtabs %} 
