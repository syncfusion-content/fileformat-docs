---
title: Perform OCR on PDF and Image Files in Mac | Syncfusion
description: Learn how to perform OCR on scanned PDF documents and images in WPF with different Tesseract versions using Syncfusion .NET OCR library. 
platform: file-formats
control: PDF
documentation: UG
keywords: Assemblies
--- 

# Perform OCR in Mac 

The [Syncfusion .NET OCR library](https://www.syncfusion.com/document-processing/pdf-framework/net/pdf-library/ocr-process) used to extract text from scanned PDFs and images in the Mac application.

## Steps to perform OCR on entire PDF document in Mac

Step 1: Create a new .NET Core console application project.
![Mac OS console application](OCR-Images/Mac_OS_Console.png)

Step 2: Select the project version.

Step 3: Install the [Syncfusion.PDF.OCR.Net.Core](https://www.nuget.org/packages/Syncfusion.PDF.OCR.Net.Core) NuGet package as a reference to your project from [NuGet.org](https://www.nuget.org/).
![Mac OS NuGet path](OCR-Images/Mac_OS_NuGet_path.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from the trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to learn about registering the Syncfusion license key in your application to use our components.

Step 4: Include the following Namespaces in the Program.cs file.
{% tabs %}
{% highlight c# tabtitle="C#" %}

using Syncfusion.OCRProcessor;

using Syncfusion.Pdf.Parsing;

{% endhighlight %}

{% endtabs %}

Step 5: Add the following code sample to the *Program.cs* file to **Perform OCR in .NET Core application on Mac OS**.
{% tabs %}

{% highlight c# tabtitle="C#" %}

//Initialize the OCR processor.
using (OCRProcessor processor = new OCRProcessor())
{
   FileStream fileStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);
   //Load a PDF document.
   PdfLoadedDocument lDoc = new PdfLoadedDocument(fileStream);
   //Set the OCR language to be processed.
   processor.Settings.Language = Languages.English;
   //Process OCR by providing the PDF document.
   processor.PerformOCR(lDoc);
   //Create memory stream.
   MemoryStream stream = new MemoryStream();
   //Save the document to the memory stream.
   lDoc.Save(stream);
   lDoc.Close();
   //Set the position as '0'.
   stream.Position = 0;
   //Download the PDF document in the browser.
   FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");
   fileStreamResult.FileDownloadName = "OCR.pdf";
   return fileStreamResult;
}

{% endhighlight %}

{% endtabs %}


By executing the program, you will get a PDF document as follows. 
![WPF OCR output screenshot](OCR-Images/Output.png)

A complete working sample can be downloaded from [GitHub](https://github.com/SyncfusionExamples/OCR-csharp-examples/tree/master/WPF).

Click [here](https://www.syncfusion.com/document-processing/pdf-framework/net) to explore the rich set of Syncfusion PDF library features.

