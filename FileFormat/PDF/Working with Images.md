---
layout: post
title: Working with Images
description: Working with images using Essential PDF- PdfImage; pdfMetafile; PdfImagemask,Image Pagination
platform: FileFormat
control: PDF
documentation: UG
---
# 

# Working with Images

Essential PDF supports both raster and vector images.

Images are supported through the **PdfImage** class, which is an abstract base class that provides the common functionality for **PdfBitmap** and **PdfMetafile** classes.

## Inserting a raster image

The following raster images are supported in Essential PDF.

* Bmp
* Jpeg
* Gif
* Png
* Tiff

You can load image streams, files on disk, and use System.Drawing.Bitmap objects to draw the images through the **DrawImage** method of the **PdfGraphics** class.

The following code snippet shows how to add a file from disk to the PDF document.

{% highlight c# %}
[C#]



//Create a new PDF document.

PdfDocument doc = new PdfDocument();

//Add a page to the document.

PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page

PdfGraphics graphics = page.Graphics;

//Load the image from the disk.

PdfBitmap image = new PdfBitmap("Autumn Leaves.jpg");

//Draw the image

graphics.DrawImage(image, 0, 0);

//Save the document.

doc.Save("Output.pdf");

//Close the document.

doc.Close(true);



{% endhighlight %}



{% highlight vb.net %}
[VB.NET]



'Create a new PDF document.

Dim doc As New PdfDocument()

'Add a page to the document.

Dim page As PdfPage = doc.Pages.Add()

'Create PDF graphics for the page

Dim graphics As PdfGraphics = page.Graphics

'Load the image from the disk.

Dim image As New PdfBitmap("Autumn Leaves.jpg")

'Draw the image

graphics.DrawImage(image, 0, 0)

'Save the document.

doc.Save("Output.pdf")

'Close the document.

doc.Close(True)



{% endhighlight %}

You can also add images into an existing PDF document using the below code snippet.

{% highlight c# %}
[C#]



//Load a PDF document.

PdfLoadedDocument doc = new PdfLoadedDocument("input.pdf");

//Get first page from document

PdfLoadedPage page = doc.Pages[0] as PdfLoadedPage;

//Create PDF graphics for the page

PdfGraphics graphics = page.Graphics;

//Load the image from the disk

PdfBitmap image = new PdfBitmap("Autumn Leaves.jpg");

//Draw the image

graphics.DrawImage(image, 0, 0);

//Save the document.

doc.Save("Output.pdf");

//Close the document.

doc.Close(true);





{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Load a PDF document.

Dim doc As New PdfLoadedDocument("input.pdf")

'Get first page from document

Dim page As PdfLoadedPage = TryCast(doc.Pages(0), PdfLoadedPage)

'Create PDF graphics for the page

Dim graphics As PdfGraphics = page.Graphics

'Load the image from the disk

Dim image As New PdfBitmap("Autumn Leaves.jpg")

'Draw the image

graphics.DrawImage(image, 0, 0)

'Save the document.

doc.Save("Output.pdf")

'Close the document.

doc.Close(True)





{% endhighlight %}

To add image from stream, use the below code snippet.

{% highlight c# %}
[C#]



//Load a PDF document.

PdfLoadedDocument doc = new PdfLoadedDocument("input.pdf");

//Get first page from document

PdfLoadedPage page = doc.Pages[0] as PdfLoadedPage;

//Create PDF graphics for the page

PdfGraphics graphics = page.Graphics;

//Load the image

Stream imageStream = File.OpenRead("Autumn Leaves.jpg");

//Load the image from the stream

PdfBitmap image = new PdfBitmap(imageStream);

//Draw the image

graphics.DrawImage(image, 0, 0);

//Save the document.

doc.Save("Output.pdf");

//Close the document.

doc.Close(true);





{% endhighlight %}

{% highlight vb.net %}
[VB.NET]



'Load a PDF document.

Dim doc As New PdfLoadedDocument("input.pdf")

'Get first page from document

Dim page As PdfLoadedPage = TryCast(doc.Pages(0), PdfLoadedPage)

'Create PDF graphics for the page

Dim graphics As PdfGraphics = page.Graphics

'Load the image

Dim imageStream As Stream = File.OpenRead("Autumn Leaves.jpg")

'Load the image from the stream

Dim image As New PdfBitmap(imageStream)

'Draw the image

graphics.DrawImage(image, 0, 0)

'Save the document.

doc.Save("Output.pdf")

'Close the document.

doc.Close(True)



{% endhighlight %}

## Inserting a vector image

Essential PDF supports adding metafile vector image. During the insertion, metafile graphics will be transformed to native PDF graphics that supports text selection and searching. The following types of metafiles are supported in Essential PDF.

* EMF only 
* EMF plus
* EMF plus dual

**PdfMetafile** class is used to load EMF images. Additionally the PdfMetafileLayoutFormat class allows you to prevent text and image split across pages in the PDF document.

The following code illustrate this,

{% highlight c# %}
[C#]



// Create a PDF Document.

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

//Create a metafile instance

PdfMetafile metafile = new PdfMetafile("metachart.emf");

//Draw the metafile in the page

metafile.Draw(page, PointF.Empty, format);

//Save the document

doc.Save("Output.pdf");

//Close the document

doc.Close(true);





{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Create a PDF Document.

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

'Create a metafile instance

Dim metafile As New PdfMetafile("metachart.emf")

'Draw the metafile in the page

metafile.Draw(page, PointF.Empty, format)

'Save the document

doc.Save("Output.pdf")

'Close the document

doc.Close(True)





{% endhighlight %}

## Working with image masking

Essential PDF supports image masking through the PdfImageMask class.

The following code illustrate shows how to add a mask to TIFF image.

{% highlight c# %}
[C#]



//Create a PDF document

PdfDocument doc = new PdfDocument();

//Add pages to the document

PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page

PdfGraphics graphics = page.Graphics;

//Load the Tiff image

PdfBitmap image = new PdfBitmap("image.tif");

//Create masking image

PdfImageMask mask = new PdfImageMask(new PdfBitmap("mask.bmp"));

image.Mask = mask;

//Draw the image

graphics.DrawImage(image, 0, 0);

//Saves the document

doc.Save("Output.pdf");

//Close the document

doc.Close(true);



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Create a PDF document

Dim doc As New PdfDocument()

'Add pages to the document

Dim page As PdfPage = doc.Pages.Add()

'Create PDF graphics for the page

Dim graphics As PdfGraphics = page.Graphics

'Load the Tiff image

Dim image As New PdfBitmap("image.tif")

'Create masking image

Dim mask As New PdfImageMask(New PdfBitmap("mask.bmp"))

image.Mask = mask

'Draw the image

graphics.DrawImage(image, 0, 0)

'Saves the document

doc.Save("Output.pdf")

'Close the document

doc.Close(True)



{% endhighlight %}

## Replacing Images in an existing PDF document

Essential PDF allows you to replace images in an existing document. The **ReplaceImage** method of the page collection allows you to replace an image.

{% highlight c# %}
[C#]

//Load the PDF document

PdfLoadedDocument doc = new PdfLoadedDocument(@"image.pdf");

//Create an image instance

PdfBitmap bmp = new PdfBitmap(@"Autumn Leaves.jpg");

//Replace the first image in the page.

doc.Pages[0].ReplaceImage(0, bmp);

//Save the document

doc.Save("Output.pdf");

//Close the document

doc.Close(true);





{% endhighlight %}



{% highlight vb.net %}
[VB.NET]



'Load the PDF document

Dim doc As New PdfLoadedDocument("image.pdf")

'Create an image instance

Dim bmp As New PdfBitmap("Autumn Leaves.jpg")

'Replace the first image in the page.

doc.Pages(0).ReplaceImage(0, bmp)

'Save the document

doc.Save("Output.pdf")

'Close the document

doc.Close(True)





{% endhighlight %}

## Image Pagination

You can allow a large image to paginate across multiple pages in the PDF document. This can be done through the **PdfLayoutFormat** class as shown below.

{% highlight c# %}
[C#]

//Create Document

PdfDocument doc = new PdfDocument();

//Add new page

PdfPage page = doc.Pages.Add();

//Load a bitmap

PdfBitmap image = new PdfBitmap("input.jpg");

//Set layout property to make the element break across the pages.

PdfLayoutFormat format = new PdfLayoutFormat();

format.Break = PdfLayoutBreakType.FitPage;

format.Layout = PdfLayoutType.Paginate;

//Draw image

image.Draw(page,20,400, format);

//Save the PDF

doc.Save("output.pdf");

doc.Close(true);



{% endhighlight %}



{% highlight vb.net %}
[VB.NET]

'Create Document

Dim doc As New PdfDocument()

'Add new page

Dim page As PdfPage = doc.Pages.Add()

'Load a bitmap

Dim image As New PdfBitmap("input.jpg")

'Set layout property to make the element break across the pages.

Dim format As New PdfLayoutFormat()

format.Break = PdfLayoutBreakType.FitPage

format.Layout = PdfLayoutType.Paginate

'Draw image

image.Draw(page, 20, 400, format)

'Save the PDF

doc.Save("output.pdf")

doc.Close(True)



{% endhighlight %}

## Applying transparency and rotation to the image

You can add transparency and rotation to the image. This is explained in the below code snippet.

{% highlight c# %}
[C#]

//Create Document

PdfDocument doc = new PdfDocument();

//Add a new page

PdfPage page = doc.Pages.Add();

//Load a bitmap

PdfBitmap image = new PdfBitmap("input.jpg");

//save the current graphics state

PdfGraphicsState state = page.Graphics.Save();

//Translate the coordinate system to the  required position

page.Graphics.TranslateTransform(20, 100);

//Apply transparency

page.Graphics.SetTransparency(0.5f);

//Rotate the coordinate system

page.Graphics.RotateTransform(-45);

// Draw image

image.Draw(page, 0, 0);

//Restore the graphics state

page.Graphics.Restore(state);

//Save the PDF

doc.Save("output.pdf");

doc.Close(true);





{% endhighlight %}



{% highlight vb.net %}
[VB.NET]

'Create Document

Dim doc As New PdfDocument()

'Add a new page

Dim page As PdfPage = doc.Pages.Add()

'Load a bitmap

Dim image As New PdfBitmap("input.jpg")

'save the current graphics state

Dim state As PdfGraphicsState = page.Graphics.Save()

'Translate the coordinate system to the  required position

page.Graphics.TranslateTransform(20, 100)

'Apply transparency

page.Graphics.SetTransparency(0.5F)

'Rotate the coordinate system

page.Graphics.RotateTransform(-45)

' Draw image

image.Draw(page, 0, 0)

'Restore the graphics state

page.Graphics.Restore(state)

'Save the PDF

doc.Save("output.pdf")

doc.Close(True)





{% endhighlight %}

