---
title: Syncfusion PDF control for Windows Forms
description: Loading and saving the PDF document in Windows Forms platform
platform: file-formats
control: PDF
documentation: UG
--- 

#Working with Windows Forms

In your Windows Forms application, add the required assemblies to use Essential PDF. [Refer here for assemblies required](/File-Formats/PDF/Assemblies-Required).

##Loading the document

The following code snippet illustrates how to load the PDF document in Windows Forms.

{% tabs %}

{% highlight c# %}

//Load the PDF document

PdfLoadedDocument loadedDocument = new PdfLoadedDocument("input.pdf");

//Get first page from document

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create PDF graphics for the page

PdfGraphics graphics = loadedPage.Graphics;

//Set the standard font

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

//Save the document

loadedDocument.Save("Output.pdf");

//Close the document

loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Load the PDF document

Dim loadedDocument As New PdfLoadedDocument("input.pdf")

'Get first page from document

Dim loadedPage As PdfLoadedPage = TryCast(loadedDocument.Pages(0), PdfLoadedPage)

'Create PDF graphics for the page

Dim graphics As PdfGraphics = loadedPage.Graphics

'Set the standard font

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 20)

'Draw the text

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, New PointF(0, 0))

'Save the document

loadedDocument.Save("Output.pdf")

'Close the document

loadedDocument.Close(True)

{% endhighlight %}

{% endtabs %}

## Saving the document

The following code example illustrates how to save the PDF document in Windows Forms.  

{% tabs %}

{% highlight c# %}

//Create a new PDF document

PdfDocument document = new PdfDocument();

//Set the page size

document.PageSettings.Size = PdfPageSize.A4;

//Add a page to the document

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page

PdfGraphics graphics = page.Graphics;

//Set the font

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

//Save the document

document.Save("Output.pdf");

//Close the document

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document

Dim document As New PdfDocument()

'Set the page size

document.PageSettings.Size = PdfPageSize.A4

'Add a page to the document

Dim page As PdfPage = document.Pages.Add()

'Create PDF graphics for the page

Dim graphics As PdfGraphics = page.Graphics

'Set the font

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 20)

'Draw the text

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, New PointF(0, 0))

'Save the document

document.Save("Output.pdf")

'Close the document

document.Close(True)

{% endhighlight %}

{% endtabs %}
