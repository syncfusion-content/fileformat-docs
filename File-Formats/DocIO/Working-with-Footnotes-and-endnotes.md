---
title: Working with Footnotes and endnotes | DocIO | Syncfusion
description: Learn how to add, modify, and remove footnotes and endnotes in a Word document using the .NET Word (DocIO) library without Microsoft Word.
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

{% highlight c# tabtitle="C# [Cross-platform]" %}
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
    //Saves the Word document to  MemoryStream
    MemoryStream stream = new MemoryStream();
    document.Save(stream, FormatType.Docx);
    document.Close();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Footnotes-and-Endnotes/Add-footnotes-in-Word-document).

## Adding a Endnotes

The following code example shows how to insert the endnotes into the Word document.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
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
    //Saves the Word document to  MemoryStream
    MemoryStream stream = new MemoryStream();
    document.Save(stream, FormatType.Docx);
    document.Close();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Footnotes-and-Endnotes/Add-endnotes-in-Word-document).

## Set Footnotes and Endnotes position

Footnotes are typically located at the bottom of a page or beneath the text being referenced, and endnotes are typically placed at the end of a document or at the end of a section. This can be done using [FootnotePosition](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WordDocument.html#Syncfusion_DocIO_DLS_WordDocument_FootnotePosition) API and [EndnotePosition](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WordDocument.html#Syncfusion_DocIO_DLS_WordDocument_EndnotePosition) API.

The following code example illustrates how to set positions for footnotes and endnotes:

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Create a new Word document.
using (WordDocument document = new WordDocument())
{
    //Create a section.
    IWSection section = document.AddSection();
    //Add a paragraph to a section.
    IWParagraph paragraph = section.AddParagraph();
    //Append the text to the paragraph.
    paragraph.AppendText("First paragraph in First section");
    //Append the footnote.
    WFootnote footnote = paragraph.AppendFootnote(FootnoteType.Footnote) as WFootnote;
    //Set the footnote character format.
    footnote.MarkerCharacterFormat.SubSuperScript = SubSuperScript.SuperScript;
    //Set the numbering format for the footnote.
    document.FootnoteNumberFormat = FootEndNoteNumberFormat.Arabic;
    //Add footnote text.
    paragraph = footnote.TextBody.AddParagraph();
    paragraph.AppendText("Footnote content");
    //Set the footnote position.
    document.FootnotePosition = FootnotePosition.PrintImmediatelyBeneathText;
    //Add the new section to the document.
    section = document.AddSection();
    //Add a paragraph to a section.
    paragraph = section.AddParagraph();
    //Append text into the paragraph.
    paragraph.AppendText("Paragraph in Second section.");
    //Append the endnote.
    WFootnote endnote = paragraph.AppendFootnote(FootnoteType.Endnote) as WFootnote;
    //Set the endnote character format.
    endnote.MarkerCharacterFormat.SubSuperScript = SubSuperScript.SuperScript;
    //Set the numbering format for the endnote.
    document.EndnoteNumberFormat = FootEndNoteNumberFormat.LowerCaseRoman;
    //Add endnote text.
    paragraph = endnote.TextBody.AddParagraph();
    paragraph.AppendText("Endnote of second section");
    //Set the endnote position.
    document.EndnotePosition = EndnotePosition.DisplayEndOfSection;
    //Add the new section to the document.
    section = document.AddSection();
    //Set a section break.
    section.BreakCode = SectionBreakCode.NoBreak;
    //Add a new paragraph to a section.
    paragraph = section.AddParagraph();
    //Append text into the paragraph.
    paragraph.AppendText("Paragraph in third Section.");
    //Save the Word document to MemoryStream.
    MemoryStream outputStream = new MemoryStream();
    document.Save(outputStream, FormatType.Docx);
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Create a new Word document.
using (WordDocument document = new WordDocument())
{
    //Create a section.
    IWSection section = document.AddSection();
    //Add a paragraph to a section.
    IWParagraph paragraph = section.AddParagraph();
    //Append the text to the paragraph.
    paragraph.AppendText("First paragraph in First section");
    //Append the footnote.
    WFootnote footnote = paragraph.AppendFootnote(FootnoteType.Footnote) as WFootnote;
    //Set the footnote character format.
    footnote.MarkerCharacterFormat.SubSuperScript = SubSuperScript.SuperScript;
    //Set the numbering format for the footnote.
    document.FootnoteNumberFormat = FootEndNoteNumberFormat.Arabic;
    //Add footnote text.
    paragraph = footnote.TextBody.AddParagraph();
    paragraph.AppendText("Footnote content");
    //Set the footnote position.
    document.FootnotePosition = FootnotePosition.PrintImmediatelyBeneathText;
    //Add the new section to the document.
    section = document.AddSection();
    //Add a paragraph to a section.
    paragraph = section.AddParagraph();
    //Append text into the paragraph.
    paragraph.AppendText("Paragraph in Second section.");
    //Append the endnote.
    WFootnote endnote = paragraph.AppendFootnote(FootnoteType.Endnote) as WFootnote;
    //Set the endnote character format.
    endnote.MarkerCharacterFormat.SubSuperScript = SubSuperScript.SuperScript;
    //Set the numbering format for the endnote.
    document.EndnoteNumberFormat = FootEndNoteNumberFormat.LowerCaseRoman;
    //Add endnote text.
    paragraph = endnote.TextBody.AddParagraph();
    paragraph.AppendText("Endnote of second section");
    //Set the endnote position.
    document.EndnotePosition = EndnotePosition.DisplayEndOfSection;
    //Add the new section to the document.
    section = document.AddSection();
    //Set a section break.
    section.BreakCode = SectionBreakCode.NoBreak;
    //Add a new paragraph to a section.
    paragraph = section.AddParagraph();
    //Append text into the paragraph.
    paragraph.AppendText("Paragraph in third Section.");
    //Save the Word document.
    document.Save("Sample.docx", FormatType.Docx);
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Create a new Word document.
Using document As WordDocument = New WordDocument()
    'Create a section.
    Dim section As IWSection = document.AddSection()
    'Add a paragraph to a section.
    Dim paragraph As IWParagraph = section.AddParagraph()
    'Append the text to the paragraph.
    paragraph.AppendText("First paragraph in First section")
    'Append the footnote.
    Dim footnote As WFootnote = TryCast(paragraph.AppendFootnote(FootnoteType.Footnote), WFootnote)
    'Set the footnote character format.
    footnote.MarkerCharacterFormat.SubSuperScript = SubSuperScript.SuperScript
    'Set the numbering format for the footnote.
    document.FootnoteNumberFormat = FootEndNoteNumberFormat.Arabic
    'Add footnote text.
    paragraph = footnote.TextBody.AddParagraph()
    paragraph.AppendText("Footnote content")
    'Set the footnote position.
    document.FootnotePosition = FootnotePosition.PrintImmediatelyBeneathText
    'Add the new section to the document.
    section = document.AddSection()
    'Add a paragraph to a section.
    paragraph = section.AddParagraph()
    'Append text into the paragraph.
    paragraph.AppendText("Paragraph in Second section.")
    'Append the endnote.
    Dim endnote As WFootnote = TryCast(paragraph.AppendFootnote(FootnoteType.Endnote), WFootnote)
    'Set the endnote character format.
    endnote.MarkerCharacterFormat.SubSuperScript = SubSuperScript.SuperScript
    'Set the numbering format for the endnote.
    document.EndnoteNumberFormat = FootEndNoteNumberFormat.LowerCaseRoman
    'Add endnote text.
    paragraph = endnote.TextBody.AddParagraph()
    paragraph.AppendText("Endnote of second section")
    'Set the endnote position.
    document.EndnotePosition = EndnotePosition.DisplayEndOfSection
    'Add the new section to the document.
    section = document.AddSection()
    'Set a section break.
    section.BreakCode = SectionBreakCode.NoBreak
    'Add a new paragraph to a section.
    paragraph = section.AddParagraph()
    'Append text into the paragraph.
    paragraph.AppendText("Paragraph in third Section.")
    'Save the Word document.
    document.Save("Sample.docx", FormatType.Docx)
End Using
{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Footnotes-and-Endnotes/Position-for-footnote-and-endnote).

## Footnote and Endnote separators

Footnote/Endnote separator is used to separate the text body content and footnote/endnote by a small line. 

A footnote/endnote continuation separator is used to indicate the footnote/endnote is carried over from the previous page by a line running across the top section. 

A footnote/endnote continuation notice is used to indicate the footnote/endnote is continued to the next page by special character or word preserved at the bottom of the footer.

The following code example shows how to change the default footnote separator.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
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
    //Saves the Word document to  MemoryStream
    MemoryStream stream = new MemoryStream();
    document.Save(stream, FormatType.Docx);
    document.Close();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Footnotes-and-Endnotes/Change-default-footnote-separator).

The following code example shows how to change the default endnote separator.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
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
    //Saves the Word document to  MemoryStream
    MemoryStream stream = new MemoryStream();
    document.Save(stream, FormatType.Docx);
    document.Close();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Footnotes-and-Endnotes/Change-default-endnote-separator).

## Modify Footnote and Endnote content
Modify footnote and endnote contents in an existing Word document.

The following code example shows how to modify the footnote and endnote content from an existing Word document:

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Open the file as Stream.
using (FileStream docStream  = new FileStream("Input.docx", FileMode.Open, FileAccess.Read))
{
    //Load the file stream into a Word document.
    using (WordDocument document = new WordDocument(docStream , FormatType.Docx))
    {
        //Access paragraph in a Word document.
        WParagraph paragraph = document.Sections[0].Paragraphs[6] as WParagraph;
        //Access footnote in the paragraph.
        WFootnote footnote = paragraph.ChildEntities[0] as WFootnote;
        //Clear the footnote content.
        footnote.TextBody.ChildEntities.Clear();
        //Add a new paragraph to the body of the footnote.
        WParagraph footnoteParagraph = footnote.TextBody.AddParagraph() as WParagraph;
        //Set the footnote character format.
        footnote.MarkerCharacterFormat.SubSuperScript = SubSuperScript.SuperScript;
        //Append the footnote text.
        footnoteParagraph.AppendText(" Footnote is modified.");
        //Access paragraph in a Word document.
        paragraph = document.Sections[2].Paragraphs[1] as WParagraph;
        //Access the endnote in the paragraph.
        WFootnote endnote = paragraph.ChildEntities[0] as WFootnote;
        //Clear the endnote content.
        endnote.TextBody.ChildEntities.Clear();
        //Add a new paragraph to the body of the endnote.
        WParagraph endnoteParagraph = endnote.TextBody.AddParagraph() as WParagraph;
        //Set the endnote character format.
        endnote.MarkerCharacterFormat.SubSuperScript = SubSuperScript.SuperScript;
        //Append the endnote text.
        endnoteParagraph.AppendText(" Endnote is modified.");
        //Save the the Word document to the MemoryStream.
        MemoryStream outputStream = new MemoryStream();
        document.Save(outputStream, FormatType.Docx);
    }
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Load an existing Word document.
using (WordDocument document = new WordDocument("Input.docx", FormatType.Docx))
{
    //Access paragraph in a Word document.
    WParagraph paragraph = document.Sections[0].Paragraphs[6] as WParagraph;
    //Access footnote in the paragraph.
    WFootnote footnote = paragraph.ChildEntities[0] as WFootnote;
    //Clear the footnote content.
    footnote.TextBody.ChildEntities.Clear();
    //Add a new paragraph to the body of the footnote.
    WParagraph footnoteParagraph = footnote.TextBody.AddParagraph() as WParagraph;
    //Set the footnote character format.
    footnote.MarkerCharacterFormat.SubSuperScript = SubSuperScript.SuperScript;
    //Append the footnote text.
    footnoteParagraph.AppendText(" Footnote is modified.");
    //Access paragraph in a Word document.
    paragraph = document.Sections[2].Paragraphs[1] as WParagraph;
    //Access the endnote in the paragraph.
    WFootnote endnote = paragraph.ChildEntities[0] as WFootnote;
    //Clear the endnote content.
    endnote.TextBody.ChildEntities.Clear();
    //Add a new paragraph to the body of the endnote.
    WParagraph endnoteParagraph = endnote.TextBody.AddParagraph() as WParagraph;
    //Set the endnote character format.
    endnote.MarkerCharacterFormat.SubSuperScript = SubSuperScript.SuperScript;
    //Append the endnote text.
    endnoteParagraph.AppendText(" Endnote is modified.");
    //Save a Word document.
    document.Save("Sample.docx", FormatType.Docx);
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Load an existing Word document.
Using document As WordDocument = New WordDocument("Input.docx", FormatType.Docx)
    'Access paragraph in a Word document.
    Dim paragraph As WParagraph = TryCast(document.Sections(0).Paragraphs(6), WParagraph)
    'Access footnote in the paragraph.
    Dim footnote As WFootnote = TryCast(paragraph.ChildEntities(0), WFootnote)
    'Clear the footnote content.
    footnote.TextBody.ChildEntities.Clear()
    'Add a new paragraph to the body of the footnote.
    Dim footnoteParagraph As WParagraph = TryCast(footnote.TextBody.AddParagraph(), WParagraph)
    'Set the footnote character format.
    footnote.MarkerCharacterFormat.SubSuperScript = SubSuperScript.SuperScript
    'Append the footnote text.
    footnoteParagraph.AppendText(" Footnote is modified.")
    'Access paragraph in a Word document.
    paragraph = TryCast(document.Sections(2).Paragraphs(1), WParagraph)
    'Access endnote in the paragraph.
    Dim endnote As WFootnote = TryCast(paragraph.ChildEntities(0), WFootnote)
    'Clear the endnote content.
    endnote.TextBody.ChildEntities.Clear()
    'Add a new paragraph to the body of the endnote.
    Dim endnoteParagraph As WParagraph = TryCast(endnote.TextBody.AddParagraph(), WParagraph)
    'Set the endnote character format.
    endnote.MarkerCharacterFormat.SubSuperScript = SubSuperScript.SuperScript
    'Append the endnote text.
    endnoteParagraph.AppendText(" Endnote is modified.")
    'Save a Word document.
    document.Save("Sample.docx", FormatType.Docx)
End Using
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Footnotes-and-Endnotes/Modify-Footnote-and-Endnote-content).

## Removing a Footnotes/Endnotes

The following code example shows how to remove the footnotes/endnotes from the Word document.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
FileStream inputStream = new FileStream("Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
//Loads the template document as stream
WordDocument document = new WordDocument(inputStream, FormatType.Docx);
//Removes footnote from the document
RemoveFootNoteEndNote(document);
//Saves the Word document to MemoryStream
FileStream outputStream = new FileStream("Result.docx", FileMode.OpenOrCreate, FileAccess.ReadWrite);
document.Save(outputStream, FormatType.Docx);
//Closes the document
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

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Loads the template document
WordDocument document = new WordDocument("Template.docx");
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Loads the template document
Dim document As New WordDocument("Template.docx")
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

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Footnotes-and-Endnotes/Remove-footnotes-and-endnotes).