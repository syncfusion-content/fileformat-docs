---
layout: post
title: Converting PowerPoint Presentation to PDF or Image
description: Converting PowerPoint Presentation to PDF; Converting PowerPoint Presentation slide to image; PowerPoint Presentation conversion
platform: FileFormats
control: Presentation
documentation: UG
---
# Conversion

## Converting PowerPoint presentation to PDF

To convert a PowerPoint presentation to PDF, include the following assemblies in the application.

<table>
<tr>
<td>
Assembly Name<br/><br/></td><td>
Short Description<br/><br/></td></tr>
<tr>
<td>
Syncfusion.Presentation.Base<br/><br/></td><td>
This assembly contains the core features needed for creating, reading, manipulating a Presentation file.<br/><br/></td></tr>
<tr>
<td>
Syncfusion.OfficeChart.Base<br/><br/></td><td>
This assembly contains the Office Chart Object model and core features needed for chart creation.<br/><br/></td></tr>
<tr>
<td>
Syncfusion.OfficeChartToImageConverter.WPF<br/><br/></td><td>
This assembly is used to convert Office Chart into Image. <br/><br/></td></tr>
<tr>
<td>
Syncfusion.Pdf.Base<br/><br/></td><td>
This assembly is used for PDF file creation. <br/><br/></td></tr>
<tr>
<td>
Syncfusion.SfChart.WPF<br/><br/></td><td>
Supporting assembly for Syncfusion.OfficeChartToImageConverter.WPF<br/><br/></td></tr>
<tr>
<td>
Syncfusion.Shared.WPF<br/><br/></td><td>
Supporting assembly for Syncfusion.OfficeChartToImageConverter.WPF<br/><br/></td></tr>
<tr>
<td>
Syncfusion.Compression.Base<br/><br/></td><td>
This assembly is used to pack the Presentation contents.<br/><br/></td></tr>
</table>
The following namespaces are required to compile the code in this topic.

1. using Syncfusion.OfficeChartToImageConverter;
2. using Syncfusion.Presentation;
3. using Syncfusion.PresentationToPdfConverter;
4. using Syncfusion.Pdf;

**PresentationToPdfConverter** class is responsible for converting an entire Presentation or a slide into PDF. The following code example demonstrates how to convert a PowerPoint presentation to PDF.

