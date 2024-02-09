---
title: Avoid exception when using Excel97 to 2003 with large number of row column index.
description: This page helps to avoid exception when using Excel97 to 2003 with large number of row column index in Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# How to avoid exception when using Excel97 to 2003 with large number of rows column index?

By default, when creating a new workbook, it is set to Excel97to2003 version which supports only 65536 rows and 256 columns. When the row and column index exceeds this limit, an ArgumentOutOfRange exception is thrown. To fix this, the DefaultVersion needs to be set as Xlsx. This version supports 1048576 rows and 16384 columns.

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