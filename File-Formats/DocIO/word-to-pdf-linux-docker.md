---
title: Word document to PDF Conversion in Linux Docker | DocIO | Syncfusion
description: This section illustrates how to convert Word document to PDF using Syncfusion Word library (Essential DocIO) in Linux Docker
platform: file-formats
control: DocIO
documentation: UG
---

# Essential DocIO in Docker

Docker is an open platform for developing, shipping, and running applications. You can use Essential DocIO in Docker container to create, read, write, and convert Microsoft Word documents to various formats. In this page, you can see how to convert Word document to PDF using Syncfusion Word library (Essential DocIO) in Linux Docker. 

## Steps to convert a Word document to PDF in Linux Docker

1. Create a new Core Console application.

![Create console app](LinuxDockerImages/Step-1.png)
![Name console app](LinuxDockerImages/Step-2.png)

2. Install below NuGet packages as a reference to your project from [NuGet.org](https://www.nuget.org/).

* [Syncfusion.DocIORenderer.Net.Core](https://www.nuget.org/packages/Syncfusion.DocIORenderer.Net.Core/)
* [SkiaSharp.NativeAssets.Linux v2.80.2](https://www.nuget.org/packages/SkiaSharp.NativeAssets.Linux/2.80.2) 

![Install DocIORenderer NuGet package](LinuxDockerImages/Step-3.png)
![Install Skiasharp NuGet package](LinuxDockerImages/Step-4.png)

3. Include the following namespaces in the Program.cs file.

{% tabs %}
{% highlight asp.net core %}

using System.IO;
using Syncfusion.DocIO.DLS;
using Syncfusion.DocIORenderer;
using Syncfusion.Pdf;

{% endhighlight %}
{% endtabs %}


4. Add the following code snippet in Program.cs file.

{% tabs %}
{% highlight asp.net core %}
//Open the file as Stream
FileStream docStream = new FileStream("Template.docx", FileMode.Open, FileAccess.Read);
//Loads file stream into Word document
WordDocument wordDocument = new WordDocument(docStream, Syncfusion.DocIO.FormatType.Automatic);
docStream.Dispose();
//Instantiation of DocIORenderer for Word to PDF conversion
DocIORenderer render = new DocIORenderer();
//Converts Word document into PDF document
PdfDocument pdfDocument = render.ConvertToPDF(wordDocument);
//Releases all resources used by the Word document and DocIO Renderer objects
render.Dispose();
wordDocument.Dispose();
//Saves the PDF file
FileStream outputStream = new FileStream("Output.pdf", FileMode.OpenOrCreate, FileAccess.ReadWrite);
pdfDocument.Save(outputStream);
//Closes the instance of PDF document object
pdfDocument.Close();
outputStream.Dispose();
{% endhighlight %}
{% endtabs %}

5. Add Docker support to that application by clicking <b>Add -> Docker Support.</b>

![Add Docker support to that console app](LinuxDockerImages/Step-5.png)

6. Choose Linux option in order to run the application in Linux Docker container.

![Choose Linux option](LinuxDockerImages/Step-6.png)

7. Open the DockerFile and you can see default Docker commands as below.

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


8. Select Docker option and Run the application.

![Run console app](LinuxDockerImages/Step-7.png)

Finally, you will get the converted PDF document as follows.

![Output PDF document](LinuxDockerImages/Step-8.png)


## Dockerfile Examples

The following examples demonstrate how the Docker file should be configured in order to convert a Word document to PDF in different Linux distributions.

## Alpine

You can use below Dockerfile to convert a Word document to PDF in Alpine Linux.

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

## CentOS

You can use below Dockerfile to convert a Word document to PDF in CentOS Linux.

{% tabs %}
{% highlight Dockerfile %}

FROM centos:8

Run dnf install dotnet-sdk-3.1 -y
RUN dnf install dotnet-runtime-3.1 -y

RUN dnf install fontconfig -y

ENTRYPOINT ["dotnet" "WordToPDFDockerSample.dll"]

{% endhighlight %}
{% endtabs %}

## Debian

You can use below Dockerfile to convert a Word document to PDF in Debian Linux.

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

## Fedora

You can use below Dockerfile to convert a Word document to PDF in Fedora Linux.

{% tabs %}
{% highlight Dockerfile %}

FROM fedora:latest

Run dnf install dotnet-sdk-3.1 -y
RUN dnf install dotnet-runtime-3.1 -y

RUN dnf install fontconfig -y

ENTRYPOINT ["dotnet" "WordToPDFDockerSample.dll"]

{% endhighlight %}
{% endtabs %}

## RHEL - Red Hat Enterprise Linux

You can use below Dockerfile to convert a Word document to PDF in RHEL Linux.

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

## Ubuntu

You can use below Dockerfile to convert a Word document to PDF in Ubuntu Linux.

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