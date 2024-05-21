---
title: Modify the Appearance of Axes in Chart | Syncfusion
description: Learn how to modify the appearance of axes in a chart in an Excel document using the Syncfusion .NET Excel (XlsIO) library without Microsoft Excel.
platform: file-formats
control: XlsIO
documentation: UG
---

# Chart Axis in Excel document

Charts typically have two axes that are used to measure and categorize data.
-  Horizontal axis (also known as category axis or x axis).
-  Vertical axis (also known as value axis or y axis).

Using XlsIO, you can **customize the axis in the chart**.

## Set the Axis Title

The following code snippet illustrates how to set the title in axis.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Set the horizontal (category) axis title.
chart.PrimaryCategoryAxis.Title = "Months";
//Set the Vertical (value) axis title.
chart.PrimaryValueAxis.Title = "Precipitation,in.";
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Set the horizontal (category) axis title.
chart.PrimaryCategoryAxis.Title = "Months";
//Set the Vertical (value) axis title.
chart.PrimaryValueAxis.Title = "Precipitation,in.";
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Set the horizontal (category) axis title.
chart.PrimaryCategoryAxis.Title = "Months"
'Set the vertical (value) axis title.
chart.PrimaryValueAxis.Title = "Precipitation,in."
{% endhighlight %}
{% endtabs %}

## Customization of Border

The following code snippet illustrates how to customize the border of Horizontal and vertical category axis.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Customize the horizontal category axis.
chart.PrimaryCategoryAxis.Border.LinePattern = ExcelChartLinePattern.CircleDot;
chart.PrimaryCategoryAxis.Border.LineColor = Syncfusion.Drawing.Color.Blue;
chart.PrimaryCategoryAxis.Border.LineWeight = ExcelChartLineWeight.Hairline;

//Customize the vertical category axis.
chart.PrimaryValueAxis.Border.LinePattern = ExcelChartLinePattern.CircleDot;
chart.PrimaryValueAxis.Border.LineColor = Syncfusion.Drawing.Color.Blue;
chart.PrimaryValueAxis.Border.LineWeight = ExcelChartLineWeight.Hairline;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Customize the horizontal category axis.
chart.PrimaryCategoryAxis.Border.LinePattern = ExcelChartLinePattern.CircleDot;
chart.PrimaryCategoryAxis.Border.LineColor = Color.Blue;
chart.PrimaryCategoryAxis.Border.LineWeight = ExcelChartLineWeight.Hairline;

//Customize the vertical category axis.
chart.PrimaryValueAxis.Border.LinePattern = ExcelChartLinePattern.CircleDot;
chart.PrimaryValueAxis.Border.LineColor = Color.Blue;
chart.PrimaryValueAxis.Border.LineWeight = ExcelChartLineWeight.Hairline;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Customize the horizontal category axis.
chart.PrimaryCategoryAxis.Border.LinePattern = ExcelChartLinePattern.CircleDot
chart.PrimaryCategoryAxis.Border.LineColor = Color.Blue
chart.PrimaryCategoryAxis.Border.LineWeight = ExcelChartLineWeight.Hairline

'Customize the vertical value axis.
chart.PrimaryValueAxis.Border.LinePattern = ExcelChartLinePattern.CircleDot
chart.PrimaryValueAxis.Border.LineColor = Color.Blue
chart.PrimaryValueAxis.Border.LineWeight = ExcelChartLineWeight.Hairline
{% endhighlight %}
{% endtabs %}

## Customization of Font

The following code snippet illustrates how to customize the border of Horizontal and vertical category axis.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Customize the horizontal category axis font.
chart.PrimaryCategoryAxis.Font.Color = ExcelKnownColors.Red;
chart.PrimaryCategoryAxis.Font.FontName = "Calibri";
chart.PrimaryCategoryAxis.Font.Bold = true;
chart.PrimaryCategoryAxis.Font.Size = 20;

