---
title: Working with Pivot Tables
description: Briefs about working with Pivot tables in XlsIO
platform: File-Formats
control: XlsIO
documentation: UG
---
# Working with Pivot Tables

You can easily arrange and summarize complex data in a [Pivot Table](https://support.office.com/en-us/article/PivotTable-I-Get-started-with-PivotTable-reports-in-Excel-2007-bfe774d3-3e20-46f7-b6a3-f7984855d665). Creation and Manipulation of pivot table is supported in Excel 2007 and later formats, and pivot table in existing document can be preserved for Excel 2003 format**.**

## Create a Pivot Table

Following are the steps for creating a simple pivot table.

* Add pivot cache
* Add Pivot table
* Add row and column fields
* Add data fields

Pivot tables do not take data directly from the source data, but rather from the pivot cache that memorizes a snapshot of the data. **IPivotCache** interface caches the data that needs to be summarized. 

The data in worksheet is added to pivot cache as below.

{% tabs %}  

{% highlight c# %}
//Create Pivot cache with the given data range
IPivotCache cache = workbook.PivotCaches.Add(worksheet["A1:H50"]);

{% endhighlight %}

{% highlight vb %}
'Create Pivot cache with the given data range
Dim cache As IPivotCache = workbook.PivotCaches.Add(worksheet("A1:H50"))

{% endhighlight %}

{% highlight UWP %}
//Create Pivot cache with the given data range
IPivotCache cache = workbook.PivotCaches.Add(worksheet["A1:H50"]);
{% endhighlight %}

{% highlight asp.net core %}
//Create Pivot cache with the given data range
IPivotCache cache = workbook.PivotCaches.Add(worksheet["A1:H50"]);
{% endhighlight %}

{% highlight Xamarin %}
//Create Pivot cache with the given data range
IPivotCache cache = workbook.PivotCaches.Add(worksheet["A1:H50"]);
{% endhighlight %}
  {% endtabs %}  

**IPivotTable** represents a single pivot table object created from the cache. It has properties that allow to customize pivot table. The following code creates a blank pivot table. 

{% tabs %}  

{% highlight c# %}
//Create "PivotTable1" with the cache at the specified range
IPivotTable pivotTable = worksheet.PivotTables.Add("PivotTable1", worksheet ["A1"], cache);

{% endhighlight %}

{% highlight vb %}
'Create "PivotTable1" with the cache at the specified range
Dim pivotTable As IPivotTable = worksheet.PivotTables.Add("PivotTable1", worksheet ("A1"), cache)

{% endhighlight %}

{% highlight UWP %}
//Create "PivotTable1" with the cache at the specified range
IPivotTable pivotTable = worksheet.PivotTables.Add("PivotTable1", worksheet ["A1"], cache);
{% endhighlight %}

{% highlight asp.net core %}
//Create "PivotTable1" with the cache at the specified range
IPivotTable pivotTable = worksheet.PivotTables.Add("PivotTable1", worksheet ["A1"], cache);
{% endhighlight %}

{% highlight Xamarin %}
//Create "PivotTable1" with the cache at the specified range
IPivotTable pivotTable = worksheet.PivotTables.Add("PivotTable1", worksheet ["A1"], cache);
{% endhighlight %}

  {% endtabs %}  

Now the pivot table should be populated with required fields. **IPivotField** represents a single field in the pivot table which includes row, column and data field axes. 

{% tabs %}  

{% highlight c# %}
//Add Pivot table fields (Row and Column fields)
pivotTable.Fields[2].Axis = PivotAxisTypes.Row;
pivotTable.Fields[6].Axis = PivotAxisTypes.Row;
pivotTable.Fields[3].Axis = PivotAxisTypes.Column;

{% endhighlight %}

{% highlight vb %}
'Add Pivot table fields (Row and Column fields)
pivotTable.Fields(2).Axis = PivotAxisTypes.Row
pivotTable.Fields(6).Axis = PivotAxisTypes.Row
pivotTable.Fields(3).Axis = PivotAxisTypes.Column

{% endhighlight %}

{% highlight UWP %}
//Add Pivot table fields (Row and Column fields)
pivotTable.Fields[2].Axis = PivotAxisTypes.Row;
pivotTable.Fields[6].Axis = PivotAxisTypes.Row;
pivotTable.Fields[3].Axis = PivotAxisTypes.Column;
{% endhighlight %}

{% highlight asp.net core %}
//Add Pivot table fields (Row and Column fields)
pivotTable.Fields[2].Axis = PivotAxisTypes.Row;
pivotTable.Fields[6].Axis = PivotAxisTypes.Row;
pivotTable.Fields[3].Axis = PivotAxisTypes.Column;
{% endhighlight %}

{% highlight Xamarin %}
//Add Pivot table fields (Row and Column fields)
pivotTable.Fields[2].Axis = PivotAxisTypes.Row;
pivotTable.Fields[6].Axis = PivotAxisTypes.Row;
pivotTable.Fields[3].Axis = PivotAxisTypes.Column;
{% endhighlight %}

  {% endtabs %}  

**IPivotDataFields** represents a collection of data fields in the pivot table. The data field is added with the required subtotal function using **PivotSubtotalTypes** enumeration. To know more about different subtotal types supported in Pivot Tables, please refer **PivotSubtotalTypes** in API section. Following is the code to configure a pivot field as a data field.

{% tabs %}  

{% highlight c# %}
//Add data field
IPivotField field = pivotTable.Fields[5];
pivotTable.DataFields.Add(field, "Sum", PivotSubtotalTypes.Sum);
{% endhighlight %}

{% highlight vb %}
'Add data field
Dim field As IPivotField = pivotTable.Fields(5)
pivotTable.DataFields.Add(field, "Sum", PivotSubtotalTypes.Sum)
{% endhighlight %}

{% highlight UWP %}
//Add data field
IPivotField field = pivotTable.Fields[5];
pivotTable.DataFields.Add(field, "Sum", PivotSubtotalTypes.Sum);
{% endhighlight %}

{% highlight asp.net core %}
//Add data field
IPivotField field = pivotTable.Fields[5];
pivotTable.DataFields.Add(field, "Sum", PivotSubtotalTypes.Sum);
{% endhighlight %}
{% highlight Xamarin %}
//Add data field
IPivotField field = pivotTable.Fields[5];
pivotTable.DataFields.Add(field, "Sum", PivotSubtotalTypes.Sum);
{% endhighlight %}
  {% endtabs %}  

Following code example illustrates how to create a pivot table with existing data in the worksheet, using XlsIO.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("PivotData.xlsx");
IWorksheet worksheet = workbook.Worksheets[0];
IWorksheet pivotsheet = workbook.Worksheets[0];

//Create Pivot cache with the given data range
IPivotCache cache = workbook.PivotCaches.Add(worksheet["A1:H50"]);

//Create "PivotTable1" with the cache at the specified range
IPivotTable pivotTable = pivotsheet.PivotTables.Add("PivotTable1", pivotsheet["A1"], cache);

//Add Pivot table fields (Row and Column fields)
pivotTable.Fields[2].Axis = PivotAxisTypes.Row;
pivotTable.Fields[6].Axis = PivotAxisTypes.Row;
pivotTable.Fields[3].Axis = PivotAxisTypes.Column;

//Add data field
IPivotField field = pivotTable.Fields[2];

pivotTable.DataFields.Add(field, "Sum", PivotSubtotalTypes.Sum);

workbook.SaveAs("PivotTable.xlsx");

workbook.Close();
excelEngine.Dispose();

{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine
Dim application As IApplication = excelEngine.Excel
application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("PivotData.xlsx")
Dim worksheet As IWorksheet = workbook.Worksheets(0)
Dim pivotsheet As IWorksheet = workbook.Worksheets(1)

'Create Pivot cache with the given data range
Dim cache As IPivotCache = workbook.PivotCaches.Add(worksheet("A1:H50"))

'Create "PivotTable1" with the cache at the specified range
Dim pivotTable As IPivotTable = pivotsheet.PivotTables.Add("PivotTable1", pivotsheet("A1"), cache)

'Add Pivot table fields (Row and Column fields)
pivotTable.Fields(2).Axis = PivotAxisTypes.Row
pivotTable.Fields(6).Axis = PivotAxisTypes.Row
pivotTable.Fields(3).Axis = PivotAxisTypes.Column

'Add data field
Dim field As IPivotField = pivotTable.Fields(5)

pivotTable.DataFields.Add(field, "Sum", PivotSubtotalTypes.Sum)

workbook.SaveAs("PivotTable.xlsx")

workbook.Close()
excelEngine.Dispose()

{% endhighlight %}

{% highlight UWP %}
//Gets assembly
Assembly assembly = typeof(App).GetTypeInfo().Assembly;

//Gets input Excel document from embedded resource collection
Stream inputStream = assembly.GetManifestResourceStream("PivotTable.PivotData.xlsx");

ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = await application.Workbooks.OpenAsync(inputStream);
IWorksheet worksheet = workbook.Worksheets[0];
IWorksheet pivotsheet = workbook.Worksheets[1];

//Create Pivot cache with the given data range
IPivotCache cache = workbook.PivotCaches.Add(worksheet["A1:H50"]);

//Create "PivotTable1" with the cache at the specified range
IPivotTable pivotTable = pivotsheet.PivotTables.Add("PivotTable1", pivotsheet["A1"], cache);

//Add Pivot table fields (Row and Column fields)
pivotTable.Fields[2].Axis = PivotAxisTypes.Row;
pivotTable.Fields[6].Axis = PivotAxisTypes.Row;
pivotTable.Fields[3].Axis = PivotAxisTypes.Column;

//Add data field
IPivotField field = pivotTable.Fields[2];

pivotTable.DataFields.Add(field, "Sum", PivotSubtotalTypes.Sum);

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "PivotTable";
savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await workbook.SaveAsAsync(storageFile);

workbook.Close();
excelEngine.Dispose();
{% endhighlight %}

{% highlight asp.net core %}
ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
FileStream fileStream = new FileStream("PivotData.xlsx", FileMode.Open, FileAccess.Read);

IWorkbook workbook = application.Workbooks.Open(fileStream);
IWorksheet worksheet = workbook.Worksheets[0];
IWorksheet pivotsheet = workbook.Worksheets[1];

//Create Pivot cache with the given data range
IPivotCache cache = workbook.PivotCaches.Add(worksheet["A1:H50"]);

//Create "PivotTable1" with the cache at the specified range
IPivotTable pivotTable = pivotsheet.PivotTables.Add("PivotTable1", pivotsheet["A1"], cache);

//Add Pivot table fields (Row and Column fields)
pivotTable.Fields[2].Axis = PivotAxisTypes.Row;
pivotTable.Fields[6].Axis = PivotAxisTypes.Row;
pivotTable.Fields[3].Axis = PivotAxisTypes.Column;

//Add data field
IPivotField field = pivotTable.Fields[2];

pivotTable.DataFields.Add(field, "Sum", PivotSubtotalTypes.Sum);

string fileName = "PivotTable.xlsx";

//Saving the workbook as stream
FileStream stream = new FileStream(fileName, FileMode.Create, FileAccess.ReadWrite);
workbook.SaveAs(stream);

stream.Dispose();
workbook.Close();
excelEngine.Dispose();
{% endhighlight %}

{% highlight Xamarin %}
//Gets assembly
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
           
//Gets input Excel document from embedded resource collection
Stream inputStream = assembly.GetManifestResourceStream("PivotTable.PivotData.xlsx");

ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open(inputStream);
IWorksheet worksheet = workbook.Worksheets[0];
IWorksheet pivotsheet = workbook.Worksheets[1];

//Create Pivot cache with the given data range
IPivotCache cache = workbook.PivotCaches.Add(worksheet["A1:H50"]);

//Create "PivotTable1" with the cache at the specified range
IPivotTable pivotTable = pivotsheet.PivotTables.Add("PivotTable1", pivotsheet["A1"], cache);

//Add Pivot table fields (Row and Column fields)
pivotTable.Fields[2].Axis = PivotAxisTypes.Row;
pivotTable.Fields[6].Axis = PivotAxisTypes.Row;
pivotTable.Fields[3].Axis = PivotAxisTypes.Column;

//Add data field
IPivotField field = pivotTable.Fields[2];

pivotTable.DataFields.Add(field, "Sum", PivotSubtotalTypes.Sum);

//Saving the workbook as stream
MemoryStream outputStream = new MemoryStream();
workbook.SaveAs(outputStream);

workbook.Close();
excelEngine.Dispose();

string fileName = "PivotTable.xlsx";

//Save the stream as Excel document and view the saved document
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    await DependencyService.Get<ISaveWindowsPhone>().SaveAndView(fileName, "application/msexcel", outputStream);
else
    DependencyService.Get<ISave>().SaveAndView(fileName, "application/msexcel", outputStream);

//Dispose the input and output stream instances
inputStream.Dispose();
outputStream.Dispose();
{% endhighlight %}
  {% endtabs %}  

The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer [SaveAndView](https://help.syncfusion.com/file-formats/xlsio/xamarin#saving-a-document) for respective code samples.

## Editing and Formatting a Pivot Table

A Pivot table can be accessed from **IPivotTables** interface which holds the collection of pivot tables in the worksheet. The below code shows how to dynamically refresh the data in a pivot table. In prior,

* Create the pivot table using Excel GUI.
* Specify the named range to be the data source of the pivot table.
* Make sure that the "Refresh on Open" option of the pivot table is selected.
* Dynamically refresh the data in the Named Range.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("PivotTable.xlsx");
IWorksheet pivotSheet = workbook.Worksheets[0];

//Change the range values that the Pivot Tables range refers to
workbook.Names["PivotRange"].RefersToRange = pivotSheet.Range["A1:D27"];

workbook.SaveAs("PivotTable_DynamicRange.xlsx");

workbook.Close();
excelEngine.Dispose();

{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine
Dim application As IApplication = excelEngine.Excel
application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("PivotTable.xlsx")
Dim pivotSheet As IWorksheet = workbook.Worksheets(0)

'Change the range values that the Pivot Tables range refers to
Private workbook.Names("PivotRange").RefersToRange = mySheet.Range("A1:D27")

workbook.SaveAs("PivotTable_DynamicRange.xlsx")

workbook.Close()
excelEngine.Dispose()

{% endhighlight %}

{% highlight UWP %}
//Gets assembly
Assembly assembly = typeof(App).GetTypeInfo().Assembly;

//Gets input Excel document from embedded resource collection
Stream inputStream = assembly.GetManifestResourceStream("PivotTable.PivotTable.xlsx");

ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = await application.Workbooks.OpenAsync(inputStream);
IWorksheet pivotSheet = workbook.Worksheets[0];

//Change the range values that the Pivot Tables range refers to
workbook.Names["PivotRange"].RefersToRange = pivotSheet.Range["A1:D27"];

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "PivotTable_DynamicRange";
savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await workbook.SaveAsAsync(storageFile);

workbook.Close();
excelEngine.Dispose();
{% endhighlight %}

{% highlight asp.net core %}
ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
application.DefaultVersion = ExcelVersion.Excel2013;

FileStream fileStream = new FileStream("PivotTable.xlsx", FileMode.Open, FileAccess.Read);

IWorkbook workbook = application.Workbooks.Open(fileStream);
IWorksheet pivotSheet = workbook.Worksheets[0];

//Change the range values that the Pivot Tables range refers to
workbook.Names["PivotRange"].RefersToRange = pivotSheet.Range["A1:D27"];

string fileName = "PivotTable_DynamicRange.xlsx";

//Saving the workbook as stream
FileStream stream = new FileStream(fileName, FileMode.Create, FileAccess.ReadWrite);
workbook.SaveAs(stream);

stream.Dispose();
workbook.Close();
excelEngine.Dispose();
{% endhighlight %}

{% highlight Xamarin %}
//Gets assembly
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
           
//Gets input Excel document from embedded resource collection
Stream inputStream = assembly.GetManifestResourceStream("PivotTable.PivotTable.xlsx");

ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open(inputStream);
IWorksheet pivotSheet = workbook.Worksheets[0];

//Change the range values that the Pivot Tables range refers to
workbook.Names["PivotRange"].RefersToRange = pivotSheet.Range["A1:D27"];

//Saving the workbook as stream
MemoryStream outputStream = new MemoryStream();
workbook.SaveAs(outputStream);

workbook.Close();
excelEngine.Dispose();

string fileName = "PivotTable_DynamicRange.xlsx";

//Save the stream as Excel document and view the saved document
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    await DependencyService.Get<ISaveWindowsPhone>().SaveAndView(fileName, "application/msexcel", outputStream);
else
    DependencyService.Get<ISave>().SaveAndView(fileName, "application/msexcel", outputStream);

//Dispose the input and output stream instances
inputStream.Dispose();
outputStream.Dispose();
{% endhighlight %}
  {% endtabs %}  

The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer [SaveAndView](https://help.syncfusion.com/file-formats/xlsio/xamarin#saving-a-document) for respective code samples.

XlsIO supports 85 built-in styles of Excel 2007, enabling users to create a table with rich formatting through PivotBuiltInStyles property as follows. To know more about various built-in styles supported, please refer **PivotBuiltInStyles** enumeration in API section.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("PivotTable.xlsx");
IWorksheet worksheet = workbook.Worksheets[1];
IPivotTable pivotTable = worksheet.PivotTables[0];

//Set BuiltInStyle
pivotTable.BuiltInStyle = PivotBuiltInStyles.PivotStyleDark12;

workbook.SaveAs("PivotTable_Style.xlsx");

workbook.Close();

//No exception will be thrown if there are unsaved workbooks
excelEngine.ThrowNotSavedOnDestroy = false;
excelEngine.Dispose();

{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine
Dim application As IApplication = excelEngine.Excel
application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("PivotTable.xlsx")
Dim sheet As IWorksheet = workbook.Worksheets(1)
Dim pivotTable As IPivotTable = sheet.PivotTables(0)

'Set BuiltInStyle
pivotTable.BuiltInStyle = PivotBuiltInStyles.PivotStyleDark12

workbook.SaveAs("PivotTable_Style.xlsx")

workbook.Close()

'No exception will be thrown if there are unsaved workbooks
excelEngine.ThrowNotSavedOnDestroy = False
excelEngine.Dispose()

{% endhighlight %}

{% highlight UWP %}
//Gets assembly
Assembly assembly = typeof(App).GetTypeInfo().Assembly;

//Gets input Excel document from embedded resource collection
Stream inputStream = assembly.GetManifestResourceStream("PivotTable.PivotTable.xlsx");

ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = await application.Workbooks.OpenAsync(inputStream);
IWorksheet worksheet = workbook.Worksheets[1];
IPivotTable pivotTable = worksheet.PivotTables[0];

//Set BuiltInStyle
pivotTable.BuiltInStyle = PivotBuiltInStyles.PivotStyleDark12;

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "PivotTable_Style";
savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await workbook.SaveAsAsync(storageFile);

workbook.Close();
excelEngine.Dispose();
{% endhighlight %}

{% highlight asp.net core %}
ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
application.DefaultVersion = ExcelVersion.Excel2013;

FileStream fileStream = new FileStream("PivotTable.xlsx", FileMode.Open, FileAccess.Read);

IWorkbook workbook = application.Workbooks.Open(fileStream);
IWorksheet worksheet = workbook.Worksheets[1];
IPivotTable pivotTable = worksheet.PivotTables[0];

//Set BuiltInStyle
pivotTable.BuiltInStyle = PivotBuiltInStyles.PivotStyleDark12;

string fileName = "PivotTable_Style.xlsx";

//Saving the workbook as stream
FileStream stream = new FileStream(fileName, FileMode.Create, FileAccess.ReadWrite);
workbook.SaveAs(stream);

stream.Dispose();
workbook.Close();
excelEngine.Dispose();
{% endhighlight %}

{% highlight Xamarin %}
//Gets assembly
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
           
//Gets input Excel document from embedded resource collection
Stream inputStream = assembly.GetManifestResourceStream("PivotTable.PivotTable.xlsx");

ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open(inputStream);
IWorksheet worksheet = workbook.Worksheets[1];
IPivotTable pivotTable = worksheet.PivotTables[0];

//Set BuiltInStyle
pivotTable.BuiltInStyle = PivotBuiltInStyles.PivotStyleDark12;

//Saving the workbook as stream
MemoryStream outputStream = new MemoryStream();
workbook.SaveAs(outputStream);

workbook.Close();
excelEngine.Dispose();

string fileName = "PivotTable_Style.xlsx";

//Save the stream as Excel document and view the saved document
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    await DependencyService.Get<ISaveWindowsPhone>().SaveAndView(fileName, "application/msexcel", outputStream);
else
    DependencyService.Get<ISave>().SaveAndView(fileName, "application/msexcel", outputStream);

//Dispose the input and output stream instances
inputStream.Dispose();
outputStream.Dispose();
{% endhighlight %}
  {% endtabs %}  

The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer [SaveAndView](https://help.syncfusion.com/file-formats/xlsio/xamarin#saving-a-document) for respective code samples.

## Applying Pivot Table Filters 

The filtered data of a pivot table displays only the subset of data that meet the specified criteria. This can be achieved in XlsIO using the **IPivotFilters** interface.



### Applying Page Filters

The page field filter or report filter, filters the pivot table based on page field items. The following code example illustrates how to apply multiple filters to the page field items.

{% tabs %}  

{% highlight c# %}
//Set field axis to page
pivotTable.Fields[4].Axis = PivotAxisTypes.Page;

//Apply page field filter
IPivotField pageField = pivotTable.Fields[4];

//Select multiple items in page field to filter
pageField.Items[1].Visible = false;
pageField.Items[2].Visible = false; 

{% endhighlight %}

{% highlight vb %}
'Set field axis to page
pivotTable.Fields(4).Axis = PivotAxisTypes.Page

'Apply page field filter
Dim pageField As IPivotField = pivotTable.Fields(4)

'Select multiple items in page field to filter
pageField.Items(1).Visible = False
pageField.Items(2).Visible = False

{% endhighlight %}

{% highlight UWP %}
//Set field axis to page
pivotTable.Fields[4].Axis = PivotAxisTypes.Page;

//Apply page field filter
IPivotField pageField = pivotTable.Fields[4];

//Select multiple items in page field to filter
pageField.Items[1].Visible = false;
pageField.Items[2].Visible = false; 
{% endhighlight %}

{% highlight asp.net core %}
//Set field axis to page
pivotTable.Fields[4].Axis = PivotAxisTypes.Page;

//Apply page field filter
IPivotField pageField = pivotTable.Fields[4];

//Select multiple items in page field to filter
pageField.Items[1].Visible = false;
pageField.Items[2].Visible = false; 
{% endhighlight %}

{% highlight Xamarin %}
//Set field axis to page
pivotTable.Fields[4].Axis = PivotAxisTypes.Page;

//Apply page field filter
IPivotField pageField = pivotTable.Fields[4];

//Select multiple items in page field to filter
pageField.Items[1].Visible = false;
pageField.Items[2].Visible = false; 
{% endhighlight %}
  {% endtabs %}  

![](Working-with-Pivot-Tables_images/Working-with-Pivot-Tables_img1.jpeg)


### Applying Row or Column Filters

The row field and column field filters, filter the pivot table based on labels, values and items of fields. The following code example illustrates how to apply these filters to a pivot table.

**Label** **Filter** 

{% tabs %}  

{% highlight c# %}
//Apply row field filter
IPivotField rowField = pivotTable.Fields[2];

//Applying Label based row field filter
rowField.PivotFilters.Add(PivotFilterType.CaptionEqual, null, "Central", null);

{% endhighlight %}

{% highlight vb %}
'Apply row field filter
Dim rowField As IPivotField = pivotTable.Fields(2)

'Applying Label based row field filter
rowField.PivotFilters.Add(PivotFilterType.CaptionEqual, Nothing, "Central", Nothing)

{% endhighlight %}

{% highlight UWP %}
//Apply row field filter
IPivotField rowField = pivotTable.Fields[2];

//Applying Label based row field filter
rowField.PivotFilters.Add(PivotFilterType.CaptionEqual, null, "Central", null);
{% endhighlight %}

{% highlight asp.net core %}
//Apply row field filter
IPivotField rowField = pivotTable.Fields[2];

//Applying Label based row field filter
rowField.PivotFilters.Add(PivotFilterType.CaptionEqual, null, "Central", null);
{% endhighlight %}

{% highlight Xamarin %}
//Apply row field filter
IPivotField rowField = pivotTable.Fields[2];

//Applying Label based row field filter
rowField.PivotFilters.Add(PivotFilterType.CaptionEqual, null, "Central", null);
{% endhighlight %}
  {% endtabs %}  

![](Working-with-Pivot-Tables_images/Working-with-Pivot-Tables_img2.jpeg)


**Value** **Filter** 

{% tabs %}  

{% highlight c# %}
IPivotField field = pivotTable.Fields[2];

//Apply value filter
field.PivotFilters.Add(PivotFilterType.ValueLessThan, field, "1341", null);

{% endhighlight %}

{% highlight vb %}
'Apply row field filter
Dim field As IPivotField = pivotTable.Fields(2)

'Applying value filter
field.PivotFilters.Add(PivotFilterType. ValueLessThan, field, "1341", Nothing)

{% endhighlight %}

{% highlight UWP %}
IPivotField field = pivotTable.Fields[2];

//Apply value filter
field.PivotFilters.Add(PivotFilterType.ValueLessThan, field, "1341", null);
{% endhighlight %}

{% highlight asp.net core %}
IPivotField field = pivotTable.Fields[2];

//Apply value filter
field.PivotFilters.Add(PivotFilterType.ValueLessThan, field, "1341", null);
{% endhighlight %}

{% highlight Xamarin %}
IPivotField field = pivotTable.Fields[2];

//Apply value filter
field.PivotFilters.Add(PivotFilterType.ValueLessThan, field, "1341", null);
{% endhighlight %}
  {% endtabs %}  

![](Working-with-Pivot-Tables_images/Working-with-Pivot-Tables_img3.jpeg)



**Multiple** **filter**

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("PivotData.xlsx");
IWorksheet worksheet = workbook.Worksheets[0];
IWorksheet pivotSheet = workbook.Worksheets[1];

IPivotCache cache = workbook.PivotCaches.Add(worksheet["A1:H50"]);

IPivotTable pivotTable = pivotSheet.PivotTables.Add("PivotTable1", pivotSheet["A1"], cache);
pivotTable.Fields[4].Axis = PivotAxisTypes.Page;
pivotTable.Fields[2].Axis = PivotAxisTypes.Row;
pivotTable.Fields[6].Axis = PivotAxisTypes.Row;
pivotTable.Fields[3].Axis = PivotAxisTypes.Column;

IPivotField dataField = pivotSheet.PivotTables[0].Fields[5];
pivotTable.DataFields.Add(dataField, "Sum of Units", PivotSubtotalTypes.Sum);

//Apply page filter
pivotTable.Fields[4].Axis = PivotAxisTypes.Page;

IPivotField pageField = pivotTable.Fields[4];

pageField.Items[1].Visible = false;
pageField.Items[2].Visible = false;

//Apply label filter
IPivotField rowField = pivotTable.Fields[2];
rowField.PivotFilters.Add(PivotFilterType.CaptionEqual, null, "East", null);

//Apply item filter
IPivotField colField = pivotTable.Fields[3];
colField.Items[0].Visible = false;
colField.Items[1].Visible = false;

//Apply value filter
IPivotField field = pivotTable.Fields[2];
field.PivotFilters.Add(PivotFilterType.ValueLessThan, field, "1341", null);

pivotTable.BuiltInStyle = PivotBuiltInStyles.PivotStyleMedium2;

pivotSheet.Activate();

workbook.SaveAs("PivotTable.xlsx");

workbook.Close();

//No exception will be thrown if there are unsaved workbooks.
excelEngine.ThrowNotSavedOnDestroy = false;
excelEngine.Dispose();

{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()
Dim application As IApplication = excelEngine.Excel
application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("PivotData.xlsx")
Dim worksheet As IWorksheet = workbook.Worksheets(0)
Dim pivotSheet As IWorksheet = workbook.Worksheets(1)

Dim cache As IPivotCache = workbook.PivotCaches.Add(worksheet("A1:H50"))

Dim pivotTable As IPivotTable = pivotSheet.PivotTables.Add("PivotTable1", pivotSheet("A1"), cache)
pivotTable.Fields(4).Axis = PivotAxisTypes.Page
pivotTable.Fields(2).Axis = PivotAxisTypes.Row
pivotTable.Fields(6).Axis = PivotAxisTypes.Row
pivotTable.Fields(3).Axis = PivotAxisTypes.Column

Dim dataField As IPivotField = pivotSheet.PivotTables(0).Fields(5)
pivotTable.DataFields.Add(dataField, "Sum of Units", PivotSubtotalTypes.Sum)

'Applying page filter
pivotTable.Fields(4).Axis = PivotAxisTypes.Page

Dim pageField As IPivotField = pivotTable.Fields(4)

pageField.Items(1).Visible = False
pageField.Items(2).Visible = False

'Apply label filter
Dim rowField As IPivotField = pivotTable.Fields(2)
rowField.PivotFilters.Add(PivotFilterType.CaptionEqual, Nothing, "East", Nothing)

'Apply item filter
Dim colField As IPivotField = pivotTable.Fields(3)
colField.Items(0).Visible = False
colField.Items(1).Visible = False

'Applying value filter
Dim field As IPivotField = pivotTable.Fields(2)
field.PivotFilters.Add(PivotFilterType. ValueLessThan, field, "1341", Nothing)

pivotTable.BuiltInStyle = PivotBuiltInStyles.PivotStyleMedium2

pivotSheet.Activate()

workbook.SaveAs("PivotTable.xlsx")

workbook.Close()

'No exception will be thrown if there are unsaved workbooks.
excelEngine.ThrowNotSavedOnDestroy = False
excelEngine.Dispose()


{% endhighlight %}

{% highlight UWP %}
//Gets assembly
Assembly assembly = typeof(App).GetTypeInfo().Assembly;

//Gets input Excel document from embedded resource collection
Stream inputStream = assembly.GetManifestResourceStream("PivotTable.PivotData.xlsx");

ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = await application.Workbooks.OpenAsync(inputStream);
IWorksheet worksheet = workbook.Worksheets[0];
IWorksheet pivotSheet = workbook.Worksheets[1];

IPivotCache cache = workbook.PivotCaches.Add(worksheet["A1:H50"]);

IPivotTable pivotTable = pivotSheet.PivotTables.Add("PivotTable1", pivotSheet["A1"], cache);
pivotTable.Fields[4].Axis = PivotAxisTypes.Page;
pivotTable.Fields[2].Axis = PivotAxisTypes.Row;
pivotTable.Fields[6].Axis = PivotAxisTypes.Row;
pivotTable.Fields[3].Axis = PivotAxisTypes.Column;

IPivotField dataField = pivotSheet.PivotTables[0].Fields[5];
pivotTable.DataFields.Add(dataField, "Sum of Units", PivotSubtotalTypes.Sum);

//Apply page filter
pivotTable.Fields[4].Axis = PivotAxisTypes.Page;

IPivotField pageField = pivotTable.Fields[4];

pageField.Items[1].Visible = false;
pageField.Items[2].Visible = false;

//Apply label filter
IPivotField rowField = pivotTable.Fields[2];
rowField.PivotFilters.Add(PivotFilterType.CaptionEqual, null, "East", null);

//Apply item filter
IPivotField colField = pivotTable.Fields[3];
colField.Items[0].Visible = false;
colField.Items[1].Visible = false;

//Apply value filter
IPivotField field = pivotTable.Fields[2];
field.PivotFilters.Add(PivotFilterType.ValueLessThan, field, "1341", null);

pivotTable.BuiltInStyle = PivotBuiltInStyles.PivotStyleMedium2;

pivotSheet.Activate();

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "PivotTable";
savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await workbook.SaveAsAsync(storageFile);

workbook.Close();
excelEngine.Dispose();
{% endhighlight %}

{% highlight asp.net core %}
ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
FileStream fileStream = new FileStream("PivotData.xlsx", FileMode.Open, FileAccess.Read);

IWorkbook workbook = application.Workbooks.Open(fileStream);
IWorksheet worksheet = workbook.Worksheets[0];
IWorksheet pivotSheet = workbook.Worksheets[1];

IPivotCache cache = workbook.PivotCaches.Add(worksheet["A1:H50"]);

IPivotTable pivotTable = pivotSheet.PivotTables.Add("PivotTable1", pivotSheet["A1"], cache);
pivotTable.Fields[4].Axis = PivotAxisTypes.Page;
pivotTable.Fields[2].Axis = PivotAxisTypes.Row;
pivotTable.Fields[6].Axis = PivotAxisTypes.Row;
pivotTable.Fields[3].Axis = PivotAxisTypes.Column;

IPivotField dataField = pivotSheet.PivotTables[0].Fields[5];
pivotTable.DataFields.Add(dataField, "Sum of Units", PivotSubtotalTypes.Sum);

//Apply page filter
pivotTable.Fields[4].Axis = PivotAxisTypes.Page;

IPivotField pageField = pivotTable.Fields[4];

pageField.Items[1].Visible = false;
pageField.Items[2].Visible = false;

//Apply label filter
IPivotField rowField = pivotTable.Fields[2];
rowField.PivotFilters.Add(PivotFilterType.CaptionEqual, null, "East", null);

//Apply item filter
IPivotField colField = pivotTable.Fields[3];
colField.Items[0].Visible = false;
colField.Items[1].Visible = false;

//Apply value filter
IPivotField field = pivotTable.Fields[2];
field.PivotFilters.Add(PivotFilterType.ValueLessThan, field, "1341", null);

pivotTable.BuiltInStyle = PivotBuiltInStyles.PivotStyleMedium2;

pivotSheet.Activate();

string fileName = "PivotTable.xlsx";

//Saving the workbook as stream
FileStream stream = new FileStream(fileName, FileMode.Create, FileAccess.ReadWrite);
workbook.SaveAs(stream);

stream.Dispose();
workbook.Close();
excelEngine.Dispose();
{% endhighlight %}

{% highlight Xamarin %}
//Gets assembly
Assembly assembly = typeof(App).GetTypeInfo().Assembly;

//Gets input Excel document from embedded resource collection
Stream inputStream = assembly.GetManifestResourceStream("PivotTable.PivotData.xlsx");

ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open(inputStream);
IWorksheet worksheet = workbook.Worksheets[0];
IWorksheet pivotSheet = workbook.Worksheets[1];

IPivotCache cache = workbook.PivotCaches.Add(worksheet["A1:H50"]);

IPivotTable pivotTable = pivotSheet.PivotTables.Add("PivotTable1", pivotSheet["A1"], cache);
pivotTable.Fields[4].Axis = PivotAxisTypes.Page;
pivotTable.Fields[2].Axis = PivotAxisTypes.Row;
pivotTable.Fields[6].Axis = PivotAxisTypes.Row;
pivotTable.Fields[3].Axis = PivotAxisTypes.Column;

IPivotField dataField = pivotSheet.PivotTables[0].Fields[5];
pivotTable.DataFields.Add(dataField, "Sum of Units", PivotSubtotalTypes.Sum);

//Apply page filter
pivotTable.Fields[4].Axis = PivotAxisTypes.Page;

IPivotField pageField = pivotTable.Fields[4];

pageField.Items[1].Visible = false;
pageField.Items[2].Visible = false;

//Apply label filter
IPivotField rowField = pivotTable.Fields[2];
rowField.PivotFilters.Add(PivotFilterType.CaptionEqual, null, "East", null);

//Apply item filter
IPivotField colField = pivotTable.Fields[3];
colField.Items[0].Visible = false;
colField.Items[1].Visible = false;

//Apply value filter
IPivotField field = pivotTable.Fields[2];
field.PivotFilters.Add(PivotFilterType.ValueLessThan, field, "1341", null);

pivotTable.BuiltInStyle = PivotBuiltInStyles.PivotStyleMedium2;

pivotSheet.Activate();

//Saving the workbook as stream
MemoryStream outputStream = new MemoryStream();
workbook.SaveAs(outputStream);

workbook.Close();
excelEngine.Dispose();

string fileName = "PivotTable.xlsx";

//Save the stream as Excel document and view the saved document
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    await DependencyService.Get<ISaveWindowsPhone>().SaveAndView(fileName, "application/msexcel", outputStream);
else
    DependencyService.Get<ISave>().SaveAndView(fileName, "application/msexcel", outputStream);

//Dispose the input and output stream instances
inputStream.Dispose();
outputStream.Dispose();
{% endhighlight %}
  {% endtabs %}  

The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer [SaveAndView](https://help.syncfusion.com/file-formats/xlsio/xamarin#saving-a-document) for respective code samples.
  
## Applying Pivot Table Settings  

Excel provides various options through the PivotTableOptions dialog box to customize the appearance of the pivot table.

XlsIO supports these pivot table options using IPivotTableOptions interface to control various settings for the existing Pivot table.  To know more about various pivot table options, please refer **IPivotTableOptions** in API section. Following code illustrates how to access PivotTableOptions object. 

{% tabs %}  

{% highlight c# %}
//Enable ColumnHeaderCaption
IPivotTable pivotTable = worksheet.PivotTables[0];

IPivotTableOptions options = pivotTable.Options;



{% endhighlight %}

{% highlight vb %}
'Enable ColumnHeaderCaption
Dim pivotTable As IPivotTable = worksheet.PivotTables(0)

Dim options As IPivotTableOptions = pivotTable.Options



{% endhighlight %}

{% highlight UWP %}
//Enable ColumnHeaderCaption
IPivotTable pivotTable = worksheet.PivotTables[0];

IPivotTableOptions options = pivotTable.Options;
{% endhighlight %}

{% highlight asp.net core %}
//Enable ColumnHeaderCaption
IPivotTable pivotTable = worksheet.PivotTables[0];

IPivotTableOptions options = pivotTable.Options;
{% endhighlight %}
{% highlight Xamarin %}
//Enable ColumnHeaderCaption
IPivotTable pivotTable = worksheet.PivotTables[0];

IPivotTableOptions options = pivotTable.Options;
{% endhighlight %}
  {% endtabs %}  

### Show or Hide the Field List

To show or hide the pivot table field list pane, the ShowFieldList property is used as below.

{% tabs %}  

{% highlight c# %}
//Enable ShowFieldList
options.ShowFieldList = false;

{% endhighlight %}

{% highlight vb %}
'Enable ShowFieldList
options.ShowFieldList = False

{% endhighlight %}

{% highlight UWP %}
//Enable ShowFieldList
options.ShowFieldList = false;
{% endhighlight %}

{% highlight asp.net core %}
//Enable ShowFieldList
options.ShowFieldList = false;
{% endhighlight %}

{% highlight Xamarin %}
//Enable ShowFieldList
options.ShowFieldList = false;
{% endhighlight %}
  {% endtabs %}  

### Header Caption

The **RowHeaderCaption** and **ColumnHeaderCaption** properties allow to edit the respective pivot table headers. The header caption can be enabled or disabled through **DisplayFieldCaption** property.

{% tabs %}  

{% highlight c# %}
//Enable header captions
options.RowHeaderCaption = "Payment Dates";
options.ColumnHeaderCaption = "Payments"; 

{% endhighlight %}

{% highlight vb %}
'Enable header captions
options.RowHeaderCaption = "Payment Dates"
options.ColumnHeaderCaption = "Payments"

{% endhighlight %}

{% highlight UWP %}
//Enable header captions
options.RowHeaderCaption = "Payment Dates";
options.ColumnHeaderCaption = "Payments"; 
{% endhighlight %}

{% highlight asp.net core %}
//Enable header captions
options.RowHeaderCaption = "Payment Dates";
options.ColumnHeaderCaption = "Payments"; 
{% endhighlight %}

{% highlight Xamarin %}
//Enable header captions
options.RowHeaderCaption = "Payment Dates";
options.ColumnHeaderCaption = "Payments"; 
{% endhighlight %}
  {% endtabs %}  

### Grand Total

XlsIO provides an equivalent API to perform grand totals with simple properties as follows.

{% tabs %}  

{% highlight c# %}
//Enable GrandTotals
pivotTable.ColumnGrand = false;
pivotTable.RowGrand = true;

{% endhighlight %}

{% highlight vb %}
'Enable GrandTotals
pivotTable.ColumnGrand = False
pivotTable.RowGrand = False

{% endhighlight %}
{% highlight UWP %}
//Enable GrandTotals
pivotTable.ColumnGrand = false;
pivotTable.RowGrand = true;
{% endhighlight %}
{% highlight asp.net core %}
//Enable GrandTotals
pivotTable.ColumnGrand = false;
pivotTable.RowGrand = true;
{% endhighlight %}
{% highlight Xamarin %}
//Enable GrandTotals
pivotTable.ColumnGrand = false;
pivotTable.RowGrand = true;
{% endhighlight %}

  {% endtabs %}  

### Show/Hide Collapse Button

You can also show/hide the **Collapse** button that appears in the fields of the pivot table, when there exists more than one item in a field. The following code example illustrates how to do this.

{% tabs %}  

{% highlight c# %}
//Enable ShowDrillIndicators
pivotTable.ShowDrillIndicators = true;

{% endhighlight %}

{% highlight vb %}
'Enable ShowDrillIndicators
pivotTable.ShowDrillIndicators = True

{% endhighlight %}

{% highlight UWP %}
//Enable ShowDrillIndicators
pivotTable.ShowDrillIndicators = true;
{% endhighlight %}
{% highlight asp.net core %}
//Enable ShowDrillIndicators
pivotTable.ShowDrillIndicators = true;
{% endhighlight %}
{% highlight Xamarin %}
//Enable ShowDrillIndicators
pivotTable.ShowDrillIndicators = true;
{% endhighlight %}
  {% endtabs %}  

### Display Field Caption and Filter Option

The Filter buttons and field names in the pivot table can be shown or hidden, as in the following code.

{% tabs %}  

{% highlight c# %}
//Enable DisplayFieldCaption
pivotTable.DisplayFieldCaptions = true;

{% endhighlight %}

{% highlight vb %}
'Enable DisplayFieldCaption
pivotTable.DisplayFieldCaptions = True

{% endhighlight %}

{% highlight UWP %}
//Enable DisplayFieldCaption
pivotTable.DisplayFieldCaptions = true;
{% endhighlight %}
{% highlight asp.net core %}
//Enable DisplayFieldCaption
pivotTable.DisplayFieldCaptions = true;
{% endhighlight %}
{% highlight Xamarin %}
//Enable DisplayFieldCaption
pivotTable.DisplayFieldCaptions = true;
{% endhighlight %}
  {% endtabs %}  

### Repeating Row Label on Each Page

You can set the row label on each page, while printing, allowing users to view the header on each page.

{% tabs %}  

{% highlight c# %}
//Enable RepeatItemsOnEachPrintedPage
pivotTable.RepeatItemsOnEachPrintedPage = true;

{% endhighlight %}

{% highlight vb %}
'Enable RepeatItemsOnEachPrintedPage
pivotTable.RepeatItemsOnEachPrintedPage = True

{% endhighlight %}

{% highlight UWP %}
//Enable RepeatItemsOnEachPrintedPage
pivotTable.RepeatItemsOnEachPrintedPage = true;
{% endhighlight %}
{% highlight asp.net core %}
//Enable RepeatItemsOnEachPrintedPage
pivotTable.RepeatItemsOnEachPrintedPage = true;
{% endhighlight %}
{% highlight Xamarin %}
//Enable RepeatItemsOnEachPrintedPage
pivotTable.RepeatItemsOnEachPrintedPage = true;
{% endhighlight %}
  {% endtabs %}  

## Other Pivot Table Operations

### Adding Calculated Field in the existing Pivot Table

Calculated field is a special type of database field that perform calculations by using the contents of other fields in the pivot table with the given formula. The formula can contain operators and expressions as in other worksheet formulas. You can use constants and refer to data from the PivotTable.

You can read and create the Calculated Fields in the existing pivot table. The following are the Excel restrictions when using the formula.

* Formula cannot contain cell references or defined names and
* Formula cannot contains Worksheet functions that require cell references 
* Formula cannot use array functions.

The calculated field In XlsIO can be achieved with following code sample.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("PivotTable.xlsx");
IWorksheet sheet = workbook.Worksheets[1];
IPivotTable pivotTable = sheet.PivotTables[0];

//Add calculated field to the first pivot table
IPivotField field = pivotTable.CalculatedFields.Add("Percent", "Sales/Total*100");

workbook.SaveAs("PivotTableCalculate.xlsx");

workbook.Close();
excelEngine.ThrowNotSavedOnDestroy = false;
excelEngine.Dispose();

{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine
Dim application As IApplication = excelEngine.Excel
application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("PivotTable.xlsx")
Dim sheet As IWorksheet = workbook.Worksheets(1)
Dim pivotTable As IPivotTable = sheet.PivotTables(0)

' Add calculated field to the first pivot table
Dim field As IPivotField = pivotTable.CalculatedFields.Add("Percent", "Sales/Total*100")

workbook.SaveAs("PivotTableCalculate.xlsx")

workbook.Close()
excelEngine.ThrowNotSavedOnDestroy = False
excelEngine.Dispose()

{% endhighlight %}

{% highlight UWP %}
//Gets assembly
Assembly assembly = typeof(App).GetTypeInfo().Assembly;

//Gets input Excel document from embedded resource collection
Stream inputStream = assembly.GetManifestResourceStream("PivotTable.PivotTable.xlsx");

ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = await application.Workbooks.OpenAsync(inputStream);
IWorksheet sheet = workbook.Worksheets[1];
IPivotTable pivotTable = sheet.PivotTables[0];

//Add calculated field to the first pivot table
IPivotField field = pivotTable.CalculatedFields.Add("Percent", "Sales/Total*100");

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "PivotTableCalculate";
savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await workbook.SaveAsAsync(storageFile);

workbook.Close();
excelEngine.Dispose();
{% endhighlight %}
{% highlight asp.net core %}
ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
application.DefaultVersion = ExcelVersion.Excel2013;

FileStream fileStream = new FileStream("PivotTable.xlsx", FileMode.Open, FileAccess.Read);

IWorkbook workbook = application.Workbooks.Open(fileStream);
IWorksheet sheet = workbook.Worksheets[1];
IPivotTable pivotTable = sheet.PivotTables[0];

//Add calculated field to the first pivot table
IPivotField field = pivotTable.CalculatedFields.Add("Percent", "Sales/Total*100");

string fileName = "PivotTableCalculate.xlsx";

//Saving the workbook as stream
FileStream stream = new FileStream(fileName, FileMode.Create, FileAccess.ReadWrite);
workbook.SaveAs(stream);

stream.Dispose();
workbook.Close();
excelEngine.Dispose();
{% endhighlight %}
{% highlight Xamarin %}
//Gets assembly
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
           
//Gets input Excel document from embedded resource collection
Stream inputStream = assembly.GetManifestResourceStream("PivotTable.PivotTable.xlsx");

ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open(inputStream);
IWorksheet sheet = workbook.Worksheets[1];
IPivotTable pivotTable = sheet.PivotTables[0];

//Add calculated field to the first pivot table
IPivotField field = pivotTable.CalculatedFields.Add("Percent", "Sales/Total*100");

//Saving the workbook as stream
MemoryStream outputStream = new MemoryStream();
workbook.SaveAs(outputStream);

workbook.Close();
excelEngine.Dispose();

string fileName = "PivotTableCalculate.xlsx";

//Save the stream as Excel document and view the saved document
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    await DependencyService.Get<ISaveWindowsPhone>().SaveAndView(fileName, "application/msexcel", outputStream);
else
    DependencyService.Get<ISave>().SaveAndView(fileName, "application/msexcel", outputStream);

//Dispose the input and output stream instances
inputStream.Dispose();
outputStream.Dispose();
{% endhighlight %}
  {% endtabs %}  

The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer [SaveAndView](https://help.syncfusion.com/file-formats/xlsio/xamarin#saving-a-document) for respective code samples.

The formula can be also be set to the formula property of the IPivotField as below.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("PivotTable.xlsx");
IWorksheet sheet = workbook.Worksheets[0];
IPivotTable pivotTable = sheet.PivotTables[0];

//Add calculated field to the first pivot table
IPivotField field = pivotTable.CalculatedFields.Add("Percent", "Sales/Total*100");

//Set Field Formula
field.Formula = "Sales/Total*200";

workbook.SaveAs("PivotTable.xlsx");

workbook.Close();
excelEngine.ThrowNotSavedOnDestroy = false;
excelEngine.Dispose();

{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine
Dim application As IApplication = excelEngine.Excel
application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("PivotTable.xlsx")
Dim sheet As IWorksheet = workbook.Worksheets(0)
Dim pivotTable As IPivotTable = sheet.PivotTables(0)

Dim field As IPivotField = pivotTable.CalculatedFields.Add("Percent", "Sales/Total*100")

'Set Field Formula
field.Formula = "Sales/Total*200"

workbook.SaveAs("PivotTable.xlsx")

workbook.Close()
excelEngine.ThrowNotSavedOnDestroy = False
excelEngine.Dispose()



{% endhighlight %}

{% highlight UWP %}
//Gets assembly
Assembly assembly = typeof(App).GetTypeInfo().Assembly;

//Gets input Excel document from embedded resource collection
Stream inputStream = assembly.GetManifestResourceStream("PivotTable.PivotTable.xlsx");

ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = await application.Workbooks.OpenAsync(inputStream);
IWorksheet sheet = workbook.Worksheets[1];
IPivotTable pivotTable = sheet.PivotTables[0];

//Add calculated field to the first pivot table
IPivotField field = pivotTable.CalculatedFields.Add("Percent", "Sales/Total*100");

//Set Field Formula
field.Formula = "Sales/Total*200";

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "PivotTableCalculate";
savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await workbook.SaveAsAsync(storageFile);

workbook.Close();
excelEngine.Dispose();
{% endhighlight %}

{% highlight asp.net core %}
ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
application.DefaultVersion = ExcelVersion.Excel2013;

FileStream fileStream = new FileStream("PivotTable.xlsx", FileMode.Open, FileAccess.Read);

IWorkbook workbook = application.Workbooks.Open(fileStream);
IWorksheet sheet = workbook.Worksheets[1];
IPivotTable pivotTable = sheet.PivotTables[0];

//Add calculated field to the first pivot table
IPivotField field = pivotTable.CalculatedFields.Add("Percent", "Sales/Total*100");

//Set Field Formula
field.Formula = "Sales/Total*200";

string fileName = "PivotTableCalculate.xlsx";

//Saving the workbook as stream
FileStream stream = new FileStream(fileName, FileMode.Create, FileAccess.ReadWrite);
workbook.SaveAs(stream);

stream.Dispose();
workbook.Close();
excelEngine.Dispose();
{% endhighlight %}
{% highlight Xamarin %}
//Gets assembly
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
           
//Gets input Excel document from embedded resource collection
Stream inputStream = assembly.GetManifestResourceStream("PivotTable.PivotTable.xlsx");

ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open(inputStream);
IWorksheet sheet = workbook.Worksheets[1];
IPivotTable pivotTable = sheet.PivotTables[0];

//Add calculated field to the first pivot table
IPivotField field = pivotTable.CalculatedFields.Add("Percent", "Sales/Total*100");

//Set Field Formula
field.Formula = "Sales/Total*200";

//Saving the workbook as stream
MemoryStream outputStream = new MemoryStream();
workbook.SaveAs(outputStream);

workbook.Close();
excelEngine.Dispose();

string fileName = "PivotTableCalculate.xlsx";

//Save the stream as Excel document and view the saved document
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    await DependencyService.Get<ISaveWindowsPhone>().SaveAndView(fileName, "application/msexcel", outputStream);
else
    DependencyService.Get<ISave>().SaveAndView(fileName, "application/msexcel", outputStream);

//Dispose the input and output stream instances
inputStream.Dispose();
outputStream.Dispose();
{% endhighlight %}
  {% endtabs %}  

The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer [SaveAndView](https://help.syncfusion.com/file-formats/xlsio/xamarin#saving-a-document) for respective code samples.
 
### Layout the Pivot Table as Excel

A Pivot Table can be created similar to Excel layout. 

The following code example illustrates how to enable Essential XlsIO to layout the pivot table like Excel. 

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("PivotData.xlsx");
IWorksheet worksheet = workbook.Worksheets[0];
IWorksheet pivotSheet = workbook.Worksheets[1];

IPivotCache cache = workbook.PivotCaches.Add(worksheet["A1:H50"]);

IPivotTable pivotTable = pivotSheet.PivotTables.Add("PivotTable1", pivotSheet["A1"], cache);
pivotTable.Fields[4].Axis = PivotAxisTypes.Page;
pivotTable.Fields[2].Axis = PivotAxisTypes.Row;
pivotTable.Fields[6].Axis = PivotAxisTypes.Row;
pivotTable.Fields[3].Axis = PivotAxisTypes.Column;

IPivotField dataField = pivotSheet.PivotTables[0].Fields[5];
pivotTable.DataFields.Add(dataField, "Sum of Units", PivotSubtotalTypes.Sum);

pivotTable.BuiltInStyle = PivotBuiltInStyles.PivotStyleDark12;

//The following code sample must be included to XlsIO layout the pivot table like Excel
pivotTable.Layout();

workbook.SaveAs("PivotTable.xlsx");

workbook.Close();
excelEngine.ThrowNotSavedOnDestroy = false;
excelEngine.Dispose();

{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine
Dim application As IApplication = excelEngine.Excel
application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("PivotData.xlsx")
Dim worksheet As IWorksheet = workbook.Worksheets(0)
Dim pivotSheet As IWorksheet = workbook.Worksheets(1)

Dim cache As IPivotCache = workbook.PivotCaches.Add(worksheet("A1:H50"))

Dim pivotTable As IPivotTable = pivotSheet.PivotTables.Add("PivotTable1", pivotSheet("A1"), cache)
pivotTable.Fields(4).Axis = PivotAxisTypes.Page
pivotTable.Fields(2).Axis = PivotAxisTypes.Row
pivotTable.Fields(6).Axis = PivotAxisTypes.Row
pivotTable.Fields(3).Axis = PivotAxisTypes.Column

Dim dataField As IPivotField = pivotSheet.PivotTables(0).Fields(5)
pivotTable.DataFields.Add(dataField, "Sum of Units", PivotSubtotalTypes.Sum)

pivotTable.BuiltInStyle = PivotBuiltInStyles.PivotStyleDark12

'The following code sample must be included to XlsIO layout the pivot table like Excel
pivotTable.Layout()

workbook.SaveAs("PivotTable.xlsx")

workbook.Close()
excelEngine.ThrowNotSavedOnDestroy = False
excelEngine.Dispose()

{% endhighlight %}

{% highlight UWP %}
//XlsIO supports layout pivot table in Windows Forms,WPF,ASP.NET and ASP.NET MVC platforms alone.
{% endhighlight %}
{% highlight asp.net core %}
//XlsIO supports layout pivot table in Windows Forms,WPF,ASP.NET and ASP.NET MVC platforms alone.
{% endhighlight %}
{% highlight Xamarin %}
//XlsIO supports layout pivot table in Windows Forms,WPF,ASP.NET and ASP.NET MVC platforms alone.
{% endhighlight %}
  {% endtabs %}  

