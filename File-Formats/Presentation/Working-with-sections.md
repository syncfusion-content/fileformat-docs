---
title: Working with sections in PowerPoint Presentation | Syncfusion |
description: Learn here all about working with sections in the Syncfusion PowerPoint Presentation Library and more.
platform: file-formats
control: Presentation
documentation: UG
keywords: sections in PowerPoint presentation
---
# Working with Sections in PowerPoint Library

[Sections](https://help.syncfusion.com/cr/file-formats/Syncfusion.Presentation.IPresentation.html#Syncfusion_Presentation_IPresentation_Sections) helps to manage the slides of a PowerPoint presentation. If a presentation has many slides, you can organize the slides using sections to make the navigation easier.

## Creating a section 

### Adding a new slide to a section

The following code example demonstrates how to add a blank slide to a section.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Creates a PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();
//Adds a section to the PowerPoint presentation
ISection section = pptxDoc.Sections.Add();
//Sets a name to the created section
section.Name = "SectionDemo";
//Adds a slide to the created section
ISlide slide = section.AddSlide(SlideLayoutType.Blank);
//Adds a text box to the slide
slide.AddTextBox(10, 10, 100, 100).TextBody.AddParagraph("Slide in SectionDemo");
//Saves the PowerPoint presentation
pptxDoc.Save("Section.pptx");
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Creates a PowerPoint presentation
Dim pptxDoc As IPresentation = Presentation.Create()
'Adds a section to the PowerPoint presentation
Dim section As ISection = pptxDoc.Sections.Add()
'Sets a name to the created section
section.Name = "SectionDemo"
'Adds a slide to the created section
Dim slide As ISlide = section.AddSlide(SlideLayoutType.Blank)
'Adds a text box to the slide
slide.AddTextBox(10, 10, 100, 100).TextBody.AddParagraph("Slide in SectionDemo")
'Saves the PowerPoint presentation
pptxDoc.Save("Section.PPTX")
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Creates a PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();
//Adds a section to the PowerPoint presentation
ISection section = pptxDoc.Sections.Add();
//Sets a name to the created section
section.Name = "SectionDemo";
//Adds a slide to the created section
ISlide slide = section.AddSlide(SlideLayoutType.Blank);
//Adds a text box to the slide
slide.AddTextBox(10, 10, 100, 100).TextBody.AddParagraph("Slide in SectionDemo");
//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Section";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });
//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();
//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Creates a PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();
//Adds a section to the PowerPoint presentation
ISection section = pptxDoc.Sections.Add();
//Sets a name to the created section
section.Name = "SectionDemo";
//Adds a slide to the created section
ISlide slide = section.AddSlide(SlideLayoutType.Blank);
//Adds a text box to the slide
slide.AddTextBox(10, 10, 100, 100).TextBody.AddParagraph("Slide in SectionDemo");
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Section.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Creates a PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();
//Adds a section to the PowerPoint presentation
ISection section = pptxDoc.Sections.Add();
//Sets a name to the created section
section.Name = "SectionDemo";
//Adds a slide to the created section
ISlide slide = section.AddSlide(SlideLayoutType.Blank);
//Adds a text box to the slide
slide.AddTextBox(10, 10, 100, 100).TextBody.AddParagraph("Slide in SectionDemo");
//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();
//Save Presentation in stream format.
pptxDoc.Save(stream);
//Close the presentation
pptxDoc.Close();
stream.Position = 0;
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Section.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Section.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
{% endhighlight %}

{% endtabs %}

### Adding an existing slide to a section

The following code example demonstrates how to add an existing slide to a section.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Loads a PowerPoint presentation
IPresentation pptxDoc = Presentation.Open("PPTXWithoutSection.PPTX");
//Creates a new section in the PowerPoint presentation
pptxDoc.Sections.Add();
//Moves the first slide to the created section
pptxDoc.Slides[0].MoveToSection(0);
//Saves the PowerPoint presentation
pptxDoc.Save("Sections.PPTX");
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Loads a PowerPoint presentation
Dim pptxDoc As IPresentation = Presentation.Open("PPTXWithoutSection.PPTX")
'Creates a new section in the PowerPoint presentation
pptxDoc.Sections.Add()
'Moves the first slide to the created section
pptxDoc.Slides(0).MoveToSection(0)
'Saves the PowerPoint presentation
pptxDoc.Save("Sections.PPTX")
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".pptx");
//Creates a storage file from FileOpenPicker
StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc= await Presentation.OpenAsync(inputStorageFile);
//Creates a new section in the PowerPoint presentation
pptxDoc.Sections.Add();
//Moves the first slide to the created section
pptxDoc.Slides[0].MoveToSection(0);
//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Sections";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });
//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();
//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream("PPTXWithSections.PPTX",FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);
//Creates a new section in the PowerPoint presentation
pptxDoc.Sections.Add();
//Moves the first slide to the created section
pptxDoc.Slides[0].MoveToSection(0);
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Section.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Sample.pptx");
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);
//Creates a new section in the PowerPoint presentation
pptxDoc.Sections.Add();
//Moves the first slide to the created section
pptxDoc.Slides[0].MoveToSection(0);
//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();
//Save Presentation in stream format.
pptxDoc.Save(stream);
//Close the presentation
pptxDoc.Close();
stream.Position = 0;
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Section.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Section.pptx.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
{% endhighlight %}

