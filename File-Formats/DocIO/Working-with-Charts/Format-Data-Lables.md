---
title: Modify the Appearance of Data Labels | Syncfusion
description: Learn how to modify the appearance of data labels in a chart in a Word document using Syncfusion .NET Core Word (DocIO) library without Microsoft Word.
platform: file-formats
control: DocIO
documentation: UG
---

# Data Labels

Data labels play a crucial role in enhancing the comprehensibility of a chart. By displaying specific information related to a data series or individual data points, data labels provide valuable context. Using Syncfusion [.NET Core Word (DocIO)](https://www.syncfusion.com/document-processing/word-framework/net-core/word-library) library, you can customize the data labels in the chart.

## Enable Data Labels in Chart

The following code snippet illustrates how to visible the data label in chart.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Enable the datalabel in chart.
chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.IsValue = true;

{% endhighlight %}
{% endtabs %}

## Customize the Data Labels

The following code snippet illustrates how to customize the data label in chart.

{% tabs %}
{% highlight c# tabtitle="C#" %}

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
{% endtabs %}

## Set the Position of Data Labels

The following code snippet illustrates how to set the position of the data label in chart.

{% tabs %}
{% highlight c# tabtitle="C#" %}

// Set the position of data labels for the first series.
chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.Position = OfficeDataLabelPosition.Center;

{% endhighlight %}
{% endtabs %}

The complete code snippet illustrating the above options is shown below.

{% tabs %}
{% highlight c# tabtitle="C#" %}

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
{% endtabs %}

You can download a complete working sample from GitHub.

By executing the program, you will get the **chart** as follows.

## Resize the Data Labels

The following code snippet illustrates how to resize the data label in chart.

{% tabs %}
{% highlight c# tabtitle="C#" %}

//Manually resizing data label area using Layout.
chart.Series[0].DataPoints[0].DataLabels.Layout.Left = 0.09;
chart.Series[0].DataPoints[0].DataLabels.Layout.Top = 0.01;

//Manually resizing data label area using Manual Layout.
chart.Series[0].DataPoints[0].DataLabels.Layout.ManualLayout.Left = 0.09;
chart.Series[0].DataPoints[0].DataLabels.Layout.ManualLayout.Top = 0.01;

{% endhighlight %}
{% endtabs %}

