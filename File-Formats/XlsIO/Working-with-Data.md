---
title: Working with Data
description: Learn how to import data to Excel file from ADO.NET objects, Collections, Array; and how to export data from Excel to ADO.NET objects or collections.
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
* CLR Objects
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

### Import Data from CLR Objects

Essential XlsIO allows you to import data directly from CLR Objects as shown below. 

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

The following code snippet provides supporting methods & class for the above code.

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

#### Import Data from CLR Objects with hyperlink

Essential XlsIO allows you to import data directly from CLR Objects and created hyperlinks in worksheet as shown below

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

## Exporting from Worksheet to CLR Objects 

XlsIO allows to export the sheet data to a **CLR Objects** by using the **ExportData&lt;T&gt;()** method. This method Exports Excel data into CLR objects from existing or newly created Excel document by matching set of properties and [DisplayNameAttribute](https://docs.microsoft.com/en-us/dotnet/api/system.componentmodel.displaynameattribute?view=netframework-4.7.1).

The following code snippet illustrates on how to export worksheet data into CLR Objects using **ExportData&lt;T&gt;**.

{% tabs %}  
{% highlight c# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
  IWorksheet worksheet = workbook.Worksheets[0];

  //Export worksheet data into CLR Objects
  List<Report> clrObjects = worksheet.ExportData<Report>(1, 1, 10, 3);

  workbook.SaveAs("CLRObjects.xlsx");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Export worksheet data into CLR Objects
  Dim clrObjects As List(Of Report) = worksheet.ExportData(Of Report)(1, 1, 10, 3)

  workbook.SaveAs("CLRObjects.xlsx")
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

  //Export worksheet data into CLR Objects
  List<Report> clrObjects = worksheet.ExportData<Report>(1, 1, 10, 3);

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "CLRObjects";
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

  //Export worksheet data into CLR Objects
  List<Report> clrObjects = worksheet.ExportData<Report>(1, 1, 10, 3);

  //Saving the workbook as stream
  FileStream stream = new FileStream("CLRObjects.xlsx", FileMode.Create, FileAccess.ReadWrite);
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

  //Export worksheet data into CLR Objects
  List<Report> clrObjects = worksheet.ExportData<Report>(1, 1, 10, 3);

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("CLRObjects.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("CLRObjects.xlsx", "application/msexcel", stream);
  }
}
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
End Class
{% endhighlight %}

{% highlight UWP %}
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

{% highlight ASP.NET Core %}
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

{% highlight Xamarin %}
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