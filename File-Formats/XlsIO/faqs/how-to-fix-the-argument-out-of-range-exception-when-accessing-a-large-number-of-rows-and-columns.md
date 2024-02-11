---
title: Fix the ArgumentOutOfRangeException when accessing a large number of rows and columns.
description: This page helps how to fix the ArgumentOutOfRangeException when accessing a large number of rows and columns in Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# How to fix the ArgumentOutOfRangeException when accessing a large number of rows and columns?

By default, when creating a new workbook, it is set to Excel97to2003 version which supports only 65536 rows and 256 columns. When the row and column index exceeds this limit, an ArgumentOutOfRange exception is thrown. To fix this, the [DefaultVersion](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IApplication.html#Syncfusion_XlsIO_IApplication_DefaultVersion) needs to be set as [Xlsx](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelVersion.html). This version supports 1048576 rows and 16384 columns.

The following code snippet shows how to set the default version of IApplication to Xlsx.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
IApplication application = excelEngine.Excel;
application.DefaultVersion = ExcelVersion.Xlsx;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
IApplication application = excelEngine.Excel;
application.DefaultVersion = ExcelVersion.Xlsx;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
IApplication application = excelEngine.Excel
application.DefaultVersion = ExcelVersion.Xlsx
{% endhighlight %}
{% endtabs %}  