---
title: Modify the Appearance of Plot Area | Syncfusion
description: Learn how to modify the appearance of plot area in a chart in a PowerPoint using .NET PowerPoint library (Presentation) without Microsoft PowerPoint.
platform: file-formats
control: PowerPoint
documentation: UG
---

# Plot Area

The plot area refers to the region that represents the plotted data in a chart. Using Syncfusion [.NET Core PowerPoint (Presentation)](https://www.syncfusion.com/document-processing/powerpoint-framework/net-core) library you can customize the **plot area** in the chart.

## Customization of Border

The following code snippet illustrates how to modify the border of the plot area.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//Format the plot area.
IOfficeChartFrameFormat chartPlotArea = chart.PlotArea;
//Plot area border settings - line pattern, color, weight.
chartPlotArea.Border.LinePattern = OfficeChartLinePattern.Solid;
chartPlotArea.Border.LineColor = Syncfusion.Drawing.Color.Blue;
chartPlotArea.Border.LineWeight = OfficeChartLineWeight.Hairline;

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

//Format the plot area.
IOfficeChartFrameFormat chartPlotArea = chart.PlotArea;
//Plot area border settings - line pattern, color, weight.
chartPlotArea.Border.LinePattern = OfficeChartLinePattern.Solid;
chartPlotArea.Border.LineColor = Color.Blue;
chartPlotArea.Border.LineWeight = OfficeChartLineWeight.Hairline;

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Format the plot area.
Dim chartPlotArea As IOfficeChartFrameFormat = chart.PlotArea
' Plot area border settings - line pattern, color, weight.
chartPlotArea.Border.LinePattern = OfficeChartLinePattern.Solid
chartPlotArea.Border.LineColor = Color.Blue
chartPlotArea.Border.LineWeight = OfficeChartLineWeight.Hairline

{% endhighlight %}
{% endtabs %}

## Customization of Color

The following code snippet illustrates how to fill the color in plot area.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

 //Set fill type and color.
 chartPlotArea.Fill.FillType = OfficeFillType.Gradient;
 chartPlotArea.Fill.GradientColorType = OfficeGradientColor.TwoColor;
 chartPlotArea.Fill.BackColor = Syncfusion.Drawing.Color.FromArgb(205, 217, 234);
 chartPlotArea.Fill.ForeColor = Syncfusion.Drawing.Color.White;

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

 //Set fill type and color.
 chartPlotArea.Fill.FillType = OfficeFillType.Gradient;
 chartPlotArea.Fill.GradientColorType = OfficeGradientColor.TwoColor;
 chartPlotArea.Fill.BackColor = Color.FromArgb(205, 217, 234);
 chartPlotArea.Fill.ForeColor = Color.White;

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

 ' Set fill type and color.
 chartPlotArea.Fill.FillType = OfficeFillType.Gradient
 chartPlotArea.Fill.GradientColorType = OfficeGradientColor.TwoColor
 chartPlotArea.Fill.BackColor = Color.FromArgb(205, 217, 234)
 chartPlotArea.Fill.ForeColor = Color.White

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

    //Plot Area.
    IOfficeChartFrameFormat chartPlotArea = chart.PlotArea;

    //Plot area border settings - line pattern, color, weight.
    chartPlotArea.Border.LinePattern = OfficeChartLinePattern.Solid;
    chartPlotArea.Border.LineColor = Syncfusion.Drawing.Color.Blue;
    chartPlotArea.Border.LineWeight = OfficeChartLineWeight.Hairline;

    //Set fill type and color.
    chartPlotArea.Fill.FillType = OfficeFillType.Gradient;
    chartPlotArea.Fill.GradientColorType = OfficeGradientColor.TwoColor;
    chartPlotArea.Fill.BackColor = Syncfusion.Drawing.Color.FromArgb(205, 217, 234);
    chartPlotArea.Fill.ForeColor = Syncfusion.Drawing.Color.White;

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

    //Plot Area.
    IOfficeChartFrameFormat chartPlotArea = chart.PlotArea;

    //Plot area border settings - line pattern, color, weight.
    chartPlotArea.Border.LinePattern = OfficeChartLinePattern.Solid;
    chartPlotArea.Border.LineColor = Syncfusion.Drawing.Color.Blue;
    chartPlotArea.Border.LineWeight = OfficeChartLineWeight.Hairline;

    //Set fill type and color.
    chartPlotArea.Fill.FillType = OfficeFillType.Gradient;
    chartPlotArea.Fill.GradientColorType = OfficeGradientColor.TwoColor;
    chartPlotArea.Fill.BackColor = Syncfusion.Drawing.Color.FromArgb(205, 217, 234);
    chartPlotArea.Fill.ForeColor = Syncfusion.Drawing.Color.White;

    //Save the PowerPoint Presentation.
    pptxDoc.Save("Result.pptx");
}

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Open an existing PowerPoint presentation.
    Using pptxDoc As IPresentation = Presentation.Open("Template.pptx")
    ' Get the first slide.
    Dim slide As ISlide = pptxDoc.Slides(0)
    ' Get the chart in the slide.
    Dim chart As IPresentationChart = TryCast(slide.Shapes(0), IPresentationChart)

    ' Access the chart's plot area.
    Dim chartPlotArea As IOfficeChartFrameFormat = chart.PlotArea

    ' Set plot area border settings - line pattern, color, weight.
    chartPlotArea.Border.LinePattern = OfficeChartLinePattern.Solid
    chartPlotArea.Border.LineColor = Color.Blue
    chartPlotArea.Border.LineWeight = OfficeChartLineWeight.Hairline

    ' Set plot area fill type and color.
    chartPlotArea.Fill.FillType = OfficeFillType.Gradient
    chartPlotArea.Fill.GradientColorType = OfficeGradientColor.TwoColor
    chartPlotArea.Fill.BackColor = Color.FromArgb(205, 217, 234)
    chartPlotArea.Fill.ForeColor = Color.White

    ' Save the PowerPoint presentation.
    pptxDoc.Save("Result.pptx")
