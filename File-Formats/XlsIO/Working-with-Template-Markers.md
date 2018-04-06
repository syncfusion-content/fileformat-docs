---
title: Working with Template Markers
description: Briefs about template markers operations
platform: File-formats
control: XlsIO
documentation: UG
---
# Working with Template Markers

A template marker is a special marker symbol created in an Excel template that appends multiple records from a data source into a worksheet. This marker automatically maps the column name in the data source and names of the marker fields in the template Excel document and fills the data (text or image). Essential XlsIO allows you to bind the template markers to data from various sources, such as 

* DataTable
* Business Objects
* Arrays

## Template marker Syntax

Each marker starts with a prefix character (by default it is “%” character). The marker is followed by the variable name and properties which are delimited by a character (by default it is semicolon “;”.)

<table>
<tr>
<td>
%&lt;MarkerVariable&gt;.&lt;Property&gt; <br/><br/>For example: %Customers.CompanyName<br/><br/>Where, “Customers” is marker variable name and CompanyName is the property name</td></tr>
</table>
You can change the marker prefix and delimiter characters by the **MarkerPrefix** and **ArgumentSeparator** properties of the ITemplateMarkersProcessor instance respectively. 

**Arguments**

You can specify the following arguments with the marker to customize the worksheet.

**Horizontal**-This argument specifies the horizontal direction of the data filling for variables.

Syntax: %&lt;MarkerVariable&gt;.&lt;Property&gt;;horizontal

**Vertical**-This argument specifies the vertical direction of the data filling for variables. By default, data will be filled in vertical direction

Syntax: %&lt;MarkerVariable&gt;.&lt;Property&gt;;vertical

**insert**-This argument inserts new row or column, depending on the direction argument for each new cell. Note that by default, the rows will not be inserted.

Syntax: %&lt;MarkerVariable&gt;.&lt;Property&gt;;insert

**insert****:****copystyles**-This argument copies styles from the above row or left column.

Syntax: %&lt;MarkerVariable&gt;.&lt;Property&gt;;insert:copystyles

**jump****:[****cell** **reference** **in** **R1C1** **notation****]-**This argument binds the data to the cell at the specified reference. Cell reference addresses can be relative or absolute.

Syntax: %&lt;MarkerVariable&gt;.&lt;Property&gt;;jump:R2C2

**copyrange****:[****top****-****left** **cell** **reference** **in** **R1C1****]:[****bottom****-****right** **cell** **reference** **in** **R1C1****]-**Copies the specified cells after each cell import.

Syntax: %&lt;MarkerVariable&gt;.&lt;Property&gt;;copyrange:R2C2:R4C4

## Bind from Array

An array of data can be bind to the marker in the template document.

**Syntax**: %VariableArray

Here is the screen shot of input template which has a template marker.

![](Working-with-Template-Markers_images/Working-with-Template_Markers_img1.jpeg)


Following code example illustrates how to bind the data from an array to a marker.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();
IWorkbook workbook = excelEngine.Excel.Workbooks.Open("Sample.xlsx");
IWorksheet worksheet = workbook.Worksheets[0];

//Create Template Marker Processor
ITemplateMarkersProcessor marker = workbook.CreateTemplateMarkersProcessor();

//Insert Array Horizontally
string[] names = new string[] { "Mickey", "Donald", "Tom", "Jerry" };
string[] descriptions = new string[] { "Mouse", "Duck", "Cat", "Mouse" };

marker.AddVariable("Names", names);
marker.AddVariable("Descriptions", descriptions);

//Process the markers in the template
marker.ApplyMarkers();

workbook.Version = ExcelVersion.Excel2013;
workbook.SaveAs("TemplateMarker.xlsx");

workbook.Close();
excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine()
Dim workbook As IWorkbook = excelEngine.Excel.Workbooks.Open("Sample.xlsx")
Dim sheet As IWorksheet = workbook.Worksheets(0)

'Create Template Marker Processor
Dim marker As ITemplateMarkersProcessor = workbook.CreateTemplateMarkersProcessor()

'Insert Array Horizontally
Dim names As String() = New String() {"Mickey", "Donald", "Tom", "Jerry"}
Dim descriptions As String() = New String() {"Mouse", "Duck", "Cat", "Mouse"}

marker.AddVariable("Names",names)
marker.AddVariable("Descriptions",descriptions)

'Process the markers in the template
marker.ApplyMarkers()

workbook.Version = ExcelVersion.Excel2013
workbook.SaveAs("TemplateMarker.xlsx")

workbook.close()
excelEngine.Dispose()



{% endhighlight %}

{% highlight UWP %}
//Gets assembly
Assembly assembly = typeof(App).GetTypeInfo().Assembly;

//Gets input Excel document from embedded resource collection
Stream inputStream = assembly.GetManifestResourceStream("Sample.xlsx");

ExcelEngine excelEngine = new ExcelEngine();
IWorkbook workbook = await excelEngine.Excel.Workbooks.OpenAsync(inputStream);
IWorksheet worksheet = workbook.Worksheets[0];

