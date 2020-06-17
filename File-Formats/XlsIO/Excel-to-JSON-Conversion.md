---
title: Syncfusion Excel to JSON Conversion
description: In this section, you can learn how to Export Excel Data as JSON
platform: File-formats
control: XlsIO
documentation: UG
---

# Excel to JSON Conversion

Essential XlsIO supports converting Excel data as JSON files by simply saving the workbook using the `SaveAsJson` method. This is support includes the featrues to save.

* a workbook as a simple JSON file or JSON file with XML schema
* a workbook to JSON
* a worksheet to JSON
* a range to JSON
* a stream with above feature

## Workbook to JSON

The following code illustrates how to convert an Excel workbook to JSON file.

{% tabs %}  

{% highlight c# %}
using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);
  
  //Saves the workbook to a JSON file
  workbook.SaveAsJson("Excel-To-JSON.json");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Excel2013
    Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)
	
	'Saves the workbook to a JSON file
    workbook.SaveAsJson("Excel-To-JSON.json")
End Using
{% endhighlight %}
{% highlight UWP %}
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

  //Saves changes to the specified storage file
  await workbook.SaveAsJsonAsync(storageFile);
}

{% endhighlight %}
{% highlight asp.net core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;

  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);

  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Saves the workbook to a JSON file
  FileStream stream = new FileStream("Excel-To-JSON.json", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAsJson(stream);
  stream.Dispose();
}
{% endhighlight %}
{% highlight Xamarin %}
using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  
  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
             
  //Gets input Excel document from embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Sample.xlsx");
  
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Saving the workbook as JSON file stream
  MemoryStream outputStream = new MemoryStream();
  workbook.SaveAsJson(outputStream);

  //Save the stream as JSON document and view the saved document  
  
  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.
  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
      await DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Excel-To-JSON.json", "application/notepad", outputStream);
  else
      DependencyService.Get<ISave>().SaveAndView("Excel-To-JSON.json", "application/notepad", outputStream);

  //Dispose the input and output stream instances
  inputStream.Dispose();
  outputStream.Dispose();
}

{% endhighlight %}
{% endtabs %}

## Workbook to JSON with and without XML schema

The following code illustrates how to convert an Excel workbook to JSON file with and without XML schema.

{% tabs %}  

{% highlight c# %}
using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);
  
  //Saves the workbook to a JSON file with schema
  workbook.SaveAsJson("Excel-To-JSON-with-schema.json", true);

  //Saves the workbook to a JSON file without schema
  workbook.SaveAsJson("Excel-To-JSON-without-schema.json", false);
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Excel2013
    Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

	'Saves the workbook to a JSON file with schema
    workbook.SaveAsJson("Excel-To-JSON-with-schema.json", true);

	'Saves the workbook to a JSON file without schema
    workbook.SaveAsJson("Excel-To-JSON-without-schema.json", false);
End Using
{% endhighlight %}
{% highlight UWP %}
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

  //Saves changes to the specified storage file
  await workbook.SaveAsJsonAsync(storageFile, true);
}

{% endhighlight %}
{% highlight asp.net core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;

  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);

  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Saves the workbook to a JSON file
  FileStream stream = new FileStream("Excel-To-JSON.json", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAsJson(stream, true);
  stream.Dispose();
}
{% endhighlight %}
{% highlight Xamarin %}
using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  
  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
             
  //Gets input Excel document from embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Sample.xlsx");
  
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Saving the workbook as JSON file stream
  MemoryStream outputStream = new MemoryStream();
  workbook.SaveAsJson(outputStream, true);

  //Save the stream as JSON document and view the saved document  
  
  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.
  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
      await DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Excel-To-JSON.json", "application/notepad", outputStream);
  else
      DependencyService.Get<ISave>().SaveAndView("Excel-To-JSON.json", "application/notepad", outputStream);

  //Dispose the input and output stream instances
  inputStream.Dispose();
  outputStream.Dispose();
}

{% endhighlight %}
{% endtabs %}

## Worksheet to JSON

The following code illustrates how to convert an Excel worksheet to JSON file.

{% tabs %}  

