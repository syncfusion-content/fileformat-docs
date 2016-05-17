---
title: Assemblies Required
description: Briefs the assemblies required for various platforms and frameworks.
platform: file-formats
control: Presentation
documentation: UG
keywords: Assemblies
---
# Assemblies Required

The following assemblies need to be referenced in your application
<table>
<tr>
<td>
Platform(s)<br/>
</td>
<td>
Assembly<br/>
</td>
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
Xamarin<br/></td><td>
Syncfusion.Presentation.Portable<br/>Syncfusion.Compression.Portable<br/>Syncfusion.OfficeChart.Portable<br/></td></tr>
<tr>
<td>
Universal Windows Platform<br/></td><td>
Syncfusion.Presentation.UWP<br/>Syncfusion.OfficeChart.UWP<br/></td></tr>
</table>

## Converting PowerPoint Presentation to PDF

For converting a PowerPoint Presentation to PDF, the following assemblies needed to be referenced in your application
<table>
<tr>
<td>
Platform(s)<br/>
</td>
<td>
Assembly<br/>
</td>
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
</table>
N> Presentation to PDF conversion is not supported in Xamarin and UWP applications.
The following assemblies are required to be referred in addition to the above mentioned assemblies for converting the chart present in the PowerPoint Presentation into PDF.
<table>
<tr>
<td>
Platform(s)<br/>
</td>
<td>
Assembly<br/>
</td>
</tr>
<tr>
<td>
WPF, Windows Forms, ASP. NET and ASP.NET MVC</br>
</td>
<td>
Syncfusion.OfficeChartToImageConverter.WPF<br/>
Syncfusion.SfChart.WPF<br/>
Syncfusion.Shared.WPF<br/>
</td>
</tr>
</table>
N> The above mentioned “Syncfusion.OfficeChartToImageConverter.WPF” assembly is supported from .NET Framework 4.0 onwards
