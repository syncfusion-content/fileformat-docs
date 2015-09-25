---
layout: Post
title: Working with lists in PowerPoint Presentation
description: Working with lists in PowerPoint Presentation
platform: FileFormats
control: Presentation
documentation: UG
---
# Working with lists

## Creating a simple list

Essential Presentation allows you to create simple and multi-level lists which makes the content easier for reading. In PowerPoint presentation lists consists the following types 

1. Numbered list
2. Bulleted list
3. Picture list 

**Numbered** **List**

The below code snippet illustrates creating a numbered list:

{% highlight c# %}
[C#]

//Create a new presentation instance.

IPresentation presentation = Presentation.Create();

//Add a blank slide into the presentation

ISlide slide = presentation.Slides.Add(SlideLayoutType.Blank);

// Add a textbox to hold the list

IShape textBoxShape = slide.AddTextBox(65, 140, 410, 270);

// Add a new paragraph with the text in the left hand side textbox.

IParagraph paragraph = textBoxShape.TextBody.AddParagraph("Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.");

//Set the list type as Numbered

paragraph.ListFormat.Type = ListType.Numbered;

//Set the numbered style (list numbering) as Arabic number following by period.

paragraph.ListFormat.NumberStyle = NumberedListStyle.ArabicPeriod;

//Set the starting value as 1

paragraph.ListFormat.StartValue = 1;

//Set the list level as 1

paragraph.IndentLevelNumber = 1;   

// Set the hanging value

paragraph.FirstLineIndent = -20;         

// Set the bullet character size. If 100, here means 100% of its text. Possible values can range from 25 to 400

paragraph.ListFormat.Size = 100;           

// Add another paragraph with the text in the left hand side textbox.

paragraph = textBoxShape.TextBody.AddParagraph("Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.");

//Set the list type as bulleted

paragraph.ListFormat.Type = ListType.Numbered;

//Set the numbered style (list numbering) as Arabic number following by period.

paragraph.ListFormat.NumberStyle = NumberedListStyle.ArabicPeriod;

//Set the list level as 1

paragraph.IndentLevelNumber = 1;

// Set the hanging value

paragraph.FirstLineIndent = -20;                     

// Set the bullet character size. If 100, here means 100% of its text. Possible values can range from 25 to 400

paragraph.ListFormat.Size = 100;

// Add another paragraph with the text in the left hand side textbox.

paragraph = textBoxShape.TextBody.AddParagraph("Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.");

//Set the list type as bulleted

paragraph.ListFormat.Type = ListType.Numbered;

//Set the numbered style (list numbering) as Arabic number following by period.

paragraph.ListFormat.NumberStyle = NumberedListStyle.ArabicPeriod;

//Set the list level as 1

paragraph.IndentLevelNumber = 1; 

// Set the hanging value

paragraph.FirstLineIndent = -20;    

// Set the bullet character size. If 100, here means 100% of its text. Possible values can range from 25 to 400

paragraph.ListFormat.Size = 100;

//Save the presentation to the file system.

presentation.Save("Sample.pptx");

Process.Start("Sample.pptx");

//Close the presentation

presentation.Close();



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Create a new presentation instance.

Dim presentation_1 As IPresentation = Presentation.Create()

'Add the slide into the presentation

Dim slide As ISlide = presentation_1.Slides.Add(SlideLayoutType.Blank)

'Add a textbox to hold the list

Dim textBoxShape As IShape = slide.AddTextBox(65, 140, 410, 270)

'Add a new paragraph with the text in the left hand side textbox.

Dim paragraph As IParagraph = textBoxShape.TextBody.AddParagraph("Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.")

'Set the list type as Numbered

paragraph.ListFormat.Type = ListType.Numbered

'Set the numbered style (list numbering) as Arabic number following by period.

paragraph.ListFormat.NumberStyle = NumberedListStyle.ArabicPeriod

'Set the starting value as 1

paragraph.ListFormat.StartValue = 1

'Set the list level as 1

paragraph.IndentLevelNumber = 1

' Set the hanging value

paragraph.FirstLineIndent = -20

' Set the bullet character size. If 100, here means 100% of its text. Possible values can range from 25 to 400

paragraph.ListFormat.Size = 100

' Add another paragraph with the text in the left hand side textbox.

paragraph = textBoxShape.TextBody.AddParagraph("Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.")

'Set the list type as bulleted

paragraph.ListFormat.Type = ListType.Numbered

'Set the numbered style (list numbering) as Arabic number following by period.

paragraph.ListFormat.NumberStyle = NumberedListStyle.ArabicPeriod

'Set the list level as 1

paragraph.IndentLevelNumber = 1

' Set the hanging value

paragraph.FirstLineIndent = -20

' Set the bullet character size. If 100, here means 100% of its text. Possible values can range from 25 to 400

paragraph.ListFormat.Size = 100

' Add another paragraph with the text in the left hand side textbox.

paragraph = textBoxShape.TextBody.AddParagraph("Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.")

'Set the list type as bulleted

paragraph.ListFormat.Type = ListType.Numbered

'Set the numbered style (list numbering) as Arabic number following by period.

paragraph.ListFormat.NumberStyle = NumberedListStyle.ArabicPeriod

'Set the list level as 1

paragraph.IndentLevelNumber = 1

' Set the hanging value

paragraph.FirstLineIndent = -20

' Set the bullet character size. If 100, here means 100% of its text. Possible values can range from 25 to 400

paragraph.ListFormat.Size = 100

'Save the presentation to the file system.

presentation_1.Save("Sample.pptx")

Process.Start("Sample.pptx")

'Close the presentation

presentation_1.Close()



{% endhighlight %}

**Bulleted** **list**

The below code snippet demonstrates creating a simple bulleted list.

{% highlight c# %}
[C#]

//Create a new presentation instance.

IPresentation presentation = Presentation.Create();

//Add the slide into the presentation

ISlide slide = presentation.Slides.Add(SlideLayoutType.Blank);

// Add a textbox to hold the list

IShape textBoxShape = slide.AddTextBox(65, 140, 410, 250);

// Add a new paragraph with the text in the left hand side textbox.

IParagraph paragraph = textBoxShape.TextBody.AddParagraph("Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.");

//Set the list type as bulleted

paragraph.ListFormat.Type = ListType.Bulleted;

//Set the bullet character for this list

paragraph.ListFormat.BulletCharacter = Convert.ToChar(183);

//Set the hanging value

paragraph.FirstLineIndent = -20;

//Set the list level as 1

paragraph.IndentLevelNumber = 1;

// Set the font for the bullet character

paragraph.ListFormat.FontName = "Symbol";

// Set the bullet character size. If 100, here means 100% of its text. Possible values can range from 25 to 400

paragraph.ListFormat.Size = 100;



// Add another paragraph with the text in the left hand side textbox.

paragraph = textBoxShape.TextBody.AddParagraph("Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.");

//Set the list type as bulleted

paragraph.ListFormat.Type = ListType.Bulleted;

//Set the bullet character for this list

paragraph.ListFormat.BulletCharacter = Convert.ToChar(183);

//Set the hanging value

paragraph.FirstLineIndent = -20;

//Set the list level as 1

paragraph.IndentLevelNumber = 1;

// Set the font for the bullet character

paragraph.ListFormat.FontName = "Symbol";

// Set the bullet character size. If 100, here means 100% of its text. Possible values can range from 25 to 400

paragraph.ListFormat.Size = 100;            

// Add another paragraph with the text in the left hand side textbox.

paragraph = textBoxShape.TextBody.AddParagraph("Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.");

//Set the list type as bulleted

paragraph.ListFormat.Type = ListType.Bulleted;

//Set the bullet character for this list

paragraph.ListFormat.BulletCharacter = Convert.ToChar(183);

//Set the hanging value

paragraph.FirstLineIndent = -20;

//Set the list level as 1

paragraph.IndentLevelNumber = 1;           

// Set the font of the bullet character

paragraph.ListFormat.FontName = "Symbol";

// Set the bullet character size. If 100, here means 100% of its text. Possible values can range from 25 to 400

paragraph.ListFormat.Size = 100;                    

//Save the presentation to the file system.

presentation.Save("Result.pptx");

Process.Start("Result.pptx");

//Close the presentation

presentation.Close();



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Create a new presentation instance.

Dim presentation_1 As IPresentation = Presentation.Create()

'Add the slide into the presentation

Dim slide As ISlide = presentation_1.Slides.Add(SlideLayoutType.Blank)

' Add a textbox to hold the list

Dim textBoxShape As IShape = slide.AddTextBox(65, 140, 410, 250)

' Add a new paragraph with the text in the left hand side textbox.

Dim paragraph As IParagraph = textBoxShape.TextBody.AddParagraph("Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.")

'Set the list type as bulleted

paragraph.ListFormat.Type = ListType.Bulleted

'Set the bullet character for this list

paragraph.ListFormat.BulletCharacter = Convert.ToChar(183)

'Set the hanging value

paragraph.FirstLineIndent = -20

'Set the list level as 1

paragraph.IndentLevelNumber = 1

' Set the font for the bullet character

paragraph.ListFormat.FontName = "Symbol"

' Set the bullet character size. If 100, here means 100% of its text. Possible values can range from 25 to 400

paragraph.ListFormat.Size = 100

' Add another paragraph with the text in the left hand side textbox.

paragraph = textBoxShape.TextBody.AddParagraph("Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.")

'Set the list type as bulleted

paragraph.ListFormat.Type = ListType.Bulleted

'Set the bullet character for this list

paragraph.ListFormat.BulletCharacter = Convert.ToChar(183)

'Set the hanging value

paragraph.FirstLineIndent = -20

'Set the list level as 1

paragraph.IndentLevelNumber = 1

' Set the font for the bullet character

paragraph.ListFormat.FontName = "Symbol"

' Set the bullet character size. If 100, here means 100% of its text. Possible values can range from 25 to 400

paragraph.ListFormat.Size = 100

' Add another paragraph with the text in the left hand side textbox.

paragraph = textBoxShape.TextBody.AddParagraph("Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.")

'Set the list type as bulleted

paragraph.ListFormat.Type = ListType.Bulleted

'Set the bullet character for this list

paragraph.ListFormat.BulletCharacter = Convert.ToChar(183)

'Set the hanging value

paragraph.FirstLineIndent = -20

'Set the list level as 1

paragraph.IndentLevelNumber = 1

' Set the font of the bullet character

paragraph.ListFormat.FontName = "Symbol"

' Set the bullet character size. If 100, here means 100% of its text. Possible values can range from 25 to 400

paragraph.ListFormat.Size = 100

'Save the presentation to the file system.

presentation_1.Save("Result.pptx")

Process.Start("Result.pptx")

'Close the presentation

presentation_1.Close()



{% endhighlight %}

**Picture** **List**

The below code snippet demonstrates creating a simple picture list.

{% highlight c# %}
[C#]

//Create a new presentation instance.

IPresentation presentation = Presentation.Create();

//Add the slide into the presentation

ISlide slide = presentation.Slides.Add(SlideLayoutType.Blank);

// Add a textbox to hold the list

IShape textBoxShape = slide.AddTextBox(65, 140, 410, 270);

// Add a new paragraph with the text in the left hand side textbox.

IParagraph paragraph = textBoxShape.TextBody.AddParagraph("Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.");

//Set the list type as Numbered

paragraph.ListFormat.Type = ListType.Picture;

//Set the image for the list.

paragraph.ListFormat.Picture(new MemoryStream(Syncfusion.Drawing.Image.FromFile("Image.png").ImageData));

// Set the picture size. If 100, here means 100% of its text. Possible values can range from 25 to 400

paragraph.ListFormat.Size = 150;

//Set the list level as 1

paragraph.IndentLevelNumber = 1;

// Set the hanging value

paragraph.FirstLineIndent = -20;

// Add another paragraph with the text in the left hand side textbox.

paragraph = textBoxShape.TextBody.AddParagraph("Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.");

//Set the list type as picture

paragraph.ListFormat.Type = ListType.Picture;

//Set the image for the list.

paragraph.ListFormat.Picture(new MemoryStream(Syncfusion.Drawing.Image.FromFile("Image.png").ImageData));

// Set the picture size. If 100, here means 100% of its text. Possible values can range from 25 to 400

paragraph.ListFormat.Size = 150;

//Set the list level as 1

paragraph.IndentLevelNumber = 1;

// Set the hanging value

paragraph.FirstLineIndent = -20;

//Save the presentation to the file system.

presentation.Save("output.pptx");

//Close the presentation

presentation.Close();



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Create a new presentation instance.

Dim presentation_1 As IPresentation = Presentation.Create()

'Add the slide into the presentation

Dim slide As ISlide = presentation_1.Slides.Add(SlideLayoutType.Blank)

' Add a textbox to hold the list

Dim textBoxShape As IShape = slide.AddTextBox(65, 140, 410, 270)

' Add a new paragraph with the text in the left hand side textbox.

Dim paragraph As IParagraph = textBoxShape.TextBody.AddParagraph("Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.")

'Set the list type as Numbered

paragraph.ListFormat.Type = ListType.Picture

'Set the image for the list.

paragraph.ListFormat.Picture(New MemoryStream (Syncfusion.Drawing. Image.FromFile("Image.png").ImageData))

' Set the picture size. If 100, here means 100% of its text. Possible values can range from 25 to 400

paragraph.ListFormat.Size = 150

'Set the list level as 1

paragraph.IndentLevelNumber = 1

' Set the hanging value

paragraph.FirstLineIndent = -20

' Add another paragraph with the text in the left hand side textbox.

paragraph = textBoxShape.TextBody.AddParagraph("Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.")

'Set the list type as picture

paragraph.ListFormat.Type = ListType.Picture

'Set the image for the list.

paragraph.ListFormat.Picture(New MemoryStream (Syncfusion.Drawing. Image.FromFile("Image.png").ImageData))

' Set the picture size. If 100, here means 100% of its text. Possible values can range from 25 to 400

paragraph.ListFormat.Size = 150

'Set the list level as 1

paragraph.IndentLevelNumber = 1

' Set the hanging value

paragraph.FirstLineIndent = -20

'Save the presentation to the file system.

presentation_1.Save("output.pptx")

'Close the presentation

presentation_1.Close()



{% endhighlight %}

## Creating a Multilevel List

We can create a multi-level list by setting the indentation levels. By default the level begins at 0 and increments by 1 for each level. A list can be incremented or decremented from levels 0 to 8 as like MS PowerPoint. 

The below code snippet demonstrates creating a multilevel list.

{% highlight c# %}
[C#]

//Create a new presentation instance.

IPresentation presentation = Presentation.Create();

//Add the slide into the presentation

ISlide slide = presentation.Slides.Add(SlideLayoutType.Blank);

//Add a textbox to hold the bulleted list

IShape textBoxShape = slide.AddTextBox(65, 140, 410, 250);

//Add paragraph to the textbox

IParagraph paragraph = textBoxShape.TextBody.AddParagraph("Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.");

//Set the list type as Numbered list

paragraph.ListFormat.Type = ListType.Numbered;

//Set the numbered style (list numbering) as Arabic number following by period.

paragraph.ListFormat.NumberStyle = NumberedListStyle.ArabicPeriod;

//Set the starting value as 1

paragraph.ListFormat.StartValue = 1;

//Set the list level as 1

paragraph.IndentLevelNumber = 1;

// Set the hanging value

paragraph.FirstLineIndent = -20;         

//Add paragraph to the textbox

paragraph = textBoxShape.TextBody.AddParagraph("Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.");

//Set the list type as Numbered list

paragraph.ListFormat.Type = ListType.Numbered;

//Set the numbered style (list numbering) as lower case alphabet following by period.

paragraph.ListFormat.NumberStyle = NumberedListStyle.AlphaLcPeriod;

//Set the list level as 2

paragraph.IndentLevelNumber = 2;

// Set the hanging value

paragraph.FirstLineIndent = -20;         

//Add paragraph to the textbox

paragraph = textBoxShape.TextBody.AddParagraph("Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.");

//Set the list type as Numbered list

paragraph.ListFormat.Type = ListType.Numbered;

//Set the numbered style (list numbering) as roman number lower casing following by period.

paragraph.ListFormat.NumberStyle = NumberedListStyle.RomanLcPeriod;

//Set the list level as 3

paragraph.IndentLevelNumber = 3;

// Set the hanging value

paragraph.FirstLineIndent = -20;         

//Add paragraph to the textbox

paragraph = textBoxShape.TextBody.AddParagraph("Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.");

//Set the list type as Numbered list

paragraph.ListFormat.Type = ListType.Numbered;

paragraph.ListFormat.NumberStyle = NumberedListStyle.ArabicPeriod;

//Set the list level as 1

paragraph.IndentLevelNumber = 1;

// Set the hanging value

paragraph.FirstLineIndent = -20;         

//Save the presentation to the file system.

presentation.Save("MultiLevelList.pptx");

//Close the presentation

presentation.Close();



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Create a new presentation instance.

Dim presentation_1 As IPresentation = Presentation.Create()

'Add the slide into the presentation

Dim slide As ISlide = presentation_1.Slides.Add(SlideLayoutType.Blank)

'Add a textbox to hold the bulleted list

Dim textBoxShape As IShape = slide.AddTextBox(65, 140, 410, 250)

'Add paragraph to the textbox

Dim paragraph As IParagraph = textBoxShape.TextBody.AddParagraph("Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.")

'Set the list type as Numbered list

paragraph.ListFormat.Type = ListType.Numbered

'Set the numbered style (list numbering) as Arabic number following by period.

paragraph.ListFormat.NumberStyle = NumberedListStyle.ArabicPeriod

'Set the starting value as 1

paragraph.ListFormat.StartValue = 1

'Set the list level as 1

paragraph.IndentLevelNumber = 1

' Set the hanging value

paragraph.FirstLineIndent = -20

'Add paragraph to the textbox

paragraph = textBoxShape.TextBody.AddParagraph("Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.")

'Set the list type as Numbered list

paragraph.ListFormat.Type = ListType.Numbered

'Set the numbered style (list numbering) as lower case alphabet following by period.

paragraph.ListFormat.NumberStyle = NumberedListStyle.AlphaLcPeriod

'Set the list level as 2

paragraph.IndentLevelNumber = 2

' Set the hanging value

paragraph.FirstLineIndent = -20

'Add paragraph to the textbox

paragraph = textBoxShape.TextBody.AddParagraph("Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.")

'Set the list type as Numbered list

paragraph.ListFormat.Type = ListType.Numbered

'Set the numbered style (list numbering) as roman number lower casing following by period.

paragraph.ListFormat.NumberStyle = NumberedListStyle.RomanLcPeriod

'Set the list level as 3

paragraph.IndentLevelNumber = 3

' Set the hanging value

paragraph.FirstLineIndent = -20

'Add paragraph to the textbox

paragraph = textBoxShape.TextBody.AddParagraph("Excepteur sint occaecat upidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.")

'Set the list type as Numbered list

paragraph.ListFormat.Type = ListType.Numbered

paragraph.ListFormat.NumberStyle = NumberedListStyle.ArabicPeriod

'Set the list level as 1

paragraph.IndentLevelNumber = 1

' Set the hanging value

paragraph.FirstLineIndent = -20

'Save the presentation to the file system.

presentation_1.Save("MultiLevelList.pptx")

'Close the presentation

presentation_1.Close()



{% endhighlight %}

The above code snippet will generate a multi-level list in presentation as below.

<table>
<tr>
<td>
{{'![C:/Users/devisrijothi/Pictures/Screenshots/Screenshot (34).png](Workingwithlist_images/Workingwithlist_img1.jpeg)'| markdownify }}
<br/><br/></td></tr>
</table>
