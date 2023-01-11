---
title: Working with PDF conformance | Syncfusion
description: This section explains how to create a PDF conformance documents and convert PDF to PDF/A conformance document.
platform: file-formats
control: PDF
documentation: UG
---
# Working with PDF Conformance

The Essential PDF currently supports the following PDF conformances:

* PDF/A-1a conformance
* PDF/A-1b conformance
* PDF/X-1a conformance
* PDF/A-2a conformance
* PDF/A-2b conformance
* PDF/A-2u conformance
* PDF/A-3a conformance
* PDF/A-3b conformance
* PDF/A-3u conformance
* PDF/A-4 conformance
* PDF/A-4e conformance
* PDF/A-4f conformance

N> 1. To know more details about PDF/A standard refer [https://en.wikipedia.org/wiki/PDF/A#Description](https://en.wikipedia.org/wiki/PDF/A#Description )
N> 2. To know more details about PDF/X standard refer [https://en.wikipedia.org/wiki/PDF/X](https://en.wikipedia.org/wiki/PDF/X)

N> Essential PDF supports PDF conformances only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

## PDF/A-1b conformance

You can create a PDF/A-1b document by specifying the conformance level as ```Pdf_A1B``` through [PdfConformanceLevel](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfConformanceLevel.html) Enum when creating the new PDF document, as shown below.

{% tabs %} 

{% highlight c# tabtitle="C#" %}

//Create a new document with PDF/A-1b standard.
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A1B);
//Add a page.
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;

//Create a solid brush.
PdfBrush brush = new PdfSolidBrush(Color.Black);
//Set the font.
Font font = new Font("Arial", 20f, FontStyle.Regular);
PdfFont pdfFont = new PdfTrueTypeFont(font, FontStyle.Regular, 12, false, true);

//Draw the text.
graphics.DrawString("Hello world!", pdfFont, brush, new PointF(20, 20));

//Save and close the document.
document.Save("Output.pdf");
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new document with PDF/A-1b standard.
Dim document As New PdfDocument(PdfConformanceLevel.Pdf_A1B)
'Add a page.
Dim page As PdfPage = document.Pages.Add()
'Create PDF graphics for the page.
Dim graphics As PdfGraphics = page.Graphics

'Create a solid brush.
Dim brush As PdfBrush = New PdfSolidBrush(Color.Black)
'Set the font.
Dim font As New Font("Arial", 20.0F, FontStyle.Regular)
Dim pdfFont As PdfFont = New PdfTrueTypeFont(font, FontStyle.Regular, 12, False, True)

'Draw the text.
graphics.DrawString("Hello world!", pdfFont, brush, New PointF(20, 20))

'Save and close the document.
document.Save("Output.pdf")
document.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Create a new document with PDF/A-1b standard
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A1B);
//Add a page to the document
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Load the TrueType font from the local file
Stream fontStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Arial.ttf");
//Initialize the PDF TrueType font
PdfFont font = new PdfTrueTypeFont(fontStream, 14);

//Draw the text
graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

//Save the document into memory stream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream);
//Close the document
document.Close(true);
//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respected code samples
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a new document with PDF/A-1b standard
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A1B);
//Add a page to the document
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Load the TrueType font from the local file
FileStream fontStream = new FileStream("Arial.ttf", FileMode.Open, FileAccess.Read);
PdfFont font = new PdfTrueTypeFont(fontStream, 14);

//Draw the text
graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new Syncfusion.Drawing.PointF(0, 0));

//Creating the stream object
MemoryStream stream = new MemoryStream();
//Save the document into memory stream
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

{% highlight c# tabtitle="Xamarin" %}

//Create a new document with PDF/A-1b standard
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A1B);
//Add a page to the document
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Load the TrueType font
Stream fontStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Arial.ttf");
//Initialize the PDF TrueType font 
PdfFont font = new PdfTrueTypeFont(fontStream, 14);

//Draw the text
graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new Syncfusion.Drawing.PointF(0, 0));

//Save the document into memory stream
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Close the document
document.Close(true);
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/PDF%20Conformance/Creating-the-new-PDFA1B-document).

## PDF/A-2b conformance

You can create a PDF/A-2b document by specifying the conformance level as ```Pdf_A2B``` through [PdfConformanceLevel](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfConformanceLevel.html) Enum when creating the new PDF document as follows.

{% tabs %}  

{% highlight c# tabtitle="C#" %}

//Create a new document with PDF/A-2b standard
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A2B);
//Add a page
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Create a solid brush
PdfBrush brush = new PdfSolidBrush(Color.Black);
//Set the font
Font font = new Font("Arial", 20f, FontStyle.Regular);
PdfFont pdfFont = new PdfTrueTypeFont(font, FontStyle.Regular, 12, false, true);

//Draw the text
graphics.DrawString("Hello world!", pdfFont, brush, new PointF(20, 20));

//Save and close the document
document.Save("Output.pdf");
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new document with PDF/A-2b standard
Dim document As New PdfDocument(PdfConformanceLevel.Pdf_A2B)
'Add a page
Dim page As PdfPage = document.Pages.Add()
'Create PDF graphics for the page
Dim graphics As PdfGraphics = page.Graphics

'Create a solid brush
Dim brush As PdfBrush = New PdfSolidBrush(Color.Black)
'Set the font
Dim font As New Font("Arial", 20.0F, FontStyle.Regular)
Dim pdfFont As PdfFont = New PdfTrueTypeFont(font, FontStyle.Regular, 12, False, True)

'Draw the text
graphics.DrawString("Hello world!", pdfFont, brush, New PointF(20, 20))

'Save and close the document
document.Save("Output.pdf")
document.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Create a new document with PDF/A-2b standard
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A2B);
//Add a page to the document
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Load the TrueType font from the local file
Stream fontStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Arial.ttf");
//Initialize the PDF TrueType font
PdfFont font = new PdfTrueTypeFont(fontStream, 14);

//Draw the text
graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

//Save the document into memory stream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream);
//Close the document
document.Close(true);
//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a new document with PDF/A-2b standard
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A2B);
//Add a page to the document
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Load the TrueType font from the local file
FileStream fontStream = new FileStream("Arial.ttf", FileMode.Open, FileAccess.Read);
PdfFont font = new PdfTrueTypeFont(fontStream, 14);

//Draw the text
graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new Syncfusion.Drawing.PointF(0, 0));

//Creating the stream object
MemoryStream stream = new MemoryStream();
//Save the document into memory stream
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

{% highlight c# tabtitle="Xamarin" %}

//Create a new document with PDF/A-2b standard
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A2B);
//Add a page to the document
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Load the TrueType font
Stream fontStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Arial.ttf");
//Initialize the PDF TrueType font 
PdfFont font = new PdfTrueTypeFont(fontStream, 14);

//Draw the text
graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new Syncfusion.Drawing.PointF(0, 0));

//Save the document into memory stream
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Close the document
document.Close(true);
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/PDF%20Conformance/Creating-the-new-PDFA2B-document).

## PDF/A-3b conformance

The PDF/A-3b conformance supports the external files as attachment to the PDF document. So you can attach any document format such as Excel, Word, HTML, CAD, or XML files.

You can create a PDF/A-3b document by specifying the conformance level as Pdf_A3B through [PdfConformanceLevel](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfConformanceLevel.html) Enum when creating the new PDF document as follows.

{% tabs %}  

{% highlight c# tabtitle="C#" %}

//Create a new document with PDF/A-3b standard
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A3B);
//Add a page
PdfPage page = document.Pages.Add();

