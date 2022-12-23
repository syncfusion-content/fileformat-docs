---
title: Hide the summary rows and columns using XlsIO | Syncfusion
description: This page shows how to hide the summary rows and columns using Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# How to hide the summary rows and columns using XlsIO?

You can hide the summary rows and columns by using the **IsSummaryRowBelow** and **IsSummaryColumnRight** properties. The following code snippet illustrates this.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Hide the summary rows at the bottom.
  worksheet.PageSetup.IsSummaryRowBelow = false;

  //Hide the summary columns to the right.
  worksheet.PageSetup.IsSummaryColumnRight = false;

  workbook.SaveAs("SuppressRowsColumns.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Hide the summary rows at the bottom.
  worksheet.PageSetup.IsSummaryRowBelow = False

  'Suppress the summary columns to the right.
  worksheet.PageSetup.IsSummaryColumnRight = False

  workbook.SaveAs("SuppressRowsColumns.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  Stream inputStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = await application.Workbooks.OpenAsync(inputStream, ExcelOpenType.Automatic);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Hide the summary rows at the bottom
  worksheet.PageSetup.IsSummaryRowBelow = false;

  //Hide the summary columns to the right
  worksheet.PageSetup.IsSummaryColumnRight = false;

  //Initializes FileSavePicker
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "SuppressRowsColumns";
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

  //Hide the summary rows at the bottom
  worksheet.PageSetup.IsSummaryRowBelow = false;

  //Hide the summary columns to the right
  worksheet.PageSetup.IsSummaryColumnRight = false;

  FileStream stream = new FileStream("SuppressRowsColumns.xlsx", FileMode.OpenOrCreate, FileAccess.ReadWrite);
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

  //Hide the summary rows at the bottom
  worksheet.PageSetup.IsSummaryRowBelow = false;

  //Hide the summary columns to the right
  worksheet.PageSetup.IsSummaryColumnRight = false;

  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);
  stream.Position = 0;
  //Save the stream as a file in the device and invoke it for viewing
  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("SuppressRowsColumns.xlsx", "application/msexcel", stream);
}
{% endhighlight %}
{% endtabs %}  

## See Also

* [What is the maximum range of Rows and Columns?](https://help.syncfusion.com/file-formats/xlsio/faqs/what-is-the-maximum-range-of-rows-and-columns)
* [How to unfreeze the rows and columns in XlsIO?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-unfreeze-the-rows-and-columns-in-xlsio)
* [How to sort two or more columns in a pivot table?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-sort-two-or-more-columns-in-a-pivot-table)
* [How to hide Excel worksheets?](https://help.syncfusion.com/file-formats/xlsio/migrate-from-office-automation-to-syncfusion-xlsio/hide-excel-worksheets)
* [How to show or hide rows and columns?](https://help.syncfusion.com/file-formats/xlsio/worksheet-rows-and-columns-manipulation#show-or-hide-rows-and-columns)
* [How to show or hide specific range?](https://help.syncfusion.com/file-formats/xlsio/worksheet-rows-and-columns-manipulation#show-or-hide-specific-range)
