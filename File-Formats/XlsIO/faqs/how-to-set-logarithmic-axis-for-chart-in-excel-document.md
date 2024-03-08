---
title: How to set Logarithmic axis for chart in Excel document | Syncfusion
description: Code example to set Logarithmic axis for chart in Excel document using Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# How to set Logarithmic axis for chart in Excel document?

The following code snippet shows how to set Logarithmic axis for chart in Excel document.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;
    FileStream inputStream = new FileStream("InputTemplate.xlsx", FileMode.Open, FileAccess.Read);
    IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelOpenType.Automatic);
    IWorksheet sheet = workbook.Worksheets[0];

    //Create a Chart
    IChartShape chart = sheet.Charts.Add();

    //Set Chart Type
    chart.ChartType = ExcelChartType.Column_Clustered;

    //Set data range in the worksheet
    chart.DataRange = sheet.Range["A1:C6"];

    //Set chart value axis
    IChartValueAxis valueAxis = chart.PrimaryValueAxis;

    //Set IsLogScale and log base
    valueAxis.IsLogScale = true;
    valueAxis.LogBase = 10;

    //Saving the workbook
    FileStream outputStream = new FileStream("Chart.xlsx", FileMode.Create, FileAccess.Write);
    workbook.SaveAs(outputStream);

    //Dispose streams
    outputStream.Dispose();
    inputStream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("InputTemplate.xlsx", ExcelOpenType.Automatic);
  IWorksheet sheet = workbook.Worksheets[0];

   //Create a Chart
    IChartShape chart = sheet.Charts.Add();

    //Set Chart Type
    chart.ChartType = ExcelChartType.Column_Clustered;

    //Set data range in the worksheet
    chart.DataRange = sheet.Range["A1:C6"];

    //Set chart value axis
    IChartValueAxis valueAxis = chart.PrimaryValueAxis;

    //Set IsLogScale and log base
    valueAxis.IsLogScale = true;
    valueAxis.LogBase = 10;

    //Saving the workbook
    workbook.SaveAs("Chart.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As New ExcelEngine()
    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Xlsx
    Dim workbook As IWorkbook = application.Workbooks.Open(InputTemplate.xlsx", ExcelOpenType.Automatic)
    Dim sheet As IWorksheet = workbook.Worksheets(0)

    ' Create a Chart
    Dim chart As IChartShape = sheet.Charts.Add()

    ' Set Chart Type
    chart.ChartType = ExcelChartType.Column_Clustered

    ' Set data range in the worksheet
    chart.DataRange = sheet.Range("A1:C6")

    ' Set chart value axis
    Dim valueAxis As IChartValueAxis = chart.PrimaryValueAxis

    ' Set IsLogScale and log base
    valueAxis.IsLogScale = True
    valueAxis.LogBase = 10

    ' Saving the workbook
    workbook.SaveAs(outputStream)

End Using
{% endhighlight %}
{% endtabs %}