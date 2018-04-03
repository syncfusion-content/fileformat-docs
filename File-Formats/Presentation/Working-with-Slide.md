---
title: Working with slides in PowerPoint presentation
description: Working with slides in PowerPoint presentation; Adding and modifying the slides in PowerPoint presentation
platform: file-formats
control: Presentation
documentation: UG
---
# Working with Slide

## Adding slide to the PowerPoint presentation

In PowerPoint presentation, a slide is a container for the elements like shapes, images, charts, text box etc. The slides may inherit the formatting and layout properties from its 'Master' and 'Layout' slides.

The following code example demonstrates how to add a blank slide to the Presentation.

{% tabs %}

{% highlight c# %}

//Creates a PowerPoint instance

IPresentation presentation = Presentation.Create();

//Adds a slide to the PowerPoint presentation

ISlide slide = presentation.Slides.Add(SlideLayoutType.Blank);

//Saves the Presentation to the file system.

presentation.Save("Sample.pptx");

//Closes the Presentation instance

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates a PowerPoint instance

Dim presentationDocument As IPresentation = Presentation.Create()

'Adds a slide to the PowerPoint presentation

Dim slide As ISlide = presentationDocument.Slides.Add(SlideLayoutType.Blank)

'Saves the Presentation to the file system.

presentationDocument.Save("Sample.pptx")

'Closes the Presentation instance

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

## Adding Custom layout slide

The slide layout are template design for the PowerPoint slides. Slide layout can contains formatting, positioning, and placeholders for a slide. There are 9 predefined layouts and custom slide layouts can also be designed.

The following code example demonstrates how to create and use a customized slide layout in PowerPoint presentation.

{% tabs %}

{% highlight c# %}

//Open the template presentation
IPresentation presentation = Presentation.Open("Sample.pptx");

//Add a new custom layout slide to the master collection with a specific layout type and name
ILayoutSlide layoutSlide = presentation.Masters[0].LayoutSlides.Add(SlideLayoutType.Blank, "CustomLayout");

//Set background of the layout slide
layoutSlide.Background.Fill.SolidFill.Color = ColorObject.FromArgb(78, 89, 90);

//Get the stream of an image
Stream pictureStream = File.Open("Image.png", FileMode.Open);

//Add the picture into layout slide
layoutSlide.Shapes.AddPicture(pictureStream, 100, 100, 100, 100);

//Add a slide of new designed custom layout to the presentation
ISlide slide = presentation.Slides.Add(layoutSlide);

//Save the presentation
presentation.Save("Output.pptx");

//Close the presentation
presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Open the template presentation
Dim presentationDocument As IPresentation = Presentation.Open("Sample.pptx")

'Add a new custom layout slide to the master collection with a specific layout type and name
Dim layoutSlide As ILayoutSlide = presentationDocument.Masters(0).LayoutSlides.Add(SlideLayoutType.Blank, "CustomLayout")

'Set background of the layout slide
layoutSlide.Background.Fill.SolidFill.Color = ColorObject.FromArgb(78, 89, 90)

'Get the stream of an image
Dim pictureStream As Stream = File.Open("Image.png", FileMode.Open)

'Add the picture into layout slide
layoutSlide.Shapes.AddPicture(pictureStream, 100, 100, 100, 100)

'Add a slide of new designed custom layout to the presentation
Dim slide As ISlide = presentationDocument.Slides.Add(layoutSlide)

'Save the presentation
presentationDocument.Save("Output.pptx")

'Close the presentation
presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

The following code example demonstrates how to add a slide with an existing slide’s layout.

{% tabs %}

{% highlight c# %}

//Open the template presentation
IPresentation presentation = Presentation.Open("Sample.pptx");
//Get the layout slide collection of the master
ILayoutSlides layoutSlides = presentation.Masters[0].LayoutSlides;
ILayoutSlide slideLayout = null;
//Get each layout slide from the collection
foreach (ILayoutSlide layout in layoutSlides)
{
//Check if the layout slide has desired custom layout name
if (layout.Name == "CustomSlideLayout")
{
slideLayout = layout;
break;
}
}
//Add slide with the desired layout.
ISlide slide = presentation.Slides.Add(slideLayout);
//Save the presentation
presentation.Save("Output.pptx");
//Close the presentation
presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Open the template presentation
Dim presentationDocument As IPresentation = Presentation.Open("Sample.pptx")
'Get the layout slide collection of the master
Dim layoutSlides As ILayoutSlides = presentationDocument.Masters(0).LayoutSlides
Dim slideLayout As ILayoutSlide = Nothing
'Get each layout slide from the collection
For Each layout As ILayoutSlide In layoutSlides
	'Check if the layout slide has desired custom layout name
	If layout.Name = "CustomSlideLayout" Then
		slideLayout = layout
		Exit For
	End If
Next
'Add slide with the desired layout.
Dim slide As ISlide = presentationDocument.Slides.Add(slideLayout)
'Save the presentation
presentationDocument.Save("Output.pptx")
'Close the presentation
presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

## Cloning slide

You can create a deep copy of a slide by cloning the slide. The cloned slide is an independent copy of its source slide. This means the changes made in the cloned slide do not affect the source slide.

{% tabs %}

{% highlight c# %}

//Opens an existing Presentation.

IPresentation presentation = Presentation.Open("Presentation.pptx");

//Retrieves the slide instance.

ISlide slide = presentation.Slides[0];

//Creates a cloned copy of slide.

ISlide slideClone = slide.Clone();

//Adds a new text box to the cloned slide.

IShape textboxShape = slideClone.AddTextBox(0, 0, 250, 250);

//Adds a paragraph with text content to the shape.

textboxShape.TextBody.AddParagraph("Hello Presentation");

//Adds the slide to the Presentation.

presentation.Slides.Add(slideClone);

//Saves the Presentation to the file system.

presentation.Save("Output.pptx");

//Closes the Presentation

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing Presentation.

Dim presentationDocument As IPresentation = Presentation.Open("Presentation.pptx")

'Retrieves the slide instance.

Dim slide As ISlide = presentationDocument.Slides(0)

'Creates a cloned copy of slide.

Dim slideClone As ISlide = slide.Clone()

'Adds a new text box to the cloned slide.

Dim textboxShape As IShape = slideClone.AddTextBox(0, 0, 250, 250)

'Adds a paragraph with text content to the shape.

textboxShape.TextBody.AddParagraph("Hello Presentation")

'Adds the slide to the Presentation.

presentationDocument.Slides.Add(slideClone)

'Saves the Presentation to the file system.

presentationDocument.Save("Output.pptx")

'Closes the Presentation

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

## Merging slide

The Essential Presentation provides ability to clone slides from one Presentation to another Presentation. With this ability, you can split a large Presentation into small ones and also merge multiple presentations to one Presentation. You can choose the theme for the cloned slide by using the enum PasteOption.

{% tabs %}

{% highlight c# %}

//Opens the source Presentation

IPresentation sourcePresentation = Presentation.Open("SourcePresentation.pptx");

//Opens the destination Presentation

IPresentation destinationPresentation = Presentation.Open("DestinationPresentation.pptx");

//Clones the first slide of the source Presentation

ISlide clonedSlide = sourcePresentation.Slides[0].Clone();

//Merges the cloned slide to the destination Presentation with paste option - Destination Theme

destinationPresentation.Slides.Add(clonedSlide, PasteOptions.UseDestinationTheme, sourcePresentation);

//Saves the destination Presentation

destinationPresentation.Save("Output.pptx");

//Closes the source presentation

sourcePresentation.Close();

//Closes the destination Presentation

destinationPresentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens the source Presentation

Dim sourcePresentation_1 As IPresentation = Presentation.Open("SourcePresentation.pptx")

'Opens the destination Presentation

Dim destinationPresentation_1 As IPresentation = Presentation.Open("DestinationPresentation.pptx")

'Clones the first slide of the source Presentation

Dim clonedSlide As ISlide = sourcePresentation_1.Slides(0).Clone()

'Merges the cloned slide to the destination Presentation with paste option - Destination Theme

destinationPresentation_1.Slides.Add(clonedSlide, PasteOptions.UseDestinationTheme, sourcePresentation_1)

'Saves the destination Presentation

destinationPresentation_1.Save("Output.pptx")

'Closes the source presentation

sourcePresentation.Close()

'Closes the destination Presentation

destinationPresentation.Close()

{% endhighlight %}

{% endtabs %}

## Removing slide

The Essential Presentation provides the ability to delete a slide by its instance or by its index position in slide collection. The following code demonstrates how to delete a slide from a presentation. 

{% tabs %}

{% highlight c# %}

//Opens an existing presentation.

IPresentation presentation = Presentation.Open("Presentation1.pptx");

//Retrieves the slide instance.

ISlide slide = presentation.Slides[0];

//Removes the specified slide from the Presentation.

presentation.Slides.Remove(slide);

// Removes the slide from the specified index.

presentation.Slides.RemoveAt(1);

//Saves the destination Presentation

presentation.Save("Output.pptx");

//Closes the Presentation instance

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing Presentation.

Dim presentationDocument As IPresentation = Presentation.Open("Presentation1.pptx")

'Retrieves the slide instance.

Dim slide As ISlide = presentationDocument.Slides(0)

'Removes the specified slide from the Presentation.

presentationDocument.Slides.Remove(slide)

'Removes the slide from the specified index.

presentationDocument.Slides.RemoveAt(1)

'Saves the destination Presentation

presentationDocument.Save("Output.pptx")

'Closes the Presentation instance

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

## Converting to image

You can convert a presentation slide to image with Essential Presentation. The following code example converts the first slide of a PowerPoint presentation into image and saves the image to a file.

{% tabs %}

{% highlight c# %}

//Opens a PowerPoint presentation file

IPresentation presentation = Presentation.Open(fileName); 

//Creates an instance of ChartToImageConverter and assigns it to ChartToImageConverter 

presentation.ChartToImageConverter = new ChartToImageConverter(); 

//Converts the first slide into image

Image image = presentation.Slides[0].ConvertToImage(Syncfusion.Drawing.ImageType.Metafile); 

//Saves the image as file

image.Save("slide1.png"); 

//Closes the Presentation instance

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens a PowerPoint presentation file

Dim presentationDocument As IPresentation = Presentation.Open(fileName)

'Creates an instance of ChartToImageConverter and assigns it to ChartToImageConverter 

presentationDocument.ChartToImageConverter = New ChartToImageConverter()

'Converts the first slide into image

Dim image As Image = presentationDocument.Slides(0).ConvertToImage(Syncfusion.Drawing.ImageType. Metafile)

'Saves the image as file

image.Save("slide1.png")

'Closes the Presentation instance

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

For more details on assemblies required for converting a slide to image,  see [Conversion](/file-formats/presentation/conversion)

N> You can print the PowerPoint presentations by using its ability to convert the slides as images. For more details, refer to [Printing a PowerPoint presentation](/file-formats/presentation/working-with-powerpoint-presentation#printing-a-powerpoint-presentation)

## Changing Slide background

The following code example demonstrates setting the background for a slide.

{% tabs %}

{% highlight c# %}

//Opens an existing Presentation.

IPresentation presentation = Presentation.Open("Presentation1.pptx");

//Retrieves the slide instance.

ISlide slide = presentation.Slides[0];

//Retrieves the background instance.

IBackground background = slide.Background;

//Sets the fill type of the background to gradient.

background.Fill.FillType = FillType.Gradient;

//Retrieves the fill of the background to the IGradientFill instance.

IGradientFill gradient = background.Fill.GradientFill;

//Adds the first gradient stop of the gradient fill.

gradient.GradientStops.Add(ColorObject.Green, 20);

//Adds the second gradient stop of the gradient fill.

gradient.GradientStops.Add(ColorObject.Yellow, 50);

//Saves the Presentation to the file system

presentation.Save("Output.pptx");

//Closes the Presentation

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing Presentation.

Dim presentationDocument As IPresentation = Presentation.Open("Presentation1.pptx")

'Retrieves the slide instance.

Dim slide As ISlide = presentationDocument.Slides(0)

'Retrieves the background instance.

Dim background As IBackground = slide.Background

'Sets the fill type of the background to gradient.

background.Fill.FillType = FillType.Gradient

'Retrieves the fill of the background to the IGradientFill instance.

Dim gradient As IGradientFill = background.Fill.GradientFill

'Adds the first gradient stop of the gradient fill.

gradient.GradientStops.Add(ColorObject.Green, 20)

'Adds the second gradient stop of the gradient fill.

gradient.GradientStops.Add(ColorObject.Yellow, 50)

'Saves the Presentation to the file system

presentationDocument.Save("Output.pptx")

'Closes the Presentation

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}