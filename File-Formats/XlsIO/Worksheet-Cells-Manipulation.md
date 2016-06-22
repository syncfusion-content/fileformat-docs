---
title: Worksheet Cells Manipulation
description: Briefs about worksheet cells manipulation in XlsIO
platform: File-formats
control: XlsIO
documentation: UG
---

# Worksheet Cells Manipulation

The **IRange** interface represents a single cell or a group of cells in a worksheet. XlsIO has several useful methods for accessing, manipulating and formatting the content in the ranges.

## Accessing a Cell or a Range

The following code shows the different ways of accessing a single cell or group of cells

N> Here row and column indexes in the range are "one based". 

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet sheet = workbook.Worksheets[0];

// Access a range by specifying cell address. 

sheet.Range["A7"].Text = "Accessing a Range by specify cell address ";

// Access a range by specifying cell row and column index. 

sheet.Range[9, 1].Text = "Accessing a Range by specify cell row and column index ";

// Access a Range by specifying using defined name.

sheet.Range["Name"].Text = "Accessing a Range by specifying using defined name.";

// Accessing a Range of cells by specifying cells address.

sheet.Range["A13:C13"].Text = "Accessing a Range of Cells (Method 1)";

// Accessing a Range of cells specifying cell row and column index.

sheet.Range[15, 1, 15, 3].Text = "Accessing a Range of Cells (Method 2)";

