---
title: Working with Metadata | Syncfusion
description: This section explains how to add metadata in the PDF document and the metadata is a data that describes the characteristics of properties of a document
platform: file-formats
control: PDF
documentation: UG
---

# Working with Metadata (XMP)

Metadata is a data that describes the characteristics or properties of a document.

Metadata includes document information properties such as author, modification date, and copyright status.

## Working with the XMP metadata

In order to work multiple applications effectively with metadata, there must be a common standard that they understand. XMP-the Extensible Metadata Platform is designed to provide such a standard.

XMP standardizes the definition, creation, and processing of metadata.

## Adding XMP metadata in a PDF document

You can add XMP metadata in a PDF document using [XmpMetadata](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xmp.XmpMetadata.html) class as shown in the code snippet below.

{% tabs %}  

{% highlight c# tabtile="C#" %}

//Create a PDF document

PdfDocument pdfDoc = new PdfDocument();

//Create a page

PdfPage page = pdfDoc.Pages.Add();

//Get XMP object

XmpMetadata metaData = pdfDoc.DocumentInformation.XmpMetadata;

//XMP Basic Schema

BasicSchema basic = metaData.BasicSchema;

//set the basic details of the document

basic.Advisory.Add("advisory");

basic.BaseURL = new Uri("http://google.com");

basic.CreateDate = DateTime.Now;

basic.CreatorTool = "creator tool";

basic.Identifier.Add("identifier");

basic.Label = "label";

basic.MetadataDate = DateTime.Now;

basic.ModifyDate = DateTime.Now;

basic.Nickname = "nickname";

basic.Rating.Add(-25);

//save the document

pdfDoc.Save("DocumentInformation.pdf");

pdfDoc.Close(true);

{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}

'Create a PDF document

Dim pdfDoc As New PdfDocument()

'Create a page

Dim page As PdfPage = pdfDoc.Pages.Add()

'Get XMP object

Dim metaData As XmpMetadata = pdfDoc.DocumentInformation.XmpMetadata

'XMP Basic Schema

Dim basic As BasicSchema = metaData.BasicSchema

'set the basic details of the document

basic.Advisory.Add("advisory")

basic.BaseURL = New Uri("http://google.com")

basic.CreateDate = DateTime.Now

basic.CreatorTool = "creator tool"

basic.Identifier.Add("identifier")

basic.Label = "label"

basic.MetadataDate = DateTime.Now

basic.ModifyDate = DateTime.Now

basic.Nickname = "nickname"

basic.Rating.Add(-25)

'save the document

pdfDoc.Save("DocumentInformation.pdf")

pdfDoc.Close(True)

{% endhighlight %}

  {% highlight c# tabtile="UWP" %}

//Essential PDF supports Metadata (XMP) only in Windows Forms, WPF, ASP.NET, ASP.NET MVC, ASP.NET Core and Xamarin platforms

{% endhighlight %}

{% highlight c# tabtile="ASP.NET Core" %}

//Create a PDF document

PdfDocument pdfDoc = new PdfDocument();

//Create a page

PdfPage page = pdfDoc.Pages.Add();

//Get XMP object

XmpMetadata metaData = pdfDoc.DocumentInformation.XmpMetadata;

//XMP Basic Schema

BasicSchema basic = metaData.BasicSchema;

//Set the basic details of the document

basic.Advisory.Add("advisory");

basic.BaseURL = new Uri("http://google.com");

basic.CreateDate = DateTime.Now;

basic.CreatorTool = "creator tool";

basic.Identifier.Add("identifier");

basic.Label = "label";

basic.MetadataDate = DateTime.Now;

basic.ModifyDate = DateTime.Now;

basic.Nickname = "nickname";

basic.Rating.Add(-25);

//Save and close the document

MemoryStream stream = new MemoryStream();

pdfDoc.Save(stream);

stream.Position = 0;

//Close the document

pdfDoc.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "DocumentInformation.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}

//Create a PDF document

PdfDocument pdfDoc = new PdfDocument();

//Create a page

PdfPage page = pdfDoc.Pages.Add();

//Get XMP object

XmpMetadata metaData = pdfDoc.DocumentInformation.XmpMetadata;

//XMP Basic Schema

BasicSchema basic = metaData.BasicSchema;

//Set the basic details of the document

basic.Advisory.Add("advisory");

basic.BaseURL = new Uri("http://google.com");

basic.CreateDate = DateTime.Now;

basic.CreatorTool = "creator tool";

basic.Identifier.Add("identifier");

basic.Label = "label";

basic.MetadataDate = DateTime.Now;

basic.ModifyDate = DateTime.Now;

basic.Nickname = "nickname";

basic.Rating.Add(-25);

//Save the document into stream

MemoryStream memoryStream = new MemoryStream();

pdfDoc.Save(memoryStream);

//Close the documents

pdfDoc.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)

{

    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("DocumentInformation.pdf", "application/pdf", memoryStream);

}

else

{

    Xamarin.Forms.DependencyService.Get<ISave>().Save("DocumentInformation.pdf", "application/pdf", memoryStream);

}

{% endhighlight %}

{% endtabs %}  

## Adding XMP metadata in an existing PDF document

You can add metadata in an existing PDF document using [XmpMetadata](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xmp.XmpMetadata.html) class, as follows.

{% tabs %}  

{% highlight c# tabtile="C#" %}

//Load the document

PdfLoadedDocument pdfDoc = new PdfLoadedDocument("input.pdf");

// Get XMP object

XmpMetadata metaData = pdfDoc.DocumentInformation.XmpMetadata;

// XMP Basic Schema

BasicSchema basic = metaData.BasicSchema;

//set the basic details of the document

basic.Advisory.Add("advisory");

basic.BaseURL = new Uri("http://google.com");

basic.CreateDate = DateTime.Now;

basic.CreatorTool = "creator tool";

basic.Identifier.Add("identifier");

basic.Label = "label";

basic.MetadataDate = DateTime.Now;

basic.ModifyDate = DateTime.Now;

basic.Nickname = "nickname";

basic.Rating.Add(-25);

//save the document

pdfDoc.Save("DocumentInformation.pdf");

pdfDoc.Close(true);

{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}

'Load the document

Dim pdfDoc As New PdfLoadedDocument("input.pdf")

'Get metaData object

Dim metaData As XmpMetadata = pdfDoc.DocumentInformation.XmpMetadata

'XMP Basic Schema

Dim basic As BasicSchema = metaData.BasicSchema

'Set the basic details of the document

basic.Advisory.Add("advisory")

basic.BaseURL = New Uri("http://google.com")

basic.CreateDate = DateTime.Now

basic.CreatorTool = "creator tool"

basic.Identifier.Add("identifier")

basic.Label = "label"

basic.MetadataDate = DateTime.Now

basic.ModifyDate = DateTime.Now

basic.Nickname = "nickname"

basic.Rating.Add(-25)

'Save the document

pdfDoc.Save("DocumentInformation.pdf")

pdfDoc.Close(True)

{% endhighlight %}

  {% highlight c# tabtile="UWP" %}

//Essential PDF supports Metadata (XMP) only in Windows Forms, WPF, ASP.NET, ASP.NET MVC, ASP.NET Core and Xamarin platforms

{% endhighlight %}

{% highlight c# tabtile="ASP.NET Core" %}

//Load the PDF document

FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);

PdfLoadedDocument pdfDoc = new PdfLoadedDocument(docStream);

//Get XMP object

XmpMetadata metaData = pdfDoc.DocumentInformation.XmpMetadata;

//XMP Basic Schema

BasicSchema basic = metaData.BasicSchema;

//Set the basic details of the document

basic.Advisory.Add("advisory");

basic.BaseURL = new Uri("http://google.com");

basic.CreateDate = DateTime.Now;

basic.CreatorTool = "creator tool";

basic.Identifier.Add("identifier");

basic.Label = "label";

basic.MetadataDate = DateTime.Now;

basic.ModifyDate = DateTime.Now;

basic.Nickname = "nickname";

basic.Rating.Add(-25);

//Save and close the document

MemoryStream stream = new MemoryStream();

pdfDoc.Save(stream);

stream.Position = 0;

//Close the document.

pdfDoc.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "DocumentInformation.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");

PdfLoadedDocument pdfDoc = new PdfLoadedDocument(docStream);

//Get XMP object

XmpMetadata metaData = pdfDoc.DocumentInformation.XmpMetadata;

//XMP Basic Schema

BasicSchema basic = metaData.BasicSchema;

//Set the basic details of the document

basic.Advisory.Add("advisory");

basic.BaseURL = new Uri("http://google.com");

basic.CreateDate = DateTime.Now;

basic.CreatorTool = "creator tool";

basic.Identifier.Add("identifier");

basic.Label = "label";

basic.MetadataDate = DateTime.Now;

basic.ModifyDate = DateTime.Now;

basic.Nickname = "nickname";

basic.Rating.Add(-25);

//Save the document into stream

MemoryStream memoryStream = new MemoryStream();

pdfDoc.Save(memoryStream);

//Close the documents

pdfDoc.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)

{

    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("DocumentInformation.pdf", "application/pdf", memoryStream);

}

else

{

    Xamarin.Forms.DependencyService.Get<ISave>().Save("DocumentInformation.pdf", "application/pdf", memoryStream);

}

{% endhighlight %}

{% endtabs %}  

## Supported Schema types

XMP is provided with the following schemas:

* Basic Schema 
* Dublin Core Schema 
* Rights Management Schema 
* Basic Job Ticket Schema 
* Paged-Text Schema 
* PDF Schema 

## Basic Schema

Basic Schema contains properties that provide basic descriptive information such as, 

* Base URL
* Creation date
* Creator tool
* Label
* Modified date.
* Meta data date
* Nickname
* Rating

[BasicSchema](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xmp.BasicSchema.html) class is used to create the basic schema properties.

Refer the following code sample to create XMP basic schema.

{% tabs %}  

{% highlight c# tabtile="C#" %}

//Create a PDF document

PdfDocument pdfDoc = new PdfDocument();

//Create a page

PdfPage page = pdfDoc.Pages.Add();

//Get metaData object

XmpMetadata metaData = pdfDoc.DocumentInformation.XmpMetadata;

//XMP Basic Schema

BasicSchema basic = metaData.BasicSchema;

//Set the basic details of the document

basic.Advisory.Add("advisory");

basic.BaseURL = new Uri("http://google.com");

basic.CreateDate = DateTime.Now;

basic.CreatorTool = "creator tool";

basic.Identifier.Add("identifier");

basic.Label = "label";

basic.MetadataDate = DateTime.Now;

basic.ModifyDate = DateTime.Now;

basic.Nickname = "nickname";

basic.Rating.Add(-25);

//Save the document

pdfDoc.Save("DocumentInformation.pdf");

pdfDoc.Close(true);

{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}

'Create a PDF document

Dim pdfDoc As New PdfDocument()

'Create a page

Dim page As PdfPage = pdfDoc.Pages.Add()

'Get metaData object

Dim metaData As XmpMetadata = pdfDoc.DocumentInformation.XmpMetadata

'XMP Basic Schema

Dim basic As BasicSchema = metaData.BasicSchema

'Set the basic details of the document

basic.Advisory.Add("advisory")

basic.BaseURL = New Uri("http://google.com")

basic.CreateDate = DateTime.Now

basic.CreatorTool = "creator tool"

basic.Identifier.Add("identifier")

basic.Label = "label"

basic.MetadataDate = DateTime.Now

basic.ModifyDate = DateTime.Now

basic.Nickname = "nickname"

basic.Rating.Add(-25)

'Save the document

pdfDoc.Save("DocumentInformation.pdf")

pdfDoc.Close(True)

{% endhighlight %}

  {% highlight c# tabtile="UWP" %}

//Essential PDF supports Metadata (XMP) only in Windows Forms, WPF, ASP.NET, ASP.NET MVC, ASP.NET Core and Xamarin platforms

{% endhighlight %}

{% highlight c# tabtile="ASP.NET Core" %}

//Create a PDF document

PdfDocument pdfDoc = new PdfDocument();

//Create a page

PdfPage page = pdfDoc.Pages.Add();

//Get metaData object

XmpMetadata metaData = pdfDoc.DocumentInformation.XmpMetadata;

//XMP Basic Schema

BasicSchema basic = metaData.BasicSchema;

//Set the basic details of the document

basic.Advisory.Add("advisory");

basic.BaseURL = new Uri("http://google.com");

basic.CreateDate = DateTime.Now;

basic.CreatorTool = "creator tool";

basic.Identifier.Add("identifier");

basic.Label = "label";

basic.MetadataDate = DateTime.Now;

basic.ModifyDate = DateTime.Now;

basic.Nickname = "nickname";

basic.Rating.Add(-25);

//Save and close the document

MemoryStream stream = new MemoryStream();

pdfDoc.Save(stream);

stream.Position = 0;

//Close the document

pdfDoc.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "DocumentInformation.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}

//Create a PDF document

PdfDocument pdfDoc = new PdfDocument();

//Create a page

PdfPage page = pdfDoc.Pages.Add();

//Get metaData object

XmpMetadata metaData = pdfDoc.DocumentInformation.XmpMetadata;

//XMP Basic Schema

BasicSchema basic = metaData.BasicSchema;

//Set the basic details of the document

basic.Advisory.Add("advisory");

basic.BaseURL = new Uri("http://google.com");

basic.CreateDate = DateTime.Now;

basic.CreatorTool = "creator tool";

basic.Identifier.Add("identifier");

basic.Label = "label";

basic.MetadataDate = DateTime.Now;

basic.ModifyDate = DateTime.Now;

basic.Nickname = "nickname";

basic.Rating.Add(-25);

//Save the document into stream

MemoryStream memoryStream = new MemoryStream();

pdfDoc.Save(memoryStream);

//Close the documents

pdfDoc.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)

{

    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("DocumentInformation.pdf", "application/pdf", memoryStream);

}

else

{

    Xamarin.Forms.DependencyService.Get<ISave>().Save("DocumentInformation.pdf", "application/pdf", memoryStream);

}

{% endhighlight %}

{% endtabs %}  

### Dublin Core Schema

The Dublin Core schema provides a set of commonly used properties such as,

* Contributor
* Coverage
* Creator
* Date
* Description
* Format
* Language
* Publisher
* Title

[DublinCoreSchema](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xmp.DublinCoreSchema.html) class is used to create the Dublin core schema properties.

{% tabs %}  

{% highlight c# tabtile="C#" %}

//Create new PDF document

PdfDocument pdfDoc = new PdfDocument();

PdfPage page = pdfDoc.Pages.Add();

//Gets XMP object

XmpMetadata metaData = pdfDoc.DocumentInformation.XmpMetadata;

//XMP Dublin core Schema

DublinCoreSchema dublin = metaData.DublinCoreSchema;

//Set the Dublin Core Schema details of the document

dublin.Creator.Add("Syncfusion");

dublin.Description.Add("Title", "Essential PDF creator");

dublin.Title.Add("Resource name", "Documentation");

dublin.Type.Add("PDF");

dublin.Publisher.Add("Essential PDF");

//Saves the document

pdfDoc.Save("DocumentInformation.pdf");

pdfDoc.Close(true);

{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}

'Create new PDF document

Dim pdfDoc As New PdfDocument()

Dim page As PdfPage = pdfDoc.Pages.Add()

'Gets XMP object

Dim metaData As XmpMetadata = pdfDoc.DocumentInformation.XmpMetadata

'XMP Dublin core Schema

Dim dublin As DublinCoreSchema = metaData.DublinCoreSchema

'Set the Dublin Core Schema details of the document

dublin.Creator.Add("Syncfusion")

dublin.Description.Add("Title", "Essential PDF creator")

dublin.Title.Add("Resource name", "Documentation")

dublin.Type.Add("PDF")

dublin.Publisher.Add("Essential PDF")

'Saves the document

pdfDoc.Save("DocumentInformation.pdf")

pdfDoc.Close(True)

{% endhighlight %}

  {% highlight c# tabtile="UWP" %}

//Essential PDF supports Metadata (XMP) only in Windows Forms, WPF, ASP.NET, ASP.NET MVC, ASP.NET Core and Xamarin platforms

{% endhighlight %}

{% highlight c# tabtile="ASP.NET Core" %}

//Create new PDF document

PdfDocument pdfDoc = new PdfDocument();

PdfPage page = pdfDoc.Pages.Add();

//Gets XMP object

XmpMetadata metaData = pdfDoc.DocumentInformation.XmpMetadata;

//XMP Dublin core Schema

DublinCoreSchema dublin = metaData.DublinCoreSchema;

//Set the Dublin Core Schema details of the document

dublin.Creator.Add("Syncfusion");

dublin.Description.Add("Title", "Essential PDF creator");

dublin.Title.Add("Resource name", "Documentation");

dublin.Type.Add("PDF");

dublin.Publisher.Add("Essential PDF");

//Save and close the document

MemoryStream stream = new MemoryStream();

pdfDoc.Save(stream);

stream.Position = 0;

//Close the document

pdfDoc.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "DocumentInformation.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}

//Create new PDF document

PdfDocument pdfDoc = new PdfDocument();

PdfPage page = pdfDoc.Pages.Add();

//Gets XMP object

XmpMetadata metaData = pdfDoc.DocumentInformation.XmpMetadata;

//XMP Dublin core Schema

DublinCoreSchema dublin = metaData.DublinCoreSchema;

//Set the Dublin Core Schema details of the document

dublin.Creator.Add("Syncfusion");

dublin.Description.Add("Title", "Essential PDF creator");

dublin.Title.Add("Resource name", "Documentation");

dublin.Type.Add("PDF");

dublin.Publisher.Add("Essential PDF");

//Save the document into stream

MemoryStream memoryStream = new MemoryStream();

pdfDoc.Save(memoryStream);

//Close the documents

pdfDoc.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)

{

    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("DocumentInformation.pdf", "application/pdf", memoryStream);

}

else

{

    Xamarin.Forms.DependencyService.Get<ISave>().Save("DocumentInformation.pdf", "application/pdf", memoryStream);

}

{% endhighlight %}

{% endtabs %}  

### Rights Management Schema

This schema includes properties related to rights management. These properties provide information regarding the legal restrictions associated with a resource.

* Certificate
* Marked
* Owner
* UsageTerm
* WebStatement

[RightsManagementSchema](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xmp.RightsManagementSchema.html) class is used to create the Rights management schema properties.

{% tabs %} 

{% highlight c# tabtile="C#" %}

//Create PDF document

PdfDocument pdfDoc = new PdfDocument();

PdfPage page = pdfDoc.Pages.Add();

//Gets XMP object

XmpMetadata metaData = pdfDoc.DocumentInformation.XmpMetadata;

//XMP Rights Management Schema

RightsManagementSchema rights = metaData.RightsManagementSchema;

//Set the Rights Management Schema details of the document

rights.Certificate = new Uri("http://syncfusion.com");

rights.Owner.Add("Syncfusion");

rights.Marked = true;

//Save and close the document

pdfDoc.Save("DocumentInformation.pdf");

pdfDoc.Close(true);

{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}

'Create PDF document

Dim pdfDoc As New PdfDocument()

Dim page As PdfPage = pdfDoc.Pages.Add()

'Gets XMP object

Dim metaData As XmpMetadata = pdfDoc.DocumentInformation.XmpMetadata

'XMP Rights Management Schema

Dim rights As RightsManagementSchema = metaData.RightsManagementSchema

'Set the Rights Management Schema details of the document

rights.Certificate = New Uri("http://syncfusion.com")

rights.Owner.Add("Syncfusion")

rights.Marked = True

'Save and close the document

pdfDoc.Save("DocumentInformation.pdf")

pdfDoc.Close(True)

{% endhighlight %}

  {% highlight c# tabtile="UWP" %}

//Essential PDF does not support Metadata (XMP) in UWP platform

{% endhighlight %}

{% highlight c# tabtile="ASP.NET Core" %}

//Create PDF document

PdfDocument pdfDoc = new PdfDocument();

PdfPage page = pdfDoc.Pages.Add();

//Gets XMP object

XmpMetadata metaData = pdfDoc.DocumentInformation.XmpMetadata;

//XMP Rights Management Schema

RightsManagementSchema rights = metaData.RightsManagementSchema;

//Set the Rights Management Schema details of the document

rights.Certificate = new Uri("http://syncfusion.com");

rights.Owner.Add("Syncfusion");

rights.Marked = true;

//Save and close the document

MemoryStream stream = new MemoryStream();

pdfDoc.Save(stream);

stream.Position = 0;

//Close the document

pdfDoc.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "DocumentInformation.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}

//Create PDF document

PdfDocument pdfDoc = new PdfDocument();

PdfPage page = pdfDoc.Pages.Add();

//Gets XMP object

XmpMetadata metaData = pdfDoc.DocumentInformation.XmpMetadata;

//XMP Rights Management Schema

RightsManagementSchema rights = metaData.RightsManagementSchema;

//Set the Rights Management Schema details of the document

rights.Certificate = new Uri("http://syncfusion.com");

rights.Owner.Add("Syncfusion");

rights.Marked = true;

//Save the document into stream

MemoryStream memoryStream = new MemoryStream();

pdfDoc.Save(memoryStream);

//Close the documents

pdfDoc.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)

{

    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("DocumentInformation.pdf", "application/pdf", memoryStream);

}

else

{

    Xamarin.Forms.DependencyService.Get<ISave>().Save("DocumentInformation.pdf", "application/pdf", memoryStream);

}

{% endhighlight %}

{% endtabs %}  

### Basic Job Ticket Schema

This schema describes very simple workflow or job information and [BasicJobTicketSchema](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xmp.BasicJobTicketSchema.html) class is used for creation.

* JobRef

{% tabs %} 

{% highlight c# tabtile="C#" %}

//Create a document

PdfDocument pdfDoc = new PdfDocument();

//Add a page

PdfPage page = pdfDoc.Pages.Add();

//Gets XMP object

XmpMetadata metaData = pdfDoc.DocumentInformation.XmpMetadata;

//XMP Rights Management Schema

BasicJobTicketSchema basicJob = metaData.BasicJobTicketSchema;

//Set the Rights Management Schema details of the document

basicJob.JobRef.Add("PDF document creation");

//Save the document

pdfDoc.Save("DocumentInformation.pdf");

pdfDoc.Close(true);

{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}

'Create a document

Dim pdfDoc As New PdfDocument()

'Add a page

Dim page As PdfPage = pdfDoc.Pages.Add()

'Gets XMP object

Dim metaData As XmpMetadata = pdfDoc.DocumentInformation.XmpMetadata

'XMP Rights Management Schema

Dim basicJob As BasicJobTicketSchema = metaData.BasicJobTicketSchema

'Set the Rights Management Schema details of the document

basicJob.JobRef.Add("PDF document creation")

'Save the document

pdfDoc.Save("DocumentInformation.pdf")

pdfDoc.Close(True)

{% endhighlight %}

  {% highlight c# tabtile="UWP" %}

//Essential PDF supports Metadata (XMP) only in Windows Forms, WPF, ASP.NET, ASP.NET MVC, ASP.NET Core and Xamarin platforms

{% endhighlight %}

{% highlight c# tabtile="ASP.NET Core" %}

//Create a document

PdfDocument pdfDoc = new PdfDocument();

//Add a page

PdfPage page = pdfDoc.Pages.Add();

//Gets XMP object

XmpMetadata metaData = pdfDoc.DocumentInformation.XmpMetadata;

//XMP Rights Management Schema

BasicJobTicketSchema basicJob = metaData.BasicJobTicketSchema;

//Set the Rights Management Schema details of the document

basicJob.JobRef.Add("PDF document creation");

//Save and close the document

MemoryStream stream = new MemoryStream();

pdfDoc.Save(stream);

stream.Position = 0;

//Close the document.

pdfDoc.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "DocumentInformation.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}

//Create a document

PdfDocument pdfDoc = new PdfDocument();

//Add a page

PdfPage page = pdfDoc.Pages.Add();

//Gets XMP object

XmpMetadata metaData = pdfDoc.DocumentInformation.XmpMetadata;

//XMP Rights Management Schema

BasicJobTicketSchema basicJob = metaData.BasicJobTicketSchema;

//Set the Rights Management Schema details of the document

basicJob.JobRef.Add("PDF document creation");

//Save the document into stream

MemoryStream memoryStream = new MemoryStream();

pdfDoc.Save(memoryStream);

//Close the documents

pdfDoc.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)

{

    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("DocumentInformation.pdf", "application/pdf", memoryStream);

}

else

{

    Xamarin.Forms.DependencyService.Get<ISave>().Save("DocumentInformation.pdf", "application/pdf", memoryStream);

}

{% endhighlight %}

{% endtabs %}  

### Paged-Text Schema

The Paged-Text schema is used for text appearance on page in a document.

* MaxPageSize
* NPages
* Colorants
* PlateNames

[PagedTextSchema](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xmp.PagedTextSchema.html) class is used for creating Paged-Text schema properties.

{% tabs %} 

{% highlight c# tabtile="C#" %}

//Create a Pdf document

PdfDocument pdfDoc = new PdfDocument();

//Create a Page

PdfPage page = pdfDoc.Pages.Add();

//Gets XMP object

XmpMetadata metaData = pdfDoc.DocumentInformation.XmpMetadata;

//XMP Page text Schema

PagedTextSchema pagedText = metaData.PagedTextSchema;

//Sets the Page text Schema details of the document

pagedText.MaxPageSize.Width = 500;

pagedText.MaxPageSize.Height = 750;

pagedText.NPages = 1;

pagedText.PlateNames.Add("Sample page");

//Saves the document

pdfDoc.Save("DocumentInformation.pdf");

pdfDoc.Close(true);

{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}

'Create a Pdf document

Dim pdfDoc As New PdfDocument()

'Create a Page

Dim page As PdfPage = pdfDoc.Pages.Add()

'Gets XMP object

Dim metaData As XmpMetadata = pdfDoc.DocumentInformation.XmpMetadata

'XMP Page text Schema

Dim pagedText As PagedTextSchema = metaData.PagedTextSchema

'Sets the Page text Schema details of the document

pagedText.MaxPageSize.Width = 500

pagedText.MaxPageSize.Height = 750

pagedText.NPages = 1

pagedText.PlateNames.Add("Sample page")

'Saves the document

pdfDoc.Save("DocumentInformation.pdf")

pdfDoc.Close(True)

{% endhighlight %}

  {% highlight c# tabtile="UWP" %}

//Essential PDF supports Metadata (XMP) only in Windows Forms, WPF, ASP.NET, ASP.NET MVC, ASP.NET Core and Xamarin platforms

{% endhighlight %}

{% highlight c# tabtile="ASP.NET Core" %}

//Create a Pdf document

PdfDocument pdfDoc = new PdfDocument();

//Create a Page

PdfPage page = pdfDoc.Pages.Add();

//Gets XMP object

XmpMetadata metaData = pdfDoc.DocumentInformation.XmpMetadata;

//XMP Page text Schema

PagedTextSchema pagedText = metaData.PagedTextSchema;

//Sets the Page text Schema details of the document

pagedText.MaxPageSize.Width = 500;

pagedText.MaxPageSize.Height = 750;

pagedText.NPages = 1;

pagedText.PlateNames.Add("Sample page");

//Save and close the document

MemoryStream stream = new MemoryStream();

pdfDoc.Save(stream);

stream.Position = 0;

//Close the document

pdfDoc.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "DocumentInformation.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}

//Create a Pdf document

PdfDocument pdfDoc = new PdfDocument();

//Create a Page

PdfPage page = pdfDoc.Pages.Add();

//Gets XMP object

XmpMetadata metaData = pdfDoc.DocumentInformation.XmpMetadata;

//XMP Page text Schema

PagedTextSchema pagedText = metaData.PagedTextSchema;

//Sets the Page text Schema details of the document

pagedText.MaxPageSize.Width = 500;

pagedText.MaxPageSize.Height = 750;

pagedText.NPages = 1;

pagedText.PlateNames.Add("Sample page");

//Save the document into stream

MemoryStream memoryStream = new MemoryStream();

pdfDoc.Save(memoryStream);

//Close the documents

pdfDoc.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)

{

    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("DocumentInformation.pdf", "application/pdf", memoryStream);

}

else

{

    Xamarin.Forms.DependencyService.Get<ISave>().Save("DocumentInformation.pdf", "application/pdf", memoryStream);

}

{% endhighlight %}

{% endtabs %}  

### PDF schema

This schema specifies properties used with Adobe PDF documents.

[PDFSchema](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xmp.PDFSchema.html) class is used to create the PDF Schema. It has the following set of properties.

{% tabs %} 

{% highlight c# tabtile="C#" %}

//Create a PDF document

PdfDocument pdfDoc = new PdfDocument();

//Add a page

PdfPage page = pdfDoc.Pages.Add();

//Gets XMP object

XmpMetadata metaData = pdfDoc.DocumentInformation.XmpMetadata;

//XMP PDF Schema

PDFSchema pdfSchema = metaData.PDFSchema;

//Set the PDF Schema details of the document

pdfSchema.Producer = "Syncfusion";

pdfSchema.PDFVersion = "1.5";

pdfSchema.Keywords = "Essential PDF";

//Save and Close the document

pdfDoc.Save("DocumentInformation.pdf");

pdfDoc.Close(true);

{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}

'Create a PDF document

Dim pdfDoc As New PdfDocument()

'Add a page

Dim page As PdfPage = pdfDoc.Pages.Add()

'Gets XMP object

Dim metaData As XmpMetadata = pdfDoc.DocumentInformation.XmpMetadata

'XMP PDF Schema

Dim pdfSchema As PDFSchema = metaData.PDFSchema

'Set the PDF Schema details of the document

pdfSchema.Producer = "Syncfusion"

pdfSchema.PDFVersion = "1.5"

pdfSchema.Keywords = "Essential PDF"

'Save and Close the document

pdfDoc.Save("DocumentInformation.pdf")

pdfDoc.Close(True)

{% endhighlight %}

  {% highlight c# tabtile="UWP" %}

//Essential PDF supports Metadata (XMP) only in Windows Forms, WPF, ASP.NET, ASP.NET MVC, ASP.NET Core and Xamarin platforms

{% endhighlight %}

{% highlight c# tabtile="ASP.NET Core" %}

//Create a PDF document

PdfDocument pdfDoc = new PdfDocument();

//Add a page

PdfPage page = pdfDoc.Pages.Add();

//Gets XMP object

XmpMetadata metaData = pdfDoc.DocumentInformation.XmpMetadata;

//XMP PDF Schema

PDFSchema pdfSchema = metaData.PDFSchema;

//Set the PDF Schema details of the document

pdfSchema.Producer = "Syncfusion";

pdfSchema.PDFVersion = "1.5";

pdfSchema.Keywords = "Essential PDF";

//Save and close the document

MemoryStream stream = new MemoryStream();

pdfDoc.Save(stream);

stream.Position = 0;

//Close the document

pdfDoc.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "DocumentInformation.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}

//Create a PDF document

PdfDocument pdfDoc = new PdfDocument();

//Add a page

PdfPage page = pdfDoc.Pages.Add();

//Gets XMP object

XmpMetadata metaData = pdfDoc.DocumentInformation.XmpMetadata;

//XMP PDF Schema

PDFSchema pdfSchema = metaData.PDFSchema;

//Set the PDF Schema details of the document

pdfSchema.Producer = "Syncfusion";

pdfSchema.PDFVersion = "1.5";

pdfSchema.Keywords = "Essential PDF";

//Save the document into stream

MemoryStream memoryStream = new MemoryStream();

pdfDoc.Save(memoryStream);

//Close the documents

pdfDoc.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)

{

    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("DocumentInformation.pdf", "application/pdf", memoryStream);

}

else

{

    Xamarin.Forms.DependencyService.Get<ISave>().Save("DocumentInformation.pdf", "application/pdf", memoryStream);

}

{% endhighlight %}

{% endtabs %}  

### Custom Schema

A custom schema defines the structure of the customized information records. You can use the [CustomSchema](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xmp.CustomSchema.html) class to: 

* Define custom metadata files and, 
* Add them to the PDF document 

Add the following code to define a custom schema. 

{% tabs %}  

{% highlight c# tabtile="C#" %}

//Create Pdf document

PdfDocument pdfDoc = new PdfDocument();

PdfPage page = pdfDoc.Pages.Add();

//Get metaData object

XmpMetadata metaData = pdfDoc.DocumentInformation.XmpMetadata;

//Create custom schema field

CustomSchema customSchema = new CustomSchema(metaData, "custom", "http://www.syncfusion.com");

customSchema["Author"] = "Syncfusion";

customSchema["creationDate"] = DateTime.Now.ToString();

customSchema["DOCID"] = "SYNCSAM001";

customSchema["Encryption"] = "Standard";

customSchema["Project"] = "Data processing";

//Save the document

pdfDoc.Save("DocumentInformation.pdf");

pdfDoc.Close(true);

{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}

'Create Pdf document

Dim pdfDoc As New PdfDocument()

Dim page As PdfPage = pdfDoc.Pages.Add()

'Get metaData object

Dim metaData As XmpMetadata = pdfDoc.DocumentInformation.XmpMetadata

'Create custom schema field

Dim customSchema As New CustomSchema(metaData, "custom", "http://www.syncfusion.com")

customSchema("Author") = "Syncfusion"

customSchema("creationDate") = DateTime.Now.ToString()

customSchema("DOCID") = "SYNCSAM001"

customSchema("Encryption") = "Standard"

customSchema("Project") = "Data processing"

'Save the document

pdfDoc.Save("DocumentInformation.pdf")

pdfDoc.Close(True)

{% endhighlight %}

  {% highlight c# tabtile="UWP" %}

//Essential PDF supports Metadata (XMP) only in Windows Forms, WPF, ASP.NET, ASP.NET MVC, ASP.NET Core and Xamarin platforms

{% endhighlight %}

{% highlight c# tabtile="ASP.NET Core" %}

//Create Pdf document

PdfDocument pdfDoc = new PdfDocument();

PdfPage page = pdfDoc.Pages.Add();

//Get metaData object

XmpMetadata metaData = pdfDoc.DocumentInformation.XmpMetadata;

//Create custom schema field

CustomSchema customSchema = new CustomSchema(metaData, "custom", "http://www.syncfusion.com");

customSchema["creationDate"] = DateTime.Now.ToString();

customSchema["DOCID"] = "SYNCSAM001";

customSchema["Encryption"] = "Standard";

customSchema["Project"] = "Data processing";

//Save and close the document

MemoryStream stream = new MemoryStream();

pdfDoc.Save(stream);

stream.Position = 0;

//Close the document

pdfDoc.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "DocumentInformation.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}

//Create Pdf document

PdfDocument pdfDoc = new PdfDocument();

PdfPage page = pdfDoc.Pages.Add();

//Get metaData object

XmpMetadata metaData = pdfDoc.DocumentInformation.XmpMetadata;

//Create custom schema field

CustomSchema customSchema = new CustomSchema(metaData, "custom", "http://www.syncfusion.com");

customSchema["creationDate"] = DateTime.Now.ToString();

customSchema["DOCID"] = "SYNCSAM001";

customSchema["Encryption"] = "Standard";

customSchema["Project"] = "Data processing";

//Save the document into stream

MemoryStream memoryStream = new MemoryStream();

pdfDoc.Save(memoryStream);

//Close the documents

pdfDoc.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)

{

    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("DocumentInformation.pdf", "application/pdf", memoryStream);

}

else

{

    Xamarin.Forms.DependencyService.Get<ISave>().Save("DocumentInformation.pdf", "application/pdf", memoryStream);

}

{% endhighlight %}

{% endtabs %}  

## Adding Custom Schema to the PDF document

Essential PDF allows you to add required metadata (custom schema) to a PDF document.

You can add custom schema using [XmpMetadata](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xmp.XmpMetadata.html) class. The following code illustrates this.

{% tabs %}  

{% highlight c# tabtile="C#" %}

//Create PDF document

PdfDocument pdfDoc = new PdfDocument();

PdfPage page = pdfDoc.Pages.Add();

//Create XML Document container

XmpMetadata metaData = new XmpMetadata(pdfDoc.DocumentInformation.XmpMetadata.XmlData);

//Create custom schema

CustomSchema customSchema = new CustomSchema(metaData, "custom", "http://www.syncfusion.com");

customSchema["Author"] = "Syncfusion";

customSchema["creationDate"] = DateTime.Now.ToString();

customSchema["DOCID"] = "SYNCSAM001";

//Save and close the document

pdfDoc.Save("CustomMetaField.pdf");

pdfDoc.Close(true);

{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}

'Create PDF document

Dim pdfDoc As New PdfDocument()

Dim page As PdfPage = pdfDoc.Pages.Add()

'Create XML Document container

Dim metaData As New XmpMetadata(pdfDoc.DocumentInformation.XmpMetadata.XmlData)

'Create custom schema

Dim customSchema As New CustomSchema(metaData, "custom", "http://www.syncfusion.com")

customSchema("Author") = "Syncfusion"

customSchema("creationDate") = DateTime.Now.ToString()

customSchema("DOCID") = "SYNCSAM001"

'Save and close the document

pdfDoc.Save("CustomMetaField.pdf")

pdfDoc.Close(True)

{% endhighlight %}

  {% highlight c# tabtile="UWP" %}

//Essential PDF supports Metadata (XMP) only in Windows Forms, WPF, ASP.NET, ASP.NET MVC, ASP.NET Core and Xamarin platforms

{% endhighlight %}

{% highlight c# tabtile="ASP.NET Core" %}

//Create PDF document

PdfDocument pdfDoc = new PdfDocument();

PdfPage page = pdfDoc.Pages.Add();

//Create XML Document container

XmpMetadata metaData = new XmpMetadata(pdfDoc.DocumentInformation.XmpMetadata.XmlData);

//Create custom schema

CustomSchema customSchema = new CustomSchema(metaData, "custom", "http://www.syncfusion.com");

customSchema["Author"] = "Syncfusion";

customSchema["creationDate"] = DateTime.Now.ToString();

customSchema["DOCID"] = "SYNCSAM001";

//Save and close the document

MemoryStream stream = new MemoryStream();

pdfDoc.Save(stream);

stream.Position = 0;

//Close the document

pdfDoc.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "CustomMetaField.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}

//Create PDF document

PdfDocument pdfDoc = new PdfDocument();

PdfPage page = pdfDoc.Pages.Add();

//Create XML Document container

XmpMetadata metaData = new XmpMetadata(pdfDoc.DocumentInformation.XmpMetadata.XmlData);

//Create custom schema

CustomSchema customSchema = new CustomSchema(metaData, "custom", "http://www.syncfusion.com");

customSchema["Author"] = "Syncfusion";

customSchema["creationDate"] = DateTime.Now.ToString();

customSchema["DOCID"] = "SYNCSAM001";

//Save the document into stream

MemoryStream memoryStream = new MemoryStream();

pdfDoc.Save(memoryStream);

//Close the documents

pdfDoc.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)

{

    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("CustomMetaField.pdf", "application/pdf", memoryStream);

}

else

{

    Xamarin.Forms.DependencyService.Get<ISave>().Save("CustomMetaField.pdf", "application/pdf", memoryStream);

}

{% endhighlight %}

{% endtabs %}  

## Adding Custom Metadata to the PDF document

The custom metadata can be added in PDF document by using the [CustomMetadata](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfDocumentInformation.html#Syncfusion_Pdf_PdfDocumentInformation_CustomMetadata) property. Refer to the following code. 

{% tabs %}  

{% highlight c# tabtile="C#" %}

//Create PDF document

PdfDocument pdfDoc = new PdfDocument();

//Add new PDF page

PdfPage page = pdfDoc.Pages.Add();

//Add Custom MetaData

pdfDoc.DocumentInformation.CustomMetadata["ID"] = "IO1";

pdfDoc.DocumentInformation.CustomMetadata["CompanyName"] = "Syncfusion";

pdfDoc.DocumentInformation.CustomMetadata["Key"] = "DocumentKey";

//Save and close the document

pdfDoc.Save("AddCustomField.pdf");

pdfDoc.Close(true);

{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}

'Create PDF document

Dim pdfDoc As New PdfDocument()

'Add new PDF page

Dim page As PdfPage = pdfDoc.Pages.Add()

'Add Custom MetaData

pdfDoc.DocumentInformation.CustomMetadata("ID") = "IO1"

pdfDoc.DocumentInformation.CustomMetadata("CompanyName") = "Syncfusion"

pdfDoc.DocumentInformation.CustomMetadata("Key") = "DocumentKey"

'Save and close the document

pdfDoc.Save("AddCustomField.pdf")

pdfDoc.Close(True)

{% endhighlight %}

  {% highlight c# tabtile="UWP" %}

//Essential PDF supports Metadata (XMP) only in Windows Forms, WPF, ASP.NET, ASP.NET MVC, ASP.NET Core and Xamarin platforms

{% endhighlight %}

{% highlight c# tabtile="ASP.NET Core" %}

//Create PDF document

PdfDocument pdfDoc = new PdfDocument();

//Add new PDF page

PdfPage page = pdfDoc.Pages.Add();

//Add Custom MetaData

pdfDoc.DocumentInformation.CustomMetadata["ID"] = "IO1";

pdfDoc.DocumentInformation.CustomMetadata["CompanyName"] = "Syncfusion";

pdfDoc.DocumentInformation.CustomMetadata["Key"] = "DocumentKey";

//Save and close the document

MemoryStream stream = new MemoryStream();

pdfDoc.Save(stream);

stream.Position = 0;

//Close the document

pdfDoc.Close(true);

//Defining the ContentType for pdf file

string contentType = "application/pdf";

//Define the file name

string fileName = "AddCustomField.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}

//Create PDF document

PdfDocument pdfDoc = new PdfDocument();

//Add new PDF page

PdfPage page = pdfDoc.Pages.Add();

//Add Custom MetaData

pdfDoc.DocumentInformation.CustomMetadata["ID"] = "IO1";

pdfDoc.DocumentInformation.CustomMetadata["CompanyName"] = "Syncfusion";

pdfDoc.DocumentInformation.CustomMetadata["Key"] = "DocumentKey";

//Save the document into stream

MemoryStream memoryStream = new MemoryStream();

pdfDoc.Save(memoryStream);

//Close the documents

pdfDoc.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)

{

    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("AddCustomField.pdf", "application/pdf", memoryStream);

}

else

{

    Xamarin.Forms.DependencyService.Get<ISave>().Save("AddCustomField.pdf", "application/pdf", memoryStream);

}

{% endhighlight %}

{% endtabs %}   

## Removing Custom Metadata from an existing PDF document

You can remove the custom metadata from an existing PDF document as follows. 

{% tabs %}  

{% highlight c# tabtile="C#" %}

//Load the document

PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");

//Remove custom metadata using key name

loadedDocument.DocumentInformation.CustomMetadata.Remove("Key");

//Save and close the document

loadedDocument.Save("Output.pdf");

loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}

'Load the document

Dim loadedDocument As PdfLoadedDocument = New PdfLoadedDocument("Input.pdf")

'Remove custom metadata using key name

loadedDocument.DocumentInformation.CustomMetadata.Remove("Key")

'Save and close the document

loadedDocument.Save("Output.pdf")

loadedDocument.Close(True)

{% endhighlight %}

  {% highlight c# tabtile="UWP" %}

//Essential PDF supports Metadata (XMP) only in Windows Forms, WPF, ASP.NET, ASP.NET MVC, ASP.NET Core and Xamarin platforms

{% endhighlight %}

{% highlight c# tabtile="ASP.NET Core" %}

//Load the PDF document

FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Remove custom metadata using key name

loadedDocument.DocumentInformation.CustomMetadata.Remove("Key");

//Save and close the document

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

{% highlight c# tabtile="Xamarin" %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Remove custom metadata using key name

loadedDocument.DocumentInformation.CustomMetadata.Remove("Key");

//Save the document into stream

MemoryStream memoryStream = new MemoryStream();

loadedDocument.Save(memoryStream);

//Close the documents

loadedDocument.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples

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

## Working with image metadata

Image metadata is a data that describes the characteristics or properties of an image which is embedded in the image file.

## Adding XMP metadata along with an image in a PDF document

You can extract the XMP metadata along with an image and add it with an image to the PDF document as shown in the code snippet below.

{% tabs %}  

{% highlight c# tabtile="C#" %}

//Create a new PDF document

PdfDocument doc = new PdfDocument();

//Add a page to the document

PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page

PdfGraphics graphics = page.Graphics;

//Load the image file from the disk which contains XMP metadata

PdfBitmap image = new PdfBitmap("Autumn Leaves.jpg", true);

//Draw the image

graphics.DrawImage(image, 0, 0);

//Save the document

doc.Save("Output.pdf");

//Close the document

doc.Close(true);

{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}

'Create a new PDF document

Dim doc As New PdfDocument()

'Add a page to the document

Dim page As PdfPage = doc.Pages.Add()

'Create PDF graphics for the page

Dim graphics As PdfGraphics = page.Graphics

'Load the image file from the disk which contains XMP metadata

Dim image As New PdfBitmap("Autumn Leaves.jpg", True)

'Draw the image

graphics.DrawImage(image, 0, 0)

'Save the document

doc.Save("Output.pdf")

'Close the document

doc.Close(True)

{% endhighlight %}

  {% highlight c# tabtile="UWP" %}

//Essential PDF supports adding XMP metadata along with an image only in Windows Forms, WPF, ASP.NET, ASP.NET MVC, ASP.NET Core and Xamarin platforms

{% endhighlight %}

{% highlight c# tabtile="ASP.NET Core" %}

//Create a new PDF document

PdfDocument doc = new PdfDocument();

//Add a page to the document

PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page

PdfGraphics graphics = page.Graphics;

//Load the image as stream which contains XMP metadata

FileStream imageStream = new FileStream("Autumn Leaves.jpg", FileMode.Open, FileAccess.Read);

PdfBitmap image = new PdfBitmap(imageStream, true);

//Draw the image

graphics.DrawImage(image, 0, 0);

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the document as stream

doc.Save(stream);

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

{% highlight c# tabtile="Xamarin" %}

//Create a new PDF document

PdfDocument doc = new PdfDocument();

//Add a page to the document

PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page

PdfGraphics graphics = page.Graphics;

//Load the image as stream which contains XMP metadata

Stream imageStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Autumn Leaves.jpg");

PdfBitmap image = new PdfBitmap(imageStream, true);

//Draw the image

graphics.DrawImage(image, 0, 0);

//Save the document as stream

MemoryStream stream = new MemoryStream();

doc.Save(stream);

//Close the document

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

## Extracting XMP metadata from PDF image

To extract the [XmpMetadata](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Xmp.XmpMetadata.html) from an image in an existing PDF document, you can use the [ImagesInfo](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfPageBase.html#Syncfusion_Pdf_PdfPageBase_ImagesInfo) property in the [PdfPageBase](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfPageBase.html) class.

Refer to the following code snippet to extract the image metadata from a PDF image.

{% tabs %}

{% highlight c# tabtile="C#" %}

//Load an existing PDF

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);

//Load the first page

PdfPageBase pageBase = loadedDocument.Pages[0];

//Extracts all the images info from first page

PdfImageInfo[] imagesInfo= pageBase.ImagesInfo;

//Extracts the XMP metadata from PDF image

XmpMetadata metadata = imagesInfo[0].XmpMetadata;

//Close the document

loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}

'Load an existing PDF

Dim loadedDocument As New PdfLoadedDocument(fileName)

'Load the first page

Dim pageBase As PdfPageBase = loadedDocument.Pages(0)

'Extracts all the images info from first page

Dim imagesInfo As PdfImageInfo[] = pageBase.ImagesInfo

'Extracts the XMP metadata from PDF image

XmpMetadata metadata = imagesInfo[0].XmpMetadata;

'Close the document

loadedDocument.Close(True)

{% endhighlight %}

  {% highlight c# tabtile="UWP" %}

//PDF supports extracting the image information from PDF document only in Windows Forms, WPF, ASP.NET, ASP.NET Core and ASP.NET MVC platforms

{% endhighlight %}

{% highlight c# tabtile="ASP.NET Core" %}

//Load an existing PDF

FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Load the first page

PdfPageBase pageBase = loadedDocument.Pages[0];

//Extracts all the images info from first page

PdfImageInfo[] imagesInfo= pageBase.GetImagesInfo();

//Extracts the XMP metadata from PDF image

XmpMetadata metadata = imagesInfo[0].XmpMetadata;

//Close the document

loadedDocument.Close(true);

{% endhighlight %}

{% highlight c# tabtile="Xamarin" %}

//PDF supports extracting the image information from PDF document only in Windows Forms, WPF, ASP.NET, ASP.NET Core and ASP.NET MVC platforms

{% endhighlight %}

{% endtabs %}

N> To extract the image information from PDF page in .NET Core, you need to include [Syncfusion.Pdf.Imaging.Portable](https://www.nuget.org/packages/Syncfusion.Pdf.Imaging.Net.Core) assembly reference in .NET Core project.
