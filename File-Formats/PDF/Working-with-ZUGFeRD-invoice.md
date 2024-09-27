---
title: Working with ZUGFeRD invoice | Syncfusion
description: This section explains how to generate,add and extract process on ZUGFeRD invoice and Validating ZUGFeRD invoices using Adobe Acrobat
platform: file-formats
control: PDF
documentation: UG
---
# Working with ZUGFeRD invoice 

The ZUGFeRD invoice is one of the uniformed data format for electronic invoices based on the ISO standard PDF/A-3, which is specifically designed for long term archiving. The ZUGFeRD invoice contains both human-readable invoice and machine-readable structured invoice data (XML).

## Generating ZUGFeRD invoice 

The Syncfusion .NET PDF library has support to create PDF document with PDF/A-3b conformance, which allow to add external file to the PDF document as attachment. The ZUGFeRD has two versions, ZugferdVersion 1.0 and ZugferdVersion 2.0. The Zugferd 2.0 is an updated version of Zugferd 1.0.

The ZUGFeRD has five conformance levels,
* Basic: Represents the structured data for simple invoices. Additional information can be included as free text.
* Comfort: Represents the structured data for fully automated invoice processing.
* Extended: Represents the additional structured data for exchanging invoice across different industry segments.
* Minimum: Represents the basic invoice details compatible with the French Standard Factur-X.
* EN16931: Represents the fully compliant with the EU Standard, though it only defines the core elements of an invoice.

N> * The ZUGFeRD conformance levels *Minimum* and *EN16931* are only supported in ZugferdVersion2.0.

The ZUGFeRD invoice document can be created by specifying the conformance level as ``Pdf_A3B`` through [PdfConformanceLevel](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfConformanceLevel.html) Enum when creating the new PDF document and set the [ZugferdConformanceLevel](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfDocument.html#Syncfusion_Pdf_PdfDocument_ZugferdConformanceLevel) property as *Basic* in [ZugferdConformanceLevel](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.ZugferdConformanceLevel.html) Enum. 

{% tabs %} 

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Create ZUGFeRD invoice PDF document
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A3B);

//Set ZUGFeRD conformance level
document.ZugferdConformanceLevel = ZugferdConformanceLevel.Basic;

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Create ZUGFeRD invoice PDF document
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A3B);

//Set ZUGFeRD conformance level
document.ZugferdConformanceLevel = ZugferdConformanceLevel.Basic;

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Create ZUGFeRD invoice PDF document
Dim document As PdfDocument = New PdfDocument(PdfConformanceLevel.Pdf_A3B) 

'Set ZUGFeRD conformance level
document.ZugferdConformanceLevel = ZugferdConformanceLevel.Basic

{% endhighlight %}

{% endtabs %}  

Using PDF/A-3b conformance, you can create a ZUGFeRD invoice PDF by specifying the [ZugferdVersion](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfDocument.html#Syncfusion_Pdf_PdfDocument_ZugferdVersion) property as *ZugferdVersion2_0* of [ZugferdVersion](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.ZugferdVersion.html) Enum. By default, ZugferdVersion1.0 used. 

{% tabs %} 

{% highlight c# tabtitle="C# [Cross-platform]" %}	

//Create ZUGFeRD invoice PDF document
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A3B);

//Specifies ZUGFeRD version            
document.ZugferdVersion = ZugferdVersion.ZugferdVersion2_0;

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Create ZUGFeRD invoice PDF document
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A3B);

//Specifies ZUGFeRD version 
document.ZugferdVersion = ZugferdVersion.ZugferdVersion2_0;

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Create ZUGFeRD invoice PDF document
Dim document As PdfDocument = New PdfDocument(PdfConformanceLevel.Pdf_A3B) 

'Specifies ZUGFeRD version 
document.ZugferdVersion = ZugferdVersion.ZugferdVersion2_0

{% endhighlight %}

{% endtabs %}  

## Adding ZUGFeRD structured data as attachment

