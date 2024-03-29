---
title: Working with Hyperlinks | Syncfusion
description: This section explains how to add hyperlink in the PowerPoint slide using Essential Presentation library
platform: file-formats
control: Presentation
documentation: UG
---
# Working with Hyperlinks

The Hyperlink is a reference to data that can link to external contents like images, files, webpage, and more. In PowerPoint slide, a hyperlink may target to any one of the following sources:

* Webpage: Represents the web content.
* File: Represents the file in some location.
* Email: Represents an Email.
* Slide: Represents the slide in the same document.

## Add hyperlink to PowerPoint shape

You can navigate to any slide of the same PowerPoint document. The following code example demonstrates how to add the hyperlink for internal document navigation.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Creates the PowerPoint Presentation instance
IPresentation pptxDoc = Presentation.Create();
//Adds a slide of blank layout type
ISlide slide1 = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Adds one more slide.
ISlide slide2 = pptxDoc.Slides.Add();
//Adds normal shape to the first slide
IShape shape = slide1.Shapes.AddShape(AutoShapeType.Rectangle, 100, 20, 200, 100);
//Sets the target slide index (index is valid from 0 to slides count – 1) as hyperlink
IHyperLink hyperLink = shape.SetHyperlink("1");
//Gets the target slide of the hyperlink
ISlide targetSlide = hyperLink.TargetSlide;
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Sample.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
//Close the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Creates the PowerPoint Presentation instance
IPresentation pptxDoc = Presentation.Create();
//Adds a slide of blank layout type
ISlide slide1 = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Adds one more slide.
ISlide slide2 = pptxDoc.Slides.Add();
//Adds normal shape to the first slide
IShape shape = slide1.Shapes.AddShape(AutoShapeType.Rectangle, 100, 20, 200, 100);
//Sets the target slide index (index is valid from 0 to slides count – 1) as hyperlink
IHyperLink hyperLink = shape.SetHyperlink("1");
//Gets the target slide of the hyperlink
ISlide targetSlide = hyperLink.TargetSlide;
//Save the presentation
pptxDoc.Save("Sample.pptx");
//Close the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Creates the PowerPoint Presentation instance
Dim pptxDoc As IPresentation = Presentation.Create() 
'Adds a slide of blank layout type
Dim slide1 As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank) 
'Adds one more slide.
Dim slide2 As ISlide = pptxDoc.Slides.Add() 
'Adds normal shape to the first slide
Dim shape As IShape = slide1.Shapes.AddShape(AutoShapeType.Rectangle, 100, 20, 200, 100) 
'Sets the target slide index (index is valid from 0 to slides count – 1) as hyperlink
Dim hyperLink As IHyperLink = shape.SetHyperlink("1")
'Gets the target slide of the hyperlink
Dim targetSlide As ISlide = hyperLink.TargetSlide
'Save the presentation
pptxDoc.Save("Sample.pptx")
'Close the presentation
pptxDoc.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Hyperlinks/Add-hyperlink-to-PowerPoint-shape).

## Add hyperlink to text

You can navigate to the specified URL from a PowerPoint slide. The following code example demonstrates how to add the web URL as a hyperlink.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Creates the PowerPoint Presentation instance
IPresentation pptxDoc = Presentation.Create();
//Adds a slide of blank layout type
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Adds normal shape to the first slide
IShape shape = slide.Shapes.AddShape(AutoShapeType.Rectangle, 100, 20, 200, 100);
//Adds paragraph into the shape
IParagraph paragraph = shape.TextBody.AddParagraph();
//Adds text to the TextPart
paragraph.Text = "Syncfusion";
//Sets the web hyperlink to the TextPart
IHyperLink hyperLink = paragraph.TextParts[0].SetHyperlink("http://www.syncfusion.com");
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Sample.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
//Close the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Creates the PowerPoint Presentation instance
IPresentation pptxDoc = Presentation.Create();
//Adds a slide of blank layout type
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Adds normal shape to the first slide
IShape shape = slide.Shapes.AddShape(AutoShapeType.Rectangle, 100, 20, 200, 100);
//Adds paragraph into the shape
IParagraph paragraph = shape.TextBody.AddParagraph();
//Adds text to the TextPart
paragraph.Text = "Syncfusion";
//Sets the web hyperlink to the TextPart
IHyperLink hyperLink = paragraph.TextParts[0].SetHyperlink("http://www.syncfusion.com");
//Save the presentation
pptxDoc.Save("Sample.pptx");
//Close the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Creates the PowerPoint Presentation instance
Dim pptxDoc As IPresentation = Presentation.Create() 
'Adds a slide of blank layout type
Dim slide As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank) 
'Adds normal shape to the first slide
Dim shape As IShape = slide.Shapes.AddShape(AutoShapeType.Rectangle,100,20,200,100) 
'Adds paragraph into the shape
Dim paragraph As IParagraph = shape.TextBody.AddParagraph() 
'Adds text to the TextPart
paragraph.Text = "Syncfusion"
'Sets the web hyperlink to the TextPart
Dim hyperLink As IHyperLink = paragraph.TextParts(0).SetHyperlink("http://www.syncfusion.com") 
'Save the presentation
pptxDoc.Save("Sample.pptx")
'Close the presentation
pptxDoc.Close()

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Hyperlinks/Add-hyperlink-to-PowerPoint-text).

