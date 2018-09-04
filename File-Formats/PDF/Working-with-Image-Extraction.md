---
title: Working with image extraction
description: This section explains extracting image from PDF document using Essential PDF
platform: file-formats
control: PDF
documentation: UG
---
# Working with image extraction

Essential PDF provides the support to extract images from a particular page or an entire PDF document.You can extract the images from a page using the ExtractImages method in the PdfPageBase class.

Please refer the below code snippet to extract the images from a PDF page.

{% tabs %}  

{% highlight c# %}


//Load an existing PDF.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);

//Load first page.

PdfPageBase pageBase = loadedDocument.Pages[0];

//Extract images from first page.

Image[] extractedImages = pageBase.ExtractImages();

//close the document

loadedDocument.Close(true);





{% endhighlight %}

{% highlight vb.net %}


'Load an existing PDF.

Dim loadedDocument As New PdfLoadedDocument(fileName)

'Load first page.

Dim pageBase As PdfPageBase = loadedDocument.Pages(0)

'Extract images from first page.

Dim extractedImages As Image() = pageBase.ExtractImages()

'close the document.

loadedDocument.Close(True)





{% endhighlight %}

{% highlight UWP %}

//PDF supports extract the images from PDF document only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

{% endhighlight %}

{% highlight ASP.NET Core %}

//PDF supports extract the images from PDF document only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

{% endhighlight %}

{% highlight Xamarin %}

//PDF supports extract the images from PDF document only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

{% endhighlight %}

{% endtabs %}  


## Image informations

To extract the image properties like bounds, image index etc. from a page, you can use ImageInfo property in the PdfPageBase class.

Please refer the below code snippet to extract the image info from PDF page.

{% tabs %}  

{% highlight c# %}


//Load an existing PDF.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);

//Load the first page.

PdfPageBase pageBase = loadedDocument.Pages[0];

//Extracts all the images info from first page.

PdfImageInfo[] imagesInfo= pageBase.ImagesInfo;

//Close the document

loadedDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Load an existing PDF.

Dim loadedDocument As New PdfLoadedDocument(fileName)

'Load first page.

Dim pageBase As PdfPageBase = loadedDocument.Pages(0)

'Extracts all the images info from first page.

Dim imagesInfo As PdfImageInfo() = pageBase.ImagesInfo

'Close the document.

loadedDocument.Close(True)



{% endhighlight %}

{% highlight UWP %}

//PDF supports extract the images from PDF document only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

{% endhighlight %}

{% highlight ASP.NET Core %}

//PDF supports extract the images from PDF document only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

{% endhighlight %}

{% highlight Xamarin %}

//PDF supports extract the images from PDF document only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

{% endhighlight %}

{% endtabs %}  