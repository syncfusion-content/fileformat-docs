---
title: Working with Footnotes and endnotes | DocIO | Syncfusion
description: This section illustrates how to insert the footnote and endnote in a Word document
platform: file-formats
control: DocIO
documentation: UG
---
# Footnotes and endnotes

Footnotes and endnotes are separate text body contents used in documents to show the source of supplementary information that does not interrupt the normal body text of the Word document. Footnotes are typically located at the bottom of a page or beneath text being referenced, and endnotes are typically placed at the end of a document or at the end of a section. When document has been divided up into one or more sections, each section of a document can contain endnotes.

Both footnotes and endnotes consist of two parts:

* A note reference mark with numbering value in the body text to indicate that additional information is in a footnote or endnote at the end of the page or the end of the document or section.
* The footnote or endnote text body content.

## Adding a Footnotes

The following code example shows how to insert the footnotes into the Word document.

{% tabs %} 

{% highlight c# %}

//Creates a new Word document
WordDocument document = new WordDocument();
//Creates a section
IWSection section = document.AddSection();
//Adds a paragraph to a section
IWParagraph paragraph = section.AddParagraph();
//Appends the text to paragraph
paragraph.AppendText("Working with footnotes");
//Formats the text
paragraph.ApplyStyle(BuiltinStyle.Heading1);
//Adds a paragraph to a section
paragraph = section.AddParagraph();
//Appends the footnotes
WFootnote footnote = (WFootnote) paragraph.AppendFootnote(Syncfusion.DocIO.FootnoteType.Footnote);
//Sets the footnote character format
footnote.MarkerCharacterFormat.SubSuperScript = SubSuperScript.SuperScript;
//Inserts the text into the paragraph
paragraph.AppendText("Sample content for footnotes").CharacterFormat.Bold = true;
//Adds footnote text
paragraph = footnote.TextBody.AddParagraph();
paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");
//Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx);
document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates a new Word document
Dim document As New WordDocument()
'Creates a section
Dim section As IWSection = document.AddSection()
'Adds a paragraph to a section
Dim paragraph As IWParagraph = section.AddParagraph()
'Appends the text to paragraph
paragraph.AppendText("Working with footnotes")
'Formats the text
paragraph.ApplyStyle(BuiltinStyle.Heading1)
'Adds a paragraph to a section
paragraph = section.AddParagraph()
'Appends the footnotes
Dim footnote As WFootnote = DirectCast(paragraph.AppendFootnote(Syncfusion.DocIO.FootnoteType.Footnote), WFootnote)
'Sets the footnote character format
footnote.MarkerCharacterFormat.SubSuperScript = SubSuperScript.SuperScript
'Inserts the text into the paragraph
paragraph.AppendText("Sample content for footnotes").CharacterFormat.Bold = True
'Adds footnote text
paragraph = footnote.TextBody.AddParagraph()
paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.")
‘Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx)
document.Close()

{% endhighlight %}

{% highlight ASP.NET CORE %}

//Creates a new instance of WordDocument (Empty Word Document)
using (WordDocument document = new WordDocument())
{
	//Creates a section
	IWSection section = document.AddSection();
	//Adds a paragraph to a section
	IWParagraph paragraph = section.AddParagraph();
	//Appends the text to paragraph
	paragraph.AppendText("Working with footnotes");
	//Formats the text
	paragraph.ApplyStyle(BuiltinStyle.Heading1);
	//Adds a paragraph to a section
	paragraph = section.AddParagraph();
	//Appends the footnotes
	WFootnote footnote = (WFootnote)paragraph.AppendFootnote(Syncfusion.DocIO.FootnoteType.Footnote);
	//Sets the footnote character format
	footnote.MarkerCharacterFormat.SubSuperScript = SubSuperScript.SuperScript;
	//Inserts the text into the paragraph
	paragraph.AppendText("Sample content for footnotes").CharacterFormat.Bold = true;
	//Adds footnote text
	paragraph = footnote.TextBody.AddParagraph();
	paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");
	MemoryStream stream = new MemoryStream();
	//Saves the Word document to  MemoryStream
	document.Save(stream, FormatType.Docx);
	document.Close();
	stream.Position = 0;
	//Download Word document in the browser
	return File(stream, "application/msword", "Result.docx");
}