## Add hyperlink to picture

You can add the email link to the shape or text on a PowerPoint slide. The following code example demonstrates how to add an email hyperlink to the picture.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Creates the PowerPoint Presentation instance
IPresentation pptxDoc = Presentation.Create();
//Adds a slide of blank layout type
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Gets a picture as stream
FileStream pictureStream = new FileStream("Image.png", FileMode.Open);
//Adds the picture to a slide by specifying its size and position.
IPicture picture = slide.Pictures.AddPicture(pictureStream, 0, 0, 250, 250);
//Sets the Email hyperlink to the picture
IHyperLink hyperLink = (picture as IShape).SetHyperlink("mailto:sales@syncfusion.com");
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Sample.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
//Close the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Creates the PowerPoint Presentation instance
IPresentation pptxDoc = Presentation.Create();
//Adds a slide of blank layout type
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Gets a picture as stream
Stream pictureStream = File.Open("Image.png", FileMode.Open);
//Adds the picture to a slide by specifying its size and position.
IPicture picture = slide.Pictures.AddPicture(pictureStream, 0, 0, 250, 250);
//Sets the Email hyperlink to the picture
IHyperLink hyperLink = (picture as IShape).SetHyperlink("mailto:sales@syncfusion.com");
//Save the presentation
pptxDoc.Save("Sample.pptx");
//Close the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Creates the PowerPoint Presentation instance
Dim pptxDoc As IPresentation = Presentation.Create() 
'Adds a slide of blank layout type
Dim slide As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank) 
'Gets a picture as stream
Dim pictureStream As Stream = File.Open("Image.png",FileMode.Open) 
'Adds the picture to a slide by specifying its size and position
Dim picture As IPicture = slide.Pictures.AddPicture(pictureStream, 0, 0, 250, 250) 
'Sets the Email hyperlink to the picture
Dim hyperLink As IHyperLink = TryCast(picture, IShape).SetHyperlink("mailto:sales@syncfusion.com") 
'Save the presentation
pptxDoc.Save("Sample.pptx")
'Close the presentation
pptxDoc.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Hyperlinks/Add-hyperlink-to-PowerPoint-picture).

You can open external documents like images, text files, PDF, etc. from the PowerPoint slide. The following code example demonstrates how to add a file hyperlink to the picture.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Creates the PowerPoint Presentation instance
IPresentation pptxDoc = Presentation.Create();
//Adds a slide of blank layout type
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Gets a picture as stream
FileStream pictureStream = new FileStream("Image.png", FileMode.Open);
//Adds the picture to a slide by specifying its size and position
IPicture picture = slide.Pictures.AddPicture(pictureStream, 0, 0, 250, 250);
//Sets the File path as hyperlink
IHyperLink hyperLink = (picture as IShape).SetHyperlink("WordDocument.docx");
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Sample.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
//Close the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Creates the PowerPoint Presentation instance
IPresentation pptxDoc = Presentation.Create();
//Adds a slide of blank layout type
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Gets a picture as stream
Stream pictureStream = File.Open("Image.png", FileMode.Open);
//Adds the picture to a slide by specifying its size and position
IPicture picture = slide.Pictures.AddPicture(pictureStream, 0, 0, 250, 250);
//Sets the File path as hyperlink
IHyperLink hyperLink = (picture as IShape).SetHyperlink("WordDocument.docx");
//Save the presentation
pptxDoc.Save("Sample.pptx");
//Close the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Creates the PowerPoint Presentation instance
Dim pptxDoc As IPresentation = Presentation.Create() 
'Adds a slide of blank layout type
Dim slide As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank) 
'Gets a picture as stream
Dim pictureStream As Stream = File.Open("Image.png",FileMode.Open) 
'Adds the picture to a slide by specifying its size and position
Dim picture As IPicture = slide.Pictures.AddPicture(pictureStream, 0, 0, 250, 250) 
'Sets the Email hyperlink to the picture
Dim hyperLink As IHyperLink = TryCast(picture, IShape).SetHyperlink("WordDocument.docx")
'Save the presentation
pptxDoc.Save("Sample.pptx")
'Close the presentation
pptxDoc.Close()

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Hyperlinks/Add-file-hyperlink-to-picture).

