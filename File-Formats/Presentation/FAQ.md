---
title: Frequently Asked Questions for PowerPoint Presentations | Syncfusion
description: This section illustrates about frequently asked questions in various options by using Essential Syncfusion Presentation library.
platform: file-formats
control: Presentation
documentation: UG
---
# FAQ’s for PowerPoint Presentations

The frequently asked questions in Essential PowerPoint Presentations are listed below.

## Why I get an exception when trying to load a PPT file?

The current version of Presentation library supports only .PPTX format - Microsoft Office 2007 and later version.

## Is it possible to print the Presentation slides?

Yes, you can print the PowerPoint presentations by using its ability to convert the slides as images and by using the [PrintDocument](https://learn.microsoft.com/en-us/dotnet/api/system.drawing.printing.printdocument?redirectedfrom=MSDN&view=dotnet-plat-ext-7.0# "") class. For more details, refer to [Printing](http://www.google.com/# "")

## Does adding audio and video to a Presentation is supported?

At present, there is no support to add audio and video to Presentation by using Essential Presentation library.

## What measure does Essential Presentation use to add slide elements such as textbox, shape, picture and charts?

We use Points to add any slide elements in a Presentation.

## Does Essential Presentation supports cloning a slide in the Presentation?

Yes, Essential Presentation library supports cloning as follows:

   * Slide in the Presentation can be cloned from one Presentation to another or within a same Presentation.
   * An entire Presentation can also be cloned as an independent copy of the original.

## Could not find Syncfusion.OfficeChartToImageConverter assembly in .NET 3.5 Framework, does it mean there is no support for chart conversion in this framework?

Yes, OfficeChartToImageConverter assembly is not supported in .NET 3.5 Framework and it is available from .NET 4.0 Framework.

## Can chart data be refreshed?

Yes, Essential Presentation supports refreshing the chart data. For more details, refer to [Working with charts](/file-formats/presentation/working-with-charts)

## Is it possible to convert 3D charts to PDF or image?

Current version of the Essential Presentation library does not provide support for converting 3D charts to PDF or image format.

## How to improve the image quality while converting the Presentation slides to image?

You can improve the quality of converted images by specifying the image resolution. Refer – [Converting PowerPoint presentation to Images](/file-formats/presentation/getting-started#converting-powerpoint-presentation-to-images)

## Why metafile (*.wmf, *.emf) and TIFF images are not preserved in PPTX to PDF/Image conversion?

In .NET Core or .NET targeting applications, metafile (*.wmf, *.emf) and TIFF images have some limitations in PresentationRenderer. Internally, PresentationRenderer use SkiaSharp graphics library to layout the text and images in PDF/Image conversion. And SkiaSharp library doesn’t support the metafile (*.emf, *.wmf) and TIFF images, so, it doesn’t preserve the images in the mentioned applications.

If the PowerPoint contains metafile (*.wmf or *.emf) and TIFF images, internally, Presentation doesn't preserve these during PPTX to PDF or image conversions to avoid pagination problems.

To preserve the expected images in the PDF/Image conversion, we suggest you convert the metafile and Tiff image formats to bitmap image format (JPEG or PNG) and then perform PPTX to PDF/Image conversion.

**Suggestion**

You can use the [WPF](https://www.nuget.org/packages/Syncfusion.PresentationToPdfConverter.Wpf/) or [Windows Forms](https://www.nuget.org/packages/Syncfusion.PresentationToPdfConverter.WinForms/) platform NuGet packages for .NET Core 3.0 or later versions targeting applications from v17.3.0.x and use the same [C# tab](https://help.syncfusion.com/file-formats/presentation/presentation-to-pdf) code examples for it. But in Mac and Linux environment, using the [WPF](https://www.nuget.org/packages/Syncfusion.PresentationToPdfConverter.Wpf/) or [Windows Forms](https://www.nuget.org/packages/Syncfusion.PresentationToPdfConverter.WinForms/) platform NuGet packages have limitations.

## What are the NuGet packages to be installed to perform PowerPoint Presentation to PDF conversion in Linux OS?

In Linux OS, perform PowerPoint presentation to PDF conversion using the .NET Core (Targeting .netcoreapp) application. Refer to [PowerPoint presentation to PDF conversion NuGet packages](https://help.syncfusion.com/file-formats/presentation/nuget-packages-required#converting-powerpoint-presentation-into-pdf) to know about the packages required to deploy the .NET Core (Targeting .netcoreapp) applications with PowerPoint presentation to PDF conversion capabilities.

In addition to the previous NuGet packages, your application needs to install the following NuGet packages.

<table>
<thead>
<tr>
<th width="20%">
Version
</th>
<th width="40%">
NuGet packages to install
</th>
</tr>
</thead>
<tr>
<td>
From v23.1.40
</td>
<td>
{{'[SkiaSharp.NativeAssets.Linux v2.88.6](https://www.nuget.org/packages/SkiaSharp.NativeAssets.Linux/2.88.6)'| markdownify }}<br/>
{{'[HarfBuzzSharp.NativeAssets.Linux v7.3.0](https://www.nuget.org/packages/HarfBuzzSharp.NativeAssets.Linux/7.3.0)'| markdownify }}
</td>
</tr>
<tr>
<td>
From v20.3.0.56 
</td>
<td>
{{'[SkiaSharp.NativeAssets.Linux v2.88.2](https://www.nuget.org/packages/SkiaSharp.NativeAssets.Linux/2.88.2)'| markdownify }}<br/>
{{'[HarfBuzzSharp.NativeAssets.Linux v2.8.2.2](https://www.nuget.org/packages/HarfBuzzSharp.NativeAssets.Linux/2.8.2.2)'| markdownify }}
</td>
</tr>
<tr>
<td>
From v20.1.0.x 
</td>
<td>
{{'[SkiaSharp.NativeAssets.Linux v2.88.0-preview.209](https://www.nuget.org/packages/SkiaSharp.NativeAssets.Linux/2.88.0-preview.209)'| markdownify }}<br/>
{{'[HarfBuzzSharp.NativeAssets.Linux v2.8.2-preview.209](https://www.nuget.org/packages/HarfBuzzSharp.NativeAssets.Linux/2.8.2-preview.209)'| markdownify }}
</td>
</tr>
<tr>
<td>
From v19.4.0.x
</td>
<td>
{{'[SkiaSharp.NativeAssets.Linux v2.80.2 NuGet](https://www.nuget.org/packages/SkiaSharp.NativeAssets.Linux/2.80.2)'| markdownify }}<br/>
{{'[HarfBuzzSharp.NativeAssets.Linux v2.6.1.7 NuGet](https://www.nuget.org/packages/HarfBuzzSharp.NativeAssets.Linux/2.6.1.7)'| markdownify }}
</td>
</tr>
<tr>
<td>
From v18.4.0.x to 19.4.0.x
</td>
<td>
{{'[SkiaSharp.NativeAssets.Linux v2.80.2 NuGet](https://www.nuget.org/packages/SkiaSharp.NativeAssets.Linux/2.80.2)'| markdownify }}<br/>
</td>
</tr>
<tr>
<td>
Before v18.4.0.x
</td>
<td>
Install the SkiaSharp.Linux NuGet package for the .NET Core application in Linux OS. Find the SkiaSharp.Linux NuGet package created by us from {{'[here](https://www.syncfusion.com/downloads/support/directtrac/general/ze/SkiaSharp.Linux.1.59.3-2103435070)'| markdownify }}.<br/>
</td>
</tr>
</table>
