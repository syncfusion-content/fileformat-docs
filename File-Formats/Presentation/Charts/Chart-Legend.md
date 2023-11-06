---
title: Modify the Appearance of Legend | Syncfusion
description: Learn how to modify the appearance of legend in a chart in a PowerPoint using .NET PowerPoint library (Presentation) without Microsoft PowerPoint.
platform: file-formats
control: PowerPoint
documentation: UG
---

# Chart Legend

Legends are visual pictorial hints that provide a viewer information that helps them understand an chart. Using Presentation, you can **customize the legend in the chart**.

## Set the Position of Legend

The following code snippet illustrates how to set the legend position in chart.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//Set the position of legend.
chart.Legend.Position = OfficeLegendPosition.Bottom;

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

//Set the position of legend.
chart.Legend.Position = OfficeLegendPosition.Bottom;

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Set the position of legend.
chart.Legend.Position = OfficeLegendPosition.Bottom

{% endhighlight %}
{% endtabs %}

## Set the layout Inclusion

The following code snippet illustrates how to prevent the overlapping the legend in chart.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//Legend without overlapping the chart.
 chart.Legend.IncludeInLayout = true;

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

//Set the position of legend.
chart.Legend.Position = OfficeLegendPosition.Bottom;

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Set the position of legend.
chart.Legend.Position = OfficeLegendPosition.Bottom

{% endhighlight %}
{% endtabs %}

## Customization of Border

The following code snippet illustrates how to modify the border of the legend in chart.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//Sets the legend border format - color, pattern, weight.
chart.Legend.FrameFormat.Border.AutoFormat = false;
chart.Legend.FrameFormat.Border.IsAutoLineColor = false;
chart.Legend.FrameFormat.Border.LineColor = Syncfusion.Drawing.Color.Blue;
chart.Legend.FrameFormat.Border.LinePattern = OfficeChartLinePattern.DashDot;
chart.Legend.FrameFormat.Border.LineWeight = OfficeChartLineWeight.Wide;

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

//Sets the legend border format - color, pattern, weight.
chart.Legend.FrameFormat.Border.AutoFormat = false;
chart.Legend.FrameFormat.Border.IsAutoLineColor = false;
chart.Legend.FrameFormat.Border.LineColor = Color.Blue;
chart.Legend.FrameFormat.Border.LinePattern = OfficeChartLinePattern.DashDot;
chart.Legend.FrameFormat.Border.LineWeight = OfficeChartLineWeight.Wide;

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Sets the legend border format - color, pattern, weight.
chart.Legend.FrameFormat.Border.AutoFormat = False
chart.Legend.FrameFormat.Border.IsAutoLineColor = False
chart.Legend.FrameFormat.Border.LineColor = Color.Blue
chart.Legend.FrameFormat.Border.LinePattern = OfficeChartLinePattern.DashDot
chart.Legend.FrameFormat.Border.LineWeight = OfficeChartLineWeight.Wide

{% endhighlight %}
{% endtabs %}

## Customization of Text Area

The following code snippet illustrates how to modify the text area of the legend in chart.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//Set the legend's text area formatting - font name, weight, color, size.
chart.Legend.TextArea.Bold = true;
chart.Legend.TextArea.Color = OfficeKnownColors.Bright_green;
chart.Legend.TextArea.FontName = "Times New Roman";
chart.Legend.TextArea.Size = 20;
chart.Legend.TextArea.Strikethrough = true;

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

//Set the legend's text area formatting - font name, weight, color, size.
chart.Legend.TextArea.Bold = true;
chart.Legend.TextArea.Color = OfficeKnownColors.Bright_green;
chart.Legend.TextArea.FontName = "Times New Roman";
chart.Legend.TextArea.Size = 20;
chart.Legend.TextArea.Strikethrough = true;

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Set the legend's text area formatting - font name, weight, color, size.
chart.Legend.TextArea.Bold = True
chart.Legend.TextArea.Color = OfficeKnownColors.Bright_green
chart.Legend.TextArea.FontName = "Times New Roman"
chart.Legend.TextArea.Size = 20
chart.Legend.TextArea.Strikethrough = True

{% endhighlight %}
{% endtabs %}

## Modify the Legend Entry

The following code snippet illustrates how to modify the legend entry.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//Modify the legend entry.
chart.Legend.LegendEntries[0].IsDeleted = true;

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

//Modify the legend entry.
chart.Legend.LegendEntries[0].IsDeleted = true;

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Modify the legend entry.
chart.Legend.LegendEntries(0).IsDeleted = True

{% endhighlight %}
{% endtabs %}


