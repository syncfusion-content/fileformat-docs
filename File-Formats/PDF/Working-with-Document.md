---
title: Working with Document | Syncfusion
description: This section explains how to set document Settings and properties to the PDF document using Essential PDF
platform: file-formats
control: PDF
documentation: UG
---
# Working with Document

## Adding the document settings

Essential PDF supports various page setting options to control the page display, through [PageSettings](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfDocument.html#Syncfusion_Pdf_PdfDocument_PageSettings) property of [PdfDocument](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfDocument.html).

You can choose the standard or custom page size when you add a page to the PDF document. This below sample illustrates how to create a PDF document with standard page size.

{% tabs %}

{% highlight c# tabtitle="C#" %}

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

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new PDF document.
Dim document As New PdfDocument()
'Set the page size.
document.PageSettings.Size = PdfPageSize.A4
'Add a page to the document
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

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

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

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

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

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

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

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/PDF%20Document/Create-a-PDF-document-with-standard-page-size/). 

You can create a PDF document with custom page size in [PdfPageSettings Size](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfPageSettings.html#Syncfusion_Pdf_PdfPageSettings_Size) property by using the following code snippet.

{% tabs %}

{% highlight c# tabtitle="C#" %}

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

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

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

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

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

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

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

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

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

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/PDF%20Document/Create-a-PDF-document-with-custom-page-size/). 

You can change page orientation from portrait to landscape, through [PdfPageOrientation](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfPageOrientation.html) Enum by using the following code snippet.

{% tabs %}

{% highlight c# tabtitle="C#" %}


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

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

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

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}


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

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}


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

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

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

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/PDF%20Document/Change-the-page-orientation-from-portrait-to-landscape/). 

