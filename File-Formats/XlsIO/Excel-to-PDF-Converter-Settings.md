---
title: Syncfusion Excel to PDF Converter Settings
description: In this section, you can learn how to convert Excel Workbook to PDF & Worksheet to PDF file using conversion settings of Excel to PDF converter;
platform: File-formats
control: XlsIO
documentation: UG
---

# Excel to PDF Converter Settings

XlsIO allows you to convert an entire workbook or a single worksheet into PDF document with conversion settings of Excel to PDF converter.

## Auto Detect Complex Script

This property enables the complex script validation for the text present in Excel document and renders it into PDF document. It's default value is FALSE.

The following complete code snippet explains how to enable `AutoDetectComplexScript` property while converting an Excel document to PDF.

{% tabs %}
{% highlight C# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");

  //Initialize ExcelToPdfConverterSettings
  ExcelToPdfConverterSettings settings = new ExcelToPdfConverterSettings();

  //Enable AutoDetectComplexScript property
  settings.AutoDetectComplexScript = true;

  //Load the Excel document into ExcelToPdfConverter
  ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);

  //Convert the Excel document to PDF with converter settings
  PdfDocument document = converter.Convert(settings);

  //Save the PDF document
  document.Save("Output.pdf");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2016
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")

  'Initialize ExcelToPdfConverterSettings
  Dim settings As ExcelToPdfConverterSettings = New ExcelToPdfConverterSettings()

  'Enable AutoDetectComplexScript property
  settings.AutoDetectComplexScript = True

  'Load the Excel document into ExcelToPdfConverter
  Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(workbook)

  'Convert the Excel document to PDF with converter settings
  Dim document As PdfDocument = converter.Convert(settings)

  'Save the PDF document
  document.Save("Output.pdf")
End Using
{% endhighlight %}

{% highlight UWP %}
//Excel To PDF conversion can be performed by referring .NET Standard assemblies in UWP platform
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;

  //Get assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Get input Excel document from an embedded resource collection
  Stream excelStream = assembly.GetManifestResourceStream("UWPSample.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Enable AutoDetectComplexScript property
  settings.AutoDetectComplexScript = true;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook,settings);

  //Save the PDF document
  MemoryStream stream = new MemoryStream();
  document.Save(stream);
  Save(stream, "Output.pdf");

  excelStream.Dispose();
}

//Save the PDF stream as a file
#region Setting output location
async void Save(Stream stream, string filename)
{
  stream.Position = 0;

  StorageFile stFile;
  if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
  {
    FileSavePicker savePicker = new FileSavePicker();
    savePicker.DefaultFileExtension = ".pdf";
    savePicker.SuggestedFileName = "Output";
    savePicker.FileTypeChoices.Add("Adobe PDF Document", new List<string>() { ".pdf" });
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
  stream.Dispose();
}
#endregion
{% endhighlight %}

{% highlight ASP.NET Core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream excelStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Enable AutoDetectComplexScript property
  settings.AutoDetectComplexScript = true;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook, settings);

  //Download the PDF file in the browser
  FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");
  fileStreamResult.FileDownloadName = "Output.pdf";
  return fileStreamResult;
}
{% endhighlight %}

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from an embedded resource collection
  Stream excelStream = assembly.GetManifestResourceStream("XamarinSample.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Enable AutoDetectComplexScript property
  settings.AutoDetectComplexScript = true;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook, settings);

  //Save the PDF document to stream
  MemoryStream stream = new MemoryStream();
  document.Save(stream);
  stream.Position = 0;

  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.pdf", "application/pdf", stream);
}
{% endhighlight %}
{% endtabs%}

## Custom Paper Size

This property helps to set the required paper size in inches. The default value is empty(i.e.,{Width = 0.0 Height = 0.0}).

The following complete code snippet explains how to set `CustomPaperSize` while converting Excel document to PDF.
{% tabs %}
{% highlight C# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");

  //Initialize ExcelToPdfConverterSettings
  ExcelToPdfConverterSettings settings = new ExcelToPdfConverterSettings();

  //Set CustomerPaperSize
  settings.CustomPaperSize = new SizeF(10, 20);

  //Load the Excel document into ExcelToPdfConverter
  ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);

  //Convert the Excel document to PDF with converter settings
  PdfDocument document = converter.Convert(settings);

  //Save the PDF document
  document.Save("Output.pdf");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2016
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")

  'Initialize ExcelToPdfConverterSettings
  Dim settings As ExcelToPdfConverterSettings = New ExcelToPdfConverterSettings()

  'Set CustomerPaperSize
  settings.CustomPaperSize = New SizeF(10, 20)

  'Load the Excel document into ExcelToPdfConverter
  Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(workbook)

  'Convert the Excel document to PDF with converter settings
  Dim document As PdfDocument = converter.Convert(settings)

  'Save the PDF document
  document.Save("Output.pdf")
End Using
{% endhighlight %}

{% highlight UWP %}
//Excel To PDF conversion can be performed by referring .NET Standard assemblies in UWP platform
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;

  //Get assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Get input Excel document from an embedded resource collection
  Stream excelStream = assembly.GetManifestResourceStream("UWPSample.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Set CustomerPaperSize
  settings.CustomPaperSize = new SizeF(10, 20);

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook,settings);

  //Save the PDF document
  MemoryStream stream = new MemoryStream();
  document.Save(stream);
  Save(stream, "Output.pdf");

  excelStream.Dispose();
}

//Save the PDF stream as a file
#region Setting output location
async void Save(Stream stream, string filename)
{
  stream.Position = 0;

  StorageFile stFile;
  if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
  {
    FileSavePicker savePicker = new FileSavePicker();
    savePicker.DefaultFileExtension = ".pdf";
    savePicker.SuggestedFileName = "Output";
    savePicker.FileTypeChoices.Add("Adobe PDF Document", new List<string>() { ".pdf" });
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
  stream.Dispose();
}
#endregion
{% endhighlight %}

{% highlight ASP.NET Core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream excelStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Set CustomerPaperSize
  settings.CustomPaperSize = new SizeF(10, 20);

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook, settings);

  //Saving the Excel to the MemoryStream 
  MemoryStream stream = new MemoryStream();
  document.Save(stream);

  //Set the position as '0'
  stream.Position = 0;

  //Download the PDF file in the browser
  FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");
  fileStreamResult.FileDownloadName = "Output.pdf";
  return fileStreamResult;
}
{% endhighlight %}

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from an embedded resource collection
  Stream excelStream = assembly.GetManifestResourceStream("XamarinSample.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Set CustomerPaperSize
  settings.CustomPaperSize = new SizeF(10, 20);

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook, settings);

  //Save the PDF document to stream
  MemoryStream stream = new MemoryStream();
  document.Save(stream);
  stream.Position = 0;

  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.pdf", "application/pdf", stream);
}
{% endhighlight %}
{% endtabs %}

## Display Gridlines

This property helps to set the gridlines display style in Excel to PDF converted document. Three display styles are **Auto**, **Invisible** and **Visible**. These are maintained under ``GridLinesDisplayStyle`` enumeration.

### Auto

Gridlines will not be rendered in the output PDF document, when display style is selected as **Auto**. Its default value is Invisible. The following code snippet explains how to select **Auto** display style for gridlines.

{% tabs %}
{% highlight C# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");

  //Initialize ExcelToPdfConverterSettings
  ExcelToPdfConverterSettings settings = new ExcelToPdfConverterSettings();

  //Set the gridlines display style as Auto
  settings.DisplayGridLines = GridLinesDisplayStyle.Auto;

  //Load the Excel document into ExcelToPdfConverter
  ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);

  //Convert the Excel document to PDF with converter settings
  PdfDocument document = converter.Convert(settings);

  //Save the PDF document
  document.Save("Output.pdf");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2016
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")

  'Initialize ExcelToPdfConverterSettings
  Dim settings As ExcelToPdfConverterSettings = New ExcelToPdfConverterSettings()

  'Set the gridlines display style as Auto
  settings.DisplayGridLines = GridLinesDisplayStyle.Auto

  'Load the Excel document into ExcelToPdfConverter
  Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(workbook)

  'Convert the Excel document to PDF with converter settings
  Dim document As PdfDocument = converter.Convert(settings)

  'Save the PDF document
  document.Save("Output.pdf")
End Using
{% endhighlight %}

{% highlight UWP %}
//Excel To PDF conversion can be performed by referring .NET Standard assemblies in UWP platform
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;

  //Get assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Get input Excel document from an embedded resource collection
  Stream excelStream = assembly.GetManifestResourceStream("UWPSample.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Set the gridlines display style as Auto
  settings.DisplayGridLines = GridLinesDisplayStyle.Auto;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook,settings);

  //Save the PDF document
  MemoryStream stream = new MemoryStream();
  document.Save(stream);
  Save(stream, "Output.pdf");

  excelStream.Dispose();
}

//Save the PDF stream as a file
#region Setting output location
async void Save(Stream stream, string filename)
{
  stream.Position = 0;

  StorageFile stFile;
  if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
  {
    FileSavePicker savePicker = new FileSavePicker();
    savePicker.DefaultFileExtension = ".pdf";
    savePicker.SuggestedFileName = "Output";
    savePicker.FileTypeChoices.Add("Adobe PDF Document", new List<string>() { ".pdf" });
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
  stream.Dispose();
}
#endregion
{% endhighlight %}

{% highlight ASP.NET Core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream excelStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Set the gridlines display style as Auto
  settings.DisplayGridLines = GridLinesDisplayStyle.Auto;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook, settings);

  //Saving the Excel to the MemoryStream 
  MemoryStream stream = new MemoryStream();
  document.Save(stream);

  //Set the position as '0'
  stream.Position = 0;

  //Download the PDF file in the browser
  FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");
  fileStreamResult.FileDownloadName = "Output.pdf";
  return fileStreamResult;
}
{% endhighlight %}

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from an embedded resource collection
  Stream excelStream = assembly.GetManifestResourceStream("XamarinSample.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Set the gridlines display style as Auto
  settings.DisplayGridLines = GridLinesDisplayStyle.Auto;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook, settings);

  //Save the PDF document to stream
  MemoryStream stream = new MemoryStream();
  document.Save(stream);
  stream.Position = 0;

  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.pdf", "application/pdf", stream);
}
{% endhighlight %}
{% endtabs %}

### Invisible

Gridlines will not be rendered in the output PDF document, when display style is selected as **Invisible**. The following code snippet explains how to select **Invisible** display style for gridlines.

