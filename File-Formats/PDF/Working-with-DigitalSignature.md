---
title: Working with Digital Signature
description: This section explains how to create a Digital Signature in the PDF document by using Essential PDF
platform: file-formats
control: PDF
documentation: UG
---
# Working with Digital Signature

## Adding a digital signature

Essential PDF allows you to add digital signature to the PDF document. In order to add digital signature, you can need a certificate with private keys. Essential PDF provides support for digital signature by using PFX files.

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

PdfBitmap signatureimg = new PdfBitmap(@"signature.jpg");

//Sets signature information

signature.Bounds = new RectangleF(new PointF(0, 0), signatureimg.PhysicalDimension);

signature.ContactInfo = "johndoe@owned.us";

signature.LocationInfo = "Honolulu, Hawaii";

signature.Reason = "I am author of this document.";

//Draws the signature image.

graphics.DrawImage(signatureimg, 0, 0);

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

Dim signatureimg As New PdfBitmap("signature.jpg")

'Sets signature info.

signature.Bounds = New RectangleF(New PointF(0, 0), signatureimg.PhysicalDimension)

signature.ContactInfo = "johndoe@owned.us"

signature.LocationInfo = "Honolulu, Hawaii"

signature.Reason = "I am author of this document."

'Draws the signature image.

graphics.DrawImage(signatureimg, 0, 0)

'Saves and closes the document.

document.Save("Output.pdf")

document.Close(True)



{% endhighlight %}
{% endtabs %}

## Adding a digital signature using stream

The following code example illustrate how to add a digital signature in the PDF document
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

//Creates a certificate instance from a .pfx file stream with private key.

PdfCertificate pdfCert = new PdfCertificate(pfxStream, "syncfusion");

//Creates a digital signature.

PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");

//Sets an image for signature field.

PdfBitmap signatureimg = new PdfBitmap(@"signature.jpg");

//Sets signature information

signature.Bounds = new RectangleF(new PointF(0, 0), signatureimg.PhysicalDimension);

signature.ContactInfo = "johndoe@owned.us";

signature.LocationInfo = "Honolulu, Hawaii";

signature.Reason = "I am author of this document.";

//Draw the signature image.

graphics.DrawImage(signatureimg, 0, 0);

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

Dim signatureimg As New PdfBitmap("signature.jpg")

'Sets signature information.

signature.Bounds = New RectangleF(New PointF(0, 0), signatureimg.PhysicalDimension)

signature.ContactInfo = "johndoe@owned.us"

signature.LocationInfo = "Honolulu, Hawaii"

signature.Reason = "I am author of this document."

'Draws the signature image.

graphics.DrawImage(signatureimg, 0, 0)

'Saves and closes the document.

document.Save("Output.pdf")

document.Close(True)

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

PdfSignatureField signatureField = new PdfSignatureField(page, "Signaturefield");

signatureField.Bounds = new RectangleF(0, 0, 100, 100);

signatureField.Signature = new PdfSignature();

//Adds certificate to the signature field.

signatureField.Signature.Certificate = new PdfCertificate(@"PDF.pfx", "syncfusion");

signatureField.Signature.Reason = "I am author of this document";



//Adds the field

loadedDocument.Form.Fields.Add(signatureField);

//Saves the certified PDF document.

loadedDocument.Save(@"Output.pdf");

loadedDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}

'Loads the PDF document with signature field

Dim loadedDocument As New PdfLoadedDocument("Input.pdf")

'Gets the page

Dim page As PdfLoadedPage = TryCast(loadedDocument.Pages(0), PdfLoadedPage)

'Creates a signature field

Dim signatureField As New PdfSignatureField(page, "Signaturefield")

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
{% endtabs %}
## Sign an existing document using stream

You can load the signature field from an existing PDF document and add certificate to the document as follows.
{% tabs %}
{% highlight c# %}
 
//Loads a PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");

//Get the first page of the document.

PdfLoadedPage page = loadedDocument.Pages[0] as PdfLoadedPage;

//Get the first signature field of the PDF document.

PdfLoadedSignatureField field = loadedDocument.Form.Fields[0] as PdfLoadedSignatureField;

//Get the stream from .pfx file.

Stream pfxStream = File.OpenRead("PDF.pfx");

//Create a certificate instance from PFX file stream with private key.

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

PdfBitmap bmp = new PdfBitmap(@"syncfusion_logo.gif");

//Adds time stamp by using the server URI and credentials.

signature.TimeStampServer = new TimeStampServer(new Uri("http://syncfusion.digistamp.com"), "user", "123456");

//Sets signature info.

signature.Bounds = new RectangleF(new PointF(0, 0), bmp.PhysicalDimension);

signature.ContactInfo = "johndoe@owned.us";

signature.LocationInfo = "Honolulu, Hawaii";

signature.Reason = "I am author of this document.";

//Draws the signature image.

graphics.DrawImage(bmp, 0, 0);

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

Dim bmp As New PdfBitmap("syncfusion_logo.gif")

'Adds time stamp by using the server URI and credentials.

signature.TimeStampServer = New TimeStampServer(New Uri("http://syncfusion.digistamp.com"), "user", "123456")

'Sets signature info.

signature.Bounds = New RectangleF(New PointF(0, 0), bmp.PhysicalDimension)

signature.ContactInfo = "johndoe@owned.us"

signature.LocationInfo = "Honolulu, Hawaii"

signature.Reason = "I am author of this document."

'Draws the signature image.

graphics.DrawImage(bmp, 0, 0)

'Saves and closes the document.

document.Save("Output.pdf")

document.Close(True)



{% endhighlight %}

{% endtabs %}