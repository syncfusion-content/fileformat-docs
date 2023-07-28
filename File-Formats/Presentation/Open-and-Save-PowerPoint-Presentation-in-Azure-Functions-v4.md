---
title: Open and save Presentation in Azure Functions v4 | Syncfusion
description: Open and save Presentation in Azure Functions v4 using .NET Core PowerPoint library (Presentation) without Microsoft PowerPoint or interop dependencies.
platform: file-formats
control: PowerPoint
documentation: UG
---

# Open and save Presentation in Azure Functions v4

Syncfusion PowerPoint is a [.NET Core PowerPoint library](https://www.syncfusion.com/document-processing/powerpoint-framework/net-core) used to create, read, edit and convert PowerPoint documents programmatically without **Microsoft PowerPoint** or interop dependencies. Using this library, you can **open and save Presentation in Azure Functions v4**.

## Steps to open and save Presentation in Azure Functions v4

Step 1: Create a new Azure Functions project.
![Create a Azure Functions project](Azure_Images/Functions_v1/Azure_PowerPoint_Presentation_to_PDF.png)

Step 2: Create a project name and select the location.
![Create a project name](Azure_Images/Functions_v1/Configuration-Open-and-Save-PowerPoint.png)

Step 3: Select function worker as **.NET Framework**. 
![Select function worker](Azure_Images/Functions_v4/Additional_Information_PowerPoint_Presentation_to_PDF.png)

Step 4: Install the [Syncfusion.Presentation.Net.Core](https://www.nuget.org/packages/Syncfusion.Presentation.Net.Core) NuGet package as a reference to your project from [NuGet.org](https://www.nuget.org/).
![Install Syncfusion.Presentation.Net.Core NuGet package](Workingwith_Core/Nuget-Package_Open_and_Save.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 5: Include the following namespaces in the **Function1.cs** file.

{% tabs %}
{% highlight c# tabtitle="C#" %}

using Syncfusion.Presentation;

{% endhighlight %}
{% endtabs %}

Step 6: Add the following code snippet in **Run** method of **Function1** class to perform **open the existing Presentation in Azure Functions v4**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Gets the input PowerPoint document as stream from request
Stream stream = req.Content.ReadAsStreamAsync().Result;
//Open an existing PowerPoint presentation
using (IPresentation pptxDoc = Presentation.Open(stream))

{% endhighlight %}
{% endtabs %}

Step 7: Add below code snippet demonstrates accessing a shape from a slide and changing the text within it.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Gets the first slide from the PowerPoint presentation
ISlide slide = pptxDoc.Slides[0];
//Gets the first shape of the slide
IShape shape = slide.Shapes[0] as IShape;
//Change the text of the shape
if (shape.TextBody.Text == "Company History")
    shape.TextBody.Text = "Company Profile";

{% endhighlight %}
{% endtabs %}

Step 8: Add below code example to **save the PowerPoint Presentation in Azure Functions v4**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

MemoryStream memoryStream = new MemoryStream();
pptxDoc.Save(memoryStream);
//Reset the memory stream position.
memoryStream.Position = 0;
//Create the response to return.
HttpResponseMessage response = new HttpResponseMessage(HttpStatusCode.OK);
//Set the PowerPoint document saved stream as content of response.
response.Content = new ByteArrayContent(memoryStream.ToArray());
//Set the contentDisposition as attachment.
response.Content.Headers.ContentDisposition = new ContentDispositionHeaderValue("attachment")
{
    FileName = "Sample.pptx"
};
//Set the content type as PowerPoint document mime type.
response.Content.Headers.ContentType = new System.Net.Http.Headers.MediaTypeHeaderValue("application/pptx");
//Return the response with output PowerPoint document stream.
return response;

{% endhighlight %}
{% endtabs %}

Step 9: Right click the project and select **Publish**. Then, create a new profile in the Publish Window.
![Create a new profile in the Publish Window](Azure_Images/Functions_v1/Publish-Open-and-Save-PowerPoint.png)

Step 10: Select the target as **Azure** and click **Next** button.
![Select the target as Azure](Azure_Images/Functions_v1/Target_PowerPoint_Presentation_to_PDF.png)

Step 11: Select the **Create new** button.
![Configure Hosting Plan](Azure_Images/Functions_v1/Function_Instance_PowerPoint_Presentation_to_PDF.png)

Step 12: Click **Create** button. 
![Select the plan type](Azure_Images/Functions_v1/Hosting-Open-and-Save-PowerPoint.png)

Step 13: After creating app service then click **Finish** button. 
![Creating app service](Azure_Images/Functions_v1/Azure-Instance-Open-and-Save-PowerPoint.png)

Step 14: Click the **Publish** button.
![Click Publish Button](Azure_Images/Functions_v1/Before-Publish-Open-and-Save-PowerPoint.png)

Step 15: Publish has been succeed.
![Publish succeeded](Azure_Images/Functions_v1/After-Publish-Open-and-Save-PowerPoint.png)

Step 16: After publishing your Azure Function, go to the [Azure portal](https://portal.azure.com) and locate the Function App that hosts your function. In the function app, you can see the list of all available functions in the app.
![Functions in Azure Portal](Azure_Images/Functions_v1/Function-app-WordtoPDF.png)

Step 17: Find the function for which you want to obtain the URL and click on its name. This will open the Function Overview page for that specific function.
![Functions in Azure Portal](Azure_Images/Functions_v1/Function1-WordtoPDF.png)

Step 18: On the Function Overview page, you will find a Get function URL button. Clicking on it will reveal the URL specific to that function. Copy that **URL** and run the console application. Then, paste the URL into the console application, this will trigger your Function to **open and save a PowerPoint document**.
![Get Function URL in Azure Portal](Azure_Images/Functions_v1/Function-URL-WordtoPDF.png)

By executing the program, you will get the **PowerPoint document** as follows.

![PowerPoint to Image in Azure Functions v4](Workingwith_Core/Open-and-Save-output-image.png)

## Steps to post the request to Azure Functions

Step 1: Create a console application to request the Azure Functions API.

Step 2: Add the following code snippet into **Main** method to post the request to Azure Functions with template PowerPoint document and get the resultant image.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Reads the template PowerPoint file.
FileStream fs = new FileStream(@"../../Data/Template.pptx", FileMode.Open, FileAccess.ReadWrite, FileShare.ReadWrite);
fs.Position = 0;
//Saves the PowerPoint file in memory stream.
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
    //Get the request stream to save the PowerPoint file stream
    Stream stream = req.GetRequestStream();
    //Write the PowerPoint file stream into request stream
    stream.Write(inputStream.ToArray(), 0, inputStream.ToArray().Length);

    //Gets the responce from the Azure Functions.
    HttpWebResponse res = (HttpWebResponse)req.GetResponse();

    //Saves the PowerPoint file stream.
    FileStream fileStream = File.Create("Sample.pptx");
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

From GitHub, you can download the [console application](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Read-and-save-PowerPoint-presentation/Open-and-save-PowerPoint/Azure/Azure_Functions/Console_Application) and [Azure Functions v4](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Read-and-save-PowerPoint-presentation/Open-and-save-PowerPoint/Azure/Azure_Functions/Azure_Functions_v4).

Click [here](https://www.syncfusion.com/document-processing/powerpoint-framework/net-core) to explore the rich set of Syncfusion PowerPoint Library (Presentation) features. 

