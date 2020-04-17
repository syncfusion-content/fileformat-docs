---
title: OCR processor for .NET Core with tesseract | Syncfusion
description: This section explains how to process OCR for the existing PDF documents and Images with different version tesseract.
platform: file-formats
control: PDF
documentation: UG
---

# Working with Optical Character Recognition (OCR)

Essential PDF provides support for Optical Character Recognition with the help of Google’s Tesseract Optical Character Recognition engine.

## Prerequisites

To use the OCR feature in the .NET core application, the following assemblies or NuGet packages should be added as a reference to the project.

### Assemblies

   *	Syncfusion.Compression.Portable.dll
   *	Syncfusion.Pdf.Portable.dll
   *	Syncfusion.PdfImaging.Portable.dll
   *    Syncfusion.OCRProcessor.Portable.dll
   *	[System.Drawing.Common](https://www.nuget.org/packages/System.Drawing.Common/4.5.0) package (v 4.5.0 or above)
   
### NuGet

   *	[Syncfusion.PDF.OCR.Net.Core](https://www.nuget.org/packages/Syncfusion.PDF.OCR.Net.Core)


You can get the TesseractBinaries and tessdata from the OCR Processor download or from the Syncfusion.PDF.OCR.Net.Core NuGet package installed location. Please refer to the following example folder path.


<b>TesseractBinaries:</b>

<span style="color:gray;font-size:14px"><i>syncfusionocrprocessor\Tesseractbinaries_core</i></span> (or)

<span style="color:gray;font-size:14px"><i>C:\Users\xxx\.nuget\packages\Syncfusion.PDF.OCR.Net.Core\XX.X.X.XX\lib\TesseractBinaries\</i></span>


<b>tessdata:</b>

<span style="color:gray;font-size:14px"><i>syncfusionocrprocessor\tessdata</i></span> (or)

<span style="color:gray;font-size:14px"><i>C:\Users\xxx\.nuget\packages\Syncfusion.PDF.OCR.Net.Core\XX.X.X.XX\lib\tessdata\</i></span>


N> The above folders can be copied from the build or NuGet to your project folder and it can be referred from the project folder. 

## Prerequisites for Windows 

*   Provide the TesseractBinaries windows folder path when creating a new OCR processor. Please refer to the following code snippet for windows.

{% tabs %}  

{% highlight ASP.NET Core %}


OCRProcessor processor = new OCRProcessor(@"TesseractBinaries\Windows");


{% endhighlight %}

{% endtabs %} 

*   Provide the tesseract language data folder path (tessdata) when performing the OCR to recognize different language images.

{% tabs %}  

{% highlight ASP.NET Core %}


processor.PerformOCR(lDoc, "tessdata\");


{% endhighlight %}

{% endtabs %} 

You can download the language packages from the following link

<a href="https://code.google.com/p/tesseract-ocr/downloads/list">https://code.google.com/p/tesseract-ocr/downloads/list</a>
        


## Prerequisites for Linux

*	We are using the “System.Drawing.Common” API in the OCR Processor. So, it is mandatory to install the “libgdiplus” and “libopenjb2-7” package. Please refer to the following commands to install the packages.

        1.sudo apt-get update
        2.sudo apt-get install libgdiplus
        3.sudo apt-get install y- libopenjb2-7
 
*	Provide the TesseractBinaries Linux folder path when creating a new OCR processor. Please refer to the following code snippet for Linux.

{% tabs %}  

{% highlight ASP.NET Core %}


OCRProcessor processor = new OCRProcessor(@"TesseractBinaries\Linux");


{% endhighlight %}

{% endtabs %} 

*	Provide the tesseract language data folder path (tessdata) when performing the OCR to recognize different language images.
              
{% tabs %}  

{% highlight ASP.NET Core %}


processor.PerformOCR(lDoc, "tessdata\");


{% endhighlight %}

{% endtabs %} 

You can download the language packages from the following link
        
<a href="https://code.google.com/p/tesseract-ocr/downloads/list">https://code.google.com/p/tesseract-ocr/downloads/list</a>


## Prerequisites for Mac


*	We are internally using the “System.Drawing.Common” package to process the image and perform the OCR in the OCR Processor. So, it is mandatory to install the “'libgdiplus”, and “tesseract” packages in the Mac machine where the OCR operations occur. Please refer to the following commands to install this package.

        1.brew install mono-libgdiplus
        2.brew install tesseract

*	Provide the TesseractBinaries Mac folder path when creating a new OCR processor. Please refer to the following code snippet for Mac.

{% tabs %}  

{% highlight ASP.NET Core %}


OCRProcessor processor = new OCRProcessor(@"TesseractBinaries\Mac");


{% endhighlight %}

{% endtabs %} 

*	Provide the tesseract language data folder path (tessdata) when performing the OCR to recognize different language images.

{% tabs %}  

{% highlight ASP.NET Core %}


processor.PerformOCR(lDoc, "tessdata\");


{% endhighlight %}

{% endtabs %} 

You can download the language packages from the following link
        
<a href="https://code.google.com/p/tesseract-ocr/downloads/list">https://code.google.com/p/tesseract-ocr/downloads/list</a>


## Performing OCR in Windows

To perform the OCR in the ASP.NET Core project in Windows, refer to the following code snippet,

{% tabs %}   

{% highlight ASP.NET Core %}


//Initialize the OCR processor with tesseract binaries folder path
using (OCRProcessor processor = new OCRProcessor(@"TesseractBinaries\Windows"))
{
//Load a PDF document
FileStream stream = new FileStream(@"Input.pdf", FileMode.Open);
PdfLoadedDocument document = new PdfLoadedDocument(stream);

//Set OCR language
processor.Settings.Language = Languages.English;

//Perform OCR with input document and tessdata (Language packs)
 processor.PerformOCR(document, @"tessdata\");

MemoryStream stream = new MemoryStream();

 //Save the document into stream.
 document.Save(stream); 

//If the position is not set to '0' then the PDF will be empty. 
stream.Position = 0;
 
//Close the document. 
document.Close(true); 

//Defining the ContentType for pdf file.
 string contentType = "application/pdf"; 

//Define the file name.
 string fileName = "Output.pdf"; 

//Creates a FileContentResult object by using the file contents, content type, and file name. 
return File(stream, contentType, fileName);
}


{% endhighlight %}

{% endtabs %} 

## Performing OCR in Linux

To perform the OCR in the ASP.NET Core project in Linux, refer to the following code snippet,

{% tabs %}   

{% highlight ASP.NET Core %}

//Initialize the OCR processor with tesseract binaries folder path
using (OCRProcessor processor = new OCRProcessor(@"TesseractBinaries\Linux"))
{
//Load a PDF document
FileStream stream = new FileStream(@"Input.pdf", FileMode.Open);
PdfLoadedDocument document = new PdfLoadedDocument(stream);

//Set OCR language
processor.Settings.Language = Languages.English;

//Perform OCR with input document and tessdata (Language packs)
 processor.PerformOCR(document, @"tessdata\");

MemoryStream stream = new MemoryStream();

 //Save the document into stream.
 document.Save(stream); 

//If the position is not set to '0' then the PDF will be empty. 
stream.Position = 0;
 
//Close the document. 
document.Close(true); 

//Defining the ContentType for pdf file.
 string contentType = "application/pdf"; 

//Define the file name.
 string fileName = "Output.pdf"; 

//Creates a FileContentResult object by using the file contents, content type, and file name. 
return File(stream, contentType, fileName);
}


{% endhighlight %}

{% endtabs %} 

## Performing OCR in Mac

To perform the OCR in the ASP.NET Core project in Mac, refer to the following code snippet,

{% tabs %}   

{% highlight ASP.NET Core %}


//Initialize the OCR processor with tesseract binaries folder path
using (OCRProcessor processor = new OCRProcessor(@"TesseractBinaries\Mac"))
{
//Load a PDF document
FileStream stream = new FileStream(@"Input.pdf", FileMode.Open);
PdfLoadedDocument document = new PdfLoadedDocument(stream);

//Set OCR language
processor.Settings.Language = Languages.English;

//Perform OCR with input document and tessdata (Language packs)
 processor.PerformOCR(document, @"tessdata\");

MemoryStream stream = new MemoryStream();

 //Save the document into stream.
 document.Save(stream); 

//If the position is not set to '0' then the PDF will be empty. 
stream.Position = 0;
 
//Close the document. 
document.Close(true); 

//Defining the ContentType for pdf file.
 string contentType = "application/pdf"; 

//Define the file name.
 string fileName = "Output.pdf"; 

//Creates a FileContentResult object by using the file contents, content type, and file name. 
return File(stream, contentType, fileName);
}


{% endhighlight %}

{% endtabs %} 

N> The [PerformOCR](https://help.syncfusion.com/cr/file-formats/Syncfusion.OCRProcessor.Base~Syncfusion.OCRProcessor.OCRProcessor~PerformOCR(PdfLoadedDocument,String).html) methods return only the text OCRed by [OCRProcessor](https://help.syncfusion.com/cr/file-formats/Syncfusion.OCRProcessor.Base~Syncfusion.OCRProcessor.OCRProcessor.html). Other existing text in the PDF page will not be returned in this method.

## Performing OCR for a region

You can perform OCR on particular region of the PDF page with help of the [PageRegion](https://help.syncfusion.com/cr/file-formats/Syncfusion.OCRProcessor.Base~Syncfusion.OCRProcessor.PageRegion.html) class. Refer to the following code snippet,

{% tabs %}   

{% highlight ASP.NET Core %}



//Initialize the OCR processor by providing the path of the tesseract 
using (OCRProcessor processor = new OCRProcessor(@"TesseractBinaries\Windows"))
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
processor.PerformOCR(document, @"tessdata\");

//Creating the stream object 
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

//Creates a FileContentResult object by using the file contents, content type, and file name. return File(stream, contentType, fileName);}



{% endhighlight %}

{% endtabs %} 


## Performing OCR with rotated pages

You can perform OCR on the rotated page of a PDF document. Refer to the following code snippet for the same.

{% tabs %} 

{% highlight ASP.NET Core %}



//Initialize the OCR processor by providing the path of tesseract 
using (OCRProcessor processor = new OCRProcessor(@"TesseractBinaries\Windows"))
{
//Load a PDF document
FileStream stream = new FileStream(@"Input.pdf", FileMode.Open);

PdfLoadedDocument document = new PdfLoadedDocument(stream);

//Set OCR language to process
processor.Settings.Language = Languages.English;

//Set the Page Segment Mode.
processor.Settings.PageSegment = PageSegMode.AutoOsd;

//Process OCR by providing the PDF document, data dictionary, and language
processor.PerformOCR(document, @"tessdata\");

//Creating the stream object 
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

//Creates a FileContentResult object by using the file contents, content type, and file name. return File(stream, contentType, fileName);
 }



{% endhighlight %}

{% endtabs %}  

## Performing OCR with Unicode characters 

You can perform OCR on Images with Unicode characters. To preserve the Unicode characters in the PDF document, use the UnicodeFont property. Refer to the following code snippet.

{% tabs %} 

{% highlight ASP.NET Core %}


//Initialize the OCR processor by providing the path of tesseract 
using (OCRProcessor processor = new OCRProcessor(@"TesseractBinaries\Windows"))
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
 processor.PerformOCR(document, @"tessdata\");


//Creating the stream object 
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

//Creates a FileContentResult object by using the file contents, content type, and file name. return File(stream, contentType, fileName);
}


{% endhighlight %}

{% endtabs %}  

 

## Layout result 

You can get the OCRed text and its bounds from an input PDF document by using the [OCRLayoutResult](https://help.syncfusion.com/cr/file-formats/Syncfusion.OCRProcessor.Base~Syncfusion.OCRProcessor.OCRLayoutResult.html) Class. Refer to the following code snippet. 
 
{% tabs %} 

{% highlight ASP.NET Core %}


//Initialize the OCR processor by providing the path of tesseract 
using (OCRProcessor processor = new OCRProcessor(@"TesseractBinaries\Windows"))
{
//Load a PDF document
FileStream stream = new FileStream(@"Input.pdf", FileMode.Open);

PdfLoadedDocument document = new PdfLoadedDocument(stream);

//Set OCR language to process
processor.Settings.Language = Languages.English;

//Process OCR by providing the PDF document, data dictionary, and language
processor.PerformOCR(lDoc, @"TessData\", out result); 
//Get OCRed line collection from first page 
OCRLineCollection lines = result.Pages[0].Lines;
//Get each OCRed line and its bounds 
 foreach(Line line in lines)
 { 
    string text = line.Text;
    RectangleF bounds = line.Rectangle;
 }
 
//Creating the stream object 
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

//Creates a FileContentResult object by using the file contents, content type, and file name. return File(stream, contentType, fileName);
}


{% endhighlight %}

{% endtabs %} 


## Performing OCR with image

You can perform OCR with images. Refer to the following code snippet.

{% tabs %} 

{% highlight ASP.NET Core %}


//Initialize the OCR processor by providing the path of the tesseract binaries

using (OCRProcessor processor = new OCRProcessor(@"TesseractBinaries\"))
{
//loading the input image
FileStream stream = new FileStream(@"Input.jpeg ", FileMode.Open);

Bitmap image = new Bitmap(stream);

//Set OCR language to process
processor.Settings.Language = Languages.English;

//Process OCR by providing the bitmap image, data dictionary, and language
string ocrText= processor.PerformOCR(image, @"tessdata\");

}

			
{% endhighlight %}

{% endtabs %}


## Temporary folder

When performing OCR with an existing scanned PDF document, the OCR Processor will create temporary files images and temporary files in a temporary folder. The files will be deleted after the OCR process is completed.

By default, the system temporary folder will be used for the process. The temporary folder path can be changed by using the [TempFolder](https://help.syncfusion.com/cr/file-formats/Syncfusion.OCRProcessor.Base~Syncfusion.OCRProcessor.OCRSettings~TempFolder.html) property available in the [OCRSettings](https://help.syncfusion.com/cr/file-formats/Syncfusion.OCRProcessor.Base~Syncfusion.OCRProcessor.OCRSettings.html) Instance. Refer to the following code snippet.

{% tabs %} 

{% highlight ASP.NET Core %}


//Initialize the OCR processor by providing the path of the tesseract 
using (OCRProcessor processor = new OCRProcessor(@"TesseractBinaries\Windows"))
{
//Load a PDF document
FileStream stream = new FileStream(@"Input.pdf", FileMode.Open);

PdfLoadedDocument document = new PdfLoadedDocument(stream);

//Set OCR language to process
processor.Settings.Language = Languages.English;

//Set custom temp file path location
processor.Settings.TempFolder = "D:/Temp/";
//Process OCR by providing the PDF document, data dictionary, and language
processor.PerformOCR(document, @"tessdata\");

//Creating the stream object 
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

//Creates a FileContentResult object by using the file contents, content type, and file name. return File(stream, contentType, fileName);
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
1.<span style="color:gray;font-size:14px"><i>TesseractBinaries\Windows\x64\libletpt1753.dll,libSyncfusionTesseract.dll</i></span><br/>
2.<span style="color:gray;font-size:14px"><i>TesseractBinaries\Windows\x86\libletpt1753.dll,libSyncfusionTesseract.dll</i></span>
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
Essential PDF supports all the languages supported by Tesseract engine in the OCR processor
The dictionary packs for the languages can be downloaded from the following online location:<br/>
<a href="https://code.google.com/p/tesseract-ocr/downloads/list">https://code.google.com/p/tesseract-ocr/downloads/list</a>
<br/><br/>
It is also mandatory to change the corresponding language code in the OCRProcessor.Settings.Language property. <br/>
For example, to perform optical character recognition in German, the property should be set as <<br/>
"processor.Settings.Language = "deu";"
</td>
</tr>
</table>



