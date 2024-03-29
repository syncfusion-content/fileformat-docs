---
title: Working with Text Extraction | Syncfusion
description: This section explains how to extract text and its bounds from a particular page or the entire PDF document.
platform: file-formats
control: PDF
documentation: UG
---
# Working with Text Extraction

Essential PDF allows you to extract the text from a particular page or the entire PDF document. 

Check the following video to quickly get started with extracting text from a PDF document in .NET using the PDF Library.
{% youtube "https://www.youtube.com/watch?v=CB4tQC-LhUU" %}

## Working with basic text extraction

You can extract the text from a page using [ExtractText](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfPageBase.html#Syncfusion_Pdf_PdfPageBase_ExtractText) method in [PdfPageBase](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfPageBase.html) class.

The following code snippet explains how to extract the texts from a page.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Load the PDF document.
FileStream docStream = new FileStream("Sample.pdf", FileMode.Open, FileAccess.Read);
//Load the PDF document.
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);
//Load the first page.
PdfPageBase page = loadedDocument.Pages[0];

//Extract text from first page.
string extractedText = page.ExtractText();
//Close the document.
loadedDocument.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Load an existing PDF.
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);
//Load the first page.
PdfPageBase page = loadedDocument.Pages[0];

//Extract text from first page.
string extractedText = page.ExtractText();
//Close the document
loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Load an existing PDF.
Dim loadedDocument As New PdfLoadedDocument(fileName)
'Load the first page.
Dim page As PdfPageBase = loadedDocument.Pages(0)

'Extract the text from first page.
Dim extractedText As String = page.ExtractText()
'close the document.
loadedDocument.Close(True)

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Text%20Extraction/Extract-the-texts-from-a-page-in-the-PDF-document/). 

N> In this method, the text is extracted in the order in which it is written in the document stream and it may not be in the order in which it is viewed in the PDF reader application.

N> Extracting text from the PDF document pages will not load the entire document content into memory.

The below code illustrates how to extract the text from entire PDF document:

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Load the PDF document.
FileStream docStream = new FileStream("Sample.pdf", FileMode.Open, FileAccess.Read);
//Load the PDF document.
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);
// Loading page collections
PdfLoadedPageCollection loadedPages = loadedDocument.Pages;

string extractedText = string.Empty;
// Extract text from existing PDF document pages
foreach (PdfLoadedPage loadedPage in loadedPages)
{
    extractedText += loadedPage.ExtractText();
}
//Close the document.
loadedDocument.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

// Load an existing PDF document.
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);
// Loading page collections
PdfLoadedPageCollection loadedPages = loadedDocument.Pages;

string extractedText = string.Empty;
// Extract text from existing PDF document pages
foreach (PdfLoadedPage loadedPage in loadedPages)
{
extractedText += loadedPage.ExtractText();
}
// Close the document.
loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Load an existing PDF document.
Dim loadedDocument As New PdfLoadedDocument(fileName)
' Loading page collections
Dim loadedPages As PdfLoadedPageCollection = loadedDocument.Pages

Dim extractedText As String = String.Empty
' Extract text from existing PDF document pages
For Each loadedPage As PdfLoadedPage In loadedPages
extractedText &= loadedPage.ExtractText()
Next loadedPage
' Close the document.
loadedDocument.Close(True)

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Text%20Extraction/Extract-text-from-the-entire-PDF-document/). 

## Working with layout based text extraction

You can extract text from the given PDF page based on its layout using [ExtractText(bool)](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfPageBase.html#Syncfusion_Pdf_PdfPageBase_ExtractText_System_Boolean_) overload. In this method, the text is extracted in the layout as it is viewed in the reader application.

Please refer the following code snippet to extract the text with layout.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Load the PDF document.
FileStream docStream = new FileStream("Sample.pdf", FileMode.Open, FileAccess.Read);
//Load the PDF document.
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);
//Load first page.
PdfPageBase page = loadedDocument.Pages[0];

//Extract text from first page.
string extractedTexts = page.ExtractText(true);
//Close the document.
loadedDocument.Close(true);

//Save the document into stream
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);
//Closes the document
loadedDocument.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Load an existing PDF.
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);
//Load first page.
PdfPageBase page = loadedDocument.Pages[0];

//Extract text from first page.
string extractedTexts = page.ExtractText(true);
//close the document
loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

//Load an existing PDF.
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);
//Load first page.
PdfPageBase page = loadedDocument.Pages[0];

//Extract text from first page.
string extractedTexts = page.ExtractText(true);
//close the document
loadedDocument.Close(true);

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Text%20Extraction/Extract-the-text-with-layout-in-a-PDF-document/). 

N> Layout based text extraction may take additional processing time when compared to the normal extraction mode.

## Text Extraction with Bounds

### Working with Lines

