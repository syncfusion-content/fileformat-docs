---
title: How to use the HTML converter in Visual Studio for Mac | Syncfusion
description: Learn how to use the HTML converter in Visual Studio for Mac with easy steps using Syncfusion .NET Core PDF library.
platform: file-formats
control: PDF
documentation: UG
keywords: Assemblies
---
# Convert HTML to PDF file in ASP.NET Core Mac

In your ASP.NET Core application, add the following assemblies to use Essential PDF:

* Syncfusion.Compression.Portable.dll
* Syncfusion.Pdf.Portable.dll
* Syncfusion.HtmlConverter.Portable.dll

For more details, refer to this [Assemblies Required](/File-Formats/PDF/Assemblies-Required) documentation.

## How to use the HTML converter in Visual Studio for Mac.

Create a new C# ASP.NET Core Web Application project.
![SampleCreation2](Convert-HTML-To-PDF/htmlconversion_images/SampleCreation1.png)

Select the Target Framework of your project.
![SampleCreation2](Convert-HTML-To-PDF/htmlconversion_images/SampleCreation2.png)

Configure your application and click <b>Create</b>.
![SampleCreation3](Convert-HTML-To-PDF/htmlconversion_images/SampleCreation3.png)

Install the [Syncfusion.HtmlToPdfConverter.QtWebKit.Net.Core](https://www.nuget.org/packages/Syncfusion.HtmlToPdfConverter.QtWebKit.Net.Core/) NuGet package as reference to your .NET Standard applications from [NuGet.org](https://www.nuget.org/).
![SampleCreation4](Convert-HTML-To-PDF/htmlconversion_images/SampleCreation4.png)

Copy the QtBinariesMac folder from the installed HtmlToPdfConverter package and paste it into the folder which contains the HTMLtoPDF.csproj file.
![SampleCreation5](Convert-HTML-To-PDF/htmlconversion_images/SampleCreation5.png)

A default controller with name HomeController.cs gets added on creation of ASP.NET MVC project. Include the following namespaces in that HomeController.cs file.

{% highlight c# %}

using Syncfusion.Pdf;
using Syncfusion.HtmlConverter;
using System.IO;
using Microsoft.AspNetCore.Hosting;

{% endhighlight %}

A default action method named Index will be present in HomeController.cs. Right click on Index method and select Go To View where you will be directed to its associated view page Index.cshtml.

Add a new button in the Index.cshtml as shown below.

{% highlight c# %}

@{Html.BeginForm("ExportToPDF", "Home", FormMethod.Post);
{
<div>
    <input type="submit" value="Convert PDF" style="width:150px;height:27px" />
</div>
}
Html.EndForm();
}
{% endhighlight %}

Add a new action method ExportToPDF in HomeController.cs and include the below code snippet to convert HTML to PDF file and download it.

{% highlight c# %}

//To get content root path of the project
private readonly IHostingEnvironment _hostingEnvironment;
public HomeController(IHostingEnvironment hostingEnvironment)
{
   _hostingEnvironment = hostingEnvironment;
}

public IActionResult ExportToPDF()
{
//Initialize HTML to PDF converter 
HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter(HtmlRenderingEngine.WebKit);

WebKitConverterSettings settings = new WebKitConverterSettings();

//Set WebKit path
settings.WebKitPath = Path.Combine(_hostingEnvironment.ContentRootPath, "QtBinariesMac");

//Assign WebKit settings to HTML converter
htmlConverter.ConverterSettings = settings;

//Convert URL to PDF
PdfDocument document = htmlConverter.Convert("https://www.google.com");

//Saving the PDF to the MemoryStream
MemoryStream stream = new MemoryStream();

document.Save(stream);

//Download the PDF document in the browser
return File(stream.ToArray(), System.Net.Mime.MediaTypeNames.Application.Pdf, "Output.pdf");

}

{% endhighlight %}

![SampleCreation6](Convert-HTML-To-PDF/htmlconversion_images/SampleCreation6.png)

Right click the project and select <b>Build</b>. 
![SampleCreation7](Convert-HTML-To-PDF/htmlconversion_images/SampleCreation7.png)

After Build succeeded. Run the application.
![SampleCreation8](Convert-HTML-To-PDF/htmlconversion_images/SampleCreation8.png)

A complete working sample can be downloaded from [HtmlToPDF.zip](https://www.syncfusion.com/downloads/support/directtrac/general/ze/HtmlToPDF-545793311)


By executing the program, you will get the PDF document as follows.
![SampleCreation9](Convert-HTML-To-PDF/htmlconversion_images/SampleCreation9.png)
