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
Windows Forms, WPF, ASP.NET Web and MVC
</td>
<td>
Syncfusion.XlsIO.Base.nupkg
</td>
</tr>
<tr>
<td>
UWP
</td>
<td>
Syncfusion.XlsIO.UWP.nupkg
</td>
</tr>
<tr>
<td>
ASP.NET Core
</td>
<td>
Syncfusion.XlsIO.NETStandard.nupkg
</td>
</tr>
<tr>
<td>
Xamarin
</td>
<td>
Syncfusion.Xamarin.XlsIO.nupkg
</td>
</tr>
</table>

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
Syncfusion.ExcelToPDFConverter.Base.nupkg
</td>
</tr>
</table>

N> Excel to PDF/Image conversion is not supported in Xamarin, UWP and ASP.NET Core applications.

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
Syncfusion.ExcelChartToImageConverter.Wpf.nupkg
</td>
</tr>
</table>

N> The "Syncfusion.ExcelChartToImageConverter.Wpf.nupkg" NuGet package is only supported from 4.0 .NET Framework onwards. 

## NuGet Package Installation and Uninstallation

To use NuGet package in your project, please refer the NuGet Package [Installation](https://help.syncfusion.com/extension/syncfusion-nuget-packages/nuget-install-and-configuration) and [Uninstallation](https://help.syncfusion.com/extension/syncfusion-nuget-packages/nuget-uninstallation-process) sections.

XlsIO NuGet packages can be installed and uninstalled using Package Manager Console. In Visual Studio, select **Tools > NuGet Package Manager > Package Manager Console** and execute the below commands in respective platforms.

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
* Install-package Syncfusion.XlsIO.Base45 -source {{'<http://nuget.syncfusion.com/nuget_windows-forms/nuget/getsyncfusionpackages/windows-forms/>'| markdownify }}<br/><br/>
* Install-package Syncfusion.ExcelToPdfConverter.Base45 -source {{'<http://nuget.syncfusion.com/nuget_windows-forms/nuget/getsyncfusionpackages/windows-forms/>'| markdownify }}<br/><br/>
* Install-package Syncfusion.ExcelChartToImageConverter.WPF45 -source {{'<http://nuget.syncfusion.com/nuget_windows-forms/nuget/getsyncfusionpackages/windows-forms/>'| markdownify }}
</td>
<td>
* Uninstall-package Syncfusion.XlsIO.Base45 -RemoveDependencies                             <br/><br/>
* Uninstall-package Syncfusion.ExcelToPdfConverter.Base45 -RemoveDependencies                             <br/><br/>
* Uninstall-package Syncfusion.ExcelChartToImageConverter.WPF45 -RemoveDependencies                             
</td>
</tr>
<tr>
<td>
UWP
</td>
<td>
Install-package Syncfusion.XlsIO.UWP46 –source {{'<http://nuget.syncfusion.com/nuget_universalwindows/nuget/getsyncfusionpackages/universalwindows>'| markdownify }}
</td>
<td>
Uninstall-package Syncfusion.XlsIO.UWP46 –RemoveDependencies
</td>
</tr>
<tr>
<td>
ASP.NET Core
</td>
<td>
Install-package Syncfusion.XlsIO.NETStandard12 -source {{'<http://nuget.syncfusion.com/nuget_aspnetcore/nuget/getsyncfusionpackages/aspnetcore>'| markdownify }}
</td>
<td>
Uninstall-package Syncfusion.XlsIO.NETStandard12 –RemoveDependencies
</td>
</tr>
<tr>
<td>
Xamarin
</td>
<td>
Install-package Syncfusion.Xamarin.XlsIO –source {{'<http://nuget.syncfusion.com/nuget_xamarin/nuget/getsyncfusionpackages/xamarin>'| markdownify }}
</td>
<td>
Uninstall-package Syncfusion.Xamarin.XlsIO –RemoveDependencies
</td>
</tr>
</table>

N> The number at the end of the NuGet package name represents .NET Framework version. In the above command "Syncfusion.XlsIO.Base45" represents the XlsIO libraries for .NET Framework 4.5 (Syncfusion.XlsIO.Base35 and Syncfusion.XlsIO.Base40 represents the libraries for .NET Framework 3.5 and 4.0 respectively).