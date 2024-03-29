---
title: Working with Bookmarks | PDF library | Syncfusion
description: This section explains how to add, modify and remove bookmarks in the PDF document by using Essential PDF
platform: file-formats
control: PDF
documentation: UG
---
# Working with Bookmarks

Essential PDF provides support to insert, remove and modify the bookmarks in the PDF Document.

## Adding Bookmarks in a PDF

The [PdfBookmarkBase](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfBookmarkBase.html) collection represents the bookmarks in a PDF document. You can add a bookmark in a new PDF document using [PdfBookmark](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfBookmark.html) class. Please refer the following code example.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

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
bookmark.Color = Syncfusion.Drawing.Color.Red;

//Save the document into stream.
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Closes the document
document.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

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
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Bookmarks/Adding-bookmarks-in-a-PDF-document/). 

## Adding Bookmarks in an existing PDF document

To add bookmarks to an existing PDF document, use the following code example.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}		

//Load the PDF document.
FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument document = new PdfLoadedDocument(docStream);
//Creates document bookmarks.
PdfBookmark bookmark = document.Bookmarks.Add("Page 1");
//Sets the destination page.
bookmark.Destination = new PdfDestination(document.Pages[0]);
//Sets the text style and color.
bookmark.TextStyle = PdfTextStyle.Bold;
bookmark.Color = Color.Red;
//Sets the destination location.
bookmark.Destination.Location = new PointF(20, 20);

//Save the document into stream.
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Closes the document.
document.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

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
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Bookmarks/Adding-bookmarks-in-an-existing-PDF-document/). 

## Adding a Child to the Bookmarks

You can add a child bookmark by using [Insert](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfBookmarkBase.html#Syncfusion_Pdf_Interactive_PdfBookmarkBase_Insert_System_Int32_System_String_) method. Please refer to the following code example.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

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
//Adds the child bookmark.
PdfBookmark childBookmark = bookmark.Insert(0, "heading 1");
childBookmark.Destination = new PdfDestination(page);
childBookmark.Destination.Location = new PointF(400, 300);
childBookmark.Destination.Zoom = 2F;
//Sets the text style and color.
bookmark.TextStyle = PdfTextStyle.Bold;
bookmark.Color = Syncfusion.Drawing.Color.Red;

//Save the document into stream.
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Closes the document.
document.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

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
//Adds the child bookmark.
PdfBookmark childBookmark = bookmark.Insert(0,"heading 1");
childBookmark.Destination = new PdfDestination(page);
childBookmark.Destination.Location = new PointF(400, 300);
childBookmark.Destination.Zoom = 2F;
//Sets the text style and color.
bookmark.TextStyle = PdfTextStyle.Bold;
bookmark.Color = Color.Red;

//Saves and closes the PDF document.
document.Save("Output.pdf");
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Bookmarks/Adding-a-child-to-the-bookmarks-in-a-PDF). 

## Inserting Bookmarks in an existing PDF

When loading an existing document, the Essential PDF loads all bookmarks of the document.  

Each loaded bookmark is represented by the [PdfLoadedBookmark](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfLoadedBookmark.html) object. The following code example illustrates how to insert new bookmarks in the existing PDF document.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Load the PDF document.
FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument document = new PdfLoadedDocument(docStream);
//Inserts a new bookmark in the existing bookmark collection.
PdfBookmark bookmark = document.Bookmarks.Insert(1, "New Page 2");
//Sets the destination page and location.
bookmark.Destination = new PdfDestination(document.Pages[1]);
bookmark.Destination.Location = new PointF(0, 300);

//Save the document into stream.
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Closes the document.
document.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Creates a new document.
PdfLoadedDocument document = new PdfLoadedDocument("Input.pdf");
//Inserts a new bookmark in the existing bookmark collection.
PdfBookmark bookmark = document.Bookmarks.Insert(1, "New Page 2");
//Sets the destination page and location.
bookmark.Destination = new PdfDestination(document.Pages[1]);
bookmark.Destination.Location = new PointF(0, 300);
//Saves and closes the PDF document.
document.Save("Output.pdf");
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Bookmarks/Inserting-bookmarks-in-an-existing-PDF/). 

