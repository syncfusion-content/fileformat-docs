---
title: Convert PowerPoint to PDF in ASP.NET Core | Syncfusion
description: Convert PowerPoint to PDF in ASP.NET Core using .NET Core PowerPoint library (Presentation) without Microsoft PowerPoint or interop dependencies.
platform: file-formats
control: PowerPoint
documentation: UG
---

# Convert PowerPoint to PDF in ASP.NET Core

Syncfusion PowerPoint is a [.NET Core PowerPoint library](https://www.syncfusion.com/document-processing/powerpoint-framework/net-core) used to create, read, edit and **convert PowerPoint presentation** programmatically without **Microsoft PowerPoint** or interop dependencies. Using this library, you can **convert a PowerPoint to PDF in ASP.NET Core**.

## Steps to convert PowerPoint to PDF programmatically

Step 1: Create a new C# ASP.NET Core web application project.

![Create ASP.NET Core Web project for PowerPoint file](Workingwith_Core/Create-Project-Open-and-Save.png)

Step 2: Install the [Syncfusion.PresentationRenderer.Net.Core](https://www.nuget.org/packages/Syncfusion.PresentationRenderer.Net.Core) NuGet package as reference to your .NET Standard applications from [NuGet.org](https://www.nuget.org/).

![Install Syncfusion.PresentationRenderer.Net.Core Nuget Package](Azure_Images/App_Service_Linux/Nuget_Package_PowerPoint_Presentation_to_PDF.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.
Step 3: Include the following namespaces in **HomeController.cs**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

using Syncfusion.Presentation;
using Syncfusion.PresentationRenderer;
using Syncfusion.Pdf;

{% endhighlight %}
{% endtabs %}

Step 4: A default action method named Index will be present in **HomeController.cs**. Right click on Index method and select **Go To View** where you will be directed to its associated view page **Index.cshtml**.

Step 5: Add a new button in the **Index.cshtml** as shown below.

{% tabs %}
{% highlight HTML %}

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

Step 6: Add a new action method **ConvertPPTXtoPDF** in HomeController.cs and include the below code snippet to **convert a PowerPoint to PDF in ASP.NET Core**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Open the file as Stream
using (FileStream fileStream = new FileStream(Path.GetFullPath("Data/Input.pptx"), FileMode.Open, FileAccess.Read))
{
    //Open the existing PowerPoint presentation with loaded stream.
    using (IPresentation pptxDoc = Presentation.Open(fileStream))
    {
        //Convert the PowerPoint presentation to PDF document.
        using (PdfDocument pdfDocument = PresentationToPdfConverter.Convert(pptxDoc))
        {
            //Create the MemoryStream to save the converted PDF.      
            MemoryStream pdfStream = new MemoryStream();
            //Save the converted PDF document to MemoryStream.
            pdfDocument.Save(pdfStream);
            pdfStream.Position = 0;
            //Download PDF document in the browser.
            return File(pdfStream, "application/pdf", "Sample.pdf");
        }
    }
}

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/PPTX-to-PDF-conversion/Convert-PowerPoint-presentation-to-PDF/ASP.NET-Core).

By executing the program, you will get the **PDF document** as follows.

![Converted PDF from PowerPoint in ASP.NET Core](PPTXtoPDF_images/Output_PowerPoint_Presentation_to-PDF.png)

Click [here](https://www.syncfusion.com/document-processing/powerpoint-framework/net-core) to explore the rich set of Syncfusion PowerPoint Library (Presentation) features. 

An online sample link to [convert PowerPoint Presentation to PDF](https://ej2.syncfusion.com/aspnetcore/PowerPoint/PPTXToPDF#/material3) in ASP.NET Core. 