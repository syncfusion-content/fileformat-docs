---
title: Convert Word to PDF in C# | DocIO | Syncfusion
description: Learn how to convert a Word document to PDF using the .NET Word (DocIO) library without Microsoft Word or interop dependencies.
platform: file-formats
control: DocIO
documentation: UG
---

# Convert Word document to PDF in C#

The Word document files can be efficiently converted to PDF format using the .NET Word (DocIO) library. With just a few lines of code, you can seamlessly create a PDF document from scratch or convert an existing Word document. By leveraging the capabilities of Essential DocIO, the conversion process is executed flawlessly.

Syncfusion Word to PDF converter is highly versatile, ensuring seamless performance across a range of platforms, including [Azure Cloud](), [Amazon Web Service (AWS)](),[Google Cloud Platform (GCP)](), [ASP.NET Core](), [ASP.NET MVC](), [ASP.NET](), [Blazor](), [Xamarin](), [Windows Forms](), [WPF](), [UWP](), [WinUI](), [.NET MAUI](), [Linux](), [Mac](). It guarantees compatibility with Windows, Linux, and macOS, making it a reliable choice for diverse operating environments.

## Key features for Word Converter

* Customize the [embedding of TrueType fonts]() in two ways.
* Essential DocIO supports [PDF documents for accessibility (508 compliance)]().
* Restrict all permissions in a PDF document using [Pdf Permissions Flags]().
* [Preserve comments balloons]() in a generated PDF when converting Word documents with comments.
* [Preserve revision marks]() in a generated PDF when converting Word documents with tracked changes or revisions.
* [Hyphenate text]() in a Word document while converting it to PDF format.
* [Preserve the complex script text]() in the converted PDF document.
* Set the [Pdf Conformance Level]() while converting Word to PDF.
* [Reduce the Main Memory usage]() in Word to PDF conversion.
* Preserve [Word document form fields as PDF form fields]() in the converted PDF document.


##  Key features for Word Converter
* You can customize the [TrueType fonts embedding]() in two ways.
* Essential DocIO allows [PDF document for accessibility (508 compliance)]() support.
* You can [restrict all the permission in a PDF document]() using Pdf Permissions Flags.
* You can [preserve comments balloon]() in a generated PDF when converting Word documents with comments.
* You can [preserve revision marks]() in a generated PDF when converting Word documents with tracked changes or revisions.
* Essential DocIO allows [hyphenating text]() in a Word document while converting it to PDF format.
* You can [preserve the complex script text]() in the converted PDF document.
* You can set the [Pdf Conformance Level]() while converting Word to PDF.
* You can [reduces the Main Memory usage]() in Word to PDF conversion.
* You can preserve [Word document form field to PDF form field]() in the converted PDF document.

## NuGet packages to convert Word to PDF

For converting Word document into PDF, the following NuGet packages need to be installed in your application.