{% endhighlight %}

{% highlight UWP %}

using (WordDocument document = new WordDocument())
{
	//Creates a section
	IWSection section = document.AddSection();
	//Adds a paragraph to a section
	IWParagraph paragraph = section.AddParagraph();
	//Appends the text to paragraph
	paragraph.AppendText("Working with footnotes");
	//Formats the text
	paragraph.ApplyStyle(BuiltinStyle.Heading1);
	//Adds a paragraph to a section
	paragraph = section.AddParagraph();
	//Appends the footnotes
	WFootnote footnote = (WFootnote)paragraph.AppendFootnote(Syncfusion.DocIO.FootnoteType.Footnote);
	//Sets the footnote character format
	footnote.MarkerCharacterFormat.SubSuperScript = SubSuperScript.SuperScript;
	//Inserts the text into the paragraph
	paragraph.AppendText("Sample content for footnotes").CharacterFormat.Bold = true;
	//Adds footnote text
	paragraph = footnote.TextBody.AddParagraph();
	paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");
	MemoryStream stream = new MemoryStream();
	//Saves the Word file to MemoryStream
	await document.SaveAsync(stream, FormatType.Docx);
	//Saves the stream as Word file in local machine
	Save(stream, "Result.docx");
	document.Close();
}

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
		savePicker.FileTypeChoices.Add("Word Documents", new List<string>() {".docx"});
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

{% highlight Xamarin %}

using (WordDocument document = new WordDocument())
{
	//Creates a section
	IWSection section = document.AddSection();
	//Adds a paragraph to a section
	IWParagraph paragraph = section.AddParagraph();
	//Appends the text to paragraph
	paragraph.AppendText("Working with footnotes");
	//Formats the text
	paragraph.ApplyStyle(BuiltinStyle.Heading1);
	//Adds a paragraph to a section
	paragraph = section.AddParagraph();
	//Appends the footnotes
	WFootnote footnote = (WFootnote)paragraph.AppendFootnote(Syncfusion.DocIO.FootnoteType.Footnote);
	//Sets the footnote character format
	footnote.MarkerCharacterFormat.SubSuperScript = SubSuperScript.SuperScript;
	//Inserts the text into the paragraph
	paragraph.AppendText("Sample content for footnotes").CharacterFormat.Bold = true;
	//Adds footnote text
	paragraph = footnote.TextBody.AddParagraph();
	paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");
	MemoryStream stream = new MemoryStream();
	document.Save(stream, FormatType.Docx);             
	//Save the stream as a file in the device and invoke it for viewing
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("WorkingWorddoc.docx", "application/msword", stream);
	//Closes the documents               
	document.Close();
}

{% endhighlight %}

{% endtabs %}

## Adding a Endnotes

The following code example shows how to insert the endnotes into the Word document.

{% tabs %}  