{% tabs %}
{% highlight C# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");

  //Initialize ExcelToPdfConverterSettings
  ExcelToPdfConverterSettings settings = new ExcelToPdfConverterSettings();

  //Set the gridlines display style as Invisible
  settings.DisplayGridLines = GridLinesDisplayStyle.Invisible;

  //Load the Excel document into ExcelToPdfConverter
  ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);

  //Convert the Excel document to PDF with converter settings
  PdfDocument document = converter.Convert(settings);

  //Save the PDF document
  document.Save("Output.pdf");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2016
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")

  'Initialize ExcelToPdfConverterSettings
  Dim settings As ExcelToPdfConverterSettings = New ExcelToPdfConverterSettings()

  'Set the gridlines display style as Invisible
  settings.DisplayGridLines = GridLinesDisplayStyle.Invisible

  'Load the Excel document into ExcelToPdfConverter
  Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(workbook)

  'Convert the Excel document to PDF with converter settings
  Dim document As PdfDocument = converter.Convert(settings)

  'Save the PDF document
  document.Save("Output.pdf")
End Using
{% endhighlight %}

{% highlight UWP %}
//Excel To PDF conversion can be performed by referring .NET Standard assemblies in UWP platform
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;

  //Get assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Get input Excel document from an embedded resource collection
  Stream excelStream = assembly.GetManifestResourceStream("UWPSample.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Set the gridlines display style as Invisible
  settings.DisplayGridLines = GridLinesDisplayStyle.Invisible;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook,settings);

  //Save the PDF document
  MemoryStream stream = new MemoryStream();
  document.Save(stream);
  Save(stream, "Output.pdf");

  excelStream.Dispose();
}

//Save the PDF stream as a file
#region Setting output location
async void Save(Stream stream, string filename)
{
  stream.Position = 0;

  StorageFile stFile;
  if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
  {
    FileSavePicker savePicker = new FileSavePicker();
    savePicker.DefaultFileExtension = ".pdf";
    savePicker.SuggestedFileName = "Output";
    savePicker.FileTypeChoices.Add("Adobe PDF Document", new List<string>() { ".pdf" });
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
  stream.Dispose();
}
#endregion
{% endhighlight %}

{% highlight ASP.NET Core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream excelStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Set the gridlines display style as Invisible
  settings.DisplayGridLines = GridLinesDisplayStyle.Invisible;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook, settings);

  //Saving the Excel to the MemoryStream 
  MemoryStream stream = new MemoryStream();
  document.Save(stream);

  //Set the position as '0'
  stream.Position = 0;

  //Download the PDF file in the browser
  FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");
  fileStreamResult.FileDownloadName = "Output.pdf";
  return fileStreamResult;
}
{% endhighlight %}

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from an embedded resource collection
  Stream excelStream = assembly.GetManifestResourceStream("XamarinSample.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Set the gridlines display style as Invisible
  settings.DisplayGridLines = GridLinesDisplayStyle.Invisible;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook, settings);

  //Save the PDF document to stream
  MemoryStream stream = new MemoryStream();
  document.Save(stream);
  stream.Position = 0;

  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.pdf", "application/pdf", stream);
}
{% endhighlight %}
{% endtabs %}

### Visible

Gridlines will be rendered in the output PDF document, when display style is selected as **Visible**. The following code snippet explains how to select **Visible** display style for gridlines.

{% tabs %}
{% highlight C# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");

  //Initialize ExcelToPdfConverterSettings
  ExcelToPdfConverterSettings settings = new ExcelToPdfConverterSettings();

  //Set the gridlines display style as Visible
  settings.DisplayGridLines = GridLinesDisplayStyle.Visible;

  //Load the Excel document into ExcelToPdfConverter
  ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);

  //Convert the Excel document to PDF with converter settings
  PdfDocument document = converter.Convert(settings);

  //Save the PDF document
  document.Save("Output.pdf");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2016
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")

  'Initialize ExcelToPdfConverterSettings
  Dim settings As ExcelToPdfConverterSettings = New ExcelToPdfConverterSettings()

  'Set the gridlines display style as Visible
  settings.DisplayGridLines = GridLinesDisplayStyle.Visible

  'Load the Excel document into ExcelToPdfConverter
  Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(workbook)

  'Convert the Excel document to PDF with converter settings
  Dim document As PdfDocument = converter.Convert(settings)

  'Save the PDF document
  document.Save("Output.pdf")
End Using
{% endhighlight %}

{% highlight UWP %}
//Excel To PDF conversion can be performed by referring .NET Standard assemblies in UWP platform
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;

  //Get assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Get input Excel document from an embedded resource collection
  Stream excelStream = assembly.GetManifestResourceStream("UWPSample.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Set the gridlines display style as Visible
  settings.DisplayGridLines = GridLinesDisplayStyle.Visible;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook,settings);

  //Save the PDF document
  MemoryStream stream = new MemoryStream();
  document.Save(stream);
  Save(stream, "Output.pdf");

  excelStream.Dispose();
}

//Save the PDF stream as a file
#region Setting output location
async void Save(Stream stream, string filename)
{
  stream.Position = 0;

  StorageFile stFile;
  if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
  {
    FileSavePicker savePicker = new FileSavePicker();
    savePicker.DefaultFileExtension = ".pdf";
    savePicker.SuggestedFileName = "Output";
    savePicker.FileTypeChoices.Add("Adobe PDF Document", new List<string>() { ".pdf" });
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
  stream.Dispose();
}
#endregion
{% endhighlight %}

{% highlight ASP.NET Core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream excelStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Set the gridlines display style as Visible
  settings.DisplayGridLines = GridLinesDisplayStyle.Visible;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook, settings);

  //Saving the Excel to the MemoryStream 
  MemoryStream stream = new MemoryStream();
  document.Save(stream);

  //Set the position as '0'
  stream.Position = 0;

  //Download the PDF file in the browser
  FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");
  fileStreamResult.FileDownloadName = "Output.pdf";
  return fileStreamResult;
}
{% endhighlight %}

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from an embedded resource collection
  Stream excelStream = assembly.GetManifestResourceStream("XamarinSample.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Set the gridlines display style as Visible
  settings.DisplayGridLines = GridLinesDisplayStyle.Visible;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook, settings);

  //Save the PDF document to stream
  MemoryStream stream = new MemoryStream();
  document.Save(stream);
  stream.Position = 0;

  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.pdf", "application/pdf", stream);
}
{% endhighlight %}
{% endtabs %}

## Embed Fonts

The Excel content will be rendered improperly when Arial Unicode MS Font is missing in the machine. In this case, enabling the `EmbedFonts` property renders the content properly.

The following code snippet explains how to enable `EmbedFonts` property.
{% tabs %}
{% highlight C# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");

  //Initialize ExcelToPdfConverterSettings
  ExcelToPdfConverterSettings settings = new ExcelToPdfConverterSettings();

  //Enable EmbedFonts
  settings.EmbedFonts = true;

  //Load the Excel document into ExcelToPdfConverter
  ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);

  //Convert the Excel document to PDF with converter settings
  PdfDocument document = converter.Convert(settings);

  //Save the PDF document
  document.Save("Output.pdf");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2016
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")

  'Initialize ExcelToPdfConverterSettings
  Dim settings As ExcelToPdfConverterSettings = New ExcelToPdfConverterSettings()

  'Enable EmbedFonts
  settings.EmbedFonts = True

  'Load the Excel document into ExcelToPdfConverter
  Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(workbook)

  'Convert the Excel document to PDF with converter settings
  Dim document As PdfDocument = converter.Convert(settings)

  'Save the PDF document
  document.Save("Output.pdf")
End Using
{% endhighlight %}

{% highlight UWP %}
//Excel To PDF conversion can be performed by referring .NET Standard assemblies in UWP platform
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;

  //Get assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Get input Excel document from an embedded resource collection
  Stream excelStream = assembly.GetManifestResourceStream("UWPSample.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Enable EmbedFonts
  settings.EmbedFonts = true;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook,settings);

  //Save the PDF document
  MemoryStream stream = new MemoryStream();
  document.Save(stream);
  Save(stream, "Output.pdf");

  excelStream.Dispose();
}

//Save the PDF stream as a file
#region Setting output location
async void Save(Stream stream, string filename)
{
  stream.Position = 0;

  StorageFile stFile;
  if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
  {
    FileSavePicker savePicker = new FileSavePicker();
    savePicker.DefaultFileExtension = ".pdf";
    savePicker.SuggestedFileName = "Output";
    savePicker.FileTypeChoices.Add("Adobe PDF Document", new List<string>() { ".pdf" });
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
  stream.Dispose();
}
{% endhighlight %}

{% highlight ASP.NET Core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream excelStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Enable EmbedFonts
  settings.EmbedFonts = true;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook, settings);

  //Saving the Excel to the MemoryStream 
  MemoryStream stream = new MemoryStream();
  document.Save(stream);

  //Set the position as '0'
  stream.Position = 0;

  //Download the PDF file in the browser
  FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");
  fileStreamResult.FileDownloadName = "Output.pdf";
  return fileStreamResult;
}
{% endhighlight %}

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from an embedded resource collection
  Stream excelStream = assembly.GetManifestResourceStream("XamarinSample.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Enable EmbedFonts
  settings.EmbedFonts = true;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook, settings);

  //Save the PDF document to stream
  MemoryStream stream = new MemoryStream();
  document.Save(stream);
  stream.Position = 0;

  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.pdf", "application/pdf", stream);
}
{% endhighlight %}
{% endtabs %}

## Export Bookmarks

The default value of `ExportBookmarks` property is TRUE and hence bookmarks are exported to PDF document by default, in Excel to PDF conversion. Disabling this property skips the bookmarks in conversion.

The following code snippet explains how to disable `ExportBookmarks` property.

{% tabs %}
{% highlight C# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");

  //Initialize ExcelToPdfConverterSettings
  ExcelToPdfConverterSettings settings = new ExcelToPdfConverterSettings();

  //Disable ExportBookmarks
  settings.ExportBookmarks = false;

  //Load the Excel document into ExcelToPdfConverter
  ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);

  //Convert the Excel document to PDF with converter settings
  PdfDocument document = converter.Convert(settings);

  //Save the PDF document
  document.Save("Output.pdf");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2016
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")

  'Initialize ExcelToPdfConverterSettings
  Dim settings As ExcelToPdfConverterSettings = New ExcelToPdfConverterSettings()

  'Disable ExportBookmarks
  settings.ExportBookmarks = False

  'Load the Excel document into ExcelToPdfConverter
  Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(workbook)

  'Convert the Excel document to PDF with converter settings
  Dim document As PdfDocument = converter.Convert(settings)

  'Save the PDF document
  document.Save("Output.pdf")
End Using
{% endhighlight %}

{% highlight UWP %}
//Excel To PDF conversion can be performed by referring .NET Standard assemblies in UWP platform
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;

  //Get assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Get input Excel document from an embedded resource collection
  Stream excelStream = assembly.GetManifestResourceStream("UWPSample.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Disable ExportBookmarks
  settings.ExportBookmarks = false;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook,settings);

  //Save the PDF document
  MemoryStream stream = new MemoryStream();
  document.Save(stream);
  Save(stream, "Output.pdf");

  excelStream.Dispose();
}

