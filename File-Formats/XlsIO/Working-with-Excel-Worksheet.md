---
title: Working with Excel Worksheet | Syncfusion
description: In this section, you can learn about various Excel worksheet operations using Syncfusion Essential XlsIO
platform: file-formats
control: XlsIO
documentation: UG
keywords: c#, vb.net, excel, syncfusion, xlsio, read excel, extract data, data from excel, excel worksheet, data from sheet, new worksheet, add worksheet, insert new worksheet, create new worksheet, insert worksheet, create worksheet, insert worksheet, create excel sheet, delete worksheet, delete sheet in excel, remove worksheet, remove sheet in excel, move sheet from one workbook to another, copy sheet from one worksheet to another, moving between sheets in excel, moving sheet, copying between sheets in excel, copying sheets 
---

# Working with Excel Worksheet 

A Workbook contains a collection of worksheets where the actual contents resides. It is possible to add and manipulate worksheets and [IWorksheet](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorksheet.html) instance represents an Excel worksheet.

## Create a Worksheet 

A new worksheet can be added into the workbook through [Create](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorksheets.html#Syncfusion_XlsIO_IWorksheets_Create) method of [IWorksheets](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorksheets.html) interface. It is also possible to specify the required number of worksheets and if not specified, XlsIO creates three worksheets by default.

The following code snippet shows how to create worksheets within a workbook.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;

  //The new workbook will have 5 worksheets
  IWorkbook workbook = application.Workbooks.Create(5);
  //Creating a Sheet
  IWorksheet sheet = workbook.Worksheets.Create();
  //Creating a Sheet with name “Sample”
  IWorksheet namedSheet = workbook.Worksheets.Create("Sample");

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx

  'The new workbook will have 5 worksheets
  Dim workbook As IWorkbook = application.Workbooks.Create(5)
  'Creating a sheet
  Dim sheet As IWorksheet = workbook.Worksheets.Create()
  'Creating a Sheet with name “Sample”
  Dim namedSheet As IWorksheet = workbook.Worksheets.Create("Sample")

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;

  //The new workbook will have 5 worksheets.
  IWorkbook workbook = application.Workbooks.Create(5);
  //Creating a Sheet
  IWorksheet sheet = workbook.Worksheets.Create();
  //Creating a Sheet with name “Sample”
  IWorksheet namedSheet = workbook.Worksheets.Create("Sample");

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

  //The new workbook will have 5 worksheets
  IWorkbook workbook = application.Workbooks.Create(5);
  //Creating a Sheet
  IWorksheet sheet = workbook.Worksheets.Create();
  //Creating a Sheet with name “Sample”
  IWorksheet namedSheet = workbook.Worksheets.Create("Sample");

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

  //The new workbook will have 5 worksheets.
  IWorkbook workbook = application.Workbooks.Create(5);
  //Creating a Sheet.
  IWorksheet sheet = workbook.Worksheets.Create();
  //Creating a Sheet with name “Sample”
  IWorksheet namedSheet = workbook.Worksheets.Create("Sample");

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

A complete working example for creating Excel worksheets in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Worksheet%20Features/Create%20Worksheet).

## Access a Worksheet 

[Worksheets](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbook.html#Syncfusion_XlsIO_IWorkbook_Worksheets) collection holds one or more worksheets present in a workbook. Accessing a particular worksheet can be done by the following ways. 

1. Specifying the index 
2. Specifying the sheet name. 

The below codes illustrate how to access a worksheet from its worksheets collection.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(2);

  //Accessing via index
  IWorksheet sheet = workbook.Worksheets[0];

  //Accessing via sheet Name
  IWorksheet NamedSheet = workbook.Worksheets["Sample"];

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(2)

  'Accessing via index
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Accessing via Sheet Name
  Dim NamedSheet As IWorksheet = workbook.Worksheets("Sample")

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(2);

  //Accessing via index
  IWorksheet sheet = workbook.Worksheets[0];

  //Accessing via sheet Name
  IWorksheet NamedSheet = workbook.Worksheets["Sample"];

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
  IWorkbook workbook = application.Workbooks.Create(2);

  //Accessing via index
  IWorksheet sheet = workbook.Worksheets[0];

  //Accessing via sheet Name
  IWorksheet NamedSheet = workbook.Worksheets["Sample"];

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
  IWorkbook workbook = application.Workbooks.Create(2);

  //Accessing via index
  IWorksheet sheet = workbook.Worksheets[0];

  //Accessing via sheet Name
  IWorksheet NamedSheet = workbook.Worksheets["Sample"];

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

A complete working example for accessing Excel worksheets in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Worksheet%20Features/Access%20Worksheet).

