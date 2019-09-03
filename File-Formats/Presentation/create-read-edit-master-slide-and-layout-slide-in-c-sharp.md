---
title: Create, read and edit Master and Layout slides in CSharp | Syncfusion
description: Create, read and edit Master slides and Layout slides in CSharp
platform: file-formats
control: PowerPoint
documentation: UG
---

# Create and edit Master and Layout slides

To get all the slides in same format, you should perform those changes in the Slide Master or Layout Master. The changes will be applied to all the slides, which inherits the master slide or layout slide.

The [Syncfusion PowerPoint library](https://www.syncfusion.com/powerpoint-framework/net) supports the following:
<ol>
<li>Access the <b>MasterSlide</b> in PowerPoint file.</li>
<li>Add <b>LayoutSlide</b> to the <b>MasterSlide</b>.</li>
<li>Customize the <b>LayoutSlide</b>.</li>
<li>Create a slide with 9 pre-defined layout slides.</li>
<li>Customize the layout slides to fit your own scenarios.</li>
</ol>

## Access the MasterSlide

In PowerPoint presentation, the **MasterSlide** is the top slide that controls all information about the theme, layout, background, color, fonts, and positioning of all slides. Using this MasterSlide, you can easily adjust the look of an existing theme or make overall changes to all your slides.

The following code example demonstrates how to access the **MasterSlide** in a PowerPoint presentation.

{% tabs %}

{% highlight c# %}
//Create a PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();
//Access the first master slide in PowerPoint file
IMasterSlide masterSlide = pptxDoc.Masters[0];
//Get the first shape name from the master slide
string shapeName = masterSlide.Shapes[0].ShapeName;
//Save the PowerPoint file
pptxDoc.Save("Sample.pptx");
//Close the Presentation instance
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net %}
'Create a PowerPoint presentation
Dim pptxDoc As IPresentation = Presentation.Create()
'Access the first master slide in PowerPoint file.
Dim masterSlide As IMasterSlide = pptxDoc.Masters(0)
'Get the first shape name from the master slide
Dim shapeName As String = masterSlide.Shapes(0).ShapeName
'Save the PowerPoint file.
pptxDoc.Save("AccessMasterSlide.pptx")
'Close the Presentation instance
pptxDoc.Close()
{% endhighlight %}

{% highlight UWP %}
//Create a PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();
//Access the first master slide in PowerPoint file
IMasterSlide masterSlide = pptxDoc.Masters[0];
//Get the first shape name from the master slide
string shapeName = masterSlide.Shapes[0].ShapeName;

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "AccessMasterSlide";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });
//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();
//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);
//Close the Presentation instance
pptxDoc.Close();
{% endhighlight %}

{% highlight ASP.NET CORE %}
//Create a PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();
//Access the first master slide in PowerPoint file
IMasterSlide masterSlide = pptxDoc.Masters[0];
//Get the first shape name from the master slide
string shapeName = masterSlide.Shapes[0].ShapeName;
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream(OutputFileName, FileMode.Create);
pptxDoc.Save(outputStream);
//Release all resources of the stream
outputStream.Dispose();
//Close the PowerPoint presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight XAMARIN %}
//Create a PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();
//Access the first master slide in PowerPoint file
IMasterSlide masterSlide = pptxDoc.Masters[0];
//Get the first shape name from the master slide
string shapeName = masterSlide.Shapes[0].ShapeName;

//Create new memory stream to save Presentation
MemoryStream stream = new MemoryStream();
//Save Presentation in stream format
pptxDoc.Save(stream);
//Close the presentation
pptxDoc.Close();
stream.Position = 0;

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Sample.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Sample.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
	
//Download the helper files from the following link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/presentation/create-read-edit-powerpoint-files-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}

## Create a custom LayoutSlide

The real-world scenarios always require more predefined templates. The Syncfusion PowerPoint library lets you build your own custom layout designs and use them to create individual slides.

The following code example demonstrates how to create new custom layout slide and access layout slide in Presentation.

{% tabs %}

