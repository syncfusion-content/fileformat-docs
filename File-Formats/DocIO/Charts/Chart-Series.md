---
title: Modify the Appearance of Series | Syncfusion
description: Learn how to modify the appearance of series in a chart in a Word document using Syncfusion .NET Word (DocIO) library without Microsoft Word.
platform: file-formats
control: DocIO
documentation: UG
---

# Chart Series

In a chart, a **series** represents a set of related data points, often depicted using lines, bars, or markers to show data trends or comparisons. Using DocIO, you can **customize the series in the chart**.

## Set the Series Name

The following code snippet illustrates how to set the series name in chart.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//Set name to chart series.
chart.Series[0].Name = "Sum of Purchases";

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

//Set name to chart series.
chart.Series[0].Name = "Sum of Purchases";

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Set name to chart series.
chart.Series(0).Name = "Sum of Purchases"

{% endhighlight %}
{% endtabs %}

## Set the Series Type

The following code snippet illustrates how to set the series type.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//Set the series type.
chart.Series[0].SerieType = OfficeChartType.Line_Markers;

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

//Set the series type.
chart.Series[0].SerieType = OfficeChartType.Line_Markers;

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Set the series type.
chart.Series(0).SerieType = OfficeChartType.Line_Markers

{% endhighlight %}
{% endtabs %}

## Customize the Series Color

The following code snippet illustrates how to customize the series color.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

// Configure the fill settings for the first series in the chart.
chart.Series[0].SerieFormat.Fill.FillType = OfficeFillType.Gradient;
chart.Series[0].SerieFormat.Fill.GradientColorType = OfficeGradientColor.TwoColor;
chart.Series[0].SerieFormat.Fill.BackColor = Syncfusion.Drawing.Color.FromArgb(205, 217, 234);
chart.Series[0].SerieFormat.Fill.ForeColor = Syncfusion.Drawing.Color.Red;

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

// Configure the fill settings for the first series in the chart.
chart.Series[0].SerieFormat.Fill.FillType = OfficeFillType.Gradient;
chart.Series[0].SerieFormat.Fill.GradientColorType = OfficeGradientColor.TwoColor;
chart.Series[0].SerieFormat.Fill.BackColor = Color.FromArgb(205, 217, 234);
chart.Series[0].SerieFormat.Fill.ForeColor = Color.Red;

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Configure the fill settings for the first series in the chart.
chart.Series(0).SerieFormat.Fill.FillType = OfficeFillType.Gradient
chart.Series(0).SerieFormat.Fill.GradientColorType = OfficeGradientColor.TwoColor
chart.Series(0).SerieFormat.Fill.BackColor = Color.FromArgb(205, 217, 234)
chart.Series(0).SerieFormat.Fill.ForeColor = Color.Red

{% endhighlight %}
{% endtabs %}

## Customize the Series Border

The following code snippet illustrates how to customize the series border.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//Customize series border.
chart.Series[0].SerieFormat.LineProperties.LineColor = Syncfusion.Drawing.Color.Red;
chart.Series[0].SerieFormat.LineProperties.LinePattern = OfficeChartLinePattern.Dot;
chart.Series[0].SerieFormat.LineProperties.LineWeight = OfficeChartLineWeight.Hairline;

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

//Customize series border.
chart.Series[0].SerieFormat.LineProperties.LineColor = Color.Red;
chart.Series[0].SerieFormat.LineProperties.LinePattern = OfficeChartLinePattern.Dot;
chart.Series[0].SerieFormat.LineProperties.LineWeight = OfficeChartLineWeight.Hairline;

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Customize series border.
chart.Series(0).SerieFormat.LineProperties.LineColor = Color.Red
chart.Series(0).SerieFormat.LineProperties.LinePattern = OfficeChartLinePattern.Dot
chart.Series(0).SerieFormat.LineProperties.LineWeight = OfficeChartLineWeight.Hairline

{% endhighlight %}
{% endtabs %}

