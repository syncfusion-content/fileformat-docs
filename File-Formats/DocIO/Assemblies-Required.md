---
title: Assemblies Required for DocIO | Syncfusion
description: This section illustrates the assemblies required to use Syncfusion Word library (Essential DocIO) in various platforms and frameworks
platform: file-formats
control: DocIO
documentation: UG
---

# Assemblies Required

The following assemblies need to be referenced in your application based on the platform.

<table>
<thead>
<tr>
<th>
Platform(s)<br/></th><th>
Assembly<br/></th></tr></thead>
<tr>
<td>
WPF, Windows Forms, ASP. NET, ASP.NET MVC<br/></td><td>
Syncfusion.DocIO.Base<br/>Syncfusion.Compression.Base<br/>Syncfusion.OfficeChart.Base<br/></td></tr>
<tr>
<td>
Windows Forms and WPF (Client Profile)<br/></td><td>
Syncfusion.DocIO.ClientProfile<br/>Syncfusion.Compression.Base<br/>Syncfusion.OfficeChart.Base<br/></td></tr>
<tr>
<td>
ASP.NET Core, Xamarin and Blazor<br/></td><td>
Syncfusion.DocIO.Portable<br/>Syncfusion.Compression.Portable<br/>Syncfusion.OfficeChart.Portable<br/></td></tr>
<tr>
<td>
Universal Windows Platform<br/></td><td>
Syncfusion.DocIO.UWP<br/>Syncfusion.OfficeChart.UWP<br/></td></tr>
<tr>
<td>
ASP.NET (Classic)<br/></td><td>
Syncfusion.DocIO.Web<br/>Syncfusion.Compression.Base<br/>Syncfusion.OfficeChart.Base<br/></td></tr>
<tr>
<td>
ASP.NET MVC (Classic)<br/></td><td>
Syncfusion.DocIO.MVC<br/>Syncfusion.Compression.Base<br/>Syncfusion.OfficeChart.Base<br/></td></tr>
<tr>
<td>
WinRT (Windows Store applications)<br/></td><td>
Syncfusion.DocIO.winrt<br/></td></tr>
<tr>
<td>
Windows Phone 8<br/></td><td>
Syncfusion.DocIO.WP8<br/>Syncfusion.Compression.WP8<br/></td></tr>
<tr>
<td>
Windows Phone 8.1 Silverlight<br/></td><td>
Syncfusion.DocIO.WPSilverlight<br/>Syncfusion.Compression.WPSilverlight<br/></td></tr>
<tr>
<td>
Windows Phone 8.1 WinRT<br/></td><td>
Syncfusion.DocIO.WP<br/>Syncfusion.Compression.WP<br/></td></tr>
<tr>
<td>
Silverlight<br/></td><td>
Syncfusion.DocIO.Silverlight<br/>Syncfusion.Compression.Silverlight<br/></td></tr>
<tr>
<td>
Universal (Classic)<br/></td><td>
Syncfusion.DocIO.Universal<br/></td></tr>
<tr>
<td>
Windows UI Library (WinUI)<br/> .NET Multi-platform App UI (.NET MAUI)<br/>
N> Support to run the DocIO applications in Windows, Android and iOS only.
</td><td>
Syncfusion.DocIO.NET<br/></td></tr>
</table>

