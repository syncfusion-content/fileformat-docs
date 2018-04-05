---
title: NuGet Packages Required
description: NuGet Packages required to use DocIO
platform: file-formats
control: DocIO
documentation: UG
---

# Installing Syncfusion DocIO through NuGet Packages 

NuGet is the one of the easiest way to download and install DocIO library to work with Word documents. The following NuGet packages need to be installed in your application.
<table>
<thead>
<tr>
<th>
Platform(s)
</th>
<th>
Package name
</th>
<th>
Package manager console command
</th>
</tr>
</thead>
<tr>
<td>
.NET Frameworks (Windows Forms, WPF, ASP.NET and ASP.NET MVC)
</td>
<td>
Syncfusion.DocIO.Base.nupkg
</td>
<td>
Install-Package Syncfusion.DocIO.Base -Source http://nuget.syncfusion.com/nuget_windows-forms/nuget/getsyncfusionpackages/windows-forms
</td>
</tr>
<tr>
<td>
ASP.NET and ASP.NET MVC
</td>
<td>
Syncfusion.Web.FileFormatsBase.nupkg
</td>
<td>
Install-Package Syncfusion.Web.FileFormatsBase -Source http://nuget.syncfusion.com/nuget_aspnet/nuget/getsyncfusionpackages/aspnet
</td>
</tr>
<tr>
<td>
ASP.NET Core
</td>
<td>
Syncfusion.DocIO.NETStandard.nupkg
</td>
<td>
Install-Package Syncfusion.DocIO.NETStandard -Source http://nuget.syncfusion.com/nuget_aspnetcore/nuget/getsyncfusionpackages/aspnetcore
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
Install-Package Syncfusion.Xamarin.DocIO -Source https://api.nuget.org/v3/index.json
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
Install-Package Syncfusion.DocIO.UWP -Source http://nuget.syncfusion.com/nuget_universalwindows/nuget/getsyncfusionpackages/universalwindows
</td>
</tr>
</table>

## Converting Word document to PDF

For converting Word document into PDF, the following NuGet packages need to be installed in your application.

<table>
<thead>
<tr>
<th>
Platform(s)
</th>
<th>
Package name
</th>
<th>
Package manager console command
</th>
</tr>
</thead>
<tr>
<td>
.NET Frameworks (Windows Forms, WPF, ASP.NET and ASP.NET MVC)
</td>
<td>
Syncfusion.DocToPdfConverter.Base.nupkg
</td>
<td>
Install-Package Syncfusion.DocToPdfConverter.Base -Source http://nuget.syncfusion.com/nuget_windows-forms/nuget/getsyncfusionpackages/windows-forms
</td>
</tr>
<tr>
<td>
ASP.NET
</td>
<td>
Syncfusion.AspNet.FileFormats.nupkg
</td>
<td>
Install-Package Syncfusion.AspNet.FileFormats -Source http://nuget.syncfusion.com/nuget_aspnet/nuget/getsyncfusionpackages/aspnet
</td>
</tr>
<tr>
<td>
ASP.NET MVC
</td>
<td>
Syncfusion.AspNet.Mvc.FileFormats.nupkg
</td>
<td>
Install-Package Syncfusion.AspNet.Mvc.FileFormats -Source http://nuget.syncfusion.com/nuget_aspnetmvc/nuget/getsyncfusionpackages/aspnetmvc
</td>
</tr>
<tr>
<td>
ASP.NET Core 
</td>
<td>
Syncfusion.DocIORenderer.NetStandard.nupkg
</td>
<td>
Install-Package Syncfusion.DocIORenderer.NetStandard -Source http://nuget.syncfusion.com/nuget_aspnetcore/nuget/getsyncfusionpackages/aspnetcore
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
Install-Package Syncfusion.Xamarin.DocIORenderer -Source https://api.nuget.org/v3/index.json
</td>
</tr>
</table>

N> Word to PDF conversion is not supported in Universal Windows Platform.


## Converting Charts in DocIO

The below NuGet package need to be installed additionally to convert the charts present in Word documents.

<table>
<thead>
<tr>
<th>
Platform(s)
</th>
<th>
Package name
</th>
<th>
Package manager console command
</th>
</tr>
</thead>
<tr>
<td>
.NET Frameworks (Windows Forms, WPF, ASP.NET and ASP.NET MVC)
</td>
<td>
Syncfusion.OfficeChartToImageConverter.WPF.nupkg
</td>
<td>
Install-Package Syncfusion.OfficeChartToImageConverter.Base -Source http://nuget.syncfusion.com/nuget_windows-forms/nuget/getsyncfusionpackages/windows-forms
</td>
</tr>
</table>

