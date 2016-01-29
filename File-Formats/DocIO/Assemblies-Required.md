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
<tr>
<td colspan=1 rowspan=1>
Platform(s)<br/></td><td colspan=1 rowspan=1>
Assembly<br/></td></tr>
<tr>
<td colspan=1 rowspan=1>
WPF, Windows Forms, ASP. NET and ASP.NET MVC<br/></td><td colspan=1 rowspan=1>
Syncfusion.DocIO.Base<br/>Syncfusion.Compression.Base<br/>Syncfusion.OfficeChart.Base<br/></td></tr>
<tr>
<td colspan=1 rowspan=1>
Windows Forms and WPF (Client Profile)<br/></td><td colspan=1 rowspan=1>
Syncfusion.DocIO.ClientProfile<br/>Syncfusion.Compression.Base<br/>Syncfusion.OfficeChart.Base<br/></td></tr>
<tr>
<td colspan=1 rowspan=1>
Universal Windows<br/></td><td colspan=1 rowspan=1>
Syncfusion.DocIO.UWP<br/></td></tr>
<tr>
<td colspan=1 rowspan=1>
Xamarin<br/></td><td colspan=1 rowspan=1>
Syncfusion.DocIO.Portable<br/>Syncfusion.Compression.Portable<br/></td></tr>
<tr>
<td colspan=1 rowspan=1>
WinRT (Windows Store applications)<br/></td><td colspan=1 rowspan=1>
Syncfusion.DocIO.winrt<br/></td></tr>
<tr>
<td colspan=1 rowspan=1>
Windows Phone 8<br/></td><td colspan=1 rowspan=1>
Syncfusion.DocIO.WP8<br/>Syncfusion.Compression.WP8<br/></td></tr>
<tr>
<td colspan=1 rowspan=1>
Windows Phone 8.1 Silverlight<br/></td><td colspan=1 rowspan=1>
Syncfusion.DocIO.WPSilverlight<br/>Syncfusion.Compression.WPSilverlight<br/></td></tr>
<tr>
<td colspan=1 rowspan=1>
Windows Phone 8.1 WinRT<br/></td><td colspan=1 rowspan=1>
Syncfusion.DocIO.WP<br/>Syncfusion.Compression.WP<br/></td></tr>
<tr>
<td colspan=1 rowspan=1>
Silverlight<br/></td><td colspan=1 rowspan=1>
Syncfusion.DocIO.Silverlight<br/>Syncfusion.Compression.Silverlight<br/></td></tr>
<tr>
<td colspan=1 rowspan=1>
ASP.NET (Classic)<br/></td><td colspan=1 rowspan=1>
Syncfusion.DocIO.Web<br/>Syncfusion.Compression.Base<br/>Syncfusion.OfficeChart.Base<br/></td></tr>
<tr>
<td colspan=1 rowspan=1>
ASP.NET MVC (Classic)<br/></td><td colspan=1 rowspan=1>
Syncfusion.DocIO.MVC<br/>Syncfusion.Compression.Base<br/>Syncfusion.OfficeChart.Base<br/></td></tr>
<tr>
<td colspan=1 rowspan=1>
Universal (Classic)<br/></td><td colspan=1 rowspan=1>
Syncfusion.DocIO.Universal<br/></td></tr>
</table>

## Converting Word document to PDF

For converting a Word document to PDF, the following assemblies need to be referenced in your application
<table>
<tr>
<td colspan=1 rowspan=1>
Platform(s)<br/></td><td colspan=1 rowspan=1>
Assembly<br/></td></tr>
<tr>
<td colspan=1 rowspan=1>
WPF, Windows Forms, ASP. NET and ASP.NET MVC<br/></td><td colspan=1 rowspan=1>
Syncfusion.DocIO.Base<br/>Syncfusion.Compression.Base<br/>Syncfusion.OfficeChart.Base<br/>Syncfusion.Pdf.Base<br/>Syncfusion.DocToPdfConverter.Base<br/></td></tr>
<tr>
<td colspan=1 rowspan=1>
Windows Forms and WPF (Client Profile)<br/></td><td colspan=1 rowspan=1>
Syncfusion.DocIO.ClientProfile<br/>Syncfusion.Compression.Base<br/>Syncfusion.OfficeChart.Base<br/>Syncfusion.Pdf.ClientProfile<br/>Syncfusion.DocToPdfConverter.ClientProfile<br/></td></tr>
</table>
N> Word to PDF conversion is not supported in Silverlight, Windows Phone, WinRT, Universal, Xamarin and UWP applications
The following assemblies are required to be referred in addition to the above mentioned assemblies for converting the chart present in the Word document into PDF.
<table>
<tr>
<td colspan=1 rowspan=1>
Platform(s)<br/></td><td colspan=1 rowspan=1>
Assembly<br/></td></tr>
<tr>
<td colspan=1 rowspan=1>
WPF, Windows Forms, ASP. NET and ASP.NET MVC<br/></td><td colspan=1 rowspan=1>
Syncfusion.OfficeChartToImageConverter.WPF<br/>Syncfusion.SfChart.WPF<br/>Syncfusion.Shared.WPF<br/></td></tr>
</table>
N> The above mentioned assemblies is supported from .NET Framework 4.0 onwards