//Create Template Marker Processor
ITemplateMarkersProcessor marker = workbook.CreateTemplateMarkersProcessor();

//Insert Array Horizontally
string[] names = new string[] { "Mickey", "Donald", "Tom", "Jerry" };
string[] descriptions = new string[] { "Mouse", "Duck", "Cat", "Mouse" };

marker.AddVariable("Names", names);
marker.AddVariable("Descriptions", descriptions);

//Process the markers in the template
marker.ApplyMarkers();

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "TemplateMarker";
savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await workbook.SaveAsAsync(storageFile);

workbook.Close();
excelEngine.Dispose();

{% endhighlight %}
{% highlight asp.netcore %}
ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;

FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);

IWorkbook workbook = application.Workbooks.Open(fileStream);
IWorksheet worksheet = workbook.Worksheets[0];

//Create Template Marker Processor
ITemplateMarkersProcessor marker = workbook.CreateTemplateMarkersProcessor();

//Insert Array Horizontally
string[] names = new string[] { "Mickey", "Donald", "Tom", "Jerry" };
string[] descriptions = new string[] { "Mouse", "Duck", "Cat", "Mouse" };

marker.AddVariable("Names", names);
marker.AddVariable("Descriptions", descriptions);

//Process the markers in the template
marker.ApplyMarkers();

//Saving the workbook as stream
workbook.Version = ExcelVersion.Excel2013;
FileStream stream = new FileStream("TemplateMarker.xlsx", FileMode.Create, FileAccess.ReadWrite);
workbook.SaveAs(stream);

stream.Dispose();
workbook.Close();
excelEngine.Dispose();

{% endhighlight %}

{% highlight Xamarin %}
//Gets assembly
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
           
//Gets input Excel document from embedded resource collection
Stream inputStream = null;
inputStream = assembly.GetManifestResourceStream("Sample.xlsx");

ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
IWorkbook workbook = application.Workbooks.Open(inputStream);
IWorksheet worksheet = workbook.Worksheets[0];

//Create Template Marker Processor
ITemplateMarkersProcessor marker = workbook.CreateTemplateMarkersProcessor();

//Insert Array Horizontally
string[] names = new string[] { "Mickey", "Donald", "Tom", "Jerry" };
string[] descriptions = new string[] { "Mouse", "Duck", "Cat", "Mouse" };

marker.AddVariable("Names", names);
marker.AddVariable("Descriptions", descriptions);

//Process the markers in the template
marker.ApplyMarkers();

//Saving the workbook as stream
workbook.Version = ExcelVersion.Excel2013;
MemoryStream outputStream = new MemoryStream();
workbook.SaveAs(outputStream);

workbook.Close();
excelEngine.Dispose();

//Save the Excel file
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    await DependencyService.Get<ISaveWindowsPhone>().Save("TemplateMarker.xlsx", "application/msexcel", outputStream);
else
    DependencyService.Get<ISave>().Save("TemplateMarker.xlsx", "application/msexcel", outputStream);

//Dispose the input and output stream instances
inputStream.Dispose();
outputStream.Dispose();

{% endhighlight %}

{% endtabs %}  

Here is the screen shot of generated excel in which array of data is bounded. 

![](Working-with-Template-Markers_images/Working-with-Template_Markers_img2.jpeg)


You can also add/insert template markers using XlsIO APIs as shown below.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();
IWorkbook workbook = excelEngine.Excel.Workbooks.Open("Sample.xlsx");
IWorksheet sheet = workbook.Worksheets[0];

//Insert Simple marker
sheet.Range["B2"].Text = "%Marker";

//Insert marker which gets value of Author name
sheet.Range["C2"].Text = "%Marker2.Worksheet.Workbook.Author";

//Insert marker which gets cell address
sheet.Range["H2"].Text = "%ArrayProperty.Cells.Address";

ITemplateMarkersProcessor marker = workbook.CreateTemplateMarkersProcessor();
marker.AddVariable("Marker", "First test of markers");
marker.AddVariable("Marker2", sheet.Range["B2"]);
marker.AddVariable("ArrayProperty", sheet.Range["B2:G2"]);

//Process the markers in the template
marker.ApplyMarkers();   

workbook.Version = ExcelVersion.Excel2013;
workbook.SaveAs("TemplateMarker.xlsx");

workbook.Close();
excelEngine.Dispose();            



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine()
Dim workbook As IWorkbook = excelEngine.Excel.Workbooks.Open("Sample.xlsx")
IWorksheet sheet = workbook.Worksheets(0)

'Insert Simple marker
sheet.Range("B2").Text = "%Marker"

'Insert marker which gets value of Author name
sheet.Range("C2").Text = "%Marker2.Worksheet.Workbook.Author"

'Insert marker which gets cell address
sheet.Range("H2").Text = "%ArrayProperty.Cells.Address"

