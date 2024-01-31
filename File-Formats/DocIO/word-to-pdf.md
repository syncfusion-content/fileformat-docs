---
title: Convert Word to PDF in C# | DocIO | Syncfusion
description: Learn how to convert a Word document to PDF, PDF/A, and PDF/UA using the .NET Word (DocIO) library without Microsoft Word or interop dependencies.
platform: file-formats
control: DocIO
documentation: UG
---

# Word document to PDF Conversion

## Converting Word to PDF

The Word document files are converted as a PDF document with a few lines of code by using the Essential DocIO. It works perfectly when you create an input Word document from scratch or load an existing Word document and easily converted into PDF. 

To quickly start converting a Word document to a PDF, please check out this video:
{% youtube "https://www.youtube.com/watch?v=8QdevnBxgHk" %}

Refer to the following links for assemblies required based on platforms to convert the Word document to PDF.

* [Word to PDF conversion assemblies](https://help.syncfusion.com/file-formats/docio/assemblies-required#converting-word-document-to-pdf) 
* [Word to PDF conversion NuGet packages](https://help.syncfusion.com/file-formats/docio/nuget-packages-required#converting-word-document-to-pdf)

The following namespaces are required to compile the code: 

**For WPF, Windows Forms, ASP.NET and ASP.NET MVC applications**
* using Syncfusion.DocIO
* using Syncfusion.DocIO.DLS
* using Syncfusion.OfficeChart
* using Syncfusion.DocToPDFConverter
* using Syncfusion.OfficeChartToImageConverter
* using Syncfusion.Pdf

**For ASP.NET Core, Blazor, Xamarin, WinUI, and .NET MAUI applications**
* using Syncfusion.DocIO
* using Syncfusion.DocIO.DLS
* using Syncfusion.DocIORenderer
* using Syncfusion.Pdf

The following code example illustrates how to convert a Word document into PDF document.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Open the file as Stream
FileStream docStream = new FileStream("Template.docx", FileMode.Open, FileAccess.Read);
//Loads file stream into Word document
WordDocument wordDocument = new WordDocument(docStream, Syncfusion.DocIO.FormatType.Automatic);
//Instantiation of DocIORenderer for Word to PDF conversion
DocIORenderer render = new DocIORenderer();
//Sets Chart rendering Options.
render.Settings.ChartRenderingOptions.ImageFormat =  ExportImageFormat.Jpeg;
//Converts Word document into PDF document
PdfDocument pdfDocument = render.ConvertToPDF(wordDocument);
//Releases all resources used by the Word document and DocIO Renderer objects
render.Dispose();
wordDocument.Dispose();
//Saves the PDF file
MemoryStream outputStream = new MemoryStream();
pdfDocument.Save(outputStream);
//Closes the instance of PDF document object
pdfDocument.Close();
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Loads an existing Word document
WordDocument wordDocument = new WordDocument("Template.docx", FormatType.Docx);
//Initializes the ChartToImageConverter for converting charts during Word to pdf conversion
wordDocument.ChartToImageConverter = new ChartToImageConverter();
//Creates an instance of the DocToPDFConverter
DocToPDFConverter converter = new DocToPDFConverter();
//Converts Word document into PDF document
PdfDocument pdfDocument = converter.ConvertToPDF(wordDocument);
//Saves the PDF file 
pdfDocument.Save("WordtoPDF.pdf");
//Closes the instance of document objects
pdfDocument.Close(true);
wordDocument.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Loads an existing Word document
Dim wordDocument As New WordDocument("Template.docx", FormatType.Docx)
'Initializes the ChartToImageConverter for converting charts during Word to pdf conversion
wordDocument.ChartToImageConverter = New ChartToImageConverter()
'Creates an instance of the DocToPDFConverter
Dim converter As New DocToPDFConverter()
'Converts Word document into PDF document
Dim pdfDocument As PdfDocument = converter.ConvertToPDF(wordDocument)
'Saves the PDF file 
pdfDocument.Save("WordtoPDF.pdf")
'Closes the instance of document objects
pdfDocument.Close(True)
wordDocument.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Convert-Word-document-to-PDF).

N> 1. For .NET Framework, creating an instance of the [ChartToImageConverter](https://help.syncfusion.com/cr/file-formats/Syncfusion.OfficeChartToImageConverter.ChartToImageConverter.html) class is mandatory to convert the charts present in the Word to PDF. Otherwise, the charts are not preserved in the converted PDF. Whereas this is not necessary for .NET Core, as ChartToImageConverter is initialized internally in Syncfusion.DocIORenderer.Portable assembly.
N> 2. Total number of pages in the converted PDF may vary based on unsupported elements in the input Word document.
N> 3. "DocIO supports Word to PDF conversion in UWP application using DocIORenderer." For further information, please refer [here](https://support.syncfusion.com/kb/article/8902/how-to-convert-word-document-to-pdf-in-uwp)

## Word to PDF conversion in Linux OS

In Linux OS, you can perform the Word to PDF conversion using .NET Core (Targeting .netcoreapp) application. You can refer [Word to PDF conversion NuGet packages](https://help.syncfusion.com/file-formats/docio/nuget-packages-required#converting-word-document-to-pdf) to know about the packages required to deploy .NET Core (Targeting .netcoreapp) application with Word to PDF conversion capabilities.

From v23.1.40, in addition to the previous NuGet packages, we recommend to use [SkiaSharp.NativeAssets.Linux v2.88.6](https://www.nuget.org/packages/SkiaSharp.NativeAssets.Linux/2.88.6) and [HarfBuzzSharp.NativeAssets.Linux v7.3.0](https://www.nuget.org/packages/HarfBuzzSharp.NativeAssets.Linux/7.3.0) NuGets to perform Word to PDF conversion in Linux environment.

If you are using prior to v23.1.40 release, please refer [here](https://help.syncfusion.com/file-formats/docio/faq#what-are-the-nuget-packages-to-be-installed-to-perform-word-to-pdf-conversion-in-linux-os) to know about how to perform Word to PDF conversion in Linux.

**Frequently Asked Questions**
* [How to copy necessary fonts to Linux containers?](https://help.syncfusion.com/file-formats/docio/faq#how-to-copy-necessary-fonts-to-linux-containers)
* [How to set culture / locale in Docker containers (Windows & Linux containers)?](https://help.syncfusion.com/file-formats/docio/faq#how-to-set-culturelocale-in-docker-containers-windows-and-linux-containers)
* [How to copy necessary Microsoft compatible fonts to Linux?](https://help.syncfusion.com/file-formats/docio/faq#how-to-copy-necessary-microsoft-compatible-fonts-to-linux)
* [How to resolve LibSkiaSharp not found Exception?](https://help.syncfusion.com/file-formats/docio/faq#how-to-resolve-libskiasharp-not-found-exception)

## Customization settings
The Essential DocIO provides settings while performing Word to PDF conversion mentioned below, 

### Fast rendering

This setting allows you to **convert PDF faster** by using direct PDF rendering approach rather than EMF rendering approach.

The following code sample shows how to convert the Word document to PDF using direct PDF rendering approach. 

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//DocIO supports Word to PDF fast rendering in Windows forms, WPF, ASP.NET and ASP.NET MVC platform alone
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Loads an existing Word document
WordDocument wordDocument = new WordDocument("Template.docx", FormatType.Docx);
//Initializes the ChartToImageConverter for converting charts during Word to pdf conversion
wordDocument.ChartToImageConverter = new ChartToImageConverter();
//Sets the scaling mode for charts (Normal mode reduces the Pdf file size)
wordDocument.ChartToImageConverter.ScalingMode = ScalingMode.Normal;
//Creates an instance of the DocToPDFConverter - responsible for Word to PDF conversion
DocToPDFConverter converter = new DocToPDFConverter();
//Sets true to enable the fast rendering using direct PDF conversion.
converter.Settings.EnableFastRendering = true;
//Converts Word document into PDF document
PdfDocument pdfDocument = converter.ConvertToPDF(wordDocument);
//Saves the PDF file to file system
pdfDocument.Save("WordtoPDF.pdf");
//Closes the instance of document objects
pdfDocument.Close(true);
wordDocument.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Loads an existing Word document
Dim wordDocument As New WordDocument("Template.docx", FormatType.Docx)
'Initializes the ChartToImageConverter for converting charts during Word to pdf conversion
wordDocument.ChartToImageConverter = New ChartToImageConverter()
'Sets the scaling mode for charts (Normal mode reduces the Pdf file size)
wordDocument.ChartToImageConverter.ScalingMode = ScalingMode.Normal
'creates an instance of the DocToPDFConverter - responsible for Word to PDF conversion
Dim converter As New DocToPDFConverter()
'Sets true to enable the fast rendering using direct PDF conversion.
converter.Settings.EnableFastRendering = true
'Converts Word document into PDF document
Dim pdfDocument As PdfDocument = converter.ConvertToPDF(wordDocument)
'Saves the PDF file to file system
pdfDocument.Save("WordtoPDF.pdf")
'Closes the instance of document objects
pdfDocument.Close(True)
wordDocument.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Enable-fast-rendering).

### Embedding fonts

You can customize the TrueType fonts embedding in two ways as follows:

#### Embed Subset Fonts

This setting allows you to **embed the particular font information** (glyphs) from the TrueType fonts used for the rendered characters in converted PDF document.

The following code sample shows how to embed the TrueType fonts into the converted PDF document.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Open the file as Stream
FileStream docStream = new FileStream("Template.docx", FileMode.Open, FileAccess.Read);
//Loads file stream into Word document
WordDocument wordDocument = new WordDocument(docStream, Syncfusion.DocIO.FormatType.Automatic);
//Instantiation of DocIORenderer for Word to PDF conversion
DocIORenderer render = new DocIORenderer();
//Sets true to embed TrueType fonts
render.Settings.EmbedFonts = true;
//Converts Word document into PDF document
PdfDocument pdfDocument = render.ConvertToPDF(wordDocument);
//Releases all resources used by the Word document and DocIO Renderer objects
render.Dispose();
wordDocument.Dispose();
//Saves the PDF file
MemoryStream outputStream = new MemoryStream();
pdfDocument.Save(outputStream);
//Closes the instance of PDF document object
pdfDocument.Close();
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Loads an existing Word document
WordDocument wordDocument = new WordDocument("Template.docx", FormatType.Docx);
//Initializes the ChartToImageConverter for converting charts during Word to pdf conversion
wordDocument.ChartToImageConverter = new ChartToImageConverter();
//Sets the scaling mode for charts (Normal mode reduces the Pdf file size)
wordDocument.ChartToImageConverter.ScalingMode = ScalingMode.Normal;
//Creates an instance of the DocToPDFConverter - responsible for Word to PDF conversion
DocToPDFConverter converter = new DocToPDFConverter();
//Sets true to embed TrueType fonts
converter.Settings.EmbedFonts = true;
//Converts Word document into PDF document
PdfDocument pdfDocument = converter.ConvertToPDF(wordDocument);
//Saves the PDF file to file system
pdfDocument.Save("WordtoPDF.pdf");
//Closes the instance of document objects
pdfDocument.Close(true);
wordDocument.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Loads an existing Word document
Dim wordDocument As New WordDocument("Template.docx", FormatType.Docx)
'Initializes the ChartToImageConverter for converting charts during Word to pdf conversion
wordDocument.ChartToImageConverter = New ChartToImageConverter()
'Sets the scaling mode for charts (Normal mode reduces the Pdf file size)
wordDocument.ChartToImageConverter.ScalingMode = ScalingMode.Normal
'creates an instance of the DocToPDFConverter - responsible for Word to PDF conversion
Dim converter As New DocToPDFConverter()
'Sets true to embed TrueType fonts 
converter.Settings.EmbedFonts = true
'Converts Word document into PDF document
Dim pdfDocument As PdfDocument = converter.ConvertToPDF(wordDocument)
'Saves the PDF file to file system
pdfDocument.Save("WordtoPDF.pdf")
'Closes the instance of document objects
pdfDocument.Close(True)
wordDocument.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Embed-subset-fonts).

#### Embed Complete Fonts

This setting allows you to embed the complete font information (glyphs) from the TrueType fonts used in converted PDF document.

The following code sample shows how to embed the complete TrueType fonts into the converted PDF document.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Open the file as Stream
FileStream docStream = new FileStream("Template.docx", FileMode.Open, FileAccess.Read);
//Loads file stream into Word document
WordDocument wordDocument = new WordDocument(docStream, Syncfusion.DocIO.FormatType.Automatic);
//Instantiation of DocIORenderer for Word to PDF conversion
DocIORenderer render = new DocIORenderer();
//Sets true to embed complete TrueType fonts
render.Settings.EmbedCompleteFonts = true;
//Converts Word document into PDF document
PdfDocument pdfDocument = render.ConvertToPDF(wordDocument);
//Releases all resources used by the Word document and DocIO Renderer objects
render.Dispose();
wordDocument.Dispose();
//Saves the PDF file
MemoryStream outputStream = new MemoryStream();
pdfDocument.Save(outputStream);
//Closes the instance of PDF document object
pdfDocument.Close();
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Loads an existing Word document
WordDocument wordDocument = new WordDocument("Template.docx", FormatType.Docx);
//Initializes the ChartToImageConverter for converting charts during Word to pdf conversion
wordDocument.ChartToImageConverter = new ChartToImageConverter();
//Sets the scaling mode for charts (Normal mode reduces the Pdf file size)
wordDocument.ChartToImageConverter.ScalingMode = ScalingMode.Normal;
//Creates an instance of the DocToPDFConverter - responsible for Word to PDF conversion
DocToPDFConverter converter = new DocToPDFConverter();
//Sets true to embed complete TrueType fonts
converter.Settings.EmbedCompleteFonts = true;
//Converts Word document into PDF document
PdfDocument pdfDocument = converter.ConvertToPDF(wordDocument);
//Saves the PDF file to file system
pdfDocument.Save("WordtoPDF.pdf");
//Closes the instance of document objects
pdfDocument.Close(true);
wordDocument.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Loads an existing Word document
Dim wordDocument As New WordDocument("Template.docx", FormatType.Docx)
'Initializes the ChartToImageConverter for converting charts during Word to pdf conversion
wordDocument.ChartToImageConverter = New ChartToImageConverter()
'Sets the scaling mode for charts (Normal mode reduces the Pdf file size)
wordDocument.ChartToImageConverter.ScalingMode = ScalingMode.Normal
'creates an instance of the DocToPDFConverter - responsible for Word to PDF conversion
Dim converter As New DocToPDFConverter()
'Sets true to embed complete TrueType fonts 
converter.Settings.EmbedCompleteFonts = true
'Converts Word document into PDF document
Dim pdfDocument As PdfDocument = converter.ConvertToPDF(wordDocument)
'Saves the PDF file to file system
pdfDocument.Save("WordtoPDF.pdf")
'Closes the instance of document objects
pdfDocument.Close(True)
wordDocument.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Embed-complete-fonts).

### Accessible PDF document

This setting allows you to determine whether to preserve document structured tags in the converted **PDF document for accessibility (508 compliance) support**. This property will set the title and description for images, diagrams and other objects in the generated PDF document. This information will be useful for **people with vision or cognitive impairments** who may not able to see or understand the object

The following code sample shows how to preserve document structured tags in the converted PDF document.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Open the file as Stream
FileStream docStream = new FileStream("Template.docx", FileMode.Open, FileAccess.Read);
//Loads file stream into Word document
WordDocument wordDocument = new WordDocument(docStream, Syncfusion.DocIO.FormatType.Automatic);
//Instantiation of DocIORenderer for Word to PDF conversion
DocIORenderer render = new DocIORenderer();
//Sets true to preserve document structured tags in the converted PDF document 
render.Settings.AutoTag = true;
//Converts Word document into PDF document
PdfDocument pdfDocument = render.ConvertToPDF(wordDocument);
//Releases all resources used by the Word document and DocIO Renderer objects
render.Dispose();
wordDocument.Dispose();
//Saves the PDF file
MemoryStream outputStream = new MemoryStream();
pdfDocument.Save(outputStream);
//Closes the instance of PDF document object
pdfDocument.Close();
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Loads an existing Word document
WordDocument wordDocument = new WordDocument("Template.docx", FormatType.Docx);
//Creates an instance of the DocToPDFConverter - responsible for Word to PDF conversion
DocToPDFConverter converter = new DocToPDFConverter();
//Sets true to preserve document structured tags in the converted PDF document 
converter.Settings.AutoTag = true;
//Converts Word document into PDF document
PdfDocument pdfDocument = converter.ConvertToPDF(wordDocument);
//Saves the PDF file to file system
pdfDocument.Save("WordtoPDF.pdf");
//Closes the instance of document objects
pdfDocument.Close(true);
wordDocument.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Loads an existing Word document
Dim wordDocument As New WordDocument("Template.docx", FormatType.Docx)
'Creates an instance of the DocToPDFConverter - responsible for Word to PDF conversion
Dim converter As New DocToPDFConverter()
'Sets true to preserve document structured tags in the converted PDF document 
converter.Settings.AutoTag = True
'Converts Word document into PDF document
Dim pdfDocument As PdfDocument = converter.ConvertToPDF(wordDocument)
'Saves the PDF file to file system
pdfDocument.Save("WordtoPDF.pdf")
'Closes the instance of document objects
pdfDocument.Close(True)
wordDocument.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Convert-Word-into-accessible-PDF).

### Word document headings to PDF bookmarks

This setting allows you to determine whether to **preserve Word document headings** (i.e., paragraph with heading style and outline level) as bookmarks in the converted PDF document. As per Microsoft Word behavior, either Word document headings or bookmarks can be exported as PDF bookmarks. By default, DocIO preserves Word documents bookmarks as PDF bookmarks in converted PDF document.

The following code sample shows how to preserve Word document headings as bookmarks in the converted PDF document.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Open the file as Stream
FileStream docStream = new FileStream("Template.docx", FileMode.Open, FileAccess.Read);
//Loads file stream into Word document
WordDocument wordDocument = new WordDocument(docStream, Syncfusion.DocIO.FormatType.Automatic);
//Instantiation of DocIORenderer for Word to PDF conversion
DocIORenderer render = new DocIORenderer();
//Sets ExportBookmarks for preserving Word document headings as PDF bookmarks
render.Settings.ExportBookmarks = Syncfusion.DocIO.ExportBookmarkType.Headings;
//Converts Word document into PDF document
PdfDocument pdfDocument = render.ConvertToPDF(wordDocument);
//Releases all resources used by the Word document and DocIO Renderer objects
render.Dispose();
wordDocument.Dispose();
//Saves the PDF file
MemoryStream outputStream = new MemoryStream();
pdfDocument.Save(outputStream);
//Closes the instance of PDF document object
pdfDocument.Close();
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Loads an existing Word document
WordDocument wordDocument = new WordDocument("Template.docx", FormatType.Docx);
//Creates an instance of the DocToPDFConverter - responsible for Word to PDF conversion
DocToPDFConverter converter = new DocToPDFConverter();
//Sets ExportBookmarks for preserving Word document headings as PDF bookmarks
converter.Settings.ExportBookmarks = Syncfusion.DocIO.ExportBookmarkType.Headings;
//Converts Word document into PDF document
PdfDocument pdfDocument = converter.ConvertToPDF(wordDocument);
//Saves the PDF file to file system
pdfDocument.Save("WordtoPDF.pdf");
//Closes the instance of document objects
pdfDocument.Close(true);
wordDocument.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Loads an existing Word document
Dim wordDocument As New WordDocument("Template.docx", FormatType.Docx)
'Creates an instance of the DocToPDFConverter - responsible for Word to PDF conversion
Dim converter As New DocToPDFConverter()
'Sets ExportBookmarks for preserving Word document headings as PDF bookmarks
converter.Settings.ExportBookmarks = Syncfusion.DocIO.ExportBookmarkType.Headings
'Converts Word document into PDF document
Dim pdfDocument As PdfDocument = converter.ConvertToPDF(wordDocument)
'Saves the PDF file to file system
pdfDocument.Save("WordtoPDF.pdf")
'Closes the instance of document objects
pdfDocument.Close(True)
wordDocument.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Export-Word-headings-into-PDF).

The following code sample shows how to preserve both Word document headings and Bookmarks as PDF bookmarks in the converted PDF document.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Open the file as Stream
FileStream docStream = new FileStream("Template.docx", FileMode.Open, FileAccess.Read);
//Loads file stream into Word document
WordDocument wordDocument = new WordDocument(docStream, Syncfusion.DocIO.FormatType.Automatic);
//Instantiation of DocIORenderer for Word to PDF conversion
DocIORenderer render = new DocIORenderer();
//Sets ExportBookmarks for preserving Word document headings as PDF bookmarks
render.Settings.ExportBookmarks = Syncfusion.DocIO.ExportBookmarkType.Headings | Syncfusion.DocIO.ExportBookmarkType.Bookmarks;
//Converts Word document into PDF document
PdfDocument pdfDocument = render.ConvertToPDF(wordDocument);
//Releases all resources used by the Word document and DocIO Renderer objects
render.Dispose();
wordDocument.Dispose();
//Saves the PDF file
MemoryStream outputStream = new MemoryStream();
pdfDocument.Save(outputStream);
//Closes the instance of PDF document object
pdfDocument.Close();
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Loads an existing Word document
WordDocument wordDocument = new WordDocument("Template.docx", FormatType.Docx);
//Creates an instance of the DocToPDFConverter - responsible for Word to PDF conversion
DocToPDFConverter converter = new DocToPDFConverter();
//Sets ExportBookmarks for preserving Word document headings as PDF bookmarks
converter.Settings.ExportBookmarks = Syncfusion.DocIO.ExportBookmarkType.Headings | Syncfusion.DocIO.ExportBookmarkType.Bookmarks;
//Converts Word document into PDF document
PdfDocument pdfDocument = converter.ConvertToPDF(wordDocument);
//Saves the PDF file to file system
pdfDocument.Save("WordtoPDF.pdf");
//Closes the instance of document objects
pdfDocument.Close(true);
wordDocument.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Loads an existing Word document
Dim wordDocument As New WordDocument("Template.docx", FormatType.Docx)
'Creates an instance of the DocToPDFConverter - responsible for Word to PDF conversion
Dim converter As New DocToPDFConverter()
'Sets ExportBookmarks for preserving Word document headings as PDF bookmarks
converter.Settings.ExportBookmarks = Syncfusion.DocIO.ExportBookmarkType.Headings | Syncfusion.DocIO.ExportBookmarkType.Bookmarks
'Converts Word document into PDF document
Dim pdfDocument As PdfDocument = converter.ConvertToPDF(wordDocument)
'Saves the PDF file to file system
pdfDocument.Save("WordtoPDF.pdf")
'Closes the instance of document objects
pdfDocument.Close(True)
wordDocument.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Export-Word-bookmarks-into-PDF).

### Word document form field to PDF form field.

This setting allows you to determine whether to **preserve Word document form fields** (Text form field, Checkbox form field and Drop-down form field) as PDF form fields in the converted PDF document. This features helps in **creating fillable PDF forms from Word document**.

The following code sample shows how to preserve Word document form field as PDF form field in the converted PDF document.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
// Open the file as Stream
FileStream docStream = new FileStream("Template.docx", FileMode.Open, FileAccess.Read);
//Loads file stream into Word document
WordDocument wordDocument = new WordDocument(docStream, Syncfusion.DocIO.FormatType.Automatic);
//Instantiation of DocIORenderer for Word to PDF conversion
DocIORenderer render = new DocIORenderer();
//Sets true to preserve the Word document form field as editable PDF form field in PDF document
render.Settings.PreserveFormFields = true;
//Converts Word document into PDF document
PdfDocument pdfDocument = render.ConvertToPDF(wordDocument);
//Releases all resources used by the Word document and DocIO Renderer objects
render.Dispose();
wordDocument.Dispose();
//Saves the PDF file
MemoryStream outputStream = new MemoryStream();
pdfDocument.Save(outputStream);
//Closes the instance of PDF document object
pdfDocument.Close();
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Loads an existing Word document
WordDocument wordDocument = new WordDocument("Template.docx", FormatType.Docx);
//Creates an instance of the DocToPDFConverter - responsible for Word to PDF conversion
DocToPDFConverter converter = new DocToPDFConverter();
//Sets true to preserve the Word document form field as editable PDF form field in PDF document
converter.Settings.PreserveFormFields = true;
//Converts Word document into PDF document
PdfDocument pdfDocument = converter.ConvertToPDF(wordDocument);
//Saves the PDF file to file system
pdfDocument.Save("WordtoPDF.pdf");
//Closes the instance of document objects
pdfDocument.Close(true);
wordDocument.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Loads an existing Word document
Dim wordDocument As New WordDocument("Template.docx", FormatType.Docx)
'Creates an instance of the DocToPDFConverter - responsible for Word to PDF conversion
Dim converter As New DocToPDFConverter()
'Sets true to preserve the Word document form field as editable PDF form field in PDF document
converter.Settings.PreserveFormFields = True
'Converts Word document into PDF document
Dim pdfDocument As PdfDocument = converter.ConvertToPDF(wordDocument)
'Saves the PDF file to file system
pdfDocument.Save("WordtoPDF.pdf")
'Closes the instance of document objects
pdfDocument.Close(True)
wordDocument.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Create-fillable-PDF-from-Word).

### Image quality 

This setting allows you to determine the **quality of the charts and JPEG images** in the converted PDF document.

The following code sample shows how to customize the image quality of charts and JPEG images in the converted PDF document.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//DocIO supports Word to PDF Image in Windows forms, WPF, ASP.NET and ASP.NET MVC platform alone
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Loads an existing Word document
WordDocument wordDocument = new WordDocument("Template.docx", FormatType.Docx);
//Initializes the ChartToImageConverter for converting charts during Word to pdf conversion
wordDocument.ChartToImageConverter = new ChartToImageConverter();
//Sets the scaling mode for charts (Normal mode reduces the Pdf file size)
wordDocument.ChartToImageConverter.ScalingMode = ScalingMode.Normal;
//Creates an instance of the DocToPDFConverter - responsible for Word to PDF conversion
DocToPDFConverter converter = new DocToPDFConverter();
//Sets the jpeg image quality to reduce the Pdf file size
converter.Settings.ImageQuality = 100;
//Sets the image resolution
converter.Settings.ImageResolution = 640;
//Converts Word document into PDF document
PdfDocument pdfDocument = converter.ConvertToPDF(wordDocument);
//Saves the PDF file to file system
pdfDocument.Save("WordtoPDF.pdf");
//Closes the instance of document objects
pdfDocument.Close(true);
wordDocument.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Loads an existing Word document
Dim wordDocument As New WordDocument("Template.docx", FormatType.Docx)
'Initializes the ChartToImageConverter for converting charts during Word to pdf conversion
wordDocument.ChartToImageConverter = New ChartToImageConverter()
'Sets the scaling mode for charts (Normal mode reduces the Pdf file size)
wordDocument.ChartToImageConverter.ScalingMode = ScalingMode.Normal
'creates an instance of the DocToPDFConverter - responsible for Word to PDF conversion
Dim converter As New DocToPDFConverter()
'Sets the jpeg image quality to reduce the Pdf file size
converter.Settings.ImageQuality = 100
'Sets the image resolution
converter.Settings.ImageResolution = 640
'Converts Word document into PDF document
Dim pdfDocument As PdfDocument = converter.ConvertToPDF(wordDocument)
'Saves the PDF file to file system
pdfDocument.Save("WordtoPDF.pdf")
'Closes the instance of document objects
pdfDocument.Close(True)
wordDocument.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Adjust-image-quality).

### Recreate Nested Metafile

This setting allows you to regenerate the nested EMF images present in the Word document during PDF conversion.

This property is recommended to resolve the scaling problem of nested metafile images by regenerating the nested metafile images present in the Word document.

The following code sample shows how to use this property to regenerate the nested EMF images present in the Word document during PDF conversion.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//DocIO supports to Recreate Nested Metafile in Windows forms, WPF, ASP.NET and ASP.NET MVC platform alone, and it's also supported in .NET Core 3.0, but it requires DocToPDFConverter assembly instead of DocIORenderer.
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Loads an existing Word document
WordDocument wordDocument = new WordDocument("Template.docx", FormatType.Docx);     
//Creates an instance of the DocToPDFConverter - responsible for Word to PDF conversion
DocToPDFConverter converter = new DocToPDFConverter();
//Sets RecreateNestedMetafile property to true to Recreate the Nested Metafile automatically
converter.Settings.RecreateNestedMetafile = true;
//Converts Word document into PDF document
PdfDocument pdfDocument = converter.ConvertToPDF(wordDocument);
//Saves the PDF file to file system
pdfDocument.Save("WordtoPDF.pdf");
//Closes the instance of document objects
pdfDocument.Close(true);
wordDocument.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Loads an existing Word document
Dim wordDocument As New WordDocument("Template.docx", FormatType.Docx)
'Initializes the ChartToImageConverter for converting charts during Word to pdf conversion
wordDocument.ChartToImageConverter = New ChartToImageConverter()
'Creates an instance of the DocToPDFConverter
Dim converter As New DocToPDFConverter()
'Sets RecreateNestedMetafile property to true to Recreate the Nested Metafile automatically
converter.Settings.RecreateNestedMetafile = True
'Converts Word document into PDF document
Dim pdfDocument As PdfDocument = converter.ConvertToPDF(wordDocument)
'Saves the PDF file 
pdfDocument.Save("WordtoPDF.pdf")
'Closes the instance of document objects
pdfDocument.Close(True)
wordDocument.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Recreate-nested-metafile).

### Identical image optimization 

This setting **reduces the Main Memory usage** in Word to PDF conversion by reusing the identical images.

The following code sample shows how to reduce the Main Memory usage while converting Word to PDF by reusing the identical images.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Open the file as Stream
FileStream docStream = new FileStream("Template.docx", FileMode.Open, FileAccess.Read);
//Loads file stream into Word document
WordDocument wordDocument = new WordDocument(docStream, Syncfusion.DocIO.FormatType.Automatic);
//Instantiation of DocIORenderer for Word to PDF conversion
DocIORenderer render = new DocIORenderer();
//Sets true to optimize the memory usage for identical images
render.Settings.OptimizeIdenticalImages = true;
//Converts Word document into PDF document
PdfDocument pdfDocument = render.ConvertToPDF(wordDocument);
//Releases all resources used by the Word document and DocIO Renderer objects
render.Dispose();
wordDocument.Dispose();
//Saves the PDF file
MemoryStream outputStream = new MemoryStream();
pdfDocument.Save(outputStream);
//Closes the instance of PDF document object
pdfDocument.Close();
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Loads an existing Word document
WordDocument wordDocument = new WordDocument("Template.docx", FormatType.Docx);
//Initializes the ChartToImageConverter for converting charts during Word to pdf conversion
wordDocument.ChartToImageConverter = new ChartToImageConverter();
//Sets the scaling mode for charts (Normal mode reduces the Pdf file size)
wordDocument.ChartToImageConverter.ScalingMode = ScalingMode.Normal;
//Creates an instance of the DocToPDFConverter - responsible for Word to PDF conversion
DocToPDFConverter converter = new DocToPDFConverter();
//Sets true to embed TrueType fonts
converter.Settings.EmbedFonts = true;
//Sets true to optimize the memory usage for identical images
converter.Settings.OptimizeIdenticalImages = true;
//Converts Word document into PDF document
PdfDocument pdfDocument = converter.ConvertToPDF(wordDocument);
//Saves the PDF file to file system
pdfDocument.Save("WordtoPDF.pdf");
//Closes the instance of document objects
pdfDocument.Close(true);
wordDocument.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Loads an existing Word document
Dim wordDocument As New WordDocument("Template.docx", FormatType.Docx)
'Initializes the ChartToImageConverter for converting charts during Word to pdf conversion
wordDocument.ChartToImageConverter = New ChartToImageConverter()
'Sets the scaling mode for charts (Normal mode reduces the Pdf file size)
wordDocument.ChartToImageConverter.ScalingMode = ScalingMode.Normal
'creates an instance of the DocToPDFConverter - responsible for Word to PDF conversion
Dim converter As New DocToPDFConverter()
'Sets true to optimize the memory usage for identical images
converter.Settings.OptimizeIdenticalImages = True
'Converts Word document into PDF document
Dim pdfDocument As PdfDocument = converter.ConvertToPDF(wordDocument)
'Saves the PDF file to file system
pdfDocument.Save("WordtoPDF.pdf")
'Closes the instance of document objects
pdfDocument.Close(True)
wordDocument.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Optimize-identical-images).

