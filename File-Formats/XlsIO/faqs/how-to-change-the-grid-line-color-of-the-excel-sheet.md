---
title: FAQ Section| XlsIO | Syncfusion
description: Code example to change the grid line color of the Excel sheet using Syncfusion .NET Excel library (XlsIO).
platform: File-formats
control: XlsIO
documentation: UG
---

# How to change the grid line color of the Excel sheet?

In Essential XlsIO, you can change the grid line color of the worksheet using **GridLineColor** property. The below code snippet illustrate this.

{% tabs %}  

{% highlight c# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Excel2013;

    IWorkbook workbook = application.Workbooks.Create(1);

    IWorksheet worksheet = workbook.Worksheets[0];

    //To change the grid line color using ExcelKnownColors
    worksheet.GridLineColor = ExcelKnownColors.Blue;

    workbook.SaveAs("GridLineColor.xlsx");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Excel2013

    Dim workbook As IWorkbook = application.Workbooks.Create(1)

    Dim worksheet As IWorksheet = workbook.Worksheets(0)

    'To change the grid line color using ExcelKnownColors
    worksheet.GridLineColor = ExcelKnownColors.Blue

    workbook.SaveAs("GridLineColor.xlsx")
End Using
{% endhighlight %}

{% highlight UWP %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
	IApplication application = excelEngine.Excel;
	application.DefaultVersion = ExcelVersion.Excel2013;
	IWorkbook workbook = application.Workbooks.Create(1);
                
    IWorksheet worksheet = workbook.Worksheets[0];

    //To change the grid line color using ExcelKnownColors
    worksheet.GridLineColor = ExcelKnownColors.Blue;

    //Initializes FileSavePicker
    FileSavePicker savePicker = new FileSavePicker();
    savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
    savePicker.SuggestedFileName = "GridLineColor";
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

    //To change the grid line color using ExcelKnownColors
    worksheet.GridLineColor = ExcelKnownColors.Blue;

    FileStream stream = new FileStream("GridLineColor.xlsx", FileMode.OpenOrCreate, FileAccess.ReadWrite);
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

    //To change the grid line color using ExcelKnownColors
    worksheet.GridLineColor = ExcelKnownColors.Blue;

    MemoryStream stream = new MemoryStream();
    workbook.SaveAs(stream);

    stream.Position = 0;

    //Save the stream as a file in the device and invoke it for viewing
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("GridLineColor.xlsx", "application/msexcel", stream);
}
{% endhighlight %}

{% endtabs %}  

## See Also

How to set a line break inside a cell?
[Show or Hide Grid Lines](https://help.syncfusion.com/file-formats/xlsio/working-with-excel-worksheet#show-or-hide-grid-lines)
[Hide Chart Gridlines](https://help.syncfusion.com/file-formats/xlsio/working-with-charts#hide-chart-gridlines)
[Highlight Worksheet Tabs](https://help.syncfusion.com/file-formats/xlsio/working-with-excel-worksheet#highlight-worksheet-tabs)
[Apply Color Settings](https://help.syncfusion.com/file-formats/xlsio/working-with-cell-or-range-formatting#apply-color-settings)
How to change data point label color of a Waterfall chart?
