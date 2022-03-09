---
title: Working with Table Of Contents | Syncfusion
description: This section illustrates how to insert and update the Table Of Content in a Word document without Microsoft Word or Office interop
platform: file-formats
control: DocIO
documentation: UG
---
# Working with Table Of Contents

[Table of contents](https://support.office.com/en-in/article/Create-a-table-of-contents-or-update-a-table-of-contents-eb275189-b93e-4559-8dd9-c279457bfd72#__create_a_table ) (TOC) is used to provide an outline of the Word document. By default table of contents will be created automatically from heading styles. 

You can add the TOC into the paragraph by specifying the `LowerHeadingLevel` and `UpperHeadingLevel`. The heading level range must be from 1 to 9.

Basically TOC determines the TOC entries based on the TOC switches. 

<table>
<thead>  
<tr>
<th> S.No <br/><br/></th>
<th>Switches<br/><br/></th>
<th>Description<br/><br/></th>
</tr>
</thead>
<tbody>  
<tr>
<td>
1<br/><br/></td><td>
\o<br/><br/></td><td>
Builds a table of contents from paragraphs formatted with built-in heading styles.<br/><br/></td></tr>
<tr>
<td>
2<br/><br/></td><td>
\h<br/><br/></td><td>
Inserts TOC entries as hyperlinks.<br/><br/></td></tr>
<tr>
<td>
3<br/><br/></td><td>
\n<br/><br/></td><td>
Omits page numbers from the table of contents. <br/><br/></td></tr>
<tr>
<td>
4<br/><br/></td><td>
\p<br/><br/></td><td>
Specifies the characters that separate a TOC entry and its page number. The default is a tab with leader dots.<br/><br/></td></tr>
<tr>
<td>
5<br/><br/></td><td>
\t<br/><br/></td><td>
Builds a table of contents from paragraphs formatted with specified styles other than the built-in heading styles<br/><br/></td></tr>
</tbody>
</table>

## Adding a TOC field

The following code example shows how to add a table of contents (TOC) in Word document. 

{% tabs %}  

{% highlight c# tabtitle="C#" %}
//Creates a new Word document
WordDocument document = new WordDocument();
//Adds the section into the Word document
IWSection section = document.AddSection();
string paraText = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.";
//Adds the paragraph into the created section
IWParagraph paragraph = section.AddParagraph();
//Appends the TOC field with LowerHeadingLevel and UpperHeadingLevel to determines the TOC entries
paragraph.AppendTOC(1, 3);
//Adds the section into the Word document
section = document.AddSection();
//Adds the paragraph into the created section
paragraph = section.AddParagraph(); 
//Adds the text for the headings
paragraph.AppendText("First Chapter");
//Sets a built-in heading style.
paragraph.ApplyStyle(BuiltinStyle.Heading1);
//Adds the text into the paragraph
section.AddParagraph().AppendText(paraText);
//Adds the section into the Word document
section = document.AddSection();
//Adds the paragraph into the created section
paragraph = section.AddParagraph();
//Adds the text for the headings
paragraph.AppendText("Second Chapter");
//Sets a built-in heading style.
paragraph.ApplyStyle(BuiltinStyle.Heading2);
//Adds the text into the paragraph
section.AddParagraph().AppendText(paraText);
//Adds the section into the Word document
section = document.AddSection();
//Adds the paragraph into the created section
paragraph = section.AddParagraph();
//Adds the text into the headings
paragraph.AppendText("Third Chapter");
//Sets a built-in heading style
paragraph.ApplyStyle(BuiltinStyle.Heading3);
//Adds the text into the paragraph.
section.AddParagraph().AppendText(paraText);
//Updates the table of contents
document.UpdateTableOfContents();
//Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Creates a new Word document
Dim document As New WordDocument()
'Adds the section into the Word document
Dim section As IWSection = document.AddSection()
Dim paraText As String = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company."
'Adds the paragraph into the created section
Dim paragraph As IWParagraph = section.AddParagraph()
'Appends the TOC field with LowerHeadingLevel and UpperHeadingLevel to determines the TOC entries
paragraph.AppendTOC(1, 3)
'Adds the section into the Word document
section = document.AddSection()
'Adds the paragraph into the created section
paragraph = section.AddParagraph()
'Adds the text for the headings
paragraph.AppendText("First Chapter")
'Sets a built-in heading style
paragraph.ApplyStyle(BuiltinStyle.Heading1)
'Adds the text into the paragraph.
section.AddParagraph().AppendText(paraText)
'Adds the section into the Word document
section = document.AddSection()
'Adds the paragraph into the created section
paragraph = section.AddParagraph()
'Adds the text for the headings
paragraph.AppendText("Second Chapter")
'Sets a built-in heading style
paragraph.ApplyStyle(BuiltinStyle.Heading2)
'Adds the text into the paragraph
section.AddParagraph().AppendText(paraText)
'Adds the section into the Word document
section = document.AddSection()
'Adds the paragraph into the created section
paragraph = section.AddParagraph()
'Adds the text into the headings
paragraph.AppendText("Third Chapter")
'Sets a built-in heading style
paragraph.ApplyStyle(BuiltinStyle.Heading3)
'Adds the text into the paragraph
section.AddParagraph().AppendText(paraText)
'Updates the table of contents
document.UpdateTableOfContents()
‘Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//DocIO supports Table of contents in WPF, Windows Forms platforms alone
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Creates a new Word document
WordDocument document = new WordDocument();
//Adds the section into the Word document
IWSection section = document.AddSection();
string paraText = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.";
//Adds the paragraph into the created section
IWParagraph paragraph = section.AddParagraph();
//Appends the TOC field with LowerHeadingLevel and UpperHeadingLevel to determines the TOC entries
paragraph.AppendTOC(1, 3);
//Adds the section into the Word document
section = document.AddSection();
//Adds the paragraph into the created section
paragraph = section.AddParagraph();
//Adds the text for the headings
paragraph.AppendText("First Chapter");
//Sets a built-in heading style.
paragraph.ApplyStyle(BuiltinStyle.Heading1);
//Adds the text into the paragraph
section.AddParagraph().AppendText(paraText);
//Adds the section into the Word document
section = document.AddSection();
//Adds the paragraph into the created section
paragraph = section.AddParagraph();
//Adds the text for the headings
paragraph.AppendText("Second Chapter");
//Sets a built-in heading style.
paragraph.ApplyStyle(BuiltinStyle.Heading2);
//Adds the text into the paragraph
section.AddParagraph().AppendText(paraText);
//Adds the section into the Word document
section = document.AddSection();
//Adds the paragraph into the created section
paragraph = section.AddParagraph();
//Adds the text into the headings
paragraph.AppendText("Third Chapter");
//Sets a built-in heading style
paragraph.ApplyStyle(BuiltinStyle.Heading3);
//Adds the text into the paragraph.
section.AddParagraph().AppendText(paraText);
//Updates the table of contents
document.UpdateTableOfContents();
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Sample.docx");
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Creates a new Word document
WordDocument document = new WordDocument();
//Adds the section into the Word document
IWSection section = document.AddSection();
string paraText = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.";
//Adds the paragraph into the created section
IWParagraph paragraph = section.AddParagraph();
//Appends the TOC field with LowerHeadingLevel and UpperHeadingLevel to determines the TOC entries
paragraph.AppendTOC(1, 3);
//Adds the section into the Word document
section = document.AddSection();
//Adds the paragraph into the created section
paragraph = section.AddParagraph();
//Adds the text for the headings
paragraph.AppendText("First Chapter");
//Sets a built-in heading style.
paragraph.ApplyStyle(BuiltinStyle.Heading1);
//Adds the text into the paragraph
section.AddParagraph().AppendText(paraText);
//Adds the section into the Word document
section = document.AddSection();
//Adds the paragraph into the created section
paragraph = section.AddParagraph();
//Adds the text for the headings
paragraph.AppendText("Second Chapter");
//Sets a built-in heading style.
paragraph.ApplyStyle(BuiltinStyle.Heading2);
//Adds the text into the paragraph
section.AddParagraph().AppendText(paraText);
//Adds the section into the Word document
section = document.AddSection();
//Adds the paragraph into the created section
paragraph = section.AddParagraph();
//Adds the text into the headings
paragraph.AppendText("Third Chapter");
//Sets a built-in heading style
paragraph.ApplyStyle(BuiltinStyle.Heading3);
//Adds the text into the paragraph.
section.AddParagraph().AppendText(paraText);
//Updates the table of contents
document.UpdateTableOfContents();
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Save the stream as a file in the device and invoke it for viewing         
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.docx", "application/msword", stream);
//Closes the document instance
document.Close();

//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Table-Of-Contents/Add-table-of-contents).

## Updating table of contents

You can also update or re-build the TOC in an existing document or document created from the scratch.  

N>  1. Updating of TOC is not supported in Silverlight, WinRT, Universal and Windows Phone applications. 
N>  2. Updating TOC makes use of the Word to PDF layout engine that may lead to update incorrect page number due to its limitations.
N>  3. In ASP.NET Core, Blazor, and Xamarin platforms, to update TOC in a Word document we recommend you to use Word to PDF [assemblies](https://help.syncfusion.com/file-formats/docio/assemblies-required#converting-word-document-to-pdf) or [NuGet](https://help.syncfusion.com/file-formats/docio/nuget-packages-required#converting-word-document-to-pdf) as a reference in your application.

The following code example shows how to update a TOC in an existing word document. 

{% tabs %} 

{% highlight c# tabtitle="C#" %}
//Opens an input word template
WordDocument document = new WordDocument(@”Template.docx”);
//Updates the table of contents.
document.UpdateTableOfContents();
//Saves and closes the Word document instance.
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Opens an input word template
Dim document As New WordDocument("Template.docx")
'Updates the table of contents.
document.UpdateTableOfContents()
‘Saves and closes the Word document instance.
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//DocIO supports Table of contents in WPF, Windows Forms platforms alone
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Opens an existing document from stream through constructor of WordDocument class
FileStream fileStreamPath = new FileStream("Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
WordDocument document = new WordDocument(fileStreamPath, FormatType.Automatic);
//Updates the table of contents.
document.UpdateTableOfContents();
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Sample.docx");
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing document through constructor of WordDocument class
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Automatic);
//Updates the table of contents
document.UpdateTableOfContents();
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Saves the stream as a file in the device and invoke it for viewing              
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.docx", "application/msword", stream);
//Closes the document instance
document.Close();

//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Table-Of-Contents/Update-table-of-contents).

## Creating table of contents with user-defined styles

The following code example shows how to create table of contents with user-defined styles instead of heading styles.

{% tabs %} 

{% highlight c# tabtitle="C#" %}
//Creates a new Word document
WordDocument document = new WordDocument();
//Creates a new custom styles
Style style = (WParagraphStyle)document.AddParagraphStyle("MyStyle");
style.CharacterFormat.Bold = true;
style.CharacterFormat.FontName = "Verdana";
style.CharacterFormat.FontSize = 25;
//Adds the section into the Word document
IWSection section = document.AddSection();
string paraText = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.";
//Adds the paragraph into the created section
IWParagraph paragraph = section.AddParagraph();
//Appends the TOC field with LowerHeadingLevel and UpperHeadingLevel to determines the TOC entries
TableOfContent tableOfContents = paragraph.AppendTOC(1, 3);
tableOfContents.UseHeadingStyles = false;
//Sets the TOC level style based on the created TOC 
tableOfContents.SetTOCLevelStyle(2, "MyStyle");
//Adds the section into the Word document
section = document.AddSection();
//Adds the paragraph into the created section
paragraph = section.AddParagraph();
//Adds the text for the headings
paragraph.AppendText("First Chapter");
//Sets the built-in heading style
paragraph.ApplyStyle("MyStyle");
//Adds the text into the paragraph
section.AddParagraph().AppendText(paraText);
//Adds the section into the Word document
section = document.AddSection();
//Adds the paragraph into the created section
paragraph = section.AddParagraph();
//Adds the text for the headings
paragraph.AppendText("Second Chapter");
//Sets the built-in heading style
paragraph.ApplyStyle(BuiltinStyle.Heading1);
//Adds the text to the paragraph
section.AddParagraph().AppendText(paraText);
//Adds the section into Word document
section = document.AddSection();
//Adds a paragraph to a created section
paragraph = section.AddParagraph();
//Adds the text for the headings
paragraph.AppendText("Third Chapter");
//Sets the built-in heading style
paragraph.ApplyStyle("MyStyle");
//Adds the text to the paragraph
section.AddParagraph().AppendText(paraText);
//Updates the table of contents
document.UpdateTableOfContents();
//Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Creates a new Word document
Dim document As New WordDocument()
'Creates a new custom styles
Dim style As Style = DirectCast(document.AddParagraphStyle("MyStyle"), WParagraphStyle)
style.CharacterFormat.Bold = True
style.CharacterFormat.FontName = "Verdana"
style.CharacterFormat.FontSize = 25
'Adds the section into the Word document
Dim section As IWSection = document.AddSection()
Dim paraText As String = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company."
'Adds the paragraph into the created section
Dim paragraph As IWParagraph = section.AddParagraph()
'Appends the TOC field with LowerHeadingLevel and UpperHeadingLevel to determine the TOC entries
Dim tableOfContents As TableOfContent = paragraph.AppendTOC(1, 3)
tableOfContents.UseHeadingStyles = False
'Sets the TOC level style based on the created TOC 
tableOfContents.SetTOCLevelStyle(2, "MyStyle")
'Adds the section into the Word document
section = document.AddSection()
'Adds the paragraph into the created section
paragraph = section.AddParagraph()
'Adds the text for the headings
paragraph.AppendText("First Chapter")
'Sets the built-in heading style
paragraph.ApplyStyle("MyStyle")
'Adds the text into the paragraph
section.AddParagraph().AppendText(paraText)
'Adds the section into the Word document
section = document.AddSection()
'Adds the paragraph into the created section
paragraph = section.AddParagraph()
'Adds the text for the headings
paragraph.AppendText("Second Chapter")
'Sets the built-in heading style
paragraph.ApplyStyle(BuiltinStyle.Heading1)
'Adds the text to the paragraph
section.AddParagraph().AppendText(paraText)
'Adds the section into Word document
section = document.AddSection()
'Adds a paragraph to created section
paragraph = section.AddParagraph()
'Adds the text for the headings
paragraph.AppendText("Third Chapter")
'Sets the built-in heading style
paragraph.ApplyStyle("My style")
'Adds the text to the paragraph
section.AddParagraph().AppendText(paraText)
'Updates the table of contents
document.UpdateTableOfContents()
‘Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//DocIO supports Table of contents in WPF, Windows Forms platforms alone
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Creates a new Word document
WordDocument document = new WordDocument();
//Creates a new custom styles
Style style = (WParagraphStyle)document.AddParagraphStyle("MyStyle");
style.CharacterFormat.Bold = true;
style.CharacterFormat.FontName = "Verdana";
style.CharacterFormat.FontSize = 25;
//Adds the section into the Word document
IWSection section = document.AddSection();
string paraText = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.";
//Adds the paragraph into the created section
IWParagraph paragraph = section.AddParagraph();
//Appends the TOC field with LowerHeadingLevel and UpperHeadingLevel to determines the TOC entries
TableOfContent tableOfContents = paragraph.AppendTOC(1, 3);
tableOfContents.UseHeadingStyles = false;
//Sets the TOC level style based on the created TOC 
tableOfContents.SetTOCLevelStyle(2, "MyStyle");
//Adds the section into the Word document
section = document.AddSection();
//Adds the paragraph into the created section
paragraph = section.AddParagraph();
//Adds the text for the headings
paragraph.AppendText("First Chapter");
//Sets the built-in heading style
paragraph.ApplyStyle("MyStyle");
//Adds the text into the paragraph
section.AddParagraph().AppendText(paraText);
//Adds the section into the Word document
section = document.AddSection();
//Adds the paragraph into the created section
paragraph = section.AddParagraph();
//Adds the text for the headings
paragraph.AppendText("Second Chapter");
//Sets the built-in heading style
paragraph.ApplyStyle(BuiltinStyle.Heading1);
//Adds the text to the paragraph
section.AddParagraph().AppendText(paraText);
//Adds the section into Word document
section = document.AddSection();
//Adds a paragraph to a created section
paragraph = section.AddParagraph();
//Adds the text for the headings
paragraph.AppendText("Third Chapter");
//Sets the built-in heading style
paragraph.ApplyStyle("MyStyle");
//Adds the text to the paragraph
section.AddParagraph().AppendText(paraText);
//Updates the table of contents
document.UpdateTableOfContents();
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Sample.docx");
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Creates a new Word document
WordDocument document = new WordDocument();
//Creates a new custom styles
Style style = (WParagraphStyle)document.AddParagraphStyle("MyStyle");
style.CharacterFormat.Bold = true;
style.CharacterFormat.FontName = "Verdana";
style.CharacterFormat.FontSize = 25;
//Adds the section into the Word document
IWSection section = document.AddSection();
string paraText = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.";
//Adds the paragraph into the created section
IWParagraph paragraph = section.AddParagraph();
//Appends the TOC field with LowerHeadingLevel and UpperHeadingLevel to determines the TOC entries
TableOfContent tableOfContents = paragraph.AppendTOC(1, 3);
tableOfContents.UseHeadingStyles = false;
//Sets the TOC level style based on the created TOC 
tableOfContents.SetTOCLevelStyle(2, "MyStyle");
//Adds the section into the Word document
section = document.AddSection();
//Adds the paragraph into the created section
paragraph = section.AddParagraph();
//Adds the text for the headings
paragraph.AppendText("First Chapter");
//Sets the built-in heading style
paragraph.ApplyStyle("MyStyle");
//Adds the text into the paragraph
section.AddParagraph().AppendText(paraText);
//Adds the section into the Word document
section = document.AddSection();
//Adds the paragraph into the created section
paragraph = section.AddParagraph();
//Adds the text for the headings
paragraph.AppendText("Second Chapter");
//Sets the built-in heading style
paragraph.ApplyStyle(BuiltinStyle.Heading1);
//Adds the text to the paragraph
section.AddParagraph().AppendText(paraText);
//Adds the section into Word document
section = document.AddSection();
//Adds a paragraph to a created section
paragraph = section.AddParagraph();
//Adds the text for the headings
paragraph.AppendText("Third Chapter");
//Sets the built-in heading style
paragraph.ApplyStyle("MyStyle");
//Adds the text to the paragraph
section.AddParagraph().AppendText(paraText);
//Updates the table of contents
document.UpdateTableOfContents();
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Save the stream as a file in the device and invoke it for viewing     
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.docx", "application/msword", stream);
//Closes the document instance
document.Close();

//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Table-Of-Contents/TOC-with-user-defined-styles).