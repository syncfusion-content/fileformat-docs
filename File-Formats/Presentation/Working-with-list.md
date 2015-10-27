---
title: Working with lists in PowerPoint Presentation
description: Working with lists in PowerPoint Presentation
platform: file-formats
control: Presentation
documentation: UG
---
# Working with lists

## Creating a simple list

Essential Presentation allows you to create simple and multi-level lists that make the content easier for reading. In PowerPoint, presentation lists consists of the following types 

1. Numbered list
2. Bulleted list
3. Picture list 

### Numbered List

The following code example illustrates how to create a numbered list:

{% tabs %}

{% highlight c# %}

//Creates a new presentation instance.

IPresentation presentation = Presentation.Create();

//Adds a blank slide into the presentation

ISlide slide = presentation.Slides.Add(SlideLayoutType.Blank);

// Adds a textbox to hold the list

IShape textBoxShape = slide.AddTextBox(65, 140, 410, 270);

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

//Saves the presentation to the file system.

presentation.Save("Sample.pptx");

Process.Start("Sample.pptx");

//Closes the presentation

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates a new presentation instance.

Dim presentationDocument As IPresentation = Presentation.Create()

'Adds the slide into the presentation

Dim slide As ISlide = presentationDocument.Slides.Add(SlideLayoutType.Blank)

'Adds a textbox to hold the list

Dim textBoxShape As IShape = slide.AddTextBox(65, 140, 410, 270)

'Adds a new paragraph with the text in the left hand side textbox.

Dim paragraph As IParagraph = textBoxShape.TextBody.AddParagraph("Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.")

'Sets the list type as Numbered

paragraph.ListFormat.Type = ListType.Numbered

'Sets the numbered style (list numbering) as Arabic number following by period.

paragraph.ListFormat.NumberStyle = NumberedListStyle.ArabicPeriod

'Sets the starting value as 1

paragraph.ListFormat.StartValue = 1

'Sets the list level as 1

paragraph.IndentLevelNumber = 1

' Sets the hanging value

paragraph.FirstLineIndent = -20

' Sets the bullet character size. Here, 100 means 100% of its text. Possible values can range from 25 to 400.

paragraph.ListFormat.Size = 100

' Adds another paragraph with the text in the left hand side textbox.

paragraph = textBoxShape.TextBody.AddParagraph("Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.")

'Sets the list type as bulleted

paragraph.ListFormat.Type = ListType.Numbered

'Sets the numbered style (list numbering) as Arabic number following by period.

paragraph.ListFormat.NumberStyle = NumberedListStyle.ArabicPeriod

'Sets the list level as 1

paragraph.IndentLevelNumber = 1

' Sets the hanging value

paragraph.FirstLineIndent = -20

' Sets the bullet character size. Here, 100 means 100% of its text. Possible values can range from 25 to 400.

paragraph.ListFormat.Size = 100

' Adds another paragraph with the text in the left hand side textbox.

paragraph = textBoxShape.TextBody.AddParagraph("Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.")

'Sets the list type as bulleted

paragraph.ListFormat.Type = ListType.Numbered

'Sets the numbered style (list numbering) as Arabic number following by period.

paragraph.ListFormat.NumberStyle = NumberedListStyle.ArabicPeriod

'Sets the list level as 1

paragraph.IndentLevelNumber = 1

' Sets the hanging value

paragraph.FirstLineIndent = -20

' Sets the bullet character size. Here, 100 means 100% of its text. Possible values can range from 25 to 400.

paragraph.ListFormat.Size = 100

'Saves the presentation to the file system.

presentationDocument.Save("Sample.pptx")

Process.Start("Sample.pptx")

'Closes the presentation

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

### Bulleted list

The following code example demonstrates how to create a simple bulleted list.

{% tabs %}

{% highlight c# %}

//Creates a new presentation instance.

IPresentation presentation = Presentation.Create();

//Adds the slide into the presentation

ISlide slide = presentation.Slides.Add(SlideLayoutType.Blank);

// Adds a textbox to hold the list

IShape textBoxShape = slide.AddTextBox(65, 140, 410, 250);

// Adds a new paragraph with the text in the left hand side textbox.

IParagraph paragraph = textBoxShape.TextBody.AddParagraph("Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.");

//Sets the list type as bulleted

paragraph.ListFormat.Type = ListType.Bulleted;

//Sets the bullet character for this list

paragraph.ListFormat.BulletCharacter = Convert.ToChar(183);

//Sets the hanging value

paragraph.FirstLineIndent = -20;

//Sets the list level as 1

paragraph.IndentLevelNumber = 1;

// Sets the font for the bullet character

paragraph.ListFormat.FontName = "Symbol";

// Sets the bullet character size. Here, 100 means 100% of its text. Possible values can range from 25 to 400.

paragraph.ListFormat.Size = 100;

// Adds another paragraph with the text in the left hand side textbox.

paragraph = textBoxShape.TextBody.AddParagraph("Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.");

//Sets the list type as bulleted

paragraph.ListFormat.Type = ListType.Bulleted;

//Sets the bullet character for this list

paragraph.ListFormat.BulletCharacter = Convert.ToChar(183);

//Sets the hanging value

paragraph.FirstLineIndent = -20;

//Sets the list level as 1

paragraph.IndentLevelNumber = 1;

// Sets the font for the bullet character

paragraph.ListFormat.FontName = "Symbol";

// Sets the bullet character size. Here, 100 means 100% of its text. Possible values can range from 25 to 400.

paragraph.ListFormat.Size = 100;            

// Adds another paragraph with the text in the left hand side textbox.

paragraph = textBoxShape.TextBody.AddParagraph("Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.");

//Sets the list type as bulleted

paragraph.ListFormat.Type = ListType.Bulleted;

//Sets the bullet character for this list

paragraph.ListFormat.BulletCharacter = Convert.ToChar(183);

//Sets the hanging value

paragraph.FirstLineIndent = -20;

//Sets the list level as 1

paragraph.IndentLevelNumber = 1;           

// Sets the font of the bullet character

paragraph.ListFormat.FontName = "Symbol";

// Sets the bullet character size. Here, 100 means 100% of its text. Possible values can range from 25 to 400.

paragraph.ListFormat.Size = 100;                    

//Saves the presentation to the file system.

presentation.Save("Result.pptx");

Process.Start("Result.pptx");

//Closes the presentation

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates a new presentation instance.

Dim presentationDocument As IPresentation = Presentation.Create()

'Adds the slide into the presentation

Dim slide As ISlide = presentationDocument.Slides.Add(SlideLayoutType.Blank)

' Adds a textbox to hold the list

Dim textBoxShape As IShape = slide.AddTextBox(65, 140, 410, 250)

' Adds a new paragraph with the text in the left hand side textbox.

Dim paragraph As IParagraph = textBoxShape.TextBody.AddParagraph("Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.")

'Sets the list type as bulleted

paragraph.ListFormat.Type = ListType.Bulleted

'Sets the bullet character for this list

paragraph.ListFormat.BulletCharacter = Convert.ToChar(183)

'Sets the hanging value

paragraph.FirstLineIndent = -20

'Sets the list level as 1

paragraph.IndentLevelNumber = 1

' Sets the font for the bullet character

paragraph.ListFormat.FontName = "Symbol"

' Sets the bullet character size. Here, 100 means 100% of its text. Possible values can range from 25 to 400.

paragraph.ListFormat.Size = 100

' Adds another paragraph with the text in the left hand side textbox.

paragraph = textBoxShape.TextBody.AddParagraph("Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.")

'Sets the list type as bulleted

paragraph.ListFormat.Type = ListType.Bulleted

'Sets the bullet character for this list

paragraph.ListFormat.BulletCharacter = Convert.ToChar(183)

'Sets the hanging value

paragraph.FirstLineIndent = -20

'Sets the list level as 1

paragraph.IndentLevelNumber = 1

' Sets the font for the bullet character

paragraph.ListFormat.FontName = "Symbol"

' Sets the bullet character size. Here, 100 means 100% of its text. Possible values can range from 25 to 400.

paragraph.ListFormat.Size = 100

' Adds another paragraph with the text in the left hand side textbox.

paragraph = textBoxShape.TextBody.AddParagraph("Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.")

'Sets the list type as bulleted

paragraph.ListFormat.Type = ListType.Bulleted

'Sets the bullet character for this list

paragraph.ListFormat.BulletCharacter = Convert.ToChar(183)

'Sets the hanging value

paragraph.FirstLineIndent = -20

'Sets the list level as 1

paragraph.IndentLevelNumber = 1

' Sets the font of the bullet character

paragraph.ListFormat.FontName = "Symbol"

' Sets the bullet character size. Here, 100 means 100% of its text. Possible values can range from 25 to 400.

paragraph.ListFormat.Size = 100

'Saves the presentation to the file system.

presentationDocument.Save("Result.pptx")

Process.Start("Result.pptx")

'Closes the presentation

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

### Picture List

The following code example demonstrates how to create a simple picture list.

{% tabs %}

{% highlight c# %}

//Creates a new presentation instance.

IPresentation presentation = Presentation.Create();

//Adds the slide into the presentation

ISlide slide = presentation.Slides.Add(SlideLayoutType.Blank);

// Adds a textbox to hold the list

IShape textBoxShape = slide.AddTextBox(65, 140, 410, 270);

// Adds a new paragraph with the text in the left hand side textbox.

IParagraph paragraph = textBoxShape.TextBody.AddParagraph("Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.");

//Sets the list type as Numbered

paragraph.ListFormat.Type = ListType.Picture;

//Sets the image for the list.

paragraph.ListFormat.Picture(new MemoryStream(Syncfusion.Drawing.Image.FromFile("Image.png").ImageData));

// Sets the picture size. Here, 100 means 100% of its text. Possible values can range from 25 to 400.

paragraph.ListFormat.Size = 150;

//Sets the list level as 1

paragraph.IndentLevelNumber = 1;

// Sets the hanging value

paragraph.FirstLineIndent = -20;

// Adds another paragraph with the text in the left hand side textbox.

paragraph = textBoxShape.TextBody.AddParagraph("Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.");

//Sets the list type as picture

paragraph.ListFormat.Type = ListType.Picture;

//Sets the image for the list.

paragraph.ListFormat.Picture(new MemoryStream(Syncfusion.Drawing.Image.FromFile("Image.png").ImageData));

// Sets the picture size. Here, 100 means 100% of its text. Possible values can range from 25 to 400.

paragraph.ListFormat.Size = 150;

//Sets the list level as 1

paragraph.IndentLevelNumber = 1;

// Sets the hanging value

paragraph.FirstLineIndent = -20;

//Saves the presentation to the file system.

presentation.Save("output.pptx");

//Closes the presentation

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates a new presentation instance.

Dim presentationDocument As IPresentation = Presentation.Create()

'Adds the slide into the presentation

Dim slide As ISlide = presentationDocument.Slides.Add(SlideLayoutType.Blank)

' Adds a textbox to hold the list

Dim textBoxShape As IShape = slide.AddTextBox(65, 140, 410, 270)

' Adds a new paragraph with the text in the left hand side textbox.

Dim paragraph As IParagraph = textBoxShape.TextBody.AddParagraph("Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.")

'Sets the list type as Numbered

paragraph.ListFormat.Type = ListType.Picture

'Sets the image for the list.

paragraph.ListFormat.Picture(New MemoryStream (Syncfusion.Drawing. Image.FromFile("Image.png").ImageData))

' Sets the picture size. Here, 100 means 100% of its text. Possible values can range from 25 to 400.

paragraph.ListFormat.Size = 150

'Sets the list level as 1

paragraph.IndentLevelNumber = 1

' Sets the hanging value

paragraph.FirstLineIndent = -20

' Adds another paragraph with the text in the left hand side textbox.

paragraph = textBoxShape.TextBody.AddParagraph("Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.")

'Sets the list type as picture

paragraph.ListFormat.Type = ListType.Picture

'Sets the image for the list.

paragraph.ListFormat.Picture(New MemoryStream (Syncfusion.Drawing. Image.FromFile("Image.png").ImageData))

' Sets the picture size. Here, 100 means 100% of its text. Possible values can range from 25 to 400.

paragraph.ListFormat.Size = 150

'Sets the list level as 1

paragraph.IndentLevelNumber = 1

' Sets the hanging value

paragraph.FirstLineIndent = -20

'Saves the presentation to the file system.

presentationDocument.Save("output.pptx")

'Closes the presentation

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

## Create a Multilevel List

You can create a multi-level list by setting the indentation levels. By default, the level begins at 0 and increments by 1 for each level. A list can be incremented or decremented from levels 0 to 8 as like MS PowerPoint. 

The following code example demonstrates how to create a multilevel list.

{% tabs %}

{% highlight c# %}

//Creates a new presentation instance.

IPresentation presentation = Presentation.Create();

//Adds the slide into the presentation

ISlide slide = presentation.Slides.Add(SlideLayoutType.Blank);

//Adds a textbox to hold the bulleted list

IShape textBoxShape = slide.AddTextBox(65, 140, 410, 250);

//Adds paragraph to the textbox

IParagraph paragraph = textBoxShape.TextBody.AddParagraph("Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.");

//Sets the list type as Numbered list

paragraph.ListFormat.Type = ListType.Numbered;

//Sets the numbered style (list numbering) as Arabic number following by period.

paragraph.ListFormat.NumberStyle = NumberedListStyle.ArabicPeriod;

//Sets the starting value as 1

paragraph.ListFormat.StartValue = 1;

//Sets the list level as 1

paragraph.IndentLevelNumber = 1;

// Sets the hanging value

paragraph.FirstLineIndent = -20;         

//Adds paragraph to the textbox

paragraph = textBoxShape.TextBody.AddParagraph("Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.");

//Sets the list type as Numbered list

paragraph.ListFormat.Type = ListType.Numbered;

//Sets the numbered style (list numbering) as lower case alphabet following by period.

paragraph.ListFormat.NumberStyle = NumberedListStyle.AlphaLcPeriod;

//Sets the list level as 2

paragraph.IndentLevelNumber = 2;

// Sets the hanging value

paragraph.FirstLineIndent = -20;         

//Add paragraph to the textbox

paragraph = textBoxShape.TextBody.AddParagraph("Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.");

//Sets the list type as Numbered list

paragraph.ListFormat.Type = ListType.Numbered;

//Sets the numbered style (list numbering) as roman number lower casing following by period.

paragraph.ListFormat.NumberStyle = NumberedListStyle.RomanLcPeriod;

//Sets the list level as 3

paragraph.IndentLevelNumber = 3;

// Sets the hanging value

paragraph.FirstLineIndent = -20;         

//Adds paragraph to the textbox

paragraph = textBoxShape.TextBody.AddParagraph("Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.");

//Sets the list type as Numbered list

paragraph.ListFormat.Type = ListType.Numbered;

paragraph.ListFormat.NumberStyle = NumberedListStyle.ArabicPeriod;

//Sets the list level as 1

paragraph.IndentLevelNumber = 1;

// Sets the hanging value

paragraph.FirstLineIndent = -20;         

//Saves the presentation to the file system.

presentation.Save("MultiLevelList.pptx");

//Closes the presentation

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates a new presentation instance.

Dim presentationDocument As IPresentation = Presentation.Create()

'Adds the slide into the presentation

Dim slide As ISlide = presentationDocument.Slides.Add(SlideLayoutType.Blank)

'Adds a textbox to hold the bulleted list

Dim textBoxShape As IShape = slide.AddTextBox(65, 140, 410, 250)

'Adds paragraph to the textbox

Dim paragraph As IParagraph = textBoxShape.TextBody.AddParagraph("Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.")

'Sets the list type as Numbered list

paragraph.ListFormat.Type = ListType.Numbered

'Sets the numbered style (list numbering) as Arabic number following by period.

paragraph.ListFormat.NumberStyle = NumberedListStyle.ArabicPeriod

'Sets the starting value as 1

paragraph.ListFormat.StartValue = 1

'Sets the list level as 1

paragraph.IndentLevelNumber = 1

' Sets the hanging value

paragraph.FirstLineIndent = -20

'Adds paragraph to the textbox

paragraph = textBoxShape.TextBody.AddParagraph("Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.")

'Sets the list type as Numbered list

paragraph.ListFormat.Type = ListType.Numbered

'Sets the numbered style (list numbering) as lower case alphabet following by period.

paragraph.ListFormat.NumberStyle = NumberedListStyle.AlphaLcPeriod

'Sets the list level as 2

paragraph.IndentLevelNumber = 2

' Sets the hanging value

paragraph.FirstLineIndent = -20

'Adds paragraph to the textbox

paragraph = textBoxShape.TextBody.AddParagraph("Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.")

'Sets the list type as Numbered list

paragraph.ListFormat.Type = ListType.Numbered

'Sets the numbered style (list numbering) as roman number lower casing following by period.

paragraph.ListFormat.NumberStyle = NumberedListStyle.RomanLcPeriod

'Sets the list level as 3

paragraph.IndentLevelNumber = 3

' Sets the hanging value

paragraph.FirstLineIndent = -20

'Adds paragraph to the textbox

paragraph = textBoxShape.TextBody.AddParagraph("Excepteur sint occaecat upidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.")

'Sets the list type as Numbered list

paragraph.ListFormat.Type = ListType.Numbered

paragraph.ListFormat.NumberStyle = NumberedListStyle.ArabicPeriod

'Sets the list level as 1

paragraph.IndentLevelNumber = 1

' Sets the hanging value

paragraph.FirstLineIndent = -20

'Saves the presentation to the file system.

presentationDocument.Save("MultiLevelList.pptx")

'Closes the presentation

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}

The above code example generates a multi-level list in presentation as follows.

![](Workingwithlist_images/Workingwithlist_img1.jpeg)