T>If the workbook contains multiple worksheets, then the parsing of the workbook will consume time. **ParseWorksheetsOnDemand** of [ExcelParseOptions](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelParseOptions.html) can be used in [Open](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbooks.html#Syncfusion_XlsIO_IWorkbooks_Open_System_String_Syncfusion_XlsIO_ExcelOpenType_Syncfusion_XlsIO_ExcelParseOptions_) method of [IWorkbooks](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbooks.html) to parse the worksheet only when it is accessed. This option can be used in a scenario where workbook contains multiple worksheets but you are going to use only few worksheets among them.

{% tabs %}
{% highlight c# tabtitle="C#" %}
IWorkbook workbook = application.Workbooks.Open(fileName,ExcelParseOptions.ParseWorksheetsOnDemand);
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Dim workbook As IWorkbook = application.Workbooks.Open(fileName, ExcelParseOptions.ParseWorksheetsOnDemand)
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
IWorkbook workbook = await application.Workbooks.OpenAsync(workbookStorageFile,ExcelOpenType.Automatic,ExcelParseOptions.ParseWorksheetsOnDemand);
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
IWorkbook workbook = application.Workbooks.Open(workbookStream,ExcelParseOptions.ParseWorksheetsOnDemand);
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
IWorkbook workbook = application.Workbooks.Open(workbookStream,ExcelParseOptions.ParseWorksheetsOnDemand);
{% endhighlight %}
{% endtabs %}  
  
## Remove a Worksheet

The following code snippet explains how to remove a worksheet from Excel workbook.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(2);

  //Removing the sheet
  workbook.Worksheets[0].Remove();

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(2)

  'Removing the sheet
  workbook.Worksheets(0).Remove()

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(2);

  //Removing the sheet
  workbook.Worksheets[0].Remove();

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
  IWorkbook workbook = application.Workbooks.Create(2);

  //Removing the sheet
  workbook.Worksheets[0].Remove();

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
  IWorkbook workbook = application.Workbooks.Create(2);

  //Removing the sheet
  workbook.Worksheets[0].Remove();

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

A complete working example for removing an Excel worksheet in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Worksheet%20Features/Remove%20Worksheet).

## Move or Copy a Worksheet

Essential XlsIO allows to move or create a copy of Excel worksheet, and insert that worksheet before or after an existing worksheet in the workbook.

### Copying Worksheets

It is possible to copy a worksheet to one another workbook or within the same workbook.

The following code example illustrates how to copy a sheet with its entire contents to another workbook.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook sourceWorkbook = application.Workbooks.Open("SourceWorkbookTemplate.xlsx");
  IWorkbook destinationWorkbook = application.Workbooks.Open("DestinationWorkbookTemplate.xlsx");

  //Copy first worksheet from the Source workbook to the destination workbook
  destinationWorkbook.Worksheets.AddCopy(sourceWorkbook.Worksheets[0]);

  destinationWorkbook.ActiveSheetIndex = 1;
  destinationWorkbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim sourceWorkbook As IWorkbook = application.Workbooks.Open("SourceWorkbookTemplate.xlsx")
  Dim destinationWorkbook As IWorkbook = application.Workbooks.Open("DestinationWorkbookTemplate.xlsx")

  'Copy first worksheet from the Source workbook to the destination workbook
  destinationWorkbook.Worksheets.AddCopy(sourceWorkbook.Worksheets(0))

  destinationWorkbook.ActiveSheetIndex = 1
  destinationWorkbook.SaveAs("Output.xlsx")
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
  StorageFile sourceFile = await openPicker.PickSingleFileAsync();
  StorageFile destinationFile = await openPicker.PickSingleFileAsync();

  //Opens the workbook
  IWorkbook sourceWorkbook = await application.Workbooks.OpenAsync(sourceFile);
  IWorkbook destinationWorkbook = await application.Workbooks.OpenAsync(destinationFile);

  //Copy first worksheet from the Source workbook to the destination workbook
  destinationWorkbook.Worksheets.AddCopy(sourceWorkbook.Worksheets[0]);
  destinationWorkbook.ActiveSheetIndex = 1;

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Output";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  await destinationWorkbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  FileStream sourceStream = new FileStream("SourceWorkbookTemplate.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook sourceWorkbook = application.Workbooks.Open(sourceStream);
  FileStream destinationStream = new FileStream("DestinationWorkbookTemplate.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook destinationWorkbook = application.Workbooks.Open(destinationStream);

  //Copy first worksheet from the Source workbook to the destination workbook
  destinationWorkbook.Worksheets.AddCopy(sourceWorkbook.Worksheets[0]);
  destinationWorkbook.ActiveSheetIndex = 1;

  //Saving the workbook as stream
  FileStream copiedStream = new FileStream("Output.xlsx", FileMode.Create, FileAccess.ReadWrite);
  destinationWorkbook.SaveAs(copiedStream);
  copiedStream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;

  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream sourceStream = assembly.GetManifestResourceStream("WorksheetFeatures.SourceWorkbookTemplate.xlsx");
  IWorkbook sourceWorkbook = application.Workbooks.Open(sourceStream);
  Stream destinationStream = assembly.GetManifestResourceStream("WorksheetFeatures.DestinationWorkbookTemplate.xlsx");
  IWorkbook destinationWorkbook = application.Workbooks.Open(destinationStream);

  //Copy first worksheet from the Source workbook to the destination workbook
  destinationWorkbook.Worksheets.AddCopy(sourceWorkbook.Worksheets[0]);
  destinationWorkbook.ActiveSheetIndex = 1;

  //Saving the workbook as stream
  MemoryStream copiedStream = new MemoryStream();
  destinationWorkbook.SaveAs(copiedStream);

  copiedStream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Output.xlsx", "application/msexcel", copiedStream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", copiedStream);
  }
}
{% endhighlight %}
{% endtabs %}

