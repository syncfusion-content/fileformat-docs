---
title: NuGet Packages for Excel to PDF | Syncfusion
description: This section illustrates the NuGet packages required to perform Excel to PDF conversion in various platforms and frameworks.
platform: file-formats
control: XlsIO
documentation: UG
---
# NuGet Packages Required for Excel to PDF conversion

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
Windows Forms,<br/>
Console Application (Targeting .NET Framework)
</td>
<td>
{{'[Syncfusion.ExcelToPDFConverter.WinForms.nupkg](https://www.nuget.org/packages/Syncfusion.ExcelToPdfConverter.WinForms/)'| markdownify }}
</td>
</tr>
<tr>
<td>
WPF
</td>
<td>
{{'[Syncfusion.ExcelToPDFConverter.Wpf.nupkg](https://www.nuget.org/packages/Syncfusion.ExcelToPdfConverter.Wpf/)'| markdownify }}
</td>
</tr>
<tr>
<td>
.NET Framework 3.5 or 4.0 Client Profile
</td>
<td>
{{'[Syncfusion.ExcelToPdfConverter.ClientProfile.nupkg](https://www.nuget.org/packages/Syncfusion.ExcelToPdfConverter.ClientProfile/)'| markdownify }}
</td>
</tr>
<tr>
<td>
ASP.NET Web Forms,<br/>
ASP.NET Core (Targeting .NET Framework)
</td>
<td>
{{'[Syncfusion.ExcelToPDFConverter.AspNet.nupkg](https://www.nuget.org/packages/Syncfusion.ExcelToPdfConverter.AspNet/)'| markdownify }}
</td>
</tr>
<tr>
<td>
ASP.NET MVC4
</td>
<td>
{{'[Syncfusion.ExcelToPDFConverter.AspNet.Mvc4.nupkg](https://www.nuget.org/packages/Syncfusion.ExcelToPdfConverter.AspNet.Mvc4/)'| markdownify }}
</td>
</tr>
<tr>
<td>
ASP.NET MVC5
</td>
<td>
{{'[Syncfusion.ExcelToPDFConverter.AspNet.Mvc5.nupkg](https://www.nuget.org/packages/Syncfusion.ExcelToPdfConverter.AspNet.Mvc5/)'| markdownify }}
</td>
</tr>
<tr>
<td>
UWP,<br/> 
ASP.NET Core (Targeting .NET Core),<br/>
Console Application (Targeting .NET Core)
</td>
<td>
{{'[Syncfusion.XlsIORenderer.Net.Core.nupkg](https://www.nuget.org/packages/Syncfusion.XlsIORenderer.Net.Core/)'| markdownify }}
</td>
</tr>
<tr>
<td>
Xamarin
</td>
<td>
{{'[Syncfusion.Xamarin.XlsIORenderer.nupkg](https://www.nuget.org/packages/Syncfusion.Xamarin.XlsIORenderer/)'| markdownify }}
</td>
</tr>
<tr>
<td>
Blazor
</td>
<td>
{{'[Syncfusion.XlsIORenderer.Net.Core.nupkg](https://www.nuget.org/packages/Syncfusion.XlsIORenderer.Net.Core/)'| markdownify }}
</td>
</tr>
<tr>
<td>
WinUI and .NET MAUI
</td>
<td>
{{'[Syncfusion.XlsIORenderer.NET.nupkg](https://www.nuget.org/packages/Syncfusion.XlsIORenderer.NET/)'| markdownify }}
</td>
</tr>
</table>

N> Excel to PDF conversion is supported from .NET Framework 2.0 and .NET Standard 1.4 onwards.

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your applications to use our components.

N> Syncfusion components are available in nuget.org

N> From the Essential Studio 2018 Volume 3 release(v16.3.0.21), Syncfusion has changed some of the NuGet package names to search and find the required Syncfusion NuGet packages in nuget.org easily based on the control and its platforms.

N> Starting with v17.3.0.x, Syncfusion provides support to .NET Core 3.0. You can use the above WPF or Windows Forms platform NuGet packages for .NET Core 3.0 targeting applications and use the same “C# tab” code examples for it.

## NuGet Package Installation and Uninstallation

To use NuGet package in your project, please refer the NuGet Package [Installation](https://help.syncfusion.com/extension/syncfusion-nuget-packages/nuget-packages#installing-nuget-packages) and [Uninstallation](https://help.syncfusion.com/extension/syncfusion-nuget-packages/nuget-uninstallation-process) sections.

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
Windows Forms
</td>
<td>
* Install-package Syncfusion.ExcelToPdfConverter.WinForms
</td>
<td>
* Uninstall-package Syncfusion.ExcelToPdfConverter.WinForms -RemoveDependencies
</td>
</tr>
<tr>
<td>
WPF
</td>
<td>
* Install-package Syncfusion.ExcelToPdfConverter.Wpf
</td>
<td>
* Uninstall-package Syncfusion.ExcelToPdfConverter.Wpf -RemoveDependencies
</td>
</tr>
<tr>
<td>
ASP.NET Web Forms
</td>
<td>
* Install-package Syncfusion.ExcelToPdfConverter.AspNet
</td>
<td>
* Uninstall-package Syncfusion.ExcelToPdfConverter.AspNet -RemoveDependencies
</td>
</tr>
<tr>
<td>
ASP.NET MVC4
</td>
<td>
* Install-package Syncfusion.ExcelToPdfConverter.AspNet.MVC4
</td>
<td>
* Uninstall-package Syncfusion.ExcelToPdfConverter.AspNet.MVC4 -RemoveDependencies
</td>
</tr>
<tr>
<td>
ASP.NET MVC5
</td>
<td>
* Install-package Syncfusion.ExcelToPdfConverter.AspNet.MVC5
</td>
<td>
* Uninstall-package Syncfusion.ExcelToPdfConverter.AspNet.MVC5 -RemoveDependencies
</td>
</tr>
<tr>
<td>
UWP
</td>
<td>
Install-package Syncfusion.XlsIORenderer.Net.Core
</td>
<td>
Uninstall-package Syncfusion.XlsIORenderer.Net.Core –RemoveDependencies
</td>
</tr>
<tr>
<td>
ASP.NET Core and Blazor
</td>
<td>
* Install-package Syncfusion.XlsIORenderer.Net.Core
</td>
<td>
* Uninstall-package Syncfusion.XlsIORenderer.Net.Core –RemoveDependencies
</td>
</tr>
<tr>
<td>
Xamarin
</td>
<td>
* Install-package Syncfusion.Xamarin.XlsIORenderer
</td>
<td>
* Uninstall-package Syncfusion.Xamarin.XlsIORenderer –RemoveDependencies
</td>
</tr>
<tr>
<td>
WinUI and .NET MAUI
</td>
<td>
* Install-package Syncfusion.XlsIORenderer.NET
</td>
<td>
* Uninstall-package Syncfusion.XlsIORenderer.NET –RemoveDependencies
</td>
</tr>
</table>