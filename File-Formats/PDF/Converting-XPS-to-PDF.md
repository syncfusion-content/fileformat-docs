---
title: Working with XPS document to PDF Conversion | Syncfusion
description: This section explains how to converting XPS document to PDF document by using Syncfusion .NET PDF library.
platform: file-formats
control: PDF
documentation: UG
---
# Converting XPS document to PDF

The XPS (XML Paper Specification) document format is a fixed document format which consists of structured XML markup that defines the layout of a document and the visual appearance of each page, along with rendering rules for distributing, archiving, rendering, processing and printing the documents.

The following code example explains how to converting XPS document to PDF using [XPSToPdfConverter](https://help.syncfusion.com/cr/file-formats/Syncfusion.XPS.XPSToPdfConverter.html) class.

The below code illustrates how to convert XPS to PDF.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Create converter class
XPSToPdfConverter converter = new XPSToPdfConverter();
//Convert the XPS to PDF
PdfDocument document = converter.Convert(xpsFileName);

//Save and close the document
document.Save("Sample.pdf");
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Create converter class
Dim converter As New XPSToPdfConverter()
'Convert the XPS to PDF
Dim document As PdfDocument = converter.Convert(xpsFileName)

'Save and close the document
document.Save("Sample.pdf")
document.Close(True)

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}

//Create converter class
XPSToPdfConverter converter = new XPSToPdfConverter();
//Load the XPS file
Stream fileStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.xps");
//Convert the XPS to PDF
PdfDocument document = converter.Convert(fileStream);

//Save the PDF document to stream
MemoryStream memoryStream = new MemoryStream();
await document.SaveAsync(memoryStream);
//Close the document
document.Close(true);
//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples
Save(memoryStream, "Sample.pdf");

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}

//Initialize XPS to PDF converter.
XPSToPdfConverter converter = new XPSToPdfConverter();
//Open the XPS file as stream.
FileStream fileStream = new FileStream(“Input.xps", FileMode.Open, FileAccess.ReadWrite);
//Convert the XPS to PDF.
PdfDocument document = converter.Convert(fileStream);

//Creating the stream object.
MemoryStream stream = new MemoryStream(); 
//Save the document into stream.
document.Save(stream); 
//If the position is not set to '0' then the PDF will be empty.
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

{% highlight c# tabtitle="Xamarin" %}

//Essential PDF supports converting XPS document to PDF only in Windows Forms, WPF, ASP.NET, ASP.NET MVC and UWP platforms.

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Document%20conversion/Converting-XPS-to-PDF-document).

N> Essential PDF supports converting XPS to PDF with [Syncfusion.XpsToPdfConverter.Net.Core](https://www.nuget.org/packages/Syncfusion.XpsToPdfConverter.Net.Core) package reference in .NET Core application.
