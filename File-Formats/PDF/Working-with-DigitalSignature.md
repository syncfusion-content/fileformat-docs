---
title: Working with Digital Signature | Syncfusion
description: This section explains how to create a digital signature in the PDF document by using Syncfusion .NET PDF library.
platform: file-formats
control: PDF
documentation: UG
---
# Working with Digital Signature

## Adding a digital signature

The Essential PDF allows you to add a [digital signature](https://www.syncfusion.com/document-processing/pdf-framework/net/pdf-library/digital-signature-pdf) to the PDF document. To add a digital signature, you need a certificate with private keys. The Essential PDF provides support for digital signature by using the PFX files, Hardware Security Module (HSM), Online Certificate Status Protocol (OCSP), Certificate Revocation List (CRL), Windows Certificate Store, and supports signatures using the Elliptic Curve Digital Signature Algorithm (ECDSA).

The following code example explains how to add a digital signature to the PDF document by using [PdfSignature](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSignature.html) class.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Creates a new PDF document
PdfDocument document = new PdfDocument();
//Adds a new page
PdfPageBase page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from PFX file with private key
PdfCertificate pdfCert = new PdfCertificate(@"PDF.pfx", "password123");
//Creates a digital signature
PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");
//Sets an image for signature field
PdfBitmap signatureImage = new PdfBitmap(@"signature.jpg");
//Sets signature information
signature.Bounds = new RectangleF(new PointF(0, 0), signatureImage.PhysicalDimension);
signature.ContactInfo = "johndoe@owned.us";
signature.LocationInfo = "Honolulu, Hawaii";
signature.Reason = "I am author of this document.";
//Draws the signature image
graphics.DrawImage(signatureImage, 0, 0);

//Saves and closes the document
document.Save("Output.pdf");
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Creates a new PDF document
Dim document As New PdfDocument()
'Adds a new page
Dim page As PdfPageBase = document.Pages.Add()
'Create PDF graphics for the page
Dim graphics As PdfGraphics = page.Graphics

'Creates a certificate instance from PFX file with private key
Dim pdfCert As New PdfCertificate("PDF.pfx", "password123")
'Creates a digital signature
Dim signature As New PdfSignature(document, page, pdfCert, "Signature")
'Sets an image for signature field
Dim signatureImage As New PdfBitmap("signature.jpg")
'Sets signature information
signature.Bounds = New RectangleF(New PointF(0, 0), signatureImage.PhysicalDimension)
signature.ContactInfo = "johndoe@owned.us"
signature.LocationInfo = "Honolulu, Hawaii"
signature.Reason = "I am author of this document."
'Draws the signature image
graphics.DrawImage(signatureImage, 0, 0)

'Saves and closes the document
document.Save("Output.pdf")
document.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Creates a new PDF document
PdfDocument document = new PdfDocument();
//Adds a new page
PdfPageBase page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from PFX file with private key
Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.PDF.pfx");
PdfCertificate pdfCert = new PdfCertificate(certificateStream, "password123");
//Creates a digital signature
PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");
//Sets an image for signature field
Stream imageStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.signature.jpg");
PdfBitmap signatureImage = new PdfBitmap(imageStream);
//Sets signature information
signature.Bounds = new RectangleF(new PointF(0, 0), signatureImage.PhysicalDimension);
signature.ContactInfo = "johndoe@owned.us";
signature.LocationInfo = "Honolulu, Hawaii";
signature.Reason = "I am author of this document.";
//Draws the signature image
graphics.DrawImage(signatureImage, 0, 0);

//Save the PDF document to stream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream);
//Close the document
document.Close(true);                                                                   
//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Creates a new PDF document
PdfDocument document = new PdfDocument();
//Adds a new page
PdfPageBase page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from PFX file with private key
FileStream certificateStream = new FileStream("PDF.pfx", FileMode.Open, FileAccess.Read);
PdfCertificate pdfCert = new PdfCertificate(certificateStream, "password123");
//Creates a digital signature
PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");
//Sets an image for signature field
FileStream imageStream = new FileStream("signature.jpg", FileMode.Open, FileAccess.Read);
//Sets an image for signature field
PdfBitmap signatureImage = new PdfBitmap(imageStream);
//Sets signature information
signature.Bounds = new RectangleF(new PointF(0, 0), signatureImage.PhysicalDimension);
signature.ContactInfo = "johndoe@owned.us";
signature.LocationInfo = "Honolulu, Hawaii";
signature.Reason = "I am author of this document.";
//Draws the signature image
graphics.DrawImage(signatureImage, 0, 0);

//Save the document into stream
MemoryStream stream = new MemoryStream();
document.Save(stream);
stream.Position = 0;
//Close the document
document.Close(true);
//Defining the ContentType for pdf file
string contentType = "application/pdf";
//Define the file name
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Creates a new PDF document
PdfDocument document = new PdfDocument();
//Adds a new page
PdfPageBase page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from PFX file with private key
Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.PDF.pfx");
PdfCertificate pdfCert = new PdfCertificate(certificateStream, "password123");
//Creates a digital signature
PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");
//Sets an image for signature field
Stream imageStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.signature.jpg");
PdfBitmap signatureImage = new PdfBitmap(imageStream);
//Sets signature information
signature.Bounds = new RectangleF(new PointF(0, 0), signatureImage.PhysicalDimension);
signature.ContactInfo = "johndoe@owned.us";
signature.LocationInfo = "Honolulu, Hawaii";
signature.Reason = "I am author of this document.";
//Draws the signature image
graphics.DrawImage(signatureImage, 0, 0);

//Save the PDF document to stream
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Closes the document
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Digital%20Signature/Add-a-digital-signature-to-the-PDF-document/).

## Adding a digital signature using stream

The following code example illustrates how to add a digital signature in the PDF document as stream using the [PdfSignature](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfCertificate.html) class as follows.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Creates a new PDF document
PdfDocument document = new PdfDocument();
//Adds a new page
PdfPageBase page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Gets a stream from .pfx file
Stream pfxStream = File.OpenRead("PDF.pfx");
//Creates a certificate instance from PFX file stream with private key
PdfCertificate pdfCert = new PdfCertificate(pfxStream, "password123");
//Creates a digital signature
PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");
//Sets an image for signature field
PdfBitmap signatureImage = new PdfBitmap(@"signature.jpg");
//Sets signature information
signature.Bounds = new RectangleF(new PointF(0, 0), signatureImage.PhysicalDimension);
signature.ContactInfo = "johndoe@owned.us";
signature.LocationInfo = "Honolulu, Hawaii";
signature.Reason = "I am author of this document.";
//Draws the signature image
graphics.DrawImage(signatureImage, 0, 0);

//Saves and closes the document
document.Save("Output.pdf");
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
 
'Creates a new PDF document
Dim document As New PdfDocument()
'Adds a new page
Dim page As PdfPageBase = document.Pages.Add()
'Create PDF graphics for the page
Dim graphics As PdfGraphics = page.Graphics

'Gets stream from .pfx file
Dim pfxStream As Stream = File.OpenRead("PDF.pfx")
'Creates a certificate instance from PFX file stream with private key
Dim pdfCert As New PdfCertificate(pfxStream, "password123")
'Creates a digital signature
Dim signature As New PdfSignature(document, page, pdfCert, "Signature")
'Sets an image for signature field
Dim signatureImage As New PdfBitmap("signature.jpg")
'Sets signature information
signature.Bounds = New RectangleF(New PointF(0, 0), signatureImage.PhysicalDimension)
signature.ContactInfo = "johndoe@owned.us"
signature.LocationInfo = "Honolulu, Hawaii"
signature.Reason = "I am author of this document."
'Draws the signature image
graphics.DrawImage(signatureImage, 0, 0)

'Saves and closes the document
document.Save("Output.pdf")
document.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Creates a new PDF document
PdfDocument document = new PdfDocument();
//Adds a new page
PdfPageBase page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from PFX file with private key
Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.PDF.pfx");
PdfCertificate pdfCert = new PdfCertificate(certificateStream, "password123");
//Creates a digital signature
PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");
//Sets an image for signature field
Stream imageStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.signature.jpg");
PdfBitmap signatureImage = new PdfBitmap(imageStream);
//Sets signature information
signature.Bounds = new RectangleF(new PointF(0, 0), signatureImage.PhysicalDimension);
signature.ContactInfo = "johndoe@owned.us";
signature.LocationInfo = "Honolulu, Hawaii";
signature.Reason = "I am author of this document.";
//Draws the signature image
graphics.DrawImage(signatureImage, 0, 0);

//Save the PDF document to stream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream);
//Close the document
document.Close(true);                                                                   
//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples
Save(stream, "output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Creates a new PDF document
PdfDocument document = new PdfDocument();
//Adds a new page
PdfPageBase page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from PFX file with private key
FileStream certificateStream = new FileStream("PDF.pfx", FileMode.Open, FileAccess.Read);
PdfCertificate pdfCert = new PdfCertificate(certificateStream, "password123");
//Creates a digital signature
PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");
//Sets an image for signature field
FileStream imageStream = new FileStream("signature.jpg", FileMode.Open, FileAccess.Read);
//Sets an image for signature field
PdfBitmap signatureImage = new PdfBitmap(imageStream);
//Sets signature information
signature.Bounds = new RectangleF(new PointF(0, 0), signatureImage.PhysicalDimension);
signature.ContactInfo = "johndoe@owned.us";
signature.LocationInfo = "Honolulu, Hawaii";
signature.Reason = "I am author of this document.";
//Draws the signature image
graphics.DrawImage(signatureImage, 0, 0);

//Save the document into stream
MemoryStream stream = new MemoryStream();
document.Save(stream);
stream.Position = 0;
//Close the document
document.Close(true);
//Defining the ContentType for pdf file
string contentType = "application/pdf";
//Define the file name
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Creates a new PDF document
PdfDocument document = new PdfDocument();
//Adds a new page
PdfPageBase page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from PFX file with private key
Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.PDF.pfx");
PdfCertificate pdfCert = new PdfCertificate(certificateStream, "password123");
//Creates a digital signature
PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");
//Sets an image for signature field
Stream imageStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.signature.jpg");
PdfBitmap signatureImage = new PdfBitmap(imageStream);
//Sets signature information
signature.Bounds = new RectangleF(new PointF(0, 0), signatureImage.PhysicalDimension);
signature.ContactInfo = "johndoe@owned.us";
signature.LocationInfo = "Honolulu, Hawaii";
signature.Reason = "I am author of this document.";
//Draws the signature image
graphics.DrawImage(signatureImage, 0, 0);

//Save the PDF document to stream
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Close the document
document.Close(true);
//Save the stream into PDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("sample.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("sample.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

You can add a digital signature to an existing document as follows.

{% tabs %}

{% highlight c# tabtitle="C#" %}
 
//Loads the PDF document with signature field
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");         
//Gets the page
PdfLoadedPage page = loadedDocument.Pages[0] as PdfLoadedPage;

//Creates a signature field
PdfSignatureField signatureField = new PdfSignatureField(page, "SignatureField");
signatureField.Bounds = new RectangleF(0, 0, 100, 100);
signatureField.Signature = new PdfSignature();
//Adds certificate to the signature field
signatureField.Signature.Certificate = new PdfCertificate(@"PDF.pfx", "password123");
signatureField.Signature.Reason = "I am author of this document";
//Adds the field
loadedDocument.Form.Fields.Add(signatureField);

//Saves the certified PDF document
loadedDocument.Save(@"Output.pdf");
loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Loads the PDF document with signature field
Dim loadedDocument As New PdfLoadedDocument("Input.pdf")
'Gets the page
Dim page As PdfLoadedPage = TryCast(loadedDocument.Pages(0), PdfLoadedPage)

'Creates a signature field
Dim signatureField As New PdfSignatureField(page, "SignatureField")
signatureField.Bounds = New RectangleF(0, 0, 100, 100)
signatureField.Signature = New PdfSignature()
'Adds certificate to the signature field
signatureField.Signature.Certificate = New PdfCertificate("PDF.pfx", "password123")
signatureField.Signature.Reason = "I am author of this document"
'Adds the field
loadedDocument.Form.Fields.Add(signatureField)

'Saves the certified PDF document
loadedDocument.Save("Output.pdf")
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
//Gets the page
PdfLoadedPage page = loadedDocument.Pages[0] as PdfLoadedPage;

//Creates a signature field
PdfSignatureField signatureField = new PdfSignatureField(page, "SignatureField");
signatureField.Bounds = new RectangleF(0, 0, 100, 100);
signatureField.Signature = new PdfSignature();
//Adds certificate to the signature field
Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.
signatureField.Signature.Certificate = new PdfCertificate(certificateStream, "password123");
signatureField.Signature.Reason = "I am author of this document";
//Adds the field
loadedDocument.Form.Fields.Add(signatureField);

//Save the PDF document to stream
MemoryStream stream = new MemoryStream();
await loadedDocument.SaveAsync(stream);
//Close the document
loadedDocument.Close(true);                                                                   
//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load the PDF document
FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);
//Gets the page
PdfLoadedPage page = loadedDocument.Pages[0] as PdfLoadedPage;

//Creates a signature field
PdfSignatureField signatureField = new PdfSignatureField(page, "SignatureField");
signatureField.Bounds = new RectangleF(0, 0, 100, 100);
signatureField.Signature = new PdfSignature();
//Adds certificate to the signature field
FileStream certificateStream = new FileStream("PDF.pfx", FileMode.Open, FileAccess.Read);
signatureField.Signature.Certificate = new PdfCertificate(certificateStream, "password123");
signatureField.Signature.Reason = "I am author of this document";
//Adds the field
loadedDocument.Form.Fields.Add(signatureField);

//Save the document into stream
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);
stream.Position = 0;
//Close the document
loadedDocument.Close(true);
//Defining the ContentType for pdf file
string contentType = "application/pdf";
//Define the file name
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Load the file as stream
Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);
//Gets the page
PdfLoadedPage page = loadedDocument.Pages[0] as PdfLoadedPage;

//Creates a signature field
PdfSignatureField signatureField = new PdfSignatureField(page, "SignatureField");
signatureField.Bounds = new RectangleF(0, 0, 100, 100);
signatureField.Signature = new PdfSignature();
//Adds certificate to the signature field
Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.PDF.pfx");
signatureField.Signature.Certificate = new PdfCertificate(certificateStream, "password123");
signatureField.Signature.Reason = "I am author of this document";
//Adds the field
loadedDocument.Form.Fields.Add(signatureField);

//Save the PDF document to stream
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);
//Close the document
loadedDocument.Close(true);
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

## Adding a digital signature using X509Certificate2

The following code example illustrates how to add digital signature in a PDF document using [X509Certificate2](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfCertificate.html#Syncfusion_Pdf_Security_PdfCertificate__ctor_System_Security_Cryptography_X509Certificates_X509Certificate2_) as follows.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Creates a new PDF document
PdfDocument document = new PdfDocument();
//Adds a new page  
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from PFX file with private key  
X509Certificate2 certificate = new X509Certificate2("PDF.pfx", "password123");
PdfCertificate pdfCertificate = new PdfCertificate(certificate);
//Creates a digital signature  
PdfSignature signature = new PdfSignature(document, page, pdfCertificate, "Signature");
//Sets an image for signature field
PdfBitmap signatureImage = new PdfBitmap(@"signature.jpg");
//Sets signature information
signature.Bounds = new RectangleF(new PointF(0, 0), signatureImage.PhysicalDimension);
signature.ContactInfo = "johndoe@owned.us";
signature.LocationInfo = "Honolulu, Hawaii";
signature.Reason = "I am author of this document.";
//Draws the signature image
graphics.DrawImage(signatureImage, 0, 0);

//Save the document
document.Save("Output.pdf");
//Close the document
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Creates a new PDF document
Dim document As New PdfDocument()
'Adds a new page  
Dim page As PdfPage = document.Pages.Add()
'Create PDF graphics for the page
Dim graphics As PdfGraphics = page.Graphics

'Creates a certificate instance from PFX file with private key  
Dim certificate As New X509Certificate2("PDF.pfx", "password123")
Dim pdfCertificate As New PdfCertificate(certificate)
'Creates a digital signature 
Dim signature As New PdfSignature(document, page, pdfCertificate, "Signature")
'Sets an image for signature field
Dim signatureImage As New PdfBitmap("signature.jpg")
'Sets signature information
signature.Bounds = New RectangleF(New PointF(0, 0), signatureImage.PhysicalDimension)
signature.ContactInfo = "johndoe@owned.us"
signature.LocationInfo = "Honolulu, Hawaii"
signature.Reason = "I am author of this document."
'Draws the signature image
graphics.DrawImage(signatureImage, 0, 0)

'Save the document
document.Save("Output.pdf")
'Close the document
document.Close(True)      

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Essential PDF supports adding a digital signature using X509Certificate2 only in Windows Forms, WPF, ASP.NET, ASP.NET MVC, and ASP.NET Core platforms. 

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Creates a new PDF document
PdfDocument document = new PdfDocument();
//Adds a new page  
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from PFX file with private key  
X509Certificate2 certificate = new X509Certificate2("PDF.pfx", "password123");
PdfCertificate pdfCertificate = new PdfCertificate(certificate);
//Creates a digital signature  
PdfSignature signature = new PdfSignature(document, page, pdfCertificate, "Signature");
//Sets an image for signature field
FileStream imageStream = new FileStream("signature.jpg", FileMode.Open, FileAccess.Read);
PdfBitmap signatureImage = new PdfBitmap(imageStream);
//Sets signature information
signature.Bounds = new RectangleF(new PointF(0, 0), signatureImage.PhysicalDimension);
signature.ContactInfo = "johndoe@owned.us";
signature.LocationInfo = "Honolulu, Hawaii";
signature.Reason = "I am author of this document.";
//Draws the signature image
graphics.DrawImage(signatureImage, 0, 0);

//Creating the stream object
MemoryStream stream = new MemoryStream();
//Save the document as stream
document.Save(stream);
//If the position is not set to '0', then the PDF will be empty
stream.Position = 0;
//Close the document
document.Close(true);
//Defining the ContentType for pdf file
string contentType = "application/pdf";
//Define the file name
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Creates a new PDF document
PdfDocument document = new PdfDocument();
//Adds a new page  
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from PFX file with private key  
Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.PDF.pfx");
MemoryStream ms = new MemoryStream();
certificateStream.CopyTo(ms);
X509Certificate2 certificate = new X509Certificate2(ms.ToArray(), "password123");
PdfCertificate pdfCertificate = new PdfCertificate(certificate);
//Creates a digital signature  
PdfSignature signature = new PdfSignature(document, page, pdfCertificate, "Signature");
//Sets an image for signature field
Stream imageStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.signature.jpg");
PdfBitmap signatureImage = new PdfBitmap(imageStream);
//Sets signature information
signature.Bounds = new RectangleF(new PointF(0, 0), signatureImage.PhysicalDimension);
signature.ContactInfo = "johndoe@owned.us";
signature.LocationInfo = "Honolulu, Hawaii";
signature.Reason = "I am author of this document.";
//Draws the signature image
graphics.DrawImage(signatureImage, 0, 0);

//Save the document as stream
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Digital%20Signature/Add-digital-signature-using-X509Certificate2/).

## Signing an existing document

You can load the signature field from the existing PDF document using [PdfLoadedSignatureField](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedSignatureField.html) class and add certificate to the document using [PdfCertificate](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfCertificate.html) class.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Loads a PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");
//Gets the first page of the document
PdfLoadedPage page = loadedDocument.Pages[0] as PdfLoadedPage;
//Gets the first signature field of the PDF document
PdfLoadedSignatureField field = loadedDocument.Form.Fields[0] as PdfLoadedSignatureField;

//Creates a certificate
PdfCertificate certificate = new PdfCertificate(@"PDF.pfx", "password123");
field.Signature = new PdfSignature(loadedDocument,page,certificate,"Signature",field);

//Saves the document
loadedDocument.Save("Output.pdf");
//Close the document
loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
 
'Loads a PDF document
Dim loadedDocument As New PdfLoadedDocument("Input.pdf")
'Gets the first page of the document
Dim page As PdfLoadedPage = TryCast(loadedDocument.Pages(0), PdfLoadedPage)
'Gets the first signature field of the PDF document
Dim field As PdfLoadedSignatureField = TryCast(loadedDocument.Form.Fields(0), PdfLoadedSignatureField)

'Creates a certificate
Dim certificate As New PdfCertificate("PDF.pfx", "password123")
field.Signature = New PdfSignature(loadedDocument, page, certificate, "Signature", field)

'Saves the document
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
//Gets the first page of the document
PdfLoadedPage page = loadedDocument.Pages[0] as PdfLoadedPage;
//Gets the first signature field of the PDF document
PdfLoadedSignatureField field = loadedDocument.Form.Fields[0] as PdfLoadedSignatureField;

//Creates a certificate
Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.
PdfCertificate certificate = new PdfCertificate(certificateStream, "password123");
field.Signature = new PdfSignature(loadedDocument, page, certificate, "Signature", field);

//Save the PDF document to stream
MemoryStream stream = new MemoryStream();
await loadedDocument.SaveAsync(stream);
//Close the document
loadedDocument.Close(true);                                                                   
//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load the PDF document
FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);
//Gets the first page of the document
PdfLoadedPage page = loadedDocument.Pages[0] as PdfLoadedPage;
//Gets the first signature field of the PDF document
PdfLoadedSignatureField field = loadedDocument.Form.Fields[0] as PdfLoadedSignatureField;

//Creates a certificate
FileStream certificateStream = new FileStream("PDF.pfx", FileMode.Open, FileAccess.Read);
PdfCertificate certificate = new PdfCertificate(certificateStream, "password123");
field.Signature = new PdfSignature(loadedDocument, page, certificate, "Signature", field);

//Save the document into stream
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);
stream.Position = 0;
//Close the document
loadedDocument.Close(true);
//Defining the ContentType for pdf file
string contentType = "application/pdf";
//Define the file name
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Load the file as stream
Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample.pdf");
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);
//Gets the first page of the document
PdfLoadedPage page = loadedDocument.Pages[0] as PdfLoadedPage;
//Gets the first signature field of the PDF document
PdfLoadedSignatureField field = loadedDocument.Form.Fields[0] as PdfLoadedSignatureField;

//Creates a certificate
Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.PDF.pfx");
PdfCertificate certificate = new PdfCertificate(certificateStream, "password123");
field.Signature = new PdfSignature(loadedDocument, page, certificate, "Signature", field);

//Save the PDF document to stream
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);
//Close the document
loadedDocument.Close(true);
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Digital%20Signature/Signing-an-existing-PDF-document/).

## Sign an existing document using stream

