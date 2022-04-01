---
title: OCR processor for .NET Framework with tesseract | Syncfusion
description: This section explains how to process OCR for the existing PDF documents and Images with different version tesseract.
platform: file-formats
control: PDF
documentation: UG
---

# Working with Optical Character Recognition (OCR)

Essential PDF provides support for Optical Character Recognition with the help of Google’s Tesseract Optical Character Recognition engine.

N>* Starting with v20.1.0.x, if you reference Syncfusion OCRProcessor assemblies from trial setup or from the NuGet feed, include a license key in your projects. Refer to [link](https://help.syncfusion.com/file-formats/licensing/licensing) to learn how to generate and register a Syncfusion license key in your application to use the components without trail message.

## Prerequisites and setting up the Tesseract Engine

* To use the OCR feature in your application, you need to add reference to the following set of assemblies.
1. Syncfusion.Compression.Base.dll
2. Syncfusion.Pdf.Base.dll
3. Syncfusion.OCRProcessor.Base.dll

* Place the SyncfusionTesseract.dll and liblept168.dll Tesseract assemblies in the local system and provide the assembly path to the OCR processor.

{% tabs %}  

{% highlight c# tabtitle="C#" %}



OCRProcessor processor = new OCRProcessor(@"TesseractBinaries\")



{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}


Dim processor As New OCRProcessor("TesseractBinaries\")



{% endhighlight %}

{% endtabs %}  

* Place the Tesseract language data {E.g eng.traineddata} in the local system and provide a path to the OCR processor 

{% tabs %}  

{% highlight c# tabtitle="C#" %}



OCRProcessor processor = new OCRProcessor(@"TesseractBinaries\");

processor.PerformOCR(lDoc, @"TessData\");



{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}


Dim processor As New OCRProcessor("TesseractBinaries\")

processor.PerformOCR(lDoc, "TessData\")



{% endhighlight %}

{% endtabs %}  

You can also download the language packages from below link

[https://github.com/tesseract-ocr/tessdata](https://github.com/tesseract-ocr/tessdata )

N> From 16.1.0.24 OCR is not a part of Essential Studio and is available as separate package (OCR Processor) under the Add-On section in the below link [https://www.syncfusion.com/downloads/latest-version](https://www.syncfusion.com/downloads/latest-version).

N> PDF supports OCR only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

## Performing OCR for an entire document

You can perform OCR on PDF document with the help of [OCRProcessor](https://help.syncfusion.com/cr/file-formats/Syncfusion.OCRProcessor.OCRProcessor.html) Class. Refer the below code snippet for the same.

{% tabs %}   

{% highlight c# tabtitle="C#" %}


//Initialize the OCR processor by providing the path of tesseract binaries(SyncfusionTesseract.dll and liblept168.dll)

using (OCRProcessor processor = new OCRProcessor(@"TesseractBinaries\"))

{

//Load a PDF document

PdfLoadedDocument lDoc = new PdfLoadedDocument("Input.pdf");

//Set OCR language to process

processor.Settings.Language = Languages.English;

//Process OCR by providing the PDF document and Tesseract data

processor.PerformOCR(lDoc, @"TessData\");

//Save the OCR processed PDF document in the disk

lDoc.Save("Sample.pdf");

lDoc.Close(true);

}



{% endhighlight %}



{% highlight vb.net tabtitle="VB.NET" %}




'Initialize the OCR processor by providing the path of tesseract binaries(SyncfusionTesseract.dll and liblept168.dll)

Using processor As New OCRProcessor("TesseractBinaries\")

'Load a PDF document

Dim lDoc As New PdfLoadedDocument("Input.pdf")

'Set OCR language to process

processor.Settings.Language = Languages.English

'Process OCR by providing the PDF document and Tesseract data

processor.PerformOCR(lDoc, "TessData\")

'Save the OCR processed PDF document in the disk

lDoc.Save("Sample.pdf")

lDoc.Close(True)

End Using



{% endhighlight %}

{% endtabs %} 

N> The PerformOCR method returns only the text OCRed by OCRProcessor. Other existing text in the PDF page won’t be returned in this method. Please check [text extraction](/file-formats/pdf/Working-with-Text-Extraction) feature for this.

## Performing OCR with tesseract version 3.05

You can perform OCR using the tesseract version 3.05. The [TesseractVersion](https://help.syncfusion.com/cr/file-formats/Syncfusion.OCRProcessor.OCRSettings.html#Syncfusion_OCRProcessor_OCRSettings_TesseractVersion) property is used to switch the tesseract version between 3.02 and 3.05. By default, OCR works with tesseract version 3.02.
 
You must use the pre built Syncfusion tesseract version 3.05 in the sample to run the OCR properly. The tesseract binaries are shipping with Syncfusion NuGet package, use the following link to download the NuGet package.

[https://www.nuget.org/packages/Syncfusion.OCRProcessor.Base](https://www.nuget.org/packages/Syncfusion.OCRProcessor.Base)

The following sample code snippet demonstrates the OCR processor with Tesseract3.05 for PDF documents.
 
{% tabs %} 

{% highlight c# tabtitle="C#" %}


using (OCRProcessor processor = new OCRProcessor(@"Tesseract3.05Binaries \")
            
{ 

//Load a PDF document 
 
PdfLoadedDocument lDoc = new PdfLoadedDocument("input.pdf"); 

//Set OCR language to process 

processor.Settings.Language = Languages.English;
 
//Set tesseract OCR Engine 
				
processor.Settings.TesseractVersion = TesseractVersion.Version3_05; 
 
//Process OCR by providing the PDF document and tesseract data, and enabling the isMemoryOptimized property
				 
processor.PerformOCR(lDoc, @"TessData\", true); 
 
//Save the OCR processed PDF document in the disk 
				
lDoc.Save("Sample.pdf"); 
               
lDoc.Close(true); 
				
} 


{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

Using processor As New OCRProcessor("Tesseract3.05Binaries\")

'Load a PDF document

Dim lDoc As New PdfLoadedDocument("Input.pdf")

'Set OCR language to process

processor.Settings.Language = Languages.English
            
'Set tesseract OCR engine

processor.Settings.TesseractVersion = TesseractVersion.Version3_05

'Process OCR by providing the PDF document and tesseract data, and enabling the isMemoryOptimized property

processor.PerformOCR(lDoc, "TessData\", True)

'Save the OCR processed PDF document in the disk

lDoc.Save("Sample.pdf")

lDoc.Close(True)

End Using
			
{% endhighlight %}

 {% endtabs %}
 
 
## Performing OCR with Tesseract Version 4.0

You can perform OCR using tesseract 4.0. The [TesseractVersion](https://help.syncfusion.com/cr/file-formats/Syncfusion.OCRProcessor.OCRSettings.html#Syncfusion_OCRProcessor_OCRSettings_TesseractVersion) property is used to switch the tesseract version. By default, OCR will be performed with tesseract version 3.02.

You must use the pre-built Syncfusion tesseract 4.0 binaries in the project to run the OCR properly. The tesseract binaries are shipping with the Syncfusion NuGet package, use the following link to download the NuGet package.


[https://www.nuget.org/packages/Syncfusion.PDF.OCR.WinForms](https://www.nuget.org/packages/Syncfusion.PDF.OCR.WinForms/)

The following code sample explains the OCR processor with Tesseract4.0 for PDF documents.
 
{% tabs %} 

{% highlight c# tabtitle="C#" %}


using (OCRProcessor processor = new OCRProcessor(@"Tesseract4.0Binaries\")

{

//Load a PDF document

PdfLoadedDocument lDoc = new PdfLoadedDocument("input.pdf");

//Set OCR language to process

processor.Settings.Language = Languages.English;

//Set tesseract OCR Engine 

processor.Settings.TesseractVersion = TesseractVersion.Version4_0;

//Process OCR by providing the PDF document and tesseract data, and enabling the isMemoryOptimized property

processor.PerformOCR(lDoc, @"TessData\", true);

//Save the OCR processed PDF document in the disk

lDoc.Save("Sample.pdf");

lDoc.Close(true);

}

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

Using processor As New OCRProcessor("Tesseract4.0Binaries\")

'Load a PDF document

Dim lDoc As New PdfLoadedDocument("Input.pdf")

'Set OCR language to process

processor.Settings.Language = Languages.English

'Set tesseract OCR engine

processor.Settings.TesseractVersion = TesseractVersion.Version4_0

'Process OCR by providing the PDF document and tesseract data, and enabling the isMemoryOptimized property

processor.PerformOCR(lDoc, "TessData\", True)

'Save the OCR processed PDF document in the disk

lDoc.Save("Sample.pdf")

lDoc.Close(True)

End Using

{% endhighlight %}

{% endtabs %}  


## Performing OCR for a region of the document

You can perform OCR on particular region or several regions of a PDF page with the help of [PageRegion](https://help.syncfusion.com/cr/file-formats/Syncfusion.OCRProcessor.PageRegion.html) class. Refer the below code snippet for the same.

{% tabs %} 

{% highlight c# tabtitle="C#" %}


//Initialize the OCR processor by providing the path of the tesseract binaries(SyncfusionTesseract.dll and liblept168.dll)

using (OCRProcessor processor = new OCRProcessor(@"TesseractBinaries\"))

{

//Load a PDF document

PdfLoadedDocument lDoc = new PdfLoadedDocument("Input.pdf");

//Set OCR language to process

processor.Settings.Language = Languages.English;

RectangleF rect = new RectangleF(0, 100, 950, 150);

//Assign rectangles to the page

List<PageRegion> pageRegions = new List<PageRegion>();

PageRegion region = new PageRegion();

region.PageIndex = 1;

region.PageRegions = new RectangleF[] { rect };

pageRegions.Add(region);

processor.Settings.Regions = pageRegions;

//Process OCR by providing the PDF document and Tesseract data

processor.PerformOCR(lDoc, @"TessData\");

//Save the OCR processed PDF document in the disk

lDoc.Save("Sample.pdf");

lDoc.Close(true);

}



{% endhighlight %}



{% highlight vb.net tabtitle="VB.NET" %}


'Initialize the OCR processor by providing the path of the tesseract binaries(SyncfusionTesseract.dll and liblept168.dll)

Using processor As New OCRProcessor("TesseractBinaries\")

'Load a PDF document

Dim lDoc As New PdfLoadedDocument("Input.pdf")

'Set OCR language to process

processor.Settings.Language = Languages.English

Dim rect As New RectangleF(0, 100, 950, 150)

'Assign rectangles to the page

Dim pageRegions As New List(Of PageRegion)()

Dim region As New PageRegion()

region.PageIndex = 1

region.PageRegions = New RectangleF() {rect}

pageRegions.Add(region)

processor.Settings.Regions = pageRegions

'Process OCR by providing the PDF document and Tesseract data

processor.PerformOCR(lDoc, "TessData\")

'Save the OCR processed PDF document in the disk

lDoc.Save("Sample.pdf")

lDoc.Close(True)



{% endhighlight %}

 {% endtabs %}  

## Performing OCR on image

You can perform OCR on an image also. Refer the below code snippets for the same.

{% tabs %} 

{% highlight c# tabtitle="C#" %}


//Initialize the OCR processor by providing the path of the tesseract binaries(SyncfusionTesseract.dll and liblept168.dll)

using (OCRProcessor processor = new OCRProcessor(@"TesseractBinaries\"))

{

//loading the input image

Bitmap image = new Bitmap("input.jpeg");

//Set OCR language to process

processor.Settings.Language = Languages.English;

//Process OCR by providing the bitmap image, data dictionary and language

string ocrText= processor.PerformOCR(image, @"TessData\");

}



{% endhighlight %}



{% highlight vb.net tabtitle="VB.NET" %}


'Initialize the OCR processor by providing the path of the tesseract binaries(SyncfusionTesseract.dll and liblept168.dll)

Using processor As New OCRProcessor("TesseractBinaries\")

'loading the input image

Dim image As New Bitmap("input.jpeg")

'Set OCR language to process

processor.Settings.Language = Languages.English

'Process OCR by providing the bitmap image, data dictionary and language

Dim ocrText As String = processor.PerformOCR(image, "TessData\")

End Using



{% endhighlight %}

 {% endtabs %}  

## Performing OCR for large PDF documents

You can optimize the memory to perform OCR for large PDF documents by enabling the isMemoryOptimized property in [PerformOCR](https://help.syncfusion.com/cr/file-formats/Syncfusion.OCRProcessor.OCRProcessor.html#Syncfusion_OCRProcessor_OCRProcessor_PerformOCR_Syncfusion_Pdf_Parsing_PdfLoadedDocument_System_String_System_Boolean_) method of [OCRProcessor](https://help.syncfusion.com/cr/file-formats/Syncfusion.OCRProcessor.OCRProcessor.html) class. Optimization will be effective only with Multithreading environment or PDF document with more images. This is demonstrated in the following code sample. 

{% tabs %} 

{% highlight c# tabtitle="C#" %}


//Initialize the OCR processor by providing the path of tesseract binaries(SyncfusionTesseract.dll and liblept168.dll)

using (OCRProcessor processor = new OCRProcessor(@"TesseractBinaries\"))

{

//Load a PDF document.

PdfLoadedDocument lDoc = new PdfLoadedDocument("Input.pdf");

//Set OCR language to process.

processor.Settings.Language = Languages.English;

//Process OCR by providing the PDF document, Tesseract data and enable isMemoryOptimized property

processor.PerformOCR(lDoc, @"TessData\",true);

//Save the OCR processed PDF document in the disk.

lDoc.Save("Sample.pdf");

lDoc.Close(true);

}


{% endhighlight %}


{% highlight vb.net tabtitle="VB.NET" %}


'Initialize the OCR processor by providing the path of tesseract binaries(SyncfusionTesseract.dll and liblept168.dll)

Using processor As New OCRProcessor("TesseractBinaries\")

'Load a PDF document.

Dim lDoc As New PdfLoadedDocument("Input.pdf")

'Set OCR language to process.

processor.Settings.Language = Languages.English

'Process OCR by providing the PDF document and Tesseract data enable isMemoryOptimized property.

processor.PerformOCR(lDoc, "TessData\", True)

'Save the OCR processed PDF document in the disk.

lDoc.Save("Sample.pdf")

lDoc.Close(True)

End Using



{% endhighlight %}

{% endtabs %}  


## Performing OCR on rotated page of PDF document

You can perform OCR on the rotated page of a PDF document. Refer to the following code snippet for the same. 


{% tabs %} 

{% highlight c# tabtitle="C#" %}


//Initialize the OCR processor by providing the path of tesseract binaries(SyncfusionTesseract.dll and liblept168.dll)

using (OCRProcessor processor = new OCRProcessor(@"TesseractBinaries\"))

{

//Load a PDF document

PdfLoadedDocument lDoc = new PdfLoadedDocument("Input.pdf");

//Set OCR language to process

processor.Settings.Language = Languages.English;

//Set OCR page auto detection rotation

processor.Settings.AutoDetectRotation = true;

//Process OCR by providing the PDF document

processor.PerformOCR(lDoc, @"TessData\");

//Save the OCR processed PDF document in the disk

lDoc.Save("Sample.pdf");

lDoc.Close(true);

}


{% endhighlight %}


{% highlight vb.net tabtitle="VB.NET" %}


'Initialize the OCR processor by providing the path of tesseract binaries(SyncfusionTesseract.dll and liblept168.dll)

Using processor As New OCRProcessor("TesseractBinaries\")

'Load a PDF document.

Dim lDoc As PdfLoadedDocument = New PdfLoadedDocument("Input.pdf")

'Set OCR language to process

processor.Settings.Language = Languages.English

'Set OCR page auto detection rotation

processor.Settings.AutoDetectRotation = true

'Process OCR by providing the PDF document

processor.PerformOCR(lDoc, "TessData\")

'Save the OCR processed PDF document in the disk

lDoc.Save("Sample.pdf")

lDoc.Close(true)

End Using



{% endhighlight %}

{% endtabs %}  

 

## Layout result from OCR

You can get the OCRed text and its bounds from a scanned PDF document by using the [OCRLayoutResult](https://help.syncfusion.com/cr/file-formats/Syncfusion.OCRProcessor.OCRLayoutResult.html) Class. Refer to the following code snippet. 
 
{% tabs %} 

{% highlight c# tabtitle="C#" %}

//Initialize the OCR processor by providing the path of tesseract binaries (SyncfusionTesseract.dll and liblept168.dll)

using (OCRProcessor processor = new OCRProcessor(@"TesseractBinaries\"))

{

//Load a PDF document

PdfLoadedDocument lDoc = new PdfLoadedDocument("Input.pdf");

//Set OCR language to process

processor.Settings.Language = Languages.English;

//Initializes OCR layout result

OCRLayoutResult result;

//Process OCR by providing the PDF document, Tesseract data, and layout result

processor.PerformOCR(lDoc, @"TessData\", out result);

//Get OCRed line collection from first page

OCRLineCollection lines = result.Pages[0].Lines;

//Get each OCRed line and its bounds

foreach(Line line in lines)
{
    string text = line.Text;

    RectangleF bounds = line.Rectangle;
}

//Save the OCR processed PDF document in the disk

lDoc.Save("Sample.pdf");

//Close the document

lDoc.Close(true);

}

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Initialize the OCR processor by providing the path of tesseract binaries (SyncfusionTesseract.dll and liblept168.dll)

Using processor As New OCRProcessor("TesseractBinaries\")

'Load a PDF document

Dim lDoc As New PdfLoadedDocument("Input.pdf")

'Set OCR language to process

processor.Settings.Language = Languages.English

'Initializes OCR layout result

Dim result As OCRLayoutResult

'Process OCR by providing the PDF document, Tesseract data, and layout result

processor.PerformOCR(lDoc, "TessData\", result)

'Get OCRed line collection from first page

Dim lines As OCRLineCollection = result.Pages(0).Lines

'Get each OCRed line and its bounds

For Each line As Line In lines

    Dim text As String = line.Text

    Dim bounds As RectangleF = line.Rectangle

Next

'Save the OCR processed PDF document in the disk

lDoc.Save("Sample.pdf")

'Close the document

lDoc.Close(True)

End Using

{% endhighlight %}

{% endtabs %} 

## Native call

Enable native call will not launch any temporary process for OCR processing, instead it will invoke the native calls.

### Tesseract 3.02

Tesseract 3.02 supports only 32-bit version. By default, this property will be disabled.

N> Enable native call will not work in 64-bit in Tesseract 3.02 version. Instead a temporary process will be launched for OCR processing.

The following sample code snippet demonstrates the OCR processor with native call support of tesseract 3.02.

{% tabs %} 

{% highlight c# tabtitle="C#" %}


using (OCRProcessor processor = new OCRProcessor(@"Tesseract3.02Binaries\")
            
{ 

//Load a PDF document 
 
PdfLoadedDocument lDoc = new PdfLoadedDocument("input.pdf"); 

//Set OCR language to process 

processor.Settings.Language = Languages.English;
 
//Set tesseract OCR Engine 
				
processor.Settings.TesseractVersion = TesseractVersion.Version3_02; 
 
//Process OCR by providing the PDF document and tesseract data, and enabling the isMemoryOptimized property
				 
processor.PerformOCR(lDoc, @"TessData\", true); 
 
//Save the OCR processed PDF document in the disk 
				
lDoc.Save("Sample.pdf"); 
               
lDoc.Close(true); 
				
} 


{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

Using processor As New OCRProcessor("Tesseract3.02Binaries\")

'Load a PDF document

Dim lDoc As New PdfLoadedDocument("Input.pdf")

'Set OCR language to process

processor.Settings.Language = Languages.English
            
'Set tesseract OCR engine

processor.Settings.TesseractVersion = TesseractVersion.Version3_02

'Process OCR by providing the PDF document and tesseract data, and enabling the isMemoryOptimized property

processor.PerformOCR(lDoc, "TessData\", True)

'Save the OCR processed PDF document in the disk

lDoc.Save("Sample.pdf")

lDoc.Close(True)

End Using
			
{% endhighlight %}

{% endtabs %}

### Tesseract 3.05

Tesseract 3.05 supports the native call for both x86 and x64 architectures.By default, the x86 tesseract binaries are available with NuGet package or the tesseract installer. 

You can download the x64 supporting tesseract binaries from the following link.

[Tesseract 64-bit binaries](http://www.syncfusion.com/downloads/support/directtrac/general/ze/Tesseract3.05_x641904984914)

N> This 64-bit binaries are required only when the native call property is enabled.
N> Make sure to provide the 64-bit binaries path while using in the 64-bit environment.

The following sample code snippet demonstrates the OCR processor with native call support of tesseract 3.05.

{% tabs %} 

{% highlight c# tabtitle="C#" %}


using (OCRProcessor processor = new OCRProcessor(@" Tesseract3.05Binaries \")
		   
{ 
			
//Load a PDF document 
 
PdfLoadedDocument lDoc = new PdfLoadedDocument("input.pdf"); 
 
//Set OCR language to process
			 
processor.Settings.Language = Languages.English;  

//Set tesseract OCR engine 
			  
processor.Settings.TesseractVersion = TesseractVersion.Version3_05; 
         
//Set enable native call
		
processor.Settings.EnableNativeCall = true;

//Process OCR by providing the PDF document and tesseract data, and enabling the isMemoryOptimized property
			  
processor.PerformOCR(lDoc, @"TessData\", true); 
 
//Save the OCR processed PDF document in the disk 
				
lDoc.Save("Sample.pdf"); 

lDoc.Close(true); 

} 


{% endhighlight %}


{% highlight vb.net tabtitle="VB.NET" %}


Using processor As New OCRProcessor("Tesseract3.05Binaries\")

'Load a PDF document

Dim lDoc As New PdfLoadedDocument("input.pdf")

'Set OCR language to process

processor.Settings.Language = Languages.English
           
'Set tesseract OCR engine

processor.Settings.TesseractVersion = TesseractVersion.Version3_05

'Set enable native call

processor.Settings.EnableNativeCall = True

'Process OCR by providing the PDF document and tesseract data, and enabling the isMemoryOptimized property

processor.PerformOCR(lDoc,"TessData\", True)

'Save the OCR processed PDF document in the disk

lDoc.Save("Sample.pdf")

lDoc.Close(True)
			
End Using



{% endhighlight %}

{% endtabs %}  

## Customizing temp folder

While performing OCR on an existing scanned PDF document, the OCR Processor will create temporary files (.temp, .tiff, .txt) and the files are deleted after the process is completed. You can change this temporary files folder location using the [TempFolder](https://help.syncfusion.com/cr/file-formats/Syncfusion.OCRProcessor.OCRSettings.html#Syncfusion_OCRProcessor_OCRSettings_TempFolder) property available in the [OCRSettings](https://help.syncfusion.com/cr/file-formats/Syncfusion.OCRProcessor.OCRSettings.html) Instance. Refer to the following code snippet.

{% tabs %}  

{% highlight c# tabtitle="C#" %}

//Initialize the OCR processor by providing the path of tesseract binaries (SyncfusionTesseract.dll and liblept168.dll)

using (OCRProcessor processor = new OCRProcessor(@"TesseractBinaries\"))

{
    
//Load a PDF document

PdfLoadedDocument lDoc = new PdfLoadedDocument("Input.pdf");

//Set OCR language to process	

processor.Settings.Language = Languages.English;

//Set custom temp file path location

processor.Settings.TempFolder = "D:/Temp/";

//Process OCR by providing the PDF document and Tesseract data

processor.PerformOCR(lDoc, @"TessData\");

//Save the OCR processed PDF document in the disk

lDoc.Save("Sample.pdf");

//Close the document

lDoc.Close(true);

}

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Initialize the OCR processor by providing the path of tesseract binaries (SyncfusionTesseract.dll and liblept168.dll)

Using processor As New OCRProcessor("TesseractBinaries\")

'Load a PDF document

Dim lDoc As New PdfLoadedDocument("Input.pdf")

'Set OCR language to process

processor.Settings.Language = Languages.English

'Set custom temp file path location

processor.Settings.TempFolder = "D:/Temp/"

'Process OCR by providing the PDF document and Tesseract data

processor.PerformOCR(lDoc, "TessData\")

'Save the OCR processed PDF document in the disk

lDoc.Save("Sample.pdf")

'Close the document

lDoc.Close(True)

End Using

{% endhighlight %}

{% endtabs %} 



## Performing OCR with different Page Segmentation Mode

You can perform OCR with various page segmentation mode. The PageSegment property is used to set the page segmentation mode. By default, OCR works with the “Auto” page segmentation mode. Kindly refer to the following code sample.
 
{% tabs %} 

{% highlight c# tabtitle="C#" %}


using (OCRProcessor processor = new OCRProcessor(@"Tesseract4.0Binaries\")

{

//Load a PDF document

PdfLoadedDocument lDoc = new PdfLoadedDocument("input.pdf");

//Set OCR language to process

processor.Settings.Language = Languages.English;

//Set tesseract OCR Engine

processor.Settings.TesseractVersion = TesseractVersion.Version4_0;

////Set OCR Page segment mode to process

processor.Settings.PageSegment = PageSegmentMode.AutoOsd;

//Process OCR by providing the PDF document and tesseract data, and enabling the isMemoryOptimized property

processor.PerformOCR(lDoc, @"TessData\", true);

//Save the OCR processed PDF document in the disk

lDoc.Save("Sample.pdf");

lDoc.Close(true);

}


{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

VB

Using processor As New OCRProcessor("Tesseract4.0Binaries\")

'Load a PDF document

Dim lDoc As New PdfLoadedDocument("Input.pdf")

'Set OCR language to process

processor.Settings.Language = Languages.English

'Set tesseract OCR engine

processor.Settings.TesseractVersion = TesseractVersion.Version4_0

'Set OCR page segment mode to process

 processor.Settings.PageSegment = PageSegmentMode.AutoOsd

'Process OCR by providing the PDF document and tesseract data, and enabling the isMemoryOptimized property

processor.PerformOCR(lDoc, "TessData\", True)

'Save the OCR processed PDF document in the disk

lDoc.Save("Sample.pdf")

lDoc.Close(True)

End Using


{% endhighlight %}

{% endtabs %} 

N> The page segmentation mode is supported only in the Tesseract version 4.0 and above.

## Performing OCR with different OCR Engine Mode

You can perform OCR with various OCR Engine Mode. The OCREngineMode property is used to set the OCR Engine modes. By default, OCR works with OCR Engine mode “Default”.

This is explained in the following code sample
 
{% tabs %} 

{% highlight c# tabtitle="C#" %}


using (OCRProcessor processor = new OCRProcessor(@"Tesseract4.0Binaries\")

{

//Load a PDF document

PdfLoadedDocument lDoc = new PdfLoadedDocument("input.pdf");

//Set OCR language to process

processor.Settings.Language = Languages.English;

//Set tesseract OCR Engine

processor.Settings.TesseractVersion = TesseractVersion.Version4_0;

//Set OCR engine mode to process
processor.Settings.OCREngineMode = OCREngineMode.LSTMOnly;

//Process OCR by providing the PDF document and tesseract data, and enabling the isMemoryOptimized property

processor.PerformOCR(lDoc, @"TessData\", true);

//Save the OCR processed PDF document in the disk

lDoc.Save("Sample.pdf");

lDoc.Close(true);

}


{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

VB

Using processor As New OCRProcessor("Tesseract3.05Binaries\")

'Load a PDF document

Dim lDoc As New PdfLoadedDocument("Input.pdf")

'Set OCR language to process

processor.Settings.Language = Languages.English

'Set tesseract OCR engine

processor.Settings.TesseractVersion = TesseractVersion.Version4_0

'Set OCR engine mode to process

processor.Settings.OCREngineMode = OCREngineMode.LSTMOnly

'Process OCR by providing the PDF document and tesseract data, and enabling the isMemoryOptimized property

processor.PerformOCR(lDoc, "TessData\", True)

'Save the OCR processed PDF document in the disk

lDoc.Save("Sample.pdf")

lDoc.Close(True)

End Using

{% endhighlight %}

{% endtabs %} 

N> The OCR Engine Mode is supported only in the Tesseract version 4.0 and above.


## Best Practices

**You can improve the accuracy of the OCR process by choosing the correct compression method when converting the scanned paper to a TIFF image and then to a PDF document.**

* Use (zip) lossless compression for color or gray-scale images.
* Use CCITT Group 4 or JBIG2 (lossless) compression for monochrome images. This ensures that optical character recognition works on the highest-quality image, thereby improving the OCR accuracy. This is especially useful in low-resolution scans.
* In addition, rotated images and skewed images can also affect the accuracy and readability of the OCR process.

**Tesseract works best with text when at least 300 dots per inch (DPI) are used, so it is beneficial to resize images.**

For more details regarding quality improvement, refer to the following link:

[https://github.com/tesseract-ocr/tesseract/wiki/ImproveQuality](https://github.com/tesseract-ocr/tesseract/wiki/ImproveQuality )

**You can set the different performance level to the OCRProcessor using [Performance](https://help.syncfusion.com/cr/file-formats/Syncfusion.OCRProcessor.Performance.html) enumeration.**

* Rapid – high speed OCR performance and provide normal OCR accuracy
* Fast – provides moderate OCR processing speed and accuracy
* Slow – Slow OCR performance and provide best OCR accuracy.

Refer below code snippet to set the performance of the OCR.

{% tabs %}  

{% highlight c# tabtitle="C#" %}


OCRProcessor processor = new OCRProcessor(@"TesseractBinaries\")

//set the OCR performance

processor.Settings.Performance = Performance.Fast;



{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}


Dim processor As New OCRProcessor("TesseractBinaries\")

'Set the OCR performance

processor.Settings.Performance = Performance.Fast



{% endhighlight %}

{% endtabs %}  

## Troubleshooting

**Issue:** You can get the exception “Tesseract has not been initialized” while performing OCR process. 

**Solution 1:** To resolve this, make sure the path of the Tesseract binaries and Tesseract data are properly provided as shown below.

{% tabs %}  

{% highlight c# tabtitle="C#" %}


//'TesseractBinaries – path of the folder containing SyncfusionTesseract.dll and liblept168.dll

OCRProcessor processor = new OCRProcessor(@"TesseractBinaries\");

//TessData – path of the folder containing the language pack

processor.PerformOCR(lDoc, @"TessData\");



{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}


'TesseractBinaries – path of the folder containing SyncfusionTesseract.dll and liblept168.dll

Dim processor As New OCRProcessor("TesseractBinaries\")

'TessData – path of the folder containing the language pack

processor.PerformOCR(lDoc, "TessData\")



{% endhighlight %}

{% endtabs %}  

**Solution 2:** Make sure that your data file version is 3.02, since the OCR processor is built with Tesseract version 3.02.

**Issue:** OCR processor doesn’t process languages other than English.

**Solution:** Essential PDF supports all the languages supported by Tesseract engine.

The dictionary packs for the languages can be downloaded from the following online location:

[https://github.com/tesseract-ocr/tesseract/wiki/Data-Files#data-files-for-version-302](https://github.com/tesseract-ocr/tesseract/wiki/Data-Files#data-files-for-version-302)

It is also mandatory to change the corresponding language code in the OCRProcessor.Settings.Language property. For example, to perform optical character recognition in German, the property should be set as processor.Settings.Language = "deu";

The following link contains the complete set of languages supported by Tesseract and their language codes.

[https://github.com/tesseract-ocr/tesseract/blob/main/doc/tesseract.1.asc#languages](https://github.com/tesseract-ocr/tesseract/blob/main/doc/tesseract.1.asc#languages)

