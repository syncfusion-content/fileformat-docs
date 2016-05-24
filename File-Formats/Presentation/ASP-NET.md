---
title: Loading and Saving the Presentation in ASP.NET platform
description: Loading and Saving the Presentation in ASP.NET platform
platform: file-formats
control: Presentation
documentation: ug
---
# ASP.NET

The below code snippet demonstrates how to load and save a PowerPoint Presentation in ASP.NET platform:

{% tabs %}

{% highlight c# %}

//Open an existing PowerPoint Presentation

IPresentation presentationDocument = Presentation.Open("Sample.pptx");

//Add slide to the Presentation

ISlide slide = presentationDocument.Slides.Add(SlideLayoutType.Blank);

//Add paragraph to the text box

IParagraph paragraph = slide.Shapes.AddTextBox(100, 120, 300, 200).TextBody.AddParagraph("Sample Text");

//Save the Presentation

presentationDocument.Save("Output.pptx", FormatType.Pptx, Response);



{% endhighlight %}

{% highlight vb.net %}

'Open an existing PowerPoint Presentation

Dim presentationDocument As IPresentation = Presentation.Open("Sample.pptx")

'Add slide to the Presentation

Dim slide As ISlide = presentationDocument.Slides.Add(SlideLayoutType.Blank)

'Add paragraph to the text box

Dim paragraph As IParagraph = slide.Shapes.AddTextBox(100, 120, 300, 200).TextBody.AddParagraph("Sample Text")

'Save the Presentation

presentationDocument.Save("Output.pptx", FormatType.Pptx, Response)

{% endhighlight %}

{% endtabs %}