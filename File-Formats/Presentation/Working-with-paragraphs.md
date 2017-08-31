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

//Creates PowerPoint Presentation

IPresentation presentation = Presentation.Create();

//Adds slide to the PowerPoint

ISlide slide = presentation.Slides.Add(SlideLayoutType.Blank);

//Adds textbox to the slide

IShape textboxShape = slide.AddTextBox(0, 0, 500, 500);

//Adds paragraph to the textbody of textbox

IParagraph paragraph = textboxShape.TextBody.AddParagraph();

//Adds a TextPart to the paragraph

ITextPart textPart = paragraph.AddTextPart();

//Adds text to the TextPart

textPart.Text = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company. The company manufactures and sells metal and composite bicycles to North American, European and Asian commercial markets. While its base operation is located in Washington with 290 employees, several regional sales teams are located throughout their market base.";

//Saves the Presentation

presentation.Save("Output.pptx");

//Closes the Presentation

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates PowerPoint Presentation

Dim presentationDocument As IPresentation = Presentation.Create()

'Adds slide to the PowerPoint

Dim slide As ISlide = presentationDocument.Slides.Add(SlideLayoutType.Blank)

'Adds textbox to the slide

Dim textboxShape As IShape = slide.AddTextBox(0, 0, 500, 500)

'Adds paragraph to the textbody of textbox

Dim paragraph As IParagraph = textboxShape.TextBody.AddParagraph()

'Adds a TextPart to the paragraph

Dim textPart As ITextPart = paragraph.AddTextPart()

'Adds text to the TextPart

textPart.Text = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company. The company manufactures and sells metal and composite bicycles to North American, European and Asian commercial markets. While its base operation is located in Washington with 290 employees, several regional sales teams are located throughout their market base."

'Saves the Presentation

presentationDocument.Save("Output.pptx")

'Closes the Presentation

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

## Applying Paragraph formatting

Each paragraph in a slide can has its own formatting types such as alignment, indent etc. The following code example demonstrates how to format a paragraph in PowerPoint presentation.

{% tabs %}

