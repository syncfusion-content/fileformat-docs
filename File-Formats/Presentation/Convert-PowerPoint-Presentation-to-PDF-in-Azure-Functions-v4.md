---
title: Convert PPTX to PDF in Azure Functions v4 | Syncfusion
description: Convert PPTX to PDF in Azure Functions v4 using .NET Core PowerPoint library (Presentation) without Microsoft PowerPoint or interop dependencies.
platform: file-formats
control: PowerPoint
documentation: UG
---

# Convert PowerPoint Presentation to PDF in Azure Functions v4

Syncfusion PowerPoint is a [.NET Core PowerPoint library](https://www.syncfusion.com/document-processing/powerpoint-framework/net-core) used to create, read, edit and **convert PowerPoint documents** programmatically without **Microsoft PowerPoint** or interop dependencies. Using this library, you can **convert a PowerPoint Presentation to PDF in Azure Functions v4**.

## Create an Azure Functions App

Step 1: Create a new Azure Functions project.
![Create a Azure Functions project](Azure_Images/Functions_v1/Azure_PowerPoint_Presentation_to_PDF.png)

Step 2: Create a project name and select the location.
![Create a project name](Azure_Images/Functions_v1/Configure_PowerPoint_Presentation_to_PDF.png)

Step 3: Select function worker as **.NET 6.0 (Long Term Support)**. 
![Select function worker](Azure_Images/Functions_v4/Additional_Information_PowerPoint_Presentation_to_PDF.png)

Step 4: Install the [Syncfusion.PresentationRenderer.Net.Core](https://www.nuget.org/packages/Syncfusion.PresentationRenderer.Net.Core) NuGet package as a reference to your project from [NuGet.org](https://www.nuget.org/).
![Install Syncfusion.PresentationRenderer.Net.Core NuGet package](Azure_Images/Functions_v4/Nuget_Package_PowerPoint_Presentation_to_PDF.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 5: Include the following namespaces in the **Function1.cs** file.
{% tabs %}

{% highlight c# tabtitle="C#" %}
using Syncfusion.Presentation;
using Syncfusion.PresentationRenderer;
using Syncfusion.Pdf;
{% endhighlight %}

{% endtabs %}

Step 6: Add the following code snippet in **Run** method of **Function1** class to perform **PowerPoint Presentation to PDF conversion** in Azure Functions and return the resultant **PDF document** to client end.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Gets the input PowerPoint document as stream from request.
Stream stream = req.Content.ReadAsStreamAsync().Result;
//Loads an existing PowerPoint document
using (IPresentation pptxDoc = Presentation.Open(stream))
{
    //Creates an instance of the DocToPDFConverter.
    using (PdfDocument pdfDocument = PresentationToPdfConverter.Convert(pptxDoc))
    {
        MemoryStream memoryStream = new MemoryStream();
        //Saves the PDF file .
        pdfDocument.Save(memoryStream);
        //Reset the memory stream position.
        memoryStream.Position = 0;
        //Create the response to return.
        HttpResponseMessage response = new HttpResponseMessage(HttpStatusCode.OK);
        //Set the PDF document saved stream as content of response.
        response.Content = new ByteArrayContent(memoryStream.ToArray());
        //Set the contentDisposition as attachment.
        response.Content.Headers.ContentDisposition = new ContentDispositionHeaderValue("attachment")
        {
            FileName = "Sample.Pdf"
        };
        //Set the content type as PDF document mime type.
        response.Content.Headers.ContentType = new System.Net.Http.Headers.MediaTypeHeaderValue("application/pdf");
        //Return the response with output PDF document stream.
        return response;
    }
}
{% endhighlight %}
{% endtabs %}

## Publish to Azure Functions

Step 1: Right click the project and select **Publish**. Then, create a new profile in the Publish Window.
![Create a new profile in the Publish Window](Azure_Images/Functions_v1/Publish_PowerPoint_Presentation_to_PDF.png)

Step 2: Select the target as **Azure** and click **Next** button.
![Select the target as Azure](Azure_Images/Functions_v1/Target_PowerPoint_Presentation_to_PDF.png)

Step 3: Select the **Create new** button.
![Configure Hosting Plan](Azure_Images/Functions_v1/Function_Instance_PowerPoint_Presentation_to_PDF.png)

Step 4: Click **Create** button. 
![Select the plan type](Azure_Images/Functions_v1/Hosting_PowerPoint_Presentation_to_PDF.png)

Step 5: After creating app service then click **Finish** button. 
![Creating app service](Azure_Images/Functions_v1/Finish_PowerPoint_Presentation_to_PDF.png)

Step 6: Click the **Publish** button.
![Click Publish Button](Azure_Images/Functions_v1/Before_Publish_PowerPoint_Presentation_to_PDF.png)

Step 7: Publish has been succeed.
![Publish succeeded](Azure_Images/Functions_v1/After_Publish_PowerPoint_Presentation_to_PDF.png)

## Obtain the Azure Function URL

Step 1: After publishing your Azure Function, go to the [Azure portal](https://portal.azure.com) and locate the Function App that hosts your function. In the function app, you can see the list of all available functions in the app.
![Functions in Azure Portal](Azure_Images/Functions_v1/Functions-WordtoPDF.png)

Step 2: Find the function for which you want to obtain the URL and click on its name. This will open the Function Overview page for that specific function.
![Functions in Azure Portal](Azure_Images/Functions_v1/Function1-WordtoPDF.png)

Step 3: On the Function Overview page, you will find a Get function URL button. Clicking on it will reveal the URL specific to that function. Copy that **URL** and run the console application. Then, paste the URL into the console application, this will trigger your Function to **convert a PowerPoint Presentation to PDF**.
![Get Function URL in Azure Portal](Azure_Images/Functions_v1/GetFuctionURL-WordtoPDF.png)

By executing the program, you will get the **PDF** as follows.

![PowerPoint to PDF in Azure Functions v4](Azure_Images/Functions_v1/Output_PowerPoint_Presentation_to-PDF.png)

## Steps to post the request to Azure Functions

Step 1: Create a console application to request the Azure Functions API.

Step 2: Add the following code snippet into **Main** method to post the request to Azure Functions with template PowerPoint document and get the resultant PDF document.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Reads the template PowerPoint document.
FileStream fs = new FileStream("Input.pptx", FileMode.Open, FileAccess.ReadWrite, FileShare.ReadWrite);
fs.Position = 0;
//Saves the PowerPoint document in memory stream.
MemoryStream inputStream = new MemoryStream();
fs.CopyTo(inputStream);
inputStream.Position = 0;
try
{
    Console.WriteLine("Please enter your Azure Functions URL :");
    string functionURL = Console.ReadLine();
    //Create HttpWebRequest with hosted azure functions URL.                
    HttpWebRequest req = (HttpWebRequest)WebRequest.Create(functionURL);
    //Set request method as POST.
    req.Method = "POST";
    //Get the request stream to save the PowerPoint document stream
    Stream stream = req.GetRequestStream();
    //Write the PowerPoint document stream into request stream.
    stream.Write(inputStream.ToArray(), 0, inputStream.ToArray().Length);
    //Gets the responce from the Azure Functions.
    HttpWebResponse res = (HttpWebResponse)req.GetResponse();
    //Saves the PDF stream.
    FileStream fileStream = File.Create("Sample.pdf");
    res.GetResponseStream().CopyTo(fileStream);
    //Dispose the streams.
    inputStream.Dispose();
    fileStream.Dispose();
}
catch (Exception ex)
{
    throw;
}

{% endhighlight %}
{% endtabs %}

From GitHub, you can download the [console application](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/PPTX-to-PDF-conversion/Convert-PowerPoint-presentation-to-PDF/Azure/Azure_Functions/Console_Application) and [Azure Functions v4](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/PPTX-to-PDF-conversion/Convert-PowerPoint-presentation-to-PDF/Azure/Azure_Functions/Azure_Functions_v4).

Click [here](https://www.syncfusion.com/document-processing/powerpoint-framework/net-core) to explore the rich set of Syncfusion PowerPoint Library (Presentation) features. 

An online sample link to [convert PowerPoint Presentation to PDF](https://ej2.syncfusion.com/aspnetcore/PowerPoint/PPTXToPDF#/material3) in ASP.NET Core. 

