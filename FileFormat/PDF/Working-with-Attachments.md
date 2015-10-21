---
layout: post
title: Working with Attachments
description: File Attachments by using Essential PDF- File Attachments
platform: FileFormat
control: PDF
documentation: UG
---
# Working with Attachments

Essential PDF provides support for file attachments in PDF documents.

Attachments can contain any kind of file with detailed information.

##  Adding attachment to a PDF document

The following code example shows how to add a text file attachment to a PDF document.

{% highlight c# %}
[C#]



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



{% highlight vb.net %}
[VB.NET]



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

Essential PDF also provides support for adding the attachments to existing PDF documents. The following code example illustrates the same.



{% highlight c# %}
[C#]



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



{% highlight vb.net %}
[VB.NET]



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

## Removing attachment from an existing PDF 

Essential PDF allows you to remove the attachments from the existing document as shown in the following code example.

{% highlight c# %}
[C#]

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



{% highlight vb.net %}
[VB.NET]



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



## Extracting and saving an attachment to the disk.

Essential PDF provides supports extracting the attachments and saving them to the disk. The following code example explains how to extract and save an attachment.

{% highlight c# %}
[C#]

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

{% highlight vb.net %}
[VB.NET]

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

