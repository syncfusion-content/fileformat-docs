---
title: Working with Animations | PowerPoint Library | Syncfusion
description: Learn here all about working with animations of Syncfusion PowerPoint Presentation Library and more.
platform: file-formats
control: Essential Presentation
documentation: UG
keywords: PowerPoint animation, slide animation, shape animation, pptx animation
---
# Working with Animations in PowerPoint Library

Animations are visual effects for the objects in PowerPoint presentation and animation helps to make a PowerPoint presentation more dynamic. Animation effects can be grouped into four categories.,

1. Entrance
2. Emphasis
3. Exit
4. Motion paths

Entrance effects can be set to enter the objects with animations during slide show. Emphasis effects animate the objects on the spot. Exit effects allow objects to leave the slide show with animations. Motion Paths allow objects to move around the slide show. Each effect contains variables such as start (On click, with previous and after previous), delay, speed, repeat, and trigger. This makes animations more flexible and interactive. 

Syncfusion Presentation library allows you to animate the text, pictures, shapes, tables, SmartArt graphics, and charts in PowerPoint presentation.

## Adding animation effect to shapes

Animation effects can be added to shapes, images, tables, charts and SmartArt diagrams. The following code example demonstrates how to add an animation effect to an shape.

{% tabs %}
{% highlight c# %}

//Create an instance for PowerPoint

using (IPresentation pptxDoc = Presentation.Create())

{

//Add a blank slide to Presentation

ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Add normal shape to slide

IShape cubeShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300);

//Access the animation sequence to create effects

ISequence sequence = slide.Timeline.MainSequence;

//Add bounce effect to the shape

IEffect bounceEffect = sequence.AddEffect(cubeShape, EffectType.Bounce, EffectSubtype.None, EffectTriggerType.OnClick);

//Save the Presentation

pptxDoc.Save("Sample.pptx");

}

{% endhighlight %}
{% highlight vb.net %}

'Create an instance for PowerPoint

Using pptxDoc As IPresentation = Presentation.Create()

   'Add a blank slide to Presentation

    Dim slide As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank)

    'Add normal shape to slide

    Dim cubeShape As IShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300)

    'Access the animation sequence to create effects

    Dim sequence As ISequence = slide.Timeline.MainSequence

    'Add bounce effect to the shape

    Dim bounceEffect As IEffect = sequence.AddEffect(cubeShape, EffectType.Bounce, EffectSubtype.None, EffectTriggerType.OnClick)

    'Save the Presentation

    pptxDoc.Save("Sample.pptx")

End Using

{% endhighlight %}

{% highlight UWP %}

//Create an instance of PowerPoint Presentation
IPresentation pptxDoc = Presentation.Create();

//Add a blank slide to Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Add normal shape to slide
IShape cubeShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300);

//Access the animation sequence to create effects
ISequence sequence = slide.Timeline.MainSequence;

//Add bounce effect to the shape
IEffect bounceEffect = sequence.AddEffect(cubeShape, EffectType.Bounce, EffectSubtype.None, EffectTriggerType.OnClick);

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

{% highlight ASP.NET CORE %}

//Create an instance for PowerPoint
IPresentation pptxDoc = Presentation.Create();

//Add a blank slide to Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Add normal shape to slide
IShape cubeShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300);

//Access the animation sequence to create effects
ISequence sequence = slide.Timeline.MainSequence;

//Add bounce effect to the shape
IEffect bounceEffect = sequence.AddEffect(cubeShape, EffectType.Bounce, EffectSubtype.None, EffectTriggerType.OnClick);

//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Sample.pptx", FileMode.Create);
pptxDoc.Save(outputStream);

{% endhighlight %}

{% highlight XAMARIN %}

//Create an instance for PowerPoint
IPresentation pptxDoc = Presentation.Create();

//Add a blank slide to Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Add normal shape to slide
IShape cubeShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300);

//Access the animation sequence to create effects
ISequence sequence = slide.Timeline.MainSequence;

//Add bounce effect to the shape
IEffect bounceEffect = sequence.AddEffect(cubeShape, EffectType.Bounce, EffectSubtype.None, EffectTriggerType.OnClick);

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

## Adding interactive animation

Animations can be interactive when it depends on another slide element., for example, an animation associated with a rectangle is triggered when user clicks an oval shape in the slide. The following code example demonstrates how to set an interactive animation.

{% tabs %}

{% highlight c# %}

//Create an instance for PowerPoint

using (IPresentation pptxDoc = Presentation.Create())

{

//Add a blank slide to Presentation

ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Add normal shape to slide

IShape cubeShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300);

//Add a shape to act as button

IShape buttonShape = slide.Shapes.AddShape(AutoShapeType.Oval, 100,100,50,50);

//Create the interactive sequence to make the animation effects interactive by triggering with button click

ISequence interactiveSequence = slide.Timeline.InteractiveSequences.Add(buttonShape);

//Add Fly effect with top subtype to animate the shape as fly from top

IEffect bounceEffect = interactiveSequence.AddEffect(cubeShape, EffectType.Fly, EffectSubtype.Top, EffectTriggerType.OnClick);

//Save the Presentation

pptxDoc.Save("Sample.pptx");

}

{% endhighlight %}

{% highlight vb.net %}

'Create an instance for PowerPoint

Using pptxDoc As IPresentation = Presentation.Create()

   'Add a blank slide to Presentation

   Dim slide As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank)

   'Add normal shape to slide

   Dim cubeShape As IShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300)

   'Add a shape to act as button

   Dim buttonShape As IShape = slide.Shapes.AddShape(AutoShapeType.Oval, 100, 100, 50, 50)

   'Create the interactive sequence to make the animation effects interactive by triggering with button click

   Dim interactiveSequence As ISequence = slide.Timeline.InteractiveSequences.Add(buttonShape)

   'Add Fly effect with top subtype to animate the shape as fly from top

   Dim bounceEffect As IEffect = interactiveSequence.AddEffect(cubeShape, EffectType.Fly, EffectSubtype.Top, EffectTriggerType.OnClick)

   'Save the Presentation

   pptxDoc.Save("Sample.pptx")

End Using

{% endhighlight %}

{% highlight UWP %}

//Create an instance of PowerPoint Presentation
IPresentation pptxDoc = Presentation.Create();

//Add a blank slide to Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Add normal shape to slide
IShape cubeShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300);

//Add a shape to act as button
IShape buttonShape = slide.Shapes.AddShape(AutoShapeType.Oval, 100,100,50,50);

