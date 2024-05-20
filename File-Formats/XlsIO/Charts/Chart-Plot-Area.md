---
title: Modify the Appearance of Plot Area | Syncfusion
description: Learn how to modify the appearance of plot area in a chart in an Excel document using Syncfusion .NET Excel (XlsIO) library without Microsoft Excel.
platform: file-formats
control: XlsIO
documentation: UG
---

# Chart Plot Area

The plot area refers to the region that represents the plotted data in a chart. Using XlsIO, you can **customize the plot area in the chart**.

## Customization of Border

The following code snippet illustrates how to modify the border of the plot area.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Format Plot Area
IChartFrameFormat chartPlotArea = chart.PlotArea;

//Set border line pattern, color, line weight.
chartPlotArea.Border.LinePattern = ExcelChartLinePattern.Solid;
chartPlotArea.Border.LineColor = Color.Blue;
chartPlotArea.Border.LineWeight = ExcelChartLineWeight.Hairline;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Format Plot Area
IChartFrameFormat chartPlotArea = chart.PlotArea;

//Set border line pattern, color, line weight.
chartPlotArea.Border.LinePattern = ExcelChartLinePattern.Solid;
chartPlotArea.Border.LineColor = Color.Blue;
chartPlotArea.Border.LineWeight = ExcelChartLineWeight.Hairline;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Format Plot Area
IChartFrameFormat chartPlotArea = chart.PlotArea

'Set border line pattern, color, line weight.
chartPlotArea.Border.LinePattern = ExcelChartLinePattern.Solid
chartPlotArea.Border.LineColor = Color.Blue
chartPlotArea.Border.LineWeight = ExcelChartLineWeight.Hairline
{% endhighlight %}
{% endtabs %}

## Customization of Color

The following code snippet illustrates how to fill the color in plot area.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Set fill type and color.
chartPlotArea.Fill.FillType = ExcelFillType.Gradient;
chartPlotArea.Fill.GradientColorType = ExcelGradientColor.TwoColor;
chartPlotArea.Fill.BackColor = Color.FromArgb(205, 217, 234);
chartPlotArea.Fill.ForeColor = Color.White;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Set fill type and color.
chartPlotArea.Fill.FillType = ExcelFillType.Gradient;
chartPlotArea.Fill.GradientColorType = ExcelGradientColor.TwoColor;
chartPlotArea.Fill.BackColor = Color.FromArgb(205, 217, 234);
chartPlotArea.Fill.ForeColor = Color.White;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Set fill type and color.
chartPlotArea.Fill.FillType = ExcelFillType.Gradient
chartPlotArea.Fill.GradientColorType = ExcelGradientColor.TwoColor
chartPlotArea.Fill.BackColor = Color.FromArgb(205, 217, 234)
chartPlotArea.Fill.ForeColor = Color.White
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

    //Format Plot Area
    IChartFrameFormat chartPlotArea = chart.PlotArea;

    //Set border line pattern, color, line weight.
    chartPlotArea.Border.LinePattern = ExcelChartLinePattern.Solid;
    chartPlotArea.Border.LineColor = Color.Blue;
    chartPlotArea.Border.LineWeight = ExcelChartLineWeight.Hairline;

    //Set fill type and color.
    chartPlotArea.Fill.FillType = ExcelFillType.Gradient;
    chartPlotArea.Fill.GradientColorType = ExcelGradientColor.TwoColor;
    chartPlotArea.Fill.BackColor = Color.FromArgb(205, 217, 234);
    chartPlotArea.Fill.ForeColor = Color.White;

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
    IWorkbook workbook = application.Workbooks.Open(@"D:\Support Sample\Format Chart Area\Format Chart Area\Data\InputTemplate.xlsx");
    IWorksheet sheet = workbook.Worksheets[0];
    IChartShape chart = sheet.Charts[0];

    //Format Plot Area
    IChartFrameFormat chartPlotArea = chart.PlotArea;

    //Set border line pattern, color, line weight.
    chartPlotArea.Border.LinePattern = ExcelChartLinePattern.Solid;
    chartPlotArea.Border.LineColor = Color.Blue;
    chartPlotArea.Border.LineWeight = ExcelChartLineWeight.Hairline;

    //Set fill type and color.
    chartPlotArea.Fill.FillType = ExcelFillType.Gradient;
    chartPlotArea.Fill.GradientColorType = ExcelGradientColor.TwoColor;
    chartPlotArea.Fill.BackColor = Color.FromArgb(205, 217, 234);
    chartPlotArea.Fill.ForeColor = Color.White;

    //Saving the workbook
    workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Xlsx
    Dim workbook As IWorkbook = application.Workbooks.Open("D:\Support Sample\Format Chart Area\Format Chart Area\Data\InputTemplate.xlsx")
    Dim sheet As IWorksheet = workbook.Worksheets(0)
    Dim chart As IChartShape = sheet.Charts(0)

    'Format Plot Area
    Dim chartPlotArea As IChartFrameFormat = chart.PlotArea

    'Set border line pattern, color, line weight.
    chartPlotArea.Border.LinePattern = ExcelChartLinePattern.Solid
    chartPlotArea.Border.LineColor = Color.Blue
    chartPlotArea.Border.LineWeight = ExcelChartLineWeight.Hairline

    'Set fill type and color.
    chartPlotArea.Fill.FillType = ExcelFillType.Gradient
    chartPlotArea.Fill.GradientColorType = ExcelGradientColor.TwoColor
    chartPlotArea.Fill.BackColor = Color.FromArgb(205, 217, 234)
    chartPlotArea.Fill.ForeColor = Color.White

    'Saving the workbook
    workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}
{% endtabs %}

