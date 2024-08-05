---
title: Converting images to PDF | Syncfusion
description: This section explains how to convert both raster and vector images to PDF document using Syncfusion .NET PDF library. 
platform: file-formats
control: PDF
documentation: UG
---

# Converting images to PDF in .NET

The Syncfusion .NET PDF library provides comprehensive support for converting both raster and vector images to PDF documents. The [PdfImage](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfImage.html) class is an abstract base class that provides common functionality for converting images to PDF documents. It is used as the base class for two concrete image classes in the Syncfusion.Pdf.Graphics namespace: [PdfBitmap](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfBitmap.html) and [PdfMetafile](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfMetafile.html).

This includes a wide range of image formats for PDF conversion. These image formats includes:
* JPEG (Joint Photographic Experts Group) 
* JPEG with Exif standard
* PNG (Portable Network Graphics)
* BMP (Windows Bitmap)
* GIF (Graphics Interchange Format)
* TIFF (Tagged Image File Format)
* EMF (Enhanced Metafile) 
* ICO and ICON (Windows Icon)

You can load images from various sources, including image streams and files on disk using [PdfBitmap](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfBitmap.html) class. Once you have loaded an image, you can draw it on a PDF document using the [DrawImage](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfGraphics.html#Syncfusion_Pdf_Graphics_PdfGraphics_DrawImage_Syncfusion_Pdf_Graphics_PdfImage_System_Drawing_PointF_) method of the [PdfGraphics](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfGraphics.html) class.

The following code example shows how to convert image to PDF document. 

{% tabs %}  

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Create a new PDF document
PdfDocument doc = new PdfDocument();
//Add a page to the document
PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;
//Load the image from the disk
FileStream imageStream = new FileStream("Autumn Leaves.jpg", FileMode.Open, FileAccess.Read);
PdfBitmap image = new PdfBitmap(imageStream);
//Draw the image
graphics.DrawImage(image, 0, 0);

//Creating the stream object
MemoryStream stream = new MemoryStream();
//Save the document as stream
doc.Save(stream);
//If the position is not set to '0' then the PDF will be empty
stream.Position = 0;
//Close the document
doc.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Create a new PDF document
PdfDocument doc = new PdfDocument();
//Add a page to the document
PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;
//Load the image from the disk
PdfBitmap image = new PdfBitmap("Autumn Leaves.jpg");
//Draw the image
graphics.DrawImage(image, 0, 0);

//Save the document
doc.Save("Output.pdf");
//Close the document
doc.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Create a new PDF document
Dim doc As New PdfDocument()
'Add a page to the document
Dim page As PdfPage = doc.Pages.Add()

'Create PDF graphics for the page
Dim graphics As PdfGraphics = page.Graphics
'Load the image from the disk
Dim image As New PdfBitmap("Autumn Leaves.jpg")
'Draw the image
graphics.DrawImage(image, 0, 0)

'Save the document
doc.Save("Output.pdf")
'Close the document
doc.Close(True)

{% endhighlight %}

{% endtabs %} 

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Images/Insert-image-in-a-new-PDF-document/). 

N> The Syncfusion .NET Core PDF library supports converting TIFF to PDF with [Syncfusion.Pdf.Imaging.Net.Core](https://www.nuget.org/packages/Syncfusion.Pdf.Imaging.Net.Core) NuGet package in ASP.NET Core platform. 


## Converting vector image to PDF

The Syncfusion .NET PDF library supports adding vector images in the Metafile format to PDF documents.During the conversion, Metafile graphics will be transformed to native PDF graphics that supports text selection and searching. The following types of Metafiles are supported in Essential PDF.
* EMF only
* EMF plus
* EMF plus dual
* WMF

The [PdfMetafile](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfMetafile.html) class is used to load EMF images and additionally the [PdfMetafileLayoutFormat](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfMetafileLayoutFormat.html) class allows you to prevent text/image split across pages in the PDF document. The following code example illustrate this. 

{% tabs %}  

{% highlight c# tabtitle="C# [Cross-platform]" %}

//PDF doesn't support inserting a vector image C#.NET Cross platforms.

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Create a PDF Document
PdfDocument doc = new PdfDocument();
//Add pages to the document
PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;
//Create the layout format
PdfMetafileLayoutFormat format = new PdfMetafileLayoutFormat();
//Split text and image between pages
format.SplitImages = true;
format.SplitTextLines = true;
//Create a Metafile instance
PdfMetafile metaChart = new PdfMetafile("MetaChart.emf");
//Draw the Metafile in the page
metaChart.Draw(page, PointF.Empty, format);

//Save the document
doc.Save("Output.pdf");
//Close the document
doc.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Create a PDF Document
Dim doc As New PdfDocument()
'Add pages to the document
Dim page As PdfPage = doc.Pages.Add()

'Create PDF graphics for the page
Dim graphics As PdfGraphics = page.Graphics
'Create the layout format
Dim format As New PdfMetafileLayoutFormat()
'Split text and image between pages
format.SplitImages = True
format.SplitTextLines = True
'Create a Metafile instance
Dim metaChart As New PdfMetafile("MetaChart.emf")
'Draw the Metafile in the page
metaChart.Draw(page, PointF.Empty, format)

'Save the document
doc.Save("Output.pdf")
'Close the document
doc.Close(True)

{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Images/Insert-vector-image-in-a-PDF-document/). 

N> EMF and WMF images are not supported in the ASP.NET Core platform.



