---
title: Resolve the File does not contain workbook stream error | Syncfusion
description: This page explains how to resolve the "File does not contain workbook stream" error in Syncfusion.XlsIO.Base.dll.
platform: file-formats
control: XlsIO
documentation: UG
---

# How to resolve the “File does not contain workbook stream” error?

XlsIO does not support files generated prior to 97-2003 version. Hence the exception "File does not contain workbook stream" occurs. This can be checked in prior with the below code snippet. 

{% tabs %}  

{% highlight c# tabtitle="C#" %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

//To check whether the file is supported

var isSupported = application.IsSupported("Sample.xls");

excelEngine.Dispose();

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

'To check whether the file is supported

Dim isSupported = application.IsSupported("Sample.xls")

excelEngine.Dispose()

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;

//To check whether the file is supported
FileStream stream = new FileStream("Sample.xls", FileMode.OpenOrCreate, FileAccess.ReadWrite);
var isSupported = application.IsSupported(stream);

excelEngine.Dispose();
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;

//To check whether the file is supported
FileStream stream = new FileStream("Sample.xls", FileMode.OpenOrCreate, FileAccess.ReadWrite);
var isSupported = application.IsSupported(stream);

excelEngine.Dispose();
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;

//To check whether the file is supported
FileStream stream = new FileStream("Sample.xls", FileMode.OpenOrCreate, FileAccess.ReadWrite);
var isSupported = application.IsSupported(stream);

excelEngine.Dispose();
{% endhighlight %}

{% endtabs %}  

N> This method is available from 12.4 version onwards.

## See Also

* [How to resolve Excel cannot open the file filename.xlsx... error?](how-to-resolve-excel-cannot-open-the-file-because-the-file-format-for-the-file-extension-is-not-valid)
* [What are the known exceptions of XlsIO?](https://help.syncfusion.com/file-formats/xlsio/known-exceptions)
* [How to open an Excel file from stream?](how-to-open-an-excel-file-from-stream)
* [How to save a file to stream?](how-to-save-a-file-to-stream)
