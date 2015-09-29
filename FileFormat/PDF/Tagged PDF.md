---
layout: Post
title: Tagged PDF
description: Creating Tagged PDF from Html File : Tagged PDF
platform: FileFormat
control: PDF
documentation: UG
---
# Tagged PDF

Essential PDF provides the support to convert HTML to TaggedPDF by using MSHTML rendering library.

Tagged PDF is a stylized use of PDF that builds the logical structure framework. It defines a set of standard structure types and attributes that allow page content (text, graphics, and images) to be extracted and reused. The contents are accessible to users with visual impairments.

To convert HTML to Tagged PDF, you can use ConvertToTaggedPDF method in HtmlConverter class.

The following code illustrates how to convert HTML to TaggedPDF:

{% highlight c# %}
C#:

//Creates a new PdfDocument.

PdfDocument document = new PdfDocument();

//Creates a new instance of HtmlConverter class.

using (HtmlConverter html = new HtmlConverter())

{

//Enable JavaScript

html.EnableJavaScript = true;

//Converts to Tagged PDF.

html.ConvertToTaggedPDF(document,"http://www.google.com");

}

//Saves and closes the document.

document.Save("Sample.pdf");

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}
VB:

'Creates a new PdfDocument.

Dim document As New PdfDocument()

'Creates a new instance of HtmlConverter class.

Using html As New HtmlConverter()

'Enables JavaScript

html.EnableJavaScript = True

'Converts to Tagged PDF.

html.ConvertToTaggedPDF(document, "http://www.google.com")

End Using

'Saves and closes the document.

document.Save("Sample.pdf")

document.Close(True)





{% endhighlight %}

**Note** : Hyperlinks are not supported in tagged PDF

