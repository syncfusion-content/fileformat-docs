---
title: RTF conversions
description: Word to RTF conversions using DocIO
platform: file-formats
control: DocIO
documentation: UG
---

# RTF Conversions

## RTF
The [Rich Text Format (RTF)](http://en.wikipedia.org/wiki/Rich_Text_Format#) is one of the document formats supported by Microsoft Word and many other word processing applications. RTF is human readable file format invented for interchanging formatted text between applications, is an optional format for Word that retains most formatting and all content of the original document.

Now, most of the word processor's (including Microsoft Word) uses the XML-based file format Microsoft has discontinued enhancements to the RTF and still supporting it. The last version was 1.9.1 released in 2008.

Essential DocIO supports to convert the RTF document into Word document and vice versa. The following code shows how to convert RTF document into Word document.

{% tabs %}
{% highlight c# %}
//Loads an existing document

WordDocument document = new WordDocument("Sample.rtf", FormatType.Rtf);

//Saves the Word document as RTF file

document.Save("RtfToWord.docx", FormatType.Docx);

//Closes the document

document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Loads an existing document

Dim document As New WordDocument("Sample.rtf", FormatType.Rtf)

'Saves the Word document as RTF file

document.Save("RtfToWord.docx", FormatType.Docx)

'Closes the document

document.Close()
{% endhighlight %}
{% endtabs %}

The following code example shows how to convert Word document into RTF document.

{% tabs %}
{% highlight c# %}
//Loads an existing document

WordDocument document = new WordDocument("Template.docx", FormatType.Docx);

//Saves the Word document as RTF file

document.Save("WordToRtf.rtf", FormatType.Rtf);

//Closes the document

document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Loads an existing document

Dim document As New WordDocument("Template.docx", FormatType.Docx)

'Saves the Word document as RTF file

document.Save("WordToRtf.rtf", FormatType.Rtf)

'Closes the document

document.Close()
{% endhighlight %}
{% endtabs %}

## Supported and Unsupported features
The supported and unsupported features of DocIO based on file formats can be referred from [here](https://help.syncfusion.com/file-formats/docio/supported-and-unsupported-features#)
