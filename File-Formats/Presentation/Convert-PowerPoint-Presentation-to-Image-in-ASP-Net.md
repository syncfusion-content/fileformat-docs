---
title: Convert PowerPoint to Image in ASP.NET | Syncfusion
description: Convert PowerPoint to image in ASP.NET using .NET PowerPoint library (Presentation) without Microsoft PowerPoint or interop dependencies.
platform: file-formats
control: PowerPoint
documentation: UG
---

# Convert PowerPoint to Image in ASP.NET

Syncfusion PowerPoint is a [.NET PowerPoint library](https://www.syncfusion.com/document-processing/powerpoint-framework/net) used to create, read, edit and **convert PowerPoint documents** programmatically without **Microsoft PowerPoint** or interop dependencies. Using this library, you can **convert a PowerPoint to image in ASP.NET**.

## Steps to convert PowerPoint to Image programmatically

Step 1: Create a new C# ASP.NET web application project.

![Create ASP.NET Web project](Workingwith_Web/Project-Open-and-Save.png)

Step 2: Select the **Empty** template to create the project.

![Select Web Forms template](Workingwith_Web/Empty-Open-and-Save.png)

Step 3: Install the [Syncfusion.PresentationRenderer.Net.Core](https://www.nuget.org/packages/Syncfusion.PresentationRenderer.Net.Core) NuGet package as reference to your .NET Standard applications from [NuGet.org](https://www.nuget.org/).

![Install Syncfusion.PresentationRenderer.Net.Core Nuget package](Azure_Images/App_Service_Linux/Nuget_Package_PowerPoint_Presentation_to_PDF.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 4: Include the following namespaces in **MainPage.aspx.cs**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

using Syncfusion.Presentation;
using Syncfusion.PresentationRenderer;

{% endhighlight %}
{% endtabs %}

Step 5: Add a new button in the **MainPage.aspx** as shown below.

{% tabs %}
{% highlight HTML %}

<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="MainPage.aspx.cs" Inherits="Convert_PowerPoint_Presentation_to_Image.WebForm1" %>

<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title></title>
</head>
<body>
    <form id="form1" runat="server">
        <div>
             <asp:Button ID="Button1" runat="server" Text="Convert PPTX to Image" OnClick="OnButtonClicked" />
        </div>
    </form>
</body>
</html>

{% endhighlight %}
{% endtabs %}

Step 6: Include the below code snippets in **MainPage.aspx.cs** to **convert a PowerPoint to image in ASP.NET**.

{% tabs %}
{% highlight c# tabtitle="C#" %}

string filePath = Server.MapPath("~/App_Data/Input.pptx");
//Open the existing PowerPoint presentation.
using (IPresentation pptxDoc = Presentation.Open(filePath))
{
    //Initialize the PresentationRenderer.
    pptxDoc.PresentationRenderer = new PresentationRenderer();
    //Converts the first slide into image.
    using (Stream stream = pptxDoc.Slides[0].ConvertToImage(ExportImageFormat.Jpeg))
    {
        //Create the output image file stream.
        using (FileStream fileStreamOutput = File.Create(Server.MapPath("~/PPTXtoImage.Jpeg")))
        {
            //Copy the converted image stream into created output image stream
            stream.CopyTo(fileStreamOutput);
        }
    }
}

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from GitHub.

By executing the program, you will get the **image** as follows.

![PowerPoint to Image in ASP.NET](PPTXtoPDF_images/Output_PowerPoint_Presentation_to-Image.png)

Click [here](https://www.syncfusion.com/document-processing/powerpoint-framework/net) to explore the rich set of Syncfusion PowerPoint Library (Presentation) features. 

An online sample link to [convert PowerPoint Presentation to image](https://ej2.syncfusion.com/aspnetcore/PowerPoint/PPTXToImage#/material3) in ASP.NET Core. 
