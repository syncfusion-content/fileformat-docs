---
title: Working with Paragraph
description: This section describes about the child elements of a Paragraph  
platform: file-formats
control: DocIO
documentation: UG
---
# Working with Paragraph

Paragraph is the basic element in the Word document that contains a textual as well as graphical contents. Each paragraph has its own formatting such as line spacing, alignment, indentation etc. Within a paragraph, the contents are represented by one or more child elements such as `WTextRange`, `WPicture`, and `Hyperlink` etc. `ParagraphItem` is the base class for the child elements of paragraph. The following elements can be the child elements of a paragraph:

* Text – represented by an instance of `WTextRange`.
* Image – represented by an instance of `WPicture`. 
* Comments - represented by an instance of `WComment`.
* Hyperlink – represented by an instance of `Hyperlink`. 
* Symbols - represented by an instance of `WSymbol`. 
* Breaks - represented by an instance of `Break`. 
* OLE Object – represented by an instance of `WOleObject`. 
* Shapes -  represented by an instance of `Shape`. 
* TextBox – represented by an instance of `WTextBox`. 
* Chart – represented by an instance of `WChart`.
* Fields – represented by an instance of `WField`.
* Form Fields – represented by an instance of `WFormField`.
* Bookmarks – represented by instances of `BookmarkStart` and `BookmarkEnd`. 
* Absolute Tab – represented by an instance of `WAbsoluteTab`.
* Footnotes, Endnotes  - represented by an instance of `WFootnote`.

The following code example illustrates how to add a new paragraph.

{% tabs %}  

