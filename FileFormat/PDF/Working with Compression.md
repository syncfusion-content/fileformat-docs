---
layout: Post
title: Working with Compression
description: Compress PDF document using Essential PDF :Compressing; Content compression; Image compression
platform: FileFormat
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

The following code snippet illustrates how to compress the content of the PDF document.

{% highlight c# %}
[C#]

//Create a new PDF document.

PdfDocument document = new PdfDocument();



//Set the compression level to best

document.Compression = PdfCompressionLevel.Best;



//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

string text = "Hello World!!!";

PdfTextElement textElement = new PdfTextElement(text, font);

PdfLayoutResult result = textElement.Draw(page, new RectangleF(0, 0, font.MeasureString(text).Width, page.GetClientSize().Height));

for (int i = 0; i < 1000; i++)

{

result = textElement.Draw(result.Page, new RectangleF(0, result.Bounds.Bottom +10, font.MeasureString(text).Width, page.GetClientSize().Height));

}

//Save the document.

document.Save("Output.pdf");

//Close the document.

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}
[VB]

'Create a new PDF document.

Dim document As New PdfDocument()

'Set the compression level to best

document.Compression = PdfCompressionLevel.Best

'Add a page to the document.

Dim page As PdfPage = document.Pages.Add()

'Create PDF graphics for the page.

Dim graphics As PdfGraphics = page.Graphics

'Set the font.

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 20)

Dim text As String = "Hello World!!!"

Dim textElement As New PdfTextElement(text, font)

Dim result As PdfLayoutResult = textElement.Draw(page, New RectangleF(0, 0, font.MeasureString(text).Width, page.GetClientSize().Height))

For i As Integer = 0 To 999

result = textElement.Draw(result.Page, New RectangleF(0, result.Bounds.Bottom + 10, font.MeasureString(text).Width, page.GetClientSize().Height))

Next

'Save the document.

document.Save("Output.pdf")

'Close the document.

document.Close(True)



{% endhighlight %}

You can compress the existing PDF document by using the following code snippet.

{% highlight c# %}
[C#]

//Load the PDF document

PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");

//Disable the incremental update

loadedDocument.FileStructure.IncrementalUpdate = false;

//Set the compression level

loadedDocument.Compression = PdfCompressionLevel.Best;

//Save and close the document

loadedDocument.Save("Output.pdf");

loadedDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}
[VB]

'Load the PDF document

Dim loadedDocument As New PdfLoadedDocument("Input.pdf")

'Disable the incremental update

loadedDocument.FileStructure.IncrementalUpdate = False

'Set the compression level

loadedDocument.Compression = PdfCompressionLevel.Best

'Save and close the document

loadedDocument.Save("Output.pdf")

loadedDocument.Close(True)



{% endhighlight %}

## Compressing images

Essential PDF allows you to compress/change the quality of the image in the PDF document by using the following code snippet.

{% highlight c# %}
[C#]

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

PdfBitmap img = new PdfBitmap("Input.jpg");

//Reduce the quality of the image

img.Quality = 50;

img.Draw(page, new PointF(0, 0));

//Save the document.

document.Save("Output.pdf");

//Close the document.

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}
[VB]

'Create a new PDF document.

Dim document As New PdfDocument()

'Add a page to the document.

Dim page As PdfPage = document.Pages.Add()

'Create PDF graphics for the page.

Dim graphics As PdfGraphics = page.Graphics

Dim img As New PdfBitmap("Input.jpg")

'Reduce the quality of the image

img.Quality = 50

img.Draw(page, New PointF(0, 0))

'Save the document.

document.Save("Output.pdf")

'Close the document.

document.Close(True)



{% endhighlight %}

You can compress the images in the existing PDF document by using the following code snippet

{% highlight c# %}
[C#]

//Load the PDF document which c images

PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");

//Disable the incremental update

loadedDocument.FileStructure.IncrementalUpdate = false;

//iterate all the pages to replace images

foreach (PdfPageBase page in loadedDocument.Pages)

{

//Extract the images from the document

Image[] extractedImages = page.ExtractImages();

//Iterate all the image

for (int j = 0; j < extractedImages.Count(); j++)

{

PdfBitmap img = new PdfBitmap(extractedImages[j]);

//reduce the quality of the image

img.Quality = 50;

//replace the compressed image with old image in the PDF document

page.ReplaceImage(j, img);

}

}

//Save and close the document

loadedDocument.Save("Output.pdf");

loadedDocument.Close(true);



{% endhighlight %}

{% highlight vb.net %}
[VB]

'Load the PDF document which consist of images

Dim loadedDocument As New PdfLoadedDocument("Input.pdf")

'Disable the incremental update

loadedDocument.FileStructure.IncrementalUpdate = False

'iterate all the pages to replace images

For Each page As PdfPageBase In loadedDocument.Pages

'Extract the images from the document

Dim extractedImages As Image() = page.ExtractImages()

'Iterate all the image

For j As Integer = 0 To extractedImages.Count() - 1

Dim img As New PdfBitmap(extractedImages(j))

'reduce the quality of the image

img.Quality = 50

'replace the compressed image with old image in the PDF document

page.ReplaceImage(j, img)

Next

Next

'Save and close the document

loadedDocument.Save("Output.pdf")

loadedDocument.Close(True)



{% endhighlight %}

