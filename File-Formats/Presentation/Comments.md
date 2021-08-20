---

title: Working with comments in PowerPoint presentation | Syncfusion
description: Learn here all about Working with comments feature of Syncfusion PowerPoint Presentation Library and more.
platform: file-formats
control: Presentation
documentation: UG
keywords: comments
---
# Working with Comments in PowerPoint Presentation
A comment is a text note attached to a location on a slide. Each comment contains an unformatted text string, information about its author and the time it was added. In a PowerPoint slide, the comments and the reply comments are sequentially maintained in a single collection. The top most comment will have the index position 0 and the other comments and replies in that slide will have the incremental index positions.

## Adding a comment
The following code example demonstrates how to add a comment in a slide.

{% tabs %}

{% highlight c# %}

//Create a PowerPoint Presentation
IPresentation pptxDoc = Presentation.Create();

//Add a slide to the Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Add a comment to the slide
slide.Comments.Add(10, 10, "Author1", "A1", "Can we change the font size to 20?", DateTime.Now);

//Save the Presentation
pptxDoc.Save("Comment.pptx");

//Close the Presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight vb.net %}

'Create a PowerPoint Presentation
Dim pptxDoc As IPresentation = Presentation.Create()

'Add a slide to the Presentation
Dim slide As ISlide = pptxDoc.Slides.Add(SlideLayoutType.Blank)

'Add a comment to the slide
slide.Comments.Add(10, 10, "Author1", "A1", "Can we change the font size to 20?", DateTime.Now)

'Save the Presentation
pptxDoc.Save("Comment.pptx")

'Close the Presentation
pptxDoc.Close()

{% endhighlight %}

{% highlight UWP %}

//Create a PowerPoint Presentation
IPresentation pptxDoc = Presentation.Create();

//Add a slide to the Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Add a comment to the slide
slide.Comments.Add(10, 10, "Author1", "A1", "Can we change the font size to 20?", DateTime.Now);

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Comment";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);

{% endhighlight %}

{% highlight ASP.NET CORE %}

//Create a PowerPoint Presentation
IPresentation pptxDoc = Presentation.Create();

//Add a slide to the Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Add a comment to the slide
slide.Comments.Add(10, 10, "Author1", "A1", "Can we change the font size to 20?", DateTime.Now);

//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("Comment.pptx", FileMode.Create);
pptxDoc.Save(outputStream);

//Close the Presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight XAMARIN %}

//Create a PowerPoint Presentation
IPresentation pptxDoc = Presentation.Create();

//Add a slide to the Presentation
ISlide slide = pptxDoc.Slides.Add(SlideLayoutType.Blank);

//Add a comment to the slide
slide.Comments.Add(10, 10, "Author1", "A1", "Can we change the font size to 20?", DateTime.Now);

//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();

//Save Presentation in stream format.
pptxDoc.Save(stream);

//Close the presentation
pptxDoc.Close();
stream.Position = 0;

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("Comment.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("Comment.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);

{% endhighlight %}

{% endtabs %}

## Replying to a comment
The following code example demonstrates how to reply to an existing comment in a slide.

{% tabs %}

{% highlight c# %}

//Create a PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open("Sample.pptx");

//Get the slide from the Presentation
ISlide slide = pptxDoc.Slides[0];

//Get the comment in the slide
IComment comment = slide.Comments[0] as IComment;

//Add reply to the comment
slide.Comments.Add("Author2", "A2", "Yes, we can we change the font size to 20", DateTime.Now, comment);

//Save the presentation
pptxDoc.Save("ReplyComment.pptx");

//Close the Presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight vb.net %}

'Create a PowerPoint Presentation
Dim pptxDoc As IPresentation = Presentation.Open("Sample.pptx")

'Get the slide from the Presentation
Dim slide As ISlide = pptxDoc.Slides(0)

'Get the comment in the slide
Dim comment As IComment = TryCast(slide.Comments(0), IComment)

'Add reply to the comment
slide.Comments.Add("Author2", "A2", "Yes, we can we change the font size to 20", DateTime.Now, comment)

'Save the presentation
pptxDoc.Save("ReplyComment.pptx")

'Close the Presentation
pptxDoc.Close()

{% endhighlight %}

{% highlight UWP %}

//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".pptx");

//Creates a storage file from FileOpenPicker
StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();

//Loads or open an PowerPoint Presentation
IPresentation pptxDoc= await Presentation.OpenAsync(inputStorageFile);

//Get the slide from the Presentation
ISlide slide = pptxDoc.Slides[0];

//Get the comment in the slide
IComment comment = slide.Comments[0] as IComment;

//Add reply to the comment
slide.Comments.Add("Author2", "A2", "Yes, we can we change the font size to 20", DateTime.Now, comment);

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "ReplyComment";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);

{% endhighlight %}

{% highlight ASP.NET CORE %}

//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream("Sample.pptx",FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);

//Get the slide from the Presentation
ISlide slide = pptxDoc.Slides[0];

//Get the comment in the slide
IComment comment = slide.Comments[0] as IComment;

//Add reply to the comment
slide.Comments.Add("Author2", "A2", "Yes, we can we change the font size to 20", DateTime.Now, comment);

//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("ReplyComment.pptx", FileMode.Create);
pptxDoc.Save(outputStream);

//Close the Presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight XAMARIN %}

//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("Sample.pptx");

//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);

//Get the slide from the Presentation
ISlide slide = pptxDoc.Slides[0];

//Get the comment in the slide
IComment comment = slide.Comments[0] as IComment;

//Add reply to the comment
slide.Comments.Add("Author2", "A2", "Yes, we can we change the font size to 20", DateTime.Now, comment);

//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();

//Save Presentation in stream format.
pptxDoc.Save(stream);

//Close the presentation
pptxDoc.Close();
stream.Position = 0;

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("ReplyComment.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("ReplyComment.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);

{% endhighlight %}

{% endtabs %}

## Modifying the comment
The following code example demonstrates how to modify the content of a comment.

{% tabs %}

{% highlight c# %}

//Create a PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open("Sample.pptx");

//Open a slide to the Presentation
ISlide slide = pptxDoc.Slides[0];

//Get the comment from the slide
IComment comment = slide.Comments[0] as IComment;

//Modify the comment text
comment.Text = "The comment text content is changed";

//Save the presentation
pptxDoc.Save("ModifyCommentText.pptx");

//Close the Presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight vb.net %}

'Create a PowerPoint Presentation
Dim pptxDoc As IPresentation = Presentation.Open("Sample.pptx")

'Open a slide to the Presentation
Dim slide As ISlide = pptxDoc.Slides(0)

'Get the comment from the slide
Dim comment As IComment = TryCast(slide.Comments(0), IComment)

'Modify the comment text
comment.Text = "The comment text content is changed"

'Save the presentation
pptxDoc.Save("ModifyCommentText.pptx")

'Close the Presentation
pptxDoc.Close()

{% endhighlight %}

{% highlight UWP %}

//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".pptx");

//Creates a storage file from FileOpenPicker
StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();

//Loads or open an PowerPoint Presentation
IPresentation pptxDoc= await Presentation.OpenAsync(inputStorageFile);

//Get the slide from the Presentation
ISlide slide = pptxDoc.Slides[0];

//Get the comment in the slide
IComment comment = slide.Comments[0] as IComment;

//Modify the comment text
comment.Text = "The comment text content is changed";

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "ModifyCommentText";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);

{% endhighlight %}

{% highlight ASP.NET CORE %}

//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream("Sample.pptx",FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);

//Open a slide to the Presentation
ISlide slide = pptxDoc.Slides[0];

//Get the comment from the slide
IComment comment = slide.Comments[0] as IComment;

//Modify the comment text
comment.Text = "The comment text content is changed";

//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("ModifyCommentText.pptx", FileMode.Create);
pptxDoc.Save(outputStream);

{% endhighlight %}

{% highlight XAMARIN %}

//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("Sample.pptx");

//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);

//Open a slide to the Presentation
ISlide slide = pptxDoc.Slides[0];

//Get the comment from the slide
IComment comment = slide.Comments[0] as IComment;

//Modify the comment text
comment.Text = "The comment text content is changed";

//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();

//Save Presentation in stream format.
pptxDoc.Save(stream);

//Close the presentation
pptxDoc.Close();
stream.Position = 0;

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("ModifyCommentText.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("ModifyCommentText.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);

{% endhighlight %}

{% endtabs %}

The following code example demonstrates how to modify the author name of a comment.

{% tabs %}

{% highlight c# %}

//Create a PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open("Sample.pptx");

//Open a slide to the Presentation
ISlide slide = pptxDoc.Slides[0];

//Get the comment from the slide
IComment comment = slide.Comments[0] as IComment;

//Modify the comment text
comment.AuthorName = "NewAuthor";

//Save the presentation
pptxDoc.Save("ModifyCommentAuthor.pptx");

//Close the Presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight vb.net %}

'Create a PowerPoint Presentation
Dim pptxDoc As IPresentation = Presentation.Open("Sample.pptx")

'Open a slide to the Presentation
Dim slide As ISlide = pptxDoc.Slides(0)

'Get the comment from the slide
Dim comment As IComment = TryCast(slide.Comments(0), IComment)

'Modify the comment text
comment.AuthorName = "NewAuthor"

'Save the presentation
pptxDoc.Save("ModifyCommentAuthor.pptx")

'Close the Presentation
pptxDoc.Close()

{% endhighlight %}

{% highlight UWP %}

//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".pptx");

//Creates a storage file from FileOpenPicker
StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();

//Loads or open an PowerPoint Presentation
IPresentation pptxDoc= await Presentation.OpenAsync(inputStorageFile);

//Get the slide from the Presentation
ISlide slide = pptxDoc.Slides[0];

//Get the comment in the slide
IComment comment = slide.Comments[0] as IComment;

//Modify the comment author name
comment.AuthorName = "NewAuthor";

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "ModifyCommentAuthor";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);

{% endhighlight %}

{% highlight ASP.NET CORE %}

//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream("Sample.pptx",FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);

//Open a slide to the Presentation
ISlide slide = pptxDoc.Slides[0];

//Get the comment from the slide
IComment comment = slide.Comments[0] as IComment;

//Modify the comment text
comment.AuthorName = "NewAuthor";

//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("ModifyCommentAuthor.pptx", FileMode.Create);
pptxDoc.Save(outputStream);

//Close the Presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight XAMARIN %}

//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("Sample.pptx");

//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);

//Open a slide to the Presentation
ISlide slide = pptxDoc.Slides[0];

//Get the comment from the slide
IComment comment = slide.Comments[0] as IComment;

//Modify the comment text
comment.AuthorName = "NewAuthor";

//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();

//Save Presentation in stream format.
pptxDoc.Save(stream);

//Close the presentation
pptxDoc.Close();
stream.Position = 0;

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("ModifyCommentAuthor.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("ModifyCommentAuthor.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);

{% endhighlight %}

{% endtabs %}

## Deleting the comment

Deleting a comment will remove all its replies from the PowerPoint slide. You can also delete a particular reply comment from a slide. You can delete a comment by specifying its reference or by specifying its position.
The following code example demonstrates how to delete a comment from a slide.

{% tabs %}

{% highlight c# %}

//Open a PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open("Sample.pptx");

//Get the first slide from the Presentation
ISlide slide = pptxDoc.Slides[0];

//Get a comment from the slide
IComment comment = slide.Comments[0];

//Remove the comment from the slide
slide.Comments.Remove(comment);

//Save the presentation
pptxDoc.Save("DeleteComment.pptx");

//Close the Presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight vb.net %}

'Open a PowerPoint Presentation
Dim pptxDoc As IPresentation = Presentation.Open("Sample.pptx")

'Get the first slide from the Presentation
Dim slide As ISlide = pptxDoc.Slides(0)

'Get a comment from the slide
Dim comment As IComment = slide.Comments(0)

'Remove the comment from the slide
slide.Comments.Remove(comment)

'Save the presentation
pptxDoc.Save("DeleteComment.pptx")

'Close the Presentation
pptxDoc.Close()

{% endhighlight %}

{% highlight UWP %}

//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".pptx");

//Creates a storage file from FileOpenPicker
StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();

//Loads or open an PowerPoint Presentation
IPresentation pptxDoc= await Presentation.OpenAsync(inputStorageFile);

//Get the slide from the Presentation
ISlide slide = pptxDoc.Slides[0];

//Get the comment in the slide
IComment comment = slide.Comments[0] as IComment;

//Remove the comment from the slide
slide.Comments.Remove(comment);

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "DeleteComment";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);

{% endhighlight %}

{% highlight ASP.NET CORE %}

//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream("Sample.pptx",FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);

//Get the first slide from the Presentation
ISlide slide = pptxDoc.Slides[0];

//Get a comment from the slide
IComment comment = slide.Comments[0];

//Remove the comment from the slide
slide.Comments.Remove(comment);

//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("DeleteComment.pptx", FileMode.Create);
pptxDoc.Save(outputStream);

//Close the Presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight XAMARIN %}

//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("Sample.pptx");

//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);

//Get the first slide from the Presentation
ISlide slide = pptxDoc.Slides[0];

//Get a comment from the slide
IComment comment = slide.Comments[0];

//Remove the comment from the slide
slide.Comments.Remove(comment);

//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();

//Save Presentation in stream format.
pptxDoc.Save(stream);

//Close the presentation
pptxDoc.Close();
stream.Position = 0;

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("DeleteComment.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("DeleteComment.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);

{% endhighlight %}

{% endtabs %}
The following code example demonstrates how to delete a comment by specifying its position.

{% tabs %}

{% highlight c# %}

//Open a PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open("Sample.pptx");

//Get the first slide from the Presentation
ISlide slide = pptxDoc.Slides[0];

//Remove the first reply comment from the slide
slide.Comments.RemoveAt(1);

//Save the presentation
pptxDoc.Save("DeleteReplyComment.pptx");

//Close the Presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight vb.net %}

'Open a PowerPoint Presentation
Dim pptxDoc As IPresentation = Presentation.Open("Sample.pptx")

'Get the first slide from the Presentation
Dim slide As ISlide = pptxDoc.Slides(0)

'Remove the first reply comment from the slide
slide.Comments.RemoveAt(1)

'Save the presentation
pptxDoc.Save("DeleteReplyComment.pptx")

'Close the Presentation
pptxDoc.Close()

{% endhighlight %}

{% highlight UWP %}

//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".pptx");

//Creates a storage file from FileOpenPicker
StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();

//Loads or open an PowerPoint Presentation
IPresentation pptxDoc= await Presentation.OpenAsync(inputStorageFile);

//Get the slide from the Presentation
ISlide slide = pptxDoc.Slides[0];

//Remove the first reply comment from the slide
slide.Comments.RemoveAt(1);

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "DeleteReplyComment";
savePicker.FileTypeChoices.Add("PowerPoint Files", new List<string>() { ".pptx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await pptxDoc.SaveAsync(storageFile);

{% endhighlight %}

{% highlight ASP.NET CORE %}

//Loads or open an PowerPoint Presentation
FileStream inputStream = new FileStream("Sample.pptx",FileMode.Open);
IPresentation pptxDoc = Presentation.Open(inputStream);

//Get the first slide from the Presentation
ISlide slide = pptxDoc.Slides[0];

//Remove the first reply comment from the slide
slide.Comments.RemoveAt(1);

//Save the PowerPoint Presentation as stream
FileStream outputStream = new FileStream("DeleteReplyComment.pptx", FileMode.Create);
pptxDoc.Save(outputStream);

//Close the Presentation
pptxDoc.Close();

{% endhighlight %}

{% highlight XAMARIN %}

//"App" is the class of Portable project.
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream("Sample.pptx");

//Loads or open an PowerPoint Presentation
IPresentation pptxDoc = Presentation.Open(inputStream);

//Get the first slide from the Presentation
ISlide slide = pptxDoc.Slides[0];

//Remove the first reply comment from the slide
slide.Comments.RemoveAt(1);

//Create new memory stream to save Presentation.
MemoryStream stream = new MemoryStream();

//Save Presentation in stream format.
pptxDoc.Save(stream);

//Close the presentation
pptxDoc.Close();
stream.Position = 0;

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer presentation/xamarin section for respective code samples.
if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("DeleteReplyComment.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);
else
    Xamarin.Forms.DependencyService.Get<ISave>().Save("DeleteReplyComment.pptx", "application/vnd.openxmlformats-officedocument.presentationml.presentation", stream);

{% endhighlight %}

{% endtabs %}
