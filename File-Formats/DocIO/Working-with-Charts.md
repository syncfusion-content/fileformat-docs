---
title: Working with Charts in Word document | DocIO | Syncfusion
description: Learn how to add, edit, and remove charts in a Word document using the .NET Word (DocIO) library without Microsoft Word or interop dependencies.
platform: file-formats
control: DocIO
documentation: UG
---
# Working with Charts in Word document

A Chart is a graphical representation of data where the data is represented as symbols such as bars, lines etc. Charts can represent numerical data, functions or some kinds of qualitative structures. DocIO supports the following chart types:

* Bar chart
* Line chart
* Pie chart
* Area chart
* Column chart
* Scatter chart
* Surface chart
* Stock chart
* Radar chart

N> DocIO supports chart only in DOCX and WordML format documents.

## Creating a simple Chart from scratch

A new chart can be created or an existing chart can be modified by using the [WChart](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WChart.html) instance. The following code example illustrates how to create a new chart.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Creates a new instance of WordDocument (Empty Word Document)
using (WordDocument document = new WordDocument())
{
    //Adds section to the document
    IWSection sec = document.AddSection();
    //Adds paragraph to the section
    IWParagraph paragraph = sec.AddParagraph();
    //Creates and Appends chart to the paragraph
    WChart chart = paragraph.AppendChart(446, 270);
    //Sets chart type
    chart.ChartType = OfficeChartType.Pie;
    //Sets chart title
    chart.ChartTitle = "Best Selling Products";
    chart.ChartTitleArea.FontName = "Calibri";
    chart.ChartTitleArea.Size = 14;
    //Sets data for chart
    chart.ChartData.SetValue(1, 1, "");
    chart.ChartData.SetValue(1, 2, "Sales");
    chart.ChartData.SetValue(2, 1, "Phyllis Lapin");
    chart.ChartData.SetValue(2, 2, 141.396);
    chart.ChartData.SetValue(3, 1, "Stanley Hudson");
    chart.ChartData.SetValue(3, 2, 80.368);
    chart.ChartData.SetValue(4, 1, "Bernard Shah");
    chart.ChartData.SetValue(4, 2, 71.155);
    chart.ChartData.SetValue(5, 1, "Patricia Lincoln");
    chart.ChartData.SetValue(5, 2, 47.234);
    chart.ChartData.SetValue(6, 1, "Camembert Pierrot");
    chart.ChartData.SetValue(6, 2, 46.825);
    chart.ChartData.SetValue(7, 1, "Thomas Hardy");
    chart.ChartData.SetValue(7, 2, 42.593);
    chart.ChartData.SetValue(8, 1, "Hanna Moos");
    chart.ChartData.SetValue(8, 2, 41.819);
    chart.ChartData.SetValue(9, 1, "Alice Mutton");
    chart.ChartData.SetValue(9, 2, 32.698);
    chart.ChartData.SetValue(10, 1, "Christina Berglund");
    chart.ChartData.SetValue(10, 2, 29.171);
    chart.ChartData.SetValue(11, 1, "Elizabeth Lincoln");
    chart.ChartData.SetValue(11, 2, 25.696);
    //Creates a new chart series with the name “Sales”
    IOfficeChartSerie pieSeries = chart.Series.Add("Sales");
    pieSeries.Values = chart.ChartData[2, 2, 11, 2];
    //Sets data label
    pieSeries.DataPoints.DefaultDataPoint.DataLabels.IsValue = true;
    pieSeries.DataPoints.DefaultDataPoint.DataLabels.Position = OfficeDataLabelPosition.Outside;
    //Sets background color
    chart.ChartArea.Fill.ForeColor = Syncfusion.Drawing.Color.FromArgb(242, 242, 242);
    chart.PlotArea.Fill.ForeColor = Syncfusion.Drawing.Color.FromArgb(242, 242, 242);
    chart.ChartArea.Border.LinePattern = OfficeChartLinePattern.None;
    //Sets category labels
    chart.PrimaryCategoryAxis.CategoryLabels = chart.ChartData[2, 1, 11, 1];
    //Saves the Word document to MemoryStream
    MemoryStream stream = new MemoryStream();
    document.Save(stream, FormatType.Docx);
    document.Close();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Creates a new Word document
WordDocument document = new WordDocument();
//Adds section to the document
IWSection sec = document.AddSection();
//Adds paragraph to the section
IWParagraph paragraph = sec.AddParagraph();
//Creates and Appends chart to the paragraph
WChart chart = paragraph.AppendChart(446, 270);
//Sets chart type
chart.ChartType = OfficeChartType.Pie;
//Sets chart title
chart.ChartTitle = "Best Selling Products";
chart.ChartTitleArea.FontName = "Calibri";
chart.ChartTitleArea.Size = 14;
//Sets data for chart
chart.ChartData.SetValue(1, 1, "");
chart.ChartData.SetValue(1, 2, "Sales");
chart.ChartData.SetValue(2, 1, "Phyllis Lapin");
chart.ChartData.SetValue(2, 2, 141.396);
chart.ChartData.SetValue(3, 1, "Stanley Hudson");
chart.ChartData.SetValue(3, 2, 80.368);
chart.ChartData.SetValue(4, 1, "Bernard Shah");
chart.ChartData.SetValue(4, 2, 71.155);
chart.ChartData.SetValue(5, 1, "Patricia Lincoln");
chart.ChartData.SetValue(5, 2, 47.234);
chart.ChartData.SetValue(6, 1, "Camembert Pierrot");
chart.ChartData.SetValue(6, 2, 46.825);
chart.ChartData.SetValue(7, 1, "Thomas Hardy");
chart.ChartData.SetValue(7, 2, 42.593);
chart.ChartData.SetValue(8, 1, "Hanna Moos");
chart.ChartData.SetValue(8, 2, 41.819);
chart.ChartData.SetValue(9, 1, "Alice Mutton");
chart.ChartData.SetValue(9, 2, 32.698);
chart.ChartData.SetValue(10, 1, "Christina Berglund");
chart.ChartData.SetValue(10, 2, 29.171);
chart.ChartData.SetValue(11, 1, "Elizabeth Lincoln");
chart.ChartData.SetValue(11, 2, 25.696);
//Creates a new chart series with the name “Sales”
IOfficeChartSerie pieSeries = chart.Series.Add("Sales");
pieSeries.Values = chart.ChartData[2, 2, 11, 2];
//Sets data label
pieSeries.DataPoints.DefaultDataPoint.DataLabels.IsValue = true;
pieSeries.DataPoints.DefaultDataPoint.DataLabels.Position = OfficeDataLabelPosition.Outside;
//Sets background color
chart.ChartArea.Fill.ForeColor = Color.FromArgb(242, 242, 242);
chart.PlotArea.Fill.ForeColor = Color.FromArgb(242, 242, 242);
chart.ChartArea.Border.LinePattern = OfficeChartLinePattern.None;
//Sets category labels
chart.PrimaryCategoryAxis.CategoryLabels = chart.ChartData[2, 1, 11, 1];            
//Saves the document
document.Save("Sample.docx", FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Creates a new Word document
Dim document As New WordDocument()
'Adds section to the document
Dim sec As IWSection = document.AddSection()
'Adds paragraph to the section
Dim paragraph As IWParagraph = sec.AddParagraph()
'Creates and Appends chart to the paragraph
Dim chart As WChart = paragraph.AppendChart(446, 270)
'Sets chart type
chart.ChartType = OfficeChartType.Pie
'Sets chart title
chart.ChartTitle = "Best Selling Products"
chart.ChartTitleArea.FontName = "Calibri"
chart.ChartTitleArea.Size = 14
'Sets data for chart
chart.ChartData.SetValue(1, 1, "")
chart.ChartData.SetValue(1, 2, "Sales")
chart.ChartData.SetValue(2, 1, "Phyllis Lapin")
chart.ChartData.SetValue(2, 2, 141.396)
chart.ChartData.SetValue(3, 1, "Stanley Hudson")
chart.ChartData.SetValue(3, 2, 80.368)
chart.ChartData.SetValue(4, 1, "Bernard Shah")
chart.ChartData.SetValue(4, 2, 71.155)
chart.ChartData.SetValue(5, 1, "Patricia Lincoln")
chart.ChartData.SetValue(5, 2, 47.234)
chart.ChartData.SetValue(6, 1, "Camembert Pierrot")
chart.ChartData.SetValue(6, 2, 46.825)
chart.ChartData.SetValue(7, 1, "Thomas Hardy")
chart.ChartData.SetValue(7, 2, 42.593)
chart.ChartData.SetValue(8, 1, "Hanna Moos")
chart.ChartData.SetValue(8, 2, 41.819)
chart.ChartData.SetValue(9, 1, "Alice Mutton")
chart.ChartData.SetValue(9, 2, 32.698)
chart.ChartData.SetValue(10, 1, "Christina Berglund")
chart.ChartData.SetValue(10, 2, 29.171)
chart.ChartData.SetValue(11, 1, "Elizabeth Lincoln")
chart.ChartData.SetValue(11, 2, 25.696)
'Creates a new chart series with the name “Sales”
Dim pieSeries As IOfficeChartSerie = chart.Series.Add("Sales")
pieSeries.Values = chart.ChartData(2, 2, 11, 2)
'Sets data label
pieSeries.DataPoints.DefaultDataPoint.DataLabels.IsValue = True
pieSeries.DataPoints.DefaultDataPoint.DataLabels.Position = OfficeDataLabelPosition.Outside
'Sets background color
chart.ChartArea.Fill.ForeColor = Color.FromArgb(242, 242, 242)
chart.PlotArea.Fill.ForeColor = Color.FromArgb(242, 242, 242)
chart.ChartArea.Border.LinePattern = OfficeChartLinePattern.None
'Sets category labels
chart.PrimaryCategoryAxis.CategoryLabels = chart.ChartData(2, 1, 11, 1)
'Saves the document
document.Save("Sample.docx", FormatType.Docx)
'Closes the document
document.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Charts/Create-chart-from-scratch).

## Creating a Chart from Excel file

The chart data can be set through the object array or can be loaded from the excel stream. The specific range of the data from the excel file can be used to set chart data. 

The following code example illustrates the chart data loaded from the excel file.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Creates a new instance of WordDocument (Empty Word Document)
using (WordDocument document = new WordDocument())
{
    //Adds section to the document
    IWSection sec = document.AddSection();
    //Adds paragraph to the section
    IWParagraph paragraph = sec.AddParagraph();
    //Loads the excel file as stream
    Stream excelStream = File.OpenRead("Excel_Template.xlsx");
    //Creates and Appends chart to the paragraph with excel stream as parameter
    WChart chart = paragraph.AppendChart(excelStream, 1, "B2:C6", 470, 300);
    //Sets chart type and title
    chart.ChartType = OfficeChartType.Column_Clustered;
    chart.ChartTitle = "Purchase Details";
    chart.ChartTitleArea.FontName = "Calibri";
    chart.ChartTitleArea.Size = 14;
    chart.ChartArea.Border.LinePattern = OfficeChartLinePattern.None;
    //Sets name to chart series
    chart.Series[0].Name = "Sum of Purchases";
    chart.Series[1].Name = "Sum of Future Expenses";
    chart.PrimaryCategoryAxis.Title = "Products";
    chart.PrimaryValueAxis.Title = "In Dollars";
    //Sets position of legend
    chart.Legend.Position = OfficeLegendPosition.Bottom;
    //Saves the Word document to  MemoryStream
    MemoryStream stream = new MemoryStream();
    document.Save(stream, FormatType.Docx);
    document.Close();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Creates a new Word document
WordDocument document = new WordDocument();
//Adds section to the document
IWSection sec = document.AddSection();
//Adds paragraph to the section
IWParagraph paragraph = sec.AddParagraph();
//Loads the excel file as stream
Stream excelStream = File.OpenRead("Excel_Template.xlsx");
//Creates and Appends chart to the paragraph with excel stream as parameter
WChart chart = paragraph.AppendChart(excelStream, 1, "B2:C6", 470, 300);
//Sets chart type and title
chart.ChartType = OfficeChartType.Column_Clustered;
chart.ChartTitle = "Purchase Details";
chart.ChartTitleArea.FontName = "Calibri";
chart.ChartTitleArea.Size = 14;
chart.ChartArea.Border.LinePattern = OfficeChartLinePattern.None;       
//Sets name to chart series
chart.Series[0].Name = "Sum of Purchases";
chart.Series[1].Name = "Sum of Future Expenses";
chart.PrimaryCategoryAxis.Title = "Products";
chart.PrimaryValueAxis.Title = "In Dollars";
//Sets position of legend
chart.Legend.Position = OfficeLegendPosition.Bottom;
//Saves the document
document.Save("Sample.docx", FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Creates a new Word document
Dim document As New WordDocument()
'Adds section to the document
Dim sec As IWSection = document.AddSection()
'Adds paragraph to the section
Dim paragraph As IWParagraph = sec.AddParagraph()
'Loads the excel file as stream
Dim excelStream As Stream = File.OpenRead("Excel_Template.xlsx")
'Creates and Appends chart to the paragraph with excel stream as parameter
Dim chart As WChart = paragraph.AppendChart(excelStream, 1, "B2:C6", 470, 300)
'Sets chart type and title
chart.ChartType = OfficeChartType.Column_Clustered
chart.ChartTitle = "Purchase Details"
chart.ChartTitleArea.FontName = "Calibri"
chart.ChartTitleArea.Size = 14
chart.ChartArea.Border.LinePattern = OfficeChartLinePattern.None
'Sets name to chart series
chart.Series(0).Name = "Sum of Purchases"
chart.Series(1).Name = "Sum of Future Expenses"
chart.PrimaryCategoryAxis.Title = "Products"
chart.PrimaryValueAxis.Title = "In Dollars"
'Sets position of legend
chart.Legend.Position = OfficeLegendPosition.Bottom
'Saves the document
document.Save("Sample.docx", FormatType.Docx)
'Closes the document
document.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Charts/Create-chart-from-Excel-file).

## Creating Custom Charts

A chart is composed of data series. Each data series is represented by a series object. When creating a custom chart, you can specify different series types for each data series. 

The following code example illustrates how to create custom charts.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Creates a new instance of WordDocument (Empty Word Document)
using (WordDocument document = new WordDocument())
{
    //Adds section to the document
    IWSection sec = document.AddSection();
    //Adds paragraph to the section
    IWParagraph paragraph = sec.AddParagraph();
    //Inputs data for chart
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
    //Creates and Appends chart to the paragraph
    WChart chart = paragraph.AppendChart(data, 470, 300);
    //Sets chart type and title
    chart.ChartTitle = "Purchase Details";
    chart.ChartTitleArea.FontName = "Calibri";
    chart.ChartTitleArea.Size = 14;
    chart.ChartArea.Border.LinePattern = OfficeChartLinePattern.None;
    //Sets series type 
    chart.Series[0].SerieType = OfficeChartType.Line_Markers;
    chart.Series[1].SerieType = OfficeChartType.Bar_Clustered;
    chart.PrimaryCategoryAxis.Title = "Products";
    chart.PrimaryValueAxis.Title = "In Dollars";
    //Sets position of legend
    chart.Legend.Position = OfficeLegendPosition.Bottom;
    //Saves the Word document to  MemoryStream
    MemoryStream stream = new MemoryStream();
    document.Save(stream, FormatType.Docx);
    document.Close();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Creates a new Word document
WordDocument document = new WordDocument();
//Adds section to the document
IWSection sec = document.AddSection();
//Adds paragraph to the section
IWParagraph paragraph = sec.AddParagraph();
//Inputs data for chart
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
//Creates and Appends chart to the paragraph
WChart chart = paragraph.AppendChart(data, 470, 300);
//Sets chart type and title
chart.ChartTitle = "Purchase Details";
chart.ChartTitleArea.FontName = "Calibri";
chart.ChartTitleArea.Size = 14;
chart.ChartArea.Border.LinePattern = OfficeChartLinePattern.None;
//Sets series type 
chart.Series[0].SerieType = OfficeChartType.Line_Markers;
chart.Series[1].SerieType = OfficeChartType.Bar_Clustered;
chart.PrimaryCategoryAxis.Title = "Products";
chart.PrimaryValueAxis.Title = "In Dollars";
//Sets position of legend
chart.Legend.Position = OfficeLegendPosition.Bottom;
//Saves the document
document.Save("Sample.docx", FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Creates a new Word document
Dim document As New WordDocument()
'Adds section to the document
Dim sec As IWSection = document.AddSection()
'Adds paragraph to the section
Dim paragraph As IWParagraph = sec.AddParagraph()
'Inputs data for chart
Dim data As Object()() = New Object(5)() {}
For i As Integer = 0 To 5
    data(i) = New Object(2) {}
Next
data(0)(0) = ""
data(1)(0) = "Camembert Pierrot"
data(2)(0) = "Alice Mutton"
data(3)(0) = "Roasted Tigers"
data(4)(0) = "Orange Shake"
data(5)(0) = "Dried Apples"
data(0)(1) = "Sum of Purchases"
data(1)(1) = 286
data(2)(1) = 680
data(3)(1) = 288
data(4)(1) = 200
data(5)(1) = 731
data(0)(2) = "Sum of Future Expenses"
data(1)(2) = 1300
data(2)(2) = 700
data(3)(2) = 1280
data(4)(2) = 1200
data(5)(2) = 2660
'Creates and Appends chart to the paragraph
Dim chart As WChart = paragraph.AppendChart(data, 470, 300)
'Sets chart type and title
chart.ChartTitle = "Purchase Details"
chart.ChartTitleArea.FontName = "Calibri"
chart.ChartTitleArea.Size = 14
chart.ChartArea.Border.LinePattern = OfficeChartLinePattern.None
'Sets series type 
chart.Series(0).SerieType = OfficeChartType.Line_Markers
chart.Series(1).SerieType = OfficeChartType.Bar_Clustered
chart.PrimaryCategoryAxis.Title = "Products"
chart.PrimaryValueAxis.Title = "In Dollars"
'Sets position of legend
chart.Legend.Position = OfficeLegendPosition.Bottom
'Saves the document
document.Save("Sample.docx", FormatType.Docx)
'Closes the document
document.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Charts/Create-custom-chart).

## Creating a Chart from Database

Generate a chart within a Word document sourced from a database by retrieving the required chart data values and subsequently assigning them to the chart's dataset.

The following code example illustrates how to create a chart in a Word document from database.

{% tabs %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

//Create a new instance of WordDocument.
using (WordDocument document = new WordDocument())
{
    document.EnsureMinimal();
    //Get the data table
    DataTable dataTable = GetDataTable();
    //Create and append the chart to the paragraph.
    WChart chart = document.LastParagraph.AppendChart(446, 270);
    chart.ChartType = OfficeChartType.Pie;
    //Assign the data.
    AddChartData(chart, dataTable);
    //Set a chart title.
    chart.ChartTitle = "Best Selling Products";
    IOfficeChartSerie pieSeries = chart.Series.Add("Sales");
    pieSeries.Values = chart.ChartData[2, 2, 11, 2];
    //Set the data label.
    pieSeries.DataPoints.DefaultDataPoint.DataLabels.IsValue = true;
    pieSeries.DataPoints.DefaultDataPoint.DataLabels.Position = OfficeDataLabelPosition.Outside;
    //Set the category labels.
    chart.PrimaryCategoryAxis.CategoryLabels = chart.ChartData[2, 1, 11, 1];
    //Set the legend.
    chart.HasLegend = true;
    //Save the Word document.
    document.Save(Path.GetFullPath(@"../../Result.docx"));
}

// Get the data to create  pie chart.
private static DataTable GetDataTable()
{
    string path = Path.GetFullPath(@"../../Data/DataBase.mdb");
    //Create a new instance of OleDbConnection
    OleDbConnection connection = new OleDbConnection();
    //Set the string to open a Database
    connection.ConnectionString = "Provider=Microsoft.JET.OLEDB.4.0;Password=\"\";User ID=Admin;Data Source=" + path;
    //Open the Database connection
    connection.Open();
    //Get all the data from the Database
    OleDbCommand query = new OleDbCommand("select * from Products", connection);
    //Create a new instance of OleDbDataAdapter
    OleDbDataAdapter adapter = new OleDbDataAdapter(query);
    //Create a new instance of DataSet
    DataSet dataSet = new DataSet();
    //Add rows in the Dataset
    adapter.Fill(dataSet);
    //Create a DataTable from the Dataset
    DataTable table = dataSet.Tables[0];
    table.TableName = "Products";
    return table;
}

// Set the value for the chart.
 private static void AddChartData(WChart chart, DataTable dataTable)
 {
     //Set the value for chart data.
     chart.ChartData.SetValue(1, 1, "Names");
     chart.ChartData.SetValue(1, 2, "Product");

     int rowIndex = 2;
     int colIndex = 1;
     //Get the value from the DataTable and set the value for chart data
     foreach (DataRow row in dataTable.Rows)
     {
         foreach (object val in row.ItemArray)
         {
             string value = val.ToString();
             chart.ChartData.SetValue(rowIndex, colIndex, value);
             colIndex++;
             if (colIndex == 3)
                 break;
         }
         colIndex = 1;
         rowIndex++;
     }
 }

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Create a new instance of WordDocument.
Using document As New WordDocument()
    document.EnsureMinimal()
    ' Get the data table
    Dim dataTable As DataTable = GetDataTable()
    ' Create and append the chart to the paragraph.
    Dim chart As WChart = document.LastParagraph.AppendChart(446, 270)
    chart.ChartType = OfficeChartType.Pie
    ' Assign the data.
    AddChartData(chart, dataTable)
    ' Set a chart title.
    chart.ChartTitle = "Best Selling Products"
    Dim pieSeries As IOfficeChartSerie = chart.Series.Add("Sales")
    pieSeries.Values = chart.ChartData(2, 2, 11, 2)
    ' Set the data label.
    pieSeries.DataPoints.DefaultDataPoint.DataLabels.IsValue = True
    pieSeries.DataPoints.DefaultDataPoint.DataLabels.Position = OfficeDataLabelPosition.Outside
    ' Set the category labels.
    chart.PrimaryCategoryAxis.CategoryLabels = chart.ChartData(2, 1, 11, 1)
    ' Set the legend.
    chart.HasLegend = True
    ' Save the Word document.
    document.Save(Path.GetFullPath("..\..\Result.docx"))
End Using

' Get the data to create a pie chart.
Private Function GetDataTable() As DataTable

    Dim path As String = System.IO.Path.GetFullPath("..\..\Data\DataBase.mdb")
    ' Create a new instance of OleDbConnection
    Dim connection As New OleDbConnection()
    ' Set the string to open a Database
    connection.ConnectionString = "Provider=Microsoft.JET.OLEDB.4.0;Password="""";User ID=Admin;Data Source=" & path
    ' Open the Database connection
    connection.Open()
    ' Get all the data from the Database
    Dim query As New OleDbCommand("select * from Products", connection)
    ' Create a new instance of OleDbDataAdapter
    Dim adapter As New OleDbDataAdapter(query)
    ' Create a new instance of DataSet
    Dim dataSet As New DataSet()
    ' Add rows in the Dataset
    adapter.Fill(dataSet)
    ' Create a DataTable from the Dataset
    Dim table As DataTable = dataSet.Tables(0)
    table.TableName = "Products"
    Return table
End Function

' Set the value for the chart.
Private Sub AddChartData(ByVal chart As WChart, ByVal dataTable As DataTable)
    ' Set the value for chart data.
    chart.ChartData.SetValue(1, 1, "Names")
    chart.ChartData.SetValue(1, 2, "Product")

    Dim rowIndex As Integer = 2
    Dim colIndex As Integer = 1
    ' Get the value from the DataTable and set the value for chart data
    For Each row As DataRow In dataTable.Rows
        For Each val As Object In row.ItemArray
            Dim value As String = val.ToString()
            chart.ChartData.SetValue(rowIndex, colIndex, value)
            colIndex += 1
            If colIndex = 3 Then
                Exit For
            End If
        Next
        colIndex = 1
        rowIndex += 1
    Next
End Sub

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from GitHub.

## Refreshing the Chart

The chart may not have the data in the referred excel file instead it may represent some other data. For those charts to have the excel data, it should be refreshed. 

The following code example illustrates how to refresh the chart.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
FileStream fileStreamPath = new FileStream(@"Data/Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx))
{
    //Gets the last paragraph
    WParagraph paragraph = document.LastParagraph;
    //Gets the chart entity from the paragraph items
    WChart chart = paragraph.ChildEntities[1] as WChart;
    // Refreshes the chart data. Set true to evaluate Excel formulas before refreshing,
    // or false to refresh only the data without evaluating formulas.
    chart.Refresh(false);
    MemoryStream stream = new MemoryStream();
    document.Save(stream, FormatType.docx);
    //Closes the Word document
    document.Close();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Loads the template document
WordDocument document = new WordDocument("Template.docx");
//Gets the last paragraph
WParagraph paragraph = document.LastParagraph;
//Gets the chart entity from the paragraph items
WChart chart = paragraph.ChildEntities[1] as WChart;
// Refreshes the chart data. Set true to evaluate Excel formulas before refreshing,
// or false to refresh only the data without evaluating formulas.
chart.Refresh(false);
//Saves and closes the document
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Loads the template document
Dim document As New WordDocument("Template.docx")
'Gets the last paragraph
Dim paragraph As WParagraph = document.LastParagraph
'Gets the chart entity from the paragraph items
Dim chart As WChart = TryCast(paragraph.ChildEntities(1), WChart)
'Refreshes the chart data. Set true to evaluate Excel formulas before refreshing,
'or false to refresh only the data without evaluating formulas.
chart.Refresh(false)
'Saves and closes the document
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Charts/Refresh-chart-data).

## Modifying the Chart data

The following code example illustrates how to modify an existing chart data.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
FileStream fileStreamPath = new FileStream("Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx))
{
    //Gets the last paragraph
    WParagraph paragraph = document.LastParagraph;
    //Gets the chart entity from the paragraph items
    WChart chart = paragraph.ChildEntities[0] as WChart;
    //Modifies the data values of chart
    chart.ChartData.SetValue(2, 2, 120);
    chart.ChartData.SetValue(3, 2, 60);
    chart.ChartData.SetValue(4, 2, 70);
    //Refreshes chart data to set the modified values
    chart.Refresh();
    MemoryStream stream = new MemoryStream();
    document.Save(stream, FormatType.docx);
    //Closes the Word document
    document.Close();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Loads the template document
WordDocument document = new WordDocument("Template.docx");
//Gets the last paragraph
WParagraph paragraph = document.LastParagraph;
//Gets the chart entity from the paragraph items
WChart chart = paragraph.ChildEntities[0] as WChart;
//Modifies the data values of chart
chart.ChartData.SetValue(2, 2, 120);
chart.ChartData.SetValue(3, 2, 60);
chart.ChartData.SetValue(4, 2, 70);
//Refreshes chart data to set the modified values
chart.Refresh();
//Saves and closes the document
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Loads the template document
Dim document As New WordDocument("Template.docx")
'Gets the last paragraph
Dim paragraph As WParagraph = document.LastParagraph
'Gets the chart entity from the paragraph items
Dim chart As WChart = TryCast(paragraph.ChildEntities(0), WChart)
'Modifies the data values of chart
chart.ChartData.SetValue(2, 2, 120)
chart.ChartData.SetValue(3, 2, 60)
chart.ChartData.SetValue(4, 2, 70)
'Refreshes chart data to set the modified values
chart.Refresh()
'Saves and closes the document
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Charts/Modify-an-existing-chart-data).

## Customizing the Chart & its elements

A Chart is composed of various elements such as plot area, chart area, title area, legend, data labels, axis etc. The following screenshot illustrates the various elements of chart.

![Illustrates the various elements of chart](workingwithchartsimages/Chart-Basic-Elements.jpeg)

1. The chart area of the chart.
2. The plot area of the chart.
3. The data points of the data series that are plotted in the chart.
4. The horizontal (category) and vertical (value) axis along where the data is plotted in the chart.
5. The legend of the chart.
6. The chart title and axis.
7. A data label that you can use to identify the details of a data point in a data series.

### Chart Title
Customize the **chart title** by modifying its name, appearance, and resizing it using the **Word (DocIO) library**. For further information, click [here](https://help.syncfusion.com/file-formats/docio/charts/chart-title).

### Chart Area
Customize the **chart area** by changing its border, colors, transparency, and more using the **Word (DocIO) library**. For further information, click [here](https://help.syncfusion.com/file-formats/docio/charts/chart-area).

### Chart Plot Area
Customize the **chart plot area** by changing its border, colors, transparency, position and adding image using the **Word (DocIO) library**. For further information, click [here](https://help.syncfusion.com/file-formats/docio/charts/chart-plot-area).

### Chart Series
 Customize the **chart series** by changing the series name, type, color, border, and more using the **Word (DocIO) library**. For further information, click [here](https://help.syncfusion.com/file-formats/docio/charts/chart-series).

### Chart Legend
Customize the **chart legend** by changing the position, border, and modifying the legend entry using the **Word (DocIO) library**. For further information, click [here](https://help.syncfusion.com/file-formats/docio/charts/chart-legend).

### Chart Data Labels
Customize the **chart data labels** by changing the position, size and more using the **Word (DocIO) library**. For further information, click [here](https://help.syncfusion.com/file-formats/docio/charts/chart-data-lables).

### Chart Axis
Customize the **chart axes** by changing the title, border, font, rotation angle and more using the **Word (DocIO) library**. For further information, click [here](https://help.syncfusion.com/file-formats/docio/charts/chart-axis).

## Applying 3D Formats

Essential DocIO allows to modify the side wall, back wall, floor of the 3D chart. The following code snippet illustrates how to apply properties for side wall, floor and back wall of a 3D chart.

{% tabs %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Creates a new Word document
WordDocument document = new WordDocument();
//Adds section to the document
IWSection sec = document.AddSection();
//Adds paragraph to the section
IWParagraph paragraph = sec.AddParagraph();
//Loads the excel file as stream
Stream excelStream = File.OpenRead("Excel_Template.xlsx");
//Creates and Appends chart to the paragraph with excel stream as parameter
WChart chart = paragraph.AppendChart(excelStream, 1, "B2:C6", 470, 300);
//Sets chart type and title
chart.ChartType = OfficeChartType.Column_Clustered_3D;
chart.ChartTitle = "Purchase Details";
chart.ChartTitleArea.FontName = "Calibri";
chart.ChartTitleArea.Size = 14;
chart.ChartArea.Border.LinePattern = OfficeChartLinePattern.None;          
//Sets name to chart series            
chart.Series[0].Name = "Sum of Purchases";
chart.Series[1].Name = "Sum of Future Expenses";
chart.PrimaryCategoryAxis.Title = "Products";
chart.PrimaryValueAxis.Title = "In Dollars";
//Sets position of legend
chart.Legend.Position = OfficeLegendPosition.Bottom;
//Sets rotation and elevation values
chart.Rotation = 20;
chart.Elevation = 15;
//Sets side wall properties
chart.SideWall.Fill.FillType = OfficeFillType.SolidColor;
chart.SideWall.Fill.ForeColor = Color.White;
chart.SideWall.Fill.BackColor = Color.White;
chart.SideWall.Border.LineColor = System.Drawing.Color.Beige;
//Sets floor fill option.
chart.Floor.Fill.FillType = OfficeFillType.Pattern;
//Sets the floor pattern Type.
chart.Floor.Fill.Pattern = OfficeGradientPattern.Pat_Divot;
//Sets the floor fore and Back ground color.
chart.Floor.Fill.ForeColor = System.Drawing.Color.Blue;
chart.Floor.Fill.BackColor = System.Drawing.Color.White;
//Sets the floor thickness.
chart.Floor.Thickness = 3;
//Sets the back wall fill option.
chart.BackWall.Fill.FillType = OfficeFillType.Gradient;
//Sets the Texture Type.
chart.BackWall.Fill.GradientColorType = OfficeGradientColor.TwoColor;
chart.BackWall.Fill.GradientStyle = OfficeGradientStyle.Diagonl_Down;
chart.BackWall.Fill.ForeColor = Color.WhiteSmoke;
chart.BackWall.Fill.BackColor = Color.LightBlue;
//Sets the Border Line color.
chart.BackWall.Border.LineColor = System.Drawing.Color.Wheat;
//Sets the Picture Type.
chart.BackWall.PictureUnit = OfficeChartPictureType.stretch;
//Sets the back wall thickness.
chart.BackWall.Thickness = 10;
//Saves and closes the document
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Creates a new Word document
Dim document As New WordDocument()
'Adds section to the document
Dim sec As IWSection = document.AddSection()
'Adds paragraph to the section
Dim paragraph As IWParagraph = sec.AddParagraph()
'Loads the excel file as stream
Dim excelStream As Stream = File.OpenRead("Excel_Template.xlsx")
'Creates and Appends chart to the paragraph with excel stream as parameter
Dim chart As WChart = paragraph.AppendChart(excelStream, 1, "B2:C6", 470, 300)
'Sets chart type and title
chart.ChartType = OfficeChartType.Column_Clustered_3D
chart.ChartTitle = "Purchase Details"
chart.ChartTitleArea.FontName = "Calibri"
chart.ChartTitleArea.Size = 14
chart.ChartArea.Border.LinePattern = OfficeChartLinePattern.None
'Sets name to chart series            
chart.Series(0).Name = "Sum of Purchases"
chart.Series(1).Name = "Sum of Future Expenses"
chart.PrimaryCategoryAxis.Title = "Products"
chart.PrimaryValueAxis.Title = "In Dollars"
'Sets position of legend
chart.Legend.Position = OfficeLegendPosition.Bottom
'Sets rotation and elevation values
chart.Rotation = 20
chart.Elevation = 15
'Sets side wall properties
chart.SideWall.Fill.FillType = OfficeFillType.SolidColor
chart.SideWall.Fill.ForeColor = Color.White
chart.SideWall.Fill.BackColor = Color.White
chart.SideWall.Border.LineColor = System.Drawing.Color.Beige
'Sets floor fill option.
chart.Floor.Fill.FillType = OfficeFillType.Pattern
'Sets the floor pattern Type.
chart.Floor.Fill.Pattern = OfficeGradientPattern.Pat_Divot
'Sets the floor fore and Back ground color.
chart.Floor.Fill.ForeColor = System.Drawing.Color.Blue
chart.Floor.Fill.BackColor = System.Drawing.Color.White
'Sets the floor thickness.
chart.Floor.Thickness = 3
'Sets the back wall fill option.
chart.BackWall.Fill.FillType = OfficeFillType.Gradient
'Sets the Texture Type.
chart.BackWall.Fill.GradientColorType = OfficeGradientColor.TwoColor
chart.BackWall.Fill.GradientStyle = OfficeGradientStyle.Diagonl_Down
chart.BackWall.Fill.ForeColor = Color.WhiteSmoke
chart.BackWall.Fill.BackColor = Color.LightBlue
'Sets the Border Line color.
chart.BackWall.Border.LineColor = System.Drawing.Color.Wheat
'Sets the Picture Type.
chart.BackWall.PictureUnit = OfficeChartPictureType.stretch
'Sets the back wall thickness.
chart.BackWall.Thickness = 10
'Saves and closes the document
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Charts/Applying-3D-formats).

## Removing Chart

The following code example illustrates how to remove the chart from the document.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Loads the template document 
FileStream fileStreamPath = new FileStream("Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);
//Gets the last paragraph
WParagraph paragraph = document.LastParagraph;
//Gets the chart entity and remove it from paragraph
foreach (ParagraphItem item in paragraph.ChildEntities)
{
    if (item is WChart)
    {
        paragraph.ChildEntities.Remove(item);
        break;
    }
}
//Saves the Word document to  MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Loads the template document
WordDocument document = new WordDocument("Template.docx");
//Gets the last paragraph
WParagraph paragraph = document.LastParagraph;
//Gets the chart entity and remove it from paragraph
foreach (ParagraphItem item in paragraph.ChildEntities)
{
    if (item is WChart)
    {
        paragraph.ChildEntities.Remove(item);
        break;
    }
}
//Saves and closes the document
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Loads the template document
Dim document As New WordDocument("Template.docx")
'Gets the last paragraph
Dim paragraph As WParagraph = document.LastParagraph
'Gets the chart entity and removes it from paragraph
For Each item As ParagraphItem In paragraph.ChildEntities
If TypeOf item Is WChart Then
paragraph.ChildEntities.Remove(item)
Exit For
End If
Next
'Saves and closes the document
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Charts/Remove-chart-from-Word-document).

## Convert chart to image

You can convert the chart in Word document as image using the [SaveAsImage](https://help.syncfusion.com/cr/file-formats/Syncfusion.OfficeChartToImageConverter.ChartToImageConverter.html#Syncfusion_OfficeChartToImageConverter_ChartToImageConverter_SaveAsImage_Syncfusion_OfficeChart_IOfficeChart_System_IO_Stream_) method in [ChartToImageConverter](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WordDocument.html#Syncfusion_DocIO_DLS_WordDocument_ChartToImageConverter).

To convert chart in Word document as an image, refer the below dependencies in your application.

<table>
<thead>
<tr>
<th width="20%">
Platform(s)
</th>
<th width="40%">
NuGets for Chart to Image
</th>
<th width="40%">
Assemblies for Chart to image
</th>
</tr>
</thead>
<tr>
<td>
Cross-platform, Xamarin
</td>
<td>
{{'[Word to PDF NuGets](https://help.syncfusion.com/file-formats/docio/nuget-packages-required#converting-word-document-to-pdf)' |  markdownify }}
</td>
<td>
{{'[Word to PDF assemblies](https://help.syncfusion.com/file-formats/docio/assemblies-required#converting-word-document-to-pdf)' |  markdownify }}
</td>
</tr>
<tr>
<td>
Windows-specific
</td>
<td>
{{'[Word to PDF NuGets](https://help.syncfusion.com/file-formats/docio/nuget-packages-required#converting-word-document-to-pdf)' |  markdownify }}<br/> {{'[Chart conversion NuGets](https://help.syncfusion.com/file-formats/docio/nuget-packages-required#converting-charts)' |  markdownify }}
</td>
<td>
{{'[Word to PDF assemblies](https://help.syncfusion.com/file-formats/docio/assemblies-required#converting-word-document-to-pdf)' |  markdownify }}<br/> {{'[Chart conversion assemblies](https://help.syncfusion.com/file-formats/docio/assemblies-required#converting-charts)' |  markdownify }}
</td>
</tr>
<tr>
<td>
UWP
</td>
<td>
{{'[Word to PDF NuGets of cross platform](https://help.syncfusion.com/file-formats/docio/nuget-packages-required#converting-word-document-to-pdf)' |  markdownify }}
</td>
<td>
{{'[Word to PDF assemblies of cross platform](https://help.syncfusion.com/file-formats/docio/assemblies-required#converting-word-document-to-pdf)' |  markdownify }}
</td>
</tr>
</table>

The following code example shows how to convert chart in the Word document as image.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Open the file as Stream.
using (FileStream docStream = new FileStream("TemplateWithChart.docx", FileMode.Open))
{
    //Load file stream into Word document.
    using (WordDocument wordDocument = new WordDocument(docStream, Syncfusion.DocIO.FormatType.Automatic))
    {
        //Get the first paragraph from the section.
        WParagraph paragraph = wordDocument.LastSection.Paragraphs[0];
        //Get the chart element from the paragraph.
        WChart chart = paragraph.ChildEntities[0] as WChart;
        //Create an instance of DocIORenderer.
        using (DocIORenderer renderer = new DocIORenderer())
        {
            //Convert chart to an image.
            using (Stream stream = chart.SaveAsImage())
            {
                //Create the output image file stream. 
                using (FileStream fileStreamOutput = File.Create("ChartToImage.jpeg"))
                {
                    //Copies the converted image stream into created output stream.
                    stream.CopyTo(fileStreamOutput);
                }
            }
        }
    }
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Loads an existing Word document.
WordDocument wordDocument = new WordDocument("TemplateWithChart.docx", FormatType.Docx);
//Initializes the ChartToImageConverter for converting charts during Word to image conversion.
wordDocument.ChartToImageConverter = new ChartToImageConverter();
//Sets the scaling mode for charts. (Normal mode reduces the file size)
wordDocument.ChartToImageConverter.ScalingMode = ScalingMode.Normal;
//Gets the first paragraph from section.
WParagraph paragraph = wordDocument.LastSection.Paragraphs[0];
//Gets the chart element in the paragarph item.
WChart chart = paragraph.ChildEntities[0] as WChart;
//Creating the memory stream for chart image.
MemoryStream stream = new MemoryStream();
//Converts chart to image.
wordDocument.ChartToImageConverter.SaveAsImage(chart.OfficeChart, stream);
Image image = Image.FromStream(stream);
//Dispose the stream.
stream.Close();
//Saving image stream to file.
image.Save("ChartToImage.jpeg", ImageFormat.Jpeg);
//Closes the document.
wordDocument.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Loads an existing Word document.
Dim wordDocument As New WordDocument("TemplateWithChart.docx", FormatType.Docx)
'Initializes the ChartToImageConverter for converting charts during Word to image conversion.
wordDocument.ChartToImageConverter = New ChartToImageConverter()
'Sets the scaling mode for charts. (Normal mode reduces the file size)
wordDocument.ChartToImageConverter.ScalingMode = ScalingMode.Normal
'Gets the first paragraph from section.
Dim paragraph As WParagraph = wordDocument.LastSection.Paragraphs(0)
'Gets the chart element in the paragarph item.
Dim chart As WChart = TryCast(paragraph.ChildEntities(0),WChart)
'Creating the memory stream for chart image.
Dim stream As New MemoryStream()
'Converts chart to image.
wordDocument.ChartToImageConverter.SaveAsImage(chart.OfficeChart, stream)
Dim image As Image = Image.FromStream(stream)
'Dispose the stream.
stream.Close()
'Saving image stream to file.
image.Save("ChartToImage.jpeg", ImageFormat.Jpeg)
'Closes the document.
wordDocument.Close()
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Open the file as Stream.
using (Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.TemplateWithChart.docx"))
{
    //Load file stream into Word document.
    using (WordDocument wordDocument = new WordDocument(docStream, FormatType.Docx))
    {
        //Get the first paragraph from the section.. 
        WParagraph paragraph = wordDocument.LastSection.Paragraphs[0];
        //Get the chart element from the paragraph.
        WChart chart = paragraph.ChildEntities[0] as WChart;
        //Create a new instance of DocIORenderer class.
        using (DocIORenderer render = new DocIORenderer())
        {
            //Convert chart to an image.
            using (Stream stream = chart.SaveAsImage())
            {
                //Save the stream as file in the device and invoke it for viewing.
                Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("ChartToImage.jpeg", "image/jpeg", stream as MemoryStream);
            }
        }
    }
}
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
// You can convert a chart to images in UWP using DocIORenderer, by using cross-platform NuGets or assemblies in a UWP application.
//Open the file as Stream.
using (Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.TemplateWithChart.docx"))
{
    //Load file stream into Word document.
    using (WordDocument wordDocument = new WordDocument(docStream, FormatType.Docx))
    {
        //Get the first paragraph from the section.
        WParagraph paragraph = wordDocument.LastSection.Paragraphs[0];
        //Get the chart element from the paragraph.
        WChart chart = paragraph.ChildEntities[0] as WChart;
        //Create a new instance of DocIORenderer class.
        using (DocIORenderer render = new DocIORenderer())
        {
            //Convert chart to an image.
            using (Stream stream = chart.SaveAsImage())
            {
                //Save the memory stream as file.
                Save(stream as MemoryStream, "ChartToImage.jpeg");
            }
        }
    }
}

//Save the image.
async void Save(MemoryStream streams, string filename)
{
    streams.Position = 0;
    StorageFile stFile;
    if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
    {
        FileSavePicker savePicker = new FileSavePicker();
        savePicker.DefaultFileExtension = ".jpeg";
        savePicker.SuggestedFileName = filename;
        savePicker.FileTypeChoices.Add("Image", new List<string>() { ".jpeg" });
        stFile = await savePicker.PickSaveFileAsync();
    }
    else
    {
        StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
        stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
    }
    if (stFile != null)
    {
        using (IRandomAccessStream zipStream = await stFile.OpenAsync(FileAccessMode.ReadWrite))
        {
            //Write compressed data from memory to file.
            using (Stream outstream = zipStream.AsStreamForWrite())
            {
                byte[] buffer = streams.ToArray();
                outstream.Write(buffer, 0, buffer.Length);
                outstream.Flush();
            }
        }
    }
    //Launch the saved image file.
    await Windows.System.Launcher.LaunchFileAsync(stFile);
}
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Charts/Convert-chart-to-image).

N> 1. To convert chart in Word document as image, it is need to refer chart conversion related [assemblies](https://help.syncfusion.com/file-formats/docio/assemblies-required#converting-charts) or [NuGet packages](https://help.syncfusion.com/file-formats/docio/nuget-packages-required#converting-charts).
N> 2. The ChartToImageConverter is supported from .NET Framework 4.0 onwards.

## Word 2016 Charts

Essential DocIO supports creating and manipulating new and modern chart types such as waterfall, which is introduced in Microsoft Word 2016.

### Waterfall

[Waterfall](https://support.microsoft.com/en-us/office/create-a-waterfall-chart-8de1ece4-ff21-4d37-acd7-546f5527f185?ui=en-us&rs=en-us&ad=us#) chart helps understand the finances of business owners by viewing profit and loss statements. You can quickly illustrate the line items in your financial data and get a clear picture of how each item is impacting your bottom line using a Waterfall chart.

The following code example illustrates how to create a [Waterfall](https://help.syncfusion.com/cr/file-formats/Syncfusion.OfficeChart.OfficeChartType.html) chart.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Creates a new Word document.
using (WordDocument document = new WordDocument())
{
    //Adds section to the document.
    IWSection sec = document.AddSection();
    //Adds paragraph to the section.
    IWParagraph paragraph = sec.AddParagraph();
    //Creates and Appends chart to the paragraph.
    WChart chart = paragraph.AppendChart(446, 270);
    //Sets chart type.
    chart.ChartType = OfficeChartType.WaterFall;
    //Sets data range.
    chart.DataRange = chart.ChartData[1, 1, 8, 2];
    chart.IsSeriesInRows = false;
    chart.ChartData.SetValue(2, 1, "Start");
    chart.ChartData.SetValue(2, 2, 120000);
    chart.ChartData.SetValue(3, 1, "Product Revenue");
    chart.ChartData.SetValue(3, 2, 570000);
    chart.ChartData.SetValue(4, 1, "Service Revenue");
    chart.ChartData.SetValue(4, 2, 230000);
    chart.ChartData.SetValue(5, 1, "Positive Balance");
    chart.ChartData.SetValue(5, 2, 920000);
    chart.ChartData.SetValue(6, 1, "Fixed Costs");
    chart.ChartData.SetValue(6, 2, -345000);
    chart.ChartData.SetValue(7, 1, "Variable Costs");
    chart.ChartData.SetValue(7, 2, -230000);
    chart.ChartData.SetValue(8, 1, "Total");
    chart.ChartData.SetValue(8, 2, 345000);
    //Data point settings as total in chart.
    IOfficeChartSerie series = chart.Series[0];
    chart.Series[0].DataPoints[3].SetAsTotal = true;
    chart.Series[0].DataPoints[6].SetAsTotal = true;
    //Showing the connector lines between data points.
    chart.Series[0].SerieFormat.ShowConnectorLines = true;
    //Set the chart title.
    chart.ChartTitle = "Company Profit (in USD)";
    //Formatting data label and legend option.
    chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.IsValue = true;
    chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.Size = 8;
    chart.Legend.Position = OfficeLegendPosition.Right;
    chart.ChartArea.Border.LinePattern = OfficeChartLinePattern.None;    
    //Saves the Word document to MemoryStream.
    MemoryStream outputStream = new MemoryStream();
    document.Save(outputStream, FormatType.Docx);
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Creates a new Word document.
using (WordDocument document = new WordDocument())
{
    //Adds section to the document.
    IWSection sec = document.AddSection();
    //Adds paragraph to the section.
    IWParagraph paragraph = sec.AddParagraph();
    //Creates and Appends chart to the paragraph.
    WChart chart = paragraph.AppendChart(446, 270);
    //Sets chart type.
    chart.ChartType = OfficeChartType.WaterFall;
    //Sets data range.
    chart.DataRange = chart.ChartData[1, 1, 8, 2];
    chart.IsSeriesInRows = false;
    chart.ChartData.SetValue(2, 1, "Start");
    chart.ChartData.SetValue(2, 2, 120000);
    chart.ChartData.SetValue(3, 1, "Product Revenue");
    chart.ChartData.SetValue(3, 2, 570000);
    chart.ChartData.SetValue(4, 1, "Service Revenue");
    chart.ChartData.SetValue(4, 2, 230000);
    chart.ChartData.SetValue(5, 1, "Positive Balance");
    chart.ChartData.SetValue(5, 2, 920000);
    chart.ChartData.SetValue(6, 1, "Fixed Costs");
    chart.ChartData.SetValue(6, 2, -345000);
    chart.ChartData.SetValue(7, 1, "Variable Costs");
    chart.ChartData.SetValue(7, 2, -230000);
    chart.ChartData.SetValue(8, 1, "Total");
    chart.ChartData.SetValue(8, 2, 345000);
    //Data point settings as total in chart.
    IOfficeChartSerie series = chart.Series[0];
    chart.Series[0].DataPoints[3].SetAsTotal = true;
    chart.Series[0].DataPoints[6].SetAsTotal = true;
    //Showing the connector lines between data points.
    chart.Series[0].SerieFormat.ShowConnectorLines = true;
    //Set the chart title.
    chart.ChartTitle = "Company Profit (in USD)";
    //Formatting data label and legend option.
    chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.IsValue = true;
    chart.Series[0].DataPoints.DefaultDataPoint.DataLabels.Size = 8;
    chart.Legend.Position = OfficeLegendPosition.Right;
    chart.ChartArea.Border.LinePattern = OfficeChartLinePattern.None;
    //Saves the WordDocument instance.
    document.Save("Sample.docx", FormatType.Docx);
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Creates a new Word document.
Using document As WordDocument = New WordDocument()
    'Adds section to the document.
    Dim sec As IWSection = document.AddSection()
    'Adds paragraph to the section.
    Dim paragraph As IWParagraph = sec.AddParagraph()
    'Creates and Appends chart to the paragraph.
    Dim chart As WChart = paragraph.AppendChart(446, 270)
    'Sets chart type.
    chart.ChartType = OfficeChartType.WaterFall
    'Sets data range.
    chart.DataRange = chart.ChartData(1, 1, 8, 2)
    chart.IsSeriesInRows = False
    chart.ChartData.SetValue(2, 1, "Start")
    chart.ChartData.SetValue(2, 2, 120000)
    chart.ChartData.SetValue(3, 1, "Product Revenue")
    chart.ChartData.SetValue(3, 2, 570000)
    chart.ChartData.SetValue(4, 1, "Service Revenue")
    chart.ChartData.SetValue(4, 2, 230000)
    chart.ChartData.SetValue(5, 1, "Positive Balance")
    chart.ChartData.SetValue(5, 2, 920000)
    chart.ChartData.SetValue(6, 1, "Fixed Costs")
    chart.ChartData.SetValue(6, 2, -345000)
    chart.ChartData.SetValue(7, 1, "Variable Costs")
    chart.ChartData.SetValue(7, 2, -230000)
    chart.ChartData.SetValue(8, 1, "Total")
    chart.ChartData.SetValue(8, 2, 345000)
    'Data point settings as total in chart.
    Dim series As IOfficeChartSerie = chart.Series(0)
    chart.Series(0).DataPoints(3).SetAsTotal = True
    chart.Series(0).DataPoints(6).SetAsTotal = True
    'Showing the connector lines between data points.
    chart.Series(0).SerieFormat.ShowConnectorLines = True
    'Set the chart title.
    chart.ChartTitle = "Company Profit (in USD)"
    'Formatting data label and legend option.
    chart.Series(0).DataPoints.DefaultDataPoint.DataLabels.IsValue = True
    chart.Series(0).DataPoints.DefaultDataPoint.DataLabels.Size = 8
    chart.Legend.Position = OfficeLegendPosition.Right
    chart.ChartArea.Border.LinePattern = OfficeChartLinePattern.None
    'Saves the WordDocument instance.
    document.Save("Sample.docx", FormatType.Docx)
End Using
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Charts/Create-waterfall-chart).

By executing the code example above, it generates the resultant Word document as follows.

![Word WaterFall Chart](workingwithchartsimages/waterfall-in-file-formats-word.png)

N>These charts are supported only in Word 2016 and are not supported in the previous versions.

## Supported Chart Types 

The following chart types are supported in DocIO.

* [Area](https://support.syncfusion.com/kb/article/11899/how-to-create-area-chart-in-word-document-using-c)
* [Area_3D](https://support.syncfusion.com/kb/article/11896/how-to-create-3d-area-chart-in-word-document-using-c)
* [Area_Stacked](https://support.syncfusion.com/kb/article/11900/how-to-create-stacked-area-chart-in-word-document-using-c)
* [Area_Stacked_100](https://support.syncfusion.com/kb/article/11890/how-to-create-100-stacked-area-chart-in-word-document-using-c)
* [Area_Stacked_100_3D](https://support.syncfusion.com/kb/article/11887/how-to-create-3d-100-stacked-area-chart-in-word-document-using-c)
* [Area_Stacked_3D](https://support.syncfusion.com/kb/article/11866/how-to-create-3d-stacked-area-chart-in-word-document-using-c)
* [Bar_Clustered](https://support.syncfusion.com/kb/article/12028/how-to-create-clustered-bar-chart-in-word-document-using-c)
* [Bar_Clustered_3D](https://support.syncfusion.com/kb/article/11976/how-to-create-3d-clustered-bar-chart-in-word-document-using-c)
* [Bar_Stacked](https://support.syncfusion.com/kb/article/12065/how-to-create-stacked-bar-chart-in-word-document-using-c)
* [Bar_Stacked_100](https://support.syncfusion.com/kb/article/12022/how-to-create-100-stacked-bar-chart-in-word-document-using-c)
* [Bar_Stacked_100_3D](https://support.syncfusion.com/kb/article/11987/how-to-create-3d-100-stacked-bar-chart-in-word-document-using-c)
* [Bar_Stacked_3D](https://support.syncfusion.com/kb/article/11997/how-to-create-3d-stacked-bar-chart-in-word-document-using-c)
* [Bubble](https://support.syncfusion.com/kb/article/12013/how-to-create-bubble-chart-in-word-document-using-c)
* [Bubble_3D](https://support.syncfusion.com/kb/article/12139/how-to-create-3d-bubble-chart-in-word-document-using-c)
* [Column_3D](https://support.syncfusion.com/kb/article/12024/how-to-create-3d-column-chart-in-word-document-using-c)
* [Column_Clustered](https://support.syncfusion.com/kb/article/11178/how-to-create-clustered-column-chart-in-word-document-using-c-and-vb-net)
* [Column_Clustered_3D](https://support.syncfusion.com/kb/article/12096/how-to-create-3d-clustered-column-chart-in-word-document-using-c)
* [Column_Stacked](https://support.syncfusion.com/kb/article/12003/how-to-create-stacked-column-chart-in-word-document-using-c)
* [Column_Stacked_100](https://support.syncfusion.com/kb/article/12093/how-to-create-100-stacked-column-chart-in-word-document-using-c)
* [Column_Stacked_100_3D](https://support.syncfusion.com/kb/article/12090/how-to-create-3d-100-stacked-column-chart-in-word-document-using-c)
* [Column_Stacked_3D](https://support.syncfusion.com/kb/article/12087/how-to-create-3d-stacked-column-chart-in-word-document-using-c)
* [Combination_Chart](https://support.syncfusion.com/kb/article/12195/how-to-create-combination-chart-in-word-document-using-c)
* [Cone_Bar_Clustered](https://support.syncfusion.com/kb/article/12118/how-to-create-clustered-bar-cone-chart-in-word-document-using-c)
* [Cone_Bar_Stacked](https://support.syncfusion.com/kb/article/12148/how-to-create-stacked-bar-cone-chart-in-word-document-using-c)
* [Cone_Bar_Stacked_100](https://support.syncfusion.com/kb/article/12145/how-to-create-100-stacked-bar-cone-chart-in-word-document-using-c)
* [Cone_Clustered](https://support.syncfusion.com/kb/article/12207/how-to-create-clustered-cone-chart-in-word-document-using-c)
* [Cone_Clustered_3D](https://support.syncfusion.com/kb/article/12142/how-to-create-3d-clustered-cone-chart-in-word-document-using-c)
* [Cone_Stacked](https://support.syncfusion.com/kb/article/12196/how-to-create-stacked-cone-chart-in-word-document-using-c)
* [Cone_Stacked_100](https://support.syncfusion.com/kb/article/12192/how-to-create-100-stacked-cone-chart-in-word-document-using-c)
* [Cylinder_Bar_Clustered](https://support.syncfusion.com/kb/article/12189/how-to-create-clustered-bar-cylinder-chart-in-word-document-using-c)
* [Cylinder_Bar_Stacked](https://support.syncfusion.com/kb/article/12210/how-to-create-stacked-bar-cylinder-chart-in-word-document-using-c)
* [Cylinder_Bar_Stacked_100](https://support.syncfusion.com/kb/article/12181/how-to-create-100-stacked-bar-cylinder-chart-in-word-document-using-c)
* [Cylinder_Clustered](https://support.syncfusion.com/kb/article/12116/how-to-create-clustered-cylinder-chart-in-word-document-using-c)
* [Cylinder_Clustered_3D](https://support.syncfusion.com/kb/article/11833/how-to-create-3d-clustered-cylinder-chart-in-word-document-using-c)
* [Cylinder_Stacked](https://support.syncfusion.com/kb/article/12124/how-to-create-stacked-cylinder-chart-in-word-document-using-c)
* [Cylinder_Stacked_100](https://support.syncfusion.com/kb/article/12170/how-to-create-100-stacked-cylinder-chart-in-word-document-using-c)
* [Doughnut](https://support.syncfusion.com/kb/article/12184/how-to-create-doughnut-chart-in-word-document-using-c)
* [Line](https://support.syncfusion.com/kb/article/12185/how-to-create-line-chart-in-word-document-using-c)
* [Line_3D](https://support.syncfusion.com/kb/article/12217/how-to-create-3d-line-chart-in-word-document-using-c)
* [Line_Markers](https://support.syncfusion.com/kb/article/12222/how-to-create-line-with-markers-chart-in-word-document-using-c)
* [Line_Markers_Stacked](https://support.syncfusion.com/kb/article/12215/how-to-create-stacked-line-with-markers-chart-in-word-document-using-c)
* [Line_Markers_Stacked_100](https://support.syncfusion.com/kb/article/12212/how-to-create-100-stacked-line-with-markers-chart-in-word-document-using-c)
* [Line_Stacked](https://support.syncfusion.com/kb/article/12211/how-to-create-stacked-line-chart-in-word-document-using-c)
* [Line_Stacked_100](https://support.syncfusion.com/kb/article/12209/how-to-create-100-stacked-line-chart-in-word-document-using-c)
* [Pie](https://support.syncfusion.com/kb/article/12162/how-to-create-pie-chart-in-word-document-using-c)
* [Pie_3D](https://support.syncfusion.com/kb/article/12165/how-to-create-3d-pie-chart-in-word-document-using-c)
* [Pie_Bar](https://support.syncfusion.com/kb/article/12169/how-to-create-bar-of-pie-chart-in-word-document-using-c)
* [Pie_Exploded](https://support.syncfusion.com/kb/article/12101/how-to-create-exploded-pie-chart-in-word-document-using-c)
* [Pie_Exploded_3D](https://support.syncfusion.com/kb/article/12321/how-to-create-3d-exploded-pie-chart-in-word-document-using-c)
* [PieOfPie](https://support.syncfusion.com/kb/article/12313/how-to-create-pie-of-pie-chart-in-word-document-using-c)
* [Pyramid_Bar_Clustered](https://support.syncfusion.com/kb/article/12264/how-to-create-clustered-bar-pyramid-chart-in-word-document-using-c)
* [Pyramid_Bar_Stacked](https://support.syncfusion.com/kb/article/12200/how-to-create-stacked-bar-pyramid-chart-in-word-document-using-c)
* [Pyramid_Bar_Stacked_100](https://support.syncfusion.com/kb/article/12197/how-to-create-100-stacked-bar-pyramid-chart-in-word-document-using-c)
* [Pyramid_Clustered](https://support.syncfusion.com/kb/article/12213/how-to-create-clustered-pyramid-chart-in-word-document-using-c)
* [Pyramid_Clustered_3D](https://support.syncfusion.com/kb/article/12110/how-to-create-3d-clustered-pyramid-chart-in-word-document-using-c)
* [Pyramid_Stacked](https://support.syncfusion.com/kb/article/12109/how-to-create-stacked-pyramid-chart-in-word-document-using-c)
* [Pyramid_Stacked_100](https://support.syncfusion.com/kb/article/12114/how-to-create-100-stacked-pyramid-chart-in-word-document-using-c)
* [Radar](https://support.syncfusion.com/kb/article/12107/how-to-create-radar-chart-in-word-document-using-c)
* [Radar_Filled](https://support.syncfusion.com/kb/article/12104/how-to-create-filled-radar-chart-in-word-document-using-c)
* [Radar_Markers](https://support.syncfusion.com/kb/article/12103/how-to-create-radar-with-markers-chart-in-word-document-using-c)
* [Scatter_Line](https://support.syncfusion.com/kb/article/12100/how-to-create-scatter-with-straight-line-chart-in-word-document-using-c)
* [Scatter_Line_Markers](https://support.syncfusion.com/kb/article/12151/how-to-create-scatter-with-straight-lines-and-markers-chart-in-word-document-using-c)
* [Scatter_Markers](https://support.syncfusion.com/kb/article/12152/how-to-create-scatter-with-markers-chart-in-word-document-using-c)
* [Scatter_SmoothedLine](https://support.syncfusion.com/kb/article/12203/how-to-create-scatter-with-smooth-line-chart-in-word-document-using-c)
* [Scatter_SmoothedLine_Markers](https://support.syncfusion.com/kb/article/12202/how-to-create-scatter-with-smooth-line-and-markers-chart-in-word-document-using-c)
* [Stock_HighLowClose](https://support.syncfusion.com/kb/article/12271/how-to-create-stock-high-low-close-chart-in-word-document-using-c)
* [Stock_OpenHighLowClose](https://support.syncfusion.com/kb/article/12266/how-to-create-stock-open-high-low-close-chart-in-word-document-using-c)
* [Stock_VolumeHighLowClose](https://support.syncfusion.com/kb/article/12262/how-to-create-stock-volume-high-low-close-chart-in-word-document-using-c)
* [Stock_VolumeOpenHighLowClose](https://support.syncfusion.com/kb/article/12350/how-to-create-stock-volume-open-high-low-close-chart-in-word-document-using-c)
* [Surface_3D](https://support.syncfusion.com/kb/article/12240/how-to-create-3d-surface-chart-in-word-document-using-c)
* [Surface_Contour](https://support.syncfusion.com/kb/article/12250/how-to-create-contour-surface-chart-in-word-document-using-c)
* [Surface_NoColor_3D](https://support.syncfusion.com/kb/article/12247/how-to-create-wireframe-3d-surface-chart-in-word-document-using-c)
* [Surface_NoColor_Contour](https://support.syncfusion.com/kb/article/12245/how-to-create-wireframe-contour-surface-chart-in-word-document-using-c)
* [WaterFall](https://support.syncfusion.com/kb/article/12243/how-to-create-waterfall-chart-in-word-document-using-c)

## See Also

* [How to set Date format in X axis of chart in Word document](https://support.syncfusion.com/kb/article/11456/how-to-set-date-format-in-x-axis-of-chart-in-word-document)
* [How to change scatter chart marker color for each data points in Word document](https://support.syncfusion.com/kb/article/11489/how-to-change-scatter-chart-marker-color-for-each-data-points-in-word-document)
* [How to create line chart in Word document using C# and VB.NET](https://support.syncfusion.com/kb/article/11136/how-to-create-line-chart-in-word-document-using-c-and-vb-net)
* [How to create clustered column chart in Word document using C# and VB.NET](https://support.syncfusion.com/kb/article/11178/how-to-create-clustered-column-chart-in-word-document-using-c-and-vb-net)
* [How to create bubble chart in Word document using C# and VB.NET](https://support.syncfusion.com/kb/article/10818/how-to-create-bubble-chart-in-word-document-using-c-and-vb-net)
* [How to create line chart with different color series in Word document using C#?](https://support.syncfusion.com/kb/article/12275/how-to-create-line-chart-with-different-color-series-in-word-document-using-c)
* [How to set column space for column charts in Word document?](https://support.syncfusion.com/kb/article/12296/how-to-set-column-space-for-column-charts-in-word-document)
* [How to set Y-axis interval for column charts in Word document?](https://support.syncfusion.com/kb/article/12294/how-to-set-y-axis-interval-for-column-charts-in-word-document)
* [How to change chart title position in the Word document?](https://support.syncfusion.com/kb/article/12292/how-to-change-chart-title-position-in-the-word-document)