---
title: Assemblies Required
description: Assemblies required to use DocIO
platform: file-formats
control: DocIO
documentation: UG
---

# Assemblies Required

The following assemblies need to be referenced in your application based on the platform.

<table>
<thead>
<tr>
<td>
Platform(s)<br/></td><td>
Assembly<br/></td></tr></thead>
<tr>
<td>
WPF, Windows Forms, ASP. NET and ASP.NET MVC<br/></td><td>
Syncfusion.DocIO.Base<br/>Syncfusion.Compression.Base<br/>Syncfusion.OfficeChart.Base<br/></td></tr>
<tr>
<td>
Windows Forms and WPF (Client Profile)<br/></td><td>
Syncfusion.DocIO.ClientProfile<br/>Syncfusion.Compression.Base<br/>Syncfusion.OfficeChart.Base<br/></td></tr>
<tr>
<td>
ASP.NET Core and Xamarin<br/></td><td>
Syncfusion.DocIO.Portable<br/>Syncfusion.Compression.Portable<br/>Syncfusion.OfficeChart.Portable<br/></td></tr>
<tr>
<td>
Universal Windows Platform<br/></td><td>
Syncfusion.DocIO.UWP<br/>Syncfusion.OfficeChart.UWP<br/></td></tr>
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
ASP.NET (Classic)<br/></td><td>
Syncfusion.DocIO.Web<br/>Syncfusion.Compression.Base<br/>Syncfusion.OfficeChart.Base<br/></td></tr>
<tr>
<td>
ASP.NET MVC (Classic)<br/></td><td>
Syncfusion.DocIO.MVC<br/>Syncfusion.Compression.Base<br/>Syncfusion.OfficeChart.Base<br/></td></tr>
<tr>
<td>
Universal (Classic)<br/></td><td>
Syncfusion.DocIO.Universal<br/></td></tr>
</table>

## Converting Word document to PDF

For converting a Word document to PDF, the following assemblies need to be referenced in your application
<table>
<thead>
<tr>
<td>
Platform(s)<br/></td><td>
Assembly<br/></td></tr></thead>
<tr>
<td>
WPF, Windows Forms, ASP. NET and ASP.NET MVC<br/></td><td>
Syncfusion.DocIO.Base<br/>Syncfusion.Compression.Base<br/>Syncfusion.OfficeChart.Base<br/>Syncfusion.Pdf.Base<br/>Syncfusion.DocToPdfConverter.Base<br/></td></tr>
<tr>
<td>
Windows Forms and WPF (Client Profile)<br/></td><td>
Syncfusion.DocIO.ClientProfile<br/>Syncfusion.Compression.Base<br/>Syncfusion.OfficeChart.Base<br/>Syncfusion.Pdf.ClientProfile<br/>Syncfusion.DocToPdfConverter.ClientProfile<br/></td></tr>
<tr>
<td>
ASP.NET Core and Xamarin<br/></td><td>
Syncfusion.DocIO.Portable<br/>Syncfusion.Compression.Portable<br/>Syncfusion.OfficeChart.Portable<br/>Syncfusion.Pdf.Portable<br/>Syncfusion.DocIORenderer.Portable<br/>SkiaSharp</tr>
</table>
N> Word to PDF conversion is supported in ASP.NET Core and Xamarin from 2018 Volume 1 release (v16.1.0.24) using SkiaSharp library.
N> Word to PDF conversion is not supported in Silverlight, Windows Phone, WinRT, Universal and UWP applications
The following assemblies are required to be referred in addition to the above mentioned assemblies for converting the chart present in the Word document into PDF.
<table>
<thead>
<tr>
<td>
Platform(s)<br/></td><td>
Assembly<br/></td></tr></thead>
<tr>
<td>
WPF, Windows Forms, ASP. NET and ASP.NET MVC<br/></td><td>
Syncfusion.OfficeChartToImageConverter.WPF<br/>Syncfusion.SfChart.WPF<br/></td></tr>
</table>
N> 1. The above mentioned assemblies is supported from .NET Framework 4.0 onwards.
N> 2. Chart conversion is not supported in ASP.NET Core and Xamarin platforms.