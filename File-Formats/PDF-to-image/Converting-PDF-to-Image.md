---
title: Converting PDF pages into images| Syncfusion
description: Learn about Converting PDF pages into images using Syncfusion PdfToImageConverter.
platform: file-formats
control: PDF to image
documentation: UG
---

# Converting PDF pages into images

PdfToImageConverter allows exporting pages of a PDF file into JPG, PNG, TIFF, and BMP formats using Convert methods. This option helps to convert PDF pages into images.

## Converting a single page into image

You can export a single page of the PDF file into an image by passing the page index as a parameter of the Convert method. Refer to the following code to export a single page of PDF into PNG image.

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

N> You can follow a similar step for exporting PDF into images in all the other image formats.
N> To maintain the transprency of output images, you are required to pass the value `true` for the `keepTransparency` parameter.
N> To avoid annotations in output images, you are required to pass the value `true` for the `isSkipAnnotations` parameter.

## Exporting a specific range of pages

You can export a specific range of PDF pages into images by passing the start and end page indexes as parameters of the Convert method. Refer to the following code to export the pages of PDF into JPEG images.

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

You can export PDF pages as images with custom width and height by passing the required size as a parameter of the Convert method. Refer to the following code to export the pages of PDF into PNG images. Refer to the following code to export the page at the index of 0 into PNG image with the width and the height of 1836 and 2372 in pixels respectively.

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

## Exporting with a custom image resolution using System.Drawing

You can export PDF pages as images with a custom horizontal and vertical resolution by passing the required `DpiX` and `DpiY` values as parameters of the Convert method respectively. Refer to the following code to export the pages of PDF into PNG images with the horizontal and vertical resolution of 200 respectively.

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

## Exporting with a custom image resolution using SkiaSharp

