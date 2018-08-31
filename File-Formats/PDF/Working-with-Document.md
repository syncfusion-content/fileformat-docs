---
title: Working with Document
description: This section explains how to set document Settings and properties to the PDF document using Essential PDF
platform: file-formats
control: PDF
documentation: UG
---
# Working with Document

## Adding the document settings

Essential PDF supports various page setting options to control the page display. 

You can choose the standard or custom page size when you add a page to the PDF document. This sample below illustrates how to create a PDF document with standard page size.

{% tabs %}

{% highlight c# %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

// Set the page size.

document.PageSettings.Size = PdfPageSize.A4;

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

//Save the document.

document.Save("Output.pdf");

//Close the document.

document.Close(true);

{% end highlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim document As New PdfDocument()

'Set the page size.

document.PageSettings.Size = PdfPageSize.A4

'Add a page to the document.

Dim page As PdfPage = document.Pages.Add()

'Create PDF graphics for the page.

Dim graphics As PdfGraphics = page.Graphics

'Set the font.

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 20)

'Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, New PointF(0, 0))

'Save the document.

document.Save("Output.pdf")

'Close the document.

document.Close(True)

{% end highlight %}

{% highlight UWP %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

// Set the page size.

document.PageSettings.Size = PdfPageSize.A4;

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

//Save the document into stream.

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document.

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Output.pdf");

{% end highlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

// Set the page size.

document.PageSettings.Size = PdfPageSize.A4;

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new Syncfusion.Drawing.PointF(0, 0));

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the document into stream

document.Save(stream);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document.

document.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% end highlight %}

{% highlight Xamarin %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

// Set the page size.

document.PageSettings.Size = PdfPageSize.A4;

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new Syncfusion.Drawing.PointF(0, 0));

//Save the document into stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document.

document.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

{% end highlight %}

{% end tabs %}

You can create a custom page size in the PDF document by using following code snippet.

{% tabs %}

{% highlight c# %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

// Set the custom page size.

document.PageSettings.Size = new SizeF(200,300);

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

//Save the document.

document.Save("Output.pdf");

//Close the document.

document.Close(true);

{% end highlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim document As New PdfDocument()

‘Set the custom page size.

document.PageSettings.Size = New SizeF(200, 300)

'Add a page to the document.

Dim page As PdfPage = document.Pages.Add()

'Create PDF graphics for the page.

Dim graphics As PdfGraphics = page.Graphics

'Set the font.

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 20)

'Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, New PointF(0, 0))

'Save the document.

document.Save("Output.pdf")

'Close the document.

document.Close(True)

{% end highlight %}

{% highlight UWP %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

// Set the custom page size.

document.PageSettings.Size = new SizeF(200, 300);

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

//Save the document into stream.

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document.

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Output.pdf");

{% end highlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

// Set the custom page size.

document.PageSettings.Size = new Syncfusion.Drawing.SizeF(200, 300);

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new Syncfusion.Drawing.PointF(0, 0));

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the document into stream

document.Save(stream);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document.

document.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% end highlight %}

{% highlight Xamarin %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

// Set the custom page size.

document.PageSettings.Size = new Syncfusion.Drawing.SizeF(200, 300);

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new Syncfusion.Drawing.PointF(0, 0));

//Save the document into stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document.

document.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

{% end highlight %}

{% end tabs %}

You can change page orientation from portrait to landscape by using the following code snippet.

{% tabs %}

{% highlight c# %}


//Create a new PDF document.

PdfDocument document = new PdfDocument();

// Set the page size.

document.PageSettings.Size = PdfPageSize.A4;

//Change the page orientation to landscape

document.PageSettings.Orientation = PdfPageOrientation.Landscape;

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

//Save the document.

document.Save("Output.pdf");

//Close the document.

document.Close(true);

{% end highlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim document As New PdfDocument()

' Set the page size.

document.PageSettings.Size = PdfPageSize.A4

'Change the page orientation to landscape

document.PageSettings.Orientation = PdfPageOrientation.Landscape

'Add a page to the document.

Dim page As PdfPage = document.Pages.Add()

'Create PDF graphics for the page.

Dim graphics As PdfGraphics = page.Graphics

'Set the font.

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 20)

'Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, New PointF(0, 0))

'Save the document.

document.Save("Output.pdf")

'Close the document.

document.Close(True)

{% end highlight %}

{% highlight UWP %}


//Create a new PDF document.

PdfDocument document = new PdfDocument();

// Set the page size.

document.PageSettings.Size = PdfPageSize.A4;

//Change the page orientation to landscape

document.PageSettings.Orientation = PdfPageOrientation.Landscape;

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

//Save the document into stream.

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document.

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Output.pdf");


{% end highlight %}

{% highlight ASP.NET Core %}


//Create a new PDF document.

PdfDocument document = new PdfDocument();

// Set the page size.

document.PageSettings.Size = PdfPageSize.A4;

//Change the page orientation to landscape

document.PageSettings.Orientation = PdfPageOrientation.Landscape;

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new Syncfusion.Drawing.PointF(0, 0));

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the document into stream

document.Save(stream);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document.

document.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);


{% end highlight %}

{% highlight Xamarin %}


//Create a new PDF document.

PdfDocument document = new PdfDocument();

// Set the page size.

document.PageSettings.Size = PdfPageSize.A4;

//Change the page orientation to landscape

document.PageSettings.Orientation = PdfPageOrientation.Landscape;

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new Syncfusion.Drawing.PointF(0, 0));

