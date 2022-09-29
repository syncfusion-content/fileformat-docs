---
title: Convert a HTML to PDF file in ASP.NET MVC | Syncfusion
description: Learn how to convert a HTML to PDF file in ASP.NET MVC with easy steps using Syncfusion .NET HTML converter library.
platform: file-formats
control: PDF
documentation: UG
keywords: Assemblies
---

# Convert HTML to PDF file in ASP.NET MVC

The Syncfusion HTML to PDF converter is a .NET library used to convert HTML or web pages to PDF. Using this library can convert HTML to PDF in ASP.NET MVC application.  

## Steps to convert HTML to PDF document in ASP.NET MVC

Create a new C# ASP.NET Web Application (.NET Framework) project.
![convert_HtmltoPdf_ASP.NET_MVC1](htmlconversion_images/aspnetmvc1.png)

Install Syncfusion.HtmlToPdfConverter.AspNet.Mvc5  NuGet package as reference to your .NET applications from NuGet.org.
![convert_HtmltoPdf_ASP.NET_MVC2](htmlconversion_images/aspnetmvc2.png)

Include the following namespaces in that HomeController.cs file.

{% highlight c# tabtitle="C#" %}

using Syncfusion.Pdf;
using Syncfusion.HtmlConverter;

{% endhighlight %}

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

Add a new action method ExportToPDF in HomeController.cs and include the below code snippet to convert HTML to PDF.

{% highlight c# tabtitle="C#" %}

// Initialize HTML to PDF converter.
HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter();

// Convert URL to PDF.
PdfDocument document = htmlConverter.Convert("https://www.syncfusion.com");

MemoryStream stream = new MemoryStream();

document.Save(stream);

return File(stream.ToArray(), System.Net.Mime.MediaTypeNames.Application.Pdf, "HTML-to-PDF.pdf");
{% endhighlight %}

A complete working demo can be downloaded from [HTMLToPdf.zip](https://www.syncfusion.com/downloads/support/directtrac/general/ze/HTML-to-PDF-MVC-Demo1437749865)

By executing the program, you will get the PDF document as follows.
![convert_HtmltoPdf_ASP.NET_MVC1](htmlconversion_images/htmltopdfoutput.png)
