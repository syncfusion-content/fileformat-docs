---
title: Modify the appearance of axis in chart | Syncfusion
description: Learn how to modify the appearance of axis in Word document using Syncfusion .NET Core Word (DocIO) library without Microsoft Word or interop dependencies.
platform: file-formats
control: DocIO
documentation: UG
---

# Chart Area

Charts typically have two axes that are used to measure and categorize data
-  Horizontal axis (also known as category axis or x axis).
-  Vertical axis (also known as value axis or y axis).

Using Syncfusion [.NET Core Word (DocIO)](https://www.syncfusion.com/document-processing/word-framework/net-core/word-library) library you can customize the axis in the chart.

## Set the axis title

The following code snippet shows how to set the title in axis.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Set the horizontal (category) axis title.
chart.PrimaryCategoryAxis.Title = "Products";
//Set the Vertical (value) axis title.
chart.PrimaryValueAxis.Title = "In Dollars";

{% endhighlight %}
{% endtabs %}

## Set the category label

The following code snippet shows how to set the category label.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Sets category labels
chart.PrimaryCategoryAxis.CategoryLabels = chart.ChartData[2, 1, 11, 1];

{% endhighlight %}
{% endtabs %}

## Customization of border

The following code snippet shows how to customize the border of Horizontol and vertical category axis.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Customize the horizontal category axis.
chart.PrimaryCategoryAxis.Border.LinePattern = OfficeChartLinePattern.CircleDot;
chart.PrimaryCategoryAxis.Border.LineColor = Syncfusion.Drawing.Color.Blue;
chart.PrimaryCategoryAxis.Border.LineWeight = OfficeChartLineWeight.Hairline;

//Customize the vertical category axis.
chart.PrimaryValueAxis.Border.LinePattern = OfficeChartLinePattern.CircleDot;
chart.PrimaryValueAxis.Border.LineColor = Syncfusion.Drawing.Color.Blue;
chart.PrimaryValueAxis.Border.LineWeight = OfficeChartLineWeight.Hairline;

{% endhighlight %}
{% endtabs %}

## Customization of font

The following code snippet shows how to customize the border of Horizontol and vertical category axis.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Customize the horizontal category axis font.
chart.PrimaryCategoryAxis.Font.Color = OfficeKnownColors.Red;
chart.PrimaryCategoryAxis.Font.FontName = "Calibri";
chart.PrimaryCategoryAxis.Font.Bold = true;
chart.PrimaryCategoryAxis.Font.Size = 20;

//Customize the vertical category axis font.
chart.PrimaryValueAxis.Font.Color = OfficeKnownColors.Red;
chart.PrimaryValueAxis.Font.FontName = "Calibri";
chart.PrimaryValueAxis.Font.Bold = true;
chart.PrimaryValueAxis.Font.Size = 20;

{% endhighlight %}
{% endtabs %}