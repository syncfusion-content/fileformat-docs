---
title: Find and highlight data in Excel | Syncfusion
description: This page shows how to find and highlight data in Excel using the Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# How to find and highlight data in Excel?

XlsIO provides following options to perform find and replace for text and numbers in Excel workbook or worksheet:

* Search for data in formulas, values or comments.
* Search for case-sensitive data and to match entire cell contents of the cell.

To know more about these options, please refer the [ExcelFindType](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelFindType.html), [ExcelFindOptions](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelFindOptions.html) in the API documentation section.

All the occurrences of a text in Excel worksheet can be found through [FindAll](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorksheet.html#Syncfusion_XlsIO_IWorksheet_FindAll_System_String_Syncfusion_XlsIO_ExcelFindType_) method.

The following code illustrates how to find all the occurrences of a value in a worksheet and highlight that data.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Finds a value 1500 in a sheet and highlights the cell which contains the value
  foreach(IRange range in sheet.FindAll(1500,ExcelFindType.Number))
  {
    range.CellStyle.Color = ExcelKnownColors.Green;
  }

  //Saving the workbook as stream
  FileStream stream = new FileStream("Output.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Finds a value 1500 in a sheet and highlights the cell which contains the value
  foreach(IRange range in sheet.FindAll(1500,ExcelFindType.Number))
  {
    range.CellStyle.Color = ExcelKnownColors.Green;
  }

  //Saving the workbook
  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Finds a value 1500 in a sheet and highlights the cell which contains the value
  For Each range As IRange In sheet.FindAll(1500, ExcelFindType.Number)
    range.CellStyle.Color = ExcelKnownColors.Green
  Next

  'Saving the workbook
  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}
{% endtabs %} 
