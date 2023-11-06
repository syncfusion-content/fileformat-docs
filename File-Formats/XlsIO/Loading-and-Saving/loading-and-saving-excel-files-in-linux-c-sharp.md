---
title: Loading and saving workbook on Linux | Syncfusion
description: Explains how to load and save Excel files on Linux applications using Syncfusion XlsIO.
platform: file-formats
control: XlsIO
documentation: UG
---
# Loading and saving workbook on Linux

## Opening an existing workbook from stream

You can open an existing workbook from stream by using the overloads of [Open](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbooks.html#Syncfusion_XlsIO_IWorkbooks_Open_System_IO_Stream_) methods of [IWorkbooks](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbooks.html) interface.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Creates a new instance for ExcelEngine
ExcelEngine excelEngine = new ExcelEngine();

//Initialize IApplication
IApplication application = excelEngine.Excel;

//A existing workbook is opened.             
FileStream inputStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
IWorkbook workbook = application.Workbooks.Open(inputStream);
{% endhighlight %}
{% endtabs %}  

## Saving an Excel workbook to stream

You can also save the created or manipulated workbook to stream using overloads of [SaveAs](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbook.html#Syncfusion_XlsIO_IWorkbook_SaveAs_System_IO_Stream_) methods.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Creates a new instance for ExcelEngine
ExcelEngine excelEngine = new ExcelEngine();

//Initialize IApplication
IApplication application = excelEngine.Excel;

//A existing workbook is opened.             
FileStream inputStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
IWorkbook workbook = application.Workbooks.Open(inputStream);

//To-Do some manipulation
//To-Do some manipulation

//Set the version of the workbook
workbook.Version = ExcelVersion.Xlsx;

//Initialize stream
FileStream outputStream = new FileStream("Output.xlsx", FileMode.Create);

//Save the workbook as stream
workbook.SaveAs(outputStream);
{% endhighlight %}
{% endtabs %} 
