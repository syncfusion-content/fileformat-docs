---
title: Add and edit images in PowerPoint slides |C# PowerPoint| |Syncfusion|
description: C# PowerPoint library to create, read, edit and convert PowerPoint files in .NET applications, ASP.NET Web, MVC, C# [Cross-platform], Xamarin and Azure platforms
platform: file-formats
control: Presentation
documentation: UG
---
# Working with PowerPoint Images

## Adding Images

Essential Presentation library facilitates adding or modifying the images in a PowerPoint Presentation. The following code example demonstrates how to add a new image to the presentation.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
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

{% highlight c# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Images/Add-image-into-PowerPoint-Slide).

## Replacing Images

The following code example demonstrates how to replace an existing image in a slide.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
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

{% highlight c# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Images/Replace-existing-image).

## Adding SVG Images

SVG images can be inserted in PowerPoint slide for displaying images with accuracy when scaling or zooming page. The Essential Presentation library allows you to insert and edit an SVG image along with its fallback image.

The following code example demonstrates how to add a new SVG image into a slide.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
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

{% highlight c# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Images/Add-SVG-image).

## Replacing SVG Images

The following code example demonstrates how to replace an existing SVG image in a slide.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
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

{% highlight c# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Images/Replace-SVG-Image).

## Crop Image

Refine the image dimensions by cropping out any unintended elements, using a cropping tool to focus the image on relevant areas.

The following code example demonstrates how to crop an image in a PowerPoint slide.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//Open an existing PowerPoint Presentation.
using (FileStream inputStream = new FileStream("Sample.docx", FileMode.Open, FileAccess.Read))
{
    using (IPresentation pptxDoc = Presentation.Open(inputStream))
    {
        //Retrieve the first slide from the Presentation.
        ISlide slide = pptxDoc.Slides[0];
        //Retrieve the first picture from the slide.
        IPicture picture = slide.Pictures[0];

        //Apply cropping to the picture.
        picture.Crop.ContainerWidth = 345;
        picture.Crop.ContainerHeight = 220;
        picture.Crop.ContainerLeft = 324;
        picture.Crop.ContainerTop = 220;

        picture.Crop.Width = 288;
        picture.Crop.Height = 144;
        picture.Crop.OffsetX = -35;
        picture.Crop.OffsetY = -65;

        //Save the PowerPoint Presentation as stream.
        FileStream outputStream = new FileStream("Output.pptx", FileMode.Create);
        pptxDoc.Save(outputStream);
    }
}

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

//Open an existing PowerPoint Presentation.
using (IPresentation pptxDoc = Presentation.Open("Sample.pptx"))
{
    //Retrieve the first slide from the Presentation.
    ISlide slide = pptxDoc.Slides[0];
    //Retrieve the first picture from the slide.
    IPicture picture = slide.Pictures[0];

    //Apply cropping to the picture.
    picture.Crop.ContainerWidth = 345;
    picture.Crop.ContainerHeight = 220;
    picture.Crop.ContainerLeft = 324;
    picture.Crop.ContainerTop = 220;

    picture.Crop.Width = 288;
    picture.Crop.Height = 144;
    picture.Crop.OffsetX = -35;
    picture.Crop.OffsetY = -65;

    // Save the PowerPoint Presentation.
    pptxDoc.Save("Output.pptx");
}

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

' Open an existing PowerPoint Presentation.
Using pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
    ' Retrieve the first slide from the Presentation.
    Dim slide As ISlide = pptxDoc.Slides(0)
    ' Retrieve the first picture from the slide.
    Dim picture As IPicture = slide.Pictures(0)

    ' Apply cropping to the picture.
    picture.Crop.ContainerWidth = 345
    picture.Crop.ContainerHeight = 220
    picture.Crop.ContainerLeft = 324
    picture.Crop.ContainerTop = 220

    picture.Crop.Width = 288
    picture.Crop.Height = 144
    picture.Crop.OffsetX = -35
    picture.Crop.OffsetY = -65

    ' Save the PowerPoint Presentation.
    pptxDoc.Save("Output.pptx")
End Using

{% endhighlight %}
{% endtabs %}

N>  The bounding box properties (ContainerLeft, ContainerTop, ContainerRight, ContainerBottom) must be set before applying this cropping property for proper functionality.

You can download a complete working sample from GitHub.

## Removing Images

The following code example demonstrates how to remove an existing image in a PowerPoint slide.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
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

{% highlight c# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Images/Remove-all-images).

