---
title: How to copy a range from one workbook to another? | XlsIO | Syncfusion
description: Code example to copy a range from one workbook to another using Syncfusion .NET Excel library (XlsIO).
platform: File-formats
control: XlsIO
documentation: UG
---

# How to copy a range from one workbook to another?

You can copy the range from source workbook to the destination workbook through CopyTo method. 

The following code snippet illustrates this.

{% tabs %}  

{% highlight c# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Excel2013;

    IWorkbook sourceWorkbook = application.Workbooks.Open("SourceWorkbook.xlsx", ExcelOpenType.Automatic);

    IWorkbook destinationWorkbook = application.Workbooks.Open("DestinationWorkbook.xlsx", ExcelOpenType.Automatic);

    //The first worksheet object in the worksheets collection in the Source Workbook is accessed.
    IWorksheet sourceWorksheet = sourceWorkbook.Worksheets[0];

    //The first worksheet object in the worksheets collection in the Destination Workbook is accessed.
    IWorksheet destinationWorksheet = destinationWorkbook.Worksheets[0];

    //Assigning an object to the range of cells (90 rows) both for source and destination.
    IRange sourceRange = sourceWorksheet.Range[1, 1, 90, 100];
    IRange destinationRange = destinationWorksheet.Range[1, 1, 90, 100];

    //Copying (90 rows) from Source to Destination worksheet.
    sourceRange.CopyTo(destinationRange);

    destinationWorkbook.SaveAs("CopyingRange.xlsx");
}
{% endhighlight %}


