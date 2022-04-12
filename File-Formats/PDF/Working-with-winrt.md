---
title: Working with WinRT
description: This section explains how to load and save PDF document in WinRT
platform: file-formats
control: PDF
documentation: UG
---

# Working with WinRT

In your WinRT application, please add the required assemblies in order to use Essential PDF. [Refer here for assemblies required](/File-Formats/PDF/Assemblies-Required).

## Loading the document 

The following code example illustrates how to load the file by using stream in WinRT.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Load the file as stream

Stream docStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Winrt_Sample.Assets.Data.Sample.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument();

await loadedDocument.OpenAsync(docStream);

//Create booklet with two sides

PdfDocument document = PdfBookletCreator.CreateBooklet(loadedDocument, new SizeF(1000, 700), true);

MemoryStream stream = new MemoryStream();

//Save the document into memory stream

await document.SaveAsync(stream);

//close the documents

document.Close(true);

loadedDocument.Close(true);

//Save the stream into pdf file

Save(stream, "Booklet.pdf");

async void Save(Stream stream, string filename)

{

stream.Position = 0;

FileSavePicker savePicker = new FileSavePicker();

savePicker.DefaultFileExtension = ".pdf";

savePicker.SuggestedFileName = filename;

savePicker.FileTypeChoices.Add("Adobe PDF Document", new List<string>() { ".pdf" });

StorageFile stFile = await savePicker.PickSaveFileAsync();

if (stFile != null)

{

Windows.Storage.Streams.IRandomAccessStream fileStream = await stFile.OpenAsync(FileAccessMode.ReadWrite);

Stream stream1 = fileStream.AsStreamForWrite();

stream1.SetLength(0);

stream1.Write((stream as MemoryStream).ToArray(), 0, (int)stream.Length);

stream1.Flush();

stream1.Dispose();

fileStream.Dispose();

}

}

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Load the file as stream

Dim docStream As Stream = GetType(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("WinrtSample.Assets.Sample.pdf")

Dim loadedDocument As New PdfLoadedDocument()

await loadedDocument.OpenAsync(docStream)

'Create booklet with two sides

Dim document As PdfDocument = PdfBookletCreator.CreateBooklet(loadedDocument, New SizeF(1000, 700), True)

Dim stream As New MemoryStream()

'Save the document into memory stream

await document.SaveAsync(stream)

'close the documents

document.Close(True)

loadedDocument.Close(True)

'Save the stream into pdf file

Save(stream, "Booklet.pdf")

Private async Sub Save(ByVal stream As Stream, ByVal filename As String)

stream.Position = 0

Dim savePicker As New FileSavePicker()

savePicker.DefaultFileExtension = ".pdf"

savePicker.SuggestedFileName = filename

savePicker.FileTypeChoices.Add("Adobe PDF Document", New List(Of String) (New String() {".pdf"}))

Dim stFile As StorageFile = await savePicker.PickSaveFileAsync()

If stFile IsNot Nothing Then

Dim fileStream As Windows.Storage.Streams.IRandomAccessStream = await stFile.OpenAsync(FileAccessMode.ReadWrite)

Dim stream1 As Stream = fileStream.AsStreamForWrite()

stream1.SetLength(0)

stream1.Write((TryCast(stream, MemoryStream)).ToArray(), 0, CInt(stream.Length))

stream1.Flush()

stream1.Dispose()

fileStream.Dispose()

End If

End Sub

{% endhighlight %}

{% endtabs %}

The following code example illustrates how to load the file by using file picker in WinRT.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//create the file open picker

var picker = new FileOpenPicker();

picker.FileTypeFilter.Add(".pdf");

//Browse the multiple files

IReadOnlyList<StorageFile> files = await picker.PickMultipleFilesAsync();

//Load the file stream

PdfLoadedDocument loadedDocument = new PdfLoadedDocument();

await loadedDocument.OpenAsync(files[0]);

//Create booklet with two sides

PdfDocument document = PdfBookletCreator.CreateBooklet(loadedDocument, new SizeF(1000, 700), true);

MemoryStream stream = new MemoryStream();

//Save the document into memory stream

await document.SaveAsync(stream);

//close the documents

document.Close(true);

loadedDocument.Close(true);

//Save the stream into pdf file

Save(stream, "Booklet.pdf");

async void Save(Stream stream, string filename)

{

stream.Position = 0;

FileSavePicker savePicker = new FileSavePicker();

savePicker.DefaultFileExtension = ".pdf";

savePicker.SuggestedFileName = filename;

savePicker.FileTypeChoices.Add("Adobe PDF Document", new List<string>() { ".pdf" });

StorageFile stFile = await savePicker.PickSaveFileAsync();

if (stFile != null)

{

Windows.Storage.Streams.IRandomAccessStream fileStream = await stFile.OpenAsync(FileAccessMode.ReadWrite);

Stream stream1 = fileStream.AsStreamForWrite();

stream1.SetLength(0);

stream1.Write((stream as MemoryStream).ToArray(), 0, (int)stream.Length);

stream1.Flush();

stream1.Dispose();

fileStream.Dispose();

}

}

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'create the file open picker

Dim picker = New FileOpenPicker()

picker.FileTypeFilter.Add(".pdf")

'Browse the multiple files

Dim files As IReadOnlyList(Of StorageFile) = await picker.PickMultipleFilesAsync()

'Load the file stream

Dim loadedDocument As New PdfLoadedDocument()

await loadedDocument.OpenAsync(files(0))

'Create booklet with two sides

Dim document As PdfDocument = PdfBookletCreator.CreateBooklet(loadedDocument, New SizeF(1000, 700), True)

Dim stream As New MemoryStream()

'Save the document into memory stream

await document.SaveAsync(stream)

'close the documents

document.Close(True)

loadedDocument.Close(True)

'Save the stream into pdf file

Save(stream, "Booklet.pdf")

Private async Sub Save(ByVal stream As Stream, ByVal filename As String)

stream.Position = 0

Dim savePicker As New FileSavePicker()

savePicker.DefaultFileExtension = ".pdf"

savePicker.SuggestedFileName = filename

savePicker.FileTypeChoices.Add("Adobe PDF Document", New List(Of String) (New String() {".pdf"}))

Dim stFile As StorageFile = await savePicker.PickSaveFileAsync()

If stFile IsNot Nothing Then

Dim fileStream As Windows.Storage.Streams.IRandomAccessStream = await stFile.OpenAsync(FileAccessMode.ReadWrite)

Dim stream1 As Stream = fileStream.AsStreamForWrite()

stream1.SetLength(0)

stream1.Write((TryCast(stream, MemoryStream)).ToArray(), 0, CInt(stream.Length))

stream1.Flush()

stream1.Dispose()

fileStream.Dispose()

End If

End Sub

{% endhighlight %}

{% endtabs %}

## Saving the document 

The following code example illustrates how to save the PDF document in WinRT by using file picker.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Create a new document

PdfDocument document = new PdfDocument();

//Add a page

PdfPage page = document.Pages.Add();

//Create Pdf graphics for the page

PdfGraphics graphics = page.Graphics;

//Create a solid brush

PdfBrush brush = new PdfSolidBrush(System.Drawing.Color.FromArgb(255, 0, 0, 0));

//Set the font

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 36);

