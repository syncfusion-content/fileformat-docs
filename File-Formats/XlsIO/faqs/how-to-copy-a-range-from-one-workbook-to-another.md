---
title: How to copy a range from one workbook to another | XlsIO | Syncfusion
description: Code example to copy a range from one workbook to another using Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# How to copy a range from one workbook to another?

You can copy the range from source workbook to the destination workbook through [CopyTo](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IRange.html#Syncfusion_XlsIO_IRange_CopyTo_Syncfusion_XlsIO_IRange_Syncfusion_XlsIO_ExcelCopyRangeOptions_) method. 

The following code snippet illustrates this.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  FileStream inputStream1 = new FileStream("SourceWorkbook.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook sourceWorkbook = application.Workbooks.Open(inputStream1, ExcelOpenType.Automatic);
  FileStream inputStream2 = new FileStream("DestinationWorkbook.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook destinationWorkbook = application.Workbooks.Open(inputStream2, ExcelOpenType.Automatic);

  //The first worksheet object in the worksheets collection in the Source Workbook is accessed.
  IWorksheet sourceWorksheet = sourceWorkbook.Worksheets[0];

  //The first worksheet object in the worksheets collection in the Destination Workbook is accessed.
  IWorksheet destinationWorksheet = destinationWorkbook.Worksheets[0];

  //Assigning an object to the range of cells (90 rows) both for source and destination.
  IRange sourceRange = sourceWorksheet.Range[1, 1, 90, 100];
  IRange destinationRange = destinationWorksheet.Range[1, 1, 90, 100];

  //Copying (90 rows) from Source to Destination worksheet.
  sourceRange.CopyTo(destinationRange);

  FileStream stream = new FileStream("CopyingRange.xlsx", FileMode.OpenOrCreate, FileAccess.ReadWrite);
  destinationWorkbook.SaveAs(stream);
  destinationWorkbook.Close();
  excelEngine.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook sourceWorkbook = application.Workbooks.Open("SourceWorkbook.xlsx", ExcelOpenType.Automatic);
  IWorkbook destinationWorkbook = application.Workbooks.Open("DestinationWorkbook.xlsx", ExcelOpenType.Automatic);

  //The first worksheet object in the worksheets collection in the Source Workbook is accessed.
  IWorksheet sourceWorksheet = sourceWorkbook.Worksheets[0];

  //The first worksheet object in the worksheets collection in the Destination Workbook is accessed.
  IWorksheet destinationWorksheet = destinationWorkbook.Worksheets[0];

  //Assigning an object to the range of cells (90 rows) both for source and destination.
  IRange sourceRange = sourceWorksheet.Range[1, 1, 90, 100];
  IRange destinationRange = destinationWorksheet.Range[1, 1, 90, 100];

  //Copying (90 rows) from Source to Destination worksheet.
  sourceRange.CopyTo(destinationRange);

  destinationWorkbook.SaveAs("CopyingRange.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim sourceWorkbook As IWorkbook = application.Workbooks.Open("SourceWorkbook.xlsx", ExcelOpenType.Automatic)
  Dim destinationWorkbook As IWorkbook = application.Workbooks.Open("DestinationWorkbook.xlsx", ExcelOpenType.Automatic)

  'The first worksheet object in the worksheets collection in the Source Workbook is accessed.
  Dim sourceWorksheet As Syncfusion.XlsIO.IWorksheet = sourceWorkbook.Worksheets(0)

  'The first worksheet object in the worksheets collection in the Destination Workbook is accessed.
  Dim destinationWorksheet As Syncfusion.XlsIO.IWorksheet = destinationWorkbook.Worksheets(0)

  'Assigning an object to the range of cells (90 rows) both for source and destination.
  Dim sourceRange As Syncfusion.XlsIO.IRange = sourceWorksheet.Range(1, 1, 90, 100)
  Dim destinationRange As Syncfusion.XlsIO.IRange = destinationWorksheet.Range(1, 1, 90, 100)

  'Copying (90 rows) from Source to Destination worksheet.
  sourceRange.CopyTo(destinationRange)

  destinationWorkbook.SaveAs("CopyingRange.xlsx")
End Using
{% endhighlight %}
{% endtabs %}  

## See Also

* [How to copy/paste the cell values that contain only formula?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-copy-paste-the-cell-values-that-contain-only-formula)
* [How to copy or move a range?](https://help.syncfusion.com/file-formats/xlsio/worksheet-cells-manipulation#copy-or-move-a-range)
* [How to copy and paste as link?](https://help.syncfusion.com/file-formats/xlsio/worksheet-cells-manipulation#copy-and-paste-as-link)
* [How to skip blanks while copying?](https://help.syncfusion.com/file-formats/xlsio/worksheet-cells-manipulation#skip-blanks-while-copying)
* [How to open an existing XLSX workbook and save it as XLS?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-open-an-existing-xlsx-workbook-and-save-it-as-xls)
