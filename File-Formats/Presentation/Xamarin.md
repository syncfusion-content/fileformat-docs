---
title: Working with Xamarin
description: Working with presentation library in Xamarin Platform
platform: file-formats
control: Presentation
documentation: UG
keywords: Working with presentation library in Xamarin Platform
---

# Working with Xamarin

In your Xamarin Application, please add the required assemblies in order to use Presentation. [Refer here for assemblies required](/File-Formats/Presentation/Assemblies-Required)

## Loading the Presentation

The following code example illustrates how to load the PowerPoint Presentation by using stream in Xamarin.
{% tabs %}
{% highlight c# %}
//Loads the PowerPoint Presentation as stream.

Assembly assembly = typeof(GettingStartedPresentation).GetTypeInfo().Assembly;

string resourcePath = "SampleBrowser.Presentation.Assets.HelloWorld.pptx";

Stream fileStream = assembly.GetManifestResourceStream(resourcePath);

//Loads or opens existing Presentation using open method of Presentation class.

IPresentation presentation = await Presentation.OpenAsync(fileStream);

//Creates Memory stream to save Presentation.

MemoryStream stream = new MemoryStream();

//Saves Presentation in stream format.

presentation.Save(stream);

presentation.Close();
{% endhighlight %}
{% endtabs %}

## Saving the Presentation

The following code example illustrates how to save the PowerPoint Presentation in Xamarin Windows Phone platform.
{% tabs %}
{% highlight c# %}
//Creates new Presentation without slides.

IPresentation presentation = Presentation.Create();

//Adds new Blank type of slide.

ISlide slide = presentation.Slides.Add(SlideLayoutType.Blank);

//Adds Rectangle auto shape with specified size and positions.

IShape shape = slide.Shapes.AddShape(AutoShapeType.Rectangle, 1.92 * 72, 1.51 * 72, 10.85 * 72, 4.12 * 72);

//Adds text into the shape.

shape.TextBody.AddParagraph("Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula");

//Creates new memory stream to save Presentation.

MemoryStream stream = new MemoryStream();

//Saves Presentation in stream format.

presentation.Save(stream);

presentation.Close();

stream.Position = 0;

Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("GettingStartedSample.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
{% endhighlight %}
{% endtabs %}
The following code example illustrates how to save the PowerPoint Presentation in Xamarin.Android platform.
{% tabs %}
{% highlight c# %}
//Creates new Presentation without slides.

IPresentation presentation = Presentation.Create();

//Adds new Blank type of slide.

ISlide slide = presentation.Slides.Add(SlideLayoutType.Blank);

//Adds Rectangle auto shape with specified size and positions.

IShape shape = slide.Shapes.AddShape(AutoShapeType.Rectangle, 1.92 * 72, 1.51 * 72, 10.85 * 72, 4.12 * 72);

//Adds text into the shape.

shape.TextBody.AddParagraph("Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula");

//Creates new memory stream to save Presentation.

MemoryStream stream = new MemoryStream();

//Saves Presentation in stream format.

presentation.Save(stream);

presentation.Close();

stream.Position = 0;

Xamarin.Forms.DependencyService.Get<ISave>().Save("GettingStartedSample.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
{% endhighlight %}
{% endtabs %}
The following code example illustrates how to save the PowerPoint Presentation in Xamarin.iOS platform.
{% tabs %}
{% highlight c# %}
//Creates new Presentation without slides.

IPresentation presentation = Presentation.Create();

//Adds new Blank type of slide.

ISlide slide = presentation.Slides.Add(SlideLayoutType.Blank);

//Adds Rectangle auto shape with specified size and positions.

IShape shape = slide.Shapes.AddShape(AutoShapeType.Rectangle, 1.92 * 72, 1.51 * 72, 10.85 * 72, 4.12 * 72);

//Adds text into the shape.

shape.TextBody.AddParagraph("Lorem ipsum dolor sit amet, lacus amet amet ultricies. Quisque mi venenatis morbi libero, orci dis, mi ut et class porta, massa ligula magna enim, aliquam orci vestibulum Turpis facilisis vitae consequat, cum a a,turpis dui consequat massa in dolor per, felis non amet.Auctor eleifend in omnis elit vestibulum, donec non elementum tellus est mauris, id aliquam, at lacus, arcu pretium proin lacus dolor et. Eu tortor, vel ultrices amet dignissim mauris vehicula");

//Creates new memory stream to save Presentation.

MemoryStream stream = new MemoryStream();

//Saves Presentation in stream format.

presentation.Save(stream);

presentation.Close();

stream.Position = 0;

Xamarin.Forms.DependencyService.Get<ISave>().Save("GettingStartedSample.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
{% endhighlight %}
{% endtabs %}

N> The image and PDF conversions are not supported in Xamarin.Forms, Xamarin.Android and Xamarin.IOS platforms.
