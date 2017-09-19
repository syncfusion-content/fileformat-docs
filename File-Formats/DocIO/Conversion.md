---
title: Conversion
description: This section illustrates how to convert a Word document into other supported file formats
platform: file-formats
control: DocIO
documentation: UG
---
# Conversion

## Converting Word document to PDF

Essential DocIO allows you to convert a Word document into PDF with a few lines of code. For converting a Word document to PDF, the following assemblies are required to be referred in your application.

<table>
<thead>
<tr>
<th>Assembly Name<br/><br/></th>
<th>Description<br/><br/></th>
</tr>
</thead>
<tbody>
<tr>
<td>
Syncfusion.DocIO.Base<br/><br/></td><td>
This assembly has the core features for creating and manipulating Word documents.<br/><br/></td></tr>
<tr>
<td>
Syncfusion.Compression.Base<br/><br/></td><td>
This assembly is used to package the Word documents<br/><br/></td></tr>
<tr>
<td>
Syncfusion.DocToPdfConverter.Base<br/><br/></td><td>
This assembly is needed for converting the Word document to PDF.<br/><br/></td></tr>
<tr>
<td>
Syncfusion.Pdf.Base<br/><br/></td><td>
This assembly has the core features for creating PDF file.<br/><br/></td></tr>
<tr>
<td>
Syncfusion.OfficeChart.Base<br/><br/></td><td>
This assembly has features to work with chart in Word document.<br/><br/></td></tr>
</tbody>
</table>
The following assemblies are required to be referred in addition to the above mentioned assemblies for converting the chart present in the Word document into PDF.

<table>
<thead>  
<tr>
<th>Assembly Name<br/><br/></th>
<th>Description<br/><br/></th></tr>
</thead>
<tbody> 
<tr>
<td>
Syncfusion.OfficeChartToImageConverter.WPF<br/><br/></td><td>
This assembly is used to convert the chart to image.<br/><br/></td></tr>
<tr>
<td>
Syncfusion.SfChart.WPF<br/><br/></td><td>
This is supporting assembly for Syncfusion.OfficeChartToImageConverter.WPF<br/><br/></td></tr>
 </tbody>
</table>


The following namespaces are required to compile the code in this topic.

* using Syncfusion.OfficeChart
* using Syncfusion.DocIO
* using Syncfusion.DocIO.DLS
* using Syncfusion.DocToPDFConverter
* using Syncfusion.Pdf
* using Syncfusion.OfficeChartToImageConverter

`DocToPDFConverter` class is responsible for converting a Word document into PDF. The following code example illustrates how to convert a Word document into PDF document.

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

 {% endtabs %}  

N> 1. Word to PDF conversion is not supported in Silverlight, Windows Phone, WinRT, Universal, Xamarin, Azure Web Service, Azure APP Service, ASP.NET Core and Universal Windows applications.
N> 2. Creating an instance of `ChartToImageConverter` class is mandatory to convert the charts present in the Word document to PDF. Otherwise, the charts are not preserved in the converted PDF.
N> 3. `ChartToImageConverter` is supported from .NET Framework 4.0 onwards.
N> 4. Total number of pages in the converted PDF may vary based on unsupported elements in the input Word document.



### Customizing the Word document to PDF conversion

Essential DocIO allows you to customize the Word to PDF conversion with the following options:

* Allows to embed the TrueType fonts used in the converted PDF
* Allows to determine the quality of the charts in the converted PDF 
* Allows to determine the quality of the JPEG images in the converted PDF
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

 
 
### Unsupported elements and Limitations in Word to PDF conversion:

<table>
<thead> 
<tr>
<th>Element</th>
<th>Limitations or Unsupported elements</th>
</tr>
 </thead>
  <tbody> 