{% highlight c# %}

//Loads the PowerPoint Presentation

IPresentation presentation = Presentation.Open("Sample.pptx");

//Gets the slide from Presentation

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

//Saves the Presentation

presentation.Save("Output.pptx");

//Closes the Presentation

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Loads the PowerPoint Presentation

Dim presentationDocument As IPresentation = Presentation.Open("Sample.pptx")

'Gets the slide from Presentation

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

'Saves the Presentation

presentationDocument.Save("Output.pptx")

'Closes the Presentation

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

## Working with text

With Essential Presentation, you can add or modify the text in a Presentation. Within the paragraph, textual contents are grouped into one or more child elements as TextParts. Each TextPart represents a region of text with a common set of formatted text. The following code example demonstrates how to add text with different formatting into a single paragraph.

{% tabs %}

{% highlight c# %}

//Loads the PowerPoint Presentation

IPresentation presentation = Presentation.Create();

//Gets the slide from Presentation

ISlide slide = presentation.Slides.Add(SlideLayoutType.Blank);

//Adds textbox to the slide

IShape textboxShape2 = slide.AddTextBox(500, 0, 400, 500);

//Adds paragraph to the textbody of textbox

IParagraph paragraph2 = textboxShape2.TextBody.AddParagraph();

//Adds a TextPart to the paragraph

ITextPart textPartFormatting = paragraph2.AddTextPart();

//Adds text to the TextPart

textPartFormatting.Text = "In 2000, AdventureWorks Cycles bought a small manufacturing plant, located in Mexico. The plant manufactures several critical subcomponents for the AdventureWorks Cycles product line. These subcomponents are shipped to the another location for final product assembly. In 2001, the plant, became the sole manufacturer and distributor of the touring bicycle product group.";

//Sets the underline color

textPartFormatting.UnderlineColor.SystemColor = Color.Black;

//Retrieves the existing font for modification

IFont font = textPartFormatting.Font;

//Sets the underline type

font.Underline = TextUnderlineType.Single;

//Sets the font weight

font.Bold = true;

//Adds a TextPart to the paragraph

ITextPart textPartFormatting2 = paragraph2.AddTextPart();

//Adds text to the TextPart

textPartFormatting2.Text = "In 2000, AdventureWorks Cycles bought a small manufacturing plant, located in Mexico.";

//Retrieves the existing font for modification

IFont font2 = textPartFormatting2.Font;

//Sets the font color

font2.Color.SystemColor = Color.Blue;

//Sets the underline type

font2.Underline = TextUnderlineType.WavyDouble;

//Saves the Presentation

presentation.Save("Output.pptx");

//Closes the Presentation

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Loads the PowerPoint Presentation

Dim presentationDocument As IPresentation = Presentation.Create()

'Gets the slide from Presentation

Dim slide As ISlide = presentationDocument.Slides.Add(SlideLayoutType.Blank)

'Adds textbox to the slide

Dim textboxShape2 As IShape = slide.AddTextBox(500, 0, 400, 500)

'Adds paragraph to the textbody of textbox

Dim paragraph2 As IParagraph = textboxShape2.TextBody.AddParagraph()

'Adds a TextPart to the paragraph

Dim textPartFormatting As ITextPart = paragraph2.AddTextPart()

'Adds text to the TextPart

textPartFormatting.Text = "In 2000, AdventureWorks Cycles bought a small manufacturing plant, located in Mexico. It manufactures several critical subcomponents for the AdventureWorks Cycles product line. These subcomponents are shipped to the another location for final product assembly. In 2001, the plant, became the sole manufacturer and distributor of the touring bicycle product group."

'Sets the underline color

textPartFormatting.UnderlineColor.SystemColor = Color.Black

'Retrieves the existing font for modification

Dim font As IFont = textPartFormatting.Font

'Sets the underline type

font.Underline = TextUnderlineType.[Single]

'Sets the font weight

font.Bold = True

'Adds a TextPart to the paragraph

Dim textPartFormatting2 As ITextPart = paragraph2.AddTextPart()

'Adds text to the TextPart

textPartFormatting2.Text = "In 2000, AdventureWorks Cycles bought a small manufacturing plant, located in Mexico."

'Retrieves the existing font for modification

Dim font2 As IFont = textPartFormatting2.Font

'Sets the font color

font2.Color.SystemColor = Color.Blue

'Sets the underline type

font2.Underline = TextUnderlineType.WavyDouble

'Saves the Presentation

presentationDocument.Save("Output.pptx")

'Closes the Presentation

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

## Modifying text

You can modify a text by accessing the existing paragraphs in a Presentation. The following code example demonstrates how to modify the content in a paragraph.

{% tabs %}

{% highlight c# %}

//Opens an existing Presentation from file system.

IPresentation presentation = Presentation.Open("Sample.pptx");

//Retrieves the first slide from Presentation

ISlide slide = presentation.Slides[0];

//Retrieves the first shape.

IShape shape = slide.Shapes[0] as IShape;

//Retrieves the first paragraph of the shape.

IParagraph paragraph = shape.TextBody.Paragraphs[0];

//Retrieves the first TextPart of the shape.

ITextPart textPart = paragraph.TextParts[0];

//Modifies the text content of the TextPart.

textPart.Text = "Hello Presentation";

//Saves the presentation to the file system.

presentation.Save("Result.pptx");

//Closes the Presentation.

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing Presentation from file system.

Dim presentationDocument As IPresentation = Presentation.Open("Sample.pptx")

'Retrieves the first slide from Presentation

Dim slide As ISlide = presentationDocument.Slides(0)

'Retrieves the first shape.

Dim shape As IShape = TryCast(slide.Shapes(0), IShape)

'Retrieves the first paragraph of the shape.

Dim paragraph As IParagraph = shape.TextBody.Paragraphs(0)

'Retrieves the first TextPart of the shape.

Dim textPart As ITextPart = paragraph.TextParts(0)

'Modifies the text content of the TextPart.

textPart.Text = "Hello Presentation"

'Saves the presentation to the file system.

presentationDocument.Save("Result.pptx")

'Closes the Presentation.

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

## Removing the paragraph 

The following code example demonstrates how to remove a paragraph from a slide.

{% tabs %}

{% highlight c# %}

//Opens an existing Presentation from file system.

IPresentation presentation = Presentation.Open("Sample.pptx");

//Retrieves the first slide from Presentation

ISlide slide = presentation.Slides[0];

//Retrieves the first shape

IShape shape = slide.Shapes[0] as IShape;

//Retrieves the first paragraph of the shape

IParagraph paragraph = shape.TextBody.Paragraphs[0];

//Removes the first paragraph from the textbody of the shape

shape.TextBody.Paragraphs.Remove(paragraph);

//Saves the presentation to the file system

presentation.Save("Result.pptx");

//Closes the Presentation

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing Presentation from file system.

Dim presentationDocument As IPresentation = Presentation.Open("Sample.pptx")

'Retrieves the first slide from Presentation

Dim slide As ISlide = presentationDocument.Slides(0)

'Retrieves the first shape.

Dim shape As IShape = TryCast(slide.Shapes(0), IShape)

'Retrieves the first paragraph of the shape.

Dim paragraph As IParagraph = shape.TextBody.Paragraphs(0)

'Removes the first paragraph from the textbody of the shape.

shape.TextBody.Paragraphs.Remove(paragraph)

'Saves the presentation to the file system.

presentationDocument.Save("Result.pptx")

'Closes the Presentation.

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}
