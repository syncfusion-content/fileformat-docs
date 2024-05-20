---
title: Modify the Appearance of Data Labels | Syncfusion
description: Learn how to modify the appearance of data labels in a chart in an Excel document using Syncfusion .NET Excel (XlsIO) library without Microsoft Excel.
platform: file-formats
control: XlsIO
documentation: UG
---

# Chart Data Labels

Data Labels on a chart make it easier to understand. They show important information about the lines or points on the chart. Using DocIO, you can **customize the data labels in the chart**.

## Enable Data Labels in Chart

The following code snippet illustrates how to add the data label in chart.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Enable the datalabel in chart.
chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.IsValue = true;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Enable the datalabel in chart.
chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.IsValue = true;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
' Enable the datalabel in chart.
chart.Series(0).DataPoints.DefaultDataPoint.DataLabels.IsValue = True
{% endhighlight %}
{% endtabs %}

## Customize the Data Labels

The following code snippet illustrates how to customize the data label in chart.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Set the data labels formatting - size, color, font name, position.
chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.Size = 10;
chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.Color = ExcelKnownColors.Black;
chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.FontName = "calibri";
chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.Bold = true;
chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.Position = ExcelDataLabelPosition.Outside;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Set the data labels formatting - size, color, font name, position.
chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.Size = 10;
chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.Color = ExcelKnownColors.Black;
chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.FontName = "calibri";
chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.Bold = true;
chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.Position = ExcelDataLabelPosition.Outside;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Set the data labels formatting - size, color, font name, position.
chart.Series(0).DataPoints.DefaultDataPoint.DataLabels.Size = 10;
chart.Series(0).DataPoints.DefaultDataPoint.DataLabels.Color = ExcelKnownColors.Black;
chart.Series(0).DataPoints.DefaultDataPoint.DataLabels.FontName = "calibri";
chart.Series(0).DataPoints.DefaultDataPoint.DataLabels.Bold = true;
chart.Series(0).DataPoints.DefaultDataPoint.DataLabels.Position = ExcelDataLabelPosition.Outside;
{% endhighlight %}
{% endtabs %}

## Set the Position of Data Labels

The following code snippet illustrates how to set the position of the data label in chart.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Set the position of data labels for the first series.
chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.Position = ExcelDataLabelPosition.Outside;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Set the position of data labels for the first series.
chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.Position = ExcelDataLabelPosition.Outside;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Set the position of data labels for the first series.
chart.Series(0).DataPoints.DefaultDataPoint.DataLabels.Position = ExcelDataLabelPosition.Outside
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

    for (int i = 0; i < chart.Series.Count; i++)
    {
        //Enable the datalabel in chart.
        chart.Series[i].DataPoints.DefaultDataPoint.DataLabels.IsValue = true;

        //Set the data labels formatting - size, color, font name, position.
        chart.Series[i].DataPoints.DefaultDataPoint.DataLabels.Size = 10;
        chart.Series[i].DataPoints.DefaultDataPoint.DataLabels.Color = ExcelKnownColors.Black;
        chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.FontName = "calibri";
        chart.Series[i].DataPoints.DefaultDataPoint.DataLabels.Bold = true;
        chart.Series[i].DataPoints.DefaultDataPoint.DataLabels.Position = ExcelDataLabelPosition.Outside;
    }

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
    IWorkbook workbook = application.Workbooks.Open(@"D:\Support Sample\Format-Data-Labels\Format-Data-Labels\Data\InputTemplate.xlsx");
    IWorksheet sheet = workbook.Worksheets[0];
    IChartShape chart = sheet.Charts[0];

    for (int i = 0; i < chart.Series.Count; i++)
    {
        //Enable the datalabel in chart.
        chart.Series[i].DataPoints.DefaultDataPoint.DataLabels.IsValue = true;

        //Set the data labels formatting - size, color, font name, position.
        chart.Series[i].DataPoints.DefaultDataPoint.DataLabels.Size = 10;
        chart.Series[i].DataPoints.DefaultDataPoint.DataLabels.Color = ExcelKnownColors.Black;
        chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.FontName = "calibri";
        chart.Series[i].DataPoints.DefaultDataPoint.DataLabels.Bold = true;
        chart.Series[i].DataPoints.DefaultDataPoint.DataLabels.Position = ExcelDataLabelPosition.Outside;
    }

    //Saving the workbook
    workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As New ExcelEngine()
    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Xlsx
    Dim workbook As IWorkbook = application.Workbooks.Open("D:\Support Sample\Format-Data-Labels\Format-Data-Labels\Data\InputTemplate.xlsx")
    Dim sheet As IWorksheet = workbook.Worksheets(0)
    Dim chart As IChartShape = sheet.Charts(0)

    For i As Integer = 0 To chart.Series.Count - 1
        'Enable the datalabel in chart.
        chart.Series(i).DataPoints.DefaultDataPoint.DataLabels.IsValue = True

        'Set the data labels formatting - size, color, font name, position.
        chart.Series(i).DataPoints.DefaultDataPoint.DataLabels.Size = 10
        chart.Series(i).DataPoints.DefaultDataPoint.DataLabels.Color = ExcelKnownColors.Black
        chart.Series(i).DataPoints.DefaultDataPoint.DataLabels.FontName = "calibri"
        chart.Series(i).DataPoints.DefaultDataPoint.DataLabels.Bold = True
        chart.Series(i).DataPoints.DefaultDataPoint.DataLabels.Position = ExcelDataLabelPosition.Outside
    Next

    'Saving the workbook
    workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}
{% endtabs %}

A complete working example to format the data labels in C# is present on [this GitHub page]().

## Resize the Data Labels

The following code snippet illustrates how to resize the data label in chart.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Manually resizing data label area using Layout.
chart.Series[0].DataPoints[0].DataLabels.Layout.Left = 3;
chart.Series[0].DataPoints[0].DataLabels.Layout.Top = 3;

//Manually resizing data label area using Manual Layout.
chart.Series[0].DataPoints[0].DataLabels.Layout.ManualLayout.Left = 3;
chart.Series[0].DataPoints[0].DataLabels.Layout.ManualLayout.Top = 3;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Manually resizing data label area using Layout.
chart.Series[0].DataPoints[0].DataLabels.Layout.Left = 3;
chart.Series[0].DataPoints[0].DataLabels.Layout.Top = 3;

//Manually resizing data label area using Manual Layout.
chart.Series[0].DataPoints[0].DataLabels.Layout.ManualLayout.Left = 3;
chart.Series[0].DataPoints[0].DataLabels.Layout.ManualLayout.Top = 3;
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
' Manually resizing data label area using Layout.
chart.Series(0).DataPoints(0).DataLabels.Layout.Left = 3
chart.Series(0).DataPoints(0).DataLabels.Layout.Top = 3

' Manually resizing data label area using Manual Layout.
chart.Series(0).DataPoints(0).DataLabels.Layout.ManualLayout.Left = 3
chart.Series(0).DataPoints(0).DataLabels.Layout.ManualLayout.Top = 3
{% endhighlight %}
{% endtabs %}