//Creates an attachment
PdfAttachment attachment = new PdfAttachment("Input.txt");
attachment.Relationship = PdfAttachmentRelationship.Alternative;
attachment.ModificationDate = DateTime.Now;
attachment.Description = "Input.txt";
attachment.MimeType = "application/txt";
//Adds the attachment to the document
document.Attachments.Add(attachment);

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;
//Create a solid brush
PdfBrush brush = new PdfSolidBrush(Color.Black);
Font font = new Font("Arial", 20f, FontStyle.Regular);
//Set the font
PdfFont pdfFont = new PdfTrueTypeFont(font, FontStyle.Regular, 12, false, true);
//Draw the text
graphics.DrawString("Hello world!", pdfFont, brush, new PointF(20, 20));

//Save and close the document
document.Save("Output.pdf");
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new document with PDF/A-3b standard
Dim document As New PdfDocument(PdfConformanceLevel.Pdf_A3B)
'Add a page
Dim page As PdfPage = document.Pages.Add()

'Creates an attachment
Dim attachment As New PdfAttachment("Input.txt")
attachment.Relationship = PdfAttachmentRelationship.Alternative
attachment.ModificationDate = DateTime.Now
attachment.Description = "Input.txt"
attachment.MimeType = "application/txt"
'Adds the attachment to the document
document.Attachments.Add(attachment)

'Create PDF graphics for the page
Dim graphics As PdfGraphics = page.Graphics
'Create a solid brush
Dim brush As PdfBrush = New PdfSolidBrush(Color.Black)
Dim font As New Font("Arial", 20.0F, FontStyle.Regular)
'Set the font
Dim pdfFont As PdfFont = New PdfTrueTypeFont(font, FontStyle.Regular, 12, False, True)
'Draw the text
graphics.DrawString("Hello world!", pdfFont, brush, New PointF(20, 20))

'Save and close the document
document.Save("Output.pdf")
document.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Create a new document with PDF/A-3b standard
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A3B);
//Add a page to the document
PdfPage page = document.Pages.Add();

//Creates an attachment
Stream fileStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Input.txt");
PdfAttachment attachment = new PdfAttachment(@"Input.txt", fileStream);
attachment.Relationship = PdfAttachmentRelationship.Alternative;
attachment.ModificationDate = DateTime.Now;
attachment.Description = "Input.txt";
attachment.MimeType = "application/txt";
//Adds the attachment to the document
document.Attachments.Add(attachment);

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;
//Load the TrueType font from the local file
Stream fontStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Arial.ttf");
//Initialize the PDF TrueType font
PdfFont font = new PdfTrueTypeFont(fontStream, 14);
//Draw the text
graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

//Save the document into memory stream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream);
//Close the document
document.Close(true);
//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respected code samples
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a new document with PDF/A-3b standard
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A3B);
//Add a page to the document
PdfPage page = document.Pages.Add();

//Creates an attachment
Stream fileStream = new FileStream("Input.txt", FileMode.Open, FileAccess.Read);
PdfAttachment attachment = new PdfAttachment("Input.txt", fileStream);
attachment.Relationship = PdfAttachmentRelationship.Alternative;
attachment.ModificationDate = DateTime.Now;
attachment.Description = "Input.txt";
attachment.MimeType = "application/txt";
//Adds the attachment to the document
document.Attachments.Add(attachment);

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;
//Load the TrueType font from the local file
FileStream fontStream = new FileStream("Arial.ttf", FileMode.Open, FileAccess.Read);
PdfFont font = new PdfTrueTypeFont(fontStream, 14);
//Draw the text
graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new Syncfusion.Drawing.PointF(0, 0));

//Creating the stream object
MemoryStream stream = new MemoryStream();
//Save the document into memory stream
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

{% highlight c# tabtitle="Xamarin" %}

//Create a new document with PDF/A-3b standard
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A3B);
//Add a page to the document
PdfPage page = document.Pages.Add();

//Creates an attachment
Stream fileStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.txt");
PdfAttachment attachment = new PdfAttachment("Input.txt", fileStream);
attachment.Relationship = PdfAttachmentRelationship.Alternative;
attachment.ModificationDate = DateTime.Now;
attachment.Description = "Input.txt";
attachment.MimeType = "application/txt";
//Adds the attachment to the document
document.Attachments.Add(attachment);

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;
//Load the TrueType font
Stream fontStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Arial.ttf");
//Initialize the PDF TrueType font 
PdfFont font = new PdfTrueTypeFont(fontStream, 14);
//Draw the text
graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new Syncfusion.Drawing.PointF(0, 0));

//Save the document into memory stream
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Close the document
document.Close(true);
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/PDF%20Conformance/Creating-the-new-PDFA3B-document).

## PDF/A-1a conformance

PDF/A-1a conformance includes all PDF/A-1b requirements in addition to the features intended to improve a document's accessibility. PDF/A-1a conformance additionally have crucial properties of Tagged PDF.

You can create a PDF/A-1a document by specifying the conformance level as ```Pdf_A1A``` through [PdfConformanceLevel](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfConformanceLevel.html) Enum when creating the new PDF document, as shown below.

{% tabs %} 

{% highlight c# tabtitle="C#" %}

//Create a new document with PDF/A-1a standard.
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A1A);
//Add a page.
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;

//Create a solid brush.
PdfBrush brush = new PdfSolidBrush(Color.Black);
//Set the font.
Font font = new Font("Arial", 20f, FontStyle.Regular);
PdfFont pdfFont = new PdfTrueTypeFont(font, FontStyle.Regular, 12, false, true);
//Draw the text.
graphics.DrawString("Hello world!", pdfFont, brush, new PointF(20, 20));

//Save and close the document.
document.Save("Output.pdf");
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new document with PDF/A-1a standard.
Dim document As New PdfDocument(PdfConformanceLevel.Pdf_A1A)
'Add a page.
Dim page As PdfPage = document.Pages.Add()
'Create PDF graphics for the page.
Dim graphics As PdfGraphics = page.Graphics

'Create a solid brush.
Dim brush As PdfBrush = New PdfSolidBrush(Color.Black)
'Set the font.
Dim font As New Font("Arial", 20.0F, FontStyle.Regular)
Dim pdfFont As PdfFont = New PdfTrueTypeFont(font, FontStyle.Regular, 12, False, True)
'Draw the text.
graphics.DrawString("Hello world!", pdfFont, brush, New PointF(20, 20))

'Save and close the document.
document.Save("Output.pdf")
document.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Create a new document with PDF/A-1a standard
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A1A);
//Add a page to the document
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Load the TrueType font from the local file
Stream fontStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Arial.ttf");
//Initialize the PDF TrueType font
PdfFont font = new PdfTrueTypeFont(fontStream, 14);
//Draw the text
graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

//Save the document into memory stream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream);
//Close the document
document.Close(true);
//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respected code samples
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a new document with PDF/A-1a standard
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A1A);
//Add a page to the document
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Load the TrueType font from the local file
FileStream fontStream = new FileStream("Arial.ttf", FileMode.Open, FileAccess.Read);
PdfFont font = new PdfTrueTypeFont(fontStream, 14);
//Draw the text
graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new Syncfusion.Drawing.PointF(0, 0));

//Creating the stream object
MemoryStream stream = new MemoryStream();
//Save the document into memory stream
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

{% highlight c# tabtitle="Xamarin" %}

//Create a new document with PDF/A-1a standard
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A1A);
//Add a page to the document
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Load the TrueType font
Stream fontStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Arial.ttf");
//Initialize the PDF TrueType font 
PdfFont font = new PdfTrueTypeFont(fontStream, 14);
//Draw the text
graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new Syncfusion.Drawing.PointF(0, 0));

