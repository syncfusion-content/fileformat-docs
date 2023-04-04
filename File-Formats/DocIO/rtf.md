---
title: RTF conversions in C# | DocIO | Syncfusion
description: Learn how to convert Word document to RTF and vice versa using the .NET Word (DocIO) library without Microsoft Word or interop dependencies.
platform: file-formats
control: DocIO
documentation: UG
---

# RTF Conversions in Word Library

## RTF
The [Rich Text Format (RTF)](http://en.wikipedia.org/wiki/Rich_Text_Format#) is one of the document formats supported by Microsoft Word and many other Word processing applications. RTF is human readable file format invented for interchanging formatted text between applications. It is an optional format for Word that retains most formatting and all content of the original document.

Most of the Word processors (including Microsoft Word) uses the XML-based file formats, Microsoft has discontinued enhancements to the RTF and still supporting it. The last version was 1.9.1 released in 2008.

The Essential DocIO converts the RTF document into Word document and vice versa. The following code shows how to convert RTF document into Word document.

{% tabs %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Loads an existing document
WordDocument document = new WordDocument("Input.rtf", FormatType.Rtf);
//Saves the Word document as RTF file
document.Save("RtfToWord.docx", FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET (.NET Windows-specific)" %}
'Loads an existing document
Dim document As New WordDocument("Input.rtf", FormatType.Rtf)
'Saves the Word document as RTF file
document.Save("RtfToWord.docx", FormatType.Docx)
'Closes the document
document.Close()
{% endhighlight %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
FileStream fileStreamPath = new FileStream("Input.rtf", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument(fileStreamPath, FormatType.Rtf))
{
    //Saves the Word document to MemoryStream
    MemoryStream stream = new MemoryStream();
    document.Save(stream, FormatType.Docx);
    //Closes the Word document
    document.Close();
}
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/RTF-conversions/Convert-RTF-to-Word).

The following code example shows how to convert Word document into RTF document.

{% tabs %}
{% highlight c# tabtitle="C# [Windows-specific]" %}
//Loads an existing document
WordDocument document = new WordDocument("Template.docx", FormatType.Docx);
//Saves the Word document as RTF file
document.Save("WordToRtf.rtf", FormatType.Rtf);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET (.NET Windows-specific)" %}
'Loads an existing document
Dim document As New WordDocument("Template.docx", FormatType.Docx)
'Saves the Word document as RTF file
document.Save("WordToRtf.rtf", FormatType.Rtf)
'Closes the document
document.Close()
{% endhighlight %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
FileStream fileStreamPath = new FileStream("Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx))
{
    //Saves the Word document to MemoryStream
    MemoryStream stream = new MemoryStream();
    document.Save(stream, FormatType.Rtf);
    //Closes the Word document
    document.Close();
}
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/RTF-conversions/Convert-Word-to-RTF).

## Supported and Unsupported features
The supported and unsupported features of DocIO based on file formats can be referred [here](https://help.syncfusion.com/file-formats/docio/supported-and-unsupported-features#)