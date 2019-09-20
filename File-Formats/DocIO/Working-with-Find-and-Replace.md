---
title: Working with Find and Replace | Syncfusion
description: This section illustrates finding a text and replacing it with a new text
platform: file-formats
control: DocIO
documentation: UG
---
# Find and Replace

You can search a particular text you like to change and replace it with another text or part of the document.

## Finding contents in a Word document

You can find the first occurrence of a particular text within a single paragraph in the document by using `Find` method and its next occurrence by using `FindNext` method. You can also find a particular text pattern in the document.

The following code example illustrates how to find a particular text and its next occurrence in the document.

{% tabs %}  

{% highlight c# %}
//Loads the template document
WordDocument document = new WordDocument("Template.docx", FormatType.Docx);
//Finds the first occurrence of a particular text in the document
TextSelection textSelection = document.Find("as graphical contents", false, true);
//Gets the found text as single text range
WTextRange textRange = textSelection.GetAsOneRange();
//Modifies the text
textRange.Text = "Replaced text";
//Sets highlight color
textRange.CharacterFormat.HighlightColor = Color.Yellow;
//Finds the next occurrence of a particular text from the previous paragraph
textSelection = document.FindNext(textRange.OwnerParagraph, "paragraph", true, false);
//Gets the found text as single text range
WTextRange range = textSelection.GetAsOneRange();
//Sets bold formatting
range.CharacterFormat.Bold = true;
//Saves and closes the document
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Loads the template document
Dim document As New WordDocument("Template.docx", FormatType.Docx)
'Find the first occurrence of a particular text in the document
Dim textSelection As TextSelection = document.Find("as graphical contents", False, True)
'Gets the found text as single text range
Dim textRange As WTextRange = textSelection.GetAsOneRange()
'Modifies the text
textRange.Text = "Replaced text"
'Sets highlight color
textRange.CharacterFormat.HighlightColor = Color.Yellow
'Finds the next occurrence of a particular text from the previous paragraph
textSelection = document.FindNext(textRange.OwnerParagraph, "paragraph", True, False)
'Gets the found text as single text range
Dim range As WTextRange = textSelection.GetAsOneRange()
'Sets bold formatting
range.CharacterFormat.Bold = True
'Saves and closes the document
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight UWP %}
//Loads the template document
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Docx);
//Finds the first occurrence of a particular text in the document
TextSelection textSelection = document.Find("as graphical contents", false, true);
//Gets the found text as single text range
WTextRange textRange = textSelection.GetAsOneRange();
//Modifies the text
textRange.Text = "Replaced text";
//Sets highlight color
textRange.CharacterFormat.HighlightColor = Color.Yellow;
//Finds the next occurrence of a particular text from the previous paragraph
textSelection = document.FindNext(textRange.OwnerParagraph, "paragraph", true, false);
//Gets the found text as single text range
WTextRange range = textSelection.GetAsOneRange();
//Sets bold formatting
range.CharacterFormat.Bold = true;
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word file in local machine
Save(stream, "Sample.docx"); 

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

{% highlight ASP.NET Core %}
//Loads the template document
FileStream fileStreamPath = new FileStream("Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);
//Finds the first occurrence of a particular text in the document
TextSelection textSelection = document.Find("as graphical contents", false, true);
//Gets the found text as single text range
WTextRange textRange = textSelection.GetAsOneRange();
//Modifies the text
textRange.Text = "Replaced text";
//Sets highlight color
textRange.CharacterFormat.HighlightColor = Color.Yellow;
//Finds the next occurrence of a particular text from the previous paragraph
textSelection = document.FindNext(textRange.OwnerParagraph, "paragraph", true, false);
//Gets the found text as single text range
WTextRange range = textSelection.GetAsOneRange();
//Sets bold formatting
range.CharacterFormat.Bold = true;
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Sample.docx");
{% endhighlight %}

{% highlight Xamarin %}
//Loads the template document
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("GettingStarted.Data.Template.docx"), FormatType.Docx);
//Finds the first occurrence of a particular text in the document
TextSelection textSelection = document.Find("as graphical contents", false, true);
//Gets the found text as single text range
WTextRange textRange = textSelection.GetAsOneRange();
//Modifies the text
textRange.Text = "Replaced text";
//Sets highlight color
textRange.CharacterFormat.HighlightColor = Color.Yellow;
//Finds the next occurrence of a particular text from the previous paragraph
textSelection = document.FindNext(textRange.OwnerParagraph, "paragraph", true, false);
//Gets the found text as single text range
WTextRange range = textSelection.GetAsOneRange();
//Sets bold formatting
range.CharacterFormat.Bold = true;
//Saves the Word document to  MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.docx", "application/msword", stream);
{% endhighlight %}