//Save the document into memory stream
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Close the document
document.Close(true);
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/PDF%20Conformance/Creating-the-new-PDFA1A-document).

## PDF/A-2a conformance

PDF/A-2a conformance includes all PDF/A-2b requirements in addition to the features intended to improve a document's accessibility. PDF/A-2a conformance additionally have crucial properties of Tagged PDF.

You can create a PDF/A-2a document by specifying the conformance level as ```Pdf_A2A``` through [PdfConformanceLevel](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfConformanceLevel.html) Enum when creating the new PDF document as follows.

{% tabs %}  

{% highlight c# tabtitle="C#" %}

//Create a new document with PDF/A-2a standard
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A2A);
//Add a page
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Create a solid brush
PdfBrush brush = new PdfSolidBrush(Color.Black);
//Set the font
Font font = new Font("Arial", 20f, FontStyle.Regular);
PdfFont pdfFont = new PdfTrueTypeFont(font, FontStyle.Regular, 12, false, true);
//Draw the text
graphics.DrawString("Hello world!", pdfFont, brush, new PointF(20, 20));

//Save and close the document
document.Save("Output.pdf");
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new document with PDF/A-2a standard
Dim document As New PdfDocument(PdfConformanceLevel.Pdf_A2A)
'Add a page
Dim page As PdfPage = document.Pages.Add()
'Create PDF graphics for the page
Dim graphics As PdfGraphics = page.Graphics

'Create a solid brush
Dim brush As PdfBrush = New PdfSolidBrush(Color.Black)
'Set the font
Dim font As New Font("Arial", 20.0F, FontStyle.Regular)
Dim pdfFont As PdfFont = New PdfTrueTypeFont(font, FontStyle.Regular, 12, False, True)
'Draw the text
graphics.DrawString("Hello world!", pdfFont, brush, New PointF(20, 20))

'Save and close the document
document.Save("Output.pdf")
document.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Create a new document with PDF/A-2a standard
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A2A);
//Add a page to the document
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Load the TrueType font from the local file
Stream fontStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Arial.ttf");
//Initialize the PDF TrueType font
PdfFont font = new PdfTrueTypeFont(fontStream, 14);
//Draw the text
graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

//Save the document into memory stream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream);
//Close the document
document.Close(true);
//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a new document with PDF/A-2a standard
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A2A);
//Add a page to the document
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Load the TrueType font from the local file
FileStream fontStream = new FileStream("Arial.ttf", FileMode.Open, FileAccess.Read);
PdfFont font = new PdfTrueTypeFont(fontStream, 14);
//Draw the text
graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new Syncfusion.Drawing.PointF(0, 0));

//Creating the stream object
MemoryStream stream = new MemoryStream();
//Save the document into memory stream
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

{% highlight c# tabtitle="Xamarin" %}

//Create a new document with PDF/A-2a standard
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A2A);
//Add a page to the document
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Load the TrueType font
Stream fontStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Arial.ttf");
//Initialize the PDF TrueType font 
PdfFont font = new PdfTrueTypeFont(fontStream, 14);
//Draw the text
graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new Syncfusion.Drawing.PointF(0, 0));

//Save the document into memory stream
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Close the document
document.Close(true);
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/PDF%20Conformance/Creating-the-new-PDFA2A-document).

## PDF/A-3a conformance

PDF/A-3a conformance includes all PDF/A-3b requirements in addition to the features intended to improve a document's accessibility. PDF/A-3a conformance additionally have crucial properties of Tagged PDF.

You can create a PDF/A-3a document by specifying the conformance level as ``Pdf_A3A`` through [PdfConformanceLevel](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfConformanceLevel.html) Enum when creating the new PDF document as follows.

{% tabs %}  

{% highlight c# tabtitle="C#" %}

//Create a new document with PDF/A-3a standard
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A3A);
//Add a page
PdfPage page = document.Pages.Add();

//Creates an attachment
PdfAttachment attachment = new PdfAttachment("Input.txt");
attachment.Relationship = PdfAttachmentRelationship.Alternative;
attachment.ModificationDate = DateTime.Now;
attachment.Description = "Input.txt";
attachment.MimeType = "application/txt";
//Adds the attachment to the document
document.Attachments.Add(attachment);

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Create a solid brush
PdfBrush brush = new PdfSolidBrush(Color.Black);
Font font = new Font("Arial", 20f, FontStyle.Regular);
//Set the font
PdfFont pdfFont = new PdfTrueTypeFont(font, FontStyle.Regular, 12, false, true);
//Draw the text
graphics.DrawString("Hello world!", pdfFont, brush, new PointF(20, 20));

//Save and close the document
document.Save("Output.pdf");
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new document with PDF/A-3a standard
Dim document As New PdfDocument(PdfConformanceLevel.Pdf_A3A)
'Add a page
Dim page As PdfPage = document.Pages.Add()

'Creates an attachment
Dim attachment As New PdfAttachment("Input.txt")
attachment.Relationship = PdfAttachmentRelationship.Alternative
attachment.ModificationDate = DateTime.Now
attachment.Description = "Input.txt"
attachment.MimeType = "application/txt"
'Adds the attachment to the document
document.Attachments.Add(attachment)

'Create PDF graphics for the page
Dim graphics As PdfGraphics = page.Graphics
'Create a solid brush
Dim brush As PdfBrush = New PdfSolidBrush(Color.Black)
'Set the font
Dim font As New Font("Arial", 20.0F, FontStyle.Regular)
Dim pdfFont As PdfFont = New PdfTrueTypeFont(font, FontStyle.Regular, 12, False, True)

'Draw the text
graphics.DrawString("Hello world!", pdfFont, brush, New PointF(20, 20))

'Save and close the document
document.Save("Output.pdf")
document.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Create a new document with PDF/A-3a standard
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A3A);
//Add a page to the document
PdfPage page = document.Pages.Add();

//Creates an attachment
Stream fileStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Input.txt");
PdfAttachment attachment = new PdfAttachment(@"Input.txt", fileStream);
attachment.Relationship = PdfAttachmentRelationship.Alternative;
attachment.ModificationDate = DateTime.Now;
attachment.Description = "Input.txt";
attachment.MimeType = "application/txt";
//Adds the attachment to the document
document.Attachments.Add(attachment);

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;
//Load the TrueType font from the local file
Stream fontStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Arial.ttf");
//Initialize the PDF TrueType font
PdfFont font = new PdfTrueTypeFont(fontStream, 14);
//Draw the text
graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

//Save the document into memory stream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream);
//Close the document
document.Close(true);
//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respected code samples
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a new document with PDF/A-3a standard
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A3A);
//Add a page to the document
PdfPage page = document.Pages.Add();

//Creates an attachment
Stream fileStream = new FileStream("Input.txt", FileMode.Open, FileAccess.Read);
PdfAttachment attachment = new PdfAttachment("Input.txt", fileStream);
attachment.Relationship = PdfAttachmentRelationship.Alternative;
attachment.ModificationDate = DateTime.Now;
attachment.Description = "Input.txt";
attachment.MimeType = "application/txt";
//Adds the attachment to the document
document.Attachments.Add(attachment);

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;
//Load the TrueType font from the local file
FileStream fontStream = new FileStream("Arial.ttf", FileMode.Open, FileAccess.Read);
PdfFont font = new PdfTrueTypeFont(fontStream, 14);
//Draw the text
graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new Syncfusion.Drawing.PointF(0, 0));

