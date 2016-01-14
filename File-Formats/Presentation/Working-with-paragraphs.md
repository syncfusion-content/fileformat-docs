---
title: Working with Paragraph in PowerPoint Presentation
description: Working with Paragraph in PowerPoint Presentation
platform: file-formats
control: Presentation
documentation: UG
---
# Working with Paragraph

## Adding Paragraph to slide

All the textual contents in a Presentation document is represented by Paragraphs. You can have any number of paragraphs within a TextBody of a textbox or shape in a PowerPoint presentation. 

The following code example demonstrates how to add a paragraph in a slide.

{% tabs %}

{% highlight c# %}

//Creates PowerPoint instance

IPresentation presentation = Presentation.Create();

//Adds slide to the PowerPoint

ISlide slide = presentation.Slides.Add(SlideLayoutType.Blank);

//Adds textbox to the slide

IShape textboxShape = slide.AddTextBox(0, 0, 500, 500);

//Adds paragraph to the textbody of textbox

IParagraph paragraph = textboxShape.TextBody.AddParagraph();

//Adds textpart to the paragraph

ITextPart textPart = paragraph.AddTextPart();

//Adds text to the textpart

textPart.Text = "Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularized in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.";

//Saves the presentation

presentation.Save("Output.pptx");

//Closes the presentation

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates PowerPoint instance

Dim presentationDocument As IPresentation = Presentation.Create()

'Adds slide to the PowerPoint

Dim slide As ISlide = presentationDocument.Slides.Add(SlideLayoutType.Blank)

'Adds textbox to the slide

Dim textboxShape As IShape = slide.AddTextBox(0, 0, 500, 500)

'Adds paragraph to the textbody of textbox

Dim paragraph As IParagraph = textboxShape.TextBody.AddParagraph()

'Adds textpart to the paragraph

Dim textPart As ITextPart = paragraph.AddTextPart()

'Adds text to the textpart

textPart.Text = "Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularized in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum."

'Saves the presentation

presentationDocument.Save("Output.pptx")

'Closes the presentation

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

## Applying Paragraph formatting

Each paragraph in a slide can has its own formatting types such as alignment, indent etc. The following code example demonstrates how to format a paragraph in PowerPoint presentation.

{% tabs %}

{% highlight c# %}

//Loads the PowerPoint presentation

IPresentation presentation = Presentation.Open("Sample.pptx");

//Gets the slide from presentation

ISlide slide = presentation.Slides[0];

//Gets the shape in slide

IShape textboxShape = slide.Shapes[0] as IShape;  

//Gets instance of a paragraph in a textbox

IParagraph paragraph = textboxShape.TextBody.Paragraphs[0];

//Applies the first line indent of the paragraph

paragraph.FirstLineIndent = 10;

//Applies the horizontal alignment of the paragraph to center.

paragraph.HorizontalAlignment = HorizontalAlignmentType.Left;

//Applies the left indent of the paragraph

paragraph.LeftIndent = 8;

//Saves the presentation

presentation.Save("Output.pptx");

//Closes the presentation

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Loads the PowerPoint presentation

Dim presentationDocument As IPresentation = Presentation.Open("Sample.pptx")

'Gets the slide from presentation

Dim slide As ISlide = presentationDocument.Slides(0)

'Gets the shape in slide

Dim textboxShape As IShape = TryCast(slide.Shapes(0), IShape)

'Gets instance of a paragraph in a textbox

Dim paragraph As IParagraph = textboxShape.TextBody.Paragraphs(0)

'Applies the first line indent of the paragraph

paragraph.FirstLineIndent = 10

'Applies the horizontal alignment of the paragraph to center.

paragraph.HorizontalAlignment = HorizontalAlignmentType.Left

'Applies the left indent of the paragraph

paragraph.LeftIndent = 8

'Saves the presentation

presentationDocument.Save("Output.pptx")

'Closes the presentation

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

## Working with text

With Essential Presentation, you can add or modify the text in a presentation. Within the paragraph, textual contents are grouped into one or more child elements as TextParts. Each TextPart represents a region of text with a common set of formatted text. The following code example demonstrates how to add text parts with different formatting into a single paragraph.

{% tabs %}

{% highlight c# %}

//Loads the PowerPoint presentation

IPresentation presentation = Presentation.Create();

//Gets the slide from presentation

ISlide slide = presentation.Slides.Add(SlideLayoutType.Blank);

//Adds textbox to the slide

IShape textboxShape2 = slide.AddTextBox(500, 0, 400, 500);

//Adds paragraph to the textbody of textbox

IParagraph paragraph2 = textboxShape2.TextBody.AddParagraph();

//Adds textpart to the paragraph

ITextPart textPartFormatting = paragraph2.AddTextPart();

//Adds text to the textpart

textPartFormatting.Text = "The standard chunk of Lorem Ipsum used since the 1500s is reproduced below for those interested. Sections 1.10.32 and 1.10.33 from 'de Finibus Bonorum et Malorum' by Cicero are also reproduced in their exact original form, accompanied by English versions from the 1914 translation by H. Rackham.";

//Sets the underline color

textPartFormatting.UnderlineColor.SystemColor = Color.Black;

//Retrieves the existing font for modification

IFont font = textPartFormatting.Font;

//Sets the underline type

font.Underline = TextUnderlineType.Single;

//Sets the font weight

font.Bold = true;

//Adds textpart to the paragraph

ITextPart textPartFormatting2 = paragraph2.AddTextPart();

//Adds text to the textpart

textPartFormatting2.Text = "The standard chunk of Lorem Ipsum used since the 1500s is reproduced below for those interested.";

//Retrieves the existing font for modification

IFont font2 = textPartFormatting2.Font;

//Sets the font color

font2.Color.SystemColor = Color.Blue;

//Sets the underline type

font2.Underline = TextUnderlineType.WavyDouble;

//Saves the presentation

presentation.Save("Output.pptx");

//Closes the presentation

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Loads the PowerPoint presentation

Dim presentationDocument As IPresentation = Presentation.Create()

'Gets the slide from presentation

Dim slide As ISlide = presentationDocument.Slides.Add(SlideLayoutType.Blank)

'Adds textbox to the slide

Dim textboxShape2 As IShape = slide.AddTextBox(500, 0, 400, 500)

'Adds paragraph to the textbody of textbox

Dim paragraph2 As IParagraph = textboxShape2.TextBody.AddParagraph()

'Adds textpart to the paragraph

Dim textPartFormatting As ITextPart = paragraph2.AddTextPart()

'Adds text to the textpart

textPartFormatting.Text = "The standard chunk of Lorem Ipsum used since the 1500s is reproduced below for those interested. Sections 1.10.32 and 1.10.33 from 'de Finibus Bonorum et Malorum' by Cicero are also reproduced in their exact original form, accompanied by English versions from the 1914 translation by H. Rackham."

'Sets the underline color

textPartFormatting.UnderlineColor.SystemColor = Color.Black

'Retrieves the existing font for modification

Dim font As IFont = textPartFormatting.Font

'Sets the underline type

font.Underline = TextUnderlineType.[Single]

'Sets the font weight

font.Bold = True

'Adds textpart to the paragraph

Dim textPartFormatting2 As ITextPart = paragraph2.AddTextPart()

'Adds text to the textpart

textPartFormatting2.Text = "The standard chunk of Lorem Ipsum used since the 1500s is reproduced below for those interested."

'Retrieves the existing font for modification

Dim font2 As IFont = textPartFormatting2.Font

'Sets the font color

font2.Color.SystemColor = Color.Blue

'Sets the underline type

font2.Underline = TextUnderlineType.WavyDouble

'Saves the presentation

presentationDocument.Save("Output.pptx")

'Closes the presentation

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

## Modifying text

You can modify a text by accessing the existing paragraphs in a presentation. The following code example demonstrates how to modify the content in a paragraph.

{% tabs %}

{% highlight c# %}

//Opens an existing presentation from file system.

IPresentation presentation = Presentation.Open("Sample.pptx");

//Retrieves the first slide from presentation

ISlide slide = presentation.Slides[0];

//Retrieves the first shape.

IShape shape = slide.Shapes[0] as IShape;

//Retrieves the first paragraph of the shape.

IParagraph paragraph = shape.TextBody.Paragraphs[0];

//Retrieves the first text part of the shape.

ITextPart textPart = paragraph.TextParts[0];

//Modifies the text content of the textpart.

textPart.Text = "Hello Presentation";

//Saves the presenation to the file system.

presentation.Save("Result.pptx");

//Closes the presentation.

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing presentation from file system.

Dim presentationDocument As IPresentation = Presentation.Open("Sample.pptx")

'Retrieves the first slide from presentation

Dim slide As ISlide = presentationDocument.Slides(0)

'Retrieves the first shape.

Dim shape As IShape = TryCast(slide.Shapes(0), IShape)

'Retrieves the first paragraph of the shape.

Dim paragraph As IParagraph = shape.TextBody.Paragraphs(0)

'Retrieves the first text part of the shape.

Dim textPart As ITextPart = paragraph.TextParts(0)

'Modifies the text content of the textpart.

textPart.Text = "Hello Presentation"

'Saves the presenation to the file system.

presentationDocument.Save("Result.pptx")

'Closes the presentation.

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

## Removing the paragraph 

The following code example demonstrates how to remove a paragraph from a slide.

{% tabs %}

{% highlight c# %}

//Opens an existing presentation from file system.

IPresentation presentation = Presentation.Open("Sample.pptx");

//Retrieves the first slide from presentation

ISlide slide = presentation.Slides[0];

//Retrieves the first shape.

IShape shape = slide.Shapes[0] as IShape;

//Retrieves the first paragraph of the shape.

IParagraph paragraph = shape.TextBody.Paragraphs[0];

//Removes the first paragraph from the textbody of the shape.

shape.TextBody.Paragraphs.Remove(paragraph);

//Saves the presenation to the file system.

presentation.Save("Result.pptx");

//Closes the presentation.

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing presentation from file system.

Dim presentationDocument As IPresentation = Presentation.Open("Sample.pptx")

'Retrieves the first slide from presentation

Dim slide As ISlide = presentationDocument.Slides(0)

'Retrieves the first shape.

Dim shape As IShape = TryCast(slide.Shapes(0), IShape)

'Retrieves the first paragraph of the shape.

Dim paragraph As IParagraph = shape.TextBody.Paragraphs(0)

'Removes the first paragraph from the textbody of the shape.

shape.TextBody.Paragraphs.Remove(paragraph)

'Saves the presenation to the file system.

presentationDocument.Save("Result.pptx")

'Closes the presentation.

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}
