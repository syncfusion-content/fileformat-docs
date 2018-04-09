---
title: Word document to PDF Conversion
description: Converting Word document to PDF using DocIO
platform: file-formats
control: DocIO
documentation: UG
---

# Word document to PDF Conversion

## Converting Word document to PDF

The Word document files are converted as a PDF document with a few lines of code by using Essential DocIO. It works perfectly when you create an input Word document from scratch or load an existing Word document and then easily convert them into PDF. 

Kindly refer the following links for assemblies required based on platforms to convert the word document to PDF.

* [Assemblies required](https://help.syncfusion.com/file-formats/docio/assemblies-required#converting-word-document-to-pdf) 
* [NuGet details](https://help.syncfusion.com/file-formats/docio/assemblies-required#converting-word-document-to-pdf)

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

{% highlight .netcore %}
//Creates an instance of WordDocument Instance (Empty Word Document)
WordDocument wordDocument = new WordDocument();
//Add a section & a paragraph in the empty document
wordDocument.EnsureMinimal();
//Append text to the last paragraph of the document
wordDocument.LastParagraph.Text = "Adventure Works Cycles, the fictitious company on which the" +
    " AdventureWorks sample databases are based, is a large, multinational manufacturing company. ";
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
{:data-downloadable="true" data-href="http://www.syncfusion.com/downloads/support/directtrac/general/ze/WordToPDFInCore304848517"}

{% highlight xamarin %}
private void OnButtonClicked(object sender, EventArgs e)
{
//Creates an instance of WordDocument Instance (Empty Word Document)
WordDocument wordDocument = new WordDocument();
//Add a section & a paragraph in the empty document
wordDocument.EnsureMinimal();
//Append text to the last paragraph of the document
wordDocument.LastParagraph.Text = "Adventure Works Cycles, the fictitious company on which the" +
    " AdventureWorks sample databases are based, is a large, multinational manufacturing company. ";
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
{:data-downloadable="true" data-href="http://www.syncfusion.com/downloads/support/directtrac/general/ze/WordToPDFInXForms2106135379"}
{% endtabs %}


## Word to PDF conversion in Linux OS
In Linux OS, we can perform the Word document to PDF conversion using .NET Core application. To deploy .NET Core application with Word to PDF conversion capabilities in Linux OS, Kindly refer the KB from [here](https://www.syncfusion.com/kb/8470#).

## Customization settings:
Essential DocIO provides special options while performing Word to PDF conversion mentioned below, 

* Allows to convert PDF faster by using direct PDF rendering approach. As default, it uses EMF rendering approach.
* Allows to embed the TrueType fonts used in the converted PDF.
* Allows to determine the quality of the charts in the converted PDF.
* Allows to determine the quality of the JPEG images in the converted PDF.
* Allows to reduce the Main Memory usage in Word to PDF conversion by reusing the identical images.

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

//Sets the jpeg image quality to reduce the Pdf file size

converter.Settings.ImageQuality = 100;

//Sets the image resolution

converter.Settings.ImageResolution = 640;

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

'Sets the jpeg image quality to reduce the Pdf file size

converter.Settings.ImageQuality = 100

'Sets the image resolution

converter.Settings.ImageResolution = 640

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

N> 1. Word to PDF conversion is not supported in Silverlight, Windows Phone, WinRT and Universal applications.
N> 2. Creating an instance of ChartToImageConverter class is mandatory to convert the charts present in the Word document to PDF. Otherwise, the charts are not preserved in the converted PDF.
N> 3. ChartToImageConverter is supported from .NET Framework 4.0 onwards.
N> 4. Total number of pages in the converted PDF may vary based on unsupported elements in the input Word document.

## Unsupported elements and Limitations in Word to PDF conversion:
<table>
<tr>
<thead> 
<tr>
<th>Element</th>
<th>Limitations or Unsupported elements</th>
</tr>
</thead>
<tr>
<td>
Predefined shapes
</td>
<td>
Only DOCX and WordML format documents are supported
</td>
</tr>
<tr>
<td>
Chart
</td>
<td>
Only DOCX and WordML format documents are supported and it supported from .NET Framework 4.0 onwards
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
Only DOCX and WordML format documents are supported
</td>
</tr>
<tr>
<td>
Underline
</td>
<td>
Single underline style only supported
</td>
</tr>
<tr>
<td>
Pagination
</td>
<td>
Essential DocIO makes sensible decision while layout the text, and its supported elements while generating the PDF documents. But however, there may not be guaranteed pagination with all the documents
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
Multi-Column text positions are calculated dynamically while layout the text. So, there may be some content position differences that occur in the PDF document.
</td>
</tr>
<tr>
<td>
Borders
</td>
<td>
Using of patterns and 3D borders are not retained in the output PDF document
</td>
</tr>
<tr>
<td>
Break – Page break, column break and Line break
</td>
<td>
Text wrapping break is not supported
</td>
</tr>
<tr>
<td>
Footnote and endnote
</td>
<td>
Number formats in Roman, Alphabets and Arabic only supported
</td>
</tr>
<tr>
<td>
Image cropping
</td>
<td>
Only DOCX and WordML format documents are supported
</td>
</tr>
<tr>
<td>
Textbox
</td>
<td>
Linked text boxes are not supported
</td>
</tr>
</table>
