---
title: Create and edit macros in PowerPoint files | Syncfusion |
description: Learn here all about working with macros in Syncfusion Essential PowerPoint Presentation Library and more.
platform: file-formats
control: Presentation
documentation: UG
---
# Working with Macros in PowerPoint Presentation Library

A macro is a series of commands that can be grouped together as a single command to automate a frequently used tasks. Macros can be created for Microsoft PowerPoint using Visual Basic for Applications (VBA). Please refer [Create Macros in PowerPoint](https://support.office.com/en-us/article/Create-a-macro-in-PowerPoint-5b07aff6-4dc9-462f-8fc9-66b4c5344e7e?ui=en-US&rs=en-US&ad=US) for more details

Macros enabled PowerPoint presentations of file types - .PPTM and .POTM can only be preserved using Essential Presentation.

## Loading and Saving Macro enabled Presentation

The following code illustrates how to load and save a macro enabled presentation.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Opens an existing macro enabled PowerPoint presentation
FileStream inputStream = new FileStream("Sample.PPTM",FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);
//Adds a blank slide to the presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Adds a text box to the slide
IParagraph paragraph = slide.Shapes.AddTextBox(100, 100, 300, 80).TextBody.AddParagraph("Preserve Macros");
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Output.PPTM", FileMode.Create);
pptxDoc.Save(outputStream);
//Closes the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Opens an existing macro enabled PowerPoint presentation
IPresentation pptxDoc = Presentation.Open("Sample.PPTM");
//Adds a blank slide to the presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Adds a text box to the slide
IParagraph paragraph = slide.Shapes.AddTextBox(100, 100, 300, 80).TextBody.AddParagraph("Preserve Macros");
//Saves the presentation
pptxDoc.Save("Output.PPTM");
//Closes the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Opens an existing macro enabled PowerPoint presentation
Dim pptxDoc As IPresentation = Presentation.Open("Sample.PPTM")
'Adds a blank slide to the presentation
Dim slide As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank)
'Adds a text box to the slide
Dim paragraph As IParagraph = slide.Shapes.AddTextBox(100, 100, 300, 80).TextBody.AddParagraph("Preserve Macros")
'Saves the presentation
pptxDoc.Save("Output.PPTM")
'Closes the presentation
pptxDoc.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Macros/Load-and-save-macro-PowerPoint).

## Removing Macros from Macro enabled Presentation

The following code example illustrates how to remove the macros present in the presentation,

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Opens an existing macro enabled PowerPoint presentation
FileStream inputStream = new FileStream("Sample.PPTM",FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);
//Checks whether the presentation has macros and then removes them
if (pptxDoc.HasMacros)
    pptxDoc.RemoveMacros();
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Output.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
//Closes the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Opens an existing macro enabled PowerPoint presentation
IPresentation pptxDoc = Presentation.Open("Sample.PPTM");
//Checks whether the presentation has macros and then removes them
if (pptxDoc.HasMacros)
    pptxDoc.RemoveMacros();
//Saves the presentation
pptxDoc.Save("Output.pptx");
//Closes the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Opens an existing macro enabled PowerPoint presentation
Dim pptxDoc As IPresentation = Presentation.Open("Sample.PPTM")
'Checks whether the presentation has macros and then removes them
If pptxDoc.HasMacros Then
    pptxDoc.RemoveMacros()
End If
'Saves the presentation
pptxDoc.Save("Output.pptx")
'Closes the presentation
pptxDoc.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Macros/Remove-macros).