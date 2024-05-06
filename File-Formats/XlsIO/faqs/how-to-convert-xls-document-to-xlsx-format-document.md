---
title: How to convert xls document to xlsx format document |Syncfusion.
description: This page explains how to convert xls document to xlsx format document using Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# How to convert xls document to xlsx format document?

The following code illustrates how to convert xls document to xlsx format document.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;
    
    //Loads an xls file
    FileStream fileStream = new FileStream("InputTemplate.xlsx", FileMode.Open, FileAccess.Read);
    IWorkbook workbook = application.Workbooks.Open(fileStream);

    //Set the workbook version to xlsx
    workbook.Version = ExcelVersion.Xlsx;
    
    //Saving the workbook as stream in xlsx format
    FileStream stream = new FileStream("Output.xlsx", FileMode.Create, FileAccess.ReadWrite);
    workbook.SaveAs(stream);
    stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine engine = new ExcelEngine())
{
    IApplication application = engine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;

    //Loads an xls file
    IWorkbook workbook = application.Workbooks.Open("InputTemplate.xls");

    //Set the workbook version to xlsx
    workbook.Version = ExcelVersion.Xlsx;

    //Saving the workbook in xlsx format
    workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using engine As ExcelEngine = New ExcelEngine()
    Dim application As IApplication = engine.Excel
    application.DefaultVersion = ExcelVersion.Xlsx

    'Loads an xls file
    Dim workbook As IWorkbook = application.Workbooks.Open("InputTemplate.xls")

    'Set the workbook version to xlsx
    workbook.Version = ExcelVersion.Xlsx;

    'Saving the workbook in xlsx format
    workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}
{% endtabs %}