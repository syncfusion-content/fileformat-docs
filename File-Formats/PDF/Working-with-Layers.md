---
title: Working with Layers
description: This section explains adding the layer in the PDF document and the layers refers to section of Content of PDF document
platform: file-formats
control: PDF
documentation: UG
---

# Working with Layers

Layers, also known as Option Content refers to sections of content in a PDF document that can be selectively viewed or hidden by document authors or consumers. This capability is useful in items such as CAD drawings, layered artwork, maps, and multi-language documents.

Essential PDF provides support to create, add and merge the layers into PDF document.

## Adding Layers in a PDF document

Essential PDF allows the users to create a layer in a PDF page using PdfPageLayer class. The below code snippet illustrates how to add the multiple layers in a new PDF document.

{% tabs %} 

{% highlight c# %}


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

 {% endtabs %}  

The below code illustrates how to add the multiple layers in an existing PDF document.

{% tabs %} 

{% highlight c# %}


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

 {% endtabs %}  

## Removing layers from an existing PDF document

You can remove the layers from layer collection, represented by the PdfPageLayerCollection of the loaded page. This is illustrated in the following code sample.

{% tabs %} 

{% highlight c# %}


//Load the existing PDF document

PdfLoadedDocument document = new PdfLoadedDocument("Input.pdf");

//Gets the first page from the document

PdfLoadedPage loadedPage = document.Pages[0] as PdfLoadedPage;

//Get the layer collection

PdfPageLayerCollection layers = loadedPage.Layers;

//Remove the layer

layers.RemoveAt(0);

//Save the document

document.Save("Output.pdf");

//Close the document

document.Close(true);




{% endhighlight %}

{% highlight vb.net %}


'Load the existing PDF document

Dim document As PdfLoadedDocument = New PdfLoadedDocument("Input.pdf")

'Gets the first page from the document

Dim loadedPage As PdfLoadedPage = TryCast(document.Pages(0), PdfLoadedPage)

'Get the layer collection

Dim layers As PdfPageLayerCollection = loadedPage.Layers

'Remove the layer.

layers.RemoveAt(0)

'Save the document.

document.Save("Output.pdf")

'Close the document.

document.Close(True)




{% endhighlight %}

 {% endtabs %}  
 

## Toggling the visibility of layers

The visibility of a layer can be mentioned while creating a new page layer.

The below code illustrates how to toggle the visibility of layers in new PDF document. 

{% tabs %}  

{% highlight c# %}


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

{% endtabs %}  

The following code illustrates how to toggle the visibility of layers in an existing PDF document.

{% tabs %}  

{% highlight c# %}


//Load the existing PDF document

PdfLoadedDocument document = new PdfLoadedDocument("Input.pdf");

//Gets the first layer from the layer collection

PdfLayer layer = document.Layers[0];

//Disable the visibility

layer.Visible = false;

//Save the document

document.Save("Output.pdf");

//Close the document

document.Close(true);

{% endhighlight %}



{% highlight vb.net %}


'Load the existing PDF document

Dim document As PdfLoadedDocument = New PdfLoadedDocument("Input.pdf")

'Get the first layer from the layer collection

Dim layer As PdfLayer = document.Layers(0)

'Disable the visibility

layer.Visible = False

'Save the document

document.Save("Output.pdf")

'Close the document

document.Close(True)


{% endhighlight %}

{% endtabs %}  

## Adding annotation to layer

Essential PDF allows the users to add annotation to layers in the PDF document. Refer to the following code snippet.  

{% tabs %}  

{% highlight c# %}


//Create new PDF document

PdfDocument document = new PdfDocument();

//Add page

PdfPage page = document.Pages.Add();

//Add the layer

PdfLayer layer = document.Layers.Add("Layer");

//Create graphics for layer

PdfGraphics graphics = layer.CreateGraphics(page);

//Draw ellipse

graphics.DrawEllipse(PdfPens.Red, new RectangleF(50, 50, 40, 40));

//Create square annotation

PdfSquareAnnotation annotation = new PdfSquareAnnotation(new RectangleF(200, 260, 50, 50), "Square annotation");

annotation.Color = new PdfColor(Color. Red);

//Set layer to annotation

annotation.Layer = layer;

//Add annotation to the created page

page.Annotations.Add(annotation);

//Save the document

document.Save("Output.pdf");

//Close the document

document.Close(true);




{% endhighlight %}



{% highlight vb.net %}


'Create new PDF document

Dim document As New PdfDocument()

'Add page

Dim page As PdfPage = document.Pages.Add()

'Add the layer

Dim Layer As PdfLayer = document.Layers.Add("Layer")

'Create graphics for layer

Dim graphics As PdfGraphics = Layer.CreateGraphics(page)

'Draw ellipse

graphics.DrawEllipse(PdfPens.Red, New RectangleF(50, 50, 40, 40))

'Create square annotation

Dim annotation As New PdfSquareAnnotation(New RectangleF(200, 260, 50, 50), "Square annotation")

annotation.Color = New PdfColor(Color.Red)

'Set layer to annotation

annotation.Layer = Layer

'Add annotation to the created page

page.Annotations.Add(annotation)

'Save the document

document.Save("Output.pdf")

'Close the document

document.Close(True)



{% endhighlight %}

{% endtabs %}  

The following code illustrates how to add annotation to the layers in an existing PDF document.

{% tabs %}  

{% highlight c# %}


//Load the existing PDF document

PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");

//Gets the first page from the document

PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Add the layer

PdfLayer Layer = loadedDocument.Layers.Add("Layer");

//Create graphics for layer

PdfGraphics graphics = Layer.CreateGraphics(loadedPage);

//Draw ellipse

graphics.DrawEllipse(PdfPens.Red, new RectangleF(50, 50, 40, 40));

//Create square annotation

PdfSquareAnnotation annotation = new PdfSquareAnnotation(new RectangleF(200, 260, 50, 50), "Square annotation");

annotation.Color = new PdfColor(Color.Red);

//Set layer to annotation

annotation.Layer = Layer;

//Add annotation to the created page

loadedPage.Annotations.Add(annotation);

//Save the document

loadedDocument.Save("Output.pdf");

//Close the document

loadedDocument.Close(true);


{% endhighlight %}



{% highlight vb.net %}


'Load the existing PDF document

Dim loadedDocument As New PdfLoadedDocument("Input.pdf")

'Gets the first page from the document

Dim loadedPage As PdfLoadedPage = TryCast(loadedDocument.Pages(0), PdfLoadedPage)

'Add the layer

Dim Layer As PdfLayer = loadedDocument.Layers.Add("Layer")

'Create graphics for layer

Dim graphics As PdfGraphics = Layer.CreateGraphics(loadedPage)

'Draw ellipse

graphics.DrawEllipse(PdfPens.Red, New RectangleF(50, 50, 40, 40))

'Create square annotation

Dim annotation As New PdfSquareAnnotation(New RectangleF(200, 260, 50, 50), "Square annotation")

annotation.Color = New PdfColor(Color.Red)

'Set layer to annotation

annotation.Layer = Layer

'Add annotation to the created page

loadedPage.Annotations.Add(annotation)

'Save the document

loadedDocument.Save("Output.pdf")

'Close the document

loadedDocument.Close(True)



{% endhighlight %}

{% endtabs %}  