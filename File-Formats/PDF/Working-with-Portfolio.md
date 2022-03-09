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

You can create a portfolio using [PdfPortfolioInformation](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfPortfolioInformation.html) class and attach a variety of documents. The following code snippet illustrates this.

{% tabs %}  

{% highlight c# tabtitle="C#" %}


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

{% highlight vb.net tabtitle="VB.NET" %}


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

  {% highlight c# tabtitle="UWP" %}

// Create a new instance of PdfDocument class.

PdfDocument document = new PdfDocument();

//Create a new portfolio

document.PortfolioInformation = new PdfPortfolioInformation();

//set the view mode of the portfolio

document.PortfolioInformation.ViewMode = PdfPortfolioViewMode.Tile;

//Create the attachment

Stream pdfStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Sample.pdf");

PdfAttachment pdfFile = new PdfAttachment("Sample.pdf", pdfStream);

pdfFile.FileName = "Sample.pdf";

//Set the startup document to view

document.PortfolioInformation.StartupDocument = pdfFile;

//Add the attachment to the document

document.Attachments.Add(pdfFile);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document

document.Close(true);                                                                   

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

// Create a new instance of PdfDocument class.

PdfDocument document = new PdfDocument();

//Create a new portfolio

document.PortfolioInformation = new PdfPortfolioInformation();

//set the view mode of the portfolio

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

//Close the document.

document.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Sample.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}

// Create a new instance of PdfDocument class.

PdfDocument document = new PdfDocument();

//Create a new portfolio

document.PortfolioInformation = new PdfPortfolioInformation();

//set the view mode of the portfolio

document.PortfolioInformation.ViewMode = PdfPortfolioViewMode.Tile;

//Create the attachment

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample.pdf");

PdfAttachment pdfFile = new PdfAttachment("Sample.pdf", docStream);

pdfFile.FileName = "Sample.pdf";

//Set the startup document to view

document.PortfolioInformation.StartupDocument = pdfFile;

//Add the attachment to the document

document.Attachments.Add(pdfFile);

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


## Extracting file from PDF Portfolio

Essential PDF also provides support for extracting the files from the PDF Portfolio and saving it to the disk. The following code snippet shows the steps to extract files from PDF Portfolio.

{% tabs %} 

{% highlight c# tabtitle="C#" %}


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

{% highlight vb.net tabtitle="VB.NET" %}


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

  {% highlight c# tabtitle="UWP" %}

//PDF supports extracting file from PDF Portfolio only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load the PDF document

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

//PDF supports extracting file from PDF Portfolio only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

{% endhighlight %}

 {% endtabs %}  

 
## Removing files from PDF Portfolio

You can also remove the files from PDF Portfolio using following code.

{% tabs %}  

{% highlight c# tabtitle="C#" %}


//Load the PDF document

PdfLoadedDocument document = new PdfLoadedDocument("Sample.pdf");

//Remove the file from the Portfolio

document.Attachments.RemoveAt(1);

//Save and close the document

document.Save("Output.pdf");

document.Close();



{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}


'Load the PDF document

Dim document As New PdfLoadedDocument("Sample.pdf")

'Remove the file from the Portfolio

document.Attachments.RemoveAt(1)

'Save and close the document

document.Save("Output.pdf")

document.Close()



{% endhighlight %}

  {% highlight c# tabtitle="UWP" %}

//Create the file open picker

var picker = new FileOpenPicker();

picker.FileTypeFilter.Add(".pdf");

//Browse and chose the file

StorageFile file = await picker.PickSingleFileAsync();

//Creates an empty PDF loaded document instance

PdfLoadedDocument document = new PdfLoadedDocument();

//Loads or opens an existing PDF document through Open method of PdfLoadedDocument class

await document.OpenAsync(file);

//Remove the file from the Portfolio

document.Attachments.RemoveAt(1);

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document

document.Close(true);                                                                   

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(stream, "output.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Load the PDF document

FileStream docStream = new FileStream("Sample.pdf", FileMode.Open, FileAccess.Read);

PdfLoadedDocument document = new PdfLoadedDocument(docStream);

//Remove the file from the Portfolio

document.Attachments.RemoveAt(0);

//Save and close the document

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

// Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample.pdf");

PdfLoadedDocument document = new PdfLoadedDocument(docStream);

//Remove the file from the Portfolio

document.Attachments.RemoveAt(0);

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
