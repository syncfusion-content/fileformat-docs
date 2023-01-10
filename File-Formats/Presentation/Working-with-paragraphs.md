---
title: Working with Paragraph in PowerPoint Presentation | Syncfusion
description: This section illustrates how to work with Paragraphs and texts in Syncfusion PowerPoint Presentation
platform: file-formats
control: Presentation
documentation: UG
---
# Working with Paragraph

## Adding Paragraph to slide

All the textual contents in a Presentation document is represented by Paragraphs. You can have any number of paragraphs within a [TextBody](https://help.syncfusion.com/cr/file-formats/Syncfusion.Presentation.ITextBody.html) of a textbox or shape in a PowerPoint presentation. 

The following code example demonstrates how to add a paragraph in a slide.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Creates PowerPoint Presentation
IPresentation pptxDoc = Presentation.Create();
//Adds slide to the PowerPoint
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Adds textbox to the slide
IShape textboxShape = slide.AddTextBox(0, 0, 500, 500);
//Adds paragraph to the textbody of textbox
IParagraph paragraph = textboxShape.TextBody.AddParagraph();
//Adds a TextPart to the paragraph
ITextPart textPart = paragraph.AddTextPart();
//Adds text to the TextPart
textPart.Text = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company. The company manufactures and sells metal and composite bicycles to North American, European and Asian commercial markets. While its base operation is located in Washington with 290 employees, several regional sales teams are located throughout their market base.";
//Saves the Presentation
pptxDoc.Save("Output.pptx");
//Closes the Presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Creates PowerPoint Presentation
Dim pptxDoc As IPresentation = Presentation.Create()
'Adds slide to the PowerPoint
Dim slide As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank)
'Adds textbox to the slide
Dim textboxShape As IShape = slide.AddTextBox(0, 0, 500, 500)
'Adds paragraph to the textbody of textbox
Dim paragraph As IParagraph = textboxShape.TextBody.AddParagraph()
'Adds a TextPart to the paragraph
Dim textPart As ITextPart = paragraph.AddTextPart()
'Adds text to the TextPart
textPart.Text = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company. The company manufactures and sells metal and composite bicycles to North American, European and Asian commercial markets. While its base operation is located in Washington with 290 employees, several regional sales teams are located throughout their market base."
'Saves the Presentation
pptxDoc.Save("Output.pptx")
'Closes the Presentation
pptxDoc.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Creates PowerPoint Presentation
IPresentation pptxDoc = Presentation.Create();
//Adds slide to the PowerPoint
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Adds textbox to the slide
IShape textboxShape = slide.AddTextBox(0, 0, 500, 500);
//Adds paragraph to the textbody of textbox
IParagraph paragraph = textboxShape.TextBody.AddParagraph();
//Adds a TextPart to the paragraph
ITextPart textPart = paragraph.AddTextPart();
//Adds text to the TextPart
textPart.Text = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company. The company manufactures and sells metal and composite bicycles to North American, European and Asian commercial markets. While its base operation is located in Washington with 290 employees, several regional sales teams are located throughout their market base.";
//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Output";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });
//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();
//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Creates PowerPoint Presentation
IPresentation pptxDoc = Presentation.Create();
//Adds slide to the PowerPoint
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Adds textbox to the slide
IShape textboxShape = slide.AddTextBox(0, 0, 500, 500);
//Adds paragraph to the textbody of textbox
IParagraph paragraph = textboxShape.TextBody.AddParagraph();
//Adds a TextPart to the paragraph
ITextPart textPart = paragraph.AddTextPart();
//Adds text to the TextPart
textPart.Text = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company. The company manufactures and sells metal and composite bicycles to North American, European and Asian commercial markets. While its base operation is located in Washington with 290 employees, several regional sales teams are located throughout their market base.";
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Output.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
//Closes the Presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Creates PowerPoint Presentation
IPresentation pptxDoc = Presentation.Create();
//Adds slide to the PowerPoint
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Adds textbox to the slide
IShape textboxShape = slide.AddTextBox(0, 0, 500, 500);
//Adds paragraph to the textbody of textbox
IParagraph paragraph = textboxShape.TextBody.AddParagraph();
//Adds a TextPart to the paragraph
ITextPart textPart = paragraph.AddTextPart();
//Adds text to the TextPart
textPart.Text = "AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company. The company manufactures and sells metal and composite bicycles to North American, European and Asian commercial markets. While its base operation is located in Washington with 290 employees, several regional sales teams are located throughout their market base.";
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Paragraphs/Add-paragraph-to-PowerPoint-slide).

## Applying Paragraph formatting

