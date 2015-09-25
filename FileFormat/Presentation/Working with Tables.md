---
layout: Post
title: Working with tables in PowerPoint Presentation
description: Working with tables in PowerPoint Presentation
platform: FileFormats
control: Presentation
documentation: UG
---
# Working with Tables

## Creating a simple table

Essential Presentation facilitates developers to add tables from scratch. The below code snippet demonstrates adding a simple table to a slide:

{% highlight c# %}
[C#]

//Create instance of PowerPoint presentation

IPresentation presentation = Presentation.Create();

//Add slide to the presentation

ISlide slide = presentation.Slides.Add(SlideLayoutType.Blank);

//Add table to the slide

ITable table = slide.Shapes.AddTable(2, 2, 100, 120, 300, 200);

//Retrieve each cell and fill text content to the cell.

ICell cell = table[0, 0];

cell.TextBody.AddParagraph("First Row and First Column");

cell = table[0, 1];

cell.TextBody.AddParagraph("First Row and Second Column");

cell = table[1, 0];

cell.TextBody.AddParagraph("Second Row and First Column");

cell = table[1, 1];

cell.TextBody.AddParagraph("Second Row and Second Column");

//Give simple description to table shape

table.Description = "Table arrangement";

//Save the presentation

presentation.Save("Table.pptx");

//Close the presentation

presentation.Close();



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Create instance of PowerPoint presentation

Dim presentation_1 As IPresentation = Presentation.Create()

'Add slide to the presentation

Dim slide As ISlide = presentation_1.Slides.Add(SlideLayoutType.Blank)

'Add table to the slide

Dim table As ITable = slide.Shapes.AddTable(2, 2, 100, 120, 300, 200)

'Retrieve each cell and fill text content to the cell.

Dim cell As ICell = table(0, 0)

cell.TextBody.AddParagraph("First Row and First Column")

cell = table(0, 1)

cell.TextBody.AddParagraph("First Row and Second Column")

cell = table(1, 0)

cell.TextBody.AddParagraph("Second Row and First Column")

cell = table(1, 1)

cell.TextBody.AddParagraph("Second Row and Second Column")

'Give simple description to table shape

table.Description = "Table arrangement"

'Save the presentation

presentation_1.Save("Table.pptx")

'Close the presentation

presentation_1.Close()



{% endhighlight %}

## Applying table formatting

You can format a table to change its appearance by customizing the table border, cell background, cell margins etc. The below code snippet demonstrates applying the custom table formatting.

{% highlight c# %}
[C#]

//Create instance of PowerPoint presentation

IPresentation presentation = Presentation.Create();

//Add slide to the presentation

ISlide slide = presentation.Slides.Add(SlideLayoutType.Blank);

//Add table to the slide

ITable table = slide.Shapes.AddTable(2, 2, 100, 120, 300, 200);

//Retrieve each cell and fill text content to the cell.

ICell cell = table[0, 0];

//Set the column width for a cell; this will set the width for entire column

cell.ColumnWidth = 400;

//Set the margin for the cell.

cell.TextBody.MarginBottom = 0;

cell.TextBody.MarginLeft = 58;

cell.TextBody.MarginRight = 29;

cell.TextBody.MarginTop = 65;

//Set the back color for the cell.

cell.Fill.SolidFill.Color.SystemColor = Color.Orange;

cell.TextBody.AddParagraph("First Row and First Column");

cell = table[0, 1];

//Set the margin for the cell.

cell.TextBody.MarginLeft = 58;

cell.TextBody.MarginRight = 29;

cell.TextBody.MarginTop = 65;

//Set the back color for the cell.

cell.Fill.SolidFill.Color.SystemColor = Color.BlueViolet;

cell.TextBody.AddParagraph("First Row and Second Column");

cell = table[1, 0];

//Set the margin for the cell.

cell.TextBody.MarginLeft = 58;

cell.TextBody.MarginRight = 29;

cell.TextBody.MarginTop = 65;

//Set the back color for the cell.

cell.Fill.SolidFill.Color.SystemColor = Color.SandyBrown;

cell.TextBody.AddParagraph("Second Row and First Column");

cell = table[1, 1];

//Set the margin for the cell.

cell.TextBody.MarginLeft = 58;

cell.TextBody.MarginRight = 29;

cell.TextBody.MarginTop = 65;

//Set the back color for the cell.

cell.Fill.SolidFill.Color.SystemColor = Color.Silver;

cell.TextBody.AddParagraph("Second Row and Second Column");

//Save the presentation

presentation.Save("Table.pptx");

//Close the presentation

presentation.Close();



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Create instance of PowerPoint presentation

Dim presentation_1 As IPresentation = Presentation.Create()

'Add slide to the presentation

Dim slide As ISlide = presentation_1.Slides.Add(SlideLayoutType.Blank)

'Add table to the slide

Dim table As ITable = slide.Shapes.AddTable(2, 2, 100, 120, 300, 200)

'Retrieve each cell and fill text content to the cell.

Dim cell As ICell = table(0, 0)

'Set the column width for a cell; this will set the width for entire column

cell.ColumnWidth = 400

'Set the margin for the cell.

cell.TextBody.MarginBottom = 0

cell.TextBody.MarginLeft = 58

cell.TextBody.MarginRight = 29

cell.TextBody.MarginTop = 65

'Set the back color for the cell.

cell.Fill.SolidFill.Color.SystemColor = Color.Orange

cell.TextBody.AddParagraph("First Row and First Column")

cell = table(0, 1)

'Set the margin for the cell.

cell.TextBody.MarginLeft = 58

cell.TextBody.MarginRight = 29

cell.TextBody.MarginTop = 65

'Set the back color for the cell.

cell.Fill.SolidFill.Color.SystemColor = Color.BlueViolet

cell.TextBody.AddParagraph("First Row and Second Column")

cell = table(1, 0)

'Set the margin for the cell.

cell.TextBody.MarginLeft = 58

cell.TextBody.MarginRight = 29

cell.TextBody.MarginTop = 65

'Set the back color for the cell.

cell.Fill.SolidFill.Color.SystemColor = Color.SandyBrown

cell.TextBody.AddParagraph("Second Row and First Column")

cell = table(1, 1)

'Set the margin for the cell.

cell.TextBody.MarginLeft = 58

cell.TextBody.MarginRight = 29

cell.TextBody.MarginTop = 65

'Set the back color for the cell.

cell.Fill.SolidFill.Color.SystemColor = Color.Silver

cell.TextBody.AddParagraph("Second Row and Second Column")

'Save the presentation

presentation_1.Save("Table.pptx")

'Close the presentation

presentation_1.Close()



{% endhighlight %}

## Applying table styles

You can format a table by applying pre-defined table styles. The below code snippet demonstrates applying predefined styles to a table.

{% highlight c# %}
[C#]

//Create instance of PowerPoint presentation

IPresentation presentation = Presentation.Create();

//Add slide to the presentation

ISlide slide = presentation.Slides.Add(SlideLayoutType.Blank);

//Add table to the slide

ITable table = slide.Shapes.AddTable(3, 3, 100, 120, 300, 200);

table.BuiltInStyle = BuiltInTableStyle.ThemedStyle2Accent4;

table.HasBandedRows = false;

table.HasHeaderRow = false;

table.HasBandedColumns = true;

table.HasFirstColumn = true;

table.HasLastColumn = true;

table.HasTotalRow = true;

//Retrieve each cell and fill text content to the cell.

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

//Add description to table shape

table.Description = "Table arrangement";

//Save the presentation

presentation.Save("Table.pptx");

//Close the presentation

presentation.Close();



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Create instance of PowerPoint presentation

Dim  presentation_1 As IPresentation = Presentation.Create()

'Add slide to the presentation

Dim slide As ISlide =  presentation_1 .Slides.Add(SlideLayoutType.Blank)

'Add table to the slide

Dim table As ITable = slide.Shapes.AddTable(3, 3, 100, 120, 300, 200)

table.BuiltInStyle = BuiltInTableStyle.ThemedStyle2Accent4

table.HasBandedRows = False

table.HasHeaderRow = False

table.HasBandedColumns = True

table.HasFirstColumn = True

table.HasLastColumn = True

table.HasTotalRow = True

'Retrieve each cell and fill text content to the cell.

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

'Add description to table shape

table.Description = "Table arrangement"

'Save the presentation

presentation_1.Save("Table.pptx")

'Close the presentation

presentation_1.Close()



{% endhighlight %}

## Modifying the table

The below code snippet demonstrates how to modify the table in existing PowerPoint presentation.

{% highlight vb.net %}
[C#]

//Create instance of PowerPoint presentation

IPresentation presentation = Presentation.Open("Table.pptx");

//Get slide from the presentation

ISlide slide = presentation.Slides[0];

//Get table from slide

ITable table = slide.Shapes[0] as ITable;

//Modify the table width

table.Width = 450;

//Change the built in style of the table

table.BuiltInStyle = BuiltInTableStyle.DarkStyle1Accent2;

//Set text content to the cell

table.Rows[0].Cells[0].TextBody.AddParagraph("Row1 Cell1");           

//Save the presentation

presentation.Save("TableModified.pptx");

//Close the presentation

presentation.Close();



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Create instance of PowerPoint presentation

Dim presentation_1 As IPresentation = Presentation.Open("Table.pptx")

'Get slide from the presentation

Dim slide As ISlide = presentation_1.Slides(0)

'Get table from slide

Dim table As ITable = TryCast(slide.Shapes(0), ITable)

'Modify the table width

table.Width = 450

'Change the built in style of the table

table.BuiltInStyle = BuiltInTableStyle.DarkStyle1Accent2

'Set text content to the cell

table.Rows(0).Cells(0).TextBody.AddParagraph("Row1 Cell1")

'Save the presentation

presentation_1.Save("TableModified.pptx")

'Close the presentation

presentation_1.Close()



{% endhighlight %}

## Merging the cells

The below code snippet shows how to merge cells in a table.

{% highlight c# %}
[C#]

//Create instance of PowerPoint presentation

IPresentation presentation = Presentation.Create();

//Add slide to the presentation

ISlide slide = presentation.Slides.Add(SlideLayoutType.Blank);

//Add table to the slide

ITable table = slide.Shapes.AddTable(2, 2, 100, 120, 300, 200);

//Retrieve first cell.

ICell firstCell = table[0, 0];

//Set the columnspan to merge the cell.

firstCell.ColumnSpan = 2;

//Retrieve each cell and fill text content to the cell.

ICell cell = table[0, 0];

cell.TextBody.AddParagraph("First Row and First Column");

cell = table[0, 1];

cell.TextBody.AddParagraph("First Row and Second Column");

cell = table[1, 0];

cell.TextBody.AddParagraph("Second Row and First Column");

cell = table[1, 1];

cell.TextBody.AddParagraph("Second Row and Second Column");

//Give simple description to table shape

table.Description = "Table arrangement";

//Save the presentation

presentation.Save("Table.pptx");

//Close the presentation

presentation.Close();



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Create instance of PowerPoint presentation

Dim presentation_1 As IPresentation = Presentation.Create()

'Add slide to the presentation

Dim slide As ISlide = presentation_1.Slides.Add(SlideLayoutType.Blank)

'Add table to the slide

Dim table As ITable = slide.Shapes.AddTable(2, 2, 100, 120, 300, 200)

'Retrieve first cell.

Dim firstCell As ICell = table(0, 0)

'Set the columnspan to merge the cell.

firstCell.ColumnSpan = 2

'Retrieve each cell and fill text content to the cell.

Dim cell As ICell = table(0, 0)

cell.TextBody.AddParagraph("First Row and First Column")

cell = table(0, 1)

cell.TextBody.AddParagraph("First Row and Second Column")

cell = table(1, 0)

cell.TextBody.AddParagraph("Second Row and First Column")

cell = table(1, 1)

cell.TextBody.AddParagraph("Second Row and Second Column")

'Give simple description to table shape

table.Description = "Table arrangement"

'Save the presentation

presentation_1.Save("Table.pptx")

'Close the presentation

presentation_1.Close()



{% endhighlight %}

## Removing the table

You can remove a table from a slide by its instance or by its index position in the shape collection. The below code snippet demonstrates removing a table in a slide.

{% highlight c# %}
[C#]

//Create instance of PowerPoint presentation

IPresentation presentation = Presentation.Open("Table.pptx");

//Get slide from the presentation

ISlide slide = presentation.Slides[0];

//Get the table from slide

ITable table = slide.Shapes[0] as ITable;

//Remove table from shape collection

slide.Shapes.Remove(table);

//Save the presentation

presentation.Save("TableRemoved.pptx");

//Close the presentation

presentation.Close();



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Create instance of PowerPoint presentation

Dim presentation_1 As IPresentation = Presentation.Open("Table.pptx")

'Get slide from the presentation

Dim slide As ISlide = presentation_1.Slides(0)

'Get the table from slide

Dim table As ITable = TryCast(slide.Shapes(0), ITable)

'Remove table from shape collection

slide.Shapes.Remove(table)

'Save the presentation

presentation_1.Save("TableRemoved.pptx")

'Close the presentation

presentation_1.Close()



{% endhighlight %}

