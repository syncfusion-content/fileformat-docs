---
title: Modify the Appearance of Legend | Syncfusion
description: Learn how to modify the appearance of legend in a chart in an Excel document using Syncfusion .NET Excel (XlsIO) library without Microsoft Excel.
platform: file-formats
control: XlsIO
documentation: UG
---

# Chart Legend in Excel document

Legends are visual pictorial hints that provide a viewer information that helps them understand an chart. Using DocIO, you can **customize the legend in the chart**.

## Set the Position of Legend

The following code snippet illustrates how to set the legend position in chart.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Set the position of legend.
chart.Legend.Position = ExcelLegendPosition.Right;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Set the position of legend.
chart.Legend.Position = ExcelLegendPosition.Right;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Set the position of legend.
chart.Legend.Position = ExcelLegendPosition.Right
{% endhighlight %}
{% endtabs %}

## Set the layout Inclusion

The following code snippet illustrates how to prevent the overlapping the legend in chart.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Legend without overlapping the chart.
chart.Legend.IncludeInLayout = true;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Legend without overlapping the chart.
chart.Legend.IncludeInLayout = true;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Legend without overlapping the chart.
chart.Legend.IncludeInLayout = true
{% endhighlight %}
{% endtabs %}

## Customization of Border

The following code snippet illustrates how to modify the border of the legend in chart.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Sets the legend border format - color, pattern, weight.
chart.Legend.FrameFormat.Border.AutoFormat = false;
chart.Legend.FrameFormat.Border.IsAutoLineColor = false;
chart.Legend.FrameFormat.Border.LineColor = Syncfusion.Drawing.Color.Black;
chart.Legend.FrameFormat.Border.LinePattern = ExcelChartLinePattern.DashDot;
chart.Legend.FrameFormat.Border.LineWeight = ExcelChartLineWeight.Narrow;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Sets the legend border format - color, pattern, weight.
chart.Legend.FrameFormat.Border.AutoFormat = false;
chart.Legend.FrameFormat.Border.IsAutoLineColor = false;
chart.Legend.FrameFormat.Border.LineColor = Syncfusion.Drawing.Color.Black;
chart.Legend.FrameFormat.Border.LinePattern = ExcelChartLinePattern.DashDot;
chart.Legend.FrameFormat.Border.LineWeight = ExcelChartLineWeight.Narrow;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Sets the legend border format - color, pattern, weight.
chart.Legend.FrameFormat.Border.AutoFormat = false
chart.Legend.FrameFormat.Border.IsAutoLineColor = false
chart.Legend.FrameFormat.Border.LineColor = Syncfusion.Drawing.Color.Black
chart.Legend.FrameFormat.Border.LinePattern = ExcelChartLinePattern.DashDot
chart.Legend.FrameFormat.Border.LineWeight = ExcelChartLineWeight.Narrow
{% endhighlight %}
{% endtabs %}

## Customization of Text Area

The following code snippet illustrates how to modify the text area of the legend in chart.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Set the legend's text area format - font name, bold, color, size.
chart.Legend.TextArea.Bold = true;
chart.Legend.TextArea.Color = ExcelKnownColors.Pink;
chart.Legend.TextArea.FontName = "Times New Roman";
chart.Legend.TextArea.Size = 10;
chart.Legend.TextArea.Strikethrough = false;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Set the legend's text area format - font name, bold, color, size.
chart.Legend.TextArea.Bold = true;
chart.Legend.TextArea.Color = ExcelKnownColors.Pink;
chart.Legend.TextArea.FontName = "Times New Roman";
chart.Legend.TextArea.Size = 10;
chart.Legend.TextArea.Strikethrough = false;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Set the legend's text area format - font name, bold, color, size.
chart.Legend.TextArea.Bold = true
chart.Legend.TextArea.Color = ExcelKnownColors.Pink
chart.Legend.TextArea.FontName = "Times New Roman"
chart.Legend.TextArea.Size = 10
chart.Legend.TextArea.Strikethrough = false
{% endhighlight %}
{% endtabs %}

## Modify the Legend Entry

The following code snippet illustrates how to modify the legend entry.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Modify the legend entry.
chart.Legend.LegendEntries[0].IsDeleted = true;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Modify the legend entry.
chart.Legend.LegendEntries[0].IsDeleted = true;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Modify the legend entry.
chart.Legend.LegendEntries(0).IsDeleted = True
{% endhighlight %}
{% endtabs %}

## Manage Legend Visibility

