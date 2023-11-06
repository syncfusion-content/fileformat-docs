---
title: Convert an Excel document to PDF in ASP.NET MVC | Syncfusion
description: Convert an Excel document to PDF in ASP.NET MVC using Sycfusion .NET Excel library (XlsIO) without Microsoft Excel or interop dependencies.
platform: file-formats
control: XlsIO
documentation: UG
---

# Convert an Excel document to PDF in ASP.NET MVC

Syncfusion XlsIO is a [.NET Excel library](https://www.syncfusion.com/document-processing/excel-framework/net/excel-library) used to create, read, edit and **convert Excel documents** programmatically without **Microsoft Excel** or interop dependencies. Using this library, you can **convert an Excel document to PDF in ASP.NET MVC**.

## Steps to convert an Excel document to PDF in C#

Step 1: Create a new ASP.NET Web Application Project.
<img src="ASP-NET-MVC_images\ASP-NET-MVC_images_img4.png" alt="Create a ASP.NET Web App project" width="100%" Height="Auto"/>

Step 2: Name the project, choose the framework and click **Create** button.
<img src="ASP-NET-MVC_images\ASP-NET-MVC_images_img5.png" alt="Name the project and choose the framework version" width="100%" Height="Auto"/>

Step 3: Select the MVC application.
<img src="ASP-NET-MVC_images\ASP-NET-MVC_images_img6.png" alt="Select the MVC App" width="100%" Height="Auto"/>

Step 4: Install the [Syncfusion.ExcelToPdfConverter.AspNet.Mvc5](https://www.nuget.org/packages/Syncfusion.ExcelToPdfConverter.AspNet.Mvc5) NuGet package as a reference to your project from [NuGet.org](https://www.nuget.org/).
<img src="ASP-NET-MVC_images\ASP-NET-MVC_images_img7.png" alt="Install Syncfusion.ExcelToPdfConverter.AspNet.Mvc5 NuGet Package" width="100%" Height="Auto"/>

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your applications to use our components. 

Step 5: Add a new button in the **Index.cshtml** as shown below.
{% tabs %}  
{% highlight CSHTML %}
@{Html.BeginForm("ConvertExceltoPDF", "Home", FormMethod.Get);
    {
        <div>
            <input type="submit" value="Convert Excel to PDF" style="width:150px;height:27px" />
        </div>
    }
    Html.EndForm();
}
{% endhighlight %}
{% endtabs %}

Step 6: Include the following namespaces in **HomeController.cs**.
{% tabs %}
{% highlight c# tabtitle="C#" %}
using Syncfusion.XlsIO;
using Syncfusion.Pdf;
using Syncfusion.ExcelToPdfConverter;
{% endhighlight %}
{% endtabs %}

Step 7: Include the below code snippet in **HomeController.cs** to **convert an Excel document to PDF**. 
{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  FileStream excelStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize ExcelToPdfConverter
  ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);

  //Initialize PDF document
  PdfDocument pdfDocument = new PdfDocument();

  //Convert Excel document into PDF document
  pdfDocument = converter.Convert();

  //Create the MemoryStream to save the converted PDF.      
  MemoryStream pdfStream = new MemoryStream();

  //Save the converted PDF document to MemoryStream.
  pdfDocument.Save(pdfStream);
  pdfStream.Position = 0;

  //Download PDF document in the browser.
  return File(pdfStream, "application/pdf", "Sample.pdf");
}
{% endhighlight %}
{% endtabs %}

A complete working example of how to convert an Excel document to PDF in ASP.NET MVC is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Getting%20Started/ASP.NET%20MVC/Convert%20Excel%20to%20PDF).

By executing the program, you will get the **PDF document** as follows.

<img src="ASP-NET-MVC_images\ASP-NET-MVC_images_img8.png" alt="Excel to PDF in ASP.NET MVC" width="100%" Height="Auto"/>

Click [here](https://www.syncfusion.com/document-processing/excel-framework/net) to explore the rich set of Syncfusion Excel library (XlsIO) features.

An online sample link to [convert an Excel document to PDF](https://ej2.syncfusion.com/aspnetmvc/Excel/ExcelToPDF#/material3) in ASP.NET MVC.
