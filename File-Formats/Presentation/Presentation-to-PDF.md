---
title: Converting PowerPoint Presentation to PDF |Syncfusion|
description: This section illustrates how to convert PowerPoint Presentation document to PDF; PowerPoint Presentation conversion
platform: file-formats
control: PowerPoint
documentation: UG
---
# Presentation to PDF conversion

PowerPoint allows you to convert an entire Presentation or a single slide into PDF document. Refer to the following links for assemblies/nuget packages required based on platforms to [convert PowerPoint document into PDF](https://www.syncfusion.com/document-processing/powerpoint-framework/net/powerpoint-to-pdf-conversion).

* [Assemblies Information](https://help.syncfusion.com/file-formats/presentation/assemblies-required)
* [NuGet Information](https://help.syncfusion.com/file-formats/presentation/nuget-packages-required#converting-powerpoint-presentation-into-pdf)

[PresentationToPdfConverter](https://help.syncfusion.com/cr/file-formats/Syncfusion.PresentationToPdfConverter.PresentationToPdfConverter.html) class is responsible for converting an entire Presentation or a slide into PDF. The following code example demonstrates how to convert a PowerPoint presentation to PDF.

{% tabs %}

{% highlight c# tabtitle="C#" %}
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

{% highlight vb.net tabtitle="VB.NET" %}
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

{% highlight c# tabtitle="ASP.NET Core" %}
//Namespaces to perform PPTX to PDF conversion
using Syncfusion.Pdf;
using Syncfusion.Presentation;
using Syncfusion.PresentationRenderer;
using System.IO;

//Load the PowerPoint presentation into stream.
using (FileStream fileStreamInput = new FileStream(@"Template.pptx", FileMode.Open, FileAccess.Read))
{
    //Open the existing PowerPoint presentation with loaded stream.
    using (IPresentation pptxDoc = Presentation.Open(fileStreamInput))
    {
        //Create the MemoryStream to save the converted PDF.
        using (MemoryStream pdfStream = new MemoryStream())
        {
            //Convert the PowerPoint document to PDF document.
            using (PdfDocument pdfDocument = PresentationToPdfConverter.Convert(pptxDoc))
            {
                //Save the converted PDF document to MemoryStream.
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

{% highlight c# tabtitle="Xamarin" %}
//Namespaces to perform PPTX to PDF conversion
using Syncfusion.Pdf;
using Syncfusion.Presentation;
using Syncfusion.PresentationRenderer;
using System.IO;

//Load the PowerPoint presentation into stream.
using (FileStream fileStreamInput = new FileStream(@"Template.pptx", FileMode.Open, FileAccess.Read))
{
    //Open the existing PowerPoint presentation with loaded stream.
    using (IPresentation pptxDoc = Presentation.Open(fileStreamInput))
    {
        //Create the MemoryStream to save the converted PDF.
        using (MemoryStream pdfStream = new MemoryStream())
        {
            //Convert the PowerPoint document to PDF document.
            using (PdfDocument pdfDocument = PresentationToPdfConverter.Convert(pptxDoc))
            {
                //Save the converted PDF document to MemoryStream.
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

N> 1. Creating an instance of [ChartToImageConverter](https://help.syncfusion.com/cr/file-formats/Syncfusion.OfficeChartToImageConverter.ChartToImageConverter.html) class is mandatory to convert the charts present in the Presentation to PDF. Otherwise, the charts are not exported to the converted PDF
N> 2. [ChartToImageConverter](https://help.syncfusion.com/cr/file-formats/Syncfusion.OfficeChartToImageConverter.ChartToImageConverter.html) is supported from .NET Framework 4.0 onwards
N> 3. The assembly "Syncfusion.SfChart.WPF" is non compliance with FIPS (Federal Information Processing Standard) algorithm policy.
N> 4. **In .NET Core targeting applications**, metafile images such as EMF and WMF have some limitations. So, those images will not preserve in Presentation document to PDF conversion using Essential Presentation. 

N> 1. To preserve the expected images in the PDF, we suggest you convert the metafile image formats to bitmap image format (JPEG or PNG) and then perform Presentation to PDF conversion.
N> 2. Otherwise, you can use the [WPF](https://www.nuget.org/packages/Syncfusion.PresentationToPdfConverter.Wpf/) or [Windows](https://www.nuget.org/packages/Syncfusion.PresentationToPdfConverter.WinForms/) Forms platform NuGet packages for .NET Core 3.0 or later versions targeting applications from v17.3.0.x and use the same [C# tab](https://help.syncfusion.com/file-formats/presentation/presentation-to-pdf) code examples for it. But in Mac and Linux environment, using the WPF or Windows Forms platform NuGet packages have limitations.


**Customizing the PowerPoint Presentation to PDF conversion**

Essential Presentation library provides you the ability to customize the Presentation to PDF conversion with the following options:

* Specify the number of slides per PDF page with [Handouts](https://help.syncfusion.com/cr/file-formats/Syncfusion.PresentationToPdfConverter.PublishOptions.html) option. 
* Convert slides with notes pages to PDF.
* Embed fonts in a PowerPoint file into the converted PDF document to avoid font-related issues across different machines and different platforms. 
* Convert a PowerPoint document to PDF with the PDF-A1B conformance standards.
* Specify fallback fonts to be used in place of missing fonts.
* Skip or include hidden slides
* Set the quality of images in the PowerPoint slides to reduce the converted PDF document size.

## PowerPoint Presentation to PDF conversion in Linux OS

In Linux OS, you can perform the PowerPoint presentation to PDF conversion using .NET Core (Targeting .netcoreapp) application. You can refer [PowerPoint presentation to PDF conversion NuGet packages](https://help.syncfusion.com/file-formats/presentation/nuget-packages-required#converting-powerpoint-presentation-into-pdf) to know about the packages required to deploy .NET Core (Targeting .netcoreapp) application with PowerPoint presentation to PDF conversion capabilities.

From v20.3.0.56, in addition to the previous NuGet packages, we recommend to use [SkiaSharp.NativeAssets.Linux v2.88.2](https://www.nuget.org/packages/SkiaSharp.NativeAssets.Linux/2.88.2) and [HarfBuzzSharp.NativeAssets.Linux v2.8.2.2](https://www.nuget.org/packages/HarfBuzzSharp.NativeAssets.Linux/2.8.2.2) NuGets to perform PowerPoint presentation to PDF conversion in Linux environment.

If you are using prior to v20.3.0.56 release, please refer [here](https://help.syncfusion.com/file-formats/presentation/faq#what-are-the-nuget-packages-to-be-installed-to-perform-powerpoint-presentation-to-pdf-conversion-in-linux-os) to know about how to perform PowerPoint presentation to PDF conversion in Linux.

## Font substitution for unavailable fonts

When a font used in a PowerPoint presentation is unavailable in the environment where it is converted to PDF, then the library substitutes the ‘Microsoft Sans Serif’ as a default font for text rendering. This leads to a difference in text layouts of PowerPoint presentation and the converted PDF document.  To avoid this, the Essential Presentation library allows you to set an alternate font for the missing font used in the PowerPoint presentation.

### Set alternate font

The following code example demonstrates how to set alternate font name for a missing font while converting a PowerPoint presentation to PDF. The provided alternate font should be installed in the production environment.

{% tabs %}
{% highlight c# tabtitle="C#" %}
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

{% highlight vb.net tabtitle="VB.NET" %}
'Load the PowerPoint presentation and convert to PDF
Dim pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
'Initialize 'ChartToImageConverter' to convert charts in the slides, and this is optional
pptxDoc.ChartToImageConverter = New ChartToImageConverter()
'Initializes the 'SubstituteFont' event to set the replacement font
AddHandler pptxDoc.FontSettings.SubstituteFont, AddressOf SubstituteFont
'Convert the PowerPoint presentation to PDF file
Dim pdfDoc As PdfDocument = PresentationToPdfConverter.Convert(pptxDoc)
'Save the PDF file.
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

{% highlight c# tabtitle="ASP.NET Core" %}
//Load the PowerPoint presentation as stream
using (FileStream fileStream = new FileStream("Sample.pptx", FileMode.Create))
{
    //Load the PowerPoint presentation from stream
    using (IPresentation pptxDoc = Presentation.Open(fileStream))
    {
        // Initializes the 'SubstituteFont' event to set the replacement font
        pptxDoc.FontSettings.SubstituteFont += SubstituteFont;
        //Convert the PowerPoint presentation to PDF file
        PdfDocument pdfDocument = PresentationToPdfConverter.Convert(pptxDoc);
        //Create new instance of file stream
        FileStream pdfStream = new FileStream("Output.pdf", FileMode.Create);
        //Save the generated PDF to file stream
        pdfDocument.Save(pdfStream);
        //Release all resources
        pdfStream.Dispose();
        pdfDocument.Close(true);
    }
}
/// <summary>
/// Sets the alternate font when a specified font is unavailable in the production environment
/// </summary>
/// <param name="sender">FontSettings type of the Presentation in which the specified font is used but unavailable in production environment. </param>
/// <param name="args">Retrieves the unavailable font name and receives the substitute font name for conversion. </param>
private static void SubstituteFont(object sender, SubstituteFontEventArgs args)
{
    if (args.OriginalFontName == "Arial Unicode MS")
        args.AlternateFontName = "Arial";
    else
        args.AlternateFontName = "Times New Roman";
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens the PowerPoint presentation
using (IPresentation pptxDoc = Presentation.Open(assembly.GetManifestResourceStream("GettingStarted.Assets.Sample.pptx")))
{
    // Initializes the 'SubstituteFont' event to set the replacement font
    pptxDoc.FontSettings.SubstituteFont += SubstituteFont;
    //Convert PowerPoint presentation to PDF
    PdfDocument pdfDocument = PresentationToPdfConverter.Convert(pptxDoc);
    //Create new instance of  MemoryStream
    MemoryStream stream = new MemoryStream(); 
    //Save the Pdf to memory stream
    pdfDocument.Save(stream);
    stream.Position = 0;
    //Save the stream as a file in the device and invoke it for viewing
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.pdf", "application/pdf", stream);
}
/// <summary>
/// Sets the alternate font when a specified font is unavailable in the production environment
/// </summary>
/// <param name="sender">FontSettings type of the Presentation in which the specified font is used but unavailable in production environment. </param>
/// <param name="args">Retrieves the unavailable font name and receives the substitute font name for conversion. </param>
private static void SubstituteFont(object sender, SubstituteFontEventArgs args)
{
    if (args.OriginalFontName == "Arial Unicode MS")
        args.AlternateFontName = "Arial";
    else
        args.AlternateFontName = "Times New Roman";
}
{% endhighlight %}

{% endtabs %}

### Upload font stream

The following code example demonstrates how to upload a font stream for missing font while converting a PowerPoint presentation to PDF. The provided alternate font stream is not mandatory to be installed in the production environment.

{% tabs %}

{% highlight c# tabtitle="C#" %}
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
/// Sets the alternate font stream when a specified font is unavailable in the production environment
/// </summary>
/// <param name="sender">FontSettings type of the Presentation in which the specified font stream is used but unavailable in production environment. </param>
/// <param name="args">Retrieves the unavailable font name and receives the substitute font stream for conversion. </param>
private static void FontSettings_SubstituteFont(object sender, SubstituteFontEventArgs args)
{
    if (args.OriginalFontName == "Arial" && args.FontStyle == FontStyle.Bold)
        args.AlternateFontStream = new FileStream("cambriab.ttf", FileMode.Open);
    else if (args.OriginalFontName == "Arial" && args.FontStyle == FontStyle.Regular)
        args.AlternateFontStream = new FileStream("BROADW.TTF", FileMode.Open);
    else
        args.AlternateFontStream = new FileStream("COOPBL.TTF", FileMode.Open);
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Load the PowerPoint presentation and convert to PDF
Dim pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
'Initialize 'ChartToImageConverter' to convert charts in the slides, and this is optional
pptxDoc.ChartToImageConverter = New ChartToImageConverter()
'Initializes the 'SubstituteFont' event to set the replacement font
AddHandler pptxDoc.FontSettings.SubstituteFont, AddressOf SubstituteFont
'Convert the PowerPoint presentation to PDF file
Dim pdfDoc As PdfDocument = PresentationToPdfConverter.Convert(pptxDoc)
'Save the PDF file.
pdfDoc.Save("Sample.pdf")
'Dispose the PowerPoint presentation instance
pptxDoc.Dispose()
'Dispose the PDF document instance
pdfDoc.Dispose()
''' <summary>
''' Sets the alternate font stream when a specified font is unavailable in the production environment
''' </summary>
''' <param name="sender">FontSettings type of the Presentation in which the specified font stream is used but unavailable in production environment.</param>
''' <param name="args">Retrieves the unavailable font name and receives the substitute font stream for conversion. </param>
Private Sub SubstituteFont(ByVal sender As Object, ByVal args As SubstituteFontEventArgs)
    ' Sets the alternate font when a specified font is not installed in the production environment
    If args.OriginalFontName = "Arial" AndAlso args.FontStyle = FontStyle.Bold Then
        args.AlternateFontStream = New FileStream("cambriab.ttf", FileMode.Open)
    ElseIf args.OriginalFontName = "Arial" AndAlso args.FontStyle = FontStyle.Regular Then
        args.AlternateFontStream = New FileStream("BROADW.TTF", FileMode.Open)
    Else
        args.AlternateFontStream = New FileStream("COOPBL.TTF", FileMode.Open)
    End If
End Sub
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Load the PowerPoint presentation as stream
using (FileStream fileStream = new FileStream("Sample.pptx", FileMode.Create))
{
    //Load the PowerPoint presentation from stream
    using (IPresentation pptxDoc = Presentation.Open(fileStream))
    {
        // Initializes the 'SubstituteFont' event to set the replacement font
        pptxDoc.FontSettings.SubstituteFont += SubstituteFont;
        //Convert the PowerPoint presentation to PDF file
        PdfDocument pdfDocument = PresentationToPdfConverter.Convert(pptxDoc);
        //Create new instance of file stream
        FileStream pdfStream = new FileStream("Output.pdf", FileMode.Create);
        //Save the generated PDF to file stream
        pdfDocument.Save(pdfStream);
        //Release all resources
        pdfStream.Dispose();
        pdfDocument.Close(true);
    }
}
/// <summary>
/// Sets the alternate font stream when a specified font is unavailable in the production environment
/// </summary>
/// <param name="sender">FontSettings type of the Presentation in which the specified font stream is used but unavailable in production environment. </param>
/// <param name="args">Retrieves the unavailable font name and receives the substitute font stream for conversion. </param>
private static void FontSettings_SubstituteFont(object sender, SubstituteFontEventArgs args)
{
    if (args.OriginalFontName == "Arial" && args.FontStyle == FontStyle.Bold)
        args.AlternateFontStream = new FileStream("cambriab.ttf", FileMode.Open);
    else if (args.OriginalFontName == "Arial" && args.FontStyle == FontStyle.Regular)
        args.AlternateFontStream = new FileStream("BROADW.TTF", FileMode.Open);
    else
        args.AlternateFontStream = new FileStream("COOPBL.TTF", FileMode.Open);
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens the PowerPoint presentation
using (IPresentation pptxDoc = Presentation.Open(assembly.GetManifestResourceStream("GettingStarted.Assets.Sample.pptx")))
{
    // Initializes the 'SubstituteFont' event to set the replacement font
    pptxDoc.FontSettings.SubstituteFont += SubstituteFont;
    //Convert PowerPoint presentation to PDF
    PdfDocument pdfDocument = PresentationToPdfConverter.Convert(pptxDoc);
    //Create new instance of  MemoryStream
    MemoryStream stream = new MemoryStream();
    //Save the Pdf to memory stream
    pdfDocument.Save(stream);
    stream.Position = 0;
    //Save the stream as a file in the device and invoke it for viewing
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.pdf", "application/pdf", stream);
}
/// <summary>
/// Sets the alternate font stream when a specified font is unavailable in the production environment
/// </summary>
/// <param name="sender">FontSettings type of the Presentation in which the specified font stream is used but unavailable in production environment. </param>
/// <param name="args">Retrieves the unavailable font name and receives the substitute font stream for conversion. </param>
private static void FontSettings_SubstituteFont(object sender, SubstituteFontEventArgs args)
{
    //"App" is the class of Portable project.
    Assembly assembly = typeof(App).GetTypeInfo().Assembly;
    if (args.OriginalFontName == "Arial" && args.FontStyle == FontStyle.Bold)
        args.AlternateFontStream = assembly.GetManifestResourceStream("GettingStarted.Assets.cambriab.ttf");
    else if (args.OriginalFontName == "Arial" && args.FontStyle == FontStyle.Regular)
        args.AlternateFontStream = assembly.GetManifestResourceStream("GettingStarted.Assets.BROADW.TTF");
    else
        args.AlternateFontStream = assembly.GetManifestResourceStream("GettingStarted.Assets.COOPBL.TTF");
}
{% endhighlight %}
{% endtabs %}

## Fallback fonts

When a glyph of input text is unavailable in mentioned font, text will not be preserved in PPTX to PDF conversion. To avoid this, Syncfusion PowerPoint library allows you to use a fallback font to preserve the text properly in PPTX to PDF conversion.

### Initialize Fallback Fonts

The following code example demonstrates how to initialize a default fallback font while converting a PowerPoint presentation to PDF.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Opens a PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open("Sample.pptx");
//Initialize the conversion settings
PresentationToPdfConverterSettings pdfConverterSettings = new PresentationToPdfConverterSettings();
//Enable the portable rendering
pdfConverterSettings.EnablePortableRendering = true;
//Use a sets of default FallbackFont collection to IPresentation
pptxDoc.FontSettings.InitializeFallbackFonts();
//Converts the PowerPoint Presentation into PDF document with Portable rendering option
PdfDocument pdfDocument = PresentationToPdfConverter.Convert(pptxDoc);
//Saves the PDF document
pdfDocument.Save("Sample.pdf");
//Closes the PDF document
pdfDocument.Close(true);
//Closes the Presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Opens a PowerPoint Presentation
Dim pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
'Initialize the conversion settings
Dim pdfConverterSettings As PresentationToPdfConverterSettings = new PresentationToPdfConverterSettings()
'Enable the portable rendering.
pdfConverterSettings.EnablePortableRendering = true
'Use a sets of default FallbackFont collection to IPresentation
pptxDoc.FontSettings.InitializeFallbackFonts
'Converts the PowerPoint Presentation into PDF document
Dim pdfDocument As PdfDocument = PresentationToPdfConverter.Convert(pptxDoc)
'Saves the PDF document
pdfDocument.Save("Sample.pdf")
'Closes the PDF document
pdfDocument.Close(True)
'Closes the Presentation
pptxDoc.Close()
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Load the PowerPoint presentation into stream
using (FileStream fileStreamInput = new FileStream(@"Template.pptx", FileMode.Open, FileAccess.Read))
{
    //Open the existing PowerPoint presentation with loaded stream
    using (IPresentation pptxDoc = Presentation.Open(fileStreamInput))
    {
        //Use a sets of default FallbackFont collection to IPresentation.
        pptxDoc.FontSettings.InitializeFallbackFonts();
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

{% highlight c# tabtitle="Xamarin" %}
//Load the PowerPoint presentation into stream
using (FileStream fileStreamInput = new FileStream(@"Template.pptx", FileMode.Open, FileAccess.Read))
{
    //Open the existing PowerPoint presentation with loaded stream
    using (IPresentation pptxDoc = Presentation.Open(fileStreamInput))
    {
        //Use a sets of default FallbackFont collection to IPresentation
        pptxDoc.FontSettings.InitializeFallbackFonts();
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

### Customize Default Fallback Fonts

The following code example demonstrates how to customize default fallback font while converting a PowerPoint presentation to PDF.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Opens a PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open("Sample.pptx");
//Initialize the conversion settings
PresentationToPdfConverterSettings pdfConverterSettings = new PresentationToPdfConverterSettings();
//Enable the portable rendering
pdfConverterSettings.EnablePortableRendering = true;
//Use a sets of default FallbackFont collection to IPresentation
pptxDoc.FontSettings.InitializeFallbackFonts();
// Customize a default fallback font name
// Modify the Hebrew script default font name as "David"
pptxDoc.FontSettings.FallbackFonts[5].FontNames = "David";
//Converts the PowerPoint Presentation into PDF document
PdfDocument pdfDocument = PresentationToPdfConverter.Convert(pptxDoc);
//Saves the PDF document
pdfDocument.Save("Sample.pdf");
//Closes the PDF document
pdfDocument.Close(true);
//Closes the Presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Opens a PowerPoint Presentation
Dim pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
'Initialize the conversion settings
Dim pdfConverterSettings As PresentationToPdfConverterSettings = new PresentationToPdfConverterSettings()
'Enable the portable rendering.
pdfConverterSettings.EnablePortableRendering = true
'Use a sets of default FallbackFont collection to IPresentation
pptxDoc.FontSettings.InitializeFallbackFonts
' Customize a default fallback font name
' Modify the Hebrew script default font name as "David"
pptxDoc.FontSettings.FallbackFonts(5).FontNames = "David"
'Converts the PowerPoint Presentation into PDF document
Dim pdfDocument As PdfDocument = PresentationToPdfConverter.Convert(pptxDoc)
'Saves the PDF document
pdfDocument.Save("Sample.pdf")
'Closes the PDF document
pdfDocument.Close(True)
'Closes the Presentation
pptxDoc.Close()
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Load the PowerPoint presentation into stream.
using (FileStream fileStreamInput = new FileStream(@"Template.pptx", FileMode.Open, FileAccess.Read))
{
    //Open the existing PowerPoint presentation with loaded stream.
    using (IPresentation pptxDoc = Presentation.Open(fileStreamInput))
    {
        //Use a sets of default FallbackFont collection to IPresentation
        pptxDoc.FontSettings.InitializeFallbackFonts();
        // Customize a default fallback font name
        // Modify the Hebrew script default font name as "David"
        pptxDoc.FontSettings.FallbackFonts[5].FontNames = "David";
        //Create the MemoryStream to save the converted PDF.
        using (MemoryStream pdfStream = new MemoryStream())
        {
            //Convert the PowerPoint document to PDF document.
            using (PdfDocument pdfDocument = PresentationToPdfConverter.Convert(pptxDoc))
            {
                //Save the converted PDF document to MemoryStream.
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

{% highlight c# tabtitle="Xamarin" %}
//Load the PowerPoint presentation into stream.
using (FileStream fileStreamInput = new FileStream(@"Template.pptx", FileMode.Open, FileAccess.Read))
{
    //Open the existing PowerPoint presentation with loaded stream.
    using (IPresentation pptxDoc = Presentation.Open(fileStreamInput))
    {
        //Use a sets of default FallbackFont collection to IPresentation
        pptxDoc.FontSettings.InitializeFallbackFonts();
        // Customize a default fallback font name
        // Modify the Hebrew script default font name as "David"
        pptxDoc.FontSettings.FallbackFonts[5].FontNames = "David";
        //Create the MemoryStream to save the converted PDF.
        using (MemoryStream pdfStream = new MemoryStream())
        {
            //Convert the PowerPoint document to PDF document.
            using (PdfDocument pdfDocument = PresentationToPdfConverter.Convert(pptxDoc))
            {
                //Save the converted PDF document to MemoryStream.
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

### Add Custom Fallback Fonts

The following code example demonstrates how to add custom fallback fonts while converting a PowerPoint presentation to PDF.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Opens a PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open("Sample.pptx");
//Initialize the conversion settings
PresentationToPdfConverterSettings pdfConverterSettings = new PresentationToPdfConverterSettings();
//Enable the portable rendering
pdfConverterSettings.EnablePortableRendering = true;
//Add custom fallback font names
// Arabic
pptxDoc.FontSettings.FallbackFonts.Add(new FallbackFont(0x0600, 0x06ff, "Arial"));
// Hebrew
pptxDoc.FontSettings.FallbackFonts.Add(new FallbackFont(0x0590, 0x05ff, "Arial"));
// Hindi
pptxDoc.FontSettings.FallbackFonts.Add(new FallbackFont(0x0900, 0x097F, "Mangal"));
// Chinese
pptxDoc.FontSettings.FallbackFonts.Add(new FallbackFont(0x4E00, 0x9FFF, "DengXian"));
// Japanese
pptxDoc.FontSettings.FallbackFonts.Add(new FallbackFont(0x3040, 0x309F, "MS Mincho"));
// Korean
pptxDoc.FontSettings.FallbackFonts.Add(new FallbackFont(0xAC00, 0xD7A3, "Malgun Gothic"));
//Converts the PowerPoint Presentation into PDF document
PdfDocument pdfDocument = PresentationToPdfConverter.Convert(pptxDoc);
//Saves the PDF document
pdfDocument.Save("Sample.pdf");
//Closes the PDF document
pdfDocument.Close(true);
//Closes the Presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Opens a PowerPoint Presentation
Dim pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
'Initialize the conversion settings
Dim pdfConverterSettings As PresentationToPdfConverterSettings = new PresentationToPdfConverterSettings()
'Enable the portable rendering.
pdfConverterSettings.EnablePortableRendering = true
'Add custom fallback font names
' Arabic
pptxDoc.FontSettings.FallbackFonts.Add(New FallbackFont(1536, 1791, "Arial"))
' Hebrew
pptxDoc.FontSettings.FallbackFonts.Add(New FallbackFont(1424, 1535, "Arial"))
' Hindi
pptxDoc.FontSettings.FallbackFonts.Add(New FallbackFont(2304, 2431, "Mangal"))
' Chinese
pptxDoc.FontSettings.FallbackFonts.Add(New FallbackFont(19968, 40959, "DengXian"))
' Japanese
pptxDoc.FontSettings.FallbackFonts.Add(New FallbackFont(12352, 12447, "MS Mincho"))
' Korean
pptxDoc.FontSettings.FallbackFonts.Add(New FallbackFont(44032, 55203, "Malgun Gothic"))
'Converts the PowerPoint Presentation into PDF document
Dim pdfDocument As PdfDocument = PresentationToPdfConverter.Convert(pptxDoc)
'Saves the PDF document
pdfDocument.Save("Sample.pdf")
'Closes the PDF document
pdfDocument.Close(True)
'Closes the Presentation
pptxDoc.Close()
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Load the PowerPoint presentation into stream.
using (FileStream fileStreamInput = new FileStream(@"Template.pptx", FileMode.Open, FileAccess.Read))
{
    //Open the existing PowerPoint presentation with loaded stream.
    using (IPresentation pptxDoc = Presentation.Open(fileStreamInput))
    {
        //Add custom fallback font names
        // Arabic
        pptxDoc.FontSettings.FallbackFonts.Add(new FallbackFont(0x0600, 0x06ff, "Arial"));
        // Hebrew
        pptxDoc.FontSettings.FallbackFonts.Add(new FallbackFont(0x0590, 0x05ff, "Arial"));
        // Hindi
        pptxDoc.FontSettings.FallbackFonts.Add(new FallbackFont(0x0900, 0x097F, "Mangal"));
        // Chinese
        pptxDoc.FontSettings.FallbackFonts.Add(new FallbackFont(0x4E00, 0x9FFF, "DengXian"));
        // Japanese
        pptxDoc.FontSettings.FallbackFonts.Add(new FallbackFont(0x3040, 0x309F, "MS Mincho"));
        // Korean
        pptxDoc.FontSettings.FallbackFonts.Add(new FallbackFont(0xAC00, 0xD7A3, "Malgun Gothic"));
        //Create the MemoryStream to save the converted PDF.
        using (MemoryStream pdfStream = new MemoryStream())
        {
            //Convert the PowerPoint document to PDF document.
            using (PdfDocument pdfDocument = PresentationToPdfConverter.Convert(pptxDoc))
            {
                //Save the converted PDF document to MemoryStream.
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

{% highlight c# tabtitle="Xamarin" %}
//Load the PowerPoint presentation into stream
using (FileStream fileStreamInput = new FileStream(@"Template.pptx", FileMode.Open, FileAccess.Read))
{
    //Open the existing PowerPoint presentation with loaded stream
    using (IPresentation pptxDoc = Presentation.Open(fileStreamInput))
    {
        //Add custom fallback font names
        // Arabic
        pptxDoc.FontSettings.FallbackFonts.Add(new FallbackFont(0x0600, 0x06ff, "Arial"));
        // Hebrew
        pptxDoc.FontSettings.FallbackFonts.Add(new FallbackFont(0x0590, 0x05ff, "Arial"));
        // Hindi
        pptxDoc.FontSettings.FallbackFonts.Add(new FallbackFont(0x0900, 0x097F, "Mangal"));
        // Chinese
        pptxDoc.FontSettings.FallbackFonts.Add(new FallbackFont(0x4E00, 0x9FFF, "DengXian"));
        // Japanese
        pptxDoc.FontSettings.FallbackFonts.Add(new FallbackFont(0x3040, 0x309F, "MS Mincho"));
        // Korean
        pptxDoc.FontSettings.FallbackFonts.Add(new FallbackFont(0xAC00, 0xD7A3, "Malgun Gothic"));
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

N> 1. Fallback fonts only supported for Arabic, Hebrew, Hindi, Chinese, Japanese and Korean languages.
N> 2. Its only supported in [Direct PDF](https://help.syncfusion.com/file-formats/presentation/presentation-to-pdf#powerpoint-to-pdf-conversion-in-azure-platform) and [Portable](https://help.syncfusion.com/file-formats/presentation/presentation-to-pdf) PDF conversion modules.

## Show Warning for unsupported elements

The Presentation library shows warning message about the unsupported elements such as Metafile images and charts (supported from .NET Standard 2.0) present in the input PowerPoint presentation, during PowerPoint to PDF conversion. It also allows you to cancel or continue the PowerPoint to PDF conversion, when any unsupported elements is present in the input PowerPoint presentation.

The following code example demonstrates how to cancel or continue the PowerPoint presentation to PDF conversion, when an unsupported elements (Metafile and Chart) are present in the input PowerPoint presentation.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Essential Presentation library supports Show warning for unsupported elements feature in ASP.NET Core, Blazor server-side application and Xamarin platforms alone.
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
//Essential Presentation supports library Show warning for unsupported elements feature in ASP.NET Core, Blazor server-side application and Xamarin platforms alone.
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
// Open the file as Stream
using (FileStream pptStream = new FileStream("Template.pptx", FileMode.Open, FileAccess.Read))
{
    //Open the existing PowerPoint presentation with loaded stream.
    using (IPresentation pptxDoc = Presentation.Open(pptStream))
    {
        //Instantiation of PresentationToPdfConverterSettings
        PresentationToPdfConverterSettings settings = new PresentationToPdfConverterSettings();
        //Gets all the warnings into the collection
        settings.Warning = new DocumentWarning();
        //Converts the PowerPoint Presentation into PDF document
        using (PdfDocument pdfDocument = PresentationToPdfConverter.Convert(pptxDoc, settings))
        {
            //If the PowerPoint to Pdf conversion has been stopped, IsCanceled value will be True, otherwise false
            if (!PresentationToPdfConverter.IsCanceled)
            {
                //Saves the PDF file
                using (FileStream outputStream = new FileStream("Output.pdf", FileMode.OpenOrCreate, FileAccess.ReadWrite))
                {
                    pdfDocument.Save(outputStream);
                    outputStream.Position = 0;
                }
            }
            else
            {
                Console.WriteLine("PowerPoint to PDF conversion is stopped , please press any key to exit the application");
                Console.ReadKey();
            }
        }
    }
}
/// <summary>
/// DocumentWarning class implements the IWarning interface
/// </summary>
/// <seealso cref="IWarning" />
public class DocumentWarning : IWarning
{
    /// <summary>
    /// Gets the Boolen value whether to continue conversion or not
    /// </summary>
    /// <param name="warningInfo">Collection of warnings</param>
    /// <returns></returns>
    public bool ShowWarnings(List<WarningInfo> warningInfo)
    {
        //By default to perform the PowerPoint to PDF conversion by setting the isContinueConversion as true.
        bool isContinueConversion = true;
        foreach (WarningInfo warning in warningInfo)
        {
            //Since there are warnings in the PowerPoint presentation the value of isContinueConversion will be set as false.
            isContinueConversion = false;
            //Print the description of the Warining
            Console.WriteLine(warning.Description);
            if (warning.Description.Contains("Metafile") || warning.Description.Contains("Chart"))
            {
                Console.WriteLine("Type [Y] if you want Do you want to continue Presentation to Pdf conversion or Type [N] to cancel the conversion");
                String confrimation = Console.ReadLine();
                //Based on warning.WarningType enumeration, you can do your manipulation.
                //Skips the PowerPoint to Pdf conversion by setting isContinueConversion value as false.
                //Continue the PowerPoint to PDF conversion by setting the isContinueConversion as true.
                if (confrimation.ToLower().Equals("y"))
                    isContinueConversion = true;
                else
                    isContinueConversion = false;
            }
        }
        return isContinueConversion;
    }
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
// Open the file as Stream
using (FileStream pptStream = new FileStream("Template.pptx", FileMode.Open, FileAccess.Read))
{
    //Open the existing PowerPoint presentation with loaded stream.
    using (IPresentation pptxDoc = Presentation.Open(pptStream))
    {
        //Instantiation of PresentationToPdfConverterSettings
        PresentationToPdfConverterSettings settings = new PresentationToPdfConverterSettings();
        //Gets all the warnings into the collection
        settings.Warning = new DocumentWarning();
        //Converts the PowerPoint Presentation into PDF document
        using (PdfDocument pdfDocument = PresentationToPdfConverter.Convert(pptxDoc, settings))
        {
            //If the PowerPoint to Pdf conversion has been stopped, IsCanceled value will be True and PDF document will not get generated, Otherwise false, then the PDF document will get generated and can be viewed.
            if (!PresentationToPdfConverter.IsCanceled)
            {
                //Saves the PDF file
                using (FileStream outputStream = new FileStream("Output.pdf", FileMode.OpenOrCreate, FileAccess.ReadWrite))
                {
                    pdfDocument.Save(outputStream);
                    outputStream.Position = 0;
                    //Save the stream as a file in the device and invoke it for viewing
                    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.pdf", "application/pdf", outputStream);
                }
            }
        }
    }
}
/// <summary>
/// DocumentWarning class implements the IWarning interface
/// </summary>
/// <seealso cref="IWarning" />
public class DocumentWarning : IWarning
{
    /// <summary>
    /// Gets the Boolen value whether to continue conversion or not
    /// </summary>
    /// <param name="warningInfo">Collection of warnings</param>
    /// <returns></returns>
    public bool ShowWarnings(List<WarningInfo> warningInfo)
    {
        //By default to perform the PowerPoint to PDF conversion by setting the isContinueConversion as true.
        bool isContinueConversion = true;
        foreach (WarningInfo warning in warningInfo)
        {
            //Since there are warnings in the PowerPoint presentation the value of isContinueConversion will be set as false.
            isContinueConversion = false;
            //Based on warning.WarningType enumeration, you can do your manipulation.
            if (warning.Description.Contains("Metafile") || warning.Description.Contains("Chart"))
            {
                //Continue the PowerPoint to PDF conversion by setting the isContinueConversion as true.
                isContinueConversion = true;
            }
        }
        return isContinueConversion;
    }
}
{% endhighlight %}
{% endtabs %}

## Handouts

The Presentation library allows you to convert a PowerPoint presentation to PDF document with [Handouts](https://help.syncfusion.com/cr/file-formats/Syncfusion.PresentationToPdfConverter.PublishOptions.html) option. Thus, the library allows selecting the number of slides to be included per PDF page. This helps converting multiple PowerPoint slides within a single PDF page. 
 
The following code sample demonstrates how to convert a PowerPoint presentation to PDF document with [Handouts](https://help.syncfusion.com/cr/file-formats/Syncfusion.PresentationToPdfConverter.PublishOptions.html) property.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Load the PowerPoint presentation to convert.
IPresentation pptxDoc = Presentation.Open("Sample.pptx");
//Enable the handouts and number of pages per slide options in converter settings.
PresentationToPdfConverterSettings pdfConverterSettings = new PresentationToPdfConverterSettings();
pdfConverterSettings.PublishOptions = PublishOptions.Handouts;
pdfConverterSettings.SlidesPerPage = SlidesPerPage.Nine;
//Convert the documents by passing the PDF conversion settings as parameter.
PdfDocument pdfDoc = PresentationToPdfConverter.Convert(pptxDoc, pdfConverterSettings);
//Save the converted PDF document.
pdfDoc.Save("Sample.pdf");
//Close the presentation instance
pptxDoc.Close();
//Close the PDF instance
pdfDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Load the PowerPoint presentation to convert.
Dim pptxDoc As IPresentation  = Presentation.Open("Sample.pptx")
'Enable the handouts and number of pages per slide options in converter settings.
Dim pdfConverterSettings As PresentationToPdfConverterSettings  = new PresentationToPdfConverterSettings()
pdfConverterSettings.PublishOptions = PublishOptions.Handouts
pdfConverterSettings.SlidesPerPage = SlidesPerPage.Nine
'Convert the documents by passing the PDF conversion settings as parameter.
Dim pdfDoc As PdfDocument  = PresentationToPdfConverter.Convert(pptxDoc, pdfConverterSettings)
'Save the converted PDF document.
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

{% highlight c# tabtitle="C#" %}
//Load the PowerPoint presentation to convert.
IPresentation pptxDoc = Presentation.Open("Sample.pptx");
//Enable the include hidden slides option in converter settings.
PresentationToPdfConverterSettings pdfConverterSettings = new PresentationToPdfConverterSettings();
pdfConverterSettings.PublishOptions = PublishOptions.NotesPages;
//Convert the documents by passing the settings as parameter.
PdfDocument pdfDoc = PresentationToPdfConverter.Convert(pptxDoc, pdfConverterSettings);
//Save the converted PDF file.
pdfDoc.Save("Sample.pdf");
//Close the presentation instance
pptxDoc.Close();
//Close the PDF instance
pdfDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Load the PowerPoint presentation to convert.
Dim pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
'Enable the include hidden slides option in converter settings.
Dim pdfConverterSettings As PresentationToPdfConverterSettings pdfConverterSettings = new PresentationToPdfConverterSettings()
pdfConverterSettings.PublishOptions = PublishOptions.NotesPages
'Convert the documents by passing the settings as parameter.
Dim pdfDoc As PdfDocument = PresentationToPdfConverter.Convert(pptxDoc, pdfConverterSettings)
'Save the converted PDF file.
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

{% highlight c# tabtitle="C#" %}

//Load the PowerPoint presentation to convert.
IPresentation pptxDoc = Presentation.Open("Sample.pptx");
//Enable or disable including the hidden slides option in converter settings.
PresentationToPdfConverterSettings pdfConverterSettings = new PresentationToPdfConverterSettings();
pdfConverterSettings.ShowHiddenSlides = true;
//Convert the documents by passing the settings as parameter.
PdfDocument pdfDoc = PresentationToPdfConverter.Convert(pptxDoc, pdfConverterSettings);
//Save the converted PDF file.
pdfDoc.Save("Sample.pdf");
//Close the presentation instance
pptxDoc.Close();
//Close the PDF instance
pdfDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Load the PowerPoint presentation to convert.
Dim pptxDoc As IPresentation  = Presentation.Open("Sample.pptx")
'Enable or disable including the hidden slides option in converter settings.
Dim pdfConverterSettings As PresentationToPdfConverterSettings  = new PresentationToPdfConverterSettings()
pdfConverterSettings.ShowHiddenSlides = true
'Convert the documents by passing the settings as parameter.
Dim pdfDoc As PdfDocument  = PresentationToPdfConverter.Convert(pptxDoc, pdfConverterSettings)
'Save the converted PDF file.
pdfDoc.Save("Sample.pdf")
'Close the presentation instance
pptxDoc.Close()
'Close the PDF instance
pdfDoc.Close()
{% endhighlight %}

{% endtabs %}

## Recreate Nested Metafile

This setting allows you to regenerate the nested EMF images in the PowerPoint presentation document during PDF conversion.

This property is recommended to resolve the scaling problem of the nested metafile images by regenerating the nested metafile images present in the PowerPoint presentation document.

The following code sample shows how to use this property to regenerate the nested EMF images in the PowerPoint presentation document during PDF conversion.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Open a PowerPoint Presentation.
using (IPresentation pptxDoc = Presentation.Open("Sample.pptx"))
{
    //Create an instance of the ChartToImageConverter and assign it to the ChartToImageConverter property of the Presentation.
    pptxDoc.ChartToImageConverter = new ChartToImageConverter();
    //Initialize the conversion settings.
    PresentationToPdfConverterSettings pdfConverterSettings = new PresentationToPdfConverterSettings();
    //Set the RecreateNestedMetafile property to true to recreate the nested metafile automatically.          
    pdfConverterSettings.RecreateNestedMetafile = true;
    //Convert the PowerPoint Presentation into a PDF document.
    using (PdfDocument pdfDocument = PresentationToPdfConverter.Convert(pptxDoc, pdfConverterSettings))
    {
        //Save a PDF document.
        pdfDocument.Save("Sample.pdf");
    }
}

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Open a PowerPoint Presentation.
Using pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
    'Create an instance of the ChartToImageConverter and assign it to the ChartToImageConverter property of the Presentation.
    pptxDoc.ChartToImageConverter = New ChartToImageConverter()
    'Initialize the conversion settings.
    Dim pdfConverterSettings As PresentationToPdfConverterSettings = New PresentationToPdfConverterSettings()
    'Set the RecreateNestedMetafile property to true to recreate the nested metafile automatically.
    pdfConverterSettings.RecreateNestedMetafile = True
    'Convert the PowerPoint Presentation into a PDF document.
    Using pdfDocument As PdfDocument = PresentationToPdfConverter.Convert(pptxDoc, pdfConverterSettings)
        'Save a PDF document.
        pdfDocument.Save("Sample.pdf")
    End Using
End Using

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

{% highlight c# tabtitle="C#" %}
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

{% highlight vb.net tabtitle="VB.NET" %}
'Load the PowerPoint presentation to convert.
Dim pptxDoc As IPresentation  = Presentation.Open("Sample.pptx")
'Enable or disable including the hidden slides option in converter settings.
Dim pdfConverterSettings As PresentationToPdfConverterSettings  = new PresentationToPdfConverterSettings()
'Set the Pdf conformance level to A1B
pdfConverterSettings.PdfConformanceLevel = PdfConformanceLevel.Pdf_A1B
'Convert the documents by passing the settings as parameter.
Dim pdfDoc As PdfDocument  = PresentationToPdfConverter.Convert(pptxDoc, pdfConverterSettings)
'Save the converted PDF file.
pdfDoc.Save("Sample.pdf")
'Close the presentation instance
pptxDoc.Close()
'Close the PDF instance
pdfDoc.Close()
{% endhighlight %}

{% endtabs %}

## Accessible PDF document

This setting allows you to determine whether to preserve structured document tags in the converted PDF document for accessibility **(508 or PDF/UA compliance)** support. This property will set the title and description for images, diagrams, and other objects in the generated PDF document. This information will be helpful for **people with vision or cognitive impairments** who may not be able to see or understand the object.

The following code sample shows how to preserve structured document tags in the converted PDF document.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Open a PowerPoint Presentation.
using (IPresentation pptxDoc = Presentation.Open("Sample.pptx"))
{
    //Create an instance of the ChartToImageConverter and assign it to the ChartToImageConverter property of the Presentation.
    pptxDoc.ChartToImageConverter = new ChartToImageConverter();
    //Initialize the conversion settings.
    PresentationToPdfConverterSettings pdfConverterSettings = new PresentationToPdfConverterSettings();
    //Enable a flag to preserve structured document tags in the converted PDF document.               
    pdfConverterSettings.AutoTag = true;
    //Convert the PowerPoint Presentation into a PDF document.
    using (PdfDocument pdfDocument = PresentationToPdfConverter.Convert(pptxDoc, pdfConverterSettings))
    {
        //Save a PDF document.
        pdfDocument.Save("Sample.pdf");
    }
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Open a PowerPoint Presentation.
Using pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
    'Create an instance of the ChartToImageConverter and assign it to the ChartToImageConverter property of the Presentation.
    pptxDoc.ChartToImageConverter = New ChartToImageConverter()
    'Initialize the conversion settings.
    Dim pdfConverterSettings As PresentationToPdfConverterSettings = New PresentationToPdfConverterSettings()
    'Enable a flag to preserve structured document tags in the converted PDF document.
    pdfConverterSettings.AutoTag = True
    'Convert the PowerPoint Presentation into a PDF document.
    Using pdfDocument As PdfDocument = PresentationToPdfConverter.Convert(pptxDoc, pdfConverterSettings)
        'Save a PDF document.
        pdfDocument.Save("Sample.pdf")
    End Using
End Using
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Load the PowerPoint presentation into a stream.
using (FileStream fileStreamInput = new FileStream("Sample.pptx", FileMode.Open, FileAccess.Read))
{
    //Open the existing PowerPoint presentation with the loaded stream.
    using (IPresentation pptxDoc = Presentation.Open(fileStreamInput))
    {
        //Instantiation of the PresentationToPdfConverterSettings.
        PresentationToPdfConverterSettings pdfConverterSettings = new PresentationToPdfConverterSettings();
        //Enable a flag to preserve structured document tags in the converted PDF document.               
        pdfConverterSettings.AutoTag = true;
        //Convert the PowerPoint document to a PDF document.
        using (PdfDocument pdfDocument = PresentationToPdfConverter.Convert(pptxDoc, pdfConverterSettings))
        {
            //Save the converted PDF document to the fileStream.
            using (FileStream fileStreamOutput = File.Create("Sample.pdf"))
            {
                pdfDocument.Save(fileStreamOutput);
                fileStreamOutput.Position = 0;
            }
        }
    }
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//The "App" is the class of the Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Open a PowerPoint presentation.
using (IPresentation pptxDoc = Presentation.Open(assembly.GetManifestResourceStream("GettingStarted.Assets.Sample.pptx")))
{
    //Instantiation of the PresentationToPdfConverterSettings.
    PresentationToPdfConverterSettings pdfConverterSettings = new PresentationToPdfConverterSettings();
    //Enable a flag to preserve structured document tags in the converted PDF document.               
    pdfConverterSettings.AutoTag = true;
    //Convert the PowerPoint Presentation into a PDF document.
    using (PdfDocument pdfDocument = PresentationToPdfConverter.Convert(pptxDoc, pdfConverterSettings))
    {
        //Save the converted PDF document to the MemoryStream.
        MemoryStream outputStream = new MemoryStream();
        pdfDocument.Save(outputStream);
        outputStream.Position = 0;
        //Save the stream as a file in the device and invoke it for viewing.
        Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.pdf", "application/pdf", outputStream);
    }
}
{% endhighlight %}

{% endtabs %}

## Chart quality

The Presentation library provides an option to decide the quality of the charts to optimize the converted PDF document size. 

N> 1. The default [ScalingMode](https://help.syncfusion.com/cr/file-formats/Syncfusion.OfficeChartToImageConverter.ChartToImageConverter.html#Syncfusion_OfficeChartToImageConverter_ChartToImageConverter_ScalingMode) for charts is [ScalingMode.Normal](https://help.syncfusion.com/cr/file-formats/Syncfusion.OfficeChart.ScalingMode.html). 
N> 2. Setting the [Best](https://help.syncfusion.com/cr/file-formats/Syncfusion.OfficeChart.ScalingMode.html) scaling mode will improve the quality of the converted charts and increase the converted PDF document size.

The following code sample demonstrates how to set the quality of the charts while PowerPoint presentation to PDF conversion

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Load the PowerPoint presentation to convert.
IPresentation pptxDoc = Presentation.Open("Sample.pptx");
//Create an instance of ChartToImageConverter and assigns it to ChartToImageConverter property of Presentation
pptxDoc.ChartToImageConverter = new ChartToImageConverter();
//Sets the scaling mode of the chart to best. 
pptxDoc.ChartToImageConverter.ScalingMode = ScalingMode.Best;
//Convert the documents by passing the PDF conversion settings as parameter.
PdfDocument pdfDoc = PresentationToPdfConverter.Convert(pptxDoc);          
//Save the converted PDF document.
pdfDoc.Save("Sample.pdf");
//Close the presentation instance
pptxDoc.Close();
//Close the PDF instance
pdfDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Load the PowerPoint presentation to convert.
Dim pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
'Create an instance of ChartToImageConverter and assigns it to ChartToImageConverter property of Presentation
pptxDoc.ChartToImageConverter = new ChartToImageConverter()
'Sets the scaling mode of the chart to best. 
pptxDoc.ChartToImageConverter.ScalingMode = ScalingMode.Best
'Convert the documents by passing the PDF conversion settings as parameter.
Dim pdfDoc As PdfDocument = PresentationToPdfConverter.Convert(pptxDoc)          
'Save the converted PDF document.
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

{% highlight c# tabtitle="C#" %}
//Load the PowerPoint presentation to convert.
IPresentation pptxDoc = Presentation.Open("Sample.pptx");
//Enable the include hidden slides option in converter settings.
PresentationToPdfConverterSettings pdfConverterSettings = new PresentationToPdfConverterSettings();
//Set the flag to optimize the identical images
pdfConverterSettings.OptimizeIdenticalImages = true;
//Convert the documents by passing the settings as parameter.
PdfDocument pdfDoc = PresentationToPdfConverter.Convert(pptxDoc, pdfConverterSettings);
//Save the converted PDF file.
pdfDoc.Save("Sample.pdf");
//Close the presentation instance
pptxDoc.Close();
//Close the PDF instance
pdfDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Load the PowerPoint presentation to convert.
Dim pptxDoc As IPresentation  = Presentation.Open("Sample.pptx")
'Enable the include hidden slides option in converter settings.
Dim pdfConverterSettings As PresentationToPdfConverterSettings  = new PresentationToPdfConverterSettings()
'Set the flag to optimize the identical images
pdfConverterSettings.OptimizeIdenticalImages = true
'Convert the documents by passing the settings as parameter.
Dim pdfDoc As PdfDocument = PresentationToPdfConverter.Convert(pptxDoc, pdfConverterSettings)
Save the converted PDF file.
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

{% highlight c# tabtitle="C#" %}
//Load the PowerPoint presentation to convert.
IPresentation pptxDoc = Presentation.Open("Sample.pptx");
//Enable the include hidden slides option in converter settings.
PresentationToPdfConverterSettings pdfConverterSettings = new PresentationToPdfConverterSettings();
//Set the image resolution
pdfConverterSettings.ImageResolution = 100;
//Set the image quality
pdfConverterSettings.ImageQuality = 100;
//Convert the documents by passing the settings as parameter.
PdfDocument pdfDoc = PresentationToPdfConverter.Convert(pptxDoc, pdfConverterSettings);
//Save the converted PDF file.
pdfDoc.Save("Sample.pdf");
//Close the presentation instance
pptxDoc.Close();
//Close the PDF instance
pdfDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Load the PowerPoint presentation to convert.
Dim pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
'Enable the include hidden slides option in converter settings.
Dim pdfConverterSettings As PresentationToPdfConverterSettings = new PresentationToPdfConverterSettings()
'Set the image resolution
pdfConverterSettings.ImageResolution = 100
'Set the image quality
pdfConverterSettings.ImageQuality = 100
'Convert the documents by passing the settings as parameter.
Dim pdfDoc As PdfDocument = PresentationToPdfConverter.Convert(pptxDoc, pdfConverterSettings)
'Save the converted PDF file.
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

{% highlight c# tabtitle="C#" %}
//Load the PowerPoint document
IPresentation pptxDoc = Presentation.Open("Table.pptx");
//Initialize the conversion settings
PresentationToPdfConverterSettings pdfConverterSettings = new PresentationToPdfConverterSettings();
//Enable the portable rendering.
pdfConverterSettings.EnablePortableRendering = true;
//Convert the PowerPoint document to PDF
PdfDocument pdfDoc = PresentationToPdfConverter.Convert(pptxDoc,pdfConverterSettings);
//Save the converted PDF file.
pdfDoc.Save("Sample.pdf");
//Close the presentation instance
pptxDoc.Close();
//Close the PDF instance
pdfDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Load the PowerPoint document
Dim pptxDoc As IPresentation = Presentation.Open("Table.pptx")
'Initialize the conversion settings
Dim pdfConverterSettings As PresentationToPdfConverterSettings = new PresentationToPdfConverterSettings()
'Enable the portable rendering.
pdfConverterSettings.EnablePortableRendering = true
'Convert the PowerPoint document to PDF
Dim pdfDoc As PdfDocument = PresentationToPdfConverter.Convert(pptxDoc,pdfConverterSettings)
'Save the converted PDF file.
pdfDoc.Save("Sample.pdf")
'Close the presentation instance
pptxDoc.Close()
'Close the PDF instance
pdfDoc.Close()
{% endhighlight %}

{% endtabs %}

## See Also

* [How to convert PPTX to PDF in Blazor WebAssembly (WASM)?](https://www.syncfusion.com/kb/13883/how-to-convert-pptx-to-pdf-in-blazor-webassembly-wasm)