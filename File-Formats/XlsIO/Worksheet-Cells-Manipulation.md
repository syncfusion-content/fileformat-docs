---
title: Worksheet Cells Manipulation | Syncfusion
description: This section illustrates about cells manipulation in Excel worksheet using Syncfusion XlsIO (a .NET Excel library).
platform: file-formats
control: XlsIO
documentation: UG
keywords: c#, vb.net, excel, read excel, edit excel, edit excel cell, write excel cell, fill excel, write excel, update excel, syncfusion, xlsio
---

# Worksheet Cells Manipulation

The [IRange](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IRange.html) interface represents a single cell or a group of cells in a worksheet. XlsIO has several useful methods for accessing, manipulating and formatting the content in the cells.

## Accessing a Cell or a Range

The following code shows the different ways of accessing a single cell or group of cells

N> Here row and column indexes in the range are "one-based". 

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Access a range by specifying cell address
  sheet.Range["A7"].Text = "Accessing a Range by specify cell address ";

  //Access a range by specifying cell row and column index
  sheet.Range[9, 1].Text = "Accessing a Range by specify cell row and column index ";

  //Access a Range by specifying using defined name
  IName name = workbook.Names.Add("Name");
  name.RefersToRange = sheet.Range["A11"];
  sheet.Range["Name"].Text = "Accessing a Range by specifying using defined name.";

  //Accessing a Range of cells by specifying cells address
  sheet.Range["A13:C13"].Text = "Accessing a Range of Cells (Method 1)";

  //Accessing a Range of cells specifying cell row and column index
  sheet.Range[15, 1, 15, 3].Text = "Accessing a Range of Cells (Method 2)";

  workbook.SaveAs("Range.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Access a range by specify cell address
  sheet.Range("A7").Text = "Accessing a Range by specify cell address "

  'Access a range by specify cell row and column index
  sheet.Range(9, 1).Text = "Accessing a Range by specify cell row and column index "

  'Access a Range by specifying using defined name
  Dim name As IName = workbook.Names.Add("Name")
  name.RefersToRange = sheet.Range("A11")
  sheet.Range("Name").Text = "Accessing a Range by specifying using defined name"

  'Accessing a Range of cells by specify cells address
  sheet.Range("A13:C13").Text = "Accessing a Range of Cells (Method 1)"

  'Accessing a Range of cells specify cell row and column index
  sheet.Range(15, 1, 15, 3).Text = "Accessing a Range of Cells (Method 2)"

  workbook.SaveAs("Range.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Access a range by specifying cell address
  sheet.Range["A7"].Text = "Accessing a Range by specify cell address ";

  //Access a range by specifying cell row and column index
  sheet.Range[9, 1].Text = "Accessing a Range by specify cell row and column index ";

  //Access a Range by specifying using defined name
  IName name = workbook.Names.Add("Name");
  name.RefersToRange = sheet.Range["A11"];
  sheet.Range["Name"].Text = "Accessing a Range by specifying using defined name";

  //Accessing a Range of cells by specifying cells address
  sheet.Range["A13:C13"].Text = "Accessing a Range of Cells (Method 1)";

  //Accessing a Range of cells specifying cell row and column index
  sheet.Range[15, 1, 15, 3].Text = "Accessing a Range of Cells (Method 2)";

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Range";
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
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Access a range by specifying cell address
  sheet.Range["A7"].Text = "Accessing a Range by specify cell address ";

  //Access a range by specifying cell row and column index
  sheet.Range[9, 1].Text = "Accessing a Range by specify cell row and column index ";

  //Access a Range by specifying using defined name
  IName name = workbook.Names.Add("Name");
  name.RefersToRange = sheet.Range["A11"];
  sheet.Range["Name"].Text = "Accessing a Range by specifying using defined name";

  //Accessing a Range of cells by specifying cells address
  sheet.Range["A13:C13"].Text = "Accessing a Range of Cells (Method 1)";

  //Accessing a Range of cells specifying cell row and column index
  sheet.Range[15, 1, 15, 3].Text = "Accessing a Range of Cells (Method 2)";

  //Saving the workbook as stream
  FileStream stream = new FileStream("Range.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Access a range by specifying cell address 
  sheet.Range["A7"].Text = "Accessing a Range by specify cell address ";

  //Access a range by specifying cell row and column index
  sheet.Range[9, 1].Text = "Accessing a Range by specify cell row and column index ";

  //Access a Range by specifying using defined name
  IName name = workbook.Names.Add("Name");
  name.RefersToRange = sheet.Range["A11"];
  sheet.Range["Name"].Text = "Accessing a Range by specifying using defined name";

  //Accessing a Range of cells by specifying cells address
  sheet.Range["A13:C13"].Text = "Accessing a Range of Cells (Method 1)";

  //Accessing a Range of cells specifying cell row and column index
  sheet.Range[15, 1, 15, 3].Text = "Accessing a Range of Cells (Method 2)";

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Range.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Range.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to access a cell or range in an Excel worksheet in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Editing%20Excel%20cells/Access%20Cell%20or%20Range).

T> You can make use of GetText, SetText, GetNumber and SetNumber methods from worksheet object that enable users to get/set values without range object.

## Accessing Relative Range

By default, accessing a range by index will return the cell or range from worksheet level. To get a relative range for the indexes provided, it is recommended to set the [ExcelRangeIndexerMode](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelRangeIndexerMode.html) option. Here, the RowIndex and ColumnIndex arguments are relative offsets, where specifying a RowIndex of 1 returns cells in the first row of the range not the first  row of the worksheet.

For example, if a range is mentioned as "B3:D5", then accessing a range with the index [1,1] will return the cell "A1" from worksheet. If the **ExcelRangeIndexerMode** is set to **Relative** then it returns "B3".

Following code example illustrates how to access the range relatively to the existing range object in XlsIO.

N> Here row and column indexes in the range are "one-based".

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;

  //Setting range index mode to relative
  application.RangeIndexerMode = ExcelRangeIndexerMode.Relative;

  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Creating a range by specifying cells address
  IRange range1 = sheet.Range["B3:D5"];

  //Accessing a range relatively to the existing range by specifying cell row and column index
  range1[2, 2].Text = "Returns C4 cell";
  range1[0, 0].Text = "Returns A2 cell";

  //Creating a Range of cells specifying cell row and column index
  IRange range2 = sheet.Range[5, 1, 10, 3];

  //Accessing a range relatively to the existing range of cells by specifying cell row and column index
  range2[2, 2, 3, 3].Text = "Returns range of cells B6 to C7";

  workbook.SaveAs("Range.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx

  'Setting range index mode to relative
  application.RangeIndexerMode = ExcelRangeIndexerMode.Relative

  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Creating a range by specifying cells address
  Dim range1 As IRange = sheet.Range("B3:D5")

  'Accessing a range relatively to the existing range by specifying cell row and column index
  range1(2, 2).Text = "Returns B4 cell"
  range1(0, 0).Text = "Returns A2 cell"

  Dim range2 As IRange = sheet.Range(5, 1, 10, 3)
  'Accessing a range relatively to the existing range of cells by specifying cell row and column index
  range2(2, 2, 3, 3).Text = "Returns range of cells B6 to C7"

  workbook.SaveAs("Range.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;

  //Setting range index mode to relative
  application.RangeIndexerMode = ExcelRangeIndexerMode.Relative;

  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Creating a range by specifying cells address
  IRange range1 = sheet.Range["B3:D5"];

  //Accessing a range relatively to the existing range by specifying cell row and column index
  range1[2, 2].Text = "Returns C4 cell";
  range1[0, 0].Text = "Returns A2 cell";

  //Creating a Range of cells specifying cell row and column index
  IRange range2 = sheet.Range[5, 1, 10, 3];

  //Accessing a range relatively to the existing range of cells by specifying cell row and column index
  range2[2, 2, 3, 3].Text = "Returns range of cells B6 to C7";

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Range";
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

  //Setting range index mode to relative
  application.RangeIndexerMode = ExcelRangeIndexerMode.Relative;

  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Creating a range by specifying cells address
  IRange range1 = sheet.Range["B3:D5"];

  //Accessing a range relatively to the existing range by specifying cell row and column index
  range1[2, 2].Text = "Returns C4 cell";
  range1[0, 0].Text = "Returns A2 cell";

  //Creating a Range of cells specifying cell row and column index
  IRange range2 = sheet.Range[5, 1, 10, 3];

  //Accessing a range relatively to the existing range of cells by specifying cell row and column index
  range2[2, 2, 3, 3].Text = "Returns range of cells B6 to C7";

  //Saving the workbook as stream
  FileStream stream = new FileStream("Range.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;

  //Setting range index mode to relative
  application.RangeIndexerMode = ExcelRangeIndexerMode.Relative;

  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Creating a range by specifying cells address
  IRange range1 = sheet.Range["B3:D5"];

  //Accessing a range relatively to the existing range by specifying cell row and column index
  range1[2, 2].Text = "Returns C4 cell";
  range1[0, 0].Text = "Returns A2 cell";

  //Creating a Range of cells specifying cell row and column index
  IRange range2 = sheet.Range[5, 1, 10, 3];

  //Accessing a range relatively to the existing range of cells by specifying cell row and column index
  range2[2, 2, 3, 3].Text = "Returns range of cells B6 to C7";

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Range.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Range.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to access relative range in an Excel worksheet in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Editing%20Excel%20cells/Access%20Relative%20Range).

### Accessing Discontinuous Ranges

It is possible to modify the contents or apply formatting to discontinuous range by accessing and adding them to the [RangesCollection](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.Implementation.Collections.RangesCollection.html).

Following code snippet illustrates how to access discontinuous range.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //range1 and range2 are discontinuous ranges
  IRange range1 = sheet.Range["A1:A2"];
  IRange range2 = sheet.Range["C1:C2"];
  IRanges ranges = sheet.CreateRangesCollection();

  //range1 and range2 are considered as a single range
  ranges.Add(range1);
  ranges.Add(range2);
  ranges.Text = "Test";

  workbook.SaveAs("Range.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'range1 and range2 are discontinuous ranges
  Dim range1 As IRange = sheet.Range("A1:A2")
  Dim range2 As IRange = sheet.Range("C1:C2")
  Dim ranges As IRanges = sheet.CreateRangesCollection()

  'range1 and range2 are considered as a single range
  ranges.Add(range1)
  ranges.Add(range2)
  ranges.Text = "Test"

  workbook.SaveAs("Range.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //range1 and range2 are discontinuous ranges
  IRange range1 = sheet.Range["A1:A2"];
  IRange range2 = sheet.Range["C1:C2"];
  IRanges ranges = sheet.CreateRangesCollection();

  //range1 and range2 are considered as a single range
  ranges.Add(range1);
  ranges.Add(range2);
  ranges.Text = "Test";

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Range";
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
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //range1 and range2 are discontinuous ranges
  IRange range1 = sheet.Range["A1:A2"];
  IRange range2 = sheet.Range["C1:C2"];
  IRanges ranges = sheet.CreateRangesCollection();

  //range1 and range2 are considered as a single range
  ranges.Add(range1);
  ranges.Add(range2);
  ranges.Text = "Test";

  //Saving the workbook as stream
  FileStream stream = new FileStream("Range.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //range1 and range2 are discontinuous ranges
  IRange range1 = sheet.Range["A1:A2"];
  IRange range2 = sheet.Range["C1:C2"];
  IRanges ranges = sheet.CreateRangesCollection();

  //range1 and range2 are considered as a single range
  ranges.Add(range1);
  ranges.Add(range2);
  ranges.Text = "Test";

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Range.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Range.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to access discontinuous range in an Excel worksheet in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Editing%20Excel%20cells/Access%20Discontinuous%20Range).

### Accessing a Cell or Range using IMigrantRange 

The [IMigrantRange](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IMigrantRange.html) interface can also be used to access a single cell or group of cells and manipulate it.  It is recommended to prefer **IMigrantRange** instead of [IRange](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IRange.html) for writing large amount of data in an optimal way. 

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];
  IMigrantRange migrantRange = sheet.MigrantRange;

  //Writing Data
  for (int row = 1; row <= migrantRange.LastRow; row++)
  {
	for (int column = 1; column <= migrantRange.LastColumn; column++)
	{
	  //Writing values
	  migrantRange.ResetRowColumn(row, column);
	  migrantRange.Text = "Test";
	}
   }
  
  workbook.SaveAs("Range.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim sheet As IWorksheet = workbook.Worksheets(0)
  Dim migrantRange As IMigrantRange = sheet.MigrantRange

  'Writing Data
  Dim row As Integer
  For row = 1 To migrantRange.LastRow Step row + 1
	Dim column As Integer
	For column = 1 To migrantRange.LastColumn Step column + 1
	  'Writing values
	  migrantRange.ResetRowColumn(row, column)
	  migrantRange.Text = "Test"
	Next
  Next

  workbook.SaveAs("Range.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];
  IMigrantRange migrantRange = sheet.MigrantRange;

  //Writing Data
  for (int row = 1; row <= migrantRange.LastRow; row++)
  {
	for (int column = 1; column <= migrantRange.LastColumn; column++)
	{
	  //Writing values
	  migrantRange.ResetRowColumn(row, column);
	  migrantRange.Text = "Test";
	}
  }

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Range";
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
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];
  IMigrantRange migrantRange = sheet.MigrantRange;

  //Writing Data
  for (int row = 1; row <= migrantRange.LastRow; row++)
  {
	for (int column = 1; column <= migrantRange.LastColumn; column++)
	{
	  //Writing values
	  migrantRange.ResetRowColumn(row, column);
	  migrantRange.Text = "Test";
	}
  }

  //Saving the workbook as stream
  FileStream stream = new FileStream("Range.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];
  IMigrantRange migrantRange = sheet.MigrantRange;

  //Writing Data
  for (int row = 1; row <= migrantRange.LastRow; row++)
  {
	for (int column = 1; column <= migrantRange.LastColumn; column++)
	{
	  //Writing values
	  migrantRange.ResetRowColumn(row, column);
	  migrantRange.Text = "Test";
	}
  }

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Range.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Range.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to access migrant range in an Excel worksheet in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Editing%20Excel%20cells/Access%20Migrant%20Range).

## Accessing used range of a Worksheet

The following code snippet shows how to get the range of used cells in a given Excel worksheet.

N> By default, XlsIO considers a cell as used, even if there exists some formatting alone. This behavior can be disabled, and make XlsIO consider a cell as used, only when there exists data, through the [UsedRangeIncludesFormatting](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.Implementation.WorksheetImpl.html#Syncfusion_XlsIO_Implementation_WorksheetImpl_UsedRangeIncludesFormatting) property.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
  IWorksheet sheet = workbook.Worksheets[0];

  //UsedRange excludes the blank cell which has formatting
  sheet.UsedRangeIncludesFormatting = false;

  //Modifying the column width and row height of the used range
  sheet.UsedRange.ColumnWidth = 20;
  sheet.UsedRange.RowHeight = 20;

  workbook.SaveAs("Range.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'UsedRange excludes the blank cell which has formatting
  sheet.UsedRangeIncludesFormatting = False

  'Modifying only the Used Ranges
  sheet.UsedRange.ColumnWidth = 20
  sheet.UsedRange.RowHeight = 20

  workbook.SaveAs("Range.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;

  //Instantiates the File Picker
  FileOpenPicker openPicker = new FileOpenPicker();
  openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
  openPicker.FileTypeFilter.Add(".xlsx");
  openPicker.FileTypeFilter.Add(".xls");
  StorageFile file = await openPicker.PickSingleFileAsync();

  //Opens the workbook
  IWorkbook workbook = await application.Workbooks.OpenAsync(file);
  IWorksheet worksheet = workbook.Worksheets[0];

  //UsedRange excludes the blank cell which has formatting
  worksheet.UsedRangeIncludesFormatting = false;

  //Modifying the column width and row height of the used range
  worksheet.UsedRange.ColumnWidth = 20;
  worksheet.UsedRange.RowHeight = 20;

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Range";
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

  //UsedRange excludes the blank cell which has formatting
  worksheet.UsedRangeIncludesFormatting = false;

  //Modifying the column width and row height of the used range
  worksheet.UsedRange.ColumnWidth = 20;
  worksheet.UsedRange.RowHeight = 20;

  //Saving the workbook as stream
  FileStream stream = new FileStream("Range.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;

  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream = assembly.GetManifestResourceStream("CellManipulation.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //UsedRange excludes the blank cell which has formatting
  worksheet.UsedRangeIncludesFormatting = false;

  //Modifying the column width and row height of the used range
  worksheet.UsedRange.ColumnWidth = 20;
  worksheet.UsedRange.RowHeight = 20;

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Range.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Range.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to access used range in an Excel worksheet in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Editing%20Excel%20cells/Access%20Used%20Range).

## Get Precedent and Dependent Cells or Range

Precedent cells are cells that are referred to by a formula in another cell. Dependent cells contain formulas that refer to other cells. XlsIO allows to trace the relationship between cells and formulas in Excel workbooks and returns the list of cells or range that are precedent and dependent.

Accessing list of precedent and dependent cells can be obtained:

*	from a worksheet
*	from a workbook

Following code example illustrates how to get precedent cells from a worksheet and entire workbook.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Open("FormulaExcel.xlsx");
  IWorksheet sheet = workbook.Worksheets[0];

  //Getting precedent cells from the worksheet
  IRange[] results1 = sheet["A1"].GetPrecedents();

  //Getting precedent cells from the workbook
  IRange[] results2 = sheet["A1"].GetPrecedents(true);

  string fileName = "Precedents.xlsx";
  workbook.SaveAs(fileName);
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Open("FormulaExcel.xlsx")
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Getting precedent cells from the worksheet
  Dim results1() As IRange = sheet("A1").GetPrecedents()

  'Getting precedent cells from the workbook
  Dim results2() As IRange = sheet("A1").GetPrecedents(True)

  Dim fileName As String = "Precedents.xlsx"
  workbook.SaveAs(fileName)
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  //Instantiates the File Picker
  FileOpenPicker openPicker = new FileOpenPicker();
  openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
  openPicker.FileTypeFilter.Add(".xlsx");
  openPicker.FileTypeFilter.Add(".xls");
  StorageFile file = await openPicker.PickSingleFileAsync();

  //Opens the workbook
  IWorkbook workbook = await application.Workbooks.OpenAsync(file);
  IWorksheet sheet = workbook.Worksheets[0];

  //Getting precedent cells from the worksheet
  IRange[] results1 = sheet["A1"].GetPrecedents();

  //Getting precedent cells from the workbook
  IRange[] results2 = sheet["A1"].GetPrecedents(true);

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Precedents";
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
  FileStream inputStream = new FileStream("FormulaExcel.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet sheet = workbook.Worksheets[0];

  //Getting precedent cells from the worksheet
  IRange[] results1 = sheet["A1"].GetPrecedents();

  //Getting precedent cells from the workbook
  IRange[] results2 = sheet["A1"].GetPrecedents(true);

  //Saving the workbook as stream
  FileStream file = new FileStream("Precedents.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(file);
  file.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream = assembly.GetManifestResourceStream("CellManipulation.FormulaExcel.xlsx");
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet sheet = workbook.Worksheets[0];

  //Getting precedent cells from the worksheet
  IRange[] results1 = sheet["A1"].GetPrecedents();

  //Getting precedent cells from the workbook
  IRange[] results2 = sheet["A1"].GetPrecedents(true);

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Precedents.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Precedents.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

Following code example illustrates how to get dependent cells from a worksheet and entire workbook.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Open("FormulaExcel.xlsx");
  IWorksheet sheet = workbook.Worksheets[0];

  //Getting dependent cells from the worksheet
  IRange[] results1 = sheet["A1"].GetDependents();

  //Getting dependent cells from the workbook
  IRange[] results2 = sheet["A1"].GetDependents(true);

  string fileName = "Dependents.xlsx";
  workbook.SaveAs(fileName);
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Open("FormulaExcel.xlsx")
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Getting dependent cells from the worksheet
  Dim results1() As IRange = sheet("A1").GetDependents()

  'Getting dependent cells from the workbook
  Dim results2() As IRange = sheet("A1").GetDependents(True)

  Dim fileName As String = "Dependents.xlsx"
  workbook.SaveAs(fileName)
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  //Instantiates the File Picker
  FileOpenPicker openPicker = new FileOpenPicker();
  openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
  openPicker.FileTypeFilter.Add(".xlsx");
  openPicker.FileTypeFilter.Add(".xls");
  StorageFile file = await openPicker.PickSingleFileAsync();

  //Opens the workbook
  IWorkbook workbook = await application.Workbooks.OpenAsync(file);
  IWorksheet sheet = workbook.Worksheets[0];

  //Getting dependent cells from the worksheet
  IRange[] results1 = sheet["A1"].GetDependents();

  //Getting dependent cells from the workbook
  IRange[] results2 = sheet["A1"].GetDependents(true);

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Dependents";
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
  FileStream inputStream = new FileStream("FormulaExcel.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet sheet = workbook.Worksheets[0];

  //Getting dependent cells from the worksheet
  IRange[] results1 = sheet["A1"].GetDependents();

  //Getting dependent cells from the workbook
  IRange[] results2 = sheet["A1"].GetDependents(true);

  //Saving the workbook as stream
  FileStream file = new FileStream("Dependents.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(file);
  file.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream = assembly.GetManifestResourceStream("CellManipulation.FormulaExcel.xlsx");
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet sheet = workbook.Worksheets[0];

  //Getting dependent cells from the worksheet
  IRange[] results1 = sheet["A1"].GetDependents();

  //Getting dependent cells from the workbook
  IRange[] results2 = sheet["A1"].GetDependents(true);

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Dependents.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Dependents.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

### Get Direct Precedent and Dependent Cells

[GetDirectDependents](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IRange.html#Syncfusion_XlsIO_IRange_GetDirectDependents) and [GetDirectPrecedents](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IRange.html#Syncfusion_XlsIO_IRange_GetDirectPrecedents) methods are used to get direct dependent/precedent cells for source range, excluding inner dependent/precedent cells. 

Following code example illustrates how to get direct precedent cells from a worksheet and entire workbook.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Open("FormulaExcel.xlsx");
  IWorksheet sheet = workbook.Worksheets[0];

  //Getting precedent cells from the worksheet
  IRange[] results1 = sheet["A1"].GetDirectPrecedents();

  //Getting precedent cells from the workbook
  IRange[] results2 = sheet["A1"].GetDirectPrecedents(true);

  string fileName = "DirectPrecedents.xlsx";
  workbook.SaveAs(fileName);
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Open("FormulaExcel.xlsx")
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Getting precedent cells from the worksheet
  Dim results1() As IRange = sheet("A1").GetDirectPrecedents()

  'Getting precedent cells from the workbook
  Dim results2() As IRange = sheet("A1").GetDirectPrecedents(True)

  Dim fileName As String = "DirectPrecedents.xlsx"
  workbook.SaveAs(fileName)
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  //Instantiates the File Picker
  FileOpenPicker openPicker = new FileOpenPicker();
  openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
  openPicker.FileTypeFilter.Add(".xlsx");
  openPicker.FileTypeFilter.Add(".xls");
  StorageFile file = await openPicker.PickSingleFileAsync();

  //Opens the workbook
  IWorkbook workbook = await application.Workbooks.OpenAsync(file);
  IWorksheet sheet = workbook.Worksheets[0];

  //Getting precedent cells from the worksheet
  IRange[] results1 = sheet["A1"].GetDirectPrecedents();

  //Getting precedent cells from the workbook
  IRange[] results2 = sheet["A1"].GetDirectPrecedents(true);

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "DirectPrecedents";
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
  FileStream inputStream = new FileStream("FormulaExcel.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet sheet = workbook.Worksheets[0];

  //Getting precedent cells from the worksheet
  IRange[] results1 = sheet["A1"].GetDirectPrecedents();

  //Getting precedent cells from the workbook
  IRange[] results2 = sheet["A1"].GetDirectPrecedents(true);

  //Saving the workbook as stream
  FileStream file = new FileStream("DirectPrecedents.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(file);
  file.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream = assembly.GetManifestResourceStream("CellManipulation.FormulaExcel.xlsx");
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet sheet = workbook.Worksheets[0];

  //Getting precedent cells from the worksheet
  IRange[] results1 = sheet["A1"].GetDirectPrecedents();

  //Getting precedent cells from the workbook
  IRange[] results2 = sheet["A1"].GetDirectPrecedents(true);

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("DirectPrecedents.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("DirectPrecedents.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

Following code example illustrates how to get direct dependent cells from a worksheet and entire workbook.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Open("FormulaExcel.xlsx");
  IWorksheet sheet = workbook.Worksheets[0];

  //Getting dependent cells from the worksheet
  IRange[] results1 = sheet["A1"].GetDirectDependents();

  //Getting dependent cells from the workbook
  IRange[] results2 = sheet["A1"].GetDirectDependents(true);

  string fileName = "DirectDependents.xlsx";
  workbook.SaveAs(fileName);
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Open("FormulaExcel.xlsx")
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Getting dependent cells from the worksheet
  Dim results1() As IRange = sheet("A1").GetDirectDependents()

  'Getting dependent cells from the workbook
  Dim results2() As IRange = sheet("A1").GetDirectDependents(True)

  Dim fileName As String = "DirectDependents.xlsx"
  workbook.SaveAs(fileName)
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  //Instantiates the File Picker
  FileOpenPicker openPicker = new FileOpenPicker();
  openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
  openPicker.FileTypeFilter.Add(".xlsx");
  openPicker.FileTypeFilter.Add(".xls");
  StorageFile file = await openPicker.PickSingleFileAsync();

  //Opens the workbook
  IWorkbook workbook = await application.Workbooks.OpenAsync(file);
  IWorksheet sheet = workbook.Worksheets[0];

  //Getting dependent cells from the worksheet
  IRange[] results1 = sheet["A1"].GetDirectDependents();

  //Getting dependent cells from the workbook
  IRange[] results2 = sheet["A1"].GetDirectDependents(true);

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "DirectDependents";
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
  FileStream inputStream = new FileStream("FormulaExcel.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet sheet = workbook.Worksheets[0];

  //Getting dependent cells from the worksheet
  IRange[] results1 = sheet["A1"].GetDirectDependents();

  //Getting dependent cells from the workbook
  IRange[] results2 = sheet["A1"].GetDirectDependents(true);

  //Saving the workbook as stream
  FileStream file = new FileStream("DirectDependents.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(file);
  file.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream = assembly.GetManifestResourceStream("CellManipulation.FormulaExcel.xlsx");
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet sheet = workbook.Worksheets[0];

  //Getting dependent cells from the worksheet
  IRange[] results1 = sheet["A1"].GetDirectDependents();

  //Getting dependent cells from the workbook
  IRange[] results2 = sheet["A1"].GetDirectDependents(true);

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("DirectDependents.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("DirectDependents.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to get the precedent and dependent cells in an Excel worksheet in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Editing%20Excel%20cells/Precedent%20and%20Dependent%20Cells).

## Clearing a Cell Content

Either entire cell content, or just formatting, contents, or comments can be removed from Excel cell. The following code example illustrates how to clear a range along with its formatting.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
  IWorksheet sheet = workbook.Worksheets[0];

  //Clearing a Range “A4” and its formatting
  sheet.Range["A4"].Clear(true);

  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs("ClearRange.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Clearing a Range “A4” and its formatting
  sheet.Range("A4").Clear(True)

  workbook.Version = ExcelVersion.Xlsx
  workbook.SaveAs("ClearRange.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;

  //Instantiates the File Picker
  FileOpenPicker openPicker = new FileOpenPicker();
  openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
  openPicker.FileTypeFilter.Add(".xlsx");
  openPicker.FileTypeFilter.Add(".xls");
  StorageFile file = await openPicker.PickSingleFileAsync();

  //Opens the workbook
  IWorkbook workbook = await application.Workbooks.OpenAsync(file);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Clearing a Range “A4” and its formatting
  worksheet.Range["A4"].Clear(true);

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "ClearRange";
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

  //Clearing a Range “A4” and its formatting
  worksheet.Range["A4"].Clear(true);

  //Saving the workbook as stream
  FileStream stream = new FileStream("ClearRange.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;

  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream = assembly.GetManifestResourceStream("CellManipulation.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Clearing a Range “A4” and its formatting
  worksheet.Range["A4"].Clear(true);

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("ClearRange.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("ClearRange.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to clear cell content in an Excel worksheet in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Editing%20Excel%20cells/Clear%20Content).

## Copy or Move a Range

A single cell or a range of cells can be copied to another range using [CopyTo](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IRange.html#Syncfusion_XlsIO_IRange_CopyTo_Syncfusion_XlsIO_IRange_) method. It is also possible to copy all the formats or only specific formats using [ExcelCopyRangeOptions](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelCopyRangeOptions.html) options. 

Following code example illustrates how to copy a cell from the source to destination.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
  IWorksheet sheet = workbook.Worksheets[0];

  //Copying a Range “A1” to “A5”
  IRange source = sheet.Range["A1"];
  IRange destination = sheet.Range["A5"];
  source.CopyTo(destination, ExcelCopyRangeOptions.All);

  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs("CopyRange.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Copying a Range “A1” to “A5”
  Dim source As IRange = sheet.Range("A1")
  Dim destination As IRange = sheet.Range("A5")
  source.CopyTo(destination, ExcelCopyRangeOptions.All)

  workbook.Version = ExcelVersion.Xlsx
  workbook.SaveAs("CopyRange.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  //Instantiates the File Picker
  FileOpenPicker openPicker = new FileOpenPicker();
  openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
  openPicker.FileTypeFilter.Add(".xlsx");
  openPicker.FileTypeFilter.Add(".xls");
  StorageFile file = await openPicker.PickSingleFileAsync();

  //Opens the workbook
  IWorkbook workbook = await application.Workbooks.OpenAsync(file);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Copying a Range “A1” to “A5”
  IRange source = worksheet.Range["A1"];
  IRange destination = worksheet.Range["A5"];
  source.CopyTo(destination, ExcelCopyRangeOptions.All);

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "CopyRange";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  workbook.Version = ExcelVersion.Xlsx;
  await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Copying a Range “A1” to “A5”
  IRange source = worksheet.Range["A1"];
  IRange destination = worksheet.Range["A5"];
  source.CopyTo(destination, ExcelCopyRangeOptions.All);

  //Saving the workbook as stream
  FileStream stream = new FileStream("CopyRange.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream = assembly.GetManifestResourceStream("CellManipulation.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Copying a Range “A1” to “A5”
  IRange source = worksheet.Range["A1"];
  IRange destination = worksheet.Range["A5"];
  source.CopyTo(destination, ExcelCopyRangeOptions.All);

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("CopyRange.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("CopyRange.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to copy range in an Excel worksheet in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Editing%20Excel%20cells/Copy%20Range).

[MoveTo](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IRange.html#Syncfusion_XlsIO_IRange_MoveTo_Syncfusion_XlsIO_IRange_) method is used for moving a range of cells to another range as shown below. 

N> **MoveTo** method does not update formulas.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
  IWorksheet sheet = workbook.Worksheets[0];

  //Moving a Range “A1” to “A5”
  IRange source = sheet.Range["A1"];
  IRange destination = sheet.Range["A5"];
  source.MoveTo(destination);

  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs("MoveRange.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Moving a Range “A1” to “A5”
  Dim source As IRange = sheet.Range("A1")
  Dim destination As IRange = sheet.Range("A5")
  source.MoveTo(destination)

  workbook.Version = ExcelVersion.Xlsx
  workbook.SaveAs("MoveRange.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  //Instantiates the File Picker
  FileOpenPicker openPicker = new FileOpenPicker();
  openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
  openPicker.FileTypeFilter.Add(".xlsx");
  openPicker.FileTypeFilter.Add(".xls");
  StorageFile file = await openPicker.PickSingleFileAsync();

  //Opens the workbook
  IWorkbook workbook = await application.Workbooks.OpenAsync(file);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Moving a Range “A1” to “A5”
  IRange source = worksheet.Range["A1"];
  IRange destination = worksheet.Range["A5"];
  source.MoveTo(destination);

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "MoveRange";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  workbook.Version = ExcelVersion.Xlsx;
  await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Moving a Range “A1” to “A5”
  IRange source = worksheet.Range["A1"];
  IRange destination = worksheet.Range["A5"];
  source.MoveTo(destination);

  //Saving the workbook as stream
  FileStream stream = new FileStream("MoveRange.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream = assembly.GetManifestResourceStream("CellsManipulation.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Moving a Range “A1” to “A5”
  IRange source = worksheet.Range["A1"];
  IRange destination = worksheet.Range["A5"];
  source.MoveTo(destination);

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("MoveRange.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("MoveRange.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to move range in an Excel worksheet in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Editing%20Excel%20cells/Move%20Range).

## Copy and Paste As Link

A range can be copied and paste the range as link to another range using a bool parameter in [CopyTo](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IRange.html#Syncfusion_XlsIO_IRange_CopyTo_Syncfusion_XlsIO_IRange_System_Boolean_) method.

Following code example illustrates how to paste a range of cells as link.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
  IWorksheet sheet = workbook.Worksheets[0];

  //Copy range as link from Range “A1” to “A5”
  IRange source = sheet.Range["A1"];
  IRange destination = sheet.Range["D5"];
  source.CopyTo(destination, true);

  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs("PasteLink.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Copy range as link from Range “A1” to “A5”
  Dim source As IRange = sheet.Range("A1")
  Dim destination As IRange = sheet.Range("A5")
  source.CopyTo(destination, True)

  workbook.Version = ExcelVersion.Xlsx
  workbook.SaveAs("PasteLink.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  //Instantiates the File Picker
  FileOpenPicker openPicker = new FileOpenPicker();
  openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
  openPicker.FileTypeFilter.Add(".xlsx");
  openPicker.FileTypeFilter.Add(".xls");
  StorageFile file = await openPicker.PickSingleFileAsync();

  //Opens the workbook
  IWorkbook workbook = await application.Workbooks.OpenAsync(file);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Copy range as link from Range “A1” to “A5”
  IRange source = worksheet.Range["A1"];
  IRange destination = worksheet.Range["A5"];
  source.CopyTo(destination, true);

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "PasteLink";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  workbook.Version = ExcelVersion.Xlsx;
  await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Copy range as link from Range “A1” to “A5”
  IRange source = worksheet.Range["A1"];
  IRange destination = worksheet.Range["A5"];
  source.CopyTo(destination, true);
  
  //Saving the workbook as stream
  FileStream stream = new FileStream("PasteLink.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream = assembly.GetManifestResourceStream("CellsManipulation.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Copy range as link from Range “A1” to “A5”
  IRange source = worksheet.Range["A1"];
  IRange destination = worksheet.Range["A5"];
  source.CopyTo(destination, true);

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("PasteLink.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("PasteLink.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to copy and paste as link in an Excel worksheet in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Editing%20Excel%20cells/Paste%20As%20Link).

## Skip Blanks While Copying

Blank cells can be skipped while copying from source to destination range by setting the parameter **skipBlanks** to TRUE in [CopyTo](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IRange.html#Syncfusion_XlsIO_IRange_CopyTo_Syncfusion_XlsIO_IRange_Syncfusion_XlsIO_ExcelCopyRangeOptions_System_Boolean_) method.

The following code illustrates how to skip blank cells while copying.

{% tabs %}

{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
  IWorksheet sheet = workbook.Worksheets[0];
  
  // Copy range as link from Range “A1” to “A5”.
  IRange source = sheet.Range["A1:A7"];
  IRange destination = sheet.Range["C3"];
  
  //Skip blanks while copying
  source.CopyTo(destination, ExcelCopyRangeOptions.All, true);
  
  //Save workbook
  workbook.SaveAs("SkipBlank.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx;
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
  Dim sheet As IWorkbook = workbook.Worksheets(0)
  
  ' Copy range as link from Range “A1” to “A5”.
  Dim source As IRange = sheet.Range("A1:A7")
  Dim destination As IRange = sheet.Range("C3")
  
  ' Skip blanks while copying
  source.CopyTo(destination, ExcelCopyRangeOptions.All, true)
  
  ' Save workbook
  workbook.SaveAs("SkipBlank.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  //Instantiates the File Picker. 
  FileOpenPicker openPicker = new FileOpenPicker();
  openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
  openPicker.FileTypeFilter.Add(".xlsx");
  openPicker.FileTypeFilter.Add(".xls");
  StorageFile openFile = await openPicker.PickSingleFileAsync();
  
  //Opens the workbook. 
  IWorkbook workbook = await application.Workbooks.OpenAsync(openFile);
  IWorksheet sheet = workbook.Worksheets[0];
  
  // Copy range as link from Range “A1” to “A5”.
  IRange source = sheet.Range["A1:A7"];
  IRange destination = sheet.Range["C3"];
  
  //Skip blanks while copying
  source.CopyTo(destination, ExcelCopyRangeOptions.All, true);
  
  //Initializes FileSavePicker.
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "SkipBlank";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });
  
  //Creates a storage file from FileSavePicker.
  StorageFile storageFile = await savePicker.PickSaveFileAsync();
  
  //Saves changes to the specified storage file.
  await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream sampleFile = new FileStream("Sample.xlsx", FileMode.Open);
  IWorkbook workbook = application.Workbooks.Open(sampleFile);
  IWorksheet sheet = workbook.Worksheets[0];             
  
  // Copy range as link from Range “A1” to “A5”.
  IRange source = sheet.Range["A1:A7"];
  IRange destination = sheet.Range["C3"];
  
  //Skip blanks while copying
  source.CopyTo(destination, ExcelCopyRangeOptions.All, true);

  //Saving the workbook to stream in XLSX format
  FileStream stream = new FileStream("SkipBlank.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs(stream);
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream = assembly.GetManifestResourceStream("CellManipulation.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet sheet = workbook.Worksheets[0];
  
  // Copy range as link from Range “A1” to “A5”.
  IRange source = sheet.Range["A1:A7"];
  IRange destination = sheet.Range["C3"];
  
  //Skip blanks while copying
  source.CopyTo(destination, ExcelCopyRangeOptions.All, true);

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);
  workbook.Close();

  //Save the document as file and view the saved document
  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.
  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("SkipBlank.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("SkipBlank.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

## Find and Replace

XlsIO provides following options to perform [find and replace](https://support.office.com/en-usa/article/Find-or-replace-text-and-numbers-on-a-worksheet-3a2c910f-01b9-4263-8db2-333dead6ae33) for text and numbers in Excel workbook or worksheet:

*	Search for data in formulas, values or comments.
*	Search for case-sensitive data and to match entire cell contents of the cell.

To know more about these options, please refer the [ExcelFindType](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelFindType.html), [ExcelFindOptions](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelFindOptions.html) in the API documentation section.

All the occurrences of a text in Excel worksheet can be found through [FindAll](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorksheet.html#Syncfusion_XlsIO_IWorksheet_FindAll_System_Boolean_) method. 

The following code illustrates how to find all the occurrences of text in a worksheet with different find options.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
  IWorksheet sheet = workbook.Worksheets[0];

  //Searches for the given string within the text of worksheet
  IRange[] result1 = sheet.FindAll("FindValue", ExcelFindType.Text);

  //Searches for the given string in formulas
  IRange[] result2 = sheet.FindAll("FindValue", ExcelFindType.Formula);

  //Searches for the given string in calculated value, number and text
  IRange[] result3 = sheet.FindAll("FindValue", ExcelFindType.Values);

  //Searches for the given string in comments
  IRange[] result4 = sheet.FindAll("FindValue", ExcelFindType.Comments);

  //Searches for the given string within the text of worksheet and case matched
  IRange[] result5 = sheet.FindAll("FindValue", ExcelFindType.Text, ExcelFindOptions.MatchCase);

  //Searches for the given string within the text of worksheet and the entire cell content matching to search text
  IRange[] result6 = sheet.FindAll("FindValue", ExcelFindType.Text, ExcelFindOptions.MatchEntireCellContent);

  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs("Find.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Searches for the given string within the text of worksheet
  Dim result1() As IRange = sheet.FindAll("FindValue", ExcelFindType.Text)

  'Searches for the given string in formulas
  Dim result2() As IRange = sheet.FindAll("FindValue", ExcelFindType.Formula)

  'Searches for the given string in calculated value, number and text
  Dim result3() As IRange = sheet.FindAll("FindValue", ExcelFindType.Values)

  'Searches for the given string in comments
  Dim result4() As IRange = sheet.FindAll("FindValue", ExcelFindType.Comments)

  'Searches for the given string within the text of worksheet and case matched
  Dim result5() As IRange = sheet.FindAll("FindValue", ExcelFindType.Text, ExcelFindOptions.MatchCase)

  'Searches for the given string within the text of worksheet and the entire cell content matching to search text
  Dim result6() As IRange = sheet.FindAll("FindValue", ExcelFindType.Text, ExcelFindOptions.MatchEntireCellContent)

  workbook.Version = ExcelVersion.Xlsx
  workbook.SaveAs("Find.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
ExcelEngine excelEngine = new ExcelEngine();
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  //Instantiates the File Picker
  FileOpenPicker openPicker = new FileOpenPicker();
  openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
  openPicker.FileTypeFilter.Add(".xlsx");
  openPicker.FileTypeFilter.Add(".xls");
  StorageFile file = await openPicker.PickSingleFileAsync();

  //Opens the workbook
  IWorkbook workbook = await application.Workbooks.OpenAsync(file);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Searches for the given string within the text of worksheet
  IRange[] result1 = worksheet.FindAll("FindValue", ExcelFindType.Text);

  //Searches for the given string in formulas
  IRange[] result2 = worksheet.FindAll("FindValue", ExcelFindType.Formula);

  //Searches for the given string in calculated value, number and text
  IRange[] result3 = worksheet.FindAll("FindValue", ExcelFindType.Values);

  //Searches for the given string in comments
  IRange[] result4 = worksheet.FindAll("FindValue", ExcelFindType.Comments);

  //Searches for the given string within the text of worksheet and case matched
  IRange[] result5 = worksheet.FindAll("FindValue", ExcelFindType.Text, ExcelFindOptions.MatchCase);

  //Searches for the given string within the text of worksheet and the entire cell content matching to search text
  IRange[] result6 = worksheet.FindAll("FindValue", ExcelFindType.Text, ExcelFindOptions.MatchEntireCellContent);

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Find";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  workbook.Version = ExcelVersion.Xlsx;
  await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Searches for the given string within the text of worksheet
  IRange[] result1 = worksheet.FindAll("FindValue", ExcelFindType.Text);

  //Searches for the given string in formulas
  IRange[] result2 = worksheet.FindAll("FindValue", ExcelFindType.Formula);

  //Searches for the given string in calculated value, number and text
  IRange[] result3 = worksheet.FindAll("FindValue", ExcelFindType.Values);

  //Searches for the given string in comments
  IRange[] result4 = worksheet.FindAll("FindValue", ExcelFindType.Comments);

  //Searches for the given string within the text of worksheet and case matched
  IRange[] result5 = worksheet.FindAll("FindValue", ExcelFindType.Text, ExcelFindOptions.MatchCase);

  //Searches for the given string within the text of worksheet and the entire cell content matching to search text
  IRange[] result6 = worksheet.FindAll("FindValue", ExcelFindType.Text, ExcelFindOptions.MatchEntireCellContent);

  //Saving the workbook as stream
  FileStream stream = new FileStream("Find.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream = assembly.GetManifestResourceStream("CellManipulation.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Searches for the given string within the text of worksheet
  IRange[] result1 = worksheet.FindAll("FindValue", ExcelFindType.Text);

  //Searches for the given string in formulas
  IRange[] result2 = worksheet.FindAll("FindValue", ExcelFindType.Formula);

  //Searches for the given string in calculated value, number and text
  IRange[] result3 = worksheet.FindAll("FindValue", ExcelFindType.Values);

  //Searches for the given string in comments
  IRange[] result4 = worksheet.FindAll("FindValue", ExcelFindType.Comments);

  //Searches for the given string within the text of worksheet and case matched
  IRange[] result5 = worksheet.FindAll("FindValue", ExcelFindType.Text, ExcelFindOptions.MatchCase);

  //Searches for the given string within the text of worksheet and the entire cell content matching to search text
  IRange[] result6 = worksheet.FindAll("FindValue", ExcelFindType.Text, ExcelFindOptions.MatchEntireCellContent);

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Find.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Find.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

It is possible to replace a text with another text with the help of [Replace](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorksheet.html#Syncfusion_XlsIO_IWorksheet_Replace_System_String_System_String_) method which searches for text which should be changed. A string can be replaced, with the data of various data types and data sources, such as data table, data column and array.

To know more about replace overloads, please refer [Replace](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorksheet.html#Syncfusion_XlsIO_IWorksheet_Replace_System_String_System_Data_DataColumn_System_Boolean_) in the API documentation section.

The following code example illustrates how to replace all occurrences of given string with various data.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
  IWorksheet sheet = workbook.Worksheets[0];

  //Replaces the given string with another string
  sheet.Replace("FindValue", "NewValue");

  //Replaces the given string with another string on match case
  sheet.Replace("FindValue", "NewValue", ExcelFindOptions.MatchCase);

  //Replaces the given string with another string matching entire cell content to the search word
  sheet.Replace("FindValue", "NewValue", ExcelFindOptions.MatchEntireCellContent);

  //Replaces the given string with DateTime value
  sheet.Replace("DateValue", DateTime.Now);

  //Replaces the given string with Array
  sheet.Replace("ArrayValue", new string[] { "ArrayValue1", "ArrayValue2", "ArrayValue3" }, true);

  //Replaces the given string with DataTable
  DataTable table = SampleDataTable();
  sheet.Replace("DataTable", table, true);

  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs("Replace.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Replaces the given string with another string
  sheet.Replace("FindValue", "NewValue")

  'Replaces the given string with another string on match case
  sheet.Replace("FindValue", "NewValue", ExcelFindOptions.MatchCase)

  'Replaces the given string with another string matching entire cell content to the search word
  sheet.Replace("FindValue", "NewValue", ExcelFindOptions.MatchEntireCellContent)

  'Replaces the given string with DateTime value
  sheet.Replace("DateValue", DateTime.Now)

  'Replaces the given string with Array
  sheet.Replace("ArrayValue", New String() {"ArrayValue1", "ArrayValue2", "ArrayValue3"}, True)

  'Replaces the given string with DataTable
  Dim table As DataTable = SampleDataTable()
  sheet.Replace("DataTable", table, True)

  workbook.Version = ExcelVersion.Xlsx
  workbook.SaveAs("Replace.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  //Instantiates the File Picker
  FileOpenPicker openPicker = new FileOpenPicker();
  openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
  openPicker.FileTypeFilter.Add(".xlsx");
  openPicker.FileTypeFilter.Add(".xls");
  StorageFile file = await openPicker.PickSingleFileAsync();

  //Opens the workbook
  IWorkbook workbook = await application.Workbooks.OpenAsync(file);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Replaces the given string with another string
  worksheet.Replace("FindValue", "NewValue");

  //Replaces the given string with another string on match case
  worksheet.Replace("FindValue", "NewValue", ExcelFindOptions.MatchCase);

  //Replaces the given string with another string matching entire cell content to the search word
  worksheet.Replace("FindValue", "NewValue", ExcelFindOptions.MatchEntireCellContent);

  //Replaces the given string with DateTime value
  worksheet.Replace("DateValue", DateTime.Now);

  //Replaces the given string with Array
  worksheet.Replace("ArrayValue", new string[] { "ArrayValue1", "ArrayValue2", "ArrayValue3" }, true);

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Replace";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  workbook.Version = ExcelVersion.Xlsx;
  await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Replaces the given string with another string
  worksheet.Replace("FindValue", "NewValue");

  //Replaces the given string with another string on match case
  worksheet.Replace("FindValue", "NewValue", ExcelFindOptions.MatchCase);

  //Replaces the given string with another string matching entire cell content to the search word
  worksheet.Replace("FindValue", "NewValue", ExcelFindOptions.MatchEntireCellContent);

  //Replaces the given string with DateTime value
  worksheet.Replace("DateValue", DateTime.Now);

  //Replaces the given string with Array
  worksheet.Replace("ArrayValue", new string[] { "ArrayValue1", "ArrayValue2", "ArrayValue3" }, true);

  //Saving the workbook as stream
  FileStream stream = new FileStream("Replace.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream = assembly.GetManifestResourceStream("CellsManipulation.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Replaces the given string with another string
  worksheet.Replace("FindValue", "NewValue");

  //Replaces the given string with another string on match case
  worksheet.Replace("FindValue", "NewValue", ExcelFindOptions.MatchCase);

  //Replaces the given string with another string matching entire cell content to the search word
  worksheet.Replace("FindValue", "NewValue", ExcelFindOptions.MatchEntireCellContent);

  //Replaces the given string with DateTime value
  worksheet.Replace("DateValue", DateTime.Now);

  //Replaces the given string with Array
  worksheet.Replace("ArrayValue", new string[] { "ArrayValue1", "ArrayValue2", "ArrayValue3" }, true);

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Replace.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Replace.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

## Data Sorting

A range of cells in Excel worksheet can be sorted based on data in one or more columns. Following types of sorting is supported in XlsIO:

* Based on Cell Values
* Based on Font Color
* Based on Cell Color

N> Currently XlsIO don’t support sorting based on cell icon, parsing and serialization of its sorting details.

### Based on Cell Values

The following code snippet explains how to sort a range of cells by values 

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
  IWorksheet sheet = workbook.Worksheets[0];

  //Creates the data sorter
  IDataSort sorter = workbook.CreateDataSorter();

  //Range to sort
  sorter.SortRange = sheet.Range["D3:D16"];

  //Adds the sort field with the column index, sort based on and order by attribute
  ISortField sortField = sorter.SortFields.Add(0, SortOn.Values, OrderBy.Ascending);

  //Adds another sort field
  ISortField sortField2 = sorter.SortFields.Add(1, SortOn.Values, OrderBy.Ascending);

  //Sort based on the sort Field attribute
  sorter.Sort();

  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs("Sort.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Creates the Data sorter
  Dim sorter As IDataSort = workbook.CreateDataSorter()

  'Specifies the sort range
  sorter.SortRange = sheet.Range("D3:D16")

  'Adds the sort field with column index, sort based on and order by attribute
  Dim sortField As ISortField = sorter.SortFields.Add(0, SortOn.Values, OrderBy.Ascending)

  'Adds the second sort field
  Dim sortField2 As ISortField = sorter.SortFields.Add(1, SortOn.Values, OrderBy.Ascending)

  'Sorts the data with the sort field attribute
  sorter.Sort()

  workbook.Version = ExcelVersion.Xlsx
  workbook.SaveAs("Sort.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  //Instantiates the File Picker
  FileOpenPicker openPicker = new FileOpenPicker();
  openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
  openPicker.FileTypeFilter.Add(".xlsx");
  openPicker.FileTypeFilter.Add(".xls");
  StorageFile file = await openPicker.PickSingleFileAsync();

  //Opens the workbook
  IWorkbook workbook = await application.Workbooks.OpenAsync(file);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Creates the data sorter
  IDataSort sorter = workbook.CreateDataSorter();

  //Range to sort
  sorter.SortRange = worksheet.Range["D3:D16"];

  //Adds the sort field with the column index, sort based on and order by attribute
  ISortField sortField = sorter.SortFields.Add(0, SortOn.Values, OrderBy.Ascending);

  //Adds another sort field
  ISortField sortField2 = sorter.SortFields.Add(1, SortOn.Values, OrderBy.Ascending);

  //Sort based on the sort Field attribute
  sorter.Sort();

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Sort";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  workbook.Version = ExcelVersion.Xlsx;
  await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream fileStream = new FileStream("SortingData.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Creates the data sorter
  IDataSort sorter = workbook.CreateDataSorter();

  //Range to sort
  sorter.SortRange = worksheet.Range["D3:D16"];

  //Adds the sort field with the column index, sort based on and order by attribute
  ISortField sortField = sorter.SortFields.Add(0, SortOn.Values, OrderBy.Ascending);

  //Adds another sort field
  ISortField sortField2 = sorter.SortFields.Add(1, SortOn.Values, OrderBy.Ascending);

  //Sort based on the sort Field attribute
  sorter.Sort();

  //Saving the workbook as stream
  FileStream stream = new FileStream("Sort.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream = assembly.GetManifestResourceStream("CellsManipulation.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Creates the data sorter
  IDataSort sorter = workbook.CreateDataSorter();

  //Range to sort
  sorter.SortRange = worksheet.Range["D3:D16"];

  //Adds the sort field with the column index, sort based on and order by attribute
  ISortField sortField = sorter.SortFields.Add(0, SortOn.Values, OrderBy.Ascending);

  //Adds another sort field
  ISortField sortField2 = sorter.SortFields.Add(1, SortOn.Values, OrderBy.Ascending);

  //Sort based on the sort Field attribute
  sorter.Sort();

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Sort.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sort.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to sort Excel data based on cell values in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Editing%20Excel%20cells/Sort%20On%20Cell%20Values).

### Based on Font Color

The following code snippet explains how to move a range of cells with the specified font color to either top or bottom of the sorting range.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
  IWorksheet sheet = workbook.Worksheets[0];

  //Creates the data sorter
  IDataSort sorter = workbook.CreateDataSorter();

  //Range to sort
  sorter.SortRange = sheet.Range["A2:D16"];

  //Creates the sort field with the column index, sort based on and order by attribute
  ISortField sortField1 = sorter.SortFields.Add(2, SortOn.FontColor, OrderBy.OnTop);

  //Specifies the color to sort the data
  sortField1.Color = Color.Red;

  //Creates another sort field with the column index, sort based on and order by attribute
  ISortField sortField2 = sorter.SortFields.Add(2, SortOn.FontColor, OrderBy.OnTop);

  //Specifies the color to sort the data
  sortField2.Color = Color.Green;

  //Sort based on the sort Field attribute
  sorter.Sort();

  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs("Sort.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Creates the Data sorter
  Dim sorter As IDataSort = workbook.CreateDataSorter()

  'Specifies the sort range
  sorter.SortRange = sheet.Range("A2:D16")

  'Adds the sort field with column index, sort based on and order by attribute
  Dim field1 As ISortField = sorter.SortFields.Add(2, SortOn.FontColor, OrderBy.OnTop)

  'Sorts the data based on this color
  field1.Color = Color.Red

  'Adds another sort field with column index, sort based on and order by attribute
  Dim field2 As ISortField = sorter.SortFields.Add(2, SortOn.FontColor, OrderBy.OnTop)

  'Sorts the data based on this color
  field2.Color = Color.Green

  'Sorts the data with the sort field attribute
  sorter.Sort()

  workbook.Version = ExcelVersion.Xlsx
  workbook.SaveAs("Sort.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  //Instantiates the File Picker
  FileOpenPicker openPicker = new FileOpenPicker();
  openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
  openPicker.FileTypeFilter.Add(".xlsx");
  openPicker.FileTypeFilter.Add(".xls");
  StorageFile file = await openPicker.PickSingleFileAsync();

  //Opens the workbook
  IWorkbook workbook = await application.Workbooks.OpenAsync(file);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Creates the data sorter
  IDataSort sorter = workbook.CreateDataSorter();

  //Range to sort
  sorter.SortRange = worksheet.Range["A2:D16"];

  //Creates the sort field with the column index, sort based on and order by attribute
  ISortField sortField1 = sorter.SortFields.Add(2, SortOn.FontColor, OrderBy.OnTop);

  //Specifies the color to sort the data
  sortField1.Color = Color.FromArgb(255, 255, 0, 0);

  //Creates another sort field with the column index, sort based on and order by attribute
  ISortField sortField2 = sorter.SortFields.Add(2, SortOn.FontColor, OrderBy.OnTop);

  //Specifies the color to sort the data
  sortField2.Color = Color.FromArgb(255, 0, 128, 0);

  //Sort based on the sort Field attribute
  sorter.Sort();

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Sort";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  workbook.Version = ExcelVersion.Xlsx;
  await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Creates the data sorter
  IDataSort sorter = workbook.CreateDataSorter();

  //Range to sort
  sorter.SortRange = worksheet.Range["A2:D16"];

  //Creates the sort field with the column index, sort based on and order by attribute
  ISortField sortField1 = sorter.SortFields.Add(2, SortOn.FontColor, OrderBy.OnTop);

  //Specifies the color to sort the data
  sortField1.Color = Color.Red;

  //Creates another sort field with the column index, sort based on and order by attribute
  ISortField sortField2 = sorter.SortFields.Add(2, SortOn.FontColor, OrderBy.OnTop);

  //Specifies the color to sort the data
  sortField2.Color = Color.Green;

  //Sort based on the sort Field attribute
  sorter.Sort();

  //Saving the workbook as stream
  FileStream stream = new FileStream("Sort.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream = assembly.GetManifestResourceStream("CellsManipulation.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Creates the data sorter
  IDataSort sorter = workbook.CreateDataSorter();

  //Range to sort
  sorter.SortRange = worksheet.Range["A2:D16"];

  //Creates the sort field with the column index, sort based on and order by attribute
  ISortField sortField1 = sorter.SortFields.Add(2, SortOn.FontColor, OrderBy.OnTop);

  //Specifies the color to sort the data
  sortField1.Color = Syncfusion.Drawing.Color.Red;

  //Creates another sort field with the column index, sort based on and order by attribute
  ISortField sortField2 = sorter.SortFields.Add(2, SortOn.FontColor, OrderBy.OnTop);

  //Specifies the color to sort the data
  sortField2.Color = Syncfusion.Drawing.Color.Green;

  //Sort based on the sort Field attribute
  sorter.Sort();

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Sort.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sort.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to sort Excel data based on font color in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Editing%20Excel%20cells/Sort%20on%20Font%20Color).

### Based on Cell Color

The following code snippet explains how to move a range of cells with the specified cell background color to either top or bottom of the sorting range.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
  IWorksheet sheet = workbook.Worksheets[0];

  //Creates the data sorter
  IDataSort sorter = workbook.CreateDataSorter();

  //Range to sort
  sorter.SortRange = sheet.Range["A2:D16"];

  //Creates the sort field with the column index, sort based on and order by attribute
  ISortField sortField1 = sorter.SortFields.Add(2, SortOn.CellColor, OrderBy.OnTop);

  //Specifies the color to sort the data
  sortField1.Color = Color.Red;

  //Creates the sort field with the column index, sort based on and order by attribute
  ISortField sortField2 = sorter.SortFields.Add(2, SortOn.CellColor, OrderBy.OnTop);

  //Specifies the color to sort the data
  sortField2.Color = Color.Green;

  //Sort based on the sort field attribute
  sorter.Sort();

  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs("Sort.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
  Dim sheet As IWorksheet = workbook.Worksheets(0)
  Dim sorter As IDataSort = workbook.CreateDataSorter()

  'Specifies the sort range.
  sorter.SortRange = sheet.Range("A2:D16")

  'Adds the sort field with column index, sort based on and order by attribute
  Dim field1 As ISortField = sorter.SortFields.Add(2, SortOn.CellColor, OrderBy.OnTop)

  'Sorts the data based on this color
  field1.Color = Color.Red

  'Adds the sort field with column index, sort based on and order by attribute
  Dim field2 As ISortField = sorter.SortFields.Add(2, SortOn.CellColor, OrderBy.OnTop)

  'Sorts the data based on this color
  field2.Color = Color.Green

  'Sorts the data with the sort field attribute
  sorter.Sort()

  workbook.Version = ExcelVersion.Xlsx
  workbook.SaveAs("Sort.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  //Instantiates the File Picker
  FileOpenPicker openPicker = new FileOpenPicker();
  openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
  openPicker.FileTypeFilter.Add(".xlsx");
  openPicker.FileTypeFilter.Add(".xls");
  StorageFile file = await openPicker.PickSingleFileAsync();

  //Opens the workbook
  IWorkbook workbook = await application.Workbooks.OpenAsync(file);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Creates the data sorter
  IDataSort sorter = workbook.CreateDataSorter();

  //Range to sort
  sorter.SortRange = worksheet.Range["A2:D16"];

  //Creates the sort field with the column index, sort based on and order by attribute
  ISortField sortField1 = sorter.SortFields.Add(2, SortOn.CellColor, OrderBy.OnTop);

  //Specifies the color to sort the data
  sortField1.Color = Color.FromArgb(255, 255, 0, 0);

  //Creates another sort field with the column index, sort based on and order by attribute
  ISortField sortField2 = sorter.SortFields.Add(2, SortOn.CellColor, OrderBy.OnTop);

  //Specifies the color to sort the data
  sortField2.Color = Color.FromArgb(255, 0, 128, 0);

  //Sort based on the sort Field attribute
  sorter.Sort();

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Sort";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  workbook.Version = ExcelVersion.Xlsx;
  await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Creates the data sorter
  IDataSort sorter = workbook.CreateDataSorter();

  //Range to sort
  sorter.SortRange = worksheet.Range["A2:D16"];

  //Creates the sort field with the column index, sort based on and order by attribute
  ISortField sortField1 = sorter.SortFields.Add(2, SortOn.CellColor, OrderBy.OnTop);

  //Specifies the color to sort the data
  sortField1.Color = Color.Red;

  //Creates another sort field with the column index, sort based on and order by attribute
  ISortField sortField2 = sorter.SortFields.Add(2, SortOn.CellColor, OrderBy.OnTop);

  //Specifies the color to sort the data
  sortField2.Color = Color.Green;

  //Sort based on the sort Field attribute
  sorter.Sort();

  //Saving the workbook as stream
  FileStream stream = new FileStream("Sort.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream = assembly.GetManifestResourceStream("CellsManipulation.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Creates the data sorter
  IDataSort sorter = workbook.CreateDataSorter();

  //Range to sort
  sorter.SortRange = worksheet.Range["A2:D16"];

  //Creates the sort field with the column index, sort based on and order by attribute
  ISortField sortField1 = sorter.SortFields.Add(2, SortOn.CellColor, OrderBy.OnTop);

  //Specifies the color to sort the data
  sortField1.Color = Syncfusion.Drawing.Color.Red;

  //Creates another sort field with the column index, sort based on and order by attribute
  ISortField sortField2 = sorter.SortFields.Add(2, SortOn.CellColor, OrderBy.OnTop);

  //Specifies the color to sort the data
  sortField2.Color = Syncfusion.Drawing.Color.Green;

  //Sort based on the sort Field attribute
  sorter.Sort();

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Sort.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sort.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to sort Excel data based on cell color in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Editing%20Excel%20cells/Sort%20On%20Cell%20Color).

## Data Filtering 

Using [AutoFilters](https://support.office.com/en-US/article/Filter-data-in-a-range-or-table-01832226-31b5-4568-8806-38c37dcc180e), data can be filtered to enable quick and easy way to find and work with a subset of data in a range of cells. When the data is filtered, entire rows are hidden if values in one or more columns does not meet the filtering criteria. The following are the types of filters that can be used in XlsIO.

* Custom Filter (Conditional)
* Combination Filter (Text and DateTime filter)
* Dynamic Filter
* Color Filter
* Icon Filter
* Advanced Filter

### Applying Filter

The following code illustrates how to apply simple auto filters.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
  IWorksheet sheet = workbook.Worksheets[0];

  //Creating an AutoFilter in the first worksheet. Specifying the AutoFilter range. 
  sheet.AutoFilters.FilterRange = sheet.Range["A1:K180"];

  //Column index to which AutoFilter must be applied
  IAutoFilter filter = sheet.AutoFilters[0];

  //To apply Top10Number filter, IsTop and IsTop10 must be enabled
  filter.IsTop = true;
  filter.IsTop10 = true;

  //Setting Top10 filter with number of cell to be filtered from top
  filter.Top10Number = 5;

  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs("Filter.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Creating an AutoFilter in the first worksheet. Specifying the AutoFilter range. 
  sheet.AutoFilters.FilterRange = sheet.Range("A1:K180")

  'Column index to which AutoFilter must be applied.
  Dim filter As IAutoFilter = sheet.AutoFilters(0)

  'To apply Top10Number filter, IsTop and IsTop10 must be enabled.
  filter.IsTop = True
  filter.IsTop10 = True

  'Setting Top10 filter with number of cell to be filtered from top
  filter.Top10Number = 5

  workbook.Version = ExcelVersion.Xlsx
  workbook.SaveAs("Filter.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  //Instantiates the File Picker
  FileOpenPicker openPicker = new FileOpenPicker();
  openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
  openPicker.FileTypeFilter.Add(".xlsx");
  openPicker.FileTypeFilter.Add(".xls");
  StorageFile file = await openPicker.PickSingleFileAsync();

  //Opens the workbook
  IWorkbook workbook = await application.Workbooks.OpenAsync(file);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Creating an AutoFilter in the first worksheet. Specifying the AutoFilter range
  worksheet.AutoFilters.FilterRange = worksheet.Range["A1:K180"];

  //Column index to which AutoFilter must be applied
  IAutoFilter filter = worksheet.AutoFilters[0];

  //To apply Top10Number filter, IsTop and IsTop10 must be enabled
  filter.IsTop = true;
  filter.IsTop10 = true;

  //Setting Top10 filter with number of cell to be filtered from top
  filter.Top10Number = 5;

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Filter";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  workbook.Version = ExcelVersion.Xlsx;
  await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Creating an AutoFilter in the first worksheet. Specifying the AutoFilter range
  worksheet.AutoFilters.FilterRange = worksheet.Range["A1:K180"];

  //Column index to which AutoFilter must be applied
  IAutoFilter filter = worksheet.AutoFilters[0];

  //To apply Top10Number filter, IsTop and IsTop10 must be enabled
  filter.IsTop = true;
  filter.IsTop10 = true;

  //Setting Top10 filter with number of cell to be filtered from top
  filter.Top10Number = 5;

  //Saving the workbook as stream
  FileStream stream = new FileStream("Filter.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream = assembly.GetManifestResourceStream("CellsManipulation.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Creating an AutoFilter in the first worksheet. Specifying the AutoFilter range
  worksheet.AutoFilters.FilterRange = worksheet.Range["A1:K180"];

  //Column index to which AutoFilter must be applied
  IAutoFilter filter = worksheet.AutoFilters[0];

  //To apply Top10Number filter, IsTop and IsTop10 must be enabled
  filter.IsTop = true;
  filter.IsTop10 = true;

  //Setting Top10 filter with number of cell to be filtered from top
  filter.Top10Number = 5;

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Filter.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Filter.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to apply filter on Excel data in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Editing%20Excel%20cells/Filter).

### Custom Filter

Following code snippet illustrates how to apply custom filter, based on first and second condition.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
  IWorksheet sheet = workbook.Worksheets[0];

  //Creating an AutoFilter in the first worksheet. Specifying the AutoFilter range
  sheet.AutoFilters.FilterRange = sheet.Range["A1:B323"];
  IAutoFilter filter = sheet.AutoFilters[1];

  //Specifying first condition
  IAutoFilterCondition firstCondition = filter.FirstCondition;
  firstCondition.ConditionOperator = ExcelFilterCondition.Greater;
  firstCondition.Double = 100;

  //Specifying second condition
  IAutoFilterCondition secondCondition = filter.SecondCondition;
  secondCondition.ConditionOperator = ExcelFilterCondition.Less;
  secondCondition.Double = 200;

  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs("Filter.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Creating an AutoFilter in the first worksheet. Specifying the AutoFilter range.
  sheet.AutoFilters.FilterRange = sheet.Range("A1:B323")
  Dim filter As IAutoFilter = sheet.AutoFilters(1)

  'Specifying first condition.
  Dim firstCondition As IAutoFilterCondition = filter.FirstCondition
  firstCondition.ConditionOperator = ExcelFilterCondition.Greater
  firstCondition.Double = 100

  'Specifying second condition.
  Dim secondCondition As IAutoFilterCondition = filter.SecondCondition
  secondCondition.ConditionOperator = ExcelFilterCondition.Less
  secondCondition.Double = 200

  workbook.Version = ExcelVersion.Xlsx
  workbook.SaveAs("Filter.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  //Instantiates the File Picker
  FileOpenPicker openPicker = new FileOpenPicker();
  openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
  openPicker.FileTypeFilter.Add(".xlsx");
  openPicker.FileTypeFilter.Add(".xls");
  StorageFile file = await openPicker.PickSingleFileAsync();

  //Opens the workbook
  IWorkbook workbook = await application.Workbooks.OpenAsync(file);
  IWorksheet sheet = workbook.Worksheets[0];

  //Creating an AutoFilter in the first worksheet. Specifying the AutoFilter range
  sheet.AutoFilters.FilterRange = sheet.Range["A1:B323"];
  IAutoFilter filter = sheet.AutoFilters[1];

  //Specifying first condition
  IAutoFilterCondition firstCondition = filter.FirstCondition;
  firstCondition.ConditionOperator = ExcelFilterCondition.Greater;
  firstCondition.Double = 100;

  //Specifying second condition
  IAutoFilterCondition secondCondition = filter.SecondCondition;
  secondCondition.ConditionOperator = ExcelFilterCondition.Less;
  secondCondition.Double = 200;

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Filter";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  workbook.Version = ExcelVersion.Xlsx;
  await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream inputStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet sheet = workbook.Worksheets[0];

  //Creating an AutoFilter in the first worksheet. Specifying the AutoFilter range
  sheet.AutoFilters.FilterRange = sheet.Range["A1:B323"];
  IAutoFilter filter = sheet.AutoFilters[1];

  //Specifying first condition
  IAutoFilterCondition firstCondition = filter.FirstCondition;
  firstCondition.ConditionOperator = ExcelFilterCondition.Greater;
  firstCondition.Double = 100;

  //Specifying second condition
  IAutoFilterCondition secondCondition = filter.SecondCondition;
  secondCondition.ConditionOperator = ExcelFilterCondition.Less;
  secondCondition.Double = 200;

  //Saving the workbook as stream
  FileStream file = new FileStream("Filter.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs(file);
  file.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream = assembly.GetManifestResourceStream("CellsManipulation.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet sheet = workbook.Worksheets[0];

  //Creating an AutoFilter in the first worksheet. Specifying the AutoFilter range
  sheet.AutoFilters.FilterRange = sheet.Range["A1:B323"];
  IAutoFilter filter = sheet.AutoFilters[1];

  //Specifying first condition
  IAutoFilterCondition firstCondition = filter.FirstCondition;
  firstCondition.ConditionOperator = ExcelFilterCondition.Greater;
  firstCondition.Double = 100;

  //Specifying second condition
  IAutoFilterCondition secondCondition = filter.SecondCondition;
  secondCondition.ConditionOperator = ExcelFilterCondition.Less;
  secondCondition.Double = 200;

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Filter.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Filter.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to apply custom filter on Excel data in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Editing%20Excel%20cells/Custom%20Filter).

### Combination Filter

This filter contains both Text filter and DateTime filter. It filters the data based on multiple criteria. Following code snippet illustrates how to apply combination filter with multiple of Text filter and DateTime filter.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
  IWorksheet sheet = workbook.Worksheets[0];

  //Creating an AutoFilter in the first worksheet. Specifying the AutoFilter range
  sheet.AutoFilters.FilterRange = sheet.Range["A1:K180"];

  //Column index to which AutoFilter must be applied
  IAutoFilter filter = sheet.AutoFilters[2];

  //Applying Text filter to filter multiple text to get filter
  filter.AddTextFilter(new string[] { "London", "Paris", "New York City" });

  //Applying DateTime filter to filter the date based on DateTimeGroupingType
  filter.AddDateFilter(new DateTime(2013, 1, 29, 0, 0, 0), DateTimeGroupingType.day);
  filter.AddDateFilter(2014, 12, 2, 10, 30, 0, DateTimeGroupingType.minute);

  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs("Filter.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Creating an AutoFilter in the first worksheet. Specifying the AutoFilter range
  sheet.AutoFilters.FilterRange = sheet.Range("A1:K180")

  'Column index to which AutoFilter must be applied
  Dim filter As IAutoFilter = sheet.AutoFilters(2)

  'Applying Text filter to filter multiple text to get filter
  filter.AddTextFilter(New String() {"London", "Paris", "New York City"})

  'Applying DateTime filter to filter the date based on DateTimeGroupingType
  filter.AddDateFilter(New DateTime(2013, 1, 29, 0, 0, 0), DateTimeGroupingType.day)
  filter.AddDateFilter(2014, 12, 2, 10, 30, 0, DateTimeGroupingType.minute)

  workbook.Version = ExcelVersion.Xlsx
  workbook.SaveAs("Filter.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  //Instantiates the File Picker
  FileOpenPicker openPicker = new FileOpenPicker();
  openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
  openPicker.FileTypeFilter.Add(".xlsx");
  openPicker.FileTypeFilter.Add(".xls");
  StorageFile file = await openPicker.PickSingleFileAsync();

  //Opens the workbook
  IWorkbook workbook = await application.Workbooks.OpenAsync(file);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Creating an AutoFilter in the first worksheet. Specifying the AutoFilter range. 
  worksheet.AutoFilters.FilterRange = worksheet.Range["A1:K180"];

  //Column index to which AutoFilter must be applied.
  IAutoFilter filter = worksheet.AutoFilters[2];

  //Applying Text filter to filter multiple text to get filter.
  filter.AddTextFilter(new string[] { "London", "Paris", "New York City" });

  //Applying DateTime filter to filter the date based on DateTimeGroupingType.
  filter.AddDateFilter(new DateTime(2013, 1, 29, 0, 0, 0), DateTimeGroupingType.day);
  filter.AddDateFilter(2014, 12, 2, 10, 30, 0, DateTimeGroupingType.minute);

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Filter";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  workbook.Version = ExcelVersion.Xlsx;
  await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Creating an AutoFilter in the first worksheet. Specifying the AutoFilter range. 
  worksheet.AutoFilters.FilterRange = worksheet.Range["A1:K180"];

  //Column index to which AutoFilter must be applied.
  IAutoFilter filter = worksheet.AutoFilters[2];

  //Applying Text filter to filter multiple text to get filter.
  filter.AddTextFilter(new string[] { "London", "Paris", "New York City" });

  //Applying DateTime filter to filter the date based on DateTimeGroupingType.
  filter.AddDateFilter(new DateTime(2013, 1, 29, 0, 0, 0), DateTimeGroupingType.day);
  filter.AddDateFilter(2014, 12, 2, 10, 30, 0, DateTimeGroupingType.minute);

  //Saving the workbook as stream
  FileStream stream = new FileStream("Filter.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream = assembly.GetManifestResourceStream("CellsManipulation.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Creating an AutoFilter in the first worksheet. Specifying the AutoFilter range. 
  worksheet.AutoFilters.FilterRange = worksheet.Range["A1:K180"];

  //Column index to which AutoFilter must be applied.
  IAutoFilter filter = worksheet.AutoFilters[2];

  //Applying Text filter to filter multiple text to get filter.
  filter.AddTextFilter(new string[] { "London", "Paris", "New York City" });

  //Applying DateTime filter to filter the date based on DateTimeGroupingType.
  filter.AddDateFilter(new DateTime(2013, 1, 29, 0, 0, 0), DateTimeGroupingType.day);
  filter.AddDateFilter(2014, 12, 2, 10, 30, 0, DateTimeGroupingType.minute);

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Filter.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Filter.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to apply combination filter on Excel data in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Editing%20Excel%20cells/Combination%20Filter).

### Dynamic Filter

Dynamic filter is a relative date filter, which filters data based on [DynamicFilterType](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.DynamicFilterType.html) enumeration. Following code snippet illustrates how to apply Dynamic filter.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
  IWorksheet sheet = workbook.Worksheets[0];

  //Creating an AutoFilter in the first worksheet. Specifying the AutoFilter range.
  sheet.AutoFilters.FilterRange = sheet.Range["A1:K180"];

  //Column index to which AutoFilter must be applied.
  IAutoFilter filter = sheet.AutoFilters[3];

  //Applying dynamic filter to filter the date based on DynamicFilterType.
  filter.AddDynamicFilter(DynamicFilterType.NextQuarter);

  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs("Filter.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Creating an AutoFilter in the first worksheet. Specifying the AutoFilter range.
  sheet.AutoFilters.FilterRange = sheet.Range("A1:K180")

  'Column index to which AutoFilter must be applied.
  Dim filter As IAutoFilter = sheet.AutoFilters(3)

  'Applying dynamic filter to filter the date based on DynamicFilterType.
  filter.AddDynamicFilter(DynamicFilterType.NextQuarter)

  workbook.Version = ExcelVersion.Xlsx
  workbook.SaveAs("Filter.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  //Instantiates the File Picker
  FileOpenPicker openPicker = new FileOpenPicker();
  openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
  openPicker.FileTypeFilter.Add(".xlsx");
  openPicker.FileTypeFilter.Add(".xls");
  StorageFile file = await openPicker.PickSingleFileAsync();

  //Opens the workbook
  IWorkbook workbook = await application.Workbooks.OpenAsync(file);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Creating an AutoFilter in the first worksheet. Specifying the AutoFilter range.
  worksheet.AutoFilters.FilterRange = worksheet.Range["A1:K180"];

  //Column index to which AutoFilter must be applied.
  IAutoFilter filter = worksheet.AutoFilters[3];

  //Applying dynamic filter to filter the date based on DynamicFilterType.
  filter.AddDynamicFilter(DynamicFilterType.NextQuarter);

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Filter";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  workbook.Version = ExcelVersion.Xlsx;
  await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Creating an AutoFilter in the first worksheet. Specifying the AutoFilter range.
  worksheet.AutoFilters.FilterRange = worksheet.Range["A1:K180"];

  //Column index to which AutoFilter must be applied.
  IAutoFilter filter = worksheet.AutoFilters[3];

  //Applying dynamic filter to filter the date based on DynamicFilterType.
  filter.AddDynamicFilter(DynamicFilterType.NextQuarter);

  //Saving the workbook as stream
  FileStream stream = new FileStream("Filter.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream = assembly.GetManifestResourceStream("CellsManipulation.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Creating an AutoFilter in the first worksheet. Specifying the AutoFilter range.
  worksheet.AutoFilters.FilterRange = worksheet.Range["A1:K180"];

  //Column index to which AutoFilter must be applied.
  IAutoFilter filter = worksheet.AutoFilters[3];

  //Applying dynamic filter to filter the date based on DynamicFilterType.
  filter.AddDynamicFilter(DynamicFilterType.NextQuarter);

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Filter.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Filter.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to apply dynamic filter on Excel data in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Editing%20Excel%20cells/Dynamic%20Filter).

### Color Filter

Color Filter can be used to filter data based on the color applied to the cell or the color applied to the text in the cell. The following code snippet show how to apply Color Filter based on Cell Color (fill color applied to the cell).

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
  IWorksheet sheet = workbook.Worksheets[0];

  //Creating an AutoFilter in the first worksheet. Specifying the AutoFilter range.
  sheet.AutoFilters.FilterRange = sheet.Range["A1:K180"];

  //Column index to which AutoFilter must be applied.
  IAutoFilter filter = sheet.AutoFilters[3];

  //Applying color filter to filter based on Cell Color.
  filter.AddColorFilter(Color.Red, ExcelColorFilterType.CellColor);

  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs("Filter.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Creating an AutoFilter in the first worksheet. Specifying the AutoFilter range.
  sheet.AutoFilters.FilterRange = sheet.Range("A1:K180")

  'Column index to which AutoFilter must be applied.
  Dim filter As IAutoFilter = sheet.AutoFilters(3)

  'Applying color filter to filter based on Cell Color.
  filter.AddColorFilter(Color.Red, ExcelColorFilterType.CellColor)

  workbook.Version = ExcelVersion.Xlsx
  workbook.SaveAs("Filter.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  //Instantiates the File Picker
  FileOpenPicker openPicker = new FileOpenPicker();
  openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
  openPicker.FileTypeFilter.Add(".xlsx");
  openPicker.FileTypeFilter.Add(".xls");
  StorageFile file = await openPicker.PickSingleFileAsync();

  //Opens the workbook
  IWorkbook workbook = await application.Workbooks.OpenAsync(file);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Creating an AutoFilter in the first worksheet. Specifying the AutoFilter range.
  worksheet.AutoFilters.FilterRange = worksheet.Range["A1:K180"];

  //Column index to which AutoFilter must be applied.
  IAutoFilter filter = worksheet.AutoFilters[3];

  //Applying color filter to filter based on Cell Color.
  filter.AddColorFilter(Color.FromArgb(255, 255, 0, 0), ExcelColorFilterType.CellColor);

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Filter";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  workbook.Version = ExcelVersion.Xlsx;
  await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Creating an AutoFilter in the first worksheet. Specifying the AutoFilter range.
  worksheet.AutoFilters.FilterRange = worksheet.Range["A1:K180"];

  //Column index to which AutoFilter must be applied.
  IAutoFilter filter = worksheet.AutoFilters[3];

  //Applying color filter to filter based on Cell Color.
  filter.AddColorFilter(Color.Red, ExcelColorFilterType.CellColor);

  //Saving the workbook as stream
  FileStream stream = new FileStream("Filter.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream = assembly.GetManifestResourceStream("CellsManipulation.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Creating an AutoFilter in the first worksheet. Specifying the AutoFilter range.
  worksheet.AutoFilters.FilterRange = worksheet.Range["A1:K180"];

  //Column index to which AutoFilter must be applied.
  IAutoFilter filter = worksheet.AutoFilters[0];

  //Applying color filter to filter based on Cell Color.
  filter.AddColorFilter(Syncfusion.Drawing.Color.Red, ExcelColorFilterType.CellColor);

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Filter.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Filter.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to apply color filter on Excel data based on cell color in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Editing%20Excel%20cells/Cell%20Color%20Filter).

To filter cells based on Font color of the text inside cells just change the [ExcelColorFilterType](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelColorFilterType.html) to Font Color. The following snippet show how to filter the cells based on font color.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
  IWorksheet sheet = workbook.Worksheets[0];

  //Creating an AutoFilter in the first worksheet. Specifying the AutoFilter range.
  sheet.AutoFilters.FilterRange = sheet.Range["A1:K180"];

  //Column index to which AutoFilter must be applied.
  IAutoFilter filter = sheet.AutoFilters[3];

  //Applying color filter to filter based on Cell Color.
  filter.AddColorFilter(Color.Red, ExcelColorFilterType.FontColor);

  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs("Filter.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Creating an AutoFilter in the first worksheet. Specifying the AutoFilter range.
  sheet.AutoFilters.FilterRange = sheet.Range("A1:K180")

  'Column index to which AutoFilter must be applied.
  Dim filter As IAutoFilter = sheet.AutoFilters(3)

  'Applying color filter to filter based on Cell Color.
  filter.AddColorFilter(Color.Red, ExcelColorFilterType.FontColor)

  workbook.Version = ExcelVersion.Xlsx
  workbook.SaveAs("Filter.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  //Instantiates the File Picker
  FileOpenPicker openPicker = new FileOpenPicker();
  openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
  openPicker.FileTypeFilter.Add(".xlsx");
  openPicker.FileTypeFilter.Add(".xls");
  StorageFile file = await openPicker.PickSingleFileAsync();

  //Opens the workbook
  IWorkbook workbook = await application.Workbooks.OpenAsync(file);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Creating an AutoFilter in the first worksheet. Specifying the AutoFilter range.
  worksheet.AutoFilters.FilterRange = worksheet.Range["A1:K180"];

  //Column index to which AutoFilter must be applied.
  IAutoFilter filter = worksheet.AutoFilters[3];

  //Applying color filter to filter based on Cell Color.
  filter.AddColorFilter(Color.FromArgb(255, 255, 0, 0), ExcelColorFilterType.FontColor);

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Filter";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  workbook.Version = ExcelVersion.Xlsx;
  await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Creating an AutoFilter in the first worksheet. Specifying the AutoFilter range.
  worksheet.AutoFilters.FilterRange = worksheet.Range["A1:K180"];

  //Column index to which AutoFilter must be applied.
  IAutoFilter filter = worksheet.AutoFilters[3];

  //Applying color filter to filter based on Cell Color.
  filter.AddColorFilter(Color.Red, ExcelColorFilterType.FontColor);

  //Saving the workbook as stream
  FileStream stream = new FileStream("Filter.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream = assembly.GetManifestResourceStream("CellsManipulation.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Creating an AutoFilter in the first worksheet. Specifying the AutoFilter range.
  worksheet.AutoFilters.FilterRange = worksheet.Range["A1:K180"];

  //Column index to which AutoFilter must be applied.
  IAutoFilter filter = worksheet.AutoFilters[0];

  //Applying color filter to filter based on Cell Color.
  filter.AddColorFilter(Syncfusion.Drawing.Color.Red, ExcelColorFilterType.FontColor);

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Filter.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Filter.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to apply color filter on Excel data based on font color in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Editing%20Excel%20cells/Font%20Color%20Filter).

### Icon Filter

Icon filter can be used to filter data that has conditional formatting with Icon Sets applied. Applying Icon Sets for numeric data adds icons to each cell based on the value present in that cell. Using Icon Filter, the data that has only a specific Icon in it can be filtered easily.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
  IWorksheet sheet = workbook.Worksheets[0];

  //Creating an AutoFilter in the first worksheet. Specifying the AutoFilter range.
  sheet.AutoFilters.FilterRange = sheet.Range["A1:K180"];

  //Column index to which AutoFilter must be applied.
  IAutoFilter filter = sheet.AutoFilters[3];

  //Applying Icon filter to filter based on applied icon set.
  filter.AddIconFilter(ExcelIconSetType.ThreeFlags, 2);

  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs("Filter.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Creating an AutoFilter in the first worksheet. Specifying the AutoFilter range.
  sheet.AutoFilters.FilterRange = sheet.Range("A1:K180")

  'Column index to which AutoFilter must be applied.
  Dim filter As IAutoFilter = sheet.AutoFilters(3)

  'Applying Icon filter to filter based on applied icon set.
  filter.AddIconFilter(ExcelIconSetType.ThreeFlags, 2)

  workbook.Version = ExcelVersion.Xlsx
  workbook.SaveAs("Filter.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  //Instantiates the File Picker
  FileOpenPicker openPicker = new FileOpenPicker();
  openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
  openPicker.FileTypeFilter.Add(".xlsx");
  openPicker.FileTypeFilter.Add(".xls");
  StorageFile file = await openPicker.PickSingleFileAsync();

  //Opens the workbook
  IWorkbook workbook = await application.Workbooks.OpenAsync(file);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Creating an AutoFilter in the first worksheet. Specifying the AutoFilter range.
  worksheet.AutoFilters.FilterRange = worksheet.Range["A1:K180"];

  //Column index to which AutoFilter must be applied.
  IAutoFilter filter = worksheet.AutoFilters[3];

  //Applying Icon filter to filter based on applied icon set.
  filter.AddIconFilter(ExcelIconSetType.ThreeFlags, 2);

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Filter";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  workbook.Version = ExcelVersion.Xlsx;
  await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Creating an AutoFilter in the first worksheet. Specifying the AutoFilter range.
  worksheet.AutoFilters.FilterRange = worksheet.Range["A1:K180"];

  //Column index to which AutoFilter must be applied.
  IAutoFilter filter = worksheet.AutoFilters[3];

  //Applying Icon filter to filter based on applied icon set.
  filter.AddIconFilter(ExcelIconSetType.ThreeFlags, 2);

  //Saving the workbook as stream
  FileStream stream = new FileStream("Filter.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream = assembly.GetManifestResourceStream("CellsManipulation.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Creating an AutoFilter in the first worksheet. Specifying the AutoFilter range.
  worksheet.AutoFilters.FilterRange = worksheet.Range["A1:K180"];

  //Column index to which AutoFilter must be applied.
  IAutoFilter filter = worksheet.AutoFilters[3];

  //Applying Icon filter to filter based on applied icon set.
  filter.AddIconFilter(ExcelIconSetType.ThreeFlags, 2);

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Filter.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Filter.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to apply icon filter on Excel data in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Editing%20Excel%20cells/Icon%20Filter).

### Advanced Filter

Advanced Filter can be used to perform more complex filtering other than basic filters. Data can be filtered with custom defined criteria range.

Advanced Filter support two types of filter action.

1. Filter In Place
2. Filter Copy

**Filter In Place**: Filter data in same location.
**Filter Copy**: Filter and copy data into new location within a worksheet.

Advanced Filter also provides an option to filter the unique records. This will remove the duplicate record from filtered data.

The following code illustrates how to apply Advanced Filter in worksheet.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  IWorkbook workbook = application.Workbooks.Open("InputData.xlsx");
  IWorksheet sheet = workbook.Worksheets[0];

  IRange filterRange = sheet.Range["A1:C6"];
  IRange criteriaRange = sheet.Range["A10:C12"];
  IRange copyToRange = sheet.Range["K5:N5"];

  //Apply the Advanced Filter with enable of unique value and copy to another place.
  sheet.AdvancedFilter(ExcelFilterAction.FilterCopy, filterRange, criteriaRange, copyToRange, true);

  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs("AdvancedFilter.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  Dim workbook As IWorkbook = application.Workbooks.Open("InputData.xlsx")
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  Dim filterRange As IRange = sheet.Range("A1:C6")
  Dim criteriaRange As IRange = sheet.Range("A10:C12")
  Dim copyToRange As IRange = sheet.Range("K5:N5")

  'Apply the Advanced filter with enable of unique value and copy to another place.
  sheet.AdvancedFilter(ExcelFilterAction.FilterCopy, filterRange, criteriaRange, copyToRange, True)

  workbook.Version = ExcelVersion.Xlsx
  workbook.SaveAs("AdvancedFilter.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  //Instantiates the File Picker
  FileOpenPicker openPicker = new FileOpenPicker();
  openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
  openPicker.FileTypeFilter.Add(".xlsx");
  openPicker.FileTypeFilter.Add(".xls");
  StorageFile file = await openPicker.PickSingleFileAsync();

  //Opens the workbook
  IWorkbook workbook = await application.Workbooks.OpenAsync(file);
  IWorksheet worksheet = workbook.Worksheets[0];

  IRange filterRange = worksheet.Range["A1:C6"];
  IRange criteriaRange = worksheet.Range["A10:C12"];
  IRange copyToRange = worksheet.Range["K5:N5"];

  //Apply the Advanced Filter with enable of unique value and copy to another place.
  worksheet.AdvancedFilter(ExcelFilterAction.FilterCopy, filterRange, criteriaRange, copyToRange, true);

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "AdvancedFilter";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  workbook.Version = ExcelVersion.Xlsx;
  await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream fileStream = new FileStream("InputData.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  IRange filterRange = worksheet.Range["A1:C6"];
  IRange criteriaRange = worksheet.Range["A10:C12"];
  IRange copyToRange = worksheet.Range["K5:N5"];

  //Apply the Advanced Filter with enable of unique value and copy to another place.
  worksheet.AdvancedFilter(ExcelFilterAction.FilterCopy, filterRange, criteriaRange, copyToRange, true);

  //Saving the workbook as stream
  FileStream stream = new FileStream("AdvancedFilter.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream = assembly.GetManifestResourceStream("CellsManipulation.InputData.xlsx");
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  IRange filterRange = worksheet.Range["A1:C6"];
  IRange criteriaRange = worksheet.Range["A10:C12"];
  IRange copyToRange = worksheet.Range["K5:N5"];

  //Apply the Advanced Filter with enable of unique value and copy to another place.
  worksheet.AdvancedFilter(ExcelFilterAction.FilterCopy, filterRange, criteriaRange, copyToRange, true);

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Filter.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Filter.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to apply advanced filter on Excel data in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Editing%20Excel%20cells/Advanced%20Filter).

### Accessing Filter

A filter and its criteria can be accessed based on its column index. Following code snippet illustrates how to access different types of filters using XlsIO.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);
  IWorksheet worksheet = workbook.Worksheets[0];

  //selecting the filter by column index
  IAutoFilter filter = worksheet.AutoFilters[0];

  switch (filter.FilterType)
  {
	case ExcelFilterType.CombinationFilter:
	  CombinationFilter filterItems = (filter.FilteredItems as CombinationFilter);
	  for (int index = 0; index < filterItems.Count; index++)
	  {
		if (filterItems[index].CombinationFilterType == ExcelCombinationFilterType.TextFilter)
		{
		  string textValue = (filterItems[index] as TextFilter).Text;
		}
		else
		{
		  DateTimeGroupingType groupType = (filterItems[index] as DateTimeFilter).GroupingType;
		}
	  }
	  break;

	case ExcelFilterType.DynamicFilter:
	  DynamicFilter dateFilter = (filter.FilteredItems as DynamicFilter);
	  DynamicFilterType dynamicFilterType = dateFilter.DateFilterType;
	  break;

	case ExcelFilterType.CustomFilter:
	  IAutoFilterCondition firstCondition = filter.FirstCondition;
	  ExcelFilterDataType types = firstCondition.DataType;
	  break;

	case ExcelFilterType.ColorFilter:
	  ColorFilter colorFilter = (filter.FilteredItems as ColorFilter);
	  Color color = colorFilter.Color;
	  ExcelColorFilterType filterType = colorFilter.ColorFilterType;
	  break;

	case ExcelFilterType.IconFilter:
	  IconFilter iconFilter = (filter.FilteredItems as IconFilter);
	  int iconId = iconFilter.IconId;
	  ExcelIconSetType iconSetType = iconFilter.IconSetType;
	  break;
  }

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'selecting the filter by column index
  Dim filter As IAutoFilter = worksheet.AutoFilters(0)

  Select Case filter.FilterType
    Case ExcelFilterType.CombinationFilter
	  Dim filterItems As CombinationFilter = TryCast(filter.FilteredItems, CombinationFilter)
	  For index As Integer = 0 To filterItems.Count - 1
		If filterItems(index).CombinationFilterType = ExcelCombinationFilterType.TextFilter Then
		  Dim textValue As String = TryCast(filterItems(index), TextFilter).Text
		Else
		  Dim groupType As DateTimeGroupingType = TryCast(filterItems(index), DateTimeFilter).GroupingType
		End If
	  Next
	  Exit Select

	Case ExcelFilterType.DynamicFilter
	  Dim dateFilter As DynamicFilter = TryCast(filter.FilteredItems, DynamicFilter)
	  Dim dynamicFilterType As DynamicFilterType = dateFilter.DateFilterType
	  Exit Select

	Case ExcelFilterType.CustomFilter
	  Dim firstCondition As IAutoFilterCondition = filter.FirstCondition
	  Dim types As ExcelFilterDataType = firstCondition.DataType
	  Exit Select

	Case ExcelFilterType.ColorFilter
	  Dim colorFilter As ColorFilter = TryCast(filter.FilteredItems, ColorFilter)
	  Dim color As Color = colorFilter.Color
	  Dim filterType As ExcelColorFilterType = colorFilter.ColorFilterType
	  Exit Select

	Case ExcelFilterType.IconFilter
	  Dim iconFilter As IconFilter = TryCast(filter.FilteredItems, IconFilter)
	  Dim iconId As Int32 = iconFilter.IconId
	  Dim iconSetType As ExcelIconSetType = iconFilter.IconSetType
	  Exit Select
  End Select

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;

  //Instantiates the File Picker
  FileOpenPicker openPicker = new FileOpenPicker();
  openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
  openPicker.FileTypeFilter.Add(".xlsx");
  openPicker.FileTypeFilter.Add(".xls");
  StorageFile file = await openPicker.PickSingleFileAsync();

  //Opens the workbook
  IWorkbook workbook = await application.Workbooks.OpenAsync(file);
  IWorksheet sheet = workbook.Worksheets[0];

  //selecting the filter by column index
  IAutoFilter filter = sheet.AutoFilters[0];

  switch (filter.FilterType)
  {
	case ExcelFilterType.CombinationFilter:
	  CombinationFilter filterItems = (filter.FilteredItems as CombinationFilter);
	  for (int index = 0; index < filterItems.Count; index++)
	  {
		if (filterItems[index].CombinationFilterType == ExcelCombinationFilterType.TextFilter)
		{
		  string textValue = (filterItems[index] as TextFilter).Text;
		}
		else
		{
		  DateTimeGroupingType groupType = (filterItems[index] as DateTimeFilter).GroupingType;
		}
	  }
	  break;

	case ExcelFilterType.DynamicFilter:
	  DynamicFilter dateFilter = (filter.FilteredItems as DynamicFilter);
	  DynamicFilterType dynamicFilterType = dateFilter.DateFilterType;
	  break;

	case ExcelFilterType.CustomFilter:
	  IAutoFilterCondition firstCondition = filter.FirstCondition;
	  ExcelFilterDataType types = firstCondition.DataType;
	  break;

	case ExcelFilterType.ColorFilter:
	  ColorFilter colorFilter = (filter.FilteredItems as ColorFilter);
	  Color color = colorFilter.Color;
	  ExcelColorFilterType filterType = colorFilter.ColorFilterType;
	  break;

	case ExcelFilterType.IconFilter:
	  IconFilter iconFilter = (filter.FilteredItems as IconFilter);
	  int iconId = iconFilter.IconId;
	  ExcelIconSetType iconSetType = iconFilter.IconSetType;
	  break;
  }

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
  FileStream inputStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet sheet = workbook.Worksheets[0];

  //selecting the filter by column index
  IAutoFilter filter = sheet.AutoFilters[0];

  switch (filter.FilterType)
  {
	case ExcelFilterType.CombinationFilter:
	  CombinationFilter filterItems = (filter.FilteredItems as CombinationFilter);
	  for (int index = 0; index < filterItems.Count; index++)
	  {
		if (filterItems[index].CombinationFilterType == ExcelCombinationFilterType.TextFilter)
		{
		  string textValue = (filterItems[index] as TextFilter).Text;
		}
		else
		{
		  DateTimeGroupingType groupType = (filterItems[index] as DateTimeFilter).GroupingType;
		}
	  }
	  break;

	case ExcelFilterType.DynamicFilter:
	  DynamicFilter dateFilter = (filter.FilteredItems as DynamicFilter);
	  DynamicFilterType dynamicFilterType = dateFilter.DateFilterType;
	  break;

	case ExcelFilterType.CustomFilter:
	  IAutoFilterCondition firstCondition = filter.FirstCondition;
	  ExcelFilterDataType types = firstCondition.DataType;
	  break;

	case ExcelFilterType.ColorFilter:
	  ColorFilter colorFilter = (filter.FilteredItems as ColorFilter);
	  Color color = colorFilter.Color;
	  ExcelColorFilterType filterType = colorFilter.ColorFilterType;
	  break;

	case ExcelFilterType.IconFilter:
	  IconFilter iconFilter = (filter.FilteredItems as IconFilter);
	  int iconId = iconFilter.IconId;
	  ExcelIconSetType iconSetType = iconFilter.IconSetType;
	  break;
  }

  //Saving the workbook as stream
  FileStream file = new FileStream("Output.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(file);
  file.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;

  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream = assembly.GetManifestResourceStream("CellsManipulation.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet sheet = workbook.Worksheets[0];

  //selecting the filter by column index
  IAutoFilter filter = sheet.AutoFilters[0];

  switch (filter.FilterType)
  {
	case ExcelFilterType.CombinationFilter:
	  CombinationFilter filterItems = (filter.FilteredItems as CombinationFilter);
	  for (int index = 0; index < filterItems.Count; index++)
	  {
		if (filterItems[index].CombinationFilterType == ExcelCombinationFilterType.TextFilter)
	    {
		  string textValue = (filterItems[index] as TextFilter).Text;
		}
		else
		{
		  DateTimeGroupingType groupType = (filterItems[index] as DateTimeFilter).GroupingType;
		}
	  }
	  break;

    case ExcelFilterType.DynamicFilter:
	  DynamicFilter dateFilter = (filter.FilteredItems as DynamicFilter);
	  DynamicFilterType dynamicFilterType = dateFilter.DateFilterType;
	  break;

	case ExcelFilterType.CustomFilter:
	  IAutoFilterCondition firstCondition = filter.FirstCondition;
	  ExcelFilterDataType types = firstCondition.DataType;
	  break;

	case ExcelFilterType.ColorFilter:
	  ColorFilter colorFilter = (filter.FilteredItems as ColorFilter);
	  Syncfusion.Drawing.Color color = colorFilter.Color;
	  ExcelColorFilterType filterType = colorFilter.ColorFilterType;
	  break;

    case ExcelFilterType.IconFilter:
	  IconFilter iconFilter = (filter.FilteredItems as IconFilter);
	  int iconId = iconFilter.IconId;
	  ExcelIconSetType iconSetType = iconFilter.IconSetType;
	  break;
  }

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Output.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to access filters from Excel worksheet in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Editing%20Excel%20cells/Accessing%20Filter).

## Hyperlinks

Hyperlink can be created in a workbook to provide quick access to web pages, places in your document and files. Hyperlink may target to any one of the following

* Worksheet range
* Web URL
* E-mail
* External files

The following code example illustrates how to insert various hyperlinks.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Creating a Hyperlink for a Website
  IHyperLink hyperlink = sheet.HyperLinks.Add(sheet.Range["C5"]);
  hyperlink.Type = ExcelHyperLinkType.Url;
  hyperlink.Address = "http://www.syncfusion.com";
  hyperlink.ScreenTip = "To know more about Syncfusion products, go through this link.";

  //Creating a Hyperlink for e-mail
  IHyperLink hyperlink1 = sheet.HyperLinks.Add(sheet.Range["C7"]);
  hyperlink1.Type = ExcelHyperLinkType.Url;
  hyperlink1.Address = "mailto:Username@syncfusion.com";
  hyperlink1.ScreenTip = "Send Mail";

  //Creating a Hyperlink for Opening Files using type as File
  IHyperLink hyperlink2 = sheet.HyperLinks.Add(sheet.Range["C9"]);
  hyperlink2.Type = ExcelHyperLinkType.File;
  hyperlink2.Address = @"C:\Program files";
  hyperlink2.ScreenTip = "File path";
  hyperlink2.TextToDisplay = "Hyperlink for files using File as type";

  //Creating a Hyperlink for Opening Files using type as Unc
  IHyperLink hyperlink3 = sheet.HyperLinks.Add(sheet.Range["C11"]);
  hyperlink3.Type = ExcelHyperLinkType.Unc;
  hyperlink3.Address = @"C:\Documents and Settings";
  hyperlink3.ScreenTip = "Click here for files";
  hyperlink3.TextToDisplay = "Hyperlink for files using Unc as type";

  //Creating a Hyperlink to another cell using type as Workbook
  IHyperLink hyperlink4 = sheet.HyperLinks.Add(sheet.Range["C13"]);
  hyperlink4.Type = ExcelHyperLinkType.Workbook;
  hyperlink4.Address = "Sheet1!A15";
  hyperlink4.ScreenTip = "Click here";
  hyperlink4.TextToDisplay = "Hyperlink to cell A15";

  workbook.SaveAs("Hyperlink.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Creating a Hyperlink for a Website
  Dim hyperlink As IHyperLink = sheet.HyperLinks.Add(sheet.Range("C5"))
  hyperlink.Type = ExcelHyperLinkType.Url
  hyperlink.Address = "http://www.Syncfusion.com"
  hyperlink.ScreenTip = "To know more about Syncfusion products, go through this link."

  'Creating a Hyperlink for e-mail
  Dim hyperlink1 As IHyperLink = sheet.HyperLinks.Add(sheet.Range("C7"))
  hyperlink1.Type = ExcelHyperLinkType.Url
  hyperlink1.Address = "mailto:Username@syncfusion.com"
  hyperlink1.ScreenTip = "Send Mail"

  'Creating a Hyperlink for Opening Files using type as File
  Dim hyperlink2 As IHyperLink = sheet.HyperLinks.Add(sheet.Range("C9"))
  hyperlink2.Type = ExcelHyperLinkType.File
  hyperlink2.Address = "C:\Program files"
  hyperlink2.ScreenTip = "File path"
  hyperlink2.TextToDisplay = "Hyperlink for files using File as type"

  'Creating a Hyperlink for Opening Files using type as Unc
  Dim hyperlink3 As IHyperLink = sheet.HyperLinks.Add(sheet.Range("C11"))
  hyperlink3.Type = ExcelHyperLinkType.Unc
  hyperlink3.Address = "C:\Documents and Settings"
  hyperlink3.ScreenTip = "Click here for files"
  hyperlink3.TextToDisplay = "Hyperlink for files using Unc as type"

  'Creating a Hyperlink to another cell using type as Workbook
  Dim hyperlink4 As IHyperLink = sheet.HyperLinks.Add(sheet.Range("C13"))
  hyperlink4.Type = ExcelHyperLinkType.Workbook
  hyperlink4.Address = "Sheet1!A15"
  hyperlink4.ScreenTip = "Click here"
  hyperlink4.TextToDisplay = "Hyperlink to cell A15"

  workbook.SaveAs("Hyperlink.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Creating a Hyperlink for a Website
  IHyperLink hyperlink = sheet.HyperLinks.Add(sheet.Range["C5"]);
  hyperlink.Type = ExcelHyperLinkType.Url;
  hyperlink.Address = "http://www.syncfusion.com";
  hyperlink.ScreenTip = "To know more about Syncfusion products, go through this link.";

  //Creating a Hyperlink for e-mail
  IHyperLink hyperlink1 = sheet.HyperLinks.Add(sheet.Range["C7"]);
  hyperlink1.Type = ExcelHyperLinkType.Url;
  hyperlink1.Address = "mailto:Username@syncfusion.com";
  hyperlink1.ScreenTip = "Send Mail";

  //Creating a Hyperlink for Opening Files using type as File
  IHyperLink hyperlink2 = sheet.HyperLinks.Add(sheet.Range["C9"]);
  hyperlink2.Type = ExcelHyperLinkType.File;
  hyperlink2.Address = @"C:\Program files";
  hyperlink2.ScreenTip = "File path";
  hyperlink2.TextToDisplay = "Hyperlink for files using File as type";

  //Creating a Hyperlink for Opening Files using type as Unc
  IHyperLink hyperlink3 = sheet.HyperLinks.Add(sheet.Range["C11"]);
  hyperlink3.Type = ExcelHyperLinkType.Unc;
  hyperlink3.Address = @"C:\Documents and Settings";
  hyperlink3.ScreenTip = "Click here for files";
  hyperlink3.TextToDisplay = "Hyperlink for files using Unc as type";

  //Creating a Hyperlink to another cell using type as Workbook
  IHyperLink hyperlink4 = sheet.HyperLinks.Add(sheet.Range["C13"]);
  hyperlink4.Type = ExcelHyperLinkType.Workbook;
  hyperlink4.Address = "Sheet1!A15";
  hyperlink4.ScreenTip = "Click here";
  hyperlink4.TextToDisplay = "Hyperlink to cell A15";

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Hyperlink";
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
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Creating a Hyperlink for a Website
  IHyperLink hyperlink = sheet.HyperLinks.Add(sheet.Range["C5"]);
  hyperlink.Type = ExcelHyperLinkType.Url;
  hyperlink.Address = "http://www.syncfusion.com";
  hyperlink.ScreenTip = "To know more about Syncfusion products, go through this link.";

  //Creating a Hyperlink for e-mail
  IHyperLink hyperlink1 = sheet.HyperLinks.Add(sheet.Range["C7"]);
  hyperlink1.Type = ExcelHyperLinkType.Url;
  hyperlink1.Address = "mailto:Username@syncfusion.com";
  hyperlink1.ScreenTip = "Send Mail";

  //Creating a Hyperlink for Opening Files using type as File
  IHyperLink hyperlink2 = sheet.HyperLinks.Add(sheet.Range["C9"]);
  hyperlink2.Type = ExcelHyperLinkType.File;
  hyperlink2.Address = @"C:\Program files";
  hyperlink2.ScreenTip = "File path";
  hyperlink2.TextToDisplay = "Hyperlink for files using File as type";

  //Creating a Hyperlink for Opening Files using type as Unc
  IHyperLink hyperlink3 = sheet.HyperLinks.Add(sheet.Range["C11"]);
  hyperlink3.Type = ExcelHyperLinkType.Unc;
  hyperlink3.Address = @"C:\Documents and Settings";
  hyperlink3.ScreenTip = "Click here for files";
  hyperlink3.TextToDisplay = "Hyperlink for files using Unc as type";

  //Creating a Hyperlink to another cell using type as Workbook
  IHyperLink hyperlink4 = sheet.HyperLinks.Add(sheet.Range["C13"]);
  hyperlink4.Type = ExcelHyperLinkType.Workbook;
  hyperlink4.Address = "Sheet1!A15";
  hyperlink4.ScreenTip = "Click here";
  hyperlink4.TextToDisplay = "Hyperlink to cell A15";

  //Saving the workbook as stream
  FileStream stream = new FileStream("Hyperlink.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Creating a Hyperlink for a Website
  IHyperLink hyperlink = sheet.HyperLinks.Add(sheet.Range["C5"]);
  hyperlink.Type = ExcelHyperLinkType.Url;
  hyperlink.Address = "http://www.syncfusion.com";
  hyperlink.ScreenTip = "To know more about Syncfusion products, go through this link.";

  //Creating a Hyperlink for e-mail
  IHyperLink hyperlink1 = sheet.HyperLinks.Add(sheet.Range["C7"]);
  hyperlink1.Type = ExcelHyperLinkType.Url;
  hyperlink1.Address = "mailto:Username@syncfusion.com";
  hyperlink1.ScreenTip = "Send Mail";

  //Creating a Hyperlink for Opening Files using type as File
  IHyperLink hyperlink2 = sheet.HyperLinks.Add(sheet.Range["C9"]);
  hyperlink2.Type = ExcelHyperLinkType.File;
  hyperlink2.Address = @"C:\Program files";
  hyperlink2.ScreenTip = "File path";
  hyperlink2.TextToDisplay = "Hyperlink for files using File as type";

  //Creating a Hyperlink for Opening Files using type as Unc
  IHyperLink hyperlink3 = sheet.HyperLinks.Add(sheet.Range["C11"]);
  hyperlink3.Type = ExcelHyperLinkType.Unc;
  hyperlink3.Address = @"C:\Documents and Settings";
  hyperlink3.ScreenTip = "Click here for files";
  hyperlink3.TextToDisplay = "Hyperlink for files using Unc as type";

  //Creating a Hyperlink to another cell using type as Workbook
  IHyperLink hyperlink4 = sheet.HyperLinks.Add(sheet.Range["C13"]);
  hyperlink4.Type = ExcelHyperLinkType.Workbook;
  hyperlink4.Address = "Sheet1!A15";
  hyperlink4.ScreenTip = "Click here";
  hyperlink4.TextToDisplay = "Hyperlink to cell A15";

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Hyperlink.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Hyperlink.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to add hyperlinks in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Editing%20Excel%20cells/Hyperlinks).

### Modifying Existing Hyperlink

The properties of existing hyperlink can be modified by accessing it through the [IRange](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IRange.html) instance.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
  IWorksheet sheet = workbook.Worksheets[0];

  //Modifying hyperlink’s text to display
  IHyperLink hyperlink = sheet.Range["C5"].Hyperlinks[0];
  hyperlink.TextToDisplay = "Syncfusion";

  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs("Hyperlink.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Modifying hyperlink’s text to display
  Dim hyperlink As IHyperLink = sheet.Range("C5").Hyperlinks(0)
  hyperlink.TextToDisplay = "Syncfusion"

  workbook.Version = ExcelVersion.Xlsx
  workbook.SaveAs("Hyperlink.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  //Instantiates the File Picker
  FileOpenPicker openPicker = new FileOpenPicker();
  openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
  openPicker.FileTypeFilter.Add(".xlsx");
  openPicker.FileTypeFilter.Add(".xls");
  StorageFile file = await openPicker.PickSingleFileAsync();

  //Opens the workbook
  IWorkbook workbook = await application.Workbooks.OpenAsync(file);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Modifying hyperlink’s text to display
  IHyperLink hyperlink = worksheet.Range["C5"].Hyperlinks[0];
  hyperlink.TextToDisplay = "Syncfusion";

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Hyperlink";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  workbook.Version = ExcelVersion.Xlsx;
  await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Modifying hyperlink’s text to display
  IHyperLink hyperlink = worksheet.Range["C5"].Hyperlinks[0];
  hyperlink.TextToDisplay = "Syncfusion";

  //Saving the workbook as stream
  FileStream stream = new FileStream("Hyperlink.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream = assembly.GetManifestResourceStream("CellsManipulation.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Modifying hyperlink’s text to display
  IHyperLink hyperlink = worksheet.Range["C5"].Hyperlinks[0];
  hyperlink.TextToDisplay = "Syncfusion";

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Hyperlink.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Hyperlink.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to modify existing hyperlink in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Editing%20Excel%20cells/Modify%20Hyperlink).

### Removing Hyperlink

Similarly, a hyperlink can also be removed from a range by accessing it through the [IRange](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IRange.html) instance.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
  IWorksheet sheet = workbook.Worksheets[0];

  //Removing Hyperlink from Range "C7"
  sheet.Range["C7"].Hyperlinks.RemoveAt(0);

  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs("Hyperlink.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Removing Hyperlink from Range "C7"
  sheet.Range("C7").Hyperlinks.RemoveAt(0)

  workbook.Version = ExcelVersion.Xlsx
  workbook.SaveAs("Hyperlink.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  //Instantiates the File Picker
  FileOpenPicker openPicker = new FileOpenPicker();
  openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
  openPicker.FileTypeFilter.Add(".xlsx");
  openPicker.FileTypeFilter.Add(".xls");
  StorageFile file = await openPicker.PickSingleFileAsync();

  //Opens the workbook
  IWorkbook workbook = await application.Workbooks.OpenAsync(file);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Removing Hyperlink from Range "C7"
  worksheet.Range["C7"].Hyperlinks.RemoveAt(0);

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Hyperlink";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  workbook.Version = ExcelVersion.Xlsx;
  await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Removing Hyperlink from Range "C7"
  worksheet.Range["C7"].Hyperlinks.RemoveAt(0);

  //Saving the workbook as stream
  FileStream stream = new FileStream("Hyperlink.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream = assembly.GetManifestResourceStream("CellsManipulation.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Removing Hyperlink from Range "C7"
  worksheet.Range["C7"].Hyperlinks.RemoveAt(0);

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.Version = ExcelVersion.Xlsx;
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Hyperlink.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Hyperlink.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to remove existing hyperlink in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Editing%20Excel%20cells/Remove%20Hyperlink).

### Hyperlinks on Shapes

**Adding** **Hyperlinks** **to** **Shapes**

Hyperlink can be added to the following shapes.

* Picture
* AutoShape
* TextBox

The following code example illustrates how to insert hyperlinks to shapes.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");

  //Adding hyperlink to TextBox 
  IWorksheet sheet = workbook.Worksheets[0];
  ITextBox textBox = sheet.TextBoxes.AddTextBox(1, 1, 100, 100);
  IHyperLink hyperlink = sheet.HyperLinks.Add((textBox as IShape), ExcelHyperLinkType.Url, "http://www.Syncfusion.com", "click here");

  //Adding hyperlink to AutoShape
  sheet = workbook.Worksheets[1];
  IShape autoShape = sheet.Shapes.AddAutoShapes(AutoShapeType.Cloud, 1, 1, 100, 100);
  hyperlink = sheet.HyperLinks.Add(autoShape, ExcelHyperLinkType.Url, "mailto:Username@syncfusion.com", "Send Mail");

  //Adding hyperlink to picture
  sheet = workbook.Worksheets[2];
  IPictureShape picture = sheet.Pictures.AddPicture(@"Image.png");
  hyperlink = sheet.HyperLinks.Add(picture);
  hyperlink.Type = ExcelHyperLinkType.Unc;
  hyperlink.Address = "C:\\Documents and Settings";
  hyperlink.ScreenTip = "Click here for files";

  workbook.SaveAs("Hyperlink.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")

  'Text box 
  Dim sheet As IWorksheet = workbook.Worksheets(0)
  Dim textBox As ITextBox = sheet.TextBoxes.AddTextBox(1, 1, 100, 100)
  Dim hyperlink As IHyperLink = sheet.HyperLinks.Add(TryCast(textBox, IShape), ExcelHyperLinkType.Url, "http://www.Syncfusion.com", "click here")

  'AutoShapes 
  sheet = workbook.Worksheets(1)
  Dim autoShape As IShape = sheet.Shapes.AddAutoShapes(AutoShapeType.Cloud, 1, 1, 100, 100)
  hyperlink = sheet.HyperLinks.Add(autoShape, ExcelHyperLinkType.Url, "mailto:Username@syncfusion.com", "Send Mail")

  'Pictures 
  sheet = workbook.Worksheets(2)
  Dim picture As IPictureShape = sheet.Pictures.AddPicture("Image.png")
  hyperlink = sheet.HyperLinks.Add(picture)
  hyperlink.Type = ExcelHyperLinkType.Unc
  hyperlink.Address = "C:\Documents and Settings"
  hyperlink.ScreenTip = "Click here for files"

  workbook.SaveAs("Hyperlink.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;

  //Instantiates the File Picker
  FileOpenPicker openPicker = new FileOpenPicker();
  openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
  openPicker.FileTypeFilter.Add(".xlsx");
  openPicker.FileTypeFilter.Add(".xls");
  StorageFile file = await openPicker.PickSingleFileAsync();

  //Opens the workbook
  IWorkbook workbook = await application.Workbooks.OpenAsync(file);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Adding hyperlink to TextBox 
  ITextBox textBox = worksheet.TextBoxes.AddTextBox(1, 1, 100, 100);
  IHyperLink hyperlink = worksheet.HyperLinks.Add((textBox as IShape), ExcelHyperLinkType.Url, "http://www.Syncfusion.com", "click here");

  //Adding hyperlink to AutoShape
  IShape autoShape = worksheet.Shapes.AddAutoShapes(AutoShapeType.Cloud, 1, 1, 100, 100);
  hyperlink = worksheet.HyperLinks.Add(autoShape, ExcelHyperLinkType.Url, "mailto:Username@syncfusion.com", "Send Mail");

  //Adding hyperlink to picture
  IPictureShape picture = worksheet.Pictures.AddPictureAsLink(5, 5, 10, 10, "Image.png");
  hyperlink = worksheet.HyperLinks.Add(picture);
  hyperlink.Type = ExcelHyperLinkType.Unc;
  hyperlink.Address = "C:\\Documents and Settings";
  hyperlink.ScreenTip = "Click here for files";

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Hyperlink";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  workbook.Version = ExcelVersion.Xlsx;
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

  //Adding hyperlink to TextBox 
  ITextBox textBox = worksheet.TextBoxes.AddTextBox(1, 1, 100, 100);
  IHyperLink hyperlink = worksheet.HyperLinks.Add((textBox as IShape), ExcelHyperLinkType.Url, "http://www.Syncfusion.com", "click here");

  //Adding hyperlink to AutoShape
  IShape autoShape = worksheet.Shapes.AddAutoShapes(AutoShapeType.Cloud, 1, 1, 100, 100);
  hyperlink = worksheet.HyperLinks.Add(autoShape, ExcelHyperLinkType.Url, "mailto:Username@syncfusion.com", "Send Mail");

  //Adding hyperlink to picture
  IPictureShape picture = worksheet.Pictures.AddPictureAsLink(5, 5, 10, 10, "Image.png");
  hyperlink = worksheet.HyperLinks.Add(picture);
  hyperlink.Type = ExcelHyperLinkType.Unc;
  hyperlink.Address = "C:\\Documents and Settings";
  hyperlink.ScreenTip = "Click here for files";

  //Saving the workbook as stream
  FileStream stream = new FileStream("Hyperlink.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;

  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream = assembly.GetManifestResourceStream("CellsManipulation.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Adding hyperlink to TextBox 
  ITextBox textBox = worksheet.TextBoxes.AddTextBox(1, 1, 100, 100);
  IHyperLink hyperlink = worksheet.HyperLinks.Add((textBox as IShape), ExcelHyperLinkType.Url, "http://www.Syncfusion.com", "click here");

  //Adding hyperlink to AutoShape
  IShape autoShape = worksheet.Shapes.AddAutoShapes(AutoShapeType.Cloud, 1, 1, 100, 100);
  hyperlink = worksheet.HyperLinks.Add(autoShape, ExcelHyperLinkType.Url, "mailto:Username@syncfusion.com", "Send Mail");

  //Adding hyperlink to picture
  IPictureShape picture = worksheet.Pictures.AddPictureAsLink(5, 5, 10, 10, "Image.png");
  hyperlink = worksheet.HyperLinks.Add(picture);
  hyperlink.Type = ExcelHyperLinkType.Unc;
  hyperlink.Address = "C:\\Documents and Settings";
  hyperlink.ScreenTip = "Click here for files";

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Hyperlink.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Hyperlink.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to add hyperlink to shape in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Editing%20Excel%20cells/Shape%20Hyperlink).

**Modifying** **Hyperlinks** **on** **Shapes**

Properties of existing hyperlink can be modified by accessing it through [IWorksheet](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorksheet.html) instance or [IShape](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IShape.html) instance.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
  IWorksheet sheet = workbook.Worksheets[0];

  //Modifying hyperlink’s screen tip through IWorksheet instance
  IHyperLink hyperlink = sheet.HyperLinks[0];
  hyperlink.ScreenTip = "Syncfusion";

  //Modifying hyperlink’s screen tip through IShape instance
  hyperlink = sheet.Shapes[0].Hyperlink;
  hyperlink.ScreenTip = "Syncfusion";

  workbook.SaveAs("Hyperlink.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Modifying hyperlink’s screen tip through IWorksheet instance
  Dim hyperlink As IHyperLink = sheet.HyperLinks(0)
  hyperlink.ScreenTip = "Syncfusion"

  'Modifying hyperlink’s screen tip through IShape instance
  hyperlink = sheet.Shapes(0).Hyperlink
  hyperlink.ScreenTip = "Syncfusion"

  workbook.SaveAs("Hyperlink.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;

  //Instantiates the File Picker
  FileOpenPicker openPicker = new FileOpenPicker();
  openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
  openPicker.FileTypeFilter.Add(".xlsx");
  openPicker.FileTypeFilter.Add(".xls");
  StorageFile file = await openPicker.PickSingleFileAsync();

  //Opens the workbook
  IWorkbook workbook = await application.Workbooks.OpenAsync(file);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Modifying hyperlink’s screen tip through IWorksheet instance
  IHyperLink hyperlink = worksheet.HyperLinks[0];
  hyperlink.ScreenTip = "Syncfusion";

  //Modifying hyperlink’s screen tip through IShape instance
  hyperlink = worksheet.Shapes[0].Hyperlink;
  hyperlink.ScreenTip = "Syncfusion";

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Hyperlink";
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

  //Modifying hyperlink’s screen tip through IWorksheet instance
  IHyperLink hyperlink = worksheet.HyperLinks[0];
  hyperlink.ScreenTip = "Syncfusion";

  //Modifying hyperlink’s screen tip through IShape instance
  hyperlink = worksheet.Shapes[0].Hyperlink;
  hyperlink.ScreenTip = "Syncfusion";

  //Saving the workbook as stream
  FileStream stream = new FileStream("Hyperlink.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;

  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream = assembly.GetManifestResourceStream("CellsManipulation.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Modifying hyperlink’s screen tip through IWorksheet instance
  IHyperLink hyperlink = worksheet.HyperLinks[0];
  hyperlink.ScreenTip = "Syncfusion";

  //Modifying hyperlink’s screen tip through IShape instance
  hyperlink = worksheet.Shapes[0].Hyperlink;
  hyperlink.ScreenTip = "Syncfusion";

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Hyperlink.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Hyperlink.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to modify shape hyperlink in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Editing%20Excel%20cells/Modify%20Shape%20Hyperlink).

**Removing** **Hyperlinks** **from** **Shapes**

The following code snippet explains how to remove hyperlink of shape.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
  IWorksheet sheet = workbook.Worksheets[0];

  //Removing hyperlink from sheet with Index
  sheet.HyperLinks.RemoveAt(0);

  workbook.SaveAs("Hyperlink.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Removing Hyperlink from sheet with Index
  sheet.HyperLinks.RemoveAt(0)

  workbook.SaveAs("Hyperlink.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;

  //Instantiates the File Picker
  FileOpenPicker openPicker = new FileOpenPicker();
  openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
  openPicker.FileTypeFilter.Add(".xlsx");
  openPicker.FileTypeFilter.Add(".xls");
  StorageFile file = await openPicker.PickSingleFileAsync();

  //Opens the workbook
  IWorkbook workbook = await application.Workbooks.OpenAsync(file);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Removing hyperlink from sheet with Index
  worksheet.HyperLinks.RemoveAt(0);

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Hyperlink";
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

  //Removing hyperlink from sheet with Index
  worksheet.HyperLinks.RemoveAt(0);

  //Saving the workbook as stream
  FileStream stream = new FileStream("Hyperlink.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;

  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream = assembly.GetManifestResourceStream("CellsManipulation.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Removing hyperlink from sheet with Index
  worksheet.HyperLinks.RemoveAt(0);

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Hyperlink.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Hyperlink.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example to remove shape hyperlink in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Editing%20Excel%20cells/Remove%20Shape%20Hyperlink).

## List of APIs under IRange 

### Cell Address

The following code snippet explains the usage of [Address](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IRange.html#Syncfusion_XlsIO_IRange_Address), [AddressGlobal](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IRange.html#Syncfusion_XlsIO_IRange_AddressGlobal), [AddressLocal](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IRange.html#Syncfusion_XlsIO_IRange_AddressLocal), [AddressR1C1](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IRange.html#Syncfusion_XlsIO_IRange_AddressR1C1), [AddressR1C1Local](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IRange.html#Syncfusion_XlsIO_IRange_AddressR1C1Local) properties.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Address
  string address = worksheet.Range[3, 4].Address;

  //Global Address
  string address_Global = worksheet.Range[3, 4].AddressGlobal;

  //Local Address
  string address_Local = worksheet.Range[3, 4].AddressLocal;

  //R1C1 Address
  string address_R1C1 = worksheet.Range[3, 4].AddressR1C1;

  //Local R1C1 Address
  string address_R1C1_Local = worksheet.Range[3, 4].AddressR1C1Local;

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Address
  Dim address As String = worksheet.Range(3, 4).Address

  'Global Address
  Dim address_Global As String = worksheet.Range(3, 4).AddressGlobal

  'Local Address
  Dim address_Local As String = worksheet.Range(3, 4).AddressLocal

  'R1C1 Address
  Dim address_R1C1 As String = worksheet.Range(3, 4).AddressR1C1

  'Local R1C1 Address
  Dim address_R1C1_Local As String = worksheet.Range(3, 4).AddressR1C1Local

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Address
  string address = worksheet.Range[3, 4].Address;

  //Global Address
  string address_Global = worksheet.Range[3, 4].AddressGlobal;

  //Local Address
  string address_Local = worksheet.Range[3, 4].AddressLocal;

  //R1C1 Address
  string address_R1C1 = worksheet.Range[3, 4].AddressR1C1;

  //Local R1C1 Address
  string address_R1C1_Local = worksheet.Range[3, 4].AddressR1C1Local;

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
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Address
  string address = worksheet.Range[3, 4].Address;

  //Global Address
  string address_Global = worksheet.Range[3, 4].AddressGlobal;

  //Local Address
  string address_Local = worksheet.Range[3, 4].AddressLocal;

  //R1C1 Address
  string address_R1C1 = worksheet.Range[3, 4].AddressR1C1;

  //Local R1C1 Address
  string address_R1C1_Local = worksheet.Range[3, 4].AddressR1C1Local;

  //Saving the Excel to the MemoryStream 
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  //Set the position as '0'
  stream.Position = 0;

  //Download the PDF file in the browser
  FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/excel");
  fileStreamResult.FileDownloadName = "Output.xlsx";
  return fileStreamResult;
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Address
  string address = worksheet.Range[3, 4].Address;

  //Global Address
  string address_Global = worksheet.Range[3, 4].AddressGlobal;

  //Local Address
  string address_Local = worksheet.Range[3, 4].AddressLocal;

  //R1C1 Address
  string address_R1C1 = worksheet.Range[3, 4].AddressR1C1;

  //Local R1C1 Address
  string address_R1C1_Local = worksheet.Range[3, 4].AddressR1C1Local;

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;
  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", stream);                
}
{% endhighlight %}
{% endtabs %}

### Boolean

As the name says, [Boolean](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IRange.html#Syncfusion_XlsIO_IRange_Boolean) property gets or sets the boolean value in a worksheet range. The following code snippet explains this.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Boolean - True
  worksheet.Range["B3"].Boolean = true;
  bool b3 = worksheet.Range["B3"].Boolean;

  //Boolean - False
  worksheet.Range["B4"].Boolean = false;
  bool b4 = worksheet.Range["B4"].Boolean;

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Boolean - True
  worksheet.Range("B3").Boolean = True
  Dim b3 As Boolean = worksheet.Range("B3").Boolean

  'Boolean - False
  worksheet.Range("B4").Boolean = False
  Dim b4 As Boolean = worksheet.Range("B4").Boolean

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Boolean - True
  worksheet.Range["B3"].Boolean = true;
  bool b3 = worksheet.Range["B3"].Boolean;

  //Boolean - False
  worksheet.Range["B4"].Boolean = false;
  bool b4 = worksheet.Range["B4"].Boolean;

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
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Boolean - True
  worksheet.Range["B3"].Boolean = true;
  bool b3 = worksheet.Range["B3"].Boolean;

  //Boolean - False
  worksheet.Range["B4"].Boolean = false;
  bool b4 = worksheet.Range["B4"].Boolean;

  //Saving the Excel to the MemoryStream 
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  //Set the position as '0'
  stream.Position = 0;

  //Download the PDF file in the browser
  FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/excel");
  fileStreamResult.FileDownloadName = "Output.xlsx";
  return fileStreamResult;
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Boolean - True
  worksheet.Range["B3"].Boolean = true;
  bool b3 = worksheet.Range["B3"].Boolean;

  //Boolean - False
  worksheet.Range["B4"].Boolean = false;
  bool b4 = worksheet.Range["B4"].Boolean;

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;
  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", stream);                
}
{% endhighlight %}
{% endtabs %}

### Borders

The following code snippet explains how to set border styles for a worksheet range using [Borders](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IRange.html#Syncfusion_XlsIO_IRange_Borders) property.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set text
  worksheet.Range["C2"].Text = "Sample";

  //Set borders
  IBorders borders = worksheet.Range["C2"].Borders;

  //Set border color
  borders[ExcelBordersIndex.EdgeTop].Color = ExcelKnownColors.Red;
  borders[ExcelBordersIndex.EdgeBottom].Color = ExcelKnownColors.Blue;

  //Set line style
  borders[ExcelBordersIndex.EdgeTop].LineStyle = ExcelLineStyle.Thick;
  borders[ExcelBordersIndex.EdgeBottom].LineStyle = ExcelLineStyle.Thick;

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Set text
  worksheet.Range("C2").Text = "Sample"

  'Set borders
  Dim borders As IBorders = worksheet.Range("C2").Borders

  'Set border color
  borders(ExcelBordersIndex.EdgeTop).Color = ExcelKnownColors.Red
  borders(ExcelBordersIndex.EdgeBottom).Color = ExcelKnownColors.Blue

  'Set line style
  borders(ExcelBordersIndex.EdgeTop).LineStyle = ExcelLineStyle.Thick
  borders(ExcelBordersIndex.EdgeBottom).LineStyle = ExcelLineStyle.Thick

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set text
  worksheet.Range["C2"].Text = "Sample";

  //Set borders
  IBorders borders = worksheet.Range["C2"].Borders;

  //Set border color
  borders[ExcelBordersIndex.EdgeTop].Color = ExcelKnownColors.Red;
  borders[ExcelBordersIndex.EdgeBottom].Color = ExcelKnownColors.Blue;

  //Set line style
  borders[ExcelBordersIndex.EdgeTop].LineStyle = ExcelLineStyle.Thick;
  borders[ExcelBordersIndex.EdgeBottom].LineStyle = ExcelLineStyle.Thick;

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
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set text
  worksheet.Range["C2"].Text = "Sample";

  //Set borders
  IBorders borders = worksheet.Range["C2"].Borders;

  //Set border color
  borders[ExcelBordersIndex.EdgeTop].Color = ExcelKnownColors.Red;
  borders[ExcelBordersIndex.EdgeBottom].Color = ExcelKnownColors.Blue;

  //Set line style
  borders[ExcelBordersIndex.EdgeTop].LineStyle = ExcelLineStyle.Thick;
  borders[ExcelBordersIndex.EdgeBottom].LineStyle = ExcelLineStyle.Thick;

  //Saving the Excel to the MemoryStream 
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  //Set the position as '0'
  stream.Position = 0;

  //Download the PDF file in the browser
  FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/excel");
  fileStreamResult.FileDownloadName = "Output.xlsx";
  return fileStreamResult;
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set text
  worksheet.Range["C2"].Text = "Sample";

  //Set borders
  IBorders borders = worksheet.Range["C2"].Borders;

  //Set border color
  borders[ExcelBordersIndex.EdgeTop].Color = ExcelKnownColors.Red;
  borders[ExcelBordersIndex.EdgeBottom].Color = ExcelKnownColors.Blue;

  //Set line style
  borders[ExcelBordersIndex.EdgeTop].LineStyle = ExcelLineStyle.Thick;
  borders[ExcelBordersIndex.EdgeBottom].LineStyle = ExcelLineStyle.Thick;

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;
  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", stream);                
}
{% endhighlight %}
{% endtabs %}

### Built-In-Style

The following code snippet explains how to add [BuiltInStyle](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IRange.html#Syncfusion_XlsIO_IRange_BuiltInStyle) for a worksheet range.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set text
  worksheet.Range["C2"].Text = "Sample";

  //Set built in style
  worksheet.Range["C2"].BuiltInStyle = BuiltInStyles.Accent3;

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Set text
  worksheet.Range("C2").Text = "Sample"

  'Set built in style
  worksheet.Range("C2").BuiltInStyle = BuiltInStyles.Accent3

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set text
  worksheet.Range["C2"].Text = "Sample";

  //Set built in style
  worksheet.Range["C2"].BuiltInStyle = BuiltInStyles.Accent3;

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
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set text
  worksheet.Range["C2"].Text = "Sample";

  //Set built in style
  worksheet.Range["C2"].BuiltInStyle = BuiltInStyles.Accent3;

  //Saving the Excel to the MemoryStream 
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  //Set the position as '0'
  stream.Position = 0;

  //Download the PDF file in the browser
  FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/excel");
  fileStreamResult.FileDownloadName = "Output.xlsx";
  return fileStreamResult;
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set text
  worksheet.Range["C2"].Text = "Sample";

  //Set built in style
  worksheet.Range["C2"].BuiltInStyle = BuiltInStyles.Accent3;

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;
  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", stream);                
}
{% endhighlight %}
{% endtabs %}

### Calculated Value

[CalculatedValue](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IRange.html#Syncfusion_XlsIO_IRange_CalculatedValue) is the evaluated value of the formula. The following code snippet explains how to get the **CalculatedValue** of the formula.

N> It is mandatory to enable sheet calculations i.e., **worksheet.EnableSheetCalculations();** before accessing the **CalculatedValue**. Else, **CalculatedValue** will be returned as null.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set values
  worksheet.Range["A1"].Number = 10;
  worksheet.Range["A2"].Number = 20;

  //Set formula
  worksheet.Range["A3"].Formula = "=SUM(A1:A2)";

  //Enable sheet calculations
  worksheet.EnableSheetCalculations();

  //Get the calculated value
  string value = worksheet.Range["A3"].CalculatedValue;

  //Disable sheet calculations
  worksheet.DisableSheetCalculations();

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Set values
  worksheet.Range("A1").Number = 10
  worksheet.Range("A2").Number = 20

  'Set formula
  worksheet.Range("A3").Formula = "=SUM(A1:A2)"

  'Enable sheet calculations
  worksheet.EnableSheetCalculations()

  'Get the calculated value
  Dim value As String = worksheet.Range("A3").CalculatedValue

  'Disable sheet calculations
  worksheet.DisableSheetCalculations()

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set values
  worksheet.Range["A1"].Number = 10;
  worksheet.Range["A2"].Number = 20;

  //Set formula
  worksheet.Range["A3"].Formula = "=SUM(A1:A2)";

  //Enable sheet calculations
  worksheet.EnableSheetCalculations();

  //Get the calculated value
  string value = worksheet.Range["A3"].CalculatedValue;

  //Disable sheet calculations
  worksheet.DisableSheetCalculations();

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
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set values
  worksheet.Range["A1"].Number = 10;
  worksheet.Range["A2"].Number = 20;

  //Set formula
  worksheet.Range["A3"].Formula = "=SUM(A1:A2)";

  //Enable sheet calculations
  worksheet.EnableSheetCalculations();

  //Get the calculated value
  string value = worksheet.Range["A3"].CalculatedValue;

  //Disable sheet calculations
  worksheet.DisableSheetCalculations();

  //Saving the Excel to the MemoryStream 
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  //Set the position as '0'
  stream.Position = 0;

  //Download the PDF file in the browser
  FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/excel");
  fileStreamResult.FileDownloadName = "Output.xlsx";
  return fileStreamResult;
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set values
  worksheet.Range["A1"].Number = 10;
  worksheet.Range["A2"].Number = 20;

  //Set formula
  worksheet.Range["A3"].Formula = "=SUM(A1:A2)";

  //Enable sheet calculations
  worksheet.EnableSheetCalculations();

  //Get the calculated value
  string value = worksheet.Range["A3"].CalculatedValue;

  //Disable sheet calculations
  worksheet.DisableSheetCalculations();

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;
  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", stream);                
}
{% endhighlight %}
{% endtabs %}

### Cells

[Cells](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IRange.html#Syncfusion_XlsIO_IRange_Cells) property maintains the collection of cells in a worksheet range. The following code snippet explains how to access this property.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Range of cells
  IRange[] cells = worksheet.Range["A1:E5"].Cells;

  foreach (IRange cell in cells)
  {
    //Assign value
    cell.Text = cell.AddressLocal;
  }

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Range of cells
  Dim cells() As IRange = worksheet.Range("A1:E5").Cells

  For Each cell As IRange In cells
    'Assign value
    cell.Text = cell.AddressLocal
  Next

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Range of cells
  IRange[] cells = worksheet.Range["A1:E5"].Cells;

  foreach (IRange cell in cells)
  {
    //Assign value
    cell.Text = cell.AddressLocal;
  }

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
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Range of cells
  IRange[] cells = worksheet.Range["A1:E5"].Cells;

  foreach (IRange cell in cells)
  {
    //Assign value
    cell.Text = cell.AddressLocal;
  }

  //Saving the Excel to the MemoryStream 
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  //Set the position as '0'
  stream.Position = 0;

  //Download the PDF file in the browser
  FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/excel");
  fileStreamResult.FileDownloadName = "Output.xlsx";
  return fileStreamResult;
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Range of cells
  IRange[] cells = worksheet.Range["A1:E5"].Cells;

  foreach (IRange cell in cells)
  {
    //Assign value
    cell.Text = cell.AddressLocal;
  }

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;
  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", stream);                
}
{% endhighlight %}
{% endtabs %}

### Cell Style Name

[CellStyleName](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IRange.html#Syncfusion_XlsIO_IRange_CellStyleName) represents the name of the style of worksheet range/cell. The default value is **Normal**.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Add style
  IStyle style = workbook.Styles.Add("CustomStyle");

  //Set color
  style.ColorIndex = ExcelKnownColors.Red;

  //Set style
  worksheet.Range["C2"].CellStyle = style;

  //Get the cell style name
  string cellStyleName = worksheet.Range["C2"].CellStyleName;

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Add style
  Dim style As IStyle = workbook.Styles.Add("CustomStyle")

  'Set color
  style.ColorIndex = ExcelKnownColors.Red

  'Set style
  worksheet.Range("C2").CellStyle = style

  'Get the cell style name
  Dim cellStyleName As String = worksheet.Range("C2").CellStyleName

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Add style
  IStyle style = workbook.Styles.Add("CustomStyle");

  //Set color
  style.ColorIndex = ExcelKnownColors.Red;

  //Set style
  worksheet.Range["C2"].CellStyle = style;

  //Get the cell style name
  string cellStyleName = worksheet.Range["C2"].CellStyleName;

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
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Add style
  IStyle style = workbook.Styles.Add("CustomStyle");

  //Set color
  style.ColorIndex = ExcelKnownColors.Red;

  //Set style
  worksheet.Range["C2"].CellStyle = style;

  //Get the cell style name
  string cellStyleName = worksheet.Range["C2"].CellStyleName;

  //Saving the Excel to the MemoryStream 
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  //Set the position as '0'
  stream.Position = 0;

  //Download the PDF file in the browser
  FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/excel");
  fileStreamResult.FileDownloadName = "Output.xlsx";
  return fileStreamResult;
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Add style
  IStyle style = workbook.Styles.Add("CustomStyle");

  //Set color
  style.ColorIndex = ExcelKnownColors.Red;

  //Set style
  worksheet.Range["C2"].CellStyle = style;

  //Get the cell style name
  string cellStyleName = worksheet.Range["C2"].CellStyleName;

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;
  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", stream);                
}
{% endhighlight %}
{% endtabs %}

### Column

[Column](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IRange.html#Syncfusion_XlsIO_IRange_Column) property gets the column index of first column in worksheet range, which is one-index based. 

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Get first column in the range
  int firstColumn = worksheet.Range["E1:R3"].Column;

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Get first column in the range
  Dim firstColumn As Integer = worksheet.Range("E1:R3").Column

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Get first column in the range
  int firstColumn = worksheet.Range["E1:R3"].Column;

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
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Get first column in the range
  int firstColumn = worksheet.Range["E1:R3"].Column;

  //Saving the Excel to the MemoryStream 
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  //Set the position as '0'
  stream.Position = 0;

  //Download the PDF file in the browser
  FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/excel");
  fileStreamResult.FileDownloadName = "Output.xlsx";
  return fileStreamResult;
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Get first column in the range
  int firstColumn = worksheet.Range["E1:R3"].Column;

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;
  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", stream);                
}
{% endhighlight %}
{% endtabs %}

### Columns

[Columns](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IRange.html#Syncfusion_XlsIO_IRange_Columns) property maintains the collection of columns in a worksheet range. 

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Columns
  IRange[] columns = worksheet.Range["A1:E5"].Columns;

  foreach (IRange column in columns)
  {
    //Assign value
    column.Text = column.AddressLocal;
  }

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Columns
  Dim columns() As IRange = worksheet.Range("A1:E5").Columns

  For Each column As IRange In columns
    'Assign value
    column.Text = column.AddressLocal
  Next

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Columns
  IRange[] columns = worksheet.Range["A1:E5"].Columns;

  foreach (IRange column in columns)
  {
    //Assign value
    column.Text = column.AddressLocal;
  }

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
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Columns
  IRange[] columns = worksheet.Range["A1:E5"].Columns;

  foreach (IRange column in columns)
  {
    //Assign value
    column.Text = column.AddressLocal;
  }

  //Saving the Excel to the MemoryStream 
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  //Set the position as '0'
  stream.Position = 0;

  //Download the PDF file in the browser
  FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/excel");
  fileStreamResult.FileDownloadName = "Output.xlsx";
  return fileStreamResult;
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Columns
  IRange[] columns = worksheet.Range["A1:E5"].Columns;

  foreach (IRange column in columns)
  {
    //Assign value
    column.Text = column.AddressLocal;
  }

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;
  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", stream);                
}
{% endhighlight %}
{% endtabs %}

### Comment

To know in detail about **Comment**, please navigate to [https://help.syncfusion.com/file-formats/xlsio/working-with-drawing-objects#comments](https://help.syncfusion.com/file-formats/xlsio/working-with-drawing-objects#comments).

### Conditional Formats

To know in detail about **Conditional Formats**, please navigate to [https://help.syncfusion.com/file-formats/xlsio/working-with-conditional-formatting](https://help.syncfusion.com/file-formats/xlsio/working-with-conditional-formatting).

### Count

[Count](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IRange.html#Syncfusion_XlsIO_IRange_Count) property returns the number of cells in that particular worksheet range.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Number of cells
  int count = worksheet.Range["A1:E5"].Count;

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Number of cells
  Dim count As Integer = worksheet.Range("A1:E5").Count

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Number of cells
  int count = worksheet.Range["A1:E5"].Count;

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
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Number of cells
  int count = worksheet.Range["A1:E5"].Count;

  //Saving the Excel to the MemoryStream 
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  //Set the position as '0'
  stream.Position = 0;

  //Download the PDF file in the browser
  FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/excel");
  fileStreamResult.FileDownloadName = "Output.xlsx";
  return fileStreamResult;
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Number of cells
  int count = worksheet.Range["A1:E5"].Count;

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;
  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", stream);
}
{% endhighlight %}
{% endtabs %}

### Data Validation

To know in detail about **Data Validation**, please navigate to [https://help.syncfusion.com/file-formats/xlsio/working-with-data-validation](https://help.syncfusion.com/file-formats/xlsio/working-with-data-validation).

### End

[End](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IRange.html#Syncfusion_XlsIO_IRange_End) property returns the last cell in the particular worksheet range.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Last cell in the range
  IRange lastCell = worksheet.Range["A1:E5"].End;

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Last cell in the range
  Dim lastCell As IRange = worksheet.Range("A1:E5").End

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Last cell in the range
  IRange lastCell = worksheet.Range["A1:E5"].End;

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
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Last cell in the range
  IRange lastCell = worksheet.Range["A1:E5"].End;

  //Saving the Excel to the MemoryStream 
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  //Set the position as '0'
  stream.Position = 0;

  //Download the PDF file in the browser
  FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/excel");
  fileStreamResult.FileDownloadName = "Output.xlsx";
  return fileStreamResult;
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Last cell in the range
  IRange lastCell = worksheet.Range["A1:E5"].End;

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;
  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", stream);
}
{% endhighlight %}
{% endtabs %}

### Entire Column

[EntireColumn](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IRange.html#Syncfusion_XlsIO_IRange_EntireColumn), as the name says gets the entire column of the particular range.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Last cell in the entire column
  IRange lastCell = worksheet.Range["A1"].EntireColumn.End;

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Last cell in the entire column
  Dim lastCell As IRange = worksheet.Range("A1").EntireColumn.End

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Last cell in the entire column
  IRange lastCell = worksheet.Range["A1"].EntireColumn.End;

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
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Last cell in the entire column
  IRange lastCell = worksheet.Range["A1"].EntireColumn.End;

  //Saving the Excel to the MemoryStream 
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  //Set the position as '0'
  stream.Position = 0;

  //Download the PDF file in the browser
  FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/excel");
  fileStreamResult.FileDownloadName = "Output.xlsx";
  return fileStreamResult;
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Last cell in the entire column
  IRange lastCell = worksheet.Range["A1"].EntireColumn.End;

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;
  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", stream);
}
{% endhighlight %}
{% endtabs %}

N> Using EntireColumn property excessively leads to time consumption and affects the performance.

### Entire Row

[EntireRow](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IRange.html#Syncfusion_XlsIO_IRange_EntireRow), as the name says gets the entire row of the particular range.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Last cell in the entire row
  IRange lastCell = worksheet.Range["A1"].EntireRow.End;

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Last cell in the entire row
  Dim lastCell As IRange = worksheet.Range("A1").EntireRow.End

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Last cell in the entire row
  IRange lastCell = worksheet.Range["A1"].EntireRow.End;

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
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Last cell in the entire row
  IRange lastCell = worksheet.Range["A1"].EntireRow.End;

  //Saving the Excel to the MemoryStream 
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  //Set the position as '0'
  stream.Position = 0;

  //Download the PDF file in the browser
  FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/excel");
  fileStreamResult.FileDownloadName = "Output.xlsx";
  return fileStreamResult;
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Last cell in the entire row
  IRange lastCell = worksheet.Range["A1"].EntireRow.End;

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;
  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", stream);
}
{% endhighlight %}
{% endtabs %}

### Formula

[Formula](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IRange.html#Syncfusion_XlsIO_IRange_Formula) property gets or sets the formula in specified range.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set values
  worksheet.Range["A1"].Number = 10;
  worksheet.Range["B1"].Number = 20;

  //Set formula
  worksheet.Range["C1"].Formula = "=SUM(A1:B1)";

  //Enable sheet calculations
  worksheet.EnableSheetCalculations();

  //Get the claculated value of formula
  string value = worksheet.Range["C1"].CalculatedValue;

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Set values
  worksheet.Range("A1").Number = 10
  worksheet.Range("B1").Number = 20

  'Set formula
  worksheet.Range("C1").Formula = "=SUM(A1:B1)"

  'Enable sheet calculations
  worksheet.EnableSheetCalculations()

  'Get the claculated value of formula
  Dim value As String = worksheet.Range("C1").CalculatedValue

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set values
  worksheet.Range["A1"].Number = 10;
  worksheet.Range["B1"].Number = 20;

  //Set formula
  worksheet.Range["C1"].Formula = "=SUM(A1:B1)";

  //Enable sheet calculations
  worksheet.EnableSheetCalculations();

  //Get the claculated value of formula
  string value = worksheet.Range["C1"].CalculatedValue;

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
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set values
  worksheet.Range["A1"].Number = 10;
  worksheet.Range["B1"].Number = 20;

  //Set formula
  worksheet.Range["C1"].Formula = "=SUM(A1:B1)";

  //Enable sheet calculations
  worksheet.EnableSheetCalculations();

  //Get the claculated value of formula
  string value = worksheet.Range["C1"].CalculatedValue;

  //Saving the Excel to the MemoryStream 
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  //Set the position as '0'
  stream.Position = 0;

  //Download the PDF file in the browser
  FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/excel");
  fileStreamResult.FileDownloadName = "Output.xlsx";
  return fileStreamResult;
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set values
  worksheet.Range["A1"].Number = 10;
  worksheet.Range["B1"].Number = 20;

  //Set formula
  worksheet.Range["C1"].Formula = "=SUM(A1:B1)";

  //Enable sheet calculations
  worksheet.EnableSheetCalculations();

  //Get the claculated value of formula
  string value = worksheet.Range["C1"].CalculatedValue;

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;
  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", stream);
}
{% endhighlight %}
{% endtabs %}

### Formula Array

To know in detail about **FormulaArray**, please navigate to [https://help.syncfusion.com/file-formats/xlsio/working-with-formulas#array-of-formula](https://help.syncfusion.com/file-formats/xlsio/working-with-formulas#array-of-formula)

### Formula Bool Value

[FormulaBoolValue](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IRange.html#Syncfusion_XlsIO_IRange_FormulaBoolValue) gets the [CalculatedValue](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IRange.html#Syncfusion_XlsIO_IRange_CalculatedValue) of formula as boolean.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set values
  worksheet.Range["A1"].Number = 10;
  worksheet.Range["B1"].Number = 20;

  //Set formula
  worksheet.Range["C1"].Formula = "=SUM(A1:B1)";

  //Set boolean
  worksheet.Range["D1"].Boolean = true;

  //Set formula
  worksheet.Range["E1"].Formula = "=D1";                

  //Enable sheet calculations
  worksheet.EnableSheetCalculations();

  //Get the formula boolean value
  bool value_C1 = worksheet.Range["C1"].FormulaBoolValue;
  bool value_E1 = worksheet.Range["E1"].FormulaBoolValue;

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Set values
  worksheet.Range("A1").Number = 10
  worksheet.Range("B1").Number = 20

  'Set formula
  worksheet.Range("C1").Formula = "=SUM(A1:B1)"

  'Set boolean
  worksheet.Range("D1").Boolean = True

  'Set formula
  worksheet.Range("E1").Formula = "=D1"

  'Enable sheet calculations
  worksheet.EnableSheetCalculations()

  'Get the formula boolean value
  Dim value_C1 As Boolean = worksheet.Range("C1").FormulaBoolValue
  Dim value_E1 As Boolean = worksheet.Range("E1").FormulaBoolValue

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set values
  worksheet.Range["A1"].Number = 10;
  worksheet.Range["B1"].Number = 20;

  //Set formula
  worksheet.Range["C1"].Formula = "=SUM(A1:B1)";

  //Set boolean
  worksheet.Range["D1"].Boolean = true;

  //Set formula
  worksheet.Range["E1"].Formula = "=D1";

  //Enable sheet calculations
  worksheet.EnableSheetCalculations();

  //Get the formula boolean value
  bool value_C1 = worksheet.Range["C1"].FormulaBoolValue;
  bool value_E1 = worksheet.Range["E1"].FormulaBoolValue;

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
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set values
  worksheet.Range["A1"].Number = 10;
  worksheet.Range["B1"].Number = 20;

  //Set formula
  worksheet.Range["C1"].Formula = "=SUM(A1:B1)";

  //Set boolean
  worksheet.Range["D1"].Boolean = true;

  //Set formula
  worksheet.Range["E1"].Formula = "=D1";

  //Enable sheet calculations
  worksheet.EnableSheetCalculations();

  //Get the formula boolean value
  bool value_C1 = worksheet.Range["C1"].FormulaBoolValue;
  bool value_E1 = worksheet.Range["E1"].FormulaBoolValue;

  //Saving the Excel to the MemoryStream 
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  //Set the position as '0'
  stream.Position = 0;

  //Download the PDF file in the browser
  FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/excel");
  fileStreamResult.FileDownloadName = "Output.xlsx";
  return fileStreamResult;
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set values
  worksheet.Range["A1"].Number = 10;
  worksheet.Range["B1"].Number = 20;

  //Set formula
  worksheet.Range["C1"].Formula = "=SUM(A1:B1)";

  //Set boolean
  worksheet.Range["D1"].Boolean = true;

  //Set formula
  worksheet.Range["E1"].Formula = "=D1";

  //Enable sheet calculations
  worksheet.EnableSheetCalculations();

  //Get the formula boolean value
  bool value_C1 = worksheet.Range["C1"].FormulaBoolValue;
  bool value_E1 = worksheet.Range["E1"].FormulaBoolValue;

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;
  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", stream);
}
{% endhighlight %}
{% endtabs %}

### Has Boolean

[HasBoolean](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IRange.html#Syncfusion_XlsIO_IRange_HasBoolean) returns whether the range has boolean value.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set values
  worksheet.Range["A1"].Boolean = true;
  worksheet.Range["A2"].Number = 10;
  worksheet.Range["A3"].Value2 = true;

  //Get if the cell has boolean value
  bool hasBoolean_A1 = worksheet.Range["A1"].HasBoolean;
  bool hasBoolean_A2 = worksheet.Range["A2"].HasBoolean;
  bool hasBoolean_A3 = worksheet.Range["A3"].HasBoolean;

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Set values
  worksheet.Range("A1").Boolean = True
  worksheet.Range("A2").Number = 10
  worksheet.Range("A3").Value2 = True

  'Get if the cell has boolean value
  Dim hasBoolean_A1 As Boolean = worksheet.Range("A1").HasBoolean
  Dim hasBoolean_A2 As Boolean = worksheet.Range("A2").HasBoolean
  Dim hasBoolean_A3 As Boolean = worksheet.Range("A3").HasBoolean

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set values
  worksheet.Range["A1"].Boolean = true;
  worksheet.Range["A2"].Number = 10;
  worksheet.Range["A3"].Value2 = true;

  //Get if the cell has boolean value
  bool hasBoolean_A1 = worksheet.Range["A1"].HasBoolean;
  bool hasBoolean_A2 = worksheet.Range["A2"].HasBoolean;
  bool hasBoolean_A3 = worksheet.Range["A3"].HasBoolean;

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
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set values
  worksheet.Range["A1"].Boolean = true;
  worksheet.Range["A2"].Number = 10;
  worksheet.Range["A3"].Value2 = true;

  //Get if the cell has boolean value
  bool hasBoolean_A1 = worksheet.Range["A1"].HasBoolean;
  bool hasBoolean_A2 = worksheet.Range["A2"].HasBoolean;
  bool hasBoolean_A3 = worksheet.Range["A3"].HasBoolean;

  //Saving the Excel to the MemoryStream 
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  //Set the position as '0'
  stream.Position = 0;

  //Download the PDF file in the browser
  FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/excel");
  fileStreamResult.FileDownloadName = "Output.xlsx";
  return fileStreamResult;
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set values
  worksheet.Range["A1"].Boolean = true;
  worksheet.Range["A2"].Number = 10;
  worksheet.Range["A3"].Value2 = true;

  //Get if the cell has boolean value
  bool hasBoolean_A1 = worksheet.Range["A1"].HasBoolean;
  bool hasBoolean_A2 = worksheet.Range["A2"].HasBoolean;
  bool hasBoolean_A3 = worksheet.Range["A3"].HasBoolean;

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;
  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", stream);
}
{% endhighlight %}
{% endtabs %}

### Has DataValidation

The following code snippet explains the behavior of [HasDataValidation](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IRange.html#Syncfusion_XlsIO_IRange_HasDataValidation) property.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Data Validation for Text Length
  IDataValidation txtLengthValidation = worksheet.Range["A3"].DataValidation;
  worksheet.Range["A1"].Text = "Enter the Text in A3";
  worksheet.Range["A1"].AutofitColumns();
  txtLengthValidation.AllowType = ExcelDataType.TextLength;
  txtLengthValidation.CompareOperator = ExcelDataValidationComparisonOperator.Between;
  txtLengthValidation.FirstFormula = "0";
  txtLengthValidation.SecondFormula = "5";

  bool validation_A1 = worksheet.Range["A1"].HasDataValidation;
  bool validation_A3 = worksheet.Range["A3"].HasDataValidation;

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Data Validation for Text Length
  Dim txtLengthValidation As IDataValidation = worksheet.Range("A3").DataValidation
  worksheet.Range("A1").Text = "Enter the Text in A3"
  worksheet.Range("A1").AutofitColumns()
  txtLengthValidation.AllowType = ExcelDataType.TextLength
  txtLengthValidation.CompareOperator = ExcelDataValidationComparisonOperator.Between
  txtLengthValidation.FirstFormula = "0"
  txtLengthValidation.SecondFormula = "5"

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Data Validation for Text Length
  IDataValidation txtLengthValidation = worksheet.Range["A3"].DataValidation;
  worksheet.Range["A1"].Text = "Enter the Text in A3";
  worksheet.Range["A1"].AutofitColumns();
  txtLengthValidation.AllowType = ExcelDataType.TextLength;
  txtLengthValidation.CompareOperator = ExcelDataValidationComparisonOperator.Between;
  txtLengthValidation.FirstFormula = "0";
  txtLengthValidation.SecondFormula = "5";

  bool validation_A1 = worksheet.Range["A1"].HasDataValidation;
  bool validation_A3 = worksheet.Range["A3"].HasDataValidation;

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
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Data Validation for Text Length
  IDataValidation txtLengthValidation = worksheet.Range["A3"].DataValidation;
  worksheet.Range["A1"].Text = "Enter the Text in A3";
  worksheet.Range["A1"].AutofitColumns();
  txtLengthValidation.AllowType = ExcelDataType.TextLength;
  txtLengthValidation.CompareOperator = ExcelDataValidationComparisonOperator.Between;
  txtLengthValidation.FirstFormula = "0";
  txtLengthValidation.SecondFormula = "5";

  bool validation_A1 = worksheet.Range["A1"].HasDataValidation;
  bool validation_A3 = worksheet.Range["A3"].HasDataValidation;

  //Saving the Excel to the MemoryStream 
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  //Set the position as '0'
  stream.Position = 0;

  //Download the PDF file in the browser
  FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/excel");
  fileStreamResult.FileDownloadName = "Output.xlsx";
  return fileStreamResult;
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Data Validation for Text Length
  IDataValidation txtLengthValidation = worksheet.Range["A3"].DataValidation;
  worksheet.Range["A1"].Text = "Enter the Text in A3";
  worksheet.Range["A1"].AutofitColumns();
  txtLengthValidation.AllowType = ExcelDataType.TextLength;
  txtLengthValidation.CompareOperator = ExcelDataValidationComparisonOperator.Between;
  txtLengthValidation.FirstFormula = "0";
  txtLengthValidation.SecondFormula = "5";

  bool validation_A1 = worksheet.Range["A1"].HasDataValidation;
  bool validation_A3 = worksheet.Range["A3"].HasDataValidation;

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;
  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", stream);
}
{% endhighlight %}
{% endtabs %}

### Has DateTime

The following code snippet explains the behavior of [HasDateTime](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IRange.html#Syncfusion_XlsIO_IRange_HasDateTime) property.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set value through Value property
  worksheet.Range["B1"].Value = "Hello World";

  //Set date time through DatTime property
  worksheet.Range["B2"].DateTime = DateTime.Now;

  //Set value through Value2 property
  worksheet.Range["B3"].Value2 = "Hello World";

  //Set date time through Value2 property
  worksheet.Range["B4"].Value2 = DateTime.Now;

  bool dateTime_B1 = worksheet.Range["B1"].HasDateTime;
  bool dateTime_B2 = worksheet.Range["B2"].HasDateTime;
  bool dateTime_B3 = worksheet.Range["B3"].HasDateTime;
  bool dateTime_B4 = worksheet.Range["B4"].HasDateTime;

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Set value through Value property
  worksheet.Range("B1").Value = "Hello World"

  'Set date time through DatTime property
  worksheet.Range("B2").DateTime = DateTime.Now

  'Set value through Value2 property
  worksheet.Range("B3").Value2 = "Hello World"

  'Set date time through Value2 property
  worksheet.Range("B4").Value2 = DateTime.Now

  Dim dateTime_B1 As Boolean = worksheet.Range("B1").HasDateTime
  Dim dateTime_B2 As Boolean = worksheet.Range("B2").HasDateTime
  Dim dateTime_B3 As Boolean = worksheet.Range("B3").HasDateTime
  Dim dateTime_B4 As Boolean = worksheet.Range("B4").HasDateTime

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set value through Value property
  worksheet.Range["B1"].Value = "Hello World";

  //Set date time through DatTime property
  worksheet.Range["B2"].DateTime = DateTime.Now;

  //Set value through Value2 property
  worksheet.Range["B3"].Value2 = "Hello World";

  //Set date time through Value2 property
  worksheet.Range["B4"].Value2 = DateTime.Now;

  bool dateTime_B1 = worksheet.Range["B1"].HasDateTime;
  bool dateTime_B2 = worksheet.Range["B2"].HasDateTime;
  bool dateTime_B3 = worksheet.Range["B3"].HasDateTime;
  bool dateTime_B4 = worksheet.Range["B4"].HasDateTime;

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
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set value through Value property
  worksheet.Range["B1"].Value = "Hello World";

  //Set date time through DatTime property
  worksheet.Range["B2"].DateTime = DateTime.Now;

  //Set value through Value2 property
  worksheet.Range["B3"].Value2 = "Hello World";

  //Set date time through Value2 property
  worksheet.Range["B4"].Value2 = DateTime.Now;

  bool dateTime_B1 = worksheet.Range["B1"].HasDateTime;
  bool dateTime_B2 = worksheet.Range["B2"].HasDateTime;
  bool dateTime_B3 = worksheet.Range["B3"].HasDateTime;
  bool dateTime_B4 = worksheet.Range["B4"].HasDateTime;

  //Saving the Excel to the MemoryStream 
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  //Set the position as '0'
  stream.Position = 0;

  //Download the PDF file in the browser
  FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/excel");
  fileStreamResult.FileDownloadName = "Output.xlsx";
  return fileStreamResult;
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set value through Value property
  worksheet.Range["B1"].Value = "Hello World";

  //Set date time through DatTime property
  worksheet.Range["B2"].DateTime = DateTime.Now;

  //Set value through Value2 property
  worksheet.Range["B3"].Value2 = "Hello World";

  //Set date time through Value2 property
  worksheet.Range["B4"].Value2 = DateTime.Now;

  bool dateTime_B1 = worksheet.Range["B1"].HasDateTime;
  bool dateTime_B2 = worksheet.Range["B2"].HasDateTime;
  bool dateTime_B3 = worksheet.Range["B3"].HasDateTime;
  bool dateTime_B4 = worksheet.Range["B4"].HasDateTime;

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;
  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", stream);
}
{% endhighlight %}
{% endtabs %}

### Has External Formula

The following code snippet explains the behavior of [HasExternalFormula](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IRange.html#Syncfusion_XlsIO_IRange_HasExternalFormula) property. 

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set normal external formula
  worksheet.Range["C1"].Formula = "[One.xlsx]Sheet1!$A$1*5";

  //Set normal formula
  worksheet.Range["A2"].Number = 10;
  worksheet.Range["B2"].Number = 20;
  worksheet.Range["C2"].Formula = "=SUM(A2:B2)";

  bool extFormula_C1 = worksheet.Range["C1"].HasExternalFormula;
  bool extFormula_C2 = worksheet.Range["C2"].HasExternalFormula;

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Set normal external formula
  worksheet.Range("C1").Formula = "[One.xlsx]Sheet1!$A$1*5"

  'Set normal formula
  worksheet.Range("A2").Number = 10
  worksheet.Range("B2").Number = 20
  worksheet.Range("C2").Formula = "=SUM(A2:B2)"

  Dim extFormula_C1 As Boolean = worksheet.Range("C1").HasExternalFormula
  Dim extFormula_C2 As Boolean = worksheet.Range("C2").HasExternalFormula

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set normal external formula
  worksheet.Range["C1"].Formula = "[One.xlsx]Sheet1!$A$1*5";

  //Set normal formula
  worksheet.Range["A2"].Number = 10;
  worksheet.Range["B2"].Number = 20;
  worksheet.Range["C2"].Formula = "=SUM(A2:B2)";

  bool extFormula_C1 = worksheet.Range["C1"].HasExternalFormula;
  bool extFormula_C2 = worksheet.Range["C2"].HasExternalFormula;

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
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set normal external formula
  worksheet.Range["C1"].Formula = "[One.xlsx]Sheet1!$A$1*5";

  //Set normal formula
  worksheet.Range["A2"].Number = 10;
  worksheet.Range["B2"].Number = 20;
  worksheet.Range["C2"].Formula = "=SUM(A2:B2)";

  bool extFormula_C1 = worksheet.Range["C1"].HasExternalFormula;
  bool extFormula_C2 = worksheet.Range["C2"].HasExternalFormula;

  //Saving the Excel to the MemoryStream 
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  //Set the position as '0'
  stream.Position = 0;

  //Download the PDF file in the browser
  FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/excel");
  fileStreamResult.FileDownloadName = "Output.xlsx";
  return fileStreamResult;
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set normal external formula
  worksheet.Range["C1"].Formula = "[One.xlsx]Sheet1!$A$1*5";

  //Set normal formula
  worksheet.Range["A2"].Number = 10;
  worksheet.Range["B2"].Number = 20;
  worksheet.Range["C2"].Formula = "=SUM(A2:B2)";

  bool extFormula_C1 = worksheet.Range["C1"].HasExternalFormula;
  bool extFormula_C2 = worksheet.Range["C2"].HasExternalFormula;

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;
  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", stream);
}
{% endhighlight %}
{% endtabs %}

### Has Formula

The following code snippet explains the behavior of [HasFormula](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IRange.html#Syncfusion_XlsIO_IRange_HasFormula) property. 

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set values
  worksheet.Range["A2"].Number = 10;
  worksheet.Range["B2"].Number = 20;

  //Set formula
  worksheet.Range["C2"].Formula = "=SUM(A2:B2)";

  bool formula_A2 = worksheet.Range["A2"].HasFormula;
  bool formula_C2 = worksheet.Range["C2"].HasFormula;

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Set values
  worksheet.Range("A2").Number = 10
  worksheet.Range("B2").Number = 20

  'Set formula
  worksheet.Range("C2").Formula = "=SUM(A2:B2)"

  Dim formula_A2 As Boolean = worksheet.Range("A2").HasFormula
  Dim formula_C2 As Boolean = worksheet.Range("C2").HasFormula

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set values
  worksheet.Range["A2"].Number = 10;
  worksheet.Range["B2"].Number = 20;

  //Set formula
  worksheet.Range["C2"].Formula = "=SUM(A2:B2)";

  bool formula_A2 = worksheet.Range["A2"].HasFormula;
  bool formula_C2 = worksheet.Range["C2"].HasFormula;

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
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set values
  worksheet.Range["A2"].Number = 10;
  worksheet.Range["B2"].Number = 20;

  //Set formula
  worksheet.Range["C2"].Formula = "=SUM(A2:B2)";

  bool formula_A2 = worksheet.Range["A2"].HasFormula;
  bool formula_C2 = worksheet.Range["C2"].HasFormula;

  //Saving the Excel to the MemoryStream 
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  //Set the position as '0'
  stream.Position = 0;

  //Download the PDF file in the browser
  FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/excel");
  fileStreamResult.FileDownloadName = "Output.xlsx";
  return fileStreamResult;
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set values
  worksheet.Range["A2"].Number = 10;
  worksheet.Range["B2"].Number = 20;

  //Set formula
  worksheet.Range["C2"].Formula = "=SUM(A2:B2)";

  bool formula_A2 = worksheet.Range["A2"].HasFormula;
  bool formula_C2 = worksheet.Range["C2"].HasFormula;

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;
  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", stream);
}
{% endhighlight %}
{% endtabs %}

### Has Formula Array

The following code snippet explains the behavior of [HasFormulaArray](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IRange.html#Syncfusion_XlsIO_IRange_HasFormulaArray) property. 

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Assign array formula
  worksheet.Range["A1:D1"].FormulaArray = "{1,2,3,4}";

  //Adding a named range for the range A1 to D1
  worksheet.Names.Add("ArrayRange", worksheet.Range["A1:D1"]);

  //Assign formula array with named range
  worksheet.Range["A2:D2"].FormulaArray = "ArrayRange+100";

  bool formulaArray = worksheet.Range["A1"].HasFormulaArray;

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Assign array formula
  worksheet.Range("A1:D1").FormulaArray = "{1,2,3,4}"

  'Adding a named range for the range A1 to D1
  worksheet.Names.Add("ArrayRange", worksheet.Range("A1:D1"))

  'Assign formula array with named range
  worksheet.Range("A2:D2").FormulaArray = "ArrayRange+100"

  Dim formulaArray As Boolean = worksheet.Range("A1").HasFormulaArray

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Assign array formula
  worksheet.Range["A1:D1"].FormulaArray = "{1,2,3,4}";

  //Adding a named range for the range A1 to D1
  worksheet.Names.Add("ArrayRange", worksheet.Range["A1:D1"]);

  //Assign formula array with named range
  worksheet.Range["A2:D2"].FormulaArray = "ArrayRange+100";

  bool formulaArray = worksheet.Range["A1"].HasFormulaArray;

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
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Assign array formula
  worksheet.Range["A1:D1"].FormulaArray = "{1,2,3,4}";

  //Adding a named range for the range A1 to D1
  worksheet.Names.Add("ArrayRange", worksheet.Range["A1:D1"]);

  //Assign formula array with named range
  worksheet.Range["A2:D2"].FormulaArray = "ArrayRange+100";

  bool formulaArray = worksheet.Range["A1"].HasFormulaArray;

  //Saving the Excel to the MemoryStream 
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  //Set the position as '0'
  stream.Position = 0;

  //Download the PDF file in the browser
  FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/excel");
  fileStreamResult.FileDownloadName = "Output.xlsx";
  return fileStreamResult;
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Assign array formula
  worksheet.Range["A1:D1"].FormulaArray = "{1,2,3,4}";

  //Adding a named range for the range A1 to D1
  worksheet.Names.Add("ArrayRange", worksheet.Range["A1:D1"]);

  //Assign formula array with named range
  worksheet.Range["A2:D2"].FormulaArray = "ArrayRange+100";

  bool formulaArray = worksheet.Range["A1"].HasFormulaArray;

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;
  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", stream);
}
{% endhighlight %}
{% endtabs %}

### Has Formula Bool Value

The following code snippet explains the behavior of [HasFormulaBoolValue](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IRange.html#Syncfusion_XlsIO_IRange_HasFormulaBoolValue) property. 

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set boolean
  worksheet.Range["D1"].Boolean = true;

  //Set formula
  worksheet.Range["E1"].Formula = "=D1";

  //Enable sheet calculations
  worksheet.EnableSheetCalculations();

  //Get the formula boolean value
  bool value_E1 = worksheet.Range["E1"].FormulaBoolValue;

  //Has formula boolean value
  bool hasValue_E1 = worksheet.Range["E1"].HasFormulaBoolValue;

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Set boolean
  worksheet.Range("D1").Boolean = True

  'Set formula
  worksheet.Range("E1").Formula = "=D1"

  'Enable sheet calculations
  worksheet.EnableSheetCalculations()

  'Get the formula boolean value
  Dim value_E1 As Boolean = worksheet.Range("E1").FormulaBoolValue

  'Has formula boolean value
  Dim hasValue_E1 As Boolean = worksheet.Range("E1").HasFormulaBoolValue

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set boolean
  worksheet.Range["D1"].Boolean = true;

  //Set formula
  worksheet.Range["E1"].Formula = "=D1";

  //Enable sheet calculations
  worksheet.EnableSheetCalculations();

  //Get the formula boolean value
  bool value_E1 = worksheet.Range["E1"].FormulaBoolValue;

  //Has formula boolean value
  bool hasValue_E1 = worksheet.Range["E1"].HasFormulaBoolValue;

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
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set boolean
  worksheet.Range["D1"].Boolean = true;

  //Set formula
  worksheet.Range["E1"].Formula = "=D1";

  //Enable sheet calculations
  worksheet.EnableSheetCalculations();

  //Get the formula boolean value
  bool value_E1 = worksheet.Range["E1"].FormulaBoolValue;

  //Has formula boolean value
  bool hasValue_E1 = worksheet.Range["E1"].HasFormulaBoolValue;

  //Saving the Excel to the MemoryStream 
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  //Set the position as '0'
  stream.Position = 0;

  //Download the PDF file in the browser
  FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/excel");
  fileStreamResult.FileDownloadName = "Output.xlsx";
  return fileStreamResult;
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set boolean
  worksheet.Range["D1"].Boolean = true;

  //Set formula
  worksheet.Range["E1"].Formula = "=D1";

  //Enable sheet calculations
  worksheet.EnableSheetCalculations();

  //Get the formula boolean value
  bool value_E1 = worksheet.Range["E1"].FormulaBoolValue;

  //Has formula boolean value
  bool hasValue_E1 = worksheet.Range["E1"].HasFormulaBoolValue;

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;
  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", stream);
}
{% endhighlight %}
{% endtabs %}

### Has Number

[HasNumber](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IRange.html#Syncfusion_XlsIO_IRange_HasNumber) property determines whether the cell has number in it.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set values
  worksheet.Range["A1"].Number = 10;
  worksheet.Range["A2"].Text = "Sample";

  //Has number
  bool hasNumber_A1 = worksheet.Range["A1"].HasNumber;
  bool hasNumber_A2 = worksheet.Range["A2"].HasNumber;

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Set values
  worksheet.Range("A1").Number = 10
  worksheet.Range("A2").Text = "Sample"

  'Has number
  Dim hasNumber_A1 As Boolean = worksheet.Range("A1").HasNumber
  Dim hasNumber_A2 As Boolean = worksheet.Range("A2").HasNumber

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set values
  worksheet.Range["A1"].Number = 10;
  worksheet.Range["A2"].Text = "Sample";

  //Has number
  bool hasNumber_A1 = worksheet.Range["A1"].HasNumber;
  bool hasNumber_A2 = worksheet.Range["A2"].HasNumber;

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
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set values
  worksheet.Range["A1"].Number = 10;
  worksheet.Range["A2"].Text = "Sample";

  //Has number
  bool hasNumber_A1 = worksheet.Range["A1"].HasNumber;
  bool hasNumber_A2 = worksheet.Range["A2"].HasNumber;

  //Saving the Excel to the MemoryStream 
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  //Set the position as '0'
  stream.Position = 0;

  //Download the PDF file in the browser
  FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/excel");
  fileStreamResult.FileDownloadName = "Output.xlsx";
  return fileStreamResult;
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Set values
  worksheet.Range["A1"].Number = 10;
  worksheet.Range["A2"].Text = "Sample";

  //Has number
  bool hasNumber_A1 = worksheet.Range["A1"].HasNumber;
  bool hasNumber_A2 = worksheet.Range["A2"].HasNumber;

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;
  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", stream);
}
{% endhighlight %}
{% endtabs %}

### Has RichText

[HasRichText](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IRange.html#Syncfusion_XlsIO_IRange_HasRichText) property determines whether the cell has rich-text in it.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Add Text
  IRange range = worksheet.Range["A1"];
  range.Text = "RichText";
  IRichTextString richText = range.RichText;

  //Formatting first 4 characters
  IFont redFont = workbook.CreateFont();
  redFont.Bold = true;
  redFont.Italic = true;
  redFont.RGBColor = Color.Red;
  richText.SetFont(0, 3, redFont);

  //Formatting last 4 characters
  IFont blueFont = workbook.CreateFont();
  blueFont.Bold = true;
  blueFont.Italic = true;
  blueFont.RGBColor = Color.Blue;
  richText.SetFont(4, 7, blueFont);

  //Has RichText
  bool hasRichText = worksheet.Range["A1"].HasRichText;

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Add Text
  Dim range As IRange = worksheet.Range("A1")
  range.Text = "RichText"
  Dim richText As IRichTextString = range.RichText

  'Formatting first 4 characters
  Dim redFont As IFont = workbook.CreateFont()
  redFont.Bold = True
  redFont.Italic = True
  redFont.RGBColor = Color.Red
  richText.SetFont(0, 3, redFont)

  'Formatting last 4 characters
  Dim blueFont As IFont = workbook.CreateFont()
  blueFont.Bold = True
  blueFont.Italic = True
  blueFont.RGBColor = Color.Blue
  richText.SetFont(4, 7, blueFont)

  'Has RichText
  Dim hasRichText As Boolean = worksheet.Range("A1").HasRichText

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Add Text
  IRange range = worksheet.Range["A1"];
  range.Text = "RichText";
  IRichTextString richText = range.RichText;

  //Formatting first 4 characters
  IFont redFont = workbook.CreateFont();
  redFont.Bold = true;
  redFont.Italic = true;
  redFont.RGBColor = Color.FromArgb(255, 255, 0, 0);
  richText.SetFont(0, 3, redFont);

  //Formatting last 4 characters
  IFont blueFont = workbook.CreateFont();
  blueFont.Bold = true;
  blueFont.Italic = true;
  blueFont.RGBColor = Color.FromArgb(255, 0, 0, 255);
  richText.SetFont(4, 7, blueFont);

  //Has RichText
  bool hasRichText = worksheet.Range["A1"].HasRichText;

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
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Add Text
  IRange range = worksheet.Range["A1"];
  range.Text = "RichText";
  IRichTextString richText = range.RichText;

  //Formatting first 4 characters
  IFont redFont = workbook.CreateFont();
  redFont.Bold = true;
  redFont.Italic = true;
  redFont.RGBColor = Color.Red;
  richText.SetFont(0, 3, redFont);

  //Formatting last 4 characters
  IFont blueFont = workbook.CreateFont();
  blueFont.Bold = true;
  blueFont.Italic = true;
  blueFont.RGBColor = Color.Blue;
  richText.SetFont(4, 7, blueFont);

  //Has RichText
  bool hasRichText = worksheet.Range["A1"].HasRichText;
  bool hasNumber_A2 = worksheet.Range["A2"].HasNumber;

  //Saving the Excel to the MemoryStream 
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  //Set the position as '0'
  stream.Position = 0;

  //Download the PDF file in the browser
  FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/excel");
  fileStreamResult.FileDownloadName = "Output.xlsx";
  return fileStreamResult;
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Add Text
  IRange range = worksheet.Range["A1"];
  range.Text = "RichText";
  IRichTextString richText = range.RichText;

  //Formatting first 4 characters
  IFont redFont = workbook.CreateFont();
  redFont.Bold = true;
  redFont.Italic = true;
  redFont.RGBColor = Syncfusion.Drawing.Color.Red;
  richText.SetFont(0, 3, redFont);

  //Formatting last 4 characters
  IFont blueFont = workbook.CreateFont();
  blueFont.Bold = true;
  blueFont.Italic = true;
  blueFont.RGBColor = Syncfusion.Drawing.Color.Blue;
  richText.SetFont(4, 7, blueFont);

  //Has RichText
  bool hasRichText = worksheet.Range["A1"].HasRichText;

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;
  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", stream);
}
{% endhighlight %}
{% endtabs %}

To know in detail about RichText, please navigate to [https://help.syncfusion.com/file-formats/xlsio/working-with-cell-or-range-formatting#rich-text-formatting](https://help.syncfusion.com/file-formats/xlsio/working-with-cell-or-range-formatting#rich-text-formatting).