//Draw the text

graphics.DrawString("Hello world!", font, brush, new PointF(20, 20));

//create the stream

MemoryStream memoryStream = new MemoryStream();

//save the document into stream

await document.SaveAsync(memoryStream);

//close the document

document.Close(true);

//save the stream into file

Save(memoryStream, "sample.pdf");

async void Save(Stream stream, string filename)

{

stream.Position = 0;

FileSavePicker savePicker = new FileSavePicker();

savePicker.DefaultFileExtension = ".pdf";

savePicker.SuggestedFileName = "Sample";

savePicker.FileTypeChoices.Add("Adobe PDF Document", new List<string>() { ".pdf" });

StorageFile stFile = await savePicker.PickSaveFileAsync();

if (stFile != null)

{

Windows.Storage.Streams.IRandomAccessStream fileStream = await stFile.OpenAsync(FileAccessMode.ReadWrite);

Stream stream1 = fileStream.AsStreamForWrite();

stream1.SetLength(0);

stream1.Write((stream as MemoryStream).ToArray(), 0, (int)stream.Length);

stream1.Flush();

stream1.Dispose();

fileStream.Dispose();

}

}

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new document

Dim document As New PdfDocument()

'Add a page

Dim page As PdfPage = document.Pages.Add()

'Create Pdf graphics for the page

Dim graphics As PdfGraphics = page.Graphics

'Create a solid brush

Dim brush As PdfBrush = New PdfSolidBrush(System.Drawing.Color.FromArgb(255, 0, 0, 0))

'Set the font

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 36)

'Draw the text

graphics.DrawString("Hello world!", font, brush, New PointF(20, 20))

'create the stream

Dim memoryStream As New MemoryStream()

'save the document into stream

Await document.SaveAsync(memoryStream)

'close the document

document.Close(True)

'save the stream into file

Save(memoryStream, "sample.pdf")

Private async Sub Save(ByVal stream As Stream, ByVal filename As String)

stream.Position = 0

Dim savePicker As New FileSavePicker()

savePicker.DefaultFileExtension = ".pdf"

savePicker.SuggestedFileName = "Sample"

savePicker.FileTypeChoices.Add("Adobe PDF Document", New List(Of String) (New String() {".pdf"}))

Dim stFile As StorageFile = await savePicker.PickSaveFileAsync()

If stFile IsNot Nothing Then

Dim fileStream As Windows.Storage.Streams.IRandomAccessStream = await stFile.OpenAsync(FileAccessMode.ReadWrite)

Dim stream1 As Stream = fileStream.AsStreamForWrite()

stream1.SetLength(0)

stream1.Write((TryCast(stream, MemoryStream)).ToArray(), 0, CInt(stream.Length))

stream1.Flush()

stream1.Dispose()

fileStream.Dispose()

End If

End Sub

{% endhighlight %}

{% endtabs %}