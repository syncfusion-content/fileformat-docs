---
layout: post
title: Working with Table Of Contents
description: This section illustrates how to insert and update the Table Of Content in a Word document
platform: FileFormat
control: DocIO
documentation: UG
---
# Working with Table Of Contents

[Table of contents](https://support.office.com/en-in/article/Create-a-table-of-contents-or-update-a-table-of-contents-eb275189-b93e-4559-8dd9-c279457bfd72#__create_a_table "") (TOC) is used to provide an outline of the Word document. By default table of contents will be created automatically from heading styles. 

You can add the TOC into the paragraph by specifying the LowerHeadingLevel and UpperHeadingLevel. The heading level range must be from 1 to 9.

Basically TOC determines the TOC entries based on the TOC switches. 

<table>
<tr>
<td>
S.No<br/><br/></td><td>
Switches<br/><br/></td><td>
Description<br/><br/></td></tr>
<tr>
<td>
1<br/><br/></td><td>
\o<br/><br/></td><td>
Builds a table of contents from paragraphs formatted with built-in heading styles.<br/><br/></td></tr>
<tr>
<td>
2<br/><br/></td><td>
\h<br/><br/></td><td>
Inserts TOC entries as hyperlinks.<br/><br/></td></tr>
<tr>
<td>
3<br/><br/></td><td>
\n<br/><br/></td><td>
Omits page numbers from the table of contents. <br/><br/></td></tr>
<tr>
<td>
4<br/><br/></td><td>
\p<br/><br/></td><td>
Specifies the characters that separate a TOC entry and its page number. The default is a tab with leader dots.<br/><br/></td></tr>
<tr>
<td>
5<br/><br/></td><td>
\t<br/><br/></td><td>
Builds a table of contents from paragraphs formatted with specified styles other than the built-in heading styles<br/><br/></td></tr>
</table>
## Adding a toc field

The following code example shows how to add a table of contents (TOC) in Word document. 

{% highlight c# %}
[C#] 

//Creates a new Word document

WordDocument document = new WordDocument();

//Adds the section into the Word document

IWSection section = document.AddSection();

string paraText = "Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula";

//Adds the paragraph into the created section

IWParagraph paragraph = section.AddParagraph();

//Appends the TOC field with LowerHeadingLevel and UpperHeadingLevel to determines the TOC entries

paragraph.AppendTOC(1, 3);

//Adds the section into the Word document

section = document.AddSection();

//Adds the paragraph into the created section

paragraph = section.AddParagraph(); 

//Adds the text for the headings

paragraph.AppendText("First Chapter");

//Sets a build in heading style.

paragraph.ApplyStyle(BuiltinStyle.Heading1);

//Adds the text into the paragraph

section.AddParagraph().AppendText(paraText);

//Adds the section into the Word document

section = document.AddSection();

//Adds the paragraph into the created section

paragraph = section.AddParagraph();

//Adds the text for the headings

paragraph.AppendText("Second Chapter");

//Sets a build in heading style.

paragraph.ApplyStyle(BuiltinStyle.Heading2);

//Adds the text into the paragraph

section.AddParagraph().AppendText(paraText);

//Adds the section into the Word document

section = document.AddSection();

//Adds the paragraph into the created section

paragraph = section.AddParagraph();

//Adds the text into the headings

paragraph.AppendText("Third Chapter");

//Sets a build in heading style

paragraph.ApplyStyle(BuiltinStyle.Heading3);

//Adds the text into the paragraph.

section.AddParagraph().AppendText(paraText);

//Updates the table of contents

document.UpdateTableOfContents();

//Saves and closes the Word document instance

document.Save("Sample.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB] 

'Creates a new Word document

Dim document As New WordDocument()

'Adds the section into the Word document

Dim section As IWSection = document.AddSection()

Dim paraText As String = "Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula"

'Adds the paragraph into the created section

Dim paragraph As IWParagraph = section.AddParagraph()

'Appends the TOC field with LowerHeadingLevel and UpperHeadingLevel to determines the TOC entries

paragraph.AppendTOC(1, 3)

'Adds the section into the Word document

section = document.AddSection()

'Adds the paragraph into the created section

paragraph = section.AddParagraph()

'Adds the text for the headings

paragraph.AppendText("First Chapter")

'Sets a build in heading style

paragraph.ApplyStyle(BuiltinStyle.Heading1)

'Adds the text into the paragraph.

section.AddParagraph().AppendText(paraText)

'Adds the section into the Word document

section = document.AddSection()

'Adds the paragraph into the created section

paragraph = section.AddParagraph()

'Adds the text for the headings

paragraph.AppendText("Second Chapter")

'Sets a build in heading style

paragraph.ApplyStyle(BuiltinStyle.Heading2)

'Adds the text into the paragraph

section.AddParagraph().AppendText(paraText)

'Adds the section into the Word document

section = document.AddSection()

'Adds the paragraph into the created section

paragraph = section.AddParagraph()

'Adds the text into the headings

paragraph.AppendText("Third Chapter")

'Sets a build in heading style

paragraph.ApplyStyle(BuiltinStyle.Heading3)

'Adds the text into the paragraph

section.AddParagraph().AppendText(paraText)

'Updates the table of contents

document.UpdateTableOfContents()

‘Saves and closes the Word document instance

document.Save("Sample.docx", FormatType.Docx)

document.Close()





{% endhighlight %}

## Updating table of contents

You can also update or re-build the TOC in an existing document or document created from the scratch.  

I> Note: 

I> TOC is not supported in Silverlight, WinRT, Univeral, Xamarin and windows phone applications using DocIO. 

I> Updating TOC makes use of the Word to PDF layouting engine that may lead to the updation of incorrect page number due to its [limitations](help.syncfusion.com# "").

The following code example shows how to update a TOC in an existing word document. 

{% highlight c# %}
[C#] 

//Opens an input word template

WordDocument document = new WordDocument(@”Template.docx”);

//Updates the table of contents.

document.UpdateTableOfContents();

//Saves and closes the Word document instance.

document.Save("Sample.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB] 

'Opens an input word template

Dim document As New WordDocument("Template.docx")

'Updates the table of contents.

document.UpdateTableOfContents()

‘Saves and closes the Word document instance.

document.Save("Sample.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

## Creating table of contents with user-defined styles

The following code example shows how to create table of contents with user-defined styles instead of heading styles.

{% highlight c# %}
[C#] 

//Creates a new Word document

WordDocument document = new WordDocument();

//Creates a new custom styles

Style style = (WParagraphStyle)document.AddParagraphStyle("Mystyle");

style.CharacterFormat.Bold = true;

style.CharacterFormat.FontName = "Verdana";

style.CharacterFormat.FontSize = 25;

//Adds the section into the Word document

IWSection section = document.AddSection();

string paraText = "Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula";

//Adds the paragraph into the created section

IWParagraph paragraph = section.AddParagraph();

//Appends the TOC field with LowerHeadingLevel and UpperHeadingLevel to determines the TOC entries

TableOfContent toc = paragraph.AppendTOC(1, 3);

toc.UseHeadingStyles = false;

//Sets the TOC level style based on the created TOC 

toc.SetTOCLevelStyle(2, "Mystyle");

//Adds the section into the Word document

section = document.AddSection();

//Adds the paragraph into the created section

paragraph = section.AddParagraph();

//Adds the text for the headings

paragraph.AppendText("First Chapter");

//Sets the build in heading style

paragraph.ApplyStyle("Mystyle");

//Adds the text into the paragraph

section.AddParagraph().AppendText(paraText);

//Adds the section into the Word document

section = document.AddSection();

//Adds the paragraph into the created section

paragraph = section.AddParagraph();

//Adds the text for the headings

paragraph.AppendText("Second Chapter");

//Sets the build in heading style

paragraph.ApplyStyle(BuiltinStyle.Heading1);

//Adds the text to the paragraph

section.AddParagraph().AppendText(paraText);

//Adds the section into Word document

section = document.AddSection();

//Adds a paragraph to a created section

paragraph = section.AddParagraph();

//Adds the text for the headings

paragraph.AppendText("Third Chapter");

//Sets the build in heading style

paragraph.ApplyStyle("Mystyle");

//Adds the text to the paragraph

section.AddParagraph().AppendText(paraText);

//Updates the table of contents

document.UpdateTableOfContents();

//Saves and closes the Word document instance

document.Save("Sample.docx", FormatType.Docx);

document.Close();





{% endhighlight %}

{% highlight vbnet %}
[VB] 

'Creates a new Word document

Dim document As New WordDocument()

'Creates a new custom styles

Dim style As Style = DirectCast(document.AddParagraphStyle("Mystyle"), WParagraphStyle)

style.CharacterFormat.Bold = True

style.CharacterFormat.FontName = "Verdana"

style.CharacterFormat.FontSize = 25

'Adds the section into the Word document

Dim section As IWSection = document.AddSection()

Dim paraText As String = "Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula"

'Adds the paragraph into the created section

Dim paragraph As IWParagraph = section.AddParagraph()

'Appends the TOC field with LowerHeadingLevel and UpperHeadingLevel to determine the TOC entries

Dim toc As TableOfContent = paragraph.AppendTOC(1, 3)

toc.UseHeadingStyles = False

'Sets the TOC level style based on the created TOC 

toc.SetTOCLevelStyle(2, "Mystyle")

'Adds the section into the Word document

section = document.AddSection()

'Adds the paragraph into the created section

paragraph = section.AddParagraph()

'Adds the text for the headings

paragraph.AppendText("First Chapter")

'Sets the build in heading style

paragraph.ApplyStyle("Mystyle")

'Adds the text into the paragraph

section.AddParagraph().AppendText(paraText)

'Adds the section into the Word document

section = document.AddSection()

'Adds the paragraph into the created section

paragraph = section.AddParagraph()

'Adds the text for the headings

paragraph.AppendText("Second Chapter")

'Sets the build in heading style

paragraph.ApplyStyle(BuiltinStyle.Heading1)

'Adds the text to the paragraph

section.AddParagraph().AppendText(paraText)

'Adds the section into Word document

section = document.AddSection()

'Adds a paragraph to created section

paragraph = section.AddParagraph()

'Adds the text for the headings

paragraph.AppendText("Third Chapter")

'Sets the build in heading style

paragraph.ApplyStyle("Mystyle")

'Adds the text to the paragraph

section.AddParagraph().AppendText(paraText)

'Updates the table of contents

document.UpdateTableOfContents()

‘Saves and closes the Word document instance

document.Save("Sample.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

