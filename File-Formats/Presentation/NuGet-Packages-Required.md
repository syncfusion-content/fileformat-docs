---
title: NuGet Packages for Presentation
description: NuGet Packages for Presentation library
platform: file-formats
control: Presentation
documentation: UG
---
# NuGet Packages Required

To work with PowerPoint Presentations, the following NuGet packages need to be installed in your application.

<table>
<tr>
<td>
{{'**Platform(s)**'| markdownify }}
</td>
<td>
{{'**NuGet Package**'| markdownify }}
</td>
</tr>
<tr>
<td>
Windows Forms and WPF
</td>
<td>
Syncfusion.Presentation.Base.nupkg
</td>
</tr>
<tr>
<td>
ASP.NET and ASP.NET MVC
</td>
<td>
Syncfusion.Web.FileFormatsBase.nupkg
</td>
</tr>
<tr>
<td>
Xamarin
</td>
<td>
Syncfusion.Xamarin.Presentation.nupkg
</td>
</tr>
<tr>
<td>
Universal Windows Platform
</td>
<td>
Syncfusion.Presentation.UWP46.nupkg
</td>
</tr>
<tr>
<td>
ASP.NET Core
</td>
<td>
Syncfusion.Presentation.AspNet.Core.nupkg
</td>
</tr>
</table>

## Converting Charts in PowerPoint Presentation

In Windows Forms and WPF platforms, the below NuGet package need to be installed additionally to convert the charts present in PowerPoint presentations.

<table>
<tr>
<td>
{{'**Platforms**'| markdownify }}
</td>
<td>
{{'**NuGet Package**'| markdownify }}
</td>
</tr>
<tr>
<td>
Windows Forms and WPF
</td>
<td>
Syncfusion.OfficeChartToImageConverter.Wpf.nupkg
</td>
</tr>
</table>

N> 1. The "Syncfusion.AspNet.FileFormats.nupkg" and "Syncfusion.AspNet.Mvc.FileFormats.nupkg" packages already includes the necessary assemblies for chart conversion. So it is not needed to additionally install the “Syncfusion.OfficeChartToImageConverter.Wpf.nupkg” NuGet package in ASP.NET and ASP.NET MVC platforms.
N> 2. The "Syncfusion.OfficeChartToImageConverter.Wpf.nupkg" NuGet package is only supported from 4.0 .NET Framework onwards.

## Converting PowerPoint Presentation to PDF

For converting PowerPoint Presentation to PDF, the following NuGet packages need to be installed in your application.

<table>
<tr>
<td>
{{'**Platform(s)**'| markdownify }}
</td>
<td>
{{'**NuGet Package**'| markdownify }}
</td>
</tr>
<tr>
<td>
Windows Forms and WPF
</td>
<td>
Syncfusion.PresentationToPdfConverter.Base.nupkg
</td>
</tr>
<tr>
<td>
ASP.NET
</td>
<td>
Syncfusion.AspNet.FileFormats.nupkg
</td>
</tr>
<tr>
<td>
ASP.NET MVC
</td>
<td>
Syncfusion.AspNet.Mvc.FileFormats.nupkg
</td>
</tr>
</table>

N> Presentation to PDF/Image conversion is not supported in Xamarin, UWP and ASP.NET Core applications. 