You can load the signature field from an existing PDF document using [PdfLoadedSignatureField](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedSignatureField.html) class and add certificate to the document as stream using [PdfCertificate](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfCertificate.html) as follows.

{% tabs %}

{% highlight c# tabtitle="C#" %}
 
//Loads a PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");
//Gets the first page of the document
PdfLoadedPage page = loadedDocument.Pages[0] as PdfLoadedPage;
//Gets the first signature field of the PDF document
PdfLoadedSignatureField field = loadedDocument.Form.Fields[0] as PdfLoadedSignatureField;

//Gets the stream from .pfx file
Stream pfxStream = File.OpenRead("PDF.pfx");
//Creates a certificate instance from PFX file stream with private key
PdfCertificate certificate = new PdfCertificate(pfxStream, "password123");
field.Signature = new PdfSignature(loadedDocument, page, certificate, "Signature", field);

//Save the document
loadedDocument.Save("Output.pdf");
//Close the document
loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
 
'Loads a PDF document
Dim loadedDocument As New PdfLoadedDocument("Input.pdf")
'Gets the first page of the document
Dim page As PdfLoadedPage = TryCast(loadedDocument.Pages(0), PdfLoadedPage)
'Gets the first signature field of the PDF document
Dim field As PdfLoadedSignatureField = TryCast(loadedDocument.Form.Fields(0), PdfLoadedSignatureField)

'Gets the stream from .pfx file
Dim pfxStream As Stream = File.OpenRead("PDF.pfx")
'Creates a certificate instance from PFX file stream with private key
Dim certificate As New PdfCertificate(pfxStream, "password123")
field.Signature = New PdfSignature(loadedDocument, page, certificate, "Signature", field)

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
//Gets the first page of the document
PdfLoadedPage page = loadedDocument.Pages[0] as PdfLoadedPage;
//Gets the first signature field of the PDF document
PdfLoadedSignatureField field = loadedDocument.Form.Fields[0] as PdfLoadedSignatureField;

//Creates a certificate
Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.PDF.pfx");
PdfCertificate certificate = new PdfCertificate(certificateStream, "password123");
field.Signature = new PdfSignature(loadedDocument, page, certificate, "Signature", field);

//Save the PDF document to stream
MemoryStream stream = new MemoryStream();
await loadedDocument.SaveAsync(stream);
//Close the document
loadedDocument.Close(true);                                                                   
//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples
Save(stream, "output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load the PDF document
FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);
//Gets the first page of the document
PdfLoadedPage page = loadedDocument.Pages[0] as PdfLoadedPage;
//Gets the first signature field of the PDF document
PdfLoadedSignatureField field = loadedDocument.Form.Fields[0] as PdfLoadedSignatureField;

//Creates a certificate
FileStream certificateStream = new FileStream("PDF.pfx", FileMode.Open, FileAccess.Read);
PdfCertificate certificate = new PdfCertificate(certificateStream, "password123");
field.Signature = new PdfSignature(loadedDocument, page, certificate, "Signature", field);

//Save the document into stream
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);
stream.Position = 0;
//Close the document
loadedDocument.Close(true);
//Defining the ContentType for pdf file
string contentType = "application/pdf";
//Define the file name
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Load the file as stream
Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample.pdf");
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);
//Gets the first page of the document
PdfLoadedPage page = loadedDocument.Pages[0] as PdfLoadedPage;
//Gets the first signature field of the PDF document
PdfLoadedSignatureField field = loadedDocument.Form.Fields[0] as PdfLoadedSignatureField;

//Creates a certificate
Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.PDF.pfx");
PdfCertificate certificate = new PdfCertificate(certificateStream, "password123");
field.Signature = new PdfSignature(loadedDocument, page, certificate, "Signature", field);

//Save the PDF document to stream
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);
//Close the document
loadedDocument.Close(true);
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

## Externally sign a PDF document 

You can sign the PDF document from external digital signature created from various sources such as HSM, USB token, smart card, or other cloud services such as DigitalSign. The following code example shows how to sign the PDF document from external signature using [ComputeHash](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSignature.html#Syncfusion_Pdf_Security_PdfSignature_ComputeHash) Event.

{% tabs %}

{% highlight c# tabtitle="C#" %}
 
//Load existing PDF document
PdfLoadedDocument document = new PdfLoadedDocument("PDF_Succinctly.pdf");
//Creates a digital signature
PdfSignature signature = new PdfSignature(document, document.Pages[0], null, "DigitalSignature");
signature.ComputeHash += Signature_ComputeHash;

//Save the PDF document
document.Save("ExternalSignature.pdf");
//Close the document
document.Close(true);

void Signature_ComputeHash(object sender, PdfSignatureEventArgs arguments)
{
    //Get the document bytes
    byte[] documentBytes = arguments.Data;
    SignedCms signedCms = new SignedCms(new ContentInfo(documentBytes), detached: true);

    //Compute the signature using the specified digital ID file and the password
    X509Certificate2 certificate = new X509Certificate2("DigitalSignatureTest.pfx", "DigitalPass123");
    var cmsSigner = new CmsSigner(certificate);
    
    //Set the digest algorithm SHA256
    cmsSigner.DigestAlgorithm = new Oid("2.16.840.1.101.3.4.2.1");
    signedCms.ComputeSignature(cmsSigner);

    //Embed the encoded digital signature to the PDF document
    arguments.SignedData = signedCms.Encode();
}

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
 
'Load existing PDF document
Dim document As PdfLoadedDocument = New PdfLoadedDocument("PDF_Succinctly.pdf")
'Creates a digital signature
Dim signature As PdfSignature = New PdfSignature(document, document.Pages(0), Nothing, "DigitalSignature")
signature.ComputeHash += Signature_ComputeHash

'Save the PDF document
document.Save("ExternalSignature.pdf")
'Close the document
document.Close(True)

Private Sub Signature_ComputeHash(ByVal sender As Object, ByVal arguments As PdfSignatureEventArgs)
    'Get the document bytes
    Dim documentBytes As Byte() = arguments.Data
    Dim signedCms As SignedCms = New SignedCms(New ContentInfo(documentBytes), detached:=True)

    'Compute the signature using the specified digital ID file and the password
    Dim certificate As X509Certificate2 = New X509Certificate2("DigitalSignatureTest.pfx", "DigitalPass123")
    Dim cmsSigner = New CmsSigner(certificate)

    'Set the digest algorithm SHA256
    cmsSigner.DigestAlgorithm = New Oid("2.16.840.1.101.3.4.2.1")
    signedCms.ComputeSignature(cmsSigner)

    'Embed the encoded digital signature to the PDF document
    arguments.SignedData = signedCms.Encode()
End Sub

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Get the stream from the document
Stream documentStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data. PDF_Succinctly.pdf");
//Load an existing signed PDF document
PdfLoadedDocument document = new PdfLoadedDocument(documentStream);

//Creates a digital signature
PdfSignature signature = new PdfSignature(document, document.Pages[0], null, "DigitalSignature");
signature.ComputeHash += Signature_ComputeHash;

//Save the PDF document to stream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream);
//Close the document
document.Close(true);
//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples
Save(stream, " ExternalSignature.pdf");

private static void Signature_ComputeHash1(object sender, PdfSignatureEventArgs ars)
{
    //Get the document bytes
    byte[] documentBytes = ars.Data;
    SignedCms signedCms = new SignedCms(new ContentInfo(documentBytes), detached: true);

    //Compute the signature using the specified digital ID file and the password
    X509Certificate2 certificate = new X509Certificate2("DigitalSignatureTest.pfx", "DigitalPass123");
    var cmsSigner = new CmsSigner(certificate);

    //Set the digest algorithm SHA256
    cmsSigner.DigestAlgorithm = new Oid("2.16.840.1.101.3.4.2.1");
    signedCms.ComputeSignature(cmsSigner);

    //Embed the encoded digital signature to the PDF document
    ars.SignedData = signedCms.Encode();
}

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Get the stream from the document
FileStream documentStream = new FileStream("PDF_Succinctly.pdf ", FileMode.Open, FileAccess.Read);
//Load the existing PDF document
PdfLoadedDocument document = new PdfLoadedDocument(documentStream);

//Creates a digital signature
PdfSignature signature = new PdfSignature(document, document.Pages[0], null, "DigitalSignature");
signature.ComputeHash += Signature_ComputeHash;

//Save the PDF document to stream
MemoryStream ms = new MemoryStream();
document.Save(ms);
//Close the PDF document 
document.Close(true);

private static void Signature_ComputeHash1(object sender, PdfSignatureEventArgs ars)
{
    //Get the document bytes
    byte[] documentBytes = ars.Data;
    SignedCms signedCms = new SignedCms(new ContentInfo(documentBytes), detached: true);

    //Compute the signature using the specified digital ID file and the password
    X509Certificate2 certificate = new X509Certificate2("DigitalSignatureTest.pfx", "DigitalPass123");
    var cmsSigner = new CmsSigner(certificate);

    //Set the digest algorithm SHA256
    cmsSigner.DigestAlgorithm = new Oid("2.16.840.1.101.3.4.2.1");
    signedCms.ComputeSignature(cmsSigner);

    //Embed the encoded digital signature to the PDF document
    ars.SignedData = signedCms.Encode();
}

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Get the stream from the document
Stream documentStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.PDF_Succinctly.pdf");
//Load an existing signed PDF document
PdfLoadedDocument document = new PdfLoadedDocument(documentStream);

//Creates a digital signature
PdfSignature signature = new PdfSignature(document, document.Pages[0], null, "DigitalSignature");
signature.ComputeHash += Signature_ComputeHash;

//Save the PDF document to stream
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Close the document
document.Close(true);

//Save the stream into pdf file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("ExternalSignature.pdf", "application/pdf", stream);
}
else
{
Xamarin.Forms.DependencyService.Get<ISave>().Save("ExternalSignature.pdf", "application/pdf", stream);
}

private static void Signature_ComputeHash1(object sender, PdfSignatureEventArgs ars)
{
    //Get the document bytes
    byte[] documentBytes = ars.Data;
    SignedCms signedCms = new SignedCms(new ContentInfo(documentBytes), detached: true);

    //Compute the signature using the specified digital ID file and the password
    X509Certificate2 certificate = new X509Certificate2("DigitalSignatureTest.pfx", "DigitalPass123");
    var cmsSigner = new CmsSigner(certificate);

    //Set the digest algorithm SHA256
    cmsSigner.DigestAlgorithm = new Oid("2.16.840.1.101.3.4.2.1");
    signedCms.ComputeSignature(cmsSigner);

    //Embed the encoded digital signature to the PDF document
    ars.SignedData = signedCms.Encode();
}

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Digital%20Signature/Externally-sign-a-PDF-document/).

## Create Long Term Validation (LTV) when signing PDF documents externally

You can create a Long Term validation (LTV) when signing PDF documents externally using your private/public certificates.The following code example shows how to create an LTV when signing a PDF document from external signature using [CreateLongTermValidity](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSignature.html#Syncfusion_Pdf_Security_PdfSignature_CreateLongTermValidity_System_Collections_Generic_List_System_Security_Cryptography_X509Certificates_X509Certificate2__) method in [PdfSignature](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSignature.html) class.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Load an existing PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");
//Get the page of the existing PDF document
PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create a new PDF signature without PdfCertificate instance
PdfSignature signature = new PdfSignature(loadedDocument, loadedPage, null, "Signature1");
//Hook up the ComputeHash event
signature.ComputeHash += Signature_ComputeHash;
//Create X509Certificate2 from your certificate to create a long-term validity
X509Certificate2 x509 = new X509Certificate2("PDF.pfx", "password123");
//Create LTV with your public certificates
signature.CreateLongTermValidity(new List<X509Certificate2> { x509 });

//Save and close the PDF document
loadedDocument.Save("SignedDocument.pdf");
loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Load an existing PDF document
Dim loadedDocument As PdfLoadedDocument = New PdfLoadedDocument("Input.pdf")
'Get the page of the existing PDF document
Dim loadedPage As PdfLoadedPage = TryCast(loadedDocument.Pages(0), PdfLoadedPage)

'Create a new PDF signature without PdfCertificate instance
Dim signature As PdfSignature = New PdfSignature(loadedDocument, loadedPage, Nothing, "Signature1")
'Hook up the ComputeHash event
AddHandler signature.ComputeHash, AddressOf Signature_ComputeHash
'Create X509Certificate2 from your certificate to create a long-term validity
Dim x509 As X509Certificate2 = New X509Certificate2("PDF.pfx", "password123")
'Create LTV with your public certificates
signature.CreateLongTermValidity(New List(Of X509Certificate2) From { x509 })

'Save and close the PDF document
loadedDocument.Save("SignedDocument.pdf")
loadedDocument.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Get the stream from the document
Stream documentStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");
//Load an existing PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(documentStream);
//Get the page of the existing PDF document
PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create a new PDF signature without PdfCertificate instance
PdfSignature signature = new PdfSignature(loadedDocument, loadedPage, null, "Signature1");
//Hook up the ComputeHash event
signature.ComputeHash += Signature_ComputeHash;
//Create X509Certificate2 from your certificate to create a long-term validity
X509Certificate2 x509 = new X509Certificate2("PDF.pfx", "password123");
//Create LTV with your public certificates4
signature.CreateLongTermValidity(new List<X509Certificate2> { x509 });

//Save the PDF document
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);
//If the position is not set to '0' then the PDF will be empty
stream.Position = 0;
//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Get the stream from the document
FileStream documentStream = new FileStream("Input.pdf ", FileMode.Open, FileAccess.Read);
//Load an existing PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(documentStream);
//Get the page of the existing PDF document
PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create a new PDF signature without PdfCertificate instance
PdfSignature signature = new PdfSignature(loadedDocument, loadedPage, null, "Signature1");
//Hook up the ComputeHash event
signature.ComputeHash += Signature_ComputeHash;
//Create X509Certificate2 from your certificate to create a long-term validity
X509Certificate2 x509 = new X509Certificate2("PDF.pfx", "password123");
//Create LTV with your public certificates
signature.CreateLongTermValidity(new List<X509Certificate2> { x509 });

//Save the PDF document
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);
//If the position is not set to '0' then the PDF will be empty
stream.Position = 0;
//Close the document
loadedDocument.Close(true);
//Defining the ContentType for pdf file
string contentType = "application/pdf";
//Define the file name
string fileName = "Output.pdf";
//Creates a File object by using the file contents, content type, and file name
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Get the stream from the document
Stream documentStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets. Input.pdf");
//Load an existing PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(documentStream);
//Get the page of the existing PDF document
PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create a new PDF signature without PdfCertificate instance
PdfSignature signature = new PdfSignature(loadedDocument, loadedPage, null, "Signature1");
//Hook up the ComputeHash event
signature.ComputeHash += Signature_ComputeHash;
//Create X509Certificate2 from your certificate to create a long-term validity
X509Certificate2 x509 = new X509Certificate2("PDF.pfx", "password123");
//Create LTV with your public certificates
signature.CreateLongTermValidity(new List<X509Certificate2> { x509 });

//Save the PDF document
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);
//If the position is not set to '0' then the PDF will be empty
stream.Position = 0;
//Save the stream into pdf file
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Digital%20Signature/Create-LTV-when-signing-PDF-documents-externally/).

## Digitally sign a PDF document using long-term archive timestamps (LTA)

The PDF LTA signature is the next level of the LTV signature. It follows the standard PAdES B-LTA. According to the standard, the validation-related information of the timestamp is added to the DSS along with other signature information mentioned in the LTV signature.

The document timestamp is also applied to the PDF document, so it provides more viability to the signature. This level is recommended for qualified electronic signatures.

The following code example shows how to sign a PDF document with LTA using [TimeStampServer](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSignature.html#Syncfusion_Pdf_Security_PdfSignature_TimeStampServer) property and [EnableLtv](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSignature.html#Syncfusion_Pdf_Security_PdfSignature_EnableLtv) property in [PdfSignature](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSignature.html) class.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Load existing PDF document.
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("PDF_Succinctly.pdf");
//Load digital ID with password.
PdfCertificate certificate = new PdfCertificate("DigitalSignatureTest.pfx", "DigitalPass123");

//Create a signature with loaded digital ID.
PdfSignature signature = new PdfSignature(loadedDocument, loadedDocument.Pages[0], certificate, "DigitalSignature");
signature.Settings.CryptographicStandard = CryptographicStandard.CADES;
signature.Settings.DigestAlgorithm = DigestAlgorithm.SHA256;
signature.TimeStampServer = new TimeStampServer(new Uri("http://timestamping.ensuredca.com"));
//Enable LTV document.
signature.EnableLtv = true;

//Save the PDF document.
loadedDocument.Save("LTV_document.pdf");
//Close the document.
loadedDocument.Close(true);

//Load existing PDF document.
PdfLoadedDocument ltDocument = new PdfLoadedDocument("LTV_document.pdf");
//Load the existing PDF page.
PdfLoadedPage lpage = ltDocument.Pages[0] as PdfLoadedPage;

//Create PDF signature with empty certificate.
PdfSignature timeStamp = new PdfSignature(lpage, "timestamp");
timeStamp.TimeStampServer = new TimeStampServer(new Uri("http://timestamping.ensuredca.com"));

//Save and close the PDF document.
ltDocument.Save("PAdES B-LTA.pdf");
ltDocument.Close(true);
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Loads a PDF document.
Dim loadedDocument As PdfLoadedDocument = New PdfLoadedDocument("PDF_Succinctly.pdf")
'Load digital ID with password.
Dim certificate As PdfCertificate = New PdfCertificate("DigitalSignatureTest.pfx", "DigitalPass123")

'Create a signature with loaded digital ID.
Dim signature As PdfSignature = New PdfSignature(loadedDocument, loadedDocument.Pages(0), certificate, "DigitalSignature")
signature.Settings.CryptographicStandard = CryptographicStandard.CADES
signature.Settings.DigestAlgorithm = DigestAlgorithm.SHA256
signature.TimeStampServer = New TimeStampServer(New Uri("http://timestamping.ensuredca.com"))
'Enable LTV document.
signature.EnableLtv = True

'Save the document.
loadedDocument.Save("LTV_document.pdf")
'Close the document.
loadedDocument.Close(True)

'Loads a PDF document.
Dim ltDocument As PdfLoadedDocument = New PdfLoadedDocument("LTV_document.pdf")
'Load the existing PDF page.
Dim lpage As PdfLoadedPage = TryCast(ltDocument.Pages(0), PdfLoadedPage)

'Create PDF signature with empty certificate.
Dim timeStamp As PdfSignature = New PdfSignature(lpage, "timestamp")
timeStamp.TimeStampServer = New TimeStampServer(New Uri("http://timestamping.ensuredca.com"))

'Save the document.
ltDocument.Save("PAdES B-LTA.pdf")
'Close the document.
ltDocument.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Get the stream from the document.
Stream documentStream1 = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Assets.Input.pdf");
//Load an existing PDF document.
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(documentStream1);
//Get the stream from the document
Stream documentStream2 = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Assets.DigitalSignatureTest.pfx");
//Load digital ID with password.
PdfCertificate certificate = new PdfCertificate(documentStream2, "DigitalPass123");

//Create a signature with loaded digital ID.
PdfSignature signature = new PdfSignature(loadedDocument, loadedDocument.Pages[0], certificate, "DigitalSignature");
signature.Settings.CryptographicStandard = CryptographicStandard.CADES;
signature.Settings.DigestAlgorithm = DigestAlgorithm.SHA256;
signature.TimeStampServer = new TimeStampServer(new Uri("http://timestamping.ensuredca.com"));
//Enable LTV document.
signature.EnableLtv = true;

//Save and close the PDF document.
MemoryStream stream1 = new MemoryStream();
loadedDocument.Save(stream1);
loadedDocument.Close(true);

//Load an existing PDF document.
PdfLoadedDocument ltDocument = new PdfLoadedDocument(stream1);
//Load the existing PDF page.
PdfLoadedPage lpage = ltDocument.Pages[0] as PdfLoadedPage;

//Create PDF signature with empty certificate.
PdfSignature timeStamp = new PdfSignature(lpage, "timestamp");
timeStamp.TimeStampServer = new TimeStampServer(new Uri("http://timestamping.ensuredca.com"));

//Save and close the PDF document.
MemoryStream stream2 = new MemoryStream();
ltDocument.Save(stream2);
ltDocument.Close(true);
//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples.
Save(stream2, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load existing PDF document.
FileStream documentStream1 = new FileStream("PDF_Succinctly.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(documentStream1);
//Load digital ID with password.
FileStream documentStream2 = new FileStream("DigitalSignatureTest.pfx", FileMode.Open, FileAccess.Read);
PdfCertificate certificate = new PdfCertificate(documentStream2, "DigitalPass123");

//Create a signature with loaded digital ID.
PdfSignature signature = new PdfSignature(loadedDocument, loadedDocument.Pages[0], certificate, "DigitalSignature");
signature.Settings.CryptographicStandard = CryptographicStandard.CADES;
signature.Settings.DigestAlgorithm = DigestAlgorithm.SHA256;
signature.TimeStampServer = new TimeStampServer(new Uri("http://timestamping.ensuredca.com"));
//Enable LTV document.
signature.EnableLtv = true;

//Save the PDF document.
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);
//Close the document.
loadedDocument.Close(true);

//Load existing PDF document.
PdfLoadedDocument ltDocument = new PdfLoadedDocument(stream);
//Load the existing PDF page.
PdfLoadedPage lpage = ltDocument.Pages[0] as PdfLoadedPage;

//Create PDF signature with empty certificate.
PdfSignature timeStamp = new PdfSignature(lpage, "timestamp");
timeStamp.TimeStampServer = new TimeStampServer(new Uri("http://timestamping.ensuredca.com"));

//Save and close the PDF document.
MemoryStream stream1 = new MemoryStream();
ltDocument.Save(stream1);
//Close the document.
ltDocument.Close(true);
//Defining the ContentType for pdf file.
string contentType = "application/pdf";
//Define the file name.
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name.
return File(stream1, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Get the stream from the document.
Stream documentStream1 = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Assets.PDF_Succinctly.pdf");
//Load an existing PDF document.
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(documentStream1);
//Get the stream from the document.
Stream documentStream2 = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Assets.DigitalSignatureTest.pfx");
//Load digital ID with password.
PdfCertificate certificate = new PdfCertificate(documentStream2, "DigitalPass123");

//Create a signature with loaded digital ID.
PdfSignature signature = new PdfSignature(loadedDocument, loadedDocument.Pages[0], certificate, "DigitalSignature");
signature.Settings.CryptographicStandard = CryptographicStandard.CADES;
signature.Settings.DigestAlgorithm = DigestAlgorithm.SHA256;
signature.TimeStampServer = new TimeStampServer(new Uri("http://timestamping.ensuredca.com"));
//Enable LTV document.
signature.EnableLtv = true;

//Save and close the PDF document.
MemoryStream stream1 = new MemoryStream();
loadedDocument.Save(stream1);
loadedDocument.Close(true);

//Load an existing PDF document.
PdfLoadedDocument ltDocument = new PdfLoadedDocument(stream1);
//Load the existing PDF page.
PdfLoadedPage lpage = ltDocument.Pages[0] as PdfLoadedPage;
//Create PDF signature with empty certificate.
PdfSignature timeStamp = new PdfSignature(lpage, "timestamp");
timeStamp.TimeStampServer = new TimeStampServer(new Uri("http://timestamping.ensuredca.com"));

//Save the stream into pdf file.
MemoryStream stream2 = new MemoryStream();
ltDocument.Save(stream2);
ltDocument.Close(true);
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream2);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream2);
}
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Digital%20Signature/Sign_PDF_with_LTA/).

