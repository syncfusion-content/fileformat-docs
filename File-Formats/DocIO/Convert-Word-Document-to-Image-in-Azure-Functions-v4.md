---
title: Convert Word document to Image in Azure Functions v4 | Syncfusion
description: Convert Word document to Image in Azure Functions v4 using .NET Core Word (DocIO) library without Microsoft Word or interop dependencies.
platform: file-formats
control: DocIO
documentation: UG
---

# Convert Word document to Image in Azure Functions v4

Syncfusion DocIO is a [.NET Core Word library](https://www.syncfusion.com/document-processing/word-framework/net/word-library) used to create, read, edit, and **convert Word documents** programmatically without **Microsoft Word** or interop dependencies. Using this library, you can **convert a Word document to image in Azure Functions v4**.

## Steps to convert a Word document to Image in Azure Functions v4

Step 1: Create a new Azure Functions project.
![Create a Azure functions project](Azure_Images/Functions_v1/Azure_Function_WordtoPDF.png)

Step 2: Create a project name and select the location.
![Create a project name](Azure_Images/Functions_v1/Configuration_WordtoImage.png)

Step 3: Select function worker as **.NET 6.0(Long-term support)**.
![Select function worker](Azure_Images/Functions_v4/Additional-Information-WordtoPDF.png)

Step 4: Install the [Syncfusion.DocIORenderer.Net.Core](https://www.nuget.org/packages/Syncfusion.DocIORenderer.Net.Core) NuGet package as a reference to your project from [NuGet.org](https://www.nuget.org/).
![Install Syncfusion.DocIORenderer.Net.Core NuGet package](Azure_Images/Functions_v4/Nuget-Package-WordtoImage.png)

Step 5: Include the following namespaces in the **Function1.cs** file.
{% tabs %}

{% highlight c# tabtitle="C#" %}
using Syncfusion.DocIO;
using Syncfusion.DocIO.DLS;
using Syncfusion.DocIORenderer;
{% endhighlight %}

{% endtabs %}

Step 6: Add the following code snippet in **Run** method of **Function1** class to perform **convert Word to image** in Azure Functions and return the resultant **image** to client end.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Gets the input Word document as stream from request
Stream stream = req.Content.ReadAsStreamAsync().Result;
//Loads an existing Word document
using (WordDocument document = new WordDocument(stream, FormatType.Docx))
{
    //Creates an instance of the DocIORenderer
    using (DocIORenderer render = new DocIORenderer())
    {
        Stream imageStream = document.RenderAsImages(0, ExportImageFormat.Jpeg);
        //Reset the stream position.
        imageStream.Position = 0;
        MemoryStream memoryStream = new MemoryStream();
        //Saves the Image file 
        imageStream.CopyTo(memoryStream);
        //Reset the memory stream position
        memoryStream.Position = 0;
        //Create the response to return
        HttpResponseMessage response = new HttpResponseMessage(HttpStatusCode.OK);
        //Set the Word document saved stream as content of response
        response.Content = new ByteArrayContent(memoryStream.ToArray());
        //Set the contentDisposition as attachment
        response.Content.Headers.ContentDisposition = new ContentDispositionHeaderValue("attachment")
        {
            FileName = "WordToImage.Jpeg"
        };
        //Set the content type as Word document mime type
        response.Content.Headers.ContentType = new System.Net.Http.Headers.MediaTypeHeaderValue("application/jpeg");
        //Return the response with output Word document stream
        return response;
    }
}

{% endhighlight %}

{% endtabs %}

Step 7: Right click the project and select **Publish**. Then, create a new profile in the Publish Window.
![Create a new profile in the Publish Window](Azure_Images/Functions_v1/Publish_WordtoImage.png)

Step 8: Select the target as **Azure** and click **Next** button.
![Select the target as Azure](Azure_Images/Functions_v1/Target_WordtoPDF.png)

Step 9: Select the **Create new** button.
![Configure Hosting Plan](Azure_Images/Functions_v1/Function_Instance_WordtoImage.png)

Step 10: Click **Create** button. 
![Select the plan type](Azure_Images/Functions_v1/Subscription_detail_WordtoImage.png)

Step 11: After creating app service then click **Finish** button. 
![Creating app service](Azure_Images/Functions_v1/Function_Instance_WordtoImage.png)

Step 12: Click the **Publish** button.
![Click Publish Button](Azure_Images/Functions_v1/Before_Publish_WordtoPDF.png)

Step 13: Publish has been succeed.
![Publish succeeded](Azure_Images/Functions_v1/Published_WordtoImage.png)

Step 14: Now, go to Azure portal and select the App Services. After running the service, click **Get function URL by copying it**. Then, paste it in the below client sample (which will request the Azure Functions, to perform **Word to image conversion** using the template Word document). You will get the output **image** as follows.

![Word to Image in Azure Functions v4](Azure_Images/Functions_v1/Output-WordtoImage.png)

## Steps to post the request to Azure Functions

Step 1: Create a console application to request the Azure Functions API.

Step 2: Add the following code snippet into **Main** method to post the request to Azure Functions with template Word document and get the resultant image.
{% tabs %}

{% highlight c# tabtitle="C#" %}

//Reads the template Word document.
FileStream fs = new FileStream("Input.docx", FileMode.Open, FileAccess.ReadWrite, FileShare.ReadWrite);
fs.Position = 0;
//Saves the Word document in memory stream.
MemoryStream inputStream = new MemoryStream();
fs.CopyTo(inputStream);
inputStream.Position = 0;
try
{
    Console.WriteLine("Please enter your Azure Functions URL :");
    string functionURL = Console.ReadLine();

    //Create HttpWebRequest with hosted azure functions URL.                
    HttpWebRequest req = (HttpWebRequest)WebRequest.Create(functionURL);
    //Set request method as POST
    req.Method = "POST";
    //Get the request stream to save the Word document stream
    Stream stream = req.GetRequestStream();
    //Write the Word document stream into request stream
    stream.Write(inputStream.ToArray(), 0, inputStream.ToArray().Length);
    //Gets the responce from the Azure Functions.
    HttpWebResponse res = (HttpWebResponse)req.GetResponse();
    //Saves the image stream.
    FileStream fileStream = File.Create("WordToImage.Jpeg");
    res.GetResponseStream().CopyTo(fileStream);
    //Dispose the streams
    inputStream.Dispose();
    fileStream.Dispose();
}
catch (Exception ex)
{
    throw;
}
{% endhighlight %}

{% endtabs %}

From GitHub, you can download the [console application](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-Image-conversion/Convert-Word-to-image/Azure/Azure_Functions/Console_Application) and [Azure Functions v4](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-Image-conversion/Convert-Word-to-image/Azure/Azure_Functions/Azure_Functions_v4).