workbook.SaveAs("Range.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim sheet As IWorkbook = workbook.Worksheets(0)

' Access a range by specify cell address. 

sheet.Range("A7").Text = "Accessing a Range by specify cell address "

' Access a range by specify cell row and column index. 

sheet.Range(9, 1).Text = "Accessing a Range by specify cell row and column index "

' Access a Range by specifying using defined name.

sheet.Range("Name").Text = "Accessing a Range by specifying using defined name."

' Accessing a Range of cells by specify cells address.

sheet.Range("A13:C13").Text = "Accessing a Range of Cells (Method 1)"

' Accessing a Range of cells specify cell row and column index.

sheet.Range(15, 1, 15, 3).Text = "Accessing a Range of Cells (Method 2)"

workbook.SaveAs("Range.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

T> You can use of GetText, SetText, GetNumber and SetNumber methods from worksheet object that enable users to get/set values without range object.

### Accessing Discontinuous Ranges

You can also access discontinuous ranges and add them to the **RangesCollection**.  You can modify the contents or applying formatting of discontinuous range through RangeCollection instance. 

Following code snippet illustrates how to access discontinuous range.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet sheet = workbook.Worksheets[0];

// range1 and range2 are discontinuous ranges.

IRange range1 = sheet.Range[ "A1:A2" ];

IRange range2 = sheet.Range["C1:C2" ];

IRanges ranges = sheet.CreateRangesCollection();

// range1 and range2 are considered as a single range

ranges.Add( range1 );

ranges.Add( range2 );

ranges.Text = "Test";

workbook.SaveAs("Range.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim sheet As IWorkbook = workbook.Worksheets(0)

' range1 and range2 are discontinuous ranges.

Dim range1 As IRange = sheet.Range("A1:A2")

Dim range2 As IRange = sheet.Range("C1:C2")

Dim ranges As IRanges = sheet.CreateRangesCollection()

' range1 and range2 are considered as a single range

ranges.Add(range1)

ranges.Add(range2)

ranges.Text = "Test"

workbook.SaveAs("Range.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

### Accessing a Cell or Range using IMigrantRange 

The **IMigrantRange** interface can also be used to access a single cell or group of cells and manipulate it.  You can prefer IMigrantRange instead of IRange while writing large amount of data which is an optimal way. 

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet sheet = workbook.Worksheets[0];

IMigrantRange migrantRange = sheet.MigrantRange;

// Writing Data.

for (int row = 1; row <= rowCount; row++)

{

for (int column = 1; column <= colCount; column++)

{

// Writing values.

migrantRange.ResetRowColumn(row, column);

migrantRange.Text = "Test";

}

}

workbook.SaveAs("Range.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim sheet As IWorkbook = workbook.Worksheets(0)

Dim migrantRange As IMigrantRange = sheet.MigrantRange

' Writing Data.

Dim row As Integer

For  row = 1 To  rowCount Step  row + 1

Dim column As Integer

For  column = 1 To  colCount Step  column + 1

' Writing values.

migrantRange.ResetRowColumn(row, column)

migrantRange.Text = "Test"

Next

Next

workbook.SaveAs("Range.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

## Accessing used range of a Worksheet

The following code snippet shows how to get the range of cells used in a given sheet.

N> By default, XlsIO considers a cell as used, even if there exists some formatting alone. You can disable this behavior, and make XlsIO consider a cell as used, only when there exists data, by using the UsedRangeIncludesFormatting property.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");

IWorksheet sheet = workbook.Worksheets[0];

// UsedRange excludes the blank cell which has formatting

sheet.UsedRangeIncludesFormatting = false;

// Modifying the column width and row height of the used range

sheet.UsedRange.ColumnWidth = 20;

sheet.UsedRange.RowHeight = 20;

workbook.SaveAs("Range.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim sheet As IWorkbook = workbook.Worksheets(0)

' UsedRange excludes the blank cell which has formatting

sheet.UsedRangeIncludesFormatting = false

' Modifying only the Used Ranges.

sheet.UsedRange.ColumnWidth = 20

sheet.UsedRange.RowHeight = 20

workbook.SaveAs("Range.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

## Clearing a Cell Content

You can delete everything in the cell, or just remove the formatting, contents, comments. The following code example illustrates how to clear a range along with its formatting.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");

IWorksheet sheet = workbook.Worksheets[0];

// Clearing a Range “A4” and its formatting.

sheet.Range["A4"].Clear(true);

workbook.SaveAs("ClearRange.xlsx");

workbook.Version = ExcelVersion.Excel2013;

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")

Dim sheet As IWorkbook = workbook.Worksheets(0)

' Clearing a Range “A4” and its formatting.

sheet.Range("A4").Clear(True)

workbook.Version = ExcelVersion.Excel2013

workbook.SaveAs("ClearRange.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

## Copy or Move a Range

You can copy a range of cells to another range using CopyTo method. You can also copy all the formats or only specific formats using **ExcelCopyRangeOptions** options. 

Following code example illustrates how to copy a range of cells from the source to destination.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");

IWorksheet sheet = workbook.Worksheets[0];

// Copying a Range “A1” to “A5”.

IRange source = sheet.Range["A1"];

IRange destination = sheet.Range["A5"];

source.CopyTo(destination,ExcelCopyRangeOptions.All);

workbook.Version = ExcelVersion.Excel2013;

workbook.SaveAs("CopyRange.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")

Dim sheet As IWorkbook = workbook.Worksheets(0)

' Copying a Range “A1” to “A5”.

Dim source As IRange = sheet.Range("A1")

Dim destination As IRange = sheet.Range("A5")

source.CopyTo(destination,ExcelCopyRangeOptions.All)

workbook.Version = ExcelVersion.Excel2013

workbook.SaveAs("CopyRange.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

**MoveTo** method is used for moving a range of cells to another range as shown below. 

N> MoveTo method does not update formulas.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx"); 

IWorksheet sheet = workbook.Worksheets[0];

// Moving a Range “A1” to “A5”.

IRange source = sheet.Range["A1"];

IRange destination = sheet.Range["A5"];

source.MoveTo(destination);

workbook.Version = ExcelVersion.Excel2013;

workbook.SaveAs("MoveRange.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")

Dim sheet As IWorkbook = workbook.Worksheets(0)

' Moving a Range “A1” to “A5”.

Dim source As IRange = sheet.Range("A1")

Dim destination As IRange = sheet.Range("A5")

source.MoveTo(destination)

workbook.Version = ExcelVersion.Excel2013

workbook.SaveAs("MoveRange.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

## Find and Replace

You can perform [find and replace](https://support.office.com/en-usa/article/Find-or-replace-text-and-numbers-on-a-worksheet-3a2c910f-01b9-4263-8db2-333dead6ae33) text and numbers in workbook or worksheet using XlsIO. Also, XlsIO provides the following options:
*	To search for data in formulas, values or comments.
*	To search for case-sensitive data and to match entire cell contents of the cell.

To know more about these options, please refer the [ExcelFindType](http://help.syncfusion.com/cr/cref_files/file-formats/xlsio/Syncfusion.XlsIO.Base~Syncfusion.XlsIO.ExcelFindType.html), [ExcelFindOptions](http://help.syncfusion.com/cr/cref_files/file-formats/xlsio/Syncfusion.XlsIO.Base~Syncfusion.XlsIO.ExcelFindOptions.html) in the API documentation section.

You can find all the occurrences of a text in worksheet by using [FindAll](http://help.syncfusion.com/cr/cref_files/file-formats/xlsio/Syncfusion.XlsIO.Base~Syncfusion.XlsIO.IWorksheet~FindAll.html) method. To know more about Find and Replace, please refer [IWorksheet](http://help.syncfusion.com/cr/cref_files/file-formats/xlsio/Syncfusion.XlsIO.Base~Syncfusion.XlsIO.IWorksheet_members.html) in the API documentation section.
The following code illustrates how to find all the occurrences of text in a worksheet with different find options.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");

IWorksheet sheet = workbook.Worksheets[0];

// Searches for the given string within the text of worksheet.
IRange[] result = sheet.FindAll("FindValue", ExcelFindType.Text);

// Searches for the given string in formulas.
IRange[] result = sheet.FindAll("FindValue", ExcelFindType.Formula);

// Searches for the given string in calculated value, number and text.
IRange[] result = sheet.FindAll("FindValue", ExcelFindType.Values);

// Searches for the given string in comments.
IRange[] result = sheet.FindAll("FindValue", ExcelFindType.Comments);

// Searches for the given string within the text of worksheet and case matched.
IRange[] result = sheet.FindAll("FindValue", ExcelFindType.Text, ExcelFindOptions.MatchCase);

// Searches for the given string within the text of worksheet and the entire cell content matching to search text.
IRange[] result = sheet.FindAll("FindValue", ExcelFindType.Text, ExcelFindOptions.MatchEntireCellContent);

workbook.Version = ExcelVersion.Excel2013;

workbook.SaveAs("Find.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")

Dim sheet As IWorkbook = workbook.Worksheets(0)

' Searches for the given string within the text of worksheet.
Dim result() As IRange = sheet.FindAll("FindValue", ExcelFindType.Text)

' Searches for the given string in formulas.
Dim result() As IRange = sheet.FindAll("FindValue", ExcelFindType.Formula)

' Searches for the given string in calculated value, number and text.
Dim result() As IRange = sheet.FindAll("FindValue", ExcelFindType.Values)

' Searches for the given string in comments.
Dim result() As IRange = sheet.FindAll("FindValue", ExcelFindType.Comments)

' Searches for the given string within the text of worksheet and case matched.
Dim result() As IRange = sheet.FindAll("FindValue", ExcelFindType.Text, ExcelFindOptions.MatchCase)

' Searches for the given string within the text of worksheet and the entire cell content matching to search text.
Dim result() As IRange = sheet.FindAll("FindValue", ExcelFindType.Text, ExcelFindOptions.MatchEntireCellContent)

workbook.SaveAs("Find.xlsx")

workbook.Close()

workbook.Version = ExcelVersion.Excel2013

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

You can replace a text with another text with the help of Replace method which searches for text you’d like to change. You can replace a string, with the data of various data types and data sources, such as data table, data column and array.
To know more about replace overloads, please refer [Replace](http://help.syncfusion.com/cr/cref_files/file-formats/xlsio/Syncfusion.XlsIO.Base~Syncfusion.XlsIO.IWorksheet~Replace.html) in the API documentation section.

The following code example illustrates how to replace all occurrences of given string with various data.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");

IWorksheet sheet = workbook.Worksheets[0];

// Replaces the given string with another string.
sheet.Replace("FindValue", "NewValue");

// Replaces the given string with another string on match case.
sheet.Replace("FindValue", "NewValue", ExcelFindOptions.MatchCase);

// Replaces the given string with another string matching entire cell content to the search word.
sheet.Replace("FindValue", "NewValue", ExcelFindOptions.MatchEntireCellContent);

// Replaces the given string with DateTime value.
sheet.Replace("DateValue", DateTime.Now);

// Replaces the given string with Array.
sheet.Replace("ArrayValue", new string[] { "ArrayValue1", "ArrayValue2", "ArrayValue3" }, true);

// Replaces the given string with DataTable.
DataTable table = SampleDataTable();

sheet.Replace("DataTable", table, true); 

workbook.Version = ExcelVersion.Excel2013;

workbook.SaveAs("Replace.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")

Dim sheet As IWorkbook = workbook.Worksheets(0)

' Replaces the given string with another string.
sheet.Replace("FindValue", "NewValue")

' Replaces the given string with another string on match case.
sheet.Replace("FindValue", "NewValue", ExcelFindOptions.MatchCase)

' Replaces the given string with another string matching entire cell content to the search word.
sheet.Replace("FindValue", "NewValue", ExcelFindOptions.MatchEntireCellContent)

' Replaces the given string with DateTime value.
sheet.Replace("DateValue", DateTime.Now)

' Replaces the given string with Array.
sheet.Replace("ArrayValue", New String() {"ArrayValue1", "ArrayValue2", "ArrayValue3"}, True)

' Replaces the given string with DataTable.
Dim table As DataTable = SampleDataTable()

sheet.Replace("DataTable", table, True)

workbook.Version = ExcelVersion.Excel2013

workbook.SaveAs("Replace.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

## Data Sorting

You can sort a range of cells based on data in one or more columns. You can perform sorting based on the following:

* Based on Cell Values
* Based on Font Color
* Based on Cell Color

N> Currently XlsIO don’t support sorting based on cell icon, parsing and serialization of its sorting details.

**Based** **on** **Cell** **Values**

The following code snippet explains how to sort a range of cells by values 

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");

IWorksheet sheet = workbook.Worksheets[0];

// Creates the data sorter

IDataSort sorter = workbook.CreateDataSorter();

// Range to sort

sorter.SortRange = sheet.Range["D3:D16"];

// Adds the sort field with the column index, sort based on and order by attribute

ISortField sortField = sorter.SortFields.Add(0, SortOn.Values, OrderBy.Ascending);

// Adds another sort field

ISortField sortField2 = sorter.SortFields.Add(1, SortOn.Values, OrderBy.Ascending);

// Sort based on the sort Field attribute

sorter.Sort();

workbook.Version = ExcelVersion.Excel2013;

workbook.SaveAs("Sort.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")

Dim sheet As IWorkbook = workbook.Worksheets(0)

' Creates the Data sorter

Dim sorter As IDataSort = workbook.CreateDataSorter()

' Specifies the sort range

sorter.SortRange = sheet.Range("D3:D16")

' Adds the sort field with column index, sort based on and order by attribute

Dim field As ISortField = sorter.SortFields.Add(2, SortOn.Values, OrderBy.OnTop)

' Adds the second sort field

field = sorter.SortFields.Add(2,SortOn.Values,OrderBy.OnTop)

' Sorts the data with the sort field attribute

sorter.Sort()

workbook.Version = ExcelVersion.Excel2013

workbook.SaveAs("Sort.xlsx")

workbook.Close()

excelEngine.Dispose()





{% endhighlight %}
{% endtabs %}  

### Based on Font Color

The following code snippet explains how to move a range of cells with the specified font color to either top or bottom of the sorting range.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");

IWorksheet sheet = workbook.Worksheets[0];

// Creates the data sorter

IDataSort sorter = workbook.CreateDataSorter();

// Range to sort

sorter.SortRange = sheet.Range["A2:D16"];

// Creates the sort field with the column index, sort based on and order by attribute

ISortField sortField1 = sorter.SortFields.Add(2, SortOn.FontColor, OrderBy.OnTop);

// Specifies the color to sort the data

sortField1.Color = Color.Red;

// Creates another sort field with the column index, sort based on and order by attribute

ISortField sortField2 = sorter.SortFields.Add(2, SortOn.FontColor, OrderBy.OnTop);

// Specifies the color to sort the data

sortField2.Color = Color.Green;

// Sort based on the sort Field attribute

sorter.Sort();

workbook.Version = ExcelVersion.Excel2013;

workbook.SaveAs("Sort.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")

Dim sheet As IWorkbook = workbook.Worksheets(0)

' Creates the Data sorter

Dim sorter As IDataSort = workbook.CreateDataSorter()

' Specifies the sort range

sorter.SortRange = sheet.Range("A2:D16")

Dim field1 As ISortField

' Adds the sort field with column index, sort based on and order by attribute

field1 = sorter.SortFields.Add(2, SortOn.FontColor,OrderBy.OnTop)

' Sorts the data based on this color

Field1.Color = Color.Red

Dim field2 As ISortField

' Adds another sort field with column index, sort based on and order by attribute

Field2 = sorter.SortFields.Add(2, SortOn.FontColor,OrderBy.OnTop)

' Sorts the data based on this color

Field2.Color = Color.Green

' Sorts the data with the sort field attribute.

sorter.Sort()

workbook.Version = ExcelVersion.Excel2013

workbook.SaveAs("Sort.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

### Based on Cell Color

The following code snippet explains how to move a range of cells with the specified cell background color to either top or bottom of the sorting range.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");

IWorksheet sheet = workbook.Worksheets[0];

// Creates the data sorter

IDataSort sorter = workbook.CreateDataSorter();

// Range to sort

sorter.SortRange = sheet.Range["A2:D16"];

// Creates the sort field with the column index, sort based on and order by attribute

ISortField sortField1 = sorter.SortFields.Add(2, SortOn.CellColor, OrderBy.OnTop);

// Specifies the color to sort the data

sortField1.Color = Color.Red;

// Creates the sort field with the column index, sort based on and order by attribute

ISortField sortField2 = sorter.SortFields.Add(2, SortOn.CellColor, OrderBy.OnTop);

// Specifies the color to sort the data

sortField2.Color = Color.Green;

// Sort based on the sort field attribute

sorter.Sort();

workbook.Version = ExcelVersion.Excel2013;

workbook.SaveAs("Sort.xlsx");

workbook.Close();

excelEngine.Dispose();




{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")

Dim sheet As IWorkbook = workbook.Worksheets(0)

Dim sorter As IDataSort = book.CreateDataSorter()

' Specifies the sort range.

sorter.SortRange = sheet.Range("A2:D16")

' Adds the sort field with column index, sort based on and order by attribute

Dim field1 As ISortField

Field1 = sorter.SortFields.Add(2, SortOn.CellColor,OrderBy.OnTop)

' Sorts the data based on this color

Field1.Color = Color.Red

' Adds the sort field with column index, sort based on and order by attribute

Dim field2 As ISortField

Field2 = sorter.SortFields.Add(2, SortOn.CellColor,OrderBy.OnTop)

' Sorts the data based on this color

Field2.Color = Color.Green

' Sorts the data with the sort field attribute

sorter.Sort()

workbook.Version = ExcelVersion.Excel2013

workbook.SaveAs("Sort.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

## Data Filtering 

Using [AutoFilters](https://support.office.com/en-US/article/Filter-data-in-a-range-or-table-01832226-31b5-4568-8806-38c37dcc180e) , you can filter data to enable quick and easy way to find and work with a subset of data in a range of cells. When you filter data, entire rows are hidden if values in one or more columns don't meet the filtering criteria.

The following code illustrates how to apply simple auto filters.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");

IWorksheet sheet = workbook.Worksheets[0];

// Creating an AutoFilter in the first worksheet. Specifying the AutoFilter range. 

sheet.AutoFilters.FilterRange = sheet.Range["A1:K180"]; 

// Column index to which Autofilter must be applied.

IAutoFilter filter = sheet.AutoFilters[0];

// To apply Top10Number filter, IsTop and IsTop10 must be enabled.

filter.IsTop = true;

filter.IsTop10 = true;

// Setting Top10 filter with number of cell to be filtered from top

filter.Top10Number = 5;

workbook.Version = ExcelVersion.Excel2013;

workbook.SaveAs("Filter.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

Dim workbook As IWorkbook = application.Workbooks. ("Sample.xlsx")

Dim sheet As IWorkbook = workbook.Worksheets(0)

' Creating an AutoFilter in the first worksheet. Specifying the AutoFilter range. 

sheet.AutoFilters.FilterRange = sheet.Range("A1:K180")

' Column index to which Autofilter must be applied.

Dim filter As IAutoFilter = sheet.AutoFilters(0)

' To apply Top10Number filter, IsTop and IsTop10 must be enabled.

filter.IsTop = True

filter.IsTop10 = True

' Setting Top10 filter with number of cell to be filtered from top

filter.Top10Number = 5

workbook.Version = ExcelVersion.Excel2013

workbook.SaveAs("Filter.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

You can also apply data filtering based on conditions. Following code snippets illustrates how to apply filter condition based on first and second condition.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");

IWorksheet sheet = workbook.Worksheets[0];

// Creating an AutoFilter in the first worksheet. Specifying the AutoFilter range.

sheet.AutoFilters.FilterRange = sheet.Range["A1:B323"];

IAutoFilter filter = sheet.AutoFilters[1];

// Specifying first condition.

IAutoFilterCondition firstCondition = filter.FirstCondition;

firstCondition.ConditionOperator = ExcelFilterCondition.Greater;

firstCondition.Double = 100;

//Specfiying second condtion.

IAutoFilterCondition secondCondition = filter.SecondCondition;

secondCondition.ConditionOperator = ExcelFilterCondition.Less;

secondCondition.Double = 200;



workbook.Version = ExcelVersion.Excel2013;

workbook.SaveAs("Filter.xlsx");

workbook.Close();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")

Dim sheet As IWorksheet = workbook.Worksheets(0)

' Creating an AutoFilter in the first worksheet. Specifying the AutoFilter range.

sheet.AutoFilters.FilterRange = sheet.Range("A1:B323")

Dim filter As IAutoFilter = sheet.AutoFilters(1)

' Specifying first condition.

Dim firstCondition As IAutoFilterCondition = filter.FirstCondition

firstCondition.ConditionOperator = ExcelFilterCondition.Greater

firstCondition.Double = 100

'Specfiying second condtion.

Dim secondCondition As IAutoFilterCondition = filter.SecondCondition

secondCondition.ConditionOperator = ExcelFilterCondition.Less

secondCondition.Double = 200

workbook.Version = ExcelVersion.Excel2013

workbook.SaveAs("Filter.xlsx")

workbook.Close()



{% endhighlight %}
{% endtabs %}  

## Hyperlinks

You can create hyperlink in a workbook to provide quick access to web pages, places in your document and files. Hyperlink may target to any one of the following

* Worksheet range
* Web URL
* E-mail
* External files

The following code example illustrates how to insert various hyperlinks.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet sheet = workbook.Worksheets[0];

// Creating a Hyperlink for a Website.

IHyperLink hyperlink = sheet.HyperLinks.Add(sheet.Range["C5"]);

hyperlink.Type = ExcelHyperLinkType.Url;

hyperlink.Address = "http://www.syncfusion.com";

hyperlink.ScreenTip = "To know more About SYNCFUSION PRODUCTS go through this link";

// Creating a Hyperlink for e-mail.

IHyperLink hyperlink1 = sheet.HyperLinks.Add(sheet.Range["C7"]);

hyperlink1.Type = ExcelHyperLinkType.Url;

hyperlink1.Address = "mailto:Username@syncfusion.com";

hyperlink1.ScreenTip = "Send Mail";

// Creating a Hyperlink for Opening Files using type as File.

IHyperLink hyperlink2 = sheet.HyperLinks.Add(sheet.Range["C9"]);

hyperlink2.Type = ExcelHyperLinkType.File;

hyperlink2.Address = @"C:\Program files";

hyperlink2.ScreenTip = "File path";

hyperlink2.TextToDisplay = "Hyperlink for files using File as type";

// Creating a Hyperlink for Opening Files using type as Unc.

IHyperLink hyperlink3 = sheet.HyperLinks.Add(sheet.Range["C11"]);

hyperlink3.Type = ExcelHyperLinkType.Unc;

hyperlink3.Address = @"C:\Documents and Settings";

hyperlink3.ScreenTip = "Click here for files";

hyperlink3.TextToDisplay = "Hyperlink for files using Unc as type";

// Creating a Hyperlink to another cell using type as Workbook.

IHyperLink hyperlink4 = sheet.HyperLinks.Add(sheet.Range["C13"]);

hyperlink4.Type = ExcelHyperLinkType.Workbook;

hyperlink4.Address = "Sheet1!A15";

hyperlink4.ScreenTip = "Click here";

hyperlink4.TextToDisplay = "Hyperlink to cell A15";

workbook.SaveAs("Hyperlink.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim sheet As IWorkbook = workbook.Worksheets(0)

' Creating a Hyperlink for a Website.

Dim hyperlink As IHyperLink = sheet.HyperLinks.Add(sheet.Range("C5"))

hyperlink.Type = ExcelHyperLinkType.Url

hyperlink.Address = "http://www.Syncfusion.com"

hyperlink.ScreenTip = "To know more About SYNCFUSION PRODUCTS go through this link"

' Creating a Hyperlink for e-mail.

Dim hyperlink1 As IHyperLink = sheet.HyperLinks.Add(sheet.Range("C7"))

hyperlink1.Type = ExcelHyperLinkType.Url

hyperlink1.Address = "mailto:Username@syncfusion.com"

hyperlink1.ScreenTip = "Send Mail"

' Creating a Hyperlink for Opening Files using type as File.

Dim hyperlink2 As IHyperLink = sheet.HyperLinks.Add(sheet.Range("C9"))

hyperlink2.Type = ExcelHyperLinkType.File

hyperlink2.Address = "C:\Program files"

hyperlink2.ScreenTip = "File path"

hyperlink2.TextToDisplay = "Hyperlink for files using File as type"

' Creating a Hyperlink for Opening Files using type as Unc.

Dim hyperlink3 As IHyperLink = sheet.HyperLinks.Add(sheet.Range("C11"))

hyperlink3.Type = ExcelHyperLinkType.Unc

hyperlink3.Address = "C:\Documents and Settings"

hyperlink3.ScreenTip = "Click here for files"

hyperlink3.TextToDisplay = "Hyperlink for files using Unc as type"

' Creating a Hyperlink to another cell using type as Workbook.

Dim hyperlink4 As IHyperLink = sheet.HyperLinks.Add(sheet.Range("C13"))

hyperlink4.Type = ExcelHyperLinkType.Workbook

hyperlink4.Address = "Sheet1!A15"

hyperlink4.ScreenTip = "Click here"

hyperlink4.TextToDisplay = "Hyperlink to cell A15"

workbook.SaveAs("Hyperlink.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

### Modifying Existing Hyperlink

You can modify the properties of existing hyperlink by accessing the Hyperlinks collection of the IRange instance.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");

IWorksheet sheet = workbook.Worksheets[0];

// Modifying hyperlink’s text to display.

IHyperLink hyperlink = sheet.Range["C5"].Hyperlinks[0];

hyperlink.TextToDisplay = "Syncfusion";

workbook.Version = ExcelVersion.Excel2013;

workbook.SaveAs("Hyperlink.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")

Dim sheet As IWorksheet = workbook.Worksheets(0)

' Modifying hyperlink’s text to display.

Dim hyperlink As IHyperLink = sheet.Range("C5").Hyperlinks(0)

hyperlink.TextToDisplay = "Syncfusion"

workbook.Version = ExcelVersion.Excel2013

workbook.SaveAs("Hyperlink.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

### Removing Hyperlink

You can remove a hyperlink from a range by accessing the Hyperlinks collection of the IRange instance.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");

IWorksheet sheet = workbook.Worksheets[0];

// Removing Hyperlink from Range "C7"

sheet.Range["C7"].Hyperlinks.RemoveAt(0);

workbook.Version = ExcelVersion.Excel2013;

workbook.SaveAs("Hyperlink.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")

Dim sheet As IWorksheet = workbook.Worksheets(0)

' Removing Hyperlink from Range "C7"

sheet.Range("C7").Hyperlinks.RemoveAt(0)

workbook.Version = ExcelVersion.Excel2013

workbook.SaveAs("Hyperlink.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  