A complete working example for copying Excel worksheets in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Worksheet%20Features/Copy%20Worksheet).

Specific copy options can be chosen while copying a worksheet, which helps to achieve customized copying by ignoring certain formatting. For more information about copy options, please refer [ExcelWorksheetCopyFlags](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelWorksheetCopyFlags.html).

### Moving a Worksheet

XlsIO allows moving worksheets from one position to another by using the [Move](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorksheet.html#Syncfusion_XlsIO_IWorksheet_Move_System_Int32_) method. The following code example illustrates how a worksheet is moved.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(3);
  IWorksheet sheet = workbook.Worksheets[0];

  //Move the Sheet
  sheet.Move(1);

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(3)
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Move the sheet
  sheet.Move(1)

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(3);
  IWorksheet sheet = workbook.Worksheets[0];

  //Move the Sheet
  sheet.Move(1);

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
  IWorkbook workbook = application.Workbooks.Create(3);
  IWorksheet sheet = workbook.Worksheets[0];

  //Move the Sheet
  sheet.Move(1);

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
  IWorkbook workbook = application.Workbooks.Create(3);
  IWorksheet sheet = workbook.Worksheets[0];

  //Move the Sheet
  sheet.Move(1);

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

A complete working example for moving Excel worksheets in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Worksheet%20Features/Move%20Worksheet).

## Highlight Worksheet Tabs 

A particular worksheet tab can be highlighted to denote its importance. Tab color can be set through the [TabColor](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ITabSheet.html#Syncfusion_XlsIO_ITabSheet_TabColor) property, as given below.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Highlighting sheet tab
  sheet.TabColor = ExcelKnownColors.Red;

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Highlighting sheet tab
  sheet.TabColor = ExcelKnownColors.Red

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Highlighting sheet tab
  sheet.TabColor = ExcelKnownColors.Red;

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
  IWorksheet sheet = workbook.Worksheets[0];

  //Highlighting sheet tab
  sheet.TabColor = ExcelKnownColors.Red;

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
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Highlighting sheet tab
  sheet.TabColor = ExcelKnownColors.Red;

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

A complete working example to highlight an Excel worksheet tab in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Worksheet%20Features/Highlight%20Worksheet%20Tab).

## Freeze Panes 	

