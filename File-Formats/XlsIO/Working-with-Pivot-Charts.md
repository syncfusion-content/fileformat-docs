---
layout: Post
title: Working with Pivot Charts
description: Briefs about Pivot Charts in XlsIO
platform: File-formats
control: XlsIO
documentation: UG
---
**Document** **Properties**

# Working with Pivot Charts

PivotCharts are interactive graphical representations of PivotTable data that allows rapid analysis of the displayed data. In XlsIO, **PivotCharts** are created by __IChart__ interface by setting its pivot source as __PivotTable__.

I> XlsIO provides PivotCharts support for XLSX format.

LINK: To create a pivot table refer in Create Pivot Table section. 

The following code snippet illustrates how to create a PivotChart.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("PivotTable.xlsx");

IWorksheet worksheet = workbook.Worksheets[0];

IPivotTable pivotTable = worksheet.PivotTables[0];


//Adding a chart to workbook

IChart pivotChart = workbook.Charts.Add();

//Set PivotTable as PivotSource to the chart

pivotChart.PivotSource = pivotTable;

//Set PivotChart type

pivotChart.PivotChartType = ExcelChartType.Column_Clustered;

workbook.SaveAs("PivotChart.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("PivotTable.xlsx")

Dim worksheet As IWorksheet = workbook.Worksheets(0)

Dim pivotTable As IPivotTable = worksheet.PivotTables(0)

'Adding a chart to workbook

Dim pivotChart As IChart = workbook.Charts.Add()

'Set PivotTable as PivotSource to the chart

pivotChart.PivotSource = pivotTable

'Set PivotChart type

pivotChart.PivotChartType = ExcelChartType.Column_Clustered


workbook.SaveAs("PivotChart.xlsx")
workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

## PivotChart Options

The following code snippet shows how to set field buttons in a pivot chart.

I> PivotChart properties are exclusive for Excel 2010 version.

{% tabs %}  

{% highlight c# %}
//Adding Pivotchart to the workbook.

IChart pivotChart = workbook.Charts.Add();

//Set Field Buttons

pivotChart.ShowAllFieldButtons = false;

pivotChart.ShowAxisFieldButtons = false;

pivotChart.ShowLegendFieldButtons = false;

pivotChart.ShowReportFilterFieldButtons = false;

pivotChart.ShowValueFieldButtons = false;   



{% endhighlight %}

{% highlight vb %}
'Insert the Pivotchart sheet to the workbook

Dim pivotChartSheet As IChart = workbook.Charts.Add()

'Set Field Buttons

pivotChartSheet.ShowAllFieldButtons = False

pivotChartSheet.ShowAxisFieldButtons = False

pivotChartSheet.ShowLegendFieldButtons = False

pivotChartSheet.ShowReportFilterFieldButtons = False

pivotChartSheet.ShowValueFieldButtons = False



{% endhighlight %}

  {% endtabs %}  

# 

