---
title: How to edit external workbook reference link | XlsIO | Syncfusion
description: Code example to edit existing external workbook reference link using Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# How to edit external workbook reference link?

Existing external workbook reference link can be modified through [URL](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.Implementation.ExternWorkbookImpl.html#Syncfusion_XlsIO_Implementation_ExternWorkbookImpl_URL) property of [ExternWorkbookImpl](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.Implementation.ExternWorkbookImpl.html) class. Please find the code snippet below.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
string DataPathBase = System.Environment.CurrentDirectory + @"\";
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  FileStream inputStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  string filepath = (workbook as WorkbookImpl).ExternWorkbooks[0].URL;

  (workbook as WorkbookImpl).ExternWorkbooks[0].URL = DataPathBase + "Template.xlsx";

  FileStream outputStream = new FileStream("Output.xlsx", FileMode.Create, FileAccess.Write);
  workbook.SaveAs(outputStream);
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
string DataPathBase = System.Environment.CurrentDirectory + @"\";
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
  string filepath = (workbook as WorkbookImpl).ExternWorkbooks[0].URL;

  (workbook as WorkbookImpl).ExternWorkbooks[0].URL = DataPathBase + "Template.xlsx";

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Dim DataPathBase As String = (System.Environment.CurrentDirectory + "\")
Using excelEngine As ExcelEngine = New ExcelEngine
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
  Dim filepath As String = CType(workbook, WorkbookImpl).ExternWorkbooks(0).URL
  CType(workbook, WorkbookImpl).ExternWorkbooks(0).URL = (DataPathBase + "Template.xlsx")
  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}
{% endtabs %} 
