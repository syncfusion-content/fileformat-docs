---
title: Working with Barcode
description: This section explains about how to add 1D & 2D barcodes to the PDF document and customize the appearance, position and size of the one dimensional barcode.
platform: file-formats
control: PDF
documentation: 
---
# Working with Barcode

Essential PDF provides support to add barcodes to the PDF document. The following barcode types are supported.

* 10 one-dimensional barcodes including Code 39 and Code 32 barcodes.
* 2 two-dimensional barcodes such as QR and DataMatrix barcode

## Adding a one dimensional barcode to the PDF document


The below code snippet shows how to add Code39 barcode to a PDF document.
{% tabs %}
{% highlight c# %}
//Creating new PDF Document

PdfDocument doc = new PdfDocument();

//Adding new page to PDF document

PdfPage page = doc.Pages.Add();

//Drawing Code39 barcode 

PdfCode39Barcode barcode = new PdfCode39Barcode(); 

//Setting height of the barcode 

barcode.BarHeight = 45; 

barcode.Text = "CODE39$"; 

//Printing barcode on to the Pdf. 

barcode.Draw(page, new PointF(25, 70 ));

//Saving the Document

doc.Save("CODE39.pdf");



{% endhighlight %}



{% highlight vb.net %}

'Creating new PDF Document

Dim doc As New PdfDocument()

'Adding new page to PDF document

Dim page As PdfPage = doc.Pages.Add()

'Drawing Code39 barcode 

Dim barcode As New PdfCode39Barcode()

'Setting height of the barcode 

barcode.BarHeight = 45

barcode.Text = "CODE39$"

'Printing barcode on to the Pdf. 

barcode.Draw(page, New PointF(25, 70))

'Saving the Document

doc.Save("CODE39.pdf")           





{% endhighlight %}

{% highlight UWP %}

//Creating new PDF Document

PdfDocument doc = new PdfDocument();

//Adding new page to PDF document

PdfPage page = doc.Pages.Add();

//Drawing Code39 barcode 

PdfCode39Barcode barcode = new PdfCode39Barcode();

//Setting height of the barcode 

barcode.BarHeight = 45;

barcode.Text = "CODE39$";

//Printing barcode on to the Pdf. 

barcode.Draw(page, new PointF(25, 70));

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await doc.SaveAsync(stream);

//Close the document

doc.Close(true);                                                                   

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Creating new PDF Document

PdfDocument doc = new PdfDocument();

//Adding new page to PDF document

PdfPage page = doc.Pages.Add();

//Drawing Code39 barcode 

PdfCode39Barcode barcode = new PdfCode39Barcode();

//Setting height of the barcode 

barcode.BarHeight = 45;

barcode.Text = "CODE39$";

//Printing barcode on to the Pdf. 

barcode.Draw(page, new PointF(25, 70));

//Save the document into stream.

MemoryStream stream = new MemoryStream();

doc.Save(stream);

stream.Position = 0;

//Close the documents.

doc.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = " CODE39.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Creating new PDF Document

PdfDocument doc = new PdfDocument();

//Adding new page to PDF document

PdfPage page = doc.Pages.Add();

//Drawing Code39 barcode 

PdfCode39Barcode barcode = new PdfCode39Barcode();

//Setting height of the barcode 

barcode.BarHeight = 45;

barcode.Text = "CODE39$";

//Printing barcode on to the Pdf. 

barcode.Draw(page, new PointF(25, 70));

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

doc.Save(stream);

//Closes the document

doc.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples

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

## Adding a two dimensional barcode to a PDF document

The below code snippet shows how to add a QR code to the PDF document.
{% tabs %}
{% highlight c# %}


//Drawing QR Barcode

PdfQRBarcode barcode = new PdfQRBarcode();

//Set Error Correction Level

barcode.ErrorCorrectionLevel = PdfErrorCorrectionLevel.High;

//Set XDimension

barcode.XDimension = 3;

barcode.Text = "http://www.syncfusion.com";

//Creating new PDF Document

PdfDocument doc = new PdfDocument();

//Adding new page to PDF document

PdfPage page = doc.Pages.Add();

//Printing barcode on to the Pdf. 

barcode.Draw(page, new PointF(25, 70));

//Saving the Document

doc.Save("QRBarcode.pdf");



{% endhighlight %}



{% highlight vb.net %}

'Drawing QR Barcode

Dim barcode As New PdfQRBarcode()

'Set Error Correction Level

barcode.ErrorCorrectionLevel = PdfErrorCorrectionLevel.High

'Set XDimension

barcode.XDimension = 3

barcode.Text = "http://www.syncfusion.com"

'Creating new PDF Document

Dim doc As New PdfDocument()

'Adding new page to PDF document

Dim page As PdfPage = doc.Pages.Add()

'Printing barcode on to the Pdf. 

barcode.Draw(page, New PointF(25, 70))

'Saving the Document

doc.Save("QRBarcode.pdf")







{% endhighlight %}

{% highlight UWP %}

//Drawing QR Barcode

PdfQRBarcode barcode = new PdfQRBarcode();

//Set Error Correction Level

barcode.ErrorCorrectionLevel = PdfErrorCorrectionLevel.High;

//Set XDimension

barcode.XDimension = 3;

barcode.Text = "http://www.syncfusion.com";

//Creating new PDF Document

PdfDocument doc = new PdfDocument();

//Adding new page to PDF document

PdfPage page = doc.Pages.Add();

//Printing barcode on to the Pdf. 

barcode.Draw(page, new PointF(25, 70));

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await doc.SaveAsync(stream);

//Close the document

doc.Close(true);                                                                   

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Drawing QR Barcode

PdfQRBarcode barcode = new PdfQRBarcode();

//Set Error Correction Level

barcode.ErrorCorrectionLevel = PdfErrorCorrectionLevel.High;

//Set XDimension

barcode.XDimension = 3;

barcode.Text = "http://www.syncfusion.com";
barcode.Text = "http://www.syncfusion.com";

//Creating new PDF Document

PdfDocument doc = new PdfDocument();

//Adding new page to PDF document

PdfPage page = doc.Pages.Add();

//Printing barcode on to the Pdf. 

barcode.Draw(page, new PointF(25, 70));

//Save the document into stream.

MemoryStream stream = new MemoryStream();

doc.Save(stream);

stream.Position = 0;

//Close the documents.

doc.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = " QRBarcode.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Drawing QR Barcode

PdfQRBarcode barcode = new PdfQRBarcode();

//Set Error Correction Level

barcode.ErrorCorrectionLevel = PdfErrorCorrectionLevel.High;

//Set XDimension

barcode.XDimension = 3;

barcode.Text = "http://www.syncfusion.com";

//Creating new PDF Document

PdfDocument doc = new PdfDocument();

//Adding new page to PDF document

PdfPage page = doc.Pages.Add();

//Printing barcode on to the Pdf. 

barcode.Draw(page, new PointF(25, 70));

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

doc.Save(stream);

//Closes the document

doc.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples

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


## Set location and size to the barcode


The following code snippets show how to set size and location for Codabar barcode to a PDF document.
{% tabs %}
{% highlight c# %}

//Creating new PDF Document

PdfDocument doc = new PdfDocument();

//Adding new page to PDF document

PdfPage page = doc.Pages.Add();

//Create new instance for Codabar barcode

PdfCodabarBarcode barcode = new PdfCodabarBarcode();

//Setting location of the barcode 

barcode.Location = new PointF(100, 100);

//Setting size of the barcode

barcode.Size = new SizeF(200, 100);

barcode.Text = "123456789$";

//Printing barcode on to the Pdf. 

barcode.Draw(page);

//Save and close the Document

doc.Save("CODABAR.pdf");

doc.Close(true);



{% endhighlight %}



{% highlight vb.net %}

'Creating new PDF Document

Dim doc As New PdfDocument()

'Adding new page to PDF document

Dim page As PdfPage = doc.Pages.Add()

'Create new instance for Codabar barcode

Dim barcode As PdfCodabarBarcode = New PdfCodabarBarcode()

'Setting location of the barcode 

barcode.Location = New PointF(100, 100)

'Setting size of the barcode

barcode.Size = New SizeF(200, 100)

barcode.Text = "123456789$"

'Printing barcode on to the Pdf. 

barcode.Draw(page)

'Save and close the Document

doc.Save("CODABAR.pdf")

doc.Close(True)      


{% endhighlight %}

{% highlight UWP %}

//Creating new PDF Document

PdfDocument doc = new PdfDocument();

//Adding new page to PDF document

PdfPage page = doc.Pages.Add();

//Create new instance for Codabar barcode

PdfCodabarBarcode barcode = new PdfCodabarBarcode();

//Setting location of the barcode 

barcode.Location = new PointF(100, 100);

//Setting size of the barcode

barcode.Size = new SizeF(200, 100);

barcode.Text = "123456789$";

//Printing barcode on to the Pdf. 

barcode.Draw(page);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await doc.SaveAsync(stream);

//Close the document

doc.Close(true);                                                                   

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Creating new PDF Document

PdfDocument doc = new PdfDocument();

//Adding new page to PDF document

PdfPage page = doc.Pages.Add();

//Create new instance for Codabar barcode

PdfCodabarBarcode barcode = new PdfCodabarBarcode();

//Setting location of the barcode 

barcode.Location = new PointF(100, 100);

//Setting size of the barcode

barcode.Size = new SizeF(200, 100);

barcode.Text = "123456789$";

//Printing barcode on to the Pdf. 

barcode.Draw(page);

//Save the document into stream.

MemoryStream stream = new MemoryStream();

doc.Save(stream);

stream.Position = 0;

//Close the documents.

doc.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = " CODABAR.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Creating new PDF Document

PdfDocument doc = new PdfDocument();

//Adding new page to PDF document

PdfPage page = doc.Pages.Add();

//Create new instance for Codabar barcode

PdfCodabarBarcode barcode = new PdfCodabarBarcode();

//Setting location of the barcode 

barcode.Location = new PointF(100, 100);

//Setting size of the barcode

barcode.Size = new SizeF(200, 100);

barcode.Text = "123456789$";

//Printing barcode on to the Pdf. 

barcode.Draw(page);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

doc.Save(stream);

//Closes the document

doc.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples

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


## Customizing the barcode appearance

The height of the barcode can be changed using the **BarHeight** property. The equivalent property to change the block size for two dimensional barcode is **XDimension**. You can also customize the barcode color by changing the DarkBarColor and LightBarColor properties.

N> This color customization is possible only for one dimensional barcodes and it is not supported for two dimensional barcodes.

## Supported barcode types

The following table contains the supported types and associated valid characters.

<table>
<thead>
<tr>
<th>
Symbol <br/><br/></th><th>
Supported characters<br/><br/></th><th>
Length<br/><br/></th></tr>
</thead>
<tbody>
<tr>
<td>
{{'[QR Code](https://en.wikipedia.org/wiki/QR_code#"")'| markdownify }}<br/><br/></td><td>
[0–9]; [A–Z (upper-case only)]; [space $ % * + - . / , :]; [Shift JIS characters]<br/><br/></td><td>
variable<br/><br/></td></tr>
<tr>
<td>
{{'[DataMatrix](https://en.wikipedia.org/wiki/Data_Matrix#"")'| markdownify }}<br/><br/></td><td>
All ASCII characters<br/><br/></td><td>
<br/><br/></td></tr>
<tr>
<td>
{{'[Code 39](https://en.wikipedia.org/wiki/Code_39#"")'| markdownify }}<br/><br/></td><td>
[0-9]; [A-Z]; [- . $ / + % SPACE]<br/><br/></td><td>
variable<br/><br/></td></tr>
<tr>
<td>
{{'[Code 39 Extended](https://en.wikipedia.org/wiki/Code_39#Full_ASCII_Code_39"")'| markdownify }}<br/><br/></td><td>
[0-9]; [A-Z]; [a-z]<br/><br/></td><td>
variable<br/><br/></td></tr>
<tr>
<td>
{{'[Code 11](https://en.wikipedia.org/wiki/Code_11#"")'| markdownify }}<br/><br/></td><td>
[0-9]; [-]<br/><br/></td><td>
variable<br/><br/></td></tr>
<tr>
<td>
{{'[Codabar](https://en.wikipedia.org/wiki/Codabar#"")'| markdownify }}<br/><br/></td><td>
[0-9]; [- $ : / . +]<br/><br/></td><td>
variable<br/><br/></td></tr>
<tr>
<td>
Code 32<br/><br/></td><td>
[0-9]<br/><br/></td><td>
8<br/><br/></td></tr>
<tr>
<td>
{{'[Code 93](https://en.wikipedia.org/wiki/Code_93#"")'| markdownify }}<br/><br/></td><td>
[0-9]; [A-Z]; [- . $ / + % SPACE]<br/><br/></td><td>
variable<br/><br/></td></tr>
<tr>
<td>
{{'[Code 93 Extended](https://en.wikipedia.org/wiki/Code_93#Full_ASCII_Code_93"")'| markdownify }}<br/><br/></td><td>
All 128 ASCII characters<br/><br/></td><td>
variable<br/><br/></td></tr>
<tr>
<td>
{{'[Code 128A](https://en.wikipedia.org/wiki/Code_128#"")'| markdownify }}<br/><br/></td><td>
[0-9]; [A-Z]; [NUL (0x00) SOH (0x01) STX (0x02) ETX (0x03) EOT(0x04) ENQ (0x05) ACK (0x06) BEL (0x07) BS (0x08) HT (0x09) LF (0x0A) VT(0x0B) FF (0x0C) CR (0x0D) SO (0x0E) SI (0x0F) DLE (0x10) DC1 (0x11) DC2(0x12) DC3 (0x13) DC4 (0x14) NAK (0x15) SYN (0x16) ETB (0x17) CAN(0x18) EM (0x19) SUB (0x1A) ESC (0x1B) FS (0x1C) GS (0x1D) RS (0x1E) US(0x1F) SPACE (0x20)]; [" ! # $ % & ' ( ) * + , - . / ; < = > ? @ [ / ]^ _ ]<br/><br/></td><td>
variable<br/><br/></td></tr>
<tr>
<td>
{{'[Code 128B](https://en.wikipedia.org/wiki/Code_128#"")'| markdownify }}<br/><br/></td><td>
[0-9]; [A-Z]; [a-z]; [SPACE (0x20) ! " # $ % & ' ( ) * + , - . / :; < = > ? @ [ / ]^ _ ` { | } ~ DEL (•) ]<br/><br/></td><td>
variable<br/><br/></td></tr>
<tr>
<td>
{{'[Code 128C](https://en.wikipedia.org/wiki/Code_128#"")'| markdownify }}<br/><br/></td><td>
ASCII 00-99(encodes each two digit with one code)<br/><br/></td><td>
variable<br/><br/></td></tr>
</tbody>
</table>