//Customize the vertical category axis font.
chart.PrimaryValueAxis.Font.Color = ExcelKnownColors.Red;
chart.PrimaryValueAxis.Font.FontName = "Calibri";
chart.PrimaryValueAxis.Font.Bold = true;
chart.PrimaryValueAxis.Font.Size = 20;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Customize the horizontal category axis font.
chart.PrimaryCategoryAxis.Font.Color = ExcelKnownColors.Red;
chart.PrimaryCategoryAxis.Font.FontName = "Calibri";
chart.PrimaryCategoryAxis.Font.Bold = true;
chart.PrimaryCategoryAxis.Font.Size = 20;

//Customize the vertical category axis font.
chart.PrimaryValueAxis.Font.Color = ExcelKnownColors.Red;
chart.PrimaryValueAxis.Font.FontName = "Calibri";
chart.PrimaryValueAxis.Font.Bold = true;
chart.PrimaryValueAxis.Font.Size = 20;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Customize the horizontal category axis font.
chart.PrimaryCategoryAxis.Font.Color = ExcelKnownColors.Red
chart.PrimaryCategoryAxis.Font.FontName = "Calibri"
chart.PrimaryCategoryAxis.Font.Bold = True
chart.PrimaryCategoryAxis.Font.Size = 20

'Customize the vertical value axis font.
chart.PrimaryValueAxis.Font.Color = ExcelKnownColors.Red
chart.PrimaryValueAxis.Font.FontName = "Calibri"
chart.PrimaryValueAxis.Font.Bold = True
chart.PrimaryValueAxis.Font.Size = 20
{% endhighlight %}
{% endtabs %}

## Text Angle Rotation

The following code snippet illustrates how to rotate the text angle for the axis title area.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Axis title area text angle rotation.
chart.PrimaryValueAxis.TitleArea.TextRotationAngle = 90;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Axis title area text angle rotation.
chart.PrimaryValueAxis.TitleArea.TextRotationAngle = 90;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Axis title area text angle rotation.
chart.PrimaryValueAxis.TitleArea.TextRotationAngle = 90
{% endhighlight %}
{% endtabs %}

## Set the Maximum value in Axis

The following code snippet illustrates how to set the maximum value in the axis.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Maximum value in the axis.
chart.PrimaryValueAxis.MaximumValue = 14.0;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Maximum value in the axis.
chart.PrimaryValueAxis.MaximumValue = 14.0;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Maximum value in the axis.
chart.PrimaryValueAxis.MaximumValue = 14.0
{% endhighlight %}
{% endtabs %}

## Set the Number format in Axis

The following code snippet illustrates how to set the number format in the axis.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Number format for axis.
chart.PrimaryValueAxis.NumberFormat = "0.0";
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Number format for axis.
chart.PrimaryValueAxis.NumberFormat = "0.0";
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Number format for axis.
chart.PrimaryValueAxis.NumberFormat = "0.0"
{% endhighlight %}
{% endtabs %}

## Manage Gridline Visibility

The following code snippet illustrates how to hide or show major and minor gridlines.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Hiding major gridlines.
chart.PrimaryValueAxis.HasMajorGridLines = false;

//Showing minor gridlines.
chart.PrimaryValueAxis.HasMinorGridLines = true;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Hiding major gridlines.
chart.PrimaryValueAxis.HasMajorGridLines = false;

//Showing minor gridlines.
chart.PrimaryValueAxis.HasMinorGridLines = true;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Hiding major gridlines.
chart.PrimaryValueAxis.HasMajorGridLines = False

'Showing minor gridlines.
chart.PrimaryValueAxis.HasMinorGridLines = True
{% endhighlight %}
{% endtabs %}

## Resize the Axis Title Area

The following code snippet illustrates how to resize the axis title area.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Manually resizing axis title area using Layout.
chart.PrimaryValueAxis.TitleArea.Layout.Left = 15;
chart.PrimaryValueAxis.TitleArea.Layout.Top = 20;
chart.PrimaryCategoryAxis.TitleArea.Layout.Left = 25;
chart.PrimaryCategoryAxis.TitleArea.Layout.Top = 20;

