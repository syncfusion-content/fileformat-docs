---
title: Modify the Appearance of Legend | Syncfusion
description: Learn how to modify the appearance of legend in a chart in a Word document using Syncfusion .NET Core Word (DocIO) library without Microsoft Word.
platform: file-formats
control: DocIO
documentation: UG
---

# Legend

Legends are visual pictorial hints that provide a viewer information that helps them understand an chart. Using Syncfusion [.NET Core Word (DocIO)](https://www.syncfusion.com/document-processing/word-framework/net-core/word-library) library, you can customize the legend in the chart.

## Set the Position of Legend

The following code snippet illustrates how to set the legend position in chart.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//Set the position of legend.
chart.Legend.Position = OfficeLegendPosition.Bottom;

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

//Set the position of legend.
chart.Legend.Position = OfficeLegendPosition.Bottom;

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Set the position of legend.
chart.Legend.Position = OfficeLegendPosition.Bottom

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

//Set the position of legend.
chart.Legend.Position = OfficeLegendPosition.Bottom;

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Set the position of legend.
chart.Legend.Position = OfficeLegendPosition.Bottom

{% endhighlight %}
{% endtabs %}

## Customization of Border

The following code snippet illustrates how to modify the border of the legend in chart.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//Sets the legend border format - color, pattern, weight.
chart.Legend.FrameFormat.Border.AutoFormat = false;
chart.Legend.FrameFormat.Border.IsAutoLineColor = false;
chart.Legend.FrameFormat.Border.LineColor = Syncfusion.Drawing.Color.Blue;
chart.Legend.FrameFormat.Border.LinePattern = OfficeChartLinePattern.DashDot;
chart.Legend.FrameFormat.Border.LineWeight = OfficeChartLineWeight.Wide;

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

//Sets the legend border format - color, pattern, weight.
chart.Legend.FrameFormat.Border.AutoFormat = false;
chart.Legend.FrameFormat.Border.IsAutoLineColor = false;
chart.Legend.FrameFormat.Border.LineColor = Color.Blue;
chart.Legend.FrameFormat.Border.LinePattern = OfficeChartLinePattern.DashDot;
chart.Legend.FrameFormat.Border.LineWeight = OfficeChartLineWeight.Wide;

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Sets the legend border format - color, pattern, weight.
chart.Legend.FrameFormat.Border.AutoFormat = False
chart.Legend.FrameFormat.Border.IsAutoLineColor = False
chart.Legend.FrameFormat.Border.LineColor = Color.Blue
chart.Legend.FrameFormat.Border.LinePattern = OfficeChartLinePattern.DashDot
chart.Legend.FrameFormat.Border.LineWeight = OfficeChartLineWeight.Wide

{% endhighlight %}
{% endtabs %}

## Customization of Text Area

The following code snippet illustrates how to modify the text area of the legend in chart.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//Set the legend's text area formatting - font name, weight, color, size.
chart.Legend.TextArea.Bold = true;
chart.Legend.TextArea.Color = OfficeKnownColors.Bright_green;
chart.Legend.TextArea.FontName = "Times New Roman";
chart.Legend.TextArea.Size = 20;
chart.Legend.TextArea.Strikethrough = true;

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

//Set the legend's text area formatting - font name, weight, color, size.
chart.Legend.TextArea.Bold = true;
chart.Legend.TextArea.Color = OfficeKnownColors.Bright_green;
chart.Legend.TextArea.FontName = "Times New Roman";
chart.Legend.TextArea.Size = 20;
chart.Legend.TextArea.Strikethrough = true;

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Set the legend's text area formatting - font name, weight, color, size.
chart.Legend.TextArea.Bold = True
chart.Legend.TextArea.Color = OfficeKnownColors.Bright_green
chart.Legend.TextArea.FontName = "Times New Roman"
chart.Legend.TextArea.Size = 20
chart.Legend.TextArea.Strikethrough = True

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

' Modify the legend entry.
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

' Manually positioning chart legend area using Layout.
chart.Legend.Layout.LeftMode = LayoutModes.Edge
chart.Legend.Layout.TopMode = LayoutModes.Edge

' Manually positioning chart legend area using Manual Layout.
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

' Manually resizing chart legend area using Layout.
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

FileStream fileStreamPath = new FileStream(Path.GetFullPath(@"../../../Data/Template.docx"), FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
//Open an existing document from file system through constructor of WordDocument class.
using (WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx))
{
    //Get the paragraph.
    WParagraph paragraph = document.LastParagraph;
    //Get the chart entity.
    WChart chart = paragraph.ChildEntities[0] as WChart;

    //Enable the legend.
    chart.HasLegend = true;

    //Set the position of legend.
    chart.Legend.Position = OfficeLegendPosition.Right;

    //Legend without overlapping the chart.
    chart.Legend.IncludeInLayout = true;
    chart.Legend.FrameFormat.Border.AutoFormat = false;
    chart.Legend.FrameFormat.Border.IsAutoLineColor = false;
    chart.Legend.FrameFormat.Border.LineColor = Syncfusion.Drawing.Color.Black;
    chart.Legend.FrameFormat.Border.LinePattern = OfficeChartLinePattern.DashDot;
    chart.Legend.FrameFormat.Border.LineWeight = OfficeChartLineWeight.Hairline;

    //Set the legend's text area formatting - font name, weight, color, size.
    chart.Legend.TextArea.Bold = true;
    chart.Legend.TextArea.Color = OfficeKnownColors.Pink;
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
    chart.Legend.Layout.Width = 40;
    chart.Legend.Layout.Height = 40;

    //Legend without overlapping the chart.
    chart.Legend.IncludeInLayout = true;

    using (FileStream outputStream = new FileStream(Path.GetFullPath(@"../../../Sample.docx"), FileMode.Create, FileAccess.ReadWrite, FileShare.ReadWrite))
    {
        //Save the Word file.
        document.Save(outputStream, FormatType.Docx);
    }
}

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

using (WordDocument document = new WordDocument("Template.docx"))
{
    //Get the paragraph.
    WParagraph paragraph = document.LastParagraph;
    //Get the chart entity.
    WChart chart = paragraph.ChildEntities[0] as WChart;

    //Enable the legend.
    chart.HasLegend = true;

    //Set the position of legend.
    chart.Legend.Position = OfficeLegendPosition.Right;

    //Legend without overlapping the chart.
    chart.Legend.IncludeInLayout = true;
    chart.Legend.FrameFormat.Border.AutoFormat = false;
    chart.Legend.FrameFormat.Border.IsAutoLineColor = false;
    chart.Legend.FrameFormat.Border.LineColor = Color.Black;
    chart.Legend.FrameFormat.Border.LinePattern = OfficeChartLinePattern.DashDot;
    chart.Legend.FrameFormat.Border.LineWeight = OfficeChartLineWeight.Hairline;

    //Set the legend's text area formatting - font name, weight, color, size.
    chart.Legend.TextArea.Bold = true;
    chart.Legend.TextArea.Color = OfficeKnownColors.Pink;
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
    chart.Legend.Layout.Width = 40;
    chart.Legend.Layout.Height = 40;

    //Legend without overlapping the chart.
    chart.Legend.IncludeInLayout = true;
    //Save the Word file.
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

You can download a complete working sample from GitHub.

By executing the program, you will get the **chart** as follows.