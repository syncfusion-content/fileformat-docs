---
title: Working with Word document with UWP
description: Create a UWP application, load the Word document and save the Word document with Syncfusion Word library
platform: file-formats
control: DocIO
documentation: UG
---

# Working with Word document in UWP

In your UWP application, please add the required assemblies in order to use DocIO. [Refer here for assemblies required](/File-Formats/DocIO/Assemblies-Required).

## Loading the document

You can load and save the Word document asynchronously using DocIO.

The following code example illustrates how to load the Word document by using stream in UWP.

{% tabs %}

{% highlight c# tabtile="C#" %}

//Load the Word document as stream

Stream docStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Sample.docx");

//Creates an empty Word document instance

WordDocument document = new WordDocument();

//Loads or opens an existing word document through Open method of WordDocument class

await document.OpenAsync(docStream, FormatType.Docx);

MemoryStream stream = new MemoryStream();

//Save the document into memory stream

await document.SaveAsync(stream, FormatType.Docx);

//Close the documents

document.Close();

//Save the stream as Word document file in local machine

Save(stream, "Result.docx");

async void Save(MemoryStream stream, string filename)
{

stream.Position = 0;

StorageFile stFile;

if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))

{

FileSavePicker savePicker = new FileSavePicker();

savePicker.DefaultFileExtension = ".docx";

savePicker.SuggestedFileName = filename;

savePicker.FileTypeChoices.Add("Word Documents", new List<string>() { ".docx" });

 stFile = await savePicker.PickSaveFileAsync();
 
 }
 
else

{

StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;

stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);

}
if (stFile != null)

{

using (IRandomAccessStream zipStream = await stFile.OpenAsync(FileAccessMode.ReadWrite))

{

// Write compressed data from memory to file

using (Stream outstream = zipStream.AsStreamForWrite())

{

byte[] buffer = stream.ToArray();

outstream.Write(buffer, 0, buffer.Length);

outstream.Flush();

}

}

}

}

{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}

'Load the Word document as stream

Dim docStream As Stream = GetType(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Sample.docx")

'Creates an empty Word document instance

Dim document As New WordDocument()

'Loads or opens an existing word document through Open method of WordDocument class

Await document.OpenAsync(docStream, FormatType.Docx)

Dim stream As New MemoryStream()

'Save the document into memory stream

Await document.SaveAsync(stream, FormatType.Docx)

'Close the documents

document.Close()

'Save the stream as Word document file in local machine

Save(stream, "Result.docx")

Private Sub Save(stream As MemoryStream, filename As String)

stream.Position = 0

Dim stFile As StorageFile

If Not (Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")) Then

Dim savePicker As New FileSavePicker()

savePicker.DefaultFileExtension = ".docx"

savePicker.SuggestedFileName = filename

savePicker.FileTypeChoices.Add("Word Documents", New List(Of String) (New String() {".docx"}))

stFile = Await savePicker.PickSaveFileAsync()

Else

Dim local As StorageFolder = Windows.Storage.ApplicationData.Current.LocalFolder

stFile = Await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting)

End If

If stFile IsNot Nothing Then

Using zipStream As IRandomAccessStream = Await stFile.OpenAsync(FileAccessMode.ReadWrite)

'Write compressed data from memory to file

Using outstream As Stream = zipStream.AsStreamForWrite()

Dim buffer As Byte() = stream.ToArray()

outstream.Write(buffer, 0, buffer.Length)

outstream.Flush()

End Using

End Using

End If

End Sub

{% endhighlight %}

{% endtabs %}

The following code example illustrates how to load the Word document by using file open picker in UWP.

{% tabs %}

{% highlight c# tabtile="C#" %}

//Create the file open picker

var picker = new FileOpenPicker();

picker.FileTypeFilter.Add(".docx");

picker.FileTypeFilter.Add(".doc");

//Browse and chose the file

StorageFile file = await picker.PickSingleFileAsync();

//Creates an empty Word document instance

WordDocument document = new WordDocument();

//Loads or opens an existing word document through Open method of WordDocument class

await document.OpenAsync(file);

MemoryStream stream = new MemoryStream();

//Save the document into memory stream

await document.SaveAsync(stream, FormatType.Docx);

//Close the documents

document.Close();

//Save the stream as Word document file in local machine

Save(stream, "Result.docx");

async void Save(MemoryStream stream, string filename)
{

stream.Position = 0;

StorageFile stFile;

if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))

{

FileSavePicker savePicker = new FileSavePicker();

savePicker.DefaultFileExtension = ".docx";

savePicker.SuggestedFileName = filename;

savePicker.FileTypeChoices.Add("Word Documents", new List<string>() { ".docx" });

stFile = await savePicker.PickSaveFileAsync();
 
}
 
else

{

StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;

stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);

}
if (stFile != null)

