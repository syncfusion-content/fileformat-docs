---
title: Create, read and edit PowerPoint slides in CSharp |Syncfusion|
description: Create, read and edit PowerPoint slides in CSharp; Adding and modifying the slides in PowerPoint presentation
platform: file-formats
control: PowerPoint
documentation: UG
---
# Working with Slides in PowerPoint  

## Adding slide to the PowerPoint presentation

In PowerPoint presentation, a slide is a container for the elements like shapes, images, charts, text box etc. The slides may inherit the formatting and layout properties from its 'Master' and 'Layout' slides.

The following code example demonstrates how to add a blank slide to the Presentation.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Creates a PowerPoint instance
IPresentation pptxDoc = Presentation.Create();
//Adds a slide to the PowerPoint presentation
ISlide slide = pptxDoc.Slides.Add();
//Saves the Presentation to the file system.
pptxDoc.Save("Sample.pptx");
//Closes the Presentation instance
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Creates a PowerPoint instance
Dim pptxDoc As IPresentation = Presentation.Create()
'Adds a slide to the PowerPoint presentation
Dim slide As ISlide = pptxDoc.Slides.Add()
'Saves the Presentation to the file system.
pptxDoc.Save("Sample.pptx")
'Closes the Presentation instance
pptxDoc.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Creates a PowerPoint instance
IPresentation pptxDoc = Presentation.Create();
//Adds new Blank type of slide.
ISlide slide = pptxDoc.Slides.Add();
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
//Creates a PowerPoint instance
IPresentation pptxDoc = Presentation.Create();
//Adds a slide to the PowerPoint presentation
ISlide slide = pptxDoc.Slides.Add();
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Sample.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
//Release all resources of the stream
outputStream.Dispose();
//Closes the Presentation instance
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Creates a PowerPoint instance
IPresentation pptxDoc = Presentation.Create();
//Adds a slide to the PowerPoint presentation
ISlide slide = pptxDoc.Slides.Add();
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Slides/Add-PowerPoint-slide).

## Create a slide with predefined LayoutSlide

The Syncfusion PowerPoint library supports the following predefined slide layout types to create a slide as equivalent to Microsoft PowerPoint:

<ul>
<li>Blank</li>
<li>Comparison</li>
<li>Content with caption</li>
<li>Picture with caption</li>
<li>Section header</li>
<li>Title</li>
<li>Title and content</li>
<li>Title and vertical text</li>
<li>Title only</li>
<li>Two content</li>
<li>Vertical title and text</li>
</ul>

The following example demonstrates how to access a slide from the predefined blank slide layout type.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Create a PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();
//Add a slide of blank layout type
ISlide slide1 = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Save the PowerPoint file
pptxDoc.Save("Sample.pptx");
//Close the PowerPoint instance
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Create a PowerPoint file
Dim pptxDoc As IPresentation = Presentation.Create()
'Add a slide of blank layout type
Dim slide1 As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank)
'Save the PowerPoint file
pptxDoc.Save("Sample.pptx")
'Close the PowerPoint instance
pptxDoc.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Create a PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();
//Add a slide of blank layout type
ISlide slide1 = pptxDoc.Slides.Add(SlideLayoutType.Blank);
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
//Create a new instance of PowerPoint Presentation file
IPresentation pptxDoc = Presentation.Create();
//Add a slide of blank layout type
ISlide slide1 = pptxDoc.Slides.Add(SlideLayoutType.Blank);    
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream(OutputFileName, FileMode.Create);
pptxDoc.Save(outputStream);
//Release all resources of the stream
outputStream.Dispose();
//Close the PowerPoint presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Create a new instance of PowerPoint Presentation file
IPresentation pptxDoc = Presentation.Create();
//Add a slide of blank layout type
ISlide slide1 = pptxDoc.Slides.Add(SlideLayoutType.Blank);    
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Slides/Add-predefined-blank-slide-layout-type).

