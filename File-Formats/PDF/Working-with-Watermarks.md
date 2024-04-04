---
title: Working with Watermarks | Syncfusion
description: This section explains how to add text and image watermarks to the newly PDF document and to an existing PDF document using Syncfusion .NET PDF library.
platform: file-formats
control: PDF
documentation: UG
---
# Working with Watermarks

The Essential PDF provides support to add watermark or stamp with text and images in the PDF document.

To quickly get started, add Watermarks and Bookmarks to a PDF document in .NET using the PDF Library. Please, check this video:
{% youtube " https://www.youtube.com/watch?v=C6nYz8fn0To" %}

## Adding text watermark in PDF document

The below code illustrates how to draw the text watermark in new PDF document using [DrawString](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfGraphics.html#Syncfusion_Pdf_Graphics_PdfGraphics_DrawString_System_String_Syncfusion_Pdf_Graphics_PdfFont_Syncfusion_Pdf_Graphics_PdfPen_Syncfusion_Pdf_Graphics_PdfBrush_System_Drawing_PointF_) method of [PdfGraphics](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfGraphics.html) class. The transparency can be applied to the text or images using [SetTransparency](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfGraphics.html#Syncfusion_Pdf_Graphics_PdfGraphics_SetTransparency_System_Single_) method and rotation can be applied using [RotateTransform](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfGraphics.html#Syncfusion_Pdf_Graphics_PdfGraphics_RotateTransform_System_Single_) method. 

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Create a new PDF document.
PdfDocument pdfDocument = new PdfDocument();
//Add a page to the PDF document.
PdfPage pdfPage = pdfDocument.Pages.Add();
//Create PDF graphics for the page.
PdfGraphics graphics = pdfPage.Graphics;

//Set the font.
PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);
//Add watermark text.
PdfGraphicsState state = graphics.Save();
graphics.SetTransparency(0.25f);
graphics.RotateTransform(-40);
graphics.DrawString("Imported using Essential PDF", font, PdfPens.Red, PdfBrushes.Red, new PointF(-150, 450));

//Save the document into stream.
MemoryStream stream = new MemoryStream();
pdfDocument.Save(stream);
stream.Position = 0;
//Close the document.
pdfDocument.Close(true);
//Defining the content type for PDF file.
string contentType = "application/pdf";
//Define the file name.
string fileName = "Watermark.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name.
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Create a new PDF document.
PdfDocument pdfDocument = new PdfDocument();
//Add a page to the PDF document.
PdfPage pdfPage = pdfDocument.Pages.Add();
//Create PDF graphics for the page.
PdfGraphics graphics = pdfPage.Graphics;

//Set the font.
PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);
//Add watermark text.
PdfGraphicsState state = graphics.Save();
graphics.SetTransparency(0.25f);
graphics.RotateTransform(-40);
graphics.DrawString("Imported using Essential PDF", font, PdfPens.Red, PdfBrushes.Red, new PointF(-150, 450));

//Save and close the document.
pdfDocument.Save("Watermark.pdf");
pdfDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Create a new PDF document.
Dim pdfDocument As New PdfDocument()
'Add a page to the PDF document.
Dim pdfPage As PdfPage = pdfDocument.Pages.Add()
'Create PDF graphics for the page.
Dim graphics As PdfGraphics = pdfPage.Graphics

'Set the font.
Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 20)
'Add watermark text.
Dim state As PdfGraphicsState = graphics.Save()
graphics.SetTransparency(0.25F)
graphics.RotateTransform(-40)
graphics.DrawString("Imported using Essential PDF", font, PdfPens.Red, PdfBrushes.Red, New PointF(-150, 450))

'Save and close the document.
pdfDocument.Save("Watermark.pdf")
pdfDocument.Close(True)

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Watermark/Adding-text-watermark-in-PDF-document).

The following screenshot shows the output of adding text watermark to PDF document. 
<img src="Watermark_images/Watermark_img1.png" alt="Text watermark to PDF" width="100%" Height="Auto"/>

The below code illustrates how to draw the text watermark in an existing PDF document using [DrawString](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfGraphics.html#Syncfusion_Pdf_Graphics_PdfGraphics_DrawString_System_String_Syncfusion_Pdf_Graphics_PdfFont_Syncfusion_Pdf_Graphics_PdfBrush_System_Drawing_PointF_) method of [PdfGraphics](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfGraphics.html) class.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Load an existing PDF document.
FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);
//Get first page from document.
PdfPageBase loadedPage = loadedDocument.Pages[0];
//Create PDF graphics for the page.
PdfGraphics graphics = loadedPage.Graphics;

