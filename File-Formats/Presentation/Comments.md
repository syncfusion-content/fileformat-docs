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

{% highlight c# tabtitle="C# [Cross-platform]" %}
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

{% highlight c# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Comments/Add-comments-in-PowerPoint).

## Replying to a comment
The following code example demonstrates how to reply to an existing comment in a slide.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
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

{% highlight c# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Comments/Add-reply-comment-in-PowerPoint).

## Modifying the comment
The following code example demonstrates how to modify the content of a comment.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
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

{% highlight c# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Comments/Modify-comment-content).

The following code example demonstrates how to modify the author name of a comment.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
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

{% highlight c# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Comments/Modify-comment-author).

## Deleting the comment

Deleting a comment will remove all its replies from the PowerPoint slide. You can also delete a particular reply comment from a slide. You can delete a comment by specifying its reference or by specifying its position.

The following code example demonstrates how to delete a comment from a slide.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
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

{% highlight c# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Comments/Delete-comment).

The following code example demonstrates how to delete a comment by specifying its position.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
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

{% highlight c# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PowerPoint-Examples/tree/master/Comments/Delete-comment-by-position).