//Create the interactive sequence to make the animation effects interactive by triggering with button click
ISequence interactiveSequence = slide.Timeline.InteractiveSequences.Add(buttonShape);

//Add Fly effect with top subtype to animate the shape as fly from top
IEffect bounceEffect = interactiveSequence.AddEffect(cubeShape, EffectType.Fly, EffectSubtype.Top, EffectTriggerType.OnClick);

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

{% highlight ASP.NET CORE %}

//Create an instance for PowerPoint
IPresentation pptxDoc = Presentation.Create();

//Add a blank slide to Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Add normal shape to slide
IShape cubeShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300);

//Add a shape to act as button
IShape buttonShape = slide.Shapes.AddShape(AutoShapeType.Oval, 100,100,50,50);

//Create the interactive sequence to make the animation effects interactive by triggering with button click
ISequence interactiveSequence = slide.Timeline.InteractiveSequences.Add(buttonShape);

//Add Fly effect with top subtype to animate the shape as fly from top
IEffect bounceEffect = interactiveSequence.AddEffect(cubeShape, EffectType.Fly, EffectSubtype.Top, EffectTriggerType.OnClick);

//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Sample.pptx", FileMode.Create);
pptxDoc.Save(outputStream);

{% endhighlight %}

{% highlight XAMARIN %}

//Create an instance for PowerPoint
IPresentation pptxDoc = Presentation.Create();

//Add a blank slide to Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Add normal shape to slide
IShape cubeShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300);

//Add a shape to act as button
IShape buttonShape = slide.Shapes.AddShape(AutoShapeType.Oval, 100,100,50,50);

//Create the interactive sequence to make the animation effects interactive by triggering with button click
ISequence interactiveSequence = slide.Timeline.InteractiveSequences.Add(buttonShape);

//Add Fly effect with top subtype to animate the shape as fly from top
IEffect bounceEffect = interactiveSequence.AddEffect(cubeShape, EffectType.Fly, EffectSubtype.Top, EffectTriggerType.OnClick);

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

## Adding animation to text

Animation effects can be applied to text. The following code example demonstrated how to set an animation effect to a text.

{% tabs %}

{% highlight c# %}

//Open an existing Presentation from file system

using (IPresentation pptxDoc = Presentation.Open("Sample.pptx"))

{

//Retrieve the first slide from Presentation

ISlide slide = pptxDoc.Slides[0];

//Retrieve the first shape

IShape shape = slide.Shapes[0] as IShape;

//Access the animation sequence to create effects

ISequence sequence = slide.Timeline.MainSequence;

//Add swivel effect with vertical subtype to the shape, build type is used to represent the animate level of the paragraph

IEffect bounceEffect = sequence.AddEffect(shape, EffectType.Swivel, EffectSubtype.Vertical, EffectTriggerType.OnClick, BuildType.ByLevelParagraphs1);

//Save the Presentation to the file system

pptxDoc.Save("Result.pptx");

}

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing Presentation from file system

Using pptxDoc As IPresentation = Presentation.Open("Sample.pptx")

   'Retrieve the first slide from Presentation

   Dim slide As ISlide = pptxDoc.Slides(0)

   'Retrieve the first shape

   Dim shape As IShape = TryCast(slide.Shapes(0), IShape)

   'Access the animation sequence to create effects

   Dim sequence As ISequence = slide.Timeline.MainSequence

   'Add swivel effect with vertical subtype to the shape, build type is used to represent the animate level of the paragraph

   Dim bounceEffect As IEffect = sequence.AddEffect(shape, EffectType.Swivel, EffectSubtype.Vertical, EffectTriggerType.OnClick, BuildType.ByLevelParagraphs1)

   'Save the Presentation to the file system

   pptxDoc.Save("Result.pptx")

End Using

{% endhighlight %}

{% highlight UWP %}

//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".pptx");

//Creates a storage file from FileOpenPicker
StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();

//Loads or open an PowerPoint Presentation
IPresentation pptxDoc= await Presentation.OpenAsync(inputStorageFile);

//Retrieve the first slide from Presentation
ISlide slide = pptxDoc.Slides[0];

//Retrieve the first shape
IShape shape = slide.Shapes[0] as IShape;

//Access the animation sequence to create effects
ISequence sequence = slide.Timeline.MainSequence;

//Add swivel effect with vertical subtype to the shape, build type is used to represent the animate level of the paragraph
IEffect bounceEffect = sequence.AddEffect(shape, EffectType.Swivel, EffectSubtype.Vertical, EffectTriggerType.OnClick, BuildType.ByLevelParagraphs1);

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

{% highlight ASP.NET CORE %}

//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream("Sample.pptx",FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);

//Retrieve the first slide from Presentation
ISlide slide = pptxDoc.Slides[0];

//Retrieve the first shape
IShape shape = slide.Shapes[0] as IShape;

//Access the animation sequence to create effects
ISequence sequence = slide.Timeline.MainSequence;

//Add swivel effect with vertical subtype to the shape, build type is used to represent the animate level of the paragraph
IEffect bounceEffect = sequence.AddEffect(shape, EffectType.Swivel, EffectSubtype.Vertical, EffectTriggerType.OnClick, BuildType.ByLevelParagraphs1);

//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream(""Result.pptx, FileMode.Create);
pptxDoc.Save(outputStream);

{% endhighlight %}

{% highlight XAMARIN %}

//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Sample.pptx");

//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);

//Retrieve the first slide from Presentation
ISlide slide = pptxDoc.Slides[0];

//Retrieve the first shape
IShape shape = slide.Shapes[0] as IShape;

//Access the animation sequence to create effects
ISequence sequence = slide.Timeline.MainSequence;

//Add swivel effect with vertical subtype to the shape, build type is used to represent the animate level of the paragraph
IEffect bounceEffect = sequence.AddEffect(shape, EffectType.Swivel, EffectSubtype.Vertical, EffectTriggerType.OnClick, BuildType.ByLevelParagraphs1);

//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();

//Save Presentation in stream format.
pptxDoc.Save(stream);

//Close the presentation
pptxDoc.Close();
stream.Position = 0;

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Result.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Result.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);

{% endhighlight %}

{% endtabs %}

## Adding exit animation effect

When you add common animation effects for both entrance and exit types, animation is applied with entrance effect by default. The following code example demonstrates how to set exist type animation for a shape.

{% tabs %}

