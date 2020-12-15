---
title: Working with Barcode | Syncfusion
description: This section explains about how to add 1D & 2D barcodes to the PDF document and customize the appearance, position and size of the one dimensional barcode.
platform: file-formats
control: PDF
documentation: 
---
# Working with Barcode

Essential PDF provides support to add barcodes to the PDF document. The following barcode types are supported.

* 10 one-dimensional barcodes including Code 39 and Code 32 barcodes.
* 2 two-dimensional barcodes such as QR, DataMatrix and PDF417 barcodes

## Adding a one dimensional barcode to the PDF document


The below code snippet shows how to add Code39 barcode using the [PdfCode39Barcode](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Barcode.PdfCode39Barcode.html) class to a PDF document.
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

The below code snippet shows how to add PdfEan13 barcode using the [PdfEan13Barcode](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Barcode.PdfEan13Barcode.html) class to a PDF document.
{% tabs %}
{% highlight c# %}

//Creates a new PdfEan13 Barcode.

PdfEan13Barcode barcode = new PdfEan13Barcode ();

//Set height of the barcode.

barcode.BarHeight = 50;

//Set the barcode text

barcode.Text = "400638133393";

//Creating new PDF document.

PdfDocument document = new PdfDocument();

//Adding new page to PDF document.

PdfPage page = document.Pages.Add(); 

//Printing barcode on to the Pdf

barcode.Draw(page, new PointF(25,70));

//Saving the document.

document.Save("EAN13Barcode.pdf");

//Close the document

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Creates a new PdfEan13 Barcode.

Dim barcode As New PdfEan13Barcode () 

'Set height of the barcode.

barcode.BarHeight = 50

'Set the barcode text

barcode.Text = "400638133393"

'Creating new PDF document.

Dim document As New PdfDocument()

'Adding new page to PDF document.

Dim page As PdfPage = document.Pages.Add()

'Printing barcode on to the Pdf

barcode.Draw(page, New PointF(25, 70))

'Saving the document.

document.Save("EAN13Barcode.pdf")

‘Close the document.

document.Close(True)

{% endhighlight %}

{% highlight UWP %}

// Creates a new PdfEan13 Barcode.

PdfEan13Barcode barcode = new PdfEan13Barcode ();

//Set height of the barcode.

barcode.BarHeight = 50;

//Set the barcode text

barcode.Text = "400638133393";

//Creating new PDF document.

PdfDocument document = new PdfDocument();

//Adding new page to PDF document.

PdfPage page = document.Pages.Add();

//Printing barcode on to the Pdf

barcode.Draw(page, new PointF(25,70));
      
//Save the PDF document to stream  

MemoryStream stream = new MemorySteam(); 

document.Save(stream);
 
//Close the document 

document.Close(true); 

//Save the stream as a PDF document file in the local machine. Refer to the PDF or UWP section for the respected code samples

Save(stream, "EAN13Barcode.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

// Creates a new PdfEan13 Barcode.

PdfEan13Barcode barcode = new PdfEan13Barcode ();

//Set height of the barcode

barcode.BarHeight = 50;

//Set the barcode text

barcode.Text = "400638133393";

//Creating new PDF document.

PdfDocument document = new PdfDocument();

//Adding new page to PDF document.

PdfPage page = document.Pages.Add();

//Printing barcode on to the Pdf

barcode.Draw(page, new PointF(25,70));

//Creating the stream object  

MemoryStream stream = new MemoryStream(); 

//Save the document into stream 

document.Save(stream); 

//If the position is not set to '0' then the PDF will be empty
 
stream.Position = 0; 

//Close the document 

document.Close(true); 

//Defining the ContentType for pdf file 

string contentType = "application/pdf"; 

//Define the file name 

string fileName = "EAN13Barcode.pdf"; 

//Creates a FileContentResult object by using the file contents, content type, and file name 

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

// Creates a new PdfEan13 Barcode.

PdfEan13Barcode barcode = new PdfEan13Barcode ();

//Set height and text of the barcode

barcode.BarHeight = 50;

barcode.Text = "400638133393";

//Creating new PDF document.

PdfDocument document = new PdfDocument();

//Adding new page to PDF document.

PdfPage page = document.Pages.Add();

//Printing barcode on to the Pdf

barcode.Draw(page, new PointF(25,70));

//Save the PDF document to stream 

MemoryStream stream = new MemoryStream(); 

document.Save(stream);

//Close the document 

document.Close(true); 

//Save the stream into pdf file 

Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("EAN13Barcode.pdf", "application/pdf", stream);

{% endhighlight %}

{% endtabs %}

The below code snippet shows how to add PdfEan8 barcode using the [PdfEan8Barcode](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Barcode.PdfEan8Barcode.html) class to a PDF document.
{% tabs %}
{% highlight c# %}

//Creates a new PdfEan8 Barcode.

PdfEan8Barcode barcode = new PdfEan8Barcode ();

//Set height of the barcode.

barcode.BarHeight = 50;

//Set the barcode text

barcode.Text = "1234567";

//Creating new PDF document.

PdfDocument document = new PdfDocument();

//Adding new page to PDF document.

PdfPage page = document.Pages.Add(); 

//Printing barcode on to the Pdf

barcode.Draw(page, new PointF(25,70));

//Saving the document.

document.Save("EAN8Barcode.pdf");

//Close the document

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Creates a new PdfEan8 Barcode.

Dim barcode As New PdfEan8Barcode () 

'Set height of the barcode.

barcode.BarHeight = 50

'Set the barcode text

barcode.Text = "1234567"

'Creating new PDF document.

Dim document As New PdfDocument()

'Adding new page to PDF document.

Dim page As PdfPage = document.Pages.Add()

'Printing barcode on to the Pdf

barcode.Draw(page, New PointF(25, 70))

'Saving the document.

document.Save("EAN8Barcode.pdf")

‘Close the document.

document.Close(True)

{% endhighlight %}

{% highlight UWP %}

// Creates a new PdfEan8 Barcode.

PdfEan8Barcode barcode = new PdfEan8Barcode ();

//Set height of the barcode.

barcode.BarHeight = 50;

//Set the barcode text

barcode.Text = "1234567";

//Creating new PDF document.

PdfDocument document = new PdfDocument();

//Adding new page to PDF document.

PdfPage page = document.Pages.Add();

//Printing barcode on to the Pdf

barcode.Draw(page, new PointF(25,70)); 
     
//Save the PDF document to stream  

MemoryStream stream = new MemorySteam();
 
document.Save(stream); 

//Close the document 

document.Close(true); 

//Save the stream as a PDF document file in the local machine. Refer to the PDF or UWP section for the respected code samples

Save(stream, "EAN8Barcode.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

// Creates a new PdfEan8 Barcode.

PdfEan8Barcode barcode = new PdfEan8Barcode ();

//Set height of the barcode

barcode.BarHeight = 50;

//Set the barcode text

barcode.Text = "1234567";

//Creating new PDF document.

PdfDocument document = new PdfDocument();

//Adding new page to PDF document.

PdfPage page = document.Pages.Add();

//Printing barcode on to the Pdf

barcode.Draw(page, new PointF(25,70));

//Creating the stream object  

MemoryStream stream = new MemoryStream();
 
//Save the document into stream 

document.Save(stream); 

//If the position is not set to '0' then the PDF will be empty 

stream.Position = 0; 

//Close the document 

document.Close(true); 

//Defining the ContentType for pdf file 

string contentType = "application/pdf";
 
//Define the file name 

string fileName = "EAN8Barcode.pdf"; 

//Creates a FileContentResult object by using the file contents, content type, and file name 

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

// Creates a new PdfEan8 Barcode.

PdfEan8Barcode barcode = new PdfEan8Barcode ();

//Set height and text of the barcode

barcode.BarHeight = 50;

barcode.Text = "1234567";

//Creating new PDF document.

PdfDocument document = new PdfDocument();

//Adding new page to PDF document.

PdfPage page = document.Pages.Add();

//Printing barcode on to the Pdf

barcode.Draw(page, new PointF(25,70));

//Save the PDF document to stream 

MemoryStream stream = new MemoryStream(); 

document.Save(stream);

//Close the document 

document.Close(true); 

//Save the stream into pdf file 

Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("EAN8Barcode.pdf", "application/pdf", stream);

{% endhighlight %}

{% endtabs %}

## Adding a two dimensional barcode to a PDF document

The below code snippet shows how to add a QR code using [PdfQRBarcode](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Barcode.PdfQRBarcode.html) class to the PDF document.
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

The below code snippet shows how to add a Pdf417 barcode code using [Pdf417Barcode](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Barcode.Pdf417Barcode.html) class to the PDF document.
{% tabs %}
{% highlight c# %}

//Creates a new Pdf417 Barcode.

Pdf417Barcode barcode = new Pdf417Barcode();

//Set error correction level.

barcode.ErrorCorrectionLevel= Pdf417ErrorCorrectionLevel.Auto;

//Set XDimension

barcode.XDimension = 2;

//Set the barcode text

barcode.Text = "http://www.syncfusion.com";

//Creating new PDF document.

PdfDocument document = new PdfDocument();

//Adding new page to PDF document.

PdfPage page = document.Pages.Add();

//Printing barcode on to the Pdf

barcode.Draw(page, new PointF(25,70));

//Saving the document.

document.Save("417Barcode.pdf");

//Close the document

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Creates a new Pdf417 Barcode.

Dim barcode As New Pdf417Barcode()

'Set error correction level.

barcode.ErrorCorrectionLevel = Pdf417ErrorCorrectionLevel.Auto

'Set XDimension

barcode.XDimension = 2

'Set the barcode text

barcode.Text = "http://www.syncfusion.com"

'Creating new PDF document.

Dim document As New PdfDocument()

'Adding new page to PDF document.

Dim page As PdfPage = document.Pages.Add()

'Printing barcode on to the Pdf

barcode.Draw(page, New PointF(25, 70))

'Saving the document.

document.Save("417Barcode.pdf")

'Close the document.

document.Close(True)

{% endhighlight %}

{% highlight UWP %}

// Creates a new Pdf417 Barcode.

Pdf417Barcode barcode = new Pdf417Barcode();

//Set error correction level.

barcode.ErrorCorrectionLevel= Pdf417ErrorCorrectionLevel.Auto;

//Set XDimension

barcode.XDimension = 2;

//Set the barcode text

barcode.Text = "http://www.syncfusion.com";

//Creating new PDF document.

PdfDocument document = new PdfDocument();

//Adding new page to PDF document.

PdfPage page = document.Pages.Add();

//Printing barcode on to the Pdf

barcode.Draw(page, new PointF(25,70)); 
     
//Save the PDF document to stream 

MemoryStream stream = new MemorySteam(); 

document.Save(stream); 

//Close the document 

document.Close(true);
 
//Save the stream as a PDF document file in the local machine. Refer to the PDF or UWP section for the respected code samples

Save(stream, "417Barcode.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

// Creates a new Pdf417 Barcode.

Pdf417Barcode barcode = new Pdf417Barcode();

//Set error correction level.

barcode.ErrorCorrectionLevel= Pdf417ErrorCorrectionLevel.Auto;

//Set XDimension

barcode.XDimension = 2;

//Set the barcode text

barcode.Text = "http://www.syncfusion.com";

//Creating new PDF document.

PdfDocument document = new PdfDocument();

//Adding new page to PDF document.

PdfPage page = document.Pages.Add();

//Printing barcode on to the Pdf

barcode.Draw(page, new PointF(25,70));

//Creating the stream object 

MemoryStream stream = new MemoryStream(); 

//Save the document into stream 

document.Save(stream); 

//If the position is not set to '0' then the PDF will be empty 

stream.Position = 0; 

//Close the document
 
document.Close(true); 

//Defining the ContentType for pdf file
 
string contentType = "application/pdf";
 
//Define the file name 

string fileName = "417Barcode.pdf"; 

//Creates a FileContentResult object by using the file contents, content type, and file name
 
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

// Creates a new Pdf417 Barcode.

Pdf417Barcode barcode = new Pdf417Barcode();

//Set error correction level.

barcode.ErrorCorrectionLevel= Pdf417ErrorCorrectionLevel.Auto;

//Set XDimension

barcode.XDimension = 2;

barcode.Text = "http://www.syncfusion.com";

//Creating new PDF document.

PdfDocument document = new PdfDocument();

//Adding new page to PDF document.

PdfPage page = document.Pages.Add();

//Printing barcode on to the Pdf

barcode.Draw(page, new PointF(25,70));

//Save the PDF document to stream 

MemoryStream stream = new MemoryStream(); 

document.Save(stream);

//Close the document
 
document.Close(true); 

//Save the stream into pdf file
 
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("417Barcode.pdf", "application/pdf", stream);

{% endhighlight %}

{% endtabs %}

## Set location and size to the barcode


The following code snippets show how to set [Size](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Barcode.PdfBarcode.html#Syncfusion_Pdf_Barcode_PdfBarcode_size) and [Location](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Barcode.PdfBarcode.html#Syncfusion_Pdf_Barcode_PdfBarcode_Location) for Codabar barcode using [PdfCodabarBarcode](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Barcode.PdfCodabarBarcode.html) class to a PDF document.
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

## Adding a barcode to the PDF document without displaying the barcode text

The following code sample shows how to add a barcode to the PDF document without displaying the barcode text.

{% tabs %}
{% highlight C# %}

//Creating a new PDF Document 
PdfDocument doc = new PdfDocument();

//Adding a new page to the PDF document 
PdfPage page = doc.Pages.Add();

//Create a new instance for the Codabar barcode 
PdfCode39Barcode barcode = new PdfCode39Barcode();

//Set the barcode location
barcode.Location = new PointF(10, 10);

//Set the barcode text
barcode.Text = "123456789";

//Disable the barcode text  
barcode.TextDisplayLocation = TextLocation.None;

//Printing barcode on to the Pdf 
barcode.Draw(page);

//Save the PDF document
doc.Save("Output.pdf");

//Close the PDF document
doc.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Creating a new PDF Document 
Dim doc As PdfDocument = New PdfDocument()

'Adding a new page to the PDF document 
Dim page As PdfPage = doc.Pages.Add()

'Create a new instance for the Codabar barcode 
Dim barcode As PdfCode39Barcode = New PdfCode39Barcode()

'Set the barcode location
barcode.Location = New PointF(10, 10)

'Set the barcode text
barcode.Text = "123456789"

'Disable the barcode text  
barcode.TextDisplayLocation = TextLocation.None

'Printing barcode on to the Pdf 
barcode.Draw(page)

'Save the PDF document 
doc.Save("Output.pdf")

'Close the PDF document
doc.Close(True)

{% endhighlight %}

{% highlight UWP %}

//Creating a new PDF Document 
PdfDocument doc = new PdfDocument();

//Adding a new page to the PDF document 
PdfPage page = doc.Pages.Add();

//Create a new instance for the Codabar barcode 
PdfCode39Barcode barcode = new PdfCode39Barcode();

//Set the barcode location
barcode.Location = new PointF(10, 10);

//Set the barcode text
barcode.Text = "123456789";

//Disable the barcode text  
barcode.TextDisplayLocation = TextLocation.None;

//Printing barcode on to the Pdf 
barcode.Draw(page);

//Save the document
MemoryStream stream = new MemoryStream();
document.Save(stream);

//Close the PDF document
document.Close(true);

//Save the stream as a PDF document file in the local machine. Refer to the PDF or UWP section for the respected code samples
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Creating new PDF Document 
PdfDocument doc = new PdfDocument();

//Adding a new page to the PDF document 
PdfPage page = doc.Pages.Add();

//Create a new instance for the Codabar barcode 
PdfCode39Barcode barcode = new PdfCode39Barcode();

//Set the barcode location
barcode.Location = new PointF(10, 10);

//Set the barcode text
barcode.Text = "123456789";

//Disable the barcode text  
barcode.TextDisplayLocation = TextLocation.None;

//Printing barcode on to the Pdf 
barcode.Draw(page);

//Creating the stream object
MemoryStream stream = new MemoryStream();

//Save the document into stream
doc.Save(stream);

//If the position is not set to '0' then the PDF will be empty
stream.Position = 0;

//Close the document
doc.Close(true);

//Defining the ContentType for pdf file
string contentType = "application/pdf";

//Define the file name
string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Creating a new PDF Document 
PdfDocument doc = new PdfDocument();

//Adding a new page to the PDF document 
PdfPage page = doc.Pages.Add();

//Create a new instance for the Codabar barcode 
PdfCode39Barcode barcode = new PdfCode39Barcode();

//Set the barcode location
barcode.Location = new PointF(10, 10);

//Set the barcode text
barcode.Text = "123456789";

//Disable the barcode text  
barcode.TextDisplayLocation = TextLocation.None;

//Printing barcode on to the Pdf 
barcode.Draw(page);

//Save the document to the stream
MemoryStream stream = new MemoryStream();
doc.Save(stream);

//Close the document
doc.Close(true);

stream.Position = 0;

//Save the stream into a pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Please refer PDF/Xamarin section for respective code samples

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

## Export Barcode as Image

Essential PDF supports converting one dimensional barcodes such as Code 39, Code 39 Extended, Code 11, Codabar, Code 32, Code 93, Code 93 Extended, Code 128A, Code 128B, UPC bar code, and Code 128C barcodes to image using the [ToImage](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Barcode.PdfUnidimensionalBarcode.html#Syncfusion_Pdf_Barcode_PdfUnidimensionalBarcode_ToImage) method of [PdfUnidimensionalBarcode](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Barcode.PdfUnidimensionalBarcode.html) instance. 

N> To export barcode as image in .NET Core, the following assembly should be referenced in your application [Syncfusion.Pdf.Imaging.Portable](https://www.nuget.org/packages/Syncfusion.Pdf.Imaging.Net.Core/) .

The following code snippet explains this.

{% tabs %}
{% highlight C# %}
//Initialize a new PdfCode39Barcode instance
PdfCode39Barcode barcode = new PdfCode39Barcode();

//Set the height and text for barcode
barcode.BarHeight = 45;
barcode.Text = "CODE39$";

//Convert the barcode to image
Image barcodeImage = barcode.ToImage(new SizeF(300, 200));

//Save the image
barcodeImage.Save("Image.png", ImageFormat.Png);
{% endhighlight %}

{% highlight vb.net %}
'Initialize a new PdfCode39Barcode instance
Dim barcode As PdfCode39Barcode = New PdfCode39Barcode

'Set the height and text for barcode
barcode.BarHeight = 45
barcode.Text = "CODE39$"

'Convert the barcode to image
Dim barcodeImage As Image = barcode.ToImage(New SizeF(300, 200))

'Save the image
barcodeImage.Save("Image.png", ImageFormat.Png)
{% endhighlight %}

{% highlight UWP %}
//PDF supports conversion of Barcode to Image only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.
{% endhighlight %}

{% highlight ASP.NET Core %}
//Initialize a new PdfCode39Barcode instance
 PdfCode39Barcode barcode = new PdfCode39Barcode();

//Set the height and text for barcode
 barcode.BarHeight = 45;

 barcode.Text = "CODE39$";

//Convert the barcode to image
 Image barcodeImage = barcode.ToImage(new SizeF(300,200)); 

using (MemoryStream stream = new MemoryStream())
 {
    //Save image to stream.
     barcodeImage.Save(stream, ImageFormat.Png);
 }       
{% endhighlight %}

{% highlight Xamarin %}
//PDF supports conversion of Barcode to Image only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.
{% endhighlight %}
{% endtabs %}

Essential PDF supports converting two-dimensional barcodes such as QR Code and Data Matrix barcode to image. The following code snippet explains how to convert a QR code to image using the [ToImage](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Barcode.PdfQRBarcode.html#Syncfusion_Pdf_Barcode_PdfQRBarcode_ToImage) method of [PdfQRBarcode](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Barcode.PdfQRBarcode.html) instance.

{% tabs %}
{% highlight C# %}
//Initialize a new PdfQRBarcode instance
PdfQRBarcode barcode = new PdfQRBarcode();

//Set the XDimension and text for barcode
barcode.XDimension = 3;
barcode.Text = "http://www.google.com";

//Convert the barcode to image
Image barcodeImage = barcode.ToImage(new SizeF(300, 300));

//Save the image
barcodeImage.Save("Image.png", ImageFormat.Png);
{% endhighlight %}

{% highlight vb.net %}
'Initialize a new PdfQRBarcode instance
Dim barcode As PdfQRBarcode = New PdfQRBarcode

'Set the XDimension and text for barcode
barcode.XDimension = 3
barcode.Text = "http://www.google.com"

'Convert the barcode to image
Dim barcodeImage As Image = barcode.ToImage(New SizeF(300, 300))

'Save the image
barcodeImage.Save("Image.jpg", ImageFormat.Png)
{% endhighlight %}

{% highlight UWP %}
//PDF supports conversion of Barcode to Image only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.
{% endhighlight %}

{% highlight ASP.NET Core %}
//Initialize a new PdfQRBarcode instance 
PdfQRBarcode barcode = new PdfQRBarcode();

//Set the XDimension and text for barcode 
barcode.XDimension = 3;
barcode.Text = "http://www.google.com";
         
//Convert the barcode to image 
Image barcodeImage = barcode.ToImage(new SizeF(300, 300));

 using (MemoryStream stream = new MemoryStream())
 {
    //Save image to stream.
    barcodeImage.Save(stream, ImageFormat.Png);
 } 
{% endhighlight %}

{% highlight Xamarin %}
//PDF supports conversion of Barcode to Image only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.
{% endhighlight %}
{% endtabs %}

## Customizing the barcode appearance

The height of the barcode can be changed using the [BarHeight](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Barcode.PdfBarcode.html#Syncfusion_Pdf_Barcode_PdfBarcode_barHeight) property. The equivalent property to change the block size for two dimensional barcode is [XDimension](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Barcode.PdfBidimensionalBarcode.html#Syncfusion_Pdf_Barcode_PdfBidimensionalBarcode_XDimension). You can also customize the barcode color by changing the DarkBarColor and LightBarColor properties.

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
<tr>
<td>
{{'[Pdf417 ](https://en.wikipedia.org/wiki/PDF417#"")'| markdownify }}<br/><br/></td><td>
[0-9]; [A-Z]; [a-z]; Mixed; Punctuation; Byte<br/><br/></td><td>
variable<br/><br/></td></tr>
</tbody>
</table>
