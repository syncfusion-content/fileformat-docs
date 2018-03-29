---
title: Creating, loading and modifying the PowerPoint presentation in ASP.NET Core platform
description: Creating, loading and modifying the PowerPoint presentation in ASP.NET Core platform
platform: file-formats
control: Presentation
documentation: UG
keywords: PPTX, ASP.NET Core, Presentation, Modify Presentation, Create Presentation
---
# ASP.NET Core

The Presentation component is supported in ASP.NET Core platform from .NET Core 1.0 version. For more details about configuring Syncfusion file-format components in ASP.NET Core application please click [here](https://help.syncfusion.com/aspnet-core/gettingstarted/getting-started-1-1-0#configure-syncfusion-file-format-components-in-aspnet-core-application).

## Packages Required

The below packages are required to create and modify the PowerPoint presentations.

1. Syncfusion.Compression.Portable
2. Syncfusion.OfficeChart.Portable
3. Syncfusion.Presentation.Portable

The below code snippet demonstrates how to create a PowerPoint Presentation in ASP.NET Core platform.

{% tabs %}
{% highlight c# %}
//Creates a new instance of PowerPoint Presentation

IPresentation presentation = Presentation.Create();

//Adds a slide to Presentation
ISlide firstSlide = presentation.Slides.Add(SlideLayoutType.Blank);

//Adds a textbox in a slide by specifying its position and size
IShape textShape = firstSlide.AddTextBox(100, 75, 756, 200);

//Adds a paragraph into the textShape
IParagraph paragraph = textShape.TextBody.AddParagraph();

//Set the horizontal alignment of paragraph 
paragraph.HorizontalAlignment = HorizontalAlignmentType.Center;

//Adds a textPart in the paragraph
ITextPart textPart = paragraph.AddTextPart("Hello Presentation");

 //Applies font formatting to the text
textPart.Font.FontSize = 80;
textPart.Font.Bold = true;

//Saves the Presentation in the given name 
presentation.Save("Sample.pptx");

//Releases the resources occupied
presentation.Close();
{% endhighlight %}
{% endtabs %}

The below code snippet demonstrates how to load and modify an existing Presentation in ASP.NET Core platform.

{% tabs %}
{% highlight c# %}
using (FileStream fileStream = new FileStream("Sample.pptx", FileMode.OpenOrCreate))
{
 //Loads the existing PowerPoint Presentation
 IPresentation presentation = Presentation.Open(fileStream);
 
//Retrieves the first slide from Presentation
 ISlide slide = presentation.Slides[0];
 
//Retrieves the first shape.
 IShape shape = slide.Shapes[0] as IShape;
 
 //Retrieves the first paragraph of the shape.
 IParagraph paragraph = shape.TextBody.Paragraphs[0];
 
//Retrieves the first text part of the shape.
 ITextPart textPart = paragraph.TextParts[0];
 
//Modifies the text content of the TextPart instance.
textPart.Text = "Hello Presentation";

//Saves the presentation to the file system.
presentation.Save("Modified.pptx");

//Closes the Presentation.
 presentation.Close();
 }
{% endhighlight %}
{% endtabs %}
