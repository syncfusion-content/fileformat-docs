---
layout: Post
title: Working with Word document
description: This section illustrates how to work with Word document
platform: FileFormat
control: DocIO
documentation: UG
---
# Working with Word document

## Iterating through document elements

The following are the important points to be remembered while iterating the document elements

* Document consists of one or more section.
* Section contains the contents present in Headers, Footers and main document through the instances of WTextBody.
* WTextBody can contain two type of elements – either paragraph or table

The following code snippet shows how to iterate throughout the Word document and remove the paragraph with a particular style

{% highlight c# %}
[C#]

using Syncfusion.DocIO.DLS;

namespace RemoveParagraphs

{

class Program

{

static void Main(string[] args)

{

WordDocument document = new WordDocument(@"TestDocument.docx");

//Process the body contents for each section in the Word document

foreach (WSection section in document.Sections)

{

//Access the Body of section where all the contents in document apart

WTextBody sectionBody = section.Body;

IterateTextBody(sectionBody);

WHeadersFooters headersFooters = section.HeadersFooters;

//Consider that OddHeader & OddFooter are applied to this document

//Iterate through the TextBody of OddHeader & OddFooter

IterateTextBody(headersFooters.OddHeader);

IterateTextBody(headersFooters.OddFooter);

}

//Save & Close the document instance

document.Save("Result.docx");

document.Close();

System.Diagnostics.Process.Start("Result.docx");

}

private static void IterateTextBody(WTextBody textBody)

{

//Iterate through the each of the child items of WTextBody

for(int i = 0; i < textBody.ChildEntities.Count; i++)

{

//IEntity is the basic unit in DocIO DOM. 

//Accessing the body items (should be either paragraph or table) as IEntity

IEntity bodyItemEntity = textBody.ChildEntities[i];

//A Text body can have 2 type of elements - Paragraph and Table

//decide the element type using EntityType

switch (bodyItemEntity.EntityType)

{

case EntityType.Paragraph:

WParagraph paragraph = bodyItemEntity as WParagraph;

//Check for particular style name and remove the paragraph from DOM

if (paragraph.StyleName == "MyStyle")

{

int index = textBody.ChildEntities.IndexOf(paragraph);

textBody.ChildEntities.RemoveAt(index);

}

break;

case EntityType.Table:

//Table is a collection of rows & cells

//Iterate through table's DOM

IterateTable(bodyItemEntity as WTable);

break;

}

}

}

private static void IterateTable(WTable table)

{

//Iterate the row collection in a table

foreach (WTableRow row in table.Rows)

{

//Iterate the cell collection in a table row

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

{% highlight vbnet %}
[VB]

Imports Syncfusion.DocIO.DLS

Namespace RemoveParagraphs

Class Program

Private Shared Sub Main(args As String())

Dim document As New WordDocument("TestDocument.docx")

'Process the body contents for each section in the Word document

For Each section As WSection In document.Sections

'Access the Body of section where all the contents in document apart

Dim sectionBody As WTextBody = section.Body

IterateTextBody(sectionBody)

Dim headersFooters As WHeadersFooters = section.HeadersFooters

'Consider that OddHeader & OddFooter are applied to this document

'Iterate through the text body of OddHeader & OddFooter

IterateTextBody(headersFooters.OddHeader)

IterateTextBody(headersFooters.OddFooter)

Next

'Save & Close the document instance

document.Save("Result.docx")

document.Close()

System.Diagnostics.Process.Start("Result.docx")

End Sub

Private Shared Sub IterateTextBody(textBody As WTextBody)

'Iterate through the each of the child items of WTextBody

For i As Integer = 0 To textBody.ChildEntities.Count - 1

'IEntity is the basic unit in DocIO DOM. 

'Accessing the body items (should be either paragraph or table) as IEntity

Dim bodyItemEntity As IEntity = textBody.ChildEntities(i)

'A Text body can have 2 type of elements - Paragraph and Table

'decide the element type using EntityType

Select Case bodyItemEntity.EntityType

Case EntityType.Paragraph

Dim paragraph As WParagraph = TryCast(bodyItemEntity, WParagraph)

'Check for particular style name and remove the paragraph from DOM

If paragraph.StyleName = "MyStyle" Then

Dim index As Integer = textBody.ChildEntities.IndexOf(paragraph)

textBody.ChildEntities.RemoveAt(index)

End If

Exit Select

Case EntityType.Table

'Table is a collection of rows & cells

'Iterate through table's DOM

IterateTable(TryCast(bodyItemEntity, WTable))

Exit Select

End Select

Next

End Sub

Private Shared Sub IterateTable(table As WTable)

'Iterate the row collection in a table

For Each row As WTableRow In table.Rows

'Iterate the cell collection in a table row

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

The following code snippet shows how to iterate throughout the paragraph and modify the hyperlink (**Hyperlink****)** Uri and specific text (**WTextRange****)** with another.

{% highlight c# %}
[C#]

using Syncfusion.DocIO.DLS;

using Syncfusion.DocIO;

namespace UpdateText

{

class Program

{

static void Main(string[] args)

{

WordDocument document = new WordDocument(@"TestDocument.docx");

//Process the body contents for each section in the Word document

foreach (WSection section in document.Sections)

{

//Access the Body of section where all the contents in document apart

WTextBody sectionBody = section.Body;

IterateTextBody(sectionBody);

WHeadersFooters headersFooters = section.HeadersFooters;

//consider that OddHeader & OddFooter are applied to this document

//Iterate through the TextBody of OddHeader & OddFooter

IterateTextBody(headersFooters.OddHeader);

IterateTextBody(headersFooters.OddFooter);

}

//Save & Close the document instance

document.Save("Result.docx");

document.Close();

System.Diagnostics.Process.Start("Result.docx");

}

private static void IterateTextBody(WTextBody textBody)

{

//Iterate through the each of the child items of WTextBody

for (int i = 0; i < textBody.ChildEntities.Count; i++)

{

//IEntity is the basic unit in DocIO DOM. 

//Accessing the body items (should be either paragraph or table) as IEntity

IEntity bodyItemEntity = textBody.ChildEntities[i];

//A Text body can have 2 type of elements - Paragraph and Table

//decide the element type using EntityType

switch (bodyItemEntity.EntityType)

{

case EntityType.Paragraph:

WParagraph paragraph = bodyItemEntity as WParagraph;

//Process the paragraph contents

//Iterate through the paragraph's DOM

IterateParagraph(paragraph);

break;

case EntityType.Table:

//Table is a collection of rows & cells

//Iterate through table's DOM

IterateTable(bodyItemEntity as WTable);

break;

}

}

}

private static void IterateTable(WTable table)

{

//Iterate the row collection in a table

foreach (WTableRow row in table.Rows)

{

//Iterate the cell collection in a table row

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

//decide the element type using EntityType

switch (entity.EntityType)

{

case EntityType.TextRange:

//Replacing the text with another

WTextRange textRange = entity as WTextRange;

if (textRange.Text == "Mayur")

{

(entity as WTextRange).Text = "Gerrit";

}

break;

case EntityType.Field:

WField field = entity as WField;

if (field.FieldType == FieldType.FieldHyperlink)

{

//Create hyperlink instance from field to manipulate the hyperlink

Hyperlink hyperlink = new Hyperlink(entity as WField);

//Modify the Uri of the hyperlink

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

{% highlight vbnet %}
[VB]

Imports Syncfusion.DocIO.DLS

Imports Syncfusion.DocIO

Namespace UpdateText

Class Program

Private Shared Sub Main(args As String())

Dim document As New WordDocument("TestDocument.docx")

'Process the body contents for each section in the Word document

For Each section As WSection In document.Sections

'Access the Body of section where all the contents in document apart

Dim sectionBody As WTextBody = section.Body

IterateTextBody(sectionBody)

Dim headersFooters As WHeadersFooters = section.HeadersFooters

'Consider that OddHeader & OddFooter are applied to this document

'Iterate through the TextBody of OddHeader & OddFooter

IterateTextBody(headersFooters.OddHeader)

IterateTextBody(headersFooters.OddFooter)

Next

'Save & Close the document instance

document.Save("Result.docx")

document.Close()

System.Diagnostics.Process.Start("Result.docx")

End Sub

Private Shared Sub IterateTextBody(textBody As WTextBody)

'Iterate through the each of the child items of WTextBody

For i As Integer = 0 To textBody.ChildEntities.Count - 1

'IEntity is the basic unit in DocIO DOM. 

'Accessing the body items (should be either paragraph or table) as IEntity

Dim bodyItemEntity As IEntity = textBody.ChildEntities(i)

'A Text body can have 2 type of elements - Paragraph and Table

'decide the element type using EntityType

Select Case bodyItemEntity.EntityType

Case EntityType.Paragraph

Dim paragraph As WParagraph = TryCast(bodyItemEntity, WParagraph)

'Process the paragraph contents

'Iterate through the paragraph's DOM

IterateParagraph(paragraph)

Exit Select

Case EntityType.Table

'Table is a collection of rows & cells

'Iterate through table's DOM

IterateTable(TryCast(bodyItemEntity, WTable))

Exit Select

End Select

Next

End Sub

Private Shared Sub IterateTable(table As WTable)

'Iterate the row collection in a table

For Each row As WTableRow In table.Rows

'Iterate the cell collection in a table row

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

'A Paragraph can have child elements such as text, image, hyperlink, symbols, etc.,

'decide the element type using EntityType

Select Case entity.EntityType

Case EntityType.TextRange

'Replacing the text with another

Dim textRange As WTextRange = TryCast(entity, WTextRange)

If textRange.Text = "Mayur" Then

TryCast(entity, WTextRange).Text = "Gerrit"

End If

Exit Select

Case EntityType.Field

Dim field As WField = TryCast(entity, WField)

If field.FieldType = FieldType.FieldHyperlink Then

'Create Hyperlink instance from field to manipulate the Hyperlink

Dim hyperlink As New Hyperlink(TryCast(entity, WField))

'Modify the Uri of the hyperlink

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

## Cloning a Word document



You can create a deep copy of a Word document using Clone method of WordDocument class. We can read the template document once from file system or stream and create multiple document copies by cloning it. This will improve the performance of document generation, as there is no need to read the Word document each time.

{% highlight c# %}
[C#]

//Open an existing document 

WordDocument inputTemplateDoc = new WordDocument(fileName);

//Create a clone of Input Template 

WordDocument clonedDocument = inputTemplateDoc.Clone();

//Save & Close the cloned document instance

clonedDocument.Save("ClonedDocument.docx");

clonedDocument.Close();

//Close the input template document instance

sourceDocument.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB]

'Open an existing document 

Dim inputTemplateDoc As New WordDocument(fileName)

'Create a clone of Input Template 

Dim clonedDocument As WordDocument = inputTemplateDoc.Clone()

'Save & Close the cloned document instance

clonedDocument.Save("ClonedDocument.docx")

clonedDocument.Close()

'Close the input template document instance

sourceDocument.Close()





{% endhighlight %}

You can also create a deep copy of document elements such as sections, paragraphs, Tables, Text, Image, OleObject, Shapes, TextBoxes and etc., the following code snippets illustrates how to clone the section and save each cloned section as a Word document. 

{% highlight c# %}
[C#]

//Open a source document

WordDocument sourceDocument = new WordDocument("SourceDocument.docx");

//Process the each section in the Word document

for (int i = 0; i < sourceDocument.Sections.Count;i++)

{

//Create new WordDocument instance to add cloned section

WordDocument destinationDocument = new WordDocument();

//Clone and add source document sections to the destination document

destinationDocument.Sections.Add(sourceDocument.Sections[i].Clone());

//Save & Close the document instance

destionationDocument.Save("Section_" + i + ".docx");

destinationDocument.Close();

}

//Close the source document instance

sourceDocument.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB]

'Open a source document

Dim sourceDocument As New WordDocument("SourceDocument.docx")

'Process the each section in the Word document

For i As Integer = 0 To sourceDocument.Sections.Count - 1

'Create new WordDocument instance to add cloned section

Dim destinationDocument As New WordDocument()

'Clone and add source document sections to the destination document

destinationDocument.Sections.Add(sourceDocument.Sections(i).Clone())

'Save & Close the document instance

destionationDocument.Save("Section_" + i + ".docx")

destinationDocument.Close()

Next

'Close the source document instance

sourceDocument.Close()



{% endhighlight %}

## Merging Word documents

You can merge multiple Word documents into single Word document using DocIO’s capability of importing contents from one document to another. The imported contents will be appended at the end of document.  The following code snippet illustrates how to import the contents from source document into destination document (where the contents will be appended). 



{% highlight c# %}
[C#]

//Open the source document 

WordDocument sourceDocument = new WordDocument(sourceFileName);

//Open the destination document 

WordDocument destinationDocument = new WordDocument(targetFileName);

//Import the contents of source document at the end of destination document

destinationDocument.ImportContent(sourceDocument, ImportOptions.UseDestinationStyles);

//Save the destination document

destinationDocument.Save(outputFileName, FormatType.Docx);

//close the document instances

sourceDocument.Close();

destinationDocument.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB]

'Open the source document 

Dim sourceDocument As New WordDocument(sourceFileName)

'Open the destination document 

Dim destinationDocument As New WordDocument(targetFileName)

'Import the contents of source document at the end of destination document

destinationDocument.ImportContent(sourceDocument, ImportOptions.UseDestinationStyles)

'Save the destination document

destinationDocument.Save(outputFileName, FormatType.Docx)

'close the document instances

sourceDocument.Close()

destinationDocument.Close()



{% endhighlight %}

In the resultant document, the imported contents will start from a new page followed by existing contents in destination document. This is the default behavior.

If your requirement is to append the contents from the same page instead of starting from a new page, we need to set the break code of First section of Source document as NoBreak. The following code snippet illustrates the importing contents from the same page.

{% highlight c# %}
[C#]

//Open the source document 

WordDocument sourceDocument = new WordDocument(sourceFileName);

//Open the destination document 

WordDocument destinationDocument = new WordDocument(targetFileName);

//Set the breakcode of First section of source document as NoBreak to avoid imported from a new page

sourceDocument.Sections[0].BreakCode = SectionBreakCode.NoBreak; 

//Import the contents of source document at the end of destination document

destinationDocument.ImportContent(sourceDocument, ImportOptions.UseDestinationStyles);

//Save the destination document

destinationDocument.Save(outputFileName, FormatType.Docx);

//Close the document instances

sourceDocument.Close();

destinationDocument.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB]

'Open the source document 

Dim sourceDocument As New WordDocument(sourceFileName)

'Open the destination document 

Dim destinationDocument As New WordDocument(targetFileName)

'Set the breakcode of First section of source document as NoBreak to avoid imported from a new page

sourceDocument.Sections(0).BreakCode = SectionBreakCode.NoBreak

'Import the contents of source document at the end of destination document

destinationDocument.ImportContent(sourceDocument, ImportOptions.UseDestinationStyles)

'Save the destination document

destinationDocument.Save(outputFileName, FormatType.Docx)

'Close the document instances

sourceDocument.Close()

destinationDocument.Close()



{% endhighlight %}

## Printing a Word document

You can print a Word document by utilizing DocIO’s capability to convert the document into images and .NET framework’s [PrintDocument](https://msdn.microsoft.com/en-us/library/System.Drawing.Printing.PrintDocument(v=vs.110).aspx# "") class

Initially you have to rasterize the pages as images as shown below

{% highlight c# %}
[C#]

//Opens the Word document.

WordDocument document = new WordDocument((string)this.textBox.Tag);

//Renders the Word document as image.

Image[] images = document.RenderAsImages(ImageType.Metafile);

//Closes the Word Document.

document.Close();





{% endhighlight %}

{% highlight vbnet %}
[VB]

'Opens the Word document.

Dim document As New WordDocument(DirectCast(Me.textBox.Tag, String))

'Renders the Word document as image.

Dim images As Image() = document.RenderAsImages(ImageType.Metafile)

'Close the Word Document.

document.Close()



{% endhighlight %}

You can specify the printer settings and page settings through the [PrintDocument](https://msdn.microsoft.com/en-us/library/System.Drawing.Printing.PrintDocument(v=vs.110).aspx# "") class. The [PrintDocument.PrintPage](https://msdn.microsoft.com/en-us/library/system.drawing.printing.printdocument.printpage%28v=vs.110%29.aspx# "") event should be handled to layout the document for printing. 

The following code snippet demonstrates how to print the Word document pages that have been rendered as an image:

{% highlight c# %}
[C#]

int endPageIndex = images.Length;

//Create new PrintDialog instance.

System.Windows.Forms.PrintDialog printDialog = new System.Windows.Forms.PrintDialog();

//Set new PrintDocument instance to print dialog.

printDialog.Document = new PrintDocument();

//Enable the print current page option.

printDialog.AllowCurrentPage = true;

//Enable the print selected pages option.

printDialog.AllowSomePages = true;

//Set the start and end page index

printDialog.PrinterSettings.FromPage = 1;

printDialog.PrinterSettings.ToPage = images.Length;

//Open the print dialog box.

if (printDialog.ShowDialog() == System.Windows.Forms.DialogResult.OK)

{

//Check if the selected page range is valid.

if (printDialog.PrinterSettings.FromPage > 0 && printDialog.PrinterSettings.ToPage <= images.Length)

{

//Update the start page of the document to print.

startPageIndex = printDialog.PrinterSettings.FromPage - 1;

//Update the end page of the document to print.

endPageIndex = printDialog.PrinterSettings.ToPage;

//Hook the PrintPage event to handle be drawing pages for printing.

printDialog.Document.PrintPage += new PrintPageEventHandler(PrintPageMethod);

//Print the document.

printDialog.Document.Print();

}

}

private void PrintPageMethod (object sender, PrintPageEventArgs e)

{

//Get the print start page width.

int currentPageWidth = images[startPageIndex].Width;

//Get the print start page height.

int currentPageHeight = images[startPageIndex].Height;

//Get the visible bounds width for print.

int visibleClipBoundsWidth = (int)e.Graphics.VisibleClipBounds.Width;

//Get the visible bounds height for print.

int visibleClipBoundsHeight = (int)e.Graphics.VisibleClipBounds.Height;

//Check if the page layout is landscape or portrait.

if (currentPageWidth > currentPageHeight)

{

//Translate the position.

e.Graphics.TranslateTransform(0, visibleClipBoundsHeight);

//Rotate the object at 270 degrees

e.Graphics.RotateTransform(270.0f);

//Draw the current page image.

e.Graphics.DrawImage(images[startPageIndex], new System.Drawing.Rectangle(0, 0, currentPageWidth, currentPageHeight));

}

else

{

//Draw the current page image.

e.Graphics.DrawImage(images[startPageIndex], new System.Drawing.Rectangle(0, 0, visibleClipBoundsWidth, visibleClipBoundsHeight));

}

//Dispose the current page image after drawing.

images[startPageIndex].Dispose();

//Increment the start page index.

startPageIndex++;

//Update if the document contains some more pages to print.

if (startPageIndex < endPageIndex)

e.HasMorePages = true;

else

startPageIndex = 0;

}





{% endhighlight %}

{% highlight vbnet %}
[VB]

Dim endPageIndex As Integer = images.Length

'Create new PrintDialog instance.

Dim printDialog As New System.Windows.Forms.PrintDialog()

'Set new PrintDocument instance to print dialog.

printDialog.Document = New PrintDocument()

'Enable the print current page option.

printDialog.AllowCurrentPage = True

'Enable the print selected pages option.

printDialog.AllowSomePages = True

'Set the start and end page index

printDialog.PrinterSettings.FromPage = 1

printDialog.PrinterSettings.ToPage = images.Length

'Open the print dialog box.

If printDialog.ShowDialog() = System.Windows.Forms.DialogResult.OK Then

'Check if the selected page range is valid.

If printDialog.PrinterSettings.FromPage > 0 AndAlso printDialog.PrinterSettings.ToPage <= images.Length Then

'Update the start page of the document to print.

startPageIndex = printDialog.PrinterSettings.FromPage - 1

'Update the end page of the document to print.

endPageIndex = printDialog.PrinterSettings.ToPage

'Hook the PrintPage event to handle be drawing pages for printing.

printDialog.Document.PrintPage += New PrintPageEventHandler(PrintPageMethod)

'Print the document.

printDialog.Document.Print()

End If

End If

Private Sub PrintPageMethod(sender As Object, e As PrintPageEventArgs)

'Get the print start page width.

Dim currentPageWidth As Integer = images(startPageIndex).Width

'Get the print start page height.

Dim currentPageHeight As Integer = images(startPageIndex).Height

'Get the visible bounds width for print.

Dim visibleClipBoundsWidth As Integer = CInt(e.Graphics.VisibleClipBounds.Width)

'Get the visible bounds height for print.

Dim visibleClipBoundsHeight As Integer = CInt(e.Graphics.VisibleClipBounds.Height)

'Check if the page layout is landscape or portrait.

If currentPageWidth > currentPageHeight Then

'Translate the position.

e.Graphics.TranslateTransform(0, visibleClipBoundsHeight)

'Rotate the object at 270 degrees

e.Graphics.RotateTransform(270.0F)

'Draw the current page image.

e.Graphics.DrawImage(images(startPageIndex), New System.Drawing.Rectangle(0, 0, currentPageWidth, currentPageHeight))

Else

'Draw the current page image.

e.Graphics.DrawImage(images(startPageIndex), New System.Drawing.Rectangle(0, 0, visibleClipBoundsWidth, visibleClipBoundsHeight))

End If

'Dispose the current page image after drawing.

images(startPageIndex).Dispose()

'Increment the start page index.

startPageIndex += 1

'Update if the document contains some more pages to print.

If startPageIndex < endPageIndex Then

e.HasMorePages = True

Else

startPageIndex = 0

End If

End Sub





{% endhighlight %}

You can download the complete working samples of the code from [here](http://www.syncfusion.com/downloads/support/directtrac/general/Sample-627835418.zip# "").

## Working with Styles

A style is predefined set of table, numbering, paragraph, and character properties which can be applied to regions within a document. DocIO provides the following functionalities related with styles.

* Access & modify the existing styles in the word document
* Create new paragraph style. 
* Apply built-in styles.

**Access** **Styles**

Paragraph and character styles present in the existing document are accessible through the WordDocument.Styles property. 

This below code snippet demonstrates how a style can be accessed and style properties like text color and first line indent can be updated.

{% highlight c# %}
[C#]

//Open an input Word template

WordDocument document = new WordDocument(inputFileName);

//Access the styles collection which contains paragraph & character styles in Word document

IStyleCollection styleCollection = document.Styles;

//Find the style with the name "Heading 1"

WParagraphStyle heading1ParagraphStyle = styleCollection.FindByName("Heading 1") as WParagraphStyle;

//Change the text color of style "Heading 1" as DarkBlue

heading1ParagraphStyle.CharacterFormat.TextColor = Color.DarkBlue;

//Change the first line indent of Paragraph as 36 points

heading1ParagraphStyle.ParagraphFormat.FirstLineIndent = 36;

document.Save(outputFileName, FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB]

'Open an input Word template

Dim document As New WordDocument(inputFileName)

'Access the styles collection which contains paragraph & character styles in Word document

Dim styleCollection As IStyleCollection = document.Styles

'Find the style with the name "Heading 1"

Dim heading1ParagraphStyle As WParagraphStyle = TryCast(styleCollection.FindByName("Heading 1"), WParagraphStyle)

'Change the text color of style "Heading 1" as DarkBlue

heading1ParagraphStyle.CharacterFormat.TextColor = Color.DarkBlue

'Change the first line indent of paragraph as 36 points

heading1ParagraphStyle.ParagraphFormat.FirstLineIndent = 36

document.Save(outputFileName, FormatType.Docx)

document.Close()



{% endhighlight %}

**Creating** **a** **new** **Paragraph** **Style**

You can create a new paragraph style using WordDocument.AddParagraphStyle method and apply it using ApplyStyle method of WParagraph class.

{% highlight c# %}
[C#]

//Open an input Word template

WordDocument document = new WordDocument();

//This method will add a section & a paragraph in the document

document.EnsureMinimal();



//Add a new paragraph style named "MyStyle"

IWParagraphStyle myStyle = document.AddParagraphStyle("MyStyle");

//Set the formattings of the style

myStyle.CharacterFormat.FontSize = 16f;

myStyle.CharacterFormat.TextColor = Color.DarkBlue;

myStyle.ParagraphFormat.HorizontalAlignment = HorizontalAlignment.Right;

//Append the contents into the paragraph

document.LastParagraph.AppendText("Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua");



//Apply the style to paragraph

document.LastParagraph.ApplyStyle("MyStyle");

document.Save(outputFileName, FormatType.Docx);

document.Close();





{% endhighlight %}

{% highlight vbnet %}
[VB]

'Open an input Word template

Dim document As New WordDocument()

'This method will add a section & a paragraph in the document

document.EnsureMinimal()

'Add a new paragraph style named "MyStyle"

Dim myStyle As IWParagraphStyle = document.AddParagraphStyle("MyStyle")

'Set the formattings of the style

myStyle.CharacterFormat.FontSize = 16.0F

myStyle.CharacterFormat.TextColor = Color.DarkBlue

myStyle.ParagraphFormat.HorizontalAlignment = HorizontalAlignment.Right

'Append the content into the paragraph

document.LastParagraph.AppendText("Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua")

'Apply the style to paragraph

document.LastParagraph.ApplyStyle("MyStyle")

document.Save(outputFileName, FormatType.Docx)

document.Close()





{% endhighlight %}

**Applying** **built****-****in** **styles**

DocIO provides a set of predefined styles to the user. You can apply those predefined styles as like shown in the below code snippet.

{% highlight c# %}
[C#]

//Open an input Word template

WordDocument document = new WordDocument();

//This method will add a section & a paragraph in the document

document.EnsureMinimal();

IWParagraph paragraph = document.LastParagraph;

//Append the content into the paragraph

paragraph.AppendText("Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua");



//Applying the style to paragraph

paragraph.ApplyStyle(BuiltinStyle.Emphasis);



document.Save(outputFileName, FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB]

'Open an input Word template

Dim document As New WordDocument()

'This method will add a section & a paragraph in the document

document.EnsureMinimal()

Dim paragraph As IWParagraph = document.LastParagraph

'Append the content into the paragraph

paragraph.AppendText("Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua")

'Apply the style to paragraph

paragraph.ApplyStyle(BuiltinStyle.Emphasis)

document.Save(outputFileName, FormatType.Docx)

document.Close()





{% endhighlight %}

## Working with Word document properties

Document properties, also known as metadata, are details about a file that describe or identify it. Also you can define additional custom document properties for the documents using DocIO Document properties are classified as two categories. 

* **Built****-****in** **DocumentProperties** - which include details such as title, author name, subject, and keywords that identify the document's topic or contents.
* **Custom** **Document** **properties** - defines the user-defined document properties

**Built****-****in** **document** **properties**

The Built-in document properties of a word document is represented by WordDocument.BuiltinDocumentProperties object. The following code snippet illustrates how to access and modify the Built-in document properties of the document.

{% highlight c# %}
[C#]

WordDocument document = new WordDocument(inputFileName);

//Access the built-in document properties

Console.WriteLine("Title - {0}",document.BuiltinDocumentProperties.Title);

Console.WriteLine("Author - {0}", document.BuiltinDocumentProperties.Author);

//Modify or set the category and company Build-in document properties

document.BuiltinDocumentProperties.Category = "Sales reports";

document.BuiltinDocumentProperties.Company = "Northwind traders";



document.Save(outputFileName, FormatType.Docx);

document.Close();





{% endhighlight %}

{% highlight vbnet %}
[VB]

Dim document As New WordDocument(inputFileName)

'Access the built-in document properties

Console.WriteLine("Title - {0}", document.BuiltinDocumentProperties.Title)

Console.WriteLine("Author - {0}", document.BuiltinDocumentProperties.Author)

'Modify or set the category and company Build-in document properties

document.BuiltinDocumentProperties.Category = "Sales reports"

document.BuiltinDocumentProperties.Company = "Northwind traders"

document.Save(outputFileName, FormatType.Docx)

document.Close()





{% endhighlight %}

**Adding** **Custom** **Document** **properties**

You add a new custom document properties through Add method of CustomProperties class. The following code snippet illustrates about how to add a new custom document properties.

{% highlight c# %}
[C#]

//Open an input word template

WordDocument document = new WordDocument(inputFileName);

//Add the custom document properties of various data type

document.CustomDocumentProperties.Add("PropertyA", "ValueofA");

document.CustomDocumentProperties.Add("PropertyB", 12.5);

document.CustomDocumentProperties.Add("PropertyC", true);

document.CustomDocumentProperties.Add("PropertyD", new DateTime(2015,7,20));



document.Save(outputFileName, FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB]

'Open an input word template

Dim document As New WordDocument(inputFileName)

'Add the custom document properties of various data type

document.CustomDocumentProperties.Add("PropertyA", "ValueofA")

document.CustomDocumentProperties.Add("PropertyB", 12.5)

document.CustomDocumentProperties.Add("PropertyC", True)

document.CustomDocumentProperties.Add("PropertyD", New DateTime(2015, 7, 20))

document.Save(outputFileName, FormatType.Docx)

document.Close()





{% endhighlight %}

**Accessing** **&** **Modifying** **Custom** **Document** **Properties**

You can access & modify an existing document property as shown in the below code snippet.

{% highlight c# %}
[C#]

WordDocument document = new WordDocument(inputFileName);

//Access an existing custom document property

DocumentProperty property = document.CustomDocumentProperties["PropertyA"];

//Modify the value of DocumentProperty instance

property.Value = "Hello world";

document.Save(outputFileName, FormatType.Docx);

document.Close();





{% endhighlight %}

{% highlight vbnet %}
[VB]

Dim document As New WordDocument(inputFileName)

'Access an existing custom document property

Dim [property] As DocumentProperty = document.CustomDocumentProperties("PropertyA")

'Modify the value of DocumentProperty instance

[property].Value = "Hello world"

document.Save(outputFileName, FormatType.Docx)

document.Close()





{% endhighlight %}

## Setting the Background for a Word document

Essential DocIO allows to apply background such as color, gradient and picture to the Word document. A background of a Word document is represented by WordDocument.Background object. 

The following code illustrates how to apply gradient as background to the document.

{% highlight c# %}
[C#]

//Create a new Word document

WordDocument document = new WordDocument();

//Add new section to the document

WSection section = document.AddSection() as WSection;

//Add new paragraph to the section

IWParagraph paragraph = section.AddParagraph() as WParagraph;

//Append text to the paragraph

paragraph.AppendText("Sample for applying document background");

//Set the background type as gradient

document.Background.Type = BackgroundType.Gradient;

//Set color for gradient

document.Background.Gradient.Color1 = Color.LightGray;

document.Background.Gradient.Color2 = Color.LightGreen;

//Set the shading style 

document.Background.Gradient.ShadingStyle = GradientShadingStyle.DiagonalUp;

document.Background.Gradient.ShadingVariant = GradientShadingVariant.ShadingDown;

//Save the document

document.Save("Sample.docx", FormatType.Docx);

//Close the document

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB]

'Create a new Word document 

Dim document As New WordDocument()

'Add new section to the document

Dim section As WSection = TryCast(document.AddSection(), WSection)

'Add new paragraph to the section 

Dim paragraph As IWParagraph = TryCast(section.AddParagraph(), WParagraph)

'Appending text to the paragraph

paragraph.AppendText("Sample for applying document background")

'Set the background type as gradient

document.Background.Type = BackgroundType.Gradient

'Set color for gradient

document.Background.Gradient.Color1 = Color.LightGray

document.Background.Gradient.Color2 = Color.LightGreen

'Set the shading style 

document.Background.Gradient.ShadingStyle = GradientShadingStyle.DiagonalUp

document.Background.Gradient.ShadingVariant = GradientShadingVariant.ShadingDown

'Save the document

document.Save("Sample.docx", FormatType.Docx)

'Close the document

document.Close()





{% endhighlight %}

The following code illustrates how to apply image as background for the document.

{% highlight c# %}
[C#]

//Create a new Word document

WordDocument document = new WordDocument();

//Add new section to the document 

WSection section = document.AddSection() as WSection;

//Add new paragraph to the section

IWParagraph paragraph = section.AddParagraph() as WParagraph;

//Append text to the paragraph

paragraph.AppendText("Sample for applying document background");

//Set the background type as picture

document.Background.Type = BackgroundType.Picture;

document.Background.Picture = Image.FromFile("Image.png");

//Save the document

document.Save("Sample.docx", FormatType.Docx);

//Close the document

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB]

'Create a new Word document

Dim document As New WordDocument()

'Add new section to document

Dim section As WSection = TryCast(document.AddSection(), WSection)

'Add new paragraph to the section

Dim paragraph As IWParagraph = TryCast(section.AddParagraph(), WParagraph)

'Append text to the paragraph

paragraph.AppendText("Sample for applying document background")

'Set the background type as picture

document.Background.Type = BackgroundType.Picture

document.Background.Picture = Image.FromFile("Image.png")

'Save the document

document.Save("Sample.docx", FormatType.Docx)

'Close the document

document.Close()



{% endhighlight %}

