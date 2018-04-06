---
title: Working with Pivot Charts
description: Briefs about Pivot Charts in XlsIO
platform: File-formats
control: XlsIO
documentation: UG 
---

# Working with Pivot Charts

PivotCharts are interactive graphical representations of PivotTable data that allows rapid analysis of the displayed data. In XlsIO, **PivotCharts** are created by __IChart__ interface by setting its pivot source as __PivotTable__.

N> XlsIO provides PivotCharts support only for XLSX format.

To create a pivot table refer [Create Pivot Table](/file-formats/xlsio/working-with-pivot-tables#create-a-pivot-table). 

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
{% highlight UWP %}
//Gets assembly
Assembly assembly = typeof(App).GetTypeInfo().Assembly;

//Gets input Excel document from embedded resource collection
Stream inputStream = assembly.GetManifestResourceStream("PivotChart.PivotTable.xlsx");

ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = await application.Workbooks.OpenAsync(inputStream);
IWorksheet worksheet = workbook.Worksheets[0];
IPivotTable pivotTable = workbook.Worksheets[1].PivotTables[0];

//Adding a chart to workbook
IChart pivotChart = workbook.Charts.Add();

//Set PivotTable as PivotSource to the chart
pivotChart.PivotSource = pivotTable;

//Set PivotChart type
pivotChart.PivotChartType = ExcelChartType.Column_Clustered;

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "PivotChart";
savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await workbook.SaveAsAsync(storageFile);

workbook.Close();
excelEngine.Dispose();

{% endhighlight %}
{% highlight asp.net core %}
ExcelEngine excelEngine = new ExcelEngine();
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
workbook.Close();
excelEngine.Dispose();

{% endhighlight %}
{% highlight Xamarin %}
//Gets assembly
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
           
//Gets input Excel document from embedded resource collection
Stream inputStream = assembly.GetManifestResourceStream("PivotChart.PivotTable.xlsx");

ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open(inputStream);
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
MemoryStream outputStream = new MemoryStream();
workbook.SaveAs(outputStream);

workbook.Close();
excelEngine.Dispose();

//Save the Excel file
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    await DependencyService.Get<ISaveWindowsPhone>().Save(fileName, "application/msexcel", outputStream);
else
    DependencyService.Get<ISave>().Save(fileName, "application/msexcel", outputStream);

//Dispose the input and output stream instances
inputStream.Dispose();
outputStream.Dispose();

{% endhighlight %}

  {% endtabs %}  

## PivotChart Options

The following code snippet shows how to set field buttons in a pivot chart.

N> PivotChart properties are supported exclusively from Excel 2010 onwards.

{% tabs %}  

{% highlight c# %}
//Adding PivotChart to the workbook
IChart pivotChart = workbook.Charts.Add();

//Set Field Buttons
pivotChart.ShowAllFieldButtons = false;
pivotChart.ShowAxisFieldButtons = false;
pivotChart.ShowLegendFieldButtons = false;
pivotChart.ShowReportFilterFieldButtons = false;
pivotChart.ShowValueFieldButtons = false;   

{% endhighlight %}

{% highlight vb %}
'Insert the PivotChart sheet to the workbook
Dim pivotChartSheet As IChart = workbook.Charts.Add()

'Set Field Buttons
pivotChartSheet.ShowAllFieldButtons = False
pivotChartSheet.ShowAxisFieldButtons = False
pivotChartSheet.ShowLegendFieldButtons = False
pivotChartSheet.ShowReportFilterFieldButtons = False
pivotChartSheet.ShowValueFieldButtons = False

{% endhighlight %}

{% highlight UWP %}
//Adding PivotChart to the workbook
IChart pivotChart = workbook.Charts.Add();

//Set Field Buttons
pivotChart.ShowAllFieldButtons = false;
pivotChart.ShowAxisFieldButtons = false;
pivotChart.ShowLegendFieldButtons = false;
pivotChart.ShowReportFilterFieldButtons = false;
pivotChart.ShowValueFieldButtons = false;  

{% endhighlight %}
{% highlight asp.net core %}
//Adding PivotChart to the workbook
IChart pivotChart = workbook.Charts.Add();

//Set Field Buttons
pivotChart.ShowAllFieldButtons = false;
pivotChart.ShowAxisFieldButtons = false;
pivotChart.ShowLegendFieldButtons = false;
pivotChart.ShowReportFilterFieldButtons = false;
pivotChart.ShowValueFieldButtons = false;  

{% endhighlight %}
{% highlight Xamarin %}
//Adding PivotChart to the workbook
IChart pivotChart = workbook.Charts.Add();

//Set Field Buttons
pivotChart.ShowAllFieldButtons = false;
pivotChart.ShowAxisFieldButtons = false;
pivotChart.ShowLegendFieldButtons = false;
pivotChart.ShowReportFilterFieldButtons = false;
pivotChart.ShowValueFieldButtons = false;   

{% endhighlight %}

  {% endtabs %}  


