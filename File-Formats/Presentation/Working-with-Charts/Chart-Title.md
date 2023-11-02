---
title: Modify the Appearance of Chart Title | Syncfusion
description: Learn how to modify the appearance of chart title in a chart in a PowerPoint using .NET Core PowerPoint library (Presentation) without Microsoft PowerPoint.
platform: file-formats
control: PowerPoint
documentation: UG
---

# Chart Title

Chart title is a concise description at the top of a chart, offering context and clarity for the data displayed. Using Presentation, you can **customize the chart title in the chart**.

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

 FileStream fileStreamPath = new FileStream("Data/Template.pptx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
      
 //Open an existing PowerPoint Presentation.
 using (IPresentation pptxDoc = Presentation.Open(fileStreamPath))
 {
     //Gets the first slide.
     ISlide slide = pptxDoc.Slides[0];
     //Gets the chart in slide.
     IPresentationChart chart = slide.Shapes[0] as IPresentationChart;

     // Set the chart title.
     chart.ChartTitle = "Purchase Details";

     // Customize chart title area.
     chart.ChartTitleArea.FontName = "Calibri";
     chart.ChartTitleArea.Bold = true;
     chart.ChartTitleArea.Color = OfficeKnownColors.Black;
     chart.ChartTitleArea.Underline = OfficeUnderline.WavyHeavy;

     //Manually resizing chart title area using Layout.
     chart.ChartTitleArea.Layout.Left = 5;

     //Enable legend.
     chart.HasLegend = true;
     chart.Legend.Position = OfficeLegendPosition.Right;

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

     // Set the chart title.
     chart.ChartTitle = "Purchase Details";

     // Customize chart title area.
     chart.ChartTitleArea.FontName = "Calibri";
     chart.ChartTitleArea.Bold = true;
     chart.ChartTitleArea.Color = OfficeKnownColors.Black;
     chart.ChartTitleArea.Underline = OfficeUnderline.WavyHeavy;

     //Manually resizing chart title area using Layout.
     chart.ChartTitleArea.Layout.Left = 5;

     //Enable legend.
     chart.HasLegend = true;
     chart.Legend.Position = OfficeLegendPosition.Right;

     //Save the PowerPoint Presentation.
     pptxDoc.Save("Result.pptx");
 }

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

Using pptxDoc As IPresentation = Presentation.Open("Template.pptx")
    ' Gets the first slide.
    Dim slide As ISlide = pptxDoc.Slides(0)
    ' Gets the chart in the slide.
    Dim chart As IPresentationChart = TryCast(slide.Shapes(0), IPresentationChart)

    ' Set the chart title.
    chart.ChartTitle = "Purchase Details"

    ' Customize chart title area.
    chart.ChartTitleArea.FontName = "Calibri"
    chart.ChartTitleArea.Bold = True
    chart.ChartTitleArea.Color = OfficeKnownColors.Black
    chart.ChartTitleArea.Underline = OfficeUnderline.WavyHeavy

    ' Manually resize the chart title area using Layout.
    chart.ChartTitleArea.Layout.Left = 5

    ' Enable legend.
    chart.HasLegend = True
    chart.Legend.Position = OfficeLegendPosition.Right

    ' Save the PowerPoint presentation.
    pptxDoc.Save("Result.pptx")
End Using

{% endhighlight %}
{% endtabs %}