{% highlight c# %}

//Create an instance for PowerPoint

using (IPresentation pptxDoc = Presentation.Create())

{

//Add a blank slide to Presentation

ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Add normal shape to slide

IShape cubeShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300);

//Access the animation sequence to create effects

ISequence sequence = slide.Timeline.MainSequence;

//Add random bars effect to the shape

IEffect effect = sequence.AddEffect(cubeShape, EffectType.RandomBars, EffectSubtype.None, EffectTriggerType.OnClick);

//Change the preset class type of the effect from default entrance to exit

effect.PresetClassType = EffectPresetClassType.Exit;

//Save the Presentation

pptxDoc.Save("Sample.pptx");

}

{% endhighlight %}

{% highlight vb.net %}

'Create an instance for PowerPoint

Using pptxDoc As IPresentation = Presentation.Create()

   'Add a blank slide to Presentation

   Dim slide As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank)

   'Add normal shape to slide

   Dim cubeShape As IShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300)

   'Access the animation sequence to create effects

   Dim sequence As ISequence = slide.Timeline.MainSequence

   'Add random bars effect to the shape

   Dim effect As IEffect = sequence.AddEffect(cubeShape, EffectType.RandomBars, EffectSubtype.None, EffectTriggerType.OnClick)

   'Change the preset class type of the effect from default entrance to exit

   effect.PresetClassType = EffectPresetClassType.[Exit]

   'Save the Presentation

   pptxDoc.Save("Sample.pptx")

End Using

{% endhighlight %}

{% highlight UWP %}

//Create an instance of PowerPoint Presentation
IPresentation pptxDoc = Presentation.Create();

//Add a blank slide to Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Add normal shape to slide
IShape cubeShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300);

//Access the animation sequence to create effects
ISequence sequence = slide.Timeline.MainSequence;

//Add random bars effect to the shape
IEffect effect = sequence.AddEffect(cubeShape, EffectType.RandomBars, EffectSubtype.None, EffectTriggerType.OnClick);

//Change the preset class type of the effect from default entrance to exit
effect.PresetClassType = EffectPresetClassType.Exit;

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

{% highlight ASP.NET CORE %}

//Create an instance for PowerPoint
IPresentation pptxDoc = Presentation.Create();

//Add a blank slide to Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Add normal shape to slide
IShape cubeShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300);

//Access the animation sequence to create effects
ISequence sequence = slide.Timeline.MainSequence;

//Add random bars effect to the shape
IEffect effect = sequence.AddEffect(cubeShape, EffectType.RandomBars, EffectSubtype.None, EffectTriggerType.OnClick);

//Change the preset class type of the effect from default entrance to exit
effect.PresetClassType = EffectPresetClassType.Exit;

//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Sample.pptx", FileMode.Create);
pptxDoc.Save(outputStream);

{% endhighlight %}

{% highlight XAMARIN %}

//Create an instance for PowerPoint
IPresentation pptxDoc = Presentation.Create();

//Add a blank slide to Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Add normal shape to slide
IShape cubeShape = slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300);

//Access the animation sequence to create effects
ISequence sequence = slide.Timeline.MainSequence;

//Add random bars effect to the shape
IEffect effect = sequence.AddEffect(cubeShape, EffectType.RandomBars, EffectSubtype.None, EffectTriggerType.OnClick);

//Change the preset class type of the effect from default entrance to exit
effect.PresetClassType = EffectPresetClassType.Exit;

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


## Edit existing animation effect

The Presentation library allows you to edit the animations in existing presentations. The following example demonstrates how to modify an existing animation applied to a shape.

{% tabs %}

{% highlight c# %}

//Open an existing Presentation from file system

using (IPresentation pptxDoc = Presentation.Open("Sample.pptx"))

{

//Retrieve the first slide from Presentation

ISlide slide = pptxDoc.Slides[0];

//Retrieve the first shape

IShape shape = slide.Shapes[0] as IShape;

//Access the animation main sequence to modify the effects

ISequence sequence = slide.Timeline.MainSequence;

//Get the animation effects of the particular shape

IEffect[] animationEffects = sequence.GetEffectsByShape(shape);

//Iterate the animation effect to make the change

IEffect animationEffect = animationEffects[0];

//Change the animation effect type from swivel to GrowAndTurn

animationEffect.Type = EffectType.GrowAndTurn;

//Save the Presentation to the file system

pptxDoc.Save("Animation.pptx");

}

{% endhighlight %}

{% highlight vb.net %}

'Open an existing Presentation from file system

Using pptxDoc As IPresentation = Presentation.Open("Sample.pptx")

   'Retrieve the first slide from Presentation

   Dim slide As ISlide = pptxDoc.Slides(0)

   'Retrieve the first shape.

   Dim shape As IShape = TryCast(slide.Shapes(0), IShape)

   'Access the animation main sequence to modify the effects

   Dim sequence As ISequence = slide.Timeline.MainSequence

   'Get the animation effects of the particular shape

   Dim animationEffects As IEffect() = sequence.GetEffectsByShape(shape)

   'Iterate the animation effect to make the change

   Dim animationEffect As IEffect = animationEffects(0)

   'Change the animation effect type from swivel to GrowAndTurn

   animationEffect.Type = EffectType.GrowAndTurn

   'Save the Presentation to the file system

   pptxDoc.Save("Animation.pptx")

End Using

{% endhighlight %}

{% highlight UWP %}

//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".pptx");

//Creates a storage file from FileOpenPicker
StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();

//Loads or open an PowerPoint Presentation
IPresentation pptxDoc= await Presentation.OpenAsync(inputStorageFile);

//Retrieve the first slide from Presentation
ISlide slide = pptxDoc.Slides[0];

//Retrieve the first shape
IShape shape = slide.Shapes[0] as IShape;

//Access the animation main sequence to modify the effects
ISequence sequence = slide.Timeline.MainSequence;

//Get the animation effects of the particular shape
IEffect[] animationEffects = sequence.GetEffectsByShape(shape);

//Iterate the animation effect to make the change
IEffect animationEffect = animationEffects[0];

//Change the animation effect type from swivel to GrowAndTurn
animationEffect.Type = EffectType.GrowAndTurn;

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

{% highlight ASP.NET CORE %}

//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream("Sample.pptx",FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);

//Retrieve the first slide from Presentation
ISlide slide = pptxDoc.Slides[0];

//Retrieve the first shape
IShape shape = slide.Shapes[0] as IShape;

//Access the animation main sequence to modify the effects
ISequence sequence = slide.Timeline.MainSequence;

//Get the animation effects of the particular shape
IEffect[] animationEffects = sequence.GetEffectsByShape(shape);

//Iterate the animation effect to make the change
IEffect animationEffect = animationEffects[0];

//Change the animation effect type from swivel to GrowAndTurn
animationEffect.Type = EffectType.GrowAndTurn;

//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Animation.pptx", FileMode.Create);
pptxDoc.Save(outputStream);

{% endhighlight %}

{% highlight XAMARIN %}

//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Sample.pptx");

//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);

//Retrieve the first slide from Presentation
ISlide slide = pptxDoc.Slides[0];

//Retrieve the first shape
IShape shape = slide.Shapes[0] as IShape;

//Access the animation main sequence to modify the effects
ISequence sequence = slide.Timeline.MainSequence;

//Get the animation effects of the particular shape
IEffect[] animationEffects = sequence.GetEffectsByShape(shape);

//Iterate the animation effect to make the change
IEffect animationEffect = animationEffects[0];

//Change the animation effect type from swivel to GrowAndTurn
animationEffect.Type = EffectType.GrowAndTurn;

//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();

//Save Presentation in stream format.
pptxDoc.Save(stream);

//Close the presentation
pptxDoc.Close();
stream.Position = 0;

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Animation.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Animation.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);

