---
title: Word document to PDF Conversion in Linux Docker | DocIO | Syncfusion
description: This section illustrates how to convert Word document to PDF using Syncfusion Word library (Essential DocIO) in Linux Docker
platform: file-formats
control: DocIO
documentation: UG
---

# Docker

Docker is an open platform for developing, shipping, and running applications. You can use Essential DocIO in Docker container to perform Word manipulation like create, read, write, and convert to various formats.

For converting a Word document to PDF, the following packages are required to be referenced in your application

* [Syncfusion.DocIORenderer.Net.Core](https://www.nuget.org/packages/Syncfusion.DocIORenderer.Net.Core/)
* [SkiaSharp.NativeAssets.Linux](https://www.nuget.org/packages/SkiaSharp.NativeAssets.Linux/2.80.3-preview.40) 


## Docker commands for various Linux distributions

### Alpine:

To run the application in Alpine Linux, use the following Dockerfile

{% tabs %}
{% highlight Dockerfile %}
FROM mcr.microsoft.com/dotnet/aspnet:3.1-alpine3.12 AS base
RUN apk update && apk upgrade && apk add fontconfig
RUN apk add --update ttf-dejavu fontconfig
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1-alpine3.12 AS build
WORKDIR /src
COPY ["WordToPDFDockerSample/WordToPDFDockerSample.csproj", "WordToPDFDockerSample/"]
RUN dotnet restore "WordToPDFDockerSample/WordToPDFDockerSample.csproj"
COPY . .
WORKDIR "/src/WordToPDFDockerSample"
RUN dotnet build "WordToPDFDockerSample.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WordToPDFDockerSample.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WordToPDFDockerSample.dll"]

{% endhighlight %}
{% endtabs %}

### CentOS:

To run the application in CentOS Linux, use the following Dockerfile

{% tabs %}
{% highlight Dockerfile %}

FROM centos:8

Run dnf install dotnet-sdk-3.1 -y
RUN dnf install dotnet-runtime-3.1 -y

RUN dnf install fontconfig -y

ENTRYPOINT ["dotnet" "WordToPDFDockerSample.dll"]

{% endhighlight %}
{% endtabs %}

### Debian:

To run the application in Debian Linux, use the following Dockerfile

{% tabs %}
{% highlight Dockerfile %}

FROM mcr.microsoft.com/dotnet/aspnet:3.1-buster-slim AS base
RUN apt-get update -y && apt-get install fontconfig -y
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1-buster-slim AS build
WORKDIR /src
COPY ["WordToPDFDockerSample/WordToPDFDockerSample.csproj", "WordToPDFDockerSample/"]
RUN dotnet restore "WordToPDFDockerSample/WordToPDFDockerSample.csproj"
COPY . .
WORKDIR "/src/WordToPDFDockerSample"
RUN dotnet build "WordToPDFDockerSample.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WordToPDFDockerSample.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ConsoleApp1.dll"]

{% endhighlight %}
{% endtabs %}

### Fedora:

To run the application in Fedora Linux, use the following Dockerfile

{% tabs %}
{% highlight Dockerfile %}

FROM fedora:latest

Run dnf install dotnet-sdk-3.1 -y
RUN dnf install dotnet-runtime-3.1 -y

RUN dnf install fontconfig -y

ENTRYPOINT ["dotnet" "WordToPDFDockerSample.dll"]

{% endhighlight %}
{% endtabs %}

### RHEL - Red Hat Enterprise Linux:

To run the application in RHEL Linux, use the following Dockerfile

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

### Ubuntu:

To run the application in Ubuntu Linux, use the following Dockerfile

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