The PDF/A-3b conformance supports the external files as attachment to the PDF document using [PdfAttachment](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfAttachment.html) class. 

{% tabs %} 

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Creates an attachment
FileStream fontStream = new FileStream("../../Data/ZUGFeRD-invoice.xml", FileMode.Open, FileAccess.Read);
PdfAttachment attachment = new PdfAttachment("ZUGFeRD-invoice.xml",invoiceStream);
attachment.Relationship = PdfAttachmentRelationship.Alternative;
attachment.ModificationDate = DateTime.Now;
attachment.Description = "ZUGFeRD-invoice";
attachment.MimeType = "application/xml";
//Add attachment to PDF document
document.Attachments.Add(attachment);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Creates an attachment
FileStream invoiceStream = new FileStream("../../Data/ZUGFeRD-invoice.xml", FileMode.Open, FileAccess.Read);
PdfAttachment attachment = new PdfAttachment("ZUGFeRD-invoice.xml",invoiceStream);
attachment.Relationship = PdfAttachmentRelationship.Alternative;
attachment.ModificationDate = DateTime.Now;
attachment.Description = "ZUGFeRD-invoice";
attachment.MimeType = "application/xml";
//Add attachment to PDF document
document.Attachments.Add(attachment);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Creates an attachment
Dim invoiceStream As FileStream = New FileStream("../../Data/ZUGFeRD-invoice.xml", FileMode.Open, FileAccess.Read)
Dim attachment As PdfAttachment = New PdfAttachment("ZUGFeRD-invoice.xml", invoiceStream)
attachment.Relationship = PdfAttachmentRelationship.Alternative
attachment.ModificationDate = DateTime.Now
attachment.Description = "ZUGFeRD-invoice"
attachment.MimeType = "application/xml"
//Add attachment to PDF document 
document.Attachments.Add(attachment)

{% endhighlight %}

{% endtabs %}  

N> *As per the ZUGFeRD standard guidelines, the XML name must be ZUGFeRD-invoice.xml.

## Complete code

The complete code to create ZUGFeRD invoice PDF document as follows.

{% tabs %} 

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Create ZUGFeRD invoice PDF document
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A3B);
//Set ZUGFeRD conformance level 
document.ZugferdConformanceLevel = ZugferdConformanceLevel.Basic;

//Creates an attachment 
FileStream fontStream = new FileStream("../../ Data / ZUGFeRD - invoice.xml", FileMode.Open, FileAccess.Read);
PdfAttachment attachment = new PdfAttachment("ZUGFeRD-invoice.xml",invoiceStream);
attachment.Relationship = PdfAttachmentRelationship.Alternative;
attachment.ModificationDate = DateTime.Now;
attachment.Description = "ZUGFeRD-invoice";
attachment.MimeType = "application/xml";
//Add attachment to PDF document
document.Attachments.Add(attachment);

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
string fileName = "Zugferd.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Create ZUGFeRD invoice PDF document
PdfDocument document = new PdfDocument(PdfConformanceLevel.Pdf_A3B);
//Set ZUGFeRD conformance level 
document.ZugferdConformanceLevel = ZugferdConformanceLevel.Basic;

//Creates an attachment 
FileStream invoiceStream = new FileStream("../../ Data / ZUGFeRD - invoice.xml", FileMode.Open, FileAccess.Read)
PdfAttachment attachment = new PdfAttachment("ZUGFeRD-invoice.xml",invoiceStream);
attachment.Relationship = PdfAttachmentRelationship.Alternative;
attachment.ModificationDate = DateTime.Now;
attachment.Description = "ZUGFeRD-invoice";
attachment.MimeType = "application/xml";
//Add attachment to PDF document
document.Attachments.Add(attachment);

//Save and close the document
document.Save("Zugferd.pdf");
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Create ZUGFeRD invoice PDF document
Dim document As PdfDocument = New PdfDocument(PdfConformanceLevel.Pdf_A3B)
'Set ZUGFeRD conformance level 
document.ZugferdConformanceLevel = ZugferdConformanceLevel.Basic

