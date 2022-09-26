---
title: Working with Word document | DocIO | Syncfusion
description: This section illustrates how to combine multiple Word documents into one, print a Word document, apply styles, and iterate through DOM elements.
platform: file-formats
control: DocIO
documentation: UG
---
# Working with Word document

## Cloning a Word document

You can create a deep copy of a Word document by using `Clone` method of `WordDocument` class. You can read the template document from file system or stream and create multiple document copies by cloning it. This improves the performance of document generation, as there is no need to read the Word document each time.

{% tabs %} 

{% highlight c# tabtitle="C#" %}
//Opens an existing document 
WordDocument inputTemplateDoc = new WordDocument(fileName);
//Creates a clone of Input Template 
WordDocument clonedDocument = inputTemplateDoc.Clone();
//Saves and closes the cloned document instance
clonedDocument.Save("ClonedDocument.docx");
clonedDocument.Close();
//Closes the input template document instance
sourceDocument.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Opens an existing document 
Dim inputTemplateDoc As New WordDocument(fileName)
'Creates a clone of Input Template 
Dim clonedDocument As WordDocument = inputTemplateDoc.Clone()
'Saves and closes the cloned document instance
clonedDocument.Save("ClonedDocument.docx")
clonedDocument.Close()
'Closes the input template document instance
sourceDocument.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
using (WordDocument document = new WordDocument(assembly.GetManifestResourceStream("CreateWordSample.Assets.Test.docx"), FormatType.Docx))
{
	WordDocument clonedDocument = document.Clone();
	MemoryStream stream = new MemoryStream();
	//Saves the Word file to MemoryStream
	await clonedDocument.SaveAsync(stream, FormatType.Docx);
	//Saves the stream as Word file in local machine
	Save(stream, "Result.docx");
	//Please refer the below link to save Word document in UWP platform
	//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
	document.Close();
	clonedDocument.Close();
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
FileStream fileStreamPath = new FileStream(@"Data/Hello World.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument(fileStreamPath, FormatType.Automatic))
{
	//Creates a clone of Input Template 
	WordDocument clonedDocument = document.Clone();
	MemoryStream stream = new MemoryStream();
	//Saves and closes the cloned document instance
	clonedDocument.Save(stream, FormatType.Docx);
	//Closes the document
	document.Close();
	clonedDocument.Close();
	stream.Position = 0;
	//Download Word document in the browser
	return File(stream, "application/msword", "Result.docx");
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
using (WordDocument document = new WordDocument(assembly.GetManifestResourceStream("CreateWordSample.Assets.Test.docx"), FormatType.Automatic))
{
	WordDocument clonedDocument = document.Clone();
	MemoryStream stream = new MemoryStream();
	clonedDocument.Save(stream, FormatType.Docx);
	//Save the stream as a file in the device and invoke it for viewing
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("WorkingWordDoc.docx", "application/msword", stream);
	//Closes the document
	clonedDocument.Close();
    document.Close();
	//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
	//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
}
{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-document/Clone-whole-Word-document).

You can also create a deep copy of document elements such as sections, paragraphs, Tables, Text, Image, OleObject, Shapes, TextBoxes and etc., The following code example illustrates how to clone the section and save each cloned section as a Word document. 

{% tabs %} 

{% highlight c# tabtitle="C#" %}
//Opens a source document
WordDocument sourceDocument = new WordDocument("SourceDocument.docx");
//Processes the each section in the Word document
for (int i = 0; i < sourceDocument.Sections.Count;i++)
{
	//Creates new WordDocument instance to add cloned section
	WordDocument destinationDocument = new WordDocument();
	//Clones and adds source document sections to the destination document
	destinationDocument.Sections.Add(sourceDocument.Sections[i].Clone());
	//Saves and closes the document instance
	destinationDocument.Save("Section_" + i + ".docx");
	destinationDocument.Close();
}
//Closes the source document instance
sourceDocument.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Opens a source document
Dim sourceDocument As New WordDocument("SourceDocument.docx")
'Processes the each section in the Word document
For i As Integer = 0 To sourceDocument.Sections.Count - 1
	'Creates new WordDocument instance to add cloned section
	Dim destinationDocument As New WordDocument()
	'Clones and adds source document sections to the destination document
	destinationDocument.Sections.Add(sourceDocument.Sections(i).Clone())
	'Saves and closes the document instance
	destinationDocument.Save("Section_" + i + ".docx")
	destinationDocument.Close()
Next
'Closes the source document instance
sourceDocument.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Creates an instance of WordDocument class
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
WordDocument sourceDocument = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.SourceDocument.docx"), FormatType.Docx);
//Processes the each section in the Word document
for (int i = 0; i < sourceDocument.Sections.Count;i++)
{
	//Creates new WordDocument instance to add cloned section
	WordDocument destinationDocument = new WordDocument();
	//Clones and adds source document sections to the destination document
	destinationDocument.Sections.Add(sourceDocument.Sections[i].Clone());		
	//Saves the Word file to MemoryStream
	MemoryStream stream = new MemoryStream();
	await destinationDocument.SaveAsync(stream, FormatType.Docx);
	//Saves the stream as Word file in local machine.Please find Save method in [link](https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp)
	Save(stream, "Section_" + i + ".docx");
	destinationDocument.Close();
}
//Closes the source document instance
sourceDocument.Close();
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Creates an instance of WordDocument class
FileStream fileStreamPath = new FileStream("SourceDocument.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
WordDocument sourceDocument = new WordDocument(fileStreamPath);
//Processes the each section in the Word document
for (int i = 0; i < sourceDocument.Sections.Count;i++)
{
	//Creates new WordDocument instance to add cloned section
	WordDocument destinationDocument = new WordDocument();
	//Clones and adds source document sections to the destination document
	destinationDocument.Sections.Add(sourceDocument.Sections[i].Clone());
	//Saves and closes the document instance
	FileStream outputStream = new FileStream("Section_" + i + ".docx", FileMode.Create, FileAccess.ReadWrite, FileShare.ReadWrite);
	destinationDocument.Save(outputStream, FormatType.Docx);
	destinationDocument.Close();
	outputStream.Flush();
	outputStream.Dispose();		
}
//Closes the source document instance
sourceDocument.Close();
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Creates an instance of WordDocument class
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
WordDocument sourceDocument = new WordDocument(assembly.GetManifestResourceStream("GettingStarted.Assets.SourceDocument.docx"), FormatType.Docx);
//Processes the each section in the Word document
for (int i = 0; i < sourceDocument.Sections.Count;i++)
{
	//Creates new WordDocument instance to add cloned section
	WordDocument destinationDocument = new WordDocument();
	//Clones and adds source document sections to the destination document
	destinationDocument.Sections.Add(sourceDocument.Sections[i].Clone());
	//Saves and closes the document instance
	MemoryStream stream = new MemoryStream();
	destinationDocument.Save(stream, FormatType.Docx);
	//Save the stream as a file in the device and invoke it for viewing
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Section_" + i + ".docx", "application/msword", stream);	
	destinationDocument.Close();
	//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
	//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
}
//Closes the source document instance
sourceDocument.Close();

{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-document/Split-by-section).

### Link Paragraph and Character Style

You can link character styles with paragraph and vice versa in a Word document using LinkedStyleName property.

The following code example explains how to link character and paragraph style.

{% tabs %} 

{% highlight c# %}
//Creates a Word document
using (WordDocument document = new WordDocument())
{
    //This method adds a section and a paragraph in the document
    document.EnsureMinimal();
    //Adds a new paragraph style named "ParagraphStyle"
    WParagraphStyle paraStyle = document.AddParagraphStyle("ParagraphStyle") as WParagraphStyle;
    //Sets the formatting of the style
    paraStyle.ParagraphFormat.HorizontalAlignment = HorizontalAlignment.Center;
    //Adds a new character style named "CharacterStyle"
    IWCharacterStyle charStyle = document.AddCharacterStyle("CharacterStyle");
    //Sets the formatting of the style
    charStyle.CharacterFormat.Bold = true;
    charStyle.CharacterFormat.Italic = true;
    //Link both paragraph and character style
     paraStyle.LinkedStyleName = "CharacterStyle";
    //Appends the contents into the paragraph
    document.LastParagraph.AppendText("AdventureWorks Cycles");
    //Applies the style to paragraph
    document.LastParagraph.ApplyStyle("ParagraphStyle");
    //Appends new paragraph in section
    document.LastSection.AddParagraph();
    //Appends the contents into the paragraph
    document.LastParagraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");
    //Applies paragraph style to the text range
    (document.LastParagraph.ChildEntities[0] as WTextRange).ApplyStyle("ParagraphStyle");
    //Saves the document
    document.Save("Result.docx", FormatType.Docx);
}
{% endhighlight %}

{% highlight vb.net %}
'Opens an input Word template
Using document As WordDocument = New WordDocument()
    'This method adds a section and a paragraph in the document
    document.EnsureMinimal()
    'Adds a new paragraph style named "ParagraphStyle"
    Dim paraStyle As WParagraphStyle = TryCast(document.AddParagraphStyle("ParagraphStyle"), WParagraphStyle)
    'Sets the formatting of the style
    paraStyle.ParagraphFormat.HorizontalAlignment = HorizontalAlignment.Center
    'Adds a new character style named "CharacterStyle"
    Dim charStyle As IWCharacterStyle = document.AddCharacterStyle("CharacterStyle")
    'Sets the formatting of the style
    charStyle.CharacterFormat.Bold = True
    charStyle.CharacterFormat.Italic = True
    'Link both paragraph and character style
    paraStyle.LinkedStyleName = "CharacterStyle"
    'Appends the content into the paragraph
    document.LastParagraph.AppendText("AdventureWorks Cycles")
    'Applies the style to paragraph
    document.LastParagraph.ApplyStyle("ParagraphStyle")
    'Appends new paragraph in section
    document.LastSection.AddParagraph()
    'Appends the content into the paragraph
    document.LastParagraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.")
    'Applies paragraph style to the text range
    Dim textRange As WTextRange = TryCast(document.LastParagraph.ChildEntities(0), WTextRange)
    textRange.ApplyStyle("ParagraphStyle")
    'Saves the document
    document.Save("Result.docx", FormatType.Docx)
End Using
{% endhighlight %}

{% highlight UWP %}
//Creates a Word document
using (WordDocument document = new WordDocument())
{
	//This method adds a section and a paragraph in the document
	document.EnsureMinimal();
	//Adds a new paragraph style named "ParagraphStyle"
	WParagraphStyle paraStyle = document.AddParagraphStyle("ParagraphStyle") as WParagraphStyle;
	//Sets the formatting of the style
	paraStyle.ParagraphFormat.HorizontalAlignment = Syncfusion.DocIO.DLS.HorizontalAlignment.Center;
	//Adds a new character style named "CharacterStyle"
	IWCharacterStyle charStyle = document.AddCharacterStyle("CharacterStyle");
	//Sets the formatting of the style
	charStyle.CharacterFormat.Bold = true;
	charStyle.CharacterFormat.Italic = true;
	//Link both paragraph and character style
	paraStyle.LinkedStyleName = "CharacterStyle";
	//Appends the contents into the paragraph
	document.LastParagraph.AppendText("AdventureWorks Cycles");
	//Applies the style to paragraph
	document.LastParagraph.ApplyStyle("ParagraphStyle");
	//Appends new paragraph in section
	document.LastSection.AddParagraph();
	//Appends the contents into the paragraph
	document.LastParagraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");
	//Applies paragraph style to the text range
	(document.LastParagraph.ChildEntities[0] as WTextRange).ApplyStyle("ParagraphStyle");
	//Saves the Word file to MemoryStream
	await document.SaveAsync(stream, FormatType.Docx);
	//Saves the stream as Word file in local machine
	Save(stream, "Result.docx");	
	//Please refer the below link to save Word document in UWP platform
	//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
}
{% endhighlight %}

{% highlight ASP.NET CORE %}
//Creates a Word document
using (WordDocument document = new WordDocument())
{
	//This method adds a section and a paragraph in the document
	document.EnsureMinimal();
	//Adds a new paragraph style named "ParagraphStyle"
	WParagraphStyle paraStyle = document.AddParagraphStyle("ParagraphStyle") as WParagraphStyle;
	//Sets the formatting of the style
	paraStyle.ParagraphFormat.HorizontalAlignment = HorizontalAlignment.Center;
	//Adds a new character style named "CharacterStyle"
	IWCharacterStyle charStyle = document.AddCharacterStyle("CharacterStyle");
	//Sets the formatting of the style
	charStyle.CharacterFormat.Bold = true;
	charStyle.CharacterFormat.Italic = true;
	//Link both paragraph and character style
	paraStyle.LinkedStyleName = "CharacterStyle";
	//Appends the contents into the paragraph
	document.LastParagraph.AppendText("AdventureWorks Cycles");
	//Applies the style to paragraph
	document.LastParagraph.ApplyStyle("ParagraphStyle");
	//Appends new paragraph in section
	document.LastSection.AddParagraph();
	//Appends the contents into the paragraph
	document.LastParagraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");
	//Applies paragraph style to the text range
	(document.LastParagraph.ChildEntities[0] as WTextRange).ApplyStyle("ParagraphStyle");
	MemoryStream stream = new MemoryStream();
	//Saves the document to  MemoryStream
	document.Save(stream, FormatType.Docx);
	stream.Position = 0;
	//Download Word document in the browser
	return File(stream, "application/msword", "Result.docx");
}
{% endhighlight %}

{% highlight XAMARIN %}
//Creates a Word document
using (WordDocument document = new WordDocument())
{
	//This method adds a section and a paragraph in the document
	document.EnsureMinimal();
	//Adds a new paragraph style named "ParagraphStyle"
	WParagraphStyle paraStyle = document.AddParagraphStyle("ParagraphStyle") as WParagraphStyle;
	//Sets the formatting of the style
	paraStyle.ParagraphFormat.HorizontalAlignment = HorizontalAlignment.Center;
	//Adds a new character style named "CharacterStyle"
	IWCharacterStyle charStyle = document.AddCharacterStyle("CharacterStyle");
	//Sets the formatting of the style
	charStyle.CharacterFormat.Bold = true;
	charStyle.CharacterFormat.Italic = true;
	//Link both paragraph and character style
	paraStyle.LinkedStyleName = "CharacterStyle";
	//Appends the contents into the paragraph
	document.LastParagraph.AppendText("AdventureWorks Cycles");
	//Applies the style to paragraph
	document.LastParagraph.ApplyStyle("ParagraphStyle");
	//Appends new paragraph in section
	document.LastSection.AddParagraph();
	//Appends the contents into the paragraph
	document.LastParagraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");
	//Applies paragraph style to the text range
	(document.LastParagraph.ChildEntities[0] as WTextRange).ApplyStyle("ParagraphStyle");
	MemoryStream stream = new MemoryStream();
	document.Save(stream, FormatType.Docx);
	//Save the stream as a file in the device and invoke it for viewing
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
	//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
	//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
}
{% endhighlight %}

{% endtabs %} 

## Working with Word document properties

Document properties, also known as metadata, are details about a file that describe or identify it. You can also define the additional custom document properties for the documents by using DocIO Document properties that are classified as two categories. 

* Built-in document properties - includes details such as title, author name, subject, and keywords that identify the document's topic or contents.
* Custom document properties - defines the user-defined document properties.

### Built-in document properties

The Built-in document properties of a word document is represented by `BuiltinDocumentProperties` property of `WordDocument` class. The following code example illustrates how to access and modify the Built-in document properties of the document.

{% tabs %} 

{% highlight c# tabtitle="C#" %}
//Opens an existing Word document
WordDocument document = new WordDocument(inputFileName);
//Accesses the built-in document properties
Console.WriteLine("Title - {0}",document.BuiltinDocumentProperties.Title);
Console.WriteLine("Author - {0}", document.BuiltinDocumentProperties.Author);
//Modifies or sets the category and company Built-in document properties
document.BuiltinDocumentProperties.Category = "Sales reports";
document.BuiltinDocumentProperties.Company = "Northwind traders";
document.Save(outputFileName, FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Opens an existing Word document
Dim document As New WordDocument(inputFileName)
'Accesses the built-in document properties
Console.WriteLine("Title - {0}", document.BuiltinDocumentProperties.Title)
Console.WriteLine("Author - {0}", document.BuiltinDocumentProperties.Author)
'Modifies or sets the category and company Built-in document properties
document.BuiltinDocumentProperties.Category = "Sales reports"
document.BuiltinDocumentProperties.Company = "Northwind traders"
'Saves and closes the document
document.Save(outputFileName, FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
using (WordDocument document = new WordDocument(assembly.GetManifestResourceStream("CreateWordSample.Assets.Test.docx"), FormatType.Docx))
{
	//Accesses the built-in document properties
	Console.WriteLine("Title - {0}", document.BuiltinDocumentProperties.Title);
	Console.WriteLine("Author - {0}", document.BuiltinDocumentProperties.Author);
	//Modifies or sets the category and company Built-in document properties
	document.BuiltinDocumentProperties.Category = "Sales reports";
	document.BuiltinDocumentProperties.Company = "Northwind traders";
	MemoryStream stream = new MemoryStream();
	//Saves the Word file to MemoryStream
	await document.SaveAsync(stream, FormatType.Docx);
	//Saves the stream as Word file in local machine
	Save(stream, "Result.docx");
	//Please refer the below link to save Word document in UWP platform
	//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
	document.Close();
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
FileStream sourceStreamPath = new FileStream(sourceFileName, FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
//Opens an source document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument(sourceStreamPath, FormatType.Automatic))
{
	//Accesses the built-in document properties
	Console.WriteLine("Title - {0}",document.BuiltinDocumentProperties.Title);
	Console.WriteLine("Author - {0}", document.BuiltinDocumentProperties.Author);
	//Modifies or sets the category and company Built-in document properties
	document.BuiltinDocumentProperties.Category = "Sales reports";
	document.BuiltinDocumentProperties.Company = "Northwind traders";
	MemoryStream stream = new MemoryStream();
	//Saves and closes the destination document to  MemoryStream
	document.Save(stream, FormatType.Docx);
	document.Close();
	stream.Position = 0;
	//Download Word document in the browser
	return File(stream, "application/msword", "Result.docx");
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
using (WordDocument document = new WordDocument(assembly.GetManifestResourceStream("XamarinFormsApp1.Assets.Hello World.docx"), FormatType.Docx))
{
	//Accesses the built-in document properties
	Console.WriteLine("Title - {0}", document.BuiltinDocumentProperties.Title);
	Console.WriteLine("Author - {0}", document.BuiltinDocumentProperties.Author);
	//Modifies or sets the category and company Built-in document properties
	document.BuiltinDocumentProperties.Category = "Sales reports";
	document.BuiltinDocumentProperties.Company = "Northwind traders";
	MemoryStream stream = new MemoryStream();
	document.Save(stream, FormatType.Docx);
	//Save the stream as a file in the device and invoke it for viewing
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("WorkingWordDoc.docx", "application/msword", stream);
	//Closes the document              
	document.Close();
	//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
	//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
}
{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-document/Modify-built-in-document-properties).

### Updating words count

You can update the count of Paragraphs, words and characters in an existing Word document or document that created from the scratch.

The following code example shows how to update word count in an existing word document.
{% tabs %} 
{% highlight c# tabtitle="C#" %}
//Open an existing document.
using (WordDocument document = new WordDocument("Sample.docx", FormatType.Docx))
{
    //Update the word count in the document.
    document.UpdateWordCount(false);
    //Get the word count in the document.
    int wordCount = document.BuiltinDocumentProperties.WordCount;
    //Get the character count in the document.
    int charCount = document.BuiltinDocumentProperties.CharCount;
    //Get the paragraph count in the document.
    int paragraphCount = document.BuiltinDocumentProperties.ParagraphCount;
    //Save the Word document.
    document.Save("Result.docx");
}
{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET" %}
'Open an existing document.
Using document As WordDocument = New WordDocument("Sample.docx", FormatType.Docx)
    'Update the word count in the document.
     document.UpdateWordCount(False)
    'Get the word count in the document.
    Dim wordCount As Integer = document.BuiltinDocumentProperties.WordCount
    'Get the character count in the document.
    Dim charCount As Integer = document.BuiltinDocumentProperties.CharCount
    'Get the paragraph count in the document.
    Dim paragraphCount As Integer = document.BuiltinDocumentProperties.ParagraphCount
    'Save the Word document.
    document.Save("Result.docx")
End Using	
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//DocIO supports updating word count in WPF, Windows Forms, ASP.NET and ASP.NET MVC, platforms alone.
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
FileStream fileStream = new FileStream("Sample.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
//Open an existing document.
using (WordDocument document = new WordDocument(fileStream, FormatType.Docx))
{
    //Update the word count in the document.
    document.UpdateWordCount(false);
    //Get the word count in the document.
    int wordCount = document.BuiltinDocumentProperties.WordCount;
    //Get the character count in the document.
    int charCount = document.BuiltinDocumentProperties.CharCount;
    //Get the paragraph count in the document.
    int paragraphCount = document.BuiltinDocumentProperties.ParagraphCount;
    MemoryStream stream = new MemoryStream();
    //Save the Word document.
    document.Save(stream, FormatType.Docx);
    stream.Position = 0;
    fileStream.Dispose();
    //Download Word document in the browser.
    return File(stream, "application/msword", "Result.docx");
}
{% endhighlight %}
{% highlight c# tabtitle="Xamarin" %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Open an existing document.
using (WordDocument document = new WordDocument((assembly.GetManifestResourceStream("XamarinFormsApp.Assets.Sample.docx")), FormatType.Docx))
{
    //Update the word count in the document.
    document.UpdateWordCount(false); 
    //Get the word count in the document. 
    int wordCount = document.BuiltinDocumentProperties.WordCount;
    //Get the character count in the document. 
    int charCount = document.BuiltinDocumentProperties.CharCount;
    //Get the paragraph count in the document. 
    int paragraphCount = document.BuiltinDocumentProperties.ParagraphCount;	
    MemoryStream stream = new MemoryStream();
    document.Save(stream, FormatType.Docx);
    //Save the stream as a file in the device and invoke it for viewing.
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
    //Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform.
    //https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
}
{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-document/Update-words-count).

### Updating pages count

You can update page count in an existing Word document or document that created from the scratch by passing true for `UpdateWordCount(performLayout)` API.

The following code example shows how to update page count in an existing word document.
{% tabs %} 
{% highlight c# tabtitle="C#" %}
//Open an existing document.
using (WordDocument document = new WordDocument("Sample.docx", FormatType.Docx))
{
    //Update the page count along with word count in the document.
    document.UpdateWordCount(true);
    //Get the page count in the document.
    int pageCount = document.BuiltinDocumentProperties.PageCount;
    //Save the Word document.
    document.Save("Result.docx");
}
{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET" %}
'Open an existing document.
Using document As WordDocument = New WordDocument("Sample.docx", FormatType.Docx)
    'Update the page count along with word count in the document.
     document.UpdateWordCount(True)
    'Get the page count in the document.
    Dim pageCount As Integer = document.BuiltinDocumentProperties.PageCount
    'Save the Word document.
    document.Save("Result.docx")
End Using	
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//DocIO supports updating page count in WPF, Windows Forms, ASP.NET and ASP.NET MVC, platforms alone.
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
FileStream fileStream = new FileStream("Sample.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
//Open an existing document.
using (WordDocument document = new WordDocument(fileStream, FormatType.Docx))
{
    //Update the page count along with word count in the document.
    document.UpdateWordCount(true);
    //Get the page count in the document.
    int pageCount = document.BuiltinDocumentProperties.PageCount;
    MemoryStream stream = new MemoryStream();
    //Save the Word document.
    document.Save(stream, FormatType.Docx);
    stream.Position = 0;
    fileStream.Dispose();
    //Download Word document in the browser.
    return File(stream, "application/msword", "Result.docx");
}
{% endhighlight %}
{% highlight c# tabtitle="Xamarin" %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Open an existing document.
using (WordDocument document = new WordDocument((assembly.GetManifestResourceStream("XamarinFormsApp.Assets.Sample.docx")), FormatType.Docx))
{
    //Update the page count and word count in the document.
    document.UpdateWordCount(true);
    //Get the page count in the document. 
    int pageCount = document.BuiltinDocumentProperties.PageCount;	
    MemoryStream stream = new MemoryStream();
    document.Save(stream, FormatType.Docx);
    //Save the stream as a file in the device and invoke it for viewing.
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
    //Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform.
    //https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
}
{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-document/Update-pages-count).

N>  1. The word to PDF layout engine is used for updating the page count in word document. Due to its limitations it may result in an incorrect page count.
N>  2. In ASP.NET Core and Xamarin platforms, to update page count in a Word document we recommend you to use Word to PDF [assemblies](https://help.syncfusion.com/file-formats/docio/assemblies-required#converting-word-document-to-pdf) or [NuGet](https://help.syncfusion.com/file-formats/docio/nuget-packages-required#converting-word-document-to-pdf) as a reference in your application to update page count in a Word document.



### Adding Custom Document properties

You add a new custom document properties through `Add` method of `CustomProperties` class. The following code example illustrates how to add a new custom document properties.

{% tabs %} 

{% highlight c# tabtitle="C#" %}
//Opens an input word template
WordDocument document = new WordDocument(inputFileName);
//Adds the custom document properties of various data types
document.CustomDocumentProperties.Add("PropertyA", "Value of A");
document.CustomDocumentProperties.Add("PropertyB", 12.5);
document.CustomDocumentProperties.Add("PropertyC", true);
document.CustomDocumentProperties.Add("PropertyD", new DateTime(2015,7,20));
//Saves and closes the document
document.Save(outputFileName, FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Opens an existing document from file system through constructor of WordDocument class
Dim document As New WordDocument(inputFileName)
'Adds the custom document properties of various data types
document.CustomDocumentProperties.Add("PropertyA", "Value of A")
document.CustomDocumentProperties.Add("PropertyB", 12.5)
document.CustomDocumentProperties.Add("PropertyC", True)
document.CustomDocumentProperties.Add("PropertyD", New DateTime(2015, 7, 20))
'Saves and closes the document
document.Save(outputFileName, FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
using (WordDocument document = new WordDocument(assembly.GetManifestResourceStream("CreateWordSample.Assets.Test.docx"), FormatType.Docx))
{
	//Adds the custom document properties of various data types
	document.CustomDocumentProperties.Add("PropertyA", "Value of A");
	document.CustomDocumentProperties.Add("PropertyB", 12.5);
	document.CustomDocumentProperties.Add("PropertyC", true);
	document.CustomDocumentProperties.Add("PropertyD", new DateTime(2015,7,20));
	MemoryStream stream = new MemoryStream();
	//Saves the Word file to MemoryStream
	await document.SaveAsync(stream, FormatType.Docx);
	//Saves the stream as Word file in local machine
	Save(stream, "Result.docx");
	//Please refer the below link to save Word document in UWP platform
	//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
	document.Close();
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
FileStream sourceStreamPath = new FileStream(sourceFileName, FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
//Opens an source document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument(sourceStreamPath, FormatType.Automatic))
{
	//Adds the custom document properties of various data types
	document.CustomDocumentProperties.Add("PropertyA", "Value of A");
	document.CustomDocumentProperties.Add("PropertyB", 12.5);
	document.CustomDocumentProperties.Add("PropertyC", true);
	document.CustomDocumentProperties.Add("PropertyD", new DateTime(2015,7,20));
	MemoryStream stream = new MemoryStream();
	//Saves and closes the destination document to  MemoryStream
	document.Save(stream, FormatType.Docx);
	document.Close();
	stream.Position = 0;
	//Download Word document in the browser
	return File(stream, "application/msword", "Result.docx");
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
using (WordDocument document = new WordDocument(assembly.GetManifestResourceStream("XamarinFormsApp1.Assets.Hello World.docx"), FormatType.Docx))
{
	//Adds the custom document properties of various data types
	document.CustomDocumentProperties.Add("PropertyA", "Value of A");
	document.CustomDocumentProperties.Add("PropertyB", 12.5);
	document.CustomDocumentProperties.Add("PropertyC", true);
	document.CustomDocumentProperties.Add("PropertyD", new DateTime(2015,7,20));
	MemoryStream stream = new MemoryStream();
	document.Save(stream, FormatType.Docx);
	//Save the stream as a file in the device and invoke it for viewing
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("WorkingWordDoc.docx", "application/msword", stream);
	//Closes the document              
	document.Close();
	//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
	//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
}
{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-document/Add-custom-document-properties).

### Accessing & Modifying Custom Document Properties

You can access and modify an existing document property as shown in the following code example.

{% tabs %} 

{% highlight c# tabtitle="C#" %}
WordDocument document = new WordDocument(inputFileName);
//Accesses an existing custom document property
DocumentProperty property = document.CustomDocumentProperties["PropertyA"];
//Modifies the value of DocumentProperty instance
property.Value = "Hello world";
document.Save(outputFileName, FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Dim document As New WordDocument(inputFileName)
'Accesses an existing custom document property
Dim [property] As DocumentProperty = document.CustomDocumentProperties("PropertyA")
'Modifies the value of DocumentProperty instance
[property].Value = "Hello world"
document.Save(outputFileName, FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
using (WordDocument document = new WordDocument(assembly.GetManifestResourceStream("CreateWordSample.Assets.Test.docx"), FormatType.Docx))
{
	//Accesses an existing custom document property
	DocumentProperty property = document.CustomDocumentProperties["PropertyA"];
	//Modifies the value of DocumentProperty instance
	property.Value = "Hello world";
	MemoryStream stream = new MemoryStream();
	//Saves the Word file to MemoryStream
	await document.SaveAsync(stream, FormatType.Docx);
	//Saves the stream as Word file in local machine
	Save(stream, "Result.docx");
	//Please refer the below link to save Word document in UWP platform
	//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
	document.Close();
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
FileStream sourceStreamPath = new FileStream(sourceFileName, FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
//Opens an source document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument(sourceStreamPath, FormatType.Automatic))
{
	//Accesses an existing custom document property
	DocumentProperty property = document.CustomDocumentProperties["PropertyA"];
	//Modifies the value of DocumentProperty instance
	property.Value = "Hello world";
	MemoryStream stream = new MemoryStream();
	//Saves and closes the destination document to  MemoryStream
	document.Save(stream, FormatType.Docx);
	document.Close();
	stream.Position = 0;
	//Download Word document in the browser
	return File(stream, "application/msword", "Result.docx");
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
using (WordDocument document = new WordDocument(assembly.GetManifestResourceStream("XamarinFormsApp1.Assets.Hello World.docx"), FormatType.Docx))
{
	//Accesses an existing custom document property
	DocumentProperty property = document.CustomDocumentProperties["PropertyA"];
	//Modifies the value of DocumentProperty instance
	property.Value = "Hello world";
	MemoryStream stream = new MemoryStream();
	document.Save(stream, FormatType.Docx);
	//Save the stream as a file in the device and invoke it for viewing
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("WorkingWordDoc.docx", "application/msword", stream);
	//Closes the document              
	document.Close();
	//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
	//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
}
{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-document/Modify-custom-document-properties).

## Working with Content Type Properties

Content type properties refers the metadata stored in a Word document, such as author name, subject, and company. DocIO represents metadata with MetaProperty instance and you can access in the Word document (DOCX, WordML) by using the ContentTypeProperties collection of WordDocument class.

The following screenshots shows the content type property in the input Word document.
![Resultant output Word document](WorkingwithWordDocument_images/QuickPart.png)

N> You can use Content Type Properties only in documents that are saved in the DOCX or WordML Format.

### Accessing and modifying the Content Type Properties

You can access and modify the value of existing metadata in the Word document (DOCX, WordML).

The following code example explains how to access and modify the value of an existing metadata in the Word document.
{% tabs %} 

{% highlight c# tabtitle="C#" %}
//Loads the template document
WordDocument document = new WordDocument("Template.docx");
//Processes the metaproperty collection in the Word document
MetaProperties metaProperties = document.ContentTypeProperties;
//Iterates through each of the child items of metaproperties
for (int i = 0; i < metaProperties.Count; i++)
{
    //Checks for particular display name of meta data and modifies its value
    switch (metaProperties[i].DisplayName)
    {
        case "ProgressStatus":
            if (metaProperties[i].Type == MetaPropertyType.Text && !metaProperties[i].IsReadOnly)
            {
                metaProperties[i].Value = "Completed";
            }
            break;
        case "Reviewed":
            if (metaProperties[i].Type == MetaPropertyType.Boolean && !metaProperties[i].IsReadOnly)
            {
                metaProperties[i].Value = true;
            }
            break;
        case "Date":
            if (metaProperties[i].Type == MetaPropertyType.DateTime && !metaProperties[i].IsReadOnly)
            {
                metaProperties[i].Value = DateTime.UtcNow;
            }
            break;
        case "Salary":
            if ((metaProperties[i].Type == MetaPropertyType.Number ||
               metaProperties[i].Type == MetaPropertyType.Currency) && !metaProperties[i].IsReadOnly)
            {
                 metaProperties[i].Value = 12000;
            }
            break;
        case "Url":
            if (metaProperties[i].Type == MetaPropertyType.Url && !metaProperties[i].IsReadOnly)
            {
                string[] value = { "https://www.syncfusion.com", "Syncfusion page" };
                metaProperties[i].Value = value;
            }
            break;
        case "User":
            if (metaProperties[i].Type == MetaPropertyType.User && !metaProperties[i].IsReadOnly)
            {
                string[] value = { "1234", "Syncfusion" };
                metaProperties[i].Value = value;
            }
            break;
        default:
            break;
    }               
}
//Saves the Word document
document.Save("Sample.docx", FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Loads the template document
Dim document As WordDocument = New WordDocument("Template.docx")
'Processes the metaproperty collection in the Word document
Dim metaProperties As MetaProperties = document.ContentTypeProperties
'Iterates through each of the child items of metaproperties
Dim i As Integer = 0
Do While (i < metaProperties.Count)
    'Checks for particular display name of meta data and modifies its value
    Select Case (metaProperties(i).DisplayName)
        Case "ProgressStatus"
            If ((metaProperties(i).Type = MetaPropertyType.Text)  _
                        AndAlso Not metaProperties(i).IsReadOnly) Then
                metaProperties(i).Value = "Completed"
            End If
            
        Case "Reviewed"
            If ((metaProperties(i).Type = MetaPropertyType.Boolean)  _
                        AndAlso Not metaProperties(i).IsReadOnly) Then
                metaProperties(i).Value = true
            End If
            
        Case "Date"
            If ((metaProperties(i).Type = MetaPropertyType.DateTime)  _
                        AndAlso Not metaProperties(i).IsReadOnly) Then
                metaProperties(i).Value = DateTime.UtcNow
            End If
            
        Case "Salary"
            If (((metaProperties(i).Type = MetaPropertyType.Number)  _
                        OrElse (metaProperties(i).Type = MetaPropertyType.Currency))  _
                        AndAlso Not metaProperties(i).IsReadOnly) Then
                metaProperties(i).Value = 12000
            End If
            
        Case "Url"
            If ((metaProperties(i).Type = MetaPropertyType.Url)  _
                        AndAlso Not metaProperties(i).IsReadOnly) Then
                Dim value() As String = New String() {"https://www.syncfusion.com", "Syncfusion page"}
                metaProperties(i).Value = value
            End If
            
        Case "User"
            If ((metaProperties(i).Type = MetaPropertyType.User)  _
                        AndAlso Not metaProperties(i).IsReadOnly) Then
                Dim value() As String = New String() {"1234", "Syncfusion"}
                metaProperties(i).Value = value
            End If
            
    End Select
    
    i = (i + 1)
Loop
'Saves the Word document
document.Save("Sample.docx", FormatType.Docx)
'Closes the document
document.Close
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
using (WordDocument document = new WordDocument(assembly.GetManifestResourceStream("CreateWordSample.Assets.Template.docx"), FormatType.Docx))
{
//Processes the metaproperty collection in the Word document
MetaProperties metaProperties = document.ContentTypeProperties;
//Iterates through each of the child items of metaproperties
for (int i = 0; i < metaProperties.Count; i++)
{
    //Checks for particular display name of meta data and modifies its value
    switch (metaProperties[i].DisplayName)
    {
        case "ProgressStatus":
            if (metaProperties[i].Type == MetaPropertyType.Text && !metaProperties[i].IsReadOnly)
            {
                metaProperties[i].Value = "Completed";
            }
            break;
        case "Reviewed":
            if (metaProperties[i].Type == MetaPropertyType.Boolean && !metaProperties[i].IsReadOnly)
            {
                metaProperties[i].Value = true;
            }
            break;
        case "Date":
            if (metaProperties[i].Type == MetaPropertyType.DateTime && !metaProperties[i].IsReadOnly)
            {
                metaProperties[i].Value = DateTime.UtcNow;
            }
            break;
        case "Salary":
            if ((metaProperties[i].Type == MetaPropertyType.Number ||
               metaProperties[i].Type == MetaPropertyType.Currency) && !metaProperties[i].IsReadOnly)
            {
                 metaProperties[i].Value = 12000;
            }
            break;
        case "Url":
            if (metaProperties[i].Type == MetaPropertyType.Url && !metaProperties[i].IsReadOnly)
            {
                string[] value = { "https://www.syncfusion.com", "Syncfusion page" };
                metaProperties[i].Value = value;
            }
            break;
        case "User":
            if (metaProperties[i].Type == MetaPropertyType.User && !metaProperties[i].IsReadOnly)
            {
                string[] value = { "1234", "Syncfusion" };
                metaProperties[i].Value = value;
            }
            break;
        default:
            break;
    }               
}
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
document.Close();
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
FileStream sourceStreamPath = new FileStream("Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
//Loads the template document
using (WordDocument document = new WordDocument(sourceStreamPath, FormatType.Docx))
{
//Processes the metaproperty collection in the Word document
MetaProperties metaProperties = document.ContentTypeProperties;
//Iterates through each of the child items of metaproperties
for (int i = 0; i < metaProperties.Count; i++)
{
    //Checks for particular display name of meta data and modifies its value
    switch (metaProperties[i].DisplayName)
    {
        case "ProgressStatus":
            if (metaProperties[i].Type == MetaPropertyType.Text && !metaProperties[i].IsReadOnly)
            {
                metaProperties[i].Value = "Completed";
            }
            break;
        case "Reviewed":
            if (metaProperties[i].Type == MetaPropertyType.Boolean && !metaProperties[i].IsReadOnly)
            {
                metaProperties[i].Value = true;
            }
            break;
        case "Date":
            if (metaProperties[i].Type == MetaPropertyType.DateTime && !metaProperties[i].IsReadOnly)
            {
                metaProperties[i].Value = DateTime.UtcNow;
            }
            break;
        case "Salary":
            if ((metaProperties[i].Type == MetaPropertyType.Number ||
               metaProperties[i].Type == MetaPropertyType.Currency) && !metaProperties[i].IsReadOnly)
            {
                 metaProperties[i].Value = 12000;
            }
            break;
        case "Url":
            if (metaProperties[i].Type == MetaPropertyType.Url && !metaProperties[i].IsReadOnly)
            {
                string[] value = { "https://www.syncfusion.com", "Syncfusion page" };
                metaProperties[i].Value = value;
            }
            break;
        case "User":
            if (metaProperties[i].Type == MetaPropertyType.User && !metaProperties[i].IsReadOnly)
            {
                string[] value = { "1234", "Syncfusion" };
                metaProperties[i].Value = value;
            }
            break;
        default:
            break;
    }               
}
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Loads the template document
using (WordDocument document = new WordDocument(assembly.GetManifestResourceStream("XamarinFormsApp1.Assets.Template.docx"), FormatType.Docx))
{
//Processes the metaproperty collection in the Word document
MetaProperties metaProperties = document.ContentTypeProperties;
//Iterates through each of the child items of metaproperties
for (int i = 0; i < metaProperties.Count; i++)
{
    //Checks for particular display name of meta data and modifies its value
    switch (metaProperties[i].DisplayName)
    {
        case "ProgressStatus":
            if (metaProperties[i].Type == MetaPropertyType.Text && !metaProperties[i].IsReadOnly)
            {
                metaProperties[i].Value = "Completed";
            }
            break;
        case "Reviewed":
            if (metaProperties[i].Type == MetaPropertyType.Boolean && !metaProperties[i].IsReadOnly)
            {
                metaProperties[i].Value = true;
            }
            break;
        case "Date":
            if (metaProperties[i].Type == MetaPropertyType.DateTime && !metaProperties[i].IsReadOnly)
            {
                metaProperties[i].Value = DateTime.UtcNow;
            }
            break;
        case "Salary":
            if ((metaProperties[i].Type == MetaPropertyType.Number ||
               metaProperties[i].Type == MetaPropertyType.Currency) && !metaProperties[i].IsReadOnly)
            {
                 metaProperties[i].Value = 12000;
            }
            break;
        case "Url":
            if (metaProperties[i].Type == MetaPropertyType.Url && !metaProperties[i].IsReadOnly)
            {
                string[] value = { "https://www.syncfusion.com", "Syncfusion page" };
                metaProperties[i].Value = value;
            }
            break;
        case "User":
            if (metaProperties[i].Type == MetaPropertyType.User && !metaProperties[i].IsReadOnly)
            {
                string[] value = { "1234", "Syncfusion" };
                metaProperties[i].Value = value;
            }
            break;
        default:
            break;
    }               
}
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Closes the document              
document.Close();
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
}
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-document/Modify-content-type-properties).
  
## Setting the Background for a Word document

Essential DocIO allows to apply background such as color, gradient and picture to the Word document. A background of a Word document is represented by `Background` property of `WordDocument' class. 

The following code illustrates how to apply gradient as background to the document.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Creates a new Word document
WordDocument document = new WordDocument();
//Adds new section to the document
WSection section = document.AddSection() as WSection;
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph() as WParagraph;
//Appends text to the paragraph
paragraph.AppendText("Sample for applying document background");
//Sets the background type as gradient
document.Background.Type = BackgroundType.Gradient;
//Sets color for gradient
document.Background.Gradient.Color1 = Color.LightGray;
document.Background.Gradient.Color2 = Color.LightGreen;
//Sets the shading style 
document.Background.Gradient.ShadingStyle = GradientShadingStyle.DiagonalUp;
document.Background.Gradient.ShadingVariant = GradientShadingVariant.ShadingDown;
//Saves the document
document.Save("Sample.docx", FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Creates a new Word document 
Dim document As New WordDocument()
'Adds new section to the document
Dim section As WSection = TryCast(document.AddSection(), WSection)
'Adds new paragraph to the section 
Dim paragraph As IWParagraph = TryCast(section.AddParagraph(), WParagraph)
'Appends text to the paragraph
paragraph.AppendText("Sample for applying document background")
'Sets the background type as gradient
document.Background.Type = BackgroundType.Gradient
'Sets color for gradient
document.Background.Gradient.Color1 = Color.LightGray
document.Background.Gradient.Color2 = Color.LightGreen
'Sets the shading style 
document.Background.Gradient.ShadingStyle = GradientShadingStyle.DiagonalUp
document.Background.Gradient.ShadingVariant = GradientShadingVariant.ShadingDown
'Saves the document
document.Save("Sample.docx", FormatType.Docx)
'Closes the document
document.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
using (WordDocument document = new WordDocument(assembly.GetManifestResourceStream("CreateWordSample.Assets.Test.docx"), FormatType.Docx))
{
	document.Background.Type = BackgroundType.Picture;
	//Sets color for gradient
	document.Background.Gradient.Color1 = Syncfusion.DocIO.DLS.Color.LightGray;
	document.Background.Gradient.Color2 = Syncfusion.DocIO.DLS.Color.LightGreen;
	//Sets the shading style 
	document.Background.Gradient.ShadingStyle = GradientShadingStyle.DiagonalUp;
	document.Background.Gradient.ShadingVariant = GradientShadingVariant.ShadingDown;
	MemoryStream stream = new MemoryStream();
	//Saves the Word file to MemoryStream
	await document.SaveAsync(stream, FormatType.Docx);
	//Saves the stream as Word file in local machine
	Save(stream, "Result.docx");
	//Please refer the below link to save Word document in UWP platform
	//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
	document.Close();
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
FileStream sourceStreamPath = new FileStream(sourceFileName, FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
//Opens an source document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument(sourceStreamPath, FormatType.Automatic))
{
	//Sets the background type as picture
	document.Background.Type = BackgroundType.Picture;
	//Sets color for gradient
	document.Background.Gradient.Color1 = Syncfusion.Drawing.Color.LightGray;
	document.Background.Gradient.Color2 = Syncfusion.Drawing.Color.LightGreen;
	//Sets the shading style 
	document.Background.Gradient.ShadingStyle = GradientShadingStyle.DiagonalUp;
	document.Background.Gradient.ShadingVariant = GradientShadingVariant.ShadingDown;
	MemoryStream stream = new MemoryStream();
	//Saves and closes the destination document to  MemoryStream
	document.Save(stream, FormatType.Docx);
	document.Close();
	stream.Position = 0;
	//Download Word document in the browser
	return File(stream, "application/msword", "Result.docx");
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
using (WordDocument document = new WordDocument(assembly.GetManifestResourceStream("XamarinFormsApp1.Assets.Hello World.docx"), FormatType.Docx))
{
	document.Background.Type = BackgroundType.Picture;
	//Sets color for gradient
	document.Background.Gradient.Color1 = Syncfusion.Drawing.Color.LightGray;
	document.Background.Gradient.Color2 = Syncfusion.Drawing.Color.LightGreen;
	//Sets the shading style 
	document.Background.Gradient.ShadingStyle = GradientShadingStyle.DiagonalUp;
	document.Background.Gradient.ShadingVariant = GradientShadingVariant.ShadingDown;
	MemoryStream stream = new MemoryStream();
	document.Save(stream, FormatType.Docx);
	//Save the stream as a file in the device and invoke it for viewing
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("WorkingWordDoc.docx", "application/msword", stream);
	//Closes the document              
	document.Close();
	//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
	//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
}
{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-document/Apply-gradient-background-to-document).

The following code illustrates how to apply image as background for the document.

{% tabs %} 

{% highlight c# tabtitle="C#" %}
//Creates a new Word document
WordDocument document = new WordDocument();
//Adds new section to the document 
WSection section = document.AddSection() as WSection;
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph() as WParagraph;
//Appends text to the paragraph
paragraph.AppendText("Sample for applying document background");
//Sets the background type as picture
document.Background.Type = BackgroundType.Picture;
document.Background.Picture = Image.FromFile("Image.png");
//Saves the document
document.Save("Sample.docx", FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Creates a new Word document
Dim document As New WordDocument()
'Adds new section to document
Dim section As WSection = TryCast(document.AddSection(), WSection)
'Adds new paragraph to the section
Dim paragraph As IWParagraph = TryCast(section.AddParagraph(), WParagraph)
'Appends text to the paragraph
paragraph.AppendText("Sample for applying document background")
'Sets the background type as picture
document.Background.Type = BackgroundType.Picture
document.Background.Picture = Image.FromFile("Image.png")
'Saves the document
document.Save("Sample.docx", FormatType.Docx)
'Closes the document
document.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
using (WordDocument document = new WordDocument(assembly.GetManifestResourceStream("CreateWordSample.Assets.Test.docx"), FormatType.Docx))
{
	document.Background.Type = BackgroundType.Picture;
	//Opens the existing image 
	Stream imageStream = assembly.GetManifestResourceStream("CreateWordSample.Assets.Picture.png");
	MemoryStream memoryStream = new MemoryStream();
	imageStream.CopyTo(memoryStream);
	document.Background.Picture = memoryStream.ToArray();
	MemoryStream stream = new MemoryStream();
	//Saves the Word file to MemoryStream
	await document.SaveAsync(stream, FormatType.Docx);
	//Saves the stream as Word file in local machine
	Save(stream, "Result.docx");
	//Please refer the below link to save Word document in UWP platform
	//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
	document.Close();
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
FileStream sourceStreamPath = new FileStream(sourceFileName, FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
//Opens an source document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument(sourceStreamPath, FormatType.Automatic))
{
	//Sets the background type as picture
	document.Background.Type = BackgroundType.Picture;
	//Opens the existing image 
	FileStream imageStream = new FileStream(@"Data/Picture.png", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
	MemoryStream memoryStream = new MemoryStream();
	imageStream.CopyTo(memoryStream);
	document.Background.Picture = memoryStream.ToArray();
	MemoryStream stream = new MemoryStream();
	//Saves and closes the destination document to  MemoryStream
	document.Save(stream, FormatType.Docx);
	document.Close(); 
	stream.Position = 0;
	//Download Word document in the browser
	return File(stream, "application/msword", "Result.docx");
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
using (WordDocument document = new WordDocument(assembly.GetManifestResourceStream("XamarinFormsApp1.Assets.Hello World.docx"), FormatType.Docx))
{
	document.Background.Type = BackgroundType.Picture;
	//Opens the existing image 
	Stream imageStream = assembly.GetManifestResourceStream("CreateWordSample.Assets.Picture.png");
	MemoryStream memoryStream = new MemoryStream();
	imageStream.CopyTo(memoryStream);
	document.Background.Picture = memoryStream.ToArray();
	MemoryStream stream = new MemoryStream();
	document.Save(stream, FormatType.Docx);
	//Save the stream as a file in the device and invoke it for viewing
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("WorkingWordDoc.docx", "application/msword", stream);
	//Closes the document              
	document.Close();
	//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
	//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
}
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-document/Apply-picture-background-to-document).

## Hide background in the print layout view

You can show or hide background colors and images in the print layout view of Word document using the `DisplayBackgrounds` API.

The following code example shows how to hide the background in print layout view of Word document.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Load Word document.
using (WordDocument document = new WordDocument(“Input.docx” FormatType.Docx))
{
//Disable a flag to hide the background in print layout view.
document.Settings.DisplayBackgrounds = false;
//Save the Word document.
document.Save(“Sample.docx”), FormatType.Docx);
}

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Load Word document.
Using document As WordDocument = New       WordDocument(“Input.docx"), FormatType.Docx)
'Disable a flag to hide the background in the print layout view. 
document.Settings.DisplayBackgrounds = False
'Save the Word document.
document.Save(“Sample.docx"), FormatType.Docx)
End Using

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable projects.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Open the file as Stream.
using (Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.docx"))
{
    //Load file stream into Word document.
    using (WordDocument document = new WordDocument(docStream, FormatType.Docx))
    {
        //Disable a flag to hide the background in the print layout view.
        document.Settings.DisplayBackgrounds = false;
        //Save the Word document to MemoryStream.
        MemoryStream stream = new MemoryStream();
        await document.SaveAsync(stream, FormatType.Docx);
        //Save the stream as a Word document file on the local machine.
        Save(stream, "Sample.docx");
        //Please refer to the below link to save the Word document in the UWP platform.
        //https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
    }
} 


{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Open the file as Stream.
using (FileStream docStream = new FileStream("Input.docx", FileMode.Open, FileAccess.Read))
{
    //Load file stream into Word document.
    using (WordDocument document = new WordDocument(docStream, FormatType.Docx))
    {
        //Disable a flag to hide the background in the print layout view.
        document.Settings.DisplayBackgrounds = false;
        //Save the Word document to MemoryStream.
        MemoryStream outputStream = new MemoryStream();
        document.Save(outputStream, FormatType.Docx);
        outputStream.Position = 0;
        //Download the Word document in the browser.
        return File(outputStream, "application/msword", "Sample.docx"); 
    }
}

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable projects.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Open the file as Stream.
using (Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.docx"))
{
    //Load the file stream into the Word document.
    using (WordDocument document = new WordDocument(docStream, FormatType.Docx))
    {
        //Disable a flag to hide the background in the print layout view.
        document.Settings.DisplayBackgrounds = false;
        //Save the Word document to MemoryStream.
        MemoryStream outputStream = new MemoryStream();
        document.Save(outputStream, FormatType.Docx);
        //Save the stream as a file in the device and invoke it for viewing.
        Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.docx", "application/msword", outputStream);
        //Please download the helper files from the  link below to save the stream as a file and open the file for viewing on the Xamarin platform
        //https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
    }
}

{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-document/Hide-backgrounds-in-print-layout-view).

## Remove background in a Word document

You can remove background colors and images in an existing Word document by setting `NoBackground` as the background type.

The following code example shows how to remove the background in a Word document:

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Load Word document.
using (WordDocument document = new WordDocument(“Input.docx” FormatType.Docx))
{
    //Remove the existing background in the Word document.
    document.Background.Type = BackgroundType.NoBackground;
    //Save the Word document.
    document.Save(“Sample.docx”), FormatType.Docx);
}

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Load Word document.
Using document As WordDocument = New WordDocument(“Input.docx"), FormatType.Docx)
    'Remove the existing background in the Word document.
    document.Background.Type = BackgroundType.NoBackground;
    'Save the Word document.
    document.Save(“Sample.docx"), FormatType.Docx)
End Using

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable projects.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Open the file as Stream.
using (Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.docx"))
{
    //Load file stream into Word document.
    using (WordDocument document = new WordDocument(docStream, FormatType.Docx))
    {
        //Remove the existing background in the Word document.
        document.Background.Type = BackgroundType.NoBackground;
        //Save the Word document to MemoryStream.
        MemoryStream stream = new MemoryStream();
        await document.SaveAsync(stream, FormatType.Docx);
        //Save the stream as a Word document file on the local machine.
        Save(stream, "Sample.docx");
        //Please refer to the link below to save a Word document in the UWP platform
        //https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
    }
} 

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Open the file as Stream.
using (FileStream docStream = new FileStream("Input.docx", FileMode.Open, FileAccess.Read))
{
    //Load the file stream into the Word document.
    using (WordDocument document = new WordDocument(docStream, FormatType.Docx))
    {
        //Remove the existing background in the Word document.
        document.Background.Type = BackgroundType.NoBackground;
        //Save the Word document to MemoryStream.
        MemoryStream outputStream = new MemoryStream();
        document.Save(outputStream, FormatType.Docx);
        outputStream.Position = 0;
        //Download the Word document in the browser.
        return File(outputStream, "application/msword", "Sample.docx"); 
    }
}

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable projects.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Open the file as Stream.
using (Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.docx"))
{
    //Load the file stream into the Word document.
    using (WordDocument document = new WordDocument(docStream, FormatType.Docx))
    {
        //Remove the existing background in the Word document.
        document.Background.Type = BackgroundType.NoBackground;
        //Save the Word document to MemoryStream.
        MemoryStream outputStream = new MemoryStream();
        document.Save(outputStream, FormatType.Docx);
        //Save the stream as a file in the device and invoke it for viewing.
        Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.docx", "application/msword", outputStream);
        //Please download the helper files from the link below to save the stream as a file and open the file for viewing on the Xamarin platform
        //https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
    }
}

{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-document/Remove-background-in-Word-document).


## Working with Alternate chunks

Updating Alternate chunk in the Word document, imports the content from the embedded alternate chunk into the main document. When saving the Word document containing alternate chunk as DOCX format document, the alternate chunk content preserved by default. But, when saving as DOC format or other formats, the alternate chunk content will not be preserved. You can use [UpdateAlternateChunks](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WordDocument.html#Syncfusion_DocIO_DLS_WordDocument_UpdateAlternateChunks) method to preserve the alternate chunk content by importing into the main document.

The following examples show how to update the alternate chunk in the word document.
{% tabs %} 
{% highlight c# tabtitle="C#" %}
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument("Sample.docx", FormatType.Docx))
{
    //Update the alternate chunks in the document
    document.UpdateAlternateChunks();
    //Saves and closes the document instance
    document.Save("Result.doc");               
}
{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET" %}
'Opens an existing document from file system through constructor of WordDocument class
Using document As WordDocument = New WordDocument("Sample.docx", FormatType.Docx)
    'Update the alternate chunks in the document
    document.UpdateAlternateChunks()
    'Saves and closes the document instance
    document.Save("Result.doc")
End Using	
{% endhighlight %}
{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
using (WordDocument document = new WordDocument(assembly.GetManifestResourceStream("CreateWordSample.Assets.Sample.docx"), FormatType.Docx))
{
    //Update the alternate chunks in the document
    document.UpdateAlternateChunks()
    MemoryStream stream = new MemoryStream();
    //Saves the Word file to MemoryStream
    await document.SaveAsync(stream, FormatType.Docx);
    //Saves the stream as Word file in local machine
    Save(stream, "Result.doc");
    //Please refer the below link to save Word document in UWP platform
    //https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
}
{% endhighlight %}
{% highlight c# tabtitle="ASP.NET Core" %}
FileStream fileStream = new FileStream("Sample.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument(fileStream, FormatType.Docx))
{    
    //Update the alternate chunks in the document
    document.UpdateAlternateChunks();
    MemoryStream stream = new MemoryStream();
    //Saves and closes the document instance
    document.Save(stream, FormatType.Doc);
    stream.Position = 0;
    fileStream.Dispose();
    //Download Word document in the browser
    return File(stream, "application/msword", "Result.doc");
}
{% endhighlight %}
{% highlight c# tabtitle="Xamarin" %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument((assembly.GetManifestResourceStream("XamarinFormsApp.Assets.Sample.docx")), FormatType.Docx))
{
    //Update the alternate chunks in the document
    document.UpdateAlternateChunks();
    MemoryStream stream = new MemoryStream();
    document.Save(stream, FormatType.Doc);
    //Save the stream as a file in the device and invoke it for viewing
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.doc", "application/msword", stream);
    //Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
    //https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
}
{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-document/Update-alternate-chunks).

## See Also

* [Iterating Word document elements](https://help.syncfusion.com/file-formats/docio/word-document/iterating-word-document-elements)
* [Merging Word documents](https://help.syncfusion.com/file-formats/docio/word-document/merging-word-documents)
* [Print Word documents](https://help.syncfusion.com/file-formats/docio/word-document/print-word-documents)
* [Split Word documents](https://help.syncfusion.com/file-formats/docio/word-document/split-word-documents)
* [Why it is not possible to access the Word document contents page by page](https://www.syncfusion.com/kb/3989/why-it-is-not-possible-to-access-the-word-document-contents-page-by-page)