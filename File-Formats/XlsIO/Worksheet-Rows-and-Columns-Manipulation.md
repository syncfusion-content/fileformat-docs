---
title: Worksheet Rows and Columns Manipulation
description: Briefs about Row and Column manipulations in XlsIO
platform: File-formats
control: XlsIO
documentation: UG
---

# Worksheet Rows and Columns Manipulation

Essential XlsIO provides rows and columns manipulation options equivalent to Excel such as insertion, deletion, hiding, adjusting dimensions, grouping, sub-totaling etc., through **IWorksheet** interface. The following sections illustrate these manipulating techniques in detail.

## Insert Rows and Columns 

The following code snippet illustrates on how to insert row and column in a worksheet.


{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");

IWorksheet worksheet = workbook.Worksheets[0];

// Insert a row

worksheet.InsertRow(3, 1, ExcelInsertOptions.FormatAsBefore);

// Inserting a column

worksheet.InsertColumn(2, 1, ExcelInsertOptions.FormatAsAfter);

workbook.SaveAs("Book1.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")

Dim worksheet As IWorksheet = workbook.Worksheets(0)

'Inserting a row

worksheet.InsertRow(3, 1, ExcelInsertOptions.FormatAsBefore)

'Inserting a column

worksheet.InsertColumn(2, 1, ExcelInsertOptions.FormatAsAfter)

workbook.SaveAs("Book1.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

N> Row and Column index of Insert methods are "one based".

To know more about insert rows and columns, please refer **WorksheetImpl** in API section.

## Delete Rows and Columns 

The following code shows how to delete rows/columns.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");

IWorksheet worksheet = workbook.Worksheets[0];

//Delete a row

worksheet.DeleteRow(3);

//Delete a column

worksheet.DeleteColumn(2);

workbook.SaveAs(Book1.xlsx);

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")

Dim worksheet As IWorksheet = workbook.Worksheets(0)

'Delete a row

worksheet.DeleteRow(3)

'Delete a column

worksheet.DeleteColumn(2)

workbook.SaveAs("Book1.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

T>To extract values little faster or to delete a larger number of rows and columns, use Un-Safe code option of **IApplication** interface as follows

{% tabs %}  

{% highlight c# %}
application.DataProviderType = ExcelDataProviderType.Unsafe;



{% endhighlight %}

{% highlight vb %}
application.DataProviderType = ExcelDataProviderType.Unsafe



{% endhighlight %}

  {% endtabs %}  
  
In addition, cells can be deleted by shifting other cells in a row/column towards up/left by one step. This can be done by using **Clear** method as shown in the below code.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");

IWorksheet worksheet = workbook.Worksheets[0];

//Shifts cells towards Left after deletion

worksheet.Range["A1:E1"].Clear(ExcelMoveDirection.MoveLeft);

//Shifts cells toward Up after deletion

worksheet.Range["A1:A6"].Clear(ExcelMoveDirection.MoveUp);

workbook.SaveAs("Book1.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")

Dim worksheet As IWorksheet = workbook.Worksheets(0)

'Shifts cells towards Left after deletion

worksheet.Range("A1:E1").Clear(ExcelMoveDirection.MoveLeft)



'Shifts cells towards Up after deletion

worksheet.Range("A1:A6").Clear(ExcelMoveDirection.MoveUp)

workbook.SaveAs("Book1.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

N> Deletion by using above method is more efficient than looping.
N> Row/Column index of these methods are "one based".

## Show or Hide Rows and Columns 

Visibility of rows and columns can be set by using **ShowRow** and **ShowColumn** methods as shown below.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");

IWorksheet worksheet = workbook.Worksheets[0];

//Hiding the first column and second row

worksheet.ShowColumn( 1, false );

worksheet.ShowRow( 2, false );

workbook.SaveAs("Book1.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")

Dim worksheet As IWorksheet = workbook.Worksheets(0)

'Hiding the first column and second row

worksheet.ShowColumn(1, False)

worksheet.ShowRow(2, False)

workbook.SaveAs("Book1.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

## Show or Hide Specific Range

Essential XlsIO allows to set visibility for a specific range. The following code snippet shows on how to set the visibility of a range.


{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet worksheet = workbook.Worksheets[0];

IRange range = worksheet[1, 4];

//Hiding the range ‘D1’
worksheet.ShowRange(range, false);

IRange firstRange = worksheet [1, 1, 3, 3];
IRange secondRange = worksheet [5, 5, 7, 7];
RangesCollection rangeCollection = new RangesCollection(application, sheet);
rangCollection.Add(firstRange);
rangeCollection.Add(secondRange);

//Hiding a collection of ranges
worksheet.ShowRange(rangeCollection, false);

workbook.SaveAs("Book1.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim worksheet As IWorksheet = workbook.Worksheets(0)

Dim range As IRange = worksheet (1, 4)

'Hiding the range ‘D1’

worksheet.ShowRange(range, False)

Dim firstRange As IRange = worksheet (1, 1, 3, 3)

Dim secondRange As IRange = worksheet (5, 5, 7, 7)

Dim rangeCollection As RangesCollection = New RangesCollection(app, sheet)

rangCollection.Add(firstRange)

rangeCollection.Add(secondRange)

'Hiding a collection of ranges

worksheet.ShowRange(rangeCollection, False)

workbook.SaveAs("Book1.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

## Adjust Row Height and Column Width 

Rows and columns can be [resized](https://support.office.com/en-ca/article/Change-the-column-width-and-row-height-72f5e3cc-994d-43e8-ae58-9774a0905f46) based on its contents. XlsIO allows to resize rows and columns in the following ways.

* Resize a specific row or column
* Resize a range of rows or columns

### Resize a specific row or column

A single row or column can be resized by **SetRowHeight** and **SetColumnWidth** methods of __IWorksheet__. Similarly, the height and width of a single row or column can be accessed using **GetRowHeight** or **GetColumnWidth** methods of __IWorksheet__. 

The following code snippet shows how to resize a single row and column.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet worksheet = workbook.Worksheets[0];

//Modifying the row height

worksheet.SetRowHeight(2, 25);

//Modifying the column width

worksheet.SetColumnWidth(1, 20);

workbook.SaveAs("Book1.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim worksheet As IWorksheet = workbook.Worksheets(0)

'Modifying the row height

worksheet.SetRowHeight(2, 25)

'Modifying the column width

Worksheet.SetColumnWidth(1, 20)

workbook.SaveAs("Book1.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

### Resize a range of rows or columns

Multiple rows or columns can be resized and accessed by using **RowHeight** and **ColumnWidth** properties of __IRange__. The following code snippet shows how to resize multiple rows and columns.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet worksheet = workbook.Worksheets[0];

//Modifying the row height

worksheet.Range["A2:A6"].RowHeight = 25;

//Modifying the column width

worksheet.Range["A1:D1"].ColumnWidth = 20;

workbook.SaveAs("Book1.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim worksheet As IWorksheet = workbook.Worksheets(0)

'Modifying the row height

worksheet.Range("A2:A6").RowHeight = 25

'Modifying the column width

worksheet.Range("A1:D1").ColumnWidth = 20

workbook.SaveAs("Book1.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

N> If a column width or a row height is 0, then the column/row is hidden.
N> Column width and row height can also be set in pixels, by using the IWorksheet.SetColumnWidthInPixel and IWorksheet.SetRowHeightInPixel methods respectively.

## Auto-Fit Rows and Columns

XlsIO allows to auto-size the width and height of a cell to fit its content. This section demonstrates various methods to auto-fit rows and columns of a worksheet.

### Auto-Fit a Single Row or Column

The following code snippet shows how a row and a column is re-sized to its content.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet worksheet = workbook.Worksheets[0];

worksheet.Range["A1"].Text = "This is a long text";

worksheet.Range["A1"].WrapText = true;

//AutoFit applied to a single row

worksheet.AutofitRow(1); 

worksheet.Range["A3"].Text = "This is a long text";

//AutoFit applied to a single column

worksheet.AutofitColumn(3);

workbook.SaveAs("Book1.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim worksheet As IWorksheet = workbook.Worksheets(0)

worksheet.Range("A1").Text = "This is a long text"

worksheet.Range("A1").WrapText = true

'AutoFit applied to a single row

worksheet.AutofitRow(1) 

worksheet.Range("A3").Text = "This is a long text"

'AutoFit applied to a single column

worksheet.AutofitColumn(3)

workbook.SaveAs("Book1.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

N> Row and Column indexes are "one based".

There is an alternative way to auto-fit row or column is by accessing the row or column, which is shown in the below code snippet.

{% tabs %}  
{% highlight c# %}
//AutoFit applied to first row

worksheet.Rows[0].AutofitRows();

//AutoFit applied to first column

worksheet.Columns[0].AutofitColumns();



{% endhighlight %}

{% highlight vb %}
'AutoFit applied to first row

worksheet.Rows(0).AutofitRows()

'AutoFit applied to first column

worksheet.Columns(0).AutofitColumns()



{% endhighlight %}
{% endtabs %}  

N> Here column and row indexes are "zero based".

### Auto-Fit Multiple Rows or Columns

Multiple rows/column can be auto fitted based on the range specified. This is depicted in the below code.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet worksheet = workbook.Worksheets[0];

//Assigning text to cells

worksheet.Range["A1:D1"].Text = "This is the Long Text";

worksheet.Range["A2:A5"].Text = "This is the Long Text using Autofit Columns and Rows";

worksheet.Range["A2:A5"].WrapText = true;

//Auto-Fit the range

worksheet.Range["A1:C1"].AutofitColumns();

worksheet.Range["A2:A5"].AutofitRows();

//Auto-fits all the columns used in the worksheet

worksheet.UsedRange.AutofitColumns();

workbook.SaveAs("Book1.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim worksheet As IWorksheet = workbook.Worksheets(0)

'Assigning text to cells

worksheet.Range("A1:D1").Text = "This is the Long Text"

worksheet.Range("A2:A5").Text = "This is the Long Text using Autofit Columns and Rows"

worksheet.Range("A2:A5").WrapText = true

'Auto-Fit the range

worksheet.Range("A1:C1").AutofitColumns()

worksheet.Range("A2:A5").AutofitRows()

'Auto-fits all the columns used in the worksheet

worksheet.UsedRange.AutofitColumns()

workbook.SaveAs("Book1.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

N> 1) If a Range is text wrapped, AutoFitColumn method will not be applied on it.
N> 2) If a Range is merged, Auto-Fit methods will not be applied on it. Note that this is the behavior of Excel as well.
N> 3) Auto fitting is a time consuming process so it might cause performance issues when used excessively.

## Group or Ungroup Rows and Columns 

Rows and columns can be grouped or ungrouped to summarize the data. The following code snippet shows how rows and columns can be grouped or ungrouped.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx")

IWorksheet worksheet = workbook.Worksheets[0];



//Group Rows

worksheet.Range["A1:A3"].Group(ExcelGroupBy.ByRows, true);

worksheet.Range["A4:A6"].Group(ExcelGroupBy.ByRows);

//Group Columns

worksheet.Range["A1:B1"].Group(ExcelGroupBy.ByColumns, false);

worksheet.Range["C1:F1"].Group(ExcelGroupBy.ByColumns);

//Ungroup Rows

worksheet.Range["A1:A3"].UnGroup(ExcelGroupBy.ByRows);

//Ungroup Columns

worksheet.Range["C1:F1"].UnGroup(ExcelGroupBy.ByColumns);

workbook.SaveAs("Book1.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")

Dim worksheet As IWorksheet = workbook.Worksheets(0)

'Group Rows

worksheet.Range( "A1:A3" ).Group(ExcelGroupBy.ByRows, True)        

worksheet.Range( "A4:A6" ).Group(ExcelGroupBy.ByRows)

'Group Columns

worksheet.Range( "A1:B1" ).Group(ExcelGroupBy.ByColumns, False)       

worksheet.Range( "C1:F1" ).Group(ExcelGroupBy.ByColumns)

'Ungroup Rows

worksheet.Range( "A1:A3" ).UnGroup(ExcelGroupBy.ByRows)       

'Ungroup Columns

worksheet.Range( "C1:F1" ).UnGroup(ExcelGroupBy.ByColumns)

workbook.SaveAs("Book1.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

### Expand or Collapse Groups

Groups can be expanded and collapsed using **ExpandGroups** and **CollapseGroups** methods of __IRange__. The following code shows how to expand and collapse groups.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");

IWorksheet worksheet = workbook.Worksheets[0];



//Expand group with flag set to expand parent

worksheet.Range["A5:A15"].ExpandGroup(ExcelGroupBy.ByRows, ExpandCollapseFlags.ExpandParent);

//Collapse group

worksheet.Range["A5:A15"].CollapseGroup(ExcelGroupBy.ByRows);

workbook.SaveAs("Book1.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")

Dim worksheet As IWorksheet = workbook.Worksheets(0)

'Expand group with flag set to expand parent

worksheet.Range("A5:A15").ExpandGroup(ExcelGroupBy.ByRows, ExpandCollapseFlags.ExpandParent)

'Collapse group

worksheet.Range("A5:A15").CollapseGroup(ExcelGroupBy.ByRows)

workbook.SaveAs("Book1.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

### Subtotal

XlsIO supports subtotaling a group to quickly calculate rows of related data by inserting subtotals and totals. 

Various Subtotal options like __Summary__ __below__ __data__, __Replace__ __current__ __subtotals__, __Page__ __break__ __between__ __groups__ can be used to customize data.

The following code shows how to add subtotal for a given range.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");

IWorksheet worksheet = workbook.Worksheets[0];

//Set the range for subtotaling

IRange range = worksheet.Range["C3:G12"];

//Perform subtotals for the range with every change in first column

//and subtotals to be included for specified list of columns

range.SubTotal(0, ConsolidationFunction.Sum, new int[] { 2, 3, 4 });

workbook.SaveAs("Book1.xlsx");

workbook.Close();

excelEngine.Dispose();          



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks. Open("Sample.xlsx")

Dim worksheet As IWorksheet = workbook.Worksheets(0)

'Set the range for subtotaling

Dim range As IRange = worksheet ("C3:G12")

'Perform subtotals for the range with every change in first column 

'and subtotals to be included for specified list of columns

range.SubTotal(0, ConsolidationFunction.Sum, New Integer() {4})

workbook.SaveAs("Book1.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

N> Here column and row indexes are "zero based".

The screenshot of the output with SubTotal generated from the above code.

![](Worksheet-Rows-and-Columns-Manipulation_images/Worksheet-Rows-and-Columns-Manipulation_img1.jpeg)


N> Summary of a group can be shown above rows and left of column using the IsSummaryRowBelow and IsSummaryColumnRight properties of IPageSetup interface. By default, these properties were set to TRUE.

