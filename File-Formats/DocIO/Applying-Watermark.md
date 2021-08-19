---
title: Applying Watermark | DocIO | Syncfusion
description: Learn here how to insert text or pictures watermark to the Word document in Syncfusion Word (DocIO) Library and more.
platform: file-formats
control: DocIO
documentation: UG
---

# Applying Watermark in Word (DocIO) Library

Watermarks are text or pictures that appear behind the docment text. You can access the watermark in the document by using the `Watermark` property of `WordDocument` class.

There are two types of watermarks: Text and Picture.

## Text Watermark

You can add or modify text watermark in the Word document. `TextWatermark` class represents text watermark in the Word document.

The following code example illustrates how to add a text watermark to the Word document.

{% tabs %} 

{% highlight c# %}
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

{% highlight vb.net %}
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

{% highlight UWP %}
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
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word file in local machine
Save(stream, "TextWatermark.docx");
//Closes the document
document.Close();
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight ASP.NET CORE %}
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
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result_watermark1.docx");
{% endhighlight %}

{% highlight XAMARIN %}
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
textWatermark.Color = Syncfusion.Drawing.Color.Black;
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("TextWatermark.docx", "application/msword", stream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}  

## Picture Watermark

You can add or modify picture watermark in the Word document. `PictureWatermark` class represents picture watermark in the Word document.

The following code example illustrates how to add a picture watermark to the Word document.

{% tabs %}  

{% highlight c# %}
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

{% highlight vb.net %}
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

{% highlight UWP %}
//DocIO supports picture watermark in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms alone.
{% endhighlight %}

{% highlight ASP.NET CORE %}
//DocIO supports picture watermark in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms alone.
{% endhighlight %}

{% highlight XAMARIN %}
//DocIO supports picture watermark in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms alone.
{% endhighlight %}

{% endtabs %}