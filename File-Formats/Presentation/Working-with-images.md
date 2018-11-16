---
title: Working with images in PowerPoint Presentation
description: Working with images in PowerPoint Presentation
platform: file-formats
control: Presentation
documentation: UG
---
# Working with images

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

