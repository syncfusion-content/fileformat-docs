---
title: How to create a Chart with a discontinuous range | XlsIO | Syncfusion
description: Code example to create a Chart with a discontinuous range using Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# How to create a Chart with a discontinuous range?

The following code example illustrates creating a chart with discontinuous data ranges.

{% tabs %}  

{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Excel2013;

    IWorkbook workbook = application.Workbooks.Create(1);

    IWorksheet worksheet = workbook.Worksheets[0];

    //Entering the data for the chart.

    worksheet.Range["A1"].Text = "Texas books Unit sales";

    worksheet.Range["A1:D1"].Merge();

    worksheet.Range["A1"].CellStyle.Font.Bold = true;

    worksheet.Range["B2"].Text = "Jan";

    worksheet.Range["C2"].Text = "Feb";

    worksheet.Range["D2"].Text = "Mar";

    worksheet.Range["A3"].Text = "Austin";

    worksheet.Range["A4"].Text = "Dallas";

    worksheet.Range["A5"].Text = "Houston";

    worksheet.Range["A6"].Text = "San Antonio";

    worksheet.Range["B3"].Number = 53.75;

    worksheet.Range["B4"].Number = 52.85;

    worksheet.Range["B5"].Number = 59.77;

    worksheet.Range["B6"].Number = 96.15;

    worksheet.Range["C3"].Number = 79.79;

    worksheet.Range["C4"].Number = 59.22;

    worksheet.Range["C5"].Number = 10.09;

    worksheet.Range["C6"].Number = 73.02;

    worksheet.Range["D3"].Number = 26.72;

    worksheet.Range["D4"].Number = 33.71;

    worksheet.Range["D5"].Number = 45.81;

    worksheet.Range["D6"].Number = 12.17;

    worksheet.Range["F1"].Number = 26.72;

    worksheet.Range["F2"].Number = 33.71;

    worksheet.Range["F3"].Number = 45.81;

    worksheet.Range["F4"].Number = 12.17;

    //Discontinuous range.

    IRanges rangesOne = worksheet.CreateRangesCollection();

    rangesOne.Add(worksheet.Range["B3:B6"]);

    rangesOne.Add(worksheet.Range["F1:F2"]);

    IRanges rangesTwo = worksheet.CreateRangesCollection();

    rangesTwo.Add(worksheet.Range["D3:D6"]);

    rangesTwo.Add(worksheet.Range["F3:F4"]);

    //Adding a New (Embedded chart) to the Worksheet.

    IChartShape shape = worksheet.Charts.Add();

    shape.PrimaryCategoryAxis.Title = "City";

    shape.PrimaryValueAxis.Title = "Sales (in Dollars)";

    shape.ChartTitle = "Texas Books Unit Sales";

    //Setting the Series Names in a Legend.

    IChartSerie serieOne = shape.Series.Add();

    serieOne.Name = "Jan";

    serieOne.Values = rangesOne;

    IChartSerie serieTwo = shape.Series.Add();

    serieTwo.Name = "March";

    serieTwo.Values = rangesTwo;

    //Setting the (Rows & Columns) Property for the Embedded chart.

    shape.BottomRow = 40;

    shape.TopRow = 10;

    shape.LeftColumn = 3;

    shape.RightColumn = 15;

    workbook.SaveAs("DiscontinuousRange.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Excel2013

    Dim workbook As IWorkbook = application.Workbooks.Create(1)

    Dim worksheet As IWorksheet = workbook.Worksheets(0)

    'Entering the data for the chart.

    worksheet.Range("A1").Text = "Texas books Unit sales"

    worksheet.Range("A1:D1").Merge()

    worksheet.Range("A1").CellStyle.Font.Bold = True

    worksheet.Range("B2").Text = "Jan"

    worksheet.Range("C2").Text = "Feb"

    worksheet.Range("D2").Text = "Mar"

    worksheet.Range("A3").Text = "Austin"

    worksheet.Range("A4").Text = "Dallas"

    worksheet.Range("A5").Text = "Houston"

    worksheet.Range("A6").Text = "San Antonio"

    worksheet.Range("B3").Number = 53.75

    worksheet.Range("B4").Number = 52.85

    worksheet.Range("B5").Number = 59.77

    worksheet.Range("B6").Number = 96.15

    worksheet.Range("C3").Number = 79.79

    worksheet.Range("C4").Number = 59.22

    worksheet.Range("C5").Number = 10.09

    worksheet.Range("C6").Number = 73.02

    worksheet.Range("D3").Number = 26.72

    worksheet.Range("D4").Number = 33.71

    worksheet.Range("D5").Number = 45.81

    worksheet.Range("D6").Number = 12.17

    worksheet.Range("F1").Number = 26.72

    worksheet.Range("F2").Number = 33.71

    worksheet.Range("F3").Number = 45.81

    worksheet.Range("F4").Number = 12.17

    'Discontinuous range.

    Dim rangesOne As IRanges = worksheet.CreateRangesCollection()

    rangesOne.Add(worksheet.Range("B3:B6"))

    rangesOne.Add(worksheet.Range("F1:F2"))

    Dim rangesTwo As IRanges = worksheet.CreateRangesCollection()

    rangesTwo.Add(worksheet.Range("D3:D6"))

    rangesTwo.Add(worksheet.Range("F3:F4"))

    'Adding a New (Embedded chart) to the Worksheet.

    Dim shape As IChartShape = worksheet.Charts.Add()

    shape.PrimaryCategoryAxis.Title = "City"

    shape.PrimaryValueAxis.Title = "Sales (in Dollars)"

    shape.ChartTitle = "Texas Books Unit Sales"

    'Setting the Series Names in a Legend.

    Dim serieOne As IChartSerie = shape.Series.Add()

    serieOne.Name = "Jan"

    serieOne.Values = rangesOne

    Dim serieTwo As IChartSerie = shape.Series.Add()

    serieTwo.Name = "March"

    serieTwo.Values = rangesTwo

    'Setting the (Rows & Columns)Property for the Embedded chart.

    shape.BottomRow = 40

    shape.TopRow = 10

    shape.LeftColumn = 3

    shape.RightColumn = 15

    workbook.SaveAs("DiscontinuousRange.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Excel2013;
    IWorkbook workbook = application.Workbooks.Create(1);

    IWorksheet worksheet = workbook.Worksheets[0];

    //Entering the data for the chart.

    worksheet.Range["A1"].Text = "Texas books Unit sales";

    worksheet.Range["A1:D1"].Merge();

    worksheet.Range["A1"].CellStyle.Font.Bold = true;

    worksheet.Range["B2"].Text = "Jan";

    worksheet.Range["C2"].Text = "Feb";

    worksheet.Range["D2"].Text = "Mar";

    worksheet.Range["A3"].Text = "Austin";

    worksheet.Range["A4"].Text = "Dallas";

    worksheet.Range["A5"].Text = "Houston";

    worksheet.Range["A6"].Text = "San Antonio";

    worksheet.Range["B3"].Number = 53.75;

    worksheet.Range["B4"].Number = 52.85;

    worksheet.Range["B5"].Number = 59.77;

    worksheet.Range["B6"].Number = 96.15;

    worksheet.Range["C3"].Number = 79.79;

    worksheet.Range["C4"].Number = 59.22;

    worksheet.Range["C5"].Number = 10.09;

    worksheet.Range["C6"].Number = 73.02;

    worksheet.Range["D3"].Number = 26.72;

    worksheet.Range["D4"].Number = 33.71;

    worksheet.Range["D5"].Number = 45.81;

    worksheet.Range["D6"].Number = 12.17;

    worksheet.Range["F1"].Number = 26.72;

    worksheet.Range["F2"].Number = 33.71;

    worksheet.Range["F3"].Number = 45.81;

    worksheet.Range["F4"].Number = 12.17;

    //Discontinuous range.

    IRanges rangesOne = worksheet.CreateRangesCollection();

    rangesOne.Add(worksheet.Range["B3:B6"]);

    rangesOne.Add(worksheet.Range["F1:F2"]);

    IRanges rangesTwo = worksheet.CreateRangesCollection();

    rangesTwo.Add(worksheet.Range["D3:D6"]);

    rangesTwo.Add(worksheet.Range["F3:F4"]);

    //Adding a New (Embedded chart) to the Worksheet.

    IChartShape shape = worksheet.Charts.Add();

    shape.PrimaryCategoryAxis.Title = "City";

    shape.PrimaryValueAxis.Title = "Sales (in Dollars)";

    shape.ChartTitle = "Texas Books Unit Sales";

    //Setting the Series Names in a Legend.

    IChartSerie serieOne = shape.Series.Add();

    serieOne.Name = "Jan";

    serieOne.Values = rangesOne;

    IChartSerie serieTwo = shape.Series.Add();

    serieTwo.Name = "March";

    serieTwo.Values = rangesTwo;

    //Setting the (Rows & Columns) Property for the Embedded chart.

    shape.BottomRow = 40;

    shape.TopRow = 10;

    shape.LeftColumn = 3;

    shape.RightColumn = 15;

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

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Excel2013;
    IWorkbook workbook = application.Workbooks.Create(1);

    IWorksheet worksheet = workbook.Worksheets[0];

    //Entering the data for the chart.

    worksheet.Range["A1"].Text = "Texas books Unit sales";

    worksheet.Range["A1:D1"].Merge();

    worksheet.Range["A1"].CellStyle.Font.Bold = true;

    worksheet.Range["B2"].Text = "Jan";

    worksheet.Range["C2"].Text = "Feb";

    worksheet.Range["D2"].Text = "Mar";

    worksheet.Range["A3"].Text = "Austin";

    worksheet.Range["A4"].Text = "Dallas";

    worksheet.Range["A5"].Text = "Houston";

    worksheet.Range["A6"].Text = "San Antonio";

    worksheet.Range["B3"].Number = 53.75;

    worksheet.Range["B4"].Number = 52.85;

    worksheet.Range["B5"].Number = 59.77;

    worksheet.Range["B6"].Number = 96.15;

    worksheet.Range["C3"].Number = 79.79;

    worksheet.Range["C4"].Number = 59.22;

    worksheet.Range["C5"].Number = 10.09;

    worksheet.Range["C6"].Number = 73.02;

    worksheet.Range["D3"].Number = 26.72;

    worksheet.Range["D4"].Number = 33.71;

    worksheet.Range["D5"].Number = 45.81;

    worksheet.Range["D6"].Number = 12.17;

    worksheet.Range["F1"].Number = 26.72;

    worksheet.Range["F2"].Number = 33.71;

    worksheet.Range["F3"].Number = 45.81;

    worksheet.Range["F4"].Number = 12.17;

    //Discontinuous range.

    IRanges rangesOne = worksheet.CreateRangesCollection();

    rangesOne.Add(worksheet.Range["B3:B6"]);

    rangesOne.Add(worksheet.Range["F1:F2"]);

    IRanges rangesTwo = worksheet.CreateRangesCollection();

    rangesTwo.Add(worksheet.Range["D3:D6"]);

    rangesTwo.Add(worksheet.Range["F3:F4"]);

    //Adding a New (Embedded chart) to the Worksheet.

    IChartShape shape = worksheet.Charts.Add();

    shape.PrimaryCategoryAxis.Title = "City";

    shape.PrimaryValueAxis.Title = "Sales (in Dollars)";

    shape.ChartTitle = "Texas Books Unit Sales";

    //Setting the Series Names in a Legend.

    IChartSerie serieOne = shape.Series.Add();

    serieOne.Name = "Jan";

    serieOne.Values = rangesOne;

    IChartSerie serieTwo = shape.Series.Add();

    serieTwo.Name = "March";

    serieTwo.Values = rangesTwo;

    //Setting the (Rows & Columns) Property for the Embedded chart.

    shape.BottomRow = 40;

    shape.TopRow = 10;

    shape.LeftColumn = 3;

    shape.RightColumn = 15;

    FileStream stream = new FileStream("DiscontinuousRange.xlsx", FileMode.OpenOrCreate, FileAccess.ReadWrite);
    workbook.SaveAs(stream);

    workbook.Close();
    excelEngine.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Excel2013;
    IWorkbook workbook = application.Workbooks.Create(1);

    IWorksheet worksheet = workbook.Worksheets[0];

    //Entering the data for the chart.

    worksheet.Range["A1"].Text = "Texas books Unit sales";

    worksheet.Range["A1:D1"].Merge();

    worksheet.Range["A1"].CellStyle.Font.Bold = true;

    worksheet.Range["B2"].Text = "Jan";

    worksheet.Range["C2"].Text = "Feb";

    worksheet.Range["D2"].Text = "Mar";

    worksheet.Range["A3"].Text = "Austin";

    worksheet.Range["A4"].Text = "Dallas";

    worksheet.Range["A5"].Text = "Houston";

    worksheet.Range["A6"].Text = "San Antonio";

    worksheet.Range["B3"].Number = 53.75;

    worksheet.Range["B4"].Number = 52.85;

    worksheet.Range["B5"].Number = 59.77;

    worksheet.Range["B6"].Number = 96.15;

    worksheet.Range["C3"].Number = 79.79;

    worksheet.Range["C4"].Number = 59.22;

    worksheet.Range["C5"].Number = 10.09;

    worksheet.Range["C6"].Number = 73.02;

    worksheet.Range["D3"].Number = 26.72;

    worksheet.Range["D4"].Number = 33.71;

    worksheet.Range["D5"].Number = 45.81;

    worksheet.Range["D6"].Number = 12.17;

    worksheet.Range["F1"].Number = 26.72;

    worksheet.Range["F2"].Number = 33.71;

    worksheet.Range["F3"].Number = 45.81;

    worksheet.Range["F4"].Number = 12.17;

    //Discontinuous range.

    IRanges rangesOne = worksheet.CreateRangesCollection();

    rangesOne.Add(worksheet.Range["B3:B6"]);

    rangesOne.Add(worksheet.Range["F1:F2"]);

    IRanges rangesTwo = worksheet.CreateRangesCollection();

    rangesTwo.Add(worksheet.Range["D3:D6"]);

    rangesTwo.Add(worksheet.Range["F3:F4"]);

    //Adding a New (Embedded chart) to the Worksheet.

    IChartShape shape = worksheet.Charts.Add();

    shape.PrimaryCategoryAxis.Title = "City";

    shape.PrimaryValueAxis.Title = "Sales (in Dollars)";

    shape.ChartTitle = "Texas Books Unit Sales";

    //Setting the Series Names in a Legend.

    IChartSerie serieOne = shape.Series.Add();

    serieOne.Name = "Jan";

    serieOne.Values = rangesOne;

    IChartSerie serieTwo = shape.Series.Add();

    serieTwo.Name = "March";

    serieTwo.Values = rangesTwo;

    //Setting the (Rows & Columns) Property for the Embedded chart.

    shape.BottomRow = 40;

    shape.TopRow = 10;

    shape.LeftColumn = 3;

    shape.RightColumn = 15;

    MemoryStream stream = new MemoryStream();
    workbook.SaveAs(stream);

    stream.Position = 0;

    //Save the stream as a file in the device and invoke it for viewing
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("DiscontinuousRange.xlsx", "application/msexcel", stream);
}
{% endhighlight %}

{% endtabs %}  

## See Also

* [How to define discontinuous ranges?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-define-discontinuous-ranges)
* [How to add chart labels to scatter points?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-add-chart-labels-to-scatter-points)
* [How to change data point label color of a Waterfall chart?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-change-data-point-label-color-of-a-waterfall-chart)
* [How to set data range to chart?](https://help.syncfusion.com/file-formats/xlsio/working-with-charts#set-data-range-to-chart)
* [How to access discontinuous ranges?](https://help.syncfusion.com/file-formats/xlsio/worksheet-cells-manipulation#accessing-discontinuous-ranges)
* [How to create a chart?](https://help.syncfusion.com/file-formats/xlsio/working-with-charts#creating-a-chart)
* [How to create a pie chart in Excel?](https://help.syncfusion.com/file-formats/xlsio/migrate-from-office-automation-to-syncfusion-xlsio/create-pie-chart-in-excel)
* [How to create a sparkline from a named range?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-create-a-sparkline-from-a-named-range)
