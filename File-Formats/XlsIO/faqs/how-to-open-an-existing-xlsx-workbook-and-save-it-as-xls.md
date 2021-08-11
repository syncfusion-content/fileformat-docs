---
title: How to open an existing XLSX workbook and save it as XLS | Syncfusion
description: Code example to open an existing XLSX workbook and save it as XLS using Syncfusion .NET Excel library (XlsIO).
platform: File-formats
control: XlsIO
documentation: UG
---

# How to open an existing XLSX workbook and save it as XLS?

You can open and save an existing .xlsx file to the .xls file by using XlsIO. The following code snippet illustrates this.

{% tabs %}  

{% highlight c# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Excel2013;

    //Open an existing Excel 2013 file
    IWorkbook workbook = excelEngine.Excel.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

    //Save it as "Excel 97 to 2003" format
    workbook.Version = ExcelVersion.Excel97to2003;

    workbook.SaveAs("Output.xls");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Excel2013

    'Open an existing Excel 2013 file
    Dim workbook As IWorkbook = excelEngine.Excel.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

    'Save it as "Excel 97 to 2003" format
    workbook.Version = ExcelVersion.Excel97to2003

    workbook.SaveAs("Output.xls")
End Using
{% endhighlight %}

{% highlight UWP %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    
    //Open an existing Excel 2013 file
    Stream inputStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
    IWorkbook workbook = await application.Workbooks.OpenAsync(inputStream, ExcelOpenType.Automatic);

    //Save it as "Excel 97 to 2003" format
    FileSavePicker savePicker = new FileSavePicker();
    savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
    savePicker.SuggestedFileName = "Output";
    savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xls" });
    StorageFile storageFile = await savePicker.PickSaveFileAsync();
    await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight ASP.NET Core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;

    //Open an existing Excel 2013 file
    FileStream inputStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
    IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelOpenType.Automatic);

    //Save it as "Excel 97 to 2003" format
    FileStream outputStream = new FileStream("Output.xls", FileMode.OpenOrCreate, FileAccess.ReadWrite);
    workbook.SaveAs(outputStream);

    workbook.Close();
    excelEngine.Dispose();
}
{% endhighlight %}

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;

    //Open an existing Excel 2013 file
    Assembly assembly = typeof(App).GetTypeInfo().Assembly;
    Stream fileStream = assembly.GetManifestResourceStream("App.Sample.xlsx");
    IWorkbook workbook = application.Workbooks.Open(fileStream);

    //Save it as "Excel 97 to 2003" format
    MemoryStream stream = new MemoryStream();
    workbook.SaveAs(stream);

    stream.Position = 0;

    //Save the stream as a file in the device and invoke it for viewing
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xls", "application/vnd.ms-excel", stream);
}
{% endhighlight %}

  {% endtabs %}  

N> Workbook must be saved in appropriate version, failing in this leads to file corruption.

## See Also

* [How to open an Excel file from stream?](faqs/how-to-open-an-excel-file-from-stream)
* [How to open an Excel 2013 Macro Enabled Template?](faqs/how-to-open-an-excel-2013-macro-enabled-template)
* [How to create and open Excel Template files by using XlsIO?](faqs/how-to-create-and-open-excel-template-files-by-using-xlsio)
* [How to save a file to stream?](faqs/how-to-save-a-file-to-stream)
* [How to merge excel files from more than one workbook to a single file?](faqs/how-to-merge-excel-files-from-more-than-one-workbook-to-a-single-file)
* [How to opening an existing workbook?](https://help.syncfusion.com/file-formats/xlsio/loading-and-saving-workbook#opening-an-existing-workbook)
* [How to save an Excel workbook to file system?](https://help.syncfusion.com/file-formats/xlsio/loading-and-saving-workbook#saving-a-excel-workbook-to-file-system)