## Digitally sign a PDF document using the Windows certificate store

A Windows certificate store is a secure way to store the digital ID. If a root certificate is added to the Windows certificate store, you do not need to manually add and trust each of the certificates that are already present in the Windows certificate store.

You can retrieve the digital ID [X509Certificate2](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfCertificate.html#Syncfusion_Pdf_Security_PdfCertificate__ctor_System_Security_Cryptography_X509Certificates_X509Certificate2_) from the Windows certificate store X509Store and use it to add a digital signature to a PDF document using [PdfSignature](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSignature.html) class.

The following code example shows how to create a PDF digital signature using the Windows certificate store.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Initialize the Windows store.
X509Store store = new X509Store("MY", StoreLocation.CurrentUser);
store.Open(OpenFlags.ReadOnly | OpenFlags.OpenExistingOnly);
X509Certificate2Collection collection = (X509Certificate2Collection)store.Certificates;
//Find the certificate using thumb print.
X509Certificate2Collection fcollection = (X509Certificate2Collection)collection.Find(X509FindType.FindByThumbprint, "F85E1C5D93115CA3F969DA3ABC8E0E9547FCCF5A", true);
X509Certificate2 digitalID = fcollection[0];

//Load existing PDF document.
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("PDF_Succinctly.pdf");
//Load X509Certificate2.
PdfCertificate certificate = new PdfCertificate(digitalID);

//Create a Revision 2 signature with loaded digital ID.
PdfSignature signature = new PdfSignature(loadedDocument, loadedDocument.Pages[0], certificate, "DigitalSignature");
//Changing the digital signature standard and hashing algorithm.
signature.Settings.CryptographicStandard = CryptographicStandard.CADES;
signature.Settings.DigestAlgorithm = DigestAlgorithm.SHA512;

//Save the PDF document.
loadedDocument.Save("WindowsStore.pdf");
//Close the document.
loadedDocument.Close(true);
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Initialize the Windows store.
Dim store As X509Store = New X509Store("MY", StoreLocation.CurrentUser)
store.Open(OpenFlags.[ReadOnly] Or OpenFlags.OpenExistingOnly)
'Find the certificate using thumb print.
Dim collection As X509Certificate2Collection = CType(store.Certificates, X509Certificate2Collection)
Dim fcollection As X509Certificate2Collection = CType(collection.Find(X509FindType.FindByThumbprint, "F85E1C5D93115CA3F969DA3ABC8E0E9547FCCF5A", True), X509Certificate2Collection)
Dim digitalID As X509Certificate2 = fcollection(0)

'Load existing PDF document.
Dim loadedDocument As PdfLoadedDocument = New PdfLoadedDocument("PDF_Succinctly.pdf")
'Load X509Certificate2.
Dim certificate As PdfCertificate = New PdfCertificate(digitalID)
'Create a Revision 2 signature with loaded digital ID.
Dim signature As PdfSignature = New PdfSignature(loadedDocument, loadedDocument.Pages(0), certificate, "DigitalSignature")
'Changing the digital signature standard and hashing algorithm.
signature.Settings.CryptographicStandard = CryptographicStandard.CADES
signature.Settings.DigestAlgorithm = DigestAlgorithm.SHA512

'Save the PDF document.
loadedDocument.Save("WindowsStore.pdf")
'Close the document.
loadedDocument.Close(True)
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Essential PDF supports Digitally sign a PDF document using Windows certificate store only in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms.

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Initialize the Windows store.
X509Store store = new X509Store("MY", StoreLocation.CurrentUser);
store.Open(OpenFlags.ReadOnly | OpenFlags.OpenExistingOnly);
X509Certificate2Collection collection = (X509Certificate2Collection)store.Certificates;
//Find the certificate using thumb print.
X509Certificate2Collection fcollection = (X509Certificate2Collection)collection.Find(X509FindType.FindByThumbprint, "F85E1C5D93115CA3F969DA3ABC8E0E9547FCCF5A", true);
X509Certificate2 digitalID = collection[0];

//Load existing PDF document.
FileStream documentStream = new FileStream("PDF_Succinctly.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(documentStream);
//Load X509Certificate2.
PdfCertificate certificate = new PdfCertificate(digitalID);

//Create a Revision 2 signature with loaded digital ID.
PdfSignature signature = new PdfSignature(loadedDocument, loadedDocument.Pages[0], certificate, "DigitalSignature");
//Changing the digital signature standard and hashing algorithm.
signature.Settings.CryptographicStandard = CryptographicStandard.CADES;
signature.Settings.DigestAlgorithm = DigestAlgorithm.SHA512;

//Save the PDF document.
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);
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

//Essential PDF supports Digitally sign a PDF document using Windows certificate store only in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms.

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Digital%20Signature/Sign_PDF_Windows_Certificate/).

## Adding a signature validation appearance based on the signature 

You can add the dynamic signature validation appearance to the signature field by enabling the [EnableValidationAppearance](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSignature.html#Syncfusion_Pdf_Security_PdfSignature_EnableValidationAppearance) property available in the [PdfSignature](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSignature.html) class, the appearance will change based on the PDF reader validation. 

Refer to the following code sample.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Creates a new PDF document
PdfDocument document = new PdfDocument();         
//Add a new page
PdfPageBase page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics=page.Graphics;

//Creates a certificate instance from the PFX file with private key         
PdfCertificate pdfCert = new PdfCertificate(@"PDF.pfx", "password123");
//Creates a digital signature
PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");
//Sets an image for the signature field
PdfBitmap signatureImage = new PdfBitmap(@"signature.jpg");
//Sets enable signature validation appearance
signature.EnableValidationAppearance = true;
//Sets signature information
signature.ContactInfo = "johndoe@owned.us";
signature.LocationInfo = "Honolulu, Hawaii";
signature.Reason = "I am author of this document.";
//Draw the signature image  
graphics.DrawImage(signatureImage, 0, 0);
 
//Save and close document
document.Save("Output.pdf");
document.Close( true );

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Creates a new PDF document
Dim document As New PdfDocument()
'Adds a new page
Dim page As PdfPageBase = document.Pages.Add()
'Create PDF graphics for the page
Dim graphics As PdfGraphics = page.Graphics

'Creates a certificate instance from the PFX file with private key
Dim pdfCert As New PdfCertificate("PDF.pfx", "password123")
'Creates a digital signature
Dim signature As New PdfSignature(document, page, pdfCert, "Signature")
'Sets an image for the signature field
Dim signatureImage As New PdfBitmap("signature.jpg")
'Sets enable signature validation appearance    
signature.EnableValidationAppearance = True
'Sets signature info
signature.Bounds = New RectangleF(New PointF(0, 0), signatureImage.PhysicalDimension)
signature.ContactInfo = "johndoe@owned.us"
signature.LocationInfo = "Honolulu, Hawaii"
signature.Reason = "I am author of this document."
'Draws the signature image
graphics.DrawImage(signatureImage, 0, 0)

'Save and close the document
document.Save("Output.pdf")
document.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Creates a new PDF document
PdfDocument document = new PdfDocument();
//Adds a new page
PdfPageBase page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from the PFX file with private key
Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.PDF.pfx");
PdfCertificate pdfCert = new PdfCertificate(certificateStream, "password123");
//Creates a digital signature
PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");
//Sets an image for signature field
Stream imageStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.signature.jpg");
PdfBitmap signatureImage = new PdfBitmap(imageStream);
//Sets enable signature validation appearance
signature.EnableValidationAppearance = true;
//Sets signature information
signature.Bounds = new RectangleF(new PointF(0, 0), signatureImage.PhysicalDimension);
signature.ContactInfo = "johndoe@owned.us";
signature.LocationInfo = "Honolulu, Hawaii";
signature.Reason = "I am author of this document.";
//Draws the signature image
graphics.DrawImage(signatureImage, 0, 0);

//Save the PDF document to stream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream);
//Close the document
document.Close(true);
//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Creates a new PDF document
PdfDocument document = new PdfDocument();
//Adds a new page
PdfPageBase page = document.Pages.Add();
//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from the PFX file with private key
FileStream certificateStream = new FileStream("PDF.pfx", FileMode.Open, FileAccess.Read);
PdfCertificate pdfCert = new PdfCertificate(certificateStream, "password123");
//Creates a digital signature
PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");
//Sets an image for the signature field
FileStream imageStream = new FileStream("signature.jpg", FileMode.Open, FileAccess.Read);
//Sets an image for signature field
PdfBitmap signatureImage = new PdfBitmap(imageStream);
//Sets enable signature validation appearance
signature.EnableValidationAppearance = true;
//Sets signature information
signature.Bounds = new RectangleF(new PointF(0, 0), signatureImage.PhysicalDimension);
signature.ContactInfo = "johndoe@owned.us";
signature.LocationInfo = "Honolulu, Hawaii";
signature.Reason = "I am author of this document.";
//Draws the signature image
graphics.DrawImage(signatureImage, 0, 0);

//Save the document into stream
MemoryStream stream = new MemoryStream();
document.Save(stream);
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

//Creates a new PDF document
PdfDocument document = new PdfDocument();
//Adds a new page
PdfPageBase page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from the PFX file with private key
Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.PDF.pfx");
PdfCertificate pdfCert = new PdfCertificate(certificateStream, "password123");
//Creates a digital signature
PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");
//Sets an image for the signature field
Stream imageStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.signature.jpg");
PdfBitmap signatureImage = new PdfBitmap(imageStream);
//Sets enable signature validation appearance
signature.EnableValidationAppearance = true;
//Sets signature information
signature.Bounds = new RectangleF(new PointF(0, 0), signatureImage.PhysicalDimension);
signature.ContactInfo = "johndoe@owned.us";
signature.LocationInfo = "Honolulu, Hawaii";
signature.Reason = "I am author of this document.";
//Draws the signature image
graphics.DrawImage(signatureImage, 0, 0);

//Save the PDF document to stream
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Close the document
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Digital%20Signature/Adding-a-signature-validation-appearance-in-a-PDF/).

## Adding a timestamp in digital signature

Essential PDF allows you to add timestamp in the digital signature of the PDF document using [TimeStampServer](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSignature.html#Syncfusion_Pdf_Security_PdfSignature_TimeStampServer) property in [PdfSignature](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSignature.html) class. The following code example explains the same.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Creates a new PDF document
PdfDocument document = new PdfDocument();
//Adds a new page
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from PFX file with private key
PdfCertificate pdfCert = new PdfCertificate(@"PDF.pfx", "password123");
//Creates a digital signature
PdfSignature signature = new PdfSignature(page, pdfCert, "Signature");
//Change the digital signature standard and hashing algorithm
signature.Settings.CryptographicStandard = CryptographicStandard.CADES;
signature.Settings.DigestAlgorithm = DigestAlgorithm.SHA512;
//Sets an image for signature field
PdfBitmap image = new PdfBitmap(@"syncfusion_logo.jpeg");
//Adds time stamp by using the server URI and credentials
signature.TimeStampServer = new TimeStampServer(new Uri("http://syncfusion.digistamp.com"), "user", "123456");
//Sets signature info
signature.Bounds = new RectangleF(new PointF(0, 0), image.PhysicalDimension);
signature.ContactInfo = "johndoe@owned.us";
signature.LocationInfo = "Honolulu, Hawaii";
signature.Reason = "I am author of this document.";
//Draws the signature image
graphics.DrawImage(image, 0, 0);

//Save and close the document
document.Save("Output.pdf");
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Creates a new PDF document
Dim document As New PdfDocument()
'Adds a new page
Dim page As PdfPage = document.Pages.Add()
'Create PDF graphics for the page
Dim graphics As PdfGraphics = page.Graphics

'Creates a certificate instance from PFX file with private key
Dim pdfCert As New PdfCertificate("PDF.pfx", "password123")
'Creates a digital signature
Dim signature As New PdfSignature(page, pdfCert, "Signature")
'Sets an image for signature field
Dim image As New PdfBitmap("syncfusion_logo.jpeg")
'Adds time stamp by using the server URI and credentials
signature.TimeStampServer = New TimeStampServer(New Uri("http://syncfusion.digistamp.com"), "user", "123456")
'Sets signature info
signature.Bounds = New RectangleF(New PointF(0, 0), image.PhysicalDimension)
signature.ContactInfo = "johndoe@owned.us"
signature.LocationInfo = "Honolulu, Hawaii"
signature.Reason = "I am author of this document."
'Draws the signature image
graphics.DrawImage(image, 0, 0)

'Save and close the document
document.Save("Output.pdf")
document.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Creates a new PDF document
PdfDocument document = new PdfDocument();
//Adds a new page
PdfPageBase page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from PFX file with private key
Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.PDF.pfx");
PdfCertificate pdfCert = new PdfCertificate(certificateStream, "password123");
//Creates a digital signature
PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");
//Sets an image for signature field
Stream imageStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.syncfusion_logo.jpeg");
PdfBitmap image = new PdfBitmap(imageStream);
//Adds time stamp by using the server URI and credentials
signature.TimeStampServer = new TimeStampServer(new Uri("http://syncfusion.digistamp.com"), "user", "123456");
//Sets signature info
signature.Bounds = new RectangleF(new PointF(0, 0), image.PhysicalDimension);
signature.ContactInfo = "johndoe@owned.us";
signature.LocationInfo = "Honolulu, Hawaii";
signature.Reason = "I am author of this document.";
//Draws the signature image
graphics.DrawImage(image, 0, 0);

//Save the PDF document to stream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream);
//Close the document
document.Close(true);
//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples
Save(stream, "output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Creates a new PDF document
PdfDocument document = new PdfDocument();
//Adds a new page
PdfPageBase page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from PFX file with private key
FileStream certificateStream = new FileStream("PDF.pfx", FileMode.Open, FileAccess.Read);
PdfCertificate pdfCert = new PdfCertificate(certificateStream, "password123");
//Creates a digital signature
PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");
//Sets an image for signature field
FileStream imageStream = new FileStream("syncfusion_logo.jpeg", FileMode.Open, FileAccess.Read);
//Sets an image for signature field
PdfBitmap image = new PdfBitmap(imageStream);
//Adds time stamp by using the server URI and credentials
signature.TimeStampServer = new TimeStampServer(new Uri("http://syncfusion.digistamp.com"), "user", "123456");
//Sets signature info
signature.Bounds = new RectangleF(new PointF(0, 0), image.PhysicalDimension);
signature.ContactInfo = "johndoe@owned.us";
signature.LocationInfo = "Honolulu, Hawaii";
signature.Reason = "I am author of this document.";
//Draws the signature image
graphics.DrawImage(image, 0, 0);

//Save the document into stream
MemoryStream stream = new MemoryStream();
document.Save(stream);
stream.Position = 0;
//Close the document
document.Close(true);
//Defining the ContentType for pdf file
string contentType = "application/pdf";
//Define the file name
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Creates a new PDF document
PdfDocument document = new PdfDocument();
//Adds a new page
PdfPageBase page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from PFX file with private key
Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.PDF.pfx");
PdfCertificate pdfCert = new PdfCertificate(certificateStream, "password123");
//Creates a digital signature
PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");
//Sets an image for signature field
Stream imageStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.syncfusion_logo.jpeg");
PdfBitmap image = new PdfBitmap(imageStream);
//Adds time stamp by using the server URI and credentials
signature.TimeStampServer = new TimeStampServer(new Uri("http://syncfusion.digistamp.com"), "user", "123456");
//Sets signature info
signature.Bounds = new RectangleF(new PointF(0, 0), image.PhysicalDimension);
signature.ContactInfo = "johndoe@owned.us";
signature.LocationInfo = "Honolulu, Hawaii";
signature.Reason = "I am author of this document.";
//Draws the signature image
graphics.DrawImage(image, 0, 0);

//Save the PDF document to stream
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Close the document
document.Close(true);
//Save the stream into PDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("sample.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("sample.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Digital%20Signature/Adding-a-timestamp-in-digital-signature-of-PDF/).

## Adding a timestamp to PDF document

You can add timestamp to the PDF document using [TimeStampServer](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSignature.html#Syncfusion_Pdf_Security_PdfSignature_TimeStampServer) property in [PdfSignature](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSignature.html) class. The following code example explains the same.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Create a new PDF document
PdfDocument document = new PdfDocument();
//Add a new page
PdfPage page = document.Pages.Add();

//Creates a digital signature
PdfSignature signature = new PdfSignature(page, "Signature");
//Add the time stamp by using the server URI
signature.TimeStampServer = new TimeStampServer(new Uri("http://syncfusion.digistamp.com"), "user", "123456");

//Save and close the document
document.Save("Output.pdf");
document.Close(true);  

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Creates a new PDF document
Dim document As New PdfDocument()
'Adds a new page
Dim page As PdfPage = document.Pages.Add()

'Creates a digital signature
Dim signature As New PdfSignature(page, "Signature")
'Adds time stamp by using the server URI
signature.TimeStampServer = New TimeStampServer(New Uri("http://syncfusion.digistamp.com"), "user", "123456")

'Save and close the document
document.Save("Output.pdf")
document.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Create a new document
PdfDocument document = new PdfDocument();
//Adds a new page
PdfPage page = document.Pages.Add();        

//Creates a digital signature
PdfSignature signature = new PdfSignature(page, "Signature");
//Add the time stamp by using the server URI
signature.TimeStampServer = new TimeStampServer(new Uri("http://syncfusion.digistamp.com"), "user", "123456");

//Save the PDF document to strea
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream);
//Close the document
document.Close(true);
//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a new pdf document
PdfDocument document = new PdfDocument();
//Adds a new page
PdfPage page = document.Pages.Add();

//Creates a digital signature
PdfSignature signature = new PdfSignature(page, "Signature");
//Add the time stamp by using the server URI
signature.TimeStampServer = new TimeStampServer(new Uri("http://syncfusion.digistamp.com"), "user", "123456");

//Save the document into stream
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);
stream.Position = 0;
//Close the document
loadedDocument.Close(true);
//Defining the ContentType for pdf file
string contentType = "application/pdf";
//Define the file name
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Create a new PDF document
PdfDocument document = new PdfDocument();            
//Add a page to the document
PdfPage page = document.Pages.Add();

//Creates a digital signature
PdfSignature signature = new PdfSignature(page, "Signature");
//Add the time stamp by using the server URI
signature.TimeStampServer = new TimeStampServer(new Uri("http://syncfusion.digistamp.com"), "user", "123456");

//Save the document into stream
MemoryStream memoryStream = new MemoryStream();
document.Save(memoryStream);
//Save the stream into PDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", memoryStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", memoryStream);
}

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Digital%20Signature/Adding-a-timestamp-to-PDF-document/).

## Adding a timestamp to existing PDF document

You can add timestamp to the existing PDF document using [TimeStampServer](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSignature.html#Syncfusion_Pdf_Security_PdfSignature_TimeStampServer) property in [PdfSignature](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSignature.html) class. The following code example explains the same.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Load the existing PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");
//Add a new page
PdfLoadedPage page = loadedDocument.Pages[0] as PdfLoadedPage;

//Creates a digital signature
PdfSignature signature = new PdfSignature(page, "Signature");
//Add the time stamp by using the server URI
signature.TimeStampServer = new TimeStampServer(new Uri("http://syncfusion.digistamp.com"), "user", "123456");

//Save the PDF document
loadedDocument.Save("Output.pdf");
//Close the document
loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Load the PDF document
Dim document As New PdfLoadedDocument("Input.pdf")
'Gets the first page of the document
Dim page As PdfLoadedPage = TryCast(document.Pages(0), PdfLoadedPage)

'Creates a digital signature
Dim signature As New PdfSignature(page, "Signature")
'Adds time stamp by using the server URI
signature.TimeStampServer = New TimeStampServer(New Uri("http://syncfusion.digistamp.com"), "user", "123456")

'Save and close the document
document.Save("Output.pdf")
document.Close(True)

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
//Gets the first page of the document
PdfLoadedPage page = loadedDocument.Pages[0] as PdfLoadedPage;

//Creates a digital signature
PdfSignature signature = new PdfSignature(page, "Signature");
//Add the time stamp by using the server URI
signature.TimeStampServer = new TimeStampServer(new Uri("http://syncfusion.digistamp.com"), "user", "123456");

//Save the document into stream
MemoryStream stream = new MemoryStream();
await loadedDocument.SaveAsync(stream);
//Close the document
loadedDocument.Close(true);
//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load the PDF document
FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);
//Gets the page
PdfLoadedPage page = loadedDocument.Pages[0] as PdfLoadedPage;

//Creates a digital signature
PdfSignature signature = new PdfSignature(page, "Signature");
//Add the time stamp by using the server URI
signature.TimeStampServer = new TimeStampServer(new Uri("http://syncfusion.digistamp.com"), "user", "123456");

//Save the document into stream
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);
stream.Position = 0;
//Close the document
loadedDocument.Close(true);
//Defining the ContentType for pdf file
string contentType = "application/pdf";
//Define the file name
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Load the file as stream
Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf ");
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);  
//Gets the page
PdfLoadedPage page = loadedDocument.Pages[0] as PdfLoadedPage;

//Creates a digital signature
PdfSignature signature = new PdfSignature(page, "Signature");
//Add the time stamp by using the server URI
signature.TimeStampServer = new TimeStampServer(new Uri("http://syncfusion.digistamp.com"), "user", "123456")

//Save the PDF document to stream
MemoryStream memoryStream = new MemoryStream();
loadedDocument.Save(memoryStream);
//Closes the document
loadedDocument.Close(true);
//Save the stream into PDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", memoryStream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", memoryStream);
}

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Digital%20Signature/Adding-a-timestamp-to-an-existing-PDF/).

## Retrieve certificate details from an existing signed PDF document

The Essential PDF provides support to get the certificate details from an existing signed PDF document such as,

