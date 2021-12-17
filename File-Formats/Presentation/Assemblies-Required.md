---
title: Assemblies Required for PowerPoint Presentation | Syncfusion
description: This section explains about how to assemblies required to convert powerpoint presentation to PDF for various platforms and frameworks.
platform: file-formats
control: Presentation
documentation: UG
keywords: Assemblies
---
# Assemblies Required for PowerPoint Presentation

The following assemblies need to be referenced in your application
<table>
<tr>
<thead>
<th>
Platform(s)</th>
<th>
Assembly
</th>
</thead>
</tr>
<tr>
<td>
WPF, Windows Forms, ASP. NET and ASP.NET MVC<br/>
</td>
<td>
Syncfusion.Presentation.Base<br/>
Syncfusion.Compression.Base<br/>
Syncfusion.OfficeChart.Base<br/>
</td>
</tr>
<tr>
<td>
ASP.NET Core, Xamarin and Blazor<br/></td><td>
Syncfusion.Presentation.Portable<br/>Syncfusion.Compression.Portable<br/>Syncfusion.OfficeChart.Portable<br/></td></tr>
<tr>
<td>
Universal Windows Platform<br/></td><td>
Syncfusion.Presentation.UWP<br/>Syncfusion.OfficeChart.UWP<br/></td></tr>
<tr>
<td>
Windows UI Library (WinUI)<br/> .NET Multi-platform App UI (.NET MAUI)
<br/>
</td><td>
Syncfusion.Presentation.NET<br/>Syncfusion.Compression.NET<br/>
Syncfusion.OfficeChart.NET<br/>
</td></tr>
</table>

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/license-key) to know about registering Syncfusion license key in your applications to use our components.
N> Essential Presentation is only supported in .NET MAUI application targeting Windows, Android and iOS.

## Converting PowerPoint Presentation to PDF

For converting a PowerPoint Presentation to PDF, the following assemblies needed to be referenced in your application
<table>
<tr>
<thead>
<th>
Platform(s)</th>
<th>
Assembly
</th>
</thead>
</tr>
<tr>
<td>
WPF, Windows Forms, ASP. NET and ASP.NET MVC<br/>
</td>
<td>
Syncfusion.Presentation.Base<br/>
Syncfusion.Compression.Base<br/>
Syncfusion.OfficeChart.Base<br/>
Syncfusion.Pdf.Base<br/>
Syncfusion.PresentationToPDFConverter.Base<br/>
</td>
</tr>
<tr>
<td>
ASP.NET Core, Xamarin and Blazor <br/>
</td>
<td>
Syncfusion.Presentation.Portable<br/>
Syncfusion.Compression.Portable<br/>
Syncfusion.OfficeChart.Portable<br/>
Syncfusion.Pdf.Portable<br/>
Syncfusion.PresentationRenderer.Portable<br/>
Syncfusion.SkiaSharpHelper.Portable<br/>
Skiasharp
</td>
</tr>
<tr>
<td>
Windows UI Library (WinUI) and .NET Multi-platform App UI (.NET MAUI)
<br/>
</td>
<td>
Syncfusion.Presentation.NET<br/>Syncfusion.Compression.NET<br/>
Syncfusion.OfficeChart.NET<br/>Syncfusion.PresentationRenderer.NET<br/> Syncfusion.SkiaSharpHelper.NET<br/>Skiasharp
</td>
</tr>
</table>

The following assemblies are required to be referred in addition to the above mentioned assemblies for converting the chart present in the PowerPoint Presentation into PDF.
<table>
<tr>
<thead>
<th>
Platform(s)</th>
<th>
Assembly
</th>
</thead>
</tr>
<tr>
<td>
WPF, Windows Forms, ASP. NET and ASP.NET MVC<br/>
</td>
<td>
Syncfusion.OfficeChartToImageConverter.WPF<br/>
Syncfusion.SfChart.WPF<br/>
</td>
</tr>
</table>
N> 1.The “Syncfusion.OfficeChartToImageConverter.WPF” assembly is supported from .NET Framework 4.0 onwards
