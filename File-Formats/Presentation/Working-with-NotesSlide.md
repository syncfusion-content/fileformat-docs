---
title: Working with Notes
description: Working with Notes
platform: file-formats 
control: Presentation
documentation: UG
keywords: Working with Notes
---

# Working with Notes

Notes are the contents associated with each slide. Adding Notes to a slide is an optional one. It shows hint for the speaker, so it is often called as “Speaker Notes”. The Notes are only visible to the presenter when monitors are shared in “Presenter View”. This is helpful to the presenter to remember the key points. You can add and modify the notes in your slide using Essential Presentation library.

## Adding Notes to a Slide

The below code example demonstrates how to create a Notes in a PowerPoint Slide.
{% tabs %}
{% highlight c# %}
//Creates a Presentation without slides.
IPresentation presentation = Presentation.Create();

//Adds new slide with blank slide layout type.
ISlide slide = presentation.Slides.Add(SlideLayoutType.Blank);

//Adds new notes slide in the specified slide.
INotesSlide notesSlide = slide.AddNotesSlide();

//Adds text content into the Notes Slide.
notesSlide.NotesTextBody.AddParagraph("Notes content");

//Saves Presentation with specified file name with extension.
presentation.Save("PresentationWithNotesSlide.pptx");
{% endhighlight %}
{% endtabs %}

## Adding Text into the Notes 

The following code example demonstrates how to add a text in a Notes. 
{% tabs %}
{% highlight c# %}
//Creates a Presentation without slides.
IPresentation presentation = Presentation.Create();

//Adds new slide with blank slide layout type.
ISlide slide = presentation.Slides.Add(SlideLayoutType.Blank);

//Adds new notes slide in the specified slide.
INotesSlide notesSlide = slide.AddNotesSlide();

//Adds Paragraph into the text body.
IParagraph paragraph = notesTextBody.AddParagraph();

//Adds text part into the Paragraph.
ITextPart textPart = paragraph.AddTextPart();

textPart.Text = "The notes slide represents the contents and key notes of the corresponding slide. It is more useful when we use Presenter View while presenting the seminars through slideshow.";

//Sets Bold format for text content.
textPart.Font.Bold=true;

// Sets font style using font name.
textPart.Font.FontName = "Times New Roman";

// Sets text content size using FontSize property.
textPart.Font.FontSize = 20;

//Saves Presentation with specified file name with extension.
presentation.Save("PresentationWithNotesSlide.pptx");
{% endhighlight %}
{% endtabs %}

## Adding a numbered list to Notes

The following code example demonstrates how to create simple numbered list as Notes.
{% tabs %}
{% highlight c# %}
//Creates a Presentation without slides.

IPresentation presentation = Presentation.Create();

//Adds new slide with blank slide layout type.

ISlide slide = presentation.Slides.Add(SlideLayoutType.Blank);

//Adds new notes slide in the specified slide.

INotesSlide notesSlide = slide.AddNotesSlide();

// Adds a textbox to hold the list 
IShape textBoxShape = notesSlide.AddTextBox(65, 140, 410, 270); 
// Adds a new paragraph with the text in the left hand side textbox. 
IParagraph paragraph = textBoxShape.TextBody.AddParagraph("Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."); 
//Sets the list type as Numbered 
paragraph.ListFormat.Type = ListType.Numbered;
 //Sets the numbered style (list numbering) as Arabic number following by period. 
paragraph.ListFormat.NumberStyle = NumberedListStyle.ArabicPeriod; 
//Sets the starting value as 1 
paragraph.ListFormat.StartValue = 1;
//Sets the list level as 1 
paragraph.IndentLevelNumber = 1;
// Sets the hanging value 
paragraph.FirstLineIndent = -20;
// Sets the bullet character size. Here, 100 means 100% of its text. Possible values can range from 25 to 400. 
paragraph.ListFormat.Size = 100;
// Adds another paragraph with the text in the left hand side textbox. 
paragraph = textBoxShape.TextBody.AddParagraph("Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat."); 
//Sets the list type as bulleted 
paragraph.ListFormat.Type = ListType.Numbered; 
//Sets the numbered style (list numbering) as Arabic number following by period. 
paragraph.ListFormat.NumberStyle = NumberedListStyle.ArabicPeriod; 
//Sets the list level as 1 
paragraph.IndentLevelNumber = 1; 
// Sets the hanging value 
paragraph.FirstLineIndent = -20; 
// Sets the bullet character size. Here, 100 means 100% of its text. Possible values can range from 25 to 400. 
paragraph.ListFormat.Size = 100; 
// Adds another paragraph with the text in the left hand side textbox. 
paragraph = textBoxShape.TextBody.AddParagraph("Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur."); 
//Sets the list type as bulleted 
paragraph.ListFormat.Type = ListType.Numbered; 
//Sets the numbered style (list numbering) as Arabic number following by period. 
paragraph.ListFormat.NumberStyle = NumberedListStyle.ArabicPeriod; 
//Sets the list level as 1 
paragraph.IndentLevelNumber = 1; 
// Sets the hanging value 
paragraph.FirstLineIndent = -20; 
// Sets the bullet character size. Here, 100 means 100% of its text. Possible values can range from 25 to 400. 
paragraph.ListFormat.Size = 100; 
//Saves the Presentation to the file system. 
presentation.Save("Sample.pptx"); 
//Closes the Presentation 
presentation.Close();
{% endhighlight %}
{% endtabs %}

## Removing Notes from a Slide

The below code example demonstrates how to remove a Notes from a PowerPoint Slide.
{% tabs %}
{% highlight c# %}
//Opens existing Presentation.
IPresentation presentation = Presentation.Open("Sample.pptx");

//Gets instance of the first slide from the Presentation.
ISlide slide = presentation.Slides[0] as ISlide;

//Removes Notes Slide from a corresponding slide.
slide.RemoveNotesSlide();

//Saves Presentation with specified file name with extension.
presentation.Save("PresentationWithNotesSlide.pptx");
{% endhighlight %}
{% endtabs %}