* [Signed date](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSignature.html#Syncfusion_Pdf_Security_PdfSignature_SignedDate)
* Expiry date
* [Signed name](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSignature.html#Syncfusion_Pdf_Security_PdfSignature_SignedName)
* [Subject name](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSignature.html#Syncfusion_Pdf_Security_PdfSignature_SignedName)
* [Issuer name](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfCertificate.html#Syncfusion_Pdf_Security_PdfCertificate_IssuerName)
* Certificate distinguished names (country, state, street, email, organization, organization unit, locality, and more).

You can get the above certificate details from an existing signed PDF document using [ValidFrom](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfCertificate.html#Syncfusion_Pdf_Security_PdfCertificate_ValidFrom) and [ValidTo](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfCertificate.html#Syncfusion_Pdf_Security_PdfCertificate_ValidTo) property.The following code example explains the same.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Load the existing signed PDF
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("SignedDocument.pdf");
//Load the PDF form
PdfLoadedForm loadedForm = loadedDocument.Form as PdfLoadedForm;
//Get the signature field
PdfLoadedSignatureField signatureField = loadedForm.Fields[0] as PdfLoadedSignatureField;

//Get the certificate
PdfCertificate certificate = signatureField.Signature.Certificate;
//Get the signed date
DateTime date = signatureField.Signature.SignedDate;
//Get the signed name
string name = signatureField.Signature.SignedName;
//Get the certificate names based on their distinguished name.
string subjectName = certificate.SubjectName
string subjectCountry = certificate.GetValue(PdfCertificateDistinguishedName.Country, PdfCertificateField.Subject);
string subjectOrganization = certificate.GetValue(PdfCertificateDistinguishedName.Organization, PdfCertificateField.Subject);
//Issuer details
string issuerName = certificate.IssuerName;
string issuerOrganization = certificate.GetValue(PdfCertificateDistinguishedName.Organization, PdfCertificateField.Issuer);
string issuerCountry = certificate.GetValue(PdfCertificateDistinguishedName.Country, PdfCertificateField.Issuer);
//Get certificate validation date information
DateTime validFrom = certificate.ValidFrom;
DateTime validTo = certificate.ValidTo;

//Close the document
loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Load the existing signed PDF
Dim loadedDocument As PdfLoadedDocument = New PdfLoadedDocument("../../Signed.pdf")
'Load the PDF form
Dim loadedForm As PdfLoadedForm = TryCast(loadedDocument.Form, PdfLoadedForm)
'Get the signature field
Dim signatureField As PdfLoadedSignatureField = TryCast(loadedForm.Fields(0), PdfLoadedSignatureField)

'Get the certificate
Dim certificate As PdfCertificate = signatureField.Signature.Certificate
'Get the signed date
Dim signedDate As DateTime = signatureField.Signature.SignedDate
'Get the signed name
Dim name As String = signatureField.Signature.SignedName
'Get the certificate names based on their distinguished name
Dim subjectName As String = certificate.SubjectName
Dim subjectCountry As String = certificate.GetValue(PdfCertificateDistinguishedName.Country, PdfCertificateField.Subject)
Dim subjectOrganization As String = certificate.GetValue(PdfCertificateDistinguishedName.Organization, PdfCertificateField.Subject)
'Issuer details
Dim issuerName As String = certificate.IssuerName
Dim issuerOrganization As String = certificate.GetValue(PdfCertificateDistinguishedName.Organization, PdfCertificateField.Issuer)
Dim issuerCountry As String = certificate.GetValue(PdfCertificateDistinguishedName.Country, PdfCertificateField.Issuer)
'Get certificate validation date information
Dim validFrom As DateTime = certificate.ValidFrom
Dim validTo As DateTime = certificate.ValidTo

'Close the PDF document
loadedDocument.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Essential PDF supports retrieving certificate details from signed PDF document only in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms.

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load the PDF document
FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);
//Get the signature field
PdfLoadedSignatureField signatureField = loadedDocument.Form.Fields[0] as PdfLoadedSignatureField;

//Get the certificate
PdfCertificate certificate = signatureField.Signature.Certificate;
//Get the signed date
DateTime date = signatureField.Signature.SignedDate;
//Get the signed name
string name = signatureField.Signature.SignedName;
//Gets the certificate subject's name
string subjectName = certificate.SubjectName;
//Gets the certificate issuer's name
string issuerName = certificate.IssuerName;
//Get certificate validation date information
DateTime validFrom = certificate.ValidFrom;
DateTime validTo = certificate.ValidTo;

//Close the document
loadedDocument.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Essential PDF supports retrieving certificate details from signed PDF document only in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms.

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Digital%20Signature/Retrieve-certificate-details-from-an-existing-PDF/).

## Enable Long Term Validation (LTV) PDF signature

The Essential PDF supports creating long term signature validation when signing the PDF document. The LTV signature allows you to check the validity of a signature long after the document was signed. To achieve long term validation, all the required elements for signature validation must be embedded in the signed PDF.

N> The resulted PDF document size will be large since all the necessary signature information, Certificate Revocation List (CRL), and Online Certificate Status Protocol (OCSP) are embedded.

The following code example explains how to create LTV PDF using [EnableLtv](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSignature.html#Syncfusion_Pdf_Security_PdfSignature_EnableLtv) property in [PdfSignature](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSignature.html) class when signing the PDF document.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Creates a new PDF document
PdfDocument document = new PdfDocument();
//Adds a new page
PdfPage page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from PFX file with private key
PdfCertificate pdfCert = new PdfCertificate(@"PDF.pfx", "password123");
//Creates a digital signature
PdfSignature signature = new PdfSignature(page, pdfCert, "Signature");
signature.Settings.CryptographicStandard = CryptographicStandard.CADES;
signature.Settings.DigestAlgorithm = DigestAlgorithm.SHA256;
//Sets an image for signature field
PdfBitmap image = new PdfBitmap(@"syncfusion_logo.jpeg");
//Adds time stamp by using the server URI and credentials
signature.TimeStampServer = new TimeStampServer(new Uri("http://syncfusion.digistamp.com"), "user", "123456");
//Enable LTV on Signature
signature.EnableLtv = true;
//Sets signature info 
signature.Bounds = new RectangleF(new PointF(0, 0), image.PhysicalDimension);
signature.ContactInfo = "johndoe@owned.us";
signature.LocationInfo = "Honolulu, Hawaii";
signature.Reason = "I am author of this document.";
//Draws the signature image
graphics.DrawImage(image, 0, 0);

//Save and close the document
document.Save("Output.pdf");
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Creates a new PDF document
Dim document As New PdfDocument()
'Adds a new page
Dim page As PdfPage = document.Pages.Add()
'Create PDF graphics for the page
Dim graphics As PdfGraphics = page.Graphics

'Creates a certificate instance from PFX file with private key
Dim pdfCert As New PdfCertificate("PDF.pfx", "password123")
'Creates a digital signature
Dim signature As New PdfSignature(page, pdfCert, "Signature")
'Sets an image for signature field
Dim image As New PdfBitmap("syncfusion_logo.jpeg")
'Adds time stamp by using the server URI and credentials
signature.TimeStampServer = New TimeStampServer(New Uri("http://syncfusion.digistamp.com"), "user", "123456")
'Enable LTV on Signature
signature.EnableLtv = True
'Sets signature info
signature.Bounds = New RectangleF(New PointF(0, 0), image.PhysicalDimension)
signature.ContactInfo = "johndoe@owned.us"
signature.LocationInfo = "Honolulu, Hawaii"
signature.Reason = "I am author of this document."
'Draws the signature image
graphics.DrawImage(image, 0, 0)

'Save and close the document
document.Save("Output.pdf")
document.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Creates a new PDF document
PdfDocument document = new PdfDocument();
//Adds a new page
PdfPageBase page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from PFX file with private key
Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.PDF.pfx");
PdfCertificate pdfCert = new PdfCertificate(certificateStream, "password123");
//Creates a digital signature
PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");
//Sets an image for signature field
Stream imageStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.syncfusion_logo.jpeg");
PdfBitmap image = new PdfBitmap(imageStream);
//Adds time stamp by using the server URI and credentials
signature.TimeStampServer = new TimeStampServer(new Uri("http://syncfusion.digistamp.com"), "user", "123456");
//Enable LTV on Signature
signature.EnableLtv = true;
//Sets signature info
signature.Bounds = new RectangleF(new PointF(0, 0), image.PhysicalDimension);
signature.ContactInfo = "johndoe@owned.us";
signature.LocationInfo = "Honolulu, Hawaii";
signature.Reason = "I am author of this document.";
//Draws the signature image
graphics.DrawImage(image, 0, 0);

//Save the PDF document to stream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream);
//Close the document
document.Close(true);
//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples
Save(stream, "output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Creates a new PDF document
PdfDocument document = new PdfDocument();
//Adds a new page
PdfPageBase page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from PFX file with private key
FileStream certificateStream = new FileStream("PDF.pfx", FileMode.Open, FileAccess.Read);
PdfCertificate pdfCert = new PdfCertificate(certificateStream, "password123");
//Creates a digital signature
PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");
//Sets an image for signature field
FileStream imageStream = new FileStream("syncfusion_logo.jpeg", FileMode.Open, FileAccess.Read);
//Sets an image for signature field
PdfBitmap image = new PdfBitmap(imageStream);
//Adds time stamp by using the server URI and credentials
signature.TimeStampServer = new TimeStampServer(new Uri("http://syncfusion.digistamp.com"), "user", "123456");
//Enable LTV on Signature
signature.EnableLtv = true;
//Sets signature info
signature.Bounds = new RectangleF(new PointF(0, 0), image.PhysicalDimension);
signature.ContactInfo = "johndoe@owned.us";
signature.LocationInfo = "Honolulu, Hawaii";
signature.Reason = "I am author of this document.";
//Draws the signature image
graphics.DrawImage(image, 0, 0);

//Save the document into stream
MemoryStream stream = new MemoryStream();
document.Save(stream);
stream.Position = 0;
//Close the document
document.Close(true);
//Defining the ContentType for pdf file
string contentType = "application/pdf";
//Define the file name
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Creates a new PDF document
PdfDocument document = new PdfDocument();
//Adds a new page
PdfPageBase page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from PFX file with private key
Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.PDF.pfx");
PdfCertificate pdfCert = new PdfCertificate(certificateStream, "password123");
//Creates a digital signature
PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");
//Sets an image for signature field
Stream imageStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.syncfusion_logo.jpeg");
PdfBitmap image = new PdfBitmap(imageStream);
//Adds time stamp by using the server URI and credentials
signature.TimeStampServer = new TimeStampServer(new Uri("http://syncfusion.digistamp.com"), "user", "123456");
//Enable LTV on Signature
signature.EnableLtv = true;
//Sets signature info
signature.Bounds = new RectangleF(new PointF(0, 0), image.PhysicalDimension);
signature.ContactInfo = "johndoe@owned.us";
signature.LocationInfo = "Honolulu, Hawaii";
signature.Reason = "I am author of this document.";
//Draws the signature image
graphics.DrawImage(image, 0, 0);

//Save the PDF document to stream
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Close the document
document.Close(true);
//Save the stream into PDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("output.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Digital%20Signature/Enable-LTV-PDF-signature/).

## Adding a digital signature with customization

The [PdfSignatureSettings](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSignatureSettings.html) allows you to add customized digital signatures to the PDF document.

### Adding a digital signature with CAdES format

As per the PDF specification 2.0, now Syncfusion PDF library supports digital signature based on CAdES (CMS Advanced Electronics Signature). The CAdES based digital signature can remain valid for long periods, even if underlying cryptographic algorithms are broken. Using the API [CryptographicStandard](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSignatureSettings.html#Syncfusion_Pdf_Security_PdfSignatureSettings_CryptographicStandard), you can change the standard between CMS (Cryptographic Message Syntax) and CAdES.

The following code example explains how to add a digital signature with [cryptographic standard](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSignatureSettings.html#Syncfusion_Pdf_Security_PdfSignatureSettings_CryptographicStandard) as CAdES through [CryptographicStandard](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.CryptographicStandard.html) Enum when creating the PDF document.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Creates a new PDF document
PdfDocument document = new PdfDocument();
//Adds a new page
PdfPageBase page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from PFX file with private key
PdfCertificate pdfCert = new PdfCertificate(@"PDF.pfx", "password123");
//Creates a digital signature
PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");
//Sets signature settings to customize cryptographic standard specified
PdfSignatureSettings settings = signature.Settings;
settings.CryptographicStandard  = CryptographicStandard.CADES;

//Sets an image for signature field
PdfBitmap signatureImage = new PdfBitmap(@"signature.jpg");
//Sets signature information
signature.Bounds = new RectangleF(new PointF(0, 0), signatureImage.PhysicalDimension);
signature.ContactInfo = "johndoe@owned.us";
signature.LocationInfo = "Honolulu, Hawaii";
signature.Reason = "I am author of this document.";
//Draws the signature image
graphics.DrawImage(signatureImage, 0, 0);

//Save and close the document
document.Save("Output.pdf");
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Creates a new PDF document
Dim document As New PdfDocument()
'Adds a new page
Dim page As PdfPageBase = document.Pages.Add()
'Create PDF graphics for the page
Dim graphics As PdfGraphics = page.Graphics

'Creates a certificate instance from PFX file with private key
Dim pdfCert As New PdfCertificate("PDF.pfx", "password123")
'Creates a digital signature
Dim signature As New PdfSignature(document, page, pdfCert, "Signature")
'Sets signature settings to customize cryptographic standard specified
Dim settings As PdfSignatureSettings = signature.Settings
settings.CryptographicStandard  = CryptographicStandard.CADES

'Sets an image for signature field
Dim signatureImage As New PdfBitmap("signature.jpg")
'Sets signature info
signature.Bounds = New RectangleF(New PointF(0, 0), signatureImage.PhysicalDimension)
signature.ContactInfo = "johndoe@owned.us"
signature.LocationInfo = "Honolulu, Hawaii"
signature.Reason = "I am author of this document."
'Draws the signature image
graphics.DrawImage(signatureImage, 0, 0)

'Save and close the document
document.Save("Output.pdf")
document.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Creates a new PDF document
PdfDocument document = new PdfDocument();
//Adds a new page
PdfPageBase page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from PFX file with private key
Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.PDF.pfx");
PdfCertificate pdfCert = new PdfCertificate(certificateStream, "password123");
//Creates a digital signature
PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");
//Sets signature settings to customize cryptographic standard specified
PdfSignatureSettings settings = signature.Settings;
settings.CryptographicStandard  = CryptographicStandard.CADES;

//Sets an image for signature field
Stream imageStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.signature.jpg");
PdfBitmap signatureImage = new PdfBitmap(imageStream);
//Sets signature information
signature.Bounds = new RectangleF(new PointF(0, 0), signatureImage.PhysicalDimension);
signature.ContactInfo = "johndoe@owned.us";
signature.LocationInfo = "Honolulu, Hawaii";
signature.Reason = "I am author of this document.";
//Draws the signature image
graphics.DrawImage(signatureImage, 0, 0);

//Save the PDF document to stream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream);
//Close the document
document.Close(true);                                                                   
//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a new PDF document
PdfDocument document = new PdfDocument();
//Add a new page
PdfPageBase page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from PFX file with private key
FileStream certificateStream = new FileStream("PDF.pfx", FileMode.Open, FileAccess.Read);
PdfCertificate pdfCert = new PdfCertificate(certificateStream, "password123");
//Creates a digital signature
PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");
//Sets signature settings to customize cryptographic standard specified
PdfSignatureSettings settings = signature.Settings;
settings.CryptographicStandard  = CryptographicStandard.CADES;

//Sets an image for signature field
FileStream imageStream = new FileStream("signature.jpg", FileMode.Open, FileAccess.Read);
//Sets an image for signature field
PdfBitmap signatureImage = new PdfBitmap(imageStream);
//Sets signature information
signature.Bounds = new RectangleF(new PointF(0, 0), signatureImage.PhysicalDimension);
signature.ContactInfo = "johndoe@owned.us";
signature.LocationInfo = "Honolulu, Hawaii";
signature.Reason = "I am author of this document.";
//Draws the signature image
graphics.DrawImage(signatureImage, 0, 0);

//Save the document into stream
MemoryStream stream = new MemoryStream();
document.Save(stream);
stream.Position = 0;
//Close the document
document.Close(true);
//Defining the ContentType for pdf file
string contentType = "application/pdf";
//Define the file name
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Create a new PDF document
PdfDocument document = new PdfDocument();
//Add a new page
PdfPageBase page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from PFX file with private key
Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.PDF.pfx");
PdfCertificate pdfCert = new PdfCertificate(certificateStream, "password123");
//Creates a digital signature
PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");
//Sets signature settings to customize cryptographic standard specified
PdfSignatureSettings settings = signature.Settings;
settings.CryptographicStandard  = CryptographicStandard.CADES;

//Sets an image for signature field
Stream imageStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.signature.jpg");
PdfBitmap signatureImage = new PdfBitmap(imageStream);
//Sets signature information
signature.Bounds = new RectangleF(new PointF(0, 0), signatureImage.PhysicalDimension);
signature.ContactInfo = "johndoe@owned.us";
signature.LocationInfo = "Honolulu, Hawaii";
signature.Reason = "I am author of this document.";
//Draws the signature image
graphics.DrawImage(signatureImage, 0, 0);

//Save the PDF document to stream
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Close the document
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Digital%20Signature/Adding-a-digital-signature-with-CAdES-format/).

### Customize digestion algorithm

In addition, you can now set the different message digest algorithm to sign PDF document using the [DigestAlgorithm](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSignatureSettings.html#Syncfusion_Pdf_Security_PdfSignatureSettings_DigestAlgorithm) enum available in the class [PdfSignatureSettings](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSignatureSettings.html). 

The following message digest algorithms are now supported:
* SHA1
* SHA256
* SHA384
* SHA512
* RIPEMD160

The following code example explains how to add a digital signature with various digest algorithms to the PDF document by specifying the [DigestAlgorithm](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSignatureSettings.html#Syncfusion_Pdf_Security_PdfSignatureSettings_DigestAlgorithm) property as **SHA256** through [DigestAlgorithm](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.DigestAlgorithm.html) enum in [PdfSignatureSettings](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSignatureSettings.html) class.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Create a new PDF document
PdfDocument document = new PdfDocument();
//Add a new page
PdfPageBase page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from PFX file with private key
PdfCertificate pdfCert = new PdfCertificate(@"PDF.pfx", "password123");
//Creates a digital signature
PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");
//Sets signature settings to customize digest algorithm specified
PdfSignatureSettings settings = signature.Settings;
settings.DigestAlgorithm = DigestAlgorithm.SHA256;

//Sets an image for signature field
PdfBitmap signatureImage = new PdfBitmap(@"signature.jpg");
//Sets signature information
signature.Bounds = new RectangleF(new PointF(0, 0), signatureImage.PhysicalDimension);
signature.ContactInfo = "johndoe@owned.us";
signature.LocationInfo = "Honolulu, Hawaii";
signature.Reason = "I am author of this document.";
//Draws the signature image
graphics.DrawImage(signatureImage, 0, 0);

//Save and close the document
document.Save("Output.pdf");
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Creates a new PDF document
Dim document As New PdfDocument()
'Adds a new page
Dim page As PdfPageBase = document.Pages.Add()
'Create PDF graphics for the page
Dim graphics As PdfGraphics = page.Graphics

'Creates a certificate instance from PFX file with private key
Dim pdfCert As New PdfCertificate("PDF.pfx", "password123")
'Creates a digital signature
Dim signature As New PdfSignature(document, page, pdfCert, "Signature")
'Sets signature settings to customize digest algorithm specified
Dim settings As PdfSignatureSettings = signature.Settings
settings.DigestAlgorithm = DigestAlgorithm.SHA256

'Sets an image for signature field
Dim signatureImage As New PdfBitmap("signature.jpg")
'Sets signature info
signature.Bounds = New RectangleF(New PointF(0, 0), signatureImage.PhysicalDimension)
signature.ContactInfo = "johndoe@owned.us"
signature.LocationInfo = "Honolulu, Hawaii"
signature.Reason = "I am author of this document."
'Draws the signature image
graphics.DrawImage(signatureImage, 0, 0)

'Save and close the document
document.Save("Output.pdf")
document.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Creates a new PDF document
PdfDocument document = new PdfDocument();
//Adds a new page
PdfPageBase page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from PFX file with private key
Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.PDF.pfx");
PdfCertificate pdfCert = new PdfCertificate(certificateStream, "password123");
//Creates a digital signature
PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");
//Sets signature settings to customize digest algorithm specified
PdfSignatureSettings settings = signature.Settings;
settings.DigestAlgorithm = DigestAlgorithm.SHA256;

//Sets an image for signature field
Stream imageStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.signature.jpg");
PdfBitmap signatureImage = new PdfBitmap(imageStream);
//Sets signature information
signature.Bounds = new RectangleF(new PointF(0, 0), signatureImage.PhysicalDimension);
signature.ContactInfo = "johndoe@owned.us";
signature.LocationInfo = "Honolulu, Hawaii";
signature.Reason = "I am author of this document.";
//Draws the signature image
graphics.DrawImage(signatureImage, 0, 0);

//Save the PDF document to stream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream);
//Close the document
document.Close(true);                                                                   
//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a new PDF document
PdfDocument document = new PdfDocument();
//Add a new page
PdfPageBase page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from PFX file with private key
FileStream certificateStream = new FileStream("PDF.pfx", FileMode.Open, FileAccess.Read);
PdfCertificate pdfCert = new PdfCertificate(certificateStream, "password123");
//Creates a digital signature
PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");
//Sets signature settings to customize digest algorithm specified
PdfSignatureSettings settings = signature.Settings;
settings.DigestAlgorithm = DigestAlgorithm.SHA256;

//Sets an image for signature field
FileStream imageStream = new FileStream("signature.jpg", FileMode.Open, FileAccess.Read);
//Sets an image for signature field
PdfBitmap signatureImage = new PdfBitmap(imageStream);
//Sets signature information
signature.Bounds = new RectangleF(new PointF(0, 0), signatureImage.PhysicalDimension);
signature.ContactInfo = "johndoe@owned.us";
signature.LocationInfo = "Honolulu, Hawaii";
signature.Reason = "I am author of this document.";
//Draws the signature image
graphics.DrawImage(signatureImage, 0, 0);

//Save the document into stream
MemoryStream stream = new MemoryStream();
document.Save(stream);
stream.Position = 0;
//Close the document
document.Close(true);
//Defining the ContentType for pdf file
string contentType = "application/pdf";
//Define the file name
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Create a new PDF document
PdfDocument document = new PdfDocument();
//Add a new page
PdfPageBase page = document.Pages.Add();
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from PFX file with private key
Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.PDF.pfx");
PdfCertificate pdfCert = new PdfCertificate(certificateStream, "password123");
//Creates a digital signature
PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");
//Sets signature settings to customize digest algorithm specified
PdfSignatureSettings settings = signature.Settings;
settings.DigestAlgorithm = DigestAlgorithm.SHA256;

//Sets an image for signature field
Stream imageStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.signature.jpg");
PdfBitmap signatureImage = new PdfBitmap(imageStream);
//Sets signature information
signature.Bounds = new RectangleF(new PointF(0, 0), signatureImage.PhysicalDimension);
signature.ContactInfo = "johndoe@owned.us";
signature.LocationInfo = "Honolulu, Hawaii";
signature.Reason = "I am author of this document.";
//Draws the signature image
graphics.DrawImage(signatureImage, 0, 0);

//Save the PDF document to stream
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Close the document
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Digital%20Signature/Add-digital-signature-with-digest-algorithm/).

## Digital signature validation

Added the support to validate the digital signatures in an existing PDF document. Digital signature validation covers the following steps to ensure the validity of the signatures:

* Validate the document modification.
* Validate the certificate chain.
* Ensure the signature with timestamp time.
* Check the revocation status of the certificate with OCSP and CRL.
* Ensure the multiple digital signatures.

You can use the [ValidateSignature](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedSignatureField.html#Syncfusion_Pdf_Parsing_PdfLoadedSignatureField_ValidateSignature) method available in the [PdfLoadedSignatureField](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedSignatureField.html) class to validate the digital signature. 

You can get the overall status from the [IsSignatureValid](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSignatureValidationResult.html#Syncfusion_Pdf_Security_PdfSignatureValidationResult_IsSignatureValid) property available in the [PdfSignatureValidationResult](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSignatureValidationResult.html) class.

The following code example explains how to validate the digitally signed PDF document signature.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Load an existing signed PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");
//Get signature field
PdfLoadedSignatureField signatureField = loadedDocument.Form.Fields[0] as PdfLoadedSignatureField;

//X509Certificate2Collection to check the signer's identity using root certificates
X509CertificateCollection collection = new X509CertificateCollection();
//Create new X509Certificate2 with the root certificate
X509Certificate2 certificate = new X509Certificate2("PDF.pfx", "password123");
//Add the certificate to the collection
collection.Add(certificate);

//Validate signature and get the validation result
PdfSignatureValidationResult result = signatureField.ValidateSignature(collection);
//Checks whether the signature is valid or not
SignatureStatus status = result.SignatureStatus;
//Checks whether the document is modified or not
bool isModified = result.IsDocumentModified;
//Signature details
string issuerName = signatureField.Signature.Certificate.IssuerName;
DateTime validFrom = signatureField.Signature.Certificate.ValidFrom;
DateTime validTo = signatureField.Signature.Certificate.ValidTo;
string signatureAlgorithm = result.SignatureAlgorithm;
DigestAlgorithm digestAlgorithm = result.DigestAlgorithm;
//Revocation validation details
RevocationResult revocationDetails = result.RevocationResult;
RevocationStatus revocationStatus = revocationDetails.OcspRevocationStatus;
bool isRevokedCRL = revocationDetails.IsRevokedCRL;

//Close the document
loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Load an existing signed PDF document
Dim loadedDocument As PdfLoadedDocument = New PdfLoadedDocument("Input.pdf")
'Get signature field
Dim signatureField As PdfLoadedSignatureField = loadedDocument.Form.Fields[0] As PdfLoadedSignatureField

'X509Certificate2Collection to check the signer's identity using root certificates
Dim collection As X509CertificateCollection = New X509CertificateCollection()
'Create new X509Certificate2 with the root certificate
Dim certificate As X509Certificate2 = New X509Certificate2("PDF.pfx", "password123")
'Add the certificate to the collection
collection.Add(certificate)

'Validate signature and get the validation result
Dim result As PdfSignatureValidationResult = signatureField.ValidateSignature(collection)
'Checks whether the signature is valid or not
Dim status As SignatureStatus = result.SignatureStatus
'Checks whether the document is modified or not
Dim isModified As Boolean = result.IsDocumentModified
'Signature details
Dim issuerName As String = signatureField.Signature.Certificate.IssuerName
Dim validFrom As DateTime = signatureField.Signature.Certificate.ValidFrom
Dim validTo As DateTime = signatureField.Signature.Certificate.ValidTo
Dim signatureAlgorithm As String = result.SignatureAlgorithm
Dim digestAlgorithm As DigestAlgorithm = result.DigestAlgorithm
'Revocation validation details
Dim revocationDetails As RevocationResult = result.RevocationResult
Dim revocationStatus As RevocationStatus = revocationDetails.OcspRevocationStatus
Dim isRevokedCRL As Boolean = revocationDetails.IsRevokedCRL

'Close the document
loadedDocument.Close(true)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Get the stream from the document
Stream documentStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Input.pdf");
//Load an existing signed PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(documentStream);
//Get signature field
PdfLoadedSignatureField signatureField = loadedDocument.Form.Fields[0] as PdfLoadedSignatureField;

//X509Certificate2Collection to check the signer's identity using root certificates
X509CertificateCollection collection = new X509CertificateCollection();
//Creates a certificate instance from PFX file with private key
Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.PDF.pfx");
byte[] data = new byte[certificateStream.Length];
certificateStream.Read(data, 0, data.Length);
//Create new X509Certificate2 with the root certificate
X509Certificate2 certificate = new X509Certificate2(data, "password123");
//Add the certificate to the collection
collection.Add(certificate);

//Validate signature and get the validation result
PdfSignatureValidationResult result = signatureField.ValidateSignature(collection);
//Checks whether the signature is valid or not
SignatureStatus status = result.SignatureStatus;
//Checks whether the document is modified or not
bool isModified = result.IsDocumentModified;
//Signature details
string issuerName = signatureField.Signature.Certificate.IssuerName;
DateTime validFrom = signatureField.Signature.Certificate.ValidFrom;
DateTime validTo = signatureField.Signature.Certificate.ValidTo;
string signatureAlgorithm = result.SignatureAlgorithm;
DigestAlgorithm digestAlgorithm = result.DigestAlgorithm;
//Revocation validation details
RevocationResult revocationDetails = result.RevocationResult;
RevocationStatus revocationStatus = revocationDetails.OcspRevocationStatus;
bool isRevokedCRL = revocationDetails.IsRevokedCRL;

//Close the document
loadedDocument.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Get the stream from the document
FileStream documentStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);
//Load an existing signed PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(documentStream);
//Get signature field
PdfLoadedSignatureField signatureField = loadedDocument.Form.Fields[0] as PdfLoadedSignatureField;

//X509Certificate2Collection to check the signer's identity using root certificates
X509CertificateCollection collection = new X509CertificateCollection();
//Creates a certificate instance from PFX file with private key
FileStream certificateStream = new FileStream("PDF.pfx", FileMode.Open, FileAccess.Read);
byte[] data = new byte[certificateStream.Length];
certificateStream.Read(data, 0, data.Length);
//Create new X509Certificate2 with the root certificate
X509Certificate2 certificate = new X509Certificate2(data, "password123");
//Add the certificate to the collection
collection.Add(certificate);

//Validate signature and get the validation result
PdfSignatureValidationResult result = signatureField.ValidateSignature(collection);
//Checks whether the signature is valid or not
SignatureStatus status = result.SignatureStatus;
//Checks whether the document is modified or not
bool isModified = result.IsDocumentModified;
//Signature details
string issuerName = signatureField.Signature.Certificate.IssuerName;
DateTime validFrom = signatureField.Signature.Certificate.ValidFrom;
DateTime validTo = signatureField.Signature.Certificate.ValidTo;
string signatureAlgorithm = result.SignatureAlgorithm;
DigestAlgorithm digestAlgorithm = result.DigestAlgorithm;
//Revocation validation details
RevocationResult revocationDetails = result.RevocationResult;
RevocationStatus revocationStatus = revocationDetails.OcspRevocationStatus;
bool isRevokedCRL = revocationDetails.IsRevokedCRL;

//Close the document
loadedDocument.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Get the stream from the document
Stream documentStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");
//Load an existing signed PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(documentStream);
//Get signature field
PdfLoadedSignatureField signatureField = loadedDocument.Form.Fields[0] as PdfLoadedSignatureField;

//X509Certificate2Collection to check the signer's identity using root certificates
X509CertificateCollection collection = new X509CertificateCollection();
//Creates a certificate instance from PFX file with private key
Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.PDF.pfx");
byte[] data = new byte[certificateStream.Length];
certificateStream.Read(data, 0, data.Length);
//Create new X509Certificate2 with the root certificate
X509Certificate2 certificate = new X509Certificate2(data, "password123");
//Add the certificate to the collection
collection.Add(certificate);

//Validate signature and get the validation result
PdfSignatureValidationResult result = signatureField.ValidateSignature(collection);
//Checks whether the signature is valid or not
SignatureStatus status = result.SignatureStatus;
//Checks whether the document is modified or not
bool isModified = result.IsDocumentModified;
//Signature details
string issuerName = signatureField.Signature.Certificate.IssuerName;
DateTime validFrom = signatureField.Signature.Certificate.ValidFrom;
DateTime validTo = signatureField.Signature.Certificate.ValidTo;
string signatureAlgorithm = result.SignatureAlgorithm;
DigestAlgorithm digestAlgorithm = result.DigestAlgorithm;
//Revocation validation details
RevocationResult revocationDetails = result.RevocationResult;
RevocationStatus revocationStatus = revocationDetails.OcspRevocationStatus;
bool isRevokedCRL = revocationDetails.IsRevokedCRL;

//Close the document
loadedDocument.Close(true);

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Digital%20Signature/Validate-the-digitally-signed-PDF-signature/).

### Validate all signatures in PDF document

Added the support to validate all the digital signatures in an existing PDF document. 

You can use the [ValidateSignatures](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedFormFieldCollection.html#Syncfusion_Pdf_Parsing_PdfLoadedFormFieldCollection_ValidateSignatures_Syncfusion_Pdf_Parsing_PdfSignatureValidationOptions_System_Collections_Generic_List_Syncfusion_Pdf_Security_PdfSignatureValidationResult___) method available in the [PdfLoadedFormFieldCollection](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedFormFieldCollection.html) class to validate all the digital signatures. You can get the list of [PdfSignatureValidationResult](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSignatureValidationResult.html) from the [ValidateSignatures](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedFormFieldCollection.html#Syncfusion_Pdf_Parsing_PdfLoadedFormFieldCollection_ValidateSignatures_Syncfusion_Pdf_Parsing_PdfSignatureValidationOptions_System_Collections_Generic_List_Syncfusion_Pdf_Security_PdfSignatureValidationResult___) method.

The following code example explains how to validate all the signatures in digitally signed PDF document.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Load an existing signed PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");

//X509Certificate2Collection to check the signer's identity using root certificates
X509CertificateCollection collection = new X509CertificateCollection();
//Create new X509Certificate2 with the root certificate
X509Certificate2 certificate = new X509Certificate2("PDF.pfx", "password123");
//Add the certificate to the collection
collection.Add(certificate);
//Validate all signatures in loaded PDF document and get the list of validation result
List<PdfSignatureValidationResult> results;
bool isValid = loadedDocument.Form.Fields.ValidateSignatures(collection, out results);

//Close the document
loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Load an existing signed PDF document
Dim loadedDocument As PdfLoadedDocument = New PdfLoadedDocument("Input.pdf")

'X509Certificate2Collection to check the signer's identity using root certificates
Dim collection As X509CertificateCollection = New X509CertificateCollection()
'Create new X509Certificate2 with the root certificate
Dim certificate As X509Certificate2 = New X509Certificate2("PDF.pfx", "password123")
'Add the certificate to the collection
collection.Add(certificate)
'Validate all signatures in loaded PDF document and get the list of validation result
Dim results As List<PdfSignatureValidationResult>
Dim isValid As Boolean = loadedDocument.Form.Fields.ValidateSignatures(collection, out results)

'Close the document
loadedDocument.Close(true)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Get the stream from the document
Stream documentStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Input.pdf");
//Load an existing signed PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(documentStream);

//X509Certificate2Collection to check the signer's identity using root certificates
X509CertificateCollection collection = new X509CertificateCollection();
//Creates a certificate instance from PFX file with private key
Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.PDF.pfx");
byte[] data = new byte[certificateStream.Length];
certificateStream.Read(data, 0, data.Length);
//Create new X509Certificate2 with the root certificate
X509Certificate2 certificate = new X509Certificate2(data, "password123");
//Add the certificate to the collection
collection.Add(certificate);
//Validate all signatures in loaded PDF document and get the list of validation result
List<PdfSignatureValidationResult> results;
bool isValid = loadedDocument.Form.Fields.ValidateSignatures(collection, out results);

//Close the document
loadedDocument.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Get the stream from the document
FileStream documentStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);
//Load an existing signed PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(documentStream);

//X509Certificate2Collection to check the signer's identity using root certificates
X509CertificateCollection collection = new X509CertificateCollection();

//Creates a certificate instance from PFX file with private key
FileStream certificateStream = new FileStream("PDF.pfx", FileMode.Open, FileAccess.Read);
byte[] data = new byte[certificateStream.Length];
certificateStream.Read(data, 0, data.Length);
//Create new X509Certificate2 with the root certificate
X509Certificate2 certificate = new X509Certificate2(data, "password123");
//Add the certificate to the collection
collection.Add(certificate);
//Validate all signatures in loaded PDF document and get the list of validation result
List<PdfSignatureValidationResult> results;
bool isValid = loadedDocument.Form.Fields.ValidateSignatures(collection, out results);

//Close the document
loadedDocument.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Get the stream from the document
Stream documentStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");
//Load an existing signed PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(documentStream);

//X509Certificate2Collection to check the signer's identity using root certificates
X509CertificateCollection collection = new X509CertificateCollection();
//Creates a certificate instance from PFX file with private key
Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.PDF.pfx");
byte[] data = new byte[certificateStream.Length];
certificateStream.Read(data, 0, data.Length);
//Create new X509Certificate2 with the root certificate
X509Certificate2 certificate = new X509Certificate2(data, "password123");
//Add the certificate to the collection
collection.Add(certificate);
//Validate all signatures in loaded PDF document and get the list of validation result
List<PdfSignatureValidationResult> results;
bool isValid = loadedDocument.Form.Fields.ValidateSignatures(collection, out results);

//Close the document
loadedDocument.Close(true);

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Digital%20Signature/Validate-all-signatures-in-digitally-signed-PDF/).

## Deferred signing in PDF document

The following code sample shows how to be deferred signing in a PDF document from an external signature using [IPdfExternalSigner](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.IPdfExternalSigner.html) class and [AddExternalSigner](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSignature.html#Syncfusion_Pdf_Security_PdfSignature_AddExternalSigner_Syncfusion_Pdf_Security_IPdfExternalSigner_System_Collections_Generic_List_System_Security_Cryptography_X509Certificates_X509Certificate2__System_Byte___) method in [PdfSignature](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSignature.html).

Steps for deferred signing: 
1.	Create a PDF document with an empty signature.
2.	Users will sign the document hash using the external services.
3.	Replace the empty signature with a signed hash from the external services using [ReplaceEmptySignature](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSignature.html#Syncfusion_Pdf_Security_PdfSignature_ReplaceEmptySignature_System_IO_Stream_System_String_System_IO_Stream_System_String_Syncfusion_Pdf_Security_IPdfExternalSigner_System_Collections_Generic_List_System_Security_Cryptography_X509Certificates_X509Certificate2__) method. 

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Load an existing PDF document.
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("PDF_Succinctly.pdf");

//Creates a digital signature.
PdfSignature signature = new PdfSignature(loadedDocument, loadedDocument.Pages[0], null, "Signature");
//Sets the signature information.
signature.Bounds = new RectangleF(new PointF(0, 0), new SizeF(100, 30));
signature.Settings.CryptographicStandard = CryptographicStandard.CADES;
signature.Settings.DigestAlgorithm = DigestAlgorithm.SHA1;

//Create an external signer.
IPdfExternalSigner externalSignature = new SignEmpty("SHA1");
//Add public certificates.
System.Collections.Generic.List<X509Certificate2> certificates = new System.Collections.Generic.List<X509Certificate2>();
certificates.Add(new X509Certificate2(Convert.FromBase64String(PublicCert)));
signature.AddExternalSigner(externalSignature, certificates, null);

//Saves the document.
loadedDocument.Save("EmptySignature.pdf");
//Closes the document.
loadedDocument.Close(true);

/// <summary>
/// Represents to sign an empty signature from an external signer.
/// </summary>
class SignEmpty : IPdfExternalSigner
{
    private string _hashAlgorithm;
    public string HashAlgorithm
    {
        get { return _hashAlgorithm; }
    }

    public SignEmpty(string hashAlgorithm)
    {
        _hashAlgorithm = hashAlgorithm;
    }

    public byte[] Sign(byte[] message, out byte[] timeStampResponse)
    {
        //Send the document hash for signing using the external services.
        SignDocumentHash(message);
        //Set a null value to create an empty signed document.
        byte[] signedBytes = null;
        timeStampResponse = null;
        return signedBytes;
    }
}
//Create an external signer with a signed hash message.
IPdfExternalSigner externalSigner = new ExternalSigner("SHA1", signedHash);
//Add public certificates.
System.Collections.Generic.List<X509Certificate2> publicCertificates = new System.Collections.Generic.List<X509Certificate2>();
publicCertificates.Add(new X509Certificate2(Convert.FromBase64String(PublicCert)));

//Create an output file stream.
MemoryStream outputFileStream = new MemoryStream();    
//Get the stream from the document.
FileStream inputFileStream = new FileStream("EmptySignature.pdf", FileMode.Open, FileAccess.Read);
string pdfPassword = string.Empty;
//Replace an empty signature.
PdfSignature.ReplaceEmptySignature(inputFileStream, pdfPassword, outputFileStream, signatureName, externalSigner, publicCertificates);

/// <summary>
/// Represents to replace an empty signature from an external signer.
/// </summary>
class ExternalSigner : IPdfExternalSigner
{
    private string _hashAlgorithm;
    private byte[] _signedHash;
    public string HashAlgorithm
    {
        get { return _hashAlgorithm; }
    }

    public ExternalSigner(string hashAlgorithm, byte[] hash)
    {
        _hashAlgorithm = hashAlgorithm;
        _signedHash = hash;
    }

    public byte[] Sign(byte[] message, out byte[] timeStampResponse)
    {
        //Set the signed hash message to replace an empty signature.
        byte[] signedBytes = _signedHash;
        timeStampResponse = null;
        return signedBytes;
    }
}

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Load an existing PDF document.
Dim loadedDocument As PdfLoadedDocument = New PdfLoadedDocument("PDF_Succinctly.pdf")

'Creates a digital signature.
Dim signature As PdfSignature = New PdfSignature(loadedDocument, loadedDocument.Pages(0), Nothing, "Signature")
'Sets the signature information.
signature.Bounds = New RectangleF(New PointF(0, 0), New SizeF(100, 30))
signature.Settings.CryptographicStandard = CryptographicStandard.CADES
signature.Settings.DigestAlgorithm = DigestAlgorithm.SHA1

'Create an external signer.
Dim externalSignature As IPdfExternalSigner = New SignEmpty("SHA1")
'Add public certificates.
Dim certificates As System.Collections.Generic.List(Of X509Certificate2) = New System.Collections.Generic.List(Of X509Certificate2)
certificates.Add(New X509Certificate2(Convert.FromBase64String(PublicCert)))
signature.AddExternalSigner(externalSignature, certificates, Nothing)

'Save the document.
loadedDocument.Save("EmptySignature.pdf")
'Close the document.
loadedDocument.Close(True)

''' <summary>
''' Represents to sign an empty signature. 
''' </summary>
Class SignEmpty
    Implements IPdfExternalSigner

    Private _hashAlgorithm As String

    Public ReadOnly Property HashAlgorithm As String Implements IPdfExternalSigner.HashAlgorithm
        Get
            Return Me._hashAlgorithm
        End Get
    End Property

    Public Sub New(ByVal hashAlgorithm As String)
        MyBase.New
        Me._hashAlgorithm = hashAlgorithm
    End Sub

    Private Function IPdfExternalSigner_Sign(message() As Byte, ByRef timeStampResponse() As Byte) As Byte() Implements IPdfExternalSigner.Sign
        'Send document hash for signing using the external services.
        Me.SignDocumentHash(message)
        'Set a null value to create an empty signed document.
        Dim signedBytes() As Byte = Nothing
        timeStampResponse = Nothing
        Return signedBytes
    End Function
End Class
'Create an external signer with a signed hash message.
Dim externalSigner As IPdfExternalSigner = New ExternalSigner("SHA1", Module1.SignedHash)
'Add public certificates.
Dim publicCertificates As System.Collections.Generic.List(Of X509Certificate2) = New System.Collections.Generic.List(Of X509Certificate2)
publicCertificates.Add(New X509Certificate2(Convert.FromBase64String(PublicCert)))

'Create an output file stream.
Dim outputFileStream As MemoryStream = New MemoryStream
'Get the stream from the document.
Dim documentStream As FileStream = New FileStream("EmptySignature.pdf ", FileMode.Open, FileAccess.Read)
Dim pdfPassword As String = String.Empty
'Replace an empty signature.
PdfSignature.ReplaceEmptySignature(documentStream, pdfPassword, outputFileStream, "Signature", externalSigner, publicCertificates)

''' <summary>
''' Represents to replace the empty signature.
''' </summary>
Class ExternalSigner
    Implements IPdfExternalSigner
    Private _hashAlgorithm As String
    Private _signedHash() As Byte

    Public ReadOnly Property HashAlgorithm As String Implements IPdfExternalSigner.HashAlgorithm
        Get
            Return Me._hashAlgorithm
        End Get
    End Property

    Public Sub New(ByVal hashAlgorithm As String, ByVal hash() As Byte)
        MyBase.New
        Me._hashAlgorithm = hashAlgorithm
        Me._signedHash = hash
    End Sub

    Private Function IPdfExternalSigner_Sign(message() As Byte, ByRef timeStampResponse() As Byte) As Byte() Implements IPdfExternalSigner.Sign
        'Set the signed hash message to replace an empty signature.
        Dim signedBytes() As Byte = Me._signedHash
        timeStampResponse = Nothing
        Return signedBytes
    End Function
End Class

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Get the stream from the document.
Stream documentStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data. PDF_Succinctly.pdf");
//Load an existing PDF document.
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(documentStream);

//Creates a digital signature.
PdfSignature signature = new PdfSignature(loadedDocument, loadedDocument.Pages[0], null, "Signature");
//Sets the signature information.
signature.Bounds = new RectangleF(new PointF(0, 0), new SizeF(100, 30));
signature.Settings.CryptographicStandard = CryptographicStandard.CADES;
signature.Settings.DigestAlgorithm = DigestAlgorithm.SHA1;

//Create an external signer.
IPdfExternalSigner externalSignature = new SignEmpty("SHA1");
//Add public certificates.
System.Collections.Generic.List<X509Certificate2> certificates = new System.Collections.Generic.List<X509Certificate2>();
certificates.Add(new X509Certificate2(Convert.FromBase64String(PublicCert)));
signature.AddExternalSigner(externalSignature, certificates, null);

//Save the document.
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);
//Close the PDF document.
loadedDocument.Close(true);
//Save the stream as a PDF document file in the local machine. Refer to the PDF or UWP section for the respected code samples.
Save(stream, "EmptySignature.pdf");

/// <summary>
/// Represents to sign an empty signature from an external signer.
/// </summary>
class SignEmpty : IPdfExternalSigner
{
    private string _hashAlgorithm;

    public string HashAlgorithm
    {
        get { return _hashAlgorithm; }
    }

    public SignEmpty(string hashAlgorithm)
    {
        _hashAlgorithm = hashAlgorithm;
    }

    public byte[] Sign(byte[] message, out byte[] timeStampResponse)
    {
        //Send document hash for signing using the external services.
        SignDocumentHash(message);
        //Set a null value to create an empty signed document.
        byte[] signedBytes = null;
        timeStampResponse = null;
        return signedBytes;
    }
}
//Create an external signer with a signed hash message.
IPdfExternalSigner externalSigner = new ExternalSigner("SHA1", signedHash);
//Add public certificates.
System.Collections.Generic.List<X509Certificate2> publicCertificates = new System.Collections.Generic.List<X509Certificate2>();
publicCertificates.Add(new X509Certificate2(Convert.FromBase64String(PublicCert)));

//Create an output file stream.
MemoryStream outputFileStream = new MemoryStream();    
//Get the stream from the document.
FileStream inputFileStream = new FileStream("EmptySignature.pdf", FileMode.Open, FileAccess.Read);
string pdfPassword = string.Empty;
//Replace an empty signature.
PdfSignature.ReplaceEmptySignature(inputFileStream, pdfPassword, outputFileStream, signatureName, externalSigner, publicCertificates);

/// <summary>
/// Represents to replace an empty signature from an external signer.
/// </summary>
class ExternalSigner : IPdfExternalSigner
{
    private string _hashAlgorithm;
    private byte[] _signedHash;
    public string HashAlgorithm
    {
        get { return _hashAlgorithm; }
    }

    public ExternalSigner(string hashAlgorithm, byte[] hash)
    {
        _hashAlgorithm = hashAlgorithm;
        _signedHash = hash;
    }

    public byte[] Sign(byte[] message, out byte[] timeStampResponse)
    {
        //Set the signed hash message to replace an empty signature.
        byte[] signedBytes = _signedHash;
        timeStampResponse = null;
        return signedBytes;
    }
}

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Get the stream from the document.
FileStream documentStream = new FileStream("PDF_Succinctly.pdf ", FileMode.Open, FileAccess.Read);
//Load an existing PDF document.
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(documentStream);

//Creates a digital signature.
PdfSignature signature = new PdfSignature(loadedDocument, loadedDocument.Pages[0], null, "Signature");
//Sets the signature information.
signature.Bounds = new RectangleF(new PointF(0, 0), new SizeF(100, 30));
signature.Settings.CryptographicStandard = CryptographicStandard.CADES;
signature.Settings.DigestAlgorithm = DigestAlgorithm.SHA1;

//Create an external signer.
IPdfExternalSigner externalSignature = new SignEmpty("SHA1");
//Add public certificates.
System.Collections.Generic.List<X509Certificate2> certificates = new System.Collections.Generic.List<X509Certificate2>();
certificates.Add(new X509Certificate2(Convert.FromBase64String(PublicCert)));
signature.AddExternalSigner(externalSignature, certificates, null);

//Save the document.
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);
//Close the PDF document.
loadedDocument.Close(true);
//Defining the ContentType for a PDF file.
string contentType = "application/pdf";
//Define the file name.
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name.
return File(stream, contentType, fileName);

/// <summary>
/// Represents to sign an empty signature from the external signer.
/// </summary>
class SignEmpty : IPdfExternalSigner
{
    private string _hashAlgorithm;

    public string HashAlgorithm
    {
        get { return _hashAlgorithm; }
    }

    public SignEmpty(string hashAlgorithm)
    {
        _hashAlgorithm = hashAlgorithm;
    }

    public byte[] Sign(byte[] message, out byte[] timeStampResponse)
    {
        //Send document hash for signing using the external services.
        SignDocumentHash(message);
        //Set a null value to create an empty signed document.
        byte[] signedBytes = null;
        timeStampResponse = null;
        return signedBytes;
    }
}
//Create an external signer with a signed hash message.
IPdfExternalSigner externalSigner = new ExternalSigner("SHA1", signedHash);
//Add public certificates.
System.Collections.Generic.List<X509Certificate2> publicCertificates = new System.Collections.Generic.List<X509Certificate2>();
publicCertificates.Add(new X509Certificate2(Convert.FromBase64String(PublicCert)));

//Create an output file stream.
MemoryStream outputFileStream = new MemoryStream();    
//Get the stream from the document.
FileStream inputFileStream = new FileStream("EmptySignature.pdf", FileMode.Open, FileAccess.Read);
string pdfPassword = string.Empty;
//Replace an empty signature.
PdfSignature.ReplaceEmptySignature(inputFileStream, pdfPassword, outputFileStream, signatureName, externalSigner, publicCertificates);

/// <summary>
/// Represents to replace an empty signature from an external signer.
/// </summary>
class ExternalSigner : IPdfExternalSigner
{
    private string _hashAlgorithm;
    private byte[] _signedHash;
    public string HashAlgorithm
    {
        get { return _hashAlgorithm; }
    }

    public ExternalSigner(string hashAlgorithm, byte[] hash)
    {
        _hashAlgorithm = hashAlgorithm;
        _signedHash = hash;
    }

    public byte[] Sign(byte[] message, out byte[] timeStampResponse)
    {
        //Set the signed hash message to replace an empty signature.
        byte[] signedBytes = _signedHash;
        timeStampResponse = null;
        return signedBytes;
    }
}

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Get the stream from the document.
Stream documentStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data. PDF_Succinctly.pdf");
//Load an existing PDF document.
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(documentStream);

//Creates a digital signature.
PdfSignature signature = new PdfSignature(loadedDocument, loadedDocument.Pages[0], null, "Signature");
//Sets the signature information.
signature.Bounds = new RectangleF(new PointF(0, 0), new SizeF(100, 30));
signature.Settings.CryptographicStandard = CryptographicStandard.CADES;
signature.Settings.DigestAlgorithm = DigestAlgorithm.SHA1;

//Create an external signer.
IPdfExternalSigner externalSignature = new SignEmpty("SHA1");
//Add public certificates.
System.Collections.Generic.List<X509Certificate2> certificates = new System.Collections.Generic.List<X509Certificate2>();
certificates.Add(new X509Certificate2(Convert.FromBase64String(PublicCert)));
signature.AddExternalSigner(externalSignature, certificates, null);

//Save the document to the stream.
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);
//Close the document.
loadedDocument.Close(true);
//If the position is not set to '0' then the PDF will be empty.
stream.Position = 0;
//Save the stream into a PDF file.
//The operation in save under Xamarin varies between Windows Phone, Android, and iOS platforms. Please refer to the PDF/Xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

/// <summary>
/// Represents to sign an empty signature from an external signer.
/// </summary>
class SignEmpty : IPdfExternalSigner
{
    private string _hashAlgorithm;
    public string HashAlgorithm
    {
        get { return _hashAlgorithm; }
    }

    public SignEmpty(string hashAlgorithm)
    {
        _hashAlgorithm = hashAlgorithm;
    }

    public byte[] Sign(byte[] message, out byte[] timeStampResponse)
    {
        //Send document hash for signing using the external services.
        SignDocumentHash(message);
        //Set a null value to create an empty signed document.
        byte[] signedBytes = null;
        timeStampResponse = null;
        return signedBytes;
    }
}
//Create an external signer with a signed hash message.
IPdfExternalSigner externalSigner = new ExternalSigner("SHA1", signedHash);
//Add public certificates.
System.Collections.Generic.List<X509Certificate2> publicCertificates = new System.Collections.Generic.List<X509Certificate2>();
publicCertificates.Add(new X509Certificate2(Convert.FromBase64String(PublicCert)));

//Create an output file stream.
MemoryStream outputFileStream = new MemoryStream();    
//Get the stream from the document.
FileStream inputFileStream = new FileStream("EmptySignature.pdf", FileMode.Open, FileAccess.Read);
string pdfPassword = string.Empty;

//Replace an empty signature.
PdfSignature.ReplaceEmptySignature(inputFileStream, pdfPassword, outputFileStream, signatureName, externalSigner, publicCertificates);

/// <summary>
/// Represents to replace an empty signature from an external signer.
/// </summary>
class ExternalSigner : IPdfExternalSigner
{
    private string _hashAlgorithm;
    private byte[] _signedHash;
    public string HashAlgorithm
    {
        get { return _hashAlgorithm; }
    }

    public ExternalSigner(string hashAlgorithm, byte[] hash)
    {
        _hashAlgorithm = hashAlgorithm;
        _signedHash = hash;
    }

    public byte[] Sign(byte[] message, out byte[] timeStampResponse)
    {
        //Set the signed hash message to replace an empty signature.
        byte[] signedBytes = _signedHash;
        timeStampResponse = null;
        return signedBytes;
    }
}

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Digital%20Signature/Deferred-signing-in-PDF-document/).

## Adding the estimated size of the signature

The following code sample shows how to add the estimated size of the signature in the PDF document using [EstimatedSignatureSize](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSignature.html#Syncfusion_Pdf_Security_PdfSignature_EstimatedSignatureSize) property.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Creating a new PDF Document. 
PdfDocument document = new PdfDocument();
//Adding a new page to the PDF document. 
PdfPageBase page = document.Pages.Add();

//Create a PDF certificate.
PdfCertificate pdfCert = new PdfCertificate(@"PDF.pfx", "password123");
//Add a new signature to the PDF page.
PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");
signature.Bounds = new Rectangle(10, 20, 400, 200);
//Sets the estimated size of the signature.
signature.EstimatedSignatureSize = 20000;

//Save the PDF document.
document.Save("Output.pdf");
//Close the PDF document.
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
 
'Creating a new PDF Document. 
Dim document As PdfDocument =  New PdfDocument()  
'Adding a new page to the PDF document. 
Dim page As PdfPageBase =  document.Pages.Add() 
 
'Create a PDF certificate.
Dim pdfCert As PdfCertificate =  New PdfCertificate("PDF.pfx","password123") 
'Add a new signature to the PDF page.
Dim signature As PdfSignature =  New PdfSignature(document,page,pdfCert,"Signature") 
signature.Bounds = New Rectangle(10, 20, 400, 200)
'Sets the estimated size of the signature.
signature.EstimatedSignatureSize = 20000
 
'Save the PDF document.
document.Save("Output.pdf")
'Close the PDF document.
document.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Creating a new PDF Document.
PdfDocument document = new PdfDocument();
//Adding a new page to the PDF document.
PdfPageBase page = document.Pages.Add();

//Creates a certificate instance from the PFX file with a private key.
Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.PDF.pfx");
PdfCertificate pdfCert = new PdfCertificate(certificateStream, "password123");
//Add a new signature to the PDF page.
PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");
signature.Bounds = new Rectangle(10, 20, 400, 200);
//Sets the estimated size of the signature.
signature.EstimatedSignatureSize = 20000;

//Save the document.
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Close the PDF document.
document.Close(true);
//Save the stream as a PDF document file in the local machine. Refer to the PDF or UWP section for the respective code samples.
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Creating a new PDF Document. 
PdfDocument document = new PdfDocument();
//Adding a new page to the PDF document.
PdfPageBase page = document.Pages.Add();

//Creates a certificate instance from the PFX file with a private key.
FileStream certificateStream = new FileStream("PDF.pfx", FileMode.Open, FileAccess.Read);
PdfCertificate pdfCert = new PdfCertificate(certificateStream, "password123"); 
//Add a new signature to the PDF page.
PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");
signature.Bounds = new Rectangle(10, 20, 400, 200);
//Sets the estimated size of the signature.
signature.EstimatedSignatureSize = 20000;

//Creating the stream object.
MemoryStream stream = new MemoryStream();
//Save the document into stream.
document.Save(stream);
//If the position is not set to '0,' then the PDF will be empty.
stream.Position = 0;
//Close the document.
document.Close(true);
//Defining the ContentType for a PDF file.
string contentType = "application/pdf";
//Define the file name.
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name.
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Creating a new PDF Document. 
PdfDocument document = new PdfDocument();
//Adding a new page to the PDF document. 
PdfPageBase page = document.Pages.Add();

//Creates a certificate instance from the PFX file with a private key.
Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.PDF.pfx");
PdfCertificate pdfCert = new PdfCertificate(certificateStream, "password123");
//Add a new signature to the PDF page.
PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");
signature.Bounds = new Rectangle(10, 20, 400, 200);
//Sets the estimated size of the signature.
signature.EstimatedSignatureSize = 20000;

//Save the document to the stream.
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Close the document.
document.Close(true);
stream.Position = 0;
//Save the stream into a PDF file.
//The operation in save under the Xamarin varies between Windows Phone, Android, and iOS platforms. Please refer to the PDF or Xamarin section for respective code samples.
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Digital%20Signature/Adding-the-estimated-size-of-the-signature/).

## Deferred signing without PKCS7 encoding

The following code sample shows deferred signing in a PDF document without PKCS7 encoding from an external signature using [IPdfExternalSigner](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.IPdfExternalSigner.html) class and [AddExternalSigner](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSignature.html#Syncfusion_Pdf_Security_PdfSignature_AddExternalSigner_Syncfusion_Pdf_Security_IPdfExternalSigner_System_Collections_Generic_List_System_Security_Cryptography_X509Certificates_X509Certificate2__System_Byte___) method.

Steps for deferred signing: 
1.	Create a PDF document with an empty signature.
2.	Users will sign the document hash using the external services.
3.	Replace the empty signature with a PKCS7 encoded signed hash from the external services using [ReplaceEmptySignature](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSignature.html#Syncfusion_Pdf_Security_PdfSignature_ReplaceEmptySignature_System_IO_Stream_System_String_System_IO_Stream_System_String_Syncfusion_Pdf_Security_IPdfExternalSigner_System_Collections_Generic_List_System_Security_Cryptography_X509Certificates_X509Certificate2__System_Boolean_s) method. 

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Load an existing PDF document.
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("PDF_Succinctly.pdf");

//Creates a digital signature.
PdfSignature signature = new PdfSignature(loadedDocument, loadedDocument.Pages[0], null, "Signature");
//Sets the signature information.
signature.Bounds = new RectangleF(new PointF(0, 0), new SizeF(100, 30));
signature.Settings.CryptographicStandard = CryptographicStandard.CADES;
signature.Settings.DigestAlgorithm = DigestAlgorithm.SHA1;

//Create an external signer.
IPdfExternalSigner externalSignature = new SignEmpty("SHA1");
//Add public certificates.
System.Collections.Generic.List<X509Certificate2> certificates = new System.Collections.Generic.List<X509Certificate2>();
signature.AddExternalSigner(externalSignature, certificates, null);

//Save a document.
loadedDocument.Save("EmptySignature.pdf");
//Close a document.
loadedDocument.Close(true);

//Create an external signer with a signed hash message.
IPdfExternalSigner externalSigner = new ExternalSigner("SHA1");
//Add public certificates.
System.Collections.Generic.List<X509Certificate2> publicCertificates = new System.Collections.Generic.List<X509Certificate2>();
publicCertificates.Add(new X509Certificate2(Convert.FromBase64String(PublicCert)));

//Create an output file stream.
MemoryStream outputFileStream = new MemoryStream();
//Get the stream from a document.
FileStream inputFileStream = new FileStream("EmptySignature.pdf", FileMode.Open, FileAccess.Read);
string pdfPassword = string.Empty;
//Deferred signing without PKCS7 encoding.
PdfSignature.ReplaceEmptySignature(inputFileStream, pdfPassword, outputFileStream, signatureName, externalSigner, publicCertificates, false);

/// <summary>
/// Represents to create an empty signature.
/// </summary>
class SignEmpty : IPdfExternalSigner
{
    private string _hashAlgorithm;
    public string HashAlgorithm
    {
        get { return _hashAlgorithm; }
    }

    public SignEmpty(string hashAlgorithm)
    {
        _hashAlgorithm = hashAlgorithm;
    }

    public byte[] Sign(byte[] message, out byte[] timeStampResponse)
    {
        //Set a null value to create an empty signed document.
        byte[] signedBytes = null;
        timeStampResponse = null;
        return signedBytes;
    }
}

/// <summary>
/// Represents to replace an empty signature from an external signer.
/// </summary>
class ExternalSigner : IPdfExternalSigner
{
    private string _hashAlgorithm;
    public string HashAlgorithm
    {
        get { return _hashAlgorithm; }
    }

    public ExternalSigner(string hashAlgorithm)
    {
        _hashAlgorithm = hashAlgorithm;
    }

    public byte[] Sign(byte[] message, out byte[] timeStampResponse)
    {
        //Set the signed encoded PKCS7 hash message to replace an empty signature.
        byte[] signedBytes = EncodedPKCS7Hash;
        timeStampResponse = null;
        return signedBytes;
    }
}

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Load an existing PDF document.
Dim loadedDocument As PdfLoadedDocument = New PdfLoadedDocument("PDF_Succinctly.pdf")

'Creates a digital signature.
Dim signature As PdfSignature = New PdfSignature(loadedDocument, loadedDocument.Pages(0), Nothing, "Signature")
'Sets the signature information.
signature.Bounds = New RectangleF(New PointF(0, 0), New SizeF(100, 30))
signature.Settings.CryptographicStandard = CryptographicStandard.CADES
signature.Settings.DigestAlgorithm = DigestAlgorithm.SHA1

' Create an external signer.
Dim externalSignature As IPdfExternalSigner = New SignEmpty("SHA1")
' Add public certificates.
Dim certificates As System.Collections.Generic.List(Of X509Certificate2) = New System.Collections.Generic.List(Of X509Certificate2)
signature.AddExternalSigner(externalSignature, certificates, Nothing)

'Save the document.
loadedDocument.Save("EmptySignature.pdf")
'Close the document.
loadedDocument.Close(True)

'Create an external signer with a signed hash message.
Dim externalSigner As IPdfExternalSigner = New ExternalSigner("SHA1")
'Add public certificates.
Dim publicCertificates As System.Collections.Generic.List(Of X509Certificate2) = New System.Collections.Generic.List(Of X509Certificate2)
publicCertificates.Add(New X509Certificate2(Convert.FromBase64String(PublicCert)))

'Create an output file stream.
Dim outputFileStream As MemoryStream = New MemoryStream
'Get the stream from the document.
Dim documentStream As FileStream = New FileStream("EmptySignature.pdf ", FileMode.Open, FileAccess.Read)
Dim pdfPassword As String = String.Empty
'Deferred signing without PKCS7 encoding 
PdfSignature.ReplaceEmptySignature(documentStream, pdfPassword, outputFileStream, "Signature", externalSigner, publicCertificates, False)

''' <summary>
''' Represents to create an empty signature.
''' </summary>
Class SignEmpty
    Implements IPdfExternalSigner
    Private _hashAlgorithm As String

    Public ReadOnly Property HashAlgorithm As String Implements IPdfExternalSigner.HashAlgorithm
        Get
            Return Me._hashAlgorithm
        End Get
    End Property

    Public Sub New(ByVal hashAlgorithm As String)
        MyBase.New
        Me._hashAlgorithm = hashAlgorithm
    End Sub

    Private Function IPdfExternalSigner_Sign(message() As Byte, ByRef timeStampResponse() As Byte) As Byte() Implements IPdfExternalSigner.Sign
        'Set a null value to create an empty signed document.
        Dim signedBytes() As Byte = Nothing
        timeStampResponse = Nothing
        Return signedBytes
    End Function
End Class

''' <summary>
''' Represents to replace the empty signature.
''' </summary>
Class ExternalSigner
    Implements IPdfExternalSigner
    Private _hashAlgorithm As String
    Public ReadOnly Property HashAlgorithm As String Implements IPdfExternalSigner.HashAlgorithm
        Get
            Return Me._hashAlgorithm
        End Get
    End Property

    Public Sub New(ByVal hashAlgorithm As String)
        MyBase.New
        Me._hashAlgorithm = hashAlgorithm
    End Sub

    Private Function IPdfExternalSigner_Sign(message() As Byte, ByRef timeStampResponse() As Byte) As Byte() Implements IPdfExternalSigner.Sign
        'Set the signed encoded PKCS7 hash message to replace an empty signature.
        Dim signedBytes() As Byte = EncodedPKCS7Hash
        timeStampResponse = Nothing
        Return signedBytes
    End Function
End Class

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Get the stream from a document.
Stream documentStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data. PDF_Succinctly.pdf");
//Load an existing PDF document.
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(documentStream);

//Creates a digital signature.
PdfSignature signature = new PdfSignature(loadedDocument, loadedDocument.Pages[0], null, "Signature");
//Sets the signature information.
signature.Bounds = new RectangleF(new PointF(0, 0), new SizeF(100, 30));
signature.Settings.CryptographicStandard = CryptographicStandard.CADES;
signature.Settings.DigestAlgorithm = DigestAlgorithm.SHA1;

//Create an external signer.
IPdfExternalSigner externalSignature = new SignEmpty("SHA1");
//Add public certificates.
System.Collections.Generic.List<X509Certificate2> certificates = new System.Collections.Generic.List<X509Certificate2>();
signature.AddExternalSigner(externalSignature, certificates, null);

//Save a document.
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);
//Close a PDF document.
loadedDocument.Close(true);
//Save the stream as a PDF document file in the local machine. Refer to the PDF or UWP section for the respected code samples
Save(stream, "EmptySignature.pdf");

//Create an external signer with a signed hash message.
IPdfExternalSigner externalSigner = new ExternalSigner("SHA1");
//Add public certificates.
System.Collections.Generic.List<X509Certificate2> publicCertificates = new System.Collections.Generic.List<X509Certificate2>();
publicCertificates.Add(new X509Certificate2(Convert.FromBase64String(PublicCert)));

//Create an output file stream.
MemoryStream outputFileStream = new MemoryStream();    
//Get the stream from the document
FileStream inputFileStream = new FileStream("EmptySignature.pdf", FileMode.Open, FileAccess.Read);
string pdfPassword = string.Empty;
// Deferred signing without PKCS7 encoding.
PdfSignature.ReplaceEmptySignature(inputFileStream, pdfPassword, outputFileStream, signatureName, externalSigner, publicCertificates, false);

/// <summary>
/// Represents to create an empty signature.
/// </summary>
class SignEmpty : IPdfExternalSigner
{
    private string _hashAlgorithm;
    public string HashAlgorithm
    {
        get { return _hashAlgorithm; }
    }

    public SignEmpty(string hashAlgorithm)
    {
        _hashAlgorithm = hashAlgorithm;
    }

    public byte[] Sign(byte[] message, out byte[] timeStampResponse)
    {
        //Set a null value to create an empty signed document.
        byte[] signedBytes = null;
        timeStampResponse = null;
        return signedBytes;
    }
}

/// <summary>
/// Represents to replace an empty signature from an external signer.
/// </summary>
class ExternalSigner : IPdfExternalSigner
{
    private string _hashAlgorithm;
    public string HashAlgorithm
    {
        get { return _hashAlgorithm; }
    }

    public ExternalSigner(string hashAlgorithm)
    {
        _hashAlgorithm = hashAlgorithm;
    }

    public byte[] Sign(byte[] message, out byte[] timeStampResponse)
    {
        //Set the signed encoded PKCS7 hash message to replace an empty signature. 
        byte[] signedBytes = EncodedPKCS7Hash;
        timeStampResponse = null;
        return signedBytes;
    }
}

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Get the stream from a document.
FileStream documentStream = new FileStream("PDF_Succinctly.pdf ", FileMode.Open, FileAccess.Read);
//Load an existing PDF document.
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(documentStream);

//Creates a digital signature.
PdfSignature signature = new PdfSignature(loadedDocument, loadedDocument.Pages[0], null, "Signature");
//Sets the signature information.
signature.Bounds = new RectangleF(new PointF(0, 0), new SizeF(100, 30));
signature.Settings.CryptographicStandard = CryptographicStandard.CADES;
signature.Settings.DigestAlgorithm = DigestAlgorithm.SHA1;

//Create an external signer.
IPdfExternalSigner externalSignature = new SignEmpty("SHA1");
//Add public certificates.
System.Collections.Generic.List<X509Certificate2> certificates = new System.Collections.Generic.List<X509Certificate2>();
signature.AddExternalSigner(externalSignature, certificates, null);

//Save a document.
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);
//Close a PDF document.
loadedDocument.Close(true);
//Defining the ContentType for a PDF file.
string contentType = "application/pdf";
//Define the file name.
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name.
return File(stream, contentType, fileName);

//Create an external signer with a signed hash message.
IPdfExternalSigner externalSigner = new ExternalSigner("SHA1");
//Add public certificates.
System.Collections.Generic.List<X509Certificate2> publicCertificates = new System.Collections.Generic.List<X509Certificate2>();
publicCertificates.Add(new X509Certificate2(Convert.FromBase64String(PublicCert)));

//Create an output file stream.
MemoryStream outputFileStream = new MemoryStream();    
// Get the stream from a document.
FileStream inputFileStream = new FileStream("EmptySignature.pdf", FileMode.Open, FileAccess.Read);
string pdfPassword = string.Empty;
//Deferred signing without PKCS7 encoding.
PdfSignature.ReplaceEmptySignature(inputFileStream, pdfPassword, outputFileStream, signatureName, externalSigner, publicCertificates, false);

/// <summary>
/// Represents to create an empty signature.
/// </summary>
class SignEmpty : IPdfExternalSigner
{
    private string _hashAlgorithm;
    public string HashAlgorithm
    {
        get { return _hashAlgorithm; }
    }

    public SignEmpty(string hashAlgorithm)
    {
        _hashAlgorithm = hashAlgorithm;
    }

    public byte[] Sign(byte[] message, out byte[] timeStampResponse)
    {
        //Set a null value to create an empty signed document.
        byte[] signedBytes = null;
        timeStampResponse = null;
        return signedBytes;
    }
}

/// <summary>
/// Represents to replace an empty signature from an external signer.
/// </summary>
class ExternalSigner : IPdfExternalSigner
{
    private string _hashAlgorithm;
    public string HashAlgorithm
    {
        get { return _hashAlgorithm; }
    }

    public ExternalSigner(string hashAlgorithm)
    {
        _hashAlgorithm = hashAlgorithm;
    }

    public byte[] Sign(byte[] message, out byte[] timeStampResponse)
    {
        //Set the signed encoded PKCS7 hash message to replace an empty signature.
        byte[] signedBytes = EncodedPKCS7Hash;
        timeStampResponse = null;
        return signedBytes;
    }
}

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Get the stream from a document.
Stream documentStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data. PDF_Succinctly.pdf");
//Load an existing PDF document.
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(documentStream);

//Creates a digital signature.
PdfSignature signature = new PdfSignature(loadedDocument, loadedDocument.Pages[0], null, "Signature");
//Sets the signature information.
signature.Bounds = new RectangleF(new PointF(0, 0), new SizeF(100, 30));
signature.Settings.CryptographicStandard = CryptographicStandard.CADES;
signature.Settings.DigestAlgorithm = DigestAlgorithm.SHA1;

//Create an external signer.
IPdfExternalSigner externalSignature = new SignEmpty("SHA1");
//Add public certificates.
System.Collections.Generic.List<X509Certificate2> certificates = new System.Collections.Generic.List<X509Certificate2>();
signature.AddExternalSigner(externalSignature, certificates, null);

//Save a document to the stream.
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);
//Close a document.
loadedDocument.Close(true);
stream.Position = 0;
//Save the stream into a PDF file.
//The operation in save under Xamarin varies between Windows Phone, Android, and iOS platforms. Please refer to the PDF or Xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

//Create an external signer with a signed hash message.
IPdfExternalSigner externalSigner = new ExternalSigner("SHA1");
//Add public certificates.
System.Collections.Generic.List<X509Certificate2> publicCertificates = new System.Collections.Generic.List<X509Certificate2>();
publicCertificates.Add(new X509Certificate2(Convert.FromBase64String(PublicCert)));

//Create an output file stream.
MemoryStream outputFileStream = new MemoryStream();    
//Get the stream from the document
FileStream inputFileStream = new FileStream("EmptySignature.pdf", FileMode.Open, FileAccess.Read);
string pdfPassword = string.Empty;
//Deferred signing without PKCS7 encoding.
PdfSignature.ReplaceEmptySignature(inputFileStream, pdfPassword, outputFileStream, signatureName, externalSigner, publicCertificates, false);

/// <summary>
/// Represents to create an empty signature.
/// </summary>
class SignEmpty : IPdfExternalSigner
{
    private string _hashAlgorithm;
    public string HashAlgorithm
    {
        get { return _hashAlgorithm; }
    }

    public SignEmpty(string hashAlgorithm)
    {
        _hashAlgorithm = hashAlgorithm;
    }

    public byte[] Sign(byte[] message, out byte[] timeStampResponse)
    {
        //Set a null value to create an empty signed document.
        byte[] signedBytes = null;
        timeStampResponse = null;
        return signedBytes;
    }
}

/// <summary>
/// Represents to replace an empty signature from an external signer.
/// </summary>
class ExternalSigner : IPdfExternalSigner
{
    private string _hashAlgorithm;
    public string HashAlgorithm
    {
        get { return _hashAlgorithm; }
    }

    public ExternalSigner(string hashAlgorithm)
    {
        _hashAlgorithm = hashAlgorithm;
    }

    public byte[] Sign(byte[] message, out byte[] timeStampResponse)
    {
        //Set the signed encoded PKCS7 hash message to replace an empty signature.
        byte[] signedBytes = EncodedPKCS7Hash;
        timeStampResponse = null;
        return signedBytes;
    }
}

{% endhighlight %}

{% endtabs %}

## Drawing text/image in the Signature Appearance

The following code example illustrates how to draw text/images in a digital appearance using [Appearance](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSignature.html#Syncfusion_Pdf_Security_PdfSignature_Appearance) property and [DrawImage](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfGraphics.html#Syncfusion_Pdf_Graphics_PdfGraphics_DrawImage_Syncfusion_Pdf_Graphics_PdfImage_System_Drawing_PointF_) method as follows.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Creates a new PDF document.
PdfDocument document = new PdfDocument();
//Adds a new page.
PdfPageBase page = document.Pages.Add();
//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from PFX file with private key.
PdfCertificate pdfCert = new PdfCertificate(@"PDF.pfx", "password123");
//Creates a digital signature.
PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");
//Sets an image for signature field.
PdfBitmap signatureImage = new PdfBitmap(@"signature.png");
//Sets signature information.
signature.Bounds = new RectangleF(0,0,200,100);
signature.ContactInfo = "johndoe@owned.us";
signature.LocationInfo = "Honolulu, Hawaii";
signature.Reason = "I am author of this document.";
//Create appearance for the digital siganture.
signature.Appearance.Normal.Graphics.DrawImage(signatureImage, signature.Bounds);

//Save the document.
document.Save("DigitalSignature.pdf");
//Close the document.
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create a new PDF document.
Dim document As New PdfDocument()
'Add a new page.
Dim page As PdfPageBase = document.Pages.Add()
'Create PDF graphics for the page.
Dim graphics As PdfGraphics = page.Graphics

'Create a certificate instance from a PFX file with a private key.
Dim pdfCert As New PdfCertificate("PDF.pfx", "password123")
'Create a digital signature.
Dim signature As New PdfSignature(document, page, pdfCert, "Signature")
'Set an image for signature field.
Dim signatureImage As New PdfBitmap("signature.jpg")
'Set the signature information.
signature.Bounds = New RectangleF(New PointF(0, 0), signatureImage.PhysicalDimension)
signature.ContactInfo = "johndoe@owned.us"
signature.LocationInfo = "Honolulu, Hawaii"
signature.Reason = "I am author of this document."
'Create appearance for the digital signature.
signature.Appearance.Normal.Graphics.DrawImage(signatureImage, signature.Bounds);

'Save and close the document.
document.Save("Output.pdf")
document.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();
//Add a new page.
PdfPageBase page = document.Pages.Add();
//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;

//Create a certificate instance from a PFX file with a private key.
Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.PDF.pfx");
PdfCertificate pdfCert = new PdfCertificate(certificateStream, "password123");
//Create a digital signature.
PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");
//Set an image for signature field.
Stream imageStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.signature.jpg");
PdfBitmap signatureImage = new PdfBitmap(imageStream);
//Set the signature information.
signature.Bounds = new RectangleF(new PointF(0, 0), signatureImage.PhysicalDimension);
signature.ContactInfo = "johndoe@owned.us";
signature.LocationInfo = "Honolulu, Hawaii";
signature.Reason = "I am author of this document.";
//Create appearance for the digital signature.
signature.Appearance.Normal.Graphics.DrawImage(signatureImage, signature.Bounds);

//Save the PDF document to stream.
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream);
//Close the document.
document.Close(true);                                                                   
//Save the stream as a PDF document file in the local machine. Refer to the PDF/UWP section for the respective code samples.
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();
//Add a new page.
PdfPageBase page = document.Pages.Add();
//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;

//Create a certificate instance from a PFX file with a private key.
FileStream certificateStream = new FileStream("PDF.pfx", FileMode.Open, FileAccess.Read);
PdfCertificate pdfCert = new PdfCertificate(certificateStream, "password123");
//Create a digital signature.
PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");
//Set an image for signature field.
FileStream imageStream = new FileStream("signature.jpg", FileMode.Open, FileAccess.Read);
//Set an image for signature field.
PdfBitmap signatureImage = new PdfBitmap(imageStream);
//Set the signature information.
signature.Bounds = new RectangleF(new PointF(0, 0), signatureImage.PhysicalDimension);
signature.ContactInfo = "johndoe@owned.us";
signature.LocationInfo = "Honolulu, Hawaii";
signature.Reason = "I am author of this document.";
//Create appearance for the digital signature.
signature.Appearance.Normal.Graphics.DrawImage(signatureImage, signature.Bounds);

//Save the document into stream.
MemoryStream stream = new MemoryStream();
document.Save(stream);
stream.Position = 0;
//Close the document.
document.Close(true);
//Define the ContentType for pdf file.
string contentType = "application/pdf";
//Define the file name.
string fileName = "Output.pdf";
//Create a FileContentResult object by using the file contents, content type, and file name.
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();
//Add a new page.
PdfPageBase page = document.Pages.Add();
//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;

//Create a certificate instance from a PFX file with a private key.
Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.PDF.pfx");
PdfCertificate pdfCert = new PdfCertificate(certificateStream, "password123");
//Create a digital signature.
PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");
//Set an image for signature field.
Stream imageStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.signature.jpg");
PdfBitmap signatureImage = new PdfBitmap(imageStream);
//Set the signature information.
signature.Bounds = new RectangleF(new PointF(0, 0), signatureImage.PhysicalDimension);
signature.ContactInfo = "johndoe@owned.us";
signature.LocationInfo = "Honolulu, Hawaii";
signature.Reason = "I am author of this document.";
//Create appearance for the digital signature.
signature.Appearance.Normal.Graphics.DrawImage(signatureImage, signature.Bounds);

//Save the PDF document to stream.
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Close the document.
document.Close(true);
//Save the stream into PDF file.
//The operation of Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples.
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Digital%20Signature/Draw-text-or-images-in-the-signature-appearance/).

## Long Term Validation (LTV) information

Added support for LTV validation and getting CRL and OCSP embedded details from the digital signature using [LtvVerificationInfo](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSignatureValidationResult.html#Syncfusion_Pdf_Security_PdfSignatureValidationResult_LtvVerificationInfo) class.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Loads an existing document.
PdfLoadedDocument document = new PdfLoadedDocument("Input.pdf");

//Gets the signature field.
PdfLoadedSignatureField signatureField = document.Form.Fields[0] as PdfLoadedSignatureField;
//Validates signature and gets the validation result.
PdfSignatureValidationResult result = signatureField.ValidateSignature();
//Gets the LTV Verification Information.
LtvVerificationInfo ltvVerificationInfo = result.LtvVerificationInfo;
//Checks whether the signature document LTV is enabled.
bool isLtvEnabled = ltvVerificationInfo.IsLtvEnabled;
//Checks whether the signature document has CRL embedded.
bool isCrlEmbedded = ltvVerificationInfo.IsCrlEmbedded;
//Checks whether the signature document has OCSP embedded.
bool isOcspEmbedded = ltvVerificationInfo.IsOcspEmbedded;

//Close the document.
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Loads an existing document
Dim document As PdfLoadedDocument = New PdfLoadedDocument("Input.pdf")

'Gets the signature field
Dim signatureField As PdfLoadedSignatureField = document.Form.Fields[0] As PdfLoadedSignatureField
'Validate signature and get validation result
Dim result As PdfSignatureValidationResult = signatureField.ValidateSignature()
'Gets the LTV Verification Information
Dim ltvVerificationInfo As LtvVerificationInfo = result.LtvVerificationInfo
'Checks whether the signature document LTV is enabled
Dim isLtvEnabled As Boolean = ltvVerificationInfo.IsLtvEnabled
'Checks whether the signature document has CRL embedded
Dim isCrlEmbedded As Boolean = ltvVerificationInfo.IsCrlEmbedded
'Checks whether the signature document has OCSP embedded
Dim isOcspEmbedded As Boolean = ltvVerificationInfo.IsOcspEmbedded

'Close the document
document.Close(true)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Get the stream from the document.
Stream documentStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Input.pdf");
//Loads an existing signed PDF document.
PdfLoadedDocument document = new PdfLoadedDocument(documentStream);

//Gets the signature field.
PdfLoadedSignatureField signatureField = document.Form.Fields[0] as PdfLoadedSignatureField;
//Validates signature and get validation result.
PdfSignatureValidationResult result = signatureField.ValidateSignature();
//Gets the LTV verification Information.
LtvVerificationInfo ltvVerificationInfo = result.LtvVerificationInfo;
//Checks whether the signature document LTV is enabled.
bool isLtvEnabled = ltvVerificationInfo.IsLtvEnabled;
//Checks whether the signature document has CRL embedded.
bool isCrlEmbedded = ltvVerificationInfo.IsCrlEmbedded;
//Checks whether the signature document has OCSP embedded.
bool isOcspEmbedded = ltvVerificationInfo.IsOcspEmbedded;

//Close the document.
document.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Gets the stream from the document.
FileStream documentStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);
//Loads an existing signed PDF document.
PdfLoadedDocument document = new PdfLoadedDocument(documentStream);

//Gets the signature field.
PdfLoadedSignatureField signatureField = document.Form.Fields[0] as PdfLoadedSignatureField;
//Validates signature and get validation result.
PdfSignatureValidationResult result = signatureField.ValidateSignature();
//Gets the LTV verification Information.
LtvVerificationInfo ltvVerificationInfo = result.LtvVerificationInfo;
//Checks whether the signature document LTV is enabled.
bool isLtvEnabled = ltvVerificationInfo.IsLtvEnabled;
//Checks whether the signature document has CRL embedded.
bool isCrlEmbedded = ltvVerificationInfo.IsCrlEmbedded;
//Checks whether the signature document has OCSP embedded.
bool isOcspEmbedded = ltvVerificationInfo.IsOcspEmbedded;

//Close the document.
document.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Get the stream from the document.
Stream documentStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");
//Loads an existing signed PDF document.
PdfLoadedDocument document = new PdfLoadedDocument(documentStream);

//Gets the signature field.
PdfLoadedSignatureField signatureField = document.Form.Fields[0] as PdfLoadedSignatureField;
//Validates signature and get validation result.
PdfSignatureValidationResult result = signatureField.ValidateSignature();
//Gets the LTV verification Information.
LtvVerificationInfo ltvVerificationInfo = result.LtvVerificationInfo;
//Checks whether the signature document LTV is enabled.
bool isLtvEnabled = ltvVerificationInfo.IsLtvEnabled;
//Checks whether the signature document has CRL embedded.
bool isCrlEmbedded = ltvVerificationInfo.IsCrlEmbedded;
//Checks whether the signature document has OCSP embedded.
bool isOcspEmbedded = ltvVerificationInfo.IsOcspEmbedded;

//Close the document.
document.Close(true);

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Digital%20Signature/Get-LTV-information/).

## Customized revocation validation

Added support to customize revocation validation using [PdfSignatureValidationOptions](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfSignatureValidationOptions.html).

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Loads an existing document
PdfLoadedDocument document = new PdfLoadedDocument("Input.pdf");

//Gets the signature field
PdfLoadedSignatureField signatureField = document.Form.Fields[0] as PdfLoadedSignatureField;
//Signature validation options
PdfSignatureValidationOptions options = new PdfSignatureValidationOptions();
//Sets the revocation type
options.RevocationValidationType = RevocationValidationType.Crl;
//Validate signature and get validation result
PdfSignatureValidationResult result = signatureField.ValidateSignature(options);

//Close the document
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Loads an existing document
Dim document As PdfLoadedDocument = New PdfLoadedDocument("Input.pdf")

'Gets the signature field
Dim signatureField As PdfLoadedSignatureField = document.Form.Fields[0] As PdfLoadedSignatureField
'Signature validation options
Dim options As PdfSignatureValidationOptions = New PdfSignatureValidationOptions()
'Sets the revocation type
options.RevocationValidationType = RevocationValidationType.Crl
'Validates signature and gets the validation result
Dim result As PdfSignatureValidationResult = signatureField.ValidateSignature(options)

'Close the document
document.Close(true)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Gets the stream from the document
Stream documentStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Input.pdf");
//Loads an existing signed PDF document
PdfLoadedDocument document = new PdfLoadedDocument(documentStream);

//Gets the signature field
PdfLoadedSignatureField signatureField = document.Form.Fields[0] as PdfLoadedSignatureField;
//Signature validation options
PdfSignatureValidationOptions options = new PdfSignatureValidationOptions();
//Sets the revocation type
options.RevocationValidationType = RevocationValidationType.Crl;
//Validate signature and get validation result
PdfSignatureValidationResult result = signatureField.ValidateSignature(options);

//Close the document
document.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Gets the stream from the document
FileStream documentStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);
//Loads an existing signed PDF document
PdfLoadedDocument document = new PdfLoadedDocument(documentStream);

