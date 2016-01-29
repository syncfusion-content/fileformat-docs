---
title: Working with UWP
description: Create a UWP application and load the document
platform: file-formats
control: DocIO
documentation: UG
---

# Working with UWP

In your UWP application, please add the required assemblies in order to use DocIO. [Refer here for assemblies required](/File-Formats/DocIO/Assemblies-Required).

## Loading the document

You can load and save the Word document asynchronously using DocIO.

The following code example illustrates how to load the Word document by using stream in UWP.

{% tabs %}

{% highlight c# %}

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

{% highlight vb.net %}

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

The following code example illustrates how to load the Word document by using file open picker in WinRT.

{% tabs %}

{% highlight c# %}

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

{% highlight vb.net %}

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

The following code example illustrates how to save the Word document in WinRT by using file save picker.

{% tabs %}

{% highlight c# %}

//Creates an empty Word document instance

WordDocument document = new WordDocument();

//Adds new section to the document

IWSection section = document.AddSection();

//Adds new paragraph to the section

IWParagraph paragraph = section.AddParagraph();

//Appends the text to the created paragraph

paragraph.AppendText("Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula");

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

{% highlight vb.net %}

'Creates an empty Word document instance

Dim document As New WordDocument()

'Adds new section to the document

Dim section As IWSection = document.AddSection()

'Adds new paragraph to the section

Dim paragraph As IWParagraph = section.AddParagraph()

'Appends the text to the created paragraph

paragraph.AppendText("Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula")

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