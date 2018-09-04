---
title: NuGet Packages for XlsIO
description: NuGet Packages for XlsIO library
platform: file-formats
control: XlsIO
documentation: UG
---
# NuGet Packages Required

To work with Excel documents, the following NuGet packages need to be installed in your application.

<table>
<tr>
<thead>
<th><b>Platform(s)</b></th>
<th><b>NuGet Package</b></th>
</thead>
</tr>
<tr>
<td>
.NET Framework (Windows Forms, WPF, ASP.NET Web Forms, ASP.NET MVC, ASP.NET Core – Targeting .NET Framework)
</td>
<td>
{{'[Syncfusion.XlsIO.Base.nupkg](https://www.nuget.org/packages/Syncfusion.XlsIO.Base/)'| markdownify }}
</td>
</tr>
<tr>
<td>
UWP
</td>
<td>
{{'[Syncfusion.XlsIO.UWP.nupkg](https://www.nuget.org/packages/Syncfusion.XlsIO.UWP/)'| markdownify }}
</td>
</tr>
<tr>
<td>
ASP.NET Core (Targeting .net core application)
</td>
<td>
{{'[Syncfusion.XlsIO.NETStandard.nupkg](https://www.nuget.org/packages/Syncfusion.XlsIO.NETStandard/)'| markdownify }}
</td>
</tr>
<tr>
<td>
Xamarin
</td>
<td>
{{'[Syncfusion.Xamarin.XlsIO.nupkg](https://www.nuget.org/packages/Syncfusion.Xamarin.XlsIO/)'| markdownify }}
</td>
</tr>
</table>

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/license-key) to know about registering Syncfusion license key in your applications to use our components.


## Converting Excel document into PDF

For converting Excel document into PDF, the following NuGet packages need to be installed in your application.

<table>
<tr>
<thead>
<th><b>Platform(s)</b></th>
<th><b>NuGet Package</b></th>
</thead>
</tr>
<tr>
<td>
Windows Forms, WPF, ASP.NET Web and MVC
</td>
<td>
{{'[Syncfusion.ExcelToPDFConverter.Base.nupkg](https://www.nuget.org/packages/Syncfusion.ExcelToPdfConverter.Base/)'| markdownify }}
</td>
</tr>
</table>

N> Excel to PDF conversion is not supported in Xamarin, UWP and .NET Core applications.

## Converting Excel Worksheet to Image

For converting an Excel worksheet to image, the following NuGet packages need to be installed in your application.

<table>
<tr>
<thead>
<th><b>Platform(s)</b></th>
<th><b>NuGet Package</b></th>
</thead>
</tr>
<tbody>
<tr>
<td>
Windows Forms, WPF, ASP.NET and ASP.NET MVC
</td>
<td>
Syncfusion.XlsIO.Base.nupkg
</td>
</tr>
<tr>
<td>
UWP and .NET Core
</td>
<td>
Syncfusion.XlsIORenderer.NETStandard.nupkg
</td>
</tr>
<tr>
<td>
Xamarin
</td>
<td>
Syncfusion.Xamarin.XlsIORenderer.nupkg
</td>
</tr>
</tbody>
</table>

N> Worksheet to image conversion is supported from .NET Framework 2.0 and .NET Standard 1.4 onwards.

## Converting Charts in XlsIO

The below NuGet package need to be installed additionally to convert the charts present in Excel documents.

<table>
<tr>
<thead>
<th><b>Platform(s)</b></th>
<th><b>NuGet Package</b></th>
</thead>
</tr>
<tr>
<td>
Windows Forms, WPF, ASP.NET Web and MVC
</td>
<td>
{{'[Syncfusion.ExcelChartToImageConverter.Wpf.nupkg](https://www.nuget.org/packages/Syncfusion.ExcelChartToImageConverter.WPF/)'| markdownify }}
</td>
</tr>
</table>

N> 1. The "Syncfusion.ExcelChartToImageConverter.Wpf.nupkg" NuGet package is only supported from 4.0 .NET Framework onwards. 
N> 2. Chart to image conversion is not supported in .NET Standard.

## NuGet Package Installation and Uninstallation

To use NuGet package in your project, please refer the NuGet Package [Installation](https://help.syncfusion.com/extension/syncfusion-nuget-packages/nuget-install-and-configuration) and [Uninstallation](https://help.syncfusion.com/extension/syncfusion-nuget-packages/nuget-uninstallation-process) sections.

XlsIO NuGet packages can be installed and uninstalled using Package Manager Console. In Visual Studio, select **Tools > NuGet Package Manager > Package Manager Console** and execute the below commands in respective platforms.

N> Syncfusion components are available in nuget.org

<table>
<tr>
<thead>
<th><b>Platform(s)</b></th>
<th><b>Install</b></th>
<th><b>UnInstall</b></th>
</thead>
</tr>
<tr>
<td>
Windows Forms, WPF, ASP.NET Web and MVC
</td>
<td>
* Install-package Syncfusion.XlsIO.Base -source {{'<https://nuget.syncfusion.com/nuget_windows-forms/nuget/getsyncfusionpackages/windows-forms/>'| markdownify }}<br/><br/>
* Install-package Syncfusion.ExcelToPdfConverter.Base -source {{'<https://nuget.syncfusion.com/nuget_windows-forms/nuget/getsyncfusionpackages/windows-forms/>'| markdownify }}<br/><br/>
* Install-package Syncfusion.ExcelChartToImageConverter.WPF -source {{'<https://nuget.syncfusion.com/nuget_windows-forms/nuget/getsyncfusionpackages/windows-forms/>'| markdownify }}
</td>
<td>
* Uninstall-package Syncfusion.XlsIO.Base -RemoveDependencies <br/><br/>
* Uninstall-package Syncfusion.ExcelToPdfConverter.Base -RemoveDependencies <br/><br/>
* Uninstall-package Syncfusion.ExcelChartToImageConverter.WPF -RemoveDependencies                             
</td>
</tr>
<tr>
<td>
UWP
</td>
<td>
Install-package Syncfusion.XlsIO.UWP –source {{'<https://nuget.syncfusion.com/nuget_universalwindows/nuget/getsyncfusionpackages/universalwindows>'| markdownify }}
</td>
<td>
Uninstall-package Syncfusion.XlsIO.UWP –RemoveDependencies
</td>
</tr>
<tr>
<td>
ASP.NET Core
</td>
<td>
Install-package Syncfusion.XlsIO.NETStandard -source {{'<https://nuget.syncfusion.com/nuget_aspnetcore/nuget/getsyncfusionpackages/aspnetcore>'| markdownify }}
</td>
<td>
Uninstall-package Syncfusion.XlsIO.NETStandard –RemoveDependencies
</td>
</tr>
<tr>
<td>
Xamarin
</td>
<td>
Install-package Syncfusion.Xamarin.XlsIO –source {{'<https://nuget.syncfusion.com/nuget_xamarin/nuget/getsyncfusionpackages/xamarin>'| markdownify }}
</td>
<td>
Uninstall-package Syncfusion.Xamarin.XlsIO –RemoveDependencies
</td>
</tr>
</table>