The following code example demonstrates how to add a slide with all other predefined slide layout types.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Create a PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();
//Add a slide of blank layout type
ISlide slide1 = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Add a slide of comparison type
ISlide slide2 = pptxDoc.Slides.Add(SlideLayoutType.Comparison);
//Add a slide of ContentWithCaption type
ISlide slide3 = pptxDoc.Slides.Add(SlideLayoutType.ContentWithCaption);
//Add a slide of PictureWithCaption type
ISlide slide4 = pptxDoc.Slides.Add(SlideLayoutType.PictureWithCaption);
//Add a slide of SectionHeader type
ISlide slide5 = pptxDoc.Slides.Add(SlideLayoutType.SectionHeader);
//Add a slide of Title type
ISlide slide6 = pptxDoc.Slides.Add(SlideLayoutType.Title);
//Add a slide of TitleAndContent type
ISlide slide7 = pptxDoc.Slides.Add(SlideLayoutType.TitleAndContent);
//Add a slide of TitleAndVerticalText type
ISlide slide8 = pptxDoc.Slides.Add(SlideLayoutType.TitleAndVerticalText);
//Add a slide of TitleOnly type
ISlide slide9 = pptxDoc.Slides.Add(SlideLayoutType.TitleOnly);
//Add a slide of TwoContent type
ISlide slide10 = pptxDoc.Slides.Add(SlideLayoutType.TwoContent);
//Add a slide of VerticalTitleAndText type
ISlide slide11 = pptxDoc.Slides.Add(SlideLayoutType.VerticalTitleAndText);
//Save the PowerPoint file
pptxDoc.Save("Sample.pptx");
//Close the PowerPoint instance
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Create a PowerPoint file
Dim pptxDoc As IPresentation = Presentation.Create()
'Add a slide of blank layout type
Dim slide1 As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank)
'Add a slide of comparison type
Dim ISlide As slide2 = pptxDoc.Slides.Add(SlideLayoutType.Comparison)
'Add a slide of ContentWithCaption type
Dim ISlide As slide3 = pptxDoc.Slides.Add(SlideLayoutType.ContentWithCaption)
'Add a slide of PictureWithCaption type
Dim ISlide As slide4 = pptxDoc.Slides.Add(SlideLayoutType.PictureWithCaption)
'Add a slide of SectionHeader type
Dim ISlide As slide5 = pptxDoc.Slides.Add(SlideLayoutType.SectionHeader)
'Add a slide of Title type
ISlide As slide6 = pptxDoc.Slides.Add(SlideLayoutType.Title)
'Add a slide of TitleAndContent type
Dim ISlide As slide7 = pptxDoc.Slides.Add(SlideLayoutType.TitleAndContent)
'Add a slide of TitleAndVerticalText type
Dim ISlide As slide8 = pptxDoc.Slides.Add(SlideLayoutType.TitleAndVerticalText)
'Add a slide of TitleOnly type
Dim ISlide As slide9 = pptxDoc.Slides.Add(SlideLayoutType.TitleOnly)
'Add a slide of TwoContent type
Dim ISlide As slide10 = pptxDoc.Slides.Add(SlideLayoutType.TwoContent)
'Add a slide of VerticalTitleAndText type
Dim ISlide As slide11 = pptxDoc.Slides.Add(SlideLayoutType.VerticalTitleAndText)
'Save the PowerPoint file
pptxDoc.Save("Sample.pptx")
'Close the PowerPoint instance
pptxDoc.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Create a PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();
//Add a slide of blank layout type
ISlide slide1 = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Add a slide of comparison type
ISlide slide2 = pptxDoc.Slides.Add(SlideLayoutType.Comparison);
//Add a slide of ContentWithCaption type
ISlide slide3 = pptxDoc.Slides.Add(SlideLayoutType.ContentWithCaption);
//Add a slide of PictureWithCaption type
ISlide slide4 = pptxDoc.Slides.Add(SlideLayoutType.PictureWithCaption);
//Add a slide of SectionHeader type
ISlide slide5 = pptxDoc.Slides.Add(SlideLayoutType.SectionHeader);
//Add a slide of Title type
ISlide slide6 = pptxDoc.Slides.Add(SlideLayoutType.Title);
//Add a slide of TitleAndContent type
ISlide slide7 = pptxDoc.Slides.Add(SlideLayoutType.TitleAndContent);
//Add a slide of TitleAndVerticalText type
ISlide slide8 = pptxDoc.Slides.Add(SlideLayoutType.TitleAndVerticalText);
//Add a slide of TitleOnly type
ISlide slide9 = pptxDoc.Slides.Add(SlideLayoutType.TitleOnly);
//Add a slide of TwoContent type
ISlide slide10 = pptxDoc.Slides.Add(SlideLayoutType.TwoContent);
//Add a slide of VerticalTitleAndText type
ISlide slide11 = pptxDoc.Slides.Add(SlideLayoutType.VerticalTitleAndText);
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
//Create a new instance of PowerPoint Presentation file
IPresentation pptxDoc = Presentation.Create();
//Add a slide of Blank type
ISlide slide1 = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Add a slide of comparison type
ISlide slide2 = pptxDoc.Slides.Add(SlideLayoutType.Comparison);
//Add a slide of ContentWithCaption type
ISlide slide3 = pptxDoc.Slides.Add(SlideLayoutType.ContentWithCaption);
//Add a slide of PictureWithCaption type
ISlide slide4 = pptxDoc.Slides.Add(SlideLayoutType.PictureWithCaption);
//Add a slide of SectionHeader type
ISlide slide5 = pptxDoc.Slides.Add(SlideLayoutType.SectionHeader);
//Add a slide of Title type
ISlide slide6 = pptxDoc.Slides.Add(SlideLayoutType.Title);
//Add a slide of TitleAndContent type
ISlide slide7 = pptxDoc.Slides.Add(SlideLayoutType.TitleAndContent);
//Add a slide of TitleAndVerticalText type
ISlide slide8 = pptxDoc.Slides.Add(SlideLayoutType.TitleAndVerticalText);
//Add a slide of TitleOnly type
ISlide slide9 = pptxDoc.Slides.Add(SlideLayoutType.TitleOnly);
//Add a slide of TwoContent type
ISlide slide10 = pptxDoc.Slides.Add(SlideLayoutType.TwoContent);
//Add a slide of VerticalTitleAndText type
ISlide slide11 = pptxDoc.Slides.Add(SlideLayoutType.VerticalTitleAndText);    
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream(OutputFileName, FileMode.Create);
pptxDoc.Save(outputStream);
//Release all resources of the stream
outputStream.Dispose();
//Close the PowerPoint presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Create a new instance of PowerPoint Presentation file
IPresentation pptxDoc = Presentation.Create();
//Add a slide of Blank type
ISlide slide1 = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Add a slide of comparison type
ISlide slide2 = pptxDoc.Slides.Add(SlideLayoutType.Comparison);
//Add a slide of ContentWithCaption type
ISlide slide3 = pptxDoc.Slides.Add(SlideLayoutType.ContentWithCaption);
//Add a slide of PictureWithCaption type
ISlide slide4 = pptxDoc.Slides.Add(SlideLayoutType.PictureWithCaption);
//Add a slide of SectionHeader type
ISlide slide5 = pptxDoc.Slides.Add(SlideLayoutType.SectionHeader);
//Add a slide of Title type
ISlide slide6 = pptxDoc.Slides.Add(SlideLayoutType.Title);
//Add a slide of TitleAndContent type
ISlide slide7 = pptxDoc.Slides.Add(SlideLayoutType.TitleAndContent);
//Add a slide of TitleAndVerticalText type
ISlide slide8 = pptxDoc.Slides.Add(SlideLayoutType.TitleAndVerticalText);
//Add a slide of TitleOnly type
ISlide slide9 = pptxDoc.Slides.Add(SlideLayoutType.TitleOnly);
//Add a slide of TwoContent type
ISlide slide10 = pptxDoc.Slides.Add(SlideLayoutType.TwoContent);
//Add a slide of VerticalTitleAndText type
ISlide slide11 = pptxDoc.Slides.Add(SlideLayoutType.VerticalTitleAndText);     
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Slides/Add-all-predefined-slide-layout-types).