N> Generally, the PDF page orientation will be updated based on the custom page size. But if a custom page orientation is set using the [Orientation](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfPageSettings.html#Syncfusion_Pdf_PdfPageSettings_Orientation) property, then the PDF page size will be updated based on the custom orientation.

You can also change orientation by setting the rotation angle using [PdfPageRotateAngle](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfPageRotateAngle.html) Enum. The following code snippet illustrates the same.

{% tabs %}

{% highlight c# tabtitle="C#" %}

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

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

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

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

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

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

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

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();
// Set the page size
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

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/PDF%20Document/Rotate_PDF_based_on_angle/). 

## Creating sections in a PDF

PDF sections are parts of the PDF document, which may contain one or more pages with their unique page settings. The following code snippet illustrates how to create a [PdfSection](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfSection.html) in a PDF document.

{% tabs %}

{% highlight c# tabtitle="C#" %}

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

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

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

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

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

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

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

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();
//Add a section to PDF document.
PdfSection section = document.Sections.Add()
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

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/PDF%20Document/Create_sections_in_PDF_document/). 

## Printing PDF document

To print a PDF document, the following assemblies have to be added as references to the project.

1. Syncfusion.Compression.Base.dll
2. Syncfusion.Pdf.Base.dll
3. Syncfusion.PdfViewer.Windows.dll 

The following code snippet illustrates how to print a PDF document.

{% tabs %}

{% highlight c# tabtitle="C#" %}

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

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

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

{% endhighlight %}

{% endtabs %}

## Working with document properties

Essential PDF allows you to set, read and modify the document information of a PDF like Author, CreationDate, Subject, Title, and Producer etc. The [DocumentInformation](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfDocumentBase.html#Syncfusion_Pdf_PdfDocumentBase_DocumentInformation) property of the [PdfDocument](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfDocument.html) or [PdfLoadedDocument](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html) provides access to this information.

The following code snippet illustrates how to set PDF document information.

{% tabs %}

{% highlight c# tabtitle="C#" %}

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
//Draw the text
graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

//Save the document.
document.Save("Output.pdf");
//Close the document.
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

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

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

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

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

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

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

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

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/PDF%20Document/Add_PDF_document_properties/). 

To read and modify the document [DocumentInformation](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfDocumentBase.html#Syncfusion_Pdf_PdfDocumentBase_DocumentInformation) property to an existing PDF document using [PDFLoadedDocument](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html) class.The following code example explain this.

{% tabs %}

{% highlight c# tabtitle="C#" %}

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

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new PDF document.
Dim document As New PdfLoadedDocument("Input.pdf")

'Modify document information.
document.DocumentInformation.Author = "Syncfusion"
document.DocumentInformation.CreationDate = DateTime.Now
document.DocumentInformation.Creator = "Essential PDF"
document.DocumentInformation.Keywords = "PDF"
document.DocumentInformation.Subject = "Document information DEMO"
document.DocumentInformation.Title = "Essential PDF Sample"

'Save the document
document.Save("Output.pdf")
'Close the document.
document.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

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

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

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
string fileNam
//Creates a FileContentResult object by using the file contents, content type, and file name.
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

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

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/PDF%20Document/Change_existing_PDF_properties). 

## Performing incremental update for PDF document

The Essential PDF supports incremental update for PDF document. The content of a PDF file can be updated incrementally without rewriting the entire file. Changes are appended to the end of the file, leaving its original contents intact. The main benefit is small changes to a large PDF document can be saved quickly but the resultant document size gets increased compared with the original PDF document. Disabling the [IncrementalUpdate](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfFileStructure.html#Syncfusion_Pdf_PdfFileStructure_IncrementalUpdate) of [PdfFileStructure](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfFileStructure.html) will rewrite the entire file, which results in a smaller PDF. This is illustrated in the following code sample.

{% tabs %}

{% highlight c# tabtitle="C#" %}

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

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

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

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

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

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

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

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

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


{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/PDF%20Document/Perform-incremental-update-for-the-PDF-document/). 

## Choosing the viewer preferences

Essential PDF allows you to set various PDF viewer preferences to be used when the generated PDF document is displayed in a PDF reader application.

You can hide the menu bar and toolbar by enabling [HideMenubar](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfViewerPreferences.html#Syncfusion_Pdf_PdfViewerPreferences_HideMenubar) and [HideToolbar](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfViewerPreferences.html#Syncfusion_Pdf_PdfViewerPreferences_HideToolbar) properties of [PdfViewerPreferences](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfViewerPreferences.html) respectively. This is illustrated in the following code sample.

{% tabs %}

{% highlight c# tabtitle="C#" %}

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

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

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

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

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

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

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

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

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

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/PDF%20Document/Create_PDF_with_viewer_preference/). 

You can also allow the reader application to initially display the bookmarks, thumbnails or attachments using [PdfPageMode](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfPageMode.html) Enum.

{% tabs %}

{% highlight c# tabtitle="C#" %}

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

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

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

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

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

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

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

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

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

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/PDF%20Document/Create-PDF-with-display-of-specific-panel/). 

## Adding document action

Please refer to the [actions](/file-formats/pdf/working-with-action "Working with action") section for more document level operations using the PdfJavascript and PDF actions.

## Working in Multi-Threading Environment

Essential PDF allows you to create or modify PDF documents simultaneously in multi-threading environment using [EnableThreadSafe](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfDocument.html#Syncfusion_Pdf_PdfDocument_EnableThreadSafe) property of [PdfDocument](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfDocument.html) class.

The following code sample illustrates how to create a PDF document in multi-threading environment.

{% tabs %}
{% highlight c# tabtitle="C#" %}

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

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET" %}

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

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/PDF%20Document/Create-a-PDF-in-multi-threading-environment). 

To modify the existing PDF document in multi-threading environment [EnableThreadSafe](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfDocument.html#Syncfusion_Pdf_PdfDocument_EnableThreadSafe) property to an existing PDF document using [PDFLoadedDocument](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html) class. The following code example explain this.
{% tabs %}
{% highlight c# tabtitle="C#" %}

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

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET" %}

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

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/PDF%20Document/Modify-existing-PDF-in-multi-threading/). 

## Uniform Resource Naming in PDF document

The Essential PDF allows you to create a PDF document with proper uniform resource naming by using the [EnableUniqueResourceNaming](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfDocument.html#Syncfusion_Pdf_PdfDocument_EnableUniqueResourceNaming) property available in the [PdfDocument](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfDocument.html) instance. By default, the resource naming is added uniquely. Disabling the ```EnableUniqueResourceNaming``` property will create a PDF document with uniform resource names.

The following code snippet explains how to have uniform resource naming in a PDF document.

{% tabs %}
{% highlight c# tabtitle="C#" %}
//Disable unique resource naming
PdfDocument.EnableUniqueResourceNaming = false;

//Create a new PDF document
PdfDocument doc = new PdfDocument();
//Add a page to the document
PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;
//Create new instance for PDF font
PdfFont font1 = new PdfStandardFont(PdfFontFamily.Helvetica, 20);
//Draw the text
graphics.DrawString("Hello World!!!", font1, PdfBrushes.Blue, new PointF(50, 50));
//Create new instance for PDF font
PdfFont font2 = new PdfTrueTypeFont(new Font("Arial", 20), true);
//Draw the text
graphics.DrawString("Hello World!!!", font2, PdfBrushes.Blue, new PointF(50, 100));
//Create new instance for PDF font
PdfFont font3 = new PdfCjkStandardFont(PdfCjkFontFamily.HeiseiMinchoW3, 20);     
//Draw the text
graphics.DrawString("こんにちは世界", font3, PdfBrushes.Blue, new PointF(50, 150));

//Save and close the document
doc.Save("Output.pdf");
doc.Close(true);
{%endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Disable unique resource naming
PdfDocument.EnableUniqueResourceNaming = False

'Create a new PDF document
Dim doc As PdfDocument = New PdfDocument
'Add a page to the document
Dim page As PdfPage = doc.Pages.Add

'Create PDF graphics for the page
Dim graphics As PdfGraphics = page.Graphics
'Create new instance for PDF font
Dim font1 As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 20)
'Draw the text
graphics.DrawString("Hello World!!!", font1, PdfBrushes.Blue, New PointF(50, 50))
'Create new instance for PDF font
Dim font2 As PdfFont = New PdfTrueTypeFont(New Font("Arial", 20), True)
'Draw the text
graphics.DrawString("Hello World!!!", font2, PdfBrushes.Blue, New PointF(50, 100))
'Create new instance for PDF font
Dim font3 As PdfFont = New PdfCjkStandardFont(PdfCjkFontFamily.HeiseiMinchoW3, 20)
'Draw the text
graphics.DrawString("こんにちは世界", font3, PdfBrushes.Blue, New PointF(50, 150))

'Save and close the document
doc.Save("Output.pdf")
doc.Close(True)
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Disable unique resource naming
PdfDocument.EnableUniqueResourceNaming = false;

//Create a new PDF document
PdfDocument doc = new PdfDocument();
//Add a page to the document
PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;
//Create new instance for PDF font
PdfFont font1 = new PdfStandardFont(PdfFontFamily.Helvetica, 20);
//Draw the text
graphics.DrawString("Hello World!!!", font1, PdfBrushes.Blue, new PointF(50, 50));
//Create new instance for PDF font
Stream fontStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Arial.ttf");
PdfFont font2 = new PdfTrueTypeFont(fontStream, 20);
//Draw the text
graphics.DrawString("Hello World!!!", font2, PdfBrushes.Blue, new PointF(50, 100));
//Create new instance for PDF font
PdfFont font3 = new PdfCjkStandardFont(PdfCjkFontFamily.HeiseiMinchoW3, 20);
//Draw the text
graphics.DrawString("こんにちは世界", font3, PdfBrushes.Blue, new PointF(50, 150));

//Create memory stream
MemoryStream ms = new MemoryStream();
//Open the document in browser after saving it
doc.Save(ms);
//Close the document
doc.Close(true);
//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respective code samples
Save(ms, "Output.pdf");
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Disable unique resource naming
PdfDocument.EnableUniqueResourceNaming = false;

//Create a new PDF document
PdfDocument doc = new PdfDocument();
//Add a page to the document
PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;
//Create new instance for PDF font
PdfFont font1 = new PdfStandardFont(PdfFontFamily.Helvetica, 20);
//Draw the text
graphics.DrawString("Hello World!!!", font1, PdfBrushes.Blue, new PointF(50, 50));
//Create new instance for PDF font
FileStream fontStream = new FileStream("Arial.ttf", FileMode.Open, FileAccess.Read);
PdfFont font2 = new PdfTrueTypeFont(fontStream, 20);
//Draw the text
graphics.DrawString("Hello World!!!", font2, PdfBrushes.Blue, new PointF(50, 100));
//Create new instance for PDF font
PdfFont font3 = new PdfCjkStandardFont(PdfCjkFontFamily.HeiseiMinchoW3, 20);
//Draw the text
graphics.DrawString("こんにちは世界", font3, PdfBrushes.Blue, new PointF(50, 150));

//Saving the PDF to the MemoryStream
MemoryStream stream = new MemoryStream();
doc.Save(stream);
//Set the position as '0'
stream.Position = 0;

//Download the PDF document in the browser
FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");
fileStreamResult.FileDownloadName = "Output.pdf";
return fileStreamResult;
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Disable unique resource naming
PdfDocument.EnableUniqueResourceNaming = false;

//Create a new PDF document
PdfDocument doc = new PdfDocument();
//Add a page to the document
PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;
//Create new instance for PDF font
PdfFont font1 = new PdfStandardFont(PdfFontFamily.Helvetica, 20);
//Draw the text
graphics.DrawString("Hello World!!!", font1, PdfBrushes.Blue, new PointF(50, 50));
//Create new instance for PDF font
Stream fontStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Arial.ttf");
PdfFont font2 = new PdfTrueTypeFont(fontStream, 20);
//Draw the text
graphics.DrawString("Hello World!!!", font2, PdfBrushes.Blue, new PointF(50, 100));
//Create new instance for PDF font
PdfFont font3 = new PdfCjkStandardFont(PdfCjkFontFamily.HeiseiMinchoW3, 20);
//Draw the text
graphics.DrawString("こんにちは世界", font3, PdfBrushes.Blue, new PointF(50, 150));

//Save the document to the stream
MemoryStream stream = new MemoryStream();
doc.Save(stream);
//Close the document
doc.Close(true);

//Save the stream into PDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}
{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/PDF%20Document/Create_PDF_with_Uniform_Resouce_Naming/). 

## Memory Optimization

Essential PDF provides support for optimization of memory using [EnableMemoryOptimization](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfDocumentBase.html#Syncfusion_Pdf_PdfDocumentBase_EnableMemoryOptimization) property in [PdfDocument](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfDocument.html) instance. Optimization will be effective only with merge, append and import functions. 

Enabling this property will optimize the memory but difference in time occurs based on the document size. This is illustrated in the following code sample.

{% tabs %}
{% highlight c# tabtitle="C#" %}
//Load an existing PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("file1.pdf");

//Create a new PDF document
PdfDocument document = new PdfDocument();

//Enable memory optimization
document.EnableMemoryOptimization = true;
//Append the document with source document
document.Append(loadedDocument);

//Save the PDF document
document.Save("Output.pdf");
//Close the documents
document.Close(true);
loadedDocument.Close(true);
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Load an existing PDF document
Dim loadedDocument As New PdfLoadedDocument("file1.pdf")

'Create a new PDF document
Dim document As New PdfDocument()

'Enable memory optimization
document.EnableMemoryOptimization = True
'Append the document with source document
document.Append(loadedDocument)

'Save the PDF document
document.Save("Output.pdf")
'Close the documents
document.Close(True)
loadedDocument.Close(True)
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Create the file open picker
var picker = new FileOpenPicker();
picker.FileTypeFilter.Add(".pdf");
//Browse and choose the file
StorageFile file = await picker.PickSingleFileAsync();

//Create an empty PDF loaded document instance
PdfLoadedDocument loadedDocument = new PdfLoadedDocument();

//Load an existing PDF document through Open method of PdfLoadedDocument class
await loadedDocument.OpenAsync(file);
//Create a new PDF document
PdfDocument document = new PdfDocument();
//Enable memory optimization
document.EnableMemoryOptimization = true;
//Append the document with source document
document.Append(loadedDocument);

//Save the PDF document to stream
MemoryStream stream = new MemoryStream();
Await document.SaveAsync(stream);
//Close the documents
document.Close(true);
loadedDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples
Save(stream, "Output.pdf");
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Load an existing PDF document
FileStream docStream = new FileStream("file1.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Create a new PDF document
PdfDocument document = new PdfDocument();

//Enable memory optimization
document.EnableMemoryOptimization = true;
//Append the document with source document
document.Append(loadedDocument);

//Save the document into stream
MemoryStream stream = new MemoryStream();
document.Save(stream);
stream.Position = 0;
//Close the documents
document.Close(true);
loadedDocument.Close(true);

//Defining the content type for PDF file
string contentType = "application/pdf";
//Define the file name
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name
return File(stream, contentType, fileName);
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Load the file as stream
Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.file1.pdf");
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Create a new PDF document
PdfDocument document = new PdfDocument();

//Enable memory optimization
document.EnableMemoryOptimization = true;
//Append the document with source document
document.Append(loadedDocument);

//Save the PDF document to stream
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Close the documents
document.Close(true);
loadedDocument.Close(true);

//Save the stream into PDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.RuntimePlatform == Device.UWP)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}
{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/PDF%20Document/Manage_memory_while_appending_PDF_document/). 

## Find corrupted PDF document   

Syncfusion PDF Library provides support to check whether the existing PDF document is corrupted or not with corruption details using [PdfDocumentAnalyzer](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfDocumentAnalyzer.html) class. The following code snippet explains how to find the corrupted PDF document.

{% tabs %}
{% highlight c# tabtitle="C#" %}
//Create a new instance for the PDF analyzer
PdfDocumentAnalyzer analyzer = new PdfDocumentAnalyzer("Input.pdf");

//Get the syntax errors
SyntaxAnalyzerResult result = analyzer.AnalyzeSyntax();
//Check whether the document is corrupted or not
if (result.IsCorrupted)
{
   //Get syntax error details from results.error
   StringBuilder builder = new StringBuilder();
   builder.AppendLine("The PDF document is corrupted.");
   int count = 1;
   foreach (PdfException exception in result.Errors)
   {
     builder.AppendLine(count++.ToString() + ": " + exception.Message);
   }
}
else               
{
   //No syntax error found in the provided PDF document
}             
analyzer.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Create a new instance for the PDF analyzer
Dim analyzer As PdfDocumentAnalyzer = New PdfDocumentAnalyzer("Input.pdf")

'Get the syntax errors
Dim result As SyntaxAnalyzerResult = analyzer.AnalyzeSyntax

'Check whether the document is corrupted or not
If result.IsCorrupted Then
   'Get syntax error details from results.error
    builder = New StringBuilder
    builder.AppendLine("The PDF document is corrupted.")
    Dim count = 1
    For Each exception As PdfException In result.Errors
         builder.AppendLine(Math.Min(Threading.Interlocked.Increment(count), count - 1).ToString & ": " & exception.Message)
    Next

Else
   'No syntax error found in the provided PDF document.
End If
analyzer.Close()
{% endhighlight %}

  {% highlight c# tabtitle="UWP" %}
//Load the PDF document as stream 
Stream pdfStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Input.pdf");                                                                                                               
             
//Create a new instance for the PDF analyzer
PdfDocumentAnalyzer analyzer = new PdfDocumentAnalyzer(pdfStream);

//Get the syntax errors.
SyntaxAnalyzerResult result = analyzer.AnalyzeSyntax();
//Check whether the document is corrupted or not
if (result.IsCorrupted)
{
     //Get syntax error details from results.error
     StringBuilder builder = new StringBuilder();
     builder.AppendLine("The PDF document is corrupted.");
     int count = 1;
     foreach (PdfException exception in result.Errors)
     {
        builder.AppendLine(count++.ToString() + ": " + exception.Message);
     }              
}
else               
{
      //No syntax error found in the provided PDF document
}                    
analyzer.Close();
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Load the PDF document 
FileStream  docStream = new  FileStream("Input.pdf", FileMode.Open, FileAccess.Read); 

//Create a new instance for the PDF analyzer
PdfDocumentAnalyzer analyzer = new PdfDocumentAnalyzer(docStream);

//Get the syntax errors
SyntaxAnalyzerResult result = analyzer.AnalyzeSyntax();
//Check whether the document is corrupted or not
if (result.IsCorrupted)
{
    //Get syntax error details from results.error
    StringBuilder builder = new StringBuilder();
    builder.AppendLine("The PDF document is corrupted.");
    int count = 1;
    foreach (PdfException exception in result.Errors)
    {
       builder.AppendLine(count++.ToString() + ": " + exception.Message);
    }              
    
}
else               
{
    //No syntax error found in the provided PDF document
}                    
analyzer.Close();
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Load the PDF document as stream 
Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");

//Create a new instance for the PDF analyzer
PdfDocumentAnalyzer analyzer = new PdfDocumentAnalyzer(docStream);

//Get the syntax errors
SyntaxAnalyzerResult result = analyzer.AnalyzeSyntax();
//Check whether the document is corrupted or not
if (result.IsCorrupted)
{
    //Get syntax error details from results.error
    StringBuilder builder = new StringBuilder();
    builder.AppendLine("The PDF document is corrupted.");
    int count = 1;
    foreach (PdfException exception in result.Errors)
    {
       builder.AppendLine(count++.ToString() + ": " + exception.Message);
    }              
}
else               
{
    //No syntax error found in the provided PDF document
}                    
analyzer.Close();
{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/PDF%20Document/Find_corrupted_PDF_document/). 

## Embed all the non-embedded fonts in the existing PDF document  

You can embed all the non-embedded fonts in the existing PDF document using the [EmbedFonts](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html#Syncfusion_Pdf_Parsing_PdfLoadedDocument_EmbedFonts) method. 
Refer to the following code sample to achieve the same,

{% tabs %}
{% highlight C# %}
//Load an existing document.
PdfLoadedDocument document = new PdfLoadedDocument("input.pdf");
//Embed all the non-embedded fonts.
if (loadedDocument.IsAllFontsEmbedded == false)
{.
     loadedDocument.EmbedFonts();
}
//Save the document.
document.Save("Output.pdf");
//Close the document.
document.Close(true);
{% endhighlight %}

{% highlight vb.net %}
//Load an existing document.
Dim document As PdfLoadedDocument = New PdfLoadedDocument("input.pdf")
// Embed all the non-embedded fonts.
If loadedDocument.IsAllFontsEmbedded = False Then
    loadedDocument.EmbedFonts()
End If
//Save the document.
document.Save("Output.pdf")
//Close the document.
document.Close(True)
{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/PDF%20Document/Embed-all-fonts-in-an-existing-PDF-document/). 

## Add or retrieve BaseUri in a PDF document

The Essential PDF allows you to get or set the [BaseUri](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfDocumentBase.html#Syncfusion_Pdf_PdfDocumentBase_BaseUri) in the PDF document. This is illustrated in the following code sample.

{% tabs %}
{% highlight C# %}
//Create a new instance of the PdfDocument class.
PdfDocument document = new PdfDocument();
//Set the Base URI.
document.BaseUri = "https://www.syncfusion.com/";
//Create a new page.
PdfPage page = document.Pages.Add();

//Save the document.
document.Save("Output.pdf");
//Close the document.
document.Close(true);
{% endhighlight %}

{% highlight vb.net %}
'Create a new instance of the PdfDocument class.
Dim document As PdfDocument = New PdfDocument()
'Set the Base URI.
document.BaseUri = "https://www.syncfusion.com/"
'Create a new page.
Dim page As PdfPage = document.Pages.Add()

'Save the document.
document.Save("Output.pdf")
'Close the document.
document.Close(True)
{% endhighlight %}

{% highlight UWP %}
//Create a new instance of the PdfDocument class.
PdfDocument document = new PdfDocument();
//Set the Base URI.
document.BaseUri = "https://www.syncfusion.com/";
//Create a new page.
PdfPage page = document.Pages.Add();

//Save the document as stream.
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream);
//Close the document.
document.Close(true);
{% endhighlight %}

{% highlight ASP.NET Core %}
//Create a new instance of the PdfDocument class.
PdfDocument document = new PdfDocument();
//Set the Base URI.
document.BaseUri = "https://www.syncfusion.com/";
//Create a new page.
PdfPage page = document.Pages.Add();

//Save the document.
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Close the document.
document.Close(true);
{% endhighlight %}

{% highlight Xamarin %}
//Create a new instance of the PdfDocument class.
PdfDocument document = new PdfDocument();
//Set the Base URI.
document.BaseUri = "https://www.syncfusion.com/";
//Create a new page.
PdfPage page = document.Pages.Add();

//Save the document.
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Close the document.
document.Close(true);
{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/PDF%20Document/Add_BaseUri_in_the_PDF_document/). 

The following code example illustrates the retrieval of [BaseUri](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfDocumentBase.html#Syncfusion_Pdf_PdfDocumentBase_BaseUri) from the loaded document.

{% tabs %}
{% highlight C# %}
//Load an existing document.
PdfLoadedDocument document = new PdfLoadedDocument("Input.pdf");

//Get the Base URI.
string baseUri = document.BaseUri;

//Close the document.
document.Close(true);
{% endhighlight %}

{% highlight vb.net %}
'Load an existing document.
Dim document As PdfLoadedDocument = New PdfLoadedDocument("Input.pdf")
'Get the Base URI.
Dim baseUri As String = document.BaseUri
'Close the document.
document.Close(True)
{% endhighlight %}

{% highlight UWP %}
//Load the PDF document as stream.
Stream pdfStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Input.pdf");
//Create an empty PDF loaded document instance.
PdfLoadedDocument document = new PdfLoadedDocument();
//Load or open an existing PDF document through the Open method of the PdfLoadedDocument class
await document.OpenAsync(pdfStream);
//Get the Base URI.
string baseUri = document.BaseUri;
//Close the document.
document.Close(true);
{% endhighlight %}

{% highlight ASP.NET Core %}
//Load the PDF document as file stream.
FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);
//Load a PDF document.
PdfLoadedDocument document = new PdfLoadedDocument(docStream);
//Get the Base URI.
string baseUri = document.BaseUri;
//Close the document.
document.Close(true);
{% endhighlight %}

{% highlight Xamarin %}
//Load the file as stream.
Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");

//Load the file stream.
PdfLoadedDocument document = new PdfLoadedDocument(docStream);
//Get the Base URI.
string baseUri = document.BaseUri;
//Close the document.
document.Close(true);
{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/PDF%20Document/Retrieve_BaseUri_from_the_existing_PDF/). 
