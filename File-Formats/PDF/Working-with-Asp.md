---
title: Working with ASP.NET 
description: This section explains how to load and save PDF document in ASP.NET
platform: file-formats
control: PDF
documentation: UG
---
# Working with Asp.net

In your ASP.NET application, please add the required assemblies in order to use Essential PDF. [Refer here for assemblies required](/File-Formats/PDF/Assemblies-Required).

## Saving the document 

The following code example illustrates how to download the PDF document in browser after saving the document.
{% tabs %}
{% highlight c# %}

//Create a new PDF document

PdfDocument document = new PdfDocument();

//Add a page to the document

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page

PdfGraphics graphics = page.Graphics;

//Draw the rectangle

graphics.DrawRectangle(PdfPens.Black, new RectangleF(0, 0, 100, 100));

//Download the document in browser

document.Save("Output.pdf",HttpContext.Current.Response,HttpReadType.Save);

//Close the document

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Create a new PDF document

Dim document As New PdfDocument()

'Add a page to the document

Dim page As PdfPage = document.Pages.Add()

'Create PDF graphics for the page

Dim graphics As PdfGraphics = page.Graphics

'Draw the rectangle

graphics.DrawRectangle(PdfPens.Black, New RectangleF(0, 0, 100, 100))

'download the document in browser

document.Save("Output.pdf", HttpContext.Current.Response, HttpReadType.Save)

'Close the document

document.Close(True)



{% endhighlight %}
{% endtabs %}
The following code example illustrates how to open the PDF document in web browser after saving the document.
{% tabs %}
{% highlight c# %}


//Create a new PDF document

PdfDocument document = new PdfDocument();

//Add a page to the document

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Draw the rectangle

graphics.DrawRectangle(PdfPens.Black, new RectangleF(0, 0, 100, 100));

// Open the document in browser after saving it

document.Save("Output.pdf", HttpContext.Current.Response, HttpReadType.Open);

//Close the document

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Create a new PDF document

Dim document As New PdfDocument()

'Add a page to the document

Dim page As PdfPage = document.Pages.Add()

'Create PDF graphics for the page

Dim graphics As PdfGraphics = page.Graphics

'Draw the rectangle

graphics.DrawRectangle(PdfPens.Black, New RectangleF(0, 0, 100, 100))

' Open the document in browser after saving it

document.Save("Output.pdf", HttpContext.Current.Response, HttpReadType.Open);

'Close the document

document.Close(True)



{% endhighlight %}
{% endtabs %}
