---
title: Working with Comments | DocIO | Syncfusion
description: Learn how to add, modify, and remove comments in a Word document using the .NET Word (DocIO) library without Microsoft Word or interop dependencies.
platform: file-formats
control: DocIO
documentation: UG
---
# Working with Comments

A comment is a note or annotation that an author or reviewer can add to a document. DocIO represents comment with [WComment](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WComment.html) instance.

N> The comment start and end ranges and dates can be preserved only on processing an existing document that already contains these information for each comment.

## Adding a Comment

You can add a new comment to the Word document by using [AppendComment](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WParagraph.html#Syncfusion_DocIO_DLS_WParagraph_AppendComment_System_String_) method of [WParagraph](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WParagraph.html) class. 

The following code illustrates how to add a new comment to the document:

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Creates a new Word document
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
//Set the date and time for comment
comment.Format.DateTime = DateTime.Now;
//Saves the Word document to MemoryStream.
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document.
document.Close();
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Creates a new Word document
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
//Set the date and time for comment
comment.Format.DateTime = DateTime.Now;
//Saves and closes the Word document
document.Save("Comment.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Creates a new Word document
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Comments/Add-comment-to-Word-document).

## Modifying a Comment

The following code illustrates how to modify the text of an existing comment in the Word document:

{% tabs %}  

{% highlight c# tabtitle="C# [Cross-platform]" %}
FileStream fileStreamPath = new FileStream("Comment.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);
//Iterates the comments in the Word document
foreach (WComment comment in document.Comments)
{
    //Modifies the last paragraph text of an existing comment when it is added by "Peter"
    if (comment.Format.User == "Peter")
        comment.TextBody.LastParagraph.Text = "Modified Comment Content";
}
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Comments/Modify-text-of-an-existing-comment).

## Inserting comments

You can insert comments into the Word document using the [AppendComment](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WParagraph.html#Syncfusion_DocIO_DLS_WParagraph_AppendComment_System_String_) and [AddCommentedItem](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WComment.html#Syncfusion_DocIO_DLS_WComment_AddCommentedItem_Syncfusion_DocIO_DLS_IParagraphItem_) methods.

The following code example illustrates how to find all occurrences of a text pattern using Regex and insert comments to them.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

using (FileStream fileStream = new FileStream("Input.docx", FileMode.Open, FileAccess.ReadWrite))
{
    //Open the existing Word document.
    using (WordDocument document = new WordDocument(fileStream, FormatType.Docx))
    {
        //Find all occurrence of a particular text ending with comma in the document using regex.
        TextSelection[] textSelection = document.FindAll(new Regex("\\w+,"));
        if (textSelection != null)
        {
            //Iterates through each occurrence and comment it.
            for (int i = 0; i < textSelection.Count(); i++)
            {
                //Get the found text as a single text range.
                WTextRange textRange = textSelection[i].GetAsOneRange();
                //Get the owner paragraph of the found text.
                WParagraph paragraph = textRange.OwnerParagraph;
                //Get the index of the found text.
                int textIndex = paragraph.ChildEntities.IndexOf(textRange);
                //Add comment to a paragraph.
                WComment comment = paragraph.AppendComment("comment test_" + i);
                //Specify the author of the comment.
                comment.Format.User = "Peter";
                //Specify the initial of the author.
                comment.Format.UserInitials = "St";
                //Set the date and time for the comment.
                comment.Format.DateTime = DateTime.Now;
                //Insert the comment next to the textrange.
                paragraph.ChildEntities.Insert(textIndex + 1, comment);
                //Add the paragraph items to the commented items.
                comment.AddCommentedItem(textRange);
            }
        }
        //Create the file stream.
        using (FileStream outputFileStream = new FileStream("Result.docx", FileMode.Create, FileAccess.ReadWrite))
        {
            //Save the Word document to the file stream.
            document.Save(outputFileStream, FormatType.Docx);
        }
    }               
}

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

//Open the existing Word document.
using (WordDocument document = new WordDocument("Input.docx", FormatType.Docx))
{
    //Find all occurrence of a particular text ending with comma in the document using regex.
    TextSelection[] textSelection = document.FindAll(new Regex("\\w+,"));
    if (textSelection != null)
    {
        //Iterates through each occurrence and comment it.
        for (int i = 0; i < textSelection.Count(); i++)
        {
            //Get the found text as a single text range.
            WTextRange textRange = textSelection[i].GetAsOneRange();
            //Get the owner paragraph of the found text.
            WParagraph paragraph = textRange.OwnerParagraph;
            //Get the index of the found text.
            int textIndex = paragraph.ChildEntities.IndexOf(textRange);
            //Add comment to a paragraph.
            WComment comment = paragraph.AppendComment("comment test_" + i);
            //Specify the author of the comment.
            comment.Format.User = "Peter";
            //Specify the initial of the author.
            comment.Format.UserInitials = "St";
            //Set the date and time for the comment.
            comment.Format.DateTime = DateTime.Now;
            //Insert the comment next to the textrange.
            paragraph.ChildEntities.Insert(textIndex + 1, comment);
            //Add the paragraph items to the commented items.
            comment.AddCommentedItem(textRange);
            //Save the Word document.
            document.Save("Result.docx");
        }
    }
}

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

Using document As New WordDocument("Input.docx", FormatType.Docx)
    ' Find all occurrences of a particular text ending with a comma in the document using regex.
    Dim textSelection As TextSelection() = document.FindAll(New Regex("\w+,"))
    If textSelection IsNot Nothing Then
        ' Iterate through each occurrence and add a comment.
        For i As Integer = 0 To textSelection.Count() - 1
            ' Get the found text as a single text range.
            Dim textRange As WTextRange = textSelection(i).GetAsOneRange()
            ' Get the owner paragraph of the found text.
            Dim paragraph As WParagraph = textRange.OwnerParagraph
            ' Get the index of the found text.
            Dim textIndex As Integer = paragraph.ChildEntities.IndexOf(textRange)
            ' Add a comment to a paragraph.
            Dim comment As WComment = paragraph.AppendComment("comment test_" & i)
            ' Specify the author of the comment.
            comment.Format.User = "Peter"
            ' Specify the initials of the author.
            comment.Format.UserInitials = "St"
            ' Set the date and time for the comment.
            comment.Format.DateTime = DateTime.Now
            ' Insert the comment next to the text range.
            paragraph.ChildEntities.Insert(textIndex + 1, comment)
            ' Add the paragraph items to the commented items.
            comment.AddCommentedItem(textRange)
        Next
        ' Save the Word document.
        document.Save("Result.docx")
    End If
End Using

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Comments/Find-text-and-insert-comment).

## Removing Comments

You can either remove all the comments or a particular comment from the Word document.

The following code illustrates how to remove all the comments in Word document.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
FileStream fileStreamPath = new FileStream("Comment.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);
//Removes all the comments in a Word document
document.Comments.Clear();
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
WordDocument document = new WordDocument("Comment.docx");
//Removes all the comments in a Word document
document.Comments.Clear();
document.Save("Result.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Dim document As New WordDocument("Comment.docx")
'Removes all the comments in a Word document
document.Comments.Clear()
document.Save("Result.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Comments/Remove-all-comments-in-Word-document).

The following code illustrates how to remove a particular comment from Word document.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
FileStream fileStreamPath = new FileStream("Comment.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);
//Removes second comments from a document.
document.Comments.RemoveAt(1);
//Saves the Word document to  MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
WordDocument document = new WordDocument("Comment.docx");
//Removes second comments from a document.
document.Comments.RemoveAt(1);
//Saves and closes the Word document
document.Save("Result.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Dim document As New WordDocument("Comment.docx")
'Removes second comments from a document.
document.Comments.RemoveAt(1)
'Saves and closes the Word document
document.Save("Result.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Comments/Remove-particular-comment-from-Word).

## Accessing parent comment

You can access the parent comment of a particular comment (reply) in a Word document using [Ancestor](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WComment.html#Syncfusion_DocIO_DLS_WComment_Ancestor) API. The ancestor for parent comment returns `null` as default.

The following code examples show how to access the parent comment of a particular comment in a Word document.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
FileStream fileStreamPath = new FileStream("Comment.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);
// Get the Ancestor comment.
document.Comments[1].Ancestor;
//Save the Word document to  MemoryStream.
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Close the document.
document.Close();
stream.Position = 0;
//Download the Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Load an existing Word document into DocIO instance.
WordDocument document = new WordDocument("Comment.docx");
//Get the Ancestor comment.
WComment ancestorComment = document.Comments[1].Ancestor;
//Save and Close the Word document.
document.Save("Result.docx", FormatType.Docx);
document.Close();

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Load an existing Word document into DocIO instance.
Dim document As WordDocument = New WordDocument("Comment.docx")
'Get the Ancestor comment.
Dim ancestorComment As WComment = document.Comments[1].Ancestor
'Save and Close the Word document.
document.Save("Result.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Comments/Access-parent-comment).

## Retrieve the commented word or items

The following code example illustrates how to get the paragraph item where it exists in the commented region based on the existing comment in the Word document.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
FileStream fileStreamPath = new FileStream("Comment.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
using(WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx))
{
    //Iterate the comments in the Word document.
    foreach (WComment comment in document.Comments)
    {
        //Get the commented word or part of a particular comment.
        if (comment.TextBody.LastParagraph.Text == "This is the second comment.")
            ParagraphItemCollection paragraphItem = comment.CommentedItems;
    }
    //Save the Word document to MemoryStream.
    MemoryStream stream = new MemoryStream();
    document.Save(stream, FormatType.Docx);
    stream.Position = 0;
    //Download the Word document in the browser.
    return File(stream, "application/msword", "Result.docx");
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using(WordDocument document = new WordDocument("Comment.docx"))
{
    //Iterate the comments in the Word document.
    foreach (WComment comment in document.Comments)
    {
        //Get the commented word or part of a particular comment.
        if (comment.TextBody.LastParagraph.Text == "This is the second comment.")
            ParagraphItemCollection paragraphItem = comment.CommentedItems;
    }
    document.Save("Result.docx", FormatType.Docx);
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using document As New WordDocument("Comment.docx")
    'Iterate the comments in the Word document.
    For Each comment As WComment In document.Comments
        If comment.TextBody.LastParagraph.Text = "This is the second comment." Then
            Dim paragraphItem As ParagraphItemCollection = comment.CommentedItems
        End If
    Next
    document.Save("Result.docx", FormatType.Docx)
End Using
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Comments/Retrieve-commented-word).

## See Also

* [How to check if a comment is resolved or not in a Word document?](https://support.syncfusion.com/kb/article/14652/how-to-check-if-comment-is-resolved-or-not-in-word-document)