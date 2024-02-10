---
title: Modify the Appearance of Data Labels | Syncfusion
description: Learn how to modify the appearance of data labels in a chart in a PowerPoint using .NET PowerPoint library (Presentation) without Microsoft PowerPoint.
platform: file-formats
control: PowerPoint
documentation: UG
---

# Chart Data Labels

Data Labels on a chart make it easier to understand. They show important information about the lines or points on the chart. Using Presentation, you can **customize the data labels in the chart**.

## Enable Data Labels in Chart

The following code snippet illustrates how to visible the data label in chart.

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

// Set the font size of the data labels.
chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.Size = 8;
// Change the color of the data labels.
chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.Color = OfficeKnownColors.Red;
// Make the data labels bold.
chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.Bold = true;
// Set the font name for the data labels.
chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.FontName = "calibri";
// Make the data labels italic.
chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.Italic = true;

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

// Set the font size of the data labels.
chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.Size = 8;
// Change the color of the data labels.
chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.Color = OfficeKnownColors.Red;
// Make the data labels bold.
chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.Bold = true;
// Set the font name for the data labels.
chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.FontName = "calibri";
// Make the data labels italic.
chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.Italic = true;

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Set the font size of the data labels.
chart.Series(0).DataPoints.DefaultDataPoint.DataLabels.Size = 8
' Change the color of the data labels.
chart.Series(0).DataPoints.DefaultDataPoint.DataLabels.Color = OfficeKnownColors.Red
' Make the data labels bold.
chart.Series(0).DataPoints.DefaultDataPoint.DataLabels.Bold = True
' Set the font name for the data labels.
chart.Series(0).DataPoints.DefaultDataPoint.DataLabels.FontName = "calibri"
' Make the data labels italic.
chart.Series(0).DataPoints.DefaultDataPoint.DataLabels.Italic = True

{% endhighlight %}
{% endtabs %}

## Set the Position of Data Labels

The following code snippet illustrates how to set the position of the data label in chart.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

// Set the position of data labels for the first series.
chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.Position = OfficeDataLabelPosition.Center;

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

// Set the position of data labels for the first series.
chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.Position = OfficeDataLabelPosition.Center;

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Set the position of data labels for the first series.
chart.Series(0).DataPoints.DefaultDataPoint.DataLabels.Position = OfficeDataLabelPosition.Center

{% endhighlight %}
{% endtabs %}

The complete code snippet illustrating the above options is shown below.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

FileStream fileStreamPath = new FileStream("Data/Template.pptx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);

//Open an existing PowerPoint Presentation.
using (IPresentation pptxDoc = Presentation.Open(fileStreamPath))
{
    //Gets the first slide.
    ISlide slide = pptxDoc.Slides[0];
    //Gets the chart in slide.
    IPresentationChart chart = slide.Shapes[0] as IPresentationChart;

    for (int i = 0; i < chart.Series.Count; i++)
    {
        //Enable the datalabel in chart.
        chart.Series[i].DataPoints.DefaultDataPoint.DataLabels.IsValue = true;

        // Set the font size of the data labels.
        chart.Series[i].DataPoints.DefaultDataPoint.DataLabels.Size = 10;
        // Change the color of the data labels. 
        chart.Series[i].DataPoints.DefaultDataPoint.DataLabels.Color = OfficeKnownColors.Black;
        // Make the data labels bold.
        chart.Series[i].DataPoints.DefaultDataPoint.DataLabels.Bold = true;
        // Set the position of data labels for the first series.
        chart.Series[i].DataPoints.DefaultDataPoint.DataLabels.Position = OfficeDataLabelPosition.Center;
    }
    using (FileStream outputStream = new FileStream("Result.pptx", FileMode.Create, FileAccess.ReadWrite, FileShare.ReadWrite))
    {
        //Save the PowerPoint Presentation.
        pptxDoc.Save(outputStream);
    }
}

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

//Open an existing PowerPoint Presentation.
using (IPresentation pptxDoc = Presentation.Open("Template.pptx"))
{
    //Gets the first slide.
    ISlide slide = pptxDoc.Slides[0];
    //Gets the chart in slide.
    IPresentationChart chart = slide.Shapes[0] as IPresentationChart;

    for (int i = 0; i < chart.Series.Count; i++)
    {
        //Enable the datalabel in chart.
        chart.Series[i].DataPoints.DefaultDataPoint.DataLabels.IsValue = true;

        // Set the font size of the data labels.
        chart.Series[i].DataPoints.DefaultDataPoint.DataLabels.Size = 10;
        // Change the color of the data labels. 
        chart.Series[i].DataPoints.DefaultDataPoint.DataLabels.Color = OfficeKnownColors.Black;
        // Make the data labels bold.
        chart.Series[i].DataPoints.DefaultDataPoint.DataLabels.Bold = true;
        // Set the position of data labels for the first series.
        chart.Series[i].DataPoints.DefaultDataPoint.DataLabels.Position = OfficeDataLabelPosition.Center;
    }
    //Save the PowerPoint Presentation.
    pptxDoc.Save("Result.pptx");
}

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Open an existing PowerPoint Presentation.
Using pptxDoc As IPresentation = Presentation.Open("Template.pptx")
    ' Gets the first slide.
    Dim slide As ISlide = pptxDoc.Slides(0)
    ' Gets the chart in the slide.
    Dim chart As IPresentationChart = TryCast(slide.Shapes(0), IPresentationChart)

    For i As Integer = 0 To chart.Series.Count - 1
        ' Enable the datalabel in the chart.
        chart.Series(i).DataPoints.DefaultDataPoint.DataLabels.IsValue = True

        ' Set the font size of the data labels.
        chart.Series(i).DataPoints.DefaultDataPoint.DataLabels.Size = 10
        ' Change the color of the data labels. 
        chart.Series(i).DataPoints.DefaultDataPoint.DataLabels.Color = OfficeKnownColors.Black
        ' Make the data labels bold.
        chart.Series(i).DataPoints.DefaultDataPoint.DataLabels.Bold = True
        ' Set the position of data labels for the first series.
        chart.Series(i).DataPoints.DefaultDataPoint.DataLabels.Position = OfficeDataLabelPosition.Center
    Next

    ' Save the PowerPoint Presentation.
    pptxDoc.Save("Result.pptx")
End Using

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Charts/Format-Data-Labels/.NET).

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

## See Also

* [How to change text of data labels for Chart in Presentation](https://support.syncfusion.com/kb/article/13828/how-to-change-the-text-in-data-labels-inside-a-chart-in-presentation-using-c-in-aspnet-core)
