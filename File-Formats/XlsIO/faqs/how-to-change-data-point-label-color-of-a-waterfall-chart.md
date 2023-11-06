---
title: How to change data point label color of Waterfall chart | Syncfusion
description: Code example to change data point label color of a Waterfall chart using Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# How to change data point label color of a Waterfall chart?

The following code snippet shows how to change data point label color of a Waterfall chart.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;
  FileStream inputStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(inputStream,ExcelOpenType.Automatic);
  IWorksheet sheet = workbook.Worksheets[0];

  //Accessing first chart in the sheet
  IChartShape chart = sheet.Charts[0];

  //Changing first data point label color
  chart.Series[0].DataPoints[0].DataLabels.IsValue = true;
  chart.Series[0].DataPoints[0].DataLabels.RGBColor = Color.Green;

  //Saving the workbook as stream
  FileStream stream = new FileStream("Waterfall.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);
  IWorksheet sheet = workbook.Worksheets[0];

  //Accessing first chart in the sheet
  IChartShape chart = sheet.Charts[0];

  //Changing first data point label color
  chart.Series[0].DataPoints[0].DataLabels.IsValue = true;
  chart.Series[0].DataPoints[0].DataLabels.RGBColor = Color.Green;

  workbook.SaveAs("Waterfall.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2016
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Create a chart
  Dim chart As IChartShape = sheet.Charts(0)

  'Changing first data point label color
  chart.Series(0).DataPoints(0).DataLabels.IsValue = true
  chart.Series(0).DataPoints(0).DataLabels.RGBColor = Color.Green

  workbook.SaveAs("Waterfall.xlsx")
End Using
{% endhighlight %}
{% endtabs %}

## See Also

* [How to change the grid line color of the Excel sheet?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-change-the-grid-line-color-of-the-excel-sheet)
* [How to import data table with its data type using template markers?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-import-data-table-with-its-data-type-using-template-markers)
* [How to add chart labels to scatter points?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-add-chart-labels-to-scatter-points)
* [How to create a Chart with a discontinuous range?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-create-a-chart-with-a-discontinuous-range)
* [How to create a Waterfall chart?](https://help.syncfusion.com/file-formats/xlsio/working-with-charts#waterfall)
* [What are the chart data label formatting?](https://help.syncfusion.com/file-formats/xlsio/working-with-charts#data-labels-appearance)
* [What are the font settings for chart legend and data labels?](https://help.syncfusion.com/file-formats/xlsio/working-with-charts#font-settings-for-chart-legend-and-data-labels)
