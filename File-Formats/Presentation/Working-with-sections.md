---
title: Working with sections in PowerPoint Presentation
description: Working with sections in PowerPoint Presentation
platform: file-formats
control: Presentation
documentation: UG
keywords: sections in PowerPoint presentation
---
# Working with Sections

Sections helps to manage the slides of a PowerPoint presentation. If a presentation has many slides, you can organize the slides using sections to make the navigation easier.

## Creating a section 

### Adding a new slide to a section

The following code example demonstrates how to add a blank slide to a section.

{% tabs %}

{% highlight c# %}

//Creates a PowerPoint presentation

IPresentation presentation = Presentation.Create();

//Adds a section to the PowerPoint presentation

ISection section = presentation.Sections.Add();

//Sets a name to the created section

section.Name = "SectionDemo";

//Adds a slide to the created section

ISlide slide = section.AddSlide(SlideLayoutType.Blank);

//Adds a text box to the slide

slide.AddTextBox(10, 10, 100, 100).TextBody.AddParagraph("Slide in SectionDemo");

//Saves the PowerPoint presentation

presentation.Save("Section.pptx");

{% endhighlight %}

{% highlight vb.net %}

'Creates a PowerPoint presentation

Dim presentationDocument As IPresentation = Presentation.Create()

'Adds a section to the PowerPoint presentation

Dim section As ISection = presentationDocument.Sections.Add()

'Sets a name to the created section

section.Name = "SectionDemo"

'Adds a slide to the created section

Dim slide As ISlide = section.AddSlide(SlideLayoutType.Blank)

'Adds a text box to the slide

slide.AddTextBox(10, 10, 100, 100).TextBody.AddParagraph("Slide in SectionDemo")

'Saves the PowerPoint presentation

presentationDocument.Save("Section.PPTX")

{% endhighlight %}

{% endtabs %}

### Adding an existing slide to a section

The following code example demonstrates how to add an existing slide to a section.

{% tabs %}

{% highlight c# %}

//Loads a PowerPoint presentation

IPresentation presentation = Presentation.Open("PPTXWithoutSection.PPTX");

//Creates a new section in the PowerPoint presentation

presentation.Sections.Add();

//Moves the first slide to the created section

presentation.Slides[0].MoveToSection(0);

//Saves the PowerPoint presentation

presentation.Save("Sections.PPTX");

{% endhighlight %}

{% highlight vb.net %}

'Loads a PowerPoint presentation

Dim presentationDocument As IPresentation = Presentation.Open("PPTXWithoutSection.PPTX")

'Creates a new section in the PowerPoint presentation

presentationDocument.Sections.Add()

'Moves the first slide to the created section

presentationDocument.Slides(0).MoveToSection(0)

'Saves the PowerPoint presentation

presentationDocument.Save("Sections.PPTX")

{% endhighlight %}

{% endtabs %}

### Inserting a section

The following code example demonstrates how to insert a section in a template PowerPoint presentation that contains sections

{% tabs %}

{% highlight c# %}

//Loads a PowerPoint presentation

IPresentation presentation = Presentation.Open("PPTXWithSections.PPTX");

//Creates a new section

ISection section = presentation.Sections.Add();

//Names the created section

section.Name = "InsertedSection";

//Inserts the section at second position.

presentation.Sections.Insert(1, section);

//Saves the PowerPoint presentation

presentation.Save("Sections.PPTX");

{% endhighlight %}

{% highlight vb.net %}

'Loads a PowerPoint presentation

Dim presentationDocument As IPresentation = Presentation.Open("PPTXWithSections.PPTX")

'Creates a new section

Dim section As ISection = presentationDocument.Sections.Add()

'Names the created section

section.Name = "InsertedSection"

'Inserts the section at second position.

presentationDocument.Sections.Insert(1, section)

'Saves the PowerPoint presentation

presentationDocument.Save("Sections.PPTX")

{% endhighlight %}

{% endtabs %}

## Moving the sections within a PowerPoint presentation

You can move the sections within a PowerPoint presentation. The following code example demonstrates how to move a section to a specific position in the navigation pane.

{% tabs %}

{% highlight c# %}

//Loads a PowerPoint presentation

IPresentation presentation = Presentation.Open("PPTXWithSections.PPTX");

//Moves the second section to third position within the PowerPoint presentation.

presentation.Sections[2].Move(3);

//Saves the PowerPoint presentation

presentation.Save("Sections.PPTX");

{% endhighlight %}

{% highlight vb.net %}

'Loads a PowerPoint presentation

Dim presentationDocument As IPresentation = Presentation.Open("PPTXWithSections.PPTX")

'Moves the second section to third position within the PowerPoint presentation.

presentationDocument.Sections(2).Move(3)

'Saves the PowerPoint presentation

presentationDocument.Save("Sections.PPTX")

{% endhighlight %}

{% endtabs %}

## Moving a slide within sections

The following code example demonstrates how to move a slide from one section to another.

{% tabs %}

{% highlight c# %}

//Loads a PowerPoint presentation

IPresentation presentation = Presentation.Open("PPTXWithSections.PPTX");

//Gets the first slide of second section in the PowerPoint presentation

ISlide slide = presentation.Sections[1].Slides[0];

//Moves the slide to first section

slide.MoveToSection(0);

//Saves the PowerPoint presentation

presentation.Save("Sections.PPTX");

{% endhighlight %}

{% highlight vb.net %}

'Loads a PowerPoint presentation

Dim presentationDocument As IPresentation = Presentation.Open("PPTXWithSections.PPTX")

'Gets the first slide of second section in the PowerPoint presentation

Dim slide As ISlide = presentationDocument.Sections(1).Slides(0)

'Moves the slide to first section

slide.MoveToSection(0)

'Saves the PowerPoint presentation

presentationDocument.Save("Sections.PPTX")

{% endhighlight %}

{% endtabs %}

## Cloning and merging the slides in a section

The following code example demonstrates how to clone the slide collection of a section and add those slides to a destination presentation.

{% tabs %}

{% highlight c# %}

//Loads a PowerPoint presentation

IPresentation presentation = Presentation.Open("PPTXWithSections.PPTX");

//Clones the slides in 3rd section

ISlides slides = presentation.Sections[2].Clone();

//Creates a destination PowerPoint presentation instance. Existing presentations can also be used here.

presentation = Presentation.Create();

//Iterates the cloned slides and adds the slides to the destination presentation

foreach (ISlide slide in slides)

presentation.Slides.Add(slide);

//Saves the PowerPoint presentation

presentation.Save("Sections.PPTX");

{% endhighlight %}

{% highlight vb.net %}

'Loads a PowerPoint presentation

Dim presentationDocument As IPresentation = Presentation.Open("PPTXWithSections.PPTX")

'Clones the slides in 3rd section

Dim slides As ISlides = presentationDocument.Sections(2).Clone()

'Creates a destination PowerPoint presentation instance. Existing presentations can also be used here.

presentationDocument = Presentation.Create()

'Iterates the cloned slides and adds the slides to the destination presentation

For Each slide As ISlide In slides

presentationDocument.Slides.Add(slide)

Next

'Save the PowerPoint presentation

presentationDocument.Save("Sections.PPTX")

{% endhighlight %}

{% endtabs %}

## Removing a section 

The following code example demonstrates how to create remove a particular section from the sections collection of a presentation.

{% tabs %}

{% highlight c# %}

//Loads a PowerPoint presentation

IPresentation presentation = Presentation.Open("PPTXWithSections.PPTX");

//Removes the second section from the PowerPoint presentation

presentation.Sections.Remove(presentation.Sections[1]);

//Saves the PowerPoint presentation

presentation.Save("Sections.PPTX");

{% endhighlight %}

{% highlight vb.net %}

'Loads a PowerPoint presentation

Dim presentationDocument As IPresentation = Presentation.Open("PPTXWithSections.PPTX")

'Removes the second section from the PowerPoint presentation

presentationDocument.Sections.Remove(presentationDocument.Sections(1))

'Saves the PowerPoint presentation

presentationDocument.Save("Sections.PPTX")

{% endhighlight %}

{% endtabs %}

## Remove all sections 

The following code example demonstrates how to remove section collection from an existing PowerPoint presentation.

{% tabs %}

{% highlight c# %}

//Loads a PowerPoint presentation

IPresentation presentation = Presentation.Open("PPTXWithSections.PPTX");

//Removes the sections

presentation.Sections.Clear();

//Saves the PowerPoint presentation

presentation.Save("Sections.PPTX");

{% endhighlight %}

{% highlight vb.net %}

'Loads a PowerPoint presentation

Dim presentationDocument As IPresentation = Presentation.Open("PPTXWithSections.PPTX")

'Removes the sections

presentationDocument.Sections.Clear()

'Saves the PowerPoint presentation

presentationDocument.Save("Sections.PPTX")

{% endhighlight %}

{% endtabs %}