<table>
<thead>
<tr>
<th width="20%">
Platform(s)
</th>
<th width="40%">
Package name
</th>
<th width="40%">
Package manager console command
</th>
</tr>
</thead>
<tr>
<td>
{{'[Windows Forms](https://help.syncfusion.com/file-formats/docio/convert-word-document-to-pdf-in-window-forms)'|  markdownify }}, Console Application (Targeting .NET Framework)
</td>
<td>
Syncfusion.DocToPdfConverter.WinForms.nupkg
</td>
<td>
Install-Package Syncfusion.DocToPdfConverter.WinForms
</td>
</tr>
<tr>
<td>
{{'[WPF](https://help.syncfusion.com/file-formats/docio/convert-word-document-to-pdf-in-wpf)'|  markdownify }}
</td>
<td>
Syncfusion.DocToPdfConverter.Wpf.nupkg
</td>
<td>
Install-Package Syncfusion.DocToPdfConverter.Wpf
</td>
</tr>
<tr>
<td>
.NET Framework 3.5 or 4.0 Client Profile
</td>
<td>
Syncfusion.DocToPdfConverter.ClientProfile.nupkg
</td>
<td>
Install-Package Syncfusion.DocToPdfConverter.ClientProfile
</td>
</tr>
<tr>
<td>
{{'[ASP.NET](https://help.syncfusion.com/file-formats/docio/convert-word-document-to-pdf-in-asp-net)'|  markdownify }}
</td>
<td>
Syncfusion.DocToPdfConverter.AspNet.nupkg
</td>
<td>
Install-Package Syncfusion.DocToPdfConverter.AspNet
</td>
</tr>
<tr>
<td>
{{'[ASP.NET MVC4](https://help.syncfusion.com/file-formats/docio/convert-word-document-to-pdf-in-asp-net-mvc)'|  markdownify }}
</td>
<td>
Syncfusion.DocToPdfConverter.AspNet.Mvc4.nupkg
</td>
<td>
Install-Package Syncfusion.DocToPdfConverter.AspNet.Mvc4
</td>
</tr>
<tr>
<td>
{{'[ASP.NET MVC5](https://help.syncfusion.com/file-formats/docio/convert-word-document-to-pdf-in-asp-net-mvc)'|  markdownify }}
</td>
<td>
Syncfusion.DocToPdfConverter.AspNet.Mvc5.nupkg
</td>
<td>
Install-Package Syncfusion.DocToPdfConverter.AspNet.Mvc5
</td>
</tr>
<tr>
<td>
{{'[ASP.NET Core](https://help.syncfusion.com/file-formats/docio/convert-word-document-to-pdf-in-asp-net-core)'|  markdownify }}, Console Application (Targeting .NET Core) and {{'[Blazor](https://help.syncfusion.com/file-formats/docio/convert-word-document-to-pdf-in-blazor)'|  markdownify }}
</td>
<td>
Syncfusion.DocIORenderer.Net.Core.nupkg<br/>
<br/>
<i>Note:</i><br/>
<i>Please refer {{'[here](https://help.syncfusion.com/file-formats/docio/faq#what-are-the-nuget-packages-to-be-installed-to-perform-word-to-pdf-conversion-in-linux-os)'| markdownify }} to know about the NuGet packages that need to be installed to perform Word to PDF conversion in Linux OS.</i><br/>
</td>
<td>
Install-Package Syncfusion.DocIORenderer.Net.Core
</td>
</tr>
<tr>
<td>
{{'[Xamarin](https://help.syncfusion.com/file-formats/docio/convert-word-document-to-pdf-in-xamarin)'|  markdownify }}
</td>
<td>
Syncfusion.Xamarin.DocIORenderer.nupkg
</td>
<td>
Install-Package Syncfusion.Xamarin.DocIORenderer
</td>
</tr>
<tr>
<td>
{{'[Windows UI Library (WinUI)](https://help.syncfusion.com/file-formats/docio/convert-word-document-to-pdf-in-winui)'|  markdownify }}<br/> {{'[.NET Multi-platform App UI (.NET MAUI)](https://help.syncfusion.com/file-formats/docio/convert-word-document-to-pdf-in-maui)'|  markdownify }}
</td>
<td>
Syncfusion.DocIORenderer.NET
</td>
<td>
Install-Package Syncfusion.DocIORenderer.NET
</td>
</tr>
</table>

N> 1. Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.
N> 2. Syncfusion components are available in [nuget.org](https://www.nuget.org/)
N> 3. Please refer the procedure to deploy your .NET Core application in Linux OS from [here](https://support.syncfusion.com/kb/article/7626/how-to-deploy-net-core-application-with-word-to-pdf-conversion-capabilities-in-linux-os).
N> 4. From v20.3.0.56, the dependent package SkiaSharp is upgraded from 2.88.0-preview.209 to 2.88.2 version and it is mandatory to use SkiaSharp.NativeAssets.Linux v2.88.2 and HarfBuzzSharp.NativeAssets.Linux v2.8.2.2 packages for converting Word documents into PDF in Linux environment.