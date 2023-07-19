---
title: Create PDF document on Linux | Syncfusion
description: Create PDF document in .NET Core application on Linux using Syncfusion .NET Core PDF library without the dependency of Adobe Acrobat.
platform: file-formats
control: PDF
documentation: UG
Keywords: linux os save pdf, linux os load pdf, c# save pdf, c# load pdf
---

# Create PDF document on Linux

The Syncfusion [.NET Core PDF library](https://www.syncfusion.com/document-processing/pdf-framework/net-core/pdf-library?_gl=1*hkw2o1*_ga*OTcwNzc5NDkuMTY4MTEwMjEwNA..*_ga_WC4JKKPHH0*MTY4NjIwMzM2Ny4xOTkuMS4xNjg2MjA3OTA2LjM4LjAuMA..&_ga=2.247303364.1146118023.1685935856-97077949.1681102104) is used to create, read, and edit PDF documents programmatically without the dependency on Adobe Acrobat. Using this library, you can **create a PDF document in ASP.NET Core application on Linux**.

## Steps to create PDF document programmatically:

Step 1: Execute the following command in the Linux terminal to create a new .NET Core Console application project.

{% highlight c# tabtitle="C#" %}

dotnet new console

{% endhighlight %}

Step 2: Install the [Syncfusion.Pdf.Net.Core](https://www.nuget.org/packages/Syncfusion.Pdf.Net.Core) NuGet package as a reference to your project from [NuGet.org](https://www.nuget.org/) by executing the following command.

{% highlight c# tabtitle="C#" %}

dotnet add package Syncfusion.Pdf.Net.Core -v xx.x.x.xx -s https://www.nuget.org/

{% endhighlight %}

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from the trial setup or from the NuGet feed, you also have to add the "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering the Syncfusion license key in your application to use our components.

Step 3: Include the following Namespaces in the Program.cs file.

{% tabs %}

{% highlight c# tabtitle="C#" %}

using Syncfusion.Pdf;
using Syncfusion.Pdf.Graphics;
using Syncfusion.Drawing;
using System.IO;

{% endhighlight %}

{% endtabs %}

Step 4: Add the following code sample to the Program.cs file to **create a PDF document in the .NET Core application on Linux**.

{% tabs %}

{% highlight c# tabtitle="C#" %}

{% endhighlight %}

{% endtabs %}

Step 5: Execute the following command to restore the NuGet packages.

{% highlight c# tabtitle="C#" %}

dotnet restore

{% endhighlight %}

![Linux Build](GettingStarted_images/Linux_Build.png)

Step 6: Execute the following command in terminal to run the application.
{% highlight c# tabtitle="C#" %}

dotnet run

{% endhighlight %}

![Linux Run](GettingStarted_images/Linux_Run.png)

A complete working sample can be downloaded from [Github](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Open%20and%20Save%20PDF%20document/Linux/Open_and_Save_PDF_Linux).

By executing the program, you will get the **PDF document** as follows. The output will be saved in parallel to program.cs file.
![Linux output PDF document](GettingStarted_images/Open_and_save_output.png)

Click [here](https://www.syncfusion.com/document-processing/pdf-framework/net-core) to explore the rich set of Syncfusion PDF library features.