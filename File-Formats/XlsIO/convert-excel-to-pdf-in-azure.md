---
title: Convert Excel to PDF in Microsoft Azure | Syncfusion
description: Learn how to convert an Excel document to PDF in Azure services using .NET Excel library (XlsIO) without Microsoft Excel or interop dependencies.
platform: file-formats
control: XlsIO
documentation: UG
---

# Convert Excel to PDF in Azure Platform 

Syncfusion XlsIO is a [.NET Excel library](https://www.syncfusion.com/document-processing/excel-framework/net) used to create, read, edit and **convert Excel documents** programmatically without **Microsoft Excel** or interop dependencies. Using this library, you can **convert an Excel document to PDF in Azure Platform** within a few lines of code.

N> If this is your first time working with Azure, please refer to the dedicated Azure development resources. This section explains how to convert Excel to PDF in C# using the Excel library (XlsIO) in Azure. 

## Prerequisites 
* An active **Microsoft Azure subscription** is required. If you don’t have one, please [create an account](https://portal.azure.com/#home) before starting.

## Azure Services
<table>
<thead>
<tr>
<th>
Azure Services<br/></th><th>
NuGet packages required<br/></th></tr></thead>
<tr>
<td>
App Service (Windows)
<br/></td><td>
{{'[Syncfusion.XlsIORenderer.Net.Core](https://www.nuget.org/packages/Syncfusion.XlsIORenderer.Net.Core)' | markdownify}}</td></tr>
<tr>
<td>
App Service (Linux)
<br/></td><td>
{{'[Syncfusion.XlsIORenderer.Net.Core](https://www.nuget.org/packages/Syncfusion.XlsIORenderer.Net.Core)' | markdownify}}<br/>
{{'[SkiaSharp.NativeAssets.Linux v2.88.2](https://www.nuget.org/packages/SkiaSharp.NativeAssets.Linux/2.88.2)' | markdownify}}<br/>{{'[HarfBuzzSharp.NativeAssets.Linux v2.8.2.2](https://www.nuget.org/packages/HarfBuzzSharp.NativeAssets.Linux/2.8.2.2)' |markdownify}} <br/></td></tr>
<tr>
<td>
Azure Functions v1
 <br/></td><td>
{{'[Syncfusion.ExcelToPdfConverter.AspNet](https://www.nuget.org/packages/Syncfusion.ExcelToPdfConverter.AspNet)' |markdownify}} <br/></td></tr>
<tr>
<td>
Azure Functions v4
<br/></td><td>
{{'[Syncfusion.XlsIORenderer.Net.Core](https://www.nuget.org/packages/Syncfusion.XlsIORenderer.Net.Core)' | markdownify }}<br/></td></tr>
</table>
