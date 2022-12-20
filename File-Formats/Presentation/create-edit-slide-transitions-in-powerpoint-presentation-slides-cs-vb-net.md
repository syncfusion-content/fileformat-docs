---
title: Add and edit transitions in PowerPoint slides | Syncfusion |
description: Code examples to create and edit PowerPoint slide transitions in .NET, C#, web, ASP.NET, UWP, MVC, Xamarin and .NET Core
platform: file-formats
control: Syncfusion PowerPoint presentation
documentation: 
keywords: PowerPoint, slide, format-table, pptx, transitions
---

# Add and edit transitions in PowerPoint slides

Slide transitions are the motion effects that occur when you move from one slide to the next during a slide show presentation. A transition can be simple as push type that pushes to the next slide or an airplane type that displays the next slide like an eye-catching effect. You can control the speed, add sound, and customize the properties of transition effects. Transition effects can be grouped into three categories.

1. Subtle
2. Exciting
3. Dynamic Content

Transition effect contains the following properties. This makes slide transition more flexible and interactive. 
 
1. Start (after a click or after certain time)
2. Duration 
3. Speed 

## Set a transition effect to a PowerPoint slide

The following code example demonstrates how to set a transition effect to a PowerPoint slide.

{% tabs %}
{% highlight c# tabtitle="C#" %}
//Create a PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();
//Add a blank slide to the presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Add a shape to the slide
IShape cubeShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300);
//Set the transition effect type 
slide.SlideTransition.TransitionEffect = TransitionEffect.Checkerboard;
//Set the transition effect options
slide.SlideTransition.TransitionEffectOption = TransitionEffectOption.Across;
//Save the presentation
pptxDoc.Save("Sample.pptx");
//Close the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Create a PowerPoint presentation
Dim pptxDoc As IPresentation = Presentation.Create()
'Add a blank slide to the presentation
Dim slide As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank)
'Add a shape to the slide
Dim cubeShape As IShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300)
'Set the transition effect type
slide.SlideTransition.TransitionEffect = TransitionEffect.Checkerboard
'Set the transition effect option
slide.SlideTransition.TransitionEffectOption = TransitionEffectOption.Across
'Save the presentation
pptxDoc.Save("Sample.pptx")
'Close the presentation
pptxDoc.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Create a PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();
//Add a blank slide to the presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Add a shape to the slide
IShape cubeShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300);
//Set the transition effect type 
slide.SlideTransition.TransitionEffect = TransitionEffect.Checkerboard;
//Set the transition effect options
slide.SlideTransition.TransitionEffectOption = TransitionEffectOption.Across;
//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Sample";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });
//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();
//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Create a PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();
//Add a blank slide to the presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Add a shape to the slide
IShape cubeShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300);
//Set the transition effect type 
slide.SlideTransition.TransitionEffect = TransitionEffect.Checkerboard;
//Set the transition effect options
slide.SlideTransition.TransitionEffectOption = TransitionEffectOption.Across;
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream(OutputFileName, FileMode.Create);
pptxDoc.Save(outputStream);
//Close the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Create a PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();
//Add a blank slide to the presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Add a shape to the slide
IShape cubeShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300);
//Set the transition effect type 
slide.SlideTransition.TransitionEffect = TransitionEffect.Checkerboard;
//Set the transition effect options
slide.SlideTransition.TransitionEffectOption = TransitionEffectOption.Across;
//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();
//Save Presentation in stream format.
pptxDoc.Save(stream);
//Close the presentation
pptxDoc.Close();
stream.Position = 0;
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Sample.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Sample.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
{% endhighlight %}

{% endtabs %}

## Modify a transition effect applied to a PowerPoint slide

You can edit the transition effects that already applied to the PowerPoint slides. Refer to the following code example.

