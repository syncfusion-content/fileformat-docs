---
title: Excel cannot open the file in File Formats XlsIO | Syncfusion
description: This page shows how to resolve "Excel cannot open the file because the file format is not valid..." using XlsIO.
platform: file-formats
control: XlsIO
documentation: UG
---

# How to resolve "Excel cannot open the file 'filename.xlsx'..." error?

This error "Excel cannot open the file 'filename.xlsx' because the file format for the file extension is not valid. Verify that the file has not been corrupted and that the file extension matches the format of the file" occurs when there is a mismatch between the file format and its extension. The default workbook creation version in XlsIO is Excel97-2003 (.xls). The application version set to the required version should match its file format during save, as in the below code. 

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;

//Set application version
application.DefaultVersion = ExcelVersion.Excel2013;

//Do some manipulation
//Do some manipulation

//Workbook is saved in Excel2013 format
FileStream stream = new FileStream("Sample.xlsx", FileMode.OpenOrCreate, FileAccess.ReadWrite);
workbook.SaveAs(stream);
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;

//Set application version
application.DefaultVersion = ExcelVersion.Excel2013;

//Do some manipulation
//Do some manipulation

//Workbook is saved in Excel2013 format
workbook.SaveAs("Sample.xlsx");
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Dim excelEngine As New ExcelEngine()
Dim application As IApplication = excelEngine.Excel

'Set application version
application.DefaultVersion = ExcelVersion.Excel2013

'Do some manipulation
'Do some manipulation

'Workbook is saved in Excel2013 format
workbook.SaveAs("Sample.xlsx")
{% endhighlight %}
{% endtabs %}  

If the application version is ignored, then the workbook version should be set properly during creation and save.

* To save a workbook in Excel2003 format, set the workbook version to Excel97to2003 and save the file with extension ‘.xls’ i.e. binary file format.

* To save a workbook in Excel 2007 and above formats, set the workbook version to Excel2007 and above and save the file with extension __‘.____xlsx’__ i.e. open XML file format.

These are represented in the below code snippet.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
workbook.Version = ExcelVersion.Excel97to2003;
FileStream stream = new FileStream("Sample.xls", FileMode.OpenOrCreate, FileAccess.ReadWrite);
workbook.SaveAs(stream);

workbook.Version = ExcelVersion.Excel2013;
FileStream stream1 = new FileStream("Sample.xlsx", FileMode.OpenOrCreate, FileAccess.ReadWrite);
workbook.SaveAs(stream1); 
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
workbook.Version = ExcelVersion.Excel97to2003;
workbook.SaveAs("Sample.xls");

workbook.Version = ExcelVersion.Excel2013;
workbook.SaveAs("Sample.xlsx");
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
workbook.Version = ExcelVersion.Excel97to2003
workbook.SaveAs("Sample.xls")

workbook.Version = ExcelVersion.Excel2013
workbook.SaveAs("Sample.xlsx")
{% endhighlight %}
{% endtabs %}  
  
## See Also

* [How to resolve the File does not contain workbook stream error](how-to-resolve-the-file-does-not-contain-workbook-stream-error)
* [What are the known exceptions of XlsIO?](https://help.syncfusion.com/document-processing/excel/excel-library/net/known-exceptions)
* [What are the supported features by file formats?](https://help.syncfusion.com/document-processing/excel/excel-library/net/supported-features-by-file-formats)
