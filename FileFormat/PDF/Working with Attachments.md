---
layout: Post
title: Working with Attachments
description: File Attachments using Essential PDF: File Attachments
platform: FileFormat
control: PDF
documentation: UG
---
# Working with Attachments

Essential PDF provides support for file attachments in PDF documents.

Attachments can contain any kind of file with detailed information.

##  Adding attachment to a PDF document

The below code snippet shows how to add a text file attachment to a PDF document.

{% highlight c# %}
[C#]



//Create a new PDF document

PdfDocument document = new PdfDocument();

//Create an attachment

PdfAttachment attachment = new PdfAttachment("Input.txt");

attachment.ModificationDate = DateTime.Now;

attachment.Description = "Input.txt";

attachment.MimeType = "application/txt";

//Add the attachment to the document

document.Attachments.Add(attachment);

//Save and close the PDF document

document.Save("Output.pdf");

document.Close(true);



{% endhighlight %}



{% highlight vb.net %}
[VB.NET]



'Create a new PDF document

Dim document As New PdfDocument()

'Create an attachment

Dim attachment As New PdfAttachment("Input.txt")

attachment.ModificationDate = DateTime.Now

attachment.Description = "Input.txt"

attachment.MimeType = "application/txt"

'Add the attachment to the document

document.Attachments.Add(attachment)

'Save and close the PDF document

document.Save("Output.pdf")

document.Close(True)



{% endhighlight %}

Essential PDF also provides support for adding the attachments to existing PDF documents. The below code snippet illustrates the same.



{% highlight c# %}
[C#]



//Create a new PDF document

PdfDocument document = new PdfDocument();

//Create an attachment

PdfAttachment attachment = new PdfAttachment("Input.txt");

attachment.ModificationDate = DateTime.Now;

attachment.Description = "Input.txt";

attachment.MimeType = "application/txt";

//Add the attachment to the document

document.Attachments.Add(attachment);

//Save and close the PDF document

document.Save("Output.pdf");

document.Close(true);



{% endhighlight %}



{% highlight vb.net %}
[VB.NET]



'Create a new PDF document

Dim document As New PdfDocument()

'Create an attachment

Dim attachment As New PdfAttachment("Input.txt")

attachment.ModificationDate = DateTime.Now

attachment.Description = "Input.txt"

attachment.MimeType = "application/txt"

'Add the attachment to the document

document.Attachments.Add(attachment)

'Save and close the PDF document

document.Save("Output.pdf")

document.Close(True)



{% endhighlight %}

## Removing attachment from an existing PDF 

Essential PDF allows you to remove the attachments from the existing document, as shown in the below code snippet.

{% highlight c# %}
[C#]

//Load the PDF document

PdfLoadedDocument document = new PdfLoadedDocument("Input.pdf");

//Remove an attachment

PdfAttachment attachment = document.Attachments[0];

document.Attachments.Remove(attachment);

document.Attachments.RemoveAt(1);

//Save and close the document

document.Save("Output.pdf");

document.Close(true);



{% endhighlight %}



{% highlight vb.net %}
[VB.NET]



'Load the PDF document

Dim document As New PdfLoadedDocument("Input.pdf")

'Remove an attachments

Dim attachment As PdfAttachment = document.Attachments(0)

document.Attachments.Remove(attachment)

document.Attachments.RemoveAt(1)

'Save and close the document

document.Save("Output.pdf")

document.Close(True)



{% endhighlight %}



## Extracting and saving an attachment to the disk.

Essential PDF provides supports extracting the attachments and saving them to the disk. The following code snippet explains how to extract and save an attachment.

{% highlight c# %}
[C#]

//Load the PDF document

PdfLoadedDocument document = new PdfLoadedDocument("Sample.pdf");

//Iterate the attachments

foreach (PdfAttachment attachment in document.Attachments)

{

//Extracting the attachment and saving it to the disk

FileStream s = new FileStream(attachment.FileName, FileMode.Create);

s.Write(attachment.Data, 0, attachment.Data.Length);

s.Dispose();

}

//Save and close the document

document.Save("Output.pdf");

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Load the PDF document

Dim document As New PdfLoadedDocument("Sample.pdf")

'Iterate the attachments

For Each attachment As PdfAttachment In document.Attachments

'Extracting the attachment and saving it to the disk

Dim s As New FileStream(attachment.FileName, FileMode.Create)

s.Write(attachment.Data, 0, attachment.Data.Length)

s.Dispose()

Next

'Save and close the document

document.Save("Output.pdf")

document.Close(True)



{% endhighlight %}

