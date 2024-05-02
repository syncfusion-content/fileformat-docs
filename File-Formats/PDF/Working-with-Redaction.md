---
title: Working with Redaction |Syncfusion
description: This section explains how to Redact the content from an existing PDF document by using Essential PDF
platform: file-formats
control: PDF
documentation: UG
---
# Working with PDF Redaction

Redacting a PDF is the process of permanently removing sensitive or confidential information from PDF documents. Syncfusion's [.NET PDF library](https://www.syncfusion.com/document-processing/pdf-framework/net/pdf-library) provides an easy way to redact PDF documents. 

N> 1.CJK text without TrueType font and complex script text cannot be redacted.
N> 2.To redact the content from the existing PDF document in .NET Core, you need to include the Syncfusion.Pdf.Imaging.Portable assembly reference in the .NET Core project.

To quickly get started with redacting PDF documents in .NET using the PDF Library, check this video. 
{% youtube "https://www.youtube.com/watch?v=sSnHbKm3WTk" %}

## Removing sensitive content from the PDF document

The following code example demonstrates the redaction of PDF documents from the specified bounds using [PdfRedaction](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Redaction.PdfRedaction.html#Syncfusion_Pdf_Redaction_PdfRedaction__ctor_System_Drawing_RectangleF_System_Drawing_Color_) class. 

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Load the existing PDF document
FileStream docStream = new FileStream(@"Input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument document = new PdfLoadedDocument(docStream);
//Get the first page from the document
PdfLoadedPage page = document.Pages[0] as PdfLoadedPage;

//Create a redaction object
PdfRedaction redaction = new PdfRedaction(new RectangleF(343, 147, 60, 17));
//Add a redaction object into the redaction collection of loaded page
page.AddRedaction(redaction);
//Redact the contents from the PDF document
document.Redact();

//Creating the stream object
MemoryStream stream = new MemoryStream();
//Save the document
document.Save(stream);
//Close the document
document.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Load a PDF document
PdfLoadedDocument document = new PdfLoadedDocument("Input.pdf");
//Get first page from the document
PdfLoadedPage page = document.Pages[0] as PdfLoadedPage;

//Create PDF redaction for the page
PdfRedaction redaction = new PdfRedaction(new RectangleF(343, 147, 60, 17), System.Drawing.Color.Black);
//Adds redaction to the loaded page
page.Redactions.Add(redaction);

//Save and close the PDF document
document.Save("Output.pdf");
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

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

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Redaction/Removing-sensitive-content-from-the-PDF-document/).

## Display text on the redacted area

You can draw overlay text on the redacted area using the [Appearance](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Redaction.PdfRedaction.html#Syncfusion_Pdf_Redaction_PdfRedaction_Appearance) property available in [PdfRedaction](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Redaction.PdfRedaction.html) class, and customize the overlay text with different font, style, color and brushes.

The following code example explains how to add overlay text in the redacted area.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Load the existing PDF document
FileStream docStream = new FileStream(@"Input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument document = new PdfLoadedDocument(docStream);
//Get the first page from the document 
PdfLoadedPage page = document.Pages[0] as PdfLoadedPage;

//Create a redaction object
PdfRedaction redaction = new PdfRedaction(new RectangleF(343, 167, 100, 25), Color.Black);
//Font for the overlay text 
PdfStandardFont font = new PdfStandardFont(PdfFontFamily.Courier, 10); 
//Draw text on the redacted area 
redaction.Appearance.Graphics.DrawString("Redacted", font, PdfBrushes.Red, new PointF(5, 5));
//Add a redaction object into the redaction collection of loaded page
page.AddRedaction(redaction);
//Redact the contents from the PDF document
document.Redact();

//Creating the stream object
MemoryStream stream = new MemoryStream();
//Save the document
document.Save(stream);
//Close the document
document.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

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

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Redaction/Display-text-on-the-redacted-area/).

## Drawing image on the redacted area

You can draw the image on the redacted area using the [Appearance](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Redaction.PdfRedaction.html#Syncfusion_Pdf_Redaction_PdfRedaction_Appearance) property in [PdfRedaction](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Redaction.PdfRedaction.html) class.

The following code example explains how to redact the information from a page by drawing image on the redacted area using appearance.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}	

//Load the existing PDF document
FileStream docStream = new FileStream(@"Input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument document = new PdfLoadedDocument(docStream);
//Get the first page from the document 
PdfLoadedPage page = document.Pages[0] as PdfLoadedPage;

//Create a PDF redaction for the page 
PdfRedaction redaction = new PdfRedaction(new RectangleF(63, 57, 182, 157)); 
//Draw the image on the redacted bounds 
PdfImage image = new PdfBitmap("Image.png"); 
redaction.Appearance.Graphics.DrawImage(image, new RectangleF(0, 0, 182, 157));
//Add a redaction object into the redaction collection of loaded page
page.AddRedaction(redaction);
//Redact the contents from the PDF document
document.Redact();

//Creating the stream object
MemoryStream stream = new MemoryStream();
//Save the document
document.Save(stream);
//Close the document
document.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

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

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Redaction/Draw-image-on-the-redacted-area-in-PDF-document/).

## Drawing pattern on the redacted area

You can draw the different patterns on the redacted area using the [Appearance](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Redaction.PdfRedaction.html#Syncfusion_Pdf_Redaction_PdfRedaction_Appearance) property in the [PdfRedaction](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Redaction.PdfRedaction.html) class.

The following code example explains how to redact the information from a page by drawing mosaic pattern on the redacted area using appearance.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}	

//Load the existing PDF document
FileStream docStream = new FileStream(@"Input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument document = new PdfLoadedDocument(docStream);
//Get the first page from the document 
PdfLoadedPage page = document.Pages[0] as PdfLoadedPage;

//Create a PDF redaction for the page 
PdfRedaction redaction = new PdfRedaction(new RectangleF(341, 149, 64, 14)); 

//Draw a mosaic pattern on the redaction bounds 
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
rect = new RectangleF(0, 0, 16, 14); PdfTilingBrush tillingBrushNew = new PdfTilingBrush(rect); 
tillingBrushNew.Graphics.DrawRectangle(tillingBrush, rect); 

/Draw rectangle on the redacted bounds 
redaction.Appearance.Graphics.DrawRectangle(tillingBrushNew, new RectangleF(0, 0, 64, 14)); 
//Add a redaction object into the redaction collection of loaded page
page.AddRedaction(redaction);
//Redact the contents from the PDF document
document.Redact();

//Creating the stream object
MemoryStream stream = new MemoryStream();
//Save the documents
document.Save(stream);
//Close the documents
document.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

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

//Draw rectangle on the redacted bounds 
redaction.Appearance.Graphics.DrawRectangle(tillingBrushNew, new RectangleF(0, 0, 64, 14));
//Adds redaction to the loaded page
page.Redactions.Add(redaction);

//Save and close the PDF document
document.Save("Output.pdf");
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

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

'Draw rectangle on the redacted bounds 
redaction.Appearance.Graphics.DrawRectangle(tillingBrushNew, New RectangleF(0, 0, 64, 14))
'Adds redaction to the loaded page
page.Redactions.Add(redaction)

'Save and close the PDF document
document.Save("Output.pdf")
document.Close(True)

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Redaction/Draw-pattern-on-the-redacted-area-in-PDF-document/).

## Fill color on the redacted area

You can draw the filled rectangle on the redacted bounds using the [FillColor](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Redaction.PdfRedaction.html#Syncfusion_Pdf_Redaction_PdfRedaction_FillColor) property in [PdfRedaction](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Redaction.PdfRedaction.html) class.

The following code example explains how to redact the information from a page with filled rectangle.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Load the existing PDF document
FileStream docStream = new FileStream(@"Input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument document = new PdfLoadedDocument(docStream);
//Get the first page from the document 
PdfLoadedPage page = document.Pages[0] as PdfLoadedPage;

//Create a PDF redaction for the page 
PdfRedaction redaction = new PdfRedaction(new RectangleF(343, 147, 60, 17)); 
//Set fill color for the redaction bounds 
redaction.FillColor = System.Drawing.Color.Black;
//Add a redaction object into the redaction collection of loaded page
page.AddRedaction(redaction);
//Redact the contents from the PDF document
document.Redact();

//Creating the stream object
MemoryStream stream = new MemoryStream();
//Save the document
document.Save(stream);
//Close the document
document.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

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

{% endtabs %}
 
You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Redaction/Fill-color-on-the-redacted-area-in-a-PDF/).

## Redaction without fill color and appearance

You can redact PDF without drawing the filled rectangle or text on the redacted bounds using the [PdfRedaction](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Redaction.PdfRedaction.html#Syncfusion_Pdf_Redaction_PdfRedaction__ctor_System_Drawing_RectangleF_) class.

The following code snippet explains how to redact the information from a page without drawing fill color and appearance on the redaction bounds.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Load the existing PDF document
FileStream docStream = new FileStream(@"Input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument document = new PdfLoadedDocument(docStream);
//Get the first page from the document 
PdfLoadedPage page = document.Pages[0] as PdfLoadedPage;

//Create a PDF redaction for the page 
PdfRedaction redaction = new PdfRedaction(new RectangleF(343, 147, 60, 17));

//Add a redaction object into the redaction collection of loaded page
page.AddRedaction(redaction);
//Redact the contents from the PDF document
document.Redact();

//Creating the stream object
MemoryStream stream = new MemoryStream();
//Save the document
document.Save(stream);
//Close the document
document.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

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

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Redaction/Redaction-without-fill-color-and-appearance/).

## Get redaction progress 

You can get the redaction process using [RedactionProgress](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html#Syncfusion_Pdf_Parsing_PdfLoadedDocument_RedactionProgress) event in [PdfLoadedDocument](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html) class.   

The code snippet to illustrate the same is given below.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Load an existing PDF document
FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);
//Load the first page
PdfLoadedPage page = loadedDocument.Pages[0] as PdfLoadedPage;

//Create PDF redaction for the page
PdfRedaction redaction = new PdfRedaction(new RectangleF(37, 94, 50, 10), System.Drawing.Color.Black);
//Add redaction to the loaded page
page.AddRedaction(redaction);
loadedDocument.RedactionProgress += redaction_TrackProgress;

//Create the stream object
MemoryStream stream = new MemoryStream();
//Save the document into stream
loadedDocument.Save(stream);
//Close the document
loadedDocument.Close(true);

//Event handler for Track redaction process
void redaction_TrackProgress(object sender, RedactionProgressEventArgs arguments)
{
 MessageBox.Show(String.Format("Redaction Process " + arguments.Progress + " % completed"));
}

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Load a PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("input.pdf");
//Load the first page
PdfLoadedPage page = loadedDocument.Pages[0] as PdfLoadedPage ;

//Create PDF redaction for the page
PdfRedaction redaction = new PdfRedaction(new RectangleF(37, 94, 50, 10), System.Drawing.Color.Black);
//Add redaction to the loaded page
page.Redactions.Add(redaction);
loadedDocument.RedactionProgress += redaction_TrackProgress;

//Save the document
loadedDocument.Save("Output.pdf");
//Close the document
loadedDocument.Close(true);

//Event handler for Track redaction process
void redaction_TrackProgress(object sender, RedactionProgressEventArgs arguments)
{
MessageBox.Show(String.Format("Redaction Process " + arguments.Progress + " % completed"));
}

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Load an existing PDF document
Dim loadedDocument As PdfLoadedDocument = New PdfLoadedDocument("input.pdf") 
'Load the first page 
Dim page As PdfLoadedPage =  loadedDocument.Pages(0) as PdfLoadedPage

'Create PDF redaction for the page
Dim redaction As PdfRedaction =  New PdfRedaction(New RectangleF(37,94,50,10),System.Drawing.Color.Black)
'Add redaction to the loaded page
page.Redactions.Add(redaction)
loadedDocument.RedactionProgress += redaction_TrackProgress

'Save the document
Dim stream As New MemoryStream()
loadedDocument.Save(stream) 
'Close the document
loadedDocument.Close(True)

'Event handler for Track redaction process
Private  Sub redaction_TrackProgress(ByVal sender As Object, ByVal arguments As RedactionProgressEventArgs)
MessageBox.Show(String.Format("Redaction Process " + arguments.Progress + " % completed"))

{% endhighlight %}

{% endtabs %}

## Redaction result 

Using [PdfRedactionResult](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Redaction.PdfRedactionResult.html) class, you can get the status of the redaction with other information. The result of the redaction operation can be obtained using Essential PDF and the below code example illustrates the same. 

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Load an existing PDF document. 
FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);
//Load the first page.
PdfLoadedPage page = loadedDocument.Pages[0];

//Create PDF redaction for the page 
PdfRedaction redaction = new PdfRedaction(new RectangleF(37, 94, 50, 10), System.Drawing.Color.Black);
//Add redaction to the loaded page
page.AddRedaction(redaction);

//Redact the contents from PDF document
List<PdfRedactionResult> results = loadedDocument.Redact();
foreach(PdfRedactionResult result in redactionResults)
{
if (result.IsRedactionSuccess)
Console.WriteLine("Content redacted successfully...");
else
Console.WriteLine("Content not redacted properly...");
}

//Create the stream object
MemoryStream stream = new MemoryStream();
//Save the document into stream
loadedDocument.Save(stream);
//Close the document
loadedDocument.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Load an existing PDF document
PdfLoadedDocument lDoc = new PdfLoadedDocument("input.pdf");
//Load the first page
PdfLoadedPage page = lDoc.Pages[0] as PdfLoadedPage;

//Create PDF redaction for the page 
PdfRedaction redaction = new PdfRedaction(new RectangleF(37, 94, 50, 10), System.Drawing.Color.Black);
//Add redaction object into redaction collection of loaded page
page.Redactions.Add(redaction);

//Redact the contents from PDF document.
List<PdfRedactionResult> redactionResults = lDoc.Redact();
foreach(PdfRedactionResult result in redactionResults)
{
if (result.IsRedactionSuccess)
Console.WriteLine("Content redacted successfully...");
else
Console.WriteLine("Content not redacted properly...");
}

//Save the document
lDoc.Save("Output.pdf");
//Close the document
lDoc.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Load an existing PDF 
Dim loadedDocument As PdfLoadedDocument = New PdfLoadedDocument("input.pdf") 
'Load the first page 
Dim page As PdfLoadedPage =  loadedDocument.Pages(0) as PdfLoadedPage

'Create PDF redaction for the page 
Dim redaction As PdfRedaction =  New PdfRedaction(New RectangleF(37,94,50,10),System.Drawing.Color.Black)
'Add redaction to the loaded page
page.Redactions.Add(redaction)

'Redact the contents from PDF document
Dim results As List<PdfRedactionResult> = loadedDocument.Redact();
For Each result As PdfRedactionResult In redactionResults
If result.IsRedactionSuccess Then 
Console.WriteLine("Content redacted successfully...")
Else
Console.WriteLine("Content not redacted properly...")
End If
Next

'Save the document
Dim stream As New MemoryStream()
loadedDocument.Save(stream) 
'Close the document
loadedDocument.Close(True)

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Redaction/Get-the-result-of-redaction-with-other-information/).

## Redact text content alone on the redacted area

You can get the Redact text content alone on the redacted area using [RedactionProgress](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html#Syncfusion_Pdf_Parsing_PdfLoadedDocument_RedactionProgress) event in [PdfLoadedDocument](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html) class.   

The code snippet to illustrate the same is given below.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Load an existing PDF document
FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);
PdfRedaction redaction = new PdfRedaction(new RectangleF(150, 150, 60, 24), Color.Transparent);
//Only the text within the redaction bounds should be redacted.
redaction.TextOnly = true;
foreach (PdfLoadedPage loadedPage in document.Pages)
{
    loadedPage.AddRedaction(redaction);
}
document.Redact();
//Create the stream object
MemoryStream stream = new MemoryStream();
//Save the document into stream
loadedDocument.Save(stream);
//Close the document
loadedDocument.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Load a PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("input.pdf");
PdfRedaction redaction = new PdfRedaction(new RectangleF(150, 150, 60, 24), Color.Transparent);
//Only the text within the redaction bounds should be redacted.
redaction.TextOnly = true;
foreach (PdfLoadedPage loadedPage in document.Pages)
{
    loadedPage.AddRedaction(redaction);
}
document.Redact();
//Save the document
loadedDocument.Save("Output.pdf");
//Close the document
loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Load an existing PDF document
Dim loadedDocument As PdfLoadedDocument = New PdfLoadedDocument("input.pdf") 
'Create PDF redaction for the page
Dim redaction As PdfRedaction = New PdfRedaction(New RectangleF(150, 150, 60, 24), Color.Transparent)
redaction.TextOnly = true;
For Each loadedPage As PdfLoadedPage In document.Pages
	loadedPage.AddRedaction(redaction)
Next
document.Redact()
'Save the document
Dim stream As New MemoryStream()
loadedDocument.Save(stream) 
'Close the document
loadedDocument.Close(True)


{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Redaction/Redact-text-content-alone-on-the-redated-area/).


## Find text by regular expression pattern and redact it from PDF document.

You can find text by regular expression pattern and redact it from PDF document using the [PdfRedaction](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Redaction.PdfRedaction.html#Syncfusion_Pdf_Redaction_PdfRedaction__ctor_System_Drawing_RectangleF_) class.

The following code snippet explains how to find text by regular expression pattern and redact it from PDF document.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

    //Create stream from an existing PDF document.
    FileStream docStream = new FileStream(Path.GetFullPath("Input.pdf"), FileMode.Open, FileAccess.Read);

    //Load the existing PDF document.
    PdfLoadedDocument document = new PdfLoadedDocument(docStream);

    //Get the first page from the document.
    PdfLoadedPage page = document.Pages[0] as PdfLoadedPage;

    TextLineCollection collection = new TextLineCollection();
    //Extract text from first page.
    string extractedText = page.ExtractText(out collection);

    foreach (TextLine line in collection.TextLine)
    {
        foreach (TextWord word in line.WordCollection)
        {
            //Define regular expression pattern to search for dates in the format MM/DD/YYYY
            string datePattern = @"\b\d{1,2}\/\d{1,2}\/\d{4}\b";
            //Search for dates
            MatchCollection dateMatches = Regex.Matches(word.Text, datePattern);
            //Add redaction if the match found
            foreach (Match dateMatch in dateMatches)
            {
                string textToFindAndRedact = dateMatch.Value;
                if (textToFindAndRedact == word.Text)
                {
                    //Create a redaction object.
                    PdfRedaction redaction = new PdfRedaction(word.Bounds, Syncfusion.Drawing.Color.Black);
                    //Add a redaction object into the redaction collection of loaded page.
                    page.AddRedaction(redaction);
                }
            }
        }
    }

    //Redact the contents from the PDF document.
    document.Redact();

    //Creating the stream object
    MemoryStream stream = new MemoryStream();
    //Save the document
    document.Save(stream);
    //Close the document
    document.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

    //Load a PDF document
    PdfLoadedDocument document = new PdfLoadedDocument("Input.pdf");

    //Get the first page from the document.
    PdfLoadedPage page = document.Pages[0] as PdfLoadedPage;

    TextLineCollection collection = new TextLineCollection();
    //Extract text from first page.
    string extractedText = page.ExtractText(out collection);

    foreach (TextLine line in collection.TextLine)
    {
        foreach (TextWord word in line.WordCollection)
        {
            //Define regular expression pattern to search for dates in the format MM/DD/YYYY
            string datePattern = @"\b\d{1,2}\/\d{1,2}\/\d{4}\b";
            //Search for dates
            MatchCollection dateMatches = Regex.Matches(word.Text, datePattern);
            //Add redaction if the match found
            foreach (Match dateMatch in dateMatches)
            {
                string textToFindAndRedact = dateMatch.Value;
                if (textToFindAndRedact == word.Text)
                {
                    //Create a redaction object.
                    PdfRedaction redaction = new PdfRedaction(word.Bounds, Syncfusion.Drawing.Color.Black);
                    //Add a redaction object into the redaction collection of loaded page.
                    page.Redactions.Add(redaction);
                }
            }
        }
    }
    //Save and close the PDF document
    document.Save("Output.pdf");
    document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Create stream from an existing PDF document.
        Dim docStream As New FileStream(Path.GetFullPath("Input.pdf"), FileMode.Open, FileAccess.Read)

        'Load the existing PDF document.
        Dim document As New PdfLoadedDocument(docStream)

        'Get the first page from the document.
        Dim page As PdfLoadedPage = TryCast(document.Pages(0), PdfLoadedPage)

        Dim collection As New TextLineCollection()
        'Extract text from first page.
        Dim extractedText As String = page.ExtractText(collection)

        For Each line As TextLine In collection.TextLine
            For Each word As TextWord In line.WordCollection
                'Define regular expression pattern to search for dates in the format MM/DD/YYYY
                Dim datePattern As String = "\b\d{1,2}\/\d{1,2}\/\d{4}\b"
                'Search for dates
                Dim dateMatches As MatchCollection = Regex.Matches(word.Text, datePattern)
                'Add redaction if the match found
                For Each dateMatch As Match In dateMatches
                    Dim textToFindAndRedact As String = dateMatch.Value
                    If textToFindAndRedact = word.Text Then
                        'Create a redaction object.
                        Dim redaction As New PdfRedaction(word.Bounds, Syncfusion.Drawing.Color.Black)
                        'Add a redaction object into the redaction collection of loaded page.
                        page.AddRedaction(redaction)
                    End If
                Next
            Next
        Next

        'Redact the contents from the PDF document.
        document.Redact()

        'Creating the stream object
        Dim stream As New MemoryStream()
        'Save the document
        document.Save(stream)
        'Close the document
        document.Close(True)

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub]().