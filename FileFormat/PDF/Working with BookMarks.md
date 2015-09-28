---
layout: Post
title: Working with Bookmarks
description: Bookmarks using Essential PDF: Bookmark
platform: FileFormat
control: PDF
documentation: UG
---
# Working with Bookmarks

**Essential** **PDF** provides support to insert, remove and modify the bookmarks in the PDF Document.

## Adding Bookmarks in a PDF

The **PdfBookmarkBase** collection represents the bookmarks in a PDF document. To add a bookmark in a new PDF document, use the below code snippets.

{% highlight c# %}
[C#]

//Create a new document.

PdfDocument document = new PdfDocument();

//Add a page.

PdfPage page = document.Pages.Add();

//Create document bookmarks.

PdfBookmark bookmark = document.Bookmarks.Add("Page 1");

//Set the destination page.

bookmark.Destination = new PdfDestination(page);

//Set the destination location.

bookmark.Destination.Location = new PointF(20, 20);

//Set the text style and color.

bookmark.TextStyle = PdfTextStyle.Bold;

bookmark.Color = Color.Red;

//Save and close the PDF document.

document.Save("Output.pdf");

document.Close(True);



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Create a new document.

Dim document As New PdfDocument()

'Add a page.

Dim page As PdfPage = document.Pages.Add()

'Create document bookmarks.

Dim bookmark As PdfBookmark = document.Bookmarks.Add("Page 1")

'Set the destination page.

bookmark.Destination = New PdfDestination(page)

'Set the destination location.

bookmark.Destination.Location = New PointF(20, 20)

'Set the text style and color.

bookmark.TextStyle = PdfTextStyle.Bold

bookmark.Color = Color.Red

'Save and close the PDF document.

document.Save("Output.pdf")

document.Close(True)



{% endhighlight %}

## Adding Bookmarks in an existing PDF document

To add bookmarks to an existing PDF document, use the below code snippets.

{% highlight c# %}
[C#]

//Load the document.

PdfLoadedDocument document = new PdfLoadedDocument("input.pdf");

//Create document bookmarks.

PdfBookmark bookmark = document.Bookmarks.Add("Page 1");

//Sets the destination page.

bookmark.Destination = new PdfDestination(document.Pages[0]);

//Set the text style and color.

bookmark.TextStyle = PdfTextStyle.Bold;

bookmark.Color = Color.Red;

//Set the destination location.

bookmark.Destination.Location = new PointF(20, 20);

//Save and close the PDF document.

document.Save("Output.pdf");

document.Close(True);





{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Load the document.

Dim document As New PdfLoadedDocument("input.pdf")

'Create document bookmarks.

Dim bookmark As PdfBookmark = document.Bookmarks.Add("Page 1")

'Set the destination page.

bookmark.Destination = New PdfDestination(document.Pages(0))

'Set the text style and color.

bookmark.TextStyle = PdfTextStyle.Bold

bookmark.Color = Color.Red

'Set the destination location.

bookmark.Destination.Location = New PointF(20, 20)

'Save and close the PDF document.

document.Save("Output.pdf")

document.Close(True)



{% endhighlight %}

## Adding a Child to the Bookmarks

To a child to a bookmark, please refer to the below code snippet.

{% highlight c# %}
[C#]

//Create a new document.

PdfDocument document = new PdfDocument();

//Add a page.

PdfPage page = document.Pages.Add();

//Create bookmark.

PdfBookmark bookmark = document.Bookmarks.Add("Page 1");

//Set the destination page.

bookmark.Destination = new PdfDestination(page);

//Set the destination location.

bookmark.Destination.Location = new PointF(20, 20);

//Adding the child bookmark

PdfBookmark childBookmark = bookmark.Insert(0,"heading 1");

childBookmark.Destination = new PdfDestination(page);

childBookmark.Destination.Location = new PointF(400, 300);

childBookmark.Destination.Zoom = 2F;

//Set the text style and color.

bookmark.TextStyle = PdfTextStyle.Bold;

bookmark.Color = Color.Red;

//Save and close the PDF document.

document.Save("Output.pdf");

document.Close(True);





{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Create a new document.

Dim document As New PdfDocument()

'Add a page.

Dim page As PdfPage = document.Pages.Add()

'Create bookmark.

Dim bookmark As PdfBookmark = document.Bookmarks.Add("Page 1")

'Set the destination page.

bookmark.Destination = New PdfDestination(page)

'Set the destination location.

bookmark.Destination.Location = New PointF(20, 20)

'Adding the child bookmark

Dim childBookmark As PdfBookmark = bookmark.Insert(0, "heading 1")

childBookmark.Destination = New PdfDestination(page)

childBookmark.Destination.Location = New PointF(400, 300)

childBookmark.Destination.Zoom = 2.0F

'Set the text style and color.

bookmark.TextStyle = PdfTextStyle.Bold

bookmark.Color = Color.Red

'Save and close the PDF document.

document.Save("Output.pdf")

document.Close(True)



{% endhighlight %}

## Inserting Bookmarks in an existing PDF

When loading an existing document, the **Essential** **PDF** loads all bookmarks of the document. 

Each loaded bookmark is represented by the **PdfLoadedBookmark** object. The following code example illustrates how to insert new bookmarks in the existing **PDF** document.

{% highlight c# %}
[C#]

//Create a new document.

PdfLoadedDocument document = new PdfLoadedDocument("Input.pdf");

//Insert a new bookmark in the existing bookmark collection.

PdfBookmark bookmark = document.Bookmarks.Insert(1, "New Page 2");

//Set the destination page and location.

bookmark.Destination = new PdfDestination(document.Pages[1]);

bookmark.Destination.Location = new PointF(0, 300);

//Save and close the PDF document.

document.Save("Output.pdf");

document.Close(True);





{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Create a new document.

Dim document As New PdfLoadedDocument("Input.pdf")

'Insert a new bookmark in the existing bookmark collection.

Dim bookmark As PdfBookmark = document.Bookmarks.Insert(1, "New Page 2")

'Set the destination page and location.

bookmark.Destination = New PdfDestination(document.Pages(1))

bookmark.Destination.Location = New PointF(0, 300)

'Save and close the PDF document.

document.Save("Output.pdf")

document.Close(True)



{% endhighlight %}

## Removing Bookmarks from an existing PDF 

You can also remove bookmarks from the existing PDF document by using the below code snippets.

{% highlight c# %}
[C#]

//Load the PDF document.

PdfLoadedDocument document = new PdfLoadedDocument("Input.pdf");

//Get all the bookmarks.

PdfBookmarkBase bookmarks = document.Bookmarks;

//Remove bookmark by bookmark name.

bookmarks.Remove("Page 1");

//Remove bookmark by index.

bookmarks.RemoveAt(1);

//Save and close the document.

document.Save("Output.pdf");

document.Close(True);



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Load the PDF document.

Dim document As New PdfLoadedDocument("Input.pdf")

'Get all the bookmarks.

Dim bookmarks As PdfBookmarkBase = document.Bookmarks

'Remove bookmark by bookmark name.

bookmarks.Remove("Page 1")

'Remove bookmark by index.

bookmarks.RemoveAt(1)

'Save and close the document.

document.Save("Output.pdf")

document.Close(True)



{% endhighlight %}

## Modifying the Bookmarks

**Essential** **PDF** allows you to modify the bookmarks in the existing PDF document. The following modifications can be done to bookmarks in an existing document. 

* Modify the bookmark style, color, title, and destination.
* Add or insert new bookmarks into the root collection.
* Add or insert new bookmarks as a child of another bookmark.
* Assign the destination of the added bookmarks to a loaded page or a new page of the document.

The following code snippet shows how to modify the destination, color, style and title of an existing bookmark collection.

{% highlight c# %}
[C#]

//Load the PDF document.

PdfLoadedDocument document = new PdfLoadedDocument("Input.pdf");

//Get all the bookmarks.

PdfBookmarkBase bookmarks = document.Bookmarks;

//Get the first bookmark and change the properties of the bookmark.

PdfLoadedBookmark bookmark = bookmarks[0] as PdfLoadedBookmark;

bookmark.Destination = new PdfDestination(document.Pages[1]);

bookmark.Color = Color.Green;

bookmark.TextStyle = PdfTextStyle.Bold;

bookmark.Title = "Changed title";

//Save the document

document.Save("Output.pdf");

document.Close(True);



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Load the PDF document.

Dim document As New PdfLoadedDocument("Input.pdf")

'Get all the bookmarks.

Dim bookmarks As PdfBookmarkBase = document.Bookmarks

'Get the first bookmark and change the properties of the bookmark.

Dim bookmark As PdfLoadedBookmark = TryCast(bookmarks(0), PdfLoadedBookmark)

bookmark.Destination = New PdfDestination(document.Pages(1))

bookmark.Color = Color.Green

bookmark.TextStyle = PdfTextStyle.Bold

bookmark.Title = "Changed title"

'Save the document

document.Save("Output.pdf")

document.Close(True)





{% endhighlight %}