{% highlight c# %}
using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

  //Active worksheet
  IWorksheet worksheet = workbook.Worksheets[0];

  //Saves the worksheet to a JSON file
  workbook.SaveAsJson("Excel-To-JSON.json", worksheet);
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Excel2013
    Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

	'Active worksheet
	Dim worksheet As IWorksheet = workbook.Worksheets(0)

	'Saves the worksheet to a JSON file
    workbook.SaveAsJson("Excel-To-JSON.json", worksheet)
End Using
{% endhighlight %}
{% highlight UWP %}
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

  //Saves changes to the specified storage file
  await workbook.SaveAsJsonAsync(storageFile, worksheet);
}

{% endhighlight %}
{% highlight asp.net core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;

  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);

  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Saves the worksheet to a JSON file
  FileStream stream = new FileStream("Excel-To-JSON.json", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAsJson(stream, worksheet);
  stream.Dispose();
}
{% endhighlight %}
{% highlight Xamarin %}
using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  
  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
             
  //Gets input Excel document from embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Sample.xlsx");
  
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Saving the worksheet as JSON file stream
  MemoryStream outputStream = new MemoryStream();
  workbook.SaveAsJson(outputStream, worksheet);

  //Save the stream as JSON document and view the saved document  
  
  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.
  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
      await DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Excel-To-JSON.json", "application/notepad", outputStream);
  else
      DependencyService.Get<ISave>().SaveAndView("Excel-To-JSON.json", "application/notepad", outputStream);

  //Dispose the input and output stream instances
  inputStream.Dispose();
  outputStream.Dispose();
}

{% endhighlight %}
{% endtabs %}

## Worksheet to JSON with and without XML schema

The following code illustrates how to convert an Excel worksheet to JSON file with and without XML schema.

{% tabs %}  

{% highlight c# %}
using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

  //Active worksheet
  IWorksheet worksheet = workbook.Worksheets[0];

  //Saves the worksheet to a JSON file with schema
  workbook.SaveAsJson("Excel-To-JSON-with-schema", worksheet, true);

  //Saves the worksheet to a JSON file without schema
  workbook.SaveAsJson("Excel-To-JSON-without-schema.json", worksheet, false);
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Excel2013
    Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

	'Active worksheet
	Dim worksheet As IWorksheet = workbook.Worksheets(0)

	'Saves the worksheet to a JSON file with schema
    workbook.SaveAsJson("Excel-To-JSON-with-schema", worksheet, true);

	'Saves the worksheet to a JSON file without schema
    workbook.SaveAsJson("Excel-To-JSON-without-schema.json", worksheet, false);
End Using
{% endhighlight %}
{% highlight UWP %}
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

  //Saves changes to the specified storage file
  await workbook.SaveAsJsonAsync(storageFile, worksheet, true);
}

{% endhighlight %}
{% highlight asp.net core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;

  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);

  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Saves the worksheet to a JSON file
  FileStream stream = new FileStream("Excel-To-JSON.json", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAsJson(stream, worksheet, true);
  stream.Dispose();
}
{% endhighlight %}
{% highlight Xamarin %}
using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  
  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
             
  //Gets input Excel document from embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Sample.xlsx");
  
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Saving the worksheet as JSON file stream
  MemoryStream outputStream = new MemoryStream();
  workbook.SaveAsJson(outputStream, worksheet, true);

  //Save the stream as JSON document and view the saved document  
  
  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.
  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
      await DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Excel-To-JSON.json", "application/notepad", outputStream);
  else
      DependencyService.Get<ISave>().SaveAndView("Excel-To-JSON.json", "application/notepad", outputStream);

  //Dispose the input and output stream instances
  inputStream.Dispose();
  outputStream.Dispose();
}

{% endhighlight %}
{% endtabs %}

## Range to JSON

The following code illustrates how to convert an Excel Custom Range to JSON file.

{% tabs %}  

{% highlight c# %}
using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

  //Active worksheet
  IWorksheet worksheet = workbook.Worksheets[0];

  //Custom range
  IRange range = worksheet.Range["A1:D5"];

  //Saves the range to a JSON file
  workbook.SaveAsJson("Excel-To-JSON.json", range);
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Excel2013
    Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)
	
	'Active worksheet
	Dim worksheet As IWorksheet = workbook.Worksheets(0)

	'Custom range
	IRange range = worksheet.Range("A1:D5")

	'Saves the range to a JSON file
    workbook.SaveAsJson("Excel-To-JSON.json", range)
