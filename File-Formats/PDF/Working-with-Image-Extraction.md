---
title: Working with image extraction | Syncfusion
description: This section explains extracting images and extracting information about images from PDF document using Essential PDF
platform: file-formats
control: PDF
documentation: UG
---
# Working with Image Extraction

Essential PDF provides the support to extract images from a particular page or an entire PDF document. You can extract the images from a page using the [ExtractImages](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Base~Syncfusion.Pdf.PdfPageBase~ExtractImages().html) method in the [PdfPageBase](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Base~Syncfusion.Pdf.PdfPageBase.html) class.

Refer to the following code snippet to extract the images from a PDF page.

{% tabs %}  

{% highlight c# %}


//Load an existing PDF

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);

//Load the first page

PdfPageBase pageBase = loadedDocument.Pages[0];

//Extract images from first page

Image[] extractedImages = pageBase.ExtractImages();

//Close the document

loadedDocument.Close(true);





{% endhighlight %}

{% highlight vb.net %}


'Load an existing PDF

Dim loadedDocument As New PdfLoadedDocument(fileName)

'Load the first page

Dim pageBase As PdfPageBase = loadedDocument.Pages(0)

'Extract images from first page

Dim extractedImages As Image() = pageBase.ExtractImages()

'Close the document

loadedDocument.Close(True)





{% endhighlight %}

{% highlight UWP %}

//PDF supports extracting the images from PDF document only in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms

{% endhighlight %}

{% highlight ASP.NET Core %}

PDF supports extract the images from PDF document only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

{% endhighlight %}

{% highlight Xamarin %}

//PDF supports extracting the images from PDF document only in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms

{% endhighlight %}

{% endtabs %}  


## Image informations

To extract the image properties such as bounds, image index, and more from a page, you can use the [ImagesInfo](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Base~Syncfusion.Pdf.PdfPageBase~ImagesInfo.html) property in the [PdfPageBase](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Base~Syncfusion.Pdf.PdfPageBase.html) class.

Refer to the following code snippet to extract the image info from a PDF page.

{% tabs %}  

{% highlight c# %}


//Load an existing PDF

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);

//Load the first page

PdfPageBase pageBase = loadedDocument.Pages[0];

//Extracts all the images info from first page

PdfImageInfo[] imagesInfo= pageBase.ImagesInfo;

//Close the document

loadedDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Load an existing PDF

Dim loadedDocument As New PdfLoadedDocument(fileName)

'Load the first page

Dim pageBase As PdfPageBase = loadedDocument.Pages(0)

'Extracts all the images info from first page

Dim imagesInfo As PdfImageInfo() = pageBase.ImagesInfo

'Close the document

loadedDocument.Close(True)



{% endhighlight %}

{% highlight UWP %}

//PDF supports extracting the images from PDF document only in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms

{% endhighlight %}

{% highlight ASP.NET Core %}

//PDF supports extract the images from PDF document only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

{% endhighlight %}

{% highlight Xamarin %}

//PDF supports extracting the image information from PDF document only in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms

{% endhighlight %}

{% endtabs %}