The complete code snippet illustrating the above options is shown below.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//Creates a new instance of WordDocument (Empty Word Document).
 using (WordDocument document = new WordDocument())
 {
     //Adds section to the document.
     IWSection sec = document.AddSection();
     //Adds paragraph to the section.
     IWParagraph paragraph = sec.AddParagraph();
     //Inputs data for chart.
     object[][] data = new object[6][];
     for (int i = 0; i < 6; i++)
         data[i] = new object[3];
     data[0][0] = "";
     data[1][0] = "Camembert Pierrot";
     data[2][0] = "Alice Mutton";
     data[3][0] = "Roasted Tigers";
     data[4][0] = "Orange Shake";
     data[5][0] = "Dried Apples";
     data[0][1] = "Sum of Purchases";
     data[1][1] = 286;
     data[2][1] = 680;
     data[3][1] = 288;
     data[4][1] = 200;
     data[5][1] = 731;
     data[0][2] = "Sum of Future Expenses";
     data[1][2] = 1300;
     data[2][2] = 700;
     data[3][2] = 1280;
     data[4][2] = 1200;
     data[5][2] = 2660;

     //Creates and Appends chart to the paragraph.
     WChart chart = paragraph.AppendChart(data, 470, 300);

     //Sets chart type and title.
     chart.ChartTitle = "Purchase Details";
     chart.ChartTitleArea.FontName = "Calibri";
     chart.ChartTitleArea.Size = 14;
     chart.ChartArea.Border.LinePattern = OfficeChartLinePattern.Solid;

     //Sets series type.
     chart.Series[0].SerieType = OfficeChartType.Line_Markers;
     chart.Series[1].SerieType = OfficeChartType.Bar_Clustered;

     chart.PrimaryCategoryAxis.Title = "Products";
     chart.PrimaryValueAxis.Title = "In Dollars";

     // Configure the fill settings for the first series in the chart.
     chart.Series[1].SerieFormat.Fill.FillType = OfficeFillType.Gradient;
     chart.Series[1].SerieFormat.Fill.GradientColorType = OfficeGradientColor.TwoColor;
     chart.Series[1].SerieFormat.Fill.BackColor = Syncfusion.Drawing.Color.FromArgb(205, 217, 234);
     chart.Series[1].SerieFormat.Fill.ForeColor = Syncfusion.Drawing.Color.Red;
     //Customize series border.
     chart.Series[1].SerieFormat.LineProperties.LineColor = Syncfusion.Drawing.Color.Red;
     chart.Series[1].SerieFormat.LineProperties.LinePattern = OfficeChartLinePattern.Dot;
     chart.Series[1].SerieFormat.LineProperties.LineWeight = OfficeChartLineWeight.Hairline;

     //Sets position of legend.
     chart.Legend.Position = OfficeLegendPosition.Bottom;

     //Creates file stream.
     using (FileStream outputFileStream = new FileStream(Path.GetFullPath(@"../../../Sample.docx"), FileMode.Create, FileAccess.ReadWrite))
     {
         //Saves the Word document to file stream.
         document.Save(outputFileStream, FormatType.Docx);
     }
 }

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

//Creates a new instance of WordDocument (Empty Word Document).
using (WordDocument document = new WordDocument())
{
    //Adds section to the document.
    IWSection sec = document.AddSection();
    //Adds paragraph to the section.
    IWParagraph paragraph = sec.AddParagraph();
    //Inputs data for chart.
    object[][] data = new object[6][];
    for (int i = 0; i < 6; i++)
        data[i] = new object[3];
    data[0][0] = "";
    data[1][0] = "Camembert Pierrot";
    data[2][0] = "Alice Mutton";
    data[3][0] = "Roasted Tigers";
    data[4][0] = "Orange Shake";
    data[5][0] = "Dried Apples";
    data[0][1] = "Sum of Purchases";
    data[1][1] = 286;
    data[2][1] = 680;
    data[3][1] = 288;
    data[4][1] = 200;
    data[5][1] = 731;
    data[0][2] = "Sum of Future Expenses";
    data[1][2] = 1300;
    data[2][2] = 700;
    data[3][2] = 1280;
    data[4][2] = 1200;
    data[5][2] = 2660;

    //Creates and Appends chart to the paragraph.
    WChart chart = paragraph.AppendChart(data, 470, 300);

    //Sets chart type and title.
    chart.ChartTitle = "Purchase Details";
    chart.ChartTitleArea.FontName = "Calibri";
    chart.ChartTitleArea.Size = 14;
    chart.ChartArea.Border.LinePattern = OfficeChartLinePattern.Solid;

    //Sets series type.
    chart.Series[0].SerieType = OfficeChartType.Line_Markers;
    chart.Series[1].SerieType = OfficeChartType.Bar_Clustered;

    chart.PrimaryCategoryAxis.Title = "Products";
    chart.PrimaryValueAxis.Title = "In Dollars";

    // Configure the fill settings for the first series in the chart.
    chart.Series[1].SerieFormat.Fill.FillType = OfficeFillType.Gradient;
    chart.Series[1].SerieFormat.Fill.GradientColorType = OfficeGradientColor.TwoColor;
    chart.Series[1].SerieFormat.Fill.BackColor = Color.FromArgb(205, 217, 234);
    chart.Series[1].SerieFormat.Fill.ForeColor = Color.Red;
    //Customize series border.
    chart.Series[1].SerieFormat.LineProperties.LineColor = Color.Red;
    chart.Series[1].SerieFormat.LineProperties.LinePattern = OfficeChartLinePattern.Dot;
    chart.Series[1].SerieFormat.LineProperties.LineWeight = OfficeChartLineWeight.Hairline;

    //Sets position of legend.
    chart.Legend.Position = OfficeLegendPosition.Bottom;
    //Saves the Word document to file stream.
    document.Save("Sample.docx");             
}

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