{

using (IRandomAccessStream zipStream = await stFile.OpenAsync(FileAccessMode.ReadWrite))

{

// Write compressed data from memory to file

using (Stream outstream = zipStream.AsStreamForWrite())

{

byte[] buffer = stream.ToArray();

outstream.Write(buffer, 0, buffer.Length);

outstream.Flush();

}

}

}

}

{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}

'Create the file open picker

Dim picker = New FileOpenPicker()

picker.FileTypeFilter.Add(".docx")

picker.FileTypeFilter.Add(".doc")

'Browse and chose the file

Dim file As StorageFile = Await picker.PickSingleFileAsync()

'Creates an empty Word document instance

Dim document As New WordDocument()

'Loads or opens an existing word document through Open method of WordDocument class

Await document.OpenAsync(file)

Dim stream As New MemoryStream()

'Save the document into memory stream

Await document.SaveAsync(stream, FormatType.Docx)

'Close the documents

document.Close()

'Save the stream as Word document file in local machine

Save(stream, "Result.docx")

Private Sub Save(stream As MemoryStream, filename As String)

stream.Position = 0

Dim stFile As StorageFile

If Not (Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")) Then

Dim savePicker As New FileSavePicker()

savePicker.DefaultFileExtension = ".docx"

savePicker.SuggestedFileName = filename

savePicker.FileTypeChoices.Add("Word Documents", New List(Of String) (New String() {".docx"}))

stFile = Await savePicker.PickSaveFileAsync()

Else

Dim local As StorageFolder = Windows.Storage.ApplicationData.Current.LocalFolder

stFile = Await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting)

End If

If stFile IsNot Nothing Then

Using zipStream As IRandomAccessStream = Await stFile.OpenAsync(FileAccessMode.ReadWrite)

'Write compressed data from memory to file

Using outstream As Stream = zipStream.AsStreamForWrite()

Dim buffer As Byte() = stream.ToArray()

outstream.Write(buffer, 0, buffer.Length)

outstream.Flush()

End Using

End Using

End If

End Sub

{% endhighlight %}

{% endtabs %}

## Save the document 

The following code example illustrates how to save the Word document in UWP by using file save picker.

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

//Save the stream into Word document file

Save(stream, "Result.docx");

async void Save(MemoryStream stream, string filename)
{

stream.Position = 0;

StorageFile stFile;

if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))

{

FileSavePicker savePicker = new FileSavePicker();

savePicker.DefaultFileExtension = ".docx";

savePicker.SuggestedFileName = filename;

savePicker.FileTypeChoices.Add("Word Documents", new List<string>() { ".docx" });

 stFile = await savePicker.PickSaveFileAsync();
 
 }
 
else

{

StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;

stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);

}
if (stFile != null)

{

using (IRandomAccessStream zipStream = await stFile.OpenAsync(FileAccessMode.ReadWrite))

{

// Write compressed data from memory to file

using (Stream outstream = zipStream.AsStreamForWrite())

{

byte[] buffer = stream.ToArray();

outstream.Write(buffer, 0, buffer.Length);

outstream.Flush();

}

}

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

'Save the stream into Word document file

Save(stream, "Result.docx")

Private Sub Save(stream As MemoryStream, filename As String)

stream.Position = 0

Dim stFile As StorageFile

If Not (Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")) Then

Dim savePicker As New FileSavePicker()

savePicker.DefaultFileExtension = ".docx"

savePicker.SuggestedFileName = filename

savePicker.FileTypeChoices.Add("Word Documents", New List(Of String) (New String() {".docx"}))

stFile = Await savePicker.PickSaveFileAsync()

Else

Dim local As StorageFolder = Windows.Storage.ApplicationData.Current.LocalFolder

stFile = Await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting)

End If

If stFile IsNot Nothing Then

Using zipStream As IRandomAccessStream = Await stFile.OpenAsync(FileAccessMode.ReadWrite)

'Write compressed data from memory to file

Using outstream As Stream = zipStream.AsStreamForWrite()

Dim buffer As Byte() = stream.ToArray()

outstream.Write(buffer, 0, buffer.Length)

outstream.Flush()

End Using

End Using

End If

End Sub

{% endhighlight %}

{% endtabs %}

N> The Image and PDF conversions are not supported in UWP Platform.