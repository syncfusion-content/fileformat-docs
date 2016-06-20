---
title: Converting PowerPoint Presentation to PDF or Image
description: Converting PowerPoint Presentation to PDF; Converting PowerPoint Presentation slide to image; PowerPoint Presentation conversion
platform: file-formats
control: Presentation
documentation: UG
---
# Conversion

## Converting PowerPoint Presentation to PDF

To convert a PowerPoint Presentation to PDF, include the following assemblies in the application.

<table>
    <thead>
        <tr>
            <th>
                Assembly Name</th>
            <th>
                Short Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                Syncfusion.Presentation.Base</td>
            <td>
                This assembly contains the core features needed for creating, reading, manipulating a Presentation file.</td>
        </tr>
        <tr>
            <td>
                Syncfusion.OfficeChart.Base</td>
            <td>
                This assembly contains the Office Chart Object model and core features needed for chart creation.</td>
        </tr>
        <tr>
            <td>
                Syncfusion.OfficeChartToImageConverter.WPF</td>
            <td>
                This assembly is used to convert Office Chart into Image. </td>
        </tr>
        <tr>
            <td>
                Syncfusion.Pdf.Base</td>
            <td>
                This assembly is used for PDF file creation. </td>
        </tr>
        <tr>
            <td>
                Syncfusion.SfChart.WPF</td>
            <td>
                Supporting assembly for Syncfusion.OfficeChartToImageConverter.WPF</td>
        </tr>       
        <tr>
            <td>
                Syncfusion.Compression.Base</td>
            <td>
                This assembly is used to pack the Presentation contents.</td>
        </tr>
    </tbody>
</table>

The following namespaces are required to compile the code in this topic.

1. Syncfusion.OfficeChartToImageConverter;
2. Syncfusion.Presentation;
3. Syncfusion.PresentationToPdfConverter;
4. Syncfusion.Pdf;

**PresentationToPdfConverter** class is responsible for converting an entire Presentation or a slide into PDF. The following code example demonstrates how to convert a PowerPoint presentation to PDF.

{% tabs %}

