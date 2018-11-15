---
title: Working with Tables
description: Briefs about tables
platform: File-formats
control: XlsIO
documentation: UG
---
# Working with Tables

## Creating a table

XlsIO supports reading and writing the table which helps to organize and analyze the related data. 

* **IListObjects** represents a collection of tables in the worksheet. 
* **IListObject** represent a table in the worksheet.

You can also create a calculated column in the table. For more details, refer [here](/file-formats/xlsio/working-with-formulas#calculated-column).

N> In XlsIO, tables are supported only for Excel 2007 and later formats (*.xlsx files).

The following code sample explains the creation of a simple table by the range of data from an existing worksheet.

{% tabs %}
{% highlight c# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Create table with the data in given range
  IListObject table = worksheet.ListObjects.Create("Table1", worksheet["A1:C8"]);

  string fileName = "Output.xlsx";
  workbook.SaveAs(fileName);
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Create table with the data in given range
  Dim table As IListObject = worksheet.ListObjects.Create("Table1", worksheet("A1:C8"))

  Dim fileName As String = "Output.xlsx"
  workbook.SaveAs(fileName)
End Using
{% endhighlight %}

{% highlight UWP %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from an embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Table.Sample.xlsx");

  IWorkbook workbook = await application.Workbooks.OpenAsync(inputStream, ExcelOpenType.Automatic);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Create table with the data in given range
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
}
{% endhighlight %}

{% highlight asp.net core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream, ExcelOpenType.Automatic);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Create table with the data in given range
  IListObject table = worksheet.ListObjects.Create("Table1", worksheet["A1:C8"]);

  string fileName = "Output.xlsx";

  //Saving the workbook as stream
  FileStream stream = new FileStream(fileName, FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from an embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Table.Sample.xlsx");

  IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelOpenType.Automatic);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Create table with the data in given range
  IListObject table = worksheet.ListObjects.Create("Table1", worksheet["A1:C8"]);

  //Saving the workbook as stream
  MemoryStream outputStream = new MemoryStream();
  workbook.SaveAs(outputStream);

  string fileName = "Output.xlsx";

  outputStream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies among Windows Phone, Android, and iOS platforms. Refer to the xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
  	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView(fileName, "application/msexcel", outputStream);
  }
  else
  {
  	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView(fileName, "application/msexcel", outputStream);
  }
}
{% endhighlight %}
{% endtabs %}

## Accessing a table

The existing tables in the worksheet can be accessed, as follows. 

{% tabs %}
{% highlight c# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
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
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
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
End Using
{% endhighlight %}

{% highlight UWP %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from an embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Table.Sample.xlsx");

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

  //Creates a storage file from the FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight asp.net core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
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
}
{% endhighlight %}

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from an embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Table.Sample.xlsx");

  IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelOpenType.Automatic);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Accessing first table in the sheet
  IListObject table = worksheet.ListObjects[0];

  //Modifying table name
  table.Name = "SalesTable";

  //Saving the workbook as stream
  MemoryStream outputStream = new MemoryStream();
  workbook.SaveAs(outputStream);

  string fileName = "Output.xlsx";

  outputStream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies among Windows Phone, Android, and iOS platforms. Refer to the xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
  	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView(fileName, "application/msexcel", outputStream);
  }
  else
  {
  	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView(fileName, "application/msexcel", outputStream);
  }
}
{% endhighlight %}
{% endtabs %}  

## Formatting a table

You can apply built-in styles to the table using XlsIO. You can also customize the table with other table style options such as Header/total row, first/last column, and banded rows to make a table easier to read.

The following code snippet illustrates how to apply built-in table style.

{% tabs %}  

{% highlight c# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Creating a table
  IListObject table = worksheet.ListObjects.Create("Table1", worksheet["A1:C8"]);

  //Formatting table with a built-in style
  table.BuiltInTableStyle = TableBuiltInStyles.TableStyleMedium9;

  string fileName = "Output.xlsx";
  workbook.SaveAs(fileName);
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Creating a table
  Dim table As IListObject = worksheet.ListObjects.Create("Table1", worksheet("A1:C8"))

  'Formatting table with a built-in style
  table.BuiltInTableStyle = TableBuiltInStyles.TableStyleMedium9

  Dim fileName As String = "Output.xlsx"
  workbook.SaveAs(fileName)
End Using
{% endhighlight %}

{% highlight UWP %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Table.Sample.xlsx");

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
}
{% endhighlight %}

{% highlight asp.net core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
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
}
{% endhighlight %}

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Table.Sample.xlsx");

  IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelOpenType.Automatic);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Creating a table
  IListObject table = worksheet.ListObjects.Create("Table1", worksheet["A1:C8"]);

  //Formatting table with a built-in style
  table.BuiltInTableStyle = TableBuiltInStyles.TableStyleMedium9;

  //Saving the workbook as stream
  MemoryStream outputStream = new MemoryStream();
  workbook.SaveAs(outputStream);

  string fileName = "Output.xlsx";

  outputStream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies among Windows Phone, Android, and iOS platforms. Refer to the xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
  	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView(fileName, "application/msexcel", outputStream);
  }
  else
  {
  	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView(fileName, "application/msexcel", outputStream);
  }
}
{% endhighlight %}
{% endtabs %}  

