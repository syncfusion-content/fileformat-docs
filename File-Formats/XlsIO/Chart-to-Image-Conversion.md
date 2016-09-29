---
title: Chart to Image Conversion
description: Briefs about Chart to Image conversion supported in XlsIO
platform: File-formats
control: XlsIO
documentation: UG
---

# Chart to Image Conversion

The following code snippets shows how to convert an Excel chart to an image using the **ExcelChartToImageConverter** class.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

application.ChartToImageConverter = new ChartToImageConverter();

application.ChartToImageConverter.ScalingMode = ScalingMode.Best;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");

IWorksheet worksheet = workbook.Worksheets[0];

IChart chart = worksheet.Charts[0];

//Creating the memory stream for chart image.

MemoryStream stream = new MemoryStream();

//Saving the chart as image.

chart.SaveAsImage(stream);

Image image = Image.FromStream(stream);

//Saving image stream to file.

image.Save("Output.png");

//Closing the workbook and disposing the Excel Engine.

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim ChartToImageConverter As chartToImageConverter = New ChartToImageConverter()

application.ChartToImageConverter = chartToImageConverter

application.ChartToImageConverter.ScalingMode = ScalingMode.Best

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")

Dim worksheet As IWorksheet = workbook.Worksheets(0)

Dim chart As IChart = worksheet.Charts(0)

'Creating the memory stream for chart image.

Dim stream As New MemoryStream()

'Saving the chart as image.

chart.SaveAsImage(stream)

Dim image As Image = Image.FromStream(stream)

'Saving image stream to file.

image.Save("Output.png")

'Closing the workbook and disposing the Excel Engine.

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

N> Chart conversion to image and PDF are supported from .NET Framework 4.0 onwards.