//Creating the stream object
MemoryStream stream = new MemoryStream();
//Save the document into memory stream
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

{% highlight c# tabtitle="Xamarin" %}

//Create a new document with PDF/A-3a standard
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A3A);
//Add a page to the document
PdfPage page = document.Pages.Add();

//Add the attachment
Stream fileStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.txt");
PdfAttachment attachment = new PdfAttachment("Input.txt", fileStream);
attachment.Relationship = PdfAttachmentRelationship.Alternative;
attachment.ModificationDate = DateTime.Now;
attachment.Description = "Input.txt";
attachment.MimeType = "application/txt";
//Adds the attachment to the document
document.Attachments.Add(attachment);

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;
//Load the TrueType font
Stream fontStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Arial.ttf");
//Initialize the PDF TrueType font 
PdfFont font = new PdfTrueTypeFont(fontStream, 14);
//Draw the text
graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new Syncfusion.Drawing.PointF(0, 0));

//Save the document into memory stream
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Close the document
document.Close(true);
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/PDF%20Conformance/Creating-the-new-PDFA3A-document).

## PDF/A-2u conformance

PDF/A-2u conformance includes all PDF/A-2b requirements, and additionally Unicode mapping for all text in the document. 

You can create a PDF/A-2u document by specifying the conformance level as ```Pdf_A2U``` through [PdfConformanceLevel](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfConformanceLevel.html) Enum when creating the new PDF document as follows.

{% tabs %}  

{% highlight c# tabtitle="C#" %}

//Create a new document with PDF/A-2u standard
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A2U);
//Add a page
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Create a solid brush
PdfBrush brush = new PdfSolidBrush(Color.Black);
Font font = new Font("Arial", 20f, FontStyle.Regular);
//Set the font
PdfFont pdfFont = new PdfTrueTypeFont(font, FontStyle.Regular, 12, false, true);
//Draw the text
graphics.DrawString("Hello world!", pdfFont, brush, new PointF(20, 20));

//Save and close the document
document.Save("Output.pdf");
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new document with PDF/A-2u standard
Dim document As New PdfDocument(PdfConformanceLevel.Pdf_A2U)
'Add a page
Dim page As PdfPage = document.Pages.Add()
'Create PDF graphics for the page
Dim graphics As PdfGraphics = page.Graphics

'Create a solid brush
Dim brush As PdfBrush = New PdfSolidBrush(Color.Black)
Dim font As New Font("Arial", 20.0F, FontStyle.Regular)
'Set the font
Dim pdfFont As PdfFont = New PdfTrueTypeFont(font, FontStyle.Regular, 12, False, True)
'Draw the text
graphics.DrawString("Hello world!", pdfFont, brush, New PointF(20, 20))

'Save and close the document
document.Save("Output.pdf")
document.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Create a new document with PDF/A-2u standard
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A2U);
//Add a page to the document
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Load the TrueType font from the local file
Stream fontStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Arial.ttf");
//Initialize the PDF TrueType font
PdfFont font = new PdfTrueTypeFont(fontStream, 14);
//Draw the text
graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

//Save the document into memory stream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream);
//Close the document
document.Close(true);
//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a new document with PDF/A-2u standard
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A2U);
//Add a page to the document
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Load the TrueType font from the local file
FileStream fontStream = new FileStream("Arial.ttf", FileMode.Open, FileAccess.Read);
PdfFont font = new PdfTrueTypeFont(fontStream, 14);
//Draw the text
graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new Syncfusion.Drawing.PointF(0, 0));

//Creating the stream object
MemoryStream stream = new MemoryStream();
//Save the document into memory stream
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

{% highlight c# tabtitle="Xamarin" %}

//Create a new document with PDF/A-2u standard
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A2U);
//Add a page to the document
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Load the TrueType font
Stream fontStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Arial.ttf");
//Initialize the PDF TrueType font 
PdfFont font = new PdfTrueTypeFont(fontStream, 14);
//Draw the text
graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new Syncfusion.Drawing.PointF(0, 0));

//Save the document into memory stream
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Close the document
document.Close(true);
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/PDF%20Conformance/Creating-the-new-PDFA2U-document).

## PDF/A-3u conformance

PDF/A-3u conformance includes all PDF/A-3b requirements, and additionally Unicode mapping for all text in the document. 

You can create a PDF/A-3u document by specifying the conformance level as ``Pdf_A3U`` through [PdfConformanceLevel](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfConformanceLevel.html) Enum when creating the new PDF document as follows.

{% tabs %}  

{% highlight c# tabtitle="C#" %}

//Create a new document with PDF/A-3u standard
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A3U);
//Add a page
PdfPage page = document.Pages.Add();

//Creates an attachment
PdfAttachment attachment = new PdfAttachment("Input.txt");
attachment.Relationship = PdfAttachmentRelationship.Alternative;
attachment.ModificationDate = DateTime.Now;
attachment.Description = "Input.txt";
attachment.MimeType = "application/txt";
//Adds the attachment to the document
document.Attachments.Add(attachment);

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;
//Create a solid brush
PdfBrush brush = new PdfSolidBrush(Color.Black);
//Set the font
Font font = new Font("Arial", 20f, FontStyle.Regular);
PdfFont pdfFont = new PdfTrueTypeFont(font, FontStyle.Regular, 12, false, true);

//Draw the text
graphics.DrawString("Hello world!", pdfFont, brush, new PointF(20, 20));

//Save and close the document
document.Save("Output.pdf");
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new document with PDF/A-3u standard
Dim document As New PdfDocument(PdfConformanceLevel.Pdf_A3U)
'Add a page
Dim page As PdfPage = document.Pages.Add()

'Creates an attachment
Dim attachment As New PdfAttachment("Input.txt")
attachment.Relationship = PdfAttachmentRelationship.Alternative
attachment.ModificationDate = DateTime.Now
attachment.Description = "Input.txt"
attachment.MimeType = "application/txt"
'Adds the attachment to the document
document.Attachments.Add(attachment)

'Create PDF graphics for the page
Dim graphics As PdfGraphics = page.Graphics
'Create a solid brush
Dim brush As PdfBrush = New PdfSolidBrush(Color.Black)
'Set the font
Dim font As New Font("Arial", 20.0F, FontStyle.Regular)
Dim pdfFont As PdfFont = New PdfTrueTypeFont(font, FontStyle.Regular, 12, False, True)

'Draw the text
graphics.DrawString("Hello world!", pdfFont, brush, New PointF(20, 20))

'Save and close the document
document.Save("Output.pdf")
document.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Create a new document with PDF/A-3u standard
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A3U);
//Add a page to the document
PdfPage page = document.Pages.Add();

//Creates an attachment
Stream fileStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Input.txt");
PdfAttachment attachment = new PdfAttachment(@"Input.txt", fileStream);
attachment.Relationship = PdfAttachmentRelationship.Alternative;
attachment.ModificationDate = DateTime.Now;
attachment.Description = "Input.txt";
attachment.MimeType = "application/txt";
//Adds the attachment to the document
document.Attachments.Add(attachment);

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;
//Load the TrueType font from the local file
Stream fontStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Arial.ttf");
//Initialize the PDF TrueType font
PdfFont font = new PdfTrueTypeFont(fontStream, 14);
//Draw the text
graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

//Save the document into memory stream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream);
//Close the document
document.Close(true);
//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respected code samples
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a new document with PDF/A-3u standard
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A3U);
//Add a page to the document
PdfPage page = document.Pages.Add();

