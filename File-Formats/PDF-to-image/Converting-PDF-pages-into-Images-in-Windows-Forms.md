---
title: Converting PDF pages into images in Windows Forms| Syncfusion;
description: Learn about Converting PDF pages into images in Windows Forms with easy steps using Syncfusion<sup>&reg;</sup>; PdfToImageConverter library.
platform: file-formats
control: PDF to image
documentation: UG
---

# Converting PDF pages into images in Windows Forms

PdfToImageConverter allows you to convert pages from a PDF document into images using the Convert method. You can convert either a single page or pages into images.

## Converting a single page into image

You can export a single page from a PDF file as an image by specifying the page index and setting the parameters `keepTransparency` and `isSkipAnnotations` in the Convert method. To preserve transparency in the output image, make sure to set the `keepTransparency` parameter to true. If you want to exclude annotations and form field elements from the output image, set the `isSkipAnnotations` parameter to true. Refer to the following code to export a single page of PDF into PNG image.

{% tabs %}
{% highlight C# %}

//Initialize PDF to Image converter.
PdfToImageConverter imageConverter = new PdfToImageConverter();
//Load the PDF document as a stream
FileStream inputStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.ReadWrite);
imageConverter.Load(inputStream);
//Convert PDF to Image.
Stream outputStream = imageConverter.Convert(0, false, false);
Bitmap image = new Bitmap(outputStream);
image.Save("sample.png");

{% endhighlight %}
{% endtabs %}

## Exporting a specific range of pages

You can export a specific range of PDF pages into images by specifying the start and end page indexes and setting the parameters `keepTransparency` and `isSkipAnnotations` in the Convert method. To preserve transparency in the output images, make sure to set the `keepTransparency` parameter to true. If you want to exclude annotations and form field elements from the output images, set the `isSkipAnnotations` parameter to true. Refer to the following code to export the pages of PDF into PNG images.

{% tabs %}
{% highlight C# %}

//Initialize PDF to Image converter.
PdfToImageConverter imageConverter = new PdfToImageConverter();
//Load the PDF document as a stream
FileStream inputStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.ReadWrite);
imageConverter.Load(inputStream);
//Convert PDF to Image.
Stream[] outputStream = imageConverter.Convert(0, imageConverter.PageCount-1, false, false);
for(int i=0; i < outputStream.Length; i++)
{
    Bitmap image = new Bitmap(outputStream[i]);
    image.Save("sample-"+i+".png");
}

{% endhighlight %}
{% endtabs %}

## Exporting with a custom image size

You can export PDF pages as images with custom width and height by passing the required size and setting the parameters `keepTransparency` and `isSkipAnnotations` in the Convert method. To preserve transparency in the output images, make sure to set the `keepTransparency` parameter to true. If you want to exclude annotations and form field elements from the output images, set the `isSkipAnnotations` parameter to true. Refer to the following code to export the pages of PDF into PNG image. Refer to the following code to export the page at the index of 0 into PNG image with the width and the height of 1836 and 2372 in pixels respectively.

{% tabs %}
{% highlight C# %}

//Initialize PDF to Image converter.
PdfToImageConverter imageConverter = new PdfToImageConverter();
//Load the PDF document as a stream
FileStream inputStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.ReadWrite);
imageConverter.Load(inputStream);
//Convert PDF to Image.
Stream outputStream = imageConverter.Convert(0, new SizeF(1836, 2372), false, false, false);
Bitmap image = new Bitmap(outputStream);
image.Save("sample.png");

{% endhighlight %}
{% endtabs %}

N> To maintain the aspect ratio of output images, you are required to pass the value `true` for the `keepAspectRatio` parameter.

## Exporting with a custom image resolution

You can export PDF pages as images with custom horizontal and vertical resolutions by specifying the desired `DpiX` and `DpiY` values and configuring the `keepTransparency` and `isSkipAnnotations` parameters in the Convert method. To preserve transparency in the output images, make sure to set the `keepTransparency` parameter to true. If you want to exclude annotations and form field elements from the output images, set the `isSkipAnnotations` parameter to true. Refer to the following code to export the pages of PDF into PNG images with the horizontal and vertical resolution of 200 respectively.

{% tabs %}
{% highlight C# %}

int startPageIndex = 0;
int endPageIndex = 3;
float dpiX=200;
float dpiY=200;

//Initialize PDF to Image converter.
PdfToImageConverter imageConverter = new PdfToImageConverter();
//Load the PDF document as a stream
FileStream inputStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.ReadWrite);
imageConverter.Load(inputStream);
//Convert PDF to Image.
Stream[] outputStream = imageConverter.Convert(startPageIndex, endPageIndex, dpiX, dpiY, false, false);
for(int i=0; i < outputStream.Length; i++)
{
    Bitmap image = new Bitmap(outputStream[i]);
    image.Save("sample-"+i+".png");
}

{% endhighlight %}
{% endtabs %}
