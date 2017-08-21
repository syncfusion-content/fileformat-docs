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

//Adds a shape with specified size and position.

IShape shape = slide.Shapes.AddShape(AutoShapeType.Rectangle, 1.92 * 72, 1.51 * 72, 10.85 * 72, 4.12 * 72);

//Adds text into the shape.

shape.TextBody.AddParagraph("In 2000, Adventure Works Cycles bought a small manufacturing plant, Importadores Neptuno, located in Mexico. Importadores Neptuno manufactures several critical subcomponents for the Adventure Works Cycles product line. These subcomponents are shipped to the Bothell location for final product assembly. In 2001, Importadores Neptuno, became the sole manufacturer and distributor of the touring bicycle product group.");

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

//Adds a shape with specified size and position.

IShape shape = slide.Shapes.AddShape(AutoShapeType.Rectangle, 1.92 * 72, 1.51 * 72, 10.85 * 72, 4.12 * 72);

//Adds text into the shape.

shape.TextBody.AddParagraph("The Northwind sample database (Northwind.mdb) is included with all versions of Access. It provides data you can experiment with and database objects that demonstrate features you might want to implement in your own databases. Using Northwind, you can become familiar with how a relational database is structured and how the database objects work together to help you enter, store, manipulate, and print your data.");

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

//Adds a shape with specified size and position.

IShape shape = slide.Shapes.AddShape(AutoShapeType.Rectangle, 1.92 * 72, 1.51 * 72, 10.85 * 72, 4.12 * 72);

//Adds text into the shape.

shape.TextBody.AddParagraph("Adventure Works Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company. The company manufactures and sells metal and composite bicycles to North American, European and Asian commercial markets. While its base operation is located in Bothell, Washington with 290 employees, several regional sales teams are located throughout their market base.");

//Creates new memory stream to save Presentation.

MemoryStream stream = new MemoryStream();

//Saves Presentation in stream format.

presentation.Save(stream);

presentation.Close();

stream.Position = 0;

Xamarin.Forms.DependencyService.Get<ISave>().Save("GettingStartedSample.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
{% endhighlight %}
{% endtabs %}

N> The image and PDF conversions are not supported in Xamarin platforms.
