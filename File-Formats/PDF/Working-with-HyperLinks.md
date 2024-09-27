---
title: Working with Hyperlinks | Syncfusion
description: This section explains how to add hyperlink in a new and existing PDF document using Syncfusion .NET PDF library 
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

{% highlight c# tabtitle="C# [Cross-platform]" %}	

//Create a new PDF document.
PdfDocument document = new PdfDocument();
//Add a page to the document.
PdfPage page = document.Pages.Add();
//Create the font.
PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 12f);

//Create the Text Web Link.
PdfTextWebLink textLink = new PdfTextWebLink();
//Set the hyperlink.
textLink.Url = "http://www.syncfusion.com";
//Set the link text.
textLink.Text = "Syncfusion .NET components and controls";
//Set the font.
textLink.Font = font;
//Draw the hyperlink in PDF page.
textLink.DrawTextWebLink(page, new PointF(10, 40));

//Save the document into stream.
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Close the document.
document.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();
//Add a page to the document.
PdfPage page = document.Pages.Add();
//Create the font.
PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 12f);

//Create the Text Web Link.
PdfTextWebLink textLink = new PdfTextWebLink();
//Set the hyperlink.
textLink.Url = "http://www.syncfusion.com";
//Set the link text.
textLink.Text = "Syncfusion .NET components and controls";
//Set the font.
textLink.Font = font;
//Draw the hyperlink in PDF page.
textLink.DrawTextWebLink(page, new PointF(10, 40));

//Save the document.
document.Save("Output.pdf");
//Close the document.
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Create a new PDF document.
Dim document As New PdfDocument()
'Add a page to the document.
Dim page As PdfPage = document.Pages.Add()
'Create the font.
Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 12.0F)

'Create the Text Web Link.
Dim textLink As New PdfTextWebLink()
'Add the hyperlink.
textLink.Url = "http://www.syncfusion.com"
'Set the link text.
textLink.Text = "Syncfusion .NET components and controls"
'Set the font.
textLink.Font = font
'Draw the hyperlink in  PDF page.
textLink.DrawTextWebLink(loadedPage.Graphics, New PointF(10, 40))

'Save the document.
document.Save("Output.pdf")
'Close the document.
document.Close(True)

{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Hyperlinks/Navigate-to-specific-URL-from-a-PDF-document/). 

To add a web hyperlink to an existing document, please refer the below code snippet.

{% tabs %}  

{% highlight c# tabtitle="C# [Cross-platform]" %}	

//Load the PDF document.
FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);
//Load the page.
PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;
//Create the font.
PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 12f);

//Create the Text Web Link.
PdfTextWebLink textLink = new PdfTextWebLink();
//Set the hyperlink.
textLink.Url = "http://www.syncfusion.com";
//Set the link text.
textLink.Text = "Syncfusion .NET components and controls";
//Set the font.
textLink.Font = font;
//Draw the hyperlink in loaded page graphics.
textLink.DrawTextWebLink(loadedPage.Graphics, new PointF(10, 40));

//Save the document into stream.
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);
//Close the document.
loadedDocument.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Load the existing PDF document.
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(@"Filename.pdf");
//Load the page.
PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;
//Create the font.
PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 12f);

//Create the Text Web Link.
PdfTextWebLink textLink = new PdfTextWebLink();
//Set the hyperlink.
textLink.Url = "http://www.syncfusion.com";
//Set the link text.
textLink.Text = "Syncfusion .NET components and controls";
//Set the font.
textLink.Font = font;
//Draw the hyperlink in loaded page graphics.
textLink.DrawTextWebLink(loadedPage.Graphics, new PointF(10, 40));

//Save the document.
loadedDocument.Save("Output.pdf");
//Close the document.
loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Load the existing PDF document.
Dim loadedDocument As New PdfLoadedDocument("fileName.pdf")
'Load the page.
Dim loadedPage As PdfLoadedPage = TryCast(loadedDocument.Pages(0), PdfLoadedPage)
'Create the font.
Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 12.0F)

