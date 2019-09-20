---
title: Working with Comments | DocIO | Syncfusion
description: This section illustrates how to add, modify and remove the comments
platform: file-formats
control: DocIO
documentation: UG
---
# Working with Comments

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

//Saves the Word document
async void Save(MemoryStream streams, string filename)
{
	streams.Position = 0;
	StorageFile stFile;
	if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
	{
		FileSavePicker savePicker = new FileSavePicker();
		savePicker.DefaultFileExtension = ".docx";
		savePicker.SuggestedFileName = filename;
		savePicker.FileTypeChoices.Add("Word Documents", new List<string>() { ".docx" });
		stFile = await savePicker.PickSaveFileAsync();
	}
	else
	{
		StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
		stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
	}
	if (stFile != null)
	{
		using (IRandomAccessStream zipStream = await stFile.OpenAsync(FileAccessMode.ReadWrite))
		{
			//Write compressed data from memory to file
			using (Stream outstream = zipStream.AsStreamForWrite())
			{
				byte[] buffer = streams.ToArray();
				outstream.Write(buffer, 0, buffer.Length);
				outstream.Flush();
			}
		}
	}
	//Launch the saved Word file
	await Windows.System.Launcher.LaunchFileAsync(stFile);
}
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
//Saves the Word document to  MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
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
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
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

//Saves the Word document
async void Save(MemoryStream streams, string filename)
{
	streams.Position = 0;
	StorageFile stFile;
	if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
	{
		FileSavePicker savePicker = new FileSavePicker();
		savePicker.DefaultFileExtension = ".docx";
		savePicker.SuggestedFileName = filename;
		savePicker.FileTypeChoices.Add("Word Documents", new List<string>() { ".docx" });
		stFile = await savePicker.PickSaveFileAsync();
	}
	else
	{
		StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
		stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
	}
	if (stFile != null)
	{
		using (IRandomAccessStream zipStream = await stFile.OpenAsync(FileAccessMode.ReadWrite))
		{
			//Write compressed data from memory to file
			using (Stream outstream = zipStream.AsStreamForWrite())
			{
				byte[] buffer = streams.ToArray();
				outstream.Write(buffer, 0, buffer.Length);
				outstream.Flush();
			}
		}
	}
	//Launch the saved Word file
	await Windows.System.Launcher.LaunchFileAsync(stFile);
}
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
//Saves the Word document to  MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
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
//Saves the Word document to  MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("ModifiedComment.docx", "application/msword", stream);
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

//Saves the Word document
async void Save(MemoryStream streams, string filename)
{
	streams.Position = 0;
	StorageFile stFile;
	if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
	{
		FileSavePicker savePicker = new FileSavePicker();
		savePicker.DefaultFileExtension = ".docx";
		savePicker.SuggestedFileName = filename;
		savePicker.FileTypeChoices.Add("Word Documents", new List<string>() { ".docx" });
		stFile = await savePicker.PickSaveFileAsync();
	}
	else
	{
		StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
		stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
	}
	if (stFile != null)
	{
		using (IRandomAccessStream zipStream = await stFile.OpenAsync(FileAccessMode.ReadWrite))
		{
			//Write compressed data from memory to file
			using (Stream outstream = zipStream.AsStreamForWrite())
			{
				byte[] buffer = streams.ToArray();
				outstream.Write(buffer, 0, buffer.Length);
				outstream.Flush();
			}
		}
	}
	//Launch the saved Word file
	await Windows.System.Launcher.LaunchFileAsync(stFile);
}
{% endhighlight %}

{% highlight ASP.NET CORE %}
FileStream fileStreamPath = new FileStream("Comment.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);
//Removes all the comments in a Word document
document.Comments.Clear();
//Saves the Word document to  MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %}

{% highlight XAMARIN %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("GettingStarted.Data.Comment.docx"), FormatType.Docx)
//Removes all the comments in a Word document
document.Comments.Clear();
//Saves the Word document to  MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
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

//Saves the Word document
async void Save(MemoryStream streams, string filename)
{
	streams.Position = 0;
	StorageFile stFile;
	if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
	{
		FileSavePicker savePicker = new FileSavePicker();
		savePicker.DefaultFileExtension = ".docx";
		savePicker.SuggestedFileName = filename;
		savePicker.FileTypeChoices.Add("Word Documents", new List<string>() { ".docx" });
		stFile = await savePicker.PickSaveFileAsync();
	}
	else
	{
		StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
		stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
	}
	if (stFile != null)
	{
		using (IRandomAccessStream zipStream = await stFile.OpenAsync(FileAccessMode.ReadWrite))
		{
			//Write compressed data from memory to file
			using (Stream outstream = zipStream.AsStreamForWrite())
			{
				byte[] buffer = streams.ToArray();
				outstream.Write(buffer, 0, buffer.Length);
				outstream.Flush();
			}
		}
	}
	//Launch the saved Word file
	await Windows.System.Launcher.LaunchFileAsync(stFile);
}
{% endhighlight %}

{% highlight ASP.NET CORE %}
FileStream fileStreamPath = new FileStream("Comment.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);
//Removes second comments from a document.
document.Comments.RemoveAt(1);
//Saves the Word document to  MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %}

{% highlight XAMARIN %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("GettingStarted.Data.Comment.docx"), FormatType.Docx)
//Removes second comments from a document.
document.Comments.RemoveAt(1);
//Saves the Word document to  MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
{% endhighlight %}

{% endtabs %}