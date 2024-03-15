---
title: Convert PDF file to Image in ASP.NET Core | Syncfusion
description: Learn how to convert a PDF file to Image in ASP.NET Core with easy steps using Syncfusion PDF TO Image Converter library.
platform: file-formats
control: PDF to image
documentation: UG
keywords: Assemblies
---

# Convert PDF file to Image in ASP.NET Core

The Syncfusion PDF to Image converter is a .NET library used to convert PDF document to image in ASP.NET Core application.

## Steps to convert PDF document to Image in ASP.NET Core application

Step 1: Create a new C# ASP.NET Core Web Application project.
![Create ASP.NET Core Web application](Asp.Net.Core_images/aspnetcore1.png)

Step 2:  In configuration windows, name your project and select Next.
![Configuration window1](Asp.Net.Core_images/aspnetcore2.png)
![Configuration window2](Asp.Net.Core_images/aspnetcore3.png)

Step 3:  Install [Syncfusion.PdfToImageConverter.Net](https://www.nuget.org/packages/Syncfusion.PdfToImageConverter.Net/) NuGet package as reference to your .NET Standard applications from [NuGet.org](https://www.nuget.org/).

N> If you want to use the PdfToImageConverter in the Linux environment, you need to install the [SkiaSharp.NativeAssets.Linux v2.88.6](https://www.nuget.org/packages/SkiaSharp.NativeAssets.Linux/2.88.6) NuGet package as reference to your applications from [NuGet.org](https://www.nuget.org/).

Step 4: A default controller with name HomeController.cs gets added on creation of ASP.NET Core project. Include the following namespaces in that HomeController.cs file.

{% highlight c# tabtitle="C#" %}

using Syncfusion.PdfToImageConverter;

{% endhighlight %}

Step 5: Add a new button in index.cshtml as shown below.

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
Stream outputStream = imageConverter.Convert(0, false, false);
MemoryStream stream = outputStream as MemoryStream;
byte[] bytes = stream.ToArray();
using (FileStream output = new FileStream("output.png", FileMode.OpenOrCreate, FileAccess.ReadWrite))
{
    output.Write(bytes, 0, bytes.Length);
}

{% endhighlight %}

By executing the program, you will get the image as follows.
![Convert PDFToImage output](GettingStarted_images/pdftoimageoutput.png)