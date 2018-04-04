---
title: Working with Tables
description: Briefs about tables
platform: File-formats
control: XlsIO
documentation: UG
---
# Working with Tables

## Creating a Table

XlsIO provides support to read and write table which helps to organize and analyze related data. 

* **IListObjects** represents a collection of tables in the worksheet. 
* **IListObject** represent a table in the worksheet

Also, you can create a calculated column in table. For more details, refer [here](/file-formats/xlsio/working-with-formulas#calculated-column).

N> In XlsIO, Tables are supported only for Excel 2007 and later formats (*.xlsx files).

The below code sample explains the creation of a simple table by the range of data from an existing worksheet

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

IWorksheet worksheet = workbook.Worksheets[0];

//Create Table with data in the given range
IListObject table = worksheet.ListObjects.Create("Table1", worksheet ["A1:C8"]);

string fileName = "Output.xlsx";

workbook.SaveAs(fileName);

workbook.Close();

excelEngine.Dispose();         



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As 

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

Dim worksheet As IWorksheet = workbook.Worksheets(0)

'Create Table with data in the given range
Dim table As IListObject = worksheet.ListObjects.Create("Table1", worksheet ("A1:C8"))

Dim fileName As String = "Output.xlsx"

workbook.SaveAs(fileName)

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

{% highlight UWP %}
//Gets assembly
Assembly assembly = typeof(App).GetTypeInfo().Assembly;

//Gets input Excel document from embedded resource collection
Stream inputStream = assembly.GetManifestResourceStream("Sample.xlsx");

ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = await application.Workbooks.OpenAsync(inputStream, ExcelOpenType.Automatic);

IWorksheet worksheet = workbook.Worksheets[0];

//Create Table with data in the given range
IListObject table = worksheet.ListObjects.Create("Table1", worksheet["A1:C8"]);

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();

savePicker.SuggestedStartLocation = PickerLocationId.Desktop;

savePicker.SuggestedFileName = "Output";

savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await workbook.SaveAsAsync(storageFile);

inputStream.Dispose();

workbook.Close();

excelEngine.Dispose();
{% endhighlight %}

{% highlight .netcore %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);

IWorkbook workbook = application.Workbooks.Open(fileStream, ExcelOpenType.Automatic);

IWorksheet worksheet = workbook.Worksheets[0];

//Create Table with data in the given range
IListObject table = worksheet.ListObjects.Create("Table1", worksheet["A1:C8"]);

string fileName = "Output.xlsx";

//Saving the workbook as stream
FileStream stream = new FileStream(fileName, FileMode.Create, FileAccess.ReadWrite);

workbook.SaveAs(stream);

stream.Dispose();

workbook.Close();

excelEngine.Dispose();
{% endhighlight %}

{% highlight Xamarin %}
//Gets assembly
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
           
//Gets input Excel document from embedded resource collection
Stream inputStream = assembly.GetManifestResourceStream("Sample.xlsx");

ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelOpenType.Automatic);

IWorksheet worksheet = workbook.Worksheets[0];

//Create Table with data in the given range
IListObject table = worksheet.ListObjects.Create("Table1", worksheet["A1:C8"]);

string fileName = "Output.xlsx";

//Saving the workbook as stream
MemoryStream outputStream = new MemoryStream();

workbook.SaveAs(outputStream);

workbook.Close();

excelEngine.Dispose();

//Save the Excel file
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    await DependencyService.Get<ISaveWindowsPhone>().Save(fileName, "application/msexcel", outputStream);
else
    DependencyService.Get<ISave>().Save(fileName, "application/msexcel", outputStream);

//Dispose the input and output stream instances
inputStream.Dispose();

outputStream.Dispose();
{% endhighlight %}

{% endtabs %}  

## Accessing a Table

Existing tables in the worksheet can be accessed, as shown below. 

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

IWorksheet worksheet = workbook.Worksheets[0];

//Accessing first table in the sheet
IListObject table = worksheet.ListObjects[0];

//Modifying table name
table.Name = "SalesTable";

string fileName = "Output.xlsx";

workbook.SaveAs(fileName);

workbook.Close();

excelEngine.Dispose();         



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

Dim worksheet As IWorksheet = workbook.Worksheets(0)

'Accessing first table in the sheet
Dim table As IListObject = worksheet.ListObjects(0)