{% endtabs %}  

You can find all the occurrence of a particular text within a single paragraph in the document by using `FindAll` method. 

The following code example illustrates how to find all the occurrences of a particular text in the document.

{% tabs %} 

{% highlight c# %}
//Loads the template document
WordDocument document = new WordDocument("Template.docx", FormatType.Docx);
//Finds all the occurrences of a particular text
TextSelection[] textSelections = document.FindAll("paragraph", false, true);
foreach (TextSelection textSelection in textSelections)
{
    //Gets the found text as single text range and sets highlight color
    WTextRange textRange = textSelection.GetAsOneRange();
    textRange.CharacterFormat.HighlightColor = Color.YellowGreen;
}
//Saves and closes the document
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Loads the template document
Dim document As New WordDocument("Template.docx", FormatType.Docx)
'Finds all the occurrences of a particular text
Dim textSelections As TextSelection() = document.FindAll("paragraph", False, True)
For Each textSelection As TextSelection In textSelections
	'Gets the found text as single text range and sets highlight color
	Dim textRange As WTextRange = textSelection.GetAsOneRange()
	textRange.CharacterFormat.HighlightColor = Color.YellowGreen
Next
'Saves and closes the document
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight UWP %}
//Loads the template document
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Docx);
//Finds all the occurrences of a particular text
TextSelection[] textSelections = document.FindAll("paragraph", false, true);
foreach (TextSelection textSelection in textSelections)
{
    //Gets the found text as single text range and sets highlight color
    WTextRange textRange = textSelection.GetAsOneRange();
    textRange.CharacterFormat.HighlightColor = Color.YellowGreen;
}
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word file in local machine
Save(stream, "Sample.docx");

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

{% highlight ASP.NET Core %}
//Loads the template document
FileStream fileStreamPath = new FileStream("Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);
//Finds all the occurrences of a particular text
TextSelection[] textSelections = document.FindAll("paragraph", false, true);
foreach (TextSelection textSelection in textSelections)
{
    //Gets the found text as single text range and sets highlight color
    WTextRange textRange = textSelection.GetAsOneRange();
    textRange.CharacterFormat.HighlightColor = Color.YellowGreen;
}
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Sample.docx");
{% endhighlight %}

{% highlight Xamarin %}
//Loads the template document
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("GettingStarted.Data.Template.docx"), FormatType.Docx);
//Finds all the occurrences of a particular text
TextSelection[] textSelections = document.FindAll("paragraph", false, true);
foreach (TextSelection textSelection in textSelections)
{
    //Gets the found text as single text range and sets highlight color
    WTextRange textRange = textSelection.GetAsOneRange();
    textRange.CharacterFormat.HighlightColor = Color.YellowGreen;
}
//Saves the Word document to  MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.docx", "application/msword", stream);
{% endhighlight %} 

{% endtabs %}  

You can find the first occurrence of a particular text extended to several paragraphs in the document by using `FindSingleLine` method and its next occurrence by using `FindNextSingleLine` method.

The following code example illustrates how to find a particular text extended to several paragraphs in the Word document.

{% tabs %}   

