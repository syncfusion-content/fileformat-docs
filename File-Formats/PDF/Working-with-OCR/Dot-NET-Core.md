---
title: OCR processor for .NET Core with tesseract | Syncfusion
description: This section explains how to process OCR for the existing PDF documents and Images with different version tesseract.
platform: file-formats
control: PDF
documentation: UG
---

# Working with Optical Character Recognition (OCR)

Essential PDF provides support for Optical Character Recognition with the help of Google’s Tesseract Optical Character Recognition engine.

N> Starting with v20.1.0.x, if you reference Syncfusion OCR processor assemblies from trial setup or from the NuGet feed, you also have to include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/license-key) to know about registering Syncfusion license key in your application to use our components.

## Prerequisites

To use the OCR feature in the .NET core and .NET application, the following assemblies or NuGet packages should be added as a reference to the project:

### Assemblies

<table>
<thead>
<tr>
<th>
.NET Standard 2.0<br/><br/></th><th>
.NET Standard 2.0 / .NET 5/.NET 6<br/><br/></th>
</tr>

</thead>
<tbody>
<tr>
<td>
Syncfusion.Compression.Portable.dll<br>
Syncfusion.Pdf.Portable.dll<br>
Syncfusion.PdfImaging.Portable.dll<br>
Syncfusion.OCRProcessor.Portable.dll<br>
{{'[System.Drawing.Common](https://www.nuget.org/packages/System.Drawing.Common/4.5.0)'| markdownify }} package (v 4.5.0 or above)
<br/><br/></td><td>
Syncfusion.Compression.NET.dll<br>
Syncfusion.Pdf.NET.dll<br>
Syncfusion.PdfImaging.NET.dll<br>
Syncfusion.OCRProcessor.NET.dll<br>
{{'[SkiaSharp](https://www.nuget.org/packages/SkiaSharp/2.88.0-preview.232)'| markdownify }} package
<br/><br/></td>
</tr>
</tbody>
</table>

### NuGet

<table>
<tr>
<thead>
<th><b>.NET  Version</b></th>
<th><b>NuGet Package</b></th>
</thead>
</tr>
<tr>
<td>
.NET Standard 2.0/.NET Standard 2.1/.NET Core 2.0/.NET Core 2.1/.NET Core 3.1
</td>
<td>
{{'[Syncfusion.PDF.OCR.Net.Core](https://www.nuget.org/packages/Syncfusion.PDF.OCR.Net.Core/)'| markdownify }}
</td>
</tr>
<tr>
<td>
.NET Standard 2.0/.NET Standard 2.1/.NET Core 2.0/.NET Core 2.1/.NET Core 3.1/.NET 5.0/.NET 6.0
</td>
<td>
{{'[Syncfusion.PDF.OCR.NET](https://www.nuget.org/packages/Syncfusion.PDF.OCR.NET/)'| markdownify }}
</td>
</tr>
</table>

N> TesseractBinaries and tessdata folders can be copied automatically from the NuGet packages. There is no need to copy these folders and set the path. 

## Prerequisites for Windows 

*   Provide the TesseractBinaries windows folder path when creating a new OCR processor. Please refer to the following code snippet for windows.
{% capture codesnippet1 %}
{% tabs %}  

