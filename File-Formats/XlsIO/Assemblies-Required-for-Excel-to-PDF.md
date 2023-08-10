---
title: Execl to PDF Assemblies Required | Syncfusion
description: Briefs the assemblies required to convert excel document to PDF for various platforms and frameworks.
platform: file-formats
control: XlsIO
documentation: UG
---

# Assemblies Required for Excel to PDF conversion

For converting an Excel document to PDF, the following assemblies need to be referenced in your application.

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
<tr>
<td>
UWP, .NET Core, Xamarin, and Blazor
</td>
<td>
Syncfusion.Compression.Portable<br/>
Syncfusion.XlsIO.Portable<br/>
Syncfusion.Pdf.Portable<br/>
Syncfusion.SkiaSharpHelper.Portable<br/>
Syncfusion.XlsIORenderer.Portable
</td>
</tr>
<tr>
<td>
WinUI and .NET MAUI
</td>
<td>
Syncfusion.Compression.NET<br/>
Syncfusion.XlsIO.NET<br/>
Syncfusion.Pdf.NET<br/>
Syncfusion.SkiaSharpHelper.NET<br/>
Syncfusion.XlsIORenderer.NET<br/>
</td>
</tr>
</tbody>
</table>

N> Excel to PDF conversion is supported from .NET Framework 2.0 and .NET Standard 1.4 onwards.

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your applications to use our components.

N> Syncfusion components are available in nuget.org


