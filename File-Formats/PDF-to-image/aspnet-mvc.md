---
title: Convert PDF document to Image in ASP.NET MVC | Syncfusion
description: Learn how to convert a PDF file to Image in ASP.NET MVC with easy steps using System Drawing library.
platform: file-formats
control: PDF
documentation: UG
keywords: Assemblies
---

# Convert PDF file to Image in ASP.NET MVC

The Syncfusion PDF to Image converter is a .NET library used to convert PDF document to image in ASP.NET MVC application.  

## Steps to convert PDF document to Image in ASP.NET MVC

Step 1: Create a new C# ASP.NET Web Application (.NET Framework) project.
![Create ASP.NET MVC application](imageconversion_images/aspnetmvc1.png)   

Step 2: In the project configuration windows, name your project and select Create.
![Configuration window1](imageconversion_images/aspnetmvc2.png)   
![Configuration window2](imageconversion_images/aspnetmvc3.png)   

Step 3: Install Syncfusion.PdfToImageConverter.Base NuGet package as reference to your .NET applications from [NuGet.org](https://www.nuget.org/).

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 4: Include the following namespaces in the HomeController.cs file.

{% highlight c# tabtitle="C#" %}

using Syncfusion.PdfToImageConverter;
using System.Drawing;
using System.IO;

{% endhighlight %}

Step 5: Add a new button in the Index.cshtml as shown below.

{% highlight c# tabtitle="C#" %}

@{Html.BeginForm("ExportToImage", "Home", FormMethod.Post);
    {
        <div>
            <input type="submit" value="Convert Image" style="width:150px;height:27px" />
        </div>
    }
    Html.EndForm();
 }

{% endhighlight %}

Step 6: Add a new action method named ExportToImage in HomeController.cs and include the below code example to convert PDF document to Image using Convert method in PdfToImageConverter class.

{% highlight c# tabtitle="C#" %}

//Initialize PDF to Image converter.
PdfToImageConverter imageConverter = new PdfToImageConverter();
//Load the PDF document as a stream
FileStream inputStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.ReadWrite);
imageConverter.Load(inputStream);
//Convert PDF to Image.
Stream outputStream = imageConvertor.Convert(0, false, false);
return File(outputStream.ToArray(), System.Net.Mime.MediaTypeNames.Image.Png, "sample.pdf");

{% endhighlight %}

By executing the program, you will get the image as follows.
![Convert PDFToImage WPF output](imageconversion_images/pdftoimageoutput.png)
