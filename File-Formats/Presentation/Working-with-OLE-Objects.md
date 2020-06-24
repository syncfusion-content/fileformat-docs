---
title: Create and edit OLE Objects in PowerPoint files |Syncfusion|
description: Create and edit OLE Objects in PowerPoint files; Insert and open a embedded OLE object in PowerPoint Presentation
platform: file-formats
control: Presentation
documentation: UG
keywords: OLE Object in PowerPoint presentation
---
# Working with OLE Objects

The OLE Object enables sharing of application objects written in different file formats. In PowerPoint presentation the application data can be inserted into a PowerPoint slide using the [programmatic identifier](https://msdn.microsoft.com/en-us/library/aa171170(v=office.11).aspx#) of each file format.

## Inserting OLE Object to a Slide

The below code snippet demonstrates how to add an Excel worksheet into a slide.

{% tabs %}

{% highlight c# %}

//Create new instance of PowerPoint presentation. [Equivalent to launching MS PowerPoint with no slides].
IPresentation pptxDoc = Presentation.Create();

//Add slide with blank layout to presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Get the excel file as stream
Stream excelStream = File.Open("OleTemplate.xlsx", FileMode.Open);

//Image to be displayed, This can be any image
Stream imageStream = File.Open("OlePicture.png", FileMode.Open);

//Add an OLE object to the slide
IOleObject oleObject = slide.Shapes.AddOleObject(imageStream, "Excel.Sheet.12", excelStream);

//Set size and position of the OLE object
oleObject.Left = 10;
oleObject.Top = 10;
oleObject.Width = 400;
oleObject.Height = 300;

//Save the presentation
pptxDoc.Save("OleObjectSample.pptx");

//Close the presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight vb.net %}

'Create new instance of PowerPoint presentation. [Equivalent to launching MS PowerPoint with no slides].
Dim pptxDoc As IPresentation = Presentation.Create()

'Add slide with blank layout to presentation
Dim slide As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank)

'Get the excel file as stream
Dim excelStream As Stream = File.Open("OleTemplate.xlsx", FileMode.Open)

'Image to be displayed, This can be any image
Dim imageStream As Stream = File.Open("OlePicture.png", FileMode.Open)

'Add an OLE object to the slide
Dim oleObject As IOleObject = slide.Shapes.AddOleObject(imageStream, "Excel.Sheet.12", excelStream)

'Set size and position of the OLE object
oleObject.Left = 10
oleObject.Top = 10
oleObject.Width = 400
oleObject.Height = 300

'Save the presentation
pptxDoc.Save("OleObjectSample.pptx")

'Close the presentation
pptxDoc.Close()

{% endhighlight %}

{% highlight UWP %}

//Create new instance of PowerPoint presentation. [Equivalent to launching MS PowerPoint with no slides].
IPresentation pptxDoc = Presentation.Create();

//Add slide with blank layout to presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Get the excel file as stream
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream excelStream = assembly.GetManifestResourceStream("UWP.Data.OleTemplate.xlsx");

//Image to be displayed, This can be any image
Stream imageStream = assembly.GetManifestResourceStream("UWP.Data.OlePicture.png");

//Add an OLE object to the slide
IOleObject oleObject = slide.Shapes.AddOleObject(imageStream, "Excel.Sheet.12", excelStream);

//Set size and position of the OLE object
oleObject.Left = 10;
oleObject.Top = 10;
oleObject.Width = 400;
oleObject.Height = 300;

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "OleObjectSample";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);

{% endhighlight %}

{% highlight ASP.NET CORE %}

//Create new instance of PowerPoint presentation.
IPresentation pptxDoc = Presentation.Create();

//Add slide with blank layout to presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Get the excel file as stream
FileStream excelStream = new FileStream("OleTemplate.xlsx", FileMode.Open);

//Image to be displayed, This can be any image
FileStream excelStream = new FileStream("OlePicture.png", FileMode.Open);

//Add an OLE object to the slide
IOleObject oleObject = slide.Shapes.AddOleObject(imageStream, "Excel.Sheet.12", excelStream);

//Set size and position of the OLE object
oleObject.Left = 10;
oleObject.Top = 10;
oleObject.Width = 400;
oleObject.Height = 300;

//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("OleObjectSample.pptx", FileMode.Create);
pptxDoc.Save(outputStream);

//Close the presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight XAMARIN %}