{% highlight c# %}

//Creates a new document
WordDocument document = new WordDocument();
//Creates a section
IWSection section = document.AddSection();
//Adds a paragraph to a section
IWParagraph paragraph = section.AddParagraph();
//Appends the text to paragraph
paragraph.AppendText("Working with footnotes");
//Formats the text
paragraph.ApplyStyle(BuiltinStyle.Heading1);
//Adds a paragraph to a section
paragraph = section.AddParagraph();
//Appends the endnote
WFootnote endnote = (WFootnote)  paragraph.AppendFootnote(Syncfusion.DocIO.FootnoteType.Endnote);
//Sets the endnote character format
endnote.MarkerCharacterFormat.SubSuperScript = SubSuperScript.SuperScript;
//Inserts the text into the paragraph
paragraph.AppendText("Sample content for endnotes").CharacterFormat.Bold = true;
//Adds footnote text
paragraph = endnote.TextBody.AddParagraph();
paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");
//Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx);
document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates a new document
Dim document As New WordDocument()
'Creates a section
Dim section As IWSection = document.AddSection()
'Adds a paragraph to a section
Dim paragraph As IWParagraph = section.AddParagraph()
'Appends the text to paragraph
paragraph.AppendText("Working with footnotes")
'Formats the text
paragraph.ApplyStyle(BuiltinStyle.Heading1)
'Adds a paragraph to a section
paragraph = section.AddParagraph()
'Appends the endnote
Dim endnote As WFootnote = DirectCast(paragraph.AppendFootnote(Syncfusion.DocIO.FootnoteType.Endnote), WFootnote)
'Sets the endnote character format
endnote.MarkerCharacterFormat.SubSuperScript = SubSuperScript.SuperScript
'Inserts the text into the paragraph
paragraph.AppendText("Sample content for endnotes").CharacterFormat.Bold = True
'Adds footnote text
paragraph = endnote.TextBody.AddParagraph()
paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.")
‘Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx)
document.Close()

{% endhighlight %}

{% highlight ASP.NET CORE %}

//Creates a new instance of WordDocument (Empty Word Document)
using (WordDocument document = new WordDocument())
{
	//Creates a section
	IWSection section = document.AddSection();
	//Adds a paragraph to a section
	IWParagraph paragraph = section.AddParagraph();
	//Appends the text to paragraph
	paragraph.AppendText("Working with footnotes");
	//Formats the text
	paragraph.ApplyStyle(BuiltinStyle.Heading1);
	//Adds a paragraph to a section
	paragraph = section.AddParagraph();
	//Appends the endnotes
	WFootnote endnote = (WFootnote)paragraph.AppendFootnote(Syncfusion.DocIO.FootnoteType.Endnote);
	//Sets the endnote character format
	endnote.MarkerCharacterFormat.SubSuperScript = SubSuperScript.SuperScript;
	//Inserts the text into the paragraph
	paragraph.AppendText("Sample content for endnotes").CharacterFormat.Bold = true;
	//Adds endnote text
	paragraph = endnote.TextBody.AddParagraph();
	paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");
	MemoryStream stream = new MemoryStream();
	//Saves the Word document to  MemoryStream
	document.Save(stream, FormatType.Docx);
	document.Close();
	stream.Position = 0;
	//Download Word document in the browser
	return File(stream, "application/msword", "Result.docx");
}

{% endhighlight %}

{% highlight UWP %}

using (WordDocument document = new WordDocument())
{
	//Creates a section
	IWSection section = document.AddSection();
	//Adds a paragraph to a section
	IWParagraph paragraph = section.AddParagraph();
	//Appends the text to paragraph
	paragraph.AppendText("Working with footnotes");
	//Formats the text
	paragraph.ApplyStyle(BuiltinStyle.Heading1);
	//Adds a paragraph to a section
	paragraph = section.AddParagraph();
	//Appends the endnotes
	WFootnote endnote = (WFootnote)paragraph.AppendFootnote(Syncfusion.DocIO.FootnoteType.Endnote);
	//Sets the endnote character format
	endnote.MarkerCharacterFormat.SubSuperScript = SubSuperScript.SuperScript;
	//Inserts the text into the paragraph
	paragraph.AppendText("Sample content for footnotes").CharacterFormat.Bold = true;
	//Adds endnote text
	paragraph = endnote.TextBody.AddParagraph();
	paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");
	MemoryStream stream = new MemoryStream();
	//Saves the Word file to MemoryStream
	await document.SaveAsync(stream, FormatType.Docx);
	//Saves the stream as Word file in local machine
	Save(stream, "Result.docx");
	document.Close();
}

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
		savePicker.FileTypeChoices.Add("Word Documents", new List<string>() {".docx"});
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

