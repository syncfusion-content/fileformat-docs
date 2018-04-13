---
title: Word document to Text Conversion
description: Converting Word document to Text using DocIO
platform: file-formats
control: DocIO
documentation: UG
---

# Text Conversion.

The Essential DocIO converts the Word document into Text file and vice versa. The following code example shows how to convert the Word document into text file.

{% tabs %}
{% highlight c# %}
//Loads a template document

WordDocument document = new WordDocument("Template.docx");

//Saves the document as text file

document.Save("WordToText.txt", FormatType.Txt);

//Closes the document

document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Loads a text file

Dim document As New WordDocument("Template.docx")

'Saves the document as text file

document.Save("WordToText.txt", FormatType.Txt)

'Closes the document

document.Close()
{% endhighlight %}
{% endtabs %}

The following code example shows how to convert a Text file into Word document.

{% tabs %}
{% highlight c# %}
//Loads a text file

WordDocument document = new WordDocument("Template.txt");

//Saves the document as text file

document.Save("TextToWord.docx", FormatType.Docx);

//Closes the document

document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Loads a text file

Dim document As New WordDocument("Template.txt")

'Saves the document as text file

document.Save("TextToWord.docx", FormatType.Docx)

'Closes the document

document.Close()
{% endhighlight %}
{% endtabs %}

The following code example shows how to retrieve the Word document contents as a plain text.

{% tabs %}
{% highlight c# %}
//Loads a template document

WordDocument document = new WordDocument("Template.docx");

//Gets the document text

string text = document.GetText();

//Creates new Word document

WordDocument newdocument = new WordDocument();

//Adds new section

IWSection section = newdocument.AddSection();

//Adds new paragraph

IWParagraph paragraph = section.AddParagraph();

//Appends the text to the paragraph

paragraph.AppendText(text);

//Saves and closes the document

newdocument.Save("Sample.docx");

newdocument.Close();

document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Loads a template document

Dim document As New WordDocument("Template.docx")

'Gets the document text

Dim text As String = document.GetText()

'Creates new Word document

Dim newdocument As New WordDocument()

'Adds new section

Dim section As IWSection = newdocument.AddSection()

'Adds new paragraph

Dim paragraph As IWParagraph = section.AddParagraph()

'Appends the text to the paragraph

paragraph.AppendText(text)

'Saves and closes the document

newdocument.Save("Sample.docx")

newdocument.Close()

document.Close()
{% endhighlight %}
{% endtabs %}
