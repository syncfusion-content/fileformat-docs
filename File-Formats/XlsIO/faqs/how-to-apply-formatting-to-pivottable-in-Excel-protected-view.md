---
title: How to apply formatting to pivot table | XlsIO | Syncfusion
description: This page explains how to apply formatting to pivot table in Excel protected view using Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# How to apply formatting to pivot table in Excel protected view?

Syncfusion XlsIO supports applying formatting to pivot table during creation. But, in the protected view, to get the formatting applied to pivot table, [Layout](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IPivotTable.html#Syncfusion_XlsIO_IPivotTable_Layout) method of [IPivotTable](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IPivotTable.html) should be called. The following code snippet explains this.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = excelEngine.Excel.Workbooks.Open("Sample.xlsx");
  IWorksheet worksheet = workbook.Worksheets[0];
  IWorksheet pivotSheet = workbook.Worksheets[1];

  //Create Pivot cache with the given data range
  IPivotCache cache = workbook.PivotCaches.Add(worksheet["A1:H50"]);

  //Create "PivotTable1" with the cache at the specified range
  IPivotTable pivotTable = pivotSheet.PivotTables.Add("PivotTable1", pivotSheet["A1"], cache);

  //Add Pivot table fields (Row and Column fields)
  pivotTable.Fields[2].Axis = PivotAxisTypes.Row;
  pivotTable.Fields[6].Axis = PivotAxisTypes.Row;
  pivotTable.Fields[3].Axis = PivotAxisTypes.Column;

  //Add data field
  IPivotField field = pivotTable.Fields[5];
  pivotTable.DataFields.Add(field, "Sum", PivotSubtotalTypes.Sum);

  //Set BuiltInStyle
  pivotTable.BuiltInStyle = PivotBuiltInStyles.PivotStyleDark15;
  pivotTable.Layout();
  workbook.SaveAs("Output.xlsx");             
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx	
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
  Dim worksheet As IWorksheet = workbook.Worksheets(0)
  Dim pivotSheet As IWorksheet = workbook.Worksheets(1)

  'Create Pivot cache with the given data range
  Dim cache As IPivotCache = workbook.PivotCaches.Add(worksheet("A1:H50"))

  'Create "PivotTable1" with the cache at the specified range
  Dim pivotTable As IPivotTable = pivotSheet.PivotTables.Add("PivotTable1", pivotSheet("A1"), cache)

  'Add Pivot table fields (Row and Column fields)
  pivotTable.Fields(2).Axis = PivotAxisTypes.Row
  pivotTable.Fields(6).Axis = PivotAxisTypes.Row
  pivotTable.Fields(3).Axis = PivotAxisTypes.Column

  'Add data field
  Dim field As IPivotField = pivotTable.Fields(5)
  pivotTable.DataFields.Add(field, "Sum", PivotSubtotalTypes.Sum)

  'Set BuiltInStyle
  pivotTable.BuiltInStyle = PivotBuiltInStyles.PivotStyleDark15
  pivotTable.Layout()
  workbook.SaveAs("PivotTable.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;

  //Instantiates the file picker
  FileOpenPicker openPicker = new FileOpenPicker();
  openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
  openPicker.FileTypeFilter.Add(".xlsx");
  openPicker.FileTypeFilter.Add(".xls");
  StorageFile file = await openPicker.PickSingleFileAsync();

  //Opens the workbook
  IWorkbook workbook = await application.Workbooks.OpenAsync(file);
  IWorksheet worksheet = workbook.Worksheets[0];
  IWorksheet pivotSheet = workbook.Worksheets[1];

  //Create Pivot cache with the given data range
  IPivotCache cache = workbook.PivotCaches.Add(worksheet["A1:H50"]);

  //Create "PivotTable1" with the cache at the specified range
  IPivotTable pivotTable = pivotSheet.PivotTables.Add("PivotTable1", pivotSheet["A1"], cache);

  //Add Pivot table fields (Row and Column fields)
  pivotTable.Fields[2].Axis = PivotAxisTypes.Row;
  pivotTable.Fields[6].Axis = PivotAxisTypes.Row;    
  pivotTable.Fields[3].Axis = PivotAxisTypes.Column;

  //Add data field
  IPivotField field = pivotTable.Fields[5];
  pivotTable.DataFields.Add(field, "Sum", PivotSubtotalTypes.Sum);

  //Set BuiltInStyle
  pivotTable.BuiltInStyle = PivotBuiltInStyles.PivotStyleDark15;
  pivotTable.Layout();

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

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];
  IWorksheet pivotSheet = workbook.Worksheets[1];

  //Create Pivot cache with the given data range
  IPivotCache cache = workbook.PivotCaches.Add(worksheet["A1:H50"]);

  //Create "PivotTable1" with the cache at the specified range
  IPivotTable pivotTable = pivotSheet.PivotTables.Add("PivotTable1", pivotSheet["A1"], cache);

  //Add Pivot table fields (Row and Column fields)
  pivotTable.Fields[2].Axis = PivotAxisTypes.Row;
  pivotTable.Fields[6].Axis = PivotAxisTypes.Row;
  pivotTable.Fields[3].Axis = PivotAxisTypes.Column;

  //Add data field
  IPivotField field = pivotTable.Fields[5];
  pivotTable.DataFields.Add(field, "Sum", PivotSubtotalTypes.Sum);

  //Set BuiltInStyle
  pivotTable.BuiltInStyle = PivotBuiltInStyles.PivotStyleDark15;
  pivotTable.Layout();

  //Saving the workbook as stream
  FileStream stream = new FileStream("Output.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;

  //"App" is the class of Portable project.
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream fileStream = assembly.GetManifestResourceStream("GettingStarted.Sample.xlsx");

  //Opens the workbook 
  IWorkbook workbook = excelEngine.Excel.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];
  IWorksheet pivotSheet = workbook.Worksheets[1];

  //Create Pivot cache with the given data range
  IPivotCache cache = workbook.PivotCaches.Add(worksheet["A1:H50"]);

  //Create "PivotTable1" with the cache at the specified range
  IPivotTable pivotTable = pivotSheet.PivotTables.Add("PivotTable1", pivotSheet["A1"], cache);

  //Add Pivot table fields (Row and Column fields)
  pivotTable.Fields[2].Axis = PivotAxisTypes.Row;
  pivotTable.Fields[6].Axis = PivotAxisTypes.Row;
  pivotTable.Fields[3].Axis = PivotAxisTypes.Column;

  //Add data field
  IPivotField field = pivotTable.Fields[5];
  pivotTable.DataFields.Add(field, "Sum", PivotSubtotalTypes.Sum);

  //Set BuiltInStyle
  pivotTable.BuiltInStyle = PivotBuiltInStyles.PivotStyleDark15;
  pivotTable.Layout();

  //Save the workbook to stream in xlsx format. 
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);
  workbook.Close();

  //Save the stream as a file in the device and invoke it for viewing
  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", stream);
}
{% endhighlight %}
{% endtabs %}
