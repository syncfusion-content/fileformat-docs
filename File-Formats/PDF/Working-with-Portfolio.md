---
title: Working with Portfolio | Syncfusion
description: Explains how to create PDF portfolio which helps to bring together content from a variety of sources, including documents, drawings, images, e-mail, & web pages
platform: file-formats
control: PDF
documentation: UG
---
# Working with Portfolio

PDF Portfolios allows the user to bring together content from a variety of sources, including documents, drawings, images, e-mail, spreadsheets and web pages. Essential PDF allows the user to create portfolios and also to extract the files from them.

## Creating a PDF portfolio

You can create a portfolio using [PdfPortfolioInformation](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfPortfolioInformation.html) class and attach a variety of documents using [PdfAttachment](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfAttachment.html) class. The following code example illustrates this.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Create a new instance of PdfDocument class
PdfDocument document = new PdfDocument();

//Create a new portfolio
document.PortfolioInformation = new PdfPortfolioInformation();
//Set the view mode of the portfolio
document.PortfolioInformation.ViewMode = PdfPortfolioViewMode.Tile;

//Create the attachment
FileStream pdfStream = new FileStream("CorporateBrochure.pdf", FileMode.Open, FileAccess.Read);
PdfAttachment pdfFile = new PdfAttachment("CorporateBrochure.pdf", pdfStream);
pdfFile.FileName = "CorporateBrochure.pdf";
//Set the startup document to view
document.PortfolioInformation.StartupDocument = pdfFile;

//Add the attachment to the document
document.Attachments.Add(pdfFile);

//Save the document into stream.
MemoryStream stream = new MemoryStream();
document.Save(stream);
stream.Position = 0;
//Close the document
document.Close(true);
//Defining the content type for PDF file
string contentType = "application/pdf";
//Define the file name.
string fileName = "Sample.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name.
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Create a new instance of PdfDocument class
PdfDocument document = new PdfDocument();

//Create a new portfolio
document.PortfolioInformation = new PdfPortfolioInformation();
//Set the view mode of the portfolio
document.PortfolioInformation.ViewMode = PdfPortfolioViewMode.Tile;

//Create the attachment
PdfAttachment pdfFile = new PdfAttachment("CorporateBrochure.pdf");
pdfFile.FileName = "CorporateBrochure.pdf";
//Set the startup document to view
document.PortfolioInformation.StartupDocument = pdfFile;

//Add the attachment to the document
document.Attachments.Add(pdfFile);

//Save and close the document.
document.Save("Sample.pdf");
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Create a new instance of PdfDocument class
Dim document As New PdfDocument()

'Create a new portfolio
document.PortfolioInformation = New PdfPortfolioInformation()
'Set the view mode of the portfolio
document.PortfolioInformation.ViewMode = PdfPortfolioViewMode.Tile

'Create the attachment
Dim pdfFile As New PdfAttachment("CorporateBrochure.pdf")
pdfFile.FileName = "CorporateBrochure.pdf"
'Set the startup document to view
document.PortfolioInformation.StartupDocument = pdfFile

'Add the attachment to the document
document.Attachments.Add(pdfFile)

'Save and close the document.
document.Save("Sample.pdf")
document.Close(True)

{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Portfolio/Create-a-portfolio-and-attach-variety-of-documents).

## Extracting file from PDF Portfolio

The Essential PDF provides support for extracting the files from the PDF Portfolio using [Attachments](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html#Syncfusion_Pdf_Parsing_PdfLoadedDocument_Attachments) property of [PdfLoadedDocument](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html) class and saving the files to the disk. The following code sample shows the steps to extract files from PDF Portfolio.

{% tabs %} 

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Load an existing PDF document
FileStream docStream = new FileStream("Sample.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument document = new PdfLoadedDocument(docStream);

//Iterate the attachments
foreach (PdfAttachment attachment in document.Attachments)
{
    //Extract the attachment and save to the disk
    FileStream s = new FileStream(attachment.FileName, FileMode.Create);
    s.Write(attachment.Data, 0, attachment.Data.Length);
    s.Dispose();
}

//Save the document into stream
MemoryStream stream = new MemoryStream();
document.Save(stream);
stream.Position = 0;
//Close the document
document.Close(true);
//Defining the content type for PDF file
string contentType = "application/pdf";
//Define the file name
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Load an existing PDF document
PdfLoadedDocument document = new PdfLoadedDocument("Sample.pdf");

//Iterate the attachments
foreach (PdfAttachment attachment in document.Attachments)
{
    //Extract the attachment and save to the disk
    FileStream s = new FileStream(attachment.FileName, FileMode.Create);
    s.Write(attachment.Data, 0, attachment.Data.Length);
    s.Dispose();
}

//Save and close the document
document.Save("Output.pdf");
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Load the PDF document
Dim document As New PdfLoadedDocument("Sample.pdf")

'Iterate the attachments
For Each attachment As PdfAttachment In document.Attachments
    'Extracting the attachment and saving into the local disk
    Dim s As New FileStream(attachment.FileName, FileMode.Create)
    s.Write(attachment.Data, 0, attachment.Data.Length)
    s.Dispose()
Next

'Save and close the document
document.Save("Output.pdf")
document.Close(True)

{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Portfolio/Extracting-the-files-from-PDF-portfolio).

## Removing files from PDF Portfolio

The following code example illustrates how to remove files from an existing PDF portfolio using [RemoveAt](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfAttachmentCollection.html#Syncfusion_Pdf_Interactive_PdfAttachmentCollection_RemoveAt_System_Int32_) method or [Remove](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfAttachmentCollection.html#Syncfusion_Pdf_Interactive_PdfAttachmentCollection_Remove_Syncfusion_Pdf_Interactive_PdfAttachment_) method of [PdfAttachmentCollection](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfAttachmentCollection.html) class. 

{% tabs %}  

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Load the PDF document
FileStream docStream = new FileStream("Sample.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument document = new PdfLoadedDocument(docStream);

//Remove the file from the Portfolio
document.Attachments.RemoveAt(0);

//Save and close the document
MemoryStream stream = new MemoryStream();
document.Save(stream);
stream.Position = 0;
//Close the document
document.Close(true);
//Defining the content type for PDF file
string contentType = "application/pdf";
//Define the file name
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Load the PDF document
PdfLoadedDocument document = new PdfLoadedDocument("Sample.pdf");

//Remove the file from the Portfolio
document.Attachments.RemoveAt(0);

//Save and close the document
document.Save("Output.pdf");
document.Close();

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Load the PDF document
Dim document As New PdfLoadedDocument("Sample.pdf")

'Remove the file from the Portfolio
document.Attachments.RemoveAt(1)

'Save and close the document
document.Save("Output.pdf")
document.Close()

{% endhighlight %}

{% endtabs %} 

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Portfolio/Remove-the-files-from-PDF-portfolio).
