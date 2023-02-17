---
title: Migrate from net framework to net core | Presentation | Syncfusion
description: This section illustrates migrating Syncfusion .NET PowerPoint (Presentation) library from .NET Framework to .NET core.
platform: file-formats
control: Presentation
documentation: UG
---
# Migrate Presentation library from .NET Framework to .NET Core
In this section, we will see about the changes which need to be considered while migrating Syncfusion .NET PowerPoint (Presentation) library from .NET Framework to .NET Core.

## NuGet Packages

<table>
<tr>
<thead>
<th>
{{'**Packages targeting .NET Framework**'| markdownify }}
</th>
<th>
{{'**Packages targeting .NET Standard 2.0/.NET Core**'| markdownify }}
</th>
</thead>
</tr>
<tr>
<td>
{{'[Syncfusion.Presentation.WinForms](https://www.nuget.org/packages/Syncfusion.Presentation.WinForms/#"")'| markdownify }}<br/>
{{'[Syncfusion.Presentation.Wpf](https://www.nuget.org/packages/Syncfusion.Presentation.Wpf/#"")'| markdownify }}<br/>
{{'[Syncfusion.Presentation.AspNet](https://www.nuget.org/packages/Syncfusion.Presentation.AspNet/#"")'| markdownify }}<br/>
{{'[Syncfusion.Presentation.AspNet.Mvc5](https://www.nuget.org/packages/Syncfusion.Presentation.AspNet.Mvc5/#"")'| markdownify }}<br/>
{{'[Syncfusion.Presentation.AspNet.Mvc4](https://www.nuget.org/packages/Syncfusion.Presentation.AspNet.Mvc4/#"")'| markdownify }}
</td>
<td>
{{'[Syncfusion.Presentation.Net.Core](https://www.nuget.org/packages/Syncfusion.Presentation.Net.Core/#"")'| markdownify }}
</td>
</tr>
<tr>
<td>
{{'[Syncfusion.PresentationToPDFConverter.WinForms](https://www.nuget.org/packages/Syncfusion.PresentationToPdfConverter.WinForms/#"")'| markdownify }}<br/>
{{'[Syncfusion.PresentationToPDFConverter.Wpf](https://www.nuget.org/packages/Syncfusion.PresentationToPdfConverter.Wpf/#"")'| markdownify }}<br/>
{{'[Syncfusion.PresentationToPDFConverter.AspNet](https://www.nuget.org/packages/Syncfusion.PresentationToPdfConverter.AspNet/#"")'| markdownify }}<br/>
{{'[Syncfusion.PresentationToPDFConverter.AspNet.Mvc4](https://www.nuget.org/packages/Syncfusion.PresentationToPdfConverter.AspNet.Mvc4/#"")'| markdownify }}<br/>
{{'[Syncfusion.PresentationToPDFConverter.AspNet.Mvc5](https://www.nuget.org/packages/Syncfusion.PresentationToPdfConverter.AspNet.Mvc5/#"")'| markdownify }}
</td>
<td>
{{'[Syncfusion.PresentationRenderer.Net.Core](https://www.nuget.org/packages/Syncfusion.PresentationRenderer.Net.Core/#"")'| markdownify }}
</td>
</tr>
</table>

## Namespace changes

<table>
<tr>
<thead>
<th>
{{'**.NET Framework**'| markdownify }}
</th>
<th>
{{'**Alternate Namespace in .NET Core**'| markdownify }}
</th>
</thead>
</tr>
<tr>
<td>
Syncfusion.PresentationToPdfConverter
</td>
<td>
Syncfusion.PresentationRenderer
</td>
</tr>
<tr>
<td>
Syncfusion.OfficeChartToImageConverter
</td>
<td>
Not applicable - Classes are moved within Syncfusion.PresentationRenderer namespace.
</td>
</tr>
</table>

## Type changes

<table>
<tr>
<thead>
<th>
{{'**Missing Types**'| markdownify }}
</th>
<th>
{{'**Alternate Types in .NET Core**'| markdownify }}
</th>
</thead>
</tr>
<tr>
<td>
{{'[ChartToImageConverter](https://help.syncfusion.com/cr/file-formats/Syncfusion.OfficeChartToImageConverter.ChartToImageConverter.html#"")'| markdownify }}
</td>
<td>
Not applicable - It is handled internally.
</td>
</tr>
</table>

## Property changes

