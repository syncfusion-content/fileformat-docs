---
title: Working with Images | Syncfusion
description: This section explains how to add and replace images in the PDF document using Essential PDF. Essential PDF supports both raster and vector images.
platform: file-formats
control: PDF
documentation: UG
---

# Working with images using various options

Essential PDF supports both raster and vector images.

Images are supported through the [PdfImage](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfImage.html) class, which is an abstract base class that provides the common functionality for [PdfBitmap](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfBitmap.html) and [PdfMetafile](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfMetafile.html) classes.

## Inserting an image in a new document

The following raster images are supported in Essential PDF.

* BMP
* JPEG
* JPEG with Exif standard
* GIF
* PNG
* TIFF
* ICO and ICON

You can load image streams, files on disk, and use System.Drawing.Bitmap objects to draw the images through the [DrawImage](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfGraphics.html#Syncfusion_Pdf_Graphics_PdfGraphics_DrawImage_Syncfusion_Pdf_Graphics_PdfImage_System_Drawing_PointF_) method of the [PdfGraphics](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfGraphics.html) class.

The following code snippet shows how to add a file from disk to the PDF document.

{% tabs %}  

{% highlight c# tabtitle="C#" %}

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

{% highlight vb.net tabtitle="VB.NET" %}


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

{% highlight c# tabtitle="UWP" %}

//Create a new PDF document
PdfDocument doc = new PdfDocument();
//Add a page to the document
PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;
//Load the image as stream from the disk
Stream imageStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Autumn Leaves.jpg");
PdfBitmap image = new PdfBitmap(imageStream);
//Draw the image
graphics.DrawImage(image, 0, 0);

//Save the document as stream
MemoryStream stream = new MemoryStream();
await doc.SaveAsync(stream);
//Close the document
doc.Close(true);
//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

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

//Defining the ContentType for pdf file
string contentType = "application/pdf";
//Define the file name
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Create a new PDF document
PdfDocument doc = new PdfDocument();
//Add a page to the document
PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;
//Load the image as stream
Stream imageStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Autumn Leaves.jpg");
PdfBitmap image = new PdfBitmap(imageStream);
//Draw the image
graphics.DrawImage(image, 0, 0);

//Save the document as stream
MemoryStream stream = new MemoryStream();
doc.Save(stream);
//Close the document
doc.Close(true);

//Save the stream into pdf file
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %} 

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Images/Insert-image-in-a-new-PDF-document/). 

## Inserting an image in an existing document

You can also add images into an existing PDF document using the below code snippet.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Load a PDF document
PdfLoadedDocument doc = new PdfLoadedDocument("input.pdf");
//Get first page from document
PdfLoadedPage page = doc.Pages[0] as PdfLoadedPage;

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

{% highlight vb.net tabtitle="VB.NET" %}

'Load a PDF document
Dim doc As New PdfLoadedDocument("input.pdf")
'Get first page from document
Dim page As PdfLoadedPage = TryCast(doc.Pages(0), PdfLoadedPage)

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

{% highlight c# tabtitle="UWP" %}


//Create the file open picker
var picker = new FileOpenPicker();
picker.FileTypeFilter.Add(".pdf");
//Browse and chose the file
StorageFile file = await picker.PickSingleFileAsync();

//Creates an empty PDF loaded document instance
PdfLoadedDocument doc = new PdfLoadedDocument();
//Loads or opens an existing PDF document through Open method of PdfLoadedDocument class
await doc.OpenAsync(file);
//Get first page from document
PdfLoadedPage page = doc.Pages[0] as PdfLoadedPage;

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;
//Load the image as stream
Stream imageStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Autumn Leaves.jpg");
PdfBitmap image = new PdfBitmap(imageStream);
//Draw the image
graphics.DrawImage(image, 0, 0);

//Save the document as stream
MemoryStream stream = new MemoryStream();
await doc.SaveAsync(stream);
//Close the document
doc.Close(true);
//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load the PDF document
FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument doc = new PdfLoadedDocument(docStream);
//Get first page from document
PdfLoadedPage page = doc.Pages[0] as PdfLoadedPage;

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

//Defining the ContentType for pdf file
string contentType = "application/pdf";
//Define the file name
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Load the file as stream
Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.pdf");
PdfLoadedDocument doc = new PdfLoadedDocument(docStream);
//Get first page from document
PdfLoadedPage page = doc.Pages[0] as PdfLoadedPage;

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;
//Load the image as stream
Stream imageStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Autumn Leaves.jpg");
PdfBitmap image = new PdfBitmap(imageStream);
//Draw the image
graphics.DrawImage(image, 0, 0);

//Save the document as stream
MemoryStream stream = new MemoryStream();
doc.Save(stream);
//Close the document
doc.Close(true);
//Save the stream into pdf file
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}  

To add image from stream, use the below code snippet.

{% tabs %}  

{% highlight c# tabtitle="C#" %}

//Load a PDF document
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

//Save the document
doc.Save("Output.pdf");
//Close the document
doc.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Load a PDF document
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

'Save the document
doc.Save("Output.pdf")
'Close the document
doc.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Create the file open picker
var picker = new FileOpenPicker();
picker.FileTypeFilter.Add(".pdf")
//Browse and chose the file
StorageFile file = await picker.PickSingleFileAsync();

//Creates an empty PDF loaded document instance
PdfLoadedDocument doc = new PdfLoadedDocument();
//Loads or opens an existing PDF document through Open method of PdfLoadedDocument class
await doc.OpenAsync(file);
//Get first page from document
PdfLoadedPage page = doc.Pages[0] as PdfLoadedPage;

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;
//Load the image as stream
Stream imageStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Autumn Leaves.jpg");
PdfBitmap image = new PdfBitmap(imageStream);
//Draw the image
graphics.DrawImage(image, 0, 0);

//Save the document as stream
MemoryStream stream = new MemoryStream();
await doc.SaveAsync(stream);
//Close the document
doc.Close(true);
//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load the PDF document
FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument doc = new PdfLoadedDocument(docStream);
//Get first page from document
PdfLoadedPage page = doc.Pages[0] as PdfLoadedPage;

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

//Defining the ContentType for pdf file
string contentType = "application/pdf";
//Define the file name
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Load the file as stream
Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.pdf");
PdfLoadedDocument doc = new PdfLoadedDocument(docStream);
//Get first page from document
PdfLoadedPage page = doc.Pages[0] as PdfLoadedPage;

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;
//Load the image as stream
Stream imageStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Autumn Leaves.jpg");
PdfBitmap image = new PdfBitmap(imageStream);
//Draw the image
graphics.DrawImage(image, 0, 0);

//Save the document as stream
MemoryStream stream = new MemoryStream();
doc.Save(stream);
//Close the document
doc.Close(true);
//Save the stream into pdf file
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Images/Insert-image-in-an-existing-PDF-document/). 

## Inserting a vector image

Essential PDF supports adding Metafile vector image. During the insertion, Metafile graphics will be transformed to native PDF graphics that supports text selection and searching. The following types of Metafiles are supported in Essential PDF.

* EMF only 
* EMF plus
* EMF plus dual
* WMF

[PdfMetafile](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfMetafile.html) class is used to load EMF images. Additionally the [PdfMetafileLayoutFormat](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfMetafileLayoutFormat.html) class allows you to prevent text and image split across pages in the PDF document.

The following code illustrate this,

{% tabs %}  

{% highlight c# tabtitle="C#" %}

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

{% highlight vb.net tabtitle="VB.NET" %}

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

{% highlight c# tabtitle="UWP" %}

//PDF supports inserting a vector image only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//PDF supports inserting a vector image only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//PDF supports inserting a vector image only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Images/Insert-vector-image-in-a-PDF-document/). 

## Working with image masking

Essential PDF supports image masking through the [PdfImageMask](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfImageMask.html) class.

The following code illustrate shows how to add a mask to TIFF image.

{% tabs %}  

{% highlight c# tabtitle="C#" %}

//Create a PDF document
PdfDocument doc = new PdfDocument();
//Add pages to the document
PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;
//Load the TIFF image
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

{% highlight vb.net tabtitle="VB.NET" %}

'Create a PDF document
Dim doc As New PdfDocument()
'Add pages to the document
Dim page As PdfPage = doc.Pages.Add()

'Create PDF graphics for the page
Dim graphics As PdfGraphics = page.Graphics
'Load the TIFF image
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

{% highlight c# tabtitle="UWP" %}

//PDF supports image masking only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a PDF document
PdfDocument doc = new PdfDocument();
//Add pages to the document
PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;
//Load the TIFF image
FileStream imageStream = new FileStream("image.tif", FileMode.Open, FileAccess.Read);
PdfTiffImage image = new PdfTiffImage(imageStream);
//Create masking image
FileStream maskStream = new FileStream("mask.bmp", FileMode.Open, FileAccess.Read);
PdfImageMask mask = new PdfImageMask(new PdfTiffImage(maskStream));
image.Mask = mask;
//Draw the image
graphics.DrawImage(image, 0, 0);
///Creating the stream object

MemoryStream stream = new MemoryStream();
//Save the document as stream
doc.Save(stream);
//If the position is not set to '0' then the PDF will be empty
stream.Position = 0;
//Close the document
doc.Close(true);

//Defining the ContentType for pdf file
string contentType = "application/pdf";
//Define the file name
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//PDF supports image masking only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms

{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Images/Add-a-mask-to-TIFF-image/). 

N> 1. Essential PDF supports image masking with [Syncfusion.Pdf.Imaging.Portable](https://www.nuget.org/packages/Syncfusion.Pdf.Imaging.Net.Core) assembly reference in ASP.NET Core.


## Replacing Images in an existing PDF document

Essential PDF allows you to replace images in an existing document. The [ReplaceImage](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfPageBase.html#Syncfusion_Pdf_PdfPageBase_ReplaceImage_System_Int32_Syncfusion_Pdf_Graphics_PdfImage_) method of the page collection allows you to replace an image.

{% tabs %} 

{% highlight c# tabtitle="C#" %}

//Load the PDF document
PdfLoadedDocument doc = new PdfLoadedDocument(@"image.pdf");
//Create an image instance
PdfBitmap image = new PdfBitmap(@"Autumn Leaves.jpg");
//Replace the first image in the page
doc.Pages[0].ReplaceImage(0, image);

//Save the document
doc.Save("Output.pdf");
//Close the document
doc.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}


'Load the PDF document
Dim doc As New PdfLoadedDocument("image.pdf")
'Create an image instance
Dim image As New PdfBitmap("Autumn Leaves.jpg")
'Replace the first image in the page
doc.Pages(0).ReplaceImage(0, image)

'Save the document
doc.Save("Output.pdf")
'Close the document
doc.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//PDF supports replacing image in an existing PDF document only in Windows Forms, WPF,ASP.NET and ASP.NET MVC platforms.

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load an existing PDF document. 
FileStream pdfStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(pdfStream);

//Create an image instance.
FileStream imageStream = new FileStream(Path.GetFullPath("Autumn Leaves.jpg"), FileMode.Open, FileAccess.Read);
PdfBitmap bmp = new PdfBitmap(imageStream);
//Replace the first image in the page
loadedDocument.Pages[0].ReplaceImage(0, bmp);

MemoryStream stream = new MemoryStream();
//Save the document as stream
loadedDocument.Save(stream);
//If the position is not set to '0' then the PDF will be empty
stream.Position = 0;
//Close the document
loadedDocument.Close(true);
//Defining the ContentType for pdf file
string contentType = "application/pdf";
//Define the file name
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//PDF supports replacing image in an existing PDF document only in Windows Forms, WPF,ASP.NET and ASP.NET MVC platforms.

{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Images/Replace-image-in-an-existing-PDF-document/). 

## Image Pagination

You can allow a large image to paginate across multiple pages in the PDF document. This can be done through the [PdfLayoutFormat](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfLayoutFormat.html) class as shown below.

{% tabs %} 

{% highlight c# tabtitle="C#" %}

//Create Document
PdfDocument doc = new PdfDocument();
//Add new page
PdfPage page = doc.Pages.Add();

//Load a bitmap
PdfBitmap image = new PdfBitmap("input.jpg");
//Set layout property to make the element break across the pages
PdfLayoutFormat format = new PdfLayoutFormat();
format.Break = PdfLayoutBreakType.FitPage;
format.Layout = PdfLayoutType.Paginate;
//Draw image
image.Draw(page,20,400, format);

//Save the PDF
doc.Save("output.pdf");
doc.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create Document
Dim doc As New PdfDocument()
'Add new page
Dim page As PdfPage = doc.Pages.Add()

'Load a bitmap
Dim image As New PdfBitmap("input.jpg")
'Set layout property to make the element break across the pages
Dim format As New PdfLayoutFormat()
format.Break = PdfLayoutBreakType.FitPage
format.Layout = PdfLayoutType.Paginate
'Draw image
image.Draw(page, 20, 400, format)

'Save the PDF
doc.Save("output.pdf")
doc.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Create Document
PdfDocument doc = new PdfDocument();
//Add new page
PdfPage page = doc.Pages.Add();

//Load the image as stream
Stream imageStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Data.Assets.Autumn Leaves.jpg");
//Load a bitmap
PdfBitmap image = new PdfBitmap(imageStream);
//Set layout property to make the element break across the pages
PdfLayoutFormat format = new PdfLayoutFormat();
format.Break = PdfLayoutBreakType.FitPage;
format.Layout = PdfLayoutType.Paginate;
//Draw image
image.Draw(page, 20, 400, format);

//Save the document as stream
MemoryStream stream = new MemoryStream();
await doc.SaveAsync(stream);
//Close the document
doc.Close(true);
//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create Document
PdfDocument doc = new PdfDocument();
//Add new page
PdfPage page = doc.Pages.Add();

//Load a bitmap
FileStream imageStream = new FileStream("Autumn Leaves.jpg", FileMode.Open, FileAccess.Read);
PdfBitmap image = new PdfBitmap(imageStream);
//Set layout property to make the element break across the pages
PdfLayoutFormat format = new PdfLayoutFormat();
format.Break = PdfLayoutBreakType.FitPage;
format.Layout = PdfLayoutType.Paginate;
//Draw image
image.Draw(page, 20, 400, format);

//Creating the stream object
MemoryStream stream = new MemoryStream();
//Save the document as stream
doc.Save(stream);
//If the position is not set to '0' then the PDF will be empty
stream.Position = 0;
//Close the document
doc.Close(true);

//Defining the ContentType for pdf file
string contentType = "application/pdf";
//Define the file name
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Create Document
PdfDocument doc = new PdfDocument();
//Add new page
PdfPage page = doc.Pages.Add();

//Load a bitmap
Stream imageStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Autumn Leaves.jpg");
PdfBitmap image = new PdfBitmap(imageStream);
//Set layout property to make the element break across the pages
PdfLayoutFormat format = new PdfLayoutFormat();
format.Break = PdfLayoutBreakType.FitPage;
format.Layout = PdfLayoutType.Paginate;
//Draw image
image.Draw(page, 20, 400, format);

//Save the document as stream
MemoryStream stream = new MemoryStream();
doc.Save(stream);
//Close the document
doc.Close(true);
//Save the stream into pdf file
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}  
 
You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Images/Paginate-an-image-in-PDF-document). 

## Applying transparency and rotation to the image

You can add transparency and rotation to the image using [SetTransparency](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfGraphics.html#Syncfusion_Pdf_Graphics_PdfGraphics_SetTransparency_System_Single_) and [RotateTransform](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfGraphics.html#Syncfusion_Pdf_Graphics_PdfGraphics_RotateTransform_System_Single_) methods of [PdfGraphics](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfGraphics.html) respectively. This is explained in the below code snippet.

{% tabs %}  

{% highlight c# tabtitle="C#" %}

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
//Draw image
image.Draw(page, 0, 0);
//Restore the graphics state
page.Graphics.Restore(state);

//Save the PDF
doc.Save("output.pdf");
doc.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

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

{% highlight c# tabtitle="UWP" %}

//Create Document
PdfDocument doc = new PdfDocument();
//Add new page
PdfPage page = doc.Pages.Add();

//Load the image as stream
Stream imageStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Data.Assets.input.jpg");
//Load a bitmap
PdfBitmap image = new PdfBitmap(imageStream);
//save the current graphics state
PdfGraphicsState state = page.Graphics.Save();
//Translate the coordinate system to the  required position
page.Graphics.TranslateTransform(20, 100);
//Apply transparency
page.Graphics.SetTransparency(0.5f);
//Rotate the coordinate system
page.Graphics.RotateTransform(-45);
//Draw image
image.Draw(page, 0, 0);
//Restore the graphics state
page.Graphics.Restore(state);

//Save the document as stream
MemoryStream stream = new MemoryStream();
await doc.SaveAsync(stream);
//Close the document
doc.Close(true);
//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create Document

PdfDocument doc = new PdfDocument();
//Add a new page
PdfPage page = doc.Pages.Add();

//Load a image as stream
FileStream imageStream = new FileStream("input.jpg", FileMode.Open, FileAccess.Read);
//Load a bitmap
PdfBitmap image = new PdfBitmap(imageStream);
//save the current graphics state
PdfGraphicsState state = page.Graphics.Save();
//Translate the coordinate system to the  required position
page.Graphics.TranslateTransform(20, 100);
//Apply transparency
page.Graphics.SetTransparency(0.5f);
//Rotate the coordinate system
page.Graphics.RotateTransform(-45);
//Draw image
image.Draw(page, 0, 0);
//Restore the graphics state
page.Graphics.Restore(state);

//Creating the stream object
MemoryStream stream = new MemoryStream();
//Save the document as strea
doc.Save(stream);
//If the position is not set to '0' then the PDF will be empty
stream.Position = 0;
//Close the document
doc.Close(true);

//Defining the ContentType for pdf file
string contentType = "application/pdf";
//Define the file name
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Create Document
PdfDocument doc = new PdfDocument();
//Add a new page
PdfPage page = doc.Pages.Add();

//Load a bitmap
Stream imageStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.jpg");
PdfBitmap image = new PdfBitmap(imageStream);
//save the current graphics state
PdfGraphicsState state = page.Graphics.Save();
//Translate the coordinate system to the  required position
page.Graphics.TranslateTransform(20, 100);
//Apply transparency
page.Graphics.SetTransparency(0.5f);
//Rotate the coordinate system
page.Graphics.RotateTransform(-45);
//Draw image
image.Draw(page, 0, 0);
//Restore the graphics state
page.Graphics.Restore(state);

//Save the document as stream
MemoryStream stream = new MemoryStream();
doc.Save(stream);
//Close the document
doc.Close(true);
//Save the stream into pdf file
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Images/Add-transparancy-and-rotation-to-the-image/). 

## Converting multi page TIFF to PDF

Multi frame TIFF image can be converted to PDF document. This can be done by accessing each frame of the multi frame TIFF image and rendering it in each page of the PDF document using [PdfBitmap](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfBitmap.html) class.

The code snippet to illustrate the same is given below.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Create a PDF document
PdfDocument pdfDocument = new PdfDocument();
//Set page margins
pdfDocument.PageSettings.Margins.All = 0;

//Load multi frame TIFF image
PdfBitmap tiffImage = new PdfBitmap("image.tiff");
//Get the frame count
int frameCount = tiffImage.FrameCount;
//Access each frame and draw into the page
for (int i = 0; i < frameCount; i++)
{
PdfPage page = pdfDocument.Pages.Add();
PdfGraphics graphics = page.Graphics;
tiffImage.ActiveFrame = i;
graphics.DrawImage(tiffImage, 0, 0, page.GetClientSize().Width, page.GetClientSize().Height);
}

//Save and close the document
pdfDocument.Save("Sample.pdf");
pdfDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a PDF document
Dim pdfDocument As New PdfDocument()
'Set page margins
pdfDocument.PageSettings.Margins.All = 0

'Load multi frame TIFF image
Dim tiffImage As New PdfBitmap("image.tiff")
'Get the frame count
Dim frameCount As Integer = tiffImage.FrameCount
'Access each frame and draw into the page
For i As Integer = 0 To frameCount - 1
Dim page As PdfPage = pdfDocument.Pages.Add()
Dim graphics As PdfGraphics = page.Graphics
tiffImage.ActiveFrame = i
graphics.DrawImage(tiffImage, 0, 0, page.GetClientSize().Width, page.GetClientSize().Height)
Next

'Save and close the document
pdfDocument.Save("Sample.pdf")
pdfDocument.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Create a PDF document
PdfDocument pdfDocument = new PdfDocument();
//Set page margins
pdfDocument.PageSettings.Margins.All = 0;

//Load multi frame TIFF image
Stream imageStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.image.tiff");
PdfBitmap tiffImage = new PdfBitmap(imageStream);
//Get the frame count
int frameCount = tiffImage.FrameCount;
//Access each frame and draw into the page
for (int i = 0; i < frameCount; i++)
{
    PdfPage page = pdfDocument.Pages.Add();
    PdfGraphics graphics = page.Graphics;
    tiffImage.ActiveFrame = i;
    graphics.DrawImage(tiffImage, 0, 0, page.GetClientSize().Width, page.GetClientSize().Height);
}

MemoryStream memoryStream = new MemoryStream();
//Save the document
await pdfDocument.SaveAsync(memoryStream);
//Close the documents
pdfDocument.Close(true);
//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples
Save(memoryStream, "Sample.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a new PDF document

PdfDocument doc = new PdfDocument();
//Set page margins
doc.PageSettings.Margins.All = 0;

//Load the multi frame TIFF image from the disk
FileStream imageStream = new FileStream("image.tiff", FileMode.Open, FileAccess.Read);
PdfTiffImage tiffImage = new PdfTiffImage(imageStream);
//Get the frame count
int frameCount = tiffImage.FrameCount;
//Access each frame and draw into the page
for (int i = 0; i < frameCount; i++)
{
    PdfPage page = doc.Pages.Add();
    PdfGraphics graphics = page.Graphics;
    tiffImage.ActiveFrame = i;
    graphics.DrawImage(tiffImage, 0, 0, page.GetClientSize().Width, page.GetClientSize().Height);
}

//Creating the stream object
MemoryStream stream = new MemoryStream();
//Save the document as stream
doc.Save(stream);
//If the position is not set to '0' then the PDF will be empty
stream.Position = 0;
//Close the document
doc.Close(true);

//Defining the ContentType for pdf file
string contentType = "application/pdf";
//Define the file name
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}


//Essential PDF supports converting multi page TIFF to PDF only in Windows Forms, WPF, ASP.NET, ASP.NET MVC and UWP platforms.

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Images/Converting-multi-page-TIFF-to-PDF). 

N> 1. Essential PDF supports converting TIFF to PDF with [Syncfusion.Pdf.Imaging.Portable](https://www.nuget.org/packages/Syncfusion.Pdf.Imaging.Net.Core) assembly reference in ASP.NET Core.

## Remove Images

The [RemoveImage](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfPageBase.html#Syncfusion_Pdf_PdfPageBase_RemoveImage_Syncfusion_Pdf_Exporting_PdfImageInfo_) method of the page collection allows you to remove an image. You can remove images from an existing document using Essential PDF.

The code snippet to illustrate the same is given below.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Load a PDF document
PdfLoadedDocument doc = new PdfLoadedDocument("input.pdf");
//Load the first page
PdfPageBase pageBase = doc.Pages[0];
//Extract images from the first page
PdfImageInfo imageInfo = pageBase.ImagesInfo[0];
//Remove the Image
pageBase.RemoveImage(imageInfo);

//Save the document
doc.Save("Output.pdf");
//Close the document
doc.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Load an existing PDF 
Dim loadedDocument As PdfLoadedDocument = New PdfLoadedDocument("input.pdf") 
'Load the first page 
Dim pageBase As PdfPageBase = loadedDocument.Pages(0)
'Extract images from the first page
Dim imageInfo As PdfImageInfo = pageBase.ImagesInfo(0)
'Remove the Image
pageBase.RemoveImage(imageInfo)
Dim stream As New MemoryStream()

'Save the document
loadedDocument.Save(stream) 
'Close the document
loadedDocument.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Essential PDF supports remove image from the existing PDF document only in Windows Forms, WPF, ASP.NET, ASP.NET MVC platforms.

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load an existing PDF.
FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);
//Load the first page.
PdfPageBase pageBase = loadedDocument.Pages[0];
//Extract images from the first page.
PdfImageInfo[] imageInfo = loadedDocument.Pages[0].GetImagesInfo();
//Remove the Image.
pageBase.RemoveImage(imageInfo[0]);
//Create the stream object
MemoryStream stream = new MemoryStream();

//Save the document into stream
loadedDocument.Save(stream);
//If the position is not set to '0' then the PDF will be empty
stream.Position = 0;
//Close the document
loadedDocument.Close(true);

//Define the ContentType for pdf file
string contentType = "application/pdf";
//Define the file name
string fileName = "Output.pdf";
//Create a FileContentResult object by using the file contents, content type and file name
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Essential PDF supports remove image from the existing PDF document only in Windows Forms, WPF, ASP.NET, ASP.NET MVC platforms.

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Images/Remove-images-from-PDF-document). 

N> 1. Essential PDF supports remove image from the existing PDF document with [Syncfusion.Pdf.Imaging.Portable](https://www.nuget.org/packages/Syncfusion.Pdf.Imaging.Net.Core) assembly reference in ASP.NET Core.