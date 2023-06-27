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

N> To extract the image information from PDF page in .NET Core, you need to include [Syncfusion.Pdf.Imaging.Portable](https://www.nuget.org/packages/Syncfusion.Pdf.Imaging.Net.Core) assembly reference in .NET Core project.