{% highlight Xamarin %}

using (WordDocument document = new WordDocument())
{
	//Creates a section
	IWSection section = document.AddSection();
	//Adds a paragraph to a section
	IWParagraph paragraph = section.AddParagraph();
	//Appends the text to paragraph
	paragraph.AppendText("Working with footnotes");
	//Formats the text
	paragraph.ApplyStyle(BuiltinStyle.Heading1);
	//Adds a paragraph to a section
	paragraph = section.AddParagraph();
	//Appends the endnotes
	WFootnote endnote = (WFootnote)paragraph.AppendFootnote(Syncfusion.DocIO.FootnoteType.Endnote);
	//Sets the endnote character format
	endnote.MarkerCharacterFormat.SubSuperScript = SubSuperScript.SuperScript;
	//Inserts the text into the paragraph
	paragraph.AppendText("Sample content for footnotes").CharacterFormat.Bold = true;
	//Adds endnote text
	paragraph = endnote.TextBody.AddParagraph();
	paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");
	MemoryStream stream = new MemoryStream();
	document.Save(stream, FormatType.Docx);    
	//Save the stream as a file in the device and invoke it for viewing
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("WorkingWorddoc.docx", "application/msword", stream);
	//Closes the documents               
	document.Close();
}

{% endhighlight %}

{% endtabs %}  
   
## Footnote and Endnote separators

Footnote/Endnote separator is used to separate the text body content and footnote/endnote by a small line. 

A footnote/endnote continuation separator is used to indicate the footnote/endnote is carried over from the previous page by a line running across the top section. 

A footnote/endnote continuation notice is used to indicate the footnote/endnote is continued to the next page by special character or word preserved at the bottom of the footer.

The following code example shows how to change the default footnote separator.

{% tabs %} 

{% highlight c# %}

//Creates a new Word document
WordDocument document = new WordDocument();
//Creates a section
IWSection section = document.AddSection();
//Adds a paragraph to a section
IWParagraph paragraph = section.AddParagraph();
//Appends the text to paragraph
paragraph.AppendText("Working with footnotes");
//Formats the text
paragraph.ApplyStyle(BuiltinStyle.Heading1);
//Adds a paragraph to a section
paragraph = section.AddParagraph();
//Appends the footnotes
WFootnote footnote = (WFootnote)paragraph.AppendFootnote(Syncfusion.DocIO.FootnoteType.Footnote);
WTextBody separator = document.Footnotes.Separator;
//Replaces the default footnote separated by text
separator.Paragraphs[0].Text = "Footnote separator";
//Sets the footnote character format
footnote.MarkerCharacterFormat.SubSuperScript = SubSuperScript.SuperScript;
//Inserts the text into the paragraph
paragraph.AppendText("Sample content for footnotes").CharacterFormat.Bold = true;
//Adds footnote text
paragraph = footnote.TextBody.AddParagraph();
paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");
//Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx);
document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates a new Word document
Dim document As New WordDocument()
'Creates a section
Dim section As IWSection = document.AddSection()
'Adds a paragraph to a section
Dim paragraph As IWParagraph = section.AddParagraph()
'Appends the text to paragraph
paragraph.AppendText("Working with footnotes")
'Formats the text
paragraph.ApplyStyle(BuiltinStyle.Heading1)
'Adds a paragraph to a section
paragraph = section.AddParagraph()
'Appends the footnotes
Dim footnote As WFootnote = DirectCast(paragraph.AppendFootnote(Syncfusion.DocIO.FootnoteType.Footnote), WFootnote)
Dim separator As WTextBody = document.Footnotes.Separator
'Replaces the default footnote separated by text
separator.Paragraphs(0).Text = "Footnote separator"
'Sets the footnote character format
footnote.MarkerCharacterFormat.SubSuperScript = SubSuperScript.SuperScript
'Inserts the text into the paragraph
paragraph.AppendText("Sample content for footnotes").CharacterFormat.Bold = True
'Adds footnote text
paragraph = footnote.TextBody.AddParagraph()
paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.")
‘Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx)
document.Close()

