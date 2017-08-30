---
title: Working with Tables
description: This section explains how to create tables in the PDF document
platform: file-formats
control: PDF
documentation: UG
---
# Working with Tables

Essential PDF provides support for two types of table models, both having a different levels of customization, which is explained below. The two types of table models are

1. PdfGrid
2. PdfLightTable.

## Creating a simple table 

### Creating a simple table using PdfLightTable in a new document


Essential PDF allows you to create the table with data sources from DataSet, Data Table, arrays and IEnumerable objects using PdfLightTable class. It allows you to perform simple formatting.

N> In Silverlight, Windows store apps and Xamarin only strongly typed IEnumerable objects are supported. 

The below code snippet illustrates how to create a simple table from a data source using PdfLightTable.

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
{% endtabs %}

You can directly add rows and columns, instead of a data source by setting DataSourceType property to PdfLightTableDataSourceType.TableDirect.

The following code illustrates how to add the data directly into the PdfLightTable.

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

{% endtabs %}

### Creating a simple table using PdfLightTable in an existing document

You can create table using PdfLightTable in the existing document by using the following code sample

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
{% endtabs %}

### Creating a simple table using PdfGrid in a new document

PdfGrid allows you to create table by entering the data manually or from an external data source. The datasource can be a data set, data table, arrays or a IEnumerable object.

N> In Silverlight, Windows store apps and Xamarin only strongly typed IEnumerable objects are supported. 

The below code snippet illustrates how to create a simple table from a data source using PdfGrid.

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

{% endtabs %}

You can set the data directly without setting any data source using PdfGridRow and PdfGridColumn classes. 

The below code snippet illustrates how to create the simple table directly using PdfGrid.

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

{% endtabs %}

### Creating a simple table using PdfGrid in an existing document

You can create a table using PdfGrid in the existing document by using the following code sample

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

{% endtabs %}

## Support for cell customization 

### Cell customization in PdfLightTable

PdfLightTable allows users to customize cell font, background, border, etc. using PdfCellStyle class.

The below code snippet illustrates how to customize the cell properties in PdfLightTable.

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

{% endtabs %}

You can set different styles for particular cell using BeginCellLayout event and EndCellLayout events in PdfLightTable class.

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

{% endtabs %}

### Cell customization in PdfGrid

PdfGridCell provides various direct options to customize cells like column span, row span, text color, background color, and etc.

The following code example illustrates you how to customize the cell in PdfGrid.

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

{% endtabs %}

## Support for rows and columns customization

### Row customization in PdfLightTable

PdfLightTable doesn’t provide direct support for row customizations. However, this can be done through the event handlers.The following code snippet illustrates how to customize the row in PdfLightTable using BeginRowLayout and EndRowLayout event handlers.

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

//Apply coloumn span

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

'Apply coloumn span

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

{% endtabs %}

### Column customization in PdfLightTable

The following code snippet illustrates how to customize the column in PdfLightTable using the PdfStringFormat class.

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

{% endtabs %}

### Row customization in PdfGrid 

You can customize row height and styles using Rows property in PdfGrid class.

The following code snippet illustrates how to customize the row in PdfGrid.

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

{% endtabs %}

### Columns customization in PdfGrid

You can customize column width and text formats using Column property in PdfGrid class.

The following code snippet illustrates how to customize the column in PdfGrid.

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

dataTable.Rows.Add(new object[] { "E02", "thomas" });

dataTable.Rows.Add(new object[] { "E03", "peter" });

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

dataTable.Rows.Add(New Object() {"E02", "thomas"})

dataTable.Rows.Add(New Object() {"E03", "peter"})

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

{% endtabs %}

## Built-in table styles

In-built table styles can be applied to both PdfGrid and PdfLightTable models and the appearance is made similar to Microsoft Word’s built-in table styles. You can also apply in-built table styles with the following additional table style options.


* Banded columns
* Banded rows
* First column
* Last column
* Header row
* Last row

The below code example illustrates how to apply built-in table styles to the PdfGrid

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

{% endtabs %}

The below code example illustrates how to apply built-in table styles to the PdfLightTable.

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

{% endtabs %}

The below code example illustrates how to apply built-in table styles with table options to the PdfGrid.

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

{% endtabs %}

## Pagination

### Pagination in PdfLightTable

Essential PDF provides support to paginate the PdfLightTable using PdfLightTableLayoutFormat class.

The below sample illustrates how to allow the PdfLightTable to flow across pages.

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

{% endtabs %}

### Pagination in PdfGrid

Essential PDF supports to paginate the grid table using PdfGridLayoutFormat class.

The below sample illustrates how to allow the PdfGrid to flow across pages.

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

{% endtabs %}

## Difference between PdfLightTable and PdfGrid

Both the PdfGrid and PdfLightTable models are supported across all the platforms and the below table explains the level of customizations both the models provide.

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