---
title: How to use the HTML converter in Visual Studio for Mac | Syncfusion
description: Learn how to use the HTML converter in Visual Studio for Mac with easy steps using Syncfusion .NET Core PDF library.
platform: file-formats
control: PDF
documentation: UG
keywords: Assemblies
---

## How to download HTML Converter Mac installer?

Refer this [link](https://help.syncfusion.com/common/essential-studio/download/) to download trial\licensed installer based on your license.

The latest WebKit HTML converter for Mac can be downloaded as PKG file from the following link,

https://www.syncfusion.com/downloads/latest-version 

In the downloads page, click the “Mac” button and download the HTML Converter Mac installer.
![MacDownload](Convert-HTML-To-PDF/htmlconversion_images/MacDownload.png)

## Step-by-Step Installation

The following procedure illustrates how to install Essential Studio WebKit HTML Converter Mac installer. 

Double-click the Syncfusion Essential Studio WebKit HTML Converter Mac installer(.pkg) file. The installer Wizard opens. Click <b>Continue</b>.
![InstallationSteps1](Convert-HTML-To-PDF/htmlconversion_images/InstallationSteps1.png)

Software License Agreement window opens. Click <b>Continue</b>.
![InstallationSteps2](Convert-HTML-To-PDF/htmlconversion_images/InstallationSteps2.png)

Confirmation window will be displayed for the License Agreement. Click <b>Agree</b>.
![InstallationSteps3](Convert-HTML-To-PDF/htmlconversion_images/InstallationSteps3.png)

N> Unlock key is not required for installing the Mac installer. Syncfusion Mac installer can be used for developing purposes without registering the Unlock key.

Destination Select windows opens. Click <b>Continue</b>.
![InstallationSteps4](Convert-HTML-To-PDF/htmlconversion_images/InstallationSteps4.png)

Installation Type window opens. Click <b>Install</b>.
![InstallationSteps5](Convert-HTML-To-PDF/htmlconversion_images/InstallationSteps5.png)

Authentication window opens. Provide your system’s username, password and click <b>Install Software</b>.
![InstallationSteps6](Convert-HTML-To-PDF/htmlconversion_images/InstallationSteps6.png)

Installation will be started in your machine.
![InstallationSteps7](Convert-HTML-To-PDF/htmlconversion_images/InstallationSteps7.png)

Completed screen will be displayed once the installation is finished. Click Close to exit the installation wizard.
![InstallationSteps8](Convert-HTML-To-PDF/htmlconversion_images/InstallationSteps8.png)

By default, Mac installer will install the files in following location.

Location: {Documents}\Syncfusion\ {version}\ {platform}
![InstallationSteps9](Convert-HTML-To-PDF/htmlconversion_images/InstallationSteps9.png)

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
