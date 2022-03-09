---
title: Working with Word document with Windows phone
description: Create a Windows phone application, load the word document and save the word document with Syncfusion Word library
platform: file-formats
control: DocIO
documentation: UG
---

# Working with Windows Phone 

In your Windows Phone application, please add the required assemblies in order to use DocIO. [Refer here for assemblies required](/File-Formats/DocIO/Assemblies-Required).

## Loading the document 

You can load and save the Word document asynchronously using DocIO.

The following code example illustrates how to load the Word document by using stream in Windows Phone.

{% tabs %}

{% highlight c# tabtile="C#" %}

//Load the Word document as stream

Stream docStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Sample.docx");

//Creates an empty Word document instance

WordDocument document = new WordDocument();

//Loads or opens an existing word document through Open method of WordDocument class

await document.OpenAsync(docStream, FormatType.Docx);

StorageFolder localFolder = Windows.Storage.ApplicationData.Current.LocalFolder;

StorageFile outFile = await localFolder.CreateFileAsync("Result.docx", CreationCollisionOption.ReplaceExisting);

using (Stream outStream = await outFile.OpenStreamForWriteAsync())
{

//Save the document into stream

await document.SaveAsync(outStream, FormatType.Docx);

//Close the document

document.Close();

}

{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}

'Load the Word document as stream

Dim docStream As Stream = GetType(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Sample.docx")

'Creates an empty Word document instance

Dim document As New WordDocument()

'Loads or opens an existing word document through Open method of WordDocument class

Await document.OpenAsync(docStream, FormatType.Docx)

Dim localFolder As StorageFolder = Windows.Storage.ApplicationData.Current.LocalFolder

Dim outFile As StorageFile = Await localFolder.CreateFileAsync("Result.docx", CreationCollisionOption.ReplaceExisting)

Using outStream As Stream = Await outFile.OpenStreamForWriteAsync()

'Save the document into stream

Await document.SaveAsync(outStream, FormatType.Docx)

'Close the document

document.Close()
	
End Using

{% endhighlight %}

{% endtabs %}

The following code example illustrates how to load the Word document by using file open picker in Windows Phone.

{% tabs %}

{% highlight c# tabtile="C#" %}

//Create the file open picker

var picker = new FileOpenPicker();

picker.FileTypeFilter.Add(".docx");

picker.FileTypeFilter.Add(".doc");

//Browse and chose the file

StorageFile files = await picker.PickSingleFileAsync();

//Creates an empty Word document instance

WordDocument document = new WordDocument();

//Loads or opens an existing word document through Open method of WordDocument class

await document.OpenAsync(files);

StorageFolder localFolder = Windows.Storage.ApplicationData.Current.LocalFolder;

StorageFile outFile = await localFolder.CreateFileAsync("Result.docx", CreationCollisionOption.ReplaceExisting);

using (Stream outStream = await outFile.OpenStreamForWriteAsync())
{

//Save the document into stream

await document.SaveAsync(outStream, FormatType.Docx);

//Close the document

document.Close();

}

{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}

'Create the file open picker

Dim picker = New FileOpenPicker()

picker.FileTypeFilter.Add(".docx")

picker.FileTypeFilter.Add(".doc")

'Browse and chose the file

Dim files As StorageFile = Await picker.PickSingleFileAsync()

'Creates an empty Word document instance

Dim document As New WordDocument()

'Loads or opens an existing word document through Open method of WordDocument class

Await document.OpenAsync(files)

Dim localFolder As StorageFolder = Windows.Storage.ApplicationData.Current.LocalFolder

Dim outFile As StorageFile = Await localFolder.CreateFileAsync("Result.docx", CreationCollisionOption.ReplaceExisting)

Using outStream As Stream = Await outFile.OpenStreamForWriteAsync()

'Save the document into stream

Await document.SaveAsync(outStream, FormatType.Docx)

'Close the document

document.Close()
	
End Using

{% endhighlight %}

{% endtabs %}

## Save the document 

The following code example illustrates how to save the Word document in Windows Phone using file save picker.

{% tabs %}

{% highlight c# tabtile="C#" %}

//Creates an empty Word document instance

WordDocument document = new WordDocument();

//Adds new section to the document

IWSection section = document.AddSection();

//Adds new paragraph to the section

IWParagraph paragraph = section.AddParagraph();

//Appends the text to the created paragraph

paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");

MemoryStream stream = new MemoryStream();

//Save the document into memory stream

await document.SaveAsync(stream, FormatType.Docx);

//Close the documents

document.Close();

//Save the stream as Word document file in local machine

Save(stream, "Result.docx");

async void Save(Stream stream, string filename)
{

stream.Position = 0;

FileSavePicker savePicker = new FileSavePicker();

savePicker.DefaultFileExtension = ".docx";

savePicker.SuggestedFileName = filename;

savePicker.FileTypeChoices.Add("Word Documents", new List<string>() { ".docx" });

StorageFile stFile = await savePicker.PickSaveFileAsync();

if (stFile != null)
{

Windows.Storage.Streams.IRandomAccessStream fileStream = await stFile.OpenAsync(FileAccessMode.ReadWrite);

Stream outStream = fileStream.AsStreamForWrite();

outStream.SetLength(0);

outStream.Write((stream as MemoryStream).ToArray(), 0, (int)stream.Length);

outStream.Flush();

outStream.Dispose();

fileStream.Dispose();

}

}

{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}

'Creates an empty Word document instance

Dim document As New WordDocument()

'Adds new section to the document

Dim section As IWSection = document.AddSection()

'Adds new paragraph to the section

Dim paragraph As IWParagraph = section.AddParagraph()

'Appends the text to the created paragraph

paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.")

Dim stream As New MemoryStream()

'Save the document into memory stream

Await document.SaveAsync(stream, FormatType.Docx)

'Close the documents

document.Close()

'Save the stream as Word document file in local machine

Save(stream, "Result.docx")

Private Sub Save(stream As Stream, filename As String)

stream.Position = 0

Dim savePicker As New FileSavePicker()

savePicker.DefaultFileExtension = ".docx"

savePicker.SuggestedFileName = filename

savePicker.FileTypeChoices.Add("Word Documents", New List(Of String) (New String() {".docx"}))

Dim stFile As StorageFile = Await savePicker.PickSaveFileAsync()

If stFile IsNot Nothing Then

Dim fileStream As Windows.Storage.Streams.IRandomAccessStream = Await stFile.OpenAsync(FileAccessMode.ReadWrite)

Dim outStream As Stream = fileStream.AsStreamForWrite()

outStream.SetLength(0)

outStream.Write(TryCast(stream, MemoryStream).ToArray(), 0, CInt(stream.Length))

outStream.Flush()

outStream.Dispose()

fileStream.Dispose()

End If

End Sub

{% endhighlight %}

{% endtabs %}