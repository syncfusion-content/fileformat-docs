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
{{'[WPF](https://help.syncfusion.com/file-formats/pdf/create-pdf-file-in-wpf)' | markdownify}}, {{'[Windows Forms](https://help.syncfusion.com/file-formats/pdf/create-pdf-file-in-windows-forms)' | markdownify}}, {{'[ ASP. NET](https://help.syncfusion.com/file-formats/pdf/create-pdf-file-in-asp-net-web-forms)' | markdownify}} and {{'[ASP.NET MVC](https://help.syncfusion.com/file-formats/pdf/create-pdf-file-in-asp-net-mvc)' | markdownify}}<br/></td><td>
Syncfusion.Pdf.Base<br/>Syncfusion.Compression.Base<br/></td></tr>
<tr>
<td>
{{'[Windows Forms](https://help.syncfusion.com/file-formats/pdf/create-pdf-file-in-windows-forms)' | markdownify}} and {{'[WPF (Client Profile)](https://help.syncfusion.com/file-formats/pdf/create-pdf-file-in-wpf)' | markdownify}}<br/></td><td>
Syncfusion.Pdf.ClientProfile<br/>Syncfusion.Compression.Base<br/></td></tr>
<tr>
<td>
{{'[Universal Windows Platform](https://help.syncfusion.com/file-formats/pdf/create-pdf-file-in-uwp)' | markdownify}}<br/></td><td>
Syncfusion.Pdf.UWP<br/></td></tr>
<tr>
<td>
{{'[Xamarin](https://help.syncfusion.com/file-formats/pdf/create-pdf-file-in-xamarin)' | markdownify}}<br/></td><td>
Syncfusion.Pdf.Portable<br/>Syncfusion.Compression.Portable<br/></td></tr>
<tr>
<td>
{{'[ASP.NET (Classic)](https://help.syncfusion.com/file-formats/pdf/create-pdf-file-in-asp-net-web-forms)' | markdownify}}<br/></td><td>
Syncfusion.Pdf.Web<br/>Syncfusion.Compression.Base<br/></td></tr>
<tr>
<td>
{{'[ASP.NET MVC (Classic)](https://help.syncfusion.com/file-formats/pdf/create-pdf-file-in-asp-net-mvc)' | markdownify}}<br/></td><td>
Syncfusion.Pdf.MVC<br/>Syncfusion.Compression.Base<br/></td></tr>
<tr>
<td>
{{'[Blazor](https://help.syncfusion.com/file-formats/pdf/create-pdf-document-in-blazor)' | markdownify}}, {{'[.NET Core](https://help.syncfusion.com/file-formats/pdf/create-pdf-file-in-asp-net-core)' | markdownify}} and {{'[.NET Platforms](https://help.syncfusion.com/file-formats/pdf/create-pdf-file-in-asp-net-mvc)' | markdownify}}<br/></td><td>
Syncfusion.Compression.Portable.dll<br/>
Syncfusion.Pdf.Portable.dll
	
<br/></td></tr>
<tr>
<td>
{{'[Windows UI library (WinUI)](https://help.syncfusion.com/file-formats/pdf/create-pdf-file-in-winui)' | markdownify}}<br/>
{{'[.NET Multi-platform App UI (.NET MAUI)](https://help.syncfusion.com/file-formats/pdf/create-pdf-file-in-maui)' | markdownify}}</td><td>
Syncfusion.Pdf.NET.dll<br/>
Syncfusion.Compression.NET.dll
	
<br/></td></tr>
</table>

## RETIRED PRODUCTS

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
WinRT (Windows Store applications)<br/></td><td>
Syncfusion.Pdf.winrt</td></tr>
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
</table>


N> The .NET Standard assemblies can be found in the following Essential Studio installation path
{Installed directory}\Syncfusion\Essential Studio\{Product version}\precompiledassemblies\{Product version}\.NET Standard 1.2\

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.

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
.NET/.NET Core<br/>
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
<thead>
<tr>
<th>
Platform(s)<br/></th><th>
Assembly<br/></th></tr></thead>
<tr>
<td>
WPF, Windows Forms, ASP. NET, and ASP.NET MVC<br/></td><td>
Syncfusion.DocIO.Base<br/>Syncfusion.Compression.Base<br/>Syncfusion.OfficeChart.Base<br/>Syncfusion.Pdf.Base<br/>Syncfusion.DocToPdfConverter.Base<br/></td></tr>
<tr>
<td>
Windows Forms and WPF (Client Profile)<br/></td><td>
Syncfusion.DocIO.ClientProfile<br/>Syncfusion.Compression.Base<br/>Syncfusion.OfficeChart.Base<br/>Syncfusion.Pdf.ClientProfile<br/>Syncfusion.DocToPdfConverter.ClientProfile<br/></td></tr>
<tr>
<td>
ASP.NET Core, Xamarin and Blazor<br/></td><td>
Syncfusion.DocIO.Portable<br/>Syncfusion.Compression.Portable<br/>Syncfusion.OfficeChart.Portable<br/>Syncfusion.Pdf.Portable<br/>Syncfusion.DocIORenderer.Portable<br/>SkiaSharp.HarfBuzz<br/>Syncfusion.SkiaSharpHelper.Portable</td></tr>
<tr>
<td>
Windows UI Library (WinUI)<br/> .NET Multi-platform App UI (.NET MAUI)<br/>
</td><td>
Syncfusion.DocIO.NET<br/>Syncfusion.Compression.NET<br/>Syncfusion.OfficeChart.NET<br/>Syncfusion.Pdf.NET<br/>Syncfusion.DocIORenderer.NET<br/> SkiaSharp<br/>Syncfusion.SkiaSharpHelper.NET</td></tr>
</table>

N> 1. Word to PDF conversion is supported in ASP.NET Core and Xamarin from 2018 Volume 1 release (v16.1.0.24) using SkiaSharp graphics library.
N> 2. Word to PDF conversion is not supported in Silverlight, Windows Phone, WinRT, Universal applications.
N> 3. Starting with v17.1.0.x, if you reference "Syncfusion.DocIORenderer", you also have to add "Syncfusion.SkiaSharpHelper" assembly reference in your projects to perform Word to PDF conversion.

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
UWP, .NET Core, Xamarin, and Blazor (Server-Side)
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

N> The "Syncfusion.OfficeChartToImageConverter.WPF" assembly is supported from .NET Framework 4.0 onwards.