'Modifying table name
table.Name = "SalesTable"

Dim fileName As String = "Output.xlsx"

workbook.SaveAs(fileName)

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

{% highlight UWP %}
//Gets assembly
Assembly assembly = typeof(App).GetTypeInfo().Assembly;

//Gets input Excel document from embedded resource collection
Stream inputStream = assembly.GetManifestResourceStream("Table.Sample.xlsx");

ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = await application.Workbooks.OpenAsync(inputStream, ExcelOpenType.Automatic);

IWorksheet worksheet = workbook.Worksheets[0];

//Accessing first table in the sheet
IListObject table = worksheet.ListObjects[0];

//Modifying table name
table.Name = "SalesTable";

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();

savePicker.SuggestedStartLocation = PickerLocationId.Desktop;

savePicker.SuggestedFileName = "Output";

savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await workbook.SaveAsAsync(storageFile);

inputStream.Dispose();

workbook.Close();

excelEngine.Dispose();
{% endhighlight %}

{% highlight .netcore %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);

IWorkbook workbook = application.Workbooks.Open(fileStream, ExcelOpenType.Automatic);

IWorksheet worksheet = workbook.Worksheets[0];

//Accessing first table in the sheet
IListObject table = worksheet.ListObjects[0];

//Modifying table name
table.Name = "SalesTable";

string fileName = "Output.xlsx";

//Saving the workbook as stream
FileStream stream = new FileStream(fileName, FileMode.Create, FileAccess.ReadWrite);

workbook.SaveAs(stream);

stream.Dispose();

workbook.Close();

excelEngine.Dispose();
{% endhighlight %}

{% highlight Xamarin %}
//Gets assembly
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
           
//Gets input Excel document from embedded resource collection
Stream inputStream = assembly.GetManifestResourceStream("Table.Sample.xlsx");

ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelOpenType.Automatic);

IWorksheet worksheet = workbook.Worksheets[0];

//Accessing first table in the sheet
IListObject table = worksheet.ListObjects[0];

//Modifying table name
table.Name = "SalesTable";

string fileName = "Output.xlsx";

//Saving the workbook as stream
MemoryStream outputStream = new MemoryStream();

workbook.SaveAs(outputStream);

workbook.Close();

excelEngine.Dispose();

//Save the Excel file
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    await DependencyService.Get<ISaveWindowsPhone>().Save(fileName, "application/msexcel", outputStream);
else
    DependencyService.Get<ISave>().Save(fileName, "application/msexcel", outputStream);

//Dispose the input and output stream instances
inputStream.Dispose();

outputStream.Dispose();
{% endhighlight %}
{% endtabs %}  

## Formatting a Table

You can apply built-in styles to table using XlsIO. You can also customize the table with other table styles options such as Header/total row, first/last column and banded rows to make a table easier to read.

The below code snippet illustrates how to apply built-in table style.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

IWorksheet worksheet = workbook.Worksheets[0];

//Creating a table
IListObject table = worksheet.ListObjects.Create("Table1", worksheet ["A1:C8"]);

//Formatting table with a built-in style
table.BuiltInTableStyle = TableBuiltInStyles.TableStyleMedium9;

string fileName = "Output.xlsx";

workbook.SaveAs(fileName);

workbook.Close();

excelEngine.Dispose();         



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

Dim worksheet As IWorksheet = workbook.Worksheets(0)

'Creating a table
Dim table As IListObject = worksheet.ListObjects.Create("Table1", worksheet ("A1:C8"))

'Formatting table with a built-in style
table.BuiltInTableStyle = TableBuiltInStyles.TableStyleMedium9

Dim fileName As String = "Output.xlsx"

workbook.SaveAs(fileName)

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

{% highlight UWP %}
//Gets assembly
Assembly assembly = typeof(App).GetTypeInfo().Assembly;

//Gets input Excel document from embedded resource collection
Stream inputStream = assembly.GetManifestResourceStream("Table.Sample.xlsx");

ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = await application.Workbooks.OpenAsync(inputStream, ExcelOpenType.Automatic);

IWorksheet worksheet = workbook.Worksheets[0];

//Creating a table
IListObject table = worksheet.ListObjects.Create("Table1", worksheet["A1:C8"]);

