---
title: Create and edit OLE Objects in PowerPoint files |Syncfusion|
description: Working with OLE Objects.The OLE Object enables sharing of application objects written in different file formats.
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
