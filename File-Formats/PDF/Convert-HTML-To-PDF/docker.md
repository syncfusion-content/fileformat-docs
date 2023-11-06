---
title: Convert a HTML to PDF file in Docker | Syncfusion
description: Learn how to convert a HTML to PDF file in docker with easy steps using Syncfusion .NET HTML converter library.
platform: file-formats
control: PDF
documentation: UG
keywords: Assemblies
---

# Convert HTML to PDF file in Linux Docker container

The Syncfusion HTML to PDF converter is a .NET library that converts HTML or web pages to PDF document in a Linux [Docker](https://www.docker.com/why-docker/) container.

## Steps to convert HTML to PDF in Linux Docker container

Step 1: Create a new ASP.NET Core application and enable the Docker support with Linux as a target OS.
![Convert HTMLToPDF Docker Step1](htmlconversion_images/DockerStep1.png)
![Convert HTMLToPDF Docker Step2](htmlconversion_images/DockerStep2.png)

Step 2: Install the [Syncfusion.HtmlToPdfConverter.Net.Linux](https://www.nuget.org/packages/Syncfusion.HtmlToPdfConverter.Net.Linux/) NuGet package as a reference to your .NET Core application [NuGet.org](https://www.nuget.org/).
![Convert HTMLToPDF Docker Step3](htmlconversion_images/DockerStep3.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 3: Include the following commands in the Docker file to install the dependent packages in the docker container.

{% highlight c# tabtitle="C#" %}

RUN apt-get update && \
apt-get install -yq --no-install-recommends \ 
libasound2 libatk1.0-0 libc6 libcairo2 libcups2 libdbus-1-3 \ 
libexpat1 libfontconfig1 libgcc1 libgconf-2-4 libgdk-pixbuf2.0-0 libglib2.0-0 libgtk-3-0 libnspr4 \ 
libpango-1.0-0 libpangocairo-1.0-0 libstdc++6 libx11-6 libx11-xcb1 libxcb1 \ 
libxcursor1 libxdamage1 libxext6 libxfixes3 libxi6 libxrandr2 libxrender1 libxss1 libxtst6 \ 
libnss3 libgbm1

{% endhighlight %}

![Convert HTMLToPDF Docker Step4](htmlconversion_images/DockerStep4.png)

Step 4: Add a new button in the index.cshtml as shown below.

{% highlight c# tabtitle="C#" %}

<div class="btn">
   @{ Html.BeginForm("ExportToPDF", "Home", FormMethod.Post);
         {
            <input type="submit" value="Export To PDF" class=" btn" />
         }
      }
</div>

{% endhighlight %}

![Convert HTMLToPDF Docker Step5](htmlconversion_images/DockerStep5.png)

Step 5: A default controller with name HomeController.cs gets added on creation of ASP.NET Core project. Include the following namespaces in that HomeController.cs file.

{% highlight c# tabtitle="C#" %}

using Syncfusion.HtmlConverter;
using Syncfusion.Pdf;
using System.IO;

{% endhighlight %}

Step 6: Add a new action method in HomeController.cs and include the below code snippet to convert HTML to PDF document using [Convert](https://help.syncfusion.com/cr/file-formats/Syncfusion.HtmlConverter.HtmlToPdfConverter.html#Syncfusion_HtmlConverter_HtmlToPdfConverter_Convert_System_String_) method in [HtmlToPdfConverter](https://help.syncfusion.com/cr/file-formats/Syncfusion.HtmlConverter.HtmlToPdfConverter.html) class. The HTML content will be scaled based on the given [ViewPortSize](https://help.syncfusion.com/cr/file-formats/Syncfusion.HtmlConverter.BlinkConverterSettings.html#Syncfusion_HtmlConverter_BlinkConverterSettings_ViewPortSize) property of [BlinkConverterSettings](https://help.syncfusion.com/cr/file-formats/Syncfusion.HtmlConverter.BlinkConverterSettings.html) class.

{% highlight c# tabtitle="C#" %}

public ActionResult ExportToPDF()
{
   //Initialize HTML to PDF converter. 
   HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter(); 
   BlinkConverterSettings settings = new BlinkConverterSettings();     
   //Set command line arguments to run without the sandbox.
   settings.CommandLineArguments.Add("--no-sandbox");
   settings.CommandLineArguments.Add("--disable-setuid-sandbox");     
   //Set Blink viewport size.
   settings.ViewPortSize = new Syncfusion.Drawing.Size(1280, 0);     
   //Assign Blink settings to the HTML converter.
   htmlConverter.ConverterSettings = settings; 
   //Convert URL to PDF document.
   PdfDocument document = htmlConverter.Convert("https://www.syncfusion.com"); 
   //Create memory stream.
   MemoryStream stream = new MemoryStream(); 
   //Save the document to memory stream. 
   document.Save(stream); 
   return File(stream.ToArray(), System.Net.Mime.MediaTypeNames.Application.Pdf, "HTML-to-PDF.pdf");
}

{% endhighlight %}

Step 7: Build and run the sample in the Docker. It will pull the Linux Docker image from the Docker hub and run the project. Now, the webpage will open in the browser. Click the button to convert the webpage to a PDF document.

By executing the program, you will get the PDF document as follows.
![Convert HTMLToPDF Dockeroutput](htmlconversion_images/htmltopdfoutput.png)

A complete working sample for converting an HTML to PDF in the Linux docker container can be downloaded from [Github](https://github.com/SyncfusionExamples/html-to-pdf-csharp-examples/tree/master/Docker).

Click [here](https://www.syncfusion.com/document-processing/pdf-framework/net-core/html-to-pdf) to explore the rich set of Syncfusion HTML to PDF converter library features. 

An online sample link to [convert HTML to PDF document](https://ej2.syncfusion.com/aspnetcore/PDF/HtmltoPDF#/material3) in ASP.NET Core. 