//Manually resizing axis title area using Manual Layout.
chart.PrimaryValueAxis.TitleArea.Layout.ManualLayout.Left = 0.04;
chart.PrimaryValueAxis.TitleArea.Layout.ManualLayout.Top = 0.34;
chart.PrimaryCategoryAxis.TitleArea.Layout.ManualLayout.Left = 0.38;
chart.PrimaryCategoryAxis.TitleArea.Layout.ManualLayout.Top = 0.95;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Manually resizing axis title area using Layout.
chart.PrimaryValueAxis.TitleArea.Layout.Left = 15;
chart.PrimaryValueAxis.TitleArea.Layout.Top = 20;
chart.PrimaryCategoryAxis.TitleArea.Layout.Left = 25;
chart.PrimaryCategoryAxis.TitleArea.Layout.Top = 20;

//Manually resizing axis title area using Manual Layout.
chart.PrimaryValueAxis.TitleArea.Layout.ManualLayout.Left = 0.04;
chart.PrimaryValueAxis.TitleArea.Layout.ManualLayout.Top = 0.34;
chart.PrimaryCategoryAxis.TitleArea.Layout.ManualLayout.Left = 0.38;
chart.PrimaryCategoryAxis.TitleArea.Layout.ManualLayout.Top = 0.95;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Manually resizing axis title area using Layout.
chart.PrimaryValueAxis.TitleArea.Layout.Left = 15
chart.PrimaryValueAxis.TitleArea.Layout.Top = 20
chart.PrimaryCategoryAxis.TitleArea.Layout.Left = 25
chart.PrimaryCategoryAxis.TitleArea.Layout.Top = 20

'Manually resizing axis title area using Manual Layout.
chart.PrimaryValueAxis.TitleArea.Layout.ManualLayout.Left = 0.04
chart.PrimaryValueAxis.TitleArea.Layout.ManualLayout.Top = 0.34
chart.PrimaryCategoryAxis.TitleArea.Layout.ManualLayout.Left = 0.38
chart.PrimaryCategoryAxis.TitleArea.Layout.ManualLayout.Top = 0.95
{% endhighlight %}
{% endtabs %}

## Set the Secondary Axis

The following code snippet illustrates how to use secondary axis in chart.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Use Secondary Axis.
chart.Series[1].UsePrimaryAxis = false;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Use Secondary Axis.
chart.Series[1].UsePrimaryAxis = false;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Use Secondary Axis for the second series.
chart.Series(1).UsePrimaryAxis = False
{% endhighlight %}
{% endtabs %}

## Secondary Value Properties

The following code snippet illustrates how to customize secondary value axis in chart.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//MaxCross in axis.
chart.SecondaryValueAxis.IsMaxCross = true;

//Axis title.
chart.SecondaryValueAxis.Title = "Temperature,deg.F";

//Axis title area text angle rotation.
chart.SecondaryValueAxis.TitleArea.TextRotationAngle = 90;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//MaxCross in axis.
chart.SecondaryValueAxis.IsMaxCross = true;

//Axis title.
chart.SecondaryValueAxis.Title = "Temperature,deg.F";

//Axis title area text angle rotation.
chart.SecondaryValueAxis.TitleArea.TextRotationAngle = 90;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Set MaxCross for the secondary value axis.
chart.SecondaryValueAxis.IsMaxCross = True

'Set the axis title for the secondary value axis.
chart.SecondaryValueAxis.Title = "Temperature,deg.F"

'Set the axis title area text rotation angle for the secondary value axis.
chart.SecondaryValueAxis.TitleArea.TextRotationAngle = 90
{% endhighlight %}
{% endtabs %}

## Secondary Category Properties