//Create new instance of PowerPoint presentation.
IPresentation pptxDoc = Presentation.Create();

//Add slide with blank layout to presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;

//Get the excel file as stream
Stream excelStream = assembly.GetManifestResourceStream("OleTemplate.xlsx");

//Image to be displayed, This can be any image
Stream imageStream = assembly.GetManifestResourceStream("OlePicture.png");

//Add an OLE object to the slide
IOleObject oleObject = slide.Shapes.AddOleObject(imageStream, "Excel.Sheet.12", excelStream);

//Set size and position of the OLE object
oleObject.Left = 10;
oleObject.Top = 10;
oleObject.Width = 400;
oleObject.Height = 300;

//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();

//Save Presentation in stream format.
pptxDoc.Save(stream);

//Close the presentation
pptxDoc.Close();
stream.Position = 0;

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("OleObjectSample.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("OleObjectSample.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);

{% endhighlight %}

{% endtabs %}

## Extract embedded OLE Object data

The below code snippet demonstrates how to extract embedded OLE Object data.

{% tabs %}

{% highlight c# %}

//Opens the specified presentation
IPresentation pptxDoc = Presentation.Open("EmbeddedOleObject.pptx");
//Gets the first slide of the Presentation
ISlide slide = pptxDoc.Slides[0];
//Gets the Ole Object of the slide
IOleObject oleObject = slide.Shapes[2] as IOleObject;
//Gets the file data of embedded Ole Object
byte[] array = oleObject.ObjectData;
//Gets the file Name of OLE Object
string outputFile = oleObject.FileName;
//Save the extracted Ole data into file system
MemoryStream memoryStream = new MemoryStream(array);
FileStream fileStream = File.Create(outputFile);
memoryStream.CopyTo(fileStream);
memoryStream.Dispose();
fileStream.Dispose();
//Close the presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens the specified presentation
Dim pptxDoc As IPresentation = Presentation.Open("EmbeddedOleObject.pptx")
'Gets the first slide of the Presentation
Dim slide As ISlide = pptxDoc.Slides(0)
'Gets the Ole Object of the slide
Dim oleObject As IOleObject = CType(slide.Shapes(2),IOleObject)
'Gets the file data of embedded Ole Object
Dim array() As Byte = oleObject.ObjectData
'Gets the file Name of OLE Object
Dim outputFile As String = oleObject.FileName
'Save the extracted Ole data into file system
Dim memoryStream As MemoryStream = New MemoryStream(array)
Dim fileStream As FileStream = File.Create(outputFile)
memoryStream.CopyTo(fileStream)
memoryStream.Dispose
fileStream.Dispose
'Close the presentation
pptxDoc.Close

{% endhighlight %}

{% highlight UWP %}

//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputFileStream = assembly.GetManifestResourceStream("Sample.Data.EmbeddedOleObject.pptx");
//Opens the specified presentation
IPresentation pptxDoc = Presentation.Open(inputFileStream);
//Gets the first slide of the Presentation
ISlide slide = pptxDoc.Slides[0];
//Gets the Ole Object of the slide
IOleObject oleObject = slide.Shapes[2] as IOleObject;
//Gets the file data of embedded Ole Object
byte[] array = oleObject.ObjectData;
//Gets the file Name of OLE Object
string outputFile = oleObject.FileName;

//Save the extracted Ole data into file system
MemoryStream memoryStream = new MemoryStream(array);
Save(memoryStream, outputFile);
//Close the PowerPoint presentation
pptxDoc.Close();

async void Save(MemoryStream streams, string filename)
{
    streams.Position = 0;
    StorageFile stFile;
    if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
    {
        FileSavePicker savePicker = new FileSavePicker();
        savePicker.DefaultFileExtension = ".docx";
        savePicker.SuggestedFileName = filename;
        savePicker.FileTypeChoices.Add("Word Documents", new List<string>() { ".docx" });
        stFile = await savePicker.PickSaveFileAsync();
    }
    else
    {
        StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
        stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
    }
    if (stFile != null)
    {
        using (IRandomAccessStream zipStream = await stFile.OpenAsync(FileAccessMode.ReadWrite))
        {
            //Write compressed data from memory to file
            using (Stream outstream = zipStream.AsStreamForWrite())
            {
                byte[] buffer = streams.ToArray();
                outstream.Write(buffer, 0, buffer.Length);
                outstream.Flush();
            }
        }
    }
    //Launch the saved Word file
    await Windows.System.Launcher.LaunchFileAsync(stFile);
}
{% endhighlight %}

{% highlight ASP.NET CORE %}

//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream("EmbeddedOleObject.pptx", FileMode.Open);
//Opens the specified presentation
IPresentation pptxDoc = Presentation.Open(inputStream);
//Gets the first slide of the Presentation
ISlide slide = pptxDoc.Slides[0];
//Gets the Ole Object of the slide
IOleObject oleObject = slide.Shapes[2] as IOleObject;
//Gets the file data of embedded Ole Object
byte[] array = oleObject.ObjectData;
//Gets the file Name of OLE Object
string outputFile = oleObject.FileName;
//Save the extracted Ole data into file system
MemoryStream memoryStream = new MemoryStream(array);
FileStream fileStream = File.Create(outputFile);
memoryStream.CopyTo(fileStream);
memoryStream.Dispose();
fileStream.Dispose();
//Close the presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight XAMARIN %}

string resourcePath = "SampleBrowser.Presentation.Samples.Templates.EmbeddedOleObject.pptx";
Assembly assembly = typeof(GettingStarted).GetTypeInfo().Assembly;
Stream fileStream = assembly.GetManifestResourceStream(resourcePath);

//Open a PowerPoint presentation
IPresentation presentation = Syncfusion.Presentation.Presentation.Open(fileStream);
//Gets the first slide of the Presentation
ISlide slide = presentation.Slides[0];
//Gets the Ole Object of the slide
IOleObject oleObject = slide.Shapes[2] as IOleObject;
//Gets the file data of embedded Ole Object
byte[] array = oleObject.ObjectData;
//Gets the file Name of OLE Object
string outputFile = oleObject.FileName;

//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream(array);
//Close the presentation
pptxDoc.Close();
stream.Position = 0;

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save(outputFile, "application/msword", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save(outputFile, "application/msword", stream);

{% endhighlight %}

{% endtabs %}

## Get file path of a linked OLE Object

The below code snippet demonstrates how to get file path of a linked OLE Object.

{% tabs %}

{% highlight c# %}

//Opens the specified presentation
IPresentation pptxDoc = Presentation.Open("EmbeddedOleObject.pptx");
//Gets the first slide of the Presentation
ISlide slide = pptxDoc.Slides[0];
//Gets the Ole Object of the slide
IOleObject oleObject = slide.Shapes[1] as IOleObject;
//Gets the path of linked Ole Object
string linkOlePath = oleObject.LinkPath;
//Save the presentation
pptxDoc.Save("OleObjectSample.pptx");
//Close the presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens the specified presentation
Dim pptxDoc As IPresentation = Presentation.Open("EmbeddedOleObject.pptx")
'Gets the first slide of the Presentation
Dim slide As ISlide = pptxDoc.Slides(0)
'Gets the Ole Object of the slide
Dim oleObject As IOleObject = CType(slide.Shapes(1), IOleObject)
'Gets the path of linked Ole Object
Dim linkOlePath As String = oleObject.LinkPath
'Save the presentation
pptxDoc.Save("OleObjectSample.pptx")
'Close the presentation
pptxDoc.Close()

{% endhighlight %}

{% highlight UWP %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputFileStream = assembly.GetManifestResourceStream("Sample.Data.EmbeddedOleObject.pptx");
//Opens the specified presentation
IPresentation pptxDoc = Presentation.Open(inputFileStream);
//Gets the first slide of the Presentation
ISlide slide = pptxDoc.Slides[0];
//Gets the Ole Object of the slide
IOleObject oleObject = slide.Shapes[1] as IOleObject;
//Gets the path of linked Ole Object
string linkOlePath = oleObject.LinkPath;

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "OleObjectSample";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);

{% endhighlight %}

{% highlight ASP.NET CORE %}

//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream("EmbeddedOleObject.pptx", FileMode.Open);
//Opens the specified presentation
IPresentation pptxDoc = Presentation.Open(inputStream);
//Gets the first slide of the Presentation
ISlide slide = pptxDoc.Slides[0];
//Gets the Ole Object of the slide
IOleObject oleObject = slide.Shapes[1] as IOleObject;
//Gets the path of linked Ole Object
string linkOlePath = oleObject.LinkPath;
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("OleObjectSample.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
//Close the presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight XAMARIN %}

string resourcePath = "SampleBrowser.Presentation.Samples.Templates.EmbeddedOleObject.pptx";
Assembly assembly = typeof(GettingStarted).GetTypeInfo().Assembly;
Stream fileStream = assembly.GetManifestResourceStream(resourcePath);

//Open a PowerPoint presentation
IPresentation presentation = Syncfusion.Presentation.Presentation.Open(fileStream);
//Gets the first slide of the Presentation
ISlide slide = presentation.Slides[0];
//Gets the Ole Object of the slide
IOleObject oleObject = slide.Shapes[1] as IOleObject;
//Gets the path of linked Ole Object
string linkOlePath = oleObject.LinkPath;

//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();

//Save Presentation in stream format.
pptxDoc.Save(stream);

//Close the presentation
pptxDoc.Close();
stream.Position = 0;

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("OleObjectSample.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("OleObjectSample.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);

{% endhighlight %}

{% endtabs %}

## Get OLE Image data

The below code snippet demonstrates how to get the OLE image data.

{% tabs %}

{% highlight c# %}

//Opens the specified presentation
IPresentation pptxDoc = Presentation.Open("ImageEmbeddedOleObject.pptx");
//Gets the first slide of the Presentation
ISlide slide = pptxDoc.Slides[0];
//Gets the Ole Object of the slide
IOleObject oleObject = slide.Shapes[1] as IOleObject;
//Gets the data of Ole Image
byte[] array = oleObject.ImageData;
//Save the extracted Ole data into file system
MemoryStream memoryStream = new MemoryStream(array);
//Extracted ole data saved as image
FileStream fileStream = File.Create("OleImage.emf");
memoryStream.CopyTo(fileStream);
memoryStream.Dispose();
fileStream.Dispose();
//Close the presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens the specified presentation
Dim pptxDoc As IPresentation = Presentation.Open("EmbeddedOleObject.pptx")
'Gets the first slide of the Presentation
Dim slide As ISlide = pptxDoc.Slides(0)
'Gets the Ole Object of the slide
Dim oleObject As IOleObject = CType(slide.Shapes(1), IOleObject)
'Gets the data of Ole Image
Dim array() As Byte = oleObject.ImageData
'Save the extracted Ole data into file system
Dim memoryStream As MemoryStream = New MemoryStream(array)
'Extracted ole data saved as image
Dim fileStream As FileStream = File.Create("OleImage.emf")
memoryStream.CopyTo(fileStream)
memoryStream.Dispose()
fileStream.Dispose()
'Close the presentation
pptxDoc.Close()

{% endhighlight %}

{% highlight UWP %}

{% endhighlight %}

{% highlight ASP.NET CORE %}

//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream("EmbeddedOleObject.pptx", FileMode.Open);
//Opens the specified presentation
IPresentation pptxDoc = Presentation.Open(inputStream);
//Gets the first slide of the Presentation
ISlide slide = pptxDoc.Slides[0];
//Gets the Ole Object of the slide
IOleObject oleObject = slide.Shapes[1] as IOleObject;
//Gets the data of Ole Image
byte[] array = oleObject.ImageData;

//Save the extracted Ole data into file system
MemoryStream memoryStream = new MemoryStream(array);
FileStream fileStream = File.Create("OleImage.emf");
memoryStream.CopyTo(fileStream);
memoryStream.Dispose();
fileStream.Dispose();
//Close the presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight XAMARIN %}

string resourcePath = "SampleBrowser.Presentation.Samples.Templates.EmbeddedOleObject.pptx";
Assembly assembly = typeof(GettingStarted).GetTypeInfo().Assembly;
Stream fileStream = assembly.GetManifestResourceStream(resourcePath);

//Open a PowerPoint presentation
IPresentation presentation = Syncfusion.Presentation.Presentation.Open(fileStream);
//Gets the first slide of the Presentation
ISlide slide = presentation.Slides[0];
//Gets the Ole Object of the slide
IOleObject oleObject = slide.Shapes[1] as IOleObject;
//Gets the data of Ole Image
byte[] array = oleObject.ImageData;

//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream(array);
//Close the presentation
pptxDoc.Close();
stream.Position = 0;

FileStream fileStreamOutput = File.Create("OleImage.emf");
stream.CopyTo(fileStreamOutput);

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("OleImage.emf", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save(outputFile, "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);

{% endhighlight %}

{% endtabs %}