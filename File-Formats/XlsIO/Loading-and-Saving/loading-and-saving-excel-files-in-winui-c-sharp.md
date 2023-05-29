---
title: Loading and saving workbook in WinUI | Syncfusion
description: Explains how to load and save Excel files in WinUI applications using Syncfusion Excel Library.
platform: file-formats
control: XlsIO
documentation: UG
---
# Loading and saving workbook in WinUI

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
Stream inputStream = executingAssembly.GetManifestResourceStream("WinUISample.Sample.xlsx");

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
Stream inputStream = executingAssembly.GetManifestResourceStream("WinUISample.Sample.xlsx");

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
Save(outputStream, "Output");
{% endhighlight %}
{% endtabs %} 

## Closing a workbook

Once after the workbook manipulation and save operation are completed, you should close the instance of [IWorkbook](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbook.html) and dispose the instance of [ExcelEngine](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelEngine.html), in order to release all the memory consumed by XlsIO’s DOM. The following code snippet illustrates how to close the instance of [IWorkbook](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbook.html) and dispose the instance of [ExcelEngine](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelEngine.html).

N> If the new instance for [ExcelEngine](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelEngine.html) is created in using statement, then there is no need to closing workbook and disposing excelEngine.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Creates a new instance for ExcelEngine
ExcelEngine excelEngine = new ExcelEngine();

//Initialize IApplication
IApplication application = excelEngine.Excel;

//Load the file into stream
Assembly executingAssembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = executingAssembly.GetManifestResourceStream("WinUISample.Sample.xlsx");

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
Save(outputStream, "Output");

//Close the instance of IWorkbook
workbook.Close();

//Dispose the instance of ExcelEngine
excelEngine.Dispose();
{% endhighlight %}
{% endtabs %}

T>You can use [ThrowNotSavedOnDestroy](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelEngine.html#Syncfusion_XlsIO_ExcelEngine_ThrowNotSavedOnDestroy) property of [ExcelEngine](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelEngine.html) object to prevent the data loss while unfortunately closing the workbook or disposing excel engine without saving contents. If it is set to true, then **ExcelWorkbookNotSavedException** will be thrown when you forgot to save the workbook before closing them. Following code illustrates how to set [ThrowNotSavedOnDestroy](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelEngine.html#Syncfusion_XlsIO_ExcelEngine_ThrowNotSavedOnDestroy) property of [ExcelEngine](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelEngine.html) object.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Creates a new instance for ExcelEngine
ExcelEngine excelEngine = new ExcelEngine();

//No exception will be thrown if there are unsaved workbooks
excelEngine.ThrowNotSavedOnDestroy = true;
{% endhighlight %}
{% endtabs %}