<tr>
<td>
Predefined shapes<br/><br/></td><td>
Only DOCX and WordML format documents are supported<br/><br/></td></tr>
<tr>
<td>
Chart<br/><br/></td><td>
Only DOCX and WordML format documents are supported and it supported from .NET Framework 4.0 onwards<br/><br/></td></tr>
<tr>
<td>
List - Bulleted, Numbered and Multi-level lists<br/><br/></td><td>
The image bullets preserved in the  document may be replaced by the disc style bullet.<br/><br/></td></tr>
<tr>
<td>
Table Styles<br/><br/></td><td>
Only DOCX and WordML format documents are supported<br/><br/></td></tr>
<tr>
<td>
Underline<br/><br/></td><td>
Single underline style only supported<br/><br/></td></tr>
<tr>
<td>
Pagination<br/><br/></td><td>
Essential DocIO makes sensible decision while layout the text, and its supported elements while generating the PDF documents. But however, there may not be guaranteed pagination with all the documents<br/><br/></td></tr>
<tr>
<td>
Custom Shapes and Grouped Shapes<br/><br/></td><td>
Not supported<br/><br/></td></tr>
<tr>
<td>
Embedded fonts<br/><br/></td><td>
Not supported<br/><br/></td></tr>
<tr>
<td>
Rotation – predefined shape<br/><br/></td><td>
Not supported<br/><br/></td></tr>
<tr>
<td>
Fit Text – Table cell<br/><br/></td><td>
Not supported<br/><br/></td></tr>
<tr>
<td>
Allow AutoFit<br/><br/></td><td>
Not supported<br/><br/></td></tr>
<tr>
<td>
Hyphenation<br/><br/></td><td>
Not supported<br/><br/></td></tr>
<tr>
<td>
Comments<br/><br/></td><td>
Not supported<br/><br/></td></tr>
<tr>
<td>
Vertical Alignment of the section<br/><br/></td><td>
Not supported<br/><br/></td></tr>
<tr>
<td>
Equation<br/><br/></td><td>
Not supported<br/><br/></td></tr>
<tr>
<td>
Track changes<br/><br/></td><td>
Not supported<br/><br/></td></tr>
<tr>
<td>
SmartArt<br/><br/></td><td>
Not supported<br/><br/></td></tr>
<tr>
<td>
WordArt<br/><br/></td><td>
Not supported<br/><br/></td></tr>
<tr>
<td>
Line and Section number<br/><br/></td><td>
Not supported<br/><br/></td></tr>
<tr>
<td>
Watermark<br/><br/></td><td>
First watermark of the Word document should be applied to the entire converted PDF document when the Word document have multiple watermarks.<br/><br/></td></tr>
<tr>
<td>
Multi-Column Texts<br/><br/></td><td>
Multi-Column text positions are calculated dynamically while layout the text. So there may be some content position differences that occur in the PDF document.<br/><br/></td></tr>
<tr>
<td>
Borders<br/><br/></td><td>
Using of patterns and 3D borders are not retained in the output PDF document<br/><br/></td></tr>
<tr>
<td>
Break – Page break, column break and Line break<br/><br/></td><td>
Text wrapping break is not supported<br/><br/></td></tr>
<tr>
<td>
Footnote and endnote<br/><br/></td><td>
Number formats in Roman, Alphabets and Arabic only supported<br/><br/></td></tr>
<tr>
<td>
Image cropping<br/><br/></td><td>
Only DOCX and WordML format documents are supported<br/><br/></td></tr>
<tr>
<td>
Textbox<br/><br/></td><td>
Linked text boxes are not supported<br/><br/></td></tr>
 </tbody>
</table>


## Rendering / Converting Word document to Image

Essential DocIO supports to convert the Word document to images using `RenderAsImages` method. The following assemblies are need to be referred for converting Word to image.

<table>
<thead> 
<tr>
<th> Assembly Name </th>
<th> Description </th>
</tr>
 </thead>
