---
title: Working with slides in PowerPoint Presentation
description: Working with slides in PowerPoint Presentation; Adding and modifying the slides in PowerPoint Presnetation
platform: file-formats
control: Presentation
documentation: UG
---
# Working with Slide

## Adding slide to the PowerPoint presentation

In presentation, a slide is a container for the elements like shapes, images, charts, text box etc. The slides may inherit the formatting and layout properties from its Master and Layout slides that reside in the PowerPoint presentation.

The following code example demonstrates how to add a blank slide to the presentation.

{% tabs %}

{% highlight c# %}

//Creates a PowerPoint instance

IPresentation presentation = Presentation.Create();

//Adds a slide to the PowerPoint presentation

ISlide slide = presentation.Slides.Add(SlideLayoutType.Blank);

//Saves the presentation to the file system.

presentation.Save("Sample.pptx");

//Closes the presentation instance

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates a PowerPoint instance

Dim presentationDocument As IPresentation = Presentation.Create()

'Adds a slide to the PowerPoint presentation

Dim slide As ISlide = presentationDocument.Slides.Add(SlideLayoutType.Blank)

'Saves the presentation to the file system.

presentationDocument.Save("Sample.pptx")

'Closes the presentation instance

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

## Cloning slide

You can create a deep copy of a slide by cloning the slide. The cloned slide is an independent copy of its source slide. This means the changes made in the cloned slide do not affect the source slide.

{% tabs %}

{% highlight c# %}

//Opens an existing presentation.

IPresentation presentation = Presentation.Open("Presentation.pptx");

//Retrieves the slide instance.

ISlide slide = presentation.Slides[0];

//Creates a cloned copy of slide.

ISlide slideClone = slide.Clone();

//Adds a new text box to the cloned slide.

IShape textboxShape = slideClone.AddTextBox(0, 0, 250, 250);

//Adds a paragraph with text content to the shape.

textboxShape.TextBody.AddParagraph("Hello Presentation");

//Adds the slide to the presentation.

presentation.Slides.Add(slideClone);

//Saves the presentation to the file system.

presentation.Save("Output.pptx");

//Closes the presentation

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing presentation.

Dim presentationDocument As IPresentation = Presentation.Open("Presentation.pptx")

'Retrieves the slide instance.

Dim slide As ISlide = presentationDocument.Slides(0)

'Creates a cloned copy of slide.

Dim slideClone As ISlide = slide.Clone()

'Adds a new text box to the cloned slide.

Dim textboxShape As IShape = slideClone.AddTextBox(0, 0, 250, 250)

'Adds a paragraph with text content to the shape.

textboxShape.TextBody.AddParagraph("Hello Presentation")

'Adds the slide to the presentation.

presentationDocument.Slides.Add(slideClone)

'Saves the presentation to the file system.

presentationDocument.Save("Output.pptx")

'Closes the presentation

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

## Merge slide

The Essential Presentation provides ability to clone slides from one presentation to another presentation. With this ability, you can split a large presentation into small ones and also merge multiple presentations to one presentation. You can choose the theme for the cloned slide by using the enum PasteOption.

{% tabs %}

{% highlight c# %}

//Opens the source presentation

IPresentation sourcePresentation = Presentation.Open("SourcePresentation.pptx");

//Opens the destination presentation

IPresentation destinationPresentation = Presentation.Open("DestinationPresentation.pptx");

//Clones the first slide of the source presentation.

ISlide clonedSlide = sourcePresentation.Slides[0].Clone();

//Merges the cloned slide to the destination presentation with paste option - Destination Them.

destinationPresentation.Slides.Add(clonedSlide, PasteOptions.UseDestinationTheme, sourcePresentation);

//Saves the destination presentation.

destinationPresentation.Save("Output.pptx");

{% endhighlight %}

{% highlight vb.net %}

'Opens the source presentation

Dim sourcePresentation_1 As IPresentation = Presentation.Open("SourcePresentation.pptx")

'Opens the destination presentation

Dim destinationPresentation_1 As IPresentation = Presentation.Open("DestinationPresentation.pptx")

'Clones the first slide of the source presentation.

Dim clonedSlide As ISlide = sourcePresentation_1.Slides(0).Clone()

'Merges the cloned slide to the destination presentation with paste option - Destination Them.

destinationPresentation_1.Slides.Add(clonedSlide, PasteOptions.UseDestinationTheme, sourcePresentation_1)

'Saves the destination presentation.

destinationPresentation_1.Save("Output.pptx")

{% endhighlight %}

{% endtabs %}

## Remove slide

The Essential Presentation provides the ability to delete a slide by its instance or by its index position in slide collection. The following code demonstrates how to delete a slide from a presentation. 

{% tabs %}

{% highlight c# %}

//Opens an existing presentation.

IPresentation presentation = Presentation.Open("Presentation1.pptx");

//Retrieves the slide instance.

ISlide slide = presentation.Slides[0];

//Removes the specified slide from the presentation.

presentation.Slides.Remove(slide);

// Removes the slide from the specified index.

presentation.Slides.RemoveAt(1);

//Saves the destination presentation.

presentation.Save("Output.pptx");

//Closes the presentation instance

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing presentation.

Dim presentationDocument As IPresentation = Presentation.Open("Presentation1.pptx")

'Retrieves the slide instance.

Dim slide As ISlide = presentationDocument.Slides(0)

'Removes the specified slide from the presentation.

presentationDocument.Slides.Remove(slide)

'Removes the slide from the specified index.

presentationDocument.Slides.RemoveAt(1)

'Saves the destination presentation.

presentationDocument.Save("Output.pptx")

'Closes the presentation instance

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

## Convert to image

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

//Closes the presentation instance

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

'Closes the presentation instance

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

For more details on assemblies required for converting a slide to image,  see [Conversion](/file-formats/presentation/conversion)

## Change Slide background

The following code example demonstrates setting the background for a slide.

{% tabs %}

{% highlight c# %}

//Opens an existing presentation.

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

//Saves the presentation to the file system.

presentation.Save("Output.pptx");

//Closes the presentation

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing presentation.

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

'Saves the presentation to the file system.

presentationDocument.Save("Output.pptx")

'Closes the presentation

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}