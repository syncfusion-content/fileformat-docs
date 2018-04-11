---
title: Word file format conversions
description: Word file format conversions supported in DocIO
platform: file-formats
control: DocIO
documentation: UG
---

# Working with Document Conversions

Essential DocIO provides a support to convert documents from one format to another format. Each file format document can be categorized as flow layout document or fixed layout document. 

**Flow layout document:**

* A flow document is designed to "reflow content" depending on application.
* Doesn’t contain any information about the position of its content.
* Dynamically render the content by application at run time.
* Example: DOC, DOCX, HTML, EPUB, RTF and TEXT file formats.

**Fixed layout document:**

* This format of fixed document is something like "what you see is what you get".
* Maintains the fixed position for each content.
* Statically preserve the content in specified position.
* Example: Image and PDF.


Essential DocIO can convert various flow document as fixed document by using our layout engine. Following conversions are supported by Essential DocIO.

* Microsoft Word file format Conversions.
* Word document to PDF.
* Word document to Image.
* RTF Conversions.
* Text Conversions.
* HTML Conversions.
* Word document to ODT.
* Word document to EPUB.

## Word file format Conversions.

The [Microsoft Word's](https://en.wikipedia.org/wiki/Microsoft_Word#) native file formats are DOC, DOCX, RTF, DOT, DOTX, DOCM, DOTM. Essential DocIO supports 3 major native file formats.

1. Word Open XML formats (2007 & later)
2. Word Binary (97-2003) format (classic)
3. RTF (classic)

N> We recommend you use DOCX file formats since Microsoft corporation stopped their development in DOC file format and new features inclusion done in DOCX file format alone. 

## Word Open XML formats (2007 & later)

The XML format introduced in Microsoft Word 2003 was a simple, XML-based format called WordprocessingML or WordML.
[Office Open XML](http://en.wikipedia.org/wiki/Office_Open_XML#) (OOXML or Microsoft Open XML (MOX)) is a zipped, new XML-based file format introduced by Microsoft in Office 2007 applications. WordprocessingML is the markup language used by Microsoft Office Word to store its DOCX documents.

DocIO supports the following WordprocessingML,

* Microsoft Word 2007
* Microsoft Word 2010
* Microsoft Word 2013
* Microsoft Word 2016

The following code example explains how to create a new Word document with few lines of code

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

### Templates

DOTX is a word document template. The following code snippet shows how to create the word document template with few lines of code,

{% tabs %}
{% highlight c# %}
//Creates an instance of WordDocument Instance (Empty Word Document)

WordDocument document = new WordDocument();

//Add a section & a paragraph in the empty document

document.EnsureMinimal();

//Append text to the last paragraph of the document

document.LastParagraph.AppendText("Hello World");

//Save and close the Word document

document.Save("Result.dotx");

document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Creates an instance of WordDocument Instance (Empty Word Document)

Dim document As New WordDocument()

'Add a section & a paragraph in the empty document

document.EnsureMinimal()

'Append text to the last paragraph of the document

document.LastParagraph.AppendText("Hello World")

'Save and close the Word document

document.Save("Result.dotx")

document.Close()
{% endhighlight %}
{% endtabs %}

### Macros

DOCM is macro enabled word document. It is same as DOCX document contains macros and scripts. DocIO provides only preservation support for macros. The following code illustrates how to load and save a macro enabled document using DocIO library.

{% tabs %}
{% highlight c# %}
// Loads the macro-enabled template.

WordDocument document = new WordDocument("Template.dotm");

// Gets the table

DataTable table = GetDataTable();

// Executes Mail Merge with groups.

document.MailMerge.ExecuteGroup(table);

//Saves and closes the document

document.Save("Sample.docm", FormatType.Word2013Docm);

document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Loads the macro-enabled template.

Dim document As New WordDocument("Template.dotm")

'Gets the table

Dim table As DataTable = GetDataTable()

'Executes Mail Merge with groups.

document.MailMerge.ExecuteGroup(table)

'Saves and closes the document

document.Save("Sample.docm", FormatType.Word2013Docm)

document.Close()
{% endhighlight %}
{% endtabs %}



## Word Processing XML conversion(.xml)

Essential DocIO supports converting the Word document into Word Processing XML document and vice versa.

N> Currently we support importing for Word Processing 2003 XML documents. Import and export support for Word Processing 2007 XML documents.

The following code example shows how to convert the Word document into Word Processing XML document.

{% tabs %}
{% highlight c# %}
//Loads an existing Word document

WordDocument document = new WordDocument("Template.docx");

//Saves the document as Word Processing ML document

document.Save("WordToWordML.xml", FormatType.WordML);

//Closes the document

document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Loads an existing Word document 

Dim document As New WordDocument("Template.docx")

'Saves the document as Word Processing ML document

document.Save("WordToWordML.xml", FormatType.WordML)

'Closes the document

document.Close()
{% endhighlight %}
{% endtabs %}

The following code example shows how to convert the Word Processing XML document into Word document.

{% tabs %}
{% highlight c# %}
// Loads an existing Word document 

WordDocument document = new WordDocument("Template.xml");

//Saves the Word Processing ML document as docx

document.Save("WordMLToWord.docx", FormatType.Docx);

//Closes the document

document.Close();
{% endhighlight %}

{% highlight vb.net %}
' Loads an existing Word document 

Dim document As New WordDocument("Template.xml")

'Saves the Word Processing ML document as docx 

document.Save("WordMLToWord.docx", FormatType.Docx)

'Closes the document

document.Close()
{% endhighlight %}
{% endtabs %}

### Unsupported elements in Word to Word Processing XML conversion:

The following table contains list of unsupported elements in Word to Word Processing XML conversion.

<table>
<thead> 
<tr>
<th>Element</th>
<th>Limitations or Unsupported elements</th>
</tr>
</thead>
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

## Word Binary (97-2003) format

DOC is one of the classic file format of word processing document. It is a proprietary binary format of Microsoft used in all the Microsoft Word versions.

DocIO library supports importing/exporting of DOC format and please find the code snippet below, for the same.

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

{% tabs %}
{% highlight c# %}
//Loads an existing document

WordDocument document = new WordDocument("Sample.doc", FormatType.Doc);

//Saves the binary document(.doc) as Word Document(.docx) file

document.Save("DocToWord.docx", FormatType.Docx);

//Closes the document

document.Close();
{% endhighlight %}

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

{% tabs %}
{% highlight c# %}
//Loads an existing document

WordDocument document = new WordDocument("Sample.docx", FormatType.Docx);

//Saves the Word Document(.docx) as binary document(.doc) file

document.Save("DocxToBinary.doc", FormatType.Doc);

//Closes the document

document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Loads an existing document

Dim document As New WordDocument("Sample.docx", FormatType.Docx)

' Saves the Word Document(.docx) as binary document(.doc) file 

document.Save("DocxToBinary.doc", FormatType.Doc)

'Closes the document

document.Close()
{% endhighlight %}
{% endtabs %}