You can get the line and its properties that contains texts by using [TextLine](https://help.syncfusion.com/cr/xamarin/Syncfusion.Pdf.TextLine.html). Refer to the following code sample.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

//PDF supports getting the lines and its properties using TextLine only in WinForms, WPF and Xamarin platforms. Instead of TextLine, TextLineCollection can be used in ASP.NET Core.

// Load the existing PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);
// Get the first page of the loaded PDF document
PdfPageBase page = loadedDocument.Pages[0];
var lineCollection = new TextLineCollection();

// Extract text from the first page
string extractedText = page.ExtractText(out lineCollection);
// Gets each line from the collection
foreach (var line in lineCollection.TextLine)
{
    // Gets bounds of the line
    RectangleF lineBounds = line.Bounds;
    // Gets text in the line
    string text = line.Text;
}

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

// Load the existing PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);
// Get the first page of the loaded PDF document
PdfPageBase page = loadedDocument.Pages[0];
TextLines lineCollection = new TextLines();

// Extract text from the first page
string extractedText = page.ExtractText(out lineCollection);
// Gets specific line from the collection
TextLine line = lineCollection[0];
// Gets bounds of the line
RectangleF lineBounds = line.Bounds;
// Gets text in the line
string text = line.Text;

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
' Load the existing PDF document
Dim loadedDocument As PdfLoadedDocument = New PdfLoadedDocument(fileName)
' Get the first page of the loaded PDF document
Dim page As PdfPageBase = loadedDocument.Pages(0)
Dim lineCollection As TextLines = New TextLines()

' Extract text from the first page
Dim extractedText As String = page.ExtractText(lineCollection)
' Gets specific line from the collection
Dim line As TextLine = lineCollection(0)
' Gets bounds of the line
Dim lineBounds As RectangleF = line.Bounds
' Gets text in the line
Dim text As String = line.Text

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Text%20Extraction/Extract-each-lines-from-an-existing-PDF-document). 

### Working with words
 
You can get the single word and its properties by using [TextWord](https://help.syncfusion.com/cr/xamarin/Syncfusion.Pdf.TextWord.html). Refer to the following code sample.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

//PDF supports getting the word and its properties using TextWord only in WinForms, WPF and Xamarin platforms. Instead of TextLine, TextLineCollection can be used in ASP.NET Core.

// Load the existing PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);
// Get the first page of the loaded PDF document
PdfPageBase page = loadedDocument.Pages[0];
var lineCollection = new TextLineCollection();

// Extract text from the first page
string extractedText = page.ExtractText(out lineCollection);
// Gets each line from the collection
foreach (var line in lineCollection.TextLine)
{   
    // Gets bounds of the line
    RectangleF lineBounds = line.Bounds;
    // Gets text in the line
    string text = line.Text;
    // Gets collection of the words in the line
    List<TextWord> textWordCollection = line.WordCollection;
}

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

// Load the existing PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);
// Get the first page of the loaded PDF document
PdfPageBase page = loadedDocument.Pages[0];
TextLines lineCollection = new TextLines();

// Extract text from the first page
string extractedText = page.ExtractText(out lineCollection);
// Gets specific line from the collection
TextLine line = lineCollection[0];
// Gets bounds of the line
RectangleF lineBounds = line.Bounds;
// Gets text in the line
string text = line.Text;
// Gets collection of the words in the line
List<TextWord> textWordCollection = line.WordCollection;

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Load the existing PDF document
Dim loadedDocument As PdfLoadedDocument = New PdfLoadedDocument(fileName)
' Get the first page of the loaded PDF document
Dim page As PdfPageBase = loadedDocument.Pages(0)
Dim lineCollection As TextLines = New TextLines()

' Extract text from the first page
Dim extractedText As String = page.ExtractText(lineCollection)
' Gets specific line from the collection
Dim line As TextLine = lineCollection(0)
' Gets bounds of the line
Dim lineBounds As RectangleF = line.Bounds
' Gets text in the line
Dim text As String = line.Text
' Gets collection of the words in the line
Dim textWordCollection As List(Of TextWord) = line.WordCollection

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Text%20Extraction/Extract-collection-of-words-from-PDF-document/). 

### Working with characters

You can get single character and its properties by using [TextGlyph](https://help.syncfusion.com/cr/xamarin/Syncfusion.Pdf.TextGlyph.html). Refer to the following code sample. 

{% tabs %}

{% highlight c# tabtitle="Xamarin" %}

//Load the existing PDF document
PdfLoadedDocument m_loadedDocument = new PdfLoadedDocument(stream);
//Get the first page of the loaded PDF document
PdfPageBase page = m_loadedDocument.Pages[0];
TextLineCollection lineCollection = new TextLineCollection();

//Extract text from the first page
string m_extractedText = page.ExtractText(out lineCollection);
//Gets specific line from the collection
TextLine line = lineCollection.TextLine[0];
//Gets collection of the words in the line
List<TextWord> textWordCollection = line.WordCollection;
//Gets word from the collection using index
TextWord textWord = textWordCollection[0];
// Gets Glyph details of the word
List<TextGlyph> textGlyphCollection = textWord.Glyphs;

//Gets character of the word
TextGlyph textGlyph = textGlyphCollection[0];
//Gets bounds of the character
RectangleF glyphBounds = textGlyph.Bounds;
//Gets font name of the character
string GlyphFontName = textGlyph.FontName;
//Gets font size of the character
float GlyphFontSize = textGlyph.FontSize;
//Gets font style of the character
FontStyle GlyphFontStyle = textGlyph.FontStyle;
//Gets character in the word
char GlyphText = textGlyph.Text;

{% endhighlight %}

{% endtabs %}
