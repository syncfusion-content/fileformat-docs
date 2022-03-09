---
title: Working with Windows Phone
description: This section explains how to load and save PDF document in Windows Phone
platform: file-formats
control: PDF
documentation: UG
---

# Working with Windows Phone 

In your Windows Phone application, please add the required assemblies in order to use Essential PDF. [Refer here for assemblies required](/File-Formats/PDF/Assemblies-Required).

## Loading the document 

The following code example illustrates how to load the file by using stream in Windows Phone.

{% tabs %}

{% highlight c# tabtile="C#" %}

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

{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}

'Load the document as stream

Dim docStream As Stream = GetType(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("windowsPhoneSample.Data.Sample.pdf")

Dim loadedDocument As New PdfLoadedDocument()

await loadedDocument.OpenAsync(docStream)

'Create booklet with two sides

Dim document As PdfDocument = PdfBookletCreator.CreateBooklet(loadedDocument, New SizeF(1000, 800), False)

Dim localFolder As StorageFolder = Windows.Storage.ApplicationData.Current.LocalFolder

Dim outFile As StorageFile = await localFolder.CreateFileAsync("Booklet.pdf", CreationCollisionOption.ReplaceExisting)

Using outStream As Stream = await outFile.OpenStreamForWriteAsync()

'save the document

await document.SaveAsync(outStream)

'Close the documents

document.Close(True)

loadedDocument.Close(True)

End Using

{% endhighlight %}

{% endtabs %}

The following code example illustrates how to load the file by using file open picker in Windows Phone.

{% tabs %}

{% highlight c# tabtile="C#" %}

//create the file open picker

var picker = new FileOpenPicker();

picker.FileTypeFilter.Add(".pdf");

//Browse the multiple files

IReadOnlyList<StorageFile> files = await picker.PickMultipleFilesAsync();

//Load the existing document using file picker

PdfLoadedDocument loadedDocument = new PdfLoadedDocument();

await loadedDocument.OpenAsync(files[0]);

//Create booklet with two sides

PdfDocument document = PdfBookletCreator.CreateBooklet(loadedDocument, new SizeF(1000, 800), false);

StorageFolder localFolder = Windows.Storage.ApplicationData.Current.LocalFolder;

StorageFile outputFile = await localFolder.CreateFileAsync("Booklet.pdf", CreationCollisionOption.ReplaceExisting);

using (Stream outStream = await outputFile.OpenStreamForWriteAsync())

{

//save the document

await document.SaveAsync(outStream);

//Close the documents

document.Close(true);

loadedDocument.Close(true);

}

{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}

'create the file open picker

Dim picker = New FileOpenPicker()

picker.FileTypeFilter.Add(".pdf")

'Browse the multiple files

Dim files As IReadOnlyList(Of StorageFile) = await picker.PickMultipleFilesAsync()

'Load the existing document

Dim loadedDocument As New PdfLoadedDocument()

await loadedDocument.OpenAsync(files[0]);

'Create booklet with two sides

Dim document As PdfDocument = PdfBookletCreator.CreateBooklet(loadedDocument, New SizeF(1000, 800), False)

Dim localFolder As StorageFolder = Windows.Storage.ApplicationData.Current.LocalFolder

Dim outFile As StorageFile = await localFolder.CreateFileAsync("Booklet.pdf", CreationCollisionOption.ReplaceExisting)

Using outStream As Stream = await outFile.OpenStreamForWriteAsync()

'save the document

await document.SaveAsync(outStream)

'Close the documents

document.Close(True)

loadedDocument.Close(True)

{% endhighlight %}

{% endtabs %}

## Saving the document 

The following code example illustrates how to save the PDF document in Windows Phone.

{% tabs %}

{% highlight c# tabtile="C#" %}

//Load the existing document

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileStream);

//Create booklet with two sides

PdfDocument document = PdfBookletCreator.CreateBooklet(loadedDocument, new SizeF(1000,800), false);

StorageFolder localFolder = Windows.Storage.ApplicationData.Current.LocalFolder;

StorageFile outFile = await localFolder.CreateFileAsync("Booklet.pdf", CreationCollisionOption.ReplaceExisting);

using (Stream outStream = await outFile.OpenStreamForWriteAsync())

{

//save the document

await document.SaveAsync(outStream);

//Close the documents

document.Close(true);

loadedDocument.Close(true);

}

{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}

'Load the existing document

Dim loadedDocument As New PdfLoadedDocument(fileStream)

'Create booklet with two sides

Dim document As PdfDocument = PdfBookletCreator.CreateBooklet(loadedDocument, New SizeF(1000,800), False)

Dim localFolder As StorageFolder = Windows.Storage.ApplicationData.Current.LocalFolder

Dim outFile As StorageFile = await localFolder.CreateFileAsync("Booklet.pdf", CreationCollisionOption.ReplaceExisting)

Using outStream As Stream = await outFile.OpenStreamForWriteAsync()

'save the document

await document.SaveAsync(outStream)

'Close the documents

document.Close(True)

loadedDocument.Close(True)

End Using

{% endhighlight %}

{% endtabs %}