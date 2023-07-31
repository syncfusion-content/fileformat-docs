---
title: Convert PowerPoint to PDF in ASP.NET | Syncfusion
description: Convert PowerPoint to PDF in ASP.NET using .NET PowerPoint library (Presentation) without Microsoft PowerPoint or interop dependencies.
platform: file-formats
control: PowerPoint
documentation: UG
---

# Convert PowerPoint to PDF in ASP.NET

Syncfusion PowerPoint is a [.NET PowerPoint library](https://www.syncfusion.com/document-processing/powerpoint-framework/net) used to create, read, edit and convert PowerPoint documents programmatically without **Microsoft PowerPoint** or interop dependencies. Using this library, you can **convert a PowerPoint to PDF in ASP.NET**.

## Steps to convert PowerPoint to PDF programmatically

Step 1: Create a new C# ASP.NET application project.

![Create ASP.NET MVC project](Workingwith_MVC/Project-Open-and-Save.png)

Step 2: Select the Empty project.

![Select MVC template](Workingwith_MVC/MVC-Open-and-Save.png)

Step 3: Install the [Syncfusion.PresentationToPDFConverter.AspNet](https://www.nuget.org/packages/Syncfusion.PresentationToPdfConverter.AspNet) NuGet package as reference to your .NET Standard applications from [NuGet.org](https://www.nuget.org/).

![Install Syncfusion.PresentationToPDFConverter.AspNet Nuget Package](Workingwith_MVC/Nuget-Open-and-Save.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 4: Add a new Web Form in your project. Right click on the project and select **Add > New Item** and add a Web Form from the list. Name it as MainPage.

Step 5: Add a new button in the **MainPage.aspx** as shown below.

{% tabs %}
{% highlight c# tabtitle="C#" %}

<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="MainPage.aspx.cs" Inherits="Convert_PowerPoint_Presentation_to_PDF.WebForm1" %>
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title></title>
</head>
<body>
    <form id="form1" runat="server">
        <div>
             <asp:Button ID="Button1" runat="server" Text="Convert PPTX to PDF" OnClick="OnButtonClicked" />
        </div>
    </form>
</body>
</html>

{% endhighlight %}
{% endtabs %}

Step 6. Include the following namespace in your **MainPage.aspx.cs** file.

{% tabs %}
{% highlight c# tabtitle="C#" %}

using Syncfusion.Presentation;
using Syncfusion.PresentationToPdfConverter;
using Syncfusion.Pdf;

{% endhighlight %}
{% endtabs %}

Step 7: Include the below code snippet in the click event of the button in **MainPage.aspx.cs**, to **convert a PowerPoint document to Pdf** and download it.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Open an existing PowerPoint document.        
string filePath = Server.MapPath("~/App_Data/Input.pptx");
//Opens a PowerPoint Presentation
using (IPresentation pptxDoc = Presentation.Open(filePath))
{
    //Converts the PowerPoint Presentation into PDF document
    using (PdfDocument pdfDocument = PresentationToPdfConverter.Convert(pptxDoc))
    {
        pdfDocument.Save("sample.pdf", HttpContext.Current.Response, HttpReadType.Save);
    }                   
} 

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from GitHub.

By executing the program, you will get the **PDF** as follows.

![Converted PDF from PowerPoint in ASP.NET](PPTXtoPDF_images/Output_PowerPoint_Presentation_to-PDF.png)

Click [here](https://www.syncfusion.com/document-processing/powerpoint-framework/net) to explore the rich set of Syncfusion PowerPoint Library (Presentation) features.
