---
title: Working with Attachments | Syncfusion
description: This section explains how to add, remove and extract attachments in the PDF document using Syncfusion .NET PDF Library. 
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

{% highlight c# tabtitle="C# [Cross-platform]" %}	

//Create a new PDF document
PdfDocument document = new PdfDocument();
//Creates an attachment
Stream fileStream = new FileStream("Input.txt", FileMode.Open, FileAccess.Read);
PdfAttachment attachment = new PdfAttachment("Input.txt", fileStream);
attachment.ModificationDate = DateTime.Now;
attachment.Description = "Input.txt";
attachment.MimeType = "application/txt";
//Adds the attachment to the document
document.Attachments.Add(attachment);

//Save the document into stream
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Close the document
document.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Create a new PDF document
PdfDocument document = new PdfDocument();
//Create an attachment
PdfAttachment attachment = new PdfAttachment("Input.txt");
attachment.ModificationDate = DateTime.Now;
attachment.Description = "Input.txt";
attachment.MimeType = "application/txt";
//Adds the attachment to the document
document.Attachments.Add(attachment);

//Save and close the PDF document
document.Save("Output.pdf");
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Create a new PDF document
Dim document As New PdfDocument()
'Create an attachment
Dim attachment As New PdfAttachment("Input.txt")
attachment.ModificationDate = DateTime.Now
attachment.Description = "Input.txt"
attachment.MimeType = "application/txt"
'Adds the attachment to the document
document.Attachments.Add(attachment)

'Save and close the PDF document
document.Save("Output.pdf")
document.Close(True)

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Attachment/Adding-attachment-to-a-PDF-document/).

Essential PDF also provides support for adding the attachments to existing PDF documents by using [PdfAttachment](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfAttachment.html) class. The following code example illustrates the same.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Load the PDF document
FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);
//Creates an attachment
Stream fileStream = new FileStream("Input.txt", FileMode.Open, FileAccess.Read);
PdfAttachment attachment = new PdfAttachment("Input.txt", fileStream);
attachment.ModificationDate = DateTime.Now;
attachment.Description = "Input.txt";
attachment.MimeType = "application/txt";
if (loadedDocument.Attachments == null)
    loadedDocument.CreateAttachment();
//Add the attachment to the document
loadedDocument.Attachments.Add(attachment);

//Save the document into stream
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);
//Close the document
loadedDocument.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

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

//Save and close the PDF document
loadedDocument.Save("Output.pdf");
loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

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

'Save and close the PDF document
loadedDocument.Save("Output.pdf")
loadedDocument.Close(True)

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Attachment/Adding-the-attachments-to-an-existing-PDF-document/).

## Removing attachment from an existing PDF 

Essential PDF allows you to remove the attachments from the existing document by using [Remove](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfAttachmentCollection.html#Syncfusion_Pdf_Interactive_PdfAttachmentCollection_Remove_Syncfusion_Pdf_Interactive_PdfAttachment_) and [RemoveAt](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfAttachmentCollection.html#Syncfusion_Pdf_Interactive_PdfAttachmentCollection_RemoveAt_System_Int32_) method in [PdfAttachment](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfAttachment.html) class. The following code example explains the same.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Load the PDF document
FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument document = new PdfLoadedDocument(docStream);
//Removes an attachment
PdfAttachment attachment = document.Attachments[0];
//document.Attachments.Remove(attachment);
document.Attachments.RemoveAt(0);

//Save the document into stream
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Close the document
document.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Loads the PDF document
PdfLoadedDocument document = new PdfLoadedDocument("Input.pdf");
//Removes an attachment
PdfAttachment attachment = document.Attachments[0];
document.Attachments.Remove(attachment);
document.Attachments.RemoveAt(1);

//Save and close the document
document.Save("Output.pdf");
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Loads the PDF document
Dim document As New PdfLoadedDocument("Input.pdf")
'Removes an attachments
Dim attachment As PdfAttachment = document.Attachments(0)
document.Attachments.Remove(attachment)
document.Attachments.RemoveAt(1)

'Save and close the document
document.Save("Output.pdf")
document.Close(True)

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Attachment/Remove-attachment-from-an-existing-PDF-document/).

## Extracting and saving an attachment to the disk.

Essential PDF provides support for extracting the attachments and saving them to the disk. The following code example explains how to extract and save an attachment using [PdfAttachment](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfAttachment.html) class.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

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

//Save the document into stream
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Close the document
document.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

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

//Save and close the document
document.Save("Output.pdf");
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Loads the PDF document
Dim document As New PdfLoadedDocument("Sample.pdf")
'Iterates the attachments
For Each attachment As PdfAttachment In document.Attachments
    'Extracts the attachment and saves it to the disk
    Dim s As New FileStream(attachment.FileName, FileMode.Create)
    s.Write(attachment.Data, 0, attachment.Data.Length)
    s.Dispose()
Next

'Save and close the document
document.Save("Output.pdf")
document.Close(True)

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Attachment/Extract-and-saving-an-attachment-to-the-disk/).