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

Refer to the following code example to merge multiple documents from disk.

{% highlight c# %}
[C#]

//Creates a new PDF document

PdfDocument finalDoc = new PdfDocument();

// Creates a string array of source files to be merged.

string[] source = { "file1.pdf, file2.pdf" };

// Merges PDFDocument.

PdfDocument.Merge(finalDoc, source);

//Saves the final document

finalDoc.Save("Sample.pdf");

//Closes the document

finalDoc.Close(true);



{% endhighlight %}



{% highlight vb.net %}
[VB]

'Creates a new PDF document

Dim finalDoc As New PdfDocument()

' Creates a string array of source files to be merged.

Dim source As String() = {"file1.pdf, file2.pdf"}

' Merges PDFDocument.

PdfDocument.Merge(finalDoc, source)

'Saves the final document

finalDoc.Save("Sample.pdf")

'Closes the document

finalDoc.Close(True)



{% endhighlight %}

You can merge the PDF document streams by using the following code example.

{% highlight c# %}
[C#]

//Creates a PDF document

PdfDocument finalDoc = new PdfDocument();

Stream stream1 = File.OpenRead("file1.pdf");

Stream stream2 = File.OpenRead("file2.pdf");

// Creates a PDF stream for merging.

Stream[] streams = { stream1, stream2 };

// Merges PDFDocument.

PdfDocumentBase.Merge(finalDoc, streams);

//Saves the document

finalDoc.Save("sample.pdf");

//Closes the document

finalDoc.Close(true);

//Disposes the streams

stream1.Dispose();

stream2.Dispose();



{% endhighlight %}



{% highlight vb.net %}
[VB]

'Creates a PDF document

Dim finalDoc As New PdfDocument()

Dim stream1 As Stream = File.OpenRead("file1.pdf")

Dim stream2 As Stream = File.OpenRead("file2.pdf")

' Creates a PDF stream for merging.

Dim streams As Stream() = {stream1, stream2}

' Merges PDFDocument.

PdfDocumentBase.Merge(finalDoc, streams)

'Saves the document

finalDoc.Save("sample.pdf")

'Closes the document

finalDoc.Close(True)

'Disposes the streams

stream1.Dispose()

stream2.Dispose()



{% endhighlight %}

## Importing pages from multiple documents

**Essential** **PDF** provides support for importing the pages from one document to another document. The following code illustrates this. The imported page is added to the end of the original document.

{% highlight c# %}
[C#]      

//Loads document

PdfLoadedDocument lDoc = new PdfLoadedDocument("file1.pdf");

//Creates a new document

PdfDocument document = new PdfDocument();

//Imports the page at 1 from the lDoc

document.ImportPage(lDoc, 1);

//Saves the document

document.Save("sample.pdf");

//Closes the document

document.Close(true);

lDoc.Close(true)



{% endhighlight %}



{% highlight vb.net %}
[VB]

'Loads document

Dim lDoc As New PdfLoadedDocument("file1.pdf")

'Creates a new document

Dim document As New PdfDocument()

'Imports the page at 1 from the lDoc

document.ImportPage(lDoc, 1)

'Saves the document

document.Save("sample.pdf")

'Closes the document

document.Close(True)

lDoc.Close(True)



{% endhighlight %}

You can import multiple pages from an existing document by using **ImportPageRange** method. The following code example illustrates this.

{% highlight c# %}
[C#]      

//Loads PDF document

PdfLoadedDocument lDoc = new PdfLoadedDocument("file1.pdf");

//Creates a new document

PdfDocument document = new PdfDocument();

//Imports the pages from the lDoc

document.ImportPageRange(lDoc, 0, lDoc.Pages.Count - 1);

//Saves the document

document.Save("sample.pdf");

//Closes the documents

document.Close(true);

lDoc.Close(true);



{% endhighlight %}



{% highlight vb.net %}
[VB]

'Loads PDF document

Dim lDoc As New PdfLoadedDocument("file1.pdf")

'Creates a new document

Dim document As New PdfDocument()

'Imports the pages from the lDoc

document.ImportPageRange(lDoc, 0, lDoc.Pages.Count - 1)

'Saves the document

document.Save("sample.pdf")

'Closes the documents

document.Close(True)

lDoc.Close(True)



{% endhighlight %}

You can also import pages from multiple documents and arrange the pages as required. The following code example explains the same.

{% highlight c# %}
[C#]      

//Loads document

PdfLoadedDocument lDoc = new PdfLoadedDocument("file1.pdf");

//Loads document

PdfLoadedDocument lDoc2 = new PdfLoadedDocument("file1.pdf");

//Creates the new document

PdfDocument document = new PdfDocument();

//Imports and arranges the pages

document.ImportPage(lDoc, 2);

document.ImportPage(lDoc2, 1);

//Saves the document

document.Save("sample.pdf");

//Closes the documents

document.Close(true);

lDoc.Close(true);

lDoc2.Close(true);



{% endhighlight %}



{% highlight vb.net %}
[VB]

'Loads a document

Dim lDoc As New PdfLoadedDocument("file1.pdf")

Dim lDoc2 As New PdfLoadedDocument("file2.pdf")

'create a new document

Dim document As New PdfDocument()

'imports and arranges the pages

document.ImportPage(lDoc, 2)

document.ImportPage(lDoc2, 1)

'Saves the document

document.Save("sample.pdf")

'Closes the documents

document.Close(True)

lDoc.Close(True)

lDoc2.Close(True)



{% endhighlight %}

## Best practices

Merging multiple large **PDF** documents can lead to high runtime memory. So, you can split the documents into multiple documents and later you can merge. This method avoids the extensive memory usage and increases the performance.

Note:  The parent PDF document has all the contents in run time memory. It releases the memory once the final PDF document instance is disposed. 

The following code shows how to split the PDF document

{% highlight c# %}
[C#]      

//Loads the PDF document

PdfLoadedDocument ldocument = new PdfLoadedDocument("large.pdf");

//Splits the document

ldocument.Split("splited.pdf");

//Closes the document

ldocument.Close(true);



{% endhighlight %}



{% highlight vb.net %}
[VB]

'Loads the PDF document

Dim ldocument As New PdfLoadedDocument("large.pdf")

'Splits the document

ldocument.Split("splited.pdf")

'Closes the document

ldocument.Close(True)



{% endhighlight %}

The following code shows how to merge the PDF documents.

{% highlight c# %}
[C#]



//Input documents

string[] inputDocuments = Directory.GetFiles("../../Data/Split");

//Creates a PDF document

PdfDocument document = new PdfDocument();

//Merges the document

PdfDocumentBase.Merge(document, inputDocuments);

//Saves and closes the document

document.Save("Output.pdf");

document.Close(true);



{% endhighlight %}



{% highlight vb.net %}
[VB.NET]

'Input documents

Dim inputDocuments As String() = Directory.GetFiles("../../Data/Split")

'Creates a PDF document

Dim document As New PdfDocument()

'Merges the document

PdfDocumentBase.Merge(document, inputDocuments)

'Saves and closes the document

document.Save("Output.pdf")

document.Close(True)



{% endhighlight %}



