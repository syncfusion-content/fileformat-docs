---
title: Modify the Appearance of Chart Area | Syncfusion
description: Learn how to modify the appearance of chart area in a chart in an Excel document using Syncfusion .NET Excel (XlsIO) library without Microsoft Excel.
platform: file-formats
control: XlsIO
documentation: UG
---

# Chart Area in Excel document

Chart area refers to the space that contains the entire chart or graph within a document. It includes all elements of the chart, such as data points, labels, axes, and the plot area. Using XlsIO, you **can customize various aspects of the chart area in the chart**.

## Customization of Border

The following code snippet illustrates how to modify the border of the chart area.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Format Chart Area
IChartFrameFormat chartArea = chart.ChartArea;

//Set border line pattern, color, line weight.
chartArea.Border.LinePattern = ExcelChartLinePattern.Solid;
chartArea.Border.LineColor = Syncfusion.Drawing.Color.Blue;
chartArea.Border.LineWeight = ExcelChartLineWeight.Hairline;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Format Chart Area
IChartFrameFormat chartArea = chart.ChartArea;

//Set border line pattern, color, line weight.
chartArea.Border.LinePattern = ExcelChartLinePattern.Solid;
chartArea.Border.LineColor = Syncfusion.Drawing.Color.Blue;
chartArea.Border.LineWeight = ExcelChartLineWeight.Hairline;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Format Chart Area
IChartFrameFormat chartArea = chart.ChartArea

'Set border line pattern, color, line weight.
chartArea.Border.LinePattern = ExcelChartLinePattern.Solid
chartArea.Border.LineColor = Syncfusion.Drawing.Color.Blue
chartArea.Border.LineWeight = ExcelChartLineWeight.Hairline
{% endhighlight %}
{% endtabs %}

## Customization of Color

The following code snippet illustrates how to fill the color in chart area.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Set fill type and fill colors.
chartArea.Fill.FillType = ExcelFillType.Gradient;
chartArea.Fill.GradientColorType = ExcelGradientColor.TwoColor;
chartArea.Fill.BackColor = Syncfusion.Drawing.Color.FromArgb(205, 217, 234);
chartArea.Fill.ForeColor = Syncfusion.Drawing.Color.White;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Set fill type and fill colors.
chartArea.Fill.FillType = ExcelFillType.Gradient;
chartArea.Fill.GradientColorType = ExcelGradientColor.TwoColor;
chartArea.Fill.BackColor = Syncfusion.Drawing.Color.FromArgb(205, 217, 234);
chartArea.Fill.ForeColor = Syncfusion.Drawing.Color.White;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Set fill type and fill colors.
chartArea.Fill.FillType = ExcelFillType.Gradient
chartArea.Fill.GradientColorType = ExcelGradientColor.TwoColor
chartArea.Fill.BackColor = Syncfusion.Drawing.Color.FromArgb(205, 217, 234)
chartArea.Fill.ForeColor = Syncfusion.Drawing.Color.White
{% endhighlight %}
{% endtabs %}