It is possible to [freeze](https://support.office.com/en-au/article/Freeze-rows-and-columns-32b23056-d13b-4b2d-aabb-de55a4c2f708) a portion of the sheet to keep it visible while you scroll through the rest of the sheet. The following code snippet shows how to freeze panes through the [FreezePanes](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IRange.html#Syncfusion_XlsIO_IRange_FreezePanes) method of [IRange](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IRange.html). 

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Applying Freeze Pane to the sheet by specifying a cell
  sheet.Range["B2"].FreezePanes();
  
  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Applying Freeze Pane to the sheet by specifying a cell
  sheet.Range("B2").FreezePanes()

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Applying Freeze Pane to the sheet by specifying a cell
  sheet.Range["B2"].FreezePanes();

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
  IWorksheet sheet = workbook.Worksheets[0];

  //Applying Freeze Pane to the sheet by specifying a cell
  sheet.Range["B2"].FreezePanes();

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
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Applying Freeze Pane to the sheet by specifying a cell
  sheet.Range["B2"].FreezePanes();

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

You can set first visible row and first visible column in non-frozen area, through the [FirstVisibleRow](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorksheet.html#Syncfusion_XlsIO_IWorksheet_FirstVisibleRow) and [FirstVisibleColumn](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorksheet.html#Syncfusion_XlsIO_IWorksheet_FirstVisibleColumn) properties as shown below

N> **FirstVisibleColumn** and **FirstVisibleRow** indexes are "zero-based".

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  sheet.Range["B2"].FreezePanes();

  //Set first visible row in the bottom pane
  sheet.FirstVisibleRow = 2;
  //Set first visible column in the right pane
  sheet.FirstVisibleColumn = 2;

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  sheet.Range("B2").FreezePanes()

  'Set first visible row in the bottom pane
  sheet.FirstVisibleRow = 2
  'Set first visible column in the right pane
  sheet.FirstVisibleColumn = 2

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  sheet.Range["B2"].FreezePanes();

  //Set first visible row in the bottom pane
  sheet.FirstVisibleRow = 2;
  //Set first visible column in the right pane
  sheet.FirstVisibleColumn = 2;

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
  IWorksheet sheet = workbook.Worksheets[0];

  sheet.Range["B2"].FreezePanes();

  //Set first visible row in the bottom pane
  sheet.FirstVisibleRow = 2;
  //Set first visible column in the right pane
  sheet.FirstVisibleColumn = 2;

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
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  sheet.Range["B2"].FreezePanes();

  //Set first visible row in the bottom pane
  sheet.FirstVisibleRow = 2;
  //Set first visible column in the right pane
  sheet.FirstVisibleColumn = 2;

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

A complete working example to freeze panes in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Worksheet%20Features/Freeze%20Panes). 

## Unfreeze Panes

It is possible to unfreeze panes in an Excel worksheet using the [RemovePanes](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorksheet.html#Syncfusion_XlsIO_IWorksheet_RemovePanes) method of [IWorksheet](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorksheet.html) interface. Refer to the following complete code snippet.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
  IWorksheet worksheet = workbook.Worksheets[0];

  //Unfreeze panes in the worksheet
  worksheet.RemovePanes();

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Unfreeze panes in the worksheet
  worksheet.RemovePanes()

  workbook.SaveAs("Output.xlsx")
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

  //Unfreeze panes in the worksheet
  worksheet.RemovePanes();

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

  //Unfreeze panes in the worksheet
  worksheet.RemovePanes();

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

  //"App" is the class of portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream = assembly.GetManifestResourceStream("ModifyWorksheet.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Unfreeze panes in the worksheet
  worksheet.RemovePanes();

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies among Windows Phone, Android, and iOS platforms. Refer to the xlsio/xamarin section for respective code samples.

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

## Split Panes 

The window into can be divided into different [panes](https://support.office.com/en-AU/article/Split-panes-to-lock-rows-or-columns-in-separate-worksheet-areas-516a7001-b3ed-4122-a6bb-fd6d4a9d6434) that scroll separately each. The following code snippets illustrates how to split the window through the [HorizontalSplit](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorksheet.html#Syncfusion_XlsIO_IWorksheet_HorizontalSplit) and [VerticalSplit](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorksheet.html#Syncfusion_XlsIO_IWorksheet_VerticalSplit) properties.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //split panes
  sheet.FirstVisibleColumn = 5;
  sheet.FirstVisibleRow = 11;
  sheet.VerticalSplit = 1100;
  sheet.HorizontalSplit = 1000;
  sheet.ActivePane = 1;

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Split Panes
  sheet.FirstVisibleColumn = 5
  sheet.FirstVisibleRow = 11
  sheet.VerticalSplit = 1100
  sheet.HorizontalSplit = 1000
  sheet.ActivePane = 1

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //split panes
  sheet.FirstVisibleColumn = 5;
  sheet.FirstVisibleRow = 11;
  sheet.VerticalSplit = 1100;
  sheet.HorizontalSplit = 1000;
  sheet.ActivePane = 1;

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
  IWorksheet sheet = workbook.Worksheets[0];

  //split panes
  sheet.FirstVisibleColumn = 5;
  sheet.FirstVisibleRow = 11;
  sheet.VerticalSplit = 1100;
  sheet.HorizontalSplit = 1000;
  sheet.ActivePane = 1;

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
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //split panes
  sheet.FirstVisibleColumn = 5;
  sheet.FirstVisibleRow = 11;
  sheet.VerticalSplit = 1100;
  sheet.HorizontalSplit = 1000;
  sheet.ActivePane = 1;

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

A complete working example to split panes in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Worksheet%20Features/Split%20Panes). 

## Page Setup Settings

[PageSetup](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorksheet.html#Syncfusion_XlsIO_IWorksheet_PageSetup) includes the size, orientation of the paper, margins, page breaks, scaling, paper size, header/ footer settings and background settings. The following code snippet shows how to set the page setup.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  sheet.Range["A1:M20"].Text = "PageBreak";

  //Set Horizontal Page Breaks
  sheet.HPageBreaks.Add(sheet.Range["A5"]);
  //Set Vertical Page Breaks
  sheet.VPageBreaks.Add(sheet.Range["B5"]);

  //Set print title
  sheet.PageSetup.PrintTitleColumns = "$B:$E";
  sheet.PageSetup.PrintTitleRows = "$2:$5";

  //Set Page Orientation as Portrait or Landscape
  sheet.PageSetup.Orientation = ExcelPageOrientation.Landscape;

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  sheet.Range("A1:M20").Text = "PageBreak"

  'Set Horizontal Page Breaks
  sheet.HPageBreaks.Add(sheet.Range("A5"))
  'Set Vertical Page Breaks
  sheet.VPageBreaks.Add(sheet.Range("B5"))

  'Set print titles
  sheet.PageSetup.PrintTitleColumns = "$B:$E"
  sheet.PageSetup.PrintTitleRows = "$2:$5"

  'Set Page Orientation as Portrait or Landscape
  sheet.PageSetup.Orientation = ExcelPageOrientation.Landscape

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  sheet.Range["A1:M20"].Text = "PageBreak";

  //Set Horizontal Page Breaks
  sheet.HPageBreaks.Add(sheet.Range["A5"]);
  //Set Vertical Page Breaks
  sheet.VPageBreaks.Add(sheet.Range["B5"]);

  //Set print title
  sheet.PageSetup.PrintTitleColumns = "$B:$E"
  sheet.PageSetup.PrintTitleRows = "$2:$5"

  //Set Page Orientation as Portrait or Landscape
  sheet.PageSetup.Orientation = ExcelPageOrientation.Landscape;

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
  IWorksheet sheet = workbook.Worksheets[0];

  sheet.Range["A1:M20"].Text = "PageBreak";

  //Set Horizontal Page Breaks
  sheet.HPageBreaks.Add(sheet.Range["A5"]);
  //Set Vertical Page Breaks
  sheet.VPageBreaks.Add(sheet.Range["B5"]);

  //Set print title
  sheet.PageSetup.PrintTitleColumns = "$B:$E";
  sheet.PageSetup.PrintTitleRows = "$2:$5";

  //Set Page Orientation as Portrait or Landscape
  sheet.PageSetup.Orientation = ExcelPageOrientation.Landscape;

  //Saving the workbook as stream
  FileStream stream = new FileStream("output.xlsx", FileMode.Create, FileAccess.ReadWrite);
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

  sheet.Range["A1:M20"].Text = "PageBreak";

  //Set Horizontal Page Breaks
  sheet.HPageBreaks.Add(sheet.Range["A5"]);
  //Set Vertical Page Breaks.
  sheet.VPageBreaks.Add(sheet.Range["B5"]);

  //Set print title
  sheet.PageSetup.PrintTitleColumns = "$B:$E";
  sheet.PageSetup.PrintTitleRows = "$2:$5";

  //Set Page Orientation as Portrait or Landscape
  sheet.PageSetup.Orientation = ExcelPageOrientation.Landscape;

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

A complete working example for Excel page setup settings in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Worksheet%20Features/PageSetup). 

## Show or Hide Worksheet 

The following code snippet shows how to hide the worksheets using [Visibility](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ITabSheet.html#Syncfusion_XlsIO_ITabSheet_Visibility) property.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(2);
  IWorksheet sheet = workbook.Worksheets[0];

  sheet.Range["A1:M20"].Text = "visibility";
  //Set visibility
  sheet.Visibility = WorksheetVisibility.Hidden;

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(2)
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  sheet.Range("A1:M20").Text = "Visibility"
  'Set visibility
  sheet.Visibility = WorksheetVisibility.Hidden

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(2);
  IWorksheet sheet = workbook.Worksheets[0];

  sheet.Range["A1:M20"].Text = "visibility";
  //Set visibility
  sheet.Visibility = WorksheetVisibility.Hidden;

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
  IWorkbook workbook = application.Workbooks.Create(2);
  IWorksheet sheet = workbook.Worksheets[0];

  sheet.Range["A1:M20"].Text = "visibility";
  //Set visibility
  sheet.Visibility = WorksheetVisibility.Hidden;

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
  IWorkbook workbook = application.Workbooks.Create(2);
  IWorksheet sheet = workbook.Worksheets[0];

  sheet.Range["A1:M20"].Text = "visibility";
  //Set visibility
  sheet.Visibility = WorksheetVisibility.Hidden;

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

A complete working example to show or hide an Excel worksheet in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Worksheet%20Features/Hide%20Worksheet). 

## Activate a Worksheet

A worksheet in an Excel workbook can be activated through [Activate](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ITabSheet.html#Syncfusion_XlsIO_ITabSheet_Activate) method. The following code snippet explains this.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(2);
  IWorksheet sheet = workbook.Worksheets[0];

  sheet.Range["A1:M20"].Text = "Activate";
  //Activate the sheet
  sheet.Activate();

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(2)
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  sheet.Range("A1:M20").Text = "Activate"
  'Activate the sheet
  sheet.Activate()

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(2);
  IWorksheet sheet = workbook.Worksheets[0];

  sheet.Range["A1:M20"].Text = "Activate";
  //Activate the sheet
  sheet.Activate();

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
  IWorkbook workbook = application.Workbooks.Create(2);
  IWorksheet sheet = workbook.Worksheets[0];

  sheet.Range["A1:M20"].Text = "Activate";
  //Activate the sheet
  sheet.Activate();

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
  IWorkbook workbook = application.Workbooks.Create(2);
  IWorksheet sheet = workbook.Worksheets[0];

  sheet.Range["A1:M20"].Text = "Activate";
  //Activate the sheet
  sheet.Activate();

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

A complete working example to activate an Excel worksheet in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Worksheet%20Features/Activate%20Worksheet). 

## Show or Hide Worksheet Tabs 

The following code snippet shows how to hide the worksheet tabs using [DisplayWorkbookTabs](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbook.html#Syncfusion_XlsIO_IWorkbook_DisplayWorkbookTabs) property.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(3);
  IWorksheet sheet = workbook.Worksheets[0];
  sheet.Range["A1:M20"].Text = "Tabs";
	
  //Hide the tab
  workbook.DisplayWorkbookTabs = false;
  //set the display tab
  workbook.DisplayedTab = 2;

  workbook.SaveAs("Output.xlsx");
}	
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(3)
  Dim sheet As IWorksheet = workbook.Worksheets(0)
  sheet.Range("A1:M20").Text = "Tabs"

  'Hide the tab
  workbook.DisplayWorkbookTabs = False
  'set the display tab
  workbook.DisplayedTab = 2

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(3);
  IWorksheet sheet = workbook.Worksheets[0];
  sheet.Range["A1:M20"].Text = "Tabs";
  
  //Hide the tab
  workbook.DisplayWorkbookTabs = false;
  //set the display tab
  workbook.DisplayedTab = 2;

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
  IWorkbook workbook = application.Workbooks.Create(3);
  IWorksheet sheet = workbook.Worksheets[0];
  sheet.Range["A1:M20"].Text = "Tabs";
	
  //Hide the tab
  workbook.DisplayWorkbookTabs = false;
  //set the display tab
  workbook.DisplayedTab = 2;

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
  IWorkbook workbook = application.Workbooks.Create(3);
  IWorksheet sheet = workbook.Worksheets[0];
  sheet.Range["A1:M20"].Text = "Tabs";
	
  //Hide the tab
  workbook.DisplayWorkbookTabs = false;
  //set the display tab
  workbook.DisplayedTab = 2;

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

A complete working example to hide Excel worksheet tab in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Worksheet%20Features/Hide%20Worksheet%20Tabs). 
 
## View Settings

### Show or Hide Row and Column Headers 

Row and column headings can be displayed or hidden through [IsRowColumnHeadersVisible](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorksheet.html#Syncfusion_XlsIO_IWorksheet_IsRowColumnHeadersVisible) property of [IWorksheet](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorksheet.html).

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  sheet.Range["A1:M20"].Text = "RowColumnHeader";
  sheet.IsRowColumnHeadersVisible = false;

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  sheet.Range("A1:M20").Text = "RowColumnHeader"
  sheet.IsRowColumnHeadersVisible = False

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  sheet.Range["A1:M20"].Text = "RowColumnHeader";
  sheet.IsRowColumnHeadersVisible = false;

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
  IWorksheet sheet = workbook.Worksheets[0];

  sheet.Range["A1:M20"].Text = "RowColumnHeader";
  sheet.IsRowColumnHeadersVisible = false;

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
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  sheet.Range["A1:M20"].Text = "RowColumnHeader";
  sheet.IsRowColumnHeadersVisible = false;

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

A complete working example to hide row and column headers in an Excel worksheet in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Worksheet%20Features/Hide%20Row%20and%20Column%20Headers). 

### Show or Hide Grid Lines 

The following code snippet shows how to hide the grid lines using [IsGridLinesVisible](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorksheet.html#Syncfusion_XlsIO_IWorksheet_IsGridLinesVisible) property.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];
  sheet.Range["A1:M20"].Text = "Gridlines";

  //Hide grid line
  sheet.IsGridLinesVisible = false;

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim sheet As IWorksheet = workbook.Worksheets(0)
  sheet.Range("A1:M20").Text = "GridLines"

  'Hide grid line
  sheet.IsGridLinesVisible = False

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];
  sheet.Range["A1:M20"].Text = "Gridlines";

  //Hide grid line
  sheet.IsGridLinesVisible = false;

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
  IWorksheet sheet = workbook.Worksheets[0];
  sheet.Range["A1:M20"].Text = "Gridlines";

  //Hide grid line
  sheet.IsGridLinesVisible = false;

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
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];
  sheet.Range["A1:M20"].Text = "Gridlines";

  //Hide grid line
  sheet.IsGridLinesVisible = false;

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