### PDF Conformance Level

This setting allows you to set the PDF conformance level.

The following code sample shows how to set the [PdfConformanceLevel](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocToPDFConverter.DocToPDFConverterSettings.html#Syncfusion_DocToPDFConverter_DocToPDFConverterSettings_PdfConformanceLevel) while converting Word to PDF.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Open the file as Stream
FileStream docStream = new FileStream("Template.docx", FileMode.Open, FileAccess.Read);
//Loads file stream into Word document
WordDocument wordDocument = new WordDocument(docStream, Syncfusion.DocIO.FormatType.Automatic);
//Instantiation of DocIORenderer for Word to PDF conversion
DocIORenderer render = new DocIORenderer();
//Set the conformance for PDF/A-1b conversion.
render.Settings.PdfConformanceLevel = PdfConformanceLevel.Pdf_A1B;
//Converts Word document into PDF document
PdfDocument pdfDocument = render.ConvertToPDF(wordDocument);
//Releases all resources used by the Word document and DocIO Renderer objects
render.Dispose();
wordDocument.Dispose();
//Saves the PDF file
MemoryStream outputStream = new MemoryStream();
pdfDocument.Save(outputStream);
//Closes the instance of PDF document object
pdfDocument.Close();
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Loads an existing Word document
WordDocument wordDocument = new WordDocument("Template.docx", FormatType.Docx);
//Initializes the ChartToImageConverter for converting charts during Word to pdf conversion
wordDocument.ChartToImageConverter = new ChartToImageConverter();
//Sets the scaling mode for charts (Normal mode reduces the Pdf file size)
wordDocument.ChartToImageConverter.ScalingMode = ScalingMode.Normal;
//Creates an instance of the DocToPDFConverter - responsible for Word to PDF conversion
DocToPDFConverter converter = new DocToPDFConverter();
//Set the conformance for PDF/A-1b conversion.
converter.Settings.PdfConformanceLevel = PdfConformanceLevel.Pdf_A1B;
//Converts Word document into PDF document
PdfDocument pdfDocument = converter.ConvertToPDF(wordDocument);
//Saves the PDF file to file system
pdfDocument.Save("WordtoPDF.pdf");
//Closes the instance of document objects
pdfDocument.Close(true);
wordDocument.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Loads an existing Word document
Dim wordDocument As New WordDocument("Template.docx", FormatType.Docx)
'Initializes the ChartToImageConverter for converting charts during Word to pdf conversion
wordDocument.ChartToImageConverter = New ChartToImageConverter()
'Sets the scaling mode for charts (Normal mode reduces the Pdf file size)
wordDocument.ChartToImageConverter.ScalingMode = ScalingMode.Normal
'creates an instance of the DocToPDFConverter - responsible for Word to PDF conversion
Dim converter As New DocToPDFConverter()
'Set the conformance for PDF/A-1b conversion.
converter.Settings.PdfConformanceLevel = PdfConformanceLevel.Pdf_A1B
'Converts Word document into PDF document
Dim pdfDocument As PdfDocument = converter.ConvertToPDF(wordDocument)
'Saves the PDF file to file system
pdfDocument.Save("WordtoPDF.pdf")
'Closes the instance of document objects
pdfDocument.Close(True)
wordDocument.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/PDF-conformance-level).

