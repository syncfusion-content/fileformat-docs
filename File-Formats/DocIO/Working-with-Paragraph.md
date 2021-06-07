---
title: Working with Paragraph | Syncfusion
description: This section explains how to work with the child elements of Paragraph in Word document using Syncfusion Word library (Essential DocIO) 
platform: file-formats
control: DocIO
documentation: UG
---
# Working with Paragraph

Paragraph is the basic element in a Word document that contains a textual and graphical contents. Each paragraph has its own formatting such as line spacing, alignment, indentation, and more. Within a paragraph, the contents are represented by one or more child elements such as `WTextRange`, `WPicture`, and `Hyperlink` and more. The `ParagraphItem` is the base class for the child elements of paragraph. The following elements can be the child elements of a paragraph:

* Text: Represented by an instance of `WTextRange`.
* Image: Represented by an instance of `WPicture`. 
* Comments: Represented by an instance of `WComment`.
* Hyperlink: Represented by an instance of `Hyperlink`. 
* Symbols: Represented by an instance of `WSymbol`. 
* Breaks: Represented by an instance of `Break`. 
* OLE Object: Represented by an instance of `WOleObject`. 
* Shapes:  Represented by an instance of `Shape`. 
* TextBox: Represented by an instance of `WTextBox`. 
* Chart: Represented by an instance of `WChart`.
* Fields: Represented by an instance of `WField`.
* Form Fields: Represented by an instance of `WFormField`.
* Bookmarks: Represented by instances of `BookmarkStart` and `BookmarkEnd`. 
* Absolute Tab: Represented by an instance of `WAbsoluteTab`.
* Footnotes and Endnotes: Represented by an instance of `WFootnote`.

The following code example explains how to add a new paragraph.

{% tabs %}  