Each paragraph in a slide can have its own formatting types such as alignment, indent etc. The following code example demonstrates how to format a paragraph in PowerPoint presentation.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Loads the PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open("Sample.pptx");
//Gets the slide from Presentation
ISlide slide = pptxDoc.Slides[0];
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
pptxDoc.Save("Output.pptx");
//Closes the Presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Loads the PowerPoint Presentation
Dim pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
'Gets the slide from Presentation
Dim slide As ISlide = pptxDoc.Slides(0)
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
pptxDoc.Save("Output.pptx")
'Closes the Presentation
pptxDoc.Close()
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
//Gets the slide from Presentation
ISlide slide = pptxDoc.Slides[0];
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
//Adds text to paragraph
paragraph.Text = "PowerPoint Presentation";
//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Output";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });
//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();
//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream("Sample.pptx",FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);
//Gets the slide from Presentation
ISlide slide = pptxDoc.Slides[0];
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
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Output.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
//Closes the Presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Sample.pptx");
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);
//Gets the slide from Presentation
ISlide slide = pptxDoc.Slides[0];
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
//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();
//Save Presentation in stream format.
pptxDoc.Save(stream);
//Close the presentation
pptxDoc.Close();
stream.Position = 0;
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Paragraphs/Apply-paragraph-formatting).

## Working with text

With Essential Presentation, you can add or modify the text in a Presentation. Within the paragraph, textual contents are grouped into one or more child elements as [TextParts](https://help.syncfusion.com/cr/file-formats/Syncfusion.Presentation.ITextParts.html). Each [TextPart](https://help.syncfusion.com/cr/file-formats/Syncfusion.Presentation.ITextPart.html) represents a region of text with a common set of formatted text. The following code example demonstrates how to add text with different formatting into a single paragraph.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Creates the PowerPoint Presentation instance
IPresentation pptxDoc = Presentation.Create();
//Gets the slide from Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
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
pptxDoc.Save("Output.pptx");
//Closes the Presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Loads the PowerPoint Presentation
Dim pptxDoc As IPresentation = Presentation.Create()
'Gets the slide from Presentation
Dim slide As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank)
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
pptxDoc.Save("Output.pptx")
'Closes the Presentation
pptxDoc.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Create the PowerPoint Presentation
IPresentation pptxDoc = Presentation.Create();
//Gets the slide from Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Adds textbox to the slide
IShape textboxShape2 = slide.AddTextBox(500, 0, 400, 500);
//Adds paragraph to the textbody of textbox
IParagraph paragraph2 = textboxShape2.TextBody.AddParagraph();
//Adds a TextPart to the paragraph
ITextPart textPartFormatting = paragraph2.AddTextPart();
//Adds text to the TextPart
textPartFormatting.Text = "In 2000, AdventureWorks Cycles bought a small manufacturing plant, located in Mexico. The plant manufactures several critical subcomponents for the AdventureWorks Cycles product line. These subcomponents are shipped to the another location for final product assembly. In 2001, the plant, became the sole manufacturer and distributor of the touring bicycle product group.";
//Sets the underline color
textPartFormatting.UnderlineColor = ColorObject.Black;
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
font2.Color = ColorObject.Blue;
//Sets the underline type
font2.Underline = TextUnderlineType.WavyDouble;
//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Output";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });
//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();
//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Creates the PowerPoint Presentation instance
IPresentation pptxDoc = Presentation.Create();
//Adds new slide to the presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Adds textbox to the slide
IShape textboxShape2 = slide.AddTextBox(500, 0, 400, 500);
//Adds paragraph to the textbody of textbox
IParagraph paragraph2 = textboxShape2.TextBody.AddParagraph();
//Adds a TextPart to the paragraph
ITextPart textPartFormatting = paragraph2.AddTextPart();
//Adds text to the TextPart
textPartFormatting.Text = "In 2000, AdventureWorks Cycles bought a small manufacturing plant, located in Mexico. The plant manufactures several critical subcomponents for the AdventureWorks Cycles product line. These subcomponents are shipped to the another location for final product assembly. In 2001, the plant, became the sole manufacturer and distributor of the touring bicycle product group.";
//Sets the underline color
textPartFormatting.UnderlineColor = ColorObject.AliceBlue;
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
font2.Color = ColorObject.BlanchedAlmond;
//Sets the underline type
font2.Underline = TextUnderlineType.WavyDouble;
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Sample.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
//Closes the Presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Creates the PowerPoint Presentation instance
IPresentation pptxDoc = Presentation.Create();
//Adds new slide to the presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Adds textbox to the slide
IShape textboxShape2 = slide.AddTextBox(500, 0, 400, 500);
//Adds paragraph to the textbody of textbox
IParagraph paragraph2 = textboxShape2.TextBody.AddParagraph();
//Adds a TextPart to the paragraph
ITextPart textPartFormatting = paragraph2.AddTextPart();
//Adds text to the TextPart
textPartFormatting.Text = "In 2000, AdventureWorks Cycles bought a small manufacturing plant, located in Mexico. The plant manufactures several critical subcomponents for the AdventureWorks Cycles product line. These subcomponents are shipped to the another location for final product assembly. In 2001, the plant, became the sole manufacturer and distributor of the touring bicycle product group.";
//Sets the underline color
textPartFormatting.UnderlineColor = ColorObject.AliceBlue;
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
font2.Color = ColorObject.BlanchedAlmond;
//Sets the underline type
font2.Underline = TextUnderlineType.WavyDouble;
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
    "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Paragraphs/Add-text-with-different-formattings).