Using document As New WordDocument()
    ' Adds a section to the document.
    Dim sec As IWSection = document.AddSection()
    
    ' Adds a paragraph to the section.
    Dim paragraph As IWParagraph = sec.AddParagraph()

    ' Inputs data for the chart.
    Dim data As Object(,) = New Object(5, 2) {}
    data(0, 0) = ""
    data(1, 0) = "Camembert Pierrot"
    data(2, 0) = "Alice Mutton"
    data(3, 0) = "Roasted Tigers"
    data(4, 0) = "Orange Shake"
    data(5, 0) = "Dried Apples"
    data(0, 1) = "Sum of Purchases"
    data(1, 1) = 286
    data(2, 1) = 680
    data(3, 1) = 288
    data(4, 1) = 200
    data(5, 1) = 731
    data(0, 2) = "Sum of Future Expenses"
    data(1, 2) = 1300
    data(2, 2) = 700
    data(3, 2) = 1280
    data(4, 2) = 1200
    data(5, 2) = 2660

    ' Creates and appends a chart to the paragraph.
    Dim chart As WChart = paragraph.AppendChart(data, 470, 300)

    ' Sets chart type and title.
    chart.ChartTitle = "Purchase Details"
    chart.ChartTitleArea.FontName = "Calibri"
    chart.ChartTitleArea.Size = 14
    chart.ChartArea.Border.LinePattern = OfficeChartLinePattern.Solid

    ' Sets series type.
    chart.Series(0).SerieType = OfficeChartType.Line_Markers
    chart.Series(1).SerieType = OfficeChartType.Bar_Clustered

    chart.PrimaryCategoryAxis.Title = "Products"
    chart.PrimaryValueAxis.Title = "In Dollars"

    ' Configure the fill settings for the first series in the chart.
    chart.Series(1).SerieFormat.Fill.FillType = OfficeFillType.Gradient
    chart.Series(1).SerieFormat.Fill.GradientColorType = OfficeGradientColor.TwoColor
    chart.Series(1).SerieFormat.Fill.BackColor = Color.FromArgb(205, 217, 234)
    chart.Series(1).SerieFormat.Fill.ForeColor = Color.Red

    ' Customize series border.
    chart.Series(1).SerieFormat.LineProperties.LineColor = Color.Red
    chart.Series(1).SerieFormat.LineProperties.LinePattern = OfficeChartLinePattern.Dot
    chart.Series(1).SerieFormat.LineProperties.LineWeight = OfficeChartLineWeight.Hairline

    ' Sets the position of the legend.
    chart.Legend.Position = OfficeLegendPosition.Bottom

    ' Saves the Word document to a file.
    document.Save("Sample.docx")
End Using

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Charts/Fomat-Series/Format-Series/.NET).

## Set the DataPoint as Total

The following code snippet illustrates how to set the Data Point as total in chart.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//Data point settings as total in chart.
chart.Series[0].DataPoints[3].SetAsTotal = true;

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

//Data point settings as total in chart.
chart.Series[0].DataPoints[3].SetAsTotal = true;

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Data point settings as total in chart.
chart.Series(0).DataPoints(3).SetAsTotal = True

{% endhighlight %}
{% endtabs %}

## Set the connector lines between data points 

