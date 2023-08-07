---
title: Convert a HTML to PDF file in Blazor | Syncfusion
description: Learn how to convert a HTML to PDF file in Blazor with easy steps using Syncfusion .NET HTML converter library.
platform: file-formats
control: PDF
documentation: UG
keywords: Assemblies
---

# Convert HTML to PDF file in Blazor

The Syncfusion HTML to PDF converter is a .NET library used to convert HTML or web pages to PDF document in Blazor application.

N> Currently, HTML to PDF converter is mainly supported in Blazor Server-Side, while it is not compatible with Blazor WASM (WebAssembly).

## Steps to convert HTML to PDF in Blazor application

Step 1: Create a new C# Blazor Server application project. Select Blazor App from the template and click the Next button.
![Create Blazor application](htmlconversion_images/blazor_step1.png)  

In the project configuration window, name your project and select Create.
![Project configuration1](htmlconversion_images/blazor_step2.png)  
![Project configuration2](htmlconversion_images/blazor_step3.png)  

Step 2: Install the [Syncfusion.HtmlToPdfConverter.Net.Windows](https://www.nuget.org/packages/Syncfusion.HtmlToPdfConverter.Net.Windows/) NuGet package as a reference to your Blazor Server application from [NuGet.org](https://www.nuget.org/).
![NuGet package installation](htmlconversion_images/blazor_step_nuget.png)  

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 3: Create a new class file named ExportService under Data folder and include the following namespaces in the file.

{% highlight c# tabtitle="C#" %}

using Syncfusion.HtmlConverter;
using Syncfusion.Pdf;
using System.IO;

{% endhighlight %}

Step 4: Add the following code to convert HTML to PDF document in ExportService class using [Convert](https://help.syncfusion.com/cr/file-formats/Syncfusion.HtmlConverter.HtmlToPdfConverter.html#Syncfusion_HtmlConverter_HtmlToPdfConverter_Convert_System_String_) method in [HtmlToPdfConverter](https://help.syncfusion.com/cr/file-formats/Syncfusion.HtmlConverter.HtmlToPdfConverter.html) class.

{% highlight c# tabtitle="C#" %}

public MemoryStream CreatePdf(string url)
{
    //Initialize HTML to PDF converter.
    HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter();    
    //Convert URL to PDF document.
    PdfDocument document = htmlConverter.Convert(url);
    //Create memory stream.
    MemoryStream stream = new MemoryStream();
    //Save the document to memory stream.
    document.Save(stream);
    return stream;
}

{% endhighlight %}

Step 5: Register your service in the ConfigureServices method available in the Startup.cs class as follows.

{% highlight c# tabtitle="C#" %}

/// <summary>
/// Register your ExportService 
/// </summary>
public void ConfigureServices(IServiceCollection services)
{
    services.AddRazorPages();
    services.AddServerSideBlazor();
    services.AddSingleton<WeatherForecastService>();
    services.AddSingleton<ExportService>();
}

{% endhighlight %}

Step 6: Inject ExportService into FetchData.razor using the following code.

{% highlight c# tabtitle="C#" %}

@inject ExportService exportService
@inject Microsoft.JSInterop.IJSRuntime JS
@inject NavigationManager NavigationManager
@using  System.IO;

{% endhighlight %}

Step 7: Create a button in the FetchData.razor using the following code.

{% highlight c# tabtitle="C#" %}

<button class="btn btn-primary" @onclick="@ExportToPdf">Export to PDF</button>

{% endhighlight %}

Step 8: Add the ExportToPdf method in FetchData.razor page to call the export service.

{% highlight c# tabtitle="C#" %}

@code {
    private string currentUrl;
    /// <summary>
    /// Get the current URL
    /// </summary>
    protected override void OnInitialized()
    {
        currentUrl = NavigationManager.Uri;
    }
}

@functions
{
    /// <summary>
    /// Create and download the PDF document
    /// </summary>
    protected async Task ExportToPdf()
    {
        ExportService exportService = new ExportService();
        using (MemoryStream excelStream = exportService.CreatePdf(currentUrl))
        {
            await JS.SaveAs("HTMLToPDF.pdf", excelStream.ToArray());
        }
    }
}

{% endhighlight %}

Step 9: Create a class file with FileUtil name and add the following code to invoke the JavaScript action to download the file in the browser.

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

Step 10: Add the following JavaScript function in the _Host.cshtml available under the Pages folder.

{% highlight c# tabtitle="C#" %}

<script type="text/javascript">
    function saveAsFile(filename, bytesBase64)
    {
        if (navigator.msSaveBlob)
        {
            //Download document in Edge browser
            var data = window.atob(bytesBase64);
            var bytes = new Uint8Array(data.length);
            for (var i = 0; i < data.length; i++)
            {
                bytes[i] = data.charCodeAt(i);
            }
            var blob = new Blob([bytes.buffer], { type: "application/octet-stream" });
            navigator.msSaveBlob(blob, filename);
        }
        else
        {
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
![Browser window](htmlconversion_images/blazor_step4.png)   

Click the Export to PDF button, and you will get the PDF document with the following output.
![HTML to PDF Blazor output](htmlconversion_images/HtmlBlazorOutput.png)   
    
A complete working sample for converting an HTML to PDF in the Blazor framework can be downloaded from [Github](https://github.com/SyncfusionExamples/html-to-pdf-csharp-examples/tree/master/Blazor).

Click [here](https://www.syncfusion.com/document-processing/pdf-framework/blazor/html-to-pdf) to explore the rich set of Syncfusion HTML to PDF converter library features. 

An online sample link to [convert HTML to PDF document](https://ej2.syncfusion.com/aspnetcore/PDF/HtmltoPDF#/material3) in ASP.NET Core.