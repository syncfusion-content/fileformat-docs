---
title: UWP
description: Briefs about loading and saving an Excel document in UWP platform.
platform: file-formats
control: XlsIO
documentation: UG
---
# UWP 

In order to use XlsIO in your UWP application, please add the required assemblies in your UWP application. Refer [Assemblies Required](/File-Formats/XlsIO/Assemblies-Required).

## Loading the document

The below code snippet illustrates how to load an Excel file using file picker in UWP.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

//Instantiates the File Picker. 

FileOpenPicker openPicker = new FileOpenPicker();

openPicker.SuggestedStartLocation = PickerLocationId.Desktop;

openPicker.FileTypeFilter.Add(".xlsx");

openPicker.FileTypeFilter.Add(".xls");

StorageFile openFile = await openPicker.PickSingleFileAsync();


//Opens the workbook. 

IWorkbook workbook = await application.Workbooks.OpenAsync(openFile);

//Sets workbook version.

workbook.Version = ExcelVersion.Excel2013;


//Initializes FileSavePicker.

FileSavePicker savePicker = new FileSavePicker();

savePicker.SuggestedStartLocation = PickerLocationId.Desktop;

savePicker.SuggestedFileName = "CreateSpreadsheet";

savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

//Creates a storage file from FileSavePicker.

StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file.

await workbook.SaveAsAsync(storageFile);

workbook.Close();

excelEngine.Dispose();
{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

'Instantiates the File Save Picker.  

Dim openPicker As New FileOpenPicker()

openPicker.SuggestedStartLocation = PickerLocationId.Desktop 

openPicker.FileTypeFilter.Add(".xlsx") 

openPicker.FileTypeFilter.Add(".xls") 

Dim openFile As StorageFile = Await openPicker.PickSingleFileAsync()


'Opens the Workbook. 

Dim workbook As IWorkbook = Await application.Workbooks.OpenAsync(openFile)

Dim workbook.SaveAsAsyncCType(As await, openFile)

'Sets workbook version.

workbook.Version = ExcelVersion.Excel2013

'Initializes FileSavePicker.

Dim savePicker As New FileSavePicker()

savePicker.SuggestedStartLocation = PickerLocationId.Desktop

savePicker.SuggestedFileName = "CreateSpreadsheet"

savePicker.FileTypeChoices.Add("Excel Files", New List(Of String)() From {".xlsx"})


'Creates a storage file from FileSavePicker.

Dim storageFile As StorageFile = Await savePicker.PickSaveFileAsync()

'Saves changes to the specified storage file.

Await workbook.SaveAsAsync(storageFile)

workbook.Close()

excelEngine.Dispose()
{% endhighlight %}

{% endtabs %}  

The below code snippet illustrates how to load an Xml file in UWP.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

//Instantiates the File Picker. 

FileOpenPicker openPicker = new FileOpenPicker();

openPicker.SuggestedStartLocation = PickerLocationId.Desktop;

openPicker.FileTypeFilter.Add(".xml");

StorageFile openFile = await openPicker.PickSingleFileAsync();


//Opens the workbook. 

IWorkbook workbook = await application.Workbooks.OpenAsync(openFile);


//Sets workbook version.

workbook.Version = ExcelVersion.Excel2013;


//Initializes FileSavePicker.

FileSavePicker savePicker = new FileSavePicker();

savePicker.SuggestedStartLocation = PickerLocationId.Desktop;

savePicker.SuggestedFileName = "CreateSpreadsheet";

savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });


//Creates a storage file from FileSavePicker.

StorageFile storageFile = await savePicker.PickSaveFileAsync();


//Saves changes to the specified storage file.

await workbook.SaveAsAsync(storageFile);

workbook.Close();

excelEngine.Dispose();
{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine()

Dim application As IApplication = ExcelEngine.Excel


'Instantiates the File Save Picker. 

Dim openPicker As New FileOpenPicker()

openPicker.SuggestedStartLocation = PickerLocationId.Desktop 

openPicker.FileTypeFilter.Add(".xml") 

Dim openFile As StorageFile = Await openPicker.PickSingleFileAsync()


'Opens the workbook.

Dim workbook As IWorkbook = Await Application.Workbooks.OpenAsync(openFile)


'Sets workbook version.

workbook.Version = ExcelVersion.Excel2013


'Initializes FileSavePicker.

Dim savePicker As New FileSavePicker()

savePicker.SuggestedStartLocation = PickerLocationId.Desktop

savePicker.SuggestedFileName = "CreateSpreadsheet"

savePicker.FileTypeChoices.Add("Excel Files", New List(Of String)() From {".xlsx"})


'Creates a storage file from FileSavePicker.

Dim storageFile As StorageFile = Await savePicker.PickSaveFileAsync()


'Saves changes to the specified storage file.

Await workbook.SaveAsAsync(storageFile)

workbook.Close()

excelEngine.Dispose()
{% endhighlight %}

{% endtabs %}  

## Saving the document

The following code snippet illustrates how to save an Excel document in UWP using file picker.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

IWorkbook workbook = application.Workbooks.Create(1);


//Instantiates the File Picker. 

FileOpenPicker openPicker = new FileOpenPicker();

openPicker.SuggestedStartLocation = PickerLocationId.Desktop;

openPicker.FileTypeFilter.Add(".xlsx");

openPicker.FileTypeFilter.Add(".xls");

StorageFile openFile = await openPicker.PickSingleFileAsync();


//Opens the workbook. 

IWorkbook workbook = await application.Workbooks.OpenAsync(openFile);

await workbook.SaveAsAsync(openFile);

workbook.Close();

excelEngine.Dispose();
{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine()

Dim application As IApplication = ExcelEngine.Excel

Dim workbook As IWorkbook = Application.Workbooks.Create(1)


'Instantiates the File Picker. 

Dim openPicker As FileOpenPicker = New FileOpenPicker()

openPicker.SuggestedStartLocation = PickerLocationId.Desktop

openPicker.FileTypeFilter.Add(".xlsx")

openPicker.FileTypeFilter.Add(".xls")

Dim openFile As StorageFile = Await openPicker.PickSingleFileAsync()


'Opens the workbook. 

Dim workbook As IWorkbook = Await Application.Workbooks.OpenAsync(openFile)

Dim workbook.SaveAsAsyncCType(As await, openFile)

workbook.Close()

excelEngine.Dispose()
{% endhighlight %}
{% endtabs %}  

