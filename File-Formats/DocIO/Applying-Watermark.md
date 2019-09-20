---
title: Applying Watermark | DocIO | Syncfusion
description: This section illustrates how to insert text or pictures watermark to the Word document
platform: file-formats
control: DocIO
documentation: UG
---

# Applying Watermark

Watermarks are text or pictures that appear behind the document text. You can access the watermark in the document by using the `Watermark` property of `WordDocument` class.

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

//Saves the Word document
async void Save(MemoryStream streams, string filename)
{
	streams.Position = 0;
	StorageFile stFile;
	if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
	{
		FileSavePicker savePicker = new FileSavePicker();
		savePicker.DefaultFileExtension = ".docx";
		savePicker.SuggestedFileName = filename;
		savePicker.FileTypeChoices.Add("Word Documents", new List<string>() { ".docx" });
		stFile = await savePicker.PickSaveFileAsync();
	}
	else
	{
		StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
		stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
	}
	if (stFile != null)
	{
		using (IRandomAccessStream zipStream = await stFile.OpenAsync(FileAccessMode.ReadWrite))
		{
			//Write compressed data from memory to file
			using (Stream outstream = zipStream.AsStreamForWrite())
			{
				byte[] buffer = streams.ToArray();
				outstream.Write(buffer, 0, buffer.Length);
				outstream.Flush();
			}
		}
	}
	//Launch the saved Word file
	await Windows.System.Launcher.LaunchFileAsync(stFile);
}

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
//Saves the Word document to  MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("TextWatermark.docx", "application/msword", stream);
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