{% tabs %}
{% highlight c# tabtitle="C#" %}
//Open an existing PowerPoint presentation
IPresentation pptxDoc = Presentation.Open("Sample.pptx");
//Retrieve the first slide from the presentation
ISlide slide = pptxDoc.Slides[0];
//Modify the transition effect applied to the slide
slide.SlideTransition.TransitionEffect = TransitionEffect.Cover;
//Set the transition subtype
slide.SlideTransition.TransitionEffectOption = TransitionEffectOption.Right;
//Save the presentation
pptxDoc.Save("Transition.pptx");
//Close the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Open an existing PowerPoint presentation
Dim pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
'Retrieve the first slide from the presentation
Dim slide As ISlide = pptxDoc.Slides(0)
'Modify the transition effect applied to the slide
slide.SlideTransition.TransitionEffect = TransitionEffect.Cover
'Set the transition subtype
slide.SlideTransition.TransitionEffectOption = TransitionEffectOption.Right
'Save the presentation
pptxDoc.Save("Transition.pptx")
'Close the presentation
pptxDoc.Close()
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
/Retrieve the first slide from the presentation
ISlide slide = pptxDoc.Slides[0];
//Modify the transition effect applied to the slide
slide.SlideTransition.TransitionEffect = TransitionEffect.Cover;
//Set the transition subtype
slide.SlideTransition.TransitionEffectOption = TransitionEffectOption.Right;
//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Transition";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });
//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();
//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream("Sample.pptx",FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);
//Retrieve the first slide from the presentation
ISlide slide = pptxDoc.Slides[0];
//Modify the transition effect applied to the slide
slide.SlideTransition.TransitionEffect = TransitionEffect.Cover;
//Set the transition subtype
slide.SlideTransition.TransitionEffectOption = TransitionEffectOption.Right;
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Transition.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
//Close the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("Sample.pptx");
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);
//Retrieve the first slide from the presentation
ISlide slide = pptxDoc.Slides[0];
//Modify the transition effect applied to the slide
slide.SlideTransition.TransitionEffect = TransitionEffect.Cover;
//Set the transition subtype
slide.SlideTransition.TransitionEffectOption = TransitionEffectOption.Right;
//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();
//Save Presentation in stream format.
pptxDoc.Save(stream);
//Close the presentation
pptxDoc.Close();
stream.Position = 0;
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Transition.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Transition.pptx"", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
{% endhighlight %}

{% endtabs %}

## Set the transition duration

You can set the transition duration value up to 59 seconds. This specifies the length of the slide transition to happen. Refer to the following code example.

{% tabs %}
{% highlight c# tabtitle="C#" %}
//Create a PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();
//Add a blank slide to the presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Add a shape to the slide
IShape cubeShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300);
//Set the transition effect type
slide.SlideTransition.TransitionEffect = TransitionEffect.Checkerboard;
// Set the duration in seconds for the transition effect. Maximum duration value is 59 seconds
slide.SlideTransition.Duration = 40;
//Save the presentation
pptxDoc.Save("Transition.pptx");
//Close the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Create a PowerPoint presentation
Dim pptxDoc As IPresentation = Presentation.Create()
'Add a blank slide to the presentation
Dim slide As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank)
'Add a shape to the slide
Dim cubeShape As IShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300)
'Add a shape to the slide
slide.SlideTransition.TransitionEffect = TransitionEffect.Checkerboard
'Set the duration value(sec) for the transition effect. Max duration value is 59 seconds
slide.SlideTransition.Duration = 40
'Save the presentation
pptxDoc.Save("Transition.pptx")
'Close the presentation
pptxDoc.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Create a PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();
//Add a blank slide to the presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Add a shape to the slide
IShape cubeShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300);
//Set the transition effect type
slide.SlideTransition.TransitionEffect = TransitionEffect.Checkerboard;
// Set the duration in seconds for the transition effect. Maximum duration value is 59 seconds
slide.SlideTransition.Duration = 40;
//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Transition";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });
//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();
//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Create a PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();
//Add a blank slide to the presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Add a shape to the slide
IShape cubeShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300);
//Set the transition effect type
slide.SlideTransition.TransitionEffect = TransitionEffect.Checkerboard;
// Set the duration in seconds for the transition effect. Maximum duration value is 59 seconds
slide.SlideTransition.Duration = 40;
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Transition.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
//Close the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Create a PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();
//Add a blank slide to the presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Add a shape to the slide
IShape cubeShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300);
//Set the transition effect type
slide.SlideTransition.TransitionEffect = TransitionEffect.Checkerboard;
// Set the duration in seconds for the transition effect. Maximum duration value is 59 seconds
slide.SlideTransition.Duration = 40;
//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();
//Save Presentation in stream format.
pptxDoc.Save(stream);
//Close the presentation
pptxDoc.Close();
stream.Position = 0;
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Transition.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Transition.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
{% endhighlight %}

{% endtabs %}

## Set the transition delay

You can set the transition delay in seconds. This delays the next transactions to happen for a certain number of seconds.  The following example demonstrates how to apply the time delay.

