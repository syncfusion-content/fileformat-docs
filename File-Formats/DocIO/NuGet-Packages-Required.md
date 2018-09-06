---
title: NuGet Packages Required
description: NuGet Packages required to use DocIO
platform: file-formats
control: DocIO
documentation: UG
---

# NuGet Packages Required

## Installing Syncfusion DocIO through NuGet Packages 

NuGet is the one of the easiest way to download and install DocIO library to read, write and edit the Word documents. The following NuGet packages need to be installed in your application.
<table>
<thead>
<tr>
<th width="20%">
Platform(s)
</th>
<th width="40%">
Package name
</th>
<th width="40%">
Package manager console command
</th>
</tr>
</thead>
<tr>
<td>
.NET Frameworks (Windows Forms, WPF, ASP.NET, ASP.NET MVC and ASP.NET Core - Targeting .NET Framework)
</td>
<td>
Syncfusion.DocIO.Base.nupkg
</td>
<td>
Install-Package Syncfusion.DocIO.Base
</td>
</tr>
<tr>
<td>
ASP.NET Core (Targeting .netcoreapp)
</td>
<td>
Syncfusion.DocIO.NETStandard.nupkg
</td>
<td>
Install-Package Syncfusion.DocIO.NETStandard
</td>
</tr>
<tr>
<td>
Xamarin
</td>
<td>
Syncfusion.Xamarin.DocIO.nupkg
</td>
<td>
Install-Package Syncfusion.Xamarin.DocIO
</td>
</tr>
<tr>
<td>
UWP
</td>
<td>
Syncfusion.DocIO.UWP.nupkg
</td>
<td>
Install-Package Syncfusion.DocIO.UWP
</td>
</tr>
</table>
N> 1. Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/license-key) to know about registering Syncfusion license key in your application to use our components.
N> 2. Syncfusion components are available in [nuget.org](https://www.nuget.org/)

## Converting Word document to PDF

For converting Word document into PDF, the following NuGet packages need to be installed in your application.

<table>
<thead>
<tr>
<th width="20%">
Platform(s)
</th>
<th width="40%">
Package name
</th>
<th width="40%">
Package manager console command
</th>
</tr>
</thead>
<tr>
<td>
.NET Frameworks (Windows Forms, WPF, ASP.NET, ASP.NET MVC and ASP.NET Core – Targeting .NET Framework)
</td>
<td>
Syncfusion.DocToPdfConverter.Base.nupkg
</td>
<td>
Install-Package Syncfusion.DocToPdfConverter.Base
</td>
</tr>
<tr>
<td>
ASP.NET Core (Targeting .netcoreapp)
</td>
<td>
Syncfusion.DocIORenderer.NetStandard.nupkg
</td>
<td>
Install-Package Syncfusion.DocIORenderer.NetStandard
</td>
</tr>
<tr>
<td>
Xamarin
</td>
<td>
Syncfusion.Xamarin.DocIORenderer.nupkg
</td>
<td>
Install-Package Syncfusion.Xamarin.DocIORenderer
</td>
</tr>
</table>

N> 1. Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/license-key) to know about registering Syncfusion license key in your application to use our components.
N> 2. Syncfusion components are available in [nuget.org](https://www.nuget.org/)
N> 3. Install SkiaSharp package version 1.59.3 in addition to DocIORenderer package.
N> 4. Please refer the procedure to deploy your .NET Core application in Linux OS from [here](https://www.syncfusion.com/kb/8470/how-to-deploy-net-core-application-with-word-to-pdf-conversion-capabilities-in-linux-os).


## Converting Charts

The following NuGet package need to be installed additionally to preserve chart as image in Word to PDF, and Image conversions.

<table>
<thead>
<tr>
<th width="20%">
Platform(s)
</th>
<th width="40%">
Package name
</th>
<th width="40%">
Package manager console command
</th>
</tr>
</thead>
<tr>
<td>
.NET Frameworks (Windows Forms, WPF, ASP.NET, ASP.NET MVC and ASP.NET Core – Targeting .NET Framework)
</td>
<td>
Syncfusion.OfficeChartToImageConverter.WPF.nupkg
</td>
<td>
Install-Package Syncfusion.OfficeChartToImageConverter.Wpf
</td>
</tr>
</table>

N> 1. Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/license-key) to know about registering Syncfusion license key in your application to use our components.
N> 2. Syncfusion components are available in [nuget.org](https://www.nuget.org/)
N> 3. The "Syncfusion.OfficeChartToImageConverter.WPF.nupkg" NuGet package is only supported from 4.0 .NET Framework onwards and it is not supported in ASP.NET Core (Targeting .netcoreapp) and Xamarin platforms.


## NuGet Package Installation and Uninstallation

To use Syncfusion NuGet packages in your project, please refer the NuGet Package [Installation](https://help.syncfusion.com/extension/syncfusion-nuget-packages/nuget-install-and-configuration#) and [Uninstallation](https://help.syncfusion.com/extension/syncfusion-nuget-packages/nuget-uninstallation-process#) sections.

DocIO NuGet packages can be installed and uninstalled using Package Manager Console. In Visual Studio, select Tools > NuGet Package Manager > Package Manager Console and execute the following commands.

### .NET Frameworks (Windows Forms, WPF, ASP.NET, ASP.NET MVC and ASP.NET Core – Targeting .NET Framework)

**NuGet Package:** Syncfusion.DocIO.Base

The package contains DocIO library that allows you to create, read and edit Word documents.

~~~
// Install package
Install-Package Syncfusion.DocIO.Base
~~~
~~~
// Uninstall package
Uninstall-Package Syncfusion.DocIO.Base -RemoveDependencies 
~~~

**NuGet Package:** Syncfusion.DocToPdfConverter.Base

The package contains the DocToPdfConverter .NET library that allows you to convert the Word documents to PDF.

~~~
// Install package
Install-Package Syncfusion.DocToPdfConverter.Base
~~~
~~~
// Uninstall package
Uninstall-Package Syncfusion.DocToPdfConverter.Base -RemoveDependencies 
~~~

**NuGet Package:** Syncfusion.OfficeChartToImageConverter.WPF

The package contains OfficeChartToImageConverter .NET library for converting the chart present in word document to image.

~~~
// Install package
Install-Package Syncfusion.OfficeChartToImageConverter.Wpf
~~~
~~~
// Uninstall package
Uninstall-Package Syncfusion.OfficeChartToImageConverter.WPF -RemoveDependencies 
~~~


### ASP.NET Core (Targeting .netcoreapp)

**NuGet Package:** Syncfusion.DocIO.NETStandard

The package contains DocIO portable library that allows you to create, read and edit Word documents.

~~~
// Install package
Install-Package Syncfusion.DocIO.NETStandard
~~~
~~~
// Uninstall package
Uninstall-Package Syncfusion.DocIO.NETStandard -RemoveDependencies 
~~~

**NuGet Package:** Syncfusion.DocIORenderer.NetStandard

The package contains the DocIORenderer .NET portable library that allows you to convert the Word documents to PDF.

~~~
// Install package
Install-Package Syncfusion.DocIORenderer.NetStandard

// Install dependent package
Install-Package SkiaSharp -Version 1.59.3
~~~
~~~
// Uninstall package
Uninstall-Package Syncfusion.DocIORenderer.NetStandard -RemoveDependencies 
~~~

### Xamarin

**NuGet Package:** Syncfusion.Xamarin.DocIO

The package contains DocIO portable library that allows you to create, read and edit Word documents.

~~~
// Install package
Install-Package Syncfusion.Xamarin.DocIO
~~~
~~~
// Uninstall package
Uninstall-Package Syncfusion.Xamarin.DocIO -RemoveDependencies 
~~~

**NuGet Package:** Syncfusion.Xamarin.DocIORenderer

The package contains the DocIORenderer .NET portable library that allows you to convert the Word documents to PDF.

~~~
// Install package
Install-Package Syncfusion.Xamarin.DocIORenderer

// Install dependent package
Install-Package SkiaSharp -Version 1.59.3
~~~
~~~
// Uninstall package
Uninstall-Package Syncfusion.Xamarin.DocIORenderer -RemoveDependencies 
~~~

### UWP

**NuGet Package:**  Syncfusion.DocIO.UWP

The package contains DocIO library that allows you to create, read and edit Word documents.

~~~
// Install package
Install-Package Syncfusion.DocIO.UWP
~~~

~~~
// Uninstall package
Uninstall-Package Syncfusion.DocIO.UWP -RemoveDependencies 
~~~

## NuGet Package details

Please find the NuGet package details from the following table. The table contains the assemblies list present in the NuGet package and dependent NuGet package details.

<table>
<thead>
<tr>
<th>
Package name
</th>
<th>
Description
</th>
<th>
Assemblies
</th>
<th>
Dependent NuGet packages
</th>
</tr>
</thead>
<tr>
<td>
Syncfusion.DocIO.Base.nupkg
</td>
<td>
Essential DocIO is a .NET Word library that allows you to create, read and edit Word documents in any .NET application without Microsoft Office dependency.
</td>
<td>
Syncfusion.DocIO.Base.dll
</td>
<td>
Syncfusion.Compression.Base.nupkg<br/>Syncfusion.OfficeChart.Base.nupkg<br/><br/></td>
</tr>
<tr>
<td>
Syncfusion.DocToPdfConverter.Base.nupkg
</td>
<td>
The DocToPdfConverter is a .NET library that allows you to convert the Word documents to PDF in any .NET Framework application without Microsoft Office dependency.
</td>
<td>
Syncfusion.DocToPDFConverter.Base.dll
</td>
<td>
Syncfusion.DocIO.Base.nupkg<br/>Syncfusion.Pdf.Base.nupkg<br/>Syncfusion.Compression.Base.nupkg<br/><br/></td>
</tr>
<tr>
<td>
Syncfusion.OfficeChartToImageConverter.WPF.nupkg
</td>
<td>
The OfficeChartToImageConverter is a .NET class library for converting Word and Presentation chart to image without using Microsoft Office.
</td>
<td>
Syncfusion.OfficeChartToImageConverter.Wpf.dll
</td>
<td>
Syncfusion.SfChart.WPF.nupkg<br/>Syncfusion.OfficeChart.Base.nupkg<br/>Syncfusion.Compression.Base.nupkg<br/><br/></td>
</tr>
<tr>
<td>
Syncfusion.DocIO.NETStandard.nupkg
</td>
<td>
Essential DocIO is a .NET Word library that allows you to create, read and edit Word documents in .NET Core application without Microsoft Office dependency.
</td>
<td>
Syncfusion.DocIO.Portable.dll
</td>
<td>
NETStandard.Library.nupkg<br/>Syncfusion.Compression.NETStandard.nupkg<br/>Syncfusion.OfficeChart.NETStandard.nupkg<br/><br/></td>
</tr>
<tr>
<td>
Syncfusion.DocIORenderer.NetStandard.nupkg
</td>
<td>
The DocIORenderer is a .NET library that allows you to convert the Word documents to PDF in .NET Core application without Microsoft Office dependency.
</td>
<td>
Syncfusion.DocIORenderer.Portable.dll
</td>
<td>
NETStandard.Library.nupkg<br/>SkiaSharp.nupkg<br/>Syncfusion.Compression.NETStandard.nupkg<br/>Syncfusion.OfficeChart.NETStandard.nupkg<br/>Syncfusion.DocIO.NETStandard.nupkg<br/>Syncfusion.Pdf.NETStandard.nupkg<br/><br/></td>
</tr>
<tr>
<td>
Syncfusion.Xamarin.DocIO.nupkg
</td>
<td>
Essential DocIO is a .NET Word library that allows you to create, read and edit Word documents in Xamarin application without Microsoft Office dependency.
</td>
<td>
Syncfusion.DocIO.Portable.dll
</td>
<td>
Syncfusion.Xamarin.Compression.nupkg<br/>Syncfusion.Xamarin.OfficeChart.nupkg<br/><br/></td>
</tr>
<tr>
<td>
Syncfusion.Xamarin.DocIORenderer.nupkg
</td>
<td>
The DocIORenderer is a .NET library that allows you to convert the Word documents to PDF in Xamarin application without Microsoft Office dependency.
</td>
<td>
Syncfusion.Compression.Portable.dll<br/>Syncfusion.DocIO.Portable.dll<br/>Syncfusion.DocIORenderer.Portable.dll<br/>Syncfusion.OfficeChart.Portable.dll<br/>Syncfusion.Pdf.Portable.dll<br/><br/></td>
<td>
SkiaSharp.nupkg<br/><br/></td>
</tr>
<tr>
<td>
Syncfusion.DocIO.UWP.nupkg
</td>
<td>
Essential DocIO is a .NET Word library that allows you to create, read and edit Word documents in Universal Windows Platform apps without Microsoft Office dependency.
</td>
<td>
Syncfusion.DocIO.UWP.dll
</td>
<td>
Syncfusion.OfficeChart.UWP.nupkg<br/><br/></td>
</tr>
</table>

