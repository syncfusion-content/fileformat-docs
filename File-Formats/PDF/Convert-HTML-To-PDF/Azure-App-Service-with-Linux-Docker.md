---
title: Convert HTML to PDF in Azure app service using the Blink with Linux docker | Syncfusion
description: Learn how to convert HTML to PDF in Azure app service using the Blink with Linux docker with easy steps using Syncfusion .NET HTML converter library.
platform: file-formats
control: PDF
documentation: UG
keywords: Assemblies
---

The Syncfusion [HTML to PDF converter](https://www.syncfusion.com/document-processing/pdf-framework/net/html-to-pdf) is a .NET library for converting webpages, SVG, MHTML, and HTML to PDF using C#. It is reliable and accurate. The result preserves all graphics, images, text, fonts, and the layout of the original HTML document or webpage. Using this library, you can convert an HTML to PDF in Azure app service using the Blink with Linux [docker](https://www.docker.com/why-docker) container. 

# Steps to convert HTML to PDF in Azure app service using the Blink with Linux docker container:

Create a new ASP.NET Core application and enable the docker support with Linux as a target OS.
![Convert HTMLToPDF Azure Docker Step1](htmlconversion_images/DockerStep1.png)
![Convert HTMLToPDF Azure Docker Step2](htmlconversion_images/DockerStep2.png)

Install the [Syncfusion.HtmlToPdfConverter.Net.Linux](https://www.nuget.org/packages/Syncfusion.HtmlToPdfConverter.Net.Linux/) NuGet package as a reference to your .NET Core application [NuGet.org](https://www.nuget.org/)
![Convert HTMLToPDF Docker Step3](htmlconversion_images/AzureDocker1.png)

Include the following commands in the docker file to install the dependent packages in the docker container.

{% highlight c# tabtitle="C#" %}

RUN apt-get update && \
     apt-get install -yq --no-install-recommends \ 
     libasound2 libatk1.0-0 libc6 libcairo2 libcups2 libdbus-1-3 \ 
     libexpat1 libfontconfig1 libgcc1 libgconf-2-4 libgdk-pixbuf2.0-0 libglib2.0-0 libgtk-3-0 libnspr4 \ 
     libpango-1.0-0 libpangocairo-1.0-0 libstdc++6 libx11-6 libx11-xcb1 libxcb1 \ 
     libxcursor1 libxdamage1 libxext6 libxfixes3 libxi6 libxrandr2 libxrender1 libxss1 libxtst6 \ 
     libnss3 libgbm1

{% endhighlight %}

![Convert HTMLToPDF Azure Docker Step4](htmlconversion_images/DockerStep4.png)

Add an Export to the PDF button in the index.cshtml.

{% highlight c# tabtitle="C#" %}

<div class="btn">
    @{ Html.BeginForm("ExportToPDF", "Home", FormMethod.Post);
        {
            <input type="submit" value="Export To PDF" class=" btn" />
        }
}
</div>

{% endhighlight %}

![Convert HTMLToPDF Azure Docker Step5](htmlconversion_images/DockerStep5.png)

Include the following namespaces and code samples in the controller for converting HTML to PDF.

{% highlight c# tabtitle="C#" %}

using Syncfusion.HtmlConverter;
using Syncfusion.Pdf;
using System.IO

{% endhighlight %}

{% highlight c# tabtitle="C#" %}

public ActionResult ExportToPDF()
{
     //Initialize HTML to PDF converter. 
     HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter();
 
     BlinkConverterSettings settings = new BlinkConverterSettings();
     
     //Set command line arguments to run without the sandbox.
     settings.CommandLineArguments.Add("--no-sandbox");
     settings.CommandLineArguments.Add("--disable-setuid-sandbox");
     
     //Assign Blink settings to the HTML converter.
     htmlConverter.ConverterSettings = settings;
 
     //Convert URL to PDF.
     PdfDocument document = htmlConverter.Convert("https://www.syncfusion.com");
 
     MemoryStream stream = new MemoryStream();
 
     //Save and close a PDF document. 
     document.Save(stream);
 
     return File(stream.ToArray(), System.Net.Mime.MediaTypeNames.Application.Pdf, "URL_to_PDF.pdf");
}

{% endhighlight %}

Build and run the sample in the docker, it will pull the Linux docker image from the docker hub and run the project. Now, the webpage will open in the browser. Click Export to PDF option to convert the Syncfusion webpage to a PDF.
![Convert HTMLToPDF Azure Docker Step6](htmlconversion_images/AzureDocker2.png)

By executing the program, you will get the PDF document as follows.
![Convert HTMLToPDF Azure Docker Step7](htmlconversion_images/htmltopdfoutput.png)

# Deploy the container to Azure container instance:

Create a publish target to deploy the docker image to Azure. 
![Convert HTMLToPDF Azure Docker Step8](htmlconversion_images/AzureDocker3.png)

Create Azure App Service with resource group, hosting plan, and container registry. 
![Convert HTMLToPDF Azure Docker Step9](htmlconversion_images/AzureDocker4.png)

Publish the docker image to Azure container instance.
![Convert HTMLToPDF Azure Docker Step9](htmlconversion_images/AzureDocker5.png)

It will push the docker image to the Azure container registry and deploy it to the Azure container instance.
![Convert HTMLToPDF Azure Docker Step9](htmlconversion_images/AzureDocker6.png)

After successful deployment, it will open the Azure website in the browser.
![Convert HTMLToPDF Azure Docker Step9](htmlconversion_images/AzureDocker6.png)

Click Export to PDF option to convert the Google webpage to a PDF. You will get the PDF document as follows.
![Convert HTMLToPDF Azure Docker Output](htmlconversion_images/htmltopdfoutput.png) 

A complete work sample can be downloaded from [BlinkLinuxDockerAzureSample.zip.](https://www.syncfusion.com/downloads/support/directtrac/general/ze/BlinkLinuxDockerAzureSample637072917)