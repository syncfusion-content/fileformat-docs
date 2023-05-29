---
title: Loading and saving workbook in UWP | Syncfusion
description: Explains how to load and save Excel files in UWP applications using Syncfusion XlsIO.
platform: file-formats
control: XlsIO
documentation: UG
---
# Loading and saving workbook in UWP

## Opening an existing workbook

You can open an existing workbook by using the overloads of [Open](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbooks.html#Syncfusion_XlsIO_IWorkbooks_Open_System_String_) methods of [IWorkbooks](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbooks.html) interface.

{% tabs %}  
{% highlight c# tabtitle="C# [Windows-specific]" %}
//Creates a new instance for ExcelEngine
ExcelEngine excelEngine = new ExcelEngine();

//Initialize IApplication
IApplication application = excelEngine.Excel;

//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".xlsx");
openPicker.FileTypeFilter.Add(".xls");
StorageFile file = await openPicker.PickSingleFileAsync();

//Opens the workbook
IWorkbook workbook = await application.Workbooks.OpenAsync(file, ExcelOpenType.Automatic);
{% endhighlight %}
{% endtabs %}

## Saving an Excel workbook

You can also save the created or manipulated workbook using overloads of [SaveAs](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbook.html#Syncfusion_XlsIO_IWorkbook_SaveAs_System_String_System_Web_HttpResponse_Syncfusion_XlsIO_ExcelDownloadType_Syncfusion_XlsIO_ExcelHttpContentType_) methods.

{% tabs %}
{% highlight c# tabtitle="C# [Windows-specific]" %}
//Creates a new instance for ExcelEngine
ExcelEngine excelEngine = new ExcelEngine();

//Initialize IApplication
IApplication application = excelEngine.Excel;

//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".xlsx");
openPicker.FileTypeFilter.Add(".xls");
StorageFile file = await openPicker.PickSingleFileAsync();

//Opens the workbook
IWorkbook workbook = await application.Workbooks.OpenAsync(file, ExcelOpenType.Automatic);

//To-Do some manipulation
//To-Do some manipulation

//Set the version of the workbook
workbook.Version = ExcelVersion.Xlsx;

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Output";
savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await workbook.SaveAsAsync(storageFile);
{% endhighlight %}
{% endtabs %} 

## Closing a workbook

Once after the workbook manipulation and save operation are completed, you should close the instance of [IWorkbook](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbook.html) and dispose the instance of [ExcelEngine](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelEngine.html), in order to release all the memory consumed by XlsIO’s DOM. The following code snippet illustrates how to close the instance of [IWorkbook](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbook.html) and dispose the instance of [ExcelEngine](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelEngine.html).

N> If the new instance for [ExcelEngine](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelEngine.html) is created in using statement, then there is no need to closing workbook and disposing excelEngine.

{% tabs %}
{% highlight c# tabtitle="C# [Windows-specific]" %}
//Creates a new instance for ExcelEngine
ExcelEngine excelEngine = new ExcelEngine();

//Initialize IApplication
IApplication application = excelEngine.Excel;

//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".xlsx");
openPicker.FileTypeFilter.Add(".xls");
StorageFile file = await openPicker.PickSingleFileAsync();

//Opens the workbook
IWorkbook workbook = await application.Workbooks.OpenAsync(file, ExcelOpenType.Automatic);

//To-Do some manipulation
//To-Do some manipulation

//Set the version of the workbook
workbook.Version = ExcelVersion.Xlsx;

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Output";
savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await workbook.SaveAsAsync(storageFile);

//Close the instance of IWorkbook
workbook.Close();

//Dispose the instance of ExcelEngine
excelEngine.Dispose();
{% endhighlight %}
{% endtabs %}

T>You can use [ThrowNotSavedOnDestroy](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelEngine.html#Syncfusion_XlsIO_ExcelEngine_ThrowNotSavedOnDestroy) property of [ExcelEngine](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelEngine.html) object to prevent the data loss while unfortunately closing the workbook or disposing excel engine without saving contents. If it is set to true, then **ExcelWorkbookNotSavedException** will be thrown when you forgot to save the workbook before closing them. Following code illustrates how to set [ThrowNotSavedOnDestroy](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelEngine.html#Syncfusion_XlsIO_ExcelEngine_ThrowNotSavedOnDestroy) property of [ExcelEngine](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelEngine.html) object.

{% tabs %}
{% highlight c# tabtitle="C# [Windows-specific]" %}
//Creates a new instance for ExcelEngine
ExcelEngine excelEngine = new ExcelEngine();

//No exception will be thrown if there are unsaved workbooks
excelEngine.ThrowNotSavedOnDestroy = true;
{% endhighlight %}
{% endtabs %}