<tbody> 
<tr>
<td>
Syncfusion.DocIO.Base<br/><br/></td><td>
This assembly has the core features for creating and manipulating Word documents.<br/><br/></td></tr>
<tr>
<td>
Syncfusion.Compression.Base<br/><br/></td><td>
This assembly is used to package the Word documents<br/><br/></td></tr>
<tr>
<td>
Syncfusion.OfficeChart.Base<br/><br/></td><td>
This assembly has features to work with chart in Word document.<br/><br/></td></tr>
 </tbody>
</table>

The following assemblies are need to be referred additionally for converting charts during Word to image conversion:

<table>
<thead>  
<tr>
<th> Assembly Name<br/><br/></th>
<th> Description<br/><br/></th>
</tr>
</thead>
<tbody>  
<tr>
<td>
Syncfusion.OfficeChartToImageConverter.WPF<br/><br/></td><td>
This assembly is used to convert the chart to image.<br/><br/></td></tr>
<tr>
<td>
Syncfusion.SfChart.WPF<br/><br/></td><td>
This is supporting assembly for Syncfusion.OfficeChartToImageConverter.WPF<br/><br/></td></tr>
</tbody>
</table>


The following namespaces are required to compile the code in this topic. 

* using Syncfusion.DocIO
* using Syncfusion.DocIO.DLS
* using Syncfusion.OfficeChart
* using Syncfusion.OfficeChartToImageConverter

T> You can get the converted images in good quality by specifying the image type as Metafile.
T> You can specify the quality of the converted charts by setting the scaling mode.

The following code illustrates how to convert the Word document to image.

{% tabs %}  