{% tabs %}
{% highlight c# tabtitle="C#" %}
//Create a PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();
//Add a blank slide to the presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Add a shape to the slide
IShape cubeShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300);
//Set the transition effect type
slide.SlideTransition.TransitionEffect = TransitionEffect.Checkerboard;
//Enable the transition time delay
slide.SlideTransition.TriggerOnTimeDelay = true;
//Assign the value for the advance time delay in seconds
slide.SlideTransition.TimeDelay = 5;
//Save the presentation
pptxDoc.Save("Sample.pptx");
//Close the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Create a PowerPoint presentation
Dim pptxDoc As IPresentation = Presentation.Create()
'Add a blank slide to the presentation
Dim slide As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank)
'Add a shape to the slide
Dim cubeShape As IShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300)
'Set the transition effect type
slide.SlideTransition.TransitionEffect = TransitionEffect.Checkerboard
'Enable the transition time delay
slide.SlideTransition.TriggerOnTimeDelay = True
'Assign the value for the advance time delay in seconds
slide.SlideTransition.TimeDelay = 5
'Save the presentation
pptxDoc.Save("Sample.pptx")
'Close the presentation
pptxDoc.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Create a PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();
//Add a blank slide to the presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Add a shape to the slide
IShape cubeShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300);
//Set the transition effect type
slide.SlideTransition.TransitionEffect = TransitionEffect.Checkerboard;
//Enable the transition time delay
slide.SlideTransition.TriggerOnTimeDelay = true;
//Assign the value for the advance time delay in seconds
slide.SlideTransition.TimeDelay = 5;
//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Sample";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });
//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();
//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Create a PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();
//Add a blank slide to the presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Add a shape to the slide
IShape cubeShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300);
//Set the transition effect type
slide.SlideTransition.TransitionEffect = TransitionEffect.Checkerboard;
//Enable the transition time delay
slide.SlideTransition.TriggerOnTimeDelay = true;
//Assign the value for the advance time delay in seconds
slide.SlideTransition.TimeDelay = 5;
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Sample.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
//Close the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Create a PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();
//Add a blank slide to the presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Add a shape to the slide
IShape cubeShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300);
//Set the transition effect type
slide.SlideTransition.TransitionEffect = TransitionEffect.Checkerboard;
//Enable the transition time delay
slide.SlideTransition.TriggerOnTimeDelay = true;
//Assign the value for the advance time delay in seconds
slide.SlideTransition.TimeDelay = 5;
//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();
//Save Presentation in stream format.
pptxDoc.Save(stream);
//Close the presentation
pptxDoc.Close();
stream.Position = 0;
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Sample.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Sample.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
{% endhighlight %}

{% endtabs %}

## Set the trigger mode for the transition

The next slide transition can be triggered by the following two ways:

1. Mouse clicks - Brings the next slide to the view.
2. Setting a time - Brings the next slide after that specified time without any interactions.

Syncfusion PowerPoint library allows you to set both the previously given trigger modes while using PowerPoint slide transitions. Refer to the following code example.

{% tabs %}
{% highlight c# tabtitle="C#" %}
//Create a PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();
//Add a blank slide to the presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Add a shape to the slide
IShape cubeShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300);
//Set the transition effect type
slide.SlideTransition.TransitionEffect = TransitionEffect.Checkerboard;
//Set transition advance on click to true. This will enable the next transition after a click
slide.SlideTransition.TriggerOnClick = true;
//Save the presentation
pptxDoc.Save("Sample.pptx");
//Close the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Create a PowerPoint presentation
Dim pptxDoc As IPresentation = Presentation.Create()
'Add a blank slide to the presentation
Dim slide As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank)
'Add a shape to the slide
Dim cubeShape As IShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300)
'Set the transition effect type
slide.SlideTransition.TransitionEffect = TransitionEffect.Checkerboard
'Set transition advance on click to true. This will enable the next transition after a click
slide.SlideTransition.TriggerOnClick = True
'Save the presentation
pptxDoc.Save("Sample.pptx")
'Close the presentation
pptxDoc.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Create a PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();
//Add a blank slide to the presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Add a shape to the slide
IShape cubeShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300);
//Set the transition effect type
slide.SlideTransition.TransitionEffect = TransitionEffect.Checkerboard;
//Set transition advance on click to true. This will enable the next transition after a click
slide.SlideTransition.TriggerOnClick = true;
//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Sample";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });
//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();
//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Create a PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();
//Add a blank slide to the presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Add a shape to the slide
IShape cubeShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300);
//Set the transition effect type
slide.SlideTransition.TransitionEffect = TransitionEffect.Checkerboard;
//Set transition advance on click to true. This will enable the next transition after a click
slide.SlideTransition.TriggerOnClick = true;
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Sample.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
//Close the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Create a PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();
//Add a blank slide to the presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Add a shape to the slide
IShape cubeShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300);
//Set the transition effect type
slide.SlideTransition.TransitionEffect = TransitionEffect.Checkerboard;
//Set transition advance on click to true. This will enable the next transition after a click
slide.SlideTransition.TriggerOnClick = true;
//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();
//Save Presentation in stream format.
pptxDoc.Save(stream);
//Close the presentation
pptxDoc.Close();
stream.Position = 0;
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Sample.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Sample.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
{% endhighlight %}

