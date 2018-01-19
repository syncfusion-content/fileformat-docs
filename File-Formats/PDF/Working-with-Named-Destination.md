---
title: Working with named destination
description: This section explains how to add, modify and remove named destination from the PDF document
platform: file-formats
control: PDF
documentation: UG
---
# Working with Named Destination

Essential PDF provides support to add, remove and modify the named destination in the PDF document. When you open a PDF file in a web browser, the first page of the PDF file will be shown by default. By adding a named destination, you can open the PDF with the desired location and magnification. The following link example shows how to open a PDF document with named destination in a web page.

Another example that uses "nameddest" parameter in URL:

e.g. [http://www.syncfusion.com/downloads/support/directtrac/general/pd/mydocument-1524150305.pdf#nameddest=Chapter3](http://www.syncfusion.com/downloads/support/directtrac/general/pd/mydocument-1524150305.pdf#nameddest=Chapter3)

**Points to remembers:**

* Individual parameters, together with their values (separated by & or #), can be no greater than 32 characters in length.
* You cannot use the reserved characters =, #, and &. There is no way to escape these special characters.

## Adding Named Destination to a PDF document

The following code example shows how to add named destination in a new PDF document.

{% tabs %}  

{% highlight c# %}

//Create a new PDF document.
PdfDocument doc = new PdfDocument();
//Add a page to the document.
PdfPage page = doc.Pages.Add();
//Create an instance for named destination.
PdfNamedDestination destination = new PdfNamedDestination("TOC");
destination.Destination = new PdfDestination(page);
//Set the location
destination.Destination.Location = new PointF(0, 500);
//Set zoom factor to 400 percentage
destination.Destination.Zoom = 4;
doc.NamedDestinationCollection.Add(destination);
//Draw the text.
page.Graphics.DrawString("Hello World!!", new PdfStandardFont(PdfFontFamily.Helvetica, 10), PdfBrushes.Black, new PointF(0, 500));
//Save the document.
doc.Save("Output.pdf");
//Close the document.
doc.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document.
Dim doc As New PdfDocument()
'Add a page to the document.
Dim page As PdfPage = doc.Pages.Add()
'Create an instance for named destination.
Dim destination As New PdfNamedDestination("TOC")
destination.Destination = New PdfDestination(page)
'Set the location
destination.Destination.Location = New PointF(0, 500)
'Set zoom factor to 400 percentage
destination.Destination.Zoom = 4
doc.NamedDestinationCollection.Add(destination)
'Draw the text.
page.Graphics.DrawString("Hello World!!", New PdfStandardFont(PdfFontFamily.Helvetica, 10), PdfBrushes.Black, New PointF(0, 500))
'Save the document.
doc.Save("Output.pdf")
'Close the document.
doc.Close(True)

{% endhighlight %}

{% endtabs %}  

## Adding Named Destination to an existing PDF document

The following code example shows how to add named destination in an existing PDF document.

{% tabs %} 

{% highlight c# %}

//Load the PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");
//Get the first page of the document
PdfPageBase page = loadedDocument.Pages[0];
//Create an instance for named destination.
PdfNamedDestination destination = new PdfNamedDestination("TOC");
destination.Destination = new PdfDestination(page);
//Set the location
destination.Destination.Location = new PointF(0, 500);
//Set zoom factor to 400 percentage
destination.Destination.Zoom = 4;
loadedDocument.NamedDestinationCollection.Add(destination);
//Save the document
loadedDocument.Save("Output.pdf");
//Close the document
loadedDocument.Close(true);


{% endhighlight %}

{% highlight vb.net %}

'Load the PDF document
Dim loadedDocument As New PdfLoadedDocument("Input.pdf")
'Get the first page of the document
Dim page As PdfPageBase = loadedDocument.Pages(0)
'Create an instance for named destination.
Dim destination As New PdfNamedDestination("TOC")
destination.Destination = New PdfDestination(page)
'Set the location
destination.Destination.Location = New PointF(0, 500)
'Set zoom factor to 400 percentage
destination.Destination.Zoom = 4
loadedDocument.NamedDestinationCollection.Add(destination)
'Save the document
loadedDocument.Save("Output.pdf")
'Close the document
loadedDocument.Close(True)

{% endhighlight %}

 {% endtabs %}  

## Removing/Modifying the named destination

You can add margin to all the PDF pages of the PDF document using the PageSettings property. The following code snippet illustrates the same.

{% tabs %}  

{% highlight c# %}

//Load the PDF document
PdfLoadedDocument lDoc = new PdfLoadedDocument("Sample.pdf");
//Get the named destination collection
PdfNamedDestinationCollection destinationCollection = lDoc.NamedDestinationCollection;
//Remove the named destination by title
destinationCollection.Remove("TOC");
            
//Modify the exiting named destination
PdfNamedDestination destination = destinationCollection[0];
destination.Title = "POC";
            
//Save the document
lDoc.Save("Output.pdf");
//Close the document
lDoc.Close(true);


{% endhighlight %}

{% highlight vb.net %}

'Load the PDF document
Dim lDoc As New PdfLoadedDocument("Sample.pdf")
'Get the named destination collection
Dim destinationCollection As PdfNamedDestinationCollection = lDoc.NamedDestinationCollection
'Remove the named destination by title
destinationCollection.Remove("TOC")

'Modify the exiting named destination
Dim destination As PdfNamedDestination = destinationCollection(0)
destination.Title = "POC"

'Save the document
lDoc.Save("Output.pdf")
'Close the document
lDoc.Close(True)

{% endhighlight %}

{% endtabs %}  


## Adding named destination to the bookmarks

The following code example shows how to add named destination to the bookmarks in the PDF document.

{% tabs %}   

{% highlight c# %}

//Create a new PDF document.
PdfDocument doc = new PdfDocument();
//Add a page to the document.
PdfPage page = doc.Pages.Add();
//Create an instance for named destination.
PdfNamedDestination destination = new PdfNamedDestination("TOC");
destination.Destination = new PdfDestination(page);
//Set the location
destination.Destination.Location = new PointF(0, 800);
//Set zoom factor to 400 percentage
destination.Destination.Zoom = 4;
//Add the named destination to the collection
doc.NamedDestinationCollection.Add(destination);
//Create a bookmark
PdfBookmark bookmark = doc.Bookmarks.Add("TOC");
//Assign the named destination to the bookmark
bookmark.NamedDestination = destination;
//Save the document
doc.Save("Sample.pdf");
//Close the document
doc.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document.
Dim doc As New PdfDocument()
'Add a page to the document.
Dim page As PdfPage = doc.Pages.Add()
'Create an instance for named destination.
Dim destination As New PdfNamedDestination("TOC")
destination.Destination = New PdfDestination(page)
'Set the location
destination.Destination.Location = New PointF(0, 800)
'Set zoom factor to 400 percentage
destination.Destination.Zoom = 4
'Add the named destination to the collection
doc.NamedDestinationCollection.Add(destination)
'Create a bookmark
Dim bookmark As PdfBookmark = doc.Bookmarks.Add("TOC")
'Assign the named destination to the bookmark
bookmark.NamedDestination = destination
'Save the document
doc.Save("Sample.pdf")
'Close the document
doc.Close(True)

{% endhighlight %}

{% endtabs %} 