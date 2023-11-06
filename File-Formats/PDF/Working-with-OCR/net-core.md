---
title: Working with OCR in File Formats PDF image and files | Syncfusion
description: Learn all about working with orc on Syncfusion Essential scanned PDF documents file and images in different tesseract versions.
platform: file-formats
control: PDF
documentation: UG
keywords: Assemblies
---

# Perform OCR in File Formats PDF library

The [Syncfusion .NET OCR library](https://www.syncfusion.com/document-processing/pdf-framework/net-core/pdf-library/ocr-process) is used to extract text from the scanned PDFs and images in the ASP.NET Core application with the help of Google's [Tesseract](https://github.com/tesseract-ocr/tesseract) Optical Character Recognition engine.

## Steps to perform OCR on entire PDF document in ASP.NET Core application

Step 1: Create a new C# ASP.NET Core Web Application project.
![Create ASP.NET Core Web application](OCR-Images/OCR-Core-app-creation.png)   

Step 2:  In configuration windows, name your project and click Next.
![ASP.NET Core project configuration1](OCR-Images/OCR-Core-project-configuration1.png)
![ASP.NET Core project configuration2](OCR-Images/OCR-Core-project-configuration2.png)

Step 3:  Install the [Syncfusion.PDF.OCR.NET](https://www.nuget.org/packages/Syncfusion.PDF.OCR.NET) NuGet package as a reference to your .NET Standard applications from [NuGet.org](https://www.nuget.org/).   
![PDF OCR ASP.NET Core NuGet package](OCR-Images/OCR-Core-NuGet-package.png)

N> 1. Beginning from version 21.1.x, the default configuration includes the addition of the TesseractBinaries and Tesseract language data folder paths, eliminating the requirement to explicitly provide these paths.
N> 2. Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 4: A default controller with the name HomeController.cs gets added to the creation of the ASP.NET Core MVC project. Include the following namespaces in that HomeController.cs file.

{% highlight c# tabtitle="C#" %}

using Syncfusion.OCRProcessor;
using Syncfusion.Pdf.Parsing;

{% endhighlight %}

Step 5: Add a new button in index.cshtml as follows.

{% highlight c# tabtitle="C#" %}

@{Html.BeginForm("PerformOCR", "Home", FormMethod.Post);
   {
      <div>
         <input type="submit" value="Perform OCR" style="width:150px;height:27px" />
      </div>
   }
   Html.EndForm();
}

{% endhighlight %}

Step 6: Add a new action method named PerformOCR in the HomeController.cs and use the following code sample to perform OCR on the entire PDF document using [PerformOCR](https://help.syncfusion.com/cr/file-formats/Syncfusion.OCRProcessor.OCRProcessor.html#Syncfusion_OCRProcessor_OCRProcessor_PerformOCR_Syncfusion_Pdf_Parsing_PdfLoadedDocument_System_String_) method of the [OCRProcessor](https://help.syncfusion.com/cr/file-formats/Syncfusion.OCRProcessor.OCRProcessor.html) class. 

{% highlight c# tabtitle="C#" %}

//Initialize the OCR processor.
using (OCRProcessor processor = new OCRProcessor())
{
   FileStream fileStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);
   //Load a PDF document.
   PdfLoadedDocument lDoc = new PdfLoadedDocument(fileStream);
   //Set OCR language to process.
   processor.Settings.Language = Languages.English;
   //Process OCR by providing the PDF document.
   processor.PerformOCR(lDoc);
   //Create memory stream.
   MemoryStream stream = new MemoryStream();
   //Save the document to memory stream.
   lDoc.Save(stream);
   lDoc.Close();
   //Set the position as '0'.
   stream.Position = 0;
   //Download the PDF document in the browser.
   FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");
   fileStreamResult.FileDownloadName = "Sample.pdf";
   return fileStreamResult;
}

{% endhighlight %}

By executing the program, you will get a PDF document as follows.
![OCR ASP.NET_Core Output](OCR-Images/OCR-output-image.png)
 
A complete working sample can be downloaded from the [Github](https://github.com/SyncfusionExamples/OCR-csharp-examples/tree/master/ASP.NET%20Core).

Click [here](https://www.syncfusion.com/document-processing/pdf-framework/net-core) to explore the rich set of Syncfusion PDF library features.