---
title: Modify the appearance of plot area | Syncfusion
description: Learn how to modify the appearance of plot area in Word document using Syncfusion .NET Core Word (DocIO) library without Microsoft Word or interop dependencies.
platform: file-formats
control: DocIO
documentation: UG
---

# Plot Area

The plot area refers to the region that represents the plotted data in a chart. Using Syncfusion [.NET Core Word (DocIO)](https://www.syncfusion.com/document-processing/word-framework/net-core/word-library) library you can customize the **plot area** in the chart.

## Customization of Border

The following code snippet shows how to modify the border of the plot area.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Format the Plot Area.
IOfficeChartFrameFormat chartPlotArea = chart.PlotArea;
//Plots area border settings - line pattern, color, weight
chartPlotArea.Border.LinePattern = OfficeChartLinePattern.Solid;
chartPlotArea.Border.LineColor = Syncfusion.Drawing.Color.Blue;
chartPlotArea.Border.LineWeight = OfficeChartLineWeight.Hairline;

{% endhighlight %}
{% endtabs %}

## Customization of Color

The following code snippet shows how to fill the color in plot area.

{% tabs %}
{% highlight c# tabtitle="C#" %}

 //Sets fill type and color
 chartPlotArea.Fill.FillType = OfficeFillType.Gradient;
 chartPlotArea.Fill.GradientColorType = OfficeGradientColor.TwoColor;
 chartPlotArea.Fill.BackColor = Syncfusion.Drawing.Color.FromArgb(205, 217, 234);
 chartPlotArea.Fill.ForeColor = Syncfusion.Drawing.Color.White;

{% endhighlight %}
{% endtabs %}

## Add Image in Plot Area

The following code snippet shows how to fill the image in plot area.

{% tabs %}
{% highlight c# tabtitle="C#" %}

FileStream imageStream = new FileStream("Data/Image.png", FileMode.Open, FileAccess.Read);
Image image = Image.FromStream(imageStream);
chartPlotArea.Fill.UserPicture(image, "image");

{% endhighlight %}
{% endtabs %}

## Set the Transparency level

The following code snippet shows how to make transparency in plot area.

{% tabs %}
{% highlight c# tabtitle="C#" %}

// Set the transparency of the plot area.
chartPlotArea.Fill.Transparency = 0.5;

{% endhighlight %}
{% endtabs %}

N> [Transparency](https://help.syncfusion.com/cr/file-formats/Syncfusion.OfficeChart.IOfficeFill.html#Syncfusion_OfficeChart_IOfficeFill_Transparency) is only applicable when [FillType](https://help.syncfusion.com/cr/file-formats/Syncfusion.OfficeChart.IOfficeFill.html#Syncfusion_OfficeChart_IOfficeFill_FillType) is set as SolidColor. Color-shaded fill is represented as a floating-point value ranging from 0.0 (Clear) to 1.0 (Opaque).

## Set the position of Plot Area

The following code snippet shows how to make transparency in plot area.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Sets position for plot area
chartPlotArea.Layout.LeftMode = LayoutModes.auto;
chartPlotArea.Layout.TopMode = LayoutModes.factor;
chartPlotArea.Layout.LayoutTarget = LayoutTargets.outer;

{% endhighlight %}
{% endtabs %}

The complete code snippet illustrating the above options is shown below.

{% tabs %}
{% highlight c# tabtitle="C#" %}

FileStream fileStreamPath = new FileStream(Path.GetFullPath(@"../../../Data/Template.docx"), FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx))
{
    //Gets the paragraph
    WParagraph paragraph = document.LastParagraph;
    //Gets the chart entity
    WChart chart = paragraph.ChildEntities[0] as WChart;
    //Modifies the chart height and width
    chart.Height = 300;
    chart.Width = 500;
    //Changes the title
    chart.ChartTitle = "New title";
    //Changes the series name of first chart series
    chart.Series[0].Name = "Modified series name";
    //Plots Area
    IOfficeChartFrameFormat chartPlotArea = chart.PlotArea;
    //Plots area border settings - line pattern, color, weight
    chartPlotArea.Border.LinePattern = OfficeChartLinePattern.Solid;
    chartPlotArea.Border.LineColor = Syncfusion.Drawing.Color.Blue;
    chartPlotArea.Border.LineWeight = OfficeChartLineWeight.Hairline;
    //Sets fill type and color
    chartPlotArea.Fill.FillType = OfficeFillType.Gradient;
    chartPlotArea.Fill.GradientColorType = OfficeGradientColor.TwoColor;
    chartPlotArea.Fill.BackColor = Syncfusion.Drawing.Color.FromArgb(205, 217, 234);
    chartPlotArea.Fill.ForeColor = Syncfusion.Drawing.Color.White;
    using (FileStream outputStream = new FileStream(Path.GetFullPath(@"../../../Sample.docx"), FileMode.Create, FileAccess.ReadWrite, FileShare.ReadWrite))
    {
        //Save the Word file.
        document.Save(outputStream, FormatType.Docx);
    }
}

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from GitHub.