---
title: Perform OCR on PDF and image files in Linux | Syncfusion
description: Learn how to perform OCR on scanned PDF documents and images in Linux with different tesseract versions using Syncfusion .NET OCR library.
control: PDF
documentation: UG
keywords: Assemblies
---

# Perform OCR in Linux

The [Syncfusion .NET OCR library](https://www.syncfusion.com/document-processing/pdf-framework/net/pdf-library/ocr-process) is used to extract text from scanned PDFs and images in the Linux application with the help of Google's [Tesseract](https://github.com/tesseract-ocr/tesseract) Optical Character Recognition engine.
## Pre-requisites

The following Linux dependencies should be installed where the conversion takes place. 

{% highlight c# tabtitle="C#" %}

sudo apt-get update
sudo apt-get install libgdiplus
sudo apt-get install libc6-dev

{% endhighlight %}

## Steps to convert HTML to PDF in .NET Core application on Linux

Step 1: Execute the following command in the Linux terminal to create a new .NET Core Console application.

{% highlight c# tabtitle="C#" %}

dotnet new console

{% endhighlight %}

![OCR Linux Step1](OCR-Images/LinuxStep1.png)

Step 2: Install the [Syncfusion.PDF.OCR.Net](https://www.nuget.org/packages/Syncfusion.PDF.OCR.Net/) NuGet package as a reference to your .NET Core application [NuGet.org](https://www.nuget.org/).

{% highlight c# tabtitle="C#" %}

dotnet add package Syncfusion.PDF.OCR.Net -v xx.x.x.xx -s https://www.nuget.org/

{% endhighlight %}

![OCR Linux Step2](OCR-Images/LinuxStep2.png)

Step 3: Include the following namespaces in Program.cs file.

{% highlight c# tabtitle="C#" %}

using Syncfusion.OCRProcessor;
using Syncfusion.Pdf;
using Syncfusion.Pdf.Parsing;

{% endhighlight %}

N> Beginning from version 21.1.x, the default configuration includes the addition of the TesseractBinaries and Tesseract language data folder paths, eliminating the requirement to explicitly provide these paths.

Step 4: Add code sample to perform OCR on entire PDF document using [PerformOCR](https://help.syncfusion.com/cr/file-formats/Syncfusion.OCRProcessor.OCRProcessor.html#Syncfusion_OCRProcessor_OCRProcessor_PerformOCR_Syncfusion_Pdf_Parsing_PdfLoadedDocument_System_String_) method of the [OCRProcessor](https://help.syncfusion.com/cr/file-formats/Syncfusion.OCRProcessor.OCRProcessor.html) class. 

{% highlight c# tabtitle="C#" %}
 
string docPath = ("input.pdf");

//Initialize the OCR processor
using (OCRProcessor processor = new OCRProcessor())
{
    //Load the PDF document 
    FileStream stream = new FileStream(docPath, FileMode.Open, FileAccess.Read);
    PdfLoadedDocument lDoc = new PdfLoadedDocument(stream);

    //Language to process the OCR
    processor.Settings.Language = Languages.English;
    //Process OCR by providing loaded PDF document, Data dictionary and language
    processor.PerformOCR(lDoc);

    //Save the OCR processed PDF document in the disk
    MemoryStream streamData = new MemoryStream();
    lDoc.Save(streamData);
    File.WriteAllBytes("Output.pdf", streamData.ToArray());
    lDoc.Close(true);
}

{% endhighlight %}

Step 5: Execute the following command to restore the NuGet packages.

{% highlight c# tabtitle="C#" %}

dotnet restore

{% endhighlight %}

![OCR Linux Step3](OCR-Images/LinuxStep3.png)

Step 6:  Execute the following command in the terminal to build the application.

{% highlight c# tabtitle="C#" %}

dotnet build

{% endhighlight %}

![OCR Linux Step4](OCR-Images/LinuxStep4.png)

Step 7: Execute the following command in the terminal to run the application.

{% highlight c# tabtitle="C#" %}

dotnet run

{% endhighlight %}

![OCR Linux Step5](OCR-Images/LinuxStep5.png)

By executing the program, you will get the PDF document as follows. The output will be saved in parallel to the program.cs file.
![OCR Linux Output](OCR-Images/OCR-output-image.png)

A complete working sample can be downloaded from [Github](https://github.com/SyncfusionExamples/OCR-csharp-examples/tree/master/Linux).
