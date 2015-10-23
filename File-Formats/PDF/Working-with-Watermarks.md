---
title: Working with Watermarks
description: Support to add watermark in the PDF document; text watermark; image watermark
platform: FileFormat
control: PDF
documentation: UG
---
# Working with Watermarks

Essential PDF provides you support to add watermark in the PDF document using PdfGraphics.

## Adding text watermark in PDF document



Essential PDF allows you to draw the text watermark in PDF document using graphics elements.

The below code illustrates how to draw the text watermark in new PDF document:

{% highlight c# %}
C#:

//Create a new PDF document.

PdfDocument pdfDocument = new PdfDocument();

//Add a page to the PDF document.

PdfPage pdfPage = pdfDocument.Pages.Add();

PdfGraphics graphics = pdfPage.Graphics;

//set the font

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//watermark text.

PdfGraphicsState state = graphics.Save();

graphics.SetTransparency(0.25f);

graphics.RotateTransform(-40);

graphics.DrawString("Imported using Essential PDF", font, PdfPens.Red, PdfBrushes.Red, new PointF(-150, 450));

//Save and close the document.

pdfDocument.Save("watermark.pdf");

pdfDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}
VB:

'Create a new PDF document.

Dim pdfDocument As New PdfDocument()

'Add a page to the PDF document.

Dim pdfPage As PdfPage = pdfDocument.Pages.Add()

Dim graphics As PdfGraphics = pdfPage.Graphics

'set the font

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 20)

' watermark text.

Dim state As PdfGraphicsState = graphics.Save()

graphics.SetTransparency(0.25F)

graphics.RotateTransform(-40)

graphics.DrawString("Imported using Essential PDF", font, PdfPens.Red, PdfBrushes.Red, New PointF(-150, 450))

'Save and close the document.

pdfDocument.Save("watermark.pdf")

pdfDocument.Close(True)



{% endhighlight %}

The below code illustrates how to draw the text watermark in existing PDF document:

{% highlight c# %}
C#:

//Load the document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);

PdfPageBase loadedPage = loadedDocument.Pages[0];

PdfGraphics graphics = loadedPage.Graphics;

//set the font

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

// watermark text.

PdfGraphicsState state = graphics.Save();

graphics.SetTransparency(0.25f);

graphics.RotateTransform(-40);

graphics.DrawString("Imported using Essential PDF", font, PdfPens.Red, PdfBrushes.Red, new PointF(-150, 450));

//Save and close the document.

loadedDocument.Save("watermark.pdf");

loadedDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}
VB:

'Load the document.

Dim loadedDocument As New PdfLoadedDocument(fileName)

Dim loadedPage As PdfPageBase = loadedDocument.Pages(0)

Dim graphics As PdfGraphics = loadedPage.Graphics

'set the font

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 20)

' watermark text.

Dim state As PdfGraphicsState = graphics.Save()

graphics.SetTransparency(0.25F)

graphics.RotateTransform(-40)

graphics.DrawString("Imported using Essential PDF", font, PdfPens.Red, PdfBrushes.Red, New PointF(-150, 450))

'Save and close the document.

loadedDocument.Save("watermark.pdf")

loadedDocument.Close(True)



{% endhighlight %}

## Adding image watermark in PDF document

To add the image watermark in PDF document, you can draw the image with transparency in PdfGraphics.

The below code illustrates how to draw the image watermark in new PDF document:

{% highlight c# %}
C#:

//Create a new PDF document.

PdfDocument pdfDocument = new PdfDocument();

//Add a page to the PDF document.

PdfPage pdfPage = pdfDocument.Pages.Add();

PdfGraphics graphics = pdfPage.Graphics;

//Image watermark.

PdfImage image = new PdfBitmap("Ani.gif");

PdfGraphicsState state = graphics.Save();

graphics.SetTransparency(0.25f);

graphics.DrawImage(image, new PointF(0, 0), pdfPage.Graphics.ClientSize);

//Save and close the document.

pdfDocument.Save("watermark.pdf");

pdfDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}
VB:

'Create a new PDF document.

Dim pdfDocument As New PdfDocument()

'Add a page to the PDF document.

Dim pdfPage As PdfPage = pdfDocument.Pages.Add()

Dim graphics As PdfGraphics = pdfPage.Graphics

'Image watermark.

Dim image As PdfImage = New PdfBitmap("Ani.gif")

Dim state As PdfGraphicsState = graphics.Save()

graphics.SetTransparency(0.25F)

graphics.DrawImage(image, New PointF(0, 0), pdfPage.Graphics.ClientSize)

'Save and close the document.

pdfDocument.Save("watermark.pdf")

pdfDocument.Close(True)



{% endhighlight %}

The below code illustrates how to draw the image watermark in existing PDF document.

{% highlight c# %}
C#:

//Load the document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);

PdfPageBase loadedPage = loadedDocument.Pages[0];

PdfGraphics graphics = loadedPage.Graphics;

//Image watermark.

PdfImage image = new PdfBitmap("Ani.gif");

PdfGraphicsState state = graphics.Save();

graphics.SetTransparency(0.25f);

graphics.DrawImage(image, new PointF(0, 0), loadedPage.Graphics.ClientSize);

//Save and close the document.

loadedDocument.Save("watermark.pdf");

loadedDocument.Close(true);





{% endhighlight %}

{% highlight vb.net %}
VB:

'Load the document.

Dim loadedDocument As New PdfLoadedDocument(fileName)

Dim loadedPage As PdfPageBase = loadedDocument.Pages(0)

Dim graphics As PdfGraphics = loadedPage.Graphics

'Image watermark.

Dim image As PdfImage = New PdfBitmap("Ani.gif")

Dim state As PdfGraphicsState = graphics.Save()

graphics.SetTransparency(0.25F)

graphics.DrawImage(image, New PointF(0, 0), loadedPage.Graphics.ClientSize)

'Save and close the document.

loadedDocument.Save("watermark.pdf")

loadedDocument.Close(True)



{% endhighlight %}