{% highlight c# %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Adds new text to the paragraph
paragraph.AppendText("Adding new paragraph to the document");
//Saves the Word document
document.Save("Sample.docx", FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Creates a new Word document 
Dim document As New WordDocument()
'Adds new section to the document
Dim section As IWSection = document.AddSection()
'Adds new paragraph to the section
Dim paragraph As IWParagraph = section.AddParagraph()
'Adds new text to the paragraph
paragraph.AppendText("Adding new paragraph to the document")
'Saves the Word document
document.Save("Sample.docx", FormatType.Docx)
'Closes the document
document.Close()
{% endhighlight %}

{% highlight UWP %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Adds new text to the paragraph
paragraph.AppendText("Adding new paragraph to the document");
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Refer to the following link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight ASP.NET CORE %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Adds new text to the paragraph
paragraph.AppendText("Adding new paragraph to the document");
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %} 

{% highlight XAMARIN %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Adds new text to the paragraph
paragraph.AppendText("Adding new paragraph to the document");
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Download the helper files from the following link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %} 

{% endtabs %}  

The following code example illustrates how to modify an existing paragraph.

{% tabs %}  

{% highlight c# %}
//Loads the template document
WordDocument document = new WordDocument("Template.docx");
//Gets the text body of first section
WTextBody textBody = document.Sections[0].Body;
//Gets the paragraph at index 1
WParagraph paragraph = textBody.Paragraphs[1];
//Iterates through the child elements of paragraph
foreach (ParagraphItem item in paragraph.ChildEntities)
{
    if (item is WTextRange)
    {
        WTextRange text = item as WTextRange;
        //Modifies the character format of the text
        text.CharacterFormat.Bold = true;
        break;
    }
}
//Saves the Word document
document.Save("Sample.docx", FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Loads the template document
Dim document As New WordDocument("Template.docx")
'Gets the text body of first section
Dim textBody As WTextBody = document.Sections(0).Body
'Gets the paragraph at index 1
Dim paragraph As WParagraph = textBody.Paragraphs(1)
'Iterates through the child elements of paragraph
For Each item As ParagraphItem In paragraph.ChildEntities
	If TypeOf item Is WTextRange Then
		Dim text As WTextRange = TryCast(item, WTextRange)
		'Modifies the character format of the text
		text.CharacterFormat.Bold = True
		Exit For
	End If
Next
'Saves the Word document
document.Save("Sample.docx", FormatType.Docx)
'Closes the document
document.Close()
{% endhighlight %}

{% highlight UWP %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream fileStream = assembly.GetManifestResourceStream("CreateWordSample.Assets.Template.docx");
//Loads the template document
WordDocument document = new WordDocument(fileStream);
//Gets the text body of first section
WTextBody textBody = document.Sections[0].Body;
//Gets the paragraph at index 1
WParagraph paragraph = textBody.Paragraphs[1];
//Iterates through the child elements of paragraph
foreach (ParagraphItem item in paragraph.ChildEntities)
{
    if (item is WTextRange)
    {
        WTextRange text = item as WTextRange;
        //Modifies the character format of the text
        text.CharacterFormat.Bold = true;
        break;
    }
}
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight ASP.NET CORE %}
FileStream fileStream = new FileStream(@"Test.docx", FileMode.Open, FileAccess.ReadWrite);
//Loads the template document
WordDocument document = new WordDocument(fileStream, FormatType.Automatic);
//Gets the text body of first section
WTextBody textBody = document.Sections[0].Body;
//Gets the paragraph at index 1
WParagraph paragraph = textBody.Paragraphs[1];
//Iterates through the child elements of paragraph
foreach (ParagraphItem item in paragraph.ChildEntities)
{
    if (item is WTextRange)
    {
        WTextRange text = item as WTextRange;
        //Modifies the character format of the text
        text.CharacterFormat.Bold = true;
        break;
    }
}
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %} 

{% highlight XAMARIN %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream fileStream = assembly.GetManifestResourceStream("CreateWordSample.Assets.Template.docx");
//Loads the template document
WordDocument document = new WordDocument(fileStream, FormatType.Automatic);
//Gets the text body of first section
WTextBody textBody = document.Sections[0].Body;
//Gets the paragraph at index 1
WParagraph paragraph = textBody.Paragraphs[1];
//Iterates through the child elements of paragraph
foreach (ParagraphItem item in paragraph.ChildEntities)
{
    if (item is WTextRange)
    {
        WTextRange text = item as WTextRange;
        //Modifies the character format of the text
        text.CharacterFormat.Bold = true;
        break;
    }
}
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Download the helper files from the following link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %} 

{% endtabs %}  

## Applying paragraph formatting

As in the Microsoft Word, DocIO provides support for all the paragraph formatting options such as line spacing, indentation, spacing before and after, keep follow, and more. The following code example explains how to apply formatting to a paragraph.

N>The `FirstLineIndent` can be used to update or retrieve both hanging and first line indents. Negative value for this property denotes the hanging indent and positive value denotes the first line indent of the paragraph.

{% tabs %} 

{% highlight c# %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Adds new text to the paragraph
IWTextRange firstText = paragraph.AppendText("Paragraphs are the basic elements of the Word document. It can contain text and images.");
//Applies paragraph formatting
paragraph.ParagraphFormat.AfterSpacing = 18f;
paragraph.ParagraphFormat.BeforeSpacing = 18f;
paragraph.ParagraphFormat.BackColor = Color.LightGray;
paragraph.ParagraphFormat.FirstLineIndent = 10f;
paragraph.ParagraphFormat.LineSpacing = 10f;
paragraph.ParagraphFormat.HorizontalAlignment = HorizontalAlignment.Right;
//Saves the Word document
document.Save("Sample.docx", FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Creates a new Word document 
Dim document As New WordDocument()
'Adds new section to the document
Dim section As IWSection = document.AddSection()
'Adds new paragraph to the section
Dim paragraph As IWParagraph = section.AddParagraph()
'Adds new text to the paragraph
Dim firstText As IWTextRange = paragraph.AppendText("Paragraphs are the basic elements of the Word document. It can contain text and images.")
'Applies paragraph formatting
paragraph.ParagraphFormat.AfterSpacing = 18.0F
paragraph.ParagraphFormat.BeforeSpacing = 18.0F
paragraph.ParagraphFormat.BackColor = Color.LightGray
paragraph.ParagraphFormat.FirstLineIndent = 10.0F
paragraph.ParagraphFormat.LineSpacing = 10.0F
paragraph.ParagraphFormat.HorizontalAlignment = HorizontalAlignment.Right
'Saves the Word document
document.Save("Sample.docx", FormatType.Docx)
'Closes the document
document.Close()
{% endhighlight %}   

{% highlight UWP %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Adds new text to the paragraph
IWTextRange firstText = paragraph.AppendText("Paragraphs are the basic elements of the Word document. It can contain text and images.");
//Applies paragraph formatting
paragraph.ParagraphFormat.AfterSpacing = 18f;
paragraph.ParagraphFormat.BeforeSpacing = 18f;
paragraph.ParagraphFormat.BackColor = Color.LightGray;
paragraph.ParagraphFormat.FirstLineIndent = 10f;
paragraph.ParagraphFormat.LineSpacing = 10f;
paragraph.ParagraphFormat.HorizontalAlignment = Syncfusion.DocIO.DLS.HorizontalAlignment.Right;
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Refer to the following link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight ASP.NET CORE %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Adds new text to the paragraph
IWTextRange firstText = paragraph.AppendText("Paragraphs are the basic elements of the Word document. It can contain text and images.");
//Applies paragraph formatting
paragraph.ParagraphFormat.AfterSpacing = 18f;
paragraph.ParagraphFormat.BeforeSpacing = 18f;
paragraph.ParagraphFormat.BackColor = Color.LightGray;
paragraph.ParagraphFormat.FirstLineIndent = 10f;
paragraph.ParagraphFormat.LineSpacing = 10f;
paragraph.ParagraphFormat.HorizontalAlignment = Syncfusion.DocIO.DLS.HorizontalAlignment.Right;
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %} 

{% highlight XAMARIN %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Adds new text to the paragraph
IWTextRange firstText = paragraph.AppendText("Paragraphs are the basic elements of the Word document. It can contain text and images.");
//Applies paragraph formatting
paragraph.ParagraphFormat.AfterSpacing = 18f;
paragraph.ParagraphFormat.BeforeSpacing = 18f;
paragraph.ParagraphFormat.BackColor = Syncfusion.Drawing.Color.LightGray;
paragraph.ParagraphFormat.FirstLineIndent = 10f;
paragraph.ParagraphFormat.LineSpacing = 10f;
paragraph.ParagraphFormat.HorizontalAlignment = Syncfusion.DocIO.DLS.HorizontalAlignment.Right;
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Download the helper files from the following link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %} 

{% endtabs %}

### Paragraph style  

Paragraph style contains definition for both font (text) and paragraph formatting that can be applied to the contents of an entire paragraph. DocIO supports various pre-defined styles and also provides ability to create custom paragraph styles.

T> You can define a custom style or modify any built-in style to the required formatting, and apply this style to the part of Word document to be formatted. You can reduce the file size and code length by using styles instead of formatting each element explicitly.

The following code example explains how to use the predefined styles.

{% tabs %}  

{% highlight c# %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph firstParagraph = section.AddParagraph();
//Adds new text to the paragraph
IWTextRange firstText = firstParagraph.AppendText("Built-in styles can be applied to the paragraph. Heading1 style is applied to this paragraph.");
//Applies built-in style for the paragraph
firstParagraph.ApplyStyle(BuiltinStyle.Heading1);
//Saves the Word document
document.Save("Sample.docx", FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Creates a new Word document 
Dim document As New WordDocument()
'Adds new section to the document
Dim section As IWSection = document.AddSection()
'Adds new paragraph to the section
Dim firstParagraph As IWParagraph = section.AddParagraph()
'Adds new text to the paragraph
Dim firstText As IWTextRange = firstParagraph.AppendText("Built-in styles can be applied to the paragraph. Heading1 style is applied to this paragraph.")
'Applies built-in style for the paragraph
firstParagraph.ApplyStyle(BuiltinStyle.Heading1)
'Saves the Word document
document.Save("Sample.docx", FormatType.Docx)
'Closes the document
document.Close()
{% endhighlight %}

{% highlight UWP %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph firstParagraph = section.AddParagraph();
//Adds new text to the paragraph
IWTextRange firstText = firstParagraph.AppendText("Built-in styles can be applied to the paragraph. Heading1 style is applied to this paragraph.");
//Applies built-in style for the paragraph
firstParagraph.ApplyStyle(BuiltinStyle.Heading1);
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Refer to the following link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight ASP.NET CORE %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph firstParagraph = section.AddParagraph();
//Adds new text to the paragraph
IWTextRange firstText = firstParagraph.AppendText("Built-in styles can be applied to the paragraph. Heading1 style is applied to this paragraph.");
//Applies built-in style for the paragraph
firstParagraph.ApplyStyle(BuiltinStyle.Heading1);
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %} 

{% highlight XAMARIN %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph firstParagraph = section.AddParagraph();
//Adds new text to the paragraph
IWTextRange firstText = firstParagraph.AppendText("Built-in styles can be applied to the paragraph. Heading1 style is applied to this paragraph.");
//Applies built-in style for the paragraph
firstParagraph.ApplyStyle(BuiltinStyle.Heading1);
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Download the helper files from the following link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %} 

{% endtabs %}

### Custom paragraph style  

The following code example explains how to create a custom paragraph style and apply it to a paragraph.

{% tabs %} 

{% highlight c# %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Creates user defined style
IWParagraphStyle style = document.AddParagraphStyle("User_defined_style");
style.ParagraphFormat.BackColor = Color.LightGray;
style.ParagraphFormat.AfterSpacing = 18f;
style.ParagraphFormat.BeforeSpacing = 18f;
style.ParagraphFormat.Borders.BorderType = Syncfusion.DocIO.DLS.BorderStyle.DotDash;
style.ParagraphFormat.Borders.LineWidth = 0.5f;
style.ParagraphFormat.LineSpacing = 15f;
style.CharacterFormat.FontName = "Calibri";
style.CharacterFormat.Italic = true;
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
IWTextRange text = paragraph.AppendText("A new paragraph style is created and is applied to this paragraph.");
//Applies the new style to paragraph
paragraph.ApplyStyle("User_defined_style");
//Saves the Word document
document.Save("Sample.docx", FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Creates a new Word document 
Dim document As New WordDocument()
'Adds new section to the document
Dim section As IWSection = document.AddSection()
'Creates user defined style
Dim style As IWParagraphStyle = document.AddParagraphStyle("User_defined_style")
style.ParagraphFormat.BackColor = Color.LightGray
style.ParagraphFormat.AfterSpacing = 18.0F
style.ParagraphFormat.BeforeSpacing = 18.0F
style.ParagraphFormat.Borders.BorderType = Syncfusion.DocIO.DLS.BorderStyle.DotDash
style.ParagraphFormat.Borders.LineWidth = 0.5F
style.ParagraphFormat.LineSpacing = 15.0F
style.CharacterFormat.FontName = "Calibri"
style.CharacterFormat.Italic = True
'Adds new paragraph to the section
Dim paragraph As IWParagraph = section.AddParagraph()
Dim text As IWTextRange = paragraph.AppendText("A new paragraph style is created and is applied to this paragraph.")
'Applies the new style to paragraph
paragraph.ApplyStyle("User_defined_style")
'Saves the Word document
document.Save("Sample.docx", FormatType.Docx)
'Closes the document
document.Close()
{% endhighlight %} 

{% highlight UWP %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Creates user defined style
IWParagraphStyle style = document.AddParagraphStyle("User_defined_style");
style.ParagraphFormat.BackColor = Color.LightGray;
style.ParagraphFormat.AfterSpacing = 18f;
style.ParagraphFormat.BeforeSpacing = 18f;
style.ParagraphFormat.Borders.BorderType = Syncfusion.DocIO.DLS.BorderStyle.DotDash;
style.ParagraphFormat.Borders.LineWidth = 0.5f;
style.ParagraphFormat.LineSpacing = 15f;
style.CharacterFormat.FontName = "Calibri";
style.CharacterFormat.Italic = true;
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
IWTextRange text = paragraph.AppendText("A new paragraph style is created and is applied to this paragraph.");
//Applies the new style to paragraph
paragraph.ApplyStyle("User_defined_style");
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Refer to the following link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight ASP.NET CORE %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Creates user defined style
IWParagraphStyle style = document.AddParagraphStyle("User_defined_style");
style.ParagraphFormat.BackColor = Color.LightGray;
style.ParagraphFormat.AfterSpacing = 18f;
style.ParagraphFormat.BeforeSpacing = 18f;
style.ParagraphFormat.Borders.BorderType = Syncfusion.DocIO.DLS.BorderStyle.DotDash;
style.ParagraphFormat.Borders.LineWidth = 0.5f;
style.ParagraphFormat.LineSpacing = 15f;
style.CharacterFormat.FontName = "Calibri";
style.CharacterFormat.Italic = true;
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
IWTextRange text = paragraph.AppendText("A new paragraph style is created and is applied to this paragraph.");
//Applies the new style to paragraph
paragraph.ApplyStyle("User_defined_style");
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %} 

{% highlight XAMARIN %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Creates user defined style
IWParagraphStyle style = document.AddParagraphStyle("User_defined_style");
style.ParagraphFormat.BackColor = Syncfusion.Drawing.Color.LightGray;
style.ParagraphFormat.AfterSpacing = 18f;
style.ParagraphFormat.BeforeSpacing = 18f;
style.ParagraphFormat.Borders.BorderType = Syncfusion.DocIO.DLS.BorderStyle.DotDash;
style.ParagraphFormat.Borders.LineWidth = 0.5f;
style.ParagraphFormat.LineSpacing = 15f;
style.CharacterFormat.FontName = "Calibri";
style.CharacterFormat.Italic = true;
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
IWTextRange text = paragraph.AppendText("A new paragraph style is created and is applied to this paragraph.");
//Applies the new style to paragraph
paragraph.ApplyStyle("User_defined_style");
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Download the helper files from the following link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %} 

{% endtabs %}

### Tab stop  

A tab stop is a horizontal position that is set for aligning text of the paragraph.  A tab character causes the carriage to go to the next tab stop.

Each paragraph has its own tab stop collection where the new tab stop can be added and existing tab stop can be removed.

The following code example explains how to add tab stops to the paragraph.

{% tabs %}  

{% highlight c# %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Adds tab stop at position 11
Tab firstTab = paragraph.ParagraphFormat.Tabs.AddTab(11, TabJustification.Left, TabLeader.Dotted);            
//Adds tab stop at position 62
paragraph.ParagraphFormat.Tabs.AddTab(62, TabJustification.Left, TabLeader.Single);
paragraph.AppendText("This sample\t illustrates the use of tabs in the paragraph. Tabs\t can be inserted or removed from the paragraph.");
//Removes tab stop from the collection
paragraph.ParagraphFormat.Tabs.RemoveByTabPosition(11);
//Saves the Word document
document.Save("Sample.docx", FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Creates a new Word document 
Dim document As New WordDocument()
'Adds new section to the document
Dim section As IWSection = document.AddSection()
'Adds new paragraph to the section
Dim paragraph As IWParagraph = section.AddParagraph()
'Adds tab stop at position 11
Dim firstTab As Tab = paragraph.ParagraphFormat.Tabs.AddTab(11, TabJustification.Left, TabLeader.Dotted)
'Adds tab stop at position 62
paragraph.ParagraphFormat.Tabs.AddTab(62, TabJustification.Left, TabLeader.[Single])
paragraph.AppendText("This sample" & vbTab & " illustrates the use of tabs in the paragraph. Tabs" & vbTab & " can be inserted or removed from the paragraph.")
'Removes tab stop from the collection
paragraph.ParagraphFormat.Tabs.RemoveByTabPosition(11)
'Saves the Word document
document.Save("Sample.docx", FormatType.Docx)
'Closes the document
document.Close()
{% endhighlight %}  

{% highlight UWP %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Adds tab stop at position 11
Tab firstTab = paragraph.ParagraphFormat.Tabs.AddTab(11, TabJustification.Left, TabLeader.Dotted);
//Adds tab stop at position 62
paragraph.ParagraphFormat.Tabs.AddTab(62, TabJustification.Left, TabLeader.Single);
paragraph.AppendText("This sample\t illustrates the use of tabs in the paragraph. Tabs\t can be inserted or removed from the paragraph.");
//Removes tab stop from the collection
paragraph.ParagraphFormat.Tabs.RemoveByTabPosition(11);
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Refer to the following link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight ASP.NET CORE %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Adds tab stop at position 11
Tab firstTab = paragraph.ParagraphFormat.Tabs.AddTab(11, TabJustification.Left, TabLeader.Dotted);
//Adds tab stop at position 62
paragraph.ParagraphFormat.Tabs.AddTab(62, TabJustification.Left, TabLeader.Single);
paragraph.AppendText("This sample\t illustrates the use of tabs in the paragraph. Tabs\t can be inserted or removed from the paragraph.");
//Removes tab stop from the collection
paragraph.ParagraphFormat.Tabs.RemoveByTabPosition(11);
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %} 

{% highlight XAMARIN %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Adds tab stop at position 11
Tab firstTab = paragraph.ParagraphFormat.Tabs.AddTab(11, TabJustification.Left, TabLeader.Dotted);
//Adds tab stop at position 62
paragraph.ParagraphFormat.Tabs.AddTab(62, TabJustification.Left, TabLeader.Single);
paragraph.AppendText("This sample\t illustrates the use of tabs in the paragraph. Tabs\t can be inserted or removed from the paragraph.");
//Removes tab stop from the collection
paragraph.ParagraphFormat.Tabs.RemoveByTabPosition(11);
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Download the helper files from the following link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %} 

{% endtabs %}

### RTL paragraph

You can set RTL (Right-to-left) direction to the paragraph in a Word document. The following code example shows how to set RTL (Right-to-left) for a paragraph in Word document.

{% tabs %}  

{% highlight C# %}
//Loads the template document
WordDocument document = new WordDocument("Template.docx");
//Gets the text body of first section
WTextBody textBody = document.Sections[0].Body;
//Gets the paragraph at index 1
WParagraph paragraph = textBody.Paragraphs[1];
//Gets a value indicating whether the paragraph is right-to-left. True indicates the paragraph direction is RTL
bool isRTL = paragraph.ParagraphFormat.Bidi;
//Sets RTL direction for a paragraph
if(!isRTL)
    paragraph.ParagraphFormat.Bidi = true;
//Saves the Word document
document.Save("Sample.docx", FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight VB.NET %}
'Loads the template document
Dim document As WordDocument = New WordDocument("Template.docx")
'Gets the text body of first section
Dim textBody As WTextBody = document.Sections(0).Body
'Gets the paragraph at index 1
Dim paragraph As WParagraph = textBody.Paragraphs(1)
'Gets a value indicating whether the paragraph is right-to-left. True indicates the paragraph direction is RTL
Dim isRTL As Boolean = paragraph.ParagraphFormat.Bidi
'Sets RTL direction for a paragraph
If Not isRTL Then
    paragraph.ParagraphFormat.Bidi = True
End If
'Saves the Word document
document.Save("Sample.docx", FormatType.Docx)
'Closes the document
document.Close()
{% endhighlight %}

{% highlight UWP %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Loads the template document
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Docx);
//Gets the text body of first section
WTextBody textBody = document.Sections[0].Body;
//Gets the paragraph at index 1
WParagraph paragraph = textBody.Paragraphs[1];
//Gets a value indicating whether the paragraph is right-to-left. True indicates the paragraph direction is RTL
bool isRTL = paragraph.ParagraphFormat.Bidi;
//Sets RTL direction for a paragraph
if(!isRTL)
    paragraph.ParagraphFormat.Bidi = true;
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Sample.docx");

//Refer to the following link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight ASP.NET CORE %}
FileStream fileStreamPath = new FileStream("Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
//Loads or opens an existing Word document through Open method of WordDocument class
WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);
//Gets the text body of first section
WTextBody textBody = document.Sections[0].Body;
//Gets the paragraph at index 1
WParagraph paragraph = textBody.Paragraphs[1];
//Gets a value indicating whether the paragraph is right-to-left. True indicates the paragraph direction is RTL
bool isRTL = paragraph.ParagraphFormat.Bidi;
//Sets RTL direction for a paragraph
if(!isRTL)
    paragraph.ParagraphFormat.Bidi = true;
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word document to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Sample.docx");
{% endhighlight %} 

{% highlight XAMARIN %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Loads or opens an existing Word document through Open method of WordDocument class
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Docx);
//Gets the text body of first section
WTextBody textBody = document.Sections[0].Body;
//Gets the paragraph at index 1
WParagraph paragraph = textBody.Paragraphs[1];
//Gets a value indicating whether the paragraph is right-to-left. True indicates the paragraph direction is RTL
bool isRTL = paragraph.ParagraphFormat.Bidi;
//Sets RTL direction for a paragraph
if(!isRTL)
    paragraph.ParagraphFormat.Bidi = true;
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.docx", "application/msword", stream);

//Download the helper files from the following link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}   

## Working with text 

Text within a paragraph is represented by one or more instances of the `WTextRange`. Each `WTextRange` instance can have its own font (text) formatting.  

The following code example explains how to append text to the paragraph.

{% tabs %} 

{% highlight c# %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph firstParagraph = section.AddParagraph();
//Adds new text to the paragraph
IWTextRange firstText = firstParagraph.AppendText("A new text is added to the paragraph.");
firstText.CharacterFormat.FontSize = 14;
firstText.CharacterFormat.Bold = true;
firstText.CharacterFormat.TextColor = Color.Green;
//Saves the Word document
document.Save("Sample.docx", FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Creates a new Word document 
Dim document As New WordDocument()
'Adds new section to the document
Dim section As IWSection = document.AddSection()
'Adds new paragraph to the section
Dim firstParagraph As IWParagraph = section.AddParagraph()
'Adds new text to the paragraph
Dim text As IWTextRange = firstParagraph.AppendText("A new text is added to the paragraph.")
text.CharacterFormat.FontSize = 14
text.CharacterFormat.Bold = True
text.CharacterFormat.TextColor = Color.Green
'Saves the Word document
document.Save("Sample.docx", FormatType.Docx)
'Closes the document
document.Close()
{% endhighlight %}

{% highlight UWP %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph firstParagraph = section.AddParagraph();
//Adds new text to the paragraph
IWTextRange firstText = firstParagraph.AppendText("A new text is added to the paragraph.");
firstText.CharacterFormat.FontSize = 14;
firstText.CharacterFormat.Bold = true;
firstText.CharacterFormat.TextColor = Color.Green;
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Refer to the following link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight ASP.NET CORE %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph firstParagraph = section.AddParagraph();
//Adds new text to the paragraph
IWTextRange firstText = firstParagraph.AppendText("A new text is added to the paragraph.");
firstText.CharacterFormat.FontSize = 14;
firstText.CharacterFormat.Bold = true;
firstText.CharacterFormat.TextColor = Color.Green;
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %} 

{% highlight XAMARIN %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph firstParagraph = section.AddParagraph();
//Adds new text to the paragraph
IWTextRange firstText = firstParagraph.AppendText("A new text is added to the paragraph.");
firstText.CharacterFormat.FontSize = 14;
firstText.CharacterFormat.Bold = true;
firstText.CharacterFormat.TextColor = Syncfusion.Drawing.Color.Green;
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Download the helper files from the following link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %} 

{% endtabs %}  

Text in the paragraph can be modified or replaced with a new text. This can be achieved by iterating through the paragraph items.

The following code example explains how to replace the text of a text range.

{% tabs %} 

{% highlight c# %}
//Loads the template document 
WordDocument document = new WordDocument("Template.docx");
//Gets the last paragraph
WParagraph lastParagraph = document.LastParagraph;
//Iterates through the paragraph items to get the text range and modifies its content.
for (int i = 0; i < lastParagraph.ChildEntities.Count; i++)
{
    if (lastParagraph.ChildEntities[i] is WTextRange)
    {
        WTextRange textRange = lastParagraph.ChildEntities[i] as WTextRange;
        textRange.Text = "First text range of the last paragraph is replaced";
        textRange.CharacterFormat.FontSize = 14;
        break;
    }
}
//Saves the Word document
document.Save("Sample.docx", FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Loads the template document 
Dim document As New WordDocument("Template.docx")
'Gets the last paragraph
Dim lastParagraph As WParagraph = document.LastParagraph
'Iterates through the paragraph items to get the text range and modifies its content
For i As Integer = 0 To lastParagraph.ChildEntities.Count - 1
	If TypeOf lastParagraph.ChildEntities(i) Is WTextRange Then
		Dim textRange As WTextRange = TryCast(lastParagraph.ChildEntities(i), WTextRange)
		textRange.Text = "First text range of the last paragraph is replaced"
		textRange.CharacterFormat.FontSize = 14
		Exit For
	End If
Next
'Saves the Word document
document.Save("Sample.docx", FormatType.Docx)
'Closes the document
document.Close()
{% endhighlight %}

{% highlight UWP %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream FileStream = assembly.GetManifestResourceStream("CreateWordSample.Assets.Template.docx");
//Loads the template document 
WordDocument document = new WordDocument(FileStream);
//Gets the last paragraph
WParagraph lastParagraph = document.LastParagraph;
//Iterates through the paragraph items to get the text range and modifies its content.
for (int i = 0; i < lastParagraph.ChildEntities.Count; i++)
{
    if (lastParagraph.ChildEntities[i] is WTextRange)
    {
        WTextRange textRange = lastParagraph.ChildEntities[i] as WTextRange;
        textRange.Text = "First text range of the last paragraph is replaced";
        textRange.CharacterFormat.FontSize = 14;
        break;
    }
}
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight ASP.NET CORE %}
FileStream fileStream = new FileStream(@"Template.docx", FileMode.Open, FileAccess.ReadWrite);
//Loads the template document 
WordDocument document = new WordDocument(fileStream, FormatType.Automatic);
//Gets the last paragraph
WParagraph lastParagraph = document.LastParagraph;
//Iterates through the paragraph items to get the text range and modifies its content.
for (int i = 0; i < lastParagraph.ChildEntities.Count; i++)
{
    if (lastParagraph.ChildEntities[i] is WTextRange)
    {
        WTextRange textRange = lastParagraph.ChildEntities[i] as WTextRange;
        textRange.Text = "First text range of the last paragraph is replaced";
        textRange.CharacterFormat.FontSize = 14;
        break;
    }
}
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %} 

{% highlight XAMARIN %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream FileStream = assembly.GetManifestResourceStream("CreateWordSample.Assets.Template.docx");
//Loads the template document 
WordDocument document = new WordDocument(FileStream, FormatType.Automatic);
//Gets the last paragraph
WParagraph lastParagraph = document.LastParagraph;
//Iterates through the paragraph items to get the text range and modifies its content.
for (int i = 0; i < lastParagraph.ChildEntities.Count; i++)
{
    if (lastParagraph.ChildEntities[i] is WTextRange)
    {
        WTextRange textRange = lastParagraph.ChildEntities[i] as WTextRange;
        textRange.Text = "First text range of the last paragraph is replaced";
        textRange.CharacterFormat.FontSize = 14;

        break;
    }
}
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Download the helper files from the following link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %} 

{% endtabs %}  

Text formatting enhances the appearance of text in the document. Text formatting includes font size, font color, font name, bold, italic, underline, etc. 

The following code example explains how to apply formatting to the text.

{% tabs %}  

{% highlight c# %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph firstParagraph = section.AddParagraph();
//Adds new text to the paragraph
IWTextRange firstText = firstParagraph.AppendText("This is the first text range. ");
//Applies formatting for first text range
firstText.CharacterFormat.Bold = true;
firstText.CharacterFormat.FontSize = 14;
firstText.CharacterFormat.Shadow = true;
firstText.CharacterFormat.SmallCaps = true;
IWTextRange secondText = firstParagraph.AppendText("This the second text range");
//Applies formatting for second text range
secondText.CharacterFormat.HighlightColor = Color.GreenYellow;
secondText.CharacterFormat.UnderlineStyle = UnderlineStyle.DotDash;
secondText.CharacterFormat.Italic = true;
secondText.CharacterFormat.FontName = "Times New Roman";
secondText.CharacterFormat.TextColor = Color.Green;
//Adds new paragraph to the section
IWParagraph secondParagraph = section.AddParagraph();
//Adds new text to the paragraph
IWTextRange thirdText = secondParagraph.AppendText("שלום עולם");
thirdText.CharacterFormat.Bidi = true;
//Sets language identifier for right to left characters.
thirdText.CharacterFormat.LocaleIdBidi = (short)LocaleIDs.he_IL;
//Saves the Word document
document.Save("Sample.docx", FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Creates a new Word document 
Dim document As New WordDocument()
'Adds new section to the document
Dim section As IWSection = document.AddSection()
'Adds new paragraph to the section
Dim firstParagraph As IWParagraph = section.AddParagraph()
'Adds new text to the paragraph
Dim firstText As IWTextRange = firstParagraph.AppendText("This is the first text range. ")
'Applies formatting for first text range
firstText.CharacterFormat.Bold = True
firstText.CharacterFormat.FontSize = 14
firstText.CharacterFormat.Shadow = True
firstText.CharacterFormat.SmallCaps = True
Dim secondText As IWTextRange = firstParagraph.AppendText("This the second text range")
'Applies formatting for second text range
secondText.CharacterFormat.HighlightColor = Color.GreenYellow
secondText.CharacterFormat.UnderlineStyle = UnderlineStyle.DotDash
secondText.CharacterFormat.Italic = True
secondText.CharacterFormat.FontName = "Times New Roman"
secondText.CharacterFormat.TextColor = Color.Green
'Adds new paragraph to the section
IWParagraph secondParagraph = section.AddParagraph()
'Adds new text to the paragraph
IWTextRange thirdText = secondParagraph.AppendText("שלום עולם")
thirdText.CharacterFormat.Bidi = true
'Sets language identifier for right to left characters.
thirdText.CharacterFormat.LocaleIdBidi = (short)LocaleIDs.he_IL
'Saves the Word document
document.Save("Sample.docx", FormatType.Docx)
'Closes the document
document.Close()
{% endhighlight %}

{% highlight UWP %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph firstParagraph = section.AddParagraph();
//Adds new text to the paragraph
IWTextRange firstText = firstParagraph.AppendText("This is the first text range. ");
//Applies formatting for first text range
firstText.CharacterFormat.Bold = true;
firstText.CharacterFormat.FontSize = 14;
firstText.CharacterFormat.Shadow = true;
firstText.CharacterFormat.SmallCaps = true;
IWTextRange secondText = firstParagraph.AppendText("This the second text range");
//Applies formatting for second text range
secondText.CharacterFormat.HighlightColor = Color.GreenYellow;
secondText.CharacterFormat.UnderlineStyle = UnderlineStyle.DotDash;
secondText.CharacterFormat.Italic = true;
secondText.CharacterFormat.FontName = "Times New Roman";
secondText.CharacterFormat.TextColor = Color.Green;
//Adds new paragraph to the section
IWParagraph secondParagraph = section.AddParagraph();
//Adds new text to the paragraph
IWTextRange thirdText = secondParagraph.AppendText("שלום עולם");
thirdText.CharacterFormat.Bidi = true;
//Sets language identifier for right to left characters.
thirdText.CharacterFormat.LocaleIdBidi = (short)LocaleIDs.he_IL;
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Refer to the following link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight ASP.NET CORE %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph firstParagraph = section.AddParagraph();
//Adds new text to the paragraph
IWTextRange firstText = firstParagraph.AppendText("This is the first text range. ");
//Applies formatting for first text range
firstText.CharacterFormat.Bold = true;
firstText.CharacterFormat.FontSize = 14;
firstText.CharacterFormat.Shadow = true;
firstText.CharacterFormat.SmallCaps = true;
IWTextRange secondText = firstParagraph.AppendText("This the second text range");
//Applies formatting for second text range
secondText.CharacterFormat.HighlightColor = Color.GreenYellow;
secondText.CharacterFormat.UnderlineStyle = UnderlineStyle.DotDash;
secondText.CharacterFormat.Italic = true;
secondText.CharacterFormat.FontName = "Times New Roman";
secondText.CharacterFormat.TextColor = Color.Green;
//Adds new paragraph to the section
IWParagraph secondParagraph = section.AddParagraph();
//Adds new text to the paragraph
IWTextRange thirdText = secondParagraph.AppendText("שלום עולם");
thirdText.CharacterFormat.Bidi = true;
//Sets language identifier for right to left characters.
thirdText.CharacterFormat.LocaleIdBidi = (short)LocaleIDs.he_IL;
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %} 

{% highlight XAMARIN %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph firstParagraph = section.AddParagraph();
//Adds new text to the paragraph
IWTextRange firstText = firstParagraph.AppendText("This is the first text range. ");
//Applies formatting for first text range
firstText.CharacterFormat.Bold = true;
firstText.CharacterFormat.FontSize = 14;
firstText.CharacterFormat.Shadow = true;
firstText.CharacterFormat.SmallCaps = true;
IWTextRange secondText = firstParagraph.AppendText("This the second text range");
//Applies formatting for second text range
secondText.CharacterFormat.HighlightColor = Syncfusion.Drawing.Color.GreenYellow;
secondText.CharacterFormat.UnderlineStyle = Syncfusion.Drawing.UnderlineStyle.DotDash;
secondText.CharacterFormat.Italic = true;
secondText.CharacterFormat.FontName = "Times New Roman";
secondText.CharacterFormat.TextColor = Syncfusion.Drawing.Color.Green;
//Adds new paragraph to the section
IWParagraph secondParagraph = section.AddParagraph();
//Adds new text to the paragraph
IWTextRange thirdText = secondParagraph.AppendText("שלום עולם");
thirdText.CharacterFormat.Bidi = true;
//Sets language identifier for right to left characters.
thirdText.CharacterFormat.LocaleIdBidi = (short)LocaleIDs.he_IL;
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Download the helper files from the following link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %} 

{% endtabs %}  

## Working with Images

DocIO provides support for both inline and absolute positioned images. 

* Inline images: The position of the image is constrained to the lines of text on the page.
* Absolute positioned images: The images can be positioned anywhere irrespective of the lines of text.

The following code example explains how to add image to the paragraph.

{% tabs %}   

{% highlight c# %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph firstParagraph = section.AddParagraph();
//Adds image to  the paragraph
IWPicture picture = firstParagraph.AppendPicture(Image.FromFile("Image.png"));
//Sets height and width for the image
picture.Height = 100;
picture.Width = 100;
//Saves the Word document
document.Save("Sample.docx", FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Creates a new Word document 
Dim document As New WordDocument()
'Adds new section to the document
Dim section As IWSection = document.AddSection()
'Adds new paragraph to the section
Dim firstParagraph As IWParagraph = section.AddParagraph()
'Adds image to  the paragraph
Dim picture As IWPicture = firstParagraph.AppendPicture(Image.FromFile("Image.png"))
'Sets height and width for the image
picture.Height = 100
picture.Width = 100
'Saves the Word document
document.Save("Sample.docx", FormatType.Docx)
'Closes the document
document.Close()
{% endhighlight %} 

{% highlight UWP %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph firstParagraph = section.AddParagraph();
//Adds image to  the paragraph
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream imageStream = assembly.GetManifestResourceStream("CreateWordSample.Assets.Image.png");
IWPicture picture = firstParagraph.AppendPicture(imageStream);
//Sets height and width for the image
picture.Height = 100;
picture.Width = 100;
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Refer to the following link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight ASP.NET CORE %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph firstParagraph = section.AddParagraph();
//Adds image to  the paragraph
FileStream imageStream = new FileStream(@"Image.png", FileMode.Open, FileAccess.ReadWrite);
IWPicture picture = firstParagraph.AppendPicture(imageStream);
//Sets height and width for the image
picture.Height = 100;
picture.Width = 100;
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %} 

{% highlight XAMARIN %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph firstParagraph = section.AddParagraph();
//Adds image to  the paragraph
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream imageStream = assembly.GetManifestResourceStream("CreateWordSample.Assets.Image.png");
IWPicture picture = firstParagraph.AppendPicture(imageStream);
//Sets height and width for the image
picture.Height = 100;
picture.Width = 100;
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Download the helper files from the following link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %} 

{% endtabs %} 

### Replace image

Image present in the document can be replaced with a new image. This can be achieved by iterating through the paragraph items.

The following code example explains how to replace an existing image.

{% tabs %}   

{% highlight c# %}
//Loads the template document
WordDocument document = new WordDocument("Template.docx");
WTextBody textbody = document.Sections[0].Body;
//Iterates through the paragraphs of the textbody
foreach (WParagraph paragraph in textbody.Paragraphs)
{
    //Iterates through the child elements of paragraph
    foreach (ParagraphItem item in paragraph.ChildEntities)
    {
        if (item is WPicture)
        {
            WPicture picture = item as WPicture;
            //Replaces the image
            if (picture.Title == "Bookmark")
                picture.LoadImage(Image.FromFile("Image.png"));
        }
    }
}
//Saves the Word document
document.Save("Sample.docx", FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Loads the template document
Dim document As New WordDocument("Template.docx")
Dim textbody As WTextBody = document.Sections(0).Body
'Iterates through the paragraphs of the textbody
For Each paragraph As WParagraph In textbody.Paragraphs
	'Iterates through the child elements of paragraph
	For Each item As ParagraphItem In paragraph.ChildEntities
		If TypeOf item Is WPicture Then
			Dim picture As WPicture = TryCast(item, WPicture)
			'Replaces the image
			If picture.Title = "Bookmark" Then
				picture.LoadImage(Image.FromFile("Image.png"))
			End If
		End If
	Next
Next
'Saves the Word document
document.Save("Sample.docx", FormatType.Docx)
'Closes the document
document.Close()
{% endhighlight %}

{% highlight UWP %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream fileStream = assembly.GetManifestResourceStream("CreateWordSample.Assets.Template.docx");
//Loads the template document
WordDocument document = new WordDocument(fileStream);
WTextBody textbody = document.Sections[0].Body;
//Iterates through the paragraphs of the textbody
foreach (WParagraph paragraph in textbody.Paragraphs)
{
    //Iterates through the child elements of paragraph
    foreach (ParagraphItem item in paragraph.ChildEntities)
    {
        if (item is WPicture)
        {
            WPicture picture = item as WPicture;
            //Replaces the image
            if (picture.Title == "Bookmark")
            {
                Stream imagestream = assembly.GetManifestResourceStream("CreateWordSample.Assets.Image.png");
                picture.LoadImage(imagestream);
            }
        }
    }
}
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Refer to the following link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight ASP.NET CORE %}
FileStream fileStream = new FileStream(@"Template.docx", FileMode.Open, FileAccess.ReadWrite);
//Loads the template document
WordDocument document = new WordDocument(fileStream, FormatType.Automatic);
WTextBody textbody = document.Sections[0].Body;
//Iterates through the paragraphs of the textbody
foreach (WParagraph paragraph in textbody.Paragraphs)
{
    //Iterates through the child elements of paragraph
    foreach (ParagraphItem item in paragraph.ChildEntities)
    {
        if (item is WPicture)
        {
            WPicture picture = item as WPicture;
            //Replaces the image
            if (picture.Title == "Bookmark")
            {
                FileStream imageStream = new FileStream(@"Image.png", FileMode.Open, FileAccess.ReadWrite);
                picture.LoadImage(imageStream);
            }
        }
    }
}
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %} 

{% highlight XAMARIN %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream fileStream = assembly.GetManifestResourceStream("XamarinFormsApp1.Assets.Template.docx");
//Loads the template document
WordDocument document = new WordDocument(fileStream, FormatType.Automatic);
WTextBody textbody = document.Sections[0].Body;
//Iterates through the paragraphs of the textbody
foreach (WParagraph paragraph in textbody.Paragraphs)
{
    //Iterates through the child elements of paragraph
    foreach (ParagraphItem item in paragraph.ChildEntities)
    {
        if (item is WPicture)
        {
            WPicture picture = item as WPicture;
            //Replaces the image
            if (picture.Title == "Bookmark")
            {
                Stream imageStream = assembly.GetManifestResourceStream("XamarinFormsApp1.Assets.Dummy-Images.jpg");
                picture.LoadImage(imageStream);
            }
        }
    }
}
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Download the helper files from the following link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %} 

{% endtabs %} 

### Remove image

Images can be removed from the document by removing it from the paragraph items. 

The following code example explains how to remove the image from the paragraph items.

{% tabs %} 

{% highlight c# %}
//Loads the template document 
WordDocument document = new WordDocument("Template.docx");
WTextBody textbody = document.Sections[0].Body;
//Iterates through the paragraphs of the textbody
foreach (WParagraph paragraph in textbody.Paragraphs)
{
    //Iterates through the child elements of paragraph
    for (int i = 0; i < paragraph.ChildEntities.Count; i++)
    {
        //Removes images from the paragraph
        if (paragraph.ChildEntities[i] is WPicture)
        {
            paragraph.Items.RemoveAt(i);
            i--;
        }
    }
}
//Saves the Word document
document.Save("Sample.docx", FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Loads the template document 
Dim document As New WordDocument("Template.docx")
Dim textbody As WTextBody = document.Sections(0).Body
'Iterates through the paragraphs of the textbody
For Each paragraph As WParagraph In textbody.Paragraphs
	'Iterates through the child elements of paragraph
	For i As Integer = 0 To paragraph.ChildEntities.Count - 1
		'Removes images from the paragraph
		If TypeOf paragraph.ChildEntities(i) Is WPicture Then
			paragraph.Items.RemoveAt(i)
			i -= 1
		End If
	Next
Next
'Saves the Word document
document.Save("Sample.docx", FormatType.Docx)
'Closes the document
document.Close()
{% endhighlight %} 

{% highlight UWP %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream fileStream = assembly.GetManifestResourceStream("CreateWordSample.Assets.Template.docx");
//Loads the template document 
WordDocument document = new WordDocument(fileStream);
WTextBody textbody = document.Sections[0].Body;
//Iterates through the paragraphs of the textbody
foreach (WParagraph paragraph in textbody.Paragraphs)
{
    //Iterates through the child elements of paragraph
    for (int i = 0; i < paragraph.ChildEntities.Count; i++)
    {
        //Removes images from the paragraph
        if (paragraph.ChildEntities[i] is WPicture)
        {
            paragraph.Items.RemoveAt(i);
            i--;
        }
    }
}
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Refer to the following link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight ASP.NET CORE %}
FileStream fileStream = new FileStream(@"Template.docx", FileMode.Open, FileAccess.ReadWrite);
//Loads the template document 
WordDocument document = new WordDocument(fileStream, FormatType.Automatic);
WTextBody textbody = document.Sections[0].Body;
//Iterates through the paragraphs of the textbody
foreach (WParagraph paragraph in textbody.Paragraphs)
{
    //Iterates through the child elements of paragraph
    for (int i = 0; i < paragraph.ChildEntities.Count; i++)
    {
        //Removes images from the paragraph
        if (paragraph.ChildEntities[i] is WPicture)
        {
            paragraph.Items.RemoveAt(i);
            i--;
        }
    }
}
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %} 

{% highlight XAMARIN %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream fileStream = assembly.GetManifestResourceStream("CreateWordSample.Assets.Template.docx");
//Loads the template document 
WordDocument document = new WordDocument(fileStream, FormatType.Automatic);
WTextBody textbody = document.Sections[0].Body;
//Iterates through the paragraphs of the textbody
foreach (WParagraph paragraph in textbody.Paragraphs)
{
    //Iterates through the child elements of paragraph
    for (int i = 0; i < paragraph.ChildEntities.Count; i++)
    {
        //Removes images from the paragraph
        if (paragraph.ChildEntities[i] is WPicture)
        {
            paragraph.Items.RemoveAt(i);
            i--;
        }
    }
}
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Download the helper files from the following link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %} 

{% endtabs %}  

### Format and rotate images

Absolute positioned images have properties such as position, wrap formats, and alignments. These properties are not applicable when the text wrapping style is inline. You can also rotate an image and apply flipping (horizontal and vertical) to it.

The following code example explains how various picture formats can be applied to the picture.

{% tabs %} 

{% highlight c# %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
paragraph.AppendText("This paragraph has picture. ");
//Appends new picture to the paragraph
WPicture picture = paragraph.AppendPicture(Image.FromFile("Image.png")) as WPicture;
//Sets text wrapping style – When the wrapping style is inline, the images are not absolutely positioned. It is added next to the text range.
picture.TextWrappingStyle = TextWrappingStyle.Square;
//Sets horizontal and vertical origin
picture.HorizontalOrigin = HorizontalOrigin.Page;
picture.VerticalOrigin = VerticalOrigin.Paragraph;
//Sets width and height for the paragraph
picture.Width = 150;
picture.Height = 100;
//Sets horizontal and vertical position for the picture
picture.HorizontalPosition = 200;
picture.VerticalPosition = 150;
//Sets lock aspect ratio for the picture
picture.LockAspectRatio = true;
picture.Name = "PictureName";
//Sets horizontal and vertical alignments
picture.HorizontalAlignment = ShapeHorizontalAlignment.Center;
picture.VerticalAlignment = ShapeVerticalAlignment.Bottom;
//Sets 90 degree rotation
picture.Rotation = 90;
//Sets horizontal flip
picture.FlipHorizontal = true;
//Saves the Word document
document.Save("Sample.docx", FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Creates a new Word document 
Dim document As New WordDocument()
'Adds new section to the document
Dim section As IWSection = document.AddSection()
'Adds new paragraph to the section
Dim paragraph As IWParagraph = section.AddParagraph()
paragraph.AppendText("This paragraph has picture. ")
'Appends new picture to the paragraph
Dim picture As WPicture = TryCast(paragraph.AppendPicture(Image.FromFile("Image.png")), WPicture)
'Sets text wrapping style – When the wrapping style is inline, the images are not absolutely positioned. It is added next to the text range.
picture.TextWrappingStyle = TextWrappingStyle.Square
'Sets horizontal and vertical origin
picture.HorizontalOrigin = HorizontalOrigin.Page
picture.VerticalOrigin = VerticalOrigin.Paragraph
'Sets width and height for the paragraph
picture.Width = 150
picture.Height = 100
'Sets horizontal and vertical position for the picture
picture.HorizontalPosition = 200
picture.VerticalPosition = 150
'Sets lock aspect ratio for the picture
picture.LockAspectRatio = true
picture.Name = "PictureName"
'Sets horizontal and vertical alignments
picture.HorizontalAlignment = ShapeHorizontalAlignment.Center
picture.VerticalAlignment = ShapeVerticalAlignment.Bottom
'Sets 90 degree rotation
picture.Rotation = 90
'Sets horizontal flip
picture.FlipHorizontal = true
'Saves the Word document
document.Save("Sample.docx", FormatType.Docx)
'Closes the document
document.Close()
{% endhighlight %}  

{% highlight UWP %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
paragraph.AppendText("This paragraph has picture. ");
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream imageStream = assembly.GetManifestResourceStream("CreateWordSample.Assets.Image.png");
//Appends new picture to the paragraph
WPicture picture = paragraph.AppendPicture(imageStream) as WPicture;
//Sets text wrapping style – When the wrapping style is inline, the images are not absolutely positioned. It is added next to the text range.
picture.TextWrappingStyle = TextWrappingStyle.Square;
//Sets horizontal and vertical origin
picture.HorizontalOrigin = HorizontalOrigin.Page;
picture.VerticalOrigin = VerticalOrigin.Paragraph;
//Sets width and height for the paragraph
picture.Width = 150;
picture.Height = 100;
//Sets horizontal and vertical position for the picture
picture.HorizontalPosition = 200;
picture.VerticalPosition = 150;
//Sets lock aspect ratio for the picture
picture.LockAspectRatio = true;
picture.Name = "PictureName";
//Sets horizontal and vertical alignments
picture.HorizontalAlignment = ShapeHorizontalAlignment.Center;
picture.VerticalAlignment = ShapeVerticalAlignment.Bottom;
//Sets 90 degree rotation
picture.Rotation = 90;
//Sets horizontal flip
picture.FlipHorizontal = true;
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Refer to the following link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight ASP.NET CORE %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
paragraph.AppendText("This paragraph has picture. ");
FileStream imageStream = new FileStream(@"Image.png", FileMode.Open, FileAccess.ReadWrite);
//Appends new picture to the paragraph
WPicture picture = paragraph.AppendPicture(imageStream) as WPicture;
//Sets text wrapping style – When the wrapping style is inline, the images are not absolutely positioned. It is added next to the text range.
picture.TextWrappingStyle = TextWrappingStyle.Square;    
//Sets horizontal and vertical origin
picture.HorizontalOrigin = HorizontalOrigin.Page;
picture.VerticalOrigin = VerticalOrigin.Paragraph;
//Sets width and height for the paragraph
picture.Width = 150;     
picture.Height = 100;
//Sets horizontal and vertical position for the picture
picture.HorizontalPosition = 200;
picture.VerticalPosition = 150;
//Sets lock aspect ratio for the picture
picture.LockAspectRatio = true;
picture.Name = "PictureName";
//Sets horizontal and vertical alignments
picture.HorizontalAlignment = ShapeHorizontalAlignment.Center;
picture.VerticalAlignment = ShapeVerticalAlignment.Bottom;
//Sets 90 degree rotation
picture.Rotation = 90;
//Sets horizontal flip
picture.FlipHorizontal = true;
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %} 

{% highlight XAMARIN %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
paragraph.AppendText("This paragraph has picture. ");
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream imageStream = assembly.GetManifestResourceStream("CreateWordSample.Assets.Image.png");
//Appends new picture to the paragraph
WPicture picture = paragraph.AppendPicture(imageStream) as WPicture;
//Sets text wrapping style – When the wrapping style is inline, the images are not absolutely positioned. It is added next to the text range.
picture.TextWrappingStyle = TextWrappingStyle.Square;
//Sets horizontal and vertical origin
picture.HorizontalOrigin = HorizontalOrigin.Page;
picture.VerticalOrigin = VerticalOrigin.Paragraph;
//Sets width and height for the paragraph
picture.Width = 150;
picture.Height = 100;
//Sets horizontal and vertical position for the picture
picture.HorizontalPosition = 200;
picture.VerticalPosition = 150;
//Sets lock aspect ratio for the picture
picture.LockAspectRatio = true;
picture.Name = "PictureName";
//Sets horizontal and vertical alignments
picture.HorizontalAlignment = ShapeHorizontalAlignment.Center;
picture.VerticalAlignment = ShapeVerticalAlignment.Bottom;
//Sets 90 degree rotation
picture.Rotation = 90;
//Sets horizontal flip
picture.FlipHorizontal = true;
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Download the helper files from the following link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %} 

{% endtabs %} 

### Find an image by title 

An Image with a specific title can be retrieved by iterating the paragraph items that can be used for further manipulations.

The following code example explains how images can be iterated from the document elements.

{% tabs %}  

{% highlight c# %}
//Creates a new Word document 
WordDocument document = new WordDocument("Template.docx");
//Gets textbody content
WTextBody textBody = document.Sections[0].Body;
//Iterates through the textbody child entities
foreach (TextBodyItem item in textBody.ChildEntities)
{
    if (item is WParagraph)
    {
        WParagraph paragraph = item as WParagraph;
        foreach (ParagraphItem paraItem in paragraph.ChildEntities)
        {
            //Gets the image from its title and modifies its width and height
            if (paraItem is WPicture)
            {
                WPicture picture = paraItem as WPicture;
                if (picture.Title == "Bookmark")
                {
                    picture.Width = 150;
                    picture.Height = 100;
                }
            }
        }
    }
}
//Saves the Word document
document.Save("Sample.docx", FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Creates a new Word document 
Dim document As New WordDocument("Template.docx")
'Gets textbody content
Dim textBody As WTextBody = document.Sections(0).Body
'Iterates through the textbody child entities
For Each item As TextBodyItem In textBody.ChildEntities
	If TypeOf item Is WParagraph Then
		Dim paragraph As WParagraph = TryCast(item, WParagraph)
		For Each paraItem As ParagraphItem In paragraph.ChildEntities
			'Gets the image from its title and modifies its width and height
			If TypeOf paraItem Is WPicture Then
				Dim picture As WPicture = TryCast(paraItem, WPicture)
				If picture.Title = "Bookmark" Then
					picture.Width = 150
					picture.Height = 100
				End If
			End If
		Next
	End If
Next
'Saves the Word document
document.Save("Sample.docx", FormatType.Docx)
'Closes the document
document.Close()
{% endhighlight %}

{% highlight UWP %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream fileStream = assembly.GetManifestResourceStream("CreateWordSample.Assets.Template.docx");
//Loads an existing Word document into DocIO instance
WordDocument document = new WordDocument(fileStream);
//Gets textbody content
WTextBody textBody = document.Sections[0].Body;
//Iterates through the textbody child entities
foreach (TextBodyItem item in textBody.ChildEntities)
{
    if (item is WParagraph)
    {
        WParagraph paragraph = item as WParagraph;
        foreach (ParagraphItem paraItem in paragraph.ChildEntities)
        {
            //Gets the image from its title and modifies its width and height
            if (paraItem is WPicture)
            {
                WPicture picture = paraItem as WPicture;
                if (picture.Title == "Bookmark")
                {
                    picture.Width = 150;
                    picture.Height = 100;
                }
            }
        }
    }
}
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Refer to the following link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight ASP.NET CORE %}
FileStream fileStream = new FileStream(@"Template.docx", FileMode.Open, FileAccess.ReadWrite);
//Loads an existing Word document into DocIO instance
WordDocument document = new WordDocument(fileStream, FormatType.Automatic);
//Gets textbody content
WTextBody textBody = document.Sections[0].Body;
//Iterates through the textbody child entities
foreach (TextBodyItem item in textBody.ChildEntities)
{
    if (item is WParagraph)
    {
        WParagraph paragraph = item as WParagraph;
        foreach (ParagraphItem paraItem in paragraph.ChildEntities)
        {
            //Gets the image from its title and modifies its width and height
            if (paraItem is WPicture)
            {
                WPicture picture = paraItem as WPicture;
                if (picture.Title == "Bookmark")
                {
                    picture.Width = 150;
                    picture.Height = 100;
                }
            }
        }
    }
}
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %} 

{% highlight XAMARIN %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream fileStream = assembly.GetManifestResourceStream("CreateWordSample.Assets.Template.docx");
//Loads an existing Word document into DocIO instance
WordDocument document = new WordDocument(fileStream, FormatType.Automatic);
//Gets textbody content
WTextBody textBody = document.Sections[0].Body;
//Iterates through the textbody child entities
foreach (TextBodyItem item in textBody.ChildEntities)
{
    if (item is WParagraph)
    {
        WParagraph paragraph = item as WParagraph;
        foreach (ParagraphItem paraItem in paragraph.ChildEntities)
        {
            //Gets the image from its title and modifies its width and height
            if (paraItem is WPicture)
            {
                WPicture picture = paraItem as WPicture;
                if (picture.Title == "Bookmark")
                {
                    picture.Width = 150;
                    picture.Height = 100;
                }
            }
        }
    }
}
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Download the helper files from the following link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %} 

{% endtabs %} 

### Add Image caption 

You can add caption to an image and update the caption numbers (Sequence fields) using `AddCaption` method.

The following code example shows how to add caption to an image.

{% tabs %} 

{% highlight c# %}
//Creates a new document
WordDocument document = new WordDocument();
//Adds a new section to the document
IWSection section = document.AddSection();
//Sets margin of the section
section.PageSetup.Margins.All = 72;
//Adds a paragraph to the section
IWParagraph paragraph = section.AddParagraph();
paragraph.ParagraphFormat.HorizontalAlignment = HorizontalAlignment.Center;
//Adds image to  the paragraph
IWPicture picture = paragraph.AppendPicture(Image.FromFile("Google.png"));
//Adds Image caption
IWParagraph lastParagragh = picture.AddCaption("Figure", CaptionNumberingFormat.Roman, CaptionPosition.AfterImage);
//Aligns the caption
lastParagragh.ParagraphFormat.HorizontalAlignment = HorizontalAlignment.Center;
//Sets after spacing
lastParagragh.ParagraphFormat.AfterSpacing = 12f;
//Sets before spacing
lastParagragh.ParagraphFormat.BeforeSpacing = 1.5f;
//Adds a paragraph to the section
paragraph = section.AddParagraph();
paragraph.ParagraphFormat.HorizontalAlignment = HorizontalAlignment.Center;
//Adds image to  the paragraph
picture = paragraph.AppendPicture(Image.FromFile("Yahoo.png"));
//Adds Image caption
lastParagragh = picture.AddCaption("Figure", CaptionNumberingFormat.Roman, CaptionPosition.AfterImage);
//Aligns the caption
lastParagragh.ParagraphFormat.HorizontalAlignment = HorizontalAlignment.Center;
//Sets before spacing
lastParagragh.ParagraphFormat.BeforeSpacing = 1.5f;
//Updates the fields in Word document
document.UpdateDocumentFields();
//Saves and closes the document
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %} 

{% highlight vb.net %}
'Creates a new document
Dim document As WordDocument = New WordDocument
'Adds a new section to the document
Dim section As IWSection = document.AddSection
'Sets margin of the section
section.PageSetup.Margins.All = 72
'Adds a paragraph to the section
Dim paragraph As IWParagraph = section.AddParagraph
paragraph.ParagraphFormat.HorizontalAlignment = HorizontalAlignment.Center
'Adds image to  the paragraph
Dim picture As IWPicture = paragraph.AppendPicture(Image.FromFile("Google.png"))
'Adds Image caption
Dim lastParagragh As IWParagraph = picture.AddCaption("Figure", CaptionNumberingFormat.Roman, CaptionPosition.AfterImage)
'Aligns the caption
lastParagragh.ParagraphFormat.HorizontalAlignment = HorizontalAlignment.Center
'Sets after spacing
lastParagragh.ParagraphFormat.AfterSpacing = 12.0F
'Sets before spacing
lastParagragh.ParagraphFormat.BeforeSpacing = 1.5F
'Adds a paragraph to the section
paragraph = section.AddParagraph
paragraph.ParagraphFormat.HorizontalAlignment = HorizontalAlignment.Center
'Adds image to  the paragraph
picture = paragraph.AppendPicture(Image.FromFile("Yahoo.png"))
'Adds Image caption
lastParagragh = picture.AddCaption("Figure", CaptionNumberingFormat.Roman, CaptionPosition.AfterImage)
'Aligns the caption
lastParagragh.ParagraphFormat.HorizontalAlignment = HorizontalAlignment.Center
'Sets before spacing
lastParagragh.ParagraphFormat.BeforeSpacing = 1.5F
'Updates the fields in Word document
document.UpdateDocumentFields()
'Saves and closes the document
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %} 

{% highlight UWP %}
//Creates a new document
WordDocument document = new WordDocument();
//Adds a new section to the document.
IWSection section = document.AddSection();
//Sets margin of the section
section.PageSetup.Margins.All = 72;
//Adds a paragraph to the section
IWParagraph paragraph = section.AddParagraph();
paragraph.ParagraphFormat.HorizontalAlignment = Syncfusion.DocIO.DLS.HorizontalAlignment.Center;
//Adds image to  the paragraph
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream imageStream = assembly.GetManifestResourceStream("Sample.Assets.Google.png");
IWPicture picture = paragraph.AppendPicture(imageStream);
//Adds Image caption
IWParagraph lastParagragh = picture.AddCaption("Figure", CaptionNumberingFormat.Roman, CaptionPosition.AfterImage);
//Aligns the caption
lastParagragh.ParagraphFormat.HorizontalAlignment = Syncfusion.DocIO.DLS.HorizontalAlignment.Center;
//Sets after spacing
lastParagragh.ParagraphFormat.AfterSpacing = 12f;
//Sets before spacing
lastParagragh.ParagraphFormat.BeforeSpacing = 1.5f;
//Adds a paragraph to the section
paragraph = section.AddParagraph();
paragraph.ParagraphFormat.HorizontalAlignment = Syncfusion.DocIO.DLS.HorizontalAlignment.Center;
//Adds image to  the paragraph
assembly = typeof(App).GetTypeInfo().Assembly;
imageStream = assembly.GetManifestResourceStream("Sample.Assets.Yahoo.png");
picture = paragraph.AppendPicture(imageStream);
//Adds Image caption
lastParagragh = picture.AddCaption("Figure", CaptionNumberingFormat.Roman, CaptionPosition.AfterImage);
//Aligns the caption
lastParagragh.ParagraphFormat.HorizontalAlignment = Syncfusion.DocIO.DLS.HorizontalAlignment.Center;
//Sets before spacing
lastParagragh.ParagraphFormat.BeforeSpacing = 1.5f;
//Updates the fields in Word document
document.UpdateDocumentFields();
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word document file in local machine
Save(stream, "Sample.docx");
//Closes the document instance
document.Close();
          
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight ASP.NET CORE %}
 //Creates a new document
WordDocument document = new WordDocument();
//Adds a new section to the document.
IWSection section = document.AddSection();
//Sets margin of the section
section.PageSetup.Margins.All = 72;
//Adds a paragraph to the section
IWParagraph paragraph = section.AddParagraph();
paragraph.ParagraphFormat.HorizontalAlignment = HorizontalAlignment.Center;
//Adds image to  the paragraph
FileStream imageStream = new FileStream(@"Google.png", FileMode.Open, FileAccess.ReadWrite);
IWPicture picture = paragraph.AppendPicture(imageStream);
//Adds Image caption
IWParagraph lastParagragh = picture.AddCaption("Figure", CaptionNumberingFormat.Roman, CaptionPosition.AfterImage);
//Aligns the caption
lastParagragh.ParagraphFormat.HorizontalAlignment = HorizontalAlignment.Center;
//Sets after spacing
lastParagragh.ParagraphFormat.AfterSpacing = 12f;
//Sets before spacing
lastParagragh.ParagraphFormat.BeforeSpacing = 1.5f;
//Adds a paragraph to the section
paragraph = section.AddParagraph();
paragraph.ParagraphFormat.HorizontalAlignment = HorizontalAlignment.Center;
//Adds image to  the paragraph
imageStream = new FileStream(@"Yahoo.png", FileMode.Open, FileAccess.ReadWrite);
picture = paragraph.AppendPicture(imageStream);
//Adds Image caption
lastParagragh = picture.AddCaption("Figure", CaptionNumberingFormat.Roman, CaptionPosition.AfterImage);
//Aligns the caption
lastParagragh.ParagraphFormat.HorizontalAlignment = HorizontalAlignment.Center;
//Sets before spacing
lastParagragh.ParagraphFormat.BeforeSpacing = 1.5f;
//Updates the fields in Word document
document.UpdateDocumentFields();
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Sample.docx");
{% endhighlight %} 

{% highlight XAMARIN %}
 //Creates a new document
WordDocument document = new WordDocument();
//Adds a new section to the document.
IWSection section = document.AddSection();
//Sets margin of the section
section.PageSetup.Margins.All = 72;
//Adds a paragraph to the section
IWParagraph paragraph = section.AddParagraph();
paragraph.ParagraphFormat.HorizontalAlignment = HorizontalAlignment.Center;
//Adds image to  the paragraph
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream imageStream = assembly.GetManifestResourceStream("Sample.Assets.Google.png");
IWPicture picture = paragraph.AppendPicture(imageStream);
//Adds Image caption
IWParagraph lastParagragh = picture.AddCaption("Figure", CaptionNumberingFormat.Roman, CaptionPosition.AfterImage);
//Aligns the caption
lastParagragh.ParagraphFormat.HorizontalAlignment = HorizontalAlignment.Center;
//Sets after spacing
lastParagragh.ParagraphFormat.AfterSpacing = 12f;
//Sets before spacing
lastParagragh.ParagraphFormat.BeforeSpacing = 1.5f;
//Adds a paragraph to the section
paragraph = section.AddParagraph();
paragraph.ParagraphFormat.HorizontalAlignment = HorizontalAlignment.Center;
//Adds image to  the paragraph
assembly = typeof(App).GetTypeInfo().Assembly;
imageStream = assembly.GetManifestResourceStream("Sample.Assets.Yahoo.png");
picture = paragraph.AppendPicture(imageStream);
//Adds Image caption
lastParagragh = picture.AddCaption("Figure", CaptionNumberingFormat.Roman, CaptionPosition.AfterImage);
//Aligns the caption
lastParagragh.ParagraphFormat.HorizontalAlignment = HorizontalAlignment.Center;
//Sets before spacing
lastParagragh.ParagraphFormat.BeforeSpacing = 1.5f;
//Updates the fields in Word document
document.UpdateDocumentFields();
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

By executing the above code example, it generates output Word document as follows.

![Output of Word document with Image caption](WorkingWithImages_images/ImageCaption.png)

## Working with lists

Lists can organize and format the contents of a document in hierarchical way. There are nine levels in the list, starting from level 0 to level 8. DocIO supports both built-in list styles and custom list styles. The following are the types of list supported in DocIO: 

* Numbered list
* Bulleted list 

The following code example explains how to create a simple bulleted list.

{% tabs %} 

{% highlight c# %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Applies default numbered list style
paragraph.ListFormat.ApplyDefBulletStyle();
//Adds text to the paragraph
paragraph.AppendText("List item 1");
//Continues the list defined
paragraph.ListFormat.ContinueListNumbering();
//Adds second paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("List item 2");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Adds new paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("List item 3");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Saves the Word document
document.Save("Sample.docx", FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Creates a new Word document 
Dim document As New WordDocument()
'Adds new section to the document
Dim section As IWSection = document.AddSection()
'Adds new paragraph to the section
Dim paragraph As IWParagraph = section.AddParagraph()
'Applies default numbered list style
paragraph.ListFormat.ApplyDefBulletStyle()
'Adds text to the paragraph
paragraph.AppendText("List item 1")
'Continues the list defined
paragraph.ListFormat.ContinueListNumbering()
'Adds second paragraph
paragraph = section.AddParagraph()
paragraph.AppendText("List item 2")
'Continues last defined list
paragraph.ListFormat.ContinueListNumbering()
'Adds new paragraph
paragraph = section.AddParagraph()
paragraph.AppendText("List item 3")
'Continues last defined list
paragraph.ListFormat.ContinueListNumbering()
'Saves the Word document
document.Save("Sample.docx", FormatType.Docx)
'Closes the document
document.Close()
{% endhighlight %}  

{% highlight UWP %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Applies default numbered list style
paragraph.ListFormat.ApplyDefBulletStyle();
//Adds text to the paragraph
paragraph.AppendText("List item 1");
//Continues the list defined
paragraph.ListFormat.ContinueListNumbering();
//Adds second paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("List item 2");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Adds new paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("List item 3");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Refer to the following link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight ASP.NET CORE %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Applies default numbered list style
paragraph.ListFormat.ApplyDefBulletStyle();
//Adds text to the paragraph
paragraph.AppendText("List item 1");
//Continues the list defined
paragraph.ListFormat.ContinueListNumbering();
//Adds second paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("List item 2");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Adds new paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("List item 3");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %} 

{% highlight XAMARIN %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Applies default numbered list style
paragraph.ListFormat.ApplyDefBulletStyle();
//Adds text to the paragraph
paragraph.AppendText("List item 1");
//Continues the list defined
paragraph.ListFormat.ContinueListNumbering();
//Adds second paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("List item 2");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Adds new paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("List item 3");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream); 
//Download the helper files from the following link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin  
{% endhighlight %} 

{% endtabs %}  

The following code example explains how to create a simple numbered list.

{% tabs %} 

{% highlight c# %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Applies default numbered list style
paragraph.ListFormat.ApplyDefNumberedStyle();
//Adds text to the paragraph
paragraph.AppendText("List item 1");
//Continues the list defined
paragraph.ListFormat.ContinueListNumbering();
//Adds second paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("List item 2");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Adds new paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("List item 3");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Saves the Word document
document.Save("Sample.docx", FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Creates a new Word document 
Dim document As New WordDocument()
'Adds new section to the document
Dim section As IWSection = document.AddSection()
'Adds new paragraph to the section
Dim paragraph As IWParagraph = section.AddParagraph()
'Applies default numbered list style
paragraph.ListFormat.ApplyDefNumberedStyle()
'Adds text to the paragraph
paragraph.AppendText("List item 1")
'Continues the list defined
paragraph.ListFormat.ContinueListNumbering()
'Adds second paragraph
paragraph = section.AddParagraph()
paragraph.AppendText("List item 2")
'Continues last defined list
paragraph.ListFormat.ContinueListNumbering()
'Adds new paragraph
paragraph = section.AddParagraph()
paragraph.AppendText("List item 3")
'Continues last defined list
paragraph.ListFormat.ContinueListNumbering()
'Saves the Word document
document.Save("Sample.docx", FormatType.Docx)
'Closes the document
document.Close()
{% endhighlight %} 

{% highlight UWP %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Applies default numbered list style
paragraph.ListFormat.ApplyDefNumberedStyle();
//Adds text to the paragraph
paragraph.AppendText("List item 1");
//Continues the list defined
paragraph.ListFormat.ContinueListNumbering();
//Adds second paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("List item 2");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Adds new paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("List item 3");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Refer to the following link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight ASP.NET CORE %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Applies default numbered list style
paragraph.ListFormat.ApplyDefNumberedStyle();
//Adds text to the paragraph
paragraph.AppendText("List item 1");
//Continues the list defined
paragraph.ListFormat.ContinueListNumbering();
//Adds second paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("List item 2");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Adds new paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("List item 3");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %} 

{% highlight XAMARIN %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Applies default numbered list style
paragraph.ListFormat.ApplyDefNumberedStyle();
//Adds text to the paragraph
paragraph.AppendText("List item 1");
//Continues the list defined
paragraph.ListFormat.ContinueListNumbering();
//Adds second paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("List item 2");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Adds new paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("List item 3");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Download the helper files from the following link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %} 

{% endtabs %}  

The following code example explains how to create a multilevel bulleted list.

{% tabs %}  

{% highlight c# %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Applies default numbered list style
paragraph.ListFormat.ApplyDefBulletStyle();
//Adds text to the paragraph
paragraph.AppendText("List item 1 - Level 0");
//Continues the list defined
paragraph.ListFormat.ContinueListNumbering();
//Adds second paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("List item 2 - Level 1");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Increases the level indent
paragraph.ListFormat.IncreaseIndentLevel();
//Adds new paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("List item 3 - Level 2");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Increases the level indent
paragraph.ListFormat.IncreaseIndentLevel();
//Saves the Word document
document.Save("Sample.docx", FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Creates a new Word document 
Dim document As New WordDocument()
'Adds new section to the document
Dim section As IWSection = document.AddSection()
'Adds new paragraph to the section
Dim paragraph As IWParagraph = section.AddParagraph()
'Applies default numbered list style
paragraph.ListFormat.ApplyDefBulletStyle()
'Adds text to the paragraph
paragraph.AppendText("List item 1 - Level 0")
'Continues the list defined
paragraph.ListFormat.ContinueListNumbering()
'Adds second paragraph
paragraph = section.AddParagraph()
paragraph.AppendText("List item 2 - Level 1")
'Continues last defined list
paragraph.ListFormat.ContinueListNumbering()
'Increases the level indent
paragraph.ListFormat.IncreaseIndentLevel()
'Adds new paragraph
paragraph = section.AddParagraph()
paragraph.AppendText("List item 3 - Level 2")
'Continues last defined list
paragraph.ListFormat.ContinueListNumbering()
'Increases the level indent
paragraph.ListFormat.IncreaseIndentLevel()
'Saves the Word document
document.Save("Sample.docx", FormatType.Docx)
'Closes the document
document.Close()
{% endhighlight %} 

{% highlight UWP %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Applies default numbered list style
paragraph.ListFormat.ApplyDefBulletStyle();
//Adds text to the paragraph
paragraph.AppendText("List item 1 - Level 0");
//Continues the list defined
paragraph.ListFormat.ContinueListNumbering();
//Adds second paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("List item 2 - Level 1");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Increases the level indent
paragraph.ListFormat.IncreaseIndentLevel();
//Adds new paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("List item 3 - Level 2");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Increases the level indent
paragraph.ListFormat.IncreaseIndentLevel();
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Refer to the following link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight ASP.NET CORE %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Applies default numbered list style
paragraph.ListFormat.ApplyDefBulletStyle();
//Adds text to the paragraph
paragraph.AppendText("List item 1 - Level 0");
//Continues the list defined
paragraph.ListFormat.ContinueListNumbering();
//Adds second paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("List item 2 - Level 1");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Increases the level indent
paragraph.ListFormat.IncreaseIndentLevel();
//Adds new paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("List item 3 - Level 2");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Increases the level indent
paragraph.ListFormat.IncreaseIndentLevel();
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %} 

{% highlight XAMARIN %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Applies default numbered list style
paragraph.ListFormat.ApplyDefBulletStyle();
//Adds text to the paragraph
paragraph.AppendText("List item 1 - Level 0");
//Continues the list defined
paragraph.ListFormat.ContinueListNumbering();
//Adds second paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("List item 2 - Level 1");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Increases the level indent
paragraph.ListFormat.IncreaseIndentLevel();
//Adds new paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("List item 3 - Level 2");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Increases the level indent
paragraph.ListFormat.IncreaseIndentLevel();
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Download the helper files from the following link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %} 

{% endtabs %}  

The following code example explains how to create multilevel numbered list.

{% tabs %}  

{% highlight c# %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Applies default numbered list style
paragraph.ListFormat.ApplyDefNumberedStyle();
//Adds text to the paragraph
paragraph.AppendText("List item 1 - Level 0");
//Continues the list defined
paragraph.ListFormat.ContinueListNumbering();
//Adds second paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("List item 2 - Level 1");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Increases the level indent
paragraph.ListFormat.IncreaseIndentLevel();
//Adds new paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("List item 3 - Level 2");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Increases the level indent
paragraph.ListFormat.IncreaseIndentLevel();
//Saves the Word document
document.Save("Sample.docx", FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Creates a new Word document 
Dim document As New WordDocument()
'Adds new section to the document
Dim section As IWSection = document.AddSection()
'Adds new paragraph to the section
Dim paragraph As IWParagraph = section.AddParagraph()
'Applies default numbered list style
paragraph.ListFormat.ApplyDefNumberedStyle()
'Adds text to the paragraph
paragraph.AppendText("List item 1 - Level 0")
'Continues the list defined
paragraph.ListFormat.ContinueListNumbering()
'Adds second paragraph
paragraph = section.AddParagraph()
paragraph.AppendText("List item 2 - Level 1")
'Continues last defined list
paragraph.ListFormat.ContinueListNumbering()
'Increases the level indent
paragraph.ListFormat.IncreaseIndentLevel()
'Adds new paragraph
paragraph = section.AddParagraph()
paragraph.AppendText("List item 3 - Level 2")
'Continues last defined list
paragraph.ListFormat.ContinueListNumbering()
'Increases the level indent
paragraph.ListFormat.IncreaseIndentLevel()
'Saves the Word document
document.Save("Sample.docx", FormatType.Docx)
'Closes the document
document.Close()
{% endhighlight %}  

{% highlight UWP %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Applies default numbered list style
paragraph.ListFormat.ApplyDefNumberedStyle();
//Adds text to the paragraph
paragraph.AppendText("List item 1 - Level 0");
//Continues the list defined
paragraph.ListFormat.ContinueListNumbering();
//Adds second paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("List item 2 - Level 1");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Increases the level indent
paragraph.ListFormat.IncreaseIndentLevel();
//Adds new paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("List item 3 - Level 2");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Increases the level indent
paragraph.ListFormat.IncreaseIndentLevel();
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
document.Close();   
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Refer to the following link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight ASP.NET CORE %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document     
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Applies default numbered list style
paragraph.ListFormat.ApplyDefNumberedStyle();
//Adds text to the paragraph
paragraph.AppendText("List item 1 - Level 0");
//Continues the list defined
paragraph.ListFormat.ContinueListNumbering();
//Adds second paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("List item 2 - Level 1");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Increases the level indent
paragraph.ListFormat.IncreaseIndentLevel();
//Adds new paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("List item 3 - Level 2");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Increases the level indent
paragraph.ListFormat.IncreaseIndentLevel();
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %} 

{% highlight XAMARIN %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Applies default numbered list style
paragraph.ListFormat.ApplyDefNumberedStyle();
//Adds text to the paragraph
paragraph.AppendText("List item 1 - Level 0");
//Continues the list defined
paragraph.ListFormat.ContinueListNumbering();
//Adds second paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("List item 2 - Level 1");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Increases the level indent
paragraph.ListFormat.IncreaseIndentLevel();
//Adds new paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("List item 3 - Level 2");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Increases the level indent
paragraph.ListFormat.IncreaseIndentLevel();
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Download the helper files from the following link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}  

The list levels can be incremented or decremented by using the `IncreaseIndentLevel` and `DecreaseIndentLevel` methods respectively. The following code example explains how to increase or decrease the list indent levels.

{% tabs %} 

{% highlight c# %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Applies default numbered list style
paragraph.ListFormat.ApplyDefNumberedStyle();
//Adds text to the paragraph
paragraph.AppendText("Multilevel numbered list - Level 0");
//Continues the list defined
paragraph.ListFormat.ContinueListNumbering();
//Adds second paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("Multilevel numbered list - Level 1");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Increases the level indent
paragraph.ListFormat.IncreaseIndentLevel();
//Adds new paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("Multilevel numbered list - Level 0");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Increases the level indent
paragraph.ListFormat.DecreaseIndentLevel();
//Adds new paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("Multilevel numbered list - Level 1");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Increases the level indent
paragraph.ListFormat.IncreaseIndentLevel();
//Saves the Word document
document.Save("Sample.docx", FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Creates a new Word document 
Dim document As New WordDocument()
'Adds new section to the document
Dim section As IWSection = document.AddSection()
'Adds new paragraph to the section
Dim paragraph As IWParagraph = section.AddParagraph()
'Applies default numbered list style
paragraph.ListFormat.ApplyDefNumberedStyle()
'Adds text to the paragraph
paragraph.AppendText("Multilevel numbered list - Level 0")
'Continues the list defined
paragraph.ListFormat.ContinueListNumbering()
'Adds second paragraph
paragraph = section.AddParagraph()
paragraph.AppendText("Multilevel numbered list - Level 1")
'Continues last defined list
paragraph.ListFormat.ContinueListNumbering()
'Increases the level indent
paragraph.ListFormat.IncreaseIndentLevel()
'Adds new paragraph
paragraph = section.AddParagraph()
paragraph.AppendText("Multilevel numbered list - Level 0")
'Continues last defined list
paragraph.ListFormat.ContinueListNumbering()
'Increases the level indent
paragraph.ListFormat.DecreaseIndentLevel()
'Adds new paragraph
paragraph = section.AddParagraph()
paragraph.AppendText("Multilevel numbered list - Level 1")
'Continues last defined list
paragraph.ListFormat.ContinueListNumbering()
'Increases the level indent
paragraph.ListFormat.IncreaseIndentLevel()
'Saves the Word document
document.Save("Sample.docx", FormatType.Docx)
'Closes the document
document.Close()
{% endhighlight %} 

{% highlight UWP %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Applies default numbered list style
paragraph.ListFormat.ApplyDefNumberedStyle();
//Adds text to the paragraph
paragraph.AppendText("Multilevel numbered list - Level 0");
//Continues the list defined
paragraph.ListFormat.ContinueListNumbering();
//Adds second paragraph
paragraph = section.AddParagraph();        
paragraph.AppendText("Multilevel numbered list - Level 1");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Increases the level indent
paragraph.ListFormat.IncreaseIndentLevel();
//Adds new paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("Multilevel numbered list - Level 0");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Increases the level indent
paragraph.ListFormat.DecreaseIndentLevel();
//Adds new paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("Multilevel numbered list - Level 1");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Increases the level indent
paragraph.ListFormat.IncreaseIndentLevel();
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Refer to the following link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight ASP.NET CORE %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Applies default numbered list style
paragraph.ListFormat.ApplyDefNumberedStyle();
//Adds text to the paragraph
paragraph.AppendText("Multilevel numbered list - Level 0");
//Continues the list defined
paragraph.ListFormat.ContinueListNumbering();
//Adds second paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("Multilevel numbered list - Level 1");  
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Increases the level indent
paragraph.ListFormat.IncreaseIndentLevel();
//Adds new paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("Multilevel numbered list - Level 0");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Increases the level indent
paragraph.ListFormat.DecreaseIndentLevel();   
//Adds new paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("Multilevel numbered list - Level 1");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Increases the level indent
paragraph.ListFormat.IncreaseIndentLevel();
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %} 

{% highlight XAMARIN %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Applies default numbered list style
paragraph.ListFormat.ApplyDefNumberedStyle();
//Adds text to the paragraph
paragraph.AppendText("Multilevel numbered list - Level 0");
//Continues the list defined
paragraph.ListFormat.ContinueListNumbering();
//Adds second paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("Multilevel numbered list - Level 1");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Increases the level indent
paragraph.ListFormat.IncreaseIndentLevel();
//Adds new paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("Multilevel numbered list - Level 0");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Increases the level indent
paragraph.ListFormat.DecreaseIndentLevel();
//Adds new paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("Multilevel numbered list - Level 1");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Increases the level indent
paragraph.ListFormat.IncreaseIndentLevel();
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Download the helper files from the following link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %} 

{% endtabs %}  

The following code example explains how to create user defined list styles.

{% tabs %}  

{% highlight c# %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection(); 
//Adds new list style to the document          
ListStyle listStyle = document.AddListStyle(ListType.Numbered, "UserDefinedList");
WListLevel levelOne = listStyle.Levels[0];
//Defines the follow character, prefix, suffix, start index for level 0
levelOne.FollowCharacter = FollowCharacterType.Tab;
levelOne.NumberPrefix = "(";
levelOne.NumberSufix = ")";
levelOne.PatternType = ListPatternType.LowRoman;
levelOne.StartAt = 1;
levelOne.TabSpaceAfter = 5;
levelOne.NumberAlignment = ListNumberAlignment.Center;
WListLevel levelTwo = listStyle.Levels[1];
//Defines the follow character, suffix, pattern, start index for level 1
levelTwo.FollowCharacter = FollowCharacterType.Tab;
levelTwo.NumberSufix = "}";
levelTwo.PatternType = ListPatternType.LowLetter;
levelTwo.StartAt = 2; 
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();  
//Adds text to the paragraph
paragraph.AppendText("User defined list - Level 0");
//Applies default numbered list style
paragraph.ListFormat.ApplyStyle("UserDefinedList");
//Adds second paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("User defined list - Level 1");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Increases the level indent
paragraph.ListFormat.IncreaseIndentLevel();
//Saves the Word document
document.Save("Sample.docx", FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Creates a new Word document 
Dim document As New WordDocument()
'Adds new section to the document
Dim section As IWSection = document.AddSection()
'Adds new list style to the document          
Dim listStyle As ListStyle = document.AddListStyle(ListType.Numbered, "UserDefinedList")
Dim levelOne As WListLevel = listStyle.Levels(0)
'Defines the follow character, prefix, suffix, start index for level 0
levelOne.FollowCharacter = FollowCharacterType.Tab
levelOne.NumberPrefix = "("
levelOne.NumberSufix = ")"
levelOne.PatternType = ListPatternType.LowRoman
levelOne.StartAt = 1
levelOne.TabSpaceAfter = 5
levelOne.NumberAlignment = ListNumberAlignment.Center
Dim levelTwo As WListLevel = listStyle.Levels(1)
'Defines the follow character, suffix, pattern, start index for level 1
levelTwo.FollowCharacter = FollowCharacterType.Tab
levelTwo.NumberSufix = "}"
levelTwo.PatternType = ListPatternType.LowLetter
levelTwo.StartAt = 2
'Adds new paragraph to the section
Dim paragraph As IWParagraph = section.AddParagraph()
'Adds text to the paragraph
paragraph.AppendText("User defined list - Level 0")
'Applies default numbered list style
paragraph.ListFormat.ApplyStyle("UserDefinedList")
'Adds second paragraph
paragraph = section.AddParagraph()
paragraph.AppendText("User defined list - Level 1")
'Continues last defined list
paragraph.ListFormat.ContinueListNumbering()
'Increases the level indent
paragraph.ListFormat.IncreaseIndentLevel()
'Saves the Word document
document.Save("Sample.docx", FormatType.Docx)
'Closes the document
document.Close()
{% endhighlight %}

{% highlight UWP %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new list style to the document          
ListStyle listStyle = document.AddListStyle(ListType.Numbered, "UserDefinedList");
WListLevel levelOne = listStyle.Levels[0];
//Defines the follow character, prefix, suffix, start index for level 0
levelOne.FollowCharacter = FollowCharacterType.Tab;
levelOne.NumberPrefix = "(";
levelOne.NumberSufix = ")";
levelOne.PatternType = ListPatternType.LowRoman;
levelOne.StartAt = 1;
levelOne.TabSpaceAfter = 5;
levelOne.NumberAlignment = ListNumberAlignment.Center;
WListLevel levelTwo = listStyle.Levels[1];
//Defines the follow character, suffix, pattern, start index for level 1
levelTwo.FollowCharacter = FollowCharacterType.Tab;
levelTwo.NumberSufix = "}";
levelTwo.PatternType = ListPatternType.LowLetter;
levelTwo.StartAt = 2;
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Adds text to the paragraph
paragraph.AppendText("User defined list - Level 0");
//Applies default numbered list style
paragraph.ListFormat.ApplyStyle("UserDefinedList");
//Adds second paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("User defined list - Level 1");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Increases the level indent
paragraph.ListFormat.IncreaseIndentLevel();
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Refer to the following link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight ASP.NET CORE %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new list style to the document          
ListStyle listStyle = document.AddListStyle(ListType.Numbered, "UserDefinedList");
WListLevel levelOne = listStyle.Levels[0];
//Defines the follow character, prefix, suffix, start index for level 0
levelOne.FollowCharacter = FollowCharacterType.Tab;
levelOne.NumberPrefix = "(";
levelOne.NumberSufix = ")";
levelOne.PatternType = ListPatternType.LowRoman;
levelOne.StartAt = 1;
levelOne.TabSpaceAfter = 5;
levelOne.NumberAlignment = ListNumberAlignment.Center;
WListLevel levelTwo = listStyle.Levels[1];
//Defines the follow character, suffix, pattern, start index for level 1
levelTwo.FollowCharacter = FollowCharacterType.Tab;
levelTwo.NumberSufix = "}";
levelTwo.PatternType = ListPatternType.LowLetter;
levelTwo.StartAt = 2;
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Adds text to the paragraph
paragraph.AppendText("User defined list - Level 0");
//Applies default numbered list style
paragraph.ListFormat.ApplyStyle("UserDefinedList");
//Adds second paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("User defined list - Level 1");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Increases the level indent
paragraph.ListFormat.IncreaseIndentLevel();
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %} 

{% highlight XAMARIN %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new list style to the document          
ListStyle listStyle = document.AddListStyle(ListType.Numbered, "UserDefinedList");
WListLevel levelOne = listStyle.Levels[0];
//Defines the follow character, prefix, suffix, start index for level 0
levelOne.FollowCharacter = FollowCharacterType.Tab;
levelOne.NumberPrefix = "(";
levelOne.NumberSufix = ")";
levelOne.PatternType = ListPatternType.LowRoman;
levelOne.StartAt = 1;
levelOne.TabSpaceAfter = 5;
levelOne.NumberAlignment = ListNumberAlignment.Center;
WListLevel levelTwo = listStyle.Levels[1];
//Defines the follow character, suffix, pattern, start index for level 1
levelTwo.FollowCharacter = FollowCharacterType.Tab;
levelTwo.NumberSufix = "}";
levelTwo.PatternType = ListPatternType.LowLetter;
levelTwo.StartAt = 2;
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Adds text to the paragraph
paragraph.AppendText("User defined list - Level 0");
//Applies default numbered list style
paragraph.ListFormat.ApplyStyle("UserDefinedList");
//Adds second paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("User defined list - Level 1");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Increases the level indent
paragraph.ListFormat.IncreaseIndentLevel();
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Download the helper files from the following link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %} 

{% endtabs %}  

The following code example explains how to create numbered list with prefix from previous level.

N> The `NumberPrefix` value for the numbered list should meet the syntax "\u000N" to update the previous list level value as prefix to the current list level. For example, it should be represented as (“\u0000.” or “\u0000.\u0001.”).

{% tabs %}  

{% highlight c# %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection(); 
//Adds new list style to the document          
ListStyle listStyle = document.AddListStyle(ListType.Numbered, "UserDefinedList");
WListLevel levelOne = listStyle.Levels[0];
//Defines the follow character, prefix from previous level, start index for level 0
levelOne.FollowCharacter = FollowCharacterType.Nothing;
levelOne.PatternType = ListPatternType.Arabic;
levelOne.StartAt = 1;
WListLevel levelTwo = listStyle.Levels[1];
//Defines the follow character, prefix from previous level, pattern, start index for level 1
levelTwo.FollowCharacter = FollowCharacterType.Nothing;
levelTwo.NumberPrefix = "\u0000.";
levelTwo.PatternType = ListPatternType.Arabic;
levelTwo.StartAt = 1;
WListLevel levelThree = listStyle.Levels[2];
//Defines the follow character, prefix from previous level, pattern, start index for level 1
levelThree.FollowCharacter = FollowCharacterType.Nothing;
levelThree.NumberPrefix = "\u0000.\u0001.";
levelThree.PatternType = ListPatternType.Arabic;
levelThree.StartAt = 1; 
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();  
//Adds text to the paragraph
paragraph.AppendText("User defined list - Level 0");
//Applies default numbered list style
paragraph.ListFormat.ApplyStyle("UserDefinedList");
//Adds second paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("User defined list - Level 1");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Increases the level indent
paragraph.ListFormat.IncreaseIndentLevel();
//Adds second paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("User defined list - Level 2");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Increases the level indent
paragraph.ListFormat.IncreaseIndentLevel();
//Saves the Word document
document.Save("Sample.docx", FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Creates a new Word document 
Dim document As New WordDocument()
'Adds new section to the document
Dim section As IWSection = document.AddSection()
'Adds new list style to the document          
Dim listStyle As ListStyle = document.AddListStyle(ListType.Numbered, "UserDefinedList")
Dim levelOne As WListLevel = listStyle.Levels(0)
'Defines the follow character, prefix from previous level, start index for level 0
levelOne.FollowCharacter = FollowCharacterType.[Nothing]
levelOne.PatternType = ListPatternType.Arabic
levelOne.StartAt = 1
Dim levelTwo As WListLevel = listStyle.Levels(1)
'Defines the follow character, prefix from previous level, pattern, start index for level 1
levelTwo.FollowCharacter = FollowCharacterType.[Nothing]
levelTwo.NumberPrefix = vbNullChar & "."
levelTwo.PatternType = ListPatternType.Arabic
levelTwo.StartAt = 1
Dim levelThree As WListLevel = listStyle.Levels(2)
'Defines the follow character, prefix from previous level, pattern, start index for level 1
levelThree.FollowCharacter = FollowCharacterType.[Nothing]
levelThree.NumberPrefix = vbNullChar & "." & ChrW(1) & "."
levelThree.PatternType = ListPatternType.Arabic
levelThree.StartAt = 1
'Adds new paragraph to the section
Dim paragraph As IWParagraph = section.AddParagraph()
'Adds text to the paragraph
paragraph.AppendText("User defined list - Level 0")
'Applies default numbered list style
paragraph.ListFormat.ApplyStyle("UserDefinedList")
'Adds second paragraph
paragraph = section.AddParagraph()
paragraph.AppendText("User defined list - Level 1")
'Continues last defined list
paragraph.ListFormat.ContinueListNumbering()
'Increases the level indent
paragraph.ListFormat.IncreaseIndentLevel()
'Adds second paragraph
paragraph = section.AddParagraph()
paragraph.AppendText("User defined list - Level 2")
'Continues last defined list
paragraph.ListFormat.ContinueListNumbering()
'Increases the level indent
paragraph.ListFormat.IncreaseIndentLevel()
'Saves the Word document
document.Save("Sample.docx", FormatType.Docx)
'Closes the document
document.Close()
{% endhighlight %}

{% highlight UWP %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new list style to the document          
ListStyle listStyle = document.AddListStyle(ListType.Numbered, "UserDefinedList");
WListLevel levelOne = listStyle.Levels[0];
//Defines the follow character, prefix from previous level, start index for level 0
levelOne.FollowCharacter = FollowCharacterType.Nothing;
levelOne.PatternType = ListPatternType.Arabic;
levelOne.StartAt = 1;
WListLevel levelTwo = listStyle.Levels[1];
//Defines the follow character, prefix from previous level, pattern, start index for level 1
levelTwo.FollowCharacter = FollowCharacterType.Nothing;
levelTwo.NumberPrefix = "\u0000.";
levelTwo.PatternType = ListPatternType.Arabic;
levelTwo.StartAt = 1;
WListLevel levelThree = listStyle.Levels[2];
//Defines the follow character, prefix from previous level, pattern, start index for level 1
levelThree.FollowCharacter = FollowCharacterType.Nothing;
levelThree.NumberPrefix = "\u0000.\u0001.";
levelThree.PatternType = ListPatternType.Arabic;
levelThree.StartAt = 1;
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Adds text to the paragraph
paragraph.AppendText("User defined list - Level 0");
//Applies default numbered list style
paragraph.ListFormat.ApplyStyle("UserDefinedList");
//Adds second paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("User defined list - Level 1");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Increases the level indent
paragraph.ListFormat.IncreaseIndentLevel();
//Adds second paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("User defined list - Level 2");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Increases the level indent
paragraph.ListFormat.IncreaseIndentLevel();
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Refer to the following link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight ASP.NET CORE %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new list style to the document          
ListStyle listStyle = document.AddListStyle(ListType.Numbered, "UserDefinedList");
WListLevel levelOne = listStyle.Levels[0];
//Defines the follow character, prefix from previous level, start index for level 0
levelOne.FollowCharacter = FollowCharacterType.Nothing;
levelOne.PatternType = ListPatternType.Arabic;
levelOne.StartAt = 1;
WListLevel levelTwo = listStyle.Levels[1];
//Defines the follow character, prefix from previous level, pattern, start index for level 1
levelTwo.FollowCharacter = FollowCharacterType.Nothing;
levelTwo.NumberPrefix = "\u0000.";
levelTwo.PatternType = ListPatternType.Arabic;
levelTwo.StartAt = 1;
WListLevel levelThree = listStyle.Levels[2];
//Defines the follow character, prefix from previous level, pattern, start index for level 1
levelThree.FollowCharacter = FollowCharacterType.Nothing;
levelThree.NumberPrefix = "\u0000.\u0001.";
levelThree.PatternType = ListPatternType.Arabic;
levelThree.StartAt = 1;
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Adds text to the paragraph
paragraph.AppendText("User defined list - Level 0");
//Applies default numbered list style
paragraph.ListFormat.ApplyStyle("UserDefinedList");
//Adds second paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("User defined list - Level 1");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Increases the level indent
paragraph.ListFormat.IncreaseIndentLevel();
//Adds second paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("User defined list - Level 2");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Increases the level indent
paragraph.ListFormat.IncreaseIndentLevel();
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %} 

{% highlight XAMARIN %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new list style to the document          
ListStyle listStyle = document.AddListStyle(ListType.Numbered, "UserDefinedList");
WListLevel levelOne = listStyle.Levels[0];
//Defines the follow character, prefix from previous level, start index for level 0
levelOne.FollowCharacter = FollowCharacterType.Nothing;
levelOne.PatternType = ListPatternType.Arabic;      
levelOne.StartAt = 1;
WListLevel levelTwo = listStyle.Levels[1];
//Defines the follow character, prefix from previous level, pattern, start index for level 1
levelTwo.FollowCharacter = FollowCharacterType.Nothing;
levelTwo.NumberPrefix = "\u0000.";
levelTwo.PatternType = ListPatternType.Arabic;
levelTwo.StartAt = 1;
WListLevel levelThree = listStyle.Levels[2];
//Defines the follow character, prefix from previous level, pattern, start index for level 1
levelThree.FollowCharacter = FollowCharacterType.Nothing;
levelThree.NumberPrefix = "\u0000.\u0001.";
levelThree.PatternType = ListPatternType.Arabic;
levelThree.StartAt = 1;
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Adds text to the paragraph
paragraph.AppendText("User defined list - Level 0");
//Applies default numbered list style
paragraph.ListFormat.ApplyStyle("UserDefinedList");
//Adds second paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("User defined list - Level 1");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Increases the level indent
paragraph.ListFormat.IncreaseIndentLevel();
//Adds second paragraph
paragraph = section.AddParagraph();
paragraph.AppendText("User defined list - Level 2");
//Continues last defined list
paragraph.ListFormat.ContinueListNumbering();
//Increases the level indent
paragraph.ListFormat.IncreaseIndentLevel();
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Download the helper files from the following link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}  

### Get list value

You can get the string that represents the appearance of **list value of the paragraph** in the Word document using the `ListString` API. 

This API holds the static string of the list value recently calculated while saving the document as Text. It is not updated automatically for each modification done in the Word document. Hence, you should either invoke the `GetText()` method of `WordDocument` or save the Word document as Text to get the actual list value from this API.

The following example shows how to **get a string that represents the appearance of list value of the paragraph**.

{% tabs %}  

{% highlight C# %}
//Loads an existing Word document
WordDocument document = new WordDocument("Template.docx");
//Gets the document text
document.GetText();
//Gets the string that represents the appearance of list value of the paragraph
String listString = document.LastParagraph.ListString;
//Saves and closes the WordDocument instance
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight VB.NET %}
'Loads an existing Word document
Dim document As WordDocument = New WordDocument("Template.docx")
' Gets the document text
document.GetText()
'Gets the string that represents the appearance of list value of the paragraph
Dim listString As String = document.LastParagraph.ListString
'Saves and closes the WordDocument instance
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight UWP %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Creates an instance of a WordDocument
WordDocument document = new WordDocument();
//Loads an existing Word document
document.Open(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Docx);
//Gets the document text
document.GetText();
//Gets the string that represents the appearance of list value of the paragraph
String listString = document.LastParagraph.ListString;
// Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
//Closes the Word document
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Sample.docx");

//Refer to the following link to save Word document in UWP platform.
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight ASP.NET CORE %}
//Loads an existing Word document
FileStream fileStreamPath = new FileStream("Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);
//Gets the document text
document.GetText();
//Gets the string that represents the appearance of list value of the paragraph
String listString = document.LastParagraph.ListString;        
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Sample.docx");
{% endhighlight %}

{% highlight XAMARIN %}
//Loads an existing Word document
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Docx);
//Gets the document text
document.GetText();
//Gets the string that represents the appearance of list value of the paragraph
String listString = document.LastParagraph.ListString;
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the Word document
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.docx", "application/msword", stream);

//Download the helper files from the following link to save the stream as file and open the file for viewing in Xamarin platform.
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}
{% endtabs %}

N> For a picture bulleted list, the `ListString` API is not valid and it will return an empty string.


## Working with hyperlinks

Hyperlink is a reference to data that can link to external contents like images, files, webpage, and more.  In Word document, a hyperlink may target to any one of the following sources:

* Webpage: Represents the web content.
* File: Represents the file in some location.
* Email: Represents an Email.
* Bookmark: Represents the bookmarks in the document.

Hyperlinks have two parts: the address and display content. 

The following code example explains how to insert a web link.

{% tabs %}  

{% highlight c# %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
paragraph.AppendText("Web Hyperlink:  ");
paragraph = section.AddParagraph();
//Appends web hyperlink to the paragraph
IWField field = paragraph.AppendHyperlink("http://www.syncfusion.com", "Syncfusion", HyperlinkType.WebLink);
//Saves the Word document
document.Save("Sample.docx", FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Creates a new Word document 
Dim document As New WordDocument()
'Adds new section to the document
Dim section As IWSection = document.AddSection()
'Adds new paragraph to the section
Dim paragraph As IWParagraph = section.AddParagraph()
paragraph.AppendText("Web Hyperlink:  ")
paragraph = section.AddParagraph()
'Appends web hyperlink to the paragraph
Dim field As IWField = paragraph.AppendHyperlink("http://www.syncfusion.com", "Syncfusion", HyperlinkType.WebLink)
'Saves the Word document
document.Save("Sample.docx", FormatType.Docx)
'Closes the document
document.Close()
{% endhighlight %}

{% highlight UWP %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
paragraph.AppendText("Web Hyperlink:  ");
paragraph = section.AddParagraph();
//Appends web hyperlink to the paragraph
IWField field = paragraph.AppendHyperlink("http://www.syncfusion.com", "Syncfusion", HyperlinkType.WebLink);
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Refer to the following link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight ASP.NET CORE %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
paragraph.AppendText("Web Hyperlink:  ");
paragraph = section.AddParagraph();
//Appends web hyperlink to the paragraph
IWField field = paragraph.AppendHyperlink("http://www.syncfusion.com", "Syncfusion", HyperlinkType.WebLink);
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %} 

{% highlight XAMARIN %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
paragraph.AppendText("Web Hyperlink:  ");
paragraph = section.AddParagraph();
//Appends web hyperlink to the paragraph
IWField field = paragraph.AppendHyperlink("http://www.syncfusion.com", "Syncfusion", HyperlinkType.WebLink);
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Download the helper files from the following link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %} 

{% endtabs %}  
 
The following code example illustrates how to add an email link.

{% tabs %} 

{% highlight c# %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
paragraph.AppendText("Email hyperlink: ");
paragraph = section.AddParagraph();
//Appends Email hyperlink to the paragraph
paragraph.AppendHyperlink("mailto:sales@syncfusion.com","Sales" , HyperlinkType.EMailLink);
//Saves the Word document
document.Save("Sample.docx", FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Creates a new Word document 
Dim document As New WordDocument()
'Adds new section to the document
Dim section As IWSection = document.AddSection()
'Adds new paragraph to the section
Dim paragraph As IWParagraph = section.AddParagraph()
paragraph.AppendText("Email hyperlink: ")
paragraph = section.AddParagraph()
'Appends Email hyperlink to the paragraph
paragraph.AppendHyperlink("mailto:sales@syncfusion.com","Sales" , HyperlinkType.EMailLink)
'Saves the Word document
document.Save("Sample.docx", FormatType.Docx)
'Closes the document
document.Close()
{% endhighlight %} 

{% highlight UWP %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
paragraph.AppendText("Email hyperlink: ");
paragraph = section.AddParagraph();
//Appends Email hyperlink to the paragraph
paragraph.AppendHyperlink("mailto:sales@syncfusion.com", "Sales", HyperlinkType.EMailLink);
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Refer to the following link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight ASP.NET CORE %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
paragraph.AppendText("Email hyperlink: ");
paragraph = section.AddParagraph();
//Appends Email hyperlink to the paragraph
paragraph.AppendHyperlink("mailto:sales@syncfusion.com", "Sales", HyperlinkType.EMailLink);
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %} 

{% highlight XAMARIN %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
paragraph.AppendText("Email hyperlink: ");
paragraph = section.AddParagraph();
//Appends Email hyperlink to the paragraph
paragraph.AppendHyperlink("mailto:sales@syncfusion.com", "Sales", HyperlinkType.EMailLink);
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Download the helper files from the following link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %} 

{% endtabs %}  

The following code example explains how to add a file hyperlink.

{% tabs %}  

{% highlight c# %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
paragraph.AppendText("File Hyperlinks: ");
paragraph = section.AddParagraph();
//Appends hyperlink field to the paragraph
paragraph.AppendHyperlink(@"Template.docx","File", HyperlinkType.FileLink);
//Saves the Word document
document.Save("Sample.docx", FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Creates a new Word document 
Dim document As New WordDocument()
'Adds new section to the document
Dim section As IWSection = document.AddSection()
'Adds new paragraph to the section
Dim paragraph As IWParagraph = section.AddParagraph()
paragraph.AppendText("File Hyperlinks: ")
paragraph = section.AddParagraph()
'Appends hyperlink field to the paragraph
paragraph.AppendHyperlink("Template.docx", "File", HyperlinkType.FileLink)
'Saves the Word document
document.Save("Sample.docx", FormatType.Docx)
'Closes the document
document.Close()
{% endhighlight %}

{% highlight UWP %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
paragraph.AppendText("File Hyperlinks: ");
paragraph = section.AddParagraph();
//Appends hyperlink field to the paragraph
paragraph.AppendHyperlink(@"Template.docx", "File", HyperlinkType.FileLink);
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();          
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Refer to the following link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight ASP.NET CORE %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
paragraph.AppendText("File Hyperlinks: ");
paragraph = section.AddParagraph();
//Appends hyperlink field to the paragraph
paragraph.AppendHyperlink(@"Template.docx", "File", HyperlinkType.FileLink);
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %} 

{% highlight XAMARIN %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
paragraph.AppendText("File Hyperlinks: ");
paragraph = section.AddParagraph();
//Appends hyperlink field to the paragraph
paragraph.AppendHyperlink(@"Template.docx", "File", HyperlinkType.FileLink);
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);   
//Download the helper files from the following link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin     
{% endhighlight %} 

{% endtabs %}  
  
The following code example explains how to add a bookmark hyperlink.

{% tabs %}  

{% highlight c# %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Creates new Bookmark
paragraph.AppendBookmarkStart("Introduction");
paragraph.AppendText("Hyperlink");
paragraph.AppendBookmarkEnd("Introduction");
paragraph.AppendText("\nA hyperlink is a reference or navigation element in a document to another section of the same document or to another document that may be on or part of a (different) domain.");
paragraph = section.AddParagraph();
paragraph.AppendText("Bookmark Hyperlink: ");
paragraph = section.AddParagraph();
//Appends Bookmark hyperlink to the paragraph
paragraph.AppendHyperlink("Introduction", "Bookmark", HyperlinkType.Bookmark);
//Saves the Word document
document.Save("Sample.docx", FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Creates a new Word document 
Dim document As New WordDocument()
'Adds new section to the document
Dim section As IWSection = document.AddSection()
'Adds new paragraph to the section
Dim paragraph As IWParagraph = section.AddParagraph()
'Creates new Bookmark
paragraph.AppendBookmarkStart("Introduction")
paragraph.AppendText("Hyperlink")
paragraph.AppendBookmarkEnd("Introduction")
paragraph.AppendText(vbLf & "A hyperlink is a reference or navigation element in a document to another section of the same document or to another document that may be on or part of a (different) domain.")
paragraph = section.AddParagraph()
paragraph.AppendText("Bookmark Hyperlink: ")
paragraph = section.AddParagraph()
'Appends Bookmark hyperlink to the paragraph
paragraph.AppendHyperlink("Introduction", "Bookmark", HyperlinkType.Bookmark)
'Saves the Word document
document.Save("Sample.docx", FormatType.Docx)
'Closes the document
document.Close()
{% endhighlight %}

{% highlight UWP %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Creates new Bookmark
paragraph.AppendBookmarkStart("Introduction");
paragraph.AppendText("Hyperlink");
paragraph.AppendBookmarkEnd("Introduction");
paragraph.AppendText("\nA hyperlink is a reference or navigation element in a document to another section of the same document or to another document that may be on or part of a (different) domain.");
paragraph = section.AddParagraph();
paragraph.AppendText("Bookmark Hyperlink: ");
paragraph = section.AddParagraph();
//Appends Bookmark hyperlink to the paragraph
paragraph.AppendHyperlink("Introduction", "Bookmark", HyperlinkType.Bookmark);
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Refer to the following link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight ASP.NET CORE %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Creates new Bookmark
paragraph.AppendBookmarkStart("Introduction");
paragraph.AppendText("Hyperlink");
paragraph.AppendBookmarkEnd("Introduction");
paragraph.AppendText("\nA hyperlink is a reference or navigation element in a document to another section of the same document or to another document that may be on or part of a (different) domain.");
paragraph = section.AddParagraph();
paragraph.AppendText("Bookmark Hyperlink: ");
paragraph = section.AddParagraph();
//Appends Bookmark hyperlink to the paragraph
paragraph.AppendHyperlink("Introduction", "Bookmark", HyperlinkType.Bookmark);
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %} 

{% highlight XAMARIN %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Creates new Bookmark
paragraph.AppendBookmarkStart("Introduction");
paragraph.AppendText("Hyperlink");
paragraph.AppendBookmarkEnd("Introduction");
paragraph.AppendText("\nA hyperlink is a reference or navigation element in a document to another section of the same document or to another document that may be on or part of a (different) domain.");
paragraph = section.AddParagraph();
paragraph.AppendText("Bookmark Hyperlink: ");
paragraph = section.AddParagraph();
//Appends Bookmark hyperlink to the paragraph
paragraph.AppendHyperlink("Introduction", "Bookmark", HyperlinkType.Bookmark);
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Download the helper files from the following link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}  

The display content for the Hyperlinks can also be an image that may redirect to some other contents.

The following code example explains how to add image hyperlink.

{% tabs %}  

{% highlight c# %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
paragraph.AppendText("Image Hyperlink");
paragraph = section.AddParagraph();
//Creates a new image instance and load image 
WPicture picture = new WPicture(document);
picture.LoadImage(Image.FromFile("Image.png"));
//Appends new image hyperlink to the paragraph
paragraph.AppendHyperlink("http://www.syncfusion.com", picture, HyperlinkType.WebLink);
//Saves the Word document
document.Save("Sample.docx", FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Creates a new Word document 
Dim document As New WordDocument()
'Adds new section to the document
Dim section As IWSection = document.AddSection()
'Adds new paragraph to the section
Dim paragraph As IWParagraph = section.AddParagraph()
paragraph.AppendText("Image Hyperlink")
paragraph = section.AddParagraph()
'Creates a new image instance and load image 
Dim picture As New WPicture(document)
picture.LoadImage(Image.FromFile("Image.png"))
'Appends new image hyperlink to the paragraph
paragraph.AppendHyperlink("http://www.syncfusion.com", picture, HyperlinkType.WebLink)
'Saves the Word document
document.Save("Sample.docx", FormatType.Docx)
'Closes the document
document.Close()
{% endhighlight %} 

{% highlight UWP %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
paragraph.AppendText("Image Hyperlink");
paragraph = section.AddParagraph();
//Creates a new image instance and load image 
WPicture picture = new WPicture(document);
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream imageStream = assembly.GetManifestResourceStream("CreateWordSample.Assets.Dummy-Images.jpg");
picture.LoadImage(imageStream);
//Appends new image hyperlink to the paragraph
paragraph.AppendHyperlink("http://www.syncfusion.com", picture, HyperlinkType.WebLink);
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Refer to the following link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight ASP.NET CORE %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
paragraph.AppendText("Image Hyperlink");
paragraph = section.AddParagraph();
//Creates a new image instance and load image 
WPicture picture = new WPicture(document);
FileStream imageStream = new FileStream(@"Mountain-200.jpg", FileMode.Open, FileAccess.ReadWrite);
picture.LoadImage(imageStream);
//Appends new image hyperlink to the paragraph
paragraph.AppendHyperlink("http://www.syncfusion.com", picture, HyperlinkType.WebLink);
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %} 

{% highlight XAMARIN %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
paragraph.AppendText("Image Hyperlink");
paragraph = section.AddParagraph();
//Creates a new image instance and load image 
WPicture picture = new WPicture(document);
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream imageStream = assembly.GetManifestResourceStream("XamarinFormsApp1.Assets.Dummy-Images.jpg");
picture.LoadImage(imageStream);
//Appends new image hyperlink to the paragraph
paragraph.AppendHyperlink("http://www.syncfusion.com", picture, HyperlinkType.WebLink);
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Download the helper files from the following link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %} 

{% endtabs %}  

The following code example explains how to modify the URL of an existing hyperlink.

{% tabs %}  

{% highlight c# %}
//Loads the template document 
WordDocument document = new WordDocument("Sample.docx", FormatType.Docx);
WParagraph paragraph = document.LastParagraph;
//Iterates through the paragraph items
foreach (ParagraphItem item in paragraph.ChildEntities)
{
    if (item is WField)
    {
        if ((item as WField).FieldType == FieldType.FieldHyperlink)
        {
            //Gets the hyperlink field
            Hyperlink link = new Hyperlink(item as WField);
            if (link.Type == HyperlinkType.WebLink)
            {
                //Modifies the url of the hyperlink
                link.Uri = "http://www.google.com";
                link.TextToDisplay = "Google";
                break;
            }
        }
    }
}
//Saves and closes the Word document
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Loads the template document 
Dim document As New WordDocument("Sample.docx", FormatType.Docx)
Dim paragraph As WParagraph = document.LastParagraph
'Iterates through the paragraph items
For Each item As ParagraphItem In paragraph.ChildEntities
	If TypeOf item Is WField Then
		If TryCast(item, WField).FieldType = FieldType.FieldHyperlink Then
			'Gets the hyperlink field
			Dim link As New Hyperlink(TryCast(item, WField))
			If link.Type = HyperlinkType.WebLink Then
				'Modifies the url of the hyperlink
				link.Uri = "http://www.google.com"
				link.TextToDisplay = "Google"
				Exit For
			End If
		End If
	End If
Next
'Saves and closes the Word document
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight UWP %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream fileStream = assembly.GetManifestResourceStream("CreateWordSample.Assets.Sample.docx");
//Loads the template document 
WordDocument document = new WordDocument(fileStream, FormatType.Docx);
WParagraph paragraph = document.LastParagraph;
//Iterates through the paragraph items
foreach (ParagraphItem item in paragraph.ChildEntities)
{
    if (item is WField)
    {
        if ((item as WField).FieldType == FieldType.FieldHyperlink)
        {
            //Gets the hyperlink field
            Hyperlink link = new Hyperlink(item as WField);
            if (link.Type == HyperlinkType.WebLink)
            {
                //Modifies the url of the hyperlink
                link.Uri = "http://www.google.com";
                link.TextToDisplay = "Google";
                break;
            }
        }
    }
}
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight ASP.NET CORE %}
FileStream fileStream = new FileStream(@"Sample.docx", FileMode.Open, FileAccess.ReadWrite);
//Loads the template document 
WordDocument document = new WordDocument(fileStream, FormatType.Docx);
WParagraph paragraph = document.LastParagraph;
//Iterates through the paragraph items
foreach (ParagraphItem item in paragraph.ChildEntities)
{
    if (item is WField)
    {
        if ((item as WField).FieldType == FieldType.FieldHyperlink)
        {
            //Gets the hyperlink field
            Hyperlink link = new Hyperlink(item as WField);
            if (link.Type == HyperlinkType.WebLink)
            {
                //Modifies the url of the hyperlink
                link.Uri = "http://www.google.com";
                link.TextToDisplay = "Google";
                break;
            }
        }
    }
}
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %} 

{% highlight XAMARIN %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream fileStream = assembly.GetManifestResourceStream("XamarinFormsApp1.Assets.Sample.docx");
//Loads the template document 
WordDocument document = new WordDocument(fileStream, FormatType.Docx);
WParagraph paragraph = document.LastParagraph;
//Iterates through the paragraph items
foreach (ParagraphItem item in paragraph.ChildEntities)
{
    if (item is WField)
    {
        if ((item as WField).FieldType == FieldType.FieldHyperlink)
        {
            //Gets the hyperlink field
            Hyperlink link = new Hyperlink(item as WField);
            if (link.Type == HyperlinkType.WebLink)
            {
                //Modifies the url of the hyperlink
                link.Uri = "http://www.google.com";
                link.TextToDisplay = "Google";
                break;
            }
        }
    }
}
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Download the helper files from the following link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %} 

{% endtabs %}  
  
## Working with symbols

Symbols are used to add contents such as currencies, numbers, punctuations, etc. DocIO represents symbols with `WSymbol` instance. Each symbol can be identified with their character codes.

The following code example explains how to add new symbol to the document.

{% tabs %}  

{% highlight c# %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
paragraph.AppendText("Example of adding symbols to the paragraph: ");
//Inserts symbol with character code 100
paragraph.AppendSymbol(100);
//Saves and closes the Word document
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Creates a new Word document 
Dim document As New WordDocument()
'Adds new section to the document
Dim section As IWSection = document.AddSection()
'Adds new paragraph to the section
Dim paragraph As IWParagraph = section.AddParagraph()
paragraph.AppendText("Example of adding symbols to the paragraph: ")
'Inserts symbol with character code 100
paragraph.AppendSymbol(100)
'Saves and closes the Word document
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %} 

{% highlight UWP %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
paragraph.AppendText("Example of adding symbols to the paragraph: ");
//Inserts symbol with character code 100
paragraph.AppendSymbol(100);
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Refer to the following link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight ASP.NET CORE %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
paragraph.AppendText("Example of adding symbols to the paragraph: ");
//Inserts symbol with character code 100
paragraph.AppendSymbol(100);
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %} 

{% highlight XAMARIN %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
paragraph.AppendText("Example of adding symbols to the paragraph: ");
//Inserts symbol with character code 100
paragraph.AppendSymbol(100);
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Download the helper files from the following link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %} 

{% endtabs %}  

The following code example explains how to modify an existing symbol.

{% tabs %} 

{% highlight c# %}
//Loads the template document
WordDocument document = new WordDocument("Sample.docx", FormatType.Docx);
//Gets the textbody content
WTextBody textbody = document.Sections[0].Body;
//Iterates through the paragraphs
foreach (WParagraph paragraph in textbody.Paragraphs)
{
    //Gets the symbol from the paragraph items
    foreach (ParagraphItem item in paragraph.ChildEntities)
    {
        if (item is WSymbol)
        {
            WSymbol symbol = item as WSymbol;
            if (symbol.CharacterCode == 100)
            {
                //Modifies the character code
                symbol.CharacterCode = 40;
                symbol.FontName = "Wingdings";
            }
        }
    }
}
//Saves and closes the Word document
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Loads the template document
Dim document As New WordDocument("Sample.docx", FormatType.Docx)
'Gets the textbody content
Dim textbody As WTextBody = document.Sections(0).Body
'Iterates through the paragraphs
For Each paragraph As WParagraph In textbody.Paragraphs
	'Gets the symbol from the paragraph items
	For Each item As ParagraphItem In paragraph.ChildEntities
		If TypeOf item Is WSymbol Then
			Dim symbol As WSymbol = TryCast(item, WSymbol)
			If symbol.CharacterCode = 100 Then
				'Modifies the character code
				symbol.CharacterCode = 40
				symbol.FontName = "Wingdings"
			End If
		End If
	Next
Next
'Saves and closes the Word document
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %} 

{% highlight UWP %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream fileStream = assembly.GetManifestResourceStream("CreateWordSample.Assets.Sample.docx");
//Loads the template document
WordDocument document = new WordDocument(fileStream, FormatType.Docx);
//Gets the textbody content
WTextBody textbody = document.Sections[0].Body;
//Iterates through the paragraphs
foreach (WParagraph paragraph in textbody.Paragraphs)
{
    //Gets the symbol from the paragraph items
    foreach (ParagraphItem item in paragraph.ChildEntities)
    {
        if (item is WSymbol)
        {
            WSymbol symbol = item as WSymbol;
            if (symbol.CharacterCode == 100)
            {
                //Modifies the character code
                symbol.CharacterCode = 40;
                symbol.FontName = "Wingdings";
            }
        }
    }
}
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Refer to the following link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight ASP.NET CORE %}
FileStream fileStream = new FileStream(@"Sample1.docx", FileMode.Open, FileAccess.ReadWrite);
//Loads the template document
WordDocument document = new WordDocument(fileStream, FormatType.Docx);
//Gets the textbody content
WTextBody textbody = document.Sections[0].Body;
//Iterates through the paragraphs
foreach (WParagraph paragraph in textbody.Paragraphs)
{
    //Gets the symbol from the paragraph items
    foreach (ParagraphItem item in paragraph.ChildEntities)
    {
        if (item is WSymbol)
        {
            WSymbol symbol = item as WSymbol;
            if (symbol.CharacterCode == 100)
            {
                //Modifies the character code
                symbol.CharacterCode = 40;
                symbol.FontName = "Wingdings";
            }
        }
    }
}
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %} 

{% highlight XAMARIN %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream fileStream = assembly.GetManifestResourceStream("XamarinFormsApp1.Assets.Sample1.docx");
//Loads the template document
WordDocument document = new WordDocument(fileStream, FormatType.Docx);
//Gets the textbody content
WTextBody textbody = document.Sections[0].Body;
//Iterates through the paragraphs
foreach (WParagraph paragraph in textbody.Paragraphs)

{
    //Gets the symbol from the paragraph items
    foreach (ParagraphItem item in paragraph.ChildEntities)
    {
        if (item is WSymbol)
        {
            WSymbol symbol = item as WSymbol;
            if (symbol.CharacterCode == 100)
            {
                //Modifies the character code
                symbol.CharacterCode = 40;
                symbol.FontName = "Wingdings";
            }
        }
    }
}
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Download the helper files from the following link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %} 

{% endtabs %}  

## Appending breaks

Breaks allows the document contents to split into multiple parts to customize the appearance of the contents. The following are the types of breaks supported in the DocIO:

* Page break: Starts the content in the next page.
* Line break: Starts the content in new line.
* Column break: Starts the content in the next column.

The following code example explains how various types of breaks can be appended to the paragraphs.

{% tabs %}  

{% highlight c# %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
paragraph.AppendText("Before line break");
//Adds line break to the paragraph
paragraph.AppendBreak(BreakType.LineBreak);
paragraph.AppendText("After line break");
IWParagraph pageBreakPara = section.AddParagraph();
pageBreakPara.AppendText("Before page break");
//Adds page break to the paragraph
pageBreakPara.AppendBreak(BreakType.PageBreak);
pageBreakPara.AppendText("After page break");
IWSection secondSection = document.AddSection();
//Adds columns to the section
secondSection.AddColumn(100, 2);
secondSection.AddColumn(100, 2);
IWParagraph columnBreakPara = secondSection.AddParagraph();
columnBreakPara.AppendText("Before column break");
//Adds column break to the paragraph
columnBreakPara.AppendBreak(BreakType.ColumnBreak);
columnBreakPara.AppendText("After column break");
//Saves and closes the document instance
document.Save("Sample.docx", FormatType.Docx);
document.Close(); 
{% endhighlight %}

{% highlight vb.net %}
'Creates a new Word document 
Dim document As New WordDocument()
'Adds new section to the document
Dim section As IWSection = document.AddSection()
'Adds new paragraph to the section
Dim paragraph As IWParagraph = section.AddParagraph()
paragraph.AppendText("Before line break")
'Adds line break to the paragraph
paragraph.AppendBreak(BreakType.LineBreak)
paragraph.AppendText("After line break")
Dim pageBreakPara As IWParagraph = section.AddParagraph()
pageBreakPara.AppendText("Before page break")
'Adds page break to the paragraph
pageBreakPara.AppendBreak(BreakType.PageBreak)
pageBreakPara.AppendText("After page break")
Dim secondSection As IWSection = document.AddSection()
'Adds columns to the section
secondSection.AddColumn(100, 2)
secondSection.AddColumn(100, 2)
Dim columnBreakPara As IWParagraph = secondSection.AddParagraph()
columnBreakPara.AppendText("Before column break")
'Adds column break to the paragraph
columnBreakPara.AppendBreak(BreakType.ColumnBreak)
columnBreakPara.AppendText("After column break")
'Saves and closes the document instance
document.Save("Sample.docx", FormatType.Docx)
document.Close() 
{% endhighlight %} 

{% highlight UWP %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
paragraph.AppendText("Before line break");
//Adds line break to the paragraph
paragraph.AppendBreak(BreakType.LineBreak);
paragraph.AppendText("After line break");
IWParagraph pageBreakPara = section.AddParagraph();
pageBreakPara.AppendText("Before page break");
//Adds page break to the paragraph
pageBreakPara.AppendBreak(BreakType.PageBreak);
pageBreakPara.AppendText("After page break");
IWSection secondSection = document.AddSection();
//Adds columns to the section
secondSection.AddColumn(100, 2);
secondSection.AddColumn(100, 2);
IWParagraph columnBreakPara = secondSection.AddParagraph();
columnBreakPara.AppendText("Before column break");
//Adds column break to the paragraph
columnBreakPara.AppendBreak(BreakType.ColumnBreak);
columnBreakPara.AppendText("After column break");
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Refer to the following link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight ASP.NET CORE %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
paragraph.AppendText("Before line break");
//Adds line break to the paragraph
paragraph.AppendBreak(BreakType.LineBreak);
paragraph.AppendText("After line break");
IWParagraph pageBreakPara = section.AddParagraph();
pageBreakPara.AppendText("Before page break");
//Adds page break to the paragraph
pageBreakPara.AppendBreak(BreakType.PageBreak);
pageBreakPara.AppendText("After page break");
IWSection secondSection = document.AddSection();    
//Adds columns to the section
secondSection.AddColumn(100, 2);
secondSection.AddColumn(100, 2);
IWParagraph columnBreakPara = secondSection.AddParagraph();
columnBreakPara.AppendText("Before column break");
//Adds column break to the paragraph
columnBreakPara.AppendBreak(BreakType.ColumnBreak);
columnBreakPara.AppendText("After column break");
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %} 

{% highlight XAMARIN %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
paragraph.AppendText("Before line break");
//Adds line break to the paragraph
paragraph.AppendBreak(BreakType.LineBreak);
paragraph.AppendText("After line break");
IWParagraph pageBreakPara = section.AddParagraph();
pageBreakPara.AppendText("Before page break");
//Adds page break to the paragraph
pageBreakPara.AppendBreak(BreakType.PageBreak);
pageBreakPara.AppendText("After page break");
IWSection secondSection = document.AddSection();
//Adds columns to the section
secondSection.AddColumn(100, 2);
secondSection.AddColumn(100, 2);
IWParagraph columnBreakPara = secondSection.AddParagraph();
columnBreakPara.AppendText("Before column break");
//Adds column break to the paragraph
columnBreakPara.AppendBreak(BreakType.ColumnBreak);
columnBreakPara.AppendText("After column break");
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream); 
//Download the helper files from the following link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %} 

{% endtabs %}  

## Appending OLE objects

OLE (Object Linking and Embedding) objects allow embedding and linking to documents and other objects. It allows the content of one program to be used in a Word document. The Objects can be inserted in the following two ways:

* Linked: The content is linked to the source file
* Embedded: The content is copied to the Word document and is not linked to the source file 

You can create and manipulate the OLE Objects of both Linked and Embedded types in the Word document by using `WOleObject` instance.

The following code example explains how to add OLE objects to the document.

{% tabs %}  

{% highlight c# %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Opens the file to be embedded
FileStream stream = new FileStream("Book1.xlsx", FileMode.Open);
//Loads the picture instance with the image need to be displayed
WPicture picture = new WPicture(document);
picture.LoadImage(Image.FromFile("Image.png"));
//Appends the OLE object to the paragraph
WOleObject object = paragraph.AppendOleObject(stream, picture, OleObjectType.ExcelWorksheet);
//Saves the Word document
document.Save("Sample.docx", FormatType.Docx);
//Closes the document
document.Close(); 
{% endhighlight %}

{% highlight vb.net %}
'Creates a new Word document 
Dim document As New WordDocument()
'Adds new section to the document
Dim section As IWSection = document.AddSection()
'Adds new paragraph to the section
Dim paragraph As IWParagraph = section.AddParagraph()
'Opens the file to be embedded
Dim stream As New FileStream("Book1.xlsx", FileMode.Open)
'Loads the picture instance with the image need to be displayed
Dim picture As New WPicture(document)
picture.LoadImage(Image.FromFile("Image.png"))
'Appends the OLE object to the paragraph
Dim object As WOleObject = paragraph.AppendOleObject(stream, picture, OleObjectType.ExcelWorksheet)
'Saves the Word document
document.Save("Sample.docx", FormatType.Docx)
'Closes the document
document.Close() 
{% endhighlight %}

{% highlight UWP %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Opens the file to be embedded
Stream fileStream = assembly.GetManifestResourceStream("CreateWordSample.Assets.Book1.xlsx");
//Loads the picture instance with the image need to be displayed
WPicture picture = new WPicture(document);
Stream imageStream = assembly.GetManifestResourceStream("CreateWordSample.Assets.Image.png");
picture.LoadImage(imageStream);
//Appends the OLE object to the paragraph
WOleObject oleObject = paragraph.AppendOleObject(fileStream, picture, OleObjectType.ExcelWorksheet);
//Saves and closes the Word document instance     
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Refer to the following link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight ASP.NET CORE %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Opens the file to be embedded
FileStream fileStream = new FileStream("Book1.xlsx", FileMode.Open);
//Loads the picture instance with the image need to be displayed
WPicture picture = new WPicture(document);
FileStream imageStream = new FileStream(@"Image.png", FileMode.Open, FileAccess.ReadWrite);
picture.LoadImage(imageStream);
//Appends the OLE object to the paragraph
WOleObject oleObject = paragraph.AppendOleObject(fileStream, picture, OleObjectType.ExcelWorksheet);
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx"); 
{% endhighlight %} 

{% highlight XAMARIN %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Opens the file to be embedded
Stream fileStream = assembly.GetManifestResourceStream("CreateWordSample.Assets.Book1.xlsx");
//Loads the picture instance with the image need to be displayed
WPicture picture = new WPicture(document);
Stream imageStream = assembly.GetManifestResourceStream("CreateWordSample.Assets.Image.png");
picture.LoadImage(imageStream);
//Appends the OLE object to the paragraph
WOleObject oleObject = paragraph.AppendOleObject(fileStream, picture, OleObjectType.ExcelWorksheet);
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Download the helper files from the following link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %} 

{% endtabs %}  
  
## Working with Text Box

Text box contains a group of textual and graphical contents. DocIO supports to create and manipulate the text box and its formatting by using the `WTextBox` instance.

The following code example explains how to add new text box to the paragraph.

{% tabs %}  

{% highlight c# %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Appends new textbox to the paragraph
IWTextBox textbox = paragraph.AppendTextBox(150, 75);
//Adds new text to the textbox body
IWParagraph textboxParagraph = textbox.TextBoxBody.AddParagraph();
textboxParagraph.AppendText("Text inside text box");
textboxParagraph = textbox.TextBoxBody.AddParagraph();
//Adds new picture to textbox body
IWPicture picture = textboxParagraph.AppendPicture(Image.FromFile(@"Image.png"));
picture.Height = 75;
picture.Width = 50;
//Saves and closes the Word document
document.Save("Sample.docx", FormatType.Docx);
document.Close(); 
{% endhighlight %}

{% highlight vb.net %}
'Creates a new Word document 
Dim document As New WordDocument()
'Adds new section to the document
Dim section As IWSection = document.AddSection()
'Adds new paragraph to the section
Dim paragraph As IWParagraph = section.AddParagraph()
'Appends new textbox to the paragraph
Dim textbox As IWTextBox = paragraph.AppendTextBox(150, 75)
'Adds new text to the textbox body
Dim textboxParagraph As IWParagraph = textbox.TextBoxBody.AddParagraph()
textboxParagraph.AppendText("Text inside text box")
textboxParagraph = textbox.TextBoxBody.AddParagraph()
'Adds new picture to textbox body
Dim picture As IWPicture = textboxParagraph.AppendPicture(Image.FromFile("Image.png"))
picture.Height = 75
picture.Width = 50
'Saves and closes the Word document
document.Save("Sample.docx", FormatType.Docx)
document.Close() 
{% endhighlight %} 

{% highlight UWP %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;            
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Appends new textbox to the paragraph
IWTextBox textbox = paragraph.AppendTextBox(150, 75);
//Adds new text to the textbox body
IWParagraph textboxParagraph = textbox.TextBoxBody.AddParagraph();
textboxParagraph.AppendText("Text inside text box");
textboxParagraph = textbox.TextBoxBody.AddParagraph();
//Adds new picture to textbox body
Stream imageStream = assembly.GetManifestResourceStream("CreateWordSample.Assets.Dummy-Images.jpg");
IWPicture picture = textboxParagraph.AppendPicture(imageStream);
picture.Height = 75;
picture.Width = 50;
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Refer to the following link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight ASP.NET CORE %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Appends new textbox to the paragraph
IWTextBox textbox = paragraph.AppendTextBox(150, 75);
//Adds new text to the textbox body
IWParagraph textboxParagraph = textbox.TextBoxBody.AddParagraph();
textboxParagraph.AppendText("Text inside text box");
textboxParagraph = textbox.TextBoxBody.AddParagraph();
//Adds new picture to textbox body
FileStream imagestream = new FileStream(@"Mountain-200.jpg", FileMode.Open, FileAccess.ReadWrite);
IWPicture picture = textboxParagraph.AppendPicture(imagestream);
picture.Height = 75;
picture.Width = 50;
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;          
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %} 

{% highlight XAMARIN %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;        
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Appends new textbox to the paragraph
IWTextBox textbox = paragraph.AppendTextBox(150, 75);
//Adds new text to the textbox body
IWParagraph textboxParagraph = textbox.TextBoxBody.AddParagraph();
textboxParagraph.AppendText("Text inside text box");
textboxParagraph = textbox.TextBoxBody.AddParagraph();
//Adds new picture to textbox body
Stream imageStream = assembly.GetManifestResourceStream("XamarinFormsApp1.Assets.Dummy-Images.jpg");
IWPicture picture = textboxParagraph.AppendPicture(imageStream);
picture.Height = 75;
picture.Width = 50;
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream); 
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %} 

{% endtabs %}

### Format and rotate text box  

Text box has its own formatting such as outline color, fill effects, text direction, wrap formats, and more. You can also rotate the text box and apply flipping (horizontal and vertical) to it.

The following code example explains how to apply formatting and rotation for text box.

{% tabs %}  

{% highlight c# %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Appends new textbox to the paragraph
IWTextBox textbox = paragraph.AppendTextBox(150, 75);
//Adds new text to the textbox body
IWParagraph textboxParagraph = textbox.TextBoxBody.AddParagraph();
textboxParagraph.AppendText("Text inside text box");
//Sets fill color and line width for textbox
textbox.TextBoxFormat.FillColor = Color.LightGreen;
textbox.TextBoxFormat.LineWidth = 2;
//Applies textbox text direction
textbox.TextBoxFormat.TextDirection = Syncfusion.DocIO.DLS.TextDirection.VerticalTopToBottom;
//Sets text wrapping style
textbox.TextBoxFormat.TextWrappingStyle = TextWrappingStyle.InFrontOfText;
//Sets horizontal and vertical position
textbox.TextBoxFormat.HorizontalPosition = 200;
textbox.TextBoxFormat.VerticalPosition = 200; 
//Sets horizontal and vertical origin
textbox.TextBoxFormat.VerticalOrigin = VerticalOrigin.Margin;
textbox.TextBoxFormat.HorizontalOrigin = HorizontalOrigin.Page;
//Sets top and bottom margin values
textbox.TextBoxFormat.InternalMargin.Bottom = 5f;
textbox.TextBoxFormat.InternalMargin.Top = 5f;
//Sets 90 degree rotation
textbox.TextBoxFormat.Rotation = 90;
//Sets horizontal flip
textbox.TextBoxFormat.FlipHorizontal = true;
//Saves and closes the Word document
document.Save("Sample.docx", FormatType.Docx);
document.Close(); 
{% endhighlight %}

{% highlight vb.net %}
'Creates a new Word document 
Dim document As New WordDocument()
'Adds new section to the document
Dim section As IWSection = document.AddSection()
'Adds new paragraph to the section
Dim paragraph As IWParagraph = section.AddParagraph()
'Appends new textbox to the paragraph
Dim textbox As IWTextBox = paragraph.AppendTextBox(150, 75)
'Adds new text to the textbox body
Dim textboxParagraph As IWParagraph = textbox.TextBoxBody.AddParagraph()
textboxParagraph.AppendText("Text inside text box")
'Sets fill color and line width for textbox
textbox.TextBoxFormat.FillColor = Color.LightGreen
textbox.TextBoxFormat.LineWidth = 2
'Applies textbox text direction
textbox.TextBoxFormat.TextDirection = Syncfusion.DocIO.DLS.TextDirection.VerticalTopToBottom
'Sets text wrapping style
textbox.TextBoxFormat.TextWrappingStyle = TextWrappingStyle.InFrontOfText
'Sets horizontal and vertical position
textbox.TextBoxFormat.HorizontalPosition = 200
textbox.TextBoxFormat.VerticalPosition = 200
'Sets horizontal and vertical origin
textbox.TextBoxFormat.VerticalOrigin = VerticalOrigin.Margin
textbox.TextBoxFormat.HorizontalOrigin = HorizontalOrigin.Page
'Sets top and bottom margin values
textbox.TextBoxFormat.InternalMargin.Bottom = 5.0F
textbox.TextBoxFormat.InternalMargin.Top = 5.0F
'Sets 90 degree rotation
textbox.TextBoxFormat.Rotation = 90
'Sets horizontal flip
textbox.TextBoxFormat.FlipHorizontal = true
'Saves and closes the Word document
document.Save("Sample.docx", FormatType.Docx)
document.Close() 
{% endhighlight %}

{% highlight UWP %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Appends new textbox to the paragraph
IWTextBox textbox = paragraph.AppendTextBox(150, 75);
//Adds new text to the textbox body
IWParagraph textboxParagraph = textbox.TextBoxBody.AddParagraph();
textboxParagraph.AppendText("Text inside text box");
//Sets fill color and line width for textbox
textbox.TextBoxFormat.FillColor = Color.LightGreen;
textbox.TextBoxFormat.LineWidth = 2;
//Applies textbox text direction
textbox.TextBoxFormat.TextDirection = Syncfusion.DocIO.DLS.TextDirection.VerticalTopToBottom;
//Sets text wrapping style
textbox.TextBoxFormat.TextWrappingStyle = TextWrappingStyle.InFrontOfText;
//Sets horizontal and vertical position
textbox.TextBoxFormat.HorizontalPosition = 200;
textbox.TextBoxFormat.VerticalPosition = 200;
//Sets horizontal and vertical origin
textbox.TextBoxFormat.VerticalOrigin = VerticalOrigin.Margin;
textbox.TextBoxFormat.HorizontalOrigin = HorizontalOrigin.Page;
//Sets top and bottom margin values
textbox.TextBoxFormat.InternalMargin.Bottom = 5f;
textbox.TextBoxFormat.InternalMargin.Top = 5f;
//Sets 90 degree rotation
textbox.TextBoxFormat.Rotation = 90;
//Sets horizontal flip
textbox.TextBoxFormat.FlipHorizontal = true;
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");

//Refer to the following link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight ASP.NET CORE %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Appends new textbox to the paragraph
IWTextBox textbox = paragraph.AppendTextBox(150, 75);
//Adds new text to the textbox body
IWParagraph textboxParagraph = textbox.TextBoxBody.AddParagraph();
textboxParagraph.AppendText("Text inside text box");
//Sets fill color and line width for textbox
textbox.TextBoxFormat.FillColor = Color.LightGreen;
textbox.TextBoxFormat.LineWidth = 2;
//Applies textbox text direction
textbox.TextBoxFormat.TextDirection = Syncfusion.DocIO.DLS.TextDirection.VerticalTopToBottom;
//Sets text wrapping style
textbox.TextBoxFormat.TextWrappingStyle = TextWrappingStyle.InFrontOfText;
//Sets horizontal and vertical position
textbox.TextBoxFormat.HorizontalPosition = 200;
textbox.TextBoxFormat.VerticalPosition = 200;
//Sets horizontal and vertical origin
textbox.TextBoxFormat.VerticalOrigin = VerticalOrigin.Margin;
textbox.TextBoxFormat.HorizontalOrigin = HorizontalOrigin.Page;
//Sets top and bottom margin values
textbox.TextBoxFormat.InternalMargin.Bottom = 5f;
textbox.TextBoxFormat.InternalMargin.Top = 5f;
//Sets 90 degree rotation
textbox.TextBoxFormat.Rotation = 90;
//Sets horizontal flip
textbox.TextBoxFormat.FlipHorizontal = true;
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %} 

{% highlight XAMARIN %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Appends new textbox to the paragraph
IWTextBox textbox = paragraph.AppendTextBox(150, 75);
//Adds new text to the textbox body
IWParagraph textboxParagraph = textbox.TextBoxBody.AddParagraph();
textboxParagraph.AppendText("Text inside text box");
//Sets fill color and line width for textbox
textbox.TextBoxFormat.FillColor = Syncfusion.Drawing.Color.LightGreen;
textbox.TextBoxFormat.LineWidth = 2;
//Applies textbox text direction
textbox.TextBoxFormat.TextDirection = Syncfusion.DocIO.DLS.TextDirection.VerticalTopToBottom;
//Sets text wrapping style
textbox.TextBoxFormat.TextWrappingStyle = TextWrappingStyle.InFrontOfText;
//Sets horizontal and vertical position
textbox.TextBoxFormat.HorizontalPosition = 200;
textbox.TextBoxFormat.VerticalPosition = 200;
//Sets horizontal and vertical origin
textbox.TextBoxFormat.VerticalOrigin = VerticalOrigin.Margin;
textbox.TextBoxFormat.HorizontalOrigin = HorizontalOrigin.Page;
//Sets top and bottom margin values
textbox.TextBoxFormat.InternalMargin.Bottom = 5f;
textbox.TextBoxFormat.InternalMargin.Top = 5f;
//Sets 90 degree rotation
textbox.TextBoxFormat.Rotation = 90;
//Sets horizontal flip
textbox.TextBoxFormat.FlipHorizontal = true;
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);

//Download the helper files from the following link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %} 

{% endtabs %}  