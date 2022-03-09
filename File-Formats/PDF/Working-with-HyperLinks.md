---
title: Working with Hyperlinks | Syncfusion
description: This section explains how to add hyperlink in the PDF document using Essential PDF
platform: file-formats
control: PDF
documentation: UG
---
# Working with Hyperlinks

In PDF, hyperlinks can be added to allow the users to navigate to another part of PDF file, web page or any other external content. Essential PDF provides support for all these types of hyperlink.

## Working with Web navigation                                                                                                                                             

You can navigate to specified URL from a PDF document by using the [PdfTextWebLink](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfTextWebLink.html) class.

Please refer the below code snippet for navigating to the web page.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 12f);

//Create the Text Web Link.

PdfTextWebLink textLink = new PdfTextWebLink();

//Set the hyperlink

textLink.Url = "http://www.syncfusion.com";

//Set the link text

textLink.Text = "Syncfusion .NET components and controls";

//Set the font

textLink.Font = font;

//Draw the hyperlink in PDF page

textLink.DrawTextWebLink(page, new PointF(10, 40));

//Save the document.

document.Save("Output.pdf");

//Close the document.

document.Close(true);





{% endhighlight %}



{% highlight vb.net tabtile="VB.NET" %}

'Create a new PDF document.

Dim document As New PdfDocument()

'Add a page to the document.

Dim page As PdfPage = document.Pages.Add()

'Create the font.

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 12.0F)

'Create the Text Web Link.

Dim textLink As New PdfTextWebLink()

'Add the hyperlink

textLink.Url = "http://www.syncfusion.com"

'Set the link text

textLink.Text = "Syncfusion .NET components and controls"

'Set the font

textLink.Font = font

'Draw the hyperlink in  PDF page

textLink.DrawTextWebLink(loadedPage.Graphics, New PointF(10, 40))

'Save the document.

document.Save("Output.pdf")

'Close the document.

document.Close(True)





{% endhighlight %}

{% highlight c# tabtile="UWP" %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 12f);

//Create the Text Web Link.

PdfTextWebLink textLink = new PdfTextWebLink();

//Set the hyperlink

textLink.Url = "http://www.syncfusion.com";

//Set the link text

textLink.Text = "Syncfusion .NET components and controls";

//Set the font

textLink.Font = font;

//Draw the hyperlink in PDF page

textLink.DrawTextWebLink(page, new PointF(10, 40));

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 12f);

//Create the Text Web Link.

PdfTextWebLink textLink = new PdfTextWebLink();

//Set the hyperlink

textLink.Url = "http://www.syncfusion.com";

//Set the link text

textLink.Text = "Syncfusion .NET components and controls";

//Set the font

textLink.Font = font;

//Draw the hyperlink in PDF page

textLink.DrawTextWebLink(page, new PointF(10, 40));

//Save the document into stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

stream.Position = 0;

//Closes the document

document.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 12f);

//Create the Text Web Link.

PdfTextWebLink textLink = new PdfTextWebLink();

//Set the hyperlink

textLink.Url = "http://www.syncfusion.com";

//Set the link text

textLink.Text = "Syncfusion .NET components and controls";

//Set the font

textLink.Font = font;

//Draw the hyperlink in PDF page

textLink.DrawTextWebLink(page, new PointF(10, 40));

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Closes the document

document.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}  


To add a web hyperlink to an existing document, please refer the below code snippet.

{% tabs %}  

{% highlight c# tabtile="C#" %}


//Load the existing PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(@"Filename.pdf");

//Load the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 12f);

//Create the Text Web Link.

PdfTextWebLink textLink = new PdfTextWebLink();

//Set the hyperlink

textLink.Url = "http://www.syncfusion.com";

//Set the link text

textLink.Text = "Syncfusion .NET components and controls";

//Set the font

textLink.Font = font;

//Draw the hyperlink in loaded page graphics

textLink.DrawTextWebLink(loadedPage.Graphics, new PointF(10, 40));

//Save the document.

loadedDocument.Save("Output.pdf");

//Close the document.

loadedDocument.Close(true);





{% endhighlight %}



{% highlight vb.net tabtile="VB.NET" %}

'Load the existing PDF document.

Dim loadedDocument As New PdfLoadedDocument("fileName.pdf")

'Load the page

Dim loadedPage As PdfLoadedPage = TryCast(loadedDocument.Pages(0), PdfLoadedPage)

'Create the font.

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 12.0F)

