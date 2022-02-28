---
title: Working with Footnotes and endnotes | DocIO | Syncfusion
description: This section illustrates about working with adding and removing a footnote and endnote in a Word document using DocIO
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
	//Please refer the below link to save Word document in UWP platform
	//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
}
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
	//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
	//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
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
paragraph.AppendText("Working with endnotes");
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
paragraph.AppendText("Working with endnotes")
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

{% highlight UWP %}
using (WordDocument document = new WordDocument())
{
	//Creates a section
	IWSection section = document.AddSection();
	//Adds a paragraph to a section
	IWParagraph paragraph = section.AddParagraph();
	//Appends the text to paragraph
	paragraph.AppendText("Working with endnotes");
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
	//Saves the Word file to MemoryStream
	await document.SaveAsync(stream, FormatType.Docx);
	//Saves the stream as Word file in local machine
	Save(stream, "Result.docx");
	document.Close();
	//Please refer the below link to save Word document in UWP platform
	//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
}
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
	paragraph.AppendText("Working with endnotes");
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

{% highlight Xamarin %}
using (WordDocument document = new WordDocument())
{
	//Creates a section
	IWSection section = document.AddSection();
	//Adds a paragraph to a section
	IWParagraph paragraph = section.AddParagraph();
	//Appends the text to paragraph
	paragraph.AppendText("Working with endnotes");
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
	document.Save(stream, FormatType.Docx);    
	//Save the stream as a file in the device and invoke it for viewing
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("WorkingWorddoc.docx", "application/msword", stream);
	//Closes the documents               
	document.Close();
	//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
	//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
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
	//Please refer the below link to save Word document in UWP platform
	//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
}
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
	//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
	//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
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
	//Please refer the below link to save Word document in UWP platform
	//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
}
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
	//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
	//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
}
{% endhighlight %}

{% endtabs %}

## Removing a Footnotes/Endnotes

The following code example shows how to remove the footnotes/endnotes from the Word document.

{% tabs %} 

