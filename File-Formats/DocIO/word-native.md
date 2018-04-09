---
title: Word native conversions
description: Word native conversions supported in DocIO
platform: file-formats
control: DocIO
documentation: UG
---

# Word native conversions
The [Microsoft Word's](https://en.wikipedia.org/wiki/Microsoft_Word#) native file formats are DOC, DOCX, RTF, DOT, DOTX, DOCM, DOTM. Essential DocIO supports 3 major native file formats.
1. Word Open XML formats (2007 & later)
2. Word Binary (97-2003) format (classic)
3. RTF (classic)
**Note:**We recommend you use DOCX file formats since Microsoft corporation stopped their development in DOC file format and new features inclusion, lot of stability improvement will be included in DOCX file format alone. 
## Word Open XML formats (2007 & later)
The XML format introduced in Microsoft Word 2003 was a simple, XML-based format called WordprocessingML or WordML.
[Office Open XML](http://en.wikipedia.org/wiki/Office_Open_XML# "") (OOXML or Microsoft Open XML (MOX)) is a zipped, new XML-based file format introduced by Microsoft in Office 2007 applications. WordprocessingML is the markup language used by Microsoft Office Word to store its DOCX documents.
DocIO supports the following WordprocessingML,
* Microsoft Word 2007
* Microsoft Word 2010
* Microsoft Word 2013
* Microsoft Word 2016
The following code example explains how to create a new Word document with few lines of code
C#:
{% tabs %}
{% highlight c# %}
//Creates an instance of WordDocument Instance (Empty Word Document)

WordDocument document = new WordDocument();

//Add a section & a paragraph in the empty document

document.EnsureMinimal();

//Append text to the last paragraph of the document

document.LastParagraph.AppendText("Hello World");

//Save and close the Word document

document.Save("Result.docx");

document.Close();
{% endhighlight %}
{% endtabs %}
VB:
{% tabs %}
{% highlight vb.net %}
'Creates an instance of WordDocument Instance (Empty Word Document)

Dim document As New WordDocument()

'Add a section & a paragraph in the empty document

document.EnsureMinimal()

'Append text to the last paragraph of the document

document.LastParagraph.AppendText("Hello World")

'Save and close the Word document

document.Save("Result.docx")

document.Close()
{% endhighlight %}
{% endtabs %}
### Word Processing XML conversion(.xml)
Essential DocIO supports converting the Word document into Word Processing XML document and vice versa.
Note:
Currently we support importing for Word Processing 2003 XML documents. Import and export support for Word Processing 2007 XML documents.
The following code example shows how to convert the Word document into Word Processing XML document.
C#
<table>
<tr>
<td>
//Loads an existing Word document
WordDocument document = new WordDocument("Template.docx");
//Saves the document as Word Processing ML document
document.Save("WordToWordML.xml", FormatType.WordML);
//Closes the document
document.Close();
</td>
</tr>
</table>
VB
<table>
<tr>
<td>
'Loads an existing Word document 
Dim document As New WordDocument("Template.docx")
'Saves the document as Word Processing ML document
document.Save("WordToWordML.xml", FormatType.WordML)
'Closes the document
document.Close()
</td>
</tr>
</table>
The following code example shows how to convert the Word Processing XML document into Word document.
C#
<table>
<tr>
<td>
// Loads an existing Word document 
WordDocument document = new WordDocument("Template.xml");
//Saves the Word Processing ML document as docx
document.Save("WordMLToWord.docx", FormatType.Docx);
//Closes the document
document.Close();
</td>
</tr>
</table>
VB
<table>
<tr>
<td>
' Loads an existing Word document 
Dim document As New WordDocument("Template.xml")
'Saves the Word Processing ML document as docx 
document.Save("WordMLToWord.docx", FormatType.Docx)
'Closes the document
document.Close()
</td>
</tr>
</table>
### Unsupported elements and Limitations in Word to Word Processing XML conversion:
<table>
<tr>
<thead>
{{'**Element**'| markdownify }}
</thead>
<thead>
{{'**Limitations or Unsupported elements**'| markdownify }}
</thead>
</tr>
<tr>
<td>
Custom Shapes and Grouped Shapes<br/><br/></td>
<td>
Not supported<br/><br/></td>
</tr>
<tr>
<td>
Embedded fonts<br/><br/></td>
<td>
Not supported<br/><br/></td>
</tr>
<tr>
<td>
Equation<br/><br/></td>
<td>
Not supported<br/><br/></td>
</tr>
<tr>
<td>
SmartArt<br/><br/></td>
<td>
Not supported<br/><br/></td>
</tr>
<tr>
<td>
WordArt<br/><br/></td>
<td>
Not supported<br/><br/></td>
</tr>
<tr>
<td>
Form Fields
</td>
<td>
Unparsed in Word Processing 2003 XML document.
</td>
</tr>
<tr>
<td>
Ole Object
</td>
<td>
Unparsed in Word Processing 2003 XML document.
</td>
</tr>
</table>
## Word Binary (97-2003) format (classic)
DOC is one of the popular file format of word processing document. It is a proprietary binary format of Microsoft used in all the Microsoft Word versions.
DocIO library supports importing/exporting of DOC format and please find the code snippet below, for the same.
C#:
{% tabs %}
{% highlight c# %}
//Creates an instance of WordDocument Instance (Empty Word Document)

WordDocument document = new WordDocument();

//Add a section & a paragraph in the empty document

document.EnsureMinimal();

//Append text to the last paragraph of the document

document.LastParagraph.AppendText("Hello World");

//Save and close the Word document

document.Save("BinaryDocument.doc");

document.Close();
{% endhighlight %}
{% endtabs %}
VB:
{% tabs %}
{% highlight vb.net %}
'Creates an instance of WordDocument Instance (Empty Word Document)

Dim document As New WordDocument()

'Add a section & a paragraph in the empty document

document.EnsureMinimal()

'Append text to the last paragraph of the document

document.LastParagraph.AppendText("Hello World")

'Save and close the Word document

document.Save("BinaryDocument.doc ")

document.Close()
{% endhighlight %}
{% endtabs %}
### DOC to DOCX and DOCX to DOC
The following code shows, how to convert the DOC file into DOCX file format using DocIO
C#:
{% tabs %}
{% highlight c# %}
//Loads an existing document

WordDocument document = new WordDocument("Sample.doc", FormatType.Doc);

//Saves the binary document(.doc) as Word Document(.docx) file

document.Save("DocToWord.docx", FormatType.Docx);

//Closes the document

document.Close();
{% endhighlight %}
{% endtabs %}
VB:
{% tabs %}
{% highlight vb.net %}
'Loads an existing document

Dim document As New WordDocument("Sample.doc", FormatType.Doc)

' Saves the binary document(.doc) as Word Document(.docx) file

document.Save("DocToWord.docx", FormatType.Docx)

'Closes the document

document.Close()
{% endhighlight %}
{% endtabs %}
The following code shows, how to convert the DOCX file into DOC file format using DocIO
C#:
{% tabs %}
{% highlight c# %}
//Loads an existing document

WordDocument document = new WordDocument("Sample.docx", FormatType.Docx);

//Saves the Word Document(.docx) as binary document(.doc) file

document.Save("DocxToBinary.doc", FormatType.Doc);

//Closes the document

document.Close();
{% endhighlight %}
{% endtabs %}
VB:
{% tabs %}
{% highlight vb.net %}
'Loads an existing document

Dim document As New WordDocument("Sample.docx", FormatType.Docx)

' Saves the Word Document(.docx) as binary document(.doc) file 

document.Save("DocxToBinary.doc", FormatType.Doc)

'Closes the document

document.Close()
{% endhighlight %}
{% endtabs %}
## RTF (classic)
The [Rich Text Format (RTF)](http://en.wikipedia.org/wiki/Rich_Text_Format# "") is one of the document formats supported by Microsoft Word and many other word processing applications. RTF is human readable file format invented for interchanging formatted text between applications, is an optional format for Word that retains most formatting and all content of the original document.
Now, most of the word processor's (including Microsoft Word) uses the XML-based file format Microsoft has discontinued enhancements to the RTF and still supporting it. The last version was 1.9.1 released in 2008.
Essential DocIO supports to convert the RTF document into Word document and vice versa. The following code shows how to convert RTF document into Word document.
C#:
{% tabs %}
{% highlight c# %}
//Loads an existing document

WordDocument document = new WordDocument("Sample.rtf", FormatType.Rtf);

//Saves the Word document as RTF file

document.Save("RtfToWord.docx", FormatType.Docx);

//Closes the document

document.Close();
{% endhighlight %}
{% endtabs %}
VB:
{% tabs %}
{% highlight vb.net %}
'Loads an existing document

Dim document As New WordDocument("Sample.rtf", FormatType.Rtf)

'Saves the Word document as RTF file

document.Save("RtfToWord.docx", FormatType.Docx)

'Closes the document

document.Close()
{% endhighlight %}
{% endtabs %}
The following code example shows how to convert Word document into RTF document.
C#:
{% tabs %}
{% highlight c# %}
//Loads an existing document

WordDocument document = new WordDocument("Template.docx", FormatType.Docx);

//Saves the Word document as RTF file

document.Save("WordToRtf.rtf", FormatType.Rtf);

//Closes the document

document.Close();
{% endhighlight %}
{% endtabs %}
VB:
{% tabs %}
{% highlight vb.net %}
'Loads an existing document

Dim document As New WordDocument("Template.docx", FormatType.Docx)

'Saves the Word document as RTF file

document.Save("WordToRtf.rtf", FormatType.Rtf)

'Closes the document

document.Close()
{% endhighlight %}
{% endtabs %}
## Supported and Unsupported features
The supported and unsupported features of DocIO based on file formats can be referred from [here](https://help.syncfusion.com/file-formats/docio/supported-and-unsupported-features#)
