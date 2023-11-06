---
title: Working with Watermarks | Syncfusion
description: This section explains how to add text and image watermarks to the newly PDF document and to an existing PDF document using Syncfusion .NET PDF library.
platform: file-formats
control: PDF
documentation: UG
---
# Working with Watermarks

The Essential PDF provides support to add watermark or stamp with text and images in the PDF document.

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
