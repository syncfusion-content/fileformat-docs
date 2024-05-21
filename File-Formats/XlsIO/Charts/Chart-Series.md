---
title: Modify the Appearance of Series | Syncfusion
description: Learn how to modify the appearance of series in a chart in an Excel document using Syncfusion .NET Excel (XlsIO) library without Microsoft Excel.
platform: file-formats
control: XlsIO
documentation: UG
---

# Chart Series in Excel document

In a chart, a **series** represents a set of related data points, often depicted using lines, bars, or markers to show data trends or comparisons. Using XlsIO, you can **customize the series in the chart**.

## Set the Series Name

The following code snippet illustrates how to set the series name in chart.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Set name to chart series.
chart.Series[0].Name = "Amount";
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Set name to chart series.
chart.Series[0].Name = "Amount";
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Set name to chart series.
chart.Series[0].Name = "Amount"
{% endhighlight %}
{% endtabs %}

## Set the Series Type

The following code snippet illustrates how to set the series type.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Set the series type.
chart.Series[0].SerieType = ExcelChartType.Line_Markers;
chart.Series[1].SerieType = ExcelChartType.Bar_Clustered;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Set the series type.
chart.Series[0].SerieType = ExcelChartType.Line_Markers;
chart.Series[1].SerieType = ExcelChartType.Bar_Clustered;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Set the series type.
chart.Series[0].SerieType = ExcelChartType.Line_Markers
chart.Series[1].SerieType = ExcelChartType.Bar_Clustered
{% endhighlight %}
{% endtabs %}

## Customize the Series Color

The following code snippet illustrates how to customize the series color.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Configure the fill settings for the series in the chart.
chart.Series[1].SerieFormat.Fill.FillType = ExcelFillType.Gradient;
chart.Series[1].SerieFormat.Fill.GradientColorType = ExcelGradientColor.TwoColor;
chart.Series[1].SerieFormat.Fill.BackColor = Syncfusion.Drawing.Color.FromArgb(205, 217, 234);
chart.Series[1].SerieFormat.Fill.ForeColor = Syncfusion.Drawing.Color.Red;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Configure the fill settings for the series in the chart.
chart.Series[1].SerieFormat.Fill.FillType = ExcelFillType.Gradient;
chart.Series[1].SerieFormat.Fill.GradientColorType = ExcelGradientColor.TwoColor;
chart.Series[1].SerieFormat.Fill.BackColor = Color.FromArgb(205, 217, 234);
chart.Series[1].SerieFormat.Fill.ForeColor = Color.Red;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Configure the fill settings for the series in the chart.
chart.Series(1).SerieFormat.Fill.FillType = ExcelFillType.Gradient
chart.Series(1).SerieFormat.Fill.GradientColorType = ExcelGradientColor.TwoColor
chart.Series(1).SerieFormat.Fill.BackColor = Color.FromArgb(205, 217, 234)
chart.Series(1).SerieFormat.Fill.ForeColor = Color.Red
{% endhighlight %}
{% endtabs %}

## Customize the Series Border

The following code snippet illustrates how to customize the series border.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Customize series border.
chart.Series[1].SerieFormat.LineProperties.LineColor = Syncfusion.Drawing.Color.Red;
chart.Series[1].SerieFormat.LineProperties.LinePattern = ExcelChartLinePattern.Dot;
chart.Series[1].SerieFormat.LineProperties.LineWeight = ExcelChartLineWeight.Narrow;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Customize series border.
chart.Series[1].SerieFormat.LineProperties.LineColor = Color.Red;
chart.Series[1].SerieFormat.LineProperties.LinePattern = ExcelChartLinePattern.Dot;
chart.Series[1].SerieFormat.LineProperties.LineWeight = ExcelChartLineWeight.Narrow;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Customize series border.
chart.Series(1).SerieFormat.LineProperties.LineColor = Color.Red
chart.Series(1).SerieFormat.LineProperties.LinePattern = ExcelChartLinePattern.Dot
chart.Series(1).SerieFormat.LineProperties.LineWeight = ExcelChartLineWeight.Narrow
{% endhighlight %}
{% endtabs %}

