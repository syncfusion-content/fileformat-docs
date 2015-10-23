---
title: Working with Compression
description: Compress PDF document by using Essential PDF -Compressing; Content compression; Image compression
platform: file-formats
control: PDF
documentation: UG
---
# Working with Compression

Essential PDF allows you to compress the PDF document and thereby reduce the file size in the following two ways.

1) Content compression
2) Image compression
## Compressing the PDF content


Essential PDF allows you to control the compression level of the document by using the PdfCompressionLevel ENUM. The compression level can be set to best, normal, none etc...

Content compression involves, 

1) Removing all extra space characters.
2) Inserting a single repeat character to indicate a string of repeated characters.
3) Substituting smaller bit strings for frequently occurring characters.

The following code example illustrates how to compress the content of the PDF document.

{% highlight c# %}
[C#]

//Creates a new PDF document.

PdfDocument document = new PdfDocument();



//Sets the compression level to best

document.Compression = PdfCompressionLevel.Best;



//Adds a page to the document.

PdfPage page = document.Pages.Add();

//Creates PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Sets the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

string text = "Hello World!!!";

PdfTextElement textElement = new PdfTextElement(text, font);

PdfLayoutResult result = textElement.Draw(page, new RectangleF(0, 0, font.MeasureString(text).Width, page.GetClientSize().Height));

for (int i = 0; i < 1000; i++)

{

result = textElement.Draw(result.Page, new RectangleF(0, result.Bounds.Bottom +10, font.MeasureString(text).Width, page.GetClientSize().Height));

}

//Saves the document.

document.Save("Output.pdf");

//Closes the document.

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}
[VB]

'Creates a new PDF document.

Dim document As New PdfDocument()

'Sets the compression level to best

document.Compression = PdfCompressionLevel.Best

'Adds a page to the document.

Dim page As PdfPage = document.Pages.Add()

'Creates PDF graphics for the page.

Dim graphics As PdfGraphics = page.Graphics

'Sets the font.

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 20)

Dim text As String = "Hello World!!!"

Dim textElement As New PdfTextElement(text, font)

Dim result As PdfLayoutResult = textElement.Draw(page, New RectangleF(0, 0, font.MeasureString(text).Width, page.GetClientSize().Height))

For i As Integer = 0 To 999

result = textElement.Draw(result.Page, New RectangleF(0, result.Bounds.Bottom + 10, font.MeasureString(text).Width, page.GetClientSize().Height))

Next

'Saves the document.

document.Save("Output.pdf")

'Closes the document.

document.Close(True)



{% endhighlight %}

You can compress the existing PDF document by using the following code example.

{% highlight c# %}
[C#]

//Loads the PDF document

PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");

//Disables the incremental update

loadedDocument.FileStructure.IncrementalUpdate = false;

//Sets the compression level

loadedDocument.Compression = PdfCompressionLevel.Best;

//Saves and closes the document

loadedDocument.Save("Output.pdf");

loadedDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}
[VB]

'Loads the PDF document

Dim loadedDocument As New PdfLoadedDocument("Input.pdf")

'Disables the incremental update

loadedDocument.FileStructure.IncrementalUpdate = False

'Sets the compression level

loadedDocument.Compression = PdfCompressionLevel.Best

'Saves and closes the document

loadedDocument.Save("Output.pdf")

loadedDocument.Close(True)



{% endhighlight %}

## Compressing images

Essential PDF allows you to compress/change the quality of the image in the PDF document by using the following code example.

{% highlight c# %}
[C#]

//Creates a new PDF document.

PdfDocument document = new PdfDocument();

//Adds a page to the document.

PdfPage page = document.Pages.Add();

//Creates PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

PdfBitmap img = new PdfBitmap("Input.jpg");

//Reduces the quality of the image

img.Quality = 50;

img.Draw(page, new PointF(0, 0));

//Saves the document.

document.Save("Output.pdf");

//Closes the document.

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}
[VB]

'Creates a new PDF document.

Dim document As New PdfDocument()

'Adds a page to the document.

Dim page As PdfPage = document.Pages.Add()

'Creates PDF graphics for the page.

Dim graphics As PdfGraphics = page.Graphics

Dim img As New PdfBitmap("Input.jpg")

'Reduces the quality of the image

img.Quality = 50

img.Draw(page, New PointF(0, 0))

'Saves the document.

document.Save("Output.pdf")

'Closes the document.

document.Close(True)



{% endhighlight %}

You can compress the images in the existing PDF document by using the following code example.

{% highlight c# %}
[C#]

//Loads the PDF document which c images

PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");

//Disables the incremental update

loadedDocument.FileStructure.IncrementalUpdate = false;

//Iterates all the pages to replace images

foreach (PdfPageBase page in loadedDocument.Pages)

{

//Extracts the images from the document

Image[] extractedImages = page.ExtractImages();

//Iterates all the image

for (int j = 0; j < extractedImages.Count(); j++)

{

PdfBitmap img = new PdfBitmap(extractedImages[j]);

//Reduces the quality of the image

img.Quality = 50;

//Replaces the compressed image with old image in the PDF document

page.ReplaceImage(j, img);

}

}

//Saves and closes the document

loadedDocument.Save("Output.pdf");

loadedDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}
[VB]

'Loads the PDF document that consist of images

Dim loadedDocument As New PdfLoadedDocument("Input.pdf")

'Disables the incremental update

loadedDocument.FileStructure.IncrementalUpdate = False

'Iterates all the pages to replace images

For Each page As PdfPageBase In loadedDocument.Pages

'Extracts the images from the document

Dim extractedImages As Image() = page.ExtractImages()

'Iterates all the image

For j As Integer = 0 To extractedImages.Count() - 1

Dim img As New PdfBitmap(extractedImages(j))

'Reduces the quality of the image

img.Quality = 50

'Replaces the compressed image with old image in the PDF document

page.ReplaceImage(j, img)

Next

Next

'Saves and closes the document

loadedDocument.Save("Output.pdf")

loadedDocument.Close(True)



{% endhighlight %}