The complete code snippet illustrating the above options is shown below.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  FileStream inputStream = new FileStream("../../../Data/InputTemplate.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelOpenType.Automatic);  
  IWorksheet sheet = workbook.Worksheets[0];
  IChartShape chart = sheet.Charts[0];

  //Format Chart Area
  IChartFrameFormat chartArea = chart.ChartArea;

  //Set border line pattern, color, line weight.
  chartArea.Border.LinePattern = ExcelChartLinePattern.Solid;
  chartArea.Border.LineColor = Syncfusion.Drawing.Color.Blue;
  chartArea.Border.LineWeight = ExcelChartLineWeight.Hairline;

  //Set fill type and fill colors.
  chartArea.Fill.FillType = ExcelFillType.Gradient;
  chartArea.Fill.GradientColorType = ExcelGradientColor.TwoColor;
  chartArea.Fill.BackColor = Syncfusion.Drawing.Color.FromArgb(205, 217, 234);
  chartArea.Fill.ForeColor = Syncfusion.Drawing.Color.White;

  //Saving the workbook as stream
  FileStream outputStream = new FileStream("Output.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(outputStream);
  outputStream.Dispose();
  inputStream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Open("InputTemplate.xlsx");
  IWorksheet sheet = workbook.Worksheets[0];
  IChartShape chart = sheet.Charts[0];

  //Format Chart Area
  IChartFrameFormat chartArea = chart.ChartArea;

  //Set border line pattern, color, line weight.
  chartArea.Border.LinePattern = ExcelChartLinePattern.Solid;
  chartArea.Border.LineColor = Color.Blue;
  chartArea.Border.LineWeight = ExcelChartLineWeight.Hairline;

  //Set fill type and fill colors.
  chartArea.Fill.FillType = ExcelFillType.Gradient;
  chartArea.Fill.GradientColorType = ExcelGradientColor.TwoColor;
  chartArea.Fill.BackColor = Color.FromArgb(205, 217, 234);
  chartArea.Fill.ForeColor = Color.White;

  //Saving the workbook as stream
  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Open("InputTemplate.xlsx")
  Dim sheet As IWorksheet = workbook.Worksheets(0)
  Dim chart As IChartShape = sheet.Charts(0)

  'Format Chart Area
  Dim chartArea As IChartFrameFormat = chart.ChartArea

  'Set border line pattern, color, line weight.
  chartArea.Border.LinePattern = ExcelChartLinePattern.Solid
  chartArea.Border.LineColor = Color.Blue
  chartArea.Border.LineWeight = ExcelChartLineWeight.Hairline

  'Set fill type and fill colors.
  chartArea.Fill.FillType = ExcelFillType.Gradient
  chartArea.Fill.GradientColorType = ExcelGradientColor.TwoColor
  chartArea.Fill.BackColor = Color.FromArgb(205, 217, 234)
  chartArea.Fill.ForeColor = Color.White

  'Saving the workbook as stream
  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}
{% endtabs %}

A complete working example to format a chart area in C# is present on [this GitHub page]().

## Add Image in Chart Area

XlsIO allows you to add image in chart area using [UserPicture](https://help.syncfusion.com/cr/windowsforms/Syncfusion.XlsIO.IFill.html#Syncfusion_XlsIO_IFill_UserPicture_System_Drawing_Image_System_String_) of [IFill](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IFill.html) interface.

The following code example illustrates how to fill the image in chart area.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Adding chart in the worksheet
  IChartShape chart = worksheet.Charts.Add();
  chart.DataRange = worksheet.Range["A1:C6"];
  chart.ChartType = ExcelChartType.Column_Clustered;
  chart.IsSeriesInRows = false;

  //Getting an image from the stream
  FileStream imageStream = new FileStream("Image.png", FileMode.Open, FileAccess.Read);
  Image image = Image.FromStream(imageStream);

  //Filling chart area of the chart with picture
  chart.ChartArea.Fill.UserPicture(image, "Image");

  //Saving the workbook as stream
  FileStream stream = new FileStream("Output.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
  IWorksheet worksheet = workbook.Worksheets[0];

  //Adding chart in the worksheet
  IChartShape chart = worksheet.Charts.Add();
  chart.DataRange = worksheet.Range["A1:C6"];
  chart.ChartType = ExcelChartType.Column_Clustered;
  chart.IsSeriesInRows = false;

  //Filling chart area of the chart with picture
  chart.ChartArea.Fill.UserPicture("Image.png");

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Adding chart in the worksheet
  Dim chart As IChartShape = worksheet.Charts.Add
  chart.DataRange = worksheet.Range("A1:C6")
  chart.ChartType = ExcelChartType.Column_Clustered
  chart.IsSeriesInRows = False

  'Filling chart area of the chart with picture
  chart.ChartArea.Fill.UserPicture("Image.png")

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}
{% endtabs %}

A complete working example to fill the image in chart area in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Create%20and%20Edit%20Charts/Picture%20in%20Chart%20Area).

## Set the Transparency level

The following code snippet illustrates how to apply transparency in chart area.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Set the transparency of the chart area.
chartArea.Fill.Transparency = 0.5;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Set the transparency of the chart area.
chartArea.Fill.Transparency = 0.5;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Set the transparency of the chart area.
chartArea.Fill.Transparency = 0.5
{% endhighlight %}
{% endtabs %}

N> [Transparency](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IFill.html#Syncfusion_XlsIO_IFill_Transparency) is only applicable when [FillType](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IFill.html#Syncfusion_XlsIO_IFill_FillType) is set as SolidColor. Color-shaded fill is represented as a floating-point value ranging from 0.0 (Clear) to 1.0 (Opaque).

## See Also
* [How to create Excel area chart in C#, VB.NET?](https://support.syncfusion.com/kb/article/7478/how-to-create-excel-area-chart-in-c-vb-net)