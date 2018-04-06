# Converting Word document to EPUB.
The Word document files are convert as EPUB v2.0 file format with few lines of code by using Essential DocIO. It only supports in Windows Forms, UWP, WPF, ASP.NET Web and MVC platforms.
The following code illustrates how to convert the Word document to EPUB file.
C#:
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
{% endtabs %}
VB:
{% tabs %}
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
The following elements are supported in Word to EPUB conversion.
* Text and Paragraph Formatting
* Lists
* Tables
* Images
* Footnote
* Hyperlink
* Styles
* Table of Contents
* Document Properties
