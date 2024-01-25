---
title: Convert HTML to PDF in Azure | Syncfusion
description: Learn how to convert HTML to PDF in Azure with easy steps using Syncfusion .NET HTML converter library.
platform: file-formats
control: PDF
documentation: UG
keywords: Assemblies
---

# Convert HTML to PDF file in Azure using C#

The Syncfusion [HTML to PDF converter](https://www.syncfusion.com/document-processing/pdf-framework/net/html-to-pdf) is a .NET library for converting webpages, SVG, MHTML, and HTML to PDF using C#. It is reliable and accurate. The result preserves all graphics, images, text, fonts, and the layout of the original HTML document or webpage. Using this library, you can convert an HTML to PDF using C# with the Blink rendering engine in Azure App Service on Linux, Azure app service using the Linux [docker](https://www.docker.com/why-docker) container and Azure Function Application Linux.

N> HTML to PDF converter is not supported with Azure App Service windows. We internally use Blink rendering engine for the conversion, it uses GDI calls for viewing and rendering the webpages. But Azure app service blocks GDI calls in the Azure website environment. As the Azure website does not have the elevated permission and enough rights, we can not launch the Chrome headless browser in the Azure app service windows (Azure website and Azure function).

## Azure App Service Linux

**Steps to convert HTML to PDF in Azure App service on Linux**

Step 1: Create a new ASP.NET Core MVC application.
![Convert HTMLToPDF Azure NetCore Step1](htmlconversion_images/AzureNetCore1.png)  

Step 2: Choose your project's target framework and select Configure for HTTPS.
![Choose project target framework](htmlconversion_images/AzureNetCore2.png) 

Step 3: Install the [Syncfusion.HtmlToPdfConverter.Net.Linux](https://www.nuget.org/packages/Syncfusion.HtmlToPdfConverter.Net.Linux/) NuGet package as a reference to your .NET Core application [NuGet.org](https://www.nuget.org/).
![NuGet package installation](htmlconversion_images/AzureNetCore3.png) 

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

There are two ways to install the dependency packages to Azure server,
* Using SSH from Azure portal.
* By running the commands from C#.

**Using SSH command line**

* After publishing the Web application, login to the Azure portal in a web interface and open the published app service. Under Development Tools Menu, Open the SSH and Click the go link.
![Convert HTMLToPDF Azure NetCore Step4](htmlconversion_images/AzureNetCore4.png) 

* From the terminal window, you can install the dependency packages. Use the following single command to install all dependencies packages.

{% highlight c# tabtitle="C#" %}

apt-get update && apt-get install -yq --no-install-recommends  libasound2 libatk1.0-0 libc6 libcairo2 libcups2 libdbus-1-3 libexpat1 libfontconfig1 libgcc1 libgconf-2-4 libgdk-pixbuf2.0-0 libglib2.0-0 libgtk-3-0 libnspr4 libpango-1.0-0 libpangocairo-1.0-0 libstdc++6 libx11-6 libx11-xcb1 libxcb1 libxcursor1 libxdamage1 libxext6 libxfixes3 libxi6 libxrandr2 libxrender1 libxss1 libxtst6 libnss3 libgbm1

{% endhighlight %}

**Running the commands from C#**

* Create a shell file with the above commands in the project and name it as dependenciesInstall.sh. In this article, these steps have been followed to install dependencies packages. 
![Convert HTMLToPDF Azure NetCore Step5](htmlconversion_images/AzureNetCore5.png) 

* Set Copy to Output Directory as "Copy if newer" to the dependenciesInstall.sh file.
![Convert HTMLToPDF Azure NetCore Step6](htmlconversion_images/AzureNetCore6.png) 

Step 4: Add an Export to the PDF button in the index.cshtml.

{% highlight c# tabtitle="C#" %}

<div class="btn">
    @{ Html.BeginForm("ExportToPDF", "Home", FormMethod.Post);
        {
            <input type="submit" value="Export To PDF" class=" btn" />
        }
    }
</div>

{% endhighlight %}

Step 5: Include the following namespaces.

{% highlight c# tabtitle="C#" %}

using Syncfusion.HtmlConverter;
using Syncfusion.Pdf;
using System.IO;

{% endhighlight %}

Step 6: Add the code samples in the controller to convert HTML to PDF document using [Convert](https://help.syncfusion.com/cr/file-formats/Syncfusion.HtmlConverter.HtmlToPdfConverter.html#Syncfusion_HtmlConverter_HtmlToPdfConverter_Convert_System_String_) method in [HtmlToPdfConverter](https://help.syncfusion.com/cr/file-formats/Syncfusion.HtmlConverter.HtmlToPdfConverter.html) class. The Blink command line arguments based on the given [CommandLineArguments](https://help.syncfusion.com/cr/file-formats/Syncfusion.HtmlConverter.BlinkConverterSettings.html#Syncfusion_HtmlConverter_BlinkConverterSettings_CommandLineArguments) property of [BlinkConverterSettings](https://help.syncfusion.com/cr/file-formats/Syncfusion.HtmlConverter.BlinkConverterSettings.html) class. .

{% highlight c# tabtitle="C#" %}

public ActionResult ExportToPDF()
{
    Environment.SetEnvironmentVariable("ASPNETCORE_ENVIRONMENT", "Development");
    //Install the dependencies packages for HTML to PDF conversion in Linux
    string shellFilePath = System.IO.Path.Combine(env.ContentRootPath, "dependenciesInstall.sh");
    InstallDependecies(shellFilePath);
    //Initialize HTML to PDF converter 
    HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter();
    BlinkConverterSettings settings = new BlinkConverterSettings();
    //Set command line arguments to run without sandbox.
    settings.CommandLineArguments.Add("--no-sandbox");
    settings.CommandLineArguments.Add("--disable-setuid-sandbox");
    //Assign BlinkConverter settings to the HTML converter 
    htmlConverter.ConverterSettings = settings;
    //Convert HTML string to PDF
    PdfDocument document = htmlConverter.Convert("http://www.syncfusion.com");
    //Save the document into stream
    MemoryStream stream = new MemoryStream();
    document.Save(stream);
    stream.Position = 0;
    //Close the document
    document.Close(true);
    //Defining the ContentType for pdf file
    string contentType = "application/pdf";
    //Define the file name
    string fileName = "URL_to_PDF.pdf";
    //Creates a FileContentResult object by using the file contents, content type, and file name
    return File(stream, contentType, fileName);
}

private void InstallDependecies(string shellFilePath)
{
    Process process = new Process
    {
        StartInfo = new ProcessStartInfo
        {
            FileName = "/bin/bash",
            Arguments = "-c " + shellFilePath,
            CreateNoWindow = true,
            UseShellExecute = false,
        }
    };
    process.Start();
    process.WaitForExit();
}

{% endhighlight %}

**Steps to publish as Azure App Linux**

Step 1: Right-click the project and select Publish.
![Convert HTMLToPDF Azure NetCore Step7](htmlconversion_images/AzureNetCore7.png)   

Step 2: Create a new profile in publish target window.
![Convert HTMLToPDF Azure NetCore Step8](htmlconversion_images/AzureNetCore8.png) 

Step 3: Create App service using Azure subscription and select a hosting plan.
![Convert HTMLToPDF Azure NetCore Step9](htmlconversion_images/AzureNetCore9.png) 

Step 4: HTML to PDF conversion works from basic hosting plan (B1 to P3). So, select the hosting plan as required. HTML to PDF conversion will not work if the hosting plan is Free/Shared.
![Convert HTMLToPDF Azure NetCore Step10](htmlconversion_images/AzureNetCore10.png) 

Step 5: After creating a profile, click the publish button.
![Convert HTMLToPDF Azure NetCore Step11](htmlconversion_images/AzureNetCore11.png)

Now, the published webpage will open in the browser. Click Export to PDF button to convert Syncfusion webpage to PDF document.
![Convert HTMLToPDF Azure NetCore Step12](htmlconversion_images/htmltopdfoutput.png)

A complete work sample for converting an HTML to PDF in Azure App service on Linux can be downloaded from [GitHub](https://github.com/SyncfusionExamples/html-to-pdf-csharp-examples/tree/master/Azure/HTML_to_PDF_Azure_app_service).

## Azure App Service Linux with docker

**Steps to convert HTML to PDF in Azure app service using Blink with Linux docker container**

Step 1: Create a new ASP.NET Core application and enable the docker support with Linux as a target OS.
![Convert HTMLToPDF Azure Docker Step1](htmlconversion_images/DockerStep1.png)

Step 2: Choose your project's target framework, select Configure for HTTPS and Enable Docker.
![Convert HTMLToPDF Azure Docker Step2](htmlconversion_images/DockerStep2.png)

Step 3: Install the [Syncfusion.HtmlToPdfConverter.Net.Linux](https://www.nuget.org/packages/Syncfusion.HtmlToPdfConverter.Net.Linux/) NuGet package as a reference to your .NET Core application [NuGet.org](https://www.nuget.org/).

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

![Convert HTMLToPDF Azure Docker Step](htmlconversion_images/DockerStep.PNG)

Step 4: Include the following commands in the docker file to install the dependent packages in the docker container.

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

Step 5: Add a new button in the Index.cshtml file.

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

Step 6: Include the following namespaces.

{% highlight c# tabtitle="C#" %}

using Syncfusion.HtmlConverter;
using Syncfusion.Pdf;
using System.IO;

{% endhighlight %}

Step 7: Add the code samples in the controller to convert HTML to PDF document using [Convert](https://help.syncfusion.com/cr/file-formats/Syncfusion.HtmlConverter.HtmlToPdfConverter.html#Syncfusion_HtmlConverter_HtmlToPdfConverter_Convert_System_String_) method in [HtmlToPdfConverter](https://help.syncfusion.com/cr/file-formats/Syncfusion.HtmlConverter.HtmlToPdfConverter.html) class. The Blink command line arguments based on the given [CommandLineArguments](https://help.syncfusion.com/cr/file-formats/Syncfusion.HtmlConverter.BlinkConverterSettings.html#Syncfusion_HtmlConverter_BlinkConverterSettings_CommandLineArguments) property of [BlinkConverterSettings](https://help.syncfusion.com/cr/file-formats/Syncfusion.HtmlConverter.BlinkConverterSettings.html) class.   

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

Step 8: Build and run the sample in docker, it will pull the Linux docker image from the docker hub and run the project. Now, the webpage will open in the browser and click the button to convert the Syncfusion webpage to a PDF.
![Convert HTMLToPDF Azure Docker Step6](htmlconversion_images/AzureDocker9.png) 

By executing the program, you will get the PDF document as follows.
![HTML to PDF output document](htmlconversion_images/htmltopdfoutput.png) 

**Deploy the container to Azure container instance**

Step 1: Create a publish target to deploy the docker image to Azure. 
![Convert HTMLToPDF Azure Docker Step8](htmlconversion_images/AzureDocker3.png) 

Step 2: Create Azure App Service with resource group, hosting plan, and container registry. 
![Convert HTMLToPDF Azure Docker Step9](htmlconversion_images/AzureDocker4.png) 

Step 3: Publish the docker image to Azure container instance.
![Convert HTMLToPDF Azure Docker Step10](htmlconversion_images/AzureDocker5.png) 

Step 4: It will push the docker image to the Azure container registry and deploy it to the Azure container instance.
![Convert HTMLToPDF Azure Docker Step11](htmlconversion_images/AzureDocker6.png)  

Step 5: After successful deployment, it will open the Azure website in the browser.
![Convert HTMLToPDF Azure Docker button](htmlconversion_images/AzureDocker9.png)

Step 6: Click the button to convert Syncfusion webpage to a PDF document. You will get the PDF document as follows. 
![Convert HTMLToPDF Azure Docker Output](htmlconversion_images/htmltopdfoutput.png)

A complete work sample can be downloaded from [Github](https://github.com/SyncfusionExamples/html-to-pdf-csharp-examples/tree/master/Azure/HTML_to_PDF_Azure_app_service_docker)

## Azure App Function Linux

**Steps to convert HTML to PDF in the Azure Functions using the Blink rendering engine**
Step 1: Create the Azure function project.
![Convert HTMLToPDF Azure Functions Step1](htmlconversion_images/AzureFunctions1.png)

Step 2: Select the Azure Functions type and .NET Core version.
![Convert HTMLToPDF Azure Functions Step2](htmlconversion_images/AzureFunctions2.png)

Step 3: Install the [Syncfusion.HtmlToPdfConverter.Net.Linux](https://www.nuget.org/packages/Syncfusion.HtmlToPdfConverter.Net.Linux/) NuGet package as a reference to your .NET Core application [NuGet.org](https://www.nuget.org/).
![Convert HTMLToPDF Azure Functions Step3](htmlconversion_images/AzureFunctions3.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 4: Include the following namespaces in Function1.cs file.

{% highlight c# tabtitle="C#" %}

using Syncfusion.HtmlConverter;
using Syncfusion.Pdf;
using System.Runtime.InteropServices;

{% endhighlight %}

Step 5: Add the following code example in the Function1 class to convert HTML to PDF document using [Convert](https://help.syncfusion.com/cr/file-formats/Syncfusion.HtmlConverter.HtmlToPdfConverter.html#Syncfusion_HtmlConverter_HtmlToPdfConverter_Convert_System_String_) method in [HtmlToPdfConverter](https://help.syncfusion.com/cr/file-formats/Syncfusion.HtmlConverter.HtmlToPdfConverter.html) class. The Blink command line arguments based on the given [CommandLineArguments](https://help.syncfusion.com/cr/file-formats/Syncfusion.HtmlConverter.BlinkConverterSettings.html#Syncfusion_HtmlConverter_BlinkConverterSettings_CommandLineArguments) property of [BlinkConverterSettings](https://help.syncfusion.com/cr/file-formats/Syncfusion.HtmlConverter.BlinkConverterSettings.html) class. 
{% highlight c# tabtitle="C#" %}

    [FunctionName("Function1")]
    public static async Task<IActionResult> Run([HttpTrigger(AuthorizationLevel.Function, "get", "post", Route = null)] HttpRequest req, ILogger log, ExecutionContext executionContext)
    {
        string blinkBinariesPath = string.Empty;
        try
        {
            blinkBinariesPath = SetupBlinkBinaries(executionContext);
        }
        catch
        {
            throw new Exception("BlinkBinaries initialization failed");
        }
        string url = req.Query["url"];
        //Initialize the HTML to PDF converter with the Blink rendering engine.
        HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter(HtmlRenderingEngine.Blink);
        BlinkConverterSettings settings = new BlinkConverterSettings();
        //Set command line arguments to run without sandbox.
        settings.CommandLineArguments.Add("--no-sandbox");
        settings.CommandLineArguments.Add("--disable-setuid-sandbox");
        settings.BlinkPath = blinkBinariesPath;
        //Assign BlinkConverter settings to the HTML converter 
        htmlConverter.ConverterSettings = settings;
        //Convert URL to PDF
        PdfDocument document = htmlConverter.Convert(url);
        MemoryStream ms = new MemoryStream();
        //Save and close the PDF document  
        document.Save(ms);
        document.Close();
        ms.Position = 0;
        return new FileStreamResult(ms, "application/pdf");
    }

{% endhighlight %}

Step 6: Add the following helper methods to copy and set permission to the BlinkBinariesLinux folder.

{% highlight c# tabtitle="C#" %}

    private static string SetupBlinkBinaries(ExecutionContext executionContext)
    {
        string blinkAppDir = Path.Combine(executionContext.FunctionAppDirectory, "BlinkBinariesLinux");
        string tempBlinkDir = Path.GetTempPath();
        string chromePath = Path.Combine(tempBlinkDir, "chrome");
        if (!File.Exists(chromePath))
        {
            CopyFilesRecursively(blinkAppDir, tempBlinkDir);
            SetExecutablePermission(tempBlinkDir);
        }
        return tempBlinkDir;
    }
    private static void CopyFilesRecursively(string sourcePath, string targetPath)
    {
        //Create all the directories from the source to the destination path.
        foreach (string dirPath in Directory.GetDirectories(sourcePath, "*", SearchOption.AllDirectories))
        {
            Directory.CreateDirectory(dirPath.Replace(sourcePath, targetPath));
        }
        //Copy all the files from the source path to the destination path.
        foreach (string newPath in Directory.GetFiles(sourcePath, "*.*", SearchOption.AllDirectories))
        {
            File.Copy(newPath, newPath.Replace(sourcePath, targetPath), true);
        }
    }
    [DllImport("libc", SetLastError = true, EntryPoint = "chmod")]
    internal static extern int Chmod(string path, FileAccessPermissions mode);
    private static void SetExecutablePermission(string tempBlinkDir)
    {
        FileAccessPermissions ExecutableFilePermissions = FileAccessPermissions.UserRead | FileAccessPermissions.UserWrite | FileAccessPermissions.UserExecute |
        FileAccessPermissions.GroupRead | FileAccessPermissions.GroupExecute | FileAccessPermissions.OtherRead | FileAccessPermissions.OtherExecute;
        string[] executableFiles = new string[] { "chrome", "chrome_sandbox" };
        foreach (string executable in executableFiles)
        {
            var execPath = Path.Combine(tempBlinkDir, executable);
            if (File.Exists(execPath))
            {
                var code = Function1.Chmod(execPath, ExecutableFilePermissions);
                if (code != 0)
                {
                    throw new Exception("Chmod operation failed");
                }
            }
        }
    }
{% endhighlight %}

Step 7: Include the below enum in the Function1.cs file. 

{% highlight c# tabtitle="C#" %}

[Flags]
internal enum FileAccessPermissions : uint
{
    OtherExecute = 1,
    OtherWrite = 2,
    OtherRead = 4,
    GroupExecute = 8,
    GroupWrite = 16,
    GroupRead = 32,
    UserExecute = 64,
    UserWrite = 128,
    UserRead = 256
}       

{% endhighlight %}

**Publish to Azure Functions Linux**

Step 1: Right-click the project and select Publish. Then, create a new profile in the Publish Window. The Blink rendering engine will work in consumption plan. So, you can create the Azure Function App service with a consumption plan.
![Convert HTMLToPDF Azure Functions Step4](htmlconversion_images/AzureFunctions4.png)

Step 2: After creating the profile, click the Publish button.
![Convert HTMLToPDF Azure Functions Step5](htmlconversion_images/AzureFunctions5.png)

Step 3: Now, go to the Azure portal and select the App Services. After running the service, click Get function URL > Copy. Include the URL as a query string in the URL. Then, paste it into the new browser tab. You will get the PDF document as follows.
![Convert HTMLToPDF Azure Functions Step6](htmlconversion_images/htmltopdfoutput.png)

A complete working sample can be downloaded from [Github](https://github.com/SyncfusionExamples/html-to-pdf-csharp-examples/tree/master/Azure/HTML_to_PDF_Azure_functions)

Click [here](https://www.syncfusion.com/document-processing/pdf-framework/net-core/html-to-pdf) to explore the rich set of Syncfusion HTML to PDF converter library features. 

An online sample link to [convert HTML to PDF document](https://ej2.syncfusion.com/aspnetcore/PDF/HtmltoPDF#/material3) in ASP.NET Core. 