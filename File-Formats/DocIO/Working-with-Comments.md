---
title: Working with Comments
description: This section illustrates how to add, modify and remove the comments
platform: file-formats
control: DocIO
documentation: UG
---
# Working with Comments

A comment is a note or annotation that an author or reviewer can add to a document. DocIO represents comment with `WComment` instance.

N>  The comment start and end ranges and dates can be preserved only on processing an existing document that already contains these information for each comment.

## Adding a Comment

You can add a new comment to the Word document by using `AppendComment` method of `WParagraph` class. 

The following code illustrates how to add a new comment to the document:

{% tabs %}  

{% highlight c# %}


//Creates a new Word document.

WordDocument document = new WordDocument();

//Adds a section and a paragraph in the document

document.EnsureMinimal();

IWParagraph paragraph = document.LastParagraph;

//Appends text to the paragraph

paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");

//Adds comment to a paragraph

WComment comment = paragraph.AppendComment("comment test");

//Specifies the author of the comment

comment.Format.User = "Peter";

//Specifies the initial of the author

comment.Format.UserInitials = "St";

//Saves and closes the Word document

document.Save("Comment.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vb.net %}


'Creates a new Word document.

Dim document As New WordDocument()

'Adds a section and a paragraph in the document

document.EnsureMinimal()

Dim paragraph As IWParagraph = document.LastParagraph

'Appends text to the paragraph

paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.")

'Adds comment to a paragraph

Dim comment As WComment = paragraph.AppendComment("comment test")

'Specifies the author of the comment

comment.Format.User = "Peter"

'Specifies the initial of the author

comment.Format.UserInitials = "St"

'Saves and closes the Word document

document.Save("Comment.docx", FormatType.Docx)

document.Close()

{% endhighlight %} 

 {% endtabs %}  

 
 
## Modifying a Comment

The following code illustrates how to modify the text of an existing comment in the Word document:

{% tabs %}  

{% highlight c# %}


WordDocument document = new WordDocument("Comment.docx");

//Iterates the comments in the Word document

foreach (WComment comment in document.Comments)

{

//Modifies the last paragraph text of an existing comment when it is added by "Peter"

if (comment.Format.User == "Peter")

comment.TextBody.LastParagraph.Text = "Modified Comment Content";

}

document.Save("ModifiedComment.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vb.net %}


Dim document As New WordDocument("Comment.docx")

'Iterates the comments in the Word document

For Each comment As WComment In document.Comments

'Modifies the last paragraph text of an existing comment when it is added by "Peter"

If comment.Format.User = "Peter" Then

comment.TextBody.LastParagraph.Text = "Modified Comment Content"

End If

Next

document.Save("ModifiedComment.docx", FormatType.Docx)

document.Close()

{% endhighlight %}

  {% endtabs %}  

  
## Removing Comments

You can either remove all the comments or a particular comment from the Word document.

The following code illustrates how to remove all the comments in Word document.

{% tabs %}  

{% highlight c# %}


WordDocument document = new WordDocument("Comment.docx");

//Removes all the comments in a Word document

document.Comments.Clear();

document.Save("Result.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vb.net %}


Dim document As New WordDocument("Comment.docx")

'Removes all the comments in a Word document

document.Comments.Clear()

document.Save("Result.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

{% endtabs %}  

The following code illustrates how to remove a particular comment from Word document.

{% tabs %} 

{% highlight c# %}


WordDocument document = new WordDocument("Comment.docx");

//Removes second comments from a document.

document.Comments.RemoveAt(1);

//Saves and closes the Word document

document.Save("Result.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vb.net %}


Dim document As New WordDocument("Comment.docx")

'Removes second comments from a document.

document.Comments.RemoveAt(1)

'Saves and closes the Word document

document.Save("Result.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

 {% endtabs %}  