## Adding Custom layout slide

The slide layout are template design for the PowerPoint slides. Slide layout can contains formatting, positioning, and placeholders for a slide. There are 9 predefined layouts and custom slide layouts can also be designed.

The following code example demonstrates how to create and use a customized slide layout in PowerPoint presentation.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Open the template presentation
IPresentation pptxDoc = Presentation.Open("Sample.pptx");
//Add a new custom layout slide to the master collection with a specific layout type and name
ILayoutSlide layoutSlide = pptxDoc.Masters[0].LayoutSlides.Add(SlideLayoutType.Blank, "CustomLayout");
//Set background of the layout slide
layoutSlide.Background.Fill.SolidFill.Color = ColorObject.FromArgb(78, 89, 90);
//Get the stream of an image
Stream pictureStream = File.Open("Image.png", FileMode.Open);
//Add the picture into layout slide
layoutSlide.Shapes.AddPicture(pictureStream, 100, 100, 100, 100);
//Add a slide of new designed custom layout to the presentation
ISlide slide = pptxDoc.Slides.Add(layoutSlide);
//Save the presentation
pptxDoc.Save("Output.pptx");
//Close the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Open the template presentation
Dim pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
'Add a new custom layout slide to the master collection with a specific layout type and name
Dim layoutSlide As ILayoutSlide = pptxDoc.Masters(0).LayoutSlides.Add(SlideLayoutType.Blank, "CustomLayout")
'Set background of the layout slide
layoutSlide.Background.Fill.SolidFill.Color = ColorObject.FromArgb(78, 89, 90)
'Get the stream of an image
Dim pictureStream As Stream = File.Open("Image.png", FileMode.Open)
'Add the picture into layout slide
layoutSlide.Shapes.AddPicture(pictureStream, 100, 100, 100, 100)
'Add a slide of new designed custom layout to the presentation
Dim slide As ISlide = pptxDoc.Slides.Add(layoutSlide)
'Save the presentation
pptxDoc.Save("Output.pptx")
'Close the presentation
pptxDoc.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".pptx");
//Creates a storage file from FileOpenPicker
StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc= await Presentation.OpenAsync(inputStorageFile);
//Add a new custom layout slide to the master collection with a specific layout type and name
ILayoutSlide layoutSlide = pptxDoc.Masters[0].LayoutSlides.Add(SlideLayoutType.Blank, "CustomLayout");
//Set background of the layout slide
layoutSlide.Background.Fill.SolidFill.Color = ColorObject.FromArgb(78, 89, 90);
//Get the stream of an image
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream pictureStream = assembly.GetManifestResourceStream("UWP.Data.Image.png");
//Add the picture into layout slide
layoutSlide.Shapes.AddPicture(pictureStream, 100, 100, 100, 100);
//Add a slide of new designed custom layout to the presentation
ISlide slide = pptxDoc.Slides.Add(layoutSlide);
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
//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream(inputFileName,FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);
//Add a new custom layout slide to the master collection with a specific layout type and name
ILayoutSlide layoutSlide = pptxDoc.Masters[0].LayoutSlides.Add(SlideLayoutType.Blank, "CustomLayout");
//Set background of the layout slide
layoutSlide.Background.Fill.SolidFill.Color = ColorObject.FromArgb(78, 89, 90);
//Get the stream of an image
FileStream pictureStream = new FileStream(inputImagePath, FileMode.Open);
//Add the picture into layout slide
layoutSlide.Shapes.AddPicture(pictureStream, 100, 100, 100, 100);
//Add a slide of new designed custom layout to the presentation
ISlide slide = pptxDoc.Slides.Add(layoutSlide);
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream(OutputFileName, FileMode.Create);
pptxDoc.Save(outputStream);
//Release all resources of the stream
outputStream.Dispose();
//Close the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream(resourcePath);
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);
//Add a new custom layout slide to the master collection with a specific layout type and name
ILayoutSlide layoutSlide = pptxDoc.Masters[0].LayoutSlides.Add(SlideLayoutType.Blank, "CustomLayout");
//Set background of the layout slide
layoutSlide.Background.Fill.SolidFill.Color = ColorObject.FromArgb(78, 89, 90);
//Get the stream of an image
Stream pictureStream = assembly.GetManifestResourceStream(picturePath);
//Add the picture into layout slide
layoutSlide.Shapes.AddPicture(pictureStream, 100, 100, 100, 100);
//Add a slide of new designed custom layout to the presentation
ISlide slide = pptxDoc.Slides.Add(layoutSlide);
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Slides/Create-and-use-custom-layout-slide).

