---
title: Working with Comments | DocIO | Syncfusion
description: This section illustrates about working with comments in the Word document without MS Word or Office interop
platform: file-formats
control: DocIO
documentation: UG
---
# Working with Comments in Word Library

A comment is a note or annotation that an author or reviewer can add to a document. DocIO represents comment with `WComment` instance.

N>  The comment start and end ranges and dates can be preserved only on processing an existing document that already contains these information for each comment.

## Adding a Comment

You can add a new comment to the Word document by using `AppendComment` method of `WParagraph` class. 

The following code illustrates how to add a new comment to the document:

{% tabs %}  

{% highlight c# %}
//Creates a new Word document
WordDocument document = new WordDocument();
//Adds a section and a paragraph in the document
document.EnsureMinimal();
IWParagraph paragraph = document.LastParagraph;
//Appends text to the paragraph
paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");
//Adds comment to a paragraph
WComment comment = paragraph.AppendComment("comment test");
//Specifies the author of the comment
comment.Format.User = "Peter";
//Specifies the initial of the author
comment.Format.UserInitials = "St";
//Set the date and time for comment
comment.Format.DateTime = DateTime.Now;
//Saves and closes the Word document
document.Save("Comment.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Creates a new Word document
Dim document As New WordDocument()
'Adds a section and a paragraph in the document
document.EnsureMinimal()
Dim paragraph As IWParagraph = document.LastParagraph
'Appends text to the paragraph
paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.")
'Adds comment to a paragraph
Dim comment As WComment = paragraph.AppendComment("comment test")
'Specifies the author of the comment
comment.Format.User = "Peter"
'Specifies the initial of the author
comment.Format.UserInitials = "St"
'Saves and closes the Word document
document.Save("Comment.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight UWP %}
//Creates a new Word document
WordDocument document = new WordDocument();
//Adds a section and a paragraph in the document
document.EnsureMinimal();
IWParagraph paragraph = document.LastParagraph;
//Appends text to the paragraph
paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");
//Adds comment to a paragraph
WComment comment = paragraph.AppendComment("comment test");
//Specifies the author of the comment
comment.Format.User = "Peter";
//Specifies the initial of the author
comment.Format.UserInitials = "St";
//Set the date and time for comment
comment.Format.DateTime = DateTime.Now;
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word file in local machine
Save(stream, "Comment.docx");
//Closes the document
document.Close();
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight ASP.NET CORE %}
//Creates a new Word document
WordDocument document = new WordDocument();
//Adds a section and a paragraph in the document
document.EnsureMinimal();
IWParagraph paragraph = document.LastParagraph;
//Appends text to the paragraph
paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");
//Adds comment to a paragraph
WComment comment = paragraph.AppendComment("comment test");
//Specifies the author of the comment
comment.Format.User = "Peter";
//Specifies the initial of the author
comment.Format.UserInitials = "St";
//Set the date and time for comment
comment.Format.DateTime = DateTime.Now;
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Comment.docx");
{% endhighlight %}

{% highlight XAMARIN %}
//Creates a new Word document
WordDocument document = new WordDocument();
//Adds a section and a paragraph in the document
document.EnsureMinimal();
IWParagraph paragraph = document.LastParagraph;
//Appends text to the paragraph
paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");
//Adds comment to a paragraph
WComment comment = paragraph.AppendComment("comment test");
//Specifies the author of the comment
comment.Format.User = "Peter";
//Specifies the initial of the author
comment.Format.UserInitials = "St";
//Set the date and time for comment
comment.Format.DateTime = DateTime.Now;
//Saves the Word document to  MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %} 

{% endtabs %}  

## Modifying a Comment

The following code illustrates how to modify the text of an existing comment in the Word document:

{% tabs %}  

{% highlight c# %}
WordDocument document = new WordDocument("Comment.docx");
//Iterates the comments in the Word document
foreach (WComment comment in document.Comments)
{
    //Modifies the last paragraph text of an existing comment when it is added by "Peter"
    if (comment.Format.User == "Peter")
        comment.TextBody.LastParagraph.Text = "Modified Comment Content";
}
document.Save("ModifiedComment.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net %}
Dim document As New WordDocument("Comment.docx")
'Iterates the comments in the Word document
For Each comment As WComment In document.Comments
	'Modifies the last paragraph text of an existing comment when it is added by "Peter"
	If comment.Format.User = "Peter" Then
		comment.TextBody.LastParagraph.Text = "Modified Comment Content"
	End If
Next
document.Save("ModifiedComment.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight UWP %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Comment.docx"), FormatType.Docx);
//Iterates the comments in the Word document
foreach (WComment comment in document.Comments)
{
    //Modifies the last paragraph text of an existing comment when it is added by "Peter"
    if (comment.Format.User == "Peter")
        comment.TextBody.LastParagraph.Text = "Modified Comment Content";
}
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word file in local machine
Save(stream, "ModifiedComment.docx");
//Closes the document
document.Close();
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight ASP.NET CORE %}
FileStream fileStreamPath = new FileStream("Comment.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);
//Iterates the comments in the Word document
foreach (WComment comment in document.Comments)
{
    //Modifies the last paragraph text of an existing comment when it is added by "Peter"
    if (comment.Format.User == "Peter")
        comment.TextBody.LastParagraph.Text = "Modified Comment Content";
}
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "ModifiedComment.docx");
{% endhighlight %}

{% highlight XAMARIN %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("GettingStarted.Data.Comment.docx"), FormatType.Docx);
//Iterates the comments in the Word document
foreach (WComment comment in document.Comments)
{
    //Modifies the last paragraph text of an existing comment when it is added by "Peter"
    if (comment.Format.User == "Peter")
        comment.TextBody.LastParagraph.Text = "Modified Comment Content";
}
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("ModifiedComment.docx", "application/msword", stream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}  
  
## Removing Comments

You can either remove all the comments or a particular comment from the Word document.

The following code illustrates how to remove all the comments in Word document.

{% tabs %}  

{% highlight c# %}
WordDocument document = new WordDocument("Comment.docx");
//Removes all the comments in a Word document
document.Comments.Clear();
document.Save("Result.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net %}
Dim document As New WordDocument("Comment.docx")
'Removes all the comments in a Word document
document.Comments.Clear()
document.Save("Result.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight UWP %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Comment.docx"), FormatType.Docx);
//Removes all the comments in a Word document
document.Comments.Clear();
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Closes the document
document.Close();
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight ASP.NET CORE %}
FileStream fileStreamPath = new FileStream("Comment.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);
//Removes all the comments in a Word document
document.Comments.Clear();
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %}

{% highlight XAMARIN %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("GettingStarted.Data.Comment.docx"), FormatType.Docx)
//Removes all the comments in a Word document
document.Comments.Clear();
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}  

The following code illustrates how to remove a particular comment from Word document.

{% tabs %} 

{% highlight c# %}
WordDocument document = new WordDocument("Comment.docx");
//Removes second comments from a document.
document.Comments.RemoveAt(1);
//Saves and closes the Word document
document.Save("Result.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net %}
Dim document As New WordDocument("Comment.docx")
'Removes second comments from a document.
document.Comments.RemoveAt(1)
'Saves and closes the Word document
document.Save("Result.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight UWP %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Comment.docx"), FormatType.Docx);
//Removes second comments from a document.
document.Comments.RemoveAt(1);
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Closes the document
document.Close();
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight ASP.NET CORE %}
FileStream fileStreamPath = new FileStream("Comment.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);
//Removes second comments from a document.
document.Comments.RemoveAt(1);
//Saves the Word document to  MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %}

{% highlight XAMARIN %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("GettingStarted.Data.Comment.docx"), FormatType.Docx)
//Removes second comments from a document
document.Comments.RemoveAt(1);
//Saves the Word document to  MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}

## Accessing parent comment

You can access the parent comment of a particular comment (reply) in a Word document using `Ancestor` API. The ancestor for parent comment returns `null` as default.

The following code examples show how to access the parent comment of a particular comment in a Word document.

{% tabs %}  

{% highlight c# %}
//Load an existing Word document into DocIO instance.
WordDocument document = new WordDocument("Comment.docx");
//Get the Ancestor comment.
WComment ancestorComment = document.Comments[1].Ancestor;
//Save and Close the Word document.
document.Save("Result.docx", FormatType.Docx);
document.Close();

{% endhighlight %}

{% highlight vb.net %}
'Load an existing Word document into DocIO instance.
Dim document As WordDocument = New WordDocument("Comment.docx")
'Get the Ancestor comment.
Dim ancestorComment As WComment = document.Comments[1].Ancestor
'Save and Close the Word document.
document.Save("Result.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight UWP %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets. Comment.docx"), FormatType.Docx);
//Get the Ancestor comment.
document.Comments[1].Ancestor;
//Save the Word file to MemoryStream.
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
//Save the stream as Word file in local machine.
Save(stream, "Result.docx");
//Close the document.
document.Close();
//Please refer to the following link to save a Word document in the UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight ASP.NET CORE %}
FileStream fileStreamPath = new FileStream("Comment.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);
// Get the Ancestor comment.
document.Comments[1].Ancestor;
//Save the Word document to  MemoryStream.
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Close the document.
document.Close();
stream.Position = 0;
//Download the Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %}

{% highlight XAMARIN %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Comment.docx"), FormatType.Docx)
//Get the Ancestor comment.
document.Comments[1].Ancestor;
//Save the Word document to  MemoryStream.
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Close the document.
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Please download the helper files from the following link to save the stream as a file and open the file for viewing in the Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}