//Formatting table with a built-in style
table.BuiltInTableStyle = TableBuiltInStyles.TableStyleMedium9;

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();

savePicker.SuggestedStartLocation = PickerLocationId.Desktop;

savePicker.SuggestedFileName = "Output";

savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await workbook.SaveAsAsync(storageFile);

inputStream.Dispose();

workbook.Close();

excelEngine.Dispose();
{% endhighlight %}

{% highlight .netcore %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);

IWorkbook workbook = application.Workbooks.Open(fileStream, ExcelOpenType.Automatic);

IWorksheet worksheet = workbook.Worksheets[0];

//Creating a table
IListObject table = worksheet.ListObjects.Create("Table1", worksheet["A1:C8"]);

//Formatting table with a built-in style
table.BuiltInTableStyle = TableBuiltInStyles.TableStyleMedium9;

string fileName = "Output.xlsx";

//Saving the workbook as stream
FileStream stream = new FileStream(fileName, FileMode.Create, FileAccess.ReadWrite);

workbook.SaveAs(stream);

stream.Dispose();

workbook.Close();

excelEngine.Dispose();
{% endhighlight %}

{% highlight Xamarin %}
//Gets assembly
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
           
//Gets input Excel document from embedded resource collection
Stream inputStream = assembly.GetManifestResourceStream("Table.Sample.xlsx");

ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelOpenType.Automatic);

IWorksheet worksheet = workbook.Worksheets[0];

//Creating a table
IListObject table = worksheet.ListObjects.Create("Table1", worksheet["A1:C8"]);

//Formatting table with a built-in style
table.BuiltInTableStyle = TableBuiltInStyles.TableStyleMedium9;

string fileName = "Output.xlsx";

//Saving the workbook as stream
MemoryStream outputStream = new MemoryStream();

workbook.SaveAs(outputStream);

workbook.Close();

excelEngine.Dispose();

//Save the Excel file
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    await DependencyService.Get<ISaveWindowsPhone>().Save(fileName, "application/msexcel", outputStream);
else
    DependencyService.Get<ISave>().Save(fileName, "application/msexcel", outputStream);

//Dispose the input and output stream instances
inputStream.Dispose();

outputStream.Dispose();
{% endhighlight %}
{% endtabs %}  
## Insert/Remove Columns in a Table

IListObject is a collection of columns, whereas a single column is represented by an instance of **IListObjectColumn**. XlsIO provides support to insert or remove columns in a table through worksheet, as below.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

IWorksheet worksheet = workbook.Worksheets[0];

//Creating a table
IListObject table = worksheet.ListObjects.Create("Table1", worksheet ["A1:C8"]);

//Inserting a column in the table
worksheet.InsertColumn(2, 2);

// Removing a column from the table
worksheet.DeleteColumn(2, 1);

string fileName = "Output.xlsx";

workbook.SaveAs(fileName);

workbook.Close();

excelEngine.Dispose();         



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

Dim worksheet As IWorksheet = workbook.Worksheets(0)

'Creating Table
Dim table As IListObject = worksheet.ListObjects.Create("Table1", worksheet ("A1:C8"))

'Inserting a column in the table
worksheet.InsertColumn(2, 2)

'Removing a column from the table
worksheet.DeleteColumn(2, 1)

Dim fileName As String = "Output.xlsx"

workbook.SaveAs(fileName)

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

{% highlight UWP %}
//Gets assembly
Assembly assembly = typeof(App).GetTypeInfo().Assembly;

//Gets input Excel document from embedded resource collection
Stream inputStream = assembly.GetManifestResourceStream("Table.Sample.xlsx");

ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = await application.Workbooks.OpenAsync(inputStream, ExcelOpenType.Automatic);

IWorksheet worksheet = workbook.Worksheets[0];

//Creating a table
IListObject table = worksheet.ListObjects.Create("Table1", worksheet["A1:C8"]);

//Inserting a column in the table
worksheet.InsertColumn(2, 2);

//Removing a column from the table
worksheet.DeleteColumn(2, 1);

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();

savePicker.SuggestedStartLocation = PickerLocationId.Desktop;

savePicker.SuggestedFileName = "Output";

savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await workbook.SaveAsAsync(storageFile);

inputStream.Dispose();

workbook.Close();

