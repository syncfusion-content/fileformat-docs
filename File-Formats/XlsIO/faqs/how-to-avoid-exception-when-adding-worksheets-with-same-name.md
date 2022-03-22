---
title: Avoid exception when adding worksheets with same name | Syncfusion
description: This page helps to avoid exception when adding worksheets with same name in Syncfusion .NET Excel library (XlsIO).
platform: File-formats
control: XlsIO
documentation: UG
---

# How to avoid exception when adding worksheets with same name?

Microsoft Excel throws exception when adding worksheet with existing worksheet name in a workbook and XlsIO does the same. But in some case, if you want to add worksheets with the same name using XlsIO then you can avoid the exception in XlsIO by setting IApplication IgnoreSheetNameException property as true.

The following code snippet shows how to add two worksheets with same name in a workbook.

{% tabs %}  
{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);

  //Set IgnoreSheetNameException property as true 
  application.IgnoreSheetNameException = true;

  //Create worksheets with same name
  IWorksheet sheet_1 = workbook.Worksheets.Create("Sheet");
  IWorksheet sheet_2 = workbook.Worksheets.Create("Sheet");

  string fileName = "Output.xlsx";
  workbook.SaveAs(fileName);
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)

  ’Set IgnoreSheetNameException property as true
  application.IgnoreSheetNameException = true
  
  ‘Create worksheets with same name
  Dim sheet_1 As IWorksheet = workbook.Worksheets.Create("Sheet")
  Dim sheet_2 As IWorksheet = workbook.Worksheets.Create("Sheet")

  Dim fileName As String = "Output.xlsx"
  workbook.SaveAs(fileName)
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);

  //Set IgnoreSheetNameException property as true 
  application.IgnoreSheetNameException = true;

  //Create worksheets with same name
  IWorksheet sheet_1 = workbook.Worksheets.Create("Sheet");
  IWorksheet sheet_2 = workbook.Worksheets.Create("Sheet");

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
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);

  //Set IgnoreSheetNameException property as true 
  application.IgnoreSheetNameException = true;

  //Create worksheets with same name
  IWorksheet sheet_1 = workbook.Worksheets.Create("Sheet");
  IWorksheet sheet_2 = workbook.Worksheets.Create("Sheet");

  //Saving the workbook as stream
  FileStream file = new FileStream("Output.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(file);
  file.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);

  //Set IgnoreSheetNameException property as true 
  application.IgnoreSheetNameException = true;

  //Create worksheets with same name
  IWorksheet sheet_1 = workbook.Worksheets.Create("Sheet");
  IWorksheet sheet_2 = workbook.Worksheets.Create("Sheet");

  //Saving the workbook as stream
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the document as file and view the saved document

  //The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

  if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
  {
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().SaveAndView(("Output.xlsx", "application/msexcel", stream);
  }
  else
  {
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", stream);
  }
}
{% endhighlight %}
{% endtabs %}

## See Also

* [How to overcome UnauthorizedAccessException?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-overcome-unauthorizedaccessexception)
* [How to overcome StackOverflow exception with IWorksheet Calculate()?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-overcome-stackoverflow-exception-with-iworksheet-calculate)
* [What are the known exceptions of XlsIO?](https://help.syncfusion.com/file-formats/xlsio/known-exceptions)
* [How to create a named range in Excel?](https://help.syncfusion.com/file-formats/xlsio/migrate-from-office-automation-to-syncfusion-xlsio/create-named-range-in-excel)
* [How to use Named Ranges with XlsIO?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-use-named-ranges-with-xlsio)

