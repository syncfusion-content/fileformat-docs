---
title: Working with PDF templates
description: This section explains how to create a PDF template is a drawing surface, where contents can be added;
platform: file-formats
control: PDF
documentation: UG
---
# Working with PDF Templates 

A PDF template is a drawing surface, where contents can be added. All the elements that can be added to a PdfPage is supported in PdfTemplate as well. The template in turn can be drawn over the page or can be positioned at any part of the page.

## Creating a new PDF template

The PdfTemplate class can be used to create a new PDF template. You can add contents to the template using graphics property of the PdfTemplate object.

The below code snippet illustrates how to add contents to the PdfTemplate and render into the new PDF page.

{% tabs %}  

{% highlight c# %}


//Create a new PDF document.

PdfDocument pdfDocument = new PdfDocument();

//Add a page to the PDF document.

PdfPage pdfPage = pdfDocument.Pages.Add();

//Create a PDF Template.

PdfTemplate template = new PdfTemplate(100, 50);

//Draw a rectangle on the template graphics 

template.Graphics.DrawRectangle(PdfBrushes.BurlyWood, new System.Drawing.RectangleF(0, 0, 100, 50));

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 14);

PdfBrush brush = new PdfSolidBrush(Color.Black);

//Draw a string using the graphics of the template.

template.Graphics.DrawString("Hello World", font, brush, 5, 5);

//Draw the template on the page graphics of the document.

pdfPage.Graphics.DrawPdfTemplate(template, PointF.Empty);

//Save the document.

pdfDocument.Save("Output.pdf");

//close the document

pdfDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Create a new PDF document.

Dim pdfDocument As New PdfDocument()

'Add a page to the PDF document.

Dim pdfPage As PdfPage = pdfDocument.Pages.Add()

'Create a PDF Template.

Dim template As New PdfTemplate(100, 50)

'Draw a rectangle on the template graphics.

template.Graphics.DrawRectangle(PdfBrushes.BurlyWood, New System.Drawing.RectangleF(0, 0, 100, 50))

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 14)

Dim brush As PdfBrush = New PdfSolidBrush(Color.Black)

'Draw a string using the graphics of the template.

template.Graphics.DrawString("Hello World", font, brush, 5, 5)

'Draw the template on the page graphics of the document.

pdfPage.Graphics.DrawPdfTemplate(template, PointF.Empty)

'Save the document.

pdfDocument.Save("Output.pdf")

'close the document

pdfDocument.Close(True)


{% endhighlight %}

{% endtabs %}  


The below code snippet illustrates how to render the PdfTemplate on an existing PDF document.

{% tabs %}  

{% highlight c# %}


//Load the existing PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);

//Load the page into Pdf document.

PdfLoadedPage LoadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create a PDF Template.

PdfTemplate template = new PdfTemplate(100, 50);

//Draw a rectangle on the template graphics.

template.Graphics.DrawRectangle(PdfBrushes.BurlyWood, new System.Drawing.RectangleF(0, 0, 100, 50));

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 14);

PdfBrush brush = new PdfSolidBrush(Color.Black);

//Draw a string on the graphics of the template.

template.Graphics.DrawString("Hello World", font, brush, 5, 5);

//Draw the template on the page graphics of the document.

LoadedPage.Graphics.DrawPdfTemplate(template, PointF.Empty);

//Save the modified document.

loadedDocument.Save("Output.pdf");

//close the document

loadedDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Load the existing PDF document.

Dim loadedDocument As New PdfLoadedDocument(fileName)

'Load the page into Pdf document.

Dim LoadedPage As PdfLoadedPage = TryCast(loadedDocument.Pages(0), PdfLoadedPage)

'Create a PDF Template.

Dim template As New PdfTemplate(100, 50)

'Draw a rectangle on the template graphics.

template.Graphics.DrawRectangle(PdfBrushes.BurlyWood, New System.Drawing.RectangleF(0, 0, 100, 50))

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 14)

