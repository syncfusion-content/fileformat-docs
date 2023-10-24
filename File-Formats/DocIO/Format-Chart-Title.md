---
title: Modify the appearance of chart title | Syncfusion
description: Learn how to modify the appearance of chart title in Word document using Syncfusion .NET Core Word (DocIO) library without Microsoft Word or interop dependencies.
platform: file-formats
control: DocIO
documentation: UG
---

## Set the Chart Title Name

The following code snippet shows how to set the chart title name.

{% tabs %}
{% highlight c# tabtitle="C#" %}

// Set the chart title.
chart.ChartTitle = "Purchase Details";

{% endhighlight %}
{% endtabs %}

## Customize the Chart Title Area

The following code snippet shows how to customize the chart title.

{% tabs %}
{% highlight c# tabtitle="C#" %}

// Customize chart title area.
chart.ChartTitleArea.FontName = "Calibri";
chart.ChartTitleArea.Bold = true;
chart.ChartTitleArea.Color = OfficeKnownColors.Red;
chart.ChartTitleArea.Underline = OfficeUnderline.DashLong;

{% endhighlight %}
{% endtabs %}

## Resize the Chart Title Area

The following code snippet shows how to resize the chart title.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Manually resizing chart title area using Layout
chart.ChartTitleArea.Layout.Top = 10;
chart.ChartTitleArea.Layout.Left = 150;

//Manually resizing chart title area using Manual Layout
chart.ChartTitleArea.Layout.ManualLayout.Top = 0.005;
chart.ChartTitleArea.Layout.ManualLayout.Left = 0.26;

{% endhighlight %}
{% endtabs %}