{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Excel2013

    Dim sourceWorkbook As IWorkbook = application.Workbooks.Open("SourceWorkbook.xlsx", ExcelOpenType.Automatic)

    Dim destinationWorkbook As IWorkbook = application.Workbooks.Open("DestinationWorkbook.xlsx", ExcelOpenType.Automatic)

    'The first worksheet object in the worksheets collection in the Source Workbook is accessed.
    Dim sourceWorksheet As Syncfusion.XlsIO.IWorksheet = sourceWorkbook.Worksheets(0)

    'The first worksheet object in the worksheets collection in the Destination Workbook is accessed.
    Dim destinationWorksheet As Syncfusion.XlsIO.IWorksheet = destinationWorkbook.Worksheets(0)

    'Assigning an object to the range of cells (90 rows) both for source and destination.
    Dim sourceRange As Syncfusion.XlsIO.IRange = sourceWorksheet.Range(1, 1, 90, 100)
    Dim destinationRange As Syncfusion.XlsIO.IRange = destinationWorksheet.Range(1, 1, 90, 100)

    'Copying (90 rows) from Source to Destination worksheet.
    sourceRange.CopyTo(destinationRange)

    destinationWorkbook.SaveAs("CopyingRange.xlsx")
End Using
{% endhighlight %}

{% highlight UWP %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;

    //Instantiates the File Picker to open the Source Workbook
    FileOpenPicker openPicker1 = new FileOpenPicker();
    openPicker1.SuggestedStartLocation = PickerLocationId.Desktop;
    openPicker1.FileTypeFilter.Add(".xlsx");
    openPicker1.FileTypeFilter.Add(".xls");
    StorageFile file1 = await openPicker1.PickSingleFileAsync();

    IWorkbook sourceWorkbook = await application.Workbooks.OpenAsync(file1, ExcelOpenType.Automatic);

    //Instantiates the File Picker to open the Destination Workbook
    FileOpenPicker openPicker2 = new FileOpenPicker();
    openPicker2.SuggestedStartLocation = PickerLocationId.Desktop;
    openPicker2.FileTypeFilter.Add(".xlsx");
    openPicker2.FileTypeFilter.Add(".xls");
    StorageFile file2 = await openPicker2.PickSingleFileAsync();

    IWorkbook destinationWorkbook = await application.Workbooks.OpenAsync(file2, ExcelOpenType.Automatic);

    //The first worksheet object in the worksheets collection in the Source Workbook is accessed.
    IWorksheet sourceWorksheet = sourceWorkbook.Worksheets[0];

    //The first worksheet object in the worksheets collection in the Destination Workbook is accessed.
    IWorksheet destinationWorksheet = destinationWorkbook.Worksheets[0];

    //Assigning an object to the range of cells (90 rows) both for source and destination.
    IRange sourceRange = sourceWorksheet.Range[1, 1, 90, 100];
    IRange destinationRange = destinationWorksheet.Range[1, 1, 90, 100];

    //Copying (90 rows) from Source to Destination worksheet.
    sourceRange.CopyTo(destinationRange);

    //Initializes FileSavePicker
    FileSavePicker savePicker = new FileSavePicker();
    savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
    savePicker.SuggestedFileName = "CopyingRange";
    savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

    //Creates a storage file from FileSavePicker
    StorageFile storageFile = await savePicker.PickSaveFileAsync();

    //Saves changes to the specified storage file
    await destinationWorkbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight ASP.NET Core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Excel2013;

    FileStream inputStream1 = new FileStream("SourceWorkbook.xlsx", FileMode.Open, FileAccess.Read);
    IWorkbook sourceWorkbook = application.Workbooks.Open(inputStream1, ExcelOpenType.Automatic);

    FileStream inputStream2 = new FileStream("DestinationWorkbook.xlsx", FileMode.Open, FileAccess.Read);
    IWorkbook destinationWorkbook = application.Workbooks.Open(inputStream2, ExcelOpenType.Automatic);

    //The first worksheet object in the worksheets collection in the Source Workbook is accessed.
    IWorksheet sourceWorksheet = sourceWorkbook.Worksheets[0];

    //The first worksheet object in the worksheets collection in the Destination Workbook is accessed.
    IWorksheet destinationWorksheet = destinationWorkbook.Worksheets[0];

    //Assigning an object to the range of cells (90 rows) both for source and destination.
    IRange sourceRange = sourceWorksheet.Range[1, 1, 90, 100];
    IRange destinationRange = destinationWorksheet.Range[1, 1, 90, 100];

    //Copying (90 rows) from Source to Destination worksheet.
    sourceRange.CopyTo(destinationRange);

    FileStream stream = new FileStream("CopyingRange.xlsx", FileMode.OpenOrCreate, FileAccess.ReadWrite);
    destinationWorkbook.SaveAs(stream);

    destinationWorkbook.Close();
    excelEngine.Dispose();
}
{% endhighlight %}

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Excel2013;

    Assembly assembly = typeof(App).GetTypeInfo().Assembly;
    Stream inputStream1 = assembly.GetManifestResourceStream("GettingStarted.SourceWorkbook.xlsx");
    IWorkbook sourceWorkbook = application.Workbooks.Open(inputStream1);

    Stream inputStream2 = assembly.GetManifestResourceStream("GettingStarted.DestinationWorkbook.xlsx");
    IWorkbook destinationWorkbook = application.Workbooks.Open(inputStream2);

    //The first worksheet object in the worksheets collection in the Source Workbook is accessed.
    IWorksheet sourceWorksheet = sourceWorkbook.Worksheets[0];

    //The first worksheet object in the worksheets collection in the Destination Workbook is accessed.
    IWorksheet destinationWorksheet = destinationWorkbook.Worksheets[0];

    //Assigning an object to the range of cells (90 rows) both for source and destination.
    IRange sourceRange = sourceWorksheet.Range[1, 1, 90, 100];
    IRange destinationRange = destinationWorksheet.Range[1, 1, 90, 100];

    //Copying (90 rows) from Source to Destination worksheet.
    sourceRange.CopyTo(destinationRange);

    MemoryStream stream = new MemoryStream();
    destinationWorkbook.SaveAs(stream);

    stream.Position = 0;

    //Save the stream as a file in the device and invoke it for viewing
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("CopyingRange.xlsx", "application/msexcel", stream);
}
{% endhighlight %}

{% endtabs %}  

## See Also

* [How to copy/paste the cell values that contain only formula?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-copy-paste-the-cell-values-that-contain-only-formula)
* [How to copy or move a range?](https://help.syncfusion.com/file-formats/xlsio/worksheet-cells-manipulation#copy-or-move-a-range)
* [How to copy and paste as link?](https://help.syncfusion.com/file-formats/xlsio/worksheet-cells-manipulation#copy-and-paste-as-link)
* [How to skip blanks while copying?](https://help.syncfusion.com/file-formats/xlsio/worksheet-cells-manipulation#skip-blanks-while-copying)
* [How to open an existing XLSX workbook and save it as XLS?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-open-an-existing-xlsx-workbook-and-save-it-as-xls)