//Save the PDF stream as a file
#region Setting output location
async void Save(Stream stream, string filename)
{
  stream.Position = 0;

  StorageFile stFile;
  if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
  {
    FileSavePicker savePicker = new FileSavePicker();
    savePicker.DefaultFileExtension = ".pdf";
    savePicker.SuggestedFileName = "Output";
    savePicker.FileTypeChoices.Add("Adobe PDF Document", new List<string>() { ".pdf" });
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
  stream.Dispose();
}
{% endhighlight %}

{% highlight ASP.NET Core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream excelStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Disable ExportBookmarks
  settings.ExportBookmarks = false;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook, settings);

  //Saving the Excel to the MemoryStream 
  MemoryStream stream = new MemoryStream();
  document.Save(stream);

  //Set the position as '0'
  stream.Position = 0;

  //Download the PDF file in the browser
  FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");
  fileStreamResult.FileDownloadName = "Output.pdf";
  return fileStreamResult;
}
{% endhighlight %}

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from an embedded resource collection
  Stream excelStream = assembly.GetManifestResourceStream("XamarinSample.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Disable ExportBookmarks
  settings.ExportBookmarks = false;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook, settings);

  //Save the PDF document to stream
  MemoryStream stream = new MemoryStream();
  document.Save(stream);
  stream.Position = 0;

  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.pdf", "application/pdf", stream);
}
{% endhighlight %}
{% endtabs %}

## Export Document Properties

Excel document properties will be exported to PDF document by default, in Excel to PDF conversion. This can be skipped by disabling the ``ExportDocumentProperties``.

The following complete code snippet explains how to disable ``ExportDocumentProperties``.
{% tabs %}
{% highlight C# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");

  //Initialize ExcelToPdfConverterSettings
  ExcelToPdfConverterSettings settings = new ExcelToPdfConverterSettings();

  //Disable ExportDocumentProperties
  settings.ExportDocumentProperties = false;

  //Load the Excel document into ExcelToPdfConverter
  ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);

  //Convert the Excel document to PDF with converter settings
  PdfDocument document = converter.Convert(settings);

  //Save the PDF document
  document.Save("Output.pdf");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2016
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")

  'Initialize ExcelToPdfConverterSettings
  Dim settings As ExcelToPdfConverterSettings = New ExcelToPdfConverterSettings()

  'Disable ExportDocumentProperties
  settings.ExportDocumentProperties = False

  'Load the Excel document into ExcelToPdfConverter
  Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(workbook)

  'Convert the Excel document to PDF with converter settings
  Dim document As PdfDocument = converter.Convert(settings)

  'Save the PDF document
  document.Save("Output.pdf")
End Using
{% endhighlight %}

{% highlight UWP %}
//Excel To PDF conversion can be performed by referring .NET Standard assemblies in UWP platform
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;

  //Get assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Get input Excel document from an embedded resource collection
  Stream excelStream = assembly.GetManifestResourceStream("UWPSample.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Disable ExportDocumentProperties
  settings.ExportDocumentProperties = false;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook,settings);

  //Save the PDF document
  MemoryStream stream = new MemoryStream();
  document.Save(stream);
  Save(stream, "Output.pdf");

  excelStream.Dispose();
}

//Save the PDF stream as a file
#region Setting output location
async void Save(Stream stream, string filename)
{
  stream.Position = 0;

  StorageFile stFile;
  if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
  {
    FileSavePicker savePicker = new FileSavePicker();
    savePicker.DefaultFileExtension = ".pdf";
    savePicker.SuggestedFileName = "Output";
    savePicker.FileTypeChoices.Add("Adobe PDF Document", new List<string>() { ".pdf" });
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
  stream.Dispose();
}
{% endhighlight %}

{% highlight ASP.NET Core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream excelStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Disable ExportDocumentProperties
  settings.ExportDocumentProperties = false;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook, settings);

  //Saving the Excel to the MemoryStream 
  MemoryStream stream = new MemoryStream();
  document.Save(stream);

  //Set the position as '0'
  stream.Position = 0;

  //Download the PDF file in the browser
  FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");
  fileStreamResult.FileDownloadName = "Output.pdf";
  return fileStreamResult;
}
{% endhighlight %}

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from an embedded resource collection
  Stream excelStream = assembly.GetManifestResourceStream("XamarinSample.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Disable ExportDocumentProperties
  settings.ExportDocumentProperties = false;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook, settings);

  //Save the PDF document to stream
  MemoryStream stream = new MemoryStream();
  document.Save(stream);
  stream.Position = 0;

  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.pdf", "application/pdf", stream);
}
{% endhighlight %}
{% endtabs %}

## Export Quality Image

The default value of ``ExportQualityImage`` if FALSE. Enabling this property exports quality image to PDF document.

The following complete code snippet explains how to enable ``ExportQualityImage`` property.

{% tabs %}
{% highlight C# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");

  //Initialize ExcelToPdfConverterSettings
  ExcelToPdfConverterSettings settings = new ExcelToPdfConverterSettings();

  //Enable ExportQualityImage
  settings.ExportQualityImage = true;

  //Load the Excel document into ExcelToPdfConverter
  ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);

  //Convert the Excel document to PDF with converter settings
  PdfDocument document = converter.Convert(settings);

  //Save the PDF document
  document.Save("Output.pdf");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2016
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")

  'Initialize ExcelToPdfConverterSettings
  Dim settings As ExcelToPdfConverterSettings = New ExcelToPdfConverterSettings()

  'Enable ExportQualityImage
  settings.ExportQualityImage = True

  'Load the Excel document into ExcelToPdfConverter
  Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(workbook)

  'Convert the Excel document to PDF with converter settings
  Dim document As PdfDocument = converter.Convert(settings)

  'Save the PDF document
  document.Save("Output.pdf")
End Using
{% endhighlight %}

{% highlight UWP %}
//Excel To PDF conversion can be performed by referring .NET Standard assemblies in UWP platform
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;

  //Get assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Get input Excel document from an embedded resource collection
  Stream excelStream = assembly.GetManifestResourceStream("UWPSample.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Enable ExportQualityImage
  settings.ExportQualityImage = true;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook,settings);

  //Save the PDF document
  MemoryStream stream = new MemoryStream();
  document.Save(stream);
  Save(stream, "Output.pdf");

  excelStream.Dispose();
}

//Save the PDF stream as a file
#region Setting output location
async void Save(Stream stream, string filename)
{
  stream.Position = 0;

  StorageFile stFile;
  if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
  {
    FileSavePicker savePicker = new FileSavePicker();
    savePicker.DefaultFileExtension = ".pdf";
    savePicker.SuggestedFileName = "Output";
    savePicker.FileTypeChoices.Add("Adobe PDF Document", new List<string>() { ".pdf" });
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
  stream.Dispose();
}
{% endhighlight %}

{% highlight ASP.NET Core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream excelStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Enable ExportQualityImage
  settings.ExportQualityImage = true;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook, settings);

  //Saving the Excel to the MemoryStream 
  MemoryStream stream = new MemoryStream();
  document.Save(stream);

  //Set the position as '0'
  stream.Position = 0;

  //Download the PDF file in the browser
  FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");
  fileStreamResult.FileDownloadName = "Output.pdf";
  return fileStreamResult;
}
{% endhighlight %}

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from an embedded resource collection
  Stream excelStream = assembly.GetManifestResourceStream("XamarinSample.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Enable ExportQualityImage
  settings.ExportQualityImage = true;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook, settings);

  //Save the PDF document to stream
  MemoryStream stream = new MemoryStream();
  document.Save(stream);
  stream.Position = 0;

  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.pdf", "application/pdf", stream);
}
{% endhighlight %}
{% endtabs %}

## Header Footer Option

Two properties available under ``HeaderFooterOption`` are ShowHeader and ShowFooter. 

### Show Header

Document header will be rendered to PDF document by default. This can be skipped by disabling the ``ShowHeader`` property.

{% tabs %}
{% highlight C# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");

  //Initialize ExcelToPdfConverterSettings
  ExcelToPdfConverterSettings settings = new ExcelToPdfConverterSettings();

  //Disable ShowHeader
  settings.HeaderFooterOption.ShowHeader = false;

  //Load the Excel document into ExcelToPdfConverter
  ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);

  //Convert the Excel document to PDF with converter settings
  PdfDocument document = converter.Convert(settings);

  //Save the PDF document
  document.Save("Output.pdf");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2016
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")

  'Initialize ExcelToPdfConverterSettings
  Dim settings As ExcelToPdfConverterSettings = New ExcelToPdfConverterSettings()

  'Disable ShowHeader
  settings.HeaderFooterOption.ShowHeader = False

  'Load the Excel document into ExcelToPdfConverter
  Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(workbook)

  'Convert the Excel document to PDF with converter settings
  Dim document As PdfDocument = converter.Convert(settings)

  'Save the PDF document
  document.Save("Output.pdf")
End Using
{% endhighlight %}

{% highlight UWP %}
//Excel To PDF conversion can be performed by referring .NET Standard assemblies in UWP platform
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;

  //Get assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Get input Excel document from an embedded resource collection
  Stream excelStream = assembly.GetManifestResourceStream("UWPSample.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Disable ShowHeader
  settings.HeaderFooterOption.ShowHeader = false;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook,settings);

  //Save the PDF document
  MemoryStream stream = new MemoryStream();
  document.Save(stream);
  Save(stream, "Output.pdf");

  excelStream.Dispose();
}

//Save the PDF stream as a file
#region Setting output location
async void Save(Stream stream, string filename)
{
  stream.Position = 0;

  StorageFile stFile;
  if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
  {
    FileSavePicker savePicker = new FileSavePicker();
    savePicker.DefaultFileExtension = ".pdf";
    savePicker.SuggestedFileName = "Output";
    savePicker.FileTypeChoices.Add("Adobe PDF Document", new List<string>() { ".pdf" });
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
  stream.Dispose();
}
{% endhighlight %}

{% highlight ASP.NET Core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream excelStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Disable ShowHeader
  settings.HeaderFooterOption.ShowHeader = false;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook, settings);

  //Saving the Excel to the MemoryStream 
  MemoryStream stream = new MemoryStream();
  document.Save(stream);

  //Set the position as '0'
  stream.Position = 0;

  //Download the PDF file in the browser
  FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");
  fileStreamResult.FileDownloadName = "Output.pdf";
  return fileStreamResult;
}
{% endhighlight %}

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from an embedded resource collection
  Stream excelStream = assembly.GetManifestResourceStream("XamarinSample.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Disable ShowHeader
  settings.HeaderFooterOption.ShowHeader = false;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook, settings);

  //Save the PDF document to stream
  MemoryStream stream = new MemoryStream();
  document.Save(stream);
  stream.Position = 0;

  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.pdf", "application/pdf", stream);
}
{% endhighlight %}
{% endtabs %}

### Show Footer

Document footer will be rendered to PDF document by default. This can be skipped by disabling the ``ShowFooter`` property.