End Using
{% endhighlight %}
{% highlight UWP %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Sample.xlsx");

  IWorkbook workbook = await excelEngine.Excel.Workbooks.OpenAsync(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];
  //Custom range
  IRange range = worksheet.Range["A1:D5"];

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Excel-To-JSON";
  savePicker.FileTypeChoices.Add("JSON Files", new List<string>() { ".json" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  await workbook.SaveAsJsonAsync(storageFile, range);
}

{% endhighlight %}
{% highlight asp.net core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;

  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);

  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Custom range
  IRange range = worksheet.Range["A1:D5"];

  //Saves the Range to a JSON file
  FileStream stream = new FileStream("Excel-To-JSON.json", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAsJson(stream, range);
  stream.Dispose();
}
{% endhighlight %}
{% highlight Xamarin %}
using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  
  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
             
  //Gets input Excel document from embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Sample.xlsx");
  
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];
  //Custom range
  IRange range = worksheet.Range["A1:D5"];

  //Saving the Range as JSON file stream
  MemoryStream outputStream = new MemoryStream();
  workbook.SaveAsJson(outputStream, range);

  //Save the stream as JSON document and view the saved document  
  
  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.
  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
      await DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Excel-To-JSON.json", "application/notepad", outputStream);
  else
      DependencyService.Get<ISave>().SaveAndView("Excel-To-JSON.json", "application/notepad", outputStream);

  //Dispose the input and output stream instances
  inputStream.Dispose();
  outputStream.Dispose();
}

{% endhighlight %}
{% endtabs %}

## Range to JSON with and without XML schema

The following code illustrates how to convert an Excel Custom Range to JSON file.

{% tabs %}  

{% highlight c# %}
using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

  //Active worksheet
  IWorksheet worksheet = workbook.Worksheets[0];

  //Custom range
  IRange range = worksheet.Range["A1:D5"];

  //Saves the range to a JSON file with schema
  workbook.SaveAsJson("Excel-To-JSON-with-schema.json", range, true);

  //Saves the range to a JSON file without schema
  workbook.SaveAsJson("Excel-To-JSON-without-schema.json", range, false);
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Excel2013
    Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)
	
	'Active worksheet
	Dim worksheet As IWorksheet = workbook.Worksheets(0)

	'Custom range
	IRange range = worksheet.Range("A1:D5")

	'Saves the range to a JSON file with schema
    workbook.SaveAsJson("Excel-To-JSON-with-schema.json", range, true)

	'Saves the range to a JSON file without schema
    workbook.SaveAsJson("Excel-To-JSON-without-schema.json", range, false)
End Using
{% endhighlight %}
{% highlight UWP %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Sample.xlsx");

  IWorkbook workbook = await excelEngine.Excel.Workbooks.OpenAsync(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];
  //Custom range
  IRange range = worksheet.Range["A1:D5"];

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Excel-To-JSON";
  savePicker.FileTypeChoices.Add("JSON Files", new List<string>() { ".json" });

  //Creates a storage file from FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Saves changes to the specified storage file
  await workbook.SaveAsJsonAsync(storageFile, range, true);
}

{% endhighlight %}
{% highlight asp.net core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;

  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);

  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Custom range
  IRange range = worksheet.Range["A1:D5"];

  //Saves the Range to a JSON file
  FileStream stream = new FileStream("Excel-To-JSON.json", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAsJson(stream, range, true);
  stream.Dispose();
}
{% endhighlight %}
{% highlight Xamarin %}
using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  
  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
             
  //Gets input Excel document from embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Sample.xlsx");
  
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];
  //Custom range
  IRange range = worksheet.Range["A1:D5"];

  //Saving the Range as JSON file stream
  MemoryStream outputStream = new MemoryStream();
  workbook.SaveAsJson(outputStream, range, true);

  //Save the stream as JSON document and view the saved document  
  
  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.
  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
      await DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Excel-To-JSON.json", "application/notepad", outputStream);
  else
      DependencyService.Get<ISave>().SaveAndView("Excel-To-JSON.json", "application/notepad", outputStream);

  //Dispose the input and output stream instances
  inputStream.Dispose();
  outputStream.Dispose();
}

