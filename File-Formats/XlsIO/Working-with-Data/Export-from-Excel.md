---
title: Export from Excel | Syncfusion
description: Learn how to Export from Excel using Syncfusion .NET Exel (XlsIO) library without Microsoft Excel.
platform: file-formats
control: XlsIO
documentation: UG
---

# Working with Excel Data 

## Exporting Data From Excel

XlsIO provides the ability to export data from Excel to the following data.

* Data Table
* Collection Objects
* Nested Collection Objects

### Export from Excel to Data Table 

XlsIO allows to export the sheet data to a **DataTable** by using the [ExportDataTable()](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.Implementation.WorksheetImpl.html#Syncfusion_XlsIO_Implementation_WorksheetImpl_ExportDataTable_Syncfusion_XlsIO_IRange_Syncfusion_XlsIO_ExcelExportDataTableOptions_) method. This method provides various options that allows to export data with specific requirement through ExcelExportDataTableOptions. 

N> XlsIO supports exporting of data from worksheet to data table in Windows Forms, WPF, ASP.NET, ASP.NET MVC and ASP.NET Core (2.0 onwards) platforms alone.

The following code snippet illustrates on how to export data from worksheet to Data grid using **DataTable**.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
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

{% highlight c# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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
{% endtabs %}  

A complete working example to export data from Excel worksheet to DataTable in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Import%20and%20Export%20Data/Worksheet%20to%20DataTable).

#### Export to Data Table with an Event

Sometimes there may be a need to control the data export from Excel to a data table. XlsIO provides an event [ExportDataTableEvent](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.Implementation.WorksheetImpl.ExportDataTableEventHandler.html) to trigger while exporting data from an Excel worksheet to a data table. This event helps to perform the following actions through the [ExportDataTableActions](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.Implementation.ExportDataTableEventArgs.html#Syncfusion_XlsIO_Implementation_ExportDataTableEventArgs_ExportDataTableAction) enumeration.

* Default          -     Exports worksheet data to the data table without any action.
* SkipRows         -     Exports worksheet data to the data table by skipping a specific row(s).
* StopExporting    -     Stops exporting the data from Excel worksheet to the data table.

N> XlsIO supports exporting of data from worksheet to data table in Windows Forms, WPF, ASP.NET, ASP.NET MVC and ASP.NET Core (NETStandard2.0 onwards) platforms alone.

The following code snippet illustrates how to export data from an Excel worksheet to a data table by triggering an event.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;
  FileStream inputStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Event to choose an action while exporting data from Excel to data table.
  worksheet.ExportDataTableEvent += ExportDataTable_EventAction();

  //Read data from the worksheet and Export to the DataTable
  DataTable customersTable = worksheet.ExportDataTable(worksheet.UsedRange, ExcelExportDataTableOptions.ColumnNames);

  //Saving the workbook as stream
  FileStream stream = new FileStream("ExportToDT.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}

//XlsIO supports binding of exported data table to data grid in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms alone
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;
  IWorkbook workbook = application.Workbooks.Open("sample.xlsx");
  IWorksheet worksheet = workbook.Worksheets[0];

  //Event to choose an action while exporting data from Excel to data table.
  worksheet.ExportDataTableEvent += ExportDataTable_EventAction();

  //Read data from the worksheet and Export to the DataTable
  DataTable customersTable = worksheet.ExportDataTable(worksheet.UsedRange, ExcelExportDataTableOptions.ColumnNames);

  //Binding the exported data table to a data grid. It can be bound to any control that supports the data table.
  DataGrid dataGrid = new DataGrid();
  dataGrid.DataSource = customersTable;
  workbook.SaveAs("ExportToGrid.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2016
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Event to choose an action while exporting data from Excel to data table.
  sheet.ExportDataTableEvent += ExportDataTable_EventAction()

  'Read data from the worksheet and Export to the DataTable
  Dim customersTable As DataTable = sheet.ExportDataTable(sheet.UsedRange, ExcelExportDataTableOptions.ColumnNames)

  'Binding the exported data table to a data grid. It can be bound to any control that supports the data table.
  Dim dataGrid As DataGrid = New DataGrid
  dataGrid.DataSource = customersTable
  workbook.SaveAs("ExportToGrid.xlsx")
End Using
{% endhighlight %}
{% endtabs %}  

The following code is the event handler for the above code.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
private void ExportDataTable_EventAction(ExportDataTableEventArgs e)
{
  if (e.ExcelValue != null && e.ExcelValue.ToString() == "Owner")
    e.ExportDataTableAction = ExportDataTableActions.SkipRow;

  if (e.DataTableColumnIndex ==0 && e.ExcelRowIndex == 5 && e.ExcelColumnIndex == 1)
    e.ExportDataTableAction = ExportDataTableActions.StopExporting;

  if (e.ExcelValue != null && e.ExcelValue.ToString() == "Mexico D.F.")
    e.DataTableValue = "Mexico";

  if (e.ColumnType.ToString() == "Double" && e.ExcelValue != null)
    e.DataTableValue = 30;
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
private void ExportDataTable_EventAction(ExportDataTableEventArgs e)
{
  if (e.ExcelValue != null && e.ExcelValue.ToString() == "Owner")
    e.ExportDataTableAction = ExportDataTableActions.SkipRow;
   
  if (e.DataTableColumnIndex ==0 && e.ExcelRowIndex == 5 && e.ExcelColumnIndex == 1)
    e.ExportDataTableAction = ExportDataTableActions.StopExporting;
   
  if (e.ExcelValue != null && e.ExcelValue.ToString() == "Mexico D.F.")
    e.DataTableValue = "Mexico";
   
  if (e.ColumnType.ToString() == "Double" && e.ExcelValue != null)
    e.DataTableValue = 30;
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Private Sub ExportDataTable_EventAction(ByVal e As ExportDataTableEventArgs)
  If e.ExcelValue IsNot Nothing AndAlso e.ExcelValue.ToString() = "Owner" Then 
    e.ExportDataTableAction = ExportDataTableActions.SkipRow
  
  If e.DataTableColumnIndex = 0 AndAlso e.ExcelRowIndex = 5 AndAlso e.ExcelColumnIndex = 1 Then 
    e.ExportDataTableAction = ExportDataTableActions.StopExporting
  
  If e.ExcelValue IsNot Nothing AndAlso e.ExcelValue.ToString() = "Mexico D.F." Then 
    e.DataTableValue = "Mexico"
  
  If e.ColumnType.ToString() = "double" AndAlso e.ExcelValue IsNot Nothing Then
    e.DataTableValue = 30
End Sub
{% endhighlight %}
{% endtabs %}

### Export from Excel to Collection Objects 

XlsIO allows to export the sheet data to a **Collection Objects** by using the [ExportData&lt;T&gt;()](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.Implementation.WorksheetImpl.html#Syncfusion_XlsIO_Implementation_WorksheetImpl_ExportData__1_System_Int32_System_Int32_System_Int32_System_Int32_) method.

The following code snippet illustrates on how to export worksheet data into Collection Objects using **ExportData&lt;T&gt;**.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
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

{% highlight c# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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
{% endtabs %}

The following code snippet provides supporting class for the above code. Here, the attributes **DisplayNameAttribute** and **Bindable** are used.

* [DisplayNameAttribute](https://docs.microsoft.com/en-us/dotnet/api/system.componentmodel.displaynameattribute?view=netframework-4.7.1) - to match the column headers with set of properties while exporting.
* [BindableAttribute](https://docs.microsoft.com/en-us/dotnet/api/system.componentmodel.bindableattribute?view=netframework-4.8) - to skip a property while exporting.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
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

{% highlight c# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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
{% endtabs %} 

A complete working example to export data from Excel worksheet to collection objects in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Import%20and%20Export%20Data/Worksheet%20to%20CollectionObjects).

### Export from Excel to Nested Class Objects

XlsIO allows to export worksheet data to nested class objects. A new overload to the existing [ExportData<T>()](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.Implementation.WorksheetImpl.html#Syncfusion_XlsIO_Implementation_WorksheetImpl_ExportData__1_System_Int32_System_Int32_System_Int32_System_Int32_System_Collections_Generic_Dictionary_System_String_System_String__) method helps to achieve this requirement by mapping column headers with class properties.

Let’s consider the input Excel document has the data as shown in the below screenshot. 

![Excel worksheet with data](../Working-with-Data_images/Working-with-Data_img5.png)

The following code illustrates how to export data from Excel worksheet to nested class objects with column headers mapping collection.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
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
        FileStream inputStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
        IWorkbook workbook = application.Workbooks.Open(inputStream);
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

{% highlight c# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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
{% endtabs %}

A complete working example to export data from Excel worksheet to nested class in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Import%20and%20Export%20Data/Worksheet%20to%20Nested%20Class).

## Github Samples

* A complete working example to export data from Excel worksheet to DataTable in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Import%20and%20Export%20Data/Worksheet%20to%20DataTable).

* A complete working example to export data from Excel worksheet to collection objects in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Import%20and%20Export%20Data/Worksheet%20to%20CollectionObjects).

* A complete working example to export data from Excel worksheet to nested class in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Import%20and%20Export%20Data/Worksheet%20to%20Nested%20Class).

