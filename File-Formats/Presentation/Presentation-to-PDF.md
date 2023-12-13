---
title: .NET PowerPoint Framework - Convert PowerPoint to PDF | Syncfusion
description: This section illustrates how to convert PowerPoint Presentation document to PDF in .NET PowerPoint Framework.
platform: file-formats
control: PowerPoint
documentation: UG
---
# PowerPoint Presentation to PDF conversion in File Formats

PowerPoint allows you to convert an entire Presentation or a single slide into PDF document. Refer to the following links for assemblies/nuget packages required based on platforms to [convert PowerPoint document into PDF](https://www.syncfusion.com/document-processing/powerpoint-framework/net/powerpoint-to-pdf-conversion).

* [Assemblies Information](https://help.syncfusion.com/file-formats/presentation/assemblies-required)
* [NuGet Information](https://help.syncfusion.com/file-formats/presentation/nuget-packages-required#converting-powerpoint-presentation-into-pdf)

To quickly start converting a PowerPoint Presentation to a PDF using .NET PowerPoint libray, please check out this video:
{% youtube "https://www.youtube.com/watch?v=nytscOICpWk" %}

[PresentationToPdfConverter](https://help.syncfusion.com/cr/file-formats/Syncfusion.PresentationToPdfConverter.PresentationToPdfConverter.html) class is responsible for converting an entire Presentation or a slide into PDF. The following code example demonstrates how to convert a PowerPoint presentation to PDF.

{% tabs %}

{% highlight C# tabtitle="C# [Cross-platform]" %}
//Namespaces to perform PPTX to PDF conversion
using Syncfusion.Pdf;
using Syncfusion.Presentation;
using Syncfusion.PresentationRenderer;
using System.IO;

//Load the PowerPoint presentation into stream.
using (FileStream fileStreamInput = new FileStream("Template.pptx", FileMode.Open, FileAccess.Read))
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

{% highlight C# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/PPTX-to-PDF-conversion/Convert-PowerPoint-presentation-to-PDF/.NET).

N> 1. Creating an instance of [ChartToImageConverter](https://help.syncfusion.com/cr/file-formats/Syncfusion.OfficeChartToImageConverter.ChartToImageConverter.html) class is mandatory to convert the charts present in the Presentation to PDF. Otherwise, the charts are not exported to the converted PDF
N> 2. The assembly "Syncfusion.SfChart.WPF" is non compliance with FIPS (Federal Information Processing Standard) algorithm policy.
N> 3. **In .NET Core targeting applications**, metafile images such as EMF and WMF have some limitations. So, those images will not preserve in Presentation document to PDF conversion using Essential Presentation. 

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

From v23.1.40, in addition to the previous NuGet packages, we recommend to use [SkiaSharp.NativeAssets.Linux v2.88.6](https://www.nuget.org/packages/SkiaSharp.NativeAssets.Linux/2.88.6) and [HarfBuzzSharp.NativeAssets.Linux v7.3.0](https://www.nuget.org/packages/HarfBuzzSharp.NativeAssets.Linux/7.3.0) NuGets to perform PowerPoint presentation to PDF conversion in Linux environment.

If you are using prior to v23.1.40 release, please refer [here](https://help.syncfusion.com/file-formats/presentation/faq#what-are-the-nuget-packages-to-be-installed-to-perform-powerpoint-presentation-to-pdf-conversion-in-linux-os) to know about how to perform PowerPoint presentation to PDF conversion in Linux.

## Font substitution for unavailable fonts

When a font used in a PowerPoint presentation is unavailable in the environment where it is converted to PDF, then the library substitutes the ‘Microsoft Sans Serif’ as a default font for text rendering. This leads to a difference in text layouts of PowerPoint presentation and the converted PDF document.  To avoid this, the Essential Presentation library allows you to set an alternate font for the missing font used in the PowerPoint presentation.

### Set alternate font

The following code example demonstrates how to set alternate font name for a missing font while converting a PowerPoint presentation to PDF. The provided alternate font should be installed in the production environment.

{% tabs %}

{% highlight C# tabtitle="C# [Cross-platform]" %}
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

{% highlight C# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/PPTX-to-PDF-conversion/Apply-substitution-font-name).

### Upload font stream

The following code example demonstrates how to upload a font stream for missing font while converting a PowerPoint presentation to PDF. The provided alternate font stream is not mandatory to be installed in the production environment.

{% tabs %}

{% highlight C# tabtitle="C# [Cross-platform]" %}
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

{% highlight C# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/PPTX-to-PDF-conversion/Apply-substitution-font-stream).

## Fallback fonts

During PowerPoint to PDF conversions, if a glyph of the input text is unavailable in the specified font, the text will not be rendered properly. To address this, the Syncfusion PowerPoint (Presentation) library allows users to specify fallback fonts. When a glyph is missing, the library will use one of the fallback fonts to render the text correctly in the output PDF document.

Users can configure fallback fonts in the following ways:
* Initialize default fallback fonts.
* Set custom fonts as fallback fonts for specific script types, including Arabic, Hebrew, Chinese, and Japanese etc.
* Set custom fonts as fallback fonts for a particular range of Unicode text.

N> Presentation internally uses user-initialized or specified fallback fonts for Unicode characters during PowerPoint to PDF conversion. Therefore, the specified fallback fonts must be installed in the production environment. Otherwise, it will not render the text properly using the fallback fonts.

### Initialize default fallback fonts

The following code example demonstrates how to initialize a default fallback font while converting a PowerPoint presentation to PDF. The *InitializeDefault* API sets the default fallback fonts for specific script types like Arabic, Hebrew, Chinese, Japanese etc.

{% tabs %}

{% highlight C# tabtitle="C# [Cross-platform]" %}
//Load the PowerPoint presentation into stream.
using (FileStream fileStreamInput = new FileStream("Template.pptx", FileMode.Open, FileAccess.Read))
{
    //Open the existing PowerPoint presentation with loaded stream.
    using (IPresentation pptxDoc = Presentation.Open(fileStreamInput))
    {
        //Use a sets of default FallbackFont collection to IPresentation.
        pptxDoc.FontSettings.FallbackFonts.InitializeDefault();
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
            //Create the output PDF file stream.
            using (FileStream fileStreamOutput = File.Create("Output.pdf"))
            {
                //Copy the converted PDF stream into created output PDF stream.
                pdfStream.CopyTo(fileStreamOutput);
            }
        }
    }
}
{% endhighlight %}

{% highlight C# tabtitle="C# [Windows-specific]" %}
//Opens a PowerPoint Presentation.
IPresentation pptxDoc = Presentation.Open("Sample.pptx");
//Initialize the conversion settings.
PresentationToPdfConverterSettings pdfConverterSettings = new PresentationToPdfConverterSettings();
//Enable the portable rendering.
pdfConverterSettings.EnablePortableRendering = true;
//Use a sets of default FallbackFont collection to IPresentation.
pptxDoc.FontSettings.FallbackFonts.InitializeDefault();
//Converts the PowerPoint Presentation into PDF document with Portable rendering option.
PdfDocument pdfDocument = PresentationToPdfConverter.Convert(pptxDoc);
//Saves the PDF document.
pdfDocument.Save("Sample.pdf");
//Closes the PDF document.
pdfDocument.Close(true);
//Closes the Presentation.
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Opens a PowerPoint Presentation.
Dim pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
'Initialize the conversion settings.
Dim pdfConverterSettings As PresentationToPdfConverterSettings = new PresentationToPdfConverterSettings()
'Enable the portable rendering.
pdfConverterSettings.EnablePortableRendering = true
'Use a sets of default FallbackFont collection to IPresentation.
pptxDoc.FontSettings.FallbackFonts.InitializeDefault
'Converts the PowerPoint Presentation into PDF document.
Dim pdfDocument As PdfDocument = PresentationToPdfConverter.Convert(pptxDoc)
'Saves the PDF document.
pdfDocument.Save("Sample.pdf")
'Closes the PDF document.
pdfDocument.Close(True)
'Closes the Presentation.
pptxDoc.Close()
{% endhighlight %}

{% endtabs %}

### Fallback fonts based on script type

The following code example demonstrates how a user can add fallback fonts based on the script types, which Presentation considers internally when converting a PowerPoint presentation to PDF.

{% tabs %}

{% highlight C# tabtitle="C# [Cross-platform]" %}
//Load the PowerPoint presentation into stream.
using (FileStream fileStreamInput = new FileStream("Template.pptx", FileMode.Open, FileAccess.Read))
{
    //Open the existing PowerPoint presentation with loaded stream.
    using (IPresentation pptxDoc = Presentation.Open(fileStreamInput))
    {
        //Adds fallback font for "Arabic" script type.
		pptxDoc.FontSettings.FallbackFonts.Add(ScriptType.Arabic, "Arial, Times New Roman");
		//Adds fallback font for "Hebrew" script type.
		pptxDoc.FontSettings.FallbackFonts.Add(ScriptType.Hebrew, "Arial, Courier New");
		//Adds fallback font for "Hindi" script type.
		pptxDoc.FontSettings.FallbackFonts.Add(ScriptType.Hindi, "Mangal, Nirmala UI");
		//Adds fallback font for "Chinese" script type.
		pptxDoc.FontSettings.FallbackFonts.Add(ScriptType.Chinese, "DengXian, MingLiU");
		//Adds fallback font for "Japanese" script type.
		pptxDoc.FontSettings.FallbackFonts.Add(ScriptType.Japanese, "Yu Mincho, MS Mincho");
		//Adds fallback font for "Thai" script type.
		pptxDoc.FontSettings.FallbackFonts.Add(ScriptType.Thai, "Tahoma, Microsoft Sans Serif");
		//Adds fallback font for "Korean" script type.
		pptxDoc.FontSettings.FallbackFonts.Add(ScriptType.Korean, "Malgun Gothic, Batang");
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
            //Create the output PDF file stream.
            using (FileStream fileStreamOutput = File.Create("Output.pdf"))
            {
                //Copy the converted PDF stream into created output PDF stream.
                pdfStream.CopyTo(fileStreamOutput);
            }
        }
    }
}
{% endhighlight %}

{% highlight C# tabtitle="C# [Windows-specific]" %}
//Opens a PowerPoint Presentation.
IPresentation pptxDoc = Presentation.Open("Sample.pptx");
//Initialize the conversion settings.
PresentationToPdfConverterSettings pdfConverterSettings = new PresentationToPdfConverterSettings();
//Enable the portable rendering.
pdfConverterSettings.EnablePortableRendering = true;
//Adds fallback font for "Arabic" script type.
pptxDoc.FontSettings.FallbackFonts.Add(ScriptType.Arabic, "Arial, Times New Roman");
//Adds fallback font for "Hebrew" script type.
pptxDoc.FontSettings.FallbackFonts.Add(ScriptType.Hebrew, "Arial, Courier New");
//Adds fallback font for "Hindi" script type.
pptxDoc.FontSettings.FallbackFonts.Add(ScriptType.Hindi, "Mangal, Nirmala UI");
//Adds fallback font for "Chinese" script type.
pptxDoc.FontSettings.FallbackFonts.Add(ScriptType.Chinese, "DengXian, MingLiU");
//Adds fallback font for "Japanese" script type.
pptxDoc.FontSettings.FallbackFonts.Add(ScriptType.Japanese, "Yu Mincho, MS Mincho");
//Adds fallback font for "Thai" script type.
pptxDoc.FontSettings.FallbackFonts.Add(ScriptType.Thai, "Tahoma, Microsoft Sans Serif");
//Adds fallback font for "Korean" script type.
pptxDoc.FontSettings.FallbackFonts.Add(ScriptType.Korean, "Malgun Gothic, Batang");
//Converts the PowerPoint Presentation into PDF document with Portable rendering option.
PdfDocument pdfDocument = PresentationToPdfConverter.Convert(pptxDoc);
//Saves the PDF document.
pdfDocument.Save("Sample.pdf");
//Closes the PDF document.
pdfDocument.Close(true);
//Closes the Presentation.
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Opens a PowerPoint Presentation.
Dim pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
'Initialize the conversion settings.
Dim pdfConverterSettings As PresentationToPdfConverterSettings = new PresentationToPdfConverterSettings()
'Enable the portable rendering.
pdfConverterSettings.EnablePortableRendering = true
'Adds fallback font for "Arabic" script type.
pptxDoc.FontSettings.FallbackFonts.Add(ScriptType.Arabic, "Arial, Times New Roman")
'Adds fallback font for "Hebrew" script type.
pptxDoc.FontSettings.FallbackFonts.Add(ScriptType.Hebrew, "Arial,Courier New")
'Adds fallback font for "Hindi" script type.
pptxDoc.FontSettings.FallbackFonts.Add(ScriptType.Hindi, "Mangal, Nirmala UI")
'Adds fallback font for "Chinese" script type.
pptxDoc.FontSettings.FallbackFonts.Add(ScriptType.Chinese, "DengXian, MingLiU")
'Adds fallback font for "Japanese" script type.
pptxDoc.FontSettings.FallbackFonts.Add(ScriptType.Japanese, "Yu Mincho, MS Mincho")
'Adds fallback font for "Thai" script type.
pptxDoc.FontSettings.FallbackFonts.Add(ScriptType.Thai, "Tahoma, Microsoft Sans Serif")
'Adds fallback font for "Korean" script type.
pptxDoc.FontSettings.FallbackFonts.Add(ScriptType.Korean, "Malgun Gothic, Batang")
'Converts the PowerPoint Presentation into PDF document.
Dim pdfDocument As PdfDocument = PresentationToPdfConverter.Convert(pptxDoc)
'Saves the PDF document.
pdfDocument.Save("Sample.pdf")
'Closes the PDF document.
pdfDocument.Close(True)
'Closes the Presentation.
pptxDoc.Close()
{% endhighlight %}

{% endtabs %}

### Fallback fonts for range of Unicode text

Users can set fallback fonts for specific Unicode range of text to be used in presentation to PDF conversion.

The following code example demonstrates how users can add fallback fonts by using a specific Unicode range of text that Presentation considers internally while converting a PowerPoint presentation to PDF.

{% tabs %}

{% highlight C# tabtitle="C# [Cross-platform]" %}
//Load the PowerPoint presentation into stream.
using (FileStream fileStreamInput = new FileStream("Template.pptx", FileMode.Open, FileAccess.Read))
{
    //Open the existing PowerPoint presentation with loaded stream.
    using (IPresentation pptxDoc = Presentation.Open(fileStreamInput))
    {
        //Adds fallback font for specific unicode range.
        // Arabic.
        pptxDoc.FontSettings.FallbackFonts.Add(new FallbackFont(0x0600, 0x06ff, "Arial"));
        // Hebrew.
        pptxDoc.FontSettings.FallbackFonts.Add(new FallbackFont(0x0590, 0x05ff, "Arial"));
        // Hindi.
        pptxDoc.FontSettings.FallbackFonts.Add(new FallbackFont(0x0900, 0x097F, "Mangal"));
        // Chinese.
        pptxDoc.FontSettings.FallbackFonts.Add(new FallbackFont(0x4E00, 0x9FFF, "DengXian"));
        // Japanese.
        pptxDoc.FontSettings.FallbackFonts.Add(new FallbackFont(0x3040, 0x309F, "MS Mincho"));
        // Korean.
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
            //Create the output PDF file stream.
            using (FileStream fileStreamOutput = File.Create("Output.pdf"))
            {
                //Copy the converted PDF stream into created output PDF stream.
                pdfStream.CopyTo(fileStreamOutput);
            }
        }
    }
}
{% endhighlight %}

{% highlight C# tabtitle="C# [Windows-specific]" %}
//Opens a PowerPoint Presentation.
IPresentation pptxDoc = Presentation.Open("Sample.pptx");
//Initialize the conversion settings.
PresentationToPdfConverterSettings pdfConverterSettings = new PresentationToPdfConverterSettings();
//Enable the portable rendering.
pdfConverterSettings.EnablePortableRendering = true;
//Adds fallback font for specific unicode range.
// Arabic.
pptxDoc.FontSettings.FallbackFonts.Add(new FallbackFont(0x0600, 0x06ff, "Arial"));
// Hebrew.
pptxDoc.FontSettings.FallbackFonts.Add(new FallbackFont(0x0590, 0x05ff, "Arial"));
// Hindi.
pptxDoc.FontSettings.FallbackFonts.Add(new FallbackFont(0x0900, 0x097F, "Mangal"));
// Chinese.
pptxDoc.FontSettings.FallbackFonts.Add(new FallbackFont(0x4E00, 0x9FFF, "DengXian"));
// Japanese.
pptxDoc.FontSettings.FallbackFonts.Add(new FallbackFont(0x3040, 0x309F, "MS Mincho"));
// Korean.
pptxDoc.FontSettings.FallbackFonts.Add(new FallbackFont(0xAC00, 0xD7A3, "Malgun Gothic"));
//Converts the PowerPoint Presentation into PDF document.
PdfDocument pdfDocument = PresentationToPdfConverter.Convert(pptxDoc);
//Saves the PDF document.
pdfDocument.Save("Sample.pdf");
//Closes the PDF document.
pdfDocument.Close(true);
//Closes the Presentation.
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Opens a PowerPoint Presentation.
Dim pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
'Initialize the conversion settings.
Dim pdfConverterSettings As PresentationToPdfConverterSettings = new PresentationToPdfConverterSettings()
'Enable the portable rendering.
pdfConverterSettings.EnablePortableRendering = true
'Adds fallback font for specific unicode range.
' Arabic.
pptxDoc.FontSettings.FallbackFonts.Add(New FallbackFont(1536, 1791, "Arial"))
' Hebrew.
pptxDoc.FontSettings.FallbackFonts.Add(New FallbackFont(1424, 1535, "Arial"))
' Hindi.
pptxDoc.FontSettings.FallbackFonts.Add(New FallbackFont(2304, 2431, "Mangal"))
' Chinese.
pptxDoc.FontSettings.FallbackFonts.Add(New FallbackFont(19968, 40959, "DengXian"))
' Japanese.
pptxDoc.FontSettings.FallbackFonts.Add(New FallbackFont(12352, 12447, "MS Mincho"))
' Korean.
pptxDoc.FontSettings.FallbackFonts.Add(New FallbackFont(44032, 55203, "Malgun Gothic"))
'Converts the PowerPoint Presentation into PDF document.
Dim pdfDocument As PdfDocument = PresentationToPdfConverter.Convert(pptxDoc)
'Saves the PDF document.
pdfDocument.Save("Sample.pdf")
'Closes the PDF document.
pdfDocument.Close(True)
'Closes the Presentation.
pptxDoc.Close()
{% endhighlight %}

{% endtabs %}

### Modify the exiting fallback fonts

The following code example demonstrates how user can modify or customize the existing fallback fonts using *FontNames* API while converting a PowerPoint presentation to PDF.

{% tabs %}

{% highlight C# tabtitle="C# [Cross-platform]" %}
//Load the PowerPoint presentation into stream.
using (FileStream fileStreamInput = new FileStream("Template.pptx", FileMode.Open, FileAccess.Read))
{
    //Open the existing PowerPoint presentation with loaded stream.
    using (IPresentation pptxDoc = Presentation.Open(fileStreamInput))
    {
        //Use a sets of default FallbackFont collection to IPresentation.
        pptxDoc.FontSettings.FallbackFonts.InitializeDefault();
        // Customize a default fallback font name.
		FallbackFonts fallbackFonts = pptxDoc.FontSettings.FallbackFonts;
		foreach (FallbackFont fallbackFont in fallbackFonts) 
		{
		   //Customize a default fallback font name as "David" for the Hebrew script.
		   if (fallbackFont.ScriptType == ScriptType.Hebrew)
		      fallbackFont.FontNames = "David";
		}
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
            //Create the output PDF file stream.
            using (FileStream fileStreamOutput = File.Create("Output.pdf"))
            {
                //Copy the converted PDF stream into created output PDF stream.
                pdfStream.CopyTo(fileStreamOutput);
            }
        }
    }
}
{% endhighlight %}

{% highlight C# tabtitle="C# [Windows-specific]" %}
//Opens a PowerPoint Presentation.
IPresentation pptxDoc = Presentation.Open("Sample.pptx");
//Initialize the conversion settings.
PresentationToPdfConverterSettings pdfConverterSettings = new PresentationToPdfConverterSettings();
//Enable the portable rendering.
pdfConverterSettings.EnablePortableRendering = true;
//Use a sets of default FallbackFont collection to IPresentation.
pptxDoc.FontSettings.FallbackFonts.InitializeDefault();
// Customize a default fallback font name.
FallbackFonts fallbackFonts = pptxDoc.FontSettings.FallbackFonts;
foreach (FallbackFont fallbackFont in fallbackFonts) 
{
   //Customize a default fallback font name as "David" for the Hebrew script.
   if (fallbackFont.ScriptType == ScriptType.Hebrew)
      fallbackFont.FontNames = "David";
}
//Converts the PowerPoint Presentation into PDF document.
PdfDocument pdfDocument = PresentationToPdfConverter.Convert(pptxDoc);
//Saves the PDF document.
pdfDocument.Save("Sample.pdf");
//Closes the PDF document.
pdfDocument.Close(true);
//Closes the Presentation.
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Opens a PowerPoint Presentation.
Dim pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
'Initialize the conversion settings.
Dim pdfConverterSettings As PresentationToPdfConverterSettings = new PresentationToPdfConverterSettings()
'Enable the portable rendering.
pdfConverterSettings.EnablePortableRendering = true
'Use a sets of default FallbackFont collection to IPresentation.
pptxDoc.FontSettings.FallbackFonts.InitializeDefault()
'Customize a default fallback font name.
Dim fallbackFonts As FallbackFonts = pptxDoc.FontSettings.FallbackFonts
For Each fallbackFont As FallbackFont In fallbackFonts 
   'Customize a default fallback font name as "David" for the Hebrew script.
   If fallbackFont.ScriptType = ScriptType.Hebrew Then
      fallbackFont.FontNames = "David"
   End If	  
Next
'Converts the PowerPoint Presentation into PDF document.
Dim pdfDocument As PdfDocument = PresentationToPdfConverter.Convert(pptxDoc)
'Saves the PDF document.
pdfDocument.Save("Sample.pdf")
'Closes the PDF document.
pdfDocument.Close(True)
'Closes the Presentation.
pptxDoc.Close()
{% endhighlight %}

{% endtabs %}

### Supported script types

The following table illustrates the supported script types by the .NET PowerPoint library (Presentation) in Presentation to PDF conversion.

<table>
<thead> 
<tr>
<th>Script types</th>
<th>Ranges</th>
<th>Default fallback fonts considered in InitializeDefault() API</th>
</tr>
</thead>
<tr>
<td>
Arabic
</td>
<td>
0x0600 - 0x06ff<br>
0x0750 - 0x077f<br>
0x08a0 - 0x08ff<br>
0xfb50 - 0xfdff<br>
0xfe70 - 0xfeff<br>
</td>
<td>
Arial, Times New Roman, Microsoft Uighur
</td>
</tr>
<tr>
<td>
Hebrew
</td>
<td>
0x0590 - 0x05ff<br>
0xfb1d - 0xfb4f<br>
</td>
<td>
Arial, Times New Roman, David
</td>
</tr>
<tr>
<td>
Hindi
</td>
<td>
0x0900 - 0x097F<br>
0xa8e0 - 0xa8ff<br>
0x1cd0 - 0x1cff<br>
</td>
<td>
Mangal, Utsaah
</td>
</tr>
<tr>
<td>
Chinese
</td>
<td>
0x4E00 - 0x9FFF<br>
0x3400 - 0x4DBF<br>
0xd840 - 0xd869<br>
0xdc00 - 0xdedf<br>
0xA960 - 0xA97F<br>
0xFF00 - 0xFFEF<br>
0x3000 - 0x303F<br>
</td>
<td>
DengXian, MingLiU, MS Gothic
</td>
</tr>
<tr>
<td>
Japanese
</td>
<td>
0x30A0 - 0x30FF<br>
0x3040 - 0x309F<br>
</td>
<td>
Yu Mincho, MS Mincho
</td>
</tr>
<tr>
<td>
Thai 
</td>
<td>
0x0E00 - 0x0E7F
</td>
<td>
Tahoma, Microsoft Sans Serif
</td>
</tr>
<tr>
<td>
Korean 
</td>
<td>
0xAC00 - 0xD7A3<br>
0x1100 - 0x11FF<br>
0x3130 - 0x318F<br>
0xA960 - 0xA97F<br>
0xD7B0 - 0xD7FF<br>
0xAC00 - 0xD7AF<br>
</td>
<td>
Malgun Gothic, Batang
</td>
</tr>
</table>

## Show Warning for unsupported elements

The Presentation library shows warning message about the unsupported elements such as Metafile images and charts (supported from .NET Standard 2.0) present in the input PowerPoint presentation, during PowerPoint to PDF conversion. It also allows you to cancel or continue the PowerPoint to PDF conversion, when any unsupported elements is present in the input PowerPoint presentation.

The following code example demonstrates how to cancel or continue the PowerPoint presentation to PDF conversion, when an unsupported elements (Metafile and Chart) are present in the input PowerPoint presentation.

{% tabs %}

{% highlight C# tabtitle="C# [Cross-platform]" %}
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

{% highlight C# tabtitle="C# [Windows-specific]" %}
//Essential Presentation library supports Show warning for unsupported elements feature in C# [Cross-platform], Blazor server-side application and Xamarin platforms alone.
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
//Essential Presentation supports library Show warning for unsupported elements feature in C# [Cross-platform], Blazor server-side application and Xamarin platforms alone.
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/PPTX-to-PDF-conversion/Show-warning-for-unsupported-elements).

## Handouts

The Presentation library allows you to convert a PowerPoint presentation to PDF document with [Handouts](https://help.syncfusion.com/cr/file-formats/Syncfusion.PresentationToPdfConverter.PublishOptions.html) option. Thus, the library allows selecting the number of slides to be included per PDF page. This helps converting multiple PowerPoint slides within a single PDF page. 
 
The following code sample demonstrates how to convert a PowerPoint presentation to PDF document with [Handouts](https://help.syncfusion.com/cr/file-formats/Syncfusion.PresentationToPdfConverter.PublishOptions.html) property.

{% tabs %}

{% highlight C# tabtitle="C# [Windows-specific]" %}

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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/PPTX-to-PDF-conversion/Convert-PowerPoint-to-PDF-with-handouts).

## Notes pages

The Presentation library allows you to convert a PowerPoint presentation to PDF document with 'notes pages' option, which will includes the notes content while PDF conversion. 

The following code sample demonstrates how to convert a PowerPoint presentation to PDF with 'notes pages'.

{% tabs %}

{% highlight C# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/PPTX-to-PDF-conversion/Convert-PowerPoint-to-PDF-with-notes).

## Include hidden slides

 The PowerPoint presentation supports hiding the slides in a presentation document. The hidden slides will not be included in the converted PDF document, by default. The Presentation library provides support to include or exclude the hidden slides while converting a PowerPoint presentation to PDF document.

The following code sample demonstrates how to include the hidden slides while converting a PowerPoint presentation to PDF document. 

{% tabs %}

{% highlight C# tabtitle="C# [Windows-specific]" %}

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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/PPTX-to-PDF-conversion/PowerPoint-to-PDF-with-hidden-slides).

## Recreate Nested Metafile

This setting allows you to regenerate the nested EMF images in the PowerPoint presentation document during PDF conversion.

This property is recommended to resolve the scaling problem of the nested metafile images by regenerating the nested metafile images present in the PowerPoint presentation document.

The following code sample shows how to use this property to regenerate the nested EMF images in the PowerPoint presentation document during PDF conversion.

{% tabs %}

{% highlight C# tabtitle="C# [Windows-specific]" %}

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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/PPTX-to-PDF-conversion/PowerPoint-to-PDF-with-nested-metafile).

## PDF Conformance

Essential Presentation currently supports following PDF conformances while converting a PowerPoint document to PDF.

* PDF/A-1b conformance
* PDF/X-1a conformance

N> 1. To know more details about PDF/A standard refer [https://en.wikipedia.org/wiki/PDF/A#Description](https://en.wikipedia.org/wiki/PDF/A#Description )
N> 2. To know more details about PDF/X standard refer [https://en.wikipedia.org/wiki/PDF/X](https://en.wikipedia.org/wiki/PDF/X)

The following code sample demonstrates how to set the PDF conformance level while PowerPoint presentation to PDF conversion.

{% tabs %}

{% highlight C# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/PPTX-to-PDF-conversion/Set-PDF-conformance-level).

## Accessible PDF document

This setting allows you to determine whether to preserve structured document tags in the converted PDF document for accessibility **(508 or PDF/UA compliance)** support. This property will set the title and description for images, diagrams, and other objects in the generated PDF document. This information will be helpful for **people with vision or cognitive impairments** who may not be able to see or understand the object.

The following code sample shows how to preserve structured document tags in the converted PDF document.

{% tabs %}

{% highlight C# tabtitle="C# [Cross-platform]" %}
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

{% highlight C# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/PPTX-to-PDF-conversion/Convert-PowerPoint-into-accessible-PDF).

## Chart quality

The Presentation library provides an option to decide the quality of the charts to optimize the converted PDF document size. 

N> 1. The default [ScalingMode](https://help.syncfusion.com/cr/file-formats/Syncfusion.OfficeChartToImageConverter.ChartToImageConverter.html#Syncfusion_OfficeChartToImageConverter_ChartToImageConverter_ScalingMode) for charts is [ScalingMode.Normal](https://help.syncfusion.com/cr/file-formats/Syncfusion.OfficeChart.ScalingMode.html). 
N> 2. Setting the [Best](https://help.syncfusion.com/cr/file-formats/Syncfusion.OfficeChart.ScalingMode.html) scaling mode will improve the quality of the converted charts and increase the converted PDF document size.

The following code sample demonstrates how to set the quality of the charts while PowerPoint presentation to PDF conversion

{% tabs %}

{% highlight C# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/PPTX-to-PDF-conversion/Set-chart-quality).

## Optimizing the converted PDF document size

**Optimizing the identical images**

The presentation library allows you to optimize the memory usage for the duplicate images while converting the PowerPoint presentation to PDF document to reduce the document size.
 
The following code sample demonstrates how to optimize the duplicate images while converting a PowerPoint presentation to PDF document. 

{% tabs %}

{% highlight C# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/PPTX-to-PDF-conversion/Optimize-duplicate-images).

**Optimizing the image quality and resolution**

You may have high resolution images in the PowerPoint slides which will impact the size of the converted PDF document. The Presentation library allows you to optimize the document size, by adjusting the quality and resolution of the images while converting the PowerPoint presentation to PDF document.
 
The following code sample demonstrates how to optimize the image quality and resolution while converting a PowerPoint presentation to PDF document. 

{% tabs %}

{% highlight C# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/PPTX-to-PDF-conversion/Optimize-image-quality-and-resolution).

## PowerPoint to PDF conversion in Azure platform

The Syncfusion PowerPoint library supports converting the PowerPoint document to PDF in Azure platform. The following code sample demonstrates how to convert a PowerPoint presentation to PDF in Azure platform.

{% tabs %}

{% highlight C# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/PPTX-to-PDF-conversion/Convert-PowerPoint-presentation-to-PDF/Azure).

## See Also

* [How to convert PPTX to PDF in Blazor WebAssembly (WASM)?](https://support.syncfusion.com/kb/article/12120/how-to-convert-pptx-to-pdf-in-blazor-webassembly-wasm)
