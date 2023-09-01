---
layout: post
title: Convert PDF to image using PDFium | Syncfusion
description: Learn about Converting PDF pages into images using Syncfusion PdfToImageConverter with the help of PDFium.
platform: file-formats
control: PDF to image
documentation: UG
---

# Convert PDF to image using PDFium

PDFium is used in Google Chrome for rendering PDF files. It provides accurate and robust PDF rendering. It is the recommended PDF rendering engine. 

N> PDFium rendering is not supported in Windows XP operating system.

## How to run PDFium in a restricted access environment

If there is any access restriction applied to the application output folder, then the Syncfusion Pdf To Image Converter cannot able to extract and consume the PDFium engine.

In that situation, you need to add the following steps to consume the PDFium rendering engine.

* Create a folder where your application can access, create & read files. For example, <b>"d:\ThirdPartyBinaries\"</b>.
* Update the path of this folder to the ReferencePath property of PdfToImageConverter control, like shown in the following code sample.
* If ReferencePath is set, then PdfToImageConverter extracts the PDFium binary inside that specified folder and consume the PDFium rendering engine.

{% tabs %}
{% highlight c# %}

PdfToImageConverter imageConverter;
imageConverter.ReferencePath = @"D:\ThirdPartyBinaries\";

{% endhighlight %}
{% endtabs %}
