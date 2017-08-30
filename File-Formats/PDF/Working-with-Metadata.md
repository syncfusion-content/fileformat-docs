---
title: Working with Metadata
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

You can add XMP metadata in a PDF document as shown in the code snippet below.

{% tabs %}  

{% highlight c# %}


//Create a PDF document

PdfDocument pdfDoc = new PdfDocument();

//Create a page

PdfPage page = pdfDoc.Pages.Add();

// Get XMP object.

XmpMetadata xmp = pdfDoc.DocumentInformation.XmpMetadata;

// XMP Basic Schema.

BasicSchema basic = xmp.BasicSchema;

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

{% highlight vb.net %}


'Create a PDF document

Dim pdfDoc As New PdfDocument()

'Create a page

Dim page As PdfPage = pdfDoc.Pages.Add()

' Get XMP object.

Dim xmp As XmpMetadata = pdfDoc.DocumentInformation.XmpMetadata

' XMP Basic Schema.

Dim basic As BasicSchema = xmp.BasicSchema

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

{% endtabs %}  


## Adding XMP metadata in an existing PDF document

You can add metadata in an existing PDF document as follow.

{% tabs %}  

{% highlight c# %}


//Load the document

PdfLoadedDocument pdfDoc = new PdfLoadedDocument("input.pdf");

// Get XMP object.

XmpMetadata xmp = pdfDoc.DocumentInformation.XmpMetadata;

// XMP Basic Schema.

BasicSchema basic = xmp.BasicSchema;

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

{% highlight vb.net %}


'Load the document

Dim pdfDoc As New PdfLoadedDocument("input.pdf")

' Get xmp object.

Dim xmp As XmpMetadata = pdfDoc.DocumentInformation.XmpMetadata

' XMP Basic Schema.

Dim basic As BasicSchema = xmp.BasicSchema

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

BasicSchema class is used to create the basic schema properties.

Refer the following code sample to create XMP basic schema

{% tabs %}  

{% highlight c# %}


//Create a PDF document

PdfDocument pdfDoc = new PdfDocument();

//Create a page

PdfPage page = pdfDoc.Pages.Add();

// Get xmp object.

XmpMetadata xmp = pdfDoc.DocumentInformation.XmpMetadata;

// XMP Basic Schema.

BasicSchema basic = xmp.BasicSchema;

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

{% highlight vb.net %}


'Create a PDF document

Dim pdfDoc As New PdfDocument()

'Create a page

Dim page As PdfPage = pdfDoc.Pages.Add()

' Get xmp object.

Dim xmp As XmpMetadata = pdfDoc.DocumentInformation.XmpMetadata

' XMP Basic Schema.

Dim basic As BasicSchema = xmp.BasicSchema

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

DublinCoreSchema class is used to create the Dublin core schema properties

{% tabs %}  

{% highlight c# %}


//Create new PDF document

PdfDocument pdfDoc = new PdfDocument();

PdfPage page = pdfDoc.Pages.Add();

//Gets XMP object.

XmpMetadata xmp = pdfDoc.DocumentInformation.XmpMetadata;

//XMP Dublincore Schema.

DublinCoreSchema dublin = xmp.DublinCoreSchema;

//Set the Dublin Core Schema details of the document.

dublin.Creator.Add("Syncfusion");

dublin.Description.Add("Title", "Essential PDF creator");

dublin.Title.Add("Resource name", "Documentation");

dublin.Type.Add("PDF");

dublin.Publisher.Add("Essential PDF");

//Saves the document.

pdfDoc.Save("DocumentInformation.pdf");

pdfDoc.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Create new PDF document

Dim pdfDoc As New PdfDocument()

Dim page As PdfPage = pdfDoc.Pages.Add()

'Gets XMP object.

Dim xmp As XmpMetadata = pdfDoc.DocumentInformation.XmpMetadata

'XMP Dublincore Schema.

Dim dublin As DublinCoreSchema = xmp.DublinCoreSchema

'Set the Dublin Core Schema details of the document.

dublin.Creator.Add("Syncfusion")

dublin.Description.Add("Title", "Essential PDF creator")

dublin.Title.Add("Resource name", "Documentation")

dublin.Type.Add("PDF")

dublin.Publisher.Add("Essential PDF")

'Saves the document.

pdfDoc.Save("DocumentInformation.pdf")

pdfDoc.Close(True)



{% endhighlight %}

{% endtabs %}  

### Rights Management Schema

This schema includes properties related to rights management. These properties provide information regarding the legal restrictions associated with a resource.

* Certificate
* Marked
* Owner
* UsageTerm
* WebStatement

{% tabs %} 

{% highlight c# %}



//Create PDF document

PdfDocument pdfDoc = new PdfDocument();

PdfPage page = pdfDoc.Pages.Add();

//Gets XMP object.

XmpMetadata xmp = pdfDoc.DocumentInformation.XmpMetadata;

//XMP Rights Management Schema.

RightsManagementSchema rights = xmp.RightsManagementSchema;

//Set the Rights Management Schema details of the document.

rights.Certificate = new Uri("http://syncfusion.com");

rights.Owner.Add("Syncfusion");

rights.Marked = true;

//Save and close the document.

pdfDoc.Save("DocumentInformation.pdf");

pdfDoc.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Create PDF document

Dim pdfDoc As New PdfDocument()

Dim page As PdfPage = pdfDoc.Pages.Add()

'Gets XMP object.

Dim xmp As XmpMetadata = pdfDoc.DocumentInformation.XmpMetadata

'XMP Rights Management Schema.

Dim rights As RightsManagementSchema = xmp.RightsManagementSchema

'Set the Rights Management Schema details of the document.

rights.Certificate = New Uri("http://syncfusion.com")

rights.Owner.Add("Syncfusion")

rights.Marked = True

'Save and close the document.

pdfDoc.Save("DocumentInformation.pdf")

pdfDoc.Close(True)



{% endhighlight %}

 {% endtabs %}  

### Basic Job Ticket Schema

This schema describes very simple workflow or job information.

* JobRef

{% tabs %} 

{% highlight c# %}



//Create a document

PdfDocument pdfDoc = new PdfDocument();

//Add a page

PdfPage page = pdfDoc.Pages.Add();

// Gets XMP object.

XmpMetadata xmp = pdfDoc.DocumentInformation.XmpMetadata;

// XMP Rights Management Schema.

BasicJobTicketSchema basicJob = xmp.BasicJobTicketSchema;

//Set the Rights Management Schema details of the document.

basicJob.JobRef.Add("PDF document creation");

//Save the document.

pdfDoc.Save("DocumentInformation.pdf");

pdfDoc.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Create a document

Dim pdfDoc As New PdfDocument()

'Add a page

Dim page As PdfPage = pdfDoc.Pages.Add()

' Gets XMP object.

Dim xmp As XmpMetadata = pdfDoc.DocumentInformation.XmpMetadata

' XMP Rights Management Schema.

Dim basicJob As BasicJobTicketSchema = xmp.BasicJobTicketSchema

'Set the Rights Management Schema details of the document.

basicJob.JobRef.Add("PDF document creation")

'Save the document.

pdfDoc.Save("DocumentInformation.pdf")

pdfDoc.Close(True)



{% endhighlight %}

 {% endtabs %}  

### Paged-Text Schema

The Paged-Text schema is used for text appearance on page in a document.

* MaxPageSize
* NPages
* Colorants
* PlateNames

{% tabs %} 

{% highlight c# %}



//Create a Pdf document

PdfDocument pdfDoc = new PdfDocument();

//Create a Page

PdfPage page = pdfDoc.Pages.Add();

//Gets XMP object.

XmpMetadata xmp = pdfDoc.DocumentInformation.XmpMetadata;

//XMP Page text Schema.

PagedTextSchema pagedText = xmp.PagedTextSchema;

//Sets the Page text Schema details of the document.

pagedText.MaxPageSize.Width = 500;

pagedText.MaxPageSize.Height = 750;

pagedText.NPages = 1;

pagedText.PlateNames.Add("Sample page");

//Saves the document.

pdfDoc.Save("DocumentInformation.pdf");

pdfDoc.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Create a Pdf document

Dim pdfDoc As New PdfDocument()

'Create a Page

Dim page As PdfPage = pdfDoc.Pages.Add()

'Gets XMP object.

Dim xmp As XmpMetadata = pdfDoc.DocumentInformation.XmpMetadata

'XMP Page text Schema.

Dim pagedText As PagedTextSchema = xmp.PagedTextSchema

'Sets the Page text Schema details of the document.

pagedText.MaxPageSize.Width = 500

pagedText.MaxPageSize.Height = 750

pagedText.NPages = 1

pagedText.PlateNames.Add("Sample page")

'Saves the document.

pdfDoc.Save("DocumentInformation.pdf")

pdfDoc.Close(True)



{% endhighlight %}

 {% endtabs %}  
 

### PDF schema

This schema specifies properties used with Adobe PDF documents.

PDFSchema class is used to create the PDF Schema. It has the following set of properties.

{% tabs %} 

{% highlight c# %}


//Create a PDF document

PdfDocument pdfDoc = new PdfDocument();

//Add a page

PdfPage page = pdfDoc.Pages.Add();

//Gets XMP object.

XmpMetadata xmp = pdfDoc.DocumentInformation.XmpMetadata;

//XMP PDF Schema.

PDFSchema pdfSchema = xmp.PDFSchema;

//Set the PDF Schema details of the document.

pdfSchema.Producer = "Syncfusion";

pdfSchema.PDFVersion = "1.5";

pdfSchema.Keywords = "Essential PDF";

//Save and Close the document.

pdfDoc.Save("DocumentInformation.pdf");

pdfDoc.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Create a PDF document

Dim pdfDoc As New PdfDocument()

'Add a page

Dim page As PdfPage = pdfDoc.Pages.Add()

'Gets XMP object.

Dim xmp As XmpMetadata = pdfDoc.DocumentInformation.XmpMetadata

'XMP PDF Schema.

Dim pdfSchema As PDFSchema = xmp.PDFSchema

'Set the PDF Schema details of the document.

pdfSchema.Producer = "Syncfusion"

pdfSchema.PDFVersion = "1.5"

pdfSchema.Keywords = "Essential PDF"

'Save and Close the document.

pdfDoc.Save("DocumentInformation.pdf")

pdfDoc.Close(True)



{% endhighlight %}

 {% endtabs %}  

### Custom Schema

A custom schema defines the structure of the customized information records. You can use the CustomSchema class to: 

* Define custom metadata files and, 
* Add them to the PDF document 

Add the following code to define a custom schema. 

{% tabs %}  

{% highlight c# %}


//Create Pdf document

PdfDocument pdfDoc = new PdfDocument();

PdfPage page = pdfDoc.Pages.Add();

// Get xmp object.

XmpMetadata xmp = pdfDoc.DocumentInformation.XmpMetadata;

//Create custom schema field

CustomSchema customSchema = new CustomSchema(xmp, "custom", "http://www.syncfusion.com");

customSchema["Author"] = "Syncfusion";

customSchema["creationDate"] = DateTime.Now.ToString();

customSchema["DOCID"] = "SYNCSAM001";

customSchema["Encryption"] = "Standard";

customSchema["Project"] = "Data processing";

//save the document

pdfDoc.Save("DocumentInformation.pdf");

pdfDoc.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Create Pdf document

Dim pdfDoc As New PdfDocument()

Dim page As PdfPage = pdfDoc.Pages.Add()

' Get xmp object.

Dim xmp As XmpMetadata = pdfDoc.DocumentInformation.XmpMetadata

'Create custom schema field

Dim customSchema As New CustomSchema(xmp, "custom", "http://www.syncfusion.com")

customSchema("Author") = "Syncfusion"

customSchema("creationDate") = DateTime.Now.ToString()

customSchema("DOCID") = "SYNCSAM001"

customSchema("Encryption") = "Standard"

customSchema("Project") = "Data processing"

'save the document

pdfDoc.Save("DocumentInformation.pdf")

pdfDoc.Close(True)



{% endhighlight %}

{% endtabs %}  


## Adding Custom Metadata to the PDF document

Essential PDF allows you to add required metadata (custom metadata) to a PDF document

You can add custom metadata Using XmpMetadata class. The following code illustrates this.

{% tabs %}  

{% highlight c# %}


//Create PDF document

PdfDocument pdfDoc = new PdfDocument();

PdfPage page = pdfDoc.Pages.Add();

//Create XML Document container.

XmpMetadata xmp = new XmpMetadata(pdfDoc.DocumentInformation.XmpMetadata.XmlData);

//Create custom schema.

CustomSchema customSchema = new CustomSchema(xmp, "custom", "http://www.syncfusion.com");

customSchema["Author"] = "Syncfusion";

customSchema["creationDate"] = DateTime.Now.ToString();

customSchema["DOCID"] = "SYNCSAM001";

//Save and close the document.

pdfDoc.Save("CustomMetaField.pdf");

pdfDoc.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Create PDF document

Dim pdfDoc As New PdfDocument()

Dim page As PdfPage = pdfDoc.Pages.Add()

'Create XML Document container.

Dim xmp As New XmpMetadata(pdfDoc.DocumentInformation.XmpMetadata.XmlData)

'Create custom schema.

Dim customSchema As New CustomSchema(xmp, "custom", "http://www.syncfusion.com")

customSchema("Author") = "Syncfusion"

customSchema("creationDate") = DateTime.Now.ToString()

customSchema("DOCID") = "SYNCSAM001"

'Save and close the document.

pdfDoc.Save("CustomMetaField.pdf")

pdfDoc.Close(True)



{% endhighlight %}

{% endtabs %}  