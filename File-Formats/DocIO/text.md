---
title: Convert Word to Text document and vice versa in C# |Syncfusion
description: Learn how to convert Word document to text file and vice versa  using the .NET Word (DocIO) library without Microsoft Word or interop dependencies.
platform: file-formats
control: DocIO
documentation: UG
---

# Text Conversions in Word Library

The Essential DocIO converts the Word document into Text file and vice versa. The following code example shows how to convert the Word document into text file.

{% tabs %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Loads a template document
WordDocument document = new WordDocument("Template.docx");
//Saves the document as text file
document.Save("WordToText.txt", FormatType.Txt);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET (.NET Windows-specific)" %}
'Loads a text file
Dim document As New WordDocument("Template.docx")
'Saves the document as text file
document.Save("WordToText.txt", FormatType.Txt)
'Closes the document
document.Close()
{% endhighlight %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
FileStream fileStreamPath = new FileStream("Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx))
{
    //Saves the Word document to  MemoryStream
    MemoryStream stream = new MemoryStream();
    document.Save(stream, FormatType.Txt);
    //Closes the Word document
    document.Close();
}
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Text-file-conversion/Convert-Word-to-text-file).

The following code example shows how to convert a Text file into Word document.

{% tabs %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Loads a text file
WordDocument document = new WordDocument("Template.txt");
//Saves the document as text file
document.Save("TextToWord.docx", FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET (.NET Windows-specific)" %}
'Loads a text file
Dim document As New WordDocument("Template.txt")
'Saves the document as text file
document.Save("TextToWord.docx", FormatType.Docx)
'Closes the document
document.Close()
{% endhighlight %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
FileStream fileStreamPath = new FileStream("Template.txt", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument(fileStreamPath, FormatType.Txt))
{
    //Saves the Word document to MemoryStream
    MemoryStream stream = new MemoryStream();
    document.Save(stream, FormatType.Docx);
    //Closes the Word document
    document.Close();
}
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Text-file-conversion/Convert-text-file-to-Word).

The following code example shows how to retrieve the Word document contents as a plain text.

{% tabs %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET (.NET Windows-specific)" %}
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

{% highlight c# tabtitle="C# [Cross-platform]" %}
FileStream fileStreamPath = new FileStream("Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx))
{
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
    //Saves the Word document to MemoryStream
    MemoryStream stream = new MemoryStream();
    newdocument.Save(stream, FormatType.Docx);
    //Closes the Word document
    document.Close();
    newdocument.Close();
}
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Text-file-conversion/Retrieve-Word-document-as-plain-text).
