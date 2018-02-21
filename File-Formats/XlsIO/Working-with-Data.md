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

//Import DataView to the worksheet.
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

'Import DataView to the worksheet.
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

	Private m_SalesPerson As String
	Private m_SalesJanJun As String	
	Private m_SalesJulDec As String
	
	Public Property SalesPerson() As String
	Get
		Return m_SalesPerson
	End Get
	
	Set(value As String)
		m_SalesPerson = Value
	End Set
	End Property

	Public Property SalesJanJun() As String
	Get
		Return m_SalesJanJun
	End Get

	Set(value As String)
		m_SalesJanJun = Value
	End Set
	End Property

	Public Property SalesJulDec() As String
	Get
		Return m_SalesJulDec
	End Get

	Set(value As String)
		m_SalesJulDec = Value
	End Set
	End Property

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

//Binding exported DataTable to data grid, likewise it can binded to any 
//user interface control which supports binding.
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

'Binding exported DataTable to data grid, likewise it can binded to any 
'user interface control which supports binding.

Me.dataGrid1.DataSource = customersTable

workbook.SaveAs("ExportToGrid.xlsx")
workbook.Close()
excelEngine.Dispose()
{% endhighlight %}
{% endtabs %}  

## Exporting from Worksheet to Business Objects 

XlsIO allows to export the sheet data to a **Business Objects** by using the **ExportData<T>****()** method. This method Exports Excel data into business objects from existing or newly created Excel document by matching set of properties and [DisplayNameAttribute](https://docs.microsoft.com/en-us/dotnet/api/system.componentmodel.displaynameattribute?view=netframework-4.7.1).

The following code snippet illustrates on how to export worksheet data into Business Objects using **ExportData<T>**.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
application.DefaultVersion = ExcelVersion.Excel2016;
IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
IWorksheet worksheet = workbook.Worksheets[0];

//Export worksheet data into Business Objects
List<Report> businessObjects = worksheet.ExportData<Report>(1, 1, 10, 3);

workbook.SaveAs("BusinessObjects.xlsx");
workbook.Close();
excelEngine.Dispose();
{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine
Dim application As IApplication = excelEngine.Excel
application.DefaultVersion = ExcelVersion.Excel2016
Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
Dim worksheet As IWorkbook = workbook.Worksheets(0)

'Export worksheet data into Business Objects
Dim businessObjects As List(Of Report) =worksheet.ExportData<Report>(1, 1, 10, 3)

workbook.SaveAs("BusinessObjects.xlsx")
workbook.Close()
excelEngine.Dispose()
{% endhighlight %}
{% endtabs %}  

The following code snippet provides supporting class for the above code.

{% tabs %}  
{% highlight c# %}
public class Report
{
    [DisplayNameAttribute("Sales Person Name")]
	public string SalesPerson { get; set; }
	public string SalesJanJun { get; set; }
	public string SalesJulDec { get; set; }

	public Report()
	{

	}
}
{% endhighlight %}

{% highlight vb %}
Public Class Report

	Private m_SalesPerson As String
	Private m_SalesJanJun As String	
	Private m_SalesJulDec As String
	
	<DisplayNameAttribute("Sales Person Name")>
	Public Property SalesPerson() As String
	Get
		Return m_SalesPerson
	End Get

	Set(value As String)
		m_SalesPerson = Value
	End Set
	End Property

	Public Property SalesJanJun() As String
	Get
		Return m_SalesJanJun
	End Get

	Set(value As String)
		m_SalesJanJun = Value
	End Set
	End Property

	Public Property SalesJulDec() As String
	Get
		Return m_SalesJulDec
	End Get

	Set(value As String)
		m_SalesJulDec = Value
	End Set
	End Property

	Public Sub New()

	End Sub

End Class
{% endhighlight %}
{% endtabs %} 

## Importing Data from Microsoft Grid Controls to Worksheet

XlsIO provides support to import data from various Microsoft grid controls with its cell formatting. The supported grid controls are: 

* DataGrid
* GridView
* DataGridView

### DataGrid

Imports data from Microsoft DataGrid control with its header and cell formatting to Excel worksheet. The following code illustrates how to import data from Microsoft DataGrid control to worksheet.
 
N> GetDataTable() method returns DataTable of applicable data to import.

{% tabs %}
{% highlight c# %}
//Initialize DataGrid control.
DataGrid dataGrid = new DataGrid();
dataGrid.DataSource = GetDataTable();

ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
application.DefaultVersion = ExcelVersion.Excel2013;
IWorkbook workbook = application.Workbooks.Create();
IWorksheet worksheet = workbook.Worksheets[0];

//Import data from DataGrid control.
worksheet.ImportDataGrid(dataGrid, 1, 1, true, true);

workbook.SaveAs("Output.xlsx");
workbook.Close();
excelEngine.Dispose();
{% endhighlight %}

{% highlight vb %}
'Initialize DataGrid control.
Dim dataGrid As DataGrid = New DataGrid()
dataGrid.DataSource = GetDataTable()

Dim excelEngine As New ExcelEngine()
Dim application As IApplication = excelEngine.Excel
application.DefaultVersion = ExcelVersion.Excel2013
Dim workbook As IWorkbook = application.Workbooks.Create()
Dim worksheet As IWorksheet = workbook.Worksheets(0)

'Import data from DataGrid control.
worksheet.ImportDataGrid(dataGrid, 1, 1, True, True)

workbook.SaveAs("Output.xlsx")

workbook.Close()
excelEngine.Dispose()
{% endhighlight %}
{% endtabs %}

### GridView

Imports data from Microsoft GridView control with its header and cell formatting to Excel worksheet. The following code illustrates how to import data from Microsoft GridView control to worksheet.

{% tabs %}
{% highlight c# %}
//Initialize GridView control.
GridView gridView = new GridView();
gridView.DataSource = GetDataTable();
gridView.DataBind();

ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
application.DefaultVersion = ExcelVersion.Excel2013;
IWorkbook workbook = application.Workbooks.Create();
IWorksheet worksheet = workbook.Worksheets[0];

//Import data from GridView control.
worksheet.ImportGridView(gridView, 1, 1, true, true);

workbook.SaveAs("Output.xlsx");
workbook.Close();
excelEngine.Dispose();
{% endhighlight %}

{% highlight vb %}
'Initialize GridView control.
Dim gridView As GridView = New GridView ()
gridView.DataSource = GetDataTable()
gridView.DataBind()

Dim excelEngine As New ExcelEngine()
Dim application As IApplication = excelEngine.Excel
application.DefaultVersion = ExcelVersion.Excel2013
Dim workbook As IWorkbook = application.Workbooks.Create()
Dim worksheet As IWorksheet = workbook.Worksheets(0)

'Import data from GridView control.
worksheet.ImportGridView(gridView, 1, 1, True, True)

workbook.SaveAs("Output.xlsx")
workbook.Close()
excelEngine.Dispose()
{% endhighlight %}
{% endtabs %}

### DataGridView

Imports data from Microsoft DataGridView control with its header and cell formatting to Excel worksheet. In addition, this API imports sorted data applied in the control. The following code illustrates how to import data from Microsoft DataGridView control to worksheet.
 
{% tabs %}
{% highlight c# %}
//Initialize DataGridView control.
DataGridView dataGridView = new DataGridView();
dataGridView.DataSource = GetDataTable();

//Apply sorting.
dataGridView.Sort(dataGridView.Columns[1], System.ComponentModel.ListSortDirection.Ascending);

ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
application.DefaultVersion = ExcelVersion.Excel2013;
IWorkbook workbook = application.Workbooks.Create();
IWorksheet worksheet = workbook.Worksheets[0];

//Import data from DataGridView control.
worksheet.ImportDataGridView(dataGridView, 1, 1, true, true);

workbook.SaveAs("Output.xlsx");
workbook.Close();
excelEngine.Dispose();
{% endhighlight %}

{% highlight vb %}
'Initialize DataGridView control.
Dim dataGridView As DataGridView = New DataGridView()
dataGridView.DataSource = GetDataTable()

'Apply sorting.
dataGridView.Sort(dataGridView.Columns(1), System.ComponentModel.ListSortDirection.Ascending)

Dim excelEngine As New ExcelEngine()
Dim application As IApplication = excelEngine.Excel
application.DefaultVersion = ExcelVersion.Excel2013
Dim workbook As IWorkbook = application.Workbooks.Create()
Dim worksheet As IWorksheet = workbook.Worksheets(0)

'Import data from DataGridView control.
worksheet.ImportDataGridView(dataGridView, 1, 1, True, True)

workbook.SaveAs("Output.xlsx")
workbook.Close()
excelEngine.Dispose()
{% endhighlight %}
{% endtabs %}