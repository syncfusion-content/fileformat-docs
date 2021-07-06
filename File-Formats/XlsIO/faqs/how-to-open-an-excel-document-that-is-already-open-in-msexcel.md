---
title: FAQ Section| XlsIO | Syncfusion
description: This page tells how to open an Excel document that is already open in Microsoft Excel in Syncfusion .NET Excel library (XlsIO).
platform: File-formats
control: XlsIO
documentation: UG
---

# How to open an Excel document using XlsIO that is already open in MS-Excel?

Syncfusion XlsIO do support opening an Excel document that is already open in Microsoft Excel. But the approaches are different in .NET Framework and .NET Standard.

OpenReadOnly method can be used in .NET Framework whereas FileShare.ReadWrite overload should be used while loading the file into file stream in .NET Standard. The following code snippet explains this.

{% tabs %}
{% highlight C# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Excel2016;

    IWorkbook workbook = application.Workbooks.OpenReadOnly("Template.xlsx");

    workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight ASP.NET Core %}
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