'Create the Text Web Link.

Dim textLink As New PdfTextWebLink()

'Add the hyperlink

textLink.Url = "http://www.syncfusion.com"

'Set the link text

textLink.Text = "Syncfusion .NET components and controls"

'Set the font

textLink.Font = font

'Draw the hyperlink in loaded page graphics

textLink.DrawTextWebLink(loadedPage.Graphics, New PointF(10, 40))

'Save the document.

loadedDocument.Save("Output1.pdf")

'Close the document.

loadedDocument.Close(True)





{% endhighlight %}

{% highlight c# tabtile="UWP" %}

//Create the file open picker

var picker = new FileOpenPicker();

picker.FileTypeFilter.Add(".pdf");

//Browse and chose the file

StorageFile file = await picker.PickSingleFileAsync();

//Creates an empty PDF loaded document instance

PdfLoadedDocument loadedDocument = new PdfLoadedDocument();

//Loads or opens an existing PDF document through Open method of PdfLoadedDocument class

await loadedDocument.OpenAsync(file);

//Load the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 12f);

//Create the Text Web Link.

PdfTextWebLink textLink = new PdfTextWebLink();

//Set the hyperlink

textLink.Url = "http://www.syncfusion.com";

//Set the link text

textLink.Text = "Syncfusion .NET components and controls";

//Set the font

textLink.Font = font;

//Draw the hyperlink in loaded page graphics

textLink.DrawTextWebLink(loadedPage.Graphics, new PointF(10, 40));

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await loadedDocument.SaveAsync(stream);

//Close the document

loadedDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Load the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 12f);

//Create the Text Web Link.

PdfTextWebLink textLink = new PdfTextWebLink();

//Set the hyperlink

textLink.Url = "http://www.syncfusion.com";

//Set the link text

textLink.Text = "Syncfusion .NET components and controls";

//Set the font

textLink.Font = font;

//Draw the hyperlink in loaded page graphics

textLink.DrawTextWebLink(loadedPage.Graphics, new PointF(10, 40));

//Save the document into stream

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

stream.Position = 0;

//Closes the document

loadedDocument.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}

//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Load the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 12f);

//Create the Text Web Link.

PdfTextWebLink textLink = new PdfTextWebLink();

//Set the hyperlink

textLink.Url = "http://www.syncfusion.com";

//Set the link text

textLink.Text = "Syncfusion .NET components and controls";

//Set the font

textLink.Font = font;

//Draw the hyperlink in loaded page graphics

textLink.DrawTextWebLink(loadedPage.Graphics, new PointF(10, 40));

//Save the document into stream

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

stream.Position = 0;

//Closes the document

loadedDocument.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% endtabs %}  


## Working with internal document navigation

To allow the users to navigate to any other part of the same document, [PdfDocumentLinkAnnotation](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfDocumentLinkAnnotation.html) class can be used. The below code explains how to add the hyperlink for internal document navigation.

{% tabs %}  

