---
layout: post
title: Accepting or Rejecting Track Changes
description: This section illustrates how to Accept or Reject the Track changes of the Word document
platform: FileFormat
control: DocIO
documentation: UG
---
# Accepting or Rejecting Track Changes

It is used to keep track of the changes made to a Word document. It helps to maintain the record of author, name and time for every insertion, deletion, or modification in a document. This can be enabled by using the TrackChanges property of the Word document.

I> Note: With this support, the changes made in the Word document by DocIO library cannot be tracked.

The following code example illustrates how to enable track changes of the document.

{% highlight c# %}
[C#]

//Creates a new Word document 

WordDocument document = new WordDocument();

//Adds new section to the document

IWSection section = document.AddSection();

//Adds new paragraph to the section

IWParagraph paragraph = section.AddParagraph();

//Appends text to the paragraph

IWTextRange text = paragraph.AppendText("This sample illustrates how to track the changes made to the word document. ");

//Sets font name and size for text

text.CharacterFormat.FontName = "Times New Roman";

text.CharacterFormat.FontSize = 14;

text = paragraph.AppendText("This track changes is useful in shared environment.");

text.CharacterFormat.FontSize = 12;

//Turns on the track changes option

document.TrackChanges = true;

//Saves and closes the document

document.Save("Sample.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB]

'Creates a new Word document 

Dim document As New WordDocument()

'Adds new section to the document

Dim section As IWSection = document.AddSection()

'Adds new paragraph to the section

Dim paragraph As IWParagraph = section.AddParagraph()

'Appends text to the paragraph

Dim text As IWTextRange = paragraph.AppendText("This sample illustrates how to track the changes made to the word document. ")

'Sets font name and size for text

text.CharacterFormat.FontName = "Times New Roman"

text.CharacterFormat.FontSize = 14

text = paragraph.AppendText("This track changes is useful in shared environment.")

text.CharacterFormat.FontSize = 12

'Turns on the track changes option

document.TrackChanges = True

'Saves and closes the document

document.Save("Sample.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

The changes made to the document can be accepted or rejected. The following code example illustrates how to accept or reject the changes made to the document. 

{% highlight c# %}
[C#]

//Loads the template document

WordDocument document = new WordDocument("TrackChanges.docx", FormatType.Docx);

//Accepts track changes of the document

if (document.HasChanges)

document.AcceptChanges();

//Saves and closes the document

document.Save("TrackChanges_Sample.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB]

'Loads the template document

Dim document As New WordDocument("TrackChanges.docx", FormatType.Docx)

'Accepts track changes of the document

If document.HasChanges Then

document.AcceptChanges()

End If

'Saves and closes the document

document.Save("TrackChanges_Sample.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

