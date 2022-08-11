---
title: Word document to PDF Conversion | DocIO | Syncfusion
description: This section illustrates how to convert Word document to PDF using Syncfusion Word library (Essential DocIO)
platform: file-formats
control: DocIO
documentation: UG
---

# Word document to PDF Conversion

## Converting Word to PDF

The Word document files are converted as a PDF document with a few lines of code by using the Essential DocIO. It works perfectly when you create an input Word document from scratch or load an existing Word document and easily converted into PDF. 

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

**For ASP.NET Core and Xamarin applications**
* using Syncfusion.DocIO
* using Syncfusion.DocIO.DLS
* using Syncfusion.DocIORenderer
* using Syncfusion.Pdf

The following code example illustrates how to convert a Word document into PDF document.

{% tabs %}
{% highlight c# tabtitle="C#" %}
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

{% highlight vb.net tabtitle="VB.NET" %}
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

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument((assembly.GetManifestResourceStream("Sample.Assets.Template.docx")),
              FormatType.Docx))
{
    //Creates an instance of DocIORenderer - responsible for Word to PDF conversion
    DocIORenderer docIORenderer = new DocIORenderer();
    //Converts Word document into PDF document
    PdfDocument pdfDocument = docIORenderer.ConvertToPDF(document);
    //Save the document into stream.
    MemoryStream stream = new MemoryStream();
    pdfDocument.Save(stream);
    //Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.
    Save(stream, "WordToPDF.pdf");
    //Closes the Word and PDF document
    docIORenderer.Dispose();
    document.Close();
    pdfDocument.Close();
}

