---
title: Open and Save PDF file in C# and VB.NET | Syncfusion
description: This page describes how to open and save PDF file from or to file system, and stream in C# and VB.NET using Syncfusion .NET PDF library.
platform: file-formats
control: PDF
documentation: UG
---
# Open and Save PDF file in C# and VB.NET

## Opening an existing PDF document

You can open an existing PDF document by using the [PdfLoadedDocument](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html) class. The following example shows how to load an existing document from physical path.
{% tabs %}
{% highlight c# %}

//Open an existing document from file system 
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");

{% endhighlight %}

{% highlight vb.net %}

'Open an existing document from file system 
Dim loadedDocument As New PdfLoadedDocument("Input.pdf")

{% endhighlight %}

{% highlight UWP %}

//PDF supports opening an existing PDF document from physical path only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

{% endhighlight %}

{% highlight ASP.NET Core %}

//PDF supports opening an existing PDF document from physical path only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

{% endhighlight %}

{% highlight Xamarin %}

//PDF supports opening an existing PDF document from physical path only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

{% endhighlight %}
{% endtabs %}
## Opening an existing PDF document from Stream

You can open an existing document from stream by using [PdfLoadedDocument](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html) class as shown below.
{% tabs %} 
{% highlight c# %}

//Opens an existing document from stream 
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(stream); 

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing document from stream 
Dim loadedDocument As New PdfLoadedDocument(stream)

{% endhighlight %}

{% highlight UWP %}

//Opens an existing document from stream 
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(stream); 

{% endhighlight %}

{% highlight ASP.NET Core %}

//Opens an existing document from stream 
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(stream); 

{% endhighlight %}

{% highlight Xamarin %}

//Opens an existing document from stream 
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(stream); 

{% endhighlight %}
{% endtabs %}
## Opening an existing PDF document from byte array

You can open an existing document from byte array by using [PdfLoadedDocument](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html) class as shown in the below code snippet.
{% tabs %} 
{% highlight c# %}

//Open an existing document from byte array 
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(byteArray); 

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing document from byte array 
Dim loadedDocument As New PdfLoadedDocument(byteArray)

{% endhighlight %}

{% highlight UWP %}

//Open an existing document from byte array 
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(byteArray); 

{% endhighlight %}

{% highlight ASP.NET Core %}

//Open an existing document from byte array 
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(byteArray); 

{% endhighlight %}

{% highlight Xamarin %}

//Open an existing document from byte array 
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(byteArray); 

{% endhighlight %}
{% endtabs %}
## Opening an Encrypted PDF document

You can open an existing encrypted PDF document from either the file system or the stream or the byte array using the following overloads as shown below

{% tabs %}
{% highlight c# %}

//Open an existing encrypted document from disk.
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf", "password");

{% endhighlight %}

{% highlight vb.net %}

'Open an existing encrypted document from disk. 
Dim loadedDocument As New PdfLoadedDocument("Input.pdf","password")

{% endhighlight %}

{% highlight UWP %}

//PDF supports opening an Encrypted PDF document from physical path only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

{% endhighlight %}

{% highlight ASP.NET Core %}

//PDF supports opening an Encrypted PDF document from physical path only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

{% endhighlight %}

{% highlight Xamarin %}

//PDF supports opening an Encrypted PDF document from physical path only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

{% endhighlight %}
{% endtabs %}

{% tabs %} 
{% highlight c# %}


//Open an existing encrypted document from stream.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(stream, "password");



{% endhighlight %}

{% highlight vb.net %}

'Open an existing encrypted document from stream.
Dim loadedDocument As New PdfLoadedDocument(stream,"password")

{% endhighlight %}

{% highlight UWP %}


//Open an existing encrypted document from stream.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(stream, "password");



{% endhighlight %}

{% highlight ASP.NET Core %}


//Open an existing encrypted document from stream.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(stream, "password");



{% endhighlight %}

{% highlight Xamarin %}


//Open an existing encrypted document from stream.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(stream, "password");



{% endhighlight %}
{% endtabs %}

{% tabs %} 
{% highlight c# %}

//Open an existing encrypted document from byte array. 
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(byteArray, "password");

{% endhighlight %}

{% highlight vb.net %}

'Open an existing encrypted document from byte array. 
Dim loadedDocument As New PdfLoadedDocument(byteArray,"password")

{% endhighlight %}

{% highlight UWP %}

//Open an existing encrypted document from byte array. 
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(byteArray, "password");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Open an existing encrypted document from byte array. 
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(byteArray, "password");

{% endhighlight %}

{% highlight Xamarin %}

//Open an existing encrypted document from byte array. 
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(byteArray, "password");

{% endhighlight %}
{% endtabs %}
## Opening a corrupted PDF document

You can open a corrupted PDF document from either the file system or the stream or the byte array using the following overloads as shown below
{% tabs %}
{% highlight c# %}

//Open an existing corrupted document from disk. 
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf", true);

{% endhighlight %}

{% highlight vb.net %}

'Open an existing corrupted document from disk. 
Dim loadedDocument As New PdfLoadedDocument("Input.pdf", True)

{% endhighlight %}

{% highlight UWP %}

//PDF supports opening a corrupted PDF document from physical path only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

{% endhighlight %}

{% highlight ASP.NET Core %}

//PDF supports opening a corrupted PDF document from physical path only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

{% endhighlight %}

{% highlight Xamarin %}

//PDF supports opening a corrupted PDF document from physical path only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

{% endhighlight %}
{% endtabs %}

{% tabs %}
{% highlight c# %}

//Open an existing corrupted document from stream. 
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(stream, true);

{% endhighlight %}

{% highlight vb.net %}

'Open an existing corrupted document from stream. 
Dim loadedDocument As New PdfLoadedDocument(stream, True)

{% endhighlight %}

{% highlight UWP %}

//Open an existing corrupted document from stream. 
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(stream, true);

{% endhighlight %}

{% highlight ASP.NET Core %}

//Open an existing corrupted document from stream. 
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(stream, true);

{% endhighlight %}

{% highlight Xamarin %}

//Open an existing corrupted document from stream. 
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(stream, true);

{% endhighlight %}
{% endtabs %}

{% tabs %}
{% highlight c# %}

//Open an existing corrupted document from byte array. 
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(byteArray, true);

{% endhighlight %}

{% highlight vb.net %}

'Open an existing corrupted document from byte array. 
Dim loadedDocument As New PdfLoadedDocument(byteArray, True)

{% endhighlight %}

{% highlight UWP %}

//Open an existing corrupted document from byte array. 
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(byteArray, true);

{% endhighlight %}

{% highlight ASP.NET Core %}

//Open an existing corrupted document from byte array. 
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(byteArray, true);

{% endhighlight %}

{% highlight Xamarin %}

//Open an existing corrupted document from byte array. 
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(byteArray, true);

{% endhighlight %}
{% endtabs %}

N> 1. The OpenAndRepair overload is capable of resolving basic cross reference offset issues and cannot repair complex document corruption.
N> 2.  Using this overload may cause performance delay when compared with other overloads, due to the repairing process.

## Saving a PDF document to file system

You can save the manipulated PDF document to file system using [Save](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Base~Syncfusion.Pdf.PdfDocumentBase~Save(String).html) method of [PdfLoadedDocument](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html) class.

{% tabs %}
{% highlight c# %}

//Load an existing PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");
//To-Do some manipulation
//To-Do some manipulation
//Save the document in file system
loadedDocument.Save("Output.pdf"); 

{% endhighlight %}

{% highlight vb.net %}

' Load an existing PDF document
Dim loadedDocument As New PdfLoadedDocument("Input.pdf")
'To-Do some manipulation
'To-Do some manipulation
'Save the document in file system
loadedDocument.Save("Output.pdf")

{% endhighlight %}

{% highlight UWP %}

//Load the PDF document as stream
Stream pdfStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Input.pdf");
//Creates an empty PDF loaded document instance
PdfLoadedDocument loadedDocument = new PdfLoadedDocument();
//Loads or opens an existing PDF document through Open method of PdfLoadedDocument class
await loadedDocument.OpenAsync(pdfStream);
//To-Do some manipulation
//To-Do some manipulation
//Save the document into stream.
MemoryStream stream = new MemoryStream();
await loadedDocument.SaveAsync(stream);
//Close the document.
loadedDocument.Close(true);
//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document
FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);
//To-Do some manipulation
//To-Do some manipulation
//Save the document into stream
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);
//If the position is not set to '0' then the PDF will be empty.
stream.Position = 0;
//Close the document.
loadedDocument.Close(true);
//Defining the ContentType for pdf file.
string contentType = "application/pdf";
//Define the file name.
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name.
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream
Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);
//To-Do some manipulation
//To-Do some manipulation
//Save the document into stream.
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);
//Close the document.
loadedDocument.Close(true);
//Save the stream into pdf file
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

{% endhighlight %}
{% endtabs %}

## Saving a PDF document to stream

You can also save the manipulated PDF document to stream using overloads of [Save](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html#Syncfusion_Pdf_Parsing_PdfLoadedDocument_Save) method.

{% tabs %}
{% highlight c# %}

//Load an existing PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");
//To-Do some manipulation
//To-Do some manipulation
//Creates an instance of memory stream
MemoryStream stream = new MemoryStream();
//Save the document stream
loadedDocument.Save(stream) ;

{% endhighlight %}

{% highlight vb.net %}

' Load an existing PDF document
Dim loadedDocument As New PdfLoadedDocument("Input.pdf")
'To-Do some manipulation
'To-Do some manipulation
'Creates an instance of memory stream
Dim stream As New MemoryStream()
'Save the document to stream
loadedDocument.Save(stream)

{% endhighlight %}

{% highlight UWP %}

//Load the PDF document as stream
Stream pdfStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Input.pdf");
//Creates an empty PDF loaded document instance
PdfLoadedDocument loadedDocument = new PdfLoadedDocument();
//Loads or opens an existing PDF document through Open method of PdfLoadedDocument class
await loadedDocument.OpenAsync(pdfStream);
//To-Do some manipulation
//To-Do some manipulation
//Save the document into stream.
MemoryStream stream = new MemoryStream();
await loadedDocument.SaveAsync(stream);

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document
FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);
//To-Do some manipulation
//To-Do some manipulation
//Save the document into stream
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream
Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);
//To-Do some manipulation
//To-Do some manipulation
//Save the document into stream.
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);

{% endhighlight %}
{% endtabs %}

## Saving a PDF document into the same file or stream

You can also resave the manipulated PDF document to the same file using overloads of [Save](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html#Syncfusion_Pdf_Parsing_PdfLoadedDocument_Save) method.

{% tabs %}
{% highlight c# %}

//Load an existing PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");
//To-Do some manipulation
//To-Do some manipulation
//Resave the document to the same file 
loadedDocument.Save() ;


{% endhighlight %}

{% highlight vb.net %}

' Load an existing PDF document
Dim loadedDocument As New PdfLoadedDocument("Input.pdf")
'To-Do some manipulation
'To-Do some manipulation
'Resave the document to the same file 
loadedDocument.Save()

{% endhighlight %}

{% highlight UWP %}

//Create the file open picker
var picker = new FileOpenPicker();
picker.FileTypeFilter.Add(".pdf");
//Browse and chose the file
StorageFile file = await picker.PickSingleFileAsync();
//Creates an empty PDF loaded document instance
PdfLoadedDocument loadedDocument = new PdfLoadedDocument();
//Loads or opens an existing PDF document through Open method of PdfLoadedDocument class
await loadedDocument.OpenAsync(file);
//To-Do some manipulation
//To-Do some manipulation  
//Resave the document to the same file
await loadedDocument.Save();

{% endhighlight %}

{% highlight ASP.NET Core %}

//PDF supports saving a PDF document into the same file only in Windows Forms, WPF, ASP.NET, ASP.NET MVC and UWP platforms.

{% endhighlight %}

{% highlight Xamarin %}

//PDF supports saving a PDF document into the same file only in Windows Forms, WPF, ASP.NET, ASP.NET MVC and UWP platforms.

{% endhighlight %}
{% endtabs %}

{% tabs %}
{% highlight c# %}

//Load an existing PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(stream);
//To-Do some manipulation
//To-Do some manipulation
//Resave the document to the same stream
loadedDocument.Save();

{% endhighlight %}

{% highlight vb.net %}

' Load an existing PDF document
Dim loadedDocument As New PdfLoadedDocument(stream)
'To-Do some manipulation
'To-Do some manipulation
'Resave the document to the same stream
loadedDocument.Save()

{% endhighlight %}
{% highlight UWP %}

//Create the file open picker
var picker = new FileOpenPicker();
picker.FileTypeFilter.Add(".pdf");
//Browse and chose the file
StorageFile file = await picker.PickSingleFileAsync();
//Creates an empty PDF loaded document instance
PdfLoadedDocument loadedDocument = new PdfLoadedDocument();
//Loads or opens an existing PDF document through Open method of PdfLoadedDocument class
await loadedDocument.OpenAsync(file);
//To-Do some manipulation
//To-Do some manipulation  
//Resave the document to the same file
await loadedDocument.Save();

{% endhighlight %}

{% highlight ASP.NET Core %}

//PDF supports saving a PDF document into the same file only in Windows Forms, WPF, ASP.NET, ASP.NET MVC and UWP platforms.

{% endhighlight %}

{% highlight Xamarin %}

//PDF supports saving a PDF document into the same file only in Windows Forms, WPF, ASP.NET, ASP.NET MVC and UWP platforms.

{% endhighlight %}
{% endtabs %}
## Closing a document

After the document manipulation and save operation are completed, you should close the instance of [PdfLoadedDocument](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html), in order to release all the memory consumed by PDF DOM. The following code snippet illustrates how to close a ```PdfLoadedDocument``` instance.

{% tabs %}
{% highlight c# %}

//Load an existing PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");
//To-Do some manipulation
//To-Do some manipulation
//Save the document in file system
loadedDocument.Save("Output.pdf"); 
//Close the document
loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net %}

' Load an existing PDF document
Dim loadedDocument As New PdfLoadedDocument("Input.pdf")
'To-Do some manipulation
'To-Do some manipulation
'Save the document in file system
loadedDocument.Save("Output.pdf")
'Close the document
loadedDocument.Close(True)

{% endhighlight %}

{% highlight UWP %}

//Load the PDF document as stream
Stream pdfStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Input.pdf");
//Creates an empty PDF loaded document instance
PdfLoadedDocument loadedDocument = new PdfLoadedDocument();
//Loads or opens an existing PDF document through Open method of PdfLoadedDocument class
await loadedDocument.OpenAsync(pdfStream);
//To-Do some manipulation
//To-Do some manipulation
//Save the document into stream.
MemoryStream stream = new MemoryStream();
await loadedDocument.SaveAsync(stream);
//Close the document.
 loadedDocument.Close(true);

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document
FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);
//To-Do some manipulation
//To-Do some manipulation
//Save the document into stream
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);
//Close the document.
loadedDocument.Close(true);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream
Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);
//To-Do some manipulation
//To-Do some manipulation
//Save the document into stream.
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);
//Close the document.
loadedDocument.Close(true);

{% endhighlight %}

{% endtabs %}

N> Close() method will dispose all the memory consumed by PDF DOM.
N> Close(true) method will dispose all the memory consumed by PDF DOM as well as disposes its document stream

## Secured documents exception

You can catch the secured document exception by opening an existing encrypted PDF document from either the file system, stream, or byte array using the following code sample as follows,

{% tabs %}
{% highlight c# %}

PdfLoadedDocument document = null;
try
{
//Load an existing document.
document = new PdfLoadedDocument("input.pdf", "password");
}
catch (Syncfusion.Pdf.PdfInvalidPasswordException exception)
{
//Secured PDF document password is invalid or opened without a password.
}
//Save a document.
document.Save("Output.pdf");
//Close a document.
document.Close(true);


{% endhighlight %}

{% highlight vb.net %}

Dim document As PdfLoadedDocument = Nothing
Try
'Load an existing document.
document = New PdfLoadedDocument("input.pdf", "password")
Catch exception As Syncfusion.Pdf.PdfInvalidPasswordException
'Secured PDF document password is invalid or opened without a password.
End Try
'Save a document.
document.Save("Output.pdf")
'Close a document.
document.Close(True)

{% endhighlight %}

{% highlight UWP %}

PdfLoadedDocument document = null;
try
{
//Open an existing encrypted document from the byte array.
document = new PdfLoadedDocument(byteArray, "password");
}
catch (Syncfusion.Pdf.PdfInvalidPasswordException exception)
{
//Secured PDF document password is invalid or opened without a password.
}
//Save a document into a stream.
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream);
//Close a document.
document.Close(true);

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load a PDF document.
FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument document = null;
try
{
//Open an existing PDF document from a stream.
document = new PdfLoadedDocument(docStream, "password");
}
catch (Syncfusion.Pdf.PdfInvalidPasswordException exception)
{
//Secured PDF document password is invalid or opened without a password.
}
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Close the document.
document.Close(true);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream.
Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");
PdfLoadedDocument document = null;
try
{
//Open an existing PDF document from a stream.
document = new PdfLoadedDocument(docStream, "password");
}
catch (Syncfusion.Pdf.PdfInvalidPasswordException exception)
{
//Secured PDF document password is invalid or opened without a password.
}
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Close a document.
document.Close(true);

{% endhighlight %}

{% endtabs %}
## Possible error messages of invalid PDF documents while loading
The following are the possible error messages of invalid PDF documents while loading:
I.	Please find some of the following corrupted error messages that cannot be repaired:
1.    Could not find a valid signature (%PDF-).
2.    Bad Format error.
3.    Lexical Error: Unmatched Input.
4.    The document does not contain EOF.
5.    The document has corrupted cross reference tables.
6.    Error: Bad input stream initializer.
7.    Fatal Error occurred.
II.	Please find  some of the possible offset error messages that may be repairable:
     1.Invalid cross-reference table with offset position.
     2.Trailer Prev offset is located in the same cross table section.

{% tabs %}
{% highlight c# %}

PdfLoadedDocument document = null;
try
{
//Open an existing PDF document from the disk.
document = new PdfLoadedDocument(“input.pdf”,true);
}
catch (Exception message)
{
//Invalid cross-reference table with offset position
//Trailer Prev offset is located in the same cross table section
//Could not find a valid signature (%PDF-).
//Bad Format error
//Lexical error: Unmatched input
//The document does not contain EOF
//The document has corrupted cross reference tables
//Error: Bad input stream initializer
//Fatal error occured
}
{% endhighlight %}

{% highlight vb.net %}

Dim document As PdfLoadedDocument = Nothing
Try
'Load an existing document.
document = New PdfLoadedDocument("input.pdf”,true)
Catch exception As Exception
‘Invalid cross-reference table with offset position
‘Trailer Prev offset is located in the same cross table section
‘Could not find a valid signature (%PDF-).
‘Bad Format error
‘Lexical error: Unmatched input
‘The document does not contain EOF
‘The document has corrupted cross reference tables
‘Error: Bad input stream initializer
‘Fatal error occured
End Try
'Save the document.
document.Save("Output.pdf")
'Close the document.
document.Close(True)


{% endhighlight %}

{% highlight ASP.NET Core %}

//Load a PDF document.
FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument document = null;
try
{
//Open an existing PDF document from the stream.
document = new PdfLoadedDocument(docStream,true);
}
catch (PdfException exception)
{
//Invalid cross-reference table with offset position
//Trailer Prev offset is located in the same cross table section
//Could not find a valid signature (%PDF-).
//Bad Format error
//Lexical error: Unmatched input
//The document does not contain EOF
//The document has corrupted cross reference table
//Error: Bad input stream initializer
//Fatal error occured
//Unexpected token name before 257
}
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Close the document.
document.Close(true);

{% endhighlight %}


{% endtabs %}
