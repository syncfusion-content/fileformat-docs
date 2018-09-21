---
title: Create, edit and format table in PowerPoint presentation slide
description: Code examples to create, edit and format PowerPoint tables in .NET, C#, web, ASP.NET, UWP, MVC, Xamarin and .NET Core
platform: file-format,.NET, C#, web, ASP.NET, UWP, MVC, Xamarin and .NET Core
control: Syncfusion PowerPoint presentation
documentation: 
keywords: PowerPoint, slide, table, format-table, rows, columns, pptx
---
## Create a table by adding rows

Essential Presentation supports creating and editing tables in PowerPoint slides by adding rows. Refer to the following code example.

{% tabs %}
{% highlight c# %}

//Create a PowerPoint presentation

IPresentation pptxDoc = Presentation.Create();

//Add slide to the presentation

ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Add a table to the slide

ITable table = slide.Shapes.AddTable(2, 2, 100, 120, 300, 200);

//Initialize index values to add text to table cells

int rowIndex = 0, colIndex;

//Iterate row-wise cells and add text to it

foreach (IRow rows in table.Rows)
{
	colIndex = 0;
	
	foreach (ICell cell in rows.Cells)	
	{
	
		cell.TextBody.AddParagraph("(" + rowIndex.ToString() + " , " + colIndex.ToString() + ")");
		
		colIndex++;
		
	}
	
	rowIndex++;

}

//Save the presentation

pptxDoc.Save("Sample.pptx");

//Close the presentation

pptxDoc.Close();

{% endhighlight %}
{% highlight vb.net %}

'Create a PowerPoint presentation

Dim pptxDoc As IPresentation = Presentation.Create()

'Add slide to the presentation

Dim slide As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank)

'Add a table to the slide

Dim table As ITable = slide.Shapes.AddTable(2, 2, 100, 120, 300, 200)

'Initialize index values to add text to table cells

Dim rowIndex As Integer = 0, colIndex As Integer

'Iterate row-wise cells and add text to it

For Each rows As IRow In table.Rows
	colIndex = 0
	
	For Each cell As ICell In rows.Cells
	
		cell.TextBody.AddParagraph("(" + rowIndex.ToString() + " , " + colIndex.ToString() + ")")
		
		colIndex += 1
		
	Next
	
	rowIndex += 1
	
Next

'Save the presentation

pptxDoc.Save("Sample.pptx")

'Close the presentation

pptxDoc.Close()

{% endhighlight %}
{% endtabs %}

## Create a table by adding columns

The following code example demonstrates how to create a simple table in a PowerPoint slide by adding columns.

{% tabs %}
{% highlight c# %}

//Create a PowerPoint presentation

IPresentation pptxDoc = Presentation.Create();

//Add slide to the presentation

ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Add a table to the slide

ITable table = slide.Shapes.AddTable(2, 2, 100, 120, 300, 200);

//Initialize index values to add text to table cells

int row = 0, col;

//Iterate row-wise cells and add text to it

foreach (IColumn columns in table.Columns)
{
	col = 0;
	
	foreach (ICell cell in columns.Cells)
	{
	
		cell.TextBody.AddParagraph("(" + row.ToString() + " , " + col.ToString() + ")");
		
		col++;
		
	}
	
	row++;
}

//Save the presentation

pptxDoc.Save("Sample.pptx");

//Close the presentation

pptxDoc.Close();
{% endhighlight %}
{% highlight vb.net %}

'Create a PowerPoint presentation

Dim pptxDoc As IPresentation = Presentation.Create()

'Add slide to the presentation

Dim slide As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank)

'Add a table to the slide

Dim table As ITable = slide.Shapes.AddTable(2, 2, 100, 120, 300, 200)

'Initialize index values to add text to the table cells

Dim row As Integer = 0, col As Integer

'Iterate row-wise cells and add text to it

For Each columns As IColumn In table.Columns
	col = 0
	
	For Each cell As ICell In columns.Cells
	
		cell.TextBody.AddParagraph("(" + row.ToString() + " , " + col.ToString() + ")")
		
		col += 1
		
	Next
	
	row += 1
	
