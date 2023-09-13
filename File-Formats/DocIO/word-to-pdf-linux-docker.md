---
title: Word document to PDF Conversion in Linux Docker | DocIO | Syncfusion
description: This section illustrates how to convert Word document to PDF using Syncfusion Word library (Essential DocIO) in Linux Docker
platform: file-formats
control: DocIO
documentation: UG
---

# Essential DocIO in Docker

Docker is an open platform for developing, shipping and running applications. You can use Essential DocIO in Docker container to create, read, write and convert Microsoft Word documents into various formats. From this page, you can learn how to convert Word document to PDF in Linux Docker using Syncfusion Word library (Essential DocIO). 

## Steps to convert a Word document to PDF in Linux Docker

Step 1: Create a new Core Console application.

![Create console app](linuxdockerimages/create-console-app-in-file-formats-word.png)
![Name console app](linuxdockerimages/name-console-app-in-file-formats-word.png)

Step 2: Install the below NuGet packages as a reference to your project from [NuGet.org](https://www.nuget.org/).

* [Syncfusion.DocIORenderer.Net.Core](https://www.nuget.org/packages/Syncfusion.DocIORenderer.Net.Core/)
* [SkiaSharp.NativeAssets.Linux v2.80.2](https://www.nuget.org/packages/SkiaSharp.NativeAssets.Linux/2.80.2) 
* [HarfBuzzSharp.NativeAssets.Linux v2.8.2.2](https://www.nuget.org/packages/HarfBuzzSharp.NativeAssets.Linux/2.8.2.2) 

![Install DocIO Renderer NuGet package](linuxdockerimages/install-renderer-nuget-in-file-formats-word.png)
![Install Skiasharp NuGet package](linuxdockerimages/install-skia-sharp-nuget-in-file-formats-word.png)

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

Step 3: Include the following namespaces in the Program.cs file.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using System.IO;
using Syncfusion.DocIO.DLS;
using Syncfusion.DocIORenderer;
using Syncfusion.Pdf;
{% endhighlight %}
{% endtabs %}

Step 4: Add the following code snippet in Program.cs file.

{% tabs %}
{% highlight c# tabtitle="C#" %}
//Open the file as Stream
using (FileStream docStream = new FileStream(@"Adventure.docx", FileMode.Open, FileAccess.Read))
{
    //Loads file stream into Word document
    using (WordDocument wordDocument = new WordDocument(docStream, Syncfusion.DocIO.FormatType.Automatic))
    {
        //Instantiation of DocIORenderer for Word to PDF conversion
        using (DocIORenderer render = new DocIORenderer())
        {
            //Converts Word document into PDF document
            using (PdfDocument pdfDocument = render.ConvertToPDF(wordDocument))
            {
                //Saves the PDF file
                using (FileStream outputStream = new FileStream("Output.pdf", FileMode.OpenOrCreate, FileAccess.ReadWrite))
                {
                    pdfDocument.Save(outputStream);
                }
            }
        }
    }
}
{% endhighlight %}
{% endtabs %}

Step 5: Add Docker support to that application by clicking <b>Add -> Docker Support.</b>

![Add Docker support to that console app](linuxdockerimages/docker-support-in-file-formats-word.png)

Step 6: Choose Linux option in order to run the application in Linux Docker container.

![Choose Linux option](linuxdockerimages/linux-option-in-file-formats-word.png)

Step 7: Open the Dockerfile to see the default Docker commands that are shown below.

{% tabs %}
{% highlight Dockerfile %}

FROM mcr.microsoft.com/dotnet/runtime:3.1 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["WordToPDFDockerSample.csproj", "."]
RUN dotnet restore "./WordToPDFDockerSample.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "WordToPDFDockerSample.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WordToPDFDockerSample.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WordToPDFDockerSample.dll"]

{% endhighlight %}
{% endtabs %}

Step 8: Select Docker option and Run the application.

![Run console app](linuxdockerimages/run-console-in-file-formats-word.png)

A complete working example of converting Word document to PDF in Linux Docker container can be downloaded from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Convert-Word-document-to-PDF/Docker/Debian/WordToPDFDockerSample).

Finally, you will get the converted PDF document as follows.

![Output PDF document](linuxdockerimages/pdf-output-document-in-file-formats-word.png)


## Dockerfile Examples

The following examples demonstrate how the Docker file should be configured in order to convert a Word document to PDF in different Linux distributions.

## Alpine

You can use the below Dockerfile to convert a Word document to PDF in Alpine Linux.

{% tabs %}
{% highlight Dockerfile %}

FROM mcr.microsoft.com/dotnet/aspnet:3.1-alpine3.12 AS base
RUN apk update && apk upgrade && apk add fontconfig
RUN apk add --update ttf-dejavu fontconfig
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:3.1-alpine3.12 AS build
WORKDIR /src
COPY ["WordToPDFDockerSample.csproj", "."]
RUN dotnet restore "./WordToPDFDockerSample.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "WordToPDFDockerSample.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WordToPDFDockerSample.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WordToPDFDockerSample.dll"]

{% endhighlight %}
{% endtabs %}

A complete working example of converting Word document to PDF in Alpine Linux Docker container can be downloaded from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Convert-Word-document-to-PDF/Docker/Alpine/WordToPDFDockerSample).

## CentOS

You can use the below Dockerfile to convert a Word document to PDF in CentOS Linux.

{% tabs %}
{% highlight Dockerfile %}

FROM centos:8

Run dnf install dotnet-sdk-3.1 -y
RUN dnf install dotnet-runtime-3.1 -y

RUN dnf install fontconfig -y

ENTRYPOINT ["dotnet" "WordToPDFDockerSample.dll"]

{% endhighlight %}
{% endtabs %}

A complete working example of converting Word document to PDF in CentOS Linux Docker container can be downloaded from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Convert-Word-document-to-PDF/Docker/CentOS/WordToPDFDockerSample).

## Debian

You can use the below Dockerfile to convert a Word document to PDF in Debian Linux.

{% tabs %}
{% highlight Dockerfile %}

FROM mcr.microsoft.com/dotnet/aspnet:3.1-buster-slim AS base
RUN apt-get update -y && apt-get install fontconfig -y
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:3.1-buster-slim AS build
WORKDIR /src
COPY ["WordToPDFDockerSample.csproj", "."]
RUN dotnet restore "./WordToPDFDockerSample.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "WordToPDFDockerSample.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WordToPDFDockerSample.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WordToPDFDockerSample.dll"]

{% endhighlight %}
{% endtabs %}

A complete working example of converting Word document to PDF in Debian Linux Docker container can be downloaded from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Convert-Word-document-to-PDF/Docker/Debian/WordToPDFDockerSample).

## Fedora

You can use the below Dockerfile to convert a Word document to PDF in Fedora Linux.

{% tabs %}
{% highlight Dockerfile %}

FROM fedora:latest

Run dnf install dotnet-sdk-3.1 -y
RUN dnf install dotnet-runtime-3.1 -y

RUN dnf install fontconfig -y

ENTRYPOINT ["dotnet" "WordToPDFDockerSample.dll"]

{% endhighlight %}
{% endtabs %}

A complete working example of converting Word document to PDF in Fedora Linux Docker container can be downloaded from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Convert-Word-document-to-PDF/Docker/Fedora/WordToPDFDockerSample).

