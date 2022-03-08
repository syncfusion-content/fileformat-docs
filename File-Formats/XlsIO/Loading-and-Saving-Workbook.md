---
title: Loading and saving workbook |Syncfusion|
description: Explains the various types of the load and save operations in present in the Syncfusion XlsIO control
platform: File-formats
control: XlsIO
documentation: UG
---

# Loading and Saving Workbook

## Opening an existing workbook

You can open an existing workbook by using the Open method of IWorkbooks interface.

{% tabs %}  
{% highlight C# %}
//Creates a new instance for ExcelEngine
ExcelEngine excelEngine = new ExcelEngine();

//Loads or open an existing workbook through Open method of IWorkbooks
IWorkbook workbook = excelEngine.Excel.Workbooks.Open(inputFileName);
{% endhighlight %}

{% highlight VB.NET %}
'Creates a new instance for ExcelEngine
Dim excelEngine As New ExcelEngine()

'Loads or open an existing workbook through Open method of IWorkbooks
Dim workbook As IWorkbook = excelEngine.Excel.Workbooks.Open(inputFileName)
{% endhighlight %}

{% highlight UWP %}
//Creates a new instance for ExcelEngine
ExcelEngine excelEngine = new ExcelEngine();

//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".xlsx");
openPicker.FileTypeFilter.Add(".xls");

//Creates a storage file from FileOpenPicker
StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();
  
//Loads or open an existing workbook
IWorkbook workbook = await excelEngine.Excel.Workbooks.OpenAsync(inputStorageFile);
{% endhighlight %}

{% highlight ASP.NET CORE %}
//Creates a new instance for ExcelEngine
ExcelEngine excelEngine = new ExcelEngine();

//Loads or open an existing workbook through Open method of IWorkbooks
FileStream inputStream = new FileStream(inputFileName, FileMode.Open);
IWorkbook workbook = excelEngine.Excel.Workbooks.Open(inputStream);
{% endhighlight %}

{% highlight XAMARIN %}
//Creates a new instance for ExcelEngine
ExcelEngine excelEngine = new ExcelEngine();

//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream(inputFilePath);

//Loads or open an existing workbook through Open method of IWorkbooks
IWorkbook workbook = excelEngine.Excel.Workbooks.Open(inputStream);
{% endhighlight %}
{% endtabs %}  

T>Files parsing can be optimized by setting **IApplication****.****UseFastRecordParsing** = **false** or **true** (true –fast mode, but less error checks and false – slower but more reliable).

{% tabs %}  
{% highlight C# %}
IApplication application = excelEngine.Excel;

//Optimize parsing
application.UseFastRecordParsing = true;
{% endhighlight %}

{% highlight VB.NET %}
Dim application As IApplication = excelEngine.Excel

'Optimize parsing
application.UseFastRecordParsing = True
{% endhighlight %}

{% highlight UWP %}
IApplication application = excelEngine.Excel;

//Optimize parsing
application.UseFastRecordParsing = true;
{% endhighlight %}

{% highlight ASP.NET CORE %}
IApplication application = excelEngine.Excel;

//Optimize parsing
application.UseFastRecordParsing = true;
{% endhighlight %}

{% highlight XAMARIN %}
IApplication application = excelEngine.Excel;

//Optimize parsing
application.UseFastRecordParsing = true;
{% endhighlight %}
{% endtabs %}  
  
## Opening an existing workbook from Stream

You can open an existing workbook from stream by using the overloads of Open methods of IWorkbooks interface.

{% tabs %}  
{% highlight C# %}
//Creates a new instance for ExcelEngine
ExcelEngine excelEngine = new ExcelEngine();

//Load the file into stream
FileStream inputStream = new FileStream(inputFileName, FileMode.Open);

//Loads or open an existing workbook through Open method of IWorkbooks
IWorkbook workbook = excelEngine.Excel.Workbooks.Open(inputStream);
{% endhighlight %}

{% highlight VB.NET %}
'Creates a new instance for ExcelEngine
Dim excelEngine As New ExcelEngine()

'Load the file into stream
Dim inputStream As FileStream = New FileStream(inputFileName, FileMode.Open)

'Loads or open an existing workbook through Open method of IWorkbooks
Dim workbook As IWorkbook = excelEngine.Excel.Workbooks.Open(inputStream)
{% endhighlight %}

{% highlight UWP %}
//Creates a new instance for ExcelEngine
ExcelEngine excelEngine = new ExcelEngine();

//Load the file into stream
FileStream inputStream = new FileStream(inputFileName, FileMode.Open);

//Loads or open an existing workbook
IWorkbook workbook = await application.Workbooks.OpenAsync(inputStream);
{% endhighlight %}

{% highlight ASP.NET CORE %}
//Creates a new instance for ExcelEngine
ExcelEngine excelEngine = new ExcelEngine();

//Load the file into stream
FileStream inputStream = new FileStream(inputFileName, FileMode.Open);

//Loads or open an existing workbook through Open method of IWorkbooks
IWorkbook workbook = application.Workbooks.Open(inputStream);
{% endhighlight %}

{% highlight XAMARIN %}
//Creates a new instance for ExcelEngine
ExcelEngine excelEngine = new ExcelEngine();

//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream(inputFilePath);

//Loads or open an existing workbook through Open method of IWorkbooks
IWorkbook workbook = application.Workbooks.Open(inputStream);
{% endhighlight %}
{% endtabs %}  

## Saving a Excel workbook to file system

You can save the created or manipulated workbook to file system using Save method of IWorkbook interface. The workbook is saved in the XLS/XLSX format based on the application/workbook version specified, whereas saved in Excel 97-2003 (*.xls) format by default.

{% tabs %}  
{% highlight C# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  //Loads or open an existing workbook through Open method of IWorkbooks
  IWorkbook workbook = excelEngine.Excel.Workbooks.Open(inputFileName);

  //To-Do some manipulation
  //To-Do some manipulation

  //Set the version of the workbook
  workbook.Version = ExcelVersion.Excel2013;

  //Save the workbook in file system as XLSX format
  workbook.SaveAs(outputFileName);
}
{% endhighlight %}

{% highlight VB.NET %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  'Loads or open an existing workbook through Open method of IWorkbooks
  Dim workbook As IWorkbook = excelEngine.Excel.Workbooks.Open(inputFileName)

  'To-Do some manipulation
  'To-Do some manipulation

  'Set the version of the workbook
  workbook.Version = ExcelVersion.Excel2013

  'Save the workbook in file system as XLSX format
  workbook.SaveAs(outputFileName)
End Using
{% endhighlight %}

{% highlight UWP %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  //Instantiates the File Picker
  FileOpenPicker openPicker = new FileOpenPicker();
  openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
  openPicker.FileTypeFilter.Add(".xlsx");
  openPicker.FileTypeFilter.Add(".xls");

  //Creates a storage file from FileOpenPicker
  StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();

  //Loads or open an existing workbook
  IWorkbook workbook = await excelEngine.Excel.Workbooks.OpenAsync(inputStorageFile);

  //To-Do some manipulation
  //To-Do some manipulation

  //Set the version of the workbook
  workbook.Version = ExcelVersion.Excel2013;

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = OutputFileName;
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

  //Creates a storage file from FileSavePicker
  StorageFile outputStorageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  await workbook.SaveAsAsync(outputStorageFile);
}
{% endhighlight %}

{% highlight ASP.NET CORE %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  //Loads or open an existing workbook
  FileStream inputStream = new FileStream(inputFileName, FileMode.Open);
  IWorkbook workbook = excelEngine.Excel.Workbooks.Open(inputStream);

  //To-Do some manipulation
  //To-Do some manipulation

  //Set the version of the workbook
  workbook.Version = ExcelVersion.Excel2013;

  //Saving the workbook
  FileStream outputStream = new FileStream(outputFileName, FileMode.Create);
  workbook.SaveAs(outputStream);
}
{% endhighlight %}

{% highlight XAMARIN %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream = assembly.GetManifestResourceStream(inputFilePath);

  //Loads or open an existing workbook through Open method of IWorkbooks
  IWorkbook workbook = excelEngine.Excel.Workbooks.Open(inputStream);

  //To-Do some manipulation
  //To-Do some manipulation

  //Set the version of the workbook
  workbook.Version = ExcelVersion.Excel2013;

  //Saving the workbook
  MemoryStream outputStream = new MemoryStream();
  workbook.SaveAs(outputStream);

  outputStream.Position = 0;

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
  	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView(outputFileName, "application/msexcel", outputStream);
  }
  else
  {
  	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView(outputFileName, "application/msexcel", outputStream);
  }
}
{% endhighlight %}
{% endtabs %}  

## Saving a Excel workbook to stream

You can also save the created or manipulated workbook to stream using overloads of Save methods

{% tabs %}  
{% highlight C# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  //Loads or open an existing workbook through Open method of IWorkbooks
  IWorkbook workbook = excelEngine.Excel.Workbooks.Open(inputFileName);

  //To-Do some manipulation
  //To-Do some manipulation

  //Set the version of the workbook
  workbook.Version = ExcelVersion.Excel2013;

  //Save the workbook as stream
  MemoryStream outputStream = new MemoryStream();
  workbook.SaveAs(outputStream);
}
{% endhighlight %}

{% highlight VB.NET %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  'Loads or open an existing workbook through Open method of IWorkbooks
  Dim workbook As IWorkbook = excelEngine.Excel.Workbooks.Open(inputFileName)

  'To-Do some manipulation
  'To-Do some manipulation

  'Set the version of the workbook
  workbook.Version = ExcelVersion.Excel2013

  'Save the workbook as stream
  Dim outputStream As MemoryStream = New MemoryStream
  workbook.SaveAs(outputStream)
End Using
{% endhighlight %}

{% highlight UWP %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  //Instantiates the File Picker
  FileOpenPicker openPicker = new FileOpenPicker();
  openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
  openPicker.FileTypeFilter.Add(".xlsx");
  openPicker.FileTypeFilter.Add(".xls");

  //Creates a storage file from FileOpenPicker
  StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();

  //Loads or open an existing workbook
  IWorkbook workbook = await excelEngine.Excel.Workbooks.OpenAsync(inputStorageFile);

  //To-Do some manipulation
  //To-Do some manipulation

  //Set the version of the workbook
  workbook.Version = ExcelVersion.Excel2013;

  //Saves changes to the specified storage file
  MemoryStream outputStream = new MemoryStream();
  await workbook.SaveAsAsync(outputStream);
}
{% endhighlight %}

{% highlight ASP.NET CORE %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  //Loads or open an existing workbook through Open method of IWorkbooks
  FileStream inputStream = new FileStream(inputFileName, FileMode.Open);
  IWorkbook workbook = excelEngine.Excel.Workbooks.Open(inputStream);

  //To-Do some manipulation
  //To-Do some manipulation

  //Set the version of the workbook
  workbook.Version = ExcelVersion.Excel2013;

  //Saving the workbook as stream
  MemoryStream outputStream = new MemoryStream();
  workbook.SaveAs(outputStream);
}
{% endhighlight %}

{% highlight XAMARIN %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  //"App" is the class of Portable project
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream inputStream = assembly.GetManifestResourceStream(inputFilePath);

  //Loads or open an existing workbook through Open method of IWorkbooks
  IWorkbook workbook = excelEngine.Excel.Workbooks.Open(inputStream);

  //To-Do some manipulation
  //To-Do some manipulation

  //Set the version of the workbook
  workbook.Version = ExcelVersion.Excel2013;

  //Save the workbook as stream
  MemoryStream outputStream = new MemoryStream();
  workbook.SaveAs(outputStream);
}
{% endhighlight %}
{% endtabs %} 

## Closing a workbook

Once after the workbook manipulation and save operation are completed, you should close the instance of IWorkbook and dispose the instance of ExcelEngine, in order to release all the memory consumed by XlsIO’s DOM. The following code snippet illustrates how to close the instance of IWorkbook and dispose the instance of ExcelEngine.

N> If the new instance for ExcelEngine is created in using statement, then there is no need to closing workbook and disposing excelEngine.

{% tabs %}  
{% highlight C# %}
//Creates a new instance for ExcelEngine
ExcelEngine excelEngine = new ExcelEngine();

//Loads or open an existing workbook through Open method of IWorkbooks
IWorkbook workbook = excelEngine.Excel.Workbooks.Open(inputFileName);

//To-Do some manipulation
//To-Do some manipulation

//Set the version of the workbook
workbook.Version = ExcelVersion.Excel2013;

//Save the workbook in file system
workbook.SaveAs(outputFileName);

//Close the instance of IWorkbook
workbook.Close();

//Dispose the instance of ExcelEngine
excelEngine.Dispose();
{% endhighlight %}

{% highlight VB.NET %}
'Creates a new instance for ExcelEngine
Dim excelEngine As New ExcelEngine()

'Loads or open an existing workbook through Open method of IWorkbooks
Dim workbook As IWorkbook = excelEngine.Excel.Workbooks.Open(inputFileName)

'To-Do some manipulation
'To-Do some manipulation

'Set the version of the workbook
workbook.Version = ExcelVersion.Excel2013

'Save the workbook in file system
workbook.SaveAs(outputFileName)

'Close the instance of IWorkbook
workbook.Close()

'Dispose the instance of ExcelEngine
excelEngine.Dispose()
{% endhighlight %}

{% highlight UWP %}
//Creates a new instance for ExcelEngine
ExcelEngine excelEngine = new ExcelEngine();

//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".xlsx");
openPicker.FileTypeFilter.Add(".xls");

//Creates a storage file from FileOpenPicker
StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();
  
//Loads or open an existing workbook
IWorkbook workbook = excelEngine.Excel.Workbooks.OpenAsync(inputStorageFile);

//To-Do some manipulation
//To-Do some manipulation

//Set the version of the workbook
workbook.Version = ExcelVersion.Excel2013;

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Output";
savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await workbook.SaveAsAsync(outputStorageFile);

//Close the instance of IWorkbook
workbook.Close();

//Dispose the instance of ExcelEngine
excelEngine.Dispose();
{% endhighlight %}

{% highlight ASP.NET CORE %}
//Creates a new instance for ExcelEngine
ExcelEngine excelEngine = new ExcelEngine();

//Loads or open an existing workbook through Open method of IWorkbooks
FileStream inputStream = new FileStream(inputFileName, FileMode.Open);
IWorkbook workbook = excelEngine.Excel.Workbooks.Open(inputStream);

//To-Do some manipulation
//To-Do some manipulation

//Set the version of the workbook
workbook.Version = ExcelVersion.Excel2013;

//Save the workbook as stream
FileStream outputStream = new FileStream("Output.xlsx", FileMode.Create);
workbook.SaveAs(outputStream);

//Close the instance of IWorkbook
workbook.Close();

//Dispose the instance of ExcelEngine
excelEngine.Dispose();
{% endhighlight %}

{% highlight XAMARIN %}
//Creates a new instance for ExcelEngine
ExcelEngine excelEngine = new ExcelEngine();

//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream(inputFilePath);

//Loads or open an existing workbook through Open method of IWorkbooks
IWorkbook workbook = excelEngine.Excel.Workbooks.Open(inputStream);

//To-Do some manipulation
//To-Do some manipulation

//Set the version of the workbook
workbook.Version = ExcelVersion.Excel2013;

//Save the workbook as stream
MemoryStream outputStream = new MemoryStream();
workbook.SaveAs(outputStream);

outputStream.Position = 0;

//Save the document as file and view the saved document

//The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
  Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Output.xlsx", "application/msexcel", outputStream);
}
else
{
  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", outputStream);
}

//Close the instance of IWorkbook
workbook.Close();

//Dispose the instance of ExcelEngine
excelEngine.Dispose();
{% endhighlight %}
{% endtabs %}

T>You can use ThrowNotSavedOnDestroy property of ExcelEngine object to prevent the data loss while unfortunately closing the workbook or disposing excel engine without saving contents. If it is set to true, then ExcelWorkbookNotSavedException will be thrown when you forgot to save the workbook before closing them. Following code illustrates how to set ThrowNotSavedOnDestroy property of ExcelEngine object.

{% tabs %}  
{% highlight C# %}
ExcelEngine excelEngine = new ExcelEngine();

//No exception will be thrown if there are unsaved workbooks
excelEngine.ThrowNotSavedOnDestroy = true;
{% endhighlight %}

{% highlight VB.NET %}
Dim excelEngine As New ExcelEngine()

'No exception will be thrown if there are unsaved workbooks
excelEngine.ThrowNotSavedOnDestroy = True
{% endhighlight %}

{% highlight UWP %}
ExcelEngine excelEngine = new ExcelEngine();

//No exception will be thrown if there are unsaved workbooks
excelEngine.ThrowNotSavedOnDestroy = true;
{% endhighlight %}

{% highlight ASP.NET CORE %}
ExcelEngine excelEngine = new ExcelEngine();

//No exception will be thrown if there are unsaved workbooks
excelEngine.ThrowNotSavedOnDestroy = true;
{% endhighlight %}

{% highlight XAMARIN %}
ExcelEngine excelEngine = new ExcelEngine();

//No exception will be thrown if there are unsaved workbooks
excelEngine.ThrowNotSavedOnDestroy = true;
{% endhighlight %}
{% endtabs %} 

A complete working example for creating and editing an Excel workbook in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Read%20and%20Edit%20Excel/Read%20and%20Edit%20Excel).
 
## Sending to a client browser

You can save & send the workbook to a client browser from a web site or web application by invoking the below shown overload of Save method.  This method explicitly make use of an instance of [HttpResponse](https://docs.microsoft.com/en-us/dotnet/api/system.web.httpresponse?view=netframework-4.8) as its parameter in order to stream the workbook to client browser. So this overload is suitable for web application which references System.Web assembly.

{% tabs %}  
{% highlight C# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  //Loads or open an existing workbook through Open method of IWorkbooks
  IWorkbook workbook = excelEngine.Excel.Workbooks.Open(inputFileName);

  //To-Do some manipulation
  //To-Do some manipulation

  //Set the version of the workbook
  workbook.Version = ExcelVersion.Excel2013;

  //Save the workbook in file system
  workbook.SaveAs(OutputFileName, Response, ExcelDownloadType.Open);
}
{% endhighlight %}

{% highlight VB.NET %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  'Loads or open an existing workbook through Open method of IWorkbooks
  Dim workbook As IWorkbook = excelEngine.Excel.Workbooks.Open(inputFileName)

  'To-Do some manipulation
  'To-Do some manipulation

  'Set the version of the workbook
  workbook.Version = ExcelVersion.Excel2013

  'Save the workbook in file system
  workbook.SaveAs(OutputFileName, Response, ExcelDownloadType.Open)
End Using
{% endhighlight %}

{% highlight UWP %}
//Saving and sending the workbook to a client browser from a web site is suitable for web applications alone.
{% endhighlight %}

{% highlight ASP.NET CORE %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  //Loads or open an existing workbook through Open method of IWorkbooks
  FileStream inputStream = new FileStream(inputFilePath, FileMode.Open);  
  IWorkbook workbook = excelEngine.Excel.Workbooks.Open(inputStream);

  //To-Do some manipulation
  //To-Do some manipulation

  //Initialize content type
  string ContentType = null;

  //Set the version of the workbook
  workbook.Version = ExcelVersion.Excel2013;
  ContentType = "Application/msexcel";

  //Save the workbook to stream
  MemoryStream outputStream = new MemoryStream();
  workbook.SaveAs(outputStream);
  outputStream.Position = 0;

  //Return the file with content type
  return File(outputStream, ContentType, outputFileName);
}
{% endhighlight %}

{% highlight XAMARIN %}
//Saving and sending the workbook to a client browser from a web site is suitable for web applications alone.
{% endhighlight %}
{% endtabs %}  

 

