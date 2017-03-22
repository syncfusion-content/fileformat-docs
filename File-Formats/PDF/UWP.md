---
title: Working with UWP
description: Create a UWP application and load the document
platform: file-formats
control: PDF
documentation: UG
---

# Working with UWP

In your UWP application, please add the required assemblies in order to use PDF. [Refer here for assemblies required](/File-Formats/pdf/Assemblies-Required).

## Loading the document

You can load and save the PDF document asynchronously using PDF.

The following code example illustrates how to load the PDF document by using stream in UWP.

{% tabs %}

{% highlight c# %}

//Load the PDF document as stream
Stream pdfStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Sample.pdf");
            
//Creates an empty PDF loaded document instance
PdfLoadedDocument document = new PdfLoadedDocument();

//Loads or opens an existing PDF document through Open method of PdfLoadedDocument class
await document.OpenAsync(pdfStream);

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the documents

document.Close(true);

//Save the stream as PDF document file in local machine

Save(stream, "Result.pdf");

async void Save(Stream stream, string filename)
{

stream.Position = 0;

StorageFile stFile;
if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
{
FileSavePicker savePicker = new FileSavePicker();
savePicker.DefaultFileExtension = ".pdf";
savePicker.SuggestedFileName = "Sample";
savePicker.FileTypeChoices.Add("Adobe PDF Document", new List<string>() { ".pdf" });
stFile = await savePicker.PickSaveFileAsync();
}
else
{
StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
}
if (stFile != null)
{
Windows.Storage.Streams.IRandomAccessStream fileStream = await stFile.OpenAsync(FileAccessMode.ReadWrite);
Stream st = fileStream.AsStreamForWrite();
st.Write((stream as MemoryStream).ToArray(), 0, (int)stream.Length);
st.Flush();
st.Dispose();
fileStream.Dispose();
}

{% endhighlight %}

{% highlight vb.net %}

'Load the PDF document as stream

Dim docStream As Stream = GetType(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Sample.pdf")

'Creates an empty PdfLoaded document instance

Dim document As New PdfLoadedDocument()

'Loads or opens an existing PDF document through Open method of PdfLoadedDocument class

Await document.OpenAsync(docStream)

Dim stream As New MemoryStream()

'Save the PDF document into memory stream

Await document.SaveAsync(stream)

'Close the PDF documents

document.Close(True)

'Save the stream as PDF document file in local machine

Save(stream, "Result.pdf")

Private Async Sub Save(stream As MemoryStream, filename As String)

stream.Position = 0

Dim stFile As StorageFile

If Not (Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")) Then

Dim savePicker As New FileSavePicker()

savePicker.DefaultFileExtension = ".pdf"

savePicker.SuggestedFileName = filename

savePicker.FileTypeChoices.Add("PDF Documents", New List(Of String)(New String() {".pdf"}))

stFile = Await savePicker.PickSaveFileAsync()

Else

Dim local As StorageFolder = Windows.Storage.ApplicationData.Current.LocalFolder

stFile = Await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting)

End If

If stFile IsNot Nothing Then

Dim pdfStream As IRandomAccessStream = Await stFile.OpenAsync(FileAccessMode.ReadWrite)
Dim st As Stream = pdfStream.AsStreamForWrite()
Dim buffer As Byte() = stream.ToArray()
st.Write(buffer, 0, buffer.Length)
st.Flush()
st.Dispose()
pdfStream.Dispose()

End If

End Sub

{% endhighlight %}

{% endtabs %}

The following code example illustrates how to load the PDF document by using file open picker in UWP.

{% tabs %}

{% highlight c# %}

//Create the file open picker

var picker = new FileOpenPicker();

picker.FileTypeFilter.Add(".pdf");

//Browse and chose the file

StorageFile file = await picker.PickSingleFileAsync();

//Creates an empty PDF loaded document instance
PdfLoadedDocument document = new PdfLoadedDocument();

//Loads or opens an existing PDF document through Open method of PdfLoadedDocument class
await document.OpenAsync(file);

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the documents

document.Close(true);

//Save the stream as PDF document file in local machine

Save(stream, "Result.pdf");

async void Save(Stream stream, string filename)
{

stream.Position = 0;

StorageFile stFile;
if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
{
FileSavePicker savePicker = new FileSavePicker();
savePicker.DefaultFileExtension = ".pdf";
savePicker.SuggestedFileName = "Sample";
savePicker.FileTypeChoices.Add("Adobe PDF Document", new List<string>() { ".pdf" });
stFile = await savePicker.PickSaveFileAsync();
}
else
{
StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
}
if (stFile != null)
{
Windows.Storage.Streams.IRandomAccessStream fileStream = await stFile.OpenAsync(FileAccessMode.ReadWrite);
Stream st = fileStream.AsStreamForWrite();
st.Write((stream as MemoryStream).ToArray(), 0, (int)stream.Length);
st.Flush();
st.Dispose();
fileStream.Dispose();
}

{% endhighlight %}

{% highlight vb.net %}

'Create the file open picker

Dim picker = New FileOpenPicker()

picker.FileTypeFilter.Add(".pdf")

'Browse and chose the file

Dim file As StorageFile = Await picker.PickSingleFileAsync()

'Creates an empty PdfLoaded document instance

Dim document As New PdfLoadedDocument()

'Loads or opens an existing PDF document through Open method of PdfLoadedDocument class

Await document.OpenAsync(file)

Dim stream As New MemoryStream()

'Save the PDF document into memory stream

Await document.SaveAsync(stream)

'Close the PDF documents

document.Close(True)

'Save the stream as PDF document file in local machine

Save(stream, "Result.pdf")

Private Async Sub Save(stream As MemoryStream, filename As String)

stream.Position = 0

Dim stFile As StorageFile

If Not (Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")) Then

Dim savePicker As New FileSavePicker()

savePicker.DefaultFileExtension = ".pdf"

savePicker.SuggestedFileName = filename

savePicker.FileTypeChoices.Add("PDF Documents", New List(Of String)(New String() {".pdf"}))

stFile = Await savePicker.PickSaveFileAsync()

Else

Dim local As StorageFolder = Windows.Storage.ApplicationData.Current.LocalFolder

stFile = Await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting)

End If

If stFile IsNot Nothing Then

Dim pdfStream As IRandomAccessStream = Await stFile.OpenAsync(FileAccessMode.ReadWrite)
Dim st As Stream = pdfStream.AsStreamForWrite()
Dim buffer As Byte() = stream.ToArray()
st.Write(buffer, 0, buffer.Length)
st.Flush()
st.Dispose()
pdfStream.Dispose()

End If

End Sub

{% endhighlight %}

{% endtabs %}

## Save the document 

The following code example illustrates how to save the PDF document in UWP by using file save picker.

{% tabs %}

{% highlight c# %}

//Creates an empty PDF document instance
PdfDocument document = new PdfDocument();

//Adding new page to the PDF document
PdfPage page = document.Pages.Add();

//Creates new PDF font
PdfStandardFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 12);

//Drawing text to the PDF document
page.Graphics.DrawString("Hello world", font, PdfBrushes.Black, 10, 10);

MemoryStream stream = new MemoryStream();

//Saves the PDF document to stream
await document.SaveAsync(stream);

//Close the document

document.Close(true);

//Save the stream as PDF document file in local machine

Save(stream, "Result.pdf");

async void Save(Stream stream, string filename)
{

stream.Position = 0;

StorageFile stFile;
if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
{
FileSavePicker savePicker = new FileSavePicker();
savePicker.DefaultFileExtension = ".pdf";
savePicker.SuggestedFileName = "Sample";
savePicker.FileTypeChoices.Add("Adobe PDF Document", new List<string>() { ".pdf" });
stFile = await savePicker.PickSaveFileAsync();
}
else
{
StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
}
if (stFile != null)
{
Windows.Storage.Streams.IRandomAccessStream fileStream = await stFile.OpenAsync(FileAccessMode.ReadWrite);
Stream st = fileStream.AsStreamForWrite();
st.Write((stream as MemoryStream).ToArray(), 0, (int)stream.Length);
st.Flush();
st.Dispose();
fileStream.Dispose();
}

{% endhighlight %}

{% highlight vb.net %}

'Creates an empty PDF document instance
Dim document As New PdfDocument()

'Adding new page to the PDF document
Dim page As PdfPage = document.Pages.Add()

'Creates new PDF font
Dim font As New PdfStandardFont(PdfFontFamily.TimesRoman, 12)

'Drawing text to the PDF document
page.Graphics.DrawString("Hello world", font, PdfBrushes.Black, 10, 10)

Dim stream As New MemoryStream()

'Saves the PDF document to stream
Await document.SaveAsync(stream)

'Close the document

document.Close(True)

'Save the stream as PDF document file in local machine

Save(stream, "Result.pdf")

Private Async Sub Save(stream As MemoryStream, filename As String)

stream.Position = 0

Dim stFile As StorageFile

If Not (Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")) Then

Dim savePicker As New FileSavePicker()

savePicker.DefaultFileExtension = ".pdf"

savePicker.SuggestedFileName = filename

savePicker.FileTypeChoices.Add("PDF Documents", New List(Of String)(New String() {".pdf"}))

stFile = Await savePicker.PickSaveFileAsync()

Else

Dim local As StorageFolder = Windows.Storage.ApplicationData.Current.LocalFolder

stFile = Await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting)

End If

If stFile IsNot Nothing Then

Dim pdfStream As IRandomAccessStream = Await stFile.OpenAsync(FileAccessMode.ReadWrite)
Dim st As Stream = pdfStream.AsStreamForWrite()
Dim buffer As Byte() = stream.ToArray()
st.Write(buffer, 0, buffer.Length)
st.Flush()
st.Dispose()
pdfStream.Dispose()

End If

End Sub

{% endhighlight %}

{% endtabs %}