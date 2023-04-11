---
title: How to open an Excel file with encoding in .NET Core | XlsIO | Syncfusion
description: This page demonstrates with an example to open an Excel file with encoding in .NET Core using Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# How to open an Excel file with encoding in .NET Core?

XlsIO do not have direct support to open an Ecvel file with encoding in .NET Core. But this can be acheived through below workaround.

{% tabs %}
{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;

  FileStream stream = new FileStream("Sample.csv", FileMode.Open, FileAccess.Read);
  System.Text.UnicodeEncoding.RegisterProvider(System.Text.CodePagesEncodingProvider.Instance);
  IWorkbook workbook = application.Workbooks.Open(stream, System.Text.UnicodeEncoding.GetEncoding("big5"));

  FileStream outputStream = new FileStream("Output.csv", FileMode.Create, FileAccess.Write);
  workbook.SaveAs(outputStream, ",");
}

{% endhighlight %}
{% endtabs %}