{% highlight c# %}
//Loads the template document
WordDocument document = new WordDocument("Footnote.docx");
//Removes footnote/endnote from the document
RemoveFootNoteEndNote(document);
//Saves and closes the Word document
document.Save("Result.docx", FormatType.Docx);
document.Close();


private static void RemoveFootNoteEndNote(WordDocument document)
{
    foreach (WSection section in document.Sections)
    {
        RemoveFootNoteEndNote(section.Body);
    }
}
private static void RemoveFootNoteEndNote(WTextBody textBody)
{
    for (int i = 0; i < textBody.ChildEntities.Count; i++)
    {
        //IEntity is the basic unit in DocIO DOM. 
        //Accesses the body items as IEntity
        IEntity bodyItemEntity = textBody.ChildEntities[i];
        //A Text body has 3 types of elements - Paragraph, Table and Block Content Control
        //Decides the element type by using EntityType
        switch (bodyItemEntity.EntityType)
        {
            case EntityType.Paragraph:
                WParagraph paragraph = bodyItemEntity as WParagraph;
                for (int j = 0; j < paragraph.ChildEntities.Count; j++)
                {
                    if (paragraph.ChildEntities[j] is WFootnote)
                    {
                        paragraph.ChildEntities.RemoveAt(j);
                    }
                }
                break;
            case EntityType.Table:
                //Table is a collection of rows and cells
                //Iterates through table's DOM and and Remove footnote.
                RemoveFootNoteEndNote(bodyItemEntity as WTable);
                break;
            case EntityType.BlockContentControl:
                BlockContentControl blockContentControl = bodyItemEntity as BlockContentControl;
                //Iterates to the body items of Block Content Control and Remove footnote.
                RemoveFootNoteEndNote(blockContentControl.TextBody);
                break;
        }
    }
}

private static void RemoveFootNoteEndNote(WTable table)
{
    //Iterates the row collection in a table.
    foreach (WTableRow row in table.Rows)
    {
        //Iterates the cell collection in a table row.
        foreach (WTableCell cell in row.Cells)
        {
            //Iterate items in cell and and Remove footnote.
            RemoveFootNoteEndNote(cell);
        }
    }
}
{% endhighlight %}

{% highlight vb.net %}
'Loads the template document
Dim document As New WordDocument("Footnote.docx")
'Removes footnote from the document
RemoveFootNoteEndNote(document);
'Saves and closes the Word document
document.Save("Result.docx", FormatType.Docx)
document.Close()

Private Shared Sub RemoveFootNoteEndNote(ByVal document As WordDocument)
    For Each section As WSection In document.Sections
        RemoveFootNoteEndNote(section.Body)
    Next
End Sub
	
Private Shared Sub RemoveFootNoteEndNote(ByVal textBody As WTextBody)
    For i As Integer = 0 To textBody.ChildEntities.Count - 1
	    'IEntity is the basic unit in DocIO DOM. 
        'Accesses the body items as IEntity
        Dim bodyItemEntity As IEntity = textBody.ChildEntities(i)
		'A Text body has 3 types of elements - Paragraph, Table and Block Content Control
        'Decides the element type by using EntityType
        Select Case bodyItemEntity.EntityType
            Case EntityType.Paragraph
                Dim paragraph As WParagraph = TryCast(bodyItemEntity, WParagraph)
                For j As Integer = 0 To paragraph.ChildEntities.Count - 1
                    If TypeOf paragraph.ChildEntities(j) Is WFootnote Then
                        paragraph.ChildEntities.RemoveAt(j)
                    End If
                Next
            Case EntityType.Table
			    'Table is a collection of rows and cells
                'Iterates through table's DOM and and Remove footnote.
                RemoveFootNoteEndNote(TryCast(bodyItemEntity, WTable))
            Case EntityType.BlockContentControl			    
                Dim blockContentControl As BlockContentControl = TryCast(bodyItemEntity, BlockContentControl)
				'Iterates to the body items of Block Content Control and Remove footnote.
                RemoveFootNoteEndNote(blockContentControl.TextBody)
        End Select
    Next
End Sub
	
Private Shared Sub RemoveFootNoteEndNote(ByVal table As WTable)
    'Iterates the row collection in a table.
    For Each row As WTableRow In table.Rows
	    'Iterates the cell collection in a table row.
        For Each cell As WTableCell In row.Cells
		    'Iterate items in cell and and Remove footnote.
            RemoveFootNoteEndNote(cell)
        Next
    Next
End Sub
{% endhighlight %}

{% highlight UWP %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Loads the template document as stream
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Footnote.docx"), FormatType.Docx);
//Removes footnote from the document
RemoveFootNoteEndNote(document);
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Closes the document
document.Close();
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp


private static void RemoveFootNoteEndNote(WordDocument document)
{
    foreach (WSection section in document.Sections)
    {
        RemoveFootNoteEndNote(section.Body);
    }
}
private static void RemoveFootNoteEndNote(WTextBody textBody)
{
    for (int i = 0; i < textBody.ChildEntities.Count; i++)
    {
        //IEntity is the basic unit in DocIO DOM. 
        //Accesses the body items as IEntity
        IEntity bodyItemEntity = textBody.ChildEntities[i];
        //A Text body has 3 types of elements - Paragraph, Table and Block Content Control
        //Decides the element type by using EntityType
        switch (bodyItemEntity.EntityType)
        {
            case EntityType.Paragraph:
                WParagraph paragraph = bodyItemEntity as WParagraph;
                for (int j = 0; j < paragraph.ChildEntities.Count; j++)
                {
                    if (paragraph.ChildEntities[j] is WFootnote)
                    {
                        paragraph.ChildEntities.RemoveAt(j);
                    }
                }
                break;
            case EntityType.Table:
                //Table is a collection of rows and cells
                //Iterates through table's DOM and and Remove footnote.
                RemoveFootNoteEndNote(bodyItemEntity as WTable);
                break;
            case EntityType.BlockContentControl:
                BlockContentControl blockContentControl = bodyItemEntity as BlockContentControl;
                //Iterates to the body items of Block Content Control and Remove footnote.
                RemoveFootNoteEndNote(blockContentControl.TextBody);
                break;
        }
    }
}

private static void RemoveFootNoteEndNote(WTable table)
{
    //Iterates the row collection in a table.
    foreach (WTableRow row in table.Rows)
    {
        //Iterates the cell collection in a table row.
        foreach (WTableCell cell in row.Cells)
        {
            //Iterate items in cell and and Remove footnote.
            RemoveFootNoteEndNote(cell);
        }
    }
}
{% endhighlight %}

{% highlight ASP.NET CORE %}
FileStream inputStream = new FileStream("Footnote.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
//Loads the template document as stream
WordDocument document = new WordDocument(inputStream, FormatType.Docx);
inputStream.Dispose();
//Removes footnote from the document
RemoveFootNoteEndNote(document);
//Saves the Word document to MemoryStream
FileStream outputStream = new FileStream("Result.docx", FileMode.OpenOrCreate, FileAccess.ReadWrite);
document.Save(outputStream, FormatType.Docx);
//Closes the document
document.Close();
outputStream.Dispose();


private static void RemoveFootNoteEndNote(WordDocument document)
{
    foreach (WSection section in document.Sections)
    {
        RemoveFootNoteEndNote(section.Body);
    }
}
private static void RemoveFootNoteEndNote(WTextBody textBody)
{
    for (int i = 0; i < textBody.ChildEntities.Count; i++)
    {
        //IEntity is the basic unit in DocIO DOM. 
        //Accesses the body items as IEntity
        IEntity bodyItemEntity = textBody.ChildEntities[i];
        //A Text body has 3 types of elements - Paragraph, Table and Block Content Control
        //Decides the element type by using EntityType
        switch (bodyItemEntity.EntityType)
        {
            case EntityType.Paragraph:
                WParagraph paragraph = bodyItemEntity as WParagraph;
                for (int j = 0; j < paragraph.ChildEntities.Count; j++)
                {
                    if (paragraph.ChildEntities[j] is WFootnote)
                    {
                        paragraph.ChildEntities.RemoveAt(j);
                    }
                }
                break;
            case EntityType.Table:
                //Table is a collection of rows and cells
                //Iterates through table's DOM and and Remove footnote.
                RemoveFootNoteEndNote(bodyItemEntity as WTable);
                break;
            case EntityType.BlockContentControl:
                BlockContentControl blockContentControl = bodyItemEntity as BlockContentControl;
                //Iterates to the body items of Block Content Control and Remove footnote.
                RemoveFootNoteEndNote(blockContentControl.TextBody);
                break;
        }
    }
}

private static void RemoveFootNoteEndNote(WTable table)
{
    //Iterates the row collection in a table.
    foreach (WTableRow row in table.Rows)
    {
        //Iterates the cell collection in a table row.
        foreach (WTableCell cell in row.Cells)
        {
            //Iterate items in cell and and Remove footnote.
            RemoveFootNoteEndNote(cell);
        }
    }
}
{% endhighlight %}

{% highlight XAMARIN %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Loads the template document as stream
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Data.Footnote.docx"), FormatType.Docx);
//Removes footnote from the document
RemoveFootNoteEndNote(document);
//Saves the Word document to  MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin


private static void RemoveFootNoteEndNote(WordDocument document)
{
    foreach (WSection section in document.Sections)
    {
        RemoveFootNoteEndNote(section.Body);
    }
}
private static void RemoveFootNoteEndNote(WTextBody textBody)
{
    for (int i = 0; i < textBody.ChildEntities.Count; i++)
    {
        //IEntity is the basic unit in DocIO DOM. 
        //Accesses the body items as IEntity
        IEntity bodyItemEntity = textBody.ChildEntities[i];
        //A Text body has 3 types of elements - Paragraph, Table and Block Content Control
        //Decides the element type by using EntityType
        switch (bodyItemEntity.EntityType)
        {
            case EntityType.Paragraph:
                WParagraph paragraph = bodyItemEntity as WParagraph;
                for (int j = 0; j < paragraph.ChildEntities.Count; j++)
                {
                    if (paragraph.ChildEntities[j] is WFootnote)
                    {
                        paragraph.ChildEntities.RemoveAt(j);
                    }
                }
                break;
            case EntityType.Table:
                //Table is a collection of rows and cells
                //Iterates through table's DOM and and Remove footnote.
                RemoveFootNoteEndNote(bodyItemEntity as WTable);
                break;
            case EntityType.BlockContentControl:
                BlockContentControl blockContentControl = bodyItemEntity as BlockContentControl;
                //Iterates to the body items of Block Content Control and Remove footnote.
                RemoveFootNoteEndNote(blockContentControl.TextBody);
                break;
        }
    }
}

private static void RemoveFootNoteEndNote(WTable table)
{
    //Iterates the row collection in a table.
    foreach (WTableRow row in table.Rows)
    {
        //Iterates the cell collection in a table row.
        foreach (WTableCell cell in row.Cells)
        {
            //Iterate items in cell and and Remove footnote.
            RemoveFootNoteEndNote(cell);
        }
    }
}
{% endhighlight %}

{% endtabs %}