---
title: Working with shapes in PowerPoint Presentation | Syncfusion |
description: Code examples to create, edit, and format PowerPoint shapes in C# using Syncfusion .NET PowerPoint library without Microsoft PowerPoint or interop dependencies.
platform: file-formats
control: Presentation
documentation: UG
---
# Working with PowerPoint Shapes

## Adding shapes to a slide

In every slide, there is a shape collection that can contain any form of graphical objects such as AutoShape, chart, text, or picture.  You can add any shape element to this collection. The [IShape](https://help.syncfusion.com/cr/file-formats/Syncfusion.Presentation.IShape.html) is the base type for the shape elements.

The following code example demonstrates how to add an AutoShape and image to the shape collection of a slide.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Creates an instance for PowerPoint
IPresentation pptxDoc = Presentation.Create();
//Adds a blank slide to Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Adds normal shape to slide
slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300);
//Creates an instance for image as stream
Stream imageStream = File.Open("Image.jpg", FileMode.Open);
//Add picture to the shape collection
IPicture picture = slide.Shapes.AddPicture(imageStream, 373, 83, 526, 382);
//Saves the Presentation
pptxDoc.Save("Sample.pptx");
//Closes the stream
imageStream.Close();
//Closes the Presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Creates an instance for PowerPoint Presentation
Dim pptxDoc As IPresentation = Presentation.Create()
'Adds a blank slide to Presentation
Dim slide As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank)
'Adds normal shape to slide
slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300)
'Creates an instance for image as stream
Dim imageStream As Stream = File.Open("Image.jpg", FileMode.Open)
'Adds picture to the shape collection
Dim picture As IPicture = slide.Shapes.AddPicture(imageStream, 373, 83, 500, 382)
'Saves the Presentation
pptxDoc.Save("Sample.pptx")
'Closes the stream
imageStream.Close()
'Closes the Presentation
pptxDoc.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Creates an instance for PowerPoint
IPresentation pptxDoc = Presentation.Create();
//Adds a blank slide to Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Adds normal shape to slide
slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300);
//Creates an instance for image as stream
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream pictureStream = assembly.GetManifestResourceStream("UWP.Data.Image.jpg");
//Add picture to the shape collection
IPicture picture = slide.Shapes.AddPicture(pictureStream, 373, 83, 526, 382);
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
//Creates an instance for PowerPoint
IPresentation pptxDoc = Presentation.Create();
//Adds a blank slide to Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Adds normal shape to slide
slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300);
//Creates an instance for image as stream
FileStream imageStream = new FileStream(imagePath, FileMode.Open);
//Add picture to the shape collection
IPicture picture = slide.Shapes.AddPicture(imageStream, 373, 83, 526, 382);
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Sample.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
//Closes the stream
imageStream.Close();
//Closes the Presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Creates an instance for PowerPoint
IPresentation pptxDoc = Presentation.Create();
//Adds a blank slide to Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank); 
//Adds normal shape to slide
slide.Shapes.AddShape(AutoShapeType.Cube, 50, 200, 300, 300);
//Creates an instance for image as stream
Stream imageStream = assembly.GetManifestResourceStream(picturePath);
//Add picture to the shape collection
IPicture picture = slide.Shapes.AddPicture(imageStream, 373, 83, 526, 382);
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
//Closes the stream
imageStream.Close();
{% endhighlight %}

{% endtabs %}

## Iterating through shapes

You can iterate through the shapes in a PowerPoint slide. The following code example demonstrates how to iterate through the shapes present in a slide for modifying its properties.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Opens an existing Presentation from the file system
IPresentation pptxDoc = Presentation.Open("Sample.pptx");
//Iterates through shapes in a slide and sets title
foreach(IShape shape in pptxDoc.Slides[0].Shapes)
{
    if (shape is IPicture)
        shape.Title = "Picture";
    else if (shape is IShape)
        shape.Title = "AutoShape";
}
//Saves the Presentation
pptxDoc.Save("Output.pptx");
//Closes the Presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Opens an existing Presentation from the file system
Dim pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
'Iterates through shapes in a slide and sets title
For Each shape As IShape In pptxDoc.Slides(0).Shapes
    If TypeOf shape Is IPicture Then
        shape.Title = "Picture"
    ElseIf TypeOf shape Is IShape Then
        shape.Title = "AutoShape"
    End If