The complete code snippet illustrating the above options is shown below.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;
    FileStream inputStream = new FileStream("../../../Data/InputTemplate.xlsx", FileMode.Open, FileAccess.Read);
    IWorkbook workbook = application.Workbooks.Open(inputStream);
    IWorksheet sheet = workbook.Worksheets[0];
    IChartShape chart = sheet.Charts[0];

    //Set name to chart series.
    chart.Series[0].Name = "Amount";

    //Set the series type.
    chart.Series[0].SerieType = ExcelChartType.Line_Markers;
    chart.Series[1].SerieType = ExcelChartType.Bar_Clustered;

    // Configure the fill settings for the series in the chart.
    chart.Series[1].SerieFormat.Fill.FillType = ExcelFillType.Gradient;
    chart.Series[1].SerieFormat.Fill.GradientColorType = ExcelGradientColor.TwoColor;
    chart.Series[1].SerieFormat.Fill.BackColor = Syncfusion.Drawing.Color.FromArgb(205, 217, 234);
    chart.Series[1].SerieFormat.Fill.ForeColor = Syncfusion.Drawing.Color.Red;

    //Customize series border.
    chart.Series[1].SerieFormat.LineProperties.LineColor = Color.Red;
    chart.Series[1].SerieFormat.LineProperties.LinePattern = ExcelChartLinePattern.Dot;
    chart.Series[1].SerieFormat.LineProperties.LineWeight = ExcelChartLineWeight.Narrow;

    //Saving the workbook as stream
    FileStream outputStream = new FileStream("Output.xlsx", FileMode.Create, FileAccess.ReadWrite);
    workbook.SaveAs(outputStream);
    outputStream.Dispose();
    inputStream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;
    IWorkbook workbook = application.Workbooks.Open("InputTemplate.xlsx");
    IWorksheet sheet = workbook.Worksheets[0];
    IChartShape chart = sheet.Charts[0];

    //Set name to chart series.
    chart.Series[0].Name = "Amount";

    //Set the series type.
    chart.Series[0].SerieType = ExcelChartType.Line_Markers;
    chart.Series[1].SerieType = ExcelChartType.Bar_Clustered;

    // Configure the fill settings for the series in the chart.
    chart.Series[1].SerieFormat.Fill.FillType = ExcelFillType.Gradient;
    chart.Series[1].SerieFormat.Fill.GradientColorType = ExcelGradientColor.TwoColor;
    chart.Series[1].SerieFormat.Fill.BackColor = Color.FromArgb(205, 217, 234);
    chart.Series[1].SerieFormat.Fill.ForeColor = Color.Red;

    //Customize series border.
    chart.Series[1].SerieFormat.LineProperties.LineColor = Color.Red;
    chart.Series[1].SerieFormat.LineProperties.LinePattern = ExcelChartLinePattern.Dot;
    chart.Series[1].SerieFormat.LineProperties.LineWeight = ExcelChartLineWeight.Narrow;

    //Saving the workbook
    workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As New ExcelEngine()
    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Xlsx
    Dim workbook As IWorkbook = application.Workbooks.Open("InputTemplate.xlsx")
    Dim sheet As IWorksheet = workbook.Worksheets(0)
    Dim chart As IChartShape = sheet.Charts(0)

    'Set name to chart series.
    chart.Series(0).Name = "Amount"

    'Set the series type.
    chart.Series(0).SerieType = ExcelChartType.Line_Markers
    chart.Series(1).SerieType = ExcelChartType.Bar_Clustered

    ' Configure the fill settings for the series in the chart.
    chart.Series(1).SerieFormat.Fill.FillType = ExcelFillType.Gradient
    chart.Series(1).SerieFormat.Fill.GradientColorType = ExcelGradientColor.TwoColor
    chart.Series(1).SerieFormat.Fill.BackColor = Color.FromArgb(205, 217, 234)
    chart.Series(1).SerieFormat.Fill.ForeColor = Color.Red

    'Customize series border.
    chart.Series(1).SerieFormat.LineProperties.LineColor = Color.Red
    chart.Series(1).SerieFormat.LineProperties.LinePattern = ExcelChartLinePattern.Dot
    chart.Series(1).SerieFormat.LineProperties.LineWeight = ExcelChartLineWeight.Narrow

    'Saving the workbook
    workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}
{% endtabs %}

A complete working example to format the series in C# is present on [this GitHub page]().

## Set the DataPoint as Total

The following code snippet illustrates how to set the Data Point as total in chart.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Data point settings as total in chart.
chart.Series[0].DataPoints[3].SetAsTotal = true;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Data point settings as total in chart.
chart.Series[0].DataPoints[3].SetAsTotal = true;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Data point settings as total in chart.
chart.Series(0).DataPoints(3).SetAsTotal = True
{% endhighlight %}
{% endtabs %}

## Set the connector lines between data points 

The following code snippet illustrates how to set the connector lines between data points. 

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Showing the connector lines between data points.
chart.Series[0].SerieFormat.ShowConnectorLines = true;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Showing the connector lines between data points.
chart.Series[0].SerieFormat.ShowConnectorLines = true;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Showing the connector lines between data points.
chart.Series(0).SerieFormat.ShowConnectorLines = True
{% endhighlight %}
{% endtabs %}