//Creates an attachment
Stream fileStream = new FileStream("Input.txt", FileMode.Open, FileAccess.Read);
PdfAttachment attachment = new PdfAttachment("Input.txt", fileStream);
attachment.Relationship = PdfAttachmentRelationship.Alternative;
attachment.ModificationDate = DateTime.Now;
attachment.Description = "Input.txt";
attachment.MimeType = "application/txt";
//Adds the attachment to the document
document.Attachments.Add(attachment);

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;
//Load the TrueType font from the local file
FileStream fontStream = new FileStream("Arial.ttf", FileMode.Open, FileAccess.Read);
PdfFont font = new PdfTrueTypeFont(fontStream, 14);
//Draw the text
graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new Syncfusion.Drawing.PointF(0, 0));

//Creating the stream object
MemoryStream stream = new MemoryStream();
//Save the document into memory stream
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

{% highlight c# tabtitle="Xamarin" %}

//Create a new document with PDF/A-3u standard
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A3U);
//Add a page to the document
PdfPage page = document.Pages.Add();

//Add the attachment
Stream fileStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.txt");
PdfAttachment attachment = new PdfAttachment("Input.txt", fileStream);
attachment.Relationship = PdfAttachmentRelationship.Alternative;
attachment.ModificationDate = DateTime.Now;
attachment.Description = "Input.txt";
attachment.MimeType = "application/txt";
//Adds the attachment to the document
document.Attachments.Add(attachment);

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;
//Load the TrueType font
Stream fontStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Arial.ttf");
//Initialize the PDF TrueType font 
PdfFont font = new PdfTrueTypeFont(fontStream, 14);
//Draw the text
graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new Syncfusion.Drawing.PointF(0, 0));

//Save the document into memory stream
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Close the document
document.Close(true);
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/PDF%20Conformance/Creating-the-new-PDFA3U-document).

## PDF/A-4 conformance

The separate conformance levels a, b, and u are not used in a PDF/A-4. Instead, PDF/A-4 encourages but does not require the addition of higher-level logical structures, and it requires Unicode mappings for all fonts.

Create a PDF/A-4 document by specifying the conformance level as ``Pdf_A4`` through the [PdfConformanceLevel](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfConformanceLevel.html) Enum when creating a new PDF document as follows.

{% tabs %}  

{% highlight c# tabtitle="C#" %}

//Create a new document with the PDF/A-4 standard. 
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A4);
//Add a page. 
PdfPage page = document.Pages.Add(); 
//Create the PDF graphics for the page. 
PdfGraphics graphics = page.Graphics; 

//Create a solid brush. 
PdfBrush brush = new PdfSolidBrush(Color.Black); 
//Set the font. 
Font font = new Font("Arial", 20f, FontStyle.Regular); 
PdfFont pdfFont = new PdfTrueTypeFont(font, FontStyle.Regular, 12, false, true); 
//Draw the text. 
graphics.DrawString("Hello world!", pdfFont, brush, new PointF(20, 20)); 

//Save and close the document. 
document.Save("Output.pdf"); 
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new document with the PDF/A-4 standard. 
Dim document As New PdfDocument(PdfConformanceLevel.Pdf_A4) 
'Add a page. 
Dim page As PdfPage = document.Pages.Add() 
'Create the PDF graphics for the page. 
Dim graphics As PdfGraphics = page.Graphics 

'Create a solid brush. 
Dim brush As PdfBrush = New PdfSolidBrush(Color.Black) 
'Set the font. 
Dim font As New Font("Arial", 20.0F, FontStyle.Regular) 
Dim pdfFont As PdfFont = New PdfTrueTypeFont(font, FontStyle.Regular, 12, False, True) 
'Draw the text. 
graphics.DrawString("Hello world!", pdfFont, brush, New PointF(20, 20)) 

'Save and close the document. 
document.Save("Output.pdf") 
document.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Create a new document with the PDF/A-4 standard. 
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A4); 
//Add a page to the document. 
PdfPage page = document.Pages.Add();
//Create the PDF graphics for the page. 
PdfGraphics graphics = page.Graphics; 

//Load the TrueType font from the local file. 
Stream fontStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Arial.ttf"); 
//Initialize the PDF TrueType font. 
PdfFont font = new PdfTrueTypeFont(fontStream, 14); 
//Draw the text. 
graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0)); 

//Save the document into the memory stream. 
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream); 
//Close the document. 
document.Close(true); 
//Save the stream as a PDF document file in the local machine. Refer to the PDF/UWP section for respective code samples. 
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a new document with the PDF/A-4 standard. 
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A4); 
//Add a page to the document. 
PdfPage page = document.Pages.Add();
//Create the PDF graphics for the page. 
PdfGraphics graphics = page.Graphics; 

//Load the TrueType font from the local file. 
FileStream fontStream = new FileStream("Arial.ttf", FileMode.Open, FileAccess.Read); 
PdfFont font = new PdfTrueTypeFont(fontStream, 14);
//Draw the text.
graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new Syncfusion.Drawing.PointF(0, 0)); 

//Create the stream object. 
MemoryStream stream = new MemoryStream(); 
//Save the document into the memory stream. 
document.Save(stream); 
//If the position is not set to '0,' a PDF will be empty.
stream.Position = 0;
//Close the document.
document.Close(true); 
//Define the ContentType for a PDF file.
string contentType = "application/pdf";
//Define the file name.
string fileName = "Output.pdf";
//Create the FileContentResult object by using the file contents, content type, and file name.
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Create a new document with the PDF/A-4 standard. 
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A4); 
//Add a page to the document. 
PdfPage page = document.Pages.Add(); 
//Create the PDF graphics for the page. 
PdfGraphics graphics = page.Graphics; 

//Load the TrueType font. 
Stream fontStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Arial.ttf"); 
//Initialize the PDF TrueType font.
PdfFont font = new PdfTrueTypeFont(fontStream, 14); 
//Draw the text. 
graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new Syncfusion.Drawing.PointF(0, 0)); 

//Save the document into the memory stream.
MemoryStream stream = new MemoryStream();
//Save the document into the memory stream.
document.Save(stream); 
//Close the document. 
document.Close(true); 
//Save the stream into a PDF file. 
//The operation in Save under the Xamarin varies between the Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples 
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/PDF%20Conformance/Creating-the-new-PDFA4-document).
	
## PDF/A-4e conformance

The PDF/A-4E ("Engineering") is intended for technical documents and replaces PDF/E. PDF/A-4e supports 3D models, rich media, and 3D annotations as well as embedded files.

Create a PDF/A-4E document by specifying the conformance level as ``Pdf_A4E`` through the [PdfConformanceLevel](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfConformanceLevel.html) Enum when creating the new PDF document as follows.

{% tabs %}  

{% highlight c# tabtitle="C#" %}

//Create a new document with the PDF/A-4E standard. 
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A4E); 
//Create a new page. 
PdfPage page = document.Pages.Add(); 

//Create a new pdf 3d annotation. 
Pdf3DAnnotation pdf3dAnnotation = new Pdf3DAnnotation(new RectangleF(10, 50, 300, 150), @"3DAnnotation.U3D"); 
//Handle the activation of the 3d annotation. 
Pdf3DActivation activation = new Pdf3DActivation(); 
activation.ActivationMode = Pdf3DActivationMode.ExplicitActivation; 
activation.ShowToolbar = true; pdf3dAnnotation.Activation = activation; 
//Add the annotation to the page. 
page.Annotations.Add(pdf3dAnnotation); 

