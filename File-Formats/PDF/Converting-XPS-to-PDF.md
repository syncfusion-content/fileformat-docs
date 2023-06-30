---
title: Working with XPS document to PDF Conversion | Syncfusion
description: This section explains how to converting XPS document to PDF document by using Syncfusion .NET PDF library.
platform: file-formats
control: PDF
documentation: UG
---
# Converting XPS document to PDF

The XPS (XML Paper Specification) document format is a fixed document format which consists of structured XML markup that defines the layout of a document and the visual appearance of each page, along with rendering rules for distributing, archiving, rendering, processing and printing the documents.

The following code example illustrates how to converting XPS document to PDF using [XPSToPdfConverter](https://help.syncfusion.com/cr/file-formats/Syncfusion.XPS.XPSToPdfConverter.html) class.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Initialize XPS to PDF converter.
XPSToPdfConverter converter = new XPSToPdfConverter();
//Open the XPS file as stream.
FileStream fileStream = new FileStream("Input.xps", FileMode.Open, FileAccess.ReadWrite);
//Convert the XPS to PDF.
PdfDocument document = converter.Convert(fileStream);

//Creating the stream object.
MemoryStream stream = new MemoryStream(); 
//Save the document into stream.
document.Save(stream); 
//Close the documents.
document.Close(true); 

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Create converter class.
XPSToPdfConverter converter = new XPSToPdfConverter();
//Convert the XPS to PDF document.
PdfDocument document = converter.Convert(xpsFileName);

//Save and close the document.
document.Save("Sample.pdf");
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Create converter class
Dim converter As New XPSToPdfConverter()
'Convert the XPS to PDF
Dim document As PdfDocument = converter.Convert(xpsFileName)

'Save and close the document
document.Save("Sample.pdf")
document.Close(True)

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Document%20conversion/Converting-XPS-to-PDF-document).

N> The Syncfusion .NET PDF library supports converting XPS to PDF with [Syncfusion.XpsToPdfConverter.Net.Core](https://www.nuget.org/packages/Syncfusion.XpsToPdfConverter.Net.Core) NuGet package reference in ASP.NET Core application.