{% tabs %}
{% highlight C# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");

  //Initialize ExcelToPdfConverterSettings
  ExcelToPdfConverterSettings settings = new ExcelToPdfConverterSettings();

  //Disable ShowFooter
  settings.HeaderFooterOption.ShowFooter = false;

  //Load the Excel document into ExcelToPdfConverter
  ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);

  //Convert the Excel document to PDF with converter settings
  PdfDocument document = converter.Convert(settings);

  //Save the PDF document
  document.Save("Output.pdf");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2016
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")

  'Initialize ExcelToPdfConverterSettings
  Dim settings As ExcelToPdfConverterSettings = New ExcelToPdfConverterSettings()

  'Disable ShowFooter
  settings.HeaderFooterOption.ShowFooter = False

  'Load the Excel document into ExcelToPdfConverter
  Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(workbook)

  'Convert the Excel document to PDF with converter settings
  Dim document As PdfDocument = converter.Convert(settings)

  'Save the PDF document
  document.Save("Output.pdf")
End Using
{% endhighlight %}

{% highlight UWP %}
//Excel To PDF conversion can be performed by referring .NET Standard assemblies in UWP platform
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;

  //Get assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Get input Excel document from an embedded resource collection
  Stream excelStream = assembly.GetManifestResourceStream("UWPSample.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Disable ShowFooter
  settings.HeaderFooterOption.ShowFooter = false;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook,settings);

  //Save the PDF document
  MemoryStream stream = new MemoryStream();
  document.Save(stream);
  Save(stream, "Output.pdf");

  excelStream.Dispose();
}

//Save the PDF stream as a file
#region Setting output location
async void Save(Stream stream, string filename)
{
  stream.Position = 0;

  StorageFile stFile;
  if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
  {
    FileSavePicker savePicker = new FileSavePicker();
    savePicker.DefaultFileExtension = ".pdf";
    savePicker.SuggestedFileName = "Output";
    savePicker.FileTypeChoices.Add("Adobe PDF Document", new List<string>() { ".pdf" });
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
  stream.Dispose();
}
{% endhighlight %}

{% highlight ASP.NET Core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream excelStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Disable ShowFooter
  settings.HeaderFooterOption.ShowFooter = false;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook, settings);

  //Saving the Excel to the MemoryStream 
  MemoryStream stream = new MemoryStream();
  document.Save(stream);

  //Set the position as '0'
  stream.Position = 0;

  //Download the PDF file in the browser
  FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");
  fileStreamResult.FileDownloadName = "Output.pdf";
  return fileStreamResult;
}
{% endhighlight %}

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from an embedded resource collection
  Stream excelStream = assembly.GetManifestResourceStream("XamarinSample.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Disable ShowFooter
  settings.HeaderFooterOption.ShowFooter = false;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook, settings);

  //Save the PDF document to stream
  MemoryStream stream = new MemoryStream();
  document.Save(stream);
  stream.Position = 0;

  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.pdf", "application/pdf", stream);
}
{% endhighlight %}
{% endtabs %}

## Convert Blank Page

Blank pages in Excel document are rendered to PDF document by default, in Excel to PDF conversion. This blank pages can be skipped by disabling the ``IsConvertBlankPage`` property.

The following code snippet explains this.

{% tabs %}
{% highlight C# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");

  //Initialize ExcelToPdfConverterSettings
  ExcelToPdfConverterSettings settings = new ExcelToPdfConverterSettings();

  //Disable IsConvertBlankPage
  settings.IsConvertBlankPage = false;

  //Load the Excel document into ExcelToPdfConverter
  ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);

  //Convert the Excel document to PDF with converter settings
  PdfDocument document = converter.Convert(settings);

  //Save the PDF document
  document.Save("Output.pdf");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2016
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")

  'Initialize ExcelToPdfConverterSettings
  Dim settings As ExcelToPdfConverterSettings = New ExcelToPdfConverterSettings()

  'Disable IsConvertBlankPage
  settings.IsConvertBlankPage = False

  'Load the Excel document into ExcelToPdfConverter
  Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(workbook)

  'Convert the Excel document to PDF with converter settings
  Dim document As PdfDocument = converter.Convert(settings)

  'Save the PDF document
  document.Save("Output.pdf")
End Using
{% endhighlight %}

{% highlight UWP %}
//Excel To PDF conversion can be performed by referring .NET Standard assemblies in UWP platform
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;

  //Get assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Get input Excel document from an embedded resource collection
  Stream excelStream = assembly.GetManifestResourceStream("UWPSample.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Disable IsConvertBlankPage
  settings.IsConvertBlankPage = false;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook,settings);

  //Save the PDF document
  MemoryStream stream = new MemoryStream();
  document.Save(stream);
  Save(stream, "Output.pdf");

  excelStream.Dispose();
}

//Save the PDF stream as a file
#region Setting output location
async void Save(Stream stream, string filename)
{
  stream.Position = 0;

  StorageFile stFile;
  if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
  {
    FileSavePicker savePicker = new FileSavePicker();
    savePicker.DefaultFileExtension = ".pdf";
    savePicker.SuggestedFileName = "Output";
    savePicker.FileTypeChoices.Add("Adobe PDF Document", new List<string>() { ".pdf" });
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
  stream.Dispose();
}
{% endhighlight %}

{% highlight ASP.NET Core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream excelStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Disable IsConvertBlankPage
  settings.IsConvertBlankPage = false;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook, settings);

  //Saving the Excel to the MemoryStream 
  MemoryStream stream = new MemoryStream();
  document.Save(stream);

  //Set the position as '0'
  stream.Position = 0;

  //Download the PDF file in the browser
  FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");
  fileStreamResult.FileDownloadName = "Output.pdf";
  return fileStreamResult;
}
{% endhighlight %}

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from an embedded resource collection
  Stream excelStream = assembly.GetManifestResourceStream("XamarinSample.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Disable IsConvertBlankPage
  settings.IsConvertBlankPage = false;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook, settings);

  //Save the PDF document to stream
  MemoryStream stream = new MemoryStream();
  document.Save(stream);
  stream.Position = 0;

  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.pdf", "application/pdf", stream);
}
{% endhighlight %}
{% endtabs %}

## Convert Blank Sheet

Blank worksheets in Excel document are rendered to PDF document by default, in Excel to PDF conversion. This blank worksheets can be skipped by disabling the ``IsConvertBlankSheet`` property.

The following code snippet explains this.

{% tabs %}
{% highlight C# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");

  //Initialize ExcelToPdfConverterSettings
  ExcelToPdfConverterSettings settings = new ExcelToPdfConverterSettings();

  //Disable IsConvertBlankSheet
  settings.IsConvertBlankSheet = false;

  //Load the Excel document into ExcelToPdfConverter
  ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);

  //Convert the Excel document to PDF with converter settings
  PdfDocument document = converter.Convert(settings);

  //Save the PDF document
  document.Save("Output.pdf");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2016
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")

  'Initialize ExcelToPdfConverterSettings
  Dim settings As ExcelToPdfConverterSettings = New ExcelToPdfConverterSettings()

  'Disable IsConvertBlankSheet
  settings.IsConvertBlankSheet = False

  'Load the Excel document into ExcelToPdfConverter
  Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(workbook)

  'Convert the Excel document to PDF with converter settings
  Dim document As PdfDocument = converter.Convert(settings)

  'Save the PDF document
  document.Save("Output.pdf")
End Using
{% endhighlight %}

{% highlight UWP %}
//Excel To PDF conversion can be performed by referring .NET Standard assemblies in UWP platform
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;

  //Get assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Get input Excel document from an embedded resource collection
  Stream excelStream = assembly.GetManifestResourceStream("UWPSample.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Disable IsConvertBlankSheet
  settings.IsConvertBlankSheet = false;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook,settings);

  //Save the PDF document
  MemoryStream stream = new MemoryStream();
  document.Save(stream);
  Save(stream, "Output.pdf");

  excelStream.Dispose();
}

//Save the PDF stream as a file
#region Setting output location
async void Save(Stream stream, string filename)
{
  stream.Position = 0;

  StorageFile stFile;
  if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
  {
    FileSavePicker savePicker = new FileSavePicker();
    savePicker.DefaultFileExtension = ".pdf";
    savePicker.SuggestedFileName = "Output";
    savePicker.FileTypeChoices.Add("Adobe PDF Document", new List<string>() { ".pdf" });
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
  stream.Dispose();
}
{% endhighlight %}

{% highlight ASP.NET Core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream excelStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Disable IsConvertBlankSheet
  settings.IsConvertBlankSheet = false;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook, settings);

  //Saving the Excel to the MemoryStream 
  MemoryStream stream = new MemoryStream();
  document.Save(stream);

  //Set the position as '0'
  stream.Position = 0;

  //Download the PDF file in the browser
  FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");
  fileStreamResult.FileDownloadName = "Output.pdf";
  return fileStreamResult;
}
{% endhighlight %}

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from an embedded resource collection
  Stream excelStream = assembly.GetManifestResourceStream("XamarinSample.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Disable IsConvertBlankSheet
  settings.IsConvertBlankSheet = false;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook, settings);

  //Save the PDF document to stream
  MemoryStream stream = new MemoryStream();
  document.Save(stream);
  stream.Position = 0;

  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.pdf", "application/pdf", stream);
}
{% endhighlight %}
{% endtabs %}

## Layout Options

This property helps to select the layout option for the Excel document in Excel to PDF conversion. Five layout options available and maintained under ``LayoutOptions`` enumeration are **Automatic**, **CustomScaling**, **FitAllColumnsOnOnePage**, **FitAllRowsOnOnePage**, **FitSheetOnOnePage** and **NoScaling**.

### Automatic

Selecting **Automatic** under ``LayoutOptions`` prints the worksheets at their actual size. It's default value is **NoScaling**. The following code snippet explains how to select the layout option as **Automatic**.

{% tabs %}
{% highlight C# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");

  //Initialize ExcelToPdfConverterSettings
  ExcelToPdfConverterSettings settings = new ExcelToPdfConverterSettings();

  //Set layout option as Automatic
  settings.LayoutOptions = LayoutOptions.Automatic;

  //Load the Excel document into ExcelToPdfConverter
  ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);

  //Convert the Excel document to PDF with converter settings
  PdfDocument document = converter.Convert(settings);

  //Save the PDF document
  document.Save("Output.pdf");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2016
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")

  'Initialize ExcelToPdfConverterSettings
  Dim settings As ExcelToPdfConverterSettings = New ExcelToPdfConverterSettings()

  'Set layout option as Automatic
  settings.LayoutOptions = LayoutOptions.Automatic

  'Load the Excel document into ExcelToPdfConverter
  Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(workbook)

  'Convert the Excel document to PDF with converter settings
  Dim document As PdfDocument = converter.Convert(settings)

  'Save the PDF document
  document.Save("Output.pdf")
End Using
{% endhighlight %}

{% highlight UWP %}
//Excel To PDF conversion can be performed by referring .NET Standard assemblies in UWP platform
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;

  //Get assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Get input Excel document from an embedded resource collection
  Stream excelStream = assembly.GetManifestResourceStream("UWPSample.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Set layout option as Automatic
  settings.LayoutOptions = LayoutOptions.Automatic;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook,settings);

  //Save the PDF document
  MemoryStream stream = new MemoryStream();
  document.Save(stream);
  Save(stream, "Output.pdf");

  excelStream.Dispose();
}