## Add space between bars

Spaces between chart bars are of two types.

1. **Series Overlap** : Space between bars of different data series of single category.
2. **Gap Width** : Space between different categories.

XlsIO allows you to adjust the space between chart bars using [Overlap](https://help.syncfusion.com/cr/windowsforms/Syncfusion.XlsIO.IChartFormat.html#Syncfusion_XlsIO_IChartFormat_Overlap) and [GapWidth](https://help.syncfusion.com/cr/windowsforms/Syncfusion.XlsIO.IChartFormat.html#Syncfusion_XlsIO_IChartFormat_GapWidth) properties of [IChartFormat](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IChartFormat.html) interface.

The following code snippet illustrates how to add space between bars.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Adding space between bars of different series of single category.
chart.Series[0].SerieFormat.CommonSerieOptions.Overlap = 60;

//Adding space between bars of different categories.
chart.Series[0].SerieFormat.CommonSerieOptions.GapWidth = 80;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Adding space between bars of different series of single category.
chart.Series[0].SerieFormat.CommonSerieOptions.Overlap = 60;

//Adding space between bars of different categories.
chart.Series[0].SerieFormat.CommonSerieOptions.GapWidth = 80;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Adding space between bars of different series of a single category.
chart.Series(0).SerieFormat.CommonSerieOptions.Overlap = 60

'Adding space between bars of different categories.
chart.Series(0).SerieFormat.CommonSerieOptions.GapWidth = 80
{% endhighlight %}
{% endtabs %}

A complete working example for adding space between chart bars in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Create%20and%20Edit%20Charts/Chart%20Bars%20Spacing).

## Add High-Low Lines

The following code snippet illustrates how to add high-low lines.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Set HasHighLowLines property to true.
chart.Series[0].SerieFormat.CommonSerieOptions.HasHighLowLines = true;

//Apply formats to HighLowLines.
chart.Series[0].SerieFormat.CommonSerieOptions.HighLowLines.LineColor = Syncfusion.Drawing.Color.Red;
chart.Series[0].SerieFormat.CommonSerieOptions.HighLowLines.LinePattern = ExcelChartLinePattern.Dot;
chart.Series[0].SerieFormat.CommonSerieOptions.HighLowLines.LineWeight = ExcelChartLineWeight.Narrow;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Set HasHighLowLines property to true.
chart.Series[0].SerieFormat.CommonSerieOptions.HasHighLowLines = true;

//Apply formats to HighLowLines.
chart.Series[0].SerieFormat.CommonSerieOptions.HighLowLines.LineColor = Color.Red;
chart.Series[0].SerieFormat.CommonSerieOptions.HighLowLines.LinePattern = ExcelChartLinePattern.Dot;
chart.Series[0].SerieFormat.CommonSerieOptions.HighLowLines.LineWeight = ExcelChartLineWeight.Narrow;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Set HasHighLowLines property to true.
chart.Series(0).SerieFormat.CommonSerieOptions.HasHighLowLines = True

'Apply formats to HighLowLines.
chart.Series(0).SerieFormat.CommonSerieOptions.HighLowLines.LineColor = Color.Red
chart.Series(0).SerieFormat.CommonSerieOptions.HighLowLines.LinePattern = ExcelChartLinePattern.Dot
chart.Series(0).SerieFormat.CommonSerieOptions.HighLowLines.LineWeight = ExcelChartLineWeight.Narrow
{% endhighlight %}
{% endtabs %}

A complete working example to show high low lines of chart in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Create%20and%20Edit%20Charts/High%20Low%20Lines).

## Add Drop Lines

The following code snippet illustrates how to add drop lines.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Set the HasDropLines property to true.
chart.Series[0].SerieFormat.CommonSerieOptions.HasDropLines = true;

//Apply formats to DropLines.
chart.Series[0].SerieFormat.CommonSerieOptions.DropLines.LineColor = Syncfusion.Drawing.Color.Red;
chart.Series[0].SerieFormat.CommonSerieOptions.DropLines.LinePattern = ExcelChartLinePattern.Dot;
chart.Series[0].SerieFormat.CommonSerieOptions.DropLines.LineWeight = ExcelChartLineWeight.Narrow;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Set the HasDropLines property to true.
chart.Series[0].SerieFormat.CommonSerieOptions.HasDropLines = true;

//Apply formats to DropLines.
chart.Series[0].SerieFormat.CommonSerieOptions.DropLines.LineColor = Color.Red;
chart.Series[0].SerieFormat.CommonSerieOptions.DropLines.LinePattern = ExcelChartLinePattern.Dot;
chart.Series[0].SerieFormat.CommonSerieOptions.DropLines.LineWeight = ExcelChartLineWeight.Narrow;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Set HasDropLines property to true.
chart.Series(0).SerieFormat.CommonSerieOptions.HasDropLines = True

