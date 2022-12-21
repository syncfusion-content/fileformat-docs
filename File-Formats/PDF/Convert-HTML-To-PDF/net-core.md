---
title: Convert a HTML to PDF file in ASP.NET Core | Syncfusion
description: Learn how to convert a HTML to PDF file in ASP.NET Core with easy steps using Syncfusion .NET HTML converter library.
platform: file-formats
control: PDF
documentation: UG
keywords: Assemblies
---

# Convert HTML to PDF file in ASP.NET Core

The Syncfusion HTML to PDF converter is a .NET library used to convert HTML or web pages to PDF document in ASP.NET Core application.  

## Steps to convert HTML to PDF in ASP.NET Core application

Step 1: Create a new C# ASP.NET Core Web Application project.
   <img src="htmlconversion_images/aspnetcore1.png" alt="convert_HtmltoPdf_ASPNET_CORE1" width="100%" Height="Auto"/>

Step 2:  In configuration windows, name your project and select Next.
   <img src="htmlconversion_images/aspnetcore2.png" alt="convert_HtmltoPdf_ASPNET_CORE2" width="100%" Height="Auto"/>
   <img src="htmlconversion_images/aspnetcore3.png" alt="convert_HtmltoPdf_ASPNET_CORE3" width="100%" Height="Auto"/>

Step 3:  Install [Syncfusion.HtmlToPdfConverter.Net.Windows](https://www.nuget.org/packages/Syncfusion.HtmlToPdfConverter.Net.Windows) NuGet package as reference to your .NET Standard applications from [NuGet.org](https://www.nuget.org/).   
   <img src="htmlconversion_images/aspnetcore4.png" alt="convert_HtmltoPdf_ASPNET_CORE4" width="100%" Height="Auto"/>

Step 4: A default controller with name HomeController.cs gets added on creation of ASP.NET Core MVC project. Include the following namespaces in that HomeController.cs file.

{% highlight c# tabtitle="C#" %}

using Syncfusion.Pdf;
using Syncfusion.HtmlConverter;
using System.IO;

{% endhighlight %}

Step 5: Add a new button in index.cshtml as shown below.

{% highlight c# tabtitle="C#" %}

@{Html.BeginForm("ExportToPDF", "Home", FormMethod.Post);
    {
        <div>
            <input type="submit" value="Convert HTML to PDF" style="width:150px;height:27px" />
        </div>
    }
    Html.EndForm();
}

{% endhighlight %}

Step 6: Add a new action method named ExportToPDF in HomeController.cs and include the below code snippet to convert HTML to PDF file and download it.

{% highlight c# tabtitle="C#" %}

//Initialize HTML to PDF converter.
HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter();
BlinkConverterSettings blinkConverterSettings = new BlinkConverterSettings();
//Set Blink viewport size.
blinkConverterSettings.ViewPortSize = new Syncfusion.Drawing.Size(1280, 0);
//Assign Blink converter settings to HTML converter.
htmlConverter.ConverterSettings = blinkConverterSettings;
//Convert URL to PDF document.
PdfDocument document = htmlConverter.Convert("https://www.syncfusion.com");
//Create memory stream.
MemoryStream stream = new MemoryStream();
//Save and close the document. 
document.Save(stream);
document.Close(); 
return File(stream.ToArray(), System.Net.Mime.MediaTypeNames.Application.Pdf, "HTML-to-PDF.pdf");

{% endhighlight %}

By executing the program, you will get the PDF document as follows.
<img src="htmlconversion_images/htmltopdfoutput.png" alt="Convert HTMLToPDF ASP.NET_Core output" width="100%" Height="Auto"/>
 
A complete working sample can be downloaded from [Github](https://github.com/SyncfusionExamples/html-to-pdf-csharp-examples/tree/master/ASP.NET%20Core).
   
   