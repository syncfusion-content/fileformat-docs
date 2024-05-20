---
title: Modify the Appearance of Chart Title | Syncfusion
description: Learn how to modify the appearance of chart title in a chart in an Excel document using Syncfusion .NET Excel (XlsIO) library without Microsoft Excel.
platform: file-formats
control: XlsIO
documentation: UG
---

# Chart Title

Chart title is a brief description at the top of a chart, offering context and clarity for the data displayed. Using XlsIO, you can **customize the chart title in the chart**.

## Set the Chart Title Name

The following code snippet illustrates how to set the chart title name.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//Set chart name and title
chart.Name = "Purchase Details";
chart.ChartTitle = "Purchase Details";

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

//Set chart name and title
chart.Name = "Purchase Details";
chart.ChartTitle = "Purchase Details";

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Set chart name and title
chart.Name = "Purchase Details"
chart.ChartTitle = "Purchase Details"

{% endhighlight %}
{% endtabs %}

## Customize the Chart Title Area

The following code snippet illustrates how to customize the chart title area.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//Customize chart title area
chart.ChartTitleArea.FontName = "Calibri";
chart.ChartTitleArea.Bold = true;
chart.ChartTitleArea.Color = ExcelKnownColors.Black;
chart.ChartTitleArea.Underline = ExcelUnderline.Single;
chart.ChartTitleArea.Size = 15;

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

//Customize chart title area
chart.ChartTitleArea.FontName = "Calibri";
chart.ChartTitleArea.Bold = true;
chart.ChartTitleArea.Color = ExcelKnownColors.Black;
chart.ChartTitleArea.Underline = ExcelUnderline.Single;
chart.ChartTitleArea.Size = 15;

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Customize chart title area
chart.ChartTitleArea.FontName = "Calibri"
chart.ChartTitleArea.Bold = True
chart.ChartTitleArea.Color = ExcelKnownColors.Black
chart.ChartTitleArea.Underline = ExcelUnderline.Single
chart.ChartTitleArea.Size = 15

{% endhighlight %}
{% endtabs %}

## Resize the Chart Title Area

The following code snippet illustrates how to resize the chart title area.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//Manually resizing chart title area using Layout.
chart.ChartTitleArea.Layout.Top = 10;
chart.ChartTitleArea.Layout.Left = 10;

//Manually resizing chart title area using Manual Layout.
chart.ChartTitleArea.Layout.ManualLayout.Top = 0.05;
chart.ChartTitleArea.Layout.ManualLayout.Left = 0.30;

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

//Manually resizing chart title area using Layout.
chart.ChartTitleArea.Layout.Top = 10;
chart.ChartTitleArea.Layout.Left = 10;

//Manually resizing chart title area using Manual Layout.
chart.ChartTitleArea.Layout.ManualLayout.Top = 0.05;
chart.ChartTitleArea.Layout.ManualLayout.Left = 0.30;

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Manually resizing chart title area using Layout.
chart.ChartTitleArea.Layout.Top = 10
chart.ChartTitleArea.Layout.Left = 10

'Manually resizing chart title area using Manual Layout.
chart.ChartTitleArea.Layout.ManualLayout.Top = 0.05
chart.ChartTitleArea.Layout.ManualLayout.Left = 0.30

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

    //Set chart name and title
    chart.Name = "Purchase Details";
    chart.ChartTitle = "Purchase Details";

    //Customize chart title area
    chart.ChartTitleArea.FontName = "Calibri";
    chart.ChartTitleArea.Bold = true;
    chart.ChartTitleArea.Color = ExcelKnownColors.Black;
    chart.ChartTitleArea.Underline = ExcelUnderline.Single;
    chart.ChartTitleArea.Size = 15;

    //Manually resizing chart title area using Layout.
    chart.ChartTitleArea.Layout.Left = 50;

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

    //Set chart name and title
    chart.Name = "Purchase Details";
    chart.ChartTitle = "Purchase Details";

    //Customize chart title area
    chart.ChartTitleArea.FontName = "Calibri";
    chart.ChartTitleArea.Bold = true;
    chart.ChartTitleArea.Color = ExcelKnownColors.Black;
    chart.ChartTitleArea.Underline = ExcelUnderline.Single;
    chart.ChartTitleArea.Size = 15;

    //Manually resizing chart title area using Layout.
    chart.ChartTitleArea.Layout.Left = 50;

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

    'Set chart name and title
    chart.Name = "Purchase Details"
    chart.ChartTitle = "Purchase Details"

    'Customize chart title area
    chart.ChartTitleArea.FontName = "Calibri"
    chart.ChartTitleArea.Bold = True
    chart.ChartTitleArea.Color = ExcelKnownColors.Black
    chart.ChartTitleArea.Underline = ExcelUnderline.Single
    chart.ChartTitleArea.Size = 15

    'Manually resizing chart title area using Layout.
    chart.ChartTitleArea.Layout.Left = 50

    'Saving the workbook as stream
    workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}
{% endtabs %}

A complete working example to format a chart title in C# is present on [this GitHub page]().

## Remove Chart Title

The following code snippet illustrates how to remove the chart title area.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//Remove the chart title 
chart.ChartTitleArea.Text = String.Empty;

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

//Remove the chart title 
chart.ChartTitleArea.Text = String.Empty;

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Remove the chart title 
chart.ChartTitleArea.Text = String.Empty

{% endhighlight %}
{% endtabs %}

## See Also

* [How to add chart title with formula in C#, VB.NET?](https://support.syncfusion.com/kb/article/10217/add-excel-chart-title-with-formula-in-c-vb-net-using-xlsio)