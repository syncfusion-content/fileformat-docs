---
title: Assemblies Required
description: Briefs the assemblies required for various platforms and frameworks.
platform: File-formats
control: XlsIO
---

# Assemblies Required

The following assemblies need to be referenced in your application based on the platform.
<table>
<tr>
<thead><th>
Platform(s)</th>
<th>
Assembly
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
WPF, Windows Forms, ASP. NET and ASP.NET MVC
</td>
<td>
Syncfusion.XlsIO.Base<br/>
Syncfusion.Compression.Base
</td>
</tr>
<tr>
<td>
Windows Forms and WPF (Client Profile)
</td>
<td>
Syncfusion.XlsIO.ClientProfile<br/>
Syncfusion.Compression.Base
</td>
</tr>
<tr>
<td>
Universal Windows
</td>
<td>
Syncfusion.XlsIO.UWP
</td>
</tr>
<tr>
<td>
Xamarin
</td>
<td>
Syncfusion.XlsIO.Portable<br/>
Syncfusion.Compression.Portable
</td>
</tr>
<tr>
<td>
WinRT (Windows Store applications)
</td>
<td>
Syncfusion.XlsIO.WinRT
</td>
</tr>
<tr>
<td>
Windows Phone 8
</td>
<td>
Syncfusion.XlsIO.WP8<br/>
Syncfusion.Compression.WP8
</td>
</tr>
<tr>
<td>
Windows Phone 8.1 Silverlight
</td>
<td>
Syncfusion.XlsIO.WPSilverlight<br/>
Syncfusion.Compression.WPSilverlight
</td>
</tr>
<tr>
<td>
Windows Phone 8.1 WinRT
</td>
<td>
Syncfusion.XlsIO.WP<br/>
Syncfusion.Compression.WP
</td>
</tr>
<tr>
<td>
Silverlight
</td>
<td>
Syncfusion.XlsIO.Silverlight<br/>
Syncfusion.Compression.Silverlight
</td>
</tr>
<tr>
<td>
ASP.NET (Classic)
</td>
<td>
Syncfusion.XlsIO.Web<br/>
Syncfusion.Compression.Base
</td>
</tr>
<tr>
<td>
ASP.NET MVC (Classic)
</td>
<td>
Syncfusion.XlsIO.MVC<br/>
Syncfusion.Compression.Base
</td>
</tr>
<tr>
<td>
Universal (Classic)
</td>
<td>
Syncfusion.XlsIO.Universal
</td>
</tr>
</tbody>
</table>

## Converting Excel document to PDF

For converting an Excel document to PDF, the following assemblies need to be referenced in your application
<table>
<tr>
<th>
Platform(s)
</th>
<th>
Assembly
</th>
</tr>
<tbody>
<tr>
<td>
WPF, Windows Forms, ASP. NET and ASP.NET MVC
</td>
<td>
Syncfusion.XlsIO.Base<br/>
Syncfusion.Compression.Base<br/>
Syncfusion.Pdf.Base<br/>
Syncfusion.ExcelToPDFConverter.Base
</td>
</tr>
<tr>
<td>
Windows Forms and WPF (Client Profile)
</td>
<td>
Syncfusion.XlsIO.ClientProfile<br/>
Syncfusion.Compression.Base<br/>
Syncfusion.Pdf.ClientProfile<br/>
Syncfusion.ExcelToPDFConverter.ClientProfile
</td>
</tr>
</tbody>
</table>

N> Excel to PDF conversion is not supported in Silverlight, Windows Phone, WinRT, Universal, Xamarin and UWP applications.

The following assemblies are to be referred in addition to the above mentioned assemblies for converting charts present in the Excel document into PDF/Image.
<table>
<tr>
<th>
Platform(s)
</th>
<th>
Assembly
</th>
</tr>
<tbody>
<tr>
<td>
WPF, Windows Forms, ASP. NET and ASP.NET MVC
</td>
<td>
Syncfusion.ExcelChartToImageConverter.WPF<br/>
Syncfusion.SfChart.WPF<br/>
Syncfusion.Shared.WPF
</td>
</tr>
</tbody>
</table>

N> The above mentioned assemblies are supported from .NET Framework 4.0 onwards.
