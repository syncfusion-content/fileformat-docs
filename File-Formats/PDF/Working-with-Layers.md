---
title: Working with Layers | Syncfusion
description: This section explains adding the layer in the PDF document and the layers refers to section of Content of PDF document
platform: file-formats
control: PDF
documentation: UG
---

# Working  with  Layers 

Layers, also known as Option Content refers to sections of content in a PDF document that can be selectively viewed or hidden by document authors or consumers. This capability is useful in items such as CAD drawings, layered artwork, maps, and multi-language documents.

Essential PDF provides support to create, add and merge the layers into PDF document.

## Adding Layers in a PDF document

Essential PDF allows the users to create a layer in a PDF page using [PdfPageLayer](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfPageLayer.html) class. The below code example illustrates how to add the multiple layers in a new PDF document.

{% tabs %} 

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Create PDF document.
PdfDocument document = new PdfDocument();
//Add the page. 
PdfPage page = document.Pages.Add();

//Add the first layer.
PdfPageLayer layer = page.Layers.Add("Layer1");
PdfGraphics graphics = layer.Graphics;
graphics.TranslateTransform(100, 60);
//Draw arc. 
PdfPen pen = new PdfPen(Syncfusion.Drawing.Color.Red, 50);
RectangleF bounds = new RectangleF(0, 0, 50, 50);
graphics.DrawArc(pen, bounds, 360, 360);

//Add another layer on the page.
PdfPageLayer layer2 = page.Layers.Add("Layer2");
graphics = layer2.Graphics;
graphics.TranslateTransform(100, 180);
//Draw ellipse. 
graphics.DrawEllipse(pen, bounds);

//Save and close the document.
MemoryStream stream = new MemoryStream();
document.Save(stream);
stream.Position = 0;
//Close the document.
document.Close(true);
//Defining the ContentType for PDF file.
string contentType = "application/pdf";
//Define the file name.
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name.
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Create PDF document.
PdfDocument document = new PdfDocument();
//Add the page. 
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Create PDF document.
Dim document As New PdfDocument()
'Add the page. 
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Layer/Adding-layers-in-a-PDF-document).

The below code illustrates how to add the multiple layers in an existing PDF document using [PdfPageLayer](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfPageLayer.html) class. 

{% tabs %} 

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Load the PDF document
FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);
//Get first page from document
PdfLoadedPage loadedPage = loadedDocument.Pages[0] as PdfLoadedPage;

//Add the first layer.
PdfPageLayer layer = loadedPage.Layers.Add("Layer1");
PdfGraphics graphics = layer.Graphics;
graphics.TranslateTransform(100, 60);
//Draw arc. 
PdfPen pen = new PdfPen(Syncfusion.Drawing.Color.Gray, 50);
RectangleF bounds = new RectangleF(0, 0, 50, 50);
graphics.DrawArc(pen, bounds, 360, 360);

//Add another layer on the page.
PdfPageLayer layer2 = loadedPage.Layers.Add("Layer2");
graphics = layer2.Graphics;
graphics.TranslateTransform(100, 180);
//Draw ellipse.
graphics.DrawEllipse(pen, bounds);

//Save and close the document
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);
stream.Position = 0;
//Close the document.
loadedDocument.Close(true);
//Defining the ContentType for pdf file.
string contentType = "application/pdf";
//Define the file name.
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name.
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Load the existing PDF document.
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);
//Get first page from document
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Load the existing PDF document.
Dim loadedDocument As New PdfLoadedDocument(fileName)
'Get first page from document
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Layer/Add-the-multiple-layers-in-an-existing-PDF-document).

## Adding annotation to layer

