---
title: Converting Word document to Image
description: Converting Word document to Image using DocIO
platform: file-formats
control: DocIO
documentation: UG
---

# Rendering / Converting Word document to Image

Essential DocIO supports to convert the Word document to images using `RenderAsImages` method. The following assemblies are need to be referred for converting Word to image.

<table>
<thead> 
<tr>
<th>Assembly Name</th>
<th>Description</th>
</tr>
</thead>
<tr>
<td>
Syncfusion.DocIO.Base<br/><br/></td>
<td>
This assembly has the core features for creating and manipulating Word documents.<br/><br/></td>
</tr>
<tr>
<td>
Syncfusion.Compression.Base<br/><br/></td>
<td>
This assembly is used to package the Word documents<br/><br/></td>
</tr>
<tr>
<td>
Syncfusion.OfficeChart.Base<br/><br/></td>
<td>
This assembly has features to work with chart in Word document.<br/><br/></td>
</tr>
</table>
The following assemblies are need to be referred additionally for converting charts during Word to image conversion:
<table>
<thead> 
<tr>
<th>Assembly Name</th>
<th>Description</th>
</tr>
</thead>
<tr>
<td>
Syncfusion.OfficeChartToImageConverter.WPF<br/><br/></td>
<td>
This assembly is used to convert the chart to image.<br/><br/></td>
</tr>
<tr>
<td>
Syncfusion.SfChart.WPF<br/><br/></td>
<td>
This is supporting assembly for Syncfusion.OfficeChartToImageConverter.WPF<br/><br/></td>
</tr>
</table>

The following namespaces are required to compile the code in this topic.

* using Syncfusion.DocIO
* using Syncfusion.DocIO.DLS
* using Syncfusion.OfficeChart
* using Syncfusion.OfficeChartToImageConverter


T> 1. You can get the converted images in good quality by specifying the image type as Metafile.
T> 2. You can specify the quality of the converted charts by setting the scaling mode.

The following code illustrates how to convert the Word document to image.


{% tabs %}
{% highlight c# %}
//Loads an existing Word document

WordDocument wordDocument = new WordDocument("Template.docx", FormatType.Docx);

//Initializes the ChartToImageConverter for converting charts during Word to image conversion

wordDocument.ChartToImageConverter = new ChartToImageConverter();

//Sets the scaling mode for charts (Normal mode reduces the file size)

wordDocument.ChartToImageConverter.ScalingMode = ScalingMode.Normal;

//Converts word document to image

Image[] images = wordDocument.RenderAsImages(ImageType.Bitmap);

int i = 0;

foreach (Image image in images)

{

//Saves the images as jpeg

image.Save("WordToImage_" + i + ".jpeg", ImageFormat.Jpeg);

i++;

}

//Closes the document

wordDocument.Close();
{% endhighlight %}

{% highlight vb.net %}
'Loads an existing Word document

Dim wordDocument As New WordDocument("Template.docx", FormatType.Docx)

'Initializes the ChartToImageConverter for converting charts during Word to image conversion

wordDocument.ChartToImageConverter = New ChartToImageConverter()

'Sets the scaling mode for charts (Normal mode reduces the file size)

wordDocument.ChartToImageConverter.ScalingMode = ScalingMode.Normal

'Converts word document to image

Dim images As Image() = wordDocument.RenderAsImages(ImageType.Bitmap)

Dim i As Integer = 0

For Each image As Image In images

'Saves the images as jpeg

image.Save("WordToImage_" & i & ".jpeg", ImageFormat.Jpeg)

i += 1

Next

'Closes the document

wordDocument.Close()
{% endhighlight %}
{% endtabs %}

N> 1. Word to Image conversion is not supported in Silverlight, Windows Phone, WinRT, Universal, Xamarin, Azure Web Service, Azure APP Service, ASP.NET Core and Universal Windows Platform applications.
N> 2. Creating an instance of ChartToImageConverter class is mandatory to convert the charts present in the Word document to Image. Otherwise, the charts are not preserved in the generated image.
N> 3. ChartToImageConverter is supported from .NET Framework 4.0 onwards.
N> 4. Total number of images may vary based on unsupported elements in the input Word document.
N> 5. Word to Image conversion has the same limitations and unsupported elements of Word to PDF conversion.