A complete working example to hide gridlines in an Excel worksheet in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Worksheet%20Features/Hide%20Gridlines).

### Set Zoom Level

The following code snippet shows how to set the zoom level by using [Zoom](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorksheet.html#Syncfusion_XlsIO_IWorksheet_Zoom) property.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];
  sheet.Range["A1:M20"].Text = "Zoom level";

  //set zoom percentage
  sheet.Zoom = 70;

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim sheet As IWorksheet = workbook.Worksheets(0)
  sheet.Range("A1:M20").Text = "Zoom level"

  'set Zoom percentage
  sheet.Zoom = 70

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];
  sheet.Range["A1:M20"].Text = "Zoom level";

  //set zoom percentage
  sheet.Zoom = 70;

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
  IWorksheet sheet = workbook.Worksheets[0];
  sheet.Range["A1:M20"].Text = "Zoom level";

  //set zoom percentage
  sheet.Zoom = 70;

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
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];
  sheet.Range["A1:M20"].Text = "Zoom level";

  //set zoom percentage
  sheet.Zoom = 70;

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

A complete working example to set zoom percentage in an Excel worksheet in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Worksheet%20Features/Set%20Zoom%20Level).

## Open a CSV File

A CSV file has to be opened by specifying the delimiter set in it. Specifying the delimiter can be ignored, if it is Comma(,), as Syncfusion XlsIO considers the default delimiter as Comma(,).

