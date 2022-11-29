---
title: Assemblies Required for PDF | Syncfusion
description: This section explains about the Syncfusion assemblies required to work with PDF file, and conversion such as HTML to PDF, Word to PDF, Excel to PDF, PPTX to PDF
platform: file-formats
control: PDF
documentation: UG
keywords: Assemblies
---
# Assemblies Required to work with PDF 

The following assemblies need to be referenced in your application based on the platform.
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
WPF, Windows Forms, ASP. NET and ASP.NET MVC<br/></td><td>
Syncfusion.Pdf.Base<br/>Syncfusion.Compression.Base<br/></td></tr>
<tr>
<td>
Windows Forms and WPF (Client Profile)<br/></td><td>
Syncfusion.Pdf.ClientProfile<br/>Syncfusion.Compression.Base<br/></td></tr>
<tr>
<td>
Universal Windows Platform<br/></td><td>
Syncfusion.Pdf.UWP<br/></td></tr>
<tr>
<td>
Xamarin<br/></td><td>
Syncfusion.Pdf.Portable<br/>Syncfusion.Compression.Portable<br/></td></tr>
<tr>
<td>
WinRT (Windows Store applications)<br/></td><td>
Syncfusion.Pdf.winrt<br/></td></tr>
<tr>
<td>
Windows Phone 8<br/></td><td>
Syncfusion.Pdf.WP8<br/>Syncfusion.Compression.WP8<br/></td></tr>
<tr>
<td>
Windows Phone 8.1 Silverlight<br/></td><td>
Syncfusion.Pdf.WPSilverlight<br/>Syncfusion.Compression.WPSilverlight<br/></td></tr>
<tr>
<td>
Windows Phone 8.1 WinRT<br/></td><td>
Syncfusion.Pdf.WP<br/>Syncfusion.Compression.WP<br/></td></tr>
<tr>
<td>
Silverlight<br/></td><td>
Syncfusion.Pdf.Silverlight<br/>Syncfusion.Compression.Silverlight<br/></td></tr>
<tr>
<td>
ASP.NET (Classic)<br/></td><td>
Syncfusion.Pdf.Web<br/>Syncfusion.Compression.Base<br/></td></tr>
<tr>
<td>
ASP.NET MVC (Classic)<br/></td><td>
Syncfusion.Pdf.MVC<br/>Syncfusion.Compression.Base<br/></td></tr>
<tr>
<td>
Universal (Classic)<br/></td><td>
Syncfusion.Pdf.Universal<br/></td></tr>
<tr>
<td>
Xamarin, UWP, Blazor, .NET Core and .NET Platforms<br/></td><td>
Syncfusion.Compression.Portable.dll<br/>
Syncfusion.Pdf.Portable.dll
	
<br/></td></tr>
</table>

N> The .NET Standard assemblies can be found in the following Essential Studio installation path
{Installed directory}\Syncfusion\Essential Studio\{Product version}\precompiledassemblies\{Product version}\.NET Standard 1.2\

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/license-key) to know about registering Syncfusion license key in your application to use our components.

## Converting HTML to PDF