Essential PDF allows the users to add different types of [Annotation](https://help.syncfusion.com/file-formats/pdf/working-with-annotations) to layers in the PDF document using [Layer](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfAnnotation.html#Syncfusion_Pdf_Interactive_PdfAnnotation_Layer) property in [PdfAnnotation](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfAnnotation.html) class. The following code example illustrates the same. 

{% tabs %}  

{% highlight c# tabtitle="C# [Cross-platform]" %}

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
annotation.Color = new PdfColor(Syncfusion.Drawing.Color.Red);
//Set layer to annotation
annotation.Layer = layer;
//Add annotation to the created page
page.Annotations.Add(annotation);

//Save and close the document
MemoryStream stream = new MemoryStream();
document.Save(stream);
stream.Position = 0;
//Close the document
document.Close(true);
//Defining the ContentType for PDF file
string contentType = "application/pdf";
//Define the file name.
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Layer/Adding-annotation-to-layer-in-the-PDF-document).

The following code illustrates how to add annotation to the layers in an existing PDF document.

{% tabs %}  

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Load the PDF document
FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);
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
annotation.Color = new PdfColor(Syncfusion.Drawing.Color.Red);
//Set layer to annotation
annotation.Layer = Layer;
//Add annotation to the created page
loadedPage.Annotations.Add(annotation);

//Save and close the document
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);
stream.Position = 0;
//Close the document
loadedDocument.Close(true);
//Defining the ContentType for PDF file
string contentType = "application/pdf";
//Define the file name
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Layer/Add-annotation-to-the-layer-in-an-existing-PDF-document).

## Nested Layers