The delimiters used in CSV file are Comma (,), Tab (\t), SemiColon (;), Colon (:), Space ( ), Equals Sign (=) etc..

The following complete code snippet explains how to open a Tab (\t) delimited CSV file using XlsIO.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;

  //Open the Tab delimited CSV file
  IWorkbook workbook = application.Workbooks.Open("Sample.csv", "\t");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  
  'Open the Tab delimited CSV file
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.csv", "\t")
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
  openPicker.FileTypeFilter.Add(".csv");
  StorageFile file = await openPicker.PickSingleFileAsync();

  //Open the Tab delimited CSV file
  IWorkbook workbook = await application.Workbooks.OpenAsync(file, "\t");
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  FileStream inputStream = new FileStream("Sample.csv", FileMode.Open, FileAccess.Read);
  
  //Open the Tab delimited CSV file
  IWorkbook workbook = application.Workbooks.Open(inputStream, "\t");
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;

  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream = assembly.GetManifestResourceStream("WorksheetFeatures.Sample.csv");
  
  //Open the Tab delimited CSV file
  IWorkbook workbook = application.Workbooks.Open(inputStream, "\t");
}
{% endhighlight %}
{% endtabs %}

## Save Worksheet as CSV

The following code example illustrates how to save a worksheet as CSV file.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];
  sheet.Range["A1:M20"].Text = "document";

  //Save the sheet as CSV
  sheet.SaveAs("Sample.csv", ",");

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim sheet As IWorksheet = workbook.Worksheets(0)
  sheet.Range("A1:M20").Text = "document"
  
  'Save the sheet as CSV 
  sheet.SaveAs("Sample.csv", ",")

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];
  sheet.Range["A1:M20"].Text = "document";

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;

  savePicker.SuggestedFileName = "Sample";
  savePicker.FileTypeChoices.Add("CSV Files", new List<string>() { ".csv" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile1 = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  await sheet.SaveAsAsync(storageFile1,",");

  savePicker.SuggestedFileName = "Output";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile2 = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  await workbook.SaveAsAsync(storageFile2);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];
  sheet.Range["A1:M20"].Text = "document";

  //Saving the sheet and workbook as streams
  FileStream sheetStream = new FileStream("Sample.csv", FileMode.Create, FileAccess.ReadWrite);
  sheet.SaveAs(sheetStream,",");
  
  FileStream stream = new FileStream("Output.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  sheetStream.Dispose();
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
  sheet.Range["A1:M20"].Text = "document";

  //Saving the sheet and workbook as streams
  MemoryStream sheetStream = new MemoryStream();
  sheet.SaveAs(sheetStream,",");
  
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  sheetStream.Position = 0;
  stream.Position = 0;
  
  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Sample.csv", "application/msexcel", sheetStream);
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Output.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.csv", "application/msexcel", sheetStream);
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}  
 
A complete working example to read and save a CSV file in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Worksheet%20Features/Read%20and%20Save%20CSV).

