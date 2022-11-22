---
title: Convert a HTML to PDF file in Mac | Syncfusion
description: Learn how to convert a HTML to PDF file in Mac with easy steps using Syncfusion .NET HTML converter library.
platform: file-formats
control: PDF
documentation: UG
keywords: Assemblies
---

# Convert HTML to PDF file in Mac

## Steps to convert HTML to PDF in ASP.NET Core MVC

1. Create a new C# ASP.NET Core Web Application project.
![Mac_step1](htmlconversion_images/mac_step1.png)

2. Select the Target Framework of your project.
![Mac_step2](htmlconversion_images/mac_step2.png)

3. Configure your application and click Create.
![Mac_step3](htmlconversion_images/mac_step3.png)

4. Install the [Syncfusion.HtmlToPdfConverter.Net.Mac](https://www.nuget.org/packages/Syncfusion.HtmlToPdfConverter.Net.Mac) NuGet package as reference to your .NET Standard applications from [NuGet.org](https://www.nuget.org/).
![Mac_step4](htmlconversion_images/mac_step4.png)

5. A default controller with name HomeController.cs gets added on creation of ASP.NET MVC project. Include the following namespaces in that HomeController.cs file.

   {% highlight c# tabtitle="C#" %}

   using Syncfusion.Pdf;
   using Syncfusion.HtmlConverter;
   using System.IO;
   using Microsoft.AspNetCore.Hosting;

   {% endhighlight %}

6. A default action method named Index will be present in HomeController.cs. Right click on Index method and select Go To View where you will be directed to its associated view page Index.cshtml.

   Add a new button in the Index.cshtml as shown below.

   {% highlight c# tabtitle="C#" %}

   @{Html.BeginForm("ExportToPDF", "Home", FormMethod.Post);
   {
     <div>
      <input type="submit" value="Convert PDF" style="width:150px;height:27px" />
     </div>
   }
   Html.EndForm();
   }

   {% endhighlight %}

7. Add a new action method ExportToPDF in HomeController.cs and include the below code snippet to convert HTML to PDF file and download it.

   {% highlight c# tabtitle="C#" %}

        public IActionResult ExportToPDF()
        {
            //Initialize HTML to PDF converter.
            HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter();
            //Convert URL to PDF.
            PdfDocument document = htmlConverter.Convert("https://www.syncfusion.com");
            MemoryStream stream = new MemoryStream();
            document.Save(stream);
            //Download the PDF document in the browser
            return File(stream.ToArray(), System.Net.Mime.MediaTypeNames.Application.Pdf, "HTML-to-PDF.pdf");
        }

   {% endhighlight %}

8. Right click the project and select Build.
![Mac_step5](htmlconversion_images/mac_step5.png)

9. After Build succeeded. Run the application.
![Mac_step6](htmlconversion_images/mac_step6.png)

10. A complete working sample can be downloaded from [Mac-HTML-to-PDF-Demo.zip](https://www.syncfusion.com/downloads/support/directtrac/general/ze/Mac-HTML-to-PDF-Demo514297355).

11. By executing the program, you will get the PDF document as follows.
![HTMLTOPDF](htmlconversion_images/htmltopdfoutput.png)
