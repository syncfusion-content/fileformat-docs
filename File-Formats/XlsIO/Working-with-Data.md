---
title: Working with Data
description: Briefs about working with data in XlsIO
platform: File-Formats
control: XlsIO
documentation: UG
---
# Working with Data 

## Importing Data to Worksheets

XlsIO provides the ability to import data into a worksheet from the following data.

* Data Table
* Data Column
* Data View
* Business Objects
* Array

### Import Data from DataTable


The following code snippet illustrates on how to import a DataTable into a worksheet using **ImportDataTable** method.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet worksheet = workbook.Worksheets[0];

DataTable table = SampleDataTable();

//Import DataTable to the worksheet.

worksheet.ImportDataTable(table, true, 1, 1);

workbook.SaveAs("ImportFromDT.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim worksheet As IWorksheet = workbook.Worksheets(0)

Dim table As DataTable = sampleDataTable()

'Import DataTable to the worksheet.

worksheet.ImportDataTable(table, True, 1, 1)

workbook.SaveAs("ImportFromDT.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

### Import Data from DataColumn

The following code snippet illustrates how to import DataColumn into a worksheet using **ImportDataColumn** method.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet worksheet = workbook.Worksheets[0];

DataTable table = SampleDataTable();

//Import Data Column to the worksheet.

DataColumn column = table.Columns[0];

worksheet.ImportDataColumn(column, true, 1, 1);

workbook.SaveAs("ImportFromDT.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim worksheet As IWorksheet = workbook.Worksheets(0)

Dim table As DataTable = sampleDataTable()

'Import DataColumn to the worksheet.

Dim column As DataColumn = table.Columns(0)

worksheet.ImportDataColumn(column, True, 1, 1)

workbook.SaveAs("ImportFromDT.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

### Import Data from DataView

The following code snippet illustrates how to import DataView into a worksheet using **ImportDataView** method.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet worksheet = workbook.Worksheets[0];

DataTable table = SampleDataTable();

//Import Dataview to the worksheet.

DataView view = table.DefaultView;

worksheet.ImportDataView(view, true, 1, 1);

workbook.SaveAs("ImportFromDT.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim worksheet As IWorksheet = workbook.Worksheets(0)

'Initialize the DataTable.

Dim table As DataTable = sampleDataTable()

'Import Dataview to the worksheet.

Dim view As DataView = table.DefaultView

worksheet.ImportDataView(view, True, 1, 1)

workbook.SaveAs("ImportFromDT.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

### Import Data from Business Objects

Essential XlsIO allows you to import data directly from Business Objects as shown below. 

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet worksheet = workbook.Worksheets[0];

//Import the data to worksheet.
IList<Customer> reports = GetSalesReports();
worksheet.ImportData(reports, 2, 1, false);

workbook.SaveAs("ImportFromDT.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim worksheet As IWorksheet = workbook.Worksheets(0)

'Import the data to worksheet.

Dim reports As IList(Of Customer) = GetSalesReports()

worksheet.ImportData(reports, 2, 1, False)

workbook.SaveAs("ImportFromDT.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

The following code snippet provides supporting methods & class for the above code.

{% tabs %}  
{% highlight c# %}
public static List<Report> GetSalesReports()

{

List<Report> reports = new List<Report>();

reports.Add(new Report("Andy Bernard", "45000", "58000"));

reports.Add(new Report("Jim Halpert", "34000", "65000"));

reports.Add(new Report("Karen Fillippelli", "75000", "64000"));

reports.Add(new Report("Phyllis Lapin", "56500", "33600" ));

reports.Add(new Report("Stanley Hudson", "46500", "52000"));

return reports;

}

public class Report

{

public string SalesPerson { get; set; }

public string SalesJanJun { get; set; }

public string SalesJulDec { get; set; }

public Report(string name, string janToJun, string julToDec)

{

SalesPerson = name;

SalesJanJun = janToJun;

SalesJulDec = julToDec;

}

}



{% endhighlight %}

{% highlight vb %}
Public Shared Function GetSalesReports() As List(Of Report)

Dim reports As New List(Of Report)()

reports.Add(New Report("Andy Bernard", "45000", "58000"))

reports.Add(New Report("Jim Halpert", "34000", "65000"))

reports.Add(New Report("Karen Fillippelli", "75000", "64000"))

reports.Add(New Report("Phyllis Lapin", "56500", "33600"))

reports.Add(New Report("Stanley Hudson", "46500", "52000"))

Return reports

End Function



Public Class Report

Public Property SalesPerson() As String

Get

Return m_SalesPerson

End Get

Set(value As String)

m_SalesPerson = Value

End Set

End Property

Private m_SalesPerson As String

Public Property SalesJanJun() As String

Get

Return m_SalesJanJun

End Get

Set(value As String)

m_SalesJanJun = Value

End Set

End Property

Private m_SalesJanJun As String

Public Property SalesJulDec() As String

Get

Return m_SalesJulDec

End Get

Set(value As String)

m_SalesJulDec = Value

End Set

End Property

Private m_SalesJulDec As String

Public Sub New(name As String, janToJun As String, julToDec As String)

SalesPerson = name

SalesJanJun = janToJun

SalesJulDec = julToDec

End Sub

End Class



{% endhighlight %}
{% endtabs %}  

### Import Data from Array

The following code snippet shows how to import array of data into a worksheet using **ImportArray** method.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet worksheet = workbook.Worksheets[0];

//Initialize the Object Array.

object[] array = new object[4]{"Total Income", "Actual Expense", "Expected Expenses", "Profit"};

//Import the Object Array to Sheet

worksheet.ImportArray(array, 1, 1, false);

workbook.SaveAs("ImportFromDT.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim worksheet As IWorksheet = workbook.Worksheets(0)

'Initialize the Array Object.

Dim array() As Object = New Object(4) {"Total Income", "Actual Expense", "Expected Expenses", "Profit"}

'Import the Array Object to Sheet.

worksheet.ImportArray(array, 1, 1, False)

workbook.SaveAs("ImportFromDT.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

## Exporting from Worksheet to Data Table 

XlsIO allows to export the sheet data to a **DataTable** by using the **ExportDataTable****()** method. This method provides various options that allows to export data with specific requirement through ExcelExportDataTableOptions. 

The following code snippet illustrates on how to export data from worksheet to Data grid using **DataTable**.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet worksheet = workbook.Worksheets[0];

// Read data from the worksheet and Export to the DataTable.

DataTable customersTable = worksheet.ExportDataTable(worksheet.UsedRange, ExcelExportDataTableOptions.ColumnNames);

//binding exported DataTable to data grid, likewise it can binded to any 

//User interface control which supports binding.

this.dataGrid1.DataSource = customersTable;

workbook.SaveAs("ExportToGrid.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim sheet As IWorkbook = workbook.Worksheets(0)

'Read data from the worksheet and Export to the DataTable.

Dim customersTable As DataTable = sheet.ExportDataTable(sheet.UsedRange, ExcelExportDataTableOptions.ColumnNames)

'binding exported DataTable to data grid, likewise it can binded to any 

'User interface control which supports binding.

Me.dataGrid1.DataSource = customersTable

workbook.SaveAs("ExportToGrid.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  
