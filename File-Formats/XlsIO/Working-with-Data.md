---
title: Working with Data | Syncfusion
description: Learn how to import data to Excel file from ADO.NET objects, Collections, Array; and how to export data from Excel to ADO.NET objects or collections.
platform: File-Formats
control: XlsIO
documentation: UG
---
# Working with Data Objects 

## Importing Data to Worksheets

XlsIO provides the ability to import data into a worksheet from the following data.

* Data Table
* Data Column
* Data View
* Collection Objects
* Nested Collection Objects
* Array

### Import Data from DataTable

The following code snippet illustrates on how to import a DataTable into a worksheet using **ImportDataTable** method.

{% tabs %}  
{% highlight c# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Initialize the DataTable
  DataTable table = SampleDataTable();
  //Import DataTable to the worksheet.
  worksheet.ImportDataTable(table, true, 1, 1);

  workbook.SaveAs("ImportFromDT.xlsx");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Initialize the DataTable
  Dim table As DataTable = sampleDataTable()
  'Import DataTable to the worksheet
  worksheet.ImportDataTable(table, True, 1, 1)

  workbook.SaveAs("ImportFromDT.xlsx")
End Using
{% endhighlight %}

{% highlight UWP %}
//XlsIO supports importing of data from data table to worksheet in Windows Forms, WPF, ASP.NET, ASP.NET MVC and ASP.NET Core (2.0 onwards) platforms alone.
{% endhighlight %}

{% highlight ASP.NET Core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Initialize the DataTable
  DataTable table = SampleDataTable();
  //Import DataTable to the worksheet
  worksheet.ImportDataTable(table, true, 1, 1);

  //Saving the workbook as stream
  FileStream stream = new FileStream("ImportFromDT.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight Xamarin %}
//XlsIO supports importing of data from data table to worksheet in Windows Forms, WPF, ASP.NET, ASP.NET MVC and ASP.NET Core (2.0 onwards) platforms alone.
{% endhighlight %}
{% endtabs %}  

### Import Data from DataColumn

The following code snippet illustrates how to import DataColumn into a worksheet using **ImportDataColumn** method.

{% tabs %}  
{% highlight c# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Initialize the DataTable
  DataTable table = SampleDataTable();
  //Import Data Column to the worksheet
  DataColumn column = table.Columns[0];
  worksheet.ImportDataColumn(column, true, 1, 1);
  
  workbook.SaveAs("ImportFromDT.xlsx");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Initialize the DataTable
  Dim table As DataTable = sampleDataTable()
  'Import DataColumn to the worksheet
  Dim column As DataColumn = table.Columns(0)
  worksheet.ImportDataColumn(column, True, 1, 1)

  workbook.SaveAs("ImportFromDT.xlsx")
End Using
{% endhighlight %}

{% highlight UWP %}
//XlsIO supports importing data column to worksheet in Windows Forms, WPF, ASP.NET, ASP.NET MVC and ASP.NET Core (2.0 onwards) platforms alone.
{% endhighlight %}

{% highlight ASP.NET Core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Initialize the DataTable
  DataTable table = SampleDataTable();
  //Import Data Column to the worksheet
  DataColumn column = table.Columns[0];
  worksheet.ImportDataColumn(column, true, 1, 1);

  //Saving the workbook as stream
  FileStream stream = new FileStream("ImportFromDT.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight Xamarin %}
//XlsIO supports importing data column to worksheet in Windows Forms, WPF, ASP.NET, ASP.NET MVC and ASP.NET Core (2.0 onwards) platforms alone.
{% endhighlight %}
{% endtabs %}  

### Import Data from DataView

The following code snippet illustrates how to import DataView into a worksheet using **ImportDataView** method.

{% tabs %}  
{% highlight c# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Initialize the DataTable
  DataTable table = SampleDataTable();
  //Import DataView to the worksheet
  DataView view = table.DefaultView;
  worksheet.ImportDataView(view, true, 1, 1);

  workbook.SaveAs("ImportFromDT.xlsx");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Initialize the DataTable
  Dim table As DataTable = sampleDataTable()
  'Import DataView to the worksheet
  Dim view As DataView = table.DefaultView
  worksheet.ImportDataView(view, True, 1, 1)

  workbook.SaveAs("ImportFromDT.xlsx")
End Using
{% endhighlight %}

{% highlight UWP %}
//XlsIO supports importing data view to worksheet in Windows Forms, WPF, ASP.NET, ASP.NET MVC and ASP.NET Core (2.0 onwards) platforms alone.
{% endhighlight %}

{% highlight ASP.NET Core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Initialize the DataTable
  DataTable table = SampleDataTable();
  //Import DataView to the worksheet
  DataView view = table.DefaultView;
  worksheet.ImportDataView(view, true, 1, 1);

  //Saving the workbook as stream
  FileStream stream = new FileStream("ImportFromDT.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight Xamarin %}
//XlsIO supports importing data view to worksheet in Windows Forms, WPF, ASP.NET, ASP.NET MVC and ASP.NET Core (2.0 onwards) platforms alone.
{% endhighlight %}
{% endtabs %}  

### Import Data from Collection Objects

Essential XlsIO allows you to import data directly from Collection Objects as shown below.

{% tabs %}  
{% highlight c# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Import the data to worksheet
  IList<Customer> reports = GetSalesReports();
  worksheet.ImportData(reports, 2, 1, false);

  workbook.SaveAs("ImportFromDT.xlsx");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Import the data to worksheet
  Dim reports As IList(Of Customer) = GetSalesReports()
  worksheet.ImportData(reports, 2, 1, False)

  workbook.SaveAs("ImportFromDT.xlsx")
End Using
{% endhighlight %}

{% highlight UWP %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Import the data to worksheet
  IList<Customer> reports = GetSalesReports();
  worksheet.ImportData(reports, 2, 1, false);

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "ImportFromDT";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight ASP.NET Core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Import the data to worksheet
  IList<Customer> reports = GetSalesReports();
  worksheet.ImportData(reports, 2, 1, false);

  //Saving the workbook as stream
  FileStream stream = new FileStream("ImportFromDT.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Import the data to worksheet
  IList<Customer> reports = GetSalesReports();
  worksheet.ImportData(reports, 2, 1, false);

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("ImportFromDT.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("ImportFromDT.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

The following code snippet provides supporting class for the above code. Here, the attributes DisplayNameAttribute and Bindable are used.

* [DisplayNameAttribute](https://docs.microsoft.com/en-us/dotnet/api/system.componentmodel.displaynameattribute?view=netframework-4.7.1) - to customize the column header name while importing.
* [BindableAttribute](https://docs.microsoft.com/en-us/dotnet/api/system.componentmodel.bindableattribute?view=netframework-4.8) - to skip a property while importing.

{% tabs %}  
{% highlight c# %}
//Gets a list of sales reports
public static List<Customer> GetSalesReports()
{
  List<Customer> reports = new List<Customer>();
  reports.Add(new Customer("Andy Bernard", "45000", "58000"));
  reports.Add(new Customer("Jim Halpert", "34000", "65000"));
  reports.Add(new Customer("Karen Fillippelli", "75000", "64000"));
  reports.Add(new Customer("Phyllis Lapin", "56500", "33600" ));
  reports.Add(new Customer("Stanley Hudson", "46500", "52000"));
  return reports;
}

//Customer details
public class Customer
{
  [DisplayNameAttribute("Sales Person Name")]
  public string SalesPerson { get; set; 
  [Bindable(false)]
  public string SalesJanJun { get; set; }
  public string SalesJulDec { get; set; }

  public Customer(string name, string janToJun, string julToDec)
  {
	SalesPerson = name;
	SalesJanJun = janToJun;
	SalesJulDec = julToDec;
  }
}
{% endhighlight %}

{% highlight vb %}
'Gets a list of sales reports
Public Function GetSalesReports() As List(Of Customer)
  Dim reports As New List(Of Customer)()
  reports.Add(New Customer("Andy Bernard", "45000", "58000"))
  reports.Add(New Customer("Jim Halpert", "34000", "65000"))
  reports.Add(New Customer("Karen Fillippelli", "75000", "64000"))
  reports.Add(New Customer("Phyllis Lapin", "56500", "33600"))
  reports.Add(New Customer("Stanley Hudson", "46500", "52000"))
  Return reports
End Function

'Customer details
Public Class Customer
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

  <Bindable(False)>
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

{% highlight UWP %}
//Gets a list of sales reports
public static List<Customer> GetSalesReports()
{
  List<Customer> reports = new List<Customer>();
  reports.Add(new Customer("Andy Bernard", "45000", "58000"));
  reports.Add(new Customer("Jim Halpert", "34000", "65000"));
  reports.Add(new Customer("Karen Fillippelli", "75000", "64000"));
  reports.Add(new Customer("Phyllis Lapin", "56500", "33600" ));
  reports.Add(new Customer("Stanley Hudson", "46500", "52000"));
  return reports;
}

//Customer details
public class Customer
{
  [DisplayNameAttribute("Sales Person Name")]
  public string SalesPerson { get; set; }
  [Bindable(false)]
  public string SalesJanJun { get; set; }
  public string SalesJulDec { get; set; }

  public Customer(string name, string janToJun, string julToDec)
  {
	SalesPerson = name;
	SalesJanJun = janToJun;
	SalesJulDec = julToDec;
  }
}
{% endhighlight %}

{% highlight ASP.NET Core %}
//Gets a list of sales reports
public static List<Customer> GetSalesReports()
{
  List<Customer> reports = new List<Customer>();
  reports.Add(new Customer("Andy Bernard", "45000", "58000"));
  reports.Add(new Customer("Jim Halpert", "34000", "65000"));
  reports.Add(new Customer("Karen Fillippelli", "75000", "64000"));
  reports.Add(new Customer("Phyllis Lapin", "56500", "33600" ));
  reports.Add(new Customer("Stanley Hudson", "46500", "52000"));
  return reports;
}

//Customer details
public class Customer
{
  [DisplayNameAttribute("Sales Person Name")]
  public string SalesPerson { get; set; }
  [Bindable(false)]
  public string SalesJanJun { get; set; }
  public string SalesJulDec { get; set; }

  public Customer(string name, string janToJun, string julToDec)
  {
	SalesPerson = name;
	SalesJanJun = janToJun;
	SalesJulDec = julToDec;
  }
}
{% endhighlight %}

{% highlight Xamarin %}
//Gets a list of sales reports
public static List<Customer> GetSalesReports()
{
  List<Customer> reports = new List<Customer>();
  reports.Add(new Customer("Andy Bernard", "45000", "58000"));
  reports.Add(new Customer("Jim Halpert", "34000", "65000"));
  reports.Add(new Customer("Karen Fillippelli", "75000", "64000"));
  reports.Add(new Customer("Phyllis Lapin", "56500", "33600" ));
  reports.Add(new Customer("Stanley Hudson", "46500", "52000"));
  return reports;
}

//Customer details
public class Customer
{
  [DisplayNameAttribute("Sales Person Name")]
  public string SalesPerson { get; set; }
  [Bindable(false)]
  public string SalesJanJun { get; set; }
  public string SalesJulDec { get; set; }

  public Customer(string name, string janToJun, string julToDec)
  {
	SalesPerson = name;
	SalesJanJun = janToJun;
	SalesJulDec = julToDec;
  }
}
{% endhighlight %}
{% endtabs %}  

### Import Data Options

ExcelImportDataOptions is a support class for ImportData() method which contains various properties to import data with formatting. 

ExcelImportDataOptions class contains the following properties:

FirstRow - Specifies first row from where the data should be imported.
FirstColumn - Specifies first column from where the data should be imported.
IncludeHeader - Specifies whether class properties names must be imported or not.
PreserveTypes - Indicates whether XlsIO should preserve column types from Data. By default, preserve type is TRUE. Setting it to True will import data based on column type, otherwise will import based on value type.

The following code snippet illustrates how to import collection objects into a worksheet using ImportData method with ExcelImportDataOptions class.

{% tabs %}  
{% highlight c# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Import the data to worksheet with Import Data Options
  IList<Customer> reports = GetSalesReports();
  
  ExcelImportDataOptions importDataOptions = new ExcelImportDataOptions();
  importDataOptions.FirstRow = 2;
  importDataOptions.FirstColumn = 1;
  importDataOptions.IncludeHeader = false;
  importDataOptions.PreserveTypes = false;
  
  worksheet.ImportData(reports, importDataOptions);

  workbook.SaveAs("ImportData.xlsx");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Import the data to worksheet with Import Data Options
  Dim reports As IList(Of Customer) = GetSalesReports()
  
  Dim importDataOptions As ExcelImportDataOptions = New ExcelImportDataOptions()
  importDataOptions.FirstRow = 2
  importDataOptions.FirstColumn = 1
  importDataOptions.IncludeHeader = False
  importDataOptions.PreserveTypes = False
  
  worksheet.ImportData(output, importDataOptions)

  workbook.SaveAs("ImportData.xlsx")
End Using
{% endhighlight %}

{% highlight UWP %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Import the data to worksheet with Import Data Options
  IList<Customer> reports = GetSalesReports();
  
  ExcelImportDataOptions importDataOptions = new ExcelImportDataOptions();
  importDataOptions.FirstRow = 2;
  importDataOptions.FirstColumn = 1;
  importDataOptions.IncludeHeader = false;
  importDataOptions.PreserveTypes = false;
  
  worksheet.ImportData(reports, importDataOptions);

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "ImportData";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight ASP.NET Core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Import the data to worksheet with Import Data Options
  IList<Customer> reports = GetSalesReports();
  
  ExcelImportDataOptions importDataOptions = new ExcelImportDataOptions();
  importDataOptions.FirstRow = 2;
  importDataOptions.FirstColumn = 1;
  importDataOptions.IncludeHeader = false;
  importDataOptions.PreserveTypes = false;
  
  worksheet.ImportData(reports, importDataOptions);

  //Saving the workbook as stream
  FileStream stream = new FileStream("ImportData.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Import the data to worksheet with Import Data Options
  IList<Customer> reports = GetSalesReports();
  
  ExcelImportDataOptions importDataOptions = new ExcelImportDataOptions();
  importDataOptions.FirstRow = 2;
  importDataOptions.FirstColumn = 1;
  importDataOptions.IncludeHeader = false;
  importDataOptions.PreserveTypes = false;
  
  worksheet.ImportData(reports, importDataOptions);

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("ImportData.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("ImportData.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

The following code snippet provides supporting class for the above code.

{% tabs %}  
{% highlight c# %}
//Gets a list of sales reports
public static List<Customer> GetSalesReports()
{
  List<Customer> reports = new List<Customer>();
  reports.Add(new Customer("Andy Bernard", "45000", "58000"));
  reports.Add(new Customer("Jim Halpert", "34000", "65000"));
  reports.Add(new Customer("Karen Fillippelli", "75000", "64000"));
  reports.Add(new Customer("Phyllis Lapin", "56500", "33600" ));
  reports.Add(new Customer("Stanley Hudson", "46500", "52000"));
  return reports;
}

//Customer details
public class Customer
{
  public string SalesPerson { get; set; 
  public string SalesJanJun { get; set; }
  public string SalesJulDec { get; set; }

  public Customer(string name, string janToJun, string julToDec)
  {
	SalesPerson = name;
	SalesJanJun = janToJun;
	SalesJulDec = julToDec;
  }
}
{% endhighlight %}

{% highlight vb %}
'Gets a list of sales reports
Public Function GetSalesReports() As List(Of Customer)
  Dim reports As New List(Of Customer)()
  reports.Add(New Customer("Andy Bernard", "45000", "58000"))
  reports.Add(New Customer("Jim Halpert", "34000", "65000"))
  reports.Add(New Customer("Karen Fillippelli", "75000", "64000"))
  reports.Add(New Customer("Phyllis Lapin", "56500", "33600"))
  reports.Add(New Customer("Stanley Hudson", "46500", "52000"))
  Return reports
End Function

'Customer details
Public Class Customer
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

{% highlight UWP %}
//Gets a list of sales reports
public static List<Customer> GetSalesReports()
{
  List<Customer> reports = new List<Customer>();
  reports.Add(new Customer("Andy Bernard", "45000", "58000"));
  reports.Add(new Customer("Jim Halpert", "34000", "65000"));
  reports.Add(new Customer("Karen Fillippelli", "75000", "64000"));
  reports.Add(new Customer("Phyllis Lapin", "56500", "33600" ));
  reports.Add(new Customer("Stanley Hudson", "46500", "52000"));
  return reports;
}

//Customer details
public class Customer
{
  public string SalesPerson { get; set; }
  public string SalesJanJun { get; set; }
  public string SalesJulDec { get; set; }

  public Customer(string name, string janToJun, string julToDec)
  {
	SalesPerson = name;
	SalesJanJun = janToJun;
	SalesJulDec = julToDec;
  }
}
{% endhighlight %}

{% highlight ASP.NET Core %}
//Gets a list of sales reports
public static List<Customer> GetSalesReports()
{
  List<Customer> reports = new List<Customer>();
  reports.Add(new Customer("Andy Bernard", "45000", "58000"));
  reports.Add(new Customer("Jim Halpert", "34000", "65000"));
  reports.Add(new Customer("Karen Fillippelli", "75000", "64000"));
  reports.Add(new Customer("Phyllis Lapin", "56500", "33600" ));
  reports.Add(new Customer("Stanley Hudson", "46500", "52000"));
  return reports;
}

//Customer details
public class Customer
{
  public string SalesPerson { get; set; }
  public string SalesJanJun { get; set; }
  public string SalesJulDec { get; set; }

  public Customer(string name, string janToJun, string julToDec)
  {
	SalesPerson = name;
	SalesJanJun = janToJun;
	SalesJulDec = julToDec;
  }
}
{% endhighlight %}

{% highlight Xamarin %}
//Gets a list of sales reports
public static List<Customer> GetSalesReports()
{
  List<Customer> reports = new List<Customer>();
  reports.Add(new Customer("Andy Bernard", "45000", "58000"));
  reports.Add(new Customer("Jim Halpert", "34000", "65000"));
  reports.Add(new Customer("Karen Fillippelli", "75000", "64000"));
  reports.Add(new Customer("Phyllis Lapin", "56500", "33600" ));
  reports.Add(new Customer("Stanley Hudson", "46500", "52000"));
  return reports;
}

//Customer details
public class Customer
{
  public string SalesPerson { get; set; }
  public string SalesJanJun { get; set; }
  public string SalesJulDec { get; set; }

  public Customer(string name, string janToJun, string julToDec)
  {
	SalesPerson = name;
	SalesJanJun = janToJun;
	SalesJulDec = julToDec;
  }
}
{% endhighlight %}
{% endtabs %}

### Import Data from Nested Collection Objects

Import hierarchical data from nested collections to Excel worksheet helps the user to analyze data in its structure. XlsIO provides more flexible options to analyze such data by importing in different layouts and grouping the imported data.

Data import can be done with the layout options:

* **Default** - Parent records imported in the first row of its collection.
* **Merge** - Parent records imported in merged rows. 
* **Repeat** - Parent records imported in all the rows. 

Imported data can be grouped with the grouping options:

* **Expand** – Imported data will be grouped and expanded.
* **Collapse** – Imported data will be grouped and collapsed at first level, by default.

Let’s see these options in detail along with code examples and screenshots.

#### Layout Options

##### Default layout option

This option adds the property value once per object for the corresponding records in the column while importing.

The following code snippet illustrates how to import data directly from nested collection objects with default layout option. The input XML file used in the code can be downloaded [here](https://www.syncfusion.com/downloads/support/directtrac/general/ze/ExportData831552872.zip).

{% tabs %}  
{% highlight c# %}
using Syncfusion.XlsIO;
using System.Collections.Generic;
using System.ComponentModel;
using System.IO;
using System.Xml.Serialization;

namespace ImportFromNestedCollection
{
    class Program
    {
        static void Main(string[] args)
        {
            ImportData();
        }

        //Main method to import data from nested collection to Excel worksheet. 
        private static void ImportData()
        {
            ExcelEngine excelEngine = new ExcelEngine();
            IApplication application = excelEngine.Excel;

            application.DefaultVersion = ExcelVersion.Excel2016;

            IWorkbook workbook = excelEngine.Excel.Workbooks.Create(1);
            IWorksheet worksheet = workbook.Worksheets[0];

            IList<Brand> vehicles = GetVehicleDetails();

            ExcelImportDataOptions importDataOptions = new ExcelImportDataOptions();

            //Imports from 4th row.
            importDataOptions.FirstRow = 4;

            //Imports column headers.
            importDataOptions.IncludeHeader = true;

            //Set layout options.
            importDataOptions.NestedDataLayoutOptions = ExcelNestedDataLayoutOptions.Default;
            
            //Import data from the nested collection.
            worksheet.ImportData(vehicles, importDataOptions);

            //Apply style to headers 
            worksheet["A1:C2"].Merge();
            worksheet["A1"].Text = "Automobile Brands in the US";

            worksheet.UsedRange.AutofitColumns();

            workbook.SaveAs("ImportData.xlsx");

            workbook.Close();
            excelEngine.Dispose();
        }

        //Helper method to load data from XML file and add them in collections. 
        private static IList<Brand> GetVehicleDetails()
        {
            XmlSerializer deserializer = new XmlSerializer(typeof(BrandObjects));

            //Read data from XML file. 
            TextReader textReader = new StreamReader(@"..\..\Data\ExportData.xml");
            BrandObjects brands = (BrandObjects)deserializer.Deserialize(textReader);

            //Initialize parent collection to add data from XML file. 
            List<Brand> list = new List<Brand>();

            string brandName = brands.BrandObject[0].BrandName;
            string vehicleType = brands.BrandObject[0].VahicleType;
            string modelName = brands.BrandObject[0].ModelName;

            //Parent class 
            Brand brand = new Brand(brandName);
            brand.VehicleTypes = new List<VehicleType>();

            VehicleType vehicle = new VehicleType(vehicleType);
            vehicle.Models = new List<Model>();

            Model model = new Model(modelName);
            brand.VehicleTypes.Add(vehicle);

            list.Add(brand);

            foreach (BrandObject brandObj in brands.BrandObject)
            {
                if (brandName == brandObj.BrandName)
                {
                    if (vehicleType == brandObj.VahicleType)
                    {
                        vehicle.Models.Add(new Model(brandObj.ModelName));
                        continue;
                    }
                    else
                    {
                        vehicle = new VehicleType(brandObj.VahicleType);
                        vehicle.Models = new List<Model>();
                        vehicle.Models.Add(new Model(brandObj.ModelName));
                        brand.VehicleTypes.Add(vehicle);
                        vehicleType = brandObj.VahicleType;
                    }
                    continue;
                }
                else
                {
                    brand = new Brand(brandObj.BrandName);
                    vehicle = new VehicleType(brandObj.VahicleType);
                    vehicle.Models = new List<Model>();
                    vehicle.Models.Add(new Model(brandObj.ModelName));
                    brand.VehicleTypes = new List<VehicleType>();
                    brand.VehicleTypes.Add(vehicle);
                    vehicleType = brandObj.VahicleType;
                    list.Add(brand);
                    brandName = brandObj.BrandName;
                }
            }

            textReader.Close();
            return list;
        }
    }

    //Parent Class 
    public class Brand
    {
        private string m_brandName;

        [DisplayNameAttribute("Brand")]
        public string BrandName
        {
            get { return m_brandName; }
            set { m_brandName = value; }
        }

        //Vehicle Types Collection 
        private IList<VehicleType> m_vehicleTypes;

        public IList<VehicleType> VehicleTypes
        {
            get { return m_vehicleTypes; }
            set { m_vehicleTypes = value; }
        }

        public Brand(string brandName)
        {
            m_brandName = brandName;
        }
    }

    //Child Class 
    public class VehicleType
    {
        private string m_vehicleName;

        [DisplayNameAttribute("Vehicle Type")]
        public string VehicleName
        {
            get { return m_vehicleName; }
            set { m_vehicleName = value; }
        }

        //Models collection 
        private IList<Model> m_models;
        public IList<Model> Models
        {
            get { return m_models; }
            set { m_models = value; }
        }

        public VehicleType(string vehicle)
        {
            m_vehicleName = vehicle;
        }
    }

    //Sub-child Class 
    public class Model
    {
        private string m_modelName;

        [DisplayNameAttribute("Model")]
        public string ModelName
        {
            get { return m_modelName; }
            set { m_modelName = value; }
        }

        public Model(string name)
        {
            m_modelName = name;
        }
    }

    //Helper Classes 
    [XmlRootAttribute("BrandObjects")]
    public class BrandObjects
    {
        [XmlElement("BrandObject")]
        public BrandObject[] BrandObject { get; set; }
    }

    public class BrandObject
    {
        public string BrandName { get; set; }
        public string VahicleType { get; set; }
        public string ModelName { get; set; }
    }
}
{% endhighlight %}

{% highlight vb %}
Imports Syncfusion.XlsIO
Imports System.Collections.Generic
Imports System.ComponentModel
Imports System.IO
Imports System.Xml.Serialization

Namespace ImportFromNestedCollection
    Class Program
        Private Shared Sub Main(ByVal args As String())
            ImportData()
        End Sub

        'Main method to import data from nested collection to Excel worksheet. 
        Private Shared Sub ImportData()
            Dim excelEngine As ExcelEngine = New ExcelEngine()
            Dim application As IApplication = excelEngine.Excel
			
            application.DefaultVersion = ExcelVersion.Excel2016
			
            Dim workbook As IWorkbook = excelEngine.Excel.Workbooks.Create(1)
            Dim worksheet As IWorksheet = workbook.Worksheets(0)
			
            Dim vehicles As IList(Of Brand) = GetVehicleDetails()
			
            Dim importDataOptions As ExcelImportDataOptions = New ExcelImportDataOptions()
			
			'Imports from 4th row.
            importDataOptions.FirstRow = 4
			
			'Imports column headers.
            importDataOptions.IncludeHeader = True
			
			'Set layout options.
            importDataOptions.NestedDataLayoutOptions = ExcelNestedDataLayoutOptions.Default
			'Import data from the nested collection.
            worksheet.ImportData(vehicles, importDataOptions)
						
			'Apply style to headers 
            worksheet("A1:C2").Merge()
            worksheet("A1").Text = "Automobile Brands in the US"
			
            worksheet.UsedRange.AutofitColumns()
			
            workbook.SaveAs("ImportData.xlsx")
			
            workbook.Close()
            excelEngine.Dispose()
        End Sub

        'Helper method to load data from XML file and add them in collections. 
        Private Shared Function GetVehicleDetails() As IList(Of Brand)
            Dim deserializer As XmlSerializer = New XmlSerializer(GetType(BrandObjects))
			
			'Read data from XML file. 
            Dim textReader As TextReader = New StreamReader("..\..\Data\ExportData.xml")
            Dim brands As BrandObjects = CType(deserializer.Deserialize(textReader), BrandObjects)
			
			'Initialize parent collection to add data from XML file. 
            Dim list As List(Of Brand) = New List(Of Brand)()
			
            Dim brandName As String = brands.BrandObject(0).BrandName
            Dim vehicleType As String = brands.BrandObject(0).VahicleType
            Dim modelName As String = brands.BrandObject(0).ModelName
			
			'Parent class 
            Dim brand As Brand = New Brand(brandName)
            brand.VehicleTypes = New List(Of VehicleType)()
			
            Dim vehicle As VehicleType = New VehicleType(vehicleType)
            vehicle.Models = New List(Of Model)()
			
            Dim model As Model = New Model(modelName)
            brand.VehicleTypes.Add(vehicle)
			
            list.Add(brand)

            For Each brandObj As BrandObject In brands.BrandObject

                If brandName = brandObj.BrandName Then

                    If vehicleType = brandObj.VahicleType Then
                        vehicle.Models.Add(New Model(brandObj.ModelName))
                        Continue For
                    Else
                        vehicle = New VehicleType(brandObj.VahicleType)
                        vehicle.Models = New List(Of Model)()
                        vehicle.Models.Add(New Model(brandObj.ModelName))
                        brand.VehicleTypes.Add(vehicle)
                        vehicleType = brandObj.VahicleType
                    End If

                    Continue For
                Else
                    brand = New Brand(brandObj.BrandName)
                    vehicle = New VehicleType(brandObj.VahicleType)
                    vehicle.Models = New List(Of Model)()
                    vehicle.Models.Add(New Model(brandObj.ModelName))
                    brand.VehicleTypes = New List(Of VehicleType)()
                    brand.VehicleTypes.Add(vehicle)
                    vehicleType = brandObj.VahicleType
                    list.Add(brand)
                    brandName = brandObj.BrandName
                End If
            Next

            textReader.Close()
            Return list
        End Function
    End Class

    'Parent Class 
    Public Class Brand
        Private m_brandName As String

        <DisplayNameAttribute("Brand")>
        Public Property BrandName As String
            Get
                Return m_brandName
            End Get
            Set(ByVal value As String)
                m_brandName = value
            End Set
        End Property

        Private m_vehicleTypes As IList(Of VehicleType)

        Public Property VehicleTypes As IList(Of VehicleType)
            Get
                Return m_vehicleTypes
            End Get
            Set(ByVal value As IList(Of VehicleType))
                m_vehicleTypes = value
            End Set
        End Property

        Public Sub New(ByVal brandName As String)
            m_brandName = brandName
        End Sub
    End Class
 
    'Child Class
    Public Class VehicleType
        Private m_vehicleName As String

        <DisplayNameAttribute("Vehicle Type")>
        Public Property VehicleName As String
            Get
                Return m_vehicleName
            End Get
            Set(ByVal value As String)
                m_vehicleName = value
            End Set
        End Property

        Private m_models As IList(Of Model)

        Public Property Models As IList(Of Model)
            Get
                Return m_models
            End Get
            Set(ByVal value As IList(Of Model))
                m_models = value
            End Set
        End Property

        Public Sub New(ByVal vehicle As String)
            m_vehicleName = vehicle
        End Sub
    End Class
    
	'Sub-child Class 
    Public Class Model
        Private m_modelName As String

        <DisplayNameAttribute("Model")>
        Public Property ModelName As String
            Get
                Return m_modelName
            End Get
            Set(ByVal value As String)
                m_modelName = value
            End Set
        End Property

        Public Sub New(ByVal name As String)
            m_modelName = name
        End Sub
    End Class

    <XmlRootAttribute("BrandObjects")>
    Public Class BrandObjects
        <XmlElement("BrandObject")>
        Public Property BrandObject As BrandObject()
    End Class

    Public Class BrandObject
        Public Property BrandName As String
        Public Property VahicleType As String
        Public Property ModelName As String
    End Class
End Namespace

{% endhighlight %}

{% highlight UWP %}
using Syncfusion.XlsIO;
using System.Collections.Generic;
using System.ComponentModel;
using System.IO;
using System.Xml.Serialization;

namespace ImportFromNestedCollection
{
    public sealed partial class MainPage : Page
    {
	    public MainPage()
        {
            this.InitializeComponent();
        }
		

        //Button click to import data from nested collection to Excel worksheet. 
		private async void btnGenerateExcel_Click(object sender, RoutedEventArgs e)
        {
            ExcelEngine excelEngine = new ExcelEngine();
            IApplication application = excelEngine.Excel;

            application.DefaultVersion = ExcelVersion.Excel2016;

            IWorkbook workbook = excelEngine.Excel.Workbooks.Create(1);
            IWorksheet worksheet = workbook.Worksheets[0];

            IList<Brand> vehicles = GetVehicleDetails();

            ExcelImportDataOptions importDataOptions = new ExcelImportDataOptions();

            //Imports from 4th row.
            importDataOptions.FirstRow = 4;

            //Imports column headers.
            importDataOptions.IncludeHeader = true;

            //Set layout options.
            importDataOptions.NestedDataLayoutOptions = ExcelNestedDataLayoutOptions.Default;
            
            //Import data from the nested collection.
            worksheet.ImportData(vehicles, importDataOptions);

            //Apply style to headers 
            worksheet["A1:C2"].Merge();
            worksheet["A1"].Text = "Automobile Brands in the US";

            worksheet.UsedRange.AutofitColumns();

            //Initializes FileSavePicker
            FileSavePicker savePicker = new FileSavePicker();
            savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
            savePicker.SuggestedFileName = "ImportData";
            savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });
	        
            //Creates a storage file from FileSavePicker
            StorageFile storageFile = await savePicker.PickSaveFileAsync();
	        
            //Saves changes to the specified storage file
            await workbook.SaveAsAsync(storageFile);

            workbook.Close();
            excelEngine.Dispose();
        }

        //Helper method to load data from XML file and add them in collections. 
        private static IList<Brand> GetVehicleDetails()
        {
            XmlSerializer deserializer = new XmlSerializer(typeof(BrandObjects));

            //Read data from XML file. 
			Assembly assembly = typeof(MainPage).GetTypeInfo().Assembly;
            Stream fileStream = assembly.GetManifestResourceStream("Sample.Data.ExportData.xml");
            TextReader textReader = new StreamReader(fileStream);
            BrandObjects brands = (BrandObjects)deserializer.Deserialize(textReader);

            //Initialize parent collection to add data from XML file. 
            List<Brand> list = new List<Brand>();

            string brandName = brands.BrandObject[0].BrandName;
            string vehicleType = brands.BrandObject[0].VahicleType;
            string modelName = brands.BrandObject[0].ModelName;

            //Parent class 
            Brand brand = new Brand(brandName);
            brand.VehicleTypes = new List<VehicleType>();

            VehicleType vehicle = new VehicleType(vehicleType);
            vehicle.Models = new List<Model>();

            Model model = new Model(modelName);
            brand.VehicleTypes.Add(vehicle);

            list.Add(brand);

            foreach (BrandObject brandObj in brands.BrandObject)
            {
                if (brandName == brandObj.BrandName)
                {
                    if (vehicleType == brandObj.VahicleType)
                    {
                        vehicle.Models.Add(new Model(brandObj.ModelName));
                        continue;
                    }
                    else
                    {
                        vehicle = new VehicleType(brandObj.VahicleType);
                        vehicle.Models = new List<Model>();
                        vehicle.Models.Add(new Model(brandObj.ModelName));
                        brand.VehicleTypes.Add(vehicle);
                        vehicleType = brandObj.VahicleType;
                    }
                    continue;
                }
                else
                {
                    brand = new Brand(brandObj.BrandName);
                    vehicle = new VehicleType(brandObj.VahicleType);
                    vehicle.Models = new List<Model>();
                    vehicle.Models.Add(new Model(brandObj.ModelName));
                    brand.VehicleTypes = new List<VehicleType>();
                    brand.VehicleTypes.Add(vehicle);
                    vehicleType = brandObj.VahicleType;
                    list.Add(brand);
                    brandName = brandObj.BrandName;
                }
            }

            textReader.Close();
            return list;
        }
    }

    //Parent Class 
    public class Brand
    {
        private string m_brandName;

        [DisplayNameAttribute("Brand")]
        public string BrandName
        {
            get { return m_brandName; }
            set { m_brandName = value; }
        }

        //Vehicle Types Collection 
        private IList<VehicleType> m_vehicleTypes;

        public IList<VehicleType> VehicleTypes
        {
            get { return m_vehicleTypes; }
            set { m_vehicleTypes = value; }
        }

        public Brand(string brandName)
        {
            m_brandName = brandName;
        }
    }

    //Child Class 
    public class VehicleType
    {
        private string m_vehicleName;

        [DisplayNameAttribute("Vehicle Type")]
        public string VehicleName
        {
            get { return m_vehicleName; }
            set { m_vehicleName = value; }
        }

        //Models collection 
        private IList<Model> m_models;
        public IList<Model> Models
        {
            get { return m_models; }
            set { m_models = value; }
        }

        public VehicleType(string vehicle)
        {
            m_vehicleName = vehicle;
        }
    }

    //Sub-child Class 
    public class Model
    {
        private string m_modelName;

        [DisplayNameAttribute("Model")]
        public string ModelName
        {
            get { return m_modelName; }
            set { m_modelName = value; }
        }

        public Model(string name)
        {
            m_modelName = name;
        }
    }

    //Helper Classes 
    [XmlRootAttribute("BrandObjects")]
    public class BrandObjects
    {
        [XmlElement("BrandObject")]
        public BrandObject[] BrandObject { get; set; }
    }

    public class BrandObject
    {
        public string BrandName { get; set; }
        public string VahicleType { get; set; }
        public string ModelName { get; set; }
    }
}
{% endhighlight %}

{% highlight ASP.NET Core %}
using Syncfusion.XlsIO;
using System.Collections.Generic;
using System.ComponentModel;
using System.IO;
using System.Xml.Serialization;

namespace ImportFromNestedCollection
{
    class Program
    {
        static void Main(string[] args)
        {
            ImportData();
        }

        //Main method to import data from nested collection to Excel worksheet. 
        private static void ImportData()
        {
            ExcelEngine excelEngine = new ExcelEngine();
            IApplication application = excelEngine.Excel;

            application.DefaultVersion = ExcelVersion.Excel2016;

            IWorkbook workbook = excelEngine.Excel.Workbooks.Create(1);
            IWorksheet worksheet = workbook.Worksheets[0];

            IList<Brand> vehicles = GetVehicleDetails();

            ExcelImportDataOptions importDataOptions = new ExcelImportDataOptions();

            //Imports from 4th row.
            importDataOptions.FirstRow = 4;

            //Imports column headers.
            importDataOptions.IncludeHeader = true;

            //Set layout options.
            importDataOptions.NestedDataLayoutOptions = ExcelNestedDataLayoutOptions.Default;
            
            //Import data from the nested collection.
            worksheet.ImportData(vehicles, importDataOptions);

            //Apply style to headers 
            worksheet["A1:C2"].Merge();
            worksheet["A1"].Text = "Automobile Brands in the US";

            worksheet.UsedRange.AutofitColumns();

            //Saving the workbook as stream
            FileStream stream = new FileStream("ImportData.xlsx", FileMode.Create, FileAccess.ReadWrite);
            workbook.SaveAs(stream);

            stream.Dispose();
            workbook.Close();
            excelEngine.Dispose();
        }

        //Helper method to load data from XML file and add them in collections. 
        private static IList<Brand> GetVehicleDetails()
        {
            XmlSerializer deserializer = new XmlSerializer(typeof(BrandObjects));

            //Read data from XML file. 
            FileStream stream = new FileStream(@"..\..\Data\ExportData.xml", FileMode.Open, FileAccess.Read);
            TextReader textReader = new StreamReader(stream);
            BrandObjects brands = (BrandObjects)deserializer.Deserialize(textReader);

            //Initialize parent collection to add data from XML file. 
            List<Brand> list = new List<Brand>();

            string brandName = brands.BrandObject[0].BrandName;
            string vehicleType = brands.BrandObject[0].VahicleType;
            string modelName = brands.BrandObject[0].ModelName;

            //Parent class 
            Brand brand = new Brand(brandName);
            brand.VehicleTypes = new List<VehicleType>();

            VehicleType vehicle = new VehicleType(vehicleType);
            vehicle.Models = new List<Model>();

            Model model = new Model(modelName);
            brand.VehicleTypes.Add(vehicle);

            list.Add(brand);

            foreach (BrandObject brandObj in brands.BrandObject)
            {
                if (brandName == brandObj.BrandName)
                {
                    if (vehicleType == brandObj.VahicleType)
                    {
                        vehicle.Models.Add(new Model(brandObj.ModelName));
                        continue;
                    }
                    else
                    {
                        vehicle = new VehicleType(brandObj.VahicleType);
                        vehicle.Models = new List<Model>();
                        vehicle.Models.Add(new Model(brandObj.ModelName));
                        brand.VehicleTypes.Add(vehicle);
                        vehicleType = brandObj.VahicleType;
                    }
                    continue;
                }
                else
                {
                    brand = new Brand(brandObj.BrandName);
                    vehicle = new VehicleType(brandObj.VahicleType);
                    vehicle.Models = new List<Model>();
                    vehicle.Models.Add(new Model(brandObj.ModelName));
                    brand.VehicleTypes = new List<VehicleType>();
                    brand.VehicleTypes.Add(vehicle);
                    vehicleType = brandObj.VahicleType;
                    list.Add(brand);
                    brandName = brandObj.BrandName;
                }
            }

            textReader.Close();
            return list;
        }
    }

    //Parent Class 
    public class Brand
    {
        private string m_brandName;

        [DisplayNameAttribute("Brand")]
        public string BrandName
        {
            get { return m_brandName; }
            set { m_brandName = value; }
        }

        //Vehicle Types Collection 
        private IList<VehicleType> m_vehicleTypes;

        public IList<VehicleType> VehicleTypes
        {
            get { return m_vehicleTypes; }
            set { m_vehicleTypes = value; }
        }

        public Brand(string brandName)
        {
            m_brandName = brandName;
        }
    }

    //Child Class 
    public class VehicleType
    {
        private string m_vehicleName;

        [DisplayNameAttribute("Vehicle Type")]
        public string VehicleName
        {
            get { return m_vehicleName; }
            set { m_vehicleName = value; }
        }

        //Models collection 
        private IList<Model> m_models;
        public IList<Model> Models
        {
            get { return m_models; }
            set { m_models = value; }
        }

        public VehicleType(string vehicle)
        {
            m_vehicleName = vehicle;
        }
    }

    //Sub-child Class 
    public class Model
    {
        private string m_modelName;

        [DisplayNameAttribute("Model")]
        public string ModelName
        {
            get { return m_modelName; }
            set { m_modelName = value; }
        }

        public Model(string name)
        {
            m_modelName = name;
        }
    }

    //Helper Classes 
    [XmlRootAttribute("BrandObjects")]
    public class BrandObjects
    {
        [XmlElement("BrandObject")]
        public BrandObject[] BrandObject { get; set; }
    }

    public class BrandObject
    {
        public string BrandName { get; set; }
        public string VahicleType { get; set; }
        public string ModelName { get; set; }
    }
}
{% endhighlight %}

{% highlight Xamarin %}
using Syncfusion.XlsIO;
using System.Collections.Generic;
using System.ComponentModel;
using System.IO;
using System.Xml.Serialization;

namespace ImportFromNestedCollection
{
    public partial class MainPage : ContentPage
    {
	    public MainPage()
        {
            this.InitializeComponent();
        }
		

        //Button click to import data from nested collection to Excel worksheet. 
		internal void OnButtonClicked(object sender, EventArgs e)
        {
            ExcelEngine excelEngine = new ExcelEngine();
            IApplication application = excelEngine.Excel;

            application.DefaultVersion = ExcelVersion.Excel2016;

            IWorkbook workbook = excelEngine.Excel.Workbooks.Create(1);
            IWorksheet worksheet = workbook.Worksheets[0];

            IList<Brand> vehicles = GetVehicleDetails();

            ExcelImportDataOptions importDataOptions = new ExcelImportDataOptions();

            //Imports from 4th row.
            importDataOptions.FirstRow = 4;

            //Imports column headers.
            importDataOptions.IncludeHeader = true;

            //Set layout options.
            importDataOptions.NestedDataLayoutOptions = ExcelNestedDataLayoutOptions.Default;
            
            //Import data from the nested collection.
            worksheet.ImportData(vehicles, importDataOptions);

            //Apply style to headers 
            worksheet["A1:C2"].Merge();
            worksheet["A1"].Text = "Automobile Brands in the US";

            worksheet.UsedRange.AutofitColumns();

            //Save the document as file and view the saved document

            //The operation in SaveAndView under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the xlsio/xamarin section for respective code samples
	        
            if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
            {
                Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("ImportData.xlsx", "application/msexcel", stream);
            }
            else
            {
                Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("ImportData.xlsx", "application/msexcel", stream);
            }   
	
            workbook.Close();
            excelEngine.Dispose();
        }

        //Helper method to load data from XML file and add them in collections. 
        private static IList<Brand> GetVehicleDetails()
        {
            XmlSerializer deserializer = new XmlSerializer(typeof(BrandObjects));

            //Read data from XML file.
			Assembly assembly = typeof(App).GetTypeInfo().Assembly;
            Stream fileStream = assembly.GetManifestResourceStream("Sample.Data.ExportData.xml");
            TextReader textReader = new StreamReader(fileStream);
            BrandObjects brands = (BrandObjects)deserializer.Deserialize(textReader);

            //Initialize parent collection to add data from XML file. 
            List<Brand> list = new List<Brand>();

            string brandName = brands.BrandObject[0].BrandName;
            string vehicleType = brands.BrandObject[0].VahicleType;
            string modelName = brands.BrandObject[0].ModelName;

            //Parent class 
            Brand brand = new Brand(brandName);
            brand.VehicleTypes = new List<VehicleType>();

            VehicleType vehicle = new VehicleType(vehicleType);
            vehicle.Models = new List<Model>();

            Model model = new Model(modelName);
            brand.VehicleTypes.Add(vehicle);

            list.Add(brand);

            foreach (BrandObject brandObj in brands.BrandObject)
            {
                if (brandName == brandObj.BrandName)
                {
                    if (vehicleType == brandObj.VahicleType)
                    {
                        vehicle.Models.Add(new Model(brandObj.ModelName));
                        continue;
                    }
                    else
                    {
                        vehicle = new VehicleType(brandObj.VahicleType);
                        vehicle.Models = new List<Model>();
                        vehicle.Models.Add(new Model(brandObj.ModelName));
                        brand.VehicleTypes.Add(vehicle);
                        vehicleType = brandObj.VahicleType;
                    }
                    continue;
                }
                else
                {
                    brand = new Brand(brandObj.BrandName);
                    vehicle = new VehicleType(brandObj.VahicleType);
                    vehicle.Models = new List<Model>();
                    vehicle.Models.Add(new Model(brandObj.ModelName));
                    brand.VehicleTypes = new List<VehicleType>();
                    brand.VehicleTypes.Add(vehicle);
                    vehicleType = brandObj.VahicleType;
                    list.Add(brand);
                    brandName = brandObj.BrandName;
                }
            }

            textReader.Close();
            return list;
        }
    }

    //Parent Class 
    public class Brand
    {
        private string m_brandName;

        [DisplayNameAttribute("Brand")]
        public string BrandName
        {
            get { return m_brandName; }
            set { m_brandName = value; }
        }

        //Vehicle Types Collection 
        private IList<VehicleType> m_vehicleTypes;

        public IList<VehicleType> VehicleTypes
        {
            get { return m_vehicleTypes; }
            set { m_vehicleTypes = value; }
        }

        public Brand(string brandName)
        {
            m_brandName = brandName;
        }
    }

    //Child Class 
    public class VehicleType
    {
        private string m_vehicleName;

        [DisplayNameAttribute("Vehicle Type")]
        public string VehicleName
        {
            get { return m_vehicleName; }
            set { m_vehicleName = value; }
        }

        //Models collection 
        private IList<Model> m_models;
        public IList<Model> Models
        {
            get { return m_models; }
            set { m_models = value; }
        }

        public VehicleType(string vehicle)
        {
            m_vehicleName = vehicle;
        }
    }

    //Sub-child Class 
    public class Model
    {
        private string m_modelName;

        [DisplayNameAttribute("Model")]
        public string ModelName
        {
            get { return m_modelName; }
            set { m_modelName = value; }
        }

        public Model(string name)
        {
            m_modelName = name;
        }
    }

    //Helper Classes 
    [XmlRootAttribute("BrandObjects")]
    public class BrandObjects
    {
        [XmlElement("BrandObject")]
        public BrandObject[] BrandObject { get; set; }
    }

    public class BrandObject
    {
        public string BrandName { get; set; }
        public string VahicleType { get; set; }
        public string ModelName { get; set; }
    }
}
{% endhighlight %}
{% endtabs %}

The following screenshot represents the output document with Default layout option.

![Output document with Default layout option](Working-with-Data_images/Working-with-Data_img1.png)

##### Merge layout option

This option merges the cells in the column for each object while importing.

The following code snippet helps to import data with merged cells.

{% tabs %}  
{% highlight c# %}
importDataOptions.NestedDataLayoutOptions = ExcelNestedDataLayoutOptions.Merge;
{% endhighlight %}

{% highlight vb %}
importDataOptions.NestedDataLayoutOptions = ExcelNestedDataLayoutOptions.Merge
{% endhighlight %}

{% highlight UWP %}
importDataOptions.NestedDataLayoutOptions = ExcelNestedDataLayoutOptions.Merge;
{% endhighlight %}

{% highlight ASP.NET Core %}
importDataOptions.NestedDataLayoutOptions = ExcelNestedDataLayoutOptions.Merge;
{% endhighlight %}

{% highlight Xamarin %}
importDataOptions.NestedDataLayoutOptions = ExcelNestedDataLayoutOptions.Merge;
{% endhighlight %}
{% endtabs %}

The following screenshot represents the output document with Merge layout option.

![Output document with Merge layout option](Working-with-Data_images/Working-with-Data_img2.png)

##### Repeat layout option

This option repeats the parent records imported in all the rows.

The following code snippet helps to import data with repeated rows.

{% tabs %}  
{% highlight c# %}
importDataOptions.NestedDataLayoutOptions = ExcelNestedDataLayoutOptions.Repeat;
{% endhighlight %}

{% highlight vb %}
importDataOptions.NestedDataLayoutOptions = ExcelNestedDataLayoutOptions.Repeat
{% endhighlight %}

{% highlight UWP %}
importDataOptions.NestedDataLayoutOptions = ExcelNestedDataLayoutOptions.Repeat;
{% endhighlight %}

{% highlight ASP.NET Core %}
importDataOptions.NestedDataLayoutOptions = ExcelNestedDataLayoutOptions.Repeat;
{% endhighlight %}

{% highlight Xamarin %}
importDataOptions.NestedDataLayoutOptions = ExcelNestedDataLayoutOptions.Repeat;
{% endhighlight %}
{% endtabs %}

The following screenshot represents the output document with Repeat layout option.

![Output document with Repeat layout option](Working-with-Data_images/Working-with-Data_img3.png)

#### Grouping Options

##### Import Data with Grouping option

Hierarchical data imported into Excel worksheet must be shown its structure to analyze more flexible. In addition, if the data is grouped according to its level, it is easier to analyze. XlsIO supports to import hierarchical data from nested collection and group them while importing.

The following are the options that is supported to group on import.

* **Expand** – Imported data will be grouped and expanded.
* **Collapse** – Imported data will be grouped and collapsed at first level, by default.

In addition, `CollapseLevel` will group and collapse the mentioned level, upto the maximum of 8 levels.

The following code snippet illustrates how to import data directly from nested collection objects with collapse group option.

{% tabs %}  
{% highlight c# %}
using Syncfusion.XlsIO;
using System.Collections.Generic;
using System.ComponentModel;
using System.IO;
using System.Xml.Serialization;

namespace ImportFromNestedCollection
{
    class Program
    {
        static void Main(string[] args)
        {
            ImportData();
        }

        //Main method to import data from nested collection to Excel worksheet. 
        private static void ImportData()
        {
            ExcelEngine excelEngine = new ExcelEngine();
            IApplication application = excelEngine.Excel;

            application.DefaultVersion = ExcelVersion.Excel2016;

            IWorkbook workbook = excelEngine.Excel.Workbooks.Create(1);
            IWorksheet worksheet = workbook.Worksheets[0];

            IList<Brand> vehicles = GetVehicleDetails();

            ExcelImportDataOptions importDataOptions = new ExcelImportDataOptions();

            //Imports from 4th row.
            importDataOptions.FirstRow = 4;

            //Imports column headers.
            importDataOptions.IncludeHeader = true;

            //Set layout options.
            importDataOptions.NestedDataLayoutOptions = ExcelNestedDataLayoutOptions.Default;
            
			//Set grouping option.
            importDataOptions.NestedDataGroupOptions = ExcelNestedDataGroupOptions.Collapse;
            
            //Set collapse level.
            //GroupingOption must set to ‘Collapse’ before applying ‘CollapseLevel’.
            importDataOptions.CollapseLevel = 2;
			
            //Import data from the nested collection.
            worksheet.ImportData(vehicles, importDataOptions);

            //Apply style to headers 
            worksheet["A1:C2"].Merge();
            worksheet["A1"].Text = "Automobile Brands in the US";

            worksheet.UsedRange.AutofitColumns();

            workbook.SaveAs("ImportData.xlsx");

            workbook.Close();
            excelEngine.Dispose();
        }

        //Helper method to load data from XML file and add them in collections. 
        private static IList<Brand> GetVehicleDetails()
        {
            XmlSerializer deserializer = new XmlSerializer(typeof(BrandObjects));

            //Read data from XML file. 
            TextReader textReader = new StreamReader(@"..\..\Data\ExportData.xml");
            BrandObjects brands = (BrandObjects)deserializer.Deserialize(textReader);

            //Initialize parent collection to add data from XML file. 
            List<Brand> list = new List<Brand>();

            string brandName = brands.BrandObject[0].BrandName;
            string vehicleType = brands.BrandObject[0].VahicleType;
            string modelName = brands.BrandObject[0].ModelName;

            //Parent class 
            Brand brand = new Brand(brandName);
            brand.VehicleTypes = new List<VehicleType>();

            VehicleType vehicle = new VehicleType(vehicleType);
            vehicle.Models = new List<Model>();

            Model model = new Model(modelName);
            brand.VehicleTypes.Add(vehicle);

            list.Add(brand);

            foreach (BrandObject brandObj in brands.BrandObject)
            {
                if (brandName == brandObj.BrandName)
                {
                    if (vehicleType == brandObj.VahicleType)
                    {
                        vehicle.Models.Add(new Model(brandObj.ModelName));
                        continue;
                    }
                    else
                    {
                        vehicle = new VehicleType(brandObj.VahicleType);
                        vehicle.Models = new List<Model>();
                        vehicle.Models.Add(new Model(brandObj.ModelName));
                        brand.VehicleTypes.Add(vehicle);
                        vehicleType = brandObj.VahicleType;
                    }
                    continue;
                }
                else
                {
                    brand = new Brand(brandObj.BrandName);
                    vehicle = new VehicleType(brandObj.VahicleType);
                    vehicle.Models = new List<Model>();
                    vehicle.Models.Add(new Model(brandObj.ModelName));
                    brand.VehicleTypes = new List<VehicleType>();
                    brand.VehicleTypes.Add(vehicle);
                    vehicleType = brandObj.VahicleType;
                    list.Add(brand);
                    brandName = brandObj.BrandName;
                }
            }

            textReader.Close();
            return list;
        }
    }

    //Parent Class 
    public class Brand
    {
        private string m_brandName;

        [DisplayNameAttribute("Brand")]
        public string BrandName
        {
            get { return m_brandName; }
            set { m_brandName = value; }
        }

        //Vehicle Types Collection 
        private IList<VehicleType> m_vehicleTypes;

        public IList<VehicleType> VehicleTypes
        {
            get { return m_vehicleTypes; }
            set { m_vehicleTypes = value; }
        }

        public Brand(string brandName)
        {
            m_brandName = brandName;
        }
    }

    //Child Class 
    public class VehicleType
    {
        private string m_vehicleName;

        [DisplayNameAttribute("Vehicle Type")]
        public string VehicleName
        {
            get { return m_vehicleName; }
            set { m_vehicleName = value; }
        }

        //Models collection 
        private IList<Model> m_models;
        public IList<Model> Models
        {
            get { return m_models; }
            set { m_models = value; }
        }

        public VehicleType(string vehicle)
        {
            m_vehicleName = vehicle;
        }
    }

    //Sub-child Class 
    public class Model
    {
        private string m_modelName;

        [DisplayNameAttribute("Model")]
        public string ModelName
        {
            get { return m_modelName; }
            set { m_modelName = value; }
        }

        public Model(string name)
        {
            m_modelName = name;
        }
    }

    //Helper Classes 
    [XmlRootAttribute("BrandObjects")]
    public class BrandObjects
    {
        [XmlElement("BrandObject")]
        public BrandObject[] BrandObject { get; set; }
    }

    public class BrandObject
    {
        public string BrandName { get; set; }
        public string VahicleType { get; set; }
        public string ModelName { get; set; }
    }
}
{% endhighlight %}

{% highlight vb %}
Imports Syncfusion.XlsIO
Imports System.Collections.Generic
Imports System.ComponentModel
Imports System.IO
Imports System.Xml.Serialization

Namespace ImportFromNestedCollection
    Class Program
        Private Shared Sub Main(ByVal args As String())
            ImportData()
        End Sub

        'Main method to import data from nested collection to Excel worksheet. 
        Private Shared Sub ImportData()
            Dim excelEngine As ExcelEngine = New ExcelEngine()
            Dim application As IApplication = excelEngine.Excel
			
            application.DefaultVersion = ExcelVersion.Excel2016
			
            Dim workbook As IWorkbook = excelEngine.Excel.Workbooks.Create(1)
            Dim worksheet As IWorksheet = workbook.Worksheets(0)
			
            Dim vehicles As IList(Of Brand) = GetVehicleDetails()
			
            Dim importDataOptions As ExcelImportDataOptions = New ExcelImportDataOptions()
			
			'Imports from 4th row.
            importDataOptions.FirstRow = 4
			
			'Imports column headers.
            importDataOptions.IncludeHeader = True
			
			'Set layout options.
            importDataOptions.NestedDataLayoutOptions = ExcelNestedDataLayoutOptions.Default
			
			'Set grouping option.
            importDataOptions.NestedDataGroupOptions = ExcelNestedDataGroupOptions.Collapse
            
            'Set collapse level.
            'GroupingOption must set to ‘Collapse’ before applying ‘CollapseLevel’.
            importDataOptions.CollapseLevel = 2;
			
			'Import data from the nested collection.
            worksheet.ImportData(vehicles, importDataOptions)
						
			'Apply style to headers 
            worksheet("A1:C2").Merge()
            worksheet("A1").Text = "Automobile Brands in the US"
			
            worksheet.UsedRange.AutofitColumns()
			
            workbook.SaveAs("ImportData.xlsx")
			
            workbook.Close()
            excelEngine.Dispose()
        End Sub

        'Helper method to load data from XML file and add them in collections. 
        Private Shared Function GetVehicleDetails() As IList(Of Brand)
            Dim deserializer As XmlSerializer = New XmlSerializer(GetType(BrandObjects))
			
			'Read data from XML file. 
            Dim textReader As TextReader = New StreamReader("..\..\Data\ExportData.xml")
            Dim brands As BrandObjects = CType(deserializer.Deserialize(textReader), BrandObjects)
			
			'Initialize parent collection to add data from XML file. 
            Dim list As List(Of Brand) = New List(Of Brand)()
			
            Dim brandName As String = brands.BrandObject(0).BrandName
            Dim vehicleType As String = brands.BrandObject(0).VahicleType
            Dim modelName As String = brands.BrandObject(0).ModelName
			
			'Parent class 
            Dim brand As Brand = New Brand(brandName)
            brand.VehicleTypes = New List(Of VehicleType)()
			
            Dim vehicle As VehicleType = New VehicleType(vehicleType)
            vehicle.Models = New List(Of Model)()
			
            Dim model As Model = New Model(modelName)
            brand.VehicleTypes.Add(vehicle)
			
            list.Add(brand)

            For Each brandObj As BrandObject In brands.BrandObject

                If brandName = brandObj.BrandName Then

                    If vehicleType = brandObj.VahicleType Then
                        vehicle.Models.Add(New Model(brandObj.ModelName))
                        Continue For
                    Else
                        vehicle = New VehicleType(brandObj.VahicleType)
                        vehicle.Models = New List(Of Model)()
                        vehicle.Models.Add(New Model(brandObj.ModelName))
                        brand.VehicleTypes.Add(vehicle)
                        vehicleType = brandObj.VahicleType
                    End If

                    Continue For
                Else
                    brand = New Brand(brandObj.BrandName)
                    vehicle = New VehicleType(brandObj.VahicleType)
                    vehicle.Models = New List(Of Model)()
                    vehicle.Models.Add(New Model(brandObj.ModelName))
                    brand.VehicleTypes = New List(Of VehicleType)()
                    brand.VehicleTypes.Add(vehicle)
                    vehicleType = brandObj.VahicleType
                    list.Add(brand)
                    brandName = brandObj.BrandName
                End If
            Next

            textReader.Close()
            Return list
        End Function
    End Class

    'Parent Class 
    Public Class Brand
        Private m_brandName As String

        <DisplayNameAttribute("Brand")>
        Public Property BrandName As String
            Get
                Return m_brandName
            End Get
            Set(ByVal value As String)
                m_brandName = value
            End Set
        End Property

        Private m_vehicleTypes As IList(Of VehicleType)

        Public Property VehicleTypes As IList(Of VehicleType)
            Get
                Return m_vehicleTypes
            End Get
            Set(ByVal value As IList(Of VehicleType))
                m_vehicleTypes = value
            End Set
        End Property

        Public Sub New(ByVal brandName As String)
            m_brandName = brandName
        End Sub
    End Class
 
    'Child Class
    Public Class VehicleType
        Private m_vehicleName As String

        <DisplayNameAttribute("Vehicle Type")>
        Public Property VehicleName As String
            Get
                Return m_vehicleName
            End Get
            Set(ByVal value As String)
                m_vehicleName = value
            End Set
        End Property

        Private m_models As IList(Of Model)

        Public Property Models As IList(Of Model)
            Get
                Return m_models
            End Get
            Set(ByVal value As IList(Of Model))
                m_models = value
            End Set
        End Property

        Public Sub New(ByVal vehicle As String)
            m_vehicleName = vehicle
        End Sub
    End Class
    
	'Sub-child Class 
    Public Class Model
        Private m_modelName As String

        <DisplayNameAttribute("Model")>
        Public Property ModelName As String
            Get
                Return m_modelName
            End Get
            Set(ByVal value As String)
                m_modelName = value
            End Set
        End Property

        Public Sub New(ByVal name As String)
            m_modelName = name
        End Sub
    End Class

    <XmlRootAttribute("BrandObjects")>
    Public Class BrandObjects
        <XmlElement("BrandObject")>
        Public Property BrandObject As BrandObject()
    End Class

    Public Class BrandObject
        Public Property BrandName As String
        Public Property VahicleType As String
        Public Property ModelName As String
    End Class
End Namespace

{% endhighlight %}

{% highlight UWP %}
using Syncfusion.XlsIO;
using System.Collections.Generic;
using System.ComponentModel;
using System.IO;
using System.Xml.Serialization;

namespace ImportFromNestedCollection
{
    public sealed partial class MainPage : Page
    {
	    public MainPage()
        {
            this.InitializeComponent();
        }
		

        //Button click to import data from nested collection to Excel worksheet. 
		private async void btnGenerateExcel_Click(object sender, RoutedEventArgs e)
        {
            ExcelEngine excelEngine = new ExcelEngine();
            IApplication application = excelEngine.Excel;

            application.DefaultVersion = ExcelVersion.Excel2016;

            IWorkbook workbook = excelEngine.Excel.Workbooks.Create(1);
            IWorksheet worksheet = workbook.Worksheets[0];

            IList<Brand> vehicles = GetVehicleDetails();

            ExcelImportDataOptions importDataOptions = new ExcelImportDataOptions();

            //Imports from 4th row.
            importDataOptions.FirstRow = 4;

            //Imports column headers.
            importDataOptions.IncludeHeader = true;

            //Set layout options.
            importDataOptions.NestedDataLayoutOptions = ExcelNestedDataLayoutOptions.Default;
            
			//Set grouping option.
            importDataOptions.NestedDataGroupOptions = ExcelNestedDataGroupOptions.Collapse;
            
            //Set collapse level.
            //GroupingOption must set to ‘Collapse’ before applying ‘CollapseLevel’.
            importDataOptions.CollapseLevel = 2;
			
            //Import data from the nested collection.
            worksheet.ImportData(vehicles, importDataOptions);

            //Apply style to headers 
            worksheet["A1:C2"].Merge();
            worksheet["A1"].Text = "Automobile Brands in the US";

            worksheet.UsedRange.AutofitColumns();

            //Initializes FileSavePicker
            FileSavePicker savePicker = new FileSavePicker();
            savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
            savePicker.SuggestedFileName = "ImportData";
            savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });
	        
            //Creates a storage file from FileSavePicker
            StorageFile storageFile = await savePicker.PickSaveFileAsync();
	        
            //Saves changes to the specified storage file
            await workbook.SaveAsAsync(storageFile);

            workbook.Close();
            excelEngine.Dispose();
        }

        //Helper method to load data from XML file and add them in collections. 
        private static IList<Brand> GetVehicleDetails()
        {
            XmlSerializer deserializer = new XmlSerializer(typeof(BrandObjects));

            //Read data from XML file. 
			Assembly assembly = typeof(MainPage).GetTypeInfo().Assembly;
            Stream fileStream = assembly.GetManifestResourceStream("Sample.Data.ExportData.xml");
            TextReader textReader = new StreamReader(fileStream);
            BrandObjects brands = (BrandObjects)deserializer.Deserialize(textReader);

            //Initialize parent collection to add data from XML file. 
            List<Brand> list = new List<Brand>();

            string brandName = brands.BrandObject[0].BrandName;
            string vehicleType = brands.BrandObject[0].VahicleType;
            string modelName = brands.BrandObject[0].ModelName;

            //Parent class 
            Brand brand = new Brand(brandName);
            brand.VehicleTypes = new List<VehicleType>();

            VehicleType vehicle = new VehicleType(vehicleType);
            vehicle.Models = new List<Model>();

            Model model = new Model(modelName);
            brand.VehicleTypes.Add(vehicle);

            list.Add(brand);

            foreach (BrandObject brandObj in brands.BrandObject)
            {
                if (brandName == brandObj.BrandName)
                {
                    if (vehicleType == brandObj.VahicleType)
                    {
                        vehicle.Models.Add(new Model(brandObj.ModelName));
                        continue;
                    }
                    else
                    {
                        vehicle = new VehicleType(brandObj.VahicleType);
                        vehicle.Models = new List<Model>();
                        vehicle.Models.Add(new Model(brandObj.ModelName));
                        brand.VehicleTypes.Add(vehicle);
                        vehicleType = brandObj.VahicleType;
                    }
                    continue;
                }
                else
                {
                    brand = new Brand(brandObj.BrandName);
                    vehicle = new VehicleType(brandObj.VahicleType);
                    vehicle.Models = new List<Model>();
                    vehicle.Models.Add(new Model(brandObj.ModelName));
                    brand.VehicleTypes = new List<VehicleType>();
                    brand.VehicleTypes.Add(vehicle);
                    vehicleType = brandObj.VahicleType;
                    list.Add(brand);
                    brandName = brandObj.BrandName;
                }
            }

            textReader.Close();
            return list;
        }
    }

    //Parent Class 
    public class Brand
    {
        private string m_brandName;

        [DisplayNameAttribute("Brand")]
        public string BrandName
        {
            get { return m_brandName; }
            set { m_brandName = value; }
        }

        //Vehicle Types Collection 
        private IList<VehicleType> m_vehicleTypes;

        public IList<VehicleType> VehicleTypes
        {
            get { return m_vehicleTypes; }
            set { m_vehicleTypes = value; }
        }

        public Brand(string brandName)
        {
            m_brandName = brandName;
        }
    }

    //Child Class 
    public class VehicleType
    {
        private string m_vehicleName;

        [DisplayNameAttribute("Vehicle Type")]
        public string VehicleName
        {
            get { return m_vehicleName; }
            set { m_vehicleName = value; }
        }

        //Models collection 
        private IList<Model> m_models;
        public IList<Model> Models
        {
            get { return m_models; }
            set { m_models = value; }
        }

        public VehicleType(string vehicle)
        {
            m_vehicleName = vehicle;
        }
    }

    //Sub-child Class 
    public class Model
    {
        private string m_modelName;

        [DisplayNameAttribute("Model")]
        public string ModelName
        {
            get { return m_modelName; }
            set { m_modelName = value; }
        }

        public Model(string name)
        {
            m_modelName = name;
        }
    }

    //Helper Classes 
    [XmlRootAttribute("BrandObjects")]
    public class BrandObjects
    {
        [XmlElement("BrandObject")]
        public BrandObject[] BrandObject { get; set; }
    }

    public class BrandObject
    {
        public string BrandName { get; set; }
        public string VahicleType { get; set; }
        public string ModelName { get; set; }
    }
}
{% endhighlight %}

{% highlight ASP.NET Core %}
using Syncfusion.XlsIO;
using System.Collections.Generic;
using System.ComponentModel;
using System.IO;
using System.Xml.Serialization;

namespace ImportFromNestedCollection
{
    class Program
    {
        static void Main(string[] args)
        {
            ImportData();
        }

        //Main method to import data from nested collection to Excel worksheet. 
        private static void ImportData()
        {
            ExcelEngine excelEngine = new ExcelEngine();
            IApplication application = excelEngine.Excel;

            application.DefaultVersion = ExcelVersion.Excel2016;

            IWorkbook workbook = excelEngine.Excel.Workbooks.Create(1);
            IWorksheet worksheet = workbook.Worksheets[0];

            IList<Brand> vehicles = GetVehicleDetails();

            ExcelImportDataOptions importDataOptions = new ExcelImportDataOptions();

            //Imports from 4th row.
            importDataOptions.FirstRow = 4;

            //Imports column headers.
            importDataOptions.IncludeHeader = true;

            //Set layout options.
            importDataOptions.NestedDataLayoutOptions = ExcelNestedDataLayoutOptions.Default;
            
			//Set grouping option.
            importDataOptions.NestedDataGroupOptions = ExcelNestedDataGroupOptions.Collapse;
            
            //Set collapse level.
            //GroupingOption must set to ‘Collapse’ before applying ‘CollapseLevel’.
            importDataOptions.CollapseLevel = 2;
			
            //Import data from the nested collection.
            worksheet.ImportData(vehicles, importDataOptions);

            //Apply style to headers 
            worksheet["A1:C2"].Merge();
            worksheet["A1"].Text = "Automobile Brands in the US";

            worksheet.UsedRange.AutofitColumns();

            //Saving the workbook as stream
            FileStream stream = new FileStream("ImportData.xlsx", FileMode.Create, FileAccess.ReadWrite);
            workbook.SaveAs(stream);

            stream.Dispose();
            workbook.Close();
            excelEngine.Dispose();
        }

        //Helper method to load data from XML file and add them in collections. 
        private static IList<Brand> GetVehicleDetails()
        {
            XmlSerializer deserializer = new XmlSerializer(typeof(BrandObjects));

            //Read data from XML file. 
            FileStream stream = new FileStream(@"..\..\Data\ExportData.xml", FileMode.Open, FileAccess.Read);
            TextReader textReader = new StreamReader(stream);
            BrandObjects brands = (BrandObjects)deserializer.Deserialize(textReader);

            //Initialize parent collection to add data from XML file. 
            List<Brand> list = new List<Brand>();

            string brandName = brands.BrandObject[0].BrandName;
            string vehicleType = brands.BrandObject[0].VahicleType;
            string modelName = brands.BrandObject[0].ModelName;

            //Parent class 
            Brand brand = new Brand(brandName);
            brand.VehicleTypes = new List<VehicleType>();

            VehicleType vehicle = new VehicleType(vehicleType);
            vehicle.Models = new List<Model>();

            Model model = new Model(modelName);
            brand.VehicleTypes.Add(vehicle);

            list.Add(brand);

            foreach (BrandObject brandObj in brands.BrandObject)
            {
                if (brandName == brandObj.BrandName)
                {
                    if (vehicleType == brandObj.VahicleType)
                    {
                        vehicle.Models.Add(new Model(brandObj.ModelName));
                        continue;
                    }
                    else
                    {
                        vehicle = new VehicleType(brandObj.VahicleType);
                        vehicle.Models = new List<Model>();
                        vehicle.Models.Add(new Model(brandObj.ModelName));
                        brand.VehicleTypes.Add(vehicle);
                        vehicleType = brandObj.VahicleType;
                    }
                    continue;
                }
                else
                {
                    brand = new Brand(brandObj.BrandName);
                    vehicle = new VehicleType(brandObj.VahicleType);
                    vehicle.Models = new List<Model>();
                    vehicle.Models.Add(new Model(brandObj.ModelName));
                    brand.VehicleTypes = new List<VehicleType>();
                    brand.VehicleTypes.Add(vehicle);
                    vehicleType = brandObj.VahicleType;
                    list.Add(brand);
                    brandName = brandObj.BrandName;
                }
            }

            textReader.Close();
            return list;
        }
    }

    //Parent Class 
    public class Brand
    {
        private string m_brandName;

        [DisplayNameAttribute("Brand")]
        public string BrandName
        {
            get { return m_brandName; }
            set { m_brandName = value; }
        }

        //Vehicle Types Collection 
        private IList<VehicleType> m_vehicleTypes;

        public IList<VehicleType> VehicleTypes
        {
            get { return m_vehicleTypes; }
            set { m_vehicleTypes = value; }
        }

        public Brand(string brandName)
        {
            m_brandName = brandName;
        }
    }

    //Child Class 
    public class VehicleType
    {
        private string m_vehicleName;

        [DisplayNameAttribute("Vehicle Type")]
        public string VehicleName
        {
            get { return m_vehicleName; }
            set { m_vehicleName = value; }
        }

        //Models collection 
        private IList<Model> m_models;
        public IList<Model> Models
        {
            get { return m_models; }
            set { m_models = value; }
        }

        public VehicleType(string vehicle)
        {
            m_vehicleName = vehicle;
        }
    }

    //Sub-child Class 
    public class Model
    {
        private string m_modelName;

        [DisplayNameAttribute("Model")]
        public string ModelName
        {
            get { return m_modelName; }
            set { m_modelName = value; }
        }

        public Model(string name)
        {
            m_modelName = name;
        }
    }

    //Helper Classes 
    [XmlRootAttribute("BrandObjects")]
    public class BrandObjects
    {
        [XmlElement("BrandObject")]
        public BrandObject[] BrandObject { get; set; }
    }

    public class BrandObject
    {
        public string BrandName { get; set; }
        public string VahicleType { get; set; }
        public string ModelName { get; set; }
    }
}
{% endhighlight %}

{% highlight Xamarin %}
using Syncfusion.XlsIO;
using System.Collections.Generic;
using System.ComponentModel;
using System.IO;
using System.Xml.Serialization;

namespace ImportFromNestedCollection
{
    public partial class MainPage : ContentPage
    {
	    public MainPage()
        {
            this.InitializeComponent();
        }
		

        //Button click to import data from nested collection to Excel worksheet. 
		internal void OnButtonClicked(object sender, EventArgs e)
        {
            ExcelEngine excelEngine = new ExcelEngine();
            IApplication application = excelEngine.Excel;

            application.DefaultVersion = ExcelVersion.Excel2016;

            IWorkbook workbook = excelEngine.Excel.Workbooks.Create(1);
            IWorksheet worksheet = workbook.Worksheets[0];

            IList<Brand> vehicles = GetVehicleDetails();

            ExcelImportDataOptions importDataOptions = new ExcelImportDataOptions();

            //Imports from 4th row.
            importDataOptions.FirstRow = 4;

            //Imports column headers.
            importDataOptions.IncludeHeader = true;

            //Set layout options.
            importDataOptions.NestedDataLayoutOptions = ExcelNestedDataLayoutOptions.Default;
            
			//Set grouping option.
            importDataOptions.NestedDataGroupOptions = ExcelNestedDataGroupOptions.Collapse;
            
            //Set collapse level.
            //GroupingOption must set to ‘Collapse’ before applying ‘CollapseLevel’.
            importDataOptions.CollapseLevel = 2;

            //Import data from the nested collection.
            worksheet.ImportData(vehicles, importDataOptions);

            //Apply style to headers 
            worksheet["A1:C2"].Merge();
            worksheet["A1"].Text = "Automobile Brands in the US";

            worksheet.UsedRange.AutofitColumns();

            //Save the document as file and view the saved document

            //The operation in SaveAndView under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the xlsio/xamarin section for respective code samples
	        
            if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
            {
                Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("ImportData.xlsx", "application/msexcel", stream);
            }
            else
            {
                Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("ImportData.xlsx", "application/msexcel", stream);
            }   
	
            workbook.Close();
            excelEngine.Dispose();
        }

        //Helper method to load data from XML file and add them in collections. 
        private static IList<Brand> GetVehicleDetails()
        {
            XmlSerializer deserializer = new XmlSerializer(typeof(BrandObjects));

            //Read data from XML file.
			Assembly assembly = typeof(App).GetTypeInfo().Assembly;
            Stream fileStream = assembly.GetManifestResourceStream("Sample.Data.ExportData.xml");
            TextReader textReader = new StreamReader(fileStream);
            BrandObjects brands = (BrandObjects)deserializer.Deserialize(textReader);

            //Initialize parent collection to add data from XML file. 
            List<Brand> list = new List<Brand>();

            string brandName = brands.BrandObject[0].BrandName;
            string vehicleType = brands.BrandObject[0].VahicleType;
            string modelName = brands.BrandObject[0].ModelName;

            //Parent class 
            Brand brand = new Brand(brandName);
            brand.VehicleTypes = new List<VehicleType>();

            VehicleType vehicle = new VehicleType(vehicleType);
            vehicle.Models = new List<Model>();

            Model model = new Model(modelName);
            brand.VehicleTypes.Add(vehicle);

            list.Add(brand);

            foreach (BrandObject brandObj in brands.BrandObject)
            {
                if (brandName == brandObj.BrandName)
                {
                    if (vehicleType == brandObj.VahicleType)
                    {
                        vehicle.Models.Add(new Model(brandObj.ModelName));
                        continue;
                    }
                    else
                    {
                        vehicle = new VehicleType(brandObj.VahicleType);
                        vehicle.Models = new List<Model>();
                        vehicle.Models.Add(new Model(brandObj.ModelName));
                        brand.VehicleTypes.Add(vehicle);
                        vehicleType = brandObj.VahicleType;
                    }
                    continue;
                }
                else
                {
                    brand = new Brand(brandObj.BrandName);
                    vehicle = new VehicleType(brandObj.VahicleType);
                    vehicle.Models = new List<Model>();
                    vehicle.Models.Add(new Model(brandObj.ModelName));
                    brand.VehicleTypes = new List<VehicleType>();
                    brand.VehicleTypes.Add(vehicle);
                    vehicleType = brandObj.VahicleType;
                    list.Add(brand);
                    brandName = brandObj.BrandName;
                }
            }

            textReader.Close();
            return list;
        }
    }

    //Parent Class 
    public class Brand
    {
        private string m_brandName;

        [DisplayNameAttribute("Brand")]
        public string BrandName
        {
            get { return m_brandName; }
            set { m_brandName = value; }
        }

        //Vehicle Types Collection 
        private IList<VehicleType> m_vehicleTypes;

        public IList<VehicleType> VehicleTypes
        {
            get { return m_vehicleTypes; }
            set { m_vehicleTypes = value; }
        }

        public Brand(string brandName)
        {
            m_brandName = brandName;
        }
    }

    //Child Class 
    public class VehicleType
    {
        private string m_vehicleName;

        [DisplayNameAttribute("Vehicle Type")]
        public string VehicleName
        {
            get { return m_vehicleName; }
            set { m_vehicleName = value; }
        }

        //Models collection 
        private IList<Model> m_models;
        public IList<Model> Models
        {
            get { return m_models; }
            set { m_models = value; }
        }

        public VehicleType(string vehicle)
        {
            m_vehicleName = vehicle;
        }
    }

    //Sub-child Class 
    public class Model
    {
        private string m_modelName;

        [DisplayNameAttribute("Model")]
        public string ModelName
        {
            get { return m_modelName; }
            set { m_modelName = value; }
        }

        public Model(string name)
        {
            m_modelName = name;
        }
    }

    //Helper Classes 
    [XmlRootAttribute("BrandObjects")]
    public class BrandObjects
    {
        [XmlElement("BrandObject")]
        public BrandObject[] BrandObject { get; set; }
    }

    public class BrandObject
    {
        public string BrandName { get; set; }
        public string VahicleType { get; set; }
        public string ModelName { get; set; }
    }
}
{% endhighlight %}
{% endtabs %}

The following screenshot represents the output document of Grouped data imported from nested collection and collapsed at level 2.

![Grouped data imported from nested collection and collapsed at level 2](Working-with-Data_images/Working-with-Data_img4.png)

#### Import Data from Collection Objects with hyperlink

Essential XlsIO allows you to import images, data with URLs, and data with mail IDs as hyperlinks from various data sources binded in Collection Objects as shown below

{% tabs %}  
{% highlight c# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Import the data to worksheet
  IList<Company> reports = GetCompanyDetails();
  worksheet.ImportData(reports, 2, 1, false);

  workbook.SaveAs("ImportFromBO.xlsx");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Import the data to worksheet
  Dim reports As IList(Of Company) = GetCompanyDetails()
  worksheet.ImportData(reports, 2, 1, False)

  workbook.SaveAs("ImportFromBO.xlsx")
End Using
{% endhighlight %}

{% highlight UWP %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Import the data to worksheet
  IList<Company> reports = GetCompanyDetails();
  worksheet.ImportData(reports, 2, 1, false);

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "ImportFromBO";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight ASP.NET Core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Import the data to worksheet
  IList<Company> reports = GetCompanyDetails();
  worksheet.ImportData(reports, 2, 1, false);

  //Saving the workbook as stream
  FileStream stream = new FileStream("ImportFromBO.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Import the data to worksheet
  IList<Company> reports = GetCompanyDetails();
  worksheet.ImportData(reports, 2, 1, false);

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("ImportFromBO.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("ImportFromBO.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

The following code snippet provides supporting methods and classes for the previous code.

{% tabs %}  
{% highlight c# %}
//Gets a list of company details
private List<Company> GetCompanyDetails()
{
    List<Company> companyList = new List<Company>();

    Company company = new Company();
    company.Name = "Syncfusion";
    Hyperlink link = new Hyperlink("https://www.syncfusion.com", "", "", "Syncfusion", ExcelHyperLinkType.Url, null);
    company.Link = link;
    companyList.Add(company);

    company = new Company();
    company.Name = "Microsoft";
    link = new Hyperlink("https://www.microsoft.com", "", "", "Microsoft", ExcelHyperLinkType.Url, null);
    company.Link = link;
    companyList.Add(company);

    company = new Company();
    company.Name = "Google";
    link = new Hyperlink("https://www.google.com", "", "", "Google", ExcelHyperLinkType.Url, null);
    company.Link = link;
    companyList.Add(company);

    return companyList;
}    
public class Hyperlink : IHyperLink
{
    public IApplication Application { get; }
    public object Parent { get;}
    public string Address { get; set; }
    public string Name { get; }
    public IRange Range { get; }
    public string ScreenTip { get; set; }
    public string SubAddress { get; set; }
    public string TextToDisplay { get; set; }
    public ExcelHyperLinkType Type { get; set; }
    public IShape Shape { get; }
    public ExcelHyperlinkAttachedType AttachedType { get; }
    public byte[] Image { get; set; }

    public Hyperlink(string address, string subAddress, string screenTip, string textToDisplay, ExcelHyperLinkType type, byte[] image)
    {
        Address = address;
        ScreenTip = screenTip;
        SubAddress = subAddress;            
        TextToDisplay = textToDisplay;
        Type = type;
        Image = image;
    }
}

public class Company
{
    public string Name { get; set; }
    public Hyperlink Link { get; set; }
}

{% endhighlight %}

{% highlight vb %}
'Gets a list of company details
Private Function GetCompanyDetails() As List(Of Company)
    Dim companyList As List(Of Company) = New List(Of Company)()
    Dim company As Company = New Company()
    company.Name = "Syncfusion"
    Dim link As Hyperlink = New Hyperlink("https://www.syncfusion.com", "", "", "Syncfusion", ExcelHyperLinkType.Url, Nothing)
    company.Link = link
    companyList.Add(company)
    company = New Company()
    company.Name = "Microsoft"
    link = New Hyperlink("https://www.microsoft.com", "", "", "Microsoft", ExcelHyperLinkType.Url, Nothing)
    company.Link = link
    companyList.Add(company)
    company = New Company()
    company.Name = "Google"
    link = New Hyperlink("https://www.google.com", "", "", "Google", ExcelHyperLinkType.Url, Nothing)
    company.Link = link
    companyList.Add(company)
    Return companyList
End Function   
Public Class Hyperlink
    Inherits IHyperLink

    Public ReadOnly Property Application As IApplication
    Public ReadOnly Property Parent As Object
    Public Property Address As String
    Public ReadOnly Property Name As String
    Public ReadOnly Property Range As IRange
    Public Property ScreenTip As String
    Public Property SubAddress As String
    Public Property TextToDisplay As String
    Public Property Type As ExcelHyperLinkType
    Public ReadOnly Property Shape As IShape
    Public ReadOnly Property AttachedType As ExcelHyperlinkAttachedType
    Public Property Image As Byte()

    Public Sub New(ByVal address As String, ByVal subAddress As String, ByVal screenTip As String, ByVal textToDisplay As String, ByVal type As ExcelHyperLinkType, ByVal image As Byte())
        Address = address
        ScreenTip = screenTip
        SubAddress = subAddress
        TextToDisplay = textToDisplay
        Type = type
        Image = image
    End Sub
End Class

Public Class Company
    Public Property Name As String
    Public Property Link As Hyperlink
End Class

{% endhighlight %}

{% highlight UWP %}
//Gets a list of company details
private List<Company> GetCompanyDetails()
{
    List<Company> companyList = new List<Company>();

    Company company = new Company();
    company.Name = "Syncfusion";
    Hyperlink link = new Hyperlink("https://www.syncfusion.com", "", "", "Syncfusion", ExcelHyperLinkType.Url, null);
    company.Link = link;
    companyList.Add(company);

    company = new Company();
    company.Name = "Microsoft";
    link = new Hyperlink("https://www.microsoft.com", "", "", "Microsoft", ExcelHyperLinkType.Url, null);
    company.Link = link;
    companyList.Add(company);

    company = new Company();
    company.Name = "Google";
    link = new Hyperlink("https://www.google.com", "", "", "Google", ExcelHyperLinkType.Url, null);
    company.Link = link;
    companyList.Add(company);

    return companyList;
}    
public class Hyperlink : IHyperLink
{
    public IApplication Application { get; }
    public object Parent { get;}
    public string Address { get; set; }
    public string Name { get; }
    public IRange Range { get; }
    public string ScreenTip { get; set; }
    public string SubAddress { get; set; }
    public string TextToDisplay { get; set; }
    public ExcelHyperLinkType Type { get; set; }
    public IShape Shape { get; }
    public ExcelHyperlinkAttachedType AttachedType { get; }
    public byte[] Image { get; set; }

    public Hyperlink(string address, string subAddress, string screenTip, string textToDisplay, ExcelHyperLinkType type, byte[] image)
    {
        Address = address;
        ScreenTip = screenTip;
        SubAddress = subAddress;            
        TextToDisplay = textToDisplay;
        Type = type;
        Image = image;
    }
}

public class Company
{
    public string Name { get; set; }
    public Hyperlink Link { get; set; }
}
{% endhighlight %}

{% highlight ASP.NET Core %}
//Gets a list of company details
private List<Company> GetCompanyDetails()
{
    List<Company> companyList = new List<Company>();

    Company company = new Company();
    company.Name = "Syncfusion";
    Hyperlink link = new Hyperlink("https://www.syncfusion.com", "", "", "Syncfusion", ExcelHyperLinkType.Url, null);
    company.Link = link;
    companyList.Add(company);

    company = new Company();
    company.Name = "Microsoft";
    link = new Hyperlink("https://www.microsoft.com", "", "", "Microsoft", ExcelHyperLinkType.Url, null);
    company.Link = link;
    companyList.Add(company);

    company = new Company();
    company.Name = "Google";
    link = new Hyperlink("https://www.google.com", "", "", "Google", ExcelHyperLinkType.Url, null);
    company.Link = link;
    companyList.Add(company);

    return companyList;
}    
public class Hyperlink : IHyperLink
{
    public IApplication Application { get; }
    public object Parent { get;}
    public string Address { get; set; }
    public string Name { get; }
    public IRange Range { get; }
    public string ScreenTip { get; set; }
    public string SubAddress { get; set; }
    public string TextToDisplay { get; set; }
    public ExcelHyperLinkType Type { get; set; }
    public IShape Shape { get; }
    public ExcelHyperlinkAttachedType AttachedType { get; }
    public byte[] Image { get; set; }

    public Hyperlink(string address, string subAddress, string screenTip, string textToDisplay, ExcelHyperLinkType type, byte[] image)
    {
        Address = address;
        ScreenTip = screenTip;
        SubAddress = subAddress;            
        TextToDisplay = textToDisplay;
        Type = type;
        Image = image;
    }
}

public class Company
{
    public string Name { get; set; }
    public Hyperlink Link { get; set; }
}
{% endhighlight %}

{% highlight Xamarin %}
//Gets a list of company details
private List<Company> GetCompanyDetails()
{
    List<Company> companyList = new List<Company>();

    Company company = new Company();
    company.Name = "Syncfusion";
    Hyperlink link = new Hyperlink("https://www.syncfusion.com", "", "", "Syncfusion", ExcelHyperLinkType.Url, null);
    company.Link = link;
    companyList.Add(company);

    company = new Company();
    company.Name = "Microsoft";
    link = new Hyperlink("https://www.microsoft.com", "", "", "Microsoft", ExcelHyperLinkType.Url, null);
    company.Link = link;
    companyList.Add(company);

    company = new Company();
    company.Name = "Google";
    link = new Hyperlink("https://www.google.com", "", "", "Google", ExcelHyperLinkType.Url, null);
    company.Link = link;
    companyList.Add(company);

    return companyList;
}    
public class Hyperlink : IHyperLink
{
    public IApplication Application { get; }
    public object Parent { get;}
    public string Address { get; set; }
    public string Name { get; }
    public IRange Range { get; }
    public string ScreenTip { get; set; }
    public string SubAddress { get; set; }
    public string TextToDisplay { get; set; }
    public ExcelHyperLinkType Type { get; set; }
    public IShape Shape { get; }
    public ExcelHyperlinkAttachedType AttachedType { get; }
    public byte[] Image { get; set; }

    public Hyperlink(string address, string subAddress, string screenTip, string textToDisplay, ExcelHyperLinkType type, byte[] image)
    {
        Address = address;
        ScreenTip = screenTip;
        SubAddress = subAddress;            
        TextToDisplay = textToDisplay;
        Type = type;
        Image = image;
    }
}

public class Company
{
    public string Name { get; set; }
    public Hyperlink Link { get; set; }
}
{% endhighlight %}
{% endtabs %} 

### Import Data from Array

The following code snippet shows how to import array of data into a worksheet using **ImportArray** method.

{% tabs %}  
{% highlight c# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Initialize the Object Array
  object[] array = new object[4] { "Total Income", "Actual Expense", "Expected Expenses", "Profit" };
  //Import the Object Array to Sheet
  worksheet.ImportArray(array, 1, 1, false);

  workbook.SaveAs("ImportFromDT.xlsx");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Initialize the Array Object
  Dim array() As Object = New Object() {"Total Income", "Actual Expense", "Expected Expenses", "Profit"}
  'Import the Array Object to Sheet
  worksheet.ImportArray(array, 1, 1, False)

  workbook.SaveAs("ImportFromDT.xlsx")
End Using
{% endhighlight %}

{% highlight UWP %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Initialize the Object Array
  object[] array = new object[4] { "Total Income", "Actual Expense", "Expected Expenses", "Profit" };
  //Import the Object Array to Sheet
  worksheet.ImportArray(array, 1, 1, false);

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "ImportFromDT";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight ASP.NET Core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Initialize the Object Array
  object[] array = new object[4] { "Total Income", "Actual Expense", "Expected Expenses", "Profit" };
  //Import the Object Array to Sheet
  worksheet.ImportArray(array, 1, 1, false);

  //Saving the workbook as stream
  FileStream stream = new FileStream("ImportFromDT.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Initialize the Object Array
  object[] array = new object[4] { "Total Income", "Actual Expense", "Expected Expenses", "Profit" };
  //Import the Object Array to Sheet
  worksheet.ImportArray(array, 1, 1, false);

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("ImportFromDT.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("ImportFromDT.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}  

## Exporting from Worksheet to Data Table 

XlsIO allows to export the sheet data to a **DataTable** by using the **ExportDataTable****()** method. This method provides various options that allows to export data with specific requirement through ExcelExportDataTableOptions. 

The following code snippet illustrates on how to export data from worksheet to Data grid using **DataTable**.

{% tabs %}  
{% highlight c# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Export3.xlsx");
  IWorksheet worksheet = workbook.Worksheets[0];

  //Read data from the worksheet and Export to the DataTable
  DataTable customersTable = worksheet.ExportDataTable(worksheet.UsedRange, ExcelExportDataTableOptions.ColumnNames);

  //Binding exported DataTable to data grid, likewise it can binded to any 
  //user interface control which supports binding
  DataGrid dataGrid = new DataGrid();
  dataGrid.DataSource = customersTable;

  workbook.SaveAs("ExportToGrid.xlsx");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Read data from the worksheet and Export to the DataTable
  Dim customersTable As DataTable = sheet.ExportDataTable(sheet.UsedRange, ExcelExportDataTableOptions.ColumnNames)

  'Binding exported DataTable to data grid, likewise it can binded to any 
  'user interface control which supports binding
  Dim dataGrid As DataGrid = New DataGrid
  dataGrid.DataSource = customersTable

  workbook.SaveAs("ExportToGrid.xlsx")
End Using
{% endhighlight %}

{% highlight UWP %}
//XlsIO supports exporting of data from worksheet to data table in Windows Forms, WPF, ASP.NET, ASP.NET MVC and ASP.NET Core (2.0 onwards) platforms alone.
{% endhighlight %}

{% highlight ASP.NET Core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  FileStream inputStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Read data from the worksheet and Export to the DataTable
  DataTable customersTable = worksheet.ExportDataTable(worksheet.UsedRange, ExcelExportDataTableOptions.ColumnNames);

  //Saving the workbook as stream
  FileStream stream = new FileStream("ExportToDT.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}

//XlsIO supports binding of exported data table to data grid in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms alone.
{% endhighlight %}

{% highlight Xamarin %}
//XlsIO supports exporting of data from worksheet to data table in Windows Forms, WPF, ASP.NET, ASP.NET MVC and ASP.NET Core (2.0 onwards) platforms alone.
{% endhighlight %}
{% endtabs %}  

## Exporting from Worksheet to Collection Objects 

XlsIO allows to export the sheet data to a **Collection Objects** by using the **ExportData&lt;T&gt;()** method.

The following code snippet illustrates on how to export worksheet data into Collection Objects using **ExportData&lt;T&gt;**.

{% tabs %}  
{% highlight c# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
  IWorksheet worksheet = workbook.Worksheets[0];

  //Export worksheet data into Collection Objects
  List<Report> collectionObjects = worksheet.ExportData<Report>(1, 1, 10, 3);

  workbook.SaveAs("CollectionObjects.xlsx");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Export worksheet data into Collection Objects
  Dim collectionObjects As List(Of Report) = worksheet.ExportData(Of Report)(1, 1, 10, 3)

  workbook.SaveAs("CollectionObjects.xlsx")
End Using
{% endhighlight %}

{% highlight UWP %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  //Instantiates the File Picker
  FileOpenPicker openPicker = new FileOpenPicker();
  openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
  openPicker.FileTypeFilter.Add(".xlsx");
  openPicker.FileTypeFilter.Add(".xls");
  StorageFile file = await openPicker.PickSingleFileAsync();

  //Opens the workbook
  IWorkbook workbook = await application.Workbooks.OpenAsync(file);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Export worksheet data into Collection Objects
  List<Report> collectionObjects = worksheet.ExportData<Report>(1, 1, 10, 3);

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "CollectionObjects";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight ASP.NET Core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Export worksheet data into Collection Objects
  List<Report> collectionObjects = worksheet.ExportData<Report>(1, 1, 10, 3);

  //Saving the workbook as stream
  FileStream stream = new FileStream("CollectionObjects.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.XlsIO.Samples.Template.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Export worksheet data into Collection Objects
  List<Report> collectionObjects = worksheet.ExportData<Report>(1, 1, 10, 3);

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("CollectionObjects.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("CollectionObjects.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

The following code snippet provides supporting class for the above code. Here, the attributes DisplayNameAttribute and Bindable are used.

* [DisplayNameAttribute](https://docs.microsoft.com/en-us/dotnet/api/system.componentmodel.displaynameattribute?view=netframework-4.7.1) - to match the column headers with set of properties while exporting.
* [BindableAttribute](https://docs.microsoft.com/en-us/dotnet/api/system.componentmodel.bindableattribute?view=netframework-4.8) - to skip a property while exporting.

{% tabs %}  
{% highlight c# %}
public class Report
{
  [DisplayNameAttribute("Sales Person Name")]
  public string SalesPerson { get; set; }
  [Bindable(false)]  
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
  
  <Bindable(False)>
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
End Class
{% endhighlight %}

{% highlight UWP %}
public class Report
{
  [DisplayNameAttribute("Sales Person Name")]
  public string SalesPerson { get; set; }
  [Bindable(false)]
  public string SalesJanJun { get; set; }
  public string SalesJulDec { get; set; }

  public Report()
  {

  }
}
{% endhighlight %}

{% highlight ASP.NET Core %}
public class Report
{
  [DisplayNameAttribute("Sales Person Name")]
  public string SalesPerson { get; set; }
  [Bindable(false)]
  public string SalesJanJun { get; set; }
  public string SalesJulDec { get; set; }

  public Report()
  {

  }
}
{% endhighlight %}

{% highlight Xamarin %}
public class Report
{
  [DisplayNameAttribute("Sales Person Name")]
  public string SalesPerson { get; set; }
  [Bindable(false)]
  public string SalesJanJun { get; set; }
  public string SalesJulDec { get; set; }

  public Report()
  {

  }
}
{% endhighlight %}
{% endtabs %} 

## Export data from Excel to Nested Class Objects

XlsIO allows to export worksheet data to nested class objects. A new overload to the existing `ExportData<T>()` method helps to achieve this requirement by mapping column headers with class properties.

Let’s consider the input Excel document has the data as shown in the below screenshot. 

![Excel worksheet with data](Working-with-Data_images/Working-with-Data_img5.png)

The following code illustrates how to export data from Excel worksheet to nested class objects with column headers mapping collection.

{% tabs %}  
{% highlight c# %}
using Syncfusion.XlsIO;
using System.Collections.Generic;

namespace ImportFromNestedCollection
{
    class Program
    {
        static void Main(string[] args)
        {
            ExportData();
        }

        //Main method to Export data from worksheet to nested class objects.
        private static void ExportData()
        {
            using (ExcelEngine excelEngine = new ExcelEngine())
            {
                IApplication application = excelEngine.Excel;
                application.DefaultVersion = ExcelVersion.Excel2013;
                IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
                IWorksheet worksheet = workbook.Worksheets[0];

                //Map column headers in worksheet with class properties. 
                Dictionary<string, string> mappingProperties = new Dictionary<string, string>();
                mappingProperties.Add("Customer ID", "CustId");
                mappingProperties.Add("Customer Name", "CustName");
                mappingProperties.Add("Customer Age", "CustAge");
                mappingProperties.Add("Order ID", "CustOrder.Order_Id");
                mappingProperties.Add("Order Price", "CustOrder.Price");

                //Export worksheet data into nested class Objects.
                List<Customer> nestedClassObjects = worksheet.ExportData<Customer>(1, 1, 10, 5, mappingProperties);

                workbook.SaveAs("NestedClassObjects.xlsx");
            }
        }
    }
 
    //Customer details class
    public partial class Customer
    {
        public int CustId { get; set; }
        public string CustName { get; set; }
        public int CustAge { get; set; }
        public Order CustOrder { get; set; }
        public Customer()
        {

        }
    }

    //Order details class
    public partial class Order
    {
        public int Order_Id { get; set; }
        public double Price { get; set; }
        public Order()
        {

        }
    }
}
{% endhighlight %}

{% highlight vb %}
Imports Syncfusion.XlsIO
Imports System.Collections.Generic

Namespace ImportFromNestedCollection
    Class Program
        Private Shared Sub Main(ByVal args As String())
            ExportData()
        End Sub

        'Main method to Export data from worksheet to nested class objects. 
        Private Shared Sub ExportData()
			Using excelEngine As ExcelEngine = New ExcelEngine()
                Dim application As IApplication = excelEngine.Excel
                application.DefaultVersion = ExcelVersion.Excel2013
                Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
                Dim worksheet As IWorksheet = workbook.Worksheets(0)
				
				'Map column headers in worksheet with class properties.
                Dim mappingProperties As Dictionary(Of String, String) = New Dictionary(Of String, String)()
                mappingProperties.Add("Customer ID", "CustId")
                mappingProperties.Add("Customer Name", "CustName")
                mappingProperties.Add("Customer Age", "CustAge")
                mappingProperties.Add("Order ID", "CustOrder.Order_Id")
                mappingProperties.Add("Order Price", "CustOrder.Price")
				
				'Export worksheet data into nested class Objects.
                Dim nestedClassObjects As List(Of Customer) = worksheet.ExportData(Of Customer)(1, 1, 10, 5, mappingProperties)
				
                workbook.SaveAs("NestedClassObjects.xlsx")
            End Using
        End Sub

    End Class
    
	'Customer details class
    Public Partial Class Customer
        Public Property CustId As Integer
        Public Property CustName As String
        Public Property CustAge As Integer
        Public Property CustOrder As Order
    
        Public Sub New()
        End Sub
    End Class
    
	'Order details class
    Public Partial Class Order
        Public Property Order_Id As Integer
        Public Property Price As Double
    
        Public Sub New()
        End Sub
    End Class
End Namespace

{% endhighlight %}

{% highlight UWP %}
using Syncfusion.XlsIO;
using System.Collections.Generic;

namespace ImportFromNestedCollection
{
    public sealed partial class MainPage : Page
    {
	    public MainPage()
        {
            this.InitializeComponent();
        }
		

        //Button click to Export data from worksheet to nested class objects. 
		private async void btnGenerateExcel_Click(object sender, RoutedEventArgs e)
        {
		    using (ExcelEngine excelEngine = new ExcelEngine())
            {
                IApplication application = excelEngine.Excel;
                application.DefaultVersion = ExcelVersion.Excel2013;
                IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
                IWorksheet worksheet = workbook.Worksheets[0];

                //Map column headers in worksheet with class properties. 
                Dictionary<string, string> mappingProperties = new Dictionary<string, string>();
                mappingProperties.Add("Customer ID", "CustId");
                mappingProperties.Add("Customer Name", "CustName");
                mappingProperties.Add("Customer Age", "CustAge");
                mappingProperties.Add("Order ID", "CustOrder.Order_Id");
                mappingProperties.Add("Order Price", "CustOrder.Price");

                //Export worksheet data into nested class Objects.
                List<Customer> nestedClassObjects = worksheet.ExportData<Customer>(1, 1, 10, 5, mappingProperties);

                //Initializes FileSavePicker
                FileSavePicker savePicker = new FileSavePicker();
                savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
                savePicker.SuggestedFileName = "NestedClassObjects";
                savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });
	            
                //Creates a storage file from FileSavePicker
                StorageFile storageFile = await savePicker.PickSaveFileAsync();
	            
                //Saves changes to the specified storage file
                await workbook.SaveAsAsync(storageFile);
            }
        }
    }

    //Customer details class
    public partial class Customer
    {
        public int CustId { get; set; }
        public string CustName { get; set; }
        public int CustAge { get; set; }
        public Order CustOrder { get; set; }
        public Customer()
        {

        }
    }

    //Order details class
    public partial class Order
    {
        public int Order_Id { get; set; }
        public double Price { get; set; }
        public Order()
        {

        }
    }
}
{% endhighlight %}

{% highlight ASP.NET Core %}
using Syncfusion.XlsIO;
using System.Collections.Generic;

namespace ImportFromNestedCollection
{
    class Program
    {
        static void Main(string[] args)
        {
            ExportData();
        }

        //Main method to Export data from worksheet to nested class objects. 
        private static void ExportData()
        {
		    using (ExcelEngine excelEngine = new ExcelEngine())
            {
                IApplication application = excelEngine.Excel;
                application.DefaultVersion = ExcelVersion.Excel2013;
                IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
                IWorksheet worksheet = workbook.Worksheets[0];

                //Map column headers in worksheet with class properties. 
                Dictionary<string, string> mappingProperties = new Dictionary<string, string>();
                mappingProperties.Add("Customer ID", "CustId");
                mappingProperties.Add("Customer Name", "CustName");
                mappingProperties.Add("Customer Age", "CustAge");
                mappingProperties.Add("Order ID", "CustOrder.Order_Id");
                mappingProperties.Add("Order Price", "CustOrder.Price");

                //Export worksheet data into nested class Objects.
                List<Customer> nestedClassObjects = worksheet.ExportData<Customer>(1, 1, 10, 5, mappingProperties);

                //Saving the workbook as stream
                FileStream stream = new FileStream("NestedClassObjects.xlsx", FileMode.Create, FileAccess.ReadWrite);
                workbook.SaveAs(stream);
			    
                stream.Dispose();
            }   
        }
    }
	
	//Customer details class
    public partial class Customer
    {
        public int CustId { get; set; }
        public string CustName { get; set; }
        public int CustAge { get; set; }
        public Order CustOrder { get; set; }
        public Customer()
        {

        }
    }

    //Order details class
    public partial class Order
    {
        public int Order_Id { get; set; }
        public double Price { get; set; }
        public Order()
        {

        }
    }
}
{% endhighlight %}

{% highlight Xamarin %}
using Syncfusion.XlsIO;
using System.Collections.Generic;

namespace ImportFromNestedCollection
{
    public partial class MainPage : ContentPage
    {
	    public MainPage()
        {
            this.InitializeComponent();
        }
		
        //Button click to Export data from worksheet to nested class objects. 
		internal void OnButtonClicked(object sender, EventArgs e)
        {
		    using (ExcelEngine excelEngine = new ExcelEngine())
            {
                IApplication application = excelEngine.Excel;
                application.DefaultVersion = ExcelVersion.Excel2013;
                IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
                IWorksheet worksheet = workbook.Worksheets[0];

                //Map column headers in worksheet with class properties. 
                Dictionary<string, string> mappingProperties = new Dictionary<string, string>();
                mappingProperties.Add("Customer ID", "CustId");
                mappingProperties.Add("Customer Name", "CustName");
                mappingProperties.Add("Customer Age", "CustAge");
                mappingProperties.Add("Order ID", "CustOrder.Order_Id");
                mappingProperties.Add("Order Price", "CustOrder.Price");

                //Export worksheet data into nested class Objects.
                List<Customer> nestedClassObjects = worksheet.ExportData<Customer>(1, 1, 10, 5, mappingProperties);

                //Save the document as file and view the saved document
                //The operation in SaveAndView under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the xlsio/xamarin section for respective code samples
	            
                if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
                {
                    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("NestedClassObjects.xlsx", "application/msexcel", stream);
                }
                else
                {
                    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("NestedClassObjects.xlsx", "application/msexcel", stream);
                }
            }
        }
    }

    //Customer details class
    public partial class Customer
    {
        public int CustId { get; set; }
        public string CustName { get; set; }
        public int CustAge { get; set; }
        public Order CustOrder { get; set; }
        public Customer()
        {

        }
    }

    //Order details class
    public partial class Order
    {
        public int Order_Id { get; set; }
        public double Price { get; set; }
        public Order()
        {

        }
    }
}
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
//Initialize DataGrid control
DataGrid dataGrid = new DataGrid();
dataGrid.DataSource = GetDataTable();

ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
application.DefaultVersion = ExcelVersion.Excel2013;
IWorkbook workbook = application.Workbooks.Create();
IWorksheet worksheet = workbook.Worksheets[0];

//Import data from DataGrid control
worksheet.ImportDataGrid(dataGrid, 1, 1, true, true);

workbook.SaveAs("Output.xlsx");
workbook.Close();
excelEngine.Dispose();
{% endhighlight %}

{% highlight vb %}
'Initialize DataGrid control
Dim dataGrid As DataGrid = New DataGrid()
dataGrid.DataSource = GetDataTable()

Dim excelEngine As New ExcelEngine()
Dim application As IApplication = excelEngine.Excel
application.DefaultVersion = ExcelVersion.Excel2013
Dim workbook As IWorkbook = application.Workbooks.Create()
Dim worksheet As IWorksheet = workbook.Worksheets(0)

'Import data from DataGrid control
worksheet.ImportDataGrid(dataGrid, 1, 1, True, True)

workbook.SaveAs("Output.xlsx")
workbook.Close()
excelEngine.Dispose()
{% endhighlight %}

{% highlight UWP %}
//XlsIO supports importing of data from data grid to worksheet in Windows Forms and WPF platforms alone.
{% endhighlight %}

{% highlight ASP.NET Core %}
//XlsIO supports importing of data from data grid to worksheet in Windows Forms and WPF platforms alone.
{% endhighlight %}

{% highlight Xamarin %}
//XlsIO supports importing of data from data grid to worksheet in Windows Forms and WPF platforms alone.
{% endhighlight %}
{% endtabs %}

### GridView

Imports data from Microsoft GridView control with its header and cell formatting to Excel worksheet. The following code illustrates how to import data from Microsoft GridView control to worksheet.

{% tabs %}
{% highlight c# %}
//Initialize GridView control
GridView gridView = new GridView();
gridView.DataSource = GetDataTable();
gridView.DataBind();

ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
application.DefaultVersion = ExcelVersion.Excel2013;
IWorkbook workbook = application.Workbooks.Create();
IWorksheet worksheet = workbook.Worksheets[0];

//Import data from GridView control
worksheet.ImportGridView(gridView, 1, 1, true, true);

workbook.SaveAs("Output.xlsx");
workbook.Close();
excelEngine.Dispose();
{% endhighlight %}

{% highlight vb %}
'Initialize GridView control
Dim gridView As GridView = New GridView ()
gridView.DataSource = GetDataTable()
gridView.DataBind()

Dim excelEngine As New ExcelEngine()
Dim application As IApplication = excelEngine.Excel
application.DefaultVersion = ExcelVersion.Excel2013
Dim workbook As IWorkbook = application.Workbooks.Create()
Dim worksheet As IWorksheet = workbook.Worksheets(0)

'Import data from GridView control
worksheet.ImportGridView(gridView, 1, 1, True, True)

workbook.SaveAs("Output.xlsx")
workbook.Close()
excelEngine.Dispose()
{% endhighlight %}

{% highlight UWP %}
//XlsIO supports importing of data from data view to worksheet in Windows Forms and WPF platforms alone.
{% endhighlight %}

{% highlight ASP.NET Core %}
//XlsIO supports importing of data from data view to worksheet in Windows Forms and WPF platforms alone.
{% endhighlight %}

{% highlight Xamarin %}
//XlsIO supports importing of data from data view to worksheet in Windows Forms and WPF platforms alone.
{% endhighlight %}
{% endtabs %}

### DataGridView

Imports data from Microsoft DataGridView control with its header and cell formatting to Excel worksheet. In addition, this API imports sorted data applied in the control. The following code illustrates how to import data from Microsoft DataGridView control to worksheet.
 
{% tabs %}
{% highlight c# %}
//Initialize DataGridView control
DataGridView dataGridView = new DataGridView();
dataGridView.DataSource = GetDataTable();

//Apply sorting.
dataGridView.Sort(dataGridView.Columns[1], System.ComponentModel.ListSortDirection.Ascending);

ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
application.DefaultVersion = ExcelVersion.Excel2013;
IWorkbook workbook = application.Workbooks.Create();
IWorksheet worksheet = workbook.Worksheets[0];

//Import data from DataGridView control
worksheet.ImportDataGridView(dataGridView, 1, 1, true, true);

workbook.SaveAs("Output.xlsx");
workbook.Close();
excelEngine.Dispose();
{% endhighlight %}

{% highlight vb %}
'Initialize DataGridView control
Dim dataGridView As DataGridView = New DataGridView()
dataGridView.DataSource = GetDataTable()

'Apply sorting.
dataGridView.Sort(dataGridView.Columns(1), System.ComponentModel.ListSortDirection.Ascending)

Dim excelEngine As New ExcelEngine()
Dim application As IApplication = excelEngine.Excel
application.DefaultVersion = ExcelVersion.Excel2013
Dim workbook As IWorkbook = application.Workbooks.Create()
Dim worksheet As IWorksheet = workbook.Worksheets(0)

'Import data from DataGridView control
worksheet.ImportDataGridView(dataGridView, 1, 1, True, True)

workbook.SaveAs("Output.xlsx")
workbook.Close()
excelEngine.Dispose()
{% endhighlight %}

{% highlight UWP %}
//XlsIO supports importing of data from data grid view to worksheet in Windows Forms and WPF platforms alone.
{% endhighlight %}

{% highlight ASP.NET Core %}
//XlsIO supports importing of data from data grid view to worksheet in Windows Forms and WPF platforms alone.
{% endhighlight %}

{% highlight Xamarin %}
//XlsIO supports importing of data from data grid view to worksheet in Windows Forms and WPF platforms alone.
{% endhighlight %}
{% endtabs %}

## Import HTML Table to Excel Worksheet

### Import HTML Table

Essential XlsIO supports importing HTML tables into Excel worksheets. The **ImportHtmlTable** method loads an HTML file and imports all the tables in the file to the worksheet.  This import operation includes the table formatting that is defined within the HTML file.

The following code snippet shows how to import HTML table into Excel worksheet.
{% tabs %}
{% highlight c# %}
using Syncfusion.XlsIO;

namespace ImportHtml
{
    class ImportHtmlTable
    {
        static void Main(string[] args)
        {
            using (ExcelEngine excelEngine = new ExcelEngine())
            {
                IApplication application = excelEngine.Excel;

                application.DefaultVersion = ExcelVersion.Xlsx;

                IWorkbook workbook = application.Workbooks.Create(1);

                IWorksheet worksheet = workbook.Worksheets[0];

                //Imports HTML table into the worksheet from first row and first column
                worksheet.ImportHtmlTable("Import-HTML-Table.html", 1, 1);

                workbook.SaveAs("Import-HTML-Table.xlsx");
            }
        }
    }
}
{% endhighlight %}

{% highlight vb %}
Imports Syncfusion.XlsIO

Module ImportHtmlTable

  Sub Main()
    Using excelEngine As ExcelEngine = New ExcelEngine()

      Dim application As IApplication = excelEngine.Excel

      application.DefaultVersion = ExcelVersion.Xlsx

      Dim workbook As IWorkbook = application.Workbooks.Create(1)

      Dim worksheet As IWorksheet = workbook.Worksheets(0)

      'Imports HTML table into the worksheet from first row and first column
      worksheet.ImportHtmlTable("Import-HTML-Table.html", 1, 1)

      workbook.SaveAs("Import-HTML-Table.xlsx")
    End Using

  End Sub

End Module

{% endhighlight %}
{% highlight UWP %}
using Syncfusion.XlsIO;
using System;
using System.Collections.Generic;
using System.IO;
using Windows.Storage;
using Windows.Storage.Pickers;
using Windows.UI.Xaml;
using Windows.UI.Xaml.Controls;

namespace ImportHtml
{
    public sealed partial class MainPage : Page
    {
        public MainPage()
        {
            this.InitializeComponent();
        }

        private async void Button_Click(object sender, RoutedEventArgs e)
        {
            ExcelEngine excelEngine = new ExcelEngine();

            IApplication application = excelEngine.Excel;

            application.DefaultVersion = ExcelVersion.Xlsx;

            IWorkbook workbook = application.Workbooks.Create(1);

            IWorksheet worksheet = workbook.Worksheets[0];

            //Instantiates the File Picker
            FileOpenPicker openPicker = new FileOpenPicker();
            openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
            openPicker.FileTypeFilter.Add(".html");
            StorageFile file = await openPicker.PickSingleFileAsync();

            Stream fileStream = await file.OpenStreamForReadAsync();

            //Imports HTML table into the worksheet from first row and first column
            worksheet.ImportHtmlTable(fileStream, 1, 1);

            //Initializes FileSavePicker
            FileSavePicker savePicker = new FileSavePicker();
            savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
            savePicker.SuggestedFileName = "ImportHTMLTable";
            savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

            //Creates a storage file from FileSavePicker
            StorageFile storageFile = await savePicker.PickSaveFileAsync();

            Stream stream = await storageFile.OpenStreamForWriteAsync();

            workbook.SaveAs(stream);

            fileStream.Close();
            stream.Close();
            workbook.Close();
            excelEngine.Dispose();            
        }
    }
}
{% endhighlight %}
{% highlight ASP.NET Core %}
using Syncfusion.XlsIO;
using System.IO;

namespace ImportHtml
{
    class ImportHtmlTable
    {
        static void Main(string[] args)
        {
            using (ExcelEngine excelEngine = new ExcelEngine())
            {
                IApplication application = excelEngine.Excel;

                application.DefaultVersion = ExcelVersion.Excel2013;

                IWorkbook workbook = application.Workbooks.Create(1);

                IWorksheet worksheet = workbook.Worksheets[0];

                //Imports HTML table into the worksheet from first row and first column
                FileStream fileStream = new FileStream("Import-HTML-Table.html", FileMode.Open, FileAccess.ReadWrite);
                worksheet.ImportHtmlTable(fileStream, 1, 1);

                //Saving the workbook as stream
                FileStream stream = new FileStream("Import-HTML-Table.xlsx", FileMode.Create, FileAccess.ReadWrite);

                workbook.SaveAs(stream);
            }
        }
    }
}
{% endhighlight %}
{% highlight xamarin %}
using Syncfusion.XlsIO;
using System.IO;
using System.Reflection;
using Xamarin.Forms;

namespace ImportHtml
{
    public partial class MainPage : ContentPage
    {
        public MainPage()
        {
            InitializeComponent();
        }
        private void BtnGenerate_Clicked(object sender, System.EventArgs e)
        {
            ExcelEngine excelEngine = new ExcelEngine();
            IApplication application = excelEngine.Excel;

            Stream stream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("ImportHTMLTable.html");

            IWorkbook workbook = application.Workbooks.Create(1);
            workbook.Version = ExcelVersion.Excel2016;

            IWorksheet worksheet = workbook.Worksheets[0];

            MemoryStream outputStream = new MemoryStream();
            string fileName = "ImportHTMLTable.xlsx";
            string contentType = "application/msexcel";

			//Imports HTML table into the worksheet from first row and first column
            worksheet.ImportHtmlTable(stream, 1, 1);

            workbook.SaveAs(outputStream);

            outputStream.Position = 0;

            if (Device.RuntimePlatform == Device.UWP)
            {
                Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save(fileName, contentType, outputStream);
            }
            else
            {
                Xamarin.Forms.DependencyService.Get<ISave>().Save(fileName, contentType, outputStream);
            }
        }
    }
}
{% endhighlight %}

The following screenshot represents the image of the input HTML file with a table.

![Input document for Import HTML table](Working-with-Data_images/Working-with-Data_img6.png)

The following screenshot represents the image of the Excel output with data imported from HTML table.

![Output document imported from HTML table](Working-with-Data_images/Working-with-Data_img7.png)
{% endtabs %}
