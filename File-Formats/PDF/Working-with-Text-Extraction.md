---
title: Working with Text Extraction
description: Extract the text from ta particular page; text extraction
platform: FileFormat
control: PDF
documentation: UG
---
# Working with Text Extraction

Essential PDF allows you to extract the text from a particular page or the entire PDF document. 

## Working with basic text extraction

You can extract the text from a page using ExtractText method in PdfPageBase class.

The following code snippet explains how to extract the texts from a page.

{% highlight c# %}
C#:

//Load an existing PDF.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);

//Load the first page.

PdfPageBase page = loadedDocument.Pages[0];

//Extract text from first page.

string extractedText = page.ExtractText();

//Close the document

loadedDocument.Close(true);





{% endhighlight %}

{% highlight vb.net %}
VB:

'Load an existing PDF.

Dim loadedDocument As New PdfLoadedDocument(fileName)

'Load the first page.

Dim page As PdfPageBase = loadedDocument.Pages(0)

'Extract the text from first page.

Dim extractedText As String = page.ExtractText()

'close the document.

loadedDocument.Close(True)





{% endhighlight %}

**Note****:** In this method, the text is extracted in the order in which it is written in the document stream and it may not be in the order in which it is viewed in the PDF reader application.

The below code illustrates how to extract the text from entire PDF document:

{% highlight c# %}
C#:

// Load an existing PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);

// Loading page collections

PdfLoadedPageCollection loadedPages = loadedDocument.Pages;

string extractedText = string.Empty;

// Extract text from existing PDF document pages

foreach (PdfLoadedPage lpage in loadedPages)

{

extractedText += lpage.ExtractText();

}

// Close the document.

loadedDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}
VB:

' Load an existing PDF document.

Dim loadedDocument As New PdfLoadedDocument(fileName)

' Loading page collections

Dim loadedPages As PdfLoadedPageCollection = loadedDocument.Pages

Dim extractedText As String = String.Empty

' Extract text from existing PDF document pages

For Each lpage As PdfLoadedPage In loadedPages

extractedText &= lpage.ExtractText()

Next lpage

' Close the document.

loadedDocument.Close(True)



{% endhighlight %}

## Working with layout based text extraction

You can extract text from the given PDF page based on its layout using ExtractText(bool) overload. In this method, the text is extracted in the layout as it is viewed in the reader application.

Please refer the following code snippet to extract the text with layout.

{% highlight c# %}
C#:

//Load an existing PDF.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);

//Load first page.

PdfPageBase page = loadedDocument.Pages[0];

//Extract text from first page.

string extractedTexts = page.ExtractText(true);

//close the document

loadedDocument.Close(true);





{% endhighlight %}

{% highlight vb.net %}
VB:

//Load an existing PDF.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);

//Load first page.

PdfPageBase page = loadedDocument.Pages[0];

//Extract text from first page.

string extractedTexts = page.ExtractText(true);

//close the document

loadedDocument.Close(true);





{% endhighlight %}

**Note****:** Layout based text extraction may take additional processing time when compared to the normal extraction mode.