{% endhighlight %}  

{% highlight ASP.NET CORE %}

//Creates a new instance of WordDocument (Empty Word Document)
using (WordDocument document = new WordDocument())
{
	//Creates a section
	IWSection section = document.AddSection();
	//Adds a paragraph to a section
	IWParagraph paragraph = section.AddParagraph();
	//Appends the text to paragraph
	paragraph.AppendText("Working with footnotes");
	//Formats the text
	paragraph.ApplyStyle(BuiltinStyle.Heading1);
	//Adds a paragraph to a section
	paragraph = section.AddParagraph();
	//Appends the footnotes
	WFootnote footnote = (WFootnote)paragraph.AppendFootnote(Syncfusion.DocIO.FootnoteType.Footnote);
	WTextBody separator = document.Footnotes.Separator;
	//Replaces the default footnote separated by text
	separator.Paragraphs[0].Text = "Footnote separator";
	//Sets the footnote character format
	footnote.MarkerCharacterFormat.SubSuperScript = SubSuperScript.SuperScript;
	//Inserts the text into the paragraph
	paragraph.AppendText("Sample content for endnotes").CharacterFormat.Bold = true;
	//Adds footnote text
	paragraph = footnote.TextBody.AddParagraph();
	paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");
	MemoryStream stream = new MemoryStream();
	//Saves the Word document to  MemoryStream
	document.Save(stream, FormatType.Docx);
	document.Close();
	stream.Position = 0;
	//Download Word document in the browser
	return File(stream, "application/msword", "Result.docx");
}

{% endhighlight %}

{% highlight UWP %}

using (WordDocument document = new WordDocument())
{
	//Creates a section
	IWSection section = document.AddSection();
	//Adds a paragraph to a section
	IWParagraph paragraph = section.AddParagraph();
	//Appends the text to paragraph
	paragraph.AppendText("Working with footnotes");
	//Formats the text
	paragraph.ApplyStyle(BuiltinStyle.Heading1);
	//Adds a paragraph to a section
	paragraph = section.AddParagraph();
	//Appends the footnotes
	WFootnote footnote = (WFootnote)paragraph.AppendFootnote(Syncfusion.DocIO.FootnoteType.Footnote);
	WTextBody separator = document.Footnotes.Separator;
	//Replaces the default footnote separated by text
	separator.Paragraphs[0].Text = "Footnote separator";
	//Sets the footnote character format
	footnote.MarkerCharacterFormat.SubSuperScript = SubSuperScript.SuperScript;
	//Inserts the text into the paragraph
	paragraph.AppendText("Sample content for endnotes").CharacterFormat.Bold = true;
	//Adds footnote text
	paragraph = footnote.TextBody.AddParagraph();
	paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");
	MemoryStream stream = new MemoryStream();
	//Saves the Word file to MemoryStream
	await document.SaveAsync(stream, FormatType.Docx);
	//Saves the stream as Word file in local machine
	Save(stream, "Result.docx");
	document.Close();
}

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
		savePicker.FileTypeChoices.Add("Word Documents", new List<string>() {".docx"});
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

{% highlight Xamarin %}