Get the following required assemblies by downloading the HTML converter installer. Download and install the HTML converter for [Windows](https://help.syncfusion.com/file-formats/pdf/convert-html-to-pdf/advanced-installation#windows), [Linux](https://help.syncfusion.com/file-formats/pdf/convert-html-to-pdf/advanced-installation#linux), and [Mac](https://help.syncfusion.com/file-formats/pdf/convert-html-to-pdf/advanced-installation#mac) respectively. Please refer to the [advanced installation](/file-formats/pdf/convert-html-to-pdf/advanced-installation) steps for more details. 

<table>
<tr>
<thead>
<th>
Platforms</th>
<th>
Assemblies
</th>
</thead>
</tr>
<tr>
<td> 
WinForms
WPF
ASP.NET
ASP.NET MVC
</td>
<td>
<ul>
<li>Syncfusion.Compression.Base.dll</li>
<li>Syncfusion.Pdf.Base.dll</li>
<li>Syncfusion.HtmlConverter.Base.dll</li>
<li>Newtonsoft.Json package (v13.0.1 or above)</li>
</ul>
</td></tr>
<tr>
<td>
.NET/.NET Core
Blazor 
</td>
<td>
<ul>
<li>Syncfusion.Compression.Portable.dll</li>
<li>Syncfusion.Pdf.Portable.dll</li>
<li>Syncfusion.HtmlConverter.Portable.dll</li>
<li>Newtonsoft.Json package (v13.0.1 or above)</li>
</ul>
</td></tr>
</table>

N> HTML to PDF conversion is not supported in Silverlight, Windows Phone, WinRT, Universal, Xamarin and UWP applications

## Converting Word document to PDF

For converting a Word document to PDF, the following assemblies need to be referenced in your application
<table>
<tr>
<td>
Platform(s)<br/></td><td>
Assembly<br/></td></tr>
<tr>
<td>
WPF, Windows Forms, ASP. NET and ASP.NET MVC<br/></td><td>
Syncfusion.DocIO.Base<br/>Syncfusion.Compression.Base<br/>Syncfusion.OfficeChart.Base<br/>Syncfusion.Pdf.Base<br/>Syncfusion.DocToPdfConverter.Base<br/></td></tr>
<tr>
<td>
Windows Forms and WPF (Client Profile)<br/></td><td>
Syncfusion.DocIO.ClientProfile<br/>Syncfusion.Compression.Base<br/>Syncfusion.OfficeChart.Base<br/>Syncfusion.Pdf.ClientProfile<br/>Syncfusion.DocToPdfConverter.ClientProfile<br/></td></tr>
</table>

N> Word to PDF conversion is not supported in Silverlight, Windows Phone, WinRT, Universal, Xamarin and UWP applications

The following assemblies are required to be referred in addition to the above mentioned assemblies for converting the chart present in the Word document into PDF.
<table>
<tr>
<td>
Platform(s)<br/></td><td>
Assembly<br/></td></tr>
<tr>
<td>
WPF, Windows Forms, ASP. NET and ASP.NET MVC<br/></td><td>
Syncfusion.OfficeChartToImageConverter.WPF<br/>Syncfusion.SfChart.WPF<br/>Syncfusion.Shared.WPF<br/></td></tr>
</table>

N> The above mentioned assemblies is supported from .NET Framework 4.0 onwards

## Converting Excel document to PDF

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
UWP, .NET Core, Xamarin and Blazor (Server-Side)
</td>
<td>
Syncfusion.Compression.Portable<br/>
Syncfusion.XlsIO.Portable<br/>
Syncfusion.Pdf.Portable<br/>
Syncfusion.SkiaSharpHelper.Portable<br/>
Syncfusion.XlsIORenderer.Portable
</td>
</tr>
</tbody>
</table>

N> Excel to PDF conversion is supported from .NET Framework 2.0 and .NET Standard 1.4 onwards.

## Converting Presentation document to PDF

For converting a presentation document to PDF, the following assemblies need to be referenced in your application.

Presentation to PDF conversion (without charts)
<table>
<tr>
<td>
Platform(s)<br/></td><td>
Assembly<br/></td></tr>
<tr>
<td>
Windows Forms, WPF, ASP.NET, ASP.NET MVC<br/></td><td>Syncfusion.Compression.Base <br/>Syncfusion.OfficeChart.Base<br/>Syncfusion.Presentation.Base<br/>Syncfusion.Pdf.Base<br/>Syncfusion.PresentationToPdfConverter.Base<br/></td></tr>
</table>
Presentation to PDF conversion (with charts)
<table>
<tr>
<td>
Platform(s)<br/></td><td>
Assembly<br/></td></tr>
<tr>
<td>
Windows Forms, WPF, ASP.NET, ASP.NET MVC<br/></td><td>Syncfusion.Compression.Base<br/>Syncfusion.OfficeChart.Base<br/>Syncfusion.Presentation.Base<br/>Syncfusion.Shared.WPF<br/>Syncfusion.SfChart.WPF<br/>Syncfusion.OfficeChartToImageConverter.WPF<br/>Syncfusion.Pdf.Base<br/>Syncfusion.PresentationToPdfConverter.Base<br/></td></tr>
</table>

N> Presentation to PDF conversion is not supported in Silverlight, Windows Phone, WinRT, Universal, Xamarin and UWP applications.
