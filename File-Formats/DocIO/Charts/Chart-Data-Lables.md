---
title: Modify the Appearance of Data Labels | Syncfusion
description: Learn how to modify the appearance of data labels in a chart in a Word document using Syncfusion .NET Word (DocIO) library without Microsoft Word.
platform: file-formats
control: DocIO
documentation: UG
---

# Chart Data Labels

Data Labels on a chart make it easier to understand. They show important information about the lines or points on the chart. Using DocIO, you can **customize the data labels in the chart**.

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

FileStream fileStreamPath = new FileStream(Path.GetFullPath(@"../../../Data/Template.docx"), FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
 //Open an existing document from file system through constructor of WordDocument class.
 using (WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx))
 {
     //Get the paragraph.
     WParagraph paragraph = document.LastParagraph;
     //Get the chart entity.
     WChart chart = paragraph.ChildEntities[0] as WChart;
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
     //Save the Word file.
     document.Save("Sample.docx");
 }

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

Using document As New WordDocument("Template.docx")
    ' Get the paragraph.
    Dim paragraph As WParagraph = document.LastParagraph
    
    ' Get the chart entity.
    Dim chart As WChart = TryCast(paragraph.ChildEntities(0), WChart)
    
    For i As Integer = 0 To chart.Series.Count - 1
        ' Enable the datalabel in chart.
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
    
    ' Save the Word file.
    document.Save("Sample.docx")
End Using

{% endhighlight %}
{% endtabs %}

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