### Enable Alternate Chunks

In the Word document, another Word documents are embedded in it and referred as AltChunks. This setting allows you to include the alternate chunks while converting Word to PDF conversion. As default, it includes alternate chunks.

The following code sample shows how to exclude the alternate chunk parts in Word to PDF conversion.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Open the file as Stream
FileStream docStream = new FileStream("Template.docx", FileMode.Open, FileAccess.Read);
//Loads file stream into Word document
WordDocument wordDocument = new WordDocument(docStream, Syncfusion.DocIO.FormatType.Automatic);
//Instantiation of DocIORenderer for Word to PDF conversion
DocIORenderer render = new DocIORenderer();
//Sets false to disable converting the alternate chunks present in Word document to PDF.
render.Settings.EnableAlternateChunks = false;
//Converts Word document into PDF document
PdfDocument pdfDocument = render.ConvertToPDF(wordDocument);
//Releases all resources used by the Word document and DocIO Renderer objects
render.Dispose();
wordDocument.Dispose();
//Saves the PDF file
MemoryStream outputStream = new MemoryStream();
pdfDocument.Save(outputStream);
//Closes the instance of PDF document object
pdfDocument.Close();
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Loads an existing Word document
WordDocument wordDocument = new WordDocument("Template.docx", FormatType.Docx);
//Initializes the ChartToImageConverter for converting charts during Word to pdf conversion
wordDocument.ChartToImageConverter = new ChartToImageConverter();
//Sets the scaling mode for charts (Normal mode reduces the Pdf file size)
wordDocument.ChartToImageConverter.ScalingMode = ScalingMode.Normal;
//Creates an instance of the DocToPDFConverter - responsible for Word to PDF conversion
DocToPDFConverter converter = new DocToPDFConverter();
//Sets false to disable converting the alternate chunks present in Word document to PDF.
converter.Settings.EnableAlternateChunks = false;
//Converts Word document into PDF document
PdfDocument pdfDocument = converter.ConvertToPDF(wordDocument);
//Saves the PDF file to file system
pdfDocument.Save("WordtoPDF.pdf");
//Closes the instance of document objects
pdfDocument.Close(true);
wordDocument.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Loads an existing Word document
Dim wordDocument As New WordDocument("Template.docx", FormatType.Docx)
'Initializes the ChartToImageConverter for converting charts during Word to pdf conversion
wordDocument.ChartToImageConverter = New ChartToImageConverter()
'Sets the scaling mode for charts (Normal mode reduces the Pdf file size)
wordDocument.ChartToImageConverter.ScalingMode = ScalingMode.Normal
'creates an instance of the DocToPDFConverter - responsible for Word to PDF conversion
Dim converter As New DocToPDFConverter()
'Sets false to disable converting the alternate chunks present in Word document to PDF.
converter.Settings.EnableAlternateChunks = false
'Converts Word document into PDF document
Dim pdfDocument As PdfDocument = converter.ConvertToPDF(wordDocument)
'Saves the PDF file to file system
pdfDocument.Save("WordtoPDF.pdf")
'Closes the instance of document objects
pdfDocument.Close(True)
wordDocument.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Disable-alternate-chunks).

