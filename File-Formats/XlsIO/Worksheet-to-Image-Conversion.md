---
title: Worksheet to Image conversion
description: Briefs about Worksheet to Image conversion in XlsIO
platform: File-formats
control: XlsIO
documentation: UG
---

# Worksheet to Image conversion

## Convert as bitmap

The following code shows how to convert the specified range of rows and columns in the worksheet to bitmap.

{% tabs %}
{% highlight c# %}
// Convert as bitmap
Image image = sheet.ConvertToImage(1, 1, 10, 20);
image.Save("Sample.png", ImageFormat.Png);
{% endhighlight %}

{% highlight vb %}
'Convert as bitmap
Dim image As Image = sheet.ConvertToImage(1, 1, 10, 20)
image.Save("Sample.png", ImageFormat.Png)
{% endhighlight %}

{% highlight UWP %}
//Note that Worksheet To Image conversion in UWP can be performed by referring NetStandard assemblies only.
// Initialize XlsIORenderer
application.XlsIORenderer = new XlsIORenderer();

//Create a new memory stream to save the image
Stream stream = new MemoryStream();

//Convert worksheet to image and save it to stream.
worksheet.ConvertToImage(1, 1, 10, 20, stream);
{% endhighlight %}

{% highlight asp.net core %}
// Initialize XlsIORenderer
application.XlsIORenderer = new XlsIORenderer();

//Create a new memory stream to save the image
Stream stream = new MemoryStream();

//Convert worksheet to image and save it to stream.
worksheet.ConvertToImage(1, 1, 10, 20, stream);
{% endhighlight %}

{% highlight Xamarin %}
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
{% highlight c# %}
// Converts and save as stream
MemoryStream stream = new MemoryStream();
sheet.ConvertToImage(1, 1, 10, 20, ImageType.Metafile, stream);
{% endhighlight %}

{% highlight vb %}
'Converts and save as stream
Dim stream As MemoryStream = New MemoryStream()
sheet.ConvertToImage(1, 1, 10, 20, ImageType.Metafile, stream)
{% endhighlight %}

{% highlight UWP %}
//Note that Worksheet To Image conversion in UWP can be performed by referring NetStandard assemblies only.
// Initialize XlsIORenderer
application.XlsIORenderer = new XlsIORenderer();

//Create a new memory stream to save the image
Stream stream = new MemoryStream();

//Convert worksheet to image and save it to stream.
worksheet.ConvertToImage(1, 1, 10, 20, stream);
{% endhighlight %}

{% highlight asp.net core %}
// Initialize XlsIORenderer
application.XlsIORenderer = new XlsIORenderer();

// Converts and save as stream
MemoryStream stream = new MemoryStream();
sheet.ConvertToImage(1, 1, 10, 20, stream);
{% endhighlight %}

{% highlight Xamarin %}
// Initialize XlsIORenderer
application.XlsIORenderer = new XlsIORenderer();

// Converts and save as stream
MemoryStream stream = new MemoryStream();
sheet.ConvertToImage(1, 1, 10, 20, stream);
{% endhighlight %}
{% endtabs %}  

The complete code snippet of the previous options is shown as follows.

{% tabs %}
{% highlight c# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
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

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
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

{% highlight UWP %}
//Note that Worksheet To Image conversion in UWP can be performed by referring NetStandard assemblies only.
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

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

{% highlight asp.net core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
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

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;

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
      DependencyService.Get<ISaveWindowsPhone>()
          .Save("Test.png", "image/png", stream);
  else
      DependencyService.Get<ISave>().Save("Test.png", "image/png", stream);
}
{% endhighlight %}
{% endtabs %}  

**Note****:**
In ASP.NET Core, UWP and Xamarin the Image format and quality can be specified using the ExportImageOptions Class. Creating an object for ExportImageOptions and 
passing the same as a parameter in the ConvertToImage method results image in the required quality and image format. By default the ImageFormat is set to 
PNG and ScalingMode is set to Best.

**Non****-****Supported** **Features****:**

* Subscript/Superscript
* Shrink to fit
* Shapes (except TextBox shape and Image)
* Complex conditional formatting
* Gradient fill is partially supported