//Save the PDF stream as a file
#region Setting output location
async void Save(Stream stream, string filename)
{
  stream.Position = 0;

  StorageFile stFile;
  if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
  {
    FileSavePicker savePicker = new FileSavePicker();
    savePicker.DefaultFileExtension = ".pdf";
    savePicker.SuggestedFileName = "Output";
    savePicker.FileTypeChoices.Add("Adobe PDF Document", new List<string>() { ".pdf" });
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
  stream.Dispose();
}
{% endhighlight %}

{% highlight ASP.NET Core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream excelStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Set layout option as Automatic
  settings.LayoutOptions = LayoutOptions.Automatic;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook, settings);

  //Saving the Excel to the MemoryStream 
  MemoryStream stream = new MemoryStream();
  document.Save(stream);

  //Set the position as '0'
  stream.Position = 0;

  //Download the PDF file in the browser
  FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");
  fileStreamResult.FileDownloadName = "Output.pdf";
  return fileStreamResult;
}
{% endhighlight %}

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from an embedded resource collection
  Stream excelStream = assembly.GetManifestResourceStream("XamarinSample.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Set layout option as Automatic
  settings.LayoutOptions = Syncfusion.XlsIORenderer.LayoutOptions.Automatic;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook, settings);

  //Save the PDF document to stream
  MemoryStream stream = new MemoryStream();
  document.Save(stream);
  stream.Position = 0;

  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.pdf", "application/pdf", stream);
}
{% endhighlight %}
{% endtabs %}

### Custom Scaling

Selecting **CustomScaling** under ``LayoutOptions`` prints the worksheets at specified scaling, i.e., zoom value set in under page setup. The following code snippet explains how to use this.

{% tabs %}
{% highlight C# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");

  //Initialize ExcelToPdfConverterSettings
  ExcelToPdfConverterSettings settings = new ExcelToPdfConverterSettings();

  //Set layout option as CustomScaling
  settings.LayoutOptions = LayoutOptions.CustomScaling;

  //Load the Excel document into ExcelToPdfConverter
  ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);

  //Convert the Excel document to PDF with converter settings
  PdfDocument document = converter.Convert(settings);

  //Save the PDF document
  document.Save("Output.pdf");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2016
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")

  'Initialize ExcelToPdfConverterSettings
  Dim settings As ExcelToPdfConverterSettings = New ExcelToPdfConverterSettings()

  'Set layout option as CustomScaling
  settings.LayoutOptions = LayoutOptions.CustomScaling

  'Load the Excel document into ExcelToPdfConverter
  Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(workbook)

  'Convert the Excel document to PDF with converter settings
  Dim document As PdfDocument = converter.Convert(settings)

  'Save the PDF document
  document.Save("Output.pdf")
End Using
{% endhighlight %}

{% highlight UWP %}
//Excel To PDF conversion can be performed by referring .NET Standard assemblies in UWP platform
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;

  //Get assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Get input Excel document from an embedded resource collection
  Stream excelStream = assembly.GetManifestResourceStream("UWPSample.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Set layout option as CustomScaling
  settings.LayoutOptions = LayoutOptions.CustomScaling;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook,settings);

  //Save the PDF document
  MemoryStream stream = new MemoryStream();
  document.Save(stream);
  Save(stream, "Output.pdf");

  excelStream.Dispose();
}

//Save the PDF stream as a file
#region Setting output location
async void Save(Stream stream, string filename)
{
  stream.Position = 0;

  StorageFile stFile;
  if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
  {
    FileSavePicker savePicker = new FileSavePicker();
    savePicker.DefaultFileExtension = ".pdf";
    savePicker.SuggestedFileName = "Output";
    savePicker.FileTypeChoices.Add("Adobe PDF Document", new List<string>() { ".pdf" });
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
  stream.Dispose();
}
{% endhighlight %}

{% highlight ASP.NET Core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream excelStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Set layout option as CustomScaling
  settings.LayoutOptions = LayoutOptions.CustomScaling;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook, settings);

  //Saving the Excel to the MemoryStream 
  MemoryStream stream = new MemoryStream();
  document.Save(stream);

  //Set the position as '0'
  stream.Position = 0;

  //Download the PDF file in the browser
  FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");
  fileStreamResult.FileDownloadName = "Output.pdf";
  return fileStreamResult;
}
{% endhighlight %}

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from an embedded resource collection
  Stream excelStream = assembly.GetManifestResourceStream("XamarinSample.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Set layout option as CustomScaling
  settings.LayoutOptions = Syncfusion.XlsIORenderer.LayoutOptions.CustomScaling;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook, settings);

  //Save the PDF document to stream
  MemoryStream stream = new MemoryStream();
  document.Save(stream);
  stream.Position = 0;

  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.pdf", "application/pdf", stream);
}
{% endhighlight %}
{% endtabs %}

### Fit All Columns On One Page

Selecting **FitAllColumnsOnOnePage** under ``LayoutOptions`` renders all columns in Excel worksheet into single PDF page. The following code snippet explains how to select the layout option as **FitAllColumnsOnOnePage**.

{% tabs %}
{% highlight C# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");

  //Initialize ExcelToPdfConverterSettings
  ExcelToPdfConverterSettings settings = new ExcelToPdfConverterSettings();

  //Set layout option as FitAllColumnsOnOnePage
  settings.LayoutOptions = LayoutOptions.FitAllColumnsOnOnePage;

  //Load the Excel document into ExcelToPdfConverter
  ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);

  //Convert the Excel document to PDF with converter settings
  PdfDocument document = converter.Convert(settings);

  //Save the PDF document
  document.Save("Output.pdf");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2016
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")

  'Initialize ExcelToPdfConverterSettings
  Dim settings As ExcelToPdfConverterSettings = New ExcelToPdfConverterSettings()

  'Set layout option as FitAllColumnsOnOnePage
  settings.LayoutOptions = LayoutOptions.FitAllColumnsOnOnePage

  'Load the Excel document into ExcelToPdfConverter
  Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(workbook)

  'Convert the Excel document to PDF with converter settings
  Dim document As PdfDocument = converter.Convert(settings)

  'Save the PDF document
  document.Save("Output.pdf")
End Using
{% endhighlight %}

{% highlight UWP %}
//Excel To PDF conversion can be performed by referring .NET Standard assemblies in UWP platform
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;

  //Get assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Get input Excel document from an embedded resource collection
  Stream excelStream = assembly.GetManifestResourceStream("UWPSample.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Set layout option as FitAllColumnsOnOnePage
  settings.LayoutOptions = LayoutOptions.FitAllColumnsOnOnePage;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook,settings);

  //Save the PDF document
  MemoryStream stream = new MemoryStream();
  document.Save(stream);
  Save(stream, "Output.pdf");

  excelStream.Dispose();
}

//Save the PDF stream as a file
#region Setting output location
async void Save(Stream stream, string filename)
{
  stream.Position = 0;

  StorageFile stFile;
  if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
  {
    FileSavePicker savePicker = new FileSavePicker();
    savePicker.DefaultFileExtension = ".pdf";
    savePicker.SuggestedFileName = "Output";
    savePicker.FileTypeChoices.Add("Adobe PDF Document", new List<string>() { ".pdf" });
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
  stream.Dispose();
}
{% endhighlight %}

{% highlight ASP.NET Core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream excelStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Set layout option as FitAllColumnsOnOnePage
  settings.LayoutOptions = LayoutOptions.FitAllColumnsOnOnePage;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook, settings);

  //Saving the Excel to the MemoryStream 
  MemoryStream stream = new MemoryStream();
  document.Save(stream);

  //Set the position as '0'
  stream.Position = 0;

  //Download the PDF file in the browser
  FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");
  fileStreamResult.FileDownloadName = "Output.pdf";
  return fileStreamResult;
}
{% endhighlight %}

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from an embedded resource collection
  Stream excelStream = assembly.GetManifestResourceStream("XamarinSample.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Set layout option as FitAllColumnsOnOnePage
  settings.LayoutOptions = Syncfusion.XlsIORenderer.LayoutOptions.FitAllColumnsOnOnePage;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook, settings);

  //Save the PDF document to stream
  MemoryStream stream = new MemoryStream();
  document.Save(stream);
  stream.Position = 0;

  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.pdf", "application/pdf", stream);
}
{% endhighlight %}
{% endtabs %}

### Fit All Rows On One Page

Selecting **FitAllRowsOnOnePage** under ``LayoutOptions`` renders all rows in Excel worksheet into single PDF page. The following code snippet explains how to select the layout option as **FitAllRowsOnOnePage**.

{% tabs %}
{% highlight C# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");

  //Initialize ExcelToPdfConverterSettings
  ExcelToPdfConverterSettings settings = new ExcelToPdfConverterSettings();

  //Set layout option as FitAllRowsOnOnePage
  settings.LayoutOptions = LayoutOptions.FitAllRowsOnOnePage;

  //Load the Excel document into ExcelToPdfConverter
  ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);

  //Convert the Excel document to PDF with converter settings
  PdfDocument document = converter.Convert(settings);

  //Save the PDF document
  document.Save("Output.pdf");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2016
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")

  'Initialize ExcelToPdfConverterSettings
  Dim settings As ExcelToPdfConverterSettings = New ExcelToPdfConverterSettings()

  'Set layout option as FitAllRowsOnOnePage
  settings.LayoutOptions = LayoutOptions.FitAllRowsOnOnePage

  'Load the Excel document into ExcelToPdfConverter
  Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(workbook)

  'Convert the Excel document to PDF with converter settings
  Dim document As PdfDocument = converter.Convert(settings)

  'Save the PDF document
  document.Save("Output.pdf")
End Using
{% endhighlight %}

{% highlight UWP %}
//Excel To PDF conversion can be performed by referring .NET Standard assemblies in UWP platform
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;

  //Get assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Get input Excel document from an embedded resource collection
  Stream excelStream = assembly.GetManifestResourceStream("UWPSample.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Set layout option as FitAllRowsOnOnePage
  settings.LayoutOptions = LayoutOptions.FitAllRowsOnOnePage;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook,settings);

  //Save the PDF document
  MemoryStream stream = new MemoryStream();
  document.Save(stream);
  Save(stream, "Output.pdf");

  excelStream.Dispose();
}