Next
'Save the presentation

pptxDoc.Save("Sample.pptx")

'Close the presentation

pptxDoc.Close()

{% endhighlight %}
{% endtabs %}

## Append a new row at the end of table

You can append new rows at the end of an existing PowerPoint table. Refer to the following code sample.

{% tabs %}
{% highlight c# %}

//Open an existing PowerPoint presentation

IPresentation pptxDoc = Presentation.Open("Table.pptx");

//Get a table in the slide

ITable table = pptxDoc.Slides[0].Shapes[0] as ITable;

//Add or append a new row at the end of table

IRow row = table.Rows.Add();

//Iterate row-wise cells and add text to it

foreach (ICell cell in row.Cells)
{
    cell.TextBody.AddParagraph(table.Rows.IndexOf(row).ToString());
	
}

//Save the presentation
pptxDoc.Save("Sample.pptx");

//Close the presentation

pptxDoc.Close();
{% endhighlight %}
{% highlight vb.net %}

'Open an existing PowerPoint presentation

Dim pptxDoc As IPresentation = Presentation.Open("Table.pptx")

'Get a table in the slide

Dim table As ITable = TryCast(pptxDoc.Slides(0).Shapes(0), ITable)

'Add a new row at the end of table

Dim row As IRow = table.Rows.Add()

'Iterate row-wise cells and add text to it

For Each cell As ICell In row.Cells

	cell.TextBody.AddParagraph(table.Rows.IndexOf(row).ToString())
	
Next

'Save the presentation

pptxDoc.Save("Sample.pptx")

'Close the presentation

pptxDoc.Close()
{% endhighlight %}
{% endtabs %}

## Copy an existing row to the end of table

You can copy an existing row to the end of a table. Refer to the following code example.

{% tabs %}
{% highlight c# %}

//Open an existing PowerPoint presentation

IPresentation pptxDoc = Presentation.Open("Table.pptx");

//Get a table in the slide

ITable table = pptxDoc.Slides[0].Shapes[0] as ITable;

//Copy the first row to the end of table

table.Rows.Add(table.Rows[0].Clone());

//Save the presentation

pptxDoc.Save("Sample.pptx");

//Close the presentation

pptxDoc.Close();

{% endhighlight %}
{% highlight vb.net %}

'Open an existing PowerPoint presentation

Dim pptxDoc As IPresentation = Presentation.Open("Table.pptx")

'Get the table in the slide

Dim table As ITable = TryCast(pptxDoc.Slides(0).Shapes(0), ITable)

'Copy the first row to the end of table

table.Rows.Add(table.Rows(0).Clone())

'Save the presentation

pptxDoc.Save("Sample.pptx")

'Close the presentation

pptxDoc.Close()

{% endhighlight %}
{% endtabs %}

## Insert a row in table

You can insert a row at the specified index position of a table. Refer to the following code example.

{% tabs %}
{% highlight c# %}

//Open an existing PowerPoint presentation

IPresentation pptxDoc = Presentation.Open("Table.pptx");

//Get a table in the slide

ITable table = pptxDoc.Slides[0].Shapes[0] as ITable;

//Insert a row at the specified index. Here, the existing first row at index 0 is copied and inserted at row index 1

table.Rows.Insert(1, table.Rows[0].Clone());

//Save the presentation

pptxDoc.Save("Sample.pptx");

//Close the presentation

pptxDoc.Close();
{% endhighlight %}
{% highlight vb.net %}
'Open an existing PowerPoint presentation

Dim pptxDoc As IPresentation = Presentation.Open("Table.pptx")

'Get a table in the slide

Dim table As ITable = TryCast(pptxDoc.Slides(0).Shapes(0), ITable)

'Insert a row at the specified index. Here, the existing first row at index 0 is copied and inserted at row index 1.

table.Rows.Insert(1, table.Rows(0).Clone())

'Save the presentation

pptxDoc.Save("Sample.pptx")

'Close the presentation

pptxDoc.Close()

{% endhighlight %}
{% endtabs %}

## Append a new column at the end table

You can append new column to a table. Refer to the following code example.

{% tabs %}
{% highlight c# %}

//Open an existing PowerPoint presentation

IPresentation pptxDoc = Presentation.Open("Table.pptx");

//Get a table in the slide

ITable table = pptxDoc.Slides[0].Shapes[0] as ITable;

//Add or append a new column at the end of table

IColumn column = table.Columns.Add();

//Iterate row-wise cells and add text to it

foreach (ICell cell in column.Cells)
{
    cell.TextBody.AddParagraph(table.Columns.IndexOf(column).ToString());
}
//Save the presentation

pptxDoc.Save("Sample.pptx");

//Close the presentation

pptxDoc.Close();

{% endhighlight %}
{% highlight vb.net %}

'Open an existing PowerPoint presentation

Dim pptxDoc As IPresentation = Presentation.Open("Table.pptx")

'Get a table in the slide

Dim table As ITable = TryCast(pptxDoc.Slides(0).Shapes(0), ITable)

'Add or append a new column at the end of table

Dim column As IColumn = table.Columns.Add()

'Iterate row-wise cells and add text to it

For Each cell As ICell In column.Cells

	cell.TextBody.AddParagraph(table.Columns.IndexOf(column).ToString())

Next

'Save the presentation

pptxDoc.Save("Sample.pptx")

'Close the presentation

pptxDoc.Close()

{% endhighlight %}
{% endtabs %}

## Copy an existing column to the end of table

You can copy an existing column and append it to the end of table. Refer to the following code example.

{% tabs %}
{% highlight c# %}

//Open an existing PowerPoint presentation

IPresentation pptxDoc = Presentation.Open("Table.pptx");

//Get a table from the slide

ITable table = pptxDoc.Slides[0].Shapes[0] as ITable;

//Copy the column and append it to the end of table

table.Columns.Add(table.Columns[0].Clone());

//Save the presentation

pptxDoc.Save("Sample.pptx");

//Close the presentation

pptxDoc.Close();

{% endhighlight %}
{% highlight vb.net %}

'Open an existing PowerPoint presentation

Dim pptxDoc As IPresentation = Presentation.Open("Table.pptx")

'Get a table from the slide

Dim table As ITable = TryCast(pptxDoc.Slides(0).Shapes(0), ITable)

'Copy the column and append it to the end of table

table.Columns.Add(table.Columns(0).Clone())

'Save the presentation

pptxDoc.Save("Sample.pptx")

'Close the presentation

pptxDoc.Close()

{% endhighlight %}
{% endtabs %}

## Insert a column to a table

You can insert a column at the specified index position of a table. Refer to the following code example.

{% tabs %}
{% highlight c# %}

//Open an existing PowerPoint presentation

IPresentation pptxDoc = Presentation.Open("Table.pptx");

//Get the table from the slide

ITable table = pptxDoc.Slides[0].Shapes[0] as ITable;

//Insert a column at the specified index. Here, the existing first column at index 0 is copied and inserted at column index 1

table.Columns.Insert(1, table.Columns[0].Clone());

//Save the presentation

pptxDoc.Save("Sample.pptx");

//Close the presentation

pptxDoc.Close();

{% endhighlight %}
{% highlight vb.net %}

'Open an existing PowerPoint presentation

Dim pptxDoc As IPresentation = Presentation.Open("Table.pptx")

'Get the table from the slide

Dim table As ITable = TryCast(pptxDoc.Slides(0).Shapes(0), ITable)

'Insert a column at the specified index. Here, the existing first column at index 0 is copied and inserted at column index 1.

table.Columns.Insert(1, table.Columns(0).Clone())

'Save the presentation

pptxDoc.Save("Sample.pptx")

'Close the presentation

pptxDoc.Close()

{% endhighlight %}

## Applying table formatting

You can format a table to change its appearance by customizing the table border, cell background, cell margins etc. The following code example demonstrates how to apply the custom table formatting.

{% tabs %}

{% highlight c# %}

//Creates instance of PowerPoint Presentation

IPresentation presentation = Presentation.Create();

//Adds slide to the Presentation

ISlide slide = presentation.Slides.Add(SlideLayoutType.Blank);

//Adds table to the slide

ITable table = slide.Shapes.AddTable(2, 2, 100, 120, 300, 200);

//Retrieves each cell and fills text content to the cell.

ICell cell = table[0, 0];

//Sets the column width for a cell; this sets the width for entire column

cell.ColumnWidth = 400;

//Sets the margin for the cell.

cell.TextBody.MarginBottom = 0;

cell.TextBody.MarginLeft = 58;

cell.TextBody.MarginRight = 29;

cell.TextBody.MarginTop = 65;

//Sets the back color for the cell.

cell.Fill.SolidFill.Color.SystemColor = Color.Orange;

cell.TextBody.AddParagraph("First Row and First Column");

cell = table[0, 1];

//Sets the margin for the cell.

cell.TextBody.MarginLeft = 58;

cell.TextBody.MarginRight = 29;

cell.TextBody.MarginTop = 65;

//Sets the back color for the cell.

cell.Fill.SolidFill.Color.SystemColor = Color.BlueViolet;

cell.TextBody.AddParagraph("First Row and Second Column");

cell = table[1, 0];

//Sets the margin for the cell.

cell.TextBody.MarginLeft = 58;

cell.TextBody.MarginRight = 29;

cell.TextBody.MarginTop = 65;

//Sets the back color for the cell.

cell.Fill.SolidFill.Color.SystemColor = Color.SandyBrown;

cell.TextBody.AddParagraph("Second Row and First Column");

cell = table[1, 1];

//Sets the margin for the cell.

cell.TextBody.MarginLeft = 58;

cell.TextBody.MarginRight = 29;

cell.TextBody.MarginTop = 65;

//Sets the back color for the cell.

cell.Fill.SolidFill.Color.SystemColor = Color.Silver;

cell.TextBody.AddParagraph("Second Row and Second Column");

//Saves the Presentation

presentation.Save("Table.pptx");

//Closes the Presentation

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates instance of PowerPoint Presentation

Dim presentationDocument As IPresentation = Presentation.Create()

'Adds slide to the Presentation

Dim slide As ISlide = presentationDocument.Slides.Add(SlideLayoutType.Blank)

'Adds table to the slide

Dim table As ITable = slide.Shapes.AddTable(2, 2, 100, 120, 300, 200)

'Retrieves each cell and fills text content to the cell.

Dim cell As ICell = table(0, 0)

'Sets the column width for a cell; this sets the width for entire column

cell.ColumnWidth = 400

'Sets the margin for the cell.

cell.TextBody.MarginBottom = 0

cell.TextBody.MarginLeft = 58

cell.TextBody.MarginRight = 29

cell.TextBody.MarginTop = 65

'Sets the back color for the cell.

cell.Fill.SolidFill.Color.SystemColor = Color.Orange

cell.TextBody.AddParagraph("First Row and First Column")

cell = table(0, 1)

'Sets the margin for the cell.

cell.TextBody.MarginLeft = 58

cell.TextBody.MarginRight = 29

cell.TextBody.MarginTop = 65

'Sets the back color for the cell.

cell.Fill.SolidFill.Color.SystemColor = Color.BlueViolet

cell.TextBody.AddParagraph("First Row and Second Column")

cell = table(1, 0)

'Sets the margin for the cell.

cell.TextBody.MarginLeft = 58

cell.TextBody.MarginRight = 29

cell.TextBody.MarginTop = 65

'Sets the back color for the cell.

cell.Fill.SolidFill.Color.SystemColor = Color.SandyBrown

cell.TextBody.AddParagraph("Second Row and First Column")

cell = table(1, 1)

'Sets the margin for the cell.

cell.TextBody.MarginLeft = 58

cell.TextBody.MarginRight = 29

cell.TextBody.MarginTop = 65

'Sets the back color for the cell.

cell.Fill.SolidFill.Color.SystemColor = Color.Silver

cell.TextBody.AddParagraph("Second Row and Second Column")

'Saves the Presentation

presentationDocument.Save("Table.pptx")

'Closes the Presentation

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

## Applying table styles

You can format a table by applying pre-defined table styles. The following code example demonstrates how to apply predefined styles to a table.

{% tabs %}

{% highlight c# %}

//Creates instance of PowerPoint Presentation

IPresentation presentation = Presentation.Create();

//Adds slide to the Presentation

ISlide slide = presentation.Slides.Add(SlideLayoutType.Blank);

//Adds table to the slide

ITable table = slide.Shapes.AddTable(3, 3, 100, 120, 300, 200);

table.BuiltInStyle = BuiltInTableStyle.ThemedStyle2Accent4;

table.HasBandedRows = false;

table.HasHeaderRow = false;

table.HasBandedColumns = true;

table.HasFirstColumn = true;

table.HasLastColumn = true;

table.HasTotalRow = true;

//Retrieves each cell and fills text content to the cell.

ICell cell = table[0, 0];

cell.TextBody.AddParagraph("First Row and First Column");

cell = table[0, 1];

cell.TextBody.AddParagraph("First Row and Second Column");

cell = table[0, 2];

cell.TextBody.AddParagraph("First Row and Third Column");

cell = table[1, 0];

cell.TextBody.AddParagraph("Second Row and First Column");

cell = table[1, 1];

cell.TextBody.AddParagraph("Second Row and Second Column");

cell = table[1, 2];

cell.TextBody.AddParagraph("Second Row and Third Column");

cell = table[2, 0];

cell.TextBody.AddParagraph("Third Row and First Column");

cell = table[2, 1];

cell.TextBody.AddParagraph("Third Row and Second Column");

cell = table[2, 2];

cell.TextBody.AddParagraph("Third Row and Third Column");

//Adds description to table shape

table.Description = "Table arrangement";

//Saves the Presentation

presentation.Save("Table.pptx");

//Closes the Presentation

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates instance of PowerPoint Presentation

Dim  presentationDocument As IPresentation = Presentation.Create()

'Adds slide to the Presentation

Dim slide As ISlide =  presentationDocument .Slides.Add(SlideLayoutType.Blank)

'Adds table to the slide

Dim table As ITable = slide.Shapes.AddTable(3, 3, 100, 120, 300, 200)

table.BuiltInStyle = BuiltInTableStyle.ThemedStyle2Accent4

table.HasBandedRows = False

table.HasHeaderRow = False

table.HasBandedColumns = True

table.HasFirstColumn = True

table.HasLastColumn = True

table.HasTotalRow = True

'Retrieves each cell and fills text content to the cell.

Dim cell As ICell = table(0, 0)

cell.TextBody.AddParagraph("First Row and First Column")

cell = table(0, 1)

cell.TextBody.AddParagraph("First Row and Second Column")

cell = table(0, 2)

cell.TextBody.AddParagraph("First Row and Third Column")

cell = table(1, 0)

cell.TextBody.AddParagraph("Second Row and First Column")

cell = table(1, 1)

cell.TextBody.AddParagraph("Second Row and Second Column")

cell = table(1, 2)

cell.TextBody.AddParagraph("Second Row and Third Column")

cell = table(2, 0)

cell.TextBody.AddParagraph("Third Row and First Column")

cell = table(2, 1)

cell.TextBody.AddParagraph("Third Row and Second Column")

cell = table(2, 2)

cell.TextBody.AddParagraph("Third Row and Third Column")

'Adds description to table shape

table.Description = "Table arrangement"

'Saves the Presentation

presentationDocument.Save("Table.pptx")

'Closes the Presentation

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

## Modifying the table

The following code example demonstrates how to modify the table in existing PowerPoint Presentation

{% tabs %}

{% highlight c# %}

//Creates instance of PowerPoint Presentation

IPresentation presentation = Presentation.Open("Table.pptx");

//Gets slide from the Presentation

ISlide slide = presentation.Slides[0];

//Gets table from slide

ITable table = slide.Shapes[0] as ITable;

//Modifies the table width

table.Width = 450;

//Changes the built in style of the table

table.BuiltInStyle = BuiltInTableStyle.DarkStyle1Accent2;

//Sets text content to the cell

table.Rows[0].Cells[0].TextBody.AddParagraph("Row1 Cell1");           

//Saves the Presentation

presentation.Save("TableModified.pptx");

//Closes the Presentation

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates instance of PowerPoint Presentation

Dim presentationDocument As IPresentation = Presentation.Open("Table.pptx")

'Gets slide from the Presentation

Dim slide As ISlide = presentationDocument.Slides(0)

'Gets table from slide

Dim table As ITable = TryCast(slide.Shapes(0), ITable)

'Modifies the table width

table.Width = 450

'Changes the built in style of the table

table.BuiltInStyle = BuiltInTableStyle.DarkStyle1Accent2

'Sets text content to the cell

table.Rows(0).Cells(0).TextBody.AddParagraph("Row1 Cell1")

'Saves the Presentation

presentationDocument.Save("TableModified.pptx")

'Closes the Presentation

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

## Merging the cells

The following code example shows how to merge cells in a table.

{% tabs %}

{% highlight c# %}

//Creates instance of PowerPoint Presentation

IPresentation presentation = Presentation.Create();

//Adds slide to the Presentation

ISlide slide = presentation.Slides.Add(SlideLayoutType.Blank);

//Adds table to the slide

ITable table = slide.Shapes.AddTable(2, 2, 100, 120, 300, 200);

//Retrieves first cell.

ICell cell = table[0, 0];

//Sets the column span value to merge the cell.

cell.ColumnSpan = 2;

//Retrieves each cell and fills text content to the cell.

cell.TextBody.AddParagraph("First Row and First Column");

cell = table[0, 1];

cell.TextBody.AddParagraph("First Row and Second Column");

cell = table[1, 0];

cell.TextBody.AddParagraph("Second Row and First Column");

cell = table[1, 1];

cell.TextBody.AddParagraph("Second Row and Second Column");

//Gives simple description to table shape

table.Description = "Table arrangement";

//Saves the Presentation

presentation.Save("Table.pptx");

//Closes the Presentation

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates instance of PowerPoint Presentation

Dim presentationDocument As IPresentation = Presentation.Create()

'Adds slide to the Presentation

Dim slide As ISlide = presentationDocument.Slides.Add(SlideLayoutType.Blank)

'Adds table to the slide

Dim table As ITable = slide.Shapes.AddTable(2, 2, 100, 120, 300, 200)

'Retrieves first cell.

Dim cell As ICell = table(0, 0)

'Sets the column span value to merge the cell.

cell.ColumnSpan = 2

'Retrieves each cell and fills text content to the cell.

cell.TextBody.AddParagraph("First Row and First Column")

cell = table(0, 1)

cell.TextBody.AddParagraph("First Row and Second Column")

cell = table(1, 0)

cell.TextBody.AddParagraph("Second Row and First Column")

cell = table(1, 1)

cell.TextBody.AddParagraph("Second Row and Second Column")

'Gives simple description to table shape

table.Description = "Table arrangement"

'Saves the Presentation

presentationDocument.Save("Table.pptx")

'Closes the Presentation

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

## Removing the table

You can remove a table from a slide by its instance or by its index position in the shape collection. The following code example demonstrates removing a table in a slide.

{% tabs %}

{% highlight c# %}

//Creates instance of PowerPoint Presentation

IPresentation presentation = Presentation.Open("Table.pptx");

//Gets slide from the Presentation

ISlide slide = presentation.Slides[0];

//Gets the table from slide

ITable table = slide.Shapes[0] as ITable;

//Removes table from shape collection

slide.Shapes.Remove(table);

//Saves the Presentation

presentation.Save("TableRemoved.pptx");

//Closes the Presentation

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates instance of PowerPoint Presentation

Dim presentationDocument As IPresentation = Presentation.Open("Table.pptx")

'Gets slide from the Presentation

Dim slide As ISlide = presentationDocument.Slides(0)

'Gets the table from slide

Dim table As ITable = TryCast(slide.Shapes(0), ITable)

'Removes table from shape collection

slide.Shapes.Remove(table)

'Saves the Presentation

presentationDocument.Save("TableRemoved.pptx")

'Closes the Presentation

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}