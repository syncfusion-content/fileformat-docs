---
title: Working with Word document
description: Learn about combining multiple Word documents as one, printing Word document, applying styles, document properties, & iterating through DOM elements
platform: file-formats
control: DocIO
documentation: UG
---
# Working with Word document

## Iterating through document elements

The following are the important points to be remembered while iterating the document elements

* Document consists of one or more sections.
* Section contains the contents present in Headers, Footers and main document through the instances of `WTextBody`.
* `WTextBody` contains two type of elements – either paragraph or table

The following code example shows how to iterate throughout the Word document and remove the paragraph with a particular style.

{% tabs %} 

{% highlight c# %}


using Syncfusion.DocIO.DLS;

namespace RemoveParagraphs

{

class Program

{

static void Main(string[] args)

{

//Opens an existing document from file system through constructor of WordDocument class

WordDocument document = new WordDocument(@"TestDocument.docx");

//Processes the body contents for each section in the Word document

foreach (WSection section in document.Sections)

{

//Accesses the Body of section where all the contents in document are apart

WTextBody sectionBody = section.Body;

IterateTextBody(sectionBody);

WHeadersFooters headersFooters = section.HeadersFooters;

//Consider that OddHeader and OddFooter are applied to this document

//Iterates through the TextBody of OddHeader and OddFooter

IterateTextBody(headersFooters.OddHeader);

IterateTextBody(headersFooters.OddFooter);

}

//Saves and closes the document instance

document.Save("Result.docx");

document.Close();

System.Diagnostics.Process.Start("Result.docx");

}

private static void IterateTextBody(WTextBody textBody)

{

//Iterates through each of the child items of WTextBody

for(int i = 0; i < textBody.ChildEntities.Count; i++)

{

//IEntity is the basic unit in DocIO DOM. 

//Accesses the body items (should be either paragraph or table) as IEntity

IEntity bodyItemEntity = textBody.ChildEntities[i];

//A Text body has 2 types of elements - Paragraph and Table

//Decides the element type by using EntityType

switch (bodyItemEntity.EntityType)

{

case EntityType.Paragraph:

WParagraph paragraph = bodyItemEntity as WParagraph;

//Checks for particular style name and removes the paragraph from DOM

if (paragraph.StyleName == "MyStyle")

{

int index = textBody.ChildEntities.IndexOf(paragraph);

textBody.ChildEntities.RemoveAt(index);

}

break;

case EntityType.Table:

//Table is a collection of rows and cells

//Iterates through table's DOM

IterateTable(bodyItemEntity as WTable);

break;

}

}

}

private static void IterateTable(WTable table)

{

//Iterates the row collection in a table

foreach (WTableRow row in table.Rows)

{

//Iterates the cell collection in a table row

foreach (WTableCell cell in row.Cells)

{

//Table cell is derived from (also a) TextBody

//Reusing the code meant for iterating TextBody

IterateTextBody(cell);

}

}

}

}

}

{% endhighlight %}

{% highlight vb.net %}

Imports Syncfusion.DocIO.DLS

Namespace RemoveParagraphs

Class Program

Private Shared Sub Main(args As String())

'Opens an existing document from file system through constructor of WordDocument class

Dim document As New WordDocument("TestDocument.docx")

'Processes the body contents for each section in the Word document

For Each section As WSection In document.Sections

'Accesses the Body of section where all the contents in document are apart

Dim sectionBody As WTextBody = section.Body

IterateTextBody(sectionBody)

Dim headersFooters As WHeadersFooters = section.HeadersFooters

'Consider that OddHeader and OddFooter are applied to this document

'Iterates through the text body of OddHeader and OddFooter

IterateTextBody(headersFooters.OddHeader)

IterateTextBody(headersFooters.OddFooter)

Next

'Saves and closes the document instance

document.Save("Result.docx")

document.Close()

System.Diagnostics.Process.Start("Result.docx")

End Sub

Private Shared Sub IterateTextBody(textBody As WTextBody)

'Iterates through the each of the child items of WTextBody

For i As Integer = 0 To textBody.ChildEntities.Count - 1

'IEntity is the basic unit in DocIO DOM. 

'Accesses the body items (should be either paragraph or table) as IEntity

Dim bodyItemEntity As IEntity = textBody.ChildEntities(i)

'A Text body has 2 types of elements - Paragraph and Table

'decide the element type using EntityType

Select Case bodyItemEntity.EntityType

Case EntityType.Paragraph

Dim paragraph As WParagraph = TryCast(bodyItemEntity, WParagraph)

'Checks for a particular style name and removes the paragraph from DOM

If paragraph.StyleName = "MyStyle" Then

Dim index As Integer = textBody.ChildEntities.IndexOf(paragraph)

textBody.ChildEntities.RemoveAt(index)

End If

Exit Select

Case EntityType.Table

'Table is a collection of rows and cells

'Iterates through table's DOM

IterateTable(TryCast(bodyItemEntity, WTable))

Exit Select

End Select

Next

End Sub

Private Shared Sub IterateTable(table As WTable)

'Iterates the row collection in a table

For Each row As WTableRow In table.Rows

'Iterates the cell collection in a table row

For Each cell As WTableCell In row.Cells

'Table cell is derived from (also a) TextBody

'Reusing the code meant for iterating TextBody

IterateTextBody(cell)

Next

Next

End Sub

End Class

End Namespace

{% endhighlight %}

{% endtabs %}  

The following code example shows how to iterate throughout the paragraph and modify the hyperlink (Hyperlink)Uri and specific text (WTextRange)with another.

{% tabs %}  

{% highlight c# %}

using Syncfusion.DocIO.DLS;

using Syncfusion.DocIO;

namespace UpdateText

{

class Program

{

static void Main(string[] args)

{

//Opens an existing document from file system through constructor of WordDocument class

WordDocument document = new WordDocument(@"TestDocument.docx");

//Processes the body contents for each section in the Word document

foreach (WSection section in document.Sections)

{

Accesses the Body of section where all the contents in document are apart

WTextBody sectionBody = section.Body;

IterateTextBody(sectionBody);

WHeadersFooters headersFooters = section.HeadersFooters;

//consider that OddHeader & OddFooter are applied to this document

//Iterates through the TextBody of OddHeader and OddFooter

IterateTextBody(headersFooters.OddHeader);

IterateTextBody(headersFooters.OddFooter);

}

//Saves and closes the document instance

document.Save("Result.docx");

document.Close();

System.Diagnostics.Process.Start("Result.docx");

}

private static void IterateTextBody(WTextBody textBody)

{

//Iterates through each of the child items of WTextBody

for (int i = 0; i < textBody.ChildEntities.Count; i++)

{

//IEntity is the basic unit in DocIO DOM. 

//Accesses the body items (should be either paragraph or table) as IEntity

IEntity bodyItemEntity = textBody.ChildEntities[i];

//A Text body has 2 types of elements - Paragraph and Table

//Decides the element type by using EntityType

switch (bodyItemEntity.EntityType)

{

case EntityType.Paragraph:

WParagraph paragraph = bodyItemEntity as WParagraph;

//Processes the paragraph contents

//Iterates through the paragraph's DOM

IterateParagraph(paragraph);

break;

case EntityType.Table:

//Table is a collection of rows and cells

//Iterates through table's DOM

IterateTable(bodyItemEntity as WTable);

break;

}

}

}

private static void IterateTable(WTable table)

{

//Iterates the row collection in a table

foreach (WTableRow row in table.Rows)

{

//Iterates the cell collection in a table row

foreach (WTableCell cell in row.Cells)

{

//Table cell is derived from (also a) TextBody

//Reusing the code meant for iterating TextBody

IterateTextBody(cell);

}

}

}

private static void IterateParagraph(WParagraph paragraph)

{

for (int i = 0; i < paragraph.ChildEntities.Count; i++)

{

Entity entity = paragraph.ChildEntities[i];

//A paragraph can have child elements such as text, image, hyperlink, symbols, etc.,

//Decides the element type by using EntityType

switch (entity.EntityType)

{

case EntityType.TextRange:

//Replaces the text with another

WTextRange textRange = entity as WTextRange;

if (textRange.Text == "Andrew")

{

(entity as WTextRange).Text = "Fuller";

}

break;

case EntityType.Field:

WField field = entity as WField;

if (field.FieldType == FieldType.FieldHyperlink)

{

//Creates hyperlink instance from field to manipulate the hyperlink

Hyperlink hyperlink = new Hyperlink(entity as WField);

//Modifies the Uri of the hyperlink

if (hyperlink.Type == HyperlinkType.WebLink && hyperlink.TextToDisplay == "HTML")

{

hyperlink.Uri = "http://www.w3schools.com/";

}

}

break;

}

}

}

}

}

{% endhighlight %}

{% highlight vb.net %}

Imports Syncfusion.DocIO.DLS

Imports Syncfusion.DocIO

Namespace UpdateText

Class Program

Private Shared Sub Main(args As String())

Dim document As New WordDocument("TestDocument.docx")

'Processes the body contents for each section in the Word document

For Each section As WSection In document.Sections

'Accesses the Body of section where all the contents in document are apart

Dim sectionBody As WTextBody = section.Body

IterateTextBody(sectionBody)

Dim headersFooters As WHeadersFooters = section.HeadersFooters

'Considers that OddHeader and OddFooter are applied to this document

'Iterates through the TextBody of OddHeader and OddFooter

IterateTextBody(headersFooters.OddHeader)

IterateTextBody(headersFooters.OddFooter)

Next

'Saves and closes the document instance

document.Save("Result.docx")

document.Close()

System.Diagnostics.Process.Start("Result.docx")

End Sub

Private Shared Sub IterateTextBody(textBody As WTextBody)

'Iterates through each of the child items of WTextBody

For i As Integer = 0 To textBody.ChildEntities.Count - 1

'IEntity is the basic unit in DocIO DOM. 

'Accesses the body items (should be either paragraph or table) as IEntity

Dim bodyItemEntity As IEntity = textBody.ChildEntities(i)

'A Text body has 2 types of elements - Paragraph and Table

'Decides the element type by using EntityType

Select Case bodyItemEntity.EntityType

Case EntityType.Paragraph

Dim paragraph As WParagraph = TryCast(bodyItemEntity, WParagraph)

'Processes the paragraph contents

'Iterates through the paragraph's DOM

IterateParagraph(paragraph)

Exit Select

Case EntityType.Table

'Table is a collection of rows and cells

'Iterates through table's DOM

IterateTable(TryCast(bodyItemEntity, WTable))

Exit Select

End Select

Next

End Sub

Private Shared Sub IterateTable(table As WTable)

'Iterates the row collection in a table

For Each row As WTableRow In table.Rows

'Iterates the cell collection in a table row

For Each cell As WTableCell In row.Cells

'Table cell is derived from (also a) TextBody

'Reusing the code meant for iterating TextBody

IterateTextBody(cell)

Next

Next

End Sub

Private Shared Sub IterateParagraph(paragraph As WParagraph)

For i As Integer = 0 To paragraph.ChildEntities.Count - 1

Dim entity As Entity = paragraph.ChildEntities(i)

'A Paragraph has child elements such as text, image, hyperlink, symbols, etc.,

'Decides the element type by using EntityType

Select Case entity.EntityType

Case EntityType.TextRange

'Replaces the text with another

Dim textRange As WTextRange = TryCast(entity, WTextRange)

If textRange.Text = "Andrew" Then

TryCast(entity, WTextRange).Text = "Fuller"

End If

Exit Select

Case EntityType.Field

Dim field As WField = TryCast(entity, WField)

If field.FieldType = FieldType.FieldHyperlink Then

'Creates Hyperlink instance from field to manipulate the Hyperlink

Dim hyperlink As New Hyperlink(TryCast(entity, WField))

'Modifies the Uri of the hyperlink

If hyperlink.Type = HyperlinkType.WebLink AndAlso hyperlink.TextToDisplay = "HTML" Then

hyperlink.Uri = "http://www.w3schools.com/"

End If

End If

Exit Select

End Select

Next

End Sub

End Class

End Namespace

{% endhighlight %}

{% endtabs %}  

## Cloning a Word document

You can create a deep copy of a Word document by using `Clone` method of `WordDocument` class. You can read the template document from file system or stream and create multiple document copies by cloning it. This improves the performance of document generation, as there is no need to read the Word document each time.

{% tabs %} 

{% highlight c# %}

//Opens an existing document 

WordDocument inputTemplateDoc = new WordDocument(fileName);

//Creates a clone of Input Template 

WordDocument clonedDocument = inputTemplateDoc.Clone();

//Saves and closes the cloned document instance

clonedDocument.Save("ClonedDocument.docx");

clonedDocument.Close();

//Closes the input template document instance

sourceDocument.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing document 

Dim inputTemplateDoc As New WordDocument(fileName)

'Creates a clone of Input Template 

Dim clonedDocument As WordDocument = inputTemplateDoc.Clone()

'Saves and closes the cloned document instance

clonedDocument.Save("ClonedDocument.docx")

clonedDocument.Close()

'Closes the input template document instance

sourceDocument.Close()

{% endhighlight %}

{% endtabs %}  
 
You can also create a deep copy of document elements such as sections, paragraphs, Tables, Text, Image, OleObject, Shapes, TextBoxes and etc., The following code example illustrates how to clone the section and save each cloned section as a Word document. 

{% tabs %} 

{% highlight c# %}

//Opens a source document

WordDocument sourceDocument = new WordDocument("SourceDocument.docx");

//Processes the each section in the Word document

for (int i = 0; i < sourceDocument.Sections.Count;i++)

{

//Creates new WordDocument instance to add cloned section

WordDocument destinationDocument = new WordDocument();

//Clones and adds source document sections to the destination document

destinationDocument.Sections.Add(sourceDocument.Sections[i].Clone());

//Saves and closes the document instance

destinationDocument.Save("Section_" + i + ".docx");

destinationDocument.Close();

}

//Closes the source document instance

sourceDocument.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens a source document

Dim sourceDocument As New WordDocument("SourceDocument.docx")

'Processes the each section in the Word document

For i As Integer = 0 To sourceDocument.Sections.Count - 1

'Creates new WordDocument instance to add cloned section

Dim destinationDocument As New WordDocument()

'Clones and adds source document sections to the destination document

destinationDocument.Sections.Add(sourceDocument.Sections(i).Clone())

'Saves and closes the document instance

destinationDocument.Save("Section_" + i + ".docx")

destinationDocument.Close()

Next

'Closes the source document instance

sourceDocument.Close()

{% endhighlight %}

{% endtabs %}  
   
## Merging Word documents

You can merge multiple Word documents into single Word document by using DocIO’s capability of importing contents from one document to another. The imported contents are appended at the end of document.  The following code example illustrates how to import the contents from source document into destination document where the contents are appended. 

{% tabs %} 

{% highlight c# %}

//Opens the source document 

WordDocument sourceDocument = new WordDocument(sourceFileName);

//Opens the destination document 

WordDocument destinationDocument = new WordDocument(targetFileName);

//Imports the contents of source document at the end of destination document

destinationDocument.ImportContent(sourceDocument, ImportOptions.UseDestinationStyles);

//Saves the destination document

destinationDocument.Save(outputFileName, FormatType.Docx);

//closes the document instances

sourceDocument.Close();

destinationDocument.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens the source document 

Dim sourceDocument As New WordDocument(sourceFileName)

'Opens the destination document 

Dim destinationDocument As New WordDocument(targetFileName)

'Imports the contents of source document at the end of destination document

destinationDocument.ImportContent(sourceDocument, ImportOptions.UseDestinationStyles)

'Saves the destination document

destinationDocument.Save(outputFileName, FormatType.Docx)

'closes the document instances

sourceDocument.Close()

destinationDocument.Close()

{% endhighlight %} 

{% endtabs %}  

In the resultant document, the imported contents start from a new page followed by existing contents in a destination document. This is the default behavior.

When your requirement is to append the contents from the same page instead of starting from a new page, you need to set the break code of first section of Source document as NoBreak. The following code example illustrates the importing contents from the same page.

{% tabs %}  

{% highlight c# %}

//Opens the source document 

WordDocument sourceDocument = new WordDocument(sourceFileName);

//Opens the destination document 

WordDocument destinationDocument = new WordDocument(targetFileName);

//Sets the break-code of First section of source document as NoBreak to avoid imported from a new page

sourceDocument.Sections[0].BreakCode = SectionBreakCode.NoBreak; 

//Imports the contents of source document at the end of destination document

destinationDocument.ImportContent(sourceDocument, ImportOptions.UseDestinationStyles);

//Saves the destination document

destinationDocument.Save(outputFileName, FormatType.Docx);

//Closes the document instances

sourceDocument.Close();

destinationDocument.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens the source document 

Dim sourceDocument As New WordDocument(sourceFileName)

'Opens the destination document 

Dim destinationDocument As New WordDocument(targetFileName)

'Sets the break-code of first section of source document as NoBreak to avoid imported from a new page

sourceDocument.Sections(0).BreakCode = SectionBreakCode.NoBreak

'Imports the contents of source document at the end of destination document

destinationDocument.ImportContent(sourceDocument, ImportOptions.UseDestinationStyles)

'Saves the destination document

destinationDocument.Save(outputFileName, FormatType.Docx)

'Closes the document instances

sourceDocument.Close()

destinationDocument.Close()

{% endhighlight %}

{% endtabs %}  

## Printing a Word document

You can print a Word document by utilizing DocIO’s capability to convert the document into images and .NET framework’s [PrintDocument](https://msdn.microsoft.com/en-us/library/System.Drawing.Printing.PrintDocument(v=vs.110).aspx#) class

Initially you have to render the pages as images as shown below

{% tabs %}  

{% highlight c# %}

//Opens the Word document.

WordDocument document = new WordDocument((string)this.textBox.Tag);

//Renders the Word document as image.

Image[] images = document.RenderAsImages(ImageType.Metafile);

//Closes the Word Document.

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens the Word document.

Dim document As New WordDocument(DirectCast(Me.textBox.Tag, String))

'Renders the Word document as image.

Dim images As Image() = document.RenderAsImages(ImageType.Metafile)

'Closes the Word Document.

document.Close()

{% endhighlight %}

{% endtabs %}  

You can specify the printer settings and page settings through the [PrintDocument](https://msdn.microsoft.com/en-us/library/System.Drawing.Printing.PrintDocument(v=vs.110).aspx#) class. The [PrintDocument.PrintPage](https://msdn.microsoft.com/en-us/library/system.drawing.printing.printdocument.printpage%28v=vs.110%29.aspx#) event should be handled to layout the document for printing. 

The following code example demonstrates how to print the Word document pages that have been rendered as an image:

{% tabs %} 

{% highlight c# %}

int endPageIndex = images.Length;

//Creates new PrintDialog instance.

System.Windows.Forms.PrintDialog printDialog = new System.Windows.Forms.PrintDialog();

//Sets new PrintDocument instance to print dialog.

printDialog.Document = new PrintDocument();

//Enables the print current page option.

printDialog.AllowCurrentPage = true;

//Enables the print selected pages option.

printDialog.AllowSomePages = true;

//Sets the start and end page index

printDialog.PrinterSettings.FromPage = 1;

printDialog.PrinterSettings.ToPage = images.Length;

//Opens the print dialog box.

if (printDialog.ShowDialog() == System.Windows.Forms.DialogResult.OK)

{

//Checks whether the selected page range is valid.

if (printDialog.PrinterSettings.FromPage > 0 && printDialog.PrinterSettings.ToPage <= images.Length)

{

//Updates the start page of the document to print.

startPageIndex = printDialog.PrinterSettings.FromPage - 1;

//Updates the end page of the document to print.

endPageIndex = printDialog.PrinterSettings.ToPage;

//Hooks the PrintPage event to handle the drawing pages for printing.

printDialog.Document.PrintPage += new PrintPageEventHandler(PrintPageMethod);

//Print the document.

printDialog.Document.Print();

}

}

private void PrintPageMethod (object sender, PrintPageEventArgs e)

{

//Gets the print start page width.

int currentPageWidth = images[startPageIndex].Width;

//Gets the print start page height.

int currentPageHeight = images[startPageIndex].Height;

//Gets the visible bounds width for print.

int visibleClipBoundsWidth = (int)e.Graphics.VisibleClipBounds.Width;

//Gets the visible bounds height for print.

int visibleClipBoundsHeight = (int)e.Graphics.VisibleClipBounds.Height;

//Checks whether the page layout is landscape or portrait.

if (currentPageWidth > currentPageHeight)

{

//Translates the position.

e.Graphics.TranslateTransform(0, visibleClipBoundsHeight);

//Rotates the object at 270 degrees

e.Graphics.RotateTransform(270.0f);

//Draws the current page image.

e.Graphics.DrawImage(images[startPageIndex], new System.Drawing.Rectangle(0, 0, currentPageWidth, currentPageHeight));

}

else

{

//Draws the current page image.

e.Graphics.DrawImage(images[startPageIndex], new System.Drawing.Rectangle(0, 0, visibleClipBoundsWidth, visibleClipBoundsHeight));

}

//Disposes the current page image after drawing.

images[startPageIndex].Dispose();

//Increments the start page index.

startPageIndex++;

//Updates whether the document contains some more pages to print.

if (startPageIndex < endPageIndex)

e.HasMorePages = true;

else

startPageIndex = 0;

}

{% endhighlight %}

{% highlight vb.net %}

Dim endPageIndex As Integer = images.Length

'Creates new PrintDialog instance.

Dim printDialog As New System.Windows.Forms.PrintDialog()

'Sets new PrintDocument instance to print dialog.

printDialog.Document = New PrintDocument()

'Enables the print current page option.

printDialog.AllowCurrentPage = True

'Enables the print selected pages option.

printDialog.AllowSomePages = True

'Sets the start and end page index

printDialog.PrinterSettings.FromPage = 1

printDialog.PrinterSettings.ToPage = images.Length

'Opens the print dialog box.

If printDialog.ShowDialog() = System.Windows.Forms.DialogResult.OK Then

'Checks whether the selected page range is valid or not.

If printDialog.PrinterSettings.FromPage > 0 AndAlso printDialog.PrinterSettings.ToPage <= images.Length Then

'Updates the start page of the document to print.

startPageIndex = printDialog.PrinterSettings.FromPage - 1

'Updates the end page of the document to print.

endPageIndex = printDialog.PrinterSettings.ToPage

'Hooks the PrintPage event to handle the drawing pages for printing.

printDialog.Document.PrintPage += New PrintPageEventHandler(PrintPageMethod)

'Prints the document.

printDialog.Document.Print()

End If

End If

Private Sub PrintPageMethod(sender As Object, e As PrintPageEventArgs)

'Gets the print start page width.

Dim currentPageWidth As Integer = images(startPageIndex).Width

'Gets the print start page height.

Dim currentPageHeight As Integer = images(startPageIndex).Height

'Gets the visible bounds width for print.

Dim visibleClipBoundsWidth As Integer = CInt(e.Graphics.VisibleClipBounds.Width)

'Gets the visible bounds height for print.

Dim visibleClipBoundsHeight As Integer = CInt(e.Graphics.VisibleClipBounds.Height)

'Checks whether the page layout is landscape or portrait.

If currentPageWidth > currentPageHeight Then

'Translates the position.

e.Graphics.TranslateTransform(0, visibleClipBoundsHeight)

'Rotates the object at 270 degrees

e.Graphics.RotateTransform(270.0F)

'Draws the current page image.

e.Graphics.DrawImage(images(startPageIndex), New System.Drawing.Rectangle(0, 0, currentPageWidth, currentPageHeight))

Else

'Draws the current page image.

e.Graphics.DrawImage(images(startPageIndex), New System.Drawing.Rectangle(0, 0, visibleClipBoundsWidth, visibleClipBoundsHeight))

End If

'Disposes the current page image after drawing.

images(startPageIndex).Dispose()

'Increments the start page index.

startPageIndex += 1

'Updates whether the document contains some more pages to print.

If startPageIndex < endPageIndex Then

e.HasMorePages = True

Else

startPageIndex = 0

End If

End Sub

{% endhighlight %}

{% endtabs %}  

You can download the complete working samples of the code from [here](http://www.syncfusion.com/downloads/support/directtrac/general/Sample-627835418.zip#).

## Working with Styles

A style is a predefined set of table, numbering, paragraph, and character properties that can be applied to regions within a document. DocIO provides the following functionalities related with styles.

* Access and modify the existing styles in the word document
* Create new paragraph style. 
* Apply built-in styles.

### Access Styles

Paragraph and character styles present in the existing document are accessible through the `Styles` property of `WordDocument` class. 

This following code example demonstrates how a style can be accessed and style properties like text color and first line indent can be updated.

{% tabs %}  

{% highlight c# %}

//Opens an input Word template

WordDocument document = new WordDocument(inputFileName);

//Accesses the styles collection that contains paragraph and character styles in Word document

IStyleCollection styleCollection = document.Styles;

//Finds the style with the name "Heading 1"

WParagraphStyle heading1ParagraphStyle = styleCollection.FindByName("Heading 1") as WParagraphStyle;

//Changes the text color of style "Heading 1" as DarkBlue

heading1ParagraphStyle.CharacterFormat.TextColor = Color.DarkBlue;

//Changes the first line indent of Paragraph as 36 points

heading1ParagraphStyle.ParagraphFormat.FirstLineIndent = 36;

//Saves and closes the document instance

document.Save(outputFileName, FormatType.Docx);

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens an input Word template

Dim document As New WordDocument(inputFileName)

'Accesses the styles collection that contains paragraph and character styles in Word document

Dim styleCollection As IStyleCollection = document.Styles

'Finds the style with the name "Heading 1"

Dim heading1ParagraphStyle As WParagraphStyle = TryCast(styleCollection.FindByName("Heading 1"), WParagraphStyle)

'Changes the text color of style "Heading 1" as DarkBlue

heading1ParagraphStyle.CharacterFormat.TextColor = Color.DarkBlue

'Changes the first line indent of paragraph as 36 points

heading1ParagraphStyle.ParagraphFormat.FirstLineIndent = 36

'Saves and closes the document instance

document.Save(outputFileName, FormatType.Docx)

document.Close()

{% endhighlight %} 

{% endtabs %}  

### Creating a new Paragraph Style

You can create a new paragraph style by using `WordDocument.AddParagraphStyle` method and apply it by using `ApplyStyle` method of `WParagraph` class.

{% tabs %}  

{% highlight c# %}

//Opens an input Word template

WordDocument document = new WordDocument();

//This method adds a section and a paragraph in the document

document.EnsureMinimal();

//Adds a new paragraph style named "MyStyle"

IWParagraphStyle myStyle = document.AddParagraphStyle("MyStyle");

//Sets the formatting of the style

myStyle.CharacterFormat.FontSize = 16f;

myStyle.CharacterFormat.TextColor = Color.DarkBlue;

myStyle.ParagraphFormat.HorizontalAlignment = HorizontalAlignment.Right;

//Appends the contents into the paragraph

document.LastParagraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");

//Applies the style to paragraph

document.LastParagraph.ApplyStyle("MyStyle");

document.Save(outputFileName, FormatType.Docx);

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens an input Word template

Dim document As New WordDocument()

'This method adds a section and a paragraph in the document

document.EnsureMinimal()

'Adds a new paragraph style named "MyStyle"

Dim myStyle As IWParagraphStyle = document.AddParagraphStyle("MyStyle")

'Sets the formatting of the style

myStyle.CharacterFormat.FontSize = 16.0F

myStyle.CharacterFormat.TextColor = Color.DarkBlue

myStyle.ParagraphFormat.HorizontalAlignment = HorizontalAlignment.Right

'Appends the content into the paragraph

document.LastParagraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.")

'Applies the style to paragraph

document.LastParagraph.ApplyStyle("MyStyle")

document.Save(outputFileName, FormatType.Docx)

document.Close()

{% endhighlight %} 

{% endtabs %}  
 
### Applying built-in styles

DocIO provides a set of predefined styles. You can apply those predefined styles as shown in the following code example.

{% tabs %} 

{% highlight c# %}

//Opens an input Word template

WordDocument document = new WordDocument();

//This method adds a section and a paragraph in the document

document.EnsureMinimal();

IWParagraph paragraph = document.LastParagraph;

//Appends the content into the paragraph

paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");

//Applies the style to paragraph

paragraph.ApplyStyle(BuiltinStyle.Emphasis);

document.Save(outputFileName, FormatType.Docx);

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens an input Word template

Dim document As New WordDocument()

'This method adds a section and a paragraph in the document

document.EnsureMinimal()

Dim paragraph As IWParagraph = document.LastParagraph

'Appends the content into the paragraph

paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.")

'Applies the style to paragraph

paragraph.ApplyStyle(BuiltinStyle.Emphasis)

document.Save(outputFileName, FormatType.Docx)

document.Close()

{% endhighlight %}

{% endtabs %}  

## Working with Word document properties

Document properties, also known as metadata, are details about a file that describe or identify it. You can also define the additional custom document properties for the documents by using DocIO Document properties that are classified as two categories. 

* Built-in document properties - includes details such as title, author name, subject, and keywords that identify the document's topic or contents.
* Custom document properties - defines the user-defined document properties.

### Built-in document properties

The Built-in document properties of a word document is represented by `BuiltinDocumentProperties` property of `WordDocument` class. The following code example illustrates how to access and modify the Built-in document properties of the document.

{% tabs %} 

{% highlight c# %}

//Opens an existing Word document

WordDocument document = new WordDocument(inputFileName);

//Accesses the built-in document properties

Console.WriteLine("Title - {0}",document.BuiltinDocumentProperties.Title);

Console.WriteLine("Author - {0}", document.BuiltinDocumentProperties.Author);

//Modifies or sets the category and company Built-in document properties

document.BuiltinDocumentProperties.Category = "Sales reports";

document.BuiltinDocumentProperties.Company = "Northwind traders";

document.Save(outputFileName, FormatType.Docx);

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing Word document

Dim document As New WordDocument(inputFileName)

'Accesses the built-in document properties

Console.WriteLine("Title - {0}", document.BuiltinDocumentProperties.Title)

Console.WriteLine("Author - {0}", document.BuiltinDocumentProperties.Author)

'Modifies or sets the category and company Built-in document properties

document.BuiltinDocumentProperties.Category = "Sales reports"

document.BuiltinDocumentProperties.Company = "Northwind traders"

'Saves and closes the document

document.Save(outputFileName, FormatType.Docx)

document.Close()

{% endhighlight %}

{% endtabs %}  

 
### Adding Custom Document properties

You add a new custom document properties through `Add` method of `CustomProperties` class. The following code example illustrates how to add a new custom document properties.

{% tabs %} 

{% highlight c# %}

//Opens an input word template

WordDocument document = new WordDocument(inputFileName);

//Adds the custom document properties of various data types

document.CustomDocumentProperties.Add("PropertyA", "Value of A");

document.CustomDocumentProperties.Add("PropertyB", 12.5);

document.CustomDocumentProperties.Add("PropertyC", true);

document.CustomDocumentProperties.Add("PropertyD", new DateTime(2015,7,20));

//Saves and closes the document

document.Save(outputFileName, FormatType.Docx);

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing document from file system through constructor of WordDocument class

Dim document As New WordDocument(inputFileName)

'Adds the custom document properties of various data types

document.CustomDocumentProperties.Add("PropertyA", "Value of A")

document.CustomDocumentProperties.Add("PropertyB", 12.5)

document.CustomDocumentProperties.Add("PropertyC", True)

document.CustomDocumentProperties.Add("PropertyD", New DateTime(2015, 7, 20))

'Saves and closes the document

document.Save(outputFileName, FormatType.Docx)

document.Close()

{% endhighlight %} 

{% endtabs %}  

### Accessing & Modifying Custom Document Properties

You can access and modify an existing document property as shown in the following code example.

{% tabs %} 

{% highlight c# %}

WordDocument document = new WordDocument(inputFileName);

//Accesses an existing custom document property

DocumentProperty property = document.CustomDocumentProperties["PropertyA"];

//Modifies the value of DocumentProperty instance

property.Value = "Hello world";

document.Save(outputFileName, FormatType.Docx);

document.Close();

{% endhighlight %}

{% highlight vb.net %}


Dim document As New WordDocument(inputFileName)

'Accesses an existing custom document property

Dim [property] As DocumentProperty = document.CustomDocumentProperties("PropertyA")

'Modifies the value of DocumentProperty instance

[property].Value = "Hello world"

document.Save(outputFileName, FormatType.Docx)

document.Close()

{% endhighlight %}  

{% endtabs %}  
  
## Setting the Background for a Word document

Essential DocIO allows to apply background such as color, gradient and picture to the Word document. A background of a Word document is represented by `Background` property of `WordDocument' class. 

The following code illustrates how to apply gradient as background to the document.

{% tabs %}

{% highlight c# %}

//Creates a new Word document

WordDocument document = new WordDocument();

//Adds new section to the document

WSection section = document.AddSection() as WSection;

//Adds new paragraph to the section

IWParagraph paragraph = section.AddParagraph() as WParagraph;

//Appends text to the paragraph

paragraph.AppendText("Sample for applying document background");

//Sets the background type as gradient

document.Background.Type = BackgroundType.Gradient;

//Sets color for gradient

document.Background.Gradient.Color1 = Color.LightGray;

document.Background.Gradient.Color2 = Color.LightGreen;

//Sets the shading style 

document.Background.Gradient.ShadingStyle = GradientShadingStyle.DiagonalUp;

document.Background.Gradient.ShadingVariant = GradientShadingVariant.ShadingDown;

//Saves the document

document.Save("Sample.docx", FormatType.Docx);

//Closes the document

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates a new Word document 

Dim document As New WordDocument()

'Adds new section to the document

Dim section As WSection = TryCast(document.AddSection(), WSection)

'Adds new paragraph to the section 

Dim paragraph As IWParagraph = TryCast(section.AddParagraph(), WParagraph)

'Appends text to the paragraph

paragraph.AppendText("Sample for applying document background")

'Sets the background type as gradient

document.Background.Type = BackgroundType.Gradient

'Sets color for gradient

document.Background.Gradient.Color1 = Color.LightGray

document.Background.Gradient.Color2 = Color.LightGreen

'Sets the shading style 

document.Background.Gradient.ShadingStyle = GradientShadingStyle.DiagonalUp

document.Background.Gradient.ShadingVariant = GradientShadingVariant.ShadingDown

'Saves the document

document.Save("Sample.docx", FormatType.Docx)

'Closes the document

document.Close()

{% endhighlight %}

 {% endtabs %}  
 
The following code illustrates how to apply image as background for the document.

{% tabs %} 

{% highlight c# %}

//Creates a new Word document

WordDocument document = new WordDocument();

//Adds new section to the document 

WSection section = document.AddSection() as WSection;

//Adds new paragraph to the section

IWParagraph paragraph = section.AddParagraph() as WParagraph;

//Appends text to the paragraph

paragraph.AppendText("Sample for applying document background");

//Sets the background type as picture

document.Background.Type = BackgroundType.Picture;

document.Background.Picture = Image.FromFile("Image.png");

//Saves the document

document.Save("Sample.docx", FormatType.Docx);

//Closes the document

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates a new Word document

Dim document As New WordDocument()

'Adds new section to document

Dim section As WSection = TryCast(document.AddSection(), WSection)

'Adds new paragraph to the section

Dim paragraph As IWParagraph = TryCast(section.AddParagraph(), WParagraph)

'Appends text to the paragraph

paragraph.AppendText("Sample for applying document background")

'Sets the background type as picture

document.Background.Type = BackgroundType.Picture

document.Background.Picture = Image.FromFile("Image.png")

'Saves the document

document.Save("Sample.docx", FormatType.Docx)

'Closes the document

document.Close()

{% endhighlight %}

{% endtabs %}  