excelEngine.Dispose();
{% endhighlight %}

{% highlight .netcore %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);

IWorkbook workbook = application.Workbooks.Open(fileStream, ExcelOpenType.Automatic);

IWorksheet worksheet = workbook.Worksheets[0];

//Creating a table
IListObject table = worksheet.ListObjects.Create("Table1", worksheet["A1:C8"]);

//Inserting a column in the table
worksheet.InsertColumn(2, 2);

//Removing a column from the table
worksheet.DeleteColumn(2, 1);

string fileName = "Output.xlsx";

//Saving the workbook as stream
FileStream stream = new FileStream(fileName, FileMode.Create, FileAccess.ReadWrite);

workbook.SaveAs(stream);

stream.Dispose();

workbook.Close();

excelEngine.Dispose();
{% endhighlight %}

{% highlight Xamarin %}
//Gets assembly
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
           
//Gets input Excel document from embedded resource collection
Stream inputStream = assembly.GetManifestResourceStream("Table.Sample.xlsx");

ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelOpenType.Automatic);

IWorksheet worksheet = workbook.Worksheets[0];

//Creating a table
IListObject table = worksheet.ListObjects.Create("Table1", worksheet["A1:C8"]);

//Inserting a column in the table
worksheet.InsertColumn(2, 2);

//Removing a column from the table
worksheet.DeleteColumn(2, 1);

string fileName = "Output.xlsx";

//Saving the workbook as stream
MemoryStream outputStream = new MemoryStream();

workbook.SaveAs(outputStream);

workbook.Close();

excelEngine.Dispose();

//Save the Excel file
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    await DependencyService.Get<ISaveWindowsPhone>().Save(fileName, "application/msexcel", outputStream);
else
    DependencyService.Get<ISave>().Save(fileName, "application/msexcel", outputStream);

//Dispose the input and output stream instances
inputStream.Dispose();

outputStream.Dispose();
{% endhighlight %}
{% endtabs %}  

N> Inserting rows/columns in a worksheet within table range also modifies table structure.

## Adding a Total Row

The "Total Row" is added to a table by accessing the **Table** **Columns**. It is possible to set calculation function to be used to the Total Row cells, by using the ExcelTotalsCalculation enumerator. To know more about this enumerator, please refer **ExcelTotalsCalculation** in API section. These cells will be updated once they are calculated.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

IWorksheet worksheet = workbook.Worksheets[0];

//Creating a table
IListObject table = worksheet.ListObjects.Create("Table1", worksheet ["A1:C8"]);

//Adding Total Row
table.ShowTotals = true;

table.Columns[0].TotalsRowLabel = "Total";

table.Columns[1].TotalsCalculation = ExcelTotalsCalculation.Sum;

table.Columns[2].TotalsCalculation = ExcelTotalsCalculation.Sum;

string fileName = "Output.xlsx";

workbook.SaveAs(fileName);

workbook.Close();

excelEngine.Dispose();         



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

Dim worksheet As IWorksheet = workbook.Worksheets(0)

'Creating a table
Dim table As IListObject = worksheet.ListObjects.Create("Table1", worksheet ("A1:C8"))

'Adding Total Row
table.ShowTotals = True

table.Columns(0).TotalsRowLabel = "Total"

table.Columns(1).TotalsCalculation = ExcelTotalsCalculation.Sum

table.Columns(2).TotalsCalculation = ExcelTotalsCalculation.Sum

Dim fileName As String = "Output.xlsx"

workbook.SaveAs(fileName)

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

{% highlight UWP %}
//Gets assembly
Assembly assembly = typeof(App).GetTypeInfo().Assembly;

//Gets input Excel document from embedded resource collection
Stream inputStream = assembly.GetManifestResourceStream("Table.Sample.xlsx");

ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = await application.Workbooks.OpenAsync(inputStream,ExcelOpenType.Automatic);

IWorksheet worksheet = workbook.Worksheets[0];

//Creating a table
IListObject table = worksheet.ListObjects.Create("Table1", worksheet["A1:C8"]);

//Adding Total Row
table.ShowTotals = true;

table.Columns[0].TotalsRowLabel = "Total";

table.Columns[1].TotalsCalculation = ExcelTotalsCalculation.Sum;

table.Columns[2].TotalsCalculation = ExcelTotalsCalculation.Sum;

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();

