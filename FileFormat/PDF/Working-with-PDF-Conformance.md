---
layout: Post
title: Working with PDF conformance
description: You can create a PDF conformance documents; PDF/A-1b; PDF/x-1a;
platform: FileFormat
control: PDF
documentation: UG
---
# Working with PDF Conformance

**Essential** **PDF** Currently supports following PDF conformances.

* PDF/A-1b conformance
* PDF/X-1a conformance

**Note****:** 

1. To know more details about PDF/A standard refer the below link.

[https://en.wikipedia.org/wiki/PDF/A#Description](https://en.wikipedia.org/wiki/PDF/A#Description "")

2. To know more details about PDF/X standard refer the below link.

[https://en.wikipedia.org/wiki/PDF/X](https://en.wikipedia.org/wiki/PDF/X# "")

3. Conformances can be added only to documents created from scratch. Currently, Essential PDF do not support converting normal PDF documents to PDF/A-1b or PDF/X-1a conformance documents.
## Adding support for PDF/A-1b conformance.


You can create a PDF/A-1b document by specifying the conformance level PdfConformanceLevel.Pdf_A1B when creating the new PDF document, as shown below.

{% highlight c# %}
[C#]

//Create a new document with PDF/A-1b standard.

PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A1B);

//Add a page.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Create a solid brush.

PdfBrush brush = new PdfSolidBrush(Color.Black);

Font font = new Font("Arial", 20f, FontStyle.Regular);

//Set the font.

PdfFont pdfFont = new PdfTrueTypeFont(font, FontStyle.Regular, 12, false, true);

//Draw the text.

graphics.DrawString("Hello world!", pdfFont, brush, new PointF(20, 20));

//Save and close the document

document.Save("Output.pdf");

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Create a new document with PDF/A-1b standard.

Dim document As New PdfDocument(PdfConformanceLevel.Pdf_A1B)

'Add a page.

Dim page As PdfPage = document.Pages.Add()

'Create PDF graphics for the page.

Dim graphics As PdfGraphics = page.Graphics

'Create a solid brush.

Dim brush As PdfBrush = New PdfSolidBrush(Color.Black)

Dim font As New Font("Arial", 20.0F, FontStyle.Regular)

'Set the font.

Dim pdfFont As PdfFont = New PdfTrueTypeFont(font, FontStyle.Regular, 12, False, True)

'Draw the text.

graphics.DrawString("Hello world!", pdfFont, brush, New PointF(20, 20))

'Save and close the document

document.Save("Output.pdf")

document.Close(True)



{% endhighlight %}

## Adding support for PDF/X-1a conformance.

You can create a PDF/X-1a document by specifying the conformance level PdfConformanceLevel.Pdf_X1A2001 when creating the new PDF document, as shown below.

{% highlight c# %}
[C#]

//Create a new document with PDF/x standard.

PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_X1A2001);

//Add a page.

PdfPage page = document.Pages.Add();

document.ColorSpace = PdfColorSpace.CMYK;

//Create Pdf graphics for the page.

PdfGraphics graphics = page.Graphics;

//Create a solid brush.

PdfBrush brush = new PdfSolidBrush(Color.Black);

Font font = new Font("Arial",20f, FontStyle.Regular);

//Set the font.

PdfFont pdfFont = new PdfTrueTypeFont(font, FontStyle.Regular, 12, false, true);

//Draw the text.

graphics.DrawString("Hello world!", pdfFont, brush, new PointF(20, 20));

//Save and close the document

document.Save("Output.pdf");

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Create a new document with PDF/x standard.

Dim document As New PdfDocument(PdfConformanceLevel.Pdf_X1A2001)

'Add a page.

Dim page As PdfPage = document.Pages.Add()

'set colorspace

document.ColorSpace = PdfColorSpace.CMYK

'Create Pdf graphics for the page.

Dim graphics As PdfGraphics = page.Graphics

'Create a solid brush.

Dim brush As PdfBrush = New PdfSolidBrush(Color.Black)

Dim font As New Font("Arial", 20.0F, FontStyle.Regular)

'Set the font.

Dim pdfFont As PdfFont = New PdfTrueTypeFont(font, FontStyle.Regular, 12, False, True)

'Draw the text.

graphics.DrawString("Hello world!", font, brush, New PointF(20, 20))

'Save and close the document

document.Save("Output.pdf")

document.Close(True)



{% endhighlight %}