//Save the PDF stream as a file
#region Setting output location
async void Save(Stream stream, string filename)
{
  stream.Position = 0;

  StorageFile stFile;
  if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
  {
    FileSavePicker savePicker = new FileSavePicker();
    savePicker.DefaultFileExtension = ".pdf";
    savePicker.SuggestedFileName = "Output";
    savePicker.FileTypeChoices.Add("Adobe PDF Document", new List<string>() { ".pdf" });
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
  stream.Dispose();
}
{% endhighlight %}

{% highlight ASP.NET Core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream excelStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Set layout option as FitAllRowsOnOnePage
  settings.LayoutOptions = LayoutOptions.FitAllRowsOnOnePage;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook, settings);

  //Saving the Excel to the MemoryStream 
  MemoryStream stream = new MemoryStream();
  document.Save(stream);

  //Set the position as '0'
  stream.Position = 0;

  //Download the PDF file in the browser
  FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");
  fileStreamResult.FileDownloadName = "Output.pdf";
  return fileStreamResult;
}
{% endhighlight %}

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from an embedded resource collection
  Stream excelStream = assembly.GetManifestResourceStream("XamarinSample.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Set layout option as FitAllRowsOnOnePage
  settings.LayoutOptions = Syncfusion.XlsIORenderer.LayoutOptions.FitAllRowsOnOnePage;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook, settings);

  //Save the PDF document to stream
  MemoryStream stream = new MemoryStream();
  document.Save(stream);
  stream.Position = 0;

  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.pdf", "application/pdf", stream);
}
{% endhighlight %}
{% endtabs %}

### Fit Sheet On One Page

Selecting **FitSheetOnOnePage** under ``LayoutOptions`` renders every single worksheet in Excel workbook into, single PDF page. The following code snippet explains how to select the layout option as **FitSheetOnOnePage**.

{% tabs %}
{% highlight C# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");

  //Initialize ExcelToPdfConverterSettings
  ExcelToPdfConverterSettings settings = new ExcelToPdfConverterSettings();

  //Set layout option as FitSheetOnOnePage
  settings.LayoutOptions = LayoutOptions.FitSheetOnOnePage;

  //Load the Excel document into ExcelToPdfConverter
  ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);

  //Convert the Excel document to PDF with converter settings
  PdfDocument document = converter.Convert(settings);

  //Save the PDF document
  document.Save("Output.pdf");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2016
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")

  'Initialize ExcelToPdfConverterSettings
  Dim settings As ExcelToPdfConverterSettings = New ExcelToPdfConverterSettings()

  'Set layout option as FitSheetOnOnePage
  settings.LayoutOptions = LayoutOptions.FitSheetOnOnePage

  'Load the Excel document into ExcelToPdfConverter
  Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(workbook)

  'Convert the Excel document to PDF with converter settings
  Dim document As PdfDocument = converter.Convert(settings)

  'Save the PDF document
  document.Save("Output.pdf")
End Using
{% endhighlight %}

{% highlight UWP %}
//Excel To PDF conversion can be performed by referring .NET Standard assemblies in UWP platform
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;

  //Get assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Get input Excel document from an embedded resource collection
  Stream excelStream = assembly.GetManifestResourceStream("UWPSample.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Set layout option as FitSheetOnOnePage
  settings.LayoutOptions = LayoutOptions.FitSheetOnOnePage;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook,settings);

  //Save the PDF document
  MemoryStream stream = new MemoryStream();
  document.Save(stream);
  Save(stream, "Output.pdf");

  excelStream.Dispose();
}

//Save the PDF stream as a file
#region Setting output location
async void Save(Stream stream, string filename)
{
  stream.Position = 0;

  StorageFile stFile;
  if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
  {
    FileSavePicker savePicker = new FileSavePicker();
    savePicker.DefaultFileExtension = ".pdf";
    savePicker.SuggestedFileName = "Output";
    savePicker.FileTypeChoices.Add("Adobe PDF Document", new List<string>() { ".pdf" });
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
  stream.Dispose();
}
{% endhighlight %}

{% highlight ASP.NET Core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream excelStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Set layout option as FitSheetOnOnePage
  settings.LayoutOptions = LayoutOptions.FitSheetOnOnePage;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook, settings);

  //Saving the Excel to the MemoryStream 
  MemoryStream stream = new MemoryStream();
  document.Save(stream);

  //Set the position as '0'
  stream.Position = 0;

  //Download the PDF file in the browser
  FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");
  fileStreamResult.FileDownloadName = "Output.pdf";
  return fileStreamResult;
}
{% endhighlight %}

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from an embedded resource collection
  Stream excelStream = assembly.GetManifestResourceStream("XamarinSample.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Set layout option as FitSheetOnOnePage
  settings.LayoutOptions = Syncfusion.XlsIORenderer.LayoutOptions.FitSheetOnOnePage;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook, settings);

  //Save the PDF document to stream
  MemoryStream stream = new MemoryStream();
  document.Save(stream);
  stream.Position = 0;

  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.pdf", "application/pdf", stream);
}
{% endhighlight %}
{% endtabs %}

### No Scaling

Selecting **NoScaling** under ``LayoutOptions`` prints the worksheets at their actual size. The following code snippet explains how to select the layout option as **NoScaling**.

{% tabs %}
{% highlight C# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");

  //Initialize ExcelToPdfConverterSettings
  ExcelToPdfConverterSettings settings = new ExcelToPdfConverterSettings();

  //Set layout option as NoScaling
  settings.LayoutOptions = LayoutOptions.NoScaling;

  //Load the Excel document into ExcelToPdfConverter
  ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);

  //Convert the Excel document to PDF with converter settings
  PdfDocument document = converter.Convert(settings);

  //Save the PDF document
  document.Save("Output.pdf");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2016
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")

  'Initialize ExcelToPdfConverterSettings
  Dim settings As ExcelToPdfConverterSettings = New ExcelToPdfConverterSettings()

  'Set layout option as NoScaling
  settings.LayoutOptions = LayoutOptions.NoScaling

  'Load the Excel document into ExcelToPdfConverter
  Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(workbook)

  'Convert the Excel document to PDF with converter settings
  Dim document As PdfDocument = converter.Convert(settings)

  'Save the PDF document
  document.Save("Output.pdf")
End Using
{% endhighlight %}

{% highlight UWP %}
//Excel To PDF conversion can be performed by referring .NET Standard assemblies in UWP platform
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;

  //Get assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Get input Excel document from an embedded resource collection
  Stream excelStream = assembly.GetManifestResourceStream("UWPSample.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Set layout option as NoScaling
  settings.LayoutOptions = LayoutOptions.NoScaling;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook,settings);

  //Save the PDF document
  MemoryStream stream = new MemoryStream();
  document.Save(stream);
  Save(stream, "Output.pdf");

  excelStream.Dispose();
}

//Save the PDF stream as a file
#region Setting output location
async void Save(Stream stream, string filename)
{
  stream.Position = 0;

  StorageFile stFile;
  if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
  {
    FileSavePicker savePicker = new FileSavePicker();
    savePicker.DefaultFileExtension = ".pdf";
    savePicker.SuggestedFileName = "Output";
    savePicker.FileTypeChoices.Add("Adobe PDF Document", new List<string>() { ".pdf" });
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
  stream.Dispose();
}
{% endhighlight %}

{% highlight ASP.NET Core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream excelStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Set layout option as NoScaling
  settings.LayoutOptions = LayoutOptions.NoScaling;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook, settings);

  //Saving the Excel to the MemoryStream 
  MemoryStream stream = new MemoryStream();
  document.Save(stream);

  //Set the position as '0'
  stream.Position = 0;

  //Download the PDF file in the browser
  FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");
  fileStreamResult.FileDownloadName = "Output.pdf";
  return fileStreamResult;
}
{% endhighlight %}

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from an embedded resource collection
  Stream excelStream = assembly.GetManifestResourceStream("XamarinSample.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Set layout option as NoScaling
  settings.LayoutOptions = Syncfusion.XlsIORenderer.LayoutOptions.NoScaling;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook, settings);

  //Save the PDF document to stream
  MemoryStream stream = new MemoryStream();
  document.Save(stream);
  stream.Position = 0;

  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.pdf", "application/pdf", stream);
}
{% endhighlight %}
{% endtabs %}

## PDF Conformance Level

Excel to PDF converter settings allows you to set the PDF conformance level. Excel to PDF currently supports following PDF conformances.
* PDF/A-1b conformance
* PDF/X-1a conformance

N> 1. To know more details about PDF conformance refer [https://help.syncfusion.com/file-formats/pdf/working-with-pdf-conformance](https://help.syncfusion.com/file-formats/pdf/working-with-pdf-conformance)
N> 2. Pdf_X1A2001 is not supported for NETStandard.

The following code illustrates  how to set the PdfConformanceLevel while converting  Excel workbook to PDF.

{% tabs %}  

{% highlight c# %}
using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

  //Open the Excel document to Convert
  ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);

  //Initialize Excel to PDF converter settings
  ExcelToPdfConverterSettings settings = new ExcelToPdfConverterSettings();
  
  // Set the conformance for PDF/A-1b conversion
  settings.PdfConformanceLevel = PdfConformanceLevel.Pdf_A1B;

  //Convert Excel document into PDF document
  PdfDocument pdfDocument = converter.Convert(settings);

  //Save the PDF file
  pdfDocument.Save("ExcelToPDF.pdf");
}

{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

  'Open the Excel document to convert
  Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(workbook)

  'Initialize Excel to PDF converter settings
  Dim settings As ExcelToPdfConverterSettings = New ExcelToPdfConverterSettings()
  
  'Set the conformance for PDF/A-1b conversion
  settings.PdfConformanceLevel = PdfConformanceLevel.Pdf_A1B

  'Convert Excel document into PDF document
  Dim pdfDocument As PdfDocument = converter.Convert(settings)

  'Save the PDF file
  pdfDocument.Save("ExcelToPDF.pdf")
End Using
{% endhighlight %}

{% highlight UWP %}
//Excel To PDF conversion can be performed by referring .NET Standard assemblies in UWP platform

#region Excel To PDF
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    
    //Gets assembly
    Assembly assembly = typeof(App).GetTypeInfo().Assembly;

    //Gets input Excel document from an embedded resource collection
    Stream excelStream = assembly.GetManifestResourceStream("ExcelToPDF.xlsx");
	
    IWorkbook workbook = await application.Workbooks.OpenAsync(excelStream);

    //Initialize XlsIO renderer.
    XlsIORenderer renderer = new XlsIORenderer();
	
    //Initialize XlsIO renderer settings
    XlsIORendererSettings settings = new XlsIORendererSettings();

    // Set the conformance for PDF/A-1b conversion
    settings.PdfConformanceLevel = PdfConformanceLevel.Pdf_A1B;
  
    //Convert Excel document into PDF document 
    PdfDocument pdfDocument = renderer.ConvertToPDF(workbook, settings);

    //Save the PDF document to stream.
    MemoryStream stream = new MemoryStream();

    await pdfDocument.SaveAsync(stream);
    Save(stream, "ExcelToPDF.pdf");

    excelStream.Dispose();
    stream.Dispose();
}
#endregion

//Save the workbook stream as a file.

