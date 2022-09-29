---
title: Convert a HTML to PDF file in Blazor | Syncfusion
description: Learn how to convert a HTML to PDF file in Blazor with easy steps using Syncfusion .NET HTML converter library.
platform: file-formats
control: PDF
documentation: UG
keywords: Assemblies
---

# Convert HTML to PDF file in Blazor

Steps to convert HTML to PDF in Blazor application

Create a new C# Blazor application project. Select Blazor App from the template and click the Next button.
![Blazor_step1](htmlconversion_images/blazor_step1.png)

Now, the project configuration window appears. Click Create button to create a new project with the default project configuration.
![Blazor_step2](htmlconversion_images/blazor_step2.png)

Install the [Syncfusion.HtmlToPdfConverter.Net.Windows](https://www.nuget.org/packages/Syncfusion.HtmlToPdfConverter.Net.Windows/) NuGet package as a reference to your Blazor application from [NuGet.org](https://www.nuget.org/).
![Blazor_step3](htmlconversion_images/blazor_step3.png)

Create a new cs file named ExportService under Data folder and include the following namespaces in the file.
![Blazor_step4](htmlconversion_images/blazor_step4.png)

{% highlight c# tabtitle="C#" %}

using Syncfusion.HtmlConverter;
using Syncfusion.Pdf;
using System.IO;

{% endhighlight %}


Add the following method in the ExportService class

{% highlight c# tabtitle="C#" %}

public MemoryStream CreatePdf()
{
    //Initialize HTML to PDF converter.
    HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter();
    //Convert URL to PDF.
    PdfDocument document = htmlConverter.Convert("https://www.syncfusion.com");
    MemoryStream stream = new MemoryStream();
    document.Save(stream);
    return stream;
}

{% endhighlight %}

Register your service in the ConfigureServices method available in the Startup.cs class as follows.

{% highlight c# tabtitle="C#" %}

public void ConfigureServices(IServiceCollection services)
{
    services.AddRazorPages();
    services.AddServerSideBlazor();
    services.AddSingleton<WeatherForecastService>();
    services.AddSingleton<ExportService>();
}

{% endhighlight %}

Inject ExportService in-to FetchData.razor using the following code.

{% highlight c# tabtitle="C#" %}

@inject ExportToFileService exportService
@inject Microsoft.JSInterop.IJSRuntime JS
@using  System.IO;

{% endhighlight %}

Create a button in the FetchData.razor using the following code.

{% highlight c# tabtitle="C#" %}

<button class="btn btn-primary" @onclick="@ExportToPdf">Export to PDF</button>

{% endhighlight %}

Add the ExportToPdf method in FetchData.razor page to call the export service.

{% highlight c# tabtitle="C#" %}

@functions
{
 
    protected async Task ExportToPdf()
    {
        using (MemoryStream excelStream =exportService.CreatePdf(forecasts))
        {
            await JS.SaveAs("HTMLToPDF.pdf", excelStream.ToArray());
        }
    }
}

{% endhighlight %}

Create a class file with FileUtil name and add the following code to invoke the JavaScript action to download the file in the browser.

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

Add the following JavaScript function in the _Host.cshtml available under the Pages folder.

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
![Blazor_step5](htmlconversion_images/blazor_step5.png)

Click the Export to PDF button, and you will get the PDF document with the following output.
![HTMLTOPDF](htmlconversion_images/htmltopdfoutput.png)

A complete work sample for converting an HTML to PDF in the Blazor framework can be downloaded from [Blazor-HTML-to-PDF-Demo.zip ](https://www.syncfusion.com/downloads/support/directtrac/general/ze/Blazor-HTML-to-PDF-Demo-899009860)
