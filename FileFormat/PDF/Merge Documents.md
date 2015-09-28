---
layout: Post
title: Merge Documents
description: Merging multiple PDF document into single PDF: Merge PDF documents; Import page
platform: FileFormat
control: PDF
documentation: UG
---
# Merge Documents

Essential PDF supports merging multiple PDF documents from disk and stream.

## Merging multiple documents from disk and stream

You can merge the multiple PDF document by specifying the path of the documents in a string array.

Please refer the below code snippet to merge multiple documents from disk.

{% highlight c# %}
[C#]

//create a new PDF document

PdfDocument finalDoc = new PdfDocument();

// Create a string array of source files which are to be merged.

string[] source = { "file1.pdf, file2.pdf" };

// Merge PDFDocument.

PdfDocument.Merge(finalDoc, source);

//save the final document

finalDoc.Save("Sample.pdf");

//close the document

finalDoc.Close(true);



{% endhighlight %}



{% highlight vb.net %}
[VB]

'create a new PDF document

Dim finalDoc As New PdfDocument()

' Create a string array of source files which are to be merged.

Dim source As String() = {"file1.pdf, file2.pdf"}

' Merge PDFDocument.

PdfDocument.Merge(finalDoc, source)

'save the final document

finalDoc.Save("Sample.pdf")

'close the document

finalDoc.Close(True)



{% endhighlight %}

You can merge the PDF document streams using the below code snippet.

{% highlight c# %}
[C#]

//create a PDF document

PdfDocument finalDoc = new PdfDocument();

Stream stream1 = File.OpenRead("file1.pdf");

Stream stream2 = File.OpenRead("file2.pdf");

// Create a PDF stream for merging.

Stream[] streams = { stream1, stream2 };

// Merge PDFDocument.

PdfDocumentBase.Merge(finalDoc, streams);

//saving the document

finalDoc.Save("sample.pdf");

//closing the document

finalDoc.Close(true);

//Dispose the streams

stream1.Dispose();

stream2.Dispose();



{% endhighlight %}



{% highlight vb.net %}
[VB]

'create a PDF document

Dim finalDoc As New PdfDocument()

Dim stream1 As Stream = File.OpenRead("file1.pdf")

Dim stream2 As Stream = File.OpenRead("file2.pdf")

' Create a PDF stream for merging.

Dim streams As Stream() = {stream1, stream2}

' Merge PDFDocument.

PdfDocumentBase.Merge(finalDoc, streams)

'saving the document

finalDoc.Save("sample.pdf")

'closing the document

finalDoc.Close(True)

'Dispose the streams

stream1.Dispose()

stream2.Dispose()



{% endhighlight %}

## Importing pages from multiple documents

**Essential** **PDF** provides support for importing the pages from one document to another document, the following code illustrate this. The imported page will be added to the end of the original document.

{% highlight c# %}
[C#]      

//Load document

PdfLoadedDocument lDoc = new PdfLoadedDocument("file1.pdf");

//create a new document

PdfDocument document = new PdfDocument();

//import the page at 1 from the lDoc

document.ImportPage(lDoc, 1);

//save the document

document.Save("sample.pdf");

//close the document

document.Close(true);

lDoc.Close(true)



{% endhighlight %}



{% highlight vb.net %}
[VB]

'Load document

Dim lDoc As New PdfLoadedDocument("file1.pdf")

'create a new document

Dim document As New PdfDocument()

'import the page at 1 from the lDoc

document.ImportPage(lDoc, 1)

'save the document

document.Save("sample.pdf")

'close the document

document.Close(True)

lDoc.Close(True)



{% endhighlight %}

You can import multiple pages from an existing document using **ImportPageRange** method, the following code sample illustrate this.

{% highlight c# %}
[C#]      

//Load PDF document

PdfLoadedDocument lDoc = new PdfLoadedDocument("file1.pdf");

//create a new document

PdfDocument document = new PdfDocument();

//import the pages from the lDoc

document.ImportPageRange(lDoc, 0, lDoc.Pages.Count - 1);

//save the document

document.Save("sample.pdf");

//close the documents

document.Close(true);

lDoc.Close(true);



{% endhighlight %}



{% highlight vb.net %}
[VB]

'Load PDF document

Dim lDoc As New PdfLoadedDocument("file1.pdf")

'create a new document

Dim document As New PdfDocument()

'import the pages from the lDoc

document.ImportPageRange(lDoc, 0, lDoc.Pages.Count - 1)

'save the document

document.Save("sample.pdf")

'close the documents

document.Close(True)

lDoc.Close(True)



{% endhighlight %}

You can also import pages from multiple documents and arrange the pages as required. The code snippet below explains the same.

{% highlight c# %}
[C#]      

//Loading document

PdfLoadedDocument lDoc = new PdfLoadedDocument("file1.pdf");

//Loading document

PdfLoadedDocument lDoc2 = new PdfLoadedDocument("file1.pdf");

//creating the new document

PdfDocument document = new PdfDocument();

//importing and arranging the pages

document.ImportPage(lDoc, 2);

document.ImportPage(lDoc2, 1);

//saving the document

document.Save("sample.pdf");

//closing the documents

document.Close(true);

lDoc.Close(true);

lDoc2.Close(true);



{% endhighlight %}



{% highlight vb.net %}
[VB]

'Load a document

Dim lDoc As New PdfLoadedDocument("file1.pdf")

Dim lDoc2 As New PdfLoadedDocument("file2.pdf")

'create a new document

Dim document As New PdfDocument()

'import and arrange the pages

document.ImportPage(lDoc, 2)

document.ImportPage(lDoc2, 1)

'save the document

document.Save("sample.pdf")

'close the documents

document.Close(True)

lDoc.Close(True)

lDoc2.Close(True)



{% endhighlight %}

## Best practices

Merging multiple large **PDF** documents can lead to high runtime memory, so you can split the documents into multiple documents and later you can merge. This method avoids the extensive memory usage and increase the performance.

Note:  The parent PDF document will have all the contents in run time memory. It will release the memory once the final PDF document instance is disposed. 

The below code shows to split the PDF document

{% highlight c# %}
[C#]      

//Load the PDF document

PdfLoadedDocument ldocument = new PdfLoadedDocument("large.pdf");

//Split the document

ldocument.Split("splited.pdf");

//Close the document

ldocument.Close(true);



{% endhighlight %}



{% highlight vb.net %}
[VB]

'Load the PDF document

Dim ldocument As New PdfLoadedDocument("large.pdf")

'Split the document

ldocument.Split("splited.pdf")

'Close the document

ldocument.Close(True)



{% endhighlight %}

The below code shows to merge the PDF documents.

{% highlight c# %}
[C#]



//Input documents

string[] inputDocuments = Directory.GetFiles("../../Data/Split");

//Create a PDF document

PdfDocument document = new PdfDocument();

//Merge the document

PdfDocumentBase.Merge(document, inputDocuments);

//Save and close the document

document.Save("Output.pdf");

document.Close(true);



{% endhighlight %}



{% highlight vb.net %}
[VB.NET]

'Input documents

Dim inputDocuments As String() = Directory.GetFiles("../../Data/Split")

'Create a PDF document

Dim document As New PdfDocument()

'Merge the document

PdfDocumentBase.Merge(document, inputDocuments)

'Save and close the document

document.Save("Output.pdf")

document.Close(True)



{% endhighlight %}