{% endhighlight %}
{% endtabs %}

## Workbook to JSON file Stream

The following code illustrates how to convert an Excel workbook to JSON file stream.

{% tabs %}  

{% highlight c# %}
using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);
  //Stream
  Stream stream = new FileStream("Excel-To-JSON.json",filemode.create);

  //Saves the workbook to a JSON file stream
  workbook.SaveAsJson(stream);
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Excel2013
    Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)
	'Stream
	Dim stream As Stream = new FileStream("Excel-To-JSON.json",filemode.create)

	'Saves the workbook to a JSON file stream
    workbook.SaveAsJson(stream)
End Using
{% endhighlight %}
{% highlight UWP %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    
    //Gets assembly
    Assembly assembly = typeof(App).GetTypeInfo().Assembly;

    //Gets input Excel document from an embedded resource collection
    Stream excelStream = assembly.GetManifestResourceStream("Sample.xlsx");
	
    IWorkbook workbook = await application.Workbooks.OpenAsync(excelStream);

    //Save the JSON to stream.
    MemoryStream stream = new MemoryStream();

    await workbook.SaveASJsonAsync(stream);
    Save(stream, "ExcelToJSON.json");

    excelStream.Dispose();
    stream.Dispose();
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
        savePicker.SuggestedFileName = "ExcelToJSON";
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
{% highlight asp.net core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;

  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);

  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Saves the workbook to a JSON file
  FileStream stream = new FileStream("Excel-To-JSON.json", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAsJson(stream);
  stream.Dispose();
}
{% endhighlight %}
{% highlight Xamarin %}
using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  
  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
             
  //Gets input Excel document from embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Sample.xlsx");
  
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Saving the workbook as JSON file stream
  MemoryStream outputStream = new MemoryStream();
  workbook.SaveAsJson(outputStream);

  //Save the stream as JSON document and view the saved document  
  
  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.
  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
      await DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Excel-To-JSON.json", "application/notepad", outputStream);
  else
      DependencyService.Get<ISave>().SaveAndView("Excel-To-JSON.json", "application/notepad", outputStream);

  //Dispose the input and output stream instances
  inputStream.Dispose();
  outputStream.Dispose();
}

{% endhighlight %}
{% endtabs %}

## Workbook to JSON file Stream with and without XML schema

The following code illustrates how to convert an Excel workbook to JSON file stream with and without XML schema.

{% tabs %}  

{% highlight c# %}
using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);
  //Stream1
  Stream stream1 = new FileStream("Excel-To-JSON_IsSchema_True.json",filemode.create);
  
  //Saves the workbook to a JSON file stream with schema
  workbook.SaveAsJson(stream1, true);
  //Stream2
  Stream stream2 = new FileStream("Excel-To-JSON_IsSchema_True.json",filemode.create);

  //Saves the workbook to a JSON file stream without schema
  workbook.SaveAsJson(stream2, false);
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Excel2013
    Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)
	'Stream1
	Dim stream1 As Stream = new FileStream("Excel-To-JSON_IsSchema_True.json",filemode.create)

	'Saves the workbook to JSON file stream with schema
    workbook.SaveAsJson(stream1, true);
	'Stream2
	Dim stream2 As Stream = new FileStream("Excel-To-JSON_IsSchema_False.json",filemode.create)

	'Saves the workbook to JSON file stream without schema
    workbook.SaveAsJson(stream2, false);
