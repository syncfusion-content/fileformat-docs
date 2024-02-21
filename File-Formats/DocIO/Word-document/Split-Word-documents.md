---
title: Split Word documents in C# | DocIO | Syncfusion
description: Learn how to split a large Word document into several smaller ones using .NET Word (DocIO) library without Microsoft Word or interop dependencies.
platform: file-formats
control: DocIO
documentation: UG
---
# Split Word documents

Syncfusion Word Library allows you to split the large Word document into number of smaller word documents by the sections, headings, bookmarks, and placeholder text in programmatically. 

By using this feature, you can be able to split/extract the necessary parts from the original document for further processing.

You can save the resultant document as a Word document (DOCX, WordML, DOC), PDF, image, HTML, RTF, and more.

To quickly start splitting Word documents, please check out this video:
{% youtube "https://www.youtube.com/watch?v=w9np2NSfq94" %}

## Split by Section

The following code example illustrates how to split the Word document by sections.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
FileStream fileStreamPath = new FileStream("Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
//Load the template document as stream
using(WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx))
{
    int i = 0;
    //Iterate each section from Word document
    foreach (WSection section in document.Sections)
    {
        //Create new Word document
        WordDocument newDocument = new WordDocument();
        //Add cloned section into new Word document
        newDocument.Sections.Add(section.Clone());
        //Saves the Word document to  MemoryStream
        FileStream outputStream = new FileStream("Section" + i + ".docx", FileMode.OpenOrCreate, FileAccess.ReadWrite);
        newDocument.Save(outputStream, FormatType.Docx);
        //Closes the document
        newDocument.Close();
        i++;
    }
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Load the template document
using (WordDocument document = new WordDocument(@"Template.docx"))
{
    int i = 0;
    //Iterate each section from Word document
    foreach (WSection section in document.Sections)
    {
        //Create new Word document
        WordDocument newDocument = new WordDocument();
        //Add cloned section into new Word document
        newDocument.Sections.Add(section.Clone());
        //Save and close the new Word documet
        newDocument.Save("Section" + i + ".docx");
        newDocument.Close();
        i++;
    }
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Load the template document
Using document As WordDocument = New WordDocument("Template.docx")
    Dim i As Integer = 0
    'Iterate each section from Word document
    For Each section As WSection In document.Sections
        'Create new Word document
        Dim newDocument As WordDocument = New WordDocument()
        'Add cloned section into new Word document
        newDocument.Sections.Add(section.Clone())
        'Save and close the new Word documet
        newDocument.Save("Section" & i & ".docx")
        newDocument.Close()
        i += 1
    Next
End Using
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-document/Split-by-section).

## Split by Headings

The following code example illustrates how to split the Word document by using headings.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
using (FileStream inputStream = new FileStream("Template.docx", FileMode.Open, FileAccess.Read))
{
    //Load the template document as stream
    using (WordDocument document = new WordDocument(inputStream, FormatType.Docx))
    {
        WordDocument newDocument = null;
        WSection newSection = null;
        int i = 0;
        //Iterate each section from Word document
        foreach (WSection section in document.Sections)
        {
            if (newDocument != null)
                newSection = AddSection(newDocument, section);
            foreach (TextBodyItem textbodyitem in section.Body.ChildEntities)
            {
                if (textbodyitem is WParagraph)
                {
                    WParagraph para = textbodyitem as WParagraph;
                    if (para.StyleName == "Heading 1")
                    {
                        if (newDocument != null)
                        {
                            //Saves the Word document
                            string fileName = "Heading" + i + ".docx";
                            SaveWordDocument(newDocument, fileName);
                            i++;
                        }
                        //Create new Word document
                        newDocument = new WordDocument();
                        newSection = AddSection(newDocument, section);
                        //Add cloned paragraphs into new section
                        AddEntity(newSection, para);
                    }
                    else if (newDocument != null)
                        //Add cloned paragraphs into new section
                        AddEntity(newSection, para);
                }
                else
                    //Add cloned item into new section
                    AddEntity(newSection, textbodyitem);
            }
        }
        if (newDocument != null)
        {
            //Saves the Word document
            string fileName = "Heading" + i + ".docx";
            SaveWordDocument(newDocument, fileName);
        }
    }
}

private static WSection AddSection(WordDocument newDocument, WSection section)
{
    //Create new session based on original document
    WSection newSection = section.Clone();
    newSection.Body.ChildEntities.Clear();
    //Remove the first page header.
    newSection.HeadersFooters.FirstPageHeader.ChildEntities.Clear();
    //Remove the first page footer.
    newSection.HeadersFooters.FirstPageFooter.ChildEntities.Clear();
    //Remove the odd footer.
    newSection.HeadersFooters.OddFooter.ChildEntities.Clear();
    //Remove the odd header.
    newSection.HeadersFooters.OddHeader.ChildEntities.Clear();
    //Remove the even header.
    newSection.HeadersFooters.EvenHeader.ChildEntities.Clear();
    //Remove the even footer.
    newSection.HeadersFooters.EvenFooter.ChildEntities.Clear();
    //Add cloned section into new document
    newDocument.Sections.Add(newSection);
    return newSection;
}

private static void AddEntity(WSection newSection, Entity entity)
{
    //Add cloned item into the newly created section
    newSection.Body.ChildEntities.Add(entity.Clone());
}

private static void SaveWordDocument(WordDocument newDocument, string fileName)
{
    using (FileStream outputStream = new FileStream(fileName, FileMode.OpenOrCreate, FileAccess.ReadWrite))
    {
        //Save file stream as Word document
        newDocument.Save(outputStream, FormatType.Docx);
        //Closes the document
        newDocument.Close();
        newDocument = null;
    }
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Load the template document
using (WordDocument doc = new WordDocument("Template.docx"))
{
    WordDocument newDocument = null;
    WSection newSection = null;
    int i = 1;
    //Iterate each section from Word document
    foreach (WSection section in doc.Sections)
    {
        if (newDocument != null)
            newSection = AddSection(newDocument, section);
        foreach (TextBodyItem textbodyitem in section.Body.ChildEntities)
        {
            if (textbodyitem is WParagraph)
            {
                WParagraph para = textbodyitem as WParagraph;
                // Check whether the paragraph has heading style or normal style
                if (para.StyleName == "Heading 1")
                {
                    if (newDocument != null)
                    {
                        string fileName = "Heading" + i + ".docx";
                        //Saves the Word document
                        SaveWordDocument(newDocument, fileName);
                        i++;
                    }
                    //Create new Word document
                    newDocument = new WordDocument();
                    newSection = AddSection(newDocument, section);
                    //Add cloned paragraphs into new section
                    AddEntity(newSection, para);
                }
                else if (newDocument != null)
                    //Add cloned paragraphs into new section
                    AddEntity(newSection, para);
            }
            else
                //Add cloned item into new section
                AddEntity(newSection, textbodyitem);
        }
    }
    if (newDocument != null)
    {
        string fileName = "Heading" + i + ".docx";
        //Saves the Word document
        SaveWordDocument(newDocument, fileName);
    }
}

private static WSection AddSection(WordDocument newDocument, WSection section)
{
    //Create new session based on original document
    WSection newSection = section.Clone();
    newSection.Body.ChildEntities.Clear();
    //Remove the first page header.
    newSection.HeadersFooters.FirstPageHeader.ChildEntities.Clear();
    //Remove the first page footer.
    newSection.HeadersFooters.FirstPageFooter.ChildEntities.Clear();
    //Remove the odd footer.
    newSection.HeadersFooters.OddFooter.ChildEntities.Clear();
    //Remove the odd header.
    newSection.HeadersFooters.OddHeader.ChildEntities.Clear();
    //Remove the even header.
    newSection.HeadersFooters.EvenHeader.ChildEntities.Clear();
    //Remove the even footer.
    newSection.HeadersFooters.EvenFooter.ChildEntities.Clear();
    //Add cloned section into new document
    newDocument.Sections.Add(newSection);
    return newSection;
}

private static void AddEntity(WSection newSection, Entity entity)
{
    //Add cloned item into the newly created section
    newSection.Body.ChildEntities.Add(entity.Clone());
}

private static void SaveWordDocument(WordDocument newDocument, string fileName)
{
    //Save file stream as Word document
    newDocument.Save(fileName, FormatType.Docx);
    //Closes the document
    newDocument.Close();
    newDocument = null;
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Load the template document
Using doc As WordDocument = New WordDocument("Template.docx")
    Dim newDocument As WordDocument = Nothing
    Dim newSection As WSection = Nothing
    Dim i As Integer = 1
    'Iterate each section from Word document
    For Each section As WSection In doc.Sections
        If newDocument IsNot Nothing Then
            newSection = AddSection(newDocument, section)
        End If
        For Each textbodyitem As TextBodyItem In section.Body.ChildEntities
            If TypeOf textbodyitem Is WParagraph Then
                Dim para As WParagraph = TryCast(textbodyitem, WParagraph)
                'Check whether the paragraph has heading style or normal style
                If para.StyleName = "Heading 1" Then
                    If newDocument IsNot Nothing Then
                        'Save and close the new Word documet
                        Dim fileName As String = "Heading" & i & ".docx"
                        SaveWordDocument(newDocument, fileName)
                        i += 1
                    End If
                    'Create new Word document
                    newDocument = New WordDocument()
                    newSection = AddSection(newDocument, section)
                    AddEntity(newSection, para)
                ElseIf newDocument IsNot Nothing Then
                    'Add cloned paragraphs into new section
                    AddEntity(newSection, para)
                End If
            Else
                'Add cloned items into new section
                AddEntity(newSection, textbodyitem)
            End If
        Next
    Next

    If newDocument IsNot Nothing Then
        'Save and close the new Word documet
        Dim fileName As String = "Heading" & i & ".docx"
        SaveWordDocument(newDocument, fileName)
    End If
End Using

Private Function AddSection(ByVal newDocument As WordDocument, ByVal section As WSection) As WSection
    Dim newSection As WSection = section.Clone()
    newSection.Body.ChildEntities.Clear()
    newSection.HeadersFooters.FirstPageHeader.ChildEntities.Clear()
    newSection.HeadersFooters.FirstPageFooter.ChildEntities.Clear()
    newSection.HeadersFooters.OddFooter.ChildEntities.Clear()
    newSection.HeadersFooters.OddHeader.ChildEntities.Clear()
    newSection.HeadersFooters.EvenHeader.ChildEntities.Clear()
    newSection.HeadersFooters.EvenFooter.ChildEntities.Clear()
    newDocument.Sections.Add(newSection)
    Return newSection
End Function

Private Sub AddEntity(ByVal newSection As WSection, ByVal entity As Entity)
    newSection.Body.ChildEntities.Add(entity.Clone())
End Sub

Private Sub SaveWordDocument(ByVal newDocument As WordDocument, ByVal fileName As String)
    newDocument.Save(fileName, FormatType.Docx)
    newDocument.Close()
    newDocument = Nothing
End Sub
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-document/Split-by-heading).

## Split by Bookmark

The following code example illustrates how to split the Word document using bookmarks.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Load an existing Word document.
FileStream fileStreamPath = new FileStream("Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
using (WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx))
{
    //Create a bookmark navigator instance to access the bookmark.
    BookmarksNavigator bookmarkNavigator = new BookmarksNavigator(document);
    //Get the bookmark collections in the document.
    BookmarkCollection bookmarkCollection = document.Bookmarks;
    foreach (Bookmark bookmark in bookmarkCollection)
    {
        //Move the virtual cursor to the location before the end of the bookmark.
        bookmarkNavigator.MoveToBookmark(bookmark.Name);
        //Get the bookmark content.
        TextBodyPart part = bookmarkNavigator.GetBookmarkContent();
        //Create a new Word document.
        WordDocument newDocument = new WordDocument();
        newDocument.AddSection();
        //Add the retrieved content to another new document.
        for (int i = 0; i < part.BodyItems.Count; i++)
            newDocument.LastSection.Body.ChildEntities.Add(part.BodyItems[i].Clone());
        using (FileStream outputFileStream = new FileStream(Path.GetFullPath(@"Result" + bookmark.Name + ".docx"), FileMode.Create, FileAccess.ReadWrite))
        {
            //Saves the Word document to file stream.
            newDocument.Save(outputFileStream, FormatType.Docx);
        }
    }
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Load an existing Word document.
using (WordDocument document = new WordDocument("Template.docx", FormatType.Docx))
{
    //Create a bookmark navigator instance to access the bookmark.
    BookmarksNavigator bookmarkNavigator = new BookmarksNavigator(document);
    //Get the bookmark collections in the document.
    BookmarkCollection bookmarkCollection =  document.Bookmarks;
    foreach (Bookmark bookmark in bookmarkCollection)
    {
        //Move the virtual cursor to the location before the end of the bookmark.
        bookmarkNavigator.MoveToBookmark(bookmark.Name);
        //Get the bookmark content.
        TextBodyPart part = bookmarkNavigator.GetBookmarkContent();
        //Create a new Word document.
        WordDocument newDocument = new WordDocument();
        newDocument.AddSection();
        //Add the retrieved content to another new document.
        for (int i = 0; i < part.BodyItems.Count; i++)
            newDocument.LastSection.Body.ChildEntities.Add(part.BodyItems[i].Clone());
        //Save the Word document.
        newDocument.Save(@"Result"+ bookmark.Name + ".docx", FormatType.Docx);
        newDocument.Close();
    }
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Load an existing Word document.
Using document As WordDocument = New WordDocument("Template.docx", FormatType.Docx)
    'Create a bookmark navigator instance to access the bookmark.
    Dim bookmarkNavigator As BookmarksNavigator = New BookmarksNavigator(document)
    'Get the bookmark collections in the document.
    Dim bookmarkCollection As BookmarkCollection = document.Bookmarks
    For Each bookmark As Bookmark In bookmarkCollection
        'Move the virtual cursor to the location before the end of the bookmark.
        bookmarkNavigator.MoveToBookmark(bookmark.Name)
        'Get the bookmark content.
        Dim part As TextBodyPart = bookmarkNavigator.GetBookmarkContent()
        'Create a new Word document.
        Dim newDocument As WordDocument = New WordDocument()
        newDocument.AddSection()
        'Add the retrieved content to another new document.
        For i As Integer = 0 To part.BodyItems.Count - 1
            newDocument.LastSection.Body.ChildEntities.Add(part.BodyItems(i).Clone())
        Next
        'Save the Word document
        newDocument.Save("Result" & bookmark.Name & ".docx", FormatType.Docx)
        newDocument.Close()
    Next
End Using
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-document/Split-by-bookmark).

## Split by placeholder text

The following code example illustrates how to split the Word document using the placeholder text.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Load an existing Word document.
FileStream fileStreamPath = new FileStream("Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
using (WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx))
{
    String[] findPlaceHolderWord = new string[] { "[First Content Start]", "[Second Content Start]", "[Third Content Start]" };
    for (int i = 0; i < findPlaceHolderWord.Length; i++)
    {
        //Get the start placeholder paragraph in the document.
        WParagraph startParagraph = document.Find(findPlaceHolderWord[i], true, true).GetAsOneRange().OwnerParagraph;
        //Get the end placeholder paragraph in the document.
        WParagraph endParagraph = document.Find(findPlaceHolderWord[i].Replace("Start", "End"), true, true).GetAsOneRange().OwnerParagraph;
        //Get the text body.
        WTextBody textBody = startParagraph.OwnerTextBody;
        //Get the start PlaceHolder index.
        int startPlaceHolderIndex = textBody.ChildEntities.IndexOf(startParagraph);
        //Get the end PlaceHolder index.
        int endPlaceHolderIndex = textBody.ChildEntities.IndexOf(endParagraph);
        //Create a new Word document.
        WordDocument newDocument = new WordDocument();
        newDocument.AddSection();
        //Add the retrieved content to another new document.
        for (int j = startPlaceHolderIndex + 1; j < endPlaceHolderIndex; j++)
            newDocument.LastSection.Body.ChildEntities.Add(textBody.ChildEntities[j].Clone());
        using (FileStream outputFileStream = new FileStream(Path.GetFullPath(@"Result" + i + ".docx"), FileMode.Create, FileAccess.ReadWrite))
        {
            //Save the Word document to file stream.
            newDocument.Save(outputFileStream, FormatType.Docx);
        }
    }
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Load an existing Word document into DocIO instance.
using (WordDocument document = new WordDocument("Template.docx", FormatType.Docx))
{
    String[] findPlaceHolderWord = new string[] { "[First Content Start]", "[Second Content Start]", "[Third Content Start]" };
    for (int i = 0; i < findPlaceHolderWord.Length; i++)
    {
        //Get the start placeholder paragraph in the document.
        WParagraph startParagraph = document.Find(findPlaceHolderWord[i], true, true).GetAsOneRange().OwnerParagraph;
        //Get the end placeholder paragraph in the document.
        WParagraph endParagraph = document.Find(findPlaceHolderWord[i].Replace("Start", "End"), true, true).GetAsOneRange().OwnerParagraph;
        //Get the text body.
        WTextBody textBody = startParagraph.OwnerTextBody;
        //Get the start PlaceHolder index.
        int startPlaceHolderIndex = textBody.ChildEntities.IndexOf(startParagraph);
        //Get the end PlaceHolder index.
        int endPlaceHolderIndex = textBody.ChildEntities.IndexOf(endParagraph);
        //Create a new Word document.
        WordDocument newDocument = new WordDocument();
        newDocument.AddSection();
        //Add the retrieved content to another new document.
        for (int j = startPlaceHolderIndex + 1; j < endPlaceHolderIndex; j++)
            newDocument.LastSection.Body.ChildEntities.Add(textBody.ChildEntities[j].Clone());
        //Save the Word document.
        newDocument.Save("Result" + i + ".docx", FormatType.Docx);
        newDocument.Close();
    }
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Load an existing Word document into DocIO instance.
Using document As WordDocument = New WordDocument("Template.docx", FormatType.Docx)
    Dim findPlaceHolderWord As String() = New String() {"[First Content Start]", "[Second Content Start]", "[Third Content Start]"}
    For i As Integer = 0 To findPlaceHolderWord.Length - 1
        'Get the start placeholder paragraph in the document.
        Dim startParagraph As WParagraph = document.Find(findPlaceHolderWord(i), True, True).GetAsOneRange().OwnerParagraph
        'Get the end placeholder paragraph in the document.
        Dim endParagraph As WParagraph = document.Find(findPlaceHolderWord(i).Replace("Start", "End"), True, True).GetAsOneRange().OwnerParagraph
        'Get the text body.
        Dim textBody As WTextBody = startParagraph.OwnerTextBody
        'Get the start PlaceHolder index.
        Dim startPlaceHolderIndex As Integer = textBody.ChildEntities.IndexOf(startParagraph)
        'Get the end PlaceHolder index.
        Dim endPlaceHolderIndex As Integer = textBody.ChildEntities.IndexOf(endParagraph)
        'Create a new Word document.
        Dim newDocument As WordDocument = New WordDocument()
        newDocument.AddSection()
        'Add the retrieved content to another new document.
        For j As Integer = startPlaceHolderIndex + 1 To endPlaceHolderIndex - 1
            newDocument.LastSection.Body.ChildEntities.Add(textBody.ChildEntities(j).Clone())
        Next
        'Save the Word document.
        newDocument.Save("Result" & i & ".docx", FormatType.Docx) 
        newDocument.Close();	   
    Next
End Using
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-document/Split-by-placeholder-text).