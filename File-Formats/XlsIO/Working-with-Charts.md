---
title: Working with Charts
description: Briefs about charts operations
platform: File-formats
control: XlsIO
documentation: UG
---
# Working with Charts 

Essential XlsIO has support for creating and modifying Excel charts inside a workbook or as a [chart worksheet](https://support.office.com/en-us/article/Create-a-chart-0baf399e-dd61-4e18-8a73-b3fd5d5680c2). 

## Creating a Chart 

The **IChartShape** interface represents the chart in a worksheet. A chart can be created either through the existing data in the worksheet, directly entering series or by adding series one by one.

The following code example illustrates how to create a chart through the existing data in the worksheet.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

IWorksheet sheet = workbook.Worksheets[0];

//Create a Chart

IChartShape chart = sheet.Charts.Add();

//Set Chart Type

chart.ChartType = ExcelChartType.Column_Clustered;

//Set data range in the worksheet

chart.DataRange = sheet.Range["A1:E5"];

workbook.SaveAs("Chart.xlsx");

workbook.Close();

excelEngine.Dispose();         



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

Dim sheet As IWorksheet= workbook.Worksheets(0)

'Create a Chart

Dim chart As IChartShape = sheet.Charts.Add()

'Set Chart Type

chart.ChartType = ExcelChartType.Column_Clustered

'Set data range in the worksheet

chart.DataRange = sheet.Range("A1:E5")

workbook.SaveAs("Chart.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

### Creating a Chart from directly entered Values

A chart in XlsIO can also be created from directly entered values. The Following code snippets illustrate how to create a chart from directly entered values.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet sheet = workbook.Worksheets[0];

object[] yValues = new object[] { 2000, 1000, 1000 };

object[] xValues = new object[] { "Total Income", "Expenses", "Profit" };

// Adding series and values

IChart chart = sheet.Charts.Add();

IChartSerie serie = chart.Series.Add(ExcelChartType.Pie);

// Enters the X and Y values directly

serie.EnteredDirectlyValues = yValues;

serie.EnteredDirectlyCategoryLabels = xValues;

workbook.SaveAs("Chart.xlsx");

workbook.Close();

excelEngine.Dispose();         



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim sheet As IWorksheet = workbook.Worksheets(0)

Dim yValues As Object() = New Object() {2000, 1000, 1000}

Dim xValues As Object() = New Object() {"Total Income", "Expenses", "Profit"}

' Adding series and values

Dim chart As IChart = sheet.Charts.Add()

Dim serie As IChartSerie = chart.Series.Add(ExcelChartType.Pie)

' Enters the X and Y values directly

serie.EnteredDirectlyValues = yValues

serie.EnteredDirectlyCategoryLabels = xValues

workbook.SaveAs("Chart.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  
 
### Creating a Chart by adding Series

A chart can also be created by adding series one by one. The following code illustrates how to create a chart through series.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet sheet = workbook.Worksheets[0];

//Inserts the sample data for the chart

sheet.Range["A1"].Text = "Month";

sheet.Range["B1"].Text = "Product A";

sheet.Range["C1"].Text = "Product B";

//Months

sheet.Range["A2"].Text = "Jan";

sheet.Range["A3"].Text = "Feb";

sheet.Range["A4"].Text = "Mar";

sheet.Range["A5"].Text = "Apr";

sheet.Range["A6"].Text = "May";

//Create a random Data

Random r = new Random();

for (int i = 2; i <= 6; i++)

{

for (int j = 2; j <= 3; j++)

{

sheet.Range[i, j].Number = r.Next(0, 500);

}

}

IChartShape chart = sheet.Charts.Add();

//Set chart type

chart.ChartType = ExcelChartType.Line;

//Set Chart Title

chart.ChartTitle = "Product Sales comparison";

//Set first serie

IChartSerie productA = chart.Series.Add("ProductA");

productA.Values = sheet.Range["B2:B6"];

productA.CategoryLabels = sheet.Range["A2:A6"];

//Set second serie

IChartSerie productB = chart.Series.Add("ProductB");

productB.Values = sheet.Range["C2:C6"];

productB.CategoryLabels = sheet.Range["A2:A6"];

workbook.SaveAs("chart.xlsx");

workbook.Close();

excelEngine.Dispose();         



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim sheet As IWorksheet = workbook.Worksheets(0)

'Inserting sample data for the chart

sheet.Range("A1").Text = "Month"

sheet.Range("B1").Text = "Product A"

sheet.Range("C1").Text = "Product B"

'Months

sheet.Range("A2").Text = "Jan"

sheet.Range("A3").Text = "Feb"

sheet.Range("A4").Text = "Mar"

sheet.Range("A5").Text = "Apr"

sheet.Range("A6").Text = "May"

'Create a random data

Dim r As Random = New Random

For i As Integer = 2 To 6

For j As Integer = 2 To 3

sheet.Range(i, j).Number = r.Next(0, 500)

Next j

Next i

Dim chart As IChartShape = sheet.Charts.Add()

'Set chart type

chart.ChartType = ExcelChartType.Line

'Set Chart Title

chart.ChartTitle = "Product Sales comparison"

'Set first serie

Dim productA As IChartSerie = chart.Series.Add("ProductA")

productA.Values = sheet.Range("B2:B6")

productA.CategoryLabels = sheet.Range("A2:A6")

'set second serie

Dim productB As IChartSerie = chart.Series.Add("ProductB")

productB.Values = sheet.Range("C2:C6")

productB.CategoryLabels = sheet.Range("A2:A6")

workbook.SaveAs("Chart.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  
 
### Creating a chart Sheet 

The following code snippet shows how to create a chart sheet (separate sheet).

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

IWorksheet sheet = workbook.Worksheets[0];

//Add the chart sheet

IChart chart = workbook.Charts.Add();

chart.ChartType = ExcelChartType.Column_Clustered;

chart.DataRange = sheet.Range["A1:E5"];

workbook.SaveAs("Chart.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

Dim sheet As IWorksheet = workbook.Worksheets(0)

'Add the chart sheet

Dim chart As IChart = workbook.Charts.Add()

chart.ChartType = ExcelChartType.Column_Clustered

chart.DataRange = sheet.Range("A1:E5")

workbook.SaveAs("Chart.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

## Creating Custom Charts 

A custom chart can be created by using different types of charts for different data series. 

For example, you can use a column chart for the first data series and a line chart for the second series. As a result you will have a column chart, combined with a line chart.

The following code sample demonstrates how to create a custom chart. 

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet sheet = workbook.Worksheets[0];

//Insert data for the chart

sheet.Range["A1"].Text = "Crescent City, CA";

sheet.Range["A1:D1"].Merge();

sheet.Range["A1"].CellStyle.Font.Bold = true;

sheet.Range["B3"].Text = "Precipitation,in.";

sheet.Range["C3"].Text = "Temperature,deg.F";

sheet.Range["A4"].Text = "Jan";

sheet.Range["A5"].Text = "Feb";

sheet.Range["A6"].Text = "March";

sheet.Range["B4"].Number = 10.9;

sheet.Range["B5"].Number = 8.9;

sheet.Range["B6"].Number = 8.6;

sheet.Range["C4"].Number = 47.5;

sheet.Range["C5"].Number = 48.7;

sheet.Range["C6"].Number = 48.9;

sheet.UsedRange.AutofitColumns();

// Adding a new chart to the Existing Worksheet

IChart chart = sheet.Charts.Add();

chart.DataRange = sheet.Range["A3:C6"];

chart.Name = "CrescentCity,CA";

chart.ChartTitle = "Crescent City, CA";

chart.IsSeriesInRows = false;

chart.PrimaryValueAxis.Title = "Precipitation,in.";

chart.PrimaryValueAxis.TitleArea.TextRotationAngle = 90;

chart.PrimaryValueAxis.MaximumValue = 14.0;

chart.PrimaryValueAxis.NumberFormat = "0.0";

// Format serie

IChartSerie serieOne = chart.Series[0];

serieOne.Name = "Precipitation,in.";

serieOne.SerieFormat.Fill.FillType = ExcelFillType.Gradient;

serieOne.SerieFormat.Fill.TwoColorGradient(ExcelGradientStyle.Vertical, ExcelGradientVariants.ShadingVariants_2);

serieOne.SerieFormat.Fill.GradientColorType = ExcelGradientColor.TwoColor;

serieOne.SerieFormat.Fill.ForeColor = Color.Plum;

//Format second serie

IChartSerie serieTwo = chart.Series[1];

serieTwo.SerieType = ExcelChartType.Line_Markers;

serieTwo.Name = "Temperature,deg.F";

//Format marker

serieTwo.SerieFormat.MarkerStyle = ExcelChartMarkerType.Diamond;

serieTwo.SerieFormat.MarkerSize = 8;

serieTwo.SerieFormat.MarkerBackgroundColor = Color.DarkGreen;

serieTwo.SerieFormat.MarkerForegroundColor = Color.DarkGreen;

serieTwo.SerieFormat.LineProperties.LineColor = Color.DarkGreen;

//Use Secondary Axis

serieTwo.UsePrimaryAxis = false;

//Display secondary axis for the series.

chart.SecondaryCategoryAxis.IsMaxCross = true;

chart.SecondaryValueAxis.IsMaxCross = true;

//Set title

chart.SecondaryValueAxis.Title = "Temperature,deg.F";

chart.SecondaryValueAxis.TitleArea.TextRotationAngle = 90;

//Hide secondary category axis

chart.SecondaryCategoryAxis.Border.LineColor = Color.Transparent;

chart.SecondaryCategoryAxis.MajorTickMark = ExcelTickMark.TickMark_None;

chart.SecondaryCategoryAxis.TickLabelPosition = ExcelTickLabelPosition.TickLabelPosition_None;

chart.Legend.Position = ExcelLegendPosition.Bottom;

chart.Legend.IsVerticalLegend = false;

workbook.SaveAs("Chart.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim sheet As IWorksheet = workbook.Worksheets(0)

'Insert data for the chart

sheet.Range("A1").Text = "Crescent City, CA"

sheet.Range("A1:D1").Merge()

sheet.Range("A1").CellStyle.Font.Bold = True

sheet.Range("B3").Text = "Precipitation,in."

sheet.Range("C3").Text = "Temperature,deg.F"

sheet.Range("A4").Text = "Jan"

sheet.Range("A5").Text = "Feb"

sheet.Range("A6").Text = "March"

sheet.Range("B4").Number = 10.9

sheet.Range("B5").Number = 8.9

sheet.Range("B6").Number = 8.6

sheet.Range("C4").Number = 47.5

sheet.Range("C5").Number = 48.7

sheet.Range("C6").Number = 48.9

sheet.UsedRange.AutofitColumns()

' Adding a new chart to the Existing Worksheet

Dim chart As IChart = sheet.Charts.Add()

chart.DataRange = sheet.Range("A3:C6")

chart.Name = "CrescentCity,CA"

chart.ChartTitle = "Crescent City, CA"

chart.IsSeriesInRows = False

chart.PrimaryValueAxis.Title = "Precipitation,in."

chart.PrimaryValueAxis.TitleArea.TextRotationAngle = 90

chart.PrimaryValueAxis.MaximumValue = 14.0

chart.PrimaryValueAxis.NumberFormat = "0.0"

' Format serie

Dim serieOne As IChartSerie = chart.Series(0)

serieOne.Name = "Precipitation,in."

serieOne.SerieFormat.Fill.FillType = ExcelFillType.Gradient

serieOne.SerieFormat.Fill.TwoColorGradient(ExcelGradientStyle.Vertical, ExcelGradientVariants.ShadingVariants_2)

serieOne.SerieFormat.Fill.GradientColorType = ExcelGradientColor.TwoColor

serieOne.SerieFormat.Fill.ForeColor = Color.Plum

'Format second serie

Dim serieTwo As IChartSerie = chart.Series(1)

serieTwo.SerieType = ExcelChartType.Line_Markers

serieTwo.Name = "Temperature,deg.F"

'Format marker

serieTwo.SerieFormat.MarkerStyle = ExcelChartMarkerType.Diamond

serieTwo.SerieFormat.MarkerSize = 8

serieTwo.SerieFormat.MarkerBackgroundColor = Color.DarkGreen

serieTwo.SerieFormat.MarkerForegroundColor = Color.DarkGreen

serieTwo.SerieFormat.LineProperties.LineColor = Color.DarkGreen

'Use Secondary Axis

serieTwo.UsePrimaryAxis = False

'Display secondary axis for the series.

chart.SecondaryCategoryAxis.IsMaxCross = True

chart.SecondaryValueAxis.IsMaxCross = True

'Set title

chart.SecondaryValueAxis.Title = "Temperature,deg.F"

chart.SecondaryValueAxis.TitleArea.TextRotationAngle = 90

'Hide secondary category axis

chart.SecondaryCategoryAxis.Border.LineColor = Color.Transparent

chart.SecondaryCategoryAxis.MajorTickMark = ExcelTickMark.TickMark_None

chart.SecondaryCategoryAxis.TickLabelPosition = ExcelTickLabelPosition.TickLabelPosition_None

chart.Legend.Position = ExcelLegendPosition.Bottom

chart.Legend.IsVerticalLegend = False

workbook.SaveAs("Chart.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

![](Working-with-Charts_images/Working-with-charts_img1.jpeg)


## Remove a chart 

The following code snippet shows how to remove the chart from the worksheet using **Remove** method.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

IWorksheet sheet = workbook.Worksheets[0];



IChartShape chart = sheet.Charts[0];

//Remove the chart from the worksheet

chart.Remove();

workbook.SaveAs("Chart.xlsx");

workbook.Close();

excelEngine.Dispose();         



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

Dim sheet As IWorksheet = workbook.Worksheets(0)

Dim chart As IChartShape = sheet.Charts(0)

'Remove the chart from the worksheet

chart.Remove()

workbook.SaveAs("Chart.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  
 
## Chart Appearance Settings

The appearance of a chart can be modified according to the convenience and usage.

### Elements of Chart

The following screen shot shows the elements of chart.

![](Working-with-Charts_images/Working-with-charts_img2.jpeg)


1. The chart area of the chart.
2. The plot area of the chart.
3. The data points of the data series that are plotted in the chart.
4. The horizontal (category) and vertical (value) axis along which the data is plotted in the chart.
5. The legend of the chart.
6. A chart axis title that you can use in the chart.
7. A data label that you can use to identify the details of a data point in a data series.

### Chart Area Appearance 

The following code snippet shows how to modify the appearance of the chart area.

{% tabs %}  
{% highlight c# %}
//Format Chart Area.

IChartFrameFormat chartArea = chart.ChartArea;

//Chart Area Settings

chartArea.Fill.FillType = ExcelFillType.Gradient;

//Set Fill Effects                    

chartArea.Fill.BackColor = Color.FromArgb(205, 217, 234);

chartArea.Fill.ForeColor = Color.White; 



{% endhighlight %}

{% highlight vb %}
'Format Chart Area.

Dim chartArea As IChartFrameFormat = chart.ChartArea

'Chart Area Settings

chartArea.Fill.FillType = ExcelFillType.Gradient

'Set Fill Effects                    

chartArea.Fill.BackColor = Color.FromArgb(205, 217, 234)

chartArea.Fill.ForeColor = Color.White



{% endhighlight %}
{% endtabs %}  

### Plot Area Appearance

The following code snippet shows how to modify the appearance of the plot area.

{% tabs %}  
{% highlight c# %}
//Set Plot Area

IChartFrameFormat  chartPlotArea = chart.PlotArea;



//Set fill color

chartPlotArea.Fill.BackColor = Color.FromArgb(205, 217, 234);

chartPlotArea.Fill.ForeColor = Color.White;





{% endhighlight %}

{% highlight vb %}
'Set Plot Area

Dim chartPlotArea As IChartFrameFormat = chart.PlotArea

'Set fill color

chartPlotArea.Fill.BackColor = Color.FromArgb(205, 217, 234)

chartPlotArea.Fill.ForeColor = Color.White



{% endhighlight %}
{% endtabs %}  

### Data Labels Appearance

The following code snippet illustrates how to modify the appearance of data labels.

{% tabs %}  
{% highlight c# %}
IChartSerie serie =  chart.Series[0];

//Set data labels color             

serie.DataPoints.DefaultDataPoint.DataLabels.Color = ExcelKnownColors.Blue;

serie.DataPoints.DefaultDataPoint.DataLabels.IsValue = true;





{% endhighlight %}

{% highlight vb %}
Dim serie As IChartSerie = chart.Series(0)

'Set data labels color             

serie.DataPoints.DefaultDataPoint.DataLabels.Color = ExcelKnownColors.Blue

serie.DataPoints.DefaultDataPoint.DataLabels.IsValue = True



{% endhighlight %}
{% endtabs %}  

### Series Appearance

The following code snippet illustrates how to modify the appearance of chart series.

{% tabs %}  
{% highlight c# %}
IChartSerie serie =  chart.Series[0];

//Fill Effects                    

serie.SerieFormat.Fill.FillType = ExcelFillType.Gradient;

serie.SerieFormat.Fill.ForeColor = Color.Yellow;



{% endhighlight %}

{% highlight vb %}
Dim serie As IChartSerie = chart.Series(0)

'Fill Effects                    

serie.SerieFormat.Fill.FillType = ExcelFillType.Gradient

serie.SerieFormat.Fill.ForeColor = Color.Yellow



{% endhighlight %}
{% endtabs %}  

The complete code snippet illustrating the above options is shown below.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

IWorksheet sheet = workbook.Worksheets[0];

IChartShape chart = sheet.Charts.Add();

chart.DataRange = sheet.UsedRange;

//Format Chart Area

IChartFrameFormat chartArea = chart.ChartArea;

//Fill Effects

chartArea.Fill.FillType = ExcelFillType.Gradient;

//Set chart area fill color

chartArea.Fill.BackColor = Color.FromArgb(205, 217, 234);

chartArea.Fill.ForeColor = Color.WhiteSmoke;

//Plot Area

IChartFrameFormat chartPlotArea = chart.PlotArea;

//Fill Effects

chartPlotArea.Fill.FillType = ExcelFillType.Gradient;

//Set plot area fill color 

chartPlotArea.Fill.BackColor = Color.FromArgb(205, 217, 234);

chartPlotArea.Fill.ForeColor = Color.YellowGreen;

workbook.SaveAs("Chart.xlsx");

workbook.Close();

excelEngine.Dispose();





{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

Dim sheet As IWorksheet = workbook.Worksheets(0)

Dim chart As IChartShape = sheet.Charts.Add()

chart.DataRange = sheet.UsedRange

'Format Chart Area.

Dim chartArea As IChartFrameFormat = chart.ChartArea

'Fill Effects

chartArea.Fill.FillType = ExcelFillType.Gradient

'Set chart area fill color

chartArea.Fill.BackColor = Color.FromArgb(205, 217, 234)

chartArea.Fill.ForeColor = Color.White

'Plot Area

Dim chartPlotArea As IChartFrameFormat = chart.PlotArea

'Fill Effects

chartPlotArea.Fill.FillType = ExcelFillType.Gradient

'Set plot area fill color

chartPlotArea.Fill.BackColor = Color.FromArgb(205, 217, 234)

chartPlotArea.Fill.ForeColor = Color.White

workbook.SaveAs("Chart.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

## Applying 3D Formats

The following code example explains how to apply 3D settings such as side wall, back wall, and floor settings.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Create(2);

IWorksheet sheet = workbook.Worksheets[0];

//Insert the data in sheet-1.

sheet.Range["B1"].Text = "Product-A";

sheet.Range["C1"].Text = "Product-B";

sheet.Range["D1"].Text = "Product-C";

sheet.Range["A2"].Text = "Jan";

sheet.Range["A3"].Text = "Feb";

sheet.Range["B2"].Number = 25;

sheet.Range["B3"].Number = 20;

sheet.Range["C2"].Number = 35;

sheet.Range["C3"].Number = 25;

sheet.Range["D2"].Number = 40;

sheet.Range["D3"].Number = 55;

IChartShape chart = sheet.Charts.Add();

chart.DataRange = sheet.Range["A1:D3"];

chart.ChartType = ExcelChartType.Column_Clustered_3D;

//Set Rotation of the 3D chart view.

chart.Rotation = 90;

//Set Back wall fill option

chart.BackWall.Fill.FillType = ExcelFillType.Gradient;

//Set Back wall thickness

chart.BackWall.Thickness = 10;

//Set Texture Type

chart.BackWall.Fill.GradientColorType = ExcelGradientColor.TwoColor;

chart.BackWall.Fill.GradientStyle = ExcelGradientStyle.Diagonal_Down;

chart.BackWall.Fill.ForeColor = System.Drawing.Color.WhiteSmoke;

chart.BackWall.Fill.BackColor = System.Drawing.Color.LightBlue;

//Set side wall fill option

chart.SideWall.Fill.FillType = ExcelFillType.SolidColor;

//Set side wall fore and back color

chart.SideWall.Fill.BackColor = System.Drawing.Color.White;

chart.SideWall.Fill.ForeColor = System.Drawing.Color.White;

//Set floor fill option

chart.Floor.Fill.FillType = ExcelFillType.Pattern;

//Set floor fore and Back color

chart.Floor.Fill.ForeColor = System.Drawing.Color.Blue;

chart.Floor.Fill.BackColor = System.Drawing.Color.White;

//Set floor thickness

chart.Floor.Thickness = 3;

workbook.SaveAs("Chart.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Create(2)

Dim sheet As IWorksheet = workbook.Worksheets(0)

'Insert data in sheet-1. 

sheet.Range("B1").Text = "Product-A"

sheet.Range("C1").Text = "Product-B"

sheet.Range("D1").Text = "Product-C"

sheet.Range("A2").Text = "Jan"

sheet.Range("A3").Text = "Feb"

sheet.Range("B2").Number = 25

sheet.Range("B3").Number = 20

sheet.Range("C2").Number = 35

sheet.Range("C3").Number = 25

sheet.Range("D2").Number = 40

sheet.Range("D3").Number = 55

Dim chart As IChartShape = sheet.Charts.Add()

chart.DataRange = sheet.Range("A1:D3")

chart.ChartType = ExcelChartType.Column_Clustered_3D

'Set Rotation of the 3D chart view.

chart.Rotation = 90

'Set Back wall fill option

chart.BackWall.Fill.FillType = ExcelFillType.Gradient

'Set Texture Type

chart.BackWall.Fill.GradientColorType = ExcelGradientColor.TwoColor

chart.BackWall.Fill.GradientStyle = ExcelGradientStyle.Diagonal_Down

chart.BackWall.Fill.ForeColor = System.Drawing.Color.WhiteSmoke

chart.BackWall.Fill.BackColor = System.Drawing.Color.LightBlue

'Set Back wall thickness

chart.BackWall.Thickness = 10

'Set side wall fill option

chart.SideWall.Fill.FillType = ExcelFillType.SolidColor

'Set sidewall fore and back color

chart.SideWall.Fill.BackColor = System.Drawing.Color.White

chart.SideWall.Fill.ForeColor = System.Drawing.Color.White

'Set floor fill option

chart.Floor.Fill.FillType = ExcelFillType.Pattern

'Set floor fore and Back color

chart.Floor.Fill.ForeColor = System.Drawing.Color.Blue

chart.Floor.Fill.BackColor = System.Drawing.Color.White

'Set floor thickness

chart.Floor.Thickness = 3

workbook.SaveAs("Chart.xlsx")

workbook.Close()

excelEngine.Dispose()





{% endhighlight %}
{% endtabs %}  

## Customizing chart and Chart Elements

### Positioning Chart

Chart can be positioned by specifying row and column indexes. The following code samples illustrates how to position a chart in a worksheet.

{% tabs %}  
{% highlight c# %}
//Positioning chart in a worksheet

chart.TopRow = 5;

chart.LeftColumn = 5;

chart.RightColumn = 10;

chart.BottomRow = 10;





{% endhighlight %}

{% highlight vb %}
'Positioning chart in a worksheet

chart.TopRow = 5

chart.LeftColumn = 5

chart.RightColumn = 10

chart.BottomRow = 10





{% endhighlight %}
{% endtabs %}  

### Positioning Chart Elements

The following code examples illustrate how to position the chart elements.

{% tabs %}  
{% highlight c# %}
//Manually positioning plot area

chart.PlotArea.Layout.LayoutTarget = LayoutTargets.inner;

chart.PlotArea.Layout.LeftMode = LayoutModes.edge;

chart.PlotArea.Layout.TopMode = LayoutModes.edge;

//Manually positioning chart legend 

chart.Legend.Layout.LeftMode = LayoutModes.edge;

chart.Legend.Layout.TopMode = LayoutModes.edge;





{% endhighlight %}

{% highlight vb %}
'Manually positioning plot area

chart.PlotArea.Layout.LayoutTarget = LayoutTargets.inner

chart.PlotArea.Layout.LeftMode = LayoutModes.edge

chart.PlotArea.Layout.TopMode = LayoutModes.edge

'Manually positioning chart legend

chart.Legend.Layout.LeftMode = LayoutModes.edge

chart.Legend.Layout.TopMode = LayoutModes.edge





{% endhighlight %}
{% endtabs %}  

### Resizing Chart


The following code sample illustrates how to resize a chart in a worksheet.

{% tabs %}  
{% highlight c# %}
IShape chart = chartShape as IShape;

// Set Height of the chart in pixels
chart.Height = 300;

// Set Width of the chart
chart.Width = 500; 



{% endhighlight %}

{% highlight vb %}
Dim chart As IShape = chartShape as IShape

'Set Height of the chart
chart.Height = 300

'Set Width of the chart
chart.Width = 500





{% endhighlight %}
{% endtabs %}  

### Resizing Chart Elements

The following code examples illustrate how to resize chart elements such as plot area and legend.

{% tabs %}  
{% highlight c# %}
//Manually resizing chart plot area
chart.PlotArea.Layout.Left = 50;
chart.PlotArea.Layout.Top = 75;
chart.PlotArea.Layout.Width = 300;
chart.PlotArea.Layout.Height = 200;

//Manually resizing chart legend 
chart.Legend.Layout.Left = 400;
chart.Legend.Layout.Top = 150;
chart.Legend.Layout.Width = 150;
chart.Legend.Layout.Height = 100;





{% endhighlight %}

{% highlight vb %}
'Manually resizing chart plot area
chart.PlotArea.Layout.Left = 50
chart.PlotArea.Layout.Top = 75
chart.PlotArea.Layout.Width = 300            
chart.PlotArea.Layout.Height = 200

'Manually resizing chart legend 
chart.Legend.Layout.Left = 400          
chart.Legend.Layout.Top = 150           
chart.Legend.Layout.Width = 150           
chart.Legend.Layout.Height = 100



{% endhighlight %}
{% endtabs %}  

### Chart with transparent background

The following code example explains how to apply transparency to chart area.

{% tabs %}  
{% highlight c# %}
//Applying transparency to chart area

chart.ChartArea.Fill.Transparency = 0.9;



{% endhighlight %}

{% highlight vb %}
'Applying transparency to chart area

chart.ChartArea.Fill.Transparency = 0.9



{% endhighlight %}
{% endtabs %}  

### Chart with style changes

The following code example explains how to set style of the chart.

{% tabs %}  
{% highlight c# %}
//Set chart style

chart.Style = 25;



{% endhighlight %}

{% highlight vb %}
'Set chart style

chart.Style = 25



{% endhighlight %}
{% endtabs %}  

N>style value must be between 1 to 48, Otherwise argument exception will be thrown and style value changes will not affect to 2016 charts.

The complete code snippet illustrating the above options is shown below.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

IWorksheet sheet = workbook.Worksheets[0];

IChartShape chart = sheet.Charts[0];

//Positioning chart in a worksheet

chart.TopRow = 5;

chart.LeftColumn = 5;

chart.RightColumn = 10;

chart.BottomRow = 10;

//Manually positioning plot area

chart.PlotArea.Layout.LayoutTarget = LayoutTargets.inner;

chart.PlotArea.Layout.LeftMode = LayoutModes.edge;

chart.PlotArea.Layout.TopMode = LayoutModes.edge;

//Manually positioning chart legend

chart.Legend.Layout.LeftMode = LayoutModes.edge;

chart.Legend.Layout.TopMode = LayoutModes.edge;

IShape chartShape = chart as IShape;

// Set Height of the chart in pixels

chartShape.Height = 300;

// Set Width of the chart

chartShape.Width =  500;

//Manually resizing chart plot area

chart.PlotArea.Layout.Left = 50;

chart.PlotArea.Layout.Top = 75;

chart.PlotArea.Layout.Width = 300;

chart.PlotArea.Layout.Height = 200;

//Manually resizing chart legend

chart.Legend.Layout.Left = 400;

chart.Legend.Layout.Top = 150;

chart.Legend.Layout.Width = 200;

chart.Legend.Layout.Height = 100;

//Applying transparency to chart area

chart.ChartArea.Fill.Transparency = 0.9;

//Set chart style

chart.Style = 25;

workbook.SaveAs("Chart.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

Dim sheet As IWorksheet = workbook.Worksheets(0)

Dim chart As IChartShape = sheet.Charts(0)

'Positioning chart in a worksheet

chart.TopRow = 5

chart.LeftColumn = 5

chart.RightColumn = 10

chart.BottomRow = 10

'Manually positioning plot area

chart.PlotArea.Layout.LayoutTarget = LayoutTargets.inner

chart.PlotArea.Layout.LeftMode = LayoutModes.edge

chart.PlotArea.Layout.TopMode = LayoutModes.edge

'Manually positioning chart legend

chart.Legend.Layout.LeftMode = LayoutModes.edge

chart.Legend.Layout.TopMode = LayoutModes.edge

Dim chartShape As IShape = TryCast(chart, IShape)

' Set Height of the chart in pixels

chartShape.Height = 300

' Set Width of the chart

chartShape.Width = 500

'Manually resizing chart plot area

chart.PlotArea.Layout.Left = 50

chart.PlotArea.Layout.Top = 75

chart.PlotArea.Layout.Width = 300

chart.PlotArea.Layout.Height = 200

'Manually resizing chart legend

chart.Legend.Layout.Left = 400

chart.Legend.Layout.Top = 150

chart.Legend.Layout.Width = 200

chart.Legend.Layout.Height = 100

'Applying transparency to chart area

chart.ChartArea.Fill.Transparency = 0.9

'Set chart style

chart.Style = 25

workbook.SaveAs("Chart.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

N> In order to position the chart elements, plot area should be smaller than chart area.

## Sparkline 

[Sparkline](https://support.office.com/en-za/article/About-sparklines-bf2059c8-1f44-4dbf-aa2e-ca792a139849) is a small chart in a worksheet cell that provides a visual representation of data.

### Sparkline Creation Using XlsIO

XlsIO provides support for creation, modification and removal of Sparklines.

* **ISparklineGroups** interface caches the SparklineGroup that need to be added to the Spreadsheet. 
* **ISparklineGroup** represents Sparklines in object, and has properties that allows  to customize it. 
* **ISparklines** interface returns the collection of Sparkline present in a Worksheet. 
* **ISparkline** represents a sparkline in the Sparklines. Currently, XlsIO supports all the three types of sparklines - Line, Column, Win/Loss.

Following code example illustrates how to create Sparklines by using XlsIO.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("spark.xlsx", ExcelOpenType.Automatic);

IWorksheet sheet = workbook.Worksheets[0];

//Add SparklineGroups

ISparklineGroup sparklineGroup = sheet.SparklineGroups.Add();

//Add SparkLineType

sparklineGroup.SparklineType = SparklineType.Line;

sparklineGroup.MarkersColor = Color.BlueViolet;

//Add sparklines

ISparklines sparklines = sparklineGroup.Add();

IRange dataRange = sheet.Range["B2:F4"];

IRange referenceRange = sheet.Range["G2:G4"];

sparklines.Add(dataRange, referenceRange);

string fileName = "Sparkline.xlsx";

workbook.SaveAs(fileName);

workbook.Close();

excelEngine.Dispose();





{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("spark.xlsx", ExcelOpenType.Automatic)

Dim sheet As IWorksheet = workbook.Worksheets(0)

'Add SparklineGroups

Dim sparklineGroup As ISparklineGroup = sheet.SparklineGroups.Add()

'Add SparkLineType

sparklineGroup.SparklineType = SparklineType.Line

sparklineGroup.MarkersColor = Color.BlueViolet

'Add sparklines

Dim sparklines As ISparklines = sparklineGroup.Add()

Dim dataRange As IRange = sheet.Range("B2:F4")

Dim referenceRange As IRange = sheet.Range("G2:G4")

sparklines.Add(dataRange, referenceRange)

Dim fileName As String = "Sparkline.xlsx"

workbook.SaveAs(fileName)

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

### Modifying an existing spark line

XlsIO provides an option to edit the data of existing Sparklines. The following code snippet shows how to achieve this.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("Sparkline.xlsx", ExcelOpenType.Automatic);

IWorksheet sheet = workbook.Worksheets[0];

ISparklineGroup sparklineGroup = sheet.SparklineGroups[0];

ISparklines sparklines = sparklineGroup[0];

IRange dataRange = sheet["A1:C4"];

IRange referenceRange = sheet["D1:D4"];

//Edit the existing sparklines data

sparklines.RefreshRanges(dataRange, referenceRange);

workbook.SaveAs("Output.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("Sparkline.xlsx", ExcelOpenType.Automatic)

Dim sheet As IWorksheet = workbook.Worksheets(0)

Dim sparklineGroup As ISparklineGroup = sheet.SparklineGroups(0)

Dim sparklines As ISparklines = sparklineGroup(0)

Dim dataRange As IRange = sheet("A1:C4")

Dim referenceRange As IRange = sheet("D1:D4")

'Edit the existing sparklines data

sparklines.RefreshRanges(dataRange, referenceRange)

workbook.SaveAs("Output.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

### Removing Sparklines

XlsIO provides an API to remove sparklines from the sparkline group and also the sparkline group from the worksheet. This is illustrated in the following code.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

IWorksheet sheet = workbook.Worksheets[0];

ISparklineGroup sparklineGroup = sheet.SparklineGroups[0];

ISparklines sparklines = sparklineGroup[0];

//Remove sparkline specified by index from the sparklines.

sparklines.Remove(sparklines[1]);

//Remove sparklines from the sparkline group.

sparklineGroup.Remove(sparklines);

//Remove sparkline group from the sheet.

sheet.SparklineGroups.Remove(sparklineGroup);

workbook.SaveAs("Output.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

Dim sheet As IWorksheet = workbook.Worksheets(0)

Dim sparklineGroup As ISparklineGroup = sheet.SparklineGroups(0)

Dim sparklines As ISparklines = sparklineGroup(0)

'Remove sparkline specified by index from the sparklines.

sparklines.Remove(sparklines(1))

'Remove sparklines from the sparkline group.

sparklineGroup.Remove(sparklines)

'Remove sparkline group from the sheet.

sheet.SparklineGroups.Remove(sparklineGroup)

workbook.SaveAs("Output.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

N> Sparklines are supported only from Excel 2007 onwards and are ignored in the earlier versions.

## Excel 2016 Charts

Essential XlsIO supports creating and manipulating new and modern chart types such as waterfall, histogram, pareto, box and whisker, tree map, and sunburst, all of which are introduced in Microsoft Excel 2016.

### Funnel

[Funnel](https://support.office.com/en-us/article/Create-a-funnel-chart-ba21bcba-f325-4d9f-93df-97074589a70e#) charts show values across multiple stages in a process.

Following code example illustrates how to create Funnel chart.

{% tabs %}
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2016;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

IWorksheet sheet = workbook.Worksheets[0];

//Create a chart

IChartShape chart = sheet.Charts.Add();

//Set chart type as Funnel

chart.ChartType = ExcelChartType.Funnel;

//Set data range in the worksheet

chart.DataRange = sheet.Range["A1:B6"];

//Set the chart title

chart.ChartTitle = "Funnel";

//Formatting the legend and data label option

chart.HasLegend = false;

chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.IsValue = true;

chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.Size = 8;

workbook.SaveAs("Funnel.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2016

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

Dim sheet As IWorksheet = workbook.Worksheets(0)

'Create a chart

Dim chart As IChartShape = sheet.Charts.Add()

'Set chart type as Funnel

chart.ChartType = ExcelChartType.Funnel

'Set data range in the worksheet

chart.DataRange = sheet.Range("A1:B6")

'Set the chart title

chart.ChartTitle = "Funnel"

'Formatting the legend and data label option

chart.HasLegend = False

chart.Series(0).DataPoints.DefaultDataPoint.DataLabels.IsValue = True

chart.Series(0).DataPoints.DefaultDataPoint.DataLabels.Size = 8

workbook.SaveAs("Funnel.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}

The input template can be downloaded [here](http://www.syncfusion.com/downloads/support/directtrac/general/ze/Funnel1191611286.zip#).


The following screen shot shows the output of above code.

![](Working-with-Charts_images/funnel.jpeg)



### Box and Whisker

[Box and Whisker](https://support.office.com/en-us/article/Create-a-box-and-whisker-chart-62f4219f-db4b-4754-aca8-4743f6190f0d#) chart shows distribution of data into quartiles, highlighting the mean and outliers. Box and Whisker charts are most commonly used in statistical analysis.

Following code example illustrates how to create Box and Whisker chart.

{% tabs %}
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2016;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

IWorksheet sheet = workbook.Worksheets[0];

//Create a chart

IChartShape chart = sheet.Charts.Add();

//Set the chart title

chart.ChartTitle = "Test Scores";

//Set chart type as Box and Whisker

chart.ChartType = ExcelChartType.BoxAndWhisker;

//Set data range in the worksheet

chart.DataRange = sheet["A1:D16"];

//Box and Whisker settings on first series

IChartSerie seriesA = chart.Series[0];

seriesA.SerieFormat.ShowInnerPoints = false;

seriesA.SerieFormat.ShowOutlierPoints = true;

seriesA.SerieFormat.ShowMeanMarkers = true;

seriesA.SerieFormat.ShowMeanLine = false;

seriesA.SerieFormat.QuartileCalculationType = ExcelQuartileCalculation.ExclusiveMedian;

//Box and Whisker settings on second series   

IChartSerie seriesB = chart.Series[1];

seriesB.SerieFormat.ShowInnerPoints = false;

seriesB.SerieFormat.ShowOutlierPoints = true;

seriesB.SerieFormat.ShowMeanMarkers = true;

seriesB.SerieFormat.ShowMeanLine = false;

seriesB.SerieFormat.QuartileCalculationType = ExcelQuartileCalculation.InclusiveMedian;

//Box and Whisker settings on third series   

IChartSerie seriesC = chart.Series[2];

seriesC.SerieFormat.ShowInnerPoints = false;

seriesC.SerieFormat.ShowOutlierPoints = true;

seriesC.SerieFormat.ShowMeanMarkers = true;

seriesC.SerieFormat.ShowMeanLine = false;

seriesC.SerieFormat.QuartileCalculationType = ExcelQuartileCalculation.ExclusiveMedian; 

workbook.SaveAs("Box and Whisker.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2016

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

Dim sheet As IWorksheet= workbook.Worksheets(0)

'Create a chart

Dim chart As IChartShape = sheet.Charts.Add()

'Set the chart title

chart.ChartTitle = "Test Scores"

'Set chart type as Box and Whisker

chart.ChartType = ExcelChartType.BoxAndWhisker

'Set data range in the worksheet

chart.DataRange = sheet("A1:D16")

'Box and Whisker settings on first series

Dim seriesA As IChartSerie = chart.Series(0)

seriesA.SerieFormat.ShowInnerPoints = False

seriesA.SerieFormat.ShowOutlierPoints = True

seriesA.SerieFormat.ShowMeanMarkers = True

seriesA.SerieFormat.ShowMeanLine = False

seriesA.SerieFormat.QuartileCalculationType = ExcelQuartileCalculation.ExclusiveMedian 

'Box and Whisker settings on second series          

Dim seriesB As IChartSerie = chart.Series(1)

seriesB.SerieFormat.ShowInnerPoints = False

seriesB.SerieFormat.ShowOutlierPoints = True

seriesB.SerieFormat.ShowMeanMarkers = True

seriesB.SerieFormat.ShowMeanLine = False

seriesB.SerieFormat.QuartileCalculationType = ExcelQuartileCalculation.InclusiveMedian

'Box and Whisker settings on third series  

Dim seriesC As IChartSerie = chart.Series(2)

seriesC.SerieFormat.ShowInnerPoints = False

seriesC.SerieFormat.ShowOutlierPoints = True

seriesC.SerieFormat.ShowMeanMarkers = True

seriesC.SerieFormat.ShowMeanLine = False

seriesC.SerieFormat.QuartileCalculationType = ExcelQuartileCalculation.ExclusiveMedian

workbook.SaveAs("Box and Whisker.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}

The input template can be downloaded [here](http://www.syncfusion.com/downloads/support/directtrac/general/ze/Box_and_Whisker1075978354.zip#).


The following screen shot shows the output of above code.

![](Working-with-Charts_images/boxandwhisker.jpeg)




### Waterfall

[Waterfall](https://support.office.com/en-us/article/Create-a-waterfall-chart-in-Office-2016-8de1ece4-ff21-4d37-acd7-546f5527f185#) chart helps to quickly understand the finances of business owners by viewing profit and loss statements. With a Waterfall chart, you can quickly illustrate the line items in your financial data and get a clear picture of how each item is impacting your bottom line.

Following code example illustrates how to create Waterfall chart.

{% tabs %}
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2016;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

IWorksheet sheet = workbook.Worksheets[0];

//Create a chart

IChartShape chart = sheet.Charts.Add();

//Set chart type as Waterfall

chart.ChartType = ExcelChartType.WaterFall;

//Set data range in the worksheet

chart.DataRange = sheet["A2:B8"];

//Data point settings as total in chart

chart.Series[0].DataPoints[3].SetAsTotal = true;

chart.Series[0].DataPoints[6].SetAsTotal = true;

//Showing the connector lines between data points

chart.Series[0].SerieFormat.ShowConnectorLines = true;

//Set the chart title

chart.ChartTitle = "Company Profit (in USD)";

//Formatting data label and legend option

chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.IsValue = true;

chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.Size = 8;

chart.Legend.Position = ExcelLegendPosition.Right;

workbook.SaveAs("Waterfall.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2016

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

Dim sheet As IWorksheet = workbook.Worksheets(0)

'Create a chart

Dim chart As IChartShape = sheet.Charts.Add()

'Set chart type as Waterfall

chart.ChartType = ExcelChartType.WaterFall

'Set data range in the worksheet

chart.DataRange = sheet("A2:B8")

'Datapoint settings as total in chart

chart.Series(0).DataPoints(3).SetAsTotal = True

chart.Series(0).DataPoints(6).SetAsTotal = True

'Showing the connector lines between data points

chart.Series(0).SerieFormat.ShowConnectorLines = True

'Set the chart title

chart.ChartTitle = "Company Profit (in USD)"

'Formatting data label and legend option

chart.Series(0).DataPoints.DefaultDataPoint.DataLabels.IsValue = True

chart.Series(0).DataPoints.DefaultDataPoint.DataLabels.Size = 8

chart.Legend.Position = ExcelLegendPosition.Right

workbook.SaveAs("Waterfall.xlsx")

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}

The input template can be downloaded [here.](http://www.syncfusion.com/downloads/support/directtrac/general/ze/waterfall1416377471.zip#)

The following screen shot shows the output of above code.

![](Working-with-Charts_images/waterfall.jpeg)



### Histogram

[Histogram](https://support.office.com/en-us/article/Create-a-histogram-85680173-064b-4024-b39d-80f17ff2f4e8# ) shows the frequencies within a distribution. Each column of the chart is called a bin, which can be changed further to analyze the data.

Following code example illustrates how to create Histogram.

{% tabs %}
{% highlight c# %}

ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2016;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

IWorksheet sheet = workbook.Worksheets[0];

//Create a chart

IChartShape chart = sheet.Charts.Add();

//Set chart type as Histogram       

chart.ChartType = ExcelChartType.Histogram;

//Set data range in the worksheet   

chart.DataRange = sheet["A1:A15"];

//Category axis bin settings        

chart.PrimaryCategoryAxis.BinWidth = 8;

//Gap width settings

chart.Series[0].SerieFormat.CommonSerieOptions.GapWidth = 6;

//Set the chart title and axis title

chart.ChartTitle = "Height Data";

chart.PrimaryValueAxis.Title = "Number of students";

chart.PrimaryCategoryAxis.Title = "Height";

//Hiding the legend

chart.HasLegend = false;

workbook.SaveAs("Histogram.xlsx");

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2016

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

Dim sheet As IWorksheet = workbook.Worksheets(0)

'Create a chart

Dim chart As IChartShape = sheet.Charts.Add()

'Set chart type as Histogram                 

chart.ChartType = ExcelChartType.Histogram

'Set data range in the worksheet

chart.DataRange = sheet("A1:A15")

'Category axis bin settings     

chart.PrimaryCategoryAxis.BinWidth = 8

'Gap width settings

chart.Series(0).SerieFormat.CommonSerieOptions.GapWidth = 6

'Set the chart title and axis title

chart.ChartTitle = "Height Data"

chart.PrimaryValueAxis.Title = "Number of students"

chart.PrimaryCategoryAxis.Title = "Height"

'Hiding the legend

chart.HasLegend = False

workbook.SaveAs("Histogram.xlsx")

workbook.Close()

excelEngine.Dispose()


{% endhighlight %}
{% endtabs %}

The input template can be downloaded [here.](http://www.syncfusion.com/downloads/support/directtrac/general/ze/histogram1512012627.zip#)

The following screen shot shows the output of above code.

![](Working-with-Charts_images/histogram.jpeg)


### Pareto

[Pareto](https://support.office.com/en-us/article/Create-a-Pareto-chart-a1512496-6dba-4743-9ab1-df5012972856#) is a sorted histogram where columns sorted in descending order and a line representing the cumulative total percentage.

Following code example illustrates how to create Pareto chart.

{% tabs %}

{% highlight c# %}

ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2016;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

IWorksheet sheet = workbook.Worksheets[0];

//Create a chart

IChartShape chart = sheet.Charts.Add();

//Set chart type as Pareto

chart.ChartType = ExcelChartType.Pareto;

//Set data range in the worksheet   

chart.DataRange = sheet["A2:B8"];

//Set category values as bin values   

chart.PrimaryCategoryAxis.IsBinningByCategory = true;

//Formatting Pareto line      

chart.Series[0].ParetoLineFormat.LineProperties.ColorIndex = ExcelKnownColors.Bright_green;

//Gap width settings

chart.Series[0].SerieFormat.CommonSerieOptions.GapWidth = 6;

//Set the chart title

chart.ChartTitle = "Expenses";

//Hiding the legend

chart.HasLegend = false;

workbook.SaveAs("Pareto.xlsx");

workbook.Close();

{% endhighlight %}

{% highlight vb %}

Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2016

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

Dim sheet As IWorksheet = workbook.Worksheets(0)

'Create a chart

Dim chart As IChartShape = sheet.Charts.Add()

'Set chart type as Pareto

chart.ChartType = ExcelChartType.Pareto

'Set data range in the worksheet

chart.DataRange = sheet("A2:B8")

'Set category axis as bin option

chart.PrimaryCategoryAxis.IsBinningByCategory = True

'Formatting Pareto line

chart.Series(0).ParetoLineFormat.LineProperties.ColorIndex = ExcelKnownColors.Bright_green

'Gap width settings

chart.Series(0).SerieFormat.CommonSerieOptions.GapWidth = 6

'Set the chart title

chart.ChartTitle = "Expenses"

'Hiding the legend

chart.HasLegend = False

workbook.SaveAs("Pareto.xlsx")

workbook.Close()

excelEngine.Dispose()

{% endhighlight %}

{% endtabs %}

The input template can be downloaded [here](http://www.syncfusion.com/downloads/support/directtrac/general/ze/pareto1141391394.zip# ).

The following screen shot shows the output of above code.

![](Working-with-Charts_images/pareto.jpeg)



### Treemap

[Treemap](https://support.office.com/en-us/article/Create-a-treemap-chart-in-Office-2016-dfe86d28-a610-4ef5-9b30-362d5c624b68#) provides a hierarchical view of data as clustered rectangle with a specific weighted attribute determining the size of the rectangle. 

Following code example illustrates how to create Treemap chart.

{% tabs %}

{% highlight c# %}

ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2016;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

IWorksheet sheet = workbook.Worksheets[0];

//Create a chart

IChartShape chart = sheet.Charts.Add();

//Set chart type as TreeMap

chart.ChartType = ExcelChartType.TreeMap;

//Set data range in the worksheet

chart.DataRange = sheet["A2:C11"];

//Set the chart title

chart.ChartTitle = "Area by countries";

//Set the Treemap label option

chart.Series[0].SerieFormat.TreeMapLabelOption = ExcelTreeMapLabelOption.Banner; 

//Formatting data labels      

chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.Size = 8;

workbook.SaveAs("Treemap.xlsx");

workbook.Close();

excelEngine.Dispose();

{% endhighlight %}

{% highlight vb %}

Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2016

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

Dim sheet As IWorksheet= workbook.Worksheets(0)

'Create a chart

Dim chart As IChartShape = sheet.Charts.Add()

'Set chart type as TreeMap

chart.ChartType = ExcelChartType.TreeMap

'Set data range in the worksheet

chart.DataRange = sheet("A2:C11")

'Set the chart title

chart.ChartTitle = "Area by countries"

'Set the Treemap label option

chart.Series(0).SerieFormat.TreeMapLabelOption = ExcelTreeMapLabelOption.Banner 

'Formatting data labels        

chart.Series(0).DataPoints.DefaultDataPoint.DataLabels.Size = 8

workbook.SaveAs("Treemap.xlsx")

workbook.Close()

excelEngine.Dispose()

{% endhighlight %}

{% endtabs %}

The input template can be downloaded [here](http://www.syncfusion.com/downloads/support/directtrac/general/ze/treemap1366604090.zip#).

The following screen shot shows the output of above code.

![](Working-with-Charts_images/treemap.jpeg)



### Sunburst

[Sunburst](https://support.office.com/en-us/article/Create-a-sunburst-chart-in-Office-2016-4a127977-62cd-4c11-b8c7-65b84a358e0c#) provides a hierarchical view of data where each level of the hierarchy is represented by one ring or circle with the innermost circle as the top of the hierarchy.

Following code example illustrates how to create Sunburst chart.

{% tabs %}

{% highlight c# %}

ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2016;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

IWorksheet sheet = workbook.Worksheets[0];

//Create a chart

IChartShape chart = sheet.Charts.Add();

//Set chart type as Sunburst

chart.ChartType = ExcelChartType.SunBurst;

//Set data range in the worksheet

chart.DataRange = sheet["A1:D16"];

//Set the chart title

chart.ChartTitle = "Sales by annual";

//Formatting data labels      

chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.Size = 8;

//Hiding the legend

chart.HasLegend = false;

workbook.SaveAs("Sunburst.xlsx");

workbook.Close();

excelEngine.Dispose();

{% endhighlight %}

{% highlight vb %}

Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2016

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

Dim sheet As IWorksheet= workbook.Worksheets(0)

'Create a chart

Dim chart As IChartShape = sheet.Charts.Add()

'Set chart type as Sunburst

chart.ChartType = ExcelChartType.SunBurst

'Set data range in the worksheet

chart.DataRange = sheet("A1:D16")

'Set the chart title

chart.ChartTitle = "Sales by annual" 

'Formatting data labels       

chart.Series(0).DataPoints.DefaultDataPoint.DataLabels.Size = 8

'Hiding the legend

chart.HasLegend = False

workbook.SaveAs("Sunburst.xlsx")

workbook.Close()

excelEngine.Dispose()

{% endhighlight %}

{% endtabs %}

The input template can be downloaded [here](http://www.syncfusion.com/downloads/support/directtrac/general/ze/sunburst1589499118.zip#).

The following screen shot shows the output of above code.

![](Working-with-Charts_images/sunburst.jpeg)


N>These Charts are supported only in Excel 2016 and are not visible in the earlier versions.


## Supported Chart Types

The following chart types are supported in XlsIO.

* [Area](https://www.syncfusion.com/kb/8380)
* [Area_3D](https://www.syncfusion.com/kb/8356) 
* [Area_Stacked](https://www.syncfusion.com/kb/8360)
* [Area_Stacked_100](https://www.syncfusion.com/kb/8357)
* [Area_Stacked_100_3D](https://www.syncfusion.com/kb/8361)
* [Area_Stacked_3D](https://www.syncfusion.com/kb/8362) 
* [Bar_Clustered](https://www.syncfusion.com/kb/8335)
* [Bar_Clustered_3D](https://www.syncfusion.com/kb/8368)
* [Bar_Stacked](https://www.syncfusion.com/kb/8371)
* [Bar_Stacked_100](https://www.syncfusion.com/kb/8365)
* [Bar_Stacked_100_3D](https://www.syncfusion.com/kb/8374)
* [Bar_Stacked_3D](https://www.syncfusion.com/kb/8366)
* [Bubble](https://www.syncfusion.com/kb/8407)
* [Bubble_3D](https://www.syncfusion.com/kb/8403)
* [Column_3D](https://www.syncfusion.com/kb/8369)
* [Column_Clustered](https://www.syncfusion.com/kb/8280)
* [Column_Clustered_3D](https://www.syncfusion.com/kb/8402)  
* [Column_Stacked](https://www.syncfusion.com/kb/8344)
* [Column_Stacked_100](https://www.syncfusion.com/kb/8445)
* [Column_Stacked_100_3D](https://www.syncfusion.com/kb/8375)
* [Column_Stacked_3D](https://www.syncfusion.com/kb/8373)
* [Combination_Chart](https://www.syncfusion.com/kb/8411)       
* [Cone_Bar_Clustered](https://www.syncfusion.com/kb/8558)
* [Cone_Bar_Stacked](https://www.syncfusion.com/kb/8528)
* [Cone_Bar_Stacked_100](https://www.syncfusion.com/kb/8524)
* [Cone_Clustered](https://www.syncfusion.com/kb/8541)
* [Cone_Clustered_3D](https://www.syncfusion.com/kb/8520)
* [Cone_Stacked](https://www.syncfusion.com/kb/8530)
* [Cone_Stacked_100](https://www.syncfusion.com/kb/8533)
* [Cylinder_Bar_Clustered](https://www.syncfusion.com/kb/8529)
* [Cylinder_Bar_Stacked](https://www.syncfusion.com/kb/8531)
* [Cylinder_Bar_Stacked_100](https://www.syncfusion.com/kb/8540)
* [Cylinder_Clustered](https://www.syncfusion.com/kb/8526)
* [Cylinder_Clustered_3D](https://www.syncfusion.com/kb/8545)
* [Cylinder_Stacked](https://www.syncfusion.com/kb/8519)
* [Cylinder_Stacked_100](https://www.syncfusion.com/kb/8543)
* [Doughnut](https://www.syncfusion.com/kb/8398)
* [Doughnut_Exploded](https://www.syncfusion.com/kb/8518)
* [Line](https://www.syncfusion.com/kb/8358)
* [Line_3D](https://www.syncfusion.com/kb/8416)
* [Line_Markers](https://www.syncfusion.com/kb/8359) 
* [Line_Markers_Stacked](https://www.syncfusion.com/kb/8379)
* [Line_Markers_Stacked_100](https://www.syncfusion.com/kb/8376)
* [Line_Stacked](https://www.syncfusion.com/kb/8372)
* [Line_Stacked_100](https://www.syncfusion.com/kb/8370)
* [Pie](https://www.syncfusion.com/kb/8423)
* [Pie_3D](https://www.syncfusion.com/kb/8426)
* [Pie_Bar](https://www.syncfusion.com/kb/8404)
* [Pie_Exploded](https://www.syncfusion.com/kb/8539)
* [Pie_Exploded_3D](https://www.syncfusion.com/kb/8559)
* [PieOfPie](https://www.syncfusion.com/kb/8406)
* [Pyramid_Bar_Clustered](https://www.syncfusion.com/kb/8521)
* [Pyramid_Bar_Stacked](https://www.syncfusion.com/kb/8547)
* [Pyramid_Bar_Stacked_100](https://www.syncfusion.com/kb/8544)
* [Pyramid_Clustered](https://www.syncfusion.com/kb/8525)
* [Pyramid_Clustered_3D](https://www.syncfusion.com/kb/8527)
* [Pyramid_Stacked](https://www.syncfusion.com/kb/8536)
* [Pyramid_Stacked_100](https://www.syncfusion.com/kb/8534)
* [Radar](https://www.syncfusion.com/kb/8408)
* [Radar_Filled](https://www.syncfusion.com/kb/8414)
* [Radar_Markers](https://www.syncfusion.com/kb/8409)
* [Scatter_Line](https://www.syncfusion.com/kb/8405)
* [Scatter_Line_Markers](https://www.syncfusion.com/kb/8400)
* [Scatter_Markers](https://www.syncfusion.com/kb/8418)
* [Scatter_SmoothedLine](https://www.syncfusion.com/kb/8401)
* [Scatter_SmoothedLine_Markers](https://www.syncfusion.com/kb/8415)
* [Stock_HighLowClose](https://www.syncfusion.com/kb/8397)
* [Stock_OpenHighLowClose](https://www.syncfusion.com/kb/8417)
* [Stock_VolumeHighLowClose](https://www.syncfusion.com/kb/8424)
* [Stock_VolumeOpenHighLowClose](https://www.syncfusion.com/kb/8425)  
* [Surface_3D](https://www.syncfusion.com/kb/8419)
* [Surface_Contour](https://www.syncfusion.com/kb/8410)
* [Surface_NoColor_3D](https://www.syncfusion.com/kb/8421)
* [Surface_NoColor_Contour](https://www.syncfusion.com/kb/8413)
* [Funnel](https://www.syncfusion.com/kb/8422)
* [Box and Whisker](https://www.syncfusion.com/kb/8428)
* [Waterfall](https://www.syncfusion.com/kb/8420)
* [Histogram](https://www.syncfusion.com/kb/8431)
* [Pareto](https://www.syncfusion.com/kb/8430)
* [Treemap](https://www.syncfusion.com/kb/8427)
* [Sunburst](https://www.syncfusion.com/kb/8429)
