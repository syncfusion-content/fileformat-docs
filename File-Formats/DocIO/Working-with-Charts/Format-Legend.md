---
title: Modify the Appearance of Legend | Syncfusion
description: Learn how to modify the appearance of legend in a chart in a Word document using Syncfusion .NET Core Word (DocIO) library without Microsoft Word.
platform: file-formats
control: DocIO
documentation: UG
---

# Legend

Legends are visual pictorial hints that provide a viewer information that helps them understand an chart. Using Syncfusion [.NET Core Word (DocIO)](https://www.syncfusion.com/document-processing/word-framework/net-core/word-library) library, you can customize the legend in the chart.

## Set the Position of Legend

The following code snippet illustrates how to set the legend position in chart.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Set the position of legend.
chart.Legend.Position = OfficeLegendPosition.Bottom;

{% endhighlight %}
{% endtabs %}

## Set the layout Inclusion

The following code snippet illustrates how to prevent the overlapping the legend in chart.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Legend without overlapping the chart.
 chart.Legend.IncludeInLayout = true;

{% endhighlight %}
{% endtabs %}

## Customization of Border

The following code snippet illustrates how to modify the border of the legend in chart.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Sets the legend border format - color, pattern, weight.
chart.Legend.FrameFormat.Border.AutoFormat = false;
chart.Legend.FrameFormat.Border.IsAutoLineColor = false;
chart.Legend.FrameFormat.Border.LineColor = Syncfusion.Drawing.Color.Blue;
chart.Legend.FrameFormat.Border.LinePattern = OfficeChartLinePattern.DashDot;
chart.Legend.FrameFormat.Border.LineWeight = OfficeChartLineWeight.Wide;

{% endhighlight %}
{% endtabs %}

## Customization of Text Area

The following code snippet illustrates how to modify the text area of the legend in chart.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Set the legend's text area formatting - font name, weight, color, size.
chart.Legend.TextArea.Bold = true;
chart.Legend.TextArea.Color = OfficeKnownColors.Bright_green;
chart.Legend.TextArea.FontName = "Times New Roman";
chart.Legend.TextArea.Size = 20;
chart.Legend.TextArea.Strikethrough = true;

{% endhighlight %}
{% endtabs %}

## Modify the Legend Entry

The following code snippet illustrates how to modify the legend entry.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Modify the legend entry.
chart.Legend.LegendEntries[0].IsDeleted = true;

{% endhighlight %}
{% endtabs %}

## Manage Legend Visibility

The following code snippet illustrates how to hide the legend in chart.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Hiding the legend.
chart.HasLegend = false;

{% endhighlight %}
{% endtabs %}

## View the Legend Horizontally

The following code snippet illustrates how to view legend horizontally.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//View legend horizontally.
chart.Legend.IsVerticalLegend = false;

{% endhighlight %}
{% endtabs %}

## Set the Position using Layout

The following code snippet illustrates how to position the legend using layout.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Manually positioning chart legend area using Layout.
chart.Legend.Layout.LeftMode = LayoutModes.edge;
chart.Legend.Layout.TopMode = LayoutModes.edge;

//Manually positioning chart legend area using Manual Layout.
chart.Legend.Layout.ManualLayout.LeftMode = LayoutModes.edge;
chart.Legend.Layout.ManualLayout.TopMode = LayoutModes.edge;

{% endhighlight %}
{% endtabs %}

## Resize the Legend

The following code snippet illustrates how to resize the legend in chart.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Manually resizing chart legend area using Layout.
chart.Legend.Layout.Left = 400;
chart.Legend.Layout.Top = 150;
chart.Legend.Layout.Width = 150;
chart.Legend.Layout.Height = 100;

//Manually resizing chart legend area using Manual Layout.
chart.Legend.Layout.ManualLayout.Height = 0.09;
chart.Legend.Layout.ManualLayout.Width = 0.30;
chart.Legend.Layout.ManualLayout.Top = 0.36;
chart.Legend.Layout.ManualLayout.Left = 0.68;

{% endhighlight %}
{% endtabs %}