{% highlight c# %}
//Loads the template document
WordDocument document = new WordDocument("Template.docx", FormatType.Docx);
//Finds the first occurrence of a particular text extended to several paragraphs in the document
TextSelection[] textSelections = document.FindSingleLine("First paragraph Second paragraph", true, false);
WParagraph paragraph = null;
foreach (TextSelection textSelection in textSelections)
{
    //Gets the found text as single text range and set highlight color
    WTextRange textRange = textSelection.GetAsOneRange();
    textRange.CharacterFormat.HighlightColor = Color.YellowGreen;
    paragraph = textRange.OwnerParagraph;
}
//Finds the next occurrence of a particular text extended to several paragraphs in the document
textSelections = document.FindNextSingleLine(paragraph, "First paragraph Second paragraph", true, false);
foreach (TextSelection textSelection in textSelections)
{
    //Gets the found text as single text range and sets italic formatting
    WTextRange text = textSelection.GetAsOneRange();
    text.CharacterFormat.Italic = true;
}
//Saves and closes the document
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Loads the template document
Dim document As New WordDocument("Template.docx", FormatType.Docx)
'Finds the first occurrence of a particular text extended to several paragraphs in the document
Dim textSelections As TextSelection() = document.FindSingleLine("First paragraph Second paragraph", True, False)
Dim paragraph As WParagraph = Nothing
For Each textSelection As TextSelection In textSelections
	'Gets the found text as single text range and sets highlight color
	Dim textRange As WTextRange = textSelection.GetAsOneRange()
	textRange.CharacterFormat.HighlightColor = Color.YellowGreen
	paragraph = textRange.OwnerParagraph
Next
'Finds the next occurrence of a particular text extended to several paragraphs in the document
textSelections = document.FindNextSingleLine(paragraph, "First paragraph Second paragraph", True, False)
For Each textSelection As TextSelection In textSelections
	'Gets the found text as single text range and sets italic formatting
	Dim text As WTextRange = textSelection.GetAsOneRange()
	text.CharacterFormat.Italic = True
Next
'Saves and closes the document
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight UWP %}
//Loads the template document
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Docx);
//Finds the first occurrence of a particular text extended to several paragraphs in the document
TextSelection[] textSelections = document.FindSingleLine("First paragraph Second paragraph", true, false);
WParagraph paragraph = null;
foreach (TextSelection textSelection in textSelections)
{
    //Gets the found text as single text range and set highlight color
    WTextRange textRange = textSelection.GetAsOneRange();
    textRange.CharacterFormat.HighlightColor = Color.YellowGreen;
    paragraph = textRange.OwnerParagraph;
}
//Finds the next occurrence of a particular text extended to several paragraphs in the document
textSelections = document.FindNextSingleLine(paragraph, "First paragraph Second paragraph", true, false);
foreach (TextSelection textSelection in textSelections)
{
    //Gets the found text as single text range and sets italic formatting
    WTextRange text = textSelection.GetAsOneRange();
    text.CharacterFormat.Italic = true;
}
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word file in local machine
Save(stream, "Sample.docx");

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

{% highlight ASP.NET Core %}
//Loads the template document
FileStream fileStreamPath = new FileStream("Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);
//Finds the first occurrence of a particular text extended to several paragraphs in the document
TextSelection[] textSelections = document.FindSingleLine("First paragraph Second paragraph", true, false);
WParagraph paragraph = null;
foreach (TextSelection textSelection in textSelections)
{
    //Gets the found text as single text range and set highlight color
    WTextRange textRange = textSelection.GetAsOneRange();
    textRange.CharacterFormat.HighlightColor = Color.YellowGreen;
    paragraph = textRange.OwnerParagraph;
}
//Finds the next occurrence of a particular text extended to several paragraphs in the document
textSelections = document.FindNextSingleLine(paragraph, "First paragraph Second paragraph", true, false);
foreach (TextSelection textSelection in textSelections)
{
    //Gets the found text as single text range and sets italic formatting
    WTextRange text = textSelection.GetAsOneRange();
    text.CharacterFormat.Italic = true;
}
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Sample.docx");
{% endhighlight %}

{% highlight Xamarin %}
//Loads the template document
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("GettingStarted.Data.Template.docx"), FormatType.Docx);
//Finds the first occurrence of a particular text extended to several paragraphs in the document
TextSelection[] textSelections = document.FindSingleLine("First paragraph Second paragraph", true, false);
WParagraph paragraph = null;
foreach (TextSelection textSelection in textSelections)
{
    //Gets the found text as single text range and set highlight color
    WTextRange textRange = textSelection.GetAsOneRange();
    textRange.CharacterFormat.HighlightColor = Color.YellowGreen;
    paragraph = textRange.OwnerParagraph;
}
//Finds the next occurrence of a particular text extended to several paragraphs in the document
textSelections = document.FindNextSingleLine(paragraph, "First paragraph Second paragraph", true, false);
foreach (TextSelection textSelection in textSelections)
{
    //Gets the found text as single text range and sets italic formatting
    WTextRange text = textSelection.GetAsOneRange();
    text.CharacterFormat.Italic = true;
}
//Saves the Word document to  MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
{% endhighlight %}

{% endtabs %} 

## Replacing the Search results

You can replace a particular text with another text, part of a document or entire document by using `Replace` method. 

The following code example illustrates how to replace a particular text.

{% tabs %}  

