---
layout: Post
title: Working with Digital Signature
description: Creating Digital Signature using Essential PDF: Digital signature; Digital Sign
platform: FileFormat
control: PDF
documentation: UG
---
# Working with Digital Signature

## Adding a digital signature

Essential PDF allows you to add digital signature to the PDF document. In order to add digital signature, you will need a certificate with private keys. Essential PDF provides support for digital signature using PFX files.

The following code snippet illustrate how to add a digital signature in the PDF document

{% highlight c# %}
[C#]

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a new page.

PdfPageBase page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

//Create a certificate instance from PFX file with private key.

PdfCertificate pdfCert = new PdfCertificate(@"PDF.pfx", "syncfusion");

//Create a digital signature.

PdfSignature signature = new PdfSignature(document, page, pdfCert, "Signature");

//Set an image for signature field.

PdfBitmap signatureimg = new PdfBitmap(@"signature.jpg");

//Set signature information

signature.Bounds = new RectangleF(new PointF(0, 0), signatureimg.PhysicalDimension);

signature.ContactInfo = "johndoe@owned.us";

signature.LocationInfo = "Honolulu, Hawaii";

signature.Reason = "I am author of this document.";

//Draw the signature image.

graphics.DrawImage(signatureimg, 0, 0);

//Save and close the document.

document.Save("Output.pdf");

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}
[VB]

'Create a new PDF document.

Dim document As New PdfDocument()

'Add a new page.

Dim page As PdfPageBase = document.Pages.Add()

Dim graphics As PdfGraphics = page.Graphics

'Create a certificate instance from PFX file with private key.

Dim pdfCert As New PdfCertificate("PDF.pfx", "syncfusion")

'Create a digital signature.

Dim signature As New PdfSignature(document, page, pdfCert, "Signature")

'Set an image for signature field.

Dim signatureimg As New PdfBitmap("signature.jpg")

'Set signature info.

signature.Bounds = New RectangleF(New PointF(0, 0), signatureimg.PhysicalDimension)

signature.ContactInfo = "johndoe@owned.us"

signature.LocationInfo = "Honolulu, Hawaii"

signature.Reason = "I am author of this document."

'Draw the signature image.

graphics.DrawImage(signatureimg, 0, 0)

'Save and close the document.

document.Save("Output.pdf")

document.Close(True)



{% endhighlight %}

You can add a digital signature to an existing document as shown below.

{% highlight c# %}
[C#]

//Load the PDF document with signature field

PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");         



//Get the page

PdfLoadedPage page = loadedDocument.Pages[0] as PdfLoadedPage;



//Create a signature field

PdfSignatureField signatureField = new PdfSignatureField(page, "Signaturefield");

signatureField.Bounds = new RectangleF(0, 0, 100, 100);

signatureField.Signature = new PdfSignature(page);

//Add certificate to the signature field

signatureField.Signature.Certificate = new PdfCertificate(@"PDF.pfx", "syncfusion");

signatureField.Signature.Reason = "I am author of this document";



//Add the field

loadedDocument.Form.Fields.Add(signatureField);

//Save the certified PDF document

loadedDocument.Save(@"Output.pdf");

loadedDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}
[VB]

'Load the PDF document with signature field

Dim loadedDocument As New PdfLoadedDocument("Input.pdf")

'Get the page

Dim page As PdfLoadedPage = TryCast(loadedDocument.Pages(0), PdfLoadedPage)

'Create a signature field

Dim signatureField As New PdfSignatureField(page, "Signaturefield")

signatureField.Bounds = New RectangleF(0, 0, 100, 100)

signatureField.Signature = New PdfSignature(page)

'Add certificate to the signature field

signatureField.Signature.Certificate = New PdfCertificate("PDF.pfx", "syncfusion")

signatureField.Signature.Reason = "I am author of this document"

'Add the field

loadedDocument.Form.Fields.Add(signatureField)

'Save the certified PDF document

loadedDocument.Save("Output.pdf")

loadedDocument.Close(True)



{% endhighlight %}

## Signing an existing document

You can load the signature field from the existing PDF document and add certificate to the document as shown below.

{% highlight c# %}
[C#]

//Load a PDF document

PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");

//Get the first page of the document

PdfLoadedPage page = loadedDocument.Pages[0] as PdfLoadedPage;

//Get the first signature field of the PDF document

PdfLoadedSignatureField field = loadedDocument.Form.Fields[0] as PdfLoadedSignatureField;

//Create a certificate

PdfCertificate certificate = new PdfCertificate(@"PDF.pfx", "syncfusion");

field.Signature = new PdfSignature(loadedDocument,page,certificate,"Signature",field);

//Save the document

loadedDocument.Save("Output.pdf");

//Close the document

loadedDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}
[VB]

'Load a PDF document

Dim loadedDocument As New PdfLoadedDocument("Input.pdf")

'Get the first page of the document

Dim page As PdfLoadedPage = TryCast(loadedDocument.Pages(0), PdfLoadedPage)

'Get the first signature field of the PDF document

Dim field As PdfLoadedSignatureField = TryCast(loadedDocument.Form.Fields(0), PdfLoadedSignatureField)

'Create a certificate

Dim certificate As New PdfCertificate("PDF.pfx", "syncfusion")

field.Signature = New PdfSignature(loadedDocument, page, certificate, "Signature", field)

'Save the document

loadedDocument.Save("Output.pdf")

'Close the document

loadedDocument.Close(True)



{% endhighlight %}

## Adding a timestamp in digital signature

Essential PDF allows you to add timestamp in the digital signature of the PDF document. The following code snippet illustrates the same.

{% highlight c# %}
[C#]

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a new page.

PdfPage page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

//Create a certificate instance from PFX file with private key.

PdfCertificate pdfCert = new PdfCertificate(@"PDF.pfx", "syncfusion");

//Create a digital signature.

PdfSignature signature = new PdfSignature(page, pdfCert, "Signature");

//Set an image for signature field

PdfBitmap bmp = new PdfBitmap(@"syncfusion_logo.gif");

//Add time stamp using the server URI and credentials.

signature.TimeStampServer = new TimeStampServer(new Uri("http://syncfusion.digistamp.com"), "user", "123456");

//Set signature info.

signature.Bounds = new RectangleF(new PointF(0, 0), bmp.PhysicalDimension);

signature.ContactInfo = "johndoe@owned.us";

signature.LocationInfo = "Honolulu, Hawaii";

signature.Reason = "I am author of this document.";

//Draw the signature image.

graphics.DrawImage(bmp, 0, 0);

//Save and close the document.

document.Save("Output.pdf");

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}
[VB]

'Create a new PDF document.

Dim document As New PdfDocument()

'Add a new page.

Dim page As PdfPage = document.Pages.Add()

Dim graphics As PdfGraphics = page.Graphics

'Create a certificate instance from PFX file with private key.

Dim pdfCert As New PdfCertificate("PDF.pfx", "syncfusion")

'Create a digital signature.

Dim signature As New PdfSignature(page, pdfCert, "Signature")

'Set an image for signature field

Dim bmp As New PdfBitmap("syncfusion_logo.gif")

'Add time stamp using the server URI and credentials.

signature.TimeStampServer = New TimeStampServer(New Uri("http://syncfusion.digistamp.com"), "user", "123456")

'Set signature info.

signature.Bounds = New RectangleF(New PointF(0, 0), bmp.PhysicalDimension)

signature.ContactInfo = "johndoe@owned.us"

signature.LocationInfo = "Honolulu, Hawaii"

signature.Reason = "I am author of this document."

'Draw the signature image.

graphics.DrawImage(bmp, 0, 0)

'Save and close the document.

document.Save("Output.pdf")

document.Close(True)



{% endhighlight %}