The following code example demonstrates how to add a slide with an existing slide’s layout.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Open the template presentation
IPresentation pptxDoc = Presentation.Open("Sample.pptx");
//Get the layout slide collection of the master
ILayoutSlides layoutSlides = pptxDoc.Masters[0].LayoutSlides;
ILayoutSlide slideLayout = null;
//Get each layout slide from the collection
foreach (ILayoutSlide layout in layoutSlides)
{
    //Check if the layout slide has desired custom layout name
    if (layout.Name == "CustomSlideLayout")
    {
        slideLayout = layout;
        break;
    }
}
//Add slide with the desired layout.
ISlide slide = pptxDoc.Slides.Add(slideLayout);
//Save the presentation
pptxDoc.Save("Output.pptx");
//Close the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Open the template presentation
Dim pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
'Get the layout slide collection of the master
Dim layoutSlides As ILayoutSlides = pptxDoc.Masters(0).LayoutSlides
Dim slideLayout As ILayoutSlide = Nothing
'Get each layout slide from the collection
For Each layout As ILayoutSlide In layoutSlides
    'Check if the layout slide has desired custom layout name
    If layout.Name = "CustomSlideLayout" Then
        slideLayout = layout
        Exit For
    End If
Next
'Add slide with the desired layout.
Dim slide As ISlide = pptxDoc.Slides.Add(slideLayout)
'Save the presentation
pptxDoc.Save("Output.pptx")
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
//Add a new custom layout slide to the master collection with a specific layout type and name
ILayoutSlide layoutSlide = pptxDoc.Masters[0].LayoutSlides.Add(SlideLayoutType.Blank, "CustomSlideLayout");
//Get the layout slide collection of the master
ILayoutSlides layoutSlides = pptxDoc.Masters[0].LayoutSlides;
ILayoutSlide slideLayout = null;
//Get each layout slide from the collection
foreach (ILayoutSlide layout in layoutSlides)
{
    //Check if the layout slide has desired custom layout name
    if (layout.Name == "CustomSlideLayout")
    {
        slideLayout = layout;
        break;
    }
}
//Add slide with the desired layout.
ISlide slide = pptxDoc.Slides.Add(slideLayout);
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
//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream(inputFileName,FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);
//Get the layout slide collection of the master
ILayoutSlides layoutSlides = pptxDoc.Masters[0].LayoutSlides;
ILayoutSlide slideLayout = null;
//Get each layout slide from the collection
foreach (ILayoutSlide layout in layoutSlides)
{
    //Check if the layout slide has desired custom layout name
    if (layout.Name == "CustomSlideLayout")
    {
        slideLayout = layout;
        break;
    }
}
//Add slide with the desired layout.
ISlide slide = pptxDoc.Slides.Add(slideLayout);
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream(OutputFileName, FileMode.Create);
pptxDoc.Save(outputStream);
//Release all resources of the stream
outputStream.Dispose();
//Close the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream(resourcePath);
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);
//Get the layout slide collection of the master
ILayoutSlides layoutSlides = pptxDoc.Masters[0].LayoutSlides;
ILayoutSlide slideLayout = null;
//Get each layout slide from the collection
foreach (ILayoutSlide layout in layoutSlides)
{
    //Check if the layout slide has desired custom layout name
    if (layout.Name == "CustomSlideLayout")
    {
        slideLayout = layout;
        break;
    }
}
//Add slide with the desired layout.
ISlide slide = pptxDoc.Slides.Add(slideLayout);
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Slides/Add-slide-with-existing-slide-layout).