Next
'Saves the Presentation
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
//Iterates through shapes in a slide and sets title
foreach(IShape shape in pptxDoc.Slides[0].Shapes)
{
    if (shape is IPicture)
        shape.Title = "Picture";
    else if (shape is IShape)
        shape.Title = "AutoShape";
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
//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream("Sample.pptx",FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);
//Iterates through shapes in a slide and sets title
foreach(IShape shape in pptxDoc.Slides[0].Shapes)
{
    if (shape is IPicture)
        shape.Title = "Picture";
    else if (shape is IShape)
        shape.Title = "AutoShape";
}
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Output.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
//Closes the Presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream fileStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Sample.pptx");
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);
//Iterates through shapes in a slide and sets title
foreach(IShape shape in pptxDoc.Slides[0].Shapes)
{
    if (shape is IPicture)
        shape.Title = "Picture";
    else if (shape is IShape)
        shape.Title = "AutoShape";
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

## Specifying shape properties

The shape properties can be used to format and modify the shapes in a slide. The following code example demonstrates how to apply formatting to a shape.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Creates instance for PowerPoint
IPresentation pptxDoc = Presentation.Open("Sample.pptx");
//Gets the first slide of the Presentation
ISlide slide = pptxDoc.Slides[0];
//Gets the shape of the slide
IShape shape = slide.Shapes[0] as IShape;
//Sets the shape name.
shape.ShapeName = "Shape1";
//Retrieves the line format of the shape.
ILineFormat lineFormat = shape.LineFormat;
//Sets the dash style of the line format.
lineFormat.DashStyle = LineDashStyle.DashDotDot;
//Sets the weight of the line format.
lineFormat.Weight = 3;
//Sets the pattern fill type to shape
shape.Fill.FillType = FillType.Pattern;
//Chooses the type of pattern 
shape.Fill.PatternFill.Pattern = PatternFillType.DashedDownwardDiagonal;
//Sets the fore color
shape.Fill.PatternFill.ForeColor = ColorObject.AliceBlue;
//Sets the back color
shape.Fill.PatternFill.BackColor = ColorObject.DarkSalmon;
//Saves the Presentation
pptxDoc.Save("Output.pptx");
//Closes the Presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Creates instance for PowerPoint
Dim pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
'Gets the first slide of the Presentation
Dim slide As ISlide = pptxDoc.Slides(0)
'Gets the shape of the slide
Dim shape As IShape = TryCast(slide.Shapes(0), IShape)
'Sets the shape name.
shape.ShapeName = "Shape1"
'Retrieves the line format of the shape.
Dim lineFormat As ILineFormat = shape.LineFormat
'Sets the dash style of the line format.
lineFormat.DashStyle = LineDashStyle.DashDotDot
'Sets the weight of the line format.
lineFormat.Weight = 3
'Sets the pattern fill type to shape
shape.Fill.FillType = FillType.Pattern
'Chooses the type of pattern 
shape.Fill.PatternFill.Pattern = PatternFillType.DashedDownwardDiagonal
'Sets the fore color
shape.Fill.PatternFill.ForeColor = ColorObject.AliceBlue
'Sets the back color
shape.Fill.PatternFill.BackColor = ColorObject.DarkSalmon
'Saves the Presentation
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
//Gets the first slide of the Presentation
ISlide slide = pptxDoc.Slides[0];
//Gets the shape of the slide
IShape shape = slide.Shapes[0] as IShape;
//Sets the shape name.
shape.ShapeName = "Shape1";
//Retrieves the line format of the shape.
ILineFormat lineFormat = shape.LineFormat;
//Sets the dash style of the line format.
lineFormat.DashStyle = LineDashStyle.DashDotDot;
//Sets the weight of the line format.
lineFormat.Weight = 3;
//Sets the pattern fill type to shape
shape.Fill.FillType = FillType.Pattern;
//Chooses the type of pattern 
shape.Fill.PatternFill.Pattern = PatternFillType.DashedDownwardDiagonal;
//Sets the fore color
shape.Fill.PatternFill.ForeColor = ColorObject.AliceBlue;
//Sets the back color
shape.Fill.PatternFill.BackColor = ColorObject.DarkSalmon;
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
FileStream inputStream = new FileStream("Sample.pptx",FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);
//Gets the first slide of the Presentation
ISlide slide = pptxDoc.Slides[0];
//Gets the shape of the slide
IShape shape = slide.Shapes[0] as IShape;
//Sets the shape name.
shape.ShapeName = "Shape1";
//Retrieves the line format of the shape.
ILineFormat lineFormat = shape.LineFormat;
//Sets the dash style of the line format.
lineFormat.DashStyle = LineDashStyle.DashDotDot;
//Sets the weight of the line format.
lineFormat.Weight = 3;
//Sets the pattern fill type to shape
shape.Fill.FillType = FillType.Pattern;
//Chooses the type of pattern 
shape.Fill.PatternFill.Pattern = PatternFillType.DashedDownwardDiagonal;
//Sets the fore color
shape.Fill.PatternFill.ForeColor = ColorObject.AliceBlue;
//Sets the back color
shape.Fill.PatternFill.BackColor = ColorObject.DarkSalmon;
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Output.pptx", FileMode.Create);
pptxDoc.Save(outputStream);         
//Closes the Presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream fileStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Sample.pptx");
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);
//Gets the first slide of the Presentation
ISlide slide = pptxDoc.Slides[0];
//Gets the shape of the slide
IShape shape = slide.Shapes[0] as IShape;
//Sets the shape name.
shape.ShapeName = "Shape1";
//Retrieves the line format of the shape.
ILineFormat lineFormat = shape.LineFormat;
//Sets the dash style of the line format.
lineFormat.DashStyle = LineDashStyle.DashDotDot;
//Sets the weight of the line format.
lineFormat.Weight = 3;
//Sets the pattern fill type to shape
shape.Fill.FillType = FillType.Pattern;
//Chooses the type of pattern 
shape.Fill.PatternFill.Pattern = PatternFillType.DashedDownwardDiagonal;
//Sets the fore color
shape.Fill.PatternFill.ForeColor = ColorObject.AliceBlue;
//Sets the back color
shape.Fill.PatternFill.BackColor = ColorObject.DarkSalmon;
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