### Complex Script Text

This setting allows you to **preserve the complex script text** in the converted PDF document.

The following code sample shows how to preserve the complex script text in the converted PDF document.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
FileStream fileStream = new FileStream("Template.docx", FileMode.Open);
//Loads an existing Word document
WordDocument wordDocument = new WordDocument(fileStream, FormatType.Docx);
//Instantiates DocIORenderer instance for Word to PDF conversion
DocIORenderer renderer = new DocIORenderer();
//Sets AutoDetectComplexScript property to true to detect the complex scripts automatically
renderer.Settings.AutoDetectComplexScript = true;
//Converts Word document into PDF document
PdfDocument pdfDocument = renderer.ConvertToPDF(wordDocument);
//Closes the instance of Word document object
wordDocument.Close();
//Releases the resources occupied by DocIORenderer instance
renderer.Dispose();
//Saves the PDF file  
MemoryStream outputStream = new MemoryStream();
pdfDocument.Save(outputStream);
//Closes the instance of PDF document object
pdfDocument.Close();
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Loads an existing Word document
WordDocument wordDocument = new WordDocument("Template.docx", FormatType.Docx);     
//Creates an instance of the DocToPDFConverter - responsible for Word to PDF conversion
DocToPDFConverter converter = new DocToPDFConverter();
//Sets AutoDetectComplexScript property to true to detect the complex scripts automatically
converter.Settings.AutoDetectComplexScript = true;
//Converts Word document into PDF document
PdfDocument pdfDocument = converter.ConvertToPDF(wordDocument);
//Saves the PDF file to file system
pdfDocument.Save("WordtoPDF.pdf");
//Closes the instance of document objects
pdfDocument.Close(true);
wordDocument.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Loads an existing Word document
Dim wordDocument As New WordDocument("Template.docx", FormatType.Docx)
'Initializes the ChartToImageConverter for converting charts during Word to pdf conversion
wordDocument.ChartToImageConverter = New ChartToImageConverter()
'Creates an instance of the DocToPDFConverter
Dim converter As New DocToPDFConverter()
'Sets AutoDetectComplexScript property to true to detect the complex scripts automatically
converter.Settings.AutoDetectComplexScript = True
'Converts Word document into PDF document
Dim pdfDocument As PdfDocument = converter.ConvertToPDF(wordDocument)
'Saves the PDF file 
pdfDocument.Save("WordtoPDF.pdf")
'Closes the instance of document objects
pdfDocument.Close(True)
wordDocument.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Preserve-complex-script-text-in-PDF).

### Hyphenation in Word-to-PDF conversion

Essential DocIO now allows hyphenating text in a Word document while converting it to PDF format based on the given language dictionaries. These dictionaries prescribe where words of a specific language can be hyphenated. Use the dictionary files as OpenOffice format dictionary.

N> If automatic hyphenation is not enabled in the Word document, you can enable it by using [WordDocument.Properties.Hyphenation.AutoHyphenation](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.Hyphenation.html#Syncfusion_DocIO_DLS_Hyphenation_AutoHyphenation) of DocIO.

The following code sample shows how to hyphenate text in a Word document while converting it to PDF format.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
FileStream fileStream = new FileStream("Template.docx", FileMode.Open);
//Loads an existing Word document
WordDocument wordDocument = new WordDocument(fileStream, FormatType.Docx);
//Instantiates DocIORenderer instance for Word to PDF conversion
DocIORenderer renderer = new DocIORenderer();
//Reads the language dictionary for hyphenation
FileStream dictionaryStream = new FileStream("hyphen_en_US.dic", FileMode.Open);
//Adds the hyphenation dictionary of the specified language
Hyphenator.Dictionaries.Add("en-US", dictionaryStream);
//Converts Word document into PDF document
PdfDocument pdfDocument = renderer.ConvertToPDF(wordDocument);
//Closes the instance of Word document object
wordDocument.Close();
//Releases the resources occupied by DocIORenderer instance
renderer.Dispose();
//Saves the PDF file  
MemoryStream outputStream = new MemoryStream();
pdfDocument.Save(outputStream);
//Closes the instance of PDF document object
pdfDocument.Close();
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Loads an existing Word document
WordDocument wordDocument = new WordDocument("Template.docx", FormatType.Docx);
//Initializes the ChartToImageConverter for converting charts during Word to pdf conversion
wordDocument.ChartToImageConverter = new ChartToImageConverter();
//Creates an instance of the DocToPDFConverter
DocToPDFConverter converter = new DocToPDFConverter();
//Adds the hyphenation dictionary of the specified language
FileStream dictionaryStream = new FileStream("hyphen_en_US.dic", FileMode.Open, FileAccess.Read);
//Adds the hyphenation dictionary of the specified language
Hyphenator.Dictionaries.Add("en-US", dictionaryStream);
//Converts Word document into PDF document
PdfDocument pdfDocument = converter.ConvertToPDF(wordDocument);
//Saves the PDF file 
pdfDocument.Save("WordtoPDF.pdf");
//Closes the instance of document objects
wordDocument.Close();
pdfDocument.Close(true);
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Loads an existing Word document
Dim wordDocument As New WordDocument("Template.docx", FormatType.Docx)
'Initializes the ChartToImageConverter for converting charts during Word to pdf conversion
wordDocument.ChartToImageConverter = New ChartToImageConverter()
'Creates an instance of the DocToPDFConverter
Dim converter As New DocToPDFConverter()
'Adds the hyphenation dictionary of the specified language
Dim dictionaryStream As New FileStream("hyphen_en_US .dic", mode:=FileMode.Open)
'Adds the hyphenation dictionary of the specified language
Hyphenator.Dictionaries.Add("en-US", dictionaryStream)
'Converts Word document into PDF document
Dim pdfDocument As PdfDocument = converter.ConvertToPDF(wordDocument)
'Saves the PDF file 
pdfDocument.Save("WordtoPDF.pdf")
'Closes the instance of document objects
pdfDocument.Close(True)
wordDocument.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Hyphenation-in-Word-to-PDF).

### Track changes in Word-to-PDF conversion

The following code sample shows how to **preserve revision marks in a generated PDF** when converting Word documents with tracked changes or revisions.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
FileStream fileStream = new FileStream("Template.docx", FileMode.Open);
//Loads an existing Word document
WordDocument wordDocument = new WordDocument(fileStream, FormatType.Docx);
//Sets revision types to preserve track changes in  Word when converting to PDF.
wordDocument.RevisionOptions.ShowMarkup = RevisionType.Deletions | RevisionType.Formatting | RevisionType.Insertions;
//Instantiates DocIORenderer instance for Word to PDF conversion
DocIORenderer renderer = new DocIORenderer();
//Converts Word document into PDF document
PdfDocument pdfDocument = renderer.ConvertToPDF(wordDocument);
//Closes the instance of Word document object
wordDocument.Close();
//Releases the resources occupied by DocIORenderer instance
renderer.Dispose();
//Saves the PDF file  
MemoryStream outputStream = new MemoryStream();
pdfDocument.Save(outputStream);
//Closes the instance of PDF document object
pdfDocument.Close();
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Loads an existing Word document
WordDocument wordDocument = new WordDocument("Template.docx", FormatType.Docx);
//Sets revision types to preserve track changes in Word when converting to PDF
wordDocument.RevisionOptions.ShowMarkup = RevisionType.Deletions | RevisionType.Formatting | RevisionType.Insertions;
//Creates an instance of the DocToPDFConverter
DocToPDFConverter converter = new DocToPDFConverter();
//Converts Word document into PDF document
PdfDocument pdfDocument = converter.ConvertToPDF(wordDocument);
//Closes the instance of Word document object
wordDocument.Close();
//Releases the resources occupied by DocToPDFConverter instance
converter.Dispose();
//Saves the PDF file
pdfDocument.Save("WordtoPDF.pdf");
//Closes the instance of PDF document object
pdfDocument.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Loads an existing Word document
Dim wordDocument As New WordDocument("Template.docx", FormatType.Docx)
'Sets revision types to preserve track changes in when converting to PDF conversion.
wordDocument.RevisionOptions.ShowMarkup = RevisionType.Deletions Or
RevisionType.Formatting Or RevisionType.Insertions
'Creates an instance of the DocToPDFConverter
Dim converter As New DocToPDFConverter()
'Converts Word document into PDF document
Dim pdfDocument As PdfDocument = converter.ConvertToPDF(wordDocument)
'Closes the instance of Word document object
wordDocument.Close()
'Releases the resources occupied by DocToPDFConverter instance
converter.Dispose()
'Saves the PDF file
pdfDocument.Save("WordtoPDF.pdf")
'Closes the instance of PDF document object
pdfDocument.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Track-changes-in-Word-to-PDF).

#### Change the Track Changes Color

You can customize how track changes markup appears in a generated PDF when converting Word documents into PDF. The following code sample shows how to customize revision marks colors.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
FileStream fileStream = new FileStream("Template.docx", FileMode.Open);
//Loads an existing Word document
WordDocument wordDocument = new WordDocument(fileStream, FormatType.Docx);
//Sets revision types to preserve track changes in  Word when converting to PDF.
wordDocument.RevisionOptions.ShowMarkup = RevisionType.Deletions | RevisionType.Formatting | RevisionType.Insertions;
//Sets the color to be used for revision bars that identify document lines containing revised information
wordDocument.RevisionOptions.RevisionBarsColor = RevisionColor.Blue;
//Sets the color to be used for inserted content Insertion
wordDocument.RevisionOptions.InsertedTextColor = RevisionColor.ClassicBlue;
//Sets the color to be used for deleted content Deletion
wordDocument.RevisionOptions.DeletedTextColor = RevisionColor.ClassicRed;
//Sets the color to be used for content with changes of formatting properties
wordDocument.RevisionOptions.RevisedPropertiesColor = RevisionColor.DarkYellow;
//Instantiates DocIORenderer instance for Word to PDF conversion
DocIORenderer renderer = new DocIORenderer();
//Converts Word document into PDF document
PdfDocument pdfDocument = renderer.ConvertToPDF(wordDocument);
//Closes the instance of Word document object
wordDocument.Close();
//Releases the resources occupied by DocIORenderer instance
renderer.Dispose();
//Saves the PDF file  
MemoryStream outputStream = new MemoryStream();
pdfDocument.Save(outputStream);
//Closes the instance of PDF document object
pdfDocument.Close();
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Loads an existing Word document
WordDocument wordDocument = new WordDocument("Template.docx", FormatType.Docx);
//Sets revision types to preserve track changes in Word when converting to PDF
wordDocument.RevisionOptions.ShowMarkup = RevisionType.Deletions | RevisionType.Formatting | RevisionType.Insertions;
//Sets the color to be used for revision bars that identify document lines containing revised information
wordDocument.RevisionOptions.RevisionBarsColor = RevisionColor.Blue;
//Sets the color to be used for inserted content Insertion
wordDocument.RevisionOptions.InsertedTextColor = RevisionColor.ClassicBlue;
//Sets the color to be used for deleted content Deletion
wordDocument.RevisionOptions.DeletedTextColor = RevisionColor.ClassicRed;
//Sets the color to be used for content with changes of formatting properties
wordDocument.RevisionOptions.RevisedPropertiesColor = RevisionColor.DarkYellow;
//Creates an instance of the DocToPDFConverter
DocToPDFConverter converter = new DocToPDFConverter();
//Converts Word document into PDF document
PdfDocument pdfDocument = converter.ConvertToPDF(wordDocument);
//Closes the instance of Word document object
wordDocument.Close();
//Releases the resources occupied by DocToPDFConverter instance
converter.Dispose();
//Saves the PDF file
pdfDocument.Save("WordtoPDF.pdf");
//Closes the instance of PDF document object
pdfDocument.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Loads an existing Word document
Dim wordDocument As New WordDocument("Template.docx", FormatType.Docx)
'Sets revision types to preserve track changes in when converting to PDF conversion
wordDocument.RevisionOptions.ShowMarkup = RevisionType.Deletions Or
RevisionType.Formatting Or RevisionType.Insertions
'Sets the color to be used for revision bars that identify document lines containing revised information
wordDocument.RevisionOptions.RevisionBarsColor = RevisionColor.Blue
'Sets the color to be used for inserted content Insertion
wordDocument.RevisionOptions.InsertedTextColor = RevisionColor.ClassicBlue
'Sets the color to be used for deleted content Deletion
wordDocument.RevisionOptions.DeletedTextColor = RevisionColor.ClassicRed
'Sets the color to be used for content with changes of formatting properties
wordDocument.RevisionOptions.RevisedPropertiesColor = RevisionColor.DarkYellow
'Creates an instance of the DocToPDFConverter
Dim converter As New DocToPDFConverter()
'Converts Word document into PDF document
Dim pdfDocument As PdfDocument = converter.ConvertToPDF(wordDocument)
'Closes the instance of Word document object
wordDocument.Close()
'Releases the resources occupied by DocToPDFConverter instance
converter.Dispose()
'Saves the PDF file
pdfDocument.Save("WordtoPDF.pdf")
'Closes the instance of PDF document object
pdfDocument.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Change-track-changes-color).

