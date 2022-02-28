---
title: Working with Content Controls | DocIO | Syncfusion
description: This section illustrates how to work with Content Controls in the Word document using Syncfusion Word library (Essential DocIO)
platform: file-formats
control: DocIO
documentation: UG
---

# Working with Content Controls

## What is Content Control?

Content controls are individual controls that you can add and customize to use in templates, forms, and documents. For example, many online forms are designed with a drop-down list control that provides a restricted set of choices.

N> You can use content controls only in documents that are saved in the Open XML Format and cannot be used in the Word 97-2003 document (.doc) format.

Content controls can be categorized based on its occurrence in a document as follows,

* InlineContentControl: Among inline content inside, as a child of a paragraph.
* BlockContentControl: Among paragraphs and tables, as a child of a Body, HeaderFooter, Comment, Footnote, or a Shape node.

### Block Content Control

You can add content control to a text body of the Word document using block content control. You can add text, tables, pictures, or other items into the block content control. Refer to the following code.

{% tabs %}
{% highlight c# %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
WTextBody textBody = section.Body;
//Adds block content control into Word document
BlockContentControl blockContentControl = textBody.AddBlockContentControl(ContentControlType.RichText) as BlockContentControl;
//Adds new paragraph in the block content control
WParagraph paragraph = blockContentControl.TextBody.AddParagraph() as WParagraph;
//Adds new text to the paragraph
paragraph.AppendText("Block content control");
//Adds new table to the block content control
WTable table = blockContentControl.TextBody.AddTable() as WTable;
//Specifies the total number of rows and columns
table.ResetCells(2, 3);
//Adds new paragraph to the block content control
paragraph = blockContentControl.TextBody.AddParagraph() as WParagraph;
//Adds image to the paragraph
paragraph.AppendPicture(Image.FromFile("Image.png"));
//Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Creates a new Word document 
Dim document As WordDocument = New WordDocument
'Adds new section to the document
Dim section As IWSection = document.AddSection
Dim textBody As WTextBody = section.Body
'Adds block content control into Word document
Dim blockContentControl As BlockContentControl = CType(textBody.AddBlockContentControl(ContentControlType.RichText), BlockContentControl)
'Adds new paragraph in the block content control
Dim paragraph As WParagraph = CType(blockContentControl.TextBody.AddParagraph, WParagraph)
'Adds new text to the paragraph
paragraph.AppendText("Block content control")
'Adds new table to the block content control
Dim table As WTable = CType(blockContentControl.TextBody.AddTable, WTable)
'Specifies the total number of rows and columns
table.ResetCells(2, 3)
'Adds new paragraph to the block content control
paragraph = CType(blockContentControl.TextBody.AddParagraph, WParagraph)
'Adds image to the paragraph
paragraph.AppendPicture(Image.FromFile("Image.png"))
'Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight UWP %}
//Creates a new Word document
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
WTextBody textBody = section.Body;
//Adds block content control into Word document
BlockContentControl blockContentControl = textBody.AddBlockContentControl(ContentControlType.RichText) as BlockContentControl;
//Adds new paragraph in the block content control
WParagraph paragraph = blockContentControl.TextBody.AddParagraph() as WParagraph;
//Adds new text to the paragraph
paragraph.AppendText("Block content control");
//Adds new table to the block content control
WTable table = blockContentControl.TextBody.AddTable() as WTable;
//Specifies the total number of rows and columns
table.ResetCells(2, 3);
//Adds new paragraph to the block content control
paragraph = blockContentControl.TextBody.AddParagraph() as WParagraph;
//Adds image to the paragraph
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream pictureStream = assembly.GetManifestResourceStream("Sample.Assets.Image.png");
paragraph.AppendPicture(pictureStream);
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
Save(stream, "Result.docx");
document.Close();
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight ASP.NET CORE %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
WTextBody textBody = section.Body;
//Adds block content control into Word document
BlockContentControl blockContentControl = textBody.AddBlockContentControl(ContentControlType.RichText) as BlockContentControl;
//Adds new paragraph in the block content control
WParagraph paragraph = blockContentControl.TextBody.AddParagraph() as WParagraph;
//Adds new text to the paragraph
paragraph.AppendText("Block content control");
//Adds new table to the block content control
WTable table = blockContentControl.TextBody.AddTable() as WTable;
//Specifies the total number of rows and columns
table.ResetCells(2, 3);
//Adds new paragraph to the block content control
paragraph = blockContentControl.TextBody.AddParagraph() as WParagraph;
//Gets the image stream
FileStream imageStream = new FileStream(@"D:\Image.png", FileMode.Open, FileAccess.Read);
//Adds image to the paragraph
paragraph.AppendPicture(imageStream);
//Creates memory stream
MemoryStream outputStream = new MemoryStream();
//Saves and closes the Word document instance
document.Save(outputStream, FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight XAMARIN %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
WTextBody textBody = section.Body;
//Adds block content control into Word document
BlockContentControl blockContentControl = textBody.AddBlockContentControl(ContentControlType.RichText) as BlockContentControl;
//Adds new paragraph in the block content control
WParagraph paragraph = blockContentControl.TextBody.AddParagraph() as WParagraph;
//Adds new text to the paragraph
paragraph.AppendText("Block content control");
//Adds new table to the block content control
WTable table = blockContentControl.TextBody.AddTable() as WTable;
//Specifies the total number of rows and columns
table.ResetCells(2, 3);
//Adds new paragraph to the block content control
paragraph = blockContentControl.TextBody.AddParagraph() as WParagraph;
//Adds image to the paragraph
Stream imageStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Image.png");
//Adds image from stream
paragraph.AppendPicture(imageStream);
//Creates memory stream
MemoryStream outputStream = new MemoryStream();
//Saves and closes the Word document instance
document.Save(outputStream, FormatType.Docx);
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", outputStream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
document.Close();
{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Content-Controls/Block-content-control).

### Inline Content Control

You can add content control as a child to a paragraph using the inline content control. You can add text, pictures, fields or other paragraph items into the inline content control. Refer to the following code.

{% tabs %}
{% highlight c# %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds one section and one paragraph to the document
document.EnsureMinimal();
//Gets the last paragraph
WParagraph paragraph = document.LastParagraph;
//Adds text to the paragraph
paragraph.AppendText("A new text is added to the paragraph. ");
//Appends inline content control to the paragraph
InlineContentControl inlineContentControl = paragraph.AppendInlineContentControl(ContentControlType.RichText) as InlineContentControl;
WTextRange textRange = new WTextRange(document);
textRange.Text = "Inline content control ";
//Adds new text to the inline content control
inlineContentControl.ParagraphItems.Add(textRange);
//Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Creates a new Word document 
Dim document As WordDocument = New WordDocument
'Adds one section and one paragraph to the document
document.EnsureMinimal()
'Adds new paragraph to the section
Dim paragraph As WParagraph = document.LastParagraph
'Adds text to the paragraph
paragraph.AppendText("A new text is added to the paragraph. ")
'Appends inline content control to the paragraph
Dim inlineContentControl As InlineContentControl = CType(paragraph.AppendInlineContentControl(ContentControlType.RichText), InlineContentControl)
Dim textRange As WTextRange = New WTextRange(document)
textRange.Text = "Inline content control "
'Adds new text to the inline content control
inlineContentControl.ParagraphItems.Add(textRange)
'Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight UWP %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds one section and one paragraph to the document
document.EnsureMinimal();
//Gets the last paragraph
WParagraph paragraph = document.LastParagraph;
//Adds text to the paragraph
paragraph.AppendText("A new text is added to the paragraph. ");
//Appends inline content control to the paragraph
InlineContentControl inlineContentControl = paragraph.AppendInlineContentControl(ContentControlType.RichText) as InlineContentControl;
WTextRange textRange = new WTextRange(document);
textRange.Text = "Inline content control ";
//Adds new text to the inline content control
inlineContentControl.ParagraphItems.Add(textRange);
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
document.Close();
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight ASP.NET CORE %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds one section and one paragraph to the document
document.EnsureMinimal();
//Gets the last paragraph
WParagraph paragraph = document.LastParagraph;
//Adds text to the paragraph
paragraph.AppendText("A new text is added to the paragraph. ");
//Appends inline content control to the paragraph
InlineContentControl inlineContentControl = paragraph.AppendInlineContentControl(ContentControlType.RichText) as InlineContentControl;
WTextRange textRange = new WTextRange(document);
textRange.Text = "Inline content control ";
//Adds new text to the inline content control
inlineContentControl.ParagraphItems.Add(textRange);
//Creates memory stream.
MemoryStream outputStream = new MemoryStream();
//Saves and closes the Word document instance
document.Save(outputStream, FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight XAMARIN %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds one section and one paragraph to the document
document.EnsureMinimal();
//Gets the last paragraph
WParagraph paragraph = document.LastParagraph;
//Adds text to the paragraph
paragraph.AppendText("A new text is added to the paragraph. ");
//Appends inline content control to the paragraph
InlineContentControl inlineContentControl = paragraph.AppendInlineContentControl(ContentControlType.RichText) as InlineContentControl;
WTextRange textRange = new WTextRange(document);
textRange.Text = "Inline content control ";
//Adds new text to the inline content control
inlineContentControl.ParagraphItems.Add(textRange);
//Creates memory stream
MemoryStream outputStream = new MemoryStream();
//Saves and closes the Word document instance
document.Save(outputStream, FormatType.Docx);
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", outputStream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
document.Close();
{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Content-Controls/Inline-content-control).

N> Currently, DocIO does not support RowContentControl and CellContentControl.

## Common properties of Content Control

You can set formatting options for the content control in the Word document. The following are the common properties of a content control.

### Title

The title of the content control. 

### Tag

The tag value to identify the content control.

### Appearance

This property allows you to define the appearance of the content controls. The appearance can be any one of the following:

* BoundingBox: Displays the contents of content control within a box.
* Tags: Displays the contents of content control within tags.
* Hidden: Displays the contents of content control without any box or tags.

### Color

Defines the color of the content control.

### Temporary 

This property defines whether to remove a content control from the Word document when you edit the contents of the content control.

### Lock Contents

Locking the contents of the content control. It restricts to modify the contents of the content control.

### Lock Content Control

It restricts to remove or delete the content control.

### Example – Content Control Common properties

The following code sample illustrates the content control properties usage.

{% tabs %}
{% highlight c# %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds one section and one paragraph to the document
document.EnsureMinimal();
//Gets the last paragraph
WParagraph paragraph = document.LastParagraph;
//Adds text to the paragraph
paragraph.AppendText("A new text is added to the paragraph. ");
//Appends rich text content control to the paragraph
IInlineContentControl contentControl = paragraph.AppendInlineContentControl(ContentControlType.RichText) as InlineContentControl;
WTextRange textRange = new WTextRange(document);
textRange.Text = "Rich text content control.";
//Adds new text to the rich text content control
contentControl.ParagraphItems.Add(textRange);
//Sets tag appearance for the content control
contentControl.ContentControlProperties.Appearance = ContentControlAppearance.Tags;
//Sets a tag property to identify the content control
contentControl.ContentControlProperties.Tag = "Rich Text";
//Sets a title for the content control
contentControl.ContentControlProperties.Title = "Text";
//Sets the color for the content control
contentControl.ContentControlProperties.Color = Color.Magenta;
//Gets the type of content control
ContentControlType controlType = contentControl.ContentControlProperties.Type;
//Enables content control lock
contentControl.ContentControlProperties.LockContentControl = true;
//Protects the contents of content control
contentControl.ContentControlProperties.LockContents = true;
//Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Creates a new Word document 
Dim document As WordDocument = New WordDocument
'Adds one section and one paragraph to the document
document.EnsureMinimal()
'Adds new paragraph to the section
Dim paragraph As WParagraph = document.LastParagraph
'Adds text to the paragraph
paragraph.AppendText("A new text is added to the paragraph. ")
'Appends rich text content control to the paragraph
Dim contentControl As IInlineContentControl = CType(paragraph.AppendInlineContentControl(ContentControlType.RichText), InlineContentControl)
Dim textRange As WTextRange = New WTextRange(document)
textRange.Text = "Rich text content control."
'Adds new text to the rich text content control
contentControl.ParagraphItems.Add(textRange)
'Sets tag appearance for the content control
contentControl.ContentControlProperties.Appearance = ContentControlAppearance.Tags
'Sets a tag property to identify the content control
contentControl.ContentControlProperties.Tag = "Rich Text"
'Sets a title for the content control
contentControl.ContentControlProperties.Title = "Text"
'Sets the color for the content control
contentControl.ContentControlProperties.Color = Color.Magenta
'Gets the type of content control
Dim controlType As ContentControlType = contentControl.ContentControlProperties.Type
'Enables content control lock
contentControl.ContentControlProperties.LockContentControl = True
'Protects the contents of content control
contentControl.ContentControlProperties.LockContents = True
'Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight UWP %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds one section and one paragraph to the document
document.EnsureMinimal();
//Gets the last paragraph
WParagraph paragraph = document.LastParagraph;
//Adds text to the paragraph
paragraph.AppendText("A new text is added to the paragraph. ");
//Appends rich text content control to the paragraph
IInlineContentControl contentControl = paragraph.AppendInlineContentControl(ContentControlType.RichText) as InlineContentControl;
WTextRange textRange = new WTextRange(document);
textRange.Text = "Rich text content control.";
//Adds new text to the rich text content control
contentControl.ParagraphItems.Add(textRange);
//Sets tag appearance for the content control
contentControl.ContentControlProperties.Appearance = ContentControlAppearance.Tags;
//Sets a tag property to identify the content control
contentControl.ContentControlProperties.Tag = "Rich Text";
//Sets a title for the content control
contentControl.ContentControlProperties.Title = "Text";
//Sets the color for the content control
contentControl.ContentControlProperties.Color = Color.Magenta;
//Gets the type of content control
ContentControlType controlType = contentControl.ContentControlProperties.Type;
//Enables content control lock
contentControl.ContentControlProperties.LockContentControl = true;
//Protects the contents of content control
contentControl.ContentControlProperties.LockContents = true;
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word file in local machine
Save(stream, "Sample.docx");
document.Close();
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight ASP.NET CORE %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds one section and one paragraph to the document
document.EnsureMinimal();
//Gets the last paragraph
WParagraph paragraph = document.LastParagraph;
//Adds text to the paragraph
paragraph.AppendText("A new text is added to the paragraph. ");
//Appends rich text content control to the paragraph
IInlineContentControl contentControl = paragraph.AppendInlineContentControl(ContentControlType.RichText) as InlineContentControl;
WTextRange textRange = new WTextRange(document);
textRange.Text = "Rich text content control.";
//Adds new text to the rich text content control
contentControl.ParagraphItems.Add(textRange);
//Sets tag appearance for the content control
contentControl.ContentControlProperties.Appearance = ContentControlAppearance.Tags;
//Sets a tag property to identify the content control
contentControl.ContentControlProperties.Tag = "Rich Text";
//Sets a title for the content control
contentControl.ContentControlProperties.Title = "Text";
//Sets the color for the content control
contentControl.ContentControlProperties.Color = Syncfusion.Drawing.Color.Magenta;
//Gets the type of content control
ContentControlType controlType = contentControl.ContentControlProperties.Type;
//Enables content control lock
contentControl.ContentControlProperties.LockContentControl = true;
//Protects the contents of content control
contentControl.ContentControlProperties.LockContents = true;
//Creates memory stream
MemoryStream outputStream = new MemoryStream();
//Saves and closes the Word document instance
document.Save(outputStream, FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight XAMARIN %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds one section and one paragraph to the document
document.EnsureMinimal();
//Gets the last paragraph
WParagraph paragraph = document.LastParagraph;
//Adds text to the paragraph
paragraph.AppendText("A new text is added to the paragraph. ");
//Appends rich text content control to the paragraph
IInlineContentControl contentControl = paragraph.AppendInlineContentControl(ContentControlType.RichText) as InlineContentControl;
WTextRange textRange = new WTextRange(document);
textRange.Text = "Rich text content control.";
//Adds new text to the rich text content control
contentControl.ParagraphItems.Add(textRange);
//Sets tag appearance for the content control
contentControl.ContentControlProperties.Appearance = ContentControlAppearance.Tags;
//Sets a tag property to identify the content control
contentControl.ContentControlProperties.Tag = "Rich Text";
//Sets a title for the content control
contentControl.ContentControlProperties.Title = "Text";
//Sets the color for the content control
contentControl.ContentControlProperties.Color = Syncfusion.Drawing.Color.Magenta;
//Gets the type of content control
ContentControlType controlType = contentControl.ContentControlProperties.Type;
//Enables content control lock
contentControl.ContentControlProperties.LockContentControl = true;
//Protects the contents of content control
contentControl.ContentControlProperties.LockContents = true;
//Creates memory stream
MemoryStream outputStream = new MemoryStream();
//Saves and closes the Word document instance
document.Save(outputStream, FormatType.Docx);
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", outputStream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
document.Close();
{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Content-Controls/Content-control-properties).

## Why Content Control?

The content controls have the following three major use cases:

* Protection
* Form Filling
* Data Binding with Content Controls (XML Mapping)

### Protection

Content controls provides options to prevent users from editing or deleting parts of a Word document contents. This is useful if you have information in a Word document or template that you should be able to read but not edit, or if you want to be able to edit content controls but not delete them. 

To protect contents inside a content control, you can use properties of the content control to prevent editing or deleting the content control:

* The **LockContents** property prevents from editing the contents of the content control.
* The **LockContentControl** property prevents from deleting the content control.

The following code sample shows how to protect the content control and its contents.

{% tabs %}
{% highlight c# %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds one section and one paragraph to the document
document.EnsureMinimal();
//Gets the last paragraph
WParagraph paragraph = document.LastParagraph;
//Adds text to the paragraph
paragraph.AppendText("A new text is added to the paragraph. ");
//Appends rich text content control to the paragraph
IInlineContentControl contentControl = paragraph.AppendInlineContentControl(ContentControlType.RichText) as InlineContentControl;
WTextRange textRange = new WTextRange(document);
textRange.Text = "Rich text content control.";
//Adds new text to the rich text content control
contentControl.ParagraphItems.Add(textRange);
//Sets tag appearance for the content control
contentControl.ContentControlProperties.Appearance = ContentControlAppearance.Tags;
//Sets a tag property to identify the content control
contentControl.ContentControlProperties.Tag = "Rich Text Protected";
//Sets a title for the content control
contentControl.ContentControlProperties.Title = "Text Protected";
//Enables content control lock
contentControl.ContentControlProperties.LockContentControl = true;
//Protects the contents of content control
contentControl.ContentControlProperties.LockContents = true;
//Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Creates a new Word document 
Dim document As WordDocument = New WordDocument
'Adds one section and one paragraph to the document
document.EnsureMinimal()
'Adds new paragraph to the section
Dim paragraph As WParagraph = document.LastParagraph
'Adds text to the paragraph
paragraph.AppendText("A new text is added to the paragraph. ")
'Appends rich text content control to the paragraph
Dim contentControl As IInlineContentControl = CType(paragraph.AppendInlineContentControl(ContentControlType.RichText), InlineContentControl)
Dim textRange As WTextRange = New WTextRange(document)
textRange.Text = "Rich text content control."
'Adds new text to the rich text content control
contentControl.ParagraphItems.Add(textRange)
'Sets tag appearance for the content control
contentControl.ContentControlProperties.Appearance = ContentControlAppearance.Tags
'Sets a tag property to identify the content control
contentControl.ContentControlProperties.Tag = "Rich Text Protected"
'Sets a title for the content control
contentControl.ContentControlProperties.Title = "Text Protected"
'Enables content control lock
contentControl.ContentControlProperties.LockContentControl = True
'Protects the contents of content control
contentControl.ContentControlProperties.LockContents = True
'Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight UWP %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds one section and one paragraph to the document
document.EnsureMinimal();
//Gets the last paragraph
WParagraph paragraph = document.LastParagraph;
//Adds text to the paragraph
paragraph.AppendText("A new text is added to the paragraph. ");
//Appends rich text content control to the paragraph
IInlineContentControl contentControl = paragraph.AppendInlineContentControl(ContentControlType.RichText) as InlineContentControl;
WTextRange textRange = new WTextRange(document);
textRange.Text = "Rich text content control.";
//Adds new text to the rich text content control
contentControl.ParagraphItems.Add(textRange);
//Sets tag appearance for the content control
contentControl.ContentControlProperties.Appearance = ContentControlAppearance.Tags;
//Sets a tag property to identify the content control
contentControl.ContentControlProperties.Tag = "Rich Text Protected";
//Sets a title for the content control
contentControl.ContentControlProperties.Title = "Text Protected";
//Enables content control lock
contentControl.ContentControlProperties.LockContentControl = true;
//Protects the contents of content control
contentControl.ContentControlProperties.LockContents = true;
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word file in local machine
Save(stream, "Sample.docx");
document.Close();
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight ASP.NET CORE %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds one section and one paragraph to the document
document.EnsureMinimal();
//Gets the last paragraph
WParagraph paragraph = document.LastParagraph;
//Adds text to the paragraph
paragraph.AppendText("A new text is added to the paragraph. ");
//Appends rich text content control to the paragraph
IInlineContentControl contentControl = paragraph.AppendInlineContentControl(ContentControlType.RichText) as InlineContentControl;
WTextRange textRange = new WTextRange(document);
textRange.Text = "Rich text content control.";
//Adds new text to the rich text content control
contentControl.ParagraphItems.Add(textRange);
//Sets tag appearance for the content control
contentControl.ContentControlProperties.Appearance = ContentControlAppearance.Tags;
//Sets a tag property to identify the content control
contentControl.ContentControlProperties.Tag = "Rich Text Protected";
//Sets a title for the content control
contentControl.ContentControlProperties.Title = "Text Protected";
//Enables content control lock
contentControl.ContentControlProperties.LockContentControl = true;
//Protects the contents of content control
contentControl.ContentControlProperties.LockContents = true;
//Creates memory stream
MemoryStream outputStream = new MemoryStream();
//Saves and closes the Word document instance
document.Save(outputStream, FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight XAMARIN %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds one section and one paragraph to the document
document.EnsureMinimal();
//Gets the last paragraph
WParagraph paragraph = document.LastParagraph;
//Adds text to the paragraph
paragraph.AppendText("A new text is added to the paragraph. ");
//Appends rich text content control to the paragraph
IInlineContentControl contentControl = paragraph.AppendInlineContentControl(ContentControlType.RichText) as InlineContentControl;
WTextRange textRange = new WTextRange(document);
textRange.Text = "Rich text content control.";
//Adds new text to the rich text content control
contentControl.ParagraphItems.Add(textRange);
//Sets tag appearance for the content control
contentControl.ContentControlProperties.Appearance = ContentControlAppearance.Tags;
//Sets a tag property to identify the content control
contentControl.ContentControlProperties.Tag = "Rich Text Protected";
//Sets a title for the content control
contentControl.ContentControlProperties.Title = "Text Protected";
//Enables content control lock
contentControl.ContentControlProperties.LockContentControl = true;
//Protects the contents of content control
contentControl.ContentControlProperties.LockContents = true;
//Creates memory stream
MemoryStream outputStream = new MemoryStream();
//Saves and closes the Word document instance
document.Save(outputStream, FormatType.Docx);
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", outputStream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
document.Close();
{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Content-Controls/Protect-content-control).

### Form Filling

Another major use case is to create the forms. You can design your own forms for various stages using the text box, check box, and list box. Refer to the following code example. 

Form creation:

{% tabs %}
{% highlight c# %}
//Create a new document
WordDocument document = new WordDocument();
//Adding a new section to the document
IWSection section = document.AddSection();
//Adding a new paragraph to the section
IWParagraph paragraph = section.AddParagraph();

#region Document formatting
//Sets background color for document
document.Background.Gradient.Color1 = System.Drawing.Color.FromArgb(232, 232, 232);
document.Background.Gradient.Color2 = System.Drawing.Color.FromArgb(255, 255, 255);
document.Background.Type = BackgroundType.Gradient;
document.Background.Gradient.ShadingStyle = GradientShadingStyle.Horizontal;
document.Background.Gradient.ShadingVariant = GradientShadingVariant.ShadingDown;
//Sets page size for document
section.PageSetup.Margins.All = 30f;
section.PageSetup.PageSize = new System.Drawing.SizeF(600, 600f);
#endregion

#region Title Section
//Adds a new table to the section
IWTable table = section.Body.AddTable();
table.ResetCells(1, 2);
//Gets the table first row
WTableRow row = table.Rows[0];
row.Height = 25f;
//Adds a new paragraph to the cell
IWParagraph cellPara = row.Cells[0].AddParagraph();
//Appends a new picture
IWPicture pic = cellPara.AppendPicture(System.Drawing.Image.FromFile(@"D:\image.jpg"));
pic.Height = 80;
pic.Width = 180;
//Adds a new paragraph to the next cell
cellPara = row.Cells[1].AddParagraph();
row.Cells[1].CellFormat.VerticalAlignment = Syncfusion.DocIO.DLS.VerticalAlignment.Middle;
row.Cells[1].CellFormat.BackColor = System.Drawing.Color.FromArgb(173, 215, 255);
//Appends the text
IWTextRange txt = cellPara.AppendText("Job Application Form");
cellPara.ParagraphFormat.HorizontalAlignment = Syncfusion.DocIO.DLS.HorizontalAlignment.Center;
//Sets the formats
txt.CharacterFormat.Bold = true;
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.FontSize = 18f;
//Sets the width and border type
row.Cells[0].Width = 200;
row.Cells[1].Width = 300;
row.Cells[1].CellFormat.Borders.BorderType = Syncfusion.DocIO.DLS.BorderStyle.Hairline;
#endregion
//Adds a new paragraph
section.AddParagraph();

#region General Information
//Adds a new table
table = section.Body.AddTable();
table.ResetCells(2, 1);
row = table.Rows[0];
row.Height = 20;
row.Cells[0].Width = 500;
//Adds a new paragraph
cellPara = row.Cells[0].AddParagraph();
//Sets a border type, color, background, and vertical alignment for cell
row.Cells[0].CellFormat.Borders.BorderType = Syncfusion.DocIO.DLS.BorderStyle.Thick;
row.Cells[0].CellFormat.Borders.Color = System.Drawing.Color.FromArgb(155, 205, 255);
row.Cells[0].CellFormat.BackColor = System.Drawing.Color.FromArgb(198, 227, 255);
row.Cells[0].CellFormat.VerticalAlignment = Syncfusion.DocIO.DLS.VerticalAlignment.Middle;
txt = cellPara.AppendText(" General Information");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.Bold = true;
txt.CharacterFormat.FontSize = 11f;
row = table.Rows[1];
cellPara = row.Cells[0].AddParagraph();
//Sets a width, border type, color and background for cell
row.Cells[0].Width = 500;
row.Cells[0].CellFormat.Borders.BorderType = Syncfusion.DocIO.DLS.BorderStyle.Hairline;
row.Cells[0].CellFormat.Borders.Color = System.Drawing.Color.FromArgb(155, 205, 255);
row.Cells[0].CellFormat.BackColor = System.Drawing.Color.FromArgb(222, 239, 255);
//Appends a text to paragraph of cell
txt = cellPara.AppendText("\n Full Name:\t\t\t\t");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.FontSize = 11f;
//Appends a new inline content control to enter the value
InlineContentControl txtField = cellPara.AppendInlineContentControl(ContentControlType.Text) as InlineContentControl;
txtField.ContentControlProperties.Title = "Text";
//Sets formatting options for text present inside a content control
txtField.BreakCharacterFormat.TextColor = System.Drawing.Color.MidnightBlue;
txtField.BreakCharacterFormat.FontName = "Arial";
txtField.BreakCharacterFormat.FontSize = 11f;
//Appends a text to paragraph of cell
txt = cellPara.AppendText("\n\n Birth Date:\t\t\t\t");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.FontSize = 11f;
//Appends a new inline content control to enter the value
txtField = cellPara.AppendInlineContentControl(ContentControlType.Date) as InlineContentControl;
txtField.ContentControlProperties.Title = "Date";
//Sets the date display format
txtField.ContentControlProperties.DateDisplayFormat = "M/d/yyyy";
//Sets formatting options for text present inside a content control
txtField.BreakCharacterFormat.TextColor = System.Drawing.Color.MidnightBlue;
txtField.BreakCharacterFormat.FontName = "Arial";
txtField.BreakCharacterFormat.FontSize = 11f;
//Appends a text to paragraph of cell
txt = cellPara.AppendText("\n\n Address:\t\t\t\t");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.FontSize = 11f;
//Appends a new inline content control to enter the value
txtField = cellPara.AppendInlineContentControl(ContentControlType.Text) as InlineContentControl;
txtField.ContentControlProperties.Title = "Text";
//Sets multiline property to true to get the multiple line input of Address
txtField.ContentControlProperties.Multiline = true;
//Sets formatting options for text present inside a content control
txtField.BreakCharacterFormat.TextColor = System.Drawing.Color.MidnightBlue;
txtField.BreakCharacterFormat.FontName = "Arial";
txtField.BreakCharacterFormat.FontSize = 11f;
//Appends a text to paragraph of cell
txt = cellPara.AppendText("\n\n Phone:\t\t\t\t");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.FontSize = 11f;
//Appends a new inline content control to enter the value
txtField = cellPara.AppendInlineContentControl(ContentControlType.Text) as InlineContentControl;
txtField.ContentControlProperties.Title = "Text";
//Sets formatting options for text present inside a content control
txtField.BreakCharacterFormat.TextColor = System.Drawing.Color.MidnightBlue;
txtField.BreakCharacterFormat.FontName = "Arial";
txtField.BreakCharacterFormat.FontSize = 11f;
//Appends a text to paragraph of cell
txt = cellPara.AppendText("\n\n Email:\t\t\t\t\t");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.FontSize = 11f;
//Appends a new inline content control to enter the value
txtField = cellPara.AppendInlineContentControl(ContentControlType.Text) as InlineContentControl;
txtField.ContentControlProperties.Title = "Text";
//Sets formatting options for text present inside a content control
txtField.BreakCharacterFormat.TextColor = System.Drawing.Color.MidnightBlue;
txtField.BreakCharacterFormat.FontName = "Arial";
txtField.BreakCharacterFormat.FontSize = 11f;
cellPara.AppendText("\n");
#endregion
section.AddParagraph();

#region Educational Qualification
//Adds a new table to the section
table = section.Body.AddTable();
table.ResetCells(2, 1);
row = table.Rows[0];
row.Height = 20;
//Sets width, border type, color, background and vertical alignment for cell
row.Cells[0].Width = 500;
row.Cells[0].CellFormat.Borders.BorderType = Syncfusion.DocIO.DLS.BorderStyle.Thick;
row.Cells[0].CellFormat.Borders.Color = System.Drawing.Color.FromArgb(155, 205, 255);
row.Cells[0].CellFormat.BackColor = System.Drawing.Color.FromArgb(198, 227, 255);
row.Cells[0].CellFormat.VerticalAlignment = Syncfusion.DocIO.DLS.VerticalAlignment.Middle;
cellPara = row.Cells[0].AddParagraph();
//Appends a text to paragraph of cell
txt = cellPara.AppendText(" Educational Qualification");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.Bold = true;
txt.CharacterFormat.FontSize = 11f;
row = table.Rows[1];
//Sets width, border type, color, and background for cell
row.Cells[0].Width = 500;
row.Cells[0].CellFormat.Borders.BorderType = Syncfusion.DocIO.DLS.BorderStyle.Hairline;
row.Cells[0].CellFormat.Borders.Color = System.Drawing.Color.FromArgb(155, 205, 255);
row.Cells[0].CellFormat.BackColor = System.Drawing.Color.FromArgb(222, 239, 255);
cellPara = row.Cells[0].AddParagraph();
//Appends a text to paragraph of cell
txt = cellPara.AppendText("\n Type:\t\t\t\t\t");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.FontSize = 11f;
//Appends a new inline content control to enter the value
InlineContentControl dropdown = cellPara.AppendInlineContentControl(ContentControlType.DropDownList) as InlineContentControl;
WTextRange textRange = new WTextRange(document);
textRange.Text = "Choose an item from drop down list";
dropdown.ParagraphItems.Add(textRange);
//Creates an item for dropdown list
ContentControlListItem item = new ContentControlListItem();
//Sets the text to be displayed as list item
item.DisplayText = "Higher";
//Sets the value to the list item
item.Value = "1";
//Adds item to the dropdown list
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
item = new ContentControlListItem();
item.DisplayText = "Vocational";
item.Value = "2";
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
item = new ContentControlListItem();
item.DisplayText = "Universal";
item.Value = "3";
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
dropdown.ContentControlProperties.Title = "Drop-Down";
//Sets formatting options for text present inside a content control
dropdown.BreakCharacterFormat.TextColor = System.Drawing.Color.MidnightBlue;
dropdown.BreakCharacterFormat.FontName = "Arial";
dropdown.BreakCharacterFormat.FontSize = 11f;
//Appends a text to paragraph of cell
txt = cellPara.AppendText("\n\n Institution:\t\t\t\t");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.FontSize = 11f;
//Appends a new inline content control to enter the value
txtField = cellPara.AppendInlineContentControl(ContentControlType.Text) as InlineContentControl;
//Sets formatting options for text present inside a content control
txtField.BreakCharacterFormat.TextColor = System.Drawing.Color.MidnightBlue;
txtField.BreakCharacterFormat.FontName = "Arial";
txtField.BreakCharacterFormat.FontSize = 11f;
//Appends a text to paragraph of cell
txt = cellPara.AppendText("\n\n Programming Languages:");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.FontSize = 11f;
//Appends a text to paragraph of cell
txt = cellPara.AppendText("\n\n\t C#:\t\t\t\t");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.FontSize = 9f;
//Appends a new inline content control to enter the value
dropdown = cellPara.AppendInlineContentControl(ContentControlType.DropDownList) as InlineContentControl;
textRange = new WTextRange(document);
textRange.Text = "Choose an item from drop down list";
dropdown.ParagraphItems.Add(textRange);
//Creates an item for dropdown list
item = new ContentControlListItem();
//Sets the text to be displayed as list item
item.DisplayText = "Perfect";
//Sets the value to the list item
item.Value = "1";
//Adds item to the dropdown list
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
item = new ContentControlListItem();
item.DisplayText = "Good";
item.Value = "2";
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
item = new ContentControlListItem();
item.DisplayText = "Excellent";
item.Value = "3";
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
//Sets formatting options for text present inside a content control
dropdown.BreakCharacterFormat.TextColor = System.Drawing.Color.MidnightBlue;
dropdown.BreakCharacterFormat.FontName = "Arial";
dropdown.BreakCharacterFormat.FontSize = 11f;
//Appends a text to paragraph of cell
txt = cellPara.AppendText("\n\n\t VB:\t\t\t\t");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.FontSize = 9f;
//Appends a new inline content control to enter the value
dropdown = cellPara.AppendInlineContentControl(ContentControlType.DropDownList) as InlineContentControl;
textRange = new WTextRange(document);
textRange.Text = "Choose an item from drop down list";
dropdown.ParagraphItems.Add(textRange);
//Creates an item for dropdown list
item = new ContentControlListItem();
//Sets the text to be displayed as list item
item.DisplayText = "Perfect";
//Sets the value to the list item
item.Value = "1";
//Adds item to the dropdown list
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
item = new ContentControlListItem();
item.DisplayText = "Good";
item.Value = "2";
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
item = new ContentControlListItem();
item.DisplayText = "Excellent";
item.Value = "3";
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
dropdown.ContentControlProperties.Title = "Drop-Down";
//Sets formatting options for text present inside a content control
dropdown.BreakCharacterFormat.TextColor = System.Drawing.Color.MidnightBlue;
dropdown.BreakCharacterFormat.FontName = "Arial";
dropdown.BreakCharacterFormat.FontSize = 11f;
#endregion
//Saves and closes the Word document instance
document.Save("Form_Template.docx");
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Create a new document
Dim document As WordDocument = New WordDocument()
'Adding a new section to the document
Dim section As IWSection = document.AddSection()
'Adding a new paragraph to the section
Dim paragraph As IWParagraph = section.AddParagraph()

#Region "Document Formatting"
'Sets background color for document
document.Background.Gradient.Color1 = System.Drawing.Color.FromArgb(232, 232, 232)
document.Background.Gradient.Color2 = System.Drawing.Color.FromArgb(255, 255, 255)
document.Background.Type = BackgroundType.Gradient
document.Background.Gradient.ShadingStyle = GradientShadingStyle.Horizontal
document.Background.Gradient.ShadingVariant = GradientShadingVariant.ShadingDown
'Sets page size for document
section.PageSetup.Margins.All = 30.0F
section.PageSetup.PageSize = New System.Drawing.SizeF(600, 600.0!)
#End Region

#Region "Title Section"
'Adds a new table to the section
Dim table As IWTable = section.Body.AddTable()
table.ResetCells(1, 2)
'Gets the table first row
Dim row As WTableRow = table.Rows(0)
row.Height = 25.0F
'Adds a New paragraph to the cell
Dim cellPara As IWParagraph = row.Cells(0).AddParagraph
'Appends a new picture
Dim pic As IWPicture = cellPara.AppendPicture(System.Drawing.Image.FromFile("D:\image.jpg"))
pic.Height = 80
pic.Width = 180
'Adds a new paragraph to the next cell
cellPara = row.Cells(1).AddParagraph
row.Cells(1).CellFormat.VerticalAlignment = Syncfusion.DocIO.DLS.VerticalAlignment.Middle
row.Cells(1).CellFormat.BackColor = System.Drawing.Color.FromArgb(173, 215, 255)
'Appends the text
Dim txt As IWTextRange = cellPara.AppendText("Job Application Form")
cellPara.ParagraphFormat.HorizontalAlignment = Syncfusion.DocIO.DLS.HorizontalAlignment.Center
'Sets the formats
txt.CharacterFormat.Bold = True
txt.CharacterFormat.FontName = "Arial"
txt.CharacterFormat.FontSize = 18.0F
'Sets the width and border type
row.Cells(0).Width = 200
row.Cells(1).Width = 300
row.Cells(1).CellFormat.Borders.BorderType = Syncfusion.DocIO.DLS.BorderStyle.Hairline
#End Region
'Adds a new paragraph
section.AddParagraph()

#Region "General Information"
'Adds a new table
table = section.AddTable()
table.ResetCells(2, 1)
row = table.Rows(0)
row.Height = 20
row.Cells(0).Width = 500
'Adds a new paragraph
cellPara = row.Cells(0).AddParagraph
'Sets a border type, color, background, and vertical alignment for cell
row.Cells(0).CellFormat.Borders.BorderType = Syncfusion.DocIO.DLS.BorderStyle.Thick
row.Cells(0).CellFormat.Borders.Color = System.Drawing.Color.FromArgb(155, 205, 255)
row.Cells(0).CellFormat.BackColor = System.Drawing.Color.FromArgb(198, 227, 255)
row.Cells(0).CellFormat.VerticalAlignment = Syncfusion.DocIO.DLS.VerticalAlignment.Middle
txt = cellPara.AppendText(" General Information")
txt.CharacterFormat.FontName = "Arial"
txt.CharacterFormat.Bold = True
txt.CharacterFormat.FontSize = 11.0F
row = table.Rows(1)
cellPara = row.Cells(0).AddParagraph
'Sets a width, border type, color and background for cell
row.Cells(0).Width = 500
row.Cells(0).CellFormat.Borders.BorderType = Syncfusion.DocIO.DLS.BorderStyle.Hairline
row.Cells(0).CellFormat.Borders.Color = System.Drawing.Color.FromArgb(155, 205, 255)
row.Cells(0).CellFormat.BackColor = System.Drawing.Color.FromArgb(222, 239, 255)
'Appends a text to paragraph of cell
txt = cellPara.AppendText(vbLf + " Full Name:" + vbTab + vbTab + vbTab + vbTab)
txt.CharacterFormat.FontName = "Arial"
txt.CharacterFormat.FontSize = 11.0F
'Appends a new inline content control to enter the value
Dim txtField As InlineContentControl = CType(cellPara.AppendInlineContentControl(ContentControlType.Text), InlineContentControl)
txtField.ContentControlProperties.Title = "Text"
'Sets formatting options for text present inside a content control
txtField.BreakCharacterFormat.TextColor = System.Drawing.Color.MidnightBlue
txtField.BreakCharacterFormat.FontName = "Arial"
txtField.BreakCharacterFormat.FontSize = 11.0F
'Appends a text to paragraph of cell
txt = cellPara.AppendText(vbLf + vbLf + " Birth Date:" + vbTab + vbTab + vbTab + vbTab)
txt.CharacterFormat.FontName = "Arial"
txt.CharacterFormat.FontSize = 11.0F
'Appends a new inline content control to enter the value
txtField = CType(cellPara.AppendInlineContentControl(ContentControlType.Date), InlineContentControl)
txtField.ContentControlProperties.Title = "Date"
'Sets the date display format
txtField.ContentControlProperties.DateDisplayFormat = "M/d/yyyy"
'Sets formatting options for text present inside a content control
txtField.BreakCharacterFormat.TextColor = System.Drawing.Color.MidnightBlue
txtField.BreakCharacterFormat.FontName = "Arial"
txtField.BreakCharacterFormat.FontSize = 11.0F
'Appends a text to paragraph of cell
txt = cellPara.AppendText(vbLf + vbLf + " Address:" + vbTab + vbTab + vbTab + vbTab)
txt.CharacterFormat.FontName = "Arial"
txt.CharacterFormat.FontSize = 11.0F
'Appends a new inline content control to enter the value
txtField = CType(cellPara.AppendInlineContentControl(ContentControlType.Text), InlineContentControl)
txtField.ContentControlProperties.Title = "Text"
'Sets multiline property to true to get the multiple line input of Address
txtField.ContentControlProperties.Multiline = True
'Sets formatting options for text present inside a content control
txtField.BreakCharacterFormat.TextColor = System.Drawing.Color.MidnightBlue
txtField.BreakCharacterFormat.FontName = "Arial"
txtField.BreakCharacterFormat.FontSize = 11.0F
'Appends a text to paragraph of cell
txt = cellPara.AppendText(vbLf + vbLf + " Phone:" + vbTab + vbTab + vbTab + vbTab)
txt.CharacterFormat.FontName = "Arial"
txt.CharacterFormat.FontSize = 11.0F
'Appends a new inline content control to enter the value
txtField = CType(cellPara.AppendInlineContentControl(ContentControlType.Text), InlineContentControl)
txtField.ContentControlProperties.Title = "Text"
'Sets formatting options for text present inside a content control
txtField.BreakCharacterFormat.TextColor = System.Drawing.Color.MidnightBlue
txtField.BreakCharacterFormat.FontName = "Arial"
txtField.BreakCharacterFormat.FontSize = 11.0F
'Appends a text to paragraph of cell
txt = cellPara.AppendText(vbLf + vbLf + " Email:" + vbTab + vbTab + vbTab + vbTab + vbTab)
txt.CharacterFormat.FontName = "Arial"
txt.CharacterFormat.FontSize = 11.0F
'Appends a New inline content control to enter the value
txtField = CType(cellPara.AppendInlineContentControl(ContentControlType.Text), InlineContentControl)
txtField.ContentControlProperties.Title = "Text"
'Sets formatting options for text present inside a content control
txtField.BreakCharacterFormat.TextColor = System.Drawing.Color.MidnightBlue
txtField.BreakCharacterFormat.FontName = "Arial"
txtField.BreakCharacterFormat.FontSize = 11.0F
cellPara.AppendText(vbLf)
#End Region
section.AddParagraph()

#Region "Educational Qualification"
'Adds a new table to the section
table = section.Body.AddTable()
table.ResetCells(2, 1)
row = table.Rows(0)
row.Height = 20
'Sets width, border type, color, background and vertical alignment for cell
row.Cells(0).Width = 500
row.Cells(0).CellFormat.Borders.BorderType = Syncfusion.DocIO.DLS.BorderStyle.Thick
row.Cells(0).CellFormat.Borders.Color = System.Drawing.Color.FromArgb(155, 205, 255)
row.Cells(0).CellFormat.BackColor = System.Drawing.Color.FromArgb(198, 227, 255)
row.Cells(0).CellFormat.VerticalAlignment = Syncfusion.DocIO.DLS.VerticalAlignment.Middle
cellPara = row.Cells(0).AddParagraph
'Appends a text to paragraph of cell
txt = cellPara.AppendText(" Educational Qualification")
txt.CharacterFormat.FontName = "Arial"
txt.CharacterFormat.Bold = True
txt.CharacterFormat.FontSize = 11.0F
row = table.Rows(1)
'Sets width, border type, color, and background for cell
row.Cells(0).Width = 500
row.Cells(0).CellFormat.Borders.BorderType = Syncfusion.DocIO.DLS.BorderStyle.Hairline
row.Cells(0).CellFormat.Borders.Color = System.Drawing.Color.FromArgb(155, 205, 255)
row.Cells(0).CellFormat.BackColor = System.Drawing.Color.FromArgb(222, 239, 255)
cellPara = row.Cells(0).AddParagraph
'Appends a text to paragraph of cell
txt = cellPara.AppendText(vbLf + " Type:" + vbTab + vbTab + vbTab + vbTab + vbTab)
txt.CharacterFormat.FontName = "Arial"
txt.CharacterFormat.FontSize = 11.0F
'Appends a new inline content control to enter the value
Dim dropdown As InlineContentControl = CType(cellPara.AppendInlineContentControl(ContentControlType.DropDownList), InlineContentControl)
Dim textRange As WTextRange = New WTextRange(document)
textRange.Text = "Choose an item from drop down list"
dropdown.ParagraphItems.Add(textRange)
'Creates an item for dropdown list
Dim item As ContentControlListItem = New ContentControlListItem()
'Sets the text to be displayed as list item
item.DisplayText = "Higher"
'Sets the value to the list item
item.Value = "1"
'Adds item to the dropdown list
dropdown.ContentControlProperties.ContentControlListItems.Add(item)
item = New ContentControlListItem()
item.DisplayText = "Vocational"
item.Value = "2"
dropdown.ContentControlProperties.ContentControlListItems.Add(item)
item = New ContentControlListItem()
item.DisplayText = "Universal"
item.Value = "3"
dropdown.ContentControlProperties.ContentControlListItems.Add(item)
dropdown.ContentControlProperties.Title = "Drop-Down"
'Sets formatting options for text present inside a content control
dropdown.BreakCharacterFormat.TextColor = System.Drawing.Color.MidnightBlue
dropdown.BreakCharacterFormat.FontName = "Arial"
dropdown.BreakCharacterFormat.FontSize = 11.0F
'Appends a text to paragraph of cell
txt = cellPara.AppendText(vbLf + vbLf + " Institution:" + vbTab + vbTab + vbTab + vbTab)
txt.CharacterFormat.FontName = "Arial"
txt.CharacterFormat.FontSize = 11.0F
'Appends a new inline content control to enter the value
txtField = CType(cellPara.AppendInlineContentControl(ContentControlType.Text), InlineContentControl)
'Sets formatting options for text present inside a content control
txtField.BreakCharacterFormat.TextColor = System.Drawing.Color.MidnightBlue
txtField.BreakCharacterFormat.FontName = "Arial"
txtField.BreakCharacterFormat.FontSize = 11.0F
'Appends a text to paragraph of cell
txt = cellPara.AppendText(vbLf + vbLf + " Programming Languages:")
txt.CharacterFormat.FontName = "Arial"
txt.CharacterFormat.FontSize = 11.0F
'Appends a text to paragraph of cell
txt = cellPara.AppendText("" + vbLf + vbLf + vbTab + " C#:" + vbTab + vbTab + vbTab + vbTab)
txt.CharacterFormat.FontName = "Arial"
txt.CharacterFormat.FontSize = 9.0F
'Appends a New inline content control to enter the value
dropdown = CType(cellPara.AppendInlineContentControl(ContentControlType.DropDownList), InlineContentControl)
textRange = New WTextRange(document)
textRange.Text = "Choose an item from drop down list"
dropdown.ParagraphItems.Add(textRange)
'Creates an item for dropdown list
item = New ContentControlListItem()
'Sets the text to be displayed as list item
item.DisplayText = "Perfect"
'Sets the value to the list item
item.Value = "1"
'Adds item to the dropdown list
dropdown.ContentControlProperties.ContentControlListItems.Add(item)
item = New ContentControlListItem()
item.DisplayText = "Good"
item.Value = "2"
dropdown.ContentControlProperties.ContentControlListItems.Add(item)
item = New ContentControlListItem()
item.DisplayText = "Excellent"
item.Value = "3"
dropdown.ContentControlProperties.ContentControlListItems.Add(item)
'Sets formatting options for text present inside a content control
dropdown.BreakCharacterFormat.TextColor = System.Drawing.Color.MidnightBlue
dropdown.BreakCharacterFormat.FontName = "Arial"
dropdown.BreakCharacterFormat.FontSize = 11.0F
'Appends a text to paragraph of cell
txt = cellPara.AppendText("" + vbLf + vbLf + vbTab& + " VB:" + vbTab + vbTab + vbTab& + vbTab)
txt.CharacterFormat.FontName = "Arial"
txt.CharacterFormat.FontSize = 9.0F
'Appends a new inline content control to enter the value
dropdown = CType(cellPara.AppendInlineContentControl(ContentControlType.DropDownList), InlineContentControl)
textRange = New WTextRange(document)
textRange.Text = "Choose an item from drop down list"
dropdown.ParagraphItems.Add(textRange)
'Creates an item for dropdown list
item = New ContentControlListItem
'Sets the text to be displayed as list item
item.DisplayText = "Perfect"
'Sets the value to the list item
item.Value = "1"
'Adds item to the dropdown list
dropdown.ContentControlProperties.ContentControlListItems.Add(item)
item = New ContentControlListItem()
item.DisplayText = "Good"
item.Value = "2"
dropdown.ContentControlProperties.ContentControlListItems.Add(item)
item = New ContentControlListItem()
item.DisplayText = "Excellent"
item.Value = "3"
dropdown.ContentControlProperties.ContentControlListItems.Add(item)
dropdown.ContentControlProperties.Title = "Drop-Down"
'Sets formatting options for text present inside a content control
dropdown.BreakCharacterFormat.TextColor = System.Drawing.Color.MidnightBlue
dropdown.BreakCharacterFormat.FontName = "Arial"
dropdown.BreakCharacterFormat.FontSize = 11.0F
#End Region
'Saves and closes the Word document instance
document.Save("Form_Template.docx")
document.Close()
{% endhighlight %}

{% highlight UWP %}
//Create a new document
WordDocument document = new WordDocument();
//Adding a new section to the document
IWSection section = document.AddSection();
//Adding a new paragraph to the section
IWParagraph paragraph = section.AddParagraph();

#region Document formatting
//Sets background color for document
document.Background.Gradient.Color1 = Color.FromArgb(232, 232, 232);
document.Background.Gradient.Color2 = Color.FromArgb(255, 255, 255);
document.Background.Type = BackgroundType.Gradient;
document.Background.Gradient.ShadingStyle = GradientShadingStyle.Horizontal;
document.Background.Gradient.ShadingVariant = GradientShadingVariant.ShadingDown;
//Sets page size for document
section.PageSetup.Margins.All = 30f;
section.PageSetup.PageSize = new SizeF(600, 600f);
#endregion

#region Title Section
//Adds a new table to the section
IWTable table = section.Body.AddTable();
table.ResetCells(1, 2);
//Gets the table first row
WTableRow row = table.Rows[0];
row.Height = 25f;
//Adds a new paragraph to the cell
IWParagraph cellPara = row.Cells[0].AddParagraph();
//Appends a new picture
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream pictureStream = assembly.GetManifestResourceStream("Sample.Assets.image.jpg");
IWPicture pic = cellPara.AppendPicture(pictureStream);
pic.Height = 80;
pic.Width = 180;
//Adds a new paragraph to the next cell
cellPara = row.Cells[1].AddParagraph();
row.Cells[1].CellFormat.VerticalAlignment = Syncfusion.DocIO.DLS.VerticalAlignment.Middle;
row.Cells[1].CellFormat.BackColor = Color.FromArgb(173, 215, 255);
//Appends the text
IWTextRange txt = cellPara.AppendText("Job Application Form");
cellPara.ParagraphFormat.HorizontalAlignment = Syncfusion.DocIO.DLS.HorizontalAlignment.Center;
//Sets the formats
txt.CharacterFormat.Bold = true;
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.FontSize = 18f;
//Sets the width and border type
row.Cells[0].Width = 200;
row.Cells[1].Width = 300;
row.Cells[1].CellFormat.Borders.BorderType = Syncfusion.DocIO.DLS.BorderStyle.Hairline;
#endregion
//Adds a new paragraph
section.AddParagraph();

#region General Information
//Adds a new table
table = section.Body.AddTable();
table.ResetCells(2, 1);
row = table.Rows[0];
row.Height = 20;
row.Cells[0].Width = 500;
//Adds a new paragraph
cellPara = row.Cells[0].AddParagraph();
//Sets a border type, color, background, and vertical alignment for cell
row.Cells[0].CellFormat.Borders.BorderType = Syncfusion.DocIO.DLS.BorderStyle.Thick;
row.Cells[0].CellFormat.Borders.Color = Color.FromArgb(155, 205, 255);
row.Cells[0].CellFormat.BackColor = Color.FromArgb(198, 227, 255);
row.Cells[0].CellFormat.VerticalAlignment = Syncfusion.DocIO.DLS.VerticalAlignment.Middle;
txt = cellPara.AppendText(" General Information");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.Bold = true;
txt.CharacterFormat.FontSize = 11f;
row = table.Rows[1];
cellPara = row.Cells[0].AddParagraph();
//Sets a width, border type, color and background for cell
row.Cells[0].Width = 500;
row.Cells[0].CellFormat.Borders.BorderType = Syncfusion.DocIO.DLS.BorderStyle.Hairline;
row.Cells[0].CellFormat.Borders.Color = Color.FromArgb(155, 205, 255);
row.Cells[0].CellFormat.BackColor = Color.FromArgb(222, 239, 255);
//Appends a text to paragraph of cell
txt = cellPara.AppendText("\n Full Name:\t\t\t\t");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.FontSize = 11f;
//Appends a new inline content control to enter the value
InlineContentControl txtField = cellPara.AppendInlineContentControl(ContentControlType.Text) as InlineContentControl;
txtField.ContentControlProperties.Title = "Text";
//Sets formatting options for text present inside a content control
txtField.BreakCharacterFormat.TextColor = Color.MidnightBlue;
txtField.BreakCharacterFormat.FontName = "Arial";
txtField.BreakCharacterFormat.FontSize = 11f;
//Appends a text to paragraph of cell
txt = cellPara.AppendText("\n\n Birth Date:\t\t\t\t");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.FontSize = 11f;
//Appends a new inline content control to enter the value
txtField = cellPara.AppendInlineContentControl(ContentControlType.Date) as InlineContentControl;
txtField.ContentControlProperties.Title = "Date";
//Sets the date display format
txtField.ContentControlProperties.DateDisplayFormat = "M/d/yyyy";
//Sets formatting options for text present inside a content control
txtField.BreakCharacterFormat.TextColor = Color.MidnightBlue;
txtField.BreakCharacterFormat.FontName = "Arial";
txtField.BreakCharacterFormat.FontSize = 11f;
//Appends a text to paragraph of cell
txt = cellPara.AppendText("\n\n Address:\t\t\t\t");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.FontSize = 11f;
//Appends a new inline content control to enter the value
txtField = cellPara.AppendInlineContentControl(ContentControlType.Text) as InlineContentControl;
txtField.ContentControlProperties.Title = "Text";
//Sets multiline property to true to get the multiple line input of Address
txtField.ContentControlProperties.Multiline = true;
//Sets formatting options for text present inside a content control
txtField.BreakCharacterFormat.TextColor = Color.MidnightBlue;
txtField.BreakCharacterFormat.FontName = "Arial";
txtField.BreakCharacterFormat.FontSize = 11f;
//Appends a text to paragraph of cell
txt = cellPara.AppendText("\n\n Phone:\t\t\t\t");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.FontSize = 11f;
//Appends a new inline content control to enter the value
txtField = cellPara.AppendInlineContentControl(ContentControlType.Text) as InlineContentControl;
txtField.ContentControlProperties.Title = "Text";
//Sets formatting options for text present inside a content control
txtField.BreakCharacterFormat.TextColor = Color.MidnightBlue;
txtField.BreakCharacterFormat.FontName = "Arial";
txtField.BreakCharacterFormat.FontSize = 11f;
//Appends a text to paragraph of cell
txt = cellPara.AppendText("\n\n Email:\t\t\t\t\t");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.FontSize = 11f;
//Appends a new inline content control to enter the value
txtField = cellPara.AppendInlineContentControl(ContentControlType.Text) as InlineContentControl;
txtField.ContentControlProperties.Title = "Text";
//Sets formatting options for text present inside a content control
txtField.BreakCharacterFormat.TextColor = Color.MidnightBlue;
txtField.BreakCharacterFormat.FontName = "Arial";
txtField.BreakCharacterFormat.FontSize = 11f;
cellPara.AppendText("\n");
#endregion
section.AddParagraph();

#region Educational Qualification
//Adds a new table to the section
table = section.Body.AddTable();
table.ResetCells(2, 1);
row = table.Rows[0];
row.Height = 20;
//Sets width, border type, color, background and vertical alignment for cell
row.Cells[0].Width = 500;
row.Cells[0].CellFormat.Borders.BorderType = Syncfusion.DocIO.DLS.BorderStyle.Thick;
row.Cells[0].CellFormat.Borders.Color = Color.FromArgb(155, 205, 255);
row.Cells[0].CellFormat.BackColor = Color.FromArgb(198, 227, 255);
row.Cells[0].CellFormat.VerticalAlignment = Syncfusion.DocIO.DLS.VerticalAlignment.Middle;
cellPara = row.Cells[0].AddParagraph();
//Appends a text to paragraph of cell
txt = cellPara.AppendText(" Educational Qualification");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.Bold = true;
txt.CharacterFormat.FontSize = 11f;
row = table.Rows[1];
//Sets width, border type, color, and background for cell
row.Cells[0].Width = 500;
row.Cells[0].CellFormat.Borders.BorderType = Syncfusion.DocIO.DLS.BorderStyle.Hairline;
row.Cells[0].CellFormat.Borders.Color = Color.FromArgb(155, 205, 255);
row.Cells[0].CellFormat.BackColor = Color.FromArgb(222, 239, 255);
cellPara = row.Cells[0].AddParagraph();
//Appends a text to paragraph of cell
txt = cellPara.AppendText("\n Type:\t\t\t\t\t");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.FontSize = 11f;
//Appends a new inline content control to enter the value
InlineContentControl dropdown = cellPara.AppendInlineContentControl(ContentControlType.DropDownList) as InlineContentControl;
WTextRange textRange = new WTextRange(document);
textRange.Text = "Choose an item from drop down list";
dropdown.ParagraphItems.Add(textRange);
//Creates an item for dropdown list
ContentControlListItem item = new ContentControlListItem();
//Sets the text to be displayed as list item
item.DisplayText = "Higher";
//Sets the value to the list item
item.Value = "1";
//Adds item to the dropdown list
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
item = new ContentControlListItem();
item.DisplayText = "Vocational";
item.Value = "2";
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
item = new ContentControlListItem();
item.DisplayText = "Universal";
item.Value = "3";
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
dropdown.ContentControlProperties.Title = "Drop-Down";
//Sets formatting options for text present inside a content control
dropdown.BreakCharacterFormat.TextColor = Color.MidnightBlue;
dropdown.BreakCharacterFormat.FontName = "Arial";
dropdown.BreakCharacterFormat.FontSize = 11f;
//Appends a text to paragraph of cell
txt = cellPara.AppendText("\n\n Institution:\t\t\t\t");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.FontSize = 11f;
//Appends a new inline content control to enter the value
txtField = cellPara.AppendInlineContentControl(ContentControlType.Text) as InlineContentControl;
//Sets formatting options for text present inside a content control
txtField.BreakCharacterFormat.TextColor = Color.MidnightBlue;
txtField.BreakCharacterFormat.FontName = "Arial";
txtField.BreakCharacterFormat.FontSize = 11f;
//Appends a text to paragraph of cell
txt = cellPara.AppendText("\n\n Programming Languages:");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.FontSize = 11f;
//Appends a text to paragraph of cell
txt = cellPara.AppendText("\n\n\t C#:\t\t\t\t");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.FontSize = 9f;
//Appends a new inline content control to enter the value
dropdown = cellPara.AppendInlineContentControl(ContentControlType.DropDownList) as InlineContentControl;
textRange = new WTextRange(document);
textRange.Text = "Choose an item from drop down list";
dropdown.ParagraphItems.Add(textRange);
//Creates an item for dropdown list
item = new ContentControlListItem();
//Sets the text to be displayed as list item
item.DisplayText = "Perfect";
//Sets the value to the list item
item.Value = "1";
//Adds item to the dropdown list
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
item = new ContentControlListItem();
item.DisplayText = "Good";
item.Value = "2";
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
item = new ContentControlListItem();
item.DisplayText = "Excellent";
item.Value = "3";
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
//Sets formatting options for text present inside a content control
dropdown.BreakCharacterFormat.TextColor = Color.MidnightBlue;
dropdown.BreakCharacterFormat.FontName = "Arial";
dropdown.BreakCharacterFormat.FontSize = 11f;
//Appends a text to paragraph of cell
txt = cellPara.AppendText("\n\n\t VB:\t\t\t\t");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.FontSize = 9f;
//Appends a new inline content control to enter the value
dropdown = cellPara.AppendInlineContentControl(ContentControlType.DropDownList) as InlineContentControl;
textRange = new WTextRange(document);
textRange.Text = "Choose an item from drop down list";
dropdown.ParagraphItems.Add(textRange);
//Creates an item for dropdown list
item = new ContentControlListItem();
//Sets the text to be displayed as list item
item.DisplayText = "Perfect";
//Sets the value to the list item
item.Value = "1";
//Adds item to the dropdown list
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
item = new ContentControlListItem();
item.DisplayText = "Good";
item.Value = "2";
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
item = new ContentControlListItem();
item.DisplayText = "Excellent";
item.Value = "3";
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
dropdown.ContentControlProperties.Title = "Drop-Down";
//Sets formatting options for text present inside a content control
dropdown.BreakCharacterFormat.TextColor = Color.MidnightBlue;
dropdown.BreakCharacterFormat.FontName = "Arial";
dropdown.BreakCharacterFormat.FontSize = 11f;
#endregion
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word file in local machine
Save(stream, "Sample.docx");
document.Close();
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight ASP.NET CORE %}
//Create a new document
WordDocument document = new WordDocument();
//Adding a new section to the document
IWSection section = document.AddSection();
//Adding a new paragraph to the section
IWParagraph paragraph = section.AddParagraph();

#region Document formatting
//Sets background color for document
document.Background.Gradient.Color1 = Syncfusion.Drawing.Color.FromArgb(232, 232, 232);
document.Background.Gradient.Color2 = Syncfusion.Drawing.Color.FromArgb(255, 255, 255);
document.Background.Type = BackgroundType.Gradient;
document.Background.Gradient.ShadingStyle = GradientShadingStyle.Horizontal;
document.Background.Gradient.ShadingVariant = GradientShadingVariant.ShadingDown;
//Sets page size for document
section.PageSetup.Margins.All = 30f;
section.PageSetup.PageSize = new Syncfusion.Drawing.SizeF(600, 600f);
#endregion

#region Title Section
//Adds a new table to the section
IWTable table = section.Body.AddTable();
table.ResetCells(1, 2);
//Gets the table first row
WTableRow row = table.Rows[0];
row.Height = 25f;
//Adds a new paragraph to the cell
IWParagraph cellPara = row.Cells[0].AddParagraph();
//Appends new picture
IWPicture pic = cellPara.AppendPicture(new FileStream(@"D:\image.jpg", FileMode.Open, FileAccess.Read));
pic.Height = 80;
pic.Width = 180;
//Adds a new paragraph to the next cell
cellPara = row.Cells[1].AddParagraph();
row.Cells[1].CellFormat.VerticalAlignment = Syncfusion.DocIO.DLS.VerticalAlignment.Middle;
row.Cells[1].CellFormat.BackColor = Syncfusion.Drawing.Color.FromArgb(173, 215, 255);
//Appends the text
IWTextRange txt = cellPara.AppendText("Job Application Form");
cellPara.ParagraphFormat.HorizontalAlignment = Syncfusion.DocIO.DLS.HorizontalAlignment.Center;
//Sets the formats
txt.CharacterFormat.Bold = true;
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.FontSize = 18f;
//Sets the widths and border types
row.Cells[0].Width = 200;
row.Cells[1].Width = 300;
row.Cells[1].CellFormat.Borders.BorderType = Syncfusion.DocIO.DLS.BorderStyle.Hairline;
#endregion
//Adds a new paragraph
section.AddParagraph();

#region General Information
//Adds a new table
table = section.Body.AddTable();
table.ResetCells(2, 1);
row = table.Rows[0];
row.Height = 20;
row.Cells[0].Width = 500;
//Adds a new paragraph
cellPara = row.Cells[0].AddParagraph();
//Sets a border type, color and background for cell
row.Cells[0].CellFormat.Borders.BorderType = Syncfusion.DocIO.DLS.BorderStyle.Thick;
row.Cells[0].CellFormat.Borders.Color = Syncfusion.Drawing.Color.FromArgb(155, 205, 255);
row.Cells[0].CellFormat.BackColor = Syncfusion.Drawing.Color.FromArgb(198, 227, 255);
row.Cells[0].CellFormat.VerticalAlignment = Syncfusion.DocIO.DLS.VerticalAlignment.Middle;
txt = cellPara.AppendText(" General Information");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.Bold = true;
txt.CharacterFormat.FontSize = 11f;
row = table.Rows[1];
cellPara = row.Cells[0].AddParagraph();
//Sets a width, border type, color and background for cell
row.Cells[0].Width = 500;
row.Cells[0].CellFormat.Borders.BorderType = Syncfusion.DocIO.DLS.BorderStyle.Hairline;
row.Cells[0].CellFormat.Borders.Color = Syncfusion.Drawing.Color.FromArgb(155, 205, 255);
row.Cells[0].CellFormat.BackColor = Syncfusion.Drawing.Color.FromArgb(222, 239, 255);
//Appends a text to paragraph of cell
txt = cellPara.AppendText("\n Full Name:\t\t\t\t");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.FontSize = 11f;
//Appends a new inline content control to enter the value
InlineContentControl txtField = cellPara.AppendInlineContentControl(ContentControlType.Text) as InlineContentControl;
txtField.ContentControlProperties.Title = "Text";
//Sets formatting options for text present insider a content control
txtField.BreakCharacterFormat.TextColor = Syncfusion.Drawing.Color.MidnightBlue;
txtField.BreakCharacterFormat.FontName = "Arial";
txtField.BreakCharacterFormat.FontSize = 11f;
//Appends a text to paragraph of cell
txt = cellPara.AppendText("\n\n Birth Date:\t\t\t\t");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.FontSize = 11f;
//Appends a new inline content control to enter the value
txtField = cellPara.AppendInlineContentControl(ContentControlType.Date) as InlineContentControl;
txtField.ContentControlProperties.Title = "Date";
//Sets the date display format
txtField.ContentControlProperties.DateDisplayFormat = "M/d/yyyy";
//Sets formatting options for text present insider a content control
txtField.BreakCharacterFormat.TextColor = Syncfusion.Drawing.Color.MidnightBlue;
txtField.BreakCharacterFormat.FontName = "Arial";
txtField.BreakCharacterFormat.FontSize = 11f;
//Appends a text to paragraph of cell
txt = cellPara.AppendText("\n\n Address:\t\t\t\t");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.FontSize = 11f;
//Appends a new inline content control to enter the value
txtField = cellPara.AppendInlineContentControl(ContentControlType.Text) as InlineContentControl;
txtField.ContentControlProperties.Title = "Text";
//Sets multiline property to true to get the multiple line input of Address
txtField.ContentControlProperties.Multiline = true;
//Sets formatting options for text present insider a content control
txtField.BreakCharacterFormat.TextColor = Syncfusion.Drawing.Color.MidnightBlue;
txtField.BreakCharacterFormat.FontName = "Arial";
txtField.BreakCharacterFormat.FontSize = 11f;
//Appends a text to paragraph of cell
txt = cellPara.AppendText("\n\n Phone:\t\t\t\t");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.FontSize = 11f;
//Appends a new inline content control to enter the value
txtField = cellPara.AppendInlineContentControl(ContentControlType.Text) as InlineContentControl;
txtField.ContentControlProperties.Title = "Text";
//Sets formatting options for text present insider a content control
txtField.BreakCharacterFormat.TextColor = Syncfusion.Drawing.Color.MidnightBlue;
txtField.BreakCharacterFormat.FontName = "Arial";
txtField.BreakCharacterFormat.FontSize = 11f;
//Appends a text to paragraph of cell
txt = cellPara.AppendText("\n\n Email:\t\t\t\t\t");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.FontSize = 11f;
//Appends a new inline content control to enter the value
txtField = cellPara.AppendInlineContentControl(ContentControlType.Text) as InlineContentControl;
txtField.ContentControlProperties.Title = "Text";
//Sets formatting options for text present insider a content control
txtField.BreakCharacterFormat.TextColor = Syncfusion.Drawing.Color.MidnightBlue;
txtField.BreakCharacterFormat.FontName = "Arial";
txtField.BreakCharacterFormat.FontSize = 11f;
cellPara.AppendText("\n");
#endregion
section.AddParagraph();

#region Educational Qualification
//Adds a new table to the section
table = section.Body.AddTable();
table.ResetCells(2, 1);
row = table.Rows[0];
row.Height = 20;
//Sets width, border type, color, background and vertical alignment for cell
row.Cells[0].Width = 500;
row.Cells[0].CellFormat.Borders.BorderType = Syncfusion.DocIO.DLS.BorderStyle.Thick;
row.Cells[0].CellFormat.Borders.Color = Syncfusion.Drawing.Color.FromArgb(155, 205, 255);
row.Cells[0].CellFormat.BackColor = Syncfusion.Drawing.Color.FromArgb(198, 227, 255);
row.Cells[0].CellFormat.VerticalAlignment = Syncfusion.DocIO.DLS.VerticalAlignment.Middle;
cellPara = row.Cells[0].AddParagraph();
//Appends a text to paragraph of cell
txt = cellPara.AppendText(" Educational Qualification");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.Bold = true;
txt.CharacterFormat.FontSize = 11f;
row = table.Rows[1];
//Sets width, border type, color, and background for cell
row.Cells[0].Width = 500;
row.Cells[0].CellFormat.Borders.BorderType = Syncfusion.DocIO.DLS.BorderStyle.Hairline;
row.Cells[0].CellFormat.Borders.Color = Syncfusion.Drawing.Color.FromArgb(155, 205, 255);
row.Cells[0].CellFormat.BackColor = Syncfusion.Drawing.Color.FromArgb(222, 239, 255);
cellPara = row.Cells[0].AddParagraph();
//Appends a text to paragraph of cell
txt = cellPara.AppendText("\n Type:\t\t\t\t\t");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.FontSize = 11f;
//Appends a new inline content control to enter the value
InlineContentControl dropdown = cellPara.AppendInlineContentControl(ContentControlType.DropDownList) as InlineContentControl;
WTextRange textRange = new WTextRange(document);
textRange.Text = "Choose an item from drop down list";
dropdown.ParagraphItems.Add(textRange);
//Creates an item for dropdown list
ContentControlListItem item = new ContentControlListItem();
//Sets the text to be displayed as list item
item.DisplayText = "Higher";
//Sets the value to the list item
item.Value = "1";
//Adds item to the dropdown list
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
item = new ContentControlListItem();
item.DisplayText = "Vocational";
item.Value = "2";
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
item = new ContentControlListItem();
item.DisplayText = "Universal";
item.Value = "3";
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
dropdown.ContentControlProperties.Title = "Drop-Down";
//Sets formatting options for text present insider a content control
dropdown.BreakCharacterFormat.TextColor = Syncfusion.Drawing.Color.MidnightBlue;
dropdown.BreakCharacterFormat.FontName = "Arial";
dropdown.BreakCharacterFormat.FontSize = 11f;
//Appends a text to paragraph of cell
txt = cellPara.AppendText("\n\n Institution:\t\t\t\t");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.FontSize = 11f;
//Appends a new inline content control to enter the value
txtField = cellPara.AppendInlineContentControl(ContentControlType.Text) as InlineContentControl;
//Sets formatting options for text present insider a content control
txtField.BreakCharacterFormat.TextColor = Syncfusion.Drawing.Color.MidnightBlue;
txtField.BreakCharacterFormat.FontName = "Arial";
txtField.BreakCharacterFormat.FontSize = 11f;
//Appends a text to paragraph of cell
txt = cellPara.AppendText("\n\n Programming Languages:");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.FontSize = 11f;
//Appends a text to paragraph of cell
txt = cellPara.AppendText("\n\n\t C#:\t\t\t\t");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.FontSize = 9f;
//Appends a new inline content control to enter the value
dropdown = cellPara.AppendInlineContentControl(ContentControlType.DropDownList) as InlineContentControl;
textRange = new WTextRange(document);
textRange.Text = "Choose an item from drop down list";
dropdown.ParagraphItems.Add(textRange);
//Creates an item for dropdown list
item = new ContentControlListItem();
//Sets the text to be displayed as list item
item.DisplayText = "Perfect";
//Sets the value to the list item
item.Value = "1";
//Adds item to the dropdown list
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
item = new ContentControlListItem();
item.DisplayText = "Good";
item.Value = "2";
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
item = new ContentControlListItem();
item.DisplayText = "Excellent";
item.Value = "3";
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
//Sets formatting options for text present insider a content control
dropdown.BreakCharacterFormat.TextColor = Syncfusion.Drawing.Color.MidnightBlue;
dropdown.BreakCharacterFormat.FontName = "Arial";
dropdown.BreakCharacterFormat.FontSize = 11f;
//Appends a text to paragraph of cell
txt = cellPara.AppendText("\n\n\t VB:\t\t\t\t");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.FontSize = 9f;
//Appends a new inline content control to enter the value
dropdown = cellPara.AppendInlineContentControl(ContentControlType.DropDownList) as InlineContentControl;
textRange = new WTextRange(document);
textRange.Text = "Choose an item from drop down list";
dropdown.ParagraphItems.Add(textRange);
//Creates an item for dropdown list
item = new ContentControlListItem();
//Sets the text to be displayed as list item
item.DisplayText = "Perfect";
//Sets the value to the list item
item.Value = "1";
//Adds item to the dropdown list
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
item = new ContentControlListItem();
item.DisplayText = "Good";
item.Value = "2";
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
item = new ContentControlListItem();
item.DisplayText = "Excellent";
item.Value = "3";
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
dropdown.ContentControlProperties.Title = "Drop-Down";
//Sets formatting options for text present insider a content control
dropdown.BreakCharacterFormat.TextColor = Syncfusion.Drawing.Color.MidnightBlue;
dropdown.BreakCharacterFormat.FontName = "Arial";
dropdown.BreakCharacterFormat.FontSize = 11f;
#endregion
//Creates memory stream
MemoryStream outputStream = new MemoryStream();
//Saves and closes the Word document instance
document.Save(outputStream, FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight XAMARIN %}
//Create a new document
WordDocument document = new WordDocument();
//Adding a new section to the document
IWSection section = document.AddSection();
//Adding a new paragraph to the section
IWParagraph paragraph = section.AddParagraph();

#region Document formatting
//Sets background color for document
document.Background.Gradient.Color1 = Syncfusion.Drawing.Color.FromArgb(232, 232, 232);
document.Background.Gradient.Color2 = Syncfusion.Drawing.Color.FromArgb(255, 255, 255);
document.Background.Type = BackgroundType.Gradient;
document.Background.Gradient.ShadingStyle = GradientShadingStyle.Horizontal;
document.Background.Gradient.ShadingVariant = GradientShadingVariant.ShadingDown;
//Sets page size for document
section.PageSetup.Margins.All = 30f;
section.PageSetup.PageSize = new Syncfusion.Drawing.SizeF(600, 600f);
#endregion

#region Title Section
//Adds a new table to the section
IWTable table = section.Body.AddTable();
table.ResetCells(1, 2);
//Gets the table first row
WTableRow row = table.Rows[0];
row.Height = 25f;
//Adds a new paragraph to the cell
IWParagraph cellPara = row.Cells[0].AddParagraph();
//Appends new picture
Stream imageStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Image.jpg");
IWPicture pic = cellPara.AppendPicture(imageStream);
pic.Height = 80;
pic.Width = 180;
//Adds a new paragraph to the next cell
cellPara = row.Cells[1].AddParagraph();
row.Cells[1].CellFormat.VerticalAlignment = Syncfusion.DocIO.DLS.VerticalAlignment.Middle;
row.Cells[1].CellFormat.BackColor = Syncfusion.Drawing.Color.FromArgb(173, 215, 255);
//Appends the text
IWTextRange txt = cellPara.AppendText("Job Application Form");
cellPara.ParagraphFormat.HorizontalAlignment = Syncfusion.DocIO.DLS.HorizontalAlignment.Center;
//Sets the formats
txt.CharacterFormat.Bold = true;
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.FontSize = 18f;
//Sets the width and border type
row.Cells[0].Width = 200;
row.Cells[1].Width = 300;
row.Cells[1].CellFormat.Borders.BorderType = Syncfusion.DocIO.DLS.BorderStyle.Hairline;
#endregion
//Adds a new paragraph
section.AddParagraph();

#region General Information
//Adds a new table
table = section.Body.AddTable();
table.ResetCells(2, 1);
row = table.Rows[0];
row.Height = 20;
row.Cells[0].Width = 500;
//Adds a new paragraph
cellPara = row.Cells[0].AddParagraph();
//Sets a border type, color, background, and vertical alignment for cell
row.Cells[0].CellFormat.Borders.BorderType = Syncfusion.DocIO.DLS.BorderStyle.Thick;
row.Cells[0].CellFormat.Borders.Color = Syncfusion.Drawing.Color.FromArgb(155, 205, 255);
row.Cells[0].CellFormat.BackColor = Syncfusion.Drawing.Color.FromArgb(198, 227, 255);
row.Cells[0].CellFormat.VerticalAlignment = Syncfusion.DocIO.DLS.VerticalAlignment.Middle;
txt = cellPara.AppendText(" General Information");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.Bold = true;
txt.CharacterFormat.FontSize = 11f;
row = table.Rows[1];
cellPara = row.Cells[0].AddParagraph();
//Sets a width, border type, color and background for cell
row.Cells[0].Width = 500;
row.Cells[0].CellFormat.Borders.BorderType = Syncfusion.DocIO.DLS.BorderStyle.Hairline;
row.Cells[0].CellFormat.Borders.Color = Syncfusion.Drawing.Color.FromArgb(155, 205, 255);
row.Cells[0].CellFormat.BackColor = Syncfusion.Drawing.Color.FromArgb(222, 239, 255);
//Appends a text to paragraph of cell
txt = cellPara.AppendText("\n Full Name:\t\t\t\t");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.FontSize = 11f;
//Appends a new inline content control to enter the value
InlineContentControl txtField = cellPara.AppendInlineContentControl(ContentControlType.Text) as InlineContentControl;
txtField.ContentControlProperties.Title = "Text";
//Sets formatting options for text present insider a content control.
txtField.BreakCharacterFormat.TextColor = Syncfusion.Drawing.Color.MidnightBlue;
txtField.BreakCharacterFormat.FontName = "Arial";
txtField.BreakCharacterFormat.FontSize = 11f;
//Appends a text to paragraph of cell
txt = cellPara.AppendText("\n\n Birth Date:\t\t\t\t");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.FontSize = 11f;
//Appends a new inline content control to enter the value
txtField = cellPara.AppendInlineContentControl(ContentControlType.Date) as InlineContentControl;
txtField.ContentControlProperties.Title = "Date";
//Sets the date display format
txtField.ContentControlProperties.DateDisplayFormat = "M/d/yyyy";
//Sets formatting options for text present insider a content control
txtField.BreakCharacterFormat.TextColor = Syncfusion.Drawing.Color.MidnightBlue;
txtField.BreakCharacterFormat.FontName = "Arial";
txtField.BreakCharacterFormat.FontSize = 11f;
//Appends a text to paragraph of cell
txt = cellPara.AppendText("\n\n Address:\t\t\t\t");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.FontSize = 11f;
//Appends a new inline content control to enter the value
txtField = cellPara.AppendInlineContentControl(ContentControlType.Text) as InlineContentControl;
txtField.ContentControlProperties.Title = "Text";
//Sets multiline property to true to get the multiple line input of Address
txtField.ContentControlProperties.Multiline = true;
//Sets formatting options for text present insider a content control
txtField.BreakCharacterFormat.TextColor = Syncfusion.Drawing.Color.MidnightBlue;
txtField.BreakCharacterFormat.FontName = "Arial";
txtField.BreakCharacterFormat.FontSize = 11f;
//Appends a text to paragraph of cell
txt = cellPara.AppendText("\n\n Phone:\t\t\t\t");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.FontSize = 11f;
//Appends a new inline content control to enter the value
txtField = cellPara.AppendInlineContentControl(ContentControlType.Text) as InlineContentControl;
txtField.ContentControlProperties.Title = "Text";
//Sets formatting options for text present insider a content control
txtField.BreakCharacterFormat.TextColor = Syncfusion.Drawing.Color.MidnightBlue;
txtField.BreakCharacterFormat.FontName = "Arial";
txtField.BreakCharacterFormat.FontSize = 11f;
//Appends a text to paragraph of cell
txt = cellPara.AppendText("\n\n Email:\t\t\t\t\t");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.FontSize = 11f;
//Appends a new inline content control to enter the value
txtField = cellPara.AppendInlineContentControl(ContentControlType.Text) as InlineContentControl;
txtField.ContentControlProperties.Title = "Text";
//Sets formatting options for text present insider a content control
txtField.BreakCharacterFormat.TextColor = Syncfusion.Drawing.Color.MidnightBlue;
txtField.BreakCharacterFormat.FontName = "Arial";
txtField.BreakCharacterFormat.FontSize = 11f;
cellPara.AppendText("\n");
#endregion
section.AddParagraph();

#region Educational Qualification
//Adds a new table to the section
table = section.Body.AddTable();
table.ResetCells(2, 1);
row = table.Rows[0];
row.Height = 20;
//Sets width, border type, color, background and vertical alignment for cell
row.Cells[0].Width = 500;
row.Cells[0].CellFormat.Borders.BorderType = Syncfusion.DocIO.DLS.BorderStyle.Thick;
row.Cells[0].CellFormat.Borders.Color = Syncfusion.Drawing.Color.FromArgb(155, 205, 255);
row.Cells[0].CellFormat.BackColor = Syncfusion.Drawing.Color.FromArgb(198, 227, 255);
row.Cells[0].CellFormat.VerticalAlignment = Syncfusion.DocIO.DLS.VerticalAlignment.Middle;
cellPara = row.Cells[0].AddParagraph();
//Appends a text to paragraph of cell
txt = cellPara.AppendText(" Educational Qualification");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.Bold = true;
txt.CharacterFormat.FontSize = 11f;
row = table.Rows[1];
//Sets width, border type, color, and background for cell
row.Cells[0].Width = 500;
row.Cells[0].CellFormat.Borders.BorderType = Syncfusion.DocIO.DLS.BorderStyle.Hairline;
row.Cells[0].CellFormat.Borders.Color = Syncfusion.Drawing.Color.FromArgb(155, 205, 255);
row.Cells[0].CellFormat.BackColor = Syncfusion.Drawing.Color.FromArgb(222, 239, 255);
cellPara = row.Cells[0].AddParagraph();
//Appends a text to paragraph of cell
txt = cellPara.AppendText("\n Type:\t\t\t\t\t");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.FontSize = 11f;
//Appends a new inline content control to enter the value
InlineContentControl dropdown = cellPara.AppendInlineContentControl(ContentControlType.DropDownList) as InlineContentControl;
WTextRange textRange = new WTextRange(document);
textRange.Text = "Choose an item from drop down list";
dropdown.ParagraphItems.Add(textRange);
//Creates an item for dropdown list
ContentControlListItem item = new ContentControlListItem();
//Sets the text to be displayed as list item
item.DisplayText = "Higher";
//Sets the value to the list item
item.Value = "1";
//Adds item to the dropdown list
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
item = new ContentControlListItem();
item.DisplayText = "Vocational";
item.Value = "2";
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
item = new ContentControlListItem();
item.DisplayText = "Universal";
item.Value = "3";
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
dropdown.ContentControlProperties.Title = "Drop-Down";
//Sets formatting options for text present insider a content control
dropdown.BreakCharacterFormat.TextColor = Syncfusion.Drawing.Color.MidnightBlue;
dropdown.BreakCharacterFormat.FontName = "Arial";
dropdown.BreakCharacterFormat.FontSize = 11f;
//Appends a text to paragraph of cell
txt = cellPara.AppendText("\n\n Institution:\t\t\t\t");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.FontSize = 11f;
//Appends a new inline content control to enter the value
txtField = cellPara.AppendInlineContentControl(ContentControlType.Text) as InlineContentControl;
//Sets formatting options for text present insider a content control
txtField.BreakCharacterFormat.TextColor = Syncfusion.Drawing.Color.MidnightBlue;
txtField.BreakCharacterFormat.FontName = "Arial";
txtField.BreakCharacterFormat.FontSize = 11f;
//Appends a text to paragraph of cell
txt = cellPara.AppendText("\n\n Programming Languages:");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.FontSize = 11f;
//Appends a text to paragraph of cell
txt = cellPara.AppendText("\n\n\t C#:\t\t\t\t");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.FontSize = 9f;
//Appends a new inline content control to enter the value
dropdown = cellPara.AppendInlineContentControl(ContentControlType.DropDownList) as InlineContentControl;
textRange = new WTextRange(document);
textRange.Text = "Choose an item from drop down list";
dropdown.ParagraphItems.Add(textRange);
//Creates an item for dropdown list
item = new ContentControlListItem();
//Sets the text to be displayed as list item
item.DisplayText = "Perfect";
//Sets the value to the list item
item.Value = "1";
//Adds item to the dropdown list
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
item = new ContentControlListItem();
item.DisplayText = "Good";
item.Value = "2";
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
item = new ContentControlListItem();
item.DisplayText = "Excellent";
item.Value = "3";
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
//Sets formatting options for text present insider a content control
dropdown.BreakCharacterFormat.TextColor = Syncfusion.Drawing.Color.MidnightBlue;
dropdown.BreakCharacterFormat.FontName = "Arial";
dropdown.BreakCharacterFormat.FontSize = 11f;
//Appends a text to paragraph of cell
txt = cellPara.AppendText("\n\n\t VB:\t\t\t\t");
txt.CharacterFormat.FontName = "Arial";
txt.CharacterFormat.FontSize = 9f;
//Appends a new inline content control to enter the value
dropdown = cellPara.AppendInlineContentControl(ContentControlType.DropDownList) as InlineContentControl;
textRange = new WTextRange(document);
textRange.Text = "Choose an item from drop down list";
dropdown.ParagraphItems.Add(textRange);
//Creates an item for dropdown list
item = new ContentControlListItem();
//Sets the text to be displayed as list item
item.DisplayText = "Perfect";
//Sets the value to the list item
item.Value = "1";
//Adds item to the dropdown list
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
item = new ContentControlListItem();
item.DisplayText = "Good";
item.Value = "2";
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
item = new ContentControlListItem();
item.DisplayText = "Excellent";
item.Value = "3";
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
dropdown.ContentControlProperties.Title = "Drop-Down";
//Sets formatting options for text present insider a content control
dropdown.BreakCharacterFormat.TextColor = Syncfusion.Drawing.Color.MidnightBlue;
dropdown.BreakCharacterFormat.FontName = "Arial";
dropdown.BreakCharacterFormat.FontSize = 11f;
#endregion
//Create memory stream
MemoryStream outputStream = new MemoryStream();
//Saves and closes the Word document instance
document.Save(outputStream, FormatType.Docx);
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", outputStream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
document.Close();
{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Content-Controls/Create-form-in-Word-document).

You can also fill the forms using the DocIO. Refer to the following code example.

Form filling:

{% tabs %}
{% highlight c# %}
//Open the created form document.
WordDocument document1 = new WordDocument("Form_Template.docx");
IWSection sec = document1.LastSection;
InlineContentControl inlineCC;
InlineContentControl dropDownCC;
WTable table1 = sec.Tables[1] as WTable;
WTableRow row1 = table1.Rows[1];

#region General Information
//Fill the name
WParagraph cellPara1 = row1.Cells[0].ChildEntities[1] as WParagraph;
inlineCC = cellPara1.ChildEntities.LastItem as InlineContentControl;
WTextRange text = new WTextRange(document1);
text.ApplyCharacterFormat(inlineCC.BreakCharacterFormat);
text.Text = "Steve Jobs";
inlineCC.ParagraphItems.Add(text);
//Fill the date of birth
cellPara1 = row1.Cells[0].ChildEntities[3] as WParagraph;
inlineCC = cellPara1.ChildEntities.LastItem as InlineContentControl;
text = new WTextRange(document1);
text.ApplyCharacterFormat(inlineCC.BreakCharacterFormat);
text.Text = "06/01/1994";
inlineCC.ParagraphItems.Add(text);
//Fill the address
cellPara1 = row1.Cells[0].ChildEntities[5] as WParagraph;
inlineCC = cellPara1.ChildEntities.LastItem as InlineContentControl;
text = new WTextRange(document1);
text.ApplyCharacterFormat(inlineCC.BreakCharacterFormat);
text.Text = "2501 Aerial Center Parkway.";
inlineCC.ParagraphItems.Add(text);
text = new WTextRange(document1);
text.ApplyCharacterFormat(inlineCC.BreakCharacterFormat);
text.Text = "Morrisville, NC 27560.";
inlineCC.ParagraphItems.Add(text);
text = new WTextRange(document1);
text.ApplyCharacterFormat(inlineCC.BreakCharacterFormat);
text.Text = "USA.";
inlineCC.ParagraphItems.Add(text);
//Fill the phone no
cellPara1 = row1.Cells[0].ChildEntities[7] as WParagraph;
inlineCC = cellPara1.ChildEntities.LastItem as InlineContentControl;
text = new WTextRange(document1);
text.ApplyCharacterFormat(inlineCC.BreakCharacterFormat);
text.Text = "+1 919.481.1974";
inlineCC.ParagraphItems.Add(text);
//Fill the email id
cellPara1 = row1.Cells[0].ChildEntities[9] as WParagraph;
inlineCC = cellPara1.ChildEntities.LastItem as InlineContentControl;
text = new WTextRange(document1);
text.ApplyCharacterFormat(inlineCC.BreakCharacterFormat);
text.Text = "steve123@email.com";
inlineCC.ParagraphItems.Add(text);
#endregion

#region Educational Information
table1 = sec.Tables[2] as WTable;
row1 = table1.Rows[1];
//Fill the education type
cellPara1 = row1.Cells[0].ChildEntities[1] as WParagraph;
dropDownCC = cellPara1.ChildEntities.LastItem as InlineContentControl;
text = new WTextRange(document1);
text.ApplyCharacterFormat(dropDownCC.BreakCharacterFormat);
text.Text = dropDownCC.ContentControlProperties.ContentControlListItems[1].DisplayText;
dropDownCC.ParagraphItems.Add(text);
//Fill the university
cellPara1 = row1.Cells[0].ChildEntities[3] as WParagraph;
inlineCC = cellPara1.ChildEntities.LastItem as InlineContentControl;
text = new WTextRange(document1);
text.ApplyCharacterFormat(dropDownCC.BreakCharacterFormat);
text.Text = "Michigan University";
inlineCC.ParagraphItems.Add(text);
//Fill the C# experience level
cellPara1 = row1.Cells[0].ChildEntities[7] as WParagraph;
dropDownCC = cellPara1.ChildEntities.LastItem as InlineContentControl;
text = new WTextRange(document1);
text.ApplyCharacterFormat(dropDownCC.BreakCharacterFormat);
text.Text = dropDownCC.ContentControlProperties.ContentControlListItems[2].DisplayText;
dropDownCC.ParagraphItems.Add(text);
//Fill the VB experience level
cellPara1 = row1.Cells[0].ChildEntities[9] as WParagraph;
dropDownCC = cellPara1.ChildEntities.LastItem as InlineContentControl;
text = new WTextRange(document1);
text.ApplyCharacterFormat(dropDownCC.BreakCharacterFormat);
text.Text = dropDownCC.ContentControlProperties.ContentControlListItems[1].DisplayText;
dropDownCC.ParagraphItems.Add(text);
#endregion
//Saves and closes the Word document instance
document1.Save("Form_Filled.docx");
document1.Close();
{% endhighlight %}

{% highlight vb.net %}
'Open the created form document
Dim document1 As WordDocument = New WordDocument("Form_Template.docx")
Dim sec As IWSection = document1.LastSection
Dim inlineCC As InlineContentControl
Dim dropDownCC As InlineContentControl
Dim table1 As WTable = CType(sec.Tables(1), WTable)
Dim row1 As WTableRow = table1.Rows(1)

#Region "General Information"
Dim cellPara1 As WParagraph = CType(row1.Cells(0).ChildEntities(1), WParagraph)
inlineCC = CType(cellPara1.ChildEntities.LastItem, InlineContentControl)
Dim text As WTextRange = New WTextRange(document1)
text.ApplyCharacterFormat(inlineCC.BreakCharacterFormat)
text.Text = "Steve Jobs"
inlineCC.ParagraphItems.Add(text)
'Fill the date of birth
cellPara1 = CType(row1.Cells(0).ChildEntities(3), WParagraph)
inlineCC = CType(cellPara1.ChildEntities.LastItem, InlineContentControl)
text = New WTextRange(document1)
text.ApplyCharacterFormat(inlineCC.BreakCharacterFormat)
text.Text = "06/01/1994"
inlineCC.ParagraphItems.Add(text)
'Fill the address
cellPara1 = CType(row1.Cells(0).ChildEntities(5), WParagraph)
inlineCC = CType(cellPara1.ChildEntities.LastItem, InlineContentControl)
text = New WTextRange(document1)
text.ApplyCharacterFormat(inlineCC.BreakCharacterFormat)
text.Text = "2501 Aerial Center Parkway."
inlineCC.ParagraphItems.Add(text)
text = New WTextRange(document1)
text.ApplyCharacterFormat(inlineCC.BreakCharacterFormat)
text.Text = "Morrisville, NC 27560."
inlineCC.ParagraphItems.Add(text)
text = New WTextRange(document1)
text.ApplyCharacterFormat(inlineCC.BreakCharacterFormat)
text.Text = "USA."
inlineCC.ParagraphItems.Add(text)
'Fill the phone no
cellPara1 = CType(row1.Cells(0).ChildEntities(7), WParagraph)
inlineCC = CType(cellPara1.ChildEntities.LastItem, InlineContentControl)
text = New WTextRange(document1)
text.ApplyCharacterFormat(inlineCC.BreakCharacterFormat)
text.Text = "+1 919.481.1974"
inlineCC.ParagraphItems.Add(text)
'Fill the email id
cellPara1 = CType(row1.Cells(0).ChildEntities(9), WParagraph)
inlineCC = CType(cellPara1.ChildEntities.LastItem, InlineContentControl)
text = New WTextRange(document1)
text.ApplyCharacterFormat(inlineCC.BreakCharacterFormat)
text.Text = "steve123@email.com"
inlineCC.ParagraphItems.Add(text)
#End Region

#Region "Educational Information"
table1 = CType(sec.Tables(2), WTable)
row1 = table1.Rows(1)
'Fill the education type
cellPara1 = CType(row1.Cells(0).ChildEntities(1), WParagraph)
dropDownCC = CType(cellPara1.ChildEntities.LastItem, InlineContentControl)
text = New WTextRange(document1)
text.ApplyCharacterFormat(dropDownCC.BreakCharacterFormat)
text.Text = dropDownCC.ContentControlProperties.ContentControlListItems(1).DisplayText
dropDownCC.ParagraphItems.Add(text)
'Fill the university
cellPara1 = CType(row1.Cells(0).ChildEntities(3), WParagraph)
inlineCC = CType(cellPara1.ChildEntities.LastItem, InlineContentControl)
text = New WTextRange(document1)
text.ApplyCharacterFormat(dropDownCC.BreakCharacterFormat)
text.Text = "Michigan University"
inlineCC.ParagraphItems.Add(text)
'Fill the C# experience level
cellPara1 = CType(row1.Cells(0).ChildEntities(7), WParagraph)
dropDownCC = CType(cellPara1.ChildEntities.LastItem, InlineContentControl)
text = New WTextRange(document1)
text.ApplyCharacterFormat(dropDownCC.BreakCharacterFormat)
text.Text = dropDownCC.ContentControlProperties.ContentControlListItems(2).DisplayText
dropDownCC.ParagraphItems.Add(text)
'Fill the VB experience level
cellPara1 = CType(row1.Cells(0).ChildEntities(9), WParagraph)
dropDownCC = CType(cellPara1.ChildEntities.LastItem, InlineContentControl)
text = New WTextRange(document1)
text.ApplyCharacterFormat(dropDownCC.BreakCharacterFormat)
text.Text = dropDownCC.ContentControlProperties.ContentControlListItems(1).DisplayText
dropDownCC.ParagraphItems.Add(text)
#End Region
document1.Save("Form_Filled.docx")
document1.Close()
{% endhighlight %}

{% highlight UWP %}
//Open the created form document
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
WordDocument document1 = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Form_Template.docx"), FormatType.Docx);
IWSection sec = document1.LastSection;
InlineContentControl inlineCC;
InlineContentControl dropDownCC;
WTable table1 = sec.Tables[1] as WTable;
WTableRow row1 = table1.Rows[1];

#region General Information
//Fill the name
WParagraph cellPara1 = row1.Cells[0].ChildEntities[1] as WParagraph;
inlineCC = cellPara1.ChildEntities.LastItem as InlineContentControl;
WTextRange text = new WTextRange(document1);
text.ApplyCharacterFormat(inlineCC.BreakCharacterFormat);
text.Text = "Steve Jobs";
inlineCC.ParagraphItems.Add(text);
//Fill the date of birth
cellPara1 = row1.Cells[0].ChildEntities[3] as WParagraph;
inlineCC = cellPara1.ChildEntities.LastItem as InlineContentControl;
text = new WTextRange(document1);
text.ApplyCharacterFormat(inlineCC.BreakCharacterFormat);
text.Text = "06/01/1994";
inlineCC.ParagraphItems.Add(text);
//Fill the address
cellPara1 = row1.Cells[0].ChildEntities[5] as WParagraph;
inlineCC = cellPara1.ChildEntities.LastItem as InlineContentControl;
text = new WTextRange(document1);
text.ApplyCharacterFormat(inlineCC.BreakCharacterFormat);
text.Text = "2501 Aerial Center Parkway.";
inlineCC.ParagraphItems.Add(text);
text = new WTextRange(document1);
text.ApplyCharacterFormat(inlineCC.BreakCharacterFormat);
text.Text = "Morrisville, NC 27560.";
inlineCC.ParagraphItems.Add(text);
text = new WTextRange(document1);
text.ApplyCharacterFormat(inlineCC.BreakCharacterFormat);
text.Text = "USA.";
inlineCC.ParagraphItems.Add(text);
//Fill the phone no
cellPara1 = row1.Cells[0].ChildEntities[7] as WParagraph;
inlineCC = cellPara1.ChildEntities.LastItem as InlineContentControl;
text = new WTextRange(document1);
text.ApplyCharacterFormat(inlineCC.BreakCharacterFormat);
text.Text = "+1 919.481.1974";
inlineCC.ParagraphItems.Add(text);
//Fill the email id
cellPara1 = row1.Cells[0].ChildEntities[9] as WParagraph;
inlineCC = cellPara1.ChildEntities.LastItem as InlineContentControl;
text = new WTextRange(document1);
text.ApplyCharacterFormat(inlineCC.BreakCharacterFormat);
text.Text = "steve123@email.com";
inlineCC.ParagraphItems.Add(text);
#endregion

#region Educational Information
table1 = sec.Tables[2] as WTable;
row1 = table1.Rows[1];
//Fill the education type
cellPara1 = row1.Cells[0].ChildEntities[1] as WParagraph;
dropDownCC = cellPara1.ChildEntities.LastItem as InlineContentControl;
text = new WTextRange(document1);
text.ApplyCharacterFormat(dropDownCC.BreakCharacterFormat);
text.Text = dropDownCC.ContentControlProperties.ContentControlListItems[1].DisplayText;
dropDownCC.ParagraphItems.Add(text);
//Fill the university
cellPara1 = row1.Cells[0].ChildEntities[3] as WParagraph;
inlineCC = cellPara1.ChildEntities.LastItem as InlineContentControl;
text = new WTextRange(document1);
text.ApplyCharacterFormat(dropDownCC.BreakCharacterFormat);
text.Text = "Michigan University";
inlineCC.ParagraphItems.Add(text);
//Fill the C# experience level
cellPara1 = row1.Cells[0].ChildEntities[7] as WParagraph;
dropDownCC = cellPara1.ChildEntities.LastItem as InlineContentControl;
text = new WTextRange(document1);
text.ApplyCharacterFormat(dropDownCC.BreakCharacterFormat);
text.Text = dropDownCC.ContentControlProperties.ContentControlListItems[2].DisplayText;
dropDownCC.ParagraphItems.Add(text);
//Fill the VB experience level
cellPara1 = row1.Cells[0].ChildEntities[9] as WParagraph;
dropDownCC = cellPara1.ChildEntities.LastItem as InlineContentControl;
text = new WTextRange(document1);
text.ApplyCharacterFormat(dropDownCC.BreakCharacterFormat);
text.Text = dropDownCC.ContentControlProperties.ContentControlListItems[1].DisplayText;
dropDownCC.ParagraphItems.Add(text);
#endregion
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
await document1.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word file in local machine
Save(stream, "Form_Filled.docx");
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
document1.Close();
{% endhighlight %}

{% highlight ASP.NET CORE %}
//Open the created form document
WordDocument document1 = new WordDocument(outputStream, FormatType.Automatic);
IWSection sec = document1.LastSection;
InlineContentControl inlineCC;
InlineContentControl dropDownCC;
WTable table1 = sec.Tables[1] as WTable;
WTableRow row1 = table1.Rows[1];

#region General Information
//Fill the name
WParagraph cellPara1 = row1.Cells[0].ChildEntities[1] as WParagraph;
inlineCC = cellPara1.ChildEntities.LastItem as InlineContentControl;
WTextRange text = new WTextRange(document1);
text.ApplyCharacterFormat(inlineCC.BreakCharacterFormat);
text.Text = "Steve Jobs";
inlineCC.ParagraphItems.Add(text);
//Fill the date of birth
cellPara1 = row1.Cells[0].ChildEntities[3] as WParagraph;
inlineCC = cellPara1.ChildEntities.LastItem as InlineContentControl;
text = new WTextRange(document1);
text.ApplyCharacterFormat(inlineCC.BreakCharacterFormat);
text.Text = "06/01/1994";
inlineCC.ParagraphItems.Add(text);
//Fill the address
cellPara1 = row1.Cells[0].ChildEntities[5] as WParagraph;
inlineCC = cellPara1.ChildEntities.LastItem as InlineContentControl;
text = new WTextRange(document1);
text.ApplyCharacterFormat(inlineCC.BreakCharacterFormat);
text.Text = "2501 Aerial Center Parkway.";
inlineCC.ParagraphItems.Add(text);
text = new WTextRange(document1);
text.ApplyCharacterFormat(inlineCC.BreakCharacterFormat);
text.Text = "Morrisville, NC 27560.";
inlineCC.ParagraphItems.Add(text);
text = new WTextRange(document1);
text.ApplyCharacterFormat(inlineCC.BreakCharacterFormat);
text.Text = "USA.";
inlineCC.ParagraphItems.Add(text);
//Fill the phone no
cellPara1 = row1.Cells[0].ChildEntities[7] as WParagraph;
inlineCC = cellPara1.ChildEntities.LastItem as InlineContentControl;
text = new WTextRange(document1);
text.ApplyCharacterFormat(inlineCC.BreakCharacterFormat);
text.Text = "+1 919.481.1974";
inlineCC.ParagraphItems.Add(text);
//Fill the email id
cellPara1 = row1.Cells[0].ChildEntities[9] as WParagraph;
inlineCC = cellPara1.ChildEntities.LastItem as InlineContentControl;
text = new WTextRange(document1);
text.ApplyCharacterFormat(inlineCC.BreakCharacterFormat);
text.Text = "steve123@email.com";
inlineCC.ParagraphItems.Add(text);
#endregion

#region Educational Information
table1 = sec.Tables[2] as WTable;
row1 = table1.Rows[1];
//Fill the education type
cellPara1 = row1.Cells[0].ChildEntities[1] as WParagraph;
dropDownCC = cellPara1.ChildEntities.LastItem as InlineContentControl;
text = new WTextRange(document1);
text.ApplyCharacterFormat(dropDownCC.BreakCharacterFormat);
text.Text = dropDownCC.ContentControlProperties.ContentControlListItems[1].DisplayText;
dropDownCC.ParagraphItems.Add(text);
//Fill the university
cellPara1 = row1.Cells[0].ChildEntities[3] as WParagraph;
inlineCC = cellPara1.ChildEntities.LastItem as InlineContentControl;
text = new WTextRange(document1);
text.ApplyCharacterFormat(dropDownCC.BreakCharacterFormat);
text.Text = "Michigan University";
inlineCC.ParagraphItems.Add(text);
//Fill the C# experience level
cellPara1 = row1.Cells[0].ChildEntities[7] as WParagraph;
dropDownCC = cellPara1.ChildEntities.LastItem as InlineContentControl;
text = new WTextRange(document1);
text.ApplyCharacterFormat(dropDownCC.BreakCharacterFormat);
text.Text = dropDownCC.ContentControlProperties.ContentControlListItems[2].DisplayText;
dropDownCC.ParagraphItems.Add(text);
//Fill the VB experience level
cellPara1 = row1.Cells[0].ChildEntities[9] as WParagraph;
dropDownCC = cellPara1.ChildEntities.LastItem as InlineContentControl;
text = new WTextRange(document1);
text.ApplyCharacterFormat(dropDownCC.BreakCharacterFormat);
text.Text = dropDownCC.ContentControlProperties.ContentControlListItems[1].DisplayText;
dropDownCC.ParagraphItems.Add(text);
#endregion
//Creates memory stream
MemoryStream saveStream = new MemoryStream();
//Saves and closes the Word document instance
document1.Save(saveStream, FormatType.Docx);
document1.Close();
{% endhighlight %}

{% highlight XAMARIN %}
//Open the created form document
Stream inputStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Form_Template.docx");
WordDocument document1 = new WordDocument(inputStream, FormatType.Automatic);
IWSection sec = document1.LastSection;
InlineContentControl inlineCC;
InlineContentControl dropDownCC;
WTable table1 = sec.Tables[1] as WTable;
WTableRow row1 = table1.Rows[1];

#region General Information
//Fill the name
WParagraph cellPara1 = row1.Cells[0].ChildEntities[1] as WParagraph;
inlineCC = cellPara1.ChildEntities.LastItem as InlineContentControl;
WTextRange text = new WTextRange(document1);
text.ApplyCharacterFormat(inlineCC.BreakCharacterFormat);
text.Text = "Steve Jobs";
inlineCC.ParagraphItems.Add(text);
//Fill the date of birth
cellPara1 = row1.Cells[0].ChildEntities[3] as WParagraph;
inlineCC = cellPara1.ChildEntities.LastItem as InlineContentControl;
text = new WTextRange(document1);
text.ApplyCharacterFormat(inlineCC.BreakCharacterFormat);
text.Text = "06/01/1994";
inlineCC.ParagraphItems.Add(text);
//Fill the address
cellPara1 = row1.Cells[0].ChildEntities[5] as WParagraph;
inlineCC = cellPara1.ChildEntities.LastItem as InlineContentControl;
text = new WTextRange(document1);
text.ApplyCharacterFormat(inlineCC.BreakCharacterFormat);
text.Text = "2501 Aerial Center Parkway.";
inlineCC.ParagraphItems.Add(text);
text = new WTextRange(document1);
text.ApplyCharacterFormat(inlineCC.BreakCharacterFormat);
text.Text = "Morrisville, NC 27560.";
inlineCC.ParagraphItems.Add(text);
text = new WTextRange(document1);
text.ApplyCharacterFormat(inlineCC.BreakCharacterFormat);
text.Text = "USA.";
inlineCC.ParagraphItems.Add(text);
//Fill the phone no
cellPara1 = row1.Cells[0].ChildEntities[7] as WParagraph;
inlineCC = cellPara1.ChildEntities.LastItem as InlineContentControl;
text = new WTextRange(document1);
text.ApplyCharacterFormat(inlineCC.BreakCharacterFormat);
text.Text = "+1 919.481.1974";
inlineCC.ParagraphItems.Add(text);
//Fill the email id
cellPara1 = row1.Cells[0].ChildEntities[9] as WParagraph;
inlineCC = cellPara1.ChildEntities.LastItem as InlineContentControl;
text = new WTextRange(document1);
text.ApplyCharacterFormat(inlineCC.BreakCharacterFormat);
text.Text = "steve123@email.com";
inlineCC.ParagraphItems.Add(text);
#endregion

#region Educational Information
table1 = sec.Tables[2] as WTable;
row1 = table1.Rows[1];
//Fill the education type
cellPara1 = row1.Cells[0].ChildEntities[1] as WParagraph;
dropDownCC = cellPara1.ChildEntities.LastItem as InlineContentControl;
text = new WTextRange(document1);
text.ApplyCharacterFormat(dropDownCC.BreakCharacterFormat);
text.Text = dropDownCC.ContentControlProperties.ContentControlListItems[1].DisplayText;
dropDownCC.ParagraphItems.Add(text);
//Fill the university
cellPara1 = row1.Cells[0].ChildEntities[3] as WParagraph;
inlineCC = cellPara1.ChildEntities.LastItem as InlineContentControl;
text = new WTextRange(document1);
text.ApplyCharacterFormat(dropDownCC.BreakCharacterFormat);
text.Text = "Michigan University";
inlineCC.ParagraphItems.Add(text);
//Fill the C# experience level
cellPara1 = row1.Cells[0].ChildEntities[7] as WParagraph;
dropDownCC = cellPara1.ChildEntities.LastItem as InlineContentControl;
text = new WTextRange(document1);
text.ApplyCharacterFormat(dropDownCC.BreakCharacterFormat);
text.Text = dropDownCC.ContentControlProperties.ContentControlListItems[2].DisplayText;
dropDownCC.ParagraphItems.Add(text);
//Fill the VB experience level
cellPara1 = row1.Cells[0].ChildEntities[9] as WParagraph;
dropDownCC = cellPara1.ChildEntities.LastItem as InlineContentControl;
text = new WTextRange(document1);
text.ApplyCharacterFormat(dropDownCC.BreakCharacterFormat);
text.Text = dropDownCC.ContentControlProperties.ContentControlListItems[1].DisplayText;
dropDownCC.ParagraphItems.Add(text);
#endregion
//Creates memory stream
MemoryStream saveStream = new MemoryStream();
//Saves and closes the Word document instance
document1.Save(saveStream, FormatType.Docx);
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", outputStream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
document1.Close();
{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Content-Controls/Fill-form-in-Word-document).

### Data Binding with Content Controls (XML Mapping)

Word allows you to store XML data, named *custom XML parts*, in a Word document. You can control the display of this data by binding content controls to elements in a custom XML part. When you open the Word document, the content controls display the values of the XML elements. Any changes that you make to the text in the content controls are saved in the custom XML part (two-way data binding). Refer to the following code sample to map custom XML parts to content control.

{% tabs %}
{% highlight c# %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Adds new XmlPart to the document
CustomXMLPart xmlPart = new CustomXMLPart(document);
//Loads the xml code
xmlPart.LoadXML(@"<books><book><author>Matt Hank</author><title>New Migration Paths of the Red Breasted Robin</title><genre>New non-fiction</genre><price>29.95</price><pub_datee>12/1/2007</pub_datee> <abstract>New You see them in the spring outside your windows.</abstract></book></books>");
//Adds the text
paragraph.AppendText("Book author name : ");
//Adds new content control to the paragraph
InlineContentControl control = paragraph.AppendInlineContentControl(ContentControlType.Text) as InlineContentControl;
//Creates the XML mapping on a content control for specified XPath
control.ContentControlProperties.XmlMapping.SetMapping("/books/book/author", "", xmlPart);
//Selects the single node
CustomXMLNode node = xmlPart.SelectSingleNode("/books/book/title");
//Adds another paragraph
paragraph = section.AddParagraph();
//Adds text
paragraph.AppendText("Book title: ");
//Appends content control to second paragraph
control = paragraph.AppendInlineContentControl(ContentControlType.Text) as InlineContentControl;
//Creates the XML data mapping on a content control for specified node
control.ContentControlProperties.XmlMapping.SetMappingByNode(node);
//Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Creates a new Word document 
Dim document As WordDocument = New WordDocument
'Adds new section to the document
Dim section As IWSection = document.AddSection
'Adds new paragraph to the section
Dim paragraph As IWParagraph = section.AddParagraph
'Adds new XmlPart to the document
Dim xmlPart As CustomXMLPart = New CustomXMLPart(document)
'Loads the xml code
xmlPart.LoadXML("<books><book><author>Matt Hank</author><title>New Migration Paths of the Red Breasted Robin</title><genre>New non-fiction</genre><price>29.95</price><pub_datee>12/1/2007</pub_datee> <abstract>New You see them in the spring outside your windows.</abstract></book></books>")
'Adds text
paragraph.AppendText("Book author name : ")
'Adds new content control to the paragraph
Dim control As InlineContentControl = CType(paragraph.AppendInlineContentControl(ContentControlType.Text), InlineContentControl)
'Creates the XML mapping on a content control for specified XPath
control.ContentControlProperties.XmlMapping.SetMapping("/books/book/author", "", xmlPart)
'Selects the single node
CustomXMLNode node = xmlPart.SelectSingleNode("/books/book/title");
'Adds another paragraph
paragraph = section.AddParagraph
'Adds text
paragraph.AppendText("Book title: ");
'Appends content control to second paragraph
control = CType(paragraph.AppendInlineContentControl(ContentControlType.Text), InlineContentControl)
'Creates the XML data mapping on a content control for specified node
control.ContentControlProperties.XmlMapping.SetMappingByNode(node)
'Saves and closes the Word document instance
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
//Adds new XmlPart to the document.
CustomXMLPart xmlPart = new CustomXMLPart(document);
//Loads the xml code
xmlPart.LoadXML(@"<books><book><author>Matt Hank</author><title>New Migration Paths of the Red Breasted Robin</title><genre>New non-fiction</genre><price>29.95</price><pub_datee>12/1/2007</pub_datee> <abstract>New You see them in the spring outside your windows.</abstract></book></books>");
//Adds the text
paragraph.AppendText("Book author name : ");
//Adds new content control to the paragraph
InlineContentControl control = paragraph.AppendInlineContentControl(ContentControlType.Text) as InlineContentControl;
//Creates the XML mapping on a content control for specified XPath
control.ContentControlProperties.XmlMapping.SetMapping("/books/book/author", "", xmlPart);
//Selects the single node
CustomXMLNode node = xmlPart.SelectSingleNode("/books/book/title");
//Adds another paragraph
paragraph = section.AddParagraph();
//Adds text
paragraph.AppendText("Book title: ");
//Appends content control to second paragraph
control = paragraph.AppendInlineContentControl(ContentControlType.Text) as InlineContentControl;
//Creates the XML data mapping on a content control for specified node
control.ContentControlProperties.XmlMapping.SetMappingByNode(node);
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word file in local machine
Save(stream, "Sample.docx");
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
document.Close();
{% endhighlight %}

{% highlight ASP.NET CORE %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Adds new XmlPart to the document
CustomXMLPart xmlPart = new CustomXMLPart(document);
//Loads the xml code
xmlPart.LoadXML(@"<books><book><author>Matt Hank</author><title>New Migration Paths of the Red Breasted Robin</title><genre>New non-fiction</genre><price>29.95</price><pub_datee>12/1/2007</pub_datee> <abstract>New You see them in the spring outside your windows.</abstract></book></books>");
//Adds text
paragraph.AppendText("Book author name : ");
//Adds new content control to the paragraph
InlineContentControl control = paragraph.AppendInlineContentControl(ContentControlType.Text) as InlineContentControl;
//Creates the XML mapping on a content control for specified XPath
control.ContentControlProperties.XmlMapping.SetMapping("/books/book/author", "", xmlPart);
//Selects the single node
CustomXMLNode node = xmlPart.SelectSingleNode("/books/book/title");
//Adds another paragraph
paragraph = section.AddParagraph();
//Adds text
paragraph.AppendText("Book title: ");
//Appends content control to second paragraph
control = paragraph.AppendInlineContentControl(ContentControlType.Text) as InlineContentControl;
//Creates the XML data mapping on a content control for specified node
control.ContentControlProperties.XmlMapping.SetMappingByNode(node);
//Creates memory stream
MemoryStream outputStream = new MemoryStream();
//Saves and closes the Word document instance
document.Save(outputStream, FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight XAMARIN %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Adds new XmlPart to the document
CustomXMLPart xmlPart = new CustomXMLPart(document);
//Loads the xml code
xmlPart.LoadXML(@"<books><book><author>Matt Hank</author><title>New Migration Paths of the Red Breasted Robin</title><genre>New non-fiction</genre><price>29.95</price><pub_datee>12/1/2007</pub_datee> <abstract>New You see them in the spring outside your windows.</abstract></book></books>");
//Adds new content control to the paragraph
InlineContentControl control = paragraph.AppendInlineContentControl(ContentControlType.Text) as InlineContentControl;
//Creates the XML mapping on a content control for specified XPath
control.ContentControlProperties.XmlMapping.SetMapping("/books/book/author", "", xmlPart);
//Selects the single node
CustomXMLNode node = xmlPart.SelectSingleNode("/books/book/title");
//Adds another paragraph
paragraph = section.AddParagraph();
//Adds text
paragraph.AppendText("Book title: ");
//Appends content control to second paragraph
control = paragraph.AppendInlineContentControl(ContentControlType.Text) as InlineContentControl;
//Creates the XML data mapping on a content control for specified node
control.ContentControlProperties.XmlMapping.SetMappingByNode(node);
//Creates memory stream
MemoryStream outputStream = new MemoryStream();
//Saves and closes the Word document instance
document.Save(outputStream, FormatType.Docx);
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", outputStream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
document.Close();
{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Content-Controls/Xml-mapping).

## Types of Content Controls

The following types of content controls can be created by using the Essential DocIO.

* Rich Text
* Plain Text
* Check Box
* Date picker
* Drop-Down List and Combo Box
* Picture

### Rich Text

A rich text content control contains text or other items, such as tables, pictures, or other content controls. The following code illustrates how to add new rich text content control. 

{% tabs %}
{% highlight c# %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds one section and one paragraph to the document
document.EnsureMinimal();
//Gets the last paragraph.
WParagraph paragraph = document.LastParagraph;
//Adds text to the paragraph
paragraph.AppendText("A new text is added to the paragraph. ");
//Appends rich text content control to the paragraph
InlineContentControl richTextControl = paragraph.AppendInlineContentControl(ContentControlType.RichText) as InlineContentControl;
WTextRange textRange = new WTextRange(document);
textRange.Text = "Rich text content control.";
//Adds new text to the rich text content control
richTextControl.ParagraphItems.Add(textRange);
WPicture picture = new WPicture(document);
picture.LoadImage(Image.FromFile("Image.png"));
picture.Height = 100;
picture.Width = 100;
//Adds new picture to the rich text content control
richTextControl.ParagraphItems.Add(picture);
//Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Creates a new Word document 
Dim document As WordDocument = New WordDocument
'Adds one section and one paragraph to the document
document.EnsureMinimal()
'Adds new paragraph to the section
Dim paragraph As WParagraph = document.LastParagraph
'Adds text to the paragraph
paragraph.AppendText("A new text is added to the paragraph. ")
'Appends rich text content control to the paragraph
Dim richTextControl As InlineContentControl = CType(paragraph.AppendInlineContentControl(ContentControlType.RichText), InlineContentControl)
Dim textRange As WTextRange = New WTextRange(document)
textRange.Text = "Rich text content control."
'Adds new text to the rich text content control
richTextControl.ParagraphItems.Add(textRange)
Dim picture As WPicture = New WPicture(document)
picture.LoadImage(Image.FromFile("Image.png"))
picture.Height = 100
picture.Width = 100
'Adds new picture to the rich text content control
richTextControl.ParagraphItems.Add(picture)
'Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight UWP %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds one section and one paragraph to the document
document.EnsureMinimal();
//Gets the last paragraph
WParagraph paragraph = document.LastParagraph;
//Adds text to the paragraph
paragraph.AppendText("A new text is added to the paragraph. ");
//Appends rich text content control to the paragraph
InlineContentControl richTextControl = paragraph.AppendInlineContentControl(ContentControlType.RichText) as InlineContentControl;
WTextRange textRange = new WTextRange(document);
textRange.Text = "Rich text content control.";
//Adds new text to the rich text content control
richTextControl.ParagraphItems.Add(textRange);
WPicture picture = new WPicture(document);
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream pictureStream = assembly.GetManifestResourceStream("Sample.Assets.Image.png");
picture.LoadImage(pictureStream);
picture.Height = 100;
picture.Width = 100;
//Adds new picture to the rich text content control
richTextControl.ParagraphItems.Add(picture);
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word file in local machine
Save(stream, "Sample.docx");
document.Close();
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight ASP.NET CORE %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds one section and one paragraph to the document
document.EnsureMinimal();
//Gets the last paragraph
WParagraph paragraph = document.LastParagraph;
//Adds text to the paragraph
paragraph.AppendText("A new text is added to the paragraph. ");
//Appends rich text content control to the paragraph
InlineContentControl richTextControl = paragraph.AppendInlineContentControl(ContentControlType.RichText) as InlineContentControl;
WTextRange textRange = new WTextRange(document);
textRange.Text = "Rich text content control.";
//Adds new text to the rich text content control
richTextControl.ParagraphItems.Add(textRange);
WPicture picture = new WPicture(document);
Stream imageStream = new FileStream(@"D:\Image.png", FileMode.Open, FileAccess.Read);
//Adds image from stream
picture.LoadImage(imageStream);
picture.Height = 100;
picture.Width = 100;
//Adds new picture to the rich text content control
richTextControl.ParagraphItems.Add(picture);
//Creates memory stream
MemoryStream outputStream = new MemoryStream();
//Saves and closes the Word document instance
document.Save(outputStream, FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight XAMARIN %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds one section and one paragraph to the document
document.EnsureMinimal();
//Gets the last paragraph
WParagraph paragraph = document.LastParagraph;
//Adds text to the paragraph
paragraph.AppendText("A new text is added to the paragraph. ");
//Appends rich text content control to the paragraph
InlineContentControl richTextControl = paragraph.AppendInlineContentControl(ContentControlType.RichText) as InlineContentControl;
WTextRange textRange = new WTextRange(document);
textRange.Text = "Rich text content control.";
//Adds new text to the rich text content control
richTextControl.ParagraphItems.Add(textRange);
WPicture picture = new WPicture(document);
Stream imageStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Image.png");
//Adds image from stream
picture.LoadImage(imageStream);
picture.Height = 100;
picture.Width = 100;
//Adds new picture to the rich text content control
richTextControl.ParagraphItems.Add(picture);
//Creates memory stream
MemoryStream outputStream = new MemoryStream();
//Saves and closes the Word document instance
document.Save(outputStream, FormatType.Docx);
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", outputStream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
document.Close();
{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Content-Controls/Rich-text-content-control).

### Plain Text

A plain text content control contains text and cannot contain other items, such as tables, pictures, or other content controls. Refer to the following code to add plain text content control.

{% tabs %}
{% highlight c# %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds one section and one paragraph to the document
document.EnsureMinimal();
//Gets the last paragraph
WParagraph paragraph = document.LastParagraph;
//Adds text to the paragraph
paragraph.AppendText("A new text is added to the paragraph. ");
//Appends plain text content control to the paragraph
InlineContentControl plainTextControl = paragraph.AppendInlineContentControl(ContentControlType.Text) as InlineContentControl;
WTextRange textRange = new WTextRange(document);
textRange.Text = "Plain text content control.";
//Adds new text to the plain text content control
plainTextControl.ParagraphItems.Add(textRange);
//Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Creates a new Word document 
Dim document As WordDocument = New WordDocument
'Adds one section and one paragraph to the document
document.EnsureMinimal()
'Adds new paragraph to the section
Dim paragraph As WParagraph = document.LastParagraph
'Adds text to the paragraph
paragraph.AppendText("A new text is added to the paragraph. ")
'Appends plain text content control to the paragraph
Dim plainTextControl As InlineContentControl = CType(paragraph.AppendInlineContentControl(ContentControlType.Text), InlineContentControl)
Dim textRange As WTextRange = New WTextRange(document)
textRange.Text = "Plain text content control."
'Adds new text to the plain text content control
plainTextControl.ParagraphItems.Add(textRange)
'Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight UWP %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds one section and one paragraph to the document
document.EnsureMinimal();
//Gets the last paragraph
WParagraph paragraph = document.LastParagraph;
//Adds text to the paragraph
paragraph.AppendText("A new text is added to the paragraph. ");
//Appends plain text content control to the paragraph
InlineContentControl plainTextControl = paragraph.AppendInlineContentControl(ContentControlType.Text) as InlineContentControl;
WTextRange textRange = new WTextRange(document);
textRange.Text = "Plain text content control.";
//Adds new text to the plain text content control
plainTextControl.ParagraphItems.Add(textRange);
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word file in local machine
Save(stream, "Sample.docx");
document.Close();//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight ASP.NET CORE %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds one section and one paragraph to the document
document.EnsureMinimal();
//Gets the last paragraph
WParagraph paragraph = document.LastParagraph;
//Adds text to the paragraph
paragraph.AppendText("A new text is added to the paragraph. ");
//Appends plain text content control to the paragraph
InlineContentControl plainTextControl = paragraph.AppendInlineContentControl(ContentControlType.Text) as InlineContentControl;
WTextRange textRange = new WTextRange(document);
textRange.Text = "Plain text content control.";
//Adds new text to the plain text content control
plainTextControl.ParagraphItems.Add(textRange);
//Creates memory stream
MemoryStream outputStream = new MemoryStream();
//Saves and closes the Word document instance
document.Save(outputStream, FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight XAMARIN %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds one section and one paragraph to the document
document.EnsureMinimal();
//Gets the last paragraph
WParagraph paragraph = document.LastParagraph;
//Adds text to the paragraph
paragraph.AppendText("A new text is added to the paragraph. ");
//Appends plain text content control to the paragraph
InlineContentControl plainTextControl = paragraph.AppendInlineContentControl(ContentControlType.Text) as InlineContentControl;
WTextRange textRange = new WTextRange(document);
textRange.Text = "Plain text content control.";
//Adds new text to the plain text content control
plainTextControl.ParagraphItems.Add(textRange);
//Creates memory stream
MemoryStream outputStream = new MemoryStream();
//Saves and closes the Word document instance
document.Save(outputStream, FormatType.Docx);
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", outputStream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
document.Close();
{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Content-Controls/Plain-text-content-control).

### Check Box

A check box content control provides a UI that represents a binary state: checked or unchecked. Default state for check box is unchecked. Refer to the following code to add check box content control.

{% tabs %}
{% highlight c# %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds one section and one paragraph to the document
document.EnsureMinimal();
//Gets the last paragraph.
WParagraph paragraph = document.LastParagraph;
//Adds text to the paragraph
paragraph.AppendText("A new text is added to the paragraph. ");
//Appends checkbox content control to the paragraph
InlineContentControl checkBox = paragraph.AppendInlineContentControl(ContentControlType.CheckBox) as InlineContentControl;
checkBox.ContentControlProperties.IsChecked = true;
//Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Creates a new Word document 
Dim document As WordDocument = New WordDocument
'Adds one section and one paragraph to the document
document.EnsureMinimal()
'Adds new paragraph to the section
Dim paragraph As WParagraph = document.LastParagraph
'Adds text to the paragraph
paragraph.AppendText("A new text is added to the paragraph. ")
'Appends checkbox content control to the paragraph
Dim checkBox As InlineContentControl = CType(paragraph.AppendInlineContentControl(ContentControlType. CheckBox), InlineContentControl)
checkBox.ContentControlProperties.IsChecked = True 
'Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight UWP %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds one section and one paragraph to the document
document.EnsureMinimal();
//Gets the last paragraph
WParagraph paragraph = document.LastParagraph;
//Adds text to the paragraph
paragraph.AppendText("A new text is added to the paragraph. ");
//Appends checkbox content control to the paragraph
InlineContentControl checkBox = paragraph.AppendInlineContentControl(ContentControlType.CheckBox) as InlineContentControl;
checkBox.ContentControlProperties.IsChecked = true;
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word file in local machine
Save(stream, "Sample.docx");
document.Close();
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight ASP.NET CORE %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds one section and one paragraph to the document
document.EnsureMinimal();
//Gets the last paragraph
WParagraph paragraph = document.LastParagraph;
//Adds text to the paragraph
paragraph.AppendText("A new text is added to the paragraph. ");
//Appends picture content control to the paragraph
InlineContentControl checkBox = paragraph.AppendInlineContentControl(ContentControlType.CheckBox) as InlineContentControl;
checkBox.ContentControlProperties.IsChecked = true;
//Creates memory stream
MemoryStream outputStream = new MemoryStream();
//Saves and closes the Word document instance
document.Save(outputStream, FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight XAMARIN %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds one section and one paragraph to the document
document.EnsureMinimal();
//Gets the last paragraph
WParagraph paragraph = document.LastParagraph;
//Adds text to the paragraph
paragraph.AppendText("A new text is added to the paragraph. ");
//Appends picture content control to the paragraph
InlineContentControl checkBox = paragraph.AppendInlineContentControl(ContentControlType.CheckBox) as InlineContentControl;
checkBox.ContentControlProperties.IsChecked = true;
//Creates memory stream
MemoryStream outputStream = new MemoryStream();
//Saves and closes the Word document instance
document.Save(outputStream, FormatType.Docx);
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", outputStream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
document.Close();
{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Content-Controls/Check-box-content-control).

### Date picker

A date picker content control provides a calendar UI for selecting a date. The calendar appears when you click the drop-down arrow in the content control. You can use regional calendars and different date formats. Refer to the following code to add date picker content control.

{% tabs %}
{% highlight c# %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds one section and one paragraph to the document
document.EnsureMinimal();
//Gets the last paragraph
WParagraph paragraph = document.LastParagraph;
//Adds text to the paragraph
paragraph.AppendText("Select Date: ");
//Appends date picker content control to the paragraph
InlineContentControl datePicker = paragraph.AppendInlineContentControl(ContentControlType.Date) as InlineContentControl;
WTextRange textRange = new WTextRange(document);
//Sets today's date to display
textRange.Text = DateTime.Now.ToShortDateString();
datePicker.ParagraphItems.Add(textRange);
//Sets calendar type for the date picker content control
datePicker.ContentControlProperties.DateCalendarType = CalendarType.Gregorian;
//Sets the format for date to display
datePicker.ContentControlProperties.DateDisplayFormat = "M/d/yyyy";
//Sets the language format for the date
datePicker.ContentControlProperties.DateDisplayLocale = LocaleIDs.en_US;
//Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Creates a new Word document 
Dim document As WordDocument = New WordDocument
'Adds one section and one paragraph to the document
document.EnsureMinimal()
'Adds new paragraph to the section
Dim paragraph As WParagraph = document.LastParagraph
'Adds text to the paragraph
paragraph.AppendText("Select Date: ")
'Appends date picker content control to the paragraph
Dim datePicker As InlineContentControl = CType(paragraph.AppendInlineContentControl(ContentControlType.Date), InlineContentControl)
Dim textRange As WTextRange = New WTextRange(document)
'Sets today's date to display
textRange.Text = DateTime.Now.ToShortDateString
datePicker.ParagraphItems.Add(textRange)
'Sets calendar type for the date picker content control
datePicker.ContentControlProperties.DateCalendarType = CalendarType.Gregorian
'Sets the format for date to display
datePicker.ContentControlProperties.DateDisplayFormat = "M/d/yyyy"
'Sets the language format for the date
datePicker.ContentControlProperties.DateDisplayLocale = LocaleIDs.en_US
'Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight UWP %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds one section and one paragraph to the document
document.EnsureMinimal();
//Gets the last paragraph
WParagraph paragraph = document.LastParagraph;
//Adds text to the paragraph
paragraph.AppendText("Select Date: ");
//Appends date picker content control to the paragraph
InlineContentControl datePicker = paragraph.AppendInlineContentControl(ContentControlType.Date) as InlineContentControl;
WTextRange textRange = new WTextRange(document);
//Sets today's date to display
textRange.Text = DateTime.Now.ToShortDateString();
datePicker.ParagraphItems.Add(textRange);
//Sets calendar type for the date picker content control
datePicker.ContentControlProperties.DateCalendarType = CalendarType.Gregorian;
//Sets the format for date to display
datePicker.ContentControlProperties.DateDisplayFormat = "M/d/yyyy";
//Sets the language format for the date
datePicker.ContentControlProperties.DateDisplayLocale = LocaleIDs.en_US;
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word file in local machine
Save(stream, "Sample.docx");
document.Close();
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight ASP.NET CORE %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds one section and one paragraph to the document
document.EnsureMinimal();
//Gets the last paragraph
WParagraph paragraph = document.LastParagraph;
//Adds text to the paragraph
paragraph.AppendText("Select Date: ");
//Appends date picker content control to the paragraph
InlineContentControl datePicker = paragraph.AppendInlineContentControl(ContentControlType.Date) as InlineContentControl;
WTextRange textRange = new WTextRange(document);
//Sets today's date to display
textRange.Text = DateTime.Now.ToString();
datePicker.ParagraphItems.Add(textRange);
//Sets calendar type for the date picker content control
datePicker.ContentControlProperties.DateCalendarType = CalendarType.Gregorian;
//Sets the format for date to display
datePicker.ContentControlProperties.DateDisplayFormat = "M/d/yyyy";
//Sets the language format for the date
datePicker.ContentControlProperties.DateDisplayLocale = LocaleIDs.en_US;
//Creates memory stream
MemoryStream outputStream = new MemoryStream();
//Saves and closes the Word document instance
document.Save(outputStream, FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight XAMARIN %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds one section and one paragraph to the document
document.EnsureMinimal();
//Gets the last paragraph
WParagraph paragraph = document.LastParagraph;
//Adds text to the paragraph
paragraph.AppendText("Select Date: ");
//Appends date picker content control to the paragraph
InlineContentControl datePicker = paragraph.AppendInlineContentControl(ContentControlType.Date) as InlineContentControl;
WTextRange textRange = new WTextRange(document);
//Sets today's date to display
textRange.Text = DateTime.Now.ToString();
datePicker.ParagraphItems.Add(textRange);
//Sets calendar type for the date picker content control
datePicker.ContentControlProperties.DateCalendarType = CalendarType.Gregorian;
//Sets the format for date to display
datePicker.ContentControlProperties.DateDisplayFormat = "M/d/yyyy";
//Sets the language format for the date
datePicker.ContentControlProperties.DateDisplayLocale = LocaleIDs.en_US;
//Creates memory stream
MemoryStream outputStream = new MemoryStream();
//Saves and closes the Word document instance
document.Save(outputStream, FormatType.Docx);
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", outputStream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
document.Close();
{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Content-Controls/Date-picker-content-control).

### Drop-Down List and Combo Box

A drop-down list content control and combo box content control displays a list of items you can select. Unlike a drop-down list, the combo box allows to add your own items. Refer to the following code to add drop-down list and combo box content controls.

{% tabs %}
{% highlight c# %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
WParagraph paragraph = section.AddParagraph() as WParagraph;
//Appends dropdown list content control to the paragraph
InlineContentControl dropdown = paragraph.AppendInlineContentControl(ContentControlType.DropDownList) as InlineContentControl;
WTextRange textRange = new WTextRange(document);
//Sets default option to display  
textRange.Text = "Choose an item from drop down list";
dropdown.ParagraphItems.Add(textRange);
//Creates an item for dropdown list
ContentControlListItem item = new ContentControlListItem();
//Sets the text to be displayed as list item
item.DisplayText = "ASP.NET MVC";
//Sets the value to the list item
item.Value = "1";
//Adds item to the dropdown list
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
item = new ContentControlListItem();
item.DisplayText = "Windows Forms";
item.Value = "2";
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
item = new ContentControlListItem();
item.DisplayText = "WPF";
item.Value = "3";
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
//Adds new paragraph to the section
paragraph = section.AddParagraph() as WParagraph;
//Appends combo box content control to the paragraph
InlineContentControl comboBox = paragraph.AppendInlineContentControl(ContentControlType.ComboBox) as InlineContentControl;
textRange = new WTextRange(document);
//Sets default option to display  
textRange.Text = "Choose an item from combo box";
comboBox.ParagraphItems.Add(textRange);
//Creates an item for combo box
item = new ContentControlListItem();
//Sets the text to be displayed as list item
item.DisplayText = "Word to HTML";
//Sets the value to the list item
item.Value = "1";
comboBox.ContentControlProperties.ContentControlListItems.Add(item);
item = new ContentControlListItem();
item.DisplayText = "Word to Image";
item.Value = "2";
comboBox.ContentControlProperties.ContentControlListItems.Add(item);
item = new ContentControlListItem();
item.DisplayText = "Word to PDF";
item.Value = "3";
comboBox.ContentControlProperties.ContentControlListItems.Add(item);
//Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Creates a new Word document 
Dim document As WordDocument = New WordDocument
'Adds new section to the document
Dim section As IWSection = document.AddSection
'Adds new paragraph to the section
Dim paragraph As WParagraph = CType(section.AddParagraph, WParagraph)
'Appends dropdown list content control to the paragraph
Dim dropdown As InlineContentControl = CType(paragraph.AppendInlineContentControl(ContentControlType.DropDownList), InlineContentControl)
Dim textRange As WTextRange = New WTextRange(document)
'Sets default option to display  
textRange.Text = "Choose an item from drop down list"
dropdown.ParagraphItems.Add(textRange)
'Creates an item for dropdown list
Dim item As ContentControlListItem = New ContentControlListItem
'Sets the text to be displayed as list item
item.DisplayText = "ASP.NET MVC"
'Sets the value to the list item
item.Value = "1"
'Adds item to the dropdown list
dropdown.ContentControlProperties.ContentControlListItems.Add(item)
item = New ContentControlListItem
item.DisplayText = "Windows Forms"
item.Value = "2"
dropdown.ContentControlProperties.ContentControlListItems.Add(item)
item = New ContentControlListItem
item.DisplayText = "WPF"
item.Value = "3"
dropdown.ContentControlProperties.ContentControlListItems.Add(item)
'Adds new paragraph to the section
paragraph = CType(section.AddParagraph, WParagraph)
'Appends combo box content control to the paragraph
Dim comboBox As InlineContentControl = CType(paragraph.AppendInlineContentControl(ContentControlType.ComboBox), InlineContentControl)
textRange = New WTextRange(document)
'Sets default option to display  
textRange.Text = "Choose an item from combo box"
comboBox.ParagraphItems.Add(textRange)
'Creates an item for combo box
item = New ContentControlListItem
'Sets the text to be displayed as list item
item.DisplayText = "Word to HTML"
'Sets the value to the list item
item.Value = "1"
comboBox.ContentControlProperties.ContentControlListItems.Add(item)
item = New ContentControlListItem
item.DisplayText = "Word to Image"
item.Value = "2"
comboBox.ContentControlProperties.ContentControlListItems.Add(item)
item = New ContentControlListItem
item.DisplayText = "Word to PDF"
item.Value = "3"
comboBox.ContentControlProperties.ContentControlListItems.Add(item)
'Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight UWP %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
WParagraph paragraph = section.AddParagraph() as WParagraph;
//Appends dropdown list content control to the paragraph
InlineContentControl dropdown = paragraph.AppendInlineContentControl(ContentControlType.DropDownList) as InlineContentControl;
WTextRange textRange = new WTextRange(document);
//Sets default option to display  
textRange.Text = "Choose an item from drop down list";
dropdown.ParagraphItems.Add(textRange);
//Creates an item for dropdown list
ContentControlListItem item = new ContentControlListItem();
//Sets the text to be displayed as list item
item.DisplayText = "ASP.NET MVC";
//Sets the value to the list item
item.Value = "1";
//Adds item to the dropdown list
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
item = new ContentControlListItem();
item.DisplayText = "Windows Forms";
item.Value = "2";
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
item = new ContentControlListItem();
item.DisplayText = "WPF";
item.Value = "3";
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
//Adds new paragraph to the section
paragraph = section.AddParagraph() as WParagraph;
//Appends combo box content control to the paragraph
InlineContentControl comboBox = paragraph.AppendInlineContentControl(ContentControlType.ComboBox) as InlineContentControl;
textRange = new WTextRange(document);
//Sets default option to display  
textRange.Text = "Choose an item from combo box";
comboBox.ParagraphItems.Add(textRange);
//Creates an item for combo box
item = new ContentControlListItem();
//Sets the text to be displayed as list item
item.DisplayText = "Word to HTML";
//Sets the value to the list item
item.Value = "1";
comboBox.ContentControlProperties.ContentControlListItems.Add(item);
item = new ContentControlListItem();
item.DisplayText = "Word to Image";
item.Value = "2";
comboBox.ContentControlProperties.ContentControlListItems.Add(item);
item = new ContentControlListItem();
item.DisplayText = "Word to PDF";
item.Value = "3";
comboBox.ContentControlProperties.ContentControlListItems.Add(item);
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word file in local machine
Save(stream, "Sample.docx");
document.Close();
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight ASP.NET CORE %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
WParagraph paragraph = section.AddParagraph() as WParagraph;
//Adds text to the paragraph
paragraph.AppendText("Choose your platform: ");
//Appends dropdown list content control to the paragraph
InlineContentControl dropdown = paragraph.AppendInlineContentControl(ContentControlType.DropDownList) as InlineContentControl;
WTextRange textRange = new WTextRange(document);
//Sets default option to display  
textRange.Text = "Choose an item";
dropdown.ParagraphItems.Add(textRange);
//Creates an item for dropdown list
ContentControlListItem item = new ContentControlListItem();
//Sets the text to be displayed as list item
item.DisplayText = "ASP.NET MVC";
//Sets the value to the list item
item.Value = "1";
//Adds item to the dropdown list
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
item = new ContentControlListItem();
item.DisplayText = "Windows Forms";
item.Value = "2";
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
item = new ContentControlListItem();
item.DisplayText = "WPF";
item.Value = "3";
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
//Adds new paragraph to the section
paragraph = section.AddParagraph() as WParagraph;
//Adds text to the paragraph
paragraph.AppendText("Choose the conversion: ");
//Appends combo box content control to the paragraph
InlineContentControl comboBox = paragraph.AppendInlineContentControl(ContentControlType.ComboBox) as InlineContentControl;
textRange = new WTextRange(document);
//Sets default option to display  
textRange.Text = "Choose an item";
comboBox.ParagraphItems.Add(textRange);
//Creates an item for combo box
item = new ContentControlListItem();
//Sets the text to be displayed as list item
item.DisplayText = "Word to HTML";
//Sets the value to the list item
item.Value = "1";
comboBox.ContentControlProperties.ContentControlListItems.Add(item);
item = new ContentControlListItem();
item.DisplayText = "Word to Image";
item.Value = "2";
comboBox.ContentControlProperties.ContentControlListItems.Add(item);
item = new ContentControlListItem();
item.DisplayText = "Word to PDF";
item.Value = "3";
comboBox.ContentControlProperties.ContentControlListItems.Add(item);
//Creates memory stream
MemoryStream outputStream = new MemoryStream();
//Saves and closes the Word document instance
document.Save(outputStream, FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight XAMARIN %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
WParagraph paragraph = section.AddParagraph() as WParagraph;
//Adds text to the paragraph
paragraph.AppendText("Choose your platform: ");
//Appends dropdown list content control to the paragraph
InlineContentControl dropdown = paragraph.AppendInlineContentControl(ContentControlType.DropDownList) as InlineContentControl;
WTextRange textRange = new WTextRange(document);
//Sets default option to display  
textRange.Text = "Choose an item";
dropdown.ParagraphItems.Add(textRange);
//Creates an item for dropdown list
ContentControlListItem item = new ContentControlListItem();
//Sets the text to be displayed as list item
item.DisplayText = "ASP.NET MVC";
//Sets the value to the list item
item.Value = "1";
//Adds item to the dropdown list
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
item = new ContentControlListItem();
item.DisplayText = "Windows Forms";
item.Value = "2";
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
item = new ContentControlListItem();
item.DisplayText = "WPF";
item.Value = "3";
dropdown.ContentControlProperties.ContentControlListItems.Add(item);
//Adds new paragraph to the section
paragraph = section.AddParagraph() as WParagraph;
//Adds text to the paragraph
paragraph.AppendText("Choose the conversion: ");
//Appends combo box content control to the paragraph
InlineContentControl comboBox = paragraph.AppendInlineContentControl(ContentControlType.ComboBox) as InlineContentControl;
textRange = new WTextRange(document);
//Sets default option to display  
textRange.Text = "Choose an item";
comboBox.ParagraphItems.Add(textRange);
//Creates an item for combo box
item = new ContentControlListItem();
//Sets the text to be displayed as list item
item.DisplayText = "Word to HTML";
//Sets the value to the list item
item.Value = "1";
comboBox.ContentControlProperties.ContentControlListItems.Add(item);
item = new ContentControlListItem();
item.DisplayText = "Word to Image";
item.Value = "2";
comboBox.ContentControlProperties.ContentControlListItems.Add(item);
item = new ContentControlListItem();
item.DisplayText = "Word to PDF";
item.Value = "3";
comboBox.ContentControlProperties.ContentControlListItems.Add(item);
//Creates memory stream
MemoryStream outputStream = new MemoryStream();
//Saves and closes the Word document instance
document.Save(outputStream, FormatType.Docx);
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", outputStream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
document.Close();
{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Content-Controls/Drop-down-list-and-combo-box).

### Picture

A picture content control displays an image. Refer to the following code to add new picture content control.

{% tabs %}
{% highlight c# %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds one section and one paragraph to the document
document.EnsureMinimal();
//Gets the last paragraph.
WParagraph paragraph = document.LastParagraph;
//Adds text to the paragraph
paragraph.AppendText("A new text is added to the paragraph. ");
//Appends picture content control to the paragraph
InlineContentControl pictureContentControl = paragraph.AppendInlineContentControl(ContentControlType.Picture) as InlineContentControl;
//Creates a new image instance and load image 
WPicture picture = new WPicture(document);
picture.LoadImage(Image.FromFile("Image.png"));
//Adds picture to the picture content control
pictureContentControl.ParagraphItems.Add(picture);
//Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Creates a new Word document 
Dim document As WordDocument = New WordDocument
'Adds one section and one paragraph to the document
document.EnsureMinimal()
'Adds new paragraph to the section
Dim paragraph As WParagraph = document.LastParagraph
'Adds text to the paragraph
paragraph.AppendText("A new text is added to the paragraph. ")
'Appends picture content control to the paragraph
Dim pictureContentControl As InlineContentControl = CType(paragraph.AppendInlineContentControl(ContentControlType.Picture), InlineContentControl)
'Creates a new image instance and load image 
Dim picture As WPicture = New WPicture(document)
picture.LoadImage(Image.FromFile("Image.png"))
'Adds picture to the picture content control
pictureContentControl.ParagraphItems.Add(picture)
'Saves and closes the Word document instance
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight UWP %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds one section and one paragraph to the document
document.EnsureMinimal();
//Gets the last paragraph
WParagraph paragraph = document.LastParagraph;
//Adds text to the paragraph
paragraph.AppendText("A new text is added to the paragraph. ");
//Appends picture content control to the paragraph
InlineContentControl pictureContentControl = paragraph.AppendInlineContentControl(ContentControlType.Picture) as InlineContentControl;
//Creates a new image instance and load image 
WPicture picture = new WPicture(document);
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream pictureStream = assembly.GetManifestResourceStream("Sample.Assets.Image.png");
picture.LoadImage(pictureStream);
//Adds picture to the picture content control
pictureContentControl.ParagraphItems.Add(picture);
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word file in local machine
Save(stream, "Sample.docx");
document.Close();
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight ASP.NET CORE %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds one section and one paragraph to the document
document.EnsureMinimal();
//Gets the last paragraph
WParagraph paragraph = document.LastParagraph;
//Adds text to the paragraph
paragraph.AppendText("A new text is added to the paragraph. ");
//Appends picture content control to the paragraph
InlineContentControl pictureContentControl = paragraph.AppendInlineContentControl(ContentControlType.Picture) as InlineContentControl;
//Creates a new image instance and load image 
WPicture picture = new WPicture(document);
Stream imageStream = new FileStream(@"D:\Image.png", FileMode.Open, FileAccess.Read);
//Adds image from stream
picture.LoadImage(imageStream);
//Adds picture to the picture content control
pictureContentControl.ParagraphItems.Add(picture);
//Creates memory stream
MemoryStream outputStream = new MemoryStream();
//Saves and closes the Word document instance
document.Save(outputStream, FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight XAMARIN %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds one section and one paragraph to the document
document.EnsureMinimal();
//Gets the last paragraph
WParagraph paragraph = document.LastParagraph;
//Adds text to the paragraph
paragraph.AppendText("A new text is added to the paragraph. ");
//Appends picture content control to the paragraph
InlineContentControl pictureContentControl = paragraph.AppendInlineContentControl(ContentControlType.Picture) as InlineContentControl;
//Creates a new image instance and load image 
WPicture picture = new WPicture(document);
Stream imageStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Image.png");
//Adds image from stream
picture.LoadImage(imageStream);
//Adds picture to the picture content control
pictureContentControl.ParagraphItems.Add(picture);
//Creates memory stream
MemoryStream outputStream = new MemoryStream();
//Saves and closes the Word document instance
document.Save(outputStream, FormatType.Docx);
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", outputStream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
document.Close();
{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Content-Controls/Picture-content-control).

## Edit Content Control

You can edit the inline content control text by iterating the child items of inline content control. The following code example shows how to edit content control text in the Word document.

{% tabs %}
{% highlight c# %}
//Loads a template document
WordDocument document = new WordDocument(@"Template.docx");
///Processes the body contents for each section in the Word document
foreach (WSection section in document.Sections)
{
    //Accesses the Body of section where all the contents in document are apart
    WTextBody sectionBody = section.Body;
    IterateTextBody(sectionBody);
}
//Saves and closes the document instance
document.Save("Sample.docx");
document.Close();

private static void IterateTextBody(WTextBody textBody)
{
    //Iterates through each of the child items of WTextBody
    for (int i = 0; i < textBody.ChildEntities.Count; i++)
    {
        //IEntity is the basic unit in DocIO DOM. 
        //Accesses the body items (should be either paragraph, table or block content control) as IEntity
        IEntity bodyItemEntity = textBody.ChildEntities[i];
        //A Text body has 3 types of elements - Paragraph, Table and Block Content Control
        //Decides the element type by using EntityType
        switch (bodyItemEntity.EntityType)
        {
            case EntityType.Paragraph:
                WParagraph paragraph = bodyItemEntity as WParagraph;
                //Processes the paragraph contents
                //Iterates through the paragraph's DOM
                IterateParagraph(paragraph.Items);
                break;
            case EntityType.Table:
                //Table is a collection of rows and cells
                //Iterates through table's DOM
                IterateTable(bodyItemEntity as WTable);
                break;
            case EntityType.BlockContentControl:
                BlockContentControl blockContentControl = bodyItemEntity as BlockContentControl;
                //Iterates to the body items of Block Content Control.
                IterateTextBody(blockContentControl.TextBody);
                break;
        }
    }
}
private static void IterateTable(WTable table)
{
    //Iterates the row collection in a table
    foreach (WTableRow row in table.Rows)
    {
        //Iterates the cell collection in a table row
        foreach (WTableCell cell in row.Cells)
        {
            //Table cell is derived from (also a) TextBody
            //Reusing the code meant for iterating TextBody
            IterateTextBody(cell);
        }
    }
}
private static void IterateParagraph(ParagraphItemCollection paraItems)
{
    for (int i = 0; i < paraItems.Count; i++)
    {
        Entity entity = paraItems[i];
        //A paragraph can have child elements such as text, image, hyperlink, symbols, etc.,
        //Decides the element type by using EntityType
        switch (entity.EntityType)
        {            
            case EntityType.TextBox:
                //Iterates to the body items of textbox.
                WTextBox textBox = entity as WTextBox;
                IterateTextBody(textBox.TextBoxBody);
                break;
            case EntityType.Shape:
                //Iterates to the body items of shape.
                Shape shape = entity as Shape;
                IterateTextBody(shape.TextBody);
                break;
            case EntityType.InlineContentControl:
                InlineContentControl inlineContentControl = entity as InlineContentControl;
                if(inlineContentControl.ContentControlProperties.Title == "ReplaceText")
                    ReplaceTextWithInlineContentControl("Hello World", inlineContentControl);
                break;
        }
    }
}
private static void ReplaceTextWithInlineContentControl(string text, InlineContentControl inlineContentControl)
{
    WCharacterFormat characterFormat = null;
    foreach (ParagraphItem item in inlineContentControl.ParagraphItems)
    {
        if (item is WTextRange)
        {
            characterFormat = (item as WTextRange).CharacterFormat;
            break;
        }
    }
    //Remove exiting items and add new text range with required text
    inlineContentControl.ParagraphItems.Clear();
    WTextRange textRange = new WTextRange(inlineContentControl.Document);
    textRange.Text = text;
    if (characterFormat != null)
        textRange.ApplyCharacterFormat(characterFormat);
    inlineContentControl.ParagraphItems.Add(textRange);
}
{% endhighlight %}

{% highlight vb.net %}
'Loads a template document
Dim document As WordDocument = New WordDocument("Template.docx")
''' Processes the body contents for each section in the Word document
For Each section As WSection In document.Sections
    'Accesses the Body of section where all the contents in document are apart
    Dim sectionBody As WTextBody = section.Body
    IterateTextBody(sectionBody)
Next
'Saves and closes the document instance
document.Save("Sample.docx")
document.Close()
		
Private Shared Sub IterateTextBody(ByVal textBody As WTextBody)
	'Iterates through each of the child items of WTextBody
	For i As Integer = 0 To textBody.ChildEntities.Count - 1
		'IEntity is the basic unit in DocIO DOM. 
		'Accesses the body items (should be either paragraph, table or block content control) as IEntity
		Dim bodyItemEntity As IEntity = textBody.ChildEntities(i)
		'A Text body has 3 types of elements - Paragraph, Table and Block Content Control
		'Decides the element type by using EntityType
		Select Case bodyItemEntity.EntityType
			Case EntityType.Paragraph
				Dim paragraph As WParagraph = TryCast(bodyItemEntity, WParagraph)
				'Processes the paragraph contents
				'Iterates through the paragraph's DOM
				IterateParagraph(paragraph.Items)
			Case EntityType.Table
				'Table is a collection of rows and cells
				'Iterates through table's DOM
				SurroundingClass.IterateTable(TryCast(bodyItemEntity, WTable))
			Case EntityType.BlockContentControl
				Dim blockContentControl As BlockContentControl = TryCast(bodyItemEntity, BlockContentControl)
				'Iterates to the body items of Block Content Control.
				IterateTextBody(blockContentControl.TextBody)
		End Select
	Next
End Sub

Private Shared Sub IterateTable(ByVal table As WTable)
    'Iterates the row collection in a table
    For Each row As WTableRow In table.Rows
        'Iterates the cell collection in a table row
        For Each cell As WTableCell In row.Cells
            'Table cell is derived from (also a) TextBody
            'Reusing the code meant for iterating TextBody
            IterateTextBody(cell)
        Next
    Next
End Sub

Private Shared Sub IterateParagraph(ByVal paraItems As ParagraphItemCollection)
    For i As Integer = 0 To paraItems.Count - 1
        Dim entity As Entity = paraItems(i)
        'A paragraph can have child elements such as text, image, hyperlink, symbols, etc.,
        'Decides the element type by using EntityType
        Select Case entity.EntityType            
            Case EntityType.TextBox
                'Iterates to the body items of textbox.
                Dim textBox As WTextBox = TryCast(entity, WTextBox)
                IterateTextBody(textBox.TextBoxBody)
            Case EntityType.Shape
                'Iterates to the body items of shape.
                Dim shape As Shape = TryCast(entity, Shape)
                IterateTextBody(shape.TextBody)
            Case EntityType.InlineContentControl
                Dim inlineContentControl As InlineContentControl = TryCast(entity, InlineContentControl)
                If inlineContentControl.ContentControlProperties.Title = "ReplaceText" Then 
				    ReplaceTextWithInlineContentControl("Hello World", inlineContentControl)
        End Select
    Next
End Sub

Private Shared Sub ReplaceTextWithInlineContentControl(ByVal text As String, ByVal inlineContentControl As InlineContentControl)
    Dim characterFormat As WCharacterFormat = Nothing
        For Each item As ParagraphItem In inlineContentControl.ParagraphItems
            If TypeOf item Is WTextRange Then
                characterFormat = TryCast(item, WTextRange).CharacterFormat
            Exit For
        End If
    Next
	'Remove exiting items and add new text range with required text
    inlineContentControl.ParagraphItems.Clear()
    Dim textRange As WTextRange = New WTextRange(inlineContentControl.Document)
    textRange.Text = text
    If characterFormat IsNot Nothing Then textRange.ApplyCharacterFormat(characterFormat)
    inlineContentControl.ParagraphItems.Add(textRange)
End Sub
{% endhighlight %}

{% highlight UWP %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("Sample.Assets.Template.docx");
            
WordDocument document = new WordDocument(inputStream, FormatType.Docx);
inputStream.Dispose();
///Processes the body contents for each section in the Word document
foreach (WSection section in document.Sections)
{
    //Accesses the Body of section where all the contents in document are apart
    WTextBody sectionBody = section.Body;
    IterateTextBody(sectionBody);
}
MemoryStream stream = new MemoryStream();
//Saves the Word document to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word document file in local machine
Save(stream, "application/msword", "Sample.docx");
document.Close();
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp

private static void IterateTextBody(WTextBody textBody)
{
    //Iterates through each of the child items of WTextBody
    for (int i = 0; i < textBody.ChildEntities.Count; i++)
    {
        //IEntity is the basic unit in DocIO DOM. 
        //Accesses the body items (should be either paragraph, table or block content control) as IEntity
        IEntity bodyItemEntity = textBody.ChildEntities[i];
        //A Text body has 3 types of elements - Paragraph, Table and Block Content Control
        //Decides the element type by using EntityType
        switch (bodyItemEntity.EntityType)
        {
            case EntityType.Paragraph:
                WParagraph paragraph = bodyItemEntity as WParagraph;
                //Processes the paragraph contents
                //Iterates through the paragraph's DOM
                IterateParagraph(paragraph.Items);
                break;
            case EntityType.Table:
                //Table is a collection of rows and cells
                //Iterates through table's DOM
                IterateTable(bodyItemEntity as WTable);
                break;
            case EntityType.BlockContentControl:
                BlockContentControl blockContentControl = bodyItemEntity as BlockContentControl;
                //Iterates to the body items of Block Content Control.
                IterateTextBody(blockContentControl.TextBody);
                break;
        }
    }
}
private static void IterateTable(WTable table)
{
    //Iterates the row collection in a table
    foreach (WTableRow row in table.Rows)
    {
        //Iterates the cell collection in a table row
        foreach (WTableCell cell in row.Cells)
        {
            //Table cell is derived from (also a) TextBody
            //Reusing the code meant for iterating TextBody
            IterateTextBody(cell);
        }
    }
}
private static void IterateParagraph(ParagraphItemCollection paraItems)
{
    for (int i = 0; i < paraItems.Count; i++)
    {
        Entity entity = paraItems[i];
        //A paragraph can have child elements such as text, image, hyperlink, symbols, etc.,
        //Decides the element type by using EntityType
        switch (entity.EntityType)
        {            
            case EntityType.TextBox:
                //Iterates to the body items of textbox.
                WTextBox textBox = entity as WTextBox;
                IterateTextBody(textBox.TextBoxBody);
                break;
            case EntityType.Shape:
                //Iterates to the body items of shape.
                Shape shape = entity as Shape;
                IterateTextBody(shape.TextBody);
                break;
            case EntityType.InlineContentControl:
                InlineContentControl inlineContentControl = entity as InlineContentControl;
                if(inlineContentControl.ContentControlProperties.Title == "ReplaceText")
                    ReplaceTextWithInlineContentControl("Hello World", inlineContentControl);
                break;
        }
    }
}

private static void ReplaceTextWithInlineContentControl(string text, InlineContentControl inlineContentControl)
{
    WCharacterFormat characterFormat = null;
    foreach (ParagraphItem item in inlineContentControl.ParagraphItems)
    {
        if (item is WTextRange)
        {
            characterFormat = (item as WTextRange).CharacterFormat;
            break;
        }
    }
	//Remove exiting items and add new text range with required text
    inlineContentControl.ParagraphItems.Clear();
    WTextRange textRange = new WTextRange(inlineContentControl.Document);
    textRange.Text = text;
    if (characterFormat != null)
        textRange.ApplyCharacterFormat(characterFormat);
    inlineContentControl.ParagraphItems.Add(textRange);
}
{% endhighlight %}

{% highlight ASP.NET CORE %}
//Open the file as Stream
FileStream docStream = new FileStream("Template.docx", FileMode.Open, FileAccess.Read);
//Creates an instance of WordDocument class
WordDocument document = new WordDocument(docStream, FormatType.Automatic);
docStream.Dispose();
///Processes the body contents for each section in the Word document
foreach (WSection section in document.Sections)
{
    //Accesses the Body of section where all the contents in document are apart
    WTextBody sectionBody = section.Body;
    IterateTextBody(sectionBody);
}
			
//Creates memory stream
MemoryStream outputStream = new MemoryStream();
//Saves and closes the Word document instance
document.Save(outputStream, FormatType.Docx);
document.Close();
outputStream.Dispose();

private static void IterateTextBody(WTextBody textBody)
{
    //Iterates through each of the child items of WTextBody
    for (int i = 0; i < textBody.ChildEntities.Count; i++)
    {
        //IEntity is the basic unit in DocIO DOM. 
        //Accesses the body items (should be either paragraph, table or block content control) as IEntity
        IEntity bodyItemEntity = textBody.ChildEntities[i];
        //A Text body has 3 types of elements - Paragraph, Table and Block Content Control
        //Decides the element type by using EntityType
        switch (bodyItemEntity.EntityType)
        {
            case EntityType.Paragraph:
                WParagraph paragraph = bodyItemEntity as WParagraph;
                //Processes the paragraph contents
                //Iterates through the paragraph's DOM
                IterateParagraph(paragraph.Items);
                break;
            case EntityType.Table:
                //Table is a collection of rows and cells
                //Iterates through table's DOM
                IterateTable(bodyItemEntity as WTable);
                break;
            case EntityType.BlockContentControl:
                BlockContentControl blockContentControl = bodyItemEntity as BlockContentControl;
                //Iterates to the body items of Block Content Control.
                IterateTextBody(blockContentControl.TextBody);
                break;
        }
    }
}
private static void IterateTable(WTable table)
{
    //Iterates the row collection in a table
    foreach (WTableRow row in table.Rows)
    {
        //Iterates the cell collection in a table row
        foreach (WTableCell cell in row.Cells)
        {
            //Table cell is derived from (also a) TextBody
            //Reusing the code meant for iterating TextBody
            IterateTextBody(cell);
        }
    }
}
private static void IterateParagraph(ParagraphItemCollection paraItems)
{
    for (int i = 0; i < paraItems.Count; i++)
    {
        Entity entity = paraItems[i];
        //A paragraph can have child elements such as text, image, hyperlink, symbols, etc.,
        //Decides the element type by using EntityType
        switch (entity.EntityType)
        {
            case EntityType.TextBox:
                //Iterates to the body items of textbox.
                WTextBox textBox = entity as WTextBox;
                IterateTextBody(textBox.TextBoxBody);
                break;
            case EntityType.Shape:
                //Iterates to the body items of shape.
                Shape shape = entity as Shape;
                IterateTextBody(shape.TextBody);
                break;
            case EntityType.InlineContentControl:
                InlineContentControl inlineContentControl = entity as InlineContentControl;
                if(inlineContentControl.ContentControlProperties.Title == "ReplaceText")
                    ReplaceTextWithInlineContentControl("Hello World", inlineContentControl);
                break;
        }
    }
}

private static void ReplaceTextWithInlineContentControl(string text, InlineContentControl inlineContentControl)
{
    WCharacterFormat characterFormat = null;
    foreach (ParagraphItem item in inlineContentControl.ParagraphItems)
    {
        if (item is WTextRange)
        {
            characterFormat = (item as WTextRange).CharacterFormat;
            break;
        }
    }
	//Remove exiting items and add new text range with required text
    inlineContentControl.ParagraphItems.Clear();
    WTextRange textRange = new WTextRange(inlineContentControl.Document);
    textRange.Text = text;
    if (characterFormat != null)
        textRange.ApplyCharacterFormat(characterFormat);
    inlineContentControl.ParagraphItems.Add(textRange);
}

{% endhighlight %}

{% highlight XAMARIN %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream fileStream = assembly.GetManifestResourceStream("Sample.Assets.Template.docx");
WordDocument document = new WordDocument(fileStream, FormatType.Automatic);
fileStream.Dispose();
///Processes the body contents for each section in the Word document
foreach (WSection section in document.Sections)
{
    //Accesses the Body of section where all the contents in document are apart
    WTextBody sectionBody = section.Body;
    IterateTextBody(sectionBody);
}

//Creates memory stream
MemoryStream outputStream = new MemoryStream();
//Saves and closes the Word document instance
document.Save(outputStream, FormatType.Docx);
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", outputStream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
document.Close();

private static void IterateTextBody(WTextBody textBody)
{
    //Iterates through each of the child items of WTextBody
    for (int i = 0; i < textBody.ChildEntities.Count; i++)
    {
        //IEntity is the basic unit in DocIO DOM. 
        //Accesses the body items (should be either paragraph, table or block content control) as IEntity
        IEntity bodyItemEntity = textBody.ChildEntities[i];
        //A Text body has 3 types of elements - Paragraph, Table and Block Content Control
        //Decides the element type by using EntityType
        switch (bodyItemEntity.EntityType)
        {
            case EntityType.Paragraph:
                WParagraph paragraph = bodyItemEntity as WParagraph;
                //Processes the paragraph contents
                //Iterates through the paragraph's DOM
                IterateParagraph(paragraph.Items);
                break;
            case EntityType.Table:
                //Table is a collection of rows and cells
                //Iterates through table's DOM
                IterateTable(bodyItemEntity as WTable);
                break;
            case EntityType.BlockContentControl:
                BlockContentControl blockContentControl = bodyItemEntity as BlockContentControl;
                //Iterates to the body items of Block Content Control.
                IterateTextBody(blockContentControl.TextBody);
                break;
        }
    }
}
private static void IterateTable(WTable table)
{
    //Iterates the row collection in a table
    foreach (WTableRow row in table.Rows)
    {
        //Iterates the cell collection in a table row
        foreach (WTableCell cell in row.Cells)
        {
            //Table cell is derived from (also a) TextBody
            //Reusing the code meant for iterating TextBody
            IterateTextBody(cell);
        }
    }
}
private static void IterateParagraph(ParagraphItemCollection paraItems)
{
    for (int i = 0; i < paraItems.Count; i++)
    {
        Entity entity = paraItems[i];
        //A paragraph can have child elements such as text, image, hyperlink, symbols, etc.,
        //Decides the element type by using EntityType
        switch (entity.EntityType)
        {
            case EntityType.TextBox:
                //Iterates to the body items of textbox.
                WTextBox textBox = entity as WTextBox;
                IterateTextBody(textBox.TextBoxBody);
                break;
            case EntityType.Shape:
                //Iterates to the body items of shape.
                Shape shape = entity as Shape;
                IterateTextBody(shape.TextBody);
                break;
            case EntityType.InlineContentControl:
                InlineContentControl inlineContentControl = entity as InlineContentControl;
                if(inlineContentControl.ContentControlProperties.Title == "ReplaceText")
                    ReplaceTextWithInlineContentControl("Hello World", inlineContentControl);
                break;
        }
    }
}

private static void ReplaceTextWithInlineContentControl(string text, InlineContentControl inlineContentControl)
{
    WCharacterFormat characterFormat = null;
    foreach (ParagraphItem item in inlineContentControl.ParagraphItems)
    {
        if (item is WTextRange)
        {
            characterFormat = (item as WTextRange).CharacterFormat;
            break;
        }
    }
	//Remove exiting items and add new text range with required text
    inlineContentControl.ParagraphItems.Clear();
    WTextRange textRange = new WTextRange(inlineContentControl.Document);
    textRange.Text = text;
    if (characterFormat != null)
        textRange.ApplyCharacterFormat(characterFormat);
    inlineContentControl.ParagraphItems.Add(textRange);
}
{% endhighlight %}
{% endtabs %}  

N> In the above-mentioned code samples, for Xamarin platforms the document is saved as stream only. To save the stream to file kindly refer code sample [here](https://help.syncfusion.com/file-formats/docio/xamarin#save-the-document#).