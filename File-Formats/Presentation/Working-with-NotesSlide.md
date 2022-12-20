---
title: Working with Notes in PowerPoint Presentation | Syncfusion |
description: Code examples to create, edit, and format notes in C# using Syncfusion .NET PowerPoint library without Microsoft PowerPoint or interop dependencies.
platform: file-formats 
control: Presentation
documentation: UG
keywords: Working with Notes
---

# Working with PowerPoint Notes

Notes are the contents associated with each slide and are visible only to the presenter when monitors are shared in “Presenter View”. It shows hint for the speaker, so it is often called as “Speaker Notes”. The presenter can optionally add key points to notes. You can add and modify the notes in your slide using Essential Presentation library.

## Adding Notes to a Slide

The below code example demonstrates how to create a Notes in a PowerPoint Slide.
{% tabs %}
{% highlight c# tabtitle="C#" %}
//Creates a Presentation without slides.
IPresentation pptxDoc = Presentation.Create();
//Adds new slide with blank slide layout type.
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Adds new notes slide in the specified slide.
INotesSlide notesSlide = slide.AddNotesSlide();
//Adds text content into the Notes Slide.
notesSlide.NotesTextBody.AddParagraph("Notes content");
//Saves Presentation with specified file name with extension.
pptxDoc.Save("PresentationWithNotesSlide.pptx");
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Creates a Presentation without slides.
Dim pptxDoc As IPresentation = Presentation.Create()
'Adds new slide with blank slide layout type.
Dim slide As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank)
'Adds new notes slide in the specified slide.
Dim notesSlide As INotesSlide = slide.AddNotesSlide()
'Adds text content into the Notes Slide.
notesSlide.NotesTextBody.AddParagraph("Notes content")
'Saves Presentation with specified file name with extension.
pptxDoc.Save("PresentationWithNotesSlide.pptx")
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Creates a Presentation without slides.
IPresentation pptxDoc = Presentation.Create();
//Adds new slide with blank slide layout type.
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Adds new notes slide in the specified slide.
INotesSlide notesSlide = slide.AddNotesSlide();
//Adds text content into the Notes Slide.
notesSlide.NotesTextBody.AddParagraph("Notes content");
//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "PresentationWithNotesSlide";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });
//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();
//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Creates a Presentation without slides.
IPresentation pptxDoc = Presentation.Create();
//Adds new slide with blank slide layout type.
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Adds new notes slide in the specified slide.
INotesSlide notesSlide = slide.AddNotesSlide();
//Adds text content into the Notes Slide.
notesSlide.NotesTextBody.AddParagraph("Notes content");
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream(OutputFileName, FileMode.Create);
pptxDoc.Save(outputStream);
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Creates a Presentation without slides.
IPresentation pptxDoc = Presentation.Create();
//Adds new slide with blank slide layout type.
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Adds new notes slide in the specified slide.
INotesSlide notesSlide = slide.AddNotesSlide();
//Adds text content into the Notes Slide.
notesSlide.NotesTextBody.AddParagraph("Notes content");
//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();
//Save Presentation in stream format.
pptxDoc.Save(stream);
//Close the presentation
pptxDoc.Close();
stream.Position = 0;
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Sample.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Sample.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
{% endhighlight %}

{% endtabs %}

## Adding Text into the Notes 

The following code example demonstrates how to add a text in a Notes.

