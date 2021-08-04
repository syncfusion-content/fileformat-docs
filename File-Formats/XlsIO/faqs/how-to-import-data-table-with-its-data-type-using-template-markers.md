---
title: Import data table with data type using template markers | Syncfusion
description: Code example of Syncfusion .NET Excel library (XlsIO) to import data table with its data type using template markers.
platform: File-formats
control: XlsIO
documentation: UG
---

# How to import data table with its data type using template markers?

You can import data table with its data type using template markers by setting the **VariableTypeAction** to None. The following code snippet illustrates this.

{% tabs %}  

{% highlight c# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IWorkbook workbook = excelEngine.Excel.Workbooks.Open("TemplateMarker_Formulas.xlsx");

    //Create Template Marker Processor
    ITemplateMarkersProcessor marker = workbook.CreateTemplateMarkersProcessor();

    //Add marker variable and preserve the text value without detecting the number formats automatically
    marker.AddVariable("NumbersTable", GetTable(), VariableTypeAction.None);

    //Process the markers in the template and fill the values as it is in the DataTable
    marker.ApplyMarkers();

    workbook.Version = ExcelVersion.Excel2013;
    workbook.SaveAs("TemplateMarkerFormulas.xlsx");
}

//GetTable() method
private static DataTable GetTable()
{
    Random r = new Random();
    DataTable dt = new DataTable("NumbersTable");

    int nCols = 4;
    int nRows = 10;

    for (int i = 0; i < nCols; i++)
        dt.Columns.Add(new DataColumn("Column" + i.ToString()));

    for (int i = 0; i < nRows; ++i)
    {
        DataRow dr = dt.NewRow();
        for (int j = 0; j < nCols; j++)
            dr[j] = r.Next(0, 10);
        dt.Rows.Add(dr);
    }

    for (int rowIndex = 0;  rowIndex < nRows; rowIndex++)
    {
        dt.Rows[rowIndex]["Column3"] = "2888-" + dt.Rows[rowIndex]["Column3"].ToString();
    }

    return dt;
}

{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
    Dim workbook As IWorkbook = excelEngine.Excel.Workbooks.Open("TemplateMarker_Formulas.xlsx")

    'Create Template Marker Processor
    Dim marker As ITemplateMarkersProcessor = workbook.CreateTemplateMarkersProcessor()

    'Add marker variable and preserve the text value without detecting the number formats automatically
    marker.AddVariable("NumbersTable", GetTable(), VariableTypeAction.None)

    'Process the markers in the template and fill the values as it is in the DataTable
    marker.ApplyMarkers()

    workbook.Version = ExcelVersion.Excel2013
    workbook.SaveAs("TemplateMarkerFormulas.xlsx")
End Using

'GetTable() method
Private Function GetTable() As DataTable
    Dim r As Random = New Random()
    Dim dt As DataTable = New DataTable("NumbersTable")
    Dim nCols As Integer = 4
    Dim nRows As Integer = 10

    For i As Integer = 0 To nCols - 1
        dt.Columns.Add(New DataColumn("Column" & i.ToString()))
    Next

    For i As Integer = 0 To nRows - 1
        Dim dr As DataRow = dt.NewRow()

        For j As Integer = 0 To nCols - 1
            dr(j) = r.[Next](0, 10)
        Next

        dt.Rows.Add(dr)
    Next

    For rowIndex As Integer = 0 To nRows - 1
        dt.Rows(rowIndex)("Column3") = "2888-" & dt.Rows(rowIndex)("Column3").ToString()
    Next

    Return dt
End Function

{% endhighlight %}

{% highlight UWP %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    Stream inputStream = new FileStream("TemplateMarker_Formulas.xlsx", FileMode.Open, FileAccess.Read);
    IWorkbook workbook = await application.Workbooks.OpenAsync(inputStream, ExcelOpenType.Automatic);

    //Create Template Marker Processor
    ITemplateMarkersProcessor marker = workbook.CreateTemplateMarkersProcessor();

    //Add marker variable and preserve the text value without detecting the number formats automatically
    marker.AddVariable("NumbersTable", GetTable(), VariableTypeAction.None);

    //Process the markers in the template and fill the values as it is in the DataTable
    marker.ApplyMarkers();

    //Initializes FileSavePicker
    FileSavePicker savePicker = new FileSavePicker();
    savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
    savePicker.SuggestedFileName = "TemplateMarkerFormulas";
    savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

    //Creates a storage file from FileSavePicker
    StorageFile storageFile = await savePicker.PickSaveFileAsync();

    //Saves changes to the specified storage file
    await workbook.SaveAsAsync(storageFile);
}

//GetTable() method
private static DataTable GetTable()
{
    Random r = new Random();
    DataTable dt = new DataTable("NumbersTable");

    int nCols = 4;
    int nRows = 10;

    for (int i = 0; i < nCols; i++)
        dt.Columns.Add(new DataColumn("Column" + i.ToString()));

    for (int i = 0; i < nRows; ++i)
    {
        DataRow dr = dt.NewRow();
        for (int j = 0; j < nCols; j++)
            dr[j] = r.Next(0, 10);
        dt.Rows.Add(dr);
    }

    for (int rowIndex = 0; rowIndex < nRows; rowIndex++)
    {
        dt.Rows[rowIndex]["Column3"] = "2888-" + dt.Rows[rowIndex]["Column3"].ToString();
    }

    return dt;
}
{% endhighlight %}

{% highlight ASP.NET Core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    FileStream inputStream = new FileStream("TemplateMarker_Formulas.xlsx", FileMode.Open, FileAccess.Read);
    IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelOpenType.Automatic);

    //Create Template Marker Processor
    ITemplateMarkersProcessor marker = workbook.CreateTemplateMarkersProcessor();

    //Add marker variable and preserve the text value without detecting the number formats automatically
    marker.AddVariable("NumbersTable", GetTable(), VariableTypeAction.None);

    //Process the markers in the template and fill the values as it is in the DataTable
    marker.ApplyMarkers();

    FileStream stream = new FileStream("TemplateMarkerFormulas.xlsx", FileMode.OpenOrCreate, FileAccess.ReadWrite);
    workbook.SaveAs(stream);

    workbook.Close();
    excelEngine.Dispose();
}

