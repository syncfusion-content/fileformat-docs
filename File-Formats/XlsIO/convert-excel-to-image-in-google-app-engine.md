---
title: Convert Excel to Image in Google App Engine | Syncfusion
description: Convert Excel to Image in Google App Engine using .NET Core Excel library (XlsIO) without Microsoft Excel or interop dependencies.
platform: file-formats
control: XlsIO
documentation: UG
---

# Convert Excel document to Image in Google App Engine

Syncfusion XlsIO is a [.NET Core Excel library](https://www.syncfusion.com/document-processing/excel-framework/net-core/excel-library) used to create, read, edit and **convert Excel documents** programmatically without **Microsoft Excel** or interop dependencies. Using this library, you can **convert an Excel document to Image in Google App Engine**.

## Set up App Engine

Step 1: Open the **Google Cloud Console** and click the **Activate Cloud Shell** button.

![Activate Cloud Shell](GCP_Images/App_Engine_Getting_Started.png)

Step 2: Click the **Cloud Shell Editor** button to view the **Workspace**.

![Open Editor in Cloud Shell](GCP_Images/Activate_Cloud_Shell.png)

Step 3: Open **Cloud Shell Terminal**, run the following **command** to confirm authentication.

{% tabs %}
{% highlight c# tabtitle="CLI" %}

gcloud auth list

{% endhighlight %}
{% endtabs %}

![Authentication for App Engine](GCP_Images/Authentication.png)

Step 4: Click the **Authorize** button.

![Click Authorize button](GCP_Images/Authorize_Button.png)

## Create an application for App Engine

Step 1: Open Visual Studio and select the ASP.NET Core Web app (Model-View-Controller) template.

![Create ASP.NET Core Web application in Visual Studio](GCP_Images/CreateProject_Create_Excel.png)

Step 2: Configure your new project according to your requirements.

![Configure your project](GCP_Images/Configuration_ExceltoImage.png)

Step 3: Click the **Create** button.

![Click create button](GCP_Images/Additional_Information_Create_Excel.png)

Step 4: Install the following **Nuget packages** in your application from [Nuget.org](https://www.nuget.org/).

* [Syncfusion.XLsIORenderer.Net.Core](https://www.nuget.org/packages/Syncfusion.XlsIORenderer.Net.Core) 
* [SkiaSharp.NativeAssets.Linux v2.88.6](https://www.nuget.org/packages/SkiaSharp.NativeAssets.Linux/2.88.6)
* [HarfBuzzSharp.NativeAssets.Linux v7.3.0](https://www.nuget.org/packages/HarfBuzzSharp.NativeAssets.Linux/7.3.0)

![Install Syncfusion.XlsIORenderer.Net.Core Nuget Package](GCP_Images/Install_Nuget_Syncfusion.png)
![Install SkiaSharp.NativeAssets.Linux Nuget Package](GCP_Images/Install_Nuget_SkiaSharp.png)
![Install HarfBuzzSharp.NativeAssets.Linux Nuget Package](GCP_Images/Install_Nuget_HarfBuzzSharp.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 5: Include the following namespaces in the **HomeController.cs** file.

{% tabs %}
{% highlight c# tabtitle="C#" %}

using Syncfusion.XlsIO;
using Syncfusion.XlsIORenderer;

{% endhighlight %}
{% endtabs %}

Step 6: A default action method named Index will be present in HomeController.cs. Right click on Index method and select **Go To View** where you will be directed to its associated view page **Index.cshtml**.

Step 7: Add a new button in the Index.cshtml as shown below.

{% tabs %}
{% highlight c# tabtitle="C#" %}

@{
    Html.BeginForm("ConvertExcelToImage", "Home", FormMethod.Get);
    {
        <div>
            <input type="submit" value="Convert Excel to image" style="width:185px;height:27px" />
        </div>
    }
    Html.EndForm();
}
{% endhighlight %}
{% endtabs %}

Step 8: Add a new action method **ConvertExcelToImage** in HomeController.cs and include the below code snippet to **convert the Excel document to image** and download it.

{% tabs %}
{% highlight c# tabtitle="C#" %}

using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  FileStream excelStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(excelStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Initialize XlsIO renderer.
  application.XlsIORenderer = new XlsIORenderer();

  //Create the MemoryStream to save the image.      
  MemoryStream imageStream = new MemoryStream();

  //Save the converted image to MemoryStream.
  worksheet.ConvertToImage(worksheet.UsedRange, imageStream);
  imageStream.Position = 0;

  //Download image in the browser.
  return File(imageStream, "application/jpeg", "Sample.jpeg");
}

{% endhighlight %}
{% endtabs %}

## Move application to App Engine

Step 1: Open the **Cloud Shell editor**.

![Cloud Shell Editor](GCP_Images/Cloud_Shell_Editor.png)

Step 2: Drag and drop the sample from your local machine to **Workspace**.

![Open the Home Workspace](GCP_Images/Workspace_ExceltoImage.png)

N> If you have your sample application in your local machine, drag and drop it into the Workspace. If you created the sample using the Cloud Shell terminal command, it will be available in the Workspace.

Step 3: Open the Cloud Shell Terminal and run the following **command** to view the files and directories within your **current Workspace**.

{% tabs %}
{% highlight c# tabtitle="CLI" %}

ls

{% endhighlight %}
{% endtabs %}

![Open the Home Workspace](GCP_Images/View_File_ExceltoImage.png)

Step 4: Run the following **command** to navigate which sample you want run.

{% tabs %}
{% highlight c# tabtitle="CLI" %}

cd Convert-Excel-to-Image

{% endhighlight %}
{% endtabs %}

![Open the Home Workspace](GCP_Images/Navigate_ExceltoImage.png)

Step 5: To ensure that the sample is working correctly, please run the application using the following command.

{% tabs %}
{% highlight c# tabtitle="CLI" %}

dotnet run --urls=http://localhost:8080

{% endhighlight %}
{% endtabs %}

![Run the application using command](GCP_Images/Run_Application_Command_ExceltoImage.png)

Step 6: Verify that the application is running properly by accessing the **Web View** -> **Preview on port 8080**.

![Verify the application is running properly](GCP_Images/Web_View_ExceltoImage.png)

Step 7: Now you can see the sample output on the preview page.

![Sample output in browser](GCP_Images/Ensure_Sample_ExceltoImage.png)

Step 8: Close the preview page and return to the terminal then press **Ctrl+C** for which will typically stop the process.

![Close the preview page](GCP_Images/Stop_Process_ExceltoImage.png)

## Publish the application

Step 1: Run the following command in **Cloud Shell Terminal** to publish the application.

{% tabs %}
{% highlight c# tabtitle="CLI" %}

dotnet publish -c Release

{% endhighlight %}
{% endtabs %}

![Publish the application](GCP_Images/Publish_ExceltoImage.png)

Step 2: Run the following command in **Cloud Shell Terminal** to navigate to the publish folder.
{% tabs %}
{% highlight c# tabtitle="CLI" %}

cd bin/Release/net6.0/publish/

{% endhighlight %}
{% endtabs %}

![Publish the application](GCP_Images/Navigate_Publish_Folder_ExceltoImage.png)

## Configure app.yaml and docker file

Step 1: Add the app.yaml file to the publish folder with the following contents.

{% tabs %}
{% highlight c# tabtitle="CLI" %}

cat <<EOT >> app.yaml
env: flex
runtime: custom   
EOT

{% endhighlight %}
{% endtabs %}

![Add required files to publish folder](GCP_Images/Yaml_File_ExceltoImage.png)

Step 2: Add the Docker file to the publish folder with the following contents.

{% tabs %}
{% highlight c# tabtitle="CLI" %}

cat <<EOT >> Dockerfile
FROM mcr.microsoft.com/dotnet/aspnet:6.0
RUN apt-get update -y && apt-get install libfontconfig -y
ADD / /app
EXPOSE 8080
ENV ASPNETCORE_URLS=http://*:8080
WORKDIR /app
ENTRYPOINT [ "dotnet", "Convert-Excel-to-Image.dll"]
EOT

{% endhighlight %}
{% endtabs %}


![Add required files to publish folder](GCP_Images/Docker_File_ExceltoImage.png)

Step 3: You can ensure **Docker** and **app.yaml** files are added in **Workspace**.

![Add required files to publish folder](GCP_Images/Check_Yaml_Docker_ExceltoImage.png)

## Deploy to App Engine

Step 1: To deploy the application to the App Engine, run the following command in Cloud Shell Terminal. Afterwards, retrieve the **URL** from the Cloud Shell Terminal.

{% tabs %}
{% highlight c# tabtitle="CLI" %}

gcloud app deploy --version v0

{% endhighlight %}
{% endtabs %}

!["Add required files to publish folder](GCP_Images/Deploy_ExceltoImage.png)

Step 2: Open the **URL** to access the application, which has been successfully deployed.

!["Add required files to publish folder](GCP_Images/Browse_ExceltoImage.png)

A complete working example of how to convert an Excel document to Image in GCP is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Getting%20Started/ASP.NET%20Core/Convert%20Excel%20to%20Image).

By executing the program, you will get the **image** as follows. The output will be saved in **bin** folder.

![Excel to Image in Google App Engine](GCP_Images/Output_ExceltoImage.png)

Click [here](https://www.syncfusion.com/document-processing/excel-framework/net-core) to explore the rich set of Syncfusion Excel library (XlsIO) features.

An online sample link to [convert an Excel document to Image](https://ej2.syncfusion.com/aspnetcore/Excel/WorksheetToImage#/material3) in ASP.NET Core.