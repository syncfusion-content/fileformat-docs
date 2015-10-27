---
title: Working with tables in PowerPoint Presentation
description: Working with tables in PowerPoint Presentation
platform: file-formats
control: Presentation
documentation: UG
---
# Working with Tables

## Creating a simple table

Essential Presentation facilitates developers to add tables from scratch. The following code example demonstrates how to add a simple table to a slide:

{% tabs %}

{% highlight c# %}

//Creates instance of PowerPoint presentation

IPresentation presentation = Presentation.Create();

//Adds slide to the presentation

ISlide slide = presentation.Slides.Add(SlideLayoutType.Blank);

//Adds table to the slide

ITable table = slide.Shapes.AddTable(2, 2, 100, 120, 300, 200);

//Retrieves each cell and fill text content to the cell.

ICell cell = table[0, 0];

cell.TextBody.AddParagraph("First Row and First Column");

cell = table[0, 1];

cell.TextBody.AddParagraph("First Row and Second Column");

cell = table[1, 0];

cell.TextBody.AddParagraph("Second Row and First Column");

cell = table[1, 1];

cell.TextBody.AddParagraph("Second Row and Second Column");

//Gives simple description to table shape

table.Description = "Table arrangement";

//Saves the presentation

presentation.Save("Table.pptx");

//Closes the presentation

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates instance of PowerPoint presentation

Dim presentationDocument As IPresentation = Presentation.Create()

'Adds slide to the presentation

Dim slide As ISlide = presentationDocument.Slides.Add(SlideLayoutType.Blank)

'Adds table to the slide

Dim table As ITable = slide.Shapes.AddTable(2, 2, 100, 120, 300, 200)

'Retrieves each cell and fills text content to the cell.

Dim cell As ICell = table(0, 0)

cell.TextBody.AddParagraph("First Row and First Column")

cell = table(0, 1)

cell.TextBody.AddParagraph("First Row and Second Column")

cell = table(1, 0)

cell.TextBody.AddParagraph("Second Row and First Column")

cell = table(1, 1)

cell.TextBody.AddParagraph("Second Row and Second Column")

'Gives simple description to table shape

table.Description = "Table arrangement"

'Saves the presentation

presentationDocument.Save("Table.pptx")

'Closes the presentation

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

## Apply table formatting

You can format a table to change its appearance by customizing the table border, cell background, cell margins etc. The following code example demonstrates how to apply the custom table formatting.

{% tabs %}

{% highlight c# %}

//Creates instance of PowerPoint presentation

IPresentation presentation = Presentation.Create();

//Adds slide to the presentation

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

//Saves the presentation

presentation.Save("Table.pptx");

//Closes the presentation

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates instance of PowerPoint presentation

Dim presentationDocument As IPresentation = Presentation.Create()

'Adds slide to the presentation

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

'Saves the presentation

presentationDocument.Save("Table.pptx")

'Closes the presentation

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

## Apply table styles

You can format a table by applying pre-defined table styles. The following code example demonstrates how to apply predefined styles to a table.

{% tabs %}

{% highlight c# %}

//Creates instance of PowerPoint presentation

IPresentation presentation = Presentation.Create();

//Adds slide to the presentation

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

//Saves the presentation

presentation.Save("Table.pptx");

//Closes the presentation

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates instance of PowerPoint presentation

Dim  presentationDocument As IPresentation = Presentation.Create()

'Adds slide to the presentation

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

'Saves the presentation

presentationDocument.Save("Table.pptx")

'Closes the presentation

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

## Modify the table

The following code example demonstrates how to modify the table in existing PowerPoint presentation.

{% tabs %}

{% highlight c# %}

//Creates instance of PowerPoint presentation

IPresentation presentation = Presentation.Open("Table.pptx");

//Gets slide from the presentation

ISlide slide = presentation.Slides[0];

//Gets table from slide

ITable table = slide.Shapes[0] as ITable;

//Modifies the table width

table.Width = 450;

//Changes the built in style of the table

table.BuiltInStyle = BuiltInTableStyle.DarkStyle1Accent2;

//Sets text content to the cell

table.Rows[0].Cells[0].TextBody.AddParagraph("Row1 Cell1");           

//Saves the presentation

presentation.Save("TableModified.pptx");

//Closes the presentation

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates instance of PowerPoint presentation

Dim presentationDocument As IPresentation = Presentation.Open("Table.pptx")

'Gets slide from the presentation

Dim slide As ISlide = presentationDocument.Slides(0)

'Gets table from slide

Dim table As ITable = TryCast(slide.Shapes(0), ITable)

'Modifies the table width

table.Width = 450

'Changes the built in style of the table

table.BuiltInStyle = BuiltInTableStyle.DarkStyle1Accent2

'Sets text content to the cell

table.Rows(0).Cells(0).TextBody.AddParagraph("Row1 Cell1")

'Saves the presentation

presentationDocument.Save("TableModified.pptx")

'Closes the presentation

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

## Merge the cells

The following code example shows how to merge cells in a table.

{% tabs %}

{% highlight c# %}

//Creates instance of PowerPoint presentation

IPresentation presentation = Presentation.Create();

//Adds slide to the presentation

ISlide slide = presentation.Slides.Add(SlideLayoutType.Blank);

//Adds table to the slide

ITable table = slide.Shapes.AddTable(2, 2, 100, 120, 300, 200);

//Retrieves first cell.

ICell firstCell = table[0, 0];

//Sets the columnspan to merge the cell.

firstCell.ColumnSpan = 2;

//Retrieves each cell and fills text content to the cell.

ICell cell = table[0, 0];

cell.TextBody.AddParagraph("First Row and First Column");

cell = table[0, 1];

cell.TextBody.AddParagraph("First Row and Second Column");

cell = table[1, 0];

cell.TextBody.AddParagraph("Second Row and First Column");

cell = table[1, 1];

cell.TextBody.AddParagraph("Second Row and Second Column");

//Gives simple description to table shape

table.Description = "Table arrangement";

//Saves the presentation

presentation.Save("Table.pptx");

//Closes the presentation

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates instance of PowerPoint presentation

Dim presentationDocument As IPresentation = Presentation.Create()

'Adds slide to the presentation

Dim slide As ISlide = presentationDocument.Slides.Add(SlideLayoutType.Blank)

'Adds table to the slide

Dim table As ITable = slide.Shapes.AddTable(2, 2, 100, 120, 300, 200)

'Retrieves first cell.

Dim firstCell As ICell = table(0, 0)

'Sets the columnspan to merge the cell.

firstCell.ColumnSpan = 2

'Retrieves each cell and fills text content to the cell.

Dim cell As ICell = table(0, 0)

cell.TextBody.AddParagraph("First Row and First Column")

cell = table(0, 1)

cell.TextBody.AddParagraph("First Row and Second Column")

cell = table(1, 0)

cell.TextBody.AddParagraph("Second Row and First Column")

cell = table(1, 1)

cell.TextBody.AddParagraph("Second Row and Second Column")

'Gives simple description to table shape

table.Description = "Table arrangement"

'Saves the presentation

presentationDocument.Save("Table.pptx")

'Closes the presentation

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

## Remove the table

You can remove a table from a slide by its instance or by its index position in the shape collection. The following code example demonstrates removing a table in a slide.

{% tabs %}

{% highlight c# %}

//Creates instance of PowerPoint presentation

IPresentation presentation = Presentation.Open("Table.pptx");

//Gets slide from the presentation

ISlide slide = presentation.Slides[0];

//Gets the table from slide

ITable table = slide.Shapes[0] as ITable;

//Removes table from shape collection

slide.Shapes.Remove(table);

//Saves the presentation

presentation.Save("TableRemoved.pptx");

//Closes the presentation

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates instance of PowerPoint presentation

Dim presentationDocument As IPresentation = Presentation.Open("Table.pptx")

'Gets slide from the presentation

Dim slide As ISlide = presentationDocument.Slides(0)

'Gets the table from slide

Dim table As ITable = TryCast(slide.Shapes(0), ITable)

'Removes table from shape collection

slide.Shapes.Remove(table)

'Saves the presentation

presentationDocument.Save("TableRemoved.pptx")

'Closes the presentation

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}