End Using
{% endhighlight %}
{% highlight UWP %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    
    //Gets assembly
    Assembly assembly = typeof(App).GetTypeInfo().Assembly;

    //Gets input Excel document from an embedded resource collection
    Stream excelStream = assembly.GetManifestResourceStream("Sample.xlsx");
	
    IWorkbook workbook = await application.Workbooks.OpenAsync(excelStream);

    //Save the JSON to stream.
    MemoryStream stream = new MemoryStream();

    await workbook.SaveASJsonAsync(stream, true);
    Save(stream, "ExcelToJSON.json");

    excelStream.Dispose();
    stream.Dispose();
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
        savePicker.SuggestedFileName = "ExcelToJSON";
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
{% highlight asp.net core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;

  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);

  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Saves the workbook to a JSON file
  FileStream stream = new FileStream("Excel-To-JSON.json", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAsJson(stream, true);
  stream.Dispose();
}
{% endhighlight %}
{% highlight Xamarin %}
using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  
  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
             
  //Gets input Excel document from embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Sample.xlsx");
  
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Saving the workbook as JSON file stream
  MemoryStream outputStream = new MemoryStream();
  workbook.SaveAsJson(outputStream, true);

  //Save the stream as JSON document and view the saved document  
  
  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.
  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
      await DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Excel-To-JSON.json", "application/notepad", outputStream);
  else
      DependencyService.Get<ISave>().SaveAndView("Excel-To-JSON.json", "application/notepad", outputStream);

  //Dispose the input and output stream instances
  inputStream.Dispose();
  outputStream.Dispose();
}

{% endhighlight %}
{% endtabs %}

## Worksheet to JSON file Stream

The following code illustrates how to convert an Excel worksheet to JSON file stream.

{% tabs %}  

