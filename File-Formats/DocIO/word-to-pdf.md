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

For WPF, Windows Forms, ASP.NET and ASP.NET MVC applications
* using Syncfusion.DocIO
* using Syncfusion.DocIO.DLS
* using Syncfusion.OfficeChart
* using Syncfusion.DocToPDFConverter
* using Syncfusion.OfficeChartToImageConverter
* using Syncfusion.Pdf

For ASP.NET Core and Xamarin applications
* using Syncfusion.DocIO
* using Syncfusion.DocIO.DLS
* using Syncfusion.DocIORenderer
* using Syncfusion.Pdf

The following code example illustrates how to convert a Word document into PDF document.

{% tabs %}
{% highlight c# %}
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

{% highlight vb.net %}
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

{% highlight UWP %}
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

{% highlight asp.net core %}
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

{% highlight XAMARIN %}
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

N> 1. Word to PDF conversion is not supported in Silverlight, Windows Phone, WinRT, and Universal applications.
N> 2. Word to PDF conversion is supported in Blazor server-side application alone and is not supported in Blazor client-side application.
N> 3. Creating an instance of ChartToImageConverter class is mandatory to convert the charts present in the Word to PDF. Otherwise, the charts are not preserved in the converted PDF.
N> 4. The ChartToImageConverter is supported from .NET Framework 4.0 onwards.
N> 5. Total number of pages in the converted PDF may vary based on unsupported elements in the input Word document.
N> 6. "DocIO supports Word to PDF conversion in UWP DocIORenderer." For further information, please refer [here](https://www.syncfusion.com/kb/10270/how-to-convert-word-document-to-pdf-in-uwp)

## Word to PDF conversion in Linux OS

In Linux OS, you can perform the Word to PDF conversion using .NET Core (Targeting .netcoreapp) application. You can refer [Word to PDF conversion NuGet packages](https://help.syncfusion.com/file-formats/docio/nuget-packages-required#converting-word-document-to-pdf) to know about the packages required to deploy .NET Core (Targeting .netcoreapp) application with Word to PDF conversion capabilities.

In addition to the previous NuGet packages, SkiaSharp.Linux helper NuGet package is required that can be generated by the following steps: 

1. Download libSkiaSharp.so [here](https://github.com/mono/SkiaSharp/releases/tag/v1.59.3#).
2. Create a folder and name it as SkiaSharp.Linux and place the downloaded file in the folder structure "SkiaSharp.Linux\runtimes\linux-x64\native"
3. Create a nuspec file with name SkiaSharp.Linux.nuspec using the following metadata information and place it inside SkiaSharp.Linux folder. The nuspec file can be customized.

	{% tabs %}
	{% highlight XML %}
	<?xml version="1.0" encoding="utf-8"?>
	<package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
		<metadata>
			<id>SkiaSharp.Linux</id>
			<version>1.59.3</version>
			<title>SkiaSharp for Linux</title>
			<authors>Syncfusion Inc.</authors>
			<owners>Syncfusion Inc.</owners>
			<requireLicenseAcceptance>false</requireLicenseAcceptance>
			<description>SkiaSharp for Linux is a supporting package for Linux platforms.</description>
			<tags>linux,cross-platform,skiasharp,net-standard,net-core,word-to-pdf</tags>
			<dependencies>
				<group targetFramework=".NETStandard1.4">
					<dependency id="SkiaSharp" version="1.59.3" />
				</group>
			</dependencies>
		</metadata>
	</package>
	{% endhighlight %}
	{% endtabs %}

4. Make sure that the nuget.exe file is present along with SkiaSharp.Linux folder (in the parent folder of SkiaSharp.Linux folder). If not, download it from [here](https://www.nuget.org/downloads#).
5. Open a command prompt and navigate to SkiaSharp.Linux folder.
6. Execute the following command.

~~~
nuget pack SkiaSharp.Linux\SkiaSharp.Linux.nuspec -outputdirectory "C:\NuGet" 
~~~

The output directory can be customized as per your need.

Now, SkiaSharp.Linux NuGet will be generated in the mentioned output directory and add the generated NuGet as additional reference. You can also find the SkiaSharp.Linux NuGet package created by us from [here](http://www.syncfusion.com/downloads/support/directtrac/general/ze/SkiaSharp.Linux.1.59.3-2103435070#).

Frequently Asked Questions
* [How to copy necessary fonts to Linux containers?](https://help.syncfusion.com/file-formats/docio/faq#how-to-copy-necessary-fonts-to-linux-containers)
* [How to set culture / locale in Docker containers (Windows & Linux containers)?](https://help.syncfusion.com/file-formats/docio/faq#how-to-set-culturelocale-in-docker-containers-windows-and-linux-containers)
* [How to resolve LibSkiaSharp not found Exception?](https://help.syncfusion.com/file-formats/docio/faq#how-to-resolve-libskiasharp-not-found-exception)

## Customization settings
The Essential DocIO provides settings while performing Word to PDF conversion mentioned below, 

### Fast rendering

This setting allows you to convert PDF faster by using direct PDF rendering approach rather than EMF rendering approach.

The following code sample shows how to convert the Word document to PDF using direct PDF rendering approach. 

{% tabs %}
{% highlight c# %}
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

{% highlight vb.net %}
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

{% highlight UWP %}
//DocIO supports Word to PDF fast rendering in Windows forms, WPF, ASP.NET and ASP.NET MVC platform alone
{% endhighlight %}

{% highlight ASP.NET CORE %}
//DocIO supports Word to PDF fast rendering in Windows forms, WPF, ASP.NET and ASP.NET MVC platform alone
{% endhighlight %}

{% highlight XAMARIN %}
//DocIO supports Word to PDF fast rendering in Windows forms, WPF, ASP.NET and ASP.NET MVC platform alone
{% endhighlight %}
{% endtabs %}

### Embedding fonts

You can customize the TrueType fonts embedding in two ways as follows:

#### Embed Subset Fonts

This setting allows you to embed the particular font information (glyphs) from the TrueType fonts used for the rendered characters in converted PDF document.

The following code sample shows how to embed the TrueType fonts into the converted PDF document.

{% tabs %}
{% highlight c# %}
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

{% highlight vb.net %}
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

{% highlight UWP %}
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

{% highlight ASP.NET Core %}
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

{% highlight Xamarin %}
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

#### Embed Complete Fonts

This setting allows you to embed the complete font information (glyphs) from the TrueType fonts used in converted PDF document.

The following code sample shows how to embed the complete TrueType fonts into the converted PDF document.

{% tabs %}
{% highlight c# %}
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

{% highlight vb.net %}
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

{% highlight UWP %}
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

{% highlight ASP.NET Core %}
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

{% highlight Xamarin %}
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

### Accessible PDF document

This setting allows you to determine whether to preserve document structured tags in the converted PDF document for accessibility (508 compliance) support. This property will set the title and description for images, diagrams and other objects in the generated PDF document. This information will be useful for people with vision or cognitive impairments who may not able to see or understand the object

The following code sample shows how to preserve document structured tags in the converted PDF document.

{% tabs %}
{% highlight c# %}
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

{% highlight vb.net %}
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

{% highlight UWP %}
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

{% highlight asp.net core %}
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

{% highlight XAMARIN %}
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

### Word document headings to PDF bookmarks

This setting allows you to determine whether to preserve Word document headings (i.e., paragraph with heading style and outline level) as bookmarks in the converted PDF document. As per Microsoft Word behavior, either Word document headings or bookmarks can be exported as PDF bookmarks. By default, DocIO preserves Word documents bookmarks as PDF bookmarks in converted PDF document.

The following code sample shows how to preserve Word document headings as bookmarks in the converted PDF document.

{% tabs %}
{% highlight c# %}
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

{% highlight vb.net %}
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

{% highlight UWP %}
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

{% highlight asp.net core %}
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

{% highlight XAMARIN %}
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

### Word document form field to PDF form field.

This setting allows you to determine whether to preserve Word document form fields (Text form field, Checkbox form field and Drop-down form field) as PDF form fields in the converted PDF document. This features helps in creating fillable PDF forms from Word document.

The following code sample shows how to preserve Word document form field as PDF form field in the converted PDF document.

{% tabs %}
{% highlight c# %}
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

{% highlight vb.net %}
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

{% highlight UWP %}
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

{% highlight asp.net core %}
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

{% highlight XAMARIN %}
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

### Image quality 

This setting allows you to determine the quality of the charts and JPEG images in the converted PDF document.

The following code sample shows how to customize the image quality of charts and JPEG images in the converted PDF document.

{% tabs %}
{% highlight c# %}
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

{% highlight vb.net %}
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

{% highlight UWP %}
//DocIO supports Word to PDF Image in Windows forms, WPF, ASP.NET and ASP.NET MVC platform alone
{% endhighlight %}

{% highlight ASP.NET CORE %}
//DocIO supports Word to PDF Image in Windows forms, WPF, ASP.NET and ASP.NET MVC platform alone
{% endhighlight %}

{% highlight XAMARIN %}
//DocIO supports Word to PDF Image in Windows forms, WPF, ASP.NET and ASP.NET MVC platform alone
{% endhighlight %}
{% endtabs %}

### Identical image optimization 

This setting reduces the Main Memory usage in Word to PDF conversion by reusing the identical images.

The following code sample shows how to reduce the Main Memory usage while converting Word to PDF by reusing the identical images.

{% tabs %}
{% highlight c# %}
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

{% highlight vb.net %}
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

{% highlight UWP %}
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

{% highlight ASP.NET Core %}
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

{% highlight Xamarin %}
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

### PDF Conformance Level

This setting allows you to set the PDF conformance level.

The following code sample shows how to set the PdfConformanceLevel while converting Word to PDF.

{% tabs %}
{% highlight c# %}
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

{% highlight vb.net %}
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

{% highlight UWP %}
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

{% highlight ASP.NET Core %}
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

{% highlight Xamarin %}
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

### Enable Alternate Chunks

This setting allows you to include the alternate chunks while converting Word to PDF conversion. As default, it includes alternate chunks.

The following code sample shows how to exclude the alternate chunk parts in Word to PDF conversion.

{% tabs %}
{% highlight c# %}
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

{% highlight vb.net %}
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

{% highlight UWP %}
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

{% highlight ASP.NET Core %}
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

{% highlight Xamarin %}
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

### Complex Script Text

This setting allows you to preserve the complex script text in the converted PDF document.

The following code sample shows how to preserve the complex script text in the converted PDF document.

{% tabs %}  

{% highlight c# %}
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
System.Diagnostics.Process.Start("WordtoPDF.pdf");
//Closes the instance of document objects
pdfDocument.Close(true);
wordDocument.Close();
{% endhighlight %}

{% highlight vb.net %}
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

{% highlight UWP %}
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

{% highlight ASP.NET Core %}
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

{% highlight Xamarin %}
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

### Hyphenation in Word-to-PDF conversion

Essential DocIO now allows hyphenating text in a Word document while converting it to PDF format based on the given language dictionaries. These dictionaries prescribe where words of a specific language can be hyphenated. Use the dictionary files as OpenOffice format dictionary.

N> 1. If automatic hyphenation is not enabled in the Word document, you can enable it by using WordDocument. property of DocIO.

The following code sample shows how to hyphenate text in a Word document while converting it to PDF format.
{% tabs %}  

{% highlight c# %}
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

{% highlight vb.net %}
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

{% highlight UWP %}
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

{% highlight ASP.NET Core %}
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

{% highlight Xamarin %}
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

### Track changes in Word-to-PDF conversion

The following code sample shows how to preserve revision marks in a generated PDF when converting Word documents with tracked changes or revisions.

{% tabs %}  

{% highlight c# %}
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

{% highlight vb.net %}
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

{% highlight UWP %}
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

{% highlight ASP.NET Core %}
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

{% highlight Xamarin %}
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

### Preserve Ole Equation as bitmap image

This setting allows you to preserve Ole Equation as bitmap image in the converted PDF document.

The following code sample shows how to preserve Ole Equation as bitmap image in the converted PDF document.

{% tabs %}  

{% highlight c# %}
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

{% highlight vb.net %}
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

{% highlight UWP %}
//DocIO supports to preserve the Ole Equation as bitmap image in the converted PDF document in Windows forms, WPF, ASP.NET and ASP.NET MVC platform alone.
{% endhighlight %}

{% highlight ASP.NET Core %}
//DocIO supports to preserve the Ole Equation as bitmap image in the converted PDF document in Windows forms, WPF, ASP.NET and ASP.NET MVC platform alone.
{% endhighlight %}

{% highlight Xamarin %}
//DocIO supports to preserve the Ole Equation as bitmap image in the converted PDF document in Windows forms, WPF, ASP.NET and ASP.NET MVC platform alone.
{% endhighlight %}

{% endtabs %}

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
List - Bulleted, Numbered and Multi-level lists
</td>
<td>
The image bullets preserved in the document may be replaced by the disc style bullet.
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
Single underline style only supported.
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
Not supported
</td>
</tr>
<tr>
<td>
Rotation – predefined shape
</td>
<td>
Not supported
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
Allow AutoFit
</td>
<td>
Not supported
</td>
</tr>
<tr>
<td>
Comments
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
Not supported
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