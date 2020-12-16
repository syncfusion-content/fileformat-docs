---
title: Working with Text | Syncfusion
description: This section explains how to add text to the PDF document using different type of fonts, TrueType fonts and standard fonts
platform: file-formats
control: PDF
documentation: UG
---
# Working with Text | Syncfusion

## Drawing text in a new document

You can add text in the new PDF document by using [DrawString](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfGraphics.html#Syncfusion_Pdf_Graphics_PdfGraphics_DrawString_System_String_Syncfusion_Pdf_Graphics_PdfFont_Syncfusion_Pdf_Graphics_PdfBrush_System_Drawing_PointF_) method of [PdfGraphics](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfGraphics.html) class as shown in the following code sample.

{% tabs %}

{% highlight c# %}

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

//Save the document.

document.Save("Output.pdf");

//Close the document.

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim document As New PdfDocument()

'Add a page to the document.

Dim page As PdfPage = document.Pages.Add()

'Create PDF graphics for the page.

Dim graphics As PdfGraphics = page.Graphics

'Set the standard font.

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 20)

'Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, New PointF(0, 0))

'Save the document.

document.Save("Output.pdf")

'Close the document.

document.Close(True)

{% endhighlight %}

{% highlight UWP %}

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

//Save the document into memory stream.

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document.

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

 //Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Set the standard font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new Syncfusion.Drawing.PointF(0, 0));

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the document into memory stream

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

{% highlight Xamarin %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Set the standard font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new Syncfusion.Drawing.PointF(0, 0));

//Save the document into memory stream.

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

## Drawing text in an existing document

The following code snippet illustrates how to add text in the existing PDF document by using [DrawString](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfGraphics.html#Syncfusion_Pdf_Graphics_PdfGraphics_DrawString_System_String_Syncfusion_Pdf_Graphics_PdfFont_Syncfusion_Pdf_Graphics_PdfBrush_System_Drawing_PointF_) method.

{% tabs %}

{% highlight c# %}

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

//Save the document.
doc.Save("Output.pdf");

//Close the document.
doc.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Load a PDF document.
Dim doc As New PdfLoadedDocument("input.pdf")

'Get first page from document
Dim page As PdfLoadedPage = TryCast(doc.Pages(0), PdfLoadedPage)

'Create PDF graphics for the page
Dim graphics As PdfGraphics = page.Graphics

'Set the standard font.
Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 20)

'Draw the text.
graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, New PointF(0, 0))

'Save the document.
doc.Save("Output.pdf")

'Close the document.
doc.Close(True)

{% endhighlight %}

{% highlight UWP %}

//Create the file open picker
var picker = new FileOpenPicker();

picker.FileTypeFilter.Add(".pdf");

//Browse and chose the file
StorageFile file = await picker.PickSingleFileAsync();

//Creates an empty PDF loaded document instance
PdfLoadedDocument doc = new PdfLoadedDocument();

//Loads or opens an existing PDF document through Open method of PdfLoadedDocument class
await doc.OpenAsync(file);

//Get first page from document
PdfLoadedPage page = doc.Pages[0] as PdfLoadedPage;

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Set the standard font.
PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.
graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

//Save the document into memory stream.
MemoryStream stream = new MemoryStream();

await doc.SaveAsync(stream);

//Close the document.
doc.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

 //Load the PDF document
FileStream docStream = new FileStream("input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument doc = new PdfLoadedDocument(docStream);

//Get first page from document
PdfLoadedPage page = doc.Pages[0] as PdfLoadedPage;

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Set the standard font.
PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.
graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new Syncfusion.Drawing.PointF(0, 0));

//Creating the stream object
MemoryStream stream = new MemoryStream();

//Save the document into memory stream
doc.Save(stream);

//If the position is not set to '0' then the PDF will be empty.
stream.Position = 0;

//Close the document.
doc.Close(true);

//Defining the ContentType for pdf file.
string contentType = "application/pdf";

//Define the file name.
string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream
Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.pdf ");

//Load a PDF document.
PdfLoadedDocument doc = new PdfLoadedDocument(docStream);

//Get first page from document
PdfLoadedPage page = doc.Pages[0] as PdfLoadedPage;

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Set the standard font.
PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.
graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new Syncfusion.Drawing.PointF(0, 0));

//Save the document into memory stream.
MemoryStream stream = new MemoryStream();

doc.Save(stream);

//Close the document.
doc.Close(true);

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

## Drawing text using different fonts

Essential PDF allows you to add text to the PDF document using the following types of fonts.

1. Standard fonts
2. TrueType fonts
3. Chinese, Japanese and Korean (CJK) fonts

### Draw text using standard fonts

PDF has fourteen base fonts, also known as standard fonts which has special significance. The details can be referred from the link below.

[Standard type 1 fonts](https://en.wikipedia.org/wiki/Portable_Document_Format#Standard_Type_1_Fonts_.28Standard_14_Fonts.29)

You can add text using the standard PDF fonts, by initializing [PdfFont](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfFont.html) class as [PdfStandardFont](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfStandardFont.html) class. The following code snippet illustrates this. 

{% tabs %}

{% highlight c# %}

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

//Save the document.

document.Save("Output.pdf");

//Close the document.

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim document As New PdfDocument()

'Add a page to the document.

Dim page As PdfPage = document.Pages.Add()

'Create PDF graphics for the page.

Dim graphics As PdfGraphics = page.Graphics

'Set the standard font.

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 20)

'Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, New PointF(0, 0))

'Save the document.

document.Save("Output.pdf")

'Close the document.

document.Close(True)

{% endhighlight %}

{% highlight UWP %}

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

//Save the document into memory stream.

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document.

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Set the standard font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new Syncfusion.Drawing.PointF(0, 0));

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the document into memory stream

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

{% highlight Xamarin %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Set the standard font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new Syncfusion.Drawing.PointF(0, 0));

//Save the document into memory stream.

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

### Draw text using TrueType fonts

You can add text using the TrueType fonts installed in the system, by initializing [PdfFont](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfFont.html) class as [PdfTrueTypeFont](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfTrueTypeFont.html) class. The following code snippet illustrates this.

{% tabs %}

