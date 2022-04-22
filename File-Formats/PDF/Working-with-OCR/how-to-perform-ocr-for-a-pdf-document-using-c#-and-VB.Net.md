---
title: How to perform OCR for a PDF document using c# and VB.NET | Syncfusion
description: This section explains how to perform OCR for a PDF document using c# and VB.NET.
platform: file-formats
control: PDF
documentation: UG
---

# How to perform OCR for a PDF document using c# and VB.NET

Syncfusion Essential PDF is a [.NET PDF library](https://www.syncfusion.com/pdf-framework/net/pdf-library) that supports OCR by using the Tesseract open-source engine. With a few lines of code, you can perform OCR on a particular region or several regions of a PDF document.

The following assemblies are required to use the OCR feature in your application:

Syncfusion assemblies
•	Syncfusion.Compression.Base.dll
•	Syncfusion.Pdf.Base.dll
•	Syncfusion.OcrProcessor.Base.dll

Tesseract assemblies
•	SyncfusionTessaract.dll (Tesseract Engine Version 4.0)
•	liblept168.dll ([Leptonica](http://www.leptonica.com/) image processing library used by Tesseract engine) 

## Steps to perform OCR on particular region of a PDF programmatically: 

1.	Create a new C# Windows Forms application project. 
![create-project.png](OCR_images/create_framework_project.png)

2.  Install [Syncfusion.Pdf.OCR.WinForms]](https://www.nuget.org/packages/Syncfusion.PDF.OCR.WinForms/) NuGet packages as reference to your .NET Framework application from [NuGet.org](https://www.nuget.org/). 
![NuGet project](OCR_images/install_NuGet_framework.png)

3.	Include the following namespaces in the Form.cs file.

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

4.	Tesseract assemblies are not added as a reference. They must be kept in the local machine, and the location of the assemblies are passed as a parameter to the OCR processor.

{% tabs %}  

{% highlight c# tabtitle="C#" %}

OCRProcessor processor = new OCRProcessor(@"TesseractBinaries\")

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

Dim processor As New OCRProcessor("TesseractBinaries\")

{% endhighlight %}

{% endtabs %}  

5.	Place the Tesseract language data {E.g eng.traineddata} in the local system and provide a path to the OCR processor.

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

6.	Use the following code snippet to process OCR for the PDF document.

{% tabs %}  

{% highlight c# tabtitle="C#" %}

//Load a PDF document.
PdfLoadedDocument lDoc = new PdfLoadedDocument("input.pdf");

OCRProcessor processor = new OCRProcessor(@"../../Tesseractbinaries/");
processor.Settings.Language = Languages.English;

//Process OCR by providing the PDF document and Tesseract data.
processor.PerformOCR(lDoc, @"../../Tessdata/");

//Save the OCR processed PDF document in the disk.
lDoc.Save("Output.pdf");
lDoc.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Load a PDF document.
Dim lDoc As New PdfLoadedDocument("input.pdf")
Dim processor As New OCRProcessor("../../Tesseractbinaries/")

'Set OCR language to process.
processor.Settings.Language = Languages.English;

'Process OCR by providing the PDF document and Tesseract data
processor.PerformOCR(lDoc, "../../Tessdata/")

'Save the OCR processed PDF document in the disk.
lDoc.Save("OCRingRegionOfPDF.pdf")
lDoc.Close(True)

{% endhighlight %}

{% endtabs %} 

A complete working sample can be downloaded here [OCRFrameworkSample.zip](https://www.syncfusion.com/downloads/support/directtrac/general/ze/OCRFramework_Sample57780594.zip)

By executing the program, you will get the text file (contains extracted text) as follows. 
![output-pdf](OCR_images/framework_output.png)