## Insert or remove columns in a table

IListObject is a collection of columns, whereas a single column is represented by an instance of **IListObjectColumn**. XlsIO supports to insert or remove columns from the table using worksheet, as follows.

{% tabs %}
{% highlight c# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Creating a table
  IListObject table = worksheet.ListObjects.Create("Table1", worksheet["A1:C8"]);

  //Inserting a column in the table
  worksheet.InsertColumn(2, 2);

  // Removing a column from the table
  worksheet.DeleteColumn(2, 1);

  string fileName = "Output.xlsx";
  workbook.SaveAs(fileName);
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Creating table
  Dim table As IListObject = worksheet.ListObjects.Create("Table1", worksheet("A1:C8"))

  'Inserting a column in the table
  worksheet.InsertColumn(2, 2)

  'Removing a column from the table
  worksheet.DeleteColumn(2, 1)

  Dim fileName As String = "Output.xlsx"
  workbook.SaveAs(fileName)
End Using
{% endhighlight %}

{% highlight UWP %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from an embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Table.Sample.xlsx");

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

  //Creates a storage file from the FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight asp.net core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
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
}
{% endhighlight %}

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from an embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Table.Sample.xlsx");

  IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelOpenType.Automatic);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Creating a table
  IListObject table = worksheet.ListObjects.Create("Table1", worksheet["A1:C8"]);

  //Inserting a column in the table
  worksheet.InsertColumn(2, 2);

  //Removing a column from the table
  worksheet.DeleteColumn(2, 1);

  //Saving the workbook as stream
  MemoryStream outputStream = new MemoryStream();
  workbook.SaveAs(outputStream);

  string fileName = "Output.xlsx";

  outputStream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies among Windows Phone, Android, and iOS platforms. Refer to the xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
  	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView(fileName, "application/msexcel", outputStream);
  }
  else
  {
  	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView(fileName, "application/msexcel", outputStream);
  }
}
{% endhighlight %}
{% endtabs %}  

N> Inserting rows or columns in a worksheet within the table range modifies table structure.

## Adding a total row

The "Total Row" is added to a table by accessing the **Table** **Columns**. It is possible to set calculation function to be used to the total row cells by using the ExcelTotalsCalculation enumerator. To learn more about this enumerator, refer to the **ExcelTotalsCalculation** in API section. These cells are updated after they are calculated.

{% tabs %}  

{% highlight c# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Creating a table
  IListObject table = worksheet.ListObjects.Create("Table1", worksheet["A1:C8"]);

  //Adding total row
  table.ShowTotals = true;
  table.Columns[0].TotalsRowLabel = "Total";
  table.Columns[1].TotalsCalculation = ExcelTotalsCalculation.Sum;
  table.Columns[2].TotalsCalculation = ExcelTotalsCalculation.Sum;

  string fileName = "Output.xlsx";
  workbook.SaveAs(fileName);
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Creating a table
  Dim table As IListObject = worksheet.ListObjects.Create("Table1", worksheet("A1:C8"))

  'Adding total row
  table.ShowTotals = True
  table.Columns(0).TotalsRowLabel = "Total"
  table.Columns(1).TotalsCalculation = ExcelTotalsCalculation.Sum
  table.Columns(2).TotalsCalculation = ExcelTotalsCalculation.Sum

  Dim fileName As String = "Output.xlsx"
  workbook.SaveAs(fileName)
End Using
{% endhighlight %}

{% highlight UWP %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Table.Sample.xlsx");

  IWorkbook workbook = await application.Workbooks.OpenAsync(inputStream, ExcelOpenType.Automatic);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Creating a table
  IListObject table = worksheet.ListObjects.Create("Table1", worksheet["A1:C8"]);

  //Adding total row
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
}
{% endhighlight %}

{% highlight asp.net core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream, ExcelOpenType.Automatic);
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
}
{% endhighlight %}

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Table.Sample.xlsx");

  IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelOpenType.Automatic);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Creating a table
  IListObject table = worksheet.ListObjects.Create("Table1", worksheet["A1:C8"]);

  //Adding total row
  table.ShowTotals = true;
  table.Columns[0].TotalsRowLabel = "Total";
  table.Columns[1].TotalsCalculation = ExcelTotalsCalculation.Sum;
  table.Columns[2].TotalsCalculation = ExcelTotalsCalculation.Sum;

  //Saving the workbook as stream
  MemoryStream outputStream = new MemoryStream();
  workbook.SaveAs(outputStream);

  string fileName = "Output.xlsx";

  outputStream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies among Windows Phone, Android, and iOS platforms. Refer to the xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
  	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView(fileName, "application/msexcel", outputStream);
  }
  else
  {
  	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView(fileName, "application/msexcel", outputStream);
  }
}
{% endhighlight %}
{% endtabs %}  

## Create a table from external connection 