#### Show or Hide Revisions in Balloons

The default Word to PDF conversion renders the deletion and formatting changes in balloons when enabling [ShowMarkup](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.RevisionOptions.html#Syncfusion_DocIO_DLS_RevisionOptions_ShowMarkup) property. However, you can hide revisions in balloons by using following code example.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
FileStream fileStream = new FileStream("Template.docx", FileMode.Open);
//Loads an existing Word document
WordDocument wordDocument = new WordDocument(fileStream, FormatType.Docx);
//Sets revision types to preserve track changes in Word when converting to PDF
wordDocument.RevisionOptions.ShowMarkup = RevisionType.Deletions | RevisionType.Formatting | RevisionType.Insertions;
//Hides showing revisions in balloons when converting Word documents to PDF
wordDocument.RevisionOptions.ShowInBalloons = RevisionType.None;
//Instantiates DocIORenderer instance for Word to PDF conversion
DocIORenderer renderer = new DocIORenderer();
//Converts Word document into PDF document
PdfDocument pdfDocument = renderer.ConvertToPDF(wordDocument);
//Closes the instance of Word document object
wordDocument.Close();
//Releases the resources occupied by DocIORenderer instance
renderer.Dispose();
//Saves the PDF file  
MemoryStream outputStream = new MemoryStream();
pdfDocument.Save(outputStream);
//Closes the instance of PDF document object
pdfDocument.Close();
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Loads an existing Word document
WordDocument wordDocument = new WordDocument("Template.docx", FormatType.Docx);
//Sets revision types to preserve track changes in Word when converting to PDF
wordDocument.RevisionOptions.ShowMarkup = RevisionType.Deletions | RevisionType.Formatting | RevisionType.Insertions;
//Hides showing revisions in balloons when converting Word documents to PDF
wordDocument.RevisionOptions.ShowInBalloons = RevisionType.None;
//Creates an instance of the DocToPDFConverter
DocToPDFConverter converter = new DocToPDFConverter();
//Converts Word document into PDF document
PdfDocument pdfDocument = converter.ConvertToPDF(wordDocument);
//Closes the instance of Word document object
wordDocument.Close();
//Releases the resources occupied by DocToPDFConverter instance
converter.Dispose();
//Saves the PDF file
pdfDocument.Save("WordtoPDF.pdf");
//Closes the instance of PDF document object
pdfDocument.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Loads an existing Word document
Dim wordDocument As New WordDocument("Template.docx", FormatType.Docx)
'Sets revision types to preserve track changes in when converting to PDF conversion
wordDocument.RevisionOptions.ShowMarkup = RevisionType.Deletions Or
RevisionType.Formatting Or RevisionType.Insertions
'Hides showing revisions in balloons when converting Word documents to PDF
wordDocument.RevisionOptions.ShowInBalloons = RevisionType.None
'Creates an instance of the DocToPDFConverter
Dim converter As New DocToPDFConverter()
'Converts Word document into PDF document
Dim pdfDocument As PdfDocument = converter.ConvertToPDF(wordDocument)
'Closes the instance of Word document object
wordDocument.Close()
'Releases the resources occupied by DocToPDFConverter instance
converter.Dispose()
'Saves the PDF file
pdfDocument.Save("WordtoPDF.pdf")
'Closes the instance of PDF document object
pdfDocument.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Show-or-hide-revisions-in-balloons).

### Comments in Word-to-PDF conversion
The following code sample shows how to **preserve comments balloon in a generated PDF** when converting Word documents with comments. Also you can customize how comments balloon color appears in a generated PDF.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
using (FileStream fileStream = new FileStream("Template.docx", FileMode.Open))
{
    //Loads an existing Word document.
    using (WordDocument wordDocument = new WordDocument(fileStream,FormatType.Docx))
    {
        //Sets ShowInBalloons to render a document comments in converted PDF document.
        wordDocument.RevisionOptions.CommentDisplayMode = CommentDisplayMode.ShowInBalloons;
        //Sets the color to be used for Comment Balloon.
        wordDocument.RevisionOptions.CommentColor = RevisionColor.Blue;
        //Creates an instance of DocIORenderer.
        using (DocIORenderer renderer = new DocIORenderer())
        {
            //Converts Word document into PDF document.
            using (PdfDocument pdfDocument = renderer.ConvertToPDF(wordDocument))
            {
                //Saves the PDF file to file system.    
                using (FileStream outputStream = new FileStream("Sample.pdf", FileMode.Create, FileAccess.ReadWrite, FileShare.ReadWrite))
                {
                    pdfDocument.Save(outputStream);
                }
            }
        }
    }
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Loads an existing Word document.
using (WordDocument wordDocument = new WordDocument("Template.docx", FormatType.Docx))
{
    //Sets ShowInBalloons to render a document comments in converted PDF document.
    wordDocument.RevisionOptions.CommentDisplayMode = CommentDisplayMode.ShowInBalloons;
    //Sets the color to be used for Comment Balloon.
    wordDocument.RevisionOptions.CommentColor = RevisionColor.Blue;
    //Initializes the ChartToImageConverter for converting charts during Word to pdf conversion.
    wordDocument.ChartToImageConverter = new ChartToImageConverter();
    //Sets the scaling mode for charts.
    wordDocument.ChartToImageConverter.ScalingMode = ScalingMode.Normal;
    //Creates an instance of the DocToPDFConverter.
    using (DocToPDFConverter converter = new DocToPDFConverter())
    {
        //Converts Word document into PDF document.
        using (PdfDocument pdfDocument = converter.ConvertToPDF(wordDocument))
        {
            //Saves the PDF file to file system.
            pdfDocument.Save("Sample.pdf");
        }
    }
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Loads an existing Word document.
Using wordDocument As WordDocument = New WordDocument("Template.docx", FormatType.Docx)
    'Sets ShowInBalloons to render a document comments in converted PDF document.
    wordDocument.RevisionOptions.CommentDisplayMode = CommentDisplayMode.ShowInBalloons
    'Sets the color to be used for Comment Balloon.
    wordDocument.RevisionOptions.CommentColor = RevisionColor.Blue
    'Initializes the ChartToImageConverter for converting charts during Word to pdf conversion.
    wordDocument.ChartToImageConverter = New ChartToImageConverter
    'Sets the scaling mode for charts.
    wordDocument.ChartToImageConverter.ScalingMode = ScalingMode.Normal
    'Creates an instance of the DocToPDFConverter.
    Using converter As New DocToPDFConverter()
        'Converts Word document into PDF document.
        Using pdfDocument As PdfDocument = converter.ConvertToPDF(wordDocument)
            'Saves the PDF file to file system.
            pdfDocument.Save("Sample.pdf")
        End Using
    End Using
End Using
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Preserve-comments-in-Word-to-PDF).

### Preserve Ole Equation as bitmap image

This setting allows you to preserve Ole Equation as bitmap image in the converted PDF document.

The following code sample shows how to preserve Ole Equation as bitmap image in the converted PDF document.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//DocIO supports to preserve the Ole Equation as bitmap image in the converted PDF document in Windows forms, WPF, ASP.NET and ASP.NET MVC platform alone.
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Loads an existing Word document
WordDocument wordDocument = new WordDocument("Template.docx", FormatType.Docx);     
//Creates an instance of the DocToPDFConverter - responsible for Word to PDF conversion
DocToPDFConverter converter = new DocToPDFConverter();
//Sets a value indicating whether to preserve the Ole Equation as bitmap image while converting a Word document to PDF
converter.Settings.PreserveOleEquationAsBitmap = true;
//Converts Word document into PDF document
PdfDocument pdfDocument = converter.ConvertToPDF(wordDocument);
//Saves the PDF file to file system
pdfDocument.Save("WordtoPDF.pdf");
//Closes the instance of document objects
pdfDocument.Close(true);
wordDocument.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Loads an existing Word document
Dim wordDocument As New WordDocument("Template.docx", FormatType.Docx)
'Initializes the ChartToImageConverter for converting charts during Word to pdf conversion
wordDocument.ChartToImageConverter = New ChartToImageConverter()
'Creates an instance of the DocToPDFConverter
Dim converter As New DocToPDFConverter()
'Sets a value indicating whether to preserve the Ole Equation as bitmap image while converting a Word document to PDF
converter.Settings.PreserveOleEquationAsBitmap = true
'Converts Word document into PDF document
Dim pdfDocument As PdfDocument = converter.ConvertToPDF(wordDocument)
'Saves the PDF file 
pdfDocument.Save("WordtoPDF.pdf")
'Closes the instance of document objects
pdfDocument.Close(True)
wordDocument.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Ole-Equation-as-bitmap).

### Restrict all permission in a PDF document

You can restrict all the permission in a PDF document using [PdfPermissionsFlags](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfPermissionsFlags.html).

The below code example shows how to restrict Copying and Printing permission of the PDF document.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Open the file as Stream
FileStream docStream = new FileStream("Template.docx", FileMode.Open, FileAccess.Read);
//Loads file stream into Word document
WordDocument wordDocument = new WordDocument(docStream, FormatType.Automatic);
docStream.Dispose();
//Instantiation of DocIORenderer for Word to PDF conversion
DocIORenderer render = new DocIORenderer();
//Converts Word document into PDF document
PdfDocument pdfDocument = render.ConvertToPDF(wordDocument);
//Document security.
PdfSecurity security = pdfDocument.Security;
//Specifies key size and encryption algorithm using 256-bit key in AES mode.
security.KeySize = PdfEncryptionKeySize.Key256Bit;
security.Algorithm = Syncfusion.Pdf.Security.PdfEncryptionAlgorithm.AES;
security.OwnerPassword = "syncfusion";
//It restrict printing and copying of PDF document
security.Permissions = ~(PdfPermissionsFlags.CopyContent | PdfPermissionsFlags.Print);
//Releases all resources used by the Word document and DocIO Renderer objects
render.Dispose();
wordDocument.Dispose();
//Saves the PDF file
FileStream outputFile = new FileStream("Output.docx", FileMode.OpenOrCreate, FileAccess.ReadWrite);
pdfDocument.Save(outputFile);
//Closes the instance of PDF document object
pdfDocument.Close();
outputFile.Dispose();
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Creates an instance of WordDocument class
WordDocument document = new WordDocument("Template.docx");
//Creates an instance of the DocToPDFConverter
DocToPDFConverter converter = new DocToPDFConverter();
//Converts Word document into PDF document
PdfDocument pdfDocument = converter.ConvertToPDF(document);
//Document security.
PdfSecurity security = pdfDocument.Security;
//Specifies key size and encryption algorithm using 256-bit key in AES mode.
security.KeySize = PdfEncryptionKeySize.Key256Bit;
security.Algorithm = Syncfusion.Pdf.Security.PdfEncryptionAlgorithm.AES;
security.OwnerPassword = "syncfusion";
//It restrict printing and copying of PDF document
security.Permissions =  ~(PdfPermissionsFlags.CopyContent | PdfPermissionsFlags.Print);
pdfDocument.Save("Output.pdf");
pdfDocument.Close();
converter.Dispose();
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Creates an instance of WordDocument class
Dim document As WordDocument = New WordDocument("Template.docx")
'Creates an instance of the DocToPDFConverter
Dim converter As DocToPDFConverter = New DocToPDFConverter()
'Converts Word document into PDF document
Dim pdfDocument As PdfDocument = converter.ConvertToPDF(document)
'Document security.
Dim security As PdfSecurity = pdfDocument.Security
'Specifies key size and encryption algorithm using 256-bit key in AES mode.
security.KeySize = PdfEncryptionKeySize.Key256Bit
security.Algorithm = Syncfusion.Pdf.Security.PdfEncryptionAlgorithm.AES
security.OwnerPassword = "syncfusion"
'It restrict printing and copying of PDF document
security.Permissions = Not (PdfPermissionsFlags.CopyContent Or PdfPermissionsFlags.Print)
pdfDocument.Save("Output.pdf")
pdfDocument.Close()
converter.Dispose()
document.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Restrict-permission-in-PDF).

## Font Substitution