//GetTable() method
private static DataTable GetTable()
{
    Random r = new Random();
    DataTable dt = new DataTable("NumbersTable");

    int nCols = 4;
    int nRows = 10;

    for (int i = 0; i < nCols; i++)
        dt.Columns.Add(new DataColumn("Column" + i.ToString()));

    for (int i = 0; i < nRows; ++i)
    {
        DataRow dr = dt.NewRow();
        for (int j = 0; j < nCols; j++)
            dr[j] = r.Next(0, 10);
        dt.Rows.Add(dr);
    }

    for (int rowIndex = 0; rowIndex < nRows; rowIndex++)
    {
        dt.Rows[rowIndex]["Column3"] = "2888-" + dt.Rows[rowIndex]["Column3"].ToString();
    }

    return dt;
}
{% endhighlight %}

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    Assembly assembly = typeof(App).GetTypeInfo().Assembly;
    Stream fileStream = assembly.GetManifestResourceStream("App.TemplateMarker_Formulas.xlsx");
    IWorkbook workbook = application.Workbooks.Open(fileStream);

    //Create Template Marker Processor
    ITemplateMarkersProcessor marker = workbook.CreateTemplateMarkersProcessor();

    //Add marker variable and preserve the text value without detecting the number formats automatically
    marker.AddVariable("NumbersTable", GetTable(), VariableTypeAction.None);

    //Process the markers in the template and fill the values as it is in the DataTable
    marker.ApplyMarkers();

    MemoryStream stream = new MemoryStream();
    workbook.SaveAs(stream);

    stream.Position = 0;

    //Save the stream as a file in the device and invoke it for viewing
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("TemplateMarkerFormulas.xlsx", "application/msexcel", stream);
}

//GetTable() method
private static DataTable GetTable()
{
    Random r = new Random();
    DataTable dt = new DataTable("NumbersTable");

    int nCols = 4;
    int nRows = 10;

    for (int i = 0; i < nCols; i++)
        dt.Columns.Add(new DataColumn("Column" + i.ToString()));

    for (int i = 0; i < nRows; ++i)
    {
        DataRow dr = dt.NewRow();
        for (int j = 0; j < nCols; j++)
            dr[j] = r.Next(0, 10);
        dt.Rows.Add(dr);
    }

    for (int rowIndex = 0; rowIndex < nRows; rowIndex++)
    {
        dt.Rows[rowIndex]["Column3"] = "2888-" + dt.Rows[rowIndex]["Column3"].ToString();
    }

    return dt;
}
{% endhighlight %}

{% endtabs %}

## See Also

* [How to import data from DataTable?](https://help.syncfusion.com/file-formats/xlsio/working-with-data#import-data-from-datatable)
* [How to import data from DataColumn?](https://help.syncfusion.com/file-formats/xlsio/working-with-data#import-data-from-datacolumn)
* [How to import data from DataView?](https://help.syncfusion.com/file-formats/xlsio/working-with-data#import-data-from-dataview)
* [How to export data from worksheet to DataTable?](https://help.syncfusion.com/file-formats/xlsio/working-with-data#import-data-from-datatable)
* [What are Import Data Options?](https://help.syncfusion.com/file-formats/xlsio/working-with-data#import-data-options)
* [How to bind from DataTable?](https://help.syncfusion.com/file-formats/xlsio/working-with-template-markers#bind-from-datatable)
* [How to bind from Nested Collection Objects with import data and group options?](https://help.syncfusion.com/file-formats/xlsio/working-with-template-markers#bind-from-nested-collection-objects-with-import-data-and-group-options)
* [How to use Template marker with conditional formatting?](https://help.syncfusion.com/file-formats/xlsio/working-with-template-markers#template-marker-with-conditional-formatting)
