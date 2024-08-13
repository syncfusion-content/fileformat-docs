---
title: Working with Brushes | Syncfusion
description: This section explains how to add shapes using different brushes such as solid brush, gradient brush, tiling brush, and more in Syncfusion .NET PDF Library.
platform: file-formats
control: PDF
documentation: UG
---
# Working with Brushes

Brushes are used to draw the content on PDF document with specific color and style. Various brushes available in Syncfusion Essential PDF are,

1. Solid Brush
2. Gradient Brush
	* Linear Gradient Brush
	* Radial Gradient Brush
3. Tiling Brush

## Solid Brush

The solid brush is used to fill an object with solid color. Essential PDF supports drawing shapes on PDF document with solid brush using the [PdfSolidBrush](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfSolidBrush.html) class. The following code snippet illustrates this.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Create a new PDF document
PdfDocument doc = new PdfDocument();
//Add a page to the document
PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;
//Create new PDF solid brush
PdfSolidBrush brush = new PdfSolidBrush(Color.Red);
//Draw ellipse on the page
graphics.DrawEllipse(brush, new RectangleF(0, 0, 200, 100));

//Save the PDF document to stream
MemoryStream stream = new MemoryStream();
doc.Save(stream);
//Close the Pdf Document
doc.Close(true);
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Create a new PDF document
PdfDocument doc = new PdfDocument();
//Add a page to the document
PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;
//Create new PDF solid brush
PdfSolidBrush brush = new PdfSolidBrush(Color.Red);
//Draw ellipse on the page
graphics.DrawEllipse(brush, new RectangleF(0, 0, 200, 100));

//Save the PDF document
doc.Save("SolidBrush.pdf");
//Close the instance of PdfDocument
doc.Close(true);
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Create a new PDF document
Dim doc As PdfDocument = New PdfDocument
'Add a page to the document
Dim page As PdfPage = doc.Pages.Add

'Create PDF graphics for the page
Dim graphics As PdfGraphics = page.Graphics
'Create new PDF solid brush
Dim brush As PdfSolidBrush = New PdfSolidBrush(Color.Red)
'Draw ellipse on the page
graphics.DrawEllipse(brush, New RectangleF(0, 0, 200, 100))

'Save the PDF document
doc.Save("SolidBrush.pdf")
'Close the instance of PdfDocument
doc.Close(True)
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Brushes/Fill-an-object-with-solid-brush-in-a-PDF/). 

## Linear gradient brush

The gradient brush is used to fill an object with blend of two or more colors. Essential PDF supports drawing shapes on PDF document with linear gradient brush using [PdfLinearGradientBrush](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfLinearGradientBrush.html) class. The following code snippet illustrates this.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Create a new PDF document
PdfDocument doc = new PdfDocument();
//Add a page to the document
PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;
//Create new PDF linear gradient brush
PdfLinearGradientBrush brush = new PdfLinearGradientBrush(new PointF(0, 0), new PointF(200, 100), Color.Red, Color.Blue);
//Draw ellipse on the page
graphics.DrawEllipse(brush, new RectangleF(0, 0, 200, 100));

//Save the PDF document to stream
MemoryStream stream = new MemoryStream();
doc.Save(stream);
//Close the Pdf Document
doc.Close(true);
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Create a new PDF document
PdfDocument doc = new PdfDocument();
//Add a page to the document
PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;
//Create new PDF linear gradient brush
PdfLinearGradientBrush brush = new PdfLinearGradientBrush(new PointF(0, 0), new PointF(200, 100), Color.Red, Color.Blue);    
//Draw ellipse on the page
graphics.DrawEllipse(brush, new RectangleF(0, 0, 200, 100));

//Save the PDF document
doc.Save("LinearGradientBrush.pdf");
//Close the instance of PdfDocument
doc.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Create a new PDF document
Dim doc As PdfDocument = New PdfDocument
'Add a page to the document
Dim page As PdfPage = doc.Pages.Add

'Create PDF graphics for the page
Dim graphics As PdfGraphics = page.Graphics
'Create new PDF linear gradient brush
Dim brush As PdfLinearGradientBrush = New PdfLinearGradientBrush(New PointF(0, 0), New PointF(200, 100), Color.Red, Color.Blue)
'Draw ellipse on the page
graphics.DrawEllipse(brush, New RectangleF(0, 0, 200, 100))

'Save the PDF document
doc.Save("LinearGradientBrush.pdf")
'Close the instance of PdfDocument
doc.Close(True)
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Brushes/Fill-an-object-with-gradient-brush-in-a-PDF/). 

