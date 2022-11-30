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

## Steps to convert HTML to PDF in Blazor application

Step 1: Create a new C# Blazor Server application project. Select Blazor App from the template and click the Next button.
   <img src="htmlconversion_images/blazor_step1.png" alt="Blazor_step1" width="100%" Height="Auto"/>

   In the project configuration window, name your project and select Create.
   <img src="htmlconversion_images/blazor_step2.png" alt="Blazor_step2" width="100%" Height="Auto"/>
   <img src="htmlconversion_images/blazor_step3.png" alt="Blazor_step3" width="100%" Height="Auto"/>

Step 2: Install the [Syncfusion.HtmlToPdfConverter.Net.Windows](https://www.nuget.org/packages/Syncfusion.HtmlToPdfConverter.Net.Windows/) NuGet package as a reference to your Blazor Server application from [NuGet.org](https://www.nuget.org/).
   <img src="htmlconversion_images/blazor_step_nuget.png" alt="blazor_step_nuget" width="100%" Height="Auto"/>

Step 3: Create a new class file named ExportService under Data folder and include the following namespaces in the file.

   {% highlight c# tabtitle="C#" %}

   using Syncfusion.HtmlConverter;
   using Syncfusion.Pdf;
   using System.IO;

   {% endhighlight %}

Step 4: Add the following code to convert HTML to PDF document in ExportService class.

   {% highlight c# tabtitle="C#" %}

   public MemoryStream CreatePdf()
   {
      //Initialize HTML to PDF converter.
      HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter();
      BlinkConverterSettings blinkConverterSettings = new BlinkConverterSettings();
      //Set Blink viewport size.
      blinkConverterSettings.ViewPortSize = new Syncfusion.Drawing.Size(1280, 0);
      //Assign Blink converter settings to HTML converter.
      htmlConverter.ConverterSettings = blinkConverterSettings;
      //Convert URL to PDF document.
      PdfDocument document = htmlConverter.Convert("https://www.syncfusion.com");
      //Create memory stream.
      MemoryStream stream = new MemoryStream();
      //Save the document to memory stream.
      document.Save(stream);
      return stream;
   }

   {% endhighlight %}

Step 5: Register your service in the ConfigureServices method available in the Startup.cs class as follows.

   {% highlight c# tabtitle="C#" %}

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
   @using  System.IO;

   {% endhighlight %}

Step 7: Create a button in the FetchData.razor using the following code.

   {% highlight c# tabtitle="C#" %}

   <button class="btn btn-primary" @onclick="@ExportToPdf">Export to PDF</button>

   {% endhighlight %}

Step 8: Add the ExportToPdf method in FetchData.razor page to call the export service.

   {% highlight c# tabtitle="C#" %}

   @functions
   {
      protected async Task ExportToPdf()
      {
         ExportService exportService = new ExportService();
         using (MemoryStream excelStream = exportService.CreatePdf())
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
   <img src="htmlconversion_images/blazor_step4.png" alt="Blazor_step4" width="100%" Height="Auto"/>

   Click the Export to PDF button, and you will get the PDF document with the following output.
   <img src="htmlconversion_images/htmltopdfoutput.png" alt="Convert HTMLToPDF Blazor output" width="100%" Height="Auto"/>
    
   A complete working sample for converting an HTML to PDF in the Blazor framework can be downloaded from [Github](https://github.com/SyncfusionExamples/html-to-pdf-csharp-examples/tree/master/Blazor).
    