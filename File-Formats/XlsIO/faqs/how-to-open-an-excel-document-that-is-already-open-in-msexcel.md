---
title: Open an Excel document that is already open in MS-Excel | Syncfusion
description: This page tells how to open an Excel document that is already open in Microsoft Excel in Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# How to open an Excel document that is already open in MS-Excel?

Syncfusion XlsIO do support opening an Excel document that is already open in Microsoft Excel. But the approaches are different in .NET Framework and .NET Standard.

[OpenReadOnly](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbooks.html#Syncfusion_XlsIO_IWorkbooks_OpenReadOnly_System_String_) method can be used in .NET Framework whereas **FileShare.ReadWrite** overload should be used while loading the file into file stream in .NET Standard. The following code snippet explains this.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;
  IWorkbook workbook = application.Workbooks.OpenReadOnly("Template.xlsx");
  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;	
  FileStream inputStream = new FileStream("Template.xlsx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
  IWorkbook workbook = application.Workbooks.Open(inputStream);	
  FileStream outputStream = new FileStream("Output.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(outputStream);
}
{% endhighlight %}
{% endtabs %}