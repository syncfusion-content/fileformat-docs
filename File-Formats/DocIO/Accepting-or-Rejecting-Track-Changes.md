---
title: Accepting or Rejecting Track Changes | DocIO | Syncfusion
description: This section illustrates how to Accept or Reject the Track changes in the Word document using Syncfusion Word library (Essential DocIO)
platform: file-formats
control: DocIO
documentation: UG
---
# Accepting or Rejecting Track Changes

It is used to keep track of the changes made to a Word document. It helps to maintain the record of author, name and time for every insertion, deletion, or modification in a document. This can be enabled by using the TrackChanges property of the Word document.

N> With this support, the changes made in the Word document by DocIO library cannot be tracked.

The following code example illustrates how to enable track changes of the document.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Appends text to the paragraph
IWTextRange text = paragraph.AppendText("This sample illustrates how to track the changes made to the word document. ");
//Sets font name and size for text
text.CharacterFormat.FontName = "Times New Roman";
text.CharacterFormat.FontSize = 14;
text = paragraph.AppendText("This track changes is useful in shared environment.");
text.CharacterFormat.FontSize = 12;
//Turns on the track changes option
document.TrackChanges = true;
//Saves and closes the document
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
'Creates a new Word document 
Dim document As New WordDocument()
'Adds new section to the document
Dim section As IWSection = document.AddSection()
'Adds new paragraph to the section
Dim paragraph As IWParagraph = section.AddParagraph()
'Appends text to the paragraph
Dim text As IWTextRange = paragraph.AppendText("This sample illustrates how to track the changes made to the word document. ")
'Sets font name and size for text
text.CharacterFormat.FontName = "Times New Roman"
text.CharacterFormat.FontSize = 14
text = paragraph.AppendText("This track changes is useful in shared environment.")
text.CharacterFormat.FontSize = 12
'Turns on the track changes option
document.TrackChanges = True
'Saves and closes the document
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Appends text to the paragraph
IWTextRange text = paragraph.AppendText("This sample illustrates how to track the changes made to the word document. ");
//Sets font name and size for text
text.CharacterFormat.FontName = "Times New Roman";
text.CharacterFormat.FontSize = 14;
text = paragraph.AppendText("This track changes is useful in shared environment.");
text.CharacterFormat.FontSize = 12;
//Turns on the track changes option
document.TrackChanges = true;
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word file in local machine
Save(stream, "Sample.docx");
document.Close();
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Appends text to the paragraph
IWTextRange text = paragraph.AppendText("This sample illustrates how to track the changes made to the word document. ");
//Sets font name and size for text
text.CharacterFormat.FontName = "Times New Roman";
text.CharacterFormat.FontSize = 14;
text = paragraph.AppendText("This track changes is useful in shared environment.");
text.CharacterFormat.FontSize = 12;
//Turns on the track changes option
document.TrackChanges = true;
//Saves the Word document to  MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Sample.docx");
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//Creates a new Word document 
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Appends text to the paragraph
IWTextRange text = paragraph.AppendText("This sample illustrates how to track the changes made to the word document. ");
//Sets font name and size for text
text.CharacterFormat.FontName = "Times New Roman";
text.CharacterFormat.FontSize = 14;
text = paragraph.AppendText("This track changes is useful in shared environment.");
text.CharacterFormat.FontSize = 12;
//Turns on the track changes option
document.TrackChanges = true;
MemoryStream stream = new MemoryStream();
//Saves the Word document to MemoryStream
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.docx", "application/msword", stream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Track-Changes/Enable-track-changes-of-Word).

## Accept all changes

You can **accept all track changes in Word document** using [AcceptAll](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.RevisionCollection.html#Syncfusion_DocIO_DLS_RevisionCollection_AcceptAll) method.

The following code example shows how to accept all the tracked changes.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Opens an existing Word document
WordDocument document = new WordDocument("Template.docx", FormatType.Docx);
//Accepts all the tracked changes revisions
if (document.HasChanges)
    document.Revisions.AcceptAll();
//Saves and closes the document
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %} 

{% highlight vb.net tabtitle="VB.NET" %}
'Opens an existing Word document
Dim document As WordDocument = New WordDocument("Template.docx", FormatType.Docx)
'Accepts all the tracked changes revisions
If document.HasChanges Then
    document.Revisions.AcceptAll()
