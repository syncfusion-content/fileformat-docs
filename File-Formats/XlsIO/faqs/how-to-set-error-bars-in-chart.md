---
title: How to set error bars in chart | Syncfusion
description: This page demonstrates with an example on how to set error bars in chart with Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# How to set error bars in chart?

Charts can be enhanced by adding error bars which help to view the margin errors and deviations. The following code snippet shows how to set error bar in a chart series.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream inputStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelOpenType.Automatic);
  IWorksheet sheet = workbook.Worksheets[0];
 
  //Create a Chart
  IChartShape chart = sheet.Charts.Add();
 
  //Set Chart Type
  chart.ChartType = ExcelChartType.Column_Clustered;
 
  //Set data range in the worksheet
  chart.DataRange = sheet.Range["A1:E5"];

  //Set error bar
  chart.Series[0].ErrorBar(true, ExcelErrorBarInclude.Plus, ExcelErrorBarType.Percentage, 50);

  FileStream stream = new FileStream("ErrorBars.xlsx", FileMode.OpenOrCreate, FileAccess.ReadWrite);
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
    IWorksheet sheet = workbook.Worksheets[0];
 
    //Create a Chart
    IChartShape chart = sheet.Charts.Add();
 
    //Set Chart Type
    chart.ChartType = ExcelChartType.Column_Clustered;
 
    //Set data range in the worksheet
    chart.DataRange = sheet.Range["A1:E5"];

    //Set error bar
    chart.Series[0].ErrorBar(true, ExcelErrorBarInclude.Plus, ExcelErrorBarType.Percentage, 50);
 
    workbook.SaveAs("ErrorBars.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)
  Dim sheet As IWorksheet =  workbook.Worksheets(0) 
 
  'Create a Chart
  Dim chart As IChartShape =  sheet.Charts.Add() 
 
  'Set Chart Type
  chart.ChartType = ExcelChartType.Column_Clustered
 
  'Set data range in the worksheet
  chart.DataRange = sheet.Range("A1:E5")
 
  'Set error bar
  chart.Series(0).ErrorBar(True, ExcelErrorBarInclude.Plus, ExcelErrorBarType.Percentage, 50)

  workbook.SaveAs("ErrorBars.xlsx")
End Using
{% endhighlight %}
{% endtabs %}

## See Also

* [How to change data point label color of a Waterfall chart?](how-to-change-data-point-label-color-of-a-waterfall-chart)
* [How to create a Chart with a discontinuous range?](how-to-create-a-chart-with-a-discontinuous-range)
* [What are the chart data label formatting?](https://help.syncfusion.com/file-formats/xlsio/working-with-charts#data-labels-appearance)
* [What are the font settings for chart legend and data labels?](https://help.syncfusion.com/file-formats/xlsio/working-with-charts#font-settings-for-chart-legend-and-data-labels)