## Modifying text

You can modify a text by accessing the existing paragraphs in a Presentation. The following code example demonstrates how to modify the content in a paragraph.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Opens an existing Presentation from file system.
IPresentation pptxDoc = Presentation.Open("Sample.pptx");
//Retrieves the first slide from Presentation
ISlide slide = pptxDoc.Slides[0];
//Retrieves the first shape.
IShape shape = slide.Shapes[0] as IShape;
//Retrieves the first paragraph of the shape.
IParagraph paragraph = shape.TextBody.Paragraphs[0];
//Retrieves the first TextPart of the shape.
ITextPart textPart = paragraph.TextParts[0];
//Modifies the text content of the TextPart.
textPart.Text = "Hello Presentation";
//Saves the presentation to the file system.
pptxDoc.Save("Result.pptx");
//Closes the Presentation.
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Opens an existing Presentation from file system.
Dim pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
'Retrieves the first slide from Presentation
Dim slide As ISlide = pptxDoc.Slides(0)
'Retrieves the first shape.
Dim shape As IShape = TryCast(slide.Shapes(0), IShape)
'Retrieves the first paragraph of the shape.
Dim paragraph As IParagraph = shape.TextBody.Paragraphs(0)
'Retrieves the first TextPart of the shape.
Dim textPart As ITextPart = paragraph.TextParts(0)
'Modifies the text content of the TextPart.
textPart.Text = "Hello Presentation"
'Saves the presentation to the file system.
pptxDoc.Save("Result.pptx")
'Closes the Presentation.
pptxDoc.Close()
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
//Retrieves the first slide from Presentation
ISlide slide = pptxDoc.Slides[0];
//Retrieves the first shape.
IShape shape = slide.Shapes[0] as IShape;
//Retrieves the first paragraph of the shape.
IParagraph paragraph = shape.TextBody.Paragraphs[0];
//Retrieves the first TextPart of the shape.
ITextPart textPart = paragraph.TextParts[0];
//Modifies the text content of the TextPart.
 textPart.Text = "Hello Presentation";
//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Result";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });
//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();
//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream("Sample.pptx",FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);
//Retrieves the first slide from Presentation
ISlide slide = pptxDoc.Slides[0];
//Retrieves the first shape.
IShape shape = slide.Shapes[0] as IShape;
//Retrieves the first paragraph of the shape.
IParagraph paragraph = shape.TextBody.Paragraphs[0];
//Retrieves the first TextPart of the shape.
ITextPart textPart = paragraph.TextParts[0];
//Modifies the text content of the TextPart.
textPart.Text = "Hello Presentation";
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Output.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
//Closes the Presentation.
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Sample.pptx");
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);
//Retrieves the first slide from Presentation
ISlide slide = pptxDoc.Slides[0];
//Retrieves the first shape.
IShape shape = slide.Shapes[0] as IShape;
//Retrieves the first paragraph of the shape.
IParagraph paragraph = shape.TextBody.Paragraphs[0];
//Retrieves the first TextPart of the shape.
ITextPart textPart = paragraph.TextParts[0];
//Modifies the text content of the TextPart.
textPart.Text = "Hello Presentation";
//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();
//Save Presentation in stream format.
pptxDoc.Save(stream);
//Close the presentation
pptxDoc.Close();
stream.Position = 0;
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Paragraphs/Modify-existing-text).

### Edit a language of TextPart

