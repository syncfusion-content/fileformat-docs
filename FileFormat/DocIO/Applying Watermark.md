---
layout: Post
title: Applying Watermark
description: This section illustrates how to insert text or pictures watermark to the Word document
platform: FileFormat
control: DocIO
documentation: UG
---
# Applying Watermark

Watermarks are text or pictures that appear behind document text. You can access the watermark in the document by using the **Watermark** property of **WordDocument** class.

There are two types of watermarks: **Text** and **Picture**.

## Text Watermark

You can add or modify text watermark in the Word document. **TextWatermark** class represents text watermark in the Word document.

The following code snippet illustrates how to add a text watermark to the Word document.

{% highlight c# %}
C#

//Create a new Word document

WordDocument document = new WordDocument();

//Add a section & a paragraph in the document

document.EnsureMinimal();

IWParagraph paragraph = document.LastParagraph;

paragraph.AppendText("Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua");

//Create a new text watermark

TextWatermark textWatermark = new TextWatermark();

//Set the created watermark to document

document.Watermark = textWatermark;

//Set the text watermark font size

textWatermark.Size = 72;

//Set the text watermark layout to Horizontal

textWatermark.Layout = WatermarkLayout.Horizontal;

textWatermark.Semitransparent = false;

//Set the text watermark text color

textWatermark.Color = Color.Black;

//Set the text to text watermark text

textWatermark.Text = "TextWatermark";

document.Save("TextWatermark.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
VB

'Create a new Word document

Dim document As New WordDocument()

'Add a section & a paragraph in the document

document.EnsureMinimal()

Dim paragraph As IWParagraph = document.LastParagraph

paragraph.AppendText("Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua")

'Create a new text watermark

Dim textWatermark As New TextWatermark()

'Set the text watermark to document

document.Watermark = textWatermark

'Set the text watermark font size

textWatermark.Size = 72

'Set the text watermark layout to Horizontal

textWatermark.Layout = WatermarkLayout.Horizontal

textWatermark.Semitransparent = False

'Set the text watermark text color

textWatermark.Color = Color.Black

'Set the text to the text watermark

textWatermark.Text = "TextWatermark"

document.Save("TextWatermark.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

## Picture Watermark

You can add or modify picture watermark in the Word document. **PictureWatermark** class represents picture watermark in the Word document.

The following code snippet illustrates how to add a picture watermark to the Word document.

{% highlight c# %}
C#

//Create a new Word document

WordDocument document = new WordDocument();

//Add a section & a paragraph in the document

document.EnsureMinimal();

IWParagraph paragraph = document.LastParagraph;

paragraph.AppendText("Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua");

//Create a new picture watermark

PictureWatermark picWatermark = new PictureWatermark();

//Set the scaling to picture

picWatermark.Scaling = 120f;

picWatermark.Washout = true;

//Set the picture watermark to document

document.Watermark = picWatermark;

//Set the image to the picture watermark

picWatermark.Picture = Image.FromFile(ImagesPath + "Water lilies.jpg");

document.Save("PictureWatermark.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
VB

'Create a new Word document

Dim document As New WordDocument()

'Add a section & a paragraph in the document

document.EnsureMinimal()

Dim paragraph As IWParagraph = document.LastParagraph

paragraph.AppendText("Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua")

'Create a new picture watermark

Dim picWatermark As New PictureWatermark()

'Set the scaling to picture

picWatermark.Scaling = 120.0F

picWatermark.Washout = True

Set the picture watermark to document

document.Watermark = picWatermark

Set the image to the picture watermark

picWatermark.Picture = Image.FromFile(ImagesPath + "Water lilies.jpg")

document.Save("PictureWatermark.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

