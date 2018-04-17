---
title: Word file format conversions
description: Word file format conversions supported in DocIO
platform: file-formats
control: DocIO
documentation: UG
---

# Working with Document Conversions

## Word File Format Conversions

The [Microsoft Word's](https://en.wikipedia.org/wiki/Microsoft_Word#) native file formats are DOC, DOCX, RTF, DOT, DOTX, DOCM, and DOTM. The Essential DocIO supports the following major native file formats.

1. Word Open XML formats (2007 & later)
2. Word Binary (97-2003) format (classic)

N> Use DOCX file formats, because Microsoft corporation stopped their development in DOC file format and new features inclusion done in DOCX file format alone.  

## Word Open XML formats (2007 & later)

[Office Open XML](http://en.wikipedia.org/wiki/Office_Open_XML#) (OOXML or Microsoft Open XML (MOX)) is a zipped, new XML-based file format introduced by Microsoft in Office 2007 applications. WordprocessingML is the markup language used by Microsoft Office Word to store its DOCX documents.

DocIO supports the following WordprocessingML:

* Microsoft Word 2007
* Microsoft Word 2010
* Microsoft Word 2013
* Microsoft Word 2016

The following code example explains how to create a new Word document with few lines of code.

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

DOTX is a Word document template. The following code snippet shows how to create the Word document template with few lines of code.

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

DOCM is a macro enabled Word document. It is same as DOCX document contains macros and scripts. The DocIO provides only preservation support for macros. The following code illustrates how to load and save a macro enabled document using the DocIO library.

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

The XML format introduced in Microsoft Word 2003 was a simple, XML-based format called WordprocessingML or WordML.
The Essential DocIO supports converting the Word document into Word Processing XML document and vice versa.

N> Currently importing and exporting the Word Processing 2003 (importing alone) and 2007 XML documents is supported.

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

DOC is one of the classic file format of Word processing document. It is a proprietary binary format of Microsoft used in all the Microsoft Word versions.

The DocIO library supports importing or exporting of DOC format and refer to the following code sample.

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
