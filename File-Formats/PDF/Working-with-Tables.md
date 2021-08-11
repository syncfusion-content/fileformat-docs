---
title: Working with Tables | PDF Library | Syncfusion
description: Learn how to create or add table to a PDF document, applying cell style & built-in table styles, automatic pagination and customize the rows and columns etc.
platform: file-formats
control: PDF
documentation: UG
---
# Working with Tables in PDF Library

Essential PDF provides support for two types of table models, both having a different levels of customization, which is explained below. The two types of table models are

1. [PdfGrid](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGrid.html)
2. [PdfLightTable](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTable.html)

## Creating a simple table 

### Creating a simple table using PdfLightTable in a new document


Essential PDF allows you to create the table with [DataSource](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTable.html#Syncfusion_Pdf_Tables_PdfLightTable_DataSource) from DataSet, Data Table, arrays and IEnumerable objects using [PdfLightTable](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTable.html) class. It allows you to perform simple formatting.

N> In Silverlight, Windows store apps and Xamarin only strongly typed IEnumerable objects are supported. 

The below code snippet illustrates how to create a simple table from a data source using ``PdfLightTable``.

{% tabs %}

{% highlight c# %}

//Create a new PDF document.

PdfDocument doc = new PdfDocument();

//Add a page.

PdfPage page = doc.Pages.Add();

// Create a PdfLightTable.

PdfLightTable pdfLightTable = new PdfLightTable();

// Initialize DataTable to assign as DateSource to the light table.

DataTable table = new DataTable();

//Include columns to the DataTable.

table.Columns.Add("Name");

table.Columns.Add("Age");

table.Columns.Add("Sex");

//Include rows to the DataTable.

table.Rows.Add(new string[] { "abc", "21", "Male" });

//Assign data source.

pdfLightTable.DataSource = table;

//Draw PdfLightTable.

pdfLightTable.Draw(page, new PointF(0, 0));

//Save the document.

doc.Save("Output.pdf");

//Close the document

doc.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim doc As New PdfDocument()

'Add a page.

Dim page As PdfPage = doc.Pages.Add()

' Create a PdfLightTable.

Dim pdfLightTable As New PdfLightTable()

' Initialize DataTable to assign as DateSource to the light table.

Dim table As New DataTable()

'Include columns to the DataTable.

table.Columns.Add("Name")

table.Columns.Add("Age")

table.Columns.Add("Sex")

'Include rows to the DataTable.

table.Rows.Add(New String() {"abc", "21", "Male"})

'Assign data source.

pdfLightTable.DataSource = table

'Draw PdfLightTable.

pdfLightTable.Draw(page, New PointF(0, 0))

'Save the document.

doc.Save("Output.pdf")

'Close the document

doc.Close(True)

{% endhighlight %}

{% highlight UWP %}

//Create a new PDF document.

PdfDocument doc = new PdfDocument();

//Add a page.

PdfPage page = doc.Pages.Add();

// Create a PdfLightTable.

PdfLightTable pdfLightTable = new PdfLightTable();

//Add values to list

List<object> data = new List<object>();

object row = new { Name = "abc", Age = "21", Sex = "Male" };

data.Add(row);

//Add list to IEnumerable

IEnumerable<object> table = data;

//Assign data source.

pdfLightTable.DataSource = table;

//Draw PdfLightTable.

pdfLightTable.Draw(page, new PointF(0, 0));

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

await doc.SaveAsync(stream);

//Close the document.

doc.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document.

PdfDocument doc = new PdfDocument();

//Add a page.

PdfPage page = doc.Pages.Add();

// Create a PdfLightTable.

PdfLightTable pdfLightTable = new PdfLightTable();

//Add values to list

List<object> data = new List<object>();

object row = new { Name = "abc", Age = "21", Sex = "Male" };

data.Add(row);

//Add list to IEnumerable

IEnumerable<object> table = data;

//Assign data source.

pdfLightTable.DataSource = table;

//Draw PdfLightTable.

pdfLightTable.Draw(page, new Syncfusion.Drawing.PointF(0, 0));

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the PDF document to stream.

doc.Save(stream);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document.

doc.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Create a new PDF document.

PdfDocument doc = new PdfDocument();

//Add a page.

PdfPage page = doc.Pages.Add();

// Create a PdfLightTable.

PdfLightTable pdfLightTable = new PdfLightTable();

//Add values to list

List<object> data = new List<object>();

object row = new { Name = "abc", Age = "21", Sex = "Male" };

data.Add(row);

//Add list to IEnumerable

IEnumerable<object> table = data;

//Assign data source.

pdfLightTable.DataSource = table;

//Draw PdfLightTable.

pdfLightTable.Draw(page, new Syncfusion.Drawing.PointF(0, 0));

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

doc.Save(stream);

//Close the document.

doc.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

{% endhighlight %}
{% endtabs %}

You can directly add rows and columns instead of a data source, by setting [DataSourceType](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTable.html#Syncfusion_Pdf_Tables_PdfLightTable_DataSourceType) property to **TableDirect** of [PdfLightTableDataSourceType](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTableDataSourceType.html) Enum.

The following code illustrates how to add the data directly into the [PdfLightTable](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTable.html).

{% tabs %}
{% highlight c# %}

//Create a new PDF document.

PdfDocument doc = new PdfDocument();

//Add a page.

PdfPage page = doc.Pages.Add();

//Acquire page's graphics.

PdfGraphics graphics = page.Graphics;

//Declare a PdfLightTable.

PdfLightTable pdfLightTable = new PdfLightTable();

//Set the Data source as direct.

pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.

pdfLightTable.Columns.Add(new PdfColumn("Roll Number"));

pdfLightTable.Columns.Add(new PdfColumn("Name"));

pdfLightTable.Columns.Add(new PdfColumn("Class"));

//Add rows.

pdfLightTable.Rows.Add(new object[] { "111", "Maxim", "III" });

//Draw the PdfLightTable.

pdfLightTable.Draw(page, PointF.Empty);

//Save the document.

doc.Save("Output.pdf");

//Close the document

doc.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim doc As New PdfDocument()

'Add a page.

Dim page As PdfPage = doc.Pages.Add()

'Acquire page's graphics.

Dim graphics As PdfGraphics = page.Graphics

'Declare a PdfLightTable.

Dim pdfLightTable As New PdfLightTable()

'Set the Data source type as direct.

pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect

'Create columns.

pdfLightTable.Columns.Add(New PdfColumn("Roll Number"))

pdfLightTable.Columns.Add(New PdfColumn("Name"))

pdfLightTable.Columns.Add(New PdfColumn("Class"))

'Add rows.

pdfLightTable.Rows.Add(New Object() {"111", "Maxim", "III"})

'Draw the PdfLightTable.

pdfLightTable.Draw(page, PointF.Empty)

'Save the document.

doc.Save("Output.pdf")

'Close the document

doc.Close(True)

{% endhighlight %}

{% highlight UWP %}

//Create a new PDF document.

PdfDocument doc = new PdfDocument();

//Add a page.

PdfPage page = doc.Pages.Add();

//Acquire page's graphics.

PdfGraphics graphics = page.Graphics;

//Declare a PdfLightTable.

PdfLightTable pdfLightTable = new PdfLightTable();

//Set the Data source as direct.

pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.

pdfLightTable.Columns.Add(new PdfColumn("Roll Number"));

pdfLightTable.Columns.Add(new PdfColumn("Name"));

pdfLightTable.Columns.Add(new PdfColumn("Class"));

//Add rows.

pdfLightTable.Rows.Add(new object[] { "111", "Maxim", "III" });

//Draw the PdfLightTable.

pdfLightTable.Draw(page, PointF.Empty);

//Save the PDF document into stream

MemoryStream stream = new MemoryStream();

await doc.SaveAsync(stream);

//Close the document.

doc.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Output.pdf");


{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document.

PdfDocument doc = new PdfDocument();

//Add a page.

PdfPage page = doc.Pages.Add();

//Acquire page's graphics.

PdfGraphics graphics = page.Graphics;

//Declare a PdfLightTable.

PdfLightTable pdfLightTable = new PdfLightTable();

//Set the Data source as direct.

pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.

pdfLightTable.Columns.Add(new PdfColumn("Roll Number"));

pdfLightTable.Columns.Add(new PdfColumn("Name"));

pdfLightTable.Columns.Add(new PdfColumn("Class"));

//Add rows.

pdfLightTable.Rows.Add(new object[] { "111", "Maxim", "III" });

//Draw the PdfLightTable.

pdfLightTable.Draw(page, Syncfusion.Drawing.PointF.Empty);

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the PDF document to stream.

doc.Save(stream);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document.

doc.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Create a new PDF document.

PdfDocument doc = new PdfDocument();

//Add a page.

PdfPage page = doc.Pages.Add();

//Acquire page's graphics.

PdfGraphics graphics = page.Graphics;

//Declare a PdfLightTable.

PdfLightTable pdfLightTable = new PdfLightTable();

//Set the Data source as direct.

pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.

pdfLightTable.Columns.Add(new PdfColumn("Roll Number"));

pdfLightTable.Columns.Add(new PdfColumn("Name"));

pdfLightTable.Columns.Add(new PdfColumn("Class"));

//Add rows.

pdfLightTable.Rows.Add(new object[] { "111", "Maxim", "III" });

//Draw the PdfLightTable.

pdfLightTable.Draw(page, Syncfusion.Drawing.PointF.Empty);

//Save the PDF document into stream

MemoryStream stream = new MemoryStream();

doc.Save(stream);

//Close the document.

doc.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

### Creating a simple table using PdfLightTable in an existing document

You can create table using [PdfLightTable](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTable.html) in the existing document by using the following code sample.

{% tabs %}

{% highlight c# %}

//Load a PDF document.
PdfLoadedDocument doc = new PdfLoadedDocument("input.pdf");

//Get first page from document
PdfLoadedPage page = doc.Pages[0] as PdfLoadedPage;
            
//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;
            
// Create a PdfLightTable.
PdfLightTable pdfLightTable = new PdfLightTable();

// Initialize DataTable to assign as DateSource to the light table.
DataTable table = new DataTable();

//Include columns to the DataTable.
table.Columns.Add("Name");

table.Columns.Add("Age");

table.Columns.Add("Sex");

//Include rows to the DataTable.
table.Rows.Add(new string[] { "abc", "21", "Male" });

//Assign data source.
pdfLightTable.DataSource = table;

//Draw PdfLightTable.
pdfLightTable.Draw(graphics, new PointF(0, 0));

//Save the document.
doc.Save("Output.pdf");

//Close the document
doc.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Load a PDF document.
Dim doc As New PdfLoadedDocument("input.pdf")

'Get first page from document
Dim page As PdfLoadedPage = TryCast(doc.Pages(0), PdfLoadedPage)

'Create PDF graphics for the page
Dim graphics As PdfGraphics = page.Graphics

' Create a PdfLightTable.
Dim pdfLightTable As New PdfLightTable()

' Initialize DataTable to assign as DateSource to the light table.
Dim table As New DataTable()

'Include columns to the DataTable.
table.Columns.Add("Name")

table.Columns.Add("Age")

table.Columns.Add("Sex")

'Include rows to the DataTable.
table.Rows.Add(New String() {"abc", "21", "Male"})

'Assign data source.
pdfLightTable.DataSource = table

'Draw PdfLightTable.
pdfLightTable.Draw(graphics, New PointF(0, 0))

'Save the document.
doc.Save("Output.pdf")

'Close the document
doc.Close(True)

{% endhighlight %}

{% highlight UWP %}

//Create the file open picker
var picker = new FileOpenPicker();

picker.FileTypeFilter.Add(".pdf");

//Browse and chose the file
StorageFile file = await picker.PickSingleFileAsync();

//Creates an empty PDF loaded document instance
PdfLoadedDocument doc = new PdfLoadedDocument();

//Loads or opens an existing PDF document through Open method of PdfLoadedDocument class
await doc.OpenAsync(file);

//Get first page from document
PdfLoadedPage page = doc.Pages[0] as PdfLoadedPage;

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Create a PdfLightTable.
PdfLightTable pdfLightTable = new PdfLightTable();

//Add values to list
List<object> data = new List<object>();

object row = new { Name = "abc", Age = "21", Sex = "Male" };
data.Add(row);

//Add list to IEnumerable
IEnumerable<object> table = data;

//Assign data source.
pdfLightTable.DataSource = table;

//Draw PdfLightTable.
pdfLightTable.Draw(graphics, new PointF(0, 0));

//Save the PDF document into stream
MemoryStream stream = new MemoryStream();
await doc.SaveAsync(stream);

//Close the document.
doc.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document
FileStream docStream = new FileStream("input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument doc = new PdfLoadedDocument(docStream);

//Get first page from document
PdfLoadedPage page = doc.Pages[0] as PdfLoadedPage;

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

// Create a PdfLightTable.
PdfLightTable pdfLightTable = new PdfLightTable();

//Add values to list
List<object> data = new List<object>();
object row = new { Name = "abc", Age = "21", Sex = "Male" };

data.Add(row);

//Add list to IEnumerable
IEnumerable<object> table = data;

//Assign data source.
pdfLightTable.DataSource = table;

//Draw PdfLightTable.
pdfLightTable.Draw(graphics, new Syncfusion.Drawing.PointF(0, 0));

//Creating the stream object
MemoryStream stream = new MemoryStream();

//Save the PDF document to stream.
doc.Save(stream);

//If the position is not set to '0' then the PDF will be empty.
stream.Position = 0;

//Close the document.
doc.Close(true);

//Defining the ContentType for pdf file.
string contentType = "application/pdf";

//Define the file name.
string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

 //Load the file as stream
Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.pdf");
PdfLoadedDocument doc = new PdfLoadedDocument(docStream);

//Get first page from document
PdfLoadedPage page = doc.Pages[0] as PdfLoadedPage;

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Create a PdfLightTable.
PdfLightTable pdfLightTable = new PdfLightTable();

//Add values to list
List<object> data = new List<object>();

object row = new { Name = "abc", Age = "21", Sex = "Male" };
data.Add(row);

//Add list to IEnumerable
IEnumerable<object> table = data;

//Assign data source.
pdfLightTable.DataSource = table;

//Draw PdfLightTable.
pdfLightTable.Draw(graphics, new Syncfusion.Drawing.PointF(0, 0));

//Save the PDF document into stream
MemoryStream stream = new MemoryStream();

doc.Save(stream);

//Close the document.
doc.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

### Creating a simple table using PdfGrid in a new document

[PdfGrid](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGrid.html) allows you to create table by entering the data manually or from an external data source. The [DataSource](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGrid.html#Syncfusion_Pdf_Grid_PdfGrid_DataSource) can be a data set, data table, arrays or a IEnumerable object.

N> In Silverlight, Windows store apps and Xamarin only strongly typed IEnumerable objects are supported. 

The below code snippet illustrates how to create a simple table from a data source using ``PdfGrid``.

{% tabs %}

{% highlight c# %}


//Create a new PDF document.

PdfDocument doc = new PdfDocument();

//Add a page.

PdfPage page = doc.Pages.Add();

//Create a PdfGrid.

PdfGrid pdfGrid = new PdfGrid();

//Create a DataTable.

DataTable dataTable = new DataTable();

//Add columns to the DataTable

dataTable.Columns.Add("ID");

dataTable.Columns.Add("Name");

//Add rows to the DataTable.

dataTable.Rows.Add(new object[] { "E01", "Clay" });

dataTable.Rows.Add(new object[] { "E02", "Thomas" });

//Assign data source.

pdfGrid.DataSource = dataTable;

//Draw grid to the page of PDF document.

pdfGrid.Draw(page, new PointF(10, 10));

//Save the document.

doc.Save("Output.pdf");

//close the document

doc.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Create a new PDF document.

Dim doc As New PdfDocument()

'Add a page.

Dim page As PdfPage = doc.Pages.Add()

' Create a PdfLightTable.

Dim pdfLightTable As New PdfLightTable()

' Initialize DataTable to assign as DateSource to the light table.

Dim table As New DataTable()

'Include columns to the DataTable.

table.Columns.Add("Name")

table.Columns.Add("Age")

table.Columns.Add("Sex")

'Include rows to the DataTable.//you can add multiple rows

table.Rows.Add(New String() {"abc", "21", "Male"})

'Set DataSourceType to the light table.

pdfLightTable.DataSourceType = PdfLightTableDataSourceType.External

'Assign data source.

pdfLightTable.DataSource = table

'Draw PdfLightTable.

pdfLightTable.Draw(page, New PointF(0, 0))

'Save the document.

doc.Save("Output.pdf")

'Close the document

doc.Close(True)

{% endhighlight %}

{% highlight UWP %}

//Create a new PDF document.

PdfDocument doc = new PdfDocument();

//Add a page.

PdfPage page = doc.Pages.Add();

//Create a PdfGrid.

PdfGrid pdfGrid = new PdfGrid();

//Add values to list

List<object> data = new List<object>();

Object row1 = new { ID = "E01", Name = "Clay" };

Object row2 = new { ID = "E02", Name = "Thomas" };

data.Add(row1);

data.Add(row2);

//Add list to IEnumerable

IEnumerable<object> dataTable = data;

//Assign data source.

pdfGrid.DataSource = dataTable;

//Draw grid to the page of PDF document.

pdfGrid.Draw(page, new PointF(10, 10));

//Save the PDF document into stream

MemoryStream stream = new MemoryStream();

await doc.SaveAsync(stream);

//Close the document.

doc.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Output.pdf");


{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document.

PdfDocument doc = new PdfDocument();

//Add a page.

PdfPage page = doc.Pages.Add();

//Create a PdfGrid.

PdfGrid pdfGrid = new PdfGrid();

//Add values to list

List<object> data = new List<object>();

Object row1 = new { ID = "E01", Name = "Clay" };

Object row2 = new { ID = "E02", Name = "Thomas" };

data.Add(row1);

data.Add(row2);

//Add list to IEnumerable

IEnumerable<object> dataTable = data;

//Assign data source.

pdfGrid.DataSource = dataTable;

//Draw grid to the page of PDF document.

pdfGrid.Draw(page, new Syncfusion.Drawing.PointF(10, 10));

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the PDF document to stream.

doc.Save(stream);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document.

doc.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Create a new PDF document.

PdfDocument doc = new PdfDocument();

//Add a page.

PdfPage page = doc.Pages.Add();

//Create a PdfGrid.

PdfGrid pdfGrid = new PdfGrid();

//Add values to list

List<object> data = new List<object>();

Object row1 = new { ID = "E01", Name = "Clay" };

Object row2 = new { ID = "E02", Name = "Thomas" };

data.Add(row1);

data.Add(row2);

//Add list to IEnumerable

IEnumerable<object> dataTable = data;

//Assign data source.

pdfGrid.DataSource = dataTable;

//Draw grid to the page of PDF document.

pdfGrid.Draw(page, new Syncfusion.Drawing.PointF(10, 10));

//Save the PDF document into stream

MemoryStream stream = new MemoryStream();

doc.Save(stream);

//Close the document.

doc.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}


{% endhighlight %}

{% endtabs %}

You can set the data directly without setting any data source using [PdfGridRow](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGridRow.html) and [PdfGridColumn](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGridColumn.html) classes. 

The below code snippet illustrates how to create the simple table directly using [PdfGrid](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGrid.html).

{% tabs %}

{% highlight c# %}


//Create a new PDF document.

PdfDocument pdfDocument = new PdfDocument();

PdfPage pdfPage = pdfDocument.Pages.Add();

//Create a new PdfGrid.

PdfGrid pdfGrid = new PdfGrid();

//Add three columns.

pdfGrid.Columns.Add(3);

//Add header.

pdfGrid.Headers.Add(1);

PdfGridRow pdfGridHeader = pdfGrid.Headers[0];

pdfGridHeader.Cells[0].Value = "Employee ID";

pdfGridHeader.Cells[1].Value = "Employee Name";

pdfGridHeader.Cells[2].Value = "Salary";

//Add rows.

PdfGridRow pdfGridRow = pdfGrid.Rows.Add();

pdfGridRow.Cells[0].Value = "E01";

pdfGridRow.Cells[1].Value = "Clay";

pdfGridRow.Cells[2].Value = "$10,000";

//Draw the PdfGrid.

pdfGrid.Draw(pdfPage, PointF.Empty);

//Save the document.

pdfDocument.Save("Output.pdf");

//Close the document

pdfDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Create a new PDF document.

Dim pdfDocument As New PdfDocument()

Dim pdfPage As PdfPage = pdfDocument.Pages.Add()

'Create a new PdfGrid.

Dim pdfGrid As New PdfGrid()

'Add three columns.

pdfGrid.Columns.Add(3)

'Add header.

pdfGrid.Headers.Add(1)

Dim pdfGridHeader As PdfGridRow = pdfGrid.Headers(0)

pdfGridHeader.Cells(0).Value = "Employee ID"

pdfGridHeader.Cells(1).Value = "Employee Name"

pdfGridHeader.Cells(2).Value = "Salary"

'Add rows.

Dim pdfGridRow As PdfGridRow = pdfGrid.Rows.Add()

pdfGridRow.Cells(0).Value = "E01"

pdfGridRow.Cells(1).Value = "Clay"

pdfGridRow.Cells(2).Value = "$10,000"

'Draw the PdfGrid.

pdfGrid.Draw(pdfPage, PointF.Empty)

'Save the document.

pdfDocument.Save("Output.pdf")

'Close the document

pdfDocument.Close(True)



{% endhighlight %}

{% highlight UWP %}

//Create a new PDF document.

PdfDocument pdfDocument = new PdfDocument();

PdfPage pdfPage = pdfDocument.Pages.Add();

//Create a new PdfGrid.

PdfGrid pdfGrid = new PdfGrid();

//Add three columns.

pdfGrid.Columns.Add(3);

//Add header.

pdfGrid.Headers.Add(1);

PdfGridRow pdfGridHeader = pdfGrid.Headers[0];

pdfGridHeader.Cells[0].Value = "Employee ID";

pdfGridHeader.Cells[1].Value = "Employee Name";

pdfGridHeader.Cells[2].Value = "Salary";

//Add rows.

PdfGridRow pdfGridRow = pdfGrid.Rows.Add();

pdfGridRow.Cells[0].Value = "E01";

pdfGridRow.Cells[1].Value = "Clay";

pdfGridRow.Cells[2].Value = "$10,000";

//Draw the PdfGrid.

pdfGrid.Draw(pdfPage, PointF.Empty);

//Save the PDF document into stream

MemoryStream stream = new MemoryStream();

await pdfDocument.SaveAsync(stream);

//Close the document.

pdfDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document.

PdfDocument pdfDocument = new PdfDocument();

PdfPage pdfPage = pdfDocument.Pages.Add();

//Create a new PdfGrid.

PdfGrid pdfGrid = new PdfGrid();

//Add three columns.

pdfGrid.Columns.Add(3);

//Add header.

pdfGrid.Headers.Add(1);

PdfGridRow pdfGridHeader = pdfGrid.Headers[0];

pdfGridHeader.Cells[0].Value = "Employee ID";

pdfGridHeader.Cells[1].Value = "Employee Name";

pdfGridHeader.Cells[2].Value = "Salary";

//Add rows.

PdfGridRow pdfGridRow = pdfGrid.Rows.Add();

pdfGridRow.Cells[0].Value = "E01";

pdfGridRow.Cells[1].Value = "Clay";

pdfGridRow.Cells[2].Value = "$10,000";

//Draw the PdfGrid.

pdfGrid.Draw(pdfPage, Syncfusion.Drawing.PointF.Empty);

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the PDF document to stream.

pdfDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document.

pdfDocument.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Create a new PDF document.

PdfDocument pdfDocument = new PdfDocument();

PdfPage pdfPage = pdfDocument.Pages.Add();

//Create a new PdfGrid.

PdfGrid pdfGrid = new PdfGrid();

//Add three columns.

pdfGrid.Columns.Add(3);

//Add header.

pdfGrid.Headers.Add(1);

PdfGridRow pdfGridHeader = pdfGrid.Headers[0];

pdfGridHeader.Cells[0].Value = "Employee ID";

pdfGridHeader.Cells[1].Value = "Employee Name";

pdfGridHeader.Cells[2].Value = "Salary";

//Add rows.

PdfGridRow pdfGridRow = pdfGrid.Rows.Add();

pdfGridRow.Cells[0].Value = "E01";

pdfGridRow.Cells[1].Value = "Clay";

pdfGridRow.Cells[2].Value = "$10,000";

//Draw the PdfGrid.

pdfGrid.Draw(pdfPage, Syncfusion.Drawing.PointF.Empty);

//Save the PDF document into stream

MemoryStream stream = new MemoryStream();

pdfDocument.Save(stream);

//Close the document.

pdfDocument.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}


{% endhighlight %}

{% endtabs %}

You can create table using [PdfGrid](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGrid.html) by loading the IEnumerable data source. Refer to the following code.

{% tabs %}

{% highlight c# %}


//Create a new PDF document

PdfDocument doc = new PdfDocument();

//Add a page

PdfPage page = doc.Pages.Add();

//Create a PdfGrid

PdfGrid pdfGrid = new PdfGrid();

//Add values to list

List<object> data = new List<object>();

Object row1 = new { ID = "1", Name = "Clay" };

Object row2 = new { ID = "2", Name = "Gray" };

Object row3 = new { ID = "3", Name = "Ash" };

data.Add(row1);

data.Add(row2);

data.Add(row3);

//Add list to IEnumerable

IEnumerable<object> tableData = data;

//Assign data source

pdfGrid.DataSource = tableData;

//Draw grid to the page of PDF document

pdfGrid.Draw(page, new PointF(10, 10));

//Save the document

doc.Save("Sample.pdf");

//close the document

doc.Close(true);




{% endhighlight %}

{% highlight vb.net %}


'Create a new PDF document

Dim doc As New PdfDocument()

'Add a page

Dim page As PdfPage = doc.Pages.Add()

'Create a PdfGrid

Dim pdfGrid As New PdfGrid()

'Add values to list

Dim data As New List(Of Object)()

Dim row1 As Object = New With {Key .ID = "1", Key .Name = "Clay"}

Dim row2 As Object = New With {Key .ID = "2", Key .Name = "Gray"}

Dim row3 As Object = New With {Key .ID = "3", Key .Name = "Ash"}

data.Add(row1)

data.Add(row2)

data.Add(row3)

'Add list to IEnumerable

Dim tableData As IEnumerable(Of Object) = data

'Assign data source

pdfGrid.DataSource = tableData

'Draw grid to the page of PDF document

pdfGrid.Draw(page, New PointF(10, 10))

'Save the document

doc.Save("Sample.pdf")

'close the document

doc.Close(True)


{% endhighlight %}

{% highlight UWP %}

//Create a new PDF document

PdfDocument doc = new PdfDocument();

//Add a page

PdfPage page = doc.Pages.Add();

//Create a PdfGrid

PdfGrid pdfGrid = new PdfGrid();

//Add values to list

List<object> data = new List<object>();

Object row1 = new { ID = "1", Name = "Clay" };

Object row2 = new { ID = "2", Name = "Gray" };

Object row3 = new { ID = "3", Name = "Ash" };

data.Add(row1);

data.Add(row2);

data.Add(row3);

//Add list to IEnumerable

IEnumerable<object> tableData = data;

//Assign data source

pdfGrid.DataSource = tableData;

//Draw grid to the page of PDF document

pdfGrid.Draw(page, new PointF(10, 10));

//Save the PDF document into stream

MemoryStream stream = new MemoryStream();

await doc.SaveAsync(stream);

//Close the document.

doc.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document

PdfDocument doc = new PdfDocument();

//Add a page

PdfPage page = doc.Pages.Add();

//Create a PdfGrid

PdfGrid pdfGrid = new PdfGrid();

//Add values to list

List<object> data = new List<object>();

Object row1 = new { ID = "1", Name = "Clay" };

Object row2 = new { ID = "2", Name = "Gray" };

Object row3 = new { ID = "3", Name = "Ash" };

data.Add(row1);

data.Add(row2);

data.Add(row3);

//Add list to IEnumerable

IEnumerable<object> tableData = data;

//Assign data source

pdfGrid.DataSource = tableData;

//Draw grid to the page of PDF document

pdfGrid.Draw(page, new Syncfusion.Drawing.PointF(10, 10));

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the PDF document to stream.

doc.Save(stream);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document.

doc.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Create a new PDF document

PdfDocument doc = new PdfDocument();

//Add a page

PdfPage page = doc.Pages.Add();

//Create a PdfGrid

PdfGrid pdfGrid = new PdfGrid();

//Add values to list

List<object> data = new List<object>();

Object row1 = new { ID = "1", Name = "Clay" };

Object row2 = new { ID = "2", Name = "Gray" };

Object row3 = new { ID = "3", Name = "Ash" };

data.Add(row1);

data.Add(row2);

data.Add(row3);

//Add list to IEnumerable

IEnumerable<object> tableData = data;

//Assign data source

pdfGrid.DataSource = tableData;

//Draw grid to the page of PDF document

pdfGrid.Draw(page, new Syncfusion.Drawing.PointF(10, 10));

//Save the PDF document into stream

MemoryStream stream = new MemoryStream();

doc.Save(stream);

//Close the document.

doc.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %} 


### Creating a simple table using PdfGrid in an existing document

You can create a table using [PdfGrid](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGrid.html) in the existing document by using the following code sample.

{% tabs %}

{% highlight c# %}

//Load a PDF document.
PdfLoadedDocument doc = new PdfLoadedDocument("input.pdf");

//Get first page from document
PdfLoadedPage page = doc.Pages[0] as PdfLoadedPage;

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Create a PdfGrid.
PdfGrid pdfGrid = new PdfGrid();

//Create a DataTable.
DataTable dataTable = new DataTable();

//Add columns to the DataTable
dataTable.Columns.Add("ID");
dataTable.Columns.Add("Name");

//Add rows to the DataTable.
dataTable.Rows.Add(new object[] { "E01", "Clay" });
dataTable.Rows.Add(new object[] { "E02", "Thomas" });

//Assign data source.
pdfGrid.DataSource = dataTable;

//Draw grid to the page of PDF document.
pdfGrid.Draw(graphics, new PointF(10, 10));

//Save the document.
doc.Save("Output.pdf");

//close the document
doc.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Load a PDF document.
Dim doc As New PdfLoadedDocument("input.pdf")

'Get first page from document
Dim page As PdfLoadedPage = TryCast(doc.Pages(0), PdfLoadedPage)

'Create PDF graphics for the page
Dim graphics As PdfGraphics = page.Graphics

'Create a PdfGrid.
Dim pdfGrid As New PdfGrid()

'Create a DataTable.
Dim dataTable As New DataTable()

'Add columns to the DataTable
dataTable.Columns.Add("ID")
dataTable.Columns.Add("Name")

'Add rows to the DataTable.
dataTable.Rows.Add(New Object() {"E01", "Clay"})
dataTable.Rows.Add(New Object() {"E02", "Thomas"})

'Assign data source.
pdfGrid.DataSource = dataTable

'Draw grid to the page of PDF document.
pdfGrid.Draw(graphics, New PointF(10, 10))

'Save the document.
doc.Save("Output.pdf")

'close the document
doc.Close(True)

{% endhighlight %}

{% highlight UWP %}

//Create the file open picker

var picker = new FileOpenPicker();

picker.FileTypeFilter.Add(".pdf");

//Browse and chose the file

StorageFile file = await picker.PickSingleFileAsync();

//Creates an empty PDF loaded document instance

PdfLoadedDocument doc = new PdfLoadedDocument();

//Loads or opens an existing PDF document through Open method of PdfLoadedDocument class

await doc.OpenAsync(file);

//Get first page from document

PdfLoadedPage page = doc.Pages[0] as PdfLoadedPage;

//Create PDF graphics for the page

PdfGraphics graphics = page.Graphics;

//Create a PdfGrid.

PdfGrid pdfGrid = new PdfGrid();

//Add values to list

List<object> data = new List<object>();

Object row1 = new { ID = "1", Name = "Clay" };

Object row2 = new { ID = "2", Name = "Thomas" };

data.Add(row1);

data.Add(row2);

//Add list to IEnumerable

IEnumerable<object> dataTable = data;

//Assign data source.

pdfGrid.DataSource = dataTable;

//Draw grid to the page of PDF document.

pdfGrid.Draw(graphics, new PointF(10, 10));

//Save the PDF document into stream

MemoryStream stream = new MemoryStream();

await doc.SaveAsync(stream);

//Close the document.

doc.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document

FileStream docStream = new FileStream("input.pdf", FileMode.Open, FileAccess.Read);

PdfLoadedDocument doc = new PdfLoadedDocument(docStream);

//Get first page from document

PdfLoadedPage page = doc.Pages[0] as PdfLoadedPage;

//Create PDF graphics for the page

PdfGraphics graphics = page.Graphics;

//Create a PdfGrid.

PdfGrid pdfGrid = new PdfGrid();

//Add values to list

List<object> data = new List<object>();

Object row1 = new { ID = "1", Name = "Clay" };

Object row2 = new { ID = "2", Name = "Thomas" };

data.Add(row1);

data.Add(row2);

//Add list to IEnumerable

IEnumerable<object> dataTable = data;

//Assign data source.

pdfGrid.DataSource = dataTable;

//Draw grid to the page of PDF document.

pdfGrid.Draw(graphics, new Syncfusion.Drawing.PointF(10, 10));

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the PDF document to stream.

doc.Save(stream);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document.

doc.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.pdf");

PdfLoadedDocument doc = new PdfLoadedDocument(docStream);

//Get first page from document

PdfLoadedPage page = doc.Pages[0] as PdfLoadedPage;

//Create PDF graphics for the page

PdfGraphics graphics = page.Graphics;

//Create a PdfGrid.

PdfGrid pdfGrid = new PdfGrid();

//Add values to list

List<object> data = new List<object>();

Object row1 = new { ID = "1", Name = "Clay" };

Object row2 = new { ID = "2", Name = "Thomas" };

data.Add(row1);

data.Add(row2);

//Add list to IEnumerable

IEnumerable<object> dataTable = data;

//Assign data source.

pdfGrid.DataSource = dataTable;

//Draw grid to the page of PDF document.

pdfGrid.Draw(graphics, new Syncfusion.Drawing.PointF(10, 10));

//Save the PDF document into stream

MemoryStream stream = new MemoryStream();

doc.Save(stream);

//Close the document.

doc.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

## Support for cell customization 

### Cell customization in PdfLightTable

[PdfLightTable](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTable.html) allows users to customize cell font, background, border, etc. using [PdfCellStyle](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfCellStyle.html) class.

The below code snippet illustrates how to customize the cell properties in ``PdfLightTable``.

{% tabs %}

{% highlight c# %}


//Create a new PDF document.

PdfDocument doc = new PdfDocument();

//Add a page.

PdfPage page = doc.Pages.Add();

//Create a PdfLightTable.

PdfLightTable pdfLightTable = new PdfLightTable();

//Set the DataSourceType as Direct.

pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.

pdfLightTable.Columns.Add(new PdfColumn("Roll Number"));

pdfLightTable.Columns.Add(new PdfColumn("Name"));

pdfLightTable.Columns.Add(new PdfColumn("Class"));

//Add Rows.

pdfLightTable.Rows.Add(new object[] { "111", "Maxim", "III" });

pdfLightTable.Rows.Add(new object[] { "112", "Minim", "III" });

//Create the font for setting the style.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 14);

//Declare and define the alternate style.

PdfCellStyle altStyle = new PdfCellStyle(font, PdfBrushes.White, PdfPens.Green);

altStyle.BackgroundBrush = PdfBrushes.DarkGray;

//Declare and define the header style.

PdfCellStyle headerStyle = new PdfCellStyle(font, PdfBrushes.White, PdfPens.Brown);

headerStyle.BackgroundBrush = PdfBrushes.Red;

pdfLightTable.Style.AlternateStyle = altStyle;

pdfLightTable.Style.HeaderStyle = headerStyle;

//Show header in the table

pdfLightTable.Style.ShowHeader = true;

//Draw the PdfLightTable.

pdfLightTable.Draw(page, PointF.Empty);

//Save the document.

doc.Save("Output.pdf");

//Close the document

doc.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Create a new PDF document.

Dim doc As New PdfDocument()

'Add a page.

Dim page As PdfPage = doc.Pages.Add()

'Create a PdfLightTable.

Dim pdfLightTable As New PdfLightTable()

'Set the DataSourceType as Direct.

pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect

'Create columns.

pdfLightTable.Columns.Add(New PdfColumn("Roll Number"))

pdfLightTable.Columns.Add(New PdfColumn("Name"))

pdfLightTable.Columns.Add(New PdfColumn("Class"))

'Add Rows.

pdfLightTable.Rows.Add(New Object() {"111", "Maxim", "III"})

pdfLightTable.Rows.Add(New Object() {"112", "Minim", "III"})

'Create the font for setting the style.

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 14)

'Declare and define the alternate style.

Dim altStyle As New PdfCellStyle(font, PdfBrushes.White, PdfPens.Green)

altStyle.BackgroundBrush = PdfBrushes.DarkGray

'Declare and define the header style.

Dim headerStyle As New PdfCellStyle(font, PdfBrushes.White, PdfPens.Brown)

headerStyle.BackgroundBrush = PdfBrushes.Red

pdfLightTable.Style.AlternateStyle = altStyle

pdfLightTable.Style.HeaderStyle = headerStyle

'Show the header in the table

pdfLightTable.Style.ShowHeader = True

'Draw the PdfLightTable.

pdfLightTable.Draw(page, PointF.Empty)

'Save the document.

doc.Save("Output.pdf")

'Close the document

doc.Close(True)



{% endhighlight %}

{% highlight UWP %}

//Create a new PDF document.

PdfDocument doc = new PdfDocument();

//Add a page.

PdfPage page = doc.Pages.Add();

//Create a PdfLightTable.

PdfLightTable pdfLightTable = new PdfLightTable();

//Set the DataSourceType as Direct.

pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.

pdfLightTable.Columns.Add(new PdfColumn("Roll Number"));

pdfLightTable.Columns.Add(new PdfColumn("Name"));

pdfLightTable.Columns.Add(new PdfColumn("Class"));

//Add Rows.

pdfLightTable.Rows.Add(new object[] { "111", "Maxim", "III" });

pdfLightTable.Rows.Add(new object[] { "112", "Minim", "III" });

//Create the font for setting the style.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 14);

//Declare and define the alternate style.

PdfCellStyle altStyle = new PdfCellStyle(font, PdfBrushes.White, PdfPens.Green);

altStyle.BackgroundBrush = PdfBrushes.DarkGray;

//Declare and define the header style.

PdfCellStyle headerStyle = new PdfCellStyle(font, PdfBrushes.White, PdfPens.Brown);

headerStyle.BackgroundBrush = PdfBrushes.Red;

pdfLightTable.Style.AlternateStyle = altStyle;

pdfLightTable.Style.HeaderStyle = headerStyle;

//Show header in the table

pdfLightTable.Style.ShowHeader = true;

//Draw the PdfLightTable.

pdfLightTable.Draw(page, PointF.Empty);

//Save the PDF document into stream

MemoryStream stream = new MemoryStream();

await doc.SaveAsync(stream);

//Close the document.

doc.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document.

PdfDocument doc = new PdfDocument();

//Add a page.

PdfPage page = doc.Pages.Add();

//Create a PdfLightTable.

PdfLightTable pdfLightTable = new PdfLightTable();

//Set the DataSourceType as Direct.

pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.

pdfLightTable.Columns.Add(new PdfColumn("Roll Number"));

pdfLightTable.Columns.Add(new PdfColumn("Name"));

pdfLightTable.Columns.Add(new PdfColumn("Class"));

//Add Rows.

pdfLightTable.Rows.Add(new object[] { "111", "Maxim", "III" });

pdfLightTable.Rows.Add(new object[] { "112", "Minim", "III" });

//Create the font for setting the style.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 14);

//Declare and define the alternate style.

PdfCellStyle altStyle = new PdfCellStyle(font, PdfBrushes.White, PdfPens.Green);

altStyle.BackgroundBrush = PdfBrushes.DarkGray;

//Declare and define the header style.

PdfCellStyle headerStyle = new PdfCellStyle(font, PdfBrushes.White, PdfPens.Brown);

headerStyle.BackgroundBrush = PdfBrushes.Red;

pdfLightTable.Style.AlternateStyle = altStyle;

pdfLightTable.Style.HeaderStyle = headerStyle;

//Show header in the table

pdfLightTable.Style.ShowHeader = true;

//Draw the PdfLightTable.

pdfLightTable.Draw(page, Syncfusion.Drawing.PointF.Empty);

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the PDF document to stream.

doc.Save(stream);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document.

doc.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Create a new PDF document.

PdfDocument doc = new PdfDocument();

//Add a page.

PdfPage page = doc.Pages.Add();

//Create a PdfLightTable.

PdfLightTable pdfLightTable = new PdfLightTable();

//Set the DataSourceType as Direct.

pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.

pdfLightTable.Columns.Add(new PdfColumn("Roll Number"));

pdfLightTable.Columns.Add(new PdfColumn("Name"));

pdfLightTable.Columns.Add(new PdfColumn("Class"));

//Add Rows.

pdfLightTable.Rows.Add(new object[] { "111", "Maxim", "III" });

pdfLightTable.Rows.Add(new object[] { "112", "Minim", "III" });

//Create the font for setting the style.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 14);

//Declare and define the alternate style.

PdfCellStyle altStyle = new PdfCellStyle(font, PdfBrushes.White, PdfPens.Green);

altStyle.BackgroundBrush = PdfBrushes.DarkGray;

//Declare and define the header style.

PdfCellStyle headerStyle = new PdfCellStyle(font, PdfBrushes.White, PdfPens.Brown);

headerStyle.BackgroundBrush = PdfBrushes.Red;

pdfLightTable.Style.AlternateStyle = altStyle;

pdfLightTable.Style.HeaderStyle = headerStyle;

//Show header in the table

pdfLightTable.Style.ShowHeader = true;

//Draw the PdfLightTable.

pdfLightTable.Draw(page, Syncfusion.Drawing.PointF.Empty);

//Save the PDF document into stream

MemoryStream stream = new MemoryStream();

doc.Save(stream);

//Close the document.

doc.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

You can set different styles for particular cell using [BeginCellLayout](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTable.html) and [EndCellLayout](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTable.html) events in [PdfLightTable](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTable.html) class.

The following code example illustrates how to draw the graphics elements in particular cell using these event handlers.

{% tabs %}

{% highlight c# %}

//Create a new PDF document.

PdfDocument doc = new PdfDocument();

//Add a page.

PdfPage page = doc.Pages.Add();

//Create a PdfLightTable

PdfLightTable pdfLightTable = new PdfLightTable();

//Set the DataSourceType as Direct.

pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.

pdfLightTable.Columns.Add(new PdfColumn("Roll Number"));

pdfLightTable.Columns.Add(new PdfColumn("Name"));

pdfLightTable.Columns.Add(new PdfColumn("Class"));

//Add rows.

pdfLightTable.Rows.Add(new object[] { "111", "Maxim", "III" });

pdfLightTable.Rows.Add(new object[] { "112", "Minim", "III" });

//Subscribing to events

pdfLightTable.BeginCellLayout += pdfLightTable_BeginCellLayout;

pdfLightTable.EndCellLayout+=pdfLightTable_EndCellLayout;

//Show the header.

pdfLightTable.Style.ShowHeader = true;

//Draw the PdfLightTable.

pdfLightTable.Draw(page, PointF.Empty);

//Save the document.

doc.Save("Output.pdf");

//Close the document

doc.Close(true);

private void pdfLightTable_EndCellLayout(object sender, EndCellLayoutEventArgs args)

{

if(args.RowIndex==0 &&args.CellIndex==0)

{

args.Graphics.DrawImage(new PdfBitmap(imageFileName), args.Bounds);

}

}

private void pdfLightTable_BeginCellLayout(object sender, BeginCellLayoutEventArgs args)

{

if (args.RowIndex == 0 && args.CellIndex == 1)

{

args.Graphics.DrawEllipse(PdfBrushes.Red, args.Bounds);

}

}

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim doc As New PdfDocument()

'Add a page.

Dim page As PdfPage = doc.Pages.Add()

'Declare a PdfLightTable

Dim pdfLightTable As New PdfLightTable()

'Set the DataSourceType as Direct.

pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect

'Create columns.

pdfLightTable.Columns.Add(New PdfColumn("Roll Number"))

pdfLightTable.Columns.Add(New PdfColumn("Name"))

pdfLightTable.Columns.Add(New PdfColumn("Class"))

'Add rows.

pdfLightTable.Rows.Add(New Object() {"111", "Maxim", "III"})

pdfLightTable.Rows.Add(New Object() {"112", "Minim", "III"})

'Subscribing to events

AddHandler pdfLightTable.BeginCellLayout, AddressOf pdfLightTable_BeginCellLayout

AddHandler pdfLightTable.EndCellLayout, AddressOf pdfLightTable_EndCellLayout

'Show the header.

pdfLightTable.Style.ShowHeader = True

'Draw the PdfLightTable.

pdfLightTable.Draw(page, PointF.Empty)

'Save the document.

doc.Save("Output.pdf")

'Close the document

doc.Close(True)

Private Sub pdfLightTable_EndCellLayout(ByVal sender As Object, ByVal args As EndCellLayoutEventArgs)

If args.RowIndex = 0 AndAlso args.CellIndex = 0 Then

args.Graphics.DrawImage(New PdfBitmap(imageFileName), args.Bounds)

End If

End Sub

Private Sub pdfLightTable_BeginCellLayout(ByVal sender As Object, ByVal args As BeginCellLayoutEventArgs)

If args.RowIndex = 0 AndAlso args.CellIndex = 1 Then

args.Graphics.DrawEllipse(PdfBrushes.Red, args.Bounds)

End If

End Sub

{% endhighlight %}

{% highlight UWP %}

//Create a new PDF document.

PdfDocument doc = new PdfDocument();

//Add a page.

PdfPage page = doc.Pages.Add();

//Create a PdfLightTable

PdfLightTable pdfLightTable = new PdfLightTable();

//Set the DataSourceType as Direct.

pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.

pdfLightTable.Columns.Add(new PdfColumn("Roll Number"));

pdfLightTable.Columns.Add(new PdfColumn("Name"));

pdfLightTable.Columns.Add(new PdfColumn("Class"));

//Add rows.

pdfLightTable.Rows.Add(new object[] { "111", "Maxim", "III" });

pdfLightTable.Rows.Add(new object[] { "112", "Minim", "III" });

//Subscribing to events

pdfLightTable.BeginCellLayout += pdfLightTable_BeginCellLayout;

pdfLightTable.EndCellLayout += pdfLightTable_EndCellLayout;

//Show the header.

pdfLightTable.Style.ShowHeader = true;

//Draw the PdfLightTable.

pdfLightTable.Draw(page, PointF.Empty);

//Save the PDF document into stream

MemoryStream stream = new MemoryStream();

await doc.SaveAsync(stream);

//Close the document.

doc.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Output.pdf");

private void pdfLightTable_EndCellLayout(object sender, EndCellLayoutEventArgs args)

{

    if (args.RowIndex == 0 && args.CellIndex == 0)

    {
        //Load the PDF document as stream

        Stream imageStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Image.jpg");

        args.Graphics.DrawImage(new PdfBitmap(imageStream), args.Bounds);

    }

}

private void pdfLightTable_BeginCellLayout(object sender, BeginCellLayoutEventArgs args)

{

    if (args.RowIndex == 0 && args.CellIndex == 1)

    {

        args.Graphics.DrawEllipse(PdfBrushes.Red, args.Bounds);

    }

}


{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document.

PdfDocument doc = new PdfDocument();

//Add a page.

PdfPage page = doc.Pages.Add();

//Create a PdfLightTable

PdfLightTable pdfLightTable = new PdfLightTable();

//Set the DataSourceType as Direct.

pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.

pdfLightTable.Columns.Add(new PdfColumn("Roll Number"));

pdfLightTable.Columns.Add(new PdfColumn("Name"));

pdfLightTable.Columns.Add(new PdfColumn("Class"));

//Add rows.

pdfLightTable.Rows.Add(new object[] { "111", "Maxim", "III" });

pdfLightTable.Rows.Add(new object[] { "112", "Minim", "III" });

//Subscribing to events

pdfLightTable.BeginCellLayout += pdfLightTable_BeginCellLayout;

pdfLightTable.EndCellLayout += pdfLightTable_EndCellLayout;

//Show the header.

pdfLightTable.Style.ShowHeader = true;

//Draw the PdfLightTable.

pdfLightTable.Draw(page, Syncfusion.Drawing.PointF.Empty);

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the PDF document to stream.

doc.Save(stream);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document.

doc.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

private void pdfLightTable_EndCellLayout(object sender, EndCellLayoutEventArgs args)

{

    if (args.RowIndex == 0 && args.CellIndex == 0)

    {
        //Load the image as stream

        FileStream imageStream = new FileStream("Image.jpg", FileMode.Open, FileAccess.Read);

        args.Graphics.DrawImage(new PdfBitmap(imageStream), args.Bounds);

    }

}

private void pdfLightTable_BeginCellLayout(object sender, BeginCellLayoutEventArgs args)

{

    if (args.RowIndex == 0 && args.CellIndex == 1)

    {

        args.Graphics.DrawEllipse(PdfBrushes.Red, args.Bounds);

    }

}


{% endhighlight %}

{% highlight Xamarin %}

//Create a new PDF document.

PdfDocument doc = new PdfDocument();

//Add a page.

PdfPage page = doc.Pages.Add();

//Create a PdfLightTable

PdfLightTable pdfLightTable = new PdfLightTable();

//Set the DataSourceType as Direct.

pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.

pdfLightTable.Columns.Add(new PdfColumn("Roll Number"));

pdfLightTable.Columns.Add(new PdfColumn("Name"));

pdfLightTable.Columns.Add(new PdfColumn("Class"));

//Add rows.

pdfLightTable.Rows.Add(new object[] { "111", "Maxim", "III" });

pdfLightTable.Rows.Add(new object[] { "112", "Minim", "III" });

//Subscribing to events

pdfLightTable.BeginCellLayout += pdfLightTable_BeginCellLayout;

pdfLightTable.EndCellLayout += pdfLightTable_EndCellLayout;

//Show the header.

pdfLightTable.Style.ShowHeader = true;

//Draw the PdfLightTable.

pdfLightTable.Draw(page, Syncfusion.Drawing.PointF.Empty);

//Save the PDF document into stream

MemoryStream stream = new MemoryStream();

doc.Save(stream);

//Close the document.

doc.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

private void pdfLightTable_EndCellLayout(object sender, EndCellLayoutEventArgs args)

{

    if (args.RowIndex == 0 && args.CellIndex == 0)

    {
        //Load the image as stream

        Stream imageStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Image.jpg");

        args.Graphics.DrawImage(new PdfBitmap(imageStream), args.Bounds);

    }

}

private void pdfLightTable_BeginCellLayout(object sender, BeginCellLayoutEventArgs args)

{

    if (args.RowIndex == 0 && args.CellIndex == 1)

    {

        args.Graphics.DrawEllipse(PdfBrushes.Red, args.Bounds);

    }

}


{% endhighlight %}

{% endtabs %}

### Cell customization in PdfGrid

[PdfGridCell](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGridCell.html) provides various direct options to customize cells like [ColumnSpan](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGridCell.html#Syncfusion_Pdf_Grid_PdfGridCell_ColumnSpan), [RowSpan](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGridCell.html#Syncfusion_Pdf_Grid_PdfGridCell_RowSpan), text color, background color, and etc.

The following code example illustrates you how to customize the cell in [PdfGrid](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGrid.html).

{% tabs %}

{% highlight c# %}

//Create a new PDF document.

PdfDocument pdfDocument = new PdfDocument();

//Create the page

PdfPage pdfPage = pdfDocument.Pages.Add();

//Create the parent grid

PdfGrid parentPdfGrid = new PdfGrid();

//Add the rows

PdfGridRow row1 = parentPdfGrid.Rows.Add();

PdfGridRow row2 = parentPdfGrid.Rows.Add();

row2.Height = 58;

//Add the columns

parentPdfGrid.Columns.Add(3);

//Set the value to the specific cell.

parentPdfGrid.Rows[0].Cells[0].Value = "Nested Table";

parentPdfGrid.Rows[0].Cells[1].RowSpan = 2;

parentPdfGrid.Rows[0].Cells[1].ColumnSpan = 2;

//Create the child table

PdfGrid childPdfGrid = new PdfGrid();

//Set the column and rows for child grid

childPdfGrid.Columns.Add(5);

for (int i = 0; i < 5; i++)

{

PdfGridRow row = childPdfGrid.Rows.Add();

for (int j = 0; j < 5; j++)

{

row.Cells[j].Value = String.Format("Cell [{0} {1}]", j, i);

}

}

//Set the value as another PdfGrid in a cell.

parentPdfGrid.Rows[0].Cells[1].Value = childPdfGrid;

//Specify the style for the PdfGridCell.

PdfGridCellStyle pdfGridCellStyle = new PdfGridCellStyle();

pdfGridCellStyle.TextPen = PdfPens.Red;

pdfGridCellStyle.Borders.All = PdfPens.Red;

pdfGridCellStyle.BackgroundImage = new PdfBitmap(imagePath);

PdfGridCell pdfGridCell = parentPdfGrid.Rows[0].Cells[0];

//Apply style

pdfGridCell.Style = pdfGridCellStyle;

//Set image position for the background image in the style.

pdfGridCell.ImagePosition = PdfGridImagePosition.Fit;

//Draw the PdfGrid.

parentPdfGrid.Draw(pdfPage, PointF.Empty);

//Save the document.

pdfDocument.Save("Output.pdf");

//close the document

pdfDocument.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim pdfDocument As New PdfDocument()

'Create the page

Dim pdfPage As PdfPage = pdfDocument.Pages.Add()

'Create the parent grid

Dim parentPdfGrid As New PdfGrid()

'Add the rows

Dim row1 As PdfGridRow = parentPdfGrid.Rows.Add()

Dim row2 As PdfGridRow = parentPdfGrid.Rows.Add()

row2.Height = 58

'Add the columns

parentPdfGrid.Columns.Add(3)

'Set the value to the specific cell.

parentPdfGrid.Rows(0).Cells(0).Value = "Nested Table"

parentPdfGrid.Rows(0).Cells(1).RowSpan = 2

parentPdfGrid.Rows(0).Cells(1).ColumnSpan = 2

'Create the child table

Dim childPdfGrid As New PdfGrid()

'Set the column and rows for child grid

childPdfGrid.Columns.Add(5)

For i As Integer = 0 To 4

Dim row As PdfGridRow = childPdfGrid.Rows.Add()

For j As Integer = 0 To 4

row.Cells(j).Value = String.Format("Cell [{0} {1}]", j, i)

Next j

Next i

'Set the value as another PdfGrid in a cell.

parentPdfGrid.Rows(0).Cells(1).Value = childPdfGrid

'Specify the style for the PdfGridCell.

Dim pdfGridCellStyle As New PdfGridCellStyle()

pdfGridCellStyle.TextPen = PdfPens.Red

pdfGridCellStyle.Borders.All = PdfPens.Red

pdfGridCellStyle.BackgroundImage = New PdfBitmap(imageFileName)

Dim pdfGridCell As PdfGridCell = parentPdfGrid.Rows(0).Cells(0)

'Apply style

pdfGridCell.Style = pdfGridCellStyle

'Set image position for the background image in the style.

pdfGridCell.ImagePosition = PdfGridImagePosition.Fit

'Draw the PdfGrid.

parentPdfGrid.Draw(pdfPage, PointF.Empty)

'Save the document.

pdfDocument.Save("Output.pdf")

'close the document

pdfDocument.Close(True)

{% endhighlight %}

{% highlight UWP %}

//Create a new PDF document.

PdfDocument pdfDocument = new PdfDocument();

//Create the page

PdfPage pdfPage = pdfDocument.Pages.Add();

//Create the parent grid

PdfGrid parentPdfGrid = new PdfGrid();

//Add the rows

PdfGridRow row1 = parentPdfGrid.Rows.Add();

PdfGridRow row2 = parentPdfGrid.Rows.Add();

row2.Height = 58;

//Add the columns

parentPdfGrid.Columns.Add(3);

//Set the value to the specific cell.

parentPdfGrid.Rows[0].Cells[0].Value = "Nested Table";

parentPdfGrid.Rows[0].Cells[1].RowSpan = 2;

parentPdfGrid.Rows[0].Cells[1].ColumnSpan = 2;

//Create the child table

PdfGrid childPdfGrid = new PdfGrid();

//Set the column and rows for child grid

childPdfGrid.Columns.Add(5);

for (int i = 0; i < 5; i++)

{

    PdfGridRow row = childPdfGrid.Rows.Add();

    for (int j = 0; j < 5; j++)

    {

        row.Cells[j].Value = String.Format("Cell [{0} {1}]", j, i);

    }

}

//Set the value as another PdfGrid in a cell.

parentPdfGrid.Rows[0].Cells[1].Value = childPdfGrid;

//Specify the style for the PdfGridCell.

PdfGridCellStyle pdfGridCellStyle = new PdfGridCellStyle();

pdfGridCellStyle.TextPen = PdfPens.Red;

pdfGridCellStyle.Borders.All = PdfPens.Red;

//Load the image as stream

Stream imageStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Data.Image.jpg");

pdfGridCellStyle.BackgroundImage = new PdfBitmap(imageStream);

PdfGridCell pdfGridCell = parentPdfGrid.Rows[0].Cells[0];

//Apply style

pdfGridCell.Style = pdfGridCellStyle;

//Set image position for the background image in the style.

pdfGridCell.ImagePosition = PdfGridImagePosition.Fit;

//Draw the PdfGrid.

parentPdfGrid.Draw(pdfPage, PointF.Empty);

//Save the PDF document into stream

MemoryStream stream = new MemoryStream();

await pdfDocument.SaveAsync(stream);

//Close the document.

pdfDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document.

PdfDocument pdfDocument = new PdfDocument();

//Create the page

PdfPage pdfPage = pdfDocument.Pages.Add();

//Create the parent grid

PdfGrid parentPdfGrid = new PdfGrid();

//Add the rows

PdfGridRow row1 = parentPdfGrid.Rows.Add();

PdfGridRow row2 = parentPdfGrid.Rows.Add();

row2.Height = 58;

//Add the columns

parentPdfGrid.Columns.Add(3);

//Set the value to the specific cell.

parentPdfGrid.Rows[0].Cells[0].Value = "Nested Table";

parentPdfGrid.Rows[0].Cells[1].RowSpan = 2;

parentPdfGrid.Rows[0].Cells[1].ColumnSpan = 2;

//Create the child table

PdfGrid childPdfGrid = new PdfGrid();

//Set the column and rows for child grid

childPdfGrid.Columns.Add(5);

for (int i = 0; i < 5; i++)

{

    PdfGridRow row = childPdfGrid.Rows.Add();

    for (int j = 0; j < 5; j++)

    {

        row.Cells[j].Value = String.Format("Cell [{0} {1}]", j, i);

    }

}

//Set the value as another PdfGrid in a cell.

parentPdfGrid.Rows[0].Cells[1].Value = childPdfGrid;

//Specify the style for the PdfGridCell.

PdfGridCellStyle pdfGridCellStyle = new PdfGridCellStyle();

pdfGridCellStyle.TextPen = PdfPens.Red;

pdfGridCellStyle.Borders.All = PdfPens.Red;

//Load image as stream

FileStream imageStream = new FileStream("Image.jpg", FileMode.Open, FileAccess.Read);

pdfGridCellStyle.BackgroundImage = new PdfBitmap(imageStream);

PdfGridCell pdfGridCell = parentPdfGrid.Rows[0].Cells[0];

//Apply style

pdfGridCell.Style = pdfGridCellStyle;

//Set image position for the background image in the style.

pdfGridCell.ImagePosition = PdfGridImagePosition.Fit;

//Draw the PdfGrid.

parentPdfGrid.Draw(pdfPage, Syncfusion.Drawing.PointF.Empty);

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the PDF document to stream.

pdfDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document.

pdfDocument.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Create a new PDF document.

PdfDocument pdfDocument = new PdfDocument();

//Create the page

PdfPage pdfPage = pdfDocument.Pages.Add();

//Create the parent grid

PdfGrid parentPdfGrid = new PdfGrid();

//Add the rows

PdfGridRow row1 = parentPdfGrid.Rows.Add();

PdfGridRow row2 = parentPdfGrid.Rows.Add();

row2.Height = 58;

//Add the columns

parentPdfGrid.Columns.Add(3);

//Set the value to the specific cell.

parentPdfGrid.Rows[0].Cells[0].Value = "Nested Table";

parentPdfGrid.Rows[0].Cells[1].RowSpan = 2;

parentPdfGrid.Rows[0].Cells[1].ColumnSpan = 2;

//Create the child table

PdfGrid childPdfGrid = new PdfGrid();

//Set the column and rows for child grid

childPdfGrid.Columns.Add(5);

for (int i = 0; i < 5; i++)

{

    PdfGridRow row = childPdfGrid.Rows.Add();

    for (int j = 0; j < 5; j++)

    {

        row.Cells[j].Value = String.Format("Cell [{0} {1}]", j, i);

    }

}

//Set the value as another PdfGrid in a cell.

parentPdfGrid.Rows[0].Cells[1].Value = childPdfGrid;

//Specify the style for the PdfGridCell.

PdfGridCellStyle pdfGridCellStyle = new PdfGridCellStyle();

pdfGridCellStyle.TextPen = PdfPens.Red;

pdfGridCellStyle.Borders.All = PdfPens.Red;

Stream imageStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Image.jpg");

pdfGridCellStyle.BackgroundImage = new PdfBitmap(imageStream);

PdfGridCell pdfGridCell = parentPdfGrid.Rows[0].Cells[0];

//Apply style

pdfGridCell.Style = pdfGridCellStyle;

//Set image position for the background image in the style.

pdfGridCell.ImagePosition = PdfGridImagePosition.Fit;

//Draw the PdfGrid.

parentPdfGrid.Draw(pdfPage, Syncfusion.Drawing.PointF.Empty);

//Save the PDF document into stream

MemoryStream stream = new MemoryStream();

pdfDocument.Save(stream);

//Close the document.

pdfDocument.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

## Support for rows and columns customization

### Row customization in PdfLightTable

[PdfLightTable](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTable.html) doesn’t provide direct support for row customizations. However, this can be done through the event handlers.The following code snippet illustrates how to customize the row in ``PdfLightTable`` using [BeginRowLayout](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTable.html) and [EndRowLayout](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTable.html) event handlers.

{% tabs %}

{% highlight c# %}

//Create a new PDF document.

PdfDocument doc = new PdfDocument();

//Add a page.

PdfPage page = doc.Pages.Add();

//Create a PdfLightTable

PdfLightTable pdfLightTable = new PdfLightTable();

//Set the DataSourceType as Direct.

pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.

pdfLightTable.Columns.Add(new PdfColumn("Roll Number"));

pdfLightTable.Columns.Add(new PdfColumn("Name"));

pdfLightTable.Columns.Add(new PdfColumn("Class"));

//Add rows.

pdfLightTable.Rows.Add(new object[] { "111", "Maxim", "III" });

pdfLightTable.Rows.Add(new object[] { "112", "Minim", "III" });

pdfLightTable.Rows.Add(new object[] { "113", "john", "III" });

pdfLightTable.Rows.Add(new object[] { "114", "peter", "III" });

//Subscribing to events

pdfLightTable.BeginRowLayout+=pdfLightTable_BeginRowLayout;

pdfLightTable.EndRowLayout+=pdfLightTable_EndRowLayout;

//Draw the PdfLightTable.

pdfLightTable.Draw(page, PointF.Empty);

//Save the document.

doc.Save("Output.pdf");

//Close the document

doc.Close(true);

private void pdfLightTable_EndRowLayout(object sender, EndRowLayoutEventArgs args)

{

//Customize the rows when row layout ends

if (args.RowIndex == 3)

args.Cancel = true;

}

private void pdfLightTable_BeginRowLayout(object sender, BeginRowLayoutEventArgs args)

{

//Apply column span

if(args.RowIndex==1)

{

PdfLightTable table = (PdfLightTable)sender;

int count = table.Columns.Count;

int[] spanMap = new int[count];

// Set just spanned cells. Negative values are not allowed.

spanMap[0] = 2;

spanMap[1] = 3;

args.ColumnSpanMap = spanMap;

}

}

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim doc As New PdfDocument()

'Add a page.

Dim page As PdfPage = doc.Pages.Add()

'Create a PdfLightTable

Dim pdfLightTable As New PdfLightTable()

'Set the DataSourceType as Direct.

pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect

'Create columns.

pdfLightTable.Columns.Add(New PdfColumn("Roll Number"))

pdfLightTable.Columns.Add(New PdfColumn("Name"))

pdfLightTable.Columns.Add(New PdfColumn("Class"))

'Add rows.

pdfLightTable.Rows.Add(New Object() { "111", "Maxim", "III" })

pdfLightTable.Rows.Add(New Object() { "112", "Minim", "III" })

pdfLightTable.Rows.Add(New Object() { "113", "john", "III" })

pdfLightTable.Rows.Add(New Object() { "114", "peter", "III" })

'Subscribing to events

AddHandler pdfLightTable.BeginRowLayout, AddressOf pdfLightTable_BeginRowLayout

AddHandler pdfLightTable.EndRowLayout, AddressOf pdfLightTable_EndRowLayout

'Draw the PdfLightTable.

pdfLightTable.Draw(page, PointF.Empty)

'Save the document.

doc.Save("Output.pdf")

'Close the document

doc.Close(True)

Private Sub pdfLightTable_EndRowLayout(ByVal sender As Object, ByVal args As EndRowLayoutEventArgs)

'Customize the rows when row layout ends

If args.RowIndex = 3 Then

args.Cancel = True

End If

End Sub

Private Sub pdfLightTable_BeginRowLayout(ByVal sender As Object, ByVal args As BeginRowLayoutEventArgs)

'Apply column span

If args.RowIndex=1 Then

Dim table As PdfLightTable = CType(sender, PdfLightTable)

Dim count As Integer = table.Columns.Count

Dim spanMap(count - 1) As Integer

' Set just spanned cells. Negative values are not allowed.

spanMap(0) = 2

spanMap(1) = 3

args.ColumnSpanMap = spanMap

End If

End Sub

{% endhighlight %}

{% highlight UWP %}

//Create a new PDF document.

PdfDocument doc = new PdfDocument();

//Add a page.

PdfPage page = doc.Pages.Add();

//Create a PdfLightTable

PdfLightTable pdfLightTable = new PdfLightTable();

//Set the DataSourceType as Direct.

pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.

pdfLightTable.Columns.Add(new PdfColumn("Roll Number"));

pdfLightTable.Columns.Add(new PdfColumn("Name"));

pdfLightTable.Columns.Add(new PdfColumn("Class"));

//Add rows.

pdfLightTable.Rows.Add(new object[] { "111", "Maxim", "III" });

pdfLightTable.Rows.Add(new object[] { "112", "Minim", "III" });

pdfLightTable.Rows.Add(new object[] { "113", "john", "III" });

pdfLightTable.Rows.Add(new object[] { "114", "peter", "III" });

//Subscribing to events

pdfLightTable.BeginRowLayout += pdfLightTable_BeginRowLayout;

pdfLightTable.EndRowLayout += pdfLightTable_EndRowLayout;

//Draw the PdfLightTable.

pdfLightTable.Draw(page, PointF.Empty);

//Save the PDF document into stream

MemoryStream stream = new MemoryStream();

await doc.SaveAsync(stream);

//Close the document.

doc.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Output.pdf");

private void pdfLightTable_EndRowLayout(object sender, EndRowLayoutEventArgs args)

{

    //Customize the rows when row layout ends

    if (args.RowIndex == 3)

    args.Cancel = true;

}

private void pdfLightTable_BeginRowLayout(object sender, BeginRowLayoutEventArgs args)

{

    //Apply column span

    if (args.RowIndex == 1)

    {

        PdfLightTable table = (PdfLightTable)sender;

        int count = table.Columns.Count;

        int[] spanMap = new int[count];

        // Set just spanned cells. Negative values are not allowed.

        spanMap[0] = 2;

        spanMap[1] = 3;

        args.ColumnSpanMap = spanMap;

    }

}


{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document.

PdfDocument doc = new PdfDocument();

//Add a page.

PdfPage page = doc.Pages.Add();

//Create a PdfLightTable

PdfLightTable pdfLightTable = new PdfLightTable();

//Set the DataSourceType as Direct.

pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.

pdfLightTable.Columns.Add(new PdfColumn("Roll Number"));

pdfLightTable.Columns.Add(new PdfColumn("Name"));

pdfLightTable.Columns.Add(new PdfColumn("Class"));

//Add rows.

pdfLightTable.Rows.Add(new object[] { "111", "Maxim", "III" });

pdfLightTable.Rows.Add(new object[] { "112", "Minim", "III" });

pdfLightTable.Rows.Add(new object[] { "113", "john", "III" });

pdfLightTable.Rows.Add(new object[] { "114", "peter", "III" });

//Subscribing to events

pdfLightTable.BeginRowLayout += pdfLightTable_BeginRowLayout;

pdfLightTable.EndRowLayout += pdfLightTable_EndRowLayout;

//Draw the PdfLightTable.

pdfLightTable.Draw(page, Syncfusion.Drawing.PointF.Empty);

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the PDF document to stream.

doc.Save(stream);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document.

doc.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

private void pdfLightTable_EndRowLayout(object sender, EndRowLayoutEventArgs args)

{

    //Customize the rows when row layout ends

    if (args.RowIndex == 3)

    args.Cancel = true;

}

private void pdfLightTable_BeginRowLayout(object sender, BeginRowLayoutEventArgs args)

{

    //Apply column span

    if (args.RowIndex == 1)

    {

        PdfLightTable table = (PdfLightTable)sender;

        int count = table.Columns.Count;

        int[] spanMap = new int[count];

        // Set just spanned cells. Negative values are not allowed.

        spanMap[0] = 2;

        spanMap[1] = 3;

        args.ColumnSpanMap = spanMap;

    }

}


{% endhighlight %}

{% highlight Xamarin %}

//Create a new PDF document.

PdfDocument doc = new PdfDocument();

//Add a page.

PdfPage page = doc.Pages.Add();

//Create a PdfLightTable

PdfLightTable pdfLightTable = new PdfLightTable();

//Set the DataSourceType as Direct.

pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.

pdfLightTable.Columns.Add(new PdfColumn("Roll Number"));

pdfLightTable.Columns.Add(new PdfColumn("Name"));

pdfLightTable.Columns.Add(new PdfColumn("Class"));

//Add rows.

pdfLightTable.Rows.Add(new object[] { "111", "Maxim", "III" });

pdfLightTable.Rows.Add(new object[] { "112", "Minim", "III" });

pdfLightTable.Rows.Add(new object[] { "113", "john", "III" });

pdfLightTable.Rows.Add(new object[] { "114", "peter", "III" });

//Subscribing to events

pdfLightTable.BeginRowLayout += pdfLightTable_BeginRowLayout;

pdfLightTable.EndRowLayout += pdfLightTable_EndRowLayout;

//Draw the PdfLightTable.

pdfLightTable.Draw(page, Syncfusion.Drawing.PointF.Empty);

//Save the PDF document into stream

MemoryStream stream = new MemoryStream();

doc.Save(stream);

//Close the document.

doc.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

### Column customization in PdfLightTable

The following code snippet illustrates how to customize the column in [PdfLightTable](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTable.html) using the [PdfStringFormat](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfStringFormat.html) class.

{% tabs %}

{% highlight c# %}

//Create a new PDF document.

PdfDocument doc = new PdfDocument();

//Add a page.

PdfPage page = doc.Pages.Add();

//Acquire page's graphics.

PdfGraphics graphics = page.Graphics;

//Create a PdfLightTable.

PdfLightTable pdfLightTable = new PdfLightTable();

//Set the DataSourceType as Direct.

pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.

pdfLightTable.Columns.Add(new PdfColumn("Roll Number"));

pdfLightTable.Columns.Add(new PdfColumn("Name"));

pdfLightTable.Columns.Add(new PdfColumn("Class"));

//Add rows.

pdfLightTable.Rows.Add(new object[] { "111", "john", "III" });

// Specify column name.

pdfLightTable.Columns[1].ColumnName = "Student Name";

//create and customize the string formats

PdfStringFormat format = new PdfStringFormat();

format.Alignment = PdfTextAlignment.Center;

format.LineAlignment = PdfVerticalAlignment.Bottom;

//Apply string format

pdfLightTable.Columns[0].StringFormat = format;

//Style to display header.

pdfLightTable.Style.ShowHeader = true;

//Draw the PdfLightTable.

pdfLightTable.Draw(page, PointF.Empty);

//Save the document.

doc.Save("Output.pdf");

//close the document

doc.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim doc As New PdfDocument()

'Add a page.

Dim page As PdfPage = doc.Pages.Add()

'Acquire page's graphics.

Dim graphics As PdfGraphics = page.Graphics

'Create a PdfLightTable.

Dim pdfLightTable As New PdfLightTable()

'Set the DataSourceType as Direct.

pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect

'Create columns.

pdfLightTable.Columns.Add(New PdfColumn("Roll Number"))

pdfLightTable.Columns.Add(New PdfColumn("Name"))

pdfLightTable.Columns.Add(New PdfColumn("Class"))

'Add rows.

pdfLightTable.Rows.Add(New Object() { "111", "john", "III" })

' Specify column name.

pdfLightTable.Columns(1).ColumnName = "Student Name"

'create and customize the string format

Dim format As New PdfStringFormat()

format.Alignment = PdfTextAlignment.Center

format.LineAlignment = PdfVerticalAlignment.Bottom

'Apply string format

pdfLightTable.Columns(0).StringFormat = format

'Style to display header.

pdfLightTable.Style.ShowHeader = True

'Draw the PdfLightTable.

pdfLightTable.Draw(page, PointF.Empty)

'Save the document.

doc.Save("Output.pdf")

'close the document

doc.Close(True)

{% endhighlight %}

{% highlight UWP %}

//Create a new PDF document.

PdfDocument doc = new PdfDocument();

//Add a page.

PdfPage page = doc.Pages.Add();

//Acquire page's graphics.

PdfGraphics graphics = page.Graphics;

//Create a PdfLightTable.

PdfLightTable pdfLightTable = new PdfLightTable();

//Set the DataSourceType as Direct.

pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.

pdfLightTable.Columns.Add(new PdfColumn("Roll Number"));

pdfLightTable.Columns.Add(new PdfColumn("Name"));

pdfLightTable.Columns.Add(new PdfColumn("Class"));

//Add rows.

pdfLightTable.Rows.Add(new object[] { "111", "john", "III" });

// Specify column name.

pdfLightTable.Columns[1].ColumnName = "Student Name";

//create and customize the string formats

PdfStringFormat format = new PdfStringFormat();

format.Alignment = PdfTextAlignment.Center;

format.LineAlignment = PdfVerticalAlignment.Bottom;

//Apply string format

pdfLightTable.Columns[0].StringFormat = format;

//Style to display header.

pdfLightTable.Style.ShowHeader = true;

//Draw the PdfLightTable.

pdfLightTable.Draw(page, PointF.Empty);

//Save the PDF document into stream

MemoryStream stream = new MemoryStream();

await doc.SaveAsync(stream);

//Close the document.

doc.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document.

PdfDocument doc = new PdfDocument();

//Add a page.

PdfPage page = doc.Pages.Add();

//Acquire page's graphics.

PdfGraphics graphics = page.Graphics;

//Create a PdfLightTable.

PdfLightTable pdfLightTable = new PdfLightTable();

//Set the DataSourceType as Direct.

pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.

pdfLightTable.Columns.Add(new PdfColumn("Roll Number"));

pdfLightTable.Columns.Add(new PdfColumn("Name"));

pdfLightTable.Columns.Add(new PdfColumn("Class"));

//Add rows.

pdfLightTable.Rows.Add(new object[] { "111", "john", "III" });

// Specify column name.

pdfLightTable.Columns[1].ColumnName = "Student Name";

//create and customize the string formats

PdfStringFormat format = new PdfStringFormat();

format.Alignment = PdfTextAlignment.Center;

format.LineAlignment = PdfVerticalAlignment.Bottom;

//Apply string format

pdfLightTable.Columns[0].StringFormat = format;

//Style to display header.

pdfLightTable.Style.ShowHeader = true;

//Draw the PdfLightTable.

pdfLightTable.Draw(page, Syncfusion.Drawing.PointF.Empty);

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the PDF document to stream.

doc.Save(stream);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document.

doc.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Create a new PDF document.

PdfDocument doc = new PdfDocument();

//Add a page.

PdfPage page = doc.Pages.Add();

//Acquire page's graphics.

PdfGraphics graphics = page.Graphics;

//Create a PdfLightTable.

PdfLightTable pdfLightTable = new PdfLightTable();

//Set the DataSourceType as Direct.

pdfLightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns.

pdfLightTable.Columns.Add(new PdfColumn("Roll Number"));

pdfLightTable.Columns.Add(new PdfColumn("Name"));

pdfLightTable.Columns.Add(new PdfColumn("Class"));

//Add rows.

pdfLightTable.Rows.Add(new object[] { "111", "john", "III" });

// Specify column name.

pdfLightTable.Columns[1].ColumnName = "Student Name";

//create and customize the string formats

PdfStringFormat format = new PdfStringFormat();

format.Alignment = PdfTextAlignment.Center;

format.LineAlignment = PdfVerticalAlignment.Bottom;

//Apply string format

pdfLightTable.Columns[0].StringFormat = format;

//Style to display header.

pdfLightTable.Style.ShowHeader = true;

//Draw the PdfLightTable.

pdfLightTable.Draw(page, Syncfusion.Drawing.PointF.Empty);

//Save the PDF document into stream

MemoryStream stream = new MemoryStream();

doc.Save(stream);

//Close the document.

doc.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

### Row customization in PdfGrid 

You can customize row height and styles using [Rows](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGrid.html#Syncfusion_Pdf_Grid_PdfGrid_Rows) property in [PdfGrid](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGrid.html) class.

The following code snippet illustrates how to customize the row in ``PdfGrid``.

{% tabs %}

{% highlight c# %}

//Create a new PDF document.

PdfDocument pdfDocument = new PdfDocument();

PdfPage pdfPage = pdfDocument.Pages.Add();

//Create a new PdfGrid.

PdfGrid pdfGrid = new PdfGrid();

//Create a DataTable.

DataTable dataTable = new DataTable();

//Add columns to the DataTable.

dataTable.Columns.Add("ID");

dataTable.Columns.Add("Name");

//Add rows to the DataTable.

dataTable.Rows.Add(new object[] { "E01", "John" });

dataTable.Rows.Add(new object[] { "E02", "Thomas" });

dataTable.Rows.Add(new object[] { "E03", "Peter" });

//Assign data source.

pdfGrid.DataSource = dataTable;

//Create an instance of PdfGridRowStyle

PdfGridRowStyle pdfGridRowStyle = new PdfGridRowStyle();

pdfGridRowStyle.BackgroundBrush = PdfBrushes.LightYellow;

pdfGridRowStyle.Font = new PdfStandardFont(PdfFontFamily.Courier, 10);

pdfGridRowStyle.TextBrush = PdfBrushes.Blue;

pdfGridRowStyle.TextPen = PdfPens.Pink;

//Set the height

pdfGrid.Rows[2].Height = 50;

//Set style for the PdfGridRow.

pdfGrid.Rows[0].Style = pdfGridRowStyle;

//Draw the PdfGrid.

PdfGridLayoutResult result = pdfGrid.Draw(pdfPage, PointF.Empty);

//Save the document.

pdfDocument.Save("Output.pdf");

//close the document

pdfDocument.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim pdfDocument As New PdfDocument()

Dim pdfPage As PdfPage = pdfDocument.Pages.Add()

'Create a new PdfGrid.

Dim pdfGrid As New PdfGrid()

'Create a DataTable.

Dim dataTable As New DataTable()

'Add columns to the DataTable.

dataTable.Columns.Add("ID")

dataTable.Columns.Add("Name")

'Add rows to the DataTable.

dataTable.Rows.Add(New Object() {"E01", "John"})

dataTable.Rows.Add(New Object() {"E02", "Thomas"})

dataTable.Rows.Add(New Object() {"E03", "Peter"})

'Assign data source.

pdfGrid.DataSource = dataTable

'Create an instance of PdfGridRowStyle

Dim pdfGridRowStyle As New PdfGridRowStyle()

pdfGridRowStyle.BackgroundBrush = PdfBrushes.LightYellow

pdfGridRowStyle.Font = New PdfStandardFont(PdfFontFamily.Courier, 10)

pdfGridRowStyle.TextBrush = PdfBrushes.Blue

pdfGridRowStyle.TextPen = PdfPens.Pink

'Set the height

pdfGrid.Rows(2).Height = 50

'Set style for the PdfGridRow.

pdfGrid.Rows(0).Style = pdfGridRowStyle

'Draw the PdfGrid.

Dim result As PdfGridLayoutResult = pdfGrid.Draw(pdfPage, PointF.Empty)

'Save the document.

pdfDocument.Save("Output.pdf")

'close the document

pdfDocument.Close(True)

{% endhighlight %}

{% highlight UWP %}

//Create a new PDF document.

PdfDocument pdfDocument = new PdfDocument();

PdfPage pdfPage = pdfDocument.Pages.Add();

//Create a new PdfGrid.

PdfGrid pdfGrid = new PdfGrid();

//Add values to list

List<object> data = new List<object>();

Object row1 = new { ID = "E01", Name = "John" };

Object row2 = new { ID = "E02", Name = "Thomas" };

Object row3 = new { ID = "E03", Name = "Peter" };

data.Add(row1);

data.Add(row2);

data.Add(row3);

//Add list to IEnumerable

IEnumerable<object> dataTable = data;

//Assign data source.

pdfGrid.DataSource = dataTable;

//Create an instance of PdfGridRowStyle

PdfGridRowStyle pdfGridRowStyle = new PdfGridRowStyle();

pdfGridRowStyle.BackgroundBrush = PdfBrushes.LightYellow;

pdfGridRowStyle.Font = new PdfStandardFont(PdfFontFamily.Courier, 10);

pdfGridRowStyle.TextBrush = PdfBrushes.Blue;

pdfGridRowStyle.TextPen = PdfPens.Pink;

//Set the height

pdfGrid.Rows[2].Height = 50;

//Set style for the PdfGridRow.

pdfGrid.Rows[0].Style = pdfGridRowStyle;

//Draw the PdfGrid.

PdfGridLayoutResult result = pdfGrid.Draw(pdfPage, PointF.Empty);

//Save the PDF document into stream

MemoryStream stream = new MemoryStream();

await pdfDocument.SaveAsync(stream);

//Close the document.

pdfDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document.

PdfDocument pdfDocument = new PdfDocument();

PdfPage pdfPage = pdfDocument.Pages.Add();

//Create a new PdfGrid.

PdfGrid pdfGrid = new PdfGrid();

//Add values to list

List<object> data = new List<object>();

Object row1 = new { ID = "E01", Name = "John" };

Object row2 = new { ID = "E02", Name = "Thomas" };

Object row3 = new { ID = "E03", Name = "Peter" };

data.Add(row1);

data.Add(row2);

data.Add(row3);

//Add list to IEnumerable

IEnumerable<object> dataTable = data;

//Assign data source.

pdfGrid.DataSource = dataTable;

//Create an instance of PdfGridRowStyle

PdfGridRowStyle pdfGridRowStyle = new PdfGridRowStyle();

pdfGridRowStyle.BackgroundBrush = PdfBrushes.LightYellow;

pdfGridRowStyle.Font = new PdfStandardFont(PdfFontFamily.Courier, 10);

pdfGridRowStyle.TextBrush = PdfBrushes.Blue;

pdfGridRowStyle.TextPen = PdfPens.Pink;

//Set the height

pdfGrid.Rows[2].Height = 50;

//Set style for the PdfGridRow.

pdfGrid.Rows[0].Style = pdfGridRowStyle;

//Draw the PdfGrid.

PdfGridLayoutResult result = pdfGrid.Draw(pdfPage, Syncfusion.Drawing.PointF.Empty);

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the PDF document to stream.

pdfDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document.

pdfDocument.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Create a new PDF document.

PdfDocument pdfDocument = new PdfDocument();

PdfPage pdfPage = pdfDocument.Pages.Add();

//Create a new PdfGrid.

PdfGrid pdfGrid = new PdfGrid();

//Add values to list

List<object> data = new List<object>();

Object row1 = new { ID = "E01", Name = "John" };

Object row2 = new { ID = "E02", Name = "Thomas" };

Object row3 = new { ID = "E03", Name = "Peter" };

data.Add(row1);

data.Add(row2);

data.Add(row3);

//Add list to IEnumerable

IEnumerable<object> dataTable = data;

//Assign data source.

pdfGrid.DataSource = dataTable;

//Create an instance of PdfGridRowStyle

PdfGridRowStyle pdfGridRowStyle = new PdfGridRowStyle();

pdfGridRowStyle.BackgroundBrush = PdfBrushes.LightYellow;

pdfGridRowStyle.Font = new PdfStandardFont(PdfFontFamily.Courier, 10);

pdfGridRowStyle.TextBrush = PdfBrushes.Blue;

pdfGridRowStyle.TextPen = PdfPens.Pink;

//Set the height

pdfGrid.Rows[2].Height = 50;

//Set style for the PdfGridRow.

pdfGrid.Rows[0].Style = pdfGridRowStyle;

//Draw the PdfGrid.

PdfGridLayoutResult result = pdfGrid.Draw(pdfPage, Syncfusion.Drawing.PointF.Empty);

//Save the PDF document into stream

MemoryStream stream = new MemoryStream();

pdfDocument.Save(stream);

//Close the document.

pdfDocument.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

### Columns customization in PdfGrid

You can customize column width and text formats using [Columns](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGrid.html#Syncfusion_Pdf_Grid_PdfGrid_Columns) property in [PdfGrid](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGrid.html) class.

The following code snippet illustrates how to customize the column in ``PdfGrid``.

{% tabs %}

{% highlight c# %}

//Create a new PDF document.

PdfDocument pdfDocument = new PdfDocument();

PdfPage pdfPage = pdfDocument.Pages.Add();

//Create a new PdfGrid.

PdfGrid pdfGrid = new PdfGrid();

//Create a DataTable.

DataTable dataTable = new DataTable();

//Add columns to the DataTable.

dataTable.Columns.Add("ID");

dataTable.Columns.Add("Name");

//Add rows to the DataTable.

dataTable.Rows.Add(new object[] { "E01", "John" });

dataTable.Rows.Add(new object[] { "E02", "Thomas" });

dataTable.Rows.Add(new object[] { "E03", "Peter" });

//Assign data source.

pdfGrid.DataSource = dataTable;

//Set the width

pdfGrid.Columns[1].Width = 50;

//create and customize the string formats

PdfStringFormat format=new PdfStringFormat();

format.Alignment=PdfTextAlignment.Center;

format.LineAlignment=PdfVerticalAlignment.Bottom;

//set the column text format

pdfGrid.Columns[0].Format = format;

//Draw the PdfGrid.

PdfGridLayoutResult result = pdfGrid.Draw(pdfPage, PointF.Empty);

//Save the document.

pdfDocument.Save("Output.pdf");

//close the document

pdfDocument.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim pdfDocument As New PdfDocument()

Dim pdfPage As PdfPage = pdfDocument.Pages.Add()

'Create a new PdfGrid.

Dim pdfGrid As New PdfGrid()

'Create a DataTable.

Dim dataTable As New DataTable()

'Add columns to the DataTable.

dataTable.Columns.Add("ID")

dataTable.Columns.Add("Name")

'Add rows to the DataTable.

dataTable.Rows.Add(New Object() {"E01", "John"})

dataTable.Rows.Add(New Object() {"E02", "Thomas"})

dataTable.Rows.Add(New Object() {"E03", "Peter"})

'Assign data source.

pdfGrid.DataSource = dataTable

'Set the width

pdfGrid.Columns(1).Width = 50

'create and customize the string formats

Dim format As New PdfStringFormat()

format.Alignment = PdfTextAlignment.Center

format.LineAlignment = PdfVerticalAlignment.Bottom

'set the column text format

pdfGrid.Columns(0).Format = format

'Draw the PdfGrid.

Dim result As PdfGridLayoutResult = pdfGrid.Draw(pdfPage, PointF.Empty)

'Save the document.

pdfDocument.Save("Output.pdf")

'close the document

pdfDocument.Close(True)

{% endhighlight %}

{% highlight UWP %}

//Create a new PDF document.

PdfDocument pdfDocument = new PdfDocument();

PdfPage pdfPage = pdfDocument.Pages.Add();

//Create a new PdfGrid.

PdfGrid pdfGrid = new PdfGrid();

//Add values to list

List<object> data = new List<object>();

Object row1 = new { ID = "E01", Name = "Clay" };

Object row2 = new { ID = "E02", Name = "Thomas" };

Object row3 = new { ID = "E02", Name = "Peter" };

data.Add(row1);

data.Add(row2);

data.Add(row3);

//Add list to IEnumerable

IEnumerable<object> dataTable = data;

//Assign data source.

pdfGrid.DataSource = dataTable;

//Set the width

pdfGrid.Columns[1].Width = 50;

//create and customize the string formats

PdfStringFormat format = new PdfStringFormat();

format.Alignment = PdfTextAlignment.Center;

format.LineAlignment = PdfVerticalAlignment.Bottom;

//set the column text format

pdfGrid.Columns[0].Format = format;

//Draw the PdfGrid.

PdfGridLayoutResult result = pdfGrid.Draw(pdfPage, PointF.Empty);

//Save the PDF document into stream

MemoryStream stream = new MemoryStream();

await pdfDocument.SaveAsync(stream);

//Close the document.

pdfDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document.

PdfDocument pdfDocument = new PdfDocument();

PdfPage pdfPage = pdfDocument.Pages.Add();

//Create a new PdfGrid.

PdfGrid pdfGrid = new PdfGrid();

//Add values to list

List<object> data = new List<object>();

Object row1 = new { ID = "E01", Name = "Clay" };

Object row2 = new { ID = "E02", Name = "Thomas" };

Object row3 = new { ID = "E02", Name = "Peter" };

data.Add(row1);

data.Add(row2);

data.Add(row3);

//Add list to IEnumerable

IEnumerable<object> dataTable = data;

//Assign data source.

pdfGrid.DataSource = dataTable;

//Set the width

pdfGrid.Columns[1].Width = 50;

//create and customize the string formats

PdfStringFormat format = new PdfStringFormat();

format.Alignment = PdfTextAlignment.Center;

format.LineAlignment = PdfVerticalAlignment.Bottom;

//set the column text format

pdfGrid.Columns[0].Format = format;

//Draw the PdfGrid.

PdfGridLayoutResult result = pdfGrid.Draw(pdfPage, Syncfusion.Drawing.PointF.Empty);

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the PDF document to stream.

pdfDocument.Save(stream);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document.

pdfDocument.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);


{% endhighlight %}

{% highlight Xamarin %}

//Create a new PDF document.

PdfDocument pdfDocument = new PdfDocument();

PdfPage pdfPage = pdfDocument.Pages.Add();

//Create a new PdfGrid.

PdfGrid pdfGrid = new PdfGrid();

//Add values to list

List<object> data = new List<object>();

Object row1 = new { ID = "E01", Name = "Clay" };

Object row2 = new { ID = "E02", Name = "Thomas" };

Object row3 = new { ID = "E02", Name = "Peter" };

data.Add(row1);

data.Add(row2);

data.Add(row3);

//Add list to IEnumerable

IEnumerable<object> dataTable = data;

//Assign data source.

pdfGrid.DataSource = dataTable;

//Set the width

pdfGrid.Columns[1].Width = 50;

//create and customize the string formats

PdfStringFormat format = new PdfStringFormat();

format.Alignment = PdfTextAlignment.Center;

format.LineAlignment = PdfVerticalAlignment.Bottom;

//set the column text format

pdfGrid.Columns[0].Format = format;

//Draw the PdfGrid.

PdfGridLayoutResult result = pdfGrid.Draw(pdfPage, Syncfusion.Drawing.PointF.Empty);

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

pdfDocument.Save(stream);

//Close the document.

pdfDocument.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

## Support for table customization

### Table customization in PdfLightTable

Essential PDF supports users to create a customizable PDF table like [CellSpacing](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTableStyle.html#Syncfusion_Pdf_Tables_PdfLightTableStyle_CellSpacing), [CellPadding](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTableStyle.html#Syncfusion_Pdf_Tables_PdfLightTableStyle_CellPadding), [RepeatHeader](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTableStyle.html#Syncfusion_Pdf_Tables_PdfLightTableStyle_RepeatHeader), [ShowHeader](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTableStyle.html#Syncfusion_Pdf_Tables_PdfLightTableStyle_ShowHeader), etc. This can be achieved by using the [PdfLightTableStyle](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTableStyle.html) class.

The following code snippet illustrates how to customize the table using [PdfLightTable](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTable.html). 

{% tabs %}

{% highlight c# %}

//Create a new PDF document

PdfDocument document = new PdfDocument();

//Add a page

PdfPage page = document.Pages.Add();

//Create a PdfLightTable

PdfLightTable pdfLightTable = new PdfLightTable();

//Initialize DataTable to assign as DateSource to the light table

DataTable table = new DataTable();

//Include columns to the DataTable

table.Columns.Add("Name");

table.Columns.Add("Age");

table.Columns.Add("Sex");

//Include rows to the DataTable

table.Rows.Add(new string[] { "abc", "21", "Male" });

//Assign data source

pdfLightTable.DataSource = table;

//Declare and define light table style

PdfLightTableStyle lightTableStyle = new PdfLightTableStyle();

//Set cell padding, which specifies the space between border and content of the cell

lightTableStyle.CellPadding = 2;

//Set cell spacing, which specifies the space between the adjacent cells

lightTableStyle.CellSpacing = 2;

//Sets to show header in table

lightTableStyle.ShowHeader = true;

//Sets to repeat header on each page

lightTableStyle.RepeatHeader = true;

//Apply style

pdfLightTable.Style = lightTableStyle;

//Draw PdfLightTable

pdfLightTable.Draw(page, new PointF(0, 0));

//Save the document

document.Save("Output.pdf");

//Close the document

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document

Dim document As New PdfDocument()

'Add a page

Dim page As PdfPage = document.Pages.Add()

'Create a PdfLightTable

Dim pdfLightTable As New PdfLightTable()

'Initialize DataTable to assign as DateSource to the light table

Dim table As New DataTable()

'Include columns to the DataTable

table.Columns.Add("Name")

table.Columns.Add("Age")

table.Columns.Add("Sex")

'Include rows to the DataTable

table.Rows.Add(New String() {"abc", "21", "Male"})

'Assign data source

pdfLightTable.DataSource = table

'Declare and define light table style

Dim lightTableStyle As New PdfLightTableStyle()

'Set cell padding, which specifies the space between border and content of the cell

lightTableStyle.CellPadding = 2

'Set cell spacing, which specifies the space between the adjacent cells

lightTableStyle.CellSpacing = 2

'Sets to show header in table

lightTableStyle.ShowHeader = True

'Sets to repeat header on each page

lightTableStyle.RepeatHeader = True

'Apply style

pdfLightTable.Style = lightTableStyle

'Draw PdfLightTable

pdfLightTable.Draw(page, New PointF(0, 0))

'Save the document

document.Save("Output.pdf")

'Close the document

document.Close(True)

{% endhighlight %}

{% highlight UWP %}

//Create a new PDF document

PdfDocument document = new PdfDocument();

//Add a page

PdfPage page = document.Pages.Add();

// Create a PdfLightTable

PdfLightTable pdfLightTable = new PdfLightTable();

//Add values to list

List<object> data = new List<object>();

object row = new { Name = "abc", Age = "21", Sex = "Male" };

data.Add(row);

//Add list to IEnumerable

IEnumerable<object> table = data;

//Assign data source

pdfLightTable.DataSource = table;

//Declare and define light table style

PdfLightTableStyle lightTableStyle = new PdfLightTableStyle();

//Set cell padding, which specifies the space between border and content of the cell

lightTableStyle.CellPadding = 2;

//Set cell spacing, which specifies the space between the adjacent cells

lightTableStyle.CellSpacing = 2;

//Sets to show header in table

lightTableStyle.ShowHeader = true;

//Sets to repeat header on each page

lightTableStyle.RepeatHeader = true;

//Apply style

pdfLightTable.Style = lightTableStyle;

//Draw PdfLightTable

pdfLightTable.Draw(page, new PointF(0, 0));

//Save the PDF document to stream

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document

PdfDocument document = new PdfDocument();

//Add a page

PdfPage page = document.Pages.Add();

// Create a PdfLightTable

PdfLightTable pdfLightTable = new PdfLightTable();

//Add values to list

List<object> data = new List<object>();

object row = new { Name = "abc", Age = "21", Sex = "Male" };

data.Add(row);

//Add list to IEnumerable

IEnumerable<object> table = data;

//Assign data source

pdfLightTable.DataSource = table;

//Declare and define light table style

PdfLightTableStyle lightTableStyle = new PdfLightTableStyle();

//Set cell padding, which specifies the space between border and content of the cell

lightTableStyle.CellPadding = 2;

//Set cell spacing, which specifies the space between the adjacent cells

lightTableStyle.CellSpacing = 2;

//Sets to show header in table

lightTableStyle.ShowHeader = true;

//Sets to repeat header on each page

lightTableStyle.RepeatHeader = true;

//Apply style

pdfLightTable.Style = lightTableStyle;

//Draw PdfLightTable

pdfLightTable.Draw(page, new PointF(0, 0));

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the document as stream

document.Save(stream);

//If the position is not set to '0', then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close(true);

//Defining the ContentType for PDF file.

string contentType = "application/pdf";

//Define the file name

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Create a new PDF document

PdfDocument document = new PdfDocument();

//Add a page

PdfPage page = document.Pages.Add();

// Create a PdfLightTable

PdfLightTable pdfLightTable = new PdfLightTable();

//Add values to list

List<object> data = new List<object>();

object row = new { Name = "abc", Age = "21", Sex = "Male" };

data.Add(row);

//Add list to IEnumerable

IEnumerable<object> table = data;

//Assign data source

pdfLightTable.DataSource = table;

//Declare and define light table style

PdfLightTableStyle lightTableStyle = new PdfLightTableStyle();	

//Set cell padding, which specifies the space between border and content of the cell

lightTableStyle.CellPadding = 2;

//Set cell spacing, which specifies the space between the adjacent cells

lightTableStyle.CellSpacing = 2;

//Sets to show header in table

lightTableStyle.ShowHeader = true;

//Sets to repeat header on each page

lightTableStyle.RepeatHeader = true;

//Apply style

pdfLightTable.Style = lightTableStyle;

//Draw PdfLightTable

pdfLightTable.Draw(page, new PointF(0, 0));

//Save the document as stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document instances

document.Close(true);

//Save the stream into PDF file

//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples

if (Device.RuntimePlatform == Device.UWP)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

### Table customization in PdfGrid

Essential PDF supports users to create a customizable PDF table like [CellSpacing](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGridStyle.html#Syncfusion_Pdf_Grid_PdfGridStyle_CellSpacing), [CellPadding](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGridStyle.html#Syncfusion_Pdf_Grid_PdfGridStyle_CellPadding), [HorizontalOverflow](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGridStyle.html#Syncfusion_Pdf_Grid_PdfGridStyle_AllowHorizontalOverflow), etc. This can be achieved by using [PdfGridStyle](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGridStyle.html) class.

The following code snippet illustrates how to customize the table using [PdfGrid](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGrid.html). 

{% tabs %}

{% highlight c# %}

//Create a new PDF document

PdfDocument document = new PdfDocument();

//Add a page

PdfPage page = document.Pages.Add();

//Create a PdfGrid

PdfGrid pdfGrid = new PdfGrid();

//Create a DataTable

DataTable dataTable = new DataTable();

//Add columns to the DataTable

dataTable.Columns.Add("ID");

dataTable.Columns.Add("Name");

//Add rows to the DataTable

dataTable.Rows.Add(new object[] { "E01", "Clay" });

dataTable.Rows.Add(new object[] { "E02", "Thomas" });

//Assign data source

pdfGrid.DataSource = dataTable;

//Declare and define the grid style

PdfGridStyle gridStyle = new PdfGridStyle();

//Set cell padding, which specifies the space between border and content of the cell

gridStyle.CellPadding = new PdfPaddings(2, 2, 2, 2);

//Set cell spacing, which specifies the space between the adjacent cells

gridStyle.CellSpacing = 2;

//Enable to adjust PDF table row width based on the text length

gridStyle.AllowHorizontalOverflow = true;

//Apply style

pdfGrid.Style = gridStyle;

//Draw grid to the page of PDF document

pdfGrid.Draw(page, new PointF(10, 10));

//Save the document

document.Save("Output.pdf");

//Close the document

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document

Dim document As New PdfDocument()

'Add a page

Dim page As PdfPage = document.Pages.Add()

'Create a PdfGrid

Dim pdfGrid As New PdfGrid()

'Create a DataTable

Dim dataTable As New DataTable()

'Add columns to the DataTable

dataTable.Columns.Add("ID")

dataTable.Columns.Add("Name")

'Add rows to the DataTable

dataTable.Rows.Add(New Object() {"E01", "Clay"})

dataTable.Rows.Add(New Object() {"E02", "Thomas"})

'Assign data source

pdfGrid.DataSource = dataTable

'Declare and define the grid style

Dim gridStyle As New PdfGridStyle()

'Set cell padding, which specifies the space between border and content of the cell

gridStyle.CellPadding = New PdfPaddings(2, 2, 2, 2)

'Set cell spacing, which specifies the space between the adjacent cells

gridStyle.CellSpacing = 2

'Enable to adjust PDF table row width based on the text length

gridStyle.AllowHorizontalOverflow = True

'Apply style

pdfGrid.Style = gridStyle

'Draw grid to the page of PDF document

pdfGrid.Draw(page, New PointF(10, 10))

'Save the document

document.Save("Output.pdf")

'Close the document

document.Close(True)

'This will open the PDF file so, the result will be seen in default PDF viewer

Process.Start("Output.pdf")

{% endhighlight %}

{% highlight UWP %}

//Create a new PDF document

PdfDocument doc = new PdfDocument();

//Add a page

PdfPage page = doc.Pages.Add();

//Create a PdfGrid

PdfGrid pdfGrid = new PdfGrid();

//Add values to list

List<object> data = new List<object>();

Object row1 = new { ID = "E01", Name = "Clay" };

Object row2 = new { ID = "E02", Name = "Thomas" };

data.Add(row1);

data.Add(row2);

//Add list to IEnumerable

IEnumerable<object> dataTable = data;

//Assign data source

pdfGrid.DataSource = dataTable;

//Declare and define the grid style

PdfGridStyle gridStyle = new PdfGridStyle();

//Set cell padding, which specifies the space between border and content of the cell

gridStyle.CellPadding = new PdfPaddings(2, 2, 2, 2);

//Set cell spacing, which specifies the space between the adjacent cells

gridStyle.CellSpacing = 2;

//Enable to adjust PDF table row width based on the text length

gridStyle.AllowHorizontalOverflow = true;

//Apply style

pdfGrid.Style = gridStyle;

//Draw grid to the page of PDF document

pdfGrid.Draw(page, new PointF(10, 10));

//Save the PDF document into stream

MemoryStream stream = new MemoryStream();

await doc.SaveAsync(stream);

//Close the document

doc.Close(true);

//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document

PdfDocument document = new PdfDocument();

//Add a page

PdfPage page = document.Pages.Add();

//Create a PdfGrid

PdfGrid pdfGrid = new PdfGrid();

//Add values to list

List<object> data = new List<object>();

Object row1 = new { ID = "E01", Name = "Clay" };

Object row2 = new { ID = "E02", Name = "Thomas" };

data.Add(row1);

data.Add(row2);

//Add list to IEnumerable

IEnumerable<object> dataTable = data;

//Assign data source

pdfGrid.DataSource = dataTable;

//Declare and define the grid style

PdfGridStyle gridStyle = new PdfGridStyle();

//Set cell padding, which specifies the space between border and content of the cell

gridStyle.CellPadding = new PdfPaddings(2, 2, 2, 2);

//Set cell spacing, which specifies the space between the adjacent cells

gridStyle.CellSpacing = 2;

//Enable to adjust PDF table row width based on the text length

gridStyle.AllowHorizontalOverflow = true;

//Apply style

pdfGrid.Style = gridStyle;

//Draw grid to the page of PDF document

pdfGrid.Draw(page, new PointF(10, 10));

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the document as stream

document.Save(stream);

//If the position is not set to '0', then the PDF will be empty

stream.Position = 0;

//Close the document

document.Close(true);

//Defining the ContentType for PDF file.

string contentType = "application/pdf";

//Define the file name

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Create a new PDF document

PdfDocument document = new PdfDocument();

//Add a page

PdfPage page = document.Pages.Add();

//Create a PdfGrid

PdfGrid pdfGrid = new PdfGrid();

//Add values to list

List<object> data = new List<object>();

Object row1 = new { ID = "E01", Name = "Clay" };

Object row2 = new { ID = "E02", Name = "Thomas" };

data.Add(row1);

data.Add(row2);

//Add list to IEnumerable

IEnumerable<object> dataTable = data;

//Assign data source

pdfGrid.DataSource = dataTable;

//Declare and define the grid style

PdfGridStyle gridStyle = new PdfGridStyle();

//Set cell padding, which specifies the space between border and content of the cell

gridStyle.CellPadding = new PdfPaddings(2, 2, 2, 2);

//Set cell spacing, which specifies the space between the adjacent cells

gridStyle.CellSpacing = 2;

//Enable to adjust PDF table row width based on the text length

gridStyle.AllowHorizontalOverflow = true;

//Apply style

pdfGrid.Style = gridStyle;

//Draw grid to the page of PDF document

pdfGrid.Draw(page, new PointF(10, 10));

//Save the document as stream

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document instances

document.Close(true);

//Save the stream into PDF file

//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples

if (Device.RuntimePlatform == Device.UWP)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

## Built-in table styles

In-built table styles can be applied to both [PdfGrid](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGrid.html) and [PdfLightTable](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTable.html) models and the appearance is made similar to Microsoft Word’s built-in table styles. You can also apply in-built table styles with the following additional table style options.


* Banded columns
* Banded rows
* First column
* Last column
* Header row
* Last row

The below code example illustrates how to apply built-in table style using [ApplyBuiltinStyle](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGrid.html#Syncfusion_Pdf_Grid_PdfGrid_ApplyBuiltinStyle_Syncfusion_Pdf_PdfGridBuiltinStyle_) method of the ``PdfGrid`` with styles from [PdfGridBuiltinStyle](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfGridBuiltinStyle.html) Enum.

{% tabs %}

{% highlight c# %}

//Create a new PDF document.
PdfDocument doc = new PdfDocument();

//Add a page.
PdfPage page = doc.Pages.Add();

//Create a PdfGrid.
PdfGrid pdfGrid = new PdfGrid();
//Create a DataTable.
DataTable dataTable = new DataTable();

//Add columns to the DataTable
dataTable.Columns.Add("ID");
dataTable.Columns.Add("Name");

//Add rows to the DataTable.
dataTable.Rows.Add(new object[] { "E01", "Clay" });
dataTable.Rows.Add(new object[] { "E02", "Thomas" });
dataTable.Rows.Add(new object[] { "E03", "George" });
dataTable.Rows.Add(new object[] { "E04", "Stefan" });
dataTable.Rows.Add(new object[] { "E05", "Mathew" });
            
//Assign data source.
pdfGrid.DataSource = dataTable;

//Apply built-in table style
pdfGrid.ApplyBuiltinStyle(PdfGridBuiltinStyle.GridTable4Accent1);
//Draw grid to the page of PDF document.
pdfGrid.Draw(page, new PointF(10, 10));

//Save the document.
doc.Save("Output.pdf");
//close the document
doc.Close(true);


{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document.
Dim doc As New PdfDocument()

'Add a page.
Dim page As PdfPage = doc.Pages.Add()

'Create a PdfGrid.
Dim pdfGrid As New PdfGrid()
'Create a DataTable.
Dim dataTable As New DataTable()

'Add columns to the DataTable
dataTable.Columns.Add("ID")
dataTable.Columns.Add("Name")

'Add rows to the DataTable.
dataTable.Rows.Add(New Object() {"E01", "Clay"})
dataTable.Rows.Add(New Object() {"E02", "Thomas"})
dataTable.Rows.Add(New Object() {"E03", "George"})
dataTable.Rows.Add(new object() {"E04", "Stefan"})
dataTable.Rows.Add(new object() {"E05", "Mathew"})

'Assign data source.
pdfGrid.DataSource = dataTable

'Apply built-in table style
pdfGrid.ApplyBuiltinStyle(PdfGridBuiltinStyle.GridTable4Accent1)
'Draw grid to the page of PDF document.
pdfGrid.Draw(page, New PointF(10, 10))

'Save the document.
doc.Save("Output.pdf")
'close the document
doc.Close(True)

{% endhighlight %}

{% highlight UWP %}

//Create a new PDF document.
PdfDocument doc = new PdfDocument();

//Add a page.
PdfPage page = doc.Pages.Add();

//Create a PdfGrid.
PdfGrid pdfGrid = new PdfGrid();

//Add values to list
List<object> data = new List<object>();

Object row1 = new { ID = "E01", Name = "Clay" };
Object row2 = new { ID = "E02", Name = "Thomas" };
Object row3 = new { ID = "E03", Name = "George" };
Object row4 = new { ID = "E04", Name = "Steffen" };
Object row5 = new { ID = "E05", Name = "Mathew" };

data.Add(row1);
data.Add(row2);
data.Add(row3);
data.Add(row4);
data.Add(row5);

//Add list to IEnumerable
IEnumerable<object> dataTable = data;

//Assign data source.
pdfGrid.DataSource = dataTable;

//Apply built-in table style
pdfGrid.ApplyBuiltinStyle(PdfGridBuiltinStyle.GridTable4Accent1);
//Draw grid to the page of PDF document.
pdfGrid.Draw(page, new PointF(10, 10));

//Save the PDF document to stream.
MemoryStream stream = new MemoryStream();

await doc.SaveAsync(stream);

//Close the document.
doc.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

 //Create a new PDF document.
PdfDocument doc = new PdfDocument();

//Add a page.
PdfPage page = doc.Pages.Add();

//Create a PdfGrid.
PdfGrid pdfGrid = new PdfGrid();

//Add values to list
List<object> data = new List<object>();

Object row1 = new { ID = "E01", Name = "Clay" };
Object row2 = new { ID = "E02", Name = "Thomas" };
Object row3 = new { ID = "E03", Name = "George" };
Object row4 = new { ID = "E04", Name = "Steffen" };
Object row5 = new { ID = "E05", Name = "Mathew" };

data.Add(row1);
data.Add(row2);
data.Add(row3);
data.Add(row4);
data.Add(row5);

//Add list to IEnumerable
IEnumerable<object> dataTable = data;

//Assign data source.
pdfGrid.DataSource = dataTable;

//Apply built-in table style
pdfGrid.ApplyBuiltinStyle(PdfGridBuiltinStyle.GridTable4Accent1);
//Draw grid to the page of PDF document.
pdfGrid.Draw(page, new Syncfusion.Drawing.PointF(10, 10));

//Creating the stream object
MemoryStream stream = new MemoryStream();

//Save the document as stream
doc.Save(stream);

//If the position is not set to '0' then the PDF will be empty.
stream.Position = 0;

//Close the document.
doc.Close(true);

//Defining the ContentType for pdf file.
string contentType = "application/pdf";

//Define the file name.
string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Create a new PDF document.
PdfDocument doc = new PdfDocument();

//Add a page.
PdfPage page = doc.Pages.Add();

//Create a PdfGrid.
PdfGrid pdfGrid = new PdfGrid();

//Add values to list
List<object> data = new List<object>();

Object row1 = new { ID = "E01", Name = "Clay" };
Object row2 = new { ID = "E02", Name = "Thomas" };
Object row3 = new { ID = "E03", Name = "George" };
Object row4 = new { ID = "E04", Name = "Steffen" };
Object row5 = new { ID = "E05", Name = "Mathew" };

data.Add(row1);
data.Add(row2);
data.Add(row3);
data.Add(row4);
data.Add(row5);

//Add list to IEnumerable
IEnumerable<object> dataTable = data;

//Assign data source.
pdfGrid.DataSource = dataTable;

//Apply built-in table style
pdfGrid.ApplyBuiltinStyle(PdfGridBuiltinStyle.GridTable4Accent1);
//Draw grid to the page of PDF document.
pdfGrid.Draw(page, new Syncfusion.Drawing.PointF(10, 10));

//Save the PDF document to stream.
MemoryStream stream = new MemoryStream();
doc.Save(stream);

//Close the document.
doc.Close(true);

//Save the stream into pdf file
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

The following image shows the PDF document with ```PdfGridBuiltinStyle.GridTable4Accent1```.
![GridTable4Accent1 image](Table_images/Gridtable4Accent1.png)

The below code example illustrates how to apply built-in table style using [ApplyBuiltinStyle](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTable.html#Syncfusion_Pdf_Tables_PdfLightTable_ApplyBuiltinStyle_Syncfusion_Pdf_PdfLightTableBuiltinStyle_) method of the ``PdfLightTable`` with styles from [PdfLightTableBuiltinStyle](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfLightTableBuiltinStyle.html) Enum.

{% tabs %}

{% highlight c# %}

//Create a new PDF document.
PdfDocument doc = new PdfDocument();

//Add a page.
PdfPage page = doc.Pages.Add();

//Create a PdfLightTable.
PdfLightTable pdfLightTable = new PdfLightTable();
//Create a DataTable.
DataTable dataTable = new DataTable();

//Add columns to the DataTable
dataTable.Columns.Add("ID");
dataTable.Columns.Add("Name");

//Add rows to the DataTable.
dataTable.Rows.Add(new object[] { "E01", "Clay" });
dataTable.Rows.Add(new object[] { "E02", "Thomas" });
dataTable.Rows.Add(new object[] { "E03", "George" });
dataTable.Rows.Add(new object[] { "E04", "Stefan" });
dataTable.Rows.Add(new object[] { "E05", "Mathew" });

//Assign data source.
pdfLightTable.DataSource = dataTable;

//Apply built-in table style
pdfLightTable.ApplyBuiltinStyle(PdfLightTableBuiltinStyle.GridTable4Accent2);

//Draw grid to the page of PDF document.
pdfLightTable.Draw(page, new PointF(10, 10));

//Save the document.
doc.Save("Output.pdf");
//close the document
doc.Close(true);


{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document.
Dim doc As New PdfDocument()

'Add a page.
Dim page As PdfPage = doc.Pages.Add()

'Create a PdfLightTable.
Dim pdfLightTable As New PdfLightTable()
'Create a DataTable.
Dim dataTable As New DataTable()

'Add columns to the DataTable
dataTable.Columns.Add("ID")
dataTable.Columns.Add("Name")

'Add rows to the DataTable.
dataTable.Rows.Add(New Object() {"E01", "Clay"})
dataTable.Rows.Add(New Object() {"E02", "Thomas"})
dataTable.Rows.Add(New Object() {"E03", "George"})
dataTable.Rows.Add(new object() { "E04", "Stefan"})
dataTable.Rows.Add(new object() { "E05", "Mathew"})

'Assign data source.
pdfLightTable.DataSource = dataTable

'Apply built-in table style
pdfLightTable.ApplyBuiltinStyle(PdfLightTableBuiltinStyle.GridTable4Accent2)

'Draw grid to the page of PDF document.
pdfLightTable.Draw(page, New PointF(10, 10))

'Save the document.
doc.Save("Output.pdf")
'close the document
doc.Close(True)

{% endhighlight %}

{% highlight UWP %}

//Create a new PDF document.
PdfDocument doc = new PdfDocument();

//Add a page.
PdfPage page = doc.Pages.Add();

//Create a PdfLightTable.
PdfLightTable pdfLightTable = new PdfLightTable();
//Add values to list
List<object> data = new List<object>();

Object row1 = new { ID = "E01", Name = "Clay" };
Object row2 = new { ID = "E02", Name = "Thomas" };
Object row3 = new { ID = "E03", Name = "George" };
Object row4 = new { ID = "E04", Name = "Steffen" };
Object row5 = new { ID = "E05", Name = "Mathew" };

data.Add(row1);
data.Add(row2);
data.Add(row3);
data.Add(row4);
data.Add(row5);

//Add list to IEnumerable
IEnumerable<object> dataTable = data;

//Assign data source.
pdfLightTable.DataSource = dataTable;

//Apply built-in table style
pdfLightTable.ApplyBuiltinStyle(PdfLightTableBuiltinStyle.GridTable4Accent2);

//Draw grid to the page of PDF document.
pdfLightTable.Draw(page, new PointF(10, 10));

//Save the PDF document to stream.
MemoryStream stream = new MemoryStream();
await doc.SaveAsync(stream);

//Close the document.
doc.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document.
PdfDocument doc = new PdfDocument();

//Add a page.
PdfPage page = doc.Pages.Add();

//Create a PdfLightTable.
PdfLightTable pdfLightTable = new PdfLightTable();

//Add values to list
List<object> data = new List<object>();

Object row1 = new { ID = "E01", Name = "Clay" };
Object row2 = new { ID = "E02", Name = "Thomas" };
Object row3 = new { ID = "E03", Name = "George" };
Object row4 = new { ID = "E04", Name = "Steffen" };
Object row5 = new { ID = "E05", Name = "Mathew" };

data.Add(row1);
data.Add(row2);
data.Add(row3);
data.Add(row4);
data.Add(row5);

//Add list to IEnumerable
IEnumerable<object> dataTable = data;

//Assign data source.
pdfLightTable.DataSource = dataTable;

//Apply built-in table style
pdfLightTable.ApplyBuiltinStyle(PdfLightTableBuiltinStyle.GridTable4Accent2);

//Draw grid to the page of PDF document.
pdfLightTable.Draw(page, new Syncfusion.Drawing.PointF(10, 10));

//Creating the stream object
MemoryStream stream = new MemoryStream();

//Save the document as stream
doc.Save(stream);

//If the position is not set to '0' then the PDF will be empty.
stream.Position = 0;

//Close the document.
doc.Close(true);

//Defining the ContentType for pdf file.
string contentType = "application/pdf";

//Define the file name.
string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Create a new PDF document.
PdfDocument doc = new PdfDocument();

//Add a page.
PdfPage page = doc.Pages.Add();

//Create a PdfLightTable.
PdfLightTable pdfLightTable = new PdfLightTable();

//Add values to list
List<object> data = new List<object>();

Object row1 = new { ID = "E01", Name = "Clay" };
Object row2 = new { ID = "E02", Name = "Thomas" };
Object row3 = new { ID = "E03", Name = "George" };
Object row4 = new { ID = "E04", Name = "Steffen" };
Object row5 = new { ID = "E05", Name = "Mathew" };

data.Add(row1);
data.Add(row2);
data.Add(row3);
data.Add(row4);
data.Add(row5);

//Add list to IEnumerable
IEnumerable<object> dataTable = data;

//Assign data source.
pdfLightTable.DataSource = dataTable;

//Apply built-in table style
pdfLightTable.ApplyBuiltinStyle(PdfLightTableBuiltinStyle.GridTable4Accent2);

//Draw grid to the page of PDF document.
pdfLightTable.Draw(page, new Syncfusion.Drawing.PointF(10, 10));

//Save the PDF document to stream.
MemoryStream stream = new MemoryStream();
doc.Save(stream);

//Close the document.
doc.Close(true);

//Save the stream into pdf file
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

The following image shows the PDF document with ```PdfGridBuiltinStyle.Gridtable4Accent2```.
![Gridtable4Accent2 image](Table_images/Gridtable4Accent2.png)

The below code example illustrates how to apply built-in table styles with table options to the [PdfGrid](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGrid.html).

{% tabs %}

{% highlight c# %}

//Create a new PDF document.
PdfDocument doc = new PdfDocument();

//Add a page.
PdfPage page = doc.Pages.Add();

//Create a PdfGrid.
PdfGrid pdfGrid = new PdfGrid();
//Create a DataTable.
DataTable dataTable = new DataTable();

//Add columns to the DataTable
dataTable.Columns.Add("ID");
dataTable.Columns.Add("Name");

//Add rows to the DataTable.
dataTable.Rows.Add(new object[] { "E01", "Clay" });
dataTable.Rows.Add(new object[] { "E02", "Thomas" });
dataTable.Rows.Add(new object[] { "E03", "George" });
dataTable.Rows.Add(new object[] { "E04", "Stefan" });
dataTable.Rows.Add(new object[] { "E05", "Mathew" });

//Assign data source.
pdfGrid.DataSource = dataTable;

PdfGridBuiltinStyleSettings tableStyleOption = new PdfGridBuiltinStyleSettings();
tableStyleOption.ApplyStyleForBandedRows = true;
tableStyleOption.ApplyStyleForHeaderRow = true;

//Apply built-in table style
pdfGrid.ApplyBuiltinStyle(PdfGridBuiltinStyle.GridTable4Accent4, tableStyleOption);
//Draw grid to the page of PDF document.
pdfGrid.Draw(page, new PointF(10, 10));

//Save the document.
doc.Save("Output.pdf");
//close the document
doc.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document.
Dim doc As New PdfDocument()

'Add a page.
Dim page As PdfPage = doc.Pages.Add()

'Create a PdfGrid.
Dim pdfGrid As New PdfGrid()
'Create a DataTable.
Dim dataTable As New DataTable()

'Add columns to the DataTable
dataTable.Columns.Add("ID")
dataTable.Columns.Add("Name")

'Add rows to the DataTable.
dataTable.Rows.Add(New Object() {"E01", "Clay"})
dataTable.Rows.Add(New Object() {"E02", "Thomas"})
dataTable.Rows.Add(New Object() {"E03", "George"})
dataTable.Rows.Add(new object() { "E04", "Stefan"})
dataTable.Rows.Add(new object() { "E05", "Mathew"})

'Assign data source.
pdfGrid.DataSource = dataTable

Dim tableStyleOption As New PdfGridBuiltinStyleSettings()
tableStyleOption.ApplyStyleForBandedRows = True
tableStyleOption.ApplyStyleForHeaderRow = True

'Apply built-in table style
pdfGrid.ApplyBuiltinStyle(PdfGridBuiltinStyle.GridTable4Accent4, tableStyleOption)
'Draw grid to the page of PDF document.
pdfGrid.Draw(page, New PointF(10, 10))

'Save the document.
doc.Save("Output.pdf")
'close the document
doc.Close(True)

{% endhighlight %}

{% highlight UWP %}

//Create a new PDF document.
PdfDocument doc = new PdfDocument();

//Add a page.
PdfPage page = doc.Pages.Add();

//Create a PdfGrid.
PdfGrid pdfGrid = new PdfGrid();

//Add values to list
List<object> data = new List<object>();

Object row1 = new { ID = "E01", Name = "Clay" };
Object row2 = new { ID = "E02", Name = "Thomas" };
Object row3 = new { ID = "E03", Name = "George" };
Object row4 = new { ID = "E04", Name = "Steffen" };
Object row5 = new { ID = "E05", Name = "Mathew" };

data.Add(row1);
data.Add(row2);
data.Add(row3);
data.Add(row4);
data.Add(row5);

//Add list to IEnumerable
IEnumerable<object> dataTable = data;

//Assign data source.
pdfGrid.DataSource = dataTable;

PdfGridBuiltinStyleSettings tableStyleOption = new PdfGridBuiltinStyleSettings();
tableStyleOption.ApplyStyleForBandedRows = true;
tableStyleOption.ApplyStyleForHeaderRow = true;

//Apply built-in table style
pdfGrid.ApplyBuiltinStyle(PdfGridBuiltinStyle.GridTable4Accent4, tableStyleOption);
//Draw grid to the page of PDF document.
pdfGrid.Draw(page, new PointF(10, 10));

//Save the PDF document to stream.
MemoryStream stream = new MemoryStream();
await doc.SaveAsync(stream);

//Close the document.
doc.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.
Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document.
PdfDocument doc = new PdfDocument();

//Add a page.
PdfPage page = doc.Pages.Add();

//Create a PdfGrid.
PdfGrid pdfGrid = new PdfGrid();

//Add values to list
List<object> data = new List<object>();

Object row1 = new { ID = "E01", Name = "Clay" };
Object row2 = new { ID = "E02", Name = "Thomas" };
Object row3 = new { ID = "E03", Name = "George" };
Object row4 = new { ID = "E04", Name = "Steffen" };
Object row5 = new { ID = "E05", Name = "Mathew" };

data.Add(row1);
data.Add(row2);
data.Add(row3);
data.Add(row4);
data.Add(row5);

//Add list to IEnumerable
IEnumerable<object> dataTable = data;

//Assign data source.
pdfGrid.DataSource = dataTable;

PdfGridBuiltinStyleSettings tableStyleOption = new PdfGridBuiltinStyleSettings();
tableStyleOption.ApplyStyleForBandedRows = true;
tableStyleOption.ApplyStyleForHeaderRow = true;

//Apply built-in table style
pdfGrid.ApplyBuiltinStyle(PdfGridBuiltinStyle.GridTable4Accent4, tableStyleOption);
//Draw grid to the page of PDF document.
pdfGrid.Draw(page, new Syncfusion.Drawing.PointF(10, 10));

//Creating the stream object
MemoryStream stream = new MemoryStream();

//Save the document as stream
doc.Save(stream);

//If the position is not set to '0' then the PDF will be empty.
stream.Position = 0;

//Close the document.
doc.Close(true);

//Defining the ContentType for pdf file.
string contentType = "application/pdf";

//Define the file name.
string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Create a new PDF document.
PdfDocument doc = new PdfDocument();

//Add a page.
PdfPage page = doc.Pages.Add();

//Create a PdfGrid.
PdfGrid pdfGrid = new PdfGrid();

//Add values to list
List<object> data = new List<object>();

Object row1 = new { ID = "E01", Name = "Clay" };
Object row2 = new { ID = "E02", Name = "Thomas" };
Object row3 = new { ID = "E03", Name = "George" };
Object row4 = new { ID = "E04", Name = "Steffen" };
Object row5 = new { ID = "E05", Name = "Mathew" };

data.Add(row1);
data.Add(row2);
data.Add(row3);
data.Add(row4);
data.Add(row5);

//Add list to IEnumerable
IEnumerable<object> dataTable = data;

//Assign data source.
pdfGrid.DataSource = dataTable;

PdfGridBuiltinStyleSettings tableStyleOption = new PdfGridBuiltinStyleSettings();
tableStyleOption.ApplyStyleForBandedRows = true;
tableStyleOption.ApplyStyleForHeaderRow = true;

//Apply built-in table style
pdfGrid.ApplyBuiltinStyle(PdfGridBuiltinStyle.GridTable4Accent4, tableStyleOption);
//Draw grid to the page of PDF document.
pdfGrid.Draw(page, new Syncfusion.Drawing.PointF(10, 10));

//Save the PDF document to stream.
MemoryStream stream = new MemoryStream();
doc.Save(stream);

//Close the document.
doc.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

The following image shows the PDF document with `PdfGridBuiltinStyle.Gridtable4Accent4`.
![Gridtable4Accent4 image](Table_images/Gridtable4Accent4.png)

## Pagination

### Pagination in PdfLightTable

Essential PDF provides support to paginate the [PdfLightTable](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTable.html) using [PdfLightTableLayoutFormat](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTableLayoutFormat.html) class.

The below sample illustrates how to allow the ``PdfLightTable`` to flow across pages.

{% tabs %}

{% highlight c# %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a page.

PdfPage page = document.Pages.Add();

// Create a PdfLightTable.

PdfLightTable pdfLightTable = new PdfLightTable();

// Initialize DataTable to assign as Date Source to the light table.

DataTable table = new DataTable();

//Include columns to the Data Table.

table.Columns.Add("Name");

table.Columns.Add("Age");

table.Columns.Add("Sex");

//Include rows to the Data Table.//you can add multiple rows

table.Rows.Add(new string[] { "abc", "21", "Male" });

//Assign data source.

pdfLightTable.DataSource = table;

//Set properties to paginate the table.

PdfLightTableLayoutFormat layoutFormat = new PdfLightTableLayoutFormat();

layoutFormat.Break = PdfLayoutBreakType.FitPage;

layoutFormat.Layout = PdfLayoutType.Paginate;

//Draw PdfLightTable.

pdfLightTable.Draw(page, new PointF(0, 0), layoutFormat);

//Save the document.

document.Save("Output.pdf");

//Close the document

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim document As New PdfDocument()

'Add a page.

Dim page As PdfPage = document.Pages.Add()

' Create a PdfLightTable.

Dim pdfLightTable As New PdfLightTable()

' Initialize DataTable to assign as Date Source to the light table.

Dim table As New DataTable()

'Include columns to the Data Table.

table.Columns.Add("Name")

table.Columns.Add("Age")

table.Columns.Add("Sex")

'Include rows to the Data Table.//you can add multiple rows

table.Rows.Add(New String() {"abc", "21", "Male"})

'Assign data source.

pdfLightTable.DataSource = table

'Set properties to paginate the table.

Dim layoutFormat As New PdfLightTableLayoutFormat()

layoutFormat.Break = PdfLayoutBreakType.FitPage

layoutFormat.Layout = PdfLayoutType.Paginate

'Draw PdfLightTable.

pdfLightTable.Draw(page, New PointF(0, 0), layoutFormat)

'Save the document.

document.Save("Output.pdf")

'Close the document

document.Close(True)

{% endhighlight %}

{% highlight UWP %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a page.

PdfPage page = document.Pages.Add();

// Create a PdfLightTable.

PdfLightTable pdfLightTable = new PdfLightTable();

//Add values to list

List<object> data = new List<object>();

//you can add multiple rows

Object row = new { Name = "abc", Age = "21", Sex = "Male" };

data.Add(row);

//Add list to IEnumerable

IEnumerable<object> table = data;

//Assign data source.

pdfLightTable.DataSource = table;

//Set properties to paginate the table.

PdfLightTableLayoutFormat layoutFormat = new PdfLightTableLayoutFormat();

layoutFormat.Break = PdfLayoutBreakType.FitPage;

layoutFormat.Layout = PdfLayoutType.Paginate;

//Draw PdfLightTable.

pdfLightTable.Draw(page, new PointF(0, 0), layoutFormat);

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document.

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a page.

PdfPage page = document.Pages.Add();

// Create a PdfLightTable.

PdfLightTable pdfLightTable = new PdfLightTable();

//Add values to list

List<object> data = new List<object>();

//you can add multiple rows

Object row = new { Name = "abc", Age = "21", Sex = "Male" };

data.Add(row);

//Add list to IEnumerable

IEnumerable<object> table = data;

//Assign data source.

pdfLightTable.DataSource = table;

//Set properties to paginate the table.

PdfLightTableLayoutFormat layoutFormat = new PdfLightTableLayoutFormat();

layoutFormat.Break = PdfLayoutBreakType.FitPage;

layoutFormat.Layout = PdfLayoutType.Paginate;

//Draw PdfLightTable.

pdfLightTable.Draw(page, new Syncfusion.Drawing.PointF(0, 0), layoutFormat);

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the document as stream

document.Save(stream);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document.

document.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a page.

PdfPage page = document.Pages.Add();

// Create a PdfLightTable.

PdfLightTable pdfLightTable = new PdfLightTable();

//Add values to list

List<object> data = new List<object>();

//you can add multiple rows

Object row = new { Name = "abc", Age = "21", Sex = "Male" };

data.Add(row);

//Add list to IEnumerable

IEnumerable<object> table = data;

//Assign data source.

pdfLightTable.DataSource = table;

//Set properties to paginate the table.

PdfLightTableLayoutFormat layoutFormat = new PdfLightTableLayoutFormat();

layoutFormat.Break = PdfLayoutBreakType.FitPage;

layoutFormat.Layout = PdfLayoutType.Paginate;

//Draw PdfLightTable.

pdfLightTable.Draw(page, new Syncfusion.Drawing.PointF(0, 0), layoutFormat);

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document.

document.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

### Pagination in PdfGrid

Essential PDF supports to paginate the [PdfGrid](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGrid.html) using [PdfGridLayoutFormat](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGridLayoutFormat.html) class.

The below sample illustrates how to allow the ``PdfGrid`` to flow across pages.

{% tabs %}

{% highlight c# %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a page

PdfPage page = document.Pages.Add();

//Create a PdfGrid

PdfGrid pdfGrid = new PdfGrid();

//Create a DataTable

DataTable dataTable = new DataTable();

//Add columns to the DataTable

dataTable.Columns.Add("ID");

dataTable.Columns.Add("Name");

//Add rows to the DataTable

dataTable.Rows.Add(new object[] { "E01", "Clay" });

dataTable.Rows.Add(new object[] { "E02", "Thomas" });

//Assign data source.

pdfGrid.DataSource = dataTable;

//Set properties to paginate the grid.

PdfGridLayoutFormat layoutFormat = new PdfGridLayoutFormat();

layoutFormat.Break = PdfLayoutBreakType.FitPage;

layoutFormat.Layout = PdfLayoutType.Paginate;

//Draw grid to the page of PDF document.

pdfGrid.Draw(page, new PointF(10, 10),layoutFormat);

//Save the document.

document.Save("Output.pdf");

//close the document

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim document As New PdfDocument()

'Add a page.

Dim page As PdfPage = document.Pages.Add()

'Create a PdfGrid.

Dim pdfGrid As New PdfGrid()

'Create a DataTable.

Dim dataTable As New DataTable()

'Add columns to the DataTable

dataTable.Columns.Add("ID")

dataTable.Columns.Add("Name")

'Add rows to the DataTable

dataTable.Rows.Add(New Object() {"E01", "Clay"})

dataTable.Rows.Add(New Object() {"E02", "Thomas"})

'Assign data source.

pdfGrid.DataSource = dataTable

'Set properties to paginate the grid

Dim layoutFormat As New PdfGridLayoutFormat()

layoutFormat.Break = PdfLayoutBreakType.FitPage

layoutFormat.Layout = PdfLayoutType.Paginate

'Draw grid to the page of PDF document.

pdfGrid.Draw(page, New PointF(10, 10), layoutFormat)

'Save the document

document.Save("Output.pdf")

'close the document

document.Close(True)

{% endhighlight %}

{% highlight UWP %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a page

PdfPage page = document.Pages.Add();

//Create a PdfGrid

PdfGrid pdfGrid = new PdfGrid();

//Add values to list

List<object> data = new List<object>();

//You can add multiple rows 

Object row1 = new { ID = "E01", Name = "Clay" };

Object row2 = new { ID = "E02", Name = "Thomas" };

data.Add(row1);

data.Add(row2);

//Add list to IEnumerable

IEnumerable<object> dataTable = data;

//Assign data source.

pdfGrid.DataSource = dataTable;

//Set properties to paginate the grid.

PdfGridLayoutFormat layoutFormat = new PdfGridLayoutFormat();

layoutFormat.Break = PdfLayoutBreakType.FitPage;

layoutFormat.Layout = PdfLayoutType.Paginate;

//Draw grid to the page of PDF document.

pdfGrid.Draw(page, new PointF(10, 10), layoutFormat);

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream);

//Close the document.

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(stream, "Output.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a page

PdfPage page = document.Pages.Add();

//Create a PdfGrid

PdfGrid pdfGrid = new PdfGrid();

//Add values to list

List<object> data = new List<object>();

//You can add multiple rows here

Object row1 = new { ID = "E01", Name = "Clay" };

Object row2 = new { ID = "E02", Name = "Thomas" };

data.Add(row1);

data.Add(row2);

//Add list to IEnumerable

IEnumerable<object> dataTable = data;

//Assign data source.

pdfGrid.DataSource = dataTable;

//Set properties to paginate the grid.

PdfGridLayoutFormat layoutFormat = new PdfGridLayoutFormat();

layoutFormat.Break = PdfLayoutBreakType.FitPage;

layoutFormat.Layout = PdfLayoutType.Paginate;

//Draw grid to the page of PDF document.

pdfGrid.Draw(page, new Syncfusion.Drawing.PointF(10, 10), layoutFormat);

//Creating the stream object

MemoryStream stream = new MemoryStream();

//Save the document as stream

document.Save(stream);

//If the position is not set to '0' then the PDF will be empty.

stream.Position = 0;

//Close the document.

document.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = "Output.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a page

PdfPage page = document.Pages.Add();

//Create a PdfGrid

PdfGrid pdfGrid = new PdfGrid();

//Add values to list

List<object> data = new List<object>();

//You can add multiple rows 

Object row1 = new { ID = "E01", Name = "Clay" };

Object row2 = new { ID = "E02", Name = "Thomas" };

data.Add(row1);

data.Add(row2);

//Add list to IEnumerable

IEnumerable<object> dataTable = data;

//Assign data source.

pdfGrid.DataSource = dataTable;

//Set properties to paginate the grid.

PdfGridLayoutFormat layoutFormat = new PdfGridLayoutFormat();

layoutFormat.Break = PdfLayoutBreakType.FitPage;

layoutFormat.Layout = PdfLayoutType.Paginate;

//Draw grid to the page of PDF document.

pdfGrid.Draw(page, new Syncfusion.Drawing.PointF(10, 10), layoutFormat);

//Save the PDF document to stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

//Close the document.

document.Close(true);

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

## Adjust table width automatically

You can automatically adjust the width of the table by enabling the [AllowHorizontalOverflow](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGridStyle.html#Syncfusion_Pdf_Grid_PdfGridStyle_AllowHorizontalOverflow) property of [PdfGridStyle](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGridStyle.html) instance. The following code snippet illustrates this.

{% tabs %}
{% highlight C# %}
//Create a new PDF document
PdfDocument document = new PdfDocument();

//Add new section to the document
PdfSection section = document.Sections.Add();

//Add a page to the section
PdfPage page = section.Pages.Add();

//Initialize PdfGrid
PdfGrid grid = new PdfGrid();

//Create a DataTable
DataTable dataTable = new DataTable();

//Add columns to the DataTable
dataTable.Columns.Add("Employee_ID");
dataTable.Columns.Add("Employee_Name");
dataTable.Columns.Add("Employee_Role");
dataTable.Columns.Add("Employee_DateOfBirth");

//Add rows to the DataTable
dataTable.Rows.Add(new object[] { "E01", "Clay", "Sales Representative", "12/8/1948" });
dataTable.Rows.Add(new object[] { "E02", "Thomas", "Sales Representative", "7/2/1963" });
dataTable.Rows.Add(new object[] { "E03", "Ash", "Sales Manager", "3/4/1955" });
dataTable.Rows.Add(new object[] { "E04", "Andrew", "Vice President, Sales", "2/19/1952" });

//Assign data source to grid
grid.DataSource = dataTable;

//Apply the table style
grid.ApplyBuiltinStyle(PdfGridBuiltinStyle.GridTable5DarkAccent5);

//Allow the horizontal overflow for PdfGrid
grid.Style.AllowHorizontalOverflow = true;

//Draw the PdfGrid on page
grid.Draw(page, PointF.Empty);

//Save the PDF document
document.Save("Output.pdf");

//Close the instance of PdfDocument
document.Close(true);
{% endhighlight %}

{% highlight vb.net %}
'Create a new PDF document
Dim document As PdfDocument = New PdfDocument

'Add new section to the document
Dim section As PdfSection = document.Sections.Add

'Add a page to the section
Dim page As PdfPage = section.Pages.Add

'Initialize PdfGrid
Dim grid As PdfGrid = New PdfGrid

'Create a DataTable
Dim dataTable As DataTable = New DataTable

'Add columns to the DataTable
dataTable.Columns.Add("Employee_ID")
dataTable.Columns.Add("Employee_Name")
dataTable.Columns.Add("Employee_Role")
dataTable.Columns.Add("Employee_DateOfBirth")

'Add rows to the DataTable
dataTable.Rows.Add(New Object() {"E01", "Clay", "Sales Representative", "12/8/1948"})
dataTable.Rows.Add(New Object() {"E02", "Thomas", "Sales Representative", "7/2/1963"})
dataTable.Rows.Add(New Object() {"E03", "Ash", "Sales Manager", "3/4//1955"})
dataTable.Rows.Add(New Object() {"E04", "Andrew", "Vice President, Sales", "2/19/1952"})

'Assign data source to grid
grid.DataSource = dataTable

'Apply the table style
grid.ApplyBuiltinStyle(PdfGridBuiltinStyle.GridTable5DarkAccent5)

'Allow the horizontal overflow for PdfGrid
grid.Style.AllowHorizontalOverflow = True

'Draw the PdfGrid on page
grid.Draw(page, PointF.Empty)

'Save the PDF document
document.Save("Output.pdf")

'Close the instance of PdfDocument
document.Close(True)
{% endhighlight %}

{% highlight UWP %}
//Create a new PDF document
PdfDocument document = new PdfDocument();

//Add new section to the document
PdfSection section = document.Sections.Add();

//Add a page to the section
PdfPage page = section.Pages.Add();

//Initialize PdfGrid
PdfGrid grid = new PdfGrid();

//Add values to list
List<object> data = new List<object>();
Object grid1row1 = new { Employee_ID = "E01", Employee_Name = "Clay", Employee_Role = "Sales Representative", Employee_DateOfBirth = "12/8/1948" };
Object grid1row2 = new { Employee_ID = "E02", Employee_Name = "Thomas", Employee_Role = "Sales Representative", Employee_DateOfBirth = "7/2/1963" };
Object grid1row3 = new { Employee_ID = "E03", Employee_Name = "Ash", Employee_Role = "Sales Manager", Employee_DateOfBirth = "3/4/1955" };
Object grid1row4 = new { Employee_ID = "E04", Employee_Name = "Andrew", Employee_Role = "Vice President, Sales", Employee_DateOfBirth = "2/19/1952" };
data.Add(grid1row1);
data.Add(grid1row2);
data.Add(grid1row3);
data.Add(grid1row4);

//Add list to IEnumerable
IEnumerable<object> dataTable = data;

//Assign data source to grid
grid.DataSource = dataTable;

//Apply the table style
grid.ApplyBuiltinStyle(PdfGridBuiltinStyle.GridTable5DarkAccent5);

//Allow the horizontal overflow for PdfGrid
grid.Style.AllowHorizontalOverflow = true;

//Draw the PdfGrid on page
grid.Draw(page, PointF.Empty);

//Create memory stream
MemoryStream stream = new MemoryStream();

//Open the document in browser after saving it
document.Save(stream);

//Close the instance of PdfDocument
document.Close(true);

//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples
Save(stream, "Output.pdf");
{% endhighlight %}

{% highlight ASP.NET Core %}
//Create a new PDF document
PdfDocument document = new PdfDocument();

//Add new section to the document
PdfSection section = document.Sections.Add();

//Add a page to the section
PdfPage page = section.Pages.Add();

//Initialize PdfGrid
PdfGrid grid = new PdfGrid();

//Add values to list
List<object> data = new List<object>();
Object grid1row1 = new { Employee_ID = "E01", Employee_Name = "Clay", Employee_Role = "Sales Representative", Employee_DateOfBirth = "12/8/1948" };
Object grid1row2 = new { Employee_ID = "E02", Employee_Name = "Thomas", Employee_Role = "Sales Representative", Employee_DateOfBirth = "7/2/1963" };
Object grid1row3 = new { Employee_ID = "E03", Employee_Name = "Ash", Employee_Role = "Sales Manager", Employee_DateOfBirth = "3/4/1955" };
Object grid1row4 = new { Employee_ID = "E04", Employee_Name = "Andrew", Employee_Role = "Vice President, Sales", Employee_DateOfBirth = "2/19/1952" };
data.Add(grid1row1);
data.Add(grid1row2);
data.Add(grid1row3);
data.Add(grid1row4);

//Add list to IEnumerable
IEnumerable<object> dataTable = data;

//Assign data source to grid
grid.DataSource = dataTable;

//Apply the table style
grid.ApplyBuiltinStyle(PdfGridBuiltinStyle.GridTable5DarkAccent5);

//Allow the horizontal overflow for PdfGrid
grid.Style.AllowHorizontalOverflow = true;

//Draw the PdfGrid on page
grid.Draw(page, PointF.Empty);

//Saving the PDF to the MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream);

//Set the position as '0'
stream.Position = 0;

//Download the PDF document in the browser
FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");
fileStreamResult.FileDownloadName = "Output.pdf";
return fileStreamResult;
{% endhighlight %}

{% highlight Xamarin %}
//Create a new PDF document
PdfDocument document = new PdfDocument();

//Add new section to the document
PdfSection section = document.Sections.Add();

//Add a page to the section
PdfPage page = section.Pages.Add();

//Initialize PdfGrid
PdfGrid grid = new PdfGrid();

//Add values to list
List<object> data = new List<object>();
Object grid1row1 = new { Employee_ID = "E01", Employee_Name = "Clay", Employee_Role = "Sales Representative", Employee_DateOfBirth = "12/8/1948" };
Object grid1row2 = new { Employee_ID = "E02", Employee_Name = "Thomas", Employee_Role = "Sales Representative", Employee_DateOfBirth = "7/2/1963" };
Object grid1row3 = new { Employee_ID = "E03", Employee_Name = "Ash", Employee_Role = "Sales Manager", Employee_DateOfBirth = "3/4/1955" };
Object grid1row4 = new { Employee_ID = "E04", Employee_Name = "Andrew", Employee_Role = "Vice President, Sales", Employee_DateOfBirth = "2/19/1952" };
data.Add(grid1row1);
data.Add(grid1row2);
data.Add(grid1row3);
data.Add(grid1row4);

//Add list to IEnumerable
IEnumerable<object> dataTable = data;

//Assign data source to grid
grid.DataSource = dataTable;

//Apply the table style
grid.ApplyBuiltinStyle(PdfGridBuiltinStyle.GridTable5DarkAccent5);

//Allow the horizontal overflow for PdfGrid
grid.Style.AllowHorizontalOverflow = true;

//Draw the PdfGrid on page
grid.Draw(page, PointF.Empty);

//Save the document to the stream
MemoryStream stream = new MemoryStream();
document.Save(stream);

//Close the instance of PdfDocument
document.Close(true);

//Save the stream into PDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}
{% endhighlight %}
{% endtabs %}

## Adding multiple tables

The Essential PDF supports maintaining the position of a PDF grid drawn on PDF page using [PdfGridLayoutResult](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGridLayoutResult.html). It provides the rendered bounds of previously added grid, which can be used to place successive elements without overlapping. You can add multiple PDF grids using the bottom position of previously rendered PDF grid. The following code snippet illustrates this.

{% tabs %}
{% highlight C# %}
//Create a new PDF document
PdfDocument document = new PdfDocument();

//Add a page
PdfPage page = document.Pages.Add();

//Create a new PdfGrid instance
PdfGrid pdfGrid = new PdfGrid();

//Create a DataTable
DataTable dataTable = new DataTable();

//Add columns to the DataTable
dataTable.Columns.Add("ID");
dataTable.Columns.Add("Name");
dataTable.Columns.Add("Salary");

//Add rows to the DataTable
dataTable.Rows.Add(new object[] { "E01", "Clay", "$10,000" });
dataTable.Rows.Add(new object[] { "E02", "Thomas", "$10,500" });
dataTable.Rows.Add(new object[] { "E03", "Simon", "$12,000" });

//Assign data source
pdfGrid.DataSource = dataTable;

//Draw grid on the page of PDF document and store the grid position in PdfGridLayoutResult
PdfGridLayoutResult pdfGridLayoutResult = pdfGrid.Draw(page, new PointF(10, 10));

//Initialize PdfGrid and DataTable
pdfGrid = new PdfGrid();
dataTable = new DataTable();

//Add columns to the DataTable
dataTable.Columns.Add("Name");
dataTable.Columns.Add("Age");
dataTable.Columns.Add("Sex");

//Add rows to the DataTable
dataTable.Rows.Add(new object[] { "Andrew", "21", "Male" });
dataTable.Rows.Add(new object[] { "Steven", "22", "Female" });
dataTable.Rows.Add(new object[] { "Michael", "24", "Male" });

//Assign data source
pdfGrid.DataSource = dataTable;

//Draw the grid on page using previous result
pdfGrid.Draw(page, new PointF(10, pdfGridLayoutResult.Bounds.Bottom + 20));

//Save the document
document.Save("Output.pdf");

//Close the document
document.Close(true);
{% endhighlight %}

{% highlight vb.net %}
'Create a new PDF document
Dim document As PdfDocument = New PdfDocument

'Add a page
Dim page As PdfPage = document.Pages.Add

'Create a new PdfGrid instance
Dim pdfGrid As PdfGrid = New PdfGrid

'Create a DataTable
Dim dataTable As DataTable = New DataTable

'Add columns to the DataTable
dataTable.Columns.Add("ID")
dataTable.Columns.Add("Name")
dataTable.Columns.Add("Salary")

'Add rows to the DataTable
dataTable.Rows.Add(New Object() {"E01", "Clay", "$10,000"})
dataTable.Rows.Add(New Object() {"E02", "Thomas", "$10,500"})
dataTable.Rows.Add(New Object() {"E03", "Simon", "$12,000"})

'Assign data source
pdfGrid.DataSource = dataTable

'Draw grid on the page of PDF document and store the grid position in PdfGridLayoutResult
Dim pdfGridLayoutResult As PdfGridLayoutResult = pdfGrid.Draw(page, New PointF(10, 10))

'Initialize PdfGrid and DataTable
pdfGrid = New PdfGrid
dataTable = New DataTable

'Add columns to the DataTable
dataTable.Columns.Add("Name")
dataTable.Columns.Add("Age")
dataTable.Columns.Add("Sex")

'Add rows to the DataTable
dataTable.Rows.Add(New Object() {"Andrew", "21", "Male"})
dataTable.Rows.Add(New Object() {"Steven", "22", "Female"})
dataTable.Rows.Add(New Object() {"Michael", "24", "Male"})

'Assign data source
pdfGrid.DataSource = dataTable

'Draw the grid on page using previous result
pdfGrid.Draw(page, New PointF(10, (pdfGridLayoutResult.Bounds.Bottom + 20)))

'Save the document
document.Save("Output.pdf")

'Close the document
document.Close(True)
{% endhighlight %}

{% highlight UWP %}
//Create a new PDF document
PdfDocument document = new PdfDocument();

//Add a page
PdfPage page = document.Pages.Add();

//Create a new PdfGrid instance
PdfGrid pdfGrid = new PdfGrid();

//Add values to list
List<object> data = new List<object>();
Object grid1row1 = new { ID = "E01", Name = "Clay", Salary = "$10,000" };
Object grid1row2 = new { ID = "E02", Name = "Thomas", Salary = "$10,500" };
Object grid1row3 = new { ID = "E03", Name = "Simon", Salary = "$12,000" };
data.Add(grid1row1);
data.Add(grid1row2);
data.Add(grid1row3);

//Add list to IEnumerable
IEnumerable<object> dataTable = data;

//Assign data source
pdfGrid.DataSource = dataTable;

//Draw grid on the page of PDF document and store the grid position in PdfGridLayoutResult
PdfGridLayoutResult pdfGridLayoutResult = pdfGrid.Draw(page, new PointF(10, 10));

//Initialize PdfGrid and list
pdfGrid = new PdfGrid();
data = new List<object>();

//Add values to list
Object grid2row1 = new { Name = "Andrew", Age = "21", Sex = "Male" };
Object grid2row2 = new { Name = "Steven", Age = "22", Sex = "Female" };
Object grid2row3 = new { Name = "Michael", Age = "24", Sex = "Male" };
data.Add(grid2row1);
data.Add(grid2row2);
data.Add(grid2row3);

//Add list to IEnumerable
dataTable = data;

//Assign data source
pdfGrid.DataSource = dataTable;

//Draw the grid on page using previously result
pdfGrid.Draw(page, new PointF(10, pdfGridLayoutResult.Bounds.Bottom + 20));

//Create memory stream
MemoryStream stream = new MemoryStream();

//Open the document in browser after saving it
document.Save(stream);

//Close the document
document.Close(true);

//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples
Save(stream, "Output.pdf");
{% endhighlight %}

{% highlight ASP.NET Core %}
//Create a new PDF document
PdfDocument document = new PdfDocument();

//Add a page
PdfPage page = document.Pages.Add();

//Create a new PdfGrid instance
PdfGrid pdfGrid = new PdfGrid();

//Add values to list
List<object> data = new List<object>();
Object grid1row1 = new { ID = "E01", Name = "Clay", Salary = "$10,000" };
Object grid1row2 = new { ID = "E02", Name = "Thomas", Salary = "$10,500" };
Object grid1row3 = new { ID = "E03", Name = "Simon", Salary = "$12,000" };
data.Add(grid1row1);
data.Add(grid1row2);
data.Add(grid1row3);

//Add list to IEnumerable
IEnumerable<object> dataTable = data;

//Assign data source
pdfGrid.DataSource = dataTable;

//Draw grid on the page of PDF document and store the grid position in PdfGridLayoutResult
PdfGridLayoutResult pdfGridLayoutResult = pdfGrid.Draw(page, new PointF(10, 10));

//Initialize PdfGrid and list
pdfGrid = new PdfGrid();
data = new List<object>();

//Add values to the list
Object grid2row1 = new { Name = "Andrew", Age = "21", Sex = "Male" };
Object grid2row2 = new { Name = "Steven", Age = "22", Sex = "Female" };
Object grid2row3 = new { Name = "Michael", Age = "24", Sex = "Male" };
data.Add(grid2row1);
data.Add(grid2row2);
data.Add(grid2row3);

//Add list to IEnumerable
dataTable = data;

//Assign data source
pdfGrid.DataSource = dataTable;

//Draw the grid on page using previous result
pdfGrid.Draw(page, new PointF(10, pdfGridLayoutResult.Bounds.Bottom + 20));

//Saving the PDF to the MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream);

//Set the position as '0'
stream.Position = 0;

//Download the PDF document in the browser
FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");
fileStreamResult.FileDownloadName = "Output.pdf";
return fileStreamResult;
{% endhighlight %}

{% highlight Xamarin %}
//Create a new PDF document
PdfDocument document = new PdfDocument();

//Add a page
PdfPage page = document.Pages.Add();

//Create a new PdfGrid instance
PdfGrid pdfGrid = new PdfGrid();

//Add values to list
List<object> data = new List<object>();
Object grid1row1 = new { ID = "E01", Name = "Clay", Salary = "$10,000" };
Object grid1row2 = new { ID = "E02", Name = "Thomas", Salary = "$10,500" };
Object grid1row3 = new { ID = "E03", Name = "Simon", Salary = "$12,000" };
data.Add(grid1row1);
data.Add(grid1row2);
data.Add(grid1row3);

//Add list to IEnumerable
IEnumerable<object> dataTable = data;

//Assign data source
pdfGrid.DataSource = dataTable;

//Draw grid on the page of PDF document and store the grid position in PdfGridLayoutResult
PdfGridLayoutResult pdfGridLayoutResult = pdfGrid.Draw(page, new PointF(10, 10));

//Initialize PdfGrid and list
pdfGrid = new PdfGrid();
data = new List<object>();

//Add values to list
Object grid2row1 = new { Name = "Andrew", Age = "21", Sex = "Male" };
Object grid2row2 = new { Name = "Steven", Age = "22", Sex = "Female" };
Object grid2row3 = new { Name = "Michael", Age = "24", Sex = "Male" };
data.Add(grid2row1);
data.Add(grid2row2);
data.Add(grid2row3);

//Add list to IEnumerable
dataTable = data;

//Assign data source
pdfGrid.DataSource = dataTable;

//Draw the grid on page using previous result
pdfGrid.Draw(page, new PointF(10, pdfGridLayoutResult.Bounds.Bottom + 20));

//Save the PDF document to stream
MemoryStream stream = new MemoryStream();
document.Save(stream);

//Close the document
document.Close(true);

//Save the stream into PDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}
{% endhighlight %}
{% endtabs %}

## String formatting

Essential PDF supports applying string formatting for whole table, a column in table, a row in table and a cell in table using the [PdfStingFormat](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfStringFormat.html) class.

### String formatting for whole table in PdfGrid

The following code snippet explains how to apply string formatting for whole table in [PdfGrid](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGrid.html).

{% tabs %}
{% highlight C# %}
//Create a new PDF document
PdfDocument document = new PdfDocument();

//Add page to the document
PdfPage page = document.Pages.Add();

//Create a new PdfGrid
PdfGrid grid = new PdfGrid();

//Create a DataTable
DataTable dataTable = new DataTable();

//Add columns to the DataTable
dataTable.Columns.Add("ID");
dataTable.Columns.Add("Name");
dataTable.Columns.Add("Salary");

//Add rows to the DataTable
dataTable.Rows.Add(new object[] { "E01", "Clay", "$10,000" });
dataTable.Rows.Add(new object[] { "E02", "Thomas", "$10,500" });
dataTable.Rows.Add(new object[] { "E03", "Simon", "$12,000" });

//Assign data source
grid.DataSource = dataTable;

//Create and customize the string formats
PdfStringFormat stringFormat = new PdfStringFormat();
stringFormat.Alignment = PdfTextAlignment.Center;
stringFormat.LineAlignment = PdfVerticalAlignment.Middle;
stringFormat.CharacterSpacing = 2f;

//Apply string formatting for whole table
for (int i = 0; i < grid.Columns.Count; i++)
{
    grid.Columns[i].Format = stringFormat;
}

//Draw the PdfGrid on page
grid.Draw(page, new PointF(10, 10));

//Save the document and close the instance of PdfDocument
document.Save("Output.pdf");
document.Close(true);
{% endhighlight %}

{% highlight vb.net %}
'Create a new PDF document
Dim document As PdfDocument = New PdfDocument

'Add page to the document
Dim page As PdfPage = document.Pages.Add

'Create a new PdfGrid
Dim grid As PdfGrid = New PdfGrid

'Create a DataTable
Dim dataTable As DataTable = New DataTable

'Add columns to the DataTable
dataTable.Columns.Add("ID")
dataTable.Columns.Add("Name")
dataTable.Columns.Add("Salary")

'Add rows to the DataTable
dataTable.Rows.Add(New Object() {"E01", "Clay", "$10,000"})
dataTable.Rows.Add(New Object() {"E02", "Thomas", "$10,500"})
dataTable.Rows.Add(New Object() {"E03", "Simon", "$12,000"})

'Assign data source
grid.DataSource = dataTable

'Create and customize the string formats
Dim stringFormat As PdfStringFormat = New PdfStringFormat
stringFormat.Alignment = PdfTextAlignment.Center
stringFormat.LineAlignment = PdfVerticalAlignment.Middle
stringFormat.CharacterSpacing = 2.0F

'Apply string formatting for whole table
Dim i As Integer = 0
For i = 0 To grid.Columns.Count - 1 Step 1
    grid.Columns(i).Format = stringFormat
Next

'Draw the PdfGrid on page
grid.Draw(page, New PointF(10, 10))

'Save the document and close the instance of PdfDocument
document.Save("Output.pdf")
document.Close(True)
{% endhighlight %}

{% highlight UWP %}
//Create a new PDF document
PdfDocument document = new PdfDocument();

//Add page to the document
PdfPage page = document.Pages.Add();

//Create a new PdfGrid
PdfGrid grid = new PdfGrid();

//Add values to list
List<object> data = new List<object>();
Object grid1row1 = new { ID = "E01", Name = "Clay", Salary = "$10,000" };
Object grid1row2 = new { ID = "E02", Name = "Thomas", Salary = "$10,500" };
Object grid1row3 = new { ID = "E03", Name = "Simon", Salary = "$12,000" };
data.Add(grid1row1);
data.Add(grid1row2);
data.Add(grid1row3);

//Add list to IEnumerable
IEnumerable<object> dataTable = data;

//Assign data source
grid.DataSource = dataTable;

//Create and customize the string formats
PdfStringFormat stringFormat = new PdfStringFormat();
stringFormat.Alignment = PdfTextAlignment.Center;
stringFormat.LineAlignment = PdfVerticalAlignment.Middle;
stringFormat.CharacterSpacing = 2f;

//Apply string formatting for whole table
for (int i = 0; i < grid.Columns.Count; i++)
{
    grid.Columns[i].Format = stringFormat;
}

//Draw the PdfGrid on page
grid.Draw(page, new PointF(10, 10));

//Create memory stream
MemoryStream ms = new MemoryStream();

//Open the document in browser after saving it
document.Save(ms);

//Close the document
document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respective code samples
Save(ms, "Output.pdf");
{% endhighlight %}

{% highlight ASP.NET Core %}
//Create a new PDF document
PdfDocument document = new PdfDocument();

//Add page to the document
PdfPage page = document.Pages.Add();

//Create a new PdfGrid
PdfGrid grid = new PdfGrid();

//Add values to list
List<object> data = new List<object>();
Object grid1row1 = new { ID = "E01", Name = "Clay", Salary = "$10,000" };
Object grid1row2 = new { ID = "E02", Name = "Thomas", Salary = "$10,500" };
Object grid1row3 = new { ID = "E03", Name = "Simon", Salary = "$12,000" };
data.Add(grid1row1);
data.Add(grid1row2);
data.Add(grid1row3);

//Add list to IEnumerable
IEnumerable<object> dataTable = data;

//Assign data source
grid.DataSource = dataTable;

//Create and customize the string formats
PdfStringFormat stringFormat = new PdfStringFormat();
stringFormat.Alignment = PdfTextAlignment.Center;
stringFormat.LineAlignment = PdfVerticalAlignment.Middle;
stringFormat.CharacterSpacing = 2f;

//Apply string formatting for whole table
for (int i = 0; i < grid.Columns.Count; i++)
{
    grid.Columns[i].Format = stringFormat;
}

//Draw the PdfGrid on page
grid.Draw(page, new PointF(10, 10));

//Saving the PDF to the MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream);

//Set the position as '0'
stream.Position = 0;

//Download the PDF document in the browser
FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");
fileStreamResult.FileDownloadName = "Output.pdf";
return fileStreamResult;
{% endhighlight %}

{% highlight Xamarin %}
//Create a new PDF document
PdfDocument document = new PdfDocument();

//Add page to the document
PdfPage page = document.Pages.Add();

//Create a new PdfGrid
PdfGrid grid = new PdfGrid();

//Add values to list
List<object> data = new List<object>();
Object grid1row1 = new { ID = "E01", Name = "Clay", Salary = "$10,000" };
Object grid1row2 = new { ID = "E02", Name = "Thomas", Salary = "$10,500" };
Object grid1row3 = new { ID = "E03", Name = "Simon", Salary = "$12,000" };
data.Add(grid1row1);
data.Add(grid1row2);
data.Add(grid1row3);

//Add list to IEnumerable
IEnumerable<object> dataTable = data;

//Assign data source
grid.DataSource = dataTable;

//Create and customize the string formats
PdfStringFormat stringFormat = new PdfStringFormat();
stringFormat.Alignment = PdfTextAlignment.Center;
stringFormat.LineAlignment = PdfVerticalAlignment.Middle;
stringFormat.CharacterSpacing = 2f;

//Apply string formatting for whole table
for (int i = 0; i < grid.Columns.Count; i++)
{
    grid.Columns[i].Format = stringFormat;
}

//Draw the PdfGrid on page
grid.Draw(page, new PointF(10, 10));

//Save the document to the stream
MemoryStream stream = new MemoryStream();
document.Save(stream);

//Close the document
document.Close(true);

//Save the stream into PDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}
{% endhighlight %}
{% endtabs %}

### String formatting for whole table in PdfLightTable

The following code snippet explains how to add string formatting for whole table in [PdfLightTable](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTable.html).

{% tabs %}
{% highlight C# %}
//Create a new PDF document
PdfDocument document = new PdfDocument();

//Add page to the document
PdfPage page = document.Pages.Add();

//Create a PdfLightTable
PdfLightTable lightTable = new PdfLightTable();

//Set the DataSourceType as Direct
lightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns
lightTable.Columns.Add(new PdfColumn("ID"));
lightTable.Columns.Add(new PdfColumn("Name"));
lightTable.Columns.Add(new PdfColumn("Salary"));

//Add rows
lightTable.Rows.Add(new object[] { "E01", "Clay", "$10,000" });
lightTable.Rows.Add(new object[] { "E02", "Thomas", "$10,500" });
lightTable.Rows.Add(new object[] { "E03", "Simon", "$12,000" });

//Enable ShowHeader
lightTable.Style.ShowHeader = true;

//Create and customize the string formats
PdfStringFormat stringFormat = new PdfStringFormat();
stringFormat.Alignment = PdfTextAlignment.Center;
stringFormat.LineAlignment = PdfVerticalAlignment.Middle;
stringFormat.CharacterSpacing = 2f;

//Apply string formatting for whole table
for (int i = 0; i < lightTable.Columns.Count; i++)
{
    lightTable.Columns[i].StringFormat = stringFormat;
}

//Draw the PdfLightTable on page
lightTable.Draw(page, new PointF(10, 10));

//Save the document and close the instance of PdfDocument
document.Save("Output.pdf");
document.Close(true);
{% endhighlight %}

{% highlight vb.net %}
'Create a new PDF document
Dim document As PdfDocument = New PdfDocument

'Add page to the document
Dim page As PdfPage = document.Pages.Add

'Create a PdfLightTable
Dim lightTable As PdfLightTable = New PdfLightTable

'Set the DataSourceType as Direct
lightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect

'Create columns
lightTable.Columns.Add(New PdfColumn("ID"))
lightTable.Columns.Add(New PdfColumn("Name"))
lightTable.Columns.Add(New PdfColumn("Salary"))

'Add rows
lightTable.Rows.Add(New Object() {"E01", "Clay", "$10,000"})
lightTable.Rows.Add(New Object() {"E02", "Thomas", "$10,500"})
lightTable.Rows.Add(New Object() {"E03", "Simon", "$12,000"})

'Enable ShowHeader
lightTable.Style.ShowHeader = True

'Create and customize the string formats
Dim stringFormat As PdfStringFormat = New PdfStringFormat
stringFormat.Alignment = PdfTextAlignment.Center
stringFormat.LineAlignment = PdfVerticalAlignment.Middle
stringFormat.CharacterSpacing = 2.0F

'Apply string formatting for whole table
Dim i As Integer = 0
For i = 0 To lightTable.Columns.Count - 1 Step 1
    lightTable.Columns(i).StringFormat = stringFormat
Next

'Draw the PdfLightTable on page
lightTable.Draw(page, New PointF(10, 10))

'Save the document and close the instance of PdfDocument
document.Save("Output.pdf")
document.Close(True)
{% endhighlight %}

{% highlight UWP %}
//Create a new PDF document
PdfDocument document = new PdfDocument();

//Add page to the document
PdfPage page = document.Pages.Add();

//Create a PdfLightTable
PdfLightTable lightTable = new PdfLightTable();

//Set the DataSourceType as Direct
lightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns
lightTable.Columns.Add(new PdfColumn("ID"));
lightTable.Columns.Add(new PdfColumn("Name"));
lightTable.Columns.Add(new PdfColumn("Salary"));

//Add rows
lightTable.Rows.Add(new object[] { "E01", "Clay", "$10,000" });
lightTable.Rows.Add(new object[] { "E02", "Thomas", "$10,500" });
lightTable.Rows.Add(new object[] { "E03", "Simon", "$12,000" });

//Enable ShowHeader
lightTable.Style.ShowHeader = true;

//Create and customize the string formats
PdfStringFormat stringFormat = new PdfStringFormat();
stringFormat.Alignment = PdfTextAlignment.Center;
stringFormat.LineAlignment = PdfVerticalAlignment.Middle;
stringFormat.CharacterSpacing = 2f;

//Apply string formatting for whole table
for (int i = 0; i < lightTable.Columns.Count; i++)
{
    lightTable.Columns[i].StringFormat = stringFormat;
}

//Draw the PdfLightTable on page
lightTable.Draw(page, new PointF(10, 10));

//Create memory stream
MemoryStream ms = new MemoryStream();

//Open the document in browser after saving it
document.Save(ms);

//Close the document
document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respective code samples
Save(ms, "Output.pdf");
{% endhighlight %}

{% highlight ASP.NET Core %}
//Create a new PDF document
PdfDocument document = new PdfDocument();

//Add page to the document
PdfPage page = document.Pages.Add();

//Create a PdfLightTable
PdfLightTable lightTable = new PdfLightTable();

//Set the DataSourceType as Direct
lightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns
lightTable.Columns.Add(new PdfColumn("ID"));
lightTable.Columns.Add(new PdfColumn("Name"));
lightTable.Columns.Add(new PdfColumn("Salary"));

//Add rows
lightTable.Rows.Add(new object[] { "E01", "Clay", "$10,000" });
lightTable.Rows.Add(new object[] { "E02", "Thomas", "$10,500" });
lightTable.Rows.Add(new object[] { "E03", "Simon", "$12,000" });

//Enable ShowHeader
lightTable.Style.ShowHeader = true;

//Create and customize the string formats
PdfStringFormat stringFormat = new PdfStringFormat();
stringFormat.Alignment = PdfTextAlignment.Center;
stringFormat.LineAlignment = PdfVerticalAlignment.Middle;
stringFormat.CharacterSpacing = 2f;

//Apply string formatting for whole table
for (int i = 0; i < lightTable.Columns.Count; i++)
{
    lightTable.Columns[i].StringFormat = stringFormat;
}

//Draw the PdfLightTable on page
lightTable.Draw(page, new PointF(10, 10));

//Saving the PDF to the MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream);

//Set the position as '0'
stream.Position = 0;

//Download the PDF document in the browser
FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");
fileStreamResult.FileDownloadName = "Output.pdf";
return fileStreamResult;
{% endhighlight %}

{% highlight Xamarin %}
//Create a new PDF document
PdfDocument document = new PdfDocument();

//Add page to the document
PdfPage page = document.Pages.Add();

//Create a PdfLightTable
PdfLightTable lightTable = new PdfLightTable();

//Set the DataSourceType as Direct
lightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns
lightTable.Columns.Add(new PdfColumn("ID"));
lightTable.Columns.Add(new PdfColumn("Name"));
lightTable.Columns.Add(new PdfColumn("Salary"));

//Add rows
lightTable.Rows.Add(new object[] { "E01", "Clay", "$10,000" });
lightTable.Rows.Add(new object[] { "E02", "Thomas", "$10,500" });
lightTable.Rows.Add(new object[] { "E03", "Simon", "$12,000" });

//Enable ShowHeader
lightTable.Style.ShowHeader = true;

//Create and customize the string formats
PdfStringFormat stringFormat = new PdfStringFormat();
stringFormat.Alignment = PdfTextAlignment.Center;
stringFormat.LineAlignment = PdfVerticalAlignment.Middle;
stringFormat.CharacterSpacing = 2f;

//Apply string formatting for whole table
for (int i = 0; i < lightTable.Columns.Count; i++)
{
    lightTable.Columns[i].StringFormat = stringFormat;
}

//Draw the PdfLightTable on page
lightTable.Draw(page, new PointF(10, 10));

//Save the document to the stream
MemoryStream stream = new MemoryStream();
document.Save(stream);

//Close the document
document.Close(true);

//Save the stream into PDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}
{% endhighlight %}
{% endtabs %}

### String formatting to a column in PdfGrid

The following code snippet explains how to add string formatting to a column in [PdfGrid](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGrid.html).

{% tabs %}
{% highlight C# %}
//Create a new PDF document
PdfDocument document = new PdfDocument();

//Add page to the document
PdfPage page = document.Pages.Add();

//Create a new PdfGrid
PdfGrid grid = new PdfGrid();

//Create a DataTable
DataTable dataTable = new DataTable();

//Add columns to the DataTable
dataTable.Columns.Add("ID");
dataTable.Columns.Add("Name");
dataTable.Columns.Add("Salary");

//Add rows to the DataTable
dataTable.Rows.Add(new object[] { "E01", "Clay", "$10,000" });
dataTable.Rows.Add(new object[] { "E02", "Thomas", "$10,500" });
dataTable.Rows.Add(new object[] { "E03", "Simon", "$12,000" });

//Assign data source
grid.DataSource = dataTable;

//create and customize the string formats
PdfStringFormat stringFormat = new PdfStringFormat();
stringFormat.Alignment = PdfTextAlignment.Center;
stringFormat.LineAlignment = PdfVerticalAlignment.Middle;
stringFormat.CharacterSpacing = 2f;

//Apply string formatting to a column
grid.Columns[1].Format = stringFormat;

//Draw the PdfGrid on page
grid.Draw(page, new PointF(10, 10));

//Save the document and close the instance of PdfDocument
document.Save("Output.pdf");
document.Close(true);
{% endhighlight %}

{% highlight vb.net %}
'Create a new PDF document
Dim document As PdfDocument = New PdfDocument

'Add page to the document
Dim page As PdfPage = document.Pages.Add

'Create a new PdfGrid
Dim grid As PdfGrid = New PdfGrid

'Create a DataTable
Dim dataTable As DataTable = New DataTable

'Add columns to the DataTable
dataTable.Columns.Add("ID")
dataTable.Columns.Add("Name")
dataTable.Columns.Add("Salary")

'Add rows to the DataTable
dataTable.Rows.Add(New Object() {"E01", "Clay", "$10,000"})
dataTable.Rows.Add(New Object() {"E02", "Thomas", "$10,500"})
dataTable.Rows.Add(New Object() {"E03", "Simon", "$12,000"})

'Assign data source
grid.DataSource = dataTable

'Create and customize the string formats
Dim stringFormat As PdfStringFormat = New PdfStringFormat
stringFormat.Alignment = PdfTextAlignment.Center
stringFormat.LineAlignment = PdfVerticalAlignment.Middle
stringFormat.CharacterSpacing = 2.0F

'Apply string formatting to a column
grid.Columns(1).Format = stringFormat

'Draw the PdfGrid on page
grid.Draw(page, New PointF(10, 10))

'Save the document and close the instance of PdfDocument
document.Save("Output.pdf")
document.Close(True)
{% endhighlight %}

{% highlight UWP %}
//Create a new PDF document
PdfDocument document = new PdfDocument();

//Add page to the document
PdfPage page = document.Pages.Add();

//Create a new PdfGrid
PdfGrid grid = new PdfGrid();

//Add values to list
List<object> data = new List<object>();
Object grid1row1 = new { ID = "E01", Name = "Clay", Salary = "$10,000" };
Object grid1row2 = new { ID = "E02", Name = "Thomas", Salary = "$10,500" };
Object grid1row3 = new { ID = "E03", Name = "Simon", Salary = "$12,000" };
data.Add(grid1row1);
data.Add(grid1row2);
data.Add(grid1row3);

//Add list to IEnumerable
IEnumerable<object> dataTable = data;

//Assign data source
grid.DataSource = dataTable;

//create and customize the string formats
PdfStringFormat stringFormat = new PdfStringFormat();
stringFormat.Alignment = PdfTextAlignment.Center;
stringFormat.LineAlignment = PdfVerticalAlignment.Middle;
stringFormat.CharacterSpacing = 2f;

//Apply string formatting to a column
grid.Columns[1].Format = stringFormat;

//Draw the PdfGrid on page
grid.Draw(page, new PointF(10, 10));

//Create memory stream
MemoryStream ms = new MemoryStream();

//Open the document in browser after saving it
document.Save(ms);

//Close the document
document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respective code samples
Save(ms, "Output.pdf");
{% endhighlight %}

{% highlight ASP.NET Core %}
//Create a new PDF document
PdfDocument document = new PdfDocument();

//Add page to the document
PdfPage page = document.Pages.Add();

//Create a new PdfGrid
PdfGrid grid = new PdfGrid();

//Add values to list
List<object> data = new List<object>();
Object grid1row1 = new { ID = "E01", Name = "Clay", Salary = "$10,000" };
Object grid1row2 = new { ID = "E02", Name = "Thomas", Salary = "$10,500" };
Object grid1row3 = new { ID = "E03", Name = "Simon", Salary = "$12,000" };
data.Add(grid1row1);
data.Add(grid1row2);
data.Add(grid1row3);

//Add list to IEnumerable
IEnumerable<object> dataTable = data;

//Assign data source
grid.DataSource = dataTable;

//create and customize the string formats
PdfStringFormat stringFormat = new PdfStringFormat();
stringFormat.Alignment = PdfTextAlignment.Center;
stringFormat.LineAlignment = PdfVerticalAlignment.Middle;
stringFormat.CharacterSpacing = 2f;

//Apply string formatting to a column
grid.Columns[1].Format = stringFormat;

//Draw the PdfGrid on page
grid.Draw(page, new PointF(10, 10));

//Saving the PDF to the MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream);

//Set the position as '0'
stream.Position = 0;

//Download the PDF document in the browser
FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");
fileStreamResult.FileDownloadName = "Output.pdf";
return fileStreamResult;
{% endhighlight %}

{% highlight Xamarin %}
//Create a new PDF document
PdfDocument document = new PdfDocument();

//Add page to the document
PdfPage page = document.Pages.Add();

//Create a new PdfGrid
PdfGrid grid = new PdfGrid();

//Add values to list
List<object> data = new List<object>();
Object grid1row1 = new { ID = "E01", Name = "Clay", Salary = "$10,000" };
Object grid1row2 = new { ID = "E02", Name = "Thomas", Salary = "$10,500" };
Object grid1row3 = new { ID = "E03", Name = "Simon", Salary = "$12,000" };
data.Add(grid1row1);
data.Add(grid1row2);
data.Add(grid1row3);

//Add list to IEnumerable
IEnumerable<object> dataTable = data;

//Assign data source
grid.DataSource = dataTable;

//create and customize the string formats
PdfStringFormat stringFormat = new PdfStringFormat();
stringFormat.Alignment = PdfTextAlignment.Center;
stringFormat.LineAlignment = PdfVerticalAlignment.Middle;
stringFormat.CharacterSpacing = 2f;

//Apply string formatting to a column
grid.Columns[1].Format = stringFormat;

//Draw the PdfGrid on page
grid.Draw(page, new PointF(10, 10));

//Save the document to the stream
MemoryStream stream = new MemoryStream();
document.Save(stream);

//Close the document
document.Close(true);

//Save the stream into PDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}
{% endhighlight %}
{% endtabs %}

### String formatting to a column in PdfLightTable

The following code snippet explains how to add string formatting to a column in [PdfLightTable](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTable.html).

{% tabs %}
{% highlight C# %}
//Create a new PDF document
PdfDocument document = new PdfDocument();

//Add page to the document
PdfPage page = document.Pages.Add();

//Create a PdfLightTable
PdfLightTable lightTable = new PdfLightTable();

//Set the DataSourceType as Direct
lightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns
lightTable.Columns.Add(new PdfColumn("ID"));
lightTable.Columns.Add(new PdfColumn("Name"));
lightTable.Columns.Add(new PdfColumn("Salary"));

//Add rows
lightTable.Rows.Add(new object[] { "E01", "Clay", "$10,000" });
lightTable.Rows.Add(new object[] { "E02", "Thomas", "$10,500" });
lightTable.Rows.Add(new object[] { "E03", "Simon", "$12,000" });

//create and customize the string formats
PdfStringFormat stringFormat = new PdfStringFormat();
stringFormat.Alignment = PdfTextAlignment.Center;
stringFormat.LineAlignment = PdfVerticalAlignment.Middle;
stringFormat.CharacterSpacing = 2f;

//Enable ShowHeader
lightTable.Style.ShowHeader = true;

//Apply string format to a column
lightTable.Columns[1].StringFormat = stringFormat;

//Draw PdfLightTable on page
lightTable.Draw(page, new PointF(10, 10));

//Save the document and close the instance of PdfDocument
document.Save("Output.pdf");
document.Close(true);
{% endhighlight %}

{% highlight vb.net %}
'Create a new PDF document
Dim document As PdfDocument = New PdfDocument

'Add page to the document
Dim page As PdfPage = document.Pages.Add

'Create a PdfLightTable
Dim lightTable As PdfLightTable = New PdfLightTable

'Set the DataSourceType as Direct
lightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect

'Create columns
lightTable.Columns.Add(New PdfColumn("ID"))
lightTable.Columns.Add(New PdfColumn("Name"))
lightTable.Columns.Add(New PdfColumn("Salary"))

'Add rows
lightTable.Rows.Add(New Object() {"E01", "Clay", "$10,000"})
lightTable.Rows.Add(New Object() {"E02", "Thomas", "$10,500"})
lightTable.Rows.Add(New Object() {"E03", "Simon", "$12,000"})

'create and customize the string formats
Dim stringFormat As PdfStringFormat = New PdfStringFormat
stringFormat.Alignment = PdfTextAlignment.Center
stringFormat.LineAlignment = PdfVerticalAlignment.Middle
stringFormat.CharacterSpacing = 2.0F

'Enable ShowHeader
lightTable.Style.ShowHeader = True

'Apply string format to a column
lightTable.Columns(1).StringFormat = stringFormat

'Draw PdfLightTable on page
lightTable.Draw(page, New PointF(10, 10))

'Save the document and close the instance of PdfDocument
document.Save("Output.pdf")
document.Close(True)
{% endhighlight %}

{% highlight UWP %}
//Create a new PDF document
PdfDocument document = new PdfDocument();

//Add page to the document
PdfPage page = document.Pages.Add();

//Create a PdfLightTable
PdfLightTable lightTable = new PdfLightTable();

//Set the DataSourceType as Direct
lightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns
lightTable.Columns.Add(new PdfColumn("ID"));
lightTable.Columns.Add(new PdfColumn("Name"));
lightTable.Columns.Add(new PdfColumn("Salary"));

//Add rows
lightTable.Rows.Add(new object[] { "E01", "Clay", "$10,000" });
lightTable.Rows.Add(new object[] { "E02", "Thomas", "$10,500" });
lightTable.Rows.Add(new object[] { "E03", "Simon", "$12,000" });

//create and customize the string formats
PdfStringFormat stringFormat = new PdfStringFormat();
stringFormat.Alignment = PdfTextAlignment.Center;
stringFormat.LineAlignment = PdfVerticalAlignment.Middle;
stringFormat.CharacterSpacing = 2f;

//Enable ShowHeader
lightTable.Style.ShowHeader = true;

//Apply string format to a column
lightTable.Columns[1].StringFormat = stringFormat;

//Draw PdfLightTable on page
lightTable.Draw(page, new PointF(10, 10));

//Create memory stream
MemoryStream ms = new MemoryStream();

//Open the document in browser after saving it
document.Save(ms);

//Close the document
document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respective code samples
Save(ms, "Output.pdf");
{% endhighlight %}

{% highlight ASP.NET Core %}
//Create a new PDF document
PdfDocument document = new PdfDocument();

//Add page to the document
PdfPage page = document.Pages.Add();

//Create a PdfLightTable
PdfLightTable lightTable = new PdfLightTable();

//Set the DataSourceType as Direct
lightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns
lightTable.Columns.Add(new PdfColumn("ID"));
lightTable.Columns.Add(new PdfColumn("Name"));
lightTable.Columns.Add(new PdfColumn("Salary"));

//Add rows
lightTable.Rows.Add(new object[] { "E01", "Clay", "$10,000" });
lightTable.Rows.Add(new object[] { "E02", "Thomas", "$10,500" });
lightTable.Rows.Add(new object[] { "E03", "Simon", "$12,000" });

//create and customize the string formats
PdfStringFormat stringFormat = new PdfStringFormat();
stringFormat.Alignment = PdfTextAlignment.Center;
stringFormat.LineAlignment = PdfVerticalAlignment.Middle;
stringFormat.CharacterSpacing = 2f;

//Enable ShowHeader
lightTable.Style.ShowHeader = true;

//Apply string format to a column
lightTable.Columns[1].StringFormat = stringFormat;

//Draw PdfLightTable on page
lightTable.Draw(page, new PointF(10, 10));

//Saving the PDF to the MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream);

//Set the position as '0'
stream.Position = 0;

//Download the PDF document in the browser
FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");
fileStreamResult.FileDownloadName = "Output.pdf";
return fileStreamResult;
{% endhighlight %}

{% highlight Xamarin %}
//Create a new PDF document
PdfDocument document = new PdfDocument();

//Add page to the document
PdfPage page = document.Pages.Add();

//Create a PdfLightTable
PdfLightTable lightTable = new PdfLightTable();

//Set the DataSourceType as Direct
lightTable.DataSourceType = PdfLightTableDataSourceType.TableDirect;

//Create columns
lightTable.Columns.Add(new PdfColumn("ID"));
lightTable.Columns.Add(new PdfColumn("Name"));
lightTable.Columns.Add(new PdfColumn("Salary"));

//Add rows
lightTable.Rows.Add(new object[] { "E01", "Clay", "$10,000" });
lightTable.Rows.Add(new object[] { "E02", "Thomas", "$10,500" });
lightTable.Rows.Add(new object[] { "E03", "Simon", "$12,000" });

//create and customize the string formats
PdfStringFormat stringFormat = new PdfStringFormat();
stringFormat.Alignment = PdfTextAlignment.Center;
stringFormat.LineAlignment = PdfVerticalAlignment.Middle;
stringFormat.CharacterSpacing = 2f;

//Enable ShowHeader
lightTable.Style.ShowHeader = true;

//Apply string format to a column
lightTable.Columns[1].StringFormat = stringFormat;

//Draw PdfLightTable on page
lightTable.Draw(page, new PointF(10, 10));

//Save the document to the stream
MemoryStream stream = new MemoryStream();
document.Save(stream);

//Close the document
document.Close(true);

//Save the stream into PDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}
{% endhighlight %}
{% endtabs %}

### String formatting for a cell in PdfGrid

The following code snippet illustrates how to add string formatting for a cell in [PdfGrid](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGrid.html).

{% tabs %}
{% highlight C# %}
//Create a new PDF document
PdfDocument document = new PdfDocument();

//Add page to the PdfDocument
PdfPage page = document.Pages.Add();

//Create a new PdfGrid
PdfGrid grid = new PdfGrid();

//Create a DataTable
DataTable dataTable = new DataTable();

//Add columns to the DataTable
dataTable.Columns.Add("ID");
dataTable.Columns.Add("Name");
dataTable.Columns.Add("Salary");

//Add rows to the DataTable
dataTable.Rows.Add(new object[] { "E01", "Clay", "$10,000" });
dataTable.Rows.Add(new object[] { "E02", "Thomas", "$10,500" });
dataTable.Rows.Add(new object[] { "E03", "Simon", "$12,000" });

//Assign data source
grid.DataSource = dataTable;

//Create and customize the string formats
PdfStringFormat stringFormat = new PdfStringFormat();
stringFormat.Alignment = PdfTextAlignment.Center;
stringFormat.LineAlignment = PdfVerticalAlignment.Middle;
stringFormat.CharacterSpacing = 2f;

//Apply string format to a cell
grid.Rows[2].Cells[1].StringFormat = stringFormat;

//Draw the PdfGrid on page
grid.Draw(page, new PointF(10, 10));

//Save the document and close the instance of PdfDocument
document.Save("Output.pdf");
document.Close(true);
{% endhighlight %}

{% highlight vb.net %}
'Create a new PDF document
Dim document As PdfDocument = New PdfDocument

'Add page to the PdfDocument
Dim page As PdfPage = document.Pages.Add

'Create a new PdfGrid
Dim grid As PdfGrid = New PdfGrid

'Create a DataTable
Dim dataTable As DataTable = New DataTable

'Add columns to the DataTable
dataTable.Columns.Add("ID")
dataTable.Columns.Add("Name")
dataTable.Columns.Add("Salary")

'Add rows to the DataTable
dataTable.Rows.Add(New Object() {"E01", "Clay", "$10,000"})
dataTable.Rows.Add(New Object() {"E02", "Thomas", "$10,500"})
dataTable.Rows.Add(New Object() {"E03", "Simon", "$12,000"})

'Assign data source
grid.DataSource = dataTable

'Create and customize the string formats
Dim stringFormat As PdfStringFormat = New PdfStringFormat
stringFormat.Alignment = PdfTextAlignment.Center
stringFormat.LineAlignment = PdfVerticalAlignment.Middle
stringFormat.CharacterSpacing = 2.0F

'Apply string format to a cell
grid.Rows(2).Cells(1).StringFormat = stringFormat

'Draw the PdfGrid on page
grid.Draw(page, New PointF(10, 10))

'Save the document and close the instance of PdfDocument
document.Save("Output.pdf")
document.Close(True)
{% endhighlight %}

{% highlight UWP %}
//Create a new PDF document
PdfDocument document = new PdfDocument();

//Add page to the PdfDocument
PdfPage page = document.Pages.Add();

//Create a new PdfGrid
PdfGrid grid = new PdfGrid();

//Add values to list
List<object> data = new List<object>();
Object grid1row1 = new { ID = "E01", Name = "Clay", Salary = "$10,000" };
Object grid1row2 = new { ID = "E02", Name = "Thomas", Salary = "$10,500" };
Object grid1row3 = new { ID = "E03", Name = "Simon", Salary = "$12,000" };
data.Add(grid1row1);
data.Add(grid1row2);
data.Add(grid1row3);

//Add list to IEnumerable
IEnumerable<object> dataTable = data;

//Assign data source
grid.DataSource = dataTable;

//create and customize the string formats
PdfStringFormat stringFormat = new PdfStringFormat();
stringFormat.Alignment = PdfTextAlignment.Center;
stringFormat.LineAlignment = PdfVerticalAlignment.Middle;
stringFormat.CharacterSpacing = 2f;

//Apply string format to a cell
grid.Rows[2].Cells[1].StringFormat = stringFormat;

//Draw the PdfGrid on page
grid.Draw(page, new PointF(10, 10));

//Create memory stream
MemoryStream ms = new MemoryStream();

//Open the document in browser after saving it
document.Save(ms);

//Close the document
document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respective code samples
Save(ms, "Output.pdf");
{% endhighlight %}

{% highlight ASP.NET Core %}
//Create a new PDF document
PdfDocument document = new PdfDocument();

//Add page to the PdfDocument
PdfPage page = document.Pages.Add();

//Create a new PdfGrid
PdfGrid grid = new PdfGrid();

//Add values to list
List<object> data = new List<object>();
Object grid1row1 = new { ID = "E01", Name = "Clay", Salary = "$10,000" };
Object grid1row2 = new { ID = "E02", Name = "Thomas", Salary = "$10,500" };
Object grid1row3 = new { ID = "E03", Name = "Simon", Salary = "$12,000" };
data.Add(grid1row1);
data.Add(grid1row2);
data.Add(grid1row3);

//Add list to IEnumerable
IEnumerable<object> dataTable = data;

//Assign data source
grid.DataSource = dataTable;

//create and customize the string formats
PdfStringFormat stringFormat = new PdfStringFormat();
stringFormat.Alignment = PdfTextAlignment.Center;
stringFormat.LineAlignment = PdfVerticalAlignment.Middle;
stringFormat.CharacterSpacing = 2f;

//Apply string format to a cell
grid.Rows[2].Cells[1].StringFormat = stringFormat;

//Draw the PdfGrid on page
grid.Draw(page, new PointF(10, 10));

//Saving the PDF to the MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream);

//Set the position as '0'
stream.Position = 0;

//Download the PDF document in the browser
FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");
fileStreamResult.FileDownloadName = "Output.pdf";
return fileStreamResult;
{% endhighlight %}

{% highlight Xamarin %}
//Create a new PDF document
PdfDocument document = new PdfDocument();

//Add page to the PdfDocument
PdfPage page = document.Pages.Add();

//Create a new PdfGrid
PdfGrid grid = new PdfGrid();

//Add values to list
List<object> data = new List<object>();
Object grid1row1 = new { ID = "E01", Name = "Clay", Salary = "$10,000" };
Object grid1row2 = new { ID = "E02", Name = "Thomas", Salary = "$10,500" };
Object grid1row3 = new { ID = "E03", Name = "Simon", Salary = "$12,000" };
data.Add(grid1row1);
data.Add(grid1row2);
data.Add(grid1row3);

//Add list to IEnumerable
IEnumerable<object> dataTable = data;

//Assign data source
grid.DataSource = dataTable;

//create and customize the string formats
PdfStringFormat stringFormat = new PdfStringFormat();
stringFormat.Alignment = PdfTextAlignment.Center;
stringFormat.LineAlignment = PdfVerticalAlignment.Middle;
stringFormat.CharacterSpacing = 2f;

//Apply string format to a cell
grid.Rows[2].Cells[1].StringFormat = stringFormat;

//Draw the PdfGrid on page
grid.Draw(page, new PointF(10, 10));

//Save the document to the stream
MemoryStream stream = new MemoryStream();
document.Save(stream);

//Close the document
document.Close(true);

//Save the stream into PDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}
{% endhighlight %}
{% endtabs %}

### String formatting for a row in PdfGrid

The following code snippet illustrates how to add string formatting for a row in [PdfGrid](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGrid.html).

{% tabs %}
{% highlight C# %}
//Create a new PDF document
PdfDocument document = new PdfDocument();

//Add page to the document
PdfPage page = document.Pages.Add();

//Create a new PdfGrid
PdfGrid grid = new PdfGrid();

//Create a DataTable
DataTable dataTable = new DataTable();

//Add columns to the DataTable
dataTable.Columns.Add("ID");
dataTable.Columns.Add("Name");
dataTable.Columns.Add("Salary");

//Add rows to the DataTable
dataTable.Rows.Add(new object[] { "E01", "Clay", "$10,000" });
dataTable.Rows.Add(new object[] { "E02", "Thomas", "$10,500" });
dataTable.Rows.Add(new object[] { "E03", "Simon", "$12,000" });

//Assign data source
grid.DataSource = dataTable;

//Create and customize the string formats
PdfStringFormat stringFormat = new PdfStringFormat();
stringFormat.Alignment = PdfTextAlignment.Center;
stringFormat.LineAlignment = PdfVerticalAlignment.Middle;
stringFormat.CharacterSpacing = 2f;

//Assign string format to a row
for (int i = 0; i < grid.Columns.Count; i++)
{
    grid.Rows[2].Cells[i].StringFormat = stringFormat;
}

//Draw the PdfGrid on page
grid.Draw(page, new PointF(10, 10));

//Save the document and close the instance of PdfDocument
document.Save("Output.pdf");
document.Close(true);
{% endhighlight %}

{% highlight vb.net %}
'Create a new PDF document
Dim document As PdfDocument = New PdfDocument

'Add page to the document
Dim page As PdfPage = document.Pages.Add

'Create a new PdfGrid
Dim grid As PdfGrid = New PdfGrid

'Create a DataTable
Dim dataTable As DataTable = New DataTable

'Add columns to the DataTable
dataTable.Columns.Add("ID")
dataTable.Columns.Add("Name")
dataTable.Columns.Add("Salary")

'Add rows to the DataTable
dataTable.Rows.Add(New Object() {"E01", "Clay", "$10,000"})
dataTable.Rows.Add(New Object() {"E02", "Thomas", "$10,500"})
dataTable.Rows.Add(New Object() {"E03", "Simon", "$12,000"})

'Assign data source
grid.DataSource = dataTable

'Create and customize the string formats
Dim stringFormat As PdfStringFormat = New PdfStringFormat
stringFormat.Alignment = PdfTextAlignment.Center
stringFormat.LineAlignment = PdfVerticalAlignment.Middle
stringFormat.CharacterSpacing = 2.0F

'Assign string format to a row
Dim i As Integer = 0
For i = 0 To grid.Columns.Count - 1 Step 1
    grid.Rows(2).Cells(i).StringFormat = stringFormat
Next

'Draw the PdfGrid on page
grid.Draw(page, New PointF(10, 10))

'Save the document and close the instance of PdfDocument
document.Save("Output.pdf")
document.Close(True)
{% endhighlight %}

{% highlight UWP %}
//Create a new PDF document
PdfDocument document = new PdfDocument();

//Add page to the PdfDocument
PdfPage page = document.Pages.Add();

//Create a new PdfGrid
PdfGrid grid = new PdfGrid();

//Add values to list
List<object> data = new List<object>();
Object grid1row1 = new { ID = "E01", Name = "Clay", Salary = "$10,000" };
Object grid1row2 = new { ID = "E02", Name = "Thomas", Salary = "$10,500" };
Object grid1row3 = new { ID = "E03", Name = "Simon", Salary = "$12,000" };
data.Add(grid1row1);
data.Add(grid1row2);
data.Add(grid1row3);

//Add list to IEnumerable
IEnumerable<object> dataTable = data;

//Assign data source
grid.DataSource = dataTable;

//create and customize the string formats
PdfStringFormat stringFormat = new PdfStringFormat();
stringFormat.Alignment = PdfTextAlignment.Center;
stringFormat.LineAlignment = PdfVerticalAlignment.Middle;
stringFormat.CharacterSpacing = 2f;

//Assign string format to a row
for (int i = 0; i < grid.Columns.Count; i++)
{
    grid.Rows[2].Cells[i].StringFormat = stringFormat;
}

//Draw the PdfGrid on page
grid.Draw(page, new PointF(10, 10));

//Create memory stream
MemoryStream ms = new MemoryStream();

//Open the document in browser after saving it
document.Save(ms);

//Close the document
document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respective code samples
Save(ms, "Output.pdf");
{% endhighlight %}

{% highlight ASP.NET Core %}
//Create a new PDF document
PdfDocument document = new PdfDocument();

//Add page to the PdfDocument
PdfPage page = document.Pages.Add();

//Create a new PdfGrid
PdfGrid grid = new PdfGrid();

//Add values to list
List<object> data = new List<object>();
Object grid1row1 = new { ID = "E01", Name = "Clay", Salary = "$10,000" };
Object grid1row2 = new { ID = "E02", Name = "Thomas", Salary = "$10,500" };
Object grid1row3 = new { ID = "E03", Name = "Simon", Salary = "$12,000" };
data.Add(grid1row1);
data.Add(grid1row2);
data.Add(grid1row3);

//Add list to IEnumerable
IEnumerable<object> dataTable = data;

//Assign data source
grid.DataSource = dataTable;

//create and customize the string formats
PdfStringFormat stringFormat = new PdfStringFormat();
stringFormat.Alignment = PdfTextAlignment.Center;
stringFormat.LineAlignment = PdfVerticalAlignment.Middle;
stringFormat.CharacterSpacing = 2f;

//Assign string format to a row
for (int i = 0; i < grid.Columns.Count; i++)
{
    grid.Rows[2].Cells[i].StringFormat = stringFormat;
}

//Draw the PdfGrid on page
grid.Draw(page, new PointF(10, 10));

//Saving the PDF to the MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream);

//Set the position as '0'
stream.Position = 0;

//Download the PDF document in the browser
FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");
fileStreamResult.FileDownloadName = "Output.pdf";
return fileStreamResult;
{% endhighlight %}

{% highlight Xamarin %}
//Create a new PDF document
PdfDocument document = new PdfDocument();

//Add page to the PdfDocument
PdfPage page = document.Pages.Add();

//Create a new PdfGrid
PdfGrid grid = new PdfGrid();

//Add values to list
List<object> data = new List<object>();
Object grid1row1 = new { ID = "E01", Name = "Clay", Salary = "$10,000" };
Object grid1row2 = new { ID = "E02", Name = "Thomas", Salary = "$10,500" };
Object grid1row3 = new { ID = "E03", Name = "Simon", Salary = "$12,000" };
data.Add(grid1row1);
data.Add(grid1row2);
data.Add(grid1row3);

//Add list to IEnumerable
IEnumerable<object> dataTable = data;

//Assign data source
grid.DataSource = dataTable;

//create and customize the string formats
PdfStringFormat stringFormat = new PdfStringFormat();
stringFormat.Alignment = PdfTextAlignment.Center;
stringFormat.LineAlignment = PdfVerticalAlignment.Middle;
stringFormat.CharacterSpacing = 2f;

//Assign string format to a row
for (int i = 0; i < grid.Columns.Count; i++)
{
    grid.Rows[2].Cells[i].StringFormat = stringFormat;
}

//Draw the PdfGrid on page
grid.Draw(page, new PointF(10, 10));

//Save the document to the stream
MemoryStream stream = new MemoryStream();
document.Save(stream);

//Close the document
document.Close(true);

//Save the stream into PDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}
{% endhighlight %}
{% endtabs %}

## Row and Column spanning

Essential PDF supports both row spanning and column spanning in a PDF table.

### Row spanning in PdfGrid

You can span a row in [PdfGrid](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGrid.html) by using the [RowSpan](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGridCell.html#Syncfusion_Pdf_Grid_PdfGridCell_RowSpan) property of [PdfGridCell](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGridCell.html). The following code snippet illustrates this.

{% tabs %}
{% highlight C# %}
//Create a new PDF document
PdfDocument document = new PdfDocument();

//Create the page
PdfPage page = document.Pages.Add();

//Create a PdfGrid
PdfGrid pdfGrid = new PdfGrid();

//Create and customize the string formats
PdfStringFormat format = new PdfStringFormat();
format.Alignment = PdfTextAlignment.Center;
format.LineAlignment = PdfVerticalAlignment.Middle;

//Add columns to PdfGrid
pdfGrid.Columns.Add(5);

//Add rows to PdfGrid
for (int i = 0; i < pdfGrid.Columns.Count; i++)
{
    PdfGridRow row = pdfGrid.Rows.Add();
    row.Height = 20;
}

//Add RowSpan
PdfGridCell gridCell = pdfGrid.Rows[1].Cells[3];
gridCell.RowSpan = 3;
gridCell.StringFormat = format;
gridCell.Value = "Row Span";
gridCell.Style.BackgroundBrush = PdfBrushes.Yellow;

//Draw the PdfGrid
pdfGrid.Draw(page, new PointF(10, 10));

//Save the document
document.Save("Output.pdf");

//Close the document
document.Close(true);
{% endhighlight %}

{% highlight vb.net %}
'Create a new PDF document
Dim document As PdfDocument = New PdfDocument

'Create the page
Dim page As PdfPage = document.Pages.Add

'Create a PdfGrid
Dim pdfGrid As PdfGrid = New PdfGrid

'Create and customize the string formats
Dim format As PdfStringFormat = New PdfStringFormat
format.Alignment = PdfTextAlignment.Center
format.LineAlignment = PdfVerticalAlignment.Middle

'Add columns to PdfGrid
pdfGrid.Columns.Add(5)

'Add rows to PdfGrid
For i = 0 To pdfGrid.Columns.Count - 1 Step 1
    Dim row As PdfGridRow = pdfGrid.Rows.Add
    row.Height = 20
Next

'Add RowSpan
Dim gridCell As PdfGridCell = pdfGrid.Rows(1).Cells(3)
gridCell.RowSpan = 3
gridCell.StringFormat = format
gridCell.Value = "Row Span"
gridCell.Style.BackgroundBrush = PdfBrushes.Yellow

'Draw the PdfGrid
pdfGrid.Draw(page, New PointF(10, 10))

'Save the document
document.Save("Output.pdf")

'Close the document
document.Close(True)
{% endhighlight %}

{% highlight UWP %}
//Create a new PDF document
PdfDocument document = new PdfDocument();

//Create the page
PdfPage page = document.Pages.Add();

//Create a PdfGrid
PdfGrid pdfGrid = new PdfGrid();

//Create and customize the string formats
PdfStringFormat format = new PdfStringFormat();
format.Alignment = PdfTextAlignment.Center;
format.LineAlignment = PdfVerticalAlignment.Middle;

//Add columns to PdfGrid
pdfGrid.Columns.Add(5);

//Add rows to PdfGrid
for (int i = 0; i < pdfGrid.Columns.Count; i++)
{
    PdfGridRow row = pdfGrid.Rows.Add();
    row.Height = 20;
}

//Add RowSpan
PdfGridCell gridCell = pdfGrid.Rows[1].Cells[3];
gridCell.RowSpan = 3;
gridCell.StringFormat = format;
gridCell.Value = "Row Span";
gridCell.Style.BackgroundBrush = PdfBrushes.Yellow;

//Draw the PdfGrid
pdfGrid.Draw(page, new PointF(10, 10));

//Create memory stream
MemoryStream ms = new MemoryStream();

//Open the document in browser after saving it
document.Save(ms);

//Close the document
document.Close(true);

//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples
Save(ms, "Sample.pdf");
{% endhighlight %}

{% highlight ASP.NET Core %}
//Create a new PDF document
PdfDocument document = new PdfDocument();

//Create the page
PdfPage page = document.Pages.Add();

//Create a PdfGrid
PdfGrid pdfGrid = new PdfGrid();

//Create and customize the string formats
PdfStringFormat format = new PdfStringFormat();
format.Alignment = PdfTextAlignment.Center;
format.LineAlignment = PdfVerticalAlignment.Middle;

//Add columns to PdfGrid
pdfGrid.Columns.Add(5);

//Add rows to PdfGrid
for (int i = 0; i < pdfGrid.Columns.Count; i++)
{
    PdfGridRow row = pdfGrid.Rows.Add();
    row.Height = 20;
}

//Add RowSpan
PdfGridCell gridCell = pdfGrid.Rows[1].Cells[3];
gridCell.RowSpan = 3;
gridCell.StringFormat = format;
gridCell.Value = "Row Span";
gridCell.Style.BackgroundBrush = PdfBrushes.Yellow;

//Draw the PdfGrid
pdfGrid.Draw(page, new PointF(10, 10));

//Saving the PDF to the MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream);

//Set the position as '0'
stream.Position = 0;

//Download the PDF document in the browser
FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");
fileStreamResult.FileDownloadName = "Sample.pdf";
return fileStreamResult;
{% endhighlight %}

{% highlight Xamarin %}
//Create a new PDF document
PdfDocument document = new PdfDocument();

//Create the page
PdfPage page = document.Pages.Add();

//Create a PdfGrid
PdfGrid pdfGrid = new PdfGrid();

//Create and customize the string formats
PdfStringFormat format = new PdfStringFormat();
format.Alignment = PdfTextAlignment.Center;
format.LineAlignment = PdfVerticalAlignment.Middle;

//Add columns to PdfGrid
pdfGrid.Columns.Add(5);

//Add rows to PdfGrid
for (int i = 0; i < pdfGrid.Columns.Count; i++)
{
    PdfGridRow row = pdfGrid.Rows.Add();
    row.Height = 20;
}

//Add RowSpan
PdfGridCell gridCell = pdfGrid.Rows[1].Cells[3];
gridCell.RowSpan = 3;
gridCell.StringFormat = format;
gridCell.Value = "Row Span";
gridCell.Style.BackgroundBrush = PdfBrushes.Yellow;

//Draw the PdfGrid
pdfGrid.Draw(page, new PointF(10, 10));

//Save the document to the stream
MemoryStream stream = new MemoryStream();
document.Save(stream);

//Close the document
document.Close(true);

//Save the stream into PDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}
{% endhighlight %}
{% endtabs %}

### Column spanning in PdfGrid

You can span a column in [PdfGrid](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGrid.html) by using the [ColumnSpan](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGridCell.html#Syncfusion_Pdf_Grid_PdfGridCell_ColumnSpan) property of [PdfGridCell](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGridCell.html). The following code snippet explains this.

{% tabs %}
{% highlight C# %}
//Create a new PDF document
PdfDocument document = new PdfDocument();

//Create the page
PdfPage page = document.Pages.Add();

//Create a PdfGrid
PdfGrid pdfGrid = new PdfGrid();

//Create and customize the string formats
PdfStringFormat format = new PdfStringFormat();
format.Alignment = PdfTextAlignment.Center;
format.LineAlignment = PdfVerticalAlignment.Middle;

//Add columns to PdfGrid
pdfGrid.Columns.Add(5);

//Add rows to PdfGrid
for (int i = 0; i < pdfGrid.Columns.Count; i++)
{
    PdfGridRow row = pdfGrid.Rows.Add();
    row.Height = 20;
}

//Add ColumnSpan
PdfGridCell gridCell = pdfGrid.Rows[1].Cells[0];
gridCell.ColumnSpan = 2;
gridCell.StringFormat = format;
gridCell.Value = "Column Span";
gridCell.Style.BackgroundBrush = PdfBrushes.Yellow;

//Draw the PdfGrid
pdfGrid.Draw(page, new PointF(10, 10));

//Save the document
document.Save("Output.pdf");

//Close the document
document.Close(true);
{% endhighlight %}

{% highlight vb.net %}
'Create a new PDF document
Dim document As PdfDocument = New PdfDocument

'Create the page
Dim page As PdfPage = document.Pages.Add

'Create a PdfGrid
Dim pdfGrid As PdfGrid = New PdfGrid

'Create and customize the string formats
Dim format As PdfStringFormat = New PdfStringFormat
format.Alignment = PdfTextAlignment.Center
format.LineAlignment = PdfVerticalAlignment.Middle

'Add columns to PdfGrid
pdfGrid.Columns.Add(5)

'Add rows to PdfGrid
For i = 0 To pdfGrid.Columns.Count - 1 Step 1
    Dim row As PdfGridRow = pdfGrid.Rows.Add
    row.Height = 20
Next

'Add ColumnSpan
Dim gridCell As PdfGridCell = pdfGrid.Rows(1).Cells(0)
gridCell.ColumnSpan = 2
gridCell.StringFormat = format
gridCell.Value = "Column Span"
gridCell.Style.BackgroundBrush = PdfBrushes.Yellow

'Draw the PdfGrid
pdfGrid.Draw(page, New PointF(10, 10))

'Save the document
document.Save("Output.pdf")

'Close the document
document.Close(True)
{% endhighlight %}

{% highlight UWP %}
//Create a new PDF document
PdfDocument document = new PdfDocument();

//Create the page
PdfPage page = document.Pages.Add();

//Create a PdfGrid
PdfGrid pdfGrid = new PdfGrid();

//Create and customize the string formats
PdfStringFormat format = new PdfStringFormat();
format.Alignment = PdfTextAlignment.Center;
format.LineAlignment = PdfVerticalAlignment.Middle;

//Add columns to PdfGrid
pdfGrid.Columns.Add(5);

//Add rows to PdfGrid
for (int i = 0; i < pdfGrid.Columns.Count; i++)
{
    PdfGridRow row = pdfGrid.Rows.Add();
    row.Height = 20;
}

//Add ColumnSpan
PdfGridCell gridCell = pdfGrid.Rows[1].Cells[0];
gridCell.ColumnSpan = 2;
gridCell.StringFormat = format;
gridCell.Value = "Column Span";
gridCell.Style.BackgroundBrush = PdfBrushes.Yellow;

//Draw the PdfGrid
pdfGrid.Draw(page, new PointF(10, 10));

//Create memory stream
MemoryStream ms = new MemoryStream();

//Open the document in browser after saving it
document.Save(ms);

//Close the document
document.Close(true);

//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples
Save(ms, "Sample.pdf");
{% endhighlight %}

{% highlight ASP.NET Core %}
//Create a new PDF document
PdfDocument document = new PdfDocument();

//Create the page
PdfPage page = document.Pages.Add();

//Create a PdfGrid
PdfGrid pdfGrid = new PdfGrid();

//Create and customize the string formats
PdfStringFormat format = new PdfStringFormat();
format.Alignment = PdfTextAlignment.Center;
format.LineAlignment = PdfVerticalAlignment.Middle;

//Add columns to PdfGrid
pdfGrid.Columns.Add(5);

//Add rows to PdfGrid
for (int i = 0; i < pdfGrid.Columns.Count; i++)
{
    PdfGridRow row = pdfGrid.Rows.Add();
    row.Height = 20;
}

//Add ColumnSpan
PdfGridCell gridCell = pdfGrid.Rows[1].Cells[0];
gridCell.ColumnSpan = 2;
gridCell.StringFormat = format;
gridCell.Value = "Column Span";
gridCell.Style.BackgroundBrush = PdfBrushes.Yellow;

//Draw the PdfGrid
pdfGrid.Draw(page, new PointF(10, 10));

//Saving the PDF to the MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream);

//Set the position as '0'
stream.Position = 0;

//Download the PDF document in the browser
FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");
fileStreamResult.FileDownloadName = "Sample.pdf";
return fileStreamResult;
{% endhighlight %}

{% highlight Xamarin %}
//Create a new PDF document
PdfDocument document = new PdfDocument();

//Create the page
PdfPage page = document.Pages.Add();

//Create a PdfGrid
PdfGrid pdfGrid = new PdfGrid();

//Create and customize the string formats
PdfStringFormat format = new PdfStringFormat();
format.Alignment = PdfTextAlignment.Center;
format.LineAlignment = PdfVerticalAlignment.Middle;

//Add columns to PdfGrid
pdfGrid.Columns.Add(5);

//Add rows to PdfGrid
for (int i = 0; i < pdfGrid.Columns.Count; i++)
{
    PdfGridRow row = pdfGrid.Rows.Add();
    row.Height = 20;
}

//Add ColumnSpan
PdfGridCell gridCell = pdfGrid.Rows[1].Cells[0];
gridCell.ColumnSpan = 2;
gridCell.StringFormat = format;
gridCell.Value = "Column Span";
gridCell.Style.BackgroundBrush = PdfBrushes.Yellow;

//Draw the PdfGrid
pdfGrid.Draw(page, new PointF(10, 10));

//Save the document to the stream
MemoryStream stream = new MemoryStream();
document.Save(stream);

//Close the document
document.Close(true);

//Save the stream into PDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}
{% endhighlight %}
{% endtabs %}

## Table cell styles

Essential PDF allows you to add different styles like background color using [BackgroundBrush](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGridStyleBase.html#Syncfusion_Pdf_Grid_PdfGridStyleBase_BackgroundBrush), background image using [BackgroundImage](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGridCellStyle.html#Syncfusion_Pdf_Grid_PdfGridCellStyle_BackgroundImage), border using [Borders](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGridCellStyle.html#Syncfusion_Pdf_Grid_PdfGridCellStyle_Borders), cell dimension by setting row [Height](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGridRow.html#Syncfusion_Pdf_Grid_PdfGridRow_Height) and column [Width](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGridColumn.html#Syncfusion_Pdf_Grid_PdfGridColumn_Width), along with spanning through [RowSpan](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGridCell.html#Syncfusion_Pdf_Grid_PdfGridCell_RowSpan) and [ColumnSpan](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGridCell.html#Syncfusion_Pdf_Grid_PdfGridCell_ColumnSpan).

The following code snippet explains how to add different cell styles to a cell in [PdfGrid](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGrid.html).

{% tabs %}
{% highlight C# %}
//Create a new PDF document
PdfDocument pdfDocument = new PdfDocument();
PdfPage pdfPage = pdfDocument.Pages.Add();

//Create a new PdfGrid instance
PdfGrid pdfGrid = new PdfGrid();

//Create a DataTable
DataTable dataTable = new DataTable();

//Add columns to the DataTable
dataTable.Columns.Add("ID");
dataTable.Columns.Add("Name");
dataTable.Columns.Add("Salary");

//Add rows to the DataTable
dataTable.Rows.Add(new object[] { "E01", "Clay", "$10,000" });
dataTable.Rows.Add(new object[] { "E02", "Thomas", "$10,500" });
dataTable.Rows.Add(new object[] { "E03", "Simon", "$12,000" });

//Assign data source to PdfGrid
pdfGrid.DataSource = dataTable;

//Assign row height and column width
pdfGrid.Rows[1].Height = 50;
pdfGrid.Columns[1].Width = 100;

//Initialize PdfGridCellStyle and set background color
PdfGridCellStyle gridCellStyle = new PdfGridCellStyle();
gridCellStyle.BackgroundBrush = PdfBrushes.Yellow;

//Assign background color to a PdfGridCell
PdfGridCell gridCell = pdfGrid.Rows[0].Cells[0];
gridCell.Style = gridCellStyle;

//Initialize PdfGridCellStyle and set background image
gridCellStyle = new PdfGridCellStyle();
gridCellStyle.BackgroundImage = PdfImage.FromFile("Autumn Leaves.jpg");

//Assign background image to a PdfGridCell
gridCell = pdfGrid.Rows[1].Cells[1];
gridCell.Style = gridCellStyle;
gridCell.ImagePosition = PdfGridImagePosition.Fit;

//Initialize PdfGridCellStyle and set the border color
gridCellStyle = new PdfGridCellStyle();
gridCellStyle.Borders.All = PdfPens.Red;

//Assign the border color to a PdfGridCell
gridCell = pdfGrid.Rows[2].Cells[2];
gridCell.Style = gridCellStyle;

//Initialize PdfGridCellStyle and set text color
gridCellStyle = new PdfGridCellStyle();
gridCellStyle.TextBrush = PdfBrushes.DarkBlue;

//Assign text color to a PdfGridCell
gridCell = pdfGrid.Rows[0].Cells[2];
gridCell.Style = gridCellStyle;

//Set the column span
pdfGrid.Rows[2].Cells[0].ColumnSpan = 2;

//Initialize PdfStringFormat and set the properties
PdfStringFormat stringFormat = new PdfStringFormat();
stringFormat.Alignment = PdfTextAlignment.Center;
stringFormat.LineAlignment = PdfVerticalAlignment.Middle;

//Set the PdfStringFormat to PdfGridCell
gridCell = pdfGrid.Rows[2].Cells[0];
gridCell.StringFormat = stringFormat;

//Draw the table in the PDF page
pdfGrid.Draw(pdfPage, new PointF(10, 10));

//Save the document
pdfDocument.Save("Output.pdf");

//Close the instance of PdfDocument
pdfDocument.Close(true);
{% endhighlight %}

{% highlight vb.net %}
'Create a new PDF document
Dim pdfDocument As PdfDocument = New PdfDocument
Dim pdfPage As PdfPage = pdfDocument.Pages.Add

'Create a new PdfGrid instance
Dim pdfGrid As PdfGrid = New PdfGrid

'Create a DataTable
Dim dataTable As DataTable = New DataTable

'Add columns to the DataTable
dataTable.Columns.Add("ID")
dataTable.Columns.Add("Name")
dataTable.Columns.Add("Salary")

'Add rows to the DataTable
dataTable.Rows.Add(New Object() {"E01", "Clay", "$10,000"})
dataTable.Rows.Add(New Object() {"E02", "Thomas", "$10,500"})
dataTable.Rows.Add(New Object() {"E03", "Simon", "$12,000"})

'Assign data source to PdfGrid
pdfGrid.DataSource = dataTable

'Assign row height and column width
pdfGrid.Rows(1).Height = 50
pdfGrid.Columns(1).Width = 100

'Initialize PdfGridCellStyle and set background color
Dim gridCellStyle As PdfGridCellStyle = New PdfGridCellStyle
gridCellStyle.BackgroundBrush = PdfBrushes.Yellow

'Assign background color to a PdfGridCell
Dim gridCell As PdfGridCell = pdfGrid.Rows(0).Cells(0)
gridCell.Style = gridCellStyle

'Initialize PdfGridCellStyle and set background image
gridCellStyle = New PdfGridCellStyle
gridCellStyle.BackgroundImage = PdfImage.FromFile("Autumn Leaves.jpg")

'Assign background image to a PdfGridCell
gridCell = pdfGrid.Rows(1).Cells(1)
gridCell.Style = gridCellStyle
gridCell.ImagePosition = PdfGridImagePosition.Fit

'Initialize PdfGridCellStyle and set the border color
gridCellStyle = New PdfGridCellStyle
gridCellStyle.Borders.All = PdfPens.Red

'Assign the border color to a PdfGridCell
gridCell = pdfGrid.Rows(2).Cells(2)
gridCell.Style = gridCellStyle

'Initialize PdfGridCellStyle and set text color
gridCellStyle = New PdfGridCellStyle
gridCellStyle.TextBrush = PdfBrushes.DarkBlue

'Assign text color to a PdfGridCell
gridCell = pdfGrid.Rows(0).Cells(2)
gridCell.Style = gridCellStyle

'Set the column span
pdfGrid.Rows(2).Cells(0).ColumnSpan = 2

'Initialize PdfStringFormat and set the properties
Dim stringFormat As PdfStringFormat = New PdfStringFormat
stringFormat.Alignment = PdfTextAlignment.Center
stringFormat.LineAlignment = PdfVerticalAlignment.Middle

'Set the PdfStringFormat to PdfGridCell
gridCell = pdfGrid.Rows(2).Cells(0)
gridCell.StringFormat = stringFormat

'Draw the table in the PDF page
pdfGrid.Draw(pdfPage, New PointF(10, 10))

'Save the document
pdfDocument.Save("Output.pdf")

'Close the instance of PdfDocument
pdfDocument.Close(True)
{% endhighlight %}

{% highlight UWP %}
//Create a new PDF document
PdfDocument pdfDocument = new PdfDocument();
PdfPage pdfPage = pdfDocument.Pages.Add();

//Create a new PdfGrid instance
PdfGrid pdfGrid = new PdfGrid();

//Add values to list
List<object> data = new List<object>();
Object grid1row1 = new { ID = "E01", Name = "Clay", Salary = "$10,000" };
Object grid1row2 = new { ID = "E02", Name = "Thomas", Salary = "$10,500" };
Object grid1row3 = new { ID = "E03", Name = "Simon", Salary = "$12,000" };
data.Add(grid1row1);
data.Add(grid1row2);
data.Add(grid1row3);

//Add list to IEnumerable
IEnumerable<object> dataTable = data;

//Assign data source to PdfGrid
pdfGrid.DataSource = dataTable;

//Assign row height and column width
pdfGrid.Rows[1].Height = 50;
pdfGrid.Columns[1].Width = 100;

//Initialize PdfGridCellStyle and set background color
PdfGridCellStyle gridCellStyle = new PdfGridCellStyle();
gridCellStyle.BackgroundBrush = PdfBrushes.Yellow;

//Assign background color to a PdfGridCell
PdfGridCell gridCell = pdfGrid.Rows[0].Cells[0];
gridCell.Style = gridCellStyle;

//Initialize PdfGridCellStyle and set background image
Stream imageStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Data.Autumn Leaves.jpg");
gridCellStyle = new PdfGridCellStyle();
gridCellStyle.BackgroundImage = PdfImage.FromStream(imageStream);

//Assign background image to a PdfGridCell
gridCell = pdfGrid.Rows[1].Cells[1];
gridCell.Style = gridCellStyle;
gridCell.ImagePosition = PdfGridImagePosition.Fit;

//Initialize PdfGridCellStyle and set the border color
gridCellStyle = new PdfGridCellStyle();
gridCellStyle.Borders.All = PdfPens.Red;

//Assign the border color to a PdfGridCell
gridCell = pdfGrid.Rows[2].Cells[2];
gridCell.Style = gridCellStyle;

//Initialize PdfGridCellStyle and set text color
gridCellStyle = new PdfGridCellStyle();
gridCellStyle.TextBrush = PdfBrushes.DarkBlue;

//Assign text color to a PdfGridCell
gridCell = pdfGrid.Rows[0].Cells[2];
gridCell.Style = gridCellStyle;

//Set the column span
pdfGrid.Rows[2].Cells[0].ColumnSpan = 2;

//Initialize PdfStringFormat and set the properties
PdfStringFormat stringFormat = new PdfStringFormat();
stringFormat.Alignment = PdfTextAlignment.Center;
stringFormat.LineAlignment = PdfVerticalAlignment.Middle;

//Set the PdfStringFormat to PdfGridCell
gridCell = pdfGrid.Rows[2].Cells[0];
gridCell.StringFormat = stringFormat;

//Draw the table in the PDF page
pdfGrid.Draw(pdfPage, new PointF(10, 10));

//Create memory stream
MemoryStream ms = new MemoryStream();

//Open the document in browser after saving it
pdfDocument.Save(ms);

//Close the document
pdfDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples
Save(ms, "Output.pdf");
{% endhighlight %}

{% highlight ASP.NET Core %}
//Create a new PDF document
PdfDocument pdfDocument = new PdfDocument();
PdfPage pdfPage = pdfDocument.Pages.Add();

//Create a new PdfGrid instance
PdfGrid pdfGrid = new PdfGrid();

//Add values to list
List<object> data = new List<object>();
Object grid1row1 = new { ID = "E01", Name = "Clay", Salary = "$10,000" };
Object grid1row2 = new { ID = "E02", Name = "Thomas", Salary = "$10,500" };
Object grid1row3 = new { ID = "E03", Name = "Simon", Salary = "$12,000" };
data.Add(grid1row1);
data.Add(grid1row2);
data.Add(grid1row3);

//Add list to IEnumerable
IEnumerable<object> dataTable = data;

//Assign data source to PdfGrid
pdfGrid.DataSource = dataTable;

//Assign row height and column width
pdfGrid.Rows[1].Height = 50;
pdfGrid.Columns[1].Width = 100;

//Initialize PdfGridCellStyle and set background color
PdfGridCellStyle gridCellStyle = new PdfGridCellStyle();
gridCellStyle.BackgroundBrush = PdfBrushes.Yellow;

//Assign background color to a PdfGridCell
PdfGridCell gridCell = pdfGrid.Rows[0].Cells[0];
gridCell.Style = gridCellStyle;

//Initialize PdfGridCellStyle and set background image
FileStream imageStream = new FileStream("Autumn Leaves.jpg", FileMode.Open);
gridCellStyle = new PdfGridCellStyle();
gridCellStyle.BackgroundImage = PdfImage.FromStream(imageStream);

//Assign background image to a PdfGridCell
gridCell = pdfGrid.Rows[1].Cells[1];
gridCell.Style = gridCellStyle;
gridCell.ImagePosition = PdfGridImagePosition.Fit;

//Initialize PdfGridCellStyle and set the border color
gridCellStyle = new PdfGridCellStyle();
gridCellStyle.Borders.All = PdfPens.Red;

//Assign the border color to a PdfGridCell
gridCell = pdfGrid.Rows[2].Cells[2];
gridCell.Style = gridCellStyle;

//Initialize PdfGridCellStyle and set text color
gridCellStyle = new PdfGridCellStyle();
gridCellStyle.TextBrush = PdfBrushes.DarkBlue;

//Assign text color to a PdfGridCell
gridCell = pdfGrid.Rows[0].Cells[2];
gridCell.Style = gridCellStyle;

//Set the column span
pdfGrid.Rows[2].Cells[0].ColumnSpan = 2;

//Initialize PdfStringFormat and set the properties
PdfStringFormat stringFormat = new PdfStringFormat();
stringFormat.Alignment = PdfTextAlignment.Center;
stringFormat.LineAlignment = PdfVerticalAlignment.Middle;

//Set the PdfStringFormat to PdfGridCell
gridCell = pdfGrid.Rows[2].Cells[0];
gridCell.StringFormat = stringFormat;

//Draw the table in the PDF page
pdfGrid.Draw(pdfPage, new PointF(10, 10));

//Saving the PDF to the MemoryStream
MemoryStream stream = new MemoryStream();
pdfDocument.Save(stream);

//Set the position as '0'
stream.Position = 0;

//Download the PDF document in the browser
FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");
fileStreamResult.FileDownloadName = "Output.pdf";
return fileStreamResult;
{% endhighlight %}

{% highlight Xamarin %}
//Create a new PDF document
PdfDocument pdfDocument = new PdfDocument();
PdfPage pdfPage = pdfDocument.Pages.Add();

//Create a new PdfGrid instance
PdfGrid pdfGrid = new PdfGrid();

//Add values to list
List<object> data = new List<object>();
Object grid1row1 = new { ID = "E01", Name = "Clay", Salary = "$10,000" };
Object grid1row2 = new { ID = "E02", Name = "Thomas", Salary = "$10,500" };
Object grid1row3 = new { ID = "E03", Name = "Simon", Salary = "$12,000" };
data.Add(grid1row1);
data.Add(grid1row2);
data.Add(grid1row3);

//Add list to IEnumerable
IEnumerable<object> dataTable = data;

//Assign data source to PdfGrid
pdfGrid.DataSource = dataTable;

//Assign row height and column width
pdfGrid.Rows[1].Height = 50;
pdfGrid.Columns[1].Width = 100;

//Initialize PdfGridCellStyle and set background color
PdfGridCellStyle gridCellStyle = new PdfGridCellStyle();
gridCellStyle.BackgroundBrush = PdfBrushes.Yellow;

//Assign background color to a PdfGridCell
PdfGridCell gridCell = pdfGrid.Rows[0].Cells[0];
gridCell.Style = gridCellStyle;

//Initialize PdfGridCellStyle and set background image
Stream imageStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Data.Autumn Leaves.jpg");
gridCellStyle = new PdfGridCellStyle();
gridCellStyle.BackgroundImage = PdfImage.FromStream(imageStream);

//Assign background image to a PdfGridCell
gridCell = pdfGrid.Rows[1].Cells[1];
gridCell.Style = gridCellStyle;
gridCell.ImagePosition = PdfGridImagePosition.Fit;

//Initialize PdfGridCellStyle and set the border color
gridCellStyle = new PdfGridCellStyle();
gridCellStyle.Borders.All = PdfPens.Red;

//Assign the border color to a PdfGridCell
gridCell = pdfGrid.Rows[2].Cells[2];
gridCell.Style = gridCellStyle;

//Initialize PdfGridCellStyle and set text color
gridCellStyle = new PdfGridCellStyle();
gridCellStyle.TextBrush = PdfBrushes.DarkBlue;

//Assign text color to a PdfGridCell
gridCell = pdfGrid.Rows[0].Cells[2];
gridCell.Style = gridCellStyle;

//Set the column span
pdfGrid.Rows[2].Cells[0].ColumnSpan = 2;

//Initialize PdfStringFormat and set the properties
PdfStringFormat stringFormat = new PdfStringFormat();
stringFormat.Alignment = PdfTextAlignment.Center;
stringFormat.LineAlignment = PdfVerticalAlignment.Middle;

//Set the PdfStringFormat to PdfGridCell
gridCell = pdfGrid.Rows[2].Cells[0];
gridCell.StringFormat = stringFormat;

//Draw the table in the PDF page
pdfGrid.Draw(pdfPage, new PointF(10, 10));

//Save the document to the stream
MemoryStream stream = new MemoryStream();
pdfDocument.Save(stream);

//Close the document
pdfDocument.Close(true);

//Save the stream into PDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}
{% endhighlight %}
{% endtabs %}

## Table row style

Essential PDF supports applying different styles to a row in [PdfGrid](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGrid.html) by using [PdfGridCellStyle](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGridCellStyle.html) and [PdfGridRow](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGridRow.html) instances. The following code snippet explains this.

{% tabs %}
{% highlight C# %}
//Create a new PDF document
PdfDocument pdfDocument = new PdfDocument();
PdfPage pdfPage = pdfDocument.Pages.Add();

//Create a new PdfGrid instance
PdfGrid pdfGrid = new PdfGrid();

//Create a DataTable
DataTable dataTable = new DataTable();

//Add columns to the DataTable
dataTable.Columns.Add("ID");
dataTable.Columns.Add("Name");
dataTable.Columns.Add("Salary");

//Add rows to the DataTable
dataTable.Rows.Add(new object[] { "E01", "Clay", "$10,000" });
dataTable.Rows.Add(new object[] { "E02", "Thomas", "$10,500" });
dataTable.Rows.Add(new object[] { "E03", "Simon", "$12,000" });

//Assign data source to PdfGrid
pdfGrid.DataSource = dataTable;

//Assign row height and column width
pdfGrid.Rows[1].Height = 50;
pdfGrid.Columns[1].Width = 100;

//Initialize PdfStringFormat and set the properties
PdfStringFormat stringFormat = new PdfStringFormat();
stringFormat.Alignment = PdfTextAlignment.Center;
stringFormat.LineAlignment = PdfVerticalAlignment.Middle;
stringFormat.CharacterSpacing = 2f;

//Initialize PdfGridCellStyle. Set background color and string format
PdfGridCellStyle gridCellStyle = new PdfGridCellStyle();
gridCellStyle.BackgroundBrush = PdfBrushes.Yellow;
gridCellStyle.StringFormat = stringFormat;

//Initialize PdfGridRow and apply PdfGridCellStyle to the row
PdfGridRow gridRow = pdfGrid.Rows[0];            
gridRow.ApplyStyle(gridCellStyle);

//Initialize PdfGridCellStyle and set background image
gridCellStyle = new PdfGridCellStyle();
gridCellStyle.BackgroundImage = PdfImage.FromFile("Autumn Leaves.jpg");

//Initialize PdfGridRow and apply PdfGridCellStyle to the row
gridRow = pdfGrid.Rows[1];
gridRow.ApplyStyle(gridCellStyle);

//Initialize PdfGridCellStyle. Set the border color and text color
gridCellStyle = new PdfGridCellStyle();
gridCellStyle.Borders.All = PdfPens.Red;
gridCellStyle.TextBrush = PdfBrushes.DarkBlue;

//Initialize PdfGridRow and apply PdfGridCellStyle to the row
gridRow = pdfGrid.Rows[2];
gridRow.ApplyStyle(gridCellStyle);

//Draw the table in the PDF page
pdfGrid.Draw(pdfPage, new PointF(10, 10));

//Save the document
pdfDocument.Save("Output.pdf");

//Close the instance of PdfDocument
pdfDocument.Close(true);
{% endhighlight %}

{% highlight vb.net %}
'Create a new PDF document
Dim pdfDocument As PdfDocument = New PdfDocument
Dim pdfPage As PdfPage = pdfDocument.Pages.Add

'Create a new PdfGrid instance
Dim pdfGrid As PdfGrid = New PdfGrid

'Create a DataTable
Dim dataTable As DataTable = New DataTable

'Add columns to the DataTable
dataTable.Columns.Add("ID")
dataTable.Columns.Add("Name")
dataTable.Columns.Add("Salary")

'Add rows to the DataTable
dataTable.Rows.Add(New Object() {"E01", "Clay", "$10,000"})
dataTable.Rows.Add(New Object() {"E02", "Thomas", "$10,500"})
dataTable.Rows.Add(New Object() {"E03", "Simon", "$12,000"})

'Assign data source to PdfGrid
pdfGrid.DataSource = dataTable

'Assign row height and column width
pdfGrid.Rows(1).Height = 50
pdfGrid.Columns(1).Width = 100

'Initialize PdfStringFormat and set the properties
Dim stringFormat As PdfStringFormat = New PdfStringFormat
stringFormat.Alignment = PdfTextAlignment.Center
stringFormat.LineAlignment = PdfVerticalAlignment.Middle
stringFormat.CharacterSpacing = 2.0F

'Initialize PdfGridCellStyle. Set background color and string format
Dim gridCellStyle As PdfGridCellStyle = New PdfGridCellStyle
gridCellStyle.BackgroundBrush = PdfBrushes.Yellow
gridCellStyle.StringFormat = stringFormat

'Initialize PdfGridRow and apply PdfGridCellStyle to the row
Dim gridRow As PdfGridRow = pdfGrid.Rows(0)
gridRow.ApplyStyle(gridCellStyle)

'Initialize PdfGridCellStyle and set background image
gridCellStyle = New PdfGridCellStyle
gridCellStyle.BackgroundImage = PdfImage.FromFile("Autumn Leaves.jpg")

'Initialize PdfGridRow and apply PdfGridCellStyle to the row
gridRow = pdfGrid.Rows(1)
gridRow.ApplyStyle(gridCellStyle)

'Initialize PdfGridCellStyle. Set the border color and text color
gridCellStyle = New PdfGridCellStyle
gridCellStyle.Borders.All = PdfPens.Red
gridCellStyle.TextBrush = PdfBrushes.DarkBlue

'Initialize PdfGridRow and apply PdfGridCellStyle to the row
gridRow = pdfGrid.Rows(2)
gridRow.ApplyStyle(gridCellStyle)

'Draw the table in the PDF page
pdfGrid.Draw(pdfPage, New PointF(10, 10))

'Save the document
pdfDocument.Save("Output.pdf")

'Close the instance of PdfDocument
pdfDocument.Close(True)
{% endhighlight %}

{% highlight UWP %}
//Create a new PDF document
PdfDocument pdfDocument = new PdfDocument();
PdfPage pdfPage = pdfDocument.Pages.Add();

//Create a new PdfGrid instance
PdfGrid pdfGrid = new PdfGrid();

//Add values to list
List<object> data = new List<object>();
Object grid1row1 = new { ID = "E01", Name = "Clay", Salary = "$10,000" };
Object grid1row2 = new { ID = "E02", Name = "Thomas", Salary = "$10,500" };
Object grid1row3 = new { ID = "E03", Name = "Simon", Salary = "$12,000" };
data.Add(grid1row1);
data.Add(grid1row2);
data.Add(grid1row3);

//Add list to IEnumerable
IEnumerable<object> dataTable = data;

//Assign data source to PdfGrid
pdfGrid.DataSource = dataTable;

//Assign row height and column width
pdfGrid.Rows[1].Height = 50;
pdfGrid.Columns[1].Width = 100;

//Initialize PdfStringFormat and set the properties
PdfStringFormat stringFormat = new PdfStringFormat();
stringFormat.Alignment = PdfTextAlignment.Center;
stringFormat.LineAlignment = PdfVerticalAlignment.Middle;
stringFormat.CharacterSpacing = 2f;

//Initialize PdfGridCellStyle. Set background color and string format
PdfGridCellStyle gridCellStyle = new PdfGridCellStyle();
gridCellStyle.BackgroundBrush = PdfBrushes.Yellow;
gridCellStyle.StringFormat = stringFormat;

//Initialize PdfGridRow and apply PdfGridCellStyle to the row
PdfGridRow gridRow = pdfGrid.Rows[0];
gridRow.ApplyStyle(gridCellStyle);

//Initialize PdfGridCellStyle and set background image
Stream imageStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Data.Autumn Leaves.jpg");
gridCellStyle = new PdfGridCellStyle();
gridCellStyle.BackgroundImage = PdfImage.FromStream(imageStream);

//Initialize PdfGridRow and apply PdfGridCellStyle to the row
gridRow = pdfGrid.Rows[1];
gridRow.ApplyStyle(gridCellStyle);

//Initialize PdfGridCellStyle. Set the border color and text color
gridCellStyle = new PdfGridCellStyle();
gridCellStyle.Borders.All = PdfPens.Red;
gridCellStyle.TextBrush = PdfBrushes.DarkBlue;

//Initialize PdfGridRow and apply PdfGridCellStyle to the row
gridRow = pdfGrid.Rows[2];
gridRow.ApplyStyle(gridCellStyle);

//Draw the table in the PDF page
pdfGrid.Draw(pdfPage, new PointF(10, 10));

//Create memory stream
MemoryStream ms = new MemoryStream();

//Open the document in browser after saving it
pdfDocument.Save(ms);

//Close the document
pdfDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to the PDF/UWP section for respective code samples
Save(ms, "Output.pdf");
{% endhighlight %}

{% highlight ASP.NET Core %}
//Create a new PDF document
PdfDocument pdfDocument = new PdfDocument();
PdfPage pdfPage = pdfDocument.Pages.Add();

//Create a new PdfGrid instance
PdfGrid pdfGrid = new PdfGrid();

//Add values to list
List<object> data = new List<object>();
Object grid1row1 = new { ID = "E01", Name = "Clay", Salary = "$10,000" };
Object grid1row2 = new { ID = "E02", Name = "Thomas", Salary = "$10,500" };
Object grid1row3 = new { ID = "E03", Name = "Simon", Salary = "$12,000" };
data.Add(grid1row1);
data.Add(grid1row2);
data.Add(grid1row3);

//Add list to IEnumerable
IEnumerable<object> dataTable = data;

//Assign data source to PdfGrid
pdfGrid.DataSource = dataTable;

//Assign row height and column width
pdfGrid.Rows[1].Height = 50;
pdfGrid.Columns[1].Width = 100;

//Initialize PdfStringFormat and set the properties
PdfStringFormat stringFormat = new PdfStringFormat();
stringFormat.Alignment = PdfTextAlignment.Center;
stringFormat.LineAlignment = PdfVerticalAlignment.Middle;
stringFormat.CharacterSpacing = 2f;

//Initialize PdfGridCellStyle. Set background color and string format
PdfGridCellStyle gridCellStyle = new PdfGridCellStyle();
gridCellStyle.BackgroundBrush = PdfBrushes.Yellow;
gridCellStyle.StringFormat = stringFormat;

//Initialize PdfGridRow and apply PdfGridCellStyle to the row
PdfGridRow gridRow = pdfGrid.Rows[0];
gridRow.ApplyStyle(gridCellStyle);

//Initialize PdfGridCellStyle and set background image
FileStream imageStream = new FileStream("Autumn Leaves.jpg", FileMode.Open);
gridCellStyle = new PdfGridCellStyle();
gridCellStyle.BackgroundImage = PdfImage.FromStream(imageStream);

//Initialize PdfGridRow and apply PdfGridCellStyle to the row
gridRow = pdfGrid.Rows[1];
gridRow.ApplyStyle(gridCellStyle);

//Initialize PdfGridCellStyle. Set the border color and text color
gridCellStyle = new PdfGridCellStyle();
gridCellStyle.Borders.All = PdfPens.Red;
gridCellStyle.TextBrush = PdfBrushes.DarkBlue;

//Initialize PdfGridRow and apply PdfGridCellStyle to the row
gridRow = pdfGrid.Rows[2];
gridRow.ApplyStyle(gridCellStyle);

//Draw the table in the PDF page
pdfGrid.Draw(pdfPage, new PointF(10, 10));

//Saving the PDF to the MemoryStream
MemoryStream stream = new MemoryStream();
pdfDocument.Save(stream);

//Set the position as '0'
stream.Position = 0;

//Download the PDF document in the browser
FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");
fileStreamResult.FileDownloadName = "Output.pdf";
return fileStreamResult;
{% endhighlight %}

{% highlight Xamarin %}
//Create a new PDF document
PdfDocument pdfDocument = new PdfDocument();
PdfPage pdfPage = pdfDocument.Pages.Add();

//Create a new PdfGrid instance
PdfGrid pdfGrid = new PdfGrid();

//Add values to list
List<object> data = new List<object>();
Object grid1row1 = new { ID = "E01", Name = "Clay", Salary = "$10,000" };
Object grid1row2 = new { ID = "E02", Name = "Thomas", Salary = "$10,500" };
Object grid1row3 = new { ID = "E03", Name = "Simon", Salary = "$12,000" };
data.Add(grid1row1);
data.Add(grid1row2);
data.Add(grid1row3);

//Add list to IEnumerable
IEnumerable<object> dataTable = data;

//Assign data source to PdfGrid
pdfGrid.DataSource = dataTable;

//Assign row height and column width
pdfGrid.Rows[1].Height = 50;
pdfGrid.Columns[1].Width = 100;

//Initialize PdfStringFormat and set the properties
PdfStringFormat stringFormat = new PdfStringFormat();
stringFormat.Alignment = PdfTextAlignment.Center;
stringFormat.LineAlignment = PdfVerticalAlignment.Middle;
stringFormat.CharacterSpacing = 2f;

//Initialize PdfGridCellStyle. Set background color and string format
PdfGridCellStyle gridCellStyle = new PdfGridCellStyle();
gridCellStyle.BackgroundBrush = PdfBrushes.Yellow;
gridCellStyle.StringFormat = stringFormat;

//Initialize PdfGridRow and apply PdfGridCellStyle to the row
PdfGridRow gridRow = pdfGrid.Rows[0];
gridRow.ApplyStyle(gridCellStyle);

//Initialize PdfGridCellStyle and set background image
Stream imageStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Data.Autumn Leaves.jpg");
gridCellStyle = new PdfGridCellStyle();
gridCellStyle.BackgroundImage = PdfImage.FromStream(imageStream);

//Initialize PdfGridRow and apply PdfGridCellStyle to the row
gridRow = pdfGrid.Rows[1];
gridRow.ApplyStyle(gridCellStyle);

//Initialize PdfGridCellStyle. Set the border color and text color
gridCellStyle = new PdfGridCellStyle();
gridCellStyle.Borders.All = PdfPens.Red;
gridCellStyle.TextBrush = PdfBrushes.DarkBlue;

//Initialize PdfGridRow and apply PdfGridCellStyle to the row
gridRow = pdfGrid.Rows[2];
gridRow.ApplyStyle(gridCellStyle);

//Draw the table in the PDF page
pdfGrid.Draw(pdfPage, new PointF(10, 10));

//Save the document to the stream
MemoryStream stream = new MemoryStream();
pdfDocument.Save(stream);

//Close the document
pdfDocument.Close(true);

//Save the stream into PDF file
//The operation in Save under Xamarin varies between Windows Phone, Android, and iOS platforms. Refer to the PDF/Xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pdf", "application/pdf", stream);
}
{% endhighlight %}
{% endtabs %}

## Difference between PdfLightTable and PdfGrid

Both the [PdfGrid](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Grid.PdfGrid.html) and [PdfLightTable](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Tables.PdfLightTable.html) models are supported across all the platforms and the below table explains the level of customizations both the models provide.

<table>
    <thead>
        <tr>
            <th>
                Features
            </th>
            <th>
                PdfLightTable
            </th>
            <th>
                PdfGrid
            </th>
    </thead>
    <tbody>
        <tr>
            <td align="center" colspan="3">
                {{ '**Formatting**' | markdownify }}
            </td>
        </tr>
        <tr>
            <td>
                Row
            </td>
            <td>
                No direct API, possible through events.
            </td>
            <td>
                Yes
            </td>
        </tr>
        <tr>
            <td>
                Column
            </td>
            <td>
                Yes (StringFormat)
            </td>
            <td>
                Yes (StringFormat)
            </td>
        </tr>
        <tr>
            <td>
                Cell
            </td>
            <td>
                No direct API for single cell formatting, possible through events.
            </td>
            <td>
                Yes
            </td>
        </tr>
        <tr>
            <td align="center" colspan="3">
                {{ '**Others**' | markdownify }}
            </td>
        </tr>
        <tr>
            <td>
                Row span
            </td>
            <td>
                No
            </td>
            <td>
                Yes
            </td>
        </tr>
        <tr>
            <td>
                Column span
            </td>
            <td>
                No direct API, possible through events.
            </td>
            <td>
                Yes
            </td>
        </tr>
        <tr>
            <td>
                Nested Grid
            </td>
            <td>
                Possible through events
            </td>
            <td>
                Yes
            </td>
        </tr>
        <tr>
            <td>
                Layout Events
            </td>
            <td>
                BeginCellLayout, BeginPageLayout, BeginRowLayout, EndCellLayout, EndPageLayout, EndRowLayout
            </td>
            <td>
                BeginPageLayout, EndPageLayout
            </td>
        </tr>
    </tbody>
</table>