{% endhighlight %}

{% endtabs %}

## Modifying animation effect sub type

Presentation library allows you to edit the sub type of animations effects in existing presentations. The following example demonstrates how to modify a sub type applied to the existing animation.

{% tabs %}

{% highlight c# %}

//Opens an existing Presentation from file system

using (IPresentation pptxDoc = Presentation.Open("Sample.pptx"))

{

//Retrieves the first slide from Presentation

ISlide slide = pptxDoc.Slides[0];

//Retrieves the first shape

IShape shape = slide.Shapes[0] as IShape;

//Access the animation main sequence to modify the effects

ISequence sequence = slide.Timeline.MainSequence;

//Get the required animation effect from the slide            

IEffect wheelEffect = sequence[0] as IEffect;

//Change the wheel animation effect sub type from 2 spoke to 4 spoke

wheelEffect.Subtype = EffectSubtype.Wheel4;

//Saves the Presentation to the file system

pptxDoc.Save("Result.pptx");

}

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing Presentation from file system

Using pptxDoc As IPresentation = Presentation.Open("Sample.pptx")

   'Retrieves the first slide from Presentation

   Dim slide As ISlide = pptxDoc.Slides(0)

   'Retrieves the first shape

   Dim shape As IShape = TryCast(slide.Shapes(0), IShape)

   'Access the animation main sequence to modify the effects

   Dim sequence As ISequence = slide.Timeline.MainSequence

   'Get the required animation effect from the slide            

   Dim wheelEffect As IEffect = TryCast(sequence(0), IEffect)

   'Change the wheel animation effect sub type from 2 spoke to 4 spoke

   wheelEffect.Subtype = EffectSubtype.Wheel4

   'Saves the Presentation to the file system

   pptxDoc.Save("Result.pptx")

End Using

{% endhighlight %}

{% highlight UWP %}

//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".pptx");

//Creates a storage file from FileOpenPicker
StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();

//Loads or open an PowerPoint Presentation
IPresentation pptxDoc= await Presentation.OpenAsync(inputStorageFile);

//Retrieves the first slide from Presentation
ISlide slide = pptxDoc.Slides[0];

//Retrieves the first shape
IShape shape = slide.Shapes[0] as IShape;

//Access the animation main sequence to modify the effects
ISequence sequence = slide.Timeline.MainSequence;

//Get the required animation effect from the slide
IEffect wheelEffect = sequence[0] as IEffect;

//Change the wheel animation effect sub type from 2 spoke to 4 spoke
wheelEffect.Subtype = EffectSubtype.Wheel4;

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Result";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);

{% endhighlight %}

{% highlight ASP.NET CORE %}

//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream("Sample.pptx",FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);

//Retrieves the first slide from Presentation
ISlide slide = pptxDoc.Slides[0];

//Retrieves the first shape
IShape shape = slide.Shapes[0] as IShape;

//Access the animation main sequence to modify the effects
ISequence sequence = slide.Timeline.MainSequence;

//Get the required animation effect from the slide            
IEffect wheelEffect = sequence[0] as IEffect;

//Change the wheel animation effect sub type from 2 spoke to 4 spoke
wheelEffect.Subtype = EffectSubtype.Wheel4;

//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Animation.pptx", FileMode.Create);
pptxDoc.Save(outputStream);

{% endhighlight %}

{% highlight XAMARIN %}

//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Sample.pptx");

//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);

//Retrieves the first slide from Presentation
ISlide slide = pptxDoc.Slides[0];

//Retrieves the first shape
IShape shape = slide.Shapes[0] as IShape;

//Access the animation main sequence to modify the effects
ISequence sequence = slide.Timeline.MainSequence;

//Get the required animation effect from the slide            
IEffect wheelEffect = sequence[0] as IEffect;

//Change the wheel animation effect sub type from 2 spoke to 4 spoke
wheelEffect.Subtype = EffectSubtype.Wheel4;

//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();

//Save Presentation in stream format.
pptxDoc.Save(stream);

//Close the presentation
pptxDoc.Close();
stream.Position = 0;

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Animation.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Animation.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);

{% endhighlight %}

{% endtabs %}

## Modifying timing of animation effect

Presentation library allows you to edit the animation timing in the existing presentations. The following example demonstrates how to modify an existing animation timing applied to a shape.

{% tabs %}

