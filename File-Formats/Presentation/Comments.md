---

title: Working with comments in PowerPoint presentation
description: Working with comments in PowerPoint presentation.
platform: file-formats
control: Presentation
documentation: UG
keywords: comments
---
# Working with Comments
A comment is a text note attached to a location on a slide. Each comment contains an unformatted text string, information about its author and the time it was added.

## Adding a comment
The following code example demonstrates how to add a comment in a slide.
{% tabs %}
{% highlight c# %}
//Create a PowerPoint Presentation
IPresentation presentationDoc = Presentation.Create();
//Add a slide to the Presentation
ISlide slide = presentationDoc.Slides.Add(SlideLayoutType.Blank);
//Add a comment to the slide
slide.Comments.Add(10, 10, "Author1", "A1", "Can we change the font size to 20?", DateTime.Now);
//Save the Presentation
presentationDoc.Save("Comment.pptx");
//Close the Presentation
presentationDoc.Close();
{% endhighlight %}
{% highlight vb.net %}
'Create a PowerPoint Presentation
Dim presentationDoc As IPresentation = Presentation.Create()
'Add a slide to the Presentation
Dim slide As ISlide = presentationDoc.Slides.Add(SlideLayoutType.Blank)
'Add a comment to the slide
slide.Comments.Add(10, 10, "Author1", "A1", "Can we change the font size to 20?", DateTime.Now)
'Save the Presentation
presentationDoc.Save("Comment.pptx")
'Close the Presentation
presentationDoc.Close()
{% endhighlight %}
{% endtabs %}
## Replying to a comment
The following code example demonstrates how to reply to an existing comment in a slide.
{% tabs %}
{% highlight c# %}
//Create a PowerPoint Presentation
IPresentation presentationDoc = Presentation.Open("Sample.pptx");
//Get the slide from the Presentation
ISlide slide = presentationDoc.Slides[0];
//Get the comment in the slide
IComment comment = slide.Comments[0] as IComment;
//Add reply to the comment
slide.Comments.Add("Author2", "A2", "Yes, we can we change the font size to 20", DateTime.Now, comment);
//Save the presentation
presentationDoc.Save("ReplyComment.pptx");
//Close the Presentation
presentationDoc.Close();
{% endhighlight %}
{% highlight vb.net %}
'Create a PowerPoint Presentation
Dim presentationDoc As IPresentation = Presentation.Open("Sample.pptx")
'Get the slide from the Presentation
Dim slide As ISlide = presentationDoc.Slides(0)
'Get the comment in the slide
Dim comment As IComment = TryCast(slide.Comments(0), IComment)
'Add reply to the comment
slide.Comments.Add("Author2", "A2", "Yes, we can we change the font size to 20", DateTime.Now, comment)
'Save the presentation
presentationDoc.Save("ReplyComment.pptx")
'Close the Presentation
presentationDoc.Close()
{% endhighlight %}
{% endtabs %}
## Modifying the comment
The following code example demonstrates how to modify the content of a comment.
{% tabs %}
{% highlight c# %}
//Create a PowerPoint Presentation
IPresentation presentationDoc = Presentation.Open("Sample.pptx");
//Open a slide to the Presentation
ISlide slide = presentationDoc.Slides[0];
//Get the comment from the slide
IComment comment = slide.Comments[0] as IComment;
//Modify the comment text
comment.Text = "The comment text content is changed";
//Save the presentation
presentationDoc.Save("ModifyCommentText.pptx");
//Close the Presentation
presentationDoc.Close();
{% endhighlight %}
{% highlight vb.net %}
'Create a PowerPoint Presentation
Dim presentationDoc As IPresentation = Presentation.Open("Sample.pptx")
'Open a slide to the Presentation
Dim slide As ISlide = presentationDoc.Slides(0)
'Get the comment from the slide
Dim comment As IComment = TryCast(slide.Comments(0), IComment)
'Modify the comment text
comment.Text = "The comment text content is changed"
'Save the presentation
presentationDoc.Save("ModifyCommentText.pptx")
'Close the Presentation
presentationDoc.Close()
{% endhighlight %}
{% endtabs %}
The following code example demonstrates how to modify the author name of a comment.
{% tabs %}
{% highlight c# %}
//Create a PowerPoint Presentation
IPresentation presentationDoc = Presentation.Open("Sample.pptx");
//Open a slide to the Presentation
ISlide slide = presentationDoc.Slides[0];
//Get the comment from the slide
IComment comment = slide.Comments[0] as IComment;
//Modify the comment text
comment.AuthorName = "NewAuthor";
//Save the presentation
presentationDoc.Save("ModifyCommentAuthor.pptx");
//Close the Presentation
presentationDoc.Close();
{% endhighlight %}
{% highlight vb.net %}
'Create a PowerPoint Presentation
Dim presentationDoc As IPresentation = Presentation.Open("Sample.pptx")
'Open a slide to the Presentation
Dim slide As ISlide = presentationDoc.Slides(0)
'Get the comment from the slide
Dim comment As IComment = TryCast(slide.Comments(0), IComment)
'Modify the comment text
comment.AuthorName = "NewAuthor"
'Save the presentation
presentationDoc.Save("ModifyCommentAuthor.pptx")
'Close the Presentation
presentationDoc.Close()
{% endhighlight %}
{% endtabs %}
## Deleting the comment
Deleting a comment will remove all its replies from the PowerPoint slide. You can also delete a particular reply comment from a slide. You can delete a comment by specifying its reference or by specifying its position. The parent comment will be at index 0 and the reply comments will hold the incremental index positions. 
The following code example demonstrates how to delete a comment from a slide.
{% tabs %}
{% highlight c# %}
//Open a PowerPoint Presentation
IPresentation presentationDoc = Presentation.Open("Sample.pptx");
//Get the first slide from the Presentation
ISlide slide = presentationDoc.Slides[0];
//Get a comment from the slide
IComment comment = slide.Comments[0];
//Remove the comment from the slide
slide.Comments.Remove(comment);
//Save the presentation
presentationDoc.Save("DeleteComment.pptx");
//Close the Presentation
presentationDoc.Close();
{% endhighlight %}
{% highlight vb.net %}
'Open a PowerPoint Presentation
Dim presentationDoc As IPresentation = Presentation.Open("Sample.pptx")
'Get the first slide from the Presentation
Dim slide As ISlide = presentationDoc.Slides(0)
'Get a comment from the slide
Dim comment As IComment = slide.Comments(0)
'Remove the comment from the slide
slide.Comments.Remove(comment)
'Save the presentation
presentationDoc.Save("DeleteComment.pptx")
'Close the Presentation
presentationDoc.Close()
{% endhighlight %}
{% endtabs %}
The following code example demonstrates how to delete a comment by specifying its position.
{% tabs %}
{% highlight c# %}
//Open a PowerPoint Presentation
IPresentation presentationDoc = Presentation.Open("Sample.pptx");
//Get the first slide from the Presentation
ISlide slide = presentationDoc.Slides[0];
//Remove the first reply comment from the slide
slide.Comments.RemoveAt(1);
//Save the presentation
presentationDoc.Save("DeleteReplyComment.pptx");
//Close the Presentation
presentationDoc.Close();
{% endhighlight %}
{% highlight vb.net %}
'Open a PowerPoint Presentation
Dim presentationDoc As IPresentation = Presentation.Open("Sample.pptx")
'Get the first slide from the Presentation
Dim slide As ISlide = presentationDoc.Slides(0)
'Remove the first reply comment from the slide
slide.Comments.RemoveAt(1)
'Save the presentation
presentationDoc.Save("DeleteReplyComment.pptx")
'Close the Presentation
presentationDoc.Close()
{% endhighlight %}
{% endtabs %}