#region Setting output location
async void Save(Stream stream, string filename)
{
    stream.Position = 0;

    StorageFile stFile;
    if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
    {
        FileSavePicker savePicker = new FileSavePicker();
        savePicker.DefaultFileExtension = ".pdf";
        savePicker.SuggestedFileName = "Sample";
        savePicker.FileTypeChoices.Add("Adobe PDF Document", new List<string>() { ".pdf" });
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

{% highlight ASP.NET Core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
   IApplication application = excelEngine.Excel;
   FileStream excelStream = new FileStream("ExcelToPDF.xlsx", FileMode.Open, FileAccess.Read);
   IWorkbook workbook = application.Workbooks.Open(excelStream);

   //Initialize XlsIO renderer.
   XlsIORenderer renderer = new XlsIORenderer();
	
   //Initialize XlsIO renderer settings
   XlsIORendererSettings settings = new XlsIORendererSettings();

   // Set the conformance for PDF/A-1b conversion
   settings.PdfConformanceLevel = PdfConformanceLevel.Pdf_A1B;
  
   //Convert Excel document into PDF document 
   PdfDocument pdfDocument = renderer.ConvertToPDF(workbook, settings);

   Stream stream = new FileStream("ExcelToPDF.pdf", FileMode.Create, FileAccess.ReadWrite);
   pdfDocument.Save(stream);

   excelStream.Dispose();
   stream.Dispose();
}
{% endhighlight %}

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
   
    //Gets assembly
    Assembly assembly = typeof(App).GetTypeInfo().Assembly;

    //Gets input Excel document from an embedded resource collection
    Stream excelStream = assembly.GetManifestResourceStream("ExcelToPDF.xlsx");

    IWorkbook workbook = application.Workbooks.Open(excelStream);

    //Initialize XlsIO renderer.
    XlsIORenderer renderer = new XlsIORenderer();
	
	//Initialize XlsIO renderer settings
	XlsIORendererSettings settings = new XlsIORendererSettings();

    // Set the conformance for PDF/A-1b conversion
    settings.PdfConformanceLevel = PdfConformanceLevel.Pdf_A1B;
  
    //Convert Excel document into PDF document 
    PdfDocument pdfDocument = renderer.ConvertToPDF(workbook, settings);

    //Save the PDF document to stream.
    MemoryStream stream = new MemoryStream();
    pdfDocument.Save(stream);

    stream.Position = 0;

    //Save the stream into pdf file
    if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    {
        Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("ExcelToPDF.pdf", "application/pdf", stream);
    }
    else
    {
        Xamarin.Forms.DependencyService.Get<ISave>().Save("ExcelToPDF.pdf", "application/pdf", stream);
    }

    excelStream.Dispose();
    stream.Dispose();
}
{% endhighlight %}

{% endtabs %}

## Template Document

``TemplateDocument`` property helps to store the PDF document. 

The following complete code snippet explains how to convert and save two Excel documents into single PDF document using ``TemplateDocument`` property.

{% tabs %}
{% highlight C# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;
  IWorkbook workbook1 = application.Workbooks.Open("Sample1.xlsx");
  IWorkbook workbook2 = application.Workbooks.Open("Sample2.xlsx");

  //Load the Excel documents into ExcelToPdfConverter
  ExcelToPdfConverter converter1 = new ExcelToPdfConverter(workbook1);
  ExcelToPdfConverter converter2 = new ExcelToPdfConverter(workbook2);

  //Convert the first Excel document to PDF
  PdfDocument document = converter1.Convert();

  //Initialize ExcelToPdfConverterSettings
  ExcelToPdfConverterSettings settings = new ExcelToPdfConverterSettings();

  //Set the document as TemplateDocument
  settings.TemplateDocument = document;

  //Create a new PDF document and convert the second Excel document with settings
  PdfDocument newDocument = new PdfDocument();
  newDocument = converter2.Convert(settings);

  //Save the new PDF Document
  newDocument.Save("Output.pdf");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2016
  Dim workbook1 As IWorkbook = application.Workbooks.Open("Sample1.xlsx")
  Dim workbook2 As IWorkbook = application.Workbooks.Open("Sample2.xlsx")

  'Load the Excel documents into ExcelToPdfConverter
  Dim converter1 As ExcelToPdfConverter = New ExcelToPdfConverter(workbook1)
  Dim converter2 As ExcelToPdfConverter = New ExcelToPdfConverter(workbook2)

  'Convert the first Excel document to PDF
  Dim document As PdfDocument = converter1.Convert

  'Initialize ExcelToPdfConverterSettings
  Dim settings As ExcelToPdfConverterSettings = New ExcelToPdfConverterSettings()

  'Set the document as TemplateDocument
  settings.TemplateDocument = document

  'Create a new PDF document and convert the second Excel document with settings
  Dim newDocument As PdfDocument = New PdfDocument
  newDocument = converter2.Convert(settings)

  'Save the PDF document
  document.Save("Output.pdf")
End Using
{% endhighlight %}

{% highlight UWP %}
//Excel To PDF conversion can be performed by referring .NET Standard assemblies in UWP platform
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;

  //Get assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel documents from an embedded resource collection
  Stream excelStream1 = assembly.GetManifestResourceStream("UWPSample.Sample1.xlsx");
  IWorkbook workbook1 = application.Workbooks.Open(excelStream1);

  Stream excelStream2 = assembly.GetManifestResourceStream("UWPSample.Sample2.xlsx");
  IWorkbook workbook2 = application.Workbooks.Open(excelStream2);

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the first Excel document to PDF
  PdfDocument document = renderer.ConvertToPDF(workbook1);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Set the document as TemplateDocument
  settings.TemplateDocument = document;

  //Convert the second Excel document to PDF with renderer settings
  PdfDocument newDocument = renderer.ConvertToPDF(workbook2, settings);

  //Save the PDF document
  MemoryStream stream = new MemoryStream();
  document.Save(stream);
  Save(stream, "Output.pdf");

  excelStream1.Dispose();
  excelStream2.Dispose();
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
    savePicker.DefaultFileExtension = ".pdf";
    savePicker.SuggestedFileName = "Sample";
    savePicker.FileTypeChoices.Add("Adobe PDF Document", new List<string>() { ".pdf" });
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

{% highlight ASP.NET Core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream excelStream1 = new FileStream("Sample1.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook1 = application.Workbooks.Open(excelStream1);

  FileStream excelStream2 = new FileStream("Sample2.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook2 = application.Workbooks.Open(excelStream2);

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the first Excel document to PDF
  PdfDocument document = renderer.ConvertToPDF(workbook1);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Set the document as TemplateDocument
  settings.TemplateDocument = document;

  //Convert the second Excel document to PDF with renderer settings
  PdfDocument newDocument = renderer.ConvertToPDF(workbook2, settings);

  //Saving the Excel to the MemoryStream 
  MemoryStream stream = new MemoryStream();
  newDocument.Save(stream);

  //Set the position as '0'
  stream.Position = 0;

  //Download the PDF file in the browser
  FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");
  fileStreamResult.FileDownloadName = "Output.pdf";
  return fileStreamResult;
}
{% endhighlight %}

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel documents from an embedded resource collection
  Stream excelStream1 = assembly.GetManifestResourceStream("XamarinSample.Sample1.xlsx");
  IWorkbook workbook1 = application.Workbooks.Open(excelStream1);

  Stream excelStream2 = assembly.GetManifestResourceStream("XamarinSample.Sample2.xlsx");
  IWorkbook workbook2 = application.Workbooks.Open(excelStream2);

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the first Excel document to PDF
  PdfDocument document = renderer.ConvertToPDF(workbook1);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Set the document as TemplateDocument
  settings.TemplateDocument = document;

  //Convert the second Excel document to PDF with renderer settings
  PdfDocument newDocument = renderer.ConvertToPDF(workbook2, settings);

  //Save the PDF document to stream
  MemoryStream stream = new MemoryStream();
  newDocument.Save(stream);
  stream.Position = 0;

  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.pdf", "application/pdf", stream);
}
{% endhighlight %}
{% endtabs %}

## Throw When Excel File Is Empty

The default value of ``ThrowWhenExcelFileIsEmpty`` property is FALSE, and hence the empty Excel document will be converted to PDF without any exception. Enabling this property throws **ExcelToPdfConverterException**, saying that the Excel document is Empty.

The following code snippet explains this.

{% tabs %}
{% highlight C# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;
  IWorkbook workbook = application.Workbooks.Create(1);

  //Initialize ExcelToPdfConverterSettings
  ExcelToPdfConverterSettings settings = new ExcelToPdfConverterSettings();

  //Enabling ThrowWhenExcelFileIsEmpty throws exception
  settings.ThrowWhenExcelFileIsEmpty = true;

  //Load the Excel document into ExcelToPdfConverter
  ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);

  //Convert the Excel document to PDF with converter settings
  PdfDocument document = converter.Convert(settings);

  //Save the PDF document
  document.Save("Output.pdf");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2016
  Dim workbook As IWorkbook = application.Workbooks.Create(1)

  'Initialize ExcelToPdfConverterSettings
  Dim settings As ExcelToPdfConverterSettings = New ExcelToPdfConverterSettings()

  'Enabling ThrowWhenExcelFileIsEmpty throws exception
  settings.ThrowWhenExcelFileIsEmpty = True

  'Load the Excel document into ExcelToPdfConverter
  Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(workbook)

  'Convert the Excel document to PDF with converter settings
  Dim document As PdfDocument = converter.Convert(settings)

  'Save the PDF document
  document.Save("Output.pdf")
End Using
{% endhighlight %}

{% highlight UWP %}
//Excel To PDF conversion can be performed by referring .NET Standard assemblies in UWP platform
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;
  IWorkbook workbook = application.Workbooks.Create(1);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Enabling ThrowWhenExcelFileIsEmpty throws exception
  settings.ThrowWhenExcelFileIsEmpty = true;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook,settings);

  //Save the PDF document
  MemoryStream stream = new MemoryStream();
  document.Save(stream);
  Save(stream, "Output.pdf");
}

//Save the PDF stream as a file
#region Setting output location
async void Save(Stream stream, string filename)
{
  stream.Position = 0;

  StorageFile stFile;
  if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
  {
    FileSavePicker savePicker = new FileSavePicker();
    savePicker.DefaultFileExtension = ".pdf";
    savePicker.SuggestedFileName = "Output";
    savePicker.FileTypeChoices.Add("Adobe PDF Document", new List<string>() { ".pdf" });
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
  stream.Dispose();
}
{% endhighlight %}

{% highlight ASP.NET Core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  IWorkbook workbook = application.Workbooks.Create(1);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Enabling ThrowWhenExcelFileIsEmpty throws exception
  settings.ThrowWhenExcelFileIsEmpty = true;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook, settings);

  //Saving the Excel to the MemoryStream 
  MemoryStream stream = new MemoryStream();
  document.Save(stream);

  //Set the position as '0'
  stream.Position = 0;

  //Download the PDF file in the browser
  FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");
  fileStreamResult.FileDownloadName = "Output.pdf";
  return fileStreamResult;
}
{% endhighlight %}

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;
  IWorkbook workbook = application.Workbooks.Create(1);

  //Initialize XlsIORendererSettings
  XlsIORendererSettings settings = new XlsIORendererSettings();

  //Enabling ThrowWhenExcelFileIsEmpty throws exception
  settings.ThrowWhenExcelFileIsEmpty = true;

  //Initialize XlsIORenderer
  XlsIORenderer renderer = new XlsIORenderer();

  //Convert the Excel document to PDF with renderer settings
  PdfDocument document = renderer.ConvertToPDF(workbook, settings);

  //Save the PDF document to stream
  MemoryStream stream = new MemoryStream();
  document.Save(stream);
  stream.Position = 0;

  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.pdf", "application/pdf", stream);
}
{% endhighlight %}
{% endtabs %}