//Gets the signature field
PdfLoadedSignatureField signatureField = document.Form.Fields[0] as PdfLoadedSignatureField;
//Signature validation options
PdfSignatureValidationOptions options = new PdfSignatureValidationOptions();
//Sets the revocation type
options.RevocationValidationType = RevocationValidationType.Crl;
//Validate signature and get validation result
PdfSignatureValidationResult result = signatureField.ValidateSignature(options);

//Close the document
document.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Gets the stream from the document
Stream documentStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");
//Loads an existing signed PDF document
PdfLoadedDocument document = new PdfLoadedDocument(documentStream);

//Gets the signature field
PdfLoadedSignatureField signatureField = document.Form.Fields[0] as PdfLoadedSignatureField;
//Signature validation options
PdfSignatureValidationOptions options = new PdfSignatureValidationOptions();
//Sets the revocation type
options.RevocationValidationType = RevocationValidationType.Crl;
//Validates signature and gets the validation result
PdfSignatureValidationResult result = signatureField.ValidateSignature(options);

//Close the document
document.Close(true);

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Digital%20Signature/Customized-revocation-validation/).

## Remove existing digital signatures from a PDF document 

The following code example illustrates how to remove existing digital signatures from a PDF document using [Remove](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfFieldCollection.html#Syncfusion_Pdf_Interactive_PdfFieldCollection_Remove_Syncfusion_Pdf_Interactive_PdfField_) method in [PdfLoadedFormFieldCollection](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedFormFieldCollection.html) class.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Load an existing PDF document.
PdfLoadedDocument pdfLoadedDocument = new PdfLoadedDocument("Input.pdf");

//Get the signature field from PDF form field collection.
PdfLoadedSignatureField signatureField = pdfLoadedDocument.Form.Fields[0] as PdfLoadedSignatureField;
//Remove signature field from form field collection.
pdfLoadedDocument.Form.Fields.Remove(signatureField);

//Save and close the PDF document.
pdfLoadedDocument.Save("RemoveDigital.pdf");
pdfLoadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Load an existing PDF document.
Dim pdfLoadedDocument As PdfLoadedDocument = New PdfLoadedDocument("Input.pdf")

'Get the signature field from PDF form field collection.
Dim signatureField As PdfLoadedSignatureField = TryCast(pdfLoadedDocument.Form.Fields(0), PdfLoadedSignatureField)
'Remove signature field from form field collection.
pdfLoadedDocument.Form.Fields.Remove(signatureField)

'Save and close the PDF document.
pdfLoadedDocument.Save("RemoveDigital.pdf")
pdfLoadedDocument.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Load an existing PDF document.
Stream docStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");
PdfLoadedDocument pdfLoadedDocument = new PdfLoadedDocument(docStream);

//Get the signature field from PDF form field collection.
PdfLoadedSignatureField signatureField = pdfLoadedDocument.Form.Fields[0] as PdfLoadedSignatureField;
//Remove signature field from form field collection.
pdfLoadedDocument.Form.Fields.Remove(signatureField);

//Save the PDF document to stream.
MemoryStream stream = new MemoryStream();
await pdfLoadedDocument.SaveAsync(stream);
//Close the document.
pdfLoadedDocument.Close(true);
//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.
Save(stream, "output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load an existing PDF document.
FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument pdfLoadedDocument = new PdfLoadedDocument(docStream);

//Get the signature field from PDF form field collection.
PdfLoadedSignatureField signatureField = pdfLoadedDocument.Form.Fields[0] as PdfLoadedSignatureField;
//Remove signature field from form field collection.
pdfLoadedDocument.Form.Fields.Remove(signatureField);

//Save the document into stream.
MemoryStream stream = new MemoryStream();
pdfLoadedDocument.Save(stream);
stream.Position = 0;
//Close the document.
pdfLoadedDocument.Close(true);
//Defining the ContentType for PDF file.
string contentType = "application/pdf";
//Define the file name.
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name.
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Load an existing PDF document.
Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");
PdfLoadedDocument pdfLoadedDocument = new PdfLoadedDocument(docStream);

//Get the signature field from PDF form field collection.
PdfLoadedSignatureField signatureField = pdfLoadedDocument.Form.Fields[0] as PdfLoadedSignatureField;
//Remove signature field from PdfLoadedDocument form field collection.
pdfLoadedDocument.Form.Fields.Remove(signatureField);

//Save the document to the stream.
MemoryStream stream = new MemoryStream();
pdfLoadedDocument.Save(stream);
//Close the document.
pdfLoadedDocument.Close(true);
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Digital%20Signature/Remove_existing_digital_signature_from_PDF/).

## Certified signature 

The following code snippet illustrates how to sign a PDF document without showing the digital signature using [Certificated](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSignature.html#Syncfusion_Pdf_Security_PdfSignature_Certificated) property in [PdfSignature](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfSignature.html) class.  

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Load an existing PDF document.
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");
//Load digital ID with password.
PdfCertificate certificate = new PdfCertificate(@"PDF.pfx", "password123");

//Create a signature with loaded digital ID.
PdfSignature signature = new PdfSignature(loadedDocument, loadedDocument.Pages[0], certificate, "DigitalSignature");
signature.Settings.CryptographicStandard = CryptographicStandard.CADES;
signature.Settings.DigestAlgorithm = DigestAlgorithm.SHA256;
//This property enables the author or certifying signature.
signature.Certificated = true;
//Allow the form fill and and comments.
signature.DocumentPermissions = PdfCertificationFlags.AllowFormFill | PdfCertificationFlags.AllowComments;

//Save and close the PDF document.
loadedDocument.Save("Certifying.pdf");
loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Load an existing PDF document.
Dim loadedDocument As PdfLoadedDocument = New PdfLoadedDocument("Input.pdf")
'Load digital ID with password. 
Dim certificate As PdfCertificate = New PdfCertificate("PDF.pfx", "password123")

'Create a signature with loaded digital ID. 
Dim signature As PdfSignature = New PdfSignature(loadedDocument, loadedDocument.Pages(0), certificate, "DigitalSignature")
signature.Settings.CryptographicStandard = CryptographicStandard.CADES
signature.Settings.DigestAlgorithm = DigestAlgorithm.SHA256
'This property enables the author or certifying signature.
signature.Certificated = True
'Allow the form fill and and comments. 
signature.DocumentPermissions = PdfCertificationFlags.AllowFormFill Or PdfCertificationFlags.AllowComments

'Save and close the PDF document.
loadedDocument.Save("Certifying.pdf")
loadedDocument.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Load an existing PDF document.
Stream docStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);
//Load digital ID with password. 
Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.PDF.pfx");
PdfCertificate certificate = new PdfCertificate(certificateStream, "password123");

//Create a signature with loaded digital ID.
PdfSignature signature = new PdfSignature(loadedDocument, loadedDocument.Pages[0], certificate, "DigitalSignature");
signature.Settings.CryptographicStandard = CryptographicStandard.CADES;
signature.Settings.DigestAlgorithm = DigestAlgorithm.SHA256;
//This property enables the author or certifying signature.
signature.Certificated = true;
//Allow the form fill and and comments.
signature.DocumentPermissions = PdfCertificationFlags.AllowFormFill | PdfCertificationFlags.AllowComments;

//Save the PDF document to stream.
MemoryStream stream = new MemoryStream();
await loadedDocument.SaveAsync(stream);
//Close the document.
loadedDocument.Close(true);
//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.
Save(stream, "output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Get stream from an existing PDF document. 
FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);
//Load digital ID with password.
FileStream certificateStream = new FileStream("PDF.pfx", FileMode.Open, FileAccess.Read);
PdfCertificate certificate = new PdfCertificate(certificateStream, "password123");

//Create a signature with loaded digital ID.
PdfSignature signature = new PdfSignature(loadedDocument, loadedDocument.Pages[0], certificate, "DigitalSignature");
signature.Settings.CryptographicStandard = CryptographicStandard.CADES;
signature.Settings.DigestAlgorithm = DigestAlgorithm.SHA256;
//This property enables the author or certifying signature.
signature.Certificated = true;
//Allow the form fill and and comments.
signature.DocumentPermissions = PdfCertificationFlags.AllowFormFill | PdfCertificationFlags.AllowComments;

//Save the document into stream.
MemoryStream stream = new MemoryStream();
document.Save(stream);
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

//Load an existing PDF document. 
Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);
//Load an existing PDF document.
Stream certificateStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.PDF.pfx");
PdfCertificate certificate = new PdfCertificate(certificateStream, "password123");

