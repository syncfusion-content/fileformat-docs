---
title: NuGet Packages Required
description: NuGet Packages required to use DocIO
platform: file-formats
control: DocIO
documentation: UG
---

# Installing Syncfusion DocIO through NuGet Packages 

NuGet is the one of the easiest way to download and install DocIO library to work with Word documents. The following NuGet packages need to be installed in your application.
<table>
<thead>
<tr>
<th>
Platform(s)
</th>
<th>
Package name
</th>
<th>
Package manager console command
</th>
</tr>
</thead>
<tr>
<td>
.NET Frameworks (Windows Forms, WPF, ASP.NET and ASP.NET MVC)
</td>
<td>
Syncfusion.DocIO.Base.nupkg
</td>
<td>
Install-Package Syncfusion.DocIO.Base -Source http://nuget.syncfusion.com/nuget_windows-forms/nuget/getsyncfusionpackages/windows-forms
</td>
</tr>
<tr>
<td>
ASP.NET and ASP.NET MVC
</td>
<td>
Syncfusion.Web.FileFormatsBase.nupkg
</td>
<td>
Install-Package Syncfusion.Web.FileFormatsBase -Source http://nuget.syncfusion.com/nuget_aspnet/nuget/getsyncfusionpackages/aspnet
</td>
</tr>
<tr>
<td>
ASP.NET Core
</td>
<td>
Syncfusion.DocIO.NETStandard.nupkg
</td>
<td>
Install-Package Syncfusion.DocIO.NETStandard -Source http://nuget.syncfusion.com/nuget_aspnetcore/nuget/getsyncfusionpackages/aspnetcore
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
Install-Package Syncfusion.Xamarin.DocIO -Source http://nuget.syncfusion.com/nuget_xamarin/nuget/getsyncfusionpackages/xamarin
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
Install-Package Syncfusion.DocIO.UWP -Source http://nuget.syncfusion.com/nuget_universalwindows/nuget/getsyncfusionpackages/universalwindows
</td>
</tr>
</table>

## Converting Word document to PDF

For converting Word document into PDF, the following NuGet packages need to be installed in your application.

<table>
<thead>
<tr>
<th>
Platform(s)
</th>
<th>
Package name
</th>
<th>
Package manager console command
</th>
</tr>
</thead>
<tr>
<td>
.NET Frameworks (Windows Forms, WPF, ASP.NET and ASP.NET MVC)
</td>
<td>
Syncfusion.DocToPdfConverter.Base.nupkg
</td>
<td>
Install-Package Syncfusion.DocToPdfConverter.Base -Source http://nuget.syncfusion.com/nuget_windows-forms/nuget/getsyncfusionpackages/windows-forms
</td>
</tr>
<tr>
<td>
ASP.NET
</td>
<td>
Syncfusion.AspNet.FileFormats.nupkg
</td>
<td>
Install-Package Syncfusion.AspNet.FileFormats -Source http://nuget.syncfusion.com/nuget_aspnet/nuget/getsyncfusionpackages/aspnet
</td>
</tr>
<tr>
<td>
ASP.NET MVC
</td>
<td>
Syncfusion.AspNet.Mvc.FileFormats.nupkg
</td>
<td>
Install-Package Syncfusion.AspNet.Mvc.FileFormats -Source http://nuget.syncfusion.com/nuget_aspnetmvc/nuget/getsyncfusionpackages/aspnetmvc
</td>
</tr>
<tr>
<td>
ASP.NET Core 
</td>
<td>
Syncfusion.DocIORenderer.NetStandard.nupkg
</td>
<td>
Install-Package Syncfusion.DocIORenderer.NetStandard -Source http://nuget.syncfusion.com/nuget_aspnetcore/nuget/getsyncfusionpackages/aspnetcore
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
Install-Package Syncfusion.Xamarin.DocIORenderer -Source http://nuget.syncfusion.com/nuget_xamarin/nuget/getsyncfusionpackages/xamarin
</td>
</tr>
</table>

N> Word to PDF conversion is not supported in Universal Windows Platform.


## Converting Charts in DocIO

The below NuGet package need to be installed additionally to convert the charts present in Word documents.

<table>
<thead>
<tr>
<th>
Platform(s)
</th>
<th>
Package name
</th>
<th>
Package manager console command
</th>
</tr>
</thead>
<tr>
<td>
.NET Frameworks (Windows Forms, WPF, ASP.NET and ASP.NET MVC)
</td>
<td>
Syncfusion.OfficeChartToImageConverter.WPF.nupkg
</td>
<td>
Install-Package Syncfusion.OfficeChartToImageConverter.Base -Source http://nuget.syncfusion.com/nuget_windows-forms/nuget/getsyncfusionpackages/windows-forms
</td>
</tr>
</table>

N> 1. The “Syncfusion. OfficeChartToImageConverter.WPF.nupkg” NuGet package is only supported from 4.0 .NET Framework onwards and also it not supported in the Universal Windows platforms.
N> 2. The “Syncfusion.AspNet.FileFormats.nupkg” and “Syncfusion.AspNet.Mvc.FileFormats.nupkg” packages already includes the necessary assemblies for chart conversion. So it is not necessary to install the “Syncfusion.OfficeChartToImageConverter.Wpf.nupkg” NuGet package additionally in ASP.NET and ASP.NET MVC platforms.


## NuGet Package Installation and Uninstallation

