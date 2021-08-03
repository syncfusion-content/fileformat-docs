---
title: How to set or format a Header/Footer? | XlsIO | Syncfusion
description: This page explains with an example to set or format a Header/Footer using Syncfusion .NET Excel library (XlsIO).
platform: File-formats
control: XlsIO
documentation: UG
---

# How to set or format a Header/Footer?

Script commands are used to set header/ footer formatting. The following code snippet illustrate this. For more information on formatting the string, see [Inserting and Formatting Text in Headers and Footers](https://docs.microsoft.com/en-us/previous-versions/office/developer/office-2007/bb225426(v=office.12))

{% tabs %}  

{% highlight c# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Excel2013;

    IWorkbook workbook = application.Workbooks.Create(1);

    IWorksheet worksheet = workbook.Worksheets[0];

    //Format the header
    worksheet.PageSetup.CenterHeader = @"&""Gothic,bold""Center Header Text";

    workbook.SaveAs("HeaderFormat.xlsx");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Excel2013

    Dim workbook As IWorkbook = application.Workbooks.Create(1)

    Dim worksheet As IWorksheet = workbook.Worksheets(0)

    'Format the header
    worksheet.PageSetup.CenterHeader = "&""Gothic,bold""Center Header Text"

    workbook.SaveAs("HeaderFormat.xlsx")
End Using
{% endhighlight %}

{% highlight UWP %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Excel2013;
    IWorkbook workbook = application.Workbooks.Create(1);

    IWorksheet worksheet = workbook.Worksheets[0];

    //Format the header
    worksheet.PageSetup.CenterHeader = @"&""Gothic,bold""Center Header Text";

    //Initializes FileSavePicker
    FileSavePicker savePicker = new FileSavePicker();
    savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
    savePicker.SuggestedFileName = "HeaderFormat";
    savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

    //Creates a storage file from FileSavePicker
    StorageFile storageFile = await savePicker.PickSaveFileAsync();

    //Saves changes to the specified storage file
    await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight ASP.NET Core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Excel2013;
    IWorkbook workbook = application.Workbooks.Create(1);

    IWorksheet worksheet = workbook.Worksheets[0];

    //Format the header
    worksheet.PageSetup.CenterHeader = @"&""Gothic,bold""Center Header Text";

    FileStream stream = new FileStream("HeaderFormat.xlsx", FileMode.OpenOrCreate, FileAccess.ReadWrite);
    workbook.SaveAs(stream);

    workbook.Close();
    excelEngine.Dispose();
}
{% endhighlight %}

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Excel2013;
    IWorkbook workbook = application.Workbooks.Create(1);

    IWorksheet worksheet = workbook.Worksheets[0];

    //Format the header
    worksheet.PageSetup.CenterHeader = @"&""Gothic,bold""Center Header Text";

    MemoryStream stream = new MemoryStream();
    workbook.SaveAs(stream);

    stream.Position = 0;

    //Save the stream as a file in the device and invoke it for viewing
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("HeaderFormat.xlsx", "application/msexcel", stream);
}
{% endhighlight %}

{% endtabs %}

N> Go to “ View -> Page Layout” option to view the header and footer in Microsoft Excel. 

## See Also

* [How to enable/disable header footer?](https://help.syncfusion.com/file-formats/xlsio/excel-to-pdf-converter-settings#header-footer-option)
* [What are page setup settings?](https://help.syncfusion.com/file-formats/xlsio/working-with-excel-worksheet#page-setup-settings)
* [How to set a line break inside a cell?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-set-a-line-break-inside-a-cell)
* [How to set print titles?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-set-print-titles)
* [How to format text within a cell?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-format-text-within-a-cell)
