---
title: Loading and saving workbook |Syncfusion|
description: Explains the various types of the load and save operations in present in the Syncfusion XlsIO control
platform: file-formats
control: XlsIO
documentation: UG
---

# Loading and Saving Workbook

## Opening an existing workbook

You can open an existing workbook by using the [Open](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbooks.html#Syncfusion_XlsIO_IWorkbooks_Open_System_String_) method of [IWorkbooks](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbooks.html) interface.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
//Creates a new instance for ExcelEngine
ExcelEngine excelEngine = new ExcelEngine();

//Loads or open an existing workbook through Open method of IWorkbooks
IWorkbook workbook = excelEngine.Excel.Workbooks.Open(inputFileName);
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Creates a new instance for ExcelEngine
Dim excelEngine As New ExcelEngine()

'Loads or open an existing workbook through Open method of IWorkbooks
Dim workbook As IWorkbook = excelEngine.Excel.Workbooks.Open(inputFileName)
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
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

{% highlight c# tabtitle="ASP.NET Core" %}
//Creates a new instance for ExcelEngine
ExcelEngine excelEngine = new ExcelEngine();

//Loads or open an existing workbook through Open method of IWorkbooks
FileStream inputStream = new FileStream(inputFileName, FileMode.Open);
IWorkbook workbook = excelEngine.Excel.Workbooks.Open(inputStream);
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
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
{% highlight c# tabtitle="C#" %}
IApplication application = excelEngine.Excel;

//Optimize parsing
application.UseFastRecordParsing = true;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Dim application As IApplication = excelEngine.Excel

'Optimize parsing
application.UseFastRecordParsing = True
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
IApplication application = excelEngine.Excel;

//Optimize parsing
application.UseFastRecordParsing = true;
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
IApplication application = excelEngine.Excel;

//Optimize parsing
application.UseFastRecordParsing = true;
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
IApplication application = excelEngine.Excel;

//Optimize parsing
application.UseFastRecordParsing = true;
{% endhighlight %}
{% endtabs %}  
  
## Opening an existing workbook from Stream

You can open an existing workbook from stream by using the overloads of [Open](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbooks.html#Syncfusion_XlsIO_IWorkbooks_Open_System_String_Syncfusion_XlsIO_ExcelOpenType_) methods of [IWorkbooks](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbooks.html) interface.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
//Creates a new instance for ExcelEngine
ExcelEngine excelEngine = new ExcelEngine();

//Load the file into stream
FileStream inputStream = new FileStream(inputFileName, FileMode.Open);

//Loads or open an existing workbook through Open method of IWorkbooks
IWorkbook workbook = excelEngine.Excel.Workbooks.Open(inputStream);
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Creates a new instance for ExcelEngine
Dim excelEngine As New ExcelEngine()

'Load the file into stream
Dim inputStream As FileStream = New FileStream(inputFileName, FileMode.Open)

'Loads or open an existing workbook through Open method of IWorkbooks
Dim workbook As IWorkbook = excelEngine.Excel.Workbooks.Open(inputStream)
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Creates a new instance for ExcelEngine
ExcelEngine excelEngine = new ExcelEngine();

//Load the file into stream
FileStream inputStream = new FileStream(inputFileName, FileMode.Open);

//Loads or open an existing workbook
IWorkbook workbook = await application.Workbooks.OpenAsync(inputStream);
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Creates a new instance for ExcelEngine
ExcelEngine excelEngine = new ExcelEngine();

//Load the file into stream
FileStream inputStream = new FileStream(inputFileName, FileMode.Open);

//Loads or open an existing workbook through Open method of IWorkbooks
IWorkbook workbook = application.Workbooks.Open(inputStream);
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
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

You can save the created or manipulated workbook to file system using [SaveAs](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbook.html#Syncfusion_XlsIO_IWorkbook_SaveAs_System_String_System_String_) method of [IWorkbook](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbook.html) interface. The workbook is saved in the XLS/XLSX format based on the application/workbook version specified, whereas saved in Excel 97-2003 (*.xls) format by default.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
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

{% highlight vb.net tabtitle="VB.NET" %}
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

{% highlight c# tabtitle="UWP" %}
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

{% highlight c# tabtitle="ASP.NET Core" %}
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

{% highlight c# tabtitle="Xamarin" %}
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

You can also save the created or manipulated workbook to stream using overloads of [SaveAs](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbook.html#Syncfusion_XlsIO_IWorkbook_SaveAs_System_String_System_String_System_Text_Encoding_) methods

{% tabs %}  
{% highlight c# tabtitle="C#" %}
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

{% highlight vb.net tabtitle="VB.NET" %}
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

{% highlight c# tabtitle="UWP" %}
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

{% highlight c# tabtitle="ASP.NET Core" %}
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

{% highlight c# tabtitle="Xamarin" %}
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

Once after the workbook manipulation and save operation are completed, you should close the instance of [IWorkbook](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbook.html) and dispose the instance of [ExcelEngine](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelEngine.html), in order to release all the memory consumed by XlsIO’s DOM. The following code snippet illustrates how to close the instance of [IWorkbook](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbook.html) and dispose the instance of [ExcelEngine](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelEngine.html).

N> If the new instance for [ExcelEngine](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelEngine.html) is created in using statement, then there is no need to closing workbook and disposing excelEngine.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
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

{% highlight vb.net tabtitle="VB.NET" %}
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

{% highlight c# tabtitle="UWP" %}
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

{% highlight c# tabtitle="ASP.NET Core" %}
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

{% highlight c# tabtitle="Xamarin" %}
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

T>You can use [ThrowNotSavedOnDestroy](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelEngine.html#Syncfusion_XlsIO_ExcelEngine_ThrowNotSavedOnDestroy) property of [ExcelEngine](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelEngine.html) object to prevent the data loss while unfortunately closing the workbook or disposing excel engine without saving contents. If it is set to true, then **ExcelWorkbookNotSavedException** will be thrown when you forgot to save the workbook before closing them. Following code illustrates how to set [ThrowNotSavedOnDestroy](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelEngine.html#Syncfusion_XlsIO_ExcelEngine_ThrowNotSavedOnDestroy) property of [ExcelEngine](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelEngine.html) object.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
ExcelEngine excelEngine = new ExcelEngine();

//No exception will be thrown if there are unsaved workbooks
excelEngine.ThrowNotSavedOnDestroy = true;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Dim excelEngine As New ExcelEngine()

'No exception will be thrown if there are unsaved workbooks
excelEngine.ThrowNotSavedOnDestroy = True
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
ExcelEngine excelEngine = new ExcelEngine();

//No exception will be thrown if there are unsaved workbooks
excelEngine.ThrowNotSavedOnDestroy = true;
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
ExcelEngine excelEngine = new ExcelEngine();

//No exception will be thrown if there are unsaved workbooks
excelEngine.ThrowNotSavedOnDestroy = true;
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
ExcelEngine excelEngine = new ExcelEngine();

//No exception will be thrown if there are unsaved workbooks
excelEngine.ThrowNotSavedOnDestroy = true;
{% endhighlight %}
{% endtabs %} 

A complete working example for creating and editing an Excel workbook in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Read%20and%20Edit%20Excel/Read%20and%20Edit%20Excel).
 
## Sending to a client browser

You can save & send the workbook to a client browser from a web site or web application by invoking the below shown overload of [SaveAs](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbook.html#Syncfusion_XlsIO_IWorkbook_SaveAs_System_String_System_Web_HttpResponse_Syncfusion_XlsIO_ExcelDownloadType_) method. This method explicitly make use of an instance of [HttpResponse](https://learn.microsoft.com/en-us/dotnet/api/system.web.httpresponse?view=netframework-4.8) as its parameter in order to stream the workbook to client browser. So this overload is suitable for web application which references **System.Web** assembly.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
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

{% highlight vb.net tabtitle="VB.NET" %}
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

{% highlight c# tabtitle="UWP" %}
//Saving and sending the workbook to a client browser from a web site is suitable for web applications alone.
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
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

{% highlight c# tabtitle="Xamarin" %}
//Saving and sending the workbook to a client browser from a web site is suitable for web applications alone.
{% endhighlight %}
{% endtabs %}  
