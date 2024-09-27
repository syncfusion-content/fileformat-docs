---
title: Working with Pivot Tables | Excel library | Syncfusion
description: In this section, you can learn how to create and use pivot tables operations in Excel document using XlsIO
platform: file-Formats
control: XlsIO
documentation: UG
---
# Working with Pivot Tables

You can easily arrange and summarize complex data in a [Pivot Table](https://support.microsoft.com/en-gb/office/create-a-pivottable-in-excel-74ce8afc-2446-4816-80ee-20ca7fb71793?redirectSourcePath=%252fen-us%252farticle%252fPivotTable-I-Get-started-with-PivotTable-reports-in-Excel-2007-bfe774d3-3e20-46f7-b6a3-f7984855d665). 

Creation and manipulation of pivot tables is supported in Excel 2007 and later formats (i.e., *.xlsx), along with preserving existing pivot tables.

N> Creation and manipulation of pivot tables is not supported in Excel 2003 format (i.e., *.xls). It is only possible to preserve the existing pivot table in this format.

## Create a pivot table

Steps to create a simple pivot table: 

* Add pivot cache
* Add pivot table
* Add row and column fields
* Add data fields

Pivot tables do not take data directly from the source data, but take from the pivot cache that memorizes a snapshot of the data. The [IPivotCache](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IPivotCache.html) interface caches the data that needs to be summarized. 

The data in worksheet is added to the pivot cache as follows.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Create Pivot cache with the given data range
IPivotCache cache = workbook.PivotCaches.Add(worksheet["A1:H50"]);
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Create Pivot cache with the given data range
IPivotCache cache = workbook.PivotCaches.Add(worksheet["A1:H50"]);
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Create Pivot cache with the given data range
Dim cache As IPivotCache = workbook.PivotCaches.Add(worksheet("A1:H50"))
{% endhighlight %}
{% endtabs %}  

[IPivotTable](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IPivotTable.html) represents a single pivot table object created from the cache. It has properties that customizes the pivot table. The following code creates a blank pivot table. 

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Create "PivotTable1" with the cache at the specified range
IPivotTable pivotTable = worksheet.PivotTables.Add("PivotTable1", worksheet["A1"], cache);
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Create "PivotTable1" with the cache at the specified range
IPivotTable pivotTable = worksheet.PivotTables.Add("PivotTable1", worksheet["A1"], cache);
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Create "PivotTable1" with the cache at the specified range
Dim pivotTable As IPivotTable = worksheet.PivotTables.Add("PivotTable1", worksheet("A1"), cache)
{% endhighlight %}
{% endtabs %}  

The pivot table should be populated with required fields. The [IPivotField](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IPivotField.html) represents a single field in the pivot table, which includes row, column, and data field axes. 

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Add Pivot table fields (row and column fields)
pivotTable.Fields[2].Axis = PivotAxisTypes.Row;
pivotTable.Fields[6].Axis = PivotAxisTypes.Row;
pivotTable.Fields[3].Axis = PivotAxisTypes.Column;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Add Pivot table fields (row and column fields)
pivotTable.Fields[2].Axis = PivotAxisTypes.Row;
pivotTable.Fields[6].Axis = PivotAxisTypes.Row;
pivotTable.Fields[3].Axis = PivotAxisTypes.Column;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Add Pivot table fields (row and column fields)
pivotTable.Fields(2).Axis = PivotAxisTypes.Row
pivotTable.Fields(6).Axis = PivotAxisTypes.Row
pivotTable.Fields(3).Axis = PivotAxisTypes.Column
{% endhighlight %}
{% endtabs %}  

The [IPivotDataFields](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IPivotDataFields.html) represents a collection of data fields in the pivot table. The data field is added with the required subtotal function using the [PivotSubtotalTypes](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.PivotSubtotalTypes.html) enumeration. The following code explains how to configure a pivot field as a data field.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Add data field
IPivotField field = pivotTable.Fields[5];
pivotTable.DataFields.Add(field, "Sum", PivotSubtotalTypes.Sum);
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Add data field
IPivotField field = pivotTable.Fields[5];
pivotTable.DataFields.Add(field, "Sum", PivotSubtotalTypes.Sum);
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Add data field
Dim field As IPivotField = pivotTable.Fields(5)
pivotTable.DataFields.Add(field, "Sum", PivotSubtotalTypes.Sum)
{% endhighlight %}
{% endtabs %}  

The following code snippet illustrates how to create a pivot table with existing data in the worksheet using XlsIO.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream fileStream = new FileStream("PivotData.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];
  IWorksheet pivotSheet = workbook.Worksheets[1];

  //Create Pivot cache with the given data range
  IPivotCache cache = workbook.PivotCaches.Add(worksheet["A1:H50"]);

  //Create "PivotTable1" with the cache at the specified range
  IPivotTable pivotTable = pivotSheet.PivotTables.Add("PivotTable1", pivotSheet["A1"], cache);

  //Add Pivot table fields (Row and Column fields)
  pivotTable.Fields[2].Axis = PivotAxisTypes.Row;
  pivotTable.Fields[6].Axis = PivotAxisTypes.Row;
  pivotTable.Fields[3].Axis = PivotAxisTypes.Column;

  //Add data field
  IPivotField field = pivotTable.Fields[5];
  pivotTable.DataFields.Add(field, "Sum", PivotSubtotalTypes.Sum);

  string fileName = "PivotTable.xlsx";
  //Saving the workbook as stream
  FileStream stream = new FileStream(fileName, FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("PivotData.xlsx");
  IWorksheet worksheet = workbook.Worksheets[0];
  IWorksheet pivotSheet = workbook.Worksheets[1];

  //Create Pivot cache with the given data range
  IPivotCache cache = workbook.PivotCaches.Add(worksheet["A1:H50"]);

  //Create "PivotTable1" with the cache at the specified range
  IPivotTable pivotTable = pivotSheet.PivotTables.Add("PivotTable1", pivotSheet["A1"], cache);

  //Add Pivot table fields (Row and Column fields)
  pivotTable.Fields[2].Axis = PivotAxisTypes.Row;
  pivotTable.Fields[6].Axis = PivotAxisTypes.Row;
  pivotTable.Fields[3].Axis = PivotAxisTypes.Column;

  //Add data field
  IPivotField field = pivotTable.Fields[5];
  pivotTable.DataFields.Add(field, "Sum", PivotSubtotalTypes.Sum);
  
  workbook.SaveAs("PivotTable.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013

  Dim workbook As IWorkbook = application.Workbooks.Open("PivotData.xlsx")
  Dim worksheet As IWorksheet = workbook.Worksheets(0)
  Dim pivotSheet As IWorksheet = workbook.Worksheets(1)

  'Create Pivot cache with the given data range
  Dim cache As IPivotCache = workbook.PivotCaches.Add(worksheet("A1:H50"))

  'Create "PivotTable1" with the cache at the specified range
  Dim pivotTable As IPivotTable = pivotSheet.PivotTables.Add("PivotTable1", pivotSheet("A1"), cache)

  'Add Pivot table fields (Row and Column fields)
  pivotTable.Fields(2).Axis = PivotAxisTypes.Row
  pivotTable.Fields(6).Axis = PivotAxisTypes.Row
  pivotTable.Fields(3).Axis = PivotAxisTypes.Column

  'Add data field
  Dim field As IPivotField = pivotTable.Fields(5)
  pivotTable.DataFields.Add(field, "Sum", PivotSubtotalTypes.Sum)

  workbook.SaveAs("PivotTable.xlsx")
End Using
{% endhighlight %}
{% endtabs %}  

A complete working example to create a pivot table in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Pivot%20Table/Create%20Pivot%20Table).

## Editing and formatting a pivot table

A pivot table can be accessed from the [IPivotTables](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IPivotTables.html) interface that have the collection of pivot tables in the worksheet. You can modify the pivot table format or pivot cell format using [IPivotTable](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IPivotTable.html) properties and methods.

### Pivot Table Formatting

XlsIO supports 85 built-in styles of Microsoft Excel used to create a table with rich formatting using the [PivotBuiltInStyles](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.PivotBuiltInStyles.html) property as follows.

The following code snippet illustrates how to apply built-in style to pivot table

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
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
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("PivotTable.xlsx");
  IWorksheet worksheet = workbook.Worksheets[1];
  IPivotTable pivotTable = worksheet.PivotTables[0];

  //Set BuiltInStyle
  pivotTable.BuiltInStyle = PivotBuiltInStyles.PivotStyleDark12;

  workbook.SaveAs("PivotTable_Style.xlsx");

  //No exception will be thrown if there are unsaved workbooks
  excelEngine.ThrowNotSavedOnDestroy = false;
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("PivotTable.xlsx")
  Dim sheet As IWorksheet = workbook.Worksheets(1)
  Dim pivotTable As IPivotTable = sheet.PivotTables(0)

  'Set BuiltInStyle
  pivotTable.BuiltInStyle = PivotBuiltInStyles.PivotStyleDark12

  workbook.SaveAs("PivotTable_Style.xlsx")

  'No exception will be thrown if there are unsaved workbooks
  excelEngine.ThrowNotSavedOnDestroy = False
End Using
{% endhighlight %}
{% endtabs %} 

A complete working example to format a pivot table in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Pivot%20Table/Format%20Pivot%20Table). 

### Pivot Cell Formatting

When you apply the cell formatting to pivot table cells, Microsoft Excel maintains the formatting information in pivot table and shows the cell formatting on pivot table cells from that pivot formats. XlsIO supports to apply cell formatting to pivot table range cells. You can apply all the cell formatting using [IPivotTable](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IPivotTable.html) [GetCellFormat](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IPivotTable.html#Syncfusion_XlsIO_IPivotTable_GetCellFormat_System_String_) method and [IPivotCellFormat](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IPivotCellFormat.html) interface.

The following code snippet illustrates how to apply cell formatting to pivot table cells.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream fileStream = new FileStream("PivotTable.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  IPivotTable pivotTable = worksheet.PivotTables[0];
  //Get the cell format for "A1" pivot range.
  IPivotCellFormat cellFormat = pivotTable.GetCellFormat("A3:C4");
  cellFormat.BackColor = ExcelKnownColors.Green;

  string fileName = "PivotFormat.xlsx";
  //Saving the workbook as stream
  FileStream stream = new FileStream(fileName, FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine engine = new ExcelEngine())
{
  IApplication application = engine.Excel;
  IWorkbook workbook = application.Workbooks.Open("PivotTable.xlsx");
  IWorksheet worksheet = workbook.Worksheets[0];

  IPivotTable pivotTable = worksheet.PivotTables[0];
  //Get the cell format for "A1" pivot range.
  IPivotCellFormat cellFormat = pivotTable.GetCellFormat("A3:C4");
  cellFormat.BackColor = ExcelKnownColors.Green;

  workbook.SaveAs("PivotFormat.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  Dim workbook As IWorkbook = application.Workbooks.Open("PivotTable.xlsx")
  Dim pivotSheet As IWorksheet = workbook.Worksheets(0)

  Dim pivotTable As IPivotTable = worksheet.PivotTables(0)
  'Get the cell format for "A1" pivot range.
  Dim cellFormat As IPivotCellFormat = pivotTable.GetCellFormat("A3:C4")
  cellFormat.BackColor = ExcelKnownColors.Green

  workbook.SaveAs("PivotFormat.xlsx")
End Using
{% endhighlight %}
{% endtabs %}

A complete working example to format a pivot cell in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Pivot%20Table/Format%20Pivot%20Cell). 

The following screenshot represents the input template of pivot table inline formatting.

<img src="working-with-pivot-tables_images/file-formats-xlsio-inline-formatting-template.png" alt="Working with Pivot Tables in File Formats XLSIO Inline Formatting Template" width="100%" Height="Auto"/>

The following screenshot represents the generated Excel file with pivot table inline formatting in XlsIO.

<img src="working-with-pivot-tables_images/file-formats-xlsio-inline-formatting-file.png" alt="Working with Pivot Tables in File Formats XLSIO Inline Formatting File" width="100%" Height="Auto"/>

## Refresh a pivot table
When you update the pivot table data source, you should refresh the pivot table manually to load the new data source into it. Essential XlsIO supports this refreshing of pivot table data source through [IsRefreshOnLoad](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.Implementation.PivotTables.PivotCacheImpl.html#Syncfusion_XlsIO_Implementation_PivotTables_PivotCacheImpl_IsRefreshOnLoad) property of [PivotCacheImpl](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.Implementation.PivotTables.PivotCacheImpl.html).

The following code shows how to dynamically refresh the data in a pivot table. In prior:

* Create the pivot table using Excel GUI.
* Specify the named range to be the data source of the pivot table.
* Make sure that the **Refresh on Open** option of the pivot table is selected.
* Dynamically refresh the data in the named range.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
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
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("PivotTable.xlsx");
  IWorksheet pivotSheet = workbook.Worksheets[0];

  //Change the range values that the Pivot Tables range refers to
  workbook.Names["PivotRange"].RefersToRange = pivotSheet.Range["A1:D27"];

  workbook.SaveAs("PivotTable_DynamicRange.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("PivotTable.xlsx")
  Dim pivotSheet As IWorksheet = workbook.Worksheets(0)

  'Change the range values that the Pivot Tables range refers to
  workbook.Names("PivotRange").RefersToRange = pivotSheet.Range("A1:D27")

  workbook.SaveAs("PivotTable_DynamicRange.xlsx")
End Using
{% endhighlight %}
{% endtabs %} 

A complete working example to refresh a pivot table dynamically in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Pivot%20Table/Dynamic%20Refresh).  

The following code snippet illustrates how to refresh the pivot table after update the cell value in pivot data source.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Updating a new value in the pivot data
  worksheet.Range["C2"].Value = "250";

  //Accessing the pivot table 
  IPivotTable pivotTable = worksheet.PivotTables[0];
  PivotTableImpl pivotTableImpl = pivotTable as PivotTableImpl;

  //Refreshing pivot cache to update the pivot table
  pivotTableImpl.Cache.IsRefreshOnLoad = true;

  //Saving the workbook as stream
  FileStream stream = new FileStream("Output.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
  IWorksheet worksheet = workbook.Worksheets[0];

  //Updating a new value in the pivot data
  worksheet.Range["C2"].Value = "250";

  //Accessing the pivot table 
  IPivotTable pivotTable = worksheet.PivotTables[0];
  PivotTableImpl pivotTableImpl = pivotTable as PivotTableImpl;

  //Refreshing pivot cache to update the pivot table
  pivotTableImpl.Cache.IsRefreshOnLoad = true;

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Updating a new value in the pivot data
  worksheet.Range("C2").Value = "250"

  'Accessing the pivot table
  Dim pivotTable As IPivotTable = worksheet.PivotTables(0)
  Dim pivotTableImpl As PivotTableImpl = CType(pivotTable, PivotTableImpl)

  'Refreshing pivot cache to update the pivot table
  pivotTableImpl.Cache.IsRefreshOnLoad = True

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}
{% endtabs %}

A complete working example to refresh a pivot table in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Pivot%20Table/Refresh%20Pivot%20Table). 

## Pivot table Layout

When you create pivot table in XlsIO, the pivot values are not set in the worksheet cells. Pivot table layout option set the pivot values to worksheet cells. XlsIO supports the layout option for all three pivot table types.

The following code snippet illustrates how to layout the pivot table.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream fileStream = new FileStream("PivotTable.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  IPivotTable pivotTable = worksheet.PivotTables[0];
  //Layout the pivot table.
  pivotTable.Layout();

  string fileName = "PivotTable_Layout.xlsx";
  //Saving the workbook as stream
  FileStream stream = new FileStream(fileName, FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  IWorkbook workbook = application.Workbooks.Open("PivotTable.xlsx");
  IWorksheet worksheet = workbook.Worksheets[1];

  IPivotTable pivotTable = worksheet.PivotTables[0];
  //Layout the pivot table.
  pivotTable.Layout();

  workbook.SaveAs("PivotTable_Layout.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  Dim workbook As IWorkbook = application.Workbooks.Open("PivotTable.xlsx")
  Dim pivotSheet As IWorksheet = workbook.Worksheets(0)

  Dim pivotTable As IPivotTable = worksheet.PivotTables(0)
  'Layout the pivot table.
  pivotTable.Layout()

  workbook.SaveAs("PivotTable_Layout.xlsx")
End Using
{% endhighlight %}
{% endtabs %}

A complete working example to layout a pivot table in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Pivot%20Table/Pivot%20Layout). 

The following screenshots represents the generated Excel file with pivot table layout in XlsIO.

Compact layout:

<img src="working-with-pivot-tables_images/file-formats-xlsio-compact-layout.png" alt="Working with Pivot Tables in File Formats XLSIO Compact Layout" width="100%" Height="Auto"/>

Outline layout:

<img src="working-with-pivot-tables_images/file-formats-xlsio-outline-layout.png" alt="Working with Pivot Tables in File Formats XLSIO Outline Layout" width="100%" Height="Auto"/>

Tabular layout:

<img src="working-with-pivot-tables_images/file-formats-xlsio-tabular-layout.png" alt="Working with Pivot Tables in File Formats XLSIO Tabular Layout" width="100%" Height="Auto"/>

### Pivot table row layout

The [PivotTableRowLayout](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.PivotTableRowLayout.html) enumeration can be used to change the pivot table row layout as Compact or Outline or Tabular as below.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  FileStream fileStream = new FileStream("PivotTable.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[1];
  IPivotTable pivotTable = worksheet.PivotTables[0];

  //Set PivotTableRowLayout
  pivotTable.Options.RowLayout = PivotTableRowLayout.Tabular;

  string fileName = "PivotTable_RowLayout.xlsx";

  //Saving the workbook as stream
  FileStream stream = new FileStream(fileName, FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  IWorkbook workbook = application.Workbooks.Open("PivotTable.xlsx");
  IWorksheet worksheet = workbook.Worksheets[1];
  IPivotTable pivotTable = worksheet.PivotTables[0];

  //Set PivotTableRowLayout
  pivotTable.Options.RowLayout = PivotTableRowLayout.Tabular;

  workbook.SaveAs("PivotTable_RowLayout.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013

  Dim workbook As IWorkbook = application.Workbooks.Open("PivotTable.xlsx")
  Dim sheet As IWorksheet = workbook.Worksheets(1)
  Dim pivotTable As IPivotTable = sheet.PivotTables(0)

  'Set PivotTableRowLayout
  pivotTable.Options.RowLayout = PivotTableRowLayout.Tabular

  workbook.SaveAs("PivotTable_RowLayout.xlsx")
End Using
{% endhighlight %}
{% endtabs %}

### Pivot table with classic layout

For classic layout, you can set the [ShowGridDropZone](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.Implementation.PivotTables.PivotTableOptions.html#Syncfusion_XlsIO_Implementation_PivotTables_PivotTableOptions_ShowGridDropZone) property to true as below.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  FileStream fileStream = new FileStream("PivotTable.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[1];
  IPivotTable pivotTable = worksheet.PivotTables[0];

  //Set PivotTableRowLayout
  pivotTable.Options.RowLayout = PivotTableRowLayout.Tabular;

  //Set classic layout
  (pivotTable.Options as PivotTableOptions).ShowGridDropZone = true; 

  string fileName = "PivotTable_ClassicLayout.xlsx";

  //Saving the workbook as stream
  FileStream stream = new FileStream(fileName, FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  IWorkbook workbook = application.Workbooks.Open("PivotTable.xlsx");
  IWorksheet worksheet = workbook.Worksheets[1];
  IPivotTable pivotTable = worksheet.PivotTables[0];

  //Set PivotTableRowLayout
  pivotTable.Options.RowLayout = PivotTableRowLayout.Tabular;

  //Set classic layout
  (pivotTable.Options as PivotTableOptions).ShowGridDropZone = true; 

  workbook.SaveAs("PivotTable_ClassicLayout.xlsx");

  //No exception will be thrown if there are unsaved workbooks
  excelEngine.ThrowNotSavedOnDestroy = false;
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013

  Dim workbook As IWorkbook = application.Workbooks.Open("PivotTable.xlsx")
  Dim sheet As IWorksheet = workbook.Worksheets(1)
  Dim pivotTable As IPivotTable = sheet.PivotTables(0)

  'Set PivotTableRowLayout
  pivotTable.Options.RowLayout = PivotTableRowLayout.Tabular

  'Set classic layout
  (TryCast(pivotTable.Options, PivotTableOptions)).ShowGridDropZone = True

  workbook.SaveAs("PivotTable_ClassicLayout.xlsx")
End Using
{% endhighlight %}
{% endtabs %}

A complete working example to layout a pivot table classically in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Pivot%20Table/Classic%20Layout). 

## Expand or collapse rows in pivot table

Essential XlsIO allows you to expand and collapse the [PivotFieldItems](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IPivotFieldItems.html) or simply the pivot table rows using [IsHiddenDetails](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.Implementation.PivotTables.PivotItemOptions.html#Syncfusion_XlsIO_Implementation_PivotTables_PivotItemOptions_IsHiddenDetails) of [PivotItemOptions](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.Implementation.PivotTables.PivotItemOptions.html).

Refer the following complete code snippets.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Create pivot cache with the given data range
  IPivotCache cache = workbook.PivotCaches.Add(worksheet["A1:C13"]);

  //Create "PivotTable1" with the cache at the specified range
  IPivotTable pivotTable = worksheet.PivotTables.Add("PivotTable1", worksheet["E1"], cache);

  //Add pivot table fields (Row and Column fields)
  pivotTable.Fields[0].Axis = PivotAxisTypes.Row;
  pivotTable.Fields[1].Axis = PivotAxisTypes.Row;

  //Add data field
  IPivotField field = pivotTable.Fields[2];
  pivotTable.DataFields.Add(field, "Sum", PivotSubtotalTypes.Sum);

  //Initialize PivotItemOptions
  PivotItemOptions options = new PivotItemOptions();
  options.IsHiddenDetails = false;

  //Collapsing the first and second items of the first pivot field using PivotItemOptions
  (pivotTable.Fields[0] as PivotFieldImpl).AddItemOption(0, options);
  (pivotTable.Fields[0] as PivotFieldImpl).AddItemOption(1, options);

  //Saving the workbook as stream
  FileStream stream = new FileStream("Output.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
  IWorksheet worksheet = workbook.Worksheets[0];

  //Create pivot cache with the given data range
  IPivotCache cache = workbook.PivotCaches.Add(worksheet["A1:C13"]);

  //Create "PivotTable1" with the cache at the specified range
  IPivotTable pivotTable = worksheet.PivotTables.Add("PivotTable1", worksheet["E1"], cache);

  //Add pivot table fields (Row and Column fields)
  pivotTable.Fields[0].Axis = PivotAxisTypes.Row;
  pivotTable.Fields[1].Axis = PivotAxisTypes.Row;

  //Add data field
  IPivotField field = pivotTable.Fields[2];
  pivotTable.DataFields.Add(field, "Sum", PivotSubtotalTypes.Sum);

  //Initialize PivotItemOptions
  PivotItemOptions options = new PivotItemOptions();
  options.IsHiddenDetails = false;

  //Collapsing the first and second items of the first pivot field using PivotItemOptions
  (pivotTable.Fields[0] as PivotFieldImpl).AddItemOption(0, options);
  (pivotTable.Fields[0] as PivotFieldImpl).AddItemOption(1, options);

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Create pivot cache with the given data range
  Dim cache As IPivotCache = workbook.PivotCaches.Add(worksheet("A1:C13"))

  'Create "PivotTable1" with the cache at the specified range
  Dim pivotTable As IPivotTable = worksheet.PivotTables.Add("PivotTable1", worksheet("E1"), cache)

  'Add pivot table fields (Row and Column fields)
  pivotTable.Fields(0).Axis = PivotAxisTypes.Row
  pivotTable.Fields(1).Axis = PivotAxisTypes.Row

  'Add data field
  Dim field As IPivotField = pivotTable.Fields(2)
  pivotTable.DataFields.Add(field, "Sum", PivotSubtotalTypes.Sum)

  'Initialize PivotItemOptions
  Dim options As PivotItemOptions = New PivotItemOptions
  options.IsHiddenDetails = False

  'Collapsing the first and second items of the first pivot field using PivotItemOptions
  CType(pivotTable.Fields(0), PivotFieldImpl).AddItemOption(0, options)
  CType(pivotTable.Fields(0), PivotFieldImpl).AddItemOption(1, options)

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}
{% endtabs %}

A complete working example to expand or collapse rows in pivot table in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Pivot%20Table/Expand%20or%20Collapse%20Pivot%20Rows). 

## Applying pivot table filters 

The filtered data of a pivot table displays only the subset of data that meets the specified criteria. This can be achieved in XlsIO using the [IPivotFilters](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IPivotFilters.html) interface.

### Applying page filters

The page field filter or report filter can filter the pivot table based on the page field items. The following code snippet illustrates how to apply multiple filters to the page field items.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Set field axis to page
pivotTable.Fields[4].Axis = PivotAxisTypes.Page;

//Apply page field filter
IPivotField pageField = pivotTable.Fields[4];

//Select multiple items in page field to filter
pageField.Items[1].Visible = false;
pageField.Items[2].Visible = false; 
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Set field axis to page
pivotTable.Fields[4].Axis = PivotAxisTypes.Page;

//Apply page field filter
IPivotField pageField = pivotTable.Fields[4];

//Select multiple items in page field to filter
pageField.Items[1].Visible = false;
pageField.Items[2].Visible = false;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Set field axis to page
pivotTable.Fields(4).Axis = PivotAxisTypes.Page

'Apply page field filter
Dim pageField As IPivotField = pivotTable.Fields(4)

'Select multiple items in page field to filter
pageField.Items(1).Visible = False
pageField.Items(2).Visible = False
{% endhighlight %}
{% endtabs %}  

<img src="working-with-pivot-tables_images/file-formats-xlsio-page-filters.jpeg" alt="Working with Pivot Tables in File Formats XLSIO Applying Page Filters" width="100%" Height="Auto"/>

### Applying row or column filters

The row and column field filters can filter the pivot table based on labels, values, and items of the fields. The following code example illustrates how to apply these filters to a pivot table.

**Label** **Filter** 

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Apply row field filter
IPivotField rowField = pivotTable.Fields[2];

//Applying Label based row field filter
rowField.PivotFilters.Add(PivotFilterType.CaptionEqual, null, "Central", null);
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Apply row field filter
IPivotField rowField = pivotTable.Fields[2];

//Applying Label based row field filter
rowField.PivotFilters.Add(PivotFilterType.CaptionEqual, null, "Central", null);
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Apply row field filter
Dim rowField As IPivotField = pivotTable.Fields(2)

'Applying Label based row field filter
rowField.PivotFilters.Add(PivotFilterType.CaptionEqual, Nothing, "Central", Nothing)
{% endhighlight %}
{% endtabs %}  

<img src="working-with-pivot-tables_images/file-formats-xlsio-label-filters.jpeg" alt="Working with Pivot Tables in File Formats XLSIO Applying Label Filters" width="100%" Height="Auto"/>

**Value** **Filter** 

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
IPivotField field = pivotTable.Fields[2];

//Apply value filter
field.PivotFilters.Add(PivotFilterType.ValueLessThan, field, "1341", null);
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
IPivotField field = pivotTable.Fields[2];

//Apply value filter
field.PivotFilters.Add(PivotFilterType.ValueLessThan, field, "1341", null);
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Apply row field filter
Dim field As IPivotField = pivotTable.Fields(2)

'Applying value filter
field.PivotFilters.Add(PivotFilterType. ValueLessThan, field, "1341", Nothing)
{% endhighlight %}
{% endtabs %}  

<img src="working-with-pivot-tables_images/file-formats-xlsio-value-filters.jpeg" alt="Working with Pivot Tables in File Formats XLSIO Applying Value Filters" width="100%" Height="Auto"/>

**Multiple** **filter**

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
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
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
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

  //No exception will be thrown if there are unsaved workbooks.
  excelEngine.ThrowNotSavedOnDestroy = false;
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
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
  field.PivotFilters.Add(PivotFilterType.ValueLessThan, field, "1341", Nothing)

  pivotTable.BuiltInStyle = PivotBuiltInStyles.PivotStyleMedium2
  pivotSheet.Activate()

  workbook.SaveAs("PivotTable.xlsx")

  'No exception will be thrown if there are unsaved workbooks
  excelEngine.ThrowNotSavedOnDestroy = False
End Using
{% endhighlight %}
{% endtabs %} 

A complete working example to apply pivot filter in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Pivot%20Table/Pivot%20Filter).  
  
## Applying pivot table settings  

Excel provides various options through the [PivotTableOptions](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.Implementation.PivotTables.PivotTableOptions.html) dialog box to customize the appearance of the pivot table.

XlsIO supports these pivot table options using the [IPivotTableOptions](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IPivotTableOptions.html) interface to control various settings for the existing pivot table. The following code illustrates how to access the **PivotTableOptions** object. 

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Enable ColumnHeaderCaption
IPivotTable pivotTable = worksheet.PivotTables[0];
IPivotTableOptions options = pivotTable.Options;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Enable ColumnHeaderCaption
IPivotTable pivotTable = worksheet.PivotTables[0];
IPivotTableOptions options = pivotTable.Options;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Enable ColumnHeaderCaption
Dim pivotTable As IPivotTable = worksheet.PivotTables(0)
Dim options As IPivotTableOptions = pivotTable.Options
{% endhighlight %}
{% endtabs %}  

### Show or hide the field list

To show or hide the pivot table field list pane, use the [ShowFieldList](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IPivotTableOptions.html#Syncfusion_XlsIO_IPivotTableOptions_ShowFieldList) property.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Enable ShowFieldList
options.ShowFieldList = false;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Enable ShowFieldList
options.ShowFieldList = false;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Enable ShowFieldList
options.ShowFieldList = False
{% endhighlight %}
{% endtabs %}  

### Header caption

The [RowHeaderCaption](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IPivotTableOptions.html#Syncfusion_XlsIO_IPivotTableOptions_RowHeaderCaption) and [ColumnHeaderCaption](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IPivotTableOptions.html#Syncfusion_XlsIO_IPivotTableOptions_ColumnHeaderCaption) properties allows to edit the respective pivot table headers. The header caption can be enabled or disabled using the [DisplayFieldCaptions](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IPivotTableOptions.html#Syncfusion_XlsIO_IPivotTableOptions_DisplayFieldCaptions) property.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Enable header captions
options.RowHeaderCaption = "Payment Dates";
options.ColumnHeaderCaption = "Payments"; 
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Enable header captions
options.RowHeaderCaption = "Payment Dates";
options.ColumnHeaderCaption = "Payments";
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Enable header captions
options.RowHeaderCaption = "Payment Dates"
options.ColumnHeaderCaption = "Payments"
{% endhighlight %}
{% endtabs %}  

### Grand total

XlsIO provides an equivalent API to perform grand totals with the properties as follows.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Enable GrandTotals
pivotTable.ColumnGrand = false;
pivotTable.RowGrand = true;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Enable GrandTotals
pivotTable.ColumnGrand = false;
pivotTable.RowGrand = true;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Enable GrandTotals
pivotTable.ColumnGrand = False
pivotTable.RowGrand = False
{% endhighlight %}
{% endtabs %}  

### Show or hide collapse button

You can also show or hide the **Collapse** button that appears in the fields of the pivot table, when more than one item exists in a field. The following code example illustrates how to do this.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Enable ShowDrillIndicators
pivotTable.ShowDrillIndicators = true;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Enable ShowDrillIndicators
pivotTable.ShowDrillIndicators = true;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Enable ShowDrillIndicators
pivotTable.ShowDrillIndicators = True
{% endhighlight %}
{% endtabs %}  

### Display field caption and filter option

The filter buttons and field names in the pivot table can be shown or hidden, as in the following code.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Enable DisplayFieldCaption
pivotTable.DisplayFieldCaptions = true;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Enable DisplayFieldCaption
pivotTable.DisplayFieldCaptions = true;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Enable DisplayFieldCaption
pivotTable.DisplayFieldCaptions = True
{% endhighlight %}
{% endtabs %}  

### Repeating row label on each page

You can set the row label on each page while printing, and the header can be viewed on each page.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Enable RepeatItemsOnEachPrintedPage
pivotTable.RepeatItemsOnEachPrintedPage = true;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Enable RepeatItemsOnEachPrintedPage
pivotTable.RepeatItemsOnEachPrintedPage = true;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Enable RepeatItemsOnEachPrintedPage
pivotTable.RepeatItemsOnEachPrintedPage = True
{% endhighlight %}
{% endtabs %} 

### Repeat Labels

You can repeat labels for row or column fields when the [pivot table layout](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.PivotTableRowLayout.html) is set to tabular or outline layout forms.

**Specific Pivot Field**

The following code illustrates how to set the repeat labels option to a specific pivot field.
{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Set repeat labels option to a specific pivot field
pivotTable.Fields[0].RepeatLabels = true;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Set repeat labels option to a specific pivot field
pivotTable.Fields[0].RepeatLabels = true;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
‘Set repeat labels option to a specific pivot field
pivotTable.Fields(0).RepeatLabels = True
{% endhighlight %}
{% endtabs %}  

**All Pivot Fields**

The following code illustrates how to set the repeat labels option to all the pivot fields.
{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Set repeat labels option to all the pivot fields
pivotTable.Options.RepeatAllLabels(true);
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Set repeat labels option to all the pivot fields
pivotTable.Options.RepeatAllLabels(true);
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
‘Set repeat labels option to all the pivot fields
pivotTable.Options.RepeatAllLabels(True)
{% endhighlight %}
{% endtabs %}

## Sort by value in Pivot Table

Pivot field [AutoSort](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IPivotField.html#Syncfusion_XlsIO_IPivotField_AutoSort_Syncfusion_XlsIO_PivotFieldSortType_System_Int32_) allows you to sort the pivot row or column fields based on the data field values. You can perform the sorting in following direction:

* Top to Bottom
* Left to Right 

### Sort a Pivot Table Field Top to Bottom

Top to Bottom sorting can sort the pivot table column field values based on the sort type. To apply Top to Bottom sorting in pivot table, you should apply the sorting in pivot row field by [AutoSort](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IPivotField.html#Syncfusion_XlsIO_IPivotField_AutoSort_Syncfusion_XlsIO_PivotFieldSortType_System_Int32_) method. The following code example illustrates how to apply Top to Bottom sorting to a pivot table.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  FileStream fileStream = new FileStream("PivotTable.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet sheet = workbook.Worksheets[1];
  IPivotTable pivotTable = sheet.PivotTables[0];

  // Pivot Top to Bottom sorting.
  IPivotField rowField = pivotTable.RowFields[0];
  rowField.AutoSort(PivotFieldSortType.Ascending, 1);

  string fileName = "PivotFieldAutoSort.xlsx";

  //Saving the workbook as stream
  FileStream stream = new FileStream(fileName, FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("PivotTable.xlsx");
  IWorksheet sheet = workbook.Worksheets[1];
  IPivotTable pivotTable = sheet.PivotTables[0];

  // Pivot Top to Bottom sorting.
  IPivotField rowField = pivotTable.RowFields[0];
  rowField.AutoSort(PivotFieldSortType.Ascending, 1);

  workbook.SaveAs("PivotFieldAutoSort.xlsx");
  excelEngine.ThrowNotSavedOnDestroy = false;
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("PivotTable.xlsx")
  Dim sheet As IWorksheet = workbook.Worksheets(1)
  Dim pivotTable As IPivotTable = sheet.PivotTables(0)

  ' Pivot Top to Bottom sorting.
  Dim rowField As IPivotField = pivotTable.RowFields(0)
  rowField.AutoSort(PivotFieldSortType.Ascending, 1)

  workbook.SaveAs("PivotTableCalculate.xlsx")
  excelEngine.ThrowNotSavedOnDestroy = False
End Using
{% endhighlight %}
{% endtabs %} 

A complete working example for top to bottom sort in pivot table in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Pivot%20Table/Sort%20Top%20to%20Bottom). 

### Sort a Pivot Table Field Left to Right

Left to Right sorting can sort the pivot table row field values based on the sort type. To apply Left to Right sorting in pivot table, you should apply the sorting in pivot column field by [AutoSort](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IPivotField.html#Syncfusion_XlsIO_IPivotField_AutoSort_Syncfusion_XlsIO_PivotFieldSortType_System_Int32_) method. The following code example illustrates how to apply Left to Right sorting to a pivot table.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  FileStream fileStream = new FileStream("PivotTable.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet sheet = workbook.Worksheets[1];
  IPivotTable pivotTable = sheet.PivotTables[0];

  // Pivot table Left to Right sorting.
  IPivotField columnField = pivotTable.ColumnFields[0];
  columnField.AutoSort(PivotFieldSortType.Ascending, 1);

  string fileName = "PivotFieldAutoSort.xlsx";

  //Saving the workbook as stream
  FileStream stream = new FileStream(fileName, FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("PivotTable.xlsx");
  IWorksheet sheet = workbook.Worksheets[1];
  IPivotTable pivotTable = sheet.PivotTables[0];

  // Pivot table Left to Right sorting.
  IPivotField columnField = pivotTable.ColumnFields[0];
  columnField.AutoSort(PivotFieldSortType.Ascending, 1);

  workbook.SaveAs("PivotFieldAutoSort.xlsx");
  excelEngine.ThrowNotSavedOnDestroy = false;
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("PivotTable.xlsx")
  Dim sheet As IWorksheet = workbook.Worksheets(1)
  Dim pivotTable As IPivotTable = sheet.PivotTables(0)

  ' Pivot table Left to Right sorting.
  Dim rowField As columnField = pivotTable.ColumnFields(0)
  columnField.AutoSort(PivotFieldSortType.Ascending, 1)

  workbook.SaveAs("PivotTableCalculate.xlsx")
  excelEngine.ThrowNotSavedOnDestroy = False
End Using
{% endhighlight %}
{% endtabs %}

A complete working example for left to right sort in pivot table in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Pivot%20Table/Sort%20Left%20to%20Right). 

N> [IsRefreshOnLoad](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.Implementation.PivotTables.PivotCacheImpl.html#Syncfusion_XlsIO_Implementation_PivotTables_PivotCacheImpl_IsRefreshOnLoad) property of [PivotCacheImpl](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.Implementation.PivotTables.PivotCacheImpl.html) is set as true when applying [AutoSort](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IPivotField.html#Syncfusion_XlsIO_IPivotField_AutoSort_Syncfusion_XlsIO_PivotFieldSortType_System_Int32_) to pivot fields.

## Other pivot table operations

### Adding calculated field in the existing pivot table

Calculated field is a special type of database field that perform calculations by using the contents of other fields in the pivot table with the given formula. The formula can contain operators and expressions as in other worksheet formulas. You can use constants and refer to the data from the PivotTable.

You can read and create the calculated fields in the existing pivot table. The following are the Excel restrictions when using the formula:

* Formula cannot contain cell references or defined names.
* Formula cannot contain Worksheet functions that require cell references. 
* Formula cannot use array functions.

The calculated field in XlsIO can be achieved using the following code sample.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
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
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("PivotTable.xlsx");
  IWorksheet sheet = workbook.Worksheets[1];
  IPivotTable pivotTable = sheet.PivotTables[0];

  //Add calculated field to the first pivot table
  IPivotField field = pivotTable.CalculatedFields.Add("Percent", "Sales/Total*100");

  workbook.SaveAs("PivotTableCalculate.xlsx");
  excelEngine.ThrowNotSavedOnDestroy = false;
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("PivotTable.xlsx")
  Dim sheet As IWorksheet = workbook.Worksheets(1)
  Dim pivotTable As IPivotTable = sheet.PivotTables(0)

  ' Add calculated field to the first pivot table
  Dim field As IPivotField = pivotTable.CalculatedFields.Add("Percent", "Sales/Total*100")

  workbook.SaveAs("PivotTableCalculate.xlsx")
  excelEngine.ThrowNotSavedOnDestroy = False
End Using
{% endhighlight %}
{% endtabs %}  

The formula can also be set to the IPivotField property as follows.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
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
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
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
  excelEngine.ThrowNotSavedOnDestroy = false;
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("PivotTable.xlsx")
  Dim sheet As IWorksheet = workbook.Worksheets(0)
  Dim pivotTable As IPivotTable = sheet.PivotTables(0)

  Dim field As IPivotField = pivotTable.CalculatedFields.Add("Percent", "Sales/Total*100")

  'Set Field Formula
  field.Formula = "Sales/Total*200"

  workbook.SaveAs("PivotTable.xlsx")
  excelEngine.ThrowNotSavedOnDestroy = False
End Using
{% endhighlight %}
{% endtabs %}  

A complete working example to add calculated field in pivot table in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Pivot%20Table/Calculated%20Field). 