N> 1. Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/license-key) to know about registering Syncfusion license key in your application to use our components.
N> 2. Syncfusion components are available in [nuget.org](https://www.nuget.org/)
N> 3. Starting with v15.3.0.x, a new Visual Studio add-in "Syncfusion Reference Manager" for WPF, and Windows Forms platforms is included. Using this add-in, you can easily add the necessary reference assemblies to your projects in an automated way. Please refer to this [link](https://help.syncfusion.com/extension/syncfusion-reference-manager/overview) for more information.
N> 4. Starting with v17.3.0.x, Syncfusion provides support to .NET Core 3.0. You can use the above WPF or Windows Forms platform assemblies for .NET Core 3.0 targeting applications and use the same "C# tab" code examples for it.

## Converting Word document to PDF

For converting a Word document to PDF, the following assemblies need to be referenced in your application
<table>
<thead>
<tr>
<th>
Platform(s)<br/></th><th>
Assembly<br/></th></tr></thead>
<tr>
<td>
WPF, Windows Forms, ASP. NET, ASP.NET MVC<br/></td><td>
Syncfusion.DocIO.Base<br/>Syncfusion.Compression.Base<br/>Syncfusion.OfficeChart.Base<br/>Syncfusion.Pdf.Base<br/>Syncfusion.DocToPdfConverter.Base<br/></td></tr>
<tr>
<td>
Windows Forms and WPF (Client Profile)<br/></td><td>
Syncfusion.DocIO.ClientProfile<br/>Syncfusion.Compression.Base<br/>Syncfusion.OfficeChart.Base<br/>Syncfusion.Pdf.ClientProfile<br/>Syncfusion.DocToPdfConverter.ClientProfile<br/></td></tr>
<tr>
<td>
ASP.NET Core, Xamarin and Blazor<br/></td><td>
Syncfusion.DocIO.Portable<br/>Syncfusion.Compression.Portable<br/>Syncfusion.OfficeChart.Portable<br/>Syncfusion.Pdf.Portable<br/>Syncfusion.DocIORenderer.Portable<br/>SkiaSharp<br/>Syncfusion.SkiaSharpHelper.Portable</td></tr>
<tr>
<td>
Windows UI Library (WinUI)<br/> .NET Multi-platform App UI (.NET MAUI)<br/>
N> Support to run the DocIO applications in Windows, Android and iOS only.
</td><td>
Syncfusion.DocIORenderer.NET<br/></td></tr>
</table>

N> 1. Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/license-key) to know about registering Syncfusion license key in your application to use our components.
N> 2. Syncfusion components are available in [nuget.org](https://www.nuget.org/)
N> 3. Starting with v15.3.0.x, a new Visual Studio add-in "Syncfusion Reference Manager" for WPF, and Windows Forms platforms is included. Using this add-in, you can easily add the necessary reference assemblies to your projects in an automated way. Please refer to this [link](https://help.syncfusion.com/extension/syncfusion-reference-manager/overview) for more information.
N> 4. Word to PDF conversion is supported in ASP.NET Core and Xamarin from 2018 Volume 1 release (v16.1.0.24) using SkiaSharp graphics library.
N> 5. Word to PDF conversion is not supported in Silverlight, Windows Phone, WinRT, Universal applications.
N> 6. Starting with v17.1.0.x, if you reference "Syncfusion.DocIORenderer", you also have to add "Syncfusion.SkiaSharpHelper" assembly reference in your projects to perform Word to PDF conversion.

## Converting Charts

The following assemblies are required to be referred in addition to the above mentioned assemblies for converting the chart present in the Word document into PDF.
<table>
<thead>
<tr>
<th>
Platform(s)<br/></th><th>
Assembly<br/></th></tr></thead>
<tr>
<td>
WPF, Windows Forms, ASP. NET, ASP.NET MVC<br/></td><td>
Syncfusion.OfficeChartToImageConverter.WPF<br/>Syncfusion.SfChart.WPF<br/></td></tr>
</table>
N> 1. Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/license-key) to know about registering Syncfusion license key in your application to use our components.
N> 2. Syncfusion components are available in [nuget.org](https://www.nuget.org/)
N> 3. Starting with v15.3.0.x, a new Visual Studio add-in "Syncfusion Reference Manager" for WPF, and Windows Forms platforms is included. Using this add-in, you can easily add the necessary reference assemblies to your projects in an automated way. Please refer to this [link](https://help.syncfusion.com/extension/syncfusion-reference-manager/overview) for more information.
N> 4. The above mentioned assemblies is supported from .NET Framework 4.0 onwards.