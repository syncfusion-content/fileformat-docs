---
title: Modify the appearance of series | Syncfusion
description: Learn how to modify the appearance of series in Word document using Syncfusion .NET Core Word (DocIO) library without Microsoft Word or interop dependencies.
platform: file-formats
control: DocIO
documentation: UG
---

# Series

Chart area refers to the space that contains the chart or graph you've inserted into a slide. It includes the entire chart and all its elements, such as data points, labels, axes, and the plot area. Using Syncfusion [.NET Core Word (DocIO)](https://www.syncfusion.com/document-processing/word-framework/net-core/word-library) library you can customize the chart area in the chart.

## Set series name
The following code snippet illustrates how to set the series name in chart.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Set name to chart series.
chart.Series[0].Name = "Sum of Purchases";

{% endhighlight %}
{% endtabs %}

## Set the series type

The following code snippet illustrates how to set the series type.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Set the series type.
chart.Series[0].SerieType = OfficeChartType.Line_Markers;

{% endhighlight %}
{% endtabs %}

## Set the DataPoint as Total
The following code snippet illustrates how to set the Data Point as total in chart.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Data point settings as total in chart.
chart.Series[0].DataPoints[3].SetAsTotal = true;
chart.Series[0].DataPoints[6].SetAsTotal = true;

{% endhighlight %}
{% endtabs %}

## Set the connector lines between data points. 

The following code snippet illustrates how to set the connector lines between data points. 

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Showing the connector lines between data points.
chart.Series[0].SerieFormat.ShowConnectorLines = true;

{% endhighlight %}
{% endtabs %}

## Customize the Data labels

The following code snippet illustrates how to customize the data labels.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Enable the datalabel in chart.
chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.IsValue = true;
//Set the datalabel size.
chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.Size = 8;
chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.FontName = "Tahoma";
chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.Size = 20;
chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.Color = OfficeKnownColors.Red;

{% endhighlight %}
{% endtabs %}

## Add space between bars

The following code snippet illustrates how to add space between bars.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Adding space between bars of different series of single category
chart.Series[0].SerieFormat.CommonSerieOptions.Overlap = 60;

//Adding space between bars of different categories
chart.Series[0].SerieFormat.CommonSerieOptions.GapWidth = 80;

{% endhighlight %}
{% endtabs %}

## Add High-Low Lines

The following code snippet illustrates how to add high-low lines.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Set HasHighLowLines property to true.
chart.Series[0].SerieFormat.CommonSerieOptions.HasHighLowLines = true;

//Apply formats to HighLowLines.
 chart.Series[0].SerieFormat.CommonSerieOptions.HighLowLines.LineColor = Syncfusion.Drawing.Color.Red;
 chart.Series[0].SerieFormat.CommonSerieOptions.HighLowLines.LinePattern = OfficeChartLinePattern.Dot;
 chart.Series[0].SerieFormat.CommonSerieOptions.HighLowLines.LineWeight = OfficeChartLineWeight.Hairline;

{% endhighlight %}
{% endtabs %}

## Add Drop Lines

The following code snippet illustrates how to add drop lines.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Set HasDropLines property to true.
chart.Series[0].SerieFormat.CommonSerieOptions.HasDropLines = true;

//Apply formats to DropLines.
chart.Series[0].SerieFormat.CommonSerieOptions.DropLines.LineColor = Syncfusion.Drawing.Color.Red;
chart.Series[0].SerieFormat.CommonSerieOptions.DropLines.LinePattern = OfficeChartLinePattern.Dot;
chart.Series[0].SerieFormat.CommonSerieOptions.DropLines.LineWeight = OfficeChartLineWeight.Hairline;

{% endhighlight %}
{% endtabs %}

## Different Marker Properties

The following code snippet illustrates how to customize the marker porperties.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Set the marker style of the first series in the chart.
chart.Series[0].SerieFormat.MarkerStyle = OfficeChartMarkerType.Star;

//Customize the marker style.
chart.Series[0].SerieFormat.MarkerSize = 8;
chart.Series[0].SerieFormat.MarkerBackgroundColor = Syncfusion.Drawing.Color.Red;
chart.Series[0].SerieFormat.MarkerForegroundColor = Syncfusion.Drawing.Color.Black;

{% endhighlight %}
{% endtabs %}

## Customize the series color

The following code snippet illustrates how to customize the series color.

{% tabs %}
{% highlight c# tabtitle="C#" %}

// Configure the fill settings for the first series in the chart.
chart.Series[0].SerieFormat.Fill.FillType = OfficeFillType.Gradient;
chart.Series[0].SerieFormat.Fill.GradientColorType = OfficeGradientColor.TwoColor;
chart.Series[0].SerieFormat.Fill.BackColor = Syncfusion.Drawing.Color.FromArgb(205, 217, 234);
chart.Series[0].SerieFormat.Fill.ForeColor = Syncfusion.Drawing.Color.Red;

{% endhighlight %}
{% endtabs %}

## Customize the Border

The following code snippet illustrates how to customize the series border.

{% tabs %}
{% highlight c# tabtitle="C#" %}

chart.Series[0].SerieFormat.LineProperties.LineColor = Syncfusion.Drawing.Color.Red;
chart.Series[0].SerieFormat.LineProperties.LinePattern = OfficeChartLinePattern.CircleDot;
chart.Series[0].SerieFormat.LineProperties.LineWeight = OfficeChartLineWeight.Wide;

{% endhighlight %}
{% endtabs %}

## Resizing datalabel --->doubt

The following code snippet illustrates how to resize the data labels.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Manually resizing data label area using Layout
chart.Series[0].DataPoints[0].DataLabels.Layout.Left = 2.5;
chart.Series[0].DataPoints[0].DataLabels.Layout.Top = 0.01;

//Manually resizing data label area using Manual Layout
chart.Series[0].DataPoints[0].DataLabels.Layout.ManualLayout.Left = 0.09;
chart.Series[0].DataPoints[0].DataLabels.Layout.ManualLayout.Top = 0.01;

{% endhighlight %}
{% endtabs %}

## Explode a Pie Chart

The following code snippet illustrates how to explode a pie chart.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Exploding the pie chart to 10%.
chart.Series[0].SerieFormat.Percent = 10;

{% endhighlight %}
{% endtabs %}