'Apply formats to DropLines.
chart.Series(0).SerieFormat.CommonSerieOptions.DropLines.LineColor = Color.Red
chart.Series(0).SerieFormat.CommonSerieOptions.DropLines.LinePattern = ExcelChartLinePattern.Dot;
chart.Series(0).SerieFormat.CommonSerieOptions.DropLines.LineWeight = ExcelChartLineWeight.Narrow
{% endhighlight %}
{% endtabs %}

A complete working example to add drop lines of chart in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Create%20and%20Edit%20Charts/Drop%20Lines).

## Add Series Lines

The following code snippet illustrates how to add series lines in chart.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Set HasSeriesLines property to true.
chart.Series[0].SerieFormat.CommonSerieOptions.HasSeriesLines = true;

//Apply formats to SeriesLines.
chart.Series[0].SerieFormat.CommonSerieOptions.PieSeriesLine.LineColor = Syncfusion.Drawing.Color.Red;
chart.Series[0].SerieFormat.CommonSerieOptions.PieSeriesLine.LinePattern = ExcelChartLinePattern.Dot;
chart.Series[0].SerieFormat.CommonSerieOptions.PieSeriesLine.LineWeight = ExcelChartLineWeight.Narrow;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Set HasSeriesLines property to true.
chart.Series[0].SerieFormat.CommonSerieOptions.HasSeriesLines = true;

//Apply formats to SeriesLines.
chart.Series[0].SerieFormat.CommonSerieOptions.PieSeriesLine.LineColor = Color.Red;
chart.Series[0].SerieFormat.CommonSerieOptions.PieSeriesLine.LinePattern = ExcelChartLinePattern.Dot;
chart.Series[0].SerieFormat.CommonSerieOptions.PieSeriesLine.LineWeight = ExcelChartLineWeight.Narrow;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Set HasSeriesLines property to true.
chart.Series(0).SerieFormat.CommonSerieOptions.HasSeriesLines = true

'Apply formats to SeriesLines.
chart.Series(0).SerieFormat.CommonSerieOptions.PieSeriesLine.LineColor = Color.Red
chart.Series(0).SerieFormat.CommonSerieOptions.PieSeriesLine.LinePattern = ExcelChartLinePattern.Dot
chart.Series(0).SerieFormat.CommonSerieOptions.PieSeriesLine.LineWeight = ExcelChartLineWeight.Narrow
{% endhighlight %}
{% endtabs %}

A complete working example to add series lines of chart in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Create%20and%20Edit%20Charts/Series%20Lines).

## Different Marker Properties

The following code snippet illustrates how to customize the marker properties.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Set the marker style of the first series in the chart.
chart.Series[0].SerieFormat.MarkerStyle = ExcelChartMarkerType.Star;

//Customize the marker style.
chart.Series[0].SerieFormat.MarkerSize = 8;
chart.Series[0].SerieFormat.MarkerBackgroundColor = Syncfusion.Drawing.Color.Red;
chart.Series[0].SerieFormat.MarkerForegroundColor = Syncfusion.Drawing.Color.Black;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Set the marker style of the first series in the chart.
chart.Series[0].SerieFormat.MarkerStyle = ExcelChartMarkerType.Star;

//Customize the marker style.
chart.Series[0].SerieFormat.MarkerSize = 8;
chart.Series[0].SerieFormat.MarkerBackgroundColor = Color.Red;
chart.Series[0].SerieFormat.MarkerForegroundColor = Color.Black;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
' Set the marker style of the first series in the chart.
chart.Series(0).SerieFormat.MarkerStyle = ExcelChartMarkerType.Star

'Customize the marker style.
chart.Series(0).SerieFormat.MarkerSize = 8
chart.Series(0).SerieFormat.MarkerBackgroundColor = Color.Red
chart.Series(0).SerieFormat.MarkerForegroundColor = Color.Black
{% endhighlight %}
{% endtabs %}

## See Also
* [How to filter Excel chart series in C#, VB.NET?](https://support.syncfusion.com/kb/article/7509/how-to-filter-excel-chart-series-in-c-vb-net)
* [How to change Excel chart series color in C#, VB.NET?](https://support.syncfusion.com/kb/article/2733/how-to-change-excel-chart-series-color-in-c-vbnet)
* [How to set trendlines for Excel chart series in C#, VB.NET?](https://support.syncfusion.com/kb/article/7532/how-to-set-trendlines-for-excel-chart-series-in-c-vb-net)