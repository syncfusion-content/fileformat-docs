---
title: Open and save Presentation in Google App Engine | Syncfusion
description: Open and save Presentation in Google App Engine using .NET Core PowerPoint library (Presentation) without Microsoft PowerPoint or interop dependencies.
platform: file-formats
control: PowerPoint
documentation: UG
---

# Open and save Presentation in Google App Engine

Syncfusion PowerPoint is a [.NET Core PowerPoint library](https://www.syncfusion.com/document-processing/powerpoint-framework/net-core) used to create, read, edit and convert PowerPoint documents programmatically without **Microsoft PowerPoint** or interop dependencies. Using this library, you can **open and save a Presentation in Google App Engine**.

## Set up App Engine

Step 1: Open the **Google Cloud Console** and click the **Activate Cloud Shell** button.
![Activate Cloud Shell](GCP_Images/Activate-Cloud-Shell-PowerPoint-Presentation-to-PDF.png)

Step 2: Click the **Cloud Shell Editor** button to view the **Workspace**.
![Open Editor in Cloud Shell](GCP_Images/Authentication-PowerPoint-Presentation-to-PDF.png)

Step 3: Open **Cloud Shell Terminal**, run the following **command** to confirm authentication.

{% tabs %}
{% highlight c# tabtitle="CLI" %}

gcloud auth list

{% endhighlight %}
{% endtabs %}

![Authentication for App Engine](GCP_Images/Editor-Button-PowerPoint-Presentation-to-PDF.png)

Step 4: Click the **Authorize** button.
![Click Authorize button](GCP_Images/Authorize-PowerPoint-Presentation-to-PDF.png)

## Create an application for App Engine

Step 1: Open Visual Studio and select the ASP.NET Core Web app (Model-View-Controller) template.
![Create ASP.NET Core Web application in Visual Studio](GCP_Images/Create-PowerPoint-Presentation-to-PDF.png)

Step 2: Configure your new project according to your requirements.
![Create ASP.NET Core Web application in Visual Studio](GCP_Images/Configure-Open-and-Save-PowerPoint-Presentation.png)

Step 3: Click the **Create** button.
![Create ASP.NET Core Web application in Visual Studio](GCP_Images/Additional-Information-PowerPoint-Presentation-to-PDF.png)

Step 4: Install the [Syncfusion.Presentation.Net.Core](https://www.nuget.org/packages/Syncfusion.Presentation.Net.Core) NuGet package as a reference to your project from [NuGet.org](https://www.nuget.org/).
![Install Syncfusion.Presentation.Net.Core NuGet package](GCP_Images/Nuget-Package-Create-PowerPoint-Presentation.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 5: Include the following namespaces in the **HomeController.cs** file.

{% tabs %}
{% highlight c# tabtitle="C#" %}

using Syncfusion.Presentation;

{% endhighlight %}
{% endtabs %}

Step 6: A default action method named Index will be present in HomeController.cs. Right click on Index method and select **Go To View** where you will be directed to its associated view page **Index.cshtml**.

Step 7: Add a new button in the Index.cshtml as shown below.

{% tabs %}
{% highlight c# tabtitle="C#" %}

@{
    Html.BeginForm("OpenAndSavePowerPoint", "Home", FormMethod.Get);
    {
        <div>
            <input type="submit" value="Open and Save PowerPoint" style="width:220px;height:27px" />
        </div>
    }
    Html.EndForm();
}


{% endhighlight %}
{% endtabs %}

Step 8: Add a new action method **OpenAndSavePowerPoint** in HomeController.cs and include the below code snippet to **open and save PowerPoint document**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

using FileStream fileStreamPath = new(Path.GetFullPath(@"Data/Template.pptx"), FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
//Open an existing PowerPoint presentation.
using IPresentation pptxDoc = Presentation.Open(fileStreamPath);

{% endhighlight %}
{% endtabs %}

Step 9: Add below code snippet demonstrates accessing a shape from a slide and changing the text within it.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Get the first slide from the PowerPoint presentation.
ISlide slide = pptxDoc.Slides[0];
//Get the first shape of the slide.
IShape shape = slide.Shapes[0] as IShape;
//Change the text of the shape.
if (shape.TextBody.Text == "Company History")
    shape.TextBody.Text = "Company Profile";

{% endhighlight %}
{% endtabs %}

Step 10: Add below code example to **save the PowerPoint Presentation**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Save the PowerPoint Presentation as stream.
MemoryStream pptxStream = new();
pptxDoc.Save(pptxStream);
pptxStream.Position = 0;
//Download Powerpoint document in the browser.
return File(pptxStream, "application/powerpoint", "Result.pptx");

{% endhighlight %}
{% endtabs %}

## Move application to App Engine

Step 1: Open the **Cloud Shell editor**.
![Cloud Shell Editor](GCP_Images/Cloud-Shell-Editor-PowerPoint-Presentation-to-PDF.png)

Step 2: Drag and drop the sample from your local machine to **Workspace**.
![Open the Home Workspace](GCP_Images/Terminal-Open-and-Save-PowerPoint-Presentation.png)

N> If you have your sample application in your local machine, drag and drop it into the Workspace. If you created the sample using the Cloud Shell terminal command, it will be available in the Workspace.

Step 3: Open the Cloud Shell Terminal and run the following **command** to view the files and directories within your **current Workspace**.

{% tabs %}
{% highlight c# tabtitle="CLI" %}

$ ls

{% endhighlight %}
{% endtabs %}

![View the files and directories](GCP_Images/View-Files-Open-and-Save-PowerPoint-Presentation.png)

Step 4: Run the following **command** to navigate which sample you want run.

{% tabs %}
{% highlight c# tabtitle="CLI" %}

$ cd Open-and-save-PowerPoint-Presentation

{% endhighlight %}
{% endtabs %}

![Navigate which sample you want run](GCP_Images/Navigate-Open-and-Save-PowerPoint-Presentation.png)

Step 5: To ensure that the sample is working correctly, please run the application using the following command.

{% tabs %}
{% highlight c# tabtitle="CLI" %}

dotnet run --urls=http://localhost:8080

{% endhighlight %}
{% endtabs %}

![Run the application using command](GCP_Images/Run-Application-Command-Open-and-Save-PowerPoint-Presentation.png)

Step 6: Verify that the application is running properly by accessing the **Web View** -> **Preview on port 8080**.
![Verify the application is running properly](GCP_Images/Web-View-Open-and-Save-PowerPoint-Presentation.png)

Step 7: Now you can see the sample output on the preview page.
![Sample output in browser](GCP_Images/Ensure-Open-and-Save-PowerPoint-Presentation.png)

Step 8: Close the preview page and return to the terminal then press **Ctrl+C** for which will typically stop the process.
![Stop the process in terminal](GCP_Images/Close-Process-Open-and-Save-PowerPoint-Presentation.png)

## Publish the application

Step 1: Run the following command in **Cloud Shell Terminal** to publish the application.

{% tabs %}
{% highlight c# tabtitle="CLI" %}

dotnet publish -c Release

{% endhighlight %}
{% endtabs %}

![Publish the application](GCP_Images/Publish-Open-and-Save-PowerPoint-Presentation.png)

Step 2: Run the following command in **Cloud Shell Terminal** to navigate to the publish folder.
{% tabs %}
{% highlight c# tabtitle="CLI" %}

cd bin/Release/net6.0/publish/

{% endhighlight %}
{% endtabs %}

![Navigate to the publish folder](GCP_Images/Navigate-Publish-Folder-Open-and-Save-PowerPoint-Presentation.png)

## Configure app.yaml and docker file

Step 1: Add the app.yaml file to the publish folder with the following contents.

{% tabs %}
{% highlight c# tabtitle="CLI" %}

$ cat <<EOT >> app.yaml
env: flex
runtime: custom   
EOT

{% endhighlight %}
{% endtabs %}

![Add required files to publish folder](GCP_Images/Yaml-File-Open-and-Save-PowerPoint-Presentation.png)

Step 2: Add the Docker file to the publish folder with the following contents.

{% tabs %}
{% highlight c# tabtitle="CLI" %}

$ cat <<EOT >> Dockerfile
FROM mcr.microsoft.com/dotnet/aspnet:6.0
RUN apt-get update -y && apt-get install libfontconfig -y
ADD / /app
EXPOSE 8080
ENV ASPNETCORE_URLS=http://*:8080
WORKDIR /app
ENTRYPOINT [ "dotnet", "Open-and-save-PowerPoint-Presentation.dll"]
EOT

{% endhighlight %}
{% endtabs %}

![Add required files to publish folder](GCP_Images/Docker-File-Open-and-Save-PowerPoint-Presentation.png)

Step 3: You can ensure **Docker** and **app.yaml** files are added in **Workspace**.
![Add required files to publish folder](GCP_Images/Ensure-Files-Open-and-Save-PowerPoint-Presentation.png)

## Deploy to App Engine

Step 1: To deploy the application to the App Engine, run the following command in Cloud Shell Terminal. Afterwards, retrieve the **URL** from the Cloud Shell Terminal.

{% tabs %}
{% highlight c# tabtitle="CLI" %}

$ gcloud app deploy --version v1

{% endhighlight %}
{% endtabs %}

![Add required files to publish folder](GCP_Images/Deploy-Open-and-Save-PowerPoint-Presentation.png)

Step 2: Open the **URL** to access the application, which has been successfully deployed.
![Add required files to publish folder](GCP_Images/Browser-Open-and-Save-PowerPoint-Presentation.png)

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Convert-Word-document-to-PDF/GCP/Google-App-Engine).

By executing the program, you will get the **PowerPoint document** as follows. The output will be saved in **bin** folder.

![Open and Save a Presentation in Google App Engine](GCP_Images/Output-Create-PowerPoint-Presentation.png)
