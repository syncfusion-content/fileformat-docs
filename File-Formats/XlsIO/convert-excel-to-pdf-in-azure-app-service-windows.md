---
title: Convert Excel to PDF in Azure App Service on Windows | Syncfusion
description: Convert Excel to PDF in Azure App Service on Windows using .NET Core Excel library (XlsIO) without Microsoft Excel or interop dependencies.
platform: file-formats
control: XlsIO
documentation: UG
---

# Convert Excel document to PDF in Azure App Service on Windows

Syncfusion XlsIO is a [.NET Core Excel library](https://www.syncfusion.com/document-processing/excel-framework/net) used to create, read, edit and **convert Excel documents** programmatically without **Microsoft Excel** or interop dependencies. Using this library, you can **convert an Excel document to PDF in Azure App Service on Windows**.

## Steps to convert Excel document to PDF in Azure App Service on Windows

Step 1: Create a new ASP.NET Core Web Application (Model-View-Controller).
<img src="Azure_Images/App_Service_Windows/Create_Application.png" alt="Create a ASP.NET Core Web App project" width="100%" Height="Auto"/>

Step 2: Name the project.
<img src="Azure_Images/App_Service_Windows/Name_the_Application.png" alt="Name the project" width="100%" Height="Auto"/>

Step 3: Select the framework and click **Create** button.
<img src="Azure_Images/App_Service_Windows/Select_Framework.png" alt="Framework version" width="100%" Height="Auto"/>

Step 4: Install the [Syncfusion.XlsIORenderer.Net.Core](https://www.nuget.org/packages/Syncfusion.XlsIORenderer.Net.Core) NuGet package as a reference to your project from [NuGet.org](https://www.nuget.org/).
<img src="Azure_Images/App_Service_Windows/Install_NuGet.png" alt="Install Syncfusion.XlsIORenderer.Net.Core NuGet Package" width="100%" Height="Auto"/>

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

## Steps to publish as Azure App Service on Windows

Step 1: Right-click the project and select **Publish** option.
<img src="Azure_Images/App_Service_Windows/Publish.png" alt="Publish" width="100%" Height="Auto"/>

Step 2: Select the publish target as **Azure**.
<img src="Azure_Images/App_Service_Windows/Publish_Profile.png" alt="Add a Publish Profile" width="100%" Height="Auto"/>

Step 3: Select the Specific target as **Azure App Service (Windows)**.
<img src="Azure_Images/App_Service_Windows/Windows_App_Service.png" alt="Select the publish target" width="100%" Height="Auto"/>

Step 4: To create a new app service, click **Create new** option.
<img src="Azure_Images/App_Service_Windows/Create_New.png" alt="Click create new option" width="100%" Height="Auto"/>

Step 5: Click the **Create** button to proceed with **App Service** creation.
<img src="Azure_Images/App_Service_Windows/Hosting.png" alt="Hosting" width="100%" Height="Auto"/>

Step 6: Click the **Finish** button to finalize the **App Service** creation.
<img src="Azure_Images/App_Service_Windows/App_Service.png" alt="App Service" width="100%" Height="Auto"/>

Step 7: Click **Close** button.
<img src="Azure_Images/App_Service_Windows/Profile_Created.png" alt="Profile created" width="100%" Height="Auto"/>

Step 8: Click the **Publish** button.
<img src="Azure_Images/App_Service_Windows/Start_Publish.png" alt="Strat publish" width="100%" Height="Auto"/>

Step 9: Now, Publish has been succeeded.
<img src="Azure_Images/App_Service_Windows/Publish_Success.png" alt="Publish has been succeeded" width="100%" Height="Auto"/>

Step 10: Now, the published webpage will open in the browser. 
<img src="Azure_Images/App_Service_Windows/CreateDocument_Button.png" alt="Browser will open after publish" width="100%" Height="Auto"/>

Step 11: Click **Create Document** to convert the given Excel document to PDF. You will get the output **PDF** document as follows.
<img src="Azure_Images/App_Service_Windows/ExcelToPDF_AppService_Windows.png" alt="Excel to PDF in Azure App Service on Windows" width="100%" Height="Auto"/>