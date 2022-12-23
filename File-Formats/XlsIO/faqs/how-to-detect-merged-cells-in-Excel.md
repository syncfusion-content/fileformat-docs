---
title: How to detect merged cells in Excel | XlsIO | Syncfusion
description: This page explains how to detect merged cells in an Excel document using Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# How to detect merged cells in Excel?

The merged cells in an Excel worksheet can be detected through [MergedCells](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorksheet.html#Syncfusion_XlsIO_IWorksheet_MergedCells) of IWorksheet. The following complete code snippet explains this.

{% tabs %} 
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
  IWorksheet worksheet = workbook.Worksheets[0];

  //Create a new worksheet
  IWorksheet mergedCells = workbook.Worksheets.Create("MergedCells");

  //Get the list of merged cells
  for (int pos = 0; pos < worksheet.MergedCells.Length; pos++)
  {
    mergedCells.Range["A" + (pos+1).ToString()].Text = (pos+1).ToString()+"th Merged region = "+ worksheet.MergedCells[pos].Address;
  }

  //Autofit the used range
  mergedCells.UsedRange.AutofitColumns();

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = ExcelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Create a new worksheet
  Dim mergedCells As IWorksheet = workbook.Worksheets.Create("MergedCells")

  'Get the list of merged cells
  For pos As Integer = 0 To worksheet.MergedCells.Length - 1 Step 1
    mergedCells.Range("A" + (pos + 1).ToString()).Text = (pos + 1).ToString() + "th Merged region = " + worksheet.MergedCells(pos).Address
  Next

  'Autofit the used range
  mergedCells.UsedRange.AutofitColumns()

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

  //Create a new worksheet
  IWorksheet mergedCells = workbook.Worksheets.Create("MergedCells");

  //Get the list of merged cells
  for (int pos = 0; pos < worksheet.MergedCells.Length; pos++)
  {
    mergedCells.Range["A" + (pos + 1).ToString()].Text = (pos + 1).ToString() + "th Merged region = " + worksheet.MergedCells[pos].Address;
  }

  //Autofit the used range
  mergedCells.UsedRange.AutofitColumns();

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

  //Create a new worksheet
  IWorksheet mergedCells = workbook.Worksheets.Create("MergedCells");

  //Get the list of merged cells
  for (int pos = 0; pos < worksheet.MergedCells.Length; pos++)
  {
    mergedCells.Range["A" + (pos + 1).ToString()].Text = (pos + 1).ToString() + "th Merged region = " + worksheet.MergedCells[pos].Address;
  }

  //Autofit the used range
  mergedCells.UsedRange.AutofitColumns();

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
  Stream inputStream = assembly.GetManifestResourceStream("XlsIOSample.Sample.xlsx");
  IWorkbook workbook = application.Workbooks.Open(inputStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Create a new worksheet
  IWorksheet mergedCells = workbook.Worksheets.Create("MergedCells");

  //Get the list of merged cells
  for (int pos = 0; pos < worksheet.MergedCells.Length; pos++)
  {
    mergedCells.Range["A" + (pos + 1).ToString()].Text = (pos + 1).ToString() + "th Merged region = " + worksheet.MergedCells[pos].Address;
  }

  //Autofit the used range
  mergedCells.UsedRange.AutofitColumns();

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
