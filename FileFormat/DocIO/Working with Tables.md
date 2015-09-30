---
layout: Post
title: Working With Tables
description: This section illustrates how to work with Tables
platform: FileFormat
control: DocIO
documentation: UG
---
# Working with Tables

A table in Word document is used to arrange document content in rows and columns. **WTable** instance represents a table in Word document. A table must contains at least one row.

1. A row is a collection of cells and it is represented by an instance of **WTableRow**. Each row must contain at least one cell.
2. A cell can contain one or more paragraphs & tables. An instance of **WTableCell** represents a table cell. Each table cell must contain at least one paragraph.

The following image illustrates how a table in Word document is organized in **Essential** **DocIO’** s DOM:

The following code snippet illustrates how to create a simple table with predefined number of rows and cells.

{% highlight c# %}
[C#]

//Create an instance of WordDocument class 

WordDocument document = new WordDocument();

//Add a section into Word document

IWSection section = document.AddSection();

//Add a new paragraph into Word document and append text into paragraph

IWTextRange textRange = section.AddParagraph().AppendText("Price Details");

textRange.CharacterFormat.FontName = "Arial";

textRange.CharacterFormat.FontSize = 12;

textRange.CharacterFormat.Bold = true;

section.AddParagraph();

//Add a new table into Word document

IWTable table = section.AddTable();

//Specify the total number of rows & columns

table.ResetCells(3, 2);

//Access the instance of the cell (first row, first cell) and add the content into cell

textRange = table[0, 0].AddParagraph().AppendText("Item");

textRange.CharacterFormat.FontName = "Arial";

textRange.CharacterFormat.FontSize = 12;

textRange.CharacterFormat.Bold = true;

//Access the instance of the cell (first row, second cell) and add the content into cell

textRange = table[0, 1].AddParagraph().AppendText("Price($)");

textRange.CharacterFormat.FontName = "Arial";

textRange.CharacterFormat.FontSize = 12;

textRange.CharacterFormat.Bold = true;

//Access the instance of the cell (second row, first cell) and add the content into cell

textRange = table[1, 0].AddParagraph().AppendText("Apple");

textRange.CharacterFormat.FontName = "Arial";

textRange.CharacterFormat.FontSize = 10;

//Access the instance of the cell (second row, second cell) and add the content into cell

textRange = table[1, 1].AddParagraph().AppendText("50");

textRange.CharacterFormat.FontName = "Arial";

textRange.CharacterFormat.FontSize = 10;

//Access the instance of the cell (third row, first cell) and add the content into cell

textRange = table[2, 0].AddParagraph().AppendText("Orange");

textRange.CharacterFormat.FontName = "Arial";

textRange.CharacterFormat.FontSize = 10;

//Access the instance of the cell (third row, second cell) and add the content into cell

textRange = table[2, 1].AddParagraph().AppendText("30");

textRange.CharacterFormat.FontName = "Arial";

textRange.CharacterFormat.FontSize = 10;

//Save the document in the given name and format

document.Save("Table.docx", FormatType.Docx);

//Release the resources occupied by WordDocument instance

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB]

'Create an instance of WordDocument class 

Dim document As New WordDocument()

'Add a section into Word document

Dim section As IWSection = document.AddSection()

'Add a new paragraph into Word document and append text into paragraph

Dim textRange As IWTextRange = section.AddParagraph().AppendText("Price Details")

textRange.CharacterFormat.FontName = "Arial"

textRange.CharacterFormat.FontSize = 12

textRange.CharacterFormat.Bold = True

section.AddParagraph()

'Add a new table into Word document

Dim table As IWTable = section.AddTable()

'Specify the total number of rows & columns

table.ResetCells(3, 2)

'Access the instance of the cell (first row, first cell) and add the content into cell

textRange = table(0, 0).AddParagraph().AppendText("Item")

textRange.CharacterFormat.FontName = "Arial"

textRange.CharacterFormat.FontSize = 12

textRange.CharacterFormat.Bold = True

'Access the instance of the cell (first row, second cell) and add the content into cell

textRange = table(0, 1).AddParagraph().AppendText("Price($)")

textRange.CharacterFormat.FontName = "Arial"

textRange.CharacterFormat.FontSize = 12

textRange.CharacterFormat.Bold = True

'Access the instance of the cell (second row, first cell) and add the content into cell

textRange = table(1, 0).AddParagraph().AppendText("Apple")

textRange.CharacterFormat.FontName = "Arial"

textRange.CharacterFormat.FontSize = 10

'Access the instance of the cell (second row, second cell) and add the content into cell

textRange = table(1, 1).AddParagraph().AppendText("50")

textRange.CharacterFormat.FontName = "Arial"

textRange.CharacterFormat.FontSize = 10

'Access the instance of the cell (third row, first cell) and add the content into cell

textRange = table(2, 0).AddParagraph().AppendText("Orange")

textRange.CharacterFormat.FontName = "Arial"

textRange.CharacterFormat.FontSize = 10

'Access the instance of the cell (third row, second cell) and add the content into cell

textRange = table(2, 1).AddParagraph().AppendText("30")

textRange.CharacterFormat.FontName = "Arial"

textRange.CharacterFormat.FontSize = 10

'Save the document in the given name and format

document.Save("Table.docx", FormatType.Docx)

'Release the resources occupied by WordDocument instance

document.Close()



{% endhighlight %}

The following code snippet illustrates how to create a simple table by dynamically adding rows.

{% highlight c# %}
[C#]

WordDocument document = new WordDocument();

IWSection section = document.AddSection();

section.AddParagraph().AppendText("Price Details");

section.AddParagraph();

//Add a new table into Word document

IWTable table = section.AddTable();

//Add the first row into table

WTableRow row = table.AddRow();

//Add the first cell into first row 

WTableCell cell = row.AddCell();

//Specify the cell width

cell.Width = 200;

cell.AddParagraph().AppendText("Item");

//Add the second cell into first row 

cell = row.AddCell();

//Specify the cell width

cell.Width = 200;

cell.AddParagraph().AppendText("Price($)");

//Add the second row into table

row = table.AddRow(true, false);

//Add the first cell into second row

cell = row.AddCell();

//Specify the cell width

cell.Width = 200;

cell.AddParagraph().AppendText("Apple");

//Add the second cell into second row

cell = row.AddCell();

//Specify the cell width

cell.Width = 200;

cell.AddParagraph().AppendText("50");

//Add the third row into table

row = table.AddRow(true, false);

//Add the first cell into third row 

cell = row.AddCell();

//Specify the cell width

cell.Width = 200;

cell.AddParagraph().AppendText("Orange");

//Add the second cell into third row 

cell = row.AddCell();

//Specify the cell width

cell.Width = 200;

cell.AddParagraph().AppendText("30");

//Add the fourth row into table

row = table.AddRow(true, false);

//Add the first cell into fourth row

cell = row.AddCell();

//Specify the cell width

cell.Width = 200;

cell.AddParagraph().AppendText("Banana");

//Add the second cell into fourth row 

cell = row.AddCell();

//Specify the cell width

cell.Width = 200;

cell.AddParagraph().AppendText("20");

//Add the fifth row to table

row = table.AddRow(true, false);

//Add the first cell into fifth row 

cell = row.AddCell();

//Specify the cell width

cell.Width = 200;

cell.AddParagraph().AppendText("Grapes");

//Add the second cell into fifth row 

cell = row.AddCell();

//Specify the cell width

cell.Width = 200;

cell.AddParagraph().AppendText("70");

document.Save("Table.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB]

Dim document As New WordDocument()

Dim section As IWSection = document.AddSection()

section.AddParagraph().AppendText("Price Details")

section.AddParagraph()

'Add a new table into Word document

Dim table As IWTable = section.AddTable()

'Add the first row into table

Dim row As WTableRow = table.AddRow()

'Add the first cell into first row 

Dim cell As WTableCell = row.AddCell()

'Specify the cell width

cell.Width = 200

cell.AddParagraph().AppendText("Item")

'Add the second cell into first row 

cell = row.AddCell()

'Specify the cell width

cell.Width = 200

cell.AddParagraph().AppendText("Price($)")

'Add the second row into table

row = table.AddRow(True, False)

'Add the first cell into second row

cell = row.AddCell()

'Specify the cell width

cell.Width = 200

cell.AddParagraph().AppendText("Apple")

'Add the second cell into second row

cell = row.AddCell()

'Specify the cell width

cell.Width = 200

cell.AddParagraph().AppendText("50")

'Add the third row into table

row = table.AddRow(True, False)

'Add the first cell into third row 

cell = row.AddCell()

'Specify the cell width

cell.Width = 200

cell.AddParagraph().AppendText("Orange")

'Add the second cell into third row 

cell = row.AddCell()

'Specify the cell width

cell.Width = 200

cell.AddParagraph().AppendText("30")

'Add the fourth row into table

row = table.AddRow(True, False)

'Add the first cell into fourth row

cell = row.AddCell()

'Specify the cell width

cell.Width = 200

cell.AddParagraph().AppendText("Banana")

'Add the second cell into fourth row 

cell = row.AddCell()

'Specify the cell width

cell.Width = 200

cell.AddParagraph().AppendText("20")

'Add the fifth row to table

row = table.AddRow(True, False)

'Add the first cell into fifth row 

cell = row.AddCell()

'Specify the cell width

cell.Width = 200

cell.AddParagraph().AppendText("Grapes")

'Add the second cell into fifth row 

cell = row.AddCell()

'Specify the cell width

cell.Width = 200

cell.AddParagraph().AppendText("70")

document.Save("Table.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

## Nested Table 

You can create a nested table by adding a new table into a cell. The following code snippet illustrates how to add a table into a cell.

{% highlight c# %}
[C#]

WordDocument document = new WordDocument();

IWSection section = document.AddSection();

section.AddParagraph().AppendText("Price Details");

IWTable table = section.AddTable();

table.ResetCells(3, 2);

table[0, 0].AddParagraph().AppendText("Item");

table[0, 1].AddParagraph().AppendText("Price($)");

table[1, 0].AddParagraph().AppendText("Items with same price");

//Add a nested table into the cell (second row, first cell).

IWTable nestTable = table[1, 0].AddTable();

//Create the specified number of rows & columns to nested table

nestTable.ResetCells(3, 1);

//Access the instance of the nested table cell (first row, first cell)

WTableCell nestedCell = nestTable.Rows[0].Cells[0];

//Specify the width of the nested cell

nestedCell.Width = 200;

//Add the content into nested cell

nestedCell.AddParagraph().AppendText("Apple");

//Access the instance of the nested table cell (second row, first cell)

nestedCell = nestTable.Rows[1].Cells[0];

//Specify the width of the nested cell

nestedCell.Width = 200;

//Add the content into nested cell

nestedCell.AddParagraph().AppendText("Orange");

//Access the instance of the nested table cell (third row, first cell)

nestedCell = nestTable.Rows[2].Cells[0];

//Specify the width of the nested cell

nestedCell.Width = 200;

//Add the content into nested cell

nestedCell.AddParagraph().AppendText("Mango");

//Access the instance of the cell (second row, second cell)

nestedCell = table.Rows[1].Cells[1];

table[1, 1].AddParagraph().AppendText("85");

table[2, 0].AddParagraph().AppendText("Pomegranate");

table[2, 1].AddParagraph().AppendText("70");

document.Save("NestedTable.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB]

Dim document As New WordDocument()

Dim section As IWSection = document.AddSection()

section.AddParagraph().AppendText("Price Details")

Dim table As IWTable = section.AddTable()

table.ResetCells(3, 2)

table(0, 0).AddParagraph().AppendText("Item")

table(0, 1).AddParagraph().AppendText("Price($)")

table(1, 0).AddParagraph().AppendText("Items with same price")

'Add a nested table into the cell (second row, first cell).

Dim nestTable As IWTable = table(1, 0).AddTable()

'Create the specified number of rows & columns to nested table

nestTable.ResetCells(3, 1)

'Access the instance of the nested table cell (first row, first cell)

Dim nestedCell As WTableCell = nestTable.Rows(0).Cells(0)

'Specify the width of the nested cell

nestedCell.Width = 200

'Add the content into nested cell

nestedCell.AddParagraph().AppendText("Apple")

'Access the instance of the nested table cell (second row, first cell)

nestedCell = nestTable.Rows(1).Cells(0)

'Specify the width of the nested cell

nestedCell.Width = 200

'Add the content into nested cell

nestedCell.AddParagraph().AppendText("Orange")

'Access the instance of the nested table cell (third row, first cell)

nestedCell = nestTable.Rows(2).Cells(0)

'Specify the width of the nested cell

nestedCell.Width = 200

'Add the content into nested cell

nestedCell.AddParagraph().AppendText("Mango")

'Access the instance of the cell (second row, second cell)

nestedCell = table.Rows(1).Cells(1)

table(1, 1).AddParagraph().AppendText("85")

table(2, 0).AddParagraph().AppendText("Pomegranate")

table(2, 1).AddParagraph().AppendText("70")

document.Save("NestedTable.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

## Apply formatting to Table, Row and Cell

The following code snippet illustrates how to load an existing document and apply table formatting options such as Borders, LeftIndent, Paddings, IsAutoResize, etc.

{% highlight c# %}
[C#]

//Create an instance of WordDocument class (Empty Word Document)

WordDocument document = new WordDocument();

//Open an existing Word document into DocIO instance

document.Open("Table.docx", FormatType.Docx);

//Access the instance of the first section in the Word document

WSection section = document.Sections[0];

//Access the instance of the first table in the section

WTable table = section.Tables[0] as WTable;

//Specify the title for the table

table.Title ="PriceDetails";

//Specify the description of the table

table.Description = "This table shows the price details of various fruits";

//Specify the left indent of the table

table.IndentFromLeft = 50;

//Specify the background color of the table

table.TableFormat.BackColor = Color.FromArgb(192, 192, 192);

//Specify the horizontal alignment of the table

table.TableFormat.HorizontalAlignment = RowAlignment.Left;

//Specify the left, right, top and bottom padding of all the cells in the table

table.TableFormat.Paddings.All = 10;

//Specify the auto resize of table to automatically resize all cell width based on its content

table.TableFormat.IsAutoResized = true;

//Specify the table top, bottom, left and right border line width

table.TableFormat.Borders.LineWidth = 2f;

//Specify the table horizontal border line width

table.TableFormat.Borders.Horizontal.LineWidth = 2f;

//Specify the table vertical border line width

table.TableFormat.Borders.Vertical.LineWidth = 2f;

//Specify the tables top, bottom, left and right border color

table.TableFormat.Borders.Color = Color.Red;

//Specify the table Horizontal border color

table.TableFormat.Borders.Horizontal.Color = Color.Red;

//Specify the table vertical border color

table.TableFormat.Borders.Vertical.Color = Color.Red;

//Specify the table borders border type

table.TableFormat.Borders.BorderType = BorderStyle.Double;

//Access the instance of the first row in the table

WTableRow row = table.Rows[0];

//Specify the row height

row.Height = 20;

//Specify the row height type

row.HeightType = TableRowHeightType.AtLeast;

document.Save("TableFormatting.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB]

'Create an instance of WordDocument class (Empty Word Document)

Dim document As New WordDocument()

'Open an existing Word document into DocIO instance

document.Open("Table.docx", FormatType.Docx)

'Access the instance of the first section in the Word document

Dim section As WSection = document.Sections(0)

'Access the instance of the first table in the section

Dim table As WTable = TryCast(section.Tables(0), WTable)

'Specify the title for the table

table.Title = "PriceDetails"

'Specify the description of the table

table.Description = "This table shows the price details of various fruits"

'Specify the left indent of the table

table.IndentFromLeft = 50

'Specify the background color of the table

table.TableFormat.BackColor = Color.FromArgb(192, 192, 192)

'Specify the horizontal alignment of the table

table.TableFormat.HorizontalAlignment = RowAlignment.Left

'Specify the left, right, top and bottom padding of all the cells in the table

table.TableFormat.Paddings.All = 10

'Specify the auto resize of table to automatically resize all cell width based on its content

table.TableFormat.IsAutoResized = True

'Specify the table top, bottom, left and right border line width

table.TableFormat.Borders.LineWidth = 2.0F

'Specify the table horizontal border line width

table.TableFormat.Borders.Horizontal.LineWidth = 2.0F

'Specify the table vertical border line width

table.TableFormat.Borders.Vertical.LineWidth = 2.0F

'Specify the tables top, bottom, left and right border color

table.TableFormat.Borders.Color = Color.Red

'Specify the table Horizontal border color

table.TableFormat.Borders.Horizontal.Color = Color.Red

'Specify the table vertical border color

table.TableFormat.Borders.Vertical.Color = Color.Red

'Specify the table borders border type

table.TableFormat.Borders.BorderType = BorderStyle.[Double]

'Access the instance of the first row in the table

Dim row As WTableRow = table.Rows(0)

'Specify the row height

row.Height = 20

'Specify the row height type

row.HeightType = TableRowHeightType.AtLeast

document.Save("TableFormatting.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

The following code snippet illustrates how to load an existing document and apply cell formatting options such as VerticalAlignment, TextDirection, Paddings, Borders, etc.

{% highlight c# %}
[C#]

WordDocument document = new WordDocument();

document.Open("Table.docx", FormatType.Docx);

WSection section = document.Sections[0];

WTable table = section.Tables[0] as WTable;

//Access the instance of the first row in the table

WTableRow row = table.Rows[0];

//Specify the row height

row.Height = 20;

//Specify the row height type

row.HeightType = TableRowHeightType.AtLeast;

//Access the instance of the first cell in the row

WTableCell cell = row.Cells[0];

//Apecify the cell back ground color

cell.CellFormat.BackColor = Color.FromArgb(192, 192, 192);

//Specify the same padding as table option as false to preserve current cell padding

cell.CellFormat.SamePaddingsAsTable = false;

//Specify the left, right, top and bottom padding of the cell

cell.CellFormat.Paddings.Left = 5;

cell.CellFormat.Paddings.Right = 5;

cell.CellFormat.Paddings.Top = 5;

cell.CellFormat.Paddings.Bottom = 5;

//Specify the vertical alignment of content of text

cell.CellFormat.VerticalAlignment = VerticalAlignment.Middle;

//Access the instance of the second cell in the row

cell = row.Cells[1];

cell.CellFormat.BackColor = Color.FromArgb(192, 192, 192);

cell.CellFormat.SamePaddingsAsTable = false;

//Specify the left, right, top and bottom padding of the cell

cell.CellFormat.Paddings.All = 5;

cell.CellFormat.VerticalAlignment = VerticalAlignment.Middle;

document.Save("TableCellFormatting.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB]

Dim document As New WordDocument()

document.Open("Table.docx", FormatType.Docx)

Dim section As WSection = document.Sections(0)

Dim table As WTable = TryCast(section.Tables(0), WTable)

'Access the instance of the first row in the table

Dim row As WTableRow = table.Rows(0)

'Specify the row height

row.Height = 20

'Specify the row height type

row.HeightType = TableRowHeightType.AtLeast

'Access the instance of the first cell in the row

Dim cell As WTableCell = row.Cells(0)

'Apecify the cell back ground color

cell.CellFormat.BackColor = Color.FromArgb(192, 192, 192)

'Specify the same padding as table option as false to preserve current cell padding

cell.CellFormat.SamePaddingsAsTable = False

'Specify the left, right, top and bottom padding of the cell

cell.CellFormat.Paddings.Left = 5

cell.CellFormat.Paddings.Right = 5

cell.CellFormat.Paddings.Top = 5

cell.CellFormat.Paddings.Bottom = 5

'Specify the vertical alignment of content of text

cell.CellFormat.VerticalAlignment = VerticalAlignment.Middle

'Access the instance of the second cell in the row

cell = row.Cells(1)

cell.CellFormat.BackColor = Color.FromArgb(192, 192, 192)

cell.CellFormat.SamePaddingsAsTable = False

'Specify the left, right, top and bottom padding of the cell

cell.CellFormat.Paddings.All = 5

cell.CellFormat.VerticalAlignment = VerticalAlignment.Middle

document.Save("TableCellFormatting.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

Working with Table Style

A table style defines a set of table, row, cell and paragraph level formatting that can be applied to a table. **WTableStyle** instance represents table style in a Word document.

I> Note: Essential DocIO currently provides support for table styles in Docx formats alone. DocIO can preserve both built-in and customized table styles on opening Docx and saving as Docx format. The visual appearance is also preserved in Word to PDF, Word to Image, and Word to HTML conversions.

The following code snippet illustrates how to apply the built-in table styles to the table.

{% highlight c# %}
[C#]

WordDocument document = new WordDocument("Table.docx", FormatType.Docx);

WSection section = document.Sections[0];

WTable table = section.Tables[0] as WTable;

//Apply "LightShading" built-in style to table

table.ApplyStyle(BuiltinTableStyle.LightShading);

document.Save("TableStyle.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB]

Dim document As New WordDocument("Table.docx", FormatType.Docx)

Dim section As WSection = document.Sections(0)

Dim table As WTable = TryCast(section.Tables(0), WTable)

'Apply "LightShading" built-in style to table

table.ApplyStyle(BuiltinTableStyle.LightShading)

document.Save("TableStyle.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

### Table style options

Once you have applied a table style, you can enable or disable the special formatting of the table. There are six options: first column, last column, banded rows, banded columns, header row and last row.  

The following code snippet illustrates how to enable & disable the special table formatting options of the table styles

{% highlight c# %}
[C#]

WordDocument document = new WordDocument("Table.docx", FormatType.Docx);

WSection section = document.Sections[0];

WTable table = section.Tables[0] as WTable;

//Applies "LightShading" built-in style to table

table.ApplyStyle(BuiltinTableStyle.LightShading);

//Enable special formatting for banded columns of the table 

table.ApplyStyleForBandedColumns = true;

//Enable special formatting for banded rows of the table

table.ApplyStyleForBandedRows = true;

//Disable special formatting for first column of the table

table.ApplyStyleForFirstColumn = false;

//Enable special formatting for header row of the table

table.ApplyStyleForHeaderRow = true;

//Enable special formatting for last column of the table

table.ApplyStyleForLastColumn = true;

//Disable special formatting for last row of the table

table.ApplyStyleForLastRow = false;

document.Save("TableStyle.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB]

Dim document As New WordDocument("Table.docx", FormatType.Docx)

Dim section As WSection = document.Sections(0)

Dim table As WTable = TryCast(section.Tables(0), WTable)

'Applies "LightShading" built-in style to table

table.ApplyStyle(BuiltinTableStyle.LightShading)

'Enable special formatting for banded columns of the table 

table.ApplyStyleForBandedColumns = True

'Enable special formatting for banded rows of the table

table.ApplyStyleForBandedRows = True

'Disable special formatting for first column of the table

table.ApplyStyleForFirstColumn = False

'Enable special formatting for header row of the table

table.ApplyStyleForHeaderRow = True

'Enable special formatting for last column of the table

table.ApplyStyleForLastColumn = True

'Disable special formatting for last row of the table

table.ApplyStyleForLastRow = False

document.Save("TableStyle.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

## Merging cells vertically and horizontally

You can combine two or more table cells located in the same row or column into a single cell.

The following code snippet illustrate how to apply horizontal merge to specified range of cells in a specified row.

{% highlight c# %}
[C#]

WordDocument document = new WordDocument();

IWSection section = document.AddSection();

section.AddParagraph().AppendText("Vertical merging of Table cells");

IWTable table = section.AddTable();

table.ResetCells(5, 5);

// Specify the horizontal merge from second cell to fifth cell in third row

table.ApplyHorizontalMerge(2, 1, 4);

document.Save("HorizontalMerge.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB]

Dim document As New WordDocument()

Dim section As IWSection = document.AddSection()

section.AddParagraph().AppendText("Vertical merging of Table cells")

Dim table As IWTable = section.AddTable()

table.ResetCells(5, 5)

' Specify the horizontal merge from second cell to fifth cell in third row

table.ApplyHorizontalMerge(2, 1, 4)

document.Save("HorizontalMerge.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

The following code snippet illustrate how to apply vertical merge to specified range of rows in a specified column.

{% highlight c# %}
[C#]

WordDocument document = new WordDocument();

IWSection section = document.AddSection();

section.AddParagraph().AppendText("Vertical merging of Table cells");

IWTable table = section.AddTable();

table.ResetCells(5, 5);

// Specify the vertical merge to the third cell, from second row to fifth row

table.ApplyVerticalMerge(2, 1, 4);

document.Save("VerticalMerge.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB]

Dim document As New WordDocument()

Dim section As IWSection = document.AddSection()

section.AddParagraph().AppendText("Vertical merging of Table cells")

Dim table As IWTable = section.AddTable()

table.ResetCells(5, 5)

' Specify the vertical merge to the third cell, from second row to fifth row

table.ApplyVerticalMerge(2, 1, 4)

document.Save("VerticalMerge.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

The following code snippet illustrate how to create a table which contains horizontal merged cells.

{% highlight c# %}
[C#]

WordDocument document = new WordDocument();

IWSection section = document.AddSection();

section.AddParagraph().AppendText("Horizontal merging of Table cells");

IWTable table = section.AddTable();

table.ResetCells(2, 2);

//Add content to table cell

table[0, 0].AddParagraph().AppendText("First row, First cell");

table[0, 1].AddParagraph().AppendText("First row, Second cell");

table[1, 0].AddParagraph().AppendText("Second row, First cell");

table[1, 1].AddParagraph().AppendText("Second row, Second cell");

//Specify the horizontal merge start to first row, first cell

table[0, 0].CellFormat.HorizontalMerge = CellMerge.Start;

//modify the cell content

table[0, 0].Paragraphs[0].Text = "Horizontally merged cell";

//Specify the horizontal merge continue to second row second cell

table[0, 1].CellFormat.HorizontalMerge = CellMerge.Continue;

document.Save("HorizontalMerge.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB]

Dim document As New WordDocument()

Dim section As IWSection = document.AddSection()

section.AddParagraph().AppendText("Horizontal merging of Table cells")

Dim table As IWTable = section.AddTable()

table.ResetCells(2, 2)

'Add content to table cell

table(0, 0).AddParagraph().AppendText("First row, First cell")

table(0, 1).AddParagraph().AppendText("First row, Second cell")

table(1, 0).AddParagraph().AppendText("Second row, First cell")

table(1, 1).AddParagraph().AppendText("Second row, Second cell")

'Specify the horizontal merge start to first row, first cell

table(0, 0).CellFormat.HorizontalMerge = CellMerge.Start

'modify the cell content

table(0, 0).Paragraphs(0).Text = "Horizontally merged cell"

'Specify the horizontal merge continue to second row second cell

table(0, 1).CellFormat.HorizontalMerge = CellMerge.[Continue]

document.Save("HorizontalMerge.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

The following code snippet illustrate how to create a table with vertical merged cells.

{% highlight c# %}
[C#]

WordDocument document = new WordDocument();

IWSection section = document.AddSection();

section.AddParagraph().AppendText("Vertical merging of Table cells");

IWTable table = section.AddTable();

table.ResetCells(2, 2);

//Add content to table cells

table[0, 0].AddParagraph().AppendText("First row, First cell");

table[0, 1].AddParagraph().AppendText("First row, Second cell");

table[1, 0].AddParagraph().AppendText("Second row, First cell");

table[1, 1].AddParagraph().AppendText("Second row, Second cell");

//Specify the vertical merge start to first row first cell

table[0, 0].CellFormat.VerticalMerge = CellMerge.Start;

//modify the cell content

table[0, 0].Paragraphs[0].Text = "Vertically merged cell";

//Specify the vertical merge continue to second row first cell

table[1, 0].CellFormat.VerticalMerge = CellMerge.Continue;

document.Save("VerticalMerge.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB]

Dim document As New WordDocument()

Dim section As IWSection = document.AddSection()

section.AddParagraph().AppendText("Vertical merging of Table cells")

Dim table As IWTable = section.AddTable()

table.ResetCells(2, 2)

'Add content to table cells

table(0, 0).AddParagraph().AppendText("First row, First cell")

table(0, 1).AddParagraph().AppendText("First row, Second cell")

table(1, 0).AddParagraph().AppendText("Second row, First cell")

table(1, 1).AddParagraph().AppendText("Second row, Second cell")

'Specify the vertical merge start to first row first cell

table(0, 0).CellFormat.VerticalMerge = CellMerge.Start

'modify the cell content

table(0, 0).Paragraphs(0).Text = "Vertically merged cell"

'Specify the vertical merge continue to second row first cell

table(1, 0).CellFormat.VerticalMerge = CellMerge.[Continue]

document.Save("VerticalMerge.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

## Specifying table header row to repeat on each page

You can specify one or more rows in a table to be repeated as header row at the top of each page, when the table spans across multiple pages. 

* In the case of a single header row it must be the first row in the table. 
* In the case of multiple header rows, then header rows must be consecutive from first row of the table.
I> 
Note: Heading rows do not have any effect with nested tables in Microsoft Word as well as DocIO 

The following code snippet illustrate how to create a table with a single header row.

{% highlight c# %}
[C#]

WordDocument document = new WordDocument();

IWSection section = document.AddSection();

IWTable table = section.AddTable();

table.ResetCells(50, 1);

WTableRow row = table.Rows[0];

//Specify the first row as a header row of the table

row.IsHeader = true;

row.Height = 20;

row.HeightType = TableRowHeightType.AtLeast;

row.Cells[0].AddParagraph().AppendText("Header Row");

for (int i = 1; i < 50; i++)

{

row = table.Rows[i];

row.Height = 20;

row.HeightType = TableRowHeightType.AtLeast;

row.Cells[0].AddParagraph().AppendText("Text in Row" + i.ToString());

}

document.Save("TableWithHeaderRow.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB]

Dim document As New WordDocument()

Dim section As IWSection = document.AddSection()

Dim table As IWTable = section.AddTable()

table.ResetCells(50, 1)

Dim row As WTableRow = table.Rows(0)

'Specify the first row as a header row of the table

row.IsHeader = True

row.Height = 20

row.HeightType = TableRowHeightType.AtLeast

row.Cells(0).AddParagraph().AppendText("Header Row")

For i As Integer = 1 To 49

row = table.Rows(i)

row.Height = 20

row.HeightType = TableRowHeightType.AtLeast

row.Cells(0).AddParagraph().AppendText("Text in Row" + i.ToString())

Next

document.Save("TableWithHeaderRow.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

## Keeping rows from breaking across pages

You can enable or disable the table row content to split across multiple pages, when the row contents does not fit in previous page.

The following code snippet illustrate how to disable all the table rows from splitting across multiple pages.

{% highlight c# %}
[C#]

WordDocument document = new WordDocument("Template.docx");

WSection section = document.Sections[0];

WTable table = section.Tables[0] as WTable;

//Disable breaking across pages for all rows in the table.

foreach (WTableRow row in table.Rows)

row.RowFormat.IsBreakAcrossPages = false;

document.Save("Result.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB]

Dim document As New WordDocument("Template.docx")

Dim section As WSection = document.Sections(0)

Dim table As WTable = TryCast(section.Tables(0), WTable)

'Disable breaking across pages for all rows in the table.

For Each row As WTableRow In table.Rows

row.RowFormat.IsBreakAcrossPages = False

Next

document.Save("Result.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

## Iterating through table elements

The following code snippet illustrate how to iterate through the table and apply back color to particular cell.

{% highlight c# %}
[C#]

WordDocument document = new WordDocument("Template.docx");

WSection section = document.Sections[0];

WTable table = section.Tables[0] as WTable;

//Iterate the rows of the table

foreach (WTableRow row in table.Rows)

{

//Iterate through the cells of rows

foreach (WTableCell cell in row.Cells)

{

//Iterate through the paragraphs of the cell

foreach (WParagraph paragraph in cell.Paragraphs)

{

//If the paragraph contains text Panda then apply green as back color to cell

if (paragraph.Text.Contains("panda"))

cell.CellFormat.BackColor = Color.Green;

}

}

}

document.Save("Sample.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB]

Dim document As New WordDocument("Template.docx")

Dim section As WSection = document.Sections(0)

Dim table As WTable = TryCast(section.Tables(0), WTable)

'Iterate the rows of the table

For Each row As WTableRow In table.Rows

'Iterate through the cells of rows

For Each cell As WTableCell In row.Cells

'Iterate through the paragraphs of the cell

For Each paragraph As WParagraph In cell.Paragraphs

'If the paragraph contains text Panda then apply green as back color to cell

If paragraph.Text.Contains("panda") Then

cell.CellFormat.BackColor = Color.Green

End If

Next

Next

Next

document.Save("Sample.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