{% endtabs %}

### Inserting a section

The following code example demonstrates how to insert a section in a template PowerPoint presentation that contains sections

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Loads a PowerPoint presentation
IPresentation pptxDoc = Presentation.Open("PPTXWithSections.PPTX");
//Creates a new section
ISection section = pptxDoc.Sections.Add();
//Names the created section
section.Name = "InsertedSection";
//Inserts the section at second position.
pptxDoc.Sections.Insert(1, section);
//Saves the PowerPoint presentation
pptxDoc.Save("Sections.PPTX");
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Loads a PowerPoint presentation
Dim pptxDoc As IPresentation = Presentation.Open("PPTXWithSections.PPTX")
'Creates a new section
Dim section As ISection = pptxDoc.Sections.Add()
'Names the created section
section.Name = "InsertedSection"
'Inserts the section at second position.
pptxDoc.Sections.Insert(1, section)
'Saves the PowerPoint presentation
pptxDoc.Save("Sections.PPTX")
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".pptx");
//Creates a storage file from FileOpenPicker
StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc= await Presentation.OpenAsync(inputStorageFile);
/Creates a new section
ISection section = pptxDoc.Sections.Add();
//Names the created section
section.Name = "InsertedSection";
//Inserts the section at second position.
pptxDoc.Sections.Insert(1, section);
//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Sections";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });
//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();
//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream("PPTXWithSections.PPTX",FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);
//Creates a new section
ISection section = pptxDoc.Sections.Add();
//Names the created section
section.Name = "InsertedSection";
//Inserts the section at second position.
pptxDoc.Sections.Insert(1, section);
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Section.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Sample.pptx");
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);
//Creates a new section
ISection section = pptxDoc.Sections.Add();
//Names the created section
section.Name = "InsertedSection";
//Inserts the section at second position.
pptxDoc.Sections.Insert(1, section);
//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();
//Save Presentation in stream format.
pptxDoc.Save(stream);
//Close the presentation
pptxDoc.Close();
stream.Position = 0;
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Section.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Section.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
{% endhighlight %}

{% endtabs %}

## Moving the sections within a PowerPoint presentation

You can move the sections within a PowerPoint presentation. The following code example demonstrates how to move a section to a specific position in the navigation pane.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Loads a PowerPoint presentation
IPresentation pptxDoc = Presentation.Open("PPTXWithSections.PPTX");
//Moves the second section to third position within the PowerPoint presentation.
pptxDoc.Sections[2].Move(3);
//Saves the PowerPoint presentation
pptxDoc.Save("Sections.PPTX");
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Loads a PowerPoint presentation
Dim pptxDoc As IPresentation = Presentation.Open("PPTXWithSections.PPTX")
'Moves the second section to third position within the PowerPoint presentation.
pptxDoc.Sections(2).Move(3)
'Saves the PowerPoint presentation
pptxDoc.Save("Sections.PPTX")
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".pptx");
//Creates a storage file from FileOpenPicker
StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc= await Presentation.OpenAsync(inputStorageFile);
//Moves the second section to third position within the PowerPoint presentation.
pptxDoc.Sections[2].Move(3);
//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Sections";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });
//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();
//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream("PPTXWithSections.PPTX",FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);
//Moves the second section to third position within the PowerPoint presentation.
pptxDoc.Sections[2].Move(3);
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Section.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Sample.pptx");
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);
//Moves the second section to third position within the PowerPoint presentation.
pptxDoc.Sections[2].Move(3);
//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();
//Save Presentation in stream format.
pptxDoc.Save(stream);
//Close the presentation
pptxDoc.Close();
stream.Position = 0;
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Section.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Section.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
{% endhighlight %}

