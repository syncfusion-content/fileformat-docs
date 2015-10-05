---
layout: Post
title: Working with Comments
description: This section illustrates how to add, modify and remove the comments
platform: FileFormat
control: DocIO
documentation: UG
---
# Working with Comments

A comment is a note or annotation that an author or reviewer can add to a document. DocIO represents comment with **WComment** instance.

Note: The comment start and end range and date can be preserved only on processing an existing document which already contains these information for each comment.

## Adding a Comment

You can add a new comment to the Word document by using **AppendComment** method of **WParagraph** class. 

The following code illustrates how to add a new comment to the document:

{% highlight c# %}
[C#]

//Creates a new Word document.

WordDocument document = new WordDocument();

//Add a section & a paragraph in the document

document.EnsureMinimal();

IWParagraph paragraph = document.LastParagraph;

//Append text to the paragraph

paragraph.AppendText("Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua");

//Add comment to a parahraph

WComment comment = paragraph.AppendComment("comment test");

//Specify the author of the comment

comment.Format.User = "Peter";

//Specify the initial of the author

comment.Format.UserInitials = "St";

//Save and close the Word document

document.Save("Comment.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB]

'Creates a new Word document.

Dim document As New WordDocument()

'Add a section & a paragraph in the document

document.EnsureMinimal()

Dim paragraph As IWParagraph = document.LastParagraph

'Append text to the paragraph

paragraph.AppendText("Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua")

'Add comment to a parahraph

Dim comment As WComment = paragraph.AppendComment("comment test")

'Specify the author of the comment

comment.Format.User = "Peter"

'Specify the initial of the author

comment.Format.UserInitials = "St"

'Save and close the Word document

document.Save("Comment.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

## Modifying a Comment

The following code illustrates how to modify the text of an existing comment in the Word document:

{% highlight c# %}
[C#]

WordDocument document = new WordDocument("Comment.docx");

//Iterate the comments in the Word document

foreach (WComment comment in document.Comments)

{

//Modify the last paragraph text of an existing comment if it is added by "Peter"

if (comment.Format.User == "Peter")

comment.TextBody.LastParagraph.Text = "Modified Comment Content";

}

document.Save("ModifiedComment.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB]

Dim document As New WordDocument("Comment.docx")

'Iterate the comments in the Word document

For Each comment As WComment In document.Comments

'Modify the last paragraph text of an existing comment if it is added by "Peter"

If comment.Format.User = "Peter" Then

comment.TextBody.LastParagraph.Text = "Modified Comment Content"

End If

Next

document.Save("ModifiedComment.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

## Removing Comments

You can either remove all the comments or a particular comment from the Word document.

The following code illustrates how to remove all the comments in Word document.

{% highlight c# %}
[C#]

WordDocument document = new WordDocument("Comment.docx");

//Remove all the comments in a Word document

document.Comments.Clear();

document.Save("Result.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB]

Dim document As New WordDocument("Comment.docx")

'Remove all the comments in a Word document

document.Comments.Clear()

document.Save("Result.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

The following code illustrates how to remove a particular comment from Word document.

{% highlight c# %}
[C#]

WordDocument document = new WordDocument("Comment.docx");

//Remove second comments from a document.

document.Comments.RemoveAt(1);

//Save and close the Word document

document.Save("Result.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB]

Dim document As New WordDocument("Comment.docx")

'Remove second comments from a document.

document.Comments.RemoveAt(1)

'Save and close the Word document

document.Save("Result.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

