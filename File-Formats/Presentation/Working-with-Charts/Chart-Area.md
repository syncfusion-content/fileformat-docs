---
title: Modify the Appearance of Chart Area | Syncfusion
description: Learn how to modify the appearance of chart area in a chart in a PowerPoint using .NET PowerPoint library (Presentation) without Microsoft PowerPoint.
platform: file-formats
control: PowerPoint
documentation: UG
---

# Chart Area

Chart area refers to the space that contains the chart or graph you've inserted into a document. It includes the entire chart and all its elements, such as data points, labels, axes, and the plot area. Using Presentation, you can **customize the chart area in the chart**.

## Customization of Border

The following code snippet illustrates how to modify the border of the chart area.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//Format the chart area.
IOfficeChartFrameFormat chartArea = chart.ChartArea;
//Set border line pattern, color, line weight.
chartArea.Border.LinePattern = OfficeChartLinePattern.Solid;
chartArea.Border.LineColor = Syncfusion.Drawing.Color.Blue;
chartArea.Border.LineWeight = OfficeChartLineWeight.Hairline;

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

//Format the chart area.
IOfficeChartFrameFormat chartArea = chart.ChartArea;
//Set border line pattern, color, line weight.
chartArea.Border.LinePattern = OfficeChartLinePattern.Solid;
chartArea.Border.LineColor = Color.Blue;
chartArea.Border.LineWeight = OfficeChartLineWeight.Hairline;

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Format the chart area.
Dim chartArea As IOfficeChartFrameFormat = chart.ChartArea
' Set border line pattern, color, line weight.
chartArea.Border.LinePattern = OfficeChartLinePattern.Solid
chartArea.Border.LineColor = Color.Blue
chartArea.Border.LineWeight = OfficeChartLineWeight.Hairline

{% endhighlight %}
{% endtabs %}

## Customization of Color

The following code snippet illustrates how to fill the color in chart area.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//Set fill type and fill colors.
chartArea.Fill.FillType = OfficeFillType.Gradient;
chartArea.Fill.GradientColorType = OfficeGradientColor.TwoColor;
chartArea.Fill.BackColor = Syncfusion.Drawing.Color.FromArgb(205, 217, 234);
chartArea.Fill.ForeColor = Syncfusion.Drawing.Color.White;

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

//Set fill type and fill colors.
chartArea.Fill.FillType = OfficeFillType.Gradient;
chartArea.Fill.GradientColorType = OfficeGradientColor.TwoColor;
chartArea.Fill.BackColor = Color.FromArgb(205, 217, 234);
chartArea.Fill.ForeColor = Color.White;

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Set fill type and fill colors.
chartArea.Fill.FillType = OfficeFillType.Gradient
chartArea.Fill.GradientColorType = OfficeGradientColor.TwoColor
chartArea.Fill.BackColor = Color.FromArgb(205, 217, 234)
chartArea.Fill.ForeColor = Color.White

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

    //Format the chart area.
    IOfficeChartFrameFormat chartArea = chart.ChartArea;

    //Set border line pattern, color, line weight.
    chartArea.Border.LinePattern = OfficeChartLinePattern.Solid;
    chartArea.Border.LineColor = Syncfusion.Drawing.Color.Blue;
    chartArea.Border.LineWeight = OfficeChartLineWeight.Hairline;

    //Set fill type and fill colors.
    chartArea.Fill.FillType = OfficeFillType.Gradient;
    chartArea.Fill.GradientColorType = OfficeGradientColor.TwoColor;
    chartArea.Fill.BackColor = Syncfusion.Drawing.Color.FromArgb(205, 217, 234);
    chartArea.Fill.ForeColor = Syncfusion.Drawing.Color.White;

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

    //Format the chart area.
    IOfficeChartFrameFormat chartArea = chart.ChartArea;

    //Set border line pattern, color, line weight.
    chartArea.Border.LinePattern = OfficeChartLinePattern.Solid;
    chartArea.Border.LineColor = Syncfusion.Drawing.Color.Blue;
    chartArea.Border.LineWeight = OfficeChartLineWeight.Hairline;

    //Set fill type and fill colors.
    chartArea.Fill.FillType = OfficeFillType.Gradient;
    chartArea.Fill.GradientColorType = OfficeGradientColor.TwoColor;
    chartArea.Fill.BackColor = Syncfusion.Drawing.Color.FromArgb(205, 217, 234);
    chartArea.Fill.ForeColor = Syncfusion.Drawing.Color.White;

    //Save the PowerPoint Presentation.
    pptxDoc.Save("Result.pptx");
}

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Load an existing PowerPoint presentation.
    Using pptxDoc As IPresentation = Presentation.Open("Template.pptx")
    ' Get the first slide.
    Dim slide As ISlide = pptxDoc.Slides(0)
    ' Get the chart in the slide.
    Dim chart As IPresentationChart = TryCast(slide.Shapes(0), IPresentationChart)

    ' Format the chart area.
    Dim chartArea As IOfficeChartFrameFormat = chart.ChartArea

    ' Set border line pattern, color, and line weight.
    chartArea.Border.LinePattern = OfficeChartLinePattern.Solid
    chartArea.Border.LineColor = Color.Blue
    chartArea.Border.LineWeight = OfficeChartLineWeight.Hairline

    ' Set fill type and fill colors.
    chartArea.Fill.FillType = OfficeFillType.Gradient
    chartArea.Fill.GradientColorType = OfficeGradientColor.TwoColor
    chartArea.Fill.BackColor = Color.FromArgb(205, 217, 234)
    chartArea.Fill.ForeColor = Color.White

    ' Save the PowerPoint presentation.
    pptxDoc.Save("Result.pptx")
End Using

{% endhighlight %}
{% endtabs %}

## Add Image in Chart Area

The following code snippet illustrates how to fill the image in chart area.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//Append image in chart area.
FileStream imageStream = new FileStream("Data/Image.png", FileMode.Open, FileAccess.Read);
Image image = Image.FromStream(imageStream);
chartArea.Fill.UserPicture(image, "image");

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

//Append image in chart area.
chartArea.Fill.UserPicture("Image.png");

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Append an image to the chart area.
chartArea.Fill.UserPicture("Image.png")

{% endhighlight %}
{% endtabs %}

## Set the Transparency level

The following code snippet illustrates how to make transparency in chart area.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

// Set the transparency of the chart area.
chartArea.Fill.Transparency = 0.5;

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

// Set the transparency of the chart area.
chartArea.Fill.Transparency = 0.5;

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Set the transparency of the chart area.
chartArea.Fill.Transparency = 0.5

{% endhighlight %}
{% endtabs %}

N> [Transparency](https://help.syncfusion.com/cr/file-formats/Syncfusion.OfficeChart.IOfficeFill.html#Syncfusion_OfficeChart_IOfficeFill_Transparency) is only applicable when [FillType](https://help.syncfusion.com/cr/file-formats/Syncfusion.OfficeChart.IOfficeFill.html#Syncfusion_OfficeChart_IOfficeFill_FillType) is set as SolidColor. Color-shaded fill is represented as a floating-point value ranging from 0.0 (Clear) to 1.0 (Opaque).

