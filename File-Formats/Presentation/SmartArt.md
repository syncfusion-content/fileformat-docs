---
title: Working with SmartArt in PowerPoint Presentation | Syncfusion
description: Code examples to create, edit, and format PowerPoint smartArt in C# using Syncfusion .NET PowerPoint library without Microsoft PowerPoint or interop dependencies.
platform: file-formats
control: Presentation
documentation: UG
---
# Working with SmartArt

A SmartArt diagram is a visual representation of your information, to effectively communicate your ideas in presentations. You can add and modify the SmartArt diagrams in PowerPoint presentations using Essential Presentation library.

## Adding SmartArt to a Slide

You can add any of the predefined SmartArt diagrams to PowerPoint Prknfjnfesentation. The following code example demonstrates adding a SmartArt to a Slide.

{% tabs %}

{% highlight c# tabtitle="C#" %}
// Create an instance of PowerPoint Presentation
IPresentation pptxDoc = Presentation.Create();
//Add a blank slide to the Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Add a BasicBlockList SmartArt to the slide at the specified size and position.
ISmartArt smartArt = slide.Shapes.AddSmartArt(SmartArtType.BasicBlockList, 0, 0, 640, 426); 
//Save the Presentation
pptxDoc.Save("SmartArt.pptx");
//Close the Presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Create an instance of PowerPoint Presentation
Dim pptxDoc As IPresentation = Presentation.Create()
'Add a blank slide to the Presentation
Dim slide As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank)
'Add a BasicBlockList SmartArt to the slide at the specified size and position.
Dim smartArt As ISmartArt = slide.Shapes.AddSmartArt(SmartArtType.BasicBlockList, 0, 0, 640, 426)
'Save the Presentation
pptxDoc.Save("SmartArt.pptx")
'Close the Presentation
pptxDoc.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Create an instance of PowerPoint Presentation
IPresentation pptxDoc = Presentation.Create();
//Add a blank slide to the Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Add a BasicBlockList SmartArt to the slide at the specified size and position.
ISmartArt smartArt = slide.Shapes.AddSmartArt(SmartArtType.BasicBlockList, 0, 0, 640, 426); 
//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "SmartArt";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });
//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();
//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
// Create an instance of PowerPoint Presentation
IPresentation pptxDoc = Presentation.Create();
//Add a blank slide to the Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Add a BasicBlockList SmartArt to the slide at the specified size and position.
ISmartArt smartArt = slide.Shapes.AddSmartArt(SmartArtType.BasicBlockList, 0, 0, 640, 426); 
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("SmartArt.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
//Close the Presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
// Create an instance of PowerPoint Presentation
IPresentation pptxDoc = Presentation.Create();
//Add a blank slide to the Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Add a BasicBlockList SmartArt to the slide at the specified size and position.
ISmartArt smartArt = slide.Shapes.AddSmartArt(SmartArtType.BasicBlockList, 0, 0, 640, 426); 
//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();
//Save Presentation in stream format.
pptxDoc.Save(stream);
//Close the presentation
pptxDoc.Close();
stream.Position = 0;
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("SmartArt.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("SmartArt.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
{% endhighlight %}

{% endtabs %}

## Adding a node to the SmartArt

You can add a new node to the SmartArt diagram. The following code example demonstrates the same.

{% tabs %}

{% highlight c# tabtitle="C#" %}
// Create an instance of PowerPoint Presentation
IPresentation pptxDoc = Presentation.Create();
//Add a blank slide to the Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Add a SmartArt to the slide at the specified size and position
ISmartArt smartArt = slide.Shapes.AddSmartArt(SmartArtType.AlternatingHexagons, 0, 0, 640, 426);
// Add a new node to the SmartArt.
ISmartArtNode newNode = smartArt.Nodes.Add();
// Set the text to the newly added node.
newNode.TextBody.AddParagraph("New main node added.");
//Save the Presentation.
pptxDoc.Save("SmartArt.pptx");
//Close the Presentation.
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Create an instance of PowerPoint Presentation
Dim pptxDoc As IPresentation = Presentation.Create()
'Add a blank slide to the Presentation
Dim slide As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank)
'Add a SmartArt to the slide at the specified size and position
Dim smartArt As ISmartArt = slide.Shapes.AddSmartArt(SmartArtType.AlternatingHexagons, 0, 0, 640, 426)
'Add a new node to the SmartArt.
Dim newNode As ISmartArtNode = smartArt.Nodes.Add()
'Set the text to the newly added node.
newNode.TextBody.AddParagraph("New main node added.")
'Save the Presentation.
pptxDoc.Save("SmartArt.pptx")
'Close the Presentation.
pptxDoc.Close()

{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Create an instance of PowerPoint Presentation
IPresentation pptxDoc = Presentation.Create();
//Add a blank slide to the Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Add a SmartArt to the slide at the specified size and position
ISmartArt smartArt = slide.Shapes.AddSmartArt(SmartArtType.AlternatingHexagons, 0, 0, 640, 426);
// Add a new node to the SmartArt.
ISmartArtNode newNode = smartArt.Nodes.Add();
// Set the text to the newly added node.
newNode.TextBody.AddParagraph("New main node added.");
//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "SmartArt";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });
//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();
//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
// Create an instance of PowerPoint Presentation
IPresentation pptxDoc = Presentation.Create();
//Add a blank slide to the Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Add a SmartArt to the slide at the specified size and position
ISmartArt smartArt = slide.Shapes.AddSmartArt(SmartArtType.AlternatingHexagons, 0, 0, 640, 426);
// Add a new node to the SmartArt.
ISmartArtNode newNode = smartArt.Nodes.Add();
// Set the text to the newly added node.
newNode.TextBody.AddParagraph("New main node added.");
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("SmartArt.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
//Close the Presentation.
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
// Create an instance of PowerPoint Presentation
IPresentation pptxDoc = Presentation.Create();
//Add a blank slide to the Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Add a SmartArt to the slide at the specified size and position
ISmartArt smartArt = slide.Shapes.AddSmartArt(SmartArtType.AlternatingHexagons, 0, 0, 640, 426);
// Add a new node to the SmartArt.
ISmartArtNode newNode = smartArt.Nodes.Add();
// Set the text to the newly added node.
newNode.TextBody.AddParagraph("New main node added.");
//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();
//Save Presentation in stream format.
pptxDoc.Save(stream);
//Close the presentation
pptxDoc.Close();
stream.Position = 0;
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("SmartArt.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("SmartArt.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
{% endhighlight %}

{% endtabs %}

In SmartArt diagrams, you can also add nodes to several nested levels. The maximum limit of nested levels may vary based on SmartArt types. The following code example demonstrates adding nested level nodes in a SmartArt.

{% tabs %}

{% highlight c# tabtitle="C#" %}
// Create an instance of PowerPoint Presentation
IPresentation pptxDoc = Presentation.Create();
//Add a blank slide to the Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Add a SmartArt to the slide at the specified size and position.
ISmartArt smartArt = slide.Shapes.AddSmartArt(SmartArtType.AlternatingHexagons, 0, 0, 640, 426);
// Add a new node to the SmartArt.
ISmartArtNode newNode = smartArt.Nodes.Add();
// Add a child node to the SmartArt node
ISmartArtNode childNode = newNode.ChildNodes.Add();
// Set a text to newly added child node.
childNode.TextBody.AddParagraph("Child node of the existing node.");
//Save the Presentation.
pptxDoc.Save("SmartArt.pptx");
//Close the Presentation.
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Create an instance of PowerPoint Presentation
Dim pptxDoc As IPresentation = Presentation.Create()
'Add a blank slide to the Presentation
Dim slide As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank)
'Add a SmartArt to the slide at the specified size and position.
Dim smartArt As ISmartArt = slide.Shapes.AddSmartArt(SmartArtType.AlternatingHexagons, 0, 0, 640, 426)
'Add a new node to the SmartArt.
Dim newNode As ISmartArtNode = smartArt.Nodes.Add()
'Add a child node to the SmartArt node
Dim childNode As ISmartArtNode = newNode.ChildNodes.Add()
'Set a text to newly added child node.
childNode.TextBody.AddParagraph("Child node of the existing node.")
'Save the Presentation.
pptxDoc.Save("SmartArt.pptx")
'Close the Presentation.
pptxDoc.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Create an instance of PowerPoint Presentation
IPresentation pptxDoc = Presentation.Create();
//Add a blank slide to the Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Add a SmartArt to the slide at the specified size and position.
ISmartArt smartArt = slide.Shapes.AddSmartArt(SmartArtType.AlternatingHexagons, 0, 0, 640, 426);
// Add a new node to the SmartArt.
ISmartArtNode newNode = smartArt.Nodes.Add();
// Add a child node to the SmartArt node
ISmartArtNode childNode = newNode.ChildNodes.Add();
// Set a text to newly added child node.
childNode.TextBody.AddParagraph("Child node of the existing node.");
//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "SmartArt";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });
//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();
//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
// Create an instance of PowerPoint Presentation
IPresentation pptxDoc = Presentation.Create();
//Add a blank slide to the Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Add a SmartArt to the slide at the specified size and position.
ISmartArt smartArt = slide.Shapes.AddSmartArt(SmartArtType.AlternatingHexagons, 0, 0, 640, 426);
// Add a new node to the SmartArt.
ISmartArtNode newNode = smartArt.Nodes.Add();
// Add a child node to the SmartArt node
ISmartArtNode childNode = newNode.ChildNodes.Add();
// Set a text to newly added child node.
childNode.TextBody.AddParagraph("Child node of the existing node.");
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("SmartArt.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
//Close the Presentation.
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
// Create an instance of PowerPoint Presentation
IPresentation pptxDoc = Presentation.Create();
//Add a blank slide to the Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Add a SmartArt to the slide at the specified size and position.
ISmartArt smartArt = slide.Shapes.AddSmartArt(SmartArtType.AlternatingHexagons, 0, 0, 640, 426);
// Add a new node to the SmartArt.
ISmartArtNode newNode = smartArt.Nodes.Add();
// Add a child node to the SmartArt node
ISmartArtNode childNode = newNode.ChildNodes.Add();
// Set a text to newly added child node.
childNode.TextBody.AddParagraph("Child node of the existing node.");
//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();
//Save Presentation in stream format.
pptxDoc.Save(stream);
//Close the presentation
pptxDoc.Close();
stream.Position = 0;
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("SmartArt.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("SmartArt.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
{% endhighlight %}

{% endtabs %}

## Modifying SmartArt appearance 

You can modify the SmartArt appearance by modifying the fill type, color, transparency etc. The below code example demonstrates modifying the appearance of SmartArt nodes.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Open a PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open("SampleDocument.pptx");
//Get the Slide from Presentation
ISlide slide = pptxDoc.Slides[0];
//Get the SmartArt from Slide.
ISmartArt smartArt = slide.Shapes[0] as ISmartArt;
//Get the first node
ISmartArtNode firstNode = smartArt.Nodes[0];
// Set the text content of node.
firstNode.TextBody.AddParagraph("First Node");
//Set the fill type of node.
firstNode.Shapes[0].Fill.FillType = FillType.Solid;
// Set the fill color of node.
firstNode.Shapes[0].Fill.SolidFill.Color = ColorObject.GreenYellow;
//Set  transparency value of fill
firstNode.Shapes[0].Fill.SolidFill.Transparency = 30;
//Save the Presentation.
pptxDoc.Save("SmartArt.pptx");
//Close the Presentation.
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Open a PowerPoint Presentation
Dim pptxDoc As IPresentation = Presentation.Open("SampleDocument.pptx")
'Get the Slide from Presentation
Dim slide As ISlide = pptxDoc.Slides(0)
'Get the SmartArt from Slide.
Dim smartArt As ISmartArt = TryCast(slide.Shapes(0), ISmartArt)
'Get the first node
Dim firstNode As ISmartArtNode = smartArt.Nodes(0)
' Set the text content of node.
firstNode.TextBody.AddParagraph("First Node")
'Set the fill type of node.
firstNode.Shapes(0).Fill.FillType = FillType.Solid
' Set the fill color of node.
firstNode.Shapes(0).Fill.SolidFill.Color = ColorObject.GreenYellow
'Set  transparency value of fill
firstNode.Shapes(0).Fill.SolidFill.Transparency = 30
'Save the Presentation.
pptxDoc.Save("SmartArt.pptx")
'Close the Presentation.
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
//Get the Slide from Presentation
ISlide slide = pptxDoc.Slides[0];
//Get the SmartArt from Slide.
ISmartArt smartArt = slide.Shapes[0] as ISmartArt;
//Get the first node
ISmartArtNode firstNode = smartArt.Nodes[0];
// Set the text content of node.
firstNode.TextBody.AddParagraph("First Node");
//Set the fill type of node.
firstNode.Shapes[0].Fill.FillType = FillType.Solid;
// Set the fill color of node.
firstNode.Shapes[0].Fill.SolidFill.Color = ColorObject.GreenYellow;
//Set  transparency value of fill
firstNode.Shapes[0].Fill.SolidFill.Transparency = 30;
//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "SmartArt";
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
//Get the Slide from Presentation
ISlide slide = pptxDoc.Slides[0];
//Get the SmartArt from Slide.
ISmartArt smartArt = slide.Shapes[0] as ISmartArt;
//Get the first node
ISmartArtNode firstNode = smartArt.Nodes[0];
// Set the text content of node.
firstNode.TextBody.AddParagraph("First Node");
//Set the fill type of node.
firstNode.Shapes[0].Fill.FillType = FillType.Solid;
// Set the fill color of node.
firstNode.Shapes[0].Fill.SolidFill.Color = ColorObject.GreenYellow;
//Set  transparency value of fill
firstNode.Shapes[0].Fill.SolidFill.Transparency = 30;
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("SmartArt.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
//Close the Presentation.
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Sample.pptx");
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);
//Get the Slide from Presentation
ISlide slide = pptxDoc.Slides[0];
//Get the SmartArt from Slide.
ISmartArt smartArt = slide.Shapes[0] as ISmartArt;
//Get the first node
ISmartArtNode firstNode = smartArt.Nodes[0];
// Set the text content of node.
firstNode.TextBody.AddParagraph("First Node");
//Set the fill type of node.
firstNode.Shapes[0].Fill.FillType = FillType.Solid;
// Set the fill color of node.
firstNode.Shapes[0].Fill.SolidFill.Color = ColorObject.GreenYellow;
//Set  transparency value of fill
firstNode.Shapes[0].Fill.SolidFill.Transparency = 30;
//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();
//Save Presentation in stream format.
pptxDoc.Save(stream);
//Close the presentation
pptxDoc.Close();
stream.Position = 0;
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("SmartArt.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("SmartArt.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
{% endhighlight %}

{% endtabs %}

## Iterating through child nodes of an existing SmartArt

You can iterate through the child nodes and access the properties of each node in a SmartArt. The following code example demonstrates accessing and modifying the text content of node.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Open a PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open("SampleDocument.pptx");
//Traverse through shape in the first slide.
foreach (IShape shape in pptxDoc.Slides[0].Shapes)
{
    if (shape is ISmartArt)
    {
        //Traverse through all nodes inside SmartArt
        foreach (ISmartArtNode mainNode in (shape as ISmartArt).Nodes)
        {
            if (mainNode.TextBody.Text == "Old Content")
            //Change the node content
            mainNode.TextBody.Paragraphs[0].TextParts[0].Text = "New Content";
        }
    }
}
//Save the Presentation.
pptxDoc.Save("SmartArt.pptx");
//Close the Presentation.
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Open a PowerPoint Presentation
Dim pptxDoc As IPresentation = Presentation.Open("SampleDocument.pptx")
'Traverse through shape in the first slide.
For Each shape As IShape In pptxDoc.Slides(0).Shapes
    If TypeOf shape Is ISmartArt Then
        'Traverse through all nodes inside SmartArt
        For Each mainNode As ISmartArtNode In TryCast(shape, ISmartArt).Nodes
            If mainNode.TextBody.Text = "Old Content" Then
                'Change the node content
                mainNode.TextBody.Paragraphs(0).TextParts(0).Text = "New Content"
            End If
        Next
    End If
Next
'Save the Presentation.
pptxDoc.Save("SmartArt.pptx")
'Close the Presentation.
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
//Traverse through shape in the first slide.
foreach (IShape shape in pptxDoc.Slides[0].Shapes)
{
    if (shape is ISmartArt)
    {
        //Traverse through all nodes inside SmartArt
        foreach (ISmartArtNode mainNode in (shape as ISmartArt).Nodes)
        {
            if (mainNode.TextBody.Text == "Old Content")
            //Change the node content
            mainNode.TextBody.Paragraphs[0].TextParts[0].Text = "New Content";
        }
    }
}
//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "SmartArt";
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
//Traverse through shape in the first slide.
foreach (IShape shape in pptxDoc.Slides[0].Shapes)
{
    if (shape is ISmartArt)
    {
        //Traverse through all nodes inside SmartArt
        foreach (ISmartArtNode mainNode in (shape as ISmartArt).Nodes)
        {
            if (mainNode.TextBody.Text == "Old Content")
            //Change the node content
            mainNode.TextBody.Paragraphs[0].TextParts[0].Text = "New Content";
        }
    }
}
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("SmartArt.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
//Close the Presentation.
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Sample.pptx");
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);
//Traverse through shape in the first slide.
foreach (IShape shape in pptxDoc.Slides[0].Shapes)
{
    if (shape is ISmartArt)
    {
        //Traverse through all nodes inside SmartArt
        foreach (ISmartArtNode mainNode in (shape as ISmartArt).Nodes)
        {
            if (mainNode.TextBody.Text == "Old Content")
            //Change the node content
            mainNode.TextBody.Paragraphs[0].TextParts[0].Text = "New Content";
        }
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
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("SmartArt.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("SmartArt.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
{% endhighlight %}

{% endtabs %}

## Removing node from an existing SmartArt

You can remove a node from the SmartArt diagram. The following code example demonstrates the same.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Open a PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open("SampleDocument.pptx");
//Get the first slide from the Presentation.
ISlide slide = pptxDoc.Slides[0];
//Get the SmartArt from slide.
ISmartArt smartArt = slide.Shapes[0] as ISmartArt;
//Remove a node at the specified index.
smartArt.Nodes.RemoveAt(4);
//Save the Presentation.
pptxDoc.Save("SmartArt.pptx");
//Close the Presentation.
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Open a PowerPoint Presentation
Dim pptxDoc As IPresentation = Presentation.Open("SampleDocument.pptx")
'Get the first slide from the Presentation.
Dim slide As ISlide = pptxDoc.Slides(0)
'Get the SmartArt from slide.
Dim smartArt As ISmartArt = TryCast(slide.Shapes(0), ISmartArt)
'Remove a node at the specified index.
smartArt.Nodes.RemoveAt(4)
'Save the Presentation.
pptxDoc.Save("SmartArt.pptx")
'Close the Presentation.
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
//Get the Slide from Presentation
ISlide slide = pptxDoc.Slides[0];
//Get the SmartArt from slide.
ISmartArt smartArt = slide.Shapes[0] as ISmartArt;
//Remove a node at the specified index.
smartArt.Nodes.RemoveAt(4);
//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "SmartArt";
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
//Get the first slide from the Presentation.
ISlide slide = pptxDoc.Slides[0];
//Get the SmartArt from slide.
ISmartArt smartArt = slide.Shapes[0] as ISmartArt;
//Remove a node at the specified index.
smartArt.Nodes.RemoveAt(4);
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("SmartArt.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
//Close the Presentation.
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Sample.pptx");
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);
//Get the first slide from the Presentation.
ISlide slide = pptxDoc.Slides[0];
//Get the SmartArt from slide.
ISmartArt smartArt = slide.Shapes[0] as ISmartArt;
//Remove a node at the specified index.
smartArt.Nodes.RemoveAt(4);
//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();
//Save Presentation in stream format.
pptxDoc.Save(stream);
//Close the presentation
pptxDoc.Close();
stream.Position = 0;
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("SmartArt.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("SmartArt.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
{% endhighlight %}

{% endtabs %}

## Assistant nodes in SmartArt

You can check whether a node is an assistant or not. Also you can change a node as assistant node or revert an assistant node to normal node.  The following code example demonstrates making an assistant node as normal node.

{% tabs %}

{% highlight c# tabtitle="C#" %}
// Create an instance of PowerPoint Presentation
IPresentation pptxDoc = Presentation.Create();

//Add a blank slide to the Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Add a SmartArt to the slide at the specified size and position
ISmartArt smartArt = slide.Shapes.AddSmartArt(SmartArtType.OrganizationChart, 0, 0, 640, 426.96);
//Traverse through all nodes of the SmartArt.
foreach (ISmartArtNode node in smartArt.Nodes)
{
    //Check if the node is assistant or not.
    if (node.IsAssistant)
    //Set the assistant node to false.
    node.IsAssistant = false;
}
//Save the Presentation.
pptxDoc.Save("Sample.pptx");
//Close the Presentation.
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Create an instance of PowerPoint Presentation
Dim pptxDoc As IPresentation = Presentation.Create()
'Add a blank slide to the Presentation
Dim slide As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank)
'Add a SmartArt to the slide at the specified size and position
Dim smartArt As ISmartArt = slide.Shapes.AddSmartArt(SmartArtType.OrganizationChart, 0, 0, 640, 426.96)
'Traverse through all nodes of the SmartArt.
For Each node As ISmartArtNode In smartArt.Nodes
    'Check if the node is assistant or not.
    If node.IsAssistant Then
        'Set the assistant node to false.
        node.IsAssistant = False
    End If
Next
'Save the Presentation.
pptxDoc.Save("Sample.pptx")
'Close the Presentation.
pptxDoc.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Create an instance of PowerPoint Presentation
IPresentation pptxDoc = Presentation.Create();
//Add a blank slide to the Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Add a SmartArt to the slide at the specified size and position
ISmartArt smartArt = slide.Shapes.AddSmartArt(SmartArtType.OrganizationChart, 0, 0, 640, 426.96);
//Traverse through all nodes of the SmartArt.
foreach (ISmartArtNode node in smartArt.Nodes)
{
    //Check if the node is assistant or not.
    if (node.IsAssistant)
        //Set the assistant node to false.
        node.IsAssistant = false;
} 
//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "SmartArt";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });
//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();
//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
// Create an instance of PowerPoint Presentation
IPresentation pptxDoc = Presentation.Create();
//Add a blank slide to the Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Add a SmartArt to the slide at the specified size and position
ISmartArt smartArt = slide.Shapes.AddSmartArt(SmartArtType.OrganizationChart, 0, 0, 640, 426.96);
//Traverse through all nodes of the SmartArt.
foreach (ISmartArtNode node in smartArt.Nodes)
{
    //Check if the node is assistant or not.
    if (node.IsAssistant)
        //Set the assistant node to false.
        node.IsAssistant = false;
}
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("SmartArt.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
//Close the Presentation.
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
// Create an instance of PowerPoint Presentation
IPresentation pptxDoc = Presentation.Create();
//Add a blank slide to the Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Add a SmartArt to the slide at the specified size and position
ISmartArt smartArt = slide.Shapes.AddSmartArt(SmartArtType.OrganizationChart, 0, 0, 640, 426.96);
//Traverse through all nodes of the SmartArt.
foreach (ISmartArtNode node in smartArt.Nodes)
{
    //Check if the node is assistant or not.
    if (node.IsAssistant)
        //Set the assistant node to false.
        node.IsAssistant = false;
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
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("SmartArt.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("SmartArt.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
{% endhighlight %}

{% endtabs %}

## Limitations

The modifications in a SmartArt (like add/remove nodes, modify position and size of nodes etc., which involve SmartArt layout changes) done by Essential Presentation will not reflected in Image and PDF conversion. Whereas layout changes will be reflected properly in the generated PPTX file when opened using Microsoft PowerPoint.

## Supported SmartArt layout types

1. Basic Block List
2. Alternating Hexagons
3. Picture Caption List
4. Lined List
5. Vertical Bullet List
6. Vertical Box List
7. Horizontal Bullet List
8. Square Accent List
9. Picture Accent List
10. Bending Picture Accent List
11. Stacked List
12. Increasing Circle Process
13. Pie Process
14. Detailed Process
15. Grouped List
16. Horizontal Picture List
17. Continuous Picture List
18. Picture Strips
19. Vertical Picture List
20. Alternating Picture Blocks
21. Vertical Picture Accent List
22. Titled Picture Accent List
23. Vertical Block List
24. Vertical Chevron List
25. Vertical Accent List
26. Vertical Arrow List
27. Trapezoid List
28. Descending Block List
29. Table List
30. Segmented Process
31. Vertical Curved List
32. Pyramid List
33. Target List
34. Vertical Circle List
35. Table Hierarchy
36. Basic Process
37. Step Up Process
38. Step Down Process
39. Accent Process
40. Alternating Flow
41. Continuous Block Process
42. Increasing Arrows Process
43. Continuous Arrow Process
44. Process Arrows
45. Circle Accent Time Line
46. Basic Time Line
47. Basic Chevron Process
48. Closed Chevron Process
49. Chevron List
50. Sub-Step Process
51. Phased Process
52. Random to Result Process
53. Staggered Process
54. Process List
55. Circle Arrow Process
56. Basic Bending Process
57. Vertical Bending Process
58. Ascending Picture Accent Process
59. Upward Arrow
60. Descending Process
61. Circular Bending Process
62. Equation
63. Vertical Equation
64. Funnel 
65. Gear
66. Arrow Ribbon
67. Opposing Arrows
68. Converging Arrows
69. Diverging Arrows
70. Basic Cycle
71. Text Cycle
72. Block Cycle
73. Non directional Cycle
74. Continuous Cycle
75. Multi Directional Cycle
76. Segmented Cycle
77. Basic Pie
78. Radial Cycle
79. Basic Radial
80. Diverging Radial
81. Radial Venn
82. Radial Cluster
83. Organization Chart
84. Name and Title Organization Chart
85. Half Circle Organization Chart
86. Circle Picture hierarchy
87. Hierarchy
88. Labeled Hierarchy
89. Horizontal Organization Chart
90. Horizontal Multi-Level Hierarchy
91. Horizontal Hierarchy
92. Horizontal Labeled Hierarchy
93. Balance
94. Circle Relationship
95. Hexagon Cluster
96. Opposing Ideas
97. Plus and Minus 
98. Reverse List
99. Counter Balance Arrows
100. Segmented Pyramid
101. Nested Target
102. Converging Radial 
103. Radial List
104. Basic Target
105. Basic Matrix
106. Titled Matrix
107. Grid Matrix
108. Cycle Matrix
109. Accent Picture
110. Circular Picture Callout
111. Snapshot Picture List
112. Spiral Picture
113. Captioned Pictures
114. Bending Picture Caption
115. Bending Picture-Semi Transparent Text
116. Bending Picture Blocks
117. Bending Picture Caption List
118. Titled Picture Blocks
119. Picture Grid
120. Picture Accent Blocks
121. Alternating Picture Circles
122. Title Picture Lineup
123. Picture Lineup
124. Framed Text Picture
125. Bubble Picture List
126. Basic Pyramid
127. Inverted Pyramid
128. Basic Venn
129. Linear Venn
130. Stacked Venn
131. Hierarchy List
132. Picture Accent Process
133. Repeating Bending Process
134. Vertical Process
