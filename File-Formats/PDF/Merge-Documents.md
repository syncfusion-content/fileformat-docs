---
title: Merge PDF Documents | Syncfusion
description: Learn how to merge or combine multiple PDF documents as one and how to import pages from one document to another using Syncfusion .NET PDF library
platform: file-formats
control: PDF
documentation: UG
---
# Merge PDF Documents using .NET PDF Library

Essential PDF supports [merging multiple PDF](https://www.syncfusion.com/document-processing/pdf-framework/net/pdf-library/merge-pdf) documents from disk and stream.

## Merging multiple documents from disk and stream

You can merge the multiple PDF document using [Merge](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfDocumentBase.html#Syncfusion_Pdf_PdfDocumentBase_Merge_Syncfusion_Pdf_PdfDocumentBase_Syncfusion_Pdf_Parsing_PdfLoadedDocument_) method of [PdfDocumentBase](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfDocumentBase.html) class, by specifying the path of the documents in a string array.

Refer to the following code example to merge multiple documents from disk.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//Due to platform limitations, the PDF file cannot be loaded from disk. However, you can merge multiple documents from stream using the following code snippet.
//Creates a PDF document.
PdfDocument finalDoc = new PdfDocument();
FileStream stream1 = new FileStream("file1.pdf", FileMode.Open, FileAccess.Read);
FileStream stream2 = new FileStream("file2.pdf", FileMode.Open, FileAccess.Read);
//Creates a PDF stream for merging.
Stream[] streams = { stream1, stream2 };
//Merges PDFDocument.
PdfDocumentBase.Merge(finalDoc, streams);

//Save the document into stream.
MemoryStream stream = new MemoryStream();
finalDoc.Save(stream);
//Close the document.
finalDoc.Close(true);
//Disposes the streams.
stream1.Dispose();
stream2.Dispose();

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Creates a new PDF document.
PdfDocument finalDoc = new PdfDocument();
//Creates a string array of source files to be merged.
string[] source = { "file1.pdf", "file2.pdf" };
//Merges PDFDocument.
PdfDocument.Merge(finalDoc, source);

//Saves the final document.
finalDoc.Save("Sample.pdf");
//Closes the document.
finalDoc.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Creates a new PDF document.
Dim finalDoc As New PdfDocument()
'Creates a string array of source files to be merged.
Dim source As String() = {"file1.pdf", "file2.pdf"}
'Merges PDFDocument.
PdfDocument.Merge(finalDoc, source)

'Saves the final document.
finalDoc.Save("Sample.pdf")
'Closes the document.
finalDoc.Close(True)

{% endhighlight %}

{% endtabs %}

You can merge the PDF document streams by using the following code example.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//Creates a PDF document.
PdfDocument finalDoc = new PdfDocument();
FileStream stream1 = new FileStream("file1.pdf", FileMode.Open, FileAccess.Read);
FileStream stream2 = new FileStream("file2.pdf", FileMode.Open, FileAccess.Read);
//Creates a PDF stream for merging.
Stream[] streams = { stream1, stream2 };
//Merges PDFDocument.
PdfDocumentBase.Merge(finalDoc, streams);

//Save the document into stream.
MemoryStream stream = new MemoryStream();
finalDoc.Save(stream);
//Close the document.
finalDoc.Close(true);
//Disposes the streams.
stream1.Dispose();
stream2.Dispose();

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Creates a PDF document.
PdfDocument finalDoc = new PdfDocument();
Stream stream1 = File.OpenRead("file1.pdf");
Stream stream2 = File.OpenRead("file2.pdf");
//Creates a PDF stream for merging.
Stream[] streams = { stream1, stream2 };
//Merges PDFDocument.
PdfDocumentBase.Merge(finalDoc, streams);

//Saves the document.
finalDoc.Save("sample.pdf");
//Closes the document.
finalDoc.Close(true);
//Disposes the streams.
stream1.Dispose();
stream2.Dispose();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Creates a PDF document.
Dim finalDoc As New PdfDocument()
Dim stream1 As Stream = File.OpenRead("file1.pdf")
Dim stream2 As Stream = File.OpenRead("file2.pdf")
'Creates a PDF stream for merging.
Dim streams As Stream() = {stream1, stream2}
'Merges PDFDocument.
PdfDocumentBase.Merge(finalDoc, streams)

'Saves the document.
finalDoc.Save("sample.pdf")
'Closes the document.
finalDoc.Close(True)
'Disposes the streams.
stream1.Dispose()
stream2.Dispose()

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Merge%20PDFs/Merge-multiple-documents-from-stream/). 

## Importing pages from multiple documents

Essential PDF provides support for importing the pages from one document to another document using [ImportPage](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfDocumentBase.html#Syncfusion_Pdf_PdfDocumentBase_ImportPage_Syncfusion_Pdf_Parsing_PdfLoadedDocument_Syncfusion_Pdf_PdfPageBase_) method. The following code illustrates this. The imported page is added to the end of the original document.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//Load the PDF document.
FileStream docStream = new FileStream("file1.pdf", FileMode.Open, FileAccess.Read);
//Load the PDF document.
PdfLoadedDocument lDoc = new PdfLoadedDocument(docStream);
//Create a new document.
PdfDocument document = new PdfDocument();
//Imports the page at 1 from the lDoc.
document.ImportPage(lDoc, 1);

//Save the document into stream.
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Closes the document.
document.Close(true);
lDoc.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Load the PDF document.
PdfLoadedDocument lDoc = new PdfLoadedDocument("file1.pdf");
//Create a new document.
PdfDocument document = new PdfDocument();
//Imports the page at 1 from the lDoc.
document.ImportPage(lDoc, 1);

//Save the document.
document.Save("sample.pdf");
//Close the document.
document.Close(true);
lDoc.Close(true)

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Load the PDF document
Dim lDoc As New PdfLoadedDocument("file1.pdf")
'Creates a new document
Dim document As New PdfDocument()
'Imports the page at 1 from the lDoc
document.ImportPage(lDoc, 1)

'Save the document
document.Save("sample.pdf")
'Close the document
document.Close(True)
lDoc.Close(True)

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Merge%20PDFs/Importing-pages-from-one-document-another-document/). 

You can import multiple pages from an existing document by using [ImportPageRange](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfDocumentBase.html#Syncfusion_Pdf_PdfDocumentBase_ImportPageRange_Syncfusion_Pdf_Parsing_PdfLoadedDocument_System_Int32_System_Int32_) method. The following code example illustrates this.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//Load the PDF document.
FileStream docStream = new FileStream("file1.pdf", FileMode.Open, FileAccess.Read);
//Load the PDF document.
PdfLoadedDocument lDoc = new PdfLoadedDocument(docStream);
//Create a new document.
PdfDocument document = new PdfDocument();
//Imports the page at 1 from the lDoc.
document.ImportPageRange(lDoc, 0, lDoc.Pages.Count - 1);

//Save the document into stream.
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Closes the document.
document.Close(true);
lDoc.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Loads PDF document.
PdfLoadedDocument lDoc = new PdfLoadedDocument("file1.pdf");
//Create a new document.
PdfDocument document = new PdfDocument();
//Imports the pages from the lDoc.
document.ImportPageRange(lDoc, 0, lDoc.Pages.Count - 1);

//Save the document.
document.Save("sample.pdf");
//Closes the documents.
document.Close(true);
lDoc.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

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

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Merge%20PDFs/Import-multiple-pages-from-an-existing-PDF).

You can also import pages from multiple documents and arrange the pages by using [ImportPage](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfDocumentBase.html#Syncfusion_Pdf_PdfDocumentBase_ImportPage_Syncfusion_Pdf_Parsing_PdfLoadedDocument_Syncfusion_Pdf_PdfPageBase_) method. The following code example explains the same.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//Load the PDF document.
FileStream docStream1 = new FileStream("file1.pdf", FileMode.Open, FileAccess.Read);
//Load the PDF document.
PdfLoadedDocument lDoc = new PdfLoadedDocument(docStream1);
//Load the PDF document.
FileStream docStream2 = new FileStream("file2.pdf", FileMode.Open, FileAccess.Read);
//Load the PDF document.
PdfLoadedDocument lDoc2 = new PdfLoadedDocument(docStream2);
//Create the new document.
PdfDocument document = new PdfDocument();
//Imports and arranges the pages.
document.ImportPage(lDoc, 1);
document.ImportPage(lDoc2, 0);

//Save the document into stream.
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Closes the documents.
document.Close(true);
lDoc.Close(true);
lDoc2.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Loads document.
PdfLoadedDocument lDoc = new PdfLoadedDocument("file1.pdf");
//Loads document.
PdfLoadedDocument lDoc2 = new PdfLoadedDocument("file1.pdf");
//Create the new document.
PdfDocument document = new PdfDocument();
//Imports and arranges the pages.
document.ImportPage(lDoc, 2);
document.ImportPage(lDoc2, 1);

//Saves the document.
document.Save("sample.pdf");
//Closes the documents.
document.Close(true);
lDoc.Close(true);
lDoc2.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

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

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Merge%20PDFs/Import-pages-from-multiple-documents-and-arrange-pages/). 

## Best practices

Merging multiple large PDF documents can lead to high runtime memory. So, you can split the documents into multiple documents and later you can merge. This method avoids the extensive memory usage and increases the performance.

N> Note:  The parent PDF document has all the contents in run time memory. It releases the memory once the final PDF document instance is disposed. 

You can split a large PDF document into multiple documents using [Split](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html#Syncfusion_Pdf_Parsing_PdfLoadedDocument_Split_System_String_) method of [PdfLoadedDocument](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html) class. The following code snippet explains this.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//PDF doesn't support splitting the document into multiple documents C#.NET Cross platforms.

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Loads the PDF document.
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("large.pdf");
//Splits the document.
loadedDocument.Split("split.pdf");
//Close the document.
loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Loads the PDF document
Dim loadedDocument As New PdfLoadedDocument("large.pdf")
'Splits the document
loadedDocument.Split("split.pdf")
'Close the document
loadedDocument.Close(True)

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Merge%20PDFs/Split-large-PDF-to-multiple-documents). 

The following code shows how to merge multiple PDF documents using [Merge](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfDocumentBase.html#Syncfusion_Pdf_PdfDocumentBase_Merge_Syncfusion_Pdf_PdfDocumentBase_System_Object___) method.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//Due to platform limitations, the PDF file cannot be loaded from disk. However, you can merge multiple documents from stream using the following code snippet.

//Creates a PDF document.
PdfDocument finalDoc = new PdfDocument();
//Load the PDF document.
FileStream stream1 = new FileStream("file1.pdf", FileMode.Open, FileAccess.Read);
FileStream stream2 = new FileStream("file2.pdf", FileMode.Open, FileAccess.Read);
//Creates a PDF stream for merging.
Stream[] streams = { stream1, stream2 };
//Merges PDFDocument.
PdfDocumentBase.Merge(finalDoc, streams);

//Save the document into stream.
MemoryStream stream = new MemoryStream();
finalDoc.Save(stream);
//Close the document.
finalDoc.Close(true);
//Disposes the streams.
stream1.Dispose();
stream2.Dispose();

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Input documents.
string[] inputDocuments = Directory.GetFiles("../../Data/Split");
//Creates a PDF document.
PdfDocument document = new PdfDocument();
//Merges the document.
PdfDocumentBase.Merge(document, inputDocuments);

//Save and close the document.
document.Save("Output.pdf");
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Input documents
Dim inputDocuments As String() = Directory.GetFiles("../../Data/Split")
'Create a PDF document
Dim document As New PdfDocument()
'Merges the document
PdfDocumentBase.Merge(document, inputDocuments)

'Save and close the document
document.Save("Output.pdf")
document.Close(True)

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Merge%20PDFs/Merge-multiple-documents-from-stream/). 

## Optimizing PDF resources when merging PDF documents

Essential PDF provides support to optimize the PDF resources when merging PDF documents. You can optimize the resources by enabling the [OptimizeResources](https://help.syncfusion.com/cr/aspnet/Syncfusion.Pdf.PdfMergeOptions.html#Syncfusion_Pdf_PdfMergeOptions_OptimizeResources) property available in the [PdfMergeOptions](https://help.syncfusion.com/cr/aspnet/Syncfusion.Pdf.PdfMergeOptions.html) class.

Refer to the following code example to optimize the PDF resources when merging PDF documents.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//Due to platform limitations, the PDF file cannot be loaded from disk. However, you can optimize PDF resources when merging multiple documents from stream using the following code snippet.
//Create a PDF document.
PdfDocument finalDoc = new PdfDocument();
//Load the PDF document.
FileStream stream1 = new FileStream("file1.pdf", FileMode.Open, FileAccess.Read);
FileStream stream2 = new FileStream("file2.pdf", FileMode.Open, FileAccess.Read);
//Creates a PDF stream for merging.
Stream[] streams = { stream1, stream2 };
PdfMergeOptions mergeOptions = new PdfMergeOptions();
//Enable Optimize Resources.
mergeOptions.OptimizeResources = true;
//Merges PDFDocument.
PdfDocumentBase.Merge(finalDoc, mergeOptions, streams);

//Save the document into stream.
MemoryStream stream = new MemoryStream();
finalDoc.Save(stream);
//Close the document.
finalDoc.Close(true);
//Disposes the streams.
stream1.Dispose();
stream2.Dispose();

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Create a new PDF document.
PdfDocument finalDoc = new PdfDocument();
//Creates a string array of source files to be merged.
string[] source = { "file1.pdf", "file2.pdf" };
PdfMergeOptions mergeOptions = new PdfMergeOptions();
//Enable Optimize Resources.
mergeOptions.OptimizeResources = true;
//Merges PDFDocument.
PdfDocument.Merge(finalDoc, mergeOptions, source);

//Save the final document.
finalDoc.Save("Sample.pdf");
//Close the document.
finalDoc.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Create a new PDF document
Dim finalDoc As New PdfDocument()
'Creates a string array of source files to be merged
Dim source As String() = {"file1.pdf", "file2.pdf"}
Dim mergeOptions As New PdfMergeOptions()
'Enable Optimize Resources
mergeOptions.OptimizeResources = True
'Merges PDFDocument
PdfDocument.Merge(finalDoc, mergeOptions, source)

'Save the final document
finalDoc.Save("Sample.pdf")
'Close the document
finalDoc.Close(True)

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Merge%20PDFs/Optimize-the-PDF-resources-when-merging-PDF-documents/). 

## Extend the margin of the PDF pages while merging PDF document

The [Syncfusion PDF library](https://www.syncfusion.com/document-processing/pdf-framework/net) provides support for extending the margins of the pdf pages by using the [ExtendMargin](https://help.syncfusion.com/cr/aspnet/Syncfusion.Pdf.PdfMergeOptions.html#Syncfusion_Pdf_PdfMergeOptions_ExtendMargin) property available from the [PdfMergeOptions](https://help.syncfusion.com/cr/aspnet/Syncfusion.Pdf.PdfMergeOptions.html) class. When ExtendMargin is set to true, then a specified margin is considered while merging the existing documents. 

The following code sample illustrates this.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
 
//Due to platform limitations, the PDF file cannot be loaded from disk. However, you can optimize PDF resources when merging multiple documents from a stream using the following code snippet.
//Create a PDF document.
PdfDocument finalDoc = new PdfDocument();
//Create new instance for the document margin.
PdfMargins margin= new PdfMargins();
margin.All=40;
//Set margin.
finalDoc.PageSettings.Margins = margin;
//Load the PDF document.
FileStream stream1 = new FileStream("file1.pdf", FileMode.Open, FileAccess.Read);
FileStream stream2 = new FileStream("file2.pdf", FileMode.Open, FileAccess.Read);
//Create a PDF stream for merging.
Stream[] streams = { stream1, stream2 };
PdfMergeOptions mergeOptions = new PdfMergeOptions();
//Enable the Extend Margin.
mergeOptions.ExtendMargin = true;
//Merge PDFDocument.
PdfDocumentBase.Merge(finalDoc, mergeOptions, streams);

//Save the document into stream.
MemoryStream stream = new MemoryStream();
finalDoc.Save(stream);
//Close the document.
finalDoc.Close(true);
//Dispose the stream.
stream1.Dispose();
stream2.Dispose();

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Create a new PDF document.
PdfDocument finalDoc = new PdfDocument();
//Create new instance for the document margin.
PdfMargins margin = new PdfMargins();
margin.All = 40;
//Set margin.
finalDoc.PageSettings.Margins = margin;
//Create a string array of source files to be merged.
string[] source = { "file1.pdf", "file2.pdf" };
PdfMergeOptions mergeOptions = new PdfMergeOptions();
// Enable the Extend Margin Property.
mergeOptions.ExtendMargin=true;
//Merge PDFDocument.
PdfDocument.Merge(finalDoc, mergeOptions, source);

//Save the final document.
finalDoc.Save("Sample.pdf");
//Close the document.
finalDoc.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Create a new PDF document
Dim finalDoc As New PdfDocument()
'Create new instance for the document margin
Dim margin As PdfMargins = New PdfMargins()
margin.All = 40
'Set margin
finalDoc.PageSettings.Margins = margin
'Create a string array of source files to be merged
Dim source As String() = {"file1.pdf", "file2.pdf"}
Dim mergeOptions As New PdfMergeOptions()
'Enable the Extend Margin Property
mergeOptions.ExtendMargin=true
'Merge PDFDocument
PdfDocument.Merge(finalDoc, mergeOptions, source)

'Save the final document
finalDoc.Save("Sample.pdf")
'Close the document
finalDoc.Close(True)

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Merge%20PDFs/Extend-the-margin-of-PDF-pages-while-merging-PDFs/). 