//Create a signature with loaded digital ID.
PdfSignature signature = new PdfSignature(loadedDocument, loadedDocument.Pages[0], certificate, "DigitalSignature");
signature.Settings.CryptographicStandard = CryptographicStandard.CADES;
signature.Settings.DigestAlgorithm = DigestAlgorithm.SHA256;
//This property enables the author or certifying signature.
signature.Certificated = true;
//Allow the form fill and and comments.
signature.DocumentPermissions = PdfCertificationFlags.AllowFormFill | PdfCertificationFlags.AllowComments;

//Save the document to the stream.
MemoryStream stream = new MemoryStream();
pdfLoadedDocument.Save(stream);
//Close the document.
pdfLoadedDocument.Close(true);
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Digital%20Signature/Sign-PDF-without-showing-digital-signature/).

## Retrieve digital signature information from an existing PDF document 

The following code snippet illustrates how to retrieve digital signature information from an existing PDF document using [IssuerName](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfCertificate.html#Syncfusion_Pdf_Security_PdfCertificate_IssuerName), [ValidFrom](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfCertificate.html#Syncfusion_Pdf_Security_PdfCertificate_ValidFrom), and [ValidTo](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfCertificate.html#Syncfusion_Pdf_Security_PdfCertificate_ValidTo) property. 

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Load an existing PDF document.
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");

//Get the signature field from PdfLoadedDocument form field collection.
PdfLoadedSignatureField signatureField = loadedDocument.Form.Fields[0] as PdfLoadedSignatureField;
PdfSignature signature = signatureField.Signature;

//Extract the signature information.
Console.WriteLine("Digitally Signed by: " + signature.Certificate.IssuerName);
Console.WriteLine("Valid From: " + signature.Certificate.ValidFrom);
Console.WriteLine("Valid To: " + signature.Certificate.ValidTo);
Console.WriteLine("Hash Algorithm : " + signature.Settings.DigestAlgorithm);
Console.WriteLine("Cryptographics Standard : " + signature.Settings.CryptographicStandard);

//Close the document.
loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Load an existing PDF document. 
Dim loadedDocument As PdfLoadedDocument = New PdfLoadedDocument("Input.pdf")

'Get the signature field from PdfLoadedDocument form field collection.
Dim signatureField As PdfLoadedSignatureField = TryCast(loadedDocument.Form.Fields(0), PdfLoadedSignatureField)
Dim signature As PdfSignature = signatureField.Signature

'Extract the signature information.
Console.WriteLine("Digitally Signed by: " & signature.Certificate.IssuerName)
Console.WriteLine("Valid From: " & signature.Certificate.ValidFrom)
Console.WriteLine("Valid To: " & signature.Certificate.ValidTo)
Console.WriteLine("Hash Algorithm : " & signature.Settings.DigestAlgorithm)
Console.WriteLine("Cryptographics Standard : " & signature.Settings.CryptographicStandard)

'Close the document.
loadedDocument.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Load an existing PDF document.
Stream docStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Get the signature field from PdfLoadedDocument form field collection.
PdfLoadedSignatureField signatureField = loadedDocument.Form.Fields[0] as PdfLoadedSignatureField;
PdfSignature signature = signatureField.Signature;

//Extract the signature information.
Console.WriteLine("Digitally Signed by: " + signature.Certificate.IssuerName);
Console.WriteLine("Valid From: " + signature.Certificate.ValidFrom);
Console.WriteLine("Valid To: " + signature.Certificate.ValidTo);
Console.WriteLine("Hash Algorithm : " + signature.Settings.DigestAlgorithm);
Console.WriteLine("Cryptographics Standard : " + signature.Settings.CryptographicStandard);

//Close the document.
loadedDocument.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Get stream from an existing PDF document. 
FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Get the signature field from PdfLoadedDocument form field collection.
PdfLoadedSignatureField signatureField = loadedDocument.Form.Fields[0] as PdfLoadedSignatureField;
PdfSignature signature = signatureField.Signature;

//Extract the signature information.
Console.WriteLine("Digitally Signed by: " + signature.Certificate.IssuerName);
Console.WriteLine("Valid From: " + signature.Certificate.ValidFrom);
Console.WriteLine("Valid To: " + signature.Certificate.ValidTo);
Console.WriteLine("Hash Algorithm : " + signature.Settings.DigestAlgorithm);
Console.WriteLine("Cryptographics Standard : " + signature.Settings.CryptographicStandard);

//Close the document.
loadedDocument.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Load an existing PDF document. 
Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Get the signature field from PdfLoadedDocument form field collection.
PdfLoadedSignatureField signatureField = loadedDocument.Form.Fields[0] as PdfLoadedSignatureField;
PdfSignature signature = signatureField.Signature;

//Extract the signature information.
Console.WriteLine("Digitally Signed by: " + signature.Certificate.IssuerName);
Console.WriteLine("Valid From: " + signature.Certificate.ValidFrom);
Console.WriteLine("Valid To: " + signature.Certificate.ValidTo);
Console.WriteLine("Hash Algorithm : " + signature.Settings.DigestAlgorithm);
Console.WriteLine("Cryptographics Standard : " + signature.Settings.CryptographicStandard);

//Close the document.
loadedDocument.Close(true);

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Digital%20Signature/Retrieve-digital-signature-information-from-PDF/).

