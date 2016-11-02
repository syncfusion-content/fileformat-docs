---
title: Working with OLE Objects
description: Working with OLE Objects
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
IPresentation presentationFile = Presentation.Create();
//Add slide with blank layout to presentation
ISlide slide = presentationFile.Slides.Add(SlideLayoutType.Blank);
//Get the excel file as stream
Stream excelStream = File.Open("OleTemplate.xlsx", FileMode.Open);
//Image to be displayed, This can be any image
Stream imageStream = File.Open("OlePicture.png", FileMode.Open);
//Add ole object to the slide
IOleObject oleObject = slide.Shapes.AddOleObject(imageStream, "Excel.Sheet.12", excelStream);
//Set size and position of the ole object
oleObject.Left = 10;
oleObject.Top = 10;
oleObject.Width = 400;
oleObject.Height = 300;
//Save the presentation
presentationFile.Save("OleObjectSample.pptx");
//Close the presentation
presentationFile.Close();
{% endhighlight %}
{% highlight vb.net %}
'Create new instance of PowerPoint presentation. [Equivalent to launching MS PowerPoint with no slides].
Dim presentationFile As IPresentation = Presentation.Create()
'Add slide with blank layout to presentation
Dim slide As ISlide = presentationFile.Slides.Add(SlideLayoutType.Blank)
'Get the excel file as stream
Dim excelStream As Stream = File.Open("OleTemplate.xlsx", FileMode.Open)
'Image to be displayed, This can be any image
Dim imageStream As Stream = File.Open("OlePicture.png", FileMode.Open)
'Add ole object to the slide
Dim oleObject As IOleObject = slide.Shapes.AddOleObject(imageStream, "Excel.Sheet.12", excelStream)
'Set size and position of the ole object
oleObject.Left = 10
oleObject.Top = 10
oleObject.Width = 400
oleObject.Height = 300
'Save the presentation
presentationFile.Save("OleObjectSample.pptx")
'Close the presentation
presentationFile.Close()
{% endhighlight %}
{% endtabs %}
