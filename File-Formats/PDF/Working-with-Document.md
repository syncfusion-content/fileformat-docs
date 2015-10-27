---
title: Working with Document
description: This section explains how to set document Setting and properties to the PDF document using Essential PDF
platform: File Format
control: PDF
documentation: UG
---
# Working with Document

## Adding the document settings

Essential PDF supports various page setting options to control the page display. 

You can choose the standard or custom page size when you add a page to the PDF document. This sample below illustrates how to create a PDF document with standard page size.

{% tabs %}

{% highlight c# %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

// Set the page size.

document.PageSettings.Size = PdfPageSize.A4;

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

//Save the document.

document.Save("Output.pdf");

//Close the document.

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim document As New PdfDocument()

'Set the page size.

document.PageSettings.Size = PdfPageSize.A4

'Add a page to the document.

Dim page As PdfPage = document.Pages.Add()

'Create PDF graphics for the page.

Dim graphics As PdfGraphics = page.Graphics

'Set the font.

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 20)

'Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, New PointF(0, 0))

'Save the document.

document.Save("Output.pdf")

'Close the document.

document.Close(True)

{% endhighlight %}

{% endtabs %}

You can create a custom page size in the PDF document by using following code snippet.

{% tabs %}

{% highlight c# %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

// Set the custom page size.

document.PageSettings.Size = new SizeF(200,300);

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

//Save the document.

document.Save("Output.pdf");

//Close the document.

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim document As New PdfDocument()

‘Set the custom page size.

document.PageSettings.Size = New SizeF(200, 300)

'Add a page to the document.

Dim page As PdfPage = document.Pages.Add()

'Create PDF graphics for the page.

Dim graphics As PdfGraphics = page.Graphics

'Set the font.

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 20)

'Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, New PointF(0, 0))

'Save the document.

document.Save("Output.pdf")

'Close the document.

document.Close(True)

{% endhighlight %}

{% endtabs %}

You can change page orientation from portrait to landscape by using the following code snippet.

{% tabs %}

{% highlight c# %}


//Create a new PDF document.

PdfDocument document = new PdfDocument();

// Set the page size.

document.PageSettings.Size = PdfPageSize.A4;

//Change the page orientation to landscape

document.PageSettings.Orientation = PdfPageOrientation.Landscape;

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

//Save the document.

document.Save("Output.pdf");

//Close the document.

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim document As New PdfDocument()

' Set the page size.

document.PageSettings.Size = PdfPageSize.A4

'Change the page orientation to landscape

document.PageSettings.Orientation = PdfPageOrientation.Landscape

'Add a page to the document.

Dim page As PdfPage = document.Pages.Add()

'Create PDF graphics for the page.

Dim graphics As PdfGraphics = page.Graphics

'Set the font.

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 20)

'Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, New PointF(0, 0))

'Save the document.

document.Save("Output.pdf")

'Close the document.

document.Close(True)

{% endhighlight %}

{% endtabs %}

You can also change orientation by setting the rotation angle using PdfPageRotateAngle Enum. The following code snippets illustrates the same.

{% tabs %}

{% highlight c# %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

// Set the page size.

document.PageSettings.Size = PdfPageSize.A4;

//Change the page orientation to 90°

document.PageSettings.Rotate = PdfPageRotateAngle.RotateAngle90;

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

//Save the document.

document.Save("Output.pdf");

//Close the document.

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim document As New PdfDocument()

‘Set the page size.

document.PageSettings.Size = PdfPageSize.A4

'Change the page orientation to 90°

document.PageSettings.Rotate = PdfPageRotateAngle.RotateAngle90

'Add a page to the document.

Dim page As PdfPage = document.Pages.Add()

'Create PDF graphics for the page.

Dim graphics As PdfGraphics = page.Graphics

'Set the font.

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 20)

'Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, New PointF(0, 0))

'Save the document.

document.Save("Output.pdf")

'Close the document.

document.Close(True)

{% endhighlight %}

{% endtabs %}

## Creating sections in a PDF

PDF sections are parts of the PDF document, which may contain one or more pages with their unique page settings. The following code snippet illustrates the same.

{% tabs %}

{% highlight c# %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a section to PDF document.

PdfSection section = document.Sections.Add();

//Add pages to the section

PdfPage page = section.Pages.Add();

//Create PDF graphics for the page

PdfGraphics graphics = page.Graphics;

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

//Save the document.

document.Save("Output.pdf");

//Close the document.

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim document As New PdfDocument()

'Add a section to PDF document.

Dim section As PdfSection = document.Sections.Add()

'Add pages to the section

Dim page As PdfPage = section.Pages.Add()

'Create PDF graphics for the page

Dim graphics As PdfGraphics = page.Graphics

'Set the font.

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 20)

'Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, New PointF(0, 0))

'Save the document.

document.Save("Output.pdf")

'Close the document.

document.Close(True)

{% endhighlight %}

{% endtabs %}

## Printing PDF document

To print a PDF document, the following assemblies has to be added as reference to the project.

1. Syncfusion.Compression.Base.dll
2. Syncfusion.Pdf.Base.dll
3. Syncfusion.PdfViewer.Windows.dll 

The following code snippet illustrates how to print a PDF document.

{% tabs %}