With Essential Presentation, you can modify the language of Presentation [TextPart](https://help.syncfusion.com/cr/file-formats/Syncfusion.Presentation.ITextPart.html). This allows viewer application to check spelling and grammar according to the language of each [TextPart](https://help.syncfusion.com/cr/file-formats/Syncfusion.Presentation.ITextPart.html). The following code example demonstrates how to modify a language of Presentation [TextPart](https://help.syncfusion.com/cr/file-formats/Syncfusion.Presentation.ITextPart.html).

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Create a Microsoft PowerPoint instance
IPresentation pptxDoc = Presentation.Create();
//Add the slide for Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Adds textbox to the slide
IShape textboxShape = slide.AddTextBox(500, 0, 400, 500);
//Adds paragraph to the textbody of textbox
IParagraph paragraph = textboxShape.TextBody.AddParagraph();
//Adds a TextPart to the paragraph
ITextPart textPart = paragraph.AddTextPart();
//Adds text to the TextPart
textPart.Text = "AdventureWorks Cycles";
//Sets a language as "Spanish (Argentina)" for TextPart.
textPart.Font.LanguageID = (short)LocaleIDs.es_AR;
//Save a PowerPoint document
pptxDoc.Save("Output.pptx");
//Close the PowerPoint instance
pptxDoc.Dispose();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Create a Microsoft PowerPoint instance
Dim pptxDoc As IPresentation = Presentation.Create
'Add the slide for Presentation
Dim slide As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank)
'Adds textbox to the slide
Dim textboxShape As IShape = slide.AddTextBox(500, 0, 400, 500)
'Adds paragraph to the textbody of textbox
Dim paragraph As IParagraph = textboxShape.TextBody.AddParagraph
'Adds a TextPart to the paragraph
Dim textPart As ITextPart = paragraph.AddTextPart
'Adds text to the TextPart
textPart.Text = "AdventureWorks Cycles"
'Sets a language as "Spanish (Argentina)" for TextPart.
textPart.Font.LanguageID = CType(LocaleIDs.es_AR,Short)
'Save a PowerPoint document
pptxDoc.Save("Output.pptx")
'Close the PowerPoint instance
pptxDoc.Dispose
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Create a Microsoft PowerPoint instance
IPresentation pptxDoc = Presentation.Create();
//Add the slide for Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Adds textbox to the slide
IShape textboxShape = slide.AddTextBox(500, 0, 400, 500);
//Adds paragraph to the textbody of textbox
IParagraph paragraph = textboxShape.TextBody.AddParagraph();
//Adds a TextPart to the paragraph
ITextPart textPart = paragraph.AddTextPart();
//Adds text to the TextPart
textPart.Text = "AdventureWorks Cycles";
//Sets a language as "Spanish (Argentina)" for TextPart.
textPart.Font.LanguageID = (short)LocaleIDs.es_AR;
//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Output";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });
//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();
//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Create a Microsoft PowerPoint instance
IPresentation pptxDoc = Presentation.Create();
//Add the slide for Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Adds textbox to the slide
IShape textboxShape = slide.AddTextBox(500, 0, 400, 500);
//Adds paragraph to the textbody of textbox
IParagraph paragraph = textboxShape.TextBody.AddParagraph();
//Adds a TextPart to the paragraph
ITextPart textPart = paragraph.AddTextPart();
//Adds text to the TextPart
textPart.Text = "AdventureWorks Cycles";
//Sets a language as "Spanish (Argentina)" for TextPart.
textPart.Font.LanguageID = (short)LocaleIDs.es_AR;
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Output.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
//Closes the Presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Create a Microsoft PowerPoint instance
IPresentation pptxDoc = Presentation.Create();
//Add the slide for Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);
//Adds textbox to the slide
IShape textboxShape = slide.AddTextBox(500, 0, 400, 500);
//Adds paragraph to the textbody of textbox
IParagraph paragraph = textboxShape.TextBody.AddParagraph();
//Adds a TextPart to the paragraph
ITextPart textPart = paragraph.AddTextPart();
//Adds text to the TextPart
textPart.Text = "AdventureWorks Cycles";
//Sets a language as "Spanish (Argentina)" for TextPart.
textPart.Font.LanguageID = (short)LocaleIDs.es_AR;
//Create new memory stream to save Presentation
MemoryStream stream = new MemoryStream();
//Save Presentation in stream format
pptxDoc.Save(stream);
//Close the presentation
pptxDoc.Close();
stream.Position = 0;
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Paragraphs/Modify-text-language).

## Enabling shrink text on overflow option

In a PowerPoint slide, if you add a text more than a shape can hold, the text will overflow from the shape. But by using a Shrink text on overflow option, you can fit a large text within a shape. The following code example demonstrates how to enable this property.

{% tabs %}

