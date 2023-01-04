---
title: How to open an Excel 2013 Macro Enabled Template | XlsIO | Syncfusion
description: Code example to open an Excel 2013 Macro Enabled Template using Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# How to open an Excel 2013 Macro Enabled Template?

You can open and save an Excel 2013 Macro Enabled Template to XLSM (Excel 2013 Macro Enabled Document) format. The following code snippet illustrates this.

{% tabs %}  

{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  //Open an existing XLTM file
  IWorkbook workbook = application.Workbooks.Open("Sample.xltm", ExcelOpenType.Automatic);

  //Save the file as XLSM
  workbook.SaveAs("Output.xlsm");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013

  'Open an existing XLTM file
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xltm", ExcelOpenType.Automatic)

  'Save the file as XLSM
  workbook.SaveAs("Output.xlsm")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;

  //Open an existing XLTM file
  Stream inputStream = new FileStream("Sample.xltm", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = await application.Workbooks.OpenAsync(inputStream, ExcelOpenType.Automatic);

  //Save the file as XLSM
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "Output";
  savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsm" });
  StorageFile storageFile = await savePicker.PickSaveFileAsync();
  await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;

  //Open an existing XLTM file
  FileStream inputStream = new FileStream("Sample.xltm", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelOpenType.Automatic);

  //Save the file as XLSM
  FileStream outputStream = new FileStream("Output.xlsm", FileMode.OpenOrCreate, FileAccess.ReadWrite);
  workbook.SaveAs(outputStream);
  workbook.Close();
  excelEngine.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;

  //Open an existing XLTM file
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream fileStream = assembly.GetManifestResourceStream("App.Sample.xltm");
  IWorkbook workbook = application.Workbooks.Open(fileStream);

  //Save the file as XLSM
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream);

  stream.Position = 0;

  //Save the stream as a file in the device and invoke it for viewing
  Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsm", "application/vnd.ms-excel.sheet.macroEnabled.12", stream);
}
{% endhighlight %}
{% endtabs %}  

## See Also

* [How to check whether an Excel document contains macro?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-check-whether-an-excel-document-contains-macro)
* [Does XlsIO support Excel files with macros that are digitally signed?](https://help.syncfusion.com/file-formats/xlsio/faqs/does-xlsio-support-excel-files-with-macros-that-are-digitally-signed)
* [Does XlsIO support password protected macro in the Excel documents?](https://help.syncfusion.com/file-formats/xlsio/faqs/does-xlsio-support-password-protected-macro-in-the-excel-documents)
* [How to create a macro?](https://help.syncfusion.com/file-formats/xlsio/working-with-macros#creating-a-macro)
* [How to edit a macro?](https://help.syncfusion.com/file-formats/xlsio/working-with-macros#editing-a-macro)
* [How to remove macros?](https://help.syncfusion.com/file-formats/xlsio/working-with-macros#removing-macros)