//Set the standard font.
PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Add watermark text.
PdfGraphicsState state = graphics.Save();
graphics.SetTransparency(0.25f);
graphics.RotateTransform(-40);
graphics.DrawString("Imported using Essential PDF", font, PdfPens.Red, PdfBrushes.Red, new PointF(-150, 

//Save the document into stream.
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);
stream.Position = 0;
//Close the document.
loadedDocument.Close(true);
//Defining the content type for PDF file.
string contentType = "application/pdf";
//Define the file name.
string fileName = "Watermark.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name.
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Load an existing PDF document.
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);
//Get first page from document.
PdfPageBase loadedPage = loadedDocument.Pages[0];
//Create PDF graphics for the page.
PdfGraphics graphics = loadedPage.Graphics;

//Set the standard font.
PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);
//Add watermark text.
PdfGraphicsState state = graphics.Save();
graphics.SetTransparency(0.25f);
graphics.RotateTransform(-40);
graphics.DrawString("Imported using Essential PDF", font, PdfPens.Red, PdfBrushes.Red, new PointF(-150, 450));

//Save and close the document.
loadedDocument.Save("Watermark.pdf");
loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Load an existing PDF document.
Dim loadedDocument As New PdfLoadedDocument(fileName)
'Get first page from document.
Dim loadedPage As PdfPageBase = loadedDocument.Pages(0)
'Create PDF graphics for the page.
Dim graphics As PdfGraphics = loadedPage.Graphics

'Set the font.
Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 20)

'Add watermark text.
Dim state As PdfGraphicsState = graphics.Save()
graphics.SetTransparency(0.25F)
graphics.RotateTransform(-40)
graphics.DrawString("Imported using Essential PDF", font, PdfPens.Red, PdfBrushes.Red, New PointF(-150, 450))

'Save and close the document.
loadedDocument.Save("Watermark.pdf")
loadedDocument.Close(True)

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Watermark/Add-text-watermark-in-an-existing-PDF-document/).

The following screenshot shows the output of adding text watermark to an existing PDF document. 
<img src="Watermark_images/Watermark_img2.png" alt="Text watermark in an existing PDF" width="100%" Height="Auto"/>

## Adding image watermark in PDF document

The below code sample illustrates how to add image watermark in PDF document, using [DrawImage](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfGraphics.html#Syncfusion_Pdf_Graphics_PdfGraphics_DrawImage_Syncfusion_Pdf_Graphics_PdfImage_System_Drawing_PointF_System_Drawing_SizeF_) method of [PdfGraphics](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfGraphics.html) class. The transparency can be applied to the text or images using [SetTransparency](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfGraphics.html#Syncfusion_Pdf_Graphics_PdfGraphics_SetTransparency_System_Single_) method and rotation can be applied using [RotateTransform](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfGraphics.html#Syncfusion_Pdf_Graphics_PdfGraphics_RotateTransform_System_Single_) method. 

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}	

//Create a new PDF document.
PdfDocument pdfDocument = new PdfDocument();
//Add a page to the PDF document.
PdfPage pdfPage = pdfDocument.Pages.Add();
//Create PDF graphics for the page. 
PdfGraphics graphics = pdfPage.Graphics;

//Load the image as stream.
FileStream imageStream = new FileStream("Image.jpeg", FileMode.Open, FileAccess.Read);
//Image watermark.
PdfImage image = new PdfBitmap(imageStream);
PdfGraphicsState state = graphics.Save();
graphics.SetTransparency(0.25f);
//Draw the image. 
graphics.DrawImage(image, new PointF(0, 0), pdfPage.Graphics.ClientSize);

//Save the document into stream.
MemoryStream stream = new MemoryStream();
pdfDocument.Save(stream);
stream.Position = 0;
//Close the document.
pdfDocument.Close(true);
//Defining the content type for PDF file.
string contentType = "application/pdf";
//Define the file name.
string fileName = "Watermark.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name.
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Create a new PDF document.
PdfDocument pdfDocument = new PdfDocument();
//Add a page to the PDF document.
PdfPage pdfPage = pdfDocument.Pages.Add();
//Create PDF graphics for the page.
PdfGraphics graphics = pdfPage.Graphics;

//Add image watermark.
PdfImage image = new PdfBitmap("Image.jpeg");
PdfGraphicsState state = graphics.Save();
graphics.SetTransparency(0.25f);
//Draw the image
graphics.DrawImage(image, new PointF(0, 0), pdfPage.Graphics.ClientSize);

//Save and close the document.
pdfDocument.Save("Watermark.pdf");
pdfDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Create a new PDF document.
Dim pdfDocument As New PdfDocument()
'Add a page to the PDF document.
Dim pdfPage As PdfPage = pdfDocument.Pages.Add()
'Create PDF graphics for the page
Dim graphics As PdfGraphics = pdfPage.Graphics