{% endtabs %}

## Moving a slide within sections

The following code example demonstrates how to move a slide from one section to another.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Loads a PowerPoint presentation
IPresentation pptxDoc = Presentation.Open("PPTXWithSections.PPTX");
//Gets the first slide of second section in the PowerPoint presentation
ISlide slide = pptxDoc.Sections[1].Slides[0];
//Moves the slide to first section
slide.MoveToSection(0);
//Saves the PowerPoint presentation
pptxDoc.Save("Sections.PPTX");
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Loads a PowerPoint presentation
Dim pptxDoc As IPresentation = Presentation.Open("PPTXWithSections.PPTX")
'Gets the first slide of second section in the PowerPoint presentation
Dim slide As ISlide = pptxDoc.Sections(1).Slides(0)
'Moves the slide to first section
slide.MoveToSection(0)
'Saves the PowerPoint presentation
pptxDoc.Save("Sections.PPTX")
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".pptx");
//Creates a storage file from FileOpenPicker
StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc= await Presentation.OpenAsync(inputStorageFile);
//Gets the first slide of second section in the PowerPoint presentation
ISlide slide = pptxDoc.Sections[1].Slides[0];
//Moves the slide to first section
slide.MoveToSection(0);
//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Sections";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });
//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();
//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream("PPTXWithSections.PPTX",FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);
//Gets the first slide of second section in the PowerPoint presentation
ISlide slide = pptxDoc.Sections[1].Slides[0];
//Moves the slide to first section
slide.MoveToSection(0);
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Section.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Sample.pptx");
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);
//Gets the first slide of second section in the PowerPoint presentation
ISlide slide = pptxDoc.Sections[1].Slides[0];
//Moves the slide to first section
slide.MoveToSection(0);
//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();
//Save Presentation in stream format.
pptxDoc.Save(stream);
//Close the presentation
pptxDoc.Close();
stream.Position = 0;
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Section.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Section.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
{% endhighlight %}

{% endtabs %}

## Cloning and merging the slides in a section

The following code example demonstrates how to clone the slide collection of a section and add those slides to a destination presentation.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Loads a PowerPoint presentation
IPresentation pptxDoc = Presentation.Open("PPTXWithSections.PPTX");
//Clones the slides in 3rd section
ISlides slides = pptxDoc.Sections[2].Clone();
//Creates a destination PowerPoint presentation instance. Existing presentations can also be used here.
pptxDoc = Presentation.Create();
//Iterates the cloned slides and adds the slides to the destination presentation
foreach (ISlide slide in slides)
    pptxDoc.Slides.Add(slide);
//Saves the PowerPoint presentation
pptxDoc.Save("Sections.PPTX");
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Loads a PowerPoint presentation
Dim pptxDoc As IPresentation = Presentation.Open("PPTXWithSections.PPTX")
'Clones the slides in 3rd section
Dim slides As ISlides = pptxDoc.Sections(2).Clone()
'Creates a destination PowerPoint presentation instance. Existing presentations can also be used here.
pptxDoc = Presentation.Create()
'Iterates the cloned slides and adds the slides to the destination presentation
For Each slide As ISlide In slides
    pptxDoc.Slides.Add(slide)
Next
'Save the PowerPoint presentation
pptxDoc.Save("Sections.PPTX")
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".pptx");
//Creates a storage file from FileOpenPicker
StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc= await Presentation.OpenAsync(inputStorageFile);
//Clones the slides in 3rd section
ISlides slides = pptxDoc.Sections[2].Clone();
//Creates a destination PowerPoint presentation instance. Existing presentations can also be used here.
pptxDoc = Presentation.Create();
//Iterates the cloned slides and adds the slides to the destination presentation
foreach (ISlide slide in slides)
    pptxDoc.Slides.Add(slide);
