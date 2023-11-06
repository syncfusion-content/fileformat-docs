---
title: How to unfreeze the rows and columns in XlsIO | XlsIO | Syncfusion
description: This page demonstrates with an example to unfreeze the rows and columns using Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# How to unfreeze the rows and columns in XlsIO?

You can unfreeze rows and columns in XlsIO by using the [RemovePanes](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorksheet.html#Syncfusion_XlsIO_IWorksheet_RemovePanes) method. The following code snippet illustrates this.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream inputStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelOpenType.Automatic);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Freeze the panes
  worksheet.Range[8, 1].FreezePanes();

  //Unfreeze the panes
  worksheet.RemovePanes();

  FileStream stream = new FileStream("Unfreeze.xlsx", FileMode.OpenOrCreate, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  workbook.Close();
  excelEngine.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Freeze the panes
  worksheet.Range[8, 1].FreezePanes();

  //Unfreeze the panes
  worksheet.RemovePanes();

  workbook.SaveAs("Unfreeze.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Freeze the panes
  worksheet.Range(8, 1).FreezePanes()

  'Unfreeze the panes
  worksheet.RemovePanes()

  workbook.SaveAs("Unfreeze.xlsx")
End Using
{% endhighlight %}
{% endtabs %}  

## See Also

* [What is the maximum range of Rows and Columns?](what-is-the-maximum-range-of-rows-and-columns)
* [How to hide the summary rows and columns using XlsIO?](how-to-hide-the-summary-rows-and-columns-using-xlsio)
* [How to sort two or more columns in a pivot table?](how-to-sort-two-or-more-columns-in-a-pivot-table)
* [How to freeze panes?](https://help.syncfusion.com/file-formats/xlsio/working-with-excel-worksheet#freeze-panes)
* [How to unfreeze panes?](https://help.syncfusion.com/file-formats/xlsio/working-with-excel-worksheet#unfreeze-panes)
* [How to split panes?](https://help.syncfusion.com/file-formats/xlsio/working-with-excel-worksheet#split-panes)