The following code snippet illustrates how to set the connector lines between data points. 

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//Showing the connector lines between data points.
chart.Series[0].SerieFormat.ShowConnectorLines = true;

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

//Showing the connector lines between data points.
chart.Series[0].SerieFormat.ShowConnectorLines = true;

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Showing the connector lines between data points.
chart.Series(0).SerieFormat.ShowConnectorLines = True

{% endhighlight %}
{% endtabs %}

## Add space between bars

The following code snippet illustrates how to add space between bars.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

 //Adding space between bars of different series of single category.
 chart.Series[0].SerieFormat.CommonSerieOptions.Overlap = -40;

 //Adding space between bars of different categories.
 chart.Series[0].SerieFormat.CommonSerieOptions.GapWidth = 100;

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

 //Adding space between bars of different series of single category.
 chart.Series[0].SerieFormat.CommonSerieOptions.Overlap = -40;

 //Adding space between bars of different categories.
 chart.Series[0].SerieFormat.CommonSerieOptions.GapWidth = 100;

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Adding space between bars of different series of a single category.
chart.Series(0).SerieFormat.CommonSerieOptions.Overlap = -40

' Adding space between bars of different categories.
chart.Series(0).SerieFormat.CommonSerieOptions.GapWidth = 100

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Charts/Fomat-Series/Chart-Bar-Spacing/.NET).

## Add High-Low Lines

The following code snippet illustrates how to add high-low lines.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//Set HasHighLowLines property to true.
chart.Series[0].SerieFormat.CommonSerieOptions.HasHighLowLines = true;

//Apply formats to HighLowLines.
chart.Series[0].SerieFormat.CommonSerieOptions.HighLowLines.LineColor = Syncfusion.Drawing.Color.Red;
chart.Series[0].SerieFormat.CommonSerieOptions.HighLowLines.LinePattern = OfficeChartLinePattern.Dot;
chart.Series[0].SerieFormat.CommonSerieOptions.HighLowLines.LineWeight = OfficeChartLineWeight.Hairline;

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

//Set HasHighLowLines property to true.
chart.Series[0].SerieFormat.CommonSerieOptions.HasHighLowLines = true;

//Apply formats to HighLowLines.
chart.Series[0].SerieFormat.CommonSerieOptions.HighLowLines.LineColor = Color.Red;
chart.Series[0].SerieFormat.CommonSerieOptions.HighLowLines.LinePattern = OfficeChartLinePattern.Dot;
chart.Series[0].SerieFormat.CommonSerieOptions.HighLowLines.LineWeight = OfficeChartLineWeight.Hairline;

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Set HasHighLowLines property to true.
chart.Series(0).SerieFormat.CommonSerieOptions.HasHighLowLines = True

' Apply formats to HighLowLines.
chart.Series(0).SerieFormat.CommonSerieOptions.HighLowLines.LineColor = Color.Red
chart.Series(0).SerieFormat.CommonSerieOptions.HighLowLines.LinePattern = OfficeChartLinePattern.Dot
chart.Series(0).SerieFormat.CommonSerieOptions.HighLowLines.LineWeight = OfficeChartLineWeight.Hairline

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Charts/Fomat-Series/Add-High-Low-Lines/.NET).

## Add Drop Lines

The following code snippet illustrates how to add drop lines.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//Set the HasDropLines property to true.
chart.Series[0].SerieFormat.CommonSerieOptions.HasDropLines = true;

//Apply formats to DropLines.
chart.Series[0].SerieFormat.CommonSerieOptions.DropLines.LineColor = Syncfusion.Drawing.Color.Red;
chart.Series[0].SerieFormat.CommonSerieOptions.DropLines.LinePattern = OfficeChartLinePattern.Dot;
chart.Series[0].SerieFormat.CommonSerieOptions.DropLines.LineWeight = OfficeChartLineWeight.Hairline;

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

//Set the HasDropLines property to true.
chart.Series[0].SerieFormat.CommonSerieOptions.HasDropLines = true;

//Apply formats to DropLines.
chart.Series[0].SerieFormat.CommonSerieOptions.DropLines.LineColor = Color.Red;
chart.Series[0].SerieFormat.CommonSerieOptions.DropLines.LinePattern = OfficeChartLinePattern.Dot;
chart.Series[0].SerieFormat.CommonSerieOptions.DropLines.LineWeight = OfficeChartLineWeight.Hairline;

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Set HasDropLines property to true.
chart.Series(0).SerieFormat.CommonSerieOptions.HasDropLines = True

