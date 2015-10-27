---
layout: Post
title: Loading and Saving the presentation in ASP.NET platform
description: Loading and Saving the presentation in ASP.NET platform
platform: ASP.NET
control: Presentation
documentation: FileFormats
---
## ASP.NET

The below code snippet demonstrates how to load and save a PowerPoint presentation in ASP.NET platform:

{% highlight c# %}
[C#]

//Open an existing PowerPoint presentation

IPresentation presentationDocument = Presentation.Open("Sample.pptx");

//Add slide to the presentation

ISlide slide = presentationDocument.Slides.Add(SlideLayoutType.Blank);

//Add paragraph to the text box

IParagraph paragraph = slide.Shapes.AddTextBox(100, 120, 300, 200).TextBody.AddParagraph("Sample Text");

//Save the presentation

presentationDocument.Save("Output.pptx", FormatType.Pptx, Response);



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Open an existing PowerPoint presentation

Dim presentationDocument As IPresentation = Presentation.Open("Sample.pptx")

'Add slide to the presentation

Dim slide As ISlide = presentationDocument.Slides.Add(SlideLayoutType.Blank)

'Add paragraph to the text box

Dim paragraph As IParagraph = slide.Shapes.AddTextBox(100, 120, 300, 200).TextBody.AddParagraph("Sample Text")

'Save the presentation

presentationDocument.Save("Output.pptx", FormatType.Pptx, Response)





{% endhighlight %}

