---
title: How to set rounded corner for chart in excel document | Syncfusion
description: Code example to set rounded corner for chart in excel document using Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# How to set rounded corner for chart in Excel document?

The following code snippet shows how to set rounded corner for chart in Excel document.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;
    IWorkbook workbook = application.Workbooks.Create(1);
    IWorksheet sheet = workbook.Worksheets[0];

    object[] xValues = new object[] { "Total Income", "Expenses", "Profit" };
    object[] yValues = new object[] { 2000, 1000, 1500 };

    //Adding series and values
    IChartShape chart = sheet.Charts.Add();
    IChartSerie serie = chart.Series.Add(ExcelChartType.Column_Clustered);

    //set the rounded border for the chart
    chart.ChartArea.IsBorderCornersRound = true;

    //sets the top row of the chart
    chart.TopRow = 5;
    chart.BottomRow = 20;
    chart.LeftColumn = 5;
    chart.RightColumn = 13;

    //Enters the X and Y values directly
    serie.EnteredDirectlyValues = yValues;
    serie.EnteredDirectlyCategoryLabels = xValues;

    //Saving the workbook as stream
    FileStream stream = new FileStream("Chart.xlsx", FileMode.Create, FileAccess.ReadWrite);
    workbook.SaveAs(stream);
    stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;
    IWorkbook workbook = application.Workbooks.Create(1);
    IWorksheet sheet = workbook.Worksheets[0];

    object[] xValues = new object[] { "Total Income", "Expenses", "Profit" };
    object[] yValues = new object[] { 2000, 1000, 1500 };

    //Adding series and values
    IChartShape chart = sheet.Charts.Add();
    IChartSerie serie = chart.Series.Add(ExcelChartType.Column_Clustered);

    //set the rounded border for the chart
    chart.ChartArea.IsBorderCornersRound = true;

    //sets the top row of the chart
    chart.TopRow = 5;
    chart.BottomRow = 20;
    chart.LeftColumn = 5;
    chart.RightColumn = 13;

    //Enters the X and Y values directly
    serie.EnteredDirectlyValues = yValues;
    serie.EnteredDirectlyCategoryLabels = xValues;

    //Saving the workbook
    workbook.SaveAs("Chart.xlsx");
    stream.Dispose();
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
    Dim Application As IApplication = excelEngine.Excel
    Application.DefaultVersion = ExcelVersion.Xlsx
    Dim workbook As IWorkbook = Application.Workbooks.Create(1)
    Dim sheet As IWorksheet = workbook.Worksheets(0)

    Dim xValues As Object() = New Object() {"Total Income", "Expenses", "Profit"}
    Dim yValues As Object() = New Object() {2000, 1000, 1000}

    'Adding series And values
    Dim chart As IChartShape = sheet.Charts.Add()
    Dim serie As IChartSerie = chart.Series.Add(ExcelChartType.Column_Clustered)

    'set the rounded border for the chart
    chart.ChartArea.IsBorderCornersRound = True

    'sets the top row of the chart
    chart.TopRow = 5
    chart.BottomRow = 20
    chart.LeftColumn = 5
    chart.RightColumn = 13

    'Enters the X And Y values directly
    serie.EnteredDirectlyValues = yValues
    serie.EnteredDirectlyCategoryLabels = xValues

    'Saving the workbook as stream
    Dim Stream As FileStream = New FileStream("Chart.xlsx", FileMode.Create, FileAccess.ReadWrite)
    workbook.SaveAs(Stream)
    Stream.Dispose()
End Using
{% endhighlight %}
{% endtabs %}

## See Also

* [How to change the border style for chart series](https://help.syncfusion.com/file-formats/xlsio/working-with-charts#border-style-for-chart-series)
* [How to explode a Pie Chart](https://help.syncfusion.com/file-formats/xlsio/working-with-charts#explode-a-pie-chart)
* [How to add picture to the chart and assign hyperlink](https://help.syncfusion.com/file-formats/xlsio/working-with-charts#add-picture-to-chart-and-assign-hyperlink)
* [How to customizing chart and chart elements](https://help.syncfusion.com/file-formats/xlsio/working-with-charts#customizing-chart-and-chart-elements)
* [How to add data label to the chart](https://help.syncfusion.com/file-formats/xlsio/working-with-charts#add-datatable-to-chart)