End If
'Saves and closes the document
document.Save("Sample.docx", FormatType.Docx)
document.Close()
System.Diagnostics.Process.Start("Sample.docx")
{% endhighlight %} 

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing word document 
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Docx);
//Accepts all the tracked changes revisions
if (document.HasChanges)
	document.Revisions.AcceptAll();
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word document file in local machine
Save(stream, "Sample.docx");
//Closes the document instance
document.Close();

//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight c# tabtitle="ASP.NET Core" %}
//Opens an existing Word document
FileStream fileStreamPath = new FileStream("Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);           
WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);
//Accepts all the tracked changes revisions in the Word document
if (document.HasChanges)
    document.Revisions.AcceptAll();
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Sample.docx");
{% endhighlight %} 

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing wod document
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Automatic);
//Accepts all the tracked changes revisions
if (document.HasChanges)
    document.Revisions.AcceptAll();
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.docx", "application/msword", stream);
//Closes the document instance
document.Close();

//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Track-Changes/Accept-all-changes).

By executing the above code example, it generates output Word document as follows.

![Accepting all track changes in Word document](WorkingWithTrackChanges_images/AcceptAll.png)

## Reject all changes

You can **reject all track changes in Word document** using [RejectAll](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.RevisionCollection.html#Syncfusion_DocIO_DLS_RevisionCollection_RejectAll) method.

The following code example shows how to reject all the tracked changes.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Opens an existing Word document
WordDocument document = new WordDocument("Template.docx", FormatType.Docx);
//Rejects all the tracked changes revisions
if (document.HasChanges)
    document.Revisions.RejectAll();
//Saves and closes the document
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %} 

{% highlight vb.net tabtitle="VB.NET" %}
'Opens an existing Word document
Dim document As WordDocument = New WordDocument("Template.docx", FormatType.Docx)
'Rejects all the tracked changes revisions
If document.HasChanges Then
    document.Revisions.RejectAll()
End If
'Saves and closes the document
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing word document 
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Docx);
//Rejects all the tracked changes revisions
if (document.HasChanges)
    document.Revisions.RejectAll();
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word document file in local machine
Save(stream, "Sample.docx");
//Closes the document instance
document.Close();

//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight c# tabtitle="ASP.NET Core" %}
//Opens an existing word document 
FileStream fileStreamPath = new FileStream("Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);           
WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);
//Rejects all the tracked changes revisions in the Word document
if (document.HasChanges)
    document.Revisions.RejectAll();
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Sample.docx");
{% endhighlight %} 

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing  word document
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Automatic);
//Rejects all the tracked changes revisions
if (document.HasChanges)
    document.Revisions.RejectAll();
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.docx", "application/msword", stream);
//Closes the document instance
document.Close();

//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Track-Changes/Reject-all-changes).

By executing the above code example, it generates output Word document as follows.

![Rejecting all track changes in Word document](WorkingWithTrackChanges_images/RejectAll.png)

## Accept all changes by a particular reviewer

You can **accept all changes made by the author** in the Word document using [Accept](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.Revision.html#Syncfusion_DocIO_DLS_Revision_Accept) method.

The following code example shows how to accept the tracked changes made by the author.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Opens an existing Word document
WordDocument document = new WordDocument("Template.docx", FormatType.Docx);
//Iterates into all the revisions in Word document
for (int i = document.Revisions.Count - 1; i >= 0; i--)
{
    //Checks the author of current revision and accepts it.
    if (document.Revisions[i].Author == "Nancy Davolio")
        document.Revisions[i].Accept();
    //Resets to last item when accept the moving related revisions.
    if (i > document.Revisions.Count - 1)
        i = document.Revisions.Count;
}
//Saves and closes the document
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %} 

{% highlight vb.net tabtitle="VB.NET" %}
'Opens an existing Word document
Dim document As WordDocument = New WordDocument("Template.docx", FormatType.Docx)
'Iterates into all the revisions in Word document
For i As Integer = document.Revisions.Count - 1 To 0 Step -1
    'Checks the author of current revision and accepts it.
    If document.Revisions(i).Author Is "Nancy Davolio" Then
        document.Revisions(i).Accept()
    End If
    'Resets to last item when accept the moving related revisions.
    If i > document.Revisions.Count - 1 Then
        i = document.Revisions.Count
    End If