{% endtabs %}

## Set the speed for transition effect

The speed is the customized property provided by Syncfusion PowerPoint library to set the transition duration mentioned [above](/file-formats/presentation/create-edit-slide-transitions-in-powerpoint-presentation-slides-cs-vb-net#set-the-transition-duration) (in this page) to a customized enumeration values. By default, each transition will happen for 2 seconds. You can change the following enumeration values to change the duration of a slide transition:

1. Default       - 2 seconds
2. Fast          - 0.5 seconds
3. Slow          - 1.0 seconds
4. Medium        - 0.75 seconds

{% tabs %}
{% highlight c# tabtitle="C#" %}
//Create a PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();
//Add a blank slide to the presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Add a shape to the slide
IShape cubeShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300);
//Set the transition effect type
slide.SlideTransition.TransitionEffect = TransitionEffect.Checkerboard;
//Set the transition effect speed enumeration. This will reduce the transition duration to 0.75 seconds from the default 2 second
slide.SlideTransition.Speed = TransitionSpeed.Medium;
//Save the presentation
pptxDoc.Save("Sample.pptx");
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Create a PowerPoint presentation
Dim pptxDoc As IPresentation = Presentation.Create()
'Add a blank slide to the presentation
Dim slide As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank)
'Add a shape to the slide
Dim cubeShape As IShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300)
'Set the transition effect type
slide.SlideTransition.TransitionEffect = TransitionEffect.Checkerboard
'Set the transition effect speed enumeration. This will reduce the transition duration to 0.75 seconds from the default 2 seconds
slide.SlideTransition.Speed = TransitionSpeed.Medium
'Save the presentation
pptxDoc.Save("Sample.pptx")
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Create a PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();
//Add a blank slide to the presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Add a shape to the slide
IShape cubeShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300);
//Set the transition effect type
slide.SlideTransition.TransitionEffect = TransitionEffect.Checkerboard;
//Set the transition effect speed enumeration. This will reduce the transition duration to 0.75 seconds from the default 2 second
slide.SlideTransition.Speed = TransitionSpeed.Medium;
//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Sample";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });
//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();
//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Create a PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();
//Add a blank slide to the presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Add a shape to the slide
IShape cubeShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300);
//Set the transition effect type
slide.SlideTransition.TransitionEffect = TransitionEffect.Checkerboard;
//Set the transition effect speed enumeration. This will reduce the transition duration to 0.75 seconds from the default 2 second
slide.SlideTransition.Speed = TransitionSpeed.Medium;
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Sample.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Create a PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();
//Add a blank slide to the presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Add a shape to the slide
IShape cubeShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300);
//Set the transition effect type
slide.SlideTransition.TransitionEffect = TransitionEffect.Checkerboard;
//Set the transition effect speed enumeration. This will reduce the transition duration to 0.75 seconds from the default 2 second
slide.SlideTransition.Speed = TransitionSpeed.Medium;
//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();
//Save Presentation in stream format.
pptxDoc.Save(stream);
//Close the presentation
pptxDoc.Close();
stream.Position = 0;
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Sample.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Sample.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
{% endhighlight %}

{% endtabs %}

## Supported transition effect types:

The following are the  list of transition effect options that can be applied to each transition effects.

