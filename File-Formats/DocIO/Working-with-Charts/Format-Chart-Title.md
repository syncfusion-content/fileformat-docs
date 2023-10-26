---
title: Modify the Appearance of Chart Title | Syncfusion
description: Learn how to modify the appearance of chart title in a chart in a Word document using Syncfusion .NET Core Word (DocIO) library without Microsoft Word.
platform: file-formats
control: DocIO
documentation: UG
---

# Chart Title

Chart title is a concise description at the top of a chart, offering context and clarity for the data displayed. Using Syncfusion [.NET Core Word (DocIO)](https://www.syncfusion.com/document-processing/word-framework/net-core/word-library) library, you can customize the chart title in the chart.

## Set the Chart Title Name

The following code snippet illustrates how to set the chart title name.

{% tabs %}
{% highlight c# tabtitle="C#" %}

// Set the chart title.
chart.ChartTitle = "Purchase Details";

{% endhighlight %}
{% endtabs %}

## Customize the Chart Title Area

The following code snippet illustrates how to customize the chart title area.

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

The following code snippet illustrates how to resize the chart title area.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Manually resizing chart title area using Layout.
chart.ChartTitleArea.Layout.Top = 10;
chart.ChartTitleArea.Layout.Left = 150;

//Manually resizing chart title area using Manual Layout.
chart.ChartTitleArea.Layout.ManualLayout.Top = 0.005;
chart.ChartTitleArea.Layout.ManualLayout.Left = 0.26;

{% endhighlight %}
{% endtabs %}