'Creates an attachment
Dim invoiceStream As FileStream = New FileStream("../../ Data / ZUGFeRD - invoice.xml", FileMode.Open, FileAccess.Read)
Dim attachment As PdfAttachment = New PdfAttachment("ZUGFeRD-invoice.xml",invoiceStream)
attachment.Relationship = PdfAttachmentRelationship.Alternative
attachment.ModificationDate = DateTime.Now
attachment.Description = "ZUGFeRD-invoice"
attachment.MimeType = "application/xml"
//Add attachment to PDF document
document.Attachments.Add(attachment)

'Save and close the document
document.Save("Zugferd.pdf")
document.Close(True)

{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/ZUGFeRD/Create-ZUGFeRD-compliment-PDF-invoice).

## Extract ZUGFeRD invoice from PDF

You can extract the ZUGFeRD invoice using [PdfAttachment](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfAttachment.html) class. 

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}	

//Load the PDF document
FileStream docStream = new FileStream("input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Iterates the attachments
foreach (PdfAttachment attachment in loadedDocument.Attachments)
{
//Extracts the ZUGFeRD invoice attachment and saves it to the disk
FileStream s = new FileStream(attachment.FileName, FileMode.Create);
s.Write(attachment.Data, 0, attachment.Data.Length);
s.Dispose();
}

//Save the document into stream
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);
stream.Position = 0;
//Closes the document
loadedDocument.Close(true);
//Defining the content type for PDF file
string contentType = "application/pdf";
//Define the file name
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Loads the PDF document
PdfLoadedDocument document = new PdfLoadedDocument("Sample.pdf");

//Iterates the attachments
foreach (PdfAttachment attachment in document.Attachments)
{
//Extracts the ZUGFeRD invoice attachment and saves it to the disk
FileStream s = new FileStream(attachment.FileName, FileMode.Create);
s.Write(attachment.Data, 0, attachment.Data.Length);
s.Dispose();
}

//Saves and closes the document
document.Save("Output.pdf");
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Loads the PDF document
Dim document As New PdfLoadedDocument("Sample.pdf")

'Iterates the attachments
For Each attachment As PdfAttachment In document.Attachments
'Extracts the attachment and saves it to the disk
Dim s As New FileStream(attachment.FileName, FileMode.Create)
s.Write(attachment.Data, 0, attachment.Data.Length)
s.Dispose()
Next

'Saves and closes the document
document.Save("Output.pdf")
document.Close(True)

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/ZUGFeRD/Extract-ZUGFeRD-invoice-from-PDF-document).

## Validating ZUGFeRD invoices using Adobe Acrobat

The ZUGFeRD invoices can be validated as follows:

1. Conformance to the PDF/A-3b standard can be checked with Preflight function in Adobe acrobat. 

    * Open the PDF and choose Tools > Print Production > Preflight in the right pane.

    * Select the PDF/A-3b profile and click the Analyze button.

<img src="ZUGFeRD_images/PDF_A_3b_Check.png" alt="PDF/A-3b Preflight Check image" width="100%" Height="Auto"/>

    * Check the result

<img src="ZUGFeRD_images/PDF_A_3b_Results.png" alt="PDF/A-3b Preflight Results image" width="100%" Height="Auto"/>

2. Conformance to the ZUGFeRD invoice can be checked as follows:

    * Open the PDF and choose Tools > Print Production > Preflight in the right pane.

    * Select the ZUGFeRD profile and click the Analyze button.

<img src="ZUGFeRD_images/PDF_ZUGFeRD_Check.png" alt="PDF ZUGFeRD Preflight Check image" width="100%" Height="Auto"/>

    * Check the result

<img src="ZUGFeRD_images/PDF_ZUGFeRD_Results.png" alt="PDF ZUGFeRD Preflight Results image" width="100%" Height="Auto"/>
