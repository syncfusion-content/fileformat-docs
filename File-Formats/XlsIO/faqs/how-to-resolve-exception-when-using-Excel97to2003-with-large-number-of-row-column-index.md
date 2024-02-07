---
title: Avoid exception when using Excel97 to 2003 with large number of row column index.
description: This page helps to avoid exception when using Excel97 to 2003 with large number of row column index in Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# How to avoid exception when using Excel97 to 2003 with large number of rows column index?

When creating a new workbook, it defaults to the Excel97to2003 version, which supports only 65,536 rows and 256 columns. If the row or column index exceeds this limit, an ArgumentException is thrown. To avoid this exception, we recommend setting the default version of the IApplication to Xlsx.

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