'Add image watermark.
Dim image As PdfImage = New PdfBitmap("Image.jpeg")
Dim state As PdfGraphicsState = graphics.Save()
graphics.SetTransparency(0.25F)
'Draw the image.
graphics.DrawImage(image, New PointF(0, 0), pdfPage.Graphics.ClientSize)

'Save and close the document.
pdfDocument.Save("Watermark.pdf")
pdfDocument.Close(True)

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Watermark/Adding-image-watermark-in-PDF-document).

The following screenshot shows the output of adding image watermark to PDF document. 
<img src="Watermark_images/Watermark_img3.jpg" alt="Image watermark to PDF" width="100%" Height="Auto"/>

The below code illustrates how to draw the image watermark in existing PDF document using  using [DrawImage](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfGraphics.html#Syncfusion_Pdf_Graphics_PdfGraphics_DrawImage_Syncfusion_Pdf_Graphics_PdfImage_System_Drawing_PointF_System_Drawing_SizeF_) method of [PdfGraphics](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfGraphics.html) class. 

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Load the PDF document
FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);
//Get first page from document
PdfPageBase loadedPage = loadedDocument.Pages[0];
//Create PDF graphics for the page
PdfGraphics graphics = loadedPage.Graphics;

//Load the image file as stream
FileStream imageStream = new FileStream("Image.jpeg", FileMode.Open, FileAccess.Read);
PdfImage image = new PdfBitmap(imageStream);
PdfGraphicsState state = graphics.Save();
graphics.SetTransparency(0.25f);
//Draw the image
graphics.DrawImage(image, new PointF(0, 0), loadedPage.Graphics.ClientSize);

//Save the document into stream
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);
stream.Position = 0;
//Close the document
loadedDocument.Close(true);
//Defining the content type for PDF file
string contentType = "application/pdf";
//Define the file name
string fileName = "Watermark.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Load an existing document.
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);
//Get first page from document.
PdfPageBase loadedPage = loadedDocument.Pages[0];
//Create PDF graphics for the page.
PdfGraphics graphics = loadedPage.Graphics;

//Add image watermark.
PdfImage image = new PdfBitmap("Image.jpeg");
PdfGraphicsState state = graphics.Save();
graphics.SetTransparency(0.25f);
//Draw the image. 
graphics.DrawImage(image, new PointF(0, 0), loadedPage.Graphics.ClientSize);

//Save and close the document.
loadedDocument.Save("watermark.pdf");
loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Load the document.
Dim loadedDocument As New PdfLoadedDocument(fileName)
'Get first page from document.
Dim loadedPage As PdfPageBase = loadedDocument.Pages(0)
'Create PDF graphics for the page
Dim graphics As PdfGraphics = loadedPage.Graphics

'Add image watermark.
Dim image As PdfImage = New PdfBitmap("Image.jpeg")
Dim state As PdfGraphicsState = graphics.Save()
graphics.SetTransparency(0.25F)
'Draw the image.
graphics.DrawImage(image, New PointF(0, 0), loadedPage.Graphics.ClientSize)

'Save and close the document.
loadedDocument.Save("watermark.pdf")
loadedDocument.Close(True)

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Watermark/Draw-the-image-watermark-in-an-existing-PDF-document).

The following screenshot shows the output of adding image watermark to an existing PDF document. 
<img src="Watermark_images/Watermark_img4.jpg" alt="Image watermark in an existing PDF" width="100%" Height="Auto"/>


### Adding Watermark Annotation

A watermark annotation is used to represent graphics that are expected to be printed at a fixed size and position on a page, regardless of the dimensions of the printed page. [PdfWatermarkAnnotation](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfWatermarkAnnotation.html) can be used.
The following code example explains how to add a watermark annotation in the PDF document

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//Load the PDF document
FileStream docStream = new FileStream("input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);
//Get the page 
PdfLoadedPage lpage = loadedDocument.Pages[0] as PdfLoadedPage;

//Creates PDF watermark annotation 
PdfWatermarkAnnotation watermark = new PdfWatermarkAnnotation(new RectangleF(50, 100, 100, 50));
//Sets properties to the annotation 
watermark.Opacity = 0.5f; 
//Create the appearance of watermark 
watermark.Appearance.Normal.Graphics.DrawString("Watermark Text", new PdfStandardFont(PdfFontFamily.Helvetica, 20), PdfBrushes.Red, new RectangleF(0, 0, 200, 50), new PdfStringFormat(PdfTextAlignment.Center, PdfVerticalAlignment.Middle));
//Adds the annotation to page 
lpage.Annotations.Add(watermark);

//Save the document into stream
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);
//Close the document 
loadedDocument.Close(true); 

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Load the existing PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("input.pdf");
//Get the page 
PdfLoadedPage lpage = loadedDocument.Pages[0] as PdfLoadedPage;