{% highlight c# %}

//Creates a new Word document 

WordDocument document = new WordDocument();

//Adds new section to the document

IWSection section = document.AddSection();

//Adds new paragraph to the section

IWParagraph paragraph = section.AddParagraph();

//Adds new text to the paragraph

paragraph.AppendText("Adding new paragraph to the document");

//Saves the Word document

document.Save("Sample.docx", FormatType.Docx);

//Closes the document

document.Close();


{% endhighlight %}

{% highlight vb.net %}

'Creates a new Word document 

Dim document As New WordDocument()

'Adds new section to the document

Dim section As IWSection = document.AddSection()

'Adds new paragraph to the section

Dim paragraph As IWParagraph = section.AddParagraph()

'Adds new text to the paragraph

paragraph.AppendText("Adding new paragraph to the document")

'Saves the Word document

document.Save("Sample.docx", FormatType.Docx)

'Closes the document

document.Close()

{% endhighlight %}

{% endtabs %}  

The following code example illustrates how to modify an existing paragraph.

{% tabs %}  

{% highlight c# %}

//Loads the template document

WordDocument document = new WordDocument("Template.docx");

//Gets the text body of first section

WTextBody textBody = document.Sections[0].Body;

//Gets the paragraph at index 1

WParagraph paragraph= textBody.Paragraphs[1];

//Iterates through the child elements of paragraph

foreach (ParagraphItem item in paragraph.ChildEntities)

{

if (item is WTextRange)

{

WTextRange text = item as WTextRange;

//Modifies the character format of the text

text.CharacterFormat.Bold = true;

break;

}

}

//Saves the Word document

document.Save("Sample.docx", FormatType.Docx);

//Closes the document

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Loads the template document

Dim document As New WordDocument("Template.docx")

'Gets the text body of first section

Dim textBody As WTextBody = document.Sections(0).Body

'Gets the paragraph at index 1

Dim paragraph As WParagraph = textBody.Paragraphs(1)

'Iterates through the child elements of paragraph

For Each item As ParagraphItem In paragraph.ChildEntities

If TypeOf item Is WTextRange Then

Dim text As WTextRange = TryCast(item, WTextRange)

'Modifies the character format of the text

text.CharacterFormat.Bold = True

Exit For

End If

Next

'Saves the Word document

document.Save("Sample.docx", FormatType.Docx)

'Closes the document

document.Close()

{% endhighlight %}

{% endtabs %}  

## Applying Paragraph Formatting

As in the Microsoft Word, DocIO provides support for all the paragraph formatting options such as line spacing, indentation, spacing before and after, keep follow etc. The following code example illustrates how to apply formatting to a paragraph.

N> `FirstLineIndent` can be used to update or retrieve for both hanging and first line indents. Negative value for this property denotes the hanging indent and positive value denotes the first line indent of the paragraph.

{% tabs %} 

{% highlight c# %}

//Creates a new Word document 

WordDocument document = new WordDocument();

//Adds new section to the document

IWSection section = document.AddSection();

//Adds new paragraph to the section

IWParagraph paragraph = section.AddParagraph();

//Adds new text to the paragraph

IWTextRange firsttext = paragraph.AppendText("Paragraphs are the basic elements of the Word document. It can contain text and images.");

//Applies paragraph formatting

paragraph.ParagraphFormat.AfterSpacing = 18f;

paragraph.ParagraphFormat.BeforeSpacing = 18f;

paragraph.ParagraphFormat.BackColor = Color.LightGray;

paragraph.ParagraphFormat.FirstLineIndent = 10f;

paragraph.ParagraphFormat.LineSpacing = 10f;

paragraph.ParagraphFormat.HorizontalAlignment = HorizontalAlignment.Right;

//Saves the Word document

document.Save("Sample.docx", FormatType.Docx);

//Closes the document

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates a new Word document 

Dim document As New WordDocument()

'Adds new section to the document

Dim section As IWSection = document.AddSection()

'Adds new paragraph to the section

Dim paragraph As IWParagraph = section.AddParagraph()

'Adds new text to the paragraph

Dim firsttext As IWTextRange = paragraph.AppendText("Paragraphs are the basic elements of the Word document. It can contain text and images.")

'Applies paragraph formatting

paragraph.ParagraphFormat.AfterSpacing = 18.0F

paragraph.ParagraphFormat.BeforeSpacing = 18.0F

paragraph.ParagraphFormat.BackColor = Color.LightGray

paragraph.ParagraphFormat.FirstLineIndent = 10.0F

paragraph.ParagraphFormat.LineSpacing = 10.0F

paragraph.ParagraphFormat.HorizontalAlignment = HorizontalAlignment.Right

'Saves the Word document

document.Save("Sample.docx", FormatType.Docx)

'Closes the document

document.Close()

{% endhighlight %}   

{% endtabs %}  

Paragraph style contains definition for both font (text) as well as paragraph formatting that can be applied to the contents of an entire paragraph. DocIO supports various pre-defined styles and also provides ability to create custom paragraph styles.

T> You can define a custom style or modify any built-in style to the required formatting, and apply this style to the part of Word document to be formatted. You can reduce the file size and code length by using styles instead of formatting each element explicitly.

The following code example illustrates how to use the predefined styles.

{% tabs %}  

{% highlight c# %}

//Creates a new Word document 

WordDocument document = new WordDocument();

//Adds new section to the document

IWSection section = document.AddSection();

//Adds new paragraph to the section

IWParagraph firstParagraph = section.AddParagraph();

//Adds new text to the paragraph

IWTextRange firsttext = firstParagraph.AppendText("Built-in styles can be applied to the paragraph. Heading1 style is applied to this paragraph.");

//Applies built-in style for the paragraph

firstParagraph.ApplyStyle(BuiltinStyle.Heading1);

//Saves the Word document

document.Save("Sample.docx", FormatType.Docx);

//Closes the document

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates a new Word document 

Dim document As New WordDocument()

'Adds new section to the document

Dim section As IWSection = document.AddSection()

'Adds new paragraph to the section

Dim firstParagraph As IWParagraph = section.AddParagraph()

'Adds new text to the paragraph

Dim firsttext As IWTextRange = firstParagraph.AppendText("Built-in styles can be applied to the paragraph. Heading1 style is applied to this paragraph.")

'Applies built-in style for the paragraph

firstParagraph.ApplyStyle(BuiltinStyle.Heading1)

'Saves the Word document

document.Save("Sample.docx", FormatType.Docx)

'Closes the document

document.Close()

{% endhighlight %}

{% endtabs %}  

The following code example illustrates how to create a custom paragraph style and apply it to a paragraph.

{% tabs %} 

{% highlight c# %}

//Creates a new Word document 

WordDocument document = new WordDocument();

//Adds new section to the document

IWSection section = document.AddSection();

//Creates user defined style

IWParagraphStyle style = document.AddParagraphStyle("User_defined_style");

style.ParagraphFormat.BackColor = Color.LightGray;

style.ParagraphFormat.AfterSpacing = 18f;

style.ParagraphFormat.BeforeSpacing = 18f;

style.ParagraphFormat.Borders.BorderType = Syncfusion.DocIO.DLS.BorderStyle.DotDash;

style.ParagraphFormat.Borders.LineWidth = 0.5f;

style.ParagraphFormat.LineSpacing = 15f;

style.CharacterFormat.FontName = "Calibri";

style.CharacterFormat.Italic = true;

//Adds new paragraph to the section

IWParagraph paragraph = section.AddParagraph();

IWTextRange text = paragraph.AppendText("A new paragraph style is created and is applied to this paragraph.");

//Applies the new style to paragraph

paragraph.ApplyStyle("User_defined_style");

//Saves the Word document

document.Save("Sample.docx", FormatType.Docx);

//Closes the document

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates a new Word document 

Dim document As New WordDocument()

'Adds new section to the document

Dim section As IWSection = document.AddSection()

'Creates user defined style

Dim style As IWParagraphStyle = document.AddParagraphStyle("User_defined_style")

style.ParagraphFormat.BackColor = Color.LightGray

style.ParagraphFormat.AfterSpacing = 18.0F

style.ParagraphFormat.BeforeSpacing = 18.0F

style.ParagraphFormat.Borders.BorderType = Syncfusion.DocIO.DLS.BorderStyle.DotDash

style.ParagraphFormat.Borders.LineWidth = 0.5F

style.ParagraphFormat.LineSpacing = 15.0F

style.CharacterFormat.FontName = "Calibri"

style.CharacterFormat.Italic = True

'Adds new paragraph to the section

Dim paragraph As IWParagraph = section.AddParagraph()

Dim text As IWTextRange = paragraph.AppendText("A new paragraph style is created and is applied to this paragraph.")

'Applies the new style to paragraph

paragraph.ApplyStyle("User_defined_style")

'Saves the Word document

document.Save("Sample.docx", FormatType.Docx)

'Closes the document

document.Close()

{% endhighlight %} 

{% endtabs %}  

A tab stop is a horizontal position that is set for aligning text of the paragraph.  A tab character causes the carriage to go to the next tab stop.

Each paragraph has its own tab stop collection where the new tab stop can be added and existing tab stop can be removed.

The following code example illustrates how to add tab stops to the paragraph.

{% tabs %}  

{% highlight c# %}

//Creates a new Word document 

WordDocument document = new WordDocument();

//Adds new section to the document

IWSection section = document.AddSection();

//Adds new paragraph to the section

IWParagraph paragraph = section.AddParagraph();

//Adds tab stop at position 11

Tab firstTab = paragraph.ParagraphFormat.Tabs.AddTab(11, TabJustification.Left, TabLeader.Dotted);            

//Adds tab stop at position 62

paragraph.ParagraphFormat.Tabs.AddTab(62, TabJustification.Left, TabLeader.Single);

paragraph.AppendText("This sample\t illustrates the use of tabs in the paragraph. Tabs\t can be inserted or removed from the paragraph.");

//Removes tab stop from the collection

paragraph.ParagraphFormat.Tabs.RemoveByTabPosition(11);

//Saves the Word document

document.Save("Sample.docx", FormatType.Docx);

//Closes the document

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates a new Word document 

Dim document As New WordDocument()

'Adds new section to the document

Dim section As IWSection = document.AddSection()

'Adds new paragraph to the section

Dim paragraph As IWParagraph = section.AddParagraph()

'Adds tab stop at position 11

Dim firstTab As Tab = paragraph.ParagraphFormat.Tabs.AddTab(11, TabJustification.Left, TabLeader.Dotted)

'Adds tab stop at position 62

paragraph.ParagraphFormat.Tabs.AddTab(62, TabJustification.Left, TabLeader.[Single])

paragraph.AppendText("This sample" & vbTab & " illustrates the use of tabs in the paragraph. Tabs" & vbTab & " can be inserted or removed from the paragraph.")

'Removes tab stop from the collection

paragraph.ParagraphFormat.Tabs.RemoveByTabPosition(11)

'Saves the Word document

document.Save("Sample.docx", FormatType.Docx)

'Closes the document

document.Close()

{% endhighlight %}  

{% endtabs %}  

## Working with Text 

Text within a paragraph is represented by one or more instances of the `WTextRange`. Each `WTextRange` instance can have its own font (text) formatting.  

The following code example illustrates how to append text to the paragraph.

{% tabs %} 

{% highlight c# %}

//Creates a new Word document 

WordDocument document = new WordDocument();

//Adds new section to the document

IWSection section = document.AddSection();

//Adds new paragraph to the section

IWParagraph firstParagraph = section.AddParagraph();

//Adds new text to the paragraph

IWTextRange firsttext = firstParagraph.AppendText("A new text is added to the paragraph.");

firsttext.CharacterFormat.FontSize = 14;

firsttext.CharacterFormat.Bold = true;

firsttext.CharacterFormat.TextColor = Color.Green;

//Saves the Word document

document.Save("Sample.docx", FormatType.Docx);

//Closes the document

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates a new Word document 

Dim document As New WordDocument()

'Adds new section to the document

Dim section As IWSection = document.AddSection()

'Adds new paragraph to the section

Dim firstParagraph As IWParagraph = section.AddParagraph()

'Adds new text to the paragraph

Dim firsttext As IWTextRange = firstParagraph.AppendText("A new text is added to the paragraph.")

firsttext.CharacterFormat.FontSize = 14

firsttext.CharacterFormat.Bold = True

firsttext.CharacterFormat.TextColor = Color.Green

'Saves the Word document

document.Save("Sample.docx", FormatType.Docx)

'Closes the document

document.Close()

{% endhighlight %}

{% endtabs %}  

Text in the paragraph can be modified or replaced with a new text. This can be achieved by iterating through the paragraph items.

The following code example illustrates how to replace the text of a text range.

{% tabs %} 

{% highlight c# %}

//Loads the template document 

WordDocument document = new WordDocument("Template.docx");

//Gets the last paragraph

WParagraph lastParagraph = document.LastParagraph;

//Iterates through the paragraph items to get the textrange and modifies its content.

for (int i = 0; i < lastParagraph.ChildEntities.Count; i++)

{

if (lastParagraph.ChildEntities[i] is WTextRange)

{

WTextRange textRange = lastParagraph.ChildEntities[i] as WTextRange;

textRange.Text = "First text range of the last paragraph is replaced";

textRange.CharacterFormat.FontSize = 14;

break;

}

} 

//Saves the Word document

document.Save("Sample.docx", FormatType.Docx);

//Closes the document

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Loads the template document 

Dim document As New WordDocument("Template.docx")

'Gets the last paragraph

Dim lastParagraph As WParagraph = document.LastParagraph

'Iterates through the paragraph items to get the textrange and modifies its content

For i As Integer = 0 To lastParagraph.ChildEntities.Count - 1

If TypeOf lastParagraph.ChildEntities(i) Is WTextRange Then

Dim textRange As WTextRange = TryCast(lastParagraph.ChildEntities(i), WTextRange)

textRange.Text = "First text range of the last paragraph is replaced"

textRange.CharacterFormat.FontSize = 14

Exit For

End If

Next

'Saves the Word document

document.Save("Sample.docx", FormatType.Docx)

'Closes the document

document.Close()

{% endhighlight %}

{% endtabs %}  

Text formatting enhances the appearance of text in the document. Text formatting includes font size, font color, font name, bold, italic, underline, etc. 

The following code example illustrates how to apply formatting for the text.

{% tabs %}  

{% highlight c# %}

//Creates a new Word document 

WordDocument document = new WordDocument();

//Adds new section to the document

IWSection section = document.AddSection();

//Adds new paragraph to the section

IWParagraph firstParagraph = section.AddParagraph();

//Adds new text to the paragraph

IWTextRange firsttext = firstParagraph.AppendText("This is the first text range. ");

//Applies formatting for first text range

firsttext.CharacterFormat.Bold = true;

firsttext.CharacterFormat.FontSize = 14;

firsttext.CharacterFormat.Shadow = true;

firsttext.CharacterFormat.SmallCaps = true;

IWTextRange secondtext = firstParagraph.AppendText("This the second text range");

//Applies formatting for second text range

secondtext.CharacterFormat.HighlightColor = Color.GreenYellow;

secondtext.CharacterFormat.UnderlineStyle = UnderlineStyle.DotDash;

secondtext.CharacterFormat.Italic = true;

secondtext.CharacterFormat.FontName = "Times New Roman";

secondtext.CharacterFormat.TextColor = Color.Green;

//Saves the Word document

document.Save("Sample.docx", FormatType.Docx);

//Closes the document

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates a new Word document 

Dim document As New WordDocument()

'Adds new section to the document

Dim section As IWSection = document.AddSection()

'Adds new paragraph to the section

Dim firstParagraph As IWParagraph = section.AddParagraph()

'Adds new text to the paragraph

Dim firsttext As IWTextRange = firstParagraph.AppendText("This is the first text range. ")

'Applies formatting for first text range

firsttext.CharacterFormat.Bold = True

firsttext.CharacterFormat.FontSize = 14

firsttext.CharacterFormat.Shadow = True

firsttext.CharacterFormat.SmallCaps = True

Dim secondtext As IWTextRange = firstParagraph.AppendText("This the second text range")

'Applies formatting for second text range

secondtext.CharacterFormat.HighlightColor = Color.GreenYellow

secondtext.CharacterFormat.UnderlineStyle = UnderlineStyle.DotDash

secondtext.CharacterFormat.Italic = True

secondtext.CharacterFormat.FontName = "Times New Roman"

secondtext.CharacterFormat.TextColor = Color.Green

'Saves the Word document

document.Save("Sample.docx", FormatType.Docx)

'Closes the document

document.Close()

{% endhighlight %}

{% endtabs %}  

## Working with Images

DocIO provides support for both inline and absolute positioned images. 

* Inline images – The position of the image is constrained to the lines of text on the page.
* Absolute positioned images – The images can be positioned anywhere irrespective of the lines of text.

The following code example illustrates how to add image to the paragraph.

{% tabs %}   

{% highlight c# %}

//Creates a new Word document 

WordDocument document = new WordDocument();

//Adds new section to the document

IWSection section = document.AddSection();

//Adds new paragraph to the section

IWParagraph firstParagraph = section.AddParagraph();

//Adds image to  the paragraph

IWPicture picture = firstParagraph.AppendPicture(Image.FromFile("Image.png"));

//Sets height and width for the image

picture.Height = 100;

picture.Width = 100;

//Saves the Word document

document.Save("Sample.docx", FormatType.Docx);

//Closes the document

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates a new Word document 

Dim document As New WordDocument()

'Adds new section to the document

Dim section As IWSection = document.AddSection()

'Adds new paragraph to the section

Dim firstParagraph As IWParagraph = section.AddParagraph()

'Adds image to  the paragraph

Dim picture As IWPicture = firstParagraph.AppendPicture(Image.FromFile("Image.png"))

'Sets height and width for the image

picture.Height = 100

picture.Width = 100

'Saves the Word document

document.Save("Sample.docx", FormatType.Docx)

'Closes the document

document.Close()

{% endhighlight %} 

 {% endtabs %} 

Image present in the document can be replaced with a new image. This can be achieved by iterating through the paragraph items.

The following code example illustrates how to replace an existing image:

{% tabs %}   

{% highlight c# %}

//Loads the template document

WordDocument document = new WordDocument("Template.docx");

WTextBody textbody = document.Sections[0].Body;            

//Iterates through the paragraphs of the textbody

foreach (WParagraph paragraph in textbody.Paragraphs)

{

//Iterates through the child elements of paragraph

foreach (ParagraphItem item in paragraph.ChildEntities)

{

if (item is WPicture)

{

WPicture picture = item as WPicture;

//Replaces the image

if(picture.Title == "Bookmark")

picture.LoadImage(Image.FromFile("Image.png"));

}

}

} 

//Saves the Word document

document.Save("Sample.docx", FormatType.Docx);

//Closes the document

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Loads the template document

Dim document As New WordDocument("Template.docx")

Dim textbody As WTextBody = document.Sections(0).Body

'Iterates through the paragraphs of the textbody

For Each paragraph As WParagraph In textbody.Paragraphs

'Iterates through the child elements of paragraph

For Each item As ParagraphItem In paragraph.ChildEntities

If TypeOf item Is WPicture Then

Dim picture As WPicture = TryCast(item, WPicture)

'Replaces the image

If picture.Title = "Bookmark" Then

picture.LoadImage(Image.FromFile("Image.png"))

End If

End If

Next

Next

'Saves the Word document

document.Save("Sample.docx", FormatType.Docx)

'Closes the document

document.Close()

{% endhighlight %}

{% endtabs %} 

Images can be removed from the document by removing it from the paragraph items. 

The following code example illustrates how to remove the image from the paragraph items:

{% tabs %} 

{% highlight c# %}

//Loads the template document 

WordDocument document = new WordDocument("Template.docx");

WTextBody textbody = document.Sections[0].Body;            

//Iterates through the paragraphs of the textbody

foreach (WParagraph paragraph in textbody.Paragraphs)

{

//Iterates through the child elements of paragraph

for (int i = 0; i < paragraph.ChildEntities.Count; i++)

{

//Removes images from the paragraph

if (paragraph.ChildEntities[i] is WPicture)

{

paragraph.Items.RemoveAt(i);

i--;

}

}

}

//Saves the Word document

document.Save("Sample.docx", FormatType.Docx);

//Closes the document

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Loads the template document 

Dim document As New WordDocument("Template.docx")

Dim textbody As WTextBody = document.Sections(0).Body

'Iterates through the paragraphs of the textbody

For Each paragraph As WParagraph In textbody.Paragraphs

'Iterates through the child elements of paragraph

For i As Integer = 0 To paragraph.ChildEntities.Count - 1

'Removes images from the paragraph

If TypeOf paragraph.ChildEntities(i) Is WPicture Then

paragraph.Items.RemoveAt(i)

i -= 1

End If

Next

Next

'Saves the Word document

document.Save("Sample.docx", FormatType.Docx)

'Closes the document

document.Close()

{% endhighlight %} 

{% endtabs %}  

Absolute positioned images have properties such as position, wrap formats, and alignments. These properties are not applicable when the text wrapping style is inline.

The following code example illustrates how various picture formats can be applied to the picture:

{% tabs %} 

{% highlight c# %}

//Creates a new Word document 

WordDocument document = new WordDocument();

//Adds new section to the document

IWSection section = document.AddSection();

//Adds new paragraph to the section

IWParagraph paragraph = section.AddParagraph();

paragraph.AppendText("This paragraph has picture. ");

//Appends new picture to the paragraph

IWPicture picture = paragraph.AppendPicture(Image.FromFile("Image.png"));

//Sets text wrapping style – When the wrapping style is inline, the images are not absolutely positioned. It is added next to the textrange.

picture.TextWrappingStyle = TextWrappingStyle.Square;

//Sets horizontal and vertical origin

picture.HorizontalOrigin = HorizontalOrigin.Page;

picture.VerticalOrigin = VerticalOrigin.Paragraph;

//Sets width and height for the paragraph

picture.Width = 150;

picture.Height = 100;

//Sets horizontal and vertical position for the picture

picture.HorizontalPosition = 200;

picture.VerticalPosition = 150;

picture.Name = "PictureName";

//Sets horizontal and vertical alignments

picture.HorizontalAlignment = ShapeHorizontalAlignment.Center;

picture.VerticalAlignment = ShapeVerticalAlignment.Bottom;

//Saves the Word document

document.Save("Sample.docx", FormatType.Docx);

//Closes the document

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates a new Word document 

Dim document As New WordDocument()

'Adds new section to the document

Dim section As IWSection = document.AddSection()

'Adds new paragraph to the section

Dim paragraph As IWParagraph = section.AddParagraph()

paragraph.AppendText("This paragraph has picture. ")

'Appends new picture to the paragraph

Dim picture As IWPicture = paragraph.AppendPicture(Image.FromFile("Image.png"))

'Sets text wrapping style – When the wrapping style is inline, the images are not absolutely positioned. It is added next to the textrange.

picture.TextWrappingStyle = TextWrappingStyle.Square

'Sets horizontal and vertical origin

picture.HorizontalOrigin = HorizontalOrigin.Page

picture.VerticalOrigin = VerticalOrigin.Paragraph

'Sets width and height for the paragraph

picture.Width = 150

picture.Height = 100

'Sets horizontal and vertical position for the picture

picture.HorizontalPosition = 200

picture.VerticalPosition = 150

picture.Name = "PictureName"

'Sets horizontal and vertical alignments

picture.HorizontalAlignment = ShapeHorizontalAlignment.Center

picture.VerticalAlignment = ShapeVerticalAlignment.Bottom

'Saves the Word document

document.Save("Sample.docx", FormatType.Docx)

'Closes the document

document.Close()

{% endhighlight %}  

{% endtabs %}  

An Image with a specific title can be retrieved by iterating the paragraph items that can be used for further manipulations.

The following code example illustrates how images can be iterated from the document elements.

{% tabs %}  

{% highlight c# %}

//Creates a new Word document 

WordDocument document = new WordDocument("Template.docx");

//Gets textbody content

WTextBody textBody = document.Sections[0].Body;

//Iterates through the textbody child entities

foreach (TextBodyItem item in textBody.ChildEntities)

{

if (item is WParagraph)

{

WParagraph paragraph = item as WParagraph;

foreach (ParagraphItem paraItem in paragraph.ChildEntities)

{

//Gets the image from its title and modifies its width and height

if (paraItem is WPicture)

{

WPicture picture = paraItem as WPicture;

if (picture.Title == "Bookmark")

{

picture.Width = 150;

picture.Height = 100;

}

}    

}

}

}

//Saves the Word document

document.Save("Sample.docx", FormatType.Docx);

//Closes the document

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates a new Word document 

Dim document As New WordDocument("Template.docx")

'Gets textbody content

Dim textBody As WTextBody = document.Sections(0).Body

'Iterates through the textbody child entities

For Each item As TextBodyItem In textBody.ChildEntities

If TypeOf item Is WParagraph Then

Dim paragraph As WParagraph = TryCast(item, WParagraph)

For Each paraItem As ParagraphItem In paragraph.ChildEntities

'Gets the image from its title and modifies its width and height

If TypeOf paraItem Is WPicture Then

Dim picture As WPicture = TryCast(paraItem, WPicture)

If picture.Title = "Bookmark" Then

picture.Width = 150

picture.Height = 100

End If

End If

Next

End If

Next

'Saves the Word document

document.Save("Sample.docx", FormatType.Docx)

'Closes the document

document.Close()

{% endhighlight %}

{% endtabs %}  

## Working with Lists

Lists can organize and format the contents of the document in hierarchical way. There are 9 levels in the list, starting from level 0 to level 8. DocIO supports both built-in list styles and custom list styles. The following are the types of list supported in DocIO. 

* Numbered list
* Bulleted list 

The following code example illustrates how to create a simple bulleted list:

{% tabs %} 

{% highlight c# %}

//Creates a new Word document 

WordDocument document = new WordDocument();

//Adds new section to the document

IWSection section = document.AddSection();

//Adds new paragraph to the section

IWParagraph paragraph = section.AddParagraph();

//Applies default numbered list style

paragraph.ListFormat.ApplyDefBulletStyle();

//Adds text to the paragraph

paragraph.AppendText("List item 1");

//Continues the list defined

paragraph.ListFormat.ContinueListNumbering();

//Adds second paragraph

paragraph = section.AddParagraph();

paragraph.AppendText("List item 2");

//Continues last defined list

paragraph.ListFormat.ContinueListNumbering();

//Adds new paragraph

paragraph = section.AddParagraph();

paragraph.AppendText("List item 3");

//Continues last defined list

paragraph.ListFormat.ContinueListNumbering();

//Saves the Word document

document.Save("Sample.docx", FormatType.Docx);

//Closes the document

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates a new Word document 

Dim document As New WordDocument()

'Adds new section to the document

Dim section As IWSection = document.AddSection()

'Adds new paragraph to the section

Dim paragraph As IWParagraph = section.AddParagraph()

'Applies default numbered list style

paragraph.ListFormat.ApplyDefBulletStyle()

'Adds text to the paragraph

paragraph.AppendText("List item 1")

'Continues the list defined

paragraph.ListFormat.ContinueListNumbering()

'Adds second paragraph

paragraph = section.AddParagraph()

paragraph.AppendText("List item 2")

'Continues last defined list

paragraph.ListFormat.ContinueListNumbering()

'Adds new paragraph

paragraph = section.AddParagraph()

paragraph.AppendText("List item 3")

'Continues last defined list

paragraph.ListFormat.ContinueListNumbering()

'Saves the Word document

document.Save("Sample.docx", FormatType.Docx)

'Closes the document

document.Close()

{% endhighlight %}  

 {% endtabs %}  

The following code example illustrates how to create simple numbered list:

{% tabs %} 

{% highlight c# %}

//Creates a new Word document 

WordDocument document = new WordDocument();

//Adds new section to the document

IWSection section = document.AddSection();

//Adds new paragraph to the section

IWParagraph paragraph = section.AddParagraph();

//Applies default numbered list style

paragraph.ListFormat.ApplyDefNumberedStyle();

//Adds text to the paragraph

paragraph.AppendText("List item 1");

//Continues the list defined

paragraph.ListFormat.ContinueListNumbering();

//Adds second paragraph

paragraph = section.AddParagraph();

paragraph.AppendText("List item 2");

//Continues last defined list

paragraph.ListFormat.ContinueListNumbering();

//Adds new paragraph

paragraph = section.AddParagraph();

paragraph.AppendText("List item 3");

//Continues last defined list

paragraph.ListFormat.ContinueListNumbering();

//Saves the Word document

document.Save("Sample.docx", FormatType.Docx);

//Closes the document

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates a new Word document 

Dim document As New WordDocument()

'Adds new section to the document

Dim section As IWSection = document.AddSection()

'Adds new paragraph to the section

Dim paragraph As IWParagraph = section.AddParagraph()

'Applies default numbered list style

paragraph.ListFormat.ApplyDefNumberedStyle()

'Adds text to the paragraph

paragraph.AppendText("List item 1")

'Continues the list defined

paragraph.ListFormat.ContinueListNumbering()

'Adds second paragraph

paragraph = section.AddParagraph()

paragraph.AppendText("List item 2")

'Continues last defined list

paragraph.ListFormat.ContinueListNumbering()

'Adds new paragraph

paragraph = section.AddParagraph()

paragraph.AppendText("List item 3")

'Continues last defined list

paragraph.ListFormat.ContinueListNumbering()

'Saves the Word document

document.Save("Sample.docx", FormatType.Docx)

'Closes the document

document.Close()

{% endhighlight %} 

  {% endtabs %}  

The following code example illustrates how to create a multi-level bulleted list.

{% tabs %}  

{% highlight c# %}

//Creates a new Word document 

WordDocument document = new WordDocument();

//Adds new section to the document

IWSection section = document.AddSection();

//Adds new paragraph to the section

IWParagraph paragraph = section.AddParagraph();

//Applies default numbered list style

paragraph.ListFormat.ApplyDefBulletStyle();

//Adds text to the paragraph

paragraph.AppendText("List item 1 - Level 0");

//Continues the list defined

paragraph.ListFormat.ContinueListNumbering();

//Adds second paragraph

paragraph = section.AddParagraph();

paragraph.AppendText("List item 2 - Level 1");

//Continues last defined list

paragraph.ListFormat.ContinueListNumbering();

//Increases the level indent

paragraph.ListFormat.IncreaseIndentLevel();

//Adds new paragraph

paragraph = section.AddParagraph();

paragraph.AppendText("List item 3 - Level 2");

//Continues last defined list

paragraph.ListFormat.ContinueListNumbering();

//Increases the level indent

paragraph.ListFormat.IncreaseIndentLevel();

//Saves the Word document

document.Save("Sample.docx", FormatType.Docx);

//Closes the document

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates a new Word document 

Dim document As New WordDocument()

'Adds new section to the document

Dim section As IWSection = document.AddSection()

'Adds new paragraph to the section

Dim paragraph As IWParagraph = section.AddParagraph()

'Applies default numbered list style

paragraph.ListFormat.ApplyDefBulletStyle()

'Adds text to the paragraph

paragraph.AppendText("List item 1 - Level 0")

'Continues the list defined

paragraph.ListFormat.ContinueListNumbering()

'Adds second paragraph

paragraph = section.AddParagraph()

paragraph.AppendText("List item 2 - Level 1")

'Continues last defined list

paragraph.ListFormat.ContinueListNumbering()

'Increases the level indent

paragraph.ListFormat.IncreaseIndentLevel()

'Adds new paragraph

paragraph = section.AddParagraph()

paragraph.AppendText("List item 3 - Level 2")

'Continues last defined list

paragraph.ListFormat.ContinueListNumbering()

'Increases the level indent

paragraph.ListFormat.IncreaseIndentLevel()

'Saves the Word document

document.Save("Sample.docx", FormatType.Docx)

'Closes the document

document.Close()

{% endhighlight %} 

{% endtabs %}  

The following code example illustrates how to create multi-level numbered list.

{% tabs %}  

{% highlight c# %}

//Creates a new Word document 

WordDocument document = new WordDocument();

//Adds new section to the document

IWSection section = document.AddSection();

//Adds new paragraph to the section

IWParagraph paragraph = section.AddParagraph();

//Applies default numbered list style

paragraph.ListFormat.ApplyDefNumberedStyle();

//Adds text to the paragraph

paragraph.AppendText("List item 1 - Level 0");

//Continues the list defined

paragraph.ListFormat.ContinueListNumbering();

//Adds second paragraph

paragraph = section.AddParagraph();

paragraph.AppendText("List item 2 - Level 1");

//Continues last defined list

paragraph.ListFormat.ContinueListNumbering();

//Increases the level indent

paragraph.ListFormat.IncreaseIndentLevel();

//Adds new paragraph

paragraph = section.AddParagraph();

paragraph.AppendText("List item 3 - Level 2");

//Continues last defined list

paragraph.ListFormat.ContinueListNumbering();

//Increases the level indent

paragraph.ListFormat.IncreaseIndentLevel();

//Saves the Word document

document.Save("Sample.docx", FormatType.Docx);

//Closes the document

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates a new Word document 

Dim document As New WordDocument()

'Adds new section to the document

Dim section As IWSection = document.AddSection()

'Adds new paragraph to the section

Dim paragraph As IWParagraph = section.AddParagraph()

'Applies default numbered list style

paragraph.ListFormat.ApplyDefNumberedStyle()

'Adds text to the paragraph

paragraph.AppendText("List item 1 - Level 0")

'Continues the list defined

paragraph.ListFormat.ContinueListNumbering()

'Adds second paragraph

paragraph = section.AddParagraph()

paragraph.AppendText("List item 2 - Level 1")

'Continues last defined list

paragraph.ListFormat.ContinueListNumbering()

'Increases the level indent

paragraph.ListFormat.IncreaseIndentLevel()

'Adds new paragraph

paragraph = section.AddParagraph()

paragraph.AppendText("List item 3 - Level 2")

'Continues last defined list

paragraph.ListFormat.ContinueListNumbering()

'Increases the level indent

paragraph.ListFormat.IncreaseIndentLevel()

'Saves the Word document

document.Save("Sample.docx", FormatType.Docx)

'Closes the document

document.Close()

{% endhighlight %}  

{% endtabs %}  

The list levels can be incremented or decremented by using the `IncreaseIndentLevel` and `DecreaseIndentLevel` methods respectively. The following code example illustrates how to increase or decrease the list indent levels.

{% tabs %} 

{% highlight c# %}

//Creates a new Word document 

WordDocument document = new WordDocument();

//Adds new section to the document

IWSection section = document.AddSection();

//Adds new paragraph to the section

IWParagraph paragraph = section.AddParagraph();

//Applies default numbered list style

paragraph.ListFormat.ApplyDefNumberedStyle();

//Adds text to the paragraph

paragraph.AppendText("Multilevel numbered list - Level 0");

//Continues the list defined

paragraph.ListFormat.ContinueListNumbering();

//Adds second paragraph

paragraph = section.AddParagraph();

paragraph.AppendText("Multilevel numbered list - Level 1");

//Continues last defined list

paragraph.ListFormat.ContinueListNumbering();

//Increases the level indent

paragraph.ListFormat.IncreaseIndentLevel();

//Adds new paragraph

paragraph = section.AddParagraph();

paragraph.AppendText("Multilevel numbered list - Level 0");

//Continues last defined list

paragraph.ListFormat.ContinueListNumbering();

//Increases the level indent

paragraph.ListFormat.DecreaseIndentLevel();

//Adds new paragraph

paragraph = section.AddParagraph();

paragraph.AppendText("Multilevel numbered list - Level 1");

//Continues last defined list

paragraph.ListFormat.ContinueListNumbering();

//Increases the level indent

paragraph.ListFormat.IncreaseIndentLevel();

//Saves the Word document

document.Save("Sample.docx", FormatType.Docx);

//Closes the document

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates a new Word document 

Dim document As New WordDocument()

'Adds new section to the document

Dim section As IWSection = document.AddSection()

'Adds new paragraph to the section

Dim paragraph As IWParagraph = section.AddParagraph()

'Applies default numbered list style

paragraph.ListFormat.ApplyDefNumberedStyle()

'Adds text to the paragraph

paragraph.AppendText("Multilevel numbered list - Level 0")

'Continues the list defined

paragraph.ListFormat.ContinueListNumbering()

'Adds second paragraph

paragraph = section.AddParagraph()

paragraph.AppendText("Multilevel numbered list - Level 1")

'Continues last defined list

paragraph.ListFormat.ContinueListNumbering()

'Increases the level indent

paragraph.ListFormat.IncreaseIndentLevel()

'Adds new paragraph

paragraph = section.AddParagraph()

paragraph.AppendText("Multilevel numbered list - Level 0")

'Continues last defined list

paragraph.ListFormat.ContinueListNumbering()

'Increases the level indent

paragraph.ListFormat.DecreaseIndentLevel()

'Adds new paragraph

paragraph = section.AddParagraph()

paragraph.AppendText("Multilevel numbered list - Level 1")

'Continues last defined list

paragraph.ListFormat.ContinueListNumbering()

'Increases the level indent

paragraph.ListFormat.IncreaseIndentLevel()

'Saves the Word document

document.Save("Sample.docx", FormatType.Docx)

'Closes the document

document.Close()

{% endhighlight %} 

{% endtabs %}  

The following code example illustrates how to create user defined list styles.

{% tabs %}  

{% highlight c# %}

//Creates a new Word document 

WordDocument document = new WordDocument();

//Adds new section to the document

IWSection section = document.AddSection(); 

//Adds new list style to the document          

ListStyle listStyle = document.AddListStyle(ListType.Numbered, "UserdefinedList");

WListLevel levelOne = listStyle.Levels[0];

//Defines the follow character, prefix, suffix, start index for level 0

levelOne.FollowCharacter = FollowCharacterType.Tab;

levelOne.NumberPrefix = "(";

levelOne.NumberSufix = ")";

levelOne.PatternType = ListPatternType.LowRoman;

levelOne.StartAt = 1;

levelOne.TabSpaceAfter = 5;

levelOne.NumberAlignment = ListNumberAlignment.Center;

WListLevel levelTwo = listStyle.Levels[1];

//Defines the follow character, suffix, pattern, start index for level 1

levelTwo.FollowCharacter = FollowCharacterType.Tab;

levelTwo.NumberSufix = "}";

levelTwo.PatternType = ListPatternType.LowLetter;

levelTwo.StartAt = 2; 

//Adds new paragraph to the section

IWParagraph paragraph = section.AddParagraph();  

//Adds text to the paragraph

paragraph.AppendText("User defined list - Level 0");

//Applies default numbered list style

paragraph.ListFormat.ApplyStyle("UserdefinedList");

//Adds second paragraph

paragraph = section.AddParagraph();

paragraph.AppendText("User defined list - Level 1");

//Continues last defined list

paragraph.ListFormat.ContinueListNumbering();

//Increases the level indent

paragraph.ListFormat.IncreaseIndentLevel();

//Saves the Word document

document.Save("Sample.docx", FormatType.Docx);

//Closes the document

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates a new Word document 

Dim document As New WordDocument()

'Adds new section to the document

Dim section As IWSection = document.AddSection()

'Adds new list style to the document          

Dim listStyle As ListStyle = document.AddListStyle(ListType.Numbered, "UserdefinedList")

Dim levelOne As WListLevel = listStyle.Levels(0)

'Defines the follow character, prefix, suffix, start index for level 0

levelOne.FollowCharacter = FollowCharacterType.Tab

levelOne.NumberPrefix = "("

levelOne.NumberSufix = ")"

levelOne.PatternType = ListPatternType.LowRoman

levelOne.StartAt = 1

levelOne.TabSpaceAfter = 5

levelOne.NumberAlignment = ListNumberAlignment.Center

Dim levelTwo As WListLevel = listStyle.Levels(1)

'Defines the follow character, suffix, pattern, start index for level 1

levelTwo.FollowCharacter = FollowCharacterType.Tab

levelTwo.NumberSufix = "}"

levelTwo.PatternType = ListPatternType.LowLetter

levelTwo.StartAt = 2

'Adds new paragraph to the section

Dim paragraph As IWParagraph = section.AddParagraph()

'Adds text to the paragraph

paragraph.AppendText("User defined list - Level 0")

'Applies default numbered list style

paragraph.ListFormat.ApplyStyle("UserdefinedList")

'Adds second paragraph

paragraph = section.AddParagraph()

paragraph.AppendText("User defined list - Level 1")

'Continues last defined list

paragraph.ListFormat.ContinueListNumbering()

'Increases the level indent

paragraph.ListFormat.IncreaseIndentLevel()

'Saves the Word document

document.Save("Sample.docx", FormatType.Docx)

'Closes the document

document.Close()

{% endhighlight %}

{% endtabs %}  

The following code example illustrates how to create numbered list with prefix from previous level.

N> `NumberPrefix` value for the numbered list should meet the syntax "\u000N" in order to update the previous list level value as prefix to the current list level. For example, it should be represented as (“\u0000.” or “\u0000.\u0001.”).

{% tabs %}  

{% highlight c# %}

//Creates a new Word document 

WordDocument document = new WordDocument();

//Adds new section to the document

IWSection section = document.AddSection(); 

//Adds new list style to the document          

ListStyle listStyle = document.AddListStyle(ListType.Numbered, "UserdefinedList");

WListLevel levelOne = listStyle.Levels[0];

//Defines the follow character, prefix from previous level, start index for level 0

levelOne.FollowCharacter = FollowCharacterType.Nothing;

levelOne.PatternType = ListPatternType.Arabic;

levelOne.StartAt = 1;

WListLevel levelTwo = listStyle.Levels[1];

//Defines the follow character, prefix from previous level, pattern, start index for level 1

levelTwo.FollowCharacter = FollowCharacterType.Nothing;

levelTwo.NumberPrefix = "\u0000.";

levelTwo.PatternType = ListPatternType.Arabic;

levelTwo.StartAt = 1;

WListLevel levelThree = listStyle.Levels[2];

//Defines the follow character, prefix from previous level, pattern, start index for level 1

levelThree.FollowCharacter = FollowCharacterType.Nothing;

levelThree.NumberPrefix = "\u0000.\u0001.";

levelThree.PatternType = ListPatternType.Arabic;

levelThree.StartAt = 1; 

//Adds new paragraph to the section

IWParagraph paragraph = section.AddParagraph();  

//Adds text to the paragraph

paragraph.AppendText("User defined list - Level 0");

//Applies default numbered list style

paragraph.ListFormat.ApplyStyle("UserdefinedList");

//Adds second paragraph

paragraph = section.AddParagraph();

paragraph.AppendText("User defined list - Level 1");

//Continues last defined list

paragraph.ListFormat.ContinueListNumbering();

//Increases the level indent

paragraph.ListFormat.IncreaseIndentLevel();

//Adds second paragraph

paragraph = section.AddParagraph();

paragraph.AppendText("User defined list - Level 2");

//Continues last defined list

paragraph.ListFormat.ContinueListNumbering();

//Increases the level indent

paragraph.ListFormat.IncreaseIndentLevel();

//Saves the Word document

document.Save("Sample.docx", FormatType.Docx);

//Closes the document

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates a new Word document 

Dim document As New WordDocument()

'Adds new section to the document

Dim section As IWSection = document.AddSection()

'Adds new list style to the document          

Dim listStyle As ListStyle = document.AddListStyle(ListType.Numbered, "UserdefinedList")

Dim levelOne As WListLevel = listStyle.Levels(0)

'Defines the follow character, prefix from previous level, start index for level 0

levelOne.FollowCharacter = FollowCharacterType.[Nothing]

levelOne.PatternType = ListPatternType.Arabic

levelOne.StartAt = 1

Dim levelTwo As WListLevel = listStyle.Levels(1)

'Defines the follow character, prefix from previous level, pattern, start index for level 1

levelTwo.FollowCharacter = FollowCharacterType.[Nothing]

levelTwo.NumberPrefix = vbNullChar & "."

levelTwo.PatternType = ListPatternType.Arabic

levelTwo.StartAt = 1

Dim levelThree As WListLevel = listStyle.Levels(2)

'Defines the follow character, prefix from previous level, pattern, start index for level 1

levelThree.FollowCharacter = FollowCharacterType.[Nothing]

levelThree.NumberPrefix = vbNullChar & "." & ChrW(1) & "."

levelThree.PatternType = ListPatternType.Arabic

levelThree.StartAt = 1

'Adds new paragraph to the section

Dim paragraph As IWParagraph = section.AddParagraph()

'Adds text to the paragraph

paragraph.AppendText("User defined list - Level 0")

'Applies default numbered list style

paragraph.ListFormat.ApplyStyle("UserdefinedList")

'Adds second paragraph

paragraph = section.AddParagraph()

paragraph.AppendText("User defined list - Level 1")

'Continues last defined list

paragraph.ListFormat.ContinueListNumbering()

'Increases the level indent

paragraph.ListFormat.IncreaseIndentLevel()

'Adds second paragraph

paragraph = section.AddParagraph()

paragraph.AppendText("User defined list - Level 2")

'Continues last defined list

paragraph.ListFormat.ContinueListNumbering()

'Increases the level indent

paragraph.ListFormat.IncreaseIndentLevel()

'Saves the Word document

document.Save("Sample.docx", FormatType.Docx)

'Closes the document

document.Close()

{% endhighlight %}

{% endtabs %}  

## Working with Hyperlinks

Hyperlink is a reference to data that can link to external contents like images, files, web page, etc.  In Word document, a hyperlink may target to any one of the following sources.

* Web Page – represents the web content
* File – represents the file in some location
* Email – represents an Email
* Bookmark – represents the bookmarks in the document

Hyperlinks have two parts – the address and the display content. 

The following code example illustrates how to insert a web link.

{% tabs %}  

{% highlight c# %}

//Creates a new Word document 

WordDocument document = new WordDocument();

//Adds new section to the document

IWSection section = document.AddSection();

//Adds new paragraph to the section

IWParagraph paragraph = section.AddParagraph();

paragraph.AppendText("Web Hyperlink:  ");

paragraph = section.AddParagraph();

//Appends web hyperlink to the paragraph

IWField field = paragraph.AppendHyperlink("http://www.syncfusion.com", "Syncfusion", HyperlinkType.WebLink);

//Saves the Word document

document.Save("Sample.docx", FormatType.Docx);

//Closes the document

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates a new Word document 

Dim document As New WordDocument()

'Adds new section to the document

Dim section As IWSection = document.AddSection()

'Adds new paragraph to the section

Dim paragraph As IWParagraph = section.AddParagraph()

paragraph.AppendText("Web Hyperlink:  ")

paragraph = section.AddParagraph()

'Appends web hyperlink to the paragraph

Dim field As IWField = paragraph.AppendHyperlink("http://www.syncfusion.com", "Syncfusion", HyperlinkType.WebLink)

'Saves the Word document

document.Save("Sample.docx", FormatType.Docx)

'Closes the document

document.Close()

{% endhighlight %}

{% endtabs %}  
 
The following code example illustrates how to add an email link.

{% tabs %} 

{% highlight c# %}

//Creates a new Word document 

WordDocument document = new WordDocument();

//Adds new section to the document

IWSection section = document.AddSection();

//Adds new paragraph to the section

IWParagraph paragraph = section.AddParagraph();

paragraph.AppendText("Email hyperlink: ");

paragraph = section.AddParagraph();

//Appends Email hyperlink to the paragraph

paragraph.AppendHyperlink("mailto:john@gmail.com","John" , HyperlinkType.EMailLink);

//Saves the Word document

document.Save("Sample.docx", FormatType.Docx);

//Closes the document

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates a new Word document 

Dim document As New WordDocument()

'Adds new section to the document

Dim section As IWSection = document.AddSection()

'Adds new paragraph to the section

Dim paragraph As IWParagraph = section.AddParagraph()

paragraph.AppendText("Email hyperlink: ")

paragraph = section.AddParagraph()

'Appends Email hyperlink to the paragraph

paragraph.AppendHyperlink("mailto:john@gmail.com", "John", HyperlinkType.EMailLink)

'Saves the Word document

document.Save("Sample.docx", FormatType.Docx)

'Closes the document

document.Close()

{% endhighlight %} 

{% endtabs %}  

The following code example illustrates how to add a file hyperlink.

{% tabs %}  

{% highlight c# %}

//Creates a new Word document 

WordDocument document = new WordDocument();

//Adds new section to the document

IWSection section = document.AddSection();

//Adds new paragraph to the section

IWParagraph paragraph = section.AddParagraph();

paragraph.AppendText("File Hyperlinks: ");

paragraph = section.AddParagraph();

//Appends hyperlink field to the paragraph

paragraph.AppendHyperlink(@"Template.docx","File", HyperlinkType.FileLink);

//Saves the Word document

document.Save("Sample.docx", FormatType.Docx);

//Closes the document

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates a new Word document 

Dim document As New WordDocument()

'Adds new section to the document

Dim section As IWSection = document.AddSection()

'Adds new paragraph to the section

Dim paragraph As IWParagraph = section.AddParagraph()

paragraph.AppendText("File Hyperlinks: ")

paragraph = section.AddParagraph()

'Appends hyperlink field to the paragraph

paragraph.AppendHyperlink("Template.docx", "File", HyperlinkType.FileLink)

'Saves the Word document

document.Save("Sample.docx", FormatType.Docx)

'Closes the document

document.Close()

{% endhighlight %}

{% endtabs %}  
  
The following code example illustrates how to add a bookmark hyperlink.

{% tabs %}  

{% highlight c# %}

//Creates a new Word document 

WordDocument document = new WordDocument();

//Adds new section to the document

IWSection section = document.AddSection();

//Adds new paragraph to the section

IWParagraph paragraph = section.AddParagraph();

//Creates new Bookmark

paragraph.AppendBookmarkStart("Introduction");

paragraph.AppendText("Hyperlink");

paragraph.AppendBookmarkEnd("Introduction");

paragraph.AppendText("\nA hyperlink is a reference or navigation element in a document to another section of the same document or to another document that may be on or part of a (different) domain.");

paragraph = section.AddParagraph();

paragraph.AppendText("Bookmark Hyperlink: ");

paragraph = section.AddParagraph();

//Appends Bookmark hyperlink to the paragraph

paragraph.AppendHyperlink("Introduction", "Bookmark", HyperlinkType.Bookmark);

//Saves the Word document

document.Save("Sample.docx", FormatType.Docx);

//Closes the document

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates a new Word document 

Dim document As New WordDocument()

'Adds new section to the document

Dim section As IWSection = document.AddSection()

'Adds new paragraph to the section

Dim paragraph As IWParagraph = section.AddParagraph()

'Creates new Bookmark

paragraph.AppendBookmarkStart("Introduction")

paragraph.AppendText("Hyperlink")

paragraph.AppendBookmarkEnd("Introduction")

paragraph.AppendText(vbLf & "A hyperlink is a reference or navigation element in a document to another section of the same document or to another document that may be on or part of a (different) domain.")

paragraph = section.AddParagraph()

paragraph.AppendText("Bookmark Hyperlink: ")

paragraph = section.AddParagraph()

'Appends Bookmark hyperlink to the paragraph

paragraph.AppendHyperlink("Introduction", "Bookmark", HyperlinkType.Bookmark)

'Saves the Word document

document.Save("Sample.docx", FormatType.Docx)

'Closes the document

document.Close()

{% endhighlight %}

{% endtabs %}  

The display content for the Hyperlinks can also be an image that may redirect to some other contents.

The following code example illustrates how to add image hyperlink.

{% tabs %}  

{% highlight c# %}

//Creates a new Word document 

WordDocument document = new WordDocument();

//Adds new section to the document

IWSection section = document.AddSection();

//Adds new paragraph to the section

IWParagraph paragraph = section.AddParagraph();

paragraph.AppendText("Image Hyperlink");

paragraph = section.AddParagraph();

//Creates a new image instance and load image 

WPicture picture = new WPicture(document);

picture.LoadImage(Image.FromFile("Image.png"));

//Appends new image hyperlink to the paragraph

paragraph.AppendHyperlink("http://www.syncfusion.com", picture, HyperlinkType.WebLink);

//Saves the Word document

document.Save("Sample.docx", FormatType.Docx);

//Closes the document

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates a new Word document 

Dim document As New WordDocument()

'Adds new section to the document

Dim section As IWSection = document.AddSection()

'Adds new paragraph to the section

Dim paragraph As IWParagraph = section.AddParagraph()

paragraph.AppendText("Image Hyperlink")

paragraph = section.AddParagraph()

'Creates a new image instance and load image 

Dim picture As New WPicture(document)

picture.LoadImage(Image.FromFile("Image.png"))

'Appends new image hyperlink to the paragraph

paragraph.AppendHyperlink("http://www.syncfusion.com", picture, HyperlinkType.WebLink)

'Saves the Word document

document.Save("Sample.docx", FormatType.Docx)

'Closes the document

document.Close()

{% endhighlight %} 

{% endtabs %}  

The following code example illustrates how to modify the URL of an existing hyperlink.

{% tabs %}  

{% highlight c# %}

//Loads the template document 

WordDocument document = new WordDocument("Sample.docx", FormatType.Docx);

WParagraph paragraph = document.LastParagraph;

//Iterates through the paragraph items

foreach (ParagraphItem item in paragraph.ChildEntities)

{

if (item is WField)

{

if ((item as WField).FieldType == FieldType.FieldHyperlink)

{

//Gets the hyperlink field

Hyperlink link = new Hyperlink(item as WField);

if (link.Type == HyperlinkType.WebLink)

{

//Modifies the url of the hyperlink

link.Uri = "http://www.google.com";

link.TextToDisplay = "Google";

break;

}

}

}

}

//Saves and closes the Word document

document.Save("Sample.docx", FormatType.Docx);

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Loads the template document 

Dim document As New WordDocument("Sample.docx", FormatType.Docx)

Dim paragraph As WParagraph = document.LastParagraph

'Iterates through the paragraph items

For Each item As ParagraphItem In paragraph.ChildEntities

If TypeOf item Is WField Then

If TryCast(item, WField).FieldType = FieldType.FieldHyperlink Then

'Gets the hyperlink field

Dim link As New Hyperlink(TryCast(item, WField))

If link.Type = HyperlinkType.WebLink Then

'Modifies the url of the hyperlink

link.Uri = "http://www.google.com"

link.TextToDisplay = "Google"

Exit For

End If

End If

End If

Next

'Saves and closes the Word document

document.Save("Sample.docx", FormatType.Docx)

document.Close()

{% endhighlight %}

{% endtabs %}  
  
## Working with Symbols

Symbols are used to add contents such as currencies, numbers, punctuations, etc. DocIO represents symbols with `WSymbol` instance. Each symbol can be identified with their character codes.

The following code example illustrates how to add new symbol to the document:

{% tabs %}  

{% highlight c# %}

//Creates a new Word document 

WordDocument document = new WordDocument();

//Adds new section to the document

IWSection section = document.AddSection();

//Adds new paragraph to the section

IWParagraph paragraph = section.AddParagraph();

paragraph.AppendText("Example of adding symbols to the paragraph: ");

//Inserts symbol with character code 100

paragraph.AppendSymbol(100);

//Saves and closes the Word document

document.Save("Sample.docx", FormatType.Docx);

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates a new Word document 

Dim document As New WordDocument()

'Adds new section to the document

Dim section As IWSection = document.AddSection()

'Adds new paragraph to the section

Dim paragraph As IWParagraph = section.AddParagraph()

paragraph.AppendText("Example of adding symbols to the paragraph: ")

'Inserts symbol with character code 100

paragraph.AppendSymbol(100)

'Saves and closes the Word document

document.Save("Sample.docx", FormatType.Docx)

document.Close()

{% endhighlight %} 

 {% endtabs %}  

The following code example illustrates how to modify an existing symbol:

{% tabs %} 

{% highlight c# %}

//Loads the template document

WordDocument document = new WordDocument("Sample.docx", FormatType.Docx);

//Gets the textbody content

WTextBody textbody = document.Sections[0].Body;

//Iterates through the paragraphs

foreach (WParagraph paragraph in textbody.Paragraphs)

{

//Gets the symbol from the paragraph items

foreach (ParagraphItem item in paragraph.ChildEntities)

{

if (item is WSymbol)

{

WSymbol symbol = item as WSymbol;

if (symbol.CharacterCode == 100)

{

//Modifies the character code

symbol.CharacterCode = 40;

symbol.FontName = "Wingdings";

}

}

}

}

//Saves and closes the Word document

document.Save("Sample.docx", FormatType.Docx);

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Loads the template document

Dim document As New WordDocument("Sample.docx", FormatType.Docx)

'Gets the textbody content

Dim textbody As WTextBody = document.Sections(0).Body

'Iterates through the paragraphs

For Each paragraph As WParagraph In textbody.Paragraphs

'Gets the symbol from the paragraph items

For Each item As ParagraphItem In paragraph.ChildEntities

If TypeOf item Is WSymbol Then

Dim symbol As WSymbol = TryCast(item, WSymbol)

If symbol.CharacterCode = 100 Then

'Modifies the character code

symbol.CharacterCode = 40

symbol.FontName = "Wingdings"

End If

End If

Next

Next

'Saves and closes the Word document

document.Save("Sample.docx", FormatType.Docx)

document.Close()

{% endhighlight %} 

{% endtabs %}  

## Appending Breaks

Breaks allow the document contents to split into multiple parts, in order customize the appearance of the contents. The following are the types of breaks supported in the DocIO.

* Page break – starts the content in the next page
* Line break – starts the content in new line
* Column break – starts the content in the next column

The following code example illustrates how various types of breaks can be appended to the paragraphs:

{% tabs %}  

{% highlight c# %}

//Creates a new Word document 

WordDocument document = new WordDocument();

//Adds new section to the document

IWSection section = document.AddSection();

//Adds new paragraph to the section

IWParagraph paragraph = section.AddParagraph();

paragraph.AppendText("Before line break");

//Adds line break to the paragraph

paragraph.AppendBreak(BreakType.LineBreak);

paragraph.AppendText("After line break");

IWParagraph pageBreakPara = section.AddParagraph();

pageBreakPara.AppendText("Before page break");

//Adds page break to the paragraph

pageBreakPara.AppendBreak(BreakType.PageBreak);

pageBreakPara.AppendText("After page break");

IWSection secondSection = document.AddSection();

//Adds columns to the section

secondSection.AddColumn(100, 2);

secondSection.AddColumn(100, 2);

IWParagraph columnBreakPara = secondSection.AddParagraph();

columnBreakPara.AppendText("Before column break");

//Adds column break to the paragraph

columnBreakPara.AppendBreak(BreakType.ColumnBreak);

columnBreakPara.AppendText("After column break");

//Saves and closes the document instance

document.Save("Sample.docx", FormatType.Docx);

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates a new Word document 

Dim document As New WordDocument()

'Adds new section to the document

Dim section As IWSection = document.AddSection()

'Adds new paragraph to the section

Dim paragraph As IWParagraph = section.AddParagraph()

paragraph.AppendText("Before line break")

'Adds line break to the paragraph

paragraph.AppendBreak(BreakType.LineBreak)

paragraph.AppendText("After line break")

Dim pageBreakPara As IWParagraph = section.AddParagraph()

pageBreakPara.AppendText("Before page break")

'Adds page break to the paragraph

pageBreakPara.AppendBreak(BreakType.PageBreak)

pageBreakPara.AppendText("After page break")

Dim secondSection As IWSection = document.AddSection()

'Adds columns to the section

secondSection.AddColumn(100, 2)

secondSection.AddColumn(100, 2)

Dim columnBreakPara As IWParagraph = secondSection.AddParagraph()

columnBreakPara.AppendText("Before column break")

'Adds column break to the paragraph

columnBreakPara.AppendBreak(BreakType.ColumnBreak)

columnBreakPara.AppendText("After column break")

'Saves and closes the document instance

document.Save("Sample.docx", FormatType.Docx)

document.Close()

{% endhighlight %} 

{% endtabs %}  

## Appending OLE Objects

OLE (Object Linking and Embedding) Objects allow embedding and linking to documents and other objects. It allows the content of one program to be used in a Word document. The Objects can be inserted in the following two ways:

* Linked – the content is linked to the source file
* Embedded – the content is copied to the Word document and is not linked to the source file 

You can create and manipulate the OLE Objects of both Linked and Embedded types in the Word document by using `WOleObject` instance.

The following code example illustrates how to add OLE objects to the document.

{% tabs %}  

{% highlight c# %}

//Creates a new Word document 

WordDocument document = new WordDocument();

//Adds new section to the document

IWSection section = document.AddSection();

//Adds new paragraph to the section

IWParagraph paragraph = section.AddParagraph();

//Opens the file to be embedded

FileStream stream = new FileStream("Book1.xlsx", FileMode.Open);

//Loads the picture instance with the image need to be displayed

WPicture picture = new WPicture(document);

picture.LoadImage(Image.FromFile("Image.png"));

//Appends the Oleobject to the paragraph

WOleObject ole = paragraph.AppendOleObject(stream, picture, OleObjectType.ExcelWorksheet);

//Saves the Word document

document.Save("Sample.docx", FormatType.Docx);

//Closes the document

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates a new Word document 

Dim document As New WordDocument()

'Adds new section to the document

Dim section As IWSection = document.AddSection()

'Adds new paragraph to the section

Dim paragraph As IWParagraph = section.AddParagraph()

'Opens the file to be embedded

Dim stream As New FileStream("Book1.xlsx", FileMode.Open)

'Loads the picture instance with the image need to be displayed

Dim picture As New WPicture(document)

picture.LoadImage(Image.FromFile("Image.png"))

'Appends the Oleobject to the paragraph

Dim ole As WOleObject = paragraph.AppendOleObject(stream, picture, OleObjectType.ExcelWorksheet)

'Saves the Word document

document.Save("Sample.docx", FormatType.Docx)

'Closes the document

document.Close()

{% endhighlight %}

{% endtabs %}  
  
## Working with Shapes

Shapes are drawing objects that include lines, curves, circles, rectangles, etc. It can be preset or custom geometry. You can create and manipulate the pre-defined shape in DOCX and WordML format documents.

The following code example illustrates how to add pre-defined shape to the document.

{% tabs %} 

{% highlight c# %}

//Creates a new Word document 

WordDocument document = new WordDocument();

//Adds new section to the document

IWSection section = document.AddSection();

//Adds new paragraph to the section

WParagraph paragraph = section.AddParagraph() as WParagraph;

//Adds new shape to the document

Shape rectangle = paragraph.AppendShape(AutoShapeType.RoundedRectangle, 150, 100);

//Sets position for shape

rectangle.VerticalPosition = 72;

rectangle.HorizontalPosition = 72;

paragraph = section.AddParagraph() as WParagraph;

//Adds textbody contents to the shape

paragraph = rectangle.TextBody.AddParagraph() as WParagraph;

IWTextRange text = paragraph.AppendText("This text is in rounded rectangle shape");

text.CharacterFormat.TextColor = Color.Green;

text.CharacterFormat.Bold = true;

//Adds another shape to the document 

paragraph = section.AddParagraph()as WParagraph;

paragraph.AppendBreak(BreakType.LineBreak);

Shape pentagon = paragraph.AppendShape(AutoShapeType.Pentagon, 100, 100);

paragraph = pentagon.TextBody.AddParagraph()as WParagraph;

paragraph.AppendText("This text is in pentagon shape");

pentagon.HorizontalPosition = 72;

pentagon.VerticalPosition = 200;

//Saves the Word document

document.Save("Sample.docx", FormatType.Docx);

//Closes the document

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates a new Word document 

Dim document As New WordDocument()

'Adds new section to the document

Dim section As IWSection = document.AddSection()

'Adds new paragraph to the section

Dim paragraph As WParagraph = TryCast(section.AddParagraph(), WParagraph)

'Adds new shape to the document

Dim rectangle As Shape = paragraph.AppendShape(AutoShapeType.RoundedRectangle, 150, 100)

'Sets position for shape

rectangle.VerticalPosition = 72

rectangle.HorizontalPosition = 72

paragraph = TryCast(section.AddParagraph(), WParagraph)

'Adds textbody contents to the shape

paragraph = TryCast(rectangle.TextBody.AddParagraph(), WParagraph)

Dim text As IWTextRange = paragraph.AppendText("This text is in rounded rectangle shape")

text.CharacterFormat.TextColor = Color.Green

text.CharacterFormat.Bold = True

'Adds another shape to the document 

paragraph = TryCast(section.AddParagraph(), WParagraph)

paragraph.AppendBreak(BreakType.LineBreak)

Dim pentagon As Shape = paragraph.AppendShape(AutoShapeType.Pentagon, 100, 100)

paragraph = TryCast(pentagon.TextBody.AddParagraph(), WParagraph)

paragraph.AppendText("This text is in pentagon shape")

pentagon.HorizontalPosition = 72

pentagon.VerticalPosition = 200

'Saves the Word document

document.Save("Sample.docx", FormatType.Docx)

'Closes the document

document.Close()

{% endhighlight %}

{% endtabs %}  

Shape can have formatting such as line color, fill color, positioning, wrap formats, etc. The following code example illustrates how to apply formatting options for shape.

{% tabs %} 

{% highlight c# %}

//Creates a new Word document 

WordDocument document = new WordDocument();

//Adds new section to the document

IWSection section = document.AddSection();

//Adds new paragraph to the section

WParagraph paragraph = section.AddParagraph() as WParagraph;

Shape rectangle = paragraph.AppendShape(AutoShapeType.RoundedRectangle, 150, 100);

rectangle.VerticalPosition = 72;

rectangle.HorizontalPosition = 72;

paragraph = section.AddParagraph();

paragraph = rectangle.TextBody.AddParagraph();

IWTextRange text = paragraph.AppendText("This text is in rounded rectangle shape");

text.CharacterFormat.TextColor = Color.Green;

text.CharacterFormat.Bold = true;

//Applies fill color for shape

rectangle.FillFormat.Fill = true;

rectangle.FillFormat.Color = Color.LightGray;

//Applies wrap formats

rectangle.WrapFormat.TextWrappingStyle = TextWrappingStyle.Square;

rectangle.WrapFormat.TextWrappingType = TextWrappingType.Right;

//Sets horizontal and vertical origin

rectangle.HorizontalOrigin = HorizontalOrigin.Margin;

rectangle.VerticalOrigin = VerticalOrigin.Page;

//Sets line format

rectangle.LineFormat.DashStyle = LineDashing.Dot;

rectangle.LineFormat.Color = Color.DarkGray;

//Saves and closes the Word document

document.Save("Sample.docx", FormatType.Docx);

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates a new Word document 

Dim document As New WordDocument()

'Adds new section to the document

Dim section As IWSection = document.AddSection()

'Adds new paragraph to the section

Dim paragraph As WParagraph = TryCast(section.AddParagraph(), WParagraph)

Dim rectangle As Shape = paragraph.AppendShape(AutoShapeType.RoundedRectangle, 150, 100)

rectangle.VerticalPosition = 72

rectangle.HorizontalPosition = 72

paragraph = section.AddParagraph()

paragraph = rectangle.TextBody.AddParagraph()

Dim text As IWTextRange = paragraph.AppendText("This text is in rounded rectangle shape")

text.CharacterFormat.TextColor = Color.Green

text.CharacterFormat.Bold = True

'Applies fill color for shape

rectangle.FillFormat.Fill = True

rectangle.FillFormat.Color = Color.LightGray

'Applies wrap formats

rectangle.WrapFormat.TextWrappingStyle = TextWrappingStyle.Square

rectangle.WrapFormat.TextWrappingType = TextWrappingType.Right

'Sets horizontal and vertical origin

rectangle.HorizontalOrigin = HorizontalOrigin.Margin

rectangle.VerticalOrigin = VerticalOrigin.Page

'Sets line format

rectangle.LineFormat.DashStyle = LineDashing.Dot

rectangle.LineFormat.Color = Color.DarkGray

'Saves and closes the Word document

document.Save("Sample.docx", FormatType.Docx)

document.Close()

{% endhighlight %}

{% endtabs %}  

## Working with Text Box

Text box contains a group of textual and graphical contents. DocIO supports to create and manipulate the text box and its formatting by using `WTextBox` instance.

The following code example illustrates how to add new text box to the paragraph.

{% tabs %}  

{% highlight c# %}

//Creates a new Word document 

WordDocument document = new WordDocument();

//Adds new section to the document

IWSection section = document.AddSection();

//Adds new paragraph to the section

IWParagraph paragraph = section.AddParagraph();

//Appends new textbox to the paragraph

IWTextBox textbox = paragraph.AppendTextBox(150, 75);

//Adds new text to the textbox body

IWParagraph textboxParagraph = textbox.TextBoxBody.AddParagraph();

textboxParagraph.AppendText("Text inside text box");

textboxParagraph = textbox.TextBoxBody.AddParagraph();

//Adds new picture to textbox body

IWPicture picture = textboxParagraph.AppendPicture(Image.FromFile(@"Image.png"));

picture.Height = 75;

picture.Width = 50;

//Saves and closes the Word document

document.Save("Sample.docx", FormatType.Docx);

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates a new Word document 

Dim document As New WordDocument()

'Adds new section to the document

Dim section As IWSection = document.AddSection()

'Adds new paragraph to the section

Dim paragraph As IWParagraph = section.AddParagraph()

'Appends new textbox to the paragraph

Dim textbox As IWTextBox = paragraph.AppendTextBox(150, 75)

'Adds new text to the textbox body

Dim textboxParagraph As IWParagraph = textbox.TextBoxBody.AddParagraph()

textboxParagraph.AppendText("Text inside text box")

textboxParagraph = textbox.TextBoxBody.AddParagraph()

'Adds new picture to textbox body

Dim picture As IWPicture = textboxParagraph.AppendPicture(Image.FromFile("Image.png"))

picture.Height = 75

picture.Width = 50

'Saves and closes the Word document

document.Save("Sample.docx", FormatType.Docx)

document.Close()

{% endhighlight %} 

{% endtabs %}  

Textbox has its own formatting such as outline color, fill effects, text direction, wrap formats, etc. The following code example illustrates how to apply formatting for textbox.

{% tabs %}  

{% highlight c# %}

//Creates a new Word document 

WordDocument document = new WordDocument();

//Adds new section to the document

IWSection section = document.AddSection();

//Adds new paragraph to the section

IWParagraph paragraph = section.AddParagraph();

//Appends new textbox to the paragraph

IWTextBox textbox = paragraph.AppendTextBox(150, 75);

//Adds new text to the textbox body

IWParagraph textboxParagraph = textbox.TextBoxBody.AddParagraph();

textboxParagraph.AppendText("Text inside text box");

//Sets fillcolor and line width for textbox

textbox.TextBoxFormat.FillColor = Color.LightGreen;

textbox.TextBoxFormat.LineWidth = 2;

//Applies textbox text direction

textbox.TextBoxFormat.TextDirection = Syncfusion.DocIO.DLS.TextDirection.VerticalTopToBottom;

//Sets text wrapping style

textbox.TextBoxFormat.TextWrappingStyle = TextWrappingStyle.InFrontOfText;

//Sets horizontal and vertical position

textbox.TextBoxFormat.HorizontalPosition = 200;

textbox.TextBoxFormat.VerticalPosition = 200; 

//Sets horizontal and vertical origin

textbox.TextBoxFormat.VerticalOrigin = VerticalOrigin.Margin;

textbox.TextBoxFormat.HorizontalOrigin = HorizontalOrigin.Page;

//Sets top and bottom margin values

textbox.TextBoxFormat.InternalMargin.Bottom = 5f;

textbox.TextBoxFormat.InternalMargin.Top = 5f;

//Saves and closes the Word document

document.Save("Sample.docx", FormatType.Docx);

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates a new Word document 

Dim document As New WordDocument()

'Adds new section to the document

Dim section As IWSection = document.AddSection()

'Adds new paragraph to the section

Dim paragraph As IWParagraph = section.AddParagraph()

'Appends new textbox to the paragraph

Dim textbox As IWTextBox = paragraph.AppendTextBox(150, 75)

'Adds new text to the textbox body

Dim textboxParagraph As IWParagraph = textbox.TextBoxBody.AddParagraph()

textboxParagraph.AppendText("Text inside text box")

'Sets fillcolor and line width for textbox

textbox.TextBoxFormat.FillColor = Color.LightGreen

textbox.TextBoxFormat.LineWidth = 2

'Applies textbox text direction

textbox.TextBoxFormat.TextDirection = Syncfusion.DocIO.DLS.TextDirection.VerticalTopToBottom

'Sets text wrapping style

textbox.TextBoxFormat.TextWrappingStyle = TextWrappingStyle.InFrontOfText

'Sets horizontal and vertical position

textbox.TextBoxFormat.HorizontalPosition = 200

textbox.TextBoxFormat.VerticalPosition = 200

'Sets horizontal and vertical origin

textbox.TextBoxFormat.VerticalOrigin = VerticalOrigin.Margin

textbox.TextBoxFormat.HorizontalOrigin = HorizontalOrigin.Page

'Sets top and bottom margin values

textbox.TextBoxFormat.InternalMargin.Bottom = 5.0F

textbox.TextBoxFormat.InternalMargin.Top = 5.0F

'Saves and closes the Word document

document.Save("Sample.docx", FormatType.Docx)

document.Close()

{% endhighlight %}

{% endtabs %}  