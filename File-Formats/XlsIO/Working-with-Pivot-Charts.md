---
title: Working with Pivot Charts | Syncfusion
description: Learn here all about working with the Pivot Charts in the Syncfusion Excel (XlsIO) Library and more.
platform: file-formats
control: XlsIO
documentation: UG 
---

# Working with Pivot Charts in Excel Library

**PivotCharts** are interactive graphical representations of **PivotTable** data that allows rapid analysis of the displayed data. In XlsIO, **PivotCharts** are created by [IChart](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IChart.html) interface by setting its pivot source as **PivotTable**.

N> XlsIO supports PivotCharts only for XLSX format.

To create a pivot table, refer [Create Pivot Table](/file-formats/xlsio/working-with-pivot-tables#create-a-pivot-table). 

The following code snippet illustrates how to create a PivotChart.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  FileStream fileStream = new FileStream("PivotTable.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];
  IPivotTable pivotTable = worksheet.PivotTables[0];

  //Adding a chart to workbook
  IChart pivotChart = workbook.Charts.Add();

  //Set PivotTable as PivotSource to the chart
  pivotChart.PivotSource = pivotTable;

  //Set PivotChart type
  pivotChart.PivotChartType = ExcelChartType.Column_Clustered;

  string fileName = "PivotChart.xlsx";

  //Saving the workbook as stream
  FileStream stream = new FileStream(fileName, FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
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
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = ExcelEngine.Excel
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
End Using
{% endhighlight %}
{% endtabs %}  

## PivotChart Options

The following code snippet shows how to set field buttons in a pivot chart.

N> The PivotChart properties are supported exclusively from Excel 2010 onwards.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Adding PivotChart to the workbook
IChart pivotChart = workbook.Charts.Add();

//Set Field Buttons
pivotChart.ShowAllFieldButtons = false;
pivotChart.ShowAxisFieldButtons = false;
pivotChart.ShowLegendFieldButtons = false;
pivotChart.ShowReportFilterFieldButtons = false;
pivotChart.ShowValueFieldButtons = false;  
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Adding PivotChart to the workbook
IChart pivotChart = workbook.Charts.Add();

//Set Field Buttons
pivotChart.ShowAllFieldButtons = false;
pivotChart.ShowAxisFieldButtons = false;
pivotChart.ShowLegendFieldButtons = false;
pivotChart.ShowReportFilterFieldButtons = false;
pivotChart.ShowValueFieldButtons = false;   
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Insert the PivotChart sheet to the workbook
Dim pivotChartSheet As IChart = workbook.Charts.Add()

'Set Field Buttons
pivotChartSheet.ShowAllFieldButtons = False
pivotChartSheet.ShowAxisFieldButtons = False
pivotChartSheet.ShowLegendFieldButtons = False
pivotChartSheet.ShowReportFilterFieldButtons = False
pivotChartSheet.ShowValueFieldButtons = False
{% endhighlight %}
{% endtabs %}  
  
A complete working example to create pivot chart in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Pivot%20Charts/Create%20Pivot%20Chart). 

## PivotChart Series

When pivot chart is created with pivot table as data source, Syncfusion XlsIO cannot create the series because the range of the pivot table is different from normal worksheet range. This is the limitation of XlsIO. To use any chart series formatting, the series should be added manually.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
pivotChartSheet.Series.Add(ExcelChartType.Column_Stacked);
pivotChartSheet.Series[0].SerieFormat.CommonSerieOptions.Overlap = 100;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
pivotChartSheet.Series.Add(ExcelChartType.Column_Stacked);
pivotChartSheet.Series[0].SerieFormat.CommonSerieOptions.Overlap = 100;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
pivotChartSheet.Series.Add(ExcelChartType.Column_Stacked)
pivotChartSheet.Series(0).SerieFormat.CommonSerieOptions.Overlap = 100
{% endhighlight %}
{% endtabs %} 

 