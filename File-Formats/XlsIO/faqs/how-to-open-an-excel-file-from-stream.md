---
title: How to open an Excel file from stream | XlsIO | Syncfusion
description: This page demonstrates with an example to open an Excel file from stream using Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# How to open an Excel file from stream?

XlsIO provides support for opening a file that is stored as a stream. The following code snippet illustrates this.

{% tabs %}  

{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Excel2013;

    //Opening a File from a Stream
    FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);

    IWorkbook workbook = application.Workbooks.Open(fileStream);

    workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Excel2013

    'Opening a File from a Stream
    Dim fileStream As New FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite)

    Dim workbook As IWorkbook = application.Workbooks.Open(fileStream)

    workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;

    //Opening a File from a Stream
    Stream inputStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
    IWorkbook workbook = await application.Workbooks.OpenAsync(inputStream, ExcelOpenType.Automatic);
	
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

    //Opening a File from a Stream
    FileStream inputStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
    IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelOpenType.Automatic);

    FileStream stream = new FileStream("Output.xlsx", FileMode.OpenOrCreate, FileAccess.ReadWrite);
    workbook.SaveAs(stream);

    workbook.Close();
    excelEngine.Dispose();
}

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;

    //Opening a File from a Stream
    Assembly assembly = typeof(App).GetTypeInfo().Assembly;
    Stream fileStream = assembly.GetManifestResourceStream("App.Sample.xlsx");
    IWorkbook workbook = application.Workbooks.Open(fileStream);
	
    MemoryStream stream = new MemoryStream();
    workbook.SaveAs(stream);

    stream.Position = 0;

    //Save the stream as a file in the device and invoke it for viewing
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", stream);
}
{% endhighlight %}

  {% endtabs %}  

## See Also

* [How to open an Excel 2013 Macro Enabled Template?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-open-an-excel-2013-macro-enabled-template)
* [How to create and open Excel Template files by using XlsIO?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-create-and-open-excel-template-files-by-using-xlsio)
* [How to open an existing workbook from stream?](https://help.syncfusion.com/file-formats/xlsio/loading-and-saving-workbook#opening-an-existing-workbook-from-stream)
* [How to open a CSV file?](https://help.syncfusion.com/file-formats/xlsio/working-with-excel-worksheet#open-a-csv-file)
* [How to open an existing XLSX workbook and save it as XLS?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-open-an-existing-xlsx-workbook-and-save-it-as-xls)
* [How to resolve the File does not contain workbook stream error in Syncfusion.XlsIO.Base.dll?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-resolve-the-file-does-not-contain-workbook-stream-error)
* [How to resolve Excel cannot open the file filename.xlsx... error?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-resolve-excel-cannot-open-the-file-because-the-file-format-for-the-file-extension-is-not-valid)
* [How to save a file to stream?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-save-a-file-to-stream)
* [How to merge excel files from more than one workbook to a single file?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-merge-excel-files-from-more-than-one-workbook-to-a-single-file)
* [Does XlsIO support Excel files with macros that are digitally signed?](https://help.syncfusion.com/file-formats/xlsio/faqs/does-xlsio-support-excel-files-with-macros-that-are-digitally-signed)
* [How does Excel file with uninstalled fonts is converted to PDF/Image?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-does-excel-file-with-uninstalled-fonts-is-converted-to-pdf-image)