{% highlight c# %}

//Opens a PowerPoint Presentation

IPresentation presentation = Presentation.Open(fileName);

//Creates an instance of ChartToImageConverter and assigns it to ChartToImageConverter property of Presentation

presentation.ChartToImageConverter = new ChartToImageConverter();

//Converts the PowerPoint Presentation into PDF document

PdfDocument PDFdocument = PresentationToPdfConverter.Convert(presentation);

//Saves the PDF document

PDFdocument.Save(@"Sample.pdf");

//Closes the PDF document

PDFdocument.Close(true);

//Closes the Presentation

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens a PowerPoint Presentation

Dim presentationDocument As IPresentation = Presentation.Open("ClonedPresentation.pptx")

'Creates an instance of ChartToImageConverter and assigns it to ChartToImageConverter property of Presentation

presentationDocument.ChartToImageConverter = New ChartToImageConverter()

'Converts the PowerPoint Presentation into PDF document

Dim PDFdocument As PdfDocument = PresentationToPdfConverter.Convert(presentationDocument)

'Saves the PDF document

PDFdocument.Save("Sample.pdf")

'Closes the PDF document

PDFdocument.Close(True)

'Closes the Presentation

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

N> 1. Creating an instance of **ChartToImageConverter** class is mandatory to convert the charts present in the Presentation to PDF. Otherwise, the charts are not exported to the converted PDF
N> 2. **ChartToImageConverter** is supported from .NET Framework 4.0 onwards
N> 3. The PDF conversion is not supported in UWP and Xamarin platforms

**Customizing** **the** **PowerPoint** **Presentation** **to** **PDF** **conversion**

Essential Presentation library provides you the ability to customize the Presentation to PDF conversion with the following options:

* Allows to include the hidden slide during conversion.
* Allows to specify the number of slides per PDF page.
* Allows to determine the quality of the charts in the converted PDF 

The following code example shows the customized PDF conversion.

{% tabs %}

{% highlight c# %}

//Opens a PowerPoint Presentation

IPresentation presentation = Presentation.Open(fileName);

//Creates an instance of ChartToImageConverter and assigns it to ChartToImageConverter property of Presentation

presentation.ChartToImageConverter = new ChartToImageConverter();

//Sets the scaling mode of the chart to best.

presentation.ChartToImageConverter.ScalingMode = ScalingMode.Best;

//Instantiates the Presentation to pdf converter settings instance.

PresentationToPdfConverterSettings settings = new PresentationToPdfConverterSettings();

//Sets the option for adding hidden slides to converted pdf

settings.ShowHiddenSlides = false;

//Sets the slide per page settings; this is optional.

settings.SlidesPerPage = SlidesPerPage.Three;

//Converts the PowerPoint Presentation into PDF document

PdfDocument PDFdocument = PresentationToPdfConverter.Convert(presentation, settings);

//Saves the PDF document

PDFdocument.Save(@"Sample.pdf");

//Closes the PDF document

PDFdocument.Close(true);

//Closes the Presentation

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens a PowerPoint Presentation

Dim presentationDocument As IPresentation = Presentation.Open(fileName)

'Creates an instance of ChartToImageConverter and assigns it to ChartToImageConverter property of Presentation

presentationDocument.ChartToImageConverter = New ChartToImageConverter()

'Sets the scaling mode of the chart to best.

presentationDocument.ChartToImageConverter.ScalingMode = ScalingMode.Best

'Instantiates the Presentation to pdf converter settings instance.

Dim settings As New PresentationToPdfConverterSettings()

'Sets the hiding slides to false; this is optional.

settings.ShowHiddenSlides = False

'Sets the slide per page settings; this is optional.

settings.SlidesPerPage = SlidesPerPage.Three

'Converts the PowerPoint Presentation into PDF document

Dim PDFdocument As PdfDocument = PresentationToPdfConverter.Convert(presentationDocument, settings)

'Saves the PDF document

PDFdocument.Save("Sample.pdf")

'Closes the PDF document

PDFdocument.Close(True)

'Closes the Presentation

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

## Converting PowerPoint Presentation to Images

An entire Presentation or a single slide can be converted to image by using Essential Presentation library. The supported image formats are listed as follows.

* BMP
* Emf
* GIF
* JPEG
* PNG
* WMF
* Icon
* Exif
* MemoryBmp
* TIFF

To convert a Presentation or a single slide to image, the following assemblies are required in an application:

<table>
    <thead>
        <tr>
            <th>
                Assembly Name</th>
            <th>
                Short Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                Syncfusion.Presentation.Base
                
                
            </td>
            <td>
                This assembly contains the core features required for creating, reading, manipulating a Presentation file.
                
                
            </td>
        </tr>
        <tr>
            <td>
                Syncfusion.Compression.Base
                
                
            </td>
            <td>
                This assembly is used to package the Presentation contents.
                
                
            </td>
        </tr>
        <tr>
            <td>
                Syncfusion.OfficeChart.Base
                
                
            </td>
            <td>
                This assembly contains the Office Chart Object model and core features needed for chart creation.
                
                
            </td>
        </tr>
        <tr>
            <td>
                Syncfusion.OfficeChartToImageConverter.WPF
                
                
            </td>
            <td>
                This assembly is used to convert Office Chart into Image. This assembly depends on Syncfusion.SfChart.WPF and Syncfusion.Shared.WPF for chart conversion.
                
                
            </td>
        </tr>
        <tr>
            <td>
                Syncfusion.SfChart.WPF
                
                
            </td>
            <td>
                Supporting assembly for Syncfusion.OfficeChartToImageConverter.WPF
                
                
            </td>
        </tr>        
    </tbody>
</table>

T> When converting a slide to image, use Metafile format for good image resolution.

The following code example demonstrates how to convert a slide to image.

{% tabs %}

{% highlight c# %}

//Opens a PowerPoint Presentation file

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

image.Dispose();

//Closes the Presentation instance

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens a PowerPoint Presentation file

Dim presentationDocument As IPresentation = Presentation.Open(fileName)

'Creates an instance of ChartToImageConverter

presentationDocument.ChartToImageConverter = New ChartToImageConverter()

'Sets the scaling mode as best

presentationDocument.ChartToImageConverter.ScalingMode = Syncfusion.OfficeChart.ScalingMode.Best

'Converts the first slide into image

Dim image As Image = presentationDocument.Slides(0).ConvertToImage(Syncfusion.Drawing.ImageType.Metafile)

'Saves the image as file

image.Save("slide1.png")

'Disposes the image

image.Dispose()

'Closes the Presentation instance

Presentation_1.Close()

{% endhighlight %}

{% endtabs %}


The following code example demonstrates the conversion of an entire Presentation to images:

{% tabs %}

{% highlight c# %}

//Loads the PowerPoint Presentation

IPresentation presentation = Presentation.Open("Sample.pptx");

//Creates instance of ChartToImageConverter

presentation.ChartToImageConverter = new ChartToImageConverter();

//Sets the scaling mode as best

presentation.ChartToImageConverter.ScalingMode = Syncfusion.OfficeChart.ScalingMode.Best;

//Converts entire Presentation to images

Image[] images = presentation.RenderAsImages(Syncfusion.Drawing.ImageType.Metafile);

//Saves the image to file system

foreach (Image image in images)

{ 

image.Save("ImageOutput" + Guid.NewGuid().ToString()+ ".png");

}



{% endhighlight %}

{% highlight vb.net %}

'Loads the PowerPoint Presentation

Dim presentationDocument As IPresentation = Presentation.Open("Sample.pptx")

'Creates instance of ChartToImageConverter

presentationDocument.ChartToImageConverter = New ChartToImageConverter()

'Sets the scaling mode as best

presentationDocument.ChartToImageConverter.ScalingMode = Syncfusion.OfficeChart.ScalingMode.Best

'Converts entire Presentation to images

Dim images As Image() = presentationDocument.RenderAsImages(Syncfusion.Drawing.ImageType.Metafile)

'Saves the image to file system

For Each image As Image In images

image.Save("ImageOutput" + Guid.NewGuid().ToString() + ".png")

Next

{% endhighlight %}

{% endtabs %}

N> 1. Instance of **ChartToImageConverter** class is mandatory to convert the charts present in the Presentation to image. Otherwise, the charts in the presentation are not exported to the converted image
N> 2. **ChartToImageConverter** is supported from .NET Framework 4.0 onward
N> 3. The image conversion is not supported in UWP and Xamarin platforms

