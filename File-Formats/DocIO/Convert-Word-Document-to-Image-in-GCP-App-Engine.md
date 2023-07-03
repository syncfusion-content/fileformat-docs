---
title: Convert Word to Image in GCP App Engine | Syncfusion
description: Convert Word to image in GCP App Engine using .NET Core Word (DocIO) library without Microsoft Word or interop dependencies.
platform: file-formats
control: DocIO
documentation: UG
---

# Convert Word to Image in GCP App Engine

Syncfusion DocIO is a [.NET Core Word library](https://www.syncfusion.com/document-processing/word-framework/net-core/word-library) that allows you to create, read, edit, and **convert Word documents** programmatically, without the need for **Microsoft Word** or interop dependencies. Using this library, you can **convert Word document to image in Google Cloud Platform (GCP) App Engine**.

## Setting Up App Engine

Step 1: Click the **Activate Cloud Shell** button.
![Activate Cloud Shell](GCP_Images/Activate-Cloud-Shell-WordtoPDF.png)

Step 2: Click the **Open editor** button.
![Open Editor in Cloud Shell](GCP_Images/Authentication-WordtoPDF.png)

Step 3: Open **Cloud Shell editor**, run the following **command** to confirm authentication.

{% tabs %}
{% highlight CLI %}

gcloud auth list

{% endhighlight %}
{% endtabs %}

![Authentication for App Engine](GCP_Images/Editor-Button-WordtoPDF.png)

Step 4: Click the **Authorize** button.
![Click Authorize button](GCP_Images/Authorize-WordtoPDF.png)

## Creating a Sample Application Using Visual Studio

Step 1: Open Visual Studio and select the ASP.NET Core Web app (Model-View-Controller) template.
![Create ASP.NET Core Web application in Visual Studio](ASP-NET-Core_images/CreateProjectforConversion.png)

Step 2: Configure your new project according to your requirements.
![Create ASP.NET Core Web application in Visual Studio](GCP_Images/Configuration_WordtoPDF.png)

Step 3: Click the **Create** button.
![Create ASP.NET Core Web application in Visual Studio](GCP_Images/Additional-Information-WordtoPDF.png)

Step 4: Install the following **Nuget packages** in your application from [Nuget.org](https://www.nuget.org/).

* [Syncfusion.DocIORenderer.Net.Core](https://www.nuget.org/packages/Syncfusion.DocIORenderer.Net.Core) 
* [SkiaSharp.NativeAssets.Linux v2.88.2](https://www.nuget.org/packages/SkiaSharp.NativeAssets.Linux/2.88.2)
* [HarfBuzzSharp.NativeAssets.Linux v2.8.2.2](https://www.nuget.org/packages/HarfBuzzSharp.NativeAssets.Linux/2.8.2.2)

 ![Install Syncfusion.DocIORenderer.Net.Core Nuget Package](Azure_Images/App_Service_Linux/Syncfusion_Nuget_Package_WordtoPDF.png)
 ![Install SkiaSharp.NativeAssets.Linux Nuget Package](Azure_Images/App_Service_Linux/SkiaSharp_Nuget-Package_WordtoPDF.png)
 ![Install HarfBuzzSharp.NativeAssets.Linux Nuget Package](Azure_Images/App_Service_Linux/HarfBuzz-Nuget-WordtoImage.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 4: Include the following namespaces in the **HomeController.cs** file.

{% tabs %}
{% highlight c# tabtitle="C#" %}

using Syncfusion.DocIO;
using Syncfusion.DocIO.DLS;
using Syncfusion.DocIORenderer;

{% endhighlight %}
{% endtabs %}

Step 5: A default action method named Index will be present in HomeController.cs. Right click on Index method and select **Go To View** where you will be directed to its associated view page **Index.cshtml**.

Step 6: Add a new button in the Index.cshtml as shown below.

{% tabs %}
{% highlight c# tabtitle="C#" %}

@{
    Html.BeginForm("ConvertWordToImage", "Home", FormMethod.Get);
    {
        <div>
            <input type="submit" value="Convert Word to image" style="width:185px;height:27px" />
        </div>
    }
    Html.EndForm();
}

{% endhighlight %}
{% endtabs %}

Step 7: Add a new action method **ConvertWordToImage** in HomeController.cs and include the below code snippet to **convert the Word document to image** and download it.

{% tabs %}
{% highlight c# tabtitle="C#" %}

using (FileStream inputStream = new FileStream(Path.GetFullPath("Data/Input.docx"), FileMode.Open, FileAccess.Read))
{
    //Creating a new document.
    using (WordDocument document = new WordDocument(inputStream, FormatType.Docx))
    {                     
        //Creates a new instance of DocIORenderer class.
        using (DocIORenderer render = new DocIORenderer())
        {
            //Converts the first page of word document to image
            imageStream = (MemoryStream)document.RenderAsImages(0, ExportImageFormat.Jpeg);
            imageStream.Position = 0;  
            //Download Word document in the browser.
            return File(imageStream, "image/jpeg", "WordToimage_Page1.jpeg");                       
        }
    }
}

{% endhighlight %}
{% endtabs %}

## Deploying the Application to App Engine

Step 1: Open the **Cloud Shell editor**.
![Cloud Shell Editor](GCP_Images/Cloud-Shell-Editor-WordtoPDF.png)

Step 2: Open the **Home Workspace** in the Cloud Shell editor.
![Open the Home Workspace](GCP_Images/Terminal-WordtoPDF.png)

N> If you have your sample application in your local machine, drag and drop it into the Workspace. If you created the sample using the Cloud Shell terminal command, it will be available in the Workspace.

Step 3: Open the terminal and run the following **command** to view the files and directories within your **current workspace** or directory.

{% tabs %}
{% highlight CLI %}

$ ls

{% endhighlight %}
{% endtabs %}

Step 4: Run the following **command** to Navigate which sample you want run.

{% tabs %}
{% highlight CLI %}

$ cd Convert-Word-Document-to-Image

{% endhighlight %}
{% endtabs %}

Step 5: Finally, **run the application** using the following command.

{% tabs %}
{% highlight CLI %}

dotnet run --urls=http://localhost:8080

{% endhighlight %}
{% endtabs %}

![Run the application using command](GCP_Images/Run-Application-Command-WordtoPDF.png)

Step 6: Verify that the application is running properly by accessing the **Web View** -> **Preview on port 8080**.
![Verify the application is running properly](GCP_Images/Web-View-WordtoPDF.png)

Step 7: Close the preview page and return to the terminal. Press **Ctrl+C** to shut down the application.

## Publishing the Application to GCP

Step 1: Run the following command in Cloud Shell to publish the application.

{% tabs %}
{% highlight CLI %}

dotnet publish -c Release

{% endhighlight %}
{% endtabs %}

![Publish the application](GCP_Images/Publish_WordtoPDF.png)

Step 2: Run the following command in Cloud Shell to Navigate to the publish folder.

{% tabs %}
{% highlight CLI %}

cd bin/Release/net6.0/publish/

{% endhighlight %}
{% endtabs %}

![Navigate to the publish folder](GCP_Images/Navigate_Publish_Folder.png)

Step 3: Add the app.yaml file to the publish folder with the following contents.

{% tabs %}
{% highlight CLI %}

$ cat <<EOT >> app.yaml
env: flex
runtime: custom   
EOT

{% endhighlight %}
{% endtabs %}

![Add required files to publish folder](GCP_Images/Docker-File-WordtoPDF.png)

Step 4: Add the Docker file to the publish folder with the following contents.

{% tabs %}
{% highlight CLI %}

$ cat <<EOT >> Dockerfile
FROM mcr.microsoft.com/dotnet/aspnet:6.0
RUN apt-get update -y && apt-get install libfontconfig -y
ADD / /app
EXPOSE 8080
ENV ASPNETCORE_URLS=http://*:8080
WORKDIR /app
ENTRYPOINT [ "dotnet", "Convert-Word-document-to-PDF.dll"]
EOT

{% endhighlight %}
{% endtabs %}

![Add required files to publish folder](GCP_Images/Deploy-to-Cloud-WordtoPDF.png)

Step 6: Run the following command in Cloud Shell to Deploy the application to cloud service.

{% tabs %}
{% highlight CLI %}

$ gcloud app deploy --version v0

{% endhighlight %}
{% endtabs %}

![Add required files to publish folder](GCP_Images/Deploy-WordtoPDF.png)

Step 8: The application is now deployed successfully.

![Add required files to publish folder](GCP_Images/Browser-WordtoPDF.png)

You can download a complete working sample from GitHub.

By executing the program, you will get the **image** as follows. The output will be saved in bin folder.

![Word to Image in GCP App Engine](WordToPDF_images/OutputImage.png)