The following code snippet illustrates how to hide the legend in chart.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Hiding the legend.
chart.HasLegend = false;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Hiding the legend.
chart.HasLegend = false;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
' Hiding the legend.
chart.HasLegend = False
{% endhighlight %}
{% endtabs %}

## View the Legend Horizontally

The following code snippet illustrates how to view legend horizontally.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//View legend horizontally.
chart.Legend.IsVerticalLegend = false;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//View legend horizontally.
chart.Legend.IsVerticalLegend = false;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
' View legend horizontally.
chart.Legend.IsVerticalLegend = False
{% endhighlight %}
{% endtabs %}

## Set the Position using Layout

The following code snippet illustrates how to position the legend using layout.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Manually positioning chart legend area using Layout.
chart.Legend.Layout.LeftMode = LayoutModes.edge;
chart.Legend.Layout.TopMode = LayoutModes.edge;

//Manually positioning chart legend area using Manual Layout.
chart.Legend.Layout.ManualLayout.LeftMode = LayoutModes.edge;
chart.Legend.Layout.ManualLayout.TopMode = LayoutModes.edge;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Manually positioning chart legend area using Layout.
chart.Legend.Layout.LeftMode = LayoutModes.edge;
chart.Legend.Layout.TopMode = LayoutModes.edge;

//Manually positioning chart legend area using Manual Layout.
chart.Legend.Layout.ManualLayout.LeftMode = LayoutModes.edge;
chart.Legend.Layout.ManualLayout.TopMode = LayoutModes.edge;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Manually positioning chart legend area using Layout.
chart.Legend.Layout.LeftMode = LayoutModes.Edge
chart.Legend.Layout.TopMode = LayoutModes.Edge

'Manually positioning chart legend area using Manual Layout.
chart.Legend.Layout.ManualLayout.LeftMode = LayoutModes.Edge
chart.Legend.Layout.ManualLayout.TopMode = LayoutModes.Edge
{% endhighlight %}
{% endtabs %}

## Resize the Legend

The following code snippet illustrates how to resize the legend in chart.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Manually resizing chart legend area using Layout.
chart.Legend.Layout.Left = 400;
chart.Legend.Layout.Top = 150;
chart.Legend.Layout.Width = 150;
chart.Legend.Layout.Height = 100;

//Manually resizing chart legend area using Manual Layout.
chart.Legend.Layout.ManualLayout.Height = 0.09;
chart.Legend.Layout.ManualLayout.Width = 0.30;
chart.Legend.Layout.ManualLayout.Top = 0.36;
chart.Legend.Layout.ManualLayout.Left = 0.68;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Manually resizing chart legend area using Layout.
chart.Legend.Layout.Left = 400;
chart.Legend.Layout.Top = 150;
chart.Legend.Layout.Width = 150;
chart.Legend.Layout.Height = 100;

//Manually resizing chart legend area using Manual Layout.
chart.Legend.Layout.ManualLayout.Height = 0.09;
chart.Legend.Layout.ManualLayout.Width = 0.30;
chart.Legend.Layout.ManualLayout.Top = 0.36;
chart.Legend.Layout.ManualLayout.Left = 0.68;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Manually resizing chart legend area using Layout.
chart.Legend.Layout.Left = 400
chart.Legend.Layout.Top = 150
chart.Legend.Layout.Width = 150
chart.Legend.Layout.Height = 100

