---
title: Convert Word document to PDF in Azure App service on Linux | Syncfusion
description: Convert Word document to PDF in Azure App service on Linux using .NET Core Word (DocIO) library without Microsoft Word or interop dependencies.
platform: file-formats
control: DocIO
documentation: UG
---

# How to convert Word document to PDF in Azure App service on Linux

Syncfusion  DocIO is a [.NET Core Word library](https://www.syncfusion.com/document-processing/word-framework/net-core/word-library) used to create, read, and edit Word documents programmatically without **Microsoft Word** or **interop** dependencies. Using this library, you can **convert a Word document to PDF in Azure App Service on Linux**.

## Steps to convert Word document to PDF in Azure App service on Linux:

Step 1: Create a new ASP.NET Core app (Model-View Controller).
![Create ASP.NET Core Web app (Model-View Controller) in Visual Studio](Azure_App_Service_Images/Create-Project-WordtoPDF.png)

Step 2: Install the [Syncfusion.DocIORenderer.Net.Core](https://www.nuget.org/packages/Syncfusion.DocIORenderer.Net.Core/) NuGet package as a reference to your .NET Core application from NuGet.org.

![Install Syncfusion.DocIORenderer.Net.Core Nuget Package](Azure_App_Service_Images/Nuget-Package-WordtoPDF.png)

Step 3: Install the [SkiaSharp.NativeAssets.Linux](https://www.nuget.org/packages/SkiaSharp.NativeAssets.Linux) NuGet package as a reference to your .NET Core application from NuGet.org.

![Install SkiaSharp.NativeAssets.Linux Nuget Package](Azure_App_Service_Images/Nuget-Package-Skia-WordtoPDF-.png)

Step 4: Create a Font folder in the ``wwwroot`` folder of the project and copy the required fonts and include the files to the project.

![Create folder and copy required fonts](Azure_App_Service_Images/Folder-WordtoPDF.png)

Step 5:Set the **copy to output directory** to **Copy if newer** to all the data files.

![Change property of Word document](Azure_App_Service_Images/Change-Property-WordtoPDF.png)

Step 6: Add an Export To PDF button in index.cshtml.

{% tabs %}

{% highlight c# tabtitle="C#" %}


@{Html.BeginForm("WordToPDF", "Home", FormMethod.Post, new { enctype = "multipart/form-data" });

{
    <div class="Common">
        <div class="tablediv">
            <div class="rowdiv">
                This sample illustrates how to convert Word document to PDF using Essential DocIO and Essential PDF.
            </div>
            &nbsp;
            <div class="rowdiv" style="border-width: 0.5px;border-style:solid; border-color: lightgray; padding: 1px 5px 7px 5px">
            Click the button to view the resultant PDF document being converted from Word document using Essential DocIO and Essential PDF. Please note that PDF viewer is required to view the resultant PDF.
            <div class="rowdiv" style="margin-top: 10px">
                <div class="celldiv">
                    Select Document :
                    @Html.TextBox("file", "", new { type = "file", accept = ".doc,.docx,.rtf,.dot,.dotm,.dotx,docm,.xml" }) <br />
                </div>
                <div class="rowdiv" style="margin-top: 8px">
                    <input class="buttonStyle" type="submit" value="Convert to PDF" name="button" style="width:150px;height:27px" />
                    <br />
                    <div class="text-danger">
                                @ViewBag.Message
                    </div>
                </div>
            </div>
        </div>
        <br />
        <div class="rowdiv" style="margin-top: 15px">
        More information about Word to PDF conversion can be found in this
        <a href="https://help.syncfusion.com/file-formats/docio/conversion#converting-word-document-to-pdf">documentation</a>
        section.
            </div>
        </div>
    </div>
        Html.EndForm();
    }
}

Step 8: Include the following namespace in that HomeController.cs file.

{% tabs %}

{% highlight c# tabtitle="C#" %}

using Syncfusion.DocIO;
using Syncfusion.DocIO.DLS;
using Syncfusion.DocIORenderer;
using Syncfusion.Pdf;
using Microsoft.AspNetCore.Hosting;

{% endhighlight %}

{% endtabs %}

Step 7: Add a new action method **WordToPDF** in HomeController.cs and include the below code snippet to **convert the Word document to PDF**.

{% tabs %}

{% highlight c# tabtitle="C#" %}

private IHostingEnvironment _env;
public HomeController(IHostingEnvironment env)
{
    _env = env;
}

/// <summary>
/// Convert Word document to PDF
/// </summary>
/// <param name="button"></param>
/// <returns></returns>
public IActionResult WordToPDF(string button)
{
    string fileLoadTime = "";
    string domLoadTime = "";
    string conversionTime = "";
    string saveTime = "";
    if (button == null)
        return View("Index");

    if (Request.Form.Files != null)
    {
        if (Request.Form.Files.Count == 0)
        {
            ViewBag.Message = string.Format("Browse a Word document and then click the button to convert as a PDF document");
            return View("Index");
        }
        // Gets the extension from file.
        string extension = Path.GetExtension(Request.Form.Files[0].FileName).ToLower();
        // Compares extension with supported extensions.
        if (extension == ".doc" || extension == ".docx" || extension == ".dot" || extension == ".dotx" || extension == ".dotm" || extension == ".docm"|| extension == ".xml" || extension == ".rtf")
        {
            MemoryStream stream = new MemoryStream();
            Request.Form.Files[0].CopyTo(stream);
            try
            {
                //Open using Syncfusion
                WordDocument document = new WordDocument(stream, Syncfusion.DocIO.FormatType.Automatic);
                document.FontSettings.SubstituteFont += FontSettings_SubstituteFont;
                stream.Dispose();
                stream = null;
                // Creates a new instance of DocIORenderer class.
                DocIORenderer render = new DocIORenderer();
                // Converts Word document into PDF document.
                PdfDocument pdf = render.ConvertToPDF(document);
                document.FontSettings.SubstituteFont -= FontSettings_SubstituteFont;
                MemoryStream memoryStream = new MemoryStream();
                // Save the PDF document.                    
                //Save using Syncfusion
                pdf.Save(memoryStream);
                memoryStream.Position = 0;
                ViewBag.OS = string.Format(System.Environment.OSVersion.ToString());
                ViewBag.Load = string.Format("FileLoadTime\t" + fileLoadTime);
                ViewBag.DomLoad = "DomLoadTime\t" + domLoadTime;
                ViewBag.Conversion = "ConversionTime\t" + conversionTime;
                ViewBag.Save = "SaveTime\t" + saveTime;
                return File(memoryStream, "application/pdf", "WordToPDF.pdf");
            }
            catch (Exception ex)
            {
                ViewBag.Message = ex.ToString();
            }
        }
        else
        {
            ViewBag.Message = string.Format("Please choose Word format document to convert to PDF");
        }
    }
    else
    {
        ViewBag.Message = string.Format("Browse a Word document and then click the button to convert as a PDF document");
    }
    return View("Index");
}

/// <summary>
/// Sets the alternate font when a specified font is not installed in the production environment
/// </summary>
/// <param name="sender"></param>
/// <param name="args"></param>
private void FontSettings_SubstituteFont(object sender, SubstituteFontEventArgs args)
{
    string filePath = string.Empty;

    //Load the file from the disk
    FileStream fileStream = null;
    //Sets the alternate font when a specified font is not installed in the production environment
    //If "Arial Unicode MS" font is not installed, then it uses the "Arial" font
    //For other missing fonts, uses the "Times New Roman"
    if (args.OriginalFontName == "Calibri")
    {
        filePath = _env.WebRootPath + @"/Fonts/calibri.ttf";
        fileStream = new FileStream(filePath, FileMode.Open, FileAccess.Read);
        args.AlternateFontStream = fileStream;
    }
    else if (args.OriginalFontName == "Arial")
    {
        filePath = _env.WebRootPath + @"/Fonts/arial.ttf";
        fileStream = new FileStream(filePath, FileMode.Open, FileAccess.Read);
        args.AlternateFontStream = fileStream;
    }
    else
    {
        filePath = _env.WebRootPath + @"/Fonts/times.ttf";
        fileStream = new FileStream(filePath, FileMode.Open, FileAccess.Read);
        args.AlternateFontStream = fileStream;
    }
}

{% endhighlight %}
{% endtabs %}

Step 9: Refer to the following steps to publish as **Azure App Linux**. Right-click the project and select Publish.:

![Right-click the project and select Publish](Azure_App_Service_Images/Publish-WordtoPDF.png)

Step 10: Click  Add a publish profile
![Add a publish profile](Azure_App_Service_Images/Publish-Profile-WordtoPDF.png)

Step 11: Select target as **Azure** and click Next button
![Right-click the project and select Publish](Azure_App_Service_Images/Target-Azure-WordtoPDF.png)

Step 12: Select specific target as **Azure App Service (Linux)** and click Next button.
![Select specific target as Azure App Service (Linux)](Azure_App_Service_Images/Specific-Target-WordtoPDF.png)

Step 13: Create App service using Azure subscription and select a hosting plan.
![Create App service using Azure subscription](Azure_App_Service_Images/Hosting-WordtoPDF.png)

Step 14: The Syncfusion DocIO library works from basic hosting plan (B1). So, select the required hosting plan. It does not work if the hosting plan is Free/Shared.
![Configure Hosting Plan](Azure_App_Service_Images/Configure-WordtoPDF.png)

Step 15: After creating a profile, click the publish button.
![Click the Publish button](Azure_App_Service_Images/Create-profile-WordtoPDF.png)

Step 16: Now, the published webpage will open in the browser. Select the Word document and Click **Convert to PDF** to convert the given Word document to a PDF.
![Published webpage](Azure_App_Service_Images/Published-Webpage-WordtoPDF.png)

A complete work sample for converting an Word document to PDF in Azure App service on Linux can be downloaded from [AzureAppServiceOnLinux](https://www.syncfusion.com/downloads/support/directtrac/general/ze/AzureAppSeviceLinux198349282?_gl=1*18f3efu*_ga*NTA2MDIxMjkzLjE2NzI3MzYzODM.*_ga_WC4JKKPHH0*MTY4NDIyMjg4NS4xMTQuMS4xNjg0MjIyOTIzLjIyLjAuMA..)

By executing the program, you will get the **PDF document** as follows.

![Output PDF document in Azure Service app on Linux](WordToPDF_images/OutputImage.png)

Take a moment to peruse the [documentation](https://help.syncfusion.com/file-formats/docio/getting-started), where you can find basic Word document processing options along with features like [mail merge](https://help.syncfusion.com/file-formats/docio/working-with-mail-merge), [merge](https://help.syncfusion.com/file-formats/docio/word-document/merging-word-documents) and [split](https://help.syncfusion.com/file-formats/docio/word-document/split-word-documents) documents, [find and replace](https://help.syncfusion.com/file-formats/docio/working-with-find-and-replace) text in the Word document, [protect](https://help.syncfusion.com/file-formats/docio/working-with-security) the Word documents, and most importantly [PDF](https://help.syncfusion.com/file-formats/docio/word-to-pdf) and [Image](https://help.syncfusion.com/file-formats/docio/word-to-image) conversions with code examples.

Explore more about the rich set of Syncfusion [Word Framework](https://www.syncfusion.com/word-framework) features.

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, include a license key in your projects. Refer to [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to learn about generating and registering Syncfusion license key in your application to use the components without trail message.