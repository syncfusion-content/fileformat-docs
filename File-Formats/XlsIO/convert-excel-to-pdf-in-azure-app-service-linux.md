---
title: Convert Excel to PDF in Azure App Service on Linux | Syncfusion
description: Convert Excel to PDF in Azure App Service on Linux using .NET Core Excel library (XlsIO) without Microsoft Excel or interop dependencies.
platform: file-formats
control: XlsIO
documentation: UG
---

# Convert Excel document to PDF in Azure App Service on Linux

Syncfusion XlsIO is a [.NET Core Excel library](https://www.syncfusion.com/document-processing/excel-framework/net) used to create, read, edit and **convert Excel documents** programmatically without **Microsoft Excel** or interop dependencies. Using this library, you can **convert an Excel document to PDF in Azure App Service on Linux**.

## Steps to convert Excel document to PDF in Azure App Service on Linux

Step 1: Create a new ASP.NET Core Web Application (Model-View-Controller).

![Create a ASP.NET Core Web App project in visual studio](Azure_Images/App_Service_Linux/Create_Application.png)
<img src="Azure_Images/App_Service_Linux/Create_Application.png" alt="Create a ASP.NET Core Web App project" width="100%" Height="Auto"/>

Step 2: Name the project.

![Name the project](Azure_Images/App_Service_Linux/Name_the_Application.png)
<img src="Azure_Images/App_Service_Linux/Name_the_Application.png" alt="Name the project" width="100%" Height="Auto"/>

Step 3: Select the framework and click **Create** button.

![Framework version](Azure_Images/App_Service_Linux/Select_Framework.png)
<img src="Azure_Images/App_Service_Linux/Select_Framework.png" alt="Framework version" width="100%" Height="Auto"/>

Step 4: Install the following NuGet packages as reference to your project from [NuGet.org](https://www.nuget.org/).

* [Syncfusion.XlsIORenderer.Net.Core](https://www.nuget.org/packages/Syncfusion.XlsIORenderer.Net.Core)
* [SkiaSharp.NativeAssets.Linux](https://www.nuget.org/packages/SkiaSharp.NativeAssets.Linux/2.88.2)
* [HarfBuzzSharp.NativeAssets.Linux](https://www.nuget.org/packages/HarfBuzzSharp.NativeAssets.Linux/2.8.2.3)

![Install Syncfusion.XlsIORenderer.Net.Core NuGet Package](Azure_Images/App_Service_Linux/Install_NuGet.png)
![Install SkiaSharp NuGet Package](Azure_Images/App_Service_Linux/SkiaSharp_NuGet.png)
![Install HarfBuzzSharp NuGet Package](Azure_Images/App_Service_Linux/HarfBuzzSharp_NuGet.png)
<img src="Azure_Images/App_Service_Linux/Install_NuGet.png" alt="Install Syncfusion.XlsIORenderer.Net.Core NuGet Package" width="100%" Height="Auto"/>
<img src="Azure_Images/App_Service_Linux/SkiaSharp_NuGet.png" alt="Install SkiaSharp NuGet Package" width="100%" Height="Auto"/>
<img src="Azure_Images/App_Service_Linux/HarfBuzzSharp_NuGet.png" alt="Install HarfBuzzSharp NuGet Package" width="100%" Height="Auto"/>

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your applications to use our components. 

Step 5: Add a new button in the **Index.cshtml** as shown below.
{% tabs %}  
{% highlight CSHTML %}
@{Html.BeginForm("CreateDocument", "Home", FormMethod.Get);
    {
        <div>
            <input type="submit" value="Create Document" style="width:150px;height:27px" />
        </div>
    }
    Html.EndForm();
}
{% endhighlight %}
{% endtabs %}

Step 6: Include the following namespaces in **HomeController.cs**.
{% tabs %}
{% highlight c# tabtitle="C#" %}
using Syncfusion.XlsIO;
using Syncfusion.XlsIORenderer;
using Syncfusion.Pdf;
{% endhighlight %}
{% endtabs %}

Step 7: Include the below code snippet in **HomeController.cs** to **convert an Excel document to PDF**. 
{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  FileStream excelStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIO renderer.
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert Excel document into PDF document 
  PdfDocument pdfDocument = renderer.ConvertToPDF(workbook);

  //Create the MemoryStream to save the converted PDF.      
  MemoryStream pdfStream = new MemoryStream();

  //Save the converted PDF document to MemoryStream.
  pdfDocument.Save(pdfStream);
  pdfStream.Position = 0;

  //Download PDF document in the browser.
  return File(pdfStream, "application/pdf", "Sample.pdf");
}
{% endhighlight %}
{% endtabs %}

## Steps to publish as Azure App Service on Linux

Step 1: Right-click the project and select **Publish** option.

![Publish](Azure_Images/App_Service_Linux/Publish.png)
<img src="Azure_Images/App_Service_Linux/Publish.png" alt="Publish" width="100%" Height="Auto"/>

Step 2: Select the publish target as **Azure**.

![Add a Publish Profile](Azure_Images/App_Service_Linux/Publish_Profile.png)
<img src="Azure_Images/App_Service_Linux/Publish_Profile.png" alt="Add a Publish Profile" width="100%" Height="Auto"/>

Step 3: Select the Specific target as **Azure App Service (Linux)**.

![Select the publish target](Azure_Images/App_Service_Linux/Linux_App_Service.png)
<img src="Azure_Images/App_Service_Linux/Linux_App_Service.png" alt="Select the publish target" width="100%" Height="Auto"/>

Step 4: To create a new app service, click **Create new** option.

![Click create new option](Azure_Images/App_Service_Linux/Create_New.png)
<img src="Azure_Images/App_Service_Linux/Create_New.png" alt="Click create new option" width="100%" Height="Auto"/>

Step 5: Click the **Create** button to proceed with **App Service** creation.

![Hosting](Azure_Images/App_Service_Linux/Hosting.png)
<img src="Azure_Images/App_Service_Linux/Hosting.png" alt="Hosting" width="100%" Height="Auto"/>

Step 6: Click the **Finish** button to finalize the **App Service** creation.

![App Service](Azure_Images/App_Service_Linux/App_Service.png)
<img src="Azure_Images/App_Service_Linux/App_Service.png" alt="App Service" width="100%" Height="Auto"/>

Step 7: Click **Close** button.

![Profile created](Azure_Images/App_Service_Linux/Profile_Created.png)
<img src="Azure_Images/App_Service_Linux/Profile_Created.png" alt="Profile created" width="100%" Height="Auto"/>

Step 8: Click the **Publish** button.

![Start publish](Azure_Images/App_Service_Linux/Start_Publish.png)
<img src="Azure_Images/App_Service_Linux/Start_Publish.png" alt="Strat publish" width="100%" Height="Auto"/>

Step 9: Now, Publish has been succeeded.

![Publish has been succeeded](Azure_Images/App_Service_Linux/Publish_Success.png)
<img src="Azure_Images/App_Service_Linux/Publish_Success.png" alt="Publish has been succeeded" width="100%" Height="Auto"/>

Step 10: Now, the published webpage will open in the browser. 

![Browser will open after publish](Azure_Images/App_Service_Linux/CreateDocument_Button.png)
<img src="Azure_Images/App_Service_Linux/CreateDocument_Button.png" alt="Browser will open after publish" width="100%" Height="Auto"/>

Step 11: Click **Create Document** to convert the given Excel document to PDF. You will get the output **PDF** document as follows.

![Output File](Azure_Images/App_Service_Linux/ExcelToPDF_AppService_Linux.png)
<img src="Azure_Images/App_Service_Linux/ExcelToPDF_AppService_Linux.png" alt="Excel to PDF in Azure App Service on Linux" width="100%" Height="Auto"/>

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Getting%20Started/Azure%20App%20Service/Convert-Excel-to-PDF). 

Click [here](https://www.syncfusion.com/document-processing/excel-framework/net-core) to explore the rich set of Syncfusion Excel library (XlsIO) features.

An online sample link to [convert an Excel document to PDF](https://ej2.syncfusion.com/aspnetcore/Excel/ExcelToPDF#/material3) in ASP.NET Core.
