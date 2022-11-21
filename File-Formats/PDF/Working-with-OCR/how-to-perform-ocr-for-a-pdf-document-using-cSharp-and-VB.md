---
title: How to perform OCR for a PDF document using C# and VB.NET | Syncfusion
description: This section explains how to perform OCR for a PDF document using syncfusion .NET OCR library in C# and VB.NET.
platform: file-formats
control: PDF
documentation: UG
---

# How to perform OCR for a PDF document using C# and VB.NET

Essential PDF provides support for Optical Character Recognition with the help of Google's [Tesseract](https://github.com/tesseract-ocr/tesseract) OCR engine. With a few lines of code, a scanned PDF document containing a raster image is converted into a searchable and selectable PDF document.

N> Starting with v20.1.0.x, if you reference Syncfusion OCR processor assemblies from trial setup or from the NuGet feed, you also have to include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/license-key) to know about registering Syncfusion license key in your application to use our components.

To use the Syncfusion OCR processor library in your application, you need to add reference to the following set of assemblies.

<b>Syncfusion assemblies</b>
1. Syncfusion.Compression.Base.dll
2. Syncfusion.Pdf.Base.dll
3. Syncfusion.OcrProcessor.Base.dll

<b>Tesseract assemblies</b>
* Syncfusion.Tesseract.dll (Tesseract Engine Version 4.0)
* liblept168.dll (Leptonica image processing library used by Tesseract engine)

## Steps to perform OCR on a entire PDF document programmatically

1. Create a new C# Windows Forms application project. 
![create-project.png](OCR-Images/WF-OCR-project.png)

2. Install [Syncfusion.Pdf.OCR.WinForms](https://www.nuget.org/packages/Syncfusion.PDF.OCR.WinForms/) NuGet packages as reference to your .NET Framework application from [NuGet.org](https://www.nuget.org/). 
![NuGet project](OCR-Images/OCR-NuGet.png)

3. Include the following namespaces in the Form1.cs file.

{% tabs %}  

{% highlight c# tabtitle="C#" %}

using Syncfusion.Pdf.Parsing;
using Syncfusion.OCRProcessor;

{% endhighlight %}

{% highlight c# tabtitle="VB.NET" %}

Imports Syncfusion.Pdf.Parsing
Imports Syncfusion.OCRProcessor

{% endhighlight %}

{% endtabs %}  

4. Tesseract assemblies are not added as a reference. They must be kept in the local machine, and the location of the assemblies are passed as a parameter to the OCR processor.

{% tabs %}  

{% highlight c# tabtitle="C#" %}

OCRProcessor processor = new OCRProcessor(@"TesseractBinaries/")

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

Dim processor As New OCRProcessor("TesseractBinaries/")

{% endhighlight %}

{% endtabs %}  

5. Place the Tesseract language data {E.g eng.traineddata} in the local system and provide a path to the OCR processor.

{% tabs %}  

{% highlight c# tabtitle="C#" %}

OCRProcessor processor = new OCRProcessor(@"TesseractBinaries/");
processor.PerformOCR(lDoc, @"TessData/");

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

Dim processor As New OCRProcessor("TesseractBinaries/")
processor.PerformOCR(lDoc, "TessData/")

{% endhighlight %}

{% endtabs %} 

6. Use the following code snippet to process OCR on a entire PDF document.

{% tabs %}  

{% highlight c# tabtitle="C#" %}

//Initialize the OCR processor by providing the path of tesseract binaries(SyncfusionTesseract.dll and liblept168.dll)
using (OCRProcessor processor = new OCRProcessor("TesseractBinaries/4.0/x86/"))
{
    //Load the PDF document
    PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");

    //Set OCR language to process
    processor.Settings.Language = Languages.English;

    //Set the tesseract version 
    processor.Settings.TesseractVersion = TesseractVersion.Version4_0;

    //Process OCR by providing the PDF document and Tesseract data
    processor.PerformOCR(loadedDocument, "Tessdata/");

    //Save the OCR processed PDF document in the disk
    loadedDocument.Save("Sample.pdf");
    loadedDocument.Close(true);
}

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Initialize the OCR processor by providing the path of tesseract binaries(SyncfusionTesseract.dll and liblept168.dll) 
Using processor As OCRProcessor = New OCRProcessor("TesseractBinaries/4.0/x86/")

    'Load the PDF document
    Dim loadedDocument As PdfLoadedDocument = New PdfLoadedDocument("Input.pdf")

    'Set OCR language to process
    processor.Settings.Language = Languages.English

    'Set the tesseract version 
    processor.Settings.TesseractVersion = TesseractVersion.Version4_0

    'Process OCR by providing the PDF document and Tesseract data
    processor.PerformOCR(loadedDocument, "Tessdata/")

    'Save the OCR processed PDF document in the disk
    loadedDocument.Save("Sample.pdf")
    loadedDocument.Close(True)

End Using

{% endhighlight %}

{% endtabs %} 

You can download a complete working sample from [GitHub]().

By executing the program, you will get the PDF document (contains selectable text) as follows. 
![output-pdf](OCR-Images/OCR-output-image.png)