## Cloning slide

You can create a deep copy of a slide by cloning the slide. The cloned slide is an independent copy of its source slide. This means the changes made in the cloned slide do not affect the source slide.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Opens an existing Presentation.
IPresentation pptxDoc = Presentation.Open("Presentation.pptx");
//Retrieves the slide instance.
ISlide slide = pptxDoc.Slides[0];
//Creates a cloned copy of slide.
ISlide slideClone = slide.Clone();
//Adds a new text box to the cloned slide.
IShape textboxShape = slideClone.AddTextBox(0, 0, 250, 250);
//Adds a paragraph with text content to the shape.
textboxShape.TextBody.AddParagraph("Hello Presentation");
//Adds the slide to the Presentation.
pptxDoc.Slides.Add(slideClone);
//Saves the Presentation to the file system.
pptxDoc.Save("Output.pptx");
//Closes the Presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Opens an existing Presentation.
Dim pptxDoc As IPresentation = Presentation.Open("Presentation.pptx")
'Retrieves the slide instance.
Dim slide As ISlide = pptxDoc.Slides(0)
'Creates a cloned copy of slide.
Dim slideClone As ISlide = slide.Clone()
'Adds a new text box to the cloned slide.
Dim textboxShape As IShape = slideClone.AddTextBox(0, 0, 250, 250)
'Adds a paragraph with text content to the shape.
textboxShape.TextBody.AddParagraph("Hello Presentation")
'Adds the slide to the Presentation.
pptxDoc.Slides.Add(slideClone)
'Saves the Presentation to the file system.
pptxDoc.Save("Output.pptx")
'Closes the Presentation
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
//Retrieves the slide instance.
ISlide slide = pptxDoc.Slides[0];
//Creates a cloned copy of slide.
ISlide slideClone = slide.Clone();
//Adds a new text box to the cloned slide.
IShape textboxShape = slideClone.AddTextBox(0, 0, 250, 250);
//Adds a paragraph with text content to the shape.
textboxShape.TextBody.AddParagraph("Hello Presentation");
//Adds the slide to the Presentation.
pptxDoc.Slides.Add(slideClone);
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
//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream(inputFileName,FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);
//Retrieves the slide instance.
ISlide slide = pptxDoc.Slides[0];
//Creates a cloned copy of slide.
ISlide slideClone = slide.Clone();
//Adds a new text box to the cloned slide.
IShape textboxShape = slideClone.AddTextBox(0, 0, 250, 250);
//Adds a paragraph with text content to the shape.
textboxShape.TextBody.AddParagraph("Hello Presentation");
//Adds the slide to the Presentation.
pptxDoc.Slides.Add(slideClone);
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream(OutputFileName, FileMode.Create);
pptxDoc.Save(outputStream);
//Release all resources of the stream
outputStream.Dispose();
//Close the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream(resourcePath);
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);
//Retrieves the slide instance.
ISlide slide = pptxDoc.Slides[0];
//Creates a cloned copy of slide.
ISlide slideClone = slide.Clone();
//Adds a new text box to the cloned slide.
IShape textboxShape = slideClone.AddTextBox(0, 0, 250, 250);
//Adds a paragraph with text content to the shape.
textboxShape.TextBody.AddParagraph("Hello Presentation");
//Adds the slide to the Presentation.
pptxDoc.Slides.Add(slideClone);
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Slides/Clone-PowerPoint-slide).

