---
title: Convert Word to PDF in ASP.NET MVC | Syncfusion
description: Convert Word to PDF in ASP.NET MVC using .NET Word (DocIO) library library without Microsoft Word or interop dependencies.
platform: file-formats
control: DocIO
documentation: UG
---

# Convert Word document to PDF in ASP.NET MVC

Syncfusion Essential DocIO is a [.NET Word library](https://www.syncfusion.com/document-processing/word-framework/net/word-library) used to create, read, edit, and **convert Word documents** programmatically without **Microsoft Word** or interop dependencies. Using this library, you can **convert a Word document to PDF in ASP.NET MVC**.

## Steps to convert Word document to PDF in C#

Step 1: Create a new ASP.NET Web Application project.

![Create ASP.NET MVC application in Visual Studio](ASP-NET-MVC_images/CreateProjectforConversion.png)

Step 2: Select the MVC application.

![Create ASP.NET MVC application in Visual Studio](ASP-NET-MVC_images/MVC.png)

Step 3: Install the [Syncfusion.DocToPdfConverter.AspNet.Mvc5](https://www.nuget.org/packages/Syncfusion.DocToPdfConverter.AspNet.Mvc5) NuGet package as a reference to your project from [NuGet.org](https://www.nuget.org/).

![Install DocIO ASP.NET MVC NuGet package](ASP-NET-MVC_images/NugetPackage.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 4: Include the following namespace in that HomeController.cs file.

{% tabs %}

{% highlight c# tabtitle="C#" %}

using Syncfusion.DocIO.DLS;
using Syncfusion.DocIO;
using Syncfusion.Pdf;
using Syncfusion.DocToPDFConverter;

{% endhighlight %}

{% endtabs %}

Step 5: A default action method named Index will be present in HomeController.cs. Right click on Index method and select **Go To View** where you will be directed to its associated view page **Index.cshtml**.

Step 6: Add a new button in the Index.cshtml as shown below.

{% tabs %}

{% highlight c# tabtitle="C#" %}

@{Html.BeginForm("ConvertWordtoPDF", "Home", FormMethod.Get);
{
<div>
    <input type="submit" value="Convert Word Document to PDF" style="width:220px;height:27px" />
</div>
}
Html.EndForm();
}

{% endhighlight %}

{% endtabs %}

Step 7: Add a new action method **ConvertWordDocumentToPDF** in HomeController.cs and include the below code snippet to **convert the Word document to PDF** and download it.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Open the file as Stream
using (FileStream docStream = new FileStream(Server.MapPath("~/App_Data/Template.docx"), FileMode.Open, FileAccess.Read))
{
    //Loads file stream into Word document
    using (WordDocument wordDocument = new WordDocument(docStream, FormatType.Docx))
    {
        //Instantiation of DocToPDFConverter for Word to PDF conversion
        using (DocToPDFConverter converter = new DocToPDFConverter())
        {
            //Converts Word document into PDF document
            using (PdfDocument pdfDocument = converter.ConvertToPDF(wordDocument))
            {
                //Saves the PDF document to MemoryStream.
                MemoryStream stream = new MemoryStream();
                pdfDocument.Save(stream);
                stream.Position = 0;

                //Download PDF document in the browser.
                return File(stream, "application/pdf", "Sample.pdf");
            }                       
        };                 
    }
}

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Convert-Word-document-to-PDF/ASP.NET-MVC).

By executing the program, you will get the **PDF document** as follows.

![Word to PDF in ASP.NET MVC](WordToPDF_images/OutputImage.png)

Click [here](https://www.syncfusion.com/document-processing/word-framework/net) to explore the rich set of Syncfusion Word library (DocIO) features. 

An online sample link to [convert Word document to PDF](https://ej2.syncfusion.com/aspnetmvc/Word/DOCtoPDF#/material3) in ASP.NET MVC 