{% highlight c# %}
//Create a PowerPoint instance
IPresentation pptxDoc = Presentation.Create();

//Add a new LayoutSlide to the PowerPoint file
ILayoutSlide layoutSlide = pptxDoc.Masters[0].LayoutSlides.Add(SlideLayoutType.Blank, "CustomLayout");
//Add a shape to the LayoutSlide
IShape shape = layoutSlide.Shapes.AddShape(AutoShapeType.Diamond, 30, 20, 400, 300);
//Change the background color for LayoutSlide
layoutSlide.Background.Fill.SolidFill.Color = ColorObject.FromArgb(78, 89, 90);

//Save the PowerPoint file
pptxDoc.Save("LayoutSlide.pptx");
//Close the Presentation instance
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net %}
'Creates a PowerPoint instance
Dim pptxDoc As IPresentation = Presentation.Create()

'Add a new LayoutSlide to the PowerPoint file
Dim layoutSlide As ILayoutSlide = pptxDoc.Masters(0).LayoutSlides.Add(SlideLayoutType.Blank, "CustomLayout")
'Add a shape to the LayoutSlide
Dim shape As IShape = layoutSlide.Shapes.AddShape(AutoShapeType.Diamond, 30, 20, 400, 300)
'Change the background color for LayoutSlide
layoutSlide.Background.Fill.SolidFill.Color = ColorObject.FromArgb(78, 89, 90)

'Save the PowerPoint file
pptxDoc.Save("LayoutSlide.pptx")
'Close the Presentation instance
pptxDoc.Close()
{% endhighlight %}

{% highlight UWP %}
//Create a PowerPoint instance
IPresentation pptxDoc = Presentation.Create();

//Add a new LayoutSlide to the PowerPoint file
ILayoutSlide layoutSlide = pptxDoc.Masters[0].LayoutSlides.Add(SlideLayoutType.Blank, "CustomLayout");
//Add a shape to the LayoutSlide
IShape shape = layoutSlide.Shapes.AddShape(AutoShapeType.Diamond, 30, 20, 400, 300);
//Change the background color for LayoutSlide
layoutSlide.Background.Fill.SolidFill.Color = ColorObject.FromArgb(78, 89, 90);

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "LayoutSlide";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });
//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);
//Close the Presentation instance
pptxDoc.Close();
{% endhighlight %}

{% highlight ASP.NET CORE %}
//Create a PowerPoint instance
IPresentation pptxDoc = Presentation.Create();

//Add a new LayoutSlide to the PowerPoint file
ILayoutSlide layoutSlide = pptxDoc.Masters[0].LayoutSlides.Add(SlideLayoutType.Blank, "CustomLayout");
//Add a shape to the LayoutSlide
IShape shape = layoutSlide.Shapes.AddShape(AutoShapeType.Diamond, 30, 20, 400, 300);
//Change the background color for LayoutSlide
layoutSlide.Background.Fill.SolidFill.Color = ColorObject.FromArgb(78, 89, 90);

//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream(OutputFileName, FileMode.Create);
pptxDoc.Save(outputStream);
//Release all resources of the stream
outputStream.Dispose();
//Close the PowerPoint presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight XAMARIN %}
//Create a PowerPoint instance
IPresentation pptxDoc = Presentation.Create();

//Add a new LayoutSlide to the PowerPoint file
ILayoutSlide layoutSlide = pptxDoc.Masters[0].LayoutSlides.Add(SlideLayoutType.Blank, "CustomLayout");
//Add a shape to the LayoutSlide
IShape shape = layoutSlide.Shapes.AddShape(AutoShapeType.Diamond, 30, 20, 400, 300);
//Change the background color for LayoutSlide
layoutSlide.Background.Fill.SolidFill.Color = ColorObject.FromArgb(78, 89, 90);

//Create new memory stream to save Presentation
MemoryStream stream = new MemoryStream();
//Save Presentation in stream format
pptxDoc.Save(stream);
//Close the presentation
pptxDoc.Close();
stream.Position = 0;

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Sample.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Sample.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
	
//Download the helper files from the following link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/presentation/create-read-edit-powerpoint-files-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}