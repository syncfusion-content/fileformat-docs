---
title: Working with Digital Signature | Syncfusion
description: This section explains how to create a Digital Signature in the PDF document by using Essential PDF
platform: file-formats
control: PDF
documentation: UG
---
# Working with Digital Signature

## Adding a digital signature

Essential PDF allows you to add digital signature to the PDF document. In order to add digital signature, you can need a certificate with private keys. Essential PDF provides support for digital signature by using PFX files, Hardware Security Module(HSM), Online Certificate Status Protocol (OCSP), Certificate Revocation List (CRL) and Windows Certificate Store.

The following code example illustrates how to add a digital signature in the PDF document.
{% tabs %}
{% highlight c# %}

//Creates a new PDF document.

PdfDocument document = new PdfDocument();

//Adds a new page.

PdfPageBase page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from PFX file with private key.

PdfCertificate pdfCert = new PdfCertificate(@"PDF.pfx", "syncfusion");

//Creates a digital signature.

PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");

//Sets an image for signature field.

PdfBitmap signatureImage = new PdfBitmap(@"signature.jpg");

//Sets signature information

signature.Bounds = new RectangleF(new PointF(0, 0), signatureImage.PhysicalDimension);

signature.ContactInfo = "johndoe@owned.us";

signature.LocationInfo = "Honolulu, Hawaii";

signature.Reason = "I am author of this document.";

//Draws the signature image.

graphics.DrawImage(signatureImage, 0, 0);

//Saves and closes the document.

document.Save("Output.pdf");

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}

'Creates a new PDF document.

Dim document As New PdfDocument()

'Adds a new page.

Dim page As PdfPageBase = document.Pages.Add()

Dim graphics As PdfGraphics = page.Graphics

'Creates a certificate instance from PFX file with private key.

Dim pdfCert As New PdfCertificate("PDF.pfx", "syncfusion")

'Creates a digital signature.

Dim signature As New PdfSignature(document, page, pdfCert, "Signature")

'Sets an image for signature field.

Dim signatureImage As New PdfBitmap("signature.jpg")

'Sets signature info.

signature.Bounds = New RectangleF(New PointF(0, 0), signatureImage.PhysicalDimension)

signature.ContactInfo = "johndoe@owned.us"

signature.LocationInfo = "Honolulu, Hawaii"

signature.Reason = "I am author of this document."

'Draws the signature image.

graphics.DrawImage(signatureImage, 0, 0)

'Saves and closes the document.

document.Save("Output.pdf")

document.Close(True)



{% endhighlight %}

{% highlight UWP %}

//Creates a new PDF document.

PdfDocument document = new PdfDocument();

//Adds a new page.

PdfPageBase page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from PFX file with private key.

Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.PDF.pfx");

PdfCertificate pdfCert = new PdfCertificate(certificateStream, "syncfusion");

//Creates a digital signature.

PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");

//Sets an image for signature field.

Stream imageStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.signature.jpg");

PdfBitmap signatureImage = new PdfBitmap(imageStream);

//Sets signature information

signature.Bounds = new RectangleF(new PointF(0, 0), signatureImage.PhysicalDimension);

signature.ContactInfo = "johndoe@owned.us";

signature.LocationInfo = "Honolulu, Hawaii";

signature.Reason = "I am author of this document.";

//Draws the signature image.

graphics.DrawImage(signatureImage, 0, 0);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document

document.Close(true);                                                                   

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Creates a new PDF document.

PdfDocument document = new PdfDocument();

//Adds a new page.

PdfPageBase page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from PFX file with private key.

FileStream certificateStream = new FileStream("PDF.pfx", FileMode.Open, FileAccess.Read);

PdfCertificate pdfCert = new PdfCertificate(certificateStream, "syncfusion");

//Creates a digital signature.

PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");

//Sets an image for signature field.

FileStream imageStream = new FileStream("signature.jpg", FileMode.Open, FileAccess.Read);

//Sets an image for signature field.

PdfBitmap signatureImage = new PdfBitmap(imageStream);

//Sets signature information

signature.Bounds = new RectangleF(new PointF(0, 0), signatureImage.PhysicalDimension);

signature.ContactInfo = "johndoe@owned.us";

signature.LocationInfo = "Honolulu, Hawaii";

signature.Reason = "I am author of this document.";

//Draws the signature image.

graphics.DrawImage(signatureImage, 0, 0);

//Save the document into stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

stream.Position = 0;

//Close the documents.

document.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Creates a new PDF document.

PdfDocument document = new PdfDocument();

//Adds a new page.

PdfPageBase page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from PFX file with private key.

Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.PDF.pfx");

PdfCertificate pdfCert = new PdfCertificate(certificateStream, "syncfusion");

//Creates a digital signature.

PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");

//Sets an image for signature field.

Stream imageStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.signature.jpg");

PdfBitmap signatureImage = new PdfBitmap(imageStream);

//Sets signature information

signature.Bounds = new RectangleF(new PointF(0, 0), signatureImage.PhysicalDimension);

signature.ContactInfo = "johndoe@owned.us";

signature.LocationInfo = "Honolulu, Hawaii";

signature.Reason = "I am author of this document.";

//Draws the signature image.

graphics.DrawImage(signatureImage, 0, 0);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Closes the document

document.Close(true);

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

## Adding a digital signature using stream

The following code example illustrates how to add a digital signature in the PDF document
using stream as follows.