using (WordDocument document = new WordDocument())
{
	//Creates a section
	IWSection section = document.AddSection();
	//Adds a paragraph to a section
	IWParagraph paragraph = section.AddParagraph();
	//Appends the text to paragraph
	paragraph.AppendText("Working with footnotes");
	//Formats the text
	paragraph.ApplyStyle(BuiltinStyle.Heading1);
	//Adds a paragraph to a section
	paragraph = section.AddParagraph();
	//Appends the footnotes
	WFootnote footnote = (WFootnote)paragraph.AppendFootnote(Syncfusion.DocIO.FootnoteType.Footnote);
	WTextBody separator = document.Footnotes.Separator;
	//Replaces the default footnote separated by text
	separator.Paragraphs[0].Text = "Footnote separator";
	//Sets the footnote character format
	footnote.MarkerCharacterFormat.SubSuperScript = SubSuperScript.SuperScript;
	//Inserts the text into the paragraph
	paragraph.AppendText("Sample content for endnotes").CharacterFormat.Bold = true;
	//Adds footnote text
	paragraph = footnote.TextBody.AddParagraph();
	paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");
	MemoryStream stream = new MemoryStream();
	document.Save(stream, FormatType.Docx);         
	//Save the stream as a file in the device and invoke it for viewing     
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("WorkingWorddoc.docx", "application/msword", stream);
	//Closes the documents               
	document.Close();
}

{% endhighlight %}

{% endtabs %}  

The following code example shows how to change the default endnote separator.

{% tabs %} 

{% highlight c# %}

//Creates a new Word document
WordDocument document = new WordDocument();
//Creates a section
IWSection section = document.AddSection();
//Adds a paragraph to a section
IWParagraph paragraph = section.AddParagraph();
//Appends the text to paragraph
paragraph.AppendText("Working with footnotes");
//Formats the text
paragraph.ApplyStyle(BuiltinStyle.Heading1);
//Adds a paragraph to  section
paragraph = section.AddParagraph();
//Appends the endnote
WFootnote endnote = (WFootnote)paragraph.AppendFootnote(Syncfusion.DocIO.FootnoteType.Endnote);
WTextBody separator = document.Endnotes.Separator;
//Replaces the default foot note separate by text
separator.Paragraphs[0].Text = "Endnote separator";
//Sets the endnote character format
endnote.MarkerCharacterFormat.SubSuperScript = SubSuperScript.SuperScript;
//Inserts the text into the paragraph
paragraph.AppendText("Sample content for endnotes").CharacterFormat.Bold = true;
//Adds the footnote text
paragraph = endnote.TextBody.AddParagraph();
paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");
//Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx);
document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates a new Word document
Dim document As New WordDocument()
'Creates a section
Dim section As IWSection = document.AddSection()
'Adds a paragraph to a section
Dim paragraph As IWParagraph = section.AddParagraph()
'Appends the text to paragraph
paragraph.AppendText("Working with footnotes")
'Formats the text
paragraph.ApplyStyle(BuiltinStyle.Heading1)
'Adds a paragraph to  section
paragraph = section.AddParagraph()
'Appends the endnote
Dim endnote As WFootnote = DirectCast(paragraph.AppendFootnote(Syncfusion.DocIO.FootnoteType.Endnote), WFootnote)
Dim separator As WTextBody = document.Endnotes.Separator
'Replaces the default footnote separated by text
separator.Paragraphs(0).Text = "Endnote separator"
'Sets the endnote character format
endnote.MarkerCharacterFormat.SubSuperScript = SubSuperScript.SuperScript
'Inserts the text into the paragraph
paragraph.AppendText("Sample content for endnotes").CharacterFormat.Bold = True
'Adds the footnote text
paragraph = endnote.TextBody.AddParagraph()
paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.")
‘Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx)
document.Close()

{% endhighlight %}

{% highlight ASP.NET CORE %}

