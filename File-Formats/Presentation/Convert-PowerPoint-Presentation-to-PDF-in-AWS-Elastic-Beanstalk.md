---
title: Convert PPTX to PDF in AWS Elastic Beanstalk | Syncfusion
description: Convert PPTX to PDF in AWS Elastic Beanstalk using .NET Core PowerPoint library (Presentation) without Microsoft PowerPoint or interop dependencies.
platform: file-formats
control: PowerPoint
documentation: UG
---

# Convert PowerPoint Presentation to PDF in AWS Elastic Beanstalk

Syncfusion PowerPoint is a [.NET Core PowerPoint library](https://www.syncfusion.com/document-processing/powerpoint-framework/net-core) used to create, read, edit and **convert PowerPoint documents** programmatically without **Microsoft PowerPoint** or interop dependencies. Using this library, you can **convert a PowerPoint Presentation to PDF in AWS Elastic Beanstalk**.

## Steps to convert PowerPoint Presentation to PDF in AWS Elastic Beanstalk

Step 1: Create a new ASP.NET Core Web application (Model-View-Controller) project.

![Create ASP.NET Core Web application in Visual Studio](Azure_Images/App_Service_Linux/Create-PowerPoint-Presentation-to-PDF.png))

Step 2: Install the following **Nuget packages** in your application from [Nuget.org](https://www.nuget.org/).

* [Syncfusion.PresentationRenderer.Net.Core](https://www.nuget.org/packages/Syncfusion.PresentationRenderer.Net.Core)
* [SkiaSharp.NativeAssets.Linux.NoDependencies v2.88.2](https://www.nuget.org/packages/SkiaSharp.NativeAssets.Linux.NoDependencies/2.88.2)

![Install Syncfusion.PresentationRenderer.Net.Core NuGet Paackage](Azure_Images/App_Service_Linux/Nuget_Package_PowerPoint_Presentation_to_PDF.png)
![Install SkiaSharp.NativeAssets.Linux.NoDependencies v2.88.2 NuGet Paackage](AWS_images/Elastic_Beanstalk_Images/Nuget-Package-PPTXtoPDF.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 3: Include the following namespaces in the **HomeController.cs** file.

{% tabs %}
{% highlight c# tabtitle="C#" %}

using Syncfusion.Presentation;
using Syncfusion.PresentationRenderer;
using Syncfusion.Pdf;

{% endhighlight %}
{% endtabs %}

Step 4: A default action method named Index will be present in HomeController.cs. Right click on Index method and select **Go To View** where you will be directed to its associated view page **Index.cshtml**.

Step 5: Add a new button in the **Index.cshtml** as shown below.

{% tabs %}
{% highlight c# tabtitle="C#" %}

@{
    Html.BeginForm("ConvertPPTXtoPDF", "Home", FormMethod.Get);
    {
        <div>
            <input type="submit" value="Convert PPTX to PDF" style="width:200px;height:27px" />
        </div>
    }
    Html.EndForm();
}

{% endhighlight %}
{% endtabs %}

Step 6: Include the below code snippet in the **Homecontroller.cs** file to **convert a PowerPoint Presentation to Pdf** and download it.

{% tabs %}
{% highlight c# tabtitle="C#" %}

public ActionResult ConvertPPTXtoPDF()
{
    using (FileStream inputStream = new FileStream(Path.GetFullPath("wwwroot/Data/Input.pptx"), FileMode.Open, FileAccess.Read))
    {
        //Open the existing PPTX document.
        using (IPresentation pptxDoc = Presentation.Open(inputStream))
        {
            //Hooks the font substitution event.
            pptxDoc.FontSettings.SubstituteFont += FontSettings_SubstituteFont;
            //Converts PPTX document into PDF document.
            using (PdfDocument pdfDocument = PresentationToPdfConverter.Convert(pptxDoc))
            {
                //Saves the PDF document to MemoryStream.
                MemoryStream stream = new MemoryStream();
                pdfDocument.Save(stream);
                //Unhooks the font substitution event after converting to PDF.
                pptxDoc.FontSettings.SubstituteFont -= FontSettings_SubstituteFont;
                stream.Position = 0;
                //Download PDF document in the browser.
                return File(stream, "application/pdf", "PPTXtoPDF.pdf");
            }
        }
    }
}

//Sets the alternate font when a specified font is not installed in the production environment.
private static void FontSettings_SubstituteFont(object sender, SubstituteFontEventArgs args)
{
    if (args.OriginalFontName == "Calibri" && args.FontStyle == FontStyle.Regular)
    {
        args.AlternateFontStream = new FileStream(Path.GetFullPath("wwwroot/Fonts/calibri.ttf"), FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
    }
}

{% endhighlight %}
{% endtabs %}

## Steps to publish as AWS Elastic Beanstalk

Step 1: Right-click the project and select **Publish to AWS Elastic Beanstalk (Legacy)** option.
![Right-click the project and select the Publish option](AWS_Images/Elastic_Beanstalk_Images/Publish-Create-PowerPoint.png)

Step 2: Select the **Deployment Target** as **Create a new application environment** and click **Next** button.
![Deployment Target in AWS Ealastic Beanstalk](AWS_Images/Elastic_Beanstalk_Images/Deployment-Target-Create-PowerPoint.png)

Step 3: Choose the **Environment Name** in the dropdown list and the **URL** will be automatically assign and check the URL is available, if available click next otherwise change the **URL**. 
![Application Environment in AWS Elastic Beanstalk](AWS_Images/Elastic_Beanstalk_Images/URL-Availability-Open-and-Save-PowerPoint.png)

Step 4: Select the instance type in **t3a.micro** from the dropdown list and click next.
![Application Environment in AWS Elastic Beanstalk](AWS_Images/Elastic_Beanstalk_Images/Launch-Configuration-Create-PowerPoint.png)

Step 5: Click the **Next** button to proceed further.
![Application Environment in AWS Elastic Beanstalk](AWS_Images/Elastic_Beanstalk_Images/Permissions-Create-PowerPoint.png)

Step 6: Click the **Next** button.
![Application Options in AWS Elastic Beanstalk](AWS_Images/Elastic_Beanstalk_Images/Application-Options-Create-PowerPoint.png)

Step 7: Click the **Deploy** button to deploy the sample on AWS Elastic Beanstalk.
![Deploy the sample in AWS Elastic Beanstalk](AWS_Images/Elastic_Beanstalk_Images/Review-Create-PowerPoint.png)

Step 8: After changing the status from **Updating** to **Environment is healthy**, click the **URL**.
![Status check in AWS Elastic Beanstalk](AWS_Images/Elastic_Beanstalk_Images/Status-Create-PowerPoint.png)

Step 9: After opening the provided **URL**, click **Create PowerPoint** button to download the PowerPoint document.
![Click button to Create a PowerPoint document](AWS_Images/Elastic_Beanstalk_Images/Browse-Open-and-Save-PowerPoint.png)

You can download a complete working sample from GitHub.

By executing the program, you will get the **PDF document** as follows.

![PPTX to PDF in AWS Elastic Beanstalk](PPTXtoPDF_images/Output_PowerPoint_Presentation_to-PDF.png)

Click [here](https://www.syncfusion.com/document-processing/powerpoint-framework/net-core) to explore the rich set of Syncfusion PowerPoint Library (Presentation) features. 

An online sample link to [convert PowerPoint Presentation to PDF](https://ej2.syncfusion.com/aspnetcore/PowerPoint/PPTXToPDF#/material3) in ASP.NET Core.