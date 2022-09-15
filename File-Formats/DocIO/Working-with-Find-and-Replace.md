---
title: Working with Find and Replace | Syncfusion
description: This section illustrates how to find a particular text and replace it with another text or part of the document
platform: file-formats
control: DocIO
documentation: UG
---
# Working with Find and Replace

You can search a particular text you like to change and replace it with another text or part of the document.

## Finding contents in a Word document

You can find the first occurrence of a particular text within a single paragraph in the document by using `Find` method and its next occurrence by using `FindNext` method. You can also find a particular text pattern in the document.

The following code example illustrates how to find a particular text and its next occurrence in the document.

{% tabs %}  

{% highlight c# tabtitle="C#" %}
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

{% highlight vb.net tabtitle="VB.NET" %}
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

{% highlight c# tabtitle="UWP" %}
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
//Closes the document
document.Close();
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
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
//Closes the document
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Sample.docx");
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
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
//Closes the document
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.docx", "application/msword", stream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Find-and-Replace/Find-and-find-next).

You can find all the occurrence of a particular text within a single paragraph in the document by using `FindAll` method. 

The following code example illustrates how to find all the occurrences of a particular text in the document.

{% tabs %} 

{% highlight c# tabtitle="C#" %}
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

{% highlight vb.net tabtitle="VB.NET" %}
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

{% highlight c# tabtitle="UWP" %}
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
//Closes the document
document.Close();
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
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
//Closes the document
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Sample.docx");
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
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
//Closes the document
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.docx", "application/msword", stream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %} 

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Find-and-Replace/Find-and-highlight-all).

You can find the first occurrence of a particular text extended to several paragraphs in the document by using `FindSingleLine` method and its next occurrence by using `FindNextSingleLine` method.

The following code example illustrates how to find a particular text extended to several paragraphs in the Word document.

{% tabs %}   

{% highlight c# tabtitle="C#" %}
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

{% highlight vb.net tabtitle="VB.NET" %}
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

{% highlight c# tabtitle="UWP" %}
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
//Closes the document
document.Close();
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
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
//Closes the document
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Sample.docx");
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
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
//Closes the document
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %} 

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Find-and-Replace/Find-and-find-next-paragraphs).

## Replacing the Search results

You can replace a particular text with another text, part of a document or entire document by using `Replace` method. 

The following code example illustrates how to replace a particular text.

{% tabs %}  

{% highlight c# tabtitle="C#" %}
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

{% highlight vb.net tabtitle="VB.NET" %}
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

{% highlight c# tabtitle="UWP" %}
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
//Closes the document
document.Close();
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
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
//Closes the document
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Replace.docx");
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
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
//Closes the document
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Replace.docx", "application/msword", stream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Find-and-Replace/Replace-text-with-body-part).

You can specify to replace only the first occurrence of the specified text by setting `ReplaceFirst` property of `WordDocument` class to true. 

The following code example illustrates how to replace the first occurrence of a particular text.

{% tabs %}  

{% highlight c# tabtitle="C#" %}
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

{% highlight vb.net tabtitle="VB.NET" %}
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

{% highlight c# tabtitle="UWP" %}
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
//Closes the document
document.Close();
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
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
//Closes the document
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Replace.docx");
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
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
//Closes the document
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Replace.docx", "application/msword", stream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %} 

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Find-and-Replace/Find-and-replace-first-occurrence).

The following code example illustrates how to replace a particular text with a Word document.

{% tabs %}  

{% highlight c# tabtitle="C#" %}
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

{% highlight vb.net tabtitle="VB.NET" %}
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

{% highlight c# tabtitle="UWP" %}
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
//Closes the document
document.Close();
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
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
//Closes the document
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Sample.docx");
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
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
//Closes the document
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.docx", "application/msword", stream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %} 

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Find-and-Replace/Replace-text-with-Word-document).

You can replace a particular text extended to several paragraphs in a document with another text or part of a document by using `ReplaceSingleLine` method.

The following code example illustrates how to replace the text extended to several paragraphs with simple text.

{% tabs %} 

{% highlight c# tabtitle="C#" %}
//Loads a template document
WordDocument document = new WordDocument("Template.docx", FormatType.Docx);
//Replaces the text extended to two paragraphs with simple text
document.ReplaceSingleLine("First paragraph Second paragraph", "Replaced paragraph", true, false);
//Saves and closes the document
document.Save("Replace.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Loads a template document
Dim document As New WordDocument("Template.docx", FormatType.Docx)
'Replaces the text extended to two paragraphs with simple text
document.ReplaceSingleLine("First paragraph Second paragraph", "Replaced paragraph", True, False)
'Saves and closes the document
document.Save("Replace.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
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
//Closes the document
document.Close();
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Loads a template document
FileStream fileStreamPath = new FileStream("Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);
//Replaces the text extended to two paragraphs with simple text
document.ReplaceSingleLine("First paragraph Second paragraph", "Replaced paragraph", true, false);
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Replace.docx");
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Loads a template document
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("GettingStarted.Data.Template.docx"), FormatType.Docx);
//Replaces the text extended to two paragraphs with simple text
document.ReplaceSingleLine("First paragraph Second paragraph", "Replaced paragraph", true, false);
//Saves the Word document to  MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Replace.docx", "application/msword", stream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Find-and-Replace/Find-and-replace-paragraphs-with-text).

## Find and replace text with other text

You can find text in a Word document and replace it with other text. Unlike the `Find` method, the Replace method replaces all occurrences of the text. You can customize it to replace only the first occurrence of a text by setting the `ReplaceFirst` property of the WordDocument class to true.

The following code example illustrates how to replace all occurrences of a misspelled word with the correctly spelled word.

{% tabs %}  

{% highlight c# tabtitle="C#" %}
//Loads the template document
WordDocument document = new WordDocument("Template.docx");
//Finds all occurrences of a misspelled word and replaces with properly spelled word
document.Replace("Cyles", "Cycles", true, true);
//Saves and closes the document
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Loads the template document
Dim document As WordDocument = New WordDocument("Template.docx")
'Finds all occurrences of a misspelled word and replaces with properly spelled word
document.Replace("Cyles", "Cycles", True, True)
'Saves and closes the document
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing word document 
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Docx);
//Finds all occurrences of a misspelled word and replaces with properly spelled word
document.Replace("Cyles", "Cycles", true, true);
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word document file in local machine
Save(stream, "Sample.docx");
//Closes the document instance
document.Close();

//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
// Saves the Word document
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Loads the template document
FileStream fileStreamPath = new FileStream("Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);
//Finds all occurrences of a misspelled word and replaces with properly spelled word
document.Replace("Cyles", "Cycles", true, true);
//Saves and closes the document
FileStream outputStream = new FileStream("Sample.docx", FileMode.Create, FileAccess.ReadWrite, FileShare.ReadWrite);
document.Save(outputStream, FormatType.Docx);
document.Close();
outputStream.Flush();
outputStream.Dispose();
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing wod document
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Automatic);
//Finds all occurrences of a misspelled word and replaces with properly spelled word
document.Replace("Cyles", "Cycles", true, true);
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Find-and-Replace/Replace-misspelled-word).

## Find and replace text with an image
You can find placeholder text in a Word document and replace it with any desired image.

The following code example illustrates how to find and replace text in a word document with an image

{% tabs %}  

{% highlight c# tabtitle="C#" %}
//Loads the template document
WordDocument document = new WordDocument("Template.docx");
//Finds all the image placeholder text in the Word document
TextSelection[] textSelections = document.FindAll(new Regex("^//(.*)"));
for (int i = 0; i < textSelections.Length; i++)
{
	//Replaces the image placeholder text with desired image
	WParagraph paragraph = new WParagraph(document);
	WPicture picture = paragraph.AppendPicture(Image.FromFile(@"Filepath" + textSelections[i].SelectedText + ".png")) as WPicture;
	TextSelection newSelection = new TextSelection(paragraph, 0, 1);
	TextBodyPart bodyPart = new TextBodyPart(document);
	bodyPart.BodyItems.Add(paragraph);
	document.Replace(textSelections[i].SelectedText, bodyPart, true, true);
}
//Saves and closes the document
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Loads the template document
Dim document As WordDocument = New WordDocument("Template.docx")
'Finds all the image placeholder text in the Word document
Dim textSelections() As TextSelection = document.FindAll(New Regex("^//(.*)"))
For i As Integer = 0 To textSelections.Length – 1
	'Replaces the image placeholder text with desired image
	Dim paragraph As WParagraph = New WParagraph(document)
	Dim picture As WPicture = CType(paragraph.AppendPicture(Image.FromFile("Filepath" + textSelections(i).SelectedText + ".png")), WPicture)
	Dim newSelection As TextSelection = New TextSelection(paragraph, 0, 1)
	Dim bodyPart As TextBodyPart = New TextBodyPart(document)
	bodyPart.BodyItems.Add(paragraph)
	document.Replace(textSelections(i).SelectedText, bodyPart, True, True)
Next
'Saves and closes the document
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing word document 
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Docx);
//Finds all the image placeholder text in the Word document
TextSelection[] textSelections = document.FindAll(new Regex("^//(.*)"));
for (int i = 0; i < textSelections.Length; i++)
{
	//Replaces the image placeholder text with desired image
	WParagraph paragraph = new WParagraph(document);
	Stream imageStream = assembly.GetManifestResourceStream("Sample.Assets." + textSelections[i].SelectedText.Trim('/') + ".png");
	WPicture picture = paragraph.AppendPicture(imageStream) as WPicture;
	TextSelection newSelection = new TextSelection(paragraph, 0, 1);
	TextBodyPart bodyPart = new TextBodyPart(document);
	bodyPart.BodyItems.Add(paragraph);
	document.Replace(textSelections[i].SelectedText, bodyPart, true, true);
}
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

{% highlight c# tabtitle="ASP.NET Core" %}
//Loads the template document
FileStream fileStreamPath = new FileStream("Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);
//Finds all the image placeholder text in the Word document
TextSelection[] textSelections = document.FindAll(new Regex("^//(.*)"));
for (int i = 0; i < textSelections.Length; i++)
{
	//Replaces the image placeholder text with desired image
	WParagraph paragraph = new WParagraph(document);
	FileStream imageStream = new FileStream("Filepath" + textSelections[i].SelectedText + ".png", FileMode.Open, FileAccess.ReadWrite);
	WPicture picture = paragraph.AppendPicture(imageStream) as WPicture;
	TextSelection newSelection = new TextSelection(paragraph, 0, 1);
	TextBodyPart bodyPart = new TextBodyPart(document);
	bodyPart.BodyItems.Add(paragraph);
	document.Replace(textSelections[i].SelectedText, bodyPart, true, true);
}
//Saves and closes the document
FileStream outputStream = new FileStream("Sample.docx", FileMode.Create, FileAccess.ReadWrite, FileShare.ReadWrite);
document.Save(outputStream, FormatType.Docx);
document.Close();
outputStream.Flush();
outputStream.Dispose();
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing wod document
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Automatic);
//Finds all the image placeholder text in the Word document
TextSelection[] textSelections = document.FindAll(new Regex("^//(.*)"));
for (int i = 0; i < textSelections.Length; i++)
{
	//Replaces the image placeholder text with desired image
	WParagraph paragraph = new WParagraph(document);
	Stream imageStream = assembly.GetManifestResourceStream("Sample.Assets."+ textSelections[i].SelectedText.Trim('/') + ".png");
	WPicture picture = paragraph.AppendPicture(imageStream) as WPicture;
	TextSelection newSelection = new TextSelection(paragraph, 0, 1);
	TextBodyPart bodyPart = new TextBodyPart(document);
	bodyPart.BodyItems.Add(paragraph);
	document.Replace(textSelections[i].SelectedText, bodyPart, true, true);
}
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Find-and-Replace/Find-and-replace-text-with-image).

## Find and replace a pattern of text with a merge field 
You can find and replace a pattern of text in a Word document with merge fields using Regex.

The following code example illustrates how to create a mail merge template by replacing a pattern of text (enclosed within ‘«’ and ‘»’) in a Word document with the desired merge fields.

{% tabs %}  

{% highlight c# tabtitle="C#" %}
//Loads the template document
WordDocument document = new WordDocument("Template.docx");
//Finds all the placeholder text enclosed within '«' and '»' in the Word document
TextSelection[] textSelections = document.FindAll(new Regex("«([(?i)image(?-i)]*:*[a-zA-Z0-9 ]*:*[a-zA-Z0-9 ]+)»"));
string[] searchedPlaceholders = new string[textSelections.Length];
for (int i = 0; i < textSelections.Length; i++)
{
	searchedPlaceholders[i] = textSelections[i].SelectedText;
}
for (int i = 0; i < searchedPlaceholders.Length; i++)
{
	//Replaces the placeholder text enclosed within '«' and '»' with desired merge field
	WParagraph paragraph = new WParagraph(document);
	paragraph.AppendField(searchedPlaceholders[i].TrimStart('«').TrimEnd('»'), FieldType.FieldMergeField);
	TextSelection newSelection = new TextSelection(paragraph, 0, paragraph.Items.Count);
	TextBodyPart bodyPart = new TextBodyPart(document);
	bodyPart.BodyItems.Add(paragraph);
	document.Replace(searchedPlaceholders[i], bodyPart, true, true, true);
}
//Saves the Word document
document.Save("Sample.docx", FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Loads the template document
Dim document As WordDocument = New WordDocument("Template.docx")
'Finds all the placeholder text enclosed within '«' and '»' in the Word document
Dim textSelections() As TextSelection = document.FindAll(New Regex("([(?i)image(?-i)]*:*[a-zA-Z0-9 ]*:*[a-zA-Z0-9 ]+)»"))
Dim searchedPlaceholders() As String = New String(textSelections.Length - 1) {}
For i As Integer = 0 To textSelections.Length - 1
	searchedPlaceholders(i) = textSelections(i).SelectedText
Next
For i As Integer = 0 To searchedPlaceholders.Length - 1
	'Replaces the placeholder text enclosed within '«' and '»' with desired merge field
	Dim paragraph As WParagraph = New WParagraph(document)
	paragraph.AppendField(searchedPlaceholders(i).TrimStart("«").TrimEnd("»"), FieldType.FieldMergeField)
	Dim newSelection As TextSelection = New TextSelection(paragraph, 0, 	paragraph.Items.Count)
	Dim bodyPart As TextBodyPart = New TextBodyPart(document)
	bodyPart.BodyItems.Add(paragraph)
	document.Replace(searchedPlaceholders(i), bodyPart, True, True, True)
Next
'Saves the Word document
document.Save("Sample.docx", FormatType.Docx)
'Closes the document
document.Close()

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing word document 
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Docx);
//Finds all the placeholder text enclosed within '«' and '»' in the Word document
TextSelection[] textSelections = document.FindAll(new Regex("«([(?i)image(?-i)]*:*[a-zA-Z0-9 ]*:*[a-zA-Z0-9 ]+)»"));
string[] searchedPlaceholders = new string[textSelections.Length];
for (int i = 0; i < textSelections.Length; i++)
{
	searchedPlaceholders[i] = textSelections[i].SelectedText;
}
for (int i = 0; i < searchedPlaceholders.Length; i++)
{
	//Replaces the placeholder text enclosed within '«' and '»' with desired merge field
	WParagraph paragraph = new WParagraph(document);
	paragraph.AppendField(searchedPlaceholders[i].TrimStart('«').TrimEnd('»'), FieldType.FieldMergeField);
	TextSelection newSelection = new TextSelection(paragraph, 0, paragraph.Items.Count);
	TextBodyPart bodyPart = new TextBodyPart(document);
	bodyPart.BodyItems.Add(paragraph);
	document.Replace(searchedPlaceholders[i], bodyPart, true, true, true);
}
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

{% highlight c# tabtitle="ASP.NET Core" %}
//Loads the template document
FileStream fileStreamPath = new FileStream("Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);
//Finds all the placeholder text enclosed within '«' and '»' in the Word document
TextSelection[] textSelections = document.FindAll(new Regex("«([(?i)image(?-i)]*:*[a-zA-Z0-9 ]*:*[a-zA-Z0-9 ]+)»"));
string[] searchedPlaceholders = new string[textSelections.Length];
for (int i = 0; i < textSelections.Length; i++)
{
	searchedPlaceholders[i] = textSelections[i].SelectedText;
}
for (int i = 0; i < searchedPlaceholders.Length; i++)
{
	//Replaces the placeholder text enclosed within '«' and '»' with desired merge field
	WParagraph paragraph = new WParagraph(document);
	paragraph.AppendField(searchedPlaceholders[i].TrimStart('«').TrimEnd('»'), FieldType.FieldMergeField);
	TextSelection newSelection = new TextSelection(paragraph, 0, paragraph.Items.Count);
	TextBodyPart bodyPart = new TextBodyPart(document);
	bodyPart.BodyItems.Add(paragraph);
	document.Replace(searchedPlaceholders[i], bodyPart, true, true, true);
}

//Saves and closes the document
FileStream outputStream = new FileStream("Sample.docx", FileMode.Create, FileAccess.ReadWrite, FileShare.ReadWrite);
document.Save(outputStream, FormatType.Docx);
document.Close();
outputStream.Flush();
outputStream.Dispose();

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing wod document
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Automatic);
//Finds all the placeholder text enclosed within '«' and '»' in the Word document
TextSelection[] textSelections = document.FindAll(new Regex("«([(?i)image(?-i)]*:*[a-zA-Z0-9 ]*:*[a-zA-Z0-9 ]+)»"));
string[] searchedPlaceholders = new string[textSelections.Length];
for (int i = 0; i < textSelections.Length; i++)
{
	searchedPlaceholders[i] = textSelections[i].SelectedText;
}
for (int i = 0; i < searchedPlaceholders.Length; i++)
{
	//Replaces the placeholder text enclosed within '«' and '»' with desired merge field
	WParagraph paragraph = new WParagraph(document);
	paragraph.AppendField(searchedPlaceholders[i].TrimStart('«').TrimEnd('»'), FieldType.FieldMergeField);
	TextSelection newSelection = new TextSelection(paragraph, 0, paragraph.Items.Count);
	TextBodyPart bodyPart = new TextBodyPart(document);
	bodyPart.BodyItems.Add(paragraph);
	document.Replace(searchedPlaceholders[i], bodyPart, true, true, true);
}
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Find-and-Replace/Find-and-replace-with-merge-field).

## Find and replace text with a table 
You can find placeholder text in a Word document and replace it with a table.

The following code example illustrates how to do this.

{% tabs %}  

{% highlight c# tabtitle="C#" %}
//Loads the template document
WordDocument document = new WordDocument("Template.docx");
//Creates a new table
WTable table = new WTable(document);
table.ResetCells(1, 6);
table[0, 0].Width = 52f;
table[0, 0].AddParagraph().AppendText("Supplier ID");
table[0, 1].Width = 128f;
table[0, 1].AddParagraph().AppendText("Company Name");
table[0, 2].Width = 70f;
table[0, 2].AddParagraph().AppendText("Contact Name");
table[0, 3].Width = 92f;
table[0, 3].AddParagraph().AppendText("Address");
table[0, 4].Width = 66.5f;
table[0, 4].AddParagraph().AppendText("City");
table[0, 5].Width = 56f;
table[0, 5].AddParagraph().AppendText("Country");
//Imports data to the table
ImportDataToTable(table);
//Applies the built-in table style (Medium Shading 1 Accent 1) to the table
table.ApplyStyle(BuiltinTableStyle.MediumShading1Accent1);
//Replaces the table placeholder text with a new table
TextBodyPart bodyPart = new TextBodyPart(document);
bodyPart.BodyItems.Add(table);
document.Replace("[Suppliers table]", bodyPart, true, true, true);
//Saves the Word document
document.Save("Sample.docx", FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Loads the template document
Dim document As WordDocument = New WordDocument("Template.docx")
'Creates a new table
Dim table As WTable = New WTable(document)
table.ResetCells(1, 6)
table(0, 0).Width = 52.0
table(0, 0).AddParagraph.AppendText("Supplier ID")
table(0, 1).Width = 128.0
table(0, 1).AddParagraph.AppendText("Company Name")
table(0, 2).Width = 70.0
table(0, 2).AddParagraph.AppendText("Contact Name")
table(0, 3).Width = 92.0
table(0, 3).AddParagraph.AppendText("Address")
table(0, 4).Width = 66.5
table(0, 4).AddParagraph.AppendText("City")
table(0, 5).Width = 56.0
table(0, 5).AddParagraph.AppendText("Country")
'Imports data to the table
ImportDataToTable(table)
'Applies the built-in table style (Medium Shading 1 Accent 1) to the table
table.ApplyStyle(BuiltinTableStyle.MediumShading1Accent1)
Dim bodyPart As TextBodyPart = New TextBodyPart(document)
bodyPart.BodyItems.Add(table)
document.Replace("[Suppliers table]", bodyPart, True, True, True)
'Saves the Word document
document.Save("Result.docx", FormatType.Docx)
'Closes the document
document.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing word document 
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Docx);
//Creates a new table
WTable table = new WTable(document);
table.ResetCells(1, 6);
table[0, 0].Width = 52f;
table[0, 0].AddParagraph().AppendText("Supplier ID");
table[0, 1].Width = 128f;
table[0, 1].AddParagraph().AppendText("Company Name");
table[0, 2].Width = 70f;
table[0, 2].AddParagraph().AppendText("Contact Name");
table[0, 3].Width = 92f;
table[0, 3].AddParagraph().AppendText("Address");
table[0, 4].Width = 66.5f;
table[0, 4].AddParagraph().AppendText("City");
table[0, 5].Width = 56f;
table[0, 5].AddParagraph().AppendText("Country");
//Imports data to the table
ImportDataToTable(table);
//Applies the built-in table style (Medium Shading 1 Accent 1) to the table
table.ApplyStyle(BuiltinTableStyle.MediumShading1Accent1);
//Replaces the table placeholder text with a new table
TextBodyPart bodyPart = new TextBodyPart(document);
bodyPart.BodyItems.Add(table);
document.Replace("[Suppliers table]", bodyPart, true, true, true);
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

{% highlight c# tabtitle="ASP.NET Core" %}
//Loads the template document
FileStream fileStreamPath = new FileStream("Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);
//Creates a new table
WTable table = new WTable(document);
table.ResetCells(1, 6);
table[0, 0].Width = 52f;
table[0, 0].AddParagraph().AppendText("Supplier ID");
table[0, 1].Width = 128f;
table[0, 1].AddParagraph().AppendText("Company Name");
table[0, 2].Width = 70f;
table[0, 2].AddParagraph().AppendText("Contact Name");
table[0, 3].Width = 92f;
table[0, 3].AddParagraph().AppendText("Address");
table[0, 4].Width = 66.5f;
table[0, 4].AddParagraph().AppendText("City");
table[0, 5].Width = 56f;
table[0, 5].AddParagraph().AppendText("Country");
//Imports data to the table
ImportDataToTable(table);
//Applies the built-in table style (Medium Shading 1 Accent 1) to the table
table.ApplyStyle(BuiltinTableStyle.MediumShading1Accent1);
//Replaces the table placeholder text with a new table
TextBodyPart bodyPart = new TextBodyPart(document);
bodyPart.BodyItems.Add(table);
document.Replace("[Suppliers table]", bodyPart, true, true, true);
//Saves and closes the document
FileStream outputStream = new FileStream("Sample.docx", FileMode.Create, FileAccess.ReadWrite, FileShare.ReadWrite);
document.Save(outputStream, FormatType.Docx);
document.Close();
outputStream.Flush();
outputStream.Dispose();
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing wod document
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Automatic);
//Creates a new table
WTable table = new WTable(document);
table.ResetCells(1, 6);
table[0, 0].Width = 52f;
table[0, 0].AddParagraph().AppendText("Supplier ID");
table[0, 1].Width = 128f;
table[0, 1].AddParagraph().AppendText("Company Name");
table[0, 2].Width = 70f;
table[0, 2].AddParagraph().AppendText("Contact Name");
table[0, 3].Width = 92f;
table[0, 3].AddParagraph().AppendText("Address");
table[0, 4].Width = 66.5f;
table[0, 4].AddParagraph().AppendText("City");
table[0, 5].Width = 56f;
table[0, 5].AddParagraph().AppendText("Country");
//Imports data to the table
ImportDataToTable(table);
//Applies the built-in table style (Medium Shading 1 Accent 1) to the table
table.ApplyStyle(BuiltinTableStyle.MediumShading1Accent1);
//Replaces the table placeholder text with a new table
TextBodyPart bodyPart = new TextBodyPart(document);
bodyPart.BodyItems.Add(table);
document.Replace("[Suppliers table]", bodyPart, true, true, true);
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

The following code example provides supporting methods for the above code.

{% tabs %}  

{% highlight c# tabtitle="C#" %}
private void ImportDataToTable(WTable table)
{
	FileStream fs = new FileStream("Suppliers.xml", FileMode.Open, FileAccess.Read);
	XmlReader reader = XmlReader.Create(fs);
	if (reader == null)
		throw new Exception("reader");
	while (reader.NodeType != XmlNodeType.Element)
		reader.Read();
	if (reader.LocalName != "SuppliersList")
		throw new XmlException("Unexpected xml tag " + reader.LocalName);
	reader.Read();
	while (reader.NodeType == XmlNodeType.Whitespace)
		reader.Read();
	while (reader.LocalName != "SuppliersList")
	{
		if (reader.NodeType == XmlNodeType.Element)
		{
			switch (reader.LocalName)
			{
				case "Suppliers":
					//Adds new row to the table for importing data from next record
					WTableRow tableRow = table.AddRow(true);
					ImportDataToRow(reader, tableRow);
					break;
			}
		}
		else
		{
			reader.Read();
			if ((reader.LocalName == "SuppliersList") && reader.NodeType == XmlNodeType.EndElement)
				break;
		}
	}
	reader.Dispose();
	fs.Dispose();
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Private Sub ImportDataToTable(ByVal table As WTable)
		Dim fs As FileStream = New FileStream("Suppliers.xml", FileMode.Open, FileAccess.Read)
		Dim reader As XmlReader = XmlReader.Create(fs)
		If (reader Is Nothing) Then
			Throw New Exception("reader")
		End If
		While (reader.NodeType <> XmlNodeType.Element)
			reader.Read()
		End While
		If (reader.LocalName <> "SuppliersList") Then
			Throw New XmlException(("Unexpected xml tag " + reader.LocalName))
		End If
		reader.Read
		While (reader.NodeType = XmlNodeType.Whitespace)
			reader.Read()
		End While
		While (reader.LocalName <> "SuppliersList")
			If (reader.NodeType = XmlNodeType.Element) Then
				Select Case (reader.LocalName)
					Case "Suppliers"
						'Adds new row to the table for importing data from next record
						Dim tableRow As WTableRow = table.AddRow(True)
						ImportDataToRow(reader, tableRow)
				End Select
			Else
				reader.Read
				If ((reader.LocalName = "SuppliersList") _
					AndAlso (reader.NodeType = XmlNodeType.EndElement)) Then
					Exit While
				End If
			End If
		End While
		reader.Dispose
		fs.Dispose
End Sub

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
private void ImportDataToTable(WTable table)
{
	//"App" is the class of Portable project
	Assembly assembly = typeof(App).GetTypeInfo().Assembly;
	XmlReader reader = XmlReader.Create(assembly.GetManifestResourceStream("Sample.Assets.Suppliers.xml"));
	if (reader == null)
		throw new Exception("reader");
	while (reader.NodeType != XmlNodeType.Element)
		reader.Read();
	if (reader.LocalName != "SuppliersList")
		throw new XmlException("Unexpected xml tag " + reader.LocalName);
	reader.Read();
	while (reader.NodeType == XmlNodeType.Whitespace)
		reader.Read();
	while (reader.LocalName != "SuppliersList")
	{
		if (reader.NodeType == XmlNodeType.Element)
		{
			switch (reader.LocalName)
			{
				case "Suppliers":
					//Adds new row to the table for importing data from next record
					WTableRow tableRow = table.AddRow(true);
					ImportDataToRow(reader, tableRow);
					break;
			}
		}
		else
		{
			reader.Read();
			if ((reader.LocalName == "SuppliersList") && reader.NodeType == XmlNodeType.EndElement)
				break;
		}
	}
	reader.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
private void ImportDataToTable(WTable table)
{
	FileStream fs = new FileStream("Suppliers.xml", FileMode.Open, FileAccess.Read);
	XmlReader reader = XmlReader.Create(fs);
	if (reader == null)
		throw new Exception("reader");
	while (reader.NodeType != XmlNodeType.Element)
		reader.Read();
	if (reader.LocalName != "SuppliersList")
		throw new XmlException("Unexpected xml tag " + reader.LocalName);
	reader.Read();
	while (reader.NodeType == XmlNodeType.Whitespace)
		reader.Read();
	while (reader.LocalName != "SuppliersList")
	{
		if (reader.NodeType == XmlNodeType.Element)
		{
			switch (reader.LocalName)
			{
				case "Suppliers":
					//Adds new row to the table for importing data from next record
					WTableRow tableRow = table.AddRow(true);
					ImportDataToRow(reader, tableRow);
					break;
			}
		}
		else
		{
			reader.Read();
			if ((reader.LocalName == "SuppliersList") && reader.NodeType == XmlNodeType.EndElement)
				break;
		}
	}
	reader.Dispose();
	fs.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
private void ImportDataToTable(WTable table)
{
	//"App" is the class of Portable project
	Assembly assembly = typeof(App).GetTypeInfo().Assembly;
	XmlReader reader = XmlReader.Create(assembly.GetManifestResourceStream("Sample.Assets.Suppliers.xml"));
	if (reader == null)
		throw new Exception("reader");
	while (reader.NodeType != XmlNodeType.Element)
		reader.Read();
	if (reader.LocalName != "SuppliersList")
		throw new XmlException("Unexpected xml tag " + reader.LocalName);
	reader.Read();
	while (reader.NodeType == XmlNodeType.Whitespace)
		reader.Read();
	while (reader.LocalName != "SuppliersList")
	{
		if (reader.NodeType == XmlNodeType.Element)
		{
			switch (reader.LocalName)
			{
				case "Suppliers":
					//Adds new row to the table for importing data from next record
					WTableRow tableRow = table.AddRow(true);
					ImportDataToRow(reader, tableRow);
					break;
			}
		}
		else
		{
			reader.Read();
			if ((reader.LocalName == "SuppliersList") && reader.NodeType == XmlNodeType.EndElement)
				break;
		}
	}
	reader.Dispose();
}
{% endhighlight %}

{% endtabs %}

The following code example provides supporting methods for the above code.

{% tabs %}  

{% highlight c# tabtitle="C#" %}
Private void ImportDataToRow(XmlReader reader, WTableRow tableRow)
{
	if (reader == null)
		throw new Exception("reader");
	while (reader.NodeType != XmlNodeType.Element)
		reader.Read();
	if (reader.LocalName != "Suppliers")
		throw new XmlException("Unexpected xml tag " + reader.LocalName);
	reader.Read();
	while (reader.NodeType == XmlNodeType.Whitespace)
		reader.Read();
	while (reader.LocalName != "Suppliers")
	{
		if (reader.NodeType == XmlNodeType.Element)
		{
			switch (reader.LocalName)
			{
				case "SupplierID":
					tableRow.Cells[0].AddParagraph().AppendText(reader.ReadElementContentAsString());
					break;
				case "CompanyName":
					tableRow.Cells[1].AddParagraph().AppendText(reader.ReadElementContentAsString());
					break;
				case "ContactName":
					tableRow.Cells[2].AddParagraph().AppendText(reader.ReadElementContentAsString());
					break;
				case "Address":
					tableRow.Cells[3].AddParagraph().AppendText(reader.ReadElementContentAsString());
					break;
				case "City":
					tableRow.Cells[4].AddParagraph().AppendText(reader.ReadElementContentAsString());
					break;
				case "Country":
					tableRow.Cells[5].AddParagraph().AppendText(reader.ReadElementContentAsString());
					break;
				default:
					reader.Skip();
					break;
			}
		}
		else
		{
			reader.Read();
			if ((reader.LocalName == "Suppliers") && reader.NodeType == XmlNodeType.EndElement)
				break;
		}
	}
}

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Private Sub ImportDataToRow(ByVal reader As XmlReader, ByVal tableRow As WTableRow)
		If (reader Is Nothing) Then
			Throw New Exception("reader")
		End If
		While (reader.NodeType <> XmlNodeType.Element)
			reader.Read()
		End While
		If (reader.LocalName <> "Suppliers") Then
			Throw New XmlException(("Unexpected xml tag " + reader.LocalName))
		End If
		reader.Read
		While (reader.NodeType = XmlNodeType.Whitespace)
			reader.Read()
		End While
		While (reader.LocalName <> "Suppliers")
			If (reader.NodeType = XmlNodeType.Element) Then
				Select Case (reader.LocalName)
					Case "SupplierID"
						tableRow.Cells(0).AddParagraph.AppendText(reader.ReadElementContentAsString)
					Case "CompanyName"
						tableRow.Cells(1).AddParagraph.AppendText(reader.ReadElementContentAsString)
					Case "ContactName"
						tableRow.Cells(2).AddParagraph.AppendText(reader.ReadElementContentAsString)
					Case "Address"
						tableRow.Cells(3).AddParagraph.AppendText(reader.ReadElementContentAsString)
					Case "City"
						tableRow.Cells(4).AddParagraph.AppendText(reader.ReadElementContentAsString)
					Case "Country"
						tableRow.Cells(5).AddParagraph.AppendText(reader.ReadElementContentAsString)
					Case Else
						reader.Skip
				End Select
			Else
				reader.Read
				If ((reader.LocalName = "Suppliers") _
					AndAlso (reader.NodeType = XmlNodeType.EndElement)) Then
					Exit While
				End If
			End If
		End While
End Sub

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
private void ImportDataToRow(XmlReader reader, WTableRow tableRow)
{
	if (reader == null)
		throw new Exception("reader");
	while (reader.NodeType != XmlNodeType.Element)
		reader.Read();
	if (reader.LocalName != "Suppliers")
		throw new XmlException("Unexpected xml tag " + reader.LocalName);
	reader.Read();
	while (reader.NodeType == XmlNodeType.Whitespace)
		reader.Read();
	while (reader.LocalName != "Suppliers")
	{
		if (reader.NodeType == XmlNodeType.Element)
		{
			switch (reader.LocalName)
			{
				case "SupplierID":
					tableRow.Cells[0].AddParagraph().AppendText(reader.ReadElementContentAsString());
					break;
				case "CompanyName":
					tableRow.Cells[1].AddParagraph().AppendText(reader.ReadElementContentAsString());
					break;
				case "ContactName":
					tableRow.Cells[2].AddParagraph().AppendText(reader.ReadElementContentAsString());
					break;
				case "Address":
					tableRow.Cells[3].AddParagraph().AppendText(reader.ReadElementContentAsString());
					break;
				case "City":
					tableRow.Cells[4].AddParagraph().AppendText(reader.ReadElementContentAsString());
					break;
				case "Country":
					tableRow.Cells[5].AddParagraph().AppendText(reader.ReadElementContentAsString());
					break;
				default:
					reader.Skip();
					break;
			}
		}
		else
		{
			reader.Read();
			if ((reader.LocalName == "Suppliers") && reader.NodeType == XmlNodeType.EndElement)
				break;
		}
	}
}

{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
Private void ImportDataToRow(XmlReader reader, WTableRow tableRow)
{
	if (reader == null)
		throw new Exception("reader");
	while (reader.NodeType != XmlNodeType.Element)
		reader.Read();
	if (reader.LocalName != "Suppliers")
		throw new XmlException("Unexpected xml tag " + reader.LocalName);
	reader.Read();
	while (reader.NodeType == XmlNodeType.Whitespace)
		reader.Read();
	while (reader.LocalName != "Suppliers")
	{
		if (reader.NodeType == XmlNodeType.Element)
		{
			switch (reader.LocalName)
			{
				case "SupplierID":
					tableRow.Cells[0].AddParagraph().AppendText(reader.ReadElementContentAsString());
					break;
				case "CompanyName":
					tableRow.Cells[1].AddParagraph().AppendText(reader.ReadElementContentAsString());
					break;
				case "ContactName":
					tableRow.Cells[2].AddParagraph().AppendText(reader.ReadElementContentAsString());
					break;
				case "Address":
					tableRow.Cells[3].AddParagraph().AppendText(reader.ReadElementContentAsString());
					break;
				case "City":
					tableRow.Cells[4].AddParagraph().AppendText(reader.ReadElementContentAsString());
					break;
				case "Country":
					tableRow.Cells[5].AddParagraph().AppendText(reader.ReadElementContentAsString());
					break;
				default:
					reader.Skip();
					break;
			}
		}
		else
		{
			reader.Read();
			if ((reader.LocalName == "Suppliers") && reader.NodeType == XmlNodeType.EndElement)
				break;
		}
	}
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
private void ImportDataToRow(XmlReader reader, WTableRow tableRow)
{
	if (reader == null)
		throw new Exception("reader");
	while (reader.NodeType != XmlNodeType.Element)
		reader.Read();
	if (reader.LocalName != "Suppliers")
		throw new XmlException("Unexpected xml tag " + reader.LocalName);
	reader.Read();
	while (reader.NodeType == XmlNodeType.Whitespace)
		reader.Read();
	while (reader.LocalName != "Suppliers")
	{
		if (reader.NodeType == XmlNodeType.Element)
		{
			switch (reader.LocalName)
			{
				case "SupplierID":
					tableRow.Cells[0].AddParagraph().AppendText(reader.ReadElementContentAsString());
					break;
				case "CompanyName":
					tableRow.Cells[1].AddParagraph().AppendText(reader.ReadElementContentAsString());
					break;
				case "ContactName":
					tableRow.Cells[2].AddParagraph().AppendText(reader.ReadElementContentAsString());
					break;
				case "Address":
					tableRow.Cells[3].AddParagraph().AppendText(reader.ReadElementContentAsString());
					break;
				case "City":
					tableRow.Cells[4].AddParagraph().AppendText(reader.ReadElementContentAsString());
					break;
				case "Country":
					tableRow.Cells[5].AddParagraph().AppendText(reader.ReadElementContentAsString());
					break;
				default:
					reader.Skip();
					break;
			}
		}
		else
		{
			reader.Read();
			if ((reader.LocalName == "Suppliers") && reader.NodeType == XmlNodeType.EndElement)
				break;
		}
	}
}
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Find-and-Replace/Find-and-replace-text-with-table).

## Find and replace text in Word document with another document 

You can find and replace text with another Word document.

The following code example illustrates how to merge or combine Word documents by replacing text with another document (the content of a subheading).

{% tabs %}  

{% highlight c# tabtitle="C#" %}
//Loads the template document
WordDocument document = new WordDocument("Template.docx");
//Finds all the content placeholder text in the Word document
TextSelection[] textSelections = document.FindAll(new Regex(@"\[(.*)\]"));
for (int i = 0; i < textSelections.Length; i++)
{
	//Replaces the content placeholder text with desired Word document.
	WordDocument subDocument = new WordDocument("Filepath"+ textSelections[i].SelectedText.TrimStart('[').TrimEnd(']') + ".docx", FormatType.Docx);
	document.Replace(textSelections[i].SelectedText, subDocument, true, true);
	subDocument.Dispose();
}
//Saves and closes the document instance
document.Save("Result.docx");
document.Close();

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}'Loads the template document
Dim document As WordDocument = New WordDocument("Template.docx")
'Finds all the content placeholder text in the Word document
Dim textSelections() As TextSelection = document.FindAll(New Regex("\[(.*)\]"))
For i As Integer = 0 To textSelections.Length - 1
	'Replaces the content placeholder text with desired Word document.
	Dim subDocument As WordDocument = New WordDocument("Filepath" + textSelections(i).SelectedText.TrimStart("[").TrimEnd("]") + ".docx", FormatType.Docx)
	document.Replace(textSelections(i).SelectedText, subDocument, True, True)
	subDocument.Dispose()
Next
'Saves and closes the document instance
document.Save("Result.docx")
document.Close()

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing word document 
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Docx);
//Finds all the content placeholder text in the Word document
TextSelection[] textSelections = document.FindAll(new Regex(@"\[(.*)\]"));
for (int i = 0; i < textSelections.Length; i++)
{
	//Replaces the content placeholder text with desired Word document.
	WordDocument subDocument = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets." + textSelections[i].SelectedText.TrimStart('[').TrimEnd(']') + ".docx"), FormatType.Docx);
	document.Replace(textSelections[i].SelectedText, subDocument, true, true);
	subDocument.Dispose();
}
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

{% highlight c# tabtitle="ASP.NET Core" %}
//Loads the template document
FileStream fileStreamPath = new FileStream("Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);
//Finds all the content placeholder text in the Word document
TextSelection[] textSelections = document.FindAll(new Regex(@"\[(.*)\]"));
for (int i = 0; i < textSelections.Length; i++)
{
	//Replaces the content placeholder text with desired Word document.
	WordDocument subDocument = new WordDocument(new FileStream("Filepath" + textSelections[i].SelectedText.TrimStart('[').TrimEnd(']') + ".docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite), FormatType.Docx);
	document.Replace(textSelections[i].SelectedText, subDocument, true, true);
	subDocument.Dispose();
}
//Saves and closes the document
FileStream outputStream = new FileStream("Sample.docx", FileMode.Create, FileAccess.ReadWrite, FileShare.ReadWrite);
document.Save(outputStream, FormatType.Docx);
document.Close();
outputStream.Flush();
outputStream.Dispose();

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing wod document
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Automatic);
//Finds all the content placeholder text in the Word document
TextSelection[] textSelections = document.FindAll(new Regex(@"\[(.*)\]"));
for (int i = 0; i < textSelections.Length; i++)
{
	//Replaces the content placeholder text with desired Word document.
	WordDocument subDocument = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets."+ textSelections[i].SelectedText.TrimStart('[').TrimEnd(']') + ".docx"), FormatType.Docx);
	document.Replace(textSelections[i].SelectedText, subDocument, true, true);
	subDocument.Dispose();
}
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Find-and-Replace/Find-and-replace-with-Word-document).

## Find and replace text extending to several paragraphs

Apart from finding text in a paragraph, you can also find and replace text that extends to several paragraphs in a Word document. You can find the first occurrence of the text that extends to several paragraphs by using the `FindSingleLine` method. Find the next occurrences of the text by using the `FindNextSingleLine` method. Similarly, you can replace text that extends to several paragraphs by using `ReplaceSingleLine` method.

The following code example illustrates how to replace text that extends to several paragraphs.

{% tabs %}  

{% highlight c# tabtitle="C#" %}
//Opens the input Word document.
WordDocument document = new WordDocument("Template.docx");
WordDocument subDocument = new WordDocument("Source.docx", FormatType.Docx);
//Gets the content from another Word document 
TextBodyPart replacePart = new TextBodyPart(subDocument);
foreach (TextBodyItem bodyItem in subDocument.LastSection.Body.ChildEntities)
{
	replacePart.BodyItems.Add(bodyItem.Clone());
}
string placeholderText = "Suppliers/Vendors of Northwind" + "Customers of Northwind"+ "Employee details of Northwind traders" + "The product information"+ "The inventory details" + "The shippers" + "Purchase Order transactions" + "Sales Order transaction" + "Inventory transactions" + "Invoices" + "[end replace]";
//Finds the text that extends to several paragraphs and replaces it with desired content
document.ReplaceSingleLine(placeholderText, replacePart, false, false);
subDocument.Dispose();
//Saves and closes the document instance
document.Save("Result.docx");
document.Close();

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Loads the template document
Dim document As WordDocument = New WordDocument("Template.docx")
Dim subDocument As WordDocument = New WordDocument("Source.docx", FormatType.Docx)
Dim replacePart As TextBodyPart = New TextBodyPart(subDocument)
'Gets the content from another Word document 
For Each bodyItem As TextBodyItem In subDocument.LastSection.Body.ChildEntities
	replacePart.BodyItems.Add(bodyItem.Clone)
Next
Dim placeholderText As String = "Suppliers/Vendors of Northwind" + "Customers of Northwind" + "Employee details of Northwind traders" + "The product information" + "The inventory details" + "The shippers" + "Purchase Order transactions" + "Sales Order transaction" + "Inventory transactions" + "Invoices" + "[end replace]"
'Finds the text that extends to several paragraphs and replaces it with desired content
document.ReplaceSingleLine(placeholderText, replacePart, False, False)
subDocument.Dispose()
'Saves and closes the document instance
document.Save("Result.docx")
document.Close()

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing word document 
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Docx);
WordDocument subDocument = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Source.docx"), FormatType.Docx);
//Gets the content from another Word document 
TextBodyPart replacePart = new TextBodyPart(subDocument);
foreach (TextBodyItem bodyItem in subDocument.LastSection.Body.ChildEntities)
{
	replacePart.BodyItems.Add(bodyItem.Clone());
}
string placeholderText = "Suppliers/Vendors of Northwind" + "Customers of Northwind" + "Employee details of Northwind traders" + "The product information" + "The inventory details" + "The shippers" + "Purchase Order transactions" + "Sales Order transaction" + "Inventory transactions" + "Invoices" + "[end replace]";
//Finds the text that extends to several paragraphs and replaces it with desired content
document.ReplaceSingleLine(placeholderText, replacePart, false, false);
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

{% highlight c# tabtitle="ASP.NET Core" %}
//Loads the template document
FileStream fileStreamPath = new FileStream("Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);
WordDocument subDocument = new WordDocument(new FileStream("Source.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite), FormatType.Docx);
//Gets the content from another Word document 
TextBodyPart replacePart = new TextBodyPart(subDocument);
foreach (TextBodyItem bodyItem in subDocument.LastSection.Body.ChildEntities)
{
	replacePart.BodyItems.Add(bodyItem.Clone());
}
string placeholderText = "Suppliers/Vendors of Northwind" + "Customers of Northwind" + "Employee details of Northwind traders" + "The product information" + "The inventory details" + "The shippers" + "Purchase Order transactions" + "Sales Order transaction" + "Inventory transactions" + "Invoices" + "[end replace]";
//Finds the text that extends to several paragraphs and replaces it with desired content
document.ReplaceSingleLine(placeholderText, replacePart, false, false);
//Saves and closes the document
FileStream outputStream = new FileStream("Sample.docx", FileMode.Create, FileAccess.ReadWrite, FileShare.ReadWrite);
document.Save(outputStream, FormatType.Docx);
document.Close();
outputStream.Flush();
outputStream.Dispose();

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing wod document
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Automatic);
WordDocument subDocument = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Source.docx"), FormatType.Docx);
//Gets the content from another Word document 
TextBodyPart replacePart = new TextBodyPart(subDocument);
foreach (TextBodyItem bodyItem in subDocument.LastSection.Body.ChildEntities)
{
	replacePart.BodyItems.Add(bodyItem.Clone());
}
string placeholderText = "Suppliers/Vendors of Northwind" + "Customers of Northwind" + "Employee details of Northwind traders" + "The product information" + "The inventory details" + "The shippers" + "Purchase Order transactions" + "Sales Order transaction" + "Inventory transactions" + "Invoices" + "[end replace]";
//Finds the text that extends to several paragraphs and replaces it with desired content
document.ReplaceSingleLine(placeholderText, replacePart, false, false);
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Find-and-Replace/Find-and-replace-multiple-paragraphs).

## Find text in a Word document and format 

You can find text in a Word document and format or highlight it .You can find the first occurrence of text using the `Find` method. Find the next occurrences of the text using the `FindNext` method.

The following code example illustrates how to find all occurrences of a length of text and highlight it.

{% tabs %}  

{% highlight c# tabtitle="C#" %}
//Loads the template document
WordDocument document = new WordDocument("Template.docx");
//Finds all occurrence of the text in the Word document
TextSelection[] textSelections = document.FindAll("Adventure", true, true);
for (int i = 0; i < textSelections.Length; i++)
{
	//Sets the highlight color for the searched text as Yellow
	textSelections[i].GetAsOneRange().CharacterFormat.HighlightColor = Color.Yellow;
}
//Saves and closes the document instance
document.Save("Result.docx");
document.Close();

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Loads the template document
Dim document As WordDocument = New WordDocument("Template.docx")
'Finds all occurrence of the text in the Word document
Dim textSelections() As TextSelection = document.FindAll("Adventure", True, True)
For i As Integer = 0 To textSelections.Length - 1
	'Sets the highlight color for the searched text as Yellow.
	textSelections(i).GetAsOneRange.CharacterFormat.HighlightColor = Color.Yellow
Next
'Saves and closes the document instance
document.Save("Result.docx")
document.Close()

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing word document 
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Docx);
//Finds all occurrence of the text in the Word document
TextSelection[] textSelections = document.FindAll("Adventure", true, true);
for (int i = 0; i < textSelections.Length; i++)
{
	//Sets the highlight color for the searched text as Yellow
	textSelections[i].GetAsOneRange().CharacterFormat.HighlightColor = Color.Yellow;
}
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

{% highlight c# tabtitle="ASP.NET Core" %}
//Loads the template document
FileStream fileStreamPath = new FileStream("Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);
//Finds all occurrence of the text in the Word document
TextSelection[] textSelections = document.FindAll("Adventure", true, true);
for (int i = 0; i < textSelections.Length; i++)
{
	//Sets the highlight color for the searched text as Yellow
	textSelections[i].GetAsOneRange().CharacterFormat.HighlightColor = Color.Yellow;
}
//Saves and closes the document
FileStream outputStream = new FileStream("Sample.docx", FileMode.Create, FileAccess.ReadWrite, FileShare.ReadWrite);
document.Save(outputStream, FormatType.Docx);
document.Close();
outputStream.Flush();
outputStream.Dispose();

{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing wod document
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Automatic);
//Finds all occurrence of the text in the Word document
TextSelection[] textSelections = document.FindAll("Adventure", true, true);
for (int i = 0; i < textSelections.Length; i++)
{
	//Sets the highlight color for the searched text as Yellow
	textSelections[i].GetAsOneRange().CharacterFormat.HighlightColor = Syncfusion.Drawing.Color.Yellow;
}
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Find-and-Replace/Find-and-highlight-all).

## Find and replace the pattern of text with normal text

You can find the pattern of text using Regex and replace it with normal text in a Word document using the `Replace` method.

The following code example illustrates how to replace the pattern of text with normal text in the Word document.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Open an existing Word document.
using (WordDocument document = new WordDocument("Template.docx", FormatType.Docx))
{
    //Replace all occurrences of the given pattern of text with normal text.
    document.Replace(new Regex("{[A-Za-z]+}"), "cycles company");
    //Save the Word document.
    document.Save("Sample.docx", FormatType.Docx);
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Open an existing Word document.
Using document As WordDocument = New WordDocument("Template.docx", FormatType.Docx)
    'Replace all occurrences of the given pattern of text with normal text.
    document.Replace(New Regex("{[A-Za-z]+}"), "cycles company")
    'Save the WordDocument instance.
    document.Save("Sample.docx", FormatType.Docx)
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Open the file as Stream.
using (Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Template.docx"))
{
    //Load the file stream into a Word document.
    using (WordDocument document = new WordDocument(docStream, FormatType.Automatic))
    {
        //Replace all occurrences of the given pattern of text with normal text.
        document.Replace(new Regex("{[A-Za-z]+}"), "cycles company");
        //Save the Word document to MemoryStream.
        MemoryStream stream = new MemoryStream();
        await document.SaveAsync(stream, FormatType.Docx);
        //Save the stream as a Word document file on the local machine.
        Save(stream, "Sample.docx");
        //Please refer to the link below to save the Word document in the UWP platform.
        //https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
    }
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Open the file as Stream.
using (FileStream docStream = new FileStream("Template.docx", FileMode.Open, FileAccess.Read))
{
    //Load the file stream into a Word document.
    using (WordDocument document = new WordDocument(docStream, FormatType.Automatic))
    {
        //Replace all occurrences of the given pattern of text with normal text.
        document.Replace(new Regex("{[A-Za-z]+}"), "cycles company");
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
//Open the file as Stream.
using (Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Template.docx"))
{
    //Load file stream into Word document.
    using (WordDocument document = new WordDocument(docStream, FormatType.Automatic))
    {
        //Replace all occurrences of the given pattern of text with normal text.
        document.Replace(new Regex("{[A-Za-z]+}"), "cycles company");
        //Save the Word document to MemoryStream.
        MemoryStream outputStream = new MemoryStream();
        document.Save(outputStream, FormatType.Docx);
        //Save the stream as a file in the device and invoke it for viewing.
        Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.docx", "application/msword", outputStream);
        //Please download the helper files from the link below to save the stream as a file and open the file for viewing on the Xamarin platform.
        //https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
    }
}
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Find-and-Replace/Replace-pattern-text-with-normal-text).

## Find and replace a pattern of multiline text

You can find a pattern of text which extends to several paragraphs using Regex and replace it with normal text in a Word document using the ` ReplaceSingleLine` method.

The following code example illustrates how to replace a pattern of multiline text with a single line in a Word document.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Open an existing Word document.
using (WordDocument document = new WordDocument("Template.docx", FormatType.Docx))
{
    //Replace the text extended to several paragraphs with simple text.
    document.ReplaceSingleLine(new Regex(@"\[(.*)\]"), "Thank you for Payment");
    //Save the Word document.
    document.Save("Sample.docx", FormatType.Docx);
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Open an existing Word document.
Using document As WordDocument = New WordDocument("Template.docx", FormatType.Docx)
    'Replace the text extended to several paragraphs with simple text.
    document.ReplaceSingleLine(New Regex("\[(.*)\]"), "Thank you for Payment")
    'Save the Word document.
    document.Save("Sample.docx", FormatType.Docx)
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Open the file as Stream.
using (Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Template.docx"))
{
    //Load the file stream into a Word document.
    using (WordDocument document = new WordDocument(docStream, FormatType.Docx))
    {
        //Replace the text extended to several paragraphs with simple text.
        document.ReplaceSingleLine(new Regex(@"\[(.*)\]"), "Thank you for Payment");
        //Save the Word document to MemoryStream.
        MemoryStream stream = new MemoryStream();
        await document.SaveAsync(stream, FormatType.Docx);
        //Save the stream as a Word document file in the local machine.
        Save(stream, "Sample.docx");
        //Please refer to the link below to save the Word document in the UWP platform.
        //https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
    }
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Open the file as Stream.
using (FileStream docStream = new FileStream("Template.docx", FileMode.Open, FileAccess.Read))
{
    //Load the file stream into a Word document.
    using (WordDocument document = new WordDocument(docStream, FormatType.Docx))
    {
        //Replace the text extended to several paragraphs with simple text.
        document.ReplaceSingleLine(new Regex(@"\[(.*)\]"), "Thank you for Payment");
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
//Open the file as Stream.
using (Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Template.docx"))
{
    //Load the file stream into a Word document.
    using (WordDocument document = new WordDocument(docStream, FormatType.Docx))
    {
        //Replace the text extended to several paragraphs with simple text.
        document.ReplaceSingleLine(new Regex(@"\[(.*)\]"), "Thank you for Payment");
        //Save the Word document to MemoryStream.
        MemoryStream outputStream = new MemoryStream();
        document.Save(outputStream, FormatType.Docx);
        //Save the stream as a file in the device and invoke it for viewing.
        Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.docx", "application/msword", outputStream);
        //Please download the helper files from the link below to save the stream as a file and open the file for viewing on the Xamarin platform.
        //https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
    }
}
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Find-and-Replace/Replace-multiline-text-with-single-line).

## Find and replace text with formatted text

You can select a text using the `Find` method and replace text in a Word document with that selected text along with formatting (bold, italic, and so on).

The following code example illustrates how to find and replace text with the formatted text in the Word document.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Open an existing Word document.
using (WordDocument document = new WordDocument("Template.docx", FormatType.Docx))
{
    //Find the first occurrence of a particular text in the document.
    TextSelection selection = document.Find(new Regex ("^«(.*)»"));
    //Replace the particular text with the selected text along with formatting.
    document.Replace("Bear", selection, false, false, true);
    //Save the Word document.
    document.Save("Sample.docx", FormatType.Docx);
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Open an existing Word document.
Using document As WordDocument = New WordDocument("Template.docx", FormatType.Docx)
    'Find the first occurrence of a particular text in the document.
    Dim selection As TextSelection = document.Find(New Regex("^«(.*)»"))
    'Replace the particular text with the selected text along with formatting.
    document.Replace("Bear", selection, False, False, True)
    'Save the Word document.
    document.Save("Sample.docx", FormatType.Docx)
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Open the file as Stream.
using (Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Template.docx"))
{
    //Load the file stream into the Word document.
    using (WordDocument document = new WordDocument(docStream, FormatType.Automatic))
    {
        //Find the first occurrence of a particular text in the document.
        TextSelection selection = document.Find(new Regex ("^«(.*)»"));
        //Replace the particular text with the selected text along with formatting.
        document.Replace("Bear", selection, false, false, true);
        //Save the Word document to MemoryStream.
        MemoryStream stream = new MemoryStream();
        await document.SaveAsync(stream, FormatType.Docx);
        //Save the stream as a Word document file on the local machine.
        Save(stream, "Sample.docx");
        //Please refer to the link below to save the Word document in the UWP platform.
        //https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
    }
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Open the file as Stream.
using (FileStream docStream = new FileStream("Template.docx", FileMode.Open, FileAccess.Read))
{
    //Load the file stream into a Word document.
    using (WordDocument document = new WordDocument(docStream, FormatType.Automatic))
    {
        //Find the first occurrence of a particular text in the document.
        TextSelection selection = document.Find(new Regex ("^«(.*)»"));
        //Replace the particular text with the selected text along with formatting.
        document.Replace("Bear", selection, false, false, true);
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
//Open the file as Stream.
using (Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Template.docx"))
{
    //Load the file stream into a Word document.
    using (WordDocument document = new WordDocument(docStream, FormatType.Automatic))
    {
        //Find the first occurrence of a particular text in the document.
        TextSelection selection = document.Find(new Regex ("^«(.*)»"));
        //Replace the particular text with the selected text along with formatting.
        document.Replace("Bear", selection, false, false, true);
        //Save the Word document to MemoryStream.
        MemoryStream outputStream = new MemoryStream();
        document.Save(outputStream, FormatType.Docx);
        //Save the stream as a file in the device and invoke it for viewing.
        Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.docx", "application/msword", outputStream);
        //Please download the helper files from the link below to save the stream as a file and open the file for viewing on the Xamarin platform.
        //https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
    }
}
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Find-and-Replace/Find-and-replace-text-with-formatted-text).

## Find and replace the text extended to several paragraphs

You can select a text which extends to several paragraphs using the `FindSingleLine` method and replace text in the Word document with that selected text.

The following code example illustrates how to find and replace the text extended to several paragraphs in the Word document.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Open an existing Word document.
using (WordDocument document = new WordDocument("Template.docx", FormatType.Docx))
{
    //Find the first occurrence of particular text extended to several paragraphs in the document.
    TextSelection[] textSelections = document.FindSingleLine(new Regex(@"\[(.*)\]"));
    //Replace the particular text extended to several paragraphs with the selected text.
    document.ReplaceSingleLine(new Regex("<<(.*)>>"), textSelections[1]);
    //Save the Word document.
    document.Save("Sample.docx", FormatType.Docx);
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Open an existing Word document.
Using document As WordDocument = New WordDocument("Template.docx", FormatType.Docx)
    'Find the first occurrence of particular text extended to several paragraphs in the document.
    Dim textSelections As TextSelection() = document.FindSingleLine(New Regex("\[(.*)\]"))
    'Replace the particular text extended to several paragraphs with the selected text.
    document.ReplaceSingleLine(New Regex("<<(.*)>>"), textSelections(1))
    'Save the Word document.
    document.Save("Sample.docx", FormatType.Docx)
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Open the file as Stream.
using (Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Template.docx"))
{
    //Load the file stream into a Word document.
    using (WordDocument document = new WordDocument(docStream, FormatType.Automatic))
    {
        //Find the first occurrence of particular text extended to several paragraphs in the document.
        TextSelection[] textSelections = document.FindSingleLine(new Regex(@"\[(.*)\]"));
        //Replace the particular text extended to several paragraphs with the selected text.
        document.ReplaceSingleLine(new Regex("<<(.*)>>"), textSelections[1]);
        //Save the Word document to MemoryStream.
        MemoryStream stream = new MemoryStream();
        await document.SaveAsync(stream, FormatType.Docx);
        //Save the stream as a Word document file in the local machine.
        Save(stream, "Sample.docx");
        //Please refer to the link below to save the Word document in the UWP platform.
        //https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
    }
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Open the file as Stream.
using (FileStream docStream = new FileStream("Template.docx", FileMode.Open, FileAccess.Read))
{
    //Load the file stream into a Word document.
    using (WordDocument document = new WordDocument(docStream, FormatType.Automatic))
    {
        //Find the first occurrence of particular text extended to several paragraphs in the document.
        TextSelection[] textSelections = document.FindSingleLine(new Regex(@"\[(.*)\]"));
        //Replace the particular text extended to several paragraphs with the selected text.
        document.ReplaceSingleLine(new Regex("<<(.*)>>"), textSelections[1]);
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
//Open the file as Stream.
using (Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Template.docx"))
{
    //Load the file stream into a Word document.
    using (WordDocument document = new WordDocument(docStream, FormatType.Automatic))
    {
        //Find the first occurrence of particular text extended to several paragraphs in the document.
        TextSelection[] textSelections = document.FindSingleLine(new Regex(@"\[(.*)\]"));
        //Replace the particular text extended to several paragraphs with the selected text.
        document.ReplaceSingleLine(new Regex("<<(.*)>>"), textSelections[1]);
        //Save the Word document to MemoryStream.
        MemoryStream outputStream = new MemoryStream();
        document.Save(outputStream, FormatType.Docx);
        //Save the stream as a file in the device and invoke it for viewing.
        Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.docx", "application/msword", outputStream);
        //Please download the helper files from the link below to save the stream as a file and open the file for viewing on the Xamarin platform.
        //https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
    }
}
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Find-and-Replace/Replace-text-extended-to-several-paragraphs).

## See Also

* [How to replace the particular text with hyperlink in Word document](https://www.syncfusion.com/kb/11774/how-to-replace-the-particular-text-with-hyperlink-in-word-document)
* [How to find the empty paragraphs in the Word document using Essential DocIO](https://www.syncfusion.com/kb/3956/how-to-find-the-empty-paragraphs-in-the-word-document-using-essential-docio)
* [How to replace text in a Word document with HTML](https://www.syncfusion.com/kb/13627/how-to-replace-text-in-a-word-document-with-html)