When the necessary fonts used in the Word document has not been installed in the production machine, then Essential DocIO uses the ”Microsoft Sans Serif” as default font for rendering the text. This leads to preservation difference in generated PDF as each font has different glyphs for characters. To learn more about the default font substitution, click [here](https://support.syncfusion.com/kb/article/6821/what-happens-when-the-word-document-used-fonts-for-a-text-is-not-installed-in-production).

To avoid this, the Essential DocIO library allows you to set an alternate font for the missing font used in the Word document.

### Use alternate font from installed fonts

You can use any other alternate fonts instead of "Microsoft Sans Serif" to layout and render the text during Word to PDF conversion by using the [SubstituteFont](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.FontSettings.html) event.

The following code example shows how to use alternate font instead of "Microsoft Sans Serif" when the specified font is not installed in the machine. 

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Open the file as Stream
FileStream docStream = new FileStream("Template.docx", FileMode.Open, FileAccess.Read);
//Loads file stream into Word document
WordDocument wordDocument = new WordDocument(docStream, Syncfusion.DocIO.FormatType.Docx);
//Hooks the font substitution event
wordDocument.FontSettings.SubstituteFont += FontSettings_SubstituteFont;
//Instantiation of DocIORenderer for Word to PDF conversion
DocIORenderer render = new DocIORenderer();
//Converts Word document into PDF document
PdfDocument pdfDocument = render.ConvertToPDF(wordDocument);
//Unhooks the font substitution event after converting to PDF
wordDocument.FontSettings.SubstituteFont -= FontSettings_SubstituteFont;
//Releases all resources used by the Word document and DocIO Renderer objects
render.Dispose();
wordDocument.Dispose();
//Saves the PDF file
MemoryStream outputStream = new MemoryStream();
pdfDocument.Save(outputStream);
//Closes the instance of PDF document object
pdfDocument.Close();
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Loads an existing Word document
WordDocument wordDocument = new WordDocument("Template.docx", FormatType.Docx);
//Initializes the ChartToImageConverter for converting charts during Word to PDF conversion
wordDocument.ChartToImageConverter = new ChartToImageConverter();
//Hooks the font substitution event
wordDocument.FontSettings.SubstituteFont += FontSettings_SubstituteFont;
//Creates an instance of the DocToPDFConverter
DocToPDFConverter converter = new DocToPDFConverter();
//Converts Word document into PDF document
PdfDocument pdfDocument = converter.ConvertToPDF(wordDocument);
//Unhooks the font substitution event after converting to PDF
wordDocument.FontSettings.SubstituteFont -= FontSettings_SubstituteFont;
//Closes the instance of Word document object
wordDocument.Close();
//Releases the resources occupied by DocToPDFConverter instance
converter.Dispose();
//Saves the PDF file
pdfDocument.Save("WordtoPDF.pdf");
//Closes the instance of PDF document object
pdfDocument.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Loads an existing Word document
Dim wordDocument As New WordDocument("Template.docx", FormatType.Docx)
'Initializes the ChartToImageConverter for converting charts during Word to PDF conversion
wordDocument.ChartToImageConverter = New ChartToImageConverter()
'Hooks the font substitution event
AddHandler wordDocument.FontSettings.SubstituteFont, AddressOf FontSettings_SubstituteFont
'Creates an instance of the DocToPDFConverter
Dim converter As DocToPDFConverter = New DocToPDFConverter
'Converts Word document into PDF document
Dim pdfDocument As PdfDocument = converter.ConvertToPDF(wordDocument)
'Unhooks the font substitution event after converting to PDF
RemoveHandler wordDocument.FontSettings.SubstituteFont, AddressOf FontSettings_SubstituteFont
'Closes the instance of Word document object
wordDocument.Close()
'Releases the resources occupied by DocToPDFConverter instance
converter.Dispose()
'Saves the PDF file
pdfDocument.Save("WordtoPDF.pdf")
'Closes the instance of PDF document object
pdfDocument.Close()
{% endhighlight %}

{% endtabs %}

###### Event Handler to use alternate installed font

The following code example shows how to set the **alternate installed font** instead of "Microsoft Sans Serif" during Word to PDF conversion.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
private void FontSettings_SubstituteFont(object sender, SubstituteFontEventArgs args)
{
    //Sets the alternate font when a specified font is not installed in the production environment
    //If "Arial Unicode MS" font is not installed, then it uses the "Arial" font
    //For other missing fonts, uses the "Times New Roman"
    if (args.OriginalFontName == "Arial Unicode MS")
        args.AlternateFontName = "Arial";
    else
        args.AlternateFontName = "Times New Roman";
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
private void FontSettings_SubstituteFont(object sender, SubstituteFontEventArgs args)
{
    //Sets the alternate font when a specified font is not installed in the production environment
    //If "Arial Unicode MS" font is not installed, then it uses the "Arial" font
    //For other missing fonts, uses the "Times New Roman"
    if (args.OriginalFontName == "Arial Unicode MS")
        args.AlternateFontName = "Arial";
    else
        args.AlternateFontName = "Times New Roman";
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Private Sub FontSettings_SubstituteFont(ByVal sender As Object, ByVal args As SubstituteFontEventArgs)
    'Sets the alternate font when a specified font is not installed in the production environment
    'If "Arial Unicode MS" font is not installed, then it uses the "Arial" font
    'For other missing fonts, uses the "Times New Roman"
    If args.OriginalFontName = "Arial Unicode MS" Then
        args.AlternateFontName = "Arial"
    Else
        args.AlternateFontName = "Times New Roman"
    End If
End Sub
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Use-alternate-installed-font).

###### Event Handler to use alternate font without installing

The following code example shows how to use the alternate fonts instead of "Microsoft Sans Serif" **without installing the fonts** into production machine.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
private void FontSettings_SubstituteFont(object sender, SubstituteFontEventArgs args)
{
    //Sets the alternate font when a specified font is not installed in the production environment
    if (args.OrignalFontName == "Arial Unicode MS" && args.FontStyle == FontStyle.Regular)
        args.AlternateFontStream = new FileStream("Arial.TTF", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
    else
        args.AlternateFontName = "Times New Roman";
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
private void FontSettings_SubstituteFont(object sender, SubstituteFontEventArgs args)
{
    //Sets the alternate font when a specified font is not installed in the production environment
    if (args.OrignalFontName == "Arial Unicode MS" && args.FontStyle == FontStyle.Regular)
        args.AlternateFontStream =  new FileStream("Arial.TTF" ,FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
    else
        args.AlternateFontName = "Times New Roman";
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Private Sub SubstituteFont(ByVal sender As Object, ByVal args As SubstituteFontEventArgs)
    'Sets the alternate font when a specified font is not installed in the production environment
    If args.OrignalFontName = "Arial Unicode MS" && args.FontStyle == FontStyle.Regular Then
        args.AlternateFontStream = New FileStream("Arial.TTF" ,FileMode.Open, FileAccess.Read, FileShare.ReadWrite)
    Else
        args.AlternateFontName = "Times New Roman"
    End If
End Sub
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Use-alternate-font-without-installing).

N> The above event will be triggered only if the specified font is not installed in production machine.

## Fallback fonts

During Word to PDF conversions, if a glyph of the input text is unavailable in the specified font, the text will not be rendered properly. To address this, the Syncfusion Word (DocIO) library allows users to specify fallback fonts. When a glyph is missing, the library will use one of the fallback fonts to render the text correctly in the output PDF document.

Users can configure fallback fonts in the following ways:
* Initialize default fallback fonts.
* Set custom fonts as fallback fonts for specific script types, including Arabic, Hebrew, Chinese, Japanese, and more.
* Set custom fonts as fallback fonts for a particular range of Unicode text.

N> DocIO internally uses user-initialized or specified fallback fonts for Unicode characters during Word to PDF conversion. Therefore, the specified fallback fonts must be installed in the production environment or embedded in the input Word document (DOCX). Otherwise, it will not render the text properly using the fallback fonts.

### Initialize default fallback fonts

The following code example demonstrates how to initialize a default fallback fonts while converting a Word document to PDF. The *InitializeDefault* API sets the default fallback fonts for specific script types like Arabic, Hebrew, Chinese, Japanese etc.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Opens the file as stream.
using (FileStream inputStream = new FileStream("Template.docx", FileMode.Open, FileAccess.Read))
{
   //Loads an existing Word document file stream.
   using (WordDocument wordDocument = new WordDocument(inputStream, Syncfusion.DocIO.FormatType.Docx))
   {
      //Initialize the default fallback fonts collection.
      wordDocument.FontSettings.FallbackFonts.InitializeDefault();
      //Instantiation of DocIORenderer for Word to PDF conversion.
      using (DocIORenderer render = new DocIORenderer())
      {
         //Converts Word document into PDF document.
         using (PdfDocument pdfDocument = render.ConvertToPDF(wordDocument))
         {
            //Saves the PDF file to file system.
            using (FileStream outputStream = new FileStream("WordToPDF.pdf", FileMode.OpenOrCreate, FileAccess.ReadWrite))
            {
               pdfDocument.Save(outputStream);
            }
         }
      }
   }
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Loads an existing Word document.
using (WordDocument wordDocument = new WordDocument("Template.docx", Syncfusion.DocIO.FormatType.Docx))
{
   //Initialize the default fallback fonts collection.
   wordDocument.FontSettings.FallbackFonts.InitializeDefault();
   //Instantiation of DocToPDFConverter for Word to PDF conversion.
   using (DocToPDFConverter converter = new DocToPDFConverter())
   {
      //Converts Word document into PDF document.
      using (PdfDocument pdfDocument = converter.ConvertToPDF(wordDocument))
      {
         //Saves the PDF file to file system.
         pdfDocument.Save("WordToPDF.pdf");
      }
   }
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Loads an existing Word document.
Using wordDocument As WordDocument = New WordDocument("Template.docx", FormatType.Docx)
    'Initialize the default fallback fonts collection.
    wordDocument.FontSettings.FallbackFonts.InitializeDefault()
    'Instantiation of DocToPDFConverter for Word to PDF conversion.
    Using converter As New DocToPDFConverter()
        'Converts Word document into PDF document.
        Using pdfDocument As PdfDocument = converter.ConvertToPDF(wordDocument)
            'Saves the PDF file to file system.
            pdfDocument.Save("WordToPDF.pdf")
        End Using
    End Using
End Using
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Initialize-default-fallback-fonts).

### Fallback fonts based on script type

The following code example demonstrates how a user can add fallback fonts based on the script types, which DocIO considers internally when converting a Word document to PDF.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Opens the file as stream.
using (FileStream inputStream = new FileStream("Template.docx", FileMode.Open, FileAccess.Read))
{
   //Loads an existing Word document file stream.
   using (WordDocument wordDocument = new WordDocument(inputStream, Syncfusion.DocIO.FormatType.Docx))
   {
      //Adds fallback font for "Arabic" script type.
      wordDocument.FontSettings.FallbackFonts.Add(ScriptType.Arabic, "Arial, Times New Roman");
      //Adds fallback font for "Hebrew" script type.
      wordDocument.FontSettings.FallbackFonts.Add(ScriptType.Hebrew, "Arial, Courier New");
      //Adds fallback font for "Hindi" script type.
      wordDocument.FontSettings.FallbackFonts.Add(ScriptType.Hindi, "Mangal, Nirmala UI");
      //Adds fallback font for "Chinese" script type.
      wordDocument.FontSettings.FallbackFonts.Add(ScriptType.Chinese, "DengXian, MingLiU");
      //Adds fallback font for "Japanese" script type.
      wordDocument.FontSettings.FallbackFonts.Add(ScriptType.Japanese, "Yu Mincho, MS Mincho");
      //Adds fallback font for "Thai" script type.
      wordDocument.FontSettings.FallbackFonts.Add(ScriptType.Thai, "Tahoma, Microsoft Sans Serif");
      //Adds fallback font for "Korean" script type.
      wordDocument.FontSettings.FallbackFonts.Add(ScriptType.Korean, "Malgun Gothic, Batang");
      //Instantiation of DocIORenderer for Word to PDF conversion.
      using (DocIORenderer render = new DocIORenderer())
      {
         //Converts Word document into PDF document.
         using (PdfDocument pdfDocument = render.ConvertToPDF(wordDocument))
         {
            //Saves the PDF file to file system.
            using (FileStream outputStream = new FileStream("WordToPDF.pdf", FileMode.OpenOrCreate, FileAccess.ReadWrite))
            {
               pdfDocument.Save(outputStream);
            }
         }
      }
   }
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Loads an existing Word document.
using (WordDocument wordDocument = new WordDocument("Template.docx", Syncfusion.DocIO.FormatType.Docx))
{
   //Adds fallback font for "Arabic" script type.
   wordDocument.FontSettings.FallbackFonts.Add(ScriptType.Arabic, "Arial, Times New Roman");
   //Adds fallback font for "Hebrew" script type.
   wordDocument.FontSettings.FallbackFonts.Add(ScriptType.Hebrew, "Arial, Courier New");
   //Adds fallback font for "Hindi" script type.
   wordDocument.FontSettings.FallbackFonts.Add(ScriptType.Hindi, "Mangal, Nirmala UI");
   //Adds fallback font for "Chinese" script type.
   wordDocument.FontSettings.FallbackFonts.Add(ScriptType.Chinese, "DengXian, MingLiU");
   //Adds fallback font for "Japanese" script type.
   wordDocument.FontSettings.FallbackFonts.Add(ScriptType.Japanese, "Yu Mincho, MS Mincho");
   //Adds fallback font for "Thai" script type.
   wordDocument.FontSettings.FallbackFonts.Add(ScriptType.Thai, "Tahoma, Microsoft Sans Serif");
   //Adds fallback font for "Korean" script type.
   wordDocument.FontSettings.FallbackFonts.Add(ScriptType.Korean, "Malgun Gothic, Batang");
   //Instantiation of DocToPDFConverter for Word to PDF conversion.
   using (DocToPDFConverter converter = new DocToPDFConverter())
   {
      //Converts Word document into PDF document.
      using (PdfDocument pdfDocument = converter.ConvertToPDF(wordDocument))
      {
         //Saves the PDF file to file system.
         pdfDocument.Save("WordToPDF.pdf");
      }
   }
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Loads an existing Word document.
Using wordDocument As WordDocument = New WordDocument("Template.docx", FormatType.Docx)
    'Adds fallback font for "Arabic" script type.
    wordDocument.FontSettings.FallbackFonts.Add(ScriptType.Arabic, "Arial, Times New Roman")
    'Adds fallback font for "Hebrew" script type.
    wordDocument.FontSettings.FallbackFonts.Add(ScriptType.Hebrew, "Arial, Courier New")
    'Adds fallback font for "Hindi" script type.
    wordDocument.FontSettings.FallbackFonts.Add(ScriptType.Hindi, "Mangal, Nirmala UI")
    'Adds fallback font for "Chinese" script type.
    wordDocument.FontSettings.FallbackFonts.Add(ScriptType.Chinese, "DengXian, MingLiU")
    'Adds fallback font for "Japanese" script type.
    wordDocument.FontSettings.FallbackFonts.Add(ScriptType.Japanese, "Yu Mincho, MS Mincho")
    'Adds fallback font for "Thai" script type.
    wordDocument.FontSettings.FallbackFonts.Add(ScriptType.Thai, "Tahoma, Microsoft Sans Serif")
    'Adds fallback font for "Korean" script type.
    wordDocument.FontSettings.FallbackFonts.Add(ScriptType.Korean, "Malgun Gothic, Batang")
    'Instantiation of DocToPDFConverter for Word to PDF conversion.
    Using converter As New DocToPDFConverter()
        'Converts Word document into PDF document.
        Using pdfDocument As PdfDocument = converter.ConvertToPDF(wordDocument)
            'Saves the PDF file to file system.
            pdfDocument.Save("WordToPDF.pdf")
        End Using
    End Using
End Using
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Fallback-fonts-based-on-scripttype).

### Fallback fonts for range of Unicode text

Users can set fallback fonts for specific Unicode range of text to be used in Word to PDF conversion.

The following code example demonstrates how users can add fallback fonts by using a specific Unicode range of text that DocIO considers internally while converting a Word document to PDF.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Opens the file as stream.
using (FileStream inputStream = new FileStream("Template.docx", FileMode.Open, FileAccess.Read))
{
   //Loads an existing Word document file stream.
   using (WordDocument wordDocument = new WordDocument(inputStream, Syncfusion.DocIO.FormatType.Docx))
   {
      //Adds fallback font for "Arabic" specific unicode range.
      wordDocument.FontSettings.FallbackFonts.Add(new FallbackFont(0x0600, 0x06ff, "Arial"));
      //Adds fallback font for "Hebrew" specific unicode range.
      wordDocument.FontSettings.FallbackFonts.Add(new FallbackFont(0x0590, 0x05ff, "Times New Roman"));
      //Adds fallback font for "Hindi" specific unicode range.
      wordDocument.FontSettings.FallbackFonts.Add(new FallbackFont(0x0900, 0x097F, "Nirmala UI"));
      //Adds fallback font for "Chinese" specific unicode range.
      wordDocument.FontSettings.FallbackFonts.Add(new FallbackFont(0x4E00, 0x9FFF, "DengXian"));
      //Adds fallback font for "Japanese" specific unicode range.
      wordDocument.FontSettings.FallbackFonts.Add(new FallbackFont(0x3040, 0x309F, "MS Gothic"));
      //Adds fallback font for "Thai" specific unicode range.
      wordDocument.FontSettings.FallbackFonts.Add(new FallbackFont(0x0E00, 0x0E7F, "Tahoma"));
      //Adds fallback font for "Korean" specific unicode range.
      wordDocument.FontSettings.FallbackFonts.Add(new FallbackFont(0xAC00, 0xD7A3, "Malgun Gothic"));
      //Instantiation of DocIORenderer for Word to PDF conversion.
      using (DocIORenderer render = new DocIORenderer())
      {
         //Converts Word document into PDF document.
         using (PdfDocument pdfDocument = render.ConvertToPDF(wordDocument))
         {
            //Saves the PDF file to file system.
            using (FileStream outputStream = new FileStream("WordToPDF.pdf", FileMode.OpenOrCreate, FileAccess.ReadWrite))
            {
               pdfDocument.Save(outputStream);
            }
         }
      }
   }
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Loads an existing Word document.
using (WordDocument wordDocument = new WordDocument("Template.docx", Syncfusion.DocIO.FormatType.Docx))
{
   //Adds fallback font for "Arabic" specific unicode range.
   wordDocument.FontSettings.FallbackFonts.Add(new FallbackFont(0x0600, 0x06ff, "Arial"));
   //Adds fallback font for "Hebrew" specific unicode range.
   wordDocument.FontSettings.FallbackFonts.Add(new FallbackFont(0x0590, 0x05ff, "Times New Roman"));
   //Adds fallback font for "Hindi" specific unicode range.
   wordDocument.FontSettings.FallbackFonts.Add(new FallbackFont(0x0900, 0x097F, "Nirmala UI"));
   //Adds fallback font for "Chinese" specific unicode range.
   wordDocument.FontSettings.FallbackFonts.Add(new FallbackFont(0x4E00, 0x9FFF, "DengXian"));
   //Adds fallback font for "Japanese" specific unicode range.
   wordDocument.FontSettings.FallbackFonts.Add(new FallbackFont(0x3040, 0x309F, "MS Gothic"));
   //Adds fallback font for "Thai" specific unicode range.
   wordDocument.FontSettings.FallbackFonts.Add(new FallbackFont(0x0E00, 0x0E7F, "Tahoma"));
   //Adds fallback font for "Korean" specific unicode range.
   wordDocument.FontSettings.FallbackFonts.Add(new FallbackFont(0xAC00, 0xD7A3, "Malgun Gothic"));
   //Instantiation of DocToPDFConverter for Word to PDF conversion.
   using (DocToPDFConverter converter = new DocToPDFConverter())
   {
      //Converts Word document into PDF document.
      using (PdfDocument pdfDocument = converter.ConvertToPDF(wordDocument))
      {
         //Saves the PDF file to file system.
         pdfDocument.Save("WordToPDF.pdf");
      }
   }
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Loads an existing Word document.
Using wordDocument As WordDocument = New WordDocument("Template.docx", FormatType.Docx)
    'Adds fallback font for "Arabic" specific unicode range.
    wordDocument.FontSettings.FallbackFonts.Add(New FallbackFont(0x0600, 0x06ff, "Arial"))
    'Adds fallback font for "Hebrew" specific unicode range.
    wordDocument.FontSettings.FallbackFonts.Add(New FallbackFont(0x0590, 0x05ff, "Times New Roman"))
    'Adds fallback font for "Hindi" specific unicode range.
    wordDocument.FontSettings.FallbackFonts.Add(New FallbackFont(0x0900, 0x097F, "Nirmala UI"))
    'Adds fallback font for "Chinese" specific unicode range.
    wordDocument.FontSettings.FallbackFonts.Add(New FallbackFont(0x4E00, 0x9FFF, "DengXian"))
    'Adds fallback font for "Japanese" specific unicode range.
    wordDocument.FontSettings.FallbackFonts.Add(New FallbackFont(0x3040, 0x309F, "MS Gothic"))
    'Adds fallback font for "Thai" specific unicode range.
    wordDocument.FontSettings.FallbackFonts.Add(New FallbackFont(0x0E00, 0x0E7F, "Tahoma"))
    'Adds fallback font for "Korean" specific unicode range.
    wordDocument.FontSettings.FallbackFonts.Add(New FallbackFont(0xAC00, 0xD7A3, "Malgun Gothic"))
    'Instantiation of DocToPDFConverter for Word to PDF conversion.
    Using converter As New DocToPDFConverter()
        'Converts Word document into PDF document.
        Using pdfDocument As PdfDocument = converter.ConvertToPDF(wordDocument)
            'Saves the PDF file to file system.
            pdfDocument.Save("WordToPDF.pdf")
        End Using
    End Using
End Using
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Fallback-fonts-for-Unicode-range).

### Modify the exiting fallback fonts

The following code example demonstrates how user can modify or customize the existing fallback fonts using *FontNames* API while converting a Word document to PDF.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Opens the file as stream.
using (FileStream inputStream = new FileStream("Template.docx", FileMode.Open, FileAccess.Read))
{
   //Loads an existing Word document file stream.
   using (WordDocument wordDocument = new WordDocument(inputStream, Syncfusion.DocIO.FormatType.Docx))
   {
      //Initialize the default fallback fonts collection.
      wordDocument.FontSettings.FallbackFonts.InitializeDefault();
      FallbackFonts fallbackFonts = wordDocument.FontSettings.FallbackFonts;
      foreach (FallbackFont fallbackFont in fallbackFonts) 
      {
         //Customize a default fallback font name as "David" for the Hebrew script.
         if (fallbackFont.ScriptType == ScriptType.Hebrew)
            fallbackFont.FontNames = "David";
         //Customize a default fallback font name as "Microsoft Sans Serif" for the Thai script.
         else if (fallbackFont.ScriptType == ScriptType.Thai)
            fallbackFont.FontNames = "Microsoft Sans Serif";
      }
      //Instantiation of DocIORenderer for Word to PDF conversion.
      using (DocIORenderer render = new DocIORenderer())
      {
         //Converts Word document into PDF document.
         using (PdfDocument pdfDocument = render.ConvertToPDF(wordDocument))
         {
            //Saves the PDF file to file system.
            using (FileStream outputStream = new FileStream("WordToPDF.pdf", FileMode.OpenOrCreate, FileAccess.ReadWrite))
            {
               pdfDocument.Save(outputStream);
            }
         }
      }
   }
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Loads an existing Word document.
using (WordDocument wordDocument = new WordDocument("Template.docx", Syncfusion.DocIO.FormatType.Docx))
{
   //Initialize the default fallback fonts collection.
   wordDocument.FontSettings.FallbackFonts.InitializeDefault();
   FallbackFonts fallbackFonts = wordDocument.FontSettings.FallbackFonts;
   foreach (FallbackFont fallbackFont in fallbackFonts) 
   {
      //Customize a default fallback font name as "David" for the Hebrew script.
      if (fallbackFont.ScriptType == ScriptType.Hebrew)
         fallbackFont.FontNames = "David";
      //Customize a default fallback font name as "Microsoft Sans Serif" for the Thai script.
      else if (fallbackFont.ScriptType == ScriptType.Thai)
         fallbackFont.FontNames = "Microsoft Sans Serif";
   }
   //Instantiation of DocToPDFConverter for Word to PDF conversion.
   using (DocToPDFConverter converter = new DocToPDFConverter())
   {
      //Converts Word document into PDF document.
      using (PdfDocument pdfDocument = converter.ConvertToPDF(wordDocument))
      {
         //Saves the PDF file to file system.
         pdfDocument.Save("WordToPDF.pdf");
      }
   }
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Loads an existing Word document.
Using wordDocument As WordDocument = New WordDocument("Template.docx", FormatType.Docx)
    'Initialize the default fallback fonts collection.
    wordDocument.FontSettings.FallbackFonts.InitializeDefault()
    Dim fallbackFonts As FallbackFonts = wordDocument.FontSettings.FallbackFonts
    For Each fallbackFont As FallbackFont In fallbackFonts
      'Customize a default fallback font name as "David" for the Hebrew script.
      If fallbackFont.ScriptType = ScriptType.Hebrew Then
         fallbackFont.FontNames = "David"
      'Customize a default fallback font name as "Microsoft Sans Serif" for the Thai script.
      ElseIf fallbackFont.ScriptType = ScriptType.Thai Then
         fallbackFont.FontNames = "Microsoft Sans Serif"
      End If
    Next
    'Instantiation of DocToPDFConverter for Word to PDF conversion.
    Using converter As New DocToPDFConverter()
        'Converts Word document into PDF document.
        Using pdfDocument As PdfDocument = converter.ConvertToPDF(wordDocument)
            'Saves the PDF file to file system.
            pdfDocument.Save("WordToPDF.pdf")
        End Using
    End Using
End Using
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Modify-the-exiting-fallback-fonts).

### Supported script types

The following table illustrates the supported script types by the .NET Word library (DocIO) in Word to PDF conversion.

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

## Show Warning for Unsupported Elements

When converting a Word document to a PDF, the presence of unsupported elements in the input Word document can lead to preservation issues in the converted PDF. The .NET Word library (DocIO) contains [Warning](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocToPDFConverter.DocToPDFConverterSettings.html#Syncfusion_DocToPDFConverter_DocToPDFConverterSettings_Warning) API, which helps to detect and handle these unsupported elements during the conversion process. This API holds the information of unsupported elements once found in the input Word document. 

Users can display warning messages for the unsupported elements using the [WarningType](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WarningInfo.html#Syncfusion_DocIO_DLS_WarningInfo_WarningType) during Word to PDF conversion. Users can set a flag to stop the conversion process based on the warning. 

The following code demonstrates how to stop conversion if the input Word document has an unsupported element like SmartArt during Word to PDF conversion.


{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
using (FileStream fileStream = new FileStream("Input.docx", FileMode.Open))
{
    //Loads an existing Word document.
    using (WordDocument wordDocument = new WordDocument(fileStream, Syncfusion.DocIO.FormatType.Automatic))
    {
        //Creates an instance of DocIORenderer.
        using (DocIORenderer renderer = new DocIORenderer())
        {
            renderer.Settings.Warning = new DocumentWarning();
            //Converts Word document into a PDF document.
            using (PdfDocument pdfDocument = renderer.ConvertToPDF(wordDocument))
            {
                //If the IsCanceled boolean is enabled, the input document will contain an unsupported element.
                if (renderer.IsCanceled)
                {
                    Console.WriteLine("The execution stopped due to unsupported element.");
                    Console.ReadKey();
                }
                else
                {
                    //Saves the PDF file.
                    FileStream outputFile = new FileStream("Output.pdf", FileMode.OpenOrCreate, FileAccess.ReadWrite);
                    pdfDocument.Save(outputFile);
                    outputFile.Dispose();
                    Console.WriteLine("Success");
                }
            }
        }
    }
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
WordDocument wordDocument = new WordDocument("Input.docx");
DocToPDFConverter converter = new DocToPDFConverter();
converter.Settings.Warning = new DocumentWarning();
PdfDocument pdfDocument = converter.ConvertToPDF(document);
//If the IsCanceled boolean is enabled, the input document will contain an unsupported element.
if (converter.IsCanceled)
{
    Console.WriteLine("The execution stopped due to unsupported element.");
    Console.ReadKey();
}
else
{
    //Saves the PDF file.
    FileStream outputFile = new FileStream("Output.pdf", FileMode.OpenOrCreate, FileAccess.ReadWrite);
    pdfDocument.Save(outputFile);
    outputFile.Dispose();
    Console.WriteLine("Success");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Dim wordDocument As New WordDocument("Input.docx")
Dim converter As New DocToPDFConverter()
converter.Settings.Warning = New DocumentWarning()
Dim pdfDocument As PdfDocument = converter.ConvertToPDF(document)

' If the IsCanceled boolean is enabled, the input document will contain an unsupported element.
If converter.IsCanceled Then
    Console.WriteLine("The execution stopped due to unsupported element.")
    Console.ReadKey()
Else
    ' Saves the PDF file.
    Using outputFile As New FileStream("Output.pdf", FileMode.OpenOrCreate, FileAccess.ReadWrite)
        pdfDocument.Save(outputFile)
        Console.WriteLine("Success")
    End Using
End If
{% endhighlight %}

{% endtabs %}

The following code demonstrates how to initialize the [Warning](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocToPDFConverter.DocToPDFConverterSettings.html#Syncfusion_DocToPDFConverter_DocToPDFConverterSettings_Warning) API and display warning messages for all unsupported elements in the input document. Additionally, this code shows how to set a flag to stop Word to PDF conversion if an unsupported element is identified.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
public class DocumentWarning : IWarning
{
    public bool ShowWarnings(List<WarningInfo> warningInfo)
    {
        bool isContinueConversion = true;
        foreach (WarningInfo warning in warningInfo)
        {
            //Based on the WarningType enumeration, you can do your manipulation.
            //Skip the Word to PDF conversion by setting the isContinueConversion value to false.
            //To stop execution if the input document has a SmartArt.
            if (warning.WarningType == WarningType.SmartArt)
                isContinueConversion = false;

            //Warning messages for unsupported elements in the input document.
            Console.WriteLine("The input document contains " + warning.WarningType + " unsupported element.");
        }
        return isContinueConversion;
    }
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
public class DocumentWarning : IWarning
{
    public bool ShowWarnings(List<WarningInfo> warningInfo)
    {
        bool isContinueConversion = true;
        foreach (WarningInfo warning in warningInfo)
        {
            //Based on the WarningType enumeration, you can do your manipulation.
            //Skip the Word to PDF conversion by setting the isContinueConversion value to false.
            //To stop execution if the input document has a SmartArt.
            if (warning.WarningType == WarningType.SmartArt)
                isContinueConversion = false;

            //Warning messages for unsupported elements in the input document.
            Console.WriteLine("The input document contains " + warning.WarningType + " unsupported element.");
        }
        return isContinueConversion;
    }
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Public Class DocumentWarning
    Implements IWarning

    Public Function ShowWarnings(warningInfo As List(Of WarningInfo)) As Boolean Implements IWarning.ShowWarnings
        Dim isContinueConversion As Boolean = True

        For Each warning As WarningInfo In warningInfo
            ' Based on the WarningType enumeration, you can perform your manipulation.
            ' Skip the Word to PDF conversion by setting the isContinueConversion value to false.
            ' To stop execution if the input document has a SmartArt.
            If warning.WarningType = WarningType.SmartArt Then
                isContinueConversion = False
            End If

            ' Warning messages for unsupported elements in the input document.
            Console.WriteLine("The input document contains " & warning.WarningType & " unsupported element.")
        Next

        Return isContinueConversion
    End Function
End Class
{% endhighlight %}

{% endtabs %}

T> Using the above Warning API, handle logic to identify the documents with unsupported elements and notify the end users to use supported elements for good preservation in the output PDF.

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Show-Warning-for-unsupported-elements)

## Unsupported elements in Word to PDF conversion

The following table shows the unsupported elements of Word to PDF conversion.

<table>
<thead> 
<tr>
<th>Element</th>
<th>Unsupported elements</th>
</tr>
</thead>
<tr>
<td>
Predefined shapes
</td>
<td>
Only DOCX and WordML format documents are supported.
</td>
</tr>
<tr>
<td>
Chart
</td>
<td>
Only DOCX and WordML format documents are supported from .NET Framework 4.0 onwards.
</td>
</tr>
<tr>
<td>
Table Styles
</td>
<td>
Only DOCX and WordML format documents are supported.
</td>
</tr>
<tr>
<td>
Pagination
</td>
<td>
The Essential DocIO makes sensible decision when layout the text, and its supported elements while generating the PDF documents. But however, there may not be guaranteed pagination with all the documents.
</td>
</tr>
<tr>
<td>
Grouped Shapes
</td>
<td>
Only DOCX and WordML format documents are supported.
</td>
</tr>
<tr>
<td>
Custom Shapes 
</td>
<td>
Only DrawingML custom shapes in DOCX and WordML format documents are supported.
</td>
</tr>
<tr>
<td>
Fit Text – Table cell
</td>
<td>
Not supported
</td>
</tr>
<tr>
<td>
Vertical Alignment of the section
</td>
<td>
Not supported
</td>
</tr>
<tr>
<td>
Equation
</td>
<td>
Mathematical equations extending to multiple lines will be rendered in a single line and content exceeding the right margin will clip in the PDF.
</td>
</tr>
<tr>
<td>
SmartArt
</td>
<td>
Not supported
</td>
</tr>
<tr>
<td>
WordArt
</td>
<td>
Not supported
</td>
</tr>
<tr>
<td>
Watermark
</td>
<td>
First watermark of the Word document should be applied to the entire converted PDF document when the Word document have multiple watermarks.
</td>
</tr>
<tr>
<td>
Multi-Column Texts
</td>
<td>
Multi-Column text positions are calculated dynamically when layout the text. So, there may be some content position differences occur in the PDF document.
</td>
</tr>
<tr>
<td>
Borders
</td>
<td>
Using of patterns and 3D borders are not retained in the output PDF document.
</td>
</tr>
<tr>
<td>
Break – Page break, column break and Line break
</td>
<td>
Text wrapping break is not supported.
</td>
</tr>
<tr>
<td>
Footnote and endnote
</td>
<td>
Number formats in Roman, Alphabets, and Arabic only supported.
</td>
</tr>
<tr>
<td>
Textbox
</td>
<td>
Linked text boxes are not supported.
</td>
</tr>
<tr>
<td>
Font kerning
</td>
<td>
Partially supported. At present, the text in a line is scaled uniformly to match the width of kerned text, instead of adjusting the space between each pair of characters.
</td>
</tr>
<tr>
<td>
Images
</td>
<td>
In .NET Core and latest target, we have limitation in metafile. Refer {{'[here](https://help.syncfusion.com/file-formats/docio/faq#why-images-are-preserved-as-redx-images-in-word-to-pdf-conversion)'| markdownify }}
</td>
</tr>
</table>

## See Also

* [How to perform font substitution in Word to PDF conversion](https://support.syncfusion.com/kb/article/7499/how-to-perform-font-substitution-in-word-to-pdf-conversion)
* [What happens when the Word document used fonts for a text is not installed in production machine during Word to PDF or Image conversion](https://support.syncfusion.com/kb/article/6821/what-happens-when-the-word-document-used-fonts-for-a-text-is-not-installed-in-production)
* [How to resolve font problems during Word to PDF or image conversion?](https://support.syncfusion.com/kb/article/13969/how-to-resolve-font-problems-during-word-to-pdf-or-image-conversion)
* [How to convert multiple Word documents to multiple PDFs and zip the PDFs in C#?](https://support.syncfusion.com/kb/article/13837/how-to-convert-multiple-word-documents-to-multiple-pdfs-and-zip-the-pdfs-in-c)
* [How to convert and replace EMF image in word document to PNG with same size](https://support.syncfusion.com/kb/article/11331/how-to-convert-and-replace-emf-image-in-word-document-to-png-with-same-size)
* [How to convert Word document to PDF in UWP](https://support.syncfusion.com/kb/article/8902/how-to-convert-word-document-to-pdf-in-uwp)
* [How to avoid conflicts while using DocIORenderer and other controls in UWP](https://support.syncfusion.com/kb/article/11445/how-to-avoid-conflicts-while-using-dociorenderer-and-other-controls-in-uwp)
* [How to deploy .NET Core application with Word to PDF conversion capabilities in Linux OS](https://www.syncfusion.com/kb/8470/how-to-deploy-net-core-application-with-word-to-pdf-conversion-capabilities-in-linux-os)
* [How to convert Word document to PDF in Azure App service on Linux](https://support.syncfusion.com/kb/article/7626/how-to-deploy-net-core-application-with-word-to-pdf-conversion-capabilities-in-linux-os)
* [Is it possible to perform Word to PDF conversion in Azure Environment ?](https://www.syncfusion.com/kb/7751/is-it-possible-to-perform-word-to-pdf-conversion-in-azure-environment)
* [How to perform Word to PDF conversion in Azure Functions v1](https://www.syncfusion.com/kb/10056/how-to-perform-word-to-pdf-conversion-in-azure-functions-v1)
* [How to mail merge Word documents and convert to PDF in Azure Functions v2](https://support.syncfusion.com/kb/article/6939/is-it-possible-to-perform-word-to-pdf-conversion-in-azure-environment)
* [How to convert Word document to PDF in AWS Lambda](https://support.syncfusion.com/kb/article/10534/how-to-convert-word-document-to-pdf-in-aws-lambda)
* [How to add signature field in the PDF converted from Word](https://support.syncfusion.com/kb/article/11438/how-to-add-signature-field-in-the-pdf-converted-from-word)
* [How to convert Word to PDF in Blazor WebAssembly (WASM)?](https://support.syncfusion.com/kb/article/12239/how-to-convert-word-to-pdf-in-blazor-webassembly-wasm)
* [How to perform Word to PDF conversion in WinForms ?](https://support.syncfusion.com/kb/article/8848/how-to-perform-word-to-pdf-conversion-in-winforms-?isInternalRefresh=False)
