---
title: Presentation Working with Find and Replace | Syncfusion
description: This section illustrates how to find a particular text and replace it with another text or part of the document
platform: file-formats
control: Presentation
documentation: UG
keywords: 
---
# Working with Find and Replace

.NET PowerPoint library allows you to search a particular text you like to change and replace it with another text in the PowerPoint presentation.

* You can replace either the first occurrence or all the occurrences of the text with another text in all PowerPoint slides and elements such as shape, textbox, table, smartart, etc.
* You can replace the text in specific slide, notes slide, master slide or layout slide.
* You can replace the text by matching case, whole word and all occurrences or first occurrence alone.
* You can also replace the content that spans across several lines.

## Find and replace in PowerPoint presentation

You can find text in a PowerPoint presentation and replace it with other text.

The following code example illustrates how to find all occurences of a particular text and replace it with other text in a PowerPoint presentation.

{% tabs %}  

{% highlight c# tabtitle="C#" %}
//Opens an existing presentation.
using (IPresentation pptxDoc = Presentation.Open("Sample.pptx"))
{
	//Finds all the occurrences of a particular text in the PowerPoint presentation
	ITextSelection[] textSelections = pptxDoc.FindAll("product", false, false);
	foreach (ITextSelection textSelection in textSelections)
	{
		//Gets the found text as single text part
		ITextPart textPart = textSelection.GetAsOneTextPart();
		//Replace the text
		textPart.Text = "Service";
	}
	//Saves the Presentation	
	pptxDoc.Save("Output.pptx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Opens an existing presentation.
Using pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
	'Finds all the occurrences of a particular text in the PowerPoint presentation
	Dim textSelections As ITextSelection() = pptxDoc.FindAll("product", False, False)
	For Each textSelection As ITextSelection In textSelections
		'Gets the found text as single text part
		Dim textPart As ITextPart = textSelection.GetAsOneTextPart()
		'Replace the text
		textPart.Text = "Service"
	Next
	'Saves the Presentation	
	pptxDoc.Save("Output.pptx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".pptx");
//Creates a storage file from FileOpenPicker
StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = await Presentation.OpenAsync(inputStorageFile);
//Finds all the occurrences of a particular text in the PowerPoint presentation
ITextSelection[] textSelections = pptxDoc.FindAll("product", false, false);
foreach (ITextSelection textSelection in textSelections)
{
	//Gets the found text as single text part
	ITextPart textPart = textSelection.GetAsOneTextPart();
	//Replace the text
	textPart.Text = "Service";
}
//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Output";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });
//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();
//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Opens an existing presentation.           
FileStream inputStream = new FileStream("Sample.pptx", FileMode.Open);
using (IPresentation pptxDoc = Presentation.Open(inputStream))
{
	//Finds all the occurrences of a particular text in the PowerPoint presentation
	ITextSelection[] textSelections = pptxDoc.FindAll("product", false, false);
	foreach (ITextSelection textSelection in textSelections)
	{
		//Gets the found text as single text part
		ITextPart textPart = textSelection.GetAsOneTextPart();
		//Replace the text
		textPart.Text = "Service";
	}
	//Save the PowerPoint Presentation as stream
	FileStream outputStream = new FileStream("Output.pptx", FileMode.Create);
	pptxDoc.Save(outputStream);
	//Release all resources of the stream
	outputStream.Dispose();
	//Closes the Presentation instance
	pptxDoc.Close();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Sample.pptx");
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);
//Finds all the occurrences of a particular text in the PowerPoint presentation
ITextSelection[] textSelections = pptxDoc.FindAll("product", false, false);
foreach (ITextSelection textSelection in textSelections)
{
	//Gets the found text as single text part
	ITextPart textPart = textSelection.GetAsOneTextPart();
	//Replace the text
	textPart.Text = "Service";
}
//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();
//Save Presentation in stream format.
pptxDoc.Save(stream);
//Close the presentation
pptxDoc.Close();
stream.Position = 0;
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
	Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
{% endhighlight %}

{% endtabs %}  

### Match case

You can find and replace the text by matching case also.

The following code example illustrates how to find all occurences of a particular text by matching its case.

{% tabs %}  

{% highlight c# tabtitle="C#" %}
//Opens an existing presentation.
using (IPresentation pptxDoc = Presentation.Open("Sample.pptx"))
{
	bool matchCase = true;
	bool wholeWord = false;
	//Finds all the occurrences of a particular text which matches the given casing
	ITextSelection[] textSelections = pptxDoc.FindAll("product", matchCase, wholeWord);
	foreach (ITextSelection textSelection in textSelections)
	{
		//Gets the found text as single text part
		ITextPart textPart = textSelection.GetAsOneTextPart();
		//Replace the text
		textPart.Text = "Service";
	}
	//Saves the Presentation	
	pptxDoc.Save("Output.pptx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Opens an existing presentation.
Using pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
	Dim matchCase = True
	Dim wholeWord = False
	'Finds all the occurrences of a particular text which matches the given casing
	Dim textSelections As ITextSelection() = pptxDoc.FindAll("product", matchCase, wholeWord)
	For Each textSelection As ITextSelection In textSelections
		'Gets the found text as single text part
		Dim textPart As ITextPart = textSelection.GetAsOneTextPart()
		'Replace the text
		textPart.Text = "Service"
	Next
	'Saves the Presentation	
	pptxDoc.Save("Output.pptx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".pptx");
//Creates a storage file from FileOpenPicker
StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = await Presentation.OpenAsync(inputStorageFile);
bool matchCase = true;
bool wholeWord = false;
//Finds all the occurrences of a particular text which matches the given casing
ITextSelection[] textSelections = pptxDoc.FindAll("product", matchCase, wholeWord);
foreach (ITextSelection textSelection in textSelections)
{
	//Gets the found text as single text part
	ITextPart textPart = textSelection.GetAsOneTextPart();
	//Replace the text
	textPart.Text = "Service";
}
//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Output";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });
//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();
//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Opens an existing presentation.           
FileStream inputStream = new FileStream("Sample.pptx", FileMode.Open);
using (IPresentation pptxDoc = Presentation.Open(inputStream))
{
	bool matchCase = true;
	bool wholeWord = false;
	//Finds all the occurrences of a particular text which matches the given casing
	ITextSelection[] textSelections = pptxDoc.FindAll("product", matchCase, wholeWord);
	foreach (ITextSelection textSelection in textSelections)
	{
		//Gets the found text as single text part
		ITextPart textPart = textSelection.GetAsOneTextPart();
		//Replace the text
		textPart.Text = "Service";
	}
	//Save the PowerPoint Presentation as stream
	FileStream outputStream = new FileStream("Output.pptx", FileMode.Create);
	pptxDoc.Save(outputStream);
	//Release all resources of the stream
	outputStream.Dispose();
	//Closes the Presentation instance
	pptxDoc.Close();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Sample.pptx");
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);
bool matchCase = true;
bool wholeWord = false;
//Finds all the occurrences of a particular text which matches the given casing
ITextSelection[] textSelections = pptxDoc.FindAll("product", matchCase, wholeWord);
foreach (ITextSelection textSelection in textSelections)
{
	//Gets the found text as single text part
	ITextPart textPart = textSelection.GetAsOneTextPart();
	//Replace the text
	textPart.Text = "Service";
}
//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();
//Save Presentation in stream format.
pptxDoc.Save(stream);
//Close the presentation
pptxDoc.Close();
stream.Position = 0;
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
	Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
{% endhighlight %}

{% endtabs %}  

### Whole words only

You can find and replace the text by matching whole word only.

The following code example illustrates how to find all occurences of a particular text by matching the whole word.

{% tabs %}  

{% highlight c# tabtitle="C#" %}
//Opens an existing presentation.
using (IPresentation pptxDoc = Presentation.Open("Sample.pptx"))
{
	bool matchCase = false;
	bool wholeWord = true;
	//Finds all the occurrences of a given whole word
	ITextSelection[] textSelections = pptxDoc.FindAll("product", matchCase, wholeWord);
	foreach (ITextSelection textSelection in textSelections)
	{
		//Gets the found text as single text part
		ITextPart textPart = textSelection.GetAsOneTextPart();
		//Replace the text
		textPart.Text = "Service";
	}
	//Saves the Presentation	
	pptxDoc.Save("Output.pptx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Opens an existing presentation.
Using pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
	Dim matchCase = False
	Dim wholeWord = True
	'Finds all the occurrences of a given whole word
	Dim textSelections As ITextSelection() = pptxDoc.FindAll("product", matchCase, wholeWord)
	For Each textSelection As ITextSelection In textSelections
		'Gets the found text as single text part
		Dim textPart As ITextPart = textSelection.GetAsOneTextPart()
		'Replace the text
		textPart.Text = "Service"
	Next
	'Saves the Presentation	
	pptxDoc.Save("Output.pptx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".pptx");
//Creates a storage file from FileOpenPicker
StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = await Presentation.OpenAsync(inputStorageFile);
bool matchCase = false;
bool wholeWord = true;
//Finds all the occurrences of a given whole word
ITextSelection[] textSelections = pptxDoc.FindAll("product", matchCase, wholeWord);
foreach (ITextSelection textSelection in textSelections)
{
	//Gets the found text as single text part
	ITextPart textPart = textSelection.GetAsOneTextPart();
	//Replace the text
	textPart.Text = "Service";
}
//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Output";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });
//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();
//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Opens an existing presentation.           
FileStream inputStream = new FileStream("Sample.pptx", FileMode.Open);
using (IPresentation pptxDoc = Presentation.Open(inputStream))
{
	bool matchCase = false;
	bool wholeWord = true;
	//Finds all the occurrences of a given whole word
	ITextSelection[] textSelections = pptxDoc.FindAll("product", matchCase, wholeWord);
	foreach (ITextSelection textSelection in textSelections)
	{
		//Gets the found text as single text part
		ITextPart textPart = textSelection.GetAsOneTextPart();
		//Replace the text
		textPart.Text = "Service";
	}
	//Save the PowerPoint Presentation as stream
	FileStream outputStream = new FileStream("Output.pptx", FileMode.Create);
	pptxDoc.Save(outputStream);
	//Release all resources of the stream
	outputStream.Dispose();
	//Closes the Presentation instance
	pptxDoc.Close();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Sample.pptx");
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);
bool matchCase = false;
bool wholeWord = true;
//Finds all the occurrences of a given whole word
ITextSelection[] textSelections = pptxDoc.FindAll("product", matchCase, wholeWord);
foreach (ITextSelection textSelection in textSelections)
{
	//Gets the found text as single text part
	ITextPart textPart = textSelection.GetAsOneTextPart();
	//Replace the text
	textPart.Text = "Service";
}
//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();
//Save Presentation in stream format.
pptxDoc.Save(stream);
//Close the presentation
pptxDoc.Close();
stream.Position = 0;
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
	Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
{% endhighlight %}

{% endtabs %}  

### Find and replace the first occurrence

You can find only the first occurrence of the text and replace it with other text.

The following code example illustrates how to find the first occurrence of particular text and replace it with other text.

{% tabs %}  

{% highlight c# tabtitle="C#" %}
//Opens an existing presentation.
using (IPresentation pptxDoc = Presentation.Open("Sample.pptx"))
{
	//Finds the first occurrence of a particular text in the PowerPoint presentation
	ITextSelection textSelection = pptxDoc.Find("product", false, false);
	//Gets the found text as single text part
	ITextPart textPart = textSelection.GetAsOneTextPart();
	//Replace the text
	textPart.Text = "Service";
	//Saves the Presentation	
	pptxDoc.Save("Output.pptx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Opens an existing presentation.
Using pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
	'Finds the first occurrence of a particular text in the PowerPoint presentation
	Dim textSelection As ITextSelection = pptxDoc.Find("product", False, False)
	'Gets the found text as single text part
	Dim textPart As ITextPart = textSelection.GetAsOneTextPart()
	'Replace the text
	textPart.Text = "Service"
	'Saves the Presentation	
	pptxDoc.Save("Output.pptx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".pptx");
//Creates a storage file from FileOpenPicker
StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = await Presentation.OpenAsync(inputStorageFile);
//Finds the first occurrence of a particular text in the PowerPoint presentation
ITextSelection textSelection = pptxDoc.Find("product", false, false);
//Gets the found text as single text part
ITextPart textPart = textSelection.GetAsOneTextPart();
//Replace the text
textPart.Text = "Service";
//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Output";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });
//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();
//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Opens an existing presentation.           
FileStream inputStream = new FileStream("Sample.pptx", FileMode.Open);
using (IPresentation pptxDoc = Presentation.Open(inputStream))
{
	//Finds the first occurrence of a particular text in the PowerPoint presentation
	ITextSelection textSelection = pptxDoc.Find("product", false, false);
	//Gets the found text as single text part
	ITextPart textPart = textSelection.GetAsOneTextPart();
	//Replace the text
	textPart.Text = "Service";
	//Save the PowerPoint Presentation as stream
	FileStream outputStream = new FileStream("Output.pptx", FileMode.Create);
	pptxDoc.Save(outputStream);
	//Release all resources of the stream
	outputStream.Dispose();
	//Closes the Presentation instance
	pptxDoc.Close();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Sample.pptx");
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);
//Finds the first occurrence of a particular text in the PowerPoint presentation
ITextSelection textSelection = pptxDoc.Find("product", false, false);
//Gets the found text as single text part
ITextPart textPart = textSelection.GetAsOneTextPart();
//Replace the text
textPart.Text = "Service";
//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();
//Save Presentation in stream format.
pptxDoc.Save(stream);
//Close the presentation
pptxDoc.Close();
stream.Position = 0;
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
	Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
{% endhighlight %}

{% endtabs %}  

## Find and replace in specific slide

You can find all occurences of a text in specific PowerPoint slide (slide, notes slide, master slide or layout slide) and replace it with other text.

The following code example illustrates how to find all occurences of a particular text and replace with other text in a specific slide.

{% tabs %}  

{% highlight c# tabtitle="C#" %}
//Opens an existing presentation.
using (IPresentation pptxDoc = Presentation.Open("Sample.pptx"))
{
	ISlide slide = pptxDoc.Slides[0];
	//Finds all the occurrences of a particular text in the specific slide
	ITextSelection[] textSelections = slide.FindAll("product", false, false);
	foreach (ITextSelection textSelection in textSelections)
	{
		//Gets the found text as single text part
		ITextPart textPart = textSelection.GetAsOneTextPart();
		//Replace the text
		textPart.Text = "Service";
	}
	//Saves the Presentation	
	pptxDoc.Save("Output.pptx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Opens an existing presentation.
Using pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
	Dim slide As ISlide = pptxDoc.Slides(0)
	'Finds all the occurrences of a particular text in the specific slide
	Dim textSelections As ITextSelection() = slide.FindAll("product", False, False)
	For Each textSelection As ITextSelection In textSelections
		'Gets the found text as single text part
		Dim textPart As ITextPart = textSelection.GetAsOneTextPart()
		'Replace the text
		textPart.Text = "Service"
	Next
	'Saves the Presentation	
	pptxDoc.Save("Output.pptx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
 //Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".pptx");
//Creates a storage file from FileOpenPicker
StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = await Presentation.OpenAsync(inputStorageFile);
ISlide slide = pptxDoc.Slides[0];
//Finds all the occurrences of a particular text in the specific slide
ITextSelection[] textSelections = slide.FindAll("product", false, false);
foreach (ITextSelection textSelection in textSelections)
{
	//Gets the found text as single text part
	ITextPart textPart = textSelection.GetAsOneTextPart();
	//Replace the text
	textPart.Text = "Service";
}
//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Output";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });
//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();
//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
 //Opens an existing presentation.           
FileStream inputStream = new FileStream("Sample.pptx", FileMode.Open);
using (IPresentation pptxDoc = Presentation.Open(inputStream))
{
	ISlide slide = pptxDoc.Slides[0];
	//Finds all the occurrences of a particular text in the specific slide
	ITextSelection[] textSelections = slide.FindAll("product", false, false);
	foreach (ITextSelection textSelection in textSelections)
	{
		//Gets the found text as single text part
		ITextPart textPart = textSelection.GetAsOneTextPart();
		//Replace the text
		textPart.Text = "Service";
	}
	//Save the PowerPoint Presentation as stream
	FileStream outputStream = new FileStream("Output.pptx", FileMode.Create);
	pptxDoc.Save(outputStream);
	//Release all resources of the stream
	outputStream.Dispose();
	//Closes the Presentation instance
	pptxDoc.Close();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Sample.pptx");
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);
ISlide slide = pptxDoc.Slides[0];
//Finds all the occurrences of a particular text in the specific slide
ITextSelection[] textSelections = slide.FindAll("product", false, false);
foreach (ITextSelection textSelection in textSelections)
{
	//Gets the found text as single text part
	ITextPart textPart = textSelection.GetAsOneTextPart();
	//Replace the text
	textPart.Text = "Service";
}
//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();
//Save Presentation in stream format.
pptxDoc.Save(stream);
//Close the presentation
pptxDoc.Close();
stream.Position = 0;
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
	Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
{% endhighlight %}

{% endtabs %}  

## Find and highlight in PowerPoint presentation

.NET PowerPoint library allows you to find all the occurences of a text in the PowerPoint presentation and highlight it.

The following code example illustrates how to find all the occurences of a particular text and highlight it.

{% tabs %}  

{% highlight c# tabtitle="C#" %}
//Opens an existing presentation.
using (IPresentation pptxDoc = Presentation.Open("Sample.pptx"))
{
	//Finds all the occurrences of a particular text in the PowerPoint presentation
	ITextSelection[] textSelections = pptxDoc.FindAll("product", false, false);
	foreach (ITextSelection textSelection in textSelections)
	{
		//Gets the found text containing text parts
		foreach (ITextPart textPart in textSelection.GetTextParts())
		{
			//Sets highlight color
			textPart.Font.HighlightColor = ColorObject.Yellow;
		}
	}
	//Saves the Presentation	
	pptxDoc.Save("Output.pptx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Opens an existing presentation.
Using pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
	'Finds all the occurrences of a particular text in the PowerPoint presentation
	Dim textSelections As ITextSelection() = pptxDoc.FindAll("product", False, False)
	For Each textSelection As ITextSelection In textSelections
		'Gets the found text containing text parts
		For Each textPart As ITextPart In textSelection.GetTextParts()
			'Sets highlight color
			textPart.Font.HighlightColor = ColorObject.Yellow
		Next
	Next
	'Saves the Presentation	
	pptxDoc.Save("Output.pptx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".pptx");
//Creates a storage file from FileOpenPicker
StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = await Presentation.OpenAsync(inputStorageFile);
//Finds all the occurrences of a particular text in the PowerPoint presentation
ITextSelection[] textSelections = pptxDoc.FindAll("product", false, false);
foreach (ITextSelection textSelection in textSelections)
{
	//Gets the found text containing text parts
	foreach (ITextPart textPart in textSelection.GetTextParts())
	{
		//Sets highlight color
		textPart.Font.HighlightColor = ColorObject.Yellow;
	}
}
//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Output";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });
//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();
//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Opens an existing presentation.           
FileStream inputStream = new FileStream("Sample.pptx", FileMode.Open);
using (IPresentation pptxDoc = Presentation.Open(inputStream))
{
	//Finds all the occurrences of a particular text in the PowerPoint presentation
	ITextSelection[] textSelections = pptxDoc.FindAll("product", false, false);
	foreach (ITextSelection textSelection in textSelections)
	{
		//Gets the found text containing text parts
		foreach (ITextPart textPart in textSelection.GetTextParts())
		{
			//Sets highlight color
			textPart.Font.HighlightColor = ColorObject.Yellow;
		}
	}
	//Save the PowerPoint Presentation as stream
	FileStream outputStream = new FileStream("Output.pptx", FileMode.Create);
	pptxDoc.Save(outputStream);
	//Release all resources of the stream
	outputStream.Dispose();
	//Closes the Presentation instance
	pptxDoc.Close();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Sample.pptx");
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);
//Finds all the occurrences of a particular text in the PowerPoint presentation
ITextSelection[] textSelections = pptxDoc.FindAll("product", false, false);
foreach (ITextSelection textSelection in textSelections)
{
	//Gets the found text containing text parts
	foreach (ITextPart textPart in textSelection.GetTextParts())
	{
		//Sets highlight color
		textPart.Font.HighlightColor = ColorObject.Yellow;
	}
}
//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();
//Save Presentation in stream format.
pptxDoc.Save(stream);
//Close the presentation
pptxDoc.Close();
stream.Position = 0;
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
	Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
{% endhighlight %}

{% endtabs %}  

## Find and highlight in specific slide

You can find all the occurences of a text in specific PowerPoint slide (slide, notes slide, master slide or layout slide) and highlight the found text.

The following code example illustrates how to find all the occurrences of a particular text and highlight it in specific slide.

{% tabs %}  

{% highlight c# tabtitle="C#" %}
//Opens an existing presentation.
using (IPresentation pptxDoc = Presentation.Open("Sample.pptx"))
{
	ISlide slide = pptxDoc.Slides[0];
	//Finds all the occurrences of a particular text in the specific slide
	ITextSelection[] textSelections = slide.FindAll("product", false, false);
	foreach (ITextSelection textSelection in textSelections)
	{
		//Gets the found text containing text parts
		foreach (ITextPart textPart in textSelection.GetTextParts())
		{
			//Sets highlight color
			textPart.Font.HighlightColor = ColorObject.Yellow;
		}
	}
	//Saves the Presentation	
	pptxDoc.Save("Output.pptx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Opens an existing presentation.
Using pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
	Dim slide As ISlide = pptxDoc.Slides(0)
	'Finds all the occurrences of a particular text in the specific slide
	Dim textSelections As ITextSelection() = slide.FindAll("product", False, False)
	For Each textSelection As ITextSelection In textSelections
		'Gets the found text containing text parts
		For Each textPart As ITextPart In textSelection.GetTextParts()
			'Sets highlight color
			textPart.Font.HighlightColor = ColorObject.Yellow
		Next
	Next
	'Saves the Presentation	
	pptxDoc.Save("Output.pptx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".pptx");
//Creates a storage file from FileOpenPicker
StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = await Presentation.OpenAsync(inputStorageFile);
ISlide slide = pptxDoc.Slides[0];
//Finds all the occurrences of a particular text in the specific slide
ITextSelection[] textSelections = slide.FindAll("product", false, false);
foreach (ITextSelection textSelection in textSelections)
{
	//Gets the found text containing text parts
	foreach (ITextPart textPart in textSelection.GetTextParts())
	{
		//Sets highlight color
		textPart.Font.HighlightColor = ColorObject.Yellow;
	}
}
//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Output";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });
//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();
//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Opens an existing presentation.           
FileStream inputStream = new FileStream("Sample.pptx", FileMode.Open);
using (IPresentation pptxDoc = Presentation.Open(inputStream))
{
	ISlide slide = pptxDoc.Slides[0];
	//Finds all the occurrences of a particular text in the specific slide
	ITextSelection[] textSelections = slide.FindAll("product", false, false);
	foreach (ITextSelection textSelection in textSelections)
	{
		//Gets the found text containing text parts
		foreach (ITextPart textPart in textSelection.GetTextParts())
		{
			//Sets highlight color
			textPart.Font.HighlightColor = ColorObject.Yellow;
		}
	}
	//Save the PowerPoint Presentation as stream
	FileStream outputStream = new FileStream("Output.pptx", FileMode.Create);
	pptxDoc.Save(outputStream);
	//Release all resources of the stream
	outputStream.Dispose();
	//Closes the Presentation instance
	pptxDoc.Close();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
 //"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Sample.pptx");
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);
ISlide slide = pptxDoc.Slides[0];
//Finds all the occurrences of a particular text in the specific slide
ITextSelection[] textSelections = slide.FindAll("product", false, false);
foreach (ITextSelection textSelection in textSelections)
{
	//Gets the found text containing text parts
	foreach (ITextPart textPart in textSelection.GetTextParts())
	{
		//Sets highlight color
		textPart.Font.HighlightColor = ColorObject.Yellow;
	}
}
//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();
//Save Presentation in stream format.
pptxDoc.Save(stream);
//Close the presentation
pptxDoc.Close();
stream.Position = 0;
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
	Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
	Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
{% endhighlight %}

{% endtabs %}
