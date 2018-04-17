---
title: Word document to PDF Conversion
description: Converting Word document to PDF using DocIO
platform: file-formats
control: DocIO
documentation: UG
---

# Word document to PDF Conversion

## Converting Word to PDF

The Word document files are converted as a PDF document with a few lines of code by using the Essential DocIO. It works perfectly when you create an input Word document from scratch or load an existing Word document and easily converted into PDF. 

Refer to the following links for assemblies required based on platforms to convert the Word document to PDF.

* [Assemblies Information](https://help.syncfusion.com/file-formats/docio/assemblies-required#converting-word-document-to-pdf) 
* [NuGet Information](https://help.syncfusion.com/file-formats/docio/nuget-packages-required#converting-word-document-to-pdf)

The following namespaces are required to compile the code: 

* using Syncfusion.DocIO
* using Syncfusion.DocIO.DLS
* using Syncfusion.OfficeChart
* using Syncfusion.DocToPDFConverter
* using Syncfusion.OfficeChartToImageConverter
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

{% highlight asp.net core %}
// Open the file as Stream
FileStream docStream = new FileStream(@"D:\Template.docx", FileMode.Open, FileAccess.Read);

//Loads file stream into Word document

WordDocument wordDocument = new WordDocument(docStream, Syncfusion.DocIO.FormatType.Automatic);

//Instantiation of DocIORenderer for Word to PDF conversion

DocIORenderer render = new DocIORenderer();

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

{% highlight xamarin %}
private void OnButtonClicked(object sender, EventArgs e)
{

//Load the Word document as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample.docx");

// Loads the stream into Word Document.

WordDocument wordDocument = new WordDocument(docStream, Syncfusion.DocIO.FormatType.Automatic);
	
//Instantiation of DocIORenderer for Word to PDF conversion

DocIORenderer render = new DocIORenderer();

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

}
{% endhighlight %}
{% endtabs %}


## Word to PDF conversion in Linux OS

In Linux OS, you can perform the Word to PDF conversion using .NET Core application. To deploy .NET Core application with Word to PDF conversion capabilities in Linux OS, the following NuGet packages are referred in your .NET Core application:

<table>
<thead>
<tr>
<th>NuGet package<br/><br/></th>
<th>Installation command in package manager<br/><br/></th>
</tr>
</thead>
<tbody>
<tr>
<td>
Syncfusion.DocIORenderer.NetStandard<br/><br/></td><td>
Install-package Syncfusion.DocIORenderer.NetStandard -source http://nuget.syncfusion.com/nuget_aspnetcore/nuget/getsyncfusionpackages/aspnetcore<br/><br/></td></tr>
<tr>
<td>
Syncfusion.DocIO.NetStandard<br/><br/></td><td>
Install-package Syncfusion.DocIO.NetStandard -source http://nuget.syncfusion.com/nuget_aspnetcore/nuget/getsyncfusionpackages/aspnetcore<br/><br/></td></tr>
<tr>
<td>
Syncfusion.Compression.NetStandard<br/><br/></td><td>
Install-package Syncfusion.Compression.NetStandard -source http://nuget.syncfusion.com/nuget_aspnetcore/nuget/getsyncfusionpackages/aspnetcore<br/><br/></td></tr>
<tr>
<td>
Syncfusion.OfficeChart.NetStandard<br/><br/></td><td>
Install-package Syncfusion.OfficeChart.NetStandard -source http://nuget.syncfusion.com/nuget_aspnetcore/nuget/getsyncfusionpackages/aspnetcore<br/><br/></td></tr>
<tr>
<td>
Syncfusion.Pdf.NetStandard<br/><br/></td><td>
Install-package Syncfusion.Pdf.NetStandard -source http://nuget.syncfusion.com/nuget_aspnetcore/nuget/getsyncfusionpackages/aspnetcore<br/><br/></td></tr>
<tr>
<td>
SkiaSharp<br/><br/></td><td>
Install-Package SkiaSharp -Version 1.59.3 -source https://nuget.org/api/v2 <br/><br/></td></tr>
</tbody>
</table>

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


## Customization settings
The Essential DocIO provides settings while performing Word to PDF conversion mentioned below, 

### Fast rendering

This setting allows you to convert PDF faster by using direct PDF rendering approach rather than EMF rendering approach.

The following code sample shows how to convert the Word document to PDF using direct PDF rendering approach. 

{% tabs %}
{% highlight c# %}
//Loads an existing Word document

WordDocument wordDocument = new WordDocument("Sample.docx", FormatType.Docx);

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

Dim wordDocument As New WordDocument("Sample.docx", FormatType.Docx)

'Initializes the ChartToImageConverter for converting charts during Word to pdf conversion

wordDocument.ChartToImageConverter = New ChartToImageConverter()

'Sets the scaling mode for charts (Normal mode reduces the Pdf file size)

wordDocument.ChartToImageConverter.ScalingMode = ScalingMode.Normal

'creates an instance of the DocToPDFConverter - responsible for Word to PDF conversion

Dim converter As New DocToPDFConverter()

' Sets true to enable the fast rendering using direct PDF conversion.
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

### Embedding fonts

You can customize the TrueType fonts embedding in two ways as follows:

#### Embed Fonts

This setting allows you to embed the particular font information (glyphs) from the TrueType fonts used for the rendered characters in converted PDF document.

The following code sample shows how to embed the TrueType fonts into the converted PDF document.

{% tabs %}
{% highlight c# %}
//Loads an existing Word document

WordDocument wordDocument = new WordDocument("Sample.docx", FormatType.Docx);

//Initializes the ChartToImageConverter for converting charts during Word to pdf conversion

wordDocument.ChartToImageConverter = new ChartToImageConverter();

//Sets the scaling mode for charts (Normal mode reduces the Pdf file size)

wordDocument.ChartToImageConverter.ScalingMode = ScalingMode.Normal;

//Creates an instance of the DocToPDFConverter - responsible for Word to PDF conversion

DocToPDFConverter converter = new DocToPDFConverter();

// Sets true to embed TrueType fonts

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

Dim wordDocument As New WordDocument("Sample.docx", FormatType.Docx)

'Initializes the ChartToImageConverter for converting charts during Word to pdf conversion

wordDocument.ChartToImageConverter = New ChartToImageConverter()

'Sets the scaling mode for charts (Normal mode reduces the Pdf file size)

wordDocument.ChartToImageConverter.ScalingMode = ScalingMode.Normal

'creates an instance of the DocToPDFConverter - responsible for Word to PDF conversion

Dim converter As New DocToPDFConverter()

' Sets true to embed TrueType fonts 

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

#### Embed Complete Fonts

This setting allows you to embed the complete font information (glyphs) from the TrueType fonts used in converted PDF document.

The following code sample shows how to embed the complete TrueType fonts into the converted PDF document.

{% tabs %}
{% highlight c# %}
//Loads an existing Word document

WordDocument wordDocument = new WordDocument("Sample.docx", FormatType.Docx);

//Initializes the ChartToImageConverter for converting charts during Word to pdf conversion

wordDocument.ChartToImageConverter = new ChartToImageConverter();

//Sets the scaling mode for charts (Normal mode reduces the Pdf file size)

wordDocument.ChartToImageConverter.ScalingMode = ScalingMode.Normal;

//Creates an instance of the DocToPDFConverter - responsible for Word to PDF conversion

DocToPDFConverter converter = new DocToPDFConverter();

// Sets true to embed complete TrueType fonts

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

Dim wordDocument As New WordDocument("Sample.docx", FormatType.Docx)

'Initializes the ChartToImageConverter for converting charts during Word to pdf conversion

wordDocument.ChartToImageConverter = New ChartToImageConverter()

'Sets the scaling mode for charts (Normal mode reduces the Pdf file size)

wordDocument.ChartToImageConverter.ScalingMode = ScalingMode.Normal

'creates an instance of the DocToPDFConverter - responsible for Word to PDF conversion

Dim converter As New DocToPDFConverter()

' Sets true to embed complete TrueType fonts 

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

### Image quality 

This setting allows you to determine the quality of the charts and JPEG images in the converted PDF document.

The following code sample shows how to customize the image quality of charts and JPEG images in the converted PDF document.

{% tabs %}
{% highlight c# %}
//Loads an existing Word document

WordDocument wordDocument = new WordDocument("Sample.docx", FormatType.Docx);

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

Dim wordDocument As New WordDocument("Sample.docx", FormatType.Docx)

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

### Identical image optimization 

This setting reduces the Main Memory usage in Word to PDF conversion by reusing the identical images.

The following code sample shows how to reduce the Main Memory usage while converting Word to PDF by reusing the identical images.

{% tabs %}
{% highlight c# %}
//Loads an existing Word document

WordDocument wordDocument = new WordDocument("Sample.docx", FormatType.Docx);

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

Dim wordDocument As New WordDocument("Sample.docx", FormatType.Docx)

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

### PDF Conformance Level

This setting allows you to set the PDF conformance level.

The following code sample shows how to set the PdfConformanceLevel while converting Word to PDF.

{% tabs %}
{% highlight c# %}
//Loads an existing Word document

WordDocument wordDocument = new WordDocument("Sample.docx", FormatType.Docx);

//Initializes the ChartToImageConverter for converting charts during Word to pdf conversion

wordDocument.ChartToImageConverter = new ChartToImageConverter();

//Sets the scaling mode for charts (Normal mode reduces the Pdf file size)

wordDocument.ChartToImageConverter.ScalingMode = ScalingMode.Normal;

//Creates an instance of the DocToPDFConverter - responsible for Word to PDF conversion

DocToPDFConverter converter = new DocToPDFConverter();

// Set the conformance for PDF/A-1b conversion.

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

Dim wordDocument As New WordDocument("Sample.docx", FormatType.Docx)

'Initializes the ChartToImageConverter for converting charts during Word to pdf conversion

wordDocument.ChartToImageConverter = New ChartToImageConverter()

'Sets the scaling mode for charts (Normal mode reduces the Pdf file size)

wordDocument.ChartToImageConverter.ScalingMode = ScalingMode.Normal

'creates an instance of the DocToPDFConverter - responsible for Word to PDF conversion

Dim converter As New DocToPDFConverter()

' Set the conformance for PDF/A-1b conversion.

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

### Enable Alternate Chunks

This setting allows you to include the alternate chunks while converting Word to PDF conversion. As default, it includes alternate chunks.

The following code sample shows how to exclude the alternate chunk parts in Word to PDF conversion.

{% tabs %}
{% highlight c# %}
//Loads an existing Word document

WordDocument wordDocument = new WordDocument("Sample.docx", FormatType.Docx);

//Initializes the ChartToImageConverter for converting charts during Word to pdf conversion

wordDocument.ChartToImageConverter = new ChartToImageConverter();

//Sets the scaling mode for charts (Normal mode reduces the Pdf file size)

wordDocument.ChartToImageConverter.ScalingMode = ScalingMode.Normal;

//Creates an instance of the DocToPDFConverter - responsible for Word to PDF conversion

DocToPDFConverter converter = new DocToPDFConverter();

// Sets false to disable converting the alternate chunks present in Word document to PDF.

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

Dim wordDocument As New WordDocument("Sample.docx", FormatType.Docx)

'Initializes the ChartToImageConverter for converting charts during Word to pdf conversion

wordDocument.ChartToImageConverter = New ChartToImageConverter()

'Sets the scaling mode for charts (Normal mode reduces the Pdf file size)

wordDocument.ChartToImageConverter.ScalingMode = ScalingMode.Normal

'creates an instance of the DocToPDFConverter - responsible for Word to PDF conversion

Dim converter As New DocToPDFConverter()

' Sets false to disable converting the alternate chunks present in Word document to PDF.

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


N> 1. Word to PDF conversion is not supported in Silverlight, Windows Phone, WinRT, and Universal applications.
N> 2. Creating an instance of ChartToImageConverter class is mandatory to convert the charts present in the Word to PDF. Otherwise, the charts are not preserved in the converted PDF.
N> 3. The ChartToImageConverter is supported from .NET Framework 4.0 onwards.
N> 4. Total number of pages in the converted PDF may vary based on unsupported elements in the input Word document.

## Unsupported elements in Word to PDF conversion

The following table shows the unsupported elements of Word to PDF conversion.

<table>
<tr>
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
Custom Shapes and Grouped Shapes
</td>
<td>
Not supported
</td>
</tr>
<tr>
<td>
Embedded fonts
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
Hyphenation
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
Track changes
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
Line and Section Number
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
Image cropping
</td>
<td>
Only DOCX and WordML format documents are supported.
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
</table>