## Manage Legend Visibility

The following code snippet illustrates how to hide the legend in chart.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//Hiding the legend.
chart.HasLegend = false;

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

//Hiding the legend.
chart.HasLegend = false;

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Hiding the legend.
chart.HasLegend = False

{% endhighlight %}
{% endtabs %}

## View the Legend Horizontally

The following code snippet illustrates how to view legend horizontally.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//View legend horizontally.
chart.Legend.IsVerticalLegend = false;

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

//View legend horizontally.
chart.Legend.IsVerticalLegend = false;

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' View legend horizontally.
chart.Legend.IsVerticalLegend = False

{% endhighlight %}
{% endtabs %}

## Set the Position using Layout

The following code snippet illustrates how to position the legend using layout.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//Manually positioning chart legend area using Layout.
chart.Legend.Layout.LeftMode = LayoutModes.edge;
chart.Legend.Layout.TopMode = LayoutModes.edge;

//Manually positioning chart legend area using Manual Layout.
chart.Legend.Layout.ManualLayout.LeftMode = LayoutModes.edge;
chart.Legend.Layout.ManualLayout.TopMode = LayoutModes.edge;

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

//Manually positioning chart legend area using Layout.
chart.Legend.Layout.LeftMode = LayoutModes.edge;
chart.Legend.Layout.TopMode = LayoutModes.edge;

//Manually positioning chart legend area using Manual Layout.
chart.Legend.Layout.ManualLayout.LeftMode = LayoutModes.edge;
chart.Legend.Layout.ManualLayout.TopMode = LayoutModes.edge;

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Manually positioning chart legend area using Layout.
chart.Legend.Layout.LeftMode = LayoutModes.Edge
chart.Legend.Layout.TopMode = LayoutModes.Edge

' Manually positioning chart legend area using Manual Layout.
chart.Legend.Layout.ManualLayout.LeftMode = LayoutModes.Edge
chart.Legend.Layout.ManualLayout.TopMode = LayoutModes.Edge

{% endhighlight %}
{% endtabs %}


## Resize the Legend

