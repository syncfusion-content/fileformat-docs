---
title: Avoid ambiguous error during migration | XlsIO | Syncfusion
description: This section explains how to avoid ambiguous error while migrating Syncfusion .NET Excel (XlsIO) library from .NET Framework to .NET core.
platform: file-formats
control: XlsIO
documentation: UG
---

# Avoid ambiguous error in XlsIO while migrating from .NET Framework to .NET Core

While migrating from .NET Framework to .NET Core, XlsIO packages should also be changed. Please look into the below link for details.

[Migrate XlsIO library from .NET Framework to .NET Core?](https://help.syncfusion.com/file-formats/xlsio/faqs/migrate-from-net-framework-to-net-core)

After migration, there might be some cases in which both XlsIO.Base and XlsIO.Portable should be used. Here, an ambiguous error is thrown for having both XlsIO.Base and XlsIO.Portable in the same application. 

In this case, XlsIO.Base alone can be used by changing the target framework from **net6.0** to **net6.0-windows** in **.csproj** file.

{% tabs %}  
{% highlight CSHTML %}
<Project Sdk="Microsoft.NET.Sdk">
    <PropertyGroup>
        <TargetFramework>net6.0-windows</TargetFramework>
        <ImplicitUsings>enable</ImplicitUsings>
        <Nullable>enable</Nullable>
    </PropertyGroup>
</Project>
{% endhighlight %}
{% endtabs %}
