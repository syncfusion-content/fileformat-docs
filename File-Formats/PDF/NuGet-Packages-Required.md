---
title: NuGet Packages for PDF
description: NuGet Packages for PDF library
platform: file-formats
control: PDF
documentation: UG
---
# NuGet Packages Required 

To work with PDF documents, the following NuGet packages need to be installed in your application.

<table>
<tr>
<thead>
<th><b>Platform(s)</b></th>
<th><b>NuGet Package</b></th>
</thead>
</tr>
<tr>
<td>
Windows Forms, WPF, ASP.NET and ASP.NET MVC
</td>
<td>
{{'[Syncfusion.Pdf.Base.nupkg](https://www.nuget.org/packages/Syncfusion.Pdf.Base/)'| markdownify }}
</td>
</tr>
<tr>
<td>
UWP
</td>
<td>
{{'[Syncfusion.Pdf.UWP.nupkg](https://www.nuget.org/packages/Syncfusion.Pdf.UWP/)'| markdownify }}
</td>
</tr>
<tr>
<td>
ASP.NET Core
</td>
<td>
{{'[Syncfusion.Pdf.NETStandard.nupkg](https://www.nuget.org/packages/Syncfusion.Pdf.NETStandard/)'| markdownify }}
</td>
</tr>
<tr>
<td>
Xamarin
</td>
<td>
{{'[Syncfusion.Xamarin.Pdf.nupkg](https://www.nuget.org/packages/Syncfusion.Xamarin.Pdf/)'| markdownify }}
</td>
</tr>
</table>

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/license-key) to know about registering Syncfusion license key in your application to use our components.


## Converting HTML to PDF

For converting HTML to PDF, the following NuGet packages need to be installed in your application.

<table>
<tr>
<thead>
<th><b>Platform(s)</b></th>
<th><b>NuGet Package</b></th>
</thead>
</tr>
<tr>
<td>
Windows Forms, WPF, ASP.NET and ASP.NET MVC
</td>
<td>
{{'[Syncfusion.HtmlToPdfConverter.nupkg](http://nuget.syncfusion.com/nuget_windows-forms/nuget/getsyncfusionpackages/windows-forms)'| markdownify }}
</td>
</tr>
<tr>
<td>
ASP.NET Core
</td>
<td>
{{'[Syncfusion.HtmlConverter.NETStandard.nupkg](http://nuget.syncfusion.com/nuget_aspnetcore/nuget/getsyncfusionpackages/aspnetcore)'| markdownify }}
</td>
</tr>
</table>

N> HTML to PDF conversion is not supported in Silverlight, Windows Phone, WinRT, Universal, Xamarin and UWP applications.	

## Converting Word to PDF

For converting Word document into PDF, the following NuGet packages need to be installed in your application.

<table>
<tr>
<thead>
<th><b>Platform(s)</b></th>
<th><b>NuGet Package</b></th>
</thead>
</tr>
<tr>
<td>
.NET Frameworks (Windows Forms, WPF, ASP.NET and ASP.NET MVC)
</td>
<td>
{{'[Syncfusion.DocToPdfConverter.Base.nupkg](https://www.nuget.org/packages/Syncfusion.DocToPdfConverter.Base/)'| markdownify }}
</td>
</tr>
<tr>
<td>
ASP.NET 
</td>
<td>
{{'[Syncfusion.AspNet.FileFormats.nupkg](https://www.nuget.org/packages/Syncfusion.AspNet.FileFormats/)'| markdownify }}
</td>
</tr>
<tr>
<td>
ASP.NET MVC
</td>
<td>
{{'[Syncfusion.AspNet.Mvc.FileFormats.nupkg](https://www.nuget.org/packages/Syncfusion.AspNet.Mvc5.FileFormats/)'| markdownify }}
</td>
</tr>
<tr>
<td>
ASP.NET Core
</td>
<td>
{{'[Syncfusion.DocIORenderer.NetStandard.nupkg](https://www.nuget.org/packages/Syncfusion.DocIORenderer.NETStandard/)'| markdownify }}
</td>
</tr>
<tr>
<td>
Xamarin
</td>
<td>
{{'[Syncfusion.Xamarin.DocIORenderer.nupkg](https://www.nuget.org/packages/Syncfusion.Xamarin.DocIORenderer/)'| markdownify }}
</td>
</tr>
</table>

N> Install SkiaSharp package version 1.59.3 in addition to DocIORenderer package.  

## Converting Excel document to PDF

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
Windows Forms, WPF, ASP.NET and ASP.NET MVC
</td>
<td>
{{'[Syncfusion.ExcelToPDFConverter.Base.nupkg](https://www.nuget.org/packages/Syncfusion.ExcelToPdfConverter.Base/)'| markdownify }}
</td>
</tr>
</table>

N> Excel to PDF/Image conversion is not supported in Xamarin, UWP and ASP.NET Core applications. 

## Converting Presentation document to PDF

For converting PowerPoint Presentation to PDF, the following NuGet packages need to be installed in your application. 

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
{{'[Syncfusion.PresentationToPdfConverter.Base.nupkg](https://www.nuget.org/packages/Syncfusion.PresentationToPdfConverter.Base/)'| markdownify }}
</td>
</tr>
</table>

N> Presentation to PDF/Image conversion is not supported in Xamarin, UWP and ASP.NET Core applications.   

## NuGet Package Installation and Uninstallation

To use NuGet package in your project, please refer the NuGet Package [Installation](https://help.syncfusion.com/extension/syncfusion-nuget-packages/nuget-install-and-configuration) and [Uninstallation](https://help.syncfusion.com/extension/syncfusion-nuget-packages/nuget-uninstallation-process) sections.

PDF NuGet packages can be installed and uninstalled using Package Manager Console. In Visual Studio, select **Tools > NuGet Package Manager > Package Manager Console** and execute the below commands in respective platforms.

N> Syncfusion components are available in [nuget.org](https://www.nuget.org/)

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
Install-package Syncfusion.Pdf.Base 
</td>
<td>
Uninstall-package Syncfusion.Pdf.Base -RemoveDependencies 
</td>
</tr>
<tr>
<td>
UWP
</td>
<td>
Install-package Syncfusion.Pdf.UWP 
</td>
<td>
Uninstall-package Syncfusion.Pdf.UWP 
</td>
</tr>
<tr>
<td>
ASP.NET Core
</td>
<td>
Install-package Syncfusion.Pdf.NETStandard
</td>
<td>
Uninstall-package Syncfusion.Pdf.NETStandard –RemoveDependencies
</td>
</tr>
<tr>
<td>
Xamarin
</td>
<td>
Install-package Syncfusion.Xamarin.Pdf 
</td>
<td>
Uninstall-package Syncfusion.Xamarin.Pdf -RemoveDependencies 
</td>
</tr>
</table>