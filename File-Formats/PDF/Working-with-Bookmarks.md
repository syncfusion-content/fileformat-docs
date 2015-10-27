---
title: Working with Bookmarks
description: This section explains how to add bookmarks to the PDF document by using Essential PDF
platform: FileFormat
control: PDF
documentation: UG
---
# Working with Bookmarks

Essential PDF provides support to insert, remove and modify the bookmarks in the PDF Document.

## Adding Bookmarks in a PDF

The PdfBookmarkBase collection represents the bookmarks in a PDF document. To add a bookmark in a new PDF document, use the following code examples.

{% tabs %}
{% highlight c# %}


//Creates a new document.

PdfDocument document = new PdfDocument();

//Adds a page.

PdfPage page = document.Pages.Add();

//Creates document bookmarks.

PdfBookmark bookmark = document.Bookmarks.Add("Page 1");

//Sets the destination page.

bookmark.Destination = new PdfDestination(page);

//Sets the destination location.

bookmark.Destination.Location = new PointF(20, 20);

//Sets the text style and color.

bookmark.TextStyle = PdfTextStyle.Bold;

bookmark.Color = Color.Red;

//Saves and closes the PDF document.

document.Save("Output.pdf");

document.Close(True);



{% endhighlight %}

{% highlight vb.net %}

'Creates a new document.

Dim document As New PdfDocument()

'Adds a page.

Dim page As PdfPage = document.Pages.Add()

'Creates document bookmarks.

Dim bookmark As PdfBookmark = document.Bookmarks.Add("Page 1")

'Sets the destination page.

bookmark.Destination = New PdfDestination(page)

'Sets the destination location.

bookmark.Destination.Location = New PointF(20, 20)

'Sets the text style and color.

bookmark.TextStyle = PdfTextStyle.Bold

bookmark.Color = Color.Red

'Saves and closes the PDF document.

document.Save("Output.pdf")

document.Close(True)



{% endhighlight %}
{% endtabs %}

## Adding Bookmarks in an existing PDF document

To add bookmarks to an existing PDF document, use the following code examples.
{% tabs %}
{% highlight c# %}


//Loads the document.

PdfLoadedDocument document = new PdfLoadedDocument("input.pdf");

//Creates document bookmarks.

PdfBookmark bookmark = document.Bookmarks.Add("Page 1");

//Sets the destination page.

bookmark.Destination = new PdfDestination(document.Pages[0]);

//Sets the text style and color.

bookmark.TextStyle = PdfTextStyle.Bold;

bookmark.Color = Color.Red;

//Sets the destination location.

bookmark.Destination.Location = new PointF(20, 20);

//Saves and closes the PDF document.

document.Save("Output.pdf");

document.Close(True);





{% endhighlight %}

{% highlight vb.net %}


'Loads the document.

Dim document As New PdfLoadedDocument("input.pdf")

'Creates document bookmarks.

Dim bookmark As PdfBookmark = document.Bookmarks.Add("Page 1")

'Sets the destination page.

bookmark.Destination = New PdfDestination(document.Pages(0))

'Sets the text style and color.

bookmark.TextStyle = PdfTextStyle.Bold

bookmark.Color = Color.Red

'Sets the destination location.

bookmark.Destination.Location = New PointF(20, 20)

'Saves and closes the PDF document.

document.Save("Output.pdf")

document.Close(True)



{% endhighlight %}
{% endtabs %}

## Adding a Child to the Bookmarks

To a child to a bookmark, refer to the following code example.

{% tabs %}
{% highlight c# %}

//Creates a new document.

PdfDocument document = new PdfDocument();

//Adds a page.

PdfPage page = document.Pages.Add();

//Creates bookmark.

PdfBookmark bookmark = document.Bookmarks.Add("Page 1");

//Sets the destination page.

bookmark.Destination = new PdfDestination(page);

//Sets the destination location.

bookmark.Destination.Location = new PointF(20, 20);

//Adds the child bookmark

PdfBookmark childBookmark = bookmark.Insert(0,"heading 1");

childBookmark.Destination = new PdfDestination(page);

childBookmark.Destination.Location = new PointF(400, 300);

childBookmark.Destination.Zoom = 2F;

//Sets the text style and color.

bookmark.TextStyle = PdfTextStyle.Bold;

bookmark.Color = Color.Red;

//Saves and closes the PDF document.

document.Save("Output.pdf");

document.Close(True);





{% endhighlight %}

{% highlight vb.net %}

'Creates a new document.

Dim document As New PdfDocument()

'Adds a page.

Dim page As PdfPage = document.Pages.Add()

'Creates bookmark.

Dim bookmark As PdfBookmark = document.Bookmarks.Add("Page 1")

'Sets the destination page.

bookmark.Destination = New PdfDestination(page)

'Sets the destination location.

bookmark.Destination.Location = New PointF(20, 20)

'Adds the child bookmark

Dim childBookmark As PdfBookmark = bookmark.Insert(0, "heading 1")

childBookmark.Destination = New PdfDestination(page)

childBookmark.Destination.Location = New PointF(400, 300)

childBookmark.Destination.Zoom = 2.0F

'Sets the text style and color.

bookmark.TextStyle = PdfTextStyle.Bold

bookmark.Color = Color.Red

'Saves and closes the PDF document.

document.Save("Output.pdf")

document.Close(True)



{% endhighlight %}
{% endtabs %}

## Inserting Bookmarks in an existing PDF

When loading an existing document, the Essential PDF loads all bookmarks of the document.  

Each loaded bookmark is represented by the PdfLoadedBookmark object. The following code example illustrates how to insert new bookmarks in the existing PDF document.

{% tabs %}
{% highlight c# %}


//Creates a new document.

PdfLoadedDocument document = new PdfLoadedDocument("Input.pdf");

//Inserts a new bookmark in the existing bookmark collection.

PdfBookmark bookmark = document.Bookmarks.Insert(1, "New Page 2");

//Sets the destination page and location.

bookmark.Destination = new PdfDestination(document.Pages[1]);

bookmark.Destination.Location = new PointF(0, 300);

//Saves and closes the PDF document.

document.Save("Output.pdf");

document.Close(True);





{% endhighlight %}

{% highlight vb.net %}

'Creates a new document.

Dim document As New PdfLoadedDocument("Input.pdf")

'Inserts a new bookmark in the existing bookmark collection.

Dim bookmark As PdfBookmark = document.Bookmarks.Insert(1, "New Page 2")

'Sets the destination page and location.

bookmark.Destination = New PdfDestination(document.Pages(1))

bookmark.Destination.Location = New PointF(0, 300)

'Saves and closes the PDF document.

document.Save("Output.pdf")

document.Close(True)



{% endhighlight %}
{% endtabs %}

## Removing Bookmarks from an existing PDF 

You can also remove bookmarks from the existing PDF document by using the following code examples.

{% tabs %}
{% highlight c# %}

//Loads the PDF document.

PdfLoadedDocument document = new PdfLoadedDocument("Input.pdf");

//Gets all the bookmarks.

PdfBookmarkBase bookmarks = document.Bookmarks;

//Removes bookmark by bookmark name.

bookmarks.Remove("Page 1");

//Removes bookmark by index.

bookmarks.RemoveAt(1);

//Saves and closes the document.

document.Save("Output.pdf");

document.Close(True);



{% endhighlight %}

{% highlight vb.net %}

'Loads the PDF document.

Dim document As New PdfLoadedDocument("Input.pdf")

'Gets all the bookmarks.

Dim bookmarks As PdfBookmarkBase = document.Bookmarks

'Removes bookmark by bookmark name.

bookmarks.Remove("Page 1")

'Removes bookmark by index.

bookmarks.RemoveAt(1)

'Saves and closes the document.

document.Save("Output.pdf")

document.Close(True)



{% endhighlight %}
{% endtabs %}

## Modifying the Bookmarks

Essential PDF allows you to modify the bookmarks in the existing PDF document. The following modifications can be done to bookmarks in an existing document. 

* Modify the bookmark style, color, title, and destination.
* Add or insert new bookmarks into the root collection.
* Add or insert new bookmarks as a child of another bookmark.
* Assign the destination of the added bookmarks to a loaded page or a new page of the document.

The following code example shows how to modify the destination, color, style and title of an existing bookmark collection.

{% tabs %}
{% highlight c# %}

//Loads the PDF document.

PdfLoadedDocument document = new PdfLoadedDocument("Input.pdf");

//Gets all the bookmarks.

PdfBookmarkBase bookmarks = document.Bookmarks;

//Gets the first bookmark and changes the properties of the bookmark.

PdfLoadedBookmark bookmark = bookmarks[0] as PdfLoadedBookmark;

bookmark.Destination = new PdfDestination(document.Pages[1]);

bookmark.Color = Color.Green;

bookmark.TextStyle = PdfTextStyle.Bold;

bookmark.Title = "Changed title";

//Saves the document

document.Save("Output.pdf");

document.Close(True);



{% endhighlight %}

{% highlight vb.net %}

'Loads the PDF document.

Dim document As New PdfLoadedDocument("Input.pdf")

'Gets all the bookmarks.

Dim bookmarks As PdfBookmarkBase = document.Bookmarks

'Gets the first bookmark and changes the properties of the bookmark.

Dim bookmark As PdfLoadedBookmark = TryCast(bookmarks(0), PdfLoadedBookmark)

bookmark.Destination = New PdfDestination(document.Pages(1))

bookmark.Color = Color.Green

bookmark.TextStyle = PdfTextStyle.Bold

bookmark.Title = "Changed title"

'Saves the document

document.Save("Output.pdf")

document.Close(True)





{% endhighlight %}
{% endtabs %}
