---
title: Converting PowerPoint Presentation to PDF
description: Converting PowerPoint Presentation to PDF; PowerPoint Presentation conversion
platform: file-formats
control: Presentation
documentation: UG
---
# Presentation to PDF conversion

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
                Syncfusion.PresentationToPDFConverter.Base</td>
            <td>
                This assembly is used to convert PowerPoint presentation to PDF document.</td>		   
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

1. Syncfusion.OfficeChartToImageConverter
2. Syncfusion.Presentation
3. Syncfusion.PresentationToPdfConverter
4. Syncfusion.Pdf

**PresentationToPdfConverter** class is responsible for converting an entire Presentation or a slide into PDF. The following code example demonstrates how to convert a PowerPoint presentation to PDF.

{% tabs %}

{% highlight c# %}

//Opens a PowerPoint Presentation

IPresentation presentation = Presentation.Open("Sample.pptx");

//Creates an instance of ChartToImageConverter and assigns it to ChartToImageConverter property of Presentation

presentation.ChartToImageConverter = new ChartToImageConverter();

//Converts the PowerPoint Presentation into PDF document

PdfDocument pdfDocument = PresentationToPdfConverter.Convert(presentation);

//Saves the PDF document

pdfDocument.Save(@"Sample.pdf");

//Closes the PDF document

pdfDocument.Close(true);

//Closes the Presentation

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens a PowerPoint Presentation

Dim presentationDocument As IPresentation = Presentation.Open("Sample.pptx")

'Creates an instance of ChartToImageConverter and assigns it to ChartToImageConverter property of Presentation

presentationDocument.ChartToImageConverter = New ChartToImageConverter()

'Converts the PowerPoint Presentation into PDF document

Dim pdfDocument As PdfDocument = PresentationToPdfConverter.Convert(presentationDocument)

'Saves the PDF document

pdfDocument.Save("Sample.pdf")

'Closes the PDF document

pdfDocument.Close(True)

'Closes the Presentation

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

N> 1. Creating an instance of **ChartToImageConverter** class is mandatory to convert the charts present in the Presentation to PDF. Otherwise, the charts are not exported to the converted PDF
N> 2. **ChartToImageConverter** is supported from .NET Framework 4.0 onwards
N> 3. The PDF conversion is not supported in UWP and Xamarin platforms
N> 4. The assembly "Syncfusion.SfChart.WPF" is non compliance with FIPS(Federal Information Processing Standard) algorithm policy.

**Customizing** **the** **PowerPoint** **Presentation** **to** **PDF** **conversion**

Essential Presentation library provides you the ability to customize the Presentation to PDF conversion with the following options:

* Allows to specify the number of slides per PDF page with 'Handouts' option. 
* Allows to convert slides with notes pages to PDF.
* Allows to include the hidden slide during conversion. 
* Allows to convert slides with optimizing the size of the images in the PowerPoint slides, to optimize the converted PDF document size.
* Allows to determine the quality of the charts in the converted PDF.

## Handouts

The Presentation library allows you to convert a PowerPoint presentation to PDF document with 'Handouts' option. Thus, the library allows selecting the number of slides to be included per PDF page. This helps converting multiple PowerPoint slides within a single PDF page. 
 
The following code sample demonstrates how to convert a PowerPoint presentation to PDF document with 'Handouts' property.

{% tabs %}

{% highlight c# %}

//Load the PowerPoint presentation to convert.
IPresentation presentation = Presentation.Open("Sample.pptx");
 
//Enable the handouts and number of pages per slide options in converter settings.
PresentationToPdfConverterSettings pdfConverterSettings = new PresentationToPdfConverterSettings();
pdfConverterSettings.PublishOptions = PublishOptions.Handouts;
pdfConverterSettings.SlidesPerPage = SlidesPerPage.Nine;
            
//Convert the documents by passing the PDF conversion settings as parameter.
PdfDocument pdfDoc = PresentationToPdfConverter.Convert(presentation, pdfConverterSettings);
 
//Save the converted PDF document.
pdfDoc.Save("Sample.pdf");
 
//Close the presentation instance
presentation.Close();
 
//Close the PDF instance
pdfDoc.Close();

{% endhighlight %}

{% endtabs %}

## Notes pages

The Presentation library allows you to convert a PowerPoint presentation to PDF document with 'notes pages' option, which will includes the notes content while PDF conversion. 

The following code sample demonstrates how to convert a PowerPoint presentation to PDF with 'notes pages'.

{% tabs %}

{% highlight c# %}

 //Load the PowerPoint presentation to convert.
IPresentation presentation = Presentation.Open("Sample.pptx");
 
//Enable the include hidden slides option in converter settings.
PresentationToPdfConverterSettings pdfConverterSettings = new PresentationToPdfConverterSettings();
pdfConverterSettings.PublishOptions = PublishOptions.NotesPages;
 
//Convert the documents by passing the settings as parameter.
PdfDocument pdfDoc = PresentationToPdfConverter.Convert(presentation, pdfConverterSettings);
 
//Save the converted PDF file.
pdfDoc.Save("Sample.pdf");
 
//Close the presentation instance
presentation.Close();
 
//Close the PDF instance
pdfDoc.Close();

{% endhighlight %}

{% endtabs %}

## Include hidden slides
 
 The PowerPoint presentation supports hiding the slides in a presentation document. The hidden slides will not be included in the converted PDF document, by default. The Presentation library provides support to include or exclude the hidden slides while converting a PowerPoint presentation to PDF document.
 
The following code sample demonstrates how to include the hidden slides while converting a PowerPoint presentation to PDF document. 

{% tabs %}

{% highlight c# %}

//Load the PowerPoint presentation to convert.
IPresentation presentation = Presentation.Open("Sample.pptx");
 
//Enable or disable including the hidden slides option in converter settings.
PresentationToPdfConverterSettings pdfConverterSettings = new PresentationToPdfConverterSettings();
pdfConverterSettings.ShowHiddenSlides = true;
 
//Convert the documents by passing the settings as parameter.
PdfDocument pdfDoc = PresentationToPdfConverter.Convert(presentation, pdfConverterSettings);
 
//Save the converted PDF file.
pdfDoc.Save("Sample.pdf");
 
//Close the presentation instance
presentation.Close();
 
//Close the PDF instance
pdfDoc.Close();

{% endhighlight %}

{% endtabs %}

## Optimizing the identical images

The presentation library allows you to optimize the memory usage for the duplicate images while converting the PowerPoint presentation to PDF document to reduce the document size.
 
The following code sample demonstrates how to optimize the duplicate images while converting a PowerPoint presentation to PDF document. 

{% tabs %}

{% highlight c# %}

//Load the PowerPoint presentation to convert.
IPresentation presentation = Presentation.Open("Sample.pptx");
 
//Enable the include hidden slides option in converter settings.
PresentationToPdfConverterSettings pdfConverterSettings = new PresentationToPdfConverterSettings();
 
//Set the flag to optimize the identical images
pdfConverterSettings.OptimizeIdenticalImages = true;
 
//Convert the documents by passing the settings as parameter.
PdfDocument pdfDoc = PresentationToPdfConverter.Convert(presentation, pdfConverterSettings);
 
//Save the converted PDF file.
pdfDoc.Save("Sample.pdf");
 
//Close the presentation instance
presentation.Close();
 
//Close the PDF instance
pdfDoc.Close();

{% endhighlight %}

{% endtabs %}

## Optimizing the image quality and resolution

You may have high resolution images in the PowerPoint slides which will impact the size of the converted PDF document. The Presentation library allows you to optimize the document size, by increasing or decreasing the quality and resolution of the images while converting the PowerPoint presentation to PDF document.
 
The following code sample demonstrates how to optimize the image quality and resolution while converting a PowerPoint presentation to PDF document. 

{% tabs %}

{% highlight c# %}

//Load the PowerPoint presentation to convert.
IPresentation presentation = Presentation.Open("Sample.pptx");
 
//Enable the include hidden slides option in converter settings.
PresentationToPdfConverterSettings pdfConverterSettings = new PresentationToPdfConverterSettings();
 
//Set the image resolution
pdfConverterSettings.ImageResolution = 100;
 
//Set the image quality
pdfConverterSettings.ImageQuality = 100;
 
//Convert the documents by passing the settings as parameter.
PdfDocument pdfDoc = PresentationToPdfConverter.Convert(presentation, pdfConverterSettings);
 
//Save the converted PDF file.
pdfDoc.Save("Sample.pdf");
 
//Close the presentation instance
presentation.Close();
 
//Close the PDF instance
pdfDoc.Close();

{% endhighlight %}

{% endtabs %}

## Chart quality

The Presentation library provides an option to determine the quality of the charts to optimize the size of the converted PDF document.

The following code sample demonstrates how to set the quality of the charts while PowerPoint presentation to PDF conversion


{% tabs %}

{% highlight c# %}

//Load the PowerPoint presentation to convert.
IPresentation presentation = Presentation.Open("Sample.pptx");

//Create an instance of ChartToImageConverter and assigns it to ChartToImageConverter property of Presentation

presentation.ChartToImageConverter = new ChartToImageConverter();

//Sets the scaling mode of the chart to best.
presentation.ChartToImageConverter.ScalingMode = ScalingMode.Best;
 
//Convert the documents by passing the PDF conversion settings as parameter.
PdfDocument pdfDoc = PresentationToPdfConverter.Convert(presentation);          
 
//Save the converted PDF document.
pdfDoc.Save("Sample.pdf");
 
//Close the presentation instance
presentation.Close();
 
//Close the PDF instance
pdfDoc.Close();

{% endhighlight %}

{% endtabs %}