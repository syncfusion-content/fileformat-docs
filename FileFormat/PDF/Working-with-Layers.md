---
layout: Post
title: Working with Layers
description: Layers refers to section of Content of PDF document: PdfPageLayer
platform: FileFormat
control: PDF
documentation: UG
---
# 

# Working with Layers

Layers, also known as Option Content refers to sections of content in a PDF document that can be selectively viewed or hidden by document authors or consumers. This capability is useful in items such as CAD drawings, layered artwork, maps, and multi-language documents.

Essential PDF provides support to create, add and merge the layers into PDF document.

## Adding Layers in a PDF document

Essential PDF allows the users to create a layer in a PDF page using PdfPageLayer class. The below code snippet illustrates how to add the multiple layers in a new PDF document.

{% highlight c# %}
C#:

//Create PDF document.

PdfDocument document = new PdfDocument();

PdfPage page = document.Pages.Add();

//Add the first layer.

PdfPageLayer layer = page.Layers.Add("Layer1");

PdfGraphics graphics = layer.Graphics;

graphics.TranslateTransform(100, 60);

//Draw arc.

PdfPen pen = new PdfPen(System.Drawing.Color.Red, 50);

RectangleF bounds = new RectangleF(0, 0, 50, 50);

graphics.DrawArc(pen, bounds, 360, 360);

//Add another layer on the page.

PdfPageLayer layer2 = page.Layers.Add("Layer2");

graphics = layer2.Graphics;

graphics.TranslateTransform(100, 180);

//Draw ellipse.

graphics.DrawEllipse(pen, bounds);

//Save the document.

document.Save("Sample.pdf");

//Close the document

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}
VB:

'Create PDF document.

Dim document As New PdfDocument()

Dim page As PdfPage = document.Pages.Add()

'Add the first layer.

Dim layer As PdfPageLayer = page.Layers.Add("Layer1")

Dim graphics As PdfGraphics = layer.Graphics

graphics.TranslateTransform(100, 60)

'Draw arc.

Dim pen As New PdfPen(System.Drawing.Color.Red, 50)

Dim bounds As New RectangleF(0, 0, 50, 50)

graphics.DrawArc(pen, bounds, 360, 360)

'Add another layer on the page.

Dim layer2 As PdfPageLayer = page.Layers.Add("Layer2")

graphics = layer2.Graphics

graphics.TranslateTransform(100, 180)

'Draw ellipse.

graphics.DrawEllipse(pen, bounds)

'Save the document.

document.Save("Sample.pdf")

'Close the document

document.Close(True)



{% endhighlight %}

The below code illustrates how to add the multiple layers in an existing PDF document.

{% highlight c# %}
C#:

//Load the existing PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Add the first layer.

PdfPageLayer layer = loadedPage.Layers.Add("Layer1");

PdfGraphics graphics = layer.Graphics;

graphics.TranslateTransform(100, 60);

//Draw arc.

PdfPen pen = new PdfPen(System.Drawing.Color.Gray, 50);

RectangleF bounds = new RectangleF(0, 0, 50, 50);

graphics.DrawArc(pen, bounds, 360, 360);

//Add another layer on the page.

PdfPageLayer layer2 = loadedPage.Layers.Add("Layer2");

graphics = layer2.Graphics;

graphics.TranslateTransform(100, 180);

//Draw ellipse.

graphics.DrawEllipse(pen, bounds);

//Save the document.

loadedDocument.Save("Output.pdf");

//Close the document

loadedDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}
VB:

'Load the existing PDF document.

Dim loadedDocument As New PdfLoadedDocument(fileName)

Dim loadedPage As PdfLoadedPage = TryCast(loadedDocument.Pages(0), PdfLoadedPage)

'Add the first layer.

Dim layer As PdfPageLayer = loadedPage.Layers.Add("Layer1")

Dim graphics As PdfGraphics = layer.Graphics

graphics.TranslateTransform(100, 60)

'Draw arc.

Dim pen As New PdfPen(System.Drawing.Color.Gray, 50)

Dim bounds As New RectangleF(0, 0, 50, 50)

graphics.DrawArc(pen, bounds, 360, 360)

'Add another layer on the page.

Dim layer2 As PdfPageLayer = loadedPage.Layers.Add("Layer2")

graphics = layer2.Graphics

graphics.TranslateTransform(100, 180)

'Draw ellipse.

graphics.DrawEllipse(pen, bounds)

'Save the document.

loadedDocument.Save("Output.pdf")

'Close the document

loadedDocument.Close(True)



{% endhighlight %}

## Toggling the visibility of layers

The visibility of a layer can be mentioned while creating a new page layer.

The below code illustrates how to toggle the visibility of layers in new PDF document. 

{% highlight c# %}
C#:

//Create the document

PdfDocument document = new PdfDocument();

//Create a page

PdfPage page = document.Pages.Add();

//Add the first layer and enable the visibility.

PdfPageLayer layer = page.Layers.Add("Layer1",true);

PdfGraphics graphics = layer.Graphics;

graphics.TranslateTransform(100, 60);

//Draw Arc.

PdfPen pen = new PdfPen(System.Drawing.Color.Red, 50);

RectangleF bounds = new RectangleF(0, 0, 50, 50);

graphics.DrawArc(pen, bounds, 360, 360);

//Add another layer on the page and disable the visibility.

PdfPageLayer layer2 = page.Layers.Add("Layer2",false);

graphics = layer2.Graphics;

graphics.TranslateTransform(100, 180);

//Draw ellipse.

graphics.DrawEllipse(pen, bounds);

//Save the document.

document.Save("Sample.pdf");

//close the document

document.Close(true);



{% endhighlight %}



{% highlight vb.net %}
VB:

'Create the document

Dim document As New PdfDocument()

'Create a page

Dim page As PdfPage = document.Pages.Add()

'Add the first layer and enable the visibility.

Dim layer As PdfPageLayer = page.Layers.Add("Layer1", True)

Dim graphics As PdfGraphics = layer.Graphics

graphics.TranslateTransform(100, 60)

'Draw Arc.

Dim pen As New PdfPen(System.Drawing.Color.Red, 50)

Dim bounds As New RectangleF(0, 0, 50, 50)

graphics.DrawArc(pen, bounds, 360, 360)

'Add another layer on the page and disable the visibility.

Dim layer2 As PdfPageLayer = page.Layers.Add("Layer2", False)

graphics = layer2.Graphics

graphics.TranslateTransform(100, 180)

'Draw ellipse.

graphics.DrawEllipse(pen, bounds)

'Save the document.

document.Save("Sample.pdf")

'close the document

document.Close(True)



{% endhighlight %}

