---
title: Chart to Image Conversion
description: Briefs about Chart to Image conversion supported in XlsIO
platform: File-formats
control: XlsIO
documentation: UG
---

# Chart to image conversion

The following code snippet shows how to convert an Excel chart to an image using the **ExcelChartToImageConverter** class.

{% tabs %}
{% highlight c# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

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

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013

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

{% highlight UWP %}
//XlsIO supports chart to image conversion in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms alone.
{% endhighlight %}

{% highlight asp.net core %}
//XlsIO supports chart to image conversion in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms alone.
{% endhighlight %}

{% highlight Xamarin %}
//XlsIO supports chart to image conversion in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms alone.
{% endhighlight %}
{% endtabs %}  

N> Chart conversion to image and PDF are supported from .NET Framework 4.0 onwards.

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

## Supported chart elements
XlsIO supports the following chart elements in image conversion:
![](Working-With-Charts_images/chart-elements.jpeg)

**Chart Elements:**
1. Axis
2. Axis titles
3. Chart title
4. Data labels
5. Grid lines
6. Legend
7. Trend line