' Manually resizing chart legend area using Manual Layout.
chart.Legend.Layout.ManualLayout.Height = 0.09
chart.Legend.Layout.ManualLayout.Width = 0.30
chart.Legend.Layout.ManualLayout.Top = 0.36
chart.Legend.Layout.ManualLayout.Left = 0.68
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

    //Enable the legend.
    chart.HasLegend = true;

    //Set the position of legend.
    chart.Legend.Position = ExcelLegendPosition.Right;

    //Sets the legend border format - color, pattern, weight.
    chart.Legend.FrameFormat.Border.AutoFormat = false;
    chart.Legend.FrameFormat.Border.IsAutoLineColor = false;
    chart.Legend.FrameFormat.Border.LineColor = Syncfusion.Drawing.Color.Black;
    chart.Legend.FrameFormat.Border.LinePattern = ExcelChartLinePattern.DashDot;
    chart.Legend.FrameFormat.Border.LineWeight = ExcelChartLineWeight.Narrow;

    //Set the legend's text area format - font name, bold, color, size.
    chart.Legend.TextArea.Bold = true;
    chart.Legend.TextArea.Color = ExcelKnownColors.Pink;
    chart.Legend.TextArea.FontName = "Times New Roman";
    chart.Legend.TextArea.Size = 10;
    chart.Legend.TextArea.Strikethrough = false;

    //View legend in vertical.
    chart.Legend.IsVerticalLegend = true;

    //Modifies the legend entry.
    chart.Legend.LegendEntries[0].IsDeleted = true;

    //Manually resizing chart legend area using Layout.
    chart.Legend.Layout.Left = 0.2;
    chart.Legend.Layout.Top = 5;
    chart.Legend.Layout.Width = 60;
    chart.Legend.Layout.Height = 40;

    //Legend without overlapping the chart.
    chart.Legend.IncludeInLayout = true;

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

    //Enable the legend.
    chart.HasLegend = true;

    //Set the position of legend.
    chart.Legend.Position = ExcelLegendPosition.Right;

    //Sets the legend border format - color, pattern, weight.
    chart.Legend.FrameFormat.Border.AutoFormat = false;
    chart.Legend.FrameFormat.Border.IsAutoLineColor = false;
    chart.Legend.FrameFormat.Border.LineColor = Color.Black;
    chart.Legend.FrameFormat.Border.LinePattern = ExcelChartLinePattern.DashDot;
    chart.Legend.FrameFormat.Border.LineWeight = ExcelChartLineWeight.Narrow;

    //Set the legend's text area format - font name, bold, color, size.
    chart.Legend.TextArea.Bold = true;
    chart.Legend.TextArea.Color = ExcelKnownColors.Pink;
    chart.Legend.TextArea.FontName = "Times New Roman";
    chart.Legend.TextArea.Size = 10;
    chart.Legend.TextArea.Strikethrough = false;

    //View legend in vertical.
    chart.Legend.IsVerticalLegend = true;

    //Modifies the legend entry.
    chart.Legend.LegendEntries[0].IsDeleted = true;

    //Manually resizing chart legend area using Layout.
    chart.Legend.Layout.Left = 0.2;
    chart.Legend.Layout.Top = 5;
    chart.Legend.Layout.Width = 60;
    chart.Legend.Layout.Height = 40;

    //Legend without overlapping the chart.
    chart.Legend.IncludeInLayout = true;

    //Saving the workbook
    workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As New ExcelEngine()
    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Xlsx
    Dim workbook As IWorkbook = application.Workbooks.Open("InputTemplate.xlsx")
    Dim sheet As IWorksheet = workbook.Worksheets(0)
    Dim chart As IChartShape = sheet.Charts(0)

    'Enable the legend.
    chart.HasLegend = True

    'Set the position of legend.
    chart.Legend.Position = ExcelLegendPosition.Right

    'Sets the legend border format - color, pattern, weight.
    chart.Legend.FrameFormat.Border.AutoFormat = False
    chart.Legend.FrameFormat.Border.IsAutoLineColor = False
    chart.Legend.FrameFormat.Border.LineColor = Color.Black
    chart.Legend.FrameFormat.Border.LinePattern = ExcelChartLinePattern.DashDot
    chart.Legend.FrameFormat.Border.LineWeight = ExcelChartLineWeight.Narrow

    'Set the legend's text area format - font name, bold, color, size.
    chart.Legend.TextArea.Bold = True
    chart.Legend.TextArea.Color = ExcelKnownColors.Pink
    chart.Legend.TextArea.FontName = "Times New Roman"
    chart.Legend.TextArea.Size = 10
    chart.Legend.TextArea.Strikethrough = False

    'View legend in vertical.
    chart.Legend.IsVerticalLegend = True

    'Modifies the legend entry.
    chart.Legend.LegendEntries(0).IsDeleted = True

    'Manually resizing chart legend area using Layout.
    chart.Legend.Layout.Left = 0.2
    chart.Legend.Layout.Top = 5
    chart.Legend.Layout.Width = 60
    chart.Legend.Layout.Height = 40

    'Legend without overlapping the chart.
    chart.Legend.IncludeInLayout = True

    'Saving the workbook
    workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}
{% endtabs %}

A complete working example to format the legend in C# is present on [this GitHub page]().

## See Also
* [How to delete Excel chart legend in C#, VB.NET?](https://support.syncfusion.com/kb/article/7525/how-to-delete-excel-chart-legend-in-c-vb-net)
* [Show or hide Excel chart legend in C#, VB.NET](https://support.syncfusion.com/kb/article/2564/show-or-hide-excel-chart-legend-in-c-vb-net)