N> The above link makes use of the absolute path of the file for navigation. So, moving the files to another machine or location may lead to file not found error in PowerPoint reader applications.

## Gets a hyperlink details from text and shape

You can get the hyperlink details from the shape or text in a PowerPoint slide.

The following code example demonstrates how to get the details about the hyperlink from shape.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream("Sample.pptx", FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);
//Retrieves the first slide from the Presentation
ISlide slide = pptxDoc.Slides[0];
//Retrieves the first shape from the slide
IShape shape = slide.Shapes[0] as IShape;
//Gets the hyperlink from the shape
IHyperLink hyperlink = shape.Hyperlink;
//Gets the type of action, the hyperlink will be performed when the shape is clicked
HyperLinkType hyperlinkType = hyperlink.Action;
//Gets the target slide of the hyperlink
ISlide targetSlide = hyperlink.TargetSlide;
//Gets the url address of the hyperlink
string url = hyperlink.Url;
//Gets the screen tip text of a hyperlink
string screenTip = hyperlink.ScreenTip;
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Result.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
//Close the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Open an existing PowerPoint presentation
IPresentation pptxDoc = Presentation.Open("Sample.pptx");
//Retrieves the first slide from the Presentation
ISlide slide = pptxDoc.Slides[0];
//Retrieves the first shape from the slide
IShape shape = slide.Shapes[0] as IShape;
//Gets the hyperlink from the shape
IHyperLink hyperlink = shape.Hyperlink;
//Gets the type of action, the hyperlink will be performed when the shape is clicked
HyperLinkType hyperlinkType = hyperlink.Action;
//Gets the target slide of the hyperlink
ISlide targetSlide = hyperlink.TargetSlide;
//Gets the url address of the hyperlink
string url = hyperlink.Url;
//Gets the screen tip text of a hyperlink
string screenTip = hyperlink.ScreenTip;
//Save the presentation
pptxDoc.Save("Result.pptx");
//Close the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Open an existing PowerPoint presentation
Dim pptxDoc As IPresentation = Presentation.Open("Table.pptx")
'Retrieves the first shape from the slide
Dim shape As IShape = TryCast(slide.Shapes(0), IShape) 
'Gets the hyperlink from the shape
Dim hyperlink As IHyperLink = shape.Hyperlink 
'Gets the type of action, the hyperlink will be performed when the shape is clicked
Dim hyperlinkType As HyperLinkType = hyperlink.Action 
'Gets the target slide of the hyperlink
Dim targetSlide As ISlide = hyperlink.TargetSlide 
'Gets the url address of the hyperlink
Dim url As String = hyperlink.Url 
'Gets the screen tip text of a hyperlink
Dim screenTip As String = hyperlink.ScreenTip 
'Save the presentation
pptxDoc.Save("Sample.pptx")
'Close the presentation
pptxDoc.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Hyperlinks/Get-hyperlink-from-shape).

The following code example demonstrates how to get the details about the hyperlink from text.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream("Sample.pptx", FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);
//Retrieves the first slide from the Presentation.
ISlide slide = pptxDoc.Slides[0];
//Retrieves the first shape from the slide
IShape shape = slide.Shapes[0] as IShape;
//Retrieves the first paragraph of the shape
IParagraph paragraph = shape.TextBody.Paragraphs[0];
//Retrieves the first TextPart of the shape
ITextPart textPart = paragraph.TextParts[0];
//Gets the hyperlink from the text
IHyperLink hyperlink = textPart.Hyperlink;
//Gets the type of action, the hyperlink will be performed when the shape is clicked
HyperLinkType hyperlinkType = hyperlink.Action;
//Gets the target slide of the hyperlink
ISlide targetSlide = hyperlink.TargetSlide;
//Gets the url address of the hyperlink
string url = hyperlink.Url;
//Gets the screen tip text of a hyperlink
string screenTip = hyperlink.ScreenTip;
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Result.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
//Close the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Open an existing PowerPoint presentation
IPresentation pptxDoc = Presentation.Open("Sample.pptx");
//Retrieves the first slide from the Presentation
ISlide slide = pptxDoc.Slides[0];
//Retrieves the first shape from the slide
IShape shape = slide.Shapes[0] as IShape;
//Retrieves the first paragraph of the shape
IParagraph paragraph = shape.TextBody.Paragraphs[0];
//Retrieves the first TextPart of the shape
ITextPart textPart = paragraph.TextParts[0];
//Gets the hyperlink from the text
IHyperLink hyperlink = textPart.Hyperlink;
//Gets the type of action, the hyperlink will be performed when the shape is clicked
HyperLinkType hyperlinkType = hyperlink.Action;
//Gets the target slide of the hyperlink
ISlide targetSlide = hyperlink.TargetSlide;
//Gets the url address of the hyperlink
string url = hyperlink.Url;
//Gets the screen tip text of a hyperlink
string screenTip = hyperlink.ScreenTip;
//Save the presentation
pptxDoc.Save("Result.pptx");
//Close the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Open an existing PowerPoint presentation
Dim pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
'Retrieves the first shape from the slide
Dim shape As IShape = TryCast(slide.Shapes(0), IShape)
'Retrieves the first paragraph of the shape
Dim paragraph As IParagraph = shape.TextBody.Paragraphs(0)
'Retrieves the first TextPart of the shape
Dim textPart As ITextPart = paragraph.TextParts(0)
'Gets the hyperlink from the text
Dim hyperlink As IHyperLink = textPart.Hyperlink 
'Gets the type of action, the hyperlink will be performed when the shape is clicked
Dim hyperlinkType As HyperLinkType = hyperlink.Action 
'Gets the target slide of the hyperlink
Dim targetSlide As ISlide = hyperlink.TargetSlide 
'Gets the url address of the hyperlink
Dim url As String = hyperlink.Url 
'Gets the screen tip text of a hyperlink
Dim screenTip As String = hyperlink.ScreenTip 
'Save the presentation
pptxDoc.Save("Result.pptx")
'Close the presentation
pptxDoc.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Hyperlinks/Get-hyperlink-from-text).

