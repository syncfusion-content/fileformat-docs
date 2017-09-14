---
title: Working with Portfolio
description: This section explains how to create PDF portfolio and the PDF Portfolios allows the user to bring together content from a variety of sources, including documents, drawings, images, e-mail, spreadsheets and web pages
platform: file-formats
control: PDF
documentation: UG
---
# Working with Portfolio

PDF Portfolios allows the user to bring together content from a variety of sources, including documents, drawings, images, e-mail, spreadsheets and web pages. Essential PDF allows the user to create portfolios and also to extract the files from them.

## Creating a PDF portfolio

To create a portfolio and attach a variety of documents, please refer the below code snippet.

{% tabs %}  

{% highlight c# %}


// Create a new instance of PdfDocument class.

PdfDocument document = new PdfDocument();

//Create a new portfolio

document.PortfolioInformation = new PdfPortfolioInformation();

//set the view mode of the portfolio

document.PortfolioInformation.ViewMode = PdfPortfolioViewMode.Tile;

//Create the attachment

PdfAttachment pdfFile = new PdfAttachment("../../Data/CorporateBrochure.pdf");

pdfFile.FileName = "CorporateBrochure.pdf";

//Set the startup document to view

document.PortfolioInformation.StartupDocument = pdfFile;

//Add the attachment to the document

document.Attachments.Add(pdfFile);

// Save and close the document.

document.Save("Sample.pdf");

document.Close(true);





{% endhighlight %}

{% highlight vb.net %}


' Create a new instance of PdfDocument class.

Dim document As New PdfDocument()

'Create a new portfolio

document.PortfolioInformation = New PdfPortfolioInformation()

'Set the view mode of the portfolio

document.PortfolioInformation.ViewMode = PdfPortfolioViewMode.Tile

'Create the attachment

Dim pdfFile As New PdfAttachment("../../Data/CorporateBrochure.pdf")

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


## Extracting file from PDF Portfolio

Essential PDF also provides support for extracting the files from the PDF Portfolio and saving it to the disk. The following code snippet shows the steps to extract files from PDF Portfolio.

{% tabs %} 

{% highlight c# %}


//Load the PDF document

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

{% highlight vb.net %}


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

 
## Removing files from PDF Portfolio

You can also remove the files from PDF Portfolio using following code.

{% tabs %}  

{% highlight c# %}


//Load the PDF document

PdfLoadedDocument document = new PdfLoadedDocument("Sample.pdf");

//Remove the file from the Portfolio

document.Attachments.RemoveAt(1);

//Save and close the document

document.Save("Output.pdf");

document.Close();



{% endhighlight %}

{% highlight vb.net %}


'Load the PDF document

Dim document As New PdfLoadedDocument("Sample.pdf")

'Remove the file from the Portfolio

document.Attachments.RemoveAt(1)

'Save and close the document

document.Save("Output.pdf")

document.Close()



{% endhighlight %}

{% endtabs %}  
