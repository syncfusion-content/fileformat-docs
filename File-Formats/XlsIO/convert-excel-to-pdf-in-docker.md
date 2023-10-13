---
title: Convert an Excel document to PDF in Linux Docker | Syncfusion
description: Convert an Excel document to PDF in Linux Docker using Sycfusion .NET Core Excel library (XlsIO) without Microsoft Excel or interop dependencies.
platform: file-formats
control: XlsIO
documentation: UG
---

# Convert an Excel document to PDF in Linux Docker

Docker is an open platform for developing, shipping and running applications. You can use Essential XlsIO in Docker container to create, read, write and convert Microsoft Excel documents into various formats. From this page, you can learn how to **convert an Excel document to PDF in Linux Docker** using Syncfusion XlsIO library (Essential XlsIO).

## Steps to convert an Excel document to PDF in Linux Docker

Step 1: Create a new Core Console application.
<img src="Docker_Images/docker_images_img1.png" alt="Create a Console Application" width="100%" Height="Auto"/>

Step 2: Name the project.
<img src="Docker_Images/docker_images_img2.png" alt="Name the project" width="100%" Height="Auto"/>

Step 3: Install the below NuGet packages as a reference to your project from [NuGet.org](https://www.nuget.org/).

* [Syncfusion.XlsIORenderer.Net.Core](https://www.nuget.org/packages/Syncfusion.XlsIORenderer.Net.Core)
* [SkiaSharp.NativeAssets.Linux v2.80.2](https://www.nuget.org/packages/SkiaSharp.NativeAssets.Linux/2.80.2) 

<img src="Docker_Images/docker_images_img3.png" alt="Install Syncfusion.XlsIORenderer.Net.Core NuGet Package" width="100%" Height="Auto"/>

<img src="Docker_Images/docker_images_img4.png" alt="Install SkiaSharp.NativeAssets.Linux v2.80.2 NuGet Package" width="100%" Height="Auto"/>

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your applications to use our components.

Step 4: Include the following namespaces in the **Program.cs** file.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using Syncfusion.XlsIO;
using Syncfusion.Pdf;
using Syncfusion.XlsIORenderer;
{% endhighlight %}
{% endtabs %}

Step 5: Add the following code snippet in **Program.cs** file.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;
    FileStream excelStream = new FileStream("InputTemplate.xlsx", FileMode.Open, FileAccess.Read);
    IWorkbook workbook = application.Workbooks.Open(excelStream);

    //Initialize XlsIO renderer.
    XlsIORenderer renderer = new XlsIORenderer();

    //Convert Excel document into PDF document 
    PdfDocument pdfDocument = renderer.ConvertToPDF(workbook);

    //Create the FileStream to save the converted PDF.
    FileStream pdfStream = new FileStream("Output.pdf", FileMode.Create, FileAccess.ReadWrite);
    pdfDocument.Save(pdfStream);
}
{% endhighlight %}
{% endtabs %}

Step 6: Add Docker support to that application by clicking <b>Add -> Docker Support.</b>

<img src="Docker_Images/docker_images_img5.png" alt="Add Docker support to that console app" width="100%" Height="Auto"/>

Step 7: Choose Linux option in order to run the application in Linux Docker container.

<img src="Docker_Images/docker_images_img6.png" alt="Choose Linux option" width="100%" Height="Auto"/>

Step 8: Open the **Dockerfile** to see the default Docker commands that are shown below.

{% tabs %}
{% highlight Dockerfile %}

FROM mcr.microsoft.com/dotnet/runtime:3.1 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["Convert-Excel-to-PDF.csproj", "."]
RUN dotnet restore "./Convert-Excel-to-PDF.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "Convert-Excel-to-PDF.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Convert-Excel-to-PDF.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Convert-Excel-to-PDF.dll"]

{% endhighlight %}
{% endtabs %}

Step 8: Select Docker option and Run the application.

<img src="Docker_Images/docker_images_img7.png" alt="Choose docker and run application" width="100%" Height="Auto"/>

A complete working example of how to convert an Excel document to PDF in docker container is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Getting%20Started/Docker).

By executing the program, you will get the **PDF document** as follows.

<img src="Docker_Images/docker_images_img8.png" alt="Output file" width="100%" Height="Auto"/>

## Dockerfile Examples

The following examples demonstrate how the Docker file should be configured in order to convert an Excel document to PDF in different Linux distributions.

## Alpine

You can use the below Dockerfile to convert an Excel document to PDF in Alpine Linux.

{% tabs %}
{% highlight Dockerfile %}

FROM mcr.microsoft.com/dotnet/aspnet:3.1-alpine3.12 AS base
RUN apk update && apk upgrade && apk add fontconfig
RUN apk add --update ttf-dejavu fontconfig
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:3.1-alpine3.12 AS build
WORKDIR /src
COPY ["Convert-Excel-to-PDF.csproj", "."]
RUN dotnet restore "./Convert-Excel-to-PDF.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "Convert-Excel-to-PDF.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Convert-Excel-to-PDF.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Convert-Excel-to-PDF.dll"]

{% endhighlight %}
{% endtabs %}

A complete working example of converting an Excel document to PDF in Alpine Linux Docker container is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Getting%20Started/Docker/Alpine/Convert%20Excel%20to%20PDF).