N> 1. The "Syncfusion.OfficeChartToImageConverter.WPF.nupkg" NuGet package is only supported from 4.0 .NET Framework onwards and also it not supported in the Universal Windows Platform.
N> 2. The "Syncfusion.AspNet.FileFormats.nupkg" and "Syncfusion.AspNet.Mvc.FileFormats.nupkg" internally includes the assemblies, necessary for the preservation of chart as image in Word to PDF, and Image conversions. So it is not necessary to install the "Syncfusion.OfficeChartToImageConverter.WPF.nupkg" NuGet package in addition to these packages.


## NuGet Package Installation and Uninstallation

To use Syncfusion NuGet packages in your project, please refer the NuGet Package [Installation](https://help.syncfusion.com/extension/syncfusion-nuget-packages/nuget-install-and-configuration#) and [Uninstallation](https://help.syncfusion.com/extension/syncfusion-nuget-packages/nuget-uninstallation-process#) sections.

DocIO NuGet packages can be installed and uninstalled using Package Manager Console. In Visual Studio, select Tools > NuGet Package Manager > Package Manager Console and execute the below commands in respective platforms.

### Platforms: .NET Frameworks (Windows Forms, WPF, ASP.NET and ASP.NET MVC)

**NuGet Package Name:** Syncfusion.DocIO.Base

Commands:

~~~
// Install package
Install-Package Syncfusion.DocIO.Base -Source http://nuget.syncfusion.com/nuget_windows-forms/nuget/getsyncfusionpackages/windows-forms 
~~~
~~~
// Un Install package
Uninstall-Package Syncfusion.DocIO.Base -RemoveDependencies 
~~~

**NuGet Package Name:** Syncfusion.DocToPdfConverter.Base

Commands:

~~~
// Install package
Install-Package Syncfusion.DocToPdfConverter.Base -Source http://nuget.syncfusion.com/nuget_windows-forms/nuget/getsyncfusionpackages/windows-forms 
~~~
~~~
// Un Install package
Uninstall-Package Syncfusion.DocToPdfConverter.Base -RemoveDependencies 
~~~

**NuGet Package Name:** Syncfusion.OfficeChartToImageConverter.WPF

Commands:

~~~
// Install package
Install-Package Syncfusion.OfficeChartToImageConverter.WPF -Source http://nuget.syncfusion.com/nuget_windows-forms/nuget/getsyncfusionpackages/windows-forms 
~~~
~~~
// Un Install package
Uninstall-Package Syncfusion.OfficeChartToImageConverter.WPF -RemoveDependencies 
~~~

### Platform: ASP.NET

**NuGet Package Name:** Syncfusion.Web.FileFormatsBase

Commands:

~~~
// Install package
Install-Package Syncfusion.Web.FileFormatsBase -Source http://nuget.syncfusion.com/nuget_aspnet/nuget/getsyncfusionpackages/aspnet 
~~~
~~~
// Un Install package
Uninstall-Package Syncfusion.Web.FileFormatsBase -RemoveDependencies 
~~~

**NuGet Package Name:** Syncfusion.AspNet.FileFormats

Commands:

~~~
// Install package
Install-Package Syncfusion.AspNet.FileFormats -Source http://nuget.syncfusion.com/nuget_aspnet/nuget/getsyncfusionpackages/aspnet
~~~
~~~
// Un Install package
Uninstall-Package Syncfusion.AspNet.FileFormats -RemoveDependencies 
~~~

### Platform: ASP.NET MVC

**NuGet Package Name:** Syncfusion.Web.FileFormatsBase

Commands:

~~~
// Install package
Install-Package Syncfusion.Web.FileFormatsBase -Source http://nuget.syncfusion.com/nuget_aspnetmvc/nuget/getsyncfusionpackages/aspnetmvc
~~~
~~~
// Un Install package
Uninstall-Package Syncfusion.Web.FileFormatsBase -RemoveDependencies 
~~~

**NuGet Package Name:** Syncfusion.AspNet.Mvc.FileFormats

Commands:

~~~
// Install package
Install-Package Syncfusion.AspNet.Mvc5.FileFormats -Source http://nuget.syncfusion.com/nuget_aspnetmvc/nuget/getsyncfusionpackages/aspnetmvc
~~~
~~~
// Un Install package
Uninstall-Package Syncfusion.AspNet.Mvc5.FileFormats -RemoveDependencies 
~~~

N> The number at the end of MVC denotes ASP.MVC version.

### Platform: ASP.NET Core

**NuGet Package Name:** Syncfusion.DocIO.NETStandard

Commands:

~~~
// Install package
Install-Package Syncfusion.DocIO.NETStandard -Source http://nuget.syncfusion.com/nuget_aspnetcore/nuget/getsyncfusionpackages/aspnetcore 
~~~
~~~
// Un Install package
Uninstall-Package Syncfusion.DocIO.NETStandard -RemoveDependencies 
~~~

**NuGet Package Name:** Syncfusion.DocIORenderer.NetStandard

Commands:

~~~
// Install package
Install-Package Syncfusion.DocIORenderer.NetStandard -Source http://nuget.syncfusion.com/nuget_aspnetcore/nuget/getsyncfusionpackages/aspnetcore 
~~~
~~~
// Un Install package
Uninstall-Package Syncfusion.DocIORenderer.NetStandard -RemoveDependencies 
~~~

### Platform: Xamarin

**NuGet Package Name:** Syncfusion.Xamarin.DocIO

Commands:

~~~
// Install package
Install-Package Syncfusion.Xamarin.DocIO -Source https://api.nuget.org/v3/index.json
~~~
~~~
// Un Install package
Uninstall-Package Syncfusion.Xamarin.DocIO -RemoveDependencies 
~~~

**NuGet Package Name:** Syncfusion.Xamarin.DocIORenderer

Commands:

~~~
// Install package
Install-Package Syncfusion.Xamarin.DocIORenderer -Source https://api.nuget.org/v3/index.json
~~~
~~~
// Un Install package
Uninstall-Package Syncfusion.Xamarin.DocIORenderer -RemoveDependencies 
~~~


### Platform: UWP

**NuGet Package Name:**  Syncfusion.DocIO.UWP

Commands:

~~~
// Install package
Install-Package Syncfusion.DocIO.UWP -Source http://nuget.syncfusion.com/nuget_universalwindows/nuget/getsyncfusionpackages/universalwindows 
~~~

~~~
// Un Install package
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
Assemblies list
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
Syncfusion.Web.FileFormatsBase.nupkg
</td>
<td>
Syncfusion File formats provides the ability to create, read, and edit PDF, Excel, Word, and PowerPoint files.
</td>
<td>
Syncfusion.Compression.Base.dll<br/>Syncfusion.DocIO.Base.dll<br/>Syncfusion.OfficeChart.Base.dll<br/>Syncfusion.Pdf.Base.dll<br/>Syncfusion.Presentation.Base.dll<br/>Syncfusion.XlsIO.Base.dll<br/><br/></td>
<td>

</td>
</tr>
<tr>
<td>
Syncfusion.AspNet.FileFormats.nupkg
</td>
<td>
Syncfusion File formats provides the ability to create, read, edit, and convert PDF, Excel, Word, and PowerPoint files.
</td>
<td>
Syncfusion.DocToPDFConverter.Base.dll<br/>Syncfusion.ExcelChartToImageConverter.WPF.dll<br/>Syncfusion.ExcelToPDFConverter.Base.dll<br/>Syncfusion.HtmlConverter.Base.dll<br/>Syncfusion.OfficeChartToImageConverter.WPF.dll<br/>Syncfusion.PresentationToPDFConverter.Base.dll<br/>Syncfusion.SfChart.WPF.dll<br/><br/></td>
<td>
Syncfusion.Web.FileFormatsBase.nupkg
</td>
</tr>
<tr>
<td>
Syncfusion.AspNet.Mvc.FileFormats.nupkg
</td>
<td>
Syncfusion File formats provides the ability to create, read, edit, and convert PDF, Excel, Word, and PowerPoint files.
</td>
<td>
Syncfusion.DocToPDFConverter.Base.dll<br/>Syncfusion.ExcelChartToImageConverter.WPF.dll<br/>Syncfusion.ExcelToPDFConverter.Base.dll<br/>Syncfusion.HtmlConverter.Base.dll<br/>Syncfusion.OfficeChartToImageConverter.WPF.dll<br/>Syncfusion.PresentationToPDFConverter.Base.dll<br/>Syncfusion.SfChart.WPF.dll<br/><br/></td>
<td>
Syncfusion.Web.FileFormatsBase.nupkg
</td>
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
Microsoft.NETCore.Portable.Compatibility.nupkg<br/>NETStandard.Library.nupkg<br/>Syncfusion.Compression.NETStandard.nupkg<br/>Syncfusion.OfficeChart.NETStandard.nupkg<br/><br/></td>
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
Microsoft.NETCore.Portable.Compatibility.nupkg<br/>NETStandard.Library.nupkg<br/>SkiaSharp.nupkg<br/>Syncfusion.Compression.NETStandard.nupkg<br/>Syncfusion.OfficeChart.NETStandard.nupkg<br/>Syncfusion.DocIO.NETStandard.nupkg<br/>Syncfusion.Pdf.NETStandard.nupkg<br/><br/></td>
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

