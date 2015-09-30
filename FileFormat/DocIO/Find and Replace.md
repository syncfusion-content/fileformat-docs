---
layout: Post
title: Find and Replace
description: This section illustrates finding a text and replacing it with a new text
platform: FileFormat
control: DocIO
documentation: UG
---
# Find and Replace

You can search a particular text you like to change and replace it with another text or part of the document.

## Finding contents in a Word document

You can find the first occurrence of a particular text within a single paragraph in the document using **Find** method and its next occurrence using **FindNext** method. You can also find a particular text pattern in the document.

The following code snippet illustrates how to find a particular text and its next occurrence in the document.

{% highlight c# %}
[C#]

//Load the template document

WordDocument document = new WordDocument("Template.docx", FormatType.Docx);

//Find the first occurrence of a particular text in the document

TextSelection textSelection = document.Find("as graphical contents", false, true);

//Get the found text as single text range

WTextRange textRange = textSelection.GetAsOneRange();

//Modify the text

textRange.Text = "Replaced text";

//Set highlight color

textRange.CharacterFormat.HighlightColor = Color.Yellow;

//Find the next occurrence of a particular text from the previous paragraph

textSelection = document.FindNext(textRange.OwnerParagraph, "paragraph", true, false);

//Get the found text as single text range

WTextRange range = textSelection.GetAsOneRange();

//Set bold formatting

range.CharacterFormat.Bold = true;

//Save and close the document

document.Save("Sample.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB]

'Load the template document

Dim document As New WordDocument("Template.docx", FormatType.Docx)

'Find the first occurrence of a particular text in the document

Dim textSelection As TextSelection = document.Find("as graphical contents", False, True)

'Get the found text as single text range

Dim textRange As WTextRange = textSelection.GetAsOneRange()

'Modify the text

textRange.Text = "Replaced text"

'Set highlight color

textRange.CharacterFormat.HighlightColor = Color.Yellow

'Find the next occurrence of a particular text from the previous paragraph

textSelection = document.FindNext(textRange.OwnerParagraph, "paragraph", True, False)

'Get the found text as single text range

Dim range As WTextRange = textSelection.GetAsOneRange()

'Set bold formatting

range.CharacterFormat.Bold = True

'Save and close the document

document.Save("Sample.docx", FormatType.Docx)

document.Close()





{% endhighlight %}

You can find all the occurrence of a particular text within a single paragraph in the document using **FindAll** method. 

The following code snippet illustrates how to find all the occurrences of a particular text in the document.

{% highlight c# %}
[C#]

//Load the template document

WordDocument document = new WordDocument("Template.docx", FormatType.Docx);

//Find all the occurrences of a particular text

TextSelection[] textSelections = document.FindAll("paragraph", false, true);

foreach (TextSelection textSelection in textSelections)

{

//Get the found text as single text range and set highlight color

WTextRange textRange = textSelection.GetAsOneRange();

textRange.CharacterFormat.HighlightColor = Color.YellowGreen;

}

//Save and close the document

document.Save("Sample.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB]

'Load the template document

Dim document As New WordDocument("Template.docx", FormatType.Docx)

'Find all the occurrences of a particular text

Dim textSelections As TextSelection() = document.FindAll("paragraph", False, True)

For Each textSelection As TextSelection In textSelections

'Get the found text as single text range and set highlight color

Dim textRange As WTextRange = textSelection.GetAsOneRange()

textRange.CharacterFormat.HighlightColor = Color.YellowGreen

Next

'Save and close the document

document.Save("Sample.docx", FormatType.Docx)

document.Close()





{% endhighlight %}

You can find the first occurrence of a particular text extended to several paragraphs in the document using **FindSingleLine** method and its next occurrence using **FindNextSingleLine** method.

The following code snippet illustrates how to find a particular text extended to several paragraphs in the Word document.

{% highlight c# %}
[C#]

//Load the template document

WordDocument document = new WordDocument("Template.docx", FormatType.Docx);

//Find the first occurrence of a particular text extended to several paragraphs in the document

TextSelection[] textSelections = document.FindSingleLine("First paragraph Second paragraph", true, false);

WParagraph paragraph = null;

foreach (TextSelection textSelection in textSelections)

{

//Get the found text as single text range and set highlight color

WTextRange textRange = textSelection.GetAsOneRange();

textRange.CharacterFormat.HighlightColor = Color.YellowGreen;

paragraph = textRange.OwnerParagraph;

}

//Find the next occurrence of a particular text extended to several paragraphs in the document

textSelections = document.FindNextSingleLine(paragraph, "First paragraph Second paragraph", true, false);

foreach (TextSelection textSelection in textSelections)

{

//Get the found text as single text range and set italic formatting

WTextRange text = textSelection.GetAsOneRange();

text.CharacterFormat.Italic = true;

}

//Save and close the document

document.Save("Sample.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB]

'Load the template document

Dim document As New WordDocument("Template.docx", FormatType.Docx)

'Find the first occurrence of a particular text extended to several paragraphs in the document

Dim textSelections As TextSelection() = document.FindSingleLine("First paragraph Second paragraph", True, False)

Dim paragraph As WParagraph = Nothing

For Each textSelection As TextSelection In textSelections

'Get the found text as single text range and set highlight color

Dim textRange As WTextRange = textSelection.GetAsOneRange()

textRange.CharacterFormat.HighlightColor = Color.YellowGreen

paragraph = textRange.OwnerParagraph

Next

'Find the next occurrence of a particular text extended to several paragraphs in the document

textSelections = document.FindNextSingleLine(paragraph, "First paragraph Second paragraph", True, False)

For Each textSelection As TextSelection In textSelections

'Get the found text as single text range and set italic formatting

Dim text As WTextRange = textSelection.GetAsOneRange()

text.CharacterFormat.Italic = True

Next

'Save and close the document

document.Save("Sample.docx", FormatType.Docx)

document.Close()





{% endhighlight %}

## Replacing the Search results

You can replace a particular text with another text, part of a document or entire document using **Replace** method. 

The following code snippet illustrates how to replace a particular text.

{% highlight c# %}
[C#]

//Load a template document

WordDocument document = new WordDocument("Template.docx", FormatType.Docx);

//Find the first occurrence of a particular text in the document

TextSelection selection = document.Find("contents", false, false);

//Initialize text body part

TextBodyPart bodyPart = new TextBodyPart(selection);

//Replace a particular text with the text body part

document.Replace("paragraph", bodyPart, false, true, true);

//Save and close the document

document.Save("Replace.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB]

'Load a template document

Dim document As New WordDocument("Template.docx", FormatType.Docx)

'Find the first occurrence of a particular text in the document

Dim selection As TextSelection = document.Find("contents", False, False)

'Initialize text body part

Dim bodyPart As New TextBodyPart(selection)

'Replace a particular text with the text body part

document.Replace("paragraph", bodyPart, False, True, True)

'Save and close the document

document.Save("Replace.docx", FormatType.Docx)

document.Close()





{% endhighlight %}

You can specify to replace only the first occurrence of the specified text by setting **ReplaceFirst** property of **WordDocument** class to true. 

The following code snippet illustrates how to replace the first occurrence of a particular text.

{% highlight c# %}
[C#]

//Load a template document

WordDocument document = new WordDocument("Template.docx", FormatType.Docx);

//Set to replace only the first occurrence of a particular text

document.ReplaceFirst = true;

//Find the first occurrence of a particular text in the document

TextSelection selection = document.Find("contents", false, false);

//Initialize text body part

TextBodyPart bodyPart = new TextBodyPart(selection);

//Replace a particular text with the text body part

document.Replace("paragraph", bodyPart, false, true, true);

//Save and close the document

document.Save("Replace.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB]

'Load a template document

Dim document As New WordDocument("Template.docx", FormatType.Docx)

'Set to replace only the first occurrence of a particular text

document.ReplaceFirst = True

'Find the first occurrence of a particular text in the document

Dim selection As TextSelection = document.Find("contents", False, False)

'Initialize text body part

Dim bodyPart As New TextBodyPart(selection)

'Replace a particular text with the text body part

document.Replace("paragraph", bodyPart, False, True, True)

'Save and close the document

document.Save("Replace.docx", FormatType.Docx)

document.Close()





{% endhighlight %}

The following code snippet illustrates how to replace a particular text with a Word document.

{% highlight c# %}
[C#]

//Load a template document

WordDocument document = new WordDocument("SourceTemplate.docx", FormatType.Docx);

//Get the document to replace the text

IWordDocument replaceDocument = new WordDocument("Template.docx");

//Replace a particular text with another document

document.Replace("paragraph", replaceDocument, false, true, true);

//Save and close the document

document.Save("Sample.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB]

'Load a template document

Dim document As New WordDocument("SourceTemplate.docx", FormatType.Docx)

'Get the document to replace the text

Dim replaceDocument As IWordDocument = New WordDocument("Template.docx")

'Replace a particular text with another document

document.Replace("paragraph", replaceDocument, False, True, True)

'Save and close the document

document.Save("Sample.docx", FormatType.Docx)

document.Close()





{% endhighlight %}

You can replace a particular text extended to several paragraphs in a document with another text or part of a document using **ReplaceSingleLine** method.

The following code snippet illustrates how to replace the text extended to several paragraphs with simple text.

{% highlight c# %}
[C#]

//Load a template document

WordDocument document = new WordDocument("Template.docx", FormatType.Docx);

//Replace the text extended to two paragraphs with simple text

document.ReplaceSingleLine("First paragraph Second paragraph", "Replaced paragraph", true, false);

//Save and close the document

document.Save("Replace.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB]

'Load a template document

Dim document As New WordDocument("Template.docx", FormatType.Docx)

'Replace the text extended to two paragraphs with simple text

document.ReplaceSingleLine("First paragraph Second paragraph", "Replaced paragraph", True, False)

'Save and close the document

document.Save("Replace.docx", FormatType.Docx)

document.Close()





{% endhighlight %}

