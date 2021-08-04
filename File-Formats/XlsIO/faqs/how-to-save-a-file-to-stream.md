---
title: How to save a file to stream | XlsIO | Syncfusion
description: This page demonstrates with an example to save a file to stream using Syncfusion .NET Excel library (XlsIO).
platform: File-formats
control: XlsIO
documentation: UG
---

# How to save a file to stream?

XlsIO provides support to save a workbook to a .NET stream. The following code snippet illustrates this.

{% tabs %}  

{% highlight c# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Excel2013;

    IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

    //Save the workbook to stream

    FileStream fileStream = new FileStream("Output.xlsx", FileMode.Create, FileAccess.ReadWrite, FileShare.ReadWrite);

    workbook.SaveAs(fileStream);
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Excel2013

    Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

    'Save the workbook to stream

    Dim fileStream As New FileStream("Output.xlsx", FileMode.Create, FileAccess.ReadWrite, FileShare.ReadWrite)

    workbook.SaveAs(fileStream)
End Using
{% endhighlight %}

{% highlight UWP %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    Stream inputStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
    IWorkbook workbook = await application.Workbooks.OpenAsync(inputStream, ExcelOpenType.Automatic);

    //Save the workbook to stream
    FileStream fileStream = new FileStream("Output.xlsx", FileMode.OpenOrCreate, FileAccess.ReadWrite);
    await workbook.SaveAsAsync(fileStream);
}
{% endhighlight %}

{% highlight ASP.NET Core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    FileStream inputStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
    IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelOpenType.Automatic);

    //Save the workbook to stream
    FileStream fileStream = new FileStream("Output.xlsx", FileMode.OpenOrCreate, FileAccess.ReadWrite);
    workbook.SaveAs(fileStream);

    workbook.Close();
    excelEngine.Dispose();
}
{% endhighlight %}

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    Assembly assembly = typeof(App).GetTypeInfo().Assembly;
    Stream inputStream = assembly.GetManifestResourceStream("App.Sample.xlsx");
    IWorkbook workbook = application.Workbooks.Open(inputStream);

    //Save the workbook to stream
    MemoryStream stream = new MemoryStream();
    workbook.SaveAs(stream);

    stream.Position = 0;

    //Save the stream as a file in the device and invoke it for viewing
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", stream);
}
{% endhighlight %}

  {% endtabs %}  

## See Also

* [How to open an Excel file from stream?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-open-an-excel-file-from-stream)
[How to save an Excel workbook to stream?](https://help.syncfusion.com/file-formats/xlsio/loading-and-saving-workbook#saving-a-excel-workbook-to-stream)
* [How to resolve the File does not contain workbook stream error in Syncfusion.XlsIO.Base.dll?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-resolve-the-file-does-not-contain-workbook-stream-error)
* [How to resolve Excel cannot open the file filename.xlsx... error?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-resolve-excel-cannot-open-the-file-because-the-file-format-for-the-file-extension-is-not-valid)
* [How to open an existing XLSX workbook and save it as XLS?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-open-an-existing-xlsx-workbook-and-save-it-as-xls)
* [How to merge excel files from more than one workbook to a single file?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-merge-excel-files-from-more-than-one-workbook-to-a-single-file)
* [Does XlsIO support Excel files with macros that are digitally signed?](https://help.syncfusion.com/file-formats/xlsio/faqs/does-xlsio-support-excel-files-with-macros-that-are-digitally-signed)
* [How does Excel file with uninstalled fonts is converted to PDF/Image?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-does-excel-file-with-uninstalled-fonts-is-converted-to-pdf-image)
