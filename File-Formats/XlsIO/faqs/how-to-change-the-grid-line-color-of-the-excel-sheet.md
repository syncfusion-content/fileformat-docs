---
title: How to change the grid line color of the Excel sheet | Syncfusion
description: Code example to change the grid line color of the Excel sheet using Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# How to change the grid line color of the Excel sheet?

In Essential XlsIO, you can change the grid line color of the worksheet using [GridLineColor](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorksheet.html#Syncfusion_XlsIO_IWorksheet_GridLineColor) property. The below code snippet illustrate this.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //To change the grid line color using ExcelKnownColors
  worksheet.GridLineColor = ExcelKnownColors.Blue;

  FileStream stream = new FileStream("GridLineColor.xlsx", FileMode.OpenOrCreate, FileAccess.ReadWrite);
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

  //To change the grid line color using ExcelKnownColors
  worksheet.GridLineColor = ExcelKnownColors.Blue;

  workbook.SaveAs("GridLineColor.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'To change the grid line color using ExcelKnownColors
  worksheet.GridLineColor = ExcelKnownColors.Blue

  workbook.SaveAs("GridLineColor.xlsx")
End Using
{% endhighlight %}
{% endtabs %}  

## See Also

* [How to set a line break inside a cell?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-set-a-line-break-inside-a-cell)
* [How to show or hide gridlines?](https://help.syncfusion.com/file-formats/xlsio/working-with-excel-worksheet#show-or-hide-grid-lines)
* [How to hide chart gridlines?](https://help.syncfusion.com/file-formats/xlsio/working-with-charts#hide-chart-gridlines)
* [How to highlight worksheet tabs?](https://help.syncfusion.com/file-formats/xlsio/working-with-excel-worksheet#highlight-worksheet-tabs)
* [How to apply color settings?](https://help.syncfusion.com/file-formats/xlsio/working-with-cell-or-range-formatting#apply-color-settings)
* [How to change data point label color of a Waterfall chart?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-change-data-point-label-color-of-a-waterfall-chart)