The following code snippet illustrates how to resize the legend in chart.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

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
{% highlight c# tabtitle="C# [Windows-specific]" %}

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
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Manually resizing chart legend area using Layout.
chart.Legend.Layout.Left = 400
chart.Legend.Layout.Top = 150
chart.Legend.Layout.Width = 150
chart.Legend.Layout.Height = 100

' Manually resizing chart legend area using Manual Layout.
chart.Legend.Layout.ManualLayout.Height = 0.09
chart.Legend.Layout.ManualLayout.Width = 0.30
chart.Legend.Layout.ManualLayout.Top = 0.36
chart.Legend.Layout.ManualLayout.Left = 0.68

{% endhighlight %}
{% endtabs %}

The complete code snippet illustrating the above options is shown below.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

 FileStream fileStreamPath = new FileStream("Data/Template.pptx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
 //Open an existing PowerPoint Presentation.
 using (IPresentation pptxDoc = Presentation.Open(fileStreamPath))
 {
     //Gets the first slide.
     ISlide slide = pptxDoc.Slides[0];
     //Gets the chart in slide.
     IPresentationChart chart = slide.Shapes[0] as IPresentationChart;

     //Enable the legend.
     chart.HasLegend = true;

     //Set the position of legend.
     chart.Legend.Position = OfficeLegendPosition.Right;

     //Legend without overlapping the chart.
     chart.Legend.IncludeInLayout = true;
     chart.Legend.FrameFormat.Border.AutoFormat = false;
     chart.Legend.FrameFormat.Border.IsAutoLineColor = false;
     chart.Legend.FrameFormat.Border.LineColor = Syncfusion.Drawing.Color.Black;
     chart.Legend.FrameFormat.Border.LinePattern = OfficeChartLinePattern.DashDot;
     chart.Legend.FrameFormat.Border.LineWeight = OfficeChartLineWeight.Hairline;

     //Set the legend's text area formatting - font name, weight, color, size.
     chart.Legend.TextArea.Bold = true;
     chart.Legend.TextArea.Color = OfficeKnownColors.Pink;
     chart.Legend.TextArea.FontName = "Times New Roman";
     chart.Legend.TextArea.Size = 10;
     chart.Legend.TextArea.Strikethrough = false;

     //View legend in vertical.
     chart.Legend.IsVerticalLegend = true;

     //Modifies the legend entry.
     chart.Legend.LegendEntries[0].IsDeleted = true;

     //Manually resizing chart legend area using Layout.
     chart.Legend.Layout.Left = 0.2;
     chart.Legend.Layout.Top = 5;
     chart.Legend.Layout.Width = 40;
     chart.Legend.Layout.Height = 40;

     //Legend without overlapping the chart.
     chart.Legend.IncludeInLayout = true;

     using (FileStream outputStream = new FileStream("Result.pptx", FileMode.Create, FileAccess.ReadWrite, FileShare.ReadWrite))
     {
         //Save the PowerPoint Presentation.
         pptxDoc.Save(outputStream);
     }
 }

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

 //Open an existing PowerPoint Presentation.
 using (IPresentation pptxDoc = Presentation.Open("Template.pptx"))
 {
     //Gets the first slide.
     ISlide slide = pptxDoc.Slides[0];
     //Gets the chart in slide.
     IPresentationChart chart = slide.Shapes[0] as IPresentationChart;

     //Enable the legend.
     chart.HasLegend = true;

     //Set the position of legend.
     chart.Legend.Position = OfficeLegendPosition.Right;

     //Legend without overlapping the chart.
     chart.Legend.IncludeInLayout = true;
     chart.Legend.FrameFormat.Border.AutoFormat = false;
     chart.Legend.FrameFormat.Border.IsAutoLineColor = false;
     chart.Legend.FrameFormat.Border.LineColor = Syncfusion.Drawing.Color.Black;
     chart.Legend.FrameFormat.Border.LinePattern = OfficeChartLinePattern.DashDot;
     chart.Legend.FrameFormat.Border.LineWeight = OfficeChartLineWeight.Hairline;

     //Set the legend's text area formatting - font name, weight, color, size.
     chart.Legend.TextArea.Bold = true;
     chart.Legend.TextArea.Color = OfficeKnownColors.Pink;
     chart.Legend.TextArea.FontName = "Times New Roman";
     chart.Legend.TextArea.Size = 10;
     chart.Legend.TextArea.Strikethrough = false;

     //View legend in vertical.
     chart.Legend.IsVerticalLegend = true;

     //Modifies the legend entry.
     chart.Legend.LegendEntries[0].IsDeleted = true;

     //Manually resizing chart legend area using Layout.
     chart.Legend.Layout.Left = 0.2;
     chart.Legend.Layout.Top = 5;
     chart.Legend.Layout.Width = 40;
     chart.Legend.Layout.Height = 40;

     //Legend without overlapping the chart.
     chart.Legend.IncludeInLayout = true;

    //Save the PowerPoint Presentation.
    pptxDoc.Save("Result.pptx");
 }

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Open an existing PowerPoint Presentation.
Using pptxDoc As IPresentation = Presentation.Open("Template.pptx")
    ' Gets the first slide.
    Dim slide As ISlide = pptxDoc.Slides(0)
    ' Gets the chart in the slide.
    Dim chart As IPresentationChart = TryCast(slide.Shapes(0), IPresentationChart)

    ' Enable the legend.
    chart.HasLegend = True

    ' Set the position of the legend.
    chart.Legend.Position = OfficeLegendPosition.Right

    ' Legend without overlapping the chart.
    chart.Legend.IncludeInLayout = True
    chart.Legend.FrameFormat.Border.AutoFormat = False
    chart.Legend.FrameFormat.Border.IsAutoLineColor = False
    chart.Legend.FrameFormat.Border.LineColor = Syncfusion.Drawing.Color.Black
    chart.Legend.FrameFormat.Border.LinePattern = OfficeChartLinePattern.DashDot
    chart.Legend.FrameFormat.Border.LineWeight = OfficeChartLineWeight.Hairline

    ' Set the legend's text area formatting - font name, weight, color, size.
    chart.Legend.TextArea.Bold = True
    chart.Legend.TextArea.Color = OfficeKnownColors.Pink
    chart.Legend.TextArea.FontName = "Times New Roman"
    chart.Legend.TextArea.Size = 10
    chart.Legend.TextArea.Strikethrough = False

    ' View legend in vertical.
    chart.Legend.IsVerticalLegend = True

    ' Modifies the legend entry.
    chart.Legend.LegendEntries(0).IsDeleted = True

    ' Manually resizing chart legend area using Layout.
    chart.Legend.Layout.Left = 0.2
    chart.Legend.Layout.Top = 5
    chart.Legend.Layout.Width = 40
    chart.Legend.Layout.Height = 40

    ' Legend without overlapping the chart.
    chart.Legend.IncludeInLayout = True

    ' Save the PowerPoint Presentation.
    pptxDoc.Save("Result.pptx")
End Using

{% endhighlight %}
{% endtabs %}
