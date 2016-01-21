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
{% highlight c# %}

//Creates an empty Word document instance

WordDocument document = new WordDocument();

//Adds new section to the document

IWSection section = document.AddSection();

//Adds new paragraph to the section

IWParagraph paragraph = section.AddParagraph();

//Appends the text to the created paragraph

paragraph.AppendText("Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula");

//Save the document

document.Save("Sample.docx", FormatType.Docx, HttpContext.Current.Response, HttpContentDisposition.Attachment);

//close the document

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates an empty Word document instance

Dim document As New WordDocument()

'Adds new section to the document

Dim section As IWSection = document.AddSection()

'Adds new paragraph to the section

Dim paragraph As IWParagraph = section.AddParagraph()

'Appends the text to the created paragraph

paragraph.AppendText("Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula")

'Save the document

document.Save("Sample.docx", FormatType.Docx, HttpContext.Current.Response, HttpContentDisposition.Attachment)

'close the document

document.Close()

{% endhighlight %}

{% endtabs %}

The following code example illustrates how to open the HTML file in web browser after saving the Word document as HTML file using DocIO.

{% tabs %}

{% highlight c# %}

//Creates an empty Word document instance

WordDocument document = new WordDocument();

//Adds new section to the document

IWSection section = document.AddSection();

//Adds new paragraph to the section

IWParagraph paragraph = section.AddParagraph();

//Appends the text to the created paragraph

paragraph.AppendText("Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula");

//Save the document

document.Save("Sample.html", FormatType.Html, HttpContext.Current.Response, HttpContentDisposition.InBrowser);

//Close the document

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates an empty Word document instance

Dim document As New WordDocument()

'Adds new section to the document

Dim section As IWSection = document.AddSection()

'Adds new paragraph to the section

Dim paragraph As IWParagraph = section.AddParagraph()

'Appends the text to the created paragraph

paragraph.AppendText("Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula")

'Save the document

document.Save("Sample.html", FormatType.Html, HttpContext.Current.Response, HttpContentDisposition.InBrowser)

'Close the document

document.Close()

{% endhighlight %}

{% endtabs %}
