---
title: Working with images in PowerPoint Presentation
description: Working with images in PowerPoint Presentation
platform: file-formats
control: Presentation
documentation: UG
---
# Working with images

## Adding Images

Essential Presentation library facilitates adding or modifying the images in a PowerPoint presentation. The following code example demonstrates how to add a new image to the presentation.

{% tabs %}

{% highlight c# %}

//Creates a instance of presentation

IPresentation presentation = Presentation.Create();

//Adds a blank slide.

ISlide slide = presentation.Slides.Add(SlideLayoutType.Blank);

//Gets a picture as stream.

Stream pictureStream = File.Open("Image.png", FileMode.Open);

//Adds the picture to a slide by specifying its size and position.

IPicture picture = slide.Pictures.AddPicture(pictureStream, 0, 0, 250, 250);

//Saves the presentation to the file system.

presentation.Save("Output.pptx");

//Closes the presentation

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates a instance of presentation

Dim presentationDocument As IPresentation = Presentation.Create()

'Adds a blank slide.

Dim slide As ISlide = presentation.Slides.Add(SlideLayoutType.Blank)

'Gets a picture as stream.

Dim pictureStream As Stream = File.Open("Image.png", FileMode.Open)

'Adds the picture to a slide by specifying its size and position.

Dim picture As IPicture = slide.Pictures.AddPicture(pictureStream, 0, 0, 250, 250)

'Saves the presentation to the file system.

presentationDocument.Save("Result.pptx")

'Closes the presentation

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

## Replace Images

The following code example demonstrates how to replace an existing image in a slide.

{% tabs %}

{% highlight c# %}

//Opens an existing presentation.

IPresentation presentation = Presentation.Open("Sample.pptx");

//Retrieves the first slide from the presentation.

ISlide slide = presentation.Slides[0];

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

//Saves the presentation to the file system.

presentation.Save("Output.pptx");

//Closes the presentation

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing presentation.

Dim presentationDocument As IPresentation = Presentation.Open("Sample.pptx")

'Retrieves the first slide from the presentation.

Dim slide As ISlide = presentationDocument.Slides(0)

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

'Saves the presentation to the file system.

presentationDocument.Save("Output.pptx")

'Closes the presentation

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

## Remove Images

The following code example demonstrates how to remove an existing image in a PowerPoint slide.

{% tabs %}

{% highlight c# %}

//Opens an existing presentation from file system.

IPresentation presentation = Presentation.Open("Sample.pptx");

//Retrieves the first slide from presentation

ISlide slide = presentation.Slides[0];

//Iterates through the pictures collection and remove the picture named "Image".

foreach (IPicture picture in slide.Pictures)

{

	//Removes the picture from the slide.

	slide.Pictures.Remove(picture);

	break;

}

//Saves the presentation to the file system.

presentation.Save("Output.pptx");

//Closes the presentation

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing presentation from file system.

Dim presentationDocument As IPresentation = Presentation.Open("Sample.pptx")

'Retrieves the first slide from presentation

Dim slide As ISlide = presentationDocument.Slides(0)

'Iterates through the pictures collection and removes the picture named "Image".

For Each picture As IPicture In slide.Pictures

'Removes the picture from the slide.

slide.Pictures.Remove(picture)

Exit For

Next

'Saves the presentation to the file system.

presentationDocument.Save("Output.pptx")

'Closes the presentation

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

