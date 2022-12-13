---
title: Perform OCR on a PDF document in Blazor | Syncfusion
description: Learn how to efficiently perform OCR on a PDF document in Blazor with easy steps using Syncfusion .NET library.
platform: file-formats
control: PDF
documentation: UG
keywords: Assemblies
---

# Perform OCR on a PDF document in Blazor

The Syncfusion Essential PDF is a .NET PDF library that supports OCR by using the Tesseract open-source engine in Blazor application.

## Steps to perform OCR on a PDF document in Blazor application

Step 1: Create a new C# Blazor Server application project. Select Blazor App from the template and click the Next button.
<img src="OCR-Images/blazor_step1.png" alt="Blazor_step1" width="100%" Height="Auto"/>

In the project configuration window, name your project and select Create.
<img src="OCR-Images/blazor_step2.png" alt="Blazor_step2" width="100%" Height="Auto"/>
<img src="OCR-Images/blazor_step3.png" alt="Blazor_step3" width="100%" Height="Auto"/>

Step 2: Install the [Syncfusion.PDF.OCR.NET](https://www.nuget.org/packages/Syncfusion.PDF.OCR.NET) NuGet package as a reference to your Blazor Server application from [NuGet.org](https://www.nuget.org/).
<img src="OCR-Images/blazor_step_nuget.png" alt="blazor_step_nuget" width="100%" Height="Auto"/>

Step 3: Tesseract assemblies are not added as a reference. They must be kept in the local machine, and the location of the assemblies is passed as a parameter to the OCR processor.

{% highlight c# tabtitle="C#" %}

OCRProcessor processor = new OCRProcessor(@"Tesseractbinaries/Windows");

{% endhighlight %}

Step 4: Place the Tesseract language data {E.g eng.traineddata} in the local system and provide a path to the OCR processor. Please use the OCR language data for other languages using the following link,
https://github.com/tesseract-ocr/tessdata

{% highlight c# tabtitle="C#" %}

OCRProcessor processor = new OCRProcessor(@"Tesseractbinaries/Windows");
processor.PerformOCR(lDoc, "tessdata/");

{% endhighlight %}

Step 5: Create a new class file named ExportService under Data folder and include the following namespaces in the file.

{% highlight c# tabtitle="C#" %}

using Syncfusion.OCRProcessor;
using Syncfusion.Pdf.Parsing;
using System.IO;

{% endhighlight %}

Step 6: Use the following code sample to perform OCR in the ExportService class.

{% highlight c# tabtitle="C#" %}

public MemoryStream CreatePdf()
{
    string docPath = Path.GetFullPath("wwwroot/Data/Input.pdf");
    string tesseractPath = Path.GetFullPath("wwwroot/Data/Tesseractbinaries/Windows");            
    //Initialize the OCR processor by providing the path of tesseract binaries(SyncfusionTesseract.dll and liblept168.dll)
    using (OCRProcessor processor = new OCRProcessor(tesseractPath))
    {
        FileStream fileStream = new FileStream(docPath, FileMode.Open, FileAccess.Read);
        //Load a PDF document
        PdfLoadedDocument lDoc = new PdfLoadedDocument(fileStream);
        //Set OCR language to process
        processor.Settings.Language = Languages.English;
        string tessdataPath = Path.GetFullPath("wwwroot/Data/tessdata");
        //Process OCR by providing the PDF document and Tesseract data
        processor.PerformOCR(lDoc, tessdataPath);
        //Create memory stream.
        MemoryStream stream = new MemoryStream();
        //Save the document to memory stream.
        lDoc.Save(stream);
        return stream;
    }
}

{% endhighlight %}

Step 7: Register your service in the ConfigureServices method available in the Startup.cs class as follows.

{% highlight c# tabtitle="C#" %}

public void ConfigureServices(IServiceCollection services)
{
    services.AddRazorPages();
    services.AddServerSideBlazor();
    services.AddSingleton<WeatherForecastService>();
    services.AddSingleton<ExportService>();
}

{% endhighlight %}

Step 8: Inject ExportService into FetchData.razor using the following code.

{% highlight c# tabtitle="C#" %}

@inject ExportService exportService
@inject Microsoft.JSInterop.IJSRuntime JS
@using  System.IO;

{% endhighlight %}

Step 9: Create a button in the FetchData.razor using the following code.

{% highlight c# tabtitle="C#" %}

<button class="btn btn-primary" @onclick="@PerformOCR">Perform OCR</button>

{% endhighlight %}

Step 10: Add the PerformOCR method in FetchData.razor page to call the export service.

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

Step 11: Create a class file with FileUtil name and add the following code to invoke the JavaScript action to download the file in the browser.

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

Step 12: Add the following JavaScript function in the _Host.cshtml available under the Pages folder.

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

By executing the program, you will get the following output in the browser.
<img src="OCR-Images/blazor_step4.png" alt="Blazor_step4" width="100%" Height="Auto"/>

Click the button, and you will get the PDF document with the following output.
<img src="OCR-Images/OCR-output-image.png" alt="Convert OCR Blazor output" width="100%" Height="Auto"/>
    
A complete working sample can be downloaded from Github.
    