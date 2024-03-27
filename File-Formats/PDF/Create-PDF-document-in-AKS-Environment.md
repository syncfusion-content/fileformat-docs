---
title: Create PDF document in AKS Environment | Syncfusion
description: Create PDF document in AKS Environment  using .NET PDF library without the dependency of Adobe Acrobat.
platform: file-formats
control: PDF
documentation: UG
---

# Create PDF document in AKS Environment 

The [Syncfusion .NET Core PDF library](https://www.syncfusion.com/document-processing/pdf-framework/net-core) is used to create, read, edit PDF documents programmatically without the dependency of Adobe Acrobat. Using this library, you can **create PDF document in AKS Environment**.

## Steps to create PDF document in AKS Environment 

Step 1: Create a new ASP.NET Core Web App (Model-View-Controller).
![Create a ASP.NET Core Web App project](AKS_images/Create-net-core-web-app.png)

Step 2: Create a project name and select the location.
![Configure your new project](AKS_images/Set_project_name.png)

Step 3: Click **Create** button.
![Additional Information](AKS_images/Sample_addition_information.png)

Step 4: Install the [Syncfusion.Pdf.Net.Core](https://www.nuget.org/packages/Syncfusion.Pdf.Net.Core/) NuGet package as a reference to your project from [NuGet.org](https://www.nuget.org/).
![Install Syncfusion.Pdf.Net.Core NuGet package](AKS_images/NuGet_package.png)


Step 5: A default action method named Index will be present in *HomeController.cs*. Right click on Index method and select Go To View where you will be directed to its associated view page *Index.cshtml*. Add a new button in the *Index.cshtml* as shown below.

{% tabs %}

{% highlight c# tabtitle="C#" %}

@{
    Html.BeginForm("CreatePDFDocument", "Home", FormMethod.Get);
    {
        <div>
            <input type="submit" value="Create PDF Document" style="width:200px;height:27px" />
        </div>
    }
    Html.EndForm();
}

{% endhighlight %}

{% endtabs %}

Step 6: Include the following namespaces in *HomeController.cs*.

{% tabs %}

{% highlight c# tabtitle="C#" %}

using Syncfusion.Pdf.Graphics;
using Syncfusion.Pdf;
using System.Diagnostics;
using Syncfusion.Drawing;

{% endhighlight %}

{% endtabs %}

Step 7: Add a new action method named CreatePDFDocument in HomeController.cs file and include the below code example to generate a PDF document in *HomeController.cs*. 

{% tabs %}

{% highlight c# tabtitle="C#" %}

    public IActionResult CreatePDFDocument()
    {
        //Create a new PDF document.
        PdfDocument document = new PdfDocument();
        //Add a page to the document.
        PdfPage page = document.Pages.Add();
        //Create PDF graphics for the page.
        PdfGraphics graphics = page.Graphics;
        //Set the standard font.
        PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);
        //Draw the text.
        graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));
        //Saving the PDF to the MemoryStream.
        MemoryStream stream = new MemoryStream();
        document.Save(stream);
        //Set the position as '0'.
        stream.Position = 0;
        //Download the PDF document in the browser.
        FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");
        fileStreamResult.FileDownloadName = "Sample.pdf";
        return fileStreamResult;
    }

{% endhighlight %}

{% endtabs %}

## Steps to publish as AKS Environment

Step 1: Right-click the project and select Publish option.
![Right-click the project and select the Publish option](AKS_images/Click_publish_button.png)

Step 2: Select the publish target as **Docker Contain Registry**.
![Select the publish target as Azure](AKS_images/Target.png)

Step 3: Select the Specific target as **Azure Contain Registry**.
![Select the publish target](AKS_images/Specific_target.png)

Step 4: To create a new app service, click **Create new** option.
![Click create new option](AKS_images/Create_new_app_service.png)

Step 5: Click the **Create** button to proceed with **Azure Contain Registry** creation.
![Click the Create button](AKS_images/Host_plan.png)

Step 6: Click the **Finish** button to finalize the **Azure Contain Registry** creation.
![Click the Finish button](AKS_images/Azure_contain_registry_finish.png)

Step 7: Click **Close** button.
![Create a ASP.NET Core Project](AKS_images/Publish_profile_creation_progress.png)

Step 8: Click the **Publish** button.
![Click the Publish button](AKS_images/Ready_to_publish_window.png)

Step 9: Now, Publish has been succeeded.
![Publish has been succeeded](AKS_images/Successful_publish.png)

Step 10: Now, the published webpage will open in the **browser**.
![Browser will open after publish](AKS_images/WebView.png)

Step 11: Select the PDF document and Click **Create PDF document** to generate the PDF document.You will get the output **PDF document** as follows.
![Create PDF document in Azure App Service on Linux](AKS_images/Output.png)

You can download a complete working sample from [GitHub]().

Click [here](https://www.syncfusion.com/document-processing/pdf-framework/net-core) to explore the rich set of Syncfusion PDF library features. 

An online sample link to [create PDF document](https://ej2.syncfusion.com/aspnetcore/PDF/HelloWorld#/material3) in ASP.NET Core. 