## Merging slide

The Essential Presentation provides ability to clone slides from one Presentation to another Presentation. With this ability, you can split a large Presentation into small ones and also merge multiple presentations to one Presentation. You can choose the theme for the cloned slide by using the enum [PasteOption](https://help.syncfusion.com/cr/file-formats/Syncfusion.Presentation.PasteOptions.html).

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Opens the source Presentation
IPresentation sourcePresentation = Presentation.Open("SourcePresentation.pptx");
//Opens the destination Presentation
IPresentation destinationPresentation = Presentation.Open("DestinationPresentation.pptx");
//Clones the first slide of the source Presentation
ISlide clonedSlide = sourcePresentation.Slides[0].Clone();
//Merges the cloned slide to the destination Presentation with paste option - Destination Theme
destinationPresentation.Slides.Add(clonedSlide, PasteOptions.UseDestinationTheme, sourcePresentation);
//Saves the destination Presentation
destinationPresentation.Save("Output.pptx");
//Closes the source presentation
sourcePresentation.Close();
//Closes the destination Presentation
destinationPresentation.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Opens the source Presentation
Dim sourcePresentation_1 As IPresentation = Presentation.Open("SourcePresentation.pptx")
'Opens the destination Presentation
Dim destinationPresentation_1 As IPresentation = Presentation.Open("DestinationPresentation.pptx")
'Clones the first slide of the source Presentation
Dim clonedSlide As ISlide = sourcePresentation_1.Slides(0).Clone()
'Merges the cloned slide to the destination Presentation with paste option - Destination Theme
destinationPresentation_1.Slides.Add(clonedSlide, PasteOptions.UseDestinationTheme, sourcePresentation_1)
'Saves the destination Presentation
destinationPresentation_1.Save("Output.pptx")
'Closes the source presentation
sourcePresentation.Close()
'Closes the destination Presentation
destinationPresentation.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".pptx");
//Creates a storage file from FileOpenPicker
StorageFile sourceStorageFile = await openPicker.PickSingleFileAsync();
//Opens the source Presentation
IPresentation sourcePresentation = await Presentation.OpenAsync(sourceStorageFile);
//Creates a storage file from FileOpenPicker
StorageFile destinationStorageFile = await openPicker.PickSingleFileAsync();
//Opens the destination Presentation
IPresentation destinationPresentation = await Presentation.OpenAsync(destinationStorageFile);
//Clones the first slide of the source Presentation
ISlide clonedSlide = sourcePresentation.Slides[0].Clone();
//Merges the cloned slide to the destination Presentation with paste option - Destination Theme
destinationPresentation.Slides.Add(clonedSlide, PasteOptions.UseDestinationTheme, sourcePresentation); 
//Saves the destination Presentation
//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Output";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });
//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();
//Saves changes to the specified storage file
await destinationPresentation.SaveAsync(storageFile);
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Opens the source Presentation
IPresentation sourcePresentation = Presentation.Open(SourcePresentationStream);
//Opens the destination Presentation
IPresentation destinationPresentation = Presentation.Open(destinationPresentationStream);
//Clones the first slide of the source Presentation
ISlide clonedSlide = sourcePresentation.Slides[0].Clone();
//Merges the cloned slide to the destination Presentation with paste option - Destination Theme
destinationPresentation.Slides.Add(clonedSlide, PasteOptions.UseDestinationTheme, sourcePresentation);
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream(OutputFileName, FileMode.Create);
destinationPresentation.Save(outputStream);
//Release all resources of the stream
outputStream.Dispose();
//Closes the source presentation
sourcePresentation.Close();
//Closes the destination Presentation
destinationPresentation.Close();
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream(sourcePresentationPath);
Stream outputStream = assembly.GetManifestResourceStream(destinationPresentationPath);
//Loads or open an PowerPoint Presentation
IPresentation sourcePresentation = Presentation.Open(inputStream);
//Loads or open an PowerPoint Presentation
IPresentation destinationPresentation = Presentation.Open(outputStream);
//Clones the first slide of the source Presentation
ISlide clonedSlide = sourcePresentation.Slides[0].Clone();
//Merges the cloned slide to the destination Presentation with paste option - Destination Theme
destinationPresentation.Slides.Add(clonedSlide, PasteOptions.UseDestinationTheme, sourcePresentation);
//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();
//Save Presentation in stream format.
destinationPresentation.Save(stream);
//Close the presentation
destinationPresentation.Close();
stream.Position = 0;
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Sample.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Sample.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Slides/Merge-PowerPoint-slide).