//Saves the PDF document
async void Save(MemoryStream streams, string filename)
{
    streams.Position = 0;
    StorageFile stFile;
    if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
    {
        FileSavePicker savePicker = new FileSavePicker();
        savePicker.DefaultFileExtension = ".pdf";
        savePicker.SuggestedFileName = filename;
        savePicker.FileTypeChoices.Add("Word Documents", new List<string>() { ".pdf" });
        stFile = await savePicker.PickSaveFileAsync();
    }
    else
    {
        StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
        stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
    }
    if (stFile != null)
    {
        using (IRandomAccessStream zipStream = await stFile.OpenAsync(FileAccessMode.ReadWrite))
        {
            //Write compressed data from memory to file
            using (Stream outstream = zipStream.AsStreamForWrite())
            {
                byte[] buffer = streams.ToArray();
                outstream.Write(buffer, 0, buffer.Length);
                outstream.Flush();
            }
        }
    }
    //Launch the saved Word file
    await Windows.System.Launcher.LaunchFileAsync(stFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
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

{% highlight c# tabtitle="Xamarin" %}
//Load the Word document as stream
Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Template.docx");
// Loads the stream into Word Document.
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
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Convert-Word-document-to-PDF).

N> 1. Word to PDF conversion is not supported in Silverlight, Windows Phone, WinRT, and Universal applications.
N> 2. Word to PDF conversion is supported in Blazor server-side application alone and is not supported in Blazor client-side application.
N> 3. For .NET Framework, creating an instance of the ChartToImageConverter class is mandatory to convert the charts present in the Word to PDF. Otherwise, the charts are not preserved in the converted PDF. Whereas this is not necessary for .NET Core, as ChartToImageConverter is initialized internally in Syncfusion.DocIORenderer.Portable assembly.
N> 4. The ChartToImageConverter is supported from .NET Framework 4.0 onwards and .NET Core 2.0 onwards.
N> 5. Total number of pages in the converted PDF may vary based on unsupported elements in the input Word document.
N> 6. "DocIO supports Word to PDF conversion in UWP application using DocIORenderer." For further information, please refer [here](https://www.syncfusion.com/kb/10270/how-to-convert-word-document-to-pdf-in-uwp)

## Word to PDF conversion in Linux OS

In Linux OS, you can perform the Word to PDF conversion using .NET Core (Targeting .netcoreapp) application. You can refer [Word to PDF conversion NuGet packages](https://help.syncfusion.com/file-formats/docio/nuget-packages-required#converting-word-document-to-pdf) to know about the packages required to deploy .NET Core (Targeting .netcoreapp) application with Word to PDF conversion capabilities.

From v20.1, in addition to the previous NuGet packages, we recommend to use [SkiaSharp.NativeAssets.Linux v2.88.0-preview.209](https://www.nuget.org/packages/SkiaSharp.NativeAssets.Linux/2.88.0-preview.209) and [HarfBuzzSharp.NativeAssets.Linux v2.8.2-preview.209](https://www.nuget.org/packages/HarfBuzzSharp.NativeAssets.Linux/2.8.2-preview.209) NuGets to perform Word to PDF conversion in Linux environment.

If you are using prior to v20.1 release, please refer [here](https://help.syncfusion.com/file-formats/docio/faq#what-are-the-nuget-packages-to-be-installed-to-perform-word-to-pdf-conversion-in-linux-os) to know about how to perform Word to PDF conversion in Linux.


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
{% highlight c# tabtitle="C#" %}
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

{% highlight vb.net tabtitle="VB.NET" %}
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

{% highlight c# tabtitle="UWP" %}
//DocIO supports Word to PDF fast rendering in Windows forms, WPF, ASP.NET and ASP.NET MVC platform alone
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//DocIO supports Word to PDF fast rendering in Windows forms, WPF, ASP.NET and ASP.NET MVC platform alone
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//DocIO supports Word to PDF fast rendering in Windows forms, WPF, ASP.NET and ASP.NET MVC platform alone
{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Enable-fast-rendering).

### Embedding fonts

You can customize the TrueType fonts embedding in two ways as follows:

#### Embed Subset Fonts

This setting allows you to **embed the particular font information** (glyphs) from the TrueType fonts used for the rendered characters in converted PDF document.

The following code sample shows how to embed the TrueType fonts into the converted PDF document.

{% tabs %}
{% highlight c# tabtitle="C#" %}
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

{% highlight vb.net tabtitle="VB.NET" %}
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

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument((assembly.GetManifestResourceStream("Sample.Assets.Template.docx")),
              FormatType.Docx))
{
    //Creates an instance of DocIORenderer - responsible for Word to PDF conversion
    DocIORenderer docIORenderer = new DocIORenderer();
    //Sets true to embed TrueType fonts
    docIORenderer.Settings.EmbedFonts = true;
    //Converts Word document into PDF document
    PdfDocument pdfDocument = docIORenderer.ConvertToPDF(document);
    //Save the document into stream.
    MemoryStream stream = new MemoryStream();
    pdfDocument.Save(stream);
    //Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.
    Save(stream, "WordToPDF.pdf");
    //Closes the Word and PDF document
    document.Close();
    pdfDocument.Close();
}

//Saves the PDF document
async void Save(MemoryStream streams, string filename)
{
    streams.Position = 0;
    StorageFile stFile;
    if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
    {
        FileSavePicker savePicker = new FileSavePicker();
        savePicker.DefaultFileExtension = ".pdf";
        savePicker.SuggestedFileName = filename;
        savePicker.FileTypeChoices.Add("Word Documents", new List<string>() { ".pdf" });
        stFile = await savePicker.PickSaveFileAsync();
    }
    else
    {
        StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
        stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
    }
    if (stFile != null)
    {
        using (IRandomAccessStream zipStream = await stFile.OpenAsync(FileAccessMode.ReadWrite))
        {
            //Write compressed data from memory to file
            using (Stream outstream = zipStream.AsStreamForWrite())
            {
                byte[] buffer = streams.ToArray();
                outstream.Write(buffer, 0, buffer.Length);
                outstream.Flush();
            }
        }
    }
    //Launch the saved Word file
    await Windows.System.Launcher.LaunchFileAsync(stFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
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

{% highlight c# tabtitle="Xamarin" %}
//Load the Word document as stream
Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Template.docx");
// Loads the stream into Word Document.
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

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Embed-subset-fonts).

#### Embed Complete Fonts

This setting allows you to embed the complete font information (glyphs) from the TrueType fonts used in converted PDF document.

The following code sample shows how to embed the complete TrueType fonts into the converted PDF document.

{% tabs %}
{% highlight c# tabtitle="C#" %}
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

{% highlight vb.net tabtitle="VB.NET" %}
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

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument((assembly.GetManifestResourceStream("Sample.Assets.Template.docx")),
              FormatType.Docx))
{
    //Creates an instance of DocIORenderer - responsible for Word to PDF conversion
    DocIORenderer docIORenderer = new DocIORenderer();
    // Sets true to embed complete TrueType fonts
    docIORenderer.Settings.EmbedCompleteFonts = true;
    //Converts Word document into PDF document
    PdfDocument pdfDocument = docIORenderer.ConvertToPDF(document);
    //Save the document into stream.
    MemoryStream stream = new MemoryStream();
    pdfDocument.Save(stream);
    //Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.
    Save(stream, "WordToPDF.pdf");
    //Closes the Word and PDF document
    document.Close();
    pdfDocument.Close();
}

//Saves the PDF document
async void Save(MemoryStream streams, string filename)
{
    streams.Position = 0;
    StorageFile stFile;
    if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
    {
        FileSavePicker savePicker = new FileSavePicker();
        savePicker.DefaultFileExtension = ".pdf";
        savePicker.SuggestedFileName = filename;
        savePicker.FileTypeChoices.Add("Word Documents", new List<string>() { ".pdf" });
        stFile = await savePicker.PickSaveFileAsync();
    }
    else
    {
        StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
        stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
    }
    if (stFile != null)
    {
        using (IRandomAccessStream zipStream = await stFile.OpenAsync(FileAccessMode.ReadWrite))
        {
            //Write compressed data from memory to file
            using (Stream outstream = zipStream.AsStreamForWrite())
            {
                byte[] buffer = streams.ToArray();
                outstream.Write(buffer, 0, buffer.Length);
                outstream.Flush();
            }
        }
    }
    //Launch the saved Word file
    await Windows.System.Launcher.LaunchFileAsync(stFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
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

{% highlight c# tabtitle="Xamarin" %}
//Load the Word document as stream
Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Template.docx");
//Loads the stream into Word Document.
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

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Embed-complete-fonts).

### Accessible PDF document

This setting allows you to determine whether to preserve document structured tags in the converted **PDF document for accessibility (508 compliance) support**. This property will set the title and description for images, diagrams and other objects in the generated PDF document. This information will be useful for **people with vision or cognitive impairments** who may not able to see or understand the object

The following code sample shows how to preserve document structured tags in the converted PDF document.

{% tabs %}
{% highlight c# tabtitle="C#" %}
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

{% highlight vb.net tabtitle="VB.NET" %}
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

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument((assembly.GetManifestResourceStream("Sample.Assets.Template.docx")),
              FormatType.Docx))
{
    //Creates an instance of DocIORenderer - responsible for Word to PDF conversion
    DocIORenderer docIORenderer = new DocIORenderer();
    //Sets true to preserve document structured tags in the converted PDF document 
    docIORenderer.Settings.AutoTag = true;
    //Converts Word document into PDF document
    PdfDocument pdfDocument = docIORenderer.ConvertToPDF(document);
    //Save the document into stream.
    MemoryStream stream = new MemoryStream();
    pdfDocument.Save(stream);
    //Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.
    Save(stream, "WordToPDF.pdf");
    //Closes the Word and PDF document
    document.Close();
    pdfDocument.Close();
}

//Saves the PDF document
async void Save(MemoryStream streams, string filename)
{
    streams.Position = 0;
    StorageFile stFile;
    if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
    {
        FileSavePicker savePicker = new FileSavePicker();
        savePicker.DefaultFileExtension = ".pdf";
        savePicker.SuggestedFileName = filename;
        savePicker.FileTypeChoices.Add("Word Documents", new List<string>() { ".pdf" });
        stFile = await savePicker.PickSaveFileAsync();
    }
    else
    {
        StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
        stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
    }
    if (stFile != null)
    {
        using (IRandomAccessStream zipStream = await stFile.OpenAsync(FileAccessMode.ReadWrite))
        {
            //Write compressed data from memory to file
            using (Stream outstream = zipStream.AsStreamForWrite())
            {
                byte[] buffer = streams.ToArray();
                outstream.Write(buffer, 0, buffer.Length);
                outstream.Flush();
            }
        }
    }
    //Launch the saved Word file
    await Windows.System.Launcher.LaunchFileAsync(stFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
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

{% highlight c# tabtitle="Xamarin" %}
//Load the Word document as stream
Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Template.docx");
// Loads the stream into Word Document.
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

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Convert-Word-into-accessible-PDF).

### Word document headings to PDF bookmarks

This setting allows you to determine whether to **preserve Word document headings** (i.e., paragraph with heading style and outline level) as bookmarks in the converted PDF document. As per Microsoft Word behavior, either Word document headings or bookmarks can be exported as PDF bookmarks. By default, DocIO preserves Word documents bookmarks as PDF bookmarks in converted PDF document.

The following code sample shows how to preserve Word document headings as bookmarks in the converted PDF document.

{% tabs %}
{% highlight c# tabtitle="C#" %}
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

{% highlight vb.net tabtitle="VB.NET" %}
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

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument((assembly.GetManifestResourceStream("Sample.Assets.Template.docx")),
              FormatType.Docx))
{
    //Creates an instance of DocIORenderer - responsible for Word to PDF conversion
    DocIORenderer docIORenderer = new DocIORenderer();
    //Sets ExportBookmarks for preserving Word document headings as PDF bookmarks
    docIORenderer.Settings.ExportBookmarks = Syncfusion.DocIO.ExportBookmarkType.Headings;
    //Converts Word document into PDF document
    PdfDocument pdfDocument = docIORenderer.ConvertToPDF(document);
    //Save the document into stream.
    MemoryStream stream = new MemoryStream();
    pdfDocument.Save(stream);
    //Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.
    Save(stream, "WordToPDF.pdf");
    //Closes the Word and PDF document
    document.Close();
    pdfDocument.Close();
}

//Saves the PDF document
async void Save(MemoryStream streams, string filename)
{
    streams.Position = 0;
    StorageFile stFile;
    if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
    {
        FileSavePicker savePicker = new FileSavePicker();
        savePicker.DefaultFileExtension = ".pdf";
        savePicker.SuggestedFileName = filename;
        savePicker.FileTypeChoices.Add("Word Documents", new List<string>() { ".pdf" });
        stFile = await savePicker.PickSaveFileAsync();
    }
    else
    {
        StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
        stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
    }
    if (stFile != null)
    {
        using (IRandomAccessStream zipStream = await stFile.OpenAsync(FileAccessMode.ReadWrite))
        {
            //Write compressed data from memory to file
            using (Stream outstream = zipStream.AsStreamForWrite())
            {
                byte[] buffer = streams.ToArray();
                outstream.Write(buffer, 0, buffer.Length);
                outstream.Flush();
            }
        }
    }
    //Launch the saved Word file
    await Windows.System.Launcher.LaunchFileAsync(stFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
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

{% highlight c# tabtitle="Xamarin" %}
//Load the Word document as stream
Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Template.docx");
// Loads the stream into Word Document.
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

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Export-Word-headings-into-PDF).

The following code sample shows how to preserve both Word document headings and Bookmarks as PDF bookmarks in the converted PDF document.

{% tabs %}
{% highlight c# tabtitle="C#" %}
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

{% highlight vb.net tabtitle="VB.NET" %}
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

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument((assembly.GetManifestResourceStream("Sample.Assets.Template.docx")),
              FormatType.Docx))
{
    //Creates an instance of DocIORenderer - responsible for Word to PDF conversion
    DocIORenderer docIORenderer = new DocIORenderer();
    //Sets ExportBookmarks for preserving Word document headings as PDF bookmarks
    docIORenderer.Settings.ExportBookmarks = Syncfusion.DocIO.ExportBookmarkType.Headings | Syncfusion.DocIO.ExportBookmarkType.Bookmarks;
    //Converts Word document into PDF document
    PdfDocument pdfDocument = docIORenderer.ConvertToPDF(document);
    //Save the document into stream.
    MemoryStream stream = new MemoryStream();
    pdfDocument.Save(stream);
    //Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.
    Save(stream, "WordToPDF.pdf");
    //Closes the Word and PDF document
    document.Close();
    pdfDocument.Close();
}

//Saves the PDF document
async void Save(MemoryStream streams, string filename)
{
    streams.Position = 0;
    StorageFile stFile;
    if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
    {
        FileSavePicker savePicker = new FileSavePicker();
        savePicker.DefaultFileExtension = ".pdf";
        savePicker.SuggestedFileName = filename;
        savePicker.FileTypeChoices.Add("Word Documents", new List<string>() { ".pdf" });
        stFile = await savePicker.PickSaveFileAsync();
    }
    else
    {
        StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
        stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
    }
    if (stFile != null)
    {
        using (IRandomAccessStream zipStream = await stFile.OpenAsync(FileAccessMode.ReadWrite))
        {
            //Write compressed data from memory to file
            using (Stream outstream = zipStream.AsStreamForWrite())
            {
                byte[] buffer = streams.ToArray();
                outstream.Write(buffer, 0, buffer.Length);
                outstream.Flush();
            }
        }
    }
    //Launch the saved Word file
    await Windows.System.Launcher.LaunchFileAsync(stFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
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

{% highlight c# tabtitle="Xamarin" %}
//Load the Word document as stream
Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Template.docx");
// Loads the stream into Word Document.
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

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Export-Word-bookmarks-into-PDF).

### Word document form field to PDF form field.

This setting allows you to determine whether to **preserve Word document form fields** (Text form field, Checkbox form field and Drop-down form field) as PDF form fields in the converted PDF document. This features helps in **creating fillable PDF forms from Word document**.

The following code sample shows how to preserve Word document form field as PDF form field in the converted PDF document.

{% tabs %}
{% highlight c# tabtitle="C#" %}
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

{% highlight vb.net tabtitle="VB.NET" %}
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

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument((assembly.GetManifestResourceStream("Sample.Assets.Template.docx")),
              FormatType.Docx))
{
    //Creates an instance of DocIORenderer - responsible for Word to PDF conversion
    DocIORenderer docIORenderer = new DocIORenderer();
    //Sets true to preserve the Word document form field as editable PDF form field in PDF document
    docIORenderer.Settings.PreserveFormFields = true;
    //Converts Word document into PDF document
    PdfDocument pdfDocument = docIORenderer.ConvertToPDF(document);
    //Save the document into stream.
    MemoryStream stream = new MemoryStream();
    pdfDocument.Save(stream);
    //Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.
    Save(stream, "WordToPDF.pdf");
    //Closes the Word and PDF document
    document.Close();
    pdfDocument.Close();
}

//Saves the PDF document
async void Save(MemoryStream streams, string filename)
{
    streams.Position = 0;
    StorageFile stFile;
    if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
    {
        FileSavePicker savePicker = new FileSavePicker();
        savePicker.DefaultFileExtension = ".pdf";
        savePicker.SuggestedFileName = filename;
        savePicker.FileTypeChoices.Add("Word Documents", new List<string>() { ".pdf" });
        stFile = await savePicker.PickSaveFileAsync();
    }
    else
    {
        StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
        stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
    }
    if (stFile != null)
    {
        using (IRandomAccessStream zipStream = await stFile.OpenAsync(FileAccessMode.ReadWrite))
        {
            //Write compressed data from memory to file
            using (Stream outstream = zipStream.AsStreamForWrite())
            {
                byte[] buffer = streams.ToArray();
                outstream.Write(buffer, 0, buffer.Length);
                outstream.Flush();
            }
        }
    }
    //Launch the saved Word file
    await Windows.System.Launcher.LaunchFileAsync(stFile);
}

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
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

{% highlight c# tabtitle="Xamarin" %}
//Load the Word document as stream
Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Template.docx");
// Loads the stream into Word Document.
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

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Create-fillable-PDF-from-Word).

### Image quality 

This setting allows you to determine the **quality of the charts and JPEG images** in the converted PDF document.

The following code sample shows how to customize the image quality of charts and JPEG images in the converted PDF document.

{% tabs %}
{% highlight c# tabtitle="C#" %}
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

{% highlight vb.net tabtitle="VB.NET" %}
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

{% highlight c# tabtitle="UWP" %}
//DocIO supports Word to PDF Image in Windows forms, WPF, ASP.NET and ASP.NET MVC platform alone
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//DocIO supports Word to PDF Image in Windows forms, WPF, ASP.NET and ASP.NET MVC platform alone
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//DocIO supports Word to PDF Image in Windows forms, WPF, ASP.NET and ASP.NET MVC platform alone
{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Adjust-image-quality).

### Recreate Nested Metafile

This setting allows you to regenerate the nested EMF images present in the Word document during PDF conversion.
This property is recommended to resolve the scaling problem of nested metafile images by regenerating the nested metafile images present in the Word document.

The following code sample shows how to use this property to regenerate the nested EMF images present in the Word document during PDF conversion.

{% tabs %}  

{% highlight c# tabtitle="C#" %}
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

{% highlight vb.net tabtitle="VB.NET" %}
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

{% highlight c# tabtitle="UWP" %}
//DocIO supports to Recreate Nested Metafile in Windows forms, WPF, ASP.NET and ASP.NET MVC platform alone.
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//DocIO supports to Recreate Nested Metafile in Windows forms, WPF, ASP.NET and ASP.NET MVC platform alone, and it's also supported in .NET Core 3.0, but it requires DocToPDFConverter assembly instead of DocIORenderer.
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//DocIO supports to Recreate Nested Metafile in Windows forms, WPF, ASP.NET and ASP.NET MVC platform alone.
{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Recreate-nested-metafile).

### Identical image optimization 

This setting **reduces the Main Memory usage** in Word to PDF conversion by reusing the identical images.

The following code sample shows how to reduce the Main Memory usage while converting Word to PDF by reusing the identical images.

{% tabs %}
{% highlight c# tabtitle="C#" %}
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

{% highlight vb.net tabtitle="VB.NET" %}
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

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument((assembly.GetManifestResourceStream("Sample.Assets.Template.docx")),
              FormatType.Docx))
{
    //Creates an instance of DocIORenderer - responsible for Word to PDF conversion
    DocIORenderer render = new DocIORenderer();
    //Sets true to optimize the memory usage for identical images
    render.Settings.OptimizeIdenticalImages = true;
    //Converts Word document into PDF document
    PdfDocument pdfDocument = render.ConvertToPDF(document);
    //Save the document into stream.
    MemoryStream stream = new MemoryStream();
    pdfDocument.Save(stream);
    //Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.
    Save(stream, "WordToPDF.pdf");
    //Closes the Word and PDF document
    document.Close();
    pdfDocument.Close();
}

//Saves the PDF document
async void Save(MemoryStream streams, string filename)
{
    streams.Position = 0;
    StorageFile stFile;
    if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
    {
        FileSavePicker savePicker = new FileSavePicker();
        savePicker.DefaultFileExtension = ".pdf";
        savePicker.SuggestedFileName = filename;
        savePicker.FileTypeChoices.Add("Word Documents", new List<string>() { ".pdf" });
        stFile = await savePicker.PickSaveFileAsync();
    }
    else
    {
        StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
        stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
    }
    if (stFile != null)
    {
        using (IRandomAccessStream zipStream = await stFile.OpenAsync(FileAccessMode.ReadWrite))
        {
            //Write compressed data from memory to file
            using (Stream outstream = zipStream.AsStreamForWrite())
            {
                byte[] buffer = streams.ToArray();
                outstream.Write(buffer, 0, buffer.Length);
                outstream.Flush();
            }
        }
    }
    //Launch the saved Word file
    await Windows.System.Launcher.LaunchFileAsync(stFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
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

{% highlight c# tabtitle="Xamarin" %}
//Load the Word document as stream
Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Template.docx");
//Loads the stream into Word Document.
WordDocument wordDocument = new WordDocument(docStream, Syncfusion.DocIO.FormatType.Automatic);
//Instantiation of DocIORenderer for Word to PDF conversion
DocIORenderer render = new DocIORenderer();
//Sets true to optimize the memory usage for identical images
render.Settings.OptimizeIdenticalImages = true;
//Converts Word document into PDF document
PdfDocument pdfDocument = render.ConvertToPDF(wordDocument);
//Releases all resources used by the Word document and DocIO Renderer objects
render.Dispose();
docStream.Dispose();
wordDocument.Dispose();
//Saves the PDF file
MemoryStream outputStream = new MemoryStream();
pdfDocument.Save(outputStream);
//Closes the instance of PDF document object
pdfDocument.Close();
outputStream.Dispose();
{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Optimize-identical-images).

### PDF Conformance Level

This setting allows you to set the PDF conformance level.

The following code sample shows how to set the PdfConformanceLevel while converting Word to PDF.

{% tabs %}
{% highlight c# tabtitle="C#" %}
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

{% highlight vb.net tabtitle="VB.NET" %}
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

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument((assembly.GetManifestResourceStream("Sample.Assets.Template.docx")),
              FormatType.Docx))
{
    //Creates an instance of DocIORenderer - responsible for Word to PDF conversion
    DocIORenderer docIORenderer = new DocIORenderer();
    // Set the conformance for PDF/A-1b conversion.
    docIORenderer.Settings.PdfConformanceLevel = PdfConformanceLevel.Pdf_A1B;
    //Converts Word document into PDF document
    PdfDocument pdfDocument = docIORenderer.ConvertToPDF(document);
    //Save the document into stream.
    MemoryStream stream = new MemoryStream();
    pdfDocument.Save(stream);
    //Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.
    Save(stream, "WordToPDF.pdf");
    //Closes the Word and PDF document
    document.Close();
    pdfDocument.Close();
}

//Saves the PDF document
async void Save(MemoryStream streams, string filename)
{
    streams.Position = 0;
    StorageFile stFile;
    if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
    {
        FileSavePicker savePicker = new FileSavePicker();
        savePicker.DefaultFileExtension = ".pdf";
        savePicker.SuggestedFileName = filename;
        savePicker.FileTypeChoices.Add("Word Documents", new List<string>() { ".pdf" });
        stFile = await savePicker.PickSaveFileAsync();
    }
    else
    {
        StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
        stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
    }
    if (stFile != null)
    {
        using (IRandomAccessStream zipStream = await stFile.OpenAsync(FileAccessMode.ReadWrite))
        {
            //Write compressed data from memory to file
            using (Stream outstream = zipStream.AsStreamForWrite())
            {
                byte[] buffer = streams.ToArray();
                outstream.Write(buffer, 0, buffer.Length);
                outstream.Flush();
            }
        }
    }
    //Launch the saved Word file
    await Windows.System.Launcher.LaunchFileAsync(stFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
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

{% highlight c# tabtitle="Xamarin" %}
//Load the Word document as stream
Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Template.docx");
// Loads the stream into Word Document.
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

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/PDF-conformance-level).

### Enable Alternate Chunks

In the Word document, another Word documents are embedded in it and referred as AltChunks. This setting allows you to include the alternate chunks while converting Word to PDF conversion. As default, it includes alternate chunks.

The following code sample shows how to exclude the alternate chunk parts in Word to PDF conversion.

{% tabs %}
{% highlight c# tabtitle="C#" %}
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

{% highlight vb.net tabtitle="VB.NET" %}
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

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument((assembly.GetManifestResourceStream("Sample.Assets.Template.docx")),
              FormatType.Docx))
{
    //Creates an instance of DocIORenderer - responsible for Word to PDF conversion
    DocIORenderer docIORenderer = new DocIORenderer();
    //Sets false to disable converting the alternate chunks present in Word document to PDF.
    docIORenderer.Settings.EnableAlternateChunks = false;
    //Converts Word document into PDF document
    PdfDocument pdfDocument = docIORenderer.ConvertToPDF(document);
    //Save the document into stream.
    MemoryStream stream = new MemoryStream();
    pdfDocument.Save(stream);
    //Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.
    Save(stream, "WordToPDF.pdf");
    //Closes the Word and PDF document
    document.Close();
    pdfDocument.Close();
}

//Saves the PDF document
async void Save(MemoryStream streams, string filename)
{
    streams.Position = 0;
    StorageFile stFile;
    if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
    {
        FileSavePicker savePicker = new FileSavePicker();
        savePicker.DefaultFileExtension = ".pdf";
        savePicker.SuggestedFileName = filename;
        savePicker.FileTypeChoices.Add("Word Documents", new List<string>() { ".pdf" });
        stFile = await savePicker.PickSaveFileAsync();
    }
    else
    {
        StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
        stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
    }
    if (stFile != null)
    {
        using (IRandomAccessStream zipStream = await stFile.OpenAsync(FileAccessMode.ReadWrite))
        {
            //Write compressed data from memory to file
            using (Stream outstream = zipStream.AsStreamForWrite())
            {
                byte[] buffer = streams.ToArray();
                outstream.Write(buffer, 0, buffer.Length);
                outstream.Flush();
            }
        }
    }
    //Launch the saved Word file
    await Windows.System.Launcher.LaunchFileAsync(stFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
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

{% highlight c# tabtitle="Xamarin" %}
//Load the Word document as stream
Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Template.docx");
//Loads the stream into Word Document.
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
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Disable-alternate-chunks).

### Complex Script Text

This setting allows you to **preserve the complex script text** in the converted PDF document.

The following code sample shows how to preserve the complex script text in the converted PDF document.

{% tabs %}  

{% highlight c# tabtitle="C#" %}
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

{% highlight vb.net tabtitle="VB.NET" %}
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

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument((assembly.GetManifestResourceStream("Sample.Assets.Template.docx")),
              FormatType.Docx))
{
    //Creates an instance of DocIORenderer - responsible for Word to PDF conversion
    DocIORenderer docIORenderer = new DocIORenderer();
    //Sets AutoDetectComplexScript property to true to detect the complex scripts automatically
	docIORenderer.Settings.AutoDetectComplexScript = true;
    //Converts Word document into PDF document
    PdfDocument pdfDocument = docIORenderer.ConvertToPDF(document);
    //Save the document into stream.
    MemoryStream stream = new MemoryStream();
    pdfDocument.Save(stream);
    //Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.
    Save(stream, "WordToPDF.pdf");
    //Closes the Word and PDF document
    document.Close();
    pdfDocument.Close();
}

//Saves the PDF document
async void Save(MemoryStream streams, string filename)
{
    streams.Position = 0;
    StorageFile stFile;
    if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
    {
        FileSavePicker savePicker = new FileSavePicker();
        savePicker.DefaultFileExtension = ".pdf";
        savePicker.SuggestedFileName = filename;
        savePicker.FileTypeChoices.Add("Word Documents", new List<string>() { ".pdf" });
        stFile = await savePicker.PickSaveFileAsync();
    }
    else
    {
        StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
        stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
    }
    if (stFile != null)
    {
        using (IRandomAccessStream zipStream = await stFile.OpenAsync(FileAccessMode.ReadWrite))
        {
            //Write compressed data from memory to file
            using (Stream outstream = zipStream.AsStreamForWrite())
            {
                byte[] buffer = streams.ToArray();
                outstream.Write(buffer, 0, buffer.Length);
                outstream.Flush();
            }
        }
    }
    //Launch the saved Word file
    await Windows.System.Launcher.LaunchFileAsync(stFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
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

{% highlight c# tabtitle="Xamarin" %}
//Load the Word document as stream
Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Template.docx");
// Loads the stream into Word Document.
WordDocument wordDocument = new WordDocument(docStream, Syncfusion.DocIO.FormatType.Automatic);
//Instantiation of DocIORenderer for Word to PDF conversion
DocIORenderer render = new DocIORenderer();
//Sets AutoDetectComplexScript property to true to detect the complex scripts automatically
render.Settings.AutoDetectComplexScript = true;
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

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Preserve-complex-script-text-in-PDF).

### Hyphenation in Word-to-PDF conversion

Essential DocIO now allows hyphenating text in a Word document while converting it to PDF format based on the given language dictionaries. These dictionaries prescribe where words of a specific language can be hyphenated. Use the dictionary files as OpenOffice format dictionary.

N> 1. If automatic hyphenation is not enabled in the Word document, you can enable it by using WordDocument.Properties.Hyphenation.AutoHyphenation of DocIO.

The following code sample shows how to hyphenate text in a Word document while converting it to PDF format.
{% tabs %}  

{% highlight c# tabtitle="C#" %}
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

{% highlight vb.net tabtitle="VB.NET" %}
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

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument((assembly.GetManifestResourceStream("Sample.Assets.Template.docx")),
              FormatType.Docx))
{
    //Creates an instance of DocIORenderer - responsible for Word to PDF conversion
    DocIORenderer docIORenderer = new DocIORenderer();
    //Reads the language dictionary for hyphenation
    FileStream dictionaryStream = new FileStream("hyphen_en_US.dic", FileMode.Open);
    //Adds the hyphenation dictionary of the specified language
    Hyphenator.Dictionaries.Add("en-US", dictionaryStream);
    //Converts Word document into PDF document
    PdfDocument pdfDocument = docIORenderer.ConvertToPDF(document);
    //Save the document into stream.
    MemoryStream stream = new MemoryStream();
    pdfDocument.Save(stream);
    //Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.
    Save(stream, "WordToPDF.pdf");
    //Closes the Word and PDF document
    document.Close();
    pdfDocument.Close();
}

//Saves the PDF document
async void Save(MemoryStream streams, string filename)
{
    streams.Position = 0;
    StorageFile stFile;
    if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
    {
        FileSavePicker savePicker = new FileSavePicker();
        savePicker.DefaultFileExtension = ".pdf";
        savePicker.SuggestedFileName = filename;
        savePicker.FileTypeChoices.Add("Word Documents", new List<string>() { ".pdf" });
        stFile = await savePicker.PickSaveFileAsync();
    }
    else
    {
        StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
        stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
    }
    if (stFile != null)
    {
        using (IRandomAccessStream zipStream = await stFile.OpenAsync(FileAccessMode.ReadWrite))
        {
            //Write compressed data from memory to file
            using (Stream outstream = zipStream.AsStreamForWrite())
            {
                byte[] buffer = streams.ToArray();
                outstream.Write(buffer, 0, buffer.Length);
                outstream.Flush();
            }
        }
    }
    //Launch the saved Word file
    await Windows.System.Launcher.LaunchFileAsync(stFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
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

{% highlight c# tabtitle="Xamarin" %}
//Load the Word document as stream
Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Template.docx");
//Loads the stream into Word Document.
WordDocument wordDocument = new WordDocument(docStream, FormatType.Automatic);
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

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Hyphenation-in-Word-to-PDF).

### Track changes in Word-to-PDF conversion

The following code sample shows how to **preserve revision marks in a generated PDF** when converting Word documents with tracked changes or revisions.

{% tabs %}  

{% highlight c# tabtitle="C#" %}
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

{% highlight vb.net tabtitle="VB.NET" %}
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

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument((assembly.GetManifestResourceStream("Sample.Assets.Template.docx")),
              FormatType.Docx))
{
    //Sets revision types to preserve track changes in  Word when converting to PDF
    document.RevisionOptions.ShowMarkup = RevisionType.Deletions | RevisionType.Formatting | RevisionType.Insertions;
    //Creates an instance of DocIORenderer - responsible for Word to PDF conversion
    DocIORenderer docIORenderer = new DocIORenderer();
    //Converts Word document into PDF document
    PdfDocument pdfDocument = docIORenderer.ConvertToPDF(document);
    //Save the document into stream.
    MemoryStream stream = new MemoryStream();
    pdfDocument.Save(stream);
    //Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.
    Save(stream, "WordToPDF.pdf");
    //Closes the Word and PDF document
    document.Close();
    pdfDocument.Close();
}

//Saves the PDF document
async void Save(MemoryStream streams, string filename)
{
    streams.Position = 0;
    StorageFile stFile;
    if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
    {
        FileSavePicker savePicker = new FileSavePicker();
        savePicker.DefaultFileExtension = ".pdf";
        savePicker.SuggestedFileName = filename;
        savePicker.FileTypeChoices.Add("Word Documents", new List<string>() { ".pdf" });
        stFile = await savePicker.PickSaveFileAsync();
    }
    else
    {
        StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
        stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
    }
    if (stFile != null)
    {
        using (IRandomAccessStream zipStream = await stFile.OpenAsync(FileAccessMode.ReadWrite))
        {
            //Write compressed data from memory to file
            using (Stream outstream = zipStream.AsStreamForWrite())
            {
                byte[] buffer = streams.ToArray();
                outstream.Write(buffer, 0, buffer.Length);
                outstream.Flush();
            }
        }
    }
    //Launch the saved Word file
    await Windows.System.Launcher.LaunchFileAsync(stFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
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

{% highlight c# tabtitle="Xamarin" %}
//Load the Word document as stream
Stream docStream =
typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Template.docx");
//Loads the stream into Word Document
WordDocument wordDocument = new WordDocument(docStream, Syncfusion.DocIO.FormatType.Automatic);
//Sets revision types to preserve track changes in  Word when converting to PDF
wordDocument.RevisionOptions.ShowMarkup = RevisionType.Deletions | RevisionType.Formatting | RevisionType.Insertions;
//Instantiation of DocIORenderer for Word to PDF conversion
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

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Track-changes-in-Word-to-PDF).

#### Change the Track Changes Color

You can customize how track changes markup appears in a generated PDF when converting Word documents into PDF. The following code sample shows how to customize revision marks colors.

{% tabs %}  

{% highlight c# tabtitle="C#" %}
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

{% highlight vb.net tabtitle="VB.NET" %}
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

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument((assembly.GetManifestResourceStream("Sample.Assets.Template.docx")),
              FormatType.Docx))
{
    //Sets revision types to preserve track changes in  Word when converting to PDF
    document.RevisionOptions.ShowMarkup = RevisionType.Deletions | RevisionType.Formatting | RevisionType.Insertions;
	//Sets the color to be used for revision bars that identify document lines containing revised information
    wordDocument.RevisionOptions.RevisionBarsColor = RevisionColor.Blue;
    //Sets the color to be used for inserted content Insertion
    wordDocument.RevisionOptions.InsertedTextColor = RevisionColor.ClassicBlue;
    //Sets the color to be used for deleted content Deletion
    wordDocument.RevisionOptions.DeletedTextColor = RevisionColor.ClassicRed;
    //Sets the color to be used for content with changes of formatting properties
    wordDocument.RevisionOptions.RevisedPropertiesColor = RevisionColor.DarkYellow;
    //Creates an instance of DocIORenderer - responsible for Word to PDF conversion
    DocIORenderer docIORenderer = new DocIORenderer();
    //Converts Word document into PDF document
    PdfDocument pdfDocument = docIORenderer.ConvertToPDF(document);
    //Save the document into stream.
    MemoryStream stream = new MemoryStream();
    pdfDocument.Save(stream);
    //Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.
    Save(stream, "WordToPDF.pdf");
    //Closes the Word and PDF document
    document.Close();
    pdfDocument.Close();
}

//Saves the PDF document
async void Save(MemoryStream streams, string filename)
{
    streams.Position = 0;
    StorageFile stFile;
    if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
    {
        FileSavePicker savePicker = new FileSavePicker();
        savePicker.DefaultFileExtension = ".pdf";
        savePicker.SuggestedFileName = filename;
        savePicker.FileTypeChoices.Add("Word Documents", new List<string>() { ".pdf" });
        stFile = await savePicker.PickSaveFileAsync();
    }
    else
    {
        StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
        stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
    }
    if (stFile != null)
    {
        using (IRandomAccessStream zipStream = await stFile.OpenAsync(FileAccessMode.ReadWrite))
        {
            //Write compressed data from memory to file
            using (Stream outstream = zipStream.AsStreamForWrite())
            {
                byte[] buffer = streams.ToArray();
                outstream.Write(buffer, 0, buffer.Length);
                outstream.Flush();
            }
        }
    }
    //Launch the saved Word file
    await Windows.System.Launcher.LaunchFileAsync(stFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
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

{% highlight c# tabtitle="Xamarin" %}
//Load the Word document as stream
Stream docStream =
typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Template.docx");
//Loads the stream into Word Document
WordDocument wordDocument = new WordDocument(docStream, Syncfusion.DocIO.FormatType.Automatic);
//Sets revision types to preserve track changes in  Word when converting to PDF
wordDocument.RevisionOptions.ShowMarkup = RevisionType.Deletions | RevisionType.Formatting | RevisionType.Insertions;
//Sets the color to be used for revision bars that identify document lines containing revised information
wordDocument.RevisionOptions.RevisionBarsColor = RevisionColor.Blue;
//Sets the color to be used for inserted content Insertion
wordDocument.RevisionOptions.InsertedTextColor = RevisionColor.ClassicBlue;
//Sets the color to be used for deleted content Deletion
wordDocument.RevisionOptions.DeletedTextColor = RevisionColor.ClassicRed;
//Sets the color to be used for content with changes of formatting properties
wordDocument.RevisionOptions.RevisedPropertiesColor = RevisionColor.DarkYellow;
//Instantiation of DocIORenderer for Word to PDF conversion
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

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Change-track-changes-color).

#### Show or Hide Revisions in Balloons

The default Word to PDF conversion renders the deletion and formatting changes in balloons when enabling ShowMarkup property. However, you can hide revisions in balloons by using following code example.

{% tabs %}  

{% highlight c# tabtitle="C#" %}
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

{% highlight vb.net tabtitle="VB.NET" %}
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

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument((assembly.GetManifestResourceStream("Sample.Assets.Template.docx")),
              FormatType.Docx))
{
    //Sets revision types to preserve track changes in Word when converting to PDF
    wordDocument.RevisionOptions.ShowMarkup = RevisionType.Deletions | RevisionType.Formatting | RevisionType.Insertions;
    //Hides showing revisions in balloons when converting Word documents to PDF
    wordDocument.RevisionOptions.ShowInBalloons = RevisionType.None;
    //Creates an instance of DocIORenderer - responsible for Word to PDF conversion
    DocIORenderer docIORenderer = new DocIORenderer();
    //Converts Word document into PDF document
    PdfDocument pdfDocument = docIORenderer.ConvertToPDF(document);
    //Save the document into stream.
    MemoryStream stream = new MemoryStream();
    pdfDocument.Save(stream);
    //Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.
    Save(stream, "WordToPDF.pdf");
    //Closes the Word and PDF document
    document.Close();
    pdfDocument.Close();
}

//Saves the PDF document
async void Save(MemoryStream streams, string filename)
{
    streams.Position = 0;
    StorageFile stFile;
    if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
    {
        FileSavePicker savePicker = new FileSavePicker();
        savePicker.DefaultFileExtension = ".pdf";
        savePicker.SuggestedFileName = filename;
        savePicker.FileTypeChoices.Add("Word Documents", new List<string>() { ".pdf" });
        stFile = await savePicker.PickSaveFileAsync();
    }
    else
    {
        StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
        stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
    }
    if (stFile != null)
    {
        using (IRandomAccessStream zipStream = await stFile.OpenAsync(FileAccessMode.ReadWrite))
        {
            //Write compressed data from memory to file
            using (Stream outstream = zipStream.AsStreamForWrite())
            {
                byte[] buffer = streams.ToArray();
                outstream.Write(buffer, 0, buffer.Length);
                outstream.Flush();
            }
        }
    }
    //Launch the saved Word file
    await Windows.System.Launcher.LaunchFileAsync(stFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
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

{% highlight c# tabtitle="Xamarin" %}
//Load the Word document as stream
Stream docStream =
typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Template.docx");
//Loads the stream into Word Document
WordDocument wordDocument = new WordDocument(docStream, Syncfusion.DocIO.FormatType.Automatic);
//Sets revision types to preserve track changes in Word when converting to PDF
wordDocument.RevisionOptions.ShowMarkup = RevisionType.Deletions | RevisionType.Formatting | RevisionType.Insertions;
//Hides showing revisions in balloons when converting Word documents to PDF
wordDocument.RevisionOptions.ShowInBalloons = RevisionType.None;
//Instantiation of DocIORenderer for Word to PDF conversion
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

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Show-or-hide-revisions-in-balloons).

### Comments in Word-to-PDF conversion
The following code sample shows how to **preserve comments balloon in a generated PDF** when converting Word documents with comments. Also you can customize how comments balloon color appears in a generated PDF.

{% tabs %}  

{% highlight c# tabtitle="C#" %}
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

{% highlight vb.net tabtitle="VB.NET" %}
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

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Loads an existing Word document.
using (WordDocument wordDocument = new WordDocument((assembly.GetManifestResourceStream("Sample.Assets.Template.docx")),FormatType.Docx))
{
	//Sets ShowInBalloons to render a document comments in converted PDF document.
	wordDocument.RevisionOptions.CommentDisplayMode = CommentDisplayMode.ShowInBalloons;
	//Sets the color to be used for Comment Balloon.
	wordDocument.RevisionOptions.CommentColor = RevisionColor.Blue;
	//Creates an instance of DocIORenderer.
	using (DocIORenderer docIORenderer = new DocIORenderer())
	{
		//Converts Word document into PDF document.
		using (PdfDocument pdfDocument = docIORenderer.ConvertToPDF(wordDocument))
		{
			//Save the document into stream.
			using (MemoryStream stream = new MemoryStream())
			{
				pdfDocument.Save(stream);
				//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.
				Save(stream, "Sample.pdf");
			}
		}
	}
}
//Saves the PDF document.
async void Save(MemoryStream streams, string filename)
{
	streams.Position = 0;
	StorageFile stFile;
	if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
	{
		FileSavePicker savePicker = new FileSavePicker();
		savePicker.DefaultFileExtension = ".pdf";
		savePicker.SuggestedFileName = filename;
		savePicker.FileTypeChoices.Add("Word Documents", new List<string>() { ".pdf" });
		stFile = await savePicker.PickSaveFileAsync();
	}
	else
	{
		StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
		stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
	}
	if (stFile != null)
	{
		using (IRandomAccessStream zipStream = await stFile.OpenAsync(FileAccessMode.ReadWrite))
		{
			//Write compressed data from memory to file.
			using (Stream outstream = zipStream.AsStreamForWrite())
			{
				byte[] buffer = streams.ToArray();
				outstream.Write(buffer, 0, buffer.Length);
				outstream.Flush();
			}
		}
	}
	//Launch the saved Word file.
	await Windows.System.Launcher.LaunchFileAsync(stFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
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

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing wod document
using (WordDocument wordDocument = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Automatic))
{
	//Sets ShowInBalloons to render a document comments in converted PDF document.
	wordDocument.RevisionOptions.CommentDisplayMode = CommentDisplayMode.ShowInBalloons;
	//Sets the color to be used for Comment Balloon.
	wordDocument.RevisionOptions.CommentColor = RevisionColor.Blue;
	//Creates an instance of DocIORenderer.
	using (DocIORenderer docIORenderer = new DocIORenderer())
	{
		//Converts Word document into PDF document.
		using (PdfDocument pdfDocument = docIORenderer.ConvertToPDF(wordDocument))
		{
			//Saves the Word document to MemoryStream
			using (MemoryStream stream = new MemoryStream())
			{
				pdfDocument.Save(stream);
				//Save the stream as a file in the device and invoke it for viewing
				Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.pdf", "application/pdf", stream);

				//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
				//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
			}
		}
	}
}
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Preserve-comments-in-Word-to-PDF).

### Preserve Ole Equation as bitmap image

This setting allows you to preserve Ole Equation as bitmap image in the converted PDF document.

The following code sample shows how to preserve Ole Equation as bitmap image in the converted PDF document.

{% tabs %}  

{% highlight c# tabtitle="C#" %}
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

{% highlight vb.net tabtitle="VB.NET" %}
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

{% highlight c# tabtitle="UWP" %}
//DocIO supports to preserve the Ole Equation as bitmap image in the converted PDF document in Windows forms, WPF, ASP.NET and ASP.NET MVC platform alone.
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//DocIO supports to preserve the Ole Equation as bitmap image in the converted PDF document in Windows forms, WPF, ASP.NET and ASP.NET MVC platform alone.
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//DocIO supports to preserve the Ole Equation as bitmap image in the converted PDF document in Windows forms, WPF, ASP.NET and ASP.NET MVC platform alone.
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Ole-Equation-as-bitmap).

### Restrict all permission in a PDF document

you can restrict all the permission in a PDF document using [PdfPermissionsFlags](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfPermissionsFlags.html)

The below code example shows how to restrict Copying and Printing permission of the PDF document.

{% tabs %}  

{% highlight c# tabtitle="C#" %}
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

{% highlight vb.net tabtitle="VB.NET" %}
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

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("Sample.Assets.Template.docx");
WordDocument wordDocument = new WordDocument(inputStream, Syncfusion.DocIO.FormatType.Automatic);
inputStream.Dispose();
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
//Save the document into stream.
MemoryStream stream = new MemoryStream();
pdfDocument.Save(stream);
//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.
Save(stream, "Output.pdf");
pdfDocument.Close();
			
//Saves the PDF document
async void Save(MemoryStream streams, string filename)
{
    streams.Position = 0;
    StorageFile stFile;
    if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
    {
        FileSavePicker savePicker = new FileSavePicker();
        savePicker.DefaultFileExtension = ".pdf";
        savePicker.SuggestedFileName = filename;
        savePicker.FileTypeChoices.Add("Word Documents", new List<string>() { ".pdf" });
        stFile = await savePicker.PickSaveFileAsync();
    }
    else
    {
        StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
        stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
    }
    if (stFile != null)
    {
        using (IRandomAccessStream zipStream = await stFile.OpenAsync(FileAccessMode.ReadWrite))
        {
            //Write compressed data from memory to file
            using (Stream outstream = zipStream.AsStreamForWrite())
            {
                byte[] buffer = streams.ToArray();
                outstream.Write(buffer, 0, buffer.Length);
                outstream.Flush();
            }
        }
    }
    //Launch the saved Word file
    await Windows.System.Launcher.LaunchFileAsync(stFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
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

{% highlight c# tabtitle="Xamarin" %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream fileStream = assembly.GetManifestResourceStream("XamarinApp.Data.Template.docx");
//Opens an existing document from file system through constructor of WordDocument class
WordDocument document = new WordDocument(fileStream, FormatType.Automatic);
fileStream.Dispose();
//Instantiation of DocIORenderer for Word to PDF conversion
DocIORenderer render = new DocIORenderer();
//Converts Word document into PDF document
PdfDocument pdfDocument = render.ConvertToPDF(document);
//Document security.
PdfSecurity security = pdfDocument.Security;
//Specifies key size and encryption algorithm using 256-bit key in AES mode.
security.KeySize = PdfEncryptionKeySize.Key256Bit;
security.Algorithm = Syncfusion.Pdf.Security.PdfEncryptionAlgorithm.AES;
security.OwnerPassword = "syncfusion";
//It restrict printing and copying of PDF document
security.Permissions = ~(PdfPermissionsFlags.CopyContent | PdfPermissionsFlags.Print);
render.Dispose();
document.Close();
//Saves the PDF file to file on local storage    
MemoryStream pdfStream = new MemoryStream();
pdfDocument.Save(pdfStream);
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.pdf", "application/pdf", pdfStream);
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Restrict-permission-in-PDF).

## Font Substitution

When the necessary fonts used in the Word document has not been installed in the production machine, then Essential DocIO uses the ”Microsoft Sans Serif” as default font for rendering the text. This leads to preservation difference in generated PDF as each font has different glyphs for characters. To learn more about the default font substitution, click [here](https://www.syncfusion.com/kb/7570/what-happens-when-the-word-document-used-fonts-for-a-text-is-not-installed-in-production).

To avoid this, the Essential DocIO library allows you to set an alternate font for the missing font used in the Word document.

### Use alternate font from installed fonts

You can use any other alternate fonts instead of "Microsoft Sans Serif" to layout and render the text during Word to PDF conversion by using the [SubstituteFont](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.FontSettings.html) event.

The following code example shows how to use alternate font instead of "Microsoft Sans Serif" when the specified font not installed in the machine. 

{% tabs %}
{% highlight c# tabtitle="C#" %}
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

{% highlight vb.net tabtitle="VB.NET" %}
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

{% highlight c# tabtitle="UWP" %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Loads an existing Word document
WordDocument document = new WordDocument();
document.Open(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Docx);
//Hooks the font substitution event
document.FontSettings.SubstituteFont += FontSettings_SubstituteFont;
//Creates an instance of DocIORenderer - responsible for Word to PDF conversion
DocIORenderer docIORenderer = new DocIORenderer();
//Converts Word document into PDF document
PdfDocument pdfDocument = docIORenderer.ConvertToPDF(document);
//Unhooks the font substitution event after converting to PDF
document.FontSettings.SubstituteFont -= FontSettings_SubstituteFont;
//Releases all resources used by the Word document and DocIO Renderer objects
docIORenderer.Dispose();
document.Close();
//Save the document into stream
MemoryStream stream = new MemoryStream();
pdfDocument.Save(stream);
//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respected code samples.
Save(stream, "WordToPDF.pdf");
//Closes the PDF document
pdfDocument.Close();

//Saves the PDF document
async void Save(MemoryStream streams, string filename)
{
    streams.Position = 0;
    StorageFile stFile;
    if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
    {
        FileSavePicker savePicker = new FileSavePicker();
        savePicker.DefaultFileExtension = ".pdf";
        savePicker.SuggestedFileName = filename;
        savePicker.FileTypeChoices.Add("Adobe PDF Document", new List<string>() { ".pdf" });
        stFile = await savePicker.PickSaveFileAsync();
    }
    else
    {
        StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
        stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
    }
    if (stFile != null)
    {
        using (IRandomAccessStream zipStream = await stFile.OpenAsync(FileAccessMode.ReadWrite))
        {
            //Write compressed data from memory to file
            using (Stream outstream = zipStream.AsStreamForWrite())
            {
                byte[] buffer = streams.ToArray();
                outstream.Write(buffer, 0, buffer.Length);
                outstream.Flush();
            }
        }
    }
    //Launch the saved Word file
    await Windows.System.Launcher.LaunchFileAsync(stFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
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
outputStream.Position = 0;
//Download Word document in the browser
return File(outputStream, "application/pdf", "WordtoPDF.pdf");
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Load the Word document as stream
Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Template.docx");
//Loads the stream into Word document
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

//Download the helper files from the following link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}
{% endtabs %}

###### Event Handler to use alternate installed font

The following code example shows how to set the **alternate installed font** instead of "Microsoft Sans Serif" during Word to PDF conversion.

{% tabs %}
{% highlight c# tabtitle="C#" %}
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

{% highlight vb.net tabtitle="VB.NET" %}
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

{% highlight c# tabtitle="UWP" %}
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

{% highlight c# tabtitle="ASP.NET Core" %}
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

{% highlight c# tabtitle="Xamarin" %}
void FontSettings_SubstituteFont(object sender, SubstituteFontEventArgs args)
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
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Use-alternate-installed-font).

###### Event Handler to use alternate font without installing

The following code example shows how to use the alternate fonts instead of "Microsoft Sans Serif" **without installing the fonts** into production machine.

{% tabs %}
{% highlight c# tabtitle="C#" %}
private void FontSettings_SubstituteFont(object sender, SubstituteFontEventArgs args)
{
    //Sets the alternate font when a specified font is not installed in the production environment
	if (args.OrignalFontName == "Arial Unicode MS" && args.FontStyle == FontStyle.Regular)
	    args.AlternateFontStream =  new FileStream("Arial.TTF" ,FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
	else
	    args.AlternateFontName = "Times New Roman";
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Private Sub SubstituteFont(ByVal sender As Object, ByVal args As SubstituteFontEventArgs)
    'Sets the alternate font when a specified font is not installed in the production environment
    If args.OrignalFontName = "Arial Unicode MS" && args.FontStyle == FontStyle.Regular Then
        args.AlternateFontStream = New FileStream("Arial.TTF" ,FileMode.Open, FileAccess.Read, FileShare.ReadWrite)
    Else
	    args.AlternateFontName = "Times New Roman"
    End If
End Sub
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
private void FontSettings_SubstituteFont(object sender, SubstituteFontEventArgs args)
{
    //Sets the alternate font when a specified font is not installed in the production environment
    if (args.OrignalFontName == "Arial Unicode MS" && args.FontStyle == FontStyle.Regular)
        args.AlternateFontStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Arial.TTF");
    else
        args.AlternateFontName = "Times New Roman";
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
private void FontSettings_SubstituteFont(object sender, SubstituteFontEventArgs args)
{
    //Sets the alternate font when a specified font is not installed in the production environment
    if (args.OrignalFontName == "Arial Unicode MS" && args.FontStyle == FontStyle.Regular)
        args.AlternateFontStream = new FileStream("Arial.TTF", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
    else
	    args.AlternateFontName = "Times New Roman";
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
private void FontSettings_SubstituteFont(object sender, SubstituteFontEventArgs args)
{
    //Sets the alternate font when a specified font is not installed in the production environment
    if (args.OrignalFontName == "Arial Unicode MS" && args.FontStyle == FontStyle.Regular)
        args.AlternateFontStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Arial.TTF");
    else
	    args.AlternateFontName = "Times New Roman";
}
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Use-alternate-font-without-installing).

N> The above event will be triggered only if the specified font is not installed in production machine.

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
Underline
</td>
<td>
Only Single, Dotted, Dash, DotDash, DotDotDash, Words, DashHeavy, DashLong, DashLongHeavy, DotDashHeavy, DotDotDashHeavy, DottedHeavy and Thick underline styles are supported.
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
</table>

## See Also

* [How to convert Word document to PDF in UWP](https://www.syncfusion.com/kb/10270/how-to-convert-word-document-to-pdf-in-uwp)
* [How to add signature field in the PDF converted from Word](https://www.syncfusion.com/kb/12956/how-to-add-signature-field-in-the-pdf-converted-from-word)
* [How to avoid conflicts while using DocIORenderer and other controls in UWP](https://www.syncfusion.com/kb/12938/how-to-avoid-conflicts-while-using-dociorenderer-and-other-controls-in-uwp)
* [How to deploy .NET Core application with Word to PDF conversion capabilities in Linux OS](https://www.syncfusion.com/kb/8470/how-to-deploy-net-core-application-with-word-to-pdf-conversion-capabilities-in-linux-os)
* [Is it possible to perform Word to PDF conversion in Azure Environment ?](https://www.syncfusion.com/kb/7751/is-it-possible-to-perform-word-to-pdf-conversion-in-azure-environment)
* [How to convert Word document to PDF in AWS Lambda](https://www.syncfusion.com/kb/11905/how-to-convert-word-document-to-pdf-in-aws-lambda)
* [How to convert Word document to PDF in Azure App service on Linux](https://www.syncfusion.com/kb/11888/how-to-convert-word-document-to-pdf-in-azure-app-service-on-linux)
* [How to mail merge Word documents and convert to PDF in Azure Functions v2](https://www.syncfusion.com/kb/11197/how-to-mail-merge-word-documents-and-convert-to-pdf-in-azure-functions-v2)