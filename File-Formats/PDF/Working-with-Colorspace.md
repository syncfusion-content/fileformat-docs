---
title: Working with Color Spaces | Syncfusion
description: This section explains how to create a PDF document with the specified color space
platform: file-formats
control: PDF
documentation: UG
---
# Working with Color Spaces

Essential PDF allows you to set the color spaces in the following different ways.

* Document Color Space
* Graphics Color Space

## Working with color space in document 


You can set the color space by using [ColorSpace](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfDocument.html#Syncfusion_Pdf_PdfDocument_ColorSpace) property in PDF document.

It supports the following types

* Device color Spaces
* CIE-based Color Spaces
* ICC-based Color Spaces

## Device Color Space


Device color space simply describes the range of colors that a camera can see, a printer can print, or a monitor can display. These color spaces depend upon the device where it is displayed. It contains the following types.

* DeviceGray
* DeviceRGB
* DeviceCMYK

##  CIE-based Color Spaces

CIE-based color space in the PDF document is classified as, 

* CalGray
* CalRGB
* Lab

You can draw a rectangle on new PDF document with **CalGray** brush using [PdfCalGrayColorSpace](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.ColorSpace.PdfCalGrayColorSpace.html) class. The following code snippet explains this.
{% tabs %}
{% highlight c# %}


//Creates a new PDF document.

PdfDocument pdfDocument = new PdfDocument();

//Adds a page to the PDF document

PdfPage pdfPage = pdfDocument.Pages.Add();

//Acquires graphics of the page.

PdfGraphics graphics = pdfPage.Graphics;

//Creates CalGray color space.

PdfCalGrayColorSpace calGrayColorSpace = new PdfCalGrayColorSpace();

//Updates color values.

calGrayColorSpace.Gamma = 0.7;

calGrayColorSpace.WhitePoint = new double[] { 0.2, 1, 0.8 };

PdfCalGrayColor calGrayColorSpace1 = new PdfCalGrayColor(calGrayColorSpace);

calGrayColorSpace1.Gray = 0.1;

PdfBrush brush = new PdfSolidBrush(calGrayColorSpace1);

RectangleF bounds = new RectangleF(0, 0, 300, 300);

//Draws rectangle by using the PdfBrush

graphics.DrawRectangle(brush, bounds);

//Saves the document.

pdfDocument.Save("Output.pdf");

//closes the document

pdfDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}

'Creates a new PDF document.

Dim pdfDocument As New PdfDocument()

'Adds a page to the PDF document

Dim pdfPage As PdfPage = pdfDocument.Pages.Add()

'Acquires graphics of the page.

Dim graphics As PdfGraphics = pdfPage.Graphics

'Creates CalGray color space.

Dim calGrayColorSpace As New PdfCalGrayColorSpace()

'Updates color values.

calGrayColorSpace.Gamma = 0.7

calGrayColorSpace.WhitePoint = New Double() {0.2, 1, 0.8}

Dim calGrayColorSpace1 As New PdfCalGrayColor(calGrayColorSpace)

calGrayColorSpace1.Gray = 0.1

Dim brush As PdfBrush = New PdfSolidBrush(calGrayColorSpace1)

Dim bounds As New RectangleF(0, 0, 300, 300)

'Draws rectangle using the PdfBrush

graphics.DrawRectangle(brush, bounds)

'Saves the document.

pdfDocument.Save("Output.pdf")

'closes the document

pdfDocument.Close(True)



{% endhighlight %}

{% highlight UWP %}

//Creates a new PDF document.

PdfDocument pdfDocument = new PdfDocument();

//Adds a page to the PDF document

PdfPage pdfPage = pdfDocument.Pages.Add();

//Acquires graphics of the page.

PdfGraphics graphics = pdfPage.Graphics;

//Creates CalGray color space.

PdfCalGrayColorSpace calGrayColorSpace = new PdfCalGrayColorSpace();

//Updates color values.

calGrayColorSpace.Gamma = 0.7;

calGrayColorSpace.WhitePoint = new double[] { 0.2, 1, 0.8 };

PdfCalGrayColor calGrayColorSpace1 = new PdfCalGrayColor(calGrayColorSpace);

calGrayColorSpace1.Gray = 0.1;

PdfBrush brush = new PdfSolidBrush(calGrayColorSpace1);

RectangleF bounds = new RectangleF(0, 0, 300, 300);

//Draws rectangle by using the PdfBrush

graphics.DrawRectangle(brush, bounds);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await pdfDocument.SaveAsync(stream);

//Close the document

pdfDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Creates a new PDF document.

PdfDocument pdfDocument = new PdfDocument();

//Adds a page to the PDF document

PdfPage pdfPage = pdfDocument.Pages.Add();

//Acquires graphics of the page.

PdfGraphics graphics = pdfPage.Graphics;

//Creates CalGray color space.

PdfCalGrayColorSpace calGrayColorSpace = new PdfCalGrayColorSpace();

//Updates color values.

calGrayColorSpace.Gamma = 0.7;

calGrayColorSpace.WhitePoint = new double[] { 0.2, 1, 0.8 };

PdfCalGrayColor calGrayColorSpace1 = new PdfCalGrayColor(calGrayColorSpace);

calGrayColorSpace1.Gray = 0.1;

PdfBrush brush = new PdfSolidBrush(calGrayColorSpace1);

RectangleF bounds = new RectangleF(0, 0, 300, 300);

//Draws rectangle by using the PdfBrush

graphics.DrawRectangle(brush, bounds);

//Save the document into stream

MemoryStream stream = new MemoryStream();

pdfDocument.Save(stream);

stream.Position = 0;

//Closes the document

pdfDocument.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Creates a new PDF document.

PdfDocument pdfDocument = new PdfDocument();

//Adds a page to the PDF document

PdfPage pdfPage = pdfDocument.Pages.Add();

//Acquires graphics of the page.

PdfGraphics graphics = pdfPage.Graphics;

//Creates CalGray color space.

PdfCalGrayColorSpace calGrayColorSpace = new PdfCalGrayColorSpace();

//Updates color values.

calGrayColorSpace.Gamma = 0.7;

calGrayColorSpace.WhitePoint = new double[] { 0.2, 1, 0.8 };

PdfCalGrayColor calGrayColorSpace1 = new PdfCalGrayColor(calGrayColorSpace);

calGrayColorSpace1.Gray = 0.1;

PdfBrush brush = new PdfSolidBrush(calGrayColorSpace1);

RectangleF bounds = new RectangleF(0, 0, 300, 300);

//Draws rectangle by using the PdfBrush

graphics.DrawRectangle(brush, bounds);

//Save the document into stream.

MemoryStream stream = new MemoryStream();

pdfDocument.Save(stream);

//Close the document.

pdfDocument.Close(true);

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

The following code example illustrates how to draw a rectangle with **CalGray** brush in existing PDF document.
{% tabs %}
{% highlight c# %}


//Loads the existing PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);

//Loads the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Acquires graphics of the page.

PdfGraphics graphics = loadedPage.Graphics;

//Creates CalGray color space.

PdfCalGrayColorSpace calGrayColorSpace = new PdfCalGrayColorSpace();

//Updates color values.

calGrayColorSpace.Gamma = 0.7;

calGrayColorSpace.WhitePoint = new double[] { 0.2, 1, 0.8 };

PdfCalGrayColor calGrayColorSpace1 = new PdfCalGrayColor(calGrayColorSpace);

calGrayColorSpace1.Gray = 0.1;

PdfBrush brush = new PdfSolidBrush(calGrayColorSpace1);

RectangleF bounds = new RectangleF(0, 0, 300, 300);

//Draws rectangle by using the PdfBrush

graphics.DrawRectangle(brush, bounds);

//Saves the modified document.

loadedDocument.Save("Output.pdf");

//Closes the document

loadedDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Loads the existing PDF document.

Dim loadedDocument As New PdfLoadedDocument(fileName)

'Loads the page

Dim loadedPage As PdfLoadedPage = TryCast(loadedDocument.Pages(0), PdfLoadedPage)

'Acquires graphics of the page.

Dim graphics As PdfGraphics = loadedPage.Graphics

'Creates CalGray color space.

Dim calGrayColorSpace As New PdfCalGrayColorSpace()

'Updates color values.

calGrayColorSpace.Gamma = 0.7

calGrayColorSpace.WhitePoint = New Double() {0.2, 1, 0.8}

Dim calGrayColorSpace1 As New PdfCalGrayColor(calGrayColorSpace)

calGrayColorSpace1.Gray = 0.1

Dim brush As PdfBrush = New PdfSolidBrush(calGrayColorSpace1)

Dim bounds As New RectangleF(0, 0, 300, 300)

'Draws rectangle by using the PdfBrush

graphics.DrawRectangle(brush, bounds)

'Saves the modified document.

loadedDocument.Save("Output.pdf")

'closes the document

loadedDocument.Close(True)





{% endhighlight %}

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

//Loads the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Acquires graphics of the page.

PdfGraphics graphics = loadedPage.Graphics;

//Creates CalGray color space.

PdfCalGrayColorSpace calGrayColorSpace = new PdfCalGrayColorSpace();

//Updates color values.

calGrayColorSpace.Gamma = 0.7;

calGrayColorSpace.WhitePoint = new double[] { 0.2, 1, 0.8 };

PdfCalGrayColor calGrayColorSpace1 = new PdfCalGrayColor(calGrayColorSpace);

calGrayColorSpace1.Gray = 0.1;

PdfBrush brush = new PdfSolidBrush(calGrayColorSpace1);

RectangleF bounds = new RectangleF(0, 0, 300, 300);

//Draws rectangle by using the PdfBrush

graphics.DrawRectangle(brush, bounds);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await loadedDocument.SaveAsync(stream);

//Close the document

loadedDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Loads the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Acquires graphics of the page.

PdfGraphics graphics = loadedPage.Graphics;

//Creates CalGray color space.

PdfCalGrayColorSpace calGrayColorSpace = new PdfCalGrayColorSpace();

//Updates color values.

calGrayColorSpace.Gamma = 0.7;

calGrayColorSpace.WhitePoint = new double[] { 0.2, 1, 0.8 };

PdfCalGrayColor calGrayColorSpace1 = new PdfCalGrayColor(calGrayColorSpace);

calGrayColorSpace1.Gray = 0.1;

PdfBrush brush = new PdfSolidBrush(calGrayColorSpace1);

RectangleF bounds = new RectangleF(0, 0, 300, 300);

//Draws rectangle by using the PdfBrush

graphics.DrawRectangle(brush, bounds);

//Save the document into stream

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

stream.Position = 0;

//Closes the document

loadedDocument.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Loads the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Acquires graphics of the page.

PdfGraphics graphics = loadedPage.Graphics;

//Creates CalGray color space.

PdfCalGrayColorSpace calGrayColorSpace = new PdfCalGrayColorSpace();

//Updates color values.

calGrayColorSpace.Gamma = 0.7;

calGrayColorSpace.WhitePoint = new double[] { 0.2, 1, 0.8 };

PdfCalGrayColor calGrayColorSpace1 = new PdfCalGrayColor(calGrayColorSpace);

calGrayColorSpace1.Gray = 0.1;

PdfBrush brush = new PdfSolidBrush(calGrayColorSpace1);

RectangleF bounds = new RectangleF(0, 0, 300, 300);

//Draws rectangle by using the PdfBrush

graphics.DrawRectangle(brush, bounds);

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

## ICC-based Color Spaces

To create color for brush/pen to render shape or text in the PDF document, you can use ICC based color spaces.

It contains the following types:

* Special color spaces –Pantone colors
* Indexed
* Separation

The following code example illustrates how to set the indexed ICC color space using [PdfCalRGBColorSpace](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.ColorSpace.PdfCalRGBColorSpace.html) class in new PDF document.

{% tabs %}
{% highlight c# %}


//Creates a new PDF document.

PdfDocument pdfDocument = new PdfDocument();

//Adds a page to the PDF document.

PdfPage pdfPage = pdfDocument.Pages.Add();

//Acquires graphics of the page.

PdfGraphics graphics = pdfPage.Graphics;

//Creates ICCBased color space.

PdfCalRGBColorSpace calRgbCS = new PdfCalRGBColorSpace();

calRgbCS.Gamma = new double[] { 7.6, 5.1, 8.5 };

calRgbCS.Matrix = new double[] { 1, 0, 0, 0, 1, 0, 0, 0, 1 };

calRgbCS.WhitePoint = new double[] { 0.7, 1, 0.8 };

//Reads the ICC profile.

FileStream fileStream = new FileStream(@"input.icc", FileMode.Open, FileAccess.Read);

byte[] profileData = new byte[fileStream.Length];

fileStream.Read(profileData, 0, profileData.Length);

fileStream.Close();

//Instantiates ICC color space.

PdfICCColorSpace iccBasedCS = new PdfICCColorSpace();

iccBasedCS.ProfileData = profileData;

iccBasedCS.AlternateColorSpace = calRgbCS;

iccBasedCS.ColorComponents = 3;

iccBasedCS.Range = new double[] { 0.0, 1.0, 0.0, 1.0, 0.0, 1.0 };

PdfICCColor red = new PdfICCColor(iccBasedCS);

red.ColorComponents = new double[] { 1, 0, 1 };

PdfBrush brush = new PdfSolidBrush(red);

RectangleF bounds = new RectangleF(0, 0, 300, 300);

//Draws rectangle by using the PdfBrush.

graphics.DrawRectangle(brush, bounds);

//Saves the document.

pdfDocument.Save("Output.pdf");

//Closes the document

pdfDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}

'Creates a new PDF document.

Dim pdfDocument As New PdfDocument()

'Adds a page to the PDF document.

Dim pdfPage As PdfPage = pdfDocument.Pages.Add()

'Acquires graphics of the page.

Dim graphics As PdfGraphics = pdfPage.Graphics

'Creates ICCBased color space.

Dim calRgbCS As New PdfCalRGBColorSpace()

calRgbCS.Gamma = New Double() {7.6, 5.1, 8.5}

calRgbCS.Matrix = New Double() {1, 0, 0, 0, 1, 0, 0, 0, 1}

calRgbCS.WhitePoint = New Double() {0.7, 1, 0.8}

'Reads the ICC profile.

Dim fileStream As New FileStream("input.icc", FileMode.Open, FileAccess.Read)

Dim profileData(fileStream.Length - 1) As Byte

fileStream.Read(profileData, 0, profileData.Length)

fileStream.Close()

'Instantiates ICC color space.

Dim iccBasedCS As New PdfICCColorSpace()

iccBasedCS.ProfileData = profileData

iccBasedCS.AlternateColorSpace = calRgbCS

iccBasedCS.ColorComponents = 3

iccBasedCS.Range = New Double() {0.0, 1.0, 0.0, 1.0, 0.0, 1.0}

Dim red As New PdfICCColor(iccBasedCS)

red.ColorComponents = New Double() {1, 0, 1}

Dim brush As PdfBrush = New PdfSolidBrush(red)

Dim bounds As New RectangleF(0, 0, 300, 300)

'Draws rectangle by using the PdfBrush.

graphics.DrawRectangle(brush, bounds)

'Saves the document.

pdfDocument.Save("Output.pdf")

'Closes the document

pdfDocument.Close(True)



{% endhighlight %}

{% highlight UWP %}

//Creates a new PDF document.

PdfDocument pdfDocument = new PdfDocument();

//Adds a page to the PDF document.

PdfPage pdfPage = pdfDocument.Pages.Add();

//Acquires graphics of the page.

PdfGraphics graphics = pdfPage.Graphics;

//Creates ICCBased color space.

PdfCalRGBColorSpace calRgbCS = new PdfCalRGBColorSpace();

calRgbCS.Gamma = new double[] { 7.6, 5.1, 8.5 };

calRgbCS.Matrix = new double[] { 1, 0, 0, 0, 1, 0, 0, 0, 1 };

calRgbCS.WhitePoint = new double[] { 0.7, 1, 0.8 };

//Reads the ICC profile.

Stream fileStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.input.icc");

byte[] profileData = new byte[fileStream.Length];

fileStream.Read(profileData, 0, profileData.Length);

fileStream.Dispose();

//Instantiates ICC color space.

PdfICCColorSpace iccBasedCS = new PdfICCColorSpace();

iccBasedCS.ProfileData = profileData;

iccBasedCS.AlternateColorSpace = calRgbCS;

iccBasedCS.ColorComponents = 3;

iccBasedCS.Range = new double[] { 0.0, 1.0, 0.0, 1.0, 0.0, 1.0 };

PdfICCColor red = new PdfICCColor(iccBasedCS);

red.ColorComponents = new double[] { 1, 0, 1 };

PdfBrush brush = new PdfSolidBrush(red);

RectangleF bounds = new RectangleF(0, 0, 300, 300);

//Draws rectangle by using the PdfBrush.

graphics.DrawRectangle(brush, bounds);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await pdfDocument.SaveAsync(stream);

//Close the document

pdfDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Creates a new PDF document.

PdfDocument pdfDocument = new PdfDocument();

//Adds a page to the PDF document.

PdfPage pdfPage = pdfDocument.Pages.Add();

//Acquires graphics of the page.

PdfGraphics graphics = pdfPage.Graphics;

//Creates ICCBased color space.

PdfCalRGBColorSpace calRgbCS = new PdfCalRGBColorSpace();

calRgbCS.Gamma = new double[] { 7.6, 5.1, 8.5 };

calRgbCS.Matrix = new double[] { 1, 0, 0, 0, 1, 0, 0, 0, 1 };

calRgbCS.WhitePoint = new double[] { 0.7, 1, 0.8 };

//Reads the ICC profile.

FileStream fileStream = new FileStream(@"input.icc", FileMode.Open, FileAccess.Read);

byte[] profileData = new byte[fileStream.Length];

fileStream.Read(profileData, 0, profileData.Length);

fileStream.Close();

//Instantiates ICC color space.

PdfICCColorSpace iccBasedCS = new PdfICCColorSpace();

iccBasedCS.ProfileData = profileData;

iccBasedCS.AlternateColorSpace = calRgbCS;

iccBasedCS.ColorComponents = 3;

iccBasedCS.Range = new double[] { 0.0, 1.0, 0.0, 1.0, 0.0, 1.0 };

PdfICCColor red = new PdfICCColor(iccBasedCS);

red.ColorComponents = new double[] { 1, 0, 1 };

PdfBrush brush = new PdfSolidBrush(red);

RectangleF bounds = new RectangleF(0, 0, 300, 300);

//Draws rectangle by using the PdfBrush.

graphics.DrawRectangle(brush, bounds);

//Save the document into stream

MemoryStream stream = new MemoryStream();

pdfDocument.Save(stream);

stream.Position = 0;

//Closes the document

pdfDocument.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Creates a new PDF document.

PdfDocument pdfDocument = new PdfDocument();

//Adds a page to the PDF document.

PdfPage pdfPage = pdfDocument.Pages.Add();

//Acquires graphics of the page.

PdfGraphics graphics = pdfPage.Graphics;

//Creates ICCBased color space.

PdfCalRGBColorSpace calRgbCS = new PdfCalRGBColorSpace();

calRgbCS.Gamma = new double[] { 7.6, 5.1, 8.5 };

calRgbCS.Matrix = new double[] { 1, 0, 0, 0, 1, 0, 0, 0, 1 };

calRgbCS.WhitePoint = new double[] { 0.7, 1, 0.8 };

//Reads the ICC profile.

Stream fileStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.icc");

byte[] profileData = new byte[fileStream.Length];

fileStream.Read(profileData, 0, profileData.Length);

fileStream.Close();

//Instantiates ICC color space.

PdfICCColorSpace iccBasedCS = new PdfICCColorSpace();

iccBasedCS.ProfileData = profileData;

iccBasedCS.AlternateColorSpace = calRgbCS;

iccBasedCS.ColorComponents = 3;

iccBasedCS.Range = new double[] { 0.0, 1.0, 0.0, 1.0, 0.0, 1.0 };

PdfICCColor red = new PdfICCColor(iccBasedCS);

red.ColorComponents = new double[] { 1, 0, 1 };

PdfBrush brush = new PdfSolidBrush(red);

RectangleF bounds = new RectangleF(0, 0, 300, 300);

//Draws rectangle by using the PdfBrush.

graphics.DrawRectangle(brush, bounds);

//Save the document into stream.

MemoryStream stream = new MemoryStream();

pdfDocument.Save(stream);

//Close the document.

pdfDocument.Close(true);

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

The following code example illustrates how to set the indexed ICC color space in existing PDF document.

{% tabs %}
{% highlight c# %}


//Loads the existing PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);

//Loads the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Acquires graphics of the page.

PdfGraphics graphics = loadedPage.Graphics;

//Creates ICCBased color space.

PdfCalRGBColorSpace calRgbCS = new PdfCalRGBColorSpace();

calRgbCS.Gamma = new double[] { 7.6, 5.1, 8.5 };

calRgbCS.Matrix = new double[] { 1, 0, 0, 0, 1, 0, 0, 0, 1 };

calRgbCS.WhitePoint = new double[] { 0.7, 1, 0.8 };

//Reads the ICC profile.

FileStream fileStream = new FileStream(@"input.icc", FileMode.Open, FileAccess.Read);

byte[] profileData = new byte[fileStream.Length];

fileStream.Read(profileData, 0, profileData.Length);

fileStream.Close();

//Instantiates ICC color space.

PdfICCColorSpace iccBasedCS = new PdfICCColorSpace();

iccBasedCS.ProfileData = profileData;

iccBasedCS.AlternateColorSpace = calRgbCS;

iccBasedCS.ColorComponents = 3;

iccBasedCS.Range = new double[] { 0.0, 1.0, 0.0, 1.0, 0.0, 1.0 };

PdfICCColor red = new PdfICCColor(iccBasedCS);

red.ColorComponents = new double[] { 1, 0, 1 };

PdfBrush brush = new PdfSolidBrush(red);

RectangleF bounds = new RectangleF(0, 0, 300, 300);

//Draws rectangle by using the PdfBrush.

graphics.DrawRectangle(brush, bounds);

//Saves the document.

loadedDocument.Save("Output.pdf");

//Closes the document

loadedDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Loads the existing PDF document.

Dim loadedDocument As New PdfLoadedDocument(fileName)

'Loads the page

Dim loadedPage As PdfLoadedPage = TryCast(loadedDocument.Pages(0), PdfLoadedPage)

'Acquires graphics of the page.

Dim graphics As PdfGraphics = loadedPage.Graphics

'Creates CalGray color space.

Dim calGrayColorSpace As New PdfCalGrayColorSpace()

'Updates color values.

calGrayColorSpace.Gamma = 0.7

calGrayColorSpace.WhitePoint = New Double() {0.2, 1, 0.8}

Dim calGrayColorSpace1 As New PdfCalGrayColor(calGrayColorSpace)

calGrayColorSpace1.Gray = 0.1

Dim brush As PdfBrush = New PdfSolidBrush(calGrayColorSpace1)

Dim bounds As New RectangleF(0, 0, 300, 300)

'Draws rectangle by using the PdfBrush

graphics.DrawRectangle(brush, bounds)

'Saves the document.

loadedDocument.Save("Output.pdf")

'Closes the document

loadedDocument.Close(True)





{% endhighlight %}

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

//Loads the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Acquires graphics of the page.

PdfGraphics graphics = loadedPage.Graphics;

//Creates ICCBased color space.

PdfCalRGBColorSpace calRgbCS = new PdfCalRGBColorSpace();

calRgbCS.Gamma = new double[] { 7.6, 5.1, 8.5 };

calRgbCS.Matrix = new double[] { 1, 0, 0, 0, 1, 0, 0, 0, 1 };

calRgbCS.WhitePoint = new double[] { 0.7, 1, 0.8 };

//Reads the ICC profile.

Stream fileStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.input.icc");

byte[] profileData = new byte[fileStream.Length];

fileStream.Read(profileData, 0, profileData.Length);

fileStream.Dispose();

//Instantiates ICC color space.

PdfICCColorSpace iccBasedCS = new PdfICCColorSpace();

iccBasedCS.ProfileData = profileData;

iccBasedCS.AlternateColorSpace = calRgbCS;

iccBasedCS.ColorComponents = 3;

iccBasedCS.Range = new double[] { 0.0, 1.0, 0.0, 1.0, 0.0, 1.0 };

PdfICCColor red = new PdfICCColor(iccBasedCS);

red.ColorComponents = new double[] { 1, 0, 1 };

PdfBrush brush = new PdfSolidBrush(red);

RectangleF bounds = new RectangleF(0, 0, 300, 300);

//Draws rectangle by using the PdfBrush.

graphics.DrawRectangle(brush, bounds);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await loadedDocument.SaveAsync(stream);

//Close the document

loadedDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Loads the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Acquires graphics of the page.

PdfGraphics graphics = loadedPage.Graphics;

//Creates ICCBased color space.

PdfCalRGBColorSpace calRgbCS = new PdfCalRGBColorSpace();

calRgbCS.Gamma = new double[] { 7.6, 5.1, 8.5 };

calRgbCS.Matrix = new double[] { 1, 0, 0, 0, 1, 0, 0, 0, 1 };

calRgbCS.WhitePoint = new double[] { 0.7, 1, 0.8 };

//Reads the ICC profile.

FileStream fileStream = new FileStream(@"input.icc", FileMode.Open, FileAccess.Read);

byte[] profileData = new byte[fileStream.Length];

fileStream.Read(profileData, 0, profileData.Length);

fileStream.Close();

//Instantiates ICC color space.

PdfICCColorSpace iccBasedCS = new PdfICCColorSpace();

iccBasedCS.ProfileData = profileData;

iccBasedCS.AlternateColorSpace = calRgbCS;

iccBasedCS.ColorComponents = 3;

iccBasedCS.Range = new double[] { 0.0, 1.0, 0.0, 1.0, 0.0, 1.0 };

PdfICCColor red = new PdfICCColor(iccBasedCS);

red.ColorComponents = new double[] { 1, 0, 1 };

PdfBrush brush = new PdfSolidBrush(red);

RectangleF bounds = new RectangleF(0, 0, 300, 300);

//Draws rectangle by using the PdfBrush.

graphics.DrawRectangle(brush, bounds);

//Save the document into stream

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

stream.Position = 0;

//Closes the document

loadedDocument.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Signature.Assets.Barcode.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Loads the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Acquires graphics of the page.

PdfGraphics graphics = loadedPage.Graphics;

//Creates ICCBased color space.

PdfCalRGBColorSpace calRgbCS = new PdfCalRGBColorSpace();

calRgbCS.Gamma = new double[] { 7.6, 5.1, 8.5 };

calRgbCS.Matrix = new double[] { 1, 0, 0, 0, 1, 0, 0, 0, 1 };

calRgbCS.WhitePoint = new double[] { 0.7, 1, 0.8 };

//Reads the ICC profile.

Stream fileStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Signature.Assets.rgb.icc");

byte[] profileData = new byte[fileStream.Length];

fileStream.Read(profileData, 0, profileData.Length);

fileStream.Close();

//Instantiates ICC color space.

PdfICCColorSpace iccBasedCS = new PdfICCColorSpace();

iccBasedCS.ProfileData = profileData;

iccBasedCS.AlternateColorSpace = calRgbCS;

iccBasedCS.ColorComponents = 3;

iccBasedCS.Range = new double[] { 0.0, 1.0, 0.0, 1.0, 0.0, 1.0 };

PdfICCColor red = new PdfICCColor(iccBasedCS);

red.ColorComponents = new double[] { 1, 0, 1 };

PdfBrush brush = new PdfSolidBrush(red);

RectangleF bounds = new RectangleF(0, 0, 300, 300);

//Draws rectangle by using the PdfBrush.

graphics.DrawRectangle(brush, bounds);

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

## Pantone colors

The following code example illustrates how to draw the graphics elements by using Pantone colors through [PdfSeparationColorSpace](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.ColorSpace.PdfSeparationColorSpace.html) class in new PDF document.

{% tabs %}
{% highlight c# %}
          

// Creates a new document

PdfDocument document = new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

// Creates exponential interpolation function

PdfExponentialInterpolationFunction function = new PdfExponentialInterpolationFunction(true);

float[] numberArray = new float[4];

numberArray[0] = 0.38f;

numberArray[1] = 0.88f;

function.C1 = numberArray;

// Creates SeparationColorSpace

PdfSeparationColorSpace colorSpace = new PdfSeparationColorSpace();

colorSpace.TintTransform = function;

colorSpace.Colorant = "PANTONE Orange 021 C";

PdfSeparationColor color = new PdfSeparationColor(colorSpace);

color.Tint = 0.7;

RectangleF bounds = new RectangleF(20, 70, 200, 100);

PdfPen pen = new PdfPen(color);

//Draws the rectangle

page.Graphics.DrawRectangle(pen, bounds);

//Saves the document

document.Save("SeparationColor.pdf");

//Closes the document

document.Close(true);





{% endhighlight %}

{% highlight vb.net %}

' Creates a new document

Dim document As PdfDocument = New PdfDocument()

' Creates a page

Dim page As PdfPage = document.Pages.Add()

' Creates exponential interpolation function 

Dim [function] As PdfExponentialInterpolationFunction = New PdfExponentialInterpolationFunction(True)

Dim numberArray() As Single = New Single(4) {}

numberArray(0) = 0.38F

numberArray(1) = 0.88F

[function].C1 = numberArray

' Creates SeparationColorSpace

Dim colorSpace As PdfSeparationColorSpace = New PdfSeparationColorSpace()

colorSpace.TintTransform = [function]

colorSpace.Colorant = "PANTONE Orange 021 C"

Dim color As PdfSeparationColor = New PdfSeparationColor(colorSpace)

color.Tint = 0.7

Dim bounds As RectangleF = New RectangleF(20, 70, 200, 100)

Dim pen As PdfPen = New PdfPen(color)

'Draws the rectangle

page.Graphics.DrawRectangle(pen, bounds)

'Saves the document

document.Save("SeparationColor.pdf")

'Closes the document

document.Close(True)



{% endhighlight %}

{% highlight UWP %}

// Creates a new document

PdfDocument document = new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

// Creates exponential interpolation function

PdfExponentialInterpolationFunction function = new PdfExponentialInterpolationFunction(true);

float[] numberArray = new float[4];

numberArray[0] = 0.38f;

numberArray[1] = 0.88f;

function.C1 = numberArray;

// Creates SeparationColorSpace

PdfSeparationColorSpace colorSpace = new PdfSeparationColorSpace();

colorSpace.TintTransform = function;

colorSpace.Colorant = "PANTONE Orange 021 C";

PdfSeparationColor color = new PdfSeparationColor(colorSpace);

color.Tint = 0.7;

RectangleF bounds = new RectangleF(20, 70, 200, 100);

PdfPen pen = new PdfPen(color);

//Draws the rectangle

page.Graphics.DrawRectangle(pen, bounds);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "SeparationColor.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

// Creates a new document

PdfDocument document = new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

// Creates exponential interpolation function

PdfExponentialInterpolationFunction function = new PdfExponentialInterpolationFunction(true);

float[] numberArray = new float[4];

numberArray[0] = 0.38f;

numberArray[1] = 0.88f;

function.C1 = numberArray;

// Creates SeparationColorSpace

PdfSeparationColorSpace colorSpace = new PdfSeparationColorSpace();

colorSpace.TintTransform = function;

colorSpace.Colorant = "PANTONE Orange 021 C";

PdfSeparationColor color = new PdfSeparationColor(colorSpace);

color.Tint = 0.7;

RectangleF bounds = new RectangleF(20, 70, 200, 100);

PdfPen pen = new PdfPen(color);

//Draws the rectangle

page.Graphics.DrawRectangle(pen, bounds);

//Save the document into stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

stream.Position = 0;

//Closes the document

document.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "SeparationColor.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

// Creates a new document

PdfDocument document = new PdfDocument();

//Creates a new page

PdfPage page = document.Pages.Add();

// Creates exponential interpolation function

PdfExponentialInterpolationFunction function = new PdfExponentialInterpolationFunction(true);

float[] numberArray = new float[4];

numberArray[0] = 0.38f;

numberArray[1] = 0.88f;

function.C1 = numberArray;

// Creates SeparationColorSpace

PdfSeparationColorSpace colorSpace = new PdfSeparationColorSpace();

colorSpace.TintTransform = function;

colorSpace.Colorant = "PANTONE Orange 021 C";

PdfSeparationColor color = new PdfSeparationColor(colorSpace);

color.Tint = 0.7;

RectangleF bounds = new RectangleF(20, 70, 200, 100);

PdfPen pen = new PdfPen(color);

//Draws the rectangle

page.Graphics.DrawRectangle(pen, bounds);

//Save the document into stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document.

document.Close(true);

//Save the stream into pdf file
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("SeparationColor.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("SeparationColor.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

The following code example illustrates how to draw the graphics elements by using Pantone colors in existing PDF document.

{% tabs %}
{% highlight c# %}


//Loads the document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

// Creates exponential interpolation function 

PdfExponentialInterpolationFunction function = new PdfExponentialInterpolationFunction(true);

float[] numberArray = new float[4];

numberArray[0] = 0.38f;

numberArray[1] = 0.88f;

function.C1 = numberArray;

// Creates SeparationColorSpace

PdfSeparationColorSpace colorSpace = new PdfSeparationColorSpace();

colorSpace.TintTransform = function;

colorSpace.Colorant = "PANTONE Orange 021 C";

PdfSeparationColor color = new PdfSeparationColor(colorSpace);

color.Tint = 0.7;

RectangleF bounds = new RectangleF(20, 70, 200, 100);

PdfPen pen = new PdfPen(color);

//Draws the rectangle

loadedPage.Graphics.DrawRectangle(pen, bounds);

//Saves the document

loadedDocument.Save("SeparationColor.pdf");

//Closes the document

loadedDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Loads the document.

Dim loadedDocument As New PdfLoadedDocument(fileName)

Dim loadedPage As PdfLoadedPage = TryCast(loadedDocument.Pages(0), PdfLoadedPage)

' Creates exponential interpolation function

Dim [function] As PdfExponentialInterpolationFunction = New PdfExponentialInterpolationFunction(True)

Dim numberArray() As Single = New Single(3) {}

numberArray(0) = 0.38F

numberArray(1) = 0.88F

[function].C1 = numberArray

' Creates SeparationColorSpace

Dim colorSpace As PdfSeparationColorSpace = New PdfSeparationColorSpace()

colorSpace.TintTransform = [function]

colorSpace.Colorant = "PANTONE Orange 021 C"

Dim color As PdfSeparationColor = New PdfSeparationColor(colorSpace)

color.Tint = 0.7

Dim bounds As RectangleF = New RectangleF(20, 70, 200, 100)

Dim pen As PdfPen = New PdfPen(color)

'Draws the rectangle

loadedPage.Graphics.DrawRectangle(pen, bounds)

'Saves the document

loadedDocument.Save("SeparationColor.pdf")

'Closes the document

loadedDocument.Close(True)



{% endhighlight %}

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

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

// Creates exponential interpolation function 

PdfExponentialInterpolationFunction function = new PdfExponentialInterpolationFunction(true);

float[] numberArray = new float[4];

numberArray[0] = 0.38f;

numberArray[1] = 0.88f;

function.C1 = numberArray;

// Creates SeparationColorSpace

PdfSeparationColorSpace colorSpace = new PdfSeparationColorSpace();

colorSpace.TintTransform = function;

colorSpace.Colorant = "PANTONE Orange 021 C";

PdfSeparationColor color = new PdfSeparationColor(colorSpace);

color.Tint = 0.7;

RectangleF bounds = new RectangleF(20, 70, 200, 100);

PdfPen pen = new PdfPen(color);

//Draws the rectangle

loadedPage.Graphics.DrawRectangle(pen, bounds);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await loadedDocument.SaveAsync(stream);

//Close the document

loadedDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "SeparationColor.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

// Creates exponential interpolation function 

PdfExponentialInterpolationFunction function = new PdfExponentialInterpolationFunction(true);

float[] numberArray = new float[4];

numberArray[0] = 0.38f;

numberArray[1] = 0.88f;

function.C1 = numberArray;

// Creates SeparationColorSpace

PdfSeparationColorSpace colorSpace = new PdfSeparationColorSpace();

colorSpace.TintTransform = function;

colorSpace.Colorant = "PANTONE Orange 021 C";

PdfSeparationColor color = new PdfSeparationColor(colorSpace);

color.Tint = 0.7;

RectangleF bounds = new RectangleF(20, 70, 200, 100);

PdfPen pen = new PdfPen(color);

//Draws the rectangle

loadedPage.Graphics.DrawRectangle(pen, bounds);

//Save the document into stream

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

stream.Position = 0;

//Closes the document

loadedDocument.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "SeparationColor.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

// Creates exponential interpolation function 

PdfExponentialInterpolationFunction function = new PdfExponentialInterpolationFunction(true);

float[] numberArray = new float[4];

numberArray[0] = 0.38f;

numberArray[1] = 0.88f;

function.C1 = numberArray;

// Creates SeparationColorSpace

PdfSeparationColorSpace colorSpace = new PdfSeparationColorSpace();

colorSpace.TintTransform = function;

colorSpace.Colorant = "PANTONE Orange 021 C";

PdfSeparationColor color = new PdfSeparationColor(colorSpace);

color.Tint = 0.7;

RectangleF bounds = new RectangleF(20, 70, 200, 100);

PdfPen pen = new PdfPen(color);

//Draws the rectangle

loadedPage.Graphics.DrawRectangle(pen, bounds);

//Save the document into stream.

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Close the document.

loadedDocument.Close(true);

//Save the stream into pdf file
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("SeparationColor.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("SeparationColor.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

## Working with color space in graphics

You can set the color spaces to the particular object in the PDF document by using the [ColorSpace](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfGraphics.html#Syncfusion_Pdf_Graphics_PdfGraphics_ColorSpace) property in [PdfGraphics](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfGraphics.html) class.

The following code illustrates how to use the color spaces in particular objects in new PDF document.
{% tabs %}
{% highlight c# %}

//Creates a new PDF document.

PdfDocument pdfDocument = new PdfDocument();

//Adds a page to the PDF document.

PdfPage pdfPage = pdfDocument.Pages.Add();

//Acquires graphics of the page.

PdfGraphics graphics = pdfPage.Graphics;

PdfPen pen = new PdfPen(Color.Red);

PdfBrush brush = new PdfSolidBrush(Color.Blue);

RectangleF rectangle = new RectangleF(0, 0, 100, 100);

//Default color space.

graphics.DrawRectangle(pen, brush, rectangle);

graphics.Save();

//GrayScale color space.

graphics.ColorSpace = PdfColorSpace.GrayScale;

graphics.DrawRectangle(pen, brush, rectangle);

//CMYK color space.

graphics.ColorSpace = PdfColorSpace.CMYK;

graphics.DrawRectangle(pen, brush, rectangle);

graphics.Restore();

//Default color space.

graphics.DrawRectangle(pen, brush, rectangle);

//Draws by using the PdfBrush.

graphics.DrawRectangle(brush, rectangle);

//Saves the document.

pdfDocument.Save("Output.pdf");

//Closes the document

pdfDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}

'Creates a new PDF document.

Dim pdfDocument As New PdfDocument()

'Adds a page to the PDF document.

Dim pdfPage As PdfPage = pdfDocument.Pages.Add()

'Acquires graphics of the page.

Dim graphics As PdfGraphics = pdfPage.Graphics

Dim pen As New PdfPen(Color.Red)

Dim brush As PdfBrush = New PdfSolidBrush(Color.Blue)

Dim rectangle As New RectangleF(0, 0, 100, 100)

'Default color space.

graphics.DrawRectangle(pen, brush, rectangle)

graphics.Save()

'GrayScale color space.

graphics.ColorSpace = PdfColorSpace.GrayScale

graphics.DrawRectangle(pen, brush, rectangle)

'CMYK color space.

graphics.ColorSpace = PdfColorSpace.CMYK

graphics.DrawRectangle(pen, brush, rectangle)

graphics.Restore()

'Default color space.

graphics.DrawRectangle(pen, brush, rectangle)

'Draws by using the PdfBrush.

graphics.DrawRectangle(brush, rectangle)

'Saves the document.

pdfDocument.Save("Output.pdf")

'Closes the document

pdfDocument.Close(True)



{% endhighlight %}

{% highlight UWP %}

//Creates a new PDF document.

PdfDocument pdfDocument = new PdfDocument();

//Adds a page to the PDF document.

PdfPage pdfPage = pdfDocument.Pages.Add();

//Acquires graphics of the page.

PdfGraphics graphics = pdfPage.Graphics;

PdfPen pen = new PdfPen(new PdfColor(255,0,0));

PdfBrush brush = new PdfSolidBrush(new PdfColor(0,0,255));

RectangleF rectangle = new RectangleF(0, 0, 100, 100);

//Default color space.

graphics.DrawRectangle(pen, brush, rectangle);

graphics.Save();

//GrayScale color space.

graphics.ColorSpace = PdfColorSpace.GrayScale;

graphics.DrawRectangle(pen, brush, rectangle);

//CMYK color space.

graphics.ColorSpace = PdfColorSpace.CMYK;

graphics.DrawRectangle(pen, brush, rectangle);

graphics.Restore();

//Default color space.

graphics.DrawRectangle(pen, brush, rectangle);

//Draws by using the PdfBrush.

graphics.DrawRectangle(brush, rectangle);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await pdfDocument.SaveAsync(stream);

//Close the document

pdfDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Creates a new PDF document.

PdfDocument pdfDocument = new PdfDocument();

//Adds a page to the PDF document.

PdfPage pdfPage = pdfDocument.Pages.Add();

//Acquires graphics of the page.

PdfGraphics graphics = pdfPage.Graphics;

PdfPen pen = new PdfPen(Color.Red);

PdfBrush brush = new PdfSolidBrush(Color.Blue);

RectangleF rectangle = new RectangleF(0, 0, 100, 100);

//Default color space.

graphics.DrawRectangle(pen, brush, rectangle);

graphics.Save();

//GrayScale color space.

graphics.ColorSpace = PdfColorSpace.GrayScale;

graphics.DrawRectangle(pen, brush, rectangle);

//CMYK color space.

graphics.ColorSpace = PdfColorSpace.CMYK;

graphics.DrawRectangle(pen, brush, rectangle);

graphics.Restore();

//Default color space.

graphics.DrawRectangle(pen, brush, rectangle);

//Draws by using the PdfBrush.

graphics.DrawRectangle(brush, rectangle);

//Save the document into stream

MemoryStream stream = new MemoryStream();

pdfDocument.Save(stream);

stream.Position = 0;

//Closes the document

pdfDocument.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Creates a new PDF document.

PdfDocument pdfDocument = new PdfDocument();

//Adds a page to the PDF document.

PdfPage pdfPage = pdfDocument.Pages.Add();

//Acquires graphics of the page.

PdfGraphics graphics = pdfPage.Graphics;

PdfPen pen = new PdfPen(Syncfusion.Drawing.Color.Red);

PdfBrush brush = new PdfSolidBrush(Syncfusion.Drawing.Color.Blue);

RectangleF rectangle = new RectangleF(0, 0, 100, 100);

//Default color space.

graphics.DrawRectangle(pen, brush, rectangle);

graphics.Save();

//GrayScale color space.

graphics.ColorSpace = PdfColorSpace.GrayScale;

graphics.DrawRectangle(pen, brush, rectangle);

//CMYK color space.

graphics.ColorSpace = PdfColorSpace.CMYK;

graphics.DrawRectangle(pen, brush, rectangle);

graphics.Restore();

//Default color space.

graphics.DrawRectangle(pen, brush, rectangle);

//Draws by using the PdfBrush.

graphics.DrawRectangle(brush, rectangle);

//Save the document into stream.

MemoryStream stream = new MemoryStream();

pdfDocument.Save(stream);

//Close the document.

pdfDocument.Close(true);

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

The following code illustrates how to use the color spaces in particular objects in existing PDF document.
{% tabs %}
{% highlight c# %}


//Loads the existing PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);

//Loads the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Acquires graphics of the page.

PdfGraphics graphics = loadedPage.Graphics;

PdfPen pen = new PdfPen(Color.Red);

PdfBrush brush = new PdfSolidBrush(Color.Blue);

RectangleF rectangle = new RectangleF(0, 0, 100, 100);

//Default color space.

graphics.DrawRectangle(pen, brush, rectangle);

graphics.Save();

//GrayScale color space.

graphics.ColorSpace = PdfColorSpace.GrayScale;

graphics.DrawRectangle(pen, brush, rectangle);

//CMYK color space.

graphics.ColorSpace = PdfColorSpace.CMYK;

graphics.DrawRectangle(pen, brush, rectangle);

graphics.Restore();

//Default color space.

graphics.DrawRectangle(pen, brush, rectangle);

//Draws by using the PdfBrush.

graphics.DrawRectangle(brush, rectangle);

//Saves the document.

loadedDocument.Save("Output.pdf");

//Closes the document

loadedDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}

'Loads the existing PDF document.

Dim loadedDocument As New PdfLoadedDocument(fileName)

'Loads the page

Dim loadedPage As PdfLoadedPage = TryCast(loadedDocument.Pages(0), PdfLoadedPage)

'Acquires graphics of the page.

Dim graphics As PdfGraphics = loadedPage.Graphics

Dim pen As New PdfPen(Color.Red)

Dim brush As PdfBrush = New PdfSolidBrush(Color.Blue)

Dim rectangle As New RectangleF(0, 0, 100, 100)

'Default color space.

graphics.DrawRectangle(pen, brush, rectangle)

graphics.Save()

'GrayScale color space.

graphics.ColorSpace = PdfColorSpace.GrayScale

graphics.DrawRectangle(pen, brush, rectangle)

'CMYK color space.

graphics.ColorSpace = PdfColorSpace.CMYK

graphics.DrawRectangle(pen, brush, rectangle)

graphics.Restore()

'Default color space.

graphics.DrawRectangle(pen, brush, rectangle)

'Draws by using the PdfBrush.

graphics.DrawRectangle(brush, rectangle)

'Saves the document.

loadedDocument.Save("Output.pdf")

'Closes the document

loadedDocument.Close(True)



{% endhighlight %}

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

//Loads the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Acquires graphics of the page.

PdfGraphics graphics = loadedPage.Graphics;

PdfPen pen = new PdfPen(new PdfColor(255,0,0));

PdfBrush brush = new PdfSolidBrush(new PdfColor(0,0,255));

RectangleF rectangle = new RectangleF(0, 0, 100, 100);

//Default color space.

graphics.DrawRectangle(pen, brush, rectangle);

graphics.Save();

//GrayScale color space.

graphics.ColorSpace = PdfColorSpace.GrayScale;

graphics.DrawRectangle(pen, brush, rectangle);

//CMYK color space.

graphics.ColorSpace = PdfColorSpace.CMYK;

graphics.DrawRectangle(pen, brush, rectangle);

graphics.Restore();

//Default color space.

graphics.DrawRectangle(pen, brush, rectangle);

//Draws by using the PdfBrush.

graphics.DrawRectangle(brush, rectangle);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await loadedDocument.SaveAsync(stream);

//Close the document

loadedDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document

FileStream docStream = new FileStream(fileName, FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Loads the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Acquires graphics of the page.

PdfGraphics graphics = loadedPage.Graphics;

PdfPen pen = new PdfPen(Color.Red);

PdfBrush brush = new PdfSolidBrush(Color.Blue);

RectangleF rectangle = new RectangleF(0, 0, 100, 100);

//Default color space.

graphics.DrawRectangle(pen, brush, rectangle);

graphics.Save();

//GrayScale color space.

graphics.ColorSpace = PdfColorSpace.GrayScale;

graphics.DrawRectangle(pen, brush, rectangle);

//CMYK color space.

graphics.ColorSpace = PdfColorSpace.CMYK;

graphics.DrawRectangle(pen, brush, rectangle);

graphics.Restore();

//Default color space.

graphics.DrawRectangle(pen, brush, rectangle);

//Draws by using the PdfBrush.

graphics.DrawRectangle(brush, rectangle);

//Save the document into stream

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

stream.Position = 0;

//Closes the document

loadedDocument.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream

 Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample.pdf");

 PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

 //Loads the page

 PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

 //Acquires graphics of the page.

 PdfGraphics graphics = loadedPage.Graphics;

 PdfPen pen = new PdfPen(Syncfusion.Drawing.Color.Red);

 PdfBrush brush = new PdfSolidBrush(Syncfusion.Drawing.Color.Blue);

 RectangleF rectangle = new RectangleF(0, 0, 100, 100);

 //Default color space.

 graphics.DrawRectangle(pen, brush, rectangle);

 graphics.Save();

 //GrayScale color space.

 graphics.ColorSpace = PdfColorSpace.GrayScale;

 graphics.DrawRectangle(pen, brush, rectangle);

 //CMYK color space.

 graphics.ColorSpace = PdfColorSpace.CMYK;

 graphics.DrawRectangle(pen, brush, rectangle);

 graphics.Restore();

 //Default color space.

 graphics.DrawRectangle(pen, brush, rectangle);

 //Draws by using the PdfBrush.

 graphics.DrawRectangle(brush, rectangle);

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