### Save worksheet as text (*.txt)

Essential XlsIO allows to save worksheet as a text file. This can be done by leaving the delimiter with a space as shown in the below codes.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];
  sheet.Range["A1:M20"].Text = "Text document";

  //Save the sheet as text
  sheet.SaveAs("Sample.txt", " ");

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim sheet As IWorksheet = workbook.Worksheets(0)
  sheet.Range("A1:M20").Text = "Text document"

  'Save the sheet as text
  sheet.SaveAs("Sample.txt", " ")

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];
  sheet.Range["A1:M20"].Text = "Text document";

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;

  savePicker.SuggestedFileName = "Sample";
  savePicker.FileTypeChoices.Add("Text Files", new List<string>() { ".txt" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile1 = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  await sheet.SaveAsAsync(storageFile1, " ");

  savePicker.SuggestedFileName = "Output";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile2 = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  await workbook.SaveAsAsync(storageFile2);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];
  sheet.Range["A1:M20"].Text = "Text document";

  //Saving the sheet and workbook as streams
  FileStream sheetStream = new FileStream("Sample.txt", FileMode.Create, FileAccess.ReadWrite);
  sheet.SaveAs(sheetStream," ");
  
  FileStream stream = new FileStream("Output.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  sheetStream.Dispose();
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
  sheet.Range["A1:M20"].Text = "Text document";

  //Saving the sheet and workbook as streams
  MemoryStream sheetStream = new MemoryStream();
  sheet.SaveAs(sheetStream," ");
  
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  sheetStream.Position = 0;
  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Sample.txt", "text/plain", sheetStream);
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Output.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.txt", "text/plain", sheetStream);
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}   

A complete working example to save an Excel worksheet as text file in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Worksheet%20Features/Save%20TextFile).

## Save Worksheet as HTML

XlsIO provides support to convert a worksheet or entire workbook to HTML with basic formatting preserved. The supporting formats in this conversion are:

1. Styles.
2. Hyperlinks.
3. Images.
4. 2D Charts.