//Creates a new instance of WordDocument (Empty Word Document)
using (WordDocument document = new WordDocument())
{
	//Creates a section
	IWSection section = document.AddSection();
	//Adds a paragraph to a section
	IWParagraph paragraph = section.AddParagraph();
	//Appends the text to paragraph
	paragraph.AppendText("Working with footnotes");
	//Formats the text
	paragraph.ApplyStyle(BuiltinStyle.Heading1);
	//Adds a paragraph to a section
	paragraph = section.AddParagraph();
	//Appends the endnotes
	WFootnote endnote = (WFootnote)paragraph.AppendFootnote(Syncfusion.DocIO.FootnoteType.Endnote);
	WTextBody separator = document.Endnotes.Separator;
	//Replaces the default endnote separated by text
	separator.Paragraphs[0].Text = "Endnote separator";
	//Sets the endnote character format
	endnote.MarkerCharacterFormat.SubSuperScript = SubSuperScript.SuperScript;
	//Inserts the text into the paragraph
	paragraph.AppendText("Sample content for endnotes").CharacterFormat.Bold = true;
	//Adds endnote text
	paragraph = endnote.TextBody.AddParagraph();
	paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");
	MemoryStream stream = new MemoryStream();
	//Saves the Word document to  MemoryStream
	document.Save(stream, FormatType.Docx);
	document.Close();
	stream.Position = 0;
	//Download Word document in the browser
	return File(stream, "application/msword", "Result.docx");
}

{% endhighlight %}

{% highlight UWP %}

using (WordDocument document = new WordDocument())
{
	//Creates a section
	IWSection section = document.AddSection();
	//Adds a paragraph to a section
	IWParagraph paragraph = section.AddParagraph();
	//Appends the text to paragraph
	paragraph.AppendText("Working with footnotes");
	//Formats the text
	paragraph.ApplyStyle(BuiltinStyle.Heading1);
	//Adds a paragraph to a section
	paragraph = section.AddParagraph();
	//Appends the endnotes
	WFootnote endnote = (WFootnote)paragraph.AppendFootnote(Syncfusion.DocIO.FootnoteType.Endnote);
	WTextBody separator = document.Endnotes.Separator;
	//Replaces the default endnote separated by text
	separator.Paragraphs[0].Text = "Endnote separator";
	//Sets the endnote character format
	endnote.MarkerCharacterFormat.SubSuperScript = SubSuperScript.SuperScript;
	//Inserts the text into the paragraph
	paragraph.AppendText("Sample content for endnotes").CharacterFormat.Bold = true;
	//Adds endnote text
	paragraph = endnote.TextBody.AddParagraph();
	paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");
	MemoryStream stream = new MemoryStream();
	//Saves the Word file to MemoryStream
	await document.SaveAsync(stream, FormatType.Docx);
	//Saves the stream as Word file in local machine
	Save(stream, "Result.docx");
	document.Close();
}

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
		savePicker.FileTypeChoices.Add("Word Documents", new List<string>() {".docx"});
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

{% highlight Xamarin %}

using (WordDocument document = new WordDocument())
{
	//Creates a section
	IWSection section = document.AddSection();
	//Adds a paragraph to a section
	IWParagraph paragraph = section.AddParagraph();
	//Appends the text to paragraph
	paragraph.AppendText("Working with footnotes");
	//Formats the text
	paragraph.ApplyStyle(BuiltinStyle.Heading1);
	//Adds a paragraph to a section
	paragraph = section.AddParagraph();
	//Appends the endnotes
	WFootnote endnote = (WFootnote)paragraph.AppendFootnote(Syncfusion.DocIO.FootnoteType.Endnote);
	WTextBody separator = document.Endnotes.Separator;
	//Replaces the default endnote separated by text
	separator.Paragraphs[0].Text = "Endnote separator";
	//Sets the endnote character format
	endnote.MarkerCharacterFormat.SubSuperScript = SubSuperScript.SuperScript;
	//Inserts the text into the paragraph
	paragraph.AppendText("Sample content for endnotes").CharacterFormat.Bold = true;
	//Adds endnote text
	paragraph = endnote.TextBody.AddParagraph();
	paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");
	MemoryStream stream = new MemoryStream();
	document.Save(stream, FormatType.Docx);            
	//Save the stream as a file in the device and invoke it for viewing
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("WorkingWorddoc.docx", "application/msword", stream);
	//Closes the documents               
	document.Close();
}

{% endhighlight %}

{% endtabs %}