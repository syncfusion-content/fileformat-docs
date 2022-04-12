---
title: Create Pie Chart in Excel | Syncfusion
description: Explains with an example on how to programmatically create pie chart in Excel and to position the chart in a worksheet using Interop and XlsIO.
platform: file-formats
control: XlsIO
documentation: UG
---

# Create Pie Chart in Excel

The pie charts are used to display the contribution of each value (slice) to a total (pie). So, it is easy to compare proportions. Pie charts always use one data series.

The following code shows how to create pie chart in Excel and to place it in a worksheet with Interop and XlsIO for .NET.

## Interop

{% tabs %}
{% highlight c# tabtitle="C#" %}
private void CreatePieChart()
{
    //Instantiate the application object
    var excelApp = new Microsoft.Office.Interop.Excel.Application();

    //Add a workbook
    Workbook workbook = excelApp.Workbooks.Add(System.Reflection.Missing.Value);

    //Get the first sheet
    Worksheet sheet = workbook.Sheets["Sheet1"];

    //Add sample data for pie chart
    //Add headings in A1 and B1.
    sheet.Cells[1, 1] = "Products";
    sheet.Cells[1, 2] = "Users";

    //Add data from A2 till B4
    sheet.Cells[2, 1] = "XlsIO";
    sheet.Cells[2, 2] = 10000;
    sheet.Cells[3, 1] = "DocIO";
    sheet.Cells[3, 2] = 8000;
    sheet.Cells[4, 1] = "PDF";
    sheet.Cells[4, 2] = 12000;

    //Add a pie chart
    ChartObjects charts = (ChartObjects)sheet.ChartObjects(Type.Missing);
    ChartObject chartObject = (ChartObject)charts.Add(10, 80, 300, 250);
    Chart chart = chartObject.Chart;
    chart.ChartType = XlChartType.xlPie;

    //Set chart title
    chart.HasTitle = true;
    chart.ChartTitle.Text = "Users";

    //Gets the cells that define the data to be charted
    Range chartRange = sheet.get_Range("A2", "B4");
    chart.SetSourceData(chartRange, Type.Missing);

    //Save the Excel file
    workbook.SaveCopyAs(@"d:\test\InteropOutput_PieChart.xlsx");

    //Quit the application
    excelApp.Quit();

}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Private Sub CreatePieChart()
    'Instantiate the application object
    Dim excelApp = New Microsoft.Office.Interop.Excel.Application()

    'Add a workbook
    Dim workbook As Workbook = excelApp.Workbooks.Add(System.Reflection.Missing.Value)

    'Get the first sheet
    Dim sheet As Worksheet = workbook.Sheets("Sheet1")

    'Add sample data for pie chart
    'Add headings in A1 and B1.
    sheet.Cells(1, 1) = "Products"
    sheet.Cells(1, 2) = "Users"

    'Add data from A2 till B4
    sheet.Cells(2, 1) = "XlsIO"
    sheet.Cells(2, 2) = 10000
    sheet.Cells(3, 1) = "DocIO"
    sheet.Cells(3, 2) = 8000
    sheet.Cells(4, 1) = "PDF"
    sheet.Cells(4, 2) = 12000

    'Add a pie chart
    Dim charts As ChartObjects = CType(sheet.ChartObjects(Type.Missing), ChartObjects)
    Dim chartObject As ChartObject = CType(charts.Add(10, 80, 300, 250), ChartObject)
    Dim chart As Chart = chartObject.Chart
    chart.ChartType = XlChartType.xlPie

    'Set chart title
    chart.HasTitle = True
    chart.ChartTitle.Text = "Users"

    'Gets the cells that define the data to be charted
    Dim chartRange As Range = sheet.Range("A2", "B4")
    chart.SetSourceData(chartRange, Type.Missing)

    'Save the file
    workbook.SaveCopyAs("d:\test1\InteropOutput_PieChart.xlsx")

    'Quit the application
    excelApp.Quit()
End Sub
{% endhighlight %}
{% endtabs %}

## XlsIO

{% tabs %}
{% highlight c# tabtitle="C#" %}
private void CreatePieChart()
{
    using (ExcelEngine excelEngine = new ExcelEngine())
    {
        //Instantiate the application object
        IApplication application = excelEngine.Excel;

        //Create a workbook
        IWorkbook workbook = application.Workbooks.Create(1);

        //Get the first sheet
        IWorksheet worksheet = workbook.Worksheets[0];

        //Add sample data for pie chart
        //Add headings in A1 and B1.
        worksheet.Range["A1"].Value = "Products";
        worksheet.Range["B1"].Value = "Users";

        //Add data from A2 till B4
        worksheet.Range["A2"].Value = "XlsIO";
        worksheet.Range["B2"].Value2 = 10000;
        worksheet.Range["A3"].Value = "DocIO";
        worksheet.Range["B3"].Value2 = 8000;
        worksheet.Range["A4"].Value = "PDF";
        worksheet.Range["B4"].Value2 = 12000;

        //Add a pie chart and set data range in the worksheet
        IChartShape chart = worksheet.Charts.Add();
        chart.DataRange = worksheet.Range["A2:B4"];
        chart.ChartType = ExcelChartType.Pie;
        chart.IsSeriesInRows = false;

        //Position chart in the worksheet
        chart.TopRow = 7;
        chart.LeftColumn = 1;
        chart.RightColumn = 7;
        chart.BottomRow = 23;

        //Set chart title
        chart.ChartTitle = "Users";

        //Save the workbook
        workbook.SaveAs(@"d:\test\XlsIOOutput_PieChart.xlsx");
    }
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Private Sub CreatePieChart()
    Using excelEngine As ExcelEngine = New ExcelEngine()
        'Instantiate the application object
        Dim application As IApplication = excelEngine.Excel

        'Create a workbook
        Dim workbook As IWorkbook = application.Workbooks.Create(1)

        'Get the first sheet
        Dim worksheet As IWorksheet = workbook.Worksheets(0)

        'Add sample data for pie chart
        'Add headings in A1 and B1.
        worksheet.Range("A1").Value = "Products"
        worksheet.Range("B1").Value = "Users"

        'Add data from A2 till B4
        worksheet.Range("A2").Value = "XlsIO"
        worksheet.Range("B2").Value2 = 10000
        worksheet.Range("A3").Value = "DocIO"
        worksheet.Range("B3").Value2 = 8000
        worksheet.Range("A4").Value = "PDF"
        worksheet.Range("B4").Value2 = 12000

        'Add a pie chart and set data range in the worksheet
        Dim chart As IChartShape = worksheet.Charts.Add()
        chart.DataRange = worksheet.Range("A2:B4")
        chart.ChartType = ExcelChartType.Pie
        chart.IsSeriesInRows = False

        'Position chart in the worksheet
        chart.TopRow = 7
        chart.LeftColumn = 1
        chart.RightColumn = 7
        chart.BottomRow = 23

        'Set chart title
        chart.ChartTitle = "Users"

        'Save as Excel file
        workbook.SaveAs("d:\test1\XlsIOOutput_PieChart.xlsx")
    End Using
End Sub
{% endhighlight %}
{% endtabs %}
