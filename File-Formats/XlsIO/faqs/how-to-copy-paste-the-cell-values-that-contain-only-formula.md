---
title: Copy/paste cell values that contain only formula| XlsIO | Syncfusion
description: Code example to copy and paste the values of the cells that contain only formulas using Essential XlsIO.
platform: file-formats
control: XlsIO
documentation: UG
---

# How to copy/paste the cell values that contain only formula?

You can copy and paste the values of the cell which contain only formula using [CopyTo](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IRange.html#Syncfusion_XlsIO_IRange_CopyTo_Syncfusion_XlsIO_IRange_Syncfusion_XlsIO_ExcelCopyRangeOptions_) method by specifying the [ExcelCopyRangeOptions](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelCopyRangeOptions.html) as **None**. The following code snippet illustrates this.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Assigning formula to a cell
  worksheet.Range["A3"].Formula = "SUM(1+1)";
  IRange sourceRange = worksheet.Range["A3"];
  IRange destinationRange = worksheet.Range["B1"];

  //Copy and paste the values using ExcelCopyRangeOption
  sourceRange.CopyTo(destinationRange, ExcelCopyRangeOptions.None);

  FileStream stream = new FileStream("Output.xlsx", FileMode.OpenOrCreate, FileAccess.ReadWrite);
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
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Assigning formula to a cell
  worksheet.Range["A3"].Formula="SUM(1+1)";
  IRange sourceRange = worksheet.Range["A3"];
  IRange destinationRange = worksheet.Range["B1"];

  //Copy and paste the values using ExcelCopyRangeOption
  sourceRange.CopyTo(destinationRange, ExcelCopyRangeOptions.None);

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Assigning formula to a cell
  worksheet.Range("A3").Formula = "SUM(1+1)"
  Dim sourceRange As IRange = worksheet.Range("A3")
  Dim destinationRange As IRange = worksheet.Range("B1")

  'Copy and paste the values using ExcelCopyRangeOption
  sourceRange.CopyTo(destinationRange, ExcelCopyRangeOptions.None)

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}
{% endtabs %}  

## See Also

* [How to copy a range from one workbook to another?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-copy-a-range-from-one-workbook-to-another)
* [How to protect certain cells in a worksheet?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-protect-certain-cells-in-a-worksheet)
* [How to set a line break inside a cell?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-set-a-line-break-inside-a-cell)
* [How to format text within a cell?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-format-text-within-a-cell)
* [How to copy or move a range?](https://help.syncfusion.com/file-formats/xlsio/worksheet-cells-manipulation#copy-or-move-a-range)
* [How to copy and paste as link?](https://help.syncfusion.com/file-formats/xlsio/worksheet-cells-manipulation#copy-and-paste-as-link)
* [How to skip blanks while copying?](https://help.syncfusion.com/file-formats/xlsio/worksheet-cells-manipulation#skip-blanks-while-copying)