Next
'Saves and closes the document
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %} 

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing word document 
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Docx);
//Iterates into all the revisions in Word document
for (int i = document.Revisions.Count - 1; i >= 0; i--)
{
    //Checks the author of current revision and accepts it.
    if (document.Revisions[i].Author == "Nancy Davolio")
        document.Revisions[i].Accept();
    //Resets to last item when accept the moving related revisions.
    if (i > document.Revisions.Count - 1)
        i = document.Revisions.Count;
}
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word document file in local machine
Save(stream, "Sample.docx");
//Closes the document instance
document.Close();

//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
//Opens an existing word document 
FileStream fileStreamPath = new FileStream("Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);           
WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);
//Iterates into all the revisions in Word document
for (int i = document.Revisions.Count - 1; i >= 0; i--)
{
    //Checks the author of current revision and accepts it.
    if (document.Revisions[i].Author == "Nancy Davolio")
        document.Revisions[i].Accept();
    //Resets to last item when accept the moving related revisions.
    if (i > document.Revisions.Count - 1)
        i = document.Revisions.Count;
}
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Sample.docx");
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing  word document
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Automatic);
//Iterates into all the revisions in Word document
for (int i = document.Revisions.Count - 1; i >= 0; i--)
{
    //Checks the author of current revision and accepts it.
    if (document.Revisions[i].Author == "Nancy Davolio")
        document.Revisions[i].Accept();
    //Resets to last item when accept the moving related revisions.
    if (i > document.Revisions.Count - 1)
        i = document.Revisions.Count;
}
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.docx", "application/msword", stream);
//Closes the document instance
document.Close();

//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Track-Changes/Accept-all-changes-made-by-author).

## Reject all changes by particular reviewer

You can **reject all changes made by the author** in the Word document using [Reject](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.Revision.html#Syncfusion_DocIO_DLS_Revision_Reject) method.

The following code example shows how to reject the tracked changes made by the author.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Opens an existing Word document
WordDocument document = new WordDocument("Template.docx", FormatType.Docx);
//Iterates into all the revisions in Word document
for (int i = document.Revisions.Count - 1; i >= 0; i--)
{
    //Checks the author of current revision and rejects it.
    if (document.Revisions[i].Author == "Nancy Davolio")
        document.Revisions[i].Reject();
    //Resets to last item when reject the moving related revisions.
    if (i > document.Revisions.Count - 1)
        i = document.Revisions.Count;
}
//Saves and closes the document
document.Save("Sample.docx", FormatType.Docx);
document.Close();
{% endhighlight %} 

{% highlight vb.net tabtitle="VB.NET" %}
'Opens an existing Word document
Dim document As WordDocument = New WordDocument("Template.docx", FormatType.Docx)
'Iterates into all the revisions in Word document
For i As Integer = document.Revisions.Count - 1 To 0 Step -1
    'Checks the author of current revision and rejects it.
    If document.Revisions(i).Author Is "Nancy Davolio" Then
        document.Revisions(i).Reject()
    End If
    'Resets to last item when accept the moving related revisions.
    If i > document.Revisions.Count - 1 Then
        i = document.Revisions.Count
    End If
Next
'Saves and closes the document
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing word document 
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Docx);
//Iterates into all the revisions in Word document
for (int i = document.Revisions.Count - 1; i >= 0; i--)
{
    //Checks the author of current revision and rejects it.
    if (document.Revisions[i].Author == "Nancy Davolio")
        document.Revisions[i].Reject();
    //Resets to last item when reject the moving related revisions.
    if (i > document.Revisions.Count - 1)
        i = document.Revisions.Count;
}
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word document file in local machine
Save(stream, "Sample.docx");
//Closes the document instance
document.Close();