<table>
<tr>
<thead>
<th>
{{'**Missing properties**'| markdownify }}
</th>
<th>
{{'**Alternate properties in .NET Core**'| markdownify }}
</th>
</thead>
</tr>
<tr>
<td>
{{'[IPresentation.ChartToImageConverter](https://help.syncfusion.com/cr/file-formats/Syncfusion.Presentation.IPresentation.html#Syncfusion_Presentation_IPresentation_ChartToImageConverter"")'| markdownify }}
</td>
<td>
Not applicable - It is handled internally.
</td>
</tr>
<tr>
<td>
{{'[PresentationToPdfConverterSettings.EnablePortableRendering](https://help.syncfusion.com/cr/file-formats/Syncfusion.PresentationToPdfConverter.PresentationToPdfConverterSettings.html#Syncfusion_PresentationToPdfConverter_PresentationToPdfConverterSettings_EnablePortableRendering"")'| markdownify }}
</td>
<td>
This is the default approach in .NET Core and handled internally.
</td>
</tr>
<tr>
<td>
{{'[PresentationToPdfConverterSettings.RecreateNestedMetafile](https://help.syncfusion.com/cr/file-formats/Syncfusion.PresentationToPdfConverter.PresentationToPdfConverterSettings.html#Syncfusion_PresentationToPdfConverter_PresentationToPdfConverterSettings_RecreateNestedMetafile"")'| markdownify }}
</td>
<td>
Not supported due to .NET Core limitations.
</td>
</tr>
<tr>
<td>
{{'[ITextBody.FitTextOption](https://help.syncfusion.com/cr/file-formats/Syncfusion.Presentation.ITextBody.html#Syncfusion_Presentation_ITextBody_FitTextOption"")'| markdownify }}
</td>
<td>
Not supported
</td>
</tr>
</table>

## Method changes:

<table>
<tr>
<thead>
<th>
{{'**Missing methods**'| markdownify }}
</th>
<th>
{{'**Alternate methods in .NET Core**'| markdownify }}
</th>
</thead>
</tr>
<tr>
<td>
{{'[Presentation.Open(String)](https://help.syncfusion.com/cr/file-formats/Syncfusion.Presentation.Presentation.html#Syncfusion_Presentation_Presentation_Open_System_String_"")'| markdownify }}
</td>
<td>
You can open the document as stream from the file system using {{'[Presentation.Open(Stream)](https://help.syncfusion.com/cr/file-formats/Syncfusion.Presentation.Presentation.html#Syncfusion_Presentation_Presentation_Open_System_IO_Stream"")'| markdownify }} API.
</td>
</tr>
<tr>
<td>
{{'[Presentation.Save(String)](https://help.syncfusion.com/cr/file-formats/Syncfusion.Presentation.Presentation.html#Syncfusion_Presentation_Presentation_Save_System_String_"")'| markdownify }}
</td>
<td>
You can save the document as stream to the file system using {{'[Presentation.Save(Stream)](https://help.syncfusion.com/cr/file-formats/Syncfusion.Presentation.Presentation.html#Syncfusion_Presentation_Presentation_Save_System_IO_Stream_"")'| markdownify }} API.
</td>
</tr>
<tr>
<td>
{{'[Presentation.Save(string fileName, FormatType formatType, HttpResponse response)](https://help.syncfusion.com/cr/file-formats/Syncfusion.Presentation.IPresentation.html#Syncfusion_Presentation_IPresentation_Save_System_String_Syncfusion_Presentation_FormatType_System_Web_HttpResponse_"")'| markdownify }}
</td>
<td>
You can save the document as stream and then download from browser.
</td>
</tr>
<tr>
<td>
{{'[IPresentationChart.SaveAsImage(Stream imageAsStream)](https://help.syncfusion.com/cr/file-formats/Syncfusion.Presentation.IPresentationChart.html#Syncfusion_Presentation_IPresentationChart_SaveAsImage_System_IO_Stream_"")'| markdownify }}
</td>
<td>
IPresentationRenderer.ConvertToImage(IPresentationChart chart, Stream outputStream)
</td>
</tr>
</table>

## Advantages
Supports Windows, macOS, Linux, docker, Azure, and AWS environments.

## Known limitations
EMF and WMF images are not supported in .NET Core platform.

## Notable changes
* Graphics library: In .NET Framework, our library makes use of System.Drawing.Common for any text measuring and graphics-related operations. Whereas in .NET Core, our library uses the SkiaSharp graphics library to provide the same type of graphics.
* The below features are make use of SkiaSharp graphics library, which are separated into a separate package, [Syncfusion.PresentationRenderer.Net.Core](https://www.nuget.org/packages/Syncfusion.PresentationRenderer.Net.Core)
	* [PowerPoint Presentation to PDF](https://help.syncfusion.com/file-formats/presentation/presentation-to-pdf)
	* [PowerPoint Presentation to Image](https://help.syncfusion.com/file-formats/presentation/presentation-to-image)
* During PowerPoint Presentation to PDF/Image conversion, if you are facing font-related problems (like accessing font from the environment), you can pass the fonts as streams using our [font substitution approach](https://help.syncfusion.com/file-formats/presentation/presentation-to-pdf#font-substitution-for-unavailable-fonts).

N> If you want to migrate without any code changes from [Syncfusion.Presentation.ASP.NET](https://www.nuget.org/packages/Syncfusion.Presentation.AspNet.Mvc4) NuGet in application targeting .NET Framework, you can consider to use anyone of the packages
N> * [Syncfusion.Presentation.WinForms](https://www.nuget.org/packages/Syncfusion.Presentation.WinForms)
N> * [Syncfusion.Presentation.Wpf](https://www.nuget.org/packages/Syncfusion.Presentation.Wpf)
N> * [Syncfusion.Presentation.AspNet.Mcv4](https://www.nuget.org/packages/Syncfusion.Presentation.AspNet.Mvc4)
N>*But, this is not a recommended approach.*
