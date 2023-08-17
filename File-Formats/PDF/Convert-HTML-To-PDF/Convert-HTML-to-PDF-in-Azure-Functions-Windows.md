---
title: Convert HTML to PDF in Azure Functions | Syncfusion
description: Convert HTML to PDF in Azure Functions using Syncfusion .NET HTML converter library.
platform: file-formats
control: PDF
documentation: UG
---

# Convert HTML to PDF file in Azure Functions

The Syncfusion [HTML to PDF converter](https://www.syncfusion.com/document-processing/pdf-framework/net/html-to-pdf) is a .NET library for converting webpages, SVG, MHTML, and HTML to PDF using C#. Using this library, you can **convert HTML to PDF document in Azure Functions on Windows**.

## Steps to convert HTML to PDF file in Azure Functions on Windows

Step 1: Create the Azure functions project.
![Convert HTMLToPDF Azure Functions Step1](Azure_images/Azure_function/AzureFunctions1.png)

Step 2: Create a project name and select the location.
![Project naming](Azure_images/Azure_function/AzureFunctions2.png)

Step 3: Select function worker as .NET 6.0(Long-term support) and select HTTP triggers as follows. 
![Convert HTMLToPDF Azure Functions Step3](Azure_images/Azure_function/AzureFunctions3.png)

Step 4: Install the [Syncfusion.HtmlToPdfConverter.QtWebKit.Net.Core](https://www.nuget.org/packages/Syncfusion.HtmlToPdfConverter.QtWebKit.Net.Core/) NuGet package as a reference to your project using **Package Manager Console**.
![Convert HTMLToPDF Azure Functions Step4](Azure_images/Azure_function/AzureFunctions4.png) 

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 5: Include the following namespaces in the **Function1.cs** file.

{% tabs %}
{% highlight c# tabtitle="C#" %}

using Syncfusion.HtmlConverter;
using Syncfusion.Pdf;

{% endhighlight %}
{% endtabs %}

Step 6: Add the following code example in **Run** method of **Function1** class to perform **convert HTML to PDF document** in Azure Functions and return the resultant **PDF document**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

[FunctionName("Function1")]
public static async Task<HttpResponseMessage> Run(
    [HttpTrigger(AuthorizationLevel.Function, "get", "post", Route = null)] HttpRequest req,
    ILogger log, ExecutionContext context)
{
    MemoryStream ms = new MemoryStream();
    try {
        //Initialize HTML to PDF converter.
        HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter(HtmlRenderingEngine.WebKit);
        WebKitConverterSettings settings = new WebKitConverterSettings();
        //Set WebKit path.
        settings.WebKitPath = Path.Combine(context.FunctionAppDirectory, "bin/runtimes/win-x64/native");            
        //Assign WebKit settings to HTML converter.
        htmlConverter.ConverterSettings = settings;
        //Convert URL to PDF.
        PdfDocument document = htmlConverter.Convert("https://www.google.com");

        //Save and close the PDF document.  
        document.Save(ms);
        document.Close();
        ms.Position = 0;
        }

        catch (Exception ex) {
            //Create a new PDF document.
            PdfDocument document = new PdfDocument();
            //Add a page to the document.
            PdfPage page = document.Pages.Add();
            //Create PDF graphics for the page.
            PdfGraphics graphics = page.Graphics;

            //Set the standard font.
            PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 5);
            //Draw the text.
            graphics.DrawString(ex.ToString(), font, PdfBrushes.Black, new Syncfusion.Drawing.PointF(0, 0));

            //Creating the stream object.
            ms = new MemoryStream();
            //Save the document into memory stream.
            document.Save(ms);
            //Close the document.
            document.Close(true);
            ms.Position = 0;
        }

        HttpResponseMessage response = new HttpResponseMessage(HttpStatusCode.OK);
        response.Content = new ByteArrayContent(ms.ToArray());
        response.Content.Headers.ContentDisposition = new ContentDispositionHeaderValue("attachment") {
            FileName = "Sample.pdf"
        };
        response.Content.Headers.ContentType = new System.Net.Http.Headers.MediaTypeHeaderValue("application/pdf");
        return response;
}

{% endhighlight %}
{% endtabs %}

Step 7: Copy the OPENSSL assemblies and paste it into the **runtimes/win-x64/native** folder which contains the HTML_to_PDF_Azure_Functions.csproj file.

N> The OPENSSL libraries can be installed by downloading its setup from the below [link.](https://www.syncfusion.com/downloads/support/directtrac/general/ze/OPENSSL-798051511)

![Right-click the project and select the publish option](Azure_images/Azure_function/runtimes.png)

Step 8: Make sure to set **Copy if newer** for all the OPENSSL assemblies.
![Right-click the project and select the publish option](Azure_images/Azure_function/copy_if_newer.png)

Step 9: Right click the project and select Publish. Then, create a new profile in the Publish Window.
![Create a new profile in the Publish Window](Azure_Images/Azure_function/Click_publish.png)

Step 10: Select the target as **Azure** and click **Next** button.
![Select the target as Azure](Azure_Images/Azure_function/Set_Azure_target.png)

Step 11: Select the **Azure Function App (Windows)** and click **Next**. 
![Select Azure function app](Azure_Images/Azure_function/Select_function_app.png)

Step 12: Select the **Create new** button.
![Configure Hosting Plan](Azure_Images/Azure_function/Select_create_new_button.png)

Step 13: Click **Create** button. 
![Browser will open after publish](Azure_images/Azure_function/WebView.png)

Step 14: After creating function app service then click **Finish** button. 
![Creating app service](Azure_Images/Azure_function/Creating_app_function.png)

Step 15: Click the **Publish** button.
![Click the Publish button](Azure_images/Azure_function/Publish_app_function.png)

Step 16: Now, Publish has been succeeded.
![Publish has been succeeded](Azure_images/Azure_function/Publish_link(function).png)

Step 17: Now, go to Azure portal and select the App Services. After running the service, click **Get function URL > Copy**. Include the URL as a query string in the URL. Then, paste it into the new browser tab. You will get the PDF document as follows. 
![Output document screenshot](Azure_Images/Azure_function/Output_screenshot.png)

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/html-to-pdf-csharp-examples/tree/master/Azure/HTML-to-PDF-Azure-Functions(Windows)).