## Capture Warnings in Excel-to-PDF Conversion

XlsIO intentionally skips unsupported elements and substitutes unsupported fonts. The elements that were not converted and the fonts that were intentionally substituted can be raised as warnings, to decide whether to proceed the conversion with the warnings or to stop the conversion.

It is recommended to implement `IWarning` interface in a supporting class. The interface holds the properties,
*	**Type** – the element that failed to convert
*	**Description** – the description of the failed element

In addition, a decision to continue the conversion process can be done here by setting boolean value to the property `Cancel`. If `Cancel` is set to TRUE the conversion cancels, else the conversion continues.

The following code snippet shows how to capture warnings during Excel-to-PDF conversion.
{% tabs %}  

{% highlight c# %}
using Syncfusion.ExcelToPdfConverter;
using Syncfusion.Pdf;
using Syncfusion.XlsIO;

namespace CaptureWarnings
{
    class Program
    {
        static void Main(string[] args)
        {
           using(ExcelEngine excelEngine = new ExcelEngine())
           {
             IApplication application = excelEngine.Excel;
             application.DefaultVersion = ExcelVersion.Excel2013;
             IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);
           
             //Open the Excel document to convert.
             ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);
           
             //Initialize warning class to capture warnings during the conversion.
             Warning warning = new Warning();
           	
             //Initialize Excel-to-PDF converter settings.
             ExcelToPdfConverterSettings settings = new ExcelToPdfConverterSettings();
             
             //Set the warning class that is implemented.
             settings.Warning = warning;
           
             //Convert Excel document into PDF document.
             PdfDocument pdfDocument = converter.Convert(settings);
           
             //If conversion process canceled null returned.
             if(pdfDocument != null)
               //Save the PDF file.
               pdfDocument.Save("ExcelToPDF.pdf");
           }
        }
    }

    /// <summary>
    /// A supporting class that implements IWarning.
    /// </summary>
    public class Warning : IWarning
    {
        public void ShowWarning(WarningInfo warning)
        {
            //Cancel the converion process if the warning type is conditional formatting.
            if (warning.Type == WarningType.ConditionalFormatting)
                Cancel = true;

            //To view or log the warning, you can make use of warning.Description.
        }
        public bool Cancel { get; set; }
    }
}


{% endhighlight %}

{% highlight vb %}
Imports Syncfusion.ExcelToPdfConverter
Imports Syncfusion.Pdf
Imports Syncfusion.XlsIO

Namespace CaptureWarnings
    Class Program
        Private Shared Sub Main(ByVal args As String())
           Using excelEngine As ExcelEngine = New ExcelEngine()
           
               Dim application As IApplication = excelEngine.Excel
               application.DefaultVersion = ExcelVersion.Excel2013
               Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)
           
               'Open the Excel document to convert.
               Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(workbook)
           
               'Initialize warning class to capture warnings during the conversion.
               Dim warning As Warning = New Warning()
           
               'Initialize Excel-to-PDF converter settings.
               Dim settings As ExcelToPdfConverterSettings = New ExcelToPdfConverterSettings()
           
               'Set the warning class that is implemented.
               settings.Warning = warning
           
               'Convert Excel document into PDF document.
               Dim pdfDocument As PdfDocument = converter.Convert(settings)
			   
               'If conversion process canceled null returned.
               If pdfDocument IsNot Nothing Then
                  'Save the PDF file.
                  pdfDocument.Save("ExcelToPDF.pdf")
           End Using
        End Sub
    End Class

    ''' <summary>
    ''' A supporting class that implements IWarning.
    ''' </summary>
    Public Class Warning
        Inherits IWarning

        Public Sub ShowWarning(ByVal warning As WarningInfo)
            'Cancel the converion process if the warning type is conditional formatting.
            If warning.Type = WarningType.ConditionalFormatting Then Cancel = True
			
            'To view or log the warning, you can make use of warning.Description.
        End Sub

        Public Property Cancel As Boolean
    End Class
End Namespace

{% endhighlight %}

{% highlight UWP %}
//Excel To PDF conversion can be performed by referring .NET Standard assemblies in UWP platform

using Syncfusion.XlsIORenderer;
using Syncfusion.Pdf;
using Syncfusion.XlsIO;

namespace CaptureWarnings
{
    class Program
    {
        void Button_Click(Object sender, EventArgs args)
        {
            using (ExcelEngine excelEngine = new ExcelEngine())
            {
            	IApplication application = excelEngine.Excel;
            	
            	//Gets assembly
            	Assembly assembly = typeof(App).GetTypeInfo().Assembly;
            
            	//Gets input Excel document from an embedded resource collection
            	Stream excelStream = assembly.GetManifestResourceStream("Sample.xlsx");
            	
            	IWorkbook workbook = await application.Workbooks.OpenAsync(excelStream);
            	
            	//Initialize warning class to capture warnings during the conversion.
            	Warning warning = new Warning();
            
            	//Initialize XlsIO renderer.
            	XlsIORenderer renderer = new XlsIORenderer();
            	
            	//Initialize XlsIO renderer settings.
            	XlsIORendererSettings settings = new XlsIORendererSettings();
            
            	//Set the warning class that is implemented.
            	settings.Warning = warning;
              
            	//Convert Excel document into PDF document.
            	PdfDocument pdfDocument = renderer.ConvertToPDF(workbook, settings);
                
                //If conversion process canceled null returned.
                if(pdfDocument != null)
                {
            	  //Save the PDF document to stream.
            	  MemoryStream stream = new MemoryStream();
            
            	  await pdfDocument.SaveAsync(stream);
            	  Save(stream, "ExcelToPDF.pdf");
                  stream.Dispose();
                }
            	excelStream.Dispose();
            }
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
            	savePicker.DefaultFileExtension = ".pdf";
            	savePicker.SuggestedFileName = "Sample";
            	savePicker.FileTypeChoices.Add("Adobe PDF Document", new List<string>() { ".pdf" });
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
    }

    /// <summary>
    /// A supporting class that implements IWarning.
    /// </summary>
    public class Warning : IWarning
    {
        public void ShowWarning(WarningInfo warning)
        {
            //Cancel the converion process if the warning type is conditional formatting.
            if (warning.Type == WarningType.ConditionalFormatting)
                Cancel = true;

            //To view or log the warning, you can make use of warning.Description.
        }
        public bool Cancel { get; set; }
    }
}
{% endhighlight %}

{% highlight ASP.NET Core %}
using Syncfusion.XlsIORenderer;
using Syncfusion.Pdf;
using Syncfusion.XlsIO;

namespace CaptureWarnings
{
    class Program
    {
        static void Main(string[] args)
        {
           using (ExcelEngine excelEngine = new ExcelEngine())
           {
              IApplication application = excelEngine.Excel;
              
              //Open the Excel document to convert.
              FileStream excelStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
              IWorkbook workbook = application.Workbooks.Open(excelStream);
           
              //Initialize warning class to capture warnings during the conversion.
              Warning warning = new Warning();
              
              //Initialize XlsIO renderer.
              XlsIORenderer renderer = new XlsIORenderer();
              
              //Initialize XlsIO renderer settings.
              XlsIORendererSettings settings = new XlsIORendererSettings();
              
              //Set the warning class that is implemented.
              settings.Warning = warning;
             
              //Convert Excel document into PDF document.
              PdfDocument pdfDocument = renderer.ConvertToPDF(workbook, settings);
           
              //If conversion process canceled null returned.
              if(pdfDocument != null)
              {
                //Save the PDF file.
                Stream stream = new FileStream("ExcelToPDF.pdf", FileMode.Create, FileAccess.ReadWrite);
                pdfDocument.Save(stream);
                stream.Dispose();
              }
              excelStream.Dispose();              
            }
        }
    }

    /// <summary>
    /// A supporting class that implements IWarning.
    /// </summary>
    public class Warning : IWarning
    {
        public void ShowWarning(WarningInfo warning)
        {
            //Cancel the converion process if the warning type is conditional formatting.
            if (warning.Type == WarningType.ConditionalFormatting)
                Cancel = true;

            //To view or log the warning, you can make use of warning.Description.
        }
        public bool Cancel { get; set; }
    }
}
{% endhighlight %}

{% highlight Xamarin %}
using Syncfusion.XlsIORenderer;
using Syncfusion.Pdf;
using Syncfusion.XlsIO;

namespace CaptureWarnings
{
    class Program
    {
        void Button_Click(Object sender, EventArgs args)
        {
            using (ExcelEngine excelEngine = new ExcelEngine())
            {
            	IApplication application = excelEngine.Excel;
               
            	//Gets assembly
            	Assembly assembly = typeof(App).GetTypeInfo().Assembly;
            
            	//Gets input Excel document from an embedded resource collection
            	Stream excelStream = assembly.GetManifestResourceStream("Sample.xlsx");
            
            	IWorkbook workbook = application.Workbooks.Open(excelStream);
            
            	//Initialize warning class to capture warnings during the conversion.
            	Warning warning = new Warning();
            
            	//Initialize XlsIO renderer.
            	XlsIORenderer renderer = new XlsIORenderer();
            	
            	//Initialize XlsIO renderer settings.
            	XlsIORendererSettings settings = new XlsIORendererSettings();
            
            	//Set the warning class that is implemented.
            	settings.Warning = warning;
              
            	//Convert Excel document into PDF document 
            	PdfDocument pdfDocument = renderer.ConvertToPDF(workbook, settings);
            
                //If conversion process canceled null returned.
                if(pdfDocument != null)
                {
            	   //Save the PDF document to stream.
            	   MemoryStream stream = new MemoryStream();
            	   pdfDocument.Save(stream);
                   
            	   stream.Position = 0;
                   
            	   //Save the stream into pdf file
            	   if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
            	   {
            	   	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("ExcelToPDF.pdf", "application/pdf", stream);
            	   }
            	   else
            	   {
            	   	Xamarin.Forms.DependencyService.Get<ISave>().Save("ExcelToPDF.pdf", "application/pdf", stream);
            	   }
                   stream.Dispose();
                }
            	excelStream.Dispose();
            }
        }
    }

    /// <summary>
    /// A supporting class that implements IWarning.
    /// </summary>
    public class Warning : IWarning
    {
        public void ShowWarning(WarningInfo warning)
        {
            //Cancel the converion process if the warning type is conditional formatting.
            if (warning.Type == WarningType.ConditionalFormatting)
                Cancel = true;

            //To view or log the warning, you can make use of warning.Description.
        }
        public bool Cancel { get; set; }
    }
}
{% endhighlight %}

{% endtabs %}

