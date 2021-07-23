---
title: FAQ Section| XlsIO | Syncfusion
description: Code example to copy and paste the values of the cells that contain only formulas using Essential XlsIO.
platform: File-formats
control: XlsIO
documentation: UG
---

# How to copy/paste the cell values that contain only formula?

You can copy and paste the values of the cell which contain only formula using CopyTo method by specifying the ExcelCopyRangeOptions as None. The following code snippet illustrates this.

{% tabs %}  

{% highlight c# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Excel2013;

    IWorkbook workbook = application.Workbooks.Create(1);

    IWorksheet worksheet = workbook.Worksheets[0];

    //Assigning formula to a cell

    worksheet.Range["A3"].Formula="SUM(1+1)";

    IRange sourceRange = worksheet.Range["A3"];

    IRange destinationRange = worksheet.Range["B1"];

    //Copy and paste the values using ExcelCopyRangeOption

    sourceRange.CopyTo(destinationRange, ExcelCopyRangeOptions.None);

    workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Excel2013

    Dim workbook As IWorkbook = application.Workbooks.Create(1)

    Dim worksheet As IWorksheet = workbook.Worksheets(0)

    'Assigning formula to a cell

    worksheet.Range("A3").Formula = "SUM(1+1)"

    Dim sourceRange As IRange = worksheet.Range("A3")

    Dim destinationRange As IRange = worksheet.Range("B1")

    'Copy and paste the values using ExcelCopyRangeOption

    sourceRange.CopyTo(destinationRange, ExcelCopyRangeOptions.None)

    workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}

{% highlight UWP %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Excel2013;
    IWorkbook workbook = application.Workbooks.Create(1);

    IWorksheet worksheet = workbook.Worksheets[0];

    //Assigning formula to a cell
    worksheet.Range["A3"].Formula = "SUM(1+1)";

    IRange sourceRange = worksheet.Range["A3"];

    IRange destinationRange = worksheet.Range["B1"];

    //Copy and paste the values using ExcelCopyRangeOption
    sourceRange.CopyTo(destinationRange, ExcelCopyRangeOptions.None);

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

{% highlight ASP.NET Core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Excel2013;
    IWorkbook workbook = application.Workbooks.Create(1);

    IWorksheet worksheet = workbook.Worksheets[0];

    //Assigning formula to a cell
    worksheet.Range["A3"].Formula = "SUM(1+1)";

    IRange sourceRange = worksheet.Range["A3"];

    IRange destinationRange = worksheet.Range["B1"];

    //Copy and paste the values using ExcelCopyRangeOption
    sourceRange.CopyTo(destinationRange, ExcelCopyRangeOptions.None);

    FileStream stream = new FileStream("Output.xlsx", FileMode.OpenOrCreate, FileAccess.ReadWrite);
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

    //Assigning formula to a cell
    worksheet.Range["A3"].Formula = "SUM(1+1)";

    IRange sourceRange = worksheet.Range["A3"];

    IRange destinationRange = worksheet.Range["B1"];

    //Copy and paste the values using ExcelCopyRangeOption
    sourceRange.CopyTo(destinationRange, ExcelCopyRangeOptions.None);

    MemoryStream stream = new MemoryStream();
    workbook.SaveAs(stream);

    stream.Position = 0;

    //Save the stream as a file in the device and invoke it for viewing
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", stream);
}
{% endhighlight %}

{% endtabs %}  

## See Also

* [How to copy a range from one workbook to another?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-copy-a-range-from-one-workbook-to-another)
* [How to protect certain cells in a worksheet?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-protect-certain-cells-in-a-worksheet)
* [How to set a line break inside a cell?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-set-a-line-break-inside-a-cell)
* [How to format text within a cell?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-format-text-within-a-cell)
* [How to copy or move a range?](https://help.syncfusion.com/file-formats/xlsio/worksheet-cells-manipulation#copy-or-move-a-range)
* [How to copy and paste as link?](https://help.syncfusion.com/file-formats/xlsio/worksheet-cells-manipulation#copy-and-paste-as-link)
* [How to skip blanks while copying?](https://help.syncfusion.com/file-formats/xlsio/worksheet-cells-manipulation#skip-blanks-while-copying)