## Removing slide

The Essential Presentation provides the ability to delete a slide by its instance or by its index position in slide collection. The following code demonstrates how to delete a slide from a presentation. 

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Opens an existing presentation.
IPresentation pptxDoc = Presentation.Open("Presentation1.pptx");
//Retrieves the slide instance.
ISlide slide = pptxDoc.Slides[0];
//Removes the specified slide from the Presentation.
pptxDoc.Slides.Remove(slide);
// Removes the slide from the specified index.
pptxDoc.Slides.RemoveAt(1);
//Saves the destination Presentation	
pptxDoc.Save("Output.pptx");
//Closes the Presentation instance
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Opens an existing Presentation.
Dim pptxDoc As IPresentation = Presentation.Open("Presentation1.pptx")
'Retrieves the slide instance.
Dim slide As ISlide = pptxDoc.Slides(0)
'Removes the specified slide from the Presentation.
pptxDoc.Slides.Remove(slide)
'Removes the slide from the specified index.
pptxDoc.Slides.RemoveAt(1)
'Saves the destination Presentation
pptxDoc.Save("Output.pptx")
'Closes the Presentation instance
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
//Retrieves the slide instance.
ISlide slide = pptxDoc.Slides[0];
//Removes the specified slide from the Presentation.
pptxDoc.Slides.Remove(slide);
//Removes the slide from the specified index.
pptxDoc.Slides.RemoveAt(1);
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
//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream(inputFileName,FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);
//Retrieves the slide instance.
ISlide slide = pptxDoc.Slides[0];
//Removes the specified slide from the Presentation.
pptxDoc.Slides.Remove(slide);
// Removes the slide from the specified index.
pptxDoc.Slides.RemoveAt(1);
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream(OutputFileName, FileMode.Create);
pptxDoc.Save(outputStream);
//Release all resources of the stream
outputStream.Dispose();
//Closes the Presentation instance
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream(resourcePath);
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);
//Retrieves the slide instance.
ISlide slide = pptxDoc.Slides[0];
//Removes the specified slide from the Presentation.
pptxDoc.Slides.Remove(slide);
// Removes the slide from the specified index.
pptxDoc.Slides.RemoveAt(1);
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Slides/Remove-PowerPoint-slide).

## Converting to image

You can convert a presentation slide to image with Essential Presentation. The following code example converts the first slide of a PowerPoint presentation into image and saves the image to a file.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Opens a PowerPoint presentation file
IPresentation pptxDoc = Presentation.Open(fileName); 
//Creates an instance of ChartToImageConverter and assigns it to ChartToImageConverter 
pptxDoc.ChartToImageConverter = new ChartToImageConverter(); 
//Converts the first slide into image
Image image = pptxDoc.Slides[0].ConvertToImage(Syncfusion.Drawing.ImageType.Metafile); 
//Saves the image as file
image.Save("slide1.png"); 
//Closes the Presentation instance
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Opens a PowerPoint presentation file
Dim pptxDoc As IPresentation = Presentation.Open(fileName)
'Creates an instance of ChartToImageConverter and assigns it to ChartToImageConverter 
pptxDoc.ChartToImageConverter = New ChartToImageConverter()
'Converts the first slide into image
Dim image As Image = pptxDoc.Slides(0).ConvertToImage(Syncfusion.Drawing.ImageType. Metafile)
'Saves the image as file
image.Save("slide1.png")
'Closes the Presentation instance
pptxDoc.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Load the presentation file using open picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.FileTypeFilter.Add(".pptx");
StorageFile inputFile = await openPicker.PickSingleFileAsync();
IPresentation pptxDoc = await Presentation.OpenAsync(inputFile);
//Pick the folder to save the converted images.
FolderPicker folderPicker = new FolderPicker();
folderPicker.ViewMode = PickerViewMode.Thumbnail;
folderPicker.FileTypeFilter.Add("*");
StorageFolder storageFolder = await folderPicker.PickSingleFolderAsync();
//Create a cancellation token to cancel the image rendering instantly.
CancellationTokenSource cancellationToken = new CancellationTokenSource();
//Convert the slide to image.
ISlide slide1 = pptxDoc.Slides[0];
StorageFile imageFile = await storageFolder.CreateFileAsync("Slide1.png", CreationCollisionOption.ReplaceExisting);
await slide1.SaveAsImageAsync(imageFile, cancellationToken.Token);
//Close the presentation instance
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//PowerPoint Presentation to image conversion is not supported for ASP.NET Core platforms.
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//PowerPoint Presentation to image conversion is not supported for Xamarin platforms.
{% endhighlight %}