{% highlight c# %}
//Loads a template document
WordDocument document = new WordDocument("Template.docx", FormatType.Docx);
//Finds the first occurrence of a particular text in the document
TextSelection selection = document.Find("contents", false, false);
//Initializes text body part
TextBodyPart bodyPart = new TextBodyPart(selection);
//Replaces a particular text with the text body part
document.Replace("paragraph", bodyPart, false, true, true);
//Saves and closes the document
document.Save("Replace.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Loads a template document
Dim document As New WordDocument("Template.docx", FormatType.Docx)
'Finds the first occurrence of a particular text in the document
Dim selection As TextSelection = document.Find("contents", False, False)
'Initializes text body part
Dim bodyPart As New TextBodyPart(selection)
'Replaces a particular text with the text body part
document.Replace("paragraph", bodyPart, False, True, True)
'Saves and closes the document
document.Save("Replace.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight UWP %}
//Loads a template document
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Docx);
//Finds the first occurrence of a particular text in the document
TextSelection selection = document.Find("contents", false, false);
//Initializes text body part
TextBodyPart bodyPart = new TextBodyPart(selection);
//Replaces a particular text with the text body part
document.Replace("paragraph", bodyPart, false, true, true);
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word file in local machine
Save(stream, "Replace.docx"); 

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

{% highlight ASP.NET Core %}
//Loads a template document
FileStream fileStreamPath = new FileStream("Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);
//Finds the first occurrence of a particular text in the document
TextSelection selection = document.Find("contents", false, false);
//Initializes text body part
TextBodyPart bodyPart = new TextBodyPart(selection);
//Replaces a particular text with the text body part
document.Replace("paragraph", bodyPart, false, true, true);
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Replace.docx");
{% endhighlight %}

{% highlight Xamarin %}
//Loads a template document
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("GettingStarted.Data.Template.docx"), FormatType.Docx);
//Finds the first occurrence of a particular text in the document
TextSelection selection = document.Find("contents", false, false);
//Initializes text body part
TextBodyPart bodyPart = new TextBodyPart(selection);
//Replaces a particular text with the text body part
document.Replace("paragraph", bodyPart, false, true, true);
//Saves the Word document to  MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Replace.docx", "application/msword", stream);
{% endhighlight %}

{% endtabs %}  

You can specify to replace only the first occurrence of the specified text by setting `ReplaceFirst` property of `WordDocument` class to true. 

The following code example illustrates how to replace the first occurrence of a particular text.

{% tabs %}  

{% highlight c# %}
//Loads a template document
WordDocument document = new WordDocument("Template.docx", FormatType.Docx);
//Sets to replace only the first occurrence of a particular text
document.ReplaceFirst = true;
//Finds the first occurrence of a particular text in the document
TextSelection selection = document.Find("contents", false, false);
//Initializes text body part
TextBodyPart bodyPart = new TextBodyPart(selection);
//Replaces a particular text with the text body part
document.Replace("paragraph", bodyPart, false, true, true);
//Saves and closes the document
document.Save("Replace.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Loads a template document
Dim document As New WordDocument("Template.docx", FormatType.Docx)
'Sets to replace only the first occurrence of a particular text
document.ReplaceFirst = True
'Finds the first occurrence of a particular text in the document
Dim selection As TextSelection = document.Find("contents", False, False)
'Initializes text body part
Dim bodyPart As New TextBodyPart(selection)
'Replaces a particular text with the text body part
document.Replace("paragraph", bodyPart, False, True, True)
'Saves and closes the document
document.Save("Replace.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight UWP %}
//Loads a template document
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Docx);
//Sets to replace only the first occurrence of a particular text
document.ReplaceFirst = true;
//Finds the first occurrence of a particular text in the document
TextSelection selection = document.Find("contents", false, false);
//Initializes text body part
TextBodyPart bodyPart = new TextBodyPart(selection);
//Replaces a particular text with the text body part
document.Replace("paragraph", bodyPart, false, true, true);
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word file in local machine
Save(stream, "Replace.docx"); 

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

{% highlight ASP.NET Core %}
//Loads a template document
FileStream fileStreamPath = new FileStream("Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);
//Sets to replace only the first occurrence of a particular text
document.ReplaceFirst = true;
//Finds the first occurrence of a particular text in the document
TextSelection selection = document.Find("contents", false, false);
//Initializes text body part
TextBodyPart bodyPart = new TextBodyPart(selection);
//Replaces a particular text with the text body part
document.Replace("paragraph", bodyPart, false, true, true);
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Replace.docx");
{% endhighlight %}

{% highlight Xamarin %}
//Loads a template document
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("GettingStarted.Data.Template.docx"), FormatType.Docx);
//Sets to replace only the first occurrence of a particular text
document.ReplaceFirst = true;
//Finds the first occurrence of a particular text in the document
TextSelection selection = document.Find("contents", false, false);
//Initializes text body part
TextBodyPart bodyPart = new TextBodyPart(selection);
//Replaces a particular text with the text body part
document.Replace("paragraph", bodyPart, false, true, true);
//Saves the Word document to  MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Replace.docx", "application/msword", stream);
{% endhighlight %} 

{% endtabs %}  

The following code example illustrates how to replace a particular text with a Word document.

{% tabs %}  

{% highlight c# %}
//Loads a template document
WordDocument document = new WordDocument("SourceTemplate.docx", FormatType.Docx);
//Gets the document to replace the text
IWordDocument replaceDocument = new WordDocument("Template.docx");
//Replaces a particular text with another document
document.Replace("paragraph", replaceDocument, false, true, true);
//Saves and closes the document
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Loads a template document
Dim document As New WordDocument("SourceTemplate.docx", FormatType.Docx)
'Gets the document to replace the text
Dim replaceDocument As IWordDocument = New WordDocument("Template.docx")
'Replaces a particular text with another document
document.Replace("paragraph", replaceDocument, False, True, True)
'Saves and closes the document
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight UWP %}
//Loads a template document
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.SourceTemplate.docx"), FormatType.Docx);
//Gets the document to replace the text
IWordDocument replaceDocument = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Docx);
//Replaces a particular text with another document
document.Replace("paragraph", replaceDocument, false, true, true);
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word file in local machine
Save(stream, "Sample.docx");

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

{% highlight ASP.NET Core %}
//Loads a template document
FileStream fileStreamPath1 = new FileStream("SourceTemplate.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
WordDocument document = new WordDocument(fileStreamPath1, FormatType.Docx);
//Gets the document to replace the text
FileStream fileStreamPath2 = new FileStream("Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
IWordDocument replaceDocument = new WordDocument(fileStreamPath2, FormatType.Docx);
//Replaces a particular text with another document
document.Replace("paragraph", replaceDocument, false, true, true);
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Sample.docx");
{% endhighlight %}

{% highlight Xamarin %}
//Loads a template document
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("GettingStarted.Data.SourceTemplate.docx"), FormatType.Docx);
//Gets the document to replace the text
IWordDocument replaceDocument = new WordDocument(assembly.GetManifestResourceStream("GettingStarted.Data.Template.docx"), FormatType.Docx);
//Replaces a particular text with another document
document.Replace("paragraph", replaceDocument, false, true, true);
//Saves the Word document to  MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.docx", "application/msword", stream);
{% endhighlight %} 

{% endtabs %}  

You can replace a particular text extended to several paragraphs in a document with another text or part of a document by using `ReplaceSingleLine` method.

The following code example illustrates how to replace the text extended to several paragraphs with simple text.

{% tabs %} 

{% highlight c# %}
//Loads a template document
WordDocument document = new WordDocument("Template.docx", FormatType.Docx);
//Replaces the text extended to two paragraphs with simple text
document.ReplaceSingleLine("First paragraph Second paragraph", "Replaced paragraph", true, false);
//Saves and closes the document
document.Save("Replace.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Loads a template document
Dim document As New WordDocument("Template.docx", FormatType.Docx)
'Replaces the text extended to two paragraphs with simple text
document.ReplaceSingleLine("First paragraph Second paragraph", "Replaced paragraph", True, False)
'Saves and closes the document
document.Save("Replace.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight UWP %}
//Loads a template document
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Docx);
//Replaces the text extended to two paragraphs with simple text
document.ReplaceSingleLine("First paragraph Second paragraph", "Replaced paragraph", true, false);
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word file in local machine
Save(stream, "Replace.docx");

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

{% highlight ASP.NET Core %}
//Loads a template document
FileStream fileStreamPath = new FileStream("Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);
//Replaces the text extended to two paragraphs with simple text
document.ReplaceSingleLine("First paragraph Second paragraph", "Replaced paragraph", true, false);
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Replace.docx");
{% endhighlight %}

{% highlight Xamarin %}
//Loads a template document
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("GettingStarted.Data.Template.docx"), FormatType.Docx);
//Replaces the text extended to two paragraphs with simple text
document.ReplaceSingleLine("First paragraph Second paragraph", "Replaced paragraph", true, false);
//Saves the Word document to  MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Replace.docx", "application/msword", stream);
{% endhighlight %}

{% endtabs %}