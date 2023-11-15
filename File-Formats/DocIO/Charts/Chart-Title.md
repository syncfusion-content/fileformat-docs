---
title: Modify the Appearance of Chart Title | Syncfusion
description: Learn how to modify the appearance of chart title in a chart in a Word document using Syncfusion .NET Word (DocIO) library without Microsoft Word.
platform: file-formats
control: DocIO
documentation: UG
---

# Chart Title

Chart title is a concise description at the top of a chart, offering context and clarity for the data displayed. Using DocIO, you can **customize the chart title in the chart**.

## Set the Chart Title Name

The following code snippet illustrates how to set the chart title name.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

// Set the chart title.
chart.ChartTitle = "Purchase Details";

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

// Set the chart title.
chart.ChartTitle = "Purchase Details";

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Set the chart title.
chart.ChartTitle = "Purchase Details"

{% endhighlight %}
{% endtabs %}

## Customize the Chart Title Area

The following code snippet illustrates how to customize the chart title area.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

// Customize chart title area.
chart.ChartTitleArea.FontName = "Calibri";
chart.ChartTitleArea.Bold = true;
chart.ChartTitleArea.Color = OfficeKnownColors.Red;
chart.ChartTitleArea.Underline = OfficeUnderline.DashLong;
chart.ChartTitleArea.Size = 14;

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

// Customize chart title area.
chart.ChartTitleArea.FontName = "Calibri";
chart.ChartTitleArea.Bold = true;
chart.ChartTitleArea.Color = OfficeKnownColors.Red;
chart.ChartTitleArea.Underline = OfficeUnderline.DashLong;
chart.ChartTitleArea.Size = 14;

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Customize chart title area.
chart.ChartTitleArea.FontName = "Calibri"
chart.ChartTitleArea.Bold = True
chart.ChartTitleArea.Color = OfficeKnownColors.Red
chart.ChartTitleArea.Underline = OfficeUnderline.DashLong
chart.ChartTitleArea.Size = 14

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
chart.ChartTitleArea.Layout.ManualLayout.Top = 0.005;
chart.ChartTitleArea.Layout.ManualLayout.Left = 0.26;

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

//Manually resizing chart title area using Layout.
chart.ChartTitleArea.Layout.Top = 10;
chart.ChartTitleArea.Layout.Left = 10;

//Manually resizing chart title area using Manual Layout.
chart.ChartTitleArea.Layout.ManualLayout.Top = 0.005;
chart.ChartTitleArea.Layout.ManualLayout.Left = 0.26;

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Manually resizing chart title area using Layout.
chart.ChartTitleArea.Layout.Top = 10
chart.ChartTitleArea.Layout.Left = 10

' Manually resizing chart title area using Manual Layout.
chart.ChartTitleArea.Layout.ManualLayout.Top = 0.005
chart.ChartTitleArea.Layout.ManualLayout.Left = 0.26

{% endhighlight %}
{% endtabs %}

The complete code snippet illustrating the above options is shown below.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

FileStream fileStreamPath = new FileStream("Data/Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
//Open an existing document from file system through constructor of WordDocument class.
using (WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx))
{
    //Get the paragraph.
    WParagraph paragraph = document.LastParagraph;
    //Get the chart entity.
    WChart chart = paragraph.ChildEntities[0] as WChart;

    // Set the chart title.
    chart.ChartTitle = "Purchase Details";

    // Customize chart title area.
    chart.ChartTitleArea.FontName = "Calibri";
    chart.ChartTitleArea.Bold = true;
    chart.ChartTitleArea.Color = OfficeKnownColors.Black;
    chart.ChartTitleArea.Underline = OfficeUnderline.WavyHeavy;

    //Manually resizing chart title area using Layout.
    chart.ChartTitleArea.Layout.Left = 5;
   
    using (FileStream outputStream = new FileStream("Sample.docx", FileMode.Create, FileAccess.ReadWrite, FileShare.ReadWrite))
    {
        //Save the Word file.
        document.Save(outputStream, FormatType.Docx);
    }
}

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

using (WordDocument document = new WordDocument("Template.docx", FormatType.Docx))
{
    //Get the paragraph.
    WParagraph paragraph = document.LastParagraph;
    //Get the chart entity.
    WChart chart = paragraph.ChildEntities[0] as WChart;
    // Set the chart title.
    chart.ChartTitle = "Purchase Details";

    // Customize chart title area.
    chart.ChartTitleArea.FontName = "Calibri";
    chart.ChartTitleArea.Bold = true;
    chart.ChartTitleArea.Color = OfficeKnownColors.Black;
    chart.ChartTitleArea.Underline = OfficeUnderline.WavyHeavy;

    //Manually resizing chart title area using Layout.
    chart.ChartTitleArea.Layout.Left = 5;
    document.Save("Sample.docx");
}

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

Using document As New WordDocument("Template.docx", FormatType.Docx)
    ' Get the paragraph.
    Dim paragraph As WParagraph = document.LastParagraph

    ' Get the chart entity.
    Dim chart As WChart = TryCast(paragraph.ChildEntities(0), WChart)

    ' Set the chart title.
    chart.ChartTitle = "Purchase Details"

    ' Customize chart title area.
    chart.ChartTitleArea.FontName = "Calibri"
    chart.ChartTitleArea.Bold = True
    chart.ChartTitleArea.Color = OfficeKnownColors.Black
    chart.ChartTitleArea.Underline = OfficeUnderline.WavyHeavy

    ' Manually resize chart title area using Layout.
    chart.ChartTitleArea.Layout.Left = 5

    document.Save("Sample.docx")
End Using

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Charts/Format-Chart-Title/.NET).