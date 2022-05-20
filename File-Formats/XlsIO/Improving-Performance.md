---
title: Improving Performance | Syncfusion
description: This section illustrates about improving the performance in Syncfusion Excel library (Essential XlsIO).
platform: File-Formats
control: XlsIO
documentation: UG
---
# Improving Performance

This section gives you an idea for improving performance while developing with XlsIO. 

## UsedRange

Get **UsedRange** globally. It is recommended to get the UsedRange in loops as follows

{% tabs %}  

{% highlight c# tabtitle="C#" %}
int lastRow = sheet.UsedRange.LastRow;

for(int i=0;i<lastRow;i++)

{

//codes

}

//Do not use like below.

for(int i = 0;i<sheet.UsedRange.LastRow;i++)

{

//codes

}





{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Dim lastRow As Integer = sheet.UsedRange.LastRow

For i As Integer = 0 To lastRow - 1

'codes

Next

'Do not use like below.

For i As Integer = 0 To sheet.UsedRange.LastRow - 1

'codes

Next



{% endhighlight %}

  {% endtabs %}  

## Range Access

Use IMigrantRange instead of IRange to optimize performance while dealing with large data.

The **IMigrantRange** interface can be used to access and manipulate worksheet range. This is an optimal method of writing values with better memory performance. 

The following code example illustrates how the **IMigrantRange** is accessed.

{% tabs %}  

{% highlight c# tabtitle="C#" %}
IMigrantRange migrantRange = workbook.Worksheets[0].MigrantRange; 

int rowCount = 10;
int colCount = 10; 

// Writing Data.
for (int row = 1; row <= rowCount; row++)
{
for (int column = 1; column <= colCount; column++)
{
// Writing values.

migrantRange.ResetRowColumn(row, column);

// Setting value of this migrant range which is similar to IRange object.

migrantRange.Value = "Syncfusion";        

}
}



{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Dim rowCount As Integer = 10
Dim colCount As Integer = 10

'Writing Data.
Dim row As Integer
Dim migrantRange As IMigrantRange = workbook.Worksheets(0).MigrantRange
For row = 1 To rowCount Step row + 1
Dim column As Integer
For column = 1 To colCount Step column + 1
'Writing values.
migrantRange.ResetRowColumn(row, column)

' Setting value of this migrant range which is similar to IRange object.

migrantRange.Value = "Syncfusion"

Next
Next



{% endhighlight %}

  {% endtabs %}  

**IMigrantRange** provides us a SetValue method in which different value for the range can be assigned. Following code snippet illustrates regarding this.

{% tabs %}  

{% highlight c# tabtitle="C#" %}
ExcelEngine excelEngine = new ExcelEngine();

excelEngine.Excel.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = excelEngine.Excel.Workbooks.Create();

IWorksheet sheet = workbook.Worksheets[0];

IMigrantRange migrantRange = workbook.Worksheets[0].MigrantRange;

// Writing values.

migrantRange.ResetRowColumn(1, 1);

//Setting boolean value

migrantRange.SetValue(true);

migrantRange.ResetRowColumn(1, 2);

//Setting DateTime value

migrantRange.SetValue(DateTime.Now);

migrantRange.ResetRowColumn(1, 3);

//Setting double value

migrantRange.SetValue(5.5);

migrantRange.ResetRowColumn(1, 4);

//Setting int value

migrantRange.SetValue(5);

migrantRange.ResetRowColumn(1, 5);

//Setting string value

migrantRange.SetValue("Syncfusion");

workbook.Version = ExcelVersion.Excel2013;

workbook.SaveAs("MigrantRange.xlsx");

workbook.Close();

excelEngine.Dispose();            



{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Dim excelEngine As New ExcelEngine()

excelEngine.Excel.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = excelEngine.Excel.Workbooks.Create()

Dim sheet As IWorksheet = workbook.Worksheets(0)

Dim migrantRange As IMigrantRange = workbook.Worksheets(0).MigrantRange

' Writing values.

migrantRange.ResetRowColumn(1, 1)

'Setting boolean value

migrantRange.SetValue(True)

migrantRange.ResetRowColumn(1, 2)

'Setting DateTime value

migrantRange.SetValue(DateTime.Now)

migrantRange.ResetRowColumn(1, 3)

'Setting double value

migrantRange.SetValue(5.5)

migrantRange.ResetRowColumn(1, 4)

'Setting int value

migrantRange.SetValue(5)

migrantRange.ResetRowColumn(1, 5)

'Setting string value

migrantRange.SetValue("Syncfusion")

workbook.Version = ExcelVersion.Excel2013

workbook.SaveAs("MigrantRange.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %} 

## Styles

Use global styles, rather than using different cell styles for each cell/range. See [Applying global styles](/file-formats/xlsio/working-with-cell-or-range-formatting#apply-global-style).

Use Begin and End call while using more than one global style for a worksheet.

{% tabs %}  

{% highlight c# tabtitle="C#" %}
//Defining body style

IStyle bodyStyle = workbook.Styles.Add("BodyStyle");

bodyStyle.BeginUpdate();

bodyStyle.Color = Color.FromArgb(239, 243, 247);

bodyStyle.Borders[ExcelBordersIndex.EdgeLeft].LineStyle = ExcelLineStyle.Thin;

bodyStyle.Borders[ExcelBordersIndex.EdgeRight].LineStyle = ExcelLineStyle.Thin;

bodyStyle.EndUpdate();



{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Defining body style

Dim bodyStyle As IStyle = workbook.Styles.Add("BodyStyle")

bodyStyle.BeginUpdate()

bodyStyle.Color = Color.FromArgb(239, 243, 247)

bodyStyle.Borders(ExcelBordersIndex.EdgeLeft).LineStyle = ExcelLineStyle.Thin

bodyStyle.Borders(ExcelBordersIndex.EdgeRight).LineStyle = ExcelLineStyle.Thin

bodyStyle.EndUpdate()



{% endhighlight %}

  {% endtabs %}  
  
### Set default row style and default column style

Performance can be improved to a greater extent by setting default styles for rows and columns instead of setting cell styles for each cells in one or more rows and columns.

{% tabs %}  

{% highlight c# tabtitle="C#" %}
//Set default styles for rows and columns

IStyle style = workbook.Styles.Add("Style"); 
style.Font.FontName = "Arial"; 
style.Font.Size = 10; 

//Set default style for the entire row (3rd row)
worksheet.SetDefaultRowStyle(3, style);

//Set default style for entire rows from 4 to 8 (4th row to 8th row)
worksheet.SetDefaultRowStyle(4, 8, style);

//Set default style for the entire column A (1st column)
worksheet.SetDefaultColumnStyle(1, style);

//Set default style for entire columns from B to L (2nd column to 12th column)
worksheet.SetDefaultColumnStyle(2, 12, style);

//Do not use like below when an entire row/column or a number of rows/columns need to be formatted with common styles, as it will affect performance

//worksheet.Range["4:8"].CellStyle.Font.FontName = "Arial"; 
//worksheet.Range["4:8"].CellStyle.Font.Size = 10;

//worksheet.Range["A:L"].CellStyle.Font.FontName = "Arial"; 
//worksheet.Range["A:L"].CellStyle.Font.Size = 10;

//CellStyle property can be used only when one cell or a range of cells has to be formatted like below

//worksheet.Range["D2"].CellStyle.Font.FontName = "Arial"; 
//worksheet.Range["A1:L2"].CellStyle.Font.Size = 10;

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Set default styles for rows and columns

Dim style As IStyle = workbook.Styles.Add("Style")
style.Font.FontName = "Arial"
style.Font.Size = 10

'Set default style for the entire row (3rd row)
worksheet.SetDefaultRowStyle(3, style)

'Set default style for entire rows from 4 to 8 (4th row to 8th row)
worksheet.SetDefaultRowStyle(4, 8, style)

'Set default style for the entire column A (1st column)
worksheet.SetDefaultColumnStyle(1, style)

'Set default style for entire columns from B to L (2nd column to 12th column)
worksheet.SetDefaultColumnStyle(2, 12, style)

'Do not use like below when an entire row/column or a number of rows/columns need to be formatted with common styles as it will affect performance

'worksheet.Range("4:8").CellStyle.Font.FontName = "Arial"
'worksheet.Range("4:8").CellStyle.Font.Size = 10

'worksheet.Range("A:L").CellStyle.Font.FontName = "Arial"
'worksheet.Range("A:L").CellStyle.Font.Size = 10

'CellStyle property can be used only when one cell or a range of cells has to be formatted like below

'worksheet.Range("D2").CellStyle.Font.FontName = "Arial"
'worksheet.Range("A1:L2").CellStyle.Font.Size = 10

{% endhighlight %}

{% endtabs %}  

## AutoFit 

Minimize AutoFit manipulations which reduces the time consumption.

For improved performance in Excel to PDF conversion, it is recommended to set the **IApplication.SkipAutoFitRow** property as TRUE.

{% tabs %}  

{% highlight c# tabtitle="C#" %}

ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;

//Skips AutoFitting of rows during conversion

application.SkipAutoFitRow = true;

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

Dim excelEngine As ExcelEngine = New ExcelEngine()
Dim application As IApplication = excelEngine.Excel

'Skips AutoFitting of rows during conversion

application.SkipAutoFitRow = True

{% endhighlight %}

  {% endtabs %} 

## Importing DataTable

**ImportDataTable** overload method which has **ImportOnSave** argument allows you to import data with less memory consumption along with improved method performance by serializing the data directly on save method. This option is preferred for larger data that need to be imported in short time.

{% tabs %}  

{% highlight c# tabtitle="C#" %}
DataTable table = Worksheet.ExportDataTable(1, 1, Worksheet.UsedRange.LastRow, Worksheet.UsedRange.LastColumn, ExcelExportDataTableOptions.DetectColumnTypes); 

//Enable ImportOnSave option along with column header.

workbook.Worksheets[0].ImportDataTable(table, 1, 1, true, true);

workbook.Version = ExcelVersion.Excel2013; 

workbook.SaveAs("Output.xlsx");



{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Dim table As DataTable = Worksheet.ExportDataTable(1, 1, Worksheet.UsedRange.LastRow, Worksheet.UsedRange.LastColumn, ExcelExportDataTableOptions.DetectColumnTypes)

'Enable ImportOnSave option along with column header.

workbook.Worksheets(0).ImportDataTable(table, 1, 1, True, True)

workbook.Version = ExcelVersion.Excel2013

workbook.SaveAs("Output.xlsx")



{% endhighlight %}

  {% endtabs %}  



**Limitations** 

* Cannot modify data dynamically
* Styles cannot be applied
* Table style cannot be applied
* Existing sheet data will be lost

## Data Validation

Use of BeginUpdate and EndUpdate methods for large blocks of Data Validation greatly improves the performance.

{% tabs %}  

{% highlight c# tabtitle="C#" %}
// List data validation for entire column

IDataValidation validation = sheet.Range["A3"].EntireColumn.DataValidation;

validation.BeginUpdate();

validation.DataRange = sheet.Range["D1:D56"];

validation.IsEmptyCellAllowed = true;

validation.IsListInFormula = false;

validation.EndUpdate();



{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
' List data validation for entire column

Dim validation As IDataValidation = sheet.Range("A3").EntireColumn.DataValidation

validation.BeginUpdate()

validation.DataRange = sheet.Range("D1:D56")

validation.IsEmptyCellAllowed = True

validation.IsListInFormula = False

validation.EndUpdate()



{% endhighlight %}

  {% endtabs %}  