<table>
<tr>
<td>
{{'**S.No**'| markdownify }}
</td>
<td>
{{'**Effects**'| markdownify }}
</td>
<td>
{{'**Effect Options**'| markdownify }}
</td>
</tr>
<tr>
<td>
1
</td>
<td>
Airplane
</td>
<td>
<li> Left </li>
<li> Right </li>
</td>
</tr>
<tr>
<td>
2
</td>
<td>
Blinds
</td>
<td>
<li> Horizontal </li>
<li> Vertical </li>
</td>
</tr>
<tr>
<td>
3
</td>
<td>
Box
</td>
<td>
<li> Left </li> 
<li> Right </li> 
<li> Up </li> 
<li> Down </li> 
</td>
</tr>
<tr>
<td>
4
</td>
<td>
Checkerboard
</td>
<td>
<li> Across </li> 
<li> Down </li> 
</td>
</tr>
<tr>
<td>
5
</td>
<td>
Circle
</td>
<td>
None
</td>
</tr>
<tr>
<td>
6
</td>
<td>
Comb
</td>
<td>
<li> Horizontal </li> 
<li> Vertical </li> 
</td>
</tr>
<tr>
<td>
7
</td>
<td>
Conveyor
</td>
<td>
<li> Left </li> 
<li> Right </li> 
</td>
</tr>
<tr>
<td>
8
</td>
<td>
Cover
</td>
<td>
<li> Left </li>
<li> Right </li>
<li> Up </li>
<li> Down </li>
<li> LeftUp </li>
<li> LeftDown </li>
<li> RightUp </li>
<li> RightDown </li>
</td>
</tr>
<tr>
<td>
9
</td>
<td>
Crush
</td>
<td>
None
</td>
</tr>
<tr>
<td>
10
</td>
<td>
Cube
</td>
<td>
<li> Left </li>
<li> Right </li>
<li> Up </li>
<li> Down </li>
</td>
</tr>
<tr>
<td>
11
</td>
<td>
Curtains
</td>
<td>
None
</td>
</tr>
<tr>
<td>
12
</td>
<td>
Cut
</td>
<td>
<li> None </li>
<li> ThroughBlack </li>
</td>
</tr>
<tr>
<td>
13
</td>
<td>
Diamond
</td>
<td>
None
</td>
</tr>
<tr>
<td>
14
</td>
<td>
Dissolve
</td>
<td>
None
</td>
</tr>
<tr>
<td>
15
</td>
<td>
Doors
</td>
<td>
<li> Horizontal </li> 
<li> Vertical </li> 
</td>
</tr>
<tr>
<td>
16
</td>
<td>
Drape
</td>
<td>
<li> Left </li> 
<li> Right </li>
</td>
</tr>
<tr>
<td>
17
</td>
<td>
FadeAway
</td>
<td>
<li> Smoothly </li>
<li> ThroughBlack </li>
</td>
</tr>
<tr>
<td>
18
</td>
<td>
FallOver
</td>
<td>
<li> Left </li>
<li> Right </li>
</td>
</tr>
<tr>
<td>
19
</td>
<td>
FerrisWheel
</td>
<td>
<li> Left </li>
<li> Right </li>
</td>
</tr>
<tr>
<td>
20
</td>
<td>
Flashbulb
</td>
<td>
None
</td>
</tr>
<tr>
<td>
21
</td>
<td>
Flip
</td>
<td>
<li> Left </li>
<li> Right </li>
</td>
</tr>
<tr>
<td>
22
</td>
<td>
FlyThrough
</td>
<td>
<li> In </li>
<li> Out </li>
<li> InBounce </li>
<li> OutBounce </li>
</td>
</tr>
<tr>
<td>
23
</td>
<td>
Fracture
</td>
<td>
None
</td>
</tr>
<tr>
<td>
24
</td>
<td>
Gallery
</td>
<td>
<li> Left </li>
<li> Right </li>
</td>
</tr>
<tr>
<td>
25
</td>
<td>
GlitterDiamond
</td>
<td>
<li> Left </li>
<li> Right </li>
<li> Up </li>
<li> Down </li>
</td>
</tr>
<tr>
<td>
26
</td>
<td>
GlitterHexagon
</td>
<td>
<li> Left </li>
<li> Right </li>
<li> Up </li>
<li> Down </li>
</td>
</tr>
<tr>
<td>
27
</td>
<td>
Honeycomb
</td>
<td>
None
</td>
</tr>
<tr>
<td>
28
</td>
<td>
Morph
</td>
<td>
<li> ByObject </li>
<li> ByWord </li>
ByChar
</td>
</tr>
<tr>
<td>
29
</td>
<td>
Newsflash
</td>
<td>
None
</td>
</tr>
<tr>
<td>
30
</td>
<td>
Orbit
</td>
<td>
<li> Left </li>
<li> Right </li>
<li> Up </li>
<li> Down </li>
</td>
</tr>
<tr>
<td>
31
</td>
<td>
Origami
</td>
<td>
<li> Left </li>
<li> Right </li>
</td>
</tr>
<tr>
<td>
32
</td>
<td>
PageCurlDouble
</td>
<td>
<li> Left </li>
<li> Right </li>
</td>
</tr>
<tr>
<td>
33
</td>
<td>
PageCurlSingle
</td>
<td>
<li> Left </li>
<li> Right </li>
</td>
</tr>
<tr>
<td>
34
</td>
<td>
Pan
</td>
<td>
<li> Left </li>
<li> Right </li>
<li> Up </li>
<li> Down </li>
</td>
</tr>
<tr>
<td>
35
</td>
<td>
PeelOff
</td>
<td>
<li> Left </li>
<li> Right </li>
</td>
</tr>
<tr>
<td>
36
</td>
<td>
Plus
</td>
<td>
None
</td>
</tr>
<tr>
<td>
37
</td>
<td>
Prestige
</td>
<td>
None
</td>
</tr>
<tr>
<td>
38
</td>
<td>
Push
</td>
<td>
<li> Left </li>
<li> Right </li>
<li> Up </li>
<li> Down </li>
</td>
</tr>
<tr>
<td>
39
</td>
<td>
Random
</td>
<td>
None
</td>
</tr>
<tr>
<td>
40
</td>
<td>
RandomBars
</td>
<td>
<li> Horizontal </li>
<li> Vertical </li>
</td>
</tr>
<tr>
<td>
41
</td>
<td>
Reveal
</td>
<td>
<li> SmoothLeft </li>
<li> SmoothRight </li>
<li> BlackLeft </li>
<li> BlackRight </li>
</td>
</tr>
<tr>
<td>
42
</td>
<td>
Ripple
</td>
<td>
<li> Center </li>
<li> RightUp </li>
<li> RightDown </li>
<li> LeftUp </li>
<li> LeftDown </li>
</td>
</tr>
<tr>
<td>
43
</td>
<td>
Rotate
</td>
<td>
<li> Left </li>
<li> Right </li>
<li> Up </li>
<li> Down </li>
</td>
</tr>
<tr>
<td>
44
</td>
<td>
Shred
</td>
<td>
<li> StripsIn </li>
<li> StripsOut </li>
<li> RectangleIn </li>
<li> RectangleOut </li>
</td>
</tr>
<tr>
<td>
45
</td>
<td>
Split
</td>
<td>
<li> HorizontalIn </li>
<li> HorizontalOut </li>
<li> VerticalIn </li>
<li> VerticalOut </li>
</td>
</tr>
<tr>
<td>
46
</td>
<td>
Strips
</td>
<td>
<li> LeftDown </li>
<li> LeftUp </li>
<li> RightDown </li>
<li> RightUp </li>
</td>
</tr>
<tr>
<td>
47
</td>
<td>
Switch
</td>
<td>
<li> Left </li>
<li> Right </li>
</td>
</tr>
<tr>
<td>
48
</td>
<td>
Uncover
</td>
<td>
<li> Left </li>
<li> Right </li>
<li> Up </li>
<li> Down </li>
<li> LeftDown </li>
<li> LeftUp </li>
<li> RightDown </li>
<li> RightUp </li>
</td>
</tr>
<tr>
<td>
49
</td>
<td>
Vortex
</td>
<td>
<li> Left </li>
<li> Right </li>
<li> Up </li>
<li> Down </li>
</td>
</tr>
<tr>
<td>
50
</td>
<td>
Warp
</td>
<td>
<li> In </li>
<li> Out </li>
</td>
</tr>
<tr>
<td>
51
</td>
<td>
Wedge
</td>
<td>
None
</td>
</tr>
<tr>
<td>
52
</td>
<td>
Wheel
</td>
<td>
<li> Spoke1 </li>
<li> Spoke2 </li>
<li> Spoke3 </li>
<li> Spoke4 </li>
<li> Spoke8 </li>
<li> Reverse1Spoke </li>
</td>
</tr>
<tr>
<td>
53
</td>
<td>
Wind
</td>
<td>
<li> Left </li>
<li> Right </li>
</td>
</tr>
<tr>
<td>
54
</td>
<td>
Window
</td>
<td>
<li> Horizontal </li>
<li> Vertical </li>
</td>
</tr>
<tr>
<td>
55
</td>
<td>
Wipe
</td>
<td>
<li> Left </li>
<li> Right </li>
<li> Up </li>
<li> Down </li>
</td>
</tr>
<tr>
<td>
56
</td>
<td>
Zoom
</td>
<td>
<li> In </li>
<li> Out </li>
</td>
</tr>
</table>
