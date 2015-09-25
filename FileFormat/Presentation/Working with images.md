---
layout: Post
title: Working with images in PowerPoint Presentation
description: Working with images in PowerPoint Presentation
platform: FileFormats
control: Presentation
documentation: UG
---
# Working with images

## Adding Images

Essential Presentation library facilitates adding or modifying the images in a PowerPoint presentation. The below code snippet demonstrates adding a new image to the presentation.

{% highlight c# %}
[C#]

//Create a instance of presentation

IPresentation presentation = Presentation.Create();

//Add a blank slide.

ISlide slide = presentation.Slides.Add(SlideLayoutType.Blank);

//Get a picture as stream.

Stream pictureStream = File.Open("Image.png", FileMode.Open);

//Add the picture to a slide by specifying its size and position.

IPicture picture = slide.Pictures.AddPicture(pictureStream, 0, 0, 250, 250);

//Save the presentation to the file system.

presentation.Save("Output.pptx");

//Close the presentation

presentation.Close();



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Create a instance of presentation

Dim presentation_1 As IPresentation = Presentation.Create()

'Add a blank slide.

Dim slide As ISlide = presentation.Slides.Add(SlideLayoutType.Blank)

'Get a picture as stream.

Dim pictureStream As Stream = File.Open("Image.png", FileMode.Open)

'Add the picture to a slide by specifying its size and position.

Dim picture As IPicture = slide.Pictures.AddPicture(pictureStream, 0, 0, 250, 250)

'Save the presentation to the file system.

presentation_1.Save("Result.pptx")

'Close the presentation

presentation_1.Close()



{% endhighlight %}

## Replacing Images

The below code snippet demonstrates replacing an existing image in a slide.

{% highlight c# %}
[C#]

//Open an existing presentation.

IPresentation presentation = Presentation.Open("Sample.pptx");

//Retrieve the first slide from the presentation.

ISlide slide = presentation.Slides[0];

//Retrieve the first picture from the slide.

IPicture picture = slide.Pictures[0];

//Get the new picture as stream.

Stream pictureStream = File.Open("Image.png", FileMode.Open);

//Create instance for memory stream

MemoryStream memoryStream = new MemoryStream();

//Copy stream to memoryStream.

pictureStream.CopyTo(memoryStream);

//Replace the existing image with new image.

picture.ImageData = memoryStream.ToArray();

//Save the presentation to the file system.

presentation.Save("Output.pptx");

//Close the presentation

presentation.Close();



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Open an existing presentation.

Dim presentation_1 As IPresentation = Presentation.Open("Sample.pptx")

'Retrieve the first slide from the presentation.

Dim slide As ISlide = presentation_1.Slides(0)

'Retrieve the first picture from the slide.

Dim picture As IPicture = slide.Pictures(0)

'Get the new picture as stream.

Dim pictureStream As Stream = File.Open("Image.png", FileMode.Open)

'Create instance for memory stream

Dim memoryStream As New MemoryStream()

'Copy stream to memoryStream.

pictureStream.CopyTo(memoryStream)

'Replace the existing image with new image.

picture.ImageData = memoryStream.ToArray()

'Save the presentation to the file system.

presentation_1.Save("Output.pptx")

'Close the presentation

presentation_1.Close()



{% endhighlight %}

## Removing Images

The below code snippet demonstrates removing an existing image in a PowerPoint slide.

{% highlight c# %}
[C#]

//Open an existing presentation from file system.

IPresentation presentation = Presentation.Open("Sample.pptx");

//Retrieve the first slide from presentation

ISlide slide = presentation.Slides[0];

//Iterate through the pictures collection and remove the picture named "Image".

foreach (IPicture picture in slide.Pictures)

{

//Remove the picture from the slide.

slide.Pictures.Remove(picture);

break;

}

//Save the presentation to the file system.

presentation.Save("Output.pptx");

//Close the presentation

presentation.Close();



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Open an existing presentation from file system.

Dim presentation_1 As IPresentation = Presentation.Open("Sample.pptx")

'Retrieve the first slide from presentation

Dim slide As ISlide = presentation_1.Slides(0)

'Iterate through the pictures collection and remove the picture named "Image".

For Each picture As IPicture In slide.Pictures

'Remove the picture from the slide.

slide.Pictures.Remove(picture)

Exit For

Next

'Save the presentation to the file system.

presentation_1.Save("Output.pptx")

'Close the presentation

presentation_1.Close()



{% endhighlight %}