'Create the Text Web Link.
Dim textLink As New PdfTextWebLink()
'Add the hyperlink.
textLink.Url = "http://www.syncfusion.com"
'Set the link text.
textLink.Text = "Syncfusion .NET components and controls"
'Set the font.
textLink.Font = font
'Draw the hyperlink in loaded page graphics.
textLink.DrawTextWebLink(loadedPage.Graphics, New PointF(10, 40))

'Save the document.
loadedDocument.Save("Output1.pdf")
'Close the document.
loadedDocument.Close(True)

{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Hyperlinks/Add-a-web-hyperlink-to-an-existing-PDF-document). 

## Working with internal document navigation

To allow the users to navigate to any other part of the same document, [PdfDocumentLinkAnnotation](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfDocumentLinkAnnotation.html) class can be used. The below code explains how to add the hyperlink for internal document navigation.

{% tabs %}  

{% highlight c# tabtitle="C# [Cross-platform]" %}	

//Create a new PDF document.
PdfDocument document = new PdfDocument();
//Create a new page. 
PdfPage page = document.Pages.Add();
//Create a new rectangle.
RectangleF docLinkAnnotationBounds = new RectangleF(10, 40, 30, 30);

//Create a new document link annotation.
PdfDocumentLinkAnnotation documentLinkAnnotation = new PdfDocumentLinkAnnotation(docLinkAnnotationBounds);
//Set the annotation flags.
documentLinkAnnotation.AnnotationFlags = PdfAnnotationFlags.NoRotate;
//Set the annotation text.
documentLinkAnnotation.Text = "Document link annotation";
//Set the annotation's color.
documentLinkAnnotation.Color = new PdfColor(Color.Navy);
//Creates another page. 
PdfPage navigationPage = document.Pages.Add();
//Set the destination.
documentLinkAnnotation.Destination = new PdfDestination(navigationPage);
//Set the document link annotation location.
documentLinkAnnotation.Destination.Location = new PointF(10, 0);
//Set the document annotation zoom level.
documentLinkAnnotation.Destination.Zoom = 5;
//Add this annotation to a new page.
page.Annotations.Add(documentLinkAnnotation);

//Save the document into stream.
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Close the document.
document.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();
//Create a new page. 
PdfPage page = document.Pages.Add();
//Create a new rectangle.
RectangleF docLinkAnnotationBounds = new RectangleF(10, 40, 30, 30);

//Create a new document link annotation.
PdfDocumentLinkAnnotation documentLinkAnnotation = new PdfDocumentLinkAnnotation(docLinkAnnotationBounds);
//Set the annotation flags.
documentLinkAnnotation.AnnotationFlags = PdfAnnotationFlags.NoRotate;
//Set the annotation text.
documentLinkAnnotation.Text = "Document link annotation";
//Set the annotation's color.
documentLinkAnnotation.Color = new PdfColor(Color.Navy);
//Creates another page.
PdfPage navigationPage = document.Pages.Add();
//Set the destination.
documentLinkAnnotation.Destination = new PdfDestination(navigationPage);
//Set the document link annotation location.
documentLinkAnnotation.Destination.Location = new Point(10, 0);
//Set the document annotation zoom level.
documentLinkAnnotation.Destination.Zoom = 5;
//Add this annotation to a new page.
page.Annotations.Add(documentLinkAnnotation);

//Save the document to disk.
document.Save("DocumentLinkAnnotation.pdf");
//Close the document.
document.Close();

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Create a new PDF document.
Dim document As New PdfDocument()
'Create a new page. 
Dim page As PdfPage = document.Pages.Add()
'Create a new rectangle.
Dim docLinkAnnotationBounds As New RectangleF(10, 40, 30, 30)

'Create a new document link annotation.
Dim documentLinkAnnotation As New PdfDocumentLinkAnnotation(docLinkAnnotationBounds)
'Set the annotation flags.
documentLinkAnnotation.AnnotationFlags = PdfAnnotationFlags.NoRotate
'Set the annotation text.
documentLinkAnnotation.Text = "Document link annotation"
'Set the annotation's color.
documentLinkAnnotation.Color = New PdfColor(Color.Navy)
'Create another page.
Dim navigationPage As PdfPage = document.Pages.Add()
'Set the destination.
documentLinkAnnotation.Destination = New PdfDestination(navigationPage)
'Set the document link annotation location.
documentLinkAnnotation.Destination.Location = New Point(10, 0)
'Set the document annotation zoom level.
documentLinkAnnotation.Destination.Zoom = 5
'Add this annotation to a new page.
page.Annotations.Add(documentLinkAnnotation)

'Save the document to disk.
document.Save("DocumentLinkAnnotation.pdf")
'Close the document.
document.Close()

{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Hyperlinks/Add-the-hyperlink-for-internal-document-navigation/). 

To add a [PdfDocumentLinkAnnotation](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfDocumentLinkAnnotation.html) to an existing document, please use the below code snippet.

{% tabs %}  

{% highlight c# tabtitle="C# [Cross-platform]" %}	

//Load the PDF document.
FileStream docStream = new FileStream("fileName.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);
//Load the page.
PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;
//Create a new rectangle.
RectangleF docLinkAnnotationBounds = new RectangleF(10, 40, 30, 30);

//Create a new document link annotation.
PdfDocumentLinkAnnotation documentLinkAnnotation = new PdfDocumentLinkAnnotation(docLinkAnnotationBounds);
//Set the annotation text.
documentLinkAnnotation.Text = "Document link annotation";
//Set the existing page for navigation.
PdfLoadedPage navigationPage = loadedDocument.Pages[1] as PdfLoadedPage;
//Set the pdf destination.
documentLinkAnnotation.Destination = new PdfDestination(navigationPage);
//Set the document link annotation location.
documentLinkAnnotation.Destination.Location = new PointF(10, 0);
//Add this annotation to respective page.
loadedPage.Annotations.Add(documentLinkAnnotation);

//Save the document into stream.
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);
//Close the document.
loadedDocument.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Load the existing PDF document.
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(@"fileName.pdf");
//Load the page.
PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;
//Create a new rectangle.
RectangleF docLinkAnnotationBounds = new RectangleF(10, 40, 30, 30);

//Create a new document link annotation.
PdfDocumentLinkAnnotation documentLinkAnnotation = new PdfDocumentLinkAnnotation(docLinkAnnotationBounds);
//Set the annotation text.
documentLinkAnnotation.Text = "Document link annotation";
//Set the existing page for navigation.
PdfLoadedPage navigationPage = loadedDocument.Pages[1] as PdfLoadedPage;
//Set the pdf destination.
documentLinkAnnotation.Destination = new PdfDestination(navigationPage);
//Set the document link annotation location.
documentLinkAnnotation.Destination.Location = new Point(10, 0);
//Add this annotation to respective page.
loadedPage.Annotations.Add(documentLinkAnnotation);

//Save the document to disk.
loadedDocument.Save("DocumentLinkAnnotation.pdf");
//Close the document.
loadedDocument.Close();

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Load the existing PDF document.
Dim loadedDocument As New PdfLoadedDocument("fileName.pdf")
'Load the page.
Dim loadedPage As PdfLoadedPage = TryCast(loadedDocument.Pages(0), PdfLoadedPage)
'Create a new rectangle.
Dim docLinkAnnotationBounds As New RectangleF(10, 40, 30, 30)

'Create a new document link annotation.
Dim documentLinkAnnotation As New PdfDocumentLinkAnnotation(docLinkAnnotationBounds)
'Set the annotation text.
documentLinkAnnotation.Text = "Document link annotation"
'Set the existing page for navigation.
Dim navigationPage As PdfLoadedPage = TryCast(loadedDocument.Pages(1), PdfLoadedPage)
'Set the pdf destination.
documentLinkAnnotation.Destination = New PdfDestination(navigationPage)
'Set the document link annotation location.
documentLinkAnnotation.Destination.Location = New Point(10, 0)
'Add this annotation to respective page.
loadedPage.Annotations.Add(documentLinkAnnotation)

'Save the document to disk.
loadedDocument.Save("DocumentLinkAnnotation.pdf")
'Close the document.
loadedDocument.Close()

{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Hyperlinks/Internal-document-navigation-to-an-existing-PDF/). 

## Working with external document navigation

You can open external documents like images, text files, PDF, etc. using [PdfFileLinkAnnotation](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfFileLinkAnnotation.html) class.

Please refer the below code snippet for navigating to external documents.

{% tabs %}  

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Create the PDF document.
PdfDocument document = new PdfDocument();
//Creates a new page. 
PdfPage page = document.Pages.Add();
//Create a new rectangle.
RectangleF bounds = new RectangleF(10, 40, 30, 30);

//Create a link for image file. 
PdfFileLinkAnnotation fileLinkAnnotation = new PdfFileLinkAnnotation(bounds, filePath);
//Add this annotation to a page.
page.Annotations.Add(fileLinkAnnotation);

//Save the document into stream.
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Close the document.
document.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Create the PDF document.
PdfDocument document = new PdfDocument();
//Creates a new page. 
PdfPage page = document.Pages.Add();
//Create a new rectangle.
RectangleF bounds = new RectangleF(10, 40, 30, 30);

//Create a link for image file. 
PdfFileLinkAnnotation fileLinkAnnotation = new PdfFileLinkAnnotation(bounds, @"..\..\Data\logo.png");
//Add this annotation to a page.
page.Annotations.Add(fileLinkAnnotation);

//Save the document to disk.
document.Save("FileLinkAnnotation.pdf");
//Close the document.
document.Close();

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Create the PDF document
Dim document As New PdfDocument()
'Creates a new page and adds it as the last page of the document
Dim page As PdfPage = document.Pages.Add()
'Create a new rectangle
Dim rectangle As New RectangleF(10, 40, 30, 30)

'Create a link for image file 
Dim fileLinkAnnotation As New PdfFileLinkAnnotation(rectangle, "..\..\Data\logo.png")
'Add this annotation to a page
page.Annotations.Add(fileLinkAnnotation)

'Save the document to disk
document.Save("FileLinkAnnotation.pdf")
'Close the document
document.Close()

{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Hyperlinks/Navigate-to-external-document/). 

N> The above link makes use of the absolute path of the file for navigation. So, moving the files to another machine or location may lead to file not found error in PDF reader applications.

To open a file in relative path, the [PdfLaunchAction](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfLaunchAction.html) can be used. While using the relative path in launch action, the files can be moved to any machine, provided the relative path is being maintained. The below code snippet explains the same.

{% tabs %}  

{% highlight c# tabtitle="C# [Cross-platform]" %}

//PDF doesn't support external document navigation in C# .NET Cross platforms. 

{% endhighlight %}

{% highlight c# tabtitle="C#" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();
//Create a new page.
PdfPage page = document.Pages.Add();

//Create the button field.
PdfButtonField submitButton = new PdfButtonField(page, "submitButton");
submitButton.Bounds = new RectangleF(100, 160, 100, 20);
submitButton.Text = "Launch";
//Create a the PdfLaunchAction.
PdfLaunchAction launchAction = new PdfLaunchAction(@"Document.txt", PdfFilePathType.Relative);
//Set the launchAction to the submitButton.
submitButton.Actions.GotFocus = launchAction;
//Add the form field.
document.Form.Fields.Add(submitButton);

//Save the document to disk.
document.Save("output.pdf");
//Close the document.
document.Close();

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new PDF document
Dim document As New PdfDocument()
'Create a new page
Dim page As PdfPage = document.Pages.Add()

'Create a new PdfButtonField
Dim submitButton As New PdfButtonField(page, "submitButton")
submitButton.Bounds = New RectangleF(25, 160, 100, 20)
submitButton.Text = "Launch"
'Create a the PdfLaunchAction
Dim launchAction As New PdfLaunchAction("Document.txt", PdfFilePathType.Relative)
'Set the launch Action to the submitButton
submitButton.Actions.GotFocus = launchAction
'Add the form field
document.Form.Fields.Add(submitButton)

'Save the document to disk
document.Save("output.pdf")
'Close the document
document.Close()

{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Hyperlinks/Open-a-file-in-relative-path-using-action/). 