The following code snippet illustrates how to customize secondary category axis in chart.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//MaxCross in axis.
chart.SecondaryCategoryAxis.IsMaxCross = true;

//Select border line color.
chart.SecondaryCategoryAxis.Border.LineColor = Syncfusion.Drawing.Color.Transparent;

//Select major tick mark option.
chart.SecondaryCategoryAxis.MajorTickMark = ExcelTickMark.TickMark_Cross;

//Select tick label position.
chart.SecondaryCategoryAxis.TickLabelPosition = ExcelTickLabelPosition.TickLabelPosition_None;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//MaxCross in axis.
chart.SecondaryCategoryAxis.IsMaxCross = true;

//Select border line color.
chart.SecondaryCategoryAxis.Border.LineColor = Color.Transparent;

//Select major tick mark option.
chart.SecondaryCategoryAxis.MajorTickMark = ExcelTickMark.TickMark_Cross;

//Select tick label position.
chart.SecondaryCategoryAxis.TickLabelPosition = ExcelTickLabelPosition.TickLabelPosition_None;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Set MaxCross for the secondary category axis.
chart.SecondaryCategoryAxis.IsMaxCross = True

'Select the border line color and make it transparent.
chart.SecondaryCategoryAxis.Border.LineColor = Color.Transparent

'Select the major tick mark option as Cross.
chart.SecondaryCategoryAxis.MajorTickMark = ExcelTickMark.TickMark_Cross