End Using

{% endhighlight %}
{% endtabs %}


You can download a complete working sample from GitHub.

By executing the program, you will get the **chart** as follows.

## Add Image in Plot Area

The following code snippet illustrates how to fill the image in plot area.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//Appeend image in plot area.
FileStream imageStream = new FileStream("Data/Image.png", FileMode.Open, FileAccess.Read);
Image image = Image.FromStream(imageStream);
chartPlotArea.Fill.UserPicture(image, "image");

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

//Appeend image in plot area.
chartPlotArea.Fill.UserPicture("Image.png");

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Append an image to the chart plot area.
chartPlotArea.Fill.UserPicture("Image.png")

{% endhighlight %}
{% endtabs %}

## Set the Transparency level

The following code snippet illustrates how to make transparency in plot area.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

// Set the transparency of the plot area.
chartPlotArea.Fill.Transparency = 0.5;

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

// Set the transparency of the plot area.
chartPlotArea.Fill.Transparency = 0.5;

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Set the transparency of the plot area.
chartPlotArea.Fill.Transparency = 0.5

{% endhighlight %}
{% endtabs %}

N> [Transparency](https://help.syncfusion.com/cr/file-formats/Syncfusion.OfficeChart.IOfficeFill.html#Syncfusion_OfficeChart_IOfficeFill_Transparency) is only applicable when [FillType](https://help.syncfusion.com/cr/file-formats/Syncfusion.OfficeChart.IOfficeFill.html#Syncfusion_OfficeChart_IOfficeFill_FillType) is set as SolidColor. Color-shaded fill is represented as a floating-point value ranging from 0.0 (Clear) to 1.0 (Opaque).

## Set the position of Plot Area

The following code snippet illustrates how to position the plot area in chart.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//Sets position for plot area.
chartPlotArea.Layout.LeftMode = LayoutModes.auto;
chartPlotArea.Layout.TopMode = LayoutModes.factor;
chartPlotArea.Layout.LayoutTarget = LayoutTargets.outer;

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

//Sets position for plot area.
chartPlotArea.Layout.LeftMode = LayoutModes.auto;
chartPlotArea.Layout.TopMode = LayoutModes.factor;
chartPlotArea.Layout.LayoutTarget = LayoutTargets.outer;

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Sets position for plot area.
chartPlotArea.Layout.LeftMode = LayoutModes.auto
chartPlotArea.Layout.TopMode = LayoutModes.factor
chartPlotArea.Layout.LayoutTarget = LayoutTargets.outer

{% endhighlight %}
{% endtabs %}
