---
title: Working with Tagged PDF
description: This section explains how to create a tagged PDF document by using Essential PDF
platform: file-formats
control: PDF
documentation: UG
---

# Tagged PDF

## Introduction

The Tagged PDF is PDF that includes structure in terms for a set of instruction that defines, reading order, and meaning of significant elements such as figures, images, lists, tables and so on. 
Usually tagged PDF used to making content accessible to users who rely on assistive technology.

This section explains how to add tags to PDF elements such as text element, Image, Shapes, Form fields, Annotations, Table, List, etc.,

## Adding tag to Text Element

You can add tag to text/paragraphs in PDF document by specifying the ```PdfTag``` property available in the ```PdfTextElement``` class and specifying the tag type as ```PdfTagType.Paragraph``` in the ```PdfStructureElement``` class.

The following code sample explains you how to add tag for the text element in PDF document.

{% tabs %}
{% highlight c# %}

//Creates new PDF document
PdfDocument doc = new PdfDocument();

//Set the document title
doc.DocumentInformation.Title = "PdfTextElement";

//Creates new page.
PdfPage page = doc.Pages.Add();

//Initialize the structure element with tag type paragraph.
PdfStructureElement structureElement = new PdfStructureElement(PdfTagType.Paragraph);

//represents the text that is exact replacement for PdfTextElement
structureElement.ActualText = "Simple paragraph element";

string text = "Adventure Works Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company. The company manufactures and sells metal and composite bicycles to North American, European and Asian commercial markets. While its base operation is located in Washington with 290 employees, several regional sales teams are located throughout their market base.";

//Initialize the PDF text element
PdfTextElement element = new PdfTextElement(text);

//Adding tag to the text element.
element.PdfTag = structureElement;

//Creates font for the text element
element.Font = new PdfStandardFont(PdfFontFamily.TimesRoman, 12);

element.Brush = new PdfSolidBrush(new PdfColor(89, 89, 93));

//Draws Text
PdfLayoutResult result = element.Draw(page, new RectangleF(0, 0, page.Graphics.ClientSize.Width, 200));

//Save the document and dispose it.
doc.Save("Output.pdf");

doc.Close(true);

{% endhighlight %}
{% highlight vb.net %}

'Creates new PDF document
Dim doc As PdfDocument = New PdfDocument()

'Set the document title
doc.DocumentInformation.Title = "PdfTextElement"

'Creates new page.
Dim page As PdfPage = doc.Pages.Add()

'Initialize the structure element with tag type paragraph.
Dim structureElement As PdfStructureElement = New PdfStructureElement(PdfTagType.Paragraph)

'represents the text that is exact replacement for PdfTextElement
structureElement.ActualText = "Simple paragraph element"

Dim text As String = "Adventure Works Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company. The company manufactures and sells metal and composite bicycles to North American, European and Asian commercial markets. While its base operation is located in Washington with 290 employees, several regional sales teams are located throughout their market base."

'Initialize the PDF text element
Dim element As PdfTextElement = New PdfTextElement(text)

'Adding tag to the text element.
element.PdfTag = structureElement

'Creates font for the text element
element.Font = New PdfStandardFont(PdfFontFamily.TimesRoman, 12)

element.Brush = New PdfSolidBrush(New PdfColor(89, 89, 93))

'Draws Text
Dim result As PdfLayoutResult = element.Draw(page, New RectangleF(0, 0, page.Graphics.ClientSize.Width, 200))

'Save the document and dispose it.
doc.Save("Output.pdf")

doc.Close(True)

{% endhighlight %}
{% endtabs %}

## Adding tag to Image

You can add tag to image in the PDF document by using the ```PdfTag``` property available in the ```PdfBitmap``` class and specifying the tag type as ```PdfTagType.Figure``` available in ```PdfStructureElement``` class. You can add alternate text to image by using ```AlternateText``` property available in the ```PdfStructureElement``` class.

The following code explains how to add tag for Image element in PDF document.

{% tabs %}
{% highlight c# %}

//Creates new PDF document
PdfDocument doc = new PdfDocument();

//Set the document title
doc.DocumentInformation.Title = "Image";

//Creates new page.
PdfPage page = doc.Pages.Add();

//Draw string
page.Graphics.DrawString("JPEG Image:", new PdfStandardFont(PdfFontFamily.Helvetica, 12, PdfFontStyle.Bold), PdfBrushes.Blue, new PointF(0, 0));

//Create a new PDF bitmap object
PdfBitmap bitmap = new PdfBitmap("syncfusion.jpg");

//Set the tag type.
PdfStructureElement imageElement = new PdfStructureElement(PdfTagType.Figure);

//Set the alternate text.
imageElement.AlternateText = "GreenTree";

//adding tag to the PDF image
bitmap.PdfTag = imageElement;

//Draw image
bitmap.Draw(page.Graphics, new PointF(50, 20));

//Save the document and dispose it.
doc.Save("Image.pdf");

doc.Close(true);

{% endhighlight %}
{% highlight vb.net %}

'Creates new PDF document
Dim doc As PdfDocument = New PdfDocument()

'Set the document title
doc.DocumentInformation.Title = "Image"

'Creates new page.
Dim page As PdfPage = doc.Pages.Add()

'Draw string
page.Graphics.DrawString("JPEG Image:", New PdfStandardFont(PdfFontFamily.Helvetica, 12, PdfFontStyle.Bold), PdfBrushes.Blue, New PointF(0, 0))

'Create a new PDF bitmap object
Dim bitmap As PdfBitmap = New PdfBitmap("syncfusion.jpg")

'Set the tag type.
Dim imageElement As PdfStructureElement = New PdfStructureElement(PdfTagType.Figure)

'Set the alternate text.
imageElement.AlternateText = "GreenTree"

'adding tag to the PDF image
bitmap.PdfTag = imageElement

'Draw image
bitmap.Draw(page.Graphics, New PointF(50, 20))

'Save the document and dispose it.
doc.Save("Image.pdf")

doc.Close(True) 

{% endhighlight %}
{% endtabs %}

## Adding tag to Shapes

You can add tag to shapes such as rectangle, line, circle and polygon etc., by using ```PdfTag``` property and specifying the tag type as ```PdfTagType.Figure```. you can set alternate text to shapes by using ```AlternateText``` property available in ```PdfStructureElement``` class.

The following code explains how to add tag for Shape element in PDF document.

{% tabs %}
{% highlight c# %}

//Creates new PDF document.
PdfDocument doc = new PdfDocument();

//Set the document title
doc.DocumentInformation.Title = "LineShape";

//Add new page
PdfPage page = doc.Pages.Add();

//Draw text.
page.Graphics.DrawString("Line Shape:", new PdfStandardFont(PdfFontFamily.Helvetica, 12, PdfFontStyle.Bold), PdfBrushes.Blue, new PointF(30, 80));

//Initialize structure element with tag type as Figure
PdfStructureElement element = new PdfStructureElement(PdfTagType.Figure);

//Set alternate text
element.AlternateText = "Line Sample";

//Initialize the line shape
PdfLine line = new PdfLine(100, 100, 100, 300);

line.Pen = new PdfPen(Color.Red);

//Adding tag to the line element
line.PdfTag = element;

//Draws the line
line.Draw(page.Graphics);

//Save the document and dispose it.
doc.Save("Output.pdf"); 

{% endhighlight %}
{% highlight vb.net %}

'Creates new PDF document.
Dim doc As PdfDocument = New PdfDocument()

'Set the document title
doc.DocumentInformation.Title = "LineShape"

'Add new page
Dim page As PdfPage = doc.Pages.Add()

'Draw text.
page.Graphics.DrawString("Line Shape:", New PdfStandardFont(PdfFontFamily.Helvetica, 12, PdfFontStyle.Bold), PdfBrushes.Blue, New PointF(30, 80))

'Initialize structure element with tag type as Figure
Dim element As PdfStructureElement = New PdfStructureElement(PdfTagType.Figure)

'Set alternate text
element.AlternateText = "Line Sample"

'Initialize the line shape
Dim line As PdfLine = New PdfLine(100, 100, 100, 300)

line.Pen = New PdfPen(Color.Red)

'Adding tag to the line element
line.PdfTag = element

'Draws the line
line.Draw(page.Graphics)

'Save the document and dispose it.
doc.Save("Output.pdf")

{% endhighlight %}
{% endtabs %}

## Adding tag to Form Fields

You can tag the form fields in the PDF document by using ```PdfTag``` property, the supported tag type is ```PdfTagType.Form```.

The following code explains how to add tag for the form fields in PDF document.

{% tabs %}
{% highlight c# %}

//Creates new PDF document
PdfDocument doc = new PdfDocument();

doc.DocumentInformation.Title = "Form Fields";

//Adds new page
PdfPage page = doc.Pages.Add();

// Create a Text box field.
PdfTextBoxField textBoxField = new PdfTextBoxField(page, "This is form field text box");

//Adding tag to the text box field
textBoxField.PdfTag = new PdfStructureElement(PdfTagType.Form);

textBoxField.Text = "Filled text box";

//Set properties to the textbox.
textBoxField.Font = new PdfStandardFont(PdfFontFamily.Helvetica, 12);

textBoxField.BorderColor = new PdfColor(Color.Gray);

textBoxField.BorderStyle = PdfBorderStyle.Beveled;

textBoxField.Bounds = new RectangleF(200, 0, 90, 20);

textBoxField.ToolTip = "TextBox field";

doc.Form.Fields.Add(textBoxField);

//Save the document and dispose it.
doc.Save("Output.pdf");

doc.Close(true);

{% endhighlight %}
{% highlight vb.net %}

'Creates new PDF document
Dim doc As PdfDocument = New PdfDocument()

doc.DocumentInformation.Title = "Form Fields"

'Adds new page
Dim page As PdfPage = doc.Pages.Add()

' Create a Text box field.
Dim textBoxField As PdfTextBoxField = New PdfTextBoxField(page, "This is form field text box")

'Adding tag to the text box field
textBoxField.PdfTag = New PdfStructureElement(PdfTagType.Form)

textBoxField.Text = "Filled text box"

'Set properties to the textbox.
textBoxField.Font = New PdfStandardFont(PdfFontFamily.Helvetica, 12)

textBoxField.BorderColor = New PdfColor(Color.Gray)

textBoxField.BorderStyle = PdfBorderStyle.Beveled

textBoxField.Bounds = New RectangleF(200, 0, 90, 20)

textBoxField.ToolTip = "TextBox field"

doc.Form.Fields.Add(textBoxField)

'Save the document and dispose it.
doc.Save("Output.pdf")

doc.Close(True)

{% endhighlight %}
{% endtabs %}

## Adding tag to Annotation

You can add tags to annotation in PDF document by using ```PdfTag``` property available in the Annotation class, you need to specify the tag type as ```PdfTagType.Annotation```.

The following code explains how to add tag for the annotations in PDF document.

{% tabs %}
{% highlight c# %}

//Creates new PDF document.
PdfDocument doc = new PdfDocument();

//Set the document title
doc.DocumentInformation.Title = "LineShape";

//Add new page
PdfPage page = doc.Pages.Add();

//Initialize the structure element with tag type as annotation
PdfStructureElement structureElement = new PdfStructureElement(PdfTagType.Annotation);

structureElement.AlternateText = "Popup Annotation";

RectangleF rectangle = new RectangleF(10, 40, 30, 30);

PdfPopupAnnotation popupAnnotation = new PdfPopupAnnotation(rectangle, "Test popup annotation");

//Adding tag for the annotation
popupAnnotation.PdfTag = structureElement;

popupAnnotation.Border.Width = 4;

popupAnnotation.Border.HorizontalRadius = 20;

popupAnnotation.Border.VerticalRadius = 30;

//Sets the PDF pop-up icon.
popupAnnotation.Icon = PdfPopupIcon.NewParagraph;

//Adds this annotation to a new page.
page.Annotations.Add(popupAnnotation);

//Saves the document to disk.
doc.Save("PopupAnnotation.pdf");

//Close the PDF document
doc.Close(true);

{% endhighlight %}
{% highlight vb.net %}

'Creates new PDF document.
Dim doc As PdfDocument = New PdfDocument()

'Set the document title
doc.DocumentInformation.Title = "LineShape"

'Add new page
Dim page As PdfPage = doc.Pages.Add()

'Initialize the structure element with tag type as annotation
Dim structureElement As PdfStructureElement = New PdfStructureElement(PdfTagType.Annotation)

structureElement.AlternateText = "Popup Annotation"

Dim rectangle As RectangleF = New RectangleF(10, 40, 30, 30)

Dim popupAnnotation As PdfPopupAnnotation = New PdfPopupAnnotation(rectangle, "Test popup annotation")

'Adding tag for the annotation
popupAnnotation.PdfTag = structureElement

popupAnnotation.Border.Width = 4

popupAnnotation.Border.HorizontalRadius = 20

popupAnnotation.Border.VerticalRadius = 30

'Sets the PDF pop-up icon.
popupAnnotation.Icon = PdfPopupIcon.NewParagraph

'Adds this annotation to a new page.
page.Annotations.Add(popupAnnotation)

'Saves the document to disk.
doc.Save("PopupAnnotation.pdf")

'Close the PDF document
doc.Close(True)

{% endhighlight %}
{% endtabs %}

## Adding tag to Hyperlink

You can tag the hyperlink present in the PDF document by using ```PdfTag``` available in the ```PdfTextWebLink``` class and the tag type is ```PdfTagType.Link```. 

The following code example shows how to add tag for hyperlink in PDF document

{% tabs %}
{% highlight c# %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();

document.DocumentInformation.Title = "Link";

//Add a page to the document.
PdfPage page = document.Pages.Add();

//Creates new pdf structure element with tag type link.
PdfStructureElement linkStructureElement = new PdfStructureElement(PdfTagType.Link);

//Create the font.
PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 12f);

//Create the Text Web Link.
PdfTextWebLink textLink = new PdfTextWebLink();

//Adding tag to text web link.
textLink.PdfTag = linkStructureElement;

//Set the hyperlink
textLink.Url = "http://www.syncfusion.com";

//Set the link text
textLink.Text = "Syncfusion .NET components and controls";

//Set the font
textLink.Font = font;

textLink.Brush = PdfBrushes.Blue;

//Draw the hyperlink in PDF page
textLink.DrawTextWebLink(page, new PointF(10, 40));

//Save the document.
document.Save("Output.pdf");

//Close the document.
document.Close(true);

{% endhighlight %}
{% highlight vb.net %}

'Create a new PDF document.
Dim document As PdfDocument = New PdfDocument()

document.DocumentInformation.Title = "Link"

'Add a page to the document.
Dim page As PdfPage = document.Pages.Add()

'Creates new pdf structure element with tag type link.
Dim linkStructureElement As PdfStructureElement = New PdfStructureElement(PdfTagType.Link)

'Create the font.
Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 12.0F)

'Create the Text Web Link.
Dim textLink As PdfTextWebLink = New PdfTextWebLink()

'Adding tag to text web link.
textLink.PdfTag = linkStructureElement

'Set the hyperlink
textLink.Url = "http://www.syncfusion.com"

'Set the link text
textLink.Text = "Syncfusion .NET components and controls"

'Set the font
textLink.Font = font

textLink.Brush = PdfBrushes.Blue

'Draw the hyperlink in PDF page
textLink.DrawTextWebLink(page, New PointF(10, 40))

'Save the document.
document.Save("Output.pdf")

'Close the document.
document.Close(True)

{% endhighlight %}
{% endtabs %}

## Adding tag to Template

You can add tags to template in PDF document by using ```PdfTag``` property available in the ```PdfTemplate``` class. 

The following code sample explains how to add tag support for the template element.

{% tabs %}
{% highlight c# %}

//Creates a new PDF document
PdfDocument pdfDocument = new PdfDocument();

pdfDocument.DocumentInformation.Title = "TemplateDocument";

//Add a page to the PDF document.
PdfPage pdfPage = pdfDocument.Pages.Add();

pdfPage.Graphics.DrawString("Rectangle:", new PdfStandardFont(PdfFontFamily.Helvetica, 12, PdfFontStyle.Bold), PdfBrushes.Blue, new PointF(0, 0));

//Create a PDF Template.
PdfTemplate template = new PdfTemplate(100, 50);

//Initialize the structure element with tag type figure.
PdfStructureElement structureElement = new PdfStructureElement(PdfTagType.Figure);

//Set alternative description for figure.
structureElement.AlternateText = "Template Figure";

//Adding tag to the template element.
template.PdfTag = structureElement;

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 14);

PdfBrush brush = new PdfSolidBrush(Color.Pink);

//Draw rectangle using template graphics
template.Graphics.DrawRectangle(brush, new RectangleF(0, 30, 150, 90));

//Draw the template on the page graphics of the document.
pdfPage.Graphics.DrawPdfTemplate(template, PointF.Empty);

//Save the document and dispose it.
pdfDocument.Save("Output.pdf");

pdfDocument.Close(true);

{% endhighlight %}
{% highlight vb.net %}

'Creates a new PDF document
Dim pdfDocument As PdfDocument = New PdfDocument()

pdfDocument.DocumentInformation.Title = "TemplateDocument"

'Add a page to the PDF document.
Dim pdfPage As PdfPage = pdfDocument.Pages.Add()

pdfPage.Graphics.DrawString("Rectangle:", New PdfStandardFont(PdfFontFamily.Helvetica, 12, PdfFontStyle.Bold), PdfBrushes.Blue, New PointF(0, 0))

'Create a PDF Template.
Dim template As PdfTemplate = New PdfTemplate(100, 50)

'Initialize the structure element with tag type figure.
Dim structureElement As PdfStructureElement = New PdfStructureElement(PdfTagType.Figure)

'Set alternative description for figure.
structureElement.AlternateText = "Template Figure"

'Adding tag to the template element.
template.PdfTag = structureElement

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 14)

Dim brush As PdfBrush = New PdfSolidBrush(Color.Pink)

'Draw rectangle using template graphics
template.Graphics.DrawRectangle(brush, New RectangleF(0, 30, 150, 90))

'Draw the template on the page graphics of the document.
pdfPage.Graphics.DrawPdfTemplate(template, PointF.Empty)

'Save the document and dispose it.
pdfDocument.Save("Output.pdf")

pdfDocument.Close(True)

{% endhighlight %}
{% endtabs %}

## Adding tag to Table

You can tag the table in the PDF document by using the tag type ```PdfTagType.Table```. The following tag types are used to mention the table header, rows and cells.

1. PdfTagType.TableHeader
2. PdfTagType.TableRow
3. PdfTagType.TableDataCell

The following code snippet illustrates how to add tag for table element.

{% tabs %}
{% highlight c# %}

//Creates a new PDF document.
PdfDocument pdfDocument = new PdfDocument();

pdfDocument.DocumentInformation.Title = "Table";

//Adds new page
PdfPage pdfPage = pdfDocument.Pages.Add();

//Initialize the new structure element with tag type table
PdfStructureElement element = new PdfStructureElement(PdfTagType.Table);

//Create a new PdfGrid.
PdfGrid pdfGrid = new PdfGrid();

//Adding tag to PDF grid.
pdfGrid.PdfTag = element;

//Add three columns.
pdfGrid.Columns.Add(3);

//Add header.
pdfGrid.Headers.Add(1);

PdfGridRow pdfGridHeader = pdfGrid.Headers[0];

pdfGridHeader.Style.Font = new PdfStandardFont(PdfFontFamily.Helvetica, 12, PdfFontStyle.Bold);

pdfGridHeader.Style.TextBrush = PdfBrushes.Brown;

//Adding tag for each row with tag type TR
pdfGridHeader.PdfTag = new PdfStructureElement(PdfTagType.TableRow);

pdfGridHeader.Cells[0].Value = "Employee ID";

//Adding tag for header cell with tag type TH
pdfGridHeader.Cells[0].PdfTag = new PdfStructureElement(PdfTagType.TableHeader);

pdfGridHeader.Cells[1].Value = "Employee Name";

//Adding tag for header cell with tag type TH
pdfGridHeader.Cells[1].PdfTag = new PdfStructureElement(PdfTagType.TableHeader);

pdfGridHeader.Cells[2].Value = "Salary";

//Adding tag for header cell with tag type TH
pdfGridHeader.Cells[2].PdfTag = new PdfStructureElement(PdfTagType.TableHeader);

//Add rows.
PdfGridRow pdfGridRow = pdfGrid.Rows.Add();

pdfGridRow.PdfTag = new PdfStructureElement(PdfTagType.TableRow);

pdfGridRow.Cells[0].Value = "E01";

pdfGridRow.Cells[1].Value = "Clay";

pdfGridRow.Cells[2].Value = "$10,000";

//Adding tag for each cell with tag type TD
pdfGridRow.Cells[0].PdfTag = new PdfStructureElement(PdfTagType.TableDataCell);

pdfGridRow.Cells[1].PdfTag = new PdfStructureElement(PdfTagType.TableDataCell);

pdfGridRow.Cells[2].PdfTag = new PdfStructureElement(PdfTagType.TableDataCell);

//Draw the PdfGrid.
pdfGrid.Draw(pdfPage, PointF.Empty);

//save the document and dispose it
pdfDocument.Save("Output.pdf");

pdfDocument.Close(true);

{% endhighlight %}
{% highlight vb.net %}

'Creates a new PDF document.
Dim pdfDocument As PdfDocument = New PdfDocument()

pdfDocument.DocumentInformation.Title = "Table"

'Adds new page
Dim pdfPage As PdfPage = pdfDocument.Pages.Add()

'Initialize the new structure element with tag type table
Dim element As PdfStructureElement = New PdfStructureElement(PdfTagType.Table)

'Create a new PdfGrid.
Dim pdfGrid As PdfGrid = New PdfGrid()

'Adding tag to PDF grid.
pdfGrid.PdfTag = element

'Add three columns.
pdfGrid.Columns.Add(3)

'Add header.
pdfGrid.Headers.Add(1)

Dim pdfGridHeader As PdfGridRow = pdfGrid.Headers(0)

pdfGridHeader.Style.Font = New PdfStandardFont(PdfFontFamily.Helvetica, 12, PdfFontStyle.Bold)

pdfGridHeader.Style.TextBrush = PdfBrushes.Brown

'Adding tag for each row with tag type TR
pdfGridHeader.PdfTag = New PdfStructureElement(PdfTagType.TableRow)

pdfGridHeader.Cells(0).Value = "Employee ID"

'Adding tag for header cell with tag type TH
pdfGridHeader.Cells(0).PdfTag = New PdfStructureElement(PdfTagType.TableHeader)

pdfGridHeader.Cells(1).Value = "Employee Name"

'Adding tag for header cell with tag type TH
pdfGridHeader.Cells(1).PdfTag = New PdfStructureElement(PdfTagType.TableHeader)

pdfGridHeader.Cells(2).Value = "Salary"

'Adding tag for header cell with tag type TH
pdfGridHeader.Cells(2).PdfTag = New PdfStructureElement(PdfTagType.TableHeader)

'Add rows.
Dim pdfGridRow As PdfGridRow = pdfGrid.Rows.Add()

pdfGridRow.PdfTag = New PdfStructureElement(PdfTagType.TableRow)

pdfGridRow.Cells(0).Value = "E01"

pdfGridRow.Cells(1).Value = "Clay"

pdfGridRow.Cells(2).Value = "$10,000"

'Adding tag for each cell with tag type TD
pdfGridRow.Cells(0).PdfTag = New PdfStructureElement(PdfTagType.TableDataCell)

pdfGridRow.Cells(1).PdfTag = New PdfStructureElement(PdfTagType.TableDataCell)

pdfGridRow.Cells(2).PdfTag = New PdfStructureElement(PdfTagType.TableDataCell)

'Draw the PdfGrid.
pdfGrid.Draw(pdfPage, PointF.Empty)

'save the document and dispose it
pdfDocument.Save("Output.pdf")

pdfDocument.Close(True)

{% endhighlight %}
{% endtabs %}

## Adding tag to List Element

You can add the tags to list element in PDF document by using tag type ```PdfTagType.List``` available in the class ```PdfStructureElement```. 

The following code example illustrates how to add tag support for List element.

{% tabs %}
{% highlight c# %}

//Create a new PDF document
PdfDocument document = new PdfDocument();

//Sets document title
document.DocumentInformation.Title = "List";

//Add a new page to the document.
PdfPage page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

SizeF size = page.Graphics.ClientSize;

//Create font
PdfFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 10, PdfFontStyle.Italic);

graphics.DrawString("List:", new PdfStandardFont(PdfFontFamily.Helvetica, 12, PdfFontStyle.Bold), PdfBrushes.Blue, new Point(10, 0));

string[] products = { "Tools", "Grid", "Chart", "Edit", "Diagram", "XlsIO", "Grouping", "Calculate", "PDF", "HTMLUI", "DocIO" };

//Create string format
PdfStringFormat format = new PdfStringFormat();

format.LineSpacing = 10f;

//Initialize new structure element with tag type List.
PdfStructureElement listElement = new PdfStructureElement(PdfTagType.List);

//Create Ordered list
PdfOrderedList pdfList = new PdfOrderedList();

//Adding tag for list element
pdfList.PdfTag = listElement;

pdfList.Marker.Brush = PdfBrushes.Black;

pdfList.Indent = 20;

//Set format for sub list
pdfList.Font = font;

pdfList.StringFormat = format;

for (int i = 0; i < products.Length; i++)
{
pdfList.Items.Add(string.Concat("Essential ", products[i]));

//Adding tag for the list item
pdfList.Items[i].PdfTag = new PdfStructureElement(PdfTagType.ListItem);
}

//Draw the list
pdfList.Draw(page, new RectangleF(0, 20, size.Width, size.Height));

// Save and close the document.
document.Save("Output.pdf");

document.Close(true);

{% endhighlight %}
{% highlight vb.net %}

'Create a new PDF document
Dim document As PdfDocument = New PdfDocument()

'Sets document title
document.DocumentInformation.Title = "List"

'Add a new page to the document.
Dim page As PdfPage = document.Pages.Add()

Dim graphics As PdfGraphics = page.Graphics

Dim size As SizeF = page.Graphics.ClientSize

'Create font
Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.TimesRoman, 10, PdfFontStyle.Italic)

graphics.DrawString("List:", New PdfStandardFont(PdfFontFamily.Helvetica, 12, PdfFontStyle.Bold), PdfBrushes.Blue, New Point(10, 0))

Dim products() As String = {"Tools", "Grid", "Chart", "Edit", "Diagram", "XlsIO", "Grouping", "Calculate", "PDF", "HTMLUI", "DocIO"}


'Create string format
Dim format As PdfStringFormat = New PdfStringFormat()

format.LineSpacing = 10.0F

'Initialize new structure element with tag type List.
Dim listElement As PdfStructureElement = New PdfStructureElement(PdfTagType.List)

'Create Ordered list
Dim pdfList As PdfOrderedList = New PdfOrderedList()

'Adding tag for list element
pdfList.PdfTag = listElement

pdfList.Marker.Brush = PdfBrushes.Black

pdfList.Indent = 20

'Set format for sub list
pdfList.Font = font

pdfList.StringFormat = format


For i As Integer = 0 To products.Length - 1

pdfList.Items.Add(String.Concat("Essential ", products(i)))

'Adding tag for the list item
pdfList.Items(i).PdfTag = New PdfStructureElement(PdfTagType.ListItem)

Next

'Draw the list
pdfList.Draw(page, New RectangleF(0, 20, size.Width, size.Height))

' Save and close the document.
document.Save("Output.pdf")

document.Close(True)

{% endhighlight %}
{% endtabs %}

## Marking PDF content as an Artifact

Artifacts in PDF document can be graphic objects or other markings that are not part of the authored content and would include such things as: headers, footers, page numbers, watermarks, cut marks, color bars, background images, lines separating content, or decorative images. 
You can add artifact tag to PDF element by using ```PdfArtifact``` class. We can specify the artifact type by using ```PdfArtifactType``` property available in the ```PdfArtifact``` class.

The following code explains how to add tag for header and footers in PDF document.

{% tabs %}
{% highlight c# %}

//Creates new PDF document
PdfDocument pdfDocument = new PdfDocument();

//Add a page to the PDF document
PdfPage pdfPage = pdfDocument.Pages.Add();

pdfDocument.DocumentInformation.Title = "HeaderFooter";

//Creating artifact type for the header
PdfArtifact headerArtifact = new PdfArtifact(PdfArtifactType.Pagination, new RectangleF(30, 40, 100, 100), new PdfAttached(PdfEdge.Top), PdfArtifactSubType.Header);

//Create a header and draw the image.
RectangleF bounds = new RectangleF(0, 0, pdfDocument.Pages[0].GetClientSize().Width, 50);

PdfPageTemplateElement header = new PdfPageTemplateElement(bounds);

//Adding artifact to the header
header.PdfTag = headerArtifact;

PdfImage image = new PdfBitmap("syncfusion.jpg");

//Draw the image in the header.            
header.Graphics.DrawImage(image, new PointF(200, 0), new SizeF(100, 50));

//Add the header at the top.
pdfDocument.Template.Top = header;

//Creating artifact type for the footer
PdfArtifact footerArtifact = new PdfArtifact(PdfArtifactType.Pagination, new PdfAttached(PdfEdge.Bottom), PdfArtifactSubType.Footer);

//Create a Page template that can be used as footer.
PdfPageTemplateElement footer = new PdfPageTemplateElement(bounds);

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 7);

PdfBrush brush = new PdfSolidBrush(Color.Black);

//Create page number field.
PdfPageNumberField pageNumber = new PdfPageNumberField(font, brush);

//Create page count field.
PdfPageCountField count = new PdfPageCountField(font, brush);

//Add the fields in composite fields.
PdfCompositeField compositeField = new PdfCompositeField(font, brush, "Page {0} of {1}", pageNumber, count);

compositeField.Bounds = footer.Bounds;

//Adding artifact type to the footer.
compositeField.PdfTag = footerArtifact;

//Draw the composite field in footer.
compositeField.Draw(footer.Graphics, new PointF(470, 40));

//Add the footer template at the bottom.
pdfDocument.Template.Bottom = footer;

//Save the document and dispose it
pdfDocument.Save("HeaderFooter.pdf");

pdfDocument.Close(true);

{% endhighlight %}
{% highlight vb.net %}

'Creates new PDF document
Dim pdfDocument As PdfDocument = New PdfDocument()

'Add a page to the PDF document
Dim pdfPage As PdfPage = pdfDocument.Pages.Add()

pdfDocument.DocumentInformation.Title = "HeaderFooter"

'Creating artifact type for the header
Dim headerArtifact As PdfArtifact = New PdfArtifact(PdfArtifactType.Pagination, New RectangleF(30, 40, 100, 100), New PdfAttached(PdfEdge.Top), PdfArtifactSubType.Header)

'Create a header and draw the image.
Dim bounds As RectangleF = New RectangleF(0, 0, pdfDocument.Pages(0).GetClientSize().Width, 50)

Dim header As PdfPageTemplateElement = New PdfPageTemplateElement(bounds)

'Adding artifact to the header
header.PdfTag = headerArtifact

Dim image As PdfImage = New PdfBitmap("syncfusion.jpg")

'Draw the image in the header.            
header.Graphics.DrawImage(image, New PointF(200, 0), New SizeF(100, 50))

'Add the header at the top.
pdfDocument.Template.Top = header

'Creating artifact type for the footer
Dim footerArtifact As PdfArtifact = New PdfArtifact(PdfArtifactType.Pagination, New PdfAttached(PdfEdge.Bottom), PdfArtifactSubType.Footer)

'Create a Page template that can be used as footer.
Dim footer As PdfPageTemplateElement = New PdfPageTemplateElement(bounds)

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 7)

Dim brush As PdfBrush = New PdfSolidBrush(Color.Black)

'Create page number field.
Dim pageNumber As PdfPageNumberField = New PdfPageNumberField(font, brush)

'Create page count field.
Dim count As PdfPageCountField = New PdfPageCountField(font, brush)

'Add the fields in composite fields.
Dim compositeField As PdfCompositeField = New PdfCompositeField(font, brush, "Page {0} of {1}", pageNumber, count)

compositeField.Bounds = footer.Bounds

'Adding artifact type to the footer.
compositeField.PdfTag = footerArtifact

'Draw the composite field in footer.
compositeField.Draw(footer.Graphics, New PointF(470, 40))

'Add the footer template at the bottom.
pdfDocument.Template.Bottom = footer

'Save the document and dispose it
pdfDocument.Save("HeaderFooter.pdf")

pdfDocument.Close(True)

{% endhighlight %}
{% endtabs %}

## Tag Reading Order

Basically, the element which draws first takes precedence over the tag reading order. You can re-order the tagged elements in document using order property. 

The following code example illustrates how to order the tagged elements in PDF document.

{% tabs %}
{% highlight c# %}

//Create a new PDF document
PdfDocument document = new PdfDocument();

//Sets document title
document.DocumentInformation.Title = "Order";

//Add a new page to the document.
PdfPage page = document.Pages.Add();

//Initialize the structure element with tag type paragraph.
PdfStructureElement structureElement = new PdfStructureElement(PdfTagType.Paragraph);

//Order the tag in third position.
structureElement.Order = 3;

PdfTextElement element = new PdfTextElement("This is paragraph ONE.", new PdfStandardFont(PdfFontFamily.Helvetica, 12));

element.Brush = new PdfSolidBrush(new PdfColor(89, 89, 93));

//Adding tag to the text element
element.PdfTag = structureElement;

element.Draw(page, new RectangleF(0, 0, page.Graphics.ClientSize.Width / 2, 200));

//Initialize the structure element with tag type paragraph.
PdfStructureElement paraStruct1 = new PdfStructureElement(PdfTagType.Paragraph);

//Order the tag in first position
paraStruct1.Order = 1;

//Creates new text element
PdfTextElement element1 = new PdfTextElement("This is paragraph TWO.", new PdfStandardFont(PdfFontFamily.Helvetica, 12));

element1.Brush = new PdfSolidBrush(new PdfColor(89, 89, 93));

//Adding tag to the text element
element1.PdfTag = paraStruct1;

element1.Draw(page, new RectangleF(0, 50, page.Graphics.ClientSize.Width / 2, 200));

//Initialize the structure element with tag type paragraph.
PdfStructureElement paraStruct2 = new PdfStructureElement(PdfTagType.Paragraph);

//Order the tag in second position
paraStruct2.Order = 2;

//Creates new text element
PdfTextElement element2 = new PdfTextElement("This is paragraph THREE.", new PdfStandardFont(PdfFontFamily.Helvetica, 12));

element2.Brush = new PdfSolidBrush(new PdfColor(89, 89, 93));

//Adding tag to the text element
element2.PdfTag = paraStruct2;

element2.Draw(page.Graphics, new PointF(0, 100));

//Save the document and dispose it.
document.Save("Output.pdf");

document.Close(true);

{% endhighlight %}
{% highlight vb.net %}

'Create a new PDF document
Dim document As PdfDocument = New PdfDocument()

'Sets document title
document.DocumentInformation.Title = "Order"

'Add a new page to the document.
Dim page As PdfPage = document.Pages.Add()

'Initialize the structure element with tag type paragraph.
Dim structureElement As PdfStructureElement = New PdfStructureElement(PdfTagType.Paragraph)

'Order the tag in third position.
structureElement.Order = 3

Dim element As PdfTextElement = New PdfTextElement("This is paragraph ONE.", New PdfStandardFont(PdfFontFamily.Helvetica, 12))

element.Brush = New PdfSolidBrush(New PdfColor(89, 89, 93))

'Adding tag to the text element
element.PdfTag = structureElement

element.Draw(page, New RectangleF(0, 0, page.Graphics.ClientSize.Width / 2, 200))

'Initialize the structure element with tag type paragraph.
Dim paraStruct1 As PdfStructureElement = New PdfStructureElement(PdfTagType.Paragraph)

'Order the tag in first position
paraStruct1.Order = 1

'Creates new text element
Dim element1 As PdfTextElement = New PdfTextElement("This is paragraph TWO.", New PdfStandardFont(PdfFontFamily.Helvetica, 12))

element1.Brush = New PdfSolidBrush(New PdfColor(89, 89, 93))

'Adding tag to the text element
element1.PdfTag = paraStruct1

element1.Draw(page, New RectangleF(0, 50, page.Graphics.ClientSize.Width / 2, 200))

'Initialize the structure element with tag type paragraph.
Dim paraStruct2 As PdfStructureElement = New PdfStructureElement(PdfTagType.Paragraph)

'Order the tag in second position
paraStruct2.Order = 2

'Creates new text element
Dim element2 As PdfTextElement = New PdfTextElement("This is paragraph THREE.", New PdfStandardFont(PdfFontFamily.Helvetica, 12))

element2.Brush = New PdfSolidBrush(New PdfColor(89, 89, 93))

'Adding tag to the text element
element2.PdfTag = paraStruct2

element2.Draw(page.Graphics, New PointF(0, 100))

'Save the document and dispose it.
document.Save("Output.pdf")

document.Close(True)

{% endhighlight %}
{% endtabs %}

## Auto Tagging a new document

When the auto-tag feature is enabled all the elements in the document is tagged with appropriate tag type i.e. Paragraph, Figure, Annotation etc. 

The following code example explains how to auto-tag the elements in PDF document.

N> While enabling the auto-tag feature, it will never add alternate texts/descriptions for figures, images and other properties related to tag

{% tabs %}
{% highlight c# %}

//Creates new PDF document
PdfDocument document = new PdfDocument();

//Set true to auto tag all elements in document
document.AutoTag = true;

document.DocumentInformation.Title = "AutoTag";

// Add a new page to the document.
PdfPage page = document.Pages.Add();

//Creates new text element
PdfTextElement element = new PdfTextElement("This is paragraph ONE.", new PdfStandardFont(PdfFontFamily.Helvetica, 12));

element.Brush = new PdfSolidBrush(new PdfColor(89, 89, 93));

element.Draw(page, new RectangleF(0, 0, page.Graphics.ClientSize.Width / 2, 200));

//Creates new text element
PdfTextElement element1 = new PdfTextElement("This is paragraph TWO.", new PdfStandardFont(PdfFontFamily.Helvetica, 12));

element1.Brush = new PdfSolidBrush(new PdfColor(89, 89, 93));

element1.Draw(page, new RectangleF(0, 50, page.Graphics.ClientSize.Width / 2, 200));

//Creates new text element
PdfTextElement element2 = new PdfTextElement("This is paragraph THREE.", new PdfStandardFont(PdfFontFamily.Helvetica, 12));

element2.Brush = new PdfSolidBrush(new PdfColor(89, 89, 93));

element2.Draw(page.Graphics, new PointF(0, 100));

//Save the document and dispose it.
document.Save("AutoTag.pdf");

document.Close(true);

{% endhighlight %}
{% highlight vb.net %}

'Creates new PDF document
Dim document As PdfDocument = New PdfDocument()

'Set true to auto tag all elements in document
document.AutoTag = True

document.DocumentInformation.Title = "AutoTag"

'Add a new page to the document.
Dim page As PdfPage = document.Pages.Add()

'Creates new text element
Dim element As PdfTextElement = New PdfTextElement("This is paragraph ONE.", New PdfStandardFont(PdfFontFamily.Helvetica, 12))

element.Brush = New PdfSolidBrush(New PdfColor(89, 89, 93))

element.Draw(page, New RectangleF(0, 0, page.Graphics.ClientSize.Width / 2, 200))

'Creates new text element
Dim element1 As PdfTextElement = New PdfTextElement("This is paragraph TWO.", New PdfStandardFont(PdfFontFamily.Helvetica, 12))

element1.Brush = New PdfSolidBrush(New PdfColor(89, 89, 93))

element1.Draw(page, New RectangleF(0, 50, page.Graphics.ClientSize.Width / 2, 200))

'Creates new text element
Dim element2 As PdfTextElement = New PdfTextElement("This is paragraph THREE.", New PdfStandardFont(PdfFontFamily.Helvetica, 12))

element2.Brush = New PdfSolidBrush(New PdfColor(89, 89, 93))

element2.Draw(page.Graphics, New PointF(0, 100))

'Save the document and dispose it.
document.Save("AutoTag.pdf")

document.Close(True)

{% endhighlight %}
{% endtabs %}

N> Once the document is auto tagged, and if any element tagged manually then manually tagged element takes the precedence.

## How to pass accessibility full check

To pass the full check accessibility, you need to follow below conventions while tagging the document.

1. PDF document “Title” need to be mentioned in the document properties.
2. Make sure images in the document either has alternate text or marked as artifact.
3. Bookmarks need to be included, for tagged PDF with more than 21 pages.
4. All the form fields require text description (Tool tip).
5. All tables in a document should have a header.
6. Tables must contain same number of columns in each row.
7. A List element must contain list Item element(LI), and list Item element can only contain label (Lbl) or body elements(LBody).

## Tagged PDF support for converting HTML to PDF

Essential PDF provides the support to convert HTML to TaggedPDF by using MSHTML rendering library.

Tagged PDF is a stylized use of PDF that builds the logical structure Framework. It defines a set of standard structure types and attributes that allow page content (text, graphics, and images) to be extracted and reused. The contents are accessible to users with visual impairments.

To convert HTML to Tagged PDF, you can use ConvertToTaggedPDF method in HtmlConverter class.

The following code illustrates how to convert HTML to TaggedPDF:

{% tabs %}
{% highlight c# %}

//Creates a new PdfDocument.

PdfDocument document = new PdfDocument();

//Creates a new instance of HtmlConverter class.

using (HtmlConverter html = new HtmlConverter())

{

//Enable JavaScript

html.EnableJavaScript = true;

//Converts to Tagged PDF.

html.ConvertToTaggedPDF(document,"http://www.google.com");

}

//Saves and closes the document.

document.Save("Sample.pdf");

document.Close(true);

{% endhighlight %}
{% highlight vb.net %}

'Creates a new PdfDocument.

Dim document As New PdfDocument()

'Creates a new instance of HtmlConverter class.

Using html As New HtmlConverter()

'Enables JavaScript

html.EnableJavaScript = True

'Converts to Tagged PDF.

html.ConvertToTaggedPDF(document, "http://www.google.com")

End Using

'Saves and closes the document.

document.Save("Sample.pdf")

document.Close(True)


{% endhighlight %}
{% endtabs %}

N> Hyperlinks are not supported in tagged PDF


