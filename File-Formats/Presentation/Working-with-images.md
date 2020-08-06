---
title: Add and edit images in PowerPoint slides |C# PowerPoint| |Syncfusion|
description: C# PowerPoint library to create, read, edit and convert PowerPoint files in .NET applications, ASP.NET Web, MVC, ASP.NET Core, Xamarin and Azure platforms
platform: file-formats
control: Presentation
documentation: UG
---
# Working with PowerPoint Images

## Adding Images

Essential Presentation library facilitates adding or modifying the images in a PowerPoint Presentation. The following code example demonstrates how to add a new image to the presentation.

{% tabs %}

{% highlight c# %}

//Creates a instance of Presentation
IPresentation pptxDoc = Presentation.Create();

//Adds a blank slide.
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Gets a picture as stream.
Stream pictureStream = File.Open("Image.png", FileMode.Open);

//Adds the picture to a slide by specifying its size and position.
IPicture picture = slide.Pictures.AddPicture(pictureStream, 0, 0, 250, 250);

//Saves the Presentation to the file system.
pptxDoc.Save("Sample.pptx");

//Dispose the image stream
pictureStream.Dispose();

//Closes the Presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates a instance of Presentation
Dim pptxDoc As IPresentation = Presentation.Create()

'Adds a blank slide.
Dim slide As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank)

'Gets a picture as stream.
Dim pictureStream As Stream = File.Open("Image.png", FileMode.Open)

'Adds the picture to a slide by specifying its size and position.
Dim picture As IPicture = slide.Pictures.AddPicture(pictureStream, 0, 0, 250, 250)

'Saves the Presentation to the file system.
pptxDoc.Save("Sample.pptx")

'Dispose the image stream
pictureStream.Dispose()

'Closes the Presentation
pptxDoc.Close()

{% endhighlight %}

{% highlight UWP %}

//Creates a instance of Presentation
IPresentation pptxDoc = Presentation.Create();

//Adds a blank slide.
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Gets a picture as stream.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream pictureStream = assembly.GetManifestResourceStream("UWP.Data.Image.png");

//Adds the picture to a slide by specifying its size and position.
IPicture picture = slide.Pictures.AddPicture(pictureStream, 0, 0, 250, 250);

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

//Creates a instance of Presentation
IPresentation pptxDoc = Presentation.Create();

//Adds a blank slide.
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Gets a picture as stream.
FileStream pictureStream = new FileStream("Image.png", FileMode.Open);

//Adds the picture to a slide by specifying its size and position.
IPicture picture = slide.Pictures.AddPicture(pictureStream, 0, 0, 250, 250);

//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Sample.pptx", FileMode.Create);
pptxDoc.Save(outputStream);

//Dispose the image stream
pictureStream.Dispose();

//Closes the Presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight XAMARIN %}

//Creates a instance of Presentation
IPresentation pptxDoc = Presentation.Create();

//Adds a blank slide.
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;

//Gets a picture as stream.
Stream pictureStream = assembly.GetManifestResourceStream("Image.png");

//Adds the picture to a slide by specifying its size and position.
IPicture picture = slide.Pictures.AddPicture(pictureStream, 0, 0, 250, 250);

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

## Replacing Images

The following code example demonstrates how to replace an existing image in a slide.

{% tabs %}

