---
title: Load PDF file in C# | Syncfusion&reg;
description: This page describes how to load PDF file from stream in C# using Syncfusion&reg; PDF to image converter library.
platform: file-formats
control: PDF to image
documentation: UG
---
# Load PDF file in C#

User can load a PDF as a stream using PdfToImageConverter, and then we can convert the PDF pages into images.

## Loading an existing PDF document using constructor

You can load an existing document to PdfToImageConverter. When creating an instance of the PdfToImageConverter class, pass the PDF document as a stream. The following example shows how to load an existing document from stream using the constructor.

{% tabs %} 

{% highlight c# tabtitle="C#" %}

//Load an existing PDF document from stream through constructor of `PdfToImageConverter` class. 
FileStream inputPDFStream = new FileStream(@"Input.pdf", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
PdfToImageConverter imageConverter = new PdfToImageConverter(inputPDFStream);

{% endhighlight %}

{% endtabs %}

## Loading an existing PDF document using load method

You can load an existing document to PdfToImageConverter. When using the 'load' method of the PdfToImageConverter class, pass the PDF document as a stream. The following example shows how to load an existing document from a stream using the 'load' method.

{% tabs %} 

{% highlight c# tabtitle="C#" %}

//Load an existing PDF document from stream through load method of `PdfToImageConverter` class.
PdfToImageConverter imageConverter = new PdfToImageConverter();
FileStream inputPDFStream = new FileStream(@"Input.pdf", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
imageConverter.Load(inputPDFStream);

{% endhighlight %}

{% endtabs %}

## Loading an Encrypted PDF document using constructor

You can load an existing encrypted document to PdfToImageConverter. When creating an instance of the PdfToImageConverter class, pass the PDF document as a stream and the password required to decrypt the provided PDF file. The following example shows how to load an existing enrypted document from a stream using the constructor.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Load an encrypted PDF document from stream through constructor of `PdfToImageConverter` class. 
FileStream inputPDFStream = new FileStream(@"Input.pdf", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
PdfToImageConverter imageConverter = new PdfToImageConverter(inputPDFStream, "password");

{% endhighlight %}

{% endtabs %}

## Loading an Encrypted PDF document using load method

You can load an existing encrypted document into PdfToImageConverter.When using the 'load' method of the PdfToImageConverter class, pass the PDF document as a stream and the password required to decrypt the provided PDF file. The following example shows how to load an existing enrypted document from a stream using the 'load' method.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Load an encrypted PDF document from stream through constructor of `PdfToImageConverter` class.
PdfToImageConverter imageConverter = new PdfToImageConverter();
FileStream inputPDFStream = new FileStream(@"Input.pdf", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
imageConverter.Load(inputPDFStream, "password");

{% endhighlight %}

{% endtabs %}