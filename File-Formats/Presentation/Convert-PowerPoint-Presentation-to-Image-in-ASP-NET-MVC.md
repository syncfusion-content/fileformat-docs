---
title: Convert PowerPoint to Image in ASP.NET MVC | Syncfusion
description: Convert PowerPoint to image in ASP.NET MVC using .NET PowerPoint library (Presentation) without Microsoft PowerPoint or interop dependencies.
platform: file-formats
control: PowerPoint
documentation: UG
---

# Convert PowerPoint to Image in ASP.NET MVC

Syncfusion PowerPoint is a [.NET PowerPoint library](https://www.syncfusion.com/document-processing/powerpoint-framework/net) used to create, read, edit and convert PowerPoint documents programmatically without **Microsoft PowerPoint** or interop dependencies. Using this library, you can **convert a PowerPoint to image in ASP.NET MVC**.

## Steps to convert PowerPoint to Image programmatically

Step 1: Create a new C# ASP.NET MVC application project.

![Create ASP.NET MVC project](Workingwith_MVC/Project-Open-and-Save.png)

Step 2: Select the **MVC** template to create the project.

![Select MVC template](Workingwith_MVC/MVC-Open-and-Save.png)

Step 3: Install the [Syncfusion.Presentation.AspNet.Mvc5](https://www.nuget.org/packages/Syncfusion.Presentation.AspNet.Mvc5) NuGet package as reference to your .NET Standard applications from [NuGet.org](https://www.nuget.org/).

![Install Syncfusion.Presentation.AspNet.Mvc5 Nuget Package](Workingwith_MVC/Nuget-Package-PPTXtoImage.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 4: Include the following namespace in that **HomeController.cs** file.

{% tabs %}
{% highlight c# tabtitle="C#" %}

using Syncfusion.Presentation;

{% endhighlight %}
{% endtabs %}

Step 5: A default action method named **Index** will be present in HomeController.cs. Right click on this action method and select **Go To View** where you will be directed to its associated view page **Index.cshtml**.

Step 6: Add a new button in the Index.cshtml as shown below.

{% tabs %}
{% highlight HTML %}

@{
    Html.BeginForm("ConvertPPTXtoImage", "Home", FormMethod.Get);
    {
        <div>
            <input type="submit" value="Convert PPTX to Image" style="width:200px;height:27px" />
        </div>
    }
    Html.EndForm();
}

{% endhighlight %}
{% endtabs %}

Step 7: Add the below code snippet in **HomeController.cs** to **convert a PowerPoint to image in ASP.NET MVC**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

public void ConvertPPTXtoImage()
{
    //Open the file as Stream.
    using (FileStream pathStream = new FileStream(Server.MapPath("~/App_Data/Input.pptx"), FileMode.Open, FileAccess.Read))
    {
        //Opens a PowerPoint Presentation.
        using (IPresentation pptxDoc = Presentation.Open(pathStream))
        {
            //Convert the first slide into image.
            Image image = pptxDoc.Slides[0].ConvertToImage(Syncfusion.Drawing.ImageType.Metafile);
            //Saves the image file to MemoryStream.
            MemoryStream stream = new MemoryStream();
            //Download image file in the browser.
            ExportAsImage(image, "PPTXToImage.Jpeg", ImageFormat.Jpeg, HttpContext.ApplicationInstance.Response);
        }
    }
}
//To download the image file.
protected void ExportAsImage(Image image, string fileName, ImageFormat imageFormat, HttpResponse response)
{
    if (ControllerContext == null)
        throw new ArgumentNullException("Context");
    string disposition = "content-disposition";
    response.AddHeader(disposition, "attachment; filename=" + fileName);
    if (imageFormat != ImageFormat.Emf)
        image.Save(response.OutputStream, imageFormat);
    Response.End();
}

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/PPTX-to-Image-conversion/Convert-PowerPoint-presentation-to-Image/ASP.NET-MVC).

By executing the program, you will get the **image** as follows.

![PowerPoint to Image in ASP.NET MVC](PPTXtoPDF_images/Output_PowerPoint_Presentation_to-Image.png)

Click [here](https://www.syncfusion.com/document-processing/powerpoint-framework/net) to explore the rich set of Syncfusion PowerPoint Library (Presentation) features. 

An online sample link to [convert PowerPoint Presentation to image](https://ej2.syncfusion.com/aspnetmvc/PowerPoint/PPTXToImage#/material3) in ASP.NET MVC. 