External connection support allows to work with most recent data right in the workbook. After the data is imported, only refresh operations are performed to retrieve the updated data.

The following code snippet explains the method of importing data through an external connection in the workbook.

{% tabs %}
{% highlight c# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Database path
  string dataPath = Path.GetFullPath(@"c:\company\DB\TestDB.mdb");

  //Connection string for DataSource
  string ConnectionString = "OLEDB;Provider=Microsoft.JET.OLEDB.4.0;Password=\"\";User ID=Admin;Data Source=" + dataPath;

  //Adding a connection to the workbook
  IConnection Connection = workbook.Connections.Add("Connection1", "Sample connection with MsAccess", ConnectionString, "", ExcelCommandType.Sql);

  //Adding a QueryTable to sheet object
  worksheet.ListObjects.AddEx(ExcelListObjectSourceType.SrcQuery, Connection, worksheet.Range["A1"]);

  //Command text for the connection
  worksheet.ListObjects[0].QueryTable.CommandText = "Select * from tableTest";

  //The query performs asynchronous action
  worksheet.ListObjects[0].QueryTable.BackgroundQuery = true;

  //The query table is refreshed when the workbook is opened
  worksheet.ListObjects[0].QueryTable.RefreshOnFileOpen = true;

  //Represents the connection description
  Connection.Description = "Sample Connection";

  //Import data to the sheet from the database
  worksheet.ListObjects[0].Refresh();

  //Auto-fits the columns
  worksheet.UsedRange.AutofitColumns();

  string fileName = "Output.xlsx";
  workbook.SaveAs(fileName);
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Database path
  Dim dataPath As String = Path.GetFullPath("c:\company\DB\TestDB.mdb")

  'Connection string for DataSource
  Dim ConnectionString As String = "OLEDB;Provider=Microsoft.JET.OLEDB.4.0;Password="""";User ID=Admin;Data Source=" + dataPath

  'Adding a connection to the workbook 
  Dim Connection As IConnection = workbook.Connections.Add("Connection1", "Sample   connection with MsAccess", ConnectionString, "", ExcelCommandType.Sql)

  'Adding a QueryTable to sheet object
  worksheet.ListObjects.AddEx(ExcelListObjectSourceType.SrcQuery, Connection, worksheet.Range("A1"))

  'Command text for the connection
  worksheet.ListObjects(0).QueryTable.CommandText = "Select * from tableTest"

  'The query performs asynchronous action
  worksheet.ListObjects(0).QueryTable.BackgroundQuery = True

  'The QueryTable is refreshed when the workbook is opened
  worksheet.ListObjects(0).QueryTable.RefreshOnFileOpen = True

  'Represents the connection description
  Connection.Description = "Sample Connection"

  'Import data to the sheet from the database
  worksheet.ListObjects(0).Refresh()

  'Auto-fits the columns
  worksheet.UsedRange.AutofitColumns()

  Dim fileName As String = "Output.xlsx"
  workbook.SaveAs(fileName)
End Using
{% endhighlight %}

{% highlight UWP %}
//XlsIO supports creation of table from external connection in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms.
{% endhighlight %}

{% highlight asp.net core %}
//XlsIO supports creation of table from external connection in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms.
{% endhighlight %}

{% highlight Xamarin %}
//XlsIO supports creation of table from external connection in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms.
{% endhighlight %}
{% endtabs %}

The following table shows different data sources and its connection string formats supported in XlsIO.

<table>
<tr>
<th>Database<br/><br/></th>
<th>Connection Type<br/><br/></th>
<th>Sample connection string<br/><br/></th></tr>
<tr>
<td rowspan ="2"> <span style="font-weight:bold">
Microsoft Access<br/><br/></span></td>
<td>
OLEDB<br/><br/></td><td>
OLEDB;Provider=Microsoft.JET.OLEDB.4.0;Password=\"\";<br/><br/>User ID=Admin;Data Source=C:\\Company\\DB\\TestDB.mdb<br/><br/></td></tr>
<tr>
<td>
ODBC<br/><br/></td><td>
ODBC;DSN=MS Access;DBQ=C:\\Company\\DB\\Testing.mdb;<br/><br/>DefaultDir=C:\\Company\\DB;FIL=MS Access;MaxBufferSize=2048;PageTimeout=5;<br/><br/></td></tr>
<tr>
<td rowspan="2"> <span style="font-weight:bold">
SQL<br/><br/></span></td>
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
Excel<br/><br/></span></td><td>
OLEDB<br/><br/></td><td>
OLEDB;Provider=Microsoft.ACE.OLEDB.12.0;Password=\"\";<br/><br/>User ID=Admin;Data Source="c:\SourceTemplate.xlsx;<br/><br/>Jet OLEDB:Engine Type=37;<br/><br/></td></tr>
<tr>
<td rowspan = "2"> <span style="font-weight:bold">
SharePoint<br/><br/></span></td>
<td>
OLEDB<br/><br/></td>
<td>
Stars with OLEDB<br/><br/></td></tr>
<tr>
<td>
ODBC<br/><br/></td><td>
Stars with ODBC<br/><br/></td></tr>
</table>