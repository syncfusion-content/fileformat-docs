---
title: Word Document to HTML conversion | DocIO | Syncfusion
description: Converting Word document to HTML using DocIO
platform: file-formats
control: DocIO
documentation: UG
---

# HTML Conversion

The Essential DocIO converts the HTML file into Word document and vice versa. You can also convert the Word document (DOC, DOCX, RTF, DOT, DOTX, DOCM, and DOTM) into HTML format. It supports only the HTML files that meets the validation either against XHTML 1.0 strict or XHTML 1.0 Transitional schema.

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

{% highlight UWP %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument((assembly.GetManifestResourceStream("CreateWordSample.Assets.Test.html")), FormatType.Html))
{
	MemoryStream stream = new MemoryStream();
	//Saves the Word file to MemoryStream
	await document.SaveAsync(stream, FormatType.Docx);
	//Saves the stream as Word file in local machine
	Save(stream, "Result.docx");
	document.Close();
}
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight ASP.NET CORE %}
FileStream fileStreamPath = new FileStream(@"Data/Hello World.html", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument(fileStreamPath, FormatType.Html))
{
     MemoryStream stream = new MemoryStream();
     document.Save(stream, FormatType.docx);
     //Closes the Word document
     document.Close();
     stream.Position = 0;
     //Download Word document in the browser
     return File(stream, "application/msword", "Result.docx");
}
{% endhighlight %}

{% highlight XAMARIN %}
//DocIO supports HTML conversion in Windows Forms, WPF, ASP.NET, ASP.NET MVC, UWP and ASP.NET CORE platforms alone.
{% endhighlight %}
{% endtabs %}

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

