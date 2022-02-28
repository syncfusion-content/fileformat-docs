---
title: Merge PDF Documents | Syncfusion
description: Learn how to merge or combine multiple PDF documents as one and how to import pages from one document to another using Syncfusion .NET PDF library
platform: file-formats
control: PDF
documentation: UG
---
# Merge PDF Documents using .NET PDF Library

Essential PDF supports [merging multiple PDF](https://www.syncfusion.com/pdf-framework/net/pdf-library/split-merge-pdf) documents from disk and stream.

## Merging multiple documents from disk and stream

You can merge the multiple PDF document using [Merge](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfDocumentBase.html#Syncfusion_Pdf_PdfDocumentBase_Merge_Syncfusion_Pdf_PdfDocumentBase_Syncfusion_Pdf_Parsing_PdfLoadedDocument_) method of [PdfDocumentBase](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfDocumentBase.html) class, by specifying the path of the documents in a string array.

Refer to the following code example to merge multiple documents from disk.

{% tabs %}
{% highlight c# %}

//Creates a new PDF document

PdfDocument finalDoc = new PdfDocument();

// Creates a string array of source files to be merged.

string[] source = { "file1.pdf", "file2.pdf" };

// Merges PDFDocument.

PdfDocument.Merge(finalDoc, source);

//Saves the final document

finalDoc.Save("Sample.pdf");

//Closes the document

finalDoc.Close(true);



{% endhighlight %}



{% highlight vb.net %}

'Creates a new PDF document

Dim finalDoc As New PdfDocument()

' Creates a string array of source files to be merged.

Dim source As String() = {"file1.pdf", "file2.pdf"}

' Merges PDFDocument.

PdfDocument.Merge(finalDoc, source)

'Saves the final document

finalDoc.Save("Sample.pdf")

'Closes the document

finalDoc.Close(True)



{% endhighlight %}

{% highlight UWP %}

//Due to platform limitations, the PDF file cannot be loaded from disk. However, you can merge specified document using the following code snippet.

//Create the file open picker

var picker = new FileOpenPicker();

picker.FileTypeFilter.Add(".pdf");

//Browse and choose the file

StorageFile file = await picker.PickSingleFileAsync();

//Creates an empty PDF loaded document instance

PdfLoadedDocument loadedDocument = new PdfLoadedDocument();

//Loads or opens an existing PDF document through Open method of PdfLoadedDocument class

await loadedDocument.OpenAsync(file);

//Create a new PDF document

PdfDocument document = new PdfDocument();

//Merge the document 

PdfDocumentBase.Merge(document, loadedDocument);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the documents

document.Close(true);

loadedDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respective code samples

Save(stream, "Sample.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Due to platform limitations, the PDF file cannot be loaded from disk. However, you can merge multiple documents from stream using the following code snippet.

//Creates a PDF document

PdfDocument finalDoc = new PdfDocument();

FileStream stream1 = new FileStream("file1.pdf", FileMode.Open, FileAccess.Read);

FileStream stream2 = new FileStream("file2.pdf", FileMode.Open, FileAccess.Read);

// Creates a PDF stream for merging

Stream[] streams = { stream1, stream2 };

// Merges PDFDocument.

PdfDocumentBase.Merge(finalDoc, streams);

//Save the document into stream

MemoryStream stream = new MemoryStream();

finalDoc.Save(stream);

stream.Position = 0;

//Close the document

finalDoc.Close(true);

//Disposes the streams.

stream1.Dispose();

stream2.Dispose();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "sample.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Due to platform limitations, the PDF file cannot be loaded from disk. However, you can merge multiple documents from stream using the following code snippet.

//Loads the file as stream

Stream stream1 = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.file1.pdf");

Stream stream2 = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.file2.pdf");

//Creates a PDF stream for merging

Stream[] source = { stream1, stream2 };

//Create a new PDF document

PdfDocument document = new PdfDocument();            

//Merge the documents

PdfDocumentBase.Merge(document, source);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the documents

document.Close(true);

//Save the stream into PDF file

//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples

if (Device.RuntimePlatform == Device.UWP)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Sample.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Sample.pdf", "application/pdf", stream);
}

{% endhighlight %}
{% endtabs %}

You can merge the PDF document streams by using the following code example.

{% tabs %}
{% highlight c# %}

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

{% highlight UWP %}

//PDF supports merging multiple documents from stream only in Windows Forms, WPF, ASP.NET, ASP.NET MVC, ASP.NET Core and Xamarin platforms. However, you can merge specified document using the following code snippet.

//Load the PDF document as stream

Stream pdfStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.file1.pdf");

//Creates an empty PDF loaded document instance

PdfLoadedDocument loadedDocument = new PdfLoadedDocument();

//Loads or opens an existing PDF document through Open method of PdfLoadedDocument class

await loadedDocument.OpenAsync(pdfStream);

//Create a new PDF document

PdfDocument document = new PdfDocument();

//Merge the document 

PdfDocumentBase.Merge(document, loadedDocument);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the documents

document.Close(true);

loadedDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples

Save(stream, "Sample.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Creates a PDF document

PdfDocument finalDoc = new PdfDocument();

FileStream stream1 = new FileStream("file1.pdf", FileMode.Open, FileAccess.Read);

FileStream stream2 = new FileStream("file2.pdf", FileMode.Open, FileAccess.Read);

// Creates a PDF stream for merging

Stream[] streams = { stream1, stream2 };

// Merges PDFDocument.

PdfDocumentBase.Merge(finalDoc, streams);

//Save the document into stream

MemoryStream stream = new MemoryStream();

finalDoc.Save(stream);

stream.Position = 0;

//Close the document

finalDoc.Close(true);

//Disposes the streams.

stream1.Dispose();

stream2.Dispose();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "sample.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Loads the file as stream

Stream stream1 = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.file1.pdf");

Stream stream2 = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.file2.pdf");

//Creates a PDF stream for merging

Stream[] source = { stream1, stream2 };

//Create a new PDF document

PdfDocument document = new PdfDocument();            

//Merge the documents

PdfDocumentBase.Merge(document, source);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the documents

document.Close(true);

//Save the stream into PDF file

//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples

if (Device.RuntimePlatform == Device.UWP)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Sample.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Sample.pdf", "application/pdf", stream);
}

{% endhighlight %}
{% endtabs %}

## Importing pages from multiple documents

Essential PDF provides support for importing the pages from one document to another document using [ImportPage](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfDocumentBase.html#Syncfusion_Pdf_PdfDocumentBase_ImportPage_Syncfusion_Pdf_Parsing_PdfLoadedDocument_Syncfusion_Pdf_PdfPageBase_) method. The following code illustrates this. The imported page is added to the end of the original document.

{% tabs %}
{% highlight c# %}     

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

{% highlight UWP %}

//Create the file open picker

var picker = new FileOpenPicker();

picker.FileTypeFilter.Add(".pdf");

//Browse and chose the file

StorageFile file = await picker.PickSingleFileAsync();

//Creates an empty PDF loaded document instance

PdfLoadedDocument lDoc = new PdfLoadedDocument();

//Loads or opens an existing PDF document through Open method of PdfLoadedDocument class

await lDoc.OpenAsync(file);

//Creates a new document

PdfDocument document = new PdfDocument();

//Imports the page at 1 from the lDoc

document.ImportPage(lDoc, 1);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Closes the document

document.Close(true);

lDoc.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "sample.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document.

FileStream docStream = new FileStream("file1.pdf", FileMode.Open, FileAccess.Read);

//Load the PDF document.

PdfLoadedDocument lDoc = new PdfLoadedDocument(docStream);

//Creates a new document

PdfDocument document = new PdfDocument();

//Imports the page at 1 from the lDoc

document.ImportPage(lDoc, 1);

//Save the document into stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

stream.Position = 0;

//Closes the document

document.Close(true);

lDoc.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "sample.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample.pdf");

PdfLoadedDocument lDoc = new PdfLoadedDocument(docStream);

//Creates a new document

PdfDocument document = new PdfDocument();

//Imports the page at 1 from the lDoc

document.ImportPage(lDoc, 1);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Closes the document

document.Close(true);

lDoc.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("sample.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("sample.pdf", "application/pdf", stream);
}

{% endhighlight %}
{% endtabs %}

You can import multiple pages from an existing document by using [ImportPageRange](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfDocumentBase.html#Syncfusion_Pdf_PdfDocumentBase_ImportPageRange_Syncfusion_Pdf_Parsing_PdfLoadedDocument_System_Int32_System_Int32_) method. The following code example illustrates this.

{% tabs %}
{% highlight c# %}      

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

{% highlight UWP %}

//Create the file open picker

var picker = new FileOpenPicker();

picker.FileTypeFilter.Add(".pdf");

//Browse and chose the file

StorageFile file = await picker.PickSingleFileAsync();

//Creates an empty PDF loaded document instance

PdfLoadedDocument lDoc = new PdfLoadedDocument();

//Loads or opens an existing PDF document through Open method of PdfLoadedDocument class

await lDoc.OpenAsync(file);

//Creates a new document

PdfDocument document = new PdfDocument();

//Imports the page at 1 from the lDoc

document.ImportPageRange(lDoc, 0, lDoc.Pages.Count - 1);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Closes the document

document.Close(true);

lDoc.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "sample.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document.

FileStream docStream = new FileStream("file1.pdf", FileMode.Open, FileAccess.Read);

//Load the PDF document.

PdfLoadedDocument lDoc = new PdfLoadedDocument(docStream);

//Creates a new document

PdfDocument document = new PdfDocument();

//Imports the page at 1 from the lDoc

document.ImportPageRange(lDoc, 0, lDoc.Pages.Count - 1);

//Save the document into stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

stream.Position = 0;

//Closes the document

document.Close(true);

lDoc.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "sample.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.file1.pdf");

PdfLoadedDocument lDoc = new PdfLoadedDocument(docStream);

//Creates a new document

PdfDocument document = new PdfDocument();

//Imports the page at 1 from the lDoc

document.ImportPageRange(lDoc, 0, lDoc.Pages.Count - 1);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Closes the document

document.Close(true);

lDoc.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("sample.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("sample.pdf", "application/pdf", stream);
}

{% endhighlight %}
{% endtabs %}

You can also import pages from multiple documents and arrange the pages as required. The following code example explains the same.

{% tabs %}
{% highlight c# %}      

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

{% highlight UWP %}

//Load the PDF document as stream
Stream pdfStream1 = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.file1.pdf");

//Creates an empty PDF loaded document instance
PdfLoadedDocument lDoc = new PdfLoadedDocument(pdfStream1);

//Load the PDF document as stream
Stream pdfStream2 = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.file2.pdf");

//Creates an empty PDF loaded document instance
PdfLoadedDocument lDoc2 = new PdfLoadedDocument(pdfStream2);

//Creates the new document

PdfDocument document = new PdfDocument();

//Imports and arranges the pages

document.ImportPage(lDoc, 2);

document.ImportPage(lDoc2, 1);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Closes the documents

document.Close(true);

lDoc.Close(true);

lDoc2.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "sample.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document.

FileStream docStream1 = new FileStream("file1.pdf", FileMode.Open, FileAccess.Read);

//Load the PDF document.

PdfLoadedDocument lDoc = new PdfLoadedDocument(docStream1);

//Load the PDF document.

FileStream docStream2 = new FileStream("file2.pdf", FileMode.Open, FileAccess.Read);

//Load the PDF document.

PdfLoadedDocument lDoc2 = new PdfLoadedDocument(docStream2);

//Creates the new document

PdfDocument document = new PdfDocument();

//Imports and arranges the pages

document.ImportPage(lDoc, 1);

document.ImportPage(lDoc2, 0);

//Save the document into stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

stream.Position = 0;

//Closes the documents

document.Close(true);

lDoc.Close(true);

lDoc2.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "sample.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream

Stream docStream1 = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.file1.pdf");

PdfLoadedDocument lDoc = new PdfLoadedDocument(docStream1);

//Load the file as stream

Stream docStream2 = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.file2.pdf");

PdfLoadedDocument lDoc2 = new PdfLoadedDocument(docStream2);

//Creates the new document

PdfDocument document = new PdfDocument();

//Imports and arranges the pages

document.ImportPage(lDoc, 1);

document.ImportPage(lDoc2, 0);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Closes the documents

document.Close(true);

lDoc.Close(true);

lDoc2.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code sample

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("sample.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("sample.pdf", "application/pdf", stream);
}

{% endhighlight %}
{% endtabs %}

## Best practices

Merging multiple large PDF documents can lead to high runtime memory. So, you can split the documents into multiple documents and later you can merge. This method avoids the extensive memory usage and increases the performance.

N> Note:  The parent PDF document has all the contents in run time memory. It releases the memory once the final PDF document instance is disposed. 

You can split a large PDF document into multiple documents using [Split](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html#Syncfusion_Pdf_Parsing_PdfLoadedDocument_Split_System_String_) method of [PdfLoadedDocument](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html) class. The following code snippet explains this.

{% tabs %}
{% highlight c# %}      

//Loads the PDF document

PdfLoadedDocument loadedDocument = new PdfLoadedDocument("large.pdf");

//Splits the document

loadedDocument.Split("split.pdf");

//Closes the document

loadedDocument.Close(true);



{% endhighlight %}



{% highlight vb.net %}

'Loads the PDF document

Dim loadedDocument As New PdfLoadedDocument("large.pdf")

'Splits the document

loadedDocument.Split("split.pdf")

'Closes the document

loadedDocument.Close(True)



{% endhighlight %}

{% highlight UWP %}

//Due to platform limitations, multiple PDF files cannot be saved to disk. So, Essential PDF supports splitting the document into multiple documents only in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms.

{% endhighlight %}

{% highlight ASP.NET Core %}

//Due to platform limitations, multiple PDF files cannot be saved to disk. So, Essential PDF supports splitting the document into multiple documents only in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms.

{% endhighlight %}

{% highlight Xamarin %}

//Due to platform limitations, multiple PDF files cannot be saved to disk. So, Essential PDF supports splitting the document into multiple documents only in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms.

{% endhighlight %}
{% endtabs %}

The following code shows how to merge multiple PDF documents.

{% tabs %}
{% highlight c# %}



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

{% highlight UWP %}

//Due to platform limitations, the PDF file cannot be loaded from disk. However, you can merge specified document using the following code snippet.

//Create the file open picker

var picker = new FileOpenPicker();

picker.FileTypeFilter.Add(".pdf");

//Browse and choose the file

StorageFile file = await picker.PickSingleFileAsync();

//Creates an empty PDF loaded document instance

PdfLoadedDocument loadedDocument = new PdfLoadedDocument();

//Loads or opens an existing PDF document through Open method of PdfLoadedDocument class

await loadedDocument.OpenAsync(file);

//Create a new PDF document

PdfDocument document = new PdfDocument();

//Merge the document 

PdfDocumentBase.Merge(document, loadedDocument);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the documents

document.Close(true);

loadedDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respective code samples

Save(stream, "Sample.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Due to platform limitations, the PDF file cannot be loaded from disk. However, you can merge multiple documents from stream using the following code snippet.

//Creates a PDF document

PdfDocument finalDoc = new PdfDocument();

FileStream stream1 = new FileStream("file1.pdf", FileMode.Open, FileAccess.Read);

FileStream stream2 = new FileStream("file2.pdf", FileMode.Open, FileAccess.Read);

// Creates a PDF stream for merging

Stream[] streams = { stream1, stream2 };

// Merges PDFDocument.

PdfDocumentBase.Merge(finalDoc, streams);

//Save the document into stream

MemoryStream stream = new MemoryStream();

finalDoc.Save(stream);

stream.Position = 0;

//Close the document

finalDoc.Close(true);

//Disposes the streams.

stream1.Dispose();

stream2.Dispose();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "sample.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Due to platform limitations, the PDF file cannot be loaded from disk. However, you can merge multiple documents from stream using the following code snippet.

//Loads the file as stream

Stream stream1 = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.file1.pdf");

Stream stream2 = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.file2.pdf");

//Creates a PDF stream for merging

Stream[] source = { stream1, stream2 };

//Create a new PDF document

PdfDocument document = new PdfDocument();            

//Merge the documents

PdfDocumentBase.Merge(document, source);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the documents

document.Close(true);

//Save the stream into PDF file

//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples

if (Device.RuntimePlatform == Device.UWP)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Sample.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Sample.pdf", "application/pdf", stream);
}

{% endhighlight %}
{% endtabs %}

## Optimizing PDF resources when merging PDF documents

Essential PDF provides support to optimize the PDF resources when merging PDF documents. You can optimize the resources by enabling the OptimizeResources property available in the PdfMergeOptions instance.

Refer to the following code example to optimize the PDF resources when merging PDF documents.

{% tabs %}
{% highlight c# %} 

//Creates a new PDF document

PdfDocument finalDoc = new PdfDocument();

//Creates a string array of source files to be merged

string[] source = { "file1.pdf", "file2.pdf" };

PdfMergeOptions mergeOptions = new PdfMergeOptions();

//Enable Optimize Resources
mergeOptions.OptimizeResources = true;

//Merges PDFDocument

PdfDocument.Merge(finalDoc, mergeOptions, source);

//Saves the final document

finalDoc.Save("Sample.pdf");

//Closes the document

finalDoc.Close(true); 

{% endhighlight %}



{% highlight vb.net %}

'Creates a new PDF document

 Dim finalDoc As New PdfDocument()

'Creates a string array of source files to be merged

 Dim source As String() = {"file1.pdf", "file2.pdf"}

 Dim mergeOptions As New PdfMergeOptions()

 'Enable Optimize Resources
 mergeOptions.OptimizeResources = True

 'Merges PDFDocument

 PdfDocument.Merge(finalDoc, mergeOptions, source)

 'Saves the final document

 finalDoc.Save("Sample.pdf")

 'Closes the document

 finalDoc.Close(True)

 {% endhighlight %}


 {% highlight ASP.NET Core %}

 //Due to platform limitations, the PDF file cannot be loaded from disk. However, you can optimize PDF resources when merging multiple documents from stream using the following code snippet

//Creates a PDF document

PdfDocument finalDoc = new PdfDocument();

FileStream stream1 = new FileStream("file1.pdf", FileMode.Open, FileAccess.Read);

FileStream stream2 = new FileStream("file2.pdf", FileMode.Open, FileAccess.Read);

//Creates a PDF stream for merging

Stream[] streams = { stream1, stream2 };

PdfMergeOptions mergeOptions = new PdfMergeOptions();

//Enable Optimize Resources
mergeOptions.OptimizeResources = true;

//Merges PDFDocument

PdfDocumentBase.Merge(finalDoc, mergeOptions, streams);

//Save the document into stream

MemoryStream stream = new MemoryStream();

finalDoc.Save(stream);

stream.Position = 0;

//Close the document

finalDoc.Close(true);

//Disposes the streams

stream1.Dispose();

stream2.Dispose();

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "sample.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Due to platform limitations, the PDF file cannot be loaded from disk. However, you can optimize PDF resources when merging multiple documents from stream using the following code snippet

//Loads the file as stream

Stream stream1 = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.file1.pdf");

Stream stream2 = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.file2.pdf");

//Creates a PDF stream for merging

Stream[] source = { stream1, stream2 };

//Create a new PDF document

PdfDocument document = new PdfDocument();

PdfMergeOptions mergeOptions = new PdfMergeOptions();

//Enable Optimize Resources
mergeOptions.OptimizeResources = true;

//Merge the documents

PdfDocumentBase.Merge(document, mergeOptions, source);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the documents

document.Close(true);

//Save the stream into PDF file

//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
       Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Sample.pdf", "application/pdf", stream);
}
else
{
       Xamarin.Forms.DependencyService.Get<ISave>().Save("Sample.pdf", "application/pdf", stream);
}

{% endhighlight %}
{% endtabs %}

## Reducing the size of the PDF file while importing pages

Essential PDF provides support for optimization of memory using EnableMemoryOptimization property in the PdfDocument instance. Optimization will be effective only with merge, append and import functions. Enabling this property will optimize the memory but a difference in time occurs based on the document size.

For example, if the PDF document has 100 pages and each page has an image in common. If we import those document pages with the EnableMemoryOptimization disabled (by default it is disabled). We will clone the image resource for each page separately. That leads to the imported document having a huge size when compared to the source PDF. If we enable the EnableMemoryOptimization, we won’t clone any resources from the source. That does not cause any PDF file size issue. Moreover, it does not cause any memory leak issues. So, without any hassle, you can enable the EnableMemoryOptimization property whenever you need this behavior.

Refer to the following code snippet to reduce the PDF file size while importing pages from multiple documents.
{% tabs %}
{% highlight c# %}     

//Load the document.

PdfLoadedDocument lDoc = new PdfLoadedDocument("file1.pdf");

//Create a new document.

PdfDocument document = new PdfDocument();

//Enable memory optimization.

document.EnableMemoryOptimization = true;

//Import the page at 1 from the lDoc.

document.ImportPageRange(lDoc, 0, 1);

//Save the document.

document.Save("sample.pdf");

//Close the document.

document.Close(true);

lDoc.Close(true);


{% endhighlight %}



{% highlight vb.net %}

'Load the document.

Dim lDoc As New PdfLoadedDocument("file1.pdf")

'Create a new document.

Dim document As New PdfDocument()

'Enable memory optimization.

document.EnableMemoryOptimization= true

'Import the page at 1 from the lDoc

document.ImportPageRange(lDoc, 0, 1)

'Save the document.

document.Save("sample.pdf")

'Close the document.

document.Close(True)

lDoc.Close(True)


{% endhighlight %}


{% highlight ASP.NET Core %}

//Load the PDF document.

FileStream docStream = new FileStream("file1.pdf", FileMode.Open, FileAccess.Read);

//Create a PDF document.

PdfLoadedDocument lDoc = new PdfLoadedDocument(docStream);

//Create a new document.

PdfDocument document = new PdfDocument();

//Enable memory optimization.

document.EnableMemoryOptimization= true;

//Import the page at 1 from the lDoc.

document.ImportPageRange(lDoc, 0, 1);

//Save the document as stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

stream.Position = 0;

//Close the document.

document.Close(true);

lDoc.Close(true);

//Define the ContentType for the pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "sample.pdf";

//Create a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% endtabs %}

## Extend the margin of the PDF pages while merging PDF document

The ['Syncfusion PDF library'](https://www.syncfusion.com/pdf-framework/net) provides support for extending the margins of the pdf pages by using the ['ExtendMargin'](https://help.syncfusion.com/cr/aspnet/Syncfusion.Pdf.PdfMergeOptions.html#Syncfusion_Pdf_PdfMergeOptions_ExtendMargin) property available from the ['PdfMergeOptions'](https://help.syncfusion.com/cr/aspnet/Syncfusion.Pdf.PdfMergeOptions.html) class. When ExtendMargin is set to true, then a specified margin is considered while merging the existing documents. 
 The following code sample illustrates this.

{% tabs %}
{% highlight c# %}

 
//Create a new PDF document

PdfDocument finalDoc = new PdfDocument();

//Create new instance for the document margin.
PdfMargins margin = new PdfMargins();

margin.All = 40;

//Create a string array of source files to be merged

string[] source = { "file1.pdf", "file2.pdf" };

PdfMergeOptions mergeOptions = new PdfMergeOptions();

// Enable the Extend Margin Property
mergeOptions.ExtendMargin=true;

//Merge PDFDocument

PdfDocument.Merge(finalDoc, mergeOptions, source);

//Save the final document

finalDoc.Save("Sample.pdf");

//Close the document

finalDoc.Close(true);


{% endhighlight %}



{% highlight vb.net %}

'Create a new PDF document

 Dim finalDoc As New PdfDocument()
'Create new instance for the document margin.
Dim margin As PdfMargins = New PdfMargins()
margin.All = 40

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

{% highlight ASP.NET Core %}
//Due to platform limitations, the PDF file cannot be loaded from disk. However, you can optimize PDF resources when merging multiple documents from a stream using the following code snippet

//Create a PDF document

PdfDocument finalDoc = new PdfDocument();

//Create new instance for the document margin.
PdfMargins margin= new PdfMargins();
margin.All=40;

FileStream stream1 = new FileStream("file1.pdf", FileMode.Open, FileAccess.Read);

FileStream stream2 = new FileStream("file2.pdf", FileMode.Open, FileAccess.Read);

//Create a PDF stream for merging

Stream[] streams = { stream1, stream2 };

PdfMergeOptions mergeOptions = new PdfMergeOptions();

//Enable the Extend Margin
mergeOptions.ExtendMargin = true;

//Merge PDFDocument

PdfDocumentBase.Merge(finalDoc, mergeOptions, streams);

//Save the document into stream

MemoryStream stream = new MemoryStream();

finalDoc.Save(stream);

stream.Position = 0;

//Close the document

finalDoc.Close(true);

//Dispose the stream

stream1.Dispose();

stream2.Dispose();

//Define the ContentType for the pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "sample.pdf";

//Create a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% endtabs %}