## Removing the shapes

The shapes can be removed from a slide by its instance or by its index position in the shape collection. The following code example demonstrates how to remove the shapes from a slide. 

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Opens an existing Presentation from file system
IPresentation pptxDoc = Presentation.Open("Sample.pptx");
//Retrieves the first slide from Presentation
ISlide slide = pptxDoc.Slides[0];
//Retrieves the first shape.
IShape shape = slide.Shapes[0] as IShape;
//Removes the shape from the shape collection.
slide.Shapes.Remove(shape);
//Saves the Presentation to the file system.
pptxDoc.Save("Result.pptx");
//Closes the Presentation.
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Opens an existing Presentation from file system
Dim pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
'Retrieves the first slide from Presentation
Dim slide As ISlide = pptxDoc.Slides(0)
'Retrieves the first shape.
Dim shape As IShape = TryCast(slide.Shapes(0), IShape)
'Removes the shape from the shape collection.
slide.Shapes.Remove(shape)
'Saves the Presentation to the file system.
pptxDoc.Save("Result.pptx")
'Closes the Presentation.
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
//Retrieves the first slide from Presentation
ISlide slide = pptxDoc.Slides[0];
//Retrieves the first shape.
IShape shape = slide.Shapes[0] as IShape;
//Removes the shape from the shape collection.
slide.Shapes.Remove(shape);
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

{% highlight c# tabtitle="ASP.NET Core" %}
//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream("Sample.pptx",FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);
//Retrieves the first slide from Presentation
ISlide slide = pptxDoc.Slides[0];
//Retrieves the first shape.
IShape shape = slide.Shapes[0] as IShape;
//Removes the shape from the shape collection.
slide.Shapes.Remove(shape);
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Output.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
//Closes the Presentation.
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream fileStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Sample.pptx");
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);
//Retrieves the first slide from Presentation
ISlide slide = pptxDoc.Slides[0];
//Retrieves the first shape.
IShape shape = slide.Shapes[0] as IShape;
//Removes the shape from the shape collection.
slide.Shapes.Remove(shape);
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

## Working with GroupShape

### Creating a GroupShape