{% highlight c# %}
[C#]

//Opens a PowerPoint presentation file

IPresentation presentation = Presentation.Open(fileName);

//Creates an instance of ChartToImageConverter and assigns it to ChartToImageConverter property of Presentation

presentation.ChartToImageConverter = new ChartToImageConverter();

//Converts the PowerPoint presentation into PDF document

PdfDocument PDFdocument = PresentationToPdfConverter.Convert(presentation);

//Saves the PDF document

PDFdocument.Save(@"SampleWithoutSetting.pdf");

//Closes the PDF document

PDFdocument.Close(true);

//Closes the presentation

presentation.Close();



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Opens a PowerPoint presentation file

Dim presentation_1 As IPresentation = Presentation.Open("ClonedPresentation.pptx")

'Creates an instance of ChartToImageConverter and assigns it to ChartToImageConverter property of Presentation

presentation_1.ChartToImageConverter = New ChartToImageConverter()

'Converts the PowerPoint presentation into PDF document

Dim PDFdocument As PdfDocument = PresentationToPdfConverter.Convert(presentation_1)

'Saves the PDF document

PDFdocument.Save("SampleWithoutSetting.pdf")

'Closes the PDF document

PDFdocument.Close(True)

'Closes the presentation

presentation_1.Close()



{% endhighlight %}

**Note****:**

1. Creating an instance of **ChartToImageConverter** class is mandatory to convert the charts present in the presentation to PDF. Otherwise, the charts are not exported to the converted PDF.
2. **ChartToImageConverter** is supported from .NET Framework 4.0 onwards

**Customizing** **the** **PowerPoint** **presentation** **to** **PDF** **conversion**

Essential Presentation library provides you the ability to customize the presentation to PDF conversion with the following options:

* Allows to include the hidden slide during conversion.
* Allows to specify the number of slides per PDF page.
* Allows to determine the quality of the charts in the converted PDF 

The following code example shows the customized PDF conversion.

{% highlight c# %}
[C#]

//Opens a PowerPoint presentation file

IPresentation presentation = Presentation.Open(fileName);

//Creates an instance of ChartToImageConverter and assigns it to ChartToImageConverter property of Presentation

presentation.ChartToImageConverter = new ChartToImageConverter();

//Sets the scaling mode of the chart to best.

presentation.ChartToImageConverter.ScalingMode = ScalingMode.Best;

//Instantiates the presentation to pdf converter settings instance.

PresentationToPdfConverterSettings settings = new PresentationToPdfConverterSettings();

//Sets the option for adding hidden slides to converted pdf

settings.ShowHiddenSlides = false;

//Sets the slide per page settings; this is optional.

settings.SlidesPerPage = SlidesPerPage.Three;

//Converts the PowerPoint presentation into PDF document

PdfDocument PDFdocument = PresentationToPdfConverter.Convert(presentation, settings);

//Saves the PDF document

PDFdocument.Save(@"SampleWithoutSetting.pdf");

//Closes the PDF document

PDFdocument.Close(true);

//Closes the presentation

presentation.Close();



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Opens a PowerPoint presentation file

Dim presentation_1 As IPresentation = Presentation.Open(fileName)

'Creates an instance of ChartToImageConverter and assigns it to ChartToImageConverter property of Presentation

presentation_1.ChartToImageConverter = New ChartToImageConverter()

'Sets the scaling mode of the chart to best.

presentation_1.ChartToImageConverter.ScalingMode = ScalingMode.Best

'Instantiates the presentation to pdf converter settings instance.

Dim settings As New PresentationToPdfConverterSettings()

'Sets the hiding slides to false; this is optional.

settings.ShowHiddenSlides = False

'Sets the slide per page settings; this is optional.

settings.SlidesPerPage = SlidesPerPage.Three

'Converts the PowerPoint presentation into PDF document

Dim PDFdocument As PdfDocument = PresentationToPdfConverter.Convert(presentation_1, settings)

'Saves the PDF document

PDFdocument.Save("SampleWithoutSetting.pdf")

'Closes the PDF document

PDFdocument.Close(True)

'Closes the presentation

presentation_1.Close()



{% endhighlight %}

## Converting PowerPoint presentation to Images

An entire presentation or a single slide can be converted to image by using Essential Presentation library. The supported image formats are listed as follows.

* Bmp
* Emf
* Gif
* Jpeg
* Png
* Wmf
* Icon
* Exif
* MemoryBmp
* Tiff

To convert a presentation or a single slide to image, the following assemblies are required in an application:

<table>
<tr>
<td>
**Assembly** **Name**<br/><br/></td><td>
**Short** **Description**<br/><br/></td></tr>
<tr>
<td>
Syncfusion.Presentation.Base<br/><br/></td><td>
This assembly contains the core features required for creating, reading, manipulating a Presentation file.<br/><br/></td></tr>
<tr>
<td>
Syncfusion.Compression.Base<br/><br/></td><td>
This assembly is used to package the Presentation contents.<br/><br/></td></tr>
<tr>
<td>
Syncfusion.OfficeChart.Base<br/><br/></td><td>
This assembly contains the Office Chart Object model and core features needed for chart creation.<br/><br/></td></tr>
<tr>
<td>
Syncfusion.OfficeChartToImageConverter.WPF<br/><br/></td><td>
This assembly is used to convert Office Chart into Image. This assembly depends on Syncfusion.SfChart.WPF and Syncfusion.Shared.WPF for chart conversion.<br/><br/></td></tr>
<tr>
<td>
Syncfusion.SfChart.WPF<br/><br/></td><td>
Supporting assembly for Syncfusion.OfficeChartToImageConverter.WPF<br/><br/></td></tr>
<tr>
<td>
Syncfusion.Shared.WPF<br/><br/></td><td>
Supporting assembly for Syncfusion.OfficeChartToImageConverter.WPF<br/><br/></td></tr>
</table>
The following code example demonstrates how to convert a slide to image.

{% highlight c# %}
[C#]

//Opens a PowerPoint presentation file

IPresentation presentation = Presentation.Open(fileName);

//Creates an instance of ChartToImageConverter

presentation.ChartToImageConverter = new ChartToImageConverter();

//Sets the scaling mode as best

presentation.ChartToImageConverter.ScalingMode = Syncfusion.OfficeChart.ScalingMode.Best;

//Converts the first slide into image

Image image = presentation.Slides[0].ConvertToImage(Syncfusion.Drawing.ImageType.Metafile);

//Saves the image as file

image.Save("slide1.png");

//Disposes the image

image.dispose();

//Closes the presentation instance

presentation.Close();



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Opens a PowerPoint presentation file

Dim presentation_1 As IPresentation = Presentation.Open(fileName)

'Creates an instance of ChartToImageConverter

presentation_1.ChartToImageConverter = New ChartToImageConverter()

'Sets the scaling mode as best

presentation_1.ChartToImageConverter.ScalingMode = Syncfusion.OfficeChart.ScalingMode.Best

'Converts the first slide into image

Dim image As Image = presentation_1.Slides(0).ConvertToImage(Syncfusion.Drawing.ImageType.Metafile)

'Saves the image as file

image.Save("slide1.png")

'Disposes the image

image.Dispose()

'Closes the presentation instance

Presentation_1.Close()



{% endhighlight %}

The following code example demonstrates the conversion of an entire presentation to images:

{% highlight c# %}
[C#]

//Loads the PowerPoint presentation

IPresentation presentation = Presentation.Open("Sample.pptx");

//Creates instance of ChartToImageConverter

presentation.ChartToImageConverter = new ChartToImageConverter();

//Sets the scaling mode as best

presentation.ChartToImageConverter.ScalingMode = Syncfusion.OfficeChart.ScalingMode.Best;

//Converts entire presentation to images

Image[] images = presentation.RenderAsImages(Syncfusion.Drawing.ImageType.Metafile);

//Saves the image to file system

foreach (Image image in images)

{ 

image.Save("ImageOutput" + Guid.NewGuid().ToString()+ ".png");

}



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Loads the PowerPoint presentation

Dim presentation_1 As IPresentation = Presentation.Open("Sample.pptx")

'Creates instance of ChartToImageConverter

presentation_1.ChartToImageConverter = New ChartToImageConverter()

'Sets the scaling mode as best

presentation_1.ChartToImageConverter.ScalingMode = Syncfusion.OfficeChart.ScalingMode.Best

'Converts entire presentation to images

Dim images As Image() = presentation_1.RenderAsImages(Syncfusion.Drawing.ImageType.Metafile)

'Saves the image to file system

For Each image As Image In images

image.Save("ImageOutput" + Guid.NewGuid().ToString() + ".png")

Next



{% endhighlight %}

**Note****:**

1. Instance of **ChartToImageConverter** class is mandatory to convert the charts present in the presentation to image. Otherwise, the charts in the presentation are not exported to the converted image.
2. **ChartToImageConverter** is supported from .NET Framework 4.0 onward.