{% highlight c# tabtitle="ASP.NET Core" %}


OCRProcessor processor = new OCRProcessor(@"TesseractBinaries/Windows");


{% endhighlight %}

{% endtabs %}
{% endcapture %}
{{ codesnippet1 | OrderList_Indent_Level_1 }} 

*   Provide the tesseract language data folder path (tessdata) when performing the OCR to recognize different language images.
{% capture codesnippet2 %}
{% tabs %}  

{% highlight c# tabtitle="ASP.NET Core" %}


processor.PerformOCR(lDoc, "tessdata/");


{% endhighlight %}

{% endtabs %} 
{% endcapture %}
{{ codesnippet2 | OrderList_Indent_Level_1 }}

You can download the language packages from the following link

[https://code.google.com/p/tesseract-ocr/downloads/list](https://code.google.com/p/tesseract-ocr/downloads/list)
        


## Prerequisites for Linux

*	We are using the “System.Drawing.Common” API in the OCR Processor. So, it is mandatory to install the “libgdiplus” and “libopenjp2-7” package. Please refer to the following commands to install the packages.

        1. sudo apt-get update
        2. sudo apt-get install libgdiplus
        3. sudo apt-get install y- libopenjp2-7
 
*	Provide the TesseractBinaries Linux folder path when creating a new OCR processor. Please refer to the following code snippet for Linux.
{% capture codesnippet3 %}
{% tabs %}  

{% highlight c# tabtitle="ASP.NET Core" %}


OCRProcessor processor = new OCRProcessor(@"TesseractBinaries/Linux");


{% endhighlight %}

{% endtabs %} 
{% endcapture %}
{{ codesnippet3 | OrderList_Indent_Level_1 }}

*	Provide the tesseract language data folder path (tessdata) when performing the OCR to recognize different language images.
 {% capture codesnippet4 %}             
{% tabs %}  

{% highlight c# tabtitle="ASP.NET Core" %}


processor.PerformOCR(lDoc, "tessdata/");


{% endhighlight %}

{% endtabs %} 
{% endcapture %}
{{ codesnippet4 | OrderList_Indent_Level_1 }}

You can download the language packages from the following link
        
[https://code.google.com/p/tesseract-ocr/downloads/list](https://code.google.com/p/tesseract-ocr/downloads/list)


## Prerequisites for Mac


*	We are internally using the “System.Drawing.Common” package to process the image and perform the OCR in the OCR Processor. So, it is mandatory to install the “'libgdiplus”, and “tesseract” packages in the Mac machine where the OCR operations occur. Please refer to the following commands to install this package.

        1. brew install mono-libgdiplus
        2. brew install tesseract

*	Provide the TesseractBinaries Mac folder path when creating a new OCR processor. Please refer to the following code snippet for Mac.
{% capture codesnippet5 %}
{% tabs %}  

{% highlight c# tabtitle="ASP.NET Core" %}


OCRProcessor processor = new OCRProcessor(@"TesseractBinaries/Mac");


{% endhighlight %}

{% endtabs %} 
{% endcapture %}
{{ codesnippet5 | OrderList_Indent_Level_1 }}

*	Provide the tesseract language data folder path (tessdata) when performing the OCR to recognize different language images.
{% capture codesnippet6 %}
{% tabs %}  

{% highlight c# tabtitle="ASP.NET Core" %}


processor.PerformOCR(lDoc, "tessdata/");


{% endhighlight %}

{% endtabs %} 
{% endcapture %}
{{ codesnippet6 | OrderList_Indent_Level_1 }}

You can download the language packages from the following link
        
[https://code.google.com/p/tesseract-ocr/downloads/list](https://code.google.com/p/tesseract-ocr/downloads/list)


## Performing OCR in Windows

To perform the OCR in the ASP.NET Core project in Windows, refer to the following code snippet,

{% tabs %}   

{% highlight c# tabtitle="ASP.NET Core" %}


//Initialize the OCR processor with tesseract binaries folder path
using (OCRProcessor processor = new OCRProcessor(@"TesseractBinaries/Windows"))
{
//Load a PDF document
FileStream stream = new FileStream(@"Input.pdf", FileMode.Open);
PdfLoadedDocument document = new PdfLoadedDocument(stream);

//Set OCR language
processor.Settings.Language = Languages.English;

//Perform OCR with input document and tessdata (Language packs)
processor.PerformOCR(document, @"tessdata/");

MemoryStream outputStream = new MemoryStream();

//Save the document into stream.
document.Save(outputStream); 

//If the position is not set to '0' then the PDF will be empty. 
outputStream.Position = 0;
 
//Close the document. 
document.Close(true); 

//Defining the ContentType for pdf file.
string contentType = "application/pdf"; 

//Define the file name.
string fileName = "Output.pdf"; 

//Creates a FileContentResult object by using the file contents, content type, and file name. 
return File(outputStream, contentType, fileName);
}


{% endhighlight %}

{% endtabs %} 

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/OCR/.NET/Perform-OCR-for-the-entire-PDF-document).

## Performing OCR in Linux

To perform the OCR in the ASP.NET Core project in Linux, refer to the following code snippet,

{% tabs %}   

{% highlight c# tabtitle="ASP.NET Core" %}

//Initialize the OCR processor with tesseract binaries folder path
using (OCRProcessor processor = new OCRProcessor(@"TesseractBinaries/Linux"))
{
//Load a PDF document
FileStream stream = new FileStream(@"Input.pdf", FileMode.Open);
PdfLoadedDocument document = new PdfLoadedDocument(stream);

//Set OCR language
processor.Settings.Language = Languages.English;

//Perform OCR with input document and tessdata (Language packs)
processor.PerformOCR(document, @"tessdata/");

MemoryStream outputStream = new MemoryStream();

//Save the document into stream.
document.Save(outputStream); 

//If the position is not set to '0' then the PDF will be empty. 
outputStream.Position = 0;
 
//Close the document. 
document.Close(true); 

//Defining the ContentType for pdf file.
string contentType = "application/pdf"; 

//Define the file name.
string fileName = "Output.pdf"; 

//Creates a FileContentResult object by using the file contents, content type, and file name. 
return File(outputStream, contentType, fileName);
}


{% endhighlight %}

{% endtabs %} 

## Performing OCR in Mac

To perform the OCR in the ASP.NET Core project in Mac, refer to the following code snippet,

{% tabs %}   

{% highlight c# tabtitle="ASP.NET Core" %}


//Initialize the OCR processor with tesseract binaries folder path
using (OCRProcessor processor = new OCRProcessor(@"TesseractBinaries/Mac"))
{
//Load a PDF document
FileStream stream = new FileStream(@"Input.pdf", FileMode.Open);
PdfLoadedDocument document = new PdfLoadedDocument(stream);

//Set OCR language
processor.Settings.Language = Languages.English;

//Perform OCR with input document and tessdata (Language packs)
processor.PerformOCR(document, @"tessdata/");

MemoryStream outputStream = new MemoryStream();

//Save the document into stream.
document.Save(outputStream); 

//If the position is not set to '0' then the PDF will be empty. 
outputStream.Position = 0;
 
//Close the document. 
document.Close(true); 

//Defining the ContentType for pdf file.
string contentType = "application/pdf"; 

//Define the file name.
string fileName = "Output.pdf"; 

//Creates a FileContentResult object by using the file contents, content type, and file name. 
return File(outputStream, contentType, fileName);
}


{% endhighlight %}

{% endtabs %} 

N> The [PerformOCR](https://help.syncfusion.com/cr/file-formats/Syncfusion.OCRProcessor.Base~Syncfusion.OCRProcessor.OCRProcessor~PerformOCR(PdfLoadedDocument,String).html) methods return only the text OCRed by [OCRProcessor](https://help.syncfusion.com/cr/file-formats/Syncfusion.OCRProcessor.OCRProcessor.html). Other existing text in the PDF page will not be returned in this method.

## Performing OCR for a region

You can perform OCR on particular region of the PDF page with help of the [PageRegion](https://help.syncfusion.com/cr/file-formats/Syncfusion.OCRProcessor.PageRegion.html) class. Refer to the following code snippet,

{% tabs %}   

{% highlight c# tabtitle="ASP.NET Core" %}



//Initialize the OCR processor by providing the path of the tesseract 
using (OCRProcessor processor = new OCRProcessor(@"TesseractBinaries/Windows"))
{
//Load a PDF document
FileStream stream = new FileStream(@"Input.pdf", FileMode.Open);

PdfLoadedDocument document = new PdfLoadedDocument(stream);

//Set OCR language to process
processor.Settings.Language = Languages.English;

RectangleF rect = new RectangleF(0, 100, 950, 150);
//Assign rectangles to the page
List<PageRegion> pageRegions = new List<PageRegion>();
//Create page region
PageRegion region = new PageRegion();
//Set page index
region.PageIndex = 1;
//Set page region
region.PageRegions = new RectangleF[] { rect };
//Add region to page region
pageRegions.Add(region);
//Set page regions
processor.Settings.Regions = pageRegions;
//Perform OCR with input document and tessdata (Language packs)
processor.PerformOCR(document, @"tessdata/");

//Creating the stream object 
MemoryStream outputStream = new MemoryStream();

//Save the document into stream.
document.Save(outputStream); 

//If the position is not set to '0' then the PDF will be empty. 
outputStream.Position = 0;
 
//Close the documents. 
document.Close(true); 

//Defining the ContentType for pdf file.
string contentType = "application/pdf"; 

//Define the file name.
string fileName = "Output.pdf"; 

//Creates a FileContentResult object by using the file contents, content type, and file name. 
return File(outputStream, contentType, fileName);
}



{% endhighlight %}

{% endtabs %} 

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/OCR/.NET/Perform-OCR-on-particular-region-of-PDF-document).

## Performing OCR with rotated pages

You can perform OCR on the rotated page of a PDF document. Refer to the following code snippet for the same.

{% tabs %} 

{% highlight c# tabtitle="ASP.NET Core" %}



//Initialize the OCR processor by providing the path of tesseract 
using (OCRProcessor processor = new OCRProcessor(@"TesseractBinaries/Windows"))
{
//Load a PDF document
FileStream stream = new FileStream(@"Input.pdf", FileMode.Open);

PdfLoadedDocument document = new PdfLoadedDocument(stream);

//Set OCR language to process
processor.Settings.Language = Languages.English;

//Set the Page Segment Mode.
processor.Settings.PageSegment = PageSegMode.AutoOsd;

//Process OCR by providing the PDF document, data dictionary, and language
processor.PerformOCR(document, @"tessdata/");

//Creating the stream object 
MemoryStream outputStream = new MemoryStream();

//Save the document into stream.
document.Save(outputStream); 

//If the position is not set to '0' then the PDF will be empty. 
outputStream.Position = 0;
 
//Close the documents. 
document.Close(true); 

//Defining the ContentType for pdf file.
string contentType = "application/pdf"; 

//Define the file name.
string fileName = "Output.pdf"; 

//Creates a FileContentResult object by using the file contents, content type, and file name.
return File(outputStream, contentType, fileName);
}



{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/OCR/.NET/Perform-OCR-on-the-rotated-page-of-the-PDF-document).

## Performing OCR with Unicode characters 

You can perform OCR on Images with Unicode characters. To preserve the Unicode characters in the PDF document, use the UnicodeFont property. Refer to the following code snippet.

{% tabs %} 

{% highlight c# tabtitle="ASP.NET Core" %}


//Initialize the OCR processor by providing the path of tesseract 
using (OCRProcessor processor = new OCRProcessor(@"TesseractBinaries/Windows"))
{
//Load a PDF document
FileStream stream = new FileStream(@"Input.pdf", FileMode.Open);

PdfLoadedDocument document = new PdfLoadedDocument(stream);

// Sets Unicode font to preserve the Unicode characters in a PDF document.
FileStream fontStream = new FileStream(@"ARIALUNI.ttf", FileMode.Open);

processor.UnicodeFont = new PdfTrueTypeFont(fontStream, 8); 

//Set OCR language to process
processor.Settings.Language = Languages.English;

//Process OCR by providing the PDF document, data dictionary, and language
processor.PerformOCR(document, @"tessdata/");

//Creating the stream object 
MemoryStream outputStream = new MemoryStream();

//Save the document into stream.
document.Save(outputStream); 

//If the position is not set to '0' then the PDF will be empty. 
outputStream.Position = 0;
 
//Close the documents. 
document.Close(true); 

//Defining the ContentType for pdf file.
string contentType = "application/pdf"; 

//Define the file name.
string fileName = "Output.pdf"; 

//Creates a FileContentResult object by using the file contents, content type, and file name.
return File(outputStream, contentType, fileName);
}


{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/OCR/.NET/Perform-OCR-with-unicode-characters-in-a-PDF-document).

## Layout result 

You can get the OCRed text and its bounds from an input PDF document by using the [OCRLayoutResult](https://help.syncfusion.com/cr/file-formats/Syncfusion.OCRProcessor.OCRLayoutResult.html) Class. Refer to the following code snippet. 
 
{% tabs %} 

{% highlight c# tabtitle="ASP.NET Core" %}


//Initialize the OCR processor by providing the path of tesseract 
using (OCRProcessor processor = new OCRProcessor(@"TesseractBinaries/Windows"))
{
//Load a PDF document
FileStream stream = new FileStream(@"Input.pdf", FileMode.Open);

PdfLoadedDocument document = new PdfLoadedDocument(stream);

//Set OCR language to process
processor.Settings.Language = Languages.English;

//Process OCR by providing the PDF document, data dictionary, and language
processor.PerformOCR(document, @"TessData/", out result); 
//Get OCRed line collection from first page 
OCRLineCollection lines = result.Pages[0].Lines;
//Get each OCRed line and its bounds 
foreach(Line line in lines)
{ 
   string text = line.Text;
   RectangleF bounds = line.Rectangle;
}
 
//Creating the stream object 
MemoryStream outputStream = new MemoryStream();

//Save the document into stream.
document.Save(outputStream); 

//If the position is not set to '0' then the PDF will be empty. 
outputStream.Position = 0;
 
//Close the documents. 
document.Close(true); 

//Defining the ContentType for pdf file.
string contentType = "application/pdf"; 

//Define the file name.
string fileName = "Output.pdf"; 

//Creates a FileContentResult object by using the file contents, content type, and file name.
return File(outputStream, contentType, fileName);
}


{% endhighlight %}

{% endtabs %} 

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/OCR/.NET/Get-the-OCR'ed-text-and-its-bounds-from-an-input-PDF).

## Performing OCR with image

You can perform OCR with images.

N> To perform OCR on images, we need to provide the image stream as input if you are using Syncfusion.PDF.OCR.NET package.

Refer to the following code snippet for Syncfusion.PDF.OCR.Net.Core package:

{% tabs %} 

{% highlight c# tabtitle="ASP.NET Core" %}


//Initialize the OCR processor by providing the path of the tesseract binaries

using (OCRProcessor processor = new OCRProcessor(@"TesseractBinaries/"))
{
//loading the input image
FileStream stream = new FileStream(@"Input.jpeg ", FileMode.Open);

Bitmap image = new Bitmap(stream);

//Set OCR language to process
processor.Settings.Language = Languages.English;

//Process OCR by providing the bitmap image, data dictionary, and language
string ocrText= processor.PerformOCR(image, @"tessdata/");

}
			
{% endhighlight %}

{% endtabs %}

Refer to the following code snippet for Syncfusion.PDF.OCR.NET package:

{% tabs %} 

{% highlight c# tabtitle="ASP.NET Core" %}

//Initialize the OCR processor by providing the path of the tesseract binaries
using (OCRProcessor processor = new OCRProcessor(@"TesseractBinaries/"))
{

FileStream stream = new FileStream("Helloworld.jpg", FileMode.Open);

//Set OCR language to process
processor.Settings.Language = Languages.English;

// Sets Unicode font to preserve the Unicode characters in a PDF document.
FileStream fontStream = new FileStream(@"ARIALUNI.ttf", FileMode.Open);

processor.UnicodeFont = new PdfTrueTypeFont(fontStream, 8);

//Perform the OCR process for an image steam.
string ocrText = processor.PerformOCR(stream, @"tessdata/");

}
			
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/OCR/.NET/Perform-OCR-on-image-file).

## OCR an Image to PDF

You can perform OCR on an image and convert it to a searchable PDF document. It is also possible to set PdfConformanceLevel to the output PDF document using OCRSettings. 

N> This PDF conformance option only applies for image OCR to PDF documents.

The following code sample illustrates how to OCR an image to a PDF document:

{% tabs %} 

{% highlight c# tabtitle="ASP.NET Core" %}

//Initialize the OCR processor by providing the path of the tesseract binaries
using (OCRProcessor processor = new OCRProcessor())
{     
//loading the input image
FileStream imageStream = new FileStream(@"Input.png ", FileMode.Open);
Bitmap image = new Bitmap(imageStream);

//Set OCR language to process
processor.Settings.Language = Languages.English;

// Sets Unicode font to preserve the Unicode characters in a PDF document
FileStream fontStream = new FileStream(@"ARIALUNI.ttf", FileMode.Open);

processor.UnicodeFont = new PdfTrueTypeFont(fontStream, true, PdfFontStyle.Regular, 10);

// Set the PDF conformance level
                
processor.Settings.Conformance = PdfConformanceLevel.Pdf_A1B;

//Process OCR by providing the bitmap image.  
PdfDocument document = processor.PerformOCR(image);

MemoryStream stream = new MemoryStream();

//Save the document into stream.
document.Save(stream);
document.Close(true);

}

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/OCR/.NET/Perform-OCR-an-image-and-convert-it-to-a-PDF-document).

## Temporary folder

When performing OCR with an existing scanned PDF document, the OCR Processor will create temporary files images and temporary files in a temporary folder. The files will be deleted after the OCR process is completed.

By default, the system temporary folder will be used for the process. The temporary folder path can be changed by using the [TempFolder](https://help.syncfusion.com/cr/file-formats/Syncfusion.OCRProcessor.OCRSettings.html#Syncfusion_OCRProcessor_OCRSettings_TempFolder) property available in the [OCRSettings](https://help.syncfusion.com/cr/file-formats/Syncfusion.OCRProcessor.OCRSettings.html) Instance. Refer to the following code snippet.

{% tabs %} 

{% highlight c# tabtitle="ASP.NET Core" %}


//Initialize the OCR processor by providing the path of the tesseract 
using (OCRProcessor processor = new OCRProcessor(@"TesseractBinaries/Windows"))
{
//Load a PDF document
FileStream stream = new FileStream(@"Input.pdf", FileMode.Open);

PdfLoadedDocument document = new PdfLoadedDocument(stream);

//Set OCR language to process
processor.Settings.Language = Languages.English;

//Set custom temp file path location
processor.Settings.TempFolder = "D:/Temp/";
//Process OCR by providing the PDF document, data dictionary, and language
processor.PerformOCR(document, @"tessdata/");

//Creating the stream object 
MemoryStream outputStream = new MemoryStream();

//Save the document into stream.
document.Save(outputStream); 

//If the position is not set to '0' then the PDF will be empty. 
outputStream.Position = 0;
 
//Close the documents. 
document.Close(true); 

//Defining the ContentType for pdf file.
string contentType = "application/pdf"; 

//Define the file name.
string fileName = "Output.pdf"; 

//Creates a FileContentResult object by using the file contents, content type, and file name.
return File(outputStream, contentType, fileName);
}


{% endhighlight %}

{% endtabs %} 

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/OCR/.NET/Set-temp-folder-while-performing-OCR).

## Performing OCR with Azure Vision
The OCR processor supports external engines to process the OCR on Image and PDF documents. Perform the OCR using external OCR engines such as Azure Computer Vision and more. 
Using the IOcrEngine interface, create an external OCR engine. Refer to the following code sample to perform OCR with Azure computer vision.

{% tabs %} 

{% highlight c# tabtitle="ASP.NET Core" %}


//Initialize the OCR processor.
using (OCRProcessor processor = new OCRProcessor())
{
//Load a PDF document.
FileStream stream = new FileStream(@"Input.pdf", FileMode.Open);
PdfLoadedDocument lDoc = new PdfLoadedDocument(stream);

//Set the OCR language.
processor.Settings.Language = Languages.English;

//Initialize the Azure vision external OCR engine.
IOcrEngine azureOcrEngine = new AzureExternalOcrEngine();

processor.ExternalEngine = azureOcrEngine;

//Perform OCR with an input document.
processor.PerformOCR(lDoc);

FileStream outputStream = new FileStream(@"Output.pdf", FileMode.CreateNew);

//Save the document into the stream.
lDoc.Save(outputStream);

//If the position is not set to '0,' a PDF will be empty. 
outputStream.Position = 0;

//Close the document. 
lDoc.Close(true);
outputStream.Close();
}


{% endhighlight %}

{% endtabs %} 

Create a new class and implement the IOcrEngine interface. Get the image stream in the PerformOCR method and process the image stream with an external OCR engine and return the OCRLayoutResult for the image. 
Refer to the following code sample to perform OCR with Azure computer vision. 
N> Provide a valid subscription key and endpoint to work with Azure computer vision. 

{% tabs %} 

{% highlight c# tabtitle="ASP.NET Core" %}


class AzureExternalOcrEngine : IOcrEngine
{
private string subscriptionKey = "SubscriptionKey";
private string endpoint = "endpoint";

public OCRLayoutResult PerformOCR(Stream imgStream)
{
ComputerVisionClient client = Authenticate();
ReadResult azureOcrResult = ReadFileUrl(client, imgStream).Result;


OCRLayoutResult result = ConvertAzureVisionOcrToOcrLayoutResult(azureOcrResult);

return result;
}

public ComputerVisionClient Authenticate()
{
ComputerVisionClient client = new ComputerVisionClient(new ApiKeyServiceClientCredentials(subscriptionKey))
{
Endpoint = endpoint
};
return client;
}

public async Task<ReadResult> ReadFileUrl(ComputerVisionClient client, Stream stream)
{
stream.Position = 0;
var textHeaders = await client.ReadInStreamAsync(stream);
string operationLocation = textHeaders.OperationLocation;

const int numberOfCharsInOperationId = 36;

string operationId = operationLocation.Substring(operationLocation.Length - numberOfCharsInOperationId);
//Extract the text.
ReadOperationResult results;
do
{
results = await client.GetReadResultAsync(Guid.Parse(operationId));
}
while ((results.Status == OperationStatusCodes.Running || results.Status == OperationStatusCodes.NotStarted));

ReadResult azureOcrResult = results.AnalyzeResult.ReadResults[0];

return azureOcrResult;
}

private OCRLayoutResult ConvertAzureVisionOcrToOcrLayoutResult(ReadResult azureVisionOcr)
{
Syncfusion.OCRProcessor.Line ocrLine;
Syncfusion.OCRProcessor.Word ocrWord;

OCRLayoutResult ocrlayoutResult = new OCRLayoutResult();

ocrlayoutResult.ImageWidth = (float)azureVisionOcr.Width;
ocrlayoutResult.ImageHeight = (float)azureVisionOcr.Height;

//Page
Syncfusion.OCRProcessor.Page normalPage = new Syncfusion.OCRProcessor.Page();

//Lines
foreach (var line in azureVisionOcr.Lines)
{
ocrLine = new Syncfusion.OCRProcessor.Line();

//Word
foreach (var word in line.Words)
{
ocrWord = new Syncfusion.OCRProcessor.Word();

Rectangle rect = GetAzureVisionBounds(word.BoundingBox);

ocrWord.Text = word.Text;
ocrWord.Rectangle = rect;

ocrLine.Add(ocrWord);
}
normalPage.Add(ocrLine);
}

ocrlayoutResult.Add(normalPage);

return ocrlayoutResult;
}

private Rectangle GetAzureVisionBounds(IList<double?> bbox)
{
Rectangle rect = Rectangle.Empty;
PointF[] pointCollection = new PointF[bbox.Count / 2];
int count = 0;
for (int i = 0; i < bbox.Count; i = i + 2)
{
pointCollection[count] = new PointF((float)bbox[i], (float)bbox[i + 1]);
count++;
}
float xMin = 0;
float yMin = 0;
float xMax = 0;
float yMax = 0;
bool first = true;

foreach (PointF point in pointCollection)
{
if (first)
{
xMin = point.X;
yMin = point.Y;
first = false;
}
else
{
if (point.X < xMin)
xMin = point.X;
else if (point.X > xMax)
xMax = point.X;
if (point.Y < yMin)
yMin = point.Y;
else if (point.Y > yMax)
yMax = point.Y;
}
}

int x = Convert.ToInt32(xMin);
int y = Convert.ToInt32(yMin);
int w = Convert.ToInt32(xMax);
int h = Convert.ToInt32(yMax);

return new Rectangle(x, y, w, h);
}
}


{% endhighlight %}

{% endtabs %} 

## Performing OCR with AWS Textract
The OCR processor supports external engines to process the OCR on Image and PDF documents. Perform the OCR using external OCR engines such as AWS Textract and more. 
Using the IOcrEngine interface, create an external OCR engine. Refer to the following code sample to perform OCR with AWS Textract.
{% tabs %} 

{% highlight c# tabtitle="ASP.NET Core" %}

//Initialize the OCR processor.
using (OCRProcessor processor = new OCRProcessor())
{
//Load a PDF document.
FileStream stream = new FileStream(@"Input.pdf", FileMode.Open);
PdfLoadedDocument lDoc = new PdfLoadedDocument(stream);

//Set the OCR language.
processor.Settings.Language = Languages.English;

//Initialize the  AWS Textract external OCR engine.
IOcrEngine azureOcrEngine = new AWSExternalOcrEngine();

processor.ExternalEngine = azureOcrEngine;

//Perform OCR with input document.
string text = processor.PerformOCR(lDoc);

FileStream outputStream = new FileStream(@"Output.pdf", FileMode.Create);

//Save the document into stream.
lDoc.Save(outputStream);

//If the position is not set to '0' then the PDF will be empty.
outputStream.Position = 0;

//Close the document.
lDoc.Close();
stream.Dispose();
outputStream.Dispose();
}


{% endhighlight %}

{% endtabs %}
Create a new class and implement the IOcrEngine interface. Get the image stream in the PerformOCR method and process the image stream with an external OCR engine and return the OCRLayoutResult for the image.
Refer to the following code sample to perform OCR with AWS Textract.
N> Provide a valid Access key and Secret Access Key to work with AWS Textract.

{% tabs %} 

{% highlight c# tabtitle="ASP.NET Core" %}

class AWSExternalOcrEngine : IOcrEngine
{
private string awsAccessKeyId = "Access key ID";
private string awsSecretAccessKey = "Secret access key";
private float imageHeight;
private float imageWidth;
public OCRLayoutResult PerformOCR(Stream stream)
{
AmazonTextractClient clientText = Authenticate();

DetectDocumentTextResponse textResponse = GetAWSTextractResult(clientText, stream).Result;
            
OCRLayoutResult oCRLayoutResult = ConvertAWSTextractResultToOcrLayoutResult(textResponse);
return oCRLayoutResult;
}

public AmazonTextractClient Authenticate()
{
AmazonTextractClient client = new AmazonTextractClient(awsAccessKeyId, awsSecretAccessKey, RegionEndpoint.USEast1);
return client;
}
        
public async Task<DetectDocumentTextResponse> GetAWSTextractResult(AmazonTextractClient client, Stream stream)
{
stream.Position = 0;
MemoryStream memoryStream = new MemoryStream();
stream.CopyTo(memoryStream);
PdfBitmap bitmap = new PdfBitmap(memoryStream);
imageHeight = bitmap.Height;
imageWidth = bitmap.Width;

DetectDocumentTextResponse response = await client.DetectDocumentTextAsync(new DetectDocumentTextRequest
{
Document = new Document
{
Bytes = memoryStream
}
});
return response;
}
        
public OCRLayoutResult ConvertAWSTextractResultToOcrLayoutResult(DetectDocumentTextResponse textResponse)
{
OCRLayoutResult layoutResult = new OCRLayoutResult();
Syncfusion.OCRProcessor.Page ocrPage = new Page();
Syncfusion.OCRProcessor.Line ocrLine;
Syncfusion.OCRProcessor.Word ocrWord;
layoutResult.ImageHeight = imageHeight;
layoutResult.ImageWidth = imageWidth;
foreach (var page in textResponse.Blocks)
{                   
ocrLine = new Line();
if (page.BlockType == "WORD")
{
ocrWord = new Word();
ocrWord.Text = page.Text;
                    
float left = page.Geometry.BoundingBox.Left;
float top = page.Geometry.BoundingBox.Top;
float width = page.Geometry.BoundingBox.Width;
float height = page.Geometry.BoundingBox.Height;
Rectangle rect = GetBoundingBox(left,top,width,height);
ocrWord.Rectangle = rect;
ocrLine.Add(ocrWord);
ocrPage.Add(ocrLine);
}               
}
layoutResult.Add(ocrPage);
return layoutResult;
}
public Rectangle GetBoundingBox(float left, float top, float width, float height)
{
int x = Convert.ToInt32(left * imageWidth);
int y = Convert.ToInt32(top * imageHeight);
int bboxWidth = Convert.ToInt32((width * imageWidth) + x);
int bboxHeight = Convert.ToInt32((height * imageHeight) + y);
Rectangle rect = new Rectangle(x,y, bboxWidth, bboxHeight);
return rect;
}
}


{% endhighlight %}

{% endtabs %} 

## Troubleshooting

<table>
<th style="font-size:14px">Exception</th>
<th style="font-size:14px">Tesseract has not been initialized exception.</th>
<tr>
<th style="font-size:14px">Reason
</th>
<td>The exception may occur if the tesseract binaries and tessdata files are not available on the provided path. 
</td>
</tr>
<tr>
<th style="font-size:14px">Solution</th>
<td>
Set the proper tesseract binaries and tessdata folder with all files and inner folders.
<br/><br/>
The tessdata folder name is case sensitive and the name should not the change. 
</td>
</tr>
</table>

<table>
<th style="font-size:14px">Exception</th>
<th style="font-size:14px">Exception has been thrown by the target of an invocation.</th>
<tr>
<th style="font-size:14px">Reason
</th>
<td>If the tesseract binaries are not in the required structure.  
</td>
</tr>
<tr>
<th style="font-size:14px">Solution</th>
<td>
To resolve this exception, ensure the tesseract binaries are in the following structure,
<br/><br/>
The tesseract binaries path is TesseractBinaries/Windows and the assemblies should be in below structure, 
<br/><br/>
1.<span style="color:gray;font-size:14px"><i>TesseractBinaries/Windows/x64/libletpt1753.dll,libSyncfusionTesseract.dll</i></span><br/>
2.<span style="color:gray;font-size:14px"><i>TesseractBinaries/Windows/x86/libletpt1753.dll,libSyncfusionTesseract.dll</i></span>
</td>
</tr>
</table>

<table>
<th style="font-size:14px">Exception</th>
<th style="font-size:14px">can't be opened because the identity of the developer cannot be confirmed.</th>
<tr>
<th style="font-size:14px">Reason
</th>
<td>This error may occur during the initial loading of OCR processor in Mac environments.   
</td>
</tr>
<tr>
<th style="font-size:14px">Solution</th>
<td>
To resolve this issue, refer this <a href="https://support.shippingeasy.com/hc/en-us/articles/211543683-What-is-the-error-identity-of-the-developer-cannot-be-confirmed-">link</a> for more details.

</td>
</tr>
</table>

<table>
<th style="font-size:14px">Exception</th>
<th style="font-size:14px">OCR processor doesn’t process languages other than English.</th>
<tr>
<th style="font-size:14px">Reason
</th>
<td>This issue may occur, if the input image has other languages and the language and tessdata is not available for that languages.    
</td>
</tr>
<tr>
<th style="font-size:14px">Solution</th>
<td>
Essential PDF supports all the languages supported by Tesseract engine in the OCR processor.
The dictionary packs for the languages can be downloaded from the following online location:<br/>
<a href="https://code.google.com/p/tesseract-ocr/downloads/list">https://code.google.com/p/tesseract-ocr/downloads/list</a>
<br/><br/>
It is also mandatory to change the corresponding language code in the OCRProcessor.Settings.Language property. <br/>
For example, to perform optical character recognition in German, the property should be set as <br/>
"processor.Settings.Language = "deu";"
</td>
</tr>
</table>