## Adding multiple signatures to a PDF document

The following code example illustrates how to add multiple signatures to a PDF document without invalidating the previous signature.  

N> It is recommended to use licensed assemblies or registered license keys in your respective applications to add multiple digital signatures to the PDF documents without invalidating the previous signatures. 

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Load an existing PDF document. 
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");
//Get the first page of the document.
PdfLoadedPage page = loadedDocument.Pages[0] as PdfLoadedPage;

//Get the first signature field of the PDF document.
PdfLoadedSignatureField signatureField1 = loadedDocument.Form.Fields[0] as PdfLoadedSignatureField;
//Create a certificate instance from a PFX file with a private key.
PdfCertificate certificate1 = new PdfCertificate("PDF.pfx", "password123");
//Add a signature to the signature field.
signatureField1.Signature = new PdfSignature(loadedDocument, page, certificate1, "Signature", signatureField1);
//Set an image for the signature field.
PdfBitmap signatureImage = new PdfBitmap(@"Student Signature.jpg");
//Insert an image in the signature appearance. 
signatureField1.Signature.Appearance.Normal.Graphics.DrawImage(signatureImage, 0, 0, 90, 20);

//Save the document into the stream.
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);

//Load the signed PDF document.
PdfLoadedDocument signedDocument = new PdfLoadedDocument(stream);
//Load the PDF page.
PdfLoadedPage loadedPage = signedDocument.Pages[0] as PdfLoadedPage;