## Removing Bookmarks from an existing PDF 

You can also remove bookmarks from the existing PDF document by using [Remove](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfBookmarkBase.html#Syncfusion_Pdf_Interactive_PdfBookmarkBase_Remove_System_String_) method. Please refer the following code example.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Load the PDF document.
FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument document = new PdfLoadedDocument(docStream);
//Gets all the bookmarks.
PdfBookmarkBase bookmarks = document.Bookmarks;
//Removes bookmark by bookmark name.
bookmarks.Remove("Page 1");
//Removes bookmark by index.
bookmarks.RemoveAt(1);

//Save the document into stream.
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Closes the document.
document.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

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
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Bookmarks/Remove-bookmarks-from-an-existing-PDF-document/). 

## Modifying the Bookmarks

Essential PDF allows you to modify the bookmarks in the existing PDF document. The following modifications can be done to bookmarks in an existing document. 

* Modify the bookmark style, color, title, and destination.
* Add or insert new bookmarks into the root collection.
* Add or insert new bookmarks as a child of another bookmark.
* Assign the destination of the added bookmarks to a loaded page or a new page of the document.

The following code example shows how to modify the [Destination](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfLoadedBookmark.html#Syncfusion_Pdf_Interactive_PdfLoadedBookmark_Destination), [Color](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfLoadedBookmark.html#Syncfusion_Pdf_Interactive_PdfLoadedBookmark_Color), [TextStyle](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfLoadedBookmark.html#Syncfusion_Pdf_Interactive_PdfLoadedBookmark_TextStyle) and [Title](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfLoadedBookmark.html#Syncfusion_Pdf_Interactive_PdfLoadedBookmark_Title) of an existing bookmark collection.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Load the PDF document.
FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument document = new PdfLoadedDocument(docStream);
//Gets all the bookmarks.
PdfBookmarkBase bookmarks = document.Bookmarks;
//Gets the first bookmark and changes the properties of the bookmark.
PdfLoadedBookmark bookmark = bookmarks[0] as PdfLoadedBookmark;
bookmark.Destination = new PdfDestination(document.Pages[0]);
bookmark.Color = Syncfusion.Drawing.Color.Green;
bookmark.TextStyle = PdfTextStyle.Bold;
bookmark.Title = "Changed title";

//Save the document into stream.
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Closes the document.
document.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

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

//Saves the document.
document.Save("Output.pdf");
//Closes the document.
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

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

'Saves the document.
document.Save("Output.pdf")
'Closes the document.
document.Close(True)

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Bookmarks/Modify-the-bookmarks-in-an-existing-PDF-document/). 

## Bookmark page index in an existing PDF document
You can get bookmark page index from the existing PDF document using [PageIndex](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfDestination.html#Syncfusion_Pdf_Interactive_PdfDestination_PageIndex) property as shown in the following code snippet.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Load the PDF document.
FileStream docStream = new FileStream("input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);
//Gets all the bookmarks.
PdfBookmarkBase bookmark = loadedDocument.Bookmarks;
//Get the bookmark page index. 
int index = bookmark[0].Destination.PageIndex;

//Save the document into stream.
MemoryStream stream = new MemoryStream();
loadedDocument.Save(stream);
//Close the document.
loadedDocument.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Load the PDF document.
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("input.pdf");
//Gets all the bookmarks.
PdfBookmarkBase bookmark = loadedDocument.Bookmarks;
//Get the bookmark page index
int index = bookmark[0].Destination.PageIndex;

//Save the document.
loadedDocument.Save("Output.pdf");
//Close the document.
loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Load the PDF document.
 Dim loadedDocument As New PdfLoadedDocument("input.pdf") 
'Gets all the bookmarks.
Dim bookmark As PdfBookmarkBase = loadedDocument.Bookmarks
'Get the bookmark page index. 
Dim index As Integer = bookmark(0).Destination.PageIndex

'Save and close the document. 
loadedDocument.Save("Output.pdf") 
loadedDocument.Close(True)

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Bookmarks/Get-bookmark-page-index-from-the-existing-PDF-document/). 