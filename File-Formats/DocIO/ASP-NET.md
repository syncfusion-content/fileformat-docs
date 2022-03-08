---
title: Working with Asp.net 
description: Create a Asp.net and save the document
platform: file-formats
control: DocIO
documentation: UG
---

# Working with ASP.NET

In your ASP.NET application, please add the required assemblies in order to use DocIO. [Refer here for assemblies required](/File-Formats/DocIO/Assemblies-Required).

## Save the document 

The following code example illustrates how to download the Word document in browser after saving the document.
{% tabs %}
{% highlight c# tabtitle="C#" %}

//Creates an empty Word document instance

WordDocument document = new WordDocument();

//Adds new section to the document

IWSection section = document.AddSection();

//Adds new paragraph to the section

IWParagraph paragraph = section.AddParagraph();

//Appends the text to the created paragraph

paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");

//Save the document

document.Save("Sample.docx", FormatType.Docx, HttpContext.Current.Response, HttpContentDisposition.Attachment);

//close the document

document.Close();

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Creates an empty Word document instance

Dim document As New WordDocument()

'Adds new section to the document

Dim section As IWSection = document.AddSection()

'Adds new paragraph to the section

Dim paragraph As IWParagraph = section.AddParagraph()

'Appends the text to the created paragraph

paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.")

'Save the document

document.Save("Sample.docx", FormatType.Docx, HttpContext.Current.Response, HttpContentDisposition.Attachment)

'close the document

document.Close()

{% endhighlight %}

{% endtabs %}

The following code example illustrates how to open the HTML file in web browser after saving the Word document as HTML file using DocIO.

{% tabs %}

{% highlight c# tabtitle="C#" %}

//Creates an empty Word document instance

WordDocument document = new WordDocument();

//Adds new section to the document

IWSection section = document.AddSection();

//Adds new paragraph to the section

IWParagraph paragraph = section.AddParagraph();

//Appends the text to the created paragraph

paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");

//Save the document

document.Save("Sample.html", FormatType.Html, HttpContext.Current.Response, HttpContentDisposition.InBrowser);

//Close the document

document.Close();

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}

'Creates an empty Word document instance

Dim document As New WordDocument()

'Adds new section to the document

Dim section As IWSection = document.AddSection()

'Adds new paragraph to the section

Dim paragraph As IWParagraph = section.AddParagraph()

'Appends the text to the created paragraph

paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.")

'Save the document

document.Save("Sample.html", FormatType.Html, HttpContext.Current.Response, HttpContentDisposition.InBrowser)

'Close the document

document.Close()

{% endhighlight %}

{% endtabs %}
