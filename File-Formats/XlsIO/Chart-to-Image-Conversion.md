---
title: Chart to Image Conversion | Syncfusion
description: This section explains about Chart to Image conversion supported in XlsIO. Use XlsIORenderer class ChartRenderingOptions for specify Image format & quality.
platform: file-formats
control: XlsIO
documentation: UG
---

# Chart to image conversion

Refer to the following links for assemblies/nuget packages required based on platforms to convert the chart to image.

* [Assemblies Information](https://help.syncfusion.com/file-formats/xlsio/assemblies-required#converting-excel-chart-to-image) 
* [NuGet Information](https://help.syncfusion.com/file-formats/xlsio/nuget-packages-required#converting-charts-in-xlsio)

The following code snippet shows how to convert an Excel chart to an image using the [ChartToImageConverter](https://help.syncfusion.com/cr/file-formats/Syncfusion.ExcelChartToImageConverter.ChartToImageConverter.html) class.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;

  // Initialize XlsIORenderer
  application.XlsIORenderer = new XlsIORenderer();

  //Set converter chart image format to PNG
  application.XlsIORenderer.ChartRenderingOptions.ImageFormat = ExportImageFormat.Png;

  IWorkbook workbook = application.Workbooks.Open(File.OpenRead("Sample.xlsx"), ExcelOpenType.Automatic);
  IWorksheet worksheet = workbook.Worksheets[0];
  IChart chart = worksheet.Charts[0];

  //Creating the memory stream for chart image
  MemoryStream stream = new MemoryStream();

  //Saving the chart as image
  chart.SaveAsImage(stream);

  //Close and Dispose
  workbook.Close();
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;

  application.ChartToImageConverter = new ChartToImageConverter();
  application.ChartToImageConverter.ScalingMode = ScalingMode.Best;

  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
  IWorksheet worksheet = workbook.Worksheets[0];
  IChart chart = worksheet.Charts[0];

  //Creating the memory stream for chart image
  MemoryStream stream = new MemoryStream();

  //Saving the chart as image
  chart.SaveAsImage(stream);
  Image image = Image.FromStream(stream);

  //Saving image stream to file
  image.Save("Output.png");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx

  Dim ChartToImageConverter As chartToImageConverter = New ChartToImageConverter()
  application.ChartToImageConverter = ChartToImageConverter
  application.ChartToImageConverter.ScalingMode = ScalingMode.Best

  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
  Dim worksheet As IWorksheet = workbook.Worksheets(0)
  Dim chart As IChart = worksheet.Charts(0)

  'Creating the memory stream for chart image
  Dim stream As New MemoryStream()

  'Saving the chart as image
  chart.SaveAsImage(stream)
  Dim image As Image = Image.FromStream(stream)

  'Saving image stream to file
  image.Save("Output.png")
End Using
{% endhighlight %}
{% endtabs %}  

A complete working example to convert Excel chart to image in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Chart%20to%20Image/Chart%20to%20Image).  

N> 1. Instance of [XlsIORenderer](https://help.syncfusion.com/cr/aspnetcore-js2/Syncfusion.XlsIORenderer.XlsIORenderer.html) class is mandatory to convert the chart to image using .NET Standard 2.0 assemblies.
N> 2. In .NET Standard, the Image format and quality can be specified using the [ChartRenderingOptions](https://help.syncfusion.com/cr/aspnetcore-js2/Syncfusion.XlsIORenderer.XlsIORenderer.html#Syncfusion_XlsIORenderer_XlsIORenderer_ChartRenderingOptions) property of XlsIORenderer class. By default the [ImageFormat](https://help.syncfusion.com/cr/file-formats/Syncfusion.Drawing.ImageFormat.html) for chart is set to JPEG and [ScalingMode](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ScalingMode.html) is set to Best.
N> 3. Chart conversion to image and PDF are supported from .NET Framework 4.0 and .NET Standard 2.0 onwards 
N> 4. Chart to Image conversion also works proper in both Blazor server-side and client-side.

## Supported chart types
XlsIO supports the following chart types in image conversion.
<table>
<tr>
<td>
{{'**Chart Type**'| markdownify }}
</td>
<td>
{{'**Chart Subtypes**'| markdownify }}
</td>
</tr>
<tr>
<td>
Area
</td>
<td>
* Area<br/>
* Area_Stacked<br/>
* Area_Stacked_100<br/>
* Area_3D
</td>
</tr>
<tr>
<td>
Bar
</td>
<td>
* Bar_Clustered<br/>
* Bar_Stacked<br/>
* Bar_Stacked_100<br/>
* Bar_Clustered_3D<br/>
* Bar_Stacked_3D<br/>
* Bar_Stacked_100_3D
</td>
</tr>
<tr>
<td>
Bubble
</td>
<td>
Bubble
</td>
</tr>
<tr>
<td>
Column
</td>
<td>
* Column_Clustered<br/>
* Column_Stacked<br/>
* Column_Stacked_100<br/>
* Column_3D<br/>
* Column_Clustered_3D<br/>
* Column_Stacked_3D<br/>
* Column_Stacked_100_3D
</td>
</tr>
<tr>
<td>
Doughnut
</td>
<td>
* Doughnut<br/>
* Doughnut_Exploded
</td>
</tr>
<tr>
<td>
Line
</td>
<td>
* Line<br/>
* Line_Markers<br/>
* Line_3D
</td>
</tr>
<tr>
<td>
Pie
</td>
<td>
* Pie<br/>
* Pie_Exploded<br/>
* Pie_3D<br/>
* Pie_Exploded_3D
</td>
</tr>
<tr>
<td>
Radar
</td>
<td>
* Radar<br/>
* Radar_Filled<br/>
* Radar_Markers
</td>
</tr>
<tr>
<td>
Scatter
</td>
<td>
* Scatter_Line<br/>
* Scatter_Line_Markers<br/>
* Scatter_Markers<br/>
* Scatter_SmoothedLine<br/>
* Scatter_SmoothedLine_Markers
</td>
</tr>
<tr>
<td>
Stock
</td>
<td>
* Stock_HighLowClose<br/>
* Stock_OpenHighLowClose
</td>
</tr>
<tr>
<td>
Excel 2016 Charts
</td>
<td>
* Funnel<br/>* Waterfall<br/>* Histogram<br/>* Pareto<br/></td>
</tr>
</table>

N> From the above supported chart types table, Waterfall and Line_3D charts are not supported in chart to image conversion in .NET Standard 2.0 onwards.

N> Only embedded charts are supported in chart to image conversion. Chart sheets are not supported.

## Supported chart elements
XlsIO supports the following chart elements in image conversion:
![Chart to Image Conversion](Working-With-Charts_images/chart-elements.jpeg)

**Chart Elements:**
1. Axis
2. Axis titles
3. Chart title
4. Data labels
5. Grid lines
6. Legend
7. Trend line