{% highlight c# tabtile="C#" %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Create a new page 

PdfPage page = document.Pages.Add();

//Create a new rectangle

RectangleF docLinkAnnotationBounds = new RectangleF(10, 40, 30, 30);

//Create a new document link annotation.

PdfDocumentLinkAnnotation documentLinkAnnotation = new PdfDocumentLinkAnnotation(docLinkAnnotationBounds);

//Set the annotation flags.

documentLinkAnnotation.AnnotationFlags = PdfAnnotationFlags.NoRotate;

//Set the annotation text.

documentLinkAnnotation.Text = "Document link annotation";

//Set the annotation's color.

documentLinkAnnotation.Color = new PdfColor(Color.Navy);

//Creates another page 

PdfPage navigationPage = document.Pages.Add();

//Set the destination.

documentLinkAnnotation.Destination = new PdfDestination(navigationPage);

//Set the document link annotation location.

documentLinkAnnotation.Destination.Location = new Point(10, 0);

//Set the document annotation zoom level

documentLinkAnnotation.Destination.Zoom = 5;

//Add this annotation to a new page.

page.Annotations.Add(documentLinkAnnotation);

//Save the document to disk.

document.Save("DocumentLinkAnnotation.pdf");

//Close the document

document.Close();





{% endhighlight %}



{% highlight vb.net tabtile="VB.NET" %}

'Create a new PDF document.

Dim document As New PdfDocument()

'Create a new page 

Dim page As PdfPage = document.Pages.Add()

'Create a new rectangle

Dim docLinkAnnotationBounds As New RectangleF(10, 40, 30, 30)

'Create a new document link annotation.

Dim documentLinkAnnotation As New PdfDocumentLinkAnnotation(docLinkAnnotationBounds)

'Set the annotation flags.

documentLinkAnnotation.AnnotationFlags = PdfAnnotationFlags.NoRotate

'Set the annotation text.

documentLinkAnnotation.Text = "Document link annotation"

'Set the annotation's color.

documentLinkAnnotation.Color = New PdfColor(Color.Navy)

'Create another page

Dim navigationPage As PdfPage = document.Pages.Add()

'Set the destination.

documentLinkAnnotation.Destination = New PdfDestination(navigationPage)

'Set the document link annotation location.

documentLinkAnnotation.Destination.Location = New Point(10, 0)

'Set the document annotation zoom level

documentLinkAnnotation.Destination.Zoom = 5

'Add this annotation to a new page.

page.Annotations.Add(documentLinkAnnotation)

'Save the document to disk.

document.Save("DocumentLinkAnnotation.pdf")

'Close the document

document.Close()





{% endhighlight %}

{% highlight c# tabtile="UWP" %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Create a new page 

PdfPage page = document.Pages.Add();

//Create a new rectangle

RectangleF docLinkAnnotationBounds = new RectangleF(10, 40, 30, 30);

//Create a new document link annotation.

PdfDocumentLinkAnnotation documentLinkAnnotation = new PdfDocumentLinkAnnotation(docLinkAnnotationBounds);

//Set the annotation flags.

documentLinkAnnotation.AnnotationFlags = PdfAnnotationFlags.NoRotate;

//Set the annotation text.

documentLinkAnnotation.Text = "Document link annotation";

//Set the annotation's color.

documentLinkAnnotation.Color = new PdfColor(System.Drawing.Color.FromArgb(0, 0, 0, 128));

//Creates another page 

PdfPage navigationPage = document.Pages.Add();

//Set the destination.

documentLinkAnnotation.Destination = new PdfDestination(navigationPage);

//Set the document link annotation location.

documentLinkAnnotation.Destination.Location = new PointF(10, 0);

//Set the document annotation zoom level

documentLinkAnnotation.Destination.Zoom = 5;

//Add this annotation to a new page.

page.Annotations.Add(documentLinkAnnotation);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "DocumentLinkAnnotation.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Create a new page 

PdfPage page = document.Pages.Add();

//Create a new rectangle

RectangleF docLinkAnnotationBounds = new RectangleF(10, 40, 30, 30);

//Create a new document link annotation.

PdfDocumentLinkAnnotation documentLinkAnnotation = new PdfDocumentLinkAnnotation(docLinkAnnotationBounds);

//Set the annotation flags.

documentLinkAnnotation.AnnotationFlags = PdfAnnotationFlags.NoRotate;

//Set the annotation text.

documentLinkAnnotation.Text = "Document link annotation";

//Set the annotation's color.

documentLinkAnnotation.Color = new PdfColor(Color.Navy);

//Creates another page 

PdfPage navigationPage = document.Pages.Add();

//Set the destination.

documentLinkAnnotation.Destination = new PdfDestination(navigationPage);

//Set the document link annotation location.

documentLinkAnnotation.Destination.Location = new PointF(10, 0);

//Set the document annotation zoom level

documentLinkAnnotation.Destination.Zoom = 5;

//Add this annotation to a new page.

page.Annotations.Add(documentLinkAnnotation);

//Save the document into stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

stream.Position = 0;

//Closes the document

document.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "DocumentLinkAnnotation.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Create a new page 

PdfPage page = document.Pages.Add();

//Create a new rectangle

RectangleF docLinkAnnotationBounds = new RectangleF(10, 40, 30, 30);

//Create a new document link annotation.

PdfDocumentLinkAnnotation documentLinkAnnotation = new PdfDocumentLinkAnnotation(docLinkAnnotationBounds);

//Set the annotation flags.

documentLinkAnnotation.AnnotationFlags = PdfAnnotationFlags.NoRotate;

//Set the annotation text.

documentLinkAnnotation.Text = "Document link annotation";

//Set the annotation's color.

documentLinkAnnotation.Color = new PdfColor(Syncfusion.Drawing.Color.Navy);

//Creates another page 

PdfPage navigationPage = document.Pages.Add();

//Set the destination.

documentLinkAnnotation.Destination = new PdfDestination(navigationPage);

//Set the document link annotation location.

documentLinkAnnotation.Destination.Location = new PointF(10, 0);

//Set the document annotation zoom level

documentLinkAnnotation.Destination.Zoom = 5;

//Add this annotation to a new page.

page.Annotations.Add(documentLinkAnnotation);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Closes the document

document.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("DocumentLinkAnnotation.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("DocumentLinkAnnotation.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}  

To add a [PdfDocumentLinkAnnotation](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfDocumentLinkAnnotation.html) to an existing document, please use the below code snippet.

{% tabs %}  

{% highlight c# tabtile="C#" %}

//Load the existing PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(@"fileName.pdf");

//Load the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create a new rectangle

RectangleF docLinkAnnotationBounds = new RectangleF(10, 40, 30, 30);

//Create a new document link annotation.

PdfDocumentLinkAnnotation documentLinkAnnotation = new PdfDocumentLinkAnnotation(docLinkAnnotationBounds);

//Set the annotation text.

documentLinkAnnotation.Text = "Document link annotation";

//Set the existing page for navigation

PdfLoadedPage navigationPage = loadedDocument.Pages[1] as PdfLoadedPage;

//Set the pdf destination.

documentLinkAnnotation.Destination = new PdfDestination(navigationPage);

//Set the document link annotation location.

documentLinkAnnotation.Destination.Location = new Point(10, 0);

//Add this annotation to respective page.

loadedPage.Annotations.Add(documentLinkAnnotation);

//Save the document to disk.

loadedDocument.Save("DocumentLinkAnnotation.pdf");

//Close the document

loadedDocument.Close();





{% endhighlight %}



{% highlight vb.net tabtile="VB.NET" %}
'Load the existing PDF document.

Dim loadedDocument As New PdfLoadedDocument("fileName.pdf")

'Load the page

Dim loadedPage As PdfLoadedPage = TryCast(loadedDocument.Pages(0), PdfLoadedPage)

'Create a new rectangle

Dim docLinkAnnotationBounds As New RectangleF(10, 40, 30, 30)

'Create a new document link annotation.

Dim documentLinkAnnotation As New PdfDocumentLinkAnnotation(docLinkAnnotationBounds)

'Set the annotation text.

documentLinkAnnotation.Text = "Document link annotation"

'Set the existing page for navigation

Dim navigationPage As PdfLoadedPage = TryCast(loadedDocument.Pages(1), PdfLoadedPage)

'Set the pdf destination.

documentLinkAnnotation.Destination = New PdfDestination(navigationPage)

'Set the document link annotation location.

documentLinkAnnotation.Destination.Location = New Point(10, 0)

'Add this annotation to respective page.

loadedPage.Annotations.Add(documentLinkAnnotation)

'Save the document to disk.

loadedDocument.Save("DocumentLinkAnnotation.pdf")

'Close the document

loadedDocument.Close()





{% endhighlight %}

{% highlight c# tabtile="UWP" %}

//Create the file open picker

var picker = new FileOpenPicker();

picker.FileTypeFilter.Add(".pdf");

//Browse and chose the file

StorageFile file = await picker.PickSingleFileAsync();

//Creates an empty PDF loaded document instance

PdfLoadedDocument loadedDocument = new PdfLoadedDocument();

//Loads or opens an existing PDF document through Open method of PdfLoadedDocument class

await loadedDocument.OpenAsync(file);

//Load the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create a new rectangle

RectangleF docLinkAnnotationBounds = new RectangleF(10, 40, 30, 30);

//Create a new document link annotation.

PdfDocumentLinkAnnotation documentLinkAnnotation = new PdfDocumentLinkAnnotation(docLinkAnnotationBounds);

//Set the annotation text.

documentLinkAnnotation.Text = "Document link annotation";

//Set the existing page for navigation

PdfLoadedPage navigationPage = loadedDocument.Pages[1] as PdfLoadedPage;

//Set the pdf destination.

documentLinkAnnotation.Destination = new PdfDestination(navigationPage);

//Set the document link annotation location.

documentLinkAnnotation.Destination.Location = new System.Drawing.PointF(10, 0);

//Add this annotation to respective page.

loadedPage.Annotations.Add(documentLinkAnnotation);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await loadedDocument.SaveAsync(stream);

//Close the document

loadedDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "DocumentLinkAnnotation.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document

FileStream docStream = new FileStream("fileName.pdf", FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Load the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create a new rectangle

RectangleF docLinkAnnotationBounds = new RectangleF(10, 40, 30, 30);

//Create a new document link annotation.

PdfDocumentLinkAnnotation documentLinkAnnotation = new PdfDocumentLinkAnnotation(docLinkAnnotationBounds);

//Set the annotation text.

documentLinkAnnotation.Text = "Document link annotation";

//Set the existing page for navigation

PdfLoadedPage navigationPage = loadedDocument.Pages[1] as PdfLoadedPage;

//Set the pdf destination.

documentLinkAnnotation.Destination = new PdfDestination(navigationPage);

//Set the document link annotation location.

documentLinkAnnotation.Destination.Location = new PointF(10, 0);

//Add this annotation to respective page.

loadedPage.Annotations.Add(documentLinkAnnotation);

//Save the document into stream

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

stream.Position = 0;

//Closes the document

loadedDocument.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "DocumentLinkAnnotation.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Load the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create a new rectangle

RectangleF docLinkAnnotationBounds = new RectangleF(10, 40, 30, 30);

//Create a new document link annotation.

PdfDocumentLinkAnnotation documentLinkAnnotation = new PdfDocumentLinkAnnotation(docLinkAnnotationBounds);

//Set the annotation text.

documentLinkAnnotation.Text = "Document link annotation";

//Set the existing page for navigation

PdfLoadedPage navigationPage = loadedDocument.Pages[1] as PdfLoadedPage;

//Set the pdf destination.

documentLinkAnnotation.Destination = new PdfDestination(navigationPage);

//Set the document link annotation location.

documentLinkAnnotation.Destination.Location = new Syncfusion.Drawing.PointF(10, 0);

//Add this annotation to respective page.

loadedPage.Annotations.Add(documentLinkAnnotation);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Closes the document

loadedDocument.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("DocumentLinkAnnotation.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("DocumentLinkAnnotation.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}  


## Working with external document navigation

You can open external documents like images, text files, PDF, etc. using [PdfFileLinkAnnotation](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfFileLinkAnnotation.html) class.

Please refer the below code snippet for navigating to external documents:

{% tabs %}  

{% highlight c# tabtile="C#" %}

//Create the PDF document

PdfDocument document = new PdfDocument();

//Creates a new page 

PdfPage page = document.Pages.Add();

//Create a new rectangle

RectangleF bounds = new RectangleF(10, 40, 30, 30);

//Create a link for image file 

PdfFileLinkAnnotation fileLinkAnnotation = new PdfFileLinkAnnotation(bounds, @"..\..\Data\logo.png");

//Add this annotation to a page.

page.Annotations.Add(fileLinkAnnotation);

//Save the document to disk.

document.Save("FileLinkAnnotation.pdf");

//close the document

document.Close();





{% endhighlight %}



{% highlight vb.net tabtile="VB.NET" %}

'Create the PDF document

Dim document As New PdfDocument()

'Creates a new page and adds it as the last page of the document

Dim page As PdfPage = document.Pages.Add()

'Create a new rectangle

Dim rectangle As New RectangleF(10, 40, 30, 30)

'Create a link for image file 

Dim fileLinkAnnotation As New PdfFileLinkAnnotation(rectangle, "..\..\Data\logo.png")

'Add this annotation to a page.

page.Annotations.Add(fileLinkAnnotation)

'Save the document to disk.

document.Save("FileLinkAnnotation.pdf")

'close the document

document.Close()





{% endhighlight %}

{% highlight c# tabtile="UWP" %}

//PDF supports external document navigation only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

{% endhighlight %}

{% highlight ASP.NET Core %}

//PDF supports external document navigation only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}

//PDF supports external document navigation only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

{% endhighlight %}

{% endtabs %}  

N> The above link makes use of the absolute path of the file for navigation. So, moving the files to another machine or location may lead to file not found error in PDF reader applications.

To open a file in relative path, the [PdfLaunchAction](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfLaunchAction.html) can be used. While using the relative path in launch action, the files can be moved to any machine, provided the relative path is being maintained. The below code snippet explains the same.

{% tabs %}  

{% highlight c# tabtile="C#" %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Create a new page

PdfPage page = document.Pages.Add();

//Create the button field

PdfButtonField submitButton = new PdfButtonField(page, "submitButton");

submitButton.Bounds = new RectangleF(100, 160, 100, 20);

submitButton.Text = "Launch";

//Create a the PdfLaunchAction

PdfLaunchAction launchAction = new PdfLaunchAction(@"..\..\Data\ Document.txt", PdfFilePathType.Relative);

//Set the launchAction to the submitButton

submitButton.Actions.GotFocus = launchAction;

//Add the form field

document.Form.Fields.Add(submitButton);

//Save the document to disk.

document.Save("output.pdf");

//close the document

document.Close();





{% endhighlight %}



{% highlight vb.net tabtile="VB.NET" %}

'Create a new PDF document.

Dim document As New PdfDocument()

'Create a new page

Dim page As PdfPage = document.Pages.Add()

'Create a new PdfButtonField

Dim submitButton As New PdfButtonField(page, "submitButton")

submitButton.Bounds = New RectangleF(25, 160, 100, 20)

submitButton.Text = "Launch"

'Create a the PdfLaunchAction

Dim launchAction As New PdfLaunchAction("..\..\Data\Document.txt", PdfFilePathType.Relative)

'Set the launch Action to the submitButton

submitButton.Actions.GotFocus = launchAction

'Add the form field

document.Form.Fields.Add(submitButton)

'Save the document to disk.

document.Save("output.pdf")

'close the document

document.Close()





{% endhighlight %}

{% highlight c# tabtile="UWP" %}

//PDF supports external document navigation only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

{% endhighlight %}

{% highlight ASP.NET Core %}

//PDF supports external document navigation only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}

//PDF supports external document navigation only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

{% endhighlight %}

{% endtabs %}  