The shapes in a slide can be grouped into a single shape. The following code snippet demonstrates how to group different slide items into a single [GroupShape](https://help.syncfusion.com/cr/file-formats/Syncfusion.Presentation.IGroupShape.html).

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Creates an instance for PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();
//Adds a blank slide to presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Adds a group shape to the slide
IGroupShape groupShape = slide.GroupShapes.AddGroupShape(20, 20, 450, 300);
//Adds a TextBox to the group shape
groupShape.Shapes.AddTextBox(30, 25, 100, 100).TextBody.AddParagraph("My TextBox");
//Gets the image stream
Stream pictureStream = File.Open("Image.png", FileMode.Open);
//Adds a picture to the group shape
groupShape.Shapes.AddPicture(pictureStream, 40, 100, 100, 100);
//Adds a shape to the group shape
groupShape.Shapes.AddShape(AutoShapeType.Rectangle, 200, 200, 90, 30);
//Save the presentation
pptxDoc.Save("Output.pptx");
//Close the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Creates an instance for PowerPoint presentation
Dim pptxDoc As IPresentation = Presentation.Create()
'Adds a blank slide to presentation
Dim slide As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank)
'Adds a group shape to the slide
Dim groupShape As IGroupShape = slide.GroupShapes.AddGroupShape(20, 20, 450, 300)
'Adds a TextBox to the group shape
groupShape.Shapes.AddTextBox(30, 25, 100, 100).TextBody.AddParagraph("My TextBox")
'Gets the image stream
Dim pictureStream As Stream = File.Open("Image.png", FileMode.Open)
'Adds a picture to the group shape
groupShape.Shapes.AddPicture(pictureStream, 40, 100, 100, 100)
'Adds a shape to the group shape
groupShape.Shapes.AddShape(AutoShapeType.Rectangle, 200, 200, 90, 30)
'Saves the presentation
pptxDoc.Save("Output.pptx")
'Closes the presentation
pptxDoc.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Creates an instance for PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();
//Adds a blank slide to presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Adds a group shape to the slide
IGroupShape groupShape = slide.GroupShapes.AddGroupShape(20, 20, 450, 300);
//Adds a TextBox to the group shape
groupShape.Shapes.AddTextBox(30, 25, 100, 100).TextBody.AddParagraph("My TextBox");
//Gets the image stream
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream pictureStream = assembly.GetManifestResourceStream("UWP.Data.Image.png");
//Adds a picture to the group shape
groupShape.Shapes.AddPicture(pictureStream, 40, 100, 100, 100);
//Adds a shape to the group shape
groupShape.Shapes.AddShape(AutoShapeType.Rectangle, 200, 200, 90, 30);
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
//Creates an instance for PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();
//Adds a blank slide to presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Adds a group shape to the slide
IGroupShape groupShape = slide.GroupShapes.AddGroupShape(20, 20, 450, 300);
//Adds a TextBox to the group shape
groupShape.Shapes.AddTextBox(30, 25, 100, 100).TextBody.AddParagraph("My TextBox");
//Gets the image stream
FileStream pictureStream = new FileStream(imagePath, FileMode.Open);
//Adds a picture to the group shape
groupShape.Shapes.AddPicture(pictureStream, 40, 100, 100, 100);
//Adds a shape to the group shape
groupShape.Shapes.AddShape(AutoShapeType.Rectangle, 200, 200, 90, 30);
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Sample.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
//Close the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Creates an instance for PowerPoint presentation
IPresentation pptxDoc = Presentation.Create();
//Adds a blank slide to presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Adds a group shape to the slide
IGroupShape groupShape = slide.GroupShapes.AddGroupShape(20, 20, 450, 300);
//Adds a TextBox to the group shape
groupShape.Shapes.AddTextBox(30, 25, 100, 100).TextBody.AddParagraph("My TextBox");
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Gets the image stream
Stream pictureStream = assembly.GetManifestResourceStream(picturePath);
//Adds a picture to the group shape
groupShape.Shapes.AddPicture(pictureStream, 40, 100, 100, 100);
//Adds a shape to the group shape
groupShape.Shapes.AddShape(AutoShapeType.Rectangle, 200, 200, 90, 30);
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

### Iterating and modifying a particular GroupShape

