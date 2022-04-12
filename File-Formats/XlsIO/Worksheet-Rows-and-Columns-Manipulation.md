---
title: Worksheet Rows and Columns Manipulation | Syncfusion
description: Briefs about Row & Column manipulations in XlsIO. It provides manipulation options equivalent to Excel such as insertion, deletion, hiding and more.
platform: File-formats
control: XlsIO
documentation: UG
---

# Worksheet Rows and Columns Manipulation

The Essential XlsIO provides rows and columns manipulation options equivalent to Excel such as insertion, deletion, hiding, adjusting dimensions, grouping, sub-totaling and more through **IWorksheet** interface.

## Insert Rows and Columns 

The following code snippet illustrates how to insert rows and columns in a worksheet.


{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
  IWorksheet worksheet = workbook.Worksheets[0];

  //Insert a row
  worksheet.InsertRow(3, 1, ExcelInsertOptions.FormatAsBefore);
  //Inserting a column
  worksheet.InsertColumn(2, 1, ExcelInsertOptions.FormatAsAfter);

  workbook.SaveAs("Book1.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Inserting a row
  worksheet.InsertRow(3, 1, ExcelInsertOptions.FormatAsBefore)
  'Inserting a column
  worksheet.InsertColumn(2, 1, ExcelInsertOptions.FormatAsAfter)

  workbook.SaveAs("Book1.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
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

  //Insert a row
  worksheet.InsertRow(3, 1, ExcelInsertOptions.FormatAsBefore);
  //Inserting a column
  worksheet.InsertColumn(2, 1, ExcelInsertOptions.FormatAsAfter);

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Book1";
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
  application.DefaultVersion = ExcelVersion.Excel2013;
  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Insert a row
  worksheet.InsertRow(3, 1, ExcelInsertOptions.FormatAsBefore);
  //Inserting a column
  worksheet.InsertColumn(2, 1, ExcelInsertOptions.FormatAsAfter);

  //Saving the workbook as stream
  FileStream stream = new FileStream("Book1.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.XlsIO.Samples.Template.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Insert a row
  worksheet.InsertRow(3, 1, ExcelInsertOptions.FormatAsBefore);
  //Inserting a column
  worksheet.InsertColumn(2, 1, ExcelInsertOptions.FormatAsAfter);

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Book1.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Book1.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to insert rows and columns in an Excel worksheet in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Format%20rows%20and%20columns/Insert%20Rows%20and%20Columns).

N> Row and Column index of Insert methods are "one based".

To know more about insert rows and columns, refer to the **WorksheetImpl** in API section.

## Delete Rows and Columns 

The following code shows how to delete rows and columns.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
  IWorksheet worksheet = workbook.Worksheets[0];

  //Delete a row
  worksheet.DeleteRow(3);
  //Delete a column
  worksheet.DeleteColumn(2);

  workbook.SaveAs("Book1.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Delete a row
  worksheet.DeleteRow(3)
  'Delete a column
  worksheet.DeleteColumn(2)

  workbook.SaveAs("Book1.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
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

  //Delete a row
  worksheet.DeleteRow(3);
  //Delete a column
  worksheet.DeleteColumn(2);

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Book1";
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
  application.DefaultVersion = ExcelVersion.Excel2013;
  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Delete a row
  worksheet.DeleteRow(3);
  //Delete a column
  worksheet.DeleteColumn(2);

  //Saving the workbook as stream
  FileStream stream = new FileStream("Book1.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.XlsIO.Samples.Template.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Delete a row
  worksheet.DeleteRow(3);
  //Delete a column
  worksheet.DeleteColumn(2);

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.
  
  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Book1.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Book1.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to delete rows and columns in an Excel worksheet in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Format%20rows%20and%20columns/Delete%20Rows%20and%20Columns).

T>To extract values little faster or to delete a larger number of rows and columns, use Un-Safe code option of **IApplication** interface as follows

{% tabs %}  

{% highlight c# tabtitle="C#" %}
application.DataProviderType = ExcelDataProviderType.Unsafe;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
application.DataProviderType = ExcelDataProviderType.Unsafe
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
application.DataProviderType = ExcelDataProviderType.Unsafe;
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//XlsIO supports DataProviderType of IApplication in Windows Forms, WPF and UWP platforms alone.
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//XlsIO supports DataProviderType of IApplication in Windows Forms, WPF and UWP platforms alone.
{% endhighlight %}
{% endtabs %}  
  
### Move Rows and Columns 

In addition, cells can be deleted by shifting other cells in a row or column towards up/left by one step. This can be done by using the **Clear** method as shown in the following code.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
  IWorksheet worksheet = workbook.Worksheets[0];

  //Shifts cells towards Left after deletion
  worksheet.Range["A1:E1"].Clear(ExcelMoveDirection.MoveLeft);
  //Shifts cells toward Up after deletion
  worksheet.Range["A1:A6"].Clear(ExcelMoveDirection.MoveUp);

  workbook.SaveAs("Book1.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Shifts cells towards Left after deletion
  worksheet.Range("A1:E1").Clear(ExcelMoveDirection.MoveLeft)
  'Shifts cells towards Up after deletion
  worksheet.Range("A1:A6").Clear(ExcelMoveDirection.MoveUp)

  workbook.SaveAs("Book1.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
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

  //Shifts cells towards Left after deletion
  worksheet.Range["A1:E1"].Clear(ExcelMoveDirection.MoveLeft);
  //Shifts cells toward Up after deletion
  worksheet.Range["A1:A6"].Clear(ExcelMoveDirection.MoveUp);

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Book1";
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
  application.DefaultVersion = ExcelVersion.Excel2013;
  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Shifts cells towards Left after deletion
  worksheet.Range["A1:E1"].Clear(ExcelMoveDirection.MoveLeft);
  //Shifts cells toward Up after deletion
  worksheet.Range["A1:A6"].Clear(ExcelMoveDirection.MoveUp);

  //Saving the workbook as stream
  FileStream stream = new FileStream("Book1.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.XlsIO.Samples.Template.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Shifts cells towards Left after deletion
  worksheet.Range["A1:E1"].Clear(ExcelMoveDirection.MoveLeft);
  //Shifts cells toward Up after deletion
  worksheet.Range["A1:A6"].Clear(ExcelMoveDirection.MoveUp);

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.
  
  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Book1.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Book1.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to move rows and columns in an Excel worksheet in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Format%20rows%20and%20columns/Move%20Rows%20and%20Columns).

N> Deletion by using above method is more efficient than looping.
N> Row/Column index of these methods are "one based".

## Show or Hide Rows and Columns 

Visibility of rows and columns can be set by using the **ShowRow** and **ShowColumn** methods as shown as follows.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
  IWorksheet worksheet = workbook.Worksheets[0];

  //Hiding the first column and second row
  worksheet.ShowColumn(1, false);
  worksheet.ShowRow(2, false);

  workbook.SaveAs("Book1.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Hiding the first column and second row
  worksheet.ShowColumn(1, False)
  worksheet.ShowRow(2, False)

  workbook.SaveAs("Book1.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
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

  //Hiding the first column and second row
  worksheet.ShowColumn(1, false);
  worksheet.ShowRow(2, false);

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Book1";
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
  application.DefaultVersion = ExcelVersion.Excel2013;
  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Hiding the first column and second row
  worksheet.ShowColumn(1, false);
  worksheet.ShowRow(2, false);

  //Saving the workbook as stream
  FileStream stream = new FileStream("Book1.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.XlsIO.Samples.Template.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Hiding the first column and second row
  worksheet.ShowColumn(1, false);
  worksheet.ShowRow(2, false);

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Book1.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Book1.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to hide rows and columns in an Excel worksheet in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Format%20rows%20and%20columns/Hide%20Rows%20and%20Columns).

## Show or Hide Specific Range

The Essential XlsIO allows to set visibility for a specific range. The following code snippet shows how to set the visibility of a range.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];
  IRange range = worksheet[1, 4];

  //Hiding the range ‘D1’
  worksheet.ShowRange(range, false);
  IRange firstRange = worksheet[1, 1, 3, 3];
  IRange secondRange = worksheet[5, 5, 7, 7];
  RangesCollection rangeCollection = new RangesCollection(application, worksheet);
  rangeCollection.Add(firstRange);
  rangeCollection.Add(secondRange);

  //Hiding a collection of ranges
  worksheet.ShowRange(rangeCollection, false);

  workbook.SaveAs("Book1.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)
  Dim range As IRange = worksheet(1, 4)

  'Hiding the range ‘D1’
  worksheet.ShowRange(range, False)
  Dim firstRange As IRange = worksheet(1, 1, 3, 3)
  Dim secondRange As IRange = worksheet(5, 5, 7, 7)
  Dim rangeCollection As RangesCollection = New RangesCollection(application, worksheet)
  rangeCollection.Add(firstRange)
  rangeCollection.Add(secondRange)

  'Hiding a collection of ranges
  worksheet.ShowRange(rangeCollection, False)

  workbook.SaveAs("Book1.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
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

  //Hiding the first column and second row
  worksheet.ShowColumn(1, false);
  worksheet.ShowRow(2, false);

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Book1";
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
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];
  IRange range = worksheet[1, 4];

  //Hiding the range ‘D1’
  worksheet.ShowRange(range, false);
  IRange firstRange = worksheet[1, 1, 3, 3];
  IRange secondRange = worksheet[5, 5, 7, 7];
  RangesCollection rangeCollection = new RangesCollection(application, worksheet);
  rangeCollection.Add(firstRange);
  rangeCollection.Add(secondRange);

  //Hiding a collection of ranges
  worksheet.ShowRange(rangeCollection, false);

  //Saving the workbook as stream
  FileStream stream = new FileStream("Book1.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];
  IRange range = worksheet[1, 4];

  //Hiding the range ‘D1’
  worksheet.ShowRange(range, false);
  IRange firstRange = worksheet[1, 1, 3, 3];
  IRange secondRange = worksheet[5, 5, 7, 7];
  RangesCollection rangeCollection = new RangesCollection(application, worksheet);
  rangeCollection.Add(firstRange);
  rangeCollection.Add(secondRange);

  //Hiding a collection of ranges
  worksheet.ShowRange(rangeCollection, false);

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.
  
  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Book1.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Book1.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to hide specific range in an Excel worksheet in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Format%20rows%20and%20columns/Hide%20Range).

N> Resetting column width manually or through AutoFit, for the columns hidden using [ShowColumn](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorksheet.html#Syncfusion_XlsIO_IWorksheet_ShowColumn_System_Int32_System_Boolean_)/[HideColumn](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorksheet.html#Syncfusion_XlsIO_IWorksheet_HideColumn_System_Int32_) methods will make the hidden columns visible.
N> Resetting row height manually or through AutoFit,  for the rows hidden using [ShowRow](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorksheet.html#Syncfusion_XlsIO_IWorksheet_ShowRow_System_Int32_System_Boolean_) /[HideRow](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorksheet.html#Syncfusion_XlsIO_IWorksheet_HideRow_System_Int32_) methods will make the hidden rows visible.

## Adjust Row Height and Column Width 

Rows and columns can be [resized](https://support.office.com/en-ca/article/Change-the-column-width-and-row-height-72f5e3cc-994d-43e8-ae58-9774a0905f46) based on its contents. The XlsIO allows to resize rows and columns in the following ways:

* Resize a specific row or column
* Resize a range of rows or columns

### Resize a specific row or column

A single row or column can be resized by the **SetRowHeight** and **SetColumnWidth** methods of __IWorksheet__. Similarly, the height and width of a single row or column can be accessed using the **GetRowHeight** or **GetColumnWidth** methods of __IWorksheet__. 

The following code snippet shows how to resize a single row and column.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Modifying the row height
  worksheet.SetRowHeight(2, 25);
  //Modifying the column width
  worksheet.SetColumnWidth(1, 20);

  workbook.SaveAs("Book1.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Modifying the row height
  worksheet.SetRowHeight(2, 25)
  'Modifying the column width
  worksheet.SetColumnWidth(1, 20)

  workbook.SaveAs("Book1.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Modifying the row height
  worksheet.SetRowHeight(2, 25);
  //Modifying the column width
  worksheet.SetColumnWidth(1, 20);

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Book1";
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
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Modifying the row height
  worksheet.SetRowHeight(2, 25);
  //Modifying the column width
  worksheet.SetColumnWidth(1, 20);

  //Saving the workbook as stream
  FileStream stream = new FileStream("Book1.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Modifying the row height
  worksheet.SetRowHeight(2, 25);
  //Modifying the column width
  worksheet.SetColumnWidth(1, 20);

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Book1.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Book1.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

### Resize a range of rows or columns

Multiple rows or columns can be resized and accessed by using the **RowHeight** and **ColumnWidth** properties of __IRange__. The following code snippet shows how to resize multiple rows and columns.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Modifying the row height
  worksheet.Range["A2:A6"].RowHeight = 25;
  //Modifying the column width
  worksheet.Range["A1:D1"].ColumnWidth = 20;

  workbook.SaveAs("Book1.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Modifying the row height
  worksheet.Range("A2:A6").RowHeight = 25
  'Modifying the column width
  worksheet.Range("A1:D1").ColumnWidth = 20

  workbook.SaveAs("Book1.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Modifying the row height
  worksheet.Range["A2:A6"].RowHeight = 25;
  //Modifying the column width
  worksheet.Range["A1:D1"].ColumnWidth = 20;

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Book1";
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
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Modifying the row height
  worksheet.Range["A2:A6"].RowHeight = 25;
  //Modifying the column width
  worksheet.Range["A1:D1"].ColumnWidth = 20;

  //Saving the workbook as stream
  FileStream stream = new FileStream("Book1.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Modifying the row height
  worksheet.Range["A2:A6"].RowHeight = 25;
  //Modifying the column width
  worksheet.Range["A1:D1"].ColumnWidth = 20;

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Book1.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Book1.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to resize rows and columns in an Excel worksheet in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Format%20rows%20and%20columns/Resize%20Rows%20and%20Columns).

N> If a column width or a row height is 0, then the column or row is hidden.
N> Column width and row height can also be set in pixels, by using the IWorksheet.SetColumnWidthInPixel and IWorksheet.SetRowHeightInPixel methods respectively.

## Auto-Fit Rows and Columns

The XlsIO allows to auto-size the width and height of a cell to fit its content. This section demonstrates various methods to auto-fit rows and columns of a worksheet.

### Auto-Fit a Single Row or Column

The following code snippet shows how a row and a column is re-sized to its content.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  worksheet.Range["A1"].Text = "This is a long text";
  worksheet.Range["A1"].WrapText = true;

  //AutoFit applied to a single row
  worksheet.AutofitRow(1);
  worksheet.Range["A3"].Text = "This is a long text";

  //AutoFit applied to a single column
  worksheet.AutofitColumn(3);

  workbook.SaveAs("Book1.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  worksheet.Range("A1").Text = "This is a long text"
  worksheet.Range("A1").WrapText = True

  'AutoFit applied to a single row
  worksheet.AutofitRow(1)
  worksheet.Range("A3").Text = "This is a long text"

  'AutoFit applied to a single column
  worksheet.AutofitColumn(3)

  workbook.SaveAs("Book1.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  worksheet.Range["A1"].Text = "This is a long text";
  worksheet.Range["A1"].WrapText = true;

  //AutoFit applied to a single row
  worksheet.AutofitRow(1);
  worksheet.Range["A3"].Text = "This is a long text";

  //AutoFit applied to a single column
  worksheet.AutofitColumn(3);

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Book1";
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
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  worksheet.Range["A1"].Text = "This is a long text";
  worksheet.Range["A1"].WrapText = true;

  //AutoFit applied to a single row
  worksheet.AutofitRow(1);
  worksheet.Range["A3"].Text = "This is a long text";

  //AutoFit applied to a single column
  worksheet.AutofitColumn(3);

  //Saving the workbook as stream
  FileStream stream = new FileStream("Book1.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  worksheet.Range["A1"].Text = "This is a long text";
  worksheet.Range["A1"].WrapText = true;

  //AutoFit applied to a single row
  worksheet.AutofitRow(1);
  worksheet.Range["A3"].Text = "This is a long text";

  //AutoFit applied to a single column
  worksheet.AutofitColumn(3);

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Book1.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Book1.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

N> Row and Column indexes are "one based".

There is an alternative way to auto-fit row or column is by accessing the row or column, which is shown in the following code snippet.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
//AutoFit applied to first row
worksheet.Rows[0].AutofitRows();
//AutoFit applied to first column
worksheet.Columns[0].AutofitColumns();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'AutoFit applied to first row
worksheet.Rows(0).AutofitRows()
'AutoFit applied to first column
worksheet.Columns(0).AutofitColumns()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//AutoFit applied to first row
worksheet.Rows[0].AutofitRows();
//AutoFit applied to first column
worksheet.Columns[0].AutofitColumns();
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//AutoFit applied to first row
worksheet.Rows[0].AutofitRows();
//AutoFit applied to first column
worksheet.Columns[0].AutofitColumns();
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//AutoFit applied to first row
worksheet.Rows[0].AutofitRows();
//AutoFit applied to first column
worksheet.Columns[0].AutofitColumns();
{% endhighlight %}
{% endtabs %}  

N> Here column and row indexes are "zero based".

### Auto-Fit Multiple Rows or Columns

Multiple rows or columns can be auto fitted based on the range specified. This is depicted in the following code.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Assigning text to cells
  worksheet.Range["A1:D1"].Text = "This is the Long Text";
  worksheet.Range["A2:A5"].Text = "This is the Long Text using AutoFit Columns and Rows";
  worksheet.Range["A2:A5"].WrapText = true;

  //Auto-Fit the range
  worksheet.Range["A1:C1"].AutofitColumns();
  worksheet.Range["A2:A5"].AutofitRows();

  //Auto-fits all the columns used in the worksheet
  worksheet.UsedRange.AutofitColumns();

  workbook.SaveAs("Book1.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Assigning text to cells
  worksheet.Range("A1:D1").Text = "This is the Long Text"
  worksheet.Range("A2:A5").Text = "This is the Long Text using AutoFit Columns and Rows"
  worksheet.Range("A2:A5").WrapText = True

  'Auto-Fit the range
  worksheet.Range("A1:C1").AutofitColumns()
  worksheet.Range("A2:A5").AutofitRows()
  'Auto-fits all the columns used in the worksheet
  worksheet.UsedRange.AutofitColumns()

  workbook.SaveAs("Book1.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Assigning text to cells
  worksheet.Range["A1:D1"].Text = "This is the Long Text";
  worksheet.Range["A2:A5"].Text = "This is the Long Text using AutoFit Columns and Rows";
  worksheet.Range["A2:A5"].WrapText = true;

  //Auto-Fit the range
  worksheet.Range["A1:C1"].AutofitColumns();
  worksheet.Range["A2:A5"].AutofitRows();

  //Auto-fits all the columns used in the worksheet
  worksheet.UsedRange.AutofitColumns();

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Book1";
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
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Assigning text to cells
  worksheet.Range["A1:D1"].Text = "This is the Long Text";
  worksheet.Range["A2:A5"].Text = "This is the Long Text using AutoFit Columns and Rows";
  worksheet.Range["A2:A5"].WrapText = true;

  //Auto-Fit the range
  worksheet.Range["A1:C1"].AutofitColumns();
  worksheet.Range["A2:A5"].AutofitRows();

  //Auto-fits all the columns used in the worksheet
  worksheet.UsedRange.AutofitColumns();

  //Saving the workbook as stream
  FileStream stream = new FileStream("Book1.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Assigning text to cells
  worksheet.Range["A1:D1"].Text = "This is the Long Text";
  worksheet.Range["A2:A5"].Text = "This is the Long Text using AutoFit Columns and Rows";
  worksheet.Range["A2:A5"].WrapText = true;

  //Auto-Fit the range
  worksheet.Range["A1:C1"].AutofitColumns();
  worksheet.Range["A2:A5"].AutofitRows();

  //Auto-fits all the columns used in the worksheet
  worksheet.UsedRange.AutofitColumns();

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Book1.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Book1.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to autofit rows and columns in an Excel worksheet in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Format%20rows%20and%20columns/Autofit%20Rows%20and%20Columns).

N> 1) If a Range is text wrapped, the AutoFitColumn method will not be applied on it.
N> 2) If a Range is merged, the Auto-Fit methods will not be applied on it. Note that this is the behavior of Excel as well.
N> 3) Auto fitting is a time consuming process so, it might cause performance issues when used excessively.

## Group or Ungroup Rows and Columns 

Rows and columns can be grouped or ungrouped to summarize the data, which is given in the following code snippet.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
  IWorksheet worksheet = workbook.Worksheets[0];

  //Group Rows
  worksheet.Range["A1:A3"].Group(ExcelGroupBy.ByRows, true);
  worksheet.Range["A4:A6"].Group(ExcelGroupBy.ByRows);
  //Group Columns
  worksheet.Range["A1:B1"].Group(ExcelGroupBy.ByColumns, false);
  worksheet.Range["C1:F1"].Group(ExcelGroupBy.ByColumns);

  //Ungroup Rows
  worksheet.Range["A1:A3"].Ungroup(ExcelGroupBy.ByRows);
  //Ungroup Columns
  worksheet.Range["C1:F1"].Ungroup(ExcelGroupBy.ByColumns);

  workbook.SaveAs("Book1.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Group Rows
  worksheet.Range("A1:A3").Group(ExcelGroupBy.ByRows, True)
  worksheet.Range("A4:A6").Group(ExcelGroupBy.ByRows)
  'Group Columns
  worksheet.Range("A1:B1").Group(ExcelGroupBy.ByColumns, False)
  worksheet.Range("C1:F1").Group(ExcelGroupBy.ByColumns)

  'Ungroup Rows
  worksheet.Range("A1:A3").Ungroup(ExcelGroupBy.ByRows)
  'Ungroup Columns
  worksheet.Range("C1:F1").Ungroup(ExcelGroupBy.ByColumns)

  workbook.SaveAs("Book1.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
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

  //Group Rows
  worksheet.Range["A1:A3"].Group(ExcelGroupBy.ByRows, true);
  worksheet.Range["A4:A6"].Group(ExcelGroupBy.ByRows);
  //Group Columns
  worksheet.Range["A1:B1"].Group(ExcelGroupBy.ByColumns, false);
  worksheet.Range["C1:F1"].Group(ExcelGroupBy.ByColumns);

  //Ungroup Rows
  worksheet.Range["A1:A3"].Ungroup(ExcelGroupBy.ByRows);
  //Ungroup Columns
  worksheet.Range["C1:F1"].Ungroup(ExcelGroupBy.ByColumns);

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Book1";
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
  application.DefaultVersion = ExcelVersion.Excel2013;
  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Group Rows
  worksheet.Range["A1:A3"].Group(ExcelGroupBy.ByRows, true);
  worksheet.Range["A4:A6"].Group(ExcelGroupBy.ByRows);
  //Group Columns
  worksheet.Range["A1:B1"].Group(ExcelGroupBy.ByColumns, false);
  worksheet.Range["C1:F1"].Group(ExcelGroupBy.ByColumns);

  //Ungroup Rows
  worksheet.Range["A1:A3"].Ungroup(ExcelGroupBy.ByRows);
  //Ungroup Columns
  worksheet.Range["C1:F1"].Ungroup(ExcelGroupBy.ByColumns);

  //Saving the workbook as stream
  FileStream stream = new FileStream("Book1.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.XlsIO.Samples.Template.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Group Rows
  worksheet.Range["A1:A3"].Group(ExcelGroupBy.ByRows, true);
  worksheet.Range["A4:A6"].Group(ExcelGroupBy.ByRows);
  //Group Columns
  worksheet.Range["A1:B1"].Group(ExcelGroupBy.ByColumns, false);
  worksheet.Range["C1:F1"].Group(ExcelGroupBy.ByColumns);

  //Ungroup Rows
  worksheet.Range["A1:A3"].Ungroup(ExcelGroupBy.ByRows);
  //Ungroup Columns
  worksheet.Range["C1:F1"].Ungroup(ExcelGroupBy.ByColumns);

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Book1.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Book1.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to group rows and columns in an Excel worksheet in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Format%20rows%20and%20columns/Group%20Rows%20and%20Columns).

A complete working example to ungroup rows and columns in an Excel worksheet in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Format%20rows%20and%20columns/Ungroup%20Rows%20and%20Columns).

### Expand or Collapse Groups

Groups can be expanded and collapsed using the **ExpandGroups** and **CollapseGroups** methods of __IRange__, which is given in the following code snippet.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
  IWorksheet worksheet = workbook.Worksheets[0];

  //Expand group with flag set to expand parent
  worksheet.Range["A5:A15"].ExpandGroup(ExcelGroupBy.ByRows, ExpandCollapseFlags.ExpandParent);

  //Collapse group
  worksheet.Range["A5:A15"].CollapseGroup(ExcelGroupBy.ByRows);

  workbook.SaveAs("Book1.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Expand group with flag set to expand parent
  worksheet.Range("A5:A15").ExpandGroup(ExcelGroupBy.ByRows, ExpandCollapseFlags.ExpandParent)

  'Collapse group
  worksheet.Range("A5:A15").CollapseGroup(ExcelGroupBy.ByRows)

  workbook.SaveAs("Book1.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
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

  //Expand group with flag set to expand parent
  worksheet.Range["A5:A15"].ExpandGroup(ExcelGroupBy.ByRows, ExpandCollapseFlags.ExpandParent);

  //Collapse group
  worksheet.Range["A5:A15"].CollapseGroup(ExcelGroupBy.ByRows);

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Book1";
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
  application.DefaultVersion = ExcelVersion.Excel2013;
  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Expand group with flag set to expand parent
  worksheet.Range["A5:A15"].ExpandGroup(ExcelGroupBy.ByRows, ExpandCollapseFlags.ExpandParent);

  //Collapse group
  worksheet.Range["A5:A15"].CollapseGroup(ExcelGroupBy.ByRows);

  //Saving the workbook as stream
  FileStream stream = new FileStream("Book1.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.XlsIO.Samples.Template.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Expand group with flag set to expand parent
  worksheet.Range["A5:A15"].ExpandGroup(ExcelGroupBy.ByRows, ExpandCollapseFlags.ExpandParent);

  //Collapse group
  worksheet.Range["A5:A15"].CollapseGroup(ExcelGroupBy.ByRows);

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Book1.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Book1.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to expand or collapse groups in an Excel worksheet in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Format%20rows%20and%20columns/Expand%20or%20Collapse%20Groups).

### Subtotal

The XlsIO supports subtotaling a group to quickly calculate rows of related data by inserting subtotals and totals. 

Various Subtotal options like __Summary__ __below__ __data__, __Replace__ __current__ __subtotals__, __Page__ __break__ __between__ __groups__ can be used to customize data.

The following code shows how to add subtotal for a given range.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set the range for subtotaling
  IRange range = worksheet.Range["C3:G12"];

  //Perform subtotals for the range with every change in first column
  //and subtotals to be included for specified list of columns
  range.SubTotal(0, ConsolidationFunction.Sum, new int[] { 2, 3, 4 });

  workbook.SaveAs("Book1.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Set the range for subtotaling
  Dim range As IRange = worksheet("C3:G12")

  'Perform subtotals for the range with every change in first column
  'and subtotals to be included for specified list of columns
  range.SubTotal(0, ConsolidationFunction.Sum, New Integer() {4})

  workbook.SaveAs("Book1.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
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

  //Set the range for subtotaling
  IRange range = worksheet.Range["C3:G12"];

  //Perform subtotals for the range with every change in first column
  //and subtotals to be included for specified list of columns
  range.SubTotal(0, ConsolidationFunction.Sum, new int[] { 2, 3, 4 });

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Book1";
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
  application.DefaultVersion = ExcelVersion.Excel2013;
  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set the range for subtotaling
  IRange range = worksheet.Range["C3:G12"];

  //Perform subtotals for the range with every change in first column
  //and subtotals to be included for specified list of columns
  range.SubTotal(0, ConsolidationFunction.Sum, new int[] { 2, 3, 4 });

  //Saving the workbook as stream
  FileStream stream = new FileStream("Book1.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.XlsIO.Samples.Template.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set the range for subtotaling
  IRange range = worksheet.Range["C3:G12"];

  //Perform subtotals for the range with every change in first column
  //and subtotals to be included for specified list of columns
  range.SubTotal(0, ConsolidationFunction.Sum, new int[] { 2, 3, 4 });

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Book1.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Book1.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

N> Here column and row indexes are "zero based".

The screenshot of the output with SubTotal generated from the previous code.

![Subtotal applied to the range](Worksheet-Rows-and-Columns-Manipulation_images/Worksheet-Rows-and-Columns-Manipulation_img1.jpeg)


N> Summary of a group can be shown above the rows and left of the column using the IsSummaryRowBelow and IsSummaryColumnRight properties of IPageSetup interface. By default, these properties are set to TRUE.

