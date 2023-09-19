---
title: Create and edit OLE Objects in PowerPoint files |Syncfusion|
description: Create and edit OLE Objects in PowerPoint files; Insert and extract an embedded OLE object in PowerPoint Presentation
platform: file-formats
control: Presentation
documentation: UG
keywords: OLE Object in PowerPoint presentation
---
# Working with OLE Objects

The OLE Object enables sharing of application objects written in different file formats. In PowerPoint presentation the application data can be inserted into a PowerPoint slide using the [programmatic identifier](https://msdn.microsoft.com/en-us/library/aa171170(v=office.11).aspx#) of each file format.

## Inserting OLE Object to a Slide

The following code example demonstrates how to add an Excel worksheet into a slide.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Create new instance of PowerPoint presentation.
IPresentation pptxDoc = Presentation.Create();
//Add slide with blank layout to presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Get the excel file as stream
FileStream excelStream = new FileStream("OleTemplate.xlsx", FileMode.Open);
//Image to be displayed, This can be any image
FileStream imageStream = new FileStream("OlePicture.png", FileMode.Open);
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

{% highlight c# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/OLE-objects/Add-Excel-in-PowerPoint-slide).

### Inserting OLE Object to a Slide with Display As Icon property

The following code example demonstrates how to add an Microsoft Word document into a slide with display as icon property.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Create new instance of PowerPoint presentation.
IPresentation pptxDoc = Presentation.Create();
//Add slide with blank layout to presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Get the Word document file as stream
FileStream wordDocumentStream = new FileStream("OleTemplate.docx", FileMode.Open);
//Image to be displayed, This can be any image
FileStream imageStream = new FileStream("OlePicture.png", FileMode.Open);
//Add an OLE object to the slide
IOleObject oleObject = slide.Shapes.AddOleObject(imageStream, "Word.Document.12", wordDocumentStream);
//Set size and position of the OLE object
oleObject.Left = 10;
oleObject.Top = 10;
oleObject.Width = 400;
oleObject.Height = 300;
//Set DisplayAsIcon as true, to open the embedded document in separate (default) application.
oleObject.DisplayAsIcon = true;
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("OleObjectSample.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
//Close the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Create new instance of PowerPoint presentation. [Equivalent to launching MS PowerPoint with no slides].
IPresentation pptxDoc = Presentation.Create();
//Add slide with blank layout to presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Get the Word document file as stream
Stream wordDocumentStream = File.Open("OleTemplate.docx", FileMode.Open);
//Image to be displayed, This can be any image
Stream imageStream = File.Open("OlePicture.png", FileMode.Open);
//Add an OLE object to the slide
IOleObject oleObject = slide.Shapes.AddOleObject(imageStream, "Word.Document.12", wordDocumentStream);
//Set size and position of the OLE objectwordStream
oleObject.Left = 10;
oleObject.Top = 10;
oleObject.Width = 400;
oleObject.Height = 300;
//Set DisplayAsIcon as true, to open the embedded document in separate (default) application.
oleObject.DisplayAsIcon = true;
//Save the presentation
pptxDoc.Save("OleObjectSample.pptx");
//Close the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Create new instance of PowerPoint presentation. [Equivalent to launching MS PowerPoint with no slides].
Dim pptxDoc As IPresentation = Presentation.Create()
'Add slide with blank layout to presentation
Dim slide As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank)
'Get the Word document file as stream
Dim wordDocumentStream As Stream = File.Open("OleTemplate.docx", FileMode.Open)
'Image to be displayed, This can be any image
Dim imageStream As Stream = File.Open("OlePicture.png", FileMode.Open)
'Add an OLE object to the slide
Dim oleObject As IOleObject = slide.Shapes.AddOleObject(imageStream, "Word.Document.12", wordDocumentStream)
'Set size and position of the OLE object
oleObject.Left = 10
oleObject.Top = 10
oleObject.Width = 400
oleObject.Height = 300
'Set DisplayAsIcon as true, to open the embedded document in separate (default) application.
oleObject.DisplayAsIcon = True
'Save the presentation
pptxDoc.Save("OleObjectSample.pptx")
'Close the presentation
pptxDoc.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/OLE-objects/Add-Microsoft-Word-document-in-slide).

## Extract embedded OLE Object data

The following code example demonstrates how to extract the embedded OLE Object data.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
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

{% highlight c# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/OLE-objects/Extract-embedded-OLE-Object-data).

## Get file path of a linked OLE Object

The following code example demonstrates how to get the file path of a linked OLE Object.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
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

{% highlight c# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/OLE-objects/Get-file-path-of-linked-OLE-Object).

## Get OLE Image data

The following code example demonstrates how to get the OLE image data.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
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

{% highlight c# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/OLE-objects/Get-OLE-image-data).