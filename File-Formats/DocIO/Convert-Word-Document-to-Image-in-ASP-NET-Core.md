---
title: Convert Word to Image in ASP.NET Core | Syncfusion
description: Convert Word to image without Microsoft Word or interop dependencies in ASP.NET Core application using .NET Core Word (DocIO) library.
platform: file-formats
control: DocIO
documentation: UG
---

# Convert Word document to Image in ASP.NET Core

Syncfusion DocIO is a [.NET Core Word library](https://www.syncfusion.com/document-processing/word-framework/net-core/word-library) used to create, read, edit, and **convert Word documents** programmatically without **Microsoft Word** or interop dependencies. Using this library, you can **convert a Word document to image in ASP.NET Core**.

## Steps to convert Word document to Image in C#

Step 1: Create a new ASP.NET Core Web application (Model-View-Controller) project.

![Create ASP.NET Core Web application in Visual Studio](ASP-NET-Core_images/CreateProjectforConversion.png)

Step 2: Install the [Syncfusion.DocIORenderer.Net.Core](https://www.nuget.org/packages/Syncfusion.DocIORenderer.Net.Core) NuGet package as a reference to your project from [NuGet.org](https://www.nuget.org/).

![Install Syncfusion.DocIORenderer.Net.Core NuGet package](ASP-NET-Core_images/NugetPackage.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 3: Include the following namespaces in the HomeController.cs file.

{% tabs %}

{% highlight c# tabtitle="C#" %}

using Syncfusion.DocIO;
using Syncfusion.DocIO.DLS;
using Syncfusion.DocIORenderer;

{% endhighlight %}

{% endtabs %}

Step 5: A default action method named Index will be present in HomeController.cs. Right click on Index method and select **Go To View** where you will be directed to its associated view page **Index.cshtml**.

Step 6: Add a new button in the Index.cshtml as shown below.

{% tabs %}

{% highlight c# tabtitle="C#" %}

@{
    Html.BeginForm("ConvertWordtoImage", "Home", FormMethod.Get);
    {
        <div>
            <input type="submit" value="Convert Word to Image" style="width:200px;height:27px" />
        </div>
    }
    Html.EndForm();
}

{% endhighlight %}

{% endtabs %}

Step 7: Add a new action method **ConvertWordtoImage** in HomeController.cs and include the below code snippet to **convert the Word document to image**.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Open the file as Stream
using (FileStream docStream = new FileStream(Path.GetFullPath("Data/Input.docx"), FileMode.Open, FileAccess.Read))
{
    //Loads file stream into Word document
    using (WordDocument wordDocument = new WordDocument(docStream, FormatType.Docx))
    {
        //Instantiation of DocIORenderer
        using (DocIORenderer render = new DocIORenderer())
        {
            //Convert the first page of the Word document into an image.
            Stream imageStream = wordDocument.RenderAsImages(0, ExportImageFormat.Jpeg);
            //Reset the stream position.
            imageStream.Position = 0;
            //Save the image file.
            return File(imageStream, "application/jpeg", "WordToImage.Jpeg");
        }
    }
}

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-Image-conversion/Convert-Word-to-image/ASP.NET-Core).

By executing the program, you will get the **image** as follows.

![Word to Image in ASP.NET Core](WordToPDF_images/Output-WordtoImage.png)