'Select the tick label position as None.
chart.SecondaryCategoryAxis.TickLabelPosition = ExcelTickLabelPosition.TickLabelPosition_None
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
    IWorkbook workbook = application.Workbooks.Open(inputStream);
    IWorksheet sheet = workbook.Worksheets[0];
    IChartShape chart = sheet.Charts[0];

    //Set the horizontal (category) axis title.
    chart.PrimaryCategoryAxis.Title = "Months";
    //Set the Vertical (value) axis title.
    chart.PrimaryValueAxis.Title = "Precipitation,in.";
    //Set title for secondary value axis
    chart.SecondaryValueAxis.Title = "Temperature,deg.F";

    //Customize the horizontal category axis.
    chart.PrimaryCategoryAxis.Border.LinePattern = ExcelChartLinePattern.Solid;
    chart.PrimaryCategoryAxis.Border.LineColor = Syncfusion.Drawing.Color.Blue;
    chart.PrimaryCategoryAxis.Border.LineWeight = ExcelChartLineWeight.Hairline;

    //Customize the vertical category axis.
    chart.PrimaryValueAxis.Border.LinePattern = ExcelChartLinePattern.Solid;
    chart.PrimaryValueAxis.Border.LineColor = Syncfusion.Drawing.Color.Blue;
    chart.PrimaryValueAxis.Border.LineWeight = ExcelChartLineWeight.Narrow;

    //Customize the horizontal category axis font.
    chart.PrimaryCategoryAxis.Font.Color = ExcelKnownColors.Red;
    chart.PrimaryCategoryAxis.Font.FontName = "Calibri";
    chart.PrimaryCategoryAxis.Font.Bold = true;
    chart.PrimaryCategoryAxis.Font.Size = 8;

    //Customize the vertical category axis font.
    chart.PrimaryValueAxis.Font.Color = ExcelKnownColors.Red;
    chart.PrimaryValueAxis.Font.FontName = "Calibri";
    chart.PrimaryValueAxis.Font.Bold = true;
    chart.PrimaryValueAxis.Font.Size = 8;


    //Customize the secondary vertical category axis.
    chart.SecondaryValueAxis.Border.LinePattern = ExcelChartLinePattern.Solid;
    chart.SecondaryValueAxis.Border.LineColor = Syncfusion.Drawing.Color.Blue;
    chart.SecondaryValueAxis.Border.LineWeight = ExcelChartLineWeight.Narrow;

    //Customize the secondary vertical category axis font.
    chart.SecondaryValueAxis.Font.Color = ExcelKnownColors.Red;
    chart.SecondaryValueAxis.Font.FontName = "Calibri";
    chart.SecondaryValueAxis.Font.Bold = true;
    chart.SecondaryValueAxis.Font.Size = 8;

    //Axis title area text angle rotation.
    chart.PrimaryValueAxis.TitleArea.TextRotationAngle = 270;

    //Maximum value in the axis.
    chart.PrimaryValueAxis.MaximumValue = 15;
    chart.PrimaryValueAxis.MinimumValue = 0;
    //Number format for axis.
    chart.PrimaryValueAxis.NumberFormat = "0.0";

    //Hiding major gridlines.
    chart.PrimaryValueAxis.HasMajorGridLines = true;

    //Showing minor gridlines.
    chart.PrimaryValueAxis.HasMinorGridLines = false;

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
    IWorkbook workbook = application.Workbooks.Open(@"D:\Support Sample\Format Axis\Format Axis\Data\InputTemplate.xlsx");
    IWorksheet sheet = workbook.Worksheets[0];
    IChartShape chart = sheet.Charts[0];

    //Set the horizontal (category) axis title.
    chart.PrimaryCategoryAxis.Title = "Months";
    //Set the Vertical (value) axis title.
    chart.PrimaryValueAxis.Title = "Precipitation,in.";
    //Set title for secondary value axis
    chart.SecondaryValueAxis.Title = "Temperature,deg.F";

    //Customize the horizontal category axis.
    chart.PrimaryCategoryAxis.Border.LinePattern = ExcelChartLinePattern.Solid;
    chart.PrimaryCategoryAxis.Border.LineColor = Color.Blue;
    chart.PrimaryCategoryAxis.Border.LineWeight = ExcelChartLineWeight.Hairline;

    //Customize the vertical category axis.
    chart.PrimaryValueAxis.Border.LinePattern = ExcelChartLinePattern.Solid;
    chart.PrimaryValueAxis.Border.LineColor = Color.Blue;
    chart.PrimaryValueAxis.Border.LineWeight = ExcelChartLineWeight.Narrow;

    //Customize the horizontal category axis font.
    chart.PrimaryCategoryAxis.Font.Color = ExcelKnownColors.Red;
    chart.PrimaryCategoryAxis.Font.FontName = "Calibri";
    chart.PrimaryCategoryAxis.Font.Bold = true;
    chart.PrimaryCategoryAxis.Font.Size = 8;

    //Customize the vertical category axis font.
    chart.PrimaryValueAxis.Font.Color = ExcelKnownColors.Red;
    chart.PrimaryValueAxis.Font.FontName = "Calibri";
    chart.PrimaryValueAxis.Font.Bold = true;
    chart.PrimaryValueAxis.Font.Size = 8;


    //Customize the secondary vertical category axis.
    chart.SecondaryValueAxis.Border.LinePattern = ExcelChartLinePattern.Solid;
    chart.SecondaryValueAxis.Border.LineColor = Color.Blue;
    chart.SecondaryValueAxis.Border.LineWeight = ExcelChartLineWeight.Narrow;

    //Customize the secondary vertical category axis font.
    chart.SecondaryValueAxis.Font.Color = ExcelKnownColors.Red;
    chart.SecondaryValueAxis.Font.FontName = "Calibri";
    chart.SecondaryValueAxis.Font.Bold = true;
    chart.SecondaryValueAxis.Font.Size = 8;

    //Axis title area text angle rotation.
    chart.PrimaryValueAxis.TitleArea.TextRotationAngle = 270;

    //Maximum value in the axis.
    chart.PrimaryValueAxis.MaximumValue = 15;
    chart.PrimaryValueAxis.MinimumValue = 0;
    //Number format for axis.
    chart.PrimaryValueAxis.NumberFormat = "0.0";

    //Hiding major gridlines.
    chart.PrimaryValueAxis.HasMajorGridLines = true;

    //Showing minor gridlines.
    chart.PrimaryValueAxis.HasMinorGridLines = false;

    //Saving the workbook
    workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As New ExcelEngine()
    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Xlsx
    Dim workbook As IWorkbook = application.Workbooks.Open("D:\Support Sample\Format Axis\Format Axis\Data\InputTemplate.xlsx")
    Dim sheet As IWorksheet = workbook.Worksheets(0)
    Dim chart As IChartShape = sheet.Charts(0)

    'Set the horizontal (category) axis title.
    chart.PrimaryCategoryAxis.Title = "Months"
    'Set the Vertical (value) axis title.
    chart.PrimaryValueAxis.Title = "Precipitation,in."
    'Set title for secondary value axis
    chart.SecondaryValueAxis.Title = "Temperature,deg.F"

    'Customize the horizontal category axis.
    chart.PrimaryCategoryAxis.Border.LinePattern = ExcelChartLinePattern.Solid
    chart.PrimaryCategoryAxis.Border.LineColor = Color.Blue
    chart.PrimaryCategoryAxis.Border.LineWeight = ExcelChartLineWeight.Hairline

    'Customize the vertical category axis.
    chart.PrimaryValueAxis.Border.LinePattern = ExcelChartLinePattern.Solid
    chart.PrimaryValueAxis.Border.LineColor = Color.Blue
    chart.PrimaryValueAxis.Border.LineWeight = ExcelChartLineWeight.Narrow

    'Customize the horizontal category axis font.
    chart.PrimaryCategoryAxis.Font.Color = ExcelKnownColors.Red
    chart.PrimaryCategoryAxis.Font.FontName = "Calibri"
    chart.PrimaryCategoryAxis.Font.Bold = True
    chart.PrimaryCategoryAxis.Font.Size = 8

    'Customize the vertical category axis font.
    chart.PrimaryValueAxis.Font.Color = ExcelKnownColors.Red
    chart.PrimaryValueAxis.Font.FontName = "Calibri"
    chart.PrimaryValueAxis.Font.Bold = True
    chart.PrimaryValueAxis.Font.Size = 8

    'Customize the secondary vertical category axis.
    chart.SecondaryValueAxis.Border.LinePattern = ExcelChartLinePattern.Solid
    chart.SecondaryValueAxis.Border.LineColor = Color.Blue
    chart.SecondaryValueAxis.Border.LineWeight = ExcelChartLineWeight.Narrow

    'Customize the secondary vertical category axis font.
    chart.SecondaryValueAxis.Font.Color = ExcelKnownColors.Red
    chart.SecondaryValueAxis.Font.FontName = "Calibri"
    chart.SecondaryValueAxis.Font.Bold = True
    chart.SecondaryValueAxis.Font.Size = 8

    'Axis title area text angle rotation.
    chart.PrimaryValueAxis.TitleArea.TextRotationAngle = 270

    'Maximum value in the axis.
    chart.PrimaryValueAxis.MaximumValue = 15
    chart.PrimaryValueAxis.MinimumValue = 0
    'Number format for axis.
    chart.PrimaryValueAxis.NumberFormat = "0.0"

    'Hiding major gridlines.
    chart.PrimaryValueAxis.HasMajorGridLines = True

    'Showing minor gridlines.
    chart.PrimaryValueAxis.HasMinorGridLines = False

    'Saving the workbook
    workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}
{% endtabs %}

A complete working example to format the axis in C# is present on [this GitHub page]().

## See Also
* [How to set vertical axis crosses value for chart axis in C#, VB.NET?](https://support.syncfusion.com/kb/article/7608/how-to-set-vertical-axis-crosses-value-for-chart-axis-in-c-vb-net)
* [How to reverse Excel chart axis order in C#, VB.NET?](https://support.syncfusion.com/kb/article/7513/how-to-reverse-excel-chart-axis-order-in-c-vb-net)