Dim brush As PdfBrush = New PdfSolidBrush(Color.Black)

'Draw a string on the graphics of the template.

template.Graphics.DrawString("Hello World", font, brush, 5, 5)

'Draw the template on the page graphics of the document.

LoadedPage.Graphics.DrawPdfTemplate(template, PointF.Empty)

'Save the modified document.

loadedDocument.Save("Output.pdf")

'close the document

loadedDocument.Close(True)



{% endhighlight %}

{% endtabs %}  

## Creating templates from existing PDF document

Essential PDF supports to create the templates from an existing PDF document page and draw it in on a new PDF document.

The below code illustrates how to create the template from an existing page and draw it in new PDF document.

{% tabs %}  

{% highlight c# %}

//Load the existing PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);

//Load the page

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Create the template from the page.

PdfTemplate template = loadedPage.CreateTemplate();

//Create a new PDF document

PdfDocument document = new PdfDocument();

//Set the document margin

document.PageSettings.SetMargins(2);

//Add the page

PdfPage page = document.Pages.Add();

//Create the graphics

PdfGraphics graphics = page.Graphics;

//Draw the template

graphics.DrawPdfTemplate(template, PointF.Empty,new SizeF(page.Size.Width/2,page.Size.Height));

//Save the new document.

document.Save("output.pdf");

//Close the documents

loadedDocument.Close(true);

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Load the existing PDF document.

Dim loadedDocument As New PdfLoadedDocument(fileName)

'Load the page

Dim loadedPage As PdfLoadedPage = TryCast(loadedDocument.Pages(0), PdfLoadedPage)

'Create the template from the page.

Dim template As PdfTemplate = loadedPage.CreateTemplate()

'Create a new PDF document

Dim document As New PdfDocument()

'Set the document margin

document.PageSettings.SetMargins(2)

'Add the page

Dim page As PdfPage = document.Pages.Add()

'Create the graphics

Dim graphics As PdfGraphics = page.Graphics

'Draw the template

graphics.DrawPdfTemplate(template, PointF.Empty, New SizeF(page.Size.Width \ 2, page.Size.Height))

'Save the new document.

document.Save("output.pdf")

'Close the documents

loadedDocument.Close(True)

document.Close(True)



{% endhighlight %}

{% endtabs %}  



## Working with PdfPageTemplateElement

PdfPageTemplateElement is template element that can be added to any part of the PDF page such as header, footer etc.

The below code illustrates how to add the page template elements in a PDF document.

{% tabs %}  

{% highlight c# %}


//Create a new PDF document.

PdfDocument pdfDocument = new PdfDocument();

//Add a page to the PDF document

PdfPage pdfPage = pdfDocument.Pages.Add();

//Create a header and draw the image.

RectangleF bounds = new RectangleF(0, 0, pdfDocument.Pages[0].GetClientSize().Width, 50);

PdfPageTemplateElement header = new PdfPageTemplateElement(bounds );

PdfImage image = new PdfBitmap(@"Logo.png");

//Draw the image in the header.

header.Graphics.DrawImage(image, new PointF(0, 0), new SizeF(100, 50));

//Add the header at the top.

pdfDocument.Template.Top = header;

//Create a Page template that can be used as footer.

PdfPageTemplateElement footer = new PdfPageTemplateElement(bounds );

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 7);

PdfBrush brush = new PdfSolidBrush(Color.Black);

//Create page number field.

PdfPageNumberField pageNumber = new PdfPageNumberField(font, brush);

//Create page count field.

PdfPageCountField count = new PdfPageCountField(font, brush);

//Add the fields in composite fields.

PdfCompositeField compositeField = new PdfCompositeField(font, brush, "Page {0} of {1}", pageNumber, count);

compositeField.Bounds = footer.Bounds;

//Draw the composite field in footer.

compositeField.Draw(footer.Graphics, new PointF(470, 40));

//Add the footer template at the bottom.

pdfDocument.Template.Bottom = footer;

//Save and close the document.

pdfDocument.Save("Output.pdf");

pdfDocument.Close(true);





{% endhighlight %}

{% highlight vb.net %}


'Create a new PDF document.

Dim pdfDocument As New PdfDocument()

'Add a page to the PDF document.

Dim pdfPage As PdfPage = pdfDocument.Pages.Add()

'Create a header and draw the image.

Dim bounds  As New RectangleF(0, 0, pdfDocument.Pages(0).GetClientSize().Width, 50)

Dim header As New PdfPageTemplateElement(bounds )

Dim image As PdfImage = New PdfBitmap("Logo.jpg")

'Draw the image in the Header.

header.Graphics.DrawImage(image, New PointF(0, 0), New SizeF(100, 50))

'Add the header at the top.

pdfDocument.Template.Top = header

'Create a page template that can be used as footer.

Dim footer As New PdfPageTemplateElement(bounds )

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 7)

