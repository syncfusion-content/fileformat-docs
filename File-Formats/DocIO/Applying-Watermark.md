---
title: Applying Watermark | DocIO | Syncfusion
description: Learn how to insert text or picture watermark into a Word document using the .NET Word (DocIO) library without Microsoft Word or interop dependencies.
platform: file-formats
control: DocIO
documentation: UG
---

# Applying Watermark in Word (DocIO) Library

Watermarks are text or pictures that appear behind the document text. You can access the watermark in the document by using the [Watermark](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WordDocument.html#Syncfusion_DocIO_DLS_WordDocument_Watermark) property of [WordDocument](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WordDocument.html) class.

There are two types of watermarks: Text and Picture.

## Text Watermark

You can add or modify text watermark in the Word document. [TextWatermark](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.TextWatermark.html) class represents text watermark in the Word document.

The following code example illustrates how to add a text watermark to the Word document.

{% tabs %} 

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Creates a new Word document
WordDocument document = new WordDocument();
//Adds a section and a paragraph in the document
document.EnsureMinimal();
IWParagraph paragraph = document.LastParagraph;
paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");
//Creates a new text watermark
TextWatermark textWatermark = new TextWatermark("TextWatermark", "", 250, 100);
//Sets the created watermark to the document
document.Watermark = textWatermark;
//Sets the text watermark font size
textWatermark.Size = 72;
//Sets the text watermark layout to Horizontal
textWatermark.Layout = WatermarkLayout.Horizontal;
textWatermark.Semitransparent = false;
//Sets the text watermark text color
textWatermark.Color = Color.Black;
//Saves the Word document to  MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Creates a new Word document
WordDocument document = new WordDocument();
//Adds a section and a paragraph in the document
document.EnsureMinimal();
IWParagraph paragraph = document.LastParagraph;
paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");
//Creates a new text watermark
TextWatermark textWatermark = new TextWatermark();
//Sets the created watermark to the document
document.Watermark = textWatermark;
//Sets the text watermark font size
textWatermark.Size = 72;
//Sets the text watermark layout to Horizontal
textWatermark.Layout = WatermarkLayout.Horizontal;
textWatermark.Semitransparent = false;
//Sets the text watermark text color
textWatermark.Color = Color.Black;
//Sets the text to text watermark text
textWatermark.Text = "TextWatermark";
document.Save("TextWatermark.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Creates a new Word document
Dim document As New WordDocument()
'Adds a section and a paragraph in the document
document.EnsureMinimal()
Dim paragraph As IWParagraph = document.LastParagraph
paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.")
'Creates a new text watermark
Dim textWatermark As New TextWatermark()
'Sets the text watermark to the document
document.Watermark = textWatermark
'Sets the text watermark font size
textWatermark.Size = 72
'Sets the text watermark layout to Horizontal
textWatermark.Layout = WatermarkLayout.Horizontal
textWatermark.Semitransparent = False
'Sets the text watermark text color
textWatermark.Color = Color.Black
'Sets the text to the text watermark
textWatermark.Text = "TextWatermark"
document.Save("TextWatermark.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Watermark/Add-text-watermark).

## Picture Watermark

You can add or modify picture watermark in the Word document. [PictureWatermark](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.PictureWatermark.html) class represents picture watermark in the Word document.

The following code example illustrates how to add a picture watermark to the Word document.

{% tabs %}  

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Creates a new Word document
WordDocument document = new WordDocument();
//Adds a section and a paragraph in the document
document.EnsureMinimal();
IWParagraph paragraph = document.LastParagraph;
paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");
//Creates a new picture watermark.
PictureWatermark picWatermark = new PictureWatermark();
//Sets the scaling to picture.
picWatermark.Scaling = 120f;
picWatermark.Washout = true;
//Sets the picture watermark to document.
document.Watermark = picWatermark;
FileStream imageStream = new FileStream("Water lilies.jpg", FileMode.Open, FileAccess.Read);
BinaryReader br = new BinaryReader(imageStream);
byte[] image = br.ReadBytes((int)imageStream.Length);
//Sets the image to the picture watermark.
picWatermark.LoadPicture(image);
//Saves the Word document to  MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Creates a new Word document
WordDocument document = new WordDocument();
//Adds a section and a paragraph in the document
document.EnsureMinimal();
IWParagraph paragraph = document.LastParagraph;
paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");
//Creates a new picture watermark
PictureWatermark picWatermark = new PictureWatermark();
//Sets the scaling to picture
picWatermark.Scaling = 120f;
picWatermark.Washout = true;
//Sets the picture watermark to document
document.Watermark = picWatermark;
//Sets the image to the picture watermark
picWatermark.Picture = Image.FromFile(ImagesPath + "Water lilies.jpg");
document.Save("PictureWatermark.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Creates a new Word document
Dim document As New WordDocument()
'Adds a section and a paragraph in the document
document.EnsureMinimal()
Dim paragraph As IWParagraph = document.LastParagraph
paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.")
'Creates a new picture watermark
Dim picWatermark As New PictureWatermark()
'Sets the scaling to picture
picWatermark.Scaling = 120.0F
picWatermark.Washout = True
Set the picture watermark to document
document.Watermark = picWatermark
Set the image to the picture watermark
picWatermark.Picture = Image.FromFile(ImagesPath + "Water lilies.jpg")
document.Save("PictureWatermark.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Watermark/Add-picture-watermark).