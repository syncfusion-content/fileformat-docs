---
title: Working with Compression | Syncfusion
description: This section explains how to Compress PDF document by using Essential PDF
platform: file-formats
control: PDF
documentation: UG
---
# Working with Compression

Essential PDF allows you to compress the PDF document and thereby reduce the file size in the following three ways.

1. Compress an existing PDF document
2. Content compression for a new document
3. Image compression for a new document

N> PDF supports compressing PDF document only in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

## Compressing existing PDF document

You can compress the existing PDF document by using [PdfLoadedDocument](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Base~Syncfusion.Pdf.Parsing.PdfLoadedDocument.html) and [PdfCompressionOptions](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Base~Syncfusion.Pdf.PdfCompressionOptions.html). The following compression techniques are used to compress the existing PDF document.

1. Compress the image with image quality
2. Optimizing embedded font
3. Optimizing page content
4. Remove metadata information

## Compressing images with image quality

You can compress all the images of an existing PDF document by enabling the [CompressImages](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Base~Syncfusion.Pdf.PdfCompressionOptions~CompressImages.html) property and assigning [ImageQuality](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Base~Syncfusion.Pdf.PdfCompressionOptions~ImageQuality.html) available in [PdfCompressionOptions](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Base~Syncfusion.Pdf.PdfCompressionOptions.html) class. The ```ImageQuality``` property is used to reduce the quality of the image based on percentage value, where 100 is unchanged quality and 10 is low quality.

The following example code snippet illustrates how to compress the images in existing PDF document.