{% highlight c# %}

PdfDocumentView viewer = new PdfDocumentView();

//Load the PDF document

viewer.Load("Input.pdf");

//Initialize print dialog.

PrintDialog dialog = new PrintDialog();

dialog.AllowPrintToFile = true;

dialog.AllowSomePages = true;

dialog.AllowCurrentPage = true;

dialog.Document = viewer.PrintDocument;

//Print the PDF document

dialog.Document.Print();

//Dispose the viewer

viewer.Dispose();

{% endhighlight %}

{% highlight vb.net %}

Dim viewer As New PdfDocumentView()

'Load the PDF document

viewer.Load("Input.pdf")

'Initialize print dialog.

Dim dialog As New PrintDialog()

dialog.AllowPrintToFile = True

dialog.AllowSomePages = True

dialog.AllowCurrentPage = True

dialog.Document = viewer.PrintDocument

'Print the PDF document

dialog.Document.Print()

'Dispose the viewer

viewer.Dispose()

{% endhighlight %}

{% endtabs %}

## Working with document properties

Essential PDF allows you to set, read and modify the document information of a PDF like Author, CreationDate, Subject, Title, and Producer etc. The **DocumentInformation** **property** of the PdfDocument or PdfLoadedDocument provides access to this information.

The following code snippet illustrates how to set PDF document information.

{% tabs %}

{% highlight c# %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Set document information.

document.DocumentInformation.Author = "Syncfusion";

document.DocumentInformation.CreationDate = DateTime.Now;

document.DocumentInformation.Creator = "Essential PDF";

document.DocumentInformation.Keywords = "PDF";

document.DocumentInformation.Subject = "Document information DEMO";

document.DocumentInformation.Title = "Essential PDF Sample";

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

//Save the document.

document.Save("Output.pdf");

//Close the document.

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim document As New PdfDocument()

'Set document information.

document.DocumentInformation.Author = "Syncfusion"

document.DocumentInformation.CreationDate = DateTime.Now

document.DocumentInformation.Creator = "Essential PDF"

document.DocumentInformation.Keywords = "PDF"

document.DocumentInformation.Subject = "Document information DEMO"

document.DocumentInformation.Title = "Essential PDF Sample"

'Add a page to the document.

Dim page As PdfPage = document.Pages.Add()

'Create PDF graphics for the page.

Dim graphics As PdfGraphics = page.Graphics

'Set the font.

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 20)

'Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, New PointF(0, 0))

'Save the document.

document.Save("Output.pdf")

'Close the document.

document.Close(True)

{% endhighlight %}

{% endtabs %}

The following code snippet shows how to read and modify the document properities of an existing PDF document.

{% tabs %}

{% highlight c# %}

//Create a new PDF document.

PdfLoadedDocument document = new PdfLoadedDocument("Input.pdf");

//Modify document information.

document.DocumentInformation.Author = "Syncfusion";

document.DocumentInformation.CreationDate = DateTime.Now;

document.DocumentInformation.Creator = "Essential PDF";

document.DocumentInformation.Keywords = "PDF";

document.DocumentInformation.Subject = "Document information DEMO";

document.DocumentInformation.Title = "Essential PDF Sample";

//Save the document.
document.Save("Output.pdf");

//Close the document.
document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim document As New PdfLoadedDocument("Input.pdf")

'Modify document information.

document.DocumentInformation.Author = "Syncfusion"

document.DocumentInformation.CreationDate = DateTime.Now

document.DocumentInformation.Creator = "Essential PDF"

document.DocumentInformation.Keywords = "PDF"

document.DocumentInformation.Subject = "Document information DEMO"

document.DocumentInformation.Title = "Essential PDF Sample"

'Save the document.

document.Save("Output.pdf")

'Close the document.

document.Close(True)

{% endhighlight %}

{% endtabs %}

## Choosing the viewer preferences

Essential PDF allows you to set various PDF viewer preferences to be used when the generated PDF document is displayed in a PDF reader application.

You can hide the menubar and toolbar by using the following code snippet.

{% tabs %}

{% highlight c# %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

//Hide viewer application's menu bar.

document.ViewerPreferences.HideMenubar = true;

//Hide viewer application's toolbar.

document.ViewerPreferences.HideToolbar = true;

//Shows user interface elements in the document's window (such as scroll bars and navigation controls).

document.ViewerPreferences.HideWindowUI = false;

//Save the document.

document.Save("Output.pdf");

//Close the document.

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim document As New PdfDocument()

'Add a page to the document.

Dim page As PdfPage = document.Pages.Add()

'Create PDF graphics for the page.

Dim graphics As PdfGraphics = page.Graphics

'Set the font.

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 20)

'Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, New PointF(0, 0))

'Hides viewer application's menu bar.

document.ViewerPreferences.HideMenubar = True

'Hides viewer application's toolbar.

document.ViewerPreferences.HideToolbar = True

'Shows user interface elements in the document's window (such as scroll bars and navigation controls).

document.ViewerPreferences.HideWindowUI = False

'Save the document.

document.Save("Output.pdf")

'Close the document.

document.Close(True)

{% endhighlight %}

{% endtabs %}

You can also allow the reader application to initially display the bookmarks, thumbnails or attachments using  PdfPageMode ENUM

{% tabs %}

{% highlight c# %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

//Show the attachments panel.

document.ViewerPreferences.PageMode = PdfPageMode.UseAttachments;

//Save the document.

document.Save("Output.pdf");

//Close the document.

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim document As New PdfDocument()

'Add a page to the document.

Dim page As PdfPage = document.Pages.Add()

'Create PDF graphics for the page.

Dim graphics As PdfGraphics = page.Graphics

'Set the font.

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 20)

'Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, New PointF(0, 0))

'Show the attachments panel.

document.ViewerPreferences.PageMode = PdfPageMode.UseAttachments

'Save the document.

document.Save("Output.pdf")

'Close the document.

document.Close(True)

{% endhighlight %}

{% endtabs %}

## Adding document action

Please refer to the actions section for more document level operations using the PdfJavascript and PDF actions.
[Action](/file-formats/pdf/working-with-action "Working with action")