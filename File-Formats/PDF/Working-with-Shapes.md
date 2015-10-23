---
title: Working with Shapes
description: Support to add shapes in the PDF document; Line; curve; path; text; rectangle; pie; arc; Bezier; ellipse
platform: file-formats
control: PDF
documentation: UG
---
# Working with Shapes

Essential PDF has support for adding the below shapes.

* Line
* Curve
* Path
* Text 
* Rectangle
* Pie
* Arc
* Bezier
* Ellipse

## Adding Shapes to a PDF document

You can add shapes with different types of brushes like solid bush, gradient brush, Tiling brush, and Image brush. Essential PDF also supports various color spaces <<link for working with color spaces>> and transparency levels.

The below code snippet shows how to add a polygon with Linear gradient brush.

{% tabs %}

{% highlight c# %}

//Create a document.

PdfDocument doc = new PdfDocument();

//Add a new page.

PdfPage page = doc.Pages.Add();

//Add pen.

PdfPen pen = new PdfPen(PdfBrushes.Brown, 10f);

//Create a gradient brush

PdfLinearGradientBrush brush = new PdfLinearGradientBrush(new PointF(10, 100), new PointF(100, 200), new PdfColor(Color.Red), new PdfColor(Color.Green));

//Create polygon points

PointF p1 = new PointF(10, 100);

PointF p2 = new PointF(10, 200);

PointF p3 = new PointF(100, 100);

PointF p4 = new PointF(100, 200);

PointF p5 = new PointF(55, 150);

PointF[] points = { p1, p2, p3, p4, p5 };

// Draw Polygon.

page.Graphics.DrawPolygon(pen, brush, points);

//Save and close the document.

doc.Save("Shapes.pdf");

doc.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Add a new page.

Dim page As PdfPage = doc.Pages.Add()

'Add pen.

Dim pen As New PdfPen(PdfBrushes.Brown, 10.0F)

'Create a gradient brush

Dim brush As New PdfLinearGradientBrush(New PointF(10, 100), New PointF(100, 200), New PdfColor(Color.Red), New PdfColor(Color.Green))

'Create polygon points

Dim p1 As New PointF(10, 100)

Dim p2 As New PointF(10, 200)

Dim p3 As New PointF(100, 100)

Dim p4 As New PointF(100, 200)

Dim p5 As New PointF(55, 150)

Dim points As PointF() = {p1, p2, p3, p4, p5}

'Draw Polygon.

page.Graphics.DrawPolygon(pen, brush, points)

'Save and close the document.

doc.Save("Shapes.pdf")

doc.Close(True)

{% endhighlight %}

{% endtabs %}

## Working with shape pagination

You can also allow large shapes to paginate across pages using the below code snippet. 

{% tabs %}

{% highlight c# %}

//Create Document

PdfDocument doc = new PdfDocument();

//Add new page

PdfPage page = doc.Pages.Add();

//Set bounds for ellipse

RectangleF rect = new RectangleF(0, 0, 100, 1000);

//Create ellipse

PdfEllipse ellipse = new PdfEllipse(rect);

//Set layout property to make the ellipse break across the pages.

PdfLayoutFormat format = new PdfLayoutFormat();

format.Break = PdfLayoutBreakType.FitPage;

format.Layout = PdfLayoutType.Paginate;

ellipse.Brush = PdfBrushes.Brown;

//Draw ellipse.

ellipse.Draw(page, 20, 20, format);

//Save and close the PDF

doc.Save("Shapes.pdf");

doc.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create Document

Dim doc As New PdfDocument()

'Add new page

Dim page As PdfPage = doc.Pages.Add()

'Set bounds for ellipse

Dim rect As New RectangleF(0, 0, 100, 1000)

'Create ellipse

Dim ellipse As New PdfEllipse(rect)

'Set layout property to make the ellipse break across the pages.

Dim format As New PdfLayoutFormat()

format.Break = PdfLayoutBreakType.FitPage

format.Layout = PdfLayoutType.Paginate

ellipse.Brush = PdfBrushes.Brown

'Draw ellipse.

ellipse.Draw(page, 20, 20, format)

'Save and close the PDF

doc.Save("Shapes.pdf")

doc.Close(True)

{% endhighlight %}

{% endtabs %}