//Get the first signature field of the PDF document.
PdfLoadedSignatureField signatureField2 = signedDocument.Form.Fields[1] as PdfLoadedSignatureField;
//Add a signature to the signature field. 
signatureField2.Signature = new PdfSignature(signedDocument, loadedPage, certificate1, "Signature", signatureField2);
//Set an image for the signature field.
PdfBitmap signatureImage1 = new PdfBitmap(@"Teacher Signature.png");
//Draw an image in the signature appearance. 
signatureField2.Signature.Appearance.Normal.Graphics.DrawImage(signatureImage1, 0, 0, 90, 20);

//Save the PDF document. 
signedDocument.Save("Multiple_signature.pdf");
//Close the PDF documents. 
signedDocument.Close(true);
loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Load an existing PDF document. 
Dim loadedDocument As PdfLoadedDocument = New PdfLoadedDocument("Input.pdf")
'Get the first page of the document.
Dim page As PdfLoadedPage = TryCast(loadedDocument.Pages(0), PdfLoadedPage)

'Get the first signature field of the PDF document.
Dim signatureField1 As PdfLoadedSignatureField = TryCast(loadedDocument.Form.Fields(0), PdfLoadedSignatureField)
'Create a certificate instance from the PFX file with a private key.
Dim certificate1 As PdfCertificate = New PdfCertificate("PDF.pfx", "password123")
'Add a signature to the signature field. 
signatureField1.Signature = New PdfSignature(loadedDocument, page, certificate1, "Signature", signatureField1
'Set an image for the signature field.
Dim signatureImage As PdfBitmap = New PdfBitmap("Student Signature.jpg")
'Draw an image in the signature appearance. 
signatureField1.Signature.Appearance.Normal.Graphics.DrawImage(signatureImage, 0, 0, 90, 20)

'Save the document into the stream.
Dim stream As MemoryStream = New MemoryStream()
loadedDocument.Save(stream)

'Load the signed PDF document.
Dim signedDocument As PdfLoadedDocument = New PdfLoadedDocument(stream)
'Load the PDF page.
Dim loadedPage As PdfLoadedPage = TryCast(signedDocument.Pages(0), PdfLoadedPage)

'Get the first signature field of the PDF document.
Dim signatureField2 As PdfLoadedSignatureField = TryCast(signedDocument.Form.Fields(1), PdfLoadedSignatureField)
signatureField2.Signature = New PdfSignature(signedDocument, loadedPage, certificate1, "Signature", signatureField2)
'Set an image for the signature field.
Dim signatureImage1 As PdfBitmap = New PdfBitmap("Teacher Signature.png")
'Draw an image in the signature appearance. 
signatureField2.Signature.Appearance.Normal.Graphics.DrawImage(signatureImage1, 0, 0, 90, 20)

'Save the PDF document. 
signedDocument.Save("Multiple_signature.pdf")
'Close the PDF documents. 
signedDocument.Close(True)
loadedDocument.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Load the file as a stream.
Stream inputStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");
//Load an existing PDF document. 
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(inputStream);
//Get the first page of the document.
PdfLoadedPage page = loadedDocument.Pages[0] as PdfLoadedPage;

//Get the first signature field of the PDF document.
PdfLoadedSignatureField signatureField1 = loadedDocument.Form.Fields[0] as PdfLoadedSignatureField;
//Get the certificate as a stream. 
Stream certificateStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.PDF.pfx");
//Creates a certificate instance from the PFX file with a private key.
PdfCertificate certificate1 = new PdfCertificate(certificateStream, "password123");
//Add a signature to the signature field.
signatureField1.Signature = new PdfSignature(loadedDocument, page, certificate1, "Signature", signatureField1);
//Get the image as a stream. 
Stream imageStream1 = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Student Signature.jpg");
//Set an image for the signature field.
PdfBitmap signatureImage = new PdfBitmap(imageStream1);
//Insert the image in the signature appearance. 
signatureField1.Signature.Appearance.Normal.Graphics.DrawImage(signatureImage, 0, 0, 90, 20);

//Save the document into the stream.
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);

//Load the signed PDF document.
PdfLoadedDocument signedDocument = new PdfLoadedDocument(stream);
//Load the PDF page.
PdfLoadedPage loadedPage = signedDocument.Pages[0] as PdfLoadedPage;

//Get the first signature field of the PDF document.
PdfLoadedSignatureField signatureField2 = signedDocument.Form.Fields[1] as PdfLoadedSignatureField;
//Add the signature to the signature field. 
signatureField2.Signature = new PdfSignature(signedDocument, loadedPage, certificate1, "Signature", signatureField2);
//Get the image as a stream. 
Stream imageStream2 = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Teacher Signature.png");
//Sets an image for the signature field.
PdfBitmap signatureImage1 = new PdfBitmap(imageStream2);
//Draw an image in the signature appearance. 
signatureField2.Signature.Appearance.Normal.Graphics.DrawImage(signatureImage1, 0, 0, 90, 20);

//Create a memory stream.
MemoryStream ms = new MemoryStream();
//Open the document in a browser after saving it.
signedDocument.Save(ms);
//Close the documents.
signedDocument.Close(true);
loadedDocument.Close(true);
//Save the PDF document. 
Save(ms, "Multiple_signature.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load the PDF document.
FileStream docStream = new FileStream("SignatureFields.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);
//Get the first page of the document.
PdfLoadedPage page = loadedDocument.Pages[0] as PdfLoadedPage;

//Get the first signature field of the PDF document.
PdfLoadedSignatureField signatureField1 = loadedDocument.Form.Fields[0] as PdfLoadedSignatureField;
//Creates a certificate.
FileStream certificateStream1 = new FileStream("PDF.pfx", FileMode.Open, FileAccess.Read);
PdfCertificate certificate1 = new PdfCertificate(certificateStream1, "password123");
//Add signature to the signature field.
signatureField1.Signature = new PdfSignature(loadedDocument, page, certificate1, "Signature", signatureField1);
//Get the image as a stream. 
FileStream imageStream = new FileStream("Student Signature.jpg", FileMode.Open, FileAccess.Read);
PdfBitmap signatureImage = new PdfBitmap(imageStream);
//Draw an image in signature appearance. 
signatureField1.Signature.Appearance.Normal.Graphics.DrawImage(signatureImage, 0, 0, 90, 20);

//Save the document into the stream.
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);

//Load the signed PDF document.
PdfLoadedDocument signedDocument = new PdfLoadedDocument(stream);
//Load the PDF page.
PdfLoadedPage loadedPage = signedDocument.Pages[0] as PdfLoadedPage;

//Get the first signature field of the PDF document.
PdfLoadedSignatureField signatureField2 = signedDocument.Form.Fields[1] as PdfLoadedSignatureField;
//Add the signature to the signature field. 
signatureField1.Signature = new PdfSignature(signedDocument, loadedPage, certificate1, "Signature", signatureField2);
//Load the image as a stream. 
FileStream imageStream1 = new FileStream("Teacher Signature.png", FileMode.Open, FileAccess.Read);
PdfBitmap signatureImage1 = new PdfBitmap(imageStream1);
//Draw the image in signature appearance. 
signatureField1.Signature.Appearance.Normal.Graphics.DrawImage(signatureImage1, 0, 0, 90, 20);

//Saving the PDF to the MemoryStream.
MemoryStream signedStream = new MemoryStream();
signedDocument.Save(signedStream);
//Set the position as '0'.
signedStream.Position = 0;
//Close the documents. 
signedDocument.Close(true);
loadedDocument.Close(true);
//Defining the ContentType for a pdf file.
string contentType = "application/pdf";
//Define the file name.
string fileName = "Multiple_Signature.pdf";
//Create the FileContentResult object by using the file contents, content type, and file name. 
return File(signedStream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

//Load the file as a stream.
Stream inputStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");
//Load an existing PDF document. 
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(inputStream);
//Get the first page of the document.
PdfLoadedPage page = loadedDocument.Pages[0] as PdfLoadedPage;

//Get the first signature field of the PDF document.
PdfLoadedSignatureField signatureField1 = loadedDocument.Form.Fields[0] as PdfLoadedSignatureField;
//Get the certificate as a stream. 
Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.PDF.pfx");
//Create a certificate instance from a PFX file with the private key.
PdfCertificate certificate1 = new PdfCertificate(certificateStream, "password123");
//Add a signature to the signature field.
signatureField1.Signature = new PdfSignature(loadedDocument, page, certificate1, "Signature", signatureField1);
//Get the image as a stream. 
Stream imageStream1 = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Student Signature.jpg");
//Set an image for the signature field.
PdfBitmap signatureImage = new PdfBitmap(imageStream1);
//Insert image in the signature appearance. 
signatureField1.Signature.Appearance.Normal.Graphics.DrawImage(signatureImage, 0, 0, 90, 20);

//Save the document into the stream.
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);

//Load the signed PDF document.
PdfLoadedDocument signedDocument = new PdfLoadedDocument(stream);
//Load the PDF page.
PdfLoadedPage loadedPage = signedDocument.Pages[0] as PdfLoadedPage;

//Gets the first signature field of the PDF document.
PdfLoadedSignatureField signatureField2 = signedDocument.Form.Fields[1] as PdfLoadedSignatureField;
//Add signature to the signature field. 
signatureField2.Signature = new PdfSignature(signedDocument, loadedPage, certificate1, "Signature", signatureField2);
//Get the image as a stream. 
Stream imageStream2 = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Teacher Signature.png");
//Sets an image for the signature field.
PdfBitmap signatureImage1 = new PdfBitmap(imageStream2);
//Draw an image in the signature appearance. 
signatureField2.Signature.Appearance.Normal.Graphics.DrawImage(signatureImage1, 0, 0, 90, 20);

//Save the document to the stream. 
MemoryStream ms = new MemoryStream();
signedDocument.Save(ms);
//Close the documents.
signedDocument.Close(true);
loadedDocument.Close(true);
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Digital%20Signature/Multiple-digital-signature/).