//Save the document into stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document.

document.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}


{% end highlight %}

{% end tabs %}

You can also change orientation by setting the rotation angle using PdfPageRotateAngle Enum. The following code snippets illustrates the same.

{% tabs %}

{% highlight c# %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

// Set the page size.

document.PageSettings.Size = PdfPageSize.A4;

//Change the page orientation to 90°

document.PageSettings.Rotate = PdfPageRotateAngle.RotateAngle90;

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

//Save the document.

document.Save("Output.pdf");

//Close the document.

document.Close(true);

{% end highlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim document As New PdfDocument()

‘Set the page size.

document.PageSettings.Size = PdfPageSize.A4

'Change the page orientation to 90°

document.PageSettings.Rotate = PdfPageRotateAngle.RotateAngle90

'Add a page to the document.

Dim page As PdfPage = document.Pages.Add()

'Create PDF graphics for the page.

Dim graphics As PdfGraphics = page.Graphics

'Set the font.

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 20)

'Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, New PointF(0, 0))

'Save the document.

document.Save("Output.pdf")

'Close the document.

document.Close(True)

{% end highlight %}

{% highlight UWP %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

// Set the page size.

document.PageSettings.Size = PdfPageSize.A4;

//Change the page orientation to 90°

document.PageSettings.Rotate = PdfPageRotateAngle.RotateAngle90;

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

//Save the document into stream.

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document.

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Output.pdf");


{% end highlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

// Set the page size.

document.PageSettings.Size = PdfPageSize.A4;

//Change the page orientation to 90°

document.PageSettings.Rotate = PdfPageRotateAngle.RotateAngle90;

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new Syncfusion.Drawing.PointF(0, 0));

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the document into stream

document.Save(stream);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document.

document.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);


{% end highlight %}

{% highlight Xamarin %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

// Set the page size.

document.PageSettings.Size = PdfPageSize.A4;

//Change the page orientation to 90°

document.PageSettings.Rotate = PdfPageRotateAngle.RotateAngle90;

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new Syncfusion.Drawing.PointF(0, 0));

//Save the document into stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document.

document.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
     Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

{% end highlight %}

{% end tabs %}

## Creating sections in a PDF

PDF sections are parts of the PDF document, which may contain one or more pages with their unique page settings. The following code snippet illustrates the same.

{% tabs %}

{% highlight c# %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a section to PDF document.

PdfSection section = document.Sections.Add();

//Add pages to the section

PdfPage page = section.Pages.Add();

//Create PDF graphics for the page

PdfGraphics graphics = page.Graphics;

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

//Save the document.

document.Save("Output.pdf");

//Close the document.

document.Close(true);

{% end highlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim document As New PdfDocument()

'Add a section to PDF document.

Dim section As PdfSection = document.Sections.Add()

'Add pages to the section

Dim page As PdfPage = section.Pages.Add()

'Create PDF graphics for the page

Dim graphics As PdfGraphics = page.Graphics

'Set the font.

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 20)

'Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, New PointF(0, 0))

'Save the document.

document.Save("Output.pdf")

'Close the document.

document.Close(True)

{% end highlight %}

{% highlight UWP %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a section to PDF document.

PdfSection section = document.Sections.Add();

//Add pages to the section

PdfPage page = section.Pages.Add();

//Create PDF graphics for the page

PdfGraphics graphics = page.Graphics;

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

//Save the document into stream.

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document.

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Output.pdf");


{% end highlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a section to PDF document.

PdfSection section = document.Sections.Add();

//Add pages to the section

PdfPage page = section.Pages.Add();

//Create PDF graphics for the page

PdfGraphics graphics = page.Graphics;

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new Syncfusion.Drawing.PointF(0, 0));

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the document into stream

document.Save(stream);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document.

document.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);


{% end highlight %}

{% highlight Xamarin %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a section to PDF document.

PdfSection section = document.Sections.Add();

//Add pages to the section

PdfPage page = section.Pages.Add();

//Create PDF graphics for the page

PdfGraphics graphics = page.Graphics;

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new Syncfusion.Drawing.PointF(0, 0));

//Save the document into stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document.

document.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}


{% end highlight %}

{% end tabs %}

## Printing PDF document

To print a PDF document, the following assemblies have to be added as references to the project.

1. Syncfusion.Compression.Base.dll
2. Syncfusion.Pdf.Base.dll
3. Syncfusion.PdfViewer.Windows.dll 

The following code snippet illustrates how to print a PDF document.

{% tabs %}

{% highlight c# %}

PdfDocumentView viewer = new PdfDocumentView();

//Load the PDF document

viewer.Load("Input.pdf");

//Initialize print dialog.

PrintDialog dialog = new PrintDialog();

dialog.AllowPrintToFile = true;

dialog.AllowSomePages = true;

dialog.AllowCurrentPage = true;

dialog.Document = viewer.PrintDocument;

//Print the PDF document

dialog.Document.Print();

//Dispose the viewer

viewer.Dispose();

{% end highlight %}

{% highlight vb.net %}

Dim viewer As New PdfDocumentView()

'Load the PDF document

viewer.Load("Input.pdf")

'Initialize print dialog.

Dim dialog As New PrintDialog()

dialog.AllowPrintToFile = True

dialog.AllowSomePages = True

dialog.AllowCurrentPage = True

dialog.Document = viewer.PrintDocument

'Print the PDF document

dialog.Document.Print()

'Dispose the viewer

viewer.Dispose()

{% end highlight %}

{% end tabs %}

## Working with document properties

Essential PDF allows you to set, read and modify the document information of a PDF like Author, CreationDate, Subject, Title, and Producer etc. The **DocumentInformation** **property** of the PdfDocument or PdfLoadedDocument provides access to this information.

The following code snippet illustrates how to set PDF document information.

{% tabs %}

{% highlight c# %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Set document information.

document.DocumentInformation.Author = "Syncfusion";

document.DocumentInformation.CreationDate = DateTime.Now;

document.DocumentInformation.Creator = "Essential PDF";

document.DocumentInformation.Keywords = "PDF";

document.DocumentInformation.Subject = "Document information DEMO";

document.DocumentInformation.Title = "Essential PDF Sample";

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

//Save the document.

document.Save("Output.pdf");

//Close the document.

document.Close(true);

{% end highlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim document As New PdfDocument()

'Set document information.

document.DocumentInformation.Author = "Syncfusion"

document.DocumentInformation.CreationDate = DateTime.Now

document.DocumentInformation.Creator = "Essential PDF"

document.DocumentInformation.Keywords = "PDF"

document.DocumentInformation.Subject = "Document information DEMO"

document.DocumentInformation.Title = "Essential PDF Sample"

'Add a page to the document.

Dim page As PdfPage = document.Pages.Add()

'Create PDF graphics for the page.

Dim graphics As PdfGraphics = page.Graphics

'Set the font.

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 20)

'Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, New PointF(0, 0))

'Save the document.

document.Save("Output.pdf")

'Close the document.

document.Close(True)

{% end highlight %}

{% highlight UWP %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Set document information.

document.DocumentInformation.Author = "Syncfusion";

document.DocumentInformation.CreationDate = DateTime.Now;

document.DocumentInformation.Creator = "Essential PDF";

document.DocumentInformation.Keywords = "PDF";

document.DocumentInformation.Subject = "Document information DEMO";

document.DocumentInformation.Title = "Essential PDF Sample";

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

//Save the document into stream.

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document.

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Output.pdf");


{% end highlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Set document information.

document.DocumentInformation.Author = "Syncfusion";

document.DocumentInformation.CreationDate = DateTime.Now;

document.DocumentInformation.Creator = "Essential PDF";

document.DocumentInformation.Keywords = "PDF";

document.DocumentInformation.Subject = "Document information DEMO";

document.DocumentInformation.Title = "Essential PDF Sample";

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the document into stream

document.Save(stream);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document.

document.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);


{% end highlight %}

{% highlight Xamarin %}

 //Create a new PDF document.

PdfDocument document = new PdfDocument();

//Set document information.

document.DocumentInformation.Author = "Syncfusion";

document.DocumentInformation.CreationDate = DateTime.Now;

document.DocumentInformation.Creator = "Essential PDF";

document.DocumentInformation.Keywords = "PDF";

document.DocumentInformation.Subject = "Document information DEMO";

document.DocumentInformation.Title = "Essential PDF Sample";

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new Syncfusion.Drawing.PointF(0, 0));

//Save the document into stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document.

document.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}


{% end highlight %}

{% end tabs %}

The following code snippet shows how to read and modify the document properties of an existing PDF document.

{% tabs %}

{% highlight c# %}

//Create a new PDF document.

PdfLoadedDocument document = new PdfLoadedDocument("Input.pdf");

//Modify document information.

document.DocumentInformation.Author = "Syncfusion";

document.DocumentInformation.CreationDate = DateTime.Now;

document.DocumentInformation.Creator = "Essential PDF";

document.DocumentInformation.Keywords = "PDF";

document.DocumentInformation.Subject = "Document information DEMO";

document.DocumentInformation.Title = "Essential PDF Sample";

//Save the document.
document.Save("Output.pdf");

//Close the document.
document.Close(true);

{% end highlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim document As New PdfLoadedDocument("Input.pdf")

'Modify document information.

document.DocumentInformation.Author = "Syncfusion"

document.DocumentInformation.CreationDate = DateTime.Now

document.DocumentInformation.Creator = "Essential PDF"

document.DocumentInformation.Keywords = "PDF"

document.DocumentInformation.Subject = "Document information DEMO"

document.DocumentInformation.Title = "Essential PDF Sample"

'Save the document.

document.Save("Output.pdf")

'Close the document.

document.Close(True)

{% end highlight %}

{% highlight UWP %}

//Create the file open picker

var picker = new FileOpenPicker();

picker.FileTypeFilter.Add(".pdf");

//Browse and chose the file

StorageFile file = await picker.PickSingleFileAsync();

//Creates an empty PDF loaded document instance

PdfLoadedDocument document = new PdfLoadedDocument();

//Loads or opens an existing PDF document through Open method of PdfLoadedDocument class

await document.OpenAsync(file);

//Modify document information.

document.DocumentInformation.Author = "Syncfusion";

document.DocumentInformation.CreationDate = DateTime.Now;

document.DocumentInformation.Creator = "Essential PDF";

document.DocumentInformation.Keywords = "PDF";

document.DocumentInformation.Subject = "Document information DEMO";

document.DocumentInformation.Title = "Essential PDF Sample";

//Save the document into stream.

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document.

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Output.pdf");


{% end highlight %}

{% highlight ASP.NET Core %}

//Load the PDF document

FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);

PdfLoadedDocument document = new PdfLoadedDocument(docStream);

//Modify document information.

document.DocumentInformation.Author = "Syncfusion";

document.DocumentInformation.CreationDate = DateTime.Now;

document.DocumentInformation.Creator = "Essential PDF";

document.DocumentInformation.Keywords = "PDF";

document.DocumentInformation.Subject = "Document information DEMO";

document.DocumentInformation.Title = "Essential PDF Sample";

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the document into stream

document.Save(stream);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document.

document.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);


{% end highlight %}

{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");

PdfLoadedDocument document = new PdfLoadedDocument(docStream);

//Modify document information.

document.DocumentInformation.Author = "Syncfusion";

document.DocumentInformation.CreationDate = DateTime.Now;

document.DocumentInformation.Creator = "Essential PDF";

document.DocumentInformation.Keywords = "PDF";

document.DocumentInformation.Subject = "Document information DEMO";

document.DocumentInformation.Title = "Essential PDF Sample";

//Save the document into stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document.

document.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}


{% end highlight %}

{% end tabs %}

## Performing incremental update for PDF document

The Essential PDF supports an incremental update for PDF document. The content of a PDF file can be updated incrementally without rewriting the entire file. Changes are appended to the end of the file, leaving its original contents intact. The main benefit is small changes to a large PDF document can be saved quickly but the resultant document size gets increased compared with the original PDF document. Disabling the incremental update will rewrite the entire file, which results in a smaller PDF. This is illustrated in the following code sample.

{% tabs %}

{% highlight c# %}

//Load the PDF document

PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");

//Disable the incremental update

loadedDocument.FileStructure.IncrementalUpdate = false;

//Set the compression level

loadedDocument.Compression = PdfCompressionLevel.Best;

//Save the document

loadedDocument.Save("Output.pdf");

//Close the document

loadedDocument.Close(true);


{% end highlight %}

{% highlight vb.net %}

'Load the PDF document

Dim loadedDocument As New PdfLoadedDocument("Input.pdf")

'Disable the incremental update

loadedDocument.FileStructure.IncrementalUpdate = False

'Set the compression level

loadedDocument.Compression = PdfCompressionLevel.Best

'Save the document

loadedDocument.Save("Output.pdf")

'Close the document

loadedDocument.Close(True)


{% end highlight %}

{% highlight UWP %}

//Create the file open picker

var picker = new FileOpenPicker();

picker.FileTypeFilter.Add(".pdf");

//Browse and chose the file

StorageFile file = await picker.PickSingleFileAsync();

//Creates an empty PDF loaded document instance

PdfLoadedDocument loadedDocument = new PdfLoadedDocument();

//Loads or opens an existing PDF document through Open method of PdfLoadedDocument class

await loadedDocument.OpenAsync(file);

//Disable the incremental update

loadedDocument.FileStructure.IncrementalUpdate = false;

//Set the compression level

loadedDocument.Compression = PdfCompressionLevel.Best;

//Save the document into stream.

MemoryStream stream = new MemoryStream();

await loadedDocument.SaveAsync(stream);

//Close the document.

loadedDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Output.pdf");


{% end highlight %}

{% highlight ASP.NET Core %}

//Load the PDF document

FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Disable the incremental update

loadedDocument.FileStructure.IncrementalUpdate = false;

//Set the compression level

loadedDocument.Compression = PdfCompressionLevel.Best;

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the document into stream

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document.

loadedDocument.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);


{% end highlight %}

{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Disable the incremental update

loadedDocument.FileStructure.IncrementalUpdate = false;

//Set the compression level

loadedDocument.Compression = PdfCompressionLevel.Best;

//Save the document into stream.

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document.

loadedDocument.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}


{% end highlight %

{% end tabs %}

## Choosing the viewer preferences

Essential PDF allows you to set various PDF viewer preferences to be used when the generated PDF document is displayed in a PDF reader application.

You can hide the menu bar and toolbar by using the following code snippet.

{% tabs %}

{% highlight c# %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

//Hide viewer application's menu bar.

document.ViewerPreferences.HideMenubar = true;

//Hide viewer application's toolbar.

document.ViewerPreferences.HideToolbar = true;

//Shows user interface elements in the document's window (such as scroll bars and navigation controls).

document.ViewerPreferences.HideWindowUI = false;

//Save the document.

document.Save("Output.pdf");

//Close the document.

document.Close(true);

{% end highlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim document As New PdfDocument()

'Add a page to the document.

Dim page As PdfPage = document.Pages.Add()

'Create PDF graphics for the page.

Dim graphics As PdfGraphics = page.Graphics

'Set the font.

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 20)

'Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, New PointF(0, 0))

'Hides viewer application's menu bar.

document.ViewerPreferences.HideMenubar = True

'Hides viewer application's toolbar.

document.ViewerPreferences.HideToolbar = True

'Shows user interface elements in the document's window (such as scroll bars and navigation controls).

document.ViewerPreferences.HideWindowUI = False

'Save the document.

document.Save("Output.pdf")

'Close the document.

document.Close(True)

{% end highlight %}

{% highlight UWP %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

//Hide viewer application's menu bar.

document.ViewerPreferences.HideMenubar = true;

//Hide viewer application's toolbar.

document.ViewerPreferences.HideToolbar = true;

//Shows user interface elements in the document's window (such as scroll bars and navigation controls).

document.ViewerPreferences.HideWindowUI = false;

//Save the document into stream.

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document.

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Output.pdf");


{% end highlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new Syncfusion.Drawing.PointF(0, 0));

//Hide viewer application's menu bar.

document.ViewerPreferences.HideMenubar = true;

//Hide viewer application's toolbar.

document.ViewerPreferences.HideToolbar = true;

//Shows user interface elements in the document's window (such as scroll bars and navigation controls).

document.ViewerPreferences.HideWindowUI = false;

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the document into stream

document.Save(stream);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document.

document.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% end highlight %}

{% highlight Xamarin %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new Syncfusion.Drawing.PointF(0, 0));

//Hide viewer application's menu bar.

document.ViewerPreferences.HideMenubar = true;

//Hide viewer application's toolbar.

document.ViewerPreferences.HideToolbar = true;

//Shows user interface elements in the document's window (such as scroll bars and navigation controls).

document.ViewerPreferences.HideWindowUI = false;

//Save the document into stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document.

document.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}


{% end highlight %}

{% end tabs %}

You can also allow the reader application to initially display the bookmarks, thumbnails or attachments using  PdfPageMode ENUM

{% tabs %}

{% highlight c# %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

//Show the attachments panel.

document.ViewerPreferences.PageMode = PdfPageMode.UseAttachments;

//Save the document.

document.Save("Output.pdf");

//Close the document.

document.Close(true);

{% end highlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim document As New PdfDocument()

'Add a page to the document.

Dim page As PdfPage = document.Pages.Add()

'Create PDF graphics for the page.

Dim graphics As PdfGraphics = page.Graphics

'Set the font.

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 20)

'Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, New PointF(0, 0))

'Show the attachments panel.

document.ViewerPreferences.PageMode = PdfPageMode.UseAttachments

'Save the document.

document.Save("Output.pdf")

'Close the document.

document.Close(True)

{% end highlight %}

{% highlight UWP %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

//Show the attachments panel.

document.ViewerPreferences.PageMode = PdfPageMode.UseAttachments;

//Save the document into stream.

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document.

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Output.pdf");

{% end highlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new Syncfusion.Drawing.PointF(0, 0));

//Show the attachments panel.

document.ViewerPreferences.PageMode = PdfPageMode.UseAttachments;

//Save the document into stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document.

document.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);


{% end highlight %}

{% highlight Xamarin %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new Syncfusion.Drawing.PointF(0, 0));

//Show the attachments panel.

document.ViewerPreferences.PageMode = PdfPageMode.UseAttachments;

//Save the document into stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document.

document.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

{% end highlight %}

{% end tabs %}

## Adding document action

Please refer to the [actions](/file-formats/pdf/working-with-action "Working with action") section for more document level operations using the PdfJavascript and PDF actions.

## Working in Multi-Threading Environment

Essential PDF allows you to create or modify PDF documents simultaneously in multi-threading environment by using ```PdfDocument.EnableThreadSafe``` instance.

The following code illustrates how to create a PDF document in multi-threading environment.

{% tabs %}
{% highlight c# %}

IEnumerable<int> works = Enumerable.Range(0, 100);

Parallel.ForEach(works, index => GeneratePDF(index));

private void GeneratePDF(int index)
{
//Enable the thread safe in PDF document.
PdfDocument.EnableThreadSafe = true;

//Create a new PDF document.
PdfDocument document = new PdfDocument();

//Add a page to the document.
PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;

//Set the standard font.
PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.
graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

string name = Guid.NewGuid().ToString();

//Save the document.
document.Save(name+".pdf");

//Close the document.
document.Close(true);
}

{% end highlight %}
{% highlight vb.net %}

Dim works As IEnumerable(Of Integer) = Enumerable.Range(0, 100)

Parallel.ForEach(works, Sub(index) GeneratePDF(index))

Private Sub GeneratePDF(ByVal index As Integer)

'Enable the thread safe in PDF document.
PdfDocument.EnableThreadSafe = True

'Create a new PDF document.
Dim document As PdfDocument = New PdfDocument()

'Add a page to the document.
Dim page As PdfPage = document.Pages.Add()

'Create PDF graphics for the page.
Dim graphics As PdfGraphics = page.Graphics

'Set the standard font.
Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 20)

'Draw the text.
graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, New PointF(0, 0))

Dim name As String = Guid.NewGuid().ToString()

'Save the document.
document.Save(name + ".pdf")

'Close the document.
document.Close(True)

End Sub

{% end highlight %}

{% highlight UWP %}

{% end highlight %}

% highlight ASP.NET Core %}

{% end highlight %}

% highlight Xamarin %}

{% end highlight %}
{% end tabs %}

You can also modify the existing document in multi-threading environment. The below samples explain how to modify the existing PDF document in multi-threading environment.

{% tabs %}
{% highlight c# %}

IEnumerable<int> works = Enumerable.Range(0, 100);

Parallel.ForEach(works, index => GeneratePDF(index));

private void GeneratePDF(int index)
{

//Enable the thread safe in PDF document.
PdfDocument.EnableThreadSafe = true;

//Load a PDF document.
PdfLoadedDocument doc = new PdfLoadedDocument("input.pdf");

//Get first page from document
PdfLoadedPage page = doc.Pages[0] as PdfLoadedPage;

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Set the standard font.
PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.
graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

string name = Guid.NewGuid().ToString();

//Save the document.
doc.Save(name+".pdf");

//Close the document.
doc.Close(true);

}

{% end highlight %}
{% highlight vb.net %}

Dim works As IEnumerable(Of Integer) = Enumerable.Range(0, 100)

Parallel.ForEach(works, Sub(index) GeneratePDF(index))

Private Sub GeneratePDF(ByVal index As Integer)

'Enable the thread safe in PDF document.
PdfDocument.EnableThreadSafe = True

'Load a PDF document.
Dim doc As PdfLoadedDocument = New PdfLoadedDocument("input.pdf")

'Get first page from document
Dim page As PdfLoadedPage = doc.Pages(0)

'Create PDF graphics for the page
Dim graphics As PdfGraphics = page.Graphics

'Set the standard font.
Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 20)

'Draw the text.
graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, New PointF(0, 0))

Dim name As String = Guid.NewGuid().ToString()

'Save the document.
doc.Save(name + ".pdf")

'Close the document.
doc.Close(True)

End Sub

{% end highlight %}
{% end tabs %}
