---
title: How to set a line break inside a cell | XlsIO | Syncfusion
description: This page illustrates on how to set a line break inside a cell using Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# How to set a line break inside a cell?

In order to set a line break inside a cell, you have to enable Text Wrapping for the cell, and then break the text. The following code snippet illustrates this.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Save the line break inside the cell
  worksheet.Range["A1"].CellStyle.WrapText = true;
  worksheet.Range["A1"].Text = String.Format("Hello\nworld");

  FileStream stream = new FileStream("LineBreak.xlsx", FileMode.OpenOrCreate, FileAccess.ReadWrite);
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

  //Save the line break inside the cell
  worksheet.Range["A1"].CellStyle.WrapText = true;
  worksheet.Range["A1"].Text = String.Format("Hello\nworld");
  workbook.SaveAs("LineBreak.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Save the line break inside the cell
  worksheet.Range("A1").CellStyle.WrapText = True
  worksheet.Range("A1").Text = String.Format("Hello" & vbLf & "world")
  workbook.SaveAs("LineBreak.xlsx")
End Using
{% endhighlight %}
{% endtabs %}  

## See Also

* [How to format text within a cell?](how-to-format-text-within-a-cell)
* [How to protect certain cells in a worksheet?](how-to-protect-certain-cells-in-a-worksheet)
* [How to copy/paste the cell values that contain only formula?](how-to-copy-paste-the-cell-values-that-contain-only-formula)
* [How to change the grid line color of the Excel sheet?](how-to-change-the-grid-line-color-of-the-excel-sheet)
* [How to show or hide gridlines?](https://help.syncfusion.com/file-formats/xlsio/working-with-excel-worksheet#show-or-hide-grid-lines)
* [How to apply wrap text?](https://help.syncfusion.com/file-formats/xlsio/working-with-cell-or-range-formatting#apply-wrap-text)