{% highlight c# %}

//Open an existing Presentation from file system

using (IPresentation pptxDoc = Presentation.Open("Sample.pptx"))

{

//Retrieves the first slide from Presentation

ISlide slide = pptxDoc.Slides[0];

//Retrieves the first shape

IShape shape = slide.Shapes[0] as IShape;

//Access the animation main sequence to modify the effects

ISequence sequence = slide.Timeline.MainSequence;

//Get the required animation effect from the slide            

IEffect pathEffect = sequence[0] as IEffect;

//Increase the duration of the animation effect

pathEffect.Behaviors[0].Timing.Duration = 5;

//Saves the Presentation to the file system

pptxDoc.Save("Result.pptx");

}

{% endhighlight %}

{% highlight vb.net %}

'Open an existing Presentation from file system

Using pptxDoc As IPresentation = Presentation.Open("Sample.pptx")

   'Retrieves the first slide from Presentation

   Dim slide As ISlide = pptxDoc.Slides(0)

   'Retrieves the first shape

   Dim shape As IShape = TryCast(slide.Shapes(0), IShape)

   'Access the animation main sequence to modify the effects

   Dim sequence As ISequence = slide.Timeline.MainSequence

   'Get the required animation effect from the slide            

   Dim pathEffect As IEffect = TryCast(sequence(0), IEffect)

   'Increase the duration of the animation effect

   pathEffect.Behaviors(0).Timing.Duration = 5

   'Save the Presentation to the file system.

   pptxDoc.Save("Result.pptx")

End Using

{% endhighlight %}

{% highlight UWP %}

//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".pptx");

//Creates a storage file from FileOpenPicker
StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();

//Loads or open an PowerPoint Presentation
IPresentation pptxDoc= await Presentation.OpenAsync(inputStorageFile);

//Retrieves the first slide from Presentation
ISlide slide = pptxDoc.Slides[0];

//Retrieves the first shape
IShape shape = slide.Shapes[0] as IShape;

//Access the animation main sequence to modify the effects
ISequence sequence = slide.Timeline.MainSequence;

//Get the required animation effect from the slide
IEffect pathEffect = sequence[0] as IEffect;

//Increase the duration of the animation effect
pathEffect.Behaviors[0].Timing.Duration = 5;

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Result";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);

{% endhighlight %}

{% highlight ASP.NET CORE %}

//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream("Sample.pptx",FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);

//Retrieves the first slide from Presentation
ISlide slide = pptxDoc.Slides[0];

//Retrieves the first shape
IShape shape = slide.Shapes[0] as IShape;

//Access the animation main sequence to modify the effects
ISequence sequence = slide.Timeline.MainSequence;

//Get the required animation effect from the slide            
IEffect pathEffect = sequence[0] as IEffect;

//Increase the duration of the animation effect
pathEffect.Behaviors[0].Timing.Duration = 5;

//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Animation.pptx", FileMode.Create);
pptxDoc.Save(outputStream);

{% endhighlight %}

{% highlight XAMARIN %}

//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Sample.pptx");

//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);

//Retrieves the first slide from Presentation
ISlide slide = pptxDoc.Slides[0];

//Retrieves the first shape
IShape shape = slide.Shapes[0] as IShape;

//Access the animation main sequence to modify the effects
ISequence sequence = slide.Timeline.MainSequence;

//Get the required animation effect from the slide            
IEffect pathEffect = sequence[0] as IEffect;

//Increase the duration of the animation effect
pathEffect.Behaviors[0].Timing.Duration = 5;

//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();

//Save Presentation in stream format.
pptxDoc.Save(stream);

//Close the presentation
pptxDoc.Close();
stream.Position = 0;

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Animation.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Animation.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);

{% endhighlight %}

{% endtabs %}

## Reordering the animation effects

Presentation library allows you to reorder the animation effects in existing presentations. The following example demonstrates how to modify an existing animation order applied to a shape.

{% tabs %}

{% highlight c# %}

//Open the existing presentation

using (IPresentation pptxDoc = Presentation.Open("Sample.pptx"))

{

//Iterate the slide

ISlide slide = pptxDoc.Slides[0];

//Iterate the shape

IShape shape = slide.Shapes[0] as IShape;

//Iterate the sequence

ISequence sequence = slide.Timeline.MainSequence;

//Get the animation effects of the shape

IEffect[] shapeAnimationEffects = sequence.GetEffectsByShape(shape);

//Get the second animation effect of the shape

IEffect effect = shapeAnimationEffects[1];

//Remove the animation effect from the sequence

sequence.Remove(effect);

//Insert the removed animation effect as first

sequence.Insert(0, effect);

//Save the created presentation

pptxDoc.Save("Output.pptx");

}

{% endhighlight %}

{% highlight vb.net %}

'Open the existing presentation

Using pptxDoc As IPresentation = Presentation.Open("Sample.pptx")

   'Iterate the slide

   Dim slide As ISlide = pptxDoc.Slides(0)

   'Iterate the shape

   Dim shape As IShape = TryCast(slide.Shapes(0), IShape)

   'Iterate the sequence

   Dim sequence As ISequence = slide.Timeline.MainSequence

   'Get the animation effects of the shape

   Dim shapeAnimationEffects As IEffect() = sequence.GetEffectsByShape(shape)

   'Get the second animation effect of the shape

   Dim effect As IEffect = shapeAnimationEffects(1)

   'Remove the animation effect from the sequence

   sequence.Remove(effect)

   'Insert the removed animation effect as first

   sequence.Insert(0, effect)

   'Save the created presentation

   pptxDoc.Save("Output.pptx")

End Using

{% endhighlight %}

{% highlight UWP %}

//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".pptx");

//Creates a storage file from FileOpenPicker
StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();

//Loads or open an PowerPoint Presentation
IPresentation pptxDoc= await Presentation.OpenAsync(inputStorageFile);

//Iterate the slide
ISlide slide = pptxDoc.Slides[0];

//Iterate the shape
IShape shape = slide.Shapes[0] as IShape;

//Iterate the sequence
ISequence sequence = slide.Timeline.MainSequence;

//Get the animation effects of the shape
IEffect[] shapeAnimationEffects = sequence.GetEffectsByShape(shape);

//Get the second animation effect of the shape
IEffect effect = shapeAnimationEffects[1];

//Remove the animation effect from the sequence
sequence.Remove(effect);

//Insert the removed animation effect as first
sequence.Insert(0, effect);

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

{% highlight ASP.NET CORE %}

//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream("Sample.pptx",FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);

//Iterate the slide
ISlide slide = pptxDoc.Slides[0];

//Iterate the shape
IShape shape = slide.Shapes[0] as IShape;

//Iterate the sequence
ISequence sequence = slide.Timeline.MainSequence;

//Get the animation effects of the shape
IEffect[] shapeAnimationEffects = sequence.GetEffectsByShape(shape);

//Get the second animation effect of the shape
IEffect effect = shapeAnimationEffects[1];

//Remove the animation effect from the sequence
sequence.Remove(effect);

//Insert the removed animation effect as first
sequence.Insert(0, effect);

//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Animation.pptx", FileMode.Create);
pptxDoc.Save(outputStream);

{% endhighlight %}

{% highlight XAMARIN %}

//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Sample.pptx");

//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);

//Iterate the slide
ISlide slide = pptxDoc.Slides[0];

//Iterate the shape
IShape shape = slide.Shapes[0] as IShape;

//Iterate the sequence
ISequence sequence = slide.Timeline.MainSequence;

//Get the animation effects of the shape
IEffect[] shapeAnimationEffects = sequence.GetEffectsByShape(shape);

//Get the second animation effect of the shape
IEffect effect = shapeAnimationEffects[1];

//Remove the animation effect from the sequence
sequence.Remove(effect);

//Insert the removed animation effect as first
sequence.Insert(0, effect);

//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();

//Save Presentation in stream format.
pptxDoc.Save(stream);

//Close the presentation
pptxDoc.Close();
stream.Position = 0;

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Animation.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Animation.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);

