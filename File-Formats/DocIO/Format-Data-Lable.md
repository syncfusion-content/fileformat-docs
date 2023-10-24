---
title: Modify the appearance of Data labels | Syncfusion
description: Learn how to modify the appearance of Data labels in Word document using Syncfusion .NET Core Word (DocIO) library without Microsoft Word or interop dependencies.
platform: file-formats
control: DocIO
documentation: UG
---

# Data Labels

Data labels play a crucial role in enhancing the comprehensibility of a chart. By displaying specific information related to a data series or individual data points, **data labels** provide valuable context. Using Syncfusion [.NET Core Word (DocIO)](https://www.syncfusion.com/document-processing/word-framework/net-core/word-library) library you can customize the legend in the chart.

## Enable Data Labels in chart
The following code snippet shows how to visible the data lable in chart.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Enable the datalabel in chart.
chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.IsValue = true;

{% endhighlight %}
{% endtabs %}

## Customize the data labels
The following code snippet shows how to customize the data lable in chart.

{% tabs %}
{% highlight c# tabtitle="C#" %}

// Set the font size of the data labels
chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.Size = 8;
// Change the color of the data labels 
chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.Color = OfficeKnownColors.Red;
// Make the data labels bold
chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.Bold = true;
// Set the font name for the data labels
chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.FontName = "calibri";
// Make the data labels italic
chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.Italic = true;
// Set the size of the data labels
chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.Size = 3;

{% endhighlight %}
{% endtabs %}

## Position of data labels
The following code snippet shows how to set the position of the data lable in chart.

{% tabs %}
{% highlight c# tabtitle="C#" %}

// Set the position of data labels for the first series.
chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.Position = OfficeDataLabelPosition.Center;


{% endhighlight %}
{% endtabs %}