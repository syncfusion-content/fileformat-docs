---
title: Modify the appearance of chart area | Syncfusion
description: : Learn how to modify the appearance of chart area in Word document using Syncfusion .NET Core Word (DocIO) library without Microsoft Word or interop dependencies.
platform: file-formats
control: PowerPoint
documentation: UG
---

# Chart Area

Chart area refers to the space that contains the chart or graph you've inserted into a slide. It includes the entire chart and all its elements, such as data points, labels, axes, and the plot area. Using Syncfusion [.NET Core Word (DocIO)](https://www.syncfusion.com/document-processing/word-framework/net-core/word-library) library you can customize the chart area in the chart.

## Customization of border
The following code snippet shows how to modify the border of the chart area.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Formats the chart area.
IOfficeChartFrameFormat chartArea = chart.ChartArea;
//Sets border line pattern, color, line weight
chartArea.Border.LinePattern = OfficeChartLinePattern.Solid;
chartArea.Border.LineColor = Syncfusion.Drawing.Color.Blue;
chartArea.Border.LineWeight = OfficeChartLineWeight.Hairline;

{% endhighlight %}
{% endtabs %}

## Customization of color

The following code snippet shows how to fill the color in chart area.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Sets fill type and fill colors
chartArea.Fill.FillType = OfficeFillType.Gradient;
chartArea.Fill.GradientColorType = OfficeGradientColor.TwoColor;
chartArea.Fill.BackColor = Syncfusion.Drawing.Color.FromArgb(205, 217, 234);
chartArea.Fill.ForeColor = Syncfusion.Drawing.Color.White;

{% endhighlight %}
{% endtabs %}

## Add Image in Chart area

The following code snippet shows how to fill the image in chart area.

{% tabs %}
{% highlight c# tabtitle="C#" %}

FileStream imageStream = new FileStream("Data/Image.png", FileMode.Open, FileAccess.Read);
Image image = Image.FromStream(imageStream);
chartArea.Fill.UserPicture(image, "image");

{% endhighlight %}
{% endtabs %}

## Set the transparency level

The following code snippet shows how to make transparency in chart area.

{% tabs %}
{% highlight c# tabtitle="C#" %}

chartArea.Fill.Transparency = 0.5;

{% endhighlight %}
{% endtabs %}

N> [Transparency](https://help.syncfusion.com/cr/file-formats/Syncfusion.OfficeChart.IOfficeFill.html#Syncfusion_OfficeChart_IOfficeFill_Transparency) is only applicable when [FillType](https://help.syncfusion.com/cr/file-formats/Syncfusion.OfficeChart.IOfficeFill.html#Syncfusion_OfficeChart_IOfficeFill_FillType) is set as SolidColor. Color-shaded fill is represented as a floating-point value ranging from 0.0 (Clear) to 1.0 (Opaque).

The complete code snippet illustrating the above options is shown below.

{% tabs %}
{% highlight c# tabtitle="C#" %}

FileStream fileStreamPath = new FileStream(“Data/Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
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
     //Formats the chart area.
     IOfficeChartFrameFormat chartArea = chart.ChartArea;
     //Sets border line pattern, color, line weight
     chartArea.Border.LinePattern = OfficeChartLinePattern.Solid;
     chartArea.Border.LineColor = Syncfusion.Drawing.Color.Blue;
     chartArea.Border.LineWeight = OfficeChartLineWeight.Hairline;
     //Sets fill type and fill colors
     chartArea.Fill.FillType = OfficeFillType.Gradient;
     chartArea.Fill.GradientColorType = OfficeGradientColor.TwoColor;
     chartArea.Fill.BackColor = Syncfusion.Drawing.Color.FromArgb(205, 217, 234);
     chartArea.Fill.ForeColor = Syncfusion.Drawing.Color.White;
     using (FileStream outputStream = new FileStream(“Sample.docx", FileMode.Create, FileAccess.ReadWrite, FileShare.ReadWrite))
     {
         //Save the Word file.
         document.Save(outputStream, FormatType.Docx);
     }
}

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from GitHub.