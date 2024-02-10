---
title: Export to Excel | Syncfusion
description: Learn how to Export to Excel using Syncfusion .NET Exel (XlsIO) library without Microsoft Excel.
platform: file-formats
control: XlsIO
documentation: UG
---

# Working with Excel Data 

## Exporting Data to Excel

XlsIO provides the ability to export data to a worksheet from the following data.

* Data Table
* Data Column
* Data View
* Collection Objects
* Nested Collection Objects
* Array
* Microsoft Grid Controls
* HTML Table

### Export from DataTable to Excel

The following code snippet illustrates on how to export from DataTable to a worksheet using [ImportDataTable](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorksheet.html#Syncfusion_XlsIO_IWorksheet_ImportDataTable_System_Data_DataTable_Syncfusion_XlsIO_IName_System_Boolean_System_Int32_System_Int32_) method.

N> XlsIO supports exporting from data table to a worksheet in Windows Forms, WPF, ASP.NET, ASP.NET MVC and ASP.NET Core (2.0 onwards) platforms alone.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
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

{% highlight c# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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
{% endtabs %}  

A complete working example to export from DataTable to an Excel worksheet in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Import%20and%20Export%20Data/DataTable%20to%20Worksheet).  

An online sample link to [export from Data table to an Excel Worksheet](https://ej2.syncfusion.com/aspnetcore/Excel/ImportExportDataTable#/material3) in ASP.NET Core.

### Export from DataColumn to Excel

The following code snippet illustrates how to export from DataColumn to a worksheet using [ImportDataColumn](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorksheet.html#Syncfusion_XlsIO_IWorksheet_ImportDataColumn_System_Data_DataColumn_System_Boolean_System_Int32_System_Int32_) method.

N> XlsIO supports exporting from DataColumn to a worksheet in Windows Forms, WPF, ASP.NET, ASP.NET MVC and ASP.NET Core (2.0 onwards) platforms alone.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
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

{% highlight c# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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
{% endtabs %}  

A complete working example to export from DataColumn to an Excel worksheet in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Import%20and%20Export%20Data/DataColumn%20to%20Worksheet).

### Export from DataView to Excel

The following code snippet illustrates how to Export from DataView to a worksheet using [ImportDataView](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorksheet.html#Syncfusion_XlsIO_IWorksheet_ImportDataView_System_Data_DataView_System_Boolean_System_Int32_System_Int32_) method.

N> XlsIO supports exporting from DataView to a worksheet in Windows Forms, WPF, ASP.NET, ASP.NET MVC and ASP.NET Core (2.0 onwards) platforms alone.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
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

{% highlight c# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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
{% endtabs %} 

A complete working example to Export from DataView to an Excel worksheet in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Import%20and%20Export%20Data/DataView%20to%20Worksheet).

### Export from Collection of Objects to Excel

Essential XlsIO allows you to export from collection of objects to a worksheet using [ImportData](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorksheet.html#Syncfusion_XlsIO_IWorksheet_ImportData_System_Collections_IEnumerable_Syncfusion_XlsIO_ExcelImportDataOptions_) method.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
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

{% highlight c# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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
{% endtabs %}

The following code snippet provides supporting class for the above code. Here, the attributes DisplayNameAttribute and Bindable are used.

* [DisplayNameAttribute](https://docs.microsoft.com/en-us/dotnet/api/system.componentmodel.displaynameattribute?view=netframework-4.7.1) - to customize the column header name while importing.
* [BindableAttribute](https://docs.microsoft.com/en-us/dotnet/api/system.componentmodel.bindableattribute?view=netframework-4.8) - to skip a property while importing.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
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

{% highlight c# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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
{% endtabs %}  

A complete working example to export from collection of objects to an Excel worksheet in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Import%20and%20Export%20Data/CollectionObjects%20to%20Worksheet).

An online sample link to [export from collection of objects to an Excel Worksheet](https://ej2.syncfusion.com/aspnetcore/Excel/CollectionObjects#/material3) in ASP.NET Core.

#### Options to Export from Collection of Objects to Excel

[ExcelImportDataOptions](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelImportDataOptions.html) is a support class for [ImportData](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorksheet.html#Syncfusion_XlsIO_IWorksheet_ImportData_System_Collections_IEnumerable_Syncfusion_XlsIO_ExcelImportDataOptions_) method which contains various properties to export from collection of objects to Excel with formatting. 

**ExcelImportDataOptions** class contains the following properties:

FirstRow - Specifies first row from where the data should be imported.
FirstColumn - Specifies first column from where the data should be imported.
IncludeHeader - Specifies whether class properties names must be imported or not.
PreserveTypes - Indicates whether XlsIO should preserve column types from Data. By default, preserve type is TRUE. Setting it to True will import data based on column type, otherwise will import based on value type.

The following code snippet illustrates how to export from collection of objects to a worksheet using **ImportData** method with **ExcelImportDataOptions** class.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
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

{% highlight c# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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
{% endtabs %}

The following code snippet provides supporting class for the above code.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
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

{% highlight c# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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
{% endtabs %}

A complete working example to export from collection of objects to an Excel worksheet with options in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Import%20and%20Export%20Data/Import%20Data%20Options).

### Export from Nested Collection Objects

Export hierarchical data from nested collections to a worksheet helps the user to analyze data in its structure. XlsIO provides more flexible options to analyze such data by exporting in different layouts and grouping.

Here, data can be exported with the following layout options:

* **Default** - Parent records imported in the first row of its collection.
* **Merge** - Parent records imported in merged rows. 
* **Repeat** - Parent records imported in all the rows. 

Here, data can be exported with the following grouping options:

* **Expand** – Imported data will be grouped and expanded.
* **Collapse** – Imported data will be grouped and collapsed at first level, by default.

Let’s see these options in detail along with code examples and screenshots.

#### Layout Options

##### Default layout option

This option adds the property value once per object for the corresponding records in the column while importing.

The following code snippet illustrates how to export from nested collection objects with default layout option. The input XML file used in the code can be downloaded [here](https://www.syncfusion.com/downloads/support/directtrac/general/ze/ExportData831552872.zip).

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
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
      FileStream stream = new FileStream("../../Data/ExportData.xml", FileMode.Open, FileAccess.Read);
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

{% highlight c# tabtitle="C# [Windows-specific]" %}
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
      TextReader textReader = new StreamReader("../../Data/ExportData.xml");
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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
      Dim textReader As TextReader = New StreamReader("../../Data/ExportData.xml")
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
{% endtabs %}

A complete working example to export from nested collection objects to an Excel worksheet with layout option in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Import%20and%20Export%20Data/Layout%20Options).

The following screenshot represents the output document with Default layout option.

![Output document with Default layout option](../Working-with-Data_images/Working-with-Data_img1.png)

##### Merge layout option

This option merges the cells in the column for each object while exporting.

The following code snippet helps to export from nested collection objects with merge layout option.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
importDataOptions.NestedDataLayoutOptions = ExcelNestedDataLayoutOptions.Merge;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
importDataOptions.NestedDataLayoutOptions = ExcelNestedDataLayoutOptions.Merge;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
importDataOptions.NestedDataLayoutOptions = ExcelNestedDataLayoutOptions.Merge
{% endhighlight %}
{% endtabs %}

The following screenshot represents the output document with Merge layout option.

![Output document with Merge layout option](../Working-with-Data_images/Working-with-Data_img2.png)

##### Repeat layout option

This option repeats the parent records exported in all the rows.

The following code snippet helps to export from nested collection objects with repeat layout option.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
importDataOptions.NestedDataLayoutOptions = ExcelNestedDataLayoutOptions.Repeat;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
importDataOptions.NestedDataLayoutOptions = ExcelNestedDataLayoutOptions.Repeat;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
importDataOptions.NestedDataLayoutOptions = ExcelNestedDataLayoutOptions.Repeat
{% endhighlight %}
{% endtabs %}

The following screenshot represents the output document with Repeat layout option.

![Output document with Repeat layout option](../Working-with-Data_images/Working-with-Data_img3.png)

#### Grouping Options

##### Export hierarchical data to Excel with grouping option

Hierarchical data exported into Excel worksheet must be shown its structure to analyze more flexible. In addition, if the data is grouped according to its level, it is easier to analyze. XlsIO supports to export hierarchical data from nested collection and group them while exporting.

The following are the options that is supported to group on export.

* **Expand** – Exported data will be grouped and expanded.
* **Collapse** – Exported data will be grouped and collapsed at first level, by default.

In addition, [CollapseLevel](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelImportDataOptions.html#Syncfusion_XlsIO_ExcelImportDataOptions_CollapseLevel) will group and collapse the mentioned level, upto the maximum of 8 levels.

The following code snippet illustrates how to export hierarchical data from nested collection objects with collapse group option.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
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
      FileStream stream = new FileStream("../../Data/ExportData.xml", FileMode.Open, FileAccess.Read);
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

{% highlight c# tabtitle="C# [Windows-specific]" %}
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
      TextReader textReader = new StreamReader("../../Data/ExportData.xml");
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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
      Dim textReader As TextReader = New StreamReader("../../Data/ExportData.xml")
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
{% endtabs %}

A complete working example to export from hierarchical data to an Excel worksheet with grouping option in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Import%20and%20Export%20Data/Grouping%20Options).

The following screenshot represents the output document of Grouped data exported from nested collection and collapsed at level 2.

![Grouped data exported from nested collection and collapsed at level 2](../Working-with-Data_images/Working-with-Data_img4.png)

#### Export Data from Collection Objects with hyperlink

Essential XlsIO allows you to export images, data with URLs, and data with mail IDs as hyperlinks from various data sources binded in Collection Objects as shown below

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
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

{% highlight c# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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
{% endtabs %}

The following code snippet provides supporting methods and classes for the previous code.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
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

{% highlight c# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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
{% endtabs %} 

A complete working example to export data from collection objects with hyperlink to an Excel worksheet in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Import%20and%20Export%20Data/Import%20with%20Hyperlink).

An online sample link to [export from nested collection of objects to an Excel Worksheet](https://ej2.syncfusion.com/aspnetcore/Excel/ImportNestedCollection#/material3) in ASP.NET Core.

### Export from Array

The following code snippet shows how to export from array to a worksheet using [ImportArray](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.Implementation.WorksheetImpl.html#Syncfusion_XlsIO_Implementation_WorksheetImpl_ImportArray_System_DateTime___System_Int32_System_Int32_System_Boolean_) method.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
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

{% highlight c# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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
{% endtabs %}  

A complete working example to export from array to an Excel worksheet in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Import%20and%20Export%20Data/Array%20to%20Worksheet).

### Export Data from DataGrid, GridView and DataGridView to Excel

XlsIO provides support to export data from various Microsoft grid controls with its cell formatting. The supported grid controls are: 

* DataGrid
* GridView
* DataGridView

#### DataGrid

Exports data from Microsoft DataGrid control with its header and cell formatting to Excel worksheet. The following code illustrates how to export data from Microsoft DataGrid control to worksheet.
 
N> GetDataTable() method returns DataTable of applicable data to export.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//XlsIO supports exporting of data from data grid to worksheet in Windows Forms and WPF platforms alone.
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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
{% endtabs %}

#### GridView

Exports data from Microsoft GridView control with its header and cell formatting to Excel worksheet. The following code illustrates how to export data from Microsoft GridView control to worksheet.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//XlsIO supports exporting of data from data view to worksheet in Windows Forms and WPF platforms alone.
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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
{% endtabs %}

#### DataGridView

Export data from Microsoft DataGridView control with its header and cell formatting to Excel worksheet. In addition, this API exports sorted data applied in the control. The following code illustrates how to export data from Microsoft DataGridView control to worksheet.
 
{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//XlsIO supports exporting of data from data grid view to worksheet in Windows Forms and WPF platforms alone.
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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
{% endtabs %}

A complete working example to export from data grid view to an Excel worksheet in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Import%20and%20Export%20Data/DataGridView%20to%20Worksheet/NET%20Framework/DataGridView%20to%20Worksheet).

### Export from HTML Table to Excel Worksheet

#### Export HTML Table

Essential XlsIO supports export HTML tables from a webpage to Excel worksheets. The [ImportHtmlTable](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.Implementation.WorksheetImpl.html#Syncfusion_XlsIO_Implementation_WorksheetImpl_ImportHtmlTable_System_IO_Stream_System_Int32_System_Int32_) method loads an HTML file and imports all the tables in the file to the worksheet.  This import operation includes the table formatting that is defined within the HTML file.

The following code snippet shows how to export HTML table to an Excel worksheet.
{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
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
        application.DefaultVersion = ExcelVersion.Xlsx;
        IWorkbook workbook = application.Workbooks.Create(1);
        IWorksheet worksheet = workbook.Worksheets[0];

        //Exports HTML table to the worksheet from first row and first column
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

{% highlight c# tabtitle="C# [Windows-specific]" %}
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

        //Exports HTML table to the worksheet from first row and first column
        worksheet.ImportHtmlTable("Import-HTML-Table.html", 1, 1);
        workbook.SaveAs("Import-HTML-Table.xlsx");
      }
    }
  }
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Imports Syncfusion.XlsIO

Module ImportHtmlTable
  Sub Main()
    Using excelEngine As ExcelEngine = New ExcelEngine()
      Dim application As IApplication = excelEngine.Excel
      application.DefaultVersion = ExcelVersion.Xlsx
      Dim workbook As IWorkbook = application.Workbooks.Create(1)
      Dim worksheet As IWorksheet = workbook.Worksheets(0)

      'Exports HTML table to the worksheet from first row and first column
      worksheet.ImportHtmlTable("Import-HTML-Table.html", 1, 1)
      workbook.SaveAs("Import-HTML-Table.xlsx")
    End Using
  End Sub
End Module
{% endhighlight %}
{% endtabs %}

A complete working example to export from HTML table to an Excel worksheet in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Import%20and%20Export%20Data/HTML%20Table%20to%20Worksheet).

An online sample link to [export from HTML table to an Excel worksheet](https://ej2.syncfusion.com/aspnetcore/Excel/HTMLToWorksheet#/material3) in ASP.NET Core.

The following screenshot represents the image of the input HTML file with a table.

![Input document with HTML table](../Working-with-Data_images/Working-with-Data_img6.png)

The following screenshot represents the image of the Excel output with data exported from the webpage with the HTML table.

![Output document with HTML table](../Working-with-Data_images/Working-with-Data_img7.png)

N> Syncfusion XlsIO supports exporting HTML tables with the inline styles alone. HTML documents with embedded styles or style sheets are not supported.

N> Syncfusion XlsIO depends on the XMLDocument object to load HTML string in which the "<" and "&" symbols are invalid. These symbols needs to be changed as "&lt;" and "&amp;" respectively, to overcome the xml exception.

N> Data formatting can be applied to the Excel cells only after exporting the HTML table to Excel.

#### Export HTML Table with Formula

Syncfusion XlsIO also supports exporting HTML table with formula to an Excel worksheet. The following code snippet explains this.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
worksheet.ImportHtmlTable("Sample.html", 1, 1, HtmlImportOptions.DetectFormulas);
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
worksheet.ImportHtmlTable("Sample.html", 1, 1, HtmlImportOptions.DetectFormulas);
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
worksheet.ImportHtmlTable("Sample.html", 1, 1, HtmlImportOptions.DetectFormulas)
{% endhighlight %}
{% endtabs %}

## Blogs

* [Export from DataTable to an Excel worksheet](https://www.syncfusion.com/blogs/post/export-data-to-excel-csharp.aspx#DataTable-to-Excel).

* [Export from collection of objects to an Excel worksheet](https://www.syncfusion.com/blogs/post/export-data-to-excel-csharp.aspx#objects-to-Excel)

* [Export from nested collection of objects to an Excel Worksheet](https://www.syncfusion.com/blogs/post/export-data-from-collection-to-excel-and-group-csharp.aspx#nested-collection-to-excel-worksheet)

* [Export from array to an Excel worksheet](https://www.syncfusion.com/blogs/post/export-data-to-excel-csharp.aspx#Array-to-Excel)

* [Export data from microsoft grid controls to an Excel worksheet](https://www.syncfusion.com/blogs/post/export-data-to-excel-csharp.aspx#DataGrid-GridView-DataGridView-to-Excel)

* [Export data from HTML table to an Excel worksheet](https://www.syncfusion.com/blogs/post/easy-steps-to-export-html-tables-to-an-excel-worksheet-in-c.aspx)

## Github Samples

* A complete working example to export from DataTable to an Excel worksheet in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Import%20and%20Export%20Data/DataTable%20to%20Worksheet).

* A complete working example to export from DataColumn to an Excel worksheet in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Import%20and%20Export%20Data/DataColumn%20to%20Worksheet).

* A complete working example to Export from DataView to an Excel worksheet in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Import%20and%20Export%20Data/DataView%20to%20Worksheet).

* A complete working example to export from collection of objects to an Excel worksheet in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Import%20and%20Export%20Data/CollectionObjects%20to%20Worksheet).

* A complete working example to export from collection of objects to an Excel worksheet with options in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Import%20and%20Export%20Data/Import%20Data%20Options).

* A complete working example to export from nested collection objects to an Excel worksheet with layout option in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Import%20and%20Export%20Data/Layout%20Options).

* A complete working example to export from hierarchical data to an Excel worksheet with grouping option in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Import%20and%20Export%20Data/Grouping%20Options).

* A complete working example to export data from collection objects with hyperlink to an Excel worksheet in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Import%20and%20Export%20Data/Import%20with%20Hyperlink).

* A complete working example to export from array to an Excel worksheet in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Import%20and%20Export%20Data/Array%20to%20Worksheet).

* A complete working example to export from data grid view to an Excel worksheet in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Import%20and%20Export%20Data/DataGridView%20to%20Worksheet/NET%20Framework/DataGridView%20to%20Worksheet).

* A complete working example to export from HTML table to an Excel worksheet in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Import%20and%20Export%20Data/HTML%20Table%20to%20Worksheet).