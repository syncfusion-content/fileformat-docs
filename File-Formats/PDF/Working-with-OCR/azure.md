---
title: Perform OCR on PDF and image files in Azure | Syncfusion
description: Learn how to perform OCR on scanned PDF documents and images with different tesseract versions in Azure using Syncfusion .NET OCR library.
platform: file-formats
control: PDF
documentation: UG
keywords: Assemblies
---

# Perform OCR in Azure using C#

The [Syncfusion .NET OCR library](https://www.syncfusion.com/document-processing/pdf-framework/net/pdf-library/ocr-process) is used to extract text from scanned PDFs and images in Azure with the help of Google's [Tesseract](https://github.com/tesseract-ocr/tesseract) Optical Character Recognition engine.

## Azure App Service Windows

### Steps to perform OCR on entire PDF document in Azure App Service

Step 1: Create a new ASP.NET Core MVC application.
<img src="OCR-Images/azure_step1.png" alt="Convert OCR Azure NetCore Step1" width="100%" Height="Auto"/> 

Step 2: In configuration windows, name your project and click Next.
<img src="OCR-Images/azure_step2.png" alt="Convert OCR Azure NetCore Step2" width="100%" Height="Auto"/> 
<img src="OCR-Images/azure_step3.png" alt="Convert OCR Azure NetCore Step3" width="100%" Height="Auto"/> 

Step 3: Install the [Syncfusion.PDF.OCR.NET](https://www.nuget.org/packages/Syncfusion.PDF.OCR.NET) NuGet package as a reference to your .NET Core application [NuGet.org](https://www.nuget.org/).
<img src="OCR-Images/azure_step4.png" alt="Convert OCR Azure NetCore Step4" width="100%" Height="Auto"/> 

Step 4: Tesseract assemblies are not added as a reference. They must be kept in the local machine, and the assemblies location is passed as a parameter to the OCR processor.

{% highlight c# tabtitle="C#" %}

OCRProcessor processor = new OCRProcessor(@"Tesseractbinaries/Windows");

{% endhighlight %}

Step 5: Place the Tesseract language data {e.g, eng.traineddata} in the local system and provide a path to the OCR processor. Please use the OCR language data for other languages using the following link.

[Tesseract language data](https://github.com/tesseract-ocr/tessdata)

{% highlight c# tabtitle="C#" %}

OCRProcessor processor = new OCRProcessor(@"Tesseractbinaries/Windows");
processor.PerformOCR(lDoc, "tessdata/");

{% endhighlight %}

Step 6: Add a new button in index.cshtml as follows.

{% highlight c# tabtitle="C#" %}

@{
    Html.BeginForm("PerformOCR", "Home", FormMethod.Get);
    {
        <br />
        <div>
            <input type="submit" value="Perform OCR" style="width:150px;height:27px" />
        </div>
    }
    Html.EndForm();
}

{% endhighlight %}

Step 7: Include the following namespaces in the HomeController.cs file.

{% highlight c# tabtitle="C#" %}

using Syncfusion.OCRProcessor;
using Syncfusion.Pdf.Parsing;
using Microsoft.AspNetCore.Hosting.IHostingEnvironment;

{% endhighlight %}

Step 8: Add the code samples for performing OCR on the entire PDF document using [PerformOCR](https://help.syncfusion.com/cr/file-formats/Syncfusion.OCRProcessor.OCRProcessor.html#Syncfusion_OCRProcessor_OCRProcessor_PerformOCR_Syncfusion_Pdf_Parsing_PdfLoadedDocument_System_String_) method of the [OCRProcessor](https://help.syncfusion.com/cr/file-formats/Syncfusion.OCRProcessor.OCRProcessor.html) class. 

{% highlight c# tabtitle="C#" %}

public IActionResult PerformOCR()
{
    //Initialize the OCR processor with tesseract binaries folder path.
    OCRProcessor processor = new OCRProcessor("Tesseractbinaries/Windows/");
    //Load a PDF document.
    PdfLoadedDocument lDoc = new PdfLoadedDocument("Input.pdf");
    //Set OCR language to process.
    processor.Settings.Language = Languages.English;
    //Perform OCR with input document and tessdata (Language packs).
    string ocr = processor.PerformOCR(lDoc, "Tessdata/");
    //Save the document. 
    MemoryStream stream = new MemoryStream();
    lDoc.Save(stream);
    return File(stream.ToArray(), System.Net.Mime.MediaTypeNames.Application.Pdf, "OCR_Azure.pdf");
}

{% endhighlight %}

Step 9: Now, check the OCR creation in the local machine.

### Steps to publish as Azure App Service

Step 1: Right-click the project and click Publish.
<img src="OCR-Images/azure_step5.png" alt="Convert OCR Azure NetCore Step5" width="100%" Height="Auto"/>

Step 2: Create a new profile in the publish target window.
<img src="OCR-Images/azure_step6.png" alt="Convert OCR Azure NetCore Step6" width="100%" Height="Auto"/>
<img src="OCR-Images/azure_step7.png" alt="Convert OCR Azure NetCore Step7" width="100%" Height="Auto"/> 

Step 3: Create an App Service using an Azure subscription and select a hosting plan based on the environment.
<img src="OCR-Images/azure_step8.png" alt="Convert OCR Azure NetCore Step8" width="100%" Height="Auto"/> 

Step 4: Configure the Hosting plan.
<img src="OCR-Images/azure_step9.png" alt="Convert OCR Azure NetCore Step9" width="100%" Height="Auto"/>

Step 5: After creating a profile, click Publish.
<img src="OCR-Images/azure_step10.png" alt="Convert OCR Azure NetCore Step10" width="100%" Height="Auto"/> 

Now, the published webpage will open in the browser, then click the **Perform OCR** button then perform OCR on a PDF document.
<img src="OCR-Images/azure_step11.png" alt="Convert OCR Azure NetCore Step11" width="100%" Height="Auto"/>
<img src="OCR-Images/OCR-output-image.png" alt="Convert OCR Azure NetCore Step11" width="100%" Height="Auto"/> 

A complete work sample for performing OCR on a PDF document in Azure App Service on Windows can be downloaded from [GitHub](https://github.com/SyncfusionExamples/OCR-csharp-examples/tree/master/Azure/Azure%20App%20Services).

## Azure Functions

### Steps to perform OCR on the entire PDF document in Azure Functions

Step 1: Create the Azure function project.
<img src="OCR-Images/AzureFunctions1.png" alt="Convert OCR Azure Functions Step1" width="100%" Height="Auto"/> 

Step 2: Select the framework to Azure Functions and select HTTP triggers as follows.
<img src="OCR-Images/AzureFunctions2.png" alt="Convert OCR Azure Functions Step2" width="100%" Height="Auto"/> 
<img src="OCR-Images/AzureFunctions3.png" alt="Convert OCR Azure Functions Step3" width="100%" Height="Auto"/>

Step 3: Install the [Syncfusion.PDF.OCR.NET](https://www.nuget.org/packages/Syncfusion.PDF.OCR.NET) NuGet package as a reference to your .NET Core application [NuGet.org](https://www.nuget.org/).
<img src="OCR-Images/AzureFunctions4.png" alt="Convert OCR Azure Functions Step4" width="100%" Height="Auto"/> 

Step 4: Tesseract assemblies are not added as a reference. They must be kept in the local machine, and the assemblies location is passed as a parameter to the OCR processor.

{% highlight c# tabtitle="C#" %}

OCRProcessor processor = new OCRProcessor(@"Tesseractbinaries/Windows");

{% endhighlight %}

Step 5: Place the Tesseract language data {E.g, eng.traineddata} in the local system and provide a path to the OCR processor. Please use the OCR language data for other languages using the following link.

[Tesseract language data](https://github.com/tesseract-ocr/tessdata)

{% highlight c# tabtitle="C#" %}

OCRProcessor processor = new OCRProcessor(@"Tesseractbinaries/Windows");
processor.PerformOCR(lDoc, "tessdata/");

{% endhighlight %}

Step 6: Include the following namespaces in the Function1.cs file to perform OCR for a PDF document using C#.

{% highlight c# tabtitle="C#" %}

using System;
using System.IO;
using System.Threading.Tasks;
using Syncfusion.OCRProcessor;
using Syncfusion.Pdf.Graphics;
using Syncfusion.Pdf;
using System.Net.Http;
using Syncfusion.Pdf.Parsing;
using System.Net.Http.Headers;
using System.Net;
using Microsoft.Azure.WebJobs.Host;
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.Http;

{% endhighlight %}

Step 7: Add the following code sample in the Function1 class to perform OCR for a PDF document using [PerformOCR](https://help.syncfusion.com/cr/file-formats/Syncfusion.OCRProcessor.OCRProcessor.html#Syncfusion_OCRProcessor_OCRProcessor_PerformOCR_Syncfusion_Pdf_Parsing_PdfLoadedDocument_System_String_) method of the [OCRProcessor](https://help.syncfusion.com/cr/file-formats/Syncfusion.OCRProcessor.OCRProcessor.html) class in Azure Functions.

{% highlight c# tabtitle="C#" %}

[FunctionName("Function1")]
public static async Task<HttpResponseMessage> Run([HttpTrigger(AuthorizationLevel.Function, "get", "post", Route = null)] HttpRequestMessage req, TraceWriter log, ExecutionContext executionContext)
{
    MemoryStream ms = new MemoryStream();
    try
    {
        string path = Path.GetFullPath(Path.Combine(executionContext.FunctionAppDirectory, "bin\\Tesseractbinaries\\Windows"));
        OCRProcessor processor = new OCRProcessor(path);
        FileStream stream = new FileStream(Path.Combine(executionContext.FunctionAppDirectory, "Data", "Input.pdf"), FileMode.Open);
        //Load a PDF document.
        PdfLoadedDocument lDoc = new PdfLoadedDocument(stream);
        //Set OCR language to process.
        processor.Settings.Language = Languages.English;
        //Perform OCR with input document and tessdata (Language packs).
        string ocr = processor.PerformOCR(lDoc, Path.Combine(executionContext.FunctionAppDirectory, "tessdata"));            
        //Save the PDF document.  
        lDoc.Save(ms);
        ms.Position = 0;
    }
    catch (Exception ex)
    {
        //Add a page to the document.
        PdfDocument document = new PdfDocument();
        PdfPage page = document.Pages.Add();
        //Create PDF graphics for the page.
        PdfGraphics graphics = page.Graphics;
        //Set the standard font.
        PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 6);
        //Draw the text.
        graphics.DrawString(ex.ToString(), font, PdfBrushes.Black, new Syncfusion.Drawing.PointF(0, 0));
        ms = new MemoryStream();
        //Save the PDF document.  
        document.Save(ms);
    }
    HttpResponseMessage response = new HttpResponseMessage(HttpStatusCode.OK);
    response.Content = new ByteArrayContent(ms.ToArray());
    response.Content.Headers.ContentDisposition = new ContentDispositionHeaderValue("attachment")
    {
        FileName = "Output.pdf"
    };
    response.Content.Headers.ContentType = new System.Net.Http.Headers.MediaTypeHeaderValue("application/pdf");
    return response;
}

{% endhighlight %}

Step 8: Now, check the OCR creation in the local machine.

### Steps to publish as Azure Functions 

Step 1: Right-click the project and click Publish. Then, create a new profile in the Publish Window. So, create the Azure Function App with a consumption plan.
<img src="OCR-Images/AzureFunctions5.png" alt="Convert OCR Azure Functions Step5" width="100%" Height="Auto"/>
<img src="OCR-Images/azure_step6.png" alt="Convert OCR Azure Functions Step6" width="100%" Height="Auto"/>
<img src="OCR-Images/AzureFunctions7.png" alt="Convert OCR Azure Functions Step7" width="100%" Height="Auto"/>

Step 2: After creating the profile, click Publish.
<img src="OCR-Images/AzureFunctions8.png" alt="Convert OCR Azure Functions Step8" width="100%" Height="Auto"/>

Step 3: Now, go to the Azure portal and select the Functions Apps. After running the service, click Get function URL > Copy. Include the URL as a query string in the URL. Then, paste it into the new browser tab. You will get a PDF document as follows.
<img src="OCR-Images/OCR-output-image.png" alt="Convert OCR Azure Functions Step9" width="100%" Height="Auto"/> 

A complete working sample can be downloaded from [GitHub](https://github.com/SyncfusionExamples/OCR-csharp-examples/tree/master/Azure/Azure%20Function).