savePicker.SuggestedStartLocation = PickerLocationId.Desktop;

savePicker.SuggestedFileName = "Output";

savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await workbook.SaveAsAsync(storageFile);

inputStream.Dispose();

workbook.Close();

excelEngine.Dispose();
{% endhighlight %}

{% highlight .netcore %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);

IWorkbook workbook = application.Workbooks.Open(fileStream,ExcelOpenType.Automatic);

IWorksheet worksheet = workbook.Worksheets[0];

//Creating a table
IListObject table = worksheet.ListObjects.Create("Table1", worksheet["A1:C8"]);

//Adding Total Row
table.ShowTotals = true;

table.Columns[0].TotalsRowLabel = "Total";

table.Columns[1].TotalsCalculation = ExcelTotalsCalculation.Sum;

table.Columns[2].TotalsCalculation = ExcelTotalsCalculation.Sum;

string fileName = "Output.xlsx";

//Saving the workbook as stream
FileStream stream = new FileStream(fileName, FileMode.Create, FileAccess.ReadWrite);

workbook.SaveAs(stream);

stream.Dispose();

workbook.Close();

excelEngine.Dispose();
{% endhighlight %}

{% highlight Xamarin %}
//Gets assembly
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
           
//Gets input Excel document from embedded resource collection
Stream inputStream = assembly.GetManifestResourceStream("Table.Sample.xlsx");

ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open(inputStream,ExcelOpenType.Automatic);

IWorksheet worksheet = workbook.Worksheets[0];

//Creating a table
IListObject table = worksheet.ListObjects.Create("Table1", worksheet["A1:C8"]);

//Adding Total Row
table.ShowTotals = true;

table.Columns[0].TotalsRowLabel = "Total";

table.Columns[1].TotalsCalculation = ExcelTotalsCalculation.Sum;

table.Columns[2].TotalsCalculation = ExcelTotalsCalculation.Sum;

string fileName = "Output.xlsx";

//Saving the workbook as stream
MemoryStream outputStream = new MemoryStream();

workbook.SaveAs(outputStream);

workbook.Close();

excelEngine.Dispose();

//Save the Excel file
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    await DependencyService.Get<ISaveWindowsPhone>().Save(fileName, "application/msexcel", outputStream);
else
    DependencyService.Get<ISave>().Save(fileName, "application/msexcel", outputStream);

//Dispose the input and output stream instances
inputStream.Dispose();

outputStream.Dispose();
{% endhighlight %}
{% endtabs %}  

## Create a Table from External Connection 

External connection support allows to work with most recent data right in the workbook. Once the data is imported, only refresh operations are performed thereafter to retrieve the updated data.

The following table shows different data sources and its connection string formats which are supported in XlsIO.

<table>
<thead>
<tr>
<th>Database<br/><br/>
<th>Connection Type<br/><br/></th>
<th>Sample connection string<br/><br/></th></tr></thead>
<tr>
<td rowspan ="2"> <span style="font-weight:bold">
Microsoft Access<br/><br/></td>
<td>
OLEDB<br/><br/></td><td>
OLEDB;Provider=Microsoft.JET.OLEDB.4.0;Password=\"\";<br/><br/>User ID=Admin;Data Source=C:\\Company\\DB\\TestDB.mdb<br/><br/></td></tr>
<tr>
<td>
ODBC<br/><br/></td><td>
ODBC;DSN=MS Access;DBQ=C:\\Company\\DB\\Testing.mdb;<br/><br/>DefaultDir=C:\\Company\\DB;FIL=MS Access;MaxBufferSize=2048;PageTimeout=5;<br/><br/></td></tr>
<tr>
<td rowspan="2"> <span style="font-weight:bold">
SQL<br/><br/></td>
<td>
OLEDB<br/><br/></td>
<td>
OLEDB;Provider=SQLOLEDB.1;Integrated Security=SSPI;<br/><br/>Persist Security Info=True;Initial Catalog=Temp;<br/><br/>Data Source=SYNCFUSION\\SQLEXPRESS;Workstation ID=SYNCINC;<br/><br/></td></tr>
<tr>
<td>
ODBC<br/><br/></td>
<td>
ODBC;DSN=Test1;UID=syncfusion;Trusted_Connection=Yes;<br/><br/>APP=Microsoft Office <br/><br/>2010;WSID=SYNCINC;DATABASE=Temp<br/><br/></td></tr>
<tr>
<td><span style="font-weight:bold">
Excel<br/><br/></td><td>
OLEDB<br/><br/></td><td>
OLEDB;Provider=Microsoft.ACE.OLEDB.12.0;Password=\"\";<br/><br/>User ID=Admin;Data Source="c:\SourceTemplate.xlsx;<br/><br/>Jet OLEDB:Engine Type=37;<br/><br/></td></tr>
<tr>
<td rowspan = "2"> <span style="font-weight:bold">
SharePoint<br/><br/></td>
<td>
OLEDB<br/><br/></td>
<td>
Stars with OLEDB<br/><br/></td></tr>
<tr>
<td>
ODBC<br/><br/></td><td>
Stars with ODBC<br/><br/></td></tr>
</table>