The following code example illustrates this.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];
  sheet.Range["A1:M20"].Text = "Html Document";

  //Save an Excel sheet as HTML file
  sheet.SaveAsHtml("Sample.html");

  //Save the workbook as HTML file
  workbook.SaveAsHtml("Sample.html", Syncfusion.XlsIO.Implementation.HtmlSaveOptions.Default);
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim sheet As IWorksheet = workbook.Worksheets(0)
  sheet.Range("A1:M20").Text = "Html Document"

  'Save an Excel sheet as HTML file
  sheet.SaveAsHtml("Sample.html")

  'Save a workbook as HTML file
  workbook.SaveAsHtml("Sample.html", Syncfusion.XlsIO.Implementation.HtmlSaveOptions.Default)
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Worksheet To HTML conversion can be performed by referring .NET Standard assemblies in UWP platform.
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;

  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];
  sheet.Range["A1:M20"].Text = "Html Document";

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Sample";
  savePicker.FileTypeChoices.Add("HTML Files", new List<string>() { ".html",".htm" });

  //Creates a storage file from the FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Converts and save to stream
  var file = await storageFile.OpenAsync(FileAccessMode.ReadWrite);
  Stream stream = file.AsStreamForWrite();
  
  //Save an Excel sheet as HTML file
  sheet.SaveAsHtml(stream);
  
  //Save a workbook as HTML file
  workbook.SaveAsHtml(stream, Syncfusion.XlsIO.Implementation.HtmlSaveOptions.Default);
  await file.FlushAsync();
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  //Initialize excel engine and open workbook
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];
  worksheet.Range["A1:M20"].Text = "Html Document";

  //Create stream to store HTML file.
  Stream stream = new MemoryStream();

  //Save an Excel sheet as HTML file
  worksheet.SaveAsHtml(stream);
  
  //Save a workbook as HTML file
  workbook.SaveAsHtml(stream, Syncfusion.XlsIO.Implementation.HtmlSaveOptions.Default);
  stream.Dispose();
  workbook.Close();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];
  sheet.Range["A1:M20"].Text = "Html Document";

  //Creates memory stream.
  MemoryStream stream = new MemoryStream();
  
  //Save an Excel sheet as HTML file
  sheet.SaveAsHtml(stream);

  //Save a workbook as HTML file
  workbook.SaveAsHtml(stream, Syncfusion.XlsIO.Implementation.HtmlSaveOptions.Default);
  
  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies among Windows Phone, Android, and iOS platforms. Refer to the xlsio/xamarin section for respective code samples.
  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
      DependencyService.Get<ISaveWindowsPhone>()
          .Save("Sample.html", "text/html", stream);
  else
      DependencyService.Get<ISave>().Save("Sample.html", "text/html", stream);
}
{% endhighlight %}
{% endtabs %}   

### Save Options

XlsIO also provides options to save a worksheet with the displayed text or value in the cell to HTML file. The following code example illustrates this.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Create the instant for SaveOptions
  HtmlSaveOptions options = new HtmlSaveOptions();
  options.TextMode = HtmlSaveOptions.GetText.DisplayText;
  options.ImagePath = @"..\..\Images\";

  //Save the sheet as HTML
  sheet.SaveAsHtml("Sample.html", options);

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Create the instant for SaveOptions
  Dim options As New HtmlSaveOptions()
  options.TextMode = HtmlSaveOptions.GetText.DisplayText
  options.ImagePath = "..\..\Images\"

  'Save the sheet as HTML
  sheet.SaveAsHtml("Sample.html", options)

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Worksheet To HTML conversion can be performed by referring .NET Standard assemblies in UWP platform.
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;

  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Sample";
  savePicker.FileTypeChoices.Add("HTML Files", new List<string>() { ".html",".htm" });

  //Creates a storage file from the FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Create the instant for SaveOptions
  HtmlSaveOptions saveOptions = new HtmlSaveOptions();
  saveOptions.TextMode = HtmlSaveOptions.GetText.DisplayText;

  //Converts and save to stream
  var file = await storageFile.OpenAsync(FileAccessMode.ReadWrite);
  Stream stream = file.AsStreamForWrite();
  sheet.SaveAsHtml(stream, saveOptions);
  await file.FlushAsync();
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  //Initialize excel engine and open workbook
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Create stream to store HTML file.
  Stream stream = new MemoryStream();

  //Create the instant for SaveOptions
  HtmlSaveOptions saveOptions = new HtmlSaveOptions();
  saveOptions.TextMode = HtmlSaveOptions.GetText.DisplayText;

  //Save and Dispose
  worksheet.SaveAsHtml(stream, saveOptions);
  stream.Dispose();
  workbook.Close();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  
  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Create the instant for SaveOptions
  HtmlSaveOptions saveOptions = new HtmlSaveOptions();
  saveOptions.TextMode = HtmlSaveOptions.GetText.DisplayText;

  //Converts and save to stream.
  MemoryStream stream = new MemoryStream();
  sheet.SaveAsHtml(stream, saveOptions);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies among Windows Phone, Android, and iOS platforms. Refer to the xlsio/xamarin section for respective code samples.
  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
      DependencyService.Get<ISaveWindowsPhone>()
          .Save("Sample.html", "text/html", stream);
  else
      DependencyService.Get<ISave>().Save("Sample.html", "text/html", stream);
}
{% endhighlight %}
{% endtabs %}  

A complete working example to save an Excel worksheet as HTML file using HtmlSaveOptions in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Worksheet%20Features/Save%20HTML).

