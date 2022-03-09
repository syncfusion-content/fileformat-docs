---
title: Working with Attachments | Syncfusion
description: This section explains how to add, remove and extract attachments in the PDF document. Attachments can contain any kind of file with detailed information. 
platform: file-formats
control: PDF
documentation: UG
---
# Working with Attachments

Essential PDF provides support for file attachments in PDF documents.

Attachments can contain any kind of file with detailed information.

##  Adding attachment to a PDF document

You can add a text file attachment to a PDF document using [PdfAttachment](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfAttachment.html) class. The following code example illustrates this.
{% tabs %}
{% highlight c# tabtitle="C#" %}



//Creates a new PDF document

PdfDocument document = new PdfDocument();

//Creates an attachment

PdfAttachment attachment = new PdfAttachment("Input.txt");

attachment.ModificationDate = DateTime.Now;

attachment.Description = "Input.txt";

attachment.MimeType = "application/txt";

//Adds the attachment to the document

document.Attachments.Add(attachment);

//Saves and closes the PDF document

document.Save("Output.pdf");

document.Close(true);



{% endhighlight %}



{% highlight vb.net tabtitle="VB.NET" %}



'Creates a new PDF document

Dim document As New PdfDocument()

'Creates an attachment

Dim attachment As New PdfAttachment("Input.txt")

attachment.ModificationDate = DateTime.Now

attachment.Description = "Input.txt"

attachment.MimeType = "application/txt"

'Adds the attachment to the document

document.Attachments.Add(attachment)

'Saves and closes the PDF document

document.Save("Output.pdf")

document.Close(True)



{% endhighlight %}

  {% highlight c# tabtitle="UWP" %}

//Creates a new PDF document

PdfDocument document = new PdfDocument();

//Load the file as stream

Stream fileStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Input.txt");

//Creates an attachment

PdfAttachment attachment = new PdfAttachment(@"Input.txt", fileStream);

attachment.ModificationDate = DateTime.Now;

attachment.Description = "Input.txt";

attachment.MimeType = "application/txt";

//Adds the attachment to the document

document.Attachments.Add(attachment);

MemoryStream memoryStream = new MemoryStream();

//Save the document.

await document.SaveAsync(memoryStream);

//Close the documents.

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to pdf/uwp section for respected code samples.

Save(memoryStream, "Output.pdf");        

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Creates a new PDF document

PdfDocument document = new PdfDocument();

Stream fileStream = new FileStream("Input.txt", FileMode.Open, FileAccess.Read);

//Creates an attachment

PdfAttachment attachment = new PdfAttachment("Input.txt", fileStream);

attachment.ModificationDate = DateTime.Now;

attachment.Description = "Input.txt";

attachment.MimeType = "application/txt";

//Adds the attachment to the document

document.Attachments.Add(attachment);

//Save the document into stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

stream.Position = 0;

//Close the documents.

document.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Creates a new PDF document

PdfDocument document = new PdfDocument();

//Creates an attachment

Stream fileStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.txt");

PdfAttachment attachment = new PdfAttachment("Input.txt", fileStream);

attachment.ModificationDate = DateTime.Now;

attachment.Description = "Input.txt";

attachment.MimeType = "application/txt";

//Adds the attachment to the document

document.Attachments.Add(attachment);

//Save the document into stream.

MemoryStream memoryStream = new MemoryStream();

document.Save(memoryStream);

//Close the documents.

document.Close(true);

//Save the stream into pdf file

//The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer pdf/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", memoryStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", memoryStream);
}

{% endhighlight %}

{% endtabs %}

Essential PDF also provides support for adding the attachments to existing PDF documents. The following code example illustrates the same.


{% tabs %}
{% highlight c# tabtitle="C#" %}


//Load an existing PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");

//Create an attachment
PdfAttachment attachment = new PdfAttachment("Input.txt");

attachment.ModificationDate = DateTime.Now;

attachment.Description = "Input.txt";

attachment.MimeType = "application/txt";

if (loadedDocument.Attachments == null)
loadedDocument.CreateAttachment();
//Add the attachment to the document
loadedDocument.Attachments.Add(attachment);

//Saves and closes the PDF document
loadedDocument.Save("Output.pdf");
loadedDocument.Close(true);


{% endhighlight %}



{% highlight vb.net tabtitle="VB.NET" %}

'Load an existing PDF document
Dim loadedDocument As New PdfLoadedDocument("Input.pdf")

'Create an attachment
Dim attachment As New PdfAttachment("Input.txt")

attachment.ModificationDate = DateTime.Now

attachment.Description = "Input.txt"

attachment.MimeType = "application/txt"

If loadedDocument.Attachments Is Nothing Then
	loadedDocument.CreateAttachment()
End If
'Add the attachment to the document
loadedDocument.Attachments.Add(attachment)

'Saves and closes the PDF document
loadedDocument.Save("Output.pdf")
loadedDocument.Close(True)

{% endhighlight %}

  {% highlight c# tabtitle="UWP" %}

//Create the file open picker

var picker = new FileOpenPicker();

picker.FileTypeFilter.Add(".pdf");

//Browse and chose the file

StorageFile file = await picker.PickSingleFileAsync();

//Creates an empty PDF loaded document instance

PdfLoadedDocument loadedDocument = new PdfLoadedDocument();

//Loads or opens an existing PDF document through Open method of PdfLoadedDocument class

await loadedDocument.OpenAsync(file);

//Load the file as stream

Stream fileStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Input.txt");

//Creates an attachment

PdfAttachment attachment = new PdfAttachment("Input.txt", fileStream);

attachment.ModificationDate = DateTime.Now;

attachment.Description = "Input.txt";

attachment.MimeType = "application/txt";

if (loadedDocument.Attachments == null)
    loadedDocument.CreateAttachment();
//Add the attachment to the document
loadedDocument.Attachments.Add(attachment);

MemoryStream memoryStream = new MemoryStream();

//Save the document.

await loadedDocument.SaveAsync(memoryStream);

//Close the documents.

loadedDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to pdf/uwp section for respected code samples.

Save(memoryStream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load the PDF document

FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

Stream fileStream = new FileStream("Input.txt", FileMode.Open, FileAccess.Read);

//Creates an attachment

PdfAttachment attachment = new PdfAttachment("Input.txt", fileStream);

attachment.ModificationDate = DateTime.Now;

attachment.Description = "Input.txt";

attachment.MimeType = "application/txt";

if (loadedDocument.Attachments == null)
    loadedDocument.CreateAttachment();
//Add the attachment to the document
loadedDocument.Attachments.Add(attachment);


//Save the document into stream.

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

stream.Position = 0;

//Close the documents.

loadedDocument.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Creates an attachment

Stream fileStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.txt");

PdfAttachment attachment = new PdfAttachment("Input.txt", fileStream);

attachment.ModificationDate = DateTime.Now;

attachment.Description = "Input.txt";

attachment.MimeType = "application/txt";

if (loadedDocument.Attachments == null)
    loadedDocument.CreateAttachment();
//Add the attachment to the document
loadedDocument.Attachments.Add(attachment);

//Save the document into stream.

MemoryStream memoryStream = new MemoryStream();

loadedDocument.Save(memoryStream);

//Close the documents.

loadedDocument.Close(true);

//Save the stream into pdf file

//The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer pdf/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", memoryStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", memoryStream);
}

{% endhighlight %}

{% endtabs %}

## Removing attachment from an existing PDF 

Essential PDF allows you to remove the attachments from the existing document by using [Remove](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfAttachmentCollection.html#Syncfusion_Pdf_Interactive_PdfAttachmentCollection_Remove_Syncfusion_Pdf_Interactive_PdfAttachment_) method, as shown in the following code example.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Loads the PDF document

PdfLoadedDocument document = new PdfLoadedDocument("Input.pdf");

//Removes an attachment

PdfAttachment attachment = document.Attachments[0];

document.Attachments.Remove(attachment);

document.Attachments.RemoveAt(1);

//Saves and closes the document

document.Save("Output.pdf");

document.Close(true);



{% endhighlight %}



{% highlight vb.net tabtitle="VB.NET" %}



'Loads the PDF document

Dim document As New PdfLoadedDocument("Input.pdf")

'Removes an attachments

Dim attachment As PdfAttachment = document.Attachments(0)

document.Attachments.Remove(attachment)

document.Attachments.RemoveAt(1)

'Saves and closes the document

document.Save("Output.pdf")

document.Close(True)



{% endhighlight %}

  {% highlight c# tabtitle="UWP" %}

//Create the file open picker

var picker = new FileOpenPicker();

picker.FileTypeFilter.Add(".pdf");

//Browse and chose the file

StorageFile file = await picker.PickSingleFileAsync();

//Creates an empty PDF loaded document instance

PdfLoadedDocument document = new PdfLoadedDocument();

//Loads or opens an existing PDF document through Open method of PdfLoadedDocument class

await document.OpenAsync(file);

//Removes an attachment

PdfAttachment attachment = document.Attachments[0];

document.Attachments.Remove(attachment);

document.Attachments.RemoveAt(1);

MemoryStream memoryStream = new MemoryStream();

//Save the document.

await document.SaveAsync(memoryStream);

//Close the documents.

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to pdf/uwp section for respected code samples.

Save(memoryStream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load the PDF document

FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);

PdfLoadedDocument document = new PdfLoadedDocument(docStream);

//Removes an attachment

PdfAttachment attachment = document.Attachments[0];

//document.Attachments.Remove(attachment);

document.Attachments.RemoveAt(0);


//Save the document into stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

stream.Position = 0;

//Close the documents.

document.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Load the file as stream

 Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");

 PdfLoadedDocument document = new PdfLoadedDocument(docStream);

 //Removes an attachment

 PdfAttachment attachment = document.Attachments[0];

 document.Attachments.Remove(attachment);

 //document.Attachments.RemoveAt(1);

 //Save the document into stream.

 MemoryStream memoryStream = new MemoryStream();

 document.Save(memoryStream);

 //Close the documents.

 document.Close(true);

 //Save the stream into pdf file

 //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer pdf/xamarin section for respective code samples.
 if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
 {
     Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", memoryStream);
 }
 else
 {
     Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", memoryStream);
 }

{% endhighlight %}

{% endtabs %}

## Extracting and saving an attachment to the disk.

Essential PDF provides support for extracting the attachments and saving them to the disk. The following code example explains how to extract and save an attachment.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Loads the PDF document

PdfLoadedDocument document = new PdfLoadedDocument("Sample.pdf");

//Iterates the attachments

foreach (PdfAttachment attachment in document.Attachments)

{

//Extracts the attachment and saves it to the disk

FileStream s = new FileStream(attachment.FileName, FileMode.Create);

s.Write(attachment.Data, 0, attachment.Data.Length);

s.Dispose();

}

//Saves and closes the document

document.Save("Output.pdf");

document.Close(true);



{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Loads the PDF document

Dim document As New PdfLoadedDocument("Sample.pdf")

'Iterates the attachments

For Each attachment As PdfAttachment In document.Attachments

'Extracts the attachment and saves it to the disk

Dim s As New FileStream(attachment.FileName, FileMode.Create)

s.Write(attachment.Data, 0, attachment.Data.Length)

s.Dispose()

Next

'Saves and closes the document

document.Save("Output.pdf")

document.Close(True)



{% endhighlight %}

  {% highlight c# tabtitle="UWP" %}

//PDF supports extracting and saving an attachment to the disk only in Windows Forms, WPF, ASP.NET, ASP.NET MVC and ASP.NET Core platforms.

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load the PDF document

FileStream docStream = new FileStream("Output.pdf", FileMode.Open, FileAccess.Read);

PdfLoadedDocument document = new PdfLoadedDocument(docStream);

//Iterates the attachments

foreach (PdfAttachment attachment in document.Attachments)

{

    //Extracts the attachment and saves it to the disk

    FileStream s = new FileStream(attachment.FileName, FileMode.Create);

    s.Write(attachment.Data, 0, attachment.Data.Length);

    s.Dispose();

}


//Save the document into stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

stream.Position = 0;

//Close the documents.

document.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//PDF supports extracting and saving an attachment to the disk only in Windows Forms, WPF, ASP.NET, ASP.NET MVC and ASP.NET Core platforms.

{% endhighlight %}

{% endtabs %}