The following code snippet explains the method of importing data through an external connection in the workbook.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet worksheet = workbook.Worksheets[0];

// Database path
string dataPath = Path.GetFullPath(@"c:\company\DB\TestDB.mdb");

// Connection string for DataSource
string ConnectionString = "OLEDB;Provider=Microsoft.JET.OLEDB.4.0;Password=\"\";User ID=Admin;Data Source=" + dataPath;

// Adding a connection to the workbook
IConnection Connection = workbook.Connections.Add("Connection1", "Sample connection with MsAccess", ConnectionString, "", ExcelCommandType.Sql);

// Adding a QueryTable to sheet object
worksheet.ListObjects.AddEx(ExcelListObjectSourceType.SrcQuery, Connection,  worksheet.Range["A1"]);

// Command Text for the Connection
worksheet.ListObjects[0].QueryTable.CommandText = "Select * from tableTest";

// The Query performs Asynchronous action
worksheet.ListObjects[0].QueryTable.BackgroundQuery = true;

// The Query Table is refreshed when the Workbook is opened
worksheet.ListObjects[0].QueryTable.RefreshOnFileOpen = true;

// Represents the connection description
Connection.Description = "Sample Connection";

// Import data to the sheet from the database
worksheet.ListObjects[0].Refresh();

// Auto-fits the columns
worksheet.UsedRange.AutofitColumns();

string fileName = "Output.xlsx";

workbook.SaveAs(fileName);

workbook.Close();

excelEngine.Dispose();         



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim worksheet As IWorksheet = workbook.Worksheets(0)

' Database path
Dim dataPath As String = Path.GetFullPath("c:\company\DB\TestDB.mdb")

' Connection string for DataSource
Dim ConnectionString As String ="OLEDB;Provider=Microsoft.JET.OLEDB.4.0;Password="""";User ID=Admin;Data Source=" + dataPath

' Adding a connection to the workbook 
Dim Connection As IConnection = workbook.Connections.Add("Connection1", "Sample   connection with MsAccess", ConnectionString, "", ExcelCommandType.Sql)

' Adding a QueryTable to sheet object
worksheet.ListObjects.AddEx(ExcelListObjectSourceType.SrcQuery, Connection, worksheet.Range("A1"))

' Command Text for the Connection
worksheet.ListObjects(0).QueryTable.CommandText = "Select * from tableTest"

' The Query performs Asynchronous action
worksheet.ListObjects(0).QueryTable.BackgroundQuery = True

' The Query Table is refreshed when the Workbook is opened
worksheet.ListObjects(0).QueryTable.RefreshOnFileOpen = True

' Represents the connection description
Connection.Description = "Sample Connection"

' Import data to the sheet from the database
worksheet.ListObjects(0).Refresh()

' Auto-fits the columns
worksheet.UsedRange.AutofitColumns()

Dim fileName As String = "Output.xlsx"

workbook.SaveAs(fileName)

workbook.Close()

excelEngine.Dispose()


{% endhighlight %}
{% highlight UWP %}
N> XlsIO supports creation of table from external connection in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms alone.
{% endhighlight %}
{% highlight .netcore %}
N> XlsIO supports creation of table from external connection in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms alone.
{% endhighlight %}
{% highlight Xamarin %}
N> XlsIO supports creation of table from external connection in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms alone.
{% endhighlight %}
{% endtabs %}  

