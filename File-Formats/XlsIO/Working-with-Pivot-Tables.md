---
title: Working with Pivot Tables
description: Briefs about working with Pivot tables in XlsIO
platform: File-Formats
control: XlsIO
documentation: UG
---
# Working with Pivot Tables

You can easily arrange and summarize complex data in a [Pivot Table](https://support.office.com/en-us/article/PivotTable-I-Get-started-with-PivotTable-reports-in-Excel-2007-bfe774d3-3e20-46f7-b6a3-f7984855d665#). Creation and Manipulation of pivot table is supported in Excel 2007 and later formats, and pivot table in existing document can be preserved for Excel 2003 format**.**

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

  {% endtabs %}  

Now the pivot table should be populated with required fields. **IPivotField** represents a single field in the pivot table which includes row, column and data field axis. 

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

  {% endtabs %}  

Following code example illustrates how to create a pivot table with existing data in the worksheet, using XlsIO.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("PivotData.xlsx");

IWorksheet worksheet = workbook.Worksheets[0];

//Create Pivot cache with the given data range

IPivotCache cache = workbook.PivotCaches.Add(worksheet["A1:H50"]);

//Create "PivotTable1" with the cache at the specified range

IPivotTable pivotTable = worksheet.PivotTables.Add("PivotTable1", worksheet ["A1"], cache);

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

'Create Pivot cache with the given data range

Dim cache As IPivotCache = workbook.PivotCaches.Add(worksheet("A1:H50"))

'Create "PivotTable1" with the cache at the specified range

Dim pivotTable As IPivotTable = worksheet.PivotTables.Add("PivotTable1", worksheet ("A1"), cache)

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

  {% endtabs %}  

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

workbook.SaveAs("PivotTable_DyanamicRange.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

XlsIO supports 85 built-in styles of Excel 2007, enabling users to create a table with rich formatting through PivotBuiltInStyles property as follows. To know more about various built-in styles supported, please refer **PivotBuiltInStyles** enumeration in API section.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("PivotTable.xlsx");

IWorksheet worksheet = workbook.Worksheets[0];

IPivotTable pivotTable = worksheet.PivotTables[0];


//Set BuitInStyle

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

Dim sheet As IWorksheet = workbook.Worksheets(0)

Dim pivotTable As IPivotTable = sheet.PivotTables(0)

'Set BuitInStyle

pivotTable.BuiltInStyle = PivotBuiltInStyles.PivotStyleDark12

workbook.SaveAs("PivotTable_Style.xlsx")

workbook.Close()

'No exception will be thrown if there are unsaved workbooks
excelEngine.ThrowNotSavedOnDestroy = False
excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

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

  {% endtabs %}  

![](Working-with-Pivot-Tables_images/Working-with-Pivot-Tables_img2.jpeg)


**Value** **Filter** 

{% tabs %}  

{% highlight c# %}
IPivotField field = pivotTable.Fields[2];

//Apply value filter

field.PivotFilters.Add(PivotFilterType.ValueLessThan, field, "1341", null)



{% endhighlight %}

{% highlight vb %}
'Apply row field filter
Dim field As IPivotField = pivotTable.Fields(2)

'Applying value filter
field.PivotFilters.Add(PivotFilterType. ValueLessThan, field, "1341", Nothing)



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

IPivotField datafield = pivotSheet.PivotTables[0].Fields[5];
pivotTable.DataFields.Add(datafield, "Sum of Units", PivotSubtotalTypes.Sum);

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

  {% endtabs %}  

## Applying Pivot Table Settings  

Excel provides various options through the PivotTableOptions dialog box to customize the appearance of the pivot table.

XlsIO supports these pivot table options using IPivotTableOptions interface to control various settings for the existing Pivot table.  To know more about various pivot table options, please refer **IPivotTableOptions** in API section. Following code illustrated how to access PivotTableOptions object. 

{% tabs %}  

{% highlight c# %}
//Enable ColumnHeaderCaption
IPivotTable pivotTable = worksheet.PivotTables[0];
IPivotTableOptions options = pivotTable.Options;



{% endhighlight %}

{% highlight vb %}
Dim pivotTable As IPivotTable = worksheet.PivotTables(0)

Dim options As IPivotTableOptions = pivotTable.Options



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

  {% endtabs %}  

### Header Caption

The **RowHeaderCaption** and **ColumnHeadercaption** properties allows to edit the respective pivot table headers. The header caption can be enabled or disabled through **DisplayFieldCaption** property.

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

  {% endtabs %}  

### Grand Total

XlsIO provides an equivalent API to perform with simple properties as follows.

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

  {% endtabs %}  

### Display Field Caption and Filter Option

The Filter buttons and field names in the pivot table can be shown or hidden, as in the following code.

{% tabs %}  

{% highlight c# %}
//Enable DisplayFieldCaption.

pivotTable.DisplayFieldCaptions = true;



{% endhighlight %}

{% highlight vb %}
'Enable DisplayFieldCaption.

pivotTable.DisplayFieldCaptions = True



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

IWorksheet sheet = workbook.Worksheets[0];

IPivotTable pivotTable = sheet.PivotTables[0];


//Add calculated field to the first pivot table

IPivotField field = pivotTable.CalculatedFields.Add("Percent", "Sales/Total*100");


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

' Add calculated field to the first pivot table

Dim field As IPivotField = pivotTable.CalculatedFields.Add("Percent", "Sales/Total*100")


workbook.SaveAs("PivotTable.xlsx")

workbook.Close()

excelEngine.ThrowNotSavedOnDestroy = False
excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

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

'Set Field Formula.

field.Formula = "Sales/Total*200"

workbook.SaveAs("PivotTable.xlsx")

workbook.Close()

excelEngine.ThrowNotSavedOnDestroy = False
excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

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

IPivotField datafield = pivotSheet.PivotTables[0].Fields[5];
pivotTable.DataFields.Add(datafield, "Sum of Units", PivotSubtotalTypes.Sum);

pivotTable.BuiltInStyle = PivotBuiltInStyles.PivotStyleDark12;

//The following code sample must be included to XlsIO layout the pivot table like Excel.

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

'The following code sample must be included to XlsIO layout the pivot table like Excel.

pivotTable.Layout()

workbook.SaveAs("PivotTable.xlsx")

workbook.Close()

excelEngine.ThrowNotSavedOnDestroy = False
excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

