---
title: ASP.NET
description: Briefs about download and open an Excel document in browser after saving the document in ASP.NET platform.
platform: file-formats
control: XlsIO
documentation: UG
---
# ASP.NET

In order to use XlsIO in your ASP.NET application, please add the required assemblies in your ASP.NET application. Refer [Assemblies Required](/File-Formats/XlsIO/Assemblies-Required).

## Saving the document

The following code snippet illustrates how to download an Excel document in browser after saving the document.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

IWorkbook workbook = application.Workbooks.Create(1);

workbook.Version = ExcelVersion.Excel2010;

workbook.SaveAs("Output.xlsx", ExcelSaveType.SaveAsXLS, Response, ExcelDownloadType.PromptDialog);

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

Dim workbook As IWorkbook = application.Workbooks.Create(1)

workbook.Version = ExcelVersion.Excel2010

workbook.SaveAs("Output.xlsx", ExcelSaveType.SaveAsXLS, Response, ExcelDownloadType.PromptDialog)

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %} 

The following code snippet illustrates how to open the excel document in web browser after saving the document.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

IWorkbook workbook = application.Workbooks.Create(1);

workbook.Version = ExcelVersion.Excel2010;

workbook.SaveAs("Output.xlsx", ExcelSaveType.SaveAsXLS, Response, ExcelDownloadType.Open);

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

Dim workbook As IWorkbook = application.Workbooks.Create(1)

workbook.Version = ExcelVersion.Excel2010

workbook.SaveAs("Output.xlsx", ExcelSaveType.SaveAsXLS, Response, ExcelDownloadType.Open)

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %} 

