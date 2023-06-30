---
title: Convert Word to PDF in GCP App Engine | Syncfusion
description: Convert Word to PDF in GCP App Engine using .NET Core Word (DocIO) library without Microsoft Word or interop dependencies.
platform: file-formats
control: DocIO
documentation: UG
---

# Convert Word to PDF in GCP App Engine

Syncfusion DocIO is a [.NET Core Word library](https://www.syncfusion.com/document-processing/word-framework/net-core/word-library) that allows you to create, read, edit, and **convert Word documents** programmatically, without the need for **Microsoft Word** or interop dependencies. In this guide, we will explore how to use Syncfusion DocIO to **convert Word document to PDF in Google Cloud Platform (GCP) App Engine**.

## Setting Up App Engine

Step 1: Click the **Activate Cloud Shell** button.
![Activate Cloud Shell](GCP_Images/Activate-Cloud-Shell-WordtoPDF.png)

Step 2: In the Cloud Shell editor, run the following **command** to confirm authentication.
```
gcloud auth list
```
![Authentication for App Engine](GCP_Images/Authentication-WordtoPDF.png)

Step 3: Click the **Authorize** button.
![Click Authorize button](GCP_Images/Authorize-WordtoPDF.png)

Step 4: Click the **Open editor** button.
![Open Editor in Cloud Shell](GCP_Images/Editor-Button-WordtoPDF.png)

## Creating a Sample Application Using Visual Studio

Step 1: Open Visual Studio and select the ASP.NET Core Web app (Model-View-Controller) template.
![Create ASP.NET Core Web application in Visual Studio](ASP-NET-Core_images/CreateProjectforConversion.png)

Step 2: Configure your new project according to your requirements.
![Create ASP.NET Core Web application in Visual Studio](GCP_Images/Configuration_WordtoPDF.png)

Step 3: Click the **Create** button.
![Create ASP.NET Core Web application in Visual Studio](GCP_Images/Additional-Information-WordtoPDF.png)

Step 4: Install the [Syncfusion.DocIORenderer.Net.Core](https://www.nuget.org/packages/Syncfusion.DocIORenderer.Net.Core) NuGet package as a reference to your project from [NuGet.org](https://www.nuget.org/).

![Install DocIO .NET Core NuGet package](ASP-NET-Core_images/NugetPackage.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 4: Include the following namespaces in the **HomeController.cs** file.

{% tabs %}
{% highlight c# tabtitle="C#" %}

using Syncfusion.DocIO;
using Syncfusion.DocIO.DLS;
using Syncfusion.DocIORenderer;
using Syncfusion.Pdf;

{% endhighlight %}
{% endtabs %}

Step 5: A default action method named Index will be present in HomeController.cs. Right click on Index method and select **Go To View** where you will be directed to its associated view page **Index.cshtml**.

Step 6: Add a new button in the Index.cshtml as shown below.

{% tabs %}
{% highlight c# tabtitle="C#" %}

@{Html.BeginForm("ConvertWordtoPDF", "Home", FormMethod.Get);
{
<div>
    <input type="submit" value="Convert Word Document to PDF" style="width:220px;height:27px" />
</div>
}
Html.EndForm();
}

{% endhighlight %}
{% endtabs %}

Step 7: Add a new action method **ConvertWordDocumentToPdf** in HomeController.cs and include the below code snippet to **convert the Word document to Pdf** and download it.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Open the file as Stream
using (FileStream docStream = new FileStream(Path.GetFullPath("Data/Template.docx"), FileMode.Open, FileAccess.Read))
{
    //Loads file stream into Word document
    using (WordDocument wordDocument = new WordDocument(docStream, FormatType.Automatic))
    {
        //Instantiation of DocIORenderer for Word to PDF conversion
        using (DocIORenderer render = new DocIORenderer())
        {
            //Converts Word document into PDF document
            PdfDocument pdfDocument = render.ConvertToPDF(wordDocument);

            //Saves the PDF document to MemoryStream.
            MemoryStream stream = new MemoryStream();
            pdfDocument.Save(stream);
            stream.Position = 0;

            //Download PDF document in the browser.
            return File(stream, "application/pdf", "Sample.pdf");
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

Step 3: Open the terminal and run the following **command** to navigate to the sample application folder.
```
Open the terminal,
$ ls
This will show the list of files and folders in workspace. Navigate to which sample you want run.
$ cd Convert-Word-Document-to-PDF
```

Step 4: Finally, **run the application** using the following command.
```
dotnet run --urls=http://localhost:8080
```
![Run the application using command](GCP_Images/Run-Application-Command-WordtoPDF.png)

Step 5: Verify that the application is running properly by accessing the **Web View** -> **Preview on port 8080**.
![Verify the application is running properly](GCP_Images/Web-View-WordtoPDF.png)

Step 6: Close the preview page and return to the terminal. Press **Ctrl+C** to shut down the application.

## Publishing the Application to GCP

Step 1: Run the following command in Cloud Shell to publish the application.
```
dotnet publish -c Release
```
![Publish the application](GCP_Images/Publish_WordtoPDF.png)

Step 2: Run the following command in Cloud Shell to Navigate to the publish folder.
```
cd bin/Release/net6.0/publish/
```
![Navigate to the publish folder](GCP_Images/Navigate_Publish_Folder.png)

Step 3: Add the app.yaml file to the publish folder with the following contents.
```
$ cat <<EOT >> app.yaml
env: flex
runtime: custom   
EOT
```
![Add required files to publish folder](GCP_Images/Docker-File-WordtoPDF.png)

Step 4: Add the Docker file to the publish folder with the following contents.
```
$ cat <<EOT >> Dockerfile
FROM mcr.microsoft.com/dotnet/aspnet:6.0
ADD / /app
EXPOSE 8080
ENV ASPNETCORE_URLS=http://*:8080
WORKDIR /app
ENTRYPOINT [ "dotnet", "Convert-Word-document-to-PDF.dll"]
EOT
```
![Add required files to publish folder](GCP_Images/Deploy-to-Cloud-WordtoPDF.png)

Step 5: Add the following command to the Dockerfile to install the libfontconfig package.
```
RUN apt-get update -y && apt-get install libfontconfig -y
```
![Add required files to publish folder](GCP_Images/Libfontconfig-WordtoPDF.png)

Step 6: Run the following command in Cloud Shell to Deploy the application to cloud service.
```
$ gcloud app deploy --version v0
```
![Add required files to publish folder](GCP_Images/Deploy-WordtoPDF.png)

Step 7: Run the following command in Cloud Shell to redeploy the updated application.
```
gcloud app deploy --version v1
```

Step 8: The application is now deployed successfully.
![Add required files to publish folder](GCP_Images/Libfontconfig-WordtoPDF.png)