//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Sections";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });
//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();
//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream("PPTXWithSections.PPTX",FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);
//Clones the slides in 3rd section
ISlides slides = pptxDoc.Sections[2].Clone();
//Creates a destination PowerPoint presentation instance. Existing presentations can also be used here.
pptxDoc = Presentation.Create();
//Iterates the cloned slides and adds the slides to the destination presentation
foreach (ISlide slide in slides)
    pptxDoc.Slides.Add(slide);
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Section.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Sample.pptx");
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);
//Clones the slides in 3rd section
ISlides slides = pptxDoc.Sections[2].Clone();
//Creates a destination PowerPoint presentation instance. Existing presentations can also be used here.
pptxDoc = Presentation.Create();
//Iterates the cloned slides and adds the slides to the destination presentation
foreach (ISlide slide in slides)
    pptxDoc.Slides.Add(slide);
//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();
//Save Presentation in stream format.
pptxDoc.Save(stream);
//Close the presentation
pptxDoc.Close();
stream.Position = 0;
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Section.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Section.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
{% endhighlight %}

{% endtabs %}

## Removing a section 

The following code example demonstrates how to create remove a particular section from the sections collection of a presentation.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Loads a PowerPoint presentation
IPresentation pptxDoc = Presentation.Open("PPTXWithSections.PPTX");
//Removes the second section from the PowerPoint presentation
pptxDoc.Sections.Remove(pptxDoc.Sections[1]);
//Saves the PowerPoint presentation
pptxDoc.Save("Sections.PPTX");
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Loads a PowerPoint presentation
Dim pptxDoc As IPresentation = Presentation.Open("PPTXWithSections.PPTX")
'Removes the second section from the PowerPoint presentation
pptxDoc.Sections.Remove(pptxDoc.Sections(1))
'Saves the PowerPoint presentation
pptxDoc.Save("Sections.PPTX")
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".pptx");
//Creates a storage file from FileOpenPicker
StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc= await Presentation.OpenAsync(inputStorageFile);
//Removes the second section from the PowerPoint presentation
pptxDoc.Sections.Remove(pptxDoc.Sections[1]);
//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Sections";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });
//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();
//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream("PPTXWithSections.PPTX",FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);
//Removes the second section from the PowerPoint presentation
pptxDoc.Sections.Remove(pptxDoc.Sections[1]);
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Section.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Sample.pptx");
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);
//Removes the second section from the PowerPoint presentation
pptxDoc.Sections.Remove(pptxDoc.Sections[1]);
//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();
//Save Presentation in stream format.
pptxDoc.Save(stream);
//Close the presentation
pptxDoc.Close();
stream.Position = 0;
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Section.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Section.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
{% endhighlight %}

{% endtabs %}

## Remove all sections 

The following code example demonstrates how to remove section collection from an existing PowerPoint presentation.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Loads a PowerPoint presentation
IPresentation pptxDoc = Presentation.Open("PPTXWithSections.PPTX");
//Removes the sections
pptxDoc.Sections.Clear();
//Saves the PowerPoint presentation
pptxDoc.Save("Sections.PPTX");
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Loads a PowerPoint presentation
Dim pptxDoc As IPresentation = Presentation.Open("PPTXWithSections.PPTX")
'Removes the sections
pptxDoc.Sections.Clear()
'Saves the PowerPoint presentation
pptxDoc.Save("Sections.PPTX")
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".pptx");
//Creates a storage file from FileOpenPicker
StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc= await Presentation.OpenAsync(inputStorageFile);
//Removes the sections
pptxDoc.Sections.Clear();
//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Sections";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });
//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();
//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream("PPTXWithSections.PPTX",FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);
//Removes the sections
pptxDoc.Sections.Clear();
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Sections.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Sample.pptx");
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);
//Removes the sections
pptxDoc.Sections.Clear();
//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();
//Save Presentation in stream format.
pptxDoc.Save(stream);
//Close the presentation
pptxDoc.Close();
stream.Position = 0;
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Sections.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Sections.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
{% endhighlight %}

{% endtabs %}