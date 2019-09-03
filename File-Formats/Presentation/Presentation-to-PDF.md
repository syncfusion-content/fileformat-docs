---
title: Converting PowerPoint Presentation to PDF | Syncfusion
description: Converting PowerPoint Presentation to PDF; PowerPoint Presentation conversion
platform: file-formats
control: PowerPoint
documentation: UG
---
# Presentation to PDF conversion

PowerPoint allows you to convert an entire Presentation or a single slide into PDF document. Refer to the following links for assemblies/nuget packages required based on platforms to convert PowerPoint document into PDF.

* [Assemblies Information](https://help.syncfusion.com/file-formats/presentation/assemblies-required)
* [NuGet Information](https://help.syncfusion.com/file-formats/presentation/nuget-packages-required#converting-powerpoint-presentation-into-pdf)

**PresentationToPdfConverter** class is responsible for converting an entire Presentation or a slide into PDF. The following code example demonstrates how to convert a PowerPoint presentation to PDF.

{% tabs %}

{% highlight c# %}
//Namespaces to perform PPTX to PDF conversion
using Syncfusion.OfficeChartToImageConverter;
using Syncfusion.Presentation;
using Syncfusion.PresentationToPdfConverter;
using Syncfusion.Pdf;

//Opens a PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open("Sample.pptx");
//Creates an instance of ChartToImageConverter and assigns it to ChartToImageConverter property of Presentation
pptxDoc.ChartToImageConverter = new ChartToImageConverter();
//Converts the PowerPoint Presentation into PDF document
PdfDocument pdfDocument = PresentationToPdfConverter.Convert(pptxDoc);
//Saves the PDF document
pdfDocument.Save("Sample.pdf");
//Closes the PDF document
pdfDocument.Close(true);
//Closes the Presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net %}
'Namespaces to perform PPTX to PDF conversion
Imports Syncfusion.OfficeChartToImageConverter
Imports Syncfusion.Presentation
Imports Syncfusion.PresentationToPdfConverter
Imports Syncfusion.Pdf

'Opens a PowerPoint Presentation
Dim pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
'Creates an instance of ChartToImageConverter and assigns it to ChartToImageConverter property of Presentation
pptxDoc.ChartToImageConverter = New ChartToImageConverter()
'Converts the PowerPoint Presentation into PDF document
Dim pdfDocument As PdfDocument = PresentationToPdfConverter.Convert(pptxDoc)
'Saves the PDF document
pdfDocument.Save("Sample.pdf")
'Closes the PDF document
pdfDocument.Close(True)
'Closes the Presentation
pptxDoc.Close()
{% endhighlight %}

{% highlight ASP.NET Core %}

//Namespaces to perform PPTX to PDF conversion
using Syncfusion.Pdf;
using Syncfusion.Presentation;
using Syncfusion.PresentationToPdfConverter;
using System.IO;

//Load the PowerPoint presentation into stream
using (FileStream fileStreamInput = new FileStream(@"Template.pptx", FileMode.Open, FileAccess.Read))
{
    //Open the existing PowerPoint presentation with loaded stream
    using (IPresentation pptxDoc = Presentation.Open(fileStreamInput))
    {
        //Create the MemoryStream to save the converted PDF
        using (MemoryStream pdfStream = new MemoryStream())
        {
            //Convert the PowerPoint document to PDF document
            using (PdfDocument pdfDocument = PresentationToPdfConverter.Convert(pptxDoc))
            {
                //Save the converted PDF document to MemoryStream
                pdfDocument.Save(pdfStream);
                pdfStream.Position = 0;
            }
            //Create the output PDF file stream
            using (FileStream fileStreamOutput = File.Create("Output.pdf"))
            {
                //Copy the converted PDF stream into created output PDF stream
                pdfStream.CopyTo(fileStreamOutput);
            }
        }
    }
}

{% endhighlight %}

{% highlight Xamarin %}

//Namespaces to perform PPTX to PDF conversion
using Syncfusion.Pdf;
using Syncfusion.Presentation;
using Syncfusion.PresentationToPdfConverter;
using System.IO;

//Load the PowerPoint presentation into stream
using (FileStream fileStreamInput = new FileStream(@"Template.pptx", FileMode.Open, FileAccess.Read))
{
    //Open the existing PowerPoint presentation with loaded stream
    using (IPresentation pptxDoc = Presentation.Open(fileStreamInput))
    {
        //Create the MemoryStream to save the converted PDF
        using (MemoryStream pdfStream = new MemoryStream())
        {
            //Convert the PowerPoint document to PDF document
            using (PdfDocument pdfDocument = PresentationToPdfConverter.Convert(pptxDoc))
            {
                //Save the converted PDF document to MemoryStream
                pdfDocument.Save(pdfStream);
                pdfStream.Position = 0;
            }
            //Create the output PDF file stream
            using (FileStream fileStreamOutput = File.Create("Output.pdf"))
            {
                //Copy the converted PDF stream into created output PDF stream
                pdfStream.CopyTo(fileStreamOutput);
            }
        }
    }
}

{% endhighlight %}

{% endtabs %}

N> 1. PowerPoint Presentation to PDF conversion is supported in Blazor server-side application alone and is not supported in Blazor client-side application. 
N> 2. Creating an instance of **ChartToImageConverter** class is mandatory to convert the charts present in the Presentation to PDF. Otherwise, the charts are not exported to the converted PDF
N> 3. **ChartToImageConverter** is supported from .NET Framework 4.0 onwards
N> 4. The assembly "Syncfusion.SfChart.WPF" is non compliance with FIPS(Federal Information Processing Standard) algorithm policy.

**Customizing the PowerPoint Presentation to PDF conversion**

Essential Presentation library provides you the ability to customize the Presentation to PDF conversion with the following options:

* Specify the number of slides per PDF page with ‘Handouts’ option. 
* Convert slides with notes pages to PDF.
* Embed fonts in a PowerPoint file into the converted PDF document to avoid font-related issues across different machines and different platforms. 
* Convert a PowerPoint document to PDF with the PDF-A1B conformance standards.
* Specify fallback fonts to be used in place of missing fonts.
* Skip or include hidden slides
* Set the quality of images in the PowerPoint slides to reduce the converted PDF document size.

## Font substitution for unavailable fonts

When a font used in a PowerPoint presentation is unavailable in the environment where it is converted to PDF, then the library substitutes the ‘Microsoft Sans Serif’ as a default font for text rendering. This leads to a difference in text layouts of PowerPoint presentation and the converted PDF document.  To avoid this, the Essential Presentation library allows you to set an alternate font for the missing font used in the PowerPoint presentation.

The following code sample demonstrates how to set a substitute font for a missing font while converting a PowerPoint presentation to PDF document.

{% tabs %}
{% highlight c# %}
//Load the PowerPoint presentation and convert to PDF
using (IPresentation pptxDoc = Presentation.Open("Sample.pptx"))
{
	//Initialize 'ChartToImageConverter' to convert charts in the slides, and this is optional
	pptxDoc.ChartToImageConverter = new ChartToImageConverter();

	// Initializes the 'SubstituteFont' event to set the replacement font
	pptxDoc.FontSettings.SubstituteFont += FontSettings_SubstituteFont;

	//Convert the PowerPoint presentation to PDF file
	using (PdfDocument pdfDoc = PresentationToPdfConverter.Convert(pptxDoc))
	{
		//Save the PDF file
		pdfDoc.Save("Sample.pdf");
	}
}

/// <summary>
/// Sets the alternate font when a specified font is unavailable in the production environment
/// </summary>
/// <param name="sender">FontSettings type of the Presentation in which the specified font is used but unavailable in production environment. </param>
/// <param name="args">Retrieves the unavailable font name and receives the substitute font name for conversion. </param>
private static void FontSettings_SubstituteFont(object sender, SubstituteFontEventArgs args)
{
	if (args.OriginalFontName == "Arial Unicode MS")
		args.AlternateFontName = "Arial";
	else
		args.AlternateFontName = "Times New Roman";
}
{% endhighlight %}

{% highlight vb.net %}
'Load the PowerPoint presentation and convert to PDF
Dim pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
'Initialize 'ChartToImageConverter' to convert charts in the slides, and this is optional
pptxDoc.ChartToImageConverter = New ChartToImageConverter()

'Initializes the 'SubstituteFont' event to set the replacement font
AddHandler pptxDoc.FontSettings.SubstituteFont, AddressOf SubstituteFont
'Convert the PowerPoint presentation to PDF file
Dim pdfDoc As PdfDocument = PresentationToPdfConverter.Convert(pptxDoc)
'Save the PDF file
pdfDoc.Save("Sample.pdf")

'Dispose the PowerPoint presentation instance
pptxDoc.Dispose()
'Dispose the PDF document instance
pdfDoc.Dispose()

''' <summary>
''' Sets the alternate font when a specified font is unavailable in the production environment
''' </summary>
''' <param name="sender">FontSettings type of the Presentation in which the specified font is used but unavailable in production environment. </param>
''' <param name="args">Retrieves the unavailable font name and receives the substitute font name for conversion. </param>
Private Sub SubstituteFont(ByVal sender As Object, ByVal args As SubstituteFontEventArgs)
' Sets the alternate font when a specified font is not installed in the production environment
If args.OriginalFontName = "Arial Unicode MS" Then
args.AlternateFontName = "Arial"
Else
args.AlternateFontName = "Times New Roman"
End If
End Sub
{% endhighlight %}
{% endtabs %}

## Handouts

The Presentation library allows you to convert a PowerPoint presentation to PDF document with 'Handouts' option. Thus, the library allows selecting the number of slides to be included per PDF page. This helps converting multiple PowerPoint slides within a single PDF page. 
 
The following code sample demonstrates how to convert a PowerPoint presentation to PDF document with 'Handouts' property.

{% tabs %}

{% highlight c# %}

//Load the PowerPoint presentation to convert
IPresentation pptxDoc = Presentation.Open("Sample.pptx");
 
//Enable the handouts and number of pages per slide options in converter settings
PresentationToPdfConverterSettings pdfConverterSettings = new PresentationToPdfConverterSettings();
pdfConverterSettings.PublishOptions = PublishOptions.Handouts;
pdfConverterSettings.SlidesPerPage = SlidesPerPage.Nine;
            
//Convert the documents by passing the PDF conversion settings as parameter
PdfDocument pdfDoc = PresentationToPdfConverter.Convert(pptxDoc, pdfConverterSettings);
 
//Save the converted PDF document
pdfDoc.Save("Sample.pdf");
 //Close the presentation instance
pptxDoc.Close();
//Close the PDF instance
pdfDoc.Close();
{% endhighlight %}

{% highlight vb.net %}

'Load the PowerPoint presentation to convert
Dim pptxDoc As IPresentation  = Presentation.Open("Sample.pptx")
 
'Enable the handouts and number of pages per slide options in converter settings
Dim pdfConverterSettings As PresentationToPdfConverterSettings  = new PresentationToPdfConverterSettings()

pdfConverterSettings.PublishOptions = PublishOptions.Handouts
pdfConverterSettings.SlidesPerPage = SlidesPerPage.Nine
            
'Convert the documents by passing the PDF conversion settings as parameter
Dim pdfDoc As PdfDocument  = PresentationToPdfConverter.Convert(pptxDoc, pdfConverterSettings)
 
'Save the converted PDF document
pdfDoc.Save("Sample.pdf")
 
'Close the presentation instance
pptxDoc.Close()
'Close the PDF instance
pdfDoc.Close()
{% endhighlight %}

{% endtabs %}

## Notes pages

The Presentation library allows you to convert a PowerPoint presentation to PDF document with 'notes pages' option, which will includes the notes content while PDF conversion. 

The following code sample demonstrates how to convert a PowerPoint presentation to PDF with 'notes pages'.

{% tabs %}

{% highlight c# %}

//Load the PowerPoint presentation to convert
IPresentation pptxDoc = Presentation.Open("Sample.pptx");
//Enable the include hidden slides option in converter settings
PresentationToPdfConverterSettings pdfConverterSettings = new PresentationToPdfConverterSettings();
pdfConverterSettings.PublishOptions = PublishOptions.NotesPages;
 
//Convert the documents by passing the settings as parameter
PdfDocument pdfDoc = PresentationToPdfConverter.Convert(pptxDoc, pdfConverterSettings);
//Save the converted PDF file
pdfDoc.Save("Sample.pdf");
 
//Close the presentation instance
pptxDoc.Close();
//Close the PDF instance
pdfDoc.Close();
{% endhighlight %}

{% highlight vb.net %}
'Load the PowerPoint presentation to convert
Dim pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
'Enable the include hidden slides option in converter settings
Dim pdfConverterSettings As PresentationToPdfConverterSettings pdfConverterSettings = new PresentationToPdfConverterSettings()
pdfConverterSettings.PublishOptions = PublishOptions.NotesPages
 
'Convert the documents by passing the settings as parameter
Dim pdfDoc As PdfDocument = PresentationToPdfConverter.Convert(pptxDoc, pdfConverterSettings)
'Save the converted PDF file
pdfDoc.Save("Sample.pdf")
 
'Close the presentation instance
pptxDoc.Close()
'Close the PDF instance
pdfDoc.Close()
{% endhighlight %}

{% endtabs %}

## Include hidden slides
 
 The PowerPoint presentation supports hiding the slides in a presentation document. The hidden slides will not be included in the converted PDF document, by default. The Presentation library provides support to include or exclude the hidden slides while converting a PowerPoint presentation to PDF document.
 
The following code sample demonstrates how to include the hidden slides while converting a PowerPoint presentation to PDF document. 

{% tabs %}

{% highlight c# %}
//Load the PowerPoint presentation to convert
IPresentation pptxDoc = Presentation.Open("Sample.pptx");
//Enable or disable including the hidden slides option in converter settings
PresentationToPdfConverterSettings pdfConverterSettings = new PresentationToPdfConverterSettings();
pdfConverterSettings.ShowHiddenSlides = true;
 
//Convert the documents by passing the settings as parameter
PdfDocument pdfDoc = PresentationToPdfConverter.Convert(pptxDoc, pdfConverterSettings);
//Save the converted PDF file
pdfDoc.Save("Sample.pdf");
 
//Close the presentation instance
pptxDoc.Close();
//Close the PDF instance
pdfDoc.Close();
{% endhighlight %}

{% highlight vb.net %}
'Load the PowerPoint presentation to convert
Dim pptxDoc As IPresentation  = Presentation.Open("Sample.pptx")
'Enable or disable including the hidden slides option in converter settings
Dim pdfConverterSettings As PresentationToPdfConverterSettings  = new PresentationToPdfConverterSettings()
pdfConverterSettings.ShowHiddenSlides = true
 
'Convert the documents by passing the settings as parameter
Dim pdfDoc As PdfDocument  = PresentationToPdfConverter.Convert(pptxDoc, pdfConverterSettings)
'Save the converted PDF file
pdfDoc.Save("Sample.pdf")
 
'Close the presentation instance
pptxDoc.Close()
'Close the PDF instance
pdfDoc.Close()
{% endhighlight %}

{% endtabs %}

## PDF Conformance

Essential Presentation currently supports following PDF conformances while converting a PowerPoint document to PDF.

* PDF/A-1b conformance
* PDF/X-1a conformance

N> 1. To know more details about PDF/A standard refer [https://en.wikipedia.org/wiki/PDF/A#Description](https://en.wikipedia.org/wiki/PDF/A#Description )
N> 2. To know more details about PDF/X standard refer [https://en.wikipedia.org/wiki/PDF/X](https://en.wikipedia.org/wiki/PDF/X)

The following code sample demonstrates how to set the PDF conformance level while PowerPoint presentation to PDF conversion.

{% tabs %}

{% highlight c# %}
//Load the PowerPoint document
IPresentation pptxDoc = Presentation.Open("Sample.pptx"));
//Initialize the conversion settings
PresentationToPdfConverterSettings pdfConverterSettings = new PresentationToPdfConverterSettings();
//Set the Pdf conformance level to A1B
pdfConverterSettings.PdfConformanceLevel = PdfConformanceLevel.Pdf_A1B;

//Convert the PowerPoint document to PDF
PdfDocument pdfDoc = PresentationToPdfConverter.Convert(pptxDoc,pdfConverterSettings);
//Save the converted PDF file.
pdfDoc.Save("Sample.pdf");

//Close the presentation instance
pptxDoc.Close();
//Close the PDF instance
pdfDoc.Close();
{% endhighlight %}

{% highlight vb.net %}
'Load the PowerPoint presentation to convert
Dim pptxDoc As IPresentation  = Presentation.Open("Sample.pptx")
'Enable or disable including the hidden slides option in converter settings
Dim pdfConverterSettings As PresentationToPdfConverterSettings  = new PresentationToPdfConverterSettings()
'Set the Pdf conformance level to A1B
pdfConverterSettings.PdfConformanceLevel = PdfConformanceLevel.Pdf_A1B
 
'Convert the documents by passing the settings as parameter
Dim pdfDoc As PdfDocument  = PresentationToPdfConverter.Convert(pptxDoc, pdfConverterSettings)
'Save the converted PDF file
pdfDoc.Save("Sample.pdf")
 
'Close the presentation instance
pptxDoc.Close()
'Close the PDF instance
pdfDoc.Close()
{% endhighlight %}

{% endtabs %}

## Chart quality

The Presentation library provides an option to decide the quality of the charts to optimize the converted PDF document size. 

N> The default 'ScalingMode' for charts is 'ScalingMode.Normal'. 
N> Setting the 'Best' scaling mode will improve the quality of the converted charts and increase the converted PDF document size.

The following code sample demonstrates how to set the quality of the charts while PowerPoint presentation to PDF conversion

{% tabs %}

{% highlight c# %}
//Load the PowerPoint presentation to convert
IPresentation pptxDoc = Presentation.Open("Sample.pptx");
//Create an instance of ChartToImageConverter and assigns it to ChartToImageConverter property of Presentation
pptxDoc.ChartToImageConverter = new ChartToImageConverter();
//Sets the scaling mode of the chart to best
pptxDoc.ChartToImageConverter.ScalingMode = ScalingMode.Best;
 
//Convert the documents by passing the PDF conversion settings as parameter
PdfDocument pdfDoc = PresentationToPdfConverter.Convert(pptxDoc);          
//Save the converted PDF document
pdfDoc.Save("Sample.pdf");
 
//Close the presentation instance
pptxDoc.Close();
//Close the PDF instance
pdfDoc.Close();
{% endhighlight %}

{% highlight vb.net %}
'Load the PowerPoint presentation to convert
Dim pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
'Create an instance of ChartToImageConverter and assigns it to ChartToImageConverter property of Presentation
pptxDoc.ChartToImageConverter = new ChartToImageConverter()
'Sets the scaling mode of the chart to best
pptxDoc.ChartToImageConverter.ScalingMode = ScalingMode.Best
 
'Convert the documents by passing the PDF conversion settings as parameter
Dim pdfDoc As PdfDocument = PresentationToPdfConverter.Convert(pptxDoc)          
'Save the converted PDF document
pdfDoc.Save("Sample.pdf")
 
'Close the presentation instance
pptxDoc.Close()
'Close the PDF instance
pdfDoc.Close()
{% endhighlight %}

{% endtabs %}

## Optimizing the converted PDF document size

**Optimizing the identical images**

The presentation library allows you to optimize the memory usage for the duplicate images while converting the PowerPoint presentation to PDF document to reduce the document size.
 
The following code sample demonstrates how to optimize the duplicate images while converting a PowerPoint presentation to PDF document. 

{% tabs %}

{% highlight c# %}
//Load the PowerPoint presentation to convert
IPresentation pptxDoc = Presentation.Open("Sample.pptx");
//Enable the include hidden slides option in converter settings
PresentationToPdfConverterSettings pdfConverterSettings = new PresentationToPdfConverterSettings();
//Set the flag to optimize the identical images
pdfConverterSettings.OptimizeIdenticalImages = true;
 
//Convert the documents by passing the settings as parameter
PdfDocument pdfDoc = PresentationToPdfConverter.Convert(pptxDoc, pdfConverterSettings);
//Save the converted PDF file
pdfDoc.Save("Sample.pdf");
 
//Close the presentation instance
pptxDoc.Close();
//Close the PDF instance
pdfDoc.Close();
{% endhighlight %}

{% highlight vb.net %}
'Load the PowerPoint presentation to convert
Dim pptxDoc As IPresentation  = Presentation.Open("Sample.pptx")
'Enable the include hidden slides option in converter settings
Dim pdfConverterSettings As PresentationToPdfConverterSettings  = new PresentationToPdfConverterSettings()
'Set the flag to optimize the identical images
pdfConverterSettings.OptimizeIdenticalImages = true
 
'Convert the documents by passing the settings as parameter
Dim pdfDoc As PdfDocument = PresentationToPdfConverter.Convert(pptxDoc, pdfConverterSettings)
Save the converted PDF file
pdfDoc.Save("Sample.pdf")
 
Close the presentation instance
pptxDoc.Close()
Close the PDF instance
pdfDoc.Close()
{% endhighlight %}

{% endtabs %}

**Optimizing the image quality and resolution**

You may have high resolution images in the PowerPoint slides which will impact the size of the converted PDF document. The Presentation library allows you to optimize the document size, by adjusting the quality and resolution of the images while converting the PowerPoint presentation to PDF document.
 
The following code sample demonstrates how to optimize the image quality and resolution while converting a PowerPoint presentation to PDF document. 

{% tabs %}

{% highlight c# %}
//Load the PowerPoint presentation to convert
IPresentation pptxDoc = Presentation.Open("Sample.pptx");

//Enable the include hidden slides option in converter settings
PresentationToPdfConverterSettings pdfConverterSettings = new PresentationToPdfConverterSettings();
//Set the image resolution
pdfConverterSettings.ImageResolution = 100;
//Set the image quality
pdfConverterSettings.ImageQuality = 100;
 
//Convert the documents by passing the settings as parameter
PdfDocument pdfDoc = PresentationToPdfConverter.Convert(pptxDoc, pdfConverterSettings);
//Save the converted PDF file
pdfDoc.Save("Sample.pdf");
//Close the presentation instance
pptxDoc.Close();
//Close the PDF instance
pdfDoc.Close();
{% endhighlight %}

{% highlight vb.net %}
'Load the PowerPoint presentation to convert
Dim pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
 
'Enable the include hidden slides option in converter settings
Dim pdfConverterSettings As PresentationToPdfConverterSettings = new PresentationToPdfConverterSettings()
'Set the image resolution
pdfConverterSettings.ImageResolution = 100
'Set the image quality
pdfConverterSettings.ImageQuality = 100
 
'Convert the documents by passing the settings as parameter
Dim pdfDoc As PdfDocument = PresentationToPdfConverter.Convert(pptxDoc, pdfConverterSettings)
'Save the converted PDF file
pdfDoc.Save("Sample.pdf")
'Close the presentation instance
pptxDoc.Close()
'Close the PDF instance
pdfDoc.Close()
{% endhighlight %}

{% endtabs %}

## PowerPoint to PDF conversion in Azure platform

The Syncfusion PowerPoint library supports converting the PowerPoint document to PDF in Azure platform. The following code sample demonstrates how to convert a PowerPoint presentation to PDF in Azure platform.

{% tabs %}

{% highlight c# %}
//Load the PowerPoint document
IPresentation pptxDoc = Presentation.Open("Table.pptx");

//Initialize the conversion settings
PresentationToPdfConverterSettings pdfConverterSettings = new PresentationToPdfConverterSettings();
//Enable the portable rendering.
pdfConverterSettings.EnablePortableRendering = true;

//Convert the PowerPoint document to PDF
PdfDocument pdfDoc = PresentationToPdfConverter.Convert(pptxDoc,pdfConverterSettings);
//Save the converted PDF file
pdfDoc.Save("Sample.pdf");
//Close the presentation instance
pptxDoc.Close();
//Close the PDF instance
pdfDoc.Close();
{% endhighlight %}

{% highlight vb.net %}
'Load the PowerPoint document
Dim pptxDoc As IPresentation = Presentation.Open("Table.pptx")

'Initialize the conversion settings
Dim pdfConverterSettings As PresentationToPdfConverterSettings = new PresentationToPdfConverterSettings()
'Enable the portable rendering
pdfConverterSettings.EnablePortableRendering = true

'Convert the PowerPoint document to PDF
Dim pdfDoc As PdfDocument = PresentationToPdfConverter.Convert(pptxDoc,pdfConverterSettings)
'Save the converted PDF file
pdfDoc.Save("Sample.pdf")
'Close the presentation instance
pptxDoc.Close()
'Close the PDF instance
pdfDoc.Close()
{% endhighlight %}

{% endtabs %}