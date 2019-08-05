---
title: Accepting or Rejecting Track Changes | DocIO | Syncfusion
description: This section illustrates how to Accept or Reject the Track changes of the Word document
platform: file-formats
control: DocIO
documentation: UG
---
# Accepting or Rejecting Track Changes

It is used to keep track of the changes made to a Word document. It helps to maintain the record of author, name and time for every insertion, deletion, or modification in a document. This can be enabled by using the TrackChanges property of the Word document.

N> 
With this support, the changes made in the Word document by DocIO library cannot be tracked.

The following code example illustrates how to enable track changes of the document.

{% tabs %}   

{% highlight c# %}
//Creates a new Word document 

WordDocument document = new WordDocument();

//Adds new section to the document

IWSection section = document.AddSection();

//Adds new paragraph to the section

IWParagraph paragraph = section.AddParagraph();

//Appends text to the paragraph

IWTextRange text = paragraph.AppendText("This sample illustrates how to track the changes made to the word document. ");

//Sets font name and size for text

text.CharacterFormat.FontName = "Times New Roman";

text.CharacterFormat.FontSize = 14;

text = paragraph.AppendText("This track changes is useful in shared environment.");

text.CharacterFormat.FontSize = 12;

//Turns on the track changes option

document.TrackChanges = true;

//Saves and closes the document

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

'Appends text to the paragraph

Dim text As IWTextRange = paragraph.AppendText("This sample illustrates how to track the changes made to the word document. ")

'Sets font name and size for text

text.CharacterFormat.FontName = "Times New Roman"

text.CharacterFormat.FontSize = 14

text = paragraph.AppendText("This track changes is useful in shared environment.")

text.CharacterFormat.FontSize = 12

'Turns on the track changes option

document.TrackChanges = True

'Saves and closes the document

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

//Appends text to the paragraph

IWTextRange text = paragraph.AppendText("This sample illustrates how to track the changes made to the word document. ");

//Sets font name and size for text

text.CharacterFormat.FontName = "Times New Roman";

text.CharacterFormat.FontSize = 14;

text = paragraph.AppendText("This track changes is useful in shared environment.");

text.CharacterFormat.FontSize = 12;

//Turns on the track changes option

document.TrackChanges = true;

//Saves the Word file to MemoryStream

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream, FormatType.Docx);

//Saves the stream as Word file in local machine

Save(stream, "Sample.docx");

document.Close();

// Saves the Word document

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

			// Write compressed data from memory to file

			using (Stream outstream = zipStream.AsStreamForWrite())

			{

				byte[] buffer = streams.ToArray();

				outstream.Write(buffer, 0, buffer.Length);

				outstream.Flush();

			}

		}

	}

	// Launch the saved Word file

	await Windows.System.Launcher.LaunchFileAsync(stFile);

}
{% endhighlight %}

{% highlight ASP.NET CORE %}
//Creates a new Word document 

WordDocument document = new WordDocument();

//Adds new section to the document

IWSection section = document.AddSection();

//Adds new paragraph to the section

IWParagraph paragraph = section.AddParagraph();

//Appends text to the paragraph

IWTextRange text = paragraph.AppendText("This sample illustrates how to track the changes made to the word document. ");

//Sets font name and size for text

text.CharacterFormat.FontName = "Times New Roman";

text.CharacterFormat.FontSize = 14;

text = paragraph.AppendText("This track changes is useful in shared environment.");

text.CharacterFormat.FontSize = 12;

//Turns on the track changes option

document.TrackChanges = true;

//Saves the Word document to  MemoryStream

MemoryStream stream = new MemoryStream();

document.Save(stream, FormatType.Docx);

stream.Position = 0;

//Download Word document in the browser

return File(stream, "application/msword", "Sample.docx");
{% endhighlight %}

{% highlight XAMARIN %}
//Creates a new Word document 

WordDocument document = new WordDocument();

//Adds new section to the document

IWSection section = document.AddSection();

//Adds new paragraph to the section

IWParagraph paragraph = section.AddParagraph();

//Appends text to the paragraph

IWTextRange text = paragraph.AppendText("This sample illustrates how to track the changes made to the word document. ");

//Sets font name and size for text

text.CharacterFormat.FontName = "Times New Roman";

text.CharacterFormat.FontSize = 14;

text = paragraph.AppendText("This track changes is useful in shared environment.");

text.CharacterFormat.FontSize = 12;

//Turns on the track changes option

document.TrackChanges = true;

MemoryStream stream = new MemoryStream();

//Saves the Word document to  MemoryStream

document.Save(stream, FormatType.Docx);

//Save the stream as a file in the device and invoke it for viewing

Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.docx", "application/msword", stream);
{% endhighlight %} 

{% endtabs %} 

The changes made to the document can be accepted or rejected. The following code example illustrates how to accept or reject the changes made to the document. 

{% tabs %}  

{% highlight c# %}
//Loads the template document

WordDocument document = new WordDocument("TrackChanges.docx", FormatType.Docx);

//Accepts track changes of the document

if (document.HasChanges)

document.AcceptChanges();

//Saves and closes the document

document.Save("TrackChanges_Sample.docx", FormatType.Docx);

document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Loads the template document

Dim document As New WordDocument("TrackChanges.docx", FormatType.Docx)

'Accepts track changes of the document

If document.HasChanges Then

document.AcceptChanges()

End If

'Saves and closes the document

document.Save("TrackChanges_Sample.docx", FormatType.Docx)

document.Close()
{% endhighlight %}

{% highlight UWP %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;

//Loads the template document

WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.TrackChanges.docx"), FormatType.Docx);

//Accepts track changes of the document

if (document.HasChanges)

document.AcceptChanges();

//Saves the Word file to MemoryStream

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream, FormatType.Docx);

//Saves the stream as Word file in local machine

Save(stream, "TrackChanges_Sample.docx");

document.Close();

// Saves the Word document

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

			// Write compressed data from memory to file

			using (Stream outstream = zipStream.AsStreamForWrite())

			{

				byte[] buffer = streams.ToArray();

				outstream.Write(buffer, 0, buffer.Length);

				outstream.Flush();

			}

		}

	}

	// Launch the saved Word file

	await Windows.System.Launcher.LaunchFileAsync(stFile);

}
{% endhighlight %}

{% highlight ASP.NET CORE %}
FileStream fileStreamPath = new FileStream(@"Data/TrackChanges.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);

//Loads the template document

WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);

//Accepts track changes of the document

if (document.HasChanges)

document.AcceptChanges();

//Saves the Word file to MemoryStream

MemoryStream stream = new MemoryStream();

document.Save(stream, FormatType.Docx);

stream.Position = 0;

//Download Word document in the browser

return File(stream, "application/msword", "TrackChanges_Sample.docx");
{% endhighlight %}

{% highlight XAMARIN %}
Assembly assembly = typeof(App).GetTypeInfo().Assembly;

//Loads the template document

WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Data.TrackChanges.docx"), FormatType.Docx);

//Accepts track changes of the document

if (document.HasChanges)

document.AcceptChanges();

MemoryStream stream = new MemoryStream();

//Saves the Word document to  MemoryStream

document.Save(stream, FormatType.Docx);

//Save the stream as a file in the device and invoke it for viewing

Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("TrackChanges_Sample.docx", "application/msword", stream);
{% endhighlight %}

{% endtabs %}  