A complete working example to format a chart plot area in C# is present on [this GitHub page]().


## Add Image in Plot Area

XlsIO allows you to add image in plot area using [UserPicture](https://help.syncfusion.com/cr/windowsforms/Syncfusion.XlsIO.IFill.html#Syncfusion_XlsIO_IFill_UserPicture_System_Drawing_Image_System_String_) of [IFill](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IFill.html) interface.

The following code example illustrates how to fill the image in chart plot area.

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

  //Filling plot area of the chart with picture
  chart.PlotArea.Fill.UserPicture(image, "Image");

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

  //Filling plot area of the chart with picture
  chart.PlotArea.Fill.UserPicture("Image.png");

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

  'Filling plot area of the chart with picture
  chart.PlotArea.Fill.UserPicture("Image.png")

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}
{% endtabs %}

A complete working example to fill the image in plot area in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Create%20and%20Edit%20Charts/Picture%20in%20Plot%20Area).

## Set the Transparency level

The following code snippet illustrates how to make transparency in plot area.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

// Set the transparency of the plot area.
chartPlotArea.Fill.Transparency = 0.5;

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

// Set the transparency of the plot area.
chartPlotArea.Fill.Transparency = 0.5;

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Set the transparency of the plot area.
chartPlotArea.Fill.Transparency = 0.5

{% endhighlight %}
{% endtabs %}

N> [Transparency](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IFill.html#Syncfusion_XlsIO_IFill_Transparency) is only applicable when [FillType](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IFill.html#Syncfusion_XlsIO_IFill_FillType) is set as SolidColor. Color-shaded fill is represented as a floating-point value ranging from 0.0 (Clear) to 1.0 (Opaque).

## Set the position of Plot Area

The following code snippet illustrates how to position the plot area in chart.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//Set the position for plot area.
chartPlotArea.Layout.LeftMode = LayoutModes.auto;
chartPlotArea.Layout.TopMode = LayoutModes.factor;
chartPlotArea.Layout.LayoutTarget = LayoutTargets.outer;

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

//Set the position for plot area.
chartPlotArea.Layout.LeftMode = LayoutModes.auto;
chartPlotArea.Layout.TopMode = LayoutModes.factor;
chartPlotArea.Layout.LayoutTarget = LayoutTargets.outer;

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Set the position for plot area.
chartPlotArea.Layout.LeftMode = LayoutModes.auto
chartPlotArea.Layout.TopMode = LayoutModes.factor
chartPlotArea.Layout.LayoutTarget = LayoutTargets.outer

{% endhighlight %}
{% endtabs %}