{% endhighlight %}

{% endtabs %}

## Creating custom path animation effect

Presentation library allows you to create and modify the custom animations in presentations. The following example demonstrates how to apply a custom animation to a shape.

{% tabs %}

{% highlight c# %}

//Creates an instance for PowerPoint

using (IPresentation pptxDoc = Presentation.Create())

{

//Adds a blank slide to Presentation

ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Adds normal shape to slide

IShape cubeShape = slide.Shapes.AddShape(AutoShapeType.Cube, 200, 0, 300, 300);

//Access the animation sequence to create effects

ISequence sequence = slide.Timeline.MainSequence;

//Add user path effect to the shape

IEffect bounceEffect = sequence.AddEffect(cubeShape, EffectType.PathUser, EffectSubtype.None, EffectTriggerType.OnClick);

//Add commands to the empty path for moving

IMotionEffect motionBehavior = ((IMotionEffect)bounceEffect.Behaviors[0]);

PointF[] points = new PointF[1];

//Add the move command to move the position of the shape

points[0] = new PointF(0, 0);

motionBehavior.Path.Add(MotionCommandPathType.MoveTo, points, MotionPathPointsType.Auto, false);

//Add the line command to move the shape in straight line

points[0] = new PointF(0, 0.25f);

motionBehavior.Path.Add(MotionCommandPathType.LineTo, points, MotionPathPointsType.Auto, false);

//Add the end command to finish the path animation

motionBehavior.Path.Add(MotionCommandPathType.End, null, MotionPathPointsType.Auto, false);

//Saves the Presentation

pptxDoc.Save("Sample.pptx");

}

{% endhighlight %}

{% highlight vb.net %}

'Creates an instance for PowerPoint

Using pptxDoc As IPresentation = Presentation.Create()

   'Adds a blank slide to Presentation

   Dim slide As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank)

   'Adds normal shape to slide

   Dim cubeShape As IShape = slide.Shapes.AddShape(AutoShapeType.Cube, 200, 0, 300, 300)

   'Access the animation sequence to create effects

   Dim sequence As ISequence = slide.Timeline.MainSequence

   'Add user path effect to the shape

   Dim bounceEffect As IEffect = sequence.AddEffect(cubeShape, EffectType.PathUser, EffectSubtype.None, EffectTriggerType.OnClick)

   'Add commands to the empty path for moving

   Dim motionBehavior As IMotionEffect = DirectCast(bounceEffect.Behaviors(0), IMotionEffect)

   Dim points As PointF() = New PointF(0) {}

   'Add the move command to move the position of the shape

   points(0) = New PointF(0, 0)

   motionBehavior.Path.Add(MotionCommandPathType.MoveTo, points, MotionPathPointsType.Auto, False)

   'Add the line command to move the shape in straight line

   points(0) = New PointF(0, 0.25F)

   motionBehavior.Path.Add(MotionCommandPathType.LineTo, points, MotionPathPointsType.Auto, False)

   'Add the end command to finish the path animation

   motionBehavior.Path.Add(MotionCommandPathType.[End], Nothing, MotionPathPointsType.Auto, False)

   'Saves the Presentation

   pptxDoc.Save("Sample.pptx")

End Using

{% endhighlight %}

{% highlight UWP %}

//Create an instance of PowerPoint Presentation
IPresentation pptxDoc = Presentation.Create();

//Add a blank slide to Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Adds normal shape to slide
IShape cubeShape = slide.Shapes.AddShape(AutoShapeType.Cube, 200, 0, 300, 300);

//Access the animation sequence to create effects
ISequence sequence = slide.Timeline.MainSequence;

//Add user path effect to the shape
IEffect bounceEffect = sequence.AddEffect(cubeShape, EffectType.PathUser, EffectSubtype.None, EffectTriggerType.OnClick);

//Add commands to the empty path for moving
IMotionEffect motionBehavior = ((IMotionEffect)bounceEffect.Behaviors[0]);
PointF[] points = new PointF[1];

//Add the move command to move the position of the shape
points[0] = new PointF(0, 0);
motionBehavior.Path.Add(MotionCommandPathType.MoveTo, points, MotionPathPointsType.Auto, false);

//Add the line command to move the shape in straight line
points[0] = new PointF(0, 0.25f);
motionBehavior.Path.Add(MotionCommandPathType.LineTo, points, MotionPathPointsType.Auto, false);

//Add the end command to finish the path animation
motionBehavior.Path.Add(MotionCommandPathType.End, null, MotionPathPointsType.Auto, false);

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

{% highlight ASP.NET CORE %}

//Creates an instance for PowerPoint
IPresentation pptxDoc = Presentation.Create();

//Adds a blank slide to Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Adds normal shape to slide
IShape cubeShape = slide.Shapes.AddShape(AutoShapeType.Cube, 200, 0, 300, 300);

//Access the animation sequence to create effects
ISequence sequence = slide.Timeline.MainSequence;

//Add user path effect to the shape
IEffect bounceEffect = sequence.AddEffect(cubeShape, EffectType.PathUser, EffectSubtype.None, EffectTriggerType.OnClick);

//Add commands to the empty path for moving
IMotionEffect motionBehavior = ((IMotionEffect)bounceEffect.Behaviors[0]);
PointF[] points = new PointF[1];

//Add the move command to move the position of the shape
points[0] = new PointF(0, 0);
motionBehavior.Path.Add(MotionCommandPathType.MoveTo, points, MotionPathPointsType.Auto, false);

//Add the line command to move the shape in straight line
points[0] = new PointF(0, 0.25f);
motionBehavior.Path.Add(MotionCommandPathType.LineTo, points, MotionPathPointsType.Auto, false);

//Add the end command to finish the path animation
motionBehavior.Path.Add(MotionCommandPathType.End, null, MotionPathPointsType.Auto, false);

//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Sample.pptx", FileMode.Create);
pptxDoc.Save(outputStream);

{% endhighlight %}

{% highlight XAMARIN %}

//Creates an instance for PowerPoint
IPresentation pptxDoc = Presentation.Create();

//Adds a blank slide to Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Adds normal shape to slide
IShape cubeShape = slide.Shapes.AddShape(AutoShapeType.Cube, 200, 0, 300, 300);

//Access the animation sequence to create effects
ISequence sequence = slide.Timeline.MainSequence;

