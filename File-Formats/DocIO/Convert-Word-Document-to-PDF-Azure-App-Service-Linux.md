---
title: Convert Word document to PDF in Azure App service on Linux | Syncfusion
description: Convert Word document to PDF in Azure App service on Linux using .NET Core Word (DocIO) library without Microsoft Word or interop dependencies.
platform: file-formats
control: DocIO
documentation: UG
---

# Convert Word to PDF in Azure App service on Windows

Syncfusion  DocIO is a [.NET Core Word library](https://www.syncfusion.com/document-processing/word-framework/net/word-library) used to create, read, edit and **convert Word documents** programmatically without **Microsoft Word** or interop dependencies. Using this library, you can **convert a Word document to PDF in Azure App service on Linux**

## Steps to convert Word document to PDF in Azure App service on Linux:

Step 1: Create a new ASP.NET Core Web App(Model-View-Controller).
![Create a ASP.NET Core Web App project](Azure_Images/App_Service_Windows/Create-Project-WordtoPDF.png)

Step 2: Create a project name and select the location.
![Configure your new project](Azure_Images/App_Service_Linux/Configure_Project_WordtoPDF.png)

Step 3: Click **Create** button
![Additional Information](Azure_Images/App_Service_Windows/Additional_Information_WordtoPDF.png)

Step 3: Install the following **Nuget packages**.

* [Syncfusion.DocIORenderer.Net.Core](https://www.nuget.org/packages/Syncfusion.DocIORenderer.Net.Core) 
* [SkiaSharp.NativeAssets.Linux](https://www.nuget.org/packages/SkiaSharp.NativeAssets.Linux)

NuGet package as a reference to your .NET Core application from NuGet.org.
 ![Install Syncfusion.DocIORenderer.Net.Core Nuget Package](Azure_Images/App_Service_Windows/Syncfusion_Nuget_Package_WordtoPDF.png)
 ![Install SkiaSharp.NativeAssets.Linux Nuget Package](Azure_Images/App_Service_Windows/SkiaSharp_Nuget-Package_WordtoPDF.png)


Step 5: Create a folder in the `wwwroot` folder of the project and copy the required **fonts** and include the files to the project.

![Create a folder](Azure_Images/App_Service_Windows/Font-Folder-WordtoPDF.png)

Step 6: Set the **copy to output directory** to **Copy if newer** to all the data files.
![Change the property of the font](Azure_Images/App_Service_Windows/Font-Property-WordtoPDF.png)

Step 7: Add a new button in the **Index.cshtml** as shown below.

{% tabs %}

{% highlight c# tabtitle="C#" %}
@{
    Html.BeginForm("WordToPDF", "Home", FormMethod.Post, new { enctype = "multipart/form-data" });

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
{% endhighlight %}

{% endtabs %}

Step 8: Include the following namespaces in **HomeController.cs**.

{% tabs %}

{% highlight c# tabtitle="C#" %}

using Syncfusion.DocIO;
using Syncfusion.DocIO.DLS;
using Syncfusion.DocIORenderer;
using Syncfusion.Pdf;
using Microsoft.AspNetCore.Hosting;

{% endhighlight %}

{% endtabs %}

Step 9: Include the below code snippet in **HomeController.cs** for  **convert the Word document to Pdf**.

{% tabs %}

{% highlight c# tabtitle="C#" %}

private Microsoft.AspNetCore.Hosting.IHostingEnvironment _env;
public HomeController(Microsoft.AspNetCore.Hosting.IHostingEnvironment env)
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
        if (extension == ".doc" || extension == ".docx" || extension == ".dot" || extension == ".dotx" || extension == ".dotm" || extension == ".docm" || extension == ".xml" || extension == ".rtf")
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


## Refer the following steps to publish as Azure App service Linux

Step 1: Right-click the project and select **Publish** option.
![Right-click the project and select the Publish option](Azure_Images/App_Service_Windows/Publish_WordtoPDF.png)

Step 2: Click the **Add a Publish Profile** button
![Click the Add a Publish Profile](Azure_Images/App_Service_Windows/Publish_Profile_WordtoPDF.png)

Step 3: Select the publish target as **Azure**.
![Select the publish target as Azure](Azure_Images/App_Service_Windows/Publish_Target_WordtoPDF.png)

Step 4: Select the Specific target as **Azure App Service (Linux)**.
![Select the publish target](Azure_Images/App_Service_Linux/Specific_Target_WordtoPDF.png)

Step 5: To create a new app service, click **Create new** option.

![Click create new option](Azure_Images/App_Service_Windows/Create_New_App_Service_WordtoPDF.png)


Step 6: Click the **Create** button to proceed with **App Service** creation.
![Click the Create button](Azure_Images/App_Service_Windows/Hosting_Plan_WordtoPDF.png)

Step 7: Click the **Finish** button to finalize the **App Service** creation.
![Click the Finish button](Azure_Images/App_Service_Windows/App_Service_WordtoPDF.png)

Step 8: Click **Close** button.
![Create a ASP.NET Core  Project](Azure_Images/App_Service_Windows/Publish_Finish_WordtoPDF.png)

Step 9: Click the **Publish** button.
![Click the Publish button](Azure_Images/App_Service_Windows/Before_Publish_WordtoPDF.png)

Step 10: Now, Publish has been succeeded.
![Publish has been succeeded](Azure_Images/App_Service_Windows/After_Publish_WordtoPDF.png)

Step 11: Now, the published webpage will open in the **browser**. Select the Word document and Click **Convert to PDF** to convert the given Word document to a PDF.
