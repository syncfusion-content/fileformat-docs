---
title: Open PDF file in C# | Syncfusion
description: This page describes how to open PDF file from stream in C# using Syncfusion PDF to image converter library.
platform: file-formats
control: PDF to image
documentation: UG
---
# Open PDF file in C#

## Opening an existing PDF document using constructor

You can open an existing document by using PdfToImageConverter class. The following example shows how to load an existing document from physical path or stream using constructor.

{% tabs %} 

{% highlight c# tabtitle="C#" %}

//Open an existing PDF document from stream through constructor of `PdfToImageConverter` class. 
FileStream inputPDFStream = new FileStream(@"Input.pdf", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
PdfToImageConverter imageConverter = new PdfToImageConverter(inputPDFStream);

{% endhighlight %}

{% endtabs %}

## Opening an existing PDF document using load method

You can open an existing document by using PdfToImageConverter class. The following example shows how to load an existing document from physical path or stream using load method.

{% tabs %} 

{% highlight c# tabtitle="C#" %}

//Open an existing PDF document from stream through load method of `PdfToImageConverter` class.
PdfToImageConverter imageConverter = new PdfToImageConverter();
FileStream inputPDFStream = new FileStream(@"Input.pdf", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
imageConverter.Load(inputPDFStream);

{% endhighlight %}

{% endtabs %}

## Opening an Encrypted PDF document using constructor

You can open an existing encrypted PDF document from either the file system or the stream using constructor of PdfToImageConverter class as shown in the below code example. 

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Open an encrypted PDF document from stream through constructor of `PdfToImageConverter` class. 
FileStream inputPDFStream = new FileStream(@"Input.pdf", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
PdfToImageConverter imageConverter = new PdfToImageConverter(inputPDFStream, "password");

{% endhighlight %}

{% endtabs %}

## Opening an Encrypted PDF document using load method

You can open an existing encrypted PDF document from either the file system or the stream using load method of PdfToImageConverter class as shown in the below code example. 

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Open an encrypted PDF document from stream through constructor of `PdfToImageConverter` class.
PdfToImageConverter imageConverter = new PdfToImageConverter();
FileStream inputPDFStream = new FileStream(@"Input.pdf", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
imageConverter.Load(inputPDFStream, "password");

{% endhighlight %}

{% endtabs %}