## Remove a hyperlink from text and shape

You can remove the hyperlink from the shape or text in a PowerPoint slide.

The following code example demonstrates how to remove a hyperlink from the shape in a PowerPoint slide.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream("Sample.pptx", FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);
//Retrieves the first slide from the Presentation
ISlide slide = pptxDoc.Slides[0];
//Retrieves the first shape from the slide
IShape shape = slide.Shapes[0] as IShape;
//Removes the hyperlink from the shape
shape.RemoveHyperlink();
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Result.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
//Close the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Open an existing PowerPoint presentation
IPresentation pptxDoc = Presentation.Open("Sample.pptx");
//Retrieves the first slide from the Presentation
ISlide slide = pptxDoc.Slides[0];
//Retrieves the first shape from the slide
IShape shape = slide.Shapes[0] as IShape;
//Removes the hyperlink from the shape
shape.RemoveHyperlink();
//Save the presentation
pptxDoc.Save("Result.pptx");
//Close the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Open an existing PowerPoint presentation
Dim pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
'Retrieves the first shape from the slide
Dim shape As IShape = TryCast(slide.Shapes(0), IShape)
'Removes the hyperlink from the shape
shape.RemoveHyperlink()
'Save the presentation
pptxDoc.Save("Result.pptx")
'Close the presentation
pptxDoc.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Hyperlinks/Remove-hyperlink-from-shape).

The following code example demonstrates how to remove a hyperlink from the text in a PowerPoint slide.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream("Sample.pptx", FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);
//Retrieves the first slide from the Presentation
ISlide slide = pptxDoc.Slides[0];
//Retrieves the first shape from the slide
IShape shape = slide.Shapes[0] as IShape;
//Retrieves the first paragraph of the shape
IParagraph paragraph = shape.TextBody.Paragraphs[0];
//Retrieves the first TextPart of the shape
ITextPart textPart = paragraph.TextParts[0];
//Removes the hyperlink from the TextPart
textPart.RemoveHyperLink();
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Result.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
//Close the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Open an existing PowerPoint presentation
IPresentation pptxDoc = Presentation.Open("Sample.pptx");
//Retrieves the first slide from the Presentation
ISlide slide = pptxDoc.Slides[0];
//Retrieves the first shape from the slide
IShape shape = slide.Shapes[0] as IShape;
//Retrieves the first paragraph of the shape
IParagraph paragraph = shape.TextBody.Paragraphs[0];
//Retrieves the first TextPart of the shape
ITextPart textPart = paragraph.TextParts[0];
//Removes the hyperlink from the TextPart
textPart.RemoveHyperLink();
//Save the presentation
pptxDoc.Save("Result.pptx");
//Close the presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Open an existing PowerPoint presentation
Dim pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
'Retrieves the first shape from the slide
Dim shape As IShape = TryCast(slide.Shapes(0), IShape)
'Retrieves the first paragraph of the shape
Dim paragraph As IParagraph = shape.TextBody.Paragraphs(0)
'Retrieves the first TextPart of the shape
Dim textPart As ITextPart = paragraph.TextParts(0)
'Removes the hyperlink from the TextPart
textPart.RemoveHyperLink()
'Save the presentation
pptxDoc.Save("Result.pptx")
'Close the presentation
pptxDoc.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Hyperlinks/Remove-hyperlink-from-text).