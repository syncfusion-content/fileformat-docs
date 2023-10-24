---
title: Modify the appearance of legend | Syncfusion
description: Learn how to modify the appearance of legend in Word document using Syncfusion .NET Core Word (DocIO) library without Microsoft Word or interop dependencies.
platform: file-formats
control: DocIO
documentation: UG
---

# Legend

Legends are visual **pictorial** hints that provide a viewer information that helps them understand an chart. Using Syncfusion [.NET Core Word (DocIO)](https://www.syncfusion.com/document-processing/word-framework/net-core/word-library) library you can customize the legend in the chart.

## Set the position of Legend

The following code snippet illustrates how to set the legend position in chart.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Set the position of legend.
chart.Legend.Position = OfficeLegendPosition.Bottom;

{% endhighlight %}
{% endtabs %}

## Set the layout inclusion

The following code snippet illustrates how to check if the legends are overlapping with the chart space or not.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Legend without overlapping the chart.
 chart.Legend.IncludeInLayout = true;

{% endhighlight %}
{% endtabs %}

## Customization of border

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

## Customization of text area

The following code snippet illustrates how to modify the text area of the legend in chart.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Sets the legend's text area formatting - font name, weight, color, size.
chart.Legend.TextArea.Bold = true;
chart.Legend.TextArea.Color = OfficeKnownColors.Bright_green;
chart.Legend.TextArea.FontName = "Times New Roman";
chart.Legend.TextArea.Size = 20;
chart.Legend.TextArea.Strikethrough = true;

{% endhighlight %}
{% endtabs %}

## Modify the legend Entry

The following code snippet illustrates how to modify the legend entry.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Modifies the legend entry.
chart.Legend.LegendEntries[0].IsDeleted = true;

{% endhighlight %}
{% endtabs %}

## Modify the legend layout 
The following code snippet illustrates how to modify the legend layout.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Modifies the legend layout - height, left, top, width.
chart.Legend.Layout.Height = 50;
chart.Legend.Layout.HeightMode = LayoutModes.factor;
chart.Legend.Layout.Left = 10;
chart.Legend.Layout.LeftMode = LayoutModes.factor;
chart.Legend.Layout.Top = 30;
chart.Legend.Layout.TopMode = LayoutModes.factor;
chart.Legend.Layout.Width = 100;
chart.Legend.Layout.WidthMode = LayoutModes.factor;

{% endhighlight %}
{% endtabs %}

## Hide Legend
The following code snippet illustrates how to hide the legend in chart.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Hiding the legend
chart.HasLegend = false;

{% endhighlight %}
{% endtabs %}

## View legend horizontally

The following code snippet illustrates how to view legend horizontally.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//View legend horizontally
chart.Legend.IsVerticalLegend = false;

{% endhighlight %}
{% endtabs %}

## Set the position using layout
The following code snippet illustrates how to position the legend using layout.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Manually positioning chart legend area using Layout
chart.Legend.Layout.LeftMode = LayoutModes.edge;
chart.Legend.Layout.TopMode = LayoutModes.edge;

//Manually positioning chart legend area using Manual Layout
chart.Legend.Layout.ManualLayout.LeftMode = LayoutModes.edge;
chart.Legend.Layout.ManualLayout.TopMode = LayoutModes.edge;

{% endhighlight %}
{% endtabs %}

## Resize the legend

The following code snippet illustrates how to resize the legend in chart.


{% tabs %}
{% highlight c# tabtitle="C#" %}

//Manually resizing chart legend area using Layout
chart.Legend.Layout.Left = 400;
chart.Legend.Layout.Top = 150;
chart.Legend.Layout.Width = 150;
chart.Legend.Layout.Height = 100;

//Manually resizing chart legend area using Manual Layout
chart.Legend.Layout.ManualLayout.Height = 0.09;
chart.Legend.Layout.ManualLayout.Width = 0.30;
chart.Legend.Layout.ManualLayout.Top = 0.36;
chart.Legend.Layout.ManualLayout.Left = 0.68;

{% endhighlight %}
{% endtabs %}
