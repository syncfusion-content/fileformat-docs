---
title: Convert PPTX to PDF in Microsoft Azure | Syncfusion
description: Learn how to convert a PPTX to PDF in Azure services using .NET PowerPoint library (Presentation) without Microsoft PowerPoint or interop dependencies.
platform: file-formats
control: PowerPoint
documentation: UG
---

# Convert PowerPoint Presentation to PDF in Azure Platform 

Syncfusion PowerPoint is a [.NET PowerPoint library](https://www.syncfusion.com/document-processing/powerpoint-framework/net) used to create, read, edit and **convert PowerPoint documents** programmatically without **Microsoft PowerPoint** or interop dependencies. Using this library, you can **convert a PowerPoint Presentation to PDF in Azure Platform** within a few lines of code.

N> If this is your first time working with Azure, please refer to the dedicated Azure development resources. This section explains how to convert PowerPoint Presentation to PDF in C# using the PowerPoint library (Presentation) in Azure. 

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
{{'[Syncfusion.PresentationRenderer.Net.Core](https://www.nuget.org/packages/Syncfusion.PresentationRenderer.Net.Core)' | markdownify}}</td></tr>
<tr>
<td>
App Service (Linux)
<br/></td><td>
{{'[Syncfusion.PresentationRenderer.Net.Core](https://www.nuget.org/packages/Syncfusion.PresentationRenderer.Net.Core)' | markdownify}}<br/>
{{'[SkiaSharp.NativeAssets.Linux v2.88.2](https://www.nuget.org/packages/SkiaSharp.NativeAssets.Linux/2.88.2)' | markdownify}}<br/>{{'[HarfBuzzSharp.NativeAssets.Linux v2.8.2.2](https://www.nuget.org/packages/HarfBuzzSharp.NativeAssets.Linux/2.8.2.2)' |markdownify}} <br/></td></tr>
<tr>
<td>
Azure Functions v1
 <br/></td><td>
{{'[Syncfusion.PresentationToPdfConverter.AspNet](https://www.nuget.org/packages/Syncfusion.PresentationToPdfConverter.AspNet)' |markdownify}} <br/></td></tr>
<tr>
<td>
Azure Functions v4
<br/></td><td>
{{'[Syncfusion.PresentationRenderer.Net.Core](https://www.nuget.org/packages/Syncfusion.PresentationRenderer.Net.Core)' | markdownify }}<br/></td></tr>
</table>
