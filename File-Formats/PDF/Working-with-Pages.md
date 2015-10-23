---
title: Working with pages
description: Addinga pages in the PDF document; PdfPage; remove pages;split pages;rearrange pages;
platform: file-formats
control: PDF
documentation: UG
---
# Working with Pages

## Adding a new page to the document

The following code sample explains you on how to add a page in a PDF document. When multiple pages are added, the new page is always added to the end of the document.

{% highlight c# %}
[C#]

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a page.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Create a solid brush.

PdfBrush brush = new PdfSolidBrush(Color.Black);

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 14);

//Draw the text.

graphics.DrawString("Hello world!", font, brush, new PointF(20, 20));

//Save the document.

document.Save("Output.pdf");

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}
[VB]

'Create a new PDF document.

Dim document As New PdfDocument()

'Add a page.

Dim page As PdfPage = document.Pages.Add()

'Create PDF graphics for the page.

Dim graphics As PdfGraphics = page.Graphics

'Create a solid brush.

Dim brush As PdfBrush = New PdfSolidBrush(Color.Black)

'Set the font.

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 14)

'Draw the text.

graphics.DrawString("Hello world!", font, brush, New PointF(20, 20))

'Save the document.

document.Save("Output.pdf")

document.Close(True)



{% endhighlight %}

## Inserting pages in a document

You can insert an empty page at any location of the existing PDF document. The below code snippet explains the same.

{% highlight c# %}
[C#]

//Load the PDF document

PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");

//Insert a new page in the begining of the document

loadedDocument.Pages.Insert(0);

//Save and close the document

loadedDocument.Save("Output.pdf");

loadedDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}
[VB]

'Load the PDF document

Dim loadedDocument As New PdfLoadedDocument("Input.pdf")

'Insert a new page in the begining of the document

loadedDocument.Pages.Insert(0)

'Save and close the document

loadedDocument.Save("Output.pdf")

loadedDocument.Close(True)



{% endhighlight %}

## Adding margin to the PDF pages

You can add margin to all the PDF pages of the PDF document using the pagesetting property. The following code snippet illustrates the same.

{% highlight c# %}
[C#]

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Set margin for all the pages

document.PageSettings.Margins.All = 10;

//Add a page.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Creates a solid brush.

PdfBrush brush = new PdfSolidBrush(Color.Black);

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 14);

//Draw the text.

graphics.DrawString("Hello world!", font, brush, new PointF(20, 20));

//Save and close the document.

document.Save("Output.pdf");

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}
[VB]

'Create a new PDF document.

Dim document As New PdfDocument()

'Set margin for all the pages

document.PageSettings.Margins.All = 10

'Add a page.

Dim page As PdfPage = document.Pages.Add()

'Create PDF graphics for the page.

Dim graphics As PdfGraphics = page.Graphics

'Create a solid brush.

Dim brush As PdfBrush = New PdfSolidBrush(Color.Black)

'Set the font.

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 14)

'Draw the text.

graphics.DrawString("Hello world!", font, brush, New PointF(20, 20))

'Save the document.

document.Save("Output.pdf")

document.Close(True)



{% endhighlight %}

## Importing pages from an existing document.

Essential PDF allows you to import a page or import a range of pages from one document to the other. The following code sample illustrates how to import a page from an existing document

