---
title: Convert Word to PDF in Linux | Syncfusion
description: Convert Word to PDF in Linux using .NET Core Word (DocIO) library without Microsoft Word or interop dependencies.
platform: file-formats
control: DocIO
documentation: UG
---

# Convert Word document to PDF in Linux

Syncfusion DocIO is a [.NET Core Word library](https://www.syncfusion.com/document-processing/word-framework/net-core/word-library) used to create, read, edit, and **convert Word documents** programmatically without **Microsoft Word** or interop dependencies. Using this library, you can **convert a Word document to PDF in .NET Core application on Linux**.

## Steps to convert a Word document to PDF in .NET Core application on Linux

Step 1: Execute the following command in **Linux terminal** to create a new .NET Core Console application.

{% tabs %}
{% highlight KCONFIG %}

dotnet new console

{% endhighlight %}
{% endtabs %}

![Create .NET Core console application on Linux](Linux-images/CreateNewProject1.png)

Step 2: Install the following **Nuget packages** in your application from [Nuget.org](https://www.nuget.org/) by execute the following command.

* [Syncfusion.DocIORenderer.Net.Core](https://www.nuget.org/packages/Syncfusion.DocIORenderer.Net.Core) 
* [SkiaSharp.NativeAssets.Linux v2.88.6](https://www.nuget.org/packages/SkiaSharp.NativeAssets.Linux/2.88.6)
* [HarfBuzzSharp.NativeAssets.Linux v2.8.2.2](https://www.nuget.org/packages/HarfBuzzSharp.NativeAssets.Linux/2.8.2.2)

{% tabs %}
{% highlight KCONFIG %}

dotnet add package Syncfusion.DocIORenderer.Net.Core -v 22.1.34 -s https://www.nuget.org/
dotnet add package SkiaSharp.NativeAssets.Linux -v 2.88.6 -s https://www.nuget.org/
dotnet add package HarfBuzzSharp.NativeAssets.Linux -v 2.8.2.2 -s https://www.nuget.org/

{% endhighlight %}
{% endtabs %}

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your applications to use our components.

Step 3: Add the following Namespaces in **Program.cs** file.

{% tabs %}
{% highlight c# tabtitle="C#" %}

using Syncfusion.DocIO;
using Syncfusion.DocIO.DLS;
using Syncfusion.DocIORenderer;
using Syncfusion.Pdf;

{% endhighlight %}
{% endtabs %}

Step 4: Add the following code snippet in **Program.cs** file.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Open the file as Stream
using (FileStream docStream = new FileStream("Data/Template.docx", FileMode.Open, FileAccess.Read))
{
    //Loads an existing Word document
    using (WordDocument wordDocument = new WordDocument(docStream, FormatType.Docx))
    {
        //Instantiation of DocIORenderer for Word to PDF conversion
        using (DocIORenderer render = new DocIORenderer())
        {
            //Converts Word document into PDF document
            using (PdfDocument pdfDocument = render.ConvertToPDF(wordDocument))
            {
                //Create FileStream to save the PDF file.
                using (FileStream outputStream = new FileStream("Result.pdf", FileMode.Create, FileAccess.ReadWrite, FileShare.ReadWrite))
                {
                    //Saves the PDF file.
                    pdfDocument.Save(outputStream);
                }
            }
        }
    }
}

{% endhighlight %}
{% endtabs %}

Step 5: Execute the following command to **restore** the NuGet packages.

{% tabs %}
{% highlight KCONFIG %}

dotnet restore

{% endhighlight %}
{% endtabs %}

![Restore the NuGet packages](Linux-images/Restore.png)

Step 6: Execute the following command in **terminal** to **run the application**.

{% tabs %}
{% highlight KCONFIG %}

dotnet run

{% endhighlight %}
{% endtabs %}

![Run the Applcation](Linux-images/Run.png)

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Convert-Word-document-to-PDF/Linux/Convert-Word-Document-to-PDF).

By executing the program, you will get the **PDF** as follows. The output will be saved in parallel to program.cs file.

![Word to PDF in Linux](WordToPDF_images/OutputImage.png)

Click [here](https://www.syncfusion.com/document-processing/word-framework/net-core) to explore the rich set of Syncfusion Word library (DocIO) features. 

An online sample link to [convert Word document to PDF](https://ej2.syncfusion.com/aspnetcore/Word/WordToPDF#/material3) in ASP.NET Core. 