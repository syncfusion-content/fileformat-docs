---
title: How to perform OCR for a PDF document using Net Core  | Syncfusion
description: This section explains how to perform OCR for a PDF document using Net Core.
platform: file-formats
control: PDF
documentation: UG
---

# How to perform OCR for a PDF document using Net Core

Optical Character Recognition (OCR) is a technology that converts scanned paper documents, in the form of PDF files or images, into searchable and editable data. 

The [Syncfusion Essential PDF](https://www.syncfusion.com/pdf-framework/net) supports OCR in the ASP.NET Core platform by using the Tesseract open-source engine from the product version [18.1.0.42](https://www.syncfusion.com/forums/152921/essential-studio-2020-volume-1-release-v18-1-0-42-is-available-for-download). 


## Steps to perform OCR on particular region of a PDF programmatically: 

1.	Create a new C# Windows Forms application project. 
![create-project.png](OCR_images/create_core_project.png)

2.	Install the [Syncfusion.PDF.OCR.Net.Core](https://www.nuget.org/packages/Syncfusion.PDF.OCR.Net.Core/) NuGet package as a reference to your .NET Standard application from [nuget.org](https://www.nuget.org/).  
![NuGet project](OCR_images/install_core_NuGet.png)

3.	The Syncfusion OCR processor internally uses Tesseract libraries to perform OCR, so you must copy the necessary tessdata and TesseractBinaries folders from the NuGet package folder to the project folder to use the OCR feature. The tessdata folder contains OCR language data, and the Tesseractbinaries contain the wrapper assemblies for Tesseract OCR. Please use the following link to download OCR language data for other languages.
[https://github.com/tesseract-ocr/tessdata](https://github.com/tesseract-ocr/tessdata)
![tessdata screenshot](OCR_images/tessdata_copy.png)

4.	Set Copy to Output Directory to Copy if newer for the Data, tessdata, and Tesseractbinaries folder. 
![copying binaries](OCR_images/tessdata_in_project.png)

5.	Refer to the location of the Tesseract assemblies that are passed as a parameter to the OCR processor. 
{% tabs %}  

{% highlight c# tabtitle="C#" %}

OCRProcessor processor = new OCRProcessor(@"TesseractBinaries\")

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

Dim processor As New OCRProcessor("TesseractBinaries\")

{% endhighlight %}

{% endtabs %}  

6.	Refer to the location of TessData that is passed as a parameter to the PerformOCR overload. 

{% tabs %}  

{% highlight c# tabtitle="C#" %}

OCRProcessor processor = new OCRProcessor("Tesseractbinaries\");
processor.PerformOCR(loadedDocument, "tessdata/");

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

Dim processor As New OCRProcessor("Tesseractbinaries\")
processor.PerformOCR(lDoc, "tessdata\")

{% endhighlight %}

{% endtabs %}  

7.	Include the following namespaces in the Program.cs file. 

{% tabs %}  

{% highlight c# tabtitle="C#" %}

using Syncfusion.Pdf.Parsing;
using Syncfusion.OCRProcessor;
using System.Drawing;

{% endhighlight %}

{% highlight c# tabtitle="VB.NET" %}

Imports Syncfusion.Pdf.Parsing
Imports Syncfusion.OCRProcessor
Imports System.Drawing

{% endhighlight %}

{% endtabs %}  

8.	Use the following code sample to perform OCR in the ASP.NET Core applicatio
{% tabs %}  

{% highlight c# tabtitle="C#" %}

string docPath = @"..\..\Data\input.pdf";
FileStream docStream = new FileStream(docPath, FileMode.Open, FileAccess.Read);

 //Load the PDF document.
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

string tesseractPath = @"..\..\Tesseractbinaries\Windows";

//Initialize the OCR processor by providing the path of tesseract binaries.
using (OCRProcessor processor = new OCRProcessor(tesseractPath))
{
//Language to process the OCR.
processor.Settings.Language = Languages.English;

string tessdataPath = @"..\..\tessdata";
 //Process OCR by providing loaded PDF document, Data dictionary, and language.
processor.PerformOCR(loadedDocument, tessdataPath);
}
//Save the PDF to the MemoryStream.
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);

//Close the PDF document.
loadedDocument.Close(true);

//Set the position as '0'
stream.Position = 0;

//Download the PDF document in the browser.
FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");

fileStreamResult.FileDownloadName = "OCR.pdf";

return fileStreamResult;

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

string docPath = @"..\..\Data\input.pdf";
FileStream docStream = new FileStream(docPath, FileMode.Open, FileAccess.Read);

 //Load the PDF document.
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

string tesseractPath = @"..\..\Tesseractbinaries\Windows";

//Initialize the OCR processor by providing the path of tesseract binaries.
using (OCRProcessor processor = new OCRProcessor(tesseractPath))
{
//Language to process the OCR.
processor.Settings.Language = Languages.English;

string tessdataPath = @"..\..\tessdata";
 //Process OCR by providing loaded PDF document, Data dictionary, and language.
processor.PerformOCR(loadedDocument, tessdataPath);
}
//Save the PDF to the MemoryStream.
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);

//Close the PDF document.
loadedDocument.Close(true);

//Set the position as '0'
stream.Position = 0;

//Download the PDF document in the browser.
FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");

fileStreamResult.FileDownloadName = "OCR.pdf";

return fileStreamResult;

{% endhighlight %}

{% endtabs %} 

A complete working sample can be downloaded here [OCRSample.zip](https://www.syncfusion.com/downloads/support/directtrac/general/ze/OCRCore_Sample794063060.zip)

By executing the program, you will get the text file (contains extracted text) as follows. 
![output-pdf](OCR_images/core_output.png)



