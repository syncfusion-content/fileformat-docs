---
title: Perform OCR on PDF and image files in Blazor | Syncfusion
description: Learn how to perform OCR on scanned PDF documents and images with different tesseract versions in Blazor using Syncfusion .NET OCR library.
platform: file-formats
control: PDF
documentation: UG
keywords: Assemblies
---

# Perform OCR in Blazor

The [Syncfusion .NET OCR library](https://www.syncfusion.com/document-processing/pdf-framework/net-core/pdf-library/ocr-process) is used to extract text from scanned PDFs and images in the Blazor application with the help of Google's [Tesseract](https://github.com/tesseract-ocr/tesseract) Optical Character Recognition engine.

## Steps to perform OCR on the entire PDF document in the Blazor application

Step 1: Create a new C# Blazor Server application project. Select Blazor App from the template and click Next.
![Blazor server app creation](OCR-Images/blazor_server_app_creation.png)

Step 2: In the project configuration window, name your project and click Create.
![Blazor server project configuraion1](OCR-Images/blazor_server_configuration1.png)
![Blazor server project configuraion1](OCR-Images/blazor_server_configuration2.png)

Step 3: Install the [Syncfusion.PDF.OCR.NET](https://www.nuget.org/packages/Syncfusion.PDF.OCR.NET) NuGet package as a reference to your Blazor Server application from [NuGet.org](https://www.nuget.org/).
![Blazor server NuGet package installation](OCR-Images/blazor_nuget_package.png)

N> 1. Beginning from version 21.1.x, the default configuration includes the addition of the TesseractBinaries and Tesseract language data folder paths, eliminating the requirement to explicitly provide these paths.
N> 2. Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 4: Create a new class file named *ExportService* under the Data folder and include the following namespaces in the file.

{% highlight c# tabtitle="C#" %}

using Syncfusion.OCRProcessor;
using Syncfusion.Pdf.Parsing;
using System.IO;

{% endhighlight %}

Step 5: Use the following code sample to perform OCR on the entire PDF document using [PerformOCR](https://help.syncfusion.com/cr/file-formats/Syncfusion.OCRProcessor.OCRProcessor.html#Syncfusion_OCRProcessor_OCRProcessor_PerformOCR_Syncfusion_Pdf_Parsing_PdfLoadedDocument_System_String_) method of the [OCRProcessor](https://help.syncfusion.com/cr/file-formats/Syncfusion.OCRProcessor.OCRProcessor.html) class in the **ExportService** file.  

{% highlight c# tabtitle="C#" %}

public MemoryStream CreatePdf()
{   
    //Initialize the OCR processor.
    using (OCRProcessor processor = new OCRProcessor("Tesseractbinaries/Windows"))
    {
        FileStream fileStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);
        //Load a PDF document.
        PdfLoadedDocument lDoc = new PdfLoadedDocument(fileStream);
        //Set OCR language to process.
        processor.Settings.Language = Languages.English;
        //Process OCR by providing the PDF document.
        processor.PerformOCR(lDoc, "tessdata/");
        //Create memory stream.
        MemoryStream stream = new MemoryStream();
        //Save the document to memory stream.
        lDoc.Save(stream);
        return stream;
    }
}

{% endhighlight %}

Step 6: Register your service in the ConfigureServices method available in the *Startup.cs* class as follows.

{% highlight c# tabtitle="C#" %}

public void ConfigureServices(IServiceCollection services)
{
    services.AddRazorPages();
    services.AddServerSideBlazor();
    services.AddSingleton<WeatherForecastService>();
    services.AddSingleton<ExportService>();
}

{% endhighlight %}

Step 7: Inject ExportService into *FetchData.razor* using the following code.

{% highlight c# tabtitle="C#" %}

@inject ExportService exportService
@inject Microsoft.JSInterop.IJSRuntime JS
@using  System.IO;

{% endhighlight %}

Step 8: Create a button in the *FetchData.razor* using the following code.

{% highlight c# tabtitle="C#" %}

<button class="btn btn-primary" @onclick="@PerformOCR">Perform OCR</button>

{% endhighlight %}

Step 9: Add the PerformOCR method in *FetchData.razor* page to call the export service.

{% highlight c# tabtitle="C#" %}

@functions
{
   protected async Task PerformOCR()
   {
       ExportService exportService = new ExportService();
       using (MemoryStream excelStream = exportService.CreatePdf())
       {
           await JS.SaveAs("Output.pdf", excelStream.ToArray());
       }
   }
}

{% endhighlight %}

Step 10: Create a class file with the FileUtil name and add the following code to invoke the JavaScript action to download the file in the browser.

{% highlight c# tabtitle="C#" %}

public static class FileUtil
{
    public static ValueTask<object> SaveAs(this IJSRuntime js, string filename, byte[] data)
     => js.InvokeAsync<object>(
         "saveAsFile",
         filename,
         Convert.ToBase64String(data));
}

{% endhighlight %}

Step 11: Add the following JavaScript function in the *_Host.cshtml* available under the Pages folder.

{% highlight c# tabtitle="C#" %}

<script type="text/javascript">
    function saveAsFile(filename, bytesBase64) {
        if (navigator.msSaveBlob) {
            //Download document in Edge browser
            var data = window.atob(bytesBase64);
            var bytes = new Uint8Array(data.length);
            for (var i = 0; i < data.length; i++) {
                bytes[i] = data.charCodeAt(i);
            }
            var blob = new Blob([bytes.buffer], { type: "application/octet-stream" });
            navigator.msSaveBlob(blob, filename);
        }
        else {
            var link = document.createElement('a');
            link.download = filename;
            link.href = "data:application/octet-stream;base64," + bytesBase64;
            document.body.appendChild(link); // Needed for Firefox
            link.click();
            document.body.removeChild(link);
        }
    }
</script>

{% endhighlight %}

You will get the following output in the browser by executing the program.
![Blazor browser window](OCR-Images/blazor_server_broswer_window.png)

Click the button and get a PDF document with the following output.
![Blazor output PDF document](OCR-Images/OCR-output-image.png)
    
A complete working sample can be downloaded from [Github](https://github.com/SyncfusionExamples/OCR-csharp-examples/tree/master/Blazor).

Click [here](https://www.syncfusion.com/document-processing/pdf-framework/blazor) to explore the rich set of Syncfusion PDF library features.