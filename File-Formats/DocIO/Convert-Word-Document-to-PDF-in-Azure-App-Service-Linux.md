---
title: Convert Word to PDF in Azure App Service on Linux | Syncfusion
description: Convert Word to PDF in Azure App Service on Linux using .NET Core Word (DocIO) library without Microsoft Word or interop dependencies. 
platform: file-formats
control: DocIO
documentation: UG
---

# Convert Word to PDF in Azure App Service on Linux

Syncfusion DocIO is a [.NET Core Word library](https://www.syncfusion.com/document-processing/word-framework/net-core/word-library) used to create, read, edit and **convert Word documents** programmatically without **Microsoft Word** or interop dependencies. Using this library, you can **convert a Word document to PDF in Azure App service on Linux**.

## Steps to convert Word document to PDF in Azure App Service on Linux

Step 1: Create a new ASP.NET Core Web App (Model-View-Controller).
![Create a ASP.NET Core Web App project](Azure_Images/App_Service_Linux/Create-Project-WordtoPDF.png)

Step 2: Create a project name and select the location.
![Configure your new project](Azure_Images/App_Service_Linux/Configure_Project_WordtoPDF.png)

Step 3: Click **Create** button.
![Additional Information](Azure_Images/App_Service_Linux/Additional_Information_WordtoPDF.png)

Step 4: Install the following **Nuget packages** in your application from [Nuget.org](https://www.nuget.org/).

* [Syncfusion.DocIORenderer.Net.Core](https://www.nuget.org/packages/Syncfusion.DocIORenderer.Net.Core) 
* [SkiaSharp.NativeAssets.Linux v2.88.2](https://www.nuget.org/packages/SkiaSharp.NativeAssets.Linux)

 ![Install Syncfusion.DocIORenderer.Net.Core Nuget Package](Azure_Images/App_Service_Linux/Syncfusion_Nuget_Package_WordtoPDF.png)
 ![Install SkiaSharp.NativeAssets.Linux Nuget Package](Azure_Images/App_Service_Linux/SkiaSharp_Nuget-Package_WordtoPDF.png)

Step 5: Add a new button in the **Index.cshtml** as shown below.

{% tabs %}

{% highlight c# tabtitle="C#" %}
@{Html.BeginForm("WordToPDF", "Home", FormMethod.Post, new { enctype = "multipart/form-data" });
 
{
    <div class="Common">
        <div class="tablediv">
            <div class="rowdiv">
                This sample illustrates how to convert Word document to PDF using .NET Word library (DocIO) and .NET PDF library (PDF).
            </div>
            &nbsp;
            <div class="rowdiv" style="border-width: 0.5px;border-style:solid; border-color: lightgray; padding: 1px 5px 7px 5px">
            Click the button to view the resultant PDF document being converted from Word document using DocIO. Please note that PDF viewer is required to view the resultant PDF.
                    <div class="rowdiv" style="margin-top: 10px">
                        <div class="celldiv">
                            Select Document :
                            @Html.TextBox("file", "", new { type = "file", accept = ".docx" }) <br />
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
        </div>
    </div>
    Html.EndForm();
    }
}
{% endhighlight %}

{% endtabs %}

Step 6: Include the following namespaces in **HomeController.cs**.

{% tabs %}

{% highlight c# tabtitle="C#" %}

using Syncfusion.DocIO;
using Syncfusion.DocIO.DLS;
using Syncfusion.DocIORenderer;
using Syncfusion.Pdf;

{% endhighlight %}

{% endtabs %}

Step 7: Include the below code snippet in **HomeController.cs** for **convert the Word document to Pdf**.

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
        if (extension == ".docx")
        {
            MemoryStream stream = new MemoryStream();
            Request.Form.Files[0].CopyTo(stream);
            try
            {
                //Open using Syncfusion
                using (WordDocument document = new WordDocument(stream, FormatType.Docx))
                {
                    stream.Dispose();                         
                    // Creates a new instance of DocIORenderer class.
                    using (DocIORenderer render = new DocIORenderer())
                    {
                        // Converts Word document into PDF document
                        using (PdfDocument pdf = render.ConvertToPDF(document))
                        {                                                                     
                            MemoryStream memoryStream = new MemoryStream();
                            // Save the PDF document
                            pdf.Save(memoryStream);
                            memoryStream.Position = 0;                       
                            return File(memoryStream, "application/pdf", "WordToPDF.pdf");
                        }                                                           
                    } 
                }                                                
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


{% endhighlight %}

{% endtabs %}

## Steps to publish as Azure App Service on Linux

Step 1: Right-click the project and select **Publish** option.
![Right-click the project and select the Publish option](Azure_Images/App_Service_Linux/Publish_WordtoPDF.png)

Step 2: Click the **Add a Publish Profile** button.
![Click the Add a Publish Profile](Azure_Images/App_Service_Linux/Publish_Profile_WordtoPDF.png)

Step 3: Select the publish target as **Azure**.
![Select the publish target as Azure](Azure_Images/App_Service_Linux/Publish_Target_WordtoPDF.png)

Step 4: Select the Specific target as **Azure App Service (Linux)**.
![Select the publish target](Azure_Images/App_Service_Linux/Specific_Target_WordtoPDF.png)

Step 5: To create a new app service, click **Create new** option.
![Click create new option](Azure_Images/App_Service_Linux/Create_New_App_Service_WordtoPDF.png)

Step 6: Click the **Create** button to proceed with **App Service** creation.
![Click the Create button](Azure_Images/App_Service_Linux/Hosting_Plan_WordtoPDF.png)

Step 7: Click the **Finish** button to finalize the **App Service** creation.
![Click the Finish button](Azure_Images/App_Service_Linux/App_Service_WordtoPDF.png)

Step 8: Click **Close** button.
![Create a ASP.NET Core Project](Azure_Images/App_Service_Linux/Publish_Finish_WordtoPDF.png)

Step 9: Click the **Publish** button.
![Click the Publish button](Azure_Images/App_Service_Linux/Before_Publish_WordtoPDF.png)

Step 10: Now, Publish has been succeeded.
![Publish has been succeeded](Azure_Images/App_Service_Linux/After_Publish_WordtoPDF.png)

Step 11: Now, the published webpage will open in the **browser**.
![Browser will open after publish](Azure_Images/App_Service_Linux/Browser_WordtoPDF.png)

Step 12: Select the Word document and Click **Convert to PDF** to convert the given Word document to a PDF.You will get the output PDF document as follows.

![Word to PDF in Azure App Service on Linux](WordToPDF_images/WordToPDF_Output_Cloud.png)

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Convert-Word-document-to-PDF/Azure/Azure_App_Service).