You can iterate through the shape collection of a [GroupShape](https://help.syncfusion.com/cr/file-formats/Syncfusion.Presentation.IGroupShape.html). Below code snippet demonstrates how to iterate through the shapes of a [GroupShape](https://help.syncfusion.com/cr/file-formats/Syncfusion.Presentation.IGroupShape.html) to modify it by removing a specific shape.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Opens a PowerPoint presentation with group shapes
IPresentation pptxDoc = Presentation.Open("Sample.pptx");
//Retrieves the first slide
ISlide slide = pptxDoc.Slides[0];
//Retrieves the first group shape of the slide
IGroupShape groupShape = slide.GroupShapes[0];
//Creates an instance to hold shape collection
IShapes shapes = groupShape.Shapes;
//Iterates the shape collection to remove the picture in a group shape
foreach (IShape shape in shapes)
{
    if (shape.SlideItemType == SlideItemType.Picture)
    {
        shapes.Remove(shape);
        break;
    }
}
//Saves the presentation
pptxDoc.Save("Output.pptx");
//Closes the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Opens a PowerPoint presentation with group shapes
Dim pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
'Retrieves the first slide
Dim slide As ISlide = pptxDoc.Slides(0)
'Retrieves the first group shape of the slide
Dim groupShape As IGroupShape = slide.GroupShapes(0)
'Creates an instance to hold shape collection
Dim shapes As IShapes = groupShape.Shapes
'Iterates shape collection to remove the picture in a group shape
For Each shape As IShape In shapes
    If shape.SlideItemType = SlideItemType.Picture Then
        shapes.Remove(shape)
        Exit For
    End If
Next
'Saves the presentation
pptxDoc.Save("Output.pptx")
'Closes the presentation
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
//Retrieves the first slide
ISlide slide = pptxDoc.Slides[0];
//Retrieves the first group shape of the slide
IGroupShape groupShape = slide.GroupShapes[0];
//Creates an instance to hold shape collection
IShapes shapes = groupShape.Shapes;
//Iterates the shape collection to remove the picture in a group shape
foreach (IShape shape in shapes)
{
    if (shape.SlideItemType == SlideItemType.Picture)
    {
        shapes.Remove(shape);
        break;
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
//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream("Sample.pptx",FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);
//Retrieves the first slide
ISlide slide = pptxDoc.Slides[0];
//Retrieves the first group shape of the slide
IGroupShape groupShape = slide.GroupShapes[0];
//Creates an instance to hold shape collection
IShapes shapes = groupShape.Shapes;
//Iterates the shape collection to remove the picture in a group shape
foreach (IShape shape in shapes)
{
    if (shape.SlideItemType == SlideItemType.Picture)
    {
        shapes.Remove(shape);
        break;
    }
}
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Output.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
//Closes the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream fileStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Sample.pptx");
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);
//Retrieves the first slide
ISlide slide = pptxDoc.Slides[0];
//Retrieves the first group shape of the slide
IGroupShape groupShape = slide.GroupShapes[0];
//Creates an instance to hold shape collection
IShapes shapes = groupShape.Shapes;
//Iterates the shape collection to remove the picture in a group shape
foreach (IShape shape in shapes)
{
    if (shape.SlideItemType == SlideItemType.Picture)
    {
        shapes.Remove(shape);
        break;
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

###  Removing a GroupShape

[GroupShape](https://help.syncfusion.com/cr/file-formats/Syncfusion.Presentation.IGroupShape.html) can be removed from a slide using its instance or by its index position in the [GroupShape](https://help.syncfusion.com/cr/file-formats/Syncfusion.Presentation.IGroupShape.html) collection of the slide. Below code snippet explains how to remove a [GroupShape](https://help.syncfusion.com/cr/file-formats/Syncfusion.Presentation.IGroupShape.html) from a slide.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Opens a PowerPoint presentation with group shapes
IPresentation pptxDoc = Presentation.Open("Sample.pptx");
//Retrieves the first slide
ISlide slide = pptxDoc.Slides[0];
//Retrieves the first group shape of the slide
IGroupShape groupShape = slide.GroupShapes[0];
//Removes the group shape from group shape collection
slide.GroupShapes.Remove(groupShape);
//Saves the presentation
pptxDoc.Save("Output.pptx");
//Closes the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Opens a PowerPoint presentation with group shapes
Dim pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
'Retrieves the first slide
Dim slide As ISlide = pptxDoc.Slides(0)
'Retrieves the first group shape of the slide
Dim groupShape As IGroupShape = slide.GroupShapes(0)
'Removes the group shape from group shape collection
slide.GroupShapes.Remove(groupShape)
'Saves the presentation
pptxDoc.Save("Output.pptx")
'Closes the presentation
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
//Retrieves the first slide
ISlide slide = pptxDoc.Slides[0];
//Retrieves the first group shape of the slide
IGroupShape groupShape = slide.GroupShapes[0];
//Removes the group shape from group shape collection
slide.GroupShapes.Remove(groupShape);
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
FileStream inputStream = new FileStream("Sample.pptx",FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);
//Retrieves the first slide
ISlide slide = pptxDoc.Slides[0];
//Retrieves the first group shape of the slide
IGroupShape groupShape = slide.GroupShapes[0];
//Removes the group shape from group shape collection
slide.GroupShapes.Remove(groupShape);
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Output.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
//Closes the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream fileStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Sample.pptx");
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);
//Retrieves the first slide
ISlide slide = pptxDoc.Slides[0];
//Retrieves the first group shape of the slide
IGroupShape groupShape = slide.GroupShapes[0];
//Removes the group shape from group shape collection
slide.GroupShapes.Remove(groupShape);
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

N> The Presentation library do not have support for converting the auto-shapes with modified adjustment values in PowerPoint presentation to image or PDF conversion. To know more about adjustment values in PowerPoint shapes please click [here](https://msdn.microsoft.com/en-us/library/office/aa220882(v=office.11).aspx).