{% highlight c# %}
using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

  //Active worksheet
  IWorksheet worksheet = workbook.Worksheets[0];
  //Stream
  Stream stream = new FileStream("Excel-To-JSON.json", FileMode.Create);

  //Saves the worksheet to a JSON file stream
  workbook.SaveAsJson(stream, worksheet);
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Excel2013
    Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

	'Active worksheet
	Dim worksheet As IWorksheet = workbook.Worksheets(0)
	'Stream
	Dim stream As Stream = new FileStream("Excel-To-JSON.json", FileStream.Create)

	'Saves the worksheet to a JSON file stream
    workbook.SaveAsJson(stream, worksheet)
End Using
{% endhighlight %}
{% highlight UWP %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    
    //Gets assembly
    Assembly assembly = typeof(App).GetTypeInfo().Assembly;

    //Gets input Excel document from an embedded resource collection
    Stream excelStream = assembly.GetManifestResourceStream("Sample.xlsx");
	
    IWorkbook workbook = await application.Workbooks.OpenAsync(excelStream);

	IWorksheet worksheet = workbook.Worksheets[0];

    //Save the JSON to stream.
    MemoryStream stream = new MemoryStream();

    await workbook.SaveASJsonAsync(stream, worksheet);
    Save(stream, "ExcelToJSON.json");

    excelStream.Dispose();
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
        savePicker.SuggestedFileName = "ExcelToJSON";
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
{% highlight asp.net core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;

  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);

  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Saves the worksheet to a JSON file
  FileStream stream = new FileStream("Excel-To-JSON.json", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAsJson(stream, worksheet);
  stream.Dispose();
}
{% endhighlight %}
{% highlight Xamarin %}
using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  
  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
             
  //Gets input Excel document from embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Sample.xlsx");
  
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Saving the worksheet as JSON file stream
  MemoryStream outputStream = new MemoryStream();
  workbook.SaveAsJson(outputStream, worksheet);

  //Save the stream as JSON document and view the saved document  
  
  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.
  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
      await DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Excel-To-JSON.json", "application/notepad", outputStream);
  else
      DependencyService.Get<ISave>().SaveAndView("Excel-To-JSON.json", "application/notepad", outputStream);

  //Dispose the input and output stream instances
  inputStream.Dispose();
  outputStream.Dispose();
}

{% endhighlight %}
{% endtabs %}

## Worksheet to JSON file Stream with and without XML schema

The following code illustrates how to convert an Excel worksheet to JSON file Stream with and without XML schema.

{% tabs %}  

{% highlight c# %}
using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

  //Active worksheet
  IWorksheet worksheet = workbook.Worksheets[0];

  //Stream1
  Stream stream1 = new FileMode("Excel-To-JSON_IsSchema_True.json", FileMode.Create);

  //Saves the worksheet to a JSON file stream with schema
  workbook.SaveAsJson(stream1, worksheet, true);

  //Stream2
  Stream stream2 = new FileMode("Excel-To-JSON_IsSchema_False.json", FileMode.Create);

  //Saves the worksheet to a JSON file stream without schema
  workbook.SaveAsJson(stream2, worksheet, false);
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Excel2013
    Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

	'Active worksheet
	Dim worksheet As IWorksheet = workbook.Worksheets(0)
	'Stream1
	Dim stream1 As Stream = new FileStream("Excel-To-JSON_IsSchema_True.json", FileMode.Create)

	'Saves the worksheet to a JSON file Stream with schema
    workbook.SaveAsJson(stream1, worksheet, true);

	'Stream2
	Dim stream2 As Stream = new FileStream("Excel-To-JSON_IsSchema_False.json", FileMode.Create)

	'Saves the worksheet to a JSON file Stream without schema
    workbook.SaveAsJson(stream2, worksheet, false);
End Using
{% endhighlight %}
{% highlight UWP %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    
    //Gets assembly
    Assembly assembly = typeof(App).GetTypeInfo().Assembly;

    //Gets input Excel document from an embedded resource collection
    Stream excelStream = assembly.GetManifestResourceStream("Sample.xlsx");
	
    IWorkbook workbook = await application.Workbooks.OpenAsync(excelStream);

	IWorksheet worksheet = workbook.Worksheets[0];

    //Save the JSON to stream.
    MemoryStream stream = new MemoryStream();

    await workbook.SaveASJsonAsync(stream, worksheet, true);
    Save(stream, "ExcelToJSON.json");

    excelStream.Dispose();
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
        savePicker.SuggestedFileName = "ExcelToJSON";
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
{% highlight Xamarin %}
using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  
  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
             
  //Gets input Excel document from embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Sample.xlsx");
  
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Saving the worksheet as JSON file stream
  MemoryStream outputStream = new MemoryStream();
  workbook.SaveAsJson(outputStream, worksheet, true);

  //Save the stream as JSON document and view the saved document  
  
  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.
  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
      await DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Excel-To-JSON.json", "application/notepad", outputStream);
  else
      DependencyService.Get<ISave>().SaveAndView("Excel-To-JSON.json", "application/notepad", outputStream);

  //Dispose the input and output stream instances
  inputStream.Dispose();
  outputStream.Dispose();
}

{% endhighlight %}
{% endtabs %}

## Range to JSON file Stream

The following code illustrates how to convert an Excel Custom Range to JSON file stream.

{% tabs %}  

{% highlight c# %}
using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

  //Active worksheet
  IWorksheet worksheet = workbook.Worksheets[0];

  //Custom range
  IRange range = worksheet.Range["A1:D5"];
  //Stream
  Stream stream = new FileStream("Excel-To-JSON.json", FileMode.Create);

  //Saves the range to a JSON file stream
  workbook.SaveAsJson(stream, range);
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Excel2013
    Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)
	
	'Active worksheet
	Dim worksheet As IWorksheet = workbook.Worksheets(0)

	'Custom range
	Dim range As IRange  = worksheet.Range("A1:D5")
	'Stream
	Dim stream As Stream = new FileStream("Excel-To-JSON.json",FileMode.Create)

	'Saves the range to a JSON file stream
    workbook.SaveAsJson(stream, worksheet)
End Using
{% endhighlight %}
{% highlight UWP %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    
    //Gets assembly
    Assembly assembly = typeof(App).GetTypeInfo().Assembly;

    //Gets input Excel document from an embedded resource collection
    Stream excelStream = assembly.GetManifestResourceStream("Sample.xlsx");
	
    IWorkbook workbook = await application.Workbooks.OpenAsync(excelStream);

	IWorksheet worksheet = workbook.Worksheets[0];
	
	IRange range = worksheet.Range["A1:D5"];

    //Save the JSON to stream.
    MemoryStream stream = new MemoryStream();

    await workbook.SaveASJsonAsync(stream, range);
    Save(stream, "ExcelToJSON.json");

    excelStream.Dispose();
    stream.Dispose();
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
        savePicker.SuggestedFileName = "ExcelToJSON";
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
{% highlight asp.net core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;

  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);

  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Custom range
  IRange range = worksheet.Range["A1:D5"];

  //Saves the Range to a JSON file
  FileStream stream = new FileStream("Excel-To-JSON.json", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAsJson(stream, range);
  stream.Dispose();
}
{% endhighlight %}
{% highlight Xamarin %}
using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  
  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
             
  //Gets input Excel document from embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Sample.xlsx");
  
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];
  //Custom range
  IRange range = worksheet.Range["A1:D5"];

  //Saving the Range as JSON file stream
  MemoryStream outputStream = new MemoryStream();
  workbook.SaveAsJson(outputStream, range);

  //Save the stream as JSON document and view the saved document  
  
  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.
  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
      await DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Excel-To-JSON.json", "application/notepad", outputStream);
  else
      DependencyService.Get<ISave>().SaveAndView("Excel-To-JSON.json", "application/notepad", outputStream);

  //Dispose the input and output stream instances
  inputStream.Dispose();
  outputStream.Dispose();
}

{% endhighlight %}
{% endtabs %}

## Range to JSON file Stream with and without XML schema

The following code illustrates how to convert an Excel Custom Range to JSON file Stream.

{% tabs %}  

{% highlight c# %}
using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

  //Active worksheet
  IWorksheet worksheet = workbook.Worksheets[0];

  //Custom range
  IRange range = worksheet.Range["A1:D5"];
   //Stream1
  Stream stream1 = new FileStream("Excel-To-JSON_IsSchema_True.json", FileMode.Create)

  //Saves the range to a JSON file stream with schema
  workbook.SaveAsJson(stream1, range, true);
  //Stream2
  Stream stream2 = new FileStream("Excel-To-JSON_IsSchema_False.json", FileMode.Create);

  //Saves the range to a JSON file stream without schema
  workbook.SaveAsJson(stream2, range, false);
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Excel2013
    Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)
	
	'Active worksheet
	Dim worksheet As IWorksheet = workbook.Worksheets(0)

	'Custom range
	Dim range As IRange = worksheet.Range("A1:D5")
	'Stream1
	Dim stream1 As Stream  = new FileStream("Excel-To-JSON_IsSchema_True.json",FileMode.Create)

	'Saves the range to a JSON file stream with schema
    workbook.SaveAsJson(stream1, worksheet, true)

	'Stream2
	Dim stream2 As Stream  = new FileStream("Excel-To-JSON_IsSchema_False.json",FileMode.Create)

	'Saves the range to a JSON file stream without schema
    workbook.SaveAsJson(stream2, worksheet, false)
End Using
{% endhighlight %}
{% highlight UWP %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    
    //Gets assembly
    Assembly assembly = typeof(App).GetTypeInfo().Assembly;

    //Gets input Excel document from an embedded resource collection
    Stream excelStream = assembly.GetManifestResourceStream("Sample.xlsx");
	
    IWorkbook workbook = await application.Workbooks.OpenAsync(excelStream);

	IWorksheet worksheet = workbook.Worksheets[0];
	
	IRange range = worksheet.Range["A1:D5"];

    //Save the JSON to stream.
    MemoryStream stream = new MemoryStream();

    await workbook.SaveASJsonAsync(stream, range, true);
    Save(stream, "ExcelToJSON.json");

    excelStream.Dispose();
    stream.Dispose();
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
        savePicker.SuggestedFileName = "ExcelToJSON";
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
{% highlight asp.net core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;

  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);

  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Custom range
  IRange range = worksheet.Range["A1:D5"];

  //Saves the Range to a JSON file
  FileStream stream = new FileStream("Excel-To-JSON.json", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAsJson(stream, range, true);
  stream.Dispose();
}
{% endhighlight %}
{% highlight Xamarin %}
using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  
  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
             
  //Gets input Excel document from embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("Sample.xlsx");
  
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];
  //Custom range
  IRange range = worksheet.Range["A1:D5"];

  //Saving the Range as JSON file stream
  MemoryStream outputStream = new MemoryStream();
  workbook.SaveAsJson(outputStream, range, true);

  //Save the stream as JSON document and view the saved document  
  
  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.
  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
      await DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Excel-To-JSON.json", "application/notepad", outputStream);
  else
      DependencyService.Get<ISave>().SaveAndView("Excel-To-JSON.json", "application/notepad", outputStream);

  //Dispose the input and output stream instances
  inputStream.Dispose();
  outputStream.Dispose();
}

{% endhighlight %}

{% endtabs %}