//Save the document to the disk.
document.Save("3DAnnotation.pdf"); 
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new document with the PDF/A-4 standard. 
Dim document As New PdfDocument(PdfConformanceLevel.Pdf_A4E) 
'Creates a new page. 
Dim page As PdfPage = document.Pages.Add()
 
'Create a new pdf 3d annotation. 
Dim pdf3dAnnotation As New Pdf3DAnnotation(New RectangleF(10, 50, 300, 150), "3DAnnotation.U3D") 
'Handle the activation of the 3d annotation. 
Dim activation As New Pdf3DActivation() 
activation.ActivationMode = Pdf3DActivationMode.ExplicitActivation
activation.ShowToolbar = True 
pdf3dAnnotation.Activation = activation 
'Add the annotation to the page.
page.Annotations.Add(pdf3dAnnotation) 

'Save the document to the disk. 
document.Save("3DAnnotation.pdf") 
document.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Create a new document with the PDF/A-4 standard. 
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A4E);
//Add a page to the document. 
PdfPage page = document.Pages.Add(); 

//Create a new pdf 3d annotation. 
FileStream inputStream = new FileStream("3DAnnotation.U3D", FileMode.Open, FileAccess.Read); 
Pdf3DAnnotation pdf3dAnnotation = new Pdf3DAnnotation(new RectangleF(10, 50, 300, 150), inputStream); 
//Handle the activation of the 3d annotation. 
Pdf3DActivation activation = new Pdf3DActivation(); 
activation.ActivationMode = Pdf3DActivationMode.ExplicitActivation; 
activation.ShowToolbar = true; pdf3dAnnotation.Activation = activation; 
//Add the annotation to the page. 
page.Annotations.Add(pdf3dAnnotation); 

//Save the document into the memory stream.
MemoryStream stream = new MemoryStream(); 
await document.SaveAsync(stream); 
//Close the document. 
document.Close(true); 
//Save the stream as a PDF document file in the local machine. Refer to the PDF/UWP section for respective code samples. 
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a new document with the PDF/A-4 standard. 
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A4); 
//Creates a new page. 
PdfPage page = document.Pages.Add(); 

//Create a new pdf 3d annotation. 
FileStream inputStream = new FileStream("3DAnnotation.U3D", FileMode.Open, FileAccess.Read); 
Pdf3DAnnotation pdf3dAnnotation = new Pdf3DAnnotation(new RectangleF(10, 50, 300, 150), inputStream); 
//Handle the activation of the 3d annotation. 
Pdf3DActivation activation = new Pdf3DActivation(); 
activation.ActivationMode = Pdf3DActivationMode.ExplicitActivation; 
activation.ShowToolbar = true; pdf3dAnnotation.Activation = activation; 
//Add the annotation to the page. 
page.Annotations.Add(pdf3dAnnotation); 

//Save the document into the stream. 
MemoryStream stream = new MemoryStream(); 
document.Save(stream); stream.Position = 0; 
//Close the document. 
document.Close(true); 
//Define the ContentType for a pdf file. 
string contentType = "application/pdf"; 
//Define the file name. 
string fileName = "3DAnnotation.pdf"; 
//Create the FileContentResult object by using the file contents, content type, and file name. 
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Create a new document with the PDF/A-4 standard. 
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A4E); 
//Create a new page. 
PdfPage page = document.Pages.Add(); 

//Create a new PDF 3d annotation. 
Stream inputStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.3DAnnotation.u3d");
Pdf3DAnnotation pdf3dAnnotation = new Pdf3DAnnotation(new RectangleF(10, 50, 300, 150), inputStream); 
//Handle the activation of the 3d annotation. 
Pdf3DActivation activation = new Pdf3DActivation(); 
activation.ActivationMode = Pdf3DActivationMode.ExplicitActivation; 
activation.ShowToolbar = true; pdf3dAnnotation.Activation = activation; 
//Add the annotation to the page. 
page.Annotations.Add(pdf3dAnnotation); 

//Save the PDF document to the stream. 
MemoryStream stream = new MemoryStream(); 
document.Save(stream); 
//Close the document.
document.Close(true);
//Save the stream into a PDF file 
//The operation in Save under the Xamarin varies between the Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples. 
if (Device.RuntimePlatform == Device.UWP) 
{ 
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("3DAnnotation.pdf", "application/pdf", stream); 
}
else 
{ 
    Xamarin.Forms.DependencyService.Get<ISave>().Save("3DAnnotation.pdf", "application/pdf", stream); 
}

{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/PDF%20Conformance/Creating-the-new-PDFA4E-document).

## PDF/A-4f conformance

The requirements of the PDF/A-3 have also been partially incorporated into PDF/A-4. Thus, the PDF/A-4f allows the embedding of arbitrary files.

Create a PDF/A-4f document by specifying the conformance level as ``Pdf_A4F`` through the [PdfConformanceLevel](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfConformanceLevel.html) Enum when creating a new PDF document as follows.

{% tabs %}  

{% highlight c# tabtitle="C#" %}

//Create a new document with the PDF/A-3b standard. 
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A4F); 
//Add a page. 
PdfPage page = document.Pages.Add(); 

//Create an attachment. 
PdfAttachment attachment = new PdfAttachment("Input.txt"); 
attachment.Relationship = PdfAttachmentRelationship.Alternative; 
attachment.ModificationDate = DateTime.Now; 
attachment.Description = "Input.txt"; 
attachment.MimeType = "application/txt";
//Add the attachment to the document. 
document.Attachments.Add(attachment); 

//Create the PDF graphics for the page. 
PdfGraphics graphics = page.Graphics; 
//Create a solid brush. 
PdfBrush brush = new PdfSolidBrush(Color.Black);
//Set the font. 
Font font = new Font("Arial", 20f, FontStyle.Regular); 
PdfFont pdfFont = new PdfTrueTypeFont(font, FontStyle.Regular, 12, false, true);
//Draw the text. 
graphics.DrawString("Hello world!", pdfFont, brush, new PointF(20, 20)); 

//Save and close the document. 
document.Save("Output.pdf"); 
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new document with the PDF/A-3b standard. 
Dim document As New PdfDocument(PdfConformanceLevel.Pdf_A4F) 
'Add a page. 
Dim page As PdfPage = document.Pages.Add() 

'Create an attachment. 
Dim attachment As New PdfAttachment("Input.txt") 
attachment.Relationship = PdfAttachmentRelationship.Alternative
attachment.ModificationDate = DateTime.Now 
attachment.Description = "Input.txt" 
attachment.MimeType = "application/txt" 
'Add the attachment to the document. 
document.Attachments.Add(attachment) 

'Create the PDF graphics for the page. 
Dim graphics As PdfGraphics = page.Graphics 
'Create a solid brush. 
Dim brush As PdfBrush = New PdfSolidBrush(Color.Black) 
'Set the font. 
Dim font As New Font("Arial", 20.0F, FontStyle.Regular) 
Dim pdfFont As PdfFont = New PdfTrueTypeFont(font, FontStyle.Regular, 12, False, True) 

'Draw the text. 
graphics.DrawString("Hello world!", pdfFont, brush, New PointF(20, 20)) 

'Save and close the document. 
document.Save("Output.pdf") 
document.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Create a new document with the PDF/A-4F standard. 
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A4F); 
//Add a page to the document. 
PdfPage page = document.Pages.Add(); 

//Create an attachment. 
Stream fileStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Input.txt"); 
PdfAttachment attachment = new PdfAttachment(@"Input.txt", fileStream); 
attachment.Relationship = PdfAttachmentRelationship.Alternative; 
attachment.ModificationDate = DateTime.Now; 
attachment.Description = "Input.txt"; 
attachment.MimeType = "application/txt"; 
//Add the attachment to the document. 
document.Attachments.Add(attachment); 

