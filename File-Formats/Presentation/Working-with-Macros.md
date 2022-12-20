---
title: Create and edit macros in PowerPoint files | Syncfusion |
description: Learn here all about working with macros in Syncfusion Essential PowerPoint Presentation Library and more.
platform: file-formats
control: Presentation
documentation: UG
---
# Working with Macros in PowerPoint Presentation Library

A macro is a series of commands that can be grouped together as a single command to automate a frequently used tasks. Macros can be created for Microsoft PowerPoint using Visual Basic for Applications (VBA). Please refer [Create Macros in PowerPoint](https://support.office.com/en-us/article/Create-a-macro-in-PowerPoint-5b07aff6-4dc9-462f-8fc9-66b4c5344e7e?ui=en-US&rs=en-US&ad=US) for more details

Macros enabled PowerPoint presentations of file types - .PPTM and .POTM can only be preserved using Essential Presentation.

## Loading and Saving Macro enabled Presentation

The following code illustrates how to load and save a macro enabled presentation.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Opens an existing macro enabled PowerPoint presentation
IPresentation pptxDoc = Presentation.Open("Sample.PPTM");
//Adds a blank slide to the presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Adds a text box to the slide
IParagraph paragraph = slide.Shapes.AddTextBox(100, 100, 300, 80).TextBody.AddParagraph("Preserve Macros");
//Saves the presentation
pptxDoc.Save("Output.PPTM");
//Closes the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Opens an existing macro enabled PowerPoint presentation
Dim pptxDoc As IPresentation = Presentation.Open("Sample.PPTM")
'Adds a blank slide to the presentation
Dim slide As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank)
'Adds a text box to the slide
Dim paragraph As IParagraph = slide.Shapes.AddTextBox(100, 100, 300, 80).TextBody.AddParagraph("Preserve Macros")
'Saves the presentation
pptxDoc.Save("Output.PPTM")
'Closes the presentation
pptxDoc.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".PPTM");
//Creates a storage file from FileOpenPicker
StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc= await Presentation.OpenAsync(inputStorageFile);
//Adds a blank slide to the presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Adds a text box to the slide
IParagraph paragraph = slide.Shapes.AddTextBox(100, 100, 300, 80).TextBody.AddParagraph("Preserve Macros");
//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Output";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".PPTM" });
//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();
//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Opens an existing macro enabled PowerPoint presentation
FileStream inputStream = new FileStream("Sample.PPTM",FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);
//Adds a blank slide to the presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Adds a text box to the slide
IParagraph paragraph = slide.Shapes.AddTextBox(100, 100, 300, 80).TextBody.AddParagraph("Preserve Macros");
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Output.PPTM", FileMode.Create);
pptxDoc.Save(outputStream);
//Closes the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Opens an existing macro enabled PowerPoint presentation
IPresentation pptxDoc = Presentation.Open(inputStream);
//Adds a blank slide to the presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Adds a text box to the slide
IParagraph paragraph = slide.Shapes.AddTextBox(100, 100, 300, 80).TextBody.AddParagraph("Preserve Macros");
//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();
//Save Presentation in stream format.
pptxDoc.Save(stream);
//Close the presentation
pptxDoc.Close();
stream.Position = 0;
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.PPTM", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.PPTM", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
{% endhighlight %}

{% endtabs %}

## Removing Macros from Macro enabled Presentation

The following code example illustrates how to remove the macros present in the presentation,

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Opens an existing macro enabled PowerPoint presentation
IPresentation pptxDoc = Presentation.Open("Sample.PPTM");
//Checks whether the presentation has macros and then removes them
if (pptxDoc.HasMacros)
    pptxDoc.RemoveMacros();
//Saves the presentation
pptxDoc.Save("Output.pptx");
//Closes the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Opens an existing macro enabled PowerPoint presentation
Dim pptxDoc As IPresentation = Presentation.Open("Sample.PPTM")
'Checks whether the presentation has macros and then removes them
If pptxDoc.HasMacros Then
    pptxDoc.RemoveMacros()
End If
'Saves the presentation
pptxDoc.Save("Output.pptx")
'Closes the presentation
pptxDoc.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".PPTM");
//Creates a storage file from FileOpenPicker
StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();
//Loads or open an Macro enabled PowerPoint Presentation
IPresentation pptxDoc= await Presentation.OpenAsync(inputStorageFile);
//Checks whether the presentation has macros and then removes them
if (pptxDoc.HasMacros)
    pptxDoc.RemoveMacros();
//Saves the presentation
pptxDoc.Save("Output.pptx");
//Closes the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Opens an existing macro enabled PowerPoint presentation
FileStream inputStream = new FileStream("Sample.PPTM",FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);
//Checks whether the presentation has macros and then removes them
if (pptxDoc.HasMacros)
    pptxDoc.RemoveMacros();
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Output.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
//Closes the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Sample.PPTM");
//Opens an existing macro enabled PowerPoint presentation
IPresentation pptxDoc = Presentation.Open(inputStream);
//Checks whether the presentation has macros and then removes them
if (pptxDoc.HasMacros)
    pptxDoc.RemoveMacros();
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

