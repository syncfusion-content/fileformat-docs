---
title: Syncfusion Excel to JSON Conversion
description: In this section, you can learn how to Export Excel workbook, worksheet, and custom range Data as JSON
platform: file-formats
control: XlsIO
documentation: UG
---

# Excel to JSON Conversion

Essential XlsIO supports to convert Excel data as JSON files by simply saving the workbook using the [SaveAsJson](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbook.html#Syncfusion_XlsIO_IWorkbook_SaveAsJson_System_String_) method. This support includes the features:

* Save as a simple JSON file or a JSON file as schema
* Save a workbook to JSON
* Save a worksheet to JSON
* Save a range to JSON
* Save as a stream with the above features

## Workbook to JSON as schema

The following code illustrates how to convert an Excel workbook to the JSON file or JSON file stream as schema.

{% tabs %}  

{% highlight c# tabtitle="C#" %}
using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

  //Saves the workbook to a JSON file, as schema by default
  workbook.SaveAsJson("Excel-Workbook-To-JSON-as-schema-default.json");

  //Saves the workbook to a JSON file as schema
  workbook.SaveAsJson("Excel-Workbook-To-JSON-as-schema.json", true);

  //Saves the workbook to a JSON filestream, as schema by default
  FileStream stream = new FileStream("Excel-Workbook-To-JSON-filestream-as-schema-default.json", FileMode.Create);
  workbook.SaveAsJson(stream);

  //Saves the workbook to a JSON filestream as schema
  FileStream stream1 = new FileStream("Excel-Workbook-To-JSON-filestream-as-schema.json", FileMode.Create);
  workbook.SaveAsJson(stream1, true);
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

  'Saves the workbook to a JSON file, as schema by default
  workbook.SaveAsJson("Excel-Workbook-To-JSON-as-schema-default.json")
	
  'Saves the workbook to a JSON file as schema
  workbook.SaveAsJson("Excel-Workbook-To-JSON-as-schema.json", true)

  'Saves the workbook to a JSON filestream as schema by default
  Dim stream As FileStream = new FileStream("Excel-Workbook-To-JSON-filestream-as-schema-default.json", FileMode.Create)
  workbook.SaveAsJson(stream)

  'Saves the workbook to a JSON filestream as schema
  Dim stream1 As FileStream = new FileStream("Excel-Workbook-To-JSON-filestream-as-schema.json",FileMode.Create)
  workbook.SaveAsJson(stream1, true)
End Using
{% endhighlight %}
{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Sample.xlsx");
  IWorkbook workbook = await excelEngine.Excel.Workbooks.OpenAsync(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Excel-To-JSON-as-schema-default";
  savePicker.FileTypeChoices.Add("JSON Files", new List<string>() { ".json" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves the workbook to a JSON as specified storage file, as schema by default
  await workbook.SaveAsJsonAsync(storageFile);

  //Saves the workbook to a JSON filestream, as schema by default
  MemoryStream stream = new MemoryStream();
  workbook.Version = ExcelVersion.Xlsx;
  await workbook.SaveAsJsonAsync(stream);
  Save(stream, "Excel-Workbook-To-JSON-filestream-as-schema-default.json");

  stream.Dispose();
  inputStream.Dispose();
}

//Save the workbook stream as a file.

#region Setting output location
async void Save(Stream stream, string filename)
{
  stream.Position = 0;

  StorageFile stFile;
  if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
  {
    FileSavePicker savePicker = new FileSavePicker();
    savePicker.DefaultFileExtension = ".json";
    savePicker.SuggestedFileName = filename;
    savePicker.FileTypeChoices.Add("JSON Files", new List<string>() { ".json" });
    stFile = await savePicker.PickSaveFileAsync();
  }
  else
  {
    StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
    stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
  }
  if (stFile != null)
  {
    Windows.Storage.Streams.IRandomAccessStream fileStream = await stFile.OpenAsync(FileAccessMode.ReadWrite);
    Stream st = fileStream.AsStreamForWrite();
    st.Write((stream as MemoryStream).ToArray(), 0, (int)stream.Length);
    st.Flush();
    st.Dispose();
    fileStream.Dispose();
  }
}
#endregion
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Saves the workbook to a JSON filestream, as schema by default
  FileStream stream = new FileStream("Excel-Workbook-To-JSON-as-schema-default.json", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAsJson(stream);

  //Saves the workbook to a JSON filestream as schema
  FileStream stream1 = new FileStream("Excel-Workbook-To-JSON-as-schema.json", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAsJson(stream1, true);

  stream.Dispose();
  stream1.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Sample.xlsx");  
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Saves the workbook as JSON filestream, as schema default 
  MemoryStream outputStream = new MemoryStream();
  workbook.SaveAsJson(outputStream);

  //Save the stream as JSON document and view the saved document    
  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.
  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Excel-Workbook-To-JSON-filestream-as-schema.json", "application/notepad", outputStream);
  }
  else
  {
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Excel-Workbook-To-JSON-filestream-as-schmea.json", "application/notepad", outputStream);
  }

  //Dispose the input and output stream instances
  inputStream.Dispose();
  outputStream.Dispose();
}

{% endhighlight %}
{% endtabs %}

A complete working example to convert Excel to JSON with schema in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Convert%20Excel%20to%20JSON/Workbook%20to%20JSON%20with%20Schema). 

## Workbook to JSON without schema

The following code illustrates how to convert an Excel workbook to the JSON file or JSON file stream without schema.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

  //Saves the workbook to a JSON file without schema
  workbook.SaveAsJson("Excel-Workbook-To-JSON-without-schema.json", false);

  //Saves the workbook to a JSON filestream without schema
  FileStream stream = new FileStream("Excel-Workbook-To-JSON-filestream-without-schema.json", FileMode.Create);
  workbook.SaveAsJson(stream, false);
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

  'Saves the workbook to a JSON file without schema
  workbook.SaveAsJson("Excel-Workbook-To-JSON-without-schema.json", false)

  'Saves the workbook to a JSON filestream without schema
  Dim stream As FileStream = new FileStream("Excel-Workbook-To-JSON-filestream-without-schema.json", FileMode.Create)
  workbook.SaveAsJson(stream, false)
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Sample.xlsx");
  IWorkbook workbook = await excelEngine.Excel.Workbooks.OpenAsync(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Excel-To-JSON-without-schema";
  savePicker.FileTypeChoices.Add("JSON Files", new List<string>() { ".json" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves workbook to JSON as specified storage file without schema
  await workbook.SaveAsJsonAsync(storageFile, file);

  //Saves the workbook to a JSON filestream without schema
  MemoryStream stream = new MemoryStream();
  workbook.Version = ExcelVersion.Xlsx;
  await workbook.SaveAsJsonAsync(stream, false);
  Save(stream, "Excel-Workbook-To-JSON-filestream-without-schema.json");

  stream.Dispose();
}

//Save the worksheet stream as a file.

#region Setting output location
async void Save(Stream stream, string filename)
{
  stream.Position = 0;

  StorageFile stFile;
  if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
  {
    FileSavePicker savePicker = new FileSavePicker();
    savePicker.DefaultFileExtension = ".json";
    savePicker.SuggestedFileName = filename;
    savePicker.FileTypeChoices.Add("JSON Files", new List<string>() { ".json" });
    stFile = await savePicker.PickSaveFileAsync();
  }
  else
  {
    StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
    stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
  }
  if (stFile != null)
  {
    Windows.Storage.Streams.IRandomAccessStream fileStream = await stFile.OpenAsync(FileAccessMode.ReadWrite);
    Stream st = fileStream.AsStreamForWrite();
    st.Write((stream as MemoryStream).ToArray(), 0, (int)stream.Length);
    st.Flush();
    st.Dispose();
    fileStream.Dispose();
  }
}
#endregion
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Saves the workbook to a JSON filestream without schema
  FileStream stream = new FileStream("Excel-Workbook-To-JSON-filestream-without-schema.json", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAsJson(stream, false);

  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Saves the workbook to JSON filestream without schema
  MemoryStream outputStream = new MemoryStream();
  workbook.SaveAsJson(outputStream, false);

  //Save the stream as JSON document and view the saved document    
  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.
  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Excel-Workbook-To-JSON-filestream-without-schema.json", "application/notepad", outputStream);
  }
  else
  {
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Excel-Workbook-To-JSON-filestream-without-schema.json", "application/notepad", outputStream);
  }

  //Dispose the input and output stream instances
  inputStream.Dispose();
  outputStream.Dispose();
}
{% endhighlight %}
{% endtabs %}

A complete working example to convert Excel to JSON without schema in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Convert%20Excel%20to%20JSON/Workbook%20to%20JSON%20without%20Schema). 

## Worksheet to JSON as schema

The following code illustrates how to convert an Excel worksheet to the JSON file or JSON file stream with schema.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

  //Active worksheet
  IWorksheet worksheet = workbook.Worksheets[0];

  //Saves the worksheet to a JSON file, as schema by default
  workbook.SaveAsJson("Excel-Worksheet-To-JSON-as-schema-default.json", worksheet);

  //Saves the worksheet to a JSON file as schema
  workbook.SaveAsJson("Excel-Worksheet-To-JSON-as-schema.json", worksheet, true);

  //Saves the worksheet to a JSON filestream, as schema by default
  FileStream stream = new FileStream("Excel-Worksheet-To-JSON-filestream-as-schema-default.json", FileMode.Create);
  workbook.SaveAsJson("stream", worksheet);

  //Saves the worksheet to a JSON filestream as schema
  FileStream stream1 = new FileStream("Excel-Worksheet-To-JSON-filestream-as-schema.json", FileMode.Create);
  workbook.SaveAsJson(stream1, worksheet, true);
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

  'Active worksheet
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Saves the worksheet to a JSON file, as schema by default
  workbook.SaveAsJson("Excel-Worksheet-To-JSON-as-schema-default.json", worksheet)

  'Saves the worksheet to a JSON file as schema
  workbook.SaveAsJson("Excel-Worksheet-To-JSON-as-schema.json", worksheet, true)

  'Saves the worksheet to a JSON filestream as schema by default
  Dim stream As FileStream = new FileStream("Excel-Worksheet-To-JSON-filestream-as-schema-default.json",FileMode.Create)
  workbook.SaveAsJson(stream, worksheet)

  'Saves the worksheet to a JSON filestream as schema
  Dim stream1 As FileStream = new FileStream("Excel-Worksheet-To-JSON-filestream-as-schema.json",FileMode.Create)
  workbook.SaveAsJson(stream1, worksheet, true)
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Sample.xlsx");
  IWorkbook workbook = await excelEngine.Excel.Workbooks.OpenAsync(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Excel-To-JSON-filestream-as-schema-default";
  savePicker.FileTypeChoices.Add("JSON Files", new List<string>() { ".json" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves the worksheet to JSON as specified storage file, as schema by default
  await workbook.SaveAsJsonAsync(storageFile, worksheet);

  //Saves the worksheet to a JSON filestream, as schema by default
  MemoryStream stream = new MemoryStream();
  workbook.Version = ExcelVersion.Xlsx;
  await workbook.SaveAsJsonAsync(stream, worksheet);
  Save(stream, "Excel-Worksheet-To-JSON-filestream-as-schema-default.json");
}

//Save the worksheet stream as a file.

#region Setting output location
async void Save(Stream stream, string filename)
{
  stream.Position = 0;

  StorageFile stFile;
  if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
  {
    FileSavePicker savePicker = new FileSavePicker();
    savePicker.DefaultFileExtension = ".json";
    savePicker.SuggestedFileName = filename;
    savePicker.FileTypeChoices.Add("JSON Files", new List<string>() { ".json" });
    stFile = await savePicker.PickSaveFileAsync();
  }
  else
  {
    StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
    stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
  }
  if (stFile != null)
  {
    Windows.Storage.Streams.IRandomAccessStream fileStream = await stFile.OpenAsync(FileAccessMode.ReadWrite);
    Stream st = fileStream.AsStreamForWrite();
    st.Write((stream as MemoryStream).ToArray(), 0, (int)stream.Length);
    st.Flush();
    st.Dispose();
    fileStream.Dispose();
  }
}
#endregion
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Saves the worksheet to a JSON filestream, as schema by default
  FileStream stream = new FileStream("Excel-Worksheet-To-JSON-filestream-as-schema-default.json", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAsJson(stream, worksheet);

  //Saves the worksheet to a JSON filestream as schema
  FileStream stream1 = new FileStream("Excel-Worksheet-To-JSON-filestream-as-schema.json", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAsJson(stream1, worksheet, true);

  stream.Dispose();
  stream1.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Saves the worksheet as JSON filestream, as schema by default 
  MemoryStream outputStream = new MemoryStream();
  workbook.SaveAsJson(outputStream, worksheet);

  //Save the stream as JSON document and view the saved document    
  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.
  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Excel-Worksheet-To-JSON-filestream-as-schema-default.json", "application/notepad", outputStream);
  }
  else
  {
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Excel-Worksheet-To-JSON-filestream-as-schema-default.json", "application/notepad", outputStream);
  }

  //Dispose the input and output stream instances
  inputStream.Dispose();
  outputStream.Dispose();
}
{% endhighlight %}
{% endtabs %}

A complete working example to convert Excel worksheet to JSON with schema in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Convert%20Excel%20to%20JSON/Worksheet%20to%20JSON%20with%20Schema). 

## Worksheet to JSON without schema

The following code illustrates how to convert an Excel worksheet to the JSON file or file stream without schema.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

  //Active worksheet
  IWorksheet worksheet = workbook.Worksheets[0];

  //Saves the worksheet to a JSON file without schema
  workbook.SaveAsJson("Excel-Worksheet-To-JSON-without-schema.json", worksheet, false);

  //Saves the worksheet to a JSON filestream without schema
  FileStream stream = new FileStream("Excel-Worksheet-To-JSON-filestream-without-schema.json", FileMode.Create); 
  workbook.SaveAsJson(stream, worksheet, false);
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

  'Active worksheet
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Saves the worksheet to a JSON file without schema
  workbook.SaveAsJson("Excel-Worksheet-To-JSON-without-schema.json", worksheet, false)

  'Saves the worksheet to a JSON filestream without schema
  Dim stream As FileStream = new FileStream("Excel-Worksheet-To-JSON-filestream-without-schema.json", FileMode.Create)
  workbook.SaveAsJson(stream, worksheet, false)
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Sample.xlsx");
  IWorkbook workbook = await excelEngine.Excel.Workbooks.OpenAsync(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Excel-To-JSON";
  savePicker.FileTypeChoices.Add("JSON Files", new List<string>() { ".json" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves the to worsheet to a JSON as specified storage file without schema
  await workbook.SaveAsJsonAsync(storageFile, worksheet, false);

  //Saves the worsheet to a JSON filestream without schema
  MemoryStream stream = new MemoryStream();
  workbook.Version = ExcelVersion.Xlsx;
  await workbook.SaveAsJsonAsync(stream, worksheet, false);
  Save(stream, "Excel-Worksheet-To-JSON-filestream-without-schema.json");

  stream.Dispose();
}

//Save the worksheet stream as a file.

#region Setting output location
async void Save(Stream stream, string filename)
{
  stream.Position = 0;

  StorageFile stFile;
  if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
  {
    FileSavePicker savePicker = new FileSavePicker();
    savePicker.DefaultFileExtension = ".json";
    savePicker.SuggestedFileName = filename;
    savePicker.FileTypeChoices.Add("JSON Files", new List<string>() { ".json" });
    stFile = await savePicker.PickSaveFileAsync();
  }
  else
  {
    StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
    stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
  }
  if (stFile != null)
  {
    Windows.Storage.Streams.IRandomAccessStream fileStream = await stFile.OpenAsync(FileAccessMode.ReadWrite);
    Stream st = fileStream.AsStreamForWrite();
    st.Write((stream as MemoryStream).ToArray(), 0, (int)stream.Length);
    st.Flush();
    st.Dispose();
    fileStream.Dispose();
  }
}
#endregion
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion =ExcelVersion.Xlsx;
  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Saves the worksheet to a JSON filestream without schema
  FileStream stream = new FileStream("Excel-Worksheet-To-JSON-filestream-without-schema.json", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAsJson(stream, worksheet, false);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Saves the worksheet to a JSON filestream without schema
  MemoryStream outputStream = new MemoryStream();
  workbook.SaveAsJson(outputStream, worksheet, false);

  //Save the stream as JSON document and view the saved document    
  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.
  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Excel-Worksheet-To-JSON-filestream-without-schema.json", "application/notepad", outputStream);
  }
  else
  {
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Excel-Worksheet-To-JSON-filestream-without-schema.json", "application/notepad", outputStream);
  }

  //Dispose the input and output stream instances
  inputStream.Dispose();
  outputStream.Dispose();
}
{% endhighlight %}
{% endtabs %}

A complete working example to convert Excel worksheet to JSON without schema in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Convert%20Excel%20to%20JSON/Worksheet%20to%20JSON%20without%20Schema). 

## Range to JSON as schema

The following code illustrates how to convert an Excel Custom Range to the JSON file or file stream as schema.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

  //Active worksheet
  IWorksheet worksheet = workbook.Worksheets[0];

  //Custom range
  IRange range = worksheet.Range["A2:A5"];

  //Saves the range to a JSON file, as schema by default
  workbook.SaveAsJson("Excel-Range-To-JSON-as-schema-default.json", range);

  //Saves the range to a JSON file as schema
  workbook.SaveAsJson("Excel-Range-To-JSON-as-schema.json", range, true);

  //Saves the range to a JSON filestream, as schema by default
  FileStream stream = new FileStream("Excel-Range-To-JSON-filestream-as-schema-default.json", FileMode.Create);
  workbook.SaveAsJson(stream, range);

  //Saves the range to a JSON filestream as schema
  FileStream stream1 = new FileStream("Excel-Range-To-JSON-filestream-as-schema.json", FileMode.Create);
  workbook.SaveAsJson(stream1, range, true);
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

  'Active worksheet
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Custom range
  Dim range As IRange = worksheet.Range("A2:A5")

  'Saves the range to a JSON file, as schema by default
  workbook.SaveAsJson("Excel-Range-To-JSON-as-schema-default.json", range)

  'Saves the range to a JSON file as schema
  workbook.SaveAsJson("Excel-Range-To-JSON-as-schema.json", range, true)

  'Saves the range to a JSON filestream, as schema by default
  Dim stream As FileStream = new FileStream("Excel-Range-To-JSON-filestream-as-schema-default.json", FileMode.Create)
  workbook.SaveAsJson(stream, range)

  'Saves the range to a JSON filestream as schema
  Dim stream1 As FileStream = new FileStream("Excel-Range-To-JSON-filestream-as-schema.json", FileMode.Create)
  workbook.SaveAsJson(stream1, range, true)
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Sample.xlsx");
  IWorkbook workbook = await excelEngine.Excel.Workbooks.OpenAsync(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Custom range
  IRange range = worksheet.Range["A2:A5"];

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Excel-To-JSON-as-schema-default";
  savePicker.FileTypeChoices.Add("JSON Files", new List<string>() { ".json" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves the Range to a JSON as specified storage file, as schema by default
  await workbook.SaveAsJsonAsync(storageFile, range);

  //Saves the Range to a JSON filestream, as schema by default
  MemoryStream stream = new MemoryStream();
  workbook.Version = ExcelVersion.Xlsx;
  await workbook.SaveAsJsonAsync(stream, range);
  Save(stream, "Excel-Range-To-JSON-filestream-as-schema-default.json");
}

//Save the Range stream as a file.

#region Setting output location
async void Save(Stream stream, string filename)
{
  stream.Position = 0;

  StorageFile stFile;
  if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
  {
    FileSavePicker savePicker = new FileSavePicker();
    savePicker.DefaultFileExtension = ".json";
    savePicker.SuggestedFileName = filename;
    savePicker.FileTypeChoices.Add("JSON Files", new List<string>() { ".json" });
    stFile = await savePicker.PickSaveFileAsync();
  }
  else
  {
    StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
    stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
  }
  if (stFile != null)
  {
    Windows.Storage.Streams.IRandomAccessStream fileStream = await stFile.OpenAsync(FileAccessMode.ReadWrite);
    Stream st = fileStream.AsStreamForWrite();
    st.Write((stream as MemoryStream).ToArray(), 0, (int)stream.Length);
    st.Flush();
    st.Dispose();
    fileStream.Dispose();
  }
}
#endregion
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Custom range
  IRange range = worksheet.Range["A2:A5"];

  //Saves the Range to a JSON filestream, as schema by default
  FileStream stream = new FileStream("Excel-Range-To-JSON-as-schema-default.json", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAsJson(stream, range);

  //Saves the Range to a JSON filestream as schema
  FileStream stream = new FileStream("Excel-Range-To-JSON-as-schema.json", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAsJson(stream, range, true);

  stream.Dispose();
  stream1.Dispose();
}
{% endhighlight %}
{% highlight c# tabtitle="Xamarin" %}
using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Sample.xlsx");  
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Custom range
  IRange range = worksheet.Range["A2:A5"];

  //Saves the Range to a JSON filestream, as schema by default
  MemoryStream outputStream = new MemoryStream();
  workbook.SaveAsJson(outputStream, range);

  //Save the stream as JSON document and view the saved document    
  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.
  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Excel-Range-To-JSON-filestream-as-schema-default.json", "application/notepad", outputStream);
  }
  else
  {
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Excel-Range-To-JSON-filestream-as-schema-default.json", "application/notepad", outputStream);
  }

  //Dispose the input and output stream instances
  inputStream.Dispose();
  outputStream.Dispose();
}
{% endhighlight %}
{% endtabs %}

A complete working example to convert range to JSON with schema in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Convert%20Excel%20to%20JSON/Range%20to%20JSON%20with%20Schema). 

## Range to JSON without schema

The following code illustrates how to convert an Excel Custom Range to the JSON file or JSON file stream without schema.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

  //Active worksheet
  IWorksheet worksheet = workbook.Worksheets[0];

  //Custom range
  IRange range = worksheet.Range["A2:A5"];

  //Saves the range to a JSON file without schema
  workbook.SaveAsJson("Excel-Range-To-JSON-without-schema.json", range, false);

  //Saves the range to a JSON filestream without schema
  FileStream stream = new FileStream("Excel-Range-To-JSON-filestream-without-schema.json", FileMode.Create);
  workbook.SaveAsJson(stream, range, false);
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

  'Active worksheet
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Custom range
  Dim range As IRange = worksheet.Range("A2:A5")

  'Saves the range to a JSON file without schema
  workbook.SaveAsJson("Excel-Range-To-JSON-without-schema.json", range, false)

  'Saves the range to a JSON filestream without schema
  Dim stream As FileStream = new FileStream("Excel-Range-To-JSON-filestream-without-schema.json", FileMode.Create)
  workbook.SaveAsJson(stream, range, false)
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Sample.xlsx");
  IWorkbook workbook = await excelEngine.Excel.Workbooks.OpenAsync(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Custom range
  IRange range = worksheet.Range["A2:A5"];

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Excel-To-JSON-without-schema";
  savePicker.FileTypeChoices.Add("JSON Files", new List<string>() { ".json" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves the Range to a JSON as specified storage file without schema
  await workbook.SaveAsJsonAsync(storageFile, range, false);

  //Saves the Range to a JSON filestream without schema
  MemoryStream stream = new MemoryStream();
  workbook.Version = ExcelVersion.Xlsx;
  await workbook.SaveAsJsonAsync(stream, range, false);
  Save(stream, "Excel-Range-To-JSON-filestream-without-schema.json");
}

//Save the Range stream as a file.

#region Setting output location
async void Save(Stream stream, string filename)
{
  stream.Position = 0;

  StorageFile stFile;
  if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
  {
    FileSavePicker savePicker = new FileSavePicker();
    savePicker.DefaultFileExtension = ".json";
    savePicker.SuggestedFileName = filename;
    savePicker.FileTypeChoices.Add("JSON Files", new List<string>() { ".json" });
    stFile = await savePicker.PickSaveFileAsync();
  }
  else
  {
    StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
    stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
  }
  if (stFile != null)
  {
    Windows.Storage.Streams.IRandomAccessStream fileStream = await stFile.OpenAsync(FileAccessMode.ReadWrite);
    Stream st = fileStream.AsStreamForWrite();
    st.Write((stream as MemoryStream).ToArray(), 0, (int)stream.Length);
    st.Flush();
    st.Dispose();
    fileStream.Dispose();
  }
}
#endregion
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Custom range
  IRange range = worksheet.Range["A2:A5"];

  //Saves the Range to a JSON filestream without schema
  FileStream stream = new FileStream("Excel-Range-To-JSON-filestream-without-schema.json", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAsJson(stream, range, false);
  stream.Dispose();
}
{% endhighlight %}
{% highlight c# tabtitle="Xamarin" %}
using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Custom range
  IRange range = worksheet.Range["A2:A5"];

  //Saves the Range to a JSON filestream without schema
  MemoryStream outputStream = new MemoryStream();
  workbook.SaveAsJson(outputStream, range, false);

  //Save the stream as JSON document and view the saved document    
  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.
  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Excel-Range-To-JSON-filestream-without-schema.json", "application/notepad", outputStream);
  }
  else
  {
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Excel-Range-To-JSON-filestream-without-schema.json", "application/notepad", outputStream);
  }

  //Dispose the input and output stream instances
  inputStream.Dispose();
  outputStream.Dispose();
}
{% endhighlight %}
{% endtabs %}

A complete working example to convert range to JSON without schema in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Convert%20Excel%20to%20JSON/Range%20to%20JSON%20without%20Schema). 