To use Syncfusion NuGet packages in your project, please refer the NuGet Package [Installation](https://help.syncfusion.com/extension/syncfusion-nuget-packages/nuget-install-and-configuration#) and [Uninstallation](https://help.syncfusion.com/extension/syncfusion-nuget-packages/nuget-uninstallation-process#) sections.

DocIO NuGet packages can be installed and uninstalled using Package Manager Console. In Visual Studio, select Tools > NuGet Package Manager > Package Manager Console and execute the below commands in respective platforms.

### Platforms: .NET Frameworks (Windows Forms, WPF, ASP.NET and ASP.NET MVC)

**NuGet Package Name:** Syncfusion.DocIO.Base

Commands:

~~~
// Install package
Install-Package Syncfusion.DocIO.Base -Source http://nuget.syncfusion.com/nuget_windows-forms/nuget/getsyncfusionpackages/windows-forms 
~~~
~~~
// Un Install package
Uninstall-Package Syncfusion.DocIO.Base -RemoveDependencies 
~~~

**NuGet Package Name:** Syncfusion.DocToPdfConverter.Base

Commands:

~~~
// Install package
Install-Package Syncfusion.DocToPdfConverter.Base -Source http://nuget.syncfusion.com/nuget_windows-forms/nuget/getsyncfusionpackages/windows-forms 
~~~
~~~
// Un Install package
Uninstall-Package Syncfusion.DocToPdfConverter.Base -RemoveDependencies 
~~~

**NuGet Package Name:** Syncfusion.OfficeChartToImageConverter.WPF

Commands:

~~~
// Install package
Install-Package Syncfusion.OfficeChartToImageConverter.WPF -Source http://nuget.syncfusion.com/nuget_windows-forms/nuget/getsyncfusionpackages/windows-forms 
~~~
~~~
// Un Install package
Uninstall-Package Syncfusion.OfficeChartToImageConverter.WPF -RemoveDependencies 
~~~

### Platform: ASP.NET

**NuGet Package Name:** Syncfusion.Web.FileFormatsBase

Commands:

~~~
// Install package
Install-Package Syncfusion.Web.FileFormatsBase -Source http://nuget.syncfusion.com/nuget_aspnet/nuget/getsyncfusionpackages/aspnet 
~~~
~~~
// Un Install package
Uninstall-Package Syncfusion.Web.FileFormatsBase -RemoveDependencies 
~~~

**NuGet Package Name:** Syncfusion.AspNet.FileFormats

Commands:

~~~
// Install package
Install-Package Syncfusion.AspNet.FileFormats -Source http://nuget.syncfusion.com/nuget_aspnet/nuget/getsyncfusionpackages/aspnet
~~~
~~~
// Un Install package
Uninstall-Package Syncfusion.AspNet.FileFormats -RemoveDependencies 
~~~

### Platform: ASP.NET MVC

**NuGet Package Name:** Syncfusion.Web.FileFormatsBase

Commands:

~~~
// Install package
Install-Package Syncfusion.Web.FileFormatsBase -Source http://nuget.syncfusion.com/nuget_aspnetmvc/nuget/getsyncfusionpackages/aspnetmvc
~~~
~~~
// Un Install package
Uninstall-Package Syncfusion.Web.FileFormatsBase -RemoveDependencies 
~~~

**NuGet Package Name:** Syncfusion.AspNet.Mvc.FileFormats

Commands:

~~~
// Install package
Install-Package Syncfusion.AspNet.Mvc5.FileFormats -Source http://nuget.syncfusion.com/nuget_aspnetmvc/nuget/getsyncfusionpackages/aspnetmvc
~~~
~~~
// Un Install package
Uninstall-Package Syncfusion.AspNet.Mvc5.FileFormats -RemoveDependencies 
~~~

N> The number at the end of MVC denotes ASP.MVC version.

### Platform: ASP.NET Core

**NuGet Package Name:** Syncfusion.DocIO.NETStandard

Commands:

~~~
// Install package
Install-Package Syncfusion.DocIO.NETStandard -Source http://nuget.syncfusion.com/nuget_aspnetcore/nuget/getsyncfusionpackages/aspnetcore 
~~~
~~~
// Un Install package
Uninstall-Package Syncfusion.DocIO.NETStandard -RemoveDependencies 
~~~

**NuGet Package Name:** Syncfusion.DocIORenderer.NetStandard

Commands:

~~~
// Install package
Install-Package Syncfusion.DocIORenderer.NetStandard -Source http://nuget.syncfusion.com/nuget_aspnetcore/nuget/getsyncfusionpackages/aspnetcore 
~~~
~~~
// Un Install package
Uninstall-Package Syncfusion.DocIORenderer.NetStandard -RemoveDependencies 
~~~

### Platform: Xamarin

**NuGet Package Name:** Syncfusion.Xamarin.DocIO

Commands:

~~~
// Install package
Install-Package Syncfusion.Xamarin.DocIO -Source http://nuget.syncfusion.com/nuget_xamarin/nuget/getsyncfusionpackages/xamarin 
~~~
~~~
// Un Install package
Uninstall-Package Syncfusion.Xamarin.DocIO -RemoveDependencies 
~~~

**NuGet Package Name:** Syncfusion.Xamarin.DocIORenderer

Commands:

~~~
// Install package
Install-Package Syncfusion.Xamarin.DocIORenderer -Source http://nuget.syncfusion.com/nuget_xamarin/nuget/getsyncfusionpackages/xamarin 
~~~
~~~
// Un Install package
Uninstall-Package Syncfusion.Xamarin.DocIORenderer -RemoveDependencies 
~~~


### Platform: UWP

**NuGet Package Name:**  Syncfusion.DocIO.UWP

Commands:

~~~
// Install package
Install-Package Syncfusion.DocIO.UWP -Source http://nuget.syncfusion.com/nuget_universalwindows/nuget/getsyncfusionpackages/universalwindows 
~~~

~~~
// Un Install package
Uninstall-Package Syncfusion.DocIO.UWP -RemoveDependencies 
~~~