//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight c# tabtitle="ASP.NET Core" %}
//Opens an existing word document 
FileStream fileStreamPath = new FileStream("Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);           
WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);
//Iterates into all the revisions in Word document
for (int i = document.Revisions.Count - 1; i >= 0; i--)
{
    //Checks the author of current revision and rejects it.
    if (document.Revisions[i].Author == "Nancy Davolio")
        document.Revisions[i].Reject();
    //Resets to last item when reject the moving related revisions.
    if (i > document.Revisions.Count - 1)
        i = document.Revisions.Count;
}
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Sample.docx");
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing  word document
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Automatic);
//Iterates into all the revisions in Word document
for (int i = document.Revisions.Count - 1; i >= 0; i--)
{
    //Checks the author of current revision and rejects it.
    if (document.Revisions[i].Author == "Nancy Davolio")
        document.Revisions[i].Reject();
    //Resets to last item when reject the moving related revisions.
    if (i > document.Revisions.Count - 1)
        i = document.Revisions.Count;
}
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.docx", "application/msword", stream);
//Closes the document instance
document.Close();

//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Track-Changes/Reject-all-changes-made-by-author).

## Revision information

You can get the **revision information of track changes** in the Word document like author name, date, and type of revision.

The following code example shows how to get the details about the revision information of track changes.

{% tabs %}

{% highlight c# tabtitle="C#" %}
//Opens an existing Word document
WordDocument document = new WordDocument("Template.docx", FormatType.Docx);
//Accesses the first revision in the word document
Revision revision = document.Revisions[0];
//Gets the name of the user who made the specified tracked change
string author = revision.Author;
// Gets the date and time that the tracked change was made
DateTime dateTime = revision.Date;
// Gets the type of the track changes revision
RevisionType revisionType = revision.RevisionType;
//Closes the document
document.Close();
{% endhighlight %} 

{% highlight vb.net tabtitle="VB.NET" %}
'Opens an existing Word document
Dim document As WordDocument = New WordDocument("Template.docx", FormatType.Docx)
'Accesses the first revision in the word document
Dim revision As Revision = document.Revisions(0)
'Gets the name of the user who made the specified tracked change
Dim author As String = revision.Author
' Gets the date and time that the tracked change was made
Dim dateTime As Date = revision.Date
' Gets the type of the track changes revision
Dim revisionType As RevisionType = revision.RevisionType
'Closes the document
document.Close()
'Saves and closes the document
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %} 

{% highlight c# tabtitle="UWP" %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing word document 
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Docx);
//Accesses the first revision in the word document
Revision revision = document.Revisions[0];
//Gets the name of the user who made the specified tracked change
string author = revision.Author;
// Gets the date and time that the tracked change was made
DateTime dateTime = revision.Date;
// Gets the type of the track changes revision
RevisionType revisionType = revision.RevisionType;
//Closes the document
document.Close();

//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %} 

{% highlight c# tabtitle="ASP.NET Core" %}
//Opens an existing word document 
FileStream fileStreamPath = new FileStream("Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);           
WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);
//Accesses the first revision in the word document
Revision revision = document.Revisions[0];
//Gets the name of the user who made the specified tracked change
string author = revision.Author;
// Gets the date and time that the tracked change was made
DateTime dateTime = revision.Date;
// Gets the type of the track changes revision
RevisionType revisionType = revision.RevisionType;
//Closes the document
document.Close();
{% endhighlight %} 

{% highlight c# tabtitle="Xamarin" %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing  word document
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Automatic);
//Accesses the first revision in the word document
Revision revision = document.Revisions[0];
//Gets the name of the user who made the specified tracked change
string author = revision.Author;
// Gets the date and time that the tracked change was made
DateTime dateTime = revision.Date;
// Gets the type of the track changes revision
RevisionType revisionType = revision.RevisionType;
//Closes the document
document.Close();
{% endhighlight %} 

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Track-Changes/Get-revision-information).

**Frequently Asked Questions**

* [How to check whether a Word document contains tracked changes or not?](https://help.syncfusion.com/file-formats/docio/faq#how-to-check-whether-a-word-document-contains-tracked-changes-or-not)
* [How to accept or reject track changes of specific type in the Word document?](https://help.syncfusion.com/file-formats/docio/faq#how-to-accept-or-reject-track-changes-of-specific-type-in-the-word-document)
* [How to enable track changes for Word document?](https://help.syncfusion.com/file-formats/docio/faq#how-to-enable-track-changes-for-word-document)