Dim brush As PdfBrush = New PdfSolidBrush(Color.Black)

'Create page number field.

Dim pageNumber As New PdfPageNumberField(font, brush)

'Create page count field.

Dim count As New PdfPageCountField(font, brush)

'Add the fields in composite fields.

Dim compositeField As New PdfCompositeField(font, brush, "Page {0} of {1}", pageNumber, count)

compositeField.Bounds = footer.Bounds

'Draw the composite field in footer.

compositeField.Draw(footer.Graphics, New PointF(470, 40))

'Add the footer template at the bottom.

pdfDocument.Template.Bottom = footer

'Save and close the document.

pdfDocument.Save("Output.pdf")

pdfDocument.Close(True)

{% endhighlight %}





{% endtabs %}  

## Creating Document Overlays 

Multiple templates can be drawn over a PDF page, to create a document-overlay. The below code illustrates how to overlay the documents.

{% tabs %} 

{% highlight c# %}


//Load the existing documents

PdfLoadedDocument loadedDocument1 = new PdfLoadedDocument(fileName1);

PdfLoadedDocument loadedDocument2 = new PdfLoadedDocument(fileName2);

//Create the new document

PdfDocument document = new PdfDocument();

PdfPage page = document.Pages.Add();

//Create a template from the first document

PdfPageBase loadedPage = loadedDocument1.Pages[0];

PdfTemplate template = loadedPage.CreateTemplate();

//Draw the loaded template into new document.

page.Graphics.DrawPdfTemplate(template, new PointF(0, 0), new SizeF(500, 700));

// Create a template from the second document

loadedPage = loadedDocument2.Pages[0];

template = loadedPage.CreateTemplate();

//Draw the loaded template into new document.

page.Graphics.DrawPdfTemplate(template, new PointF(10, 10), new SizeF(400, 500));

//Save the new document.

document.Save("output.pdf");

//Close the documents

loadedDocument1.Close(true);

loadedDocument2.Close(true);

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}


'Load the existing documents

Dim loadedDocument1 As New PdfLoadedDocument(fileName1)

Dim loadedDocument2 As New PdfLoadedDocument(fileName2)

'Create the new document

Dim document As New PdfDocument()

Dim page As PdfPage = document.Pages.Add()

'Create a template from the first document 

Dim loadedPage As PdfPageBase = loadedDocument1.Pages(0)

Dim template As PdfTemplate = loadedPage.CreateTemplate()

'Draw the loaded template into new document.

page.Graphics.DrawPdfTemplate(template, New PointF(0, 0), New SizeF(500, 700))

'Create a template from the first document 

loadedPage = loadedDocument2.Pages(0)

template = loadedPage.CreateTemplate()

'Draw the loaded template into new document.

page.Graphics.DrawPdfTemplate(template, New PointF(10, 10), New SizeF(400, 500))

'Save the new document.

document.Save("output.pdf")

'Close the documents

loadedDocument1.Close(True)

loadedDocument2.Close(True)

document.Close(True)



{% endhighlight %}

 {% endtabs %}  