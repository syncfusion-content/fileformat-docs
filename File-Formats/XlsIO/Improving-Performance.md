---
title: Improving Performance
description: Brief about improving performance in XlsIO
platform: File-Formats
control: XlsIO
documentation: UG
---
# Improving Performance

This section gives you an idea for improving performance while developing with XlsIO. 

## UsedRange

Get **UsedRange** globally. It is recommended to get the UsedRange in loops as follows

{% tabs %}  

{% highlight c# %}
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

{% highlight vb %}
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

Use IMigrantRange instead of IRange to optimize performance while dealing with large data. LINK- Reference to Tips section.

## Styles

Use global styles, rather than using different cell styles for each cell/range. LINK- Reference to global style section.

Use Begin and End call while using more than one global style for a worksheet.

{% tabs %}  

{% highlight c# %}
//Defining body style

IStyle bodyStyle = workbook.Styles.Add("BodyStyle");

bodyStyle.BeginUpdate();

bodyStyle.Color = Color.FromArgb(239, 243, 247);

bodyStyle.Borders[ExcelBordersIndex.EdgeLeft].LineStyle = ExcelLineStyle.Thin;

bodyStyle.Borders[ExcelBordersIndex.EdgeRight].LineStyle = ExcelLineStyle.Thin;

bodyStyle.EndUpdate();



{% endhighlight %}

{% highlight vb %}
'Defining body style

Dim bodyStyle As IStyle = workbook.Styles.Add("BodyStyle")

bodyStyle.BeginUpdate()

bodyStyle.Color = Color.FromArgb(239, 243, 247)

bodyStyle.Borders(ExcelBordersIndex.EdgeLeft).LineStyle = ExcelLineStyle.Thin

bodyStyle.Borders(ExcelBordersIndex.EdgeRight).LineStyle = ExcelLineStyle.Thin

bodyStyle.EndUpdate()



{% endhighlight %}

  {% endtabs %}  

## AutoFit 

Minimize AutoFit manipulations which reduces the time consumption.

## Importing DataTable

**ImportDataTable** overload method which has **ImportonSave** argument allows you to import data with less memory consumption along with improve method performance by serializing the data directly on save method. This options is preferred for larger data that need to be import in short time.

{% tabs %}  

{% highlight c# %}
DataTable table = Worksheet.ExportDataTable(1, 1, Worksheet.UsedRange.LastRow, Worksheet.UsedRange.LastColumn, ExcelExportDataTableOptions.DetectColumnTypes); 

//Enabling the import on save options.

workbook.Worksheets[0].ImportDataTable(table, 1, 1, true);

workbook.Version = ExcelVersion.Excel2013; 

workbook.SaveAs("Output.xlsx");



{% endhighlight %}

{% highlight vb %}
Dim table As DataTable = Worksheet.ExportDataTable(1, 1, Worksheet.UsedRange.LastRow, Worksheet.UsedRange.LastColumn, ExcelExportDataTableOptions.DetectColumnTypes)

'Enabling the import on save options.

workbook.Worksheets(0).ImportDataTable(table, 1, 1, True)

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

{% highlight c# %}
// List data validation for entire column

IDataValidation validation = sheet.Range["A3"].EntireColumn.DataValidation;

validation.BeginUpdate();

validation.DataRange = sheet.Range["D1:D56"];

validation.IsEmptyCellAllowed = true;

validation.IsListInFormula = false;

validation.EndUpdate();



{% endhighlight %}

{% highlight vb %}
' List data validation for entire column

Dim validation As IDataValidation = sheet.Range("A3").EntireColumn.DataValidation

validation.BeginUpdate()

validation.DataRange = sheet.Range("D1:D56")

validation.IsEmptyCellAllowed = True

validation.IsListInFormula = False

validation.EndUpdate()



{% endhighlight %}

  {% endtabs %}  