## Debian

You can use the below Dockerfile to convert an Excel document to PDF in Debian Linux.

{% tabs %}
{% highlight Dockerfile %}

FROM mcr.microsoft.com/dotnet/aspnet:3.1-buster-slim AS base
RUN apt-get update -y && apt-get install fontconfig -y
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:3.1-buster-slim AS build
WORKDIR /src
COPY ["Convert-Excel-to-PDF.csproj", "."]
RUN dotnet restore "./Convert-Excel-to-PDF.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "Convert-Excel-to-PDF.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Convert-Excel-to-PDF.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Convert-Excel-to-PDF.dll"]

{% endhighlight %}
{% endtabs %}

A complete working example of converting an Excel document to PDF in Debian Linux Docker container is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Getting%20Started/Docker/Debian/Convert%20Excel%20to%20PDF).

## RHEL - Red Hat Enterprise Linux

You can use the below Dockerfile to convert an Excel document to PDF in RHEL Linux.

{% tabs %}
{% highlight Dockerfile %}

FROM registry.access.redhat.com/ubi8/dotnet-31-runtime AS base
USER root
RUN yum -y install fontconfig --disablerepo=epel
WORKDIR /

FROM registry.access.redhat.com/ubi8/dotnet-31 AS build
WORKDIR /src
COPY ["Convert-Excel-to-PDF.csproj", ""]
RUN dotnet restore "./Convert-Excel-to-PDF.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "Convert-Excel-to-PDF.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Convert-Excel-to-PDF.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Convert-Excel-to-PDF.dll"]

{% endhighlight %}
{% endtabs %}

A complete working example of converting an Excel document to PDF in RHEL Linux Docker container is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Getting%20Started/Docker/RHEL/Convert%20Excel%20to%20PDF).

## Ubuntu

You can use the below Dockerfile to convert an Excel document to PDF in Ubuntu Linux.

{% tabs %}
{% highlight Dockerfile %}

FROM mcr.microsoft.com/dotnet/core/runtime:3.1-bionic AS base
RUN apt-get update -y && apt-get install fontconfig -y
WORKDIR /app

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-bionic AS build
WORKDIR /src
COPY ["Convert-Excel-to-PDF.csproj", ""]
RUN dotnet restore "./Convert-Excel-to-PDF.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "Convert-Excel-to-PDF.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Convert-Excel-to-PDF.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Convert-Excel-to-PDF.dll"]

{% endhighlight %}
{% endtabs %}

A complete working example of converting an Excel document to PDF in Ubuntu Linux Docker container is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Getting%20Started/Docker/Ubuntu/Convert%20Excel%20to%20PDF).

Click [here](https://www.syncfusion.com/document-processing/excel-framework/net-core) to explore the rich set of Syncfusion Excel library (XlsIO) features.

An online sample link to [convert an Excel document to PDF](https://ej2.syncfusion.com/aspnetcore/Excel/ExcelToPDF#/material3) in ASP.NET Core.