{% highlight c# %}

//Opens an existing Presentation.
IPresentation pptxDoc = Presentation.Open("Sample.pptx");

//Retrieves the first slide from the Presentation.
ISlide slide = pptxDoc.Slides[0];

//Retrieves the first picture from the slide.
IPicture picture = slide.Pictures[0];

//Gets the new picture as stream.
Stream pictureStream = File.Open("Image.png", FileMode.Open);

//Creates instance for memory stream
MemoryStream memoryStream = new MemoryStream();

//Copies stream to memoryStream.
pictureStream.CopyTo(memoryStream);

//Replaces the existing image with new image.
picture.ImageData = memoryStream.ToArray();

//Saves the Presentation to the file system.
pptxDoc.Save("Output.pptx");

//Closes the Presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing Presentation.
Dim pptxDoc As IPresentation = Presentation.Open("Sample.pptx")

'Retrieves the first slide from the Presentation.
Dim slide As ISlide = pptxDoc.Slides(0)

'Retrieves the first picture from the slide.
Dim picture As IPicture = slide.Pictures(0)

'Gets the new picture as stream.
Dim pictureStream As Stream = File.Open("Image.png", FileMode.Open)

'Creates instance for memory stream
Dim memoryStream As New MemoryStream()

'Copies stream to memoryStream.
pictureStream.CopyTo(memoryStream)

'Replaces the existing image with new image.
picture.ImageData = memoryStream.ToArray()

'Saves the Presentation to the file system.
pptxDoc.Save("Output.pptx")

'Closes the Presentation
pptxDoc.Close()

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

//Retrieves the first slide from the Presentation.
ISlide slide = pptxDoc.Slides[0];

//Retrieves the first picture from the slide.
IPicture picture = slide.Pictures[0];

//Gets the new picture as stream.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;

//Gets the new picture as stream.
Stream pictureStream = assembly.GetManifestResourceStream("UWP.Data.Image.png");

//Creates instance for memory stream
MemoryStream memoryStream = new MemoryStream();

//Copies stream to memoryStream.
pictureStream.CopyTo(memoryStream);

//Replaces the existing image with new image.
picture.ImageData = memoryStream.ToArray();

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

//Retrieves the first slide from the Presentation.
ISlide slide = pptxDoc.Slides[0];

//Retrieves the first picture from the slide.
IPicture picture = slide.Pictures[0];

//Gets the new picture as stream.
FileStream pictureStream = new FileStream("Image.png", FileMode.Open);

//Creates instance for memory stream
MemoryStream memoryStream = new MemoryStream();

//Copies stream to memoryStream.
pictureStream.CopyTo(memoryStream);

//Replaces the existing image with new image.
picture.ImageData = memoryStream.ToArray();

//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Output.pptx", FileMode.Create);
pptxDoc.Save(outputStream);

//Closes the Presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight XAMARIN %}

//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Sample.pptx");

//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);

//Retrieves the first slide from the Presentation.
ISlide slide = pptxDoc.Slides[0];

//Retrieves the first picture from the slide.
IPicture picture = slide.Pictures[0];

//Gets the new picture as stream.
Stream pictureStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Image.png");

//Creates instance for memory stream
MemoryStream memoryStream = new MemoryStream();

//Copies stream to memoryStream.
pictureStream.CopyTo(memoryStream);

//Replaces the existing image with new image.
picture.ImageData = memoryStream.ToArray();

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

## Adding SVG Images

SVG images can be inserted in PowerPoint slide for displaying images with accuracy when scaling or zooming page. The Essential Presentation library allows you to insert and edit an SVG image along with its fallback image.

The following code example demonstrates how to add a new SVG image into a slide.

{% tabs %}

{% highlight c# %}

//Creates an instance of Presentation
IPresentation pptxDoc = Presentation.Create();

//Adds a blank slide
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Gets a SVG image (icon) as stream
Stream svgImageStream = File.Open("Image.svg", FileMode.Open);

//Gets a fallback image as stream
Stream fallbackImageStream = File.Open("Image.png", FileMode.Open);

//Adds the icon to a slide by specifying its size and position
IPicture icon = slide.Pictures.AddPicture(svgImageStream, fallbackImageStream, 0, 0, 250, 250);

//Saves the Presentation to the file system
pptxDoc.Save("Sample.pptx");

//Dispose the fallback image stream
fallbackImageStream.Dispose();

//Dispose the SVG image stream
svgImageStream.Dispose();

//Closes the Presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates an instance of Presentation
Dim pptxDoc As IPresentation = Presentation.Create() 
 
'Adds a blank slide
Dim slide As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank) 
 
'Gets a SVG image (icon) as stream
Dim svgImageStream As Stream = File.Open("Image.svg",FileMode.Open) 
 
'Gets a fallback image as stream
Dim fallbackImageStream As Stream = File.Open("Image.png",FileMode.Open) 
 
'Adds the icon to a slide by specifying its size and position
Dim icon As IPicture = slide.Pictures.AddPicture(svgImageStream, fallbackImageStream, 0, 0, 250, 250) 
 
'Saves the Presentation to the file system
pptxDoc.Save("Sample.pptx")
 
'Dispose the fallback image stream
fallbackImageStream.Dispose()
 
'Dispose the SVG image stream
svgImageStream.Dispose()
 
'Closes the Presentation
pptxDoc.Close()

{% endhighlight %}

{% highlight UWP %}

//Creates a instance of Presentation
IPresentation pptxDoc = Presentation.Create();

//Adds a blank slide.
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Gets a SVG image (icon) as stream
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream svgImageStream = assembly.GetManifestResourceStream("UWP.Data.Image.svg");

//Gets a fallback image as stream
Stream fallbackImageStream = assembly.GetManifestResourceStream("UWP.Data.Image.png");

//Adds the icon to a slide by specifying its size and position
IPicture icon = slide.Pictures.AddPicture(svgImageStream, fallbackImageStream, 0, 0, 250, 250);

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

//Creates an instance of Presentation
IPresentation pptxDoc = Presentation.Create();

//Adds a blank slide
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Gets a SVG image (icon) as stream
FileStream svgImageStream = new FileStream("Image.svg", FileMode.Open);

//Gets a fallback image as stream
FileStream fallbackImageStream = new FileStream("Image.png", FileMode.Open);

//Adds the icon to a slide by specifying its size and position
IPicture icon = slide.Pictures.AddPicture(svgImageStream, fallbackImageStream, 0, 0, 250, 250);

//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Sample.pptx", FileMode.Create);
pptxDoc.Save(outputStream);

//Dispose the fallback image stream
fallbackImageStream.Dispose();

//Dispose the SVG image stream
svgImageStream.Dispose();

//Closes the Presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight XAMARIN %}

//Creates an instance of Presentation
IPresentation pptxDoc = Presentation.Create();

//Adds a blank slide
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;

//Gets a SVG image (icon) as stream
Stream svgImageStream = assembly.GetManifestResourceStream("Image.svg");

//Gets a fallback image as stream
Stream fallbackImageStream = assembly.GetManifestResourceStream("Image.png");

//Adds the icon to a slide by specifying its size and position
IPicture icon = slide.Pictures.AddPicture(svgImageStream, fallbackImageStream, 0, 0, 250, 250);

//Create new memory stream to save Presentation
MemoryStream stream = new MemoryStream();

//Save Presentation in stream format
pptxDoc.Save(stream);

//Dispose the fallback image stream
fallbackImageStream.Dispose();

//Dispose the SVG image stream
svgImageStream.Dispose();

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

## Replacing SVG Images

The following code example demonstrates how to replace an existing SVG image in a slide.

{% tabs %}

{% highlight c# %}

//Opens an existing Presentation
IPresentation pptxDoc = Presentation.Open("Sample.pptx");

//Retrieves the first slide from the Presentation
ISlide slide = pptxDoc.Slides[0];

//Retrieves the icon object from the slide
IPicture icon = slide.Pictures[0];

//Gets the new picture as stream
Stream pictureStream = File.Open("Image.svg", FileMode.Open);

//Creates instance for memory stream
MemoryStream memoryStream = new MemoryStream();

//Copies stream to memoryStream
pictureStream.CopyTo(memoryStream);

//Replaces the existing icon image with new image
//SvgData property will return null, if it is not an icon
icon.SvgData = memoryStream.ToArray();

//Saves the Presentation to the file system
pptxDoc.Save("Output.pptx");

//Closes the Presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing Presentation.
Dim pptxDoc As IPresentation = Presentation.Open("Sample.pptx")

'Retrieves the first slide from the Presentation
Dim slide As ISlide = pptxDoc.Slides(0)

'Retrieves the icon object from the slide
Dim icon As IPicture = slide.Pictures(0)

'Gets the new picture as stream
Dim pictureStream As Stream = File.Open("Image.svg", FileMode.Open)

'Creates instance for memory stream
Dim memoryStream As New MemoryStream()

'Copies stream to memoryStream
pictureStream.CopyTo(memoryStream)

'Replaces the existing icon image with new image
'SvgData property will return null, if it is not an icon
icon.SvgData = memoryStream.ToArray()

'Saves the Presentation to the file system
pptxDoc.Save("Output.pptx")

'Closes the Presentation
pptxDoc.Close()

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

//Retrieves the first slide from the Presentation
ISlide slide = pptxDoc.Slides[0];

//Retrieves the icon object from the slide
IPicture icon = slide.Pictures[0];

//Gets the new picture as stream
Assembly assembly = typeof(App).GetTypeInfo().Assembly;

//Gets the new picture as stream
Stream pictureStream = assembly.GetManifestResourceStream("UWP.Data.Image.svg");

//Creates instance for memory stream
MemoryStream memoryStream = new MemoryStream();

//Copies stream to memoryStream
pictureStream.CopyTo(memoryStream);

//Replaces the existing icon image with new image
//SvgData property will return null, if it is not an icon
icon.SvgData = memoryStream.ToArray();

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

//Retrieves the first slide from the Presentation
ISlide slide = pptxDoc.Slides[0];

//Retrieves the icon object from the slide
IPicture icon = slide.Pictures[0];

//Gets the new picture as stream
FileStream pictureStream = new FileStream("Image.svg", FileMode.Open);

//Creates instance for memory stream
MemoryStream memoryStream = new MemoryStream();

//Copies stream to memoryStream
pictureStream.CopyTo(memoryStream);

//Replaces the existing icon image with new image
//SvgData property will return null, if it is not an icon
icon.SvgData = memoryStream.ToArray();

//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Output.pptx", FileMode.Create);
pptxDoc.Save(outputStream);

//Closes the Presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight XAMARIN %}

//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Sample.pptx");

//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);

//Retrieves the first slide from the Presentation
ISlide slide = pptxDoc.Slides[0];

//Retrieves the icon object from the slide
IPicture icon = slide.Pictures[0];

//Gets the new picture as stream
Stream pictureStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Image.svg");

//Creates instance for memory stream
MemoryStream memoryStream = new MemoryStream();

//Copies stream to memoryStream
pictureStream.CopyTo(memoryStream);

//Replaces the existing icon image with new image
//SvgData property will return null, if it is not an icon
icon.SvgData = memoryStream.ToArray();

//Create new memory stream to save Presentation
MemoryStream stream = new MemoryStream();

//Save Presentation in stream format
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

## Removing Images

The following code example demonstrates how to remove an existing image in a PowerPoint slide.

{% tabs %}

{% highlight c# %}

//Opens an existing Presentation from file system.
IPresentation pptxDoc = Presentation.Open("Sample.pptx");

//Retrieves the first slide from Presentation
ISlide slide = pptxDoc.Slides[0];

//Iterates through the pictures collection and remove the picture named "Image".
foreach (IPicture picture in slide.Pictures)

{

	//Removes the picture from the slide.

	slide.Pictures.Remove(picture);

	break;

}

//Saves the Presentation to the file system.
pptxDoc.Save("Output.pptx");

//Closes the Presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing Presentation from file system.
Dim pptxDoc As IPresentation = Presentation.Open("Sample.pptx")

'Retrieves the first slide from Presentation
Dim slide As ISlide = pptxDoc.Slides(0)

'Iterates through the pictures collection and removes the picture named "Image".
For Each picture As IPicture In slide.Pictures

'Removes the picture from the slide.
slide.Pictures.Remove(picture)

Exit For

Next

'Saves the Presentation to the file system.
pptxDoc.Save("Output.pptx")

'Closes the Presentation
pptxDoc.Close()

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

//Iterates through the pictures collection and remove the picture named "Image".

foreach (IPicture picture in slide.Pictures)

{

	//Removes the picture from the slide.

	slide.Pictures.Remove(picture);

	break;

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

//Retrieves the first slide from Presentation
ISlide slide = pptxDoc.Slides[0];

//Iterates through the pictures collection and remove the picture named "Image".
foreach (IPicture picture in slide.Pictures)

{

	//Removes the picture from the slide.

	slide.Pictures.Remove(picture);

	break;

}

//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Output.pptx", FileMode.Create);
pptxDoc.Save(outputStream);

//Closes the Presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight XAMARIN %}

//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Sample.pptx");

//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);

//Retrieves the first slide from Presentation
ISlide slide = pptxDoc.Slides[0];

//Iterates through the pictures collection and remove the picture named "Image".
foreach (IPicture picture in slide.Pictures)

{

	//Removes the picture from the slide.

	slide.Pictures.Remove(picture);

	break;

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

