---
title: Working with ASP.NET Core
description: Briefs about loading and saving the PDF document in ASP.NET Core platform
platform: file-formats
control: PDF
documentation: UG
---

# Working with ASP.NET Core

In your ASP.NET Core application, add the required assemblies to use Essential PDF. [Refer here for assemblies required](/File-Formats/PDF/Assemblies-Required).

## Loading the document

The following code example illustrates how to load the PDF document in ASP.NET Core.

{% highlight c# %}

//Load the PDF document

FileStream docStream = new FileStream("Sample.pdf", FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the document as stream

loadedDocument.Save(stream);

//If the position is not set to '0', then the PDF will be empty.

stream.Position = 0;

//Close the document

loadedDocument.Close(true);

//Defining the ContentType for PDF file

string contentType = "application/pdf";

//Define the file name

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

## Saving the document

The following code snippet illustrates how to save the PDF document in ASP.NET Core.

{% highlight c# %}

//Create a new document

PdfDocument document = new PdfDocument();

//Add a page

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page

PdfGraphics graphics = page.Graphics;

//Create a solid brush

PdfBrush brush = new PdfSolidBrush(Syncfusion.Drawing.Color.Black);

//Set the font

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 36);

//Draw the text

graphics.DrawString("Hello world!", font, brush, new Syncfusion.Drawing.PointF(20, 20));

//Creating the stream object 

MemoryStream stream = new MemoryStream();

//Save the document as stream

document.Save(stream);

//If the position is not set to '0', then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close(true);

//Defining the ContentType for PDF file

string contentType = "application/pdf";

//Define the file name

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}