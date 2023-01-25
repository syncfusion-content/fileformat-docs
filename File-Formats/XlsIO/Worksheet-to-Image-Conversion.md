---
title: Worksheet to Image conversion in Excel Library | Syncfusion
description: Learn here all about worksheet to image conversion feature of Syncfusion Excel (XlsIO) Library and more.
platform: file-formats
control: XlsIO
documentation: UG
---

# Worksheet to Image conversion in Excel Library

## Assemblies Required

Refer to the following links for assemblies/nuget packages required based on platforms to convert the worksheet to image.

* [Assemblies Information](https://help.syncfusion.com/file-formats/xlsio/assemblies-required#converting-excel-worksheet-to-image) 
* [NuGet Information](https://help.syncfusion.com/file-formats/xlsio/nuget-packages-required#converting-excel-worksheet-to-image)

## Convert as bitmap

The following code shows how to convert the specified range of rows and columns in the worksheet to bitmap.

{% tabs %}
{% highlight c# tabtitle="C#" %}
// Convert as bitmap
Image image = sheet.ConvertToImage(1, 1, 10, 20);
image.Save("Sample.png", ImageFormat.Png);
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Convert as bitmap
Dim image As Image = sheet.ConvertToImage(1, 1, 10, 20)
image.Save("Sample.png", ImageFormat.Png)
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Worksheet To Image conversion can be performed by referring .NET Standard assemblies in UWP platform.

// Initialize XlsIORenderer
application.XlsIORenderer = new XlsIORenderer();

//Create a new memory stream to save the image
Stream stream = new MemoryStream();

//Convert worksheet to image and save it to stream.
worksheet.ConvertToImage(1, 1, 10, 20, stream);
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
// Initialize XlsIORenderer
application.XlsIORenderer = new XlsIORenderer();

//Create a new memory stream to save the image
Stream stream = new MemoryStream();

//Convert worksheet to image and save it to stream.
worksheet.ConvertToImage(1, 1, 10, 20, stream);
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
// Initialize XlsIORenderer
application.XlsIORenderer = new XlsIORenderer();

//Create a new memory stream to save the image
Stream stream = new MemoryStream();

//Convert worksheet to image and save it to stream.
worksheet.ConvertToImage(1, 1, 10, 20, stream);
{% endhighlight %}
{% endtabs %}  

## Save as stream

The following code snippet shows how to save a sheet as stream.

{% tabs %}
{% highlight c# tabtitle="C#" %}
// Converts and save as stream
MemoryStream stream = new MemoryStream();
sheet.ConvertToImage(1, 1, 10, 20, ImageType.Metafile, stream);
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Converts and save as stream
Dim stream As MemoryStream = New MemoryStream()
sheet.ConvertToImage(1, 1, 10, 20, ImageType.Metafile, stream)
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Worksheet To Image conversion can be performed by referring .NET Standard assemblies in UWP platform.

// Initialize XlsIORenderer
application.XlsIORenderer = new XlsIORenderer();

//Create a new memory stream to save the image
Stream stream = new MemoryStream();

//Convert worksheet to image and save it to stream.
worksheet.ConvertToImage(1, 1, 10, 20, stream);
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
// Initialize XlsIORenderer
application.XlsIORenderer = new XlsIORenderer();

// Converts and save as stream
MemoryStream stream = new MemoryStream();
sheet.ConvertToImage(1, 1, 10, 20, stream);
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
// Initialize XlsIORenderer
application.XlsIORenderer = new XlsIORenderer();

// Converts and save as stream
MemoryStream stream = new MemoryStream();
sheet.ConvertToImage(1, 1, 10, 20, stream);
{% endhighlight %}
{% endtabs %}  

The complete code snippet of the previous options is given below.

{% tabs %}
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);
  IWorksheet sheet = workbook.Worksheets[0];

  //Convert as bitmap
  Image image = sheet.ConvertToImage(1, 1, 10, 20);

  image.Save("Sample.png", ImageFormat.Png);

  //Converts and save as stream
  MemoryStream stream = new MemoryStream();
  sheet.ConvertToImage(1, 1, 10, 20, ImageType.Metafile, stream);

  //Save the workbook to disk
  workbook.SaveAs("Sample.xlsx");

  //No exception will be thrown if there are unsaved workbooks
  excelEngine.ThrowNotSavedOnDestroy = false;
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Open("sample.xlsx", ExcelOpenType.Automatic)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Convert as bitmap
  Dim image As Image = worksheet.ConvertToImage(1, 1, 10, 20)

  image.Save("Sample.png", ImageFormat.Png)

  'Converts and save as stream
  Dim stream As MemoryStream = New MemoryStream()
  worksheet.ConvertToImage(1, 1, 10, 20, ImageType.Metafile, stream)

  'Save the workbook to disk
  workbook.SaveAs("Sample.xlsx")

  'No exception will be thrown if there are unsaved workbooks.
  excelEngine.ThrowNotSavedOnDestroy = False
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Worksheet To Image conversion can be performed by referring .NET Standard assemblies in UWP platform.

using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;

  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from an embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("WorksheetToImage.Sample.xlsx");

  IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelOpenType.Automatic);
  IWorksheet sheet = workbook.Worksheets[0];

  //Initialize XlsIORenderer
  application.XlsIORenderer = new XlsIORenderer();

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Output";
  savePicker.FileTypeChoices.Add("Image Files", new List<string>() { ".png",".jpeg",".jpg" });

  //Creates a storage file from the FileSavePicker
  StorageFile storageFile = await savePicker.PickSaveFileAsync();

  //Converts and save to stream
  var file = await storageFile.OpenAsync(FileAccessMode.ReadWrite);
  Stream stream = file.AsStreamForWrite();
  sheet.ConvertToImage(1, 1, 10, 20, stream);
  await file.FlushAsync();
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Open(File.OpenRead("Sample.xlsx"), ExcelOpenType.Automatic);
  IWorksheet sheet = workbook.Worksheets[0];

  //Initialize XlsIORenderer
  application.XlsIORenderer = new XlsIORenderer();  

  //Converts and save as stream
  MemoryStream stream = new MemoryStream();
  sheet.ConvertToImage(1, 1, 10, 20, stream);

  //Close and Dispose
  workbook.Close();
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  //Gets assembly
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;

  //Gets input Excel document from an embedded resource collection
  Stream inputStream = assembly.GetManifestResourceStream("WorksheetToImage.Sample.xlsx");

  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet sheet = workbook.Worksheets[0];

  //Initializing XlsIORenderer
  application.XlsIORenderer = new XlsIORenderer();

  //Converts and save to stream.
  MemoryStream stream = new MemoryStream();
  sheet.ConvertToImage(1, 1, 10, 20, stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies among Windows Phone, Android, and iOS platforms. Refer to the xlsio/xamarin section for respective code samples.
  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView("Test.png", "image/png", stream);
  }
  else
  {
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Test.png", "image/png", stream);
  }
}
{% endhighlight %}
{% endtabs %} 

A complete working example to convert Excel worksheet to image in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Worksheet%20to%20Image/Worksheet%20to%20Image). 

N> 1. Instance of [XlsIORenderer](https://help.syncfusion.com/cr/aspnetcore-js2/Syncfusion.XlsIORenderer.XlsIORenderer.html) class is mandatory to convert the worksheet to image using .NET Standard assemblies.
N> 2. In .NET Standard, the Image format and quality can be specified using the **ExportImageOptions** class. By default the [ImageFormat](https://help.syncfusion.com/cr/file-formats/Syncfusion.Drawing.ImageFormat.html) is set to PNG and [ScalingMode](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ScalingMode.html) is set to Best.
N> 3. Worksheet to image conversion is supported from .NET Framework 2.0 and .NET Standard 1.4 onwards.

**Non****-****Supported** **Features****:**

* Subscript/Superscript
* Shrink to fit
* Shapes (except TextBox shape and Image)
* Complex conditional formatting
* Gradient fill is partially supported