//Add user path effect to the shape
IEffect bounceEffect = sequence.AddEffect(cubeShape, EffectType.PathUser, EffectSubtype.None, EffectTriggerType.OnClick);

//Add commands to the empty path for moving
IMotionEffect motionBehavior = ((IMotionEffect)bounceEffect.Behaviors[0]);
PointF[] points = new PointF[1];

//Add the move command to move the position of the shape
points[0] = new PointF(0, 0);
motionBehavior.Path.Add(MotionCommandPathType.MoveTo, points, MotionPathPointsType.Auto, false);

//Add the line command to move the shape in straight line
points[0] = new PointF(0, 0.25f);
motionBehavior.Path.Add(MotionCommandPathType.LineTo, points, MotionPathPointsType.Auto, false);

//Add the end command to finish the path animation
motionBehavior.Path.Add(MotionCommandPathType.End, null, MotionPathPointsType.Auto, false);

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

## Removing animation effect

Presentation library allows you to remove the animation effects from a shape. The following example demonstrates how to remove an animation effect from a shape.

{% tabs %}

{% highlight c# %}

//Open the existing presentation

using (IPresentation pptxDoc = Presentation.Open("Sample.pptx"))

{

//Iterate the slide

ISlide slide = pptxDoc.Slides[0];

//Retrieves the first shape

IShape shape = slide.Shapes[0] as IShape;

//Iterate the sequence

ISequence sequence = slide.Timeline.MainSequence;

//To Remove the animation effects from the shape

//Get the animation effects of the particular shape

IEffect[] animationEffects = sequence.GetEffectsByShape(shape);

//Remove the animation effect from the main sequence

foreach (IEffect effect in animationEffects)
{
   sequence.Remove(effect);
}

//Save the created presentation

pptxDoc.Save("Result.pptx");

}

{% endhighlight %}

{% highlight vb.net %}

'Open the existing presentation

Using pptxDoc As IPresentation = Presentation.Open("Sample.pptx")

   'Iterate the slide

   Dim slide As ISlide = pptxDoc.Slides(0)

   'Retrieves the first shape

   Dim shape As IShape = TryCast(slide.Shapes(0), IShape)

   'Iterate the sequence

   Dim sequence As ISequence = slide.Timeline.MainSequence

   'To Remove the animation effects from the shape

   'Get the animation effects of the particular shape

   Dim animationEffects As IEffect() = sequence.GetEffectsByShape(shape)

   'Remove the animation effect from the main sequence

   For Each effect As IEffect In animationEffects
      sequence.Remove(effect)
   Next

   'Save the created presentation

   pptxDoc.Save("Result.pptx")

End Using

{% endhighlight %}

{% highlight UWP %}

//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".pptx");

//Creates a storage file from FileOpenPicker
StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();

//Loads or open an PowerPoint Presentation
IPresentation pptxDoc= await Presentation.OpenAsync(inputStorageFile);

//Iterate the slide
ISlide slide = pptxDoc.Slides[0];

//Retrieves the first shape
IShape shape = slide.Shapes[0] as IShape;

//Iterate the sequence
ISequence sequence = slide.Timeline.MainSequence;

//To Remove the animation effects from the shape
//Get the animation effects of the particular shape
IEffect[] animationEffects = sequence.GetEffectsByShape(shape);

//Remove the animation effect from the main sequence

foreach (IEffect effect in animationEffects)
{
   sequence.Remove(effect);
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

{% highlight ASP.NET CORE %}

//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream("Sample.pptx",FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);

//Iterate the slide
ISlide slide = pptxDoc.Slides[0];

//Retrieves the first shape
IShape shape = slide.Shapes[0] as IShape;

//Iterate the sequence
ISequence sequence = slide.Timeline.MainSequence;

//To Remove the animation effects from the shape
//Get the animation effects of the particular shape
IEffect[] animationEffects = sequence.GetEffectsByShape(shape);

//Remove the animation effect from the main sequence
foreach (IEffect effect in animationEffects)
{
   sequence.Remove(effect);
}

//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Animation.pptx", FileMode.Create);
pptxDoc.Save(outputStream);

{% endhighlight %}

{% highlight XAMARIN %}

//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Sample.pptx");

//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);

//Iterate the slide
ISlide slide = pptxDoc.Slides[0];

//Retrieves the first shape
IShape shape = slide.Shapes[0] as IShape;

//Iterate the sequence
ISequence sequence = slide.Timeline.MainSequence;

//To Remove the animation effects from the shape
//Get the animation effects of the particular shape
IEffect[] animationEffects = sequence.GetEffectsByShape(shape);

//Remove the animation effect from the main sequence
foreach (IEffect effect in animationEffects)
{
   sequence.Remove(effect);
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
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Animation.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Animation.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);

{% endhighlight %}

{% endtabs %}

## Supported animation effects type

Syncfusion Presentation library supports the following predefined animation effects with the sub types like Microsoft PowerPoint.

<table>
<tr>
<td>
{{'**Effects**'| markdownify }}
</td>
<td>
{{'**Entrance**'| markdownify }}
</td>
<td>
{{'**Exit**'| markdownify }}
</td>
<td>
{{'**Emphasis**'| markdownify }}
</td>
<td>
{{'**Motion path**'| markdownify }}
</td>
<td>
{{'**Effect options**'| markdownify }}
</td>
</tr>
<tr>
<td>
Appear
</td>
<td>
Yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
CurveUpDown
</td>
<td>
Yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
Ascend
</td>
<td>
Yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
Blast
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
Blinds
</td>
<td>
Yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
<li> Horizontal </li>
<li> Vertical </li>
</td>
</tr>
<tr>
<td>
Blink
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
BoldFlash
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
BoldReveal
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
Boomerang
</td>
<td>
Yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
Bounce
</td>
<td>
Yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
Box
</td>
<td>
Yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
<li> In </li>
<li> Out </li>
</td>
</tr>
<tr>
<td>
BrushOnColor
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
BrushOnUnderline
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
CenterRevolve
</td>
<td>
Yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
ChangeFillColor
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
<li> Instant </li>
<li> Gradual </li>
<li> GradualAndCycleClockwise </li>
<li> GradualAndCycleCounterClockwise </li>
</td>
</tr>
<tr>
<td>
ChangeFont
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
<li> Instant </li>
<li> Gradual </li>
</td>
</tr>
<tr>
<td>
ChangeFontColor
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
<li> Instant </li>
<li> Gradual </li>
<li> GradualAndCycleClockwise </li>
<li> GradualAndCycleCounterClockwise </li>
</td>
</tr>
<tr>
<td>
ChangeFontSize
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
<li> Instant </li>
<li> Gradual </li>
</td>
</tr>
<tr>
<td>
ChangeFontStyle
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
<li> FontBold </li>
<li> FontItalic </li>
<li> FontUnderline </li>
</td>
</tr>
<tr>
<td>
ChangeLineColor
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
<li> Instant </li>
<li> Gradual </li>
<li> GradualAndCycleClockwise </li>
<li> GradualAndCycleCounterClockwise </li>
</td>
</tr>
<tr>
<td>
Checkerboard
</td>
<td>
Yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
<li> Vertical </li>
<li> Across </li>
</td>
</tr>
<tr>
<td>
Circle
</td>
<td>
Yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
<li> In </li>
<li> Out </li>
</td>
</tr>
<tr>
<td>
ColorBlend
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
ColorTypewriter
</td>
<td>
Yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
ColorWave
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
ComplementaryColor
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
ComplementaryColor2
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
Compress
</td>
<td>
Yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
ContrastingColor
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
Crawl
</td>
<td>
Yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
<li> Right </li>
<li> Left </li>
<li> Top </li>
<li> Bottom </li>
</td>
</tr>
<tr>
<td>
Credits
</td>
<td>
Yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
Custom
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
- 
</td>
</tr>
<tr>
<td>
Darken
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
Desaturate
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
Descend
</td>
<td>
Yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
Diamond
</td>
<td>
Yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
<li> In </li>
<li> Out </li>
</td>
</tr>
<tr>
<td>
Dissolve
</td>
<td>
Yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
EaseInOut
</td>
<td>
Yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
Expand
</td>
<td>
Yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
Fade
</td>
<td>
Yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
FadedSwivel
</td>
<td>
Yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
FadedZoom
</td>
<td>
Yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
<li> None </li>
<li> Center </li>
</td>
</tr>
<tr>
<td>
FlashBulb
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
FlashOnce
</td>
<td>
Yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
Flicker
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
Flip
</td>
<td>
Yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
Float
</td>
<td>
Yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
Fly
</td>
<td>
Yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
<li> Right </li>
<li> Left </li>
<li> Top </li>
<li> Bottom </li>
<li> TopLeft </li>
<li> TopRight </li>
<li> BottomLeft </li>
<li> BottomRight </li>
</td>
</tr>
<tr>
<td>
Fold
</td>
<td>
Yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
Glide
</td>
<td>
Yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
GrowAndTurn
</td>
<td>
Yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
GrowShrink
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
GrowWithColor
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
Lighten
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
LightSpeed
</td>
<td>
Yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
Path4PointStar
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
Path5PointStar
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
Path6PointStar
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
Path8PointStar
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathArcDown
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathArcLeft
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathArcRight
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathArcUp
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathBean
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathBounceLeft
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathBounceRight
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathBuzzsaw
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathCircle
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathCrescentMoon
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathCurvedSquare
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathCurvedX
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathCurvyLeft
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathCurvyRight
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathCurvyStar
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathDecayingWave
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathDiagonalDownRight
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathDiagonalUpRight
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathDiamond
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathDown
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathEqualTriangle
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathFigure8Four
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathFootball
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathFunnel
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathHeart
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathHeartbeat
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathHexagon
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathHorizontalFigure8
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathInvertedSquare
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathInvertedTriangle
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathLeft
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathLoopdeLoop
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathNeutron
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathOctagon
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathParallelogram
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathPeanut
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathPentagon
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathPlus
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathPointyStar
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathRight
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathRightTriangle
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathSCurve1
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathSCurve2
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathSineWave
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathSpiralLeft
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathSpiralRight
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathSpring
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathSquare
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathStairsDown
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathSwoosh
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathTeardrop
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathTrapezoid
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathTurnDown
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathTurnRight
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathTurnUp
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathTurnUpRight
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathUp
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathUser
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathVerticalFigure8
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathWave
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
PathZigzag
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
Peek
</td>
<td>
Yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
<li> Bottom </li>
<li> Left </li>
<li> Right </li>
<li> Top </li>
</td>
</tr>
<tr>
<td>
Pinwheel
</td>
<td>
Yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
Plus
</td>
<td>
Yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
<li> In </li>
<li> Out </li>
</td>
</tr>
<tr>
<td>
RandomBars
</td>
<td>
Yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
<li> Horizontal </li>
<li> Vertical </li>
</td>
</tr>
<tr>
<td>
RandomEffects
</td>
<td>
Yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
RiseUp
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
Shimmer
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
Sling
</td>
<td>
Yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
Spin
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
Spinner
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
Spiral
</td>
<td>
Yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
Split
</td>
<td>
Yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
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
Stretch
</td>
<td>
yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
<li> Right </li>
<li> Left </li>
<li> Top </li>
<li> Bottom </li>
<li> Across </li>
</td>
</tr>
<tr>
<td>
Strips
</td>
<td>
Yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
<li> UpLeft </li>
<li> UpRight </li>
<li> DownLeft </li> 
<li> DownRight </li>
</td>
</tr>
<tr>
<td>
StyleEmphasis
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
Swish
</td>
<td>
Yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
Swivel
</td>
<td>
Yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
<li> Horizontal </li>
<li> Vertical </li>
</td>
</tr>
<tr>
<td>
Teeter
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
Thread
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
Transparency
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
Unfold
</td>
<td>
yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
VerticalGrow
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
Wave
</td>
<td>
-
</td>
<td>
-
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
Wedge
</td>
<td>
Yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
Wheel
</td>
<td>
Yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
<li> Wheel1 </li>
<li> Wheel2 </li>
<li> Wheel3 </li>
<li> Wheel4 </li>
<li> Wheel8 </li>
</td>
</tr>
<tr>
<td>
Whip
</td>
<td>
yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
Wipe
</td>
<td>
Yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
<li> Top </li>
<li> Right </li>
<li> Bottom </li>
<li> Left </li>
</td>
</tr>
<tr>
<td>
Magnify
</td>
<td>
Yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
None 
</td>
</tr>
<tr>
<td>
Zoom
</td>
<td>
Yes
</td>
<td>
Yes
</td>
<td>
-
</td>
<td>
-
</td>
<td>
<li> In </li>
<li> Out </li>
<li> InCenter - only for Entrance type </li>
<li> OutBottom - only for Entrance type </li>
<li> OutSlightly </li>
<li> InSlightly </li>
<li> OutCenter - only for Exit type </li>
<li> InBottom - only for Exit type </li>
</td>
</tr>
</table>