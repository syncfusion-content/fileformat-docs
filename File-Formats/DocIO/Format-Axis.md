---
title: Modify the appearance of axes in chart | Syncfusion
description: Learn how to modify the appearance of axes in a chart using Syncfusion .NET Core Word (DocIO) library without Microsoft Word or interop dependencies.
platform: file-formats
control: DocIO
documentation: UG
---

# Chart Axis

Charts typically have two axes that are used to measure and categorize data
-  Horizontal axis (also known as category axis or x axis).
-  Vertical axis (also known as value axis or y axis).

Using Syncfusion [.NET Core Word (DocIO)](https://www.syncfusion.com/document-processing/word-framework/net-core/word-library) library you can customize the **axis** in the chart.

## Set the Axis Title

The following code snippet illustrates how to set the title in axis.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Set the horizontal (category) axis title.
chart.PrimaryCategoryAxis.Title = "Products";
//Set the Vertical (value) axis title.
chart.PrimaryValueAxis.Title = "In Dollars";

{% endhighlight %}
{% endtabs %}

## Customization of Border

The following code snippet illustrates how to customize the border of Horizontol and vertical category axis.

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

## Customization of Font

The following code snippet illustrates how to customize the border of Horizontol and vertical category axis.

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

## Text Angle Rotation

The following code snippet illustrates how to rotate the text angle for the axis title area.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Axis title area text angle rotation.
chart.PrimaryValueAxis.TitleArea.TextRotationAngle = 90;

{% endhighlight %}
{% endtabs %}

## Set the Maximum value in Axis

The following code snippet illustrates how to set the maximum value in the axis.
{% tabs %}
{% highlight c# tabtitle="C#" %}

//Maximum value in the axis
chart.PrimaryValueAxis.MaximumValue = 14.0;

{% endhighlight %}
{% endtabs %}

## Set the Number format in Axis

The following code snippet illustrates how to set the number format in the axis.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Number format for axis
chart.PrimaryValueAxis.NumberFormat = "0.0";

{% endhighlight %}
{% endtabs %}

## Set the Category Label

The following code snippet illustrates how to set the category label.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Sets category labels
chart.PrimaryCategoryAxis.CategoryLabels = chart.ChartData[2, 1, 11, 1];

{% endhighlight %}
{% endtabs %}

## Manage Gridline Visibility

The following code snippet illustrates how to hide or show major and minor gridlines.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Hiding major gridlines
chart.PrimaryValueAxis.HasMajorGridLines = false;

//Showing minor gridlines
chart.PrimaryValueAxis.HasMinorGridLines = true;

{% endhighlight %}
{% endtabs %}

## Resize the Axis Title Area

The following code snippet illustrates how to resize the axis title area.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Manually resizing axis title area using Layout
chart.PrimaryValueAxis.TitleArea.Layout.Left = 15;
chart.PrimaryValueAxis.TitleArea.Layout.Top = 20;
chart.PrimaryCategoryAxis.TitleArea.Layout.Left = 25;
chart.PrimaryCategoryAxis.TitleArea.Layout.Top = 20;

//Manually resizing axis title area using Manual Layout
chart.PrimaryValueAxis.TitleArea.Layout.ManualLayout.Left = 0.04;
chart.PrimaryValueAxis.TitleArea.Layout.ManualLayout.Top = 0.34;
chart.PrimaryCategoryAxis.TitleArea.Layout.ManualLayout.Left = 0.38;
chart.PrimaryCategoryAxis.TitleArea.Layout.ManualLayout.Top = 0.95;

{% endhighlight %}
{% endtabs %}

## Set the Secondary Axis

The following code snippet illustrates how to use secondary axis in chart.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Use Secondary Axis
chart.Series[1].UsePrimaryAxis = false;

//Set title for secondary value axis
chart.SecondaryValueAxis.Title = "Temperature,deg.F";

{% endhighlight %}
{% endtabs %}

## Secondary Value Properties

The following code snippet illustrates how to customize secondary value axis in chart.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//MaxCross in axis
chart.SecondaryValueAxis.IsMaxCross = true;

//Axis title
chart.SecondaryValueAxis.Title = "Temperature,deg.F";

//Axis title area text angle rotation
chart.SecondaryValueAxis.TitleArea.TextRotationAngle = 90;

{% endhighlight %}
{% endtabs %}

## Secondary Category Properties

The following code snippet illustrates how to customize secondary category axis in chart.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//MaxCross in axis
chart.SecondaryCategoryAxis.IsMaxCross = true;

//Select border line color
chart.SecondaryCategoryAxis.Border.LineColor = Syncfusion.Drawing.Color.Transparent;

//Select major tick mark option
chart.SecondaryCategoryAxis.MajorTickMark = OfficeTickMark.TickMark_Cross;

//Select tick label position
chart.SecondaryCategoryAxis.TickLabelPosition = OfficeTickLabelPosition.TickLabelPosition_None;

{% endhighlight %}
{% endtabs %}