{% tabs %}
{% highlight c# %}

//Creates a new PDF document.

PdfDocument document = new PdfDocument();

//Adds a new page.

PdfPageBase page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

//Gets a stream from .pfx file.

Stream pfxStream = File.OpenRead("PDF.pfx");

//Creates a certificate instance from PFX file stream with private key.

PdfCertificate pdfCert = new PdfCertificate(pfxStream, "syncfusion");

//Creates a digital signature.

PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");

//Sets an image for signature field.

PdfBitmap signatureImage = new PdfBitmap(@"signature.jpg");

//Sets signature information

signature.Bounds = new RectangleF(new PointF(0, 0), signatureImage.PhysicalDimension);

signature.ContactInfo = "johndoe@owned.us";

signature.LocationInfo = "Honolulu, Hawaii";

signature.Reason = "I am author of this document.";

//Draws the signature image.

graphics.DrawImage(signatureImage, 0, 0);

//Saves and closes the document.

document.Save("Output.pdf");

document.Close(true);

{% endhighlight %}
{% highlight vb.net %}
 
'Creates a new PDF document.

Dim document As New PdfDocument()

'Adds a new page.

Dim page As PdfPageBase = document.Pages.Add()

Dim graphics As PdfGraphics = page.Graphics

'Gets stream from .pfx file.

Dim pfxStream As Stream = File.OpenRead("PDF.pfx")

'Creates a certificate instance from PFX file stream with private key.

Dim pdfCert As New PdfCertificate(pfxStream, "syncfusion")

'Creates a digital signature.

Dim signature As New PdfSignature(document, page, pdfCert, "Signature")

'Sets an image for signature field.

Dim signatureImage As New PdfBitmap("signature.jpg")

'Sets signature information.

signature.Bounds = New RectangleF(New PointF(0, 0), signatureImage.PhysicalDimension)

signature.ContactInfo = "johndoe@owned.us"

signature.LocationInfo = "Honolulu, Hawaii"

signature.Reason = "I am author of this document."

'Draws the signature image.

graphics.DrawImage(signatureImage, 0, 0)

'Saves and closes the document.

document.Save("Output.pdf")

document.Close(True)

{% endhighlight %}

{% highlight UWP %}

//Creates a new PDF document.

PdfDocument document = new PdfDocument();

//Adds a new page.

PdfPageBase page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from PFX file with private key.

Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.

PdfCertificate pdfCert = new PdfCertificate(certificateStream, "syncfusion");

//Creates a digital signature.

PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");

//Sets an image for signature field.

Stream imageStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.signature.jpg");

PdfBitmap signatureImage = new PdfBitmap(imageStream);

//Sets signature information

signature.Bounds = new RectangleF(new PointF(0, 0), signatureImage.PhysicalDimension);

signature.ContactInfo = "johndoe@owned.us";

signature.LocationInfo = "Honolulu, Hawaii";

signature.Reason = "I am author of this document.";

//Draws the signature image.

graphics.DrawImage(signatureImage, 0, 0);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document

document.Close(true);                                                                   

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Creates a new PDF document.

PdfDocument document = new PdfDocument();

//Adds a new page.

PdfPageBase page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from PFX file with private key.

FileStream certificateStream = new FileStream("PDF.pfx", FileMode.Open, FileAccess.Read);

PdfCertificate pdfCert = new PdfCertificate(certificateStream, "syncfusion");

//Creates a digital signature.

PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");

//Sets an image for signature field.

FileStream imageStream = new FileStream("signature.jpg", FileMode.Open, FileAccess.Read);

//Sets an image for signature field.

PdfBitmap signatureImage = new PdfBitmap(imageStream);

//Sets signature information

signature.Bounds = new RectangleF(new PointF(0, 0), signatureImage.PhysicalDimension);

signature.ContactInfo = "johndoe@owned.us";

signature.LocationInfo = "Honolulu, Hawaii";

signature.Reason = "I am author of this document.";

//Draws the signature image.

graphics.DrawImage(signatureImage, 0, 0);

//Save the document into stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

stream.Position = 0;

//Close the documents.

document.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Creates a new PDF document.

PdfDocument document = new PdfDocument();

//Adds a new page.

PdfPageBase page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from PFX file with private key.

Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.PDF.pfx");

PdfCertificate pdfCert = new PdfCertificate(certificateStream, "syncfusion");

//Creates a digital signature.

PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");

//Sets an image for signature field.

Stream imageStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.signature.jpg");

PdfBitmap signatureImage = new PdfBitmap(imageStream);

//Sets signature information

signature.Bounds = new RectangleF(new PointF(0, 0), signatureImage.PhysicalDimension);

signature.ContactInfo = "johndoe@owned.us";

signature.LocationInfo = "Honolulu, Hawaii";

signature.Reason = "I am author of this document.";

//Draws the signature image.

graphics.DrawImage(signatureImage, 0, 0);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Closes the document

document.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples

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
{% highlight c# %}
 
//Loads the PDF document with signature field.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");         

//Gets the page.

PdfLoadedPage page = loadedDocument.Pages[0] as PdfLoadedPage;

//Creates a signature field.

PdfSignatureField signatureField = new PdfSignatureField(page, "SignatureField");

signatureField.Bounds = new RectangleF(0, 0, 100, 100);

signatureField.Signature = new PdfSignature();

//Adds certificate to the signature field.

signatureField.Signature.Certificate = new PdfCertificate(@"PDF.pfx", "syncfusion");

signatureField.Signature.Reason = "I am author of this document";

//Adds the field.

loadedDocument.Form.Fields.Add(signatureField);

//Saves the certified PDF document.

loadedDocument.Save(@"Output.pdf");

loadedDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}
'Loads the PDF document with signature field.

Dim loadedDocument As New PdfLoadedDocument("Input.pdf")

'Gets the page.

Dim page As PdfLoadedPage = TryCast(loadedDocument.Pages(0), PdfLoadedPage)

'Creates a signature field.

Dim signatureField As New PdfSignatureField(page, "SignatureField")

signatureField.Bounds = New RectangleF(0, 0, 100, 100)

signatureField.Signature = New PdfSignature()

'Adds certificate to the signature field.

signatureField.Signature.Certificate = New PdfCertificate("PDF.pfx", "syncfusion")

signatureField.Signature.Reason = "I am author of this document"

'Adds the field.

loadedDocument.Form.Fields.Add(signatureField)

'Saves the certified PDF document.

loadedDocument.Save("Output.pdf")

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

//Gets the page.

PdfLoadedPage page = loadedDocument.Pages[0] as PdfLoadedPage;

//Creates a signature field.

PdfSignatureField signatureField = new PdfSignatureField(page, "SignatureField");

signatureField.Bounds = new RectangleF(0, 0, 100, 100);

signatureField.Signature = new PdfSignature();

//Adds certificate to the signature field.

Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.

signatureField.Signature.Certificate = new PdfCertificate(certificateStream, "syncfusion");

signatureField.Signature.Reason = "I am author of this document";

//Adds the field.

loadedDocument.Form.Fields.Add(signatureField);

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

FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Gets the page.

PdfLoadedPage page = loadedDocument.Pages[0] as PdfLoadedPage;

//Creates a signature field.

PdfSignatureField signatureField = new PdfSignatureField(page, "SignatureField");

signatureField.Bounds = new RectangleF(0, 0, 100, 100);

signatureField.Signature = new PdfSignature();

//Adds certificate to the signature field.

FileStream certificateStream = new FileStream("PDF.pfx", FileMode.Open, FileAccess.Read);

signatureField.Signature.Certificate = new PdfCertificate(certificateStream, "syncfusion");

signatureField.Signature.Reason = "I am author of this document";

//Adds the field.

loadedDocument.Form.Fields.Add(signatureField);

//Save the document into stream.

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

stream.Position = 0;

//Close the documents.

loadedDocument.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Gets the page.

PdfLoadedPage page = loadedDocument.Pages[0] as PdfLoadedPage;

//Creates a signature field.

PdfSignatureField signatureField = new PdfSignatureField(page, "SignatureField");

signatureField.Bounds = new RectangleF(0, 0, 100, 100);

signatureField.Signature = new PdfSignature();

//Adds certificate to the signature field.

Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.PDF.pfx");

signatureField.Signature.Certificate = new PdfCertificate(certificateStream, "syncfusion");

signatureField.Signature.Reason = "I am author of this document";

//Adds the field.

loadedDocument.Form.Fields.Add(signatureField);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Closes the document

loadedDocument.Close(true);

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

## Adding a digital signature using X509Certificate2

The following code example illustrates how to add digital signature in a PDF document using X509Certificate2 as follows.

{% tabs %}

{% highlight c# %}

//Creates a new PDF document

PdfDocument document = new PdfDocument();

//Adds a new page  

PdfPage page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from PFX file with private key  

X509Certificate2 certificate = new X509Certificate2("PDF.pfx", "syncfusion");

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

{% highlight vb.net %}

'Creates a new PDF document

Dim document As New PdfDocument()

'Adds a new page  

Dim page As PdfPage = document.Pages.Add()

Dim graphics As PdfGraphics = page.Graphics

'Creates a certificate instance from PFX file with private key  

Dim certificate As New X509Certificate2("PDF.pfx", "syncfusion")

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

{% highlight UWP %}

//Essential PDF supports adding a digital signature using X509Certificate2 only in Windows Forms, WPF, ASP.NET, ASP.NET MVC and ASP.NET Core platforms. 

{% endhighlight %}

{% highlight ASP.NET Core %}

//Creates a new PDF document

PdfDocument document = new PdfDocument();

//Adds a new page  

PdfPage page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from PFX file with private key  

X509Certificate2 certificate = new X509Certificate2("PDF.pfx", "syncfusion");

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

//Defining the ContentType for PDF file

string contentType = "application/pdf";

//Define the file name

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Creates a new PDF document

PdfDocument document = new PdfDocument();

//Adds a new page  

PdfPage page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from PFX file with private key  

Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.PDF.pfx");

MemoryStream ms = new MemoryStream();
certificateStream.CopyTo(ms);

X509Certificate2 certificate = new X509Certificate2(ms.ToArray(), "syncfusion");

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

## Adding a digital signature using Windows Certificate Store

Essential PDF supports adding digital signature to a PDF document from Windows Certificate Store. The following code snippet explains this.

{% tabs %}
{% highlight C# %}
//Create a new PDF document
PdfDocument document = new PdfDocument();

//Add page to the document
PdfPage page = document.Pages.Add();

//Get the certificate from store
PdfCertificate certificate = PdfCertificate.FindBySubject(StoreType.ROOT, "syncfusion");

//Load the image into PdfImage
PdfImage image = PdfImage.FromFile("Logo.png");

//Add the signature
PdfSignature signature = new PdfSignature(document, page, certificate, "Signature 1");
            
//Set the appearance for signature
signature.Bounds = new RectangleF(new PointF(5, 5), new SizeF(image.Width, image.Height + 100));
signature.ContactInfo = "johndoe@owned.us";
signature.LocationInfo = "Honolulu, Hawaii";
signature.Reason = "I am author of this document.";

string validto = "Valid To: " + signature.Certificate.ValidTo.ToString();
string validfrom = "Valid From: " + signature.Certificate.ValidFrom.ToString();

//Create a solid brush
PdfSolidBrush brush = new PdfSolidBrush(new PdfColor(1, 1, 255));

//Create a PdfPen
PdfPen pen = new PdfPen(brush, 1);

//Initialize a standard font
PdfFont font = new PdfStandardFont(PdfFontFamily.Courier, 12, PdfFontStyle.Regular);

//Initialize PdfGraphics
PdfGraphics g = signature.Appearance.Normal.Graphics;

//Draw the image
g.DrawImage(image, 0, 0);

//Draw string
g.DrawString(validfrom, font, pen, brush, 0, image.Height);
g.DrawString(validto, font, pen, brush, 0, image.Height + 50);

//Save the PDF document
document.Save("Output.pdf");

//Close the instance of PdfDocument
document.Close(true);
{% endhighlight %}

{% highlight vb.net %}
'Create a new PDF document
Dim document As PdfDocument = New PdfDocument

'Add page to the document
Dim page As PdfPage = document.Pages.Add

'Get the certificate from store
Dim certificate As PdfCertificate = PdfCertificate.FindBySubject(StoreType.ROOT, "syncfusion")

'Load the image into PdfImage
Dim image As PdfImage = PdfImage.FromFile("Logo.png")

'Add the signature
Dim signature As PdfSignature = New PdfSignature(document, page, certificate, "Signature 1")

'Set the appearance for signature
signature.Bounds = New RectangleF(New PointF(5, 5), New SizeF(image.Width, (image.Height + 100)))
signature.ContactInfo = "johndoe@owned.us"
signature.LocationInfo = "Honolulu, Hawaii"
signature.Reason = "I am author of this document."

Dim validto As String = ("Valid To: " + signature.Certificate.ValidTo.ToString)
Dim validfrom As String = ("Valid From: " + signature.Certificate.ValidFrom.ToString)

'Create a solid brush
Dim brush As PdfSolidBrush = New PdfSolidBrush(New PdfColor(1, 1, 255))

'Create a PdfPen
Dim pen As PdfPen = New PdfPen(brush, 1)

'Initialize a standard font
Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Courier, 12, PdfFontStyle.Regular)

'Initialize PdfGraphics
Dim g As PdfGraphics = signature.Appearance.Normal.Graphics

'Draw the image
g.DrawImage(image, 0, 0)

'Draw string
g.DrawString(validfrom, font, pen, brush, 0, image.Height)
g.DrawString(validto, font, pen, brush, 0, (image.Height + 50))

'Save the PDF document
document.Save("Output.pdf")

'Close the instance of PdfDocument
document.Close(True)
{% endhighlight %}
{% endtabs %}

You can get all the certificates available from the store by using the following code snippet.

{% tabs %}
{% highlight C# %}
PdfCertificate[] certificates = PdfCertificate.GetCertificates();

//Method to get all the PdfCertificate list
public static PdfCertificate[] GetPDFCertificates()
{
    //Get the certificate collection
    List<PdfCertificate> certCollection = new List<PdfCertificate>();

    GetStoreCertificates(StoreName.My, certCollection);
    GetStoreCertificates(StoreName.CertificateAuthority, certCollection);
    GetStoreCertificates(StoreName.Root, certCollection);
    return certCollection.ToArray();
}

private static void GetStoreCertificates(StoreName name, List<PdfCertificate> certList)
{
    //Set the store location to local machine
    X509Store store = new X509Store(name, StoreLocation.LocalMachine);
    store.Open(OpenFlags.MaxAllowed);
    foreach (X509Certificate2 x509Cert in store.Certificates)
    {
        //PdfCertificate constructor to load the X509Certificate directly
        PdfCertificate cert = new PdfCertificate(x509Cert);
        certList.Add(cert);
    }
}
{% endhighlight %}

{% highlight vb.net %}
Dim certificates() As PdfCertificate = PdfCertificate.GetCertificates()

'Method to get all the PdfCertificate list
Public Function GetPDFCertificates() As PdfCertificate()
    'Get the certificate collection
    Dim certCollection As List(Of PdfCertificate) = New List(Of PdfCertificate)

    GetStoreCertificates(StoreName.My, certCollection)
    GetStoreCertificates(StoreName.CertificateAuthority, certCollection)
    GetStoreCertificates(StoreName.Root, certCollection)
    Return certCollection.ToArray
End Function

Private Sub GetStoreCertificates(ByVal name As StoreName, ByVal certList As List(Of PdfCertificate))
    'Set the store location to local machine
    Dim store As X509Store = New X509Store(name, StoreLocation.LocalMachine)
    store.Open(OpenFlags.MaxAllowed)
    For Each x509Cert As X509Certificate2 In store.Certificates
        'PdfCertificate constructor to load the X509Certificate directly
        Dim cert As PdfCertificate = New PdfCertificate(x509Cert)
        certList.Add(cert)
    Next
End Sub
{% endhighlight %}
{% endtabs %}

## Signing an existing document

You can load the signature field from the existing PDF document and add certificate to the document as follows.
{% tabs %}
{% highlight c# %}


//Loads a PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");

//Gets the first page of the document.

PdfLoadedPage page = loadedDocument.Pages[0] as PdfLoadedPage;

//Gets the first signature field of the PDF document.

PdfLoadedSignatureField field = loadedDocument.Form.Fields[0] as PdfLoadedSignatureField;

//Creates a certificate.

PdfCertificate certificate = new PdfCertificate(@"PDF.pfx", "syncfusion");

field.Signature = new PdfSignature(loadedDocument,page,certificate,"Signature",field);

//Saves the document.

loadedDocument.Save("Output.pdf");

//Closes the document.

loadedDocument.Close(true);

{% endhighlight %}
{% highlight vb.net %}
 
'Loads a PDF document.

Dim loadedDocument As New PdfLoadedDocument("Input.pdf")

'Gets the first page of the document.

Dim page As PdfLoadedPage = TryCast(loadedDocument.Pages(0), PdfLoadedPage)

'Gets the first signature field of the PDF document.

Dim field As PdfLoadedSignatureField = TryCast(loadedDocument.Form.Fields(0), PdfLoadedSignatureField)

'Creates a certificate.

Dim certificate As New PdfCertificate("PDF.pfx", "syncfusion")

field.Signature = New PdfSignature(loadedDocument, page, certificate, "Signature", field)

'Saves the document.

loadedDocument.Save("Output.pdf")

'Closes the document.

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

//Gets the first page of the document.

PdfLoadedPage page = loadedDocument.Pages[0] as PdfLoadedPage;

//Gets the first signature field of the PDF document.

PdfLoadedSignatureField field = loadedDocument.Form.Fields[0] as PdfLoadedSignatureField;

//Creates a certificate.

Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.

PdfCertificate certificate = new PdfCertificate(certificateStream, "syncfusion");

field.Signature = new PdfSignature(loadedDocument, page, certificate, "Signature", field);

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

FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Gets the first page of the document.

PdfLoadedPage page = loadedDocument.Pages[0] as PdfLoadedPage;

//Gets the first signature field of the PDF document.

PdfLoadedSignatureField field = loadedDocument.Form.Fields[0] as PdfLoadedSignatureField;

//Creates a certificate.

FileStream certificateStream = new FileStream("PDF.pfx", FileMode.Open, FileAccess.Read);

PdfCertificate certificate = new PdfCertificate(certificateStream, "syncfusion");

field.Signature = new PdfSignature(loadedDocument, page, certificate, "Signature", field);

//Save the document into stream.

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

stream.Position = 0;

//Close the documents.

loadedDocument.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Gets the first page of the document.

PdfLoadedPage page = loadedDocument.Pages[0] as PdfLoadedPage;

//Gets the first signature field of the PDF document.

PdfLoadedSignatureField field = loadedDocument.Form.Fields[0] as PdfLoadedSignatureField;

//Creates a certificate.

Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.PDF.pfx");

PdfCertificate certificate = new PdfCertificate(certificateStream, "syncfusion");

field.Signature = new PdfSignature(loadedDocument, page, certificate, "Signature", field);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Closes the document

loadedDocument.Close(true);

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
## Sign an existing document using stream

You can load the signature field from an existing PDF document and add certificate to the document using stream as follows.
{% tabs %}
{% highlight c# %}
 
//Loads a PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");

//Gets the first page of the document.

PdfLoadedPage page = loadedDocument.Pages[0] as PdfLoadedPage;

//Gets the first signature field of the PDF document.

PdfLoadedSignatureField field = loadedDocument.Form.Fields[0] as PdfLoadedSignatureField;

//Gets the stream from .pfx file.

Stream pfxStream = File.OpenRead("PDF.pfx");

//Creates a certificate instance from PFX file stream with private key.

PdfCertificate certificate = new PdfCertificate(pfxStream, "syncfusion");

field.Signature = new PdfSignature(loadedDocument, page, certificate, "Signature", field);

//Saves the document.

loadedDocument.Save("Output.pdf");

//Closes the document.

loadedDocument.Close(true);

{% endhighlight %}
{% highlight vb.net %}
 
'Loads a PDF document.

Dim loadedDocument As New PdfLoadedDocument("Input.pdf")

'Gets the first page of the document.

Dim page As PdfLoadedPage = TryCast(loadedDocument.Pages(0), PdfLoadedPage)

'Gets the first signature field of the PDF document.
Dim field As PdfLoadedSignatureField = TryCast(loadedDocument.Form.Fields(0), PdfLoadedSignatureField)

'Gets the stream from .pfx file.

Dim pfxStream As Stream = File.OpenRead("PDF.pfx")

'Creates a certificate instance from PFX file stream with private key.

Dim certificate As New PdfCertificate(pfxStream, "syncfusion")

field.Signature = New PdfSignature(loadedDocument, page, certificate, "Signature", field)

'Saves the document.

loadedDocument.Save("Output.pdf")

'Closes the document.

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

//Gets the first page of the document.

PdfLoadedPage page = loadedDocument.Pages[0] as PdfLoadedPage;

//Gets the first signature field of the PDF document.

PdfLoadedSignatureField field = loadedDocument.Form.Fields[0] as PdfLoadedSignatureField;

//Creates a certificate.

Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.PDF.pfx");

PdfCertificate certificate = new PdfCertificate(certificateStream, "syncfusion");

field.Signature = new PdfSignature(loadedDocument, page, certificate, "Signature", field);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await loadedDocument.SaveAsync(stream);

//Close the document

loadedDocument.Close(true);                                                                   

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document

FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Gets the first page of the document.

PdfLoadedPage page = loadedDocument.Pages[0] as PdfLoadedPage;

//Gets the first signature field of the PDF document.

PdfLoadedSignatureField field = loadedDocument.Form.Fields[0] as PdfLoadedSignatureField;

//Creates a certificate.

FileStream certificateStream = new FileStream("PDF.pfx", FileMode.Open, FileAccess.Read);

PdfCertificate certificate = new PdfCertificate(certificateStream, "syncfusion");

field.Signature = new PdfSignature(loadedDocument, page, certificate, "Signature", field);

//Save the document into stream.

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

stream.Position = 0;

//Close the documents.

loadedDocument.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Gets the first page of the document.

PdfLoadedPage page = loadedDocument.Pages[0] as PdfLoadedPage;

//Gets the first signature field of the PDF document.

PdfLoadedSignatureField field = loadedDocument.Form.Fields[0] as PdfLoadedSignatureField;

//Creates a certificate.

Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.PDF.pfx");

PdfCertificate certificate = new PdfCertificate(certificateStream, "syncfusion");

field.Signature = new PdfSignature(loadedDocument, page, certificate, "Signature", field);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

//Closes the document

loadedDocument.Close(true);

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


## Adding a signature validation appearance based on the signature 

You can add the dynamic signature validation appearance to the signature field by enabling the “EnableValidationAppearance” property available in the “PdfSignature” class, the appearance will change based on the PDF reader validation. 

Refer to the following code sample.

{% tabs %}

{% highlight c# %}


//Creates a new PDF document

PdfDocument document = new PdfDocument();
         
//Add a new page

PdfPageBase page = document.Pages.Add();

PdfGraphics graphics=page.Graphics;

//Creates a certificate instance from the PFX file with private key
            
PdfCertificate pdfCert = new PdfCertificate(@"PDF.pfx", "syncfusion");

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
 
//Save and close documents

document.Save("Output.pdf");

document.Close( true );

{% endhighlight %}

{% highlight vb.net %}

'Creates a new PDF document

Dim document As New PdfDocument()

'Adds a new page

Dim page As PdfPageBase = document.Pages.Add()

Dim graphics As PdfGraphics = page.Graphics

'Creates a certificate instance from the PFX file with private key

Dim pdfCert As New PdfCertificate("PDF.pfx", "syncfusion")

'Creates a digital signature

Dim signature As New PdfSignature(document, page, pdfCert, "Signature")

'Sets an image for the signature field

Dim signatureImage As New PdfBitmap("signature.jpg")

‘Sets enable signature validation appearance
        
signature.EnableValidationAppearance = True

'Sets signature info

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

{% highlight UWP %}

//Creates a new PDF document

PdfDocument document = new PdfDocument();

//Adds a new page

PdfPageBase page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from the PFX file with private key

Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.PDF.pfx");

PdfCertificate pdfCert = new PdfCertificate(certificateStream, "syncfusion");

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

{% highlight ASP.NET Core %}


//Creates a new PDF document

PdfDocument document = new PdfDocument();

//Adds a new page

PdfPageBase page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from the PFX file with private key

FileStream certificateStream = new FileStream("PDF.pfx", FileMode.Open, FileAccess.Read);

PdfCertificate pdfCert = new PdfCertificate(certificateStream, "syncfusion");

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

//Close the documents

document.Close(true);

//Defining the ContentType for PDF file

string contentType = "application/pdf";

//Define the file name

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);            //Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples

Save(stream, "Output.pdf");


{% endhighlight %}

{% highlight Xamarin %}


//Creates a new PDF document

PdfDocument document = new PdfDocument();

//Adds a new page

PdfPageBase page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from the PFX file with private key

Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.PDF.pfx");

PdfCertificate pdfCert = new PdfCertificate(certificateStream, "syncfusion");

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

//Closes the document

document.Close(true);

//Save the stream into PDF file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Refer to the PDF/Xamarin section for respective code samples.

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



## Adding a timestamp in digital signature

Essential PDF allows you to add timestamp in the digital signature of the PDF document. The following code example illustrates the same.

{% tabs %}
{% highlight c# %}


//Creates a new PDF document.

PdfDocument document = new PdfDocument();

//Adds a new page.

PdfPage page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from PFX file with private key.

PdfCertificate pdfCert = new PdfCertificate(@"PDF.pfx", "syncfusion");

//Creates a digital signature.

PdfSignature signature = new PdfSignature(page, pdfCert, "Signature");

//Sets an image for signature field.

PdfBitmap image = new PdfBitmap(@"syncfusion_logo.gif");

//Adds time stamp by using the server URI and credentials.

signature.TimeStampServer = new TimeStampServer(new Uri("http://syncfusion.digistamp.com"), "user", "123456");

//Sets signature info.

signature.Bounds = new RectangleF(new PointF(0, 0), image.PhysicalDimension);

signature.ContactInfo = "johndoe@owned.us";

signature.LocationInfo = "Honolulu, Hawaii";

signature.Reason = "I am author of this document.";

//Draws the signature image.

graphics.DrawImage(image, 0, 0);

//Saves and closes the document.

document.Save("Output.pdf");

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}

'Creates a new PDF document.

Dim document As New PdfDocument()

'Adds a new page.

Dim page As PdfPage = document.Pages.Add()

Dim graphics As PdfGraphics = page.Graphics

'Creates a certificate instance from PFX file with private key.

Dim pdfCert As New PdfCertificate("PDF.pfx", "syncfusion")

'Creates a digital signature.

Dim signature As New PdfSignature(page, pdfCert, "Signature")

'Sets an image for signature field.

Dim image As New PdfBitmap("syncfusion_logo.gif")

'Adds time stamp by using the server URI and credentials.

signature.TimeStampServer = New TimeStampServer(New Uri("http://syncfusion.digistamp.com"), "user", "123456")

'Sets signature info.

signature.Bounds = New RectangleF(New PointF(0, 0), image.PhysicalDimension)

signature.ContactInfo = "johndoe@owned.us"

signature.LocationInfo = "Honolulu, Hawaii"

signature.Reason = "I am author of this document."

'Draws the signature image.

graphics.DrawImage(image, 0, 0)

'Saves and closes the document.

document.Save("Output.pdf")

document.Close(True)



{% endhighlight %}

{% highlight UWP %}

//Creates a new PDF document.

PdfDocument document = new PdfDocument();

//Adds a new page.

PdfPageBase page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from PFX file with private key.

Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.PDF.pfx");

PdfCertificate pdfCert = new PdfCertificate(certificateStream, "syncfusion");

//Creates a digital signature.

PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");

//Sets an image for signature field.

Stream imageStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.syncfusion_logo.gif");

PdfBitmap image = new PdfBitmap(imageStream);

//Adds time stamp by using the server URI and credentials.

signature.TimeStampServer = new TimeStampServer(new Uri("http://syncfusion.digistamp.com"), "user", "123456");

//Sets signature info.

signature.Bounds = new RectangleF(new PointF(0, 0), image.PhysicalDimension);

signature.ContactInfo = "johndoe@owned.us";

signature.LocationInfo = "Honolulu, Hawaii";

signature.Reason = "I am author of this document.";

//Draws the signature image.

graphics.DrawImage(image, 0, 0);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Creates a new PDF document.

PdfDocument document = new PdfDocument();

//Adds a new page.

PdfPageBase page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from PFX file with private key.

FileStream certificateStream = new FileStream("PDF.pfx", FileMode.Open, FileAccess.Read);

PdfCertificate pdfCert = new PdfCertificate(certificateStream, "syncfusion");

//Creates a digital signature.

PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");

//Sets an image for signature field.

FileStream imageStream = new FileStream("syncfusion_logo.gif", FileMode.Open, FileAccess.Read);

//Sets an image for signature field.

PdfBitmap image = new PdfBitmap(imageStream);

//Adds time stamp by using the server URI and credentials.

signature.TimeStampServer = new TimeStampServer(new Uri("http://syncfusion.digistamp.com"), "user", "123456");

//Sets signature info.

signature.Bounds = new RectangleF(new PointF(0, 0), image.PhysicalDimension);

signature.ContactInfo = "johndoe@owned.us";

signature.LocationInfo = "Honolulu, Hawaii";

signature.Reason = "I am author of this document.";

//Draws the signature image.

graphics.DrawImage(image, 0, 0);

//Save the document into stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

stream.Position = 0;

//Close the documents.

document.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Creates a new PDF document.

PdfDocument document = new PdfDocument();

//Adds a new page.

PdfPageBase page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from PFX file with private key.

Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.PDF.pfx");

PdfCertificate pdfCert = new PdfCertificate(certificateStream, "syncfusion");

//Creates a digital signature.

PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");

//Sets an image for signature field.

Stream imageStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.syncfusion_logo.gif");

PdfBitmap image = new PdfBitmap(imageStream);

//Adds time stamp by using the server URI and credentials.

signature.TimeStampServer = new TimeStampServer(new Uri("http://syncfusion.digistamp.com"), "user", "123456");

//Sets signature info.

signature.Bounds = new RectangleF(new PointF(0, 0), image.PhysicalDimension);

signature.ContactInfo = "johndoe@owned.us";

signature.LocationInfo = "Honolulu, Hawaii";

signature.Reason = "I am author of this document.";

//Draws the signature image.

graphics.DrawImage(image, 0, 0);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Closes the document

document.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples

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

## Adding a timestamp to PDF document

You can add timestamp to PDF document, using the following code snippet.

{% tabs %}

{% highlight c# %}

//Creates a new PDF document.

PdfDocument document = new PdfDocument();

//Adds a new page.

PdfPage page = document.Pages.Add();

//Creates a digital signature.

PdfSignature signature = new PdfSignature(page, "Signature");

//Add the time stamp by using the server URI.

signature.TimeStampServer = new TimeStampServer(new Uri("http://syncfusion.digistamp.com"), "user", "123456");

//Save and close the document

document.Save("Output.pdf");

document.Close(true);  

{% endhighlight %}

{% highlight vb.net %}

'Creates a new PDF document.

Dim document As New PdfDocument()

'Adds a new page.

Dim page As PdfPage = document.Pages.Add()

'Creates a digital signature.

Dim signature As New PdfSignature(page, "Signature")

'Adds time stamp by using the server URI.

signature.TimeStampServer = New TimeStampServer(New Uri("http://syncfusion.digistamp.com"), "user", "123456")

'Saves and closes the document.

document.Save("Output.pdf")

document.Close(True)

{% endhighlight %}

{% highlight UWP %}

//Create a new document

PdfDocument document = new PdfDocument();

//Adds a new page.

PdfPage page = document.Pages.Add();        

//Creates a digital signature.

PdfSignature signature = new PdfSignature(page, "Signature");

//Add the time stamp by using the server URI.

signature.TimeStampServer = new TimeStampServer(new Uri("http://syncfusion.digistamp.com"), "user", "123456");

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document. 

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples. 

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new pdf document

PdfDocument document = new PdfDocument();

//Adds a new page

PdfPage page = document.Pages.Add();

//Creates a digital signature.

PdfSignature signature = new PdfSignature(page, "Signature");

//Add the time stamp by using the server URI.

signature.TimeStampServer = new TimeStampServer(new Uri("http://syncfusion.digistamp.com"), "user", "123456");

//Save the document into stream.

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

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

{% highlight Xamarin %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();            

//Add a page.

PdfPage page = document.Pages.Add();

//Creates a digital signature.

PdfSignature signature = new PdfSignature(page, "Signature");

//Add the time stamp by using the server URI.

signature.TimeStampServer = new TimeStampServer(new Uri("http://syncfusion.digistamp.com"), "user", "123456");

//Save the document into stream

MemoryStream memoryStream = new MemoryStream();

document.Save(memoryStream);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

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

## Adding a timestamp to existing PDF document

You can add timestamp to existing PDF document, using the following code snippet.

{% tabs %}

{% highlight c# %}

//Load the existing PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");

//Add a new page.

PdfLoadedPage page = loadedDocument.Pages[0] as PdfLoadedPage;

//Creates a digital signature.

PdfSignature signature = new PdfSignature(page, "Signature");

//Add the time stamp by using the server URI.

signature.TimeStampServer = new TimeStampServer(new Uri("http://syncfusion.digistamp.com"), "user", "123456");

//Saves  the document

loadedDocument.Save("Output.pdf");

//Closes the document

loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Load the PDF document. 

Dim document As New PdfLoadedDocument("Input.pdf")

'Gets the first page of the document.

Dim page As PdfLoadedPage = TryCast(document.Pages(0), PdfLoadedPage)

'Creates a digital signature.

Dim signature As New PdfSignature(page, "Signature")

'Adds time stamp by using the server URI.

signature.TimeStampServer = New TimeStampServer(New Uri("http://syncfusion.digistamp.com"), "user", "123456")

'Saves and closes the document.

document.Save("Output.pdf")

document.Close(True)

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

//Gets the first page of the document.

PdfLoadedPage page = loadedDocument.Pages[0] as PdfLoadedPage;

//Creates a digital signature.

PdfSignature signature = new PdfSignature(page, "Signature");

//Add the time stamp by using the server URI.

signature.TimeStampServer = new TimeStampServer(new Uri("http://syncfusion.digistamp.com"), "user", "123456");

MemoryStream stream = new MemoryStream();

await loadedDocument.SaveAsync(stream);

//Close the document. 

loadedDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples. 

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document

FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Gets the page.

PdfLoadedPage page = loadedDocument.Pages[0] as PdfLoadedPage;

//Creates a digital signature.

PdfSignature signature = new PdfSignature(page, "Signature");

//Add the time stamp by using the server URI.

signature.TimeStampServer = new TimeStampServer(new Uri("http://syncfusion.digistamp.com"), "user", "123456");

//Save the document into stream.

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

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

{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf ");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);  

//Gets the page.

PdfLoadedPage page = loadedDocument.Pages[0] as PdfLoadedPage;

//Creates a digital signature.

PdfSignature signature = new PdfSignature(page, "Signature");

//Add the time stamp by using the server URI.

signature.TimeStampServer = new TimeStampServer(new Uri("http://syncfusion.digistamp.com"), "user", "123456")

//Save the PDF document to stream

MemoryStream memoryStream = new MemoryStream();

loadedDocument.Save(memoryStream);

//Closes the document

loadedDocument.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

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

## Retrieve certificate details from an existing signed PDF document

The Essential PDF provides support to get the certificate details from an existing signed PDF document such as,

* Signed date
* Expiry date
* Signed name
* Subject name
* Issuer name
* Certificate distinguished names (country, state, street, email, organization, organization unit, locality, and more).

You can get the above certificate details from an existing signed PDF document by using the following code snippet.

{% tabs %}

{% highlight c# %}

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

string subjectName = certificate.SubjectName;

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

{% highlight vb.net %}

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

loadedDocument.Close(True)


{% endhighlight %}

{% highlight UWP %}

//Essential PDF supports retrieving certificate details from signed PDF document only in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms

{% endhighlight %}

{% highlight ASP.NET Core %}

//Essential PDF supports retrieving certificate details from signed PDF document only in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms

{% endhighlight %}

{% highlight Xamarin %}

//Essential PDF supports retrieving certificate details from signed PDF document only in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms

{% endhighlight %}

{% endtabs %}

## Enable Long Term Validation (LTV) PDF signature

The Essential PDF supports creating long term signature validation when signing the PDF document. The LTV signature allows you to check the validity of a signature long after the document was signed. To achieve long term validation, all the required elements for signature validation must be embedded in the signed PDF.

Note: The resulted PDF document size will be large, since all the necessary signature information, Certificate Revocation List (CRL), and Online Certificate Status Protocol (OCSP) are embedded.

The following code example illustrates how to create LTV PDF.

{% tabs %}

{% highlight c# %}

//Creates a new PDF document.

PdfDocument document = new PdfDocument();

//Adds a new page.

PdfPage page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from PFX file with private key.

PdfCertificate pdfCert = new PdfCertificate(@"PDF.pfx", "syncfusion");

//Creates a digital signature.

PdfSignature signature = new PdfSignature(page, pdfCert, "Signature");

//Sets an image for signature field.

PdfBitmap image = new PdfBitmap(@"syncfusion_logo.gif");

//Adds time stamp by using the server URI and credentials.

signature.TimeStampServer = new TimeStampServer(new Uri("http://syncfusion.digistamp.com"), "user", "123456");

//Enable LTV on Signature

signature.EnableLtv = true;

//Sets signature info.

signature.Bounds = new RectangleF(new PointF(0, 0), image.PhysicalDimension);

signature.ContactInfo = "johndoe@owned.us";

signature.LocationInfo = "Honolulu, Hawaii";

signature.Reason = "I am author of this document.";

//Draws the signature image.

graphics.DrawImage(image, 0, 0);

//Saves and closes the document.

document.Save("Output.pdf");

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Creates a new PDF document.

Dim document As New PdfDocument()

'Adds a new page.

Dim page As PdfPage = document.Pages.Add()

Dim graphics As PdfGraphics = page.Graphics

'Creates a certificate instance from PFX file with private key.

Dim pdfCert As New PdfCertificate("PDF.pfx", "syncfusion")

'Creates a digital signature.

Dim signature As New PdfSignature(page, pdfCert, "Signature")

'Sets an image for signature field.

Dim image As New PdfBitmap("syncfusion_logo.gif")

'Adds time stamp by using the server URI and credentials.

signature.TimeStampServer = New TimeStampServer(New Uri("http://syncfusion.digistamp.com"), "user", "123456")

'Enable LTV on Signature

signature.EnableLtv = True

'Sets signature info.

signature.Bounds = New RectangleF(New PointF(0, 0), image.PhysicalDimension)

signature.ContactInfo = "johndoe@owned.us"

signature.LocationInfo = "Honolulu, Hawaii"

signature.Reason = "I am author of this document."

'Draws the signature image.

graphics.DrawImage(image, 0, 0)

'Saves and closes the document.

document.Save("Output.pdf")

document.Close(True)

{% endhighlight %}

{% highlight UWP %}

//Creates a new PDF document.

PdfDocument document = new PdfDocument();

//Adds a new page.

PdfPageBase page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from PFX file with private key.

Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.PDF.pfx");

PdfCertificate pdfCert = new PdfCertificate(certificateStream, "syncfusion");

//Creates a digital signature.

PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");

//Sets an image for signature field.

Stream imageStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.syncfusion_logo.gif");

PdfBitmap image = new PdfBitmap(imageStream);

//Adds time stamp by using the server URI and credentials.

signature.TimeStampServer = new TimeStampServer(new Uri("http://syncfusion.digistamp.com"), "user", "123456");

//Enable LTV on Signature

signature.EnableLtv = true;

//Sets signature info.

signature.Bounds = new RectangleF(new PointF(0, 0), image.PhysicalDimension);

signature.ContactInfo = "johndoe@owned.us";

signature.LocationInfo = "Honolulu, Hawaii";

signature.Reason = "I am author of this document.";

//Draws the signature image.

graphics.DrawImage(image, 0, 0);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Creates a new PDF document.

PdfDocument document = new PdfDocument();

//Adds a new page.

PdfPageBase page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from PFX file with private key.

FileStream certificateStream = new FileStream("PDF.pfx", FileMode.Open, FileAccess.Read);

PdfCertificate pdfCert = new PdfCertificate(certificateStream, "syncfusion");

//Creates a digital signature.

PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");

//Sets an image for signature field.

FileStream imageStream = new FileStream("syncfusion_logo.gif", FileMode.Open, FileAccess.Read);

//Sets an image for signature field.

PdfBitmap image = new PdfBitmap(imageStream);

//Adds time stamp by using the server URI and credentials.

signature.TimeStampServer = new TimeStampServer(new Uri("http://syncfusion.digistamp.com"), "user", "123456");

//Enable LTV on Signature

signature.EnableLtv = true;

//Sets signature info.

signature.Bounds = new RectangleF(new PointF(0, 0), image.PhysicalDimension);

signature.ContactInfo = "johndoe@owned.us";

signature.LocationInfo = "Honolulu, Hawaii";

signature.Reason = "I am author of this document.";

//Draws the signature image.

graphics.DrawImage(image, 0, 0);

//Save the document into stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

stream.Position = 0;

//Close the documents.

document.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Creates a new PDF document.

PdfDocument document = new PdfDocument();

//Adds a new page.

PdfPageBase page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

//Creates a certificate instance from PFX file with private key.

Stream certificateStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.PDF.pfx");

PdfCertificate pdfCert = new PdfCertificate(certificateStream, "syncfusion");

//Creates a digital signature.

PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");

//Sets an image for signature field.

Stream imageStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.syncfusion_logo.gif");

PdfBitmap image = new PdfBitmap(imageStream);

//Adds time stamp by using the server URI and credentials.

signature.TimeStampServer = new TimeStampServer(new Uri("http://syncfusion.digistamp.com"), "user", "123456");

//Enable LTV on Signature

signature.EnableLtv = true;

//Sets signature info.

signature.Bounds = new RectangleF(new PointF(0, 0), image.PhysicalDimension);

signature.ContactInfo = "johndoe@owned.us";

signature.LocationInfo = "Honolulu, Hawaii";

signature.Reason = "I am author of this document.";

//Draws the signature image.

graphics.DrawImage(image, 0, 0);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Closes the document

document.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("output.pdf", "application/pdf", stream);

{% endhighlight %}

{% endtabs %}