{% tabs %}
{% highlight c# tabtitle="C#" %}
//Creates a Presentation without slides.
IPresentation pptxDoc = Presentation.Create();
//Adds new slide with blank slide layout type.
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Adds new notes slide in the specified slide.
INotesSlide notesSlide = slide.AddNotesSlide();
//Adds Paragraph into the text body.
IParagraph paragraph = notesSlide.NotesTextBody.AddParagraph();
//Adds text part into the Paragraph.
ITextPart textPart = paragraph.AddTextPart();
textPart.Text = "The notes slide represents the contents and key notes of the corresponding slide. It is more useful when we use Presenter View while presenting the seminars through SlideShow.";
//Sets Bold format for text content.
textPart.Font.Bold=true;
// Sets font style using font name.
textPart.Font.FontName = "Times New Roman";
// Sets text content size using FontSize property.
textPart.Font.FontSize = 20;
//Saves Presentation with specified file name with extension.
pptxDoc.Save("PresentationWithNotesSlide.pptx");
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Creates a Presentation without slides.
Dim pptxDoc As IPresentation = Presentation.Create()
'Adds new slide with blank slide layout type.
Dim slide As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank)
'Adds new notes slide in the specified slide.
Dim notesSlide As INotesSlide = slide.AddNotesSlide()
'Adds Paragraph into the text body.
Dim paragraph As IParagraph = notesSlide.NotesTextBody.AddParagraph()
'Adds text part into the Paragraph.
Dim textPart As ITextPart = paragraph.AddTextPart()
textPart.Text = "The notes slide represents the contents and key notes of the corresponding slide. It is more useful when we use Presenter View while presenting the seminars through SlideShow."
'Sets Bold format for text content.
textPart.Font.Bold = True
'Sets font style using font name.
textPart.Font.FontName = "Times New Roman"
'Sets text content size using FontSize property.
textPart.Font.FontSize = 20
'Saves Presentation with specified file name with extension.
pptxDoc.Save("PresentationWithNotesSlide.pptx")
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Creates a Presentation without slides.
IPresentation pptxDoc = Presentation.Create();
//Adds new slide with blank slide layout type.
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Adds new notes slide in the specified slide.
INotesSlide notesSlide = slide.AddNotesSlide();
//Adds Paragraph into the text body.
IParagraph paragraph = notesSlide.NotesTextBody.AddParagraph();
//Adds text part into the Paragraph.
ITextPart textPart = paragraph.AddTextPart();
textPart.Text = "The notes slide represents the contents and key notes of the corresponding slide. It is more useful when we use Presenter View while presenting the seminars through SlideShow.";
//Sets Bold format for text content.
textPart.Font.Bold=true;
//Sets font style using font name.
textPart.Font.FontName = "Times New Roman";
//Sets text content size using FontSize property.
textPart.Font.FontSize = 20;
//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "PresentationWithNotesSlide";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });
//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();
//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Creates a Presentation without slides.
IPresentation pptxDoc = Presentation.Create();
//Adds new slide with blank slide layout type.
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Adds new notes slide in the specified slide.
INotesSlide notesSlide = slide.AddNotesSlide();
//Adds Paragraph into the text body.
IParagraph paragraph = notesSlide.NotesTextBody.AddParagraph();
//Adds text part into the Paragraph.
ITextPart textPart = paragraph.AddTextPart();
textPart.Text = "The notes slide represents the contents and key notes of the corresponding slide. It is more useful when we use Presenter View while presenting the seminars through SlideShow.";
//Sets Bold format for text content.
textPart.Font.Bold=true;
// Sets font style using font name.
textPart.Font.FontName = "Times New Roman";
// Sets text content size using FontSize property.
textPart.Font.FontSize = 20;
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream(OutputFileName, FileMode.Create);
pptxDoc.Save(outputStream);
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Creates a Presentation without slides.
IPresentation pptxDoc = Presentation.Create();
//Adds new slide with blank slide layout type.
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Adds new notes slide in the specified slide.
INotesSlide notesSlide = slide.AddNotesSlide();
//Adds Paragraph into the text body.
IParagraph paragraph = notesSlide.NotesTextBody.AddParagraph();
//Adds text part into the Paragraph.
ITextPart textPart = paragraph.AddTextPart();
textPart.Text = "The notes slide represents the contents and key notes of the corresponding slide. It is more useful when we use Presenter View while presenting the seminars through SlideShow.";
//Sets Bold format for text content.
textPart.Font.Bold=true;
//Sets font style using font name.
textPart.Font.FontName = "Times New Roman";
//Sets text content size using FontSize property.
textPart.Font.FontSize = 20;
//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();
//Save Presentation in stream format.
pptxDoc.Save(stream);
//Close the presentation
pptxDoc.Close();
stream.Position = 0;
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Sample.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Sample.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
{% endhighlight %}

{% endtabs %}

## Adding a numbered list to Notes

The following code example demonstrates how to create simple numbered list as Notes.