{% highlight UWP %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument((assembly.GetManifestResourceStream("CreateWordSample.Assets.Test.docx")), FormatType.Docx))
{
	MemoryStream stream = new MemoryStream();
	//Saves the Word file to MemoryStream
	await document.SaveAsync(stream, FormatType.Html);
	//Saves the stream as Word file in local machine
	Save(stream, "Result.html");
	document.Close();
}
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight ASP.NET CORE %}
FileStream fileStreamPath = new FileStream(@"Data/Hello World.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx))
{
     MemoryStream stream = new MemoryStream();
     document.Save(stream, FormatType.Html);
     //Closes the Word document
     document.Close();
     stream.Position = 0;
     //Download Word document in the browser
     return File(stream, "application/chrome", "Result.html");
}
{% endhighlight %}

{% highlight XAMARIN %}
//DocIO supports HTML conversion in Windows Forms, WPF, ASP.NET, ASP.NET MVC, UWP and ASP.NET CORE platforms alone.
{% endhighlight %}

{% endtabs %}

## Customization settings

The Essential DocIO provides settings while performing HTML to Word conversion and vice versa.

### Customizing the HTML to Word conversion

The Essential DocIO provides settings while performing HTML to Word conversion as mentioned as follows: 

* Validate the HTML string against XHTML 1.0 Strict and Transitional schema.
* Insert the HTML string at the specified position of the document body contents.
* Append HTML string to the specified paragraph.

The following code example shows how to customize the HTML to Word conversion.

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

N> 1. Inserting XHTML string is not supported in Silverlight, Windows Phone, and Xamarin applications.
N> 2. XHTML validation against XHTML 1.0 Strict and Transitional schema is not supported in Windows Store applications.
N> 3. XHTMLValidationType.Transitional: Default validation while importing HTML file.
N> 4. XHTMLValidationType.None: Validates the HTML file against XHTML format and it doesn’t perform any schema validation.

### Customizing the Word to HTML conversion

You can customize the Word to HTML conversion with the following options:

* Extract the images used in the HTML document at the specified file directory
* Specify to export the header and footer of the Word document in the HTML
* Specify to consider Text Input field as a editable fields or text
* Specify the CSS style sheet type and its name

N> While exporting header and footer, DocIO exports the first section header content at the top of the HTML file and first section footer content at the end of the HTML file.

The following code sample shows how to customize Word to HTML conversion.

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

## Supported and unsupported items

The following document elements and attributes are supported by DocIO in Word to HTML and HTML to Word conversions.

<table>
<thead> 
<tr>
<th>Document Element</th>
<th>Attribute</th>
<th>Support Status</th>
<th>Notes</th>
</tr>
</thead>
<tr>
<td>
Bookmark<br/><br/></td>
<td>
Id<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
Border<br/><br/><br/><br/></td>
<td>
Color<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Distance from text<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Line style<br/><br/></td>
<td>
Partial<br/><br/></td>
<td>
Some line styles are rendered as solid.<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Line width<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
Document Properties<br/><br/></td>
<td>
<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
Field<br/><br/></td>
<td>
<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
Footnotes and Endnotes<br/><br/></td>
<td>
<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
Form Field<br/><br/></td>
<td>
Text input, Checkbox and combo box<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
Header / Footer<br/><br/></td>
<td>
Different per section<br/><br/></td>
<td>
Partial<br/><br/></td>
<td>
Only odd header of the first section is preserved in HTML export.<br/><br/></td>
</tr>
<tr>
<td>
Hyperlink<br/><br/></td>
<td>
External URL<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Local<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
Image<br/><br/></td>
<td>
Inline<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Scale<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
List<br/><br/></td>
<td>
Custom bullets<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Multi-level<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Numbered<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Restart numbering<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Standard bullets<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
Comment<br/><br/></td>
<td>
<br/><br/></td>
<td>
No<br/><br/></td>
<td>
<br/><br/></td>
</tr>
<tr>
<td>
Symbols<br/><br/></td>
<td>
<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
<br/><br/></td>
</tr>
<tr>
<td>
Paragraph<br/><br/></td>
<td>
Alignment<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Borders<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
See Borders, for more details.<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Keep lines and paragraphs together<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Paragraph Indents<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Line spacing<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Page break before<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Shading<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
See Shading, for more details.<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Spacing before and after<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
Shading<br/><br/><br/><br/></td>
<td>
Background color<br/><br/></td>
<td>
Partial<br/><br/></td>
<td>
Solid background colors are supported.<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Foreground color<br/><br/></td>
<td>
Partial<br/><br/></td>
<td>
Solid foreground color is used when background color is auto.<br/><br/></td>
</tr>
<tr>
<td>
Styles<br/><br/><br/><br/></td>
<td>
Paragraph styles<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Character styles<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
List styles<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
Table<br/><br/><br/><br/></td>
<td>
Alignment<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Cell margins<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Column widths<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Indent from left<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Preferred width<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Spacing between cells<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Borders<br/><br/></td>
<td>
Partial<br/><br/></td>
<td>
See Borders, for more details.<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Shading<br/><br/></td>
<td>
Partial<br/><br/></td>
<td>
See Shading, for more details.<br/><br/></td>
</tr>
<tr>
<td>
Nested Table<br/><br/></td>
<td>
<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
<br/><br/></td>
</tr>
<tr>
<td>
Table Cell<br/><br/><br/><br/></td>
<td>
Borders<br/><br/></td>
<td>
Partial<br/><br/></td>
<td>
See Borders, for more details.<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Cell margins<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Horizontal merge<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Shading<br/><br/></td>
<td>
Partial<br/><br/></td>
<td>
See Shading, for more details.<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Vertical alignment<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Vertical merge<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
Table Row<br/><br/></td>
<td>
Height<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Padding<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
Text<br/><br/><br/><br/></td>
<td>
All caps<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Bold<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Character spacing<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Color<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Emboss<br/><br/></td>
<td>
Partial<br/><br/></td>
<td>
Rendered as bold.<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Engrave<br/><br/></td>
<td>
Partial<br/><br/></td>
<td>
Rendered as bold.<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Font<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Hidden<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Highlighting<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Imprint<br/><br/></td>
<td>
Partial<br/><br/></td>
<td>
Rendered as bold.<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Italic<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Line breaks<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Outline<br/><br/></td>
<td>
Partial<br/><br/></td>
<td>
Rendered as bold.<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Page breaks<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Shading<br/><br/></td>
<td>
Partial<br/><br/></td>
<td>
See Shading, for more details.<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Small caps<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Special symbols<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Strike out<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Subscript / Superscript<br/><br/></td>
<td>
Yes<br/><br/></td>
<td>
-<br/><br/></td>
</tr>
<tr>
<td>
<br/><br/></td>
<td>
Underline<br/><br/></td>
<td>
Partial<br/><br/></td>
<td>
Underline types and colors are ignored.
</td>
</tr>
</table>
