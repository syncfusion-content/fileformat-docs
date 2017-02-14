---
title: Working with macros in PowerPoint Presentation
description: Working with macros in PowerPoint Presentation
platform: file-formats
control: Presentation
documentation: UG
---
# Working with Macros

A macro is a series of commands that can be grouped together as a single command to automate a frequently used tasks. Macros can be created for Microsoft PowerPoint using Visual Basic for Applications (VBA). Please refer [Create Macros in PowerPoint](https://support.office.com/en-us/article/Create-a-macro-in-PowerPoint-5b07aff6-4dc9-462f-8fc9-66b4c5344e7e?ui=en-US&rs=en-US&ad=US) for more details

Macros enabled PowerPoint presentations of file types - .PPTM and .POTM can only be preserved using Essential Presentation.

## Loading and Saving Macro enabled Presentation

The following code illustrates how to load and save a macro enabled presentation.

{% tabs %}

{% highlight c# %}

//Opens an existing macro enabled PowerPoint presentation

IPresentation presentation = Presentation.Open("Test.pptm");

//Adds a blank slide to the presentation

ISlide slide = presentation.Slides.Add(SlideLayoutType.Blank);

//Adds a text box to the slide

IParagraph paragraph = slide.Shapes.AddTextBox(100, 100, 300, 80).TextBody.AddParagraph("Preserve Macros");

//Saves the presentation

presentation.Save("Output.pptm");

//Closes the presentation

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing macro enabled PowerPoint presentation

Dim presentationDocument As IPresentation = Presentation.Open("Test.pptm")

'Adds a blank slide to the presentation

Dim slide As ISlide = presentationDocument.Slides.Add(SlideLayoutType.Blank)

'Adds a text box to the slide

Dim paragraph As IParagraph = slide.Shapes.AddTextBox(100, 100, 300, 80).TextBody.AddParagraph("Preserve Macros")

'Saves the presentation

presentationDocument.Save("Output.pptm")

'Closes the presentation

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

## Removing Macros from Macro enabled Presentation

The following code example illustrates how to remove the macros present in the presentation,

{% tabs %}

{% highlight c# %}

//Opens an existing macro enabled PowerPoint presentation

IPresentation presentation = Presentation.Open("Sample.pptm");

//Checks whether the presentation has macros and then removes them

if (presentation.HasMacros)

presentation.RemoveMacros();

//Saves the presentation

presentation.Save("Output.pptx");

//Closes the presentation

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing macro enabled PowerPoint presentation

Dim presentationDocument As IPresentation = Presentation.Open("Sample.pptm")

'Checks whether the presentation has macros and then removes them

If presentationDocument.HasMacros Then

presentationDocument.RemoveMacros()

End If

'Saves the presentation

presentationDocument.Save("Output.pptx")

'Closes the presentation

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