{% highlight c# tabtitle="C#" %}
// Create a new PowerPoint file.
using (IPresentation ppDoc = Presentation.Create())
{
    //Add a slide to the PowerPoint file.
    ISlide slide = ppDoc.Slides.Add(SlideLayoutType.Blank);
    //Add a text box to the slide
    IShape textBox = slide.Shapes.AddTextBox(100, 100, 100, 100);
    //Add text to the text box. 
    textBox.TextBody.AddParagraph("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");
    //Set the property to shrink text on overflow. 
    textBox.TextBody.FitTextOption = FitTextOption.ShrinkTextOnOverFlow;
    //Save the PowerPoint file
    ppDoc.Save("Sample.pptx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Create a new PowerPoint file
Dim pptxDoc As IPresentation = Presentation.Create()
'Adds slide to the PowerPoint
Dim slide As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank)
'Adds textbox to the slide
Dim textboxShape As IShape = slide.AddTextBox(0, 0, 500, 500)
'Adds paragraph to the textbody of textbox
Dim paragraph As IParagraph = textboxShape.TextBody.AddParagraph("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.")
'Set the property to shrink text on overflow.
textboxShape.TextBody.FitTextOption = FitTextOption.ShrinkTextOnOverFlow
'Save the PowerPoint file
pptxDoc.Save("Output.pptx")
'Close the PowerPoint file
pptxDoc.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Paragraphs/Enable-text-shrink-on-overflow).

N> The shrink text on overflow is not supported in UWP, ASP.NET CORE and Xamarin platforms.

## Removing the paragraph 

The following code example demonstrates how to remove a paragraph from a slide.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Opens an existing Presentation from file system.
IPresentation pptxDoc = Presentation.Open("Sample.pptx");
//Retrieves the first slide from Presentation
ISlide slide = pptxDoc.Slides[0];
//Retrieves the first shape
IShape shape = slide.Shapes[0] as IShape;
//Retrieves the first paragraph of the shape
IParagraph paragraph = shape.TextBody.Paragraphs[0];
//Removes the first paragraph from the textbody of the shape
shape.TextBody.Paragraphs.Remove(paragraph);
//Saves the presentation to the file system
pptxDoc.Save("Result.pptx");
//Closes the Presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Opens an existing Presentation from file system.
Dim pptxDoc As IPresentation = Presentation.Open("Sample.pptx")
'Retrieves the first slide from Presentation
Dim slide As ISlide = pptxDoc.Slides(0)
'Retrieves the first shape.
Dim shape As IShape = TryCast(slide.Shapes(0), IShape)
'Retrieves the first paragraph of the shape.
Dim paragraph As IParagraph = shape.TextBody.Paragraphs(0)
'Removes the first paragraph from the textbody of the shape.
shape.TextBody.Paragraphs.Remove(paragraph)
'Saves the presentation to the file system.
pptxDoc.Save("Result.pptx")
'Closes the Presentation.
pptxDoc.Close()
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
//Retrieves the first slide from Presentation
ISlide slide = pptxDoc.Slides[0];
//Retrieves the first shape.
IShape shape = slide.Shapes[0] as IShape;
//Retrieves the first paragraph of the shape.
IParagraph paragraph = shape.TextBody.Paragraphs[0];
//Removes the first paragraph from the textbody of the shape
shape.TextBody.Paragraphs.Remove(paragraph);
//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Result";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });
//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();
//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream("Sample.pptx",FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);
//Retrieves the first slide from Presentation
ISlide slide = pptxDoc.Slides[0];
//Retrieves the first shape
IShape shape = slide.Shapes[0] as IShape;
//Retrieves the first paragraph of the shape
IParagraph paragraph = shape.TextBody.Paragraphs[0];
//Removes the first paragraph from the textbody of the shape
shape.TextBody.Paragraphs.Remove(paragraph);
//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Output.pptx", FileMode.Create);
pptxDoc.Save(outputStream);
//Closes the Presentation
pptxDoc.Close();
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("SampleBrowser.Presentation.Samples.Template.Sample.pptx");
//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);
//Retrieves the first slide from Presentation
ISlide slide = pptxDoc.Slides[0];
//Retrieves the first shape
IShape shape = slide.Shapes[0] as IShape;
//Retrieves the first paragraph of the shape
IParagraph paragraph = shape.TextBody.Paragraphs[0];
//Removes the first paragraph from the textbody of the shape
shape.TextBody.Paragraphs.Remove(paragraph);
//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();
//Save Presentation in stream format.
pptxDoc.Save(stream);
//Close the presentation
pptxDoc.Close();
stream.Position = 0;
//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Output.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Output.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Paragraphs/Remove-paragraph).