## RHEL - Red Hat Enterprise Linux

You can use the below Dockerfile to convert a Word document to PDF in RHEL Linux.

{% tabs %}
{% highlight Dockerfile %}

FROM registry.access.redhat.com/ubi8/dotnet-31-runtime AS base
USER root
RUN yum -y install fontconfig --disablerepo=epel
WORKDIR /

FROM registry.access.redhat.com/ubi8/dotnet-31 AS build
WORKDIR /src
COPY ["WordToPDFDockerSample.csproj", ""]
RUN dotnet restore "./WordToPDFDockerSample.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "WordToPDFDockerSample.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WordToPDFDockerSample.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WordToPDFDockerSample.dll"]

{% endhighlight %}
{% endtabs %}

A complete working example of converting Word document to PDF in RHEL Linux Docker container can be downloaded from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Convert-Word-document-to-PDF/Docker/RHEL/WordToPDFDockerSample).

## Ubuntu

You can use the below Dockerfile to convert a Word document to PDF in Ubuntu Linux.

{% tabs %}
{% highlight Dockerfile %}

FROM mcr.microsoft.com/dotnet/core/runtime:3.1-bionic AS base
RUN apt-get update -y && apt-get install fontconfig -y
WORKDIR /app

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-bionic AS build
WORKDIR /src
COPY ["WordToPDFDockerSample.csproj", ""]
RUN dotnet restore "./WordToPDFDockerSample.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "WordToPDFDockerSample.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WordToPDFDockerSample.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WordToPDFDockerSample.dll"]

{% endhighlight %}
{% endtabs %}

A complete working example of converting Word document to PDF in Ubuntu Linux Docker container can be downloaded from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-to-PDF-Conversion/Convert-Word-document-to-PDF/Docker/Ubuntu/WordToPDFDockerSample).

Click [here](https://www.syncfusion.com/document-processing/word-framework/net-core) to explore the rich set of Syncfusion Word library (DocIO) features. 

An online sample link to [convert Word document to PDF](https://ej2.syncfusion.com/aspnetcore/Word/WordToPDF#/material3) in ASP.NET Core.