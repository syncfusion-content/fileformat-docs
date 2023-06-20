---
title: Convert PPTX to PDF in Azure Functions v4 | Syncfusion
description: Convert PPTX to PDF in Azure Functions v4 using PowerPoint library (Presentation) without Microsoft PowerPoint or interop dependencies.
platform: file-formats
control: DocIO
documentation: UG
---

# Convert PowerPoint Presentation to PDF in Azure Functions v4

Syncfusion PowerPoint is a [.NET PowerPoint library](https://www.syncfusion.com/document-processing/powerpoint-framework/net-core) used to create, read, edit and **convert PowerPoint documents** programmatically without **Microsoft PowerPoint** or interop dependencies. Using this library, you can **convert a PowerPoint Presentation to PDF**.

## Steps to convert a PowerPoint Presentation to PDF in Azure Functions v4

Step 1: Create a new Azure Functions project.
![Create a Azure Functions project](Azure_Images/Functions_v1/Azure_PowerPoint_Presentation_to_PDF.png)

Step 2: Create a project name and select the location.
![Create a project name](Azure_Images/Functions_v1/Configure_PowerPoint_Presentation_to_PDF.png)

Step 3: Select function worker as **.NET Framework**. 
![Select function worker](Azure_Images/Functions_v4/Additional_Information_PowerPoint_Presentation_to_PDF.png)

Step 4: Install the [Syncfusion.PresentationRenderer.Net.Core](https://www.nuget.org/packages/Syncfusion.PresentationRenderer.Net.Core) NuGet package as a reference to your project from [NuGet.org](https://www.nuget.org/).
![Install Syncfusion.PresentationRenderer.Net.Core NuGet package](Azure_Images/Functions_v4/Nuget_Package_PowerPoint_Presentation_to_PDF.png)

Step 4: Include the following namespaces in the **Function1.cs** file.
{% tabs %}

{% highlight c# tabtitle="C#" %}
using Syncfusion.Presentation;
using Syncfusion.PresentationRenderer;
using Syncfusion.Pdf;
{% endhighlight %}

{% endtabs %}

Step 5: Add the following code snippet in **Run** method of **Function1** class to perform **PowerPoint Presentation to PDF conversion** in Azure Functions and return the resultant **PDF document** to client end.

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

Step 6: Right click the project and select **Publish**. Then, create a new profile in the Publish Window.
![Create a new profile in the Publish Window](Azure_Images/Functions_v1/Publish_PowerPoint_Presentation_to_PDF.png)

Step 7: Select the target as **Azure** and click **Next** button.
![Select the target as Azure](Azure_Images/Functions_v1/Target_PowerPoint_Presentation_to_PDF.png)

Step 8: Select the **Create new** button.
![Configure Hosting Plan](Azure_Images/Functions_v1/Function_Instance_PowerPoint_Presentation_to_PDF.png)

Step 9: Click **Create** button. 
![Select the plan type](Azure_Images/Functions_v1/Hosting_PowerPoint_Presentation_to_PDF.png)

Step 10: After creating app service then click **Finish** button. 
![Creating app service](Azure_Images/Functions_v1/Finish_PowerPoint_Presentation_to_PDF.png)

Step 11: Click the **Publish** button.
![Click Publish Button](Azure_Images/Functions_v1/Before_Publish_PowerPoint_Presentation_to_PDF.png)

Step 12: Publish has been succeed.
![Publish succeeded](Azure_Images/Functions_v1/After_Publish_PowerPoint_Presentation_to_PDF.png)

Step 13: Now, go to Azure portal and select the App Services. After running the service, click **Get function URL by copying it**. Then, paste it in the below client sample (which will request the Azure Functions, to perform **PowerPoint Presentation to PDF conversion** using the template PowerPoint document). You will get the output PDF document as follows.

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

From GitHub, you can download the [console application](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Convert-Word-document-to-PDF/Azure/Azure_Functions/Console_Application) and [Azure Functions v1](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Convert-Word-document-to-PDF/Azure/Azure_Functions/Azure_Functions_v1).

