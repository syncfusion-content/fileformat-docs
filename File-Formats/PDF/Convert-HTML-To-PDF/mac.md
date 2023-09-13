---
title: Convert a HTML to PDF file in Mac | Syncfusion
description: Learn how to convert a HTML to PDF file in Mac with easy steps using Syncfusion .NET HTML converter library.
platform: file-formats
control: PDF
documentation: UG
keywords: Assemblies
---

# Convert HTML to PDF file in Mac using C#

The Syncfusion [HTML to PDF converter](https://www.syncfusion.com/pdf-framework/net/html-to-pdf) is a .NET library for converting webpages, SVG, MHTML, and HTML to PDF using C#. It is reliable and accurate. Using this library, you can convert HTML to PDF document in Mac.

## Steps to convert HTML to PDF in ASP.NET Core MVC

Step 1: Create a new C# ASP.NET Core Web Application project.
![Create ASP.NET Core Web application](htmlconversion_images/mac_step1.png)  

Step 2: Select the Target Framework of your project.
![Select target framework](htmlconversion_images/mac_step2.png)  

Step 3: Configure your application and click Create.
![Configure the application](htmlconversion_images/mac_step3.png)

Step 4: Install the [Syncfusion.HtmlToPdfConverter.Net.Mac](https://www.nuget.org/packages/Syncfusion.HtmlToPdfConverter.Net.Mac) NuGet package as reference to your .NET Standard applications from [NuGet.org](https://www.nuget.org/).
![NuGet package installation](htmlconversion_images/mac_step4.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 5: A default controller with name HomeController.cs gets added on creation of ASP.NET MVC project. Include the following namespaces in that HomeController.cs file.

{% highlight c# tabtitle="C#" %}

using Syncfusion.Pdf;
using Syncfusion.HtmlConverter;
using System.IO;
using Microsoft.AspNetCore.Hosting;

{% endhighlight %}

Step 6: A default action method named Index will be present in HomeController.cs. Right click on Index method and select Go To View where you will be directed to its associated view page Index.cshtml. Add a new button in the Index.cshtml as shown below.

{% highlight c# tabtitle="C#" %}

@{Html.BeginForm("ExportToPDF", "Home", FormMethod.Post);
    {
        <div>
            <input type="submit" value="Convert PDF" style="width:150px;height:27px" />
        </div>
     }
        Html.EndForm();
 }

{% endhighlight %}

Step 7: Add a new action method ExportToPDF in HomeController.cs and include the below code example to convert HTML to PDF file using [Convert](https://help.syncfusion.com/cr/file-formats/Syncfusion.HtmlConverter.HtmlToPdfConverter.html#Syncfusion_HtmlConverter_HtmlToPdfConverter_Convert_System_String_) method in [HtmlToPdfConverter](https://help.syncfusion.com/cr/file-formats/Syncfusion.HtmlConverter.HtmlToPdfConverter.html) class.

{% highlight c# tabtitle="C#" %}

public IActionResult ExportToPDF()
{
    //Initialize HTML to PDF converter.
    HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter();
    //Convert URL to PDF.
    PdfDocument document = htmlConverter.Convert("https://www.syncfusion.com");
    MemoryStream stream = new MemoryStream();
    document.Save(stream);
    //Download the PDF document in the browser
    return File(stream.ToArray(), System.Net.Mime.MediaTypeNames.Application.Pdf, "HTML-to-PDF.pdf");
}

{% endhighlight %}

Step 8: Right click the project and select Build.
![Build project](htmlconversion_images/mac_step5.png)

N> Once the build succeeded, unzip the chromium.app file in bin folder (bin-> Debug-> net6.0-> runtimes-> osx-> native-> Chromium.app)`

Step 9: Run the application.
![Run application](htmlconversion_images/mac_step6.png)

By executing the program, you will get the PDF document as follows.
![HTML to PDF output document](htmlconversion_images/htmltopdfoutput.png)

A complete working sample can be downloaded from [Github](https://github.com/SyncfusionExamples/html-to-pdf-csharp-examples/tree/master/Mac).

Click [here](https://www.syncfusion.com/document-processing/pdf-framework/net-core/html-to-pdf) to explore the rich set of Syncfusion HTML to PDF converter library features. 

An online sample link to [convert HTML to PDF document](https://ej2.syncfusion.com/aspnetcore/PDF/HtmltoPDF#/material3) in ASP.NET Core. 