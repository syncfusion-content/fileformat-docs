---
layout: Post
title: Working with Sections
description: This section illustrates how to Work with Sections
platform: FileFormat
control: DocIO
documentation: UG
---
# Working with Sections

A Section contains the contents present in Headers, Footers and main document through the instances of WTextBody. A section also have a specific set of properties used to define the page settings, number of columns, headers and footers and so on which decides how the text appears. WTextBody represents group of paragraphs and tables etc. 

{% highlight c# %}
[C#] 

//Create a new Word document

WordDocument document = new WordDocument();

//Add new section to the document

IWSection section = document.AddSection();

//Add new paragraph to the section

IWParagraph paragraph = section.AddParagraph();

//Append the text to the created paragraph

paragraph.AppendText("Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula");

//Save and close the Word document instance

document.Save("Sample.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB] 

'Create a new Word document

Dim document As New WordDocument()

'Add new section to the document

Dim section As IWSection = document.AddSection()

'Add new paragraph to created section

Dim paragraph As IWParagraph = section.AddParagraph()

'Append the text to the created paragraph

paragraph.AppendText("Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula")

‘Save & close the Word document instance

document.Save("Sample.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

You can add the multiple sections into the document. When you add more than one section into the word document, the section start from the next page by default.

You can also add a new section which starts on a same page by specifying the BreakCode as shown in below code snippet.

{% highlight c# %}
[C#] 

//Create a new Word document

WordDocument document = new WordDocument();

//Add new section to the document

IWSection section = document.AddSection();

//Add a paragraph to created section

IWParagraph paragraph = section.AddParagraph();

string paraText = "Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula";

//Append the text to the created paragraph

paragraph.AppendText(paraText);

//Add the new section to the document

section = document.AddSection();

//Set a section break

section.BreakCode = SectionBreakCode.NoBreak;

//Add a paragraph to created section

paragraph = section.AddParagraph();

//Append the text to the created paragraph

paragraph.AppendText(paraText); 

//Save and close the Word document instance

document.Save("Sample.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB] 

'Create a new Word document

Dim document As New WordDocument()

'Add the section into Word document

Dim section As IWSection = document.AddSection()

'Add a paragraph to created section

Dim paragraph As IWParagraph = section.AddParagraph()

Dim paraText As String = "Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula"

'Append the text to the created paragraph

paragraph.AppendText(paraText)

'Add the new section to the document

section = document.AddSection()

'Set a section break

section.BreakCode = SectionBreakCode.NoBreak

'Add a paragraph to created section

paragraph = section.AddParagraph()

'Append the text to the created paragraph

paragraph.AppendText(paraText)

‘Save & close the Word document instance

document.Save("Sample.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

## Specifying Page Properties

Each section have its own page setup properties such as page size, orientation, margins, borders, etc. 

The following code snippet shows how to set the page setup properties

{% highlight c# %}
[C#] 

WordDocument document = new WordDocument();

IWSection section = document.AddSection();

//Set page setup options

section.PageSetup.Orientation = PageOrientation.Landscape;

section.PageSetup.Margins.All = 72;

section.PageSetup.Borders.LineWidth = 2;

//Add a paragraph to created section

IWParagraph paragraph = section.AddParagraph();

//Append the text to the created paragraph

paragraph.AppendText("Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula"); 

//Save and close the Word document instance

document.Save("Sample.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB] 

Dim document As New WordDocument()

Dim section As IWSection = document.AddSection()

'Set page setup options

section.PageSetup.Orientation = PageOrientation.Landscape

section.PageSetup.Margins.All = 72

section.PageSetup.Borders.LineWidth = 2

'Add a paragraph to created section

Dim paragraph As IWParagraph = section.AddParagraph()

'Append the text to the created paragraph.

paragraph.AppendText("Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula")

‘Save & close the Word document instance

document.Save("Sample.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

## Creating Multi-column document

You can split the contents into two or more columns by specifying the column width and spacing between columns.

The following code snippet shows how to display contents in multiple columns.

{% highlight c# %}
[C#] 

//Create a new Word document

WordDocument document = new WordDocument();

//Add the section into Word document

IWSection section = document.AddSection();

//Add the column into the section

section.AddColumn(150, 20);

//Add the column into the section

section.AddColumn(150, 20);

//Add the column into the section

section.AddColumn(150, 20);

//Add a paragraph to created section

IWParagraph paragraph = section.AddParagraph();

//Add a paragraph to created section

paragraph = section.AddParagraph();

string paraText = "Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula";

//Append the text to the created paragraph

paragraph.AppendText(paraText);

//Add the column breaks

paragraph.AppendBreak(BreakType.ColumnBreak);

//Add a paragraph to created section

paragraph = section.AddParagraph();

//Append the text to the created paragraph

paragraph.AppendText(paraText);

//Add the column breaks

paragraph.AppendBreak(BreakType.ColumnBreak);

//Add a paragraph to created section

paragraph = section.AddParagraph();

//Append the text to the created paragraph

paragraph.AppendText(paraText);

//Save and close the Word document instance

document.Save("Sample.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB] 

'Create a new Word document

Dim document As New WordDocument()

'Add the section into Word document

Dim section As IWSection = document.AddSection()

'Add the column into the section

section.AddColumn(150, 20)

'Add the column into the section

section.AddColumn(150, 20)

'Add the column into the section

section.AddColumn(150, 20)

'Add a paragraph to created section

Dim paragraph As IWParagraph = section.AddParagraph()

'Add a paragraph to created section

paragraph = section.AddParagraph()

Dim paraText As String = "Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula"

'Append the text to the created paragraph

paragraph.AppendText(paraText)

'Add the column breaks

paragraph.AppendBreak(BreakType.ColumnBreak)

'Add a paragraph to created section

paragraph = section.AddParagraph()

'Append the text to the created paragraph

paragraph.AppendText(paraText)

'Add the column breaks

paragraph.AppendBreak(BreakType.ColumnBreak)

'Add a paragraph to created section

paragraph = section.AddParagraph()

'Append the text to the created paragraph

paragraph.AppendText(paraText)

‘Save & close the Word document instance

document.Save("Sample.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

## Creating document with different page settings

You can prefer to have more than sections in a Word document if you have the need to have different page settings or headers & footers for a specific set of contents. The following code snippet illustrates how to create a Word document with multiple sections whose page orientation are portrait and landscape respectively.

{% highlight c# %}
[C#] 

//Create a new Word document

WordDocument document = new WordDocument();

//Add the section into Word document

IWSection section = document.AddSection();

//Add a paragraph to created section

IWParagraph paragraph = section.AddParagraph();

string paraText = "Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula";

//Append the text to the created paragraph

paragraph.AppendText(paraText);

//Set the page orientation as portrait

section.PageSetup.Orientation = PageOrientation.Portrait;

//Add the new section to the document

section = document.AddSection();

//Set the section break

section.BreakCode = SectionBreakCode.NewPage;

paragraph = section.AddParagraph();

//Set the page orientation as land scape

section.PageSetup.Orientation = PageOrientation.Landscape;

//Append the text to the paragraph

paragraph.AppendText(paraText);

//Save and close the Word document instance

document.Save("Sample.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB] 

'Create a new Word document

Dim document As New WordDocument()

'Add the section into Word document

Dim section As IWSection = document.AddSection()

'Add a paragraph to created section

Dim paragraph As IWParagraph = section.AddParagraph()

Dim paraText As String = "Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula"

'Append the text to the created paragraph

paragraph.AppendText(paraText)

'Set the page orientation as portrait

section.PageSetup.Orientation = PageOrientation.Portrait

'Add the new section to the document

section = document.AddSection()

'Set the section break

section.BreakCode = SectionBreakCode.NewPage

paragraph = section.AddParagraph()

'Set the page orientation as land scape

section.PageSetup.Orientation = PageOrientation.Landscape

'Append the text to the paragraph

paragraph.AppendText(paraText)

‘Save & close the Word document instance

document.Save("Sample.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

## Working with Headers and Footers

Header and footer also represents the group of paragraphs and tables which occurs at the top and bottom of the page respectively. Header and footer may vary for each section. The following are the types of Headers/Footers:

  * FirstPageHeader – Represents the first page header of the document.
  * FirstPageFooter – Represents the first page footer of the document. 
  * OddHeader – Represents the odd page header of the document and it is the default header for the section. 
  * OddFooter – Represents the odd page footer of the document and it is the default footer for the section.
  * EvenHeader – Represents the even page header of the document.
  * Even Footer - Represents the even page footer of the document.

The following code snippet illustrates how to add simple header and footer into a Word document.

{% highlight c# %}
[C#] 

//Create a new document

WordDocument document = new WordDocument();

//Add the first section to the document

IWSection section = document.AddSection();

//Add a paragraph to the section

IWParagraph paragraph = section.AddParagraph();

string paraText = "Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula";

//Append some text to the first page in document

paragraph.AppendText("\r\r[ First Page ] \r\r" + paraText);

paragraph.ParagraphFormat.PageBreakAfter = true;

//Append some text to the second page in document

paragraph = section.AddParagraph();

paragraph.AppendText("\r\r[ Second Page ] \r\r" + paraText);

paragraph.ParagraphFormat.PageBreakAfter = true;

//Append some text to the third page in document

paragraph = section.AddParagraph();

paragraph.AppendText("\r\r[ Third Page ] \r\r" + paraText);

//Insert the default page header

paragraph = section.HeadersFooters.OddHeader.AddParagraph();

paragraph.AppendText("[ Default Page Header ]");

//Insert the default Page footer

paragraph = section.HeadersFooters.OddFooter.AddParagraph();

paragraph.AppendText("[ Default Page Footer ]");

//Save and close the Word document instance

document.Save("Sample.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB] 

'Create a new document

Dim document As New WordDocument()

'Add the first section to the document

Dim section As IWSection = document.AddSection()

'Add a paragraph to the section

Dim paragraph As IWParagraph = section.AddParagraph()

Dim paraText As String = "Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula"

'Append some text to the first page in document

paragraph.AppendText(Convert.ToString(vbCr & vbCr & "[ First Page ] " & vbCr & vbCr) & paraText)

paragraph.ParagraphFormat.PageBreakAfter = True

'Append some text to the second page in document

paragraph = section.AddParagraph()

paragraph.AppendText(Convert.ToString(vbCr & vbCr & "[ Second Page ] " & vbCr & vbCr) & paraText)

paragraph.ParagraphFormat.PageBreakAfter = True

'Append some text to the third page in document

paragraph = section.AddParagraph()

paragraph.AppendText(Convert.ToString(vbCr & vbCr & "[ Third Page ] " & vbCr & vbCr) & paraText)

'Insert the default page header

paragraph = section.HeadersFooters.OddHeader.AddParagraph()

paragraph.AppendText("[ Default Page Header ]")

'Insert the default Page footer

paragraph = section.HeadersFooters.OddFooter.AddParagraph()

paragraph.AppendText("[ Default Page Footer ]")

‘Save & close the Word document instance

document.Save("Sample.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

You can have a specific header and footer contents for the first page in a Word document. The following code illustrates the same. 

{% highlight c# %}
[C#] 

//Create a new document

WordDocument document = new WordDocument();

//Add the first section to the document

IWSection section = document.AddSection();

//Set DifferentFirstPage as true for inserting header and footer text

section.PageSetup.DifferentFirstPage = true;

//Add a paragraph to the section

IWParagraph paragraph = section.AddParagraph();

string paraText = "Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula";

//Append some text to the first page in document

paragraph.AppendText("\r\r[ First Page ] \r\r" + paraText);

paragraph.ParagraphFormat.PageBreakAfter = true;

//Append some text to the second page in document

paragraph = section.AddParagraph();

paragraph.AppendText("\r\r[ Second Page ] \r\r" + paraText);

paragraph.ParagraphFormat.PageBreakAfter = true;

//Append some text to the third page in document

paragraph = section.AddParagraph();

paragraph.AppendText("\r\r[ Third Page ] \r\r" + paraText);

//Insert the first page header

paragraph = section.HeadersFooters.FirstPageHeader.AddParagraph();

paragraph.AppendText("[First Page Header ]");

//Insert the first page footer

paragraph = section.HeadersFooters.FirstPageFooter.AddParagraph();

paragraph.AppendText("[ First Page Footer ]");

//Insert the default page header

paragraph = section.HeadersFooters.OddHeader.AddParagraph();

paragraph.AppendText("[ Default Page Header ]");

//Insert the default page footer

paragraph = section.HeadersFooters.OddFooter.AddParagraph();

paragraph.AppendText("[ Default Page Footer ]");

//Save and close the Word document instance

document.Save("Sample.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB] 

'Create a new document

Dim document As New WordDocument()

'Add the first section to the document

Dim section As IWSection = document.AddSection()

'Set DifferentFirstPage as true for inserting header and footer text

section.PageSetup.DifferentFirstPage = True

'Add a paragraph to the section

Dim paragraph As IWParagraph = section.AddParagraph()

Dim paraText As String = "Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula"

'Append some text to the first page in document

paragraph.AppendText(Convert.ToString(vbCr & vbCr & "[ First Page ] " & vbCr & vbCr) & paraText)

paragraph.ParagraphFormat.PageBreakAfter = True

'Append some text to the second page in document

paragraph = section.AddParagraph()

paragraph.AppendText(Convert.ToString(vbCr & vbCr & "[ Second Page ] " & vbCr & vbCr) & paraText)

paragraph.ParagraphFormat.PageBreakAfter = True

'Append some text to the third page in document

paragraph = section.AddParagraph()

paragraph.AppendText(Convert.ToString(vbCr & vbCr & "[ Third Page ] " & vbCr & vbCr) & paraText)

'Insert the first page header

paragraph = section.HeadersFooters.FirstPageHeader.AddParagraph()

paragraph.AppendText("[First Page Header ]")

'Insert the first page footer

paragraph = section.HeadersFooters.FirstPageFooter.AddParagraph()

paragraph.AppendText("[ First Page Footer ]")

'Insert the default page header

paragraph = section.HeadersFooters.OddHeader.AddParagraph()

paragraph.AppendText("[ Default Page Header ]")

'Insert the default page footer

paragraph = section.HeadersFooters.OddFooter.AddParagraph()

paragraph.AppendText("[ Default Page Footer ]")

‘Save & close the Word document instance

document.Save("Sample.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

A Word document can have different header and footer for odd and even pages.

The following code snippet shows how to sets different header and footer for the odd and even pages of the document. 

{% highlight c# %}
[C#] 

//Create a new document

WordDocument document = new WordDocument();

//Add the first section to the document

IWSection section = document.AddSection();

//Set DifferentOddAndEvenPages as true for inserting header and footer text

section.PageSetup.DifferentOddAndEvenPages = true;

//Add a paragraph to the section

IWParagraph paragraph = section.AddParagraph();

string paraText = "Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula";

//Append some text to the first page in document

paragraph.AppendText("\r\r[ First Page ] \r\r" + paraText);

paragraph.ParagraphFormat.PageBreakAfter = true;

//Append some text to the second page in document

paragraph = section.AddParagraph();

paragraph.AppendText("\r\r[ Second Page ] \r\r" + paraText);

paragraph.ParagraphFormat.PageBreakAfter = true;

//Append some text to the third page in document

paragraph = section.AddParagraph();

paragraph.AppendText("\r\r[ Third Page ] \r\r" + paraText);

//Insert the odd page header

paragraph = section.HeadersFooters.OddHeader.AddParagraph();

paragraph.AppendText("[ Odd Page Header ]");

//Insert the default page footer

paragraph = section.HeadersFooters.OddFooter.AddParagraph();

paragraph.AppendText("[ Odd Page Footer ]");

//Insert the even page header

paragraph = section.HeadersFooters.EvenHeader.AddParagraph();

paragraph.AppendText("[Even Page Header ]");

//Insert the even page footer

paragraph = section.HeadersFooters.EvenFooter.AddParagraph();

paragraph.AppendText("[ Even Page Footer ]");

//Save and close the Word document instance

document.Save("Sample.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB] 

'Create a new document

Dim document As New WordDocument()

'Add the first section to the document

Dim section As IWSection = document.AddSection()

'Set DifferentOddAndEvenPages as true for inserting header and footer text

section.PageSetup.DifferentOddAndEvenPages = True

'Add a paragraph to the section

Dim paragraph As IWParagraph = section.AddParagraph()

Dim paraText As String = "Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula"

'Append some text to the first page in document

paragraph.AppendText(Convert.ToString(vbCr & vbCr & "[ First Page ] " & vbCr & vbCr) & paraText)

paragraph.ParagraphFormat.PageBreakAfter = True

'Append some text to the second page in document

paragraph = section.AddParagraph()

paragraph.AppendText(Convert.ToString(vbCr & vbCr & "[ Second Page ] " & vbCr & vbCr) & paraText)

paragraph.ParagraphFormat.PageBreakAfter = True

'Append some text to the third page in document

paragraph = section.AddParagraph()

paragraph.AppendText(Convert.ToString(vbCr & vbCr & "[ Third Page ] " & vbCr & vbCr) & paraText)

'Insert the odd page header

paragraph = section.HeadersFooters.OddHeader.AddParagraph()

paragraph.AppendText("[ Odd Page Header ]")

'Insert the default page footer

paragraph = section.HeadersFooters.OddFooter.AddParagraph()

paragraph.AppendText("[ Odd Page Footer ]")

'Insert the even page header

paragraph = section.HeadersFooters.EvenHeader.AddParagraph()

paragraph.AppendText("[Even Page Header ]")

'Insert the even page footer

paragraph = section.HeadersFooters.EvenFooter.AddParagraph()

paragraph.AppendText("[ Even Page Footer ]")

‘Save & close the Word document instance

document.Save("Sample.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

You can use the previous section header and footer for the current section using LinkToPrevious property.

The following code snippet shows how to link the previous section header and footer for the current section.

{% highlight c# %}
[C#] 

//Create a new document

WordDocument document = new WordDocument();

//Add the first section to the document

IWSection section = document.AddSection();

//Insert the first section header

section.HeadersFooters.Header.AddParagraph().AppendText("[ First Section Header ]");

//Insert the first section footer

section.HeadersFooters.Footer.AddParagraph().AppendText("[ First Section Footer ]");

//Add a paragraph to the section

IWParagraph paragraph = section.AddParagraph();

string paraText = "Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula";

//Append some text to the first page in document

paragraph.AppendText("\r\r[ First Page ] \r\r" + paraText);

//Add the second section to the document

section = document.AddSection();

//Insert the second section header

section.HeadersFooters.Header.AddParagraph().AppendText("[ Second Section Header ]");

//Insert the second section footer.

section.HeadersFooters.Footer.AddParagraph().AppendText("[ Second Section Footer ]");

//Set LinkToPrevious as true for retrieve the header and footer from previous section

section.HeadersFooters.LinkToPrevious = true;

//Append some text to the second page in document

paragraph = section.AddParagraph();

paragraph.AppendText("\r\r[ Second Page ] \r\r" + paraText);

//Add the third section to the document

section = document.AddSection();

//Insert the third section header

section.HeadersFooters.Header.AddParagraph().AppendText("[ Third Section Header ]");

//Insert the third section footer

section.HeadersFooters.Footer.AddParagraph().AppendText("[ Third Section Footer ]");

//Append some text to the third page in document

paragraph = section.AddParagraph();

paragraph.AppendText("\r\r[ Third Page ] \r\r" + paraText);

//Save and close the Word document instance

document.Save("Sample.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB] 

'Create a new document

Dim document As New WordDocument()

'Add the first section to the document

Dim section As IWSection = document.AddSection()

'Insert the first section header

section.HeadersFooters.Header.AddParagraph().AppendText("[ First Section Header ]")

'Insert the first section footer

section.HeadersFooters.Footer.AddParagraph().AppendText("[ First Section Footer ]")

'Add a paragraph to the section

Dim paragraph As IWParagraph = section.AddParagraph()

Dim paraText As String = "Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula"

'Append some text to the first page in document

paragraph.AppendText(Convert.ToString(vbCr & vbCr & "[ First Page ] " & vbCr & vbCr) & paraText)

'Add the second section to the document

section = document.AddSection()

'Insert the second section header

section.HeadersFooters.Header.AddParagraph().AppendText("[ Second Section Header ]")

'Insert the second section footer

section.HeadersFooters.Footer.AddParagraph().AppendText("[ Second Section Footer ]")

'Set LinkToPrevious as true for retrieve the header and footer from previous section

section.HeadersFooters.LinkToPrevious = True

'Append some text to the second page in document

paragraph = section.AddParagraph()

paragraph.AppendText(Convert.ToString(vbCr & vbCr & "[ Second Page ] " & vbCr & vbCr) & paraText)

'Add the third section to the document

section = document.AddSection()

'Insert the third section header

section.HeadersFooters.Header.AddParagraph().AppendText("[ Third Section Header ]")

'Insert the third section footer

section.HeadersFooters.Footer.AddParagraph().AppendText("[ Third Section Footer ]")

'Append some text to the third page in document

paragraph = section.AddParagraph()

paragraph.AppendText(Convert.ToString(vbCr & vbCr & "[ Third Page ] " & vbCr & vbCr) & paraText)

‘Save & close the Word document instance

document.Save("Sample.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

## Adding Page Numbers

You can insert the current page number within the document contents. The following code snippet illustrates how to insert current page number within footer.   

{% highlight c# %}
[C#] 

//Create a new Word document

WordDocument document = new WordDocument();

//Add the section into Word document

IWSection section = document.AddSection();

section.PageSetup.PageStartingNumber = 1;

section.PageSetup.RestartPageNumbering = true;

section.PageSetup.PageNumberStyle = PageNumberStyle.Arabic;

//Add a footer paragraph text to the document

IWParagraph paragraph = section.HeadersFooters.Footer.AddParagraph();

paragraph.ParagraphFormat.Tabs.AddTab(523f, TabJustification.Right, TabLeader.NoLeader);

//Add text for the footer paragraph

paragraph.AppendText("Copyright Northwind Inc. 2001 - 2015");

//Add page number field to the document

paragraph.AppendText("\tPage ");

paragraph.AppendField("Page", FieldType.FieldPage);

//Add the paragraph

paragraph = section.AddParagraph();

//Append the text to the created paragraph

paragraph.AppendText("Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula");

//Save and close the Word document instance

document.Save("Sample.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB] 

'Create a new Word document

Dim document As New WordDocument()

'Add the section into Word document

Dim section As IWSection = document.AddSection()

section.PageSetup.PageStartingNumber = 1

section.PageSetup.RestartPageNumbering = True

section.PageSetup.PageNumberStyle = PageNumberStyle.Arabic

'Add a footer paragraph text to the document

Dim paragraph As IWParagraph = section.HeadersFooters.Footer.AddParagraph()

paragraph.ParagraphFormat.Tabs.AddTab(523.0F, TabJustification.Right, TabLeader.NoLeader)

'Add text for the footer paragraph

paragraph.AppendText("Copyright Northwind Inc. 2001 - 2015")

'Add page number field to the document

paragraph.AppendText(vbTab & "Page ")

paragraph.AppendField("Page", FieldType.FieldPage)

'Add the paragraph

paragraph = section.AddParagraph()

'Append the text to the created paragraph

paragraph.AppendText("Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula")

'Save & close the Word document instance

document.Save("Sample.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

The following code snippet illustrates how to add the current page number and total number of pages in header/footer. 

{% highlight c# %}
[C#] 

//Create a new Word document

WordDocument document = new WordDocument();

//Add the section into Word document

IWSection section = document.AddSection();

section.PageSetup.PageStartingNumber = 1;

section.PageSetup.RestartPageNumbering = true;

section.PageSetup.PageNumberStyle = PageNumberStyle.Arabic;

//Add a footer paragraph text to the document

IWParagraph paragraph = section.HeadersFooters.Footer.AddParagraph();

paragraph.ParagraphFormat.Tabs.AddTab(523f, TabJustification.Right, TabLeader.NoLeader);

// Add text for the footer paragraph

paragraph.AppendText("Copyright Northwind Inc. 2001 - 2015\t");

//Add the text

paragraph.AppendText(" Page ");

//Add page number field to the document

paragraph.AppendField("CurrentPageNumber", FieldType.FieldPage);

// Add the text

paragraph.AppendText(" of ");

//Add number of page field to the document

paragraph.AppendField("TotalNumberOfPages", FieldType.FieldNumPages);

//Add the paragraph

paragraph = section.AddParagraph();

//Append the text to the created paragraph

paragraph.AppendText("Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula");

//Save and close the Word document instance

document.Save("Sample.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB] 

'Create a new Word document

Dim document As New WordDocument()

'Add the section into Word document

Dim section As IWSection = document.AddSection()

section.PageSetup.PageStartingNumber = 1

section.PageSetup.RestartPageNumbering = True

section.PageSetup.PageNumberStyle = PageNumberStyle.Arabic

'Add a footer paragraph text to the document

Dim paragraph As IWParagraph = section.HeadersFooters.Footer.AddParagraph()

paragraph.ParagraphFormat.Tabs.AddTab(523.0F, TabJustification.Right, TabLeader.NoLeader)

'Add text for the footer paragraph

paragraph.AppendText("Copyright Northwind Inc. 2001 - 2015" & vbTab)

'Add the text

paragraph.AppendText(" Page ")

'Add page number field to the document

paragraph.AppendField("CurrentPageNumber", FieldType.FieldPage)

'Add the text

paragraph.AppendText(" of ")

'Add number of page field to the document

paragraph.AppendField("TotalNumberOfPages", FieldType.FieldNumPages)

'Add the paragraph

paragraph = section.AddParagraph()

'Append the text to the created paragraph

paragraph.AppendText("Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula")

‘Save & close the Word document instance

document.Save("Sample.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

The following code snippet shows how to adjust the height of header and footer.

{% highlight c# %}
[C#] 

//Create a new document

WordDocument document = new WordDocument();

//Add the first section to the document

IWSection section = document.AddSection();

//Specify the value to header distance

section.PageSetup.HeaderDistance = 100;

// Specify the value to footer distance

section.PageSetup.FooterDistance = 100;

//Add a paragraph to the section

IWParagraph paragraph = section.AddParagraph();

string paraText = "Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula";

//Append some text to the first page in document

paragraph.AppendText("\r\r[ First Page ] \r\r" + paraText);

paragraph.ParagraphFormat.PageBreakAfter = true;

//Append some text to the second page in document

paragraph = section.AddParagraph();

paragraph.AppendText("\r\r[ Second Page ] \r\r" + paraText);

paragraph.ParagraphFormat.PageBreakAfter = true;

//Append some text to the third page in document

paragraph = section.AddParagraph();

paragraph.AppendText("\r\r[ Third Page ] \r\r" + paraText);

//Insert the default page header

paragraph = section.HeadersFooters.OddHeader.AddParagraph();

paragraph.AppendText("[ Default Page Header ]");

//Insert the default page footer

paragraph = section.HeadersFooters.OddFooter.AddParagraph();

paragraph.AppendText("[ Default Page Footer ]");

//Save and close the Word document instance

document.Save("Sample.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB] 

'Create a new document

Dim document As New WordDocument()

'Add the first section to the document

Dim section As IWSection = document.AddSection()

'Specify the value to header distance

section.PageSetup.HeaderDistance = 100

' Specify the value to footer distance

section.PageSetup.FooterDistance = 100

'Add a paragraph to the section

Dim paragraph As IWParagraph = section.AddParagraph()

Dim paraText As String = "Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula"

'Append some text to the first page in document

paragraph.AppendText(Convert.ToString(vbCr & vbCr & "[ First Page ] " & vbCr & vbCr) & paraText)

paragraph.ParagraphFormat.PageBreakAfter = True

'Append some text to the second page in document

paragraph = section.AddParagraph()

paragraph.AppendText(Convert.ToString(vbCr & vbCr & "[ Second Page ] " & vbCr & vbCr) & paraText)

paragraph.ParagraphFormat.PageBreakAfter = True

'Append some text to the third page in document

paragraph = section.AddParagraph()

paragraph.AppendText(Convert.ToString(vbCr & vbCr & "[ Third Page ] " & vbCr & vbCr) & paraText)

'Insert the default page header

paragraph = section.HeadersFooters.OddHeader.AddParagraph()

paragraph.AppendText("[ Default Page Header ]")

'Insert the default page footer

paragraph = section.HeadersFooters.OddFooter.AddParagraph()

paragraph.AppendText("[ Default Page Footer ]")

‘Save & close the Word document instance

document.Save("Sample.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

## Removing a Section

The following code snippet illustrates how to remove a particular section from the Word document

{% highlight c# %}
[C#] 

//Open an input Word template

WordDocument document = new WordDocument(inputFileName);

//Remove the second section from the collection

document.Sections.RemoveAt(1);

//Save and close the Word document instance

document.Save("Sample.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB] 

'Open an input Word template

Dim document As New WordDocument(inputFileName)

'Remove the second section from the collection

document.Sections.RemoveAt(1)

‘Save & close the Word document instance

document.Save("Sample.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

