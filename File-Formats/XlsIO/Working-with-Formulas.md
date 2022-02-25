---
title: Working with Formulas | Syncfusion
description: Learn how to create, read, edit & calculate formula in an Excel file. It provides support for all types of formula that Microsoft Excel supports.
platform: File-formats
control: XlsIO
documentation: UG
---
# Working with Formulas

[Formulas](https://support.office.com/en-ca/article/Overview-of-formulas-7abfda78-eff3-4cc6-b4a7-6350d512d2dc) are entries in Excel that have equations, by which values are calculated. A typical formula might contain cell references, constants, and even functions. 

## Enable and Disable Calculation

To perform calculation in an Excel workbook, it is recommended to invoke **EnableSheetCalculations** method of __IWorksheet__. Enabling this method will initialize [CalcEngine](/file-formats/xlsio/working-with-formulas#calculation-engine) objects and retrieves calculated values of formulas in a worksheet. 

The following code sample illustrates on how to enable worksheet formula calculations.

{% tabs %}  
{% highlight c# %}
IWorksheet sheet = workbook.Worksheets[0];

//Formula calculation is enabled for the sheet
sheet.EnableSheetCalculations();
{% endhighlight %}

{% highlight vb %}
Dim sheet As IWorksheet = workbook.Worksheets(0)

'Formula calculation is enabled for the sheet
sheet.EnableSheetCalculations()
{% endhighlight %}

{% highlight UWP %}
IWorksheet sheet = workbook.Worksheets[0];

//Formula calculation is enabled for the sheet
sheet.EnableSheetCalculations();
{% endhighlight %}

{% highlight ASP.NET Core %}
IWorksheet sheet = workbook.Worksheets[0];

//Formula calculation is enabled for the sheet
sheet.EnableSheetCalculations();
{% endhighlight %}

{% highlight Xamarin %}
IWorksheet sheet = workbook.Worksheets[0];

//Formula calculation is enabled for the sheet
sheet.EnableSheetCalculations();
{% endhighlight %}
{% endtabs %}   

On completion of worksheet calculation, it is recommended to invoke **DisableSheetCalculations** method of __IWorksheet__. This will dispose all the [CalcEngine](/file-formats/xlsio/working-with-formulas#calculation-engine) objects.

The following code sample illustrates on how to disable worksheet formula calculations.

{% tabs %}  
{% highlight c# %}
IWorksheet sheet = workbook.Worksheets[0];

//Formula calculation is disabled for the sheet
sheet.DisableSheetCalculations();
{% endhighlight %}

{% highlight vb %}
Dim sheet As IWorksheet = workbook.Worksheets(0)

'Formula calculation is disabled for the sheet
sheet.DisableSheetCalculations()
{% endhighlight %}

{% highlight UWP %}
IWorksheet sheet = workbook.Worksheets[0];

//Formula calculation is disabled for the sheet
sheet.DisableSheetCalculations();
{% endhighlight %}

{% highlight ASP.NET Core %}
IWorksheet sheet = workbook.Worksheets[0];

//Formula calculation is disabled for the sheet
sheet.DisableSheetCalculations();
{% endhighlight %}

{% highlight Xamarin %}
IWorksheet sheet = workbook.Worksheets[0];

//Formula calculation is disabled for the sheet
sheet.DisableSheetCalculations();
{% endhighlight %}
{% endtabs %}   

## Writing a Formula

In a worksheet, formulas can be entered by using the **Formula** property of IRange instance. Following code example illustrates on how to write a formula.

{% tabs %}  
{% highlight c# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Setting values to the cells
  sheet.Range["A1"].Number = 10;
  sheet.Range["B1"].Number = 10;

  //Setting formula in the cell
  sheet.Range["C1"].Formula = "=SUM(A1,B1)";

  workbook.SaveAs("Formula.xlsx");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Setting values to the cells
  sheet.Range("A1").Number = 10
  sheet.Range("B1").Number = 10

  'Setting formula for the range
  sheet.Range("C1").Formula = "=SUM(A1,B1)"

  workbook.SaveAs("Formula.xlsx")
End Using
{% endhighlight %}

{% highlight UWP %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Setting values to the cells
  sheet.Range["A1"].Number = 10;
  sheet.Range["B1"].Number = 10;

  //Setting formula in the cell
  sheet.Range["C1"].Formula = "=SUM(A1,B1)";

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Formula";
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
  IWorksheet sheet = workbook.Worksheets[0];

  //Setting values to the cells
  sheet.Range["A1"].Number = 10;
  sheet.Range["B1"].Number = 10;

  //Setting formula in the cell
  sheet.Range["C1"].Formula = "=SUM(A1,B1)";

  //Saving the workbook as stream
  FileStream stream = new FileStream("Formula.xlsx", FileMode.Create, FileAccess.ReadWrite);
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
  IWorksheet sheet = workbook.Worksheets[0];

  //Setting values to the cells
  sheet.Range["A1"].Number = 10;
  sheet.Range["B1"].Number = 10;
 
  //Setting formula in the cell
  sheet.Range["C1"].Formula = "=SUM(A1,B1)";

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Formula.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Formula.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

### Formula with Cross-sheet References

XlsIO supports using formulas across worksheets. The following code shows how to apply formula with cross-sheet references.

{% tabs %}  
{% highlight c# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create();
  IWorksheet sheet = workbook.Worksheets[0];

  //Setting formula for the range with cross-sheet reference
  sheet.Range["C2"].Formula = "=SUM(Sheet2!B2,Sheet1!A2)";

  workbook.SaveAs("Formula.xlsx");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create()
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Setting formula for the range with cross-sheet reference
  sheet.Range("C2").Formula = "=SUM(Sheet2!B2,Sheet1!A2)"

  workbook.SaveAs("Formula.xlsx")
End Using
{% endhighlight %}

{% highlight UWP %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create();
  IWorksheet sheet = workbook.Worksheets[0];

  //Setting formula for the range with cross-sheet reference
  sheet.Range["C2"].Formula = "=SUM(Sheet2!B2,Sheet1!A2)";

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Formula";
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
  IWorkbook workbook = application.Workbooks.Create();
  IWorksheet sheet = workbook.Worksheets[0];

  //Setting formula for the range with cross-sheet reference
  sheet.Range["C2"].Formula = "=SUM(Sheet2!B2,Sheet1!A2)";

  //Saving the workbook as stream
  FileStream stream = new FileStream("Formula.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create();
  IWorksheet sheet = workbook.Worksheets[0];

  //Setting formula for the range with cross-sheet reference
  sheet.Range["C2"].Formula = "=SUM(Sheet2!B2,Sheet1!A2)";

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Formula.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Formula.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

## Reading a Formula

Formulas are string values which can be accessed using **Formula** property of __IRange__. If a cell has formula, the **Value** property of __IRange__ will also return the formula as string.

The following code shows how to read a formula.

{% tabs %}  
{% highlight c# %}
//Returns the formula in C1 style notation
string formula = sheet["C1"].Formula;
{% endhighlight %}

{% highlight vb %}
'Returns the formula in C1 style notation
Dim formula as String = sheet("C1").Formula
{% endhighlight %}

{% highlight UWP %}
//Returns the formula in C1 style notation
string formula = sheet["C1"].Formula;
{% endhighlight %}

{% highlight ASP.NET Core %}
//Returns the formula in C1 style notation
string formula = sheet["C1"].Formula;
{% endhighlight %}

{% highlight Xamarin %}
//Returns the formula in C1 style notation
string formula = sheet["C1"].Formula;
{% endhighlight %}
{% endtabs %}   

## Accessing a Calculated value

To evaluate formula, it is must to [enable sheet calculation](/file-formats/xlsio/working-with-formulas#enable-and-disable-calculation) in prior. After enabling the sheet calculation, the formula can be evaluated using **CalculatedValue** of __IRange__, which returns a string value.

The following code shows how to access a calculated value.

{% tabs %}
{% highlight c# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);
  IWorksheet sheet = workbook.Worksheets[0];

  sheet.EnableSheetCalculations();

  //Returns the calculated value of a formula using the most current inputs
  string calculatedValue = sheet["A1"].CalculatedValue;

  sheet.DisableSheetCalculations();

  workbook.SaveAs("Formula.xlsx");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  sheet.EnableSheetCalculations()

  'Returns the calculated value of a formula using the most current inputs
  Dim calculatedValue As String = sheet("C1").CalculatedValue

  sheet.DisableSheetCalculations()

  workbook.SaveAs("Formula.xlsx")
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
  IWorkbook workbook = await application.Workbooks.OpenAsync(file, ExcelOpenType.Automatic);
  IWorksheet sheet = workbook.Worksheets[0];

  sheet.EnableSheetCalculations();

  //Returns the calculated value of a formula using the most current inputs
  string calculatedValue = sheet["C1"].CalculatedValue;

  sheet.DisableSheetCalculations();

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Formula";
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
  IWorkbook workbook = application.Workbooks.Open(fileStream, ExcelOpenType.Automatic);
  IWorksheet sheet = workbook.Worksheets[0];

  sheet.EnableSheetCalculations();

  //Returns the calculated value of a formula using the most current inputs
  string calculatedValue = sheet["C1"].CalculatedValue;

  sheet.DisableSheetCalculations();

  //Saving the workbook as stream
  FileStream stream = new FileStream("Formula.xlsx", FileMode.Create, FileAccess.ReadWrite);
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
  IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelOpenType.Automatic);
  IWorksheet sheet = workbook.Worksheets[0];

  sheet.EnableSheetCalculations();

  //Returns the calculated value of a formula using the most current inputs
  string calculatedValue = sheet["C1"].CalculatedValue;

  sheet.DisableSheetCalculations();

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Formula.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Formula.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

Apart from __CalculatedValue__ property, the evaluated values can be accessed as **bool**, **DateTime** and **double** data types. To obtain updated values of these types, **CalculatedValue** property must be called in prior.

To know more about evaluated values, please refer **IRange** in API section.

The following code shows how to access calculated values in different types.

{% tabs %}  
{% highlight c# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);
  IWorksheet sheet = workbook.Worksheets[0];

  //Previous Value '2'
  sheet["E1"].Number = 3;

  sheet.EnableSheetCalculations();

  //It has formula 'ISEVEN(E1)'
  //Returns the calculated value of a formula as Boolean
  bool B1_PreviousValue = sheet["B1"].FormulaBoolValue;
  string value = sheet.Range["B1"].CalculatedValue;
  bool B1_LatestValue = sheet["B1"].FormulaBoolValue;

  //It has formula 'TODAY()'
  //Returns the calculated value of a formula as DateTime
  DateTime C1_PreviousValue = sheet["C1"].FormulaDateTime;
  value = sheet.Range["C1"].CalculatedValue;
  DateTime C1_LatestValue = sheet["C1"].FormulaDateTime;

  //It has formula '=E1'
  //Returns the calculated value of a formula as double
  double D1_PreviousValue = sheet["D1"].FormulaNumberValue;
  value = sheet.Range["D1"].CalculatedValue;
  double D1_LatestValue = sheet["D1"].FormulaNumberValue;

  sheet.DisableSheetCalculations();

  workbook.SaveAs("Formula.xlsx");
} 

//Output

//B1_PreviousValue - true                     	B1_LatestValue - false
//C1_PreviousValue - {3/27/2018 12:00:00 AM} 	C1_LatestValue - {3/28/2018 12:00:00 AM}
//D1_PreviousValue - 2.0                        D1_LatestValue - 3.0
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Previous Value '2'
  sheet("E1").Number = 3

  sheet.EnableSheetCalculations()

  'It has formula 'ISEVEN(E1)'
  'Returns the calculated value of a formula as Boolean
  Dim B1_PreviousValue As Boolean = sheet("B1").FormulaBoolValue
  Dim value As String = sheet.Range("B1").CalculatedValue
  Dim B1_LatestValue As Boolean = sheet("B1").FormulaBoolValue

  'It has formula 'TODAY()'
  'Returns the calculated value of a formula as DateTime
  Dim C1_PreviousValue As DateTime = sheet("C1").FormulaDateTime
  value = sheet.Range("C1").CalculatedValue
  Dim C1_LatestValue As DateTime = sheet("C1").FormulaDateTime

  'It has formula '=E1'
  'Returns the calculated value of a formula as double
  Dim D1_PreviousValue As Double = sheet("D1").FormulaNumberValue
  value = sheet.Range("D1").CalculatedValue
  Dim D1_LatestValue As Double = sheet("D1").FormulaNumberValue

  sheet.DisableSheetCalculations()

  workbook.SaveAs("Formula.xlsx")
End Using

'Output

'B1_PreviousValue - true                     	B1_LatestValue - false
'C1_PreviousValue - {3/27/2018 12:00:00 AM} 	C1_LatestValue - {3/28/2018 12:00:00 AM}
'D1_PreviousValue - 2.0                        	D1_LatestValue - 3.0
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
  IWorkbook workbook = await application.Workbooks.OpenAsync(file, ExcelOpenType.Automatic);
  IWorksheet sheet = workbook.Worksheets[0];

  //Previous Value '2'
  sheet["E1"].Number = 3;

  sheet.EnableSheetCalculations();

  //It has formula 'ISEVEN(E1)'
  //Returns the calculated value of a formula as Boolean
  bool B1_PreviousValue = sheet["B1"].FormulaBoolValue;
  string value = sheet.Range["B1"].CalculatedValue;
  bool B1_LatestValue = sheet["B1"].FormulaBoolValue;

  //It has formula 'TODAY()'
  //Returns the calculated value of a formula as DateTime
  DateTime C1_PreviousValue = sheet["C1"].FormulaDateTime;
  value = sheet.Range["C1"].CalculatedValue;
  DateTime C1_LatestValue = sheet["C1"].FormulaDateTime;

  //It has formula '=E1'
  //Returns the calculated value of a formula as double
  double D1_PreviousValue = sheet["D1"].FormulaNumberValue;
  value = sheet.Range["D1"].CalculatedValue;
  double D1_LatestValue = sheet["D1"].FormulaNumberValue;

  sheet.DisableSheetCalculations();

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Formula";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  await workbook.SaveAsAsync(storageFile);
}

//Output

//B1_PreviousValue - true                     	B1_LatestValue - false
//C1_PreviousValue - {3/27/2018 12:00:00 AM} 	C1_LatestValue - {3/28/2018 12:00:00 AM}
//D1_PreviousValue - 2.0                        D1_LatestValue - 3.0
{% endhighlight %}

{% highlight ASP.NET Core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream, ExcelOpenType.Automatic);
  IWorksheet sheet = workbook.Worksheets[0];

  //Previous Value '2'
  sheet["E1"].Number = 3;

  sheet.EnableSheetCalculations();

  //It has formula 'ISEVEN(E1)'
  //Returns the calculated value of a formula as Boolean
  bool B1_PreviousValue = sheet["B1"].FormulaBoolValue;
  string value = sheet.Range["B1"].CalculatedValue;
  bool B1_LatestValue = sheet["B1"].FormulaBoolValue;

  //It has formula 'TODAY()'
  //Returns the calculated value of a formula as DateTime
  DateTime C1_PreviousValue = sheet["C1"].FormulaDateTime;
  value = sheet.Range["C1"].CalculatedValue;
  DateTime C1_LatestValue = sheet["C1"].FormulaDateTime;

  //It has formula '=E1'
  //Returns the calculated value of a formula as double
  double D1_PreviousValue = sheet["D1"].FormulaNumberValue;
  value = sheet.Range["D1"].CalculatedValue;
  double D1_LatestValue = sheet["D1"].FormulaNumberValue;

  sheet.DisableSheetCalculations();

  //Saving the workbook as stream
  FileStream stream = new FileStream("Formula.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}

//Output

//B1_PreviousValue - true                     	B1_LatestValue - false
//C1_PreviousValue - {3/27/2018 12:00:00 AM} 	C1_LatestValue - {3/28/2018 12:00:00 AM}
//D1_PreviousValue - 2.0                        D1_LatestValue - 3.0
{% endhighlight %}

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.XlsIO.Samples.Template.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelOpenType.Automatic);
  IWorksheet sheet = workbook.Worksheets[0];

  //Previous Value '2'
  sheet["E1"].Number = 3;

  sheet.EnableSheetCalculations();

  //It has formula 'ISEVEN(E1)'
  //Returns the calculated value of a formula as Boolean
  bool B1_PreviousValue = sheet["B1"].FormulaBoolValue;
  string value = sheet.Range["B1"].CalculatedValue;
  bool B1_LatestValue = sheet["B1"].FormulaBoolValue;

  //It has formula 'TODAY()'
  //Returns the calculated value of a formula as DateTime
  DateTime C1_PreviousValue = sheet["C1"].FormulaDateTime;
  value = sheet.Range["C1"].CalculatedValue;
  DateTime C1_LatestValue = sheet["C1"].FormulaDateTime;

  //It has formula '=E1'
  //Returns the calculated value of a formula as double
  double D1_PreviousValue = sheet["D1"].FormulaNumberValue;
  value = sheet.Range["D1"].CalculatedValue;
  double D1_LatestValue = sheet["D1"].FormulaNumberValue;

  sheet.DisableSheetCalculations();

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Formula.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Formula.xlsx", "application/msexcel", stream);
  }
}

//Output

//B1_PreviousValue - true                     	B1_LatestValue - false
//C1_PreviousValue - {3/27/2018 12:00:00 AM} 	C1_LatestValue - {3/28/2018 12:00:00 AM}
//D1_PreviousValue - 2.0                        D1_LatestValue - 3.0
{% endhighlight %}
{% endtabs %}

N> Calculated value for external reference formulas can be evaluated in XlsIO.

## Applying Argument Separators Based on Cultures

Formula separators vary for different cultures, and exceptions can be thrown in such cases. This can be overcome by setting the separators by using **SetSeparators** method of __IWorkbook__.

Following code illustrates on how to change the formula separators.

{% tabs %}  
{% highlight c# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Setting the argument separator
  workbook.SetSeparators(';', ',');

  workbook.SaveAs("Formula.xlsx");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)

  'Setting the argument separator
  workbook.SetSeparators(";", ",")

  workbook.SaveAs("Formula.xlsx")
End Using
{% endhighlight %}

{% highlight UWP %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);

  //Setting the argument separator
  workbook.SetSeparators(';', ',');

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Formula";
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

  //Setting the argument separator
  workbook.SetSeparators(';', ',');

  //Saving the workbook as stream
  FileStream stream = new FileStream("Formula.xlsx", FileMode.Create, FileAccess.ReadWrite);
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

  //Setting the argument separator
  workbook.SetSeparators(';', ',');

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Formula.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Formula.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

## Array of Formula

Array formula is a special type of formula in Excel. It works with an array or series of data values, rather than a single data value which can be done through **FormulaArray** property of __IRange__ instance.

Following code shows how an array of values from [Named Range](/file-formats/xlsio/working-with-formulas#defined-names) is used for computation. 

{% tabs %}  
{% highlight c# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Assign array formula
  sheet.Range["A1:D1"].FormulaArray = "{1,2,3,4}";

  //Adding a named range for the range A1 to D1
  sheet.Names.Add("ArrayRange", sheet.Range["A1:D1"]);

  //Assign formula array with named range
  sheet.Range["A2:D2"].FormulaArray = "ArrayRange+100";

  string fileName = "FormulaArray.xlsx";
  workbook.SaveAs(fileName);
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Assign array formula
  sheet.Range("A1:D1").FormulaArray = "{1,2,3,4}"

  'Adding a named range for the range A1 to D1
  sheet.Names.Add("ArrayRange", sheet.Range("A1:D1"))

  'Assign formula array with named range
  sheet.Range("A2:D2").FormulaArray = "ArrayRange+100"

  workbook.SaveAs("FormulaArray.xlsx")
End Using
{% endhighlight %}

{% highlight UWP %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Assign array formula
  sheet.Range["A1:D1"].FormulaArray = "{1,2,3,4}";

  //Adding a named range for the range A1 to D1
  sheet.Names.Add("ArrayRange", sheet.Range["A1:D1"]);

  //Assign formula array with named range
  sheet.Range["A2:D2"].FormulaArray = "ArrayRange+100";

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "FormulaArray";
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
  IWorksheet sheet = workbook.Worksheets[0];

  //Assign array formula
  sheet.Range["A1:D1"].FormulaArray = "{1,2,3,4}";

  //Adding a named range for the range A1 to D1
  sheet.Names.Add("ArrayRange", sheet.Range["A1:D1"]);

  //Assign formula array with named range
  sheet.Range["A2:D2"].FormulaArray = "ArrayRange+100";

  //Saving the workbook as stream
  FileStream stream = new FileStream("FormulaArray.xlsx", FileMode.Create, FileAccess.ReadWrite);
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
  IWorksheet sheet = workbook.Worksheets[0];

  //Assign array formula
  sheet.Range["A1:D1"].FormulaArray = "{1,2,3,4}";

  //Adding a named range for the range A1 to D1
  sheet.Names.Add("ArrayRange", sheet.Range["A1:D1"]);

  //Assign formula array with named range
  sheet.Range["A2:D2"].FormulaArray = "ArrayRange+100";

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("FormulaArray.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("FormulaArray.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

## Incremental Formula

The relative cell references in the formulas are automatically incremented by 1, when you fill formulas down a column or across a row by enabling the EnableIncrementalFormula property of **IApplication** interface.

The below code snippet shows how to increment the cell references by 1 in the formulas.

{% tabs %}  
{% highlight c# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  //Enables the incremental formula to updates the reference in cell
  application.EnableIncrementalFormula = true;

  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Formula are automatically increments by one for the range of cells
  sheet["A1:A5"].Formula = "=B1+C1";

  workbook.SaveAs("IncrementalFormula.xlsx");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013

  'Enables the incremental formula to updates the reference in cell
  application.EnableIncrementalFormula = True

  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Formula are automatically increments by one for the range of cells
  sheet("A1:A5").Formula = "=B1+C1"

  workbook.SaveAs("IncrementalFormula.xlsx")
End Using
{% endhighlight %}

{% highlight UWP %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  //Enables the incremental formula to updates the reference in cell
  application.EnableIncrementalFormula = true;

  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Formula are automatically increments by one for the range of cells
  sheet["A1:A5"].Formula = "=B1+C1";

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "IncrementalFormula";
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

  //Enables the incremental formula to updates the reference in cell
  application.EnableIncrementalFormula = true;

  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Formula are automatically increments by one for the range of cells
  sheet["A1:A5"].Formula = "=B1+C1";

  //Saving the workbook as stream
  FileStream stream = new FileStream("IncrementalFormula.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  //Enables the incremental formula to updates the reference in cell
  application.EnableIncrementalFormula = true;

  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Formula are automatically increments by one for the range of cells
  sheet["A1:A5"].Formula = "=B1+C1";

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("IncrementalFormula.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("IncrementalFormula.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

## External Formula

XlsIO supports to write and preserve external formula.

External formula is the one which refers to a cell or a range of cells or a defined named range from outside the current worksheet/workbook. The main benefit of using an external reference is that whenever the referenced cell(s) in another worksheet changes, the value returned by the external cell reference is automatically updated.

Following code illustrates the insertion of a formula that refers to cell 'A1' in another workbook which is enclosed in a square bracket [One.xlsx].

{% tabs %}  
{% highlight c# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Write an external formula value
  sheet.Range["C1"].Formula = "[One.xlsx]Sheet1!$A$1*5";

  workbook.SaveAs("Formula.xlsx");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Write an external formula value
  sheet.Range("C1").Formula = "[One.xlsx]Sheet1!$A$1*5"

  workbook.SaveAs("Formula.xlsx")
End Using
{% endhighlight %}

{% highlight UWP %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Write an external formula value
  sheet.Range["C1"].Formula = "[One.xlsx]Sheet1!$A$1*5";

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Formula";
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
  IWorksheet sheet = workbook.Worksheets[0];

  //Write an external formula value
  sheet.Range["C1"].Formula = "[One.xlsx]Sheet1!$A$1*5";

  //Saving the workbook as stream
  FileStream stream = new FileStream("Formula.xlsx", FileMode.Create, FileAccess.ReadWrite);
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
  IWorksheet sheet = workbook.Worksheets[0];

  //Write an external formula value
  sheet.Range["C1"].Formula = "[One.xlsx]Sheet1!$A$1*5";

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Formula.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Formula.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

N> Links are updated automatically in Microsoft Excel to view the result for the preceding code.

## Calculated Column

XlsIO supports to create, access and modify [calculated column](https://support.office.com/en-us/article/Create-edit-or-remove-a-calculated-column-in-an-Excel-table-4507b5aa-8859-407c-b3eb-743a2650af3c) in a table. When you enter a formula in a table column, Excel creates a calculated column. This column uses a single formula that’s automatically extended to additional rows in the column and adjusted for each row. You just enter a formula once, and Excel immediately fills it down to create the calculated column.

Also, XlsIO supports [structured reference](https://support.office.com/en-us/article/Use-structured-references-in-Excel-table-formulas-75fb07d3-826a-449c-b76f-363057e3d16f) in calculated column in table from Excel 2013.

The following code snippet illustrates how to create a calculated column.

{% tabs %}  
{% highlight c# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Create Table with data in the given range
  IListObject table = worksheet.ListObjects.Create("Table1", worksheet["A1:D3"]);

  //Create data
  worksheet[1, 1].Text = "Products";
  worksheet[1, 2].Text = "Rate";
  worksheet[1, 3].Text = "Quantity";
  worksheet[1, 4].Text = "Total";

  worksheet[2, 1].Text = "Item1";
  worksheet[2, 2].Number = 200;
  worksheet[2, 3].Number = 2;

  worksheet[3, 1].Text = "Item2";
  worksheet[3, 2].Number = 200;
  worksheet[3, 3].Number = 2;

  //Set table formula
  table.Columns[3].CalculatedFormula = "SUM(20,[Rate]*[Quantity])";

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

  'Create Table with data in the given range
  Dim table As IListObject = worksheet.ListObjects.Create("Table1", worksheet("A1:D3"))

  'Create data
  worksheet(1, 1).Text = "Products"
  worksheet(1, 2).Text = "Rate"
  worksheet(1, 3).Text = "Quantity"
  worksheet(1, 4).Text = "Total"

  worksheet(2, 1).Text = "Item1"
  worksheet(2, 2).Number = 200
  worksheet(2, 3).Number = 2

  worksheet(3, 1).Text = "Item2"
  worksheet(3, 2).Number = 200
  worksheet(3, 3).Number = 2

  'Set table formula
  table.Columns(3).CalculatedFormula = "SUM(20,[Rate]*[Quantity])"

  Dim fileName As String = "Output.xlsx"
  workbook.SaveAs(fileName)
End Using
{% endhighlight %}

{% highlight UWP %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Create Table with data in the given range
  IListObject table = worksheet.ListObjects.Create("Table1", worksheet["A1:D3"]);

  //Create data
  worksheet[1, 1].Text = "Products";
  worksheet[1, 2].Text = "Rate";
  worksheet[1, 3].Text = "Quantity";
  worksheet[1, 4].Text = "Total";

  worksheet[2, 1].Text = "Item1";
  worksheet[2, 2].Number = 200;
  worksheet[2, 3].Number = 2;

  worksheet[3, 1].Text = "Item2";
  worksheet[3, 2].Number = 200;
  worksheet[3, 3].Number = 2;

  //Set table formula
  table.Columns[3].CalculatedFormula = "SUM(20,[Rate]*[Quantity])";

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

{% highlight ASP.NET Core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Create Table with data in the given range
  IListObject table = worksheet.ListObjects.Create("Table1", worksheet["A1:D3"]);

  //Create data
  worksheet[1, 1].Text = "Products";
  worksheet[1, 2].Text = "Rate";
  worksheet[1, 3].Text = "Quantity";
  worksheet[1, 4].Text = "Total";

  worksheet[2, 1].Text = "Item1";
  worksheet[2, 2].Number = 200;
  worksheet[2, 3].Number = 2;

  worksheet[3, 1].Text = "Item2";
  worksheet[3, 2].Number = 200;
  worksheet[3, 3].Number = 2;

  //Set table formula
  table.Columns[3].CalculatedFormula = "SUM(20,[Rate]*[Quantity])";

  //Saving the workbook as stream
  FileStream stream = new FileStream("Output.xlsx", FileMode.Create, FileAccess.ReadWrite);
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

  //Create Table with data in the given range
  IListObject table = worksheet.ListObjects.Create("Table1", worksheet["A1:D3"]);

  //Create data
  worksheet[1, 1].Text = "Products";
  worksheet[1, 2].Text = "Rate";
  worksheet[1, 3].Text = "Quantity";
  worksheet[1, 4].Text = "Total";

  worksheet[2, 1].Text = "Item1";
  worksheet[2, 2].Number = 200;
  worksheet[2, 3].Number = 2;

  worksheet[3, 1].Text = "Item2";
  worksheet[3, 2].Number = 200;
  worksheet[3, 3].Number = 2;

  //Set table formula
  table.Columns[3].CalculatedFormula = "SUM(20,[Rate]*[Quantity])";

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

## Supported Functions

XlsIO supports all the formulas supported by Excel. Whereas, below is the list of functions that XlsIO performs calculation and returns a calculated value.

<table>
<tr>
<th>
Functions<br/><br/></th><th>
Description<br/><br/></th></tr>
<tbody>
<tr>
<td>
ABS<br/><br/></td><td>
Returns the absolute value of a number<br/><br/></td></tr>
<tr>
<td>
ACOS<br/><br/></td><td>
Returns the arccosine of a number<br/><br/></td></tr>
<tr>
<td>
ACOSH<br/><br/></td><td>
Returns the inverse hyperbolic cosine of a number<br/><br/></td></tr>
<tr>
<td>
ADDRESS<br/><br/></td><td>
Returns a reference as text to a single cell in a worksheet<br/><br/></td></tr>
<tr>
<td>
AND<br/><br/></td><td>
Returns TRUE if all of its arguments are TRUE<br/><br/></td></tr>
<tr>
<td>
AREAS<br/><br/></td><td>
Returns the number of areas in a reference<br/><br/></td></tr>
<tr>
<td>
ARRAYTOTEXT<br/><br/></td><td>
Returns the text representation of an array. Calculating the formula result in XlsIO is not supported.<br/><br/></td></tr>
<tr>
<td>
ASC<br/><br/></td><td>
Changes full-width (double-byte) English letters or katakana within a character string to half-width (single-byte) characters<br/><br/></td></tr>
<tr>
<td>
ASIN<br/><br/></td><td>
Returns the arcsine of a number<br/><br/></td></tr>
<tr>
<td>
ASINH<br/><br/></td><td>
Returns the inverse hyperbolic sine of a number<br/><br/></td></tr>
<tr>
<td>
ATAN<br/><br/></td><td>
Returns the arctangent of a number<br/><br/></td></tr>
<tr>
<td>
ATAN2<br/><br/></td><td>
Returns the arctangent from x- and y-coordinates<br/><br/></td></tr>
<tr>
<td>
ATANH<br/><br/></td><td>
Returns the inverse hyperbolic tangent of a number<br/><br/></td></tr>
<tr>
<td>
AVEDEV<br/><br/></td><td>
Returns the average of the absolute deviations of data points from their mean<br/><br/></td></tr>
<tr>
<td>
AVERAGE<br/><br/></td><td>
Returns the average of its arguments<br/><br/></td></tr>
<tr>
<td>
AVERAGEA<br/><br/></td><td>
Returns the average of its arguments, including numbers, text, and logical values<br/><br/></td></tr>
<tr>
<td>
AVERAGEIF<br/><br/></td><td>
Returns the average (arithmetic mean) of all the cells in a range that meet a given criterion<br/><br/></td></tr>
<tr>
<td>
AVERAGEIFS<br/><br/></td><td>
Returns the average (arithmetic mean) of all cells that meet multiple criteria<br/><br/></td></tr>
<tr>
<td>
BESSELI<br/><br/></td><td>
Returns the modified Bessel function In(x)<br/><br/></td></tr>
<tr>
<td>
BESSELJ<br/><br/></td><td>
Returns the Bessel function Jn(x)<br/><br/></td></tr>
<tr>
<td>
BESSELK<br/><br/></td><td>
Returns the modified Bessel function Kn(x)<br/><br/></td></tr>
<tr>
<td>
BESSELY<br/><br/></td><td>
Returns the Bessel function Yn(x)<br/><br/></td></tr>
<tr>
<td>
BIN2DEC<br/><br/></td><td>
Converts a binary number to decimal<br/><br/></td></tr>
<tr>
<td>
BIN2HEX<br/><br/></td><td>
Converts a binary number to hexadecimal<br/><br/></td></tr>
<tr>
<td>
BIN2OCT<br/><br/></td><td>
Converts a binary number to octal<br/><br/></td></tr>
<tr>
<td>
BINOMDIST<br/><br/></td><td>
Returns the individual term binomial distribution probability<br/><br/></td></tr>
<tr>
<td>
CEILING<br/><br/></td><td>
Rounds a number to the nearest integer or to the nearest multiple of significance<br/><br/></td></tr>
<tr>
<td>
CELL<br/><br/></td><td>
Returns information about the formatting, location, or contents of a cell<br/><br/></td></tr>
<tr>
<td>
CHAR<br/><br/></td><td>
Returns the character specified by the code number<br/><br/></td></tr>
<tr>
<td>
CHIDIST<br/><br/></td><td>
Returns the one-tailed probability of the chi-squared distribution<br/><br/></td></tr>
<tr>
<td>
CHIINV<br/><br/></td><td>
Returns the inverse of the one-tailed probability of the chi-squared distribution<br/><br/></td></tr>
<tr>
<td>
CHITEST<br/><br/></td><td>
Returns the test for independence<br/><br/></td></tr>
<tr>
<td>
CHOOSE<br/><br/></td><td>
Chooses a value from a list of values<br/><br/></td></tr>
<tr>
<td>
CLEAN<br/><br/></td><td>
Removes all non-printable characters from text<br/><br/></td></tr>
<tr>
<td>
CODE<br/><br/></td><td>
Returns a numeric code for the first character in a text string<br/><br/></td></tr>
<tr>
<td>
COLUMN<br/><br/></td><td>
Returns the column number of a reference<br/><br/></td></tr>
<tr>
<td>
COLUMNS<br/><br/></td><td>
Returns the number of columns in a reference<br/><br/></td></tr>
<tr>
<td>
COMBIN<br/><br/></td><td>
Returns the number of combinations for a given number of objects<br/><br/></td></tr>
<tr>
<td>
COMPLEX<br/><br/></td><td>
Converts real and imaginary coefficients into a complex number<br/><br/></td></tr>
<tr>
<td>
CONCAT<br/><br/></td><td>
Combines the text from multiple ranges and/or strings<br/><br/></td></tr>
<tr>
<td>
CONCATENATE<br/><br/></td><td>
Joins several text items into one text item<br/><br/></td></tr>
<tr>
<td>
CONFIDENCE<br/><br/></td><td>
Returns the confidence interval for a population mean<br/><br/></td></tr>
<tr>
<td>
CONVERT<br/><br/></td><td>
Converts a number from one measurement system to another<br/><br/></td></tr>
<tr>
<td>
CORREL<br/><br/></td><td>
Returns the correlation coefficient between two data sets<br/><br/></td></tr>
<tr>
<td>
COS<br/><br/></td><td>
Returns the cosine of a number<br/><br/></td></tr>
<tr>
<td>
COSH<br/><br/></td><td>
Returns the hyperbolic cosine of a number<br/><br/></td></tr>
<tr>
<td>
COUNT<br/><br/></td><td>
Counts how many numbers are in the list of arguments<br/><br/></td></tr>
<tr>
<td>
COUNTA<br/><br/></td><td>
Counts how many values are in the list of arguments<br/><br/></td></tr>
<tr>
<td>
COUNTBLANK<br/><br/></td><td>
Counts the number of blank cells within a range<br/><br/></td></tr>
<tr>
<td>
COUNTIF<br/><br/></td><td>
Counts the number of non-blank cells within a range that meet the given criteria<br/><br/></td></tr>
<tr>
<td>
COVAR<br/><br/></td><td>
Returns covariance, the average of the products of paired deviations<br/><br/></td></tr>
<tr>
<td>
CRITBINOM<br/><br/></td><td>
Returns the smallest value for which the cumulative binomial distribution is less than or equal to a criterion value<br/><br/></td></tr>
<tr>
<td>
CUMIPMT<br/><br/></td><td>
Returns the cumulative interest paid between two periods<br/><br/></td></tr>
<tr>
<td>
CUMPRINC<br/><br/></td><td>
Returns the cumulative principal paid on a loan between two periods<br/><br/></td></tr>
<tr>
<td>
DATE<br/><br/></td><td>
Returns the serial number of a particular date<br/><br/></td></tr>
<tr>
<td>
DATEVALUE<br/><br/></td><td>
Converts a date in the form of text to a serial number<br/><br/></td></tr>
<tr>
<td>
DAY<br/><br/></td><td>
Converts a serial number to a day of the month<br/><br/></td></tr>
<tr>
<td>
DAYS360<br/><br/></td><td>
Calculates the number of days between two dates based on a 360-day year<br/><br/></td></tr>
<tr>
<td>
DB<br/><br/></td><td>
Returns the depreciation of an asset for a specified period by using the fixed-declining balance method<br/><br/></td></tr>
<tr>
<td>
DDB<br/><br/></td><td>
Returns the depreciation of an asset for a specified period by using the double-declining balance method or some other method that you specify<br/><br/></td></tr>
<tr>
<td>
DEC2BIN<br/><br/></td><td>
Converts a decimal number to binary<br/><br/></td></tr>
<tr>
<td>
DECHEX<br/><br/></td><td>
Converts a decimal number to hexadecimal<br/><br/></td></tr>
<tr>
<td>
DEC2OCT<br/><br/></td><td>
Converts a decimal number to octal<br/><br/></td></tr>
<tr>
<td>
DEGREES<br/><br/></td><td>
Converts radians to degrees<br/><br/></td></tr>
<tr>
<td>
DELTA<br/><br/></td><td>
Tests whether two values are equal<br/><br/></td></tr>
<tr>
<td>
DEVSQ<br/><br/></td><td>
Returns the sum of squares of deviations<br/><br/></td></tr>
<tr>
<td>
DISC<br/><br/></td><td>
Returns the discount rate for a security<br/><br/></td></tr>
<tr>
<td>
DOLLAR<br/><br/></td><td>
Converts a number to text, using the $ (dollar) currency format<br/><br/></td></tr>
<tr>
<td>
DOLLARDE<br/><br/></td><td>
Converts a dollar price, expressed as a fraction, into a dollar price, expressed as a decimal number<br/><br/></td></tr>
<tr>
<td>
DOLLARFR<br/><br/></td><td>
Converts a dollar price, expressed as a decimal number, into a dollar price, expressed as a fraction<br/><br/></td></tr>
<tr>
<td>
DURATION<br/><br/></td><td>
Returns the annual duration of a security with periodic interest payments<br/><br/></td></tr>
<tr>
<td>
EDATE<br/><br/></td><td>
Returns the serial number of the date that is the indicated number of months before or after the start date<br/><br/></td></tr>
<tr>
<td>
EFFECT<br/><br/></td><td>
Returns the effective annual interest rate<br/><br/></td></tr>
<tr>
<td>
EOMONTH<br/><br/></td><td>
Returns the serial number of the last day of the month before or after a specified number of months<br/><br/></td></tr>
<tr>
<td>
ERF<br/><br/></td><td>
Returns the error function<br/><br/></td></tr>
<tr>
<td>
ERFC<br/><br/></td><td>
Returns the complementary error function<br/><br/></td></tr>
<tr>
<td>
ERROR.TYPE<br/><br/></td><td>
Returns a number corresponding to an error type<br/><br/></td></tr>
<tr>
<td>
EVEN<br/><br/></td><td>
Rounds a number up to the nearest even integer<br/><br/></td></tr>
<tr>
<td>
EXACT<br/><br/></td><td>
Checks to see if two text values are identical<br/><br/></td></tr>
<tr>
<td>
EXP<br/><br/></td><td>
Returns {{'__e__ '| markdownify }}raised to the power of a given number<br/><br/></td></tr>
<tr>
<td>
EXPONDIST<br/><br/></td><td>
Returns the exponential distribution<br/><br/></td></tr>
<tr>
<td>
FACT<br/><br/></td><td>
Returns the factorial of a number<br/><br/></td></tr>
<tr>
<td>
FACTDOUBLE<br/><br/></td><td>
Returns the double factorial of a number<br/><br/></td></tr>
<tr>
<td>
FDIST<br/><br/></td><td>
Returns the F probability distribution<br/><br/></td></tr>
<tr>
<td>
FIND, FINDB<br/><br/></td><td>
Finds one text value within another (case-sensitive)<br/><br/></td></tr>
<tr>
<td>
FINV<br/><br/></td><td>
Returns the inverse of the F probability distribution<br/><br/></td></tr>
<tr>
<td>
FISHER<br/><br/></td><td>
Returns the Fisher transformation<br/><br/></td></tr>
<tr>
<td>
FISHER<br/><br/></td><td>
Returns the inverse of the Fisher transformation<br/><br/></td></tr>
<tr>
<td>
FIXED<br/><br/></td><td>
Formats a number as text with a fixed number of decimals<br/><br/></td></tr>
<tr>
<td>
FLOOR<br/><br/></td><td>
Rounds a number down, toward zero<br/><br/></td></tr>
<tr>
<td>
FORECAST<br/><br/></td><td>
Returns a value along a linear trend<br/><br/></td></tr>
<tr>
<td>
FV<br/><br/></td><td>
Returns the future value of an investment<br/><br/></td></tr>
<tr>
<td>
FVSCHEDULE<br/><br/></td><td>
Returns the future value of an initial principal after applying a series of compound interest rates<br/><br/></td></tr>
<tr>
<td>
GAMMADIST<br/><br/></td><td>
Returns the gamma distribution<br/><br/></td></tr>
<tr>
<td>
GAMMAINV<br/><br/></td><td>
Returns the inverse of the gamma cumulative distribution<br/><br/></td></tr>
<tr>
<td>
GAMMALIN<br/><br/></td><td>
Returns the natural logarithm of the gamma function, Γ(x)<br/><br/></td></tr>
<tr>
<td>
GCD<br/><br/></td><td>
Returns the greatest common divisor<br/><br/></td></tr>
<tr>
<td>
GEOMEAN<br/><br/></td><td>
Returns the geometric mean<br/><br/></td></tr>
<tr>
<td>
GESTEP<br/><br/></td><td>
Tests whether a number is greater than a threshold value<br/><br/></td></tr>
<tr>
<td>
GROWTH<br/><br/></td><td>
Returns values along an exponential trend<br/><br/></td></tr>
<tr>
<td>
HARMEAN<br/><br/></td><td>
Returns the harmonic mean<br/><br/></td></tr>
<tr>
<td>
HEX2BIN<br/><br/></td><td>
Converts a hexadecimal number to binary<br/><br/></td></tr>
<tr>
<td>
HEX2DEC<br/><br/></td><td>
Converts a hexadecimal number to decimal<br/><br/></td></tr>
<tr>
<td>
HEX2OCT<br/><br/></td><td>
Converts a hexadecimal number to octal<br/><br/></td></tr>
<tr>
<td>
HLOOKUP<br/><br/></td><td>
Looks in the top row of an array and returns the value of the indicated cell<br/><br/></td></tr>
<tr>
<td>
HOUR<br/><br/></td><td>
Converts a serial number to an hour<br/><br/></td></tr>
<tr>
<td>
HYPERLINK<br/><br/></td><td>
Creates a shortcut or jump that opens a document stored on a network server, an intranet, or the Internet<br/><br/></td></tr>
<tr>
<td>
HYPGEOMDIST<br/><br/></td><td>
Returns the hypergeometric distribution<br/><br/></td></tr>
<tr>
<td>
IF<br/><br/></td><td>
Specifies a logical test to perform<br/><br/></td></tr>
<tr>
<td>
IFERROR<br/><br/></td><td>
Returns a specified value if a formula evaluates to an error.<br/><br/></td></tr>
<tr>
<td>
IFS<br/><br/></td><td>
Checks whether one or more conditions are met and returns a value that corresponds to the first TRUE condition<br/><br/></td></tr>
<tr>
<td>
IMABS<br/><br/></td><td>
Returns the absolute value (modulus) of a complex number<br/><br/></td></tr>
<tr>
<td>
IMAGINARY<br/><br/></td><td>
Returns the imaginary coefficient of a complex number<br/><br/></td></tr>
<tr>
<td>
IMARGUMENT<br/><br/></td><td>
Returns the argument theta, an angle expressed in radians<br/><br/></td></tr>
<tr>
<td>
IMCONJUGATE<br/><br/></td><td>
Returns the complex conjugate of a complex number<br/><br/></td></tr>
<tr>
<td>
IMCOS<br/><br/></td><td>
Returns the cosine of a complex number<br/><br/></td></tr>
<tr>
<td>
IMDIV<br/><br/></td><td>
Returns the quotient of two complex numbers<br/><br/></td></tr>
<tr>
<td>
IMEXP<br/><br/></td><td>
Returns the exponential of a complex number<br/><br/></td></tr>
<tr>
<td>
IMLN<br/><br/></td><td>
Returns the natural logarithm of a complex number<br/><br/></td></tr>
<tr>
<td>
IMLOG10<br/><br/></td><td>
Returns the base-10 logarithm of a complex number<br/><br/></td></tr>
<tr>
<td>
IMLOG2<br/><br/></td><td>
Returns the base-2 logarithm of a complex number<br/><br/></td></tr>
<tr>
<td>
IMPOWER<br/><br/></td><td>
Returns a complex number raised to an integer power<br/><br/></td></tr>
<tr>
<td>
IMPRODUCT<br/><br/></td><td>
Returns the product of from 2 to 29 complex numbers<br/><br/></td></tr>
<tr>
<td>
IMREAL<br/><br/></td><td>
Returns the real coefficient of a complex number<br/><br/></td></tr>
<tr>
<td>
IMSIN<br/><br/></td><td>
Returns the sine of a complex number<br/><br/></td></tr>
<tr>
<td>
IMSQRT<br/><br/></td><td>
Returns the square root of a complex number<br/><br/></td></tr>
<tr>
<td>
IMSUB<br/><br/></td><td>
Returns the difference between two complex numbers<br/><br/></td></tr>
<tr>
<td>
IMSUM<br/><br/></td><td>
Returns the sum of complex numbers<br/><br/></td></tr>
<tr>
<td>
INDEX<br/><br/></td><td>
Uses an index to choose a value from a reference or array<br/><br/></td></tr>
<tr>
<td>
INDIRECT<br/><br/></td><td>
Returns a reference indicated by a text value<br/><br/></td></tr>
<tr>
<td>
INFO<br/><br/></td><td>
Returns information about the current operating environment<br/><br/></td></tr>
<tr>
<td>
INT<br/><br/></td><td>
Rounds a number down to the nearest integer<br/><br/></td></tr>
<tr>
<td>
INTERCEPT<br/><br/></td><td>
Returns the intercept of the linear regression line<br/><br/></td></tr>
<tr>
<td>
INTRATE<br/><br/></td><td>
Returns the interest rate for a fully invested security<br/><br/></td></tr>
<tr>
<td>
IPMT<br/><br/></td><td>
Returns the interest payment for an investment for a given period<br/><br/></td></tr>
<tr>
<td>
IRR<br/><br/></td><td>
Returns the internal rate of return for a series of cash flows<br/><br/></td></tr>
<tr>
<td>
ISBLANK<br/><br/></td><td>
Returns TRUE if the value is blank<br/><br/></td></tr>
<tr>
<td>
ISERR<br/><br/></td><td>
Returns TRUE if the value is any error value except #N/A<br/><br/></td></tr>
<tr>
<td>
ISERROR<br/><br/></td><td>
Returns TRUE if the value is any error value<br/><br/></td></tr>
<tr>
<td>
ISEVEN<br/><br/></td><td>
Returns TRUE if the number is even<br/><br/></td></tr>
<tr>
<td>
ISLOGICAL<br/><br/></td><td>
Returns TRUE if the value is a logical value<br/><br/></td></tr>
<tr>
<td>
ISAN<br/><br/></td><td>
Returns TRUE if the value is the #N/A error value<br/><br/></td></tr>
<tr>
<td>
ISNONTEXT<br/><br/></td><td>
Returns TRUE if the value is not text<br/><br/></td></tr>
<tr>
<td>
ISNUMBER<br/><br/></td><td>
Returns TRUE if the value is a number<br/><br/></td></tr>
<tr>
<td>
ISODD<br/><br/></td><td>
Returns TRUE if the number is odd<br/><br/></td></tr>
<tr>
<td>
ISMPT<br/><br/></td><td>
Calculates the interest paid during a specific period of an investment<br/><br/></td></tr>
<tr>
<td>
ISREF<br/><br/></td><td>
Returns TRUE if the value is a reference<br/><br/></td></tr>
<tr>
<td>
ISTEXT<br/><br/></td><td>
Returns TRUE if the value is text<br/><br/></td></tr>
<tr>
<td>
KURT<br/><br/></td><td>
Returns the kurtosis of a data set<br/><br/></td></tr>
<tr>
<td>
LARGE<br/><br/></td><td>
Returns the k-th largest value in a data set<br/><br/></td></tr>
<tr>
<td>
LCM<br/><br/></td><td>
Returns the least common multiple<br/><br/></td></tr>
<tr>
<td>
LEFT, LEFTB<br/><br/></td><td>
Returns the leftmost characters from a text value<br/><br/></td></tr>
<tr>
<td>
LET<br/><br/></td><td>
Returns the result of a formula that can use variables. Calculating the formula result in XlsIO is not supported.<br/><br/></td></tr>
<tr>
<td>
LEN, LENB<br/><br/></td><td>
Returns the number of characters in a text string<br/><br/></td></tr>
<tr>
<td>
LN<br/><br/></td><td>
Returns the natural logarithm of a number<br/><br/></td></tr>
<tr>
<td>
LOG<br/><br/></td><td>
Returns the logarithm of a number to a specified base<br/><br/></td></tr>
<tr>
<td>
LOG10<br/><br/></td><td>
Returns the base-10 logarithm of a number<br/><br/></td></tr>
<tr>
<td>
LOGEST<br/><br/></td><td>
Returns the parameters of an exponential trend<br/><br/></td></tr>
<tr>
<td>
LOGINV<br/><br/></td><td>
Returns the inverse of the log-normal distribution<br/><br/></td></tr>
<tr>
<td>
LOGNORMDIST<br/><br/></td><td>
Returns the cumulative log-normal distribution<br/><br/></td></tr>
<tr>
<td>
LOOKUP<br/><br/></td><td>
Looks up values in a vector or array<br/><br/></td></tr>
<tr>
<td>
LOWER<br/><br/></td><td>
Converts text to lowercase<br/><br/></td></tr>
<tr>
<td>
MATCH<br/><br/></td><td>
Looks up values in a reference or array<br/><br/></td></tr>
<tr>
<td>
MAX<br/><br/></td><td>
Returns the maximum value in a list of arguments<br/><br/></td></tr>
<tr>
<td>
MAXA<br/><br/></td><td>
Returns the maximum value in a list of arguments, including numbers, text, and logical values<br/><br/></td></tr>
<tr>
<td>
MAXIFS<br/><br/></td><td>
Returns the maximum value among cells specified by a given set of conditions or criteria<br/><br/></td></tr>
<tr>
<td>
MDETERM<br/><br/></td><td>
Returns the matrix determinant of an array<br/><br/></td></tr>
<tr>
<td>
MEDIAN<br/><br/></td><td>
Returns the median of the given numbers<br/><br/></td></tr>
<tr>
<td>
MID, MIDB<br/><br/></td><td>
Returns a specific number of characters from a text string starting at the position you specify<br/><br/></td></tr>
<tr>
<td>
MIN<br/><br/></td><td>
Returns the minimum value in a list of arguments<br/><br/></td></tr>
<tr>
<td>
MINA<br/><br/></td><td>
Returns the smallest value in a list of arguments, including numbers, text, and logical values<br/><br/></td></tr>
<tr>
<td>
MINIFS<br/><br/></td><td>
Returns the minimum value among cells specified by a given set of conditions or criteria<br/><br/></td></tr>
<tr>
<td>
MINUTE<br/><br/></td><td>
Converts a serial number to a minute<br/><br/></td></tr>
<tr>
<td>
MINVERSE<br/><br/></td><td>
Returns the matrix inverse of an array<br/><br/></td></tr>
<tr>
<td>
MIRR<br/><br/></td><td>
Returns the internal rate of return where positive and negative cash flows are financed at different rates<br/><br/></td></tr>
<tr>
<td>
MMULT<br/><br/></td><td>
Returns the matrix product of two arrays<br/><br/></td></tr>
<tr>
<td>
MOD<br/><br/></td><td>
Returns the remainder from division<br/><br/></td></tr>
<tr>
<td>
MODE<br/><br/></td><td>
Returns the most common value in a data set<br/><br/></td></tr>
<tr>
<td>
MMONTH<br/><br/></td><td>
Converts a serial number to a month<br/><br/></td></tr>
<tr>
<td>
MROUND<br/><br/></td><td>
Returns a number rounded to the desired multiple<br/><br/></td></tr>
<tr>
<td>
MULTINOMINAL<br/><br/></td><td>
Returns the multinomial of a set of numbers<br/><br/></td></tr>
<tr>
<td>
N<br/><br/></td><td>
Returns a value converted to a number<br/><br/></td></tr>
<tr>
<td>
NA<br/><br/></td><td>
Returns the error value #N/A<br/><br/></td></tr>
<tr>
<td>
NEGBINOMDIST<br/><br/></td><td>
Returns the negative binomial distribution<br/><br/></td></tr>
<tr>
<td>
NETWORKDAYS<br/><br/></td><td>
Returns the number of whole workdays between two dates<br/><br/></td></tr>
<tr>
<td>
NORMDIST<br/><br/></td><td>
Returns the normal cumulative distribution<br/><br/></td></tr>
<tr>
<td>
NORMINV<br/><br/></td><td>
Returns the inverse of the normal cumulative distribution<br/><br/></td></tr>
<tr>
<td>
NORMSDIST<br/><br/></td><td>
Returns the standard normal cumulative distribution<br/><br/></td></tr>
<tr>
<td>
NORMSINV<br/><br/></td><td>
Returns the inverse of the standard normal cumulative distribution<br/><br/></td></tr>
<tr>
<td>
NOT<br/><br/></td><td>
Reverses the logic of its argument<br/><br/></td></tr>
<tr>
<td>
NOW<br/><br/></td><td>
Returns the serial number of the current date and time<br/><br/></td></tr>
<tr>
<td>
NPER<br/><br/></td><td>
Returns the number of periods for an investment<br/><br/></td></tr>
<tr>
<td>
NPV<br/><br/></td><td>
Returns the net present value of an investment based on a series of periodic cash flows and a discount rate<br/><br/></td></tr>
<tr>
<td>
OCT2BIN<br/><br/></td><td>
Converts an octal number to binary<br/><br/></td></tr>
<tr>
<td>
OCT2DEC<br/><br/></td><td>
Converts an octal number to decimal<br/><br/></td></tr>
<tr>
<td>
OCT2HEX<br/><br/></td><td>
Converts an octal number to hexadecimal<br/><br/></td></tr>
<tr>
<td>
ODD<br/><br/></td><td>
Rounds a number up to the nearest odd integer<br/><br/></td></tr>
<tr>
<td>
OFFSET<br/><br/></td><td>
Returns a reference offset from a given reference<br/><br/></td></tr>
<tr>
<td>
OR<br/><br/></td><td>
Returns TRUE if any argument is TRUE<br/><br/></td></tr>
<tr>
<td>
PEARSON<br/><br/></td><td>
Returns the Pearson product moment correlation coefficient<br/><br/></td></tr>
<tr>
<td>
PERCENTILE<br/><br/></td><td>
Returns the k-th percentile of values in a range<br/><br/></td></tr>
<tr>
<td>
PERCENTRANK<br/><br/></td><td>
Returns the percentage rank of a value in a data set<br/><br/></td></tr>
<tr>
<td>
PERMUT<br/><br/></td><td>
Returns the number of permutations for a given number of objects<br/><br/></td></tr>
<tr>
<td>
PI<br/><br/></td><td>
Returns the value of pi<br/><br/></td></tr>
<tr>
<td>
PMT<br/><br/></td><td>
Returns the periodic payment for an annuity<br/><br/></td></tr>
<tr>
<td>
POISSON<br/><br/></td><td>
Returns the Poisson distribution<br/><br/></td></tr>
<tr>
<td>
POWER<br/><br/></td><td>
Returns the result of a number raised to a power<br/><br/></td></tr>
<tr>
<td>
PPMT<br/><br/></td><td>
Returns the payment on the principal for an investment for a given period<br/><br/></td></tr>
<tr>
<td>
PROB<br/><br/></td><td>
Returns the probability that values in a range are between two limits<br/><br/></td></tr>
<tr>
<td>
PRODUCT<br/><br/></td><td>
Multiplies its arguments<br/><br/></td></tr>
<tr>
<td>
PROPER<br/><br/></td><td>
Capitalizes the first letter in each word of a text value<br/><br/></td></tr>
<tr>
<td>
PV<br/><br/></td><td>
Returns the present value of an investment<br/><br/></td></tr>
<tr>
<td>
QUARTILE<br/><br/></td><td>
Returns the quartile of a data set<br/><br/></td></tr>
<tr>
<td>
QUOTIENT<br/><br/></td><td>
Returns the integer portion of a division<br/><br/></td></tr>
<tr>
<td>
RADIANS<br/><br/></td><td>
Converts degrees to radians<br/><br/></td></tr>
<tr>
<td>
RAND<br/><br/></td><td>
Returns a random number between 0 and 1<br/><br/></td></tr>
<tr>
<td>
RANDBETWEEN<br/><br/></td><td>
Returns a random number between the numbers you specify<br/><br/></td></tr>
<tr>
<td>
RANK<br/><br/></td><td>
Returns the rank of a number in a list of numbers<br/><br/></td></tr>
<tr>
<td>
RATE<br/><br/></td><td>
Returns the interest rate per period of an annuity<br/><br/></td></tr>
<tr>
<td>
RECEIVED<br/><br/></td><td>
Returns the amount received at maturity for a fully invested security<br/><br/></td></tr>
<tr>
<td>
REPLACE, REPLACEB<br/><br/></td><td>
Replaces characters within text<br/><br/></td></tr>
<tr>
<td>
REPT<br/><br/></td><td>
Repeats text a given number of times<br/><br/></td></tr>
<tr>
<td>
RIGHT, RIGHTB<br/><br/></td><td>
Returns the rightmost characters from a text value<br/><br/></td></tr>
<tr>
<td>
ROMAN<br/><br/></td><td>
Converts an Arabic numeral to roman, as text<br/><br/></td></tr>
<tr>
<td>
ROUND<br/><br/></td><td>
Rounds a number to a specified number of digits<br/><br/></td></tr>
<tr>
<td>
ROUNDDOWN<br/><br/></td><td>
Rounds a number down, toward zero<br/><br/></td></tr>
<tr>
<td>
ROUNDUP<br/><br/></td><td>
Rounds a number up, away from zero<br/><br/></td></tr>
<tr>
<td>
ROW<br/><br/></td><td>
Returns the row number of a reference<br/><br/></td></tr>
<tr>
<td>
ROWS<br/><br/></td><td>
Returns the number of rows in a reference<br/><br/></td></tr>
<tr>
<td>
RSQ<br/><br/></td><td>
Returns the square of the Pearson product moment correlation coefficient<br/><br/></td></tr>
<tr>
<td>
SEARCH, SEARCHB<br/><br/></td><td>
Finds one text value within another (not case-sensitive)<br/><br/></td></tr>
<tr>
<td>
SECOND<br/><br/></td><td>
Converts a serial number to a second<br/><br/></td></tr>
<tr>
<td>
SERIESSUM<br/><br/></td><td>
Returns the sum of a power series based on the formula<br/><br/></td></tr>
<tr>
<td>
SIGN<br/><br/></td><td>
Returns the sign of a number<br/><br/></td></tr>
<tr>
<td>
SIN<br/><br/></td><td>
Returns the sine of the given angle<br/><br/></td></tr>
<tr>
<td>
SINH<br/><br/></td><td>
Returns the hyperbolic sine of a number<br/><br/></td></tr>
<tr>
<td>
SKEW<br/><br/></td><td>
Returns the skewness of a distribution<br/><br/></td></tr>
<tr>
<td>
SLN<br/><br/></td><td>
Returns the straight-line depreciation of an asset for one period<br/><br/></td></tr>
<tr>
<td>
SLOPE<br/><br/></td><td>
Returns the slope of the linear regression line<br/><br/></td></tr>
<tr>
<td>
SMALL<br/><br/></td><td>
Returns the k-th smallest value in a data set<br/><br/></td></tr>
<tr>
<td>
SQRT<br/><br/></td><td>
Returns a positive square root<br/><br/></td></tr>
<tr>
<td>
SQRTPI<br/><br/></td><td>
Returns the square root of (number * pi)<br/><br/></td></tr>
<tr>
<td>
STANDARDIZE<br/><br/></td><td>
Returns a normalized value<br/><br/></td></tr>
<tr>
<td>
STDEV<br/><br/></td><td>
Estimates standard deviation based on a sample<br/><br/></td></tr>
<tr>
<td>
STDEVA<br/><br/></td><td>
Estimates standard deviation based on a sample, including numbers, text, and logical values<br/><br/></td></tr>
<tr>
<td>
STDEVP<br/><br/></td><td>
Calculates standard deviation based on the entire population<br/><br/></td></tr>
<tr>
<td>
STDEVPA<br/><br/></td><td>
Calculates standard deviation based on the entire population, including numbers, text, and logical values<br/><br/></td></tr>
<tr>
<td>
STEYX<br/><br/></td><td>
Returns the standard error of the predicted y-value for each x in the regression<br/><br/></td></tr>
<tr>
<td>
SUBSTITUTE<br/><br/></td><td>
Substitutes new text for old text in a text string<br/><br/></td></tr>
<tr>
<td>
SUBTOTAL<br/><br/></td><td>
Returns a subtotal in a list or database<br/><br/></td></tr>
<tr>
<td>
SUM<br/><br/></td><td>
Adds its arguments<br/><br/></td></tr>
<tr>
<td>
SUMIF<br/><br/></td><td>
Adds the cells specified by a given criteria<br/><br/></td></tr>
<tr>
<td>
SUMPRODUCT<br/><br/></td><td>
Returns the sum of the products of corresponding array components<br/><br/></td></tr>
<tr>
<td>
SUMSQ<br/><br/></td><td>
Returns the sum of the squares of the arguments<br/><br/></td></tr>
<tr>
<td>
SUMX2MY2<br/><br/></td><td>
Returns the sum of the difference of squares of corresponding values in two arrays<br/><br/></td></tr>
<tr>
<td>
SUMX2PY2<br/><br/></td><td>
Returns the sum of the sum of squares of corresponding values in two arrays<br/><br/></td></tr>
<tr>
<td>
SUMXMY2<br/><br/></td><td>
Returns the sum of squares of differences of corresponding values in two arrays<br/><br/></td></tr>
<tr>
<td>
SWITCH<br/><br/></td><td>
Evaluates an expression against a list of values and returns the result corresponding to the first matching value. If there is no match, an optional default value may be returned.<br/><br/></td></tr>
<tr>
<td>
SYD<br/><br/></td><td>
Returns the sum-of-years'digits depreciation of an asset for a specified period<br/><br/></td></tr>
<tr>
<td>
T<br/><br/></td><td>
Converts its arguments to text<br/><br/></td></tr>
<tr>
<td>
TAN<br/><br/></td><td>
Returns the tangent of a number<br/><br/></td></tr>
<tr>
<td>
TANH<br/><br/></td><td>
Returns the hyperbolic tangent of a number<br/><br/></td></tr>
<tr>
<td>
TEXT<br/><br/></td><td>
Formats a number and converts it to text<br/><br/></td></tr>
<tr>
<td>
TEXTJOIN<br/><br/></td><td>
Combines the text from multiple ranges and/or strings with a delimiter you specify between each text value that will be combined<br/><br/></td></tr>
<tr>
<td>
TIME<br/><br/></td><td>
Returns the serial number of a particular time<br/><br/></td></tr>
<tr>
<td>
TIMEVALUE<br/><br/></td><td>
Converts a time in the form of text to a serial number<br/><br/></td></tr>
<tr>
<td>
TODAY<br/><br/></td><td>
Returns the serial number of today's date<br/><br/></td></tr>
<tr>
<td>
TRANSPORSE<br/><br/></td><td>
Returns the transpose of an array<br/><br/></td></tr>
<tr>
<td>
TRIM<br/><br/></td><td>
Removes spaces from text<br/><br/></td></tr>
<tr>
<td>
TRIMMEAN<br/><br/></td><td>
Returns the mean of the interior of a data set<br/><br/></td></tr>
<tr>
<td>
TRUNC<br/><br/></td><td>
Truncates a number to an integer<br/><br/></td></tr>
<tr>
<td>
TYPE<br/><br/></td><td>
Returns a number indicating the data type of a value<br/><br/></td></tr>
<tr>
<td>
UNIQUE<br/><br/></td><td>
Returns the list of unique values present inside a list or range. Calculating the formula result in XlsIO is not supported. <br/><br/></td></tr>
<tr>
<td>
UPPER<br/><br/></td><td>
Converts text to uppercase<br/><br/></td></tr>
<tr>
<td>
VALUE<br/><br/></td><td>
Converts a text argument to a number<br/><br/></td></tr>
<tr>
<td>
VALUETOTEXT<br/><br/></td><td>
Returns the text from any specified value. Calculating the formula result in XlsIO is not supported.<br/><br/></td></tr>
<tr>
<td>
VAR<br/><br/></td><td>
Estimates variance based on a sample<br/><br/></td></tr>
<tr>
<td>
VARA<br/><br/></td><td>
Estimates variance based on a sample, including numbers, text, and logical values<br/><br/></td></tr>
<tr>
<td>
VARP<br/><br/></td><td>
Calculates variance based on the entire population<br/><br/></td></tr>
<tr>
<td>
VARPA<br/><br/></td><td>
Calculates variance based on the entire population, including numbers, text, and logical values<br/><br/></td></tr>
<tr>
<td>
VDB<br/><br/></td><td>
Returns the depreciation of an asset for a specified or partial period by using a declining balance method<br/><br/></td></tr>
<tr>
<td>
VLOOKUP<br/><br/></td><td>
Looks in the first column of an array and moves across the row to return the value of a cell<br/><br/></td></tr>
<tr>
<td>
WEEKDAY<br/><br/></td><td>
Converts a serial number to a day of the week<br/><br/></td></tr>
<tr>
<td>
WEEKNUM<br/><br/></td><td>
Converts a serial number to a number representing where the week falls numerically with a year<br/><br/></td></tr>
<tr>
<td>
WEIBULL<br/><br/></td><td>
Returns the Weibull distribution<br/><br/></td></tr>
<tr>
<td>
WORKDAY<br/><br/></td><td>
Returns the serial number of the date before or after a specified number of workdays<br/><br/></td></tr>
<tr>
<td>
XIRR<br/><br/></td><td>
Returns the internal rate of return for a schedule of cash flows that is not necessarily periodic<br/><br/></td></tr>
<tr>
<td>
XLOOKUP<br/><br/></td><td>
Returns the value Corresponding to the first match it finds else returns the next approximate match. Calculating the formula result in XlsIO is not supported.<br/><br/></td></tr>
<tr>
<td>
XMATCH<br/><br/></td><td>
Returns the position of a value in a list, table or cell range. Calculating the formula result in XlsIO is not supported.<br/><br/></td></tr>
<tr>
<td>
YEAR<br/><br/></td><td>
Converts a serial number to a year<br/><br/></td></tr>
<tr>
<td>
YEARFRAC<br/><br/></td><td>
Returns the year fraction representing the number of whole days between start_date and end_date<br/><br/></td></tr>
<tr>
<td>
ZTEST<br/><br/></td><td>
Returns the one-tailed probability-value of a z-test<br/><br/></td></tr>
<tr>
<td>
FALSE<br/><br/></td><td>
Returns the logical value FALSE<br/><br/></td></tr>
<tr>
<td>
TRUE<br/><br/></td><td>
Returns the logical value TRUE<br/><br/></td></tr>
</tbody>
</table>

## Add-in Functions

Add-ins are mini-programs or custom functions that enhance the feature set of the Microsoft Excel application. These Add-ins can be accessed by registering it at first from Excel and refer it using XlsIO. For more details on adding AddIn functions, see [Add or remove Add-ins](https://support.office.com/en-ZA/article/add-or-remove-add-ins-64d3d147-98fb-4b82-8833-709d54e3ace1)

The following code illustrates on how to include and access Add-ins in XlsIO.

{% tabs %}  
{% highlight c# %}
//Step1: Create AddIn (AddIn.xlam)
//AddIn.xlam file has the below custom function
//Function AddInFunction(firstValue As Integer, secondValue As Integer) As Integer
//
//Dim result As Integer
//result = firstValue + secondValue
//AddInFunction = result
//
//End Function
//Step2: Register the AddIn in Excel by adding the above file to Excel Application by locating the .xlam file through the menu (Developer -> Add-ins -> Browse)

using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  IAddInFunctions unknownFunctions = workbook.AddInFunctions;

  //Adding the XLAM file reference to AddIn functions
  //NOTE: The add-in name must be same as the function name
  unknownFunctions.Add(@"D:\AddIn.xlam", "AddInFunction");

  //Use the function. The expected result is 30
  sheet.Range["A3"].Formula = "AddInFunction(10,20)";

  string fileName = "AddIn.xlsx";
  workbook.Version = ExcelVersion.Excel2010;
  workbook.SaveAs(fileName);
}
{% endhighlight %}

{% highlight vb %}
'Step1: Create AddIn (AddIn.xlam)
'AddIn.xlam file has the below custom function
'Function AddInFunction(firstValue As Integer, secondValue As Integer) As Integer
'
'Dim result As Integer
'result = firstValue + secondValue
'AddInFunction = result
'
'End Function
'Step2: Register the AddIn in Excel by adding the above file to Excel Application by locating the .xlam file through the menu (Developer -> Add-ins -> Browse)

Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  Dim unknownFunctions As IAddInFunctions = workbook.AddInFunctions

  'Adding the XLAM file reference to AddIn functions
  'NOTE: The add-in name must be same as the function name
  unknownFunctions.Add("D:\AddIn.xlam", "AddInFunction")

  'Use the function. The expected result is 30
  sheet.Range("A3").Formula = "AddInFunction(10,20)"

  Dim fileName As String = "AddIn.xlsx"
  workbook.Version = ExcelVersion.Excel2010
  workbook.SaveAs(fileName)
End Using
{% endhighlight %}

{% highlight UWP %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  IAddInFunctions unknownFunctions = workbook.AddInFunctions;

  //Adding the XLAM file reference to AddIn functions
  //NOTE: The add-in name must be same as the function name
  unknownFunctions.Add("AddInFunction");

  //Use the function. The expected result is 30
  sheet.Range["A3"].Formula = "AddInFunction(10,20)";

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "AddIn";
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
  IWorksheet sheet = workbook.Worksheets[0];

  IAddInFunctions unknownFunctions = workbook.AddInFunctions;

  //Adding the XLAM file reference to AddIn functions
  //NOTE: The add-in name must be same as the function name
  unknownFunctions.Add("AddInFunction");

  //Use the function. The expected result is 30
  sheet.Range["A3"].Formula = "AddInFunction(10,20)";

  //Saving the workbook as stream
  FileStream stream = new FileStream("AddIn.xlsx", FileMode.Create, FileAccess.ReadWrite);
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
  IWorksheet sheet = workbook.Worksheets[0];

  IAddInFunctions unknownFunctions = workbook.AddInFunctions;

  //Adding the XLAM file reference to AddIn functions
  //NOTE: The add-in name must be same as the function name
  unknownFunctions.Add("AddInFunction");

  //Use the function. The expected result is 30
  sheet.Range["A3"].Formula = "AddInFunction(10,20)";

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("AddIn.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("AddIn.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}   

N> If you move the file to another computer, or distribute it, the workbook will expect to find the same Add-In, in the same place, on their computers. But, if the Add-In is moved or deleted from the computer, the workbook won't be able to find it, and your code won't work. Make sure that the Add-In is accessed by locating the .xlam file through the menu (Developer -> Add-ins -> Browse).

## Defined Names

Cell ranges can be [defined by names](https://support.office.com/en-ZA/article/define-and-use-names-in-formulas-b2bacf14-945d-41d4-b3aa-267b18a23f6e) to perform formula calculation. This section explains about creating named ranges and accessing them from workbook or worksheet levels.

The following code shows how to define a named range from workbook level.

{% tabs %}  
{% highlight c# %}
//Defining a name in workbook level for the cell A1
IName name = workbook.Names.Add("BookLevelName"); 
name.RefersToRange = worksheet.Range["A1"];
{% endhighlight %}

{% highlight vb %}
'Defining a name in workbook level for the cell A1
Dim name As IName = workbook.Names.Add("BookLevelName")
name.RefersToRange = worksheet.Range("A1")
{% endhighlight %}

{% highlight UWP %}
//Defining a name in workbook level for the cell A1
IName name = workbook.Names.Add("BookLevelName"); 
name.RefersToRange = worksheet.Range["A1"];
{% endhighlight %}

{% highlight ASP.NET Core %}
//Defining a name in workbook level for the cell A1
IName name = workbook.Names.Add("BookLevelName"); 
name.RefersToRange = worksheet.Range["A1"];
{% endhighlight %}

{% highlight Xamarin %}
//Defining a name in workbook level for the cell A1
IName name = workbook.Names.Add("BookLevelName"); 
name.RefersToRange = worksheet.Range["A1"];
{% endhighlight %}
{% endtabs %}   

The following code shows how to define a named range from worksheet level.

{% tabs %}  
{% highlight c# %}
//Defining a name in worksheet level for the cell B1
IName name = worksheet.Names.Add("SheetLevelName");
name.RefersToRange = worksheet.Range["B1"];
{% endhighlight %}

{% highlight vb %}
'Defining a name in worksheet level for the cell B1
Dim name As IName = worksheet.Names.Add("SheetLevelName")
name.RefersToRange = worksheet.Range("B1")
{% endhighlight %}

{% highlight UWP %}
//Defining a name in worksheet level for the cell B1
IName name = worksheet.Names.Add("SheetLevelName");
name.RefersToRange = worksheet.Range["B1"];
{% endhighlight %}

{% highlight ASP.NET Core %}
//Defining a name in worksheet level for the cell B1
IName name = worksheet.Names.Add("SheetLevelName");
name.RefersToRange = worksheet.Range["B1"];
{% endhighlight %}

{% highlight Xamarin %}
//Defining a name in worksheet level for the cell B1
IName name = worksheet.Names.Add("SheetLevelName");
name.RefersToRange = worksheet.Range["B1"];
{% endhighlight %}
{% endtabs %}   

### Named Ranges in Formulas

Following code example illustrates how to create workbook-level named ranges and use it in formulas.

{% tabs %}  
{% highlight c# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Defining a name in workbook level for the cell A1
  IName name1 = workbook.Names.Add("One");
  name1.RefersToRange = sheet.Range["A1"];

  //Defining a name in workbook level for the cell B1
  IName name2 = workbook.Names.Add("Two");
  name2.RefersToRange = sheet.Range["B1"];

  //Formula using defined names
  sheet.Range["C1"].Formula = "=SUM(One,Two)";

  workbook.SaveAs("Formula.xlsx");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Defining a name in workbook level for the cell A1
  Dim name1 As IName = workbook.Names.Add("One")
  name1.RefersToRange = sheet.Range("A1")

  'Defining a name in workbook level for the cell B1
  Dim name2 As IName = workbook.Names.Add("Two")
  name2.RefersToRange = sheet.Range("B1")

  'Formula using defined names
  sheet.Range("C1").Formula = "=SUM(One,Two)"

  workbook.SaveAs("Formula.xlsx")
End Using
{% endhighlight %}

{% highlight UWP %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Defining a name in workbook level for the cell A1
  IName name1 = workbook.Names.Add("One");
  name1.RefersToRange = sheet.Range["A1"];

  //Defining a name in workbook level for the cell B1
   IName name2 = workbook.Names.Add("Two");
  name2.RefersToRange = sheet.Range["B1"];

  //Formula using defined names
  sheet.Range["C1"].Formula = "=SUM(One,Two)";

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Formula";
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
  IWorksheet sheet = workbook.Worksheets[0];

  //Defining a name in workbook level for the cell A1
  IName name1 = workbook.Names.Add("One");
  name1.RefersToRange = sheet.Range["A1"];

  //Defining a name in workbook level for the cell B1
  IName name2 = workbook.Names.Add("Two");
  name2.RefersToRange = sheet.Range["B1"];

  //Formula using defined names
  sheet.Range["C1"].Formula = "=SUM(One,Two)";

  //Saving the workbook as stream
  FileStream stream = new FileStream("Formula.xlsx", FileMode.Create, FileAccess.ReadWrite);
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
  IWorksheet sheet = workbook.Worksheets[0];

  //Defining a name in workbook level for the cell A1
  IName name1 = workbook.Names.Add("One");
  name1.RefersToRange = sheet.Range["A1"];

  //Defining a name in workbook level for the cell B1
  IName name2 = workbook.Names.Add("Two");
  name2.RefersToRange = sheet.Range["B1"];

  //Formula using defined names
  sheet.Range["C1"].Formula = "=SUM(One,Two)";

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Formula.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Formula.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

### Deleting Named Ranges

Named ranges defined in workbook and worksheet levels can be deleted in different ways. The following code shows the possibilities of deleting named ranges.

{% tabs %}  
{% highlight c# %}
//Deleting named range object
IName name = workbook.Names[0];
name.Delete();

//Deleting named range from workbook
workbook.Names["BookLevelName"].Delete();
//Deleting named range from worksheet
sheet.Names["SheetLevelName"].Delete();
{% endhighlight %}

{% highlight vb %}
'Deleting named range object
Dim name As IName = workbook.Names(0)
name.Delete()

'Deleting named range from workbook
workbook.Names("BookLevelName").Delete()
'Deleting named range from worksheet
sheet.Names("SheetLevelName").Delete()
{% endhighlight %}

{% highlight UWP %}
//Deleting named range object
IName name = workbook.Names[0];
name.Delete();

//Deleting named range from workbook
workbook.Names["BookLevelName"].Delete();
//Deleting named range from worksheet
sheet.Names["SheetLevelName"].Delete();
{% endhighlight %}

{% highlight ASP.NET Core %}
//Deleting named range object
IName name = workbook.Names[0];
name.Delete();

//Deleting named range from workbook
workbook.Names["BookLevelName"].Delete();
//Deleting named range from worksheet
sheet.Names["SheetLevelName"].Delete();
{% endhighlight %}

{% highlight Xamarin %}
//Deleting named range object
IName name = workbook.Names[0];
name.Delete();

//Deleting named range from workbook
workbook.Names["BookLevelName"].Delete();
//Deleting named range from worksheet
sheet.Names["SheetLevelName"].Delete();
{% endhighlight %}
{% endtabs %}   

## Formula Auditing

Microsoft Excel constantly checks in the background for potential errors in your worksheets, when open. If an error is located (or, at the least, what Excel thinks is an error), then the cell is "flagged" with a small green triangle in the upper-left corner of the cell. Auditing a formula helps to identify the error in it. 

In certain cases, these errors can be ignored so that the error will not appear in further error checks. The **IgnoreErrorOptions** property of __IRange__ manages different types of errors checks, for example numbers stored as text, formula calculation errors and validation errors.

To know more about IgnoreErrorOptions, please refer ExcelIgnoreError enumeration in API section.

Following code illustrates on how to ignore or set error indicators.

{% tabs %}  
{% highlight c# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
  IWorksheet sheet = workbook.Worksheets[0];

  //Sets warning if number is entered as text
  sheet.Range["A2:D2"].IgnoreErrorOptions = ExcelIgnoreError.NumberAsText;

  //Ignores all the error warnings
  sheet.Range["A3"].IgnoreErrorOptions = ExcelIgnoreError.None;

  workbook.SaveAs("FormulaAuditing.xlsx");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Sets warning if number is entered as text
  sheet.Range("A2:D2").IgnoreErrorOptions = ExcelIgnoreError.NumberAsText

  'Ignores all the error warnings
  sheet.Range("A3").IgnoreErrorOptions = ExcelIgnoreError.None

  workbook.SaveAs("FormulaAuditing.xlsx")
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
  IWorksheet sheet = workbook.Worksheets[0];

  //Sets warning if number is entered as text
  sheet.Range["A2:D2"].IgnoreErrorOptions = ExcelIgnoreError.NumberAsText;

  //Ignores all the error warnings
  sheet.Range["A3"].IgnoreErrorOptions = ExcelIgnoreError.None;

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "FormulaAuditing";
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
  FileStream inputStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet sheet = workbook.Worksheets[0];

  //Sets warning if number is entered as text.
  sheet.Range["A2:D2"].IgnoreErrorOptions = ExcelIgnoreError.NumberAsText;

  //Ignores all the error warnings.
  sheet.Range["A3"].IgnoreErrorOptions = ExcelIgnoreError.None;

  //Saving the workbook as stream
  FileStream file = new FileStream("FormulaAuditing.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(file);
  file.Dispose();
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
  IWorksheet sheet = workbook.Worksheets[0];

  //Sets warning if number is entered as text
  sheet.Range["A2:D2"].IgnoreErrorOptions = ExcelIgnoreError.NumberAsText;

  //Ignores all the error warnings
  sheet.Range["A3"].IgnoreErrorOptions = ExcelIgnoreError.None;

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("FormulaAuditing.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("FormulaAuditing.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

## Calculation Engine

Essential Calculate is now (from v9.1.x.x) integrated with Essential XlsIO, and thus makes it possible to calculate formulas entered at runtime without any additional references or packages.

N> Do not add reference to Syncfusion.Calculate.Base. It will throw conflict errors as these are already integrated with XlsIO.

N> Only the formulas that are supported by Calculate engine can be calculated at runtime using Essential XlsIO.

## Calculate Options

Calculate engines provides certain options like calculation modes, Recalculate before Save and Enable iterations to perform specific calculation. 

### Calculation Modes

There are various calculation [modes](https://docs.microsoft.com/en-us/office/troubleshoot/excel/current-mode-of-calculation) that enable users to customize formula calculations according to their needs. They are:

* Automatic
* Automatic except for Data Tables
* Manual

Following code illustrates on how to set calculation mode in XlsIO.

{% tabs %}  
{% highlight c# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Setting calculation mode for a workbook
  workbook.CalculationOptions.CalculationMode = ExcelCalculationMode.Manual;

  workbook.SaveAs("CalculationMode.xlsx");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Setting calculation mode for a workbook
  workbook.CalculationOptions.CalculationMode = ExcelCalculationMode.Manual

  workbook.SaveAs("CalculationMode.xlsx")
End Using
{% endhighlight %}

{% highlight UWP %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Setting calculation mode for a workbook
  workbook.CalculationOptions.CalculationMode = ExcelCalculationMode.Manual;

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "CalculationMode";
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
  IWorksheet sheet = workbook.Worksheets[0];

  //Setting calculation mode for a workbook
  workbook.CalculationOptions.CalculationMode = ExcelCalculationMode.Manual;

  //Saving the workbook as stream
  FileStream stream = new FileStream("CalculationMode.xlsx", FileMode.Create, FileAccess.ReadWrite);
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
  IWorksheet sheet = workbook.Worksheets[0];

  //Setting calculation mode for a workbook
  workbook.CalculationOptions.CalculationMode = ExcelCalculationMode.Manual;

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("CalculationMode.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("CalculationMode.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

### Recalculate Before Save

In Manual mode, this option controls whether Microsoft Excel should recalculate the workbook as a part of Save process. You can set this option by using **RecalcOnSave** property of __ICalculationOptions__ interface.

{% tabs %}  
{% highlight c# %}
ICalculationOptions calcOptions = workbook.CalculationOptions;

//Set RecalcOnSave to false to avoid re calculation of workbook while saving
calcOptions.RecalcOnSave = false;
{% endhighlight %}

{% highlight vb %}
Dim calcOptions As ICalculationOptions = workbook.CalculationOptions

'Set RecalcOnSave to false to avoid re calculation of workbook while saving
calcOptions.RecalcOnSave = False
{% endhighlight %}

{% highlight UWP %}
ICalculationOptions calcOptions = workbook.CalculationOptions;

//Set RecalcOnSave to false to avoid re calculation of workbook while saving
calcOptions.RecalcOnSave = false;
{% endhighlight %}

{% highlight ASP.NET Core %}
ICalculationOptions calcOptions = workbook.CalculationOptions;

//Set RecalcOnSave to false to avoid re calculation of workbook while saving
calcOptions.RecalcOnSave = false;
{% endhighlight %}

{% highlight Xamarin %}
ICalculationOptions calcOptions = workbook.CalculationOptions;

//Set RecalcOnSave to false to avoid re calculation of workbook while saving
calcOptions.RecalcOnSave = false;
{% endhighlight %}
{% endtabs %}   

### Iteration

Iteration is the repeated recalculation of a worksheet until a specific numeric condition is met. If a formula refers back to one of its own cells, it is must determine how many times the formula should recalculate.

Iteration settings will control the maximum number of iteration and the amount of acceptable change. By default, **IsIterationEnabled** is false, so that Excel does not try to solve accidental circular references. 

Following code snippet illustrates how to set the Iterations.

{% tabs %}  
{% highlight c# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Setting iteration
  workbook.CalculationOptions.IsIterationEnabled = true;

  //Number of times to recalculate
  workbook.CalculationOptions.MaximumIteration = 99;

  //Number of acceptable changes
  workbook.CalculationOptions.MaximumChange = 40;

  workbook.SaveAs("Iteration.xlsx");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim sheet As IWorkbook = workbook.Worksheets(0)

  'Setting Iteration
  workbook.CalculationOptions.IsIterationEnabled = True

  'Number of times to recalculate
  workbook.CalculationOptions.MaximumIteration = 99

  'Number of acceptable changes
  workbook.CalculationOptions.MaximumChange = 40

  workbook.SaveAs("Iteration.xlsx")
End Using
{% endhighlight %}

{% highlight UWP %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Setting iteration
  workbook.CalculationOptions.IsIterationEnabled = true;

  //Number of times to recalculate
  workbook.CalculationOptions.MaximumIteration = 99;

  //Number of acceptable changes
  workbook.CalculationOptions.MaximumChange = 40;

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Iteration";
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
  IWorksheet sheet = workbook.Worksheets[0];

  //Setting iteration
  workbook.CalculationOptions.IsIterationEnabled = true;

  //Number of times to recalculate
  workbook.CalculationOptions.MaximumIteration = 99;

  //Number of acceptable changes
  workbook.CalculationOptions.MaximumChange = 40;

  //Saving the workbook as stream
  FileStream stream = new FileStream("Iteration.xlsx", FileMode.Create, FileAccess.ReadWrite);
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
  IWorksheet sheet = workbook.Worksheets[0];

  //Setting iteration
  workbook.CalculationOptions.IsIterationEnabled = true;

  //Number of times to recalculate
  workbook.CalculationOptions.MaximumIteration = 99;

  //Number of acceptable changes
  workbook.CalculationOptions.MaximumChange = 40;

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Iteration.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Iteration.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}  