## Radial Gradient Brush

The gradient brush is used to fill an object with blend of two or more colors. You can draw any shape on PDF document with radial gradient brush using [PdfRadialGradientBrush](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfRadialGradientBrush.html) class. The following code snippet explains this.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Create a new PDF document
PdfDocument doc = new PdfDocument();
//Add a page to the document
PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;
//Create new PDF radial gradient brush
PdfRadialGradientBrush brush = new PdfRadialGradientBrush(new PointF(50, 50), 0, new PointF(50, 50), 50, Color.Red, Color.Blue);
//Draw ellipse on the page
graphics.DrawEllipse(brush, new RectangleF(0, 0, 100, 100));

//Save the PDF document stream
MemoryStream stream = new MemoryStream();
doc.Save(stream);
//Close the Pdf Document
doc.Close(true);
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Create a new PDF document
PdfDocument doc = new PdfDocument();
//Add a page to the document
PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;
//Create new PDF radial gradient brush
PdfRadialGradientBrush brush = new PdfRadialGradientBrush(new PointF(50, 50), 0, new PointF(50, 50), 50, Color.Red, Color.Blue);      
//Draw ellipse on the page
graphics.DrawEllipse(brush, new RectangleF(0, 0, 100, 100));

//Save the PDF document
doc.Save("RadialGradientBrush.pdf");
//Close the instance of PdfDocument
doc.Close(true);
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Create a new PDF document
Dim doc As PdfDocument = New PdfDocument
'Add a page to the document
Dim page As PdfPage = doc.Pages.Add

'Create PDF graphics for the page
Dim graphics As PdfGraphics = page.Graphics
'Create new PDF radial gradient brush
Dim brush As PdfRadialGradientBrush = New PdfRadialGradientBrush(New PointF(50, 50), 0, New PointF(50, 50), 50, Color.Red, Color.Blue)
'Draw ellipse on the page
graphics.DrawEllipse(brush, New RectangleF(0, 0, 100, 100))

'Save the PDF document
doc.Save("RadialGradientBrush.pdf")
'Close the instance of PdfDocument
doc.Close(True)
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Brushes/Draw-shapes-on-PDF-with-radial-gradient-brush/). 

## Tiling Brush

The tiling brush is used to draw an object repeatedly. You can draw any shape on PDF page with tiling brush using [PdfTilingBrush](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfTilingBrush.html) class. The following code snippet explains this.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Create a new PDF document
PdfDocument doc = new PdfDocument();
//Add a page to the document
PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;
//Create new PDF tiling brush
PdfTilingBrush brush = new PdfTilingBrush(new RectangleF(0, 0, 11, 11));
//Draw ellipse inside the tile
brush.Graphics.DrawEllipse(PdfPens.Red, new RectangleF(0, 0, 10, 10));
//Draw ellipse
graphics.DrawEllipse(brush, new RectangleF(0, 0, 200, 100));

//Save the PDF document to stream
MemoryStream stream = new MemoryStream();
doc.Save(stream);
//Close the Pdf Document
doc.Close(true);
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Create a new PDF document
PdfDocument doc = new PdfDocument();
//Add a page to the document
PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;
//Create new PDF tiling brush
PdfTilingBrush brush = new PdfTilingBrush(new RectangleF(0, 0, 11, 11));
//Draw ellipse inside the tile
brush.Graphics.DrawEllipse(PdfPens.Red, new RectangleF(0, 0, 10, 10));
//Draw ellipse
graphics.DrawEllipse(brush, new RectangleF(0, 0, 200, 100));

//Save the PDF document
doc.Save("TilingBrush.pdf");
//Close the instance of PdfDocument
doc.Close(true);
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Create a new PDF document
Dim doc As PdfDocument = New PdfDocument
'Add a page to the document
Dim page As PdfPage = doc.Pages.Add

'Create PDF graphics for the page
Dim graphics As PdfGraphics = page.Graphics
'Create new PDF tiling brush
Dim brush As PdfTilingBrush = New PdfTilingBrush(New RectangleF(0, 0, 11, 11))
'Draw ellipse inside the tile
brush.Graphics.DrawEllipse(PdfPens.Red, New RectangleF(0, 0, 10, 10))
'Draw ellipse
graphics.DrawEllipse(brush, New RectangleF(0, 0, 200, 100))

'Save the PDF document
doc.Save("TilingBrush.pdf")
'Close the instance of PdfDocument
doc.Close(True)
{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Brushes/Draw-shape-on-PDF-with-tiling-brush/). 