//Create the PDF graphics for the page. 
PdfGraphics graphics = page.Graphics; 

//Load the TrueType font from the local file.
Stream fontStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Arial.ttf"); 
//Initialize the PDF TrueType font. 
PdfFont font = new PdfTrueTypeFont(fontStream, 14); 
//Draw the text. 
graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0)); 

//Save the document into the memory stream. 
MemoryStream stream = new MemoryStream(); 
await document.SaveAsync(stream); 
//Close the document. 
document.Close(true); 
//Save the stream as a PDF document file in the local machine. Refer to the PDF/UWP section for respective code samples. 
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a new document with the PDF/A-4F standard. 
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A4F); 
//Add a page to the document. 
PdfPage page = document.Pages.Add(); 

//Create an attachment. 
Stream fileStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Input.txt"); 
PdfAttachment attachment = new PdfAttachment(@"Input.txt", fileStream); 
attachment.Relationship = PdfAttachmentRelationship.Alternative; 
attachment.ModificationDate = DateTime.Now; 
attachment.Description = "Input.txt"; 
attachment.MimeType = "application/txt"; 

//Add the attachment to the document. 
document.Attachments.Add(attachment); 

//Create the PDF graphics for the page. 
PdfGraphics graphics = page.Graphics; 
//Load the TrueType font from the local file.
Stream fontStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Arial.ttf"); 
//Initialize the PDF TrueType font. 
PdfFont font = new PdfTrueTypeFont(fontStream, 14); 
//Draw the text. 
graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0)); 

//Save the document into the memory stream. 
MemoryStream stream = new MemoryStream(); 
await document.SaveAsync(stream); 
//Close the document. 
document.Close(true); 
//Save the stream as a PDF document file in the local machine. Refer to the PDF/UWP section for respective code samples. 
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Create a new document with the PDF/A-4F standard. 
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A4F);
 
//Add a page to the document. 
PdfPage page = document.Pages.Add(); 
Stream fileStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.txt"); 
PdfAttachment attachment = new PdfAttachment("Input.txt", fileStream); 
attachment.Relationship = PdfAttachmentRelationship.Alternative; 
attachment.ModificationDate = DateTime.Now; 
attachment.Description = "Input.txt"; 
attachment.MimeType = "application/txt"; 
//Add the attachment to the document. 
document.Attachments.Add(attachment); 

//Create the PDF graphics for the page. 
PdfGraphics graphics = page.Graphics; 
//Load the TrueType font. 
Stream fontStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Arial.ttf"); 
//Initialize the PDF TrueType font.
PdfFont font = new PdfTrueTypeFont(fontStream, 14); 
//Draw the text. 
graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new Syncfusion.Drawing.PointF(0, 0)); 

//Save the document into the memory stream. 
MemoryStream stream = new MemoryStream(); 
document.Save(stream); 
//Close the document. 
document.Close(true); 
//Save the stream into a PDF file. 
//The operation in Save under the Xamarin varies between the Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples. 
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/PDF%20Conformance/Creating-a-new-PDFA4F-document).

## PDF/X-1a conformance

You can create a PDF/X-1a document by specifying the conformance level as ```Pdf_X1A2001``` through [PdfConformanceLevel](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfConformanceLevel.html) Enum when creating the new PDF document, as shown below.

{% tabs %}  

{% highlight c# tabtitle="C#" %}

//Create a new document with PDF/x standard.
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_X1A2001);
//Add a page.
PdfPage page = document.Pages.Add();
//Set color space. 
document.ColorSpace = PdfColorSpace.CMYK;

//Create Pdf graphics for the page.
PdfGraphics graphics = page.Graphics;
//Create a solid brush.
PdfBrush brush = new PdfSolidBrush(Color.Black);
//Set the font.
Font font = new Font("Arial",20f, FontStyle.Regular);
PdfFont pdfFont = new PdfTrueTypeFont(font, FontStyle.Regular, 12, false, true);
//Draw the text.
graphics.DrawString("Hello world!", pdfFont, brush, new PointF(20, 20));

//Save and close the document.
document.Save("Output.pdf");
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new document with PDF/x standard.
Dim document As New PdfDocument(PdfConformanceLevel.Pdf_X1A2001)
'Add a page.
Dim page As PdfPage = document.Pages.Add()

'Set ColorSpace
document.ColorSpace = PdfColorSpace.CMYK

'Create Pdf graphics for the page.
Dim graphics As PdfGraphics = page.Graphics
'Create a solid brush.
Dim brush As PdfBrush = New PdfSolidBrush(Color.Black)
'Set the font.
Dim font As New Font("Arial", 20.0F, FontStyle.Regular)
Dim pdfFont As PdfFont = New PdfTrueTypeFont(font, FontStyle.Regular, 12, False, True)
'Draw the text.
graphics.DrawString("Hello world!", font, brush, New PointF(20, 20))

'Save and close the document.
document.Save("Output.pdf")
document.Close(True)

{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/PDF%20Conformance/Create-a-PDFX1A-conformance-document).

## PDF to PDF/A conversion

