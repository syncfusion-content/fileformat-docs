---
title: Working with Redaction |Syncfusion
description: This section explains how to Redact PDF document by using Essential PDF
platform: file-formats
control: PDF
documentation: UG
---
# Working with PDF Redaction

## Removing sensitive content from the PDF document

Essential PDF supports removing or redacting the sensitive text and images from the PDF documents. Redaction is the process of permanently removing sensitive information from the PDF document, use the [PdfRedaction](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Redaction.PdfRedaction.html) class to remove content.

N> Note: CJK text without TrueType font and complex script text cannot be redacted.

The following sample code snippet demonstrates the redaction of PDF documents from the specified bounds.

{% tabs %}
{% highlight c# %}

//Load a PDF document

PdfLoadedDocument document = new PdfLoadedDocument("Input.pdf");

// Get first page from the document

PdfLoadedPage page = document.Pages[0] as PdfLoadedPage;

//Create PDF redaction for the page

PdfRedaction redaction = new PdfRedaction(new RectangleF(343, 147, 60, 17), System.Drawing.Color.Black);

//Adds redaction to the loaded page

page.Redactions.Add(redaction);

//Save and close the PDF document

document.Save("Output.pdf");

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Load a PDF document

Dim document As PdfLoadedDocument = New PdfLoadedDocument("Input.pdf")

'Get first page from the document

Dim page As PdfLoadedPage = TryCast(document.Pages(0), PdfLoadedPage)

'Create PDF redaction for the page

Dim redaction As PdfRedaction = New PdfRedaction(New RectangleF(343, 147, 60, 17), System.Drawing.Color.Black)

'Adds redaction to the loaded page

page.Redactions.Add(redaction)

'Save and close the PDF document

document.Save("Output.pdf")

document.Close(True)

{% endhighlight %}

{% highlight UWP %}

//PDF supports redaction only in Windows Forms, WPF, ASP.NET, ASP.NET MVC.

{% endhighlight %}

{% highlight ASP.NET Core %}

//PDF supports redaction only in Windows Forms, WPF, ASP.NET, ASP.NET MVC.

{% endhighlight %}

{% highlight Xamarin %}

//PDF supports redaction only in Windows Forms, WPF, ASP.NET, ASP.NET MVC.

{% endhighlight %}
{% endtabs %}

## Display text on the redacted area

You can draw overlay text on the redacted area using the [Appearance](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Redaction.PdfRedaction.html#Syncfusion_Pdf_Redaction_PdfRedaction_Appearance) property available in [PdfRedaction](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Redaction.PdfRedaction.html) class, and customize the overlay text with different font, style, color and brushes.

The following code snippet explains how to add overlay text in the redacted area.

{% tabs %}
{% highlight c# %}

//Load a PDF document

PdfLoadedDocument document = new PdfLoadedDocument("Input.pdf");

//Get first page from the document

PdfLoadedPage page = document.Pages[0] as PdfLoadedPage;

//Create PDF redaction for the page

PdfRedaction redaction = new PdfRedaction(new RectangleF(343, 147, 60, 17));

//Font for the overlay text

PdfStandardFont font = new PdfStandardFont(PdfFontFamily.Courier, 10);

//Draw text on the redacted area

redaction.Appearance.Graphics.DrawString("Redacted", font, PdfBrushes.Red, new PointF(5, 5));

//Adds redaction to the loaded page

page.Redactions.Add(redaction);

//Save and close the PDF document

document.Save("Output.pdf");

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Load a PDF document

Dim document As PdfLoadedDocument = New PdfLoadedDocument("Input.pdf")

'Get first page from the document

Dim page As PdfLoadedPage = TryCast(document.Pages(0), PdfLoadedPage)

'Create PDF redaction for the page

Dim redaction As PdfRedaction = New PdfRedaction(New RectangleF(343, 147, 60, 17))

'Font for the overlay text

Dim font As PdfStandardFont = New PdfStandardFont(PdfFontFamily.Courier, 10)

'Draw text on the redacted area

redaction.Appearance.Graphics.DrawString("Redacted", font, PdfBrushes.Red, New PointF(5, 5))

'Adds redaction to the loaded page

page.Redactions.Add(redaction)

'Save and close the PDF document

document.Save("Output.pdf")

document.Close(True)

{% endhighlight %}

{% highlight UWP %}

//PDF supports redaction only in Windows Forms, WPF, ASP.NET, ASP.NET MVC.

{% endhighlight %}

{% highlight ASP.NET Core %}

//PDF supports redaction only in Windows Forms, WPF, ASP.NET, ASP.NET MVC.

{% endhighlight %}

{% highlight Xamarin %}

//PDF supports redaction only in Windows Forms, WPF, ASP.NET, ASP.NET MVC.

{% endhighlight %}
{% endtabs %}

## Drawing image on the redacted area

You can draw the image on the redacted area using the [Appearance](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Redaction.PdfRedaction.html#Syncfusion_Pdf_Redaction_PdfRedaction_Appearance) property in [PdfRedaction](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Redaction.PdfRedaction.html) class.

The following code snippet explains how to redact the information from a page by drawing image on the redacted area using appearance.

{% tabs %}
{% highlight c# %}

//Load a PDF document

PdfLoadedDocument document = new PdfLoadedDocument("Input.pdf");

//Get first page from the document

PdfLoadedPage page = document.Pages[0] as PdfLoadedPage;

//Create PDF redaction for the page

PdfRedaction redaction = new PdfRedaction(new RectangleF(63, 57, 182, 157));

//Draw image on the redacted bounds

PdfImage image = new PdfBitmap("Image.png");

redaction.Appearance.Graphics.DrawImage(image, new RectangleF(0, 0, 182, 157));

//Adds redaction to the loaded page

page.Redactions.Add(redaction);

//Save and close the PDF document

document.Save("Output.pdf");

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Load a PDF document

Dim document As PdfLoadedDocument = New PdfLoadedDocument("Input.pdf")

'Get first page from the document

Dim page As PdfLoadedPage = TryCast(document.Pages(0), PdfLoadedPage)

'Create PDF redaction for the page

Dim redaction As PdfRedaction = New PdfRedaction(New RectangleF(63, 57, 182, 157))

'Draw image on the redacted bounds

Dim image As PdfImage = New PdfBitmap("Image.png")

redaction.Appearance.Graphics.DrawImage(image, New RectangleF(0, 0, 182, 157))

'Draw image on the redacted bounds

page.Redactions.Add(redaction)

'Save and close the PDF document

document.Save("Output.pdf")

document.Close(True)

{% endhighlight %}

{% highlight UWP %}

//PDF supports redaction only in Windows Forms, WPF, ASP.NET, ASP.NET MVC.

{% endhighlight %}

{% highlight ASP.NET Core %}

//PDF supports redaction only in Windows Forms, WPF, ASP.NET, ASP.NET MVC.

{% endhighlight %}

{% highlight Xamarin %}

//PDF supports redaction only in Windows Forms, WPF, ASP.NET, ASP.NET MVC.

{% endhighlight %}
{% endtabs %}

## Drawing pattern on the redacted area

You can draw the patterns on the redacted area using the [Appearance](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Redaction.PdfRedaction.html#Syncfusion_Pdf_Redaction_PdfRedaction_Appearance) property in [PdfRedaction](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Redaction.PdfRedaction.html) class.

The following code snippet explains how to redact the information from a page by drawing mosaic pattern on the redacted area using appearance.

{% tabs %}
{% highlight c# %}

//Load a PDF document

PdfLoadedDocument document = new PdfLoadedDocument("Input.pdf");

//Get first page from the document

PdfLoadedPage page = document.Pages[0] as PdfLoadedPage;

//Create PDF redaction for the page

PdfRedaction redaction = new PdfRedaction(new RectangleF(341, 149, 64, 14));

//Draw mosaic pattern on the redaction bounds

RectangleF rect = new RectangleF(0, 0, 8, 8);

PdfTilingBrush tillingBrush = new PdfTilingBrush(rect);

tillingBrush.Graphics.DrawRectangle(PdfBrushes.Gray, new RectangleF(0, 0, 2, 2));

tillingBrush.Graphics.DrawRectangle(PdfBrushes.White, new RectangleF(2, 0, 2, 2));

tillingBrush.Graphics.DrawRectangle(PdfBrushes.LightGray, new RectangleF(4, 0, 2, 2));

tillingBrush.Graphics.DrawRectangle(PdfBrushes.DarkGray, new RectangleF(6, 0, 2, 2));

tillingBrush.Graphics.DrawRectangle(PdfBrushes.White, new RectangleF(0, 2, 2, 2));

tillingBrush.Graphics.DrawRectangle(PdfBrushes.LightGray, new RectangleF(2, 2, 2, 2));

tillingBrush.Graphics.DrawRectangle(PdfBrushes.Black, new RectangleF(4, 2, 2, 2));

tillingBrush.Graphics.DrawRectangle(PdfBrushes.LightGray, new RectangleF(6, 2, 2, 2));

tillingBrush.Graphics.DrawRectangle(PdfBrushes.LightGray, new RectangleF(0, 4, 2, 2));

tillingBrush.Graphics.DrawRectangle(PdfBrushes.DarkGray, new RectangleF(2, 4, 2, 2));

tillingBrush.Graphics.DrawRectangle(PdfBrushes.LightGray, new RectangleF(4, 4, 2, 2));

tillingBrush.Graphics.DrawRectangle(PdfBrushes.White, new RectangleF(6, 4, 2, 2));

tillingBrush.Graphics.DrawRectangle(PdfBrushes.Black, new RectangleF(0, 6, 2, 2));

tillingBrush.Graphics.DrawRectangle(PdfBrushes.LightGray, new RectangleF(2, 6, 2, 2));

tillingBrush.Graphics.DrawRectangle(PdfBrushes.Black, new RectangleF(4, 6, 2, 2));

tillingBrush.Graphics.DrawRectangle(PdfBrushes.DarkGray, new RectangleF(6, 6, 2, 2));

rect = new RectangleF(0, 0, 16, 14);

PdfTilingBrush tillingBrushNew = new PdfTilingBrush(rect);

tillingBrushNew.Graphics.DrawRectangle(tillingBrush, rect);

redaction.Appearance.Graphics.DrawRectangle(tillingBrushNew, new RectangleF(0, 0, 64, 14));

//Adds redaction to the loaded page

page.Redactions.Add(redaction);

//Save and close the PDF document

document.Save("Output.pdf");

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Load a PDF document

Dim document As PdfLoadedDocument = New PdfLoadedDocument("Input.pdf")

'Get first page from the document

Dim page As PdfLoadedPage = TryCast(document.Pages(0), PdfLoadedPage)

'Create PDF redaction for the page

Dim redaction As PdfRedaction = New PdfRedaction(New RectangleF(341, 149, 64, 14))

'Draw mosaic pattern on the redaction bounds

Dim rect As RectangleF = New RectangleF(0, 0, 8, 8)

Dim tillingBrush As PdfTilingBrush = New PdfTilingBrush(rect)

tillingBrush.Graphics.DrawRectangle(PdfBrushes.Gray, New RectangleF(0, 0, 2, 2))

tillingBrush.Graphics.DrawRectangle(PdfBrushes.White, New RectangleF(2, 0, 2, 2))

tillingBrush.Graphics.DrawRectangle(PdfBrushes.LightGray, New RectangleF(4, 0, 2, 2))

tillingBrush.Graphics.DrawRectangle(PdfBrushes.DarkGray, New RectangleF(6, 0, 2, 2))

tillingBrush.Graphics.DrawRectangle(PdfBrushes.White, New RectangleF(0, 2, 2, 2))

tillingBrush.Graphics.DrawRectangle(PdfBrushes.LightGray, New RectangleF(2, 2, 2, 2))

tillingBrush.Graphics.DrawRectangle(PdfBrushes.Black, New RectangleF(4, 2, 2, 2))

tillingBrush.Graphics.DrawRectangle(PdfBrushes.LightGray, New RectangleF(6, 2, 2, 2))

tillingBrush.Graphics.DrawRectangle(PdfBrushes.LightGray, New RectangleF(0, 4, 2, 2))

tillingBrush.Graphics.DrawRectangle(PdfBrushes.DarkGray, New RectangleF(2, 4, 2, 2))

tillingBrush.Graphics.DrawRectangle(PdfBrushes.LightGray, New RectangleF(4, 4, 2, 2))

tillingBrush.Graphics.DrawRectangle(PdfBrushes.White, New RectangleF(6, 4, 2, 2))

tillingBrush.Graphics.DrawRectangle(PdfBrushes.Black, New RectangleF(0, 6, 2, 2))

tillingBrush.Graphics.DrawRectangle(PdfBrushes.LightGray, New RectangleF(2, 6, 2, 2))

tillingBrush.Graphics.DrawRectangle(PdfBrushes.Black, New RectangleF(4, 6, 2, 2))

tillingBrush.Graphics.DrawRectangle(PdfBrushes.DarkGray, New RectangleF(6, 6, 2, 2))

rect = New RectangleF(0, 0, 16, 14)

Dim tillingBrushNew As PdfTilingBrush = New PdfTilingBrush(rect)

tillingBrushNew.Graphics.DrawRectangle(tillingBrush, rect)

redaction.Appearance.Graphics.DrawRectangle(tillingBrushNew, New RectangleF(0, 0, 64, 14))

'Adds redaction to the loaded page

page.Redactions.Add(redaction)

'Save and close the PDF document

document.Save("Output.pdf")

document.Close(True)

{% endhighlight %}

{% highlight UWP %}

//PDF supports redaction only in Windows Forms, WPF, ASP.NET, ASP.NET MVC.

{% endhighlight %}

{% highlight ASP.NET Core %}

//PDF supports redaction only in Windows Forms, WPF, ASP.NET, ASP.NET MVC.

{% endhighlight %}

{% highlight Xamarin %}

//PDF supports redaction only in Windows Forms, WPF, ASP.NET, ASP.NET MVC.

{% endhighlight %}
{% endtabs %}

## Fill color on the redacted area

You can draw the filled rectangle on the redacted bounds using the [FillColor](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Redaction.PdfRedaction.html#Syncfusion_Pdf_Redaction_PdfRedaction_FillColor) property in [PdfRedaction](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Redaction.PdfRedaction.html) class.

The following code snippet explains how to redact the information from a page with filled rectangle.

{% tabs %}
{% highlight c# %}

//Load a PDF document

PdfLoadedDocument document = new PdfLoadedDocument("Input.pdf");

//Get first page from the document

PdfLoadedPage page = document.Pages[0] as PdfLoadedPage;

//Create PDF redaction for the page

PdfRedaction redaction = new PdfRedaction(new RectangleF(343, 147, 60, 17));

//Set fill color for the redaction bounds

redaction.FillColor = System.Drawing.Color.Black;

//Adds redaction to the loaded page

page.Redactions.Add(redaction);

//Save and close the PDF document

document.Save("Output.pdf");

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Load a PDF document

Dim document As PdfLoadedDocument = New PdfLoadedDocument("Input.pdf")

'Get first page from the document

Dim page As PdfLoadedPage = TryCast(document.Pages(0), PdfLoadedPage)

'Create PDF redaction for the page

Dim redaction As PdfRedaction = New PdfRedaction(New RectangleF(343, 147, 60, 17))

'Set fill color for the redaction bounds

redaction.FillColor = System.Drawing.Color.Black

'Adds redaction to the loaded page

page.Redactions.Add(redaction)

'Save and close the PDF document

document.Save("Output.pdf")

document.Close(True)

{% endhighlight %}

{% highlight UWP %}

//PDF supports redaction only in Windows Forms, WPF, ASP.NET, ASP.NET MVC.

{% endhighlight %}

{% highlight ASP.NET Core %}

//PDF supports redaction only in Windows Forms, WPF, ASP.NET, ASP.NET MVC.

{% endhighlight %}

{% highlight Xamarin %}

//PDF supports redaction only in Windows Forms, WPF, ASP.NET, ASP.NET MVC.

{% endhighlight %}
{% endtabs %}

## Redaction without fill color and appearance

You can redact PDF without drawing the filled rectangle or text on the redacted bounds.

The following code snippet explains how to redact the information from a page without drawing fill color and appearance on the redaction bounds.

{% tabs %}
{% highlight c# %}

//Load a PDF document

PdfLoadedDocument document = new PdfLoadedDocument("Input.pdf");

//Get first page from the document

PdfLoadedPage page = document.Pages[0] as PdfLoadedPage;

//Create PDF redaction for the page

PdfRedaction redaction = new PdfRedaction(new RectangleF(343, 147, 60, 17));

//Adds redaction to the loaded page

page.Redactions.Add(redaction);

//Save and close the PDF document

document.Save("Output.pdf");

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Load a PDF document

Dim document As PdfLoadedDocument = New PdfLoadedDocument("Input.pdf")

'Get first page from the document

Dim page As PdfLoadedPage = TryCast(document.Pages(0), PdfLoadedPage)

'Create PDF redaction for the page

Dim redaction As PdfRedaction = New PdfRedaction(New RectangleF(343, 147, 60, 17))

'Adds redaction to the loaded page

page.Redactions.Add(redaction)

'Save and close the PDF document

document.Save("Output.pdf")

document.Close(True)

{% endhighlight %}

{% highlight UWP %}

//PDF supports redaction only in Windows Forms, WPF, ASP.NET, ASP.NET MVC.

{% endhighlight %}

{% highlight ASP.NET Core %}

//PDF supports redaction only in Windows Forms, WPF, ASP.NET, ASP.NET MVC.

{% endhighlight %}

{% highlight Xamarin %}

//PDF supports redaction only in Windows Forms, WPF, ASP.NET, ASP.NET MVC.

{% endhighlight %}
{% endtabs %}
