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
The following code snippet shows how to set the series name in chart.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Set name to chart series.
chart.Series[0].Name = "Sum of Purchases";

{% endhighlight %}
{% endtabs %}

## Set the series type

The following code snippet shows how to set the series type.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Sets series type 
chart.Series[0].SerieType = OfficeChartType.Line_Markers;

{% endhighlight %}
{% endtabs %}

## Set the DataPoint as Total
The following code snippet shows how to set the Data Point as toal in chart.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Data point settings as total in chart.
chart.Series[0].DataPoints[3].SetAsTotal = true;
chart.Series[0].DataPoints[6].SetAsTotal = true;

{% endhighlight %}
{% endtabs %}

## Set the connector lines between data points. 

The following code snippet shows how to set the connector lines between data points. 

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Showing the connector lines between data points.
chart.Series[0].SerieFormat.ShowConnectorLines = true;

{% endhighlight %}
{% endtabs %}

## Customize the Data label

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Enable the datalabel in chart.
chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.IsValue = true;
//Set the datalabel size.
chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.Size = 8;

{% endhighlight %}
{% endtabs %}