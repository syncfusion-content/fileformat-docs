---
title: NuGet Packages Required | Syncfusion
description: This section illustrates the NuGet packages required to use Syncfusion Word library (Essential DocIO) in various platforms and frameworks
platform: file-formats
control: DocIO
documentation: UG
---

# NuGet Packages Required

## Installing Syncfusion DocIO through NuGet Packages 

NuGet is the one of the easiest way to download and install DocIO library to read, write and edit the Word documents. The following NuGet packages need to be installed in your application.
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
Windows Forms, Console Application (Targeting .NET Framework)
</td>
<td>
Syncfusion.DocIO.WinForms.nupkg
</td>
<td>
Install-Package Syncfusion.DocIO.WinForms
</td>
</tr>
<tr>
<td>
WPF
</td>
<td>
Syncfusion.DocIO.Wpf.nupkg
</td>
<td>
Install-Package Syncfusion.DocIO.Wpf
</td>
</tr>
<tr>
<td>
.NET Framework 3.5 or 4.0 Client Profile
</td>
<td>
Syncfusion.DocIO.ClientProfile.nupkg
</td>
<td>
Install-Package Syncfusion.DocIO.ClientProfile
</td>
</tr>
<tr>
<td>
ASP.NET
</td>
<td>
Syncfusion.DocIO.AspNet.nupkg
</td>
<td>
Install-Package Syncfusion.DocIO.AspNet
</td>
</tr>
<tr>
<td>
ASP.NET MVC4
</td>
<td>
Syncfusion.DocIO.AspNet.Mvc4.nupkg
</td>
<td>
Install-Package Syncfusion.DocIO.AspNet.Mvc4
</td>
</tr>
<tr>
<td>
ASP.NET MVC5
</td>
<td>
Syncfusion.DocIO.AspNet.Mvc5.nupkg
</td>
<td>
Install-Package Syncfusion.DocIO.AspNet.Mvc5
</td>
</tr>
<tr>
<td>
ASP.NET Core, Console Application (Targeting .NET Core) and Blazor
</td>
<td>
Syncfusion.DocIO.Net.Core.nupkg
</td>
<td>
Install-Package Syncfusion.DocIO.Net.Core
</td>
</tr>
<tr>
<td>
Xamarin
</td>
<td>
Syncfusion.Xamarin.DocIO.nupkg
</td>
<td>
Install-Package Syncfusion.Xamarin.DocIO
</td>
</tr>
<tr>
<td>
UWP
</td>
<td>
Syncfusion.DocIO.UWP.nupkg
</td>
<td>
Install-Package Syncfusion.DocIO.UWP
</td>
</tr>
</table>
N> 1. Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/license-key) to know about registering Syncfusion license key in your application to use our components.
N> 2. Syncfusion components are available in [nuget.org](https://www.nuget.org/)
N> 3. Starting with v17.3.0.x, Syncfusion provides support to .NET Core 3.0. You can use the above WPF or Windows Forms platform NuGet packages for .NET Core 3.0 targeting applications and use the same "C# tab" code examples for it.

## Converting Word document to PDF

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
Windows Forms, Console Application (Targeting .NET Framework)
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
WPF
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
ASP.NET 
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
ASP.NET MVC4
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
ASP.NET MVC5
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
ASP.NET Core, Console Application (Targeting .NET Core) and Blazor
</td>
<td>
Syncfusion.DocIORenderer.Net.Core.nupkg<br/>
<i>Note</i><br/>
<i>From v18.4.0.x:</i><br/>
Install [SkiaSharp.NativeAssets.Linux v2.80.2 NuGet](https://www.nuget.org/packages/SkiaSharp.NativeAssets.Linux/2.80.2) package for .Net Core application in Linux OS.<br/>
<i>Before v18.4.0.x</i><br/>
Install SkiaSharp.Linux NuGet package for .Net Core application in Linux OS. you can find the SkiaSharp.Linux NuGet package created by us from [here](http://www.syncfusion.com/downloads/support/directtrac/general/ze/SkiaSharp.Linux.1.59.3-2103435070#).
</td>
<td>
Install-Package Syncfusion.DocIORenderer.Net.Core
</td>
</tr>
<tr>
<td>
Xamarin
</td>
<td>
Syncfusion.Xamarin.DocIORenderer.nupkg
</td>
<td>
Install-Package Syncfusion.Xamarin.DocIORenderer
</td>
</tr>
</table>

N> 1. Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/license-key) to know about registering Syncfusion license key in your application to use our components.
N> 2. Syncfusion components are available in [nuget.org](https://www.nuget.org/)
N> 3. Please refer the procedure to deploy your .NET Core application in Linux OS from [here](https://www.syncfusion.com/kb/8470/how-to-deploy-net-core-application-with-word-to-pdf-conversion-capabilities-in-linux-os).
N> 4. From v18.4.0.x, the dependent package SkiaSharp is upgraded from 1.59.3 to 2.80.2 version and it is mandatory to use SkiaSharp.NativeAssets.Linux v2.80.2 package instead of SkiaSharp.Linux v1.59.3 for converting Word documents into PDF in Linux environment.

## Converting Charts

The following NuGet package need to be installed additionally to preserve chart as image in Word to PDF, and Image conversions.

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
Windows Forms, Console Application (Targeting .NET Framework)
</td>
<td>
Syncfusion.OfficeChartToImageConverter.WinForms.nupkg
</td>
<td>
Install-Package Syncfusion.OfficeChartToImageConverter.WinForms
</td>
</tr>
<tr>
<td>
WPF
</td>
<td>
Syncfusion.OfficeChartToImageConverter.Wpf.nupkg
</td>
<td>
Install-Package Syncfusion.OfficeChartToImageConverter.Wpf
</td>
</tr>
<tr>
<td>
ASP.NET 
</td>
<td>
Syncfusion.OfficeChartToImageConverter.AspNet.nupkg
</td>
<td>
Install-Package Syncfusion.OfficeChartToImageConverter.AspNet
</td>
</tr>
<tr>
<td>
ASP.NET MVC4
</td>
<td>
Syncfusion.OfficeChartToImageConverter.AspNet.Mvc4.nupkg
</td>
<td>
Install-Package Syncfusion.OfficeChartToImageConverter.AspNet.Mvc4
</td>
</tr>
<tr>
<td>
ASP.NET MVC5
</td>
<td>
Syncfusion.OfficeChartToImageConverter.AspNet.Mvc5.nupkg
</td>
<td>
Install-Package Syncfusion.OfficeChartToImageConverter.AspNet.Mvc5
</td>
</tr>
</table>

N> 1. Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/license-key) to know about registering Syncfusion license key in your application to use our components.
N> 2. Syncfusion components are available in [nuget.org](https://www.nuget.org/)
N> 3. The "Syncfusion.OfficeChartToImageConverter.WPF.nupkg" NuGet package is only supported from 4.0 .NET Framework onwards and it is not supported in ASP.NET Core, Blazor and Xamarin platforms.


## NuGet Package Installation and Uninstallation

To use Syncfusion NuGet packages in your project, please refer the NuGet Package [Installation](https://help.syncfusion.com/extension/syncfusion-nuget-packages/nuget-install-and-configuration#) and [Uninstallation](https://help.syncfusion.com/extension/syncfusion-nuget-packages/nuget-uninstallation-process#) sections.

DocIO NuGet packages can be installed and uninstalled using Package Manager Console. In Visual Studio, select Tools > NuGet Package Manager > Package Manager Console and execute the following commands.

### Windows Forms

**NuGet Package:** Syncfusion.DocIO.WinForms

The package contains DocIO library that allows you to create, read and edit Word documents.

~~~
// Install package
Install-Package Syncfusion.DocIO.WinForms
~~~
~~~
// Uninstall package
Uninstall-Package Syncfusion.DocIO.WinForms -RemoveDependencies 
~~~

**NuGet Package:** Syncfusion.DocToPdfConverter.WinForms

The package contains the DocToPdfConverter .NET library that allows you to convert the Word documents to PDF.

~~~
// Install package
Install-Package Syncfusion.DocToPdfConverter.WinForms
~~~
~~~
// Uninstall package
Uninstall-Package Syncfusion.DocToPdfConverter.WinForms -RemoveDependencies 
~~~

**NuGet Package:** Syncfusion.OfficeChartToImageConverter.WinForms

The package contains OfficeChartToImageConverter .NET library for converting the chart present in word document to image.

~~~
// Install package
Install-Package Syncfusion.OfficeChartToImageConverter.WinForms
~~~
~~~
// Uninstall package
Uninstall-Package Syncfusion.OfficeChartToImageConverter.WinForms -RemoveDependencies 
~~~

### WPF

**NuGet Package:** Syncfusion.DocIO.Wpf

The package contains DocIO library that allows you to create, read and edit Word documents.

~~~
// Install package
Install-Package Syncfusion.DocIO.Wpf
~~~
~~~
// Uninstall package
Uninstall-Package Syncfusion.DocIO.Wpf -RemoveDependencies 
~~~

**NuGet Package:** Syncfusion.DocToPdfConverter.Wpf

The package contains the DocToPdfConverter .NET library that allows you to convert the Word documents to PDF.

~~~
// Install package
Install-Package Syncfusion.DocToPdfConverter.Wpf
~~~
~~~
// Uninstall package
Uninstall-Package Syncfusion.DocToPdfConverter.Wpf -RemoveDependencies 
~~~

**NuGet Package:** Syncfusion.OfficeChartToImageConverter.Wpf

The package contains OfficeChartToImageConverter .NET library for converting the chart present in word document to image.

~~~
// Install package
Install-Package Syncfusion.OfficeChartToImageConverter.Wpf
~~~
~~~
// Uninstall package
Uninstall-Package Syncfusion.OfficeChartToImageConverter.Wpf -RemoveDependencies 
~~~

### ASP.NET 

**NuGet Package:** Syncfusion.DocIO.AspNet

The package contains DocIO library that allows you to create, read and edit Word documents.

~~~
// Install package
Install-Package Syncfusion.DocIO.AspNet
~~~
~~~
// Uninstall package
Uninstall-Package Syncfusion.DocIO.AspNet -RemoveDependencies 
~~~

**NuGet Package:** Syncfusion.DocToPdfConverter.AspNet

The package contains the DocToPdfConverter .NET library that allows you to convert the Word documents to PDF.

~~~
// Install package
Install-Package Syncfusion.DocToPdfConverter.AspNet
~~~
~~~
// Uninstall package
Uninstall-Package Syncfusion.DocToPdfConverter.AspNet -RemoveDependencies 
~~~

**NuGet Package:** Syncfusion.OfficeChartToImageConverter.AspNet

The package contains OfficeChartToImageConverter .NET library for converting the chart present in word document to image.

~~~
// Install package
Install-Package Syncfusion.OfficeChartToImageConverter.AspNet
~~~
~~~
// Uninstall package
Uninstall-Package Syncfusion.OfficeChartToImageConverter.AspNet -RemoveDependencies 
~~~

### ASP.NET MVC4

**NuGet Package:** Syncfusion.DocIO.AspNet.Mvc4

The package contains DocIO library that allows you to create, read and edit Word documents.

~~~
// Install package
Install-Package Syncfusion.DocIO.AspNet.Mvc4
~~~
~~~
// Uninstall package
Uninstall-Package Syncfusion.DocIO.AspNet.Mvc4 -RemoveDependencies 
~~~

**NuGet Package:** Syncfusion.DocToPdfConverter.AspNet.Mvc4

The package contains the DocToPdfConverter .NET library that allows you to convert the Word documents to PDF.

~~~
// Install package
Install-Package Syncfusion.DocToPdfConverter.AspNet.Mvc4
~~~
~~~
// Uninstall package
Uninstall-Package Syncfusion.DocToPdfConverter.AspNet.Mvc4 -RemoveDependencies 
~~~

**NuGet Package:** Syncfusion.OfficeChartToImageConverter.AspNet.Mvc4

The package contains OfficeChartToImageConverter .NET library for converting the chart present in word document to image.

~~~
// Install package
Install-Package Syncfusion.OfficeChartToImageConverter.AspNet.Mvc4
~~~
~~~
// Uninstall package
Uninstall-Package Syncfusion.OfficeChartToImageConverter.AspNet.Mvc4 -RemoveDependencies 
~~~

### ASP.NET MVC5

**NuGet Package:** Syncfusion.DocIO.AspNet.Mvc5

The package contains DocIO library that allows you to create, read and edit Word documents.

~~~
// Install package
Install-Package Syncfusion.DocIO.AspNet.Mvc5
~~~
~~~
// Uninstall package
Uninstall-Package Syncfusion.DocIO.AspNet.Mvc5 -RemoveDependencies 
~~~

**NuGet Package:** Syncfusion.DocToPdfConverter.AspNet.Mvc5

The package contains the DocToPdfConverter .NET library that allows you to convert the Word documents to PDF.

~~~
// Install package
Install-Package Syncfusion.DocToPdfConverter.AspNet.Mvc5
~~~
~~~
// Uninstall package
Uninstall-Package Syncfusion.DocToPdfConverter.AspNet.Mvc5 -RemoveDependencies 
~~~

**NuGet Package:** Syncfusion.OfficeChartToImageConverter.AspNet.Mvc5

The package contains OfficeChartToImageConverter .NET library for converting the chart present in word document to image.

~~~
// Install package
Install-Package Syncfusion.OfficeChartToImageConverter.AspNet.Mvc5
~~~
~~~
// Uninstall package
Uninstall-Package Syncfusion.OfficeChartToImageConverter.AspNet.Mvc5 -RemoveDependencies 
~~~

### ASP.NET Core and Blazor

**NuGet Package:** Syncfusion.DocIO.Net.Core

The package contains DocIO portable library that allows you to create, read and edit Word documents.

~~~
// Install package
Install-Package Syncfusion.DocIO.Net.Core
~~~
~~~
// Uninstall package
Uninstall-Package Syncfusion.DocIO.Net.Core -RemoveDependencies 
~~~

**NuGet Package:** Syncfusion.DocIORenderer.Net.Core

The package contains the DocIORenderer .NET portable library that allows you to convert the Word documents to PDF.

~~~
// Install package
Install-Package Syncfusion.DocIORenderer.Net.Core

~~~
~~~
// Uninstall package
Uninstall-Package Syncfusion.DocIORenderer.Net.Core -RemoveDependencies 
~~~

### Xamarin

**NuGet Package:** Syncfusion.Xamarin.DocIO

The package contains DocIO portable library that allows you to create, read and edit Word documents.

~~~
// Install package
Install-Package Syncfusion.Xamarin.DocIO
~~~
~~~
// Uninstall package
Uninstall-Package Syncfusion.Xamarin.DocIO -RemoveDependencies 
~~~

**NuGet Package:** Syncfusion.Xamarin.DocIORenderer

The package contains the DocIORenderer .NET portable library that allows you to convert the Word documents to PDF.

~~~
// Install package
Install-Package Syncfusion.Xamarin.DocIORenderer

~~~
~~~
// Uninstall package
Uninstall-Package Syncfusion.Xamarin.DocIORenderer -RemoveDependencies 
~~~

### UWP

**NuGet Package:**  Syncfusion.DocIO.UWP

The package contains DocIO library that allows you to create, read and edit Word documents.

~~~
// Install package
Install-Package Syncfusion.DocIO.UWP
~~~

~~~
// Uninstall package
Uninstall-Package Syncfusion.DocIO.UWP -RemoveDependencies 
~~~
