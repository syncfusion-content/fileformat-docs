---
title: How to define discontinuous ranges | XlsIO | Syncfusion
description: This page explains with an example to define discontinuous ranges using Syncfusion .NET Excel library (XlsIO).
platform: File-formats
control: XlsIO
documentation: UG
---

# How to define discontinuous ranges?

You can define a discontinuous range by adding different ranges to the Range collection. The following code example illustrates this.

{% tabs %}  

{% highlight c# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Excel2013;

    IWorkbook workbook = application.Workbooks.Create(1);

    IWorksheet worksheet = workbook.Worksheets[0];

    //Create Range collection.

    IRanges rangeCollection = worksheet.CreateRangesCollection();

    //Add different ranges to the Range collection.

    rangeCollection.Add(worksheet.Range["D2:D3"]);

    rangeCollection.Add(worksheet.Range["D10:D11"]);

    rangeCollection.Text = "Welcome";

    workbook.SaveAs("DiscontinuousRange.xlsx");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Excel2013

    Dim workbook As IWorkbook = application.Workbooks.Create(1)

    Dim worksheet As IWorksheet = workbook.Worksheets(0)

    'Create Range collection.

    Dim range As IRanges = worksheet.CreateRangesCollection()

    'Add different ranges to the Range collection.

    range.Add(worksheet.Range("D2:D3"))

    range.Add(worksheet.Range("D10:D11"))

    range.Text = "Welcome"

    workbook.SaveAs("DiscontinuousRange.xlsx")
End Using
{% endhighlight %}

{% highlight UWP %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Excel2013;
    IWorkbook workbook = application.Workbooks.Create(1);

    IWorksheet worksheet = workbook.Worksheets[0];

    //Create Range collection.

    IRanges rangeCollection = worksheet.CreateRangesCollection();

    //Add different ranges to the Range collection.

    rangeCollection.Add(worksheet.Range["D2:D3"]);

    rangeCollection.Add(worksheet.Range["D10:D11"]);

    rangeCollection.Text = "Welcome";

    //Initializes FileSavePicker
    FileSavePicker savePicker = new FileSavePicker();
    savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
    savePicker.SuggestedFileName = "DiscontinuousRange";
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

    //Create Range collection.

    IRanges rangeCollection = worksheet.CreateRangesCollection();

    //Add different ranges to the Range collection.

    rangeCollection.Add(worksheet.Range["D2:D3"]);

    rangeCollection.Add(worksheet.Range["D10:D11"]);

    rangeCollection.Text = "Welcome";

    FileStream stream = new FileStream("DiscontinuousRange.xlsx", FileMode.OpenOrCreate, FileAccess.ReadWrite);
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

    //Create Range collection.

    IRanges rangeCollection = worksheet.CreateRangesCollection();

    //Add different ranges to the Range collection.

    rangeCollection.Add(worksheet.Range["D2:D3"]);

    rangeCollection.Add(worksheet.Range["D10:D11"]);

    rangeCollection.Text = "Welcome";

    MemoryStream stream = new MemoryStream();
    workbook.SaveAs(stream);

    stream.Position = 0;

    //Save the stream as a file in the device and invoke it for viewing
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("DiscontinuousRange.xlsx", "application/msexcel", stream);
}
{% endhighlight %}

{% endtabs %}  

## See Also

* [How to create a Chart with a discontinuous range?](faqs/how-to-create-a-chart-with-a-discontinuous-range)
* [How to show or hide a specific range?](https://help.syncfusion.com/file-formats/xlsio/worksheet-rows-and-columns-manipulation#show-or-hide-specific-range)
* [How to access a cell or a range?](https://help.syncfusion.com/file-formats/xlsio/worksheet-cells-manipulation#accessing-a-cell-or-a-range)
* [How to access relative range?](https://help.syncfusion.com/file-formats/xlsio/worksheet-cells-manipulation#accessing-relative-range)
* [How to access discontinuous ranges?](https://help.syncfusion.com/file-formats/xlsio/worksheet-cells-manipulation#accessing-discontinuous-ranges)
* [How to access used range of a worksheet?](https://help.syncfusion.com/file-formats/xlsio/worksheet-cells-manipulation#accessing-used-range-of-a-worksheet)
* [How to copy or move a range?](https://help.syncfusion.com/file-formats/xlsio/worksheet-cells-manipulation#copy-or-move-a-range)

