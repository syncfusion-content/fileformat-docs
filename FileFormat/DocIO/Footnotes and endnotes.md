---
layout: Post
title: Footnotes and endnotes
description: This section illustrates how to insert the footnote and endnote in a Word document
platform: FileFormat
control: DocIO
documentation: UG
---
# Footnotes and endnotes

__Footnotes__ and __endnotes__ are separate text body content used in documents to show the source of supplementary information which does not interrupt the normal body text of the Word document. __Footnotes__ are typically located at the bottom of a page or beneath text being referenced, and __endnotes__ are typically placed at the end of a document or at the end of a section. When document has been divided up into one or more sections, each section of a document can contain endnotes.

Both footnotes and endnotes consist of two parts:

* A note reference mark with numbering value in the body text to indicate that additional information is in a footnote or endnote at the end of the page or the end of the document or section.
* The footnote or endnote text body content.
## Adding a Footnotes


The following code snippet shows how to insert the footnotes into the Word document.

{% highlight c# %}
[C#]

//Create a new Word document

WordDocument document = new WordDocument();

//Create a section

IWSection section = document.AddSection();

//Add a paragraph to a section

IWParagraph paragraph = section.AddParagraph();

//Append the text to pargraph

paragraph.AppendText("Working with footnotes");

//Formatting the text

paragraph.ApplyStyle(BuiltinStyle.Heading1);

//Add a paragraph to a section

paragraph = section.AddParagraph();

//Append the footnotes

WFootnote footnote = (WFootnote) paragraph.AppendFootnote(Syncfusion.DocIO.FootnoteType.Footnote);

//Set the footnote character format

footnote.MarkerCharacterFormat.SubSuperScript = SubSuperScript.SuperScript;

//Inserts the text into the paragraph

paragraph.AppendText("Sample content for footnotes").CharacterFormat.Bold = true;

//Add footnote text

paragraph = footnote.TextBody.AddParagraph();

paragraph.AppendText("Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula");

//Save and close the Word document instance

document.Save("Sample.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB]

'Create a new Word document

Dim document As New WordDocument()

'Create a section

Dim section As IWSection = document.AddSection()

'Add a paragraph to a section

Dim paragraph As IWParagraph = section.AddParagraph()

'Append the text to pargraph

paragraph.AppendText("Working with footnotes")

'Formatting the text

paragraph.ApplyStyle(BuiltinStyle.Heading1)

'Add a paragraph to a section

paragraph = section.AddParagraph()

'Append the footnotes

Dim footnote As WFootnote = DirectCast(paragraph.AppendFootnote(Syncfusion.DocIO.FootnoteType.Footnote), WFootnote)

'Set the footnote character format

footnote.MarkerCharacterFormat.SubSuperScript = SubSuperScript.SuperScript

'Inserts the text into the paragraph

paragraph.AppendText("Sample content for footnotes").CharacterFormat.Bold = True

'Add footnote text

paragraph = footnote.TextBody.AddParagraph()

paragraph.AppendText("Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula")

‘Save & close the Word document instance

document.Save("Sample.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

## Adding a Endnotes

The following code snippet shows how to insert the endnotes into the Word document.

{% highlight c# %}
[C#]

//Create a new document

WordDocument document = new WordDocument();

//Create a section

IWSection section = document.AddSection();

//Add a paragraph to a section

IWParagraph paragraph = section.AddParagraph();

//Append the text to paragraph

paragraph.AppendText("Working with footnotes");

//Formatting the text

paragraph.ApplyStyle(BuiltinStyle.Heading1);

//Add a paragraph to a section

paragraph = section.AddParagraph();

//Append the endnote

WFootnote endnote = (WFootnote)  paragraph.AppendFootnote(Syncfusion.DocIO.FootnoteType.Endnote);

//Set the endnote character format

endnote.MarkerCharacterFormat.SubSuperScript = SubSuperScript.SuperScript;

//Insert the text into the paragraph

paragraph.AppendText("Sample content for endnotes").CharacterFormat.Bold = true;

//Add footnote text

paragraph = endnote.TextBody.AddParagraph();

paragraph.AppendText("Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula");

//Save and close the Word document instance

document.Save("Sample.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB]

'Create a new document

Dim document As New WordDocument()

'Create a section

Dim section As IWSection = document.AddSection()

'Add a paragraph to a section

Dim paragraph As IWParagraph = section.AddParagraph()

'Append the text to paragraph

paragraph.AppendText("Working with footnotes")

'Formatting the text

paragraph.ApplyStyle(BuiltinStyle.Heading1)

'Add a paragraph to a section

paragraph = section.AddParagraph()

'Append the endnote

Dim endnote As WFootnote = DirectCast(paragraph.AppendFootnote(Syncfusion.DocIO.FootnoteType.Endnote), WFootnote)

'Set the endnote character format

endnote.MarkerCharacterFormat.SubSuperScript = SubSuperScript.SuperScript

'Insert the text into the paragraph

paragraph.AppendText("Sample content for endnotes").CharacterFormat.Bold = True

'Add footnote text

paragraph = endnote.TextBody.AddParagraph()

paragraph.AppendText("Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula")

‘Save & close the Word document instance

document.Save("Sample.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

## Footnote and Endnote separators

Footnote/Endnote separator is used to separate the text body content and footnote/endnote by a small line. 

A footnote/endnote continuation separator is used to indicating that the footnote/endnote is carried over from the previous page by a line running across the top section. 

A footnote/endnote continuation notice is used to indicating that the footnote/endnote is continue to the next page by special character or word preserved at the bottom of the footer.

The following code snippet shows how to change the default footnote separator.

{% highlight c# %}
[C#]

//Create a new Word document

WordDocument document = new WordDocument();

//Create a section

IWSection section = document.AddSection();

//Add a paragraph to a section

IWParagraph paragraph = section.AddParagraph();

//Append the text to paragraph

paragraph.AppendText("Working with footnotes");

//Formatting the text

paragraph.ApplyStyle(BuiltinStyle.Heading1);

//Add a paragraph to a section

paragraph = section.AddParagraph();

//Append the footnotes

WFootnote footnote = (WFootnote)paragraph.AppendFootnote(Syncfusion.DocIO.FootnoteType.Footnote);

WTextBody separator = document.Footnotes.Separator;

//Replace the default foot note separate by text

separator.Paragraphs[0].Text = "Footnote separator";

//Set the footnote character format

footnote.MarkerCharacterFormat.SubSuperScript = SubSuperScript.SuperScript;

//Inserts the text into the paragraph

paragraph.AppendText("Sample content for footnotes").CharacterFormat.Bold = true;

//Add footnote text

paragraph = footnote.TextBody.AddParagraph();

paragraph.AppendText("Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula");

//Save and close the Word document instance

document.Save("Sample.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB]

'Create a new Word document

Dim document As New WordDocument()

'Create a section

Dim section As IWSection = document.AddSection()

'Add a paragraph to a section

Dim paragraph As IWParagraph = section.AddParagraph()

'Append the text to paragraph

paragraph.AppendText("Working with footnotes")

'Formatting the text

paragraph.ApplyStyle(BuiltinStyle.Heading1)

'Add a paragraph to a section

paragraph = section.AddParagraph()

'Append the footnotes

Dim footnote As WFootnote = DirectCast(paragraph.AppendFootnote(Syncfusion.DocIO.FootnoteType.Footnote), WFootnote)

Dim separator As WTextBody = document.Footnotes.Separator

'Replace the default foot note separate by text

separator.Paragraphs(0).Text = "Footnote separator"

'Set the footnote character format

footnote.MarkerCharacterFormat.SubSuperScript = SubSuperScript.SuperScript

'Inserts the text into the paragraph

paragraph.AppendText("Sample content for footnotes").CharacterFormat.Bold = True

'Add footnote text

paragraph = footnote.TextBody.AddParagraph()

paragraph.AppendText("Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula")

‘Save & close the Word document instance

document.Save("Sample.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

The following code snippet shows how to change the default endnote separator.

{% highlight c# %}
[C#]

//Create a new Word document

WordDocument document = new WordDocument();

//Create a section

IWSection section = document.AddSection();

//Add a paragraph to a section

IWParagraph paragraph = section.AddParagraph();

//Append the text to paragraph

paragraph.AppendText("Working with footnotes");

//Formatting the text

paragraph.ApplyStyle(BuiltinStyle.Heading1);

//Add a paragraph to  section

paragraph = section.AddParagraph();

//Append the endnote

WFootnote endnote = (WFootnote)paragraph.AppendFootnote(Syncfusion.DocIO.FootnoteType.Endnote);

WTextBody separator = document.Endnotes.Separator;

//Replace the default foot note separate by text

separator.Paragraphs[0].Text = "Endnote separator";

//Set the endnote character format

endnote.MarkerCharacterFormat.SubSuperScript = SubSuperScript.SuperScript;

//Insert the text into the paragraph

paragraph.AppendText("Sample content for endnotes").CharacterFormat.Bold = true;

//Add the footnote text

paragraph = endnote.TextBody.AddParagraph();

paragraph.AppendText("Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula");

//Save and close the Word document instance

document.Save("Sample.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB]

'Create a new Word document

Dim document As New WordDocument()

'Create a section

Dim section As IWSection = document.AddSection()

'Add a paragraph to a section

Dim paragraph As IWParagraph = section.AddParagraph()

'Append the text to paragraph

paragraph.AppendText("Working with footnotes")

'Formatting the text

paragraph.ApplyStyle(BuiltinStyle.Heading1)

'Add a paragraph to  section

paragraph = section.AddParagraph()

'Append the endnote

Dim endnote As WFootnote = DirectCast(paragraph.AppendFootnote(Syncfusion.DocIO.FootnoteType.Endnote), WFootnote)

Dim separator As WTextBody = document.Endnotes.Separator

'Replace the default foot note separate by text

separator.Paragraphs(0).Text = "Endnote separator"

'Set the endnote character format

endnote.MarkerCharacterFormat.SubSuperScript = SubSuperScript.SuperScript

'Insert the text into the paragraph

paragraph.AppendText("Sample content for endnotes").CharacterFormat.Bold = True

'Add the footnote text

paragraph = endnote.TextBody.AddParagraph()

paragraph.AppendText("Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula")

‘Save & close the Word document instance

document.Save("Sample.docx", FormatType.Docx)

document.Close()





{% endhighlight %}