' Apply formats to DropLines.
chart.Series(0).SerieFormat.CommonSerieOptions.DropLines.LineColor = Color.Red
chart.Series(0).SerieFormat.CommonSerieOptions.DropLines.LinePattern = OfficeChartLinePattern.Dot
chart.Series(0).SerieFormat.CommonSerieOptions.DropLines.LineWeight = OfficeChartLineWeight.Hairline

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Charts/Fomat-Series/Add-Drop-Lines/.NET).

## Add Series Lines

The following code snippet illustrates how to add series lines in chart.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//Set HasSeriesLines property to true.
chart.Series[0].SerieFormat.CommonSerieOptions.HasSeriesLines = true;

//Apply formats to SeriesLines.
chart.Series[0].SerieFormat.CommonSerieOptions.PieSeriesLine.LineColor = Syncfusion.Drawing.Color.Red;
chart.Series[0].SerieFormat.CommonSerieOptions.PieSeriesLine.LinePattern = OfficeChartLinePattern.Dot;
chart.Series[0].SerieFormat.CommonSerieOptions.PieSeriesLine.LineWeight = OfficeChartLineWeight.Hairline;

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

//Set HasSeriesLines property to true.
chart.Series[0].SerieFormat.CommonSerieOptions.HasSeriesLines = true;

//Apply formats to SeriesLines.
chart.Series[0].SerieFormat.CommonSerieOptions.PieSeriesLine.LineColor = Color.Red;
chart.Series[0].SerieFormat.CommonSerieOptions.PieSeriesLine.LinePattern = OfficeChartLinePattern.Dot;
chart.Series[0].SerieFormat.CommonSerieOptions.PieSeriesLine.LineWeight = OfficeChartLineWeight.Hairline;

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Set HasSeriesLines property to true.
chart.Series(0).SerieFormat.CommonSerieOptions.HasSeriesLines = True

' Apply formats to SeriesLines.
chart.Series(0).SerieFormat.CommonSerieOptions.PieSeriesLine.LineColor = Color.Red
chart.Series(0).SerieFormat.CommonSerieOptions.PieSeriesLine.LinePattern = OfficeChartLinePattern.Dot
chart.Series(0).SerieFormat.CommonSerieOptions.PieSeriesLine.LineWeight = OfficeChartLineWeight.Hairline

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Charts/Fomat-Series/Add-Series-Lines/.NET).

## Different Marker Properties

The following code snippet illustrates how to customize the marker properties.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//Set the marker style of the first series in the chart.
chart.Series[0].SerieFormat.MarkerStyle = OfficeChartMarkerType.Star;

//Customize the marker style.
chart.Series[0].SerieFormat.MarkerSize = 8;
chart.Series[0].SerieFormat.MarkerBackgroundColor = Syncfusion.Drawing.Color.Red;
chart.Series[0].SerieFormat.MarkerForegroundColor = Syncfusion.Drawing.Color.Black;

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

//Set the marker style of the first series in the chart.
chart.Series[0].SerieFormat.MarkerStyle = OfficeChartMarkerType.Star;

//Customize the marker style.
chart.Series[0].SerieFormat.MarkerSize = 8;
chart.Series[0].SerieFormat.MarkerBackgroundColor = Color.Red;
chart.Series[0].SerieFormat.MarkerForegroundColor = Color.Black;

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Set the marker style of the first series in the chart.
chart.Series(0).SerieFormat.MarkerStyle = OfficeChartMarkerType.Star

' Customize the marker style.
chart.Series(0).SerieFormat.MarkerSize = 8
chart.Series(0).SerieFormat.MarkerBackgroundColor = Color.Red
chart.Series(0).SerieFormat.MarkerForegroundColor = Color.Black

{% endhighlight %}
{% endtabs %}

## Explode a Pie Chart

The following code snippet illustrates how to explode a pie chart.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//Exploding the pie chart to 10%.
chart.Series[0].SerieFormat.Percent = 10;

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

//Exploding the pie chart to 10%.
chart.Series[0].SerieFormat.Percent = 10;

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Exploding the pie chart to 10%.
chart.Series(0).SerieFormat.Percent = 10

{% endhighlight %}
{% endtabs %}


You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Charts/Fomat-Series/Explode-Pie-Chart/.NET).

