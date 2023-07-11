---
title: Working with image extraction | Syncfusion
description: This section explains extracting images and extracting information about images from PDF document using Essential PDF
platform: file-formats
control: PDF
documentation: UG
---
# Working with Image Extraction

The Essential PDF provides support to extract images from a particular page or an entire PDF document. You can extract the images from a page using the [ExtractImages](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfPageBase.html#Syncfusion_Pdf_PdfPageBase_ExtractImages().html) method in the [PdfPageBase](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfPageBase.html) class.

Refer to the following code snippet to extract the images from a PDF page.

{% tabs %}  

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Load an existing PDF
FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);
//Load the first page
PdfPageBase pageBase = loadedDocument.Pages[0];

//Extract images from first page
Stream[] extractedImages = pageBase.ExtractImages();
//Close the document
loadedDocument.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Load an existing PDF
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);
//Load the first page
PdfPageBase pageBase = loadedDocument.Pages[0];

//Extract images from first page
Image[] extractedImages = pageBase.ExtractImages();
//Close the document
loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Load an existing PDF
Dim loadedDocument As New PdfLoadedDocument(fileName)
'Load the first page
Dim pageBase As PdfPageBase = loadedDocument.Pages(0)

'Extract images from first page
Dim extractedImages As Image() = pageBase.ExtractImages()
'Close the document
loadedDocument.Close(True)

{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Image%20Extraction/Extract-images-from-a-PDF-pages/). 

N> To extract the images from PDF page in .NET Core, you need to include [Syncfusion.Pdf.Imaging.Portable](https://www.nuget.org/packages/Syncfusion.Pdf.Imaging.Net.Core) assembly reference in .NET Core project.

## Image informations

To extract the image properties such as bounds, image index, and more from a page, you can use the [ImagesInfo](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfPageBase.html#Syncfusion_Pdf_PdfPageBase_ImagesInfo) property in the [PdfPageBase](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfPageBase.html) class.

Refer to the following code snippet to extract the image info from a PDF page.

{% tabs %}  

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Load an existing PDF
FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);
//Load the first page
PdfPageBase pageBase = loadedDocument.Pages[0];

//Extracts all the images info from first page
PdfImageInfo[] imagesInfo= pageBase.GetImagesInfo();
//Close the document
loadedDocument.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Load an existing PDF
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);
//Load the first page
PdfPageBase pageBase = loadedDocument.Pages[0];

//Extracts all the images info from first page
PdfImageInfo[] imagesInfo= pageBase.ImagesInfo;
//Close the document
loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Load an existing PDF
Dim loadedDocument As New PdfLoadedDocument(fileName)
'Load the first page
Dim pageBase As PdfPageBase = loadedDocument.Pages(0)

'Extracts all the images info from first page
Dim imagesInfo As PdfImageInfo[] = pageBase.ImagesInfo
'Close the document
loadedDocument.Close(True)

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Image%20Extraction/Extract-the-image-info-from-a-PDF-page/). 

## Extract images from PDF documents with better memory consumption and performance

The following code example illustrates how to extract images from an entire PDF document using the [PdfDocumentExtractor](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfDocumentExtractor.html) class.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Get stream from an existing PDF document.
FileStream inputStream = new FileStream(@"Input.pdf", FileMode.Open, FileAccess.Read);
//Initialize the PDF document extractor.
PdfDocumentExtractor documentExtractor = new PdfDocumentExtractor();
//Load the PDF document.
documentExtractor.Load(inputStream);
//Get the page count.
int pageCount = documentExtractor.PageCount;
// Extract images from the PDF document.
Stream[] images = documentExtractor.ExtractImages();
// Extract images by page range.
Stream[] streams = documentExtractor.ExtractImages(2, 6);
// Release all resources used by the PDF image extractor.
documentExtractor.Dispose();

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Get stream from an existing PDF document.
FileStream inputStream = new FileStream(@"Input.pdf", FileMode.Open, FileAccess.Read);
//Initialize the PDF document extractor.
PdfDocumentExtractor documentExtractor = new PdfDocumentExtractor();
//Load the PDF document.
documentExtractor.Load(inputStream);
//Get the page count.
int pageCount = documentExtractor.PageCount;
// Extract images from the PDF document.
Stream[] images = documentExtractor.ExtractImages();
// Extract images by page range.
Stream[] streams = documentExtractor.ExtractImages(2, 6);
// Release all resources used by the PDF image extractor.
documentExtractor.Dispose();

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Get stream from an existing PDF document.
Dim inputStream As FileStream = New FileStream("Input.pdf", FileMode.Open, FileAccess.Read)
'Initialize the PDF document extractor.
Dim documentExtractor As PdfDocumentExtractor = New PdfDocumentExtractor()
'Load the PDF document.
documentExtractor.Load(inputStream)
'Get the page count.
Dim pageCount As Integer = documentExtractor.PageCount
'Extract images from the PDF document.
Dim images As Stream() = documentExtractor.ExtractImages()
'Extract images by page range.
Dim streams As Stream() = documentExtractor.ExtractImages(2, 6)
'Release all resources used by the PDF image extractor.
documentExtractor.Dispose()

{% endhighlight %}

{% endtabs %}

N> To extract the image information from PDF page in .NET Core, you need to include [Syncfusion.Pdf.Imaging.Portable](https://www.nuget.org/packages/Syncfusion.Pdf.Imaging.Net.Core) assembly reference in .NET Core project.
