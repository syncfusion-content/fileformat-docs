---
layout: Post
title: Working with Paragraph in PowerPoint Presentation
description: Working with Paragraph in PowerPoint Presentation
platform: FileFormats
control: Presentation
documentation: UG
---
# Working with Paragraph

## Adding Paragraph to slide

All the textual contents in a Presentation document is represented by Paragraphs. We can have any number of paragraphs within a [TextBody](http://www.google.com/# "") of a textbox or shape in a PowerPoint presentation. 

The below code snippet demonstrates adding a paragraph in a slide.

{% highlight c# %}
[C#]

//Create PowerPoint instance

IPresentation presentation = Presentation.Create();

//Add slide to the PowerPoint

ISlide slide = presentation.Slides.Add(SlideLayoutType.Blank);

//Add textbox to the slide

IShape textboxShape = slide.AddTextBox(0, 0, 500, 500);

//Add paragraph to the textbody of textbox

IParagraph paragraph = textboxShape.TextBody.AddParagraph();

//Add textpart to the paragraph

ITextPart textPart = paragraph.AddTextPart();

//Add text to the textpart

textPart.Text = "Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularized in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.";

//Save the presentation

presentation.Save("Output.pptx");

//Close the presentation

presentation.Close();



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Create PowerPoint instance

Dim presentation_1 As IPresentation = Presentation.Create()

'Add slide to the PowerPoint

Dim slide As ISlide = presentation_1.Slides.Add(SlideLayoutType.Blank)

'Add textbox to the slide

Dim textboxShape As IShape = slide.AddTextBox(0, 0, 500, 500)

'Add paragraph to the textbody of textbox

Dim paragraph As IParagraph = textboxShape.TextBody.AddParagraph()

'Add textpart to the paragraph

Dim textPart As ITextPart = paragraph.AddTextPart()

'Add text to the textpart

textPart.Text = "Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularized in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum."

'Save the presentation

presentation_1.Save("Output.pptx")

'Close the presentation

presentation_1.Close()



{% endhighlight %}

## Applying Paragraph formatting

Each paragraph in a slide can have its own formatting such as alignment, indent etc.  The below code snippet demonstrates how to format a paragraph in PowerPoint presentation.

{% highlight c# %}
[C#]

//Load the PowerPoint presentation

IPresentation presentation = Presentation.Open("Sample.pptx");

//Get the slide from presentation

ISlide slide = presentation.Slides[0];

//Get the shape in slide

IShape textboxShape = slide.Shapes[0] as IShape;  

//Get instance of a paragraph in a textbox

IParagraph paragraph = textboxShape.TextBody.Paragraphs[0];

//Applies the first line indent of the paragraph

paragraph.FirstLineIndent = 10;

//Applies the horizontal alignment of the paragraph to center.

paragraph.HorizontalAlignment = HorizontalAlignmentType.Left;

//Applies the left indent of the paragraph

paragraph.LeftIndent = 8;

//Save the presentation

presentation.Save("Output.pptx");

//Close the presentation

presentation.Close();



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Load the PowerPoint presentation

Dim presentation_1 As IPresentation = Presentation.Open("Sample.pptx")

'Get the slide from presentation

Dim slide As ISlide = presentation_1.Slides(0)

'Get the shape in slide

Dim textboxShape As IShape = TryCast(slide.Shapes(0), IShape)

'Get instance of a paragraph in a textbox

Dim paragraph As IParagraph = textboxShape.TextBody.Paragraphs(0)

'Applies the first line indent of the paragraph

paragraph.FirstLineIndent = 10

'Applies the horizontal alignment of the paragraph to center.

paragraph.HorizontalAlignment = HorizontalAlignmentType.Left

'Applies the left indent of the paragraph

paragraph.LeftIndent = 8

'Save the presentation

presentation_1.Save("Output.pptx")

'Close the presentation

presentation_1.Close()



{% endhighlight %}

## Working with text

With Essential Presentation, we can add or modify the text in a presentation. Within the paragraph, textual contents are grouped into one or more child elements as [TextParts](http://www.google.com/# ""). Each TextPart represents a region of text with a common set of formatted text. The below code snippet demonstrates how to add text parts with different formatting into a single paragraph.

{% highlight c# %}
[C#]

//Load the PowerPoint presentation

IPresentation presentation = Presentation.Create();

//Get the slide from presentation

ISlide slide = presentation.Slides.Add(SlideLayoutType.Blank);

//Add textbox to the slide

IShape textboxShape2 = slide.AddTextBox(500, 0, 400, 500);

//Add paragraph to the textbody of textbox

IParagraph paragraph2 = textboxShape2.TextBody.AddParagraph();

//Add textpart to the paragraph

ITextPart textPartFormatting = paragraph2.AddTextPart();

//Add text to the textpart

textPartFormatting.Text = "The standard chunk of Lorem Ipsum used since the 1500s is reproduced below for those interested. Sections 1.10.32 and 1.10.33 from 'de Finibus Bonorum et Malorum' by Cicero are also reproduced in their exact original form, accompanied by English versions from the 1914 translation by H. Rackham.";

//Set the underline color

textPartFormatting.UnderLineColor.SystemColor = Color.Black;

//Retrieve the existing font for modification

IFont font = textPartFormatting.Font;

//Set the underline type

font.UnderLine = TextUnderlineType.Single;

//Set the font weight

font.Bold = true;

//Add textpart to the paragraph

ITextPart textPartFormatting2 = paragraph2.AddTextPart();

//Add text to the textpart

textPartFormatting2.Text = "The standard chunk of Lorem Ipsum used since the 1500s is reproduced below for those interested.";

//Retrieve the existing font for modification

IFont font2 = textPartFormatting2.Font;

//Set the font color

font2.Color.SystemColor = Color.Blue;

//Set the underline type

font2.UnderLine = TextUnderlineType.WavyDouble;

//Save the presentation

presentation.Save("Output.pptx");

//Close the presentation

presentation.Close();



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Load the PowerPoint presentation

Dim presentation_1 As IPresentation = Presentation.Create()

'Get the slide from presentation

Dim slide As ISlide = presentation_1.Slides.Add(SlideLayoutType.Blank)

'Add textbox to the slide

Dim textboxShape2 As IShape = slide.AddTextBox(500, 0, 400, 500)

'Add paragraph to the textbody of textbox

Dim paragraph2 As IParagraph = textboxShape2.TextBody.AddParagraph()

'Add textpart to the paragraph

Dim textPartFormatting As ITextPart = paragraph2.AddTextPart()

'Add text to the textpart

textPartFormatting.Text = "The standard chunk of Lorem Ipsum used since the 1500s is reproduced below for those interested. Sections 1.10.32 and 1.10.33 from 'de Finibus Bonorum et Malorum' by Cicero are also reproduced in their exact original form, accompanied by English versions from the 1914 translation by H. Rackham."

'Set the underline color

textPartFormatting.UnderLineColor.SystemColor = Color.Black

'Retrieve the existing font for modification

Dim font As IFont = textPartFormatting.Font

'Set the underline type

font.UnderLine = TextUnderlineType.[Single]

'Set the font weight

font.Bold = True

'Add textpart to the paragraph

Dim textPartFormatting2 As ITextPart = paragraph2.AddTextPart()

'Add text to the textpart

textPartFormatting2.Text = "The standard chunk of Lorem Ipsum used since the 1500s is reproduced below for those interested."

'Retrieve the existing font for modification

Dim font2 As IFont = textPartFormatting2.Font

'Set the font color

font2.Color.SystemColor = Color.Blue

'Set the underline type

font2.UnderLine = TextUnderlineType.WavyDouble

'Save the presentation

presentation_1.Save("Output.pptx")

'Close the presentation

presentation_1.Close()



{% endhighlight %}

## Modifying text

You can modify a text by accessing the existing paragraphs in a presentation. The below code snippet demonstrates modifying the content in a paragraph.

{% highlight c# %}
[C#]

//Open an existing presentation from file system.

IPresentation presentation = Presentation.Open("Sample.pptx");

//Retrieve the first slide from presentation

ISlide slide = presentation.Slides[0];

//Retrieve the first shape.

IShape shape = slide.Shapes[0] as IShape;

//Retrieve the first paragraph of the shape.

IParagraph paragraph = shape.TextBody.Paragraphs[0];

//Retrieve the first text part of the shape.

ITextPart textPart = paragraph.TextParts[0];

//Modifies the text content of the textpart.

textPart.Text = "Hello Presentation";

//Save the presenation to the file system.

presentation.Save("Result.pptx");

//Close the presentation.

presentation.Close();



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Open an existing presentation from file system.

Dim presentation_1 As IPresentation = Presentation.Open("Sample.pptx")

'Retrieve the first slide from presentation

Dim slide As ISlide = presentation_1.Slides(0)

'Retrieve the first shape.

Dim shape As IShape = TryCast(slide.Shapes(0), IShape)

'Retrieve the first paragraph of the shape.

Dim paragraph As IParagraph = shape.TextBody.Paragraphs(0)

'Retrieve the first text part of the shape.

Dim textPart As ITextPart = paragraph.TextParts(0)

'Modifies the text content of the textpart.

textPart.Text = "Hello Presentation"

'Save the presenation to the file system.

presentation_1.Save("Result.pptx")

'Close the presentation.

presentation_1.Close()



{% endhighlight %}

## Removing the paragraph 

The below code snippet demonstrates removing a paragraph from a slide.

{% highlight c# %}
[C#]

//Open an existing presentation from file system.

IPresentation presentation = Presentation.Open("Sample.pptx");

//Retrieve the first slide from presentation

ISlide slide = presentation.Slides[0];

//Retrieve the first shape.

IShape shape = slide.Shapes[0] as IShape;

//Retrieve the first paragraph of the shape.

IParagraph paragraph = shape.TextBody.Paragraphs[0];

//Remove the first paragraph from the textbody of the shape.

shape.TextBody.Paragraphs.Remove(paragraph);

//Save the presenation to the file system.

presentation.Save("Result.pptx");

//Close the presentation.

presentation.Close();



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Open an existing presentation from file system.

Dim presentation_1 As IPresentation = Presentation.Open("Sample.pptx")

'Retrieve the first slide from presentation

Dim slide As ISlide = presentation_1.Slides(0)

'Retrieve the first shape.

Dim shape As IShape = TryCast(slide.Shapes(0), IShape)

'Retrieve the first paragraph of the shape.

Dim paragraph As IParagraph = shape.TextBody.Paragraphs(0)

'Remove the first paragraph from the textbody of the shape.

shape.TextBody.Paragraphs.Remove(paragraph)

'Save the presenation to the file system.

presentation_1.Save("Result.pptx")

'Close the presentation.

presentation_1.Close()



{% endhighlight %}