{% tabs %}
{% highlight c# tabtitle="C#" %}
//Creates a Presentation without slides.
IPresentation pptxDoc = Presentation.Create();
//Adds new slide with blank slide layout type.
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Adds new notes slide in the specified slide.
INotesSlide notesSlide = slide.AddNotesSlide();
// Adds a new paragraph with the text in the left hand side textbox. 
IParagraph paragraph = notesSlide.NotesTextBody.AddParagraph("The Northwind sample database (Northwind.mdb) is included with all versions of Access."); 
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
paragraph = notesSlide.NotesTextBody.AddParagraph("It provides data you can experiment with and database objects that demonstrate features you might want to implement in your own databases."); 
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
paragraph = notesSlide.NotesTextBody.AddParagraph("Using Northwind, you can become familiar with how a relational database is structured and how the database objects work together to help you enter, store, manipulate, and print your data."); 
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
pptxDoc.Save("Sample.pptx"); 
//Closes the Presentation 
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Creates a Presentation without slides.
Dim pptxDoc As IPresentation = Presentation.Create()
'Adds new slide with blank slide layout type.
Dim slide As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank)
'Adds new notes slide in the specified slide.
Dim notesSlide As INotesSlide = slide.AddNotesSlide()
' Adds a new paragraph with the text in the left hand side textbox. 
Dim paragraph As IParagraph = notesSlide.NotesTextBody.AddParagraph("The Northwind sample database (Northwind.mdb) is included with all versions of Access.")
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
paragraph = notesSlide.NotesTextBody.AddParagraph("It provides data you can experiment with and database objects that demonstrate features you might want to implement in your own databases.")
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
paragraph = notesSlide.NotesTextBody.AddParagraph("Using Northwind, you can become familiar with how a relational database is structured and how the database objects work together to help you enter, store, manipulate, and print your data.")
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
'Saves the Presentation to the file system. 
pptxDoc.Save("Sample.pptx")
'Closes the Presentation 
pptxDoc.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Creates a Presentation without slides.
IPresentation pptxDoc = Presentation.Create();
//Adds new slide with blank slide layout type.
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Adds new notes slide in the specified slide.
INotesSlide notesSlide = slide.AddNotesSlide();
// Adds a new paragraph with the text in the left hand side textbox. 
IParagraph paragraph = notesSlide.NotesTextBody.AddParagraph("The Northwind sample database (Northwind.mdb) is included with all versions of Access."); 
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
paragraph = notesSlide.NotesTextBody.AddParagraph("It provides data you can experiment with and database objects that demonstrate features you might want to implement in your own databases."); 
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
paragraph = notesSlide.NotesTextBody.AddParagraph("Using Northwind, you can become familiar with how a relational database is structured and how the database objects work together to help you enter, store, manipulate, and print your data."); 
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
//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Sample";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });
//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();
//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile); 
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Creates a Presentation without slides.
IPresentation pptxDoc = Presentation.Create();
//Adds new slide with blank slide layout type.
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Adds new notes slide in the specified slide.
INotesSlide notesSlide = slide.AddNotesSlide();
// Adds a new paragraph with the text in the left hand side textbox. 
IParagraph paragraph = notesSlide.NotesTextBody.AddParagraph("The Northwind sample database (Northwind.mdb) is included with all versions of Access."); 
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
paragraph = notesSlide.NotesTextBody.AddParagraph("It provides data you can experiment with and database objects that demonstrate features you might want to implement in your own databases."); 
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
paragraph = notesSlide.NotesTextBody.AddParagraph("Using Northwind, you can become familiar with how a relational database is structured and how the database objects work together to help you enter, store, manipulate, and print your data."); 
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
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream(OutputFileName, FileMode.Create);
pptxDoc.Save(outputStream);
//Closes the Presentation 
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Creates a Presentation without slides.
IPresentation pptxDoc = Presentation.Create();
//Adds new slide with blank slide layout type.
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Adds new notes slide in the specified slide.
INotesSlide notesSlide = slide.AddNotesSlide();
// Adds a new paragraph with the text in the left hand side textbox. 
IParagraph paragraph = notesSlide.NotesTextBody.AddParagraph("The Northwind sample database (Northwind.mdb) is included with all versions of Access."); 
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
paragraph = notesSlide.NotesTextBody.AddParagraph("It provides data you can experiment with and database objects that demonstrate features you might want to implement in your own databases."); 
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
paragraph = notesSlide.NotesTextBody.AddParagraph("Using Northwind, you can become familiar with how a relational database is structured and how the database objects work together to help you enter, store, manipulate, and print your data."); 
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
//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();
//Save Presentation in stream format.
pptxDoc.Save(stream);
//Close the presentation
pptxDoc.Close();
stream.Position = 0;
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Sample.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Sample.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
{% endhighlight %}

{% endtabs %}

## Removing Notes from a Slide

The below code example demonstrates how to remove a Notes from a PowerPoint Slide.
{% tabs %}

{% highlight c# tabtitle="C#" %}
//Opens an existing PowerPoint presentation.
IPresentation pptxDoc = Presentation.Open("Sample.pptx");
//Gets instance of the first slide from the Presentation.
ISlide slide = pptxDoc.Slides[0] as ISlide;
//Removes Notes Slide from a corresponding slide.
slide.RemoveNotesSlide();
//Saves Presentation with specified file name with extension.
pptxDoc.Save("PresentationWithNotesSlide.pptx");
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Opens an existing PowerPoint presentation.
Dim pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
'Gets instance of the first slide from the Presentation.
Dim slide As ISlide = TryCast(pptxDoc.Slides(0), ISlide)
'Removes Notes Slide from a corresponding slide.
slide.RemoveNotesSlide()
'Saves Presentation with specified file name with extension.
pptxDoc.Save("PresentationWithNotesSlide.pptx")
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".pptx");
//Creates a storage file from FileOpenPicker
StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc= await Presentation.OpenAsync(inputStorageFile);
//Gets instance of the first slide from the Presentation.
ISlide slide = pptxDoc.Slides[0] as ISlide;
//Removes Notes Slide from a corresponding slide.
slide.RemoveNotesSlide();
//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "PresentationWithNotesSlide";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });
//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();
//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream(inputFileName,FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);
//Gets instance of the first slide from the Presentation.
ISlide slide = pptxDoc.Slides[0] as ISlide;
//Removes Notes Slide from a corresponding slide.
slide.RemoveNotesSlide();
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream(OutputFileName, FileMode.Create);
pptxDoc.Save(outputStream);
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream(resourcePath);
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);
//Gets instance of the first slide from the Presentation.
ISlide slide = pptxDoc.Slides[0] as ISlide;
//Removes Notes Slide from a corresponding slide.
slide.RemoveNotesSlide();
//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();
//Save Presentation in stream format.
pptxDoc.Save(stream);
//Close the presentation
pptxDoc.Close();
stream.Position = 0;
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Sample.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Sample.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
{% endhighlight %}

{% endtabs %}