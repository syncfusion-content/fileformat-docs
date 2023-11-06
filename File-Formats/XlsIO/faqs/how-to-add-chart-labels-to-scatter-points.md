---
title: How to add chart labels to scatter points | XlsIO | Syncfusion
description: This page shows how to add chart labels to scatter points using Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# How to add chart labels to scatter points?

The following code illustrates adding chart labels to the scatter points of the chart.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream inputStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelOpenType.Automatic);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Get the chart from the charts collection
  IChart chart = worksheet.Charts[0];

  //Get the first series from the Series collection
  IChartSerie serieOne = chart.Series[0];

  //Set the Series name to the Data Labels through Data Points
  serieOne.DataPoints[0].DataLabels.IsSeriesName = true;

  //Set the Value to the Data Labels through Data Points
  serieOne.DataPoints[0].DataLabels.IsValue = true;

  FileStream stream = new FileStream("ChartLabels.xlsx", FileMode.OpenOrCreate, FileAccess.ReadWrite);
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

  //Get the chart from the charts collection
  IChart chart = worksheet.Charts[0];

  //Get the first series from the Series collection
  IChartSerie serieOne = chart.Series[0];

  //Set the Series name to the Data Labels through Data Points
  serieOne.DataPoints[0].DataLabels.IsSeriesName = true;

  //Set the Value to the Data Labels through Data Points
  serieOne.DataPoints[0].DataLabels.IsValue = true;

  workbook.SaveAs("ChartLabels.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Get the chart from the charts collection
  Dim chart As IChart = worksheet.Charts(0)

  'Get the first series from the Series collection
  Dim serieOne As IChartSerie = chart.Series(0)

  'Set the Series name to the Data Labels through Data Points
  serieOne.DataPoints(0).DataLabels.IsSeriesName = True

  'Set the Value to the Data Labels through Data Points
  serieOne.DataPoints(0).DataLabels.IsValue = True

  workbook.SaveAs("ChartLabels.xlsx")
End Using
{% endhighlight %}
{% endtabs %}

## See Also

* [How to change data point label color of a Waterfall chart?](how-to-change-data-point-label-color-of-a-waterfall-chart)
* [How to create a Chart with a discontinuous range?](how-to-create-a-chart-with-a-discontinuous-range)
* [What are the chart data label formatting?](https://help.syncfusion.com/file-formats/xlsio/working-with-charts#data-labels-appearance)
* [What are the font settings for chart legend and data labels?](https://help.syncfusion.com/file-formats/xlsio/working-with-charts#font-settings-for-chart-legend-and-data-labels)