Dim marker As ITemplateMarkersProcessor = workbook.CreateTemplateMarkersProcessor()
marker.AddVariable("Marker", "First test of markers")
marker.AddVariable("Marker2", sheet.Range("B2"))
marker.AddVariable("ArrayProperty", sheet.Range("B2:G2"))

'Process the markers in the template
marker.ApplyMarkers()

workbook.Version = ExcelVersion.Excel2013
workbook.SaveAs("TemplateMarker.xlsx")

workbook.close()
excelEngine.Dispose()



{% endhighlight %}

{% highlight UWP %}
//Gets assembly
Assembly assembly = typeof(App).GetTypeInfo().Assembly;

//Gets input Excel document from embedded resource collection
Stream inputStream = assembly.GetManifestResourceStream("Sample.xlsx");

ExcelEngine excelEngine = new ExcelEngine();
IWorkbook workbook = await excelEngine.Excel.Workbooks.OpenAsync(inputStream);
IWorksheet sheet = workbook.Worksheets[0];

//Insert Simple marker
sheet.Range["B2"].Text = "%Marker";

//Insert marker which gets value of Author name
sheet.Range["C2"].Text = "%Marker2.Worksheet.Workbook.Author";

//Insert marker which gets cell address
sheet.Range["H2"].Text = "%ArrayProperty.Cells.Address";

ITemplateMarkersProcessor marker = workbook.CreateTemplateMarkersProcessor();
marker.AddVariable("Marker", "First test of markers");
marker.AddVariable("Marker2", sheet.Range["B2"]);
marker.AddVariable("ArrayProperty", sheet.Range["B2:G2"]);

//Process the markers in the template
marker.ApplyMarkers();

workbook.Version = ExcelVersion.Excel2013;

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "TemplateMarker";
savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await workbook.SaveAsAsync(storageFile);

workbook.Close();
excelEngine.Dispose();

{% endhighlight %}

{% highlight asp.netcore %}
ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;

FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);

IWorkbook workbook = application.Workbooks.Open(fileStream);
IWorksheet sheet = workbook.Worksheets[0];

//Insert Simple marker
sheet.Range["B2"].Text = "%Marker";

//Insert marker which gets value of Author name
sheet.Range["C2"].Text = "%Marker2.Worksheet.Workbook.Author";

//Insert marker which gets cell address
sheet.Range["H2"].Text = "%ArrayProperty.Cells.Address";

ITemplateMarkersProcessor marker = workbook.CreateTemplateMarkersProcessor();
marker.AddVariable("Marker", "First test of markers");
marker.AddVariable("Marker2", sheet.Range["B2"]);
marker.AddVariable("ArrayProperty", sheet.Range["B2:G2"]);

//Process the markers in the template
marker.ApplyMarkers();

//Saving the workbook as stream
workbook.Version = ExcelVersion.Excel2013;
FileStream stream = new FileStream("TemplateMarker.xlsx", FileMode.Create, FileAccess.ReadWrite);
workbook.SaveAs(stream);

stream.Dispose();
workbook.Close();
excelEngine.Dispose();

{% endhighlight %}

{% highlight Xamarin %}
//Gets assembly
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
           
//Gets input Excel document from embedded resource collection
Stream inputStream = null;

inputStream = assembly.GetManifestResourceStream("Sample.xlsx");

ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
IWorkbook workbook = application.Workbooks.Open(inputStream);
IWorksheet sheet = workbook.Worksheets[0];

//Insert Simple marker
sheet.Range["B2"].Text = "%Marker";

//Insert marker which gets value of Author name
sheet.Range["C2"].Text = "%Marker2.Worksheet.Workbook.Author";

//Insert marker which gets cell address
sheet.Range["H2"].Text = "%ArrayProperty.Cells.Address";

ITemplateMarkersProcessor marker = workbook.CreateTemplateMarkersProcessor();
marker.AddVariable("Marker", "First test of markers");
marker.AddVariable("Marker2", sheet.Range["B2"]);
marker.AddVariable("ArrayProperty", sheet.Range["B2:G2"]);

//Process the markers in the template
marker.ApplyMarkers();

//Saving the workbook as stream
workbook.Version = ExcelVersion.Excel2013;
MemoryStream outputStream = new MemoryStream();
workbook.SaveAs(outputStream);

workbook.Close();
excelEngine.Dispose();

//Save the Excel file
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    await DependencyService.Get<ISaveWindowsPhone>().Save("TemplateMarker.xlsx", "application/msexcel", outputStream);
else
    DependencyService.Get<ISave>().Save("TemplateMarker.xlsx", "application/msexcel", outputStream);

//Dispose the input and output stream instances
inputStream.Dispose();
outputStream.Dispose();

{% endhighlight %}
{% endtabs %}  

## Bind from DataTable

**Syntax****:**

<table>
<tr>
<td>
%&lt;DataSource&gt;.&lt;FieldName&gt; <br/><br/>For example: %Products.ProductName<br/><br/>Where, “Products” is a data source which can be data tables, datasets, data readers and data views and ProductName is the field name or column name<br/><br/></td></tr>
</table>
By default, DataTable values will be filled in the worksheet as a string format. You can detect data type and number format of DataTable values by using VariableTypeAction enumerator. To know more about the VariableTypeAction enumerator, please refer **VariableTypeAction** in API section.