{% highlight c# %}


//Loads an existing Word document

WordDocument wordDocument = new WordDocument("Template.docx", FormatType.Docx);

//Initializes the ChartToImageConverter for converting charts during Word to image conversion

wordDocument.ChartToImageConverter = new ChartToImageConverter();

//Sets the scaling mode for charts (Normal mode reduces the file size)

wordDocument.ChartToImageConverter.ScalingMode = ScalingMode.Normal;

//Converts word document to image

Image[] images = wordDocument.RenderAsImages(ImageType.Bitmap);

int i = 0;

foreach (Image image in images)

{

//Saves the images as jpeg

image.Save("WordToImage_" + i + ".jpeg", ImageFormat.Jpeg);

i++;

}

//Closes the document

wordDocument.Close();



{% endhighlight %}



{% highlight vb.net %}


'Loads an existing Word document

Dim wordDocument As New WordDocument("Template.docx", FormatType.Docx)

'Initializes the ChartToImageConverter for converting charts during Word to image conversion

wordDocument.ChartToImageConverter = New ChartToImageConverter()

'Sets the scaling mode for charts (Normal mode reduces the file size)

wordDocument.ChartToImageConverter.ScalingMode = ScalingMode.Normal

'Converts word document to image

Dim images As Image() = wordDocument.RenderAsImages(ImageType.Bitmap)

Dim i As Integer = 0

For Each image As Image In images

'Saves the images as jpeg

image.Save("WordToImage_" & i & ".jpeg", ImageFormat.Jpeg)

i += 1

Next

'Closes the document

wordDocument.Close()

{% endhighlight %} 

 {% endtabs %}  

N> 1. Word to Image conversion is not supported in Silverlight, Windows Phone, WinRT, Universal, Xamarin, Azure Web Service, Azure APP Service, ASP.NET Core and Universal Windows applications.
N> 2. Creating an instance of `ChartToImageConverter` class is mandatory to convert the charts present in the Word document to Image. Otherwise, the charts are not preserved in the generated image.
N> 3. `ChartToImageConverter` is supported from .NET Framework 4.0 onwards.
N> 4. Total number of images may vary based on unsupported elements in the input Word document.
N> 5. Word to Image conversion has the same limitations and unsupported elements of Word to PDF conversion.

## RTF conversion 

Essential DocIO supports to convert the RTF document into Word document and vice versa. The following code shows how to convert RTF document into Word document.

{% tabs %} 

{% highlight c# %}

//Loads an existing document

WordDocument document = new WordDocument("Sample.rtf", FormatType.Rtf);

//Saves the Word document as RTF file

document.Save("RtfToWord.docx", FormatType.Docx);

//Closes the document

document.Close();



{% endhighlight %}



{% highlight vb.net %}


'Loads an existing document

Dim document As New WordDocument("Sample.rtf", FormatType.Rtf)

'Saves the Word document as RTF file

document.Save("RtfToWord.docx", FormatType.Docx)

'Closes the document

document.Close()

{% endhighlight %} 

  {% endtabs %}  

The following code example shows how to convert Word document into RTF document 

{% tabs %}  

{% highlight c# %}


//Loads an existing document

WordDocument document = new WordDocument("Template.docx", FormatType.Docx);

//Saves the Word document as RTF file

document.Save("WordToRtf.rtf", FormatType.Rtf);

//Closes the document

document.Close();



{% endhighlight %}

{% highlight vb.net %}


'Loads an existing document

Dim document As New WordDocument("Template.docx", FormatType.Docx)

'Saves the Word document as RTF file

document.Save("WordToRtf.rtf", FormatType.Rtf)

'Closes the document

document.Close()

{% endhighlight %}

  {% endtabs %}  

## HTML conversion

Essential DocIO supports converting the HTML file into Word document and vice versa. It supports only the HTML files that meet the validation either against XHTML 1.0 strict or XHTML 1.0 Transitional schema. 

The following code example shows how to convert the HTML file into Word document. 

{% tabs %}   

{% highlight c# %}


//Loads the HTML document against transitional schema validation

WordDocument document = new WordDocument("Sample.html", FormatType.Html, XHTMLValidationType.Transitional);

//Saves the Word document

document.Save("HTMLtoWord.docx", FormatType.Docx);

//Closes the document

document.Close();



{% endhighlight %}

{% highlight vb.net %}


' Loads the HTML document against transitional schema validation 

Dim document As New WordDocument("Sample.html", FormatType.Html, XHTMLValidationType.Transitional)

'Saves the Word document

document.Save("HTMLtoWord.docx", FormatType.Docx)

'Closes the document

document.Close()

{% endhighlight %} 

 {% endtabs %} 

### Customizing the HTML to Word conversion

You can customize the HTML to Word conversion with the following options:

* Validate the HTML string against XHTML 1.0 Strict and Transitional schema
* Insert the HTML string at the specified position of the document body contents
* Append HTML string to the specified paragraph

The following Code example shows how to customize the HTML to Word conversion.

{% tabs %}  

{% highlight c# %}


//Loads the template document

WordDocument document = new WordDocument("Template.docx");

//Html string to be inserted

string htmlstring = "<p><b>This text is inserted as HTML string.</b></p>";

//Validates the Html string

bool isValidHtml = document.LastSection.Body.IsValidXHTML(htmlstring, XHTMLValidationType.Transitional);

//When the Html string passes validation, it is inserted to the document

if (isValidHtml)

{

//Appends Html string as first item of the second paragraph in the document

document.Sections[0].Body.InsertXHTML(htmlstring, 2, 0);

//Appends the Html string to first paragraph in the document

document.Sections[0].Body.Paragraphs[0].AppendHTML(htmlstring);

}

//Saves and closes the document

document.Save("Sample.docx");

document.Close();



{% endhighlight %}

{% highlight vb.net %}


'Loads the template document

Dim document As New WordDocument("Template.docx")

'Html string to be inserted

Dim htmlstring As String = "<p><b>This text is inserted as HTML string.</b></p>"

'Validates the Html string

Dim isValidHtmlAs Boolean = document.LastSection.Body.IsValidXHTML(htmlstring, XHTMLValidationType.Transitional)

'When the Html string passes validation, it is inserted to document

If isValidHtmlThen

'Appends Html string as first item of the second paragraph in the document

document.Sections(0).Body.InsertXHTML(htmlstring, 2, 0)

'Appends the Html string to first paragraph in the document

document.Sections(0).Body.Paragraphs(0).AppendHTML(htmlstring)

End If

'Saves and closes the document

document.Save("Sample.docx")

document.Close()

{% endhighlight %}

  {% endtabs %}  

N> 1. Inserting XHTML string is not supported in Silverlight, Windows Phone and Xamarin applications.
N> 2. XHTML validation against XHTML 1.0 Strict and Transitional schema is not supported in Windows Store applications.
N> 3. XHTMLValidationType.Transitional - default validation while importing HTML file.
N> 4. XHTMLValidationType.None - validate the HTML file against XHTML format and it doesn’t perform any schema validation.



The following code example shows how to convert the Word document into HTML.

{% tabs %}  

{% highlight c# %}

//Loads the template document

WordDocument document = new WordDocument("Template.docx", FormatType.Docx);

//Saves the document as Html file

document.Save("WordToHtml.html", FormatType.Html);

//Closes the document 

document.Close();

{% endhighlight %}

{% highlight vb.net %}


'Loads the template document

Dim document As New WordDocument("Template.docx", FormatType.Docx)

'Saves the document as Html file

document.Save("WordToHtml.html", FormatType.Html)

'Closes the document 

document.Close()

{% endhighlight %}

  {% endtabs %}  

### Customizing the Word to HTML conversion

You can customize the Word to HTML conversion with the following options:

* Extract the images used in the HTML document at the specified file directory 
* Specify to export the header and footer of the Word document in the HTML 
* Specify to consider Text Input field as a editable fields or text 
* Specify the CSS style sheet type and its name

N> 
While exporting header and footer, DocIO exports the first section header content at the top of the HTML file and first section footer content at the end of the HTML file

The following code example shows how to customize Word to HTML conversion.

{% tabs %} 

{% highlight c# %}


//Loads an existing document

WordDocument document = new WordDocument("Template.docx");

HTMLExport export = new HTMLExport();

//The images in the input document are copied to this folder

document.SaveOptions.HtmlExportImagesFolder = @"D:\Data\";

//The headers and footers in the input are exported

document.SaveOptions.HtmlExportHeadersFooters = true;

//Exports the text form fields as editable

document.SaveOptions.HtmlExportTextInputFormFieldAsText = false;

//Sets the style sheet type

document.SaveOptions.HtmlExportCssStyleSheetType = CssStyleSheetType.External;

//Sets name for style sheet

document.SaveOptions.HtmlExportCssStyleSheetFileName = "UserDefinedFileName.css";

//Saves the document as html file

export.SaveAsXhtml(document, "WordtoHtml.html");

document.Close();



{% endhighlight %}

{% highlight vb.net %}


'Loads an existing document

Dim document As New WordDocument("Template.docx")

Dim export As New HTMLExport()

'The images in the input document are copied to this folder

document.SaveOptions.HtmlExportImagesFolder = "D:\Data\"

'The headers and footers in the input are exported

document.SaveOptions.HtmlExportHeadersFooters = True

'Exports the text form fields as editable

document.SaveOptions.HtmlExportTextInputFormFieldAsText = False

'Sets the style sheet type

document.SaveOptions.HtmlExportCssStyleSheetType = CssStyleSheetType.External

'Sets name for style sheet

document.SaveOptions.HtmlExportCssStyleSheetFileName = "UserDefinedFileName.css"

'Saves the document as html file

export.SaveAsXhtml(document, "WordtoHtml.html")

document.Close()

{% endhighlight %} 

  {% endtabs %}  

### Supported Document elements

The following document elements and attributes are supported by DocIO in Word to HTML and HTML to Word conversions.

<table>
<thead>  
<tr>
<th> Document Element </th>
<th> Attribute </th>
<th> Support Status </th>
<th> Notes </th>
</tr>
</thead>
<tbody>  
<tr>
<td>
Bookmark<br/><br/></td><td>
Id<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
Border<br/><br/><br/><br/></td><td>
Color<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Distance from text<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Line style<br/><br/></td><td>
Partial<br/><br/></td><td>
Some line styles are rendered as solid.<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Line width<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
Document Properties<br/><br/></td><td>
<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
Field<br/><br/></td><td>
<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
Footnotes and Endnotes<br/><br/></td><td>
<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
Form Field<br/><br/></td><td>
Text input, Checkbox and combo box<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
Header / Footer<br/><br/></td><td>
Different per section<br/><br/></td><td>
Partial<br/><br/></td><td>
Only odd header of the first section is preserved in HTML export.<br/><br/></td></tr>
<tr>
<td>
Hyperlink<br/><br/></td><td>
External URL<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Local<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
Image<br/><br/></td><td>
Inline<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Scale<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
List<br/><br/></td><td>
Custom bullets<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Multi-level<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Numbered<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Restart numbering<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Standard bullets<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
Comment<br/><br/></td><td>
<br/><br/></td><td>
No<br/><br/></td><td>
<br/><br/></td></tr>
<tr>
<td>
Symbols<br/><br/></td><td>
<br/><br/></td><td>
Yes<br/><br/></td><td>
<br/><br/></td></tr>
<tr>
<td>
Paragraph<br/><br/></td><td>
Alignment<br/><br/></td><td>
Yes<br/><br/></td><td>
<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Borders<br/><br/></td><td>
Yes<br/><br/></td><td>
See Borders, for more details.<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Keep lines and paragraphs together<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Paragraph Indents<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Line spacing<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Page break before<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Shading<br/><br/></td><td>
Yes<br/><br/></td><td>
See Shading, for more details.<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Spacing before and after<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
Shading<br/><br/><br/><br/></td><td>
Background color<br/><br/></td><td>
Partial<br/><br/></td><td>
Solid background colors are supported.<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Foreground color<br/><br/></td><td>
Partial<br/><br/></td><td>
Solid foreground color is used when background color is auto.<br/><br/></td></tr>
<tr>
<td>
Styles<br/><br/><br/><br/></td><td>
Paragraph styles<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Character styles<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
List styles<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
Table<br/><br/><br/><br/></td><td>
Alignment<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Cell margins<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Column widths<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Indent from left<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Preferred width<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Spacing between cells<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Borders<br/><br/></td><td>
Partial<br/><br/></td><td>
See Borders, for more details.<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Shading<br/><br/></td><td>
Partial<br/><br/></td><td>
See Shading, for more details.<br/><br/></td></tr>
<tr>
<td>
Nested Table<br/><br/></td><td>
<br/><br/></td><td>
Yes<br/><br/></td><td>
<br/><br/></td></tr>
<tr>
<td>
Table Cell<br/><br/><br/><br/></td><td>
Borders<br/><br/></td><td>
Partial<br/><br/></td><td>
See Borders, for more details.<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Cell margins<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Horizontal merge<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Shading<br/><br/></td><td>
Partial<br/><br/></td><td>
See Shading, for more details.<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Vertical alignment<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Vertical merge<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
Table Row<br/><br/></td><td>
Height<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Padding<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
Text<br/><br/><br/><br/></td><td>
All caps<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Bold<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Character spacing<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Color<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Emboss<br/><br/></td><td>
Partial<br/><br/></td><td>
Rendered as bold.<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Engrave<br/><br/></td><td>
Partial<br/><br/></td><td>
Rendered as bold.<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Font<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Hidden<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Highlighting<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Imprint<br/><br/></td><td>
Partial<br/><br/></td><td>
Rendered as bold.<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Italic<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Line breaks<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Outline<br/><br/></td><td>
Partial<br/><br/></td><td>
Rendered as bold.<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Page breaks<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Shading<br/><br/></td><td>
Partial<br/><br/></td><td>
See Shading, for more details.<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Small caps<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Special symbols<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Strike out<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Subscript / Superscript<br/><br/></td><td>
Yes<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
<br/><br/></td><td>
Underline<br/><br/></td><td>
Partial<br/><br/></td><td>
Underline types and colors are ignored.<br/><br/></td></tr>
</tbody>
</table>


## Text file

Essential DocIO supports to convert the Word document into Text file and vice versa. The following code example shows how to convert the Word document into text file.


{% tabs %}  

{% highlight c# %}


//Loads a template document

WordDocument document = new WordDocument("Template.docx");

//Saves the document as text file

document.Save("WordToText.txt", FormatType.Txt);

//Closes the document

document.Close();



{% endhighlight %}

{% highlight vb.net %}

'Loads a text file

Dim document As New WordDocument("Template.docx")

'Saves the document as text file

document.Save("WordToText.txt", FormatType.Txt)

'Closes the document

document.Close()

{% endhighlight %} 

 {% endtabs %}  

The following code example shows how to convert a Text file into Word document. 

{% tabs %}  

{% highlight c# %}


//Loads a text file

WordDocument document = new WordDocument("Template.txt");

//Saves the document as text file

document.Save("TextToWord.docx", FormatType.Docx);

//Closes the document

document.Close();



{% endhighlight %}

{% highlight vb.net %}

'Loads a text file

Dim document As New WordDocument("Template.txt")

'Saves the document as text file

document.Save("TextToWord.docx", FormatType.Docx)

'Closes the document

document.Close()

{% endhighlight %} 

{% endtabs %}  

The following code example shows how to retrieve the Word document contents as a plain text.

{% tabs %} 

{% highlight c# %}

//Loads a template document

WordDocument document = new WordDocument("Template.docx");

//Gets the document text

string text = document.GetText();

//Creates new Word document

WordDocument newdocument = new WordDocument();

//Adds new section

IWSection section = newdocument.AddSection();

//Adds new paragraph

IWParagraph paragraph = section.AddParagraph();

//Appends the text to the paragraph

paragraph.AppendText(text);

//Saves and closes the document

newdocument.Save("Sample.docx");

newdocument.Close();

document.Close();



{% endhighlight %}

{% highlight vb.net %}

'Loads a template document

Dim document As New WordDocument("Template.docx")

'Gets the document text

Dim text As String = document.GetText()

'Creates new Word document

Dim newdocument As New WordDocument()

'Adds new section

Dim section As IWSection = newdocument.AddSection()

'Adds new paragraph

Dim paragraph As IWParagraph = section.AddParagraph()

'Appends the text to the paragraph

paragraph.AppendText(text)

'Saves and closes the document

newdocument.Save("Sample.docx")

newdocument.Close()

document.Close()

{% endhighlight %} 

  {% endtabs %}  

  
## Word to EPUB

Essential DocIO supports to convert the Word document into EPUB v2.0. It only supports in Windows Forms, UWP, WPF, ASP.NET Web and MVC platforms. The following elements are supported in Word to EPUB conversion.

* Text and Paragraph Formatting
* Lists
* Tables
* Images
* Footnote
* Hyperlink
* Styles
* Table of Contents
* Document Properties

The following code illustrates how to convert the Word document to EPUB file.

{% tabs %}  

{% highlight c# %}


//Loads an existing document

WordDocument document = new WordDocument("Template.docx", FormatType.Docx);

//Exports the fonts used in the document

document.SaveOptions.EPubExportFont = true;

//Exports header and footer

document.SaveOptions.HtmlExportHeadersFooters = true;

//Saves the document as EPub file

document.Save("WordToEPub.epub", FormatType.EPub);

//Closes the document

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Loads an existing document

Dim document As New WordDocument("Template.docx", FormatType.Docx)

'Exports the fonts used in the document

document.SaveOptions.EPubExportFont = True

'Exports header and footer

document.SaveOptions.HtmlExportHeadersFooters = True

'Saves the document as EPub file

document.Save("WordToEPub.epub", FormatType.EPub)

'Closes the document

document.Close()



{% endhighlight %}

{% endtabs %}  