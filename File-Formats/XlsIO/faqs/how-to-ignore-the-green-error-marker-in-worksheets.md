---
title: Ignore green error marker in worksheets | XlsIo | Syncfusion
description: This page demonstrates how to ignore the green error marker in worksheets using Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# How to ignore the green error marker in worksheets?

When there exists data that are of different formats, the error marker appears in cells. In XlsIO You can ignore this by using [IgnoreErrorOptions](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IRange.html#Syncfusion_XlsIO_IRange_IgnoreErrorOptions) property. The following code snippet illustrate this.

{% tabs %} 
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Ignore Error Options
  worksheet.Range["B3"].IgnoreErrorOptions = ExcelIgnoreError.All;

  workbook.SaveAs("IgnoreGreenError.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Ignore Error Options
  worksheet.Range("B3").IgnoreErrorOptions = ExcelIgnoreError.All

  workbook.SaveAs("IgnoreGreenError.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  Stream inputStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = await application.Workbooks.OpenAsync(inputStream, ExcelOpenType.Automatic);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Ignore Error Options
  worksheet.Range["B3"].IgnoreErrorOptions = ExcelIgnoreError.All;

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "IgnoreGreenError";
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
  FileStream inputStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelOpenType.Automatic);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Ignore Error Options
  worksheet.Range["B3"].IgnoreErrorOptions = ExcelIgnoreError.All;

  FileStream stream = new FileStream("IgnoreGreenError.xlsx", FileMode.OpenOrCreate, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  workbook.Close();
  excelEngine.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream fileStream = assembly.GetManifestResourceStream("App.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Ignore Error Options
  worksheet.Range["B3"].IgnoreErrorOptions = ExcelIgnoreError.All;

  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);
  stream.Position = 0;
  //Save the stream as a file in the device and invoke it for viewing
  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("IgnoreGreenError.xlsx", "application/msexcel", stream);
}
{% endhighlight %}
{% endtabs %}  

## See Also

* [How to ignore print areas set in a worksheet?](how-to-ignore-print-areas-set-in-a-worksheet)
* [How to resolve Excel cannot open the file filename.xlsx... error?](how-to-resolve-excel-cannot-open-the-file-because-the-file-format-for-the-file-extension-is-not-valid)
* [How to resolve the File does not contain workbook stream error in Syncfusion.XlsIO.Base.dll?](how-to-resolve-the-file-does-not-contain-workbook-stream-error)