{% endtabs %}

For more details on assemblies required for converting a slide to image,  see [Conversion](https://help.syncfusion.com/file-formats/presentation/presentation-to-image#assemblies-required)

N> You can print the PowerPoint presentations by using its ability to convert the slides as images. For more details, refer to [Printing a PowerPoint presentation](/file-formats/presentation/working-with-powerpoint-presentation#printing-a-powerpoint-presentation)

## Changing Slide background

The following code example demonstrates setting the background for a slide.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Opens an existing Presentation.
IPresentation pptxDoc = Presentation.Open("Presentation1.pptx");
//Retrieves the slide instance.
ISlide slide = pptxDoc.Slides[0];
//Retrieves the background instance.
IBackground background = slide.Background;
//Sets the fill type of the background to gradient.
background.Fill.FillType = FillType.Gradient;
//Retrieves the fill of the background to the IGradientFill instance.
IGradientFill gradient = background.Fill.GradientFill;
//Adds the first gradient stop of the gradient fill.
gradient.GradientStops.Add(ColorObject.Green, 20);
//Adds the second gradient stop of the gradient fill.
gradient.GradientStops.Add(ColorObject.Yellow, 50);
//Saves the Presentation to the file system
pptxDoc.Save("Output.pptx");
//Closes the Presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Opens an existing Presentation.
Dim pptxDoc As IPresentation = Presentation.Open("Presentation1.pptx")
'Retrieves the slide instance.
Dim slide As ISlide = pptxDoc.Slides(0)
'Retrieves the background instance.
Dim background As IBackground = slide.Background
'Sets the fill type of the background to gradient.
background.Fill.FillType = FillType.Gradient
'Retrieves the fill of the background to the IGradientFill instance.
Dim gradient As IGradientFill = background.Fill.GradientFill
'Adds the first gradient stop of the gradient fill.
gradient.GradientStops.Add(ColorObject.Green, 20)
'Adds the second gradient stop of the gradient fill.
gradient.GradientStops.Add(ColorObject.Yellow, 50)
'Saves the Presentation to the file system
pptxDoc.Save("Output.pptx")
'Closes the Presentation
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
//Retrieves the slide instance.
ISlide slide = pptxDoc.Slides[0];
//Retrieves the background instance.
IBackground background = slide.Background;
//Sets the fill type of the background to gradient.
background.Fill.FillType = FillType.Gradient;
//Retrieves the fill of the background to the IGradientFill instance.
IGradientFill gradient = background.Fill.GradientFill;
//Adds the first gradient stop of the gradient fill.
gradient.GradientStops.Add(ColorObject.Green, 20);
//Adds the second gradient stop of the gradient fill.
gradient.GradientStops.Add(ColorObject.Yellow, 50);
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
//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream(inputFileName,FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);
//Retrieves the slide instance.
ISlide slide = pptxDoc.Slides[0];
//Retrieves the background instance.
IBackground background = slide.Background;
//Sets the fill type of the background to gradient.
background.Fill.FillType = FillType.Gradient;
//Retrieves the fill of the background to the IGradientFill instance.
IGradientFill gradient = background.Fill.GradientFill;
//Adds the first gradient stop of the gradient fill.
gradient.GradientStops.Add(ColorObject.Green, 20);
//Adds the second gradient stop of the gradient fill.
gradient.GradientStops.Add(ColorObject.Yellow, 50);
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream(OutputFileName, FileMode.Create);
pptxDoc.Save(outputStream);
//Release all resources of the stream
outputStream.Dispose();
//Closes the Presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream(resourcePath);
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);
//Retrieves the slide instance.
ISlide slide = pptxDoc.Slides[0];
//Retrieves the background instance.
IBackground background = slide.Background;
//Sets the fill type of the background to gradient.
background.Fill.FillType = FillType.Gradient;
//Retrieves the fill of the background to the IGradientFill instance.
IGradientFill gradient = background.Fill.GradientFill;
//Adds the first gradient stop of the gradient fill.
gradient.GradientStops.Add(ColorObject.Green, 20);
//Adds the second gradient stop of the gradient fill.
gradient.GradientStops.Add(ColorObject.Yellow, 50);
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Slides/Change-PowerPoint-slide-background).