{% tabs %}
{% highlight c# %}

//Load the existing PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("input.pdf");

//Create a new compression option.
PdfCompressionOptions options = new PdfCompressionOptions();

//Enable the compress image.
options.CompressImages = true;

//Set the image quality.
options.ImageQuality = 50;

//Assign the compression option to the document
loadedDocument.CompressionOptions = options;

//Save the PDF document
loadedDocument.Save("Output.pdf");

//Close the document
loadedDocument.Close(true);

{% endhighlight %}
{% highlight vb.net %}

'Load the existing PDF document
Dim loadedDocument As PdfLoadedDocument = New PdfLoadedDocument("input.pdf")

'Create a new compression option.
Dim options As PdfCompressionOptions = New PdfCompressionOptions()

'Enable the compress image.
options.CompressImages = True

'Set the image quality.
options.ImageQuality = 50

'Assign the compression option to the document
loadedDocument.CompressionOptions = options

'Save the PDF document
loadedDocument.Save("Output.pdf")

'Close the document
loadedDocument.Close(True)

{% endhighlight %}

{% endtabs %}

## Optimizing embedded font

You can optimize the embedded fonts in an existing PDF document by enabling the [OptimizeFont](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Base~Syncfusion.Pdf.PdfCompressionOptions~OptimizeFont.html) property available in the [PdfCompressionOptions](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Base~Syncfusion.Pdf.PdfCompressionOptions.html) class. This technique reduces the font file size by removing all the unused glyph data.

The following example code snippet illustrates how to optimize embedded font in existing PDF document.

{% tabs %}
{% highlight c# %}

//Load the existing PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("input.pdf");

//Create a new compression option.
PdfCompressionOptions options = new PdfCompressionOptions();

//Enable the optimize font option
options.OptimizeFont = true;

//Assign the compression option to the document
loadedDocument.CompressionOptions = options;

//Save the PDF document
loadedDocument.Save("Output.pdf");

//Close the document
loadedDocument.Close(true);

{% endhighlight %}
{% highlight vb.net %}

'Load the existing PDF document
Dim loadedDocument As PdfLoadedDocument = New PdfLoadedDocument("input.pdf")

'Create a new compression option.
Dim options As PdfCompressionOptions = New PdfCompressionOptions()

'Enable the optimize font option
options.OptimizeFont = True

'Assign the compression option to the document
loadedDocument.CompressionOptions = options

'Save the PDF document
loadedDocument.Save("Output.pdf")

'Close the document
loadedDocument.Close(True)

{% endhighlight %}

{% endtabs %}

N> The font compression support only in TrueType and Type2 embedded fonts.

## Optimizing page contents

You can compress the page contents in an existing PDF document by enabling the [OptimizePageContents](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Base~Syncfusion.Pdf.PdfCompressionOptions~OptimizePageContents.html) property available in the [PdfCompressionOptions](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Base~Syncfusion.Pdf.PdfCompressionOptions.html) class. This technique removes the unwanted data in the content streams such as commented lines, white spaces, etc.,

The following example code snippet illustrates how to optimize page contents in existing PDF document.

{% tabs %}
{% highlight c# %}

//Load the existing PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("input.pdf");

//Create a new compression option.
PdfCompressionOptions options = new PdfCompressionOptions();

//Enable the optimize page contents.
options.OptimizePageContents = true;

//Assign the compression option to the document
loadedDocument.CompressionOptions = options;

//Save the PDF document
loadedDocument.Save("Output.pdf");

//Close the document
loadedDocument.Close(true);

{% endhighlight %}
{% highlight vb.net %}

'Load the existing PDF document
Dim loadedDocument As PdfLoadedDocument = New PdfLoadedDocument("input.pdf")

'Create a new compression option.
Dim options As PdfCompressionOptions = New PdfCompressionOptions()

'Enable the optimize page contents.
options.OptimizePageContents = True

'Assign the compression option to the document
loadedDocument.CompressionOptions = options

'Save the PDF document
loadedDocument.Save("Output.pdf")

'Close the document
loadedDocument.Close(True)

{% endhighlight %}

{% endtabs %}

## Remove metadata information

You can reduce the PDF file size by removing the PDF document metadata information. This can be achieved by enabling the [RemoveMetadata](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Base~Syncfusion.Pdf.PdfCompressionOptions~RemoveMetadata.html) property available in the [PdfCompressionOptions](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Base~Syncfusion.Pdf.PdfCompressionOptions.html) class.

The following example code snippet illustrates how to optimize page contents in existing PDF document.

{% tabs %}
{% highlight c# %}

//Load the existing PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("input.pdf");
//Create a new compression option.
PdfCompressionOptions options = new PdfCompressionOptions();
//Set to remove the metadata information.
options.RemoveMetadata = true;
//Assign the compression option to the document
loadedDocument.CompressionOptions = options;
//Save the PDF document
loadedDocument.Save("Output.pdf");
//Close the document
loadedDocument.Close(true);

{% endhighlight %}
{% highlight vb.net %}

'Load the existing PDF document
Dim loadedDocument As PdfLoadedDocument = New PdfLoadedDocument("input.pdf")

'Create a new compression option.
Dim options As PdfCompressionOptions = New PdfCompressionOptions()

'Set to remove the metadata information.
options.RemoveMetadata = True

'Assign the compression option to the document
loadedDocument.CompressionOptions = options

'Save the PDF document
loadedDocument.Save("Output.pdf")

'Close the document
loadedDocument.Close(True)

{% endhighlight %}

{% endtabs %}

## Compressing the PDF content

Essential PDF allows you to control the compression level of the document by using the [PdfCompressionLevel](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Base~Syncfusion.Pdf.PdfCompressionLevel.html) Enum. The compression level can be set to best, normal, none etc...
Content compression involves,

1) Removing all extra space characters.
2) Inserting a single repeat character to indicate a string of repeated characters.
3) Substituting smaller bit strings for frequently occurring characters.

The following code snippet illustrates how to compress the content of the PDF document.

{% tabs %}
{% highlight c# %}

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

{% endtabs %}

You can compress the existing PDF document by using the following code snippet.

{% tabs %}
{% highlight c# %}

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

{% endtabs %}

## Compressing images

Essential PDF allows you to compress/change the quality of the image in the PDF document by using the following code snippet.

{% tabs %}
{% highlight c# %}


//Create a new PDF document.
PdfDocument document = new PdfDocument();

//Add a page to the document.
PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;

PdfBitmap image = new PdfBitmap("Input.jpg");

//Reduce the quality of the image
image.Quality = 50;

image.Draw(page, new PointF(0, 0));

//Save the document.
document.Save("Output.pdf");

//Close the document.
document.Close(true);

{% endhighlight %}
{% highlight vb.net %}

'Create a new PDF document.
Dim document As New PdfDocument()

'Add a page to the document.
Dim page As PdfPage = document.Pages.Add()

'Create PDF graphics for the page.
Dim graphics As PdfGraphics = page.Graphics

Dim image As New PdfBitmap("Input.jpg")

'Reduce the quality of the image
image.Quality = 50

image.Draw(page, New PointF(0, 0))

'Save the document.
document.Save("Output.pdf")

'Close the document.
document.Close(True)

{% endhighlight %}

{% endtabs %}

You can compress the images in the existing PDF document by using the following code snippet.

{% tabs %}
{% highlight c# %}

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
PdfBitmap image = new PdfBitmap(extractedImages[j]);

//reduce the quality of the image
image.Quality = 50;

//replace the compressed image with old image in the PDF document
page.ReplaceImage(j, image);
}

}

//Save and close the document
loadedDocument.Save("Output.pdf");

loadedDocument.Close(true);

{% endhighlight %}
{% highlight vb.net %}

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

Dim image As New PdfBitmap(extractedImages(j))

'reduce the quality of the image
image.Quality = 50

'replace the compressed image with old image in the PDF document
page.ReplaceImage(j, image)

Next
Next

'Save and close the document
loadedDocument.Save("Output.pdf")

loadedDocument.Close(True)

{% endhighlight %}

{% endtabs %}
