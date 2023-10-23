---
title: Modify the appearance of chart title | Syncfusion
description: Learn how to modify the appearance of chart title in Word document using Syncfusion .NET Core Word (DocIO) library without Microsoft Word or interop dependencies.
platform: file-formats
control: DocIO
documentation: UG
---

## Set the chart title

The following code snippet shows how to set the chart title name.

{% tabs %}
{% highlight c# tabtitle="C#" %}

// Set the chart title.
chart.ChartTitle = "Purchase Details";

{% endhighlight %}
{% endtabs %}

## Customization of chart title 

The following code snippet shows how to customize the chart title.

{% tabs %}
{% highlight c# tabtitle="C#" %}

// Set the font name and size for the chart title area.
chart.ChartTitleArea.FontName = "Calibri";
chart.ChartTitleArea.Size = 14;

{% endhighlight %}
{% endtabs %}

## Set the position of chart title 

The following code snippet shows how to set the position of chart title.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Sets position for title area
chart.ChartTitleArea.Layout.Left = 10;
chart.ChartTitleArea.Layout.Top = 8;

{% endhighlight %}
{% endtabs %}