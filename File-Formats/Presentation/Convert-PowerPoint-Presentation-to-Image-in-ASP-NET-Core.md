---
title: Convert PowerPoint to Image in ASP.NET Core | Syncfusion
description: Convert PowerPoint to image in ASP.NET Core using .NET Core PowerPoint library (Presentation) without Microsoft PowerPoint or interop dependencies.
platform: file-formats
control: PowerPoint
documentation: UG
---

# Convert PowerPoint to Image in ASP.NET Core

Syncfusion PowerPoint is a [.NET Core PowerPoint library](https://www.syncfusion.com/document-processing/powerpoint-framework/net-core) used to create, read, edit and **convert PowerPoint documents** programmatically without **Microsoft PowerPoint** or interop dependencies. Using this library, you can **convert a PowerPoint to image in ASP.NET Core**.

## Steps to convert PowerPoint to Image programmatically

Step 1: Create a new C# ASP.NET Core web application project.

![Create ASP.NET Core Web project for PowerPoint file](Workingwith_Core/Create-Project-Open-and-Save.png)

Step 2: Install the [Syncfusion.PresentationRenderer.Net.Core](https://www.nuget.org/packages/Syncfusion.PresentationRenderer.Net.Core) NuGet package as reference to your .NET Standard applications from [NuGet.org](https://www.nuget.org/).

![Install Syncfusion.PresentationRenderer.Net.Core Nuget Package](Workingwith_Core/Nuget-Package_Open_and_Save.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.
Step 3: Include the following namespaces in **HomeController.cs**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

using Syncfusion.Presentation;
using Syncfusion.PresentationRenderer;

{% endhighlight %}
{% endtabs %}

Step 4: A default action method named Index will be present in **HomeController.cs**. Right click on Index method and select **Go To View** where you will be directed to its associated view page **Index.cshtml**.

Step 5: Add a new button in the **Index.cshtml** as shown below.

{% tabs %}
{% highlight HTML %}

@{
    Html.BeginForm("ConvertPPTXtoImage", "Home", FormMethod.Post, new { enctype = "multipart/form-data" });
    {
        <div class="Common">
            <div class="tablediv">
                <div class="rowdiv">
                    This sample illustrates how to convert PowerPoint document to image using PowerPoint library.
                </div>
                &nbsp;
                <div class="rowdiv" style="border-width: 0.5px;border-style:solid; border-color: lightgray; padding: 1px 5px 7px 5px">
                    Click the button to view the resultant image document being converted from PowerPoint document.
                    <div class="rowdiv" style="margin-top: 10px">
                        <div class="celldiv">
                            Select Document :
                            @Html.TextBox("file", "", new { type = "file", accept = ".pptx" }) <br />
                        </div>
                        <div class="rowdiv" style="margin-top: 8px">
                            <input class="buttonStyle" type="submit" value="Convert to image" name="button" style="width:150px;height:27px" />
                            <br />
                            <div class="text-danger">
                                @ViewBag.Message
                            </div>
                        </div>
                    </div>
                </div>
                <br />
            </div>
        </div>
        Html.EndForm();
    }
}

{% endhighlight %}
{% endtabs %}

Step 6: Add a new action method **ConvertPPTXtoImage** in HomeController.cs and include the below code snippet to **convert a PowerPoint to image in ASP.NET Core**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

public ActionResult ConvertPPTXtoImage(string button)
{
    if (button == null)
        return View("Index");
    if (Request.Form.Files != null)
    {
        if (Request.Form.Files.Count == 0)
        {
            ViewBag.Message = string.Format("Browse a PowerPoint Presentation and then click the button to convert as a image");
            return View("Index");
        }
        // Gets the extension from file.
        string extension = Path.GetExtension(Request.Form.Files[0].FileName).ToLower();
        // Compares extension with supported extensions.
        if (extension == ".pptx")
        {
            MemoryStream memoryStream = new MemoryStream();
            Request.Form.Files[0].CopyTo(memoryStream);
            try
            {
                //Open the existing PowerPoint presentation with loaded stream.
                using (IPresentation pptxDoc = Presentation.Open(memoryStream))
                {
                    //Initialize the PresentationRenderer to perform image conversion.
                    pptxDoc.PresentationRenderer = new PresentationRenderer();
                    //Convert PowerPoint slide to image as stream.
                    Stream stream = pptxDoc.Slides[0].ConvertToImage(ExportImageFormat.Jpeg);
                    //Reset the stream position
                    stream.Position = 0;
                    //Download image in the browser.
                    return File(stream, "application/jpeg", "PPTXtoImage.Jpeg");
                }
            }
            catch (Exception ex)
            {
                ViewBag.Message = ex.ToString();
            }
        }
        else
        {
            ViewBag.Message = string.Format("Please choose PowerPoint document to convert to image");
        }
    }
    else
    {
        ViewBag.Message = string.Format("Browse a PowerPoint document and then click the button to convert as a image");
    }
    return View("Index");
}

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from GitHub.

By executing the program, you will get the **image** as follows.

![PowerPoint to Image in ASP.NET Core](PPTXtoPDF_images/Output_PowerPoint_Presentation_to-Image.png)