{% highlight c# %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Use the font installed in the machine

PdfFont font = new PdfTrueTypeFont(new Font("Arial", 14));

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

//Save the document.

document.Save("Output.pdf");

//Close the document.

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim document As New PdfDocument()

'Add a page to the document.

Dim page As PdfPage = document.Pages.Add()

'Create PDF graphics for the page.

Dim graphics As PdfGraphics = page.Graphics

'Use the font installed in the machine

Dim font As PdfFont = New PdfTrueTypeFont(New Font("Arial", 14))

'Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, New PointF(0, 0))

'Save the document.

document.Save("Output.pdf")

'Close the document.

document.Close(True)

{% endhighlight %}
{% endtabs %}
You can add text using the font file from local file system by providing the path of the TrueType font location. The following code snippet explains the same.
{% tabs %}
{% highlight c# %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Provide the path of the local *.ttf file

PdfFont font = new PdfTrueTypeFont(new Font("Arial.ttf", 14));

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

//Save the document.

document.Save("Output.pdf");

//Close the document.

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim document As New PdfDocument()

'Add a page to the document.

Dim page As PdfPage = document.Pages.Add()

'Create PDF graphics for the page.

Dim graphics As PdfGraphics = page.Graphics

' Provide the path of the local *.ttf file

Dim font As PdfFont = New PdfTrueTypeFont(New Font("Arial.ttf", 14))

'Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, New PointF(0, 0))

'Save the document.

document.Save("Output.pdf")

'Close the document.

document.Close(True)

{% endhighlight %}

{% highlight UWP %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Load the TrueType font from the local *.ttf file.

Stream fontStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Arial.ttf");

//Initialize the PDF TrueType font. 

PdfFont font = new PdfTrueTypeFont(fontStream, 14);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

//Save the document into memory stream.

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document.

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Load the TrueType font from the local *.ttf file.

FileStream fontStream = new FileStream("Arial.ttf", FileMode.Open, FileAccess.Read);

PdfFont font = new PdfTrueTypeFont(fontStream, 14);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new Syncfusion.Drawing.PointF(0, 0));

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the document into memory stream

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

{% highlight Xamarin %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Load the TrueType font. 

Stream fontStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Arial.ttf");

//Initialize the PDF TrueType font.  

PdfFont font = new PdfTrueTypeFont(fontStream, 14);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new Syncfusion.Drawing.PointF(0, 0));

//Save the document into memory stream.

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

### Draw text using CJK fonts

You can add text using CJK fonts, initializing [PdfFont](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfFont.html) class as [PdfCjkStandardFont](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfCjkStandardFont.html) class. The following code sample illustrates this.

{% tabs %}

{% highlight c# %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();

//Add a page to the document.
PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;

//Set the standard font.
PdfFont font = new PdfCjkStandardFont(PdfCjkFontFamily.HeiseiMinchoW3, 20);

//Draw the text.
graphics.DrawString("こんにちは世界", font, PdfBrushes.Black, new PointF(0, 0));

//Save the document.
document.Save("Output.pdf");

//Close the document.
document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document.
Dim document As New PdfDocument()

'Add a page to the document.
Dim page As PdfPage = document.Pages.Add()

'Create PDF graphics for the page.
Dim graphics As PdfGraphics = page.Graphics

'Set the standard font.
Dim font As PdfFont = New PdfCjkStandardFont(PdfCjkFontFamily.HeiseiMinchoW3, 20)

'Draw the text.
graphics.DrawString("こんにちは世界", font, PdfBrushes.Black, New PointF(0, 0))

'Save the document.
document.Save("Output.pdf")

'Close the document.
document.Close(True)

{% endhighlight %}

{% highlight UWP %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();

//Add a page to the document.
PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;

//Set the standard font.
PdfFont font = new PdfCjkStandardFont(PdfCjkFontFamily.HeiseiMinchoW3, 20);

//Draw the text.
graphics.DrawString("こんにちは世界", font, PdfBrushes.Black, new PointF(0, 0));

//Save the document into memory stream.
MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document.
document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();

//Add a page to the document.
PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;

//Set the standard font.
PdfFont font = new PdfCjkStandardFont(PdfCjkFontFamily.HeiseiMinchoW3, 20);

//Draw the text.
graphics.DrawString("こんにちは世界", font, PdfBrushes.Black, new Syncfusion.Drawing.PointF(0, 0));

//Creating the stream object
MemoryStream stream = new MemoryStream();

//Save the document into memory stream
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

{% highlight Xamarin %}

 //Create a new PDF document.
PdfDocument document = new PdfDocument();

//Add a page to the document.
PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;

//Set the standard font.
PdfFont font = new PdfCjkStandardFont(PdfCjkFontFamily.HeiseiMinchoW3, 20);

//Draw the text.
graphics.DrawString("こんにちは世界", font, PdfBrushes.Black, new Syncfusion.Drawing.PointF(0, 0));

//Save the document into memory stream.
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

## Measuring a string

The Essential PDF allows you to measure the size of a string which uses the ```PdfFont``` through [MeasureString](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfFont.html#Syncfusion_Pdf_Graphics_PdfFont_MeasureString_System_String_) method of it and returns the size. Refer to the following code sample.

{% tabs %}

{% highlight c# %}

//Create the new PDF document

PdfDocument document = new PdfDocument();

//Add a page to the document

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page

PdfGraphics graphics = page.Graphics;

//Create a new PDF font instance

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 12);

string text = "Hello World!";

//Measure the text

SizeF size = font.MeasureString(text);

//Draw string to the PDF page

graphics.DrawString(text, font, PdfBrushes.Black, new RectangleF(PointF.Empty, size));

//Save the document

document.Save("Output.pdf");

//Close the document

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create the new PDF document

Dim document As New PdfDocument()

'Add a page to the document

Dim page As PdfPage = document.Pages.Add()

'Create PDF graphics for the page

Dim graphics As PdfGraphics = page.Graphics

'Create a new PDF font instance

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 12)

Dim text As String = "Hello World!"

'Measure the text

Dim size As SizeF = font.MeasureString(text)

'Draw string to the PDF page

graphics.DrawString(text, font, PdfBrushes.Black, New RectangleF(PointF.Empty, size))

'Save the document

document.Save("Output.pdf")

'Close the document

document.Close(True)

{% endhighlight %}

{% highlight UWP %}

//Create the new PDF document

PdfDocument document = new PdfDocument();

//Add a page to the document

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page

PdfGraphics graphics = page.Graphics;

//Create a new PDF font instance

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 12);

string text = "Hello World!";

//Measure the text

SizeF size = font.MeasureString(text);

//Draw string to the PDF page

graphics.DrawString(text, font, PdfBrushes.Black, new RectangleF(PointF.Empty, size));

//Save the document as stream

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document instances

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Create the new PDF document

PdfDocument document = new PdfDocument();

//Add a page to the document

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page

PdfGraphics graphics = page.Graphics;

//Create a new PDF font instance

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 12);

string text = "Hello World!";

//Measure the text

SizeF size = font.MeasureString(text);

//Draw string to th ePDF page

graphics.DrawString(text, font, PdfBrushes.Black, new RectangleF(PointF.Empty, size));

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the document as stream

document.Save(stream);

//If the position is not set to '0', then the PDF will be empty.

stream.Position = 0;

//Close the document

document.Close(true);

//Defining the ContentType for PDF file.

string contentType = "application/pdf";

//Define the file name

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Create the new PDF document

PdfDocument document = new PdfDocument();

//Add a page to the document

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page

PdfGraphics graphics = page.Graphics;

//Create a new PDF font instance

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 12);

string text = "Hello World!";

//Measure the text

SizeF size = font.MeasureString(text);

//Draw string to the PDF page

graphics.DrawString(text, font, PdfBrushes.Black, new RectangleF(PointF.Empty, size));

//Save the document as stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document instances

document.Close(true);

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

## Embedding fonts and working with Unicode text

To embed a font or display Unicode text in the document, the ‘Unicode’ Boolean parameter of the [PdfTrueTypeFont](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfTrueTypeFont.html#Syncfusion_Pdf_Base__ctor) constructor has to be set to true. The following code illustrates the same.

N> To render a Unicode text in the PDF document the chosen font should have the Unicode rendering capability.

{% tabs %}

{% highlight c# %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//use the system installed font

PdfFont font = new PdfTrueTypeFont(new Font("Arial Unicode MS", 14), true);

//Read the unicode text from the text file.

StreamReader reader = new StreamReader(@"input.txt", Encoding.Unicode);

string text = reader.ReadToEnd();

reader.Close();

//Draw the text.

graphics.DrawString(text, font, PdfBrushes.Black, new PointF(0, 0));

//Save the document.

document.Save("Output.pdf");

//Close the document.

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim document As New PdfDocument()

'Add a page to the document.

Dim page As PdfPage = document.Pages.Add()

'Create PDF graphics for the page.

Dim graphics As PdfGraphics = page.Graphics

'use the system installed font

Dim font As PdfFont = New PdfTrueTypeFont(New Font("Arial Unicode MS", 14), True)

'Read the unicode text from the text file.

Dim reader As New StreamReader("input.txt", Encoding.Unicode)

Dim text As String = reader.ReadToEnd()

reader.Close()

'Draw the text.

graphics.DrawString(text, font, PdfBrushes.Black, New PointF(0, 0))

'Save the document.

document.Save("Output.pdf")

'Close the document.

document.Close(True)

{% endhighlight %}

{% highlight UWP %}

//PDF supports embedding fonts or displaying a Unicode text in the PDF document by default in UWP platform. 

{% endhighlight %}

{% highlight Xamarin %}

//PDF supports embedding fonts or displaying a Unicode text in the PDF document by default in Xamarin platform. 

{% endhighlight %}

{% highlight ASP.NET Core %}

//PDF supports embedding fonts or displaying a Unicode text in the PDF document by default in ASP.NET Core platform. 

{% endhighlight %}

{% endtabs %}

## Drawing Right-To-Left text 

The Essential PDF allows you to draw the right-to-left language text in a PDF document. To draw RTL scripts such as Arabic, Hebrew, Persian, and Urdu, set the value of [TextDirection](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfStringFormat.html#Syncfusion_Pdf_Graphics_PdfStringFormat_TextDirection) property in the [PdfStringFormat](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfStringFormat.html) class to RightToLeft using [PdfTextDirection](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfTextDirection.html) Enum. The languages (e.g., Sindhi and Kurdish) that have more than one script and can be written in either right-to-left or left-to-right format. The LeftToRight value of the TextDirection property is used to draw RTL text in the left-to-right format. Refer to the following code sample.

{% tabs %}

{% highlight c# %}

//Create a new PDF document

PdfDocument doc = new PdfDocument();

//Add a page to the document

PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page

PdfGraphics graphics = page.Graphics;

//Create font

PdfFont font = new PdfTrueTypeFont(new Font("Arial", 14), true);

//Set the format for string

PdfStringFormat format = new PdfStringFormat();

//Set right-to-left text direction for RTL text

format.TextDirection = PdfTextDirection.RightToLeft;

//Set the text alignment

format.Alignment = PdfTextAlignment.Right;

format.ParagraphIndent = 35f;

//Read the text from file

StreamReader reader = new StreamReader("Arabic.txt", Encoding.Unicode);

string text = reader.ReadToEnd();

reader.Close();

//Draw string with right-to-left format

graphics.DrawString(text, font, PdfBrushes.Black, new RectangleF(0, 0, page.GetClientSize().Width, page.GetClientSize().Height), format);

//Set left-to-right text direction for RTL text

format.TextDirection = PdfTextDirection.LeftToRight;

//Set the text alignment

format.Alignment = PdfTextAlignment.Left;

//Draw string with left-to-right format

graphics.DrawString(text, font, PdfBrushes.Black, new RectangleF(0, 100, page.GetClientSize().Width, page.GetClientSize().Height), format);

//Save the document

doc.Save("Output.pdf");

//Close the document

doc.Close(true);


{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document

Dim doc As PdfDocument = New PdfDocument()

'Add a page to the document

Dim page As PdfPage = doc.Pages.Add()

'Create PDF graphics for the page

Dim graphics As PdfGraphics = page.Graphics

'Create font

Dim font As PdfFont = New PdfTrueTypeFont(New Font("Arial", 14), True)

'Set the format for string

Dim format As PdfStringFormat = New PdfStringFormat()

'Set right-to-left text direction for RTL text

format.TextDirection = PdfTextDirection.RightToLeft

'Set the alignment

format.Alignment = PdfTextAlignment.Right

format.ParagraphIndent = 35.0F

'Read the text from file

Dim reader As StreamReader = New StreamReader("Arabic.txt", Encoding.Unicode)

Dim text As String = reader.ReadToEnd()

reader.Close()

'Draw string with right-to-left format

graphics.DrawString(text, font, PdfBrushes.Black, new RectangleF(0, 0, page.GetClientSize().Width, page.GetClientSize().Height), format)

'Set left-to-right text direction for RTL text

format.TextDirection = PdfTextDirection.LeftToRight

'Set the text alignment

format.Alignment = PdfTextAlignment.Left

'Draw string with left-to-right format

graphics.DrawString(text, font, PdfBrushes.Black, new RectangleF(0, 100, page.GetClientSize().Width, page.GetClientSize().Height), format)

'Save the document

doc.Save("Output.pdf")

'Close the document

doc.Close(True)

{% endhighlight %}

{% highlight UWP %}

 //Create a new PDF document

PdfDocument doc = new PdfDocument();

//Add a page to the document

PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page

PdfGraphics graphics = page.Graphics;

//Load the TrueType font

Stream fontStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.arial.ttf");

//Initialize the PDF TrueType font

PdfFont font = new PdfTrueTypeFont(fontStream, 14, PdfFontStyle.Regular);

//Set the format for string

PdfStringFormat format = new PdfStringFormat();

//Set right-to-left text direction for RTL text

format.TextDirection = PdfTextDirection.RightToLeft;

//Set the alignment

format.Alignment = PdfTextAlignment.Right;

format.ParagraphIndent = 35f;

//Read the text from file

Stream inputStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Arabic.txt");

StreamReader reader = new StreamReader(inputStream);

string text = reader.ReadToEnd();

reader.Dispose();

//Draw string with right-to-left format

graphics.DrawString(text, font, PdfBrushes.Black, new RectangleF(0, 0, page.GetClientSize().Width, page.GetClientSize().Height), format);

//Set left-to-right text direction for RTL text

format.TextDirection = PdfTextDirection.LeftToRight;

//Set the text alignment

format.Alignment = PdfTextAlignment.Left;

//Draw string with left-to-right format

graphics.DrawString(text, font, PdfBrushes.Black, new RectangleF(0, 100, page.GetClientSize().Width, page.GetClientSize().Height), format);

//Save the document into memory stream

MemoryStream stream = new MemoryStream();

await doc.SaveAsync(stream);

//Close the document

doc.Close(true);

//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document

PdfDocument doc = new PdfDocument();

//Add a page to the document

PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page

PdfGraphics graphics = page.Graphics;

//Create font

FileStream fontStream = new FileStream("arial.ttf", FileMode.Open, FileAccess.Read);

PdfFont font = new PdfTrueTypeFont(fontStream, 14);

//Set the format for string

PdfStringFormat format = new PdfStringFormat();

//Set right-to-left text direction for RTL text

format.TextDirection = PdfTextDirection.RightToLeft;

//Set the alignment

format.Alignment = PdfTextAlignment.Right;

format.ParagraphIndent = 35f;

//Read the text from file

FileStream rtlText = new FileStream("Arabic.txt", FileMode.Open, FileAccess.Read);

StreamReader reader = new StreamReader(rtlText, Encoding.Unicode);

string text = reader.ReadToEnd();

reader.Dispose();

//Draw string with right-to-left format

graphics.DrawString(text, font, PdfBrushes.Black, new RectangleF(0, 0, page.GetClientSize().Width, page.GetClientSize().Height), format);

//Set left-to-right text direction for RTL text

format.TextDirection = PdfTextDirection.LeftToRight;

//Set the text alignment

format.Alignment = PdfTextAlignment.Left;

//Draw string with left-to-right format

graphics.DrawString(text, font, PdfBrushes.Black, new RectangleF(0, 100, page.GetClientSize().Width, page.GetClientSize().Height), format);

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the document into memory stream

doc.Save(stream);

//If the position is not set to '0', then the PDF will be empty

stream.Position = 0;

//Close the document

doc.Close(true);

//Defining the ContentType for PDF file

string contentType = "application/pdf";

//Define the file name

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Create a new PDF document

PdfDocument doc = new PdfDocument();

//Add a page to the document

PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page

PdfGraphics graphics = page.Graphics;

//Load the TrueType font

Stream fontStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.arial.ttf");

//Initialize the PDF TrueType font

PdfFont font = new PdfTrueTypeFont(fontStream, 14, PdfFontStyle.Regular);

//Read the text from file

Stream inputStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Arabic.txt");

StreamReader reader = new StreamReader(inputStream);

string text = reader.ReadToEnd();

reader.Dispose();

//Set the format for string

PdfStringFormat format = new PdfStringFormat();

//Set the property for RTL text

format.TextDirection = PdfTextDirection.RightToLeft;

//Set the alignment

format.Alignment = PdfTextAlignment.Right;

format.ParagraphIndent = 35f;

//Draw string with right-to-left format

graphics.DrawString(text, font, PdfBrushes.Black, new Syncfusion.Drawing.RectangleF(0, 0, page.GetClientSize().Width, page.GetClientSize().Height), format);

//Set left-to-right text direction for RTL text

format.TextDirection = PdfTextDirection.LeftToRight;

//Set the text alignment

format.Alignment = PdfTextAlignment.Left;

//Draw string with left-to-right format

graphics.DrawString(text, font, PdfBrushes.Black, new Syncfusion.Drawing.RectangleF(0, 100, page.GetClientSize().Width, page.GetClientSize().Height), format);

//Save the document into memory stream

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

## Adding a HTML Styled Text

Essential PDF provides support to render simple HTML string in a PDF document that can flow through multiple pages. This can be done by using the [PdfHTMLTextElement](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfHTMLTextElement.html) class.

1. The PdfHTMLTextElement class provides support for a basic set of HTML tags, to render HTML format text in the PDF document.

   Supported tags (Should be XHTML-compliant)

   * Font
   * B
   * I
   * U
   * Sub
   * Sup
   * BR
   
2. The [PdfMetafileLayoutFormat](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfMetafileLayoutFormat.html) class enables to break the HTML text into multiple pages.
3. Complex HTML with CSS are not supported in this class. Please use [HTML to PDF](/file-formats/pdf/converting-html-to-pdf "Converting HTML documents To PDF") section for complex HTML with CSS and URL's

The following code example illustrates how to render the HTML string in a PDF document.   

{% tabs %}

{% highlight c# %}

//Create a new PDF document.

PdfDocument doc = new PdfDocument();

//Add a page to the document.

PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Courier, 14);

//Simple HTML content

string htmlText = "<font color='#0000F8'>Essential PDF</font> is a <u><i>.NET</i></u> " +

"library with the capability to produce Adobe PDF files ";

//Render HtmlText.

PdfHTMLTextElement richTextElement = new PdfHTMLTextElement(htmlText, font, PdfBrushes.Black);

richTextElement.TextAlign = TextAlign.Left;

//Format Layout.

PdfMetafileLayoutFormat format = new PdfMetafileLayoutFormat();

format.Layout = PdfLayoutType.Paginate;

format.Break = PdfLayoutBreakType.FitPage;



//Draw htmlString.

richTextElement.Draw(page, new RectangleF(0, 20, page.GetClientSize().Width, page.GetClientSize().Height), format);

//Save the document.

doc.Save("Output.pdf");

//Close the document.

doc.Close(true);



{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim doc As New PdfDocument()

'Add a page to the document.

Dim page As PdfPage = doc.Pages.Add()

'Create PDF graphics for the page.

Dim graphics As PdfGraphics = page.Graphics

'Set the font.

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Courier, 14)

'Simple HTML content

Dim htmlText As String = "<font color='#0000F8'>Essential PDF</font> is a <u><i>.NET</i></u> " + "library with the capability to produce Adobe PDF files "

'Render HtmlText.

Dim richTextElement As New PdfHTMLTextElement(htmlText, font, PdfBrushes.Black)

richTextElement.TextAlign = TextAlign.Left

'Format Layout.

Dim format As New PdfMetafileLayoutFormat()

format.Layout = PdfLayoutType.Paginate

format.Break = PdfLayoutBreakType.FitPage

'Draw htmlString.

richTextElement.Draw(page, New RectangleF(0, 20, page.GetClientSize().Width, page.GetClientSize().Height), format)

'Save the document.

doc.Save("Output.pdf")

'Close the document.

doc.Close(True)

{% endhighlight %}

{% highlight UWP %}

//PDF supports Adding HTML Styled Text only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

{% endhighlight %}

{% highlight ASP.NET Core %}

//create a new PDF document

PdfDocument doc = new PdfDocument();

//Add a page to the document

PdfPage page = doc.Pages.Add();

//create PDF graphics for the page

PdfGraphics graphics = page.Graphics;

//set the font

PdfFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 14, PdfFontStyle.Regular);

//simple HTML content

string htmlText = "<font color='#0000F8' face='TimesRoman' size='14'><i><b><u>Essential PDF</u></b></i></font> is a <u><i>.NET</i></u> library with the capability to produce Adobe PDF files";

//Render Html text

PdfHTMLTextElement richTextElement = new PdfHTMLTextElement(htmlText, font, PdfBrushes.Black);

//Format layout

PdfLayoutFormat format = new PdfLayoutFormat();

format.Layout = PdfLayoutType.Paginate;

format.Break = PdfLayoutBreakType.FitPage;

//Draw htmlString.

richTextElement.Draw(page, new RectangleF(0, 20, page.GetClientSize().Width, page.GetClientSize().Height), format);

//Save the document into stream 

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty. 

stream.Position = 0;

//Close the document 

loadedDocument.Close(true);

//Defining the ContentType for pdf file. 

string contentType = "application/pdf";

//Define the file name. 

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name. 

return File(stream, contentType, fileName);


{% endhighlight %}

{% highlight Xamarin %}

//PDF supports Adding HTML Styled Text only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

{% endhighlight %}

{% endtabs %}

## Creating a multicolumn PDF document

Essential PDF allows you to create multi-column text in PDF document by using [PdfTextElement](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfTextElement.html) class. The following code example illustrates the same.

{% tabs %}

{% highlight c# %}

//Create a PDF document instance

PdfDocument document = new PdfDocument();

//Add page to the document

PdfPage page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

string text = "Adventure Works Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company. The company manufactures and sells metal and composite bicycles to North American, European and Asian commercial markets. While its base operation is located in Washington with 290 employees, several regional sales teams are located throughout their market base.";

//Create a text element with the text and font

PdfTextElement textElement = new PdfTextElement(text, new PdfStandardFont(PdfFontFamily.TimesRoman, 14));

//Draw the text in the first column

textElement.Draw(page, new RectangleF(0, 0, page.GetClientSize().Width / 2, page.GetClientSize().Height));

textElement = new PdfTextElement(text, new PdfStandardFont(PdfFontFamily.TimesRoman, 14));

//Draw the text in the second column

textElement.Draw(page, new RectangleF(page.GetClientSize().Width / 2, 0, page.GetClientSize().Width / 2, page.GetClientSize().Height));

document.Save("Output.pdf");

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a PDF document instance

Dim document As New PdfDocument()

'Add page to the document

Dim page As PdfPage = document.Pages.Add()

Dim graphics As PdfGraphics = page.Graphics

Dim text As String = "Adventure Works Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company. The company manufactures and sells metal and composite bicycles to North American, European and Asian commercial markets. While its base operation is located in Washington with 290 employees, several regional sales teams are located throughout their market base."

'Create a text element with the text and font

Dim textElement As New PdfTextElement(text, New PdfStandardFont(PdfFontFamily.TimesRoman, 14))

'Draw the text in the first column

textElement.Draw(page, New RectangleF(0, 0, page.GetClientSize().Width / 2, page.GetClientSize().Height))

textElement = New PdfTextElement(text, New PdfStandardFont(PdfFontFamily.TimesRoman, 14))

'Draw the text in the second column

textElement.Draw(page, New RectangleF(page.GetClientSize().Width / 2, 0, page.GetClientSize().Width / 2, page.GetClientSize().Height))

document.Save("Output.pdf")

document.Close(True)

{% endhighlight %}

{% highlight UWP %}

//Create a PDF document instance

PdfDocument document = new PdfDocument();

//Add page to the document

PdfPage page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

string text = "Adventure Works Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company. The company manufactures and sells metal and composite bicycles to North American, European and Asian commercial markets. While its base operation is located in Washington with 290 employees, several regional sales teams are located throughout their market base.";

//Create a text element with the text and font

PdfTextElement textElement = new PdfTextElement(text, new PdfStandardFont(PdfFontFamily.TimesRoman, 14));

//Draw the text in the first column

textElement.Draw(page, new RectangleF(0, 0, page.GetClientSize().Width / 2, page.GetClientSize().Height));

textElement = new PdfTextElement(text, new PdfStandardFont(PdfFontFamily.TimesRoman, 14));

//Draw the text in the second column

textElement.Draw(page, new RectangleF(page.GetClientSize().Width / 2, 0, page.GetClientSize().Width / 2, page.GetClientSize().Height));

//Save the document into memory stream.

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document.

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Output.pdf");


{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a PDF document instance

PdfDocument document = new PdfDocument();

//Add page to the document

PdfPage page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

string text = "Adventure Works Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company. The company manufactures and sells metal and composite bicycles to North American, European and Asian commercial markets. While its base operation is located in Washington with 290 employees, several regional sales teams are located throughout their market base.";

//Create a text element with the text and font

PdfTextElement textElement = new PdfTextElement(text, new PdfStandardFont(PdfFontFamily.TimesRoman, 14));

//Draw the text in the first column

textElement.Draw(page, new RectangleF(0, 0, page.GetClientSize().Width / 2, page.GetClientSize().Height));

textElement = new PdfTextElement(text, new PdfStandardFont(PdfFontFamily.TimesRoman, 14));

//Draw the text in the second column

textElement.Draw(page, new RectangleF(page.GetClientSize().Width / 2, 0, page.GetClientSize().Width / 2, page.GetClientSize().Height));

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the document into memory stream

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

{% highlight Xamarin %}

//Create a PDF document instance

PdfDocument document = new PdfDocument();

//Add page to the document

PdfPage page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

string text = "Adventure Works Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company. The company manufactures and sells metal and composite bicycles to North American, European and Asian commercial markets. While its base operation is located in Washington with 290 employees, several regional sales teams are located throughout their market base.";

//Create a text element with the text and font

PdfTextElement textElement = new PdfTextElement(text, new PdfStandardFont(PdfFontFamily.TimesRoman, 14));

//Draw the text in the first column

textElement.Draw(page, new Syncfusion.Drawing.RectangleF(0, 0, page.GetClientSize().Width / 2, page.GetClientSize().Height));

textElement = new PdfTextElement(text, new PdfStandardFont(PdfFontFamily.TimesRoman, 14));

//Draw the text in the second column

textElement.Draw(page, new Syncfusion.Drawing.RectangleF(page.GetClientSize().Width / 2, 0, page.GetClientSize().Width / 2, page.GetClientSize().Height));

//Save the document into memory stream.

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

The [PdfLayoutFormat](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfLayoutFormat.html) class helps to allow the text to flow across pages. The [PdfLayoutResult](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfLayoutResult.html) class provides the rendered bounds of the previously added text which can be used to place successive elements without overlapping.

The following code snippet illustrates how to add elements relatively and also allow the text to flow across multiple pages.

{% tabs %}

{% highlight c# %}

//Create a PDF document instance

PdfDocument document = new PdfDocument();

//Add page to the document

PdfPage page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

//Read the long text from the text file.

StreamReader reader = new StreamReader(@"input.txt", Encoding.ASCII);

string text = reader.ReadToEnd();

reader.Close();



const int paragraphGap = 10;



//Create a text element with the text and font

PdfTextElement textElement = new PdfTextElement(text, new PdfStandardFont(PdfFontFamily.TimesRoman, 14));

PdfLayoutFormat layoutFormat = new PdfLayoutFormat();

layoutFormat.Layout = PdfLayoutType.Paginate;

layoutFormat.Break = PdfLayoutBreakType.FitPage;



//Draw the first paragraph

PdfLayoutResult result = textElement.Draw(page, new RectangleF(0, 0, page.GetClientSize().Width / 2, page.GetClientSize().Height), layoutFormat);

//Draw the second paragraph from the first paragraph end position

result = textElement.Draw(page, new RectangleF(0, result.Bounds.Bottom + paragraphGap, page.GetClientSize().Width / 2, page.GetClientSize().Height), layoutFormat);

document.Save("Output.pdf");

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a PDF document instance

Dim document As New PdfDocument()

'Add page to the document

Dim page As PdfPage = document.Pages.Add()

Dim graphics As PdfGraphics = page.Graphics

'Read the RTL text from the text file.

Dim reader As New StreamReader("input.txt", Encoding.ASCII)

Dim text As String = reader.ReadToEnd()

reader.Close()

Const paragraphGap As Integer = 10

'Create a text element with the text and font

Dim textElement As New PdfTextElement(text, New PdfStandardFont(PdfFontFamily.TimesRoman, 14))

Dim layoutFormat As New PdfLayoutFormat()

layoutFormat.Layout = PdfLayoutType.Paginate

layoutFormat.Break = PdfLayoutBreakType.FitPage

'Draw the first paragraph

Dim result As PdfLayoutResult = textElement.Draw(page, New RectangleF(0, 0, page.GetClientSize().Width / 2, page.GetClientSize().Height), layoutFormat)

'Draw the second paragraph from the first paragraph end position

result = textElement.Draw(page, New RectangleF(0, result.Bounds.Bottom + paragraphGap, page.GetClientSize().Width / 2, page.GetClientSize().Height), layoutFormat)

document.Save("Output.pdf")

document.Close(True)

{% endhighlight %}

{% highlight UWP %}

 //Create a PDF document instance

PdfDocument document = new PdfDocument();

//Add page to the document

PdfPage page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

//Read the long text from the text file.

Stream inputStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Input.txt");

StreamReader reader = new StreamReader(inputStream, Encoding.ASCII);

string text = reader.ReadToEnd();

reader.Dispose();

const int paragraphGap = 10;

//Create a text element with the text and font

PdfTextElement textElement = new PdfTextElement(text, new PdfStandardFont(PdfFontFamily.TimesRoman, 14));

PdfLayoutFormat layoutFormat = new PdfLayoutFormat();

layoutFormat.Layout = PdfLayoutType.Paginate;

layoutFormat.Break = PdfLayoutBreakType.FitPage;

//Draw the first paragraph

PdfLayoutResult result = textElement.Draw(page, new RectangleF(0, 0, page.GetClientSize().Width / 2, page.GetClientSize().Height), layoutFormat);

//Draw the second paragraph from the first paragraph end position

result = textElement.Draw(page, new RectangleF(0, result.Bounds.Bottom + paragraphGap, page.GetClientSize().Width / 2, page.GetClientSize().Height), layoutFormat);

//Save the document into memory stream.

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document.

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

 //Create a PDF document instance

PdfDocument document = new PdfDocument();

//Add page to the document

PdfPage page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

//Read the long text from the text file.

FileStream inputStream = new FileStream("Input.txt", FileMode.Open, FileAccess.Read);

StreamReader reader = new StreamReader(inputStream, Encoding.ASCII);

string text = reader.ReadToEnd();

reader.Dispose();


const int paragraphGap = 10;


//Create a text element with the text and font

PdfTextElement textElement = new PdfTextElement(text, new PdfStandardFont(PdfFontFamily.TimesRoman, 14));

PdfLayoutFormat layoutFormat = new PdfLayoutFormat();

layoutFormat.Layout = PdfLayoutType.Paginate;

layoutFormat.Break = PdfLayoutBreakType.FitPage;

//Draw the first paragraph

PdfLayoutResult result = textElement.Draw(page, new RectangleF(0, 0, page.GetClientSize().Width / 2, page.GetClientSize().Height), layoutFormat);

//Draw the second paragraph from the first paragraph end position

result = textElement.Draw(page, new RectangleF(0, result.Bounds.Bottom + paragraphGap, page.GetClientSize().Width / 2, page.GetClientSize().Height), layoutFormat);

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the document into memory stream

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

{% highlight Xamarin %}

//Create a PDF document instance

PdfDocument document = new PdfDocument();

//Add page to the document

PdfPage page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

//Read the long text from the text file.

Stream inputStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.txt");

StreamReader reader = new StreamReader(inputStream, Encoding.UTF8);

string text = reader.ReadToEnd();

reader.Dispose();


const int paragraphGap = 10;


//Create a text element with the text and font

PdfTextElement textElement = new PdfTextElement(text, new PdfStandardFont(PdfFontFamily.TimesRoman, 14));

PdfLayoutFormat layoutFormat = new PdfLayoutFormat();

layoutFormat.Layout = PdfLayoutType.Paginate;

layoutFormat.Break = PdfLayoutBreakType.FitPage;

//Draw the first paragraph

PdfLayoutResult result = textElement.Draw(page, new Syncfusion.Drawing.RectangleF(0, 0, page.GetClientSize().Width / 2, page.GetClientSize().Height), layoutFormat);

//Draw the second paragraph from the first paragraph end position

result = textElement.Draw(page, new Syncfusion.Drawing.RectangleF(0, result.Bounds.Bottom + paragraphGap, page.GetClientSize().Width / 2, page.GetClientSize().Height), layoutFormat);

//Save the document into memory stream.

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

## Inserting Rich Text Format contents 

Essential PDF allows you to insert a RTF text into a PDF document by converting it as bitmap or metafile image and rendering it using [FromRtf](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfImage.html#Syncfusion_Pdf_Graphics_PdfImage_FromRtf_System_String_System_Single_Syncfusion_Pdf_Graphics_PdfImageType_) method of [PdfImage](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfImage.html) class.

The following code example illustrates how to insert RTF text in PDF document.

{% tabs %}

{% highlight c# %}

//Create a new PDF document.

PdfDocument doc = new PdfDocument();

//Add a page.

PdfPage page = doc.Pages.Add();

SizeF bounds = page.GetClientSize();

//Read RTF document.

StreamReader reader = new StreamReader(@"input.rtf", Encoding.ASCII);

string text = reader.ReadToEnd();

reader.Close();

//Convert it to Metafile.

PdfMetafile imageMetafile = (PdfMetafile)PdfImage.FromRtf(text, bounds.Width, PdfImageType.Metafile);

PdfMetafileLayoutFormat format = new PdfMetafileLayoutFormat();

//Allow text to flow multiple pages without any break.

format.SplitTextLines = true;

//Draws image.

imageMetafile.Draw(page, 0, 0, format);

//Save the document.

doc.Save("Output.pdf");

doc.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim doc As New PdfDocument()

'Add a page.

Dim page As PdfPage = doc.Pages.Add()

Dim bounds As SizeF = page.GetClientSize()

'Read RTF document.

Dim reader As New StreamReader("input.rtf", Encoding.ASCII)

Dim text As String = reader.ReadToEnd()

reader.Close()

'Convert it to Metafile.

Dim imageMetafile As PdfMetafile = DirectCast(PdfImage.FromRtf(text, bounds.Width, PdfImageType.Metafile), PdfMetafile)

Dim format As New PdfMetafileLayoutFormat()

'Allow text to flow multiple pages without any break.

format.SplitTextLines = True

'Draws image.

imageMetafile.Draw(page, 0, 0, format)

'Save the document.

doc.Save("Output.pdf")

doc.Close(True)

{% endhighlight %}

{% highlight UWP %}

//PDF supports Inserting Rich Text Format contents only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

{% endhighlight %}

{% highlight ASP.NET Core %}

//PDF supports Inserting Rich Text Format contents only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

{% endhighlight %}

{% highlight Xamarin %}

//PDF supports Inserting Rich Text Format contents only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

{% endhighlight %}

{% endtabs %}


N> For converting complex RTF content to PDF, refer the [RTF to PDF](/file-formats/pdf/working-with-document-conversions#converting-rtf-documents-to-pdf "Working with document conversions") section.

## Adding an Ordered List 


Essential PDF allows you to create an ordered list in the document. Ordered List is represented by the [PdfOrderedList](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Lists.PdfOrderedList.html) class and can be numerical or alphabetical. The following code snippet illustrates the same.

{% tabs %}

{% highlight c# %}

//Create a new instance of PdfDocument class.

PdfDocument document = new PdfDocument();

//Add a new page to the document.

PdfPage page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

SizeF size = page.Graphics.ClientSize;

//Create font 

PdfFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 10, PdfFontStyle.Italic);

string[] products = { "Tools", "Grid", "Chart", "Edit", "Diagram", "XlsIO", "Grouping", "Calculate", "PDF", "HTMLUI", "DocIO" };

//Create string format

PdfStringFormat format = new PdfStringFormat();

format.LineSpacing = 10f;

//Create Ordered list

PdfOrderedList pdfList = new PdfOrderedList();

pdfList.Marker.Brush = PdfBrushes.Black;

pdfList.Indent = 20;

//Set format for sub list

pdfList.Font = font;

pdfList.StringFormat = format;

foreach (string s in products)

{

//Add items

pdfList.Items.Add(string.Concat("Essential ", s));

}

pdfList.Draw(page, new RectangleF(0, 20, size.Width, size.Height));  

// Save and close the document.

document.Save("Output.pdf");

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}

'Create a new instance of PdfDocument class.

Dim document As New PdfDocument()

'Add a new page to the document.

Dim page As PdfPage = document.Pages.Add()

Dim graphics As PdfGraphics = page.Graphics

Dim size As SizeF = page.Graphics.ClientSize

'Create font 

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.TimesRoman, 10, PdfFontStyle.Italic)

Dim products As String() = {"Tools", "Grid", "Chart", "Edit", "Diagram", "XlsIO", _

"Grouping", "Calculate", "PDF", "HTMLUI", "DocIO"}

'Create string format

Dim format As New PdfStringFormat()

format.LineSpacing = 10.0F

'Create Ordered list

Dim pdfList As New PdfOrderedList()

pdfList.Marker.Brush = PdfBrushes.Black

pdfList.Indent = 20

'Set format for sub list

pdfList.Font = font

pdfList.StringFormat = format

For Each s As String In products

'Add items

pdfList.Items.Add(String.Concat("Essential ", s))

Next

pdfList.Draw(page, New RectangleF(0, 20, size.Width, size.Height))

' Save and close the document.

document.Save("Output.pdf")

document.Close(True)

{% endhighlight %}

{% highlight UWP %}

//Create a new instance of PdfDocument class.

PdfDocument document = new PdfDocument();

//Add a new page to the document.

PdfPage page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

SizeF size = page.Graphics.ClientSize;

//Create font 

PdfFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 10, PdfFontStyle.Italic);

string[] products = { "Tools", "Grid", "Chart", "Edit", "Diagram", "XlsIO", "Grouping", "Calculate", "PDF", "HTMLUI", "DocIO" };

//Create string format

PdfStringFormat format = new PdfStringFormat();

format.LineSpacing = 10f;

//Create Ordered list

PdfOrderedList pdfList = new PdfOrderedList();

pdfList.Marker.Brush = PdfBrushes.Black;

pdfList.Indent = 20;

//Set format for sub list

pdfList.Font = font;

pdfList.StringFormat = format;

foreach (string s in products)

{

//Add items

pdfList.Items.Add(string.Concat("Essential ", s));

}

pdfList.Draw(page, new RectangleF(0, 20, size.Width, size.Height));

//Save the document into memory stream.

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document.

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Output.pdf"); 


{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new instance of PdfDocument class.

PdfDocument document = new PdfDocument();

//Add a new page to the document.

PdfPage page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

SizeF size = page.Graphics.ClientSize;

//Create font 

PdfFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 10, PdfFontStyle.Italic);

string[] products = { "Tools", "Grid", "Chart", "Edit", "Diagram", "XlsIO", "Grouping", "Calculate", "PDF", "HTMLUI", "DocIO" };

//Create string format

PdfStringFormat format = new PdfStringFormat();

format.LineSpacing = 10f;

//Create Ordered list

PdfOrderedList pdfList = new PdfOrderedList();

pdfList.Marker.Brush = PdfBrushes.Black;

pdfList.Indent = 20;

//Set format for sub list

pdfList.Font = font;

pdfList.StringFormat = format;

foreach (string s in products)

{

    //Add items

    pdfList.Items.Add(string.Concat("Essential ", s));

}

pdfList.Draw(page, new RectangleF(0, 20, size.Width, size.Height));

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the document into memory stream

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

{% highlight Xamarin %}

//Create a new instance of PdfDocument class.

PdfDocument document = new PdfDocument();

//Add a new page to the document.

PdfPage page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

Syncfusion.Drawing.SizeF size = page.Graphics.ClientSize;

//Create font 

PdfFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 10, PdfFontStyle.Italic);

string[] products = { "Tools", "Grid", "Chart", "Edit", "Diagram", "XlsIO", "Grouping", "Calculate", "PDF", "HTMLUI", "DocIO" };

//Create string format

PdfStringFormat format = new PdfStringFormat();

format.LineSpacing = 10f;

//Create Ordered list

PdfOrderedList pdfList = new PdfOrderedList();

pdfList.Marker.Brush = PdfBrushes.Black;

pdfList.Indent = 20;

//Set format for sub list

pdfList.Font = font;

pdfList.StringFormat = format;

foreach (string s in products)

{

//Add items

pdfList.Items.Add(string.Concat("Essential ", s));

}

pdfList.Draw(page, new Syncfusion.Drawing.RectangleF(0, 20, size.Width, size.Height));

//Save the document into memory stream.

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

## Adding an Unordered List 

Essential PDF also provides support to create an unordered List that is represented by the [PdfUnorderedList](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Lists.PdfUnorderedList.html) class. An Unordered list can be bullets, circle or an image. The following code snippet illustrates the same.

{% tabs %}

{% highlight c# %}

//Create a new instance of PdfDocument class.

PdfDocument document = new PdfDocument();

//Add a new page to the document.

PdfPage page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

SizeF size = page.Graphics.ClientSize;

//Create an unordered list

PdfUnorderedList list = new PdfUnorderedList();

//Set the marker style

list.Marker.Style = PdfUnorderedMarkerStyle.Disk;

//Create font and write title

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 12, PdfFontStyle.Regular);

//Create string format

PdfStringFormat format = new PdfStringFormat();

format.LineSpacing = 10f;

// Format list

list.Font = font;

list.StringFormat = format;

//Set list indent

list.Indent = 10;

//Add items to the list

list.Items.Add("PDF");

list.Items.Add("XlsIO");

list.Items.Add("DocIO");

list.Items.Add("PPT");

//Set text indent

list.TextIndent = 10;

//Draw list

list.Draw(page, new RectangleF(0, 10, size.Width, size.Height));

// Save and close the document.

document.Save("Output.pdf");

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a new instance of PdfDocument class.

Dim document As New PdfDocument()

'Add a new page to the document.

Dim page As PdfPage = document.Pages.Add()

Dim graphics As PdfGraphics = page.Graphics

Dim size As SizeF = page.Graphics.ClientSize

'Create an unordered list

Dim list As New PdfUnorderedList()

'Set the marker style

list.Marker.Style = PdfUnorderedMarkerStyle.Disk

'Create font and write title

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 12, PdfFontStyle.Regular)

'Create string format

Dim format As New PdfStringFormat()

format.LineSpacing = 10.0F

' Format list

list.Font = font

list.StringFormat = format

'Set list indent

list.Indent = 10

'Add items to the list

list.Items.Add("PDF")

list.Items.Add("XlsIO")

list.Items.Add("DocIO")

list.Items.Add("PPT")

'Set text indent

list.TextIndent = 10

'Draw list

list.Draw(page, New RectangleF(0, 10, size.Width, size.Height))

'Save and close the document.

document.Save("Output.pdf")

document.Close(True)

{% endhighlight %}

{% highlight UWP %}

//Create a new instance of PdfDocument class.

PdfDocument document = new PdfDocument();

//Add a new page to the document.

PdfPage page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

SizeF size = page.Graphics.ClientSize;

//Create an unordered list

PdfUnorderedList list = new PdfUnorderedList();

//Set the marker style

list.Marker.Style = PdfUnorderedMarkerStyle.Disk;

//Create font and write title

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 12, PdfFontStyle.Regular);

//Create string format

PdfStringFormat format = new PdfStringFormat();

format.LineSpacing = 10f;

// Format list

list.Font = font;

list.StringFormat = format;

//Set list indent

list.Indent = 10;

//Add items to the list

list.Items.Add("PDF");

list.Items.Add("XlsIO");

list.Items.Add("DocIO");

list.Items.Add("PPT");

//Set text indent

list.TextIndent = 10;

//Draw list

list.Draw(page, new RectangleF(0, 10, size.Width, size.Height));

//Save the document into memory stream.

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document.

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Output.pdf");


{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new instance of PdfDocument class.

PdfDocument document = new PdfDocument();

//Add a new page to the document.

PdfPage page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

SizeF size = page.Graphics.ClientSize;

//Create an unordered list

PdfUnorderedList list = new PdfUnorderedList();

//Set the marker style

list.Marker.Style = PdfUnorderedMarkerStyle.Disk;

//Create font and write title

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 12, PdfFontStyle.Regular);

//Create string format

PdfStringFormat format = new PdfStringFormat();

format.LineSpacing = 10f;

// Format list

list.Font = font;

list.StringFormat = format;

//Set list indent

list.Indent = 10;

//Add items to the list

list.Items.Add("PDF");

list.Items.Add("XlsIO");

list.Items.Add("DocIO");

list.Items.Add("PPT");

//Set text indent

list.TextIndent = 10;

//Draw list

list.Draw(page, new RectangleF(0, 10, size.Width, size.Height));

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the document into memory stream

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

{% highlight Xamarin %}

//Create a new instance of PdfDocument class.

PdfDocument document = new PdfDocument();

//Add a new page to the document.

PdfPage page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

Syncfusion.Drawing.SizeF size = page.Graphics.ClientSize;

//Create an unordered list

PdfUnorderedList list = new PdfUnorderedList();

//Set the marker style

list.Marker.Style = PdfUnorderedMarkerStyle.Disk;

//Create font and write title

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 12, PdfFontStyle.Regular);

//Create string format

PdfStringFormat format = new PdfStringFormat();

format.LineSpacing = 10f;

// Format list

list.Font = font;

list.StringFormat = format;

//Set list indent

list.Indent = 10;

//Add items to the list

list.Items.Add("PDF");

list.Items.Add("XlsIO");

list.Items.Add("DocIO");

list.Items.Add("PPT");

//Set text indent

list.TextIndent = 10;

//Draw list

list.Draw(page, new Syncfusion.Drawing.RectangleF(0, 10, size.Width, size.Height));

//Save the document into memory stream.

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

## Replace Fonts in an existing document

Essential PDF allows you to replace the fonts in an existing PDF document by using the [Replace](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.Fonts.PdfUsedFont.html#Syncfusion_Pdf_Graphics_Fonts_PdfUsedFont_Replace_Syncfusion_Pdf_Graphics_PdfFont_) method. The following code snippet illustrates the same.

{% tabs %}

{% highlight c# %}

//Creates a new PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");

//Replace font 
loadedDocument.UsedFonts[0].Replace(new PdfStandardFont(PdfFontFamily.TimesRoman, 12));

//Save the document
loadedDocument.Save("Output.pdf");

loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Creates a new PDF document.

Dim loadedDocument As New PdfLoadedDocument("Input.pdf")

'Replace font

loadedDocument.UsedFonts(0).Replace(New PdfStandardFont(PdfFontFamily.TimesRoman, 12))

'Save the document

loadedDocument.Save("Output.pdf")

loadedDocument.Close(True)

{% endhighlight %}

{% highlight UWP %}

//PDF supports Replace fonts in an existing document only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

{% endhighlight %}

{% highlight ASP.NET Core %}

//PDF supports Replace fonts in an existing document only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

{% endhighlight %}

{% highlight Xamarin %}

//PDF supports Replace fonts in an existing document only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

{% endhighlight %}

{% endtabs %}

## Search and get the bounds of a text in a document

You can search for a particular text in a document and get the bounds using [FindText](https://help.syncfusion.com/cr/file-formats/Syncfusion.Windows.Forms.PdfViewer.PdfViewerControl.html#Syncfusion_Windows_Forms_PdfViewer_PdfViewerControl_FindText_System_String_System_Collections_Generic_Dictionary_System_Int32_System_Collections_Generic_List_System_Drawing_RectangleF____) method of [PdfViewerControl](https://help.syncfusion.com/cr/windowsforms/Syncfusion.Windows.Forms.PdfViewer.PdfViewerControl.html) class. To include this functionality, you need to add the below mentioned assemblies as reference to the project.

1. Syncfusion.Compression.Base.dll
2. Syncfusion.Pdf.Base.dll
3. Syncfusion.PdfViewer.Windows.dll 

The following code snippet illustrates how to get the bound of a text from PDF document.

{% tabs %}

{% highlight c# %}

PdfViewerControl documentViewer = new PdfViewerControl();

//Load the PDF document

documentViewer.Load("Input.pdf");

//Get the occurrences of the target text and location.

Dictionary<int, List<RectangleF>> textSearch = new Dictionary<int, List<RectangleF>>();

bool IsMatchFound = documentViewer.FindText("hello", out textSearch);

documentViewer.Dispose();

{% endhighlight %}

{% highlight vb.net %}

Dim documentViewer As New PdfViewerControl()

'Load the PDF document

documentViewer.Load("Input.pdf")

'Get the occurrences of the target text and location.

Dim textSearch As New Dictionary(Of Integer, List(Of RectangleF))()

Dim IsMatchFound As Boolean = documentViewer.FindText("hello", textSearch)

documentViewer.Dispose()

{% endhighlight %}

{% endtabs %}

## Drawing complex script language text

Essential PDF allows you to add complex script language text in the PDF document by using the [ComplexScript](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfStringFormat.html#Syncfusion_Pdf_Graphics_PdfStringFormat_ComplexScript) property available in [PdfStringFormat](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfStringFormat.html) class. The following code snippet illustrates this.

{% tabs %}

{% highlight c# %}

//Create a new PDF document

PdfDocument doc = new PdfDocument();

//Add a page to the document

PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page

PdfGraphics graphics = page.Graphics;

//Set the font with Unicode option

Font font = new Font("Tahoma", 14);

PdfFont pdfFont = new PdfTrueTypeFont(font, true);

//Set the format for string

PdfStringFormat format = new PdfStringFormat();

//Set the format as complex script layout type

format.ComplexScript = true;

//Draw the text

graphics.DrawString("สวัสดีชาวโลก", pdfFont, PdfBrushes.Black, new RectangleF(0, 0, page.GetClientSize().Width, page.GetClientSize().Height), format);

//Save the document
 
doc.Save("Output.pdf");

//Close the document

doc.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document 

Dim doc As New PdfDocument()

'Add a page to the document

Dim page As PdfPage = doc.Pages.Add()

'Create PDF graphics for the page 

Dim graphics As PdfGraphics = page.Graphics

'Set the font with Unicode option 

Dim font As New Font("Tahoma", 14)

Dim pdfFont As PdfFont = New PdfTrueTypeFont(font, True)

'Set the format for string

Dim format As New PdfStringFormat()

'Set the format as complex script layout type 

format.ComplexScript = True

'Draw the text

graphics.DrawString("สวัสดีชาวโลก", pdfFont, PdfBrushes.Black, New RectangleF(0, 0, page.GetClientSize().Width, page.GetClientSize().Height), format)

'Save the document 

doc.Save("Output.pdf")

'Close the document

doc.Close(True)

{% endhighlight %}

{% highlight UWP %}

//Create a new PDF document

PdfDocument doc = new PdfDocument();

//Add a page to the document

PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page

PdfGraphics graphics = page.Graphics;

//Set the font with Unicode option

Stream fontStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("ComplexScriptSample.Assets.tahoma.ttf");

//Create a new PDF font instance

PdfFont font = new PdfTrueTypeFont(fontStream, 10);
           
//Set the format for string

PdfStringFormat format = new PdfStringFormat();

//Set the format as complex script layout type

format.ComplexScript = true;

//Draw the text

graphics.DrawString("สวัสดีชาวโลก", pdfFont, PdfBrushes.Black, new RectangleF(0, 0, page.GetClientSize().Width, page.GetClientSize().Height), format);

//Save the PDF document
         
MemoryStream stream = new MemoryStream();

await doc.SaveAsync(stream);

//Close the PDF document

doc.Close(true);

//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respected code samples

 Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document

PdfDocument doc = new PdfDocument();

//Add a page to the document

PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page

PdfGraphics graphics = page.Graphics;

FileStream fontStream = new FileStream("tahoma.ttf", FileMode.Open, FileAccess.Read);

//Create a new PDF font instance

PdfFont font = new PdfTrueTypeFont(fontStream, 10);
           
//Set the format for string

PdfStringFormat format = new PdfStringFormat();

//Set the format as complex script layout type

format.ComplexScript = true;

//Draw the text

graphics.DrawString("สวัสดีชาวโลก", pdfFont, PdfBrushes.Black, new RectangleF(0, 0, page.GetClientSize().Width, page.GetClientSize().Height), format);

//Save the PDF document
        
MemoryStream stream = new MemoryStream();

doc.Save(stream);

//Close the PDF document

doc.Close(true);

//Defining the content type for PDF file.

string contentType = "application/pdf";

//Define the file name

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Create a new PDF document

PdfDocument doc = new PdfDocument();

//Add a page to the document

PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page

PdfGraphics graphics = page.Graphics;

//Load the font as stream

Stream fontStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.tahoma.ttf");

//Create a new PDF font instance

PdfFont font = new PdfTrueTypeFont(fontStream, 10);
           
//Set the format for string

PdfStringFormat format = new PdfStringFormat();

//Set the format as complex script layout type

format.ComplexScript = true;

//Draw the text

graphics.DrawString("สวัสดีชาวโลก", pdfFont, PdfBrushes.Black, new RectangleF(0, 0, page.GetClientSize().Width, page.GetClientSize().Height), format);

//Save the PDF document
           
MemoryStream stream = new MemoryStream();

doc.Save(stream);

//Close the PDF document

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

You can add the complex script language text in an existing PDF document by using the following code sample.

{% tabs %}

{% highlight c# %}

//Load a PDF document

PdfLoadedDocument doc = new PdfLoadedDocument("input.pdf");

//Get first page from the document

PdfLoadedPage page = doc.Pages[0] as PdfLoadedPage;

//Create PDF graphics for the page

PdfGraphics graphics = page.Graphics;

//Set the font with Unicode option

Font font = new Font("Tahoma", 14);

PdfFont pdfFont = new PdfTrueTypeFont(font, true);

//Set the format for string

PdfStringFormat format = new PdfStringFormat();

//Set the format as complex script layout type

format.ComplexScript = true;

//Draw the text

graphics.DrawString("สวัสดีชาวโลก", pdfFont, PdfBrushes.Black, new RectangleF(0, 0, page.Size.Width, page.Size.Height), format);

//Save the document

doc.Save("Output.pdf");

//Close the document

doc.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Load a PDF document

Dim doc As New PdfLoadedDocument("input.pdf")

'Get first page from the document 

Dim page As PdfLoadedPage = TryCast(doc.Pages(0), PdfLoadedPage)

'Create PDF graphics for the page 

Dim graphics As PdfGraphics = page.Graphics

'Set the font with Unicode option 

Dim font As New Font("Tahoma", 14)

Dim pdfFont As PdfFont = New PdfTrueTypeFont(font, True)

'Set the format for string 

Dim format As New PdfStringFormat()

'Set the format as complex script layout type 

format.ComplexScript = True

'Draw the text 

graphics.DrawString("สวัสดีชาวโลก", pdfFont, PdfBrushes.Black, New RectangleF(0, 0, page.Size.Width, page.Size.Height), format)

'Save the document 

doc.Save("Output.pdf")

'Close the document

doc.Close(True)

{% endhighlight %}

{% highlight UWP %}

Stream inputFileStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("input.pdf");

//Load a PDF document

PdfLoadedDocument doc = new PdfLoadedDocument(inputFileStream);

//Get first page from the document

PdfLoadedPage page = doc.Pages[0] as PdfLoadedPage;

//Create PDF graphics for the page

PdfGraphics graphics = page.Graphics;

//Set the font with Unicode option

Font font = new Font("Tahoma", 14);

PdfFont pdfFont = new PdfTrueTypeFont(font, true);

//Set the format for string

PdfStringFormat format = new PdfStringFormat();

//Set the format as complex script layout type

format.ComplexScript = true;

//Draw the text

graphics.DrawString("สวัสดีชาวโลก", pdfFont, PdfBrushes.Black, new RectangleF(0, 0, page.Size.Width, page.Size.Height), format);

//Save the PDF document

MemoryStream stream = new MemoryStream();

await doc.SaveAsync(stream);

//Close the PDF document

doc.Close(true);

//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

FileStream inputFileStream = new FileStream("input.pdf", FileMode.Open, FileAccess.Read);

//Load a PDF document

PdfLoadedDocument doc = new PdfLoadedDocument(inputFileStream);

//Get first page from the document

PdfLoadedPage page = doc.Pages[0] as PdfLoadedPage;

//Create PDF graphics for the page

PdfGraphics graphics = page.Graphics;

//Set the font with Unicode option

Font font = new Font("Tahoma", 14);

PdfFont pdfFont = new PdfTrueTypeFont(font, true);

//Set the format for string

PdfStringFormat format = new PdfStringFormat();

//Set the format as complex script layout type

format.ComplexScript = true;

//Draw the text

graphics.DrawString("สวัสดีชาวโลก", pdfFont, PdfBrushes.Black, new RectangleF(0, 0, page.Size.Width, page.Size.Height), format);

//Save the PDF document
          
MemoryStream stream = new MemoryStream();

await doc.Save(stream);

//Close the PDF document

doc.Close(true);

//Defining the content type for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

Stream inputFileStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.pdf");

//Load a PDF document

PdfLoadedDocument doc = new PdfLoadedDocument(inputFileStream);

//Get first page from the document

PdfLoadedPage page = doc.Pages[0] as PdfLoadedPage;

//Create PDF graphics for the page

PdfGraphics graphics = page.Graphics;

//Set the font with Unicode option

Font font = new Font("Tahoma", 14);

PdfFont pdfFont = new PdfTrueTypeFont(font, true);

//Set the format for string

PdfStringFormat format = new PdfStringFormat();

//Set the format as complex script layout type

format.ComplexScript = true;

//Draw the text

graphics.DrawString("สวัสดีชาวโลก", pdfFont, PdfBrushes.Black, new RectangleF(0, 0, page.Size.Width, page.Size.Height), format);

//Save the PDF document
          
MemoryStream stream = new MemoryStream();

await doc.Save(stream);

//Close the PDF document

doc.Close(true);

//Save the stream into PDF file

//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples.

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

## Drawing text using OpenType font

Essential PDF supports drawing text on a PDF document with OpenType font using [PdfTrueTypeFont](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfTrueTypeFont.html) class, by providing the path of font file from local file system. The following code snippet illustrates this.

{% tabs %}

{% highlight c# %}

//Create a new PDF document

PdfDocument document = new PdfDocument();

//Add a page to the document

PdfPage page = document.Pages.Add();

//Create  font

Stream fontStream = System.IO.File.OpenRead("Font.otf");

PdfFont font = new PdfTrueTypeFont(fontStream, 14);

//Text to draw

string text = "Syncfusion Essential PDF is a.NET PDF library used to create, read, and edit PDF files in any application";

//Get page client size

SizeF clipBounds = page.Graphics.ClientSize;

RectangleF rect = new RectangleF(0, 0, clipBounds.Width, clipBounds.Height); 

//Draw the text

page.Graphics.DrawString(text, font, PdfBrushes.Blue, rect);

//Save the document

document.Save("Output.pdf");

//Close the document

document.Close(true); 

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document

Dim document As PdfDocument = New PdfDocument 

'Add a page to the document

Dim page As PdfPage = document.Pages.Add

'Create font

Dim fontStream As Stream = System.IO.File.OpenRead("Font.otf")

Dim font As PdfFont = New PdfTrueTypeFont(fontStream, 14)

'Text to draw

Dim text As String = "Syncfusion Essential PDF is a.NET PDF library used to create, read, and edit PDF files in any application"

'Get page client size

Dim clipBounds As SizeF = page.Graphics.ClientSize

Dim rect As RectangleF = New RectangleF(0, 0, clipBounds.Width, clipBounds.Height)

'Draw the text

page.Graphics.DrawString(text, font, PdfBrushes.Blue, rect)

'Save the document

document.Save("Output.pdf")

'Close the document

document.Close(true)

{% endhighlight %}

{% highlight UWP %}

//Create a new PDF document

PdfDocument document = new PdfDocument();

//Add a page

PdfPage page = document.Pages.Add();

//Create font

Stream fontStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Font.otf");

PdfFont font = new PdfTrueTypeFont(fontStream, 14);

//Text to draw

string text = @"Syncfusion Essential PDF is a.NET PDF library used to create, read, and edit PDF files in any application";

//Create a brush

PdfBrush brush = new PdfSolidBrush(new PdfColor(0, 0, 0));

//Create a pen

PdfPen pen = new PdfPen(new PdfColor(0, 0, 0));

//Get page client size

SizeF clipBounds = page.Graphics.ClientSize;

RectangleF rect = new RectangleF(0, 0, clipBounds.Width, clipBounds.Height);

//Draw the text

page.Graphics.DrawString(text, font, brush, rect);

//Save the PDF document

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the PDF document

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respected code samples

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document

PdfDocument document = new PdfDocument();

//Add a page

PdfPage page = document.Pages.Add();

//Create font

FileStream fontFileStream = new FileStream("Font.otf", FileMode.Open, FileAccess.Read);

PdfFont font = new PdfTrueTypeFont(fontFileStream, 14);

//Text to draw

string text = "Syncfusion Essential PDF is a.NET Core PDF library used to create, read, and edit PDF files in any application";

//Create a brush

PdfBrush brush = new PdfSolidBrush(new PdfColor(0, 0, 0));

//Create a pen

PdfPen pen = new PdfPen(new PdfColor(0, 0, 0));

//Get page client size

SizeF clipBounds = page.Graphics.ClientSize;

RectangleF rect = new RectangleF(0, 0, clipBounds.Width, clipBounds.Height);            

//Draw the text

page.Graphics.DrawString(text, font, brush, rect);

//Save the PDF document

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the PDF document

document.Close(true);

//Defining the content type for PDF file

string contentType = "application/pdf";

//Define the file name

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Create a new PDF document

PdfDocument document = new PdfDocument();

//Add a page

PdfPage page = document.Pages.Add();

//Create font

Stream fontStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Font.otf");

PdfFont font = new PdfTrueTypeFont(fontStream, 14);

//Text to draw

string text = @"Syncfusion Essential PDF is a.NET PDF library used to create, read, and edit PDF files in any application";

//Create a brush

PdfBrush brush = new PdfSolidBrush(new PdfColor(0, 0, 0));

//Create a pen

PdfPen pen = new PdfPen(new PdfColor(0, 0, 0));

//Get page client size

SizeF clipBounds = page.Graphics.ClientSize;

RectangleF rect = new RectangleF(0, 0, clipBounds.Width, clipBounds.Height);

//Draw the text

page.Graphics.DrawString(text, font, brush, rect);

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the PDF document

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

## Drawing text with baseline alignment

The Essential PDF allows you to draw text using a different type of fonts with different sizes with the same baseline alignment in the PDF document by using the EnableBaseline property available in [PdfStringFormat](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfStringFormat.html) class. The following code sample explains this.

{% tabs %}

{% highlight c# %}

//Create a new PDF document

PdfDocument document = new PdfDocument();

//Add a page to the document

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page

PdfGraphics graphics = page.Graphics;

//Create a new PDF font instance

PdfFont font = new PdfTrueTypeFont(new Font("Tahoma",8), 8);

PdfFont font1 = new PdfTrueTypeFont(new Font("Calibri",20), 20);

PdfFont font2 = new PdfStandardFont(PdfFontFamily.Helvetica,16);

PdfFont font3 = new PdfTrueTypeFont(new Font("Arial",25), 25);

//Set the format for string

PdfStringFormat format = new PdfStringFormat();

//Set the line alignment

format.LineAlignment = PdfVerticalAlignment.Bottom;

//Set baseline for the line alignment

format.EnableBaseline = true;

//Draw the text

graphics.DrawString("Hello World!", font, PdfBrushes.Black, new PointF(0, 50), format);

graphics.DrawString("Hello World!", font1, PdfBrushes.Black, new PointF(65, 50), format);

graphics.DrawString("Hello World!", font2, PdfBrushes.Black, new PointF(220, 50), format);

graphics.DrawString("Hello World!", font3, PdfBrushes.Black, new PointF(320, 50), format);

//Save the document
 
document.Save("Output.pdf");

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

'Create a new PDF font instance

Dim font As PdfFont = New PdfTrueTypeFont(new Font("Tahoma",8), 8)

Dim font1 As PdfFont = New PdfTrueTypeFont(new Font("Calibri",20), 20)
   
Dim font2 As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica,16)
     
Dim font3 As PdfFont = New PdfTrueTypeFont(new Font("Arial",25), 25)

'Set the format for string

Dim format As New PdfStringFormat()

'Set the line alignment

format.LineAlignment = PdfVerticalAlignment.Bottom;

'Set baseline for the line alignment

format.EnableBaseline = True

'Draw the text

graphics.DrawString("Hello World!", font, PdfBrushes.Black, New PointF(0, 50), format)

graphics.DrawString("Hello World!", font1, PdfBrushes.Black, New PointF(65, 50), format)

graphics.DrawString("Hello World!", font2, PdfBrushes.Black, New PointF(220, 50), format)

graphics.DrawString("Hello World!", font3, PdfBrushes.Black, New PointF(320, 50), format)

'Save the document 

document.Save("Output.pdf")

'Close the document

document.Close(True)

{% endhighlight %}

{% highlight UWP %}

//Create a new PDF document

PdfDocument doc = new PdfDocument();

//Add a page to the document

PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page

PdfGraphics graphics = page.Graphics;

//Set the font 

Stream fontStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.tahoma.ttf");

Stream fontStream1 = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Arial.ttf");

Stream fontStream2 = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Calibri.ttf");

//Create a new PDF font instance

PdfFont font = new PdfTrueTypeFont(fontStream, 8);

PdfFont font1 = new PdfTrueTypeFont(fontStream1, 20);

PdfFont font2 = new PdfStandardFont(PdfFontFamily.Helvetica,16);

PdfFont font3 = new PdfTrueTypeFont(fontStream2, 25);
           
//Set the format for string

PdfStringFormat format = new PdfStringFormat();

//Set the line alignment

format.LineAlignment = PdfVerticalAlignment.Bottom;

//Set baseline for the line alignment

format.EnableBaseline = true;

//Draw the text

graphics.DrawString("Hello World!", font, PdfBrushes.Black, new PointF(0, 50), format);

graphics.DrawString("Hello World!", font1, PdfBrushes.Black, new PointF(65, 50), format);

graphics.DrawString("Hello World!", font2, PdfBrushes.Black, new PointF(220, 50), format);

graphics.DrawString("Hello World!", font3, PdfBrushes.Black, new PointF(320, 50), format);

//Save the PDF document
         
MemoryStream stream = new MemoryStream();

await doc.SaveAsync(stream);

//Close the PDF document

doc.Close(true);

//Save the stream as PDF document file in the local machine. Refer to the PDF or UWP section for the respected code samples

 Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document

PdfDocument doc = new PdfDocument();

//Add a page to the document

PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page

PdfGraphics graphics = page.Graphics;

FileStream fontStream = new FileStream("tahoma.ttf", FileMode.Open, FileAccess.Read);

FileStream fontStream1 = new FileStream("Arial.ttf", FileMode.Open, FileAccess.Read);

FileStream fontStream2 = new FileStream("Calibri.ttf", FileMode.Open, FileAccess.Read);

//Create a new PDF font instance

PdfFont font = new PdfTrueTypeFont(fontStream, 8);

PdfFont font1 = new PdfTrueTypeFont(fontStream1, 20);

PdfFont font2 = new PdfStandardFont(PdfFontFamily.Helvetica,16);

PdfFont font3 = new PdfTrueTypeFont(fontStream2, 25);
           
//Set the format for string

PdfStringFormat format = new PdfStringFormat();

//Set the line alignment

format.LineAlignment = PdfVerticalAlignment.Bottom;

//Set baseline for the line alignment

format.EnableBaseline = true;

//Draw the text

graphics.DrawString("Hello World!", font, PdfBrushes.Black, new PointF(0, 50), format);

graphics.DrawString("Hello World!", font1, PdfBrushes.Black, new PointF(65, 50), format);

graphics.DrawString("Hello World!", font2, PdfBrushes.Black, new PointF(220, 50), format);

graphics.DrawString("Hello World!", font3, PdfBrushes.Black, new PointF(320, 50), format);

//Save the PDF document
        
MemoryStream stream = new MemoryStream();

doc.Save(stream);

//Close the PDF document

doc.Close(true);

//Defining the content type for PDF file.

string contentType = "application/pdf";

//Define the file name

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Create a new PDF document

PdfDocument doc = new PdfDocument();

//Add a page to the document

PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page

PdfGraphics graphics = page.Graphics;

//Load the font as a stream

Stream fontStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.tahoma.ttf");

Stream fontStream1 = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Arial.ttf");

Stream fontStream2 = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Calibri.ttf");

//Create a new PDF font instance

PdfFont font = new PdfTrueTypeFont(fontStream, 8);

PdfFont font1 = new PdfTrueTypeFont(fontStream1, 20);

PdfFont font2 = new PdfStandardFont(PdfFontFamily.Helvetica,16);

PdfFont font3 = new PdfTrueTypeFont(fontStream2, 25);
           
//Set the format for string

PdfStringFormat format = new PdfStringFormat();

//Set the line alignment

format.LineAlignment = PdfVerticalAlignment.Bottom;

//Set baseline for the line alignment

format.EnableBaseline = true;

//Draw the text

graphics.DrawString("Hello World!", font, PdfBrushes.Black, new PointF(0, 50), format);

graphics.DrawString("Hello World!", font1, PdfBrushes.Black, new PointF(65, 50), format);

graphics.DrawString("Hello World!", font2, PdfBrushes.Black, new PointF(220, 50), format);

graphics.DrawString("Hello World!", font3, PdfBrushes.Black, new PointF(320, 50), format);

//Save the PDF document
           
MemoryStream stream = new MemoryStream();

doc.Save(stream);

//Close the PDF document

doc.Close(true);

//Save the stream into PDF file

//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF or Xamarin section for the respective code samples

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