An existing PDF document can be converted to PDF/A conformance document, by setting the [Conformance](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html#Syncfusion_Pdf_Parsing_PdfLoadedDocument_Conformance) value in the [PdfLoadedDocument](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html) to ```Pdf_A1B```,```Pdf_A2B```,```Pdf_A3B```, and ```Pdf_A``` of  [PdfConformanceLevel](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfConformanceLevel.html). Refer to the following code sample to achieve the same.

N> To convert the existing PDF to PDF/A conformance document in .NET Core, you need to include the Syncfusion.Pdf.Imaging.Portable assembly reference in the .NET Core project.

{% tabs %}  

{% highlight c# tabtitle="C#" %}

//Load an existing PDF.
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");

//Set the conformance for PDF/A-1b conversion.
loadedDocument.Conformance = PdfConformanceLevel.Pdf_A1B;

//Save and close the document.
loadedDocument.Save("Output.pdf");
loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Load an existing PDF.
Dim document As New PdfLoadedDocument("Input.pdf")

'Set the conformance for PDF/A-1b conversion.
loadedDocument.Conformance = PdfConformanceLevel.Pdf_A1B

'Save and close the document.
loadedDocument.Save("Output.pdf")
loadedDocument.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load an existing PDF document
FileStream docStream = new FileStream(@"Input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Sample level font event handling
loadedDocument.SubstituteFont += LoadedDocument_SubstituteFont ;
//Convert the loaded document to PDF/A document
loadedDocument.ConvertToPDFA(PdfConformanceLevel.Pdf_A1B);

//Save the document
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream); 
stream.Position = 0; 
//Close the document 
loadedDocument.Close(true); 
//Defining the ContentType for pdf file 
string contentType = "application/pdf";
//Define the file name 
string fileName = "output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name
return File(stream, contentType, fileName);

{% endhighlight %}

{% endtabs %}  

To convert an existing PDF document to the PDFA document in .NET Core, you need to substitute the non-embedded fonts in the input document. Refer to the the following code sample to achieve the same.

{% tabs %} 

{% highlight c# tabtitle="ASP.NET Core" %}

static void LoadedDocument_SubstituteFont(object sender, PdfFontEventArgs args)
{
     //get the font name
     string fontName = args.FontName.Split(',')[0];
     //get the font style
     PdfFontStyle fontStyle = args.FontStyle;
     SKFontStyle sKFontStyle = SKFontStyle.Normal;

     if (fontStyle != PdfFontStyle.Regular)
     {
         if (fontStyle == PdfFontStyle.Bold)
         {
             sKFontStyle = SKFontStyle.Bold;
         }
         else if (fontStyle == PdfFontStyle.Italic)
         {
             sKFontStyle = SKFontStyle.Italic;
         }
         else if (fontStyle == (PdfFontStyle.Italic | PdfFontStyle.Bold))
         {
             sKFontStyle = SKFontStyle.BoldItalic;
         }
    }
	
    SKTypeface typeface = SKTypeface.FromFamilyName(fontName, sKFontStyle);
    SKStreamAsset typeFaceStream = typeface.OpenStream();
    MemoryStream memoryStream = null;
    if (typeFaceStream != null && typeFaceStream.Length > 0)
    {
         //Create the fontData from the type face stream.	 
         byte[] fontData = new byte[typeFaceStream.Length - 1];	 
         typeFaceStream.Read(fontData, typeFaceStream.Length);	 
         typeFaceStream.Dispose();	 
         //Create the new memory stream from the font data.	 
         memoryStream = new MemoryStream(fontData);
    }	
    //set the font stream to the event args.	
    args.FontStream = memoryStream;
}

{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/PDF%20Conformance/Get-PDF-to-PDFA-conversion-progress).

N> 1. Converting PDF to PDF/X-1a conformance document is not supported.
N> 2. CMYK color space images and symbolic fonts are not supported.
N> 3. From the .NET Framework 3.5 version, the Essential PDF is compatible with the PDF to PDF/A conversion. 

## Get PDF Conformance Level

You can find the conformance level of the existing PDF document using the [Conformance](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html#Syncfusion_Pdf_Parsing_PdfLoadedDocument_Conformance) property in the [PdfLoadedDocument](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html) class. Refer to the following code sample to get the conformance level of the existing PDF document. 

{% tabs %} 

{% highlight c# tabtitle="C#" %}

//Load an existing PDF document. 
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf"); 

//Get the conformance level of the loaded document. 
PdfConformanceLevel conformance = loadedDocument.Conformance;

//Close the document. 
loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Load an existing PDF. 
Dim document As New PdfLoadedDocument("Input.pdf") 

'Get the conformance level of the loaded document. 
PdfConformanceLevel conformance = loadedDocument.Conformance;

'Close the document. 
loadedDocument.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Create the file open picker 
var picker = new FileOpenPicker(); 
picker.FileTypeFilter.Add(".pdf"); 
//Browse and choose the file 
StorageFile file = await picker.PickSingleFileAsync(); 
//Creates an empty PDF loaded document instance. 
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(); 
//Loads or opens an existing PDF document through Open method of the PdfLoadedDocument class 
await loadedDocument.OpenAsync(file); 

//Get the conformance level of the loaded document. 
PdfConformanceLevel conformance = loadedDocument.Conformance;

//Close the document. 
loadedDocument.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load an existing PDF document
FileStream docStream = new FileStream(@"Input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Get the conformance level of the loaded document. 
PdfConformanceLevel conformance = loadedDocument.Conformance;

//Close the document.
loadedDocument.Close(true); 

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Load the file as a stream. 
Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample.pdf");
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream); 

//Get the conformance level of the loaded document. 
PdfConformanceLevel conformance = loadedDocument.Conformance;

//Close the document. 
loadedDocument.Close(true);

{% endhighlight %}

{% endtabs %} 

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/PDF%20Conformance/Get-the-conformance-level-of-the-existing-PDF-document).

## Get PDF to PDF/A conversion progress

You can get conversion progress using [PdfAConversionProgress](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html#Syncfusion_Pdf_Parsing_PdfLoadedDocument_PdfAConversionProgress) event.

The following code sample shows the delegate for handling PDF to PDF/A conversion process

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Load a PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("input.pdf");

//Set the conformance for PDF/A-1b conversion.
loadedDocument.Conformance = PdfConformanceLevel.Pdf_A1B;
loadedDocument.PdfAConversionProgress += pdfAConversion_TrackProgress;

//Save the document
loadedDocument.Save("Output.pdf");

//Close the document
loadedDocument.Close(true);

//Event handler for Track PDF to PDF/A conversion process
void pdfAConversion_TrackProgress(object sender, PdfAConversionProgressEventArgs arguments)
{
MessageBox.Show(String.Format("PDF to PDF/A conversion Process " + arguments. ProgressValue + " % completed"));
}

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Load a PDF document 
Dim loadedDocument As PdfLoadedDocument = New PdfLoadedDocument("input.pdf") 

'Set the conformance for PDF/A-1b conversion.
loadedDocument.Conformance = PdfConformanceLevel.Pdf_A1B
loadedDocument.PdfAConversionProgress += pdfAConversion_TrackProgress

'Save the document
loadedDocument.Save("Output.pdf")

'Close the document
loadedDocument.Close(True)

'Event handler for Track PDF to PDF/A conversion process
Private  Sub pdfAConversion_TrackProgress(ByVal sender As Object, ByVal arguments As PdfAConversionProgressEventArgs)
MessageBox.Show(String.Format(PDF to PDF/A conversion Process " + arguments. ProgressValue + " % completed"))

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load an existing PDF document. 
FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Set the conformance for PDF/A-1b conversion.
loadedDocument.Conformance = PdfConformanceLevel.Pdf_A1B;
loadedDocument.PdfAConversionProgress += pdfAConversion_TrackProgress;

//Creating the stream object.
MemoryStream stream = new MemoryStream();
//Save the document into stream.
loadedDocument.Save(stream);
//If the position is not set to '0' then the PDF will be empty.
loadedDocument.Position = 0;
//Close the document.
loadedDocument.Close(true);

//Event handler for Track PDF to PDF/A conversion process.
void pdfAConversion_TrackProgress(object sender, PdfAConversionProgressEventArgs arguments)
{
MessageBox.Show(String.Format("PDF to PDF/A conversion Process " + arguments. ProgressValue + " % completed"));
}

//Defining the ContentType for pdf file
string contentType = "application/pdf";
//Define the file name
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name
return File(stream, contentType, fileName);

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/PDF%20Conformance/Get-PDF-to-PDFA-conversion-progress).

## PDF/A to PDF conversion

An existing PDF/A conformance document can be converted to a PDF document using the [RemoveConformance](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html#Syncfusion_Pdf_Parsing_PdfLoadedDocument_RemoveConformance) method in the [PdfLoadedDocument](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html) class. Refer to the following code sample to achieve the same,

{% tabs %}  

{% highlight c# %}

//Load an existing document.
PdfLoadedDocument document = new PdfLoadedDocument("input.pdf");

//Remove PDF/A conformance.
document.RemoveConformance();

//Save the document.
document.Save("Output.pdf");
//Close the document.
document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Load an existing document.
Dim document As PdfLoadedDocument = New PdfLoadedDocument("input.pdf")

'Remove PDF/A conformance.
document.RemoveConformance()

'Save the document.
document.Save("Output.pdf")
'Close the document.
document.Close(True)

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load a PDF document.
FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument document = new PdfLoadedDocument(docStream);

//Remove PDF/A conformance.
document.RemoveConformance();

//Save the document.
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Close the document.
document.Close(true);
//Defining the ContentType for pdf file 
string contentType = "application/pdf";
//Define the file name 
string fileName = "output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream.
Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");
PdfLoadedDocument document = new PdfLoadedDocument(docStream);

//Remove PDF/A conformance.
document.RemoveConformance();

//Save the document.
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Close the document.
document.Close(true);

{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/PDF%20Conformance/Convert-PDFA-to-PDF-document).
