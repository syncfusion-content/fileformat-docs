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

You can get the certificate details such as subject name, issuer name, and expiry date from an existing signed PDF document using the following code snippet.

{% tabs %}

{% highlight c# %}

//Load the existing signed PDF document

PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");

//Gets the page of the document

PdfLoadedPage page = loadedDocument.Pages[0] as PdfLoadedPage;

//Gets the signature field from the PDF document

PdfLoadedSignatureField field = loadedDocument.Form.Fields[0] as PdfLoadedSignatureField;

//Get PDF Certificate instance from signature field

PdfCertificate certificate = field.Signature.Certificate;

//Get the certificate details

string issuerName = certificate.IssuerName;

string subjectName = certificate.SubjectName;

DateTime validFrom = certificate.ValidFrom;

DateTime validTo = certificate.ValidTo;

//Close the document 

loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Load the existing signed PDF document

Dim loadedDocument As New PdfLoadedDocument("Input.pdf")

'Gets the page of the document

Dim page As PdfLoadedPage = TryCast(loadedDocument.Pages(0), PdfLoadedPage)

'Gets the signature field from the PDF document

Dim field As PdfLoadedSignatureField = TryCast(loadedDocument.Form.Fields(0), PdfLoadedSignatureField)

'Get PDF certificate instance from signature field

Dim certificate As PdfCertificate = field.Signature.Certificate

'Get the certificate details

Dim issuerName As String = certificate.IssuerName

Dim subjectName As String = certificate.SubjectName

Dim validFrom As DateTime = certificate.ValidFrom

Dim validTo As DateTime = certificate.ValidTo

'Close the document 

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