{% highlight c# %}
[C#]

//Load the PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");

//Create a new PDF document.

PdfDocument document = new PdfDocument();

int startIndex = 0;

int endIndex = loadedDocument.Pages.Count - 1;

//Import all the pages to the new PDF document.

document.ImportPageRange(loadedDocument, startIndex, endIndex);

//Save the document.

document.Save("Output.pdf");

//Close both document instances.

loadedDocument.Close(true);

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}
[VB]

'Load the PDF document.

Dim loadedDocument As New PdfLoadedDocument("Input.pdf")

'Create a new PDF document.

Dim document As New PdfDocument()

Dim startIndex As Integer = 0

Dim endIndex As Integer = loadedDocument.Pages.Count - 1

'Import all the pages to the new PDF document.

document.ImportPageRange(loadedDocument, startIndex, endIndex)

'Save the document.

document.Save("Output.pdf")

'Close both document instances.

loadedDocument.Close(True)

document.Close(True)



{% endhighlight %}

## Rearranging pages in an existing document

You can rearrange the pages in an existing PDF document using ReArrange method. The following code snippet illustrates the same.

{% highlight c# %}
[C#]

//Load the PDF document

PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");

//Rearrange the page by index

loadedDocument.Pages.ReArrange(new int[] {1, 0});

//Save and close the document

loadedDocument.Save("Output.pdf");

loadedDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}
[VB]

'Load the PDF document

Dim loadedDocument As New PdfLoadedDocument("Input.pdf")

'Rearrange the page by index

loadedDocument.Pages.ReArrange(New Integer() {1, 0})

'Save and close the document

loadedDocument.Save("Output.pdf")

loadedDocument.Close(True)



{% endhighlight %}

## Removing pages from a document

You can remove the pages from the existing PDF document as shown in the below code snippet. 

{% highlight c# %}
[C#]

//Load the PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");



//Remove the first page in the PDF document

loadedDocument.Pages.RemoveAt(0);

//Save the document.

loadedDocument.Save("Output.pdf");

//Close the document.            loadedDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}
[VB]

'Load the PDF document.

Dim loadedDocument As New PdfLoadedDocument("Input.pdf")

'Remove the first page in the PDF document

loadedDocument.Pages.RemoveAt(0)

'Save the document.

loadedDocument.Save("Output.pdf")

'Close the document.

loadedDocument.Close(True)



{% endhighlight %}

## Rotating a PDF page

You can rotate a particular PDF page in the PDF document, using the following code snippet. 

{% highlight c# %}
[C#]

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a section.

PdfSection section = document.Sections.Add();

//Rotate a section/page

section.PageSettings.Rotate = PdfPageRotateAngle.RotateAngle90;

PdfPage page = section.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Create a solid brush.

PdfBrush brush = new PdfSolidBrush(Color.Black);

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 14);

//Draws the text.

graphics.DrawString("Rotated by 90 degree", font, brush, new PointF(20, 20));

//Save the document.

document.Save("Output.pdf");

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}
[VB]

'Create a new PDF document.

Dim document As New PdfDocument()

'Add a section.

Dim section As PdfSection = document.Sections.Add()

'Rotate a section/page

section.PageSettings.Rotate = PdfPageRotateAngle.RotateAngle90

Dim page As PdfPage = section.Pages.Add()

'Create PDF graphics for the page.

Dim graphics As PdfGraphics = page.Graphics

'Create a solid brush.

Dim brush As PdfBrush = New PdfSolidBrush(Color.Black)

'Set the font.

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 14)

'Draw the text.

graphics.DrawString("Rotated by 90 degree", font, brush, New PointF(20, 20))

'Save the document.

document.Save("Output.pdf")

document.Close(True)





{% endhighlight %}

## Splitting a PDF file to individual pages

Essential PDF allows to split the pages of an existing PDF document into multiple individual PDF documents. The following code snippet explains the same.

{% highlight c# %}
[C#]

//Load document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument("OutputE.pdf");

//Sets pattern.

const string destFilePattern = "Output" + "{0}.pdf";

//Split the pages into separate documents.

loadedDocument.Split(destFilePattern);

//close the document

loadedDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}
[VB]

'Load document.

Dim loadedDocument As New PdfLoadedDocument("OutputE.pdf")

'Sets pattern.

Const destFilePattern As String = "Output" + "{0}.pdf"

'Split the pages into separate documents.

loadedDocument.Split(destFilePattern)

'close the document

loadedDocument.Close(True)



{% endhighlight %}

