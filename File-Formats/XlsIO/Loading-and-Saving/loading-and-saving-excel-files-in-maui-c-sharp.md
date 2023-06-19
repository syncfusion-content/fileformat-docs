---
title: Loading and saving workbook in .NET MAUI | Syncfusion
description: Explains how to load and save Excel files in .NET MAUI applications using Syncfusion Excel Library.
platform: file-formats
control: XlsIO
documentation: UG
---
# Loading and saving workbook in .NET MAUI

## Opening an existing workbook from stream

You can open an existing workbook from stream by using the overloads of [Open](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbooks.html#Syncfusion_XlsIO_IWorkbooks_Open_System_IO_Stream_) methods of [IWorkbooks](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbooks.html) interface.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Creates a new instance for ExcelEngine
ExcelEngine excelEngine = new ExcelEngine();

//Initialize IApplication
IApplication application = excelEngine.Excel;

//Load the file into stream
Assembly executingAssembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = executingAssembly.GetManifestResourceStream("MAUISample.Sample.xlsx");

//Loads or open an existing workbook through Open method of IWorkbooks
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

//Load the file into stream
Assembly executingAssembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = executingAssembly.GetManifestResourceStream("MAUISample.Sample.xlsx");

//Loads or open an existing workbook through Open method of IWorkbooks
IWorkbook workbook = application.Workbooks.Open(inputStream);

//To-Do some manipulation
//To-Do some manipulation

//Set the version of the workbook
workbook.Version = ExcelVersion.Xlsx;

//Saving the workbook as stream
MemoryStream outputStream = new MemoryStream();
workbook.SaveAs(outputStream);
outputStream.Position = 0;

//Saves the memory stream as a file.
SaveService saveService = new SaveService();
saveService.SaveAndView("Output.xlsx", "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", ms);
{% endhighlight %}
{% endtabs %} 

The code for SaveService helper class is present in below pages.
[https://help.syncfusion.com/file-formats/xlsio/create-read-edit-excel-files-in-maui-c-sharp#save-service-class-in-portable-project](https://help.syncfusion.com/file-formats/xlsio/create-read-edit-excel-files-in-maui-c-sharp#save-service-class-in-portable-project)
[https://help.syncfusion.com/file-formats/xlsio/create-read-edit-excel-files-in-maui-c-sharp#save-and-view-the-excel-document-in-windows](https://help.syncfusion.com/file-formats/xlsio/create-read-edit-excel-files-in-maui-c-sharp#save-and-view-the-excel-document-in-windows)
[https://help.syncfusion.com/file-formats/xlsio/create-read-edit-excel-files-in-maui-c-sharp#save-and-view-the-excel-document-in-android](https://help.syncfusion.com/file-formats/xlsio/create-read-edit-excel-files-in-maui-c-sharp#save-and-view-the-excel-document-in-android)
[https://help.syncfusion.com/file-formats/xlsio/create-read-edit-excel-files-in-maui-c-sharp#save-and-view-the-excel-document-in-ios](https://help.syncfusion.com/file-formats/xlsio/create-read-edit-excel-files-in-maui-c-sharp#save-and-view-the-excel-document-in-ios)
[https://help.syncfusion.com/file-formats/xlsio/create-read-edit-excel-files-in-maui-c-sharp#save-and-view-the-excel-document-in-maccatalyst](https://help.syncfusion.com/file-formats/xlsio/create-read-edit-excel-files-in-maui-c-sharp#save-and-view-the-excel-document-in-maccatalyst)