Here is the screen shot of input template which has a template marker.

![](Working-with-Template-Markers_images/Working-with-Template_Markers_img3.jpeg)


The following code snippet illustrates how to detect data type and apply number format with template marker.

{% tabs %}  
{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();
IWorkbook workbook = excelEngine.Excel.Workbooks.Open("TemplateMarker.xlsx");

//Create Template Marker Processor
ITemplateMarkersProcessor marker = workbook.CreateTemplateMarkersProcessor();

DataTable reports = new DataTable();
reports.Columns.Add("SalesPerson");
reports.Columns.Add("FromDate", typeof(DateTime));
reports.Columns.Add("ToDate", typeof(DateTime));
reports.Rows.Add("Andy Bernard", new DateTime(2014, 09, 08), new DateTime(2014, 09, 11));
reports.Rows.Add("Jim Halpert", new DateTime(2014, 09, 11), new DateTime(2014, 09, 15));
reports.Rows.Add("Karen Fillippelli", new DateTime(2014, 09, 15), new DateTime(2014, 09, 20));
reports.Rows.Add("Phyllis Lapin", new DateTime(2014, 09, 21), new DateTime(2014, 09, 25));
reports.Rows.Add("Stanley Hudson", new DateTime(2014, 09, 26), new DateTime(2014, 09, 30));

// Detects number format in DateTable values
marker.AddVariable("Reports", reports,VariableTypeAction.DetectNumberFormat);

//Process the markers and detect the number format along with the data type in the template
marker.ApplyMarkers();

workbook.Version = ExcelVersion.Excel2013;
workbook.SaveAs("TemplateMarkerWithFormat.xlsx");

workbook.Close();
excelEngine.Dispose(); 

{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()
Dim workbook As IWorkbook = excelEngine.Excel.Workbooks.Open("TemplateMarker.xlsx")

'Create Template Marker Processor
Dim marker As ITemplateMarkersProcessor = workbook.CreateTemplateMarkersProcessor()

Dim reports As New DataTable()
reports.Columns.Add("SalesPerson")
reports.Columns.Add("FromDate", GetType(DateTime))
reports.Columns.Add("ToDate", GetType(DateTime))
reports.Rows.Add("Andy Bernard", New DateTime(2014, 9, 8), New DateTime(2014, 9, 11))
reports.Rows.Add("Jim Halpert", New DateTime(2014, 9, 11), New DateTime(2014, 9, 15))
reports.Rows.Add("Karen Fillippelli", New DateTime(2014, 9, 15), New DateTime(2014, 9, 20))
reports.Rows.Add("Phyllis Lapin", New DateTime(2014, 9, 21), New DateTime(2014, 9, 25))
reports.Rows.Add("Stanley Hudson", New DateTime(2014, 9, 26), New DateTime(2014, 9, 30))

'Detects number format in DateTable values
marker.AddVariable("Reports", reports, VariableTypeAction.DetectNumberFormat)

'Process the markers and detect the number format along with the data type in the template
marker.ApplyMarkers()

workbook.Version = ExcelVersion.Excel2013
workbook.SaveAs("TemplateMarkerWithFormat.xlsx")

workbook.Close()
excelEngine.Dispose()

{% endhighlight %}

{% highlight UWP %}
N> XlsIO supports binding data from data table using template markers in Windows Forms, WPF, ASP.NET, ASP.NET MVC and ASP.NET Core (2.0 onwards) platforms alone.
{% endhighlight %}
{% highlight asp.netcore %}
ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
FileStream fileStream = new FileStream("TemplateMarker.xlsx", FileMode.Open, FileAccess.Read);
IWorkbook workbook = application.Workbooks.Open(fileStream);

//Create Template Marker Processor
ITemplateMarkersProcessor marker = workbook.CreateTemplateMarkersProcessor();

DataTable reports = new DataTable();
reports.Columns.Add("SalesPerson");
reports.Columns.Add("FromDate", typeof(DateTime));
reports.Columns.Add("ToDate", typeof(DateTime));
reports.Rows.Add("Andy Bernard", new DateTime(2014, 09, 08), new DateTime(2014, 09, 11));
reports.Rows.Add("Jim Halpert", new DateTime(2014, 09, 11), new DateTime(2014, 09, 15));
reports.Rows.Add("Karen Fillippelli", new DateTime(2014, 09, 15), new DateTime(2014, 09, 20));
reports.Rows.Add("Phyllis Lapin", new DateTime(2014, 09, 21), new DateTime(2014, 09, 25));
reports.Rows.Add("Stanley Hudson", new DateTime(2014, 09, 26), new DateTime(2014, 09, 30));
            
//Detects number format in DateTable values
marker.AddVariable("Reports", reports, VariableTypeAction.DetectNumberFormat);

//Process the markers and detect the number format along with the data type in the template
marker.ApplyMarkers();

//Saving the workbook as stream
workbook.Version = ExcelVersion.Excel2013;

FileStream stream = new FileStream("TemplateMarkerWithFormat.xlsx", FileMode.Create, FileAccess.ReadWrite);
workbook.SaveAs(stream);

stream.Dispose();
workbook.Close();
excelEngine.Dispose();

{% endhighlight %}

{% highlight Xamarin %}
N> XlsIO supports binding data from data table using template markers in Windows Forms, WPF, ASP.NET, ASP.NET MVC and ASP.NET Core (2.0 onwards) platforms alone.
{% endhighlight %}
{% endtabs %}  

Here is the screen shot of generated excel in which data type is detected and then number format is applied.   

![](Working-with-Template-Markers_images/Working-with-Template_Markers_img4.jpeg)


## Bind from Business objects with images

You can generate reports more appealingly with image support in Template Markers. The possible images supported are listed below.

* GIF
* JPEG
* PNG
* BMP
* TIFF

XlsIO detects the property as image when its type is System.Drawing.Image or byte [].The image can be formatted using following arguments 

<table>
<tr>
<th>
No<br/><br/></th><th>
Image arguments<br/><br/></th><th>
Description<br/><br/></th></tr>
<tr>
<td>
1<br/><br/></td><td><span style="font-weight:bold">
No argument</span><br/>Ex: %Reports.Image;<br/><br/></td><td>
Image is applied with a default size (50x50 pixels) and position (Top-Left).<br/><br/></td></tr>
<tr>
<td>
2<br/><br/></td><td><span style="font-weight:bold">
fittocell</span><br/>Ex: %Reports.Image;fittocell<br/><br/></td><td>
The image is applied to cell width and height.<br/><br/></td></tr>
<tr>
<td>
3<br/><br/></td><td><span style="font-weight:bold">
size:</span>width,height<br/><br/>Ex:<br/><br/>%Reports.Image;size:60<br/><br/>(or)<br/><br/>%Reports.Image;size:60,60<br/><br/></td><td>
Image is applied to the specified size (width, height).<br/><br/>Height parameter is optional. Value of width is applied when height is not specified.<br/><br/></td></tr>
<tr>
<td>
4<br/><br/></td><td><span style="font-weight:bold">
position:</span>position<br/><br/>Ex:<br/><br/>%Reports.Image;position:middle-center<br/><br/>(or)<br/><br/>%Reports.Image;position:right <br/><br/></td><td>
Image is positioned (top-left, top-center, etc.,) within the cell.<br/><br/></td></tr>
</table>
In the following example, a marker is added for merging images.  Like a simple template marker, data source and property name is specified (%Reports.Image;) for image also. 

![](Working-with-Template-Markers_images/Working-with-Template_Markers_img5.jpeg)


__Marker__ __added__ __for__ __merging__ __images__

N> Image can be used in array, DataTable and Business objects.

Different positions of image are maintained internally in ImageVerticalPosition and ImageHorizontalPosition enumerators.  To know more about this, please refer **ImageVerticalPosition** and **ImageHorizontalPosition** enumerators respectively in API section.

The output screens of all the image insertion options along with its input templates are as follows.

**Default** **image** **input** **and** **output**

Input Template

![](Working-with-Template-Markers_images/Working-with-Template_Markers_img6.jpeg)


Generated Output

![](Working-with-Template-Markers_images/Working-with-Template_Markers_img7.jpeg)


**Image** **with** **FitToCell** **attribute**

Input Template

![](Working-with-Template-Markers_images/Working-with-Template_Markers_img8.jpeg)


Generated Output

![](Working-with-Template-Markers_images/Working-with-Template_Markers_img9.jpeg)


**Image** **with** **Size**

Input Template

![](Working-with-Template-Markers_images/Working-with-Template_Markers_img10.jpeg)


Generated Output

![](Working-with-Template-Markers_images/Working-with-Template_Markers_img11.jpeg)


**Image** **with** **Position**

Input Template

![](Working-with-Template-Markers_images/Working-with-Template_Markers_img12.jpeg)


Generated Output

![](Working-with-Template-Markers_images/Working-with-Template_Markers_img13.jpeg)


**Image** **with** **position** **and** **size**

Input Template

![](Working-with-Template-Markers_images/Working-with-Template_Markers_img14.jpeg)


Generated Output

![](Working-with-Template-Markers_images/Working-with-Template_Markers_img15.jpeg)


You can also refer [Template based data filling using Template Markers](/file-formats/xlsio/getting-started#template-based-data-filling-using-template-markers) section in [Getting Started](/file-formats/xlsio/getting-started) for the sample regarding template marker with images.

## Template Marker with Conditional Formatting

You can create or apply conditional format to the template marker range.  

Here is the screen shot of input template which has a template marker.

![](Working-with-Template-Markers_images/Working-with-Template_Markers_img16.jpeg)


The following code sample illustrates how to create or apply conditional format to the marker.

{% tabs %}  
{% highlight c# %}
#region Initialize Workbook

ExcelEngine excelEngine = new ExcelEngine();
IWorkbook workbook = excelEngine.Excel.Workbooks.Open("TemplateMarker.xlsx");
IWorksheet worksheet = workbook.Worksheets[0];

#endregion

#region Create Template Marker

//Create Template Marker Processor
ITemplateMarkersProcessor marker = workbook.CreateTemplateMarkersProcessor();

IConditionalFormats conditionalFormats = marker.CreateConditionalFormats(worksheet["C5"]);

#region Data Bar

//Apply markers using Formula
IConditionalFormat condition = conditionalFormats.AddCondition();

//Set Data bar and icon set for the same cell
//Set the format type
condition.FormatType = ExcelCFType.DataBar;

IDataBar dataBar = condition.DataBar;

//Set the constraint
dataBar.MinPoint.Type = ConditionValueType.LowestValue;
dataBar.MinPoint.Value = "0";
dataBar.MaxPoint.Type = ConditionValueType.HighestValue;
dataBar.MaxPoint.Value = "0";

//Set color for Bar
dataBar.BarColor = Color.FromArgb(156, 208, 243);

//Hide the value in data bar
dataBar.ShowValue = false;

#endregion

#region IconSet

condition = conditionalFormats.AddCondition();
condition.FormatType = ExcelCFType.IconSet;

IIconSet iconSet = condition.IconSet;
iconSet.IconSet = ExcelIconSetType.FourRating;
iconSet.IconCriteria[0].Type = ConditionValueType.LowestValue;
iconSet.IconCriteria[0].Value = "0";
iconSet.IconCriteria[1].Type = ConditionValueType.HighestValue;
iconSet.IconCriteria[1].Value = "0";
iconSet.ShowIconOnly = true;

#endregion

conditionalFormats = marker.CreateConditionalFormats(worksheet["D5"]);

#region Color Scale

condition = conditionalFormats.AddCondition();
condition.FormatType = ExcelCFType.ColorScale;

IColorScale colorScale = condition.ColorScale;

//Sets 3 - color scale
colorScale.SetConditionCount(3);

colorScale.Criteria[0].FormatColorRGB = Color.FromArgb(230, 197, 218);
colorScale.Criteria[0].Type = ConditionValueType.LowestValue;
colorScale.Criteria[0].Value = "0";

colorScale.Criteria[1].FormatColorRGB = Color.FromArgb(244, 210, 178);
colorScale.Criteria[1].Type = ConditionValueType.Percentile;
colorScale.Criteria[1].Value = "50";

colorScale.Criteria[2].FormatColorRGB = Color.FromArgb(245, 247, 171);
colorScale.Criteria[2].Type = ConditionValueType.HighestValue;
colorScale.Criteria[2].Value = "0";

#endregion

conditionalFormats = marker.CreateConditionalFormats(worksheet["E5"]);

#region IconSet

condition = conditionalFormats.AddCondition();
condition.FormatType = ExcelCFType.IconSet;

iconSet = condition.IconSet;
iconSet.IconSet = ExcelIconSetType.ThreeSymbols;

iconSet.IconCriteria[0].Type = ConditionValueType.LowestValue;
iconSet.IconCriteria[0].Value = "0";

iconSet.IconCriteria[1].Type = ConditionValueType.HighestValue;
iconSet.IconCriteria[1].Value = "0";

iconSet.ShowIconOnly = false;

#endregion

marker.AddVariable("Reports", GetDataTable());

//Process the markers in the template
marker.ApplyMarkers();

#endregion

#region Save the Workbook

workbook.Version = ExcelVersion.Excel2013;
workbook.SaveAs("TemplateMarkerCF.xlsx");

#endregion

workbook.Close();
excelEngine.Dispose();


{% endhighlight %}

{% highlight vb %}
'Region "Initialize Workbook"

Dim excelEngine As New ExcelEngine()
Dim workbook As IWorkbook = excelEngine.Excel.Workbooks.Open("TemplateMarker.xlsx")
Dim worksheet As IWorksheet = workbook.Worksheets(0)

'End Region

'Region "Create Template Marker"

'Create Template Marker Processor
Dim marker As ITemplateMarkersProcessor = workbook.CreateTemplateMarkersProcessor()

Dim conditionalFormats As IConditionalFormats = marker.CreateConditionalFormats(worksheet("C5"))

'Region "Data Bar"

'Apply markers using Formula
Dim condition As IConditionalFormat = conditionalFormats.AddCondition()

'Set Data bar and icon set for the same cell
'Set the format type
condition.FormatType = ExcelCFType.DataBar

Dim dataBar As IDataBar = condition.DataBar

'Set the constraint
dataBar.MinPoint.Type = ConditionValueType.LowestValue
dataBar.MinPoint.Value = "0"
dataBar.MaxPoint.Type = ConditionValueType.HighestValue
dataBar.MaxPoint.Value = "0"

'Set color for Bar
dataBar.BarColor = Color.FromArgb(156, 208, 243)

'Hide the value in data bar
dataBar.ShowValue = False

'End Region

'Region "IconSet"

condition = conditionalFormats.AddCondition()
condition.FormatType = ExcelCFType.IconSet

Dim iconSet As IIconSet = condition.IconSet
iconSet.IconSet = ExcelIconSetType.FourRating

iconSet.IconCriteria(0).Type = ConditionValueType.LowestValue
iconSet.IconCriteria(0).Value = "0"

iconSet.IconCriteria(1).Type = ConditionValueType.HighestValue
iconSet.IconCriteria(1).Value = "0"

iconSet.ShowIconOnly = True

'End Region

conditionalFormats = marker.CreateConditionalFormats(worksheet("D5"))

'Region "Color Scale"

condition = conditionalFormats.AddCondition()
condition.FormatType = ExcelCFType.ColorScale

Dim colorScale As IColorScale = condition.ColorScale

'Sets 3 - color scale
colorScale.SetConditionCount(3)

colorScale.Criteria(0).FormatColorRGB = Color.FromArgb(230, 197, 218)
colorScale.Criteria(0).Type = ConditionValueType.LowestValue
colorScale.Criteria(0).Value = "0"

colorScale.Criteria(1).FormatColorRGB = Color.FromArgb(244, 210, 178)
colorScale.Criteria(1).Type = ConditionValueType.Percentile
colorScale.Criteria(1).Value = "50"

colorScale.Criteria(2).FormatColorRGB = Color.FromArgb(245, 247, 171)
colorScale.Criteria(2).Type = ConditionValueType.HighestValue
colorScale.Criteria(2).Value = "0"

'End Region

conditionalFormats = marker.CreateConditionalFormats(worksheet("E5"))

'Region "IconSet"

condition = conditionalFormats.AddCondition()
condition.FormatType = ExcelCFType.IconSet

iconSet = condition.IconSet
iconSet.IconSet = ExcelIconSetType.ThreeSymbols

iconSet.IconCriteria(0).Type = ConditionValueType.LowestValue
iconSet.IconCriteria(0).Value = "0"

iconSet.IconCriteria(1).Type = ConditionValueType.HighestValue
iconSet.IconCriteria(1).Value = "0"

iconSet.ShowIconOnly = False

'End Region

marker.AddVariable("Reports", GetDataTable())

'Process the markers in the template
marker.ApplyMarkers()

'End Region

'Region "Save the Workbook"

workbook.Version = ExcelVersion.Excel2013
workbook.SaveAs("TemplateMarkerCF.xlsx")

'End Region

workbook.Close()
excelEngine.Dispose()



{% endhighlight %}
{% highlight UWP %}
N> XlsIO supports applying conditional formats to template markers data range from data table in Windows Forms, WPF, ASP.NET, ASP.NET MVC and ASP.NET Core (2.0 onwards) platforms alone.
{% endhighlight %}

{% highlight asp.netcore %}
#region Initialize Workbook

ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;

FileStream fileStream = new FileStream("TemplateMarker.xlsx", FileMode.Open, FileAccess.Read);

IWorkbook workbook = application.Workbooks.Open(fileStream);
IWorksheet worksheet = workbook.Worksheets[0];

#endregion

#region Create Template Marker

//Create Template Marker Processor
ITemplateMarkersProcessor marker = workbook.CreateTemplateMarkersProcessor();

IConditionalFormats conditionalFormats = marker.CreateConditionalFormats(worksheet["C5"]);

#endregion

#region Data Bar

//Apply markers using Formula
IConditionalFormat condition = conditionalFormats.AddCondition();

//Set Data bar and icon set for the same cell
//Set the format type
condition.FormatType = ExcelCFType.DataBar;

IDataBar dataBar = condition.DataBar;

//Set the constraint
dataBar.MinPoint.Type = ConditionValueType.LowestValue;
dataBar.MinPoint.Value = "0";
dataBar.MaxPoint.Type = ConditionValueType.HighestValue;
dataBar.MaxPoint.Value = "0";

//Set color for Bar
dataBar.BarColor = Color.FromArgb(156, 208, 243);

//Hide the value in data bar
dataBar.ShowValue = false;

#endregion

#region IconSet

condition = conditionalFormats.AddCondition();
condition.FormatType = ExcelCFType.IconSet;

IIconSet iconSet = condition.IconSet;
iconSet.IconSet = ExcelIconSetType.FourRating;

iconSet.IconCriteria[0].Type = ConditionValueType.LowestValue;
iconSet.IconCriteria[0].Value = "0";

iconSet.IconCriteria[1].Type = ConditionValueType.HighestValue;
iconSet.IconCriteria[1].Value = "0";

iconSet.ShowIconOnly = true;

#endregion

conditionalFormats = marker.CreateConditionalFormats(worksheet["D5"]);

#region Color Scale

condition = conditionalFormats.AddCondition();
condition.FormatType = ExcelCFType.ColorScale;

IColorScale colorScale = condition.ColorScale;

//Sets 3 - color scale
colorScale.SetConditionCount(3);

colorScale.Criteria[0].FormatColorRGB = Color.FromArgb(230, 197, 218);
colorScale.Criteria[0].Type = ConditionValueType.LowestValue;
colorScale.Criteria[0].Value = "0";

colorScale.Criteria[1].FormatColorRGB = Color.FromArgb(244, 210, 178);
colorScale.Criteria[1].Type = ConditionValueType.Percentile;
colorScale.Criteria[1].Value = "50";

colorScale.Criteria[2].FormatColorRGB = Color.FromArgb(245, 247, 171);
colorScale.Criteria[2].Type = ConditionValueType.HighestValue;
colorScale.Criteria[2].Value = "0";

#endregion

conditionalFormats = marker.CreateConditionalFormats(worksheet["E5"]);

#region IconSet

condition = conditionalFormats.AddCondition();
condition.FormatType = ExcelCFType.IconSet;

iconSet = condition.IconSet;
iconSet.IconSet = ExcelIconSetType.ThreeSymbols;

iconSet.IconCriteria[0].Type = ConditionValueType.LowestValue;
iconSet.IconCriteria[0].Value = "0";

iconSet.IconCriteria[1].Type = ConditionValueType.HighestValue;
iconSet.IconCriteria[1].Value = "0";

iconSet.ShowIconOnly = false;

#endregion

marker.AddVariable("Reports", GetDataTable());

//Process the markers in the template
marker.ApplyMarkers();

//Saving the workbook as stream
workbook.Version = ExcelVersion.Excel2013;
FileStream stream = new FileStream("TemplateMarkerCF.xlsx", FileMode.Create, FileAccess.ReadWrite);
workbook.SaveAs(stream);

stream.Dispose();
workbook.Close();
excelEngine.Dispose();

{% endhighlight %}

{% highlight Xamarin %}
N> XlsIO supports applying conditional formats to template markers data range from data table in Windows Forms, WPF, ASP.NET, ASP.NET MVC and ASP.NET Core (2.0 onwards) platforms alone.
{% endhighlight %}
{% endtabs %}  

**GetDataTable** **Method****:**

{% tabs %}  
{% highlight c# %}
private DataTable GetDataTable()

{

DataTable reports = new DataTable();

reports.Columns.Add("SalesPerson");
reports.Columns.Add("SalesJanJun", typeof(int));
reports.Columns.Add("SalesJulDec", typeof(int));
reports.Columns.Add("Change", typeof(int));

reports.Rows.Add("Andy Bernard", 45000, 58000, 29);
reports.Rows.Add("Jim Halpert", 34000, 65000, 91);
reports.Rows.Add("Karen Fillippelli", 75000, 64000, -15);
reports.Rows.Add("Phyllis Lapin", 56500, 33600, -40);
reports.Rows.Add("Stanley Hudson", 46500, 52000, 12);

return reports;

}



{% endhighlight %}

{% highlight vb %}
Private Function GetDataTable() As DataTable

Dim reports As New DataTable()

reports.Columns.Add("SalesPerson")
reports.Columns.Add("SalesJanJun", GetType(Integer))
reports.Columns.Add("SalesJulDec", GetType(Integer))
reports.Columns.Add("Change", GetType(Integer))

reports.Rows.Add("Andy Bernard", 45000, 58000, 29)
reports.Rows.Add("Jim Halpert", 34000, 65000, 91)
reports.Rows.Add("Karen Fillippelli", 75000, 64000, -15)
reports.Rows.Add("Phyllis Lapin", 56500, 33600, -40)
reports.Rows.Add("Stanley Hudson", 46500, 52000, 12)

Return reports

End Function



{% endhighlight %}
{% highlight UWP %}
N> DataTable is supported in Windows forms,WPF,ASP.NET,ASP.NET MVC and ASP.NET Core(2.0 onwards) platforms alone.
{% endhighlight %}
{% highlight asp.netcore %}
private DataTable GetDataTable()

{

DataTable reports = new DataTable();

reports.Columns.Add("SalesPerson");
reports.Columns.Add("SalesJanJun", typeof(int));
reports.Columns.Add("SalesJulDec", typeof(int));
reports.Columns.Add("Change", typeof(int));

reports.Rows.Add("Andy Bernard", 45000, 58000, 29);
reports.Rows.Add("Jim Halpert", 34000, 65000, 91);
reports.Rows.Add("Karen Fillippelli", 75000, 64000, -15);
reports.Rows.Add("Phyllis Lapin", 56500, 33600, -40);
reports.Rows.Add("Stanley Hudson", 46500, 52000, 12);

return reports;

}



{% endhighlight %}
{% highlight Xamarin %}
N> DataTable is supported in Windows forms,WPF,ASP.NET, ASP.NET MVC and ASP.NET Core(2.0 onwards) platforms alone.
{% endhighlight %}
{% endtabs %}  

Here is the screen shot of generated excel in which conditional format is applied.

![](Working-with-Template-Markers_images/Working-with-Template_Markers_img17.jpeg)




