---
title: Convert Excel to Image in Azure App Service on Linux | Syncfusion
description: Convert Excel to Image in Azure App Service on Linux using .NET Core Excel library (XlsIO) without Microsoft Excel or interop dependencies.
platform: file-formats
control: XlsIO
documentation: UG
---

# Convert Excel document to Image in Azure App Service on Linux

Syncfusion XlsIO is a [.NET Core Excel library](https://www.syncfusion.com/document-processing/excel-framework/net) used to create, read, edit and **convert Excel documents** programmatically without **Microsoft Excel** or interop dependencies. Using this library, you can **convert an Excel document to Image in Azure App Service on Linux**.

## Steps to convert Excel document to Image in Azure App Service on Linux

Step 1: Create a new ASP.NET Core Web Application (Model-View-Controller).
<img src="Azure_Images/App_Service_Linux/Create_Application.png" alt="Create a ASP.NET Core Web App project" width="100%" Height="Auto"/>

Step 2: Name the project.
<img src="Azure_Images/App_Service_Linux/Name_the_Application_Image.png" alt="Name the project" width="100%" Height="Auto"/>

Step 3: Select the framework and click **Create** button.
<img src="Azure_Images/App_Service_Linux/Select_Framework.png" alt="Framework version" width="100%" Height="Auto"/>

Step 4: Install the following NuGet packages as reference to your project from [NuGet.org](https://www.nuget.org/).

* [Syncfusion.XlsIORenderer.Net.Core](https://www.nuget.org/packages/Syncfusion.XlsIORenderer.Net.Core)
* [SkiaSharp.NativeAssets.Linux](https://www.nuget.org/packages/SkiaSharp.NativeAssets.Linux/2.88.2)
* [HarfBuzzSharp.NativeAssets.Linux](https://www.nuget.org/packages/HarfBuzzSharp.NativeAssets.Linux/2.8.2.3)

<img src="Azure_Images/App_Service_Linux/Install_NuGet_Image.png" alt="Install Syncfusion.XlsIORenderer.Net.Core NuGet Package" width="100%" Height="Auto"/>
<img src="Azure_Images/App_Service_Linux/SkiaSharp_NuGet_Image.png" alt="Install SkiaSharp NuGet Package" width="100%" Height="Auto"/>
<img src="Azure_Images/App_Service_Linux/HarfBuzzSharp_NuGet_Image.png" alt="Install HarfBuzzSharp NuGet Package" width="100%" Height="Auto"/>

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
{% endhighlight %}
{% endtabs %}

Step 7: Include the below code snippet in **HomeController.cs** to **convert an Excel document to Image**. 
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

## Steps to publish as Azure App Service on Linux

Step 1: Right-click the project and select **Publish** option.
<img src="Azure_Images/App_Service_Linux/Publish_Image.png" alt="Publish" width="100%" Height="Auto"/>

Step 2: Select the publish target as **Azure**.
<img src="Azure_Images/App_Service_Linux/Publish_Profile.png" alt="Add a Publish Profile" width="100%" Height="Auto"/>

Step 3: Select the Specific target as **Azure App Service (Linux)**.
<img src="Azure_Images/App_Service_Linux/Linux_App_Service.png" alt="Select the publish target" width="100%" Height="Auto"/>

Step 4: To create a new app service, click **Create new** option.
<img src="Azure_Images/App_Service_Linux/Create_New.png" alt="Click create new option" width="100%" Height="Auto"/>

Step 5: Click the **Create** button to proceed with **App Service** creation.
<img src="Azure_Images/App_Service_Linux/Hosting_Image.png" alt="Hosting" width="100%" Height="Auto"/>

Step 6: Click the **Finish** button to finalize the **App Service** creation.
<img src="Azure_Images/App_Service_Linux/App_Service_Image.png" alt="App Service" width="100%" Height="Auto"/>

Step 7: Click **Close** button.
<img src="Azure_Images/App_Service_Linux/Profile_Created_Image.png" alt="Profile created" width="100%" Height="Auto"/>

Step 8: Click the **Publish** button.
<img src="Azure_Images/App_Service_Linux/Start_Publish_Image.png" alt="Strat publish" width="100%" Height="Auto"/>

Step 9: Now, Publish has been succeeded.
<img src="Azure_Images/App_Service_Linux/Publish_Success_Image.png" alt="Publish has been succeeded" width="100%" Height="Auto"/>

Step 10: Now, the published webpage will open in the browser. 
<img src="Azure_Images/App_Service_Linux/CreateDocument_Button_Image.png" alt="Browser will open after publish" width="100%" Height="Auto"/>

Step 11: Click **Create Document** to convert the given Excel document to Image. You will get the output **Image** as follows.
<img src="Azure_Images/App_Service_Linux/ExcelToImage_AppService_Linux.png" alt="Excel to Image in Azure App Service on Linux" width="100%" Height="Auto"/>
