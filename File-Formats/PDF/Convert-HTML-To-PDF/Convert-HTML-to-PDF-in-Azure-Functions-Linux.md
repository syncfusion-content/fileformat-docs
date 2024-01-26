---
title: Convert HTML to PDF in Azure Functions Linux| Syncfusion
description: Learn how to convert HTML to PDF in Azure Linux with easy steps using Syncfusion .NET HTML to PDF converter library.
platform: file-formats
control: PDF
documentation: UG
---

# Convert HTML to PDF in Azure Functions Linux

The Syncfusion [HTML to PDF converter](https://www.syncfusion.com/document-processing/pdf-framework/net/html-to-pdf) is a .NET Core library for converting webpages, SVG, MHTML, and HTML to PDF using C#. The result preserves all graphics, images, text, fonts, and the layout of the original HTML document or webpage. Using this library, you can convert an HTML to PDF using C# with the Blink rendering engine in Azure Functions Linux.

N> HTML to PDF converter is not supported with Azure App Service windows. We internally use Blink rendering engine for the conversion, it uses GDI calls for viewing and rendering the webpages. But Azure app service blocks GDI calls in the Azure website environment. As the Azure website does not have the elevated permission and enough rights, we can not launch the Chrome headless browser in the Azure app service windows (Azure website and Azure function).

## Steps to convert HTML to PDF in the Azure Functions using the Blink rendering engine

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
        string blinkAppDir = Path.Combine(executionContext.FunctionAppDirectory, "bin/runtimes/linux/native");
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

Click [here](https://www.syncfusion.com/document-processing/pdf-framework/net-core/html-to-pdf) to explore the rich set of Syncfusion HTML to PDF converter library features. 

An online sample link to [convert HTML to PDF document](https://ej2.syncfusion.com/aspnetcore/PDF/HtmltoPDF#/material3) in ASP.NET Core. 