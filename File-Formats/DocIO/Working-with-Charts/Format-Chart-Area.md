---
title: Modify the Appearance of Chart Area | Syncfusion
description: Learn how to modify the appearance of chart area in a chart in a Word document using Syncfusion .NET Core Word (DocIO) library without Microsoft Word.
platform: file-formats
control: DocIO
documentation: UG
---

# Chart Area

Chart area refers to the space that contains the chart or graph you've inserted into a slide. It includes the entire chart and all its elements, such as data points, labels, axes, and the plot area. Using Syncfusion [.NET Core Word (DocIO)](https://www.syncfusion.com/document-processing/word-framework/net-core/word-library) library, you can customize the chart area in the chart.

## Customization of Border

The following code snippet illustrates how to modify the border of the chart area.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Format the chart area.
IOfficeChartFrameFormat chartArea = chart.ChartArea;
//Set border line pattern, color, line weight.
chartArea.Border.LinePattern = OfficeChartLinePattern.Solid;
chartArea.Border.LineColor = Syncfusion.Drawing.Color.Blue;
chartArea.Border.LineWeight = OfficeChartLineWeight.Hairline;

{% endhighlight %}
{% endtabs %}

## Customization of Color

The following code snippet illustrates how to fill the color in chart area.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Set fill type and fill colors.
chartArea.Fill.FillType = OfficeFillType.Gradient;
chartArea.Fill.GradientColorType = OfficeGradientColor.TwoColor;
chartArea.Fill.BackColor = Syncfusion.Drawing.Color.FromArgb(205, 217, 234);
chartArea.Fill.ForeColor = Syncfusion.Drawing.Color.White;

{% endhighlight %}
{% endtabs %}

The complete code snippet illustrating the above options is shown below.

{% tabs %}
{% highlight c# tabtitle="C#" %}

 FileStream fileStreamPath = new FileStream("Data/Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
 //Open an existing document from file system through constructor of WordDocument class.
 using (WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx))
 {
     //Get the paragraph.
     WParagraph paragraph = document.LastParagraph;
     //Get the chart entity.
     WChart chart = paragraph.ChildEntities[0] as WChart;
     //Modify the chart height and width.
     chart.Height = 300;
     chart.Width = 500;

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

     using (FileStream outputStream = new FileStream("Sample.docx", FileMode.Create, FileAccess.ReadWrite, FileShare.ReadWrite))
     {
         //Save the Word file.
         document.Save(outputStream, FormatType.Docx);
     }
 }

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from GitHub.

By executing the program, you will get the **chart** as follows.

## Add Image in Chart Area

The following code snippet illustrates how to fill the image in chart area.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Append image in chart area.
FileStream imageStream = new FileStream("Data/Image.png", FileMode.Open, FileAccess.Read);
Image image = Image.FromStream(imageStream);
chartArea.Fill.UserPicture(image, "image");

{% endhighlight %}
{% endtabs %}

## Set the Transparency level

The following code snippet illustrates how to make transparency in chart area.

{% tabs %}
{% highlight c# tabtitle="C#" %}

// Set the transparency of the chart area.
chartArea.Fill.Transparency = 0.5;

{% endhighlight %}
{% endtabs %}

N> [Transparency](https://help.syncfusion.com/cr/file-formats/Syncfusion.OfficeChart.IOfficeFill.html#Syncfusion_OfficeChart_IOfficeFill_Transparency) is only applicable when [FillType](https://help.syncfusion.com/cr/file-formats/Syncfusion.OfficeChart.IOfficeFill.html#Syncfusion_OfficeChart_IOfficeFill_FillType) is set as SolidColor. Color-shaded fill is represented as a floating-point value ranging from 0.0 (Clear) to 1.0 (Opaque).

