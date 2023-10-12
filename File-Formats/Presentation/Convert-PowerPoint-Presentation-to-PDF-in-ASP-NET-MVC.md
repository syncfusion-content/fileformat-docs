---
title: Convert PowerPoint to PDF in ASP.NET MVC | Syncfusion
description: Convert PowerPoint to PDF in ASP.NET MVC using .NET PowerPoint library (Presentation) without Microsoft PowerPoint or interop dependencies.
platform: file-formats
control: PowerPoint
documentation: UG
---

# Convert PowerPoint to PDF in ASP.NET MVC

Syncfusion PowerPoint is a [.NET PowerPoint library](https://www.syncfusion.com/document-processing/powerpoint-framework/net) used to create, read, edit and convert PowerPoint presentation programmatically without **Microsoft PowerPoint** or interop dependencies. Using this library, you can **convert a PowerPoint to PDF in ASP.NET MVC**.

## Steps to convert PowerPoint to PDF programmatically

Step 1: Create a new C# ASP.NET MVC application project.

![Create ASP.NET MVC project](Workingwith_MVC/Project-Open-and-Save.png)

Step 2: Select the **MVC** template to create the project.

![Select MVC template](Workingwith_MVC/MVC-Open-and-Save.png)

Step 3: Install the [Syncfusion.PresentationToPdfConverter.AspNet.Mvc5](https://www.nuget.org/packages/Syncfusion.PresentationToPdfConverter.AspNet.Mvc5) NuGet package as reference to your .NET Standard applications from [NuGet.org](https://www.nuget.org/).

![Install Syncfusion.PresentationToPdfConverter.AspNet.Mvc5 Nuget Package](Workingwith_MVC/Nuget-Open-and-Save.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 4: Include the following namespace in that **HomeController.cs** file.

{% tabs %}
{% highlight c# tabtitle="C#" %}

using Syncfusion.Presentation;
using Syncfusion.PresentationToPdfConverter;
using Syncfusion.Pdf;

{% endhighlight %}
{% endtabs %}

Step 5: A default action method named **Index** will be present in HomeController.cs. Right click on this action method and select **Go To View** where you will be directed to its associated view page **Index.cshtml**.

Step 6: Add a new button in the Index.cshtml as shown below.

{% tabs %}
{% highlight HTML %}

@{
    Html.BeginForm("ConvertPPTXtoPDF", "Home", FormMethod.Get);
    {
        <br />
        <div>
            <input type="submit" value="Convert PPTX to PDF" style="width:200px;height:27px" />
        </div>
    }
    Html.EndForm();
}

{% endhighlight %}
{% endtabs %}

Step 7: Add a new action method **ConvertPPTXtoPDF** in HomeController.cs and include the below code snippet to **convert a PowerPoint to PDF in ASP.NET MVC**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Open the file as Stream
using (FileStream pathStream = new FileStream(Server.MapPath("~/App_Data/Input.pptx"), FileMode.Open, FileAccess.Read))
{
    //Opens a PowerPoint Presentation
    using (IPresentation pptxDoc = Presentation.Open(pathStream))
    {     
        //Converts the PowerPoint Presentation into PDF document
        using (PdfDocument pdfDocument = PresentationToPdfConverter.Convert(pptxDoc))
        {
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/PPTX-to-PDF-conversion/Convert-PowerPoint-presentation-to-PDF/ASP.NET-MVC)

By executing the program, you will get the **PDF** as follows.

![Converted PDF from PowerPoint in ASP.NET MVC](PPTXtoPDF_images/Output_PowerPoint_Presentation_to-PDF.png)

Click [here](https://www.syncfusion.com/document-processing/powerpoint-framework/net) to explore the rich set of Syncfusion PowerPoint Library (Presentation) features.

An online sample link to [convert PowerPoint Presentation to PDF](https://ej2.syncfusion.com/aspnetmvc/PowerPoint/PPTXToPdf#/material3) in ASP.NET MVC 