//Creates PDF watermark annotation 
PdfWatermarkAnnotation watermark = new PdfWatermarkAnnotation(new RectangleF(50, 100, 100, 50));
//Sets properties to the annotation 
watermark.Opacity = 0.5f; 
//Create the appearance of watermark 
watermark.Appearance.Normal.Graphics.DrawString("Watermark Text", new PdfStandardFont(PdfFontFamily.Helvetica, 20), PdfBrushes.Red, new RectangleF(0, 0, 200, 50), new PdfStringFormat(PdfTextAlignment.Center, PdfVerticalAlignment.Middle));
//Adds the annotation to page 
lpage.Annotations.Add(watermark); 

//Saves the document to disk. 
loadedDocument.Save("WatermarkAnnotation.pdf"); 
loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Load the existing PDF document
 Dim loadedDocument As New PdfLoadedDocument("input.pdf")
'Get the page 
Dim lpage As PdfLoadedPage = TryCast(loadedDocument.Pages(0),PdfLoadedPage)

'Creates PDF watermark annotation
Dim watermark As New PdfWatermarkAnnotation(New RectangleF(50, 100, 100, 50)) 
watermark.Opacity = 0.5f; 
'Creates the appearance of watermark
watermark.Appearance.Normal.Graphics.DrawString("Watermark Text", New PdfStandardFont(PdfFontFamily.Helvetica, 20), PdfBrushes.Red, New RectangleF(0, 0, 200, 50), New PdfStringFormat(PdfTextAlignment.Center, PdfVerticalAlignment.Middle))
'Adds annotation to the page 
lpage.Annotations.Add(watermark)

'Saves the document to disk. 
loadedDocument.Save("WatermarkAnnotation.pdf")
loadedDocument.Close(True)

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Annotation/Add-watermark-annotation-in-the-PDF-document).


### Removing Watermark Annotation

You can remove the Watermark annotation from the annotation collection, represented by the [PdfLoadedAnnotationCollection](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedAnnotationCollection.html) of the loaded page. The following code illustrates this.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

    //Load the PDF document
    FileStream docStream = new FileStream("input.pdf", FileMode.Open, FileAccess.Read);
    PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);
    // Iterate through the annotations collection and remove PdfLoadedWatermark annotations
    foreach (PdfPageBase page in loadedDocument.Pages)
    {
        for (int i = page.Annotations.Count - 1; i >= 0; i--)
        {
            // Check if the annotation is a PdfLoadedWatermarkAnnotation
            if (page.Annotations[i] is PdfLoadedWatermarkAnnotation)
            {
                // Remove the PdfLoadedWatermarkAnnotation
                page.Annotations.RemoveAt(i);
            }
        }
    }

    //Save the document into stream
    MemoryStream stream = new MemoryStream();
    loadedDocument.Save(stream);
    //Close the document 
    loadedDocument.Close(true); 

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

    //Load the existing PDF document
    PdfLoadedDocument loadedDocument = new PdfLoadedDocument("input.pdf");
    // Iterate through the annotations collection and remove PdfLoadedWatermark annotations
    foreach (PdfPageBase page in loadedDocument.Pages)
    {
        for (int i = page.Annotations.Count - 1; i >= 0; i--)
        {
            // Check if the annotation is a PdfLoadedWatermarkAnnotation
            if (page.Annotations[i] is PdfLoadedWatermarkAnnotation)
            {
                // Remove the PdfLoadedWatermarkAnnotation
                page.Annotations.RemoveAt(i);
            }
        }
    } 

    //Saves the document to disk. 
    loadedDocument.Save("WatermarkAnnotation.pdf"); 
    loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

    'Load the existing PDF document
    Dim loadedDocument As New PdfLoadedDocument("input.pdf")
    ' Iterate through the annotations collection and remove PdfLoadedWatermark annotations
    For Each page As PdfPageBase In loadedDocument.Pages
        Dim i As Integer = page.Annotations.Count - 1
        While i >= 0
            ' Check if the annotation is a PdfLoadedWatermarkAnnotation
            If TypeOf page.Annotations(i) Is PdfLoadedWatermarkAnnotation Then
                ' Remove the PdfLoadedWatermarkAnnotation
                page.Annotations.RemoveAt(i)
            End If
            i -= 1
        End While
    Next

    'Saves the document to disk. 
    loadedDocument.Save("WatermarkAnnotation.pdf")
    loadedDocument.Close(True)

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Watermark/Removing-watermark-annotation-in-PDF-document).