Essential PDF allows users to add nested layers in the PDF document by adding child layer to parent layer using [Layers](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfLayer.html#Syncfusion_Pdf_PdfLayer_Layers) property of [PdfLayer](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfLayer.html) class. Refer to the following code example. 

{% tabs %} 

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Create the PDF document
PdfDocument document = new PdfDocument();
//Add the page
PdfPage page = document.Pages.Add();

//Add the parent layer
PdfLayer layer = document.Layers.Add("Layer1");
PdfGraphics graphics = layer.CreateGraphics(page);
graphics.TranslateTransform(100, 60);

//Draw an arc
PdfPen pen = new PdfPen(Color.Red, 50);
RectangleF bounds = new RectangleF(0, 0, 50, 50);
graphics.DrawArc(pen, bounds, 360, 360);

//Add the child layer
PdfLayer layer2 = layer.Layers.Add("Layer2");
graphics = layer2.CreateGraphics(page);
graphics.TranslateTransform(100, 180);
//Draw an ellipse
graphics.DrawEllipse(pen, bounds);

//Creating the stream object
MemoryStream stream = new MemoryStream();
//Save the document as stream
document.Save(stream);
//If the position is not set to '0', the PDF will be empty
stream.Position = 0;
//Close the document
document.Close(true);
//Defining the ContentType for PDF file
string contentType = "application/pdf";
//Define the file name
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name
return File(stream, contentType, fileName);

{% endhighlight %}  

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Create the PDF document
PdfDocument document = new PdfDocument();
//Add the page
PdfPage page = document.Pages.Add();

//Add the parent layer
PdfLayer layer = document.Layers.Add("Layer1");
PdfGraphics graphics = layer.CreateGraphics(page);
graphics.TranslateTransform(100, 60);

//Draw an arc
PdfPen pen = new PdfPen(Color.Red, 50);
RectangleF bounds = new RectangleF(0, 0, 50, 50);
graphics.DrawArc(pen, bounds, 360, 360);

//Add the child layer
PdfLayer layer2 = layer.Layers.Add("Layer2");
graphics = layer2.CreateGraphics(page);
graphics.TranslateTransform(100, 180);
//Draw an ellipse
graphics.DrawEllipse(pen, bounds);

//Save the document
document.Save("Output.pdf");
//Close the document
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Create the PDF document
Dim document As New PdfDocument()
'Add the page
Dim page As PdfPage = document.Pages.Add()

'Add the parent layer
Dim layer As PdfLayer = document.Layers.Add("Layer1")
Dim graphics As PdfGraphics = layer.CreateGraphics(page)
graphics.TranslateTransform(100, 60)

'Draw an arc
Dim pen As New PdfPen(Color.Red, 50)
Dim bounds As New RectangleF(0, 0, 50, 50)
graphics.DrawArc(pen, bounds, 360, 360)

'Add the child layer
Dim layer2 As PdfLayer = layer.Layers.Add("Layer2")
graphics = layer2.CreateGraphics(page)
graphics.TranslateTransform(100, 180)
'Draw an ellipse
graphics.DrawEllipse(pen, bounds)

'Save the document
document.Save("Output.pdf")
'Close the document
document.Close(True)

{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Layer/Add-nested-layers-in-the-PDF-document).

## Removing layers from an existing PDF document

You can remove the layers using [RemoveAt](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfPageLayerCollection.html#Syncfusion_Pdf_PdfPageLayerCollection_RemoveAt_System_Int32_) method or [Remove](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfPageLayerCollection.html#Syncfusion_Pdf_PdfPageLayerCollection_Remove_System_String_) method from layer collection, represented by the [PdfPageLayerCollection](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfPageLayerCollection.html) of the [PdfLoadedPage](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfLoadedPage.html). This is illustrated in the following code sample.

{% tabs %} 

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Load the PDF document
FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument document = new PdfLoadedDocument(docStream);
//Gets the first page from the document
PdfLoadedPage loadedPage = document.Pages[0] as PdfLoadedPage;

//Get the layer collection
PdfPageLayerCollection layers = loadedPage.Layers;
//Remove the layer
layers.RemoveAt(0);

//Save and close the document
MemoryStream stream = new MemoryStream();
document.Save(stream);
stream.Position = 0;
//Close the document
document.Close(true);
//Defining the ContentType for pdf file.
string contentType = "application/pdf";
//Define the file name.
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name.
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Load the existing PDF document
Dim document As PdfLoadedDocument = New PdfLoadedDocument("Input.pdf")
'Gets the first page from the document
Dim loadedPage As PdfLoadedPage = TryCast(document.Pages(0), PdfLoadedPage)

'Get the layer collection
Dim layers As PdfPageLayerCollection = loadedPage.Layers
'Remove the layer.
layers.RemoveAt(0)

'Save the document
document.Save("Output.pdf")
'Close the document
document.Close(True)

{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Layer/Removing-layers-from-an-existing-PDF-document).
 
## Flattening the layers in an existing PDF document

You can flatten a layer in a PDF document by removing it from the [PdfDocumentLayerCollection](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfDocumentLayerCollection.html) using [RemoveAt](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfDocumentLayerCollection.html#Syncfusion_Pdf_PdfDocumentLayerCollection_RemoveAt_System_Int32_) method or [Remove](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfDocumentLayerCollection.html#Syncfusion_Pdf_PdfDocumentLayerCollection_Remove_System_String_) method. The following code snippet explains this.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Load the existing PDF document
FileStream inputStream = new FileStream("Layers.pdf", FileMode.Open);
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(inputStream);

//Get the layer collection
PdfDocumentLayerCollection layers = loadedDocument.Layers;
//Flatten a layer in the PDF document
layers.RemoveAt(0);

//Saving the PDF to the MemoryStream
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);
//Set the position as '0'
stream.Position = 0;
//Download the PDF document in the browser
FileStreamResult fileStreamResult = new FileStreamResult(stream, "application/pdf");
fileStreamResult.FileDownloadName = "Output.pdf";
return fileStreamResult;

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Load the existing PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Layers.pdf");

//Get the layer collection
PdfDocumentLayerCollection layers = loadedDocument.Layers;
//Flatten a layer in the PDF document
layers.RemoveAt(0);

//Save the PDF document
loadedDocument.Save("Output.pdf");
//Close the instance of PdfLoadedDocument
loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Load the existing PDF document
Dim loadedDocument As PdfLoadedDocument = New PdfLoadedDocument("Layers.pdf")

'Get the layer collection
Dim layers As PdfDocumentLayerCollection = loadedDocument.Layers
'Flatten a layer in the PDF document
layers.RemoveAt(0)

'Save the PDF document
loadedDocument.Save("Output.pdf")
'Close the instance of PdfLoadedDocument
loadedDocument.Close(True)

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Layer/Flattening-the-layers-in-an-existing-PDF-document/).

## Toggling the visibility of layers

The visibility of a layer can be mentioned while creating a new page layer using [Add](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfPageLayerCollection.html#Syncfusion_Pdf_PdfPageLayerCollection_Add_System_String_System_Boolean_) method in [PdfPageLayerCollection](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfPageLayerCollection.html) class by specifying the *visibility* as **true**.

The below code illustrates how to toggle the visibility of layers in new PDF document. 

{% tabs %}  

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Create the document
PdfDocument document = new PdfDocument();
//Create a page
PdfPage page = document.Pages.Add();

//Add the first layer and enable the visibility.
PdfPageLayer layer = page.Layers.Add("Layer1", true);
PdfGraphics graphics = layer.Graphics;
graphics.TranslateTransform(100, 60);

//Draw Arc
PdfPen pen = new PdfPen(Syncfusion.Drawing.Color.Red, 50);
RectangleF bounds = new RectangleF(0, 0, 50, 50);
graphics.DrawArc(pen, bounds, 360, 360);

//Add another layer on the page and disable the visibility.
PdfPageLayer layer2 = page.Layers.Add("Layer2", false);
graphics = layer2.Graphics;
graphics.TranslateTransform(100, 180);
//Draw ellipse
graphics.DrawEllipse(pen, bounds);

//Save and close the document
MemoryStream stream = new MemoryStream();
document.Save(stream);
stream.Position = 0;
//Close the document
document.Close(true);
//Defining the content type for PDF file
string contentType = "application/pdf";
//Define the file name
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

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

//Close the document.
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Create the document
Dim document As New PdfDocument()
'Create a page
Dim page As PdfPage = document.Pages.Add()

'Add the first layer and enable the visibility.
Dim layer As PdfPageLayer = page.Layers.Add("Layer1", True)
Dim graphics As PdfGraphics = layer.Graphics
graphics.TranslateTransform(100, 60)

'Draw Arc
Dim pen As New PdfPen(System.Drawing.Color.Red, 50)
Dim bounds As New RectangleF(0, 0, 50, 50)
graphics.DrawArc(pen, bounds, 360, 360)

'Add another layer on the page and disable the visibility.
Dim layer2 As PdfPageLayer = page.Layers.Add("Layer2", False)
graphics = layer2.Graphics
graphics.TranslateTransform(100, 180)
'Draw ellipse
graphics.DrawEllipse(pen, bounds)

'Save the document.
document.Save("Sample.pdf")
'Close the document
document.Close(True)

{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Layer/Toggle-the-visibility-of-layers-in-new-PDF-document).

The following code illustrates how to toggle the visibility of layers in an existing PDF document by disabling the [Visible](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfLayer.html#Syncfusion_Pdf_PdfLayer_Visible) property of the [PdfLayer](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfLayer.html) class.

{% tabs %}  

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Load the PDF document
FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument document = new PdfLoadedDocument(docStream);

//Gets the first layer from the layer collection
PdfLayer layer = document.Layers[0];
//Disable the visibility
layer.Visible = false;

//Save and close the document
MemoryStream stream = new MemoryStream();
document.Save(stream);
stream.Position = 0;
//Close the document
document.Close(true);
//Defining the content type for PDF file.
string contentType = "application/pdf";
//Define the file name
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Layer/Toggle-the-visibility-of-layers-in-an-existing-PDF).

## Lock or Unlock layers

The layers can be locked or unlocked while creating a new layer in a PDF document by enabling or disabling the [Locked](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfLayer.html#Syncfusion_Pdf_PdfLayer_Locked) property in [PdfLayer](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfLayer.html) class.  

The following code sample shows how to add a lock state to the layer in a new PDF document.
 
{% tabs %}  

{% highlight c# tabtitle="C# [Cross-platform]" %}	

//Creating a new PDF document. 
PdfDocument document = new PdfDocument();
//Adding a new page to the PDF document.
PdfPage page = document.Pages.Add();

//Create a layer.
PdfLayer layer = document.Layers.Add("Layer");
//Set a lock state.  
layer.Locked = true;

//Create graphics for a layer.
PdfGraphics graphics = layer.CreateGraphics(page);
//Draw ellipse.
graphics.DrawEllipse(PdfPens.Red, new RectangleF(50, 50, 40, 40));

//Creating the stream object.
MemoryStream stream = new MemoryStream();
//Save the document into stream.
document.Save(stream);
//If the position is not set to '0,' then the PDF will be empty.
stream.Position = 0;
//Close the document.
document.Close(true);
//Defining the content type for a PDF file.
string contentType = "application/pdf";
//Define the file name.
string fileName = "Output.pdf";
//Creates a FileContentResult object by using the file contents, content type, and file name.
return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Creating a new PDF document. 
PdfDocument document = new PdfDocument();
//Adding a new page to the PDF document. 
PdfPage page = document.Pages.Add();

//Create a layer.
PdfLayer layer = document.Layers.Add("Layer");
//Set a lock state.  
layer.Locked = true;

//Create graphics for a layer.
PdfGraphics graphics = layer.CreateGraphics(page);
//Draw ellipse.
graphics.DrawEllipse(PdfPens.Red, new RectangleF(50, 50, 40, 40));

//Save the PDF document.
document.Save("Output.pdf");
//Close the PDF document.
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Creating a new PDF document. 
Dim document As PdfDocument =  New PdfDocument() 
'Adding a new page to the PDF document. 
Dim page As PdfPage =  document.Pages.Add() 
 
'Create a layer. 
Dim layer As PdfLayer =  document.Layers.Add("Layer") 

'Set a lock state.
layer.Locked = True
 
'Create graphics for a layer.
Dim graphics As PdfGraphics =  layer.CreateGraphics(page) 
'Draw ellipse.
graphics.DrawEllipse(PdfPens.Red,New RectangleF(50,50,40,40))
 
'Save the PDF document.
document.Save("Output.pdf")
'Close the PDF document.
document.Close(True)

{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Layer/Add-a-lock-state-to-the-layer-in-a-new-PDF-document).

## Removing the layer with its graphical content

The Syncfusion PDF library allows users to remove layers from PDF documents, and we can also remove the graphical content of layers upto n layer recursively.
We can remove  layers from the layer collection, represented by the ['PdfPageLayerCollection'](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfPageLayerCollection.html) of the loaded page by mentioning only the index ['RemoveAt(0)'](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfDocumentLayerCollection.html#Syncfusion_Pdf_PdfDocumentLayerCollection_Remove_System_String_). We can also remove the graphic content of the layer by using ['RemoveAt(0, true)'](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfDocumentLayerCollection.html#Syncfusion_Pdf_PdfDocumentLayerCollection_RemoveAt_System_Int32_System_Boolean_) method from the layer collection by mentioning the index and enabling the removeGraphicalContent parameter.

This is illustrated in the following code sample.

{% tabs %}  

{% highlight c# tabtitle="C# [Cross-platform]" %}

//PDF doesn't support removing the layer with its graphical content in C#/.NET cross platforms. 

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Load the existing PDF document.
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Layers.pdf");

//Get the layer collection.
PdfDocumentLayerCollection layers = loadedDocument.Layers;
if (layers?.Count > 0)
{
    if (layers[0].Layers.Count > 0)
    {
        //Remove the first child layer with graphical content.
        layers[0].Layers.RemoveAt(0, true);
    }
}

//Save the PDF document.
loadedDocument.Save("Output.pdf");
//Close the instance of PdfLoadedDocument.
loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Load the existing PDF document.
Dim loadedDocument As PdfLoadedDocument = New PdfLoadedDocument("Output.pdf")

'Get the layer collection.
Dim layers As PdfDocumentLayerCollection = loadedDocument.Layers

If layers?.Count > 0 Then
    If layers(0).Layers.Count > 0 Then
        'Remove the first child layer with graphical content.
        layers(0).Layers.RemoveAt(0, True)
    End If
End If

'Save the PDF document.
loadedDocument.Save("Output.pdf")
'Close the instance of PdfLoadedDocument.
loadedDocument.Close(True)

{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Layer/Removing-the-layer-with-its-graphical-content).