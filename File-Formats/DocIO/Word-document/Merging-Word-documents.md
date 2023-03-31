---
title: Merge Word documents in C# | DocIO | Syncfusion
description: Learn how to merge multiple Word documents into one using .NET Word (DocIO) library without Microsoft Word or interop dependencies.
platform: file-formats
control: DocIO
documentation: UG
---
# Merging Word documents

You can merge multiple Word documents into single Word document by using DocIO’s capability of importing contents from one document to another. The imported contents are appended at the end of document.

## Merge document in new page

The following code example illustrates how to import the contents from source document into destination document where the contents are appended. 

{% tabs %}

{% highlight c# tabtitle="C# (.NET Cross platform)" %}
FileStream sourceStreamPath = new FileStream(sourceFileName, FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
FileStream destinationStreamPath = new FileStream(destinationFileName, FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
//Opens an source document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument(sourceStreamPath, FormatType.Automatic))
{
    //Opens the destination document 
    WordDocument destinationDocument = new WordDocument(destinationStreamPath, FormatType.Docx);
    //Imports the contents of source document at the end of destination document
    destinationDocument.ImportContent(document, ImportOptions.UseDestinationStyles);
    //Saves and closes the destination document to  MemoryStream
    MemoryStream stream = new MemoryStream();
    destinationDocument.Save(stream, FormatType.Docx);
    destinationDocument.Close();
    document.Close(); 
}
{% endhighlight %}

{% highlight c# tabtitle="C# (.NET Windows-specific)" %}
//Opens the source document 
WordDocument sourceDocument = new WordDocument(sourceFileName);
//Opens the destination document 
WordDocument destinationDocument = new WordDocument(targetFileName);
//Imports the contents of source document at the end of destination document
destinationDocument.ImportContent(sourceDocument, ImportOptions.UseDestinationStyles);
//Saves the destination document
destinationDocument.Save(outputFileName, FormatType.Docx);
//closes the document instances
sourceDocument.Close();
destinationDocument.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB. NET (.NET Windows-specific)" %}
'Opens the source document 
Dim sourceDocument As New WordDocument(sourceFileName)
'Opens the destination document 
Dim destinationDocument As New WordDocument(targetFileName)
'Imports the contents of source document at the end of destination document
destinationDocument.ImportContent(sourceDocument, ImportOptions.UseDestinationStyles)
'Saves the destination document
destinationDocument.Save(outputFileName, FormatType.Docx)
'closes the document instances
sourceDocument.Close()
destinationDocument.Close()
{% endhighlight %} 

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-document/Merge-documents-in-new-page).

In the resultant document, the imported contents start from a new page followed by existing contents in a destination document. This is the default behavior.

## Merge document in same page

When your requirement is to append the contents from the same page instead of starting from a new page, you need to set the break code of first section of Source document as [NoBreak](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.SectionBreakCode.html). The following code example illustrates the importing contents from the same page.

{% tabs %}

{% highlight c# tabtitle="C# (.NET Cross platform)" %}
FileStream sourceStreamPath = new FileStream(sourceFileName, FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
FileStream destinationStreamPath = new FileStream(destinationFileName, FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
//Opens an source document from file system through constructor of WordDocument class
using (WordDocument document = new WordDocument(sourceStreamPath, FormatType.Automatic))
{
    //Opens the destination document 
    WordDocument destinationDocument = new WordDocument(destinationStreamPath, FormatType.Docx);
    //Sets the break-code of First section of source document as NoBreak to avoid imported from a new page
    document.Sections[0].BreakCode = SectionBreakCode.NoBreak; 
    //Imports the contents of source document at the end of destination document
    destinationDocument.ImportContent(document, ImportOptions.UseDestinationStyles);
    //Saves and closes the destination document to  MemoryStream
    MemoryStream stream = new MemoryStream();
    destinationDocument.Save(stream, FormatType.Docx);
    destinationDocument.Close();
    document.Close(); 
}
{% endhighlight %}

{% highlight c# tabtitle="C# (.NET Windows-specific)" %}
//Opens the source document 
WordDocument sourceDocument = new WordDocument(sourceFileName);
//Opens the destination document 
WordDocument destinationDocument = new WordDocument(targetFileName);
//Sets the break-code of First section of source document as NoBreak to avoid imported from a new page
sourceDocument.Sections[0].BreakCode = SectionBreakCode.NoBreak; 
//Imports the contents of source document at the end of destination document
destinationDocument.ImportContent(sourceDocument, ImportOptions.UseDestinationStyles);
//Saves the destination document
destinationDocument.Save(outputFileName, FormatType.Docx);
//Closes the document instances
sourceDocument.Close();
destinationDocument.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB. NET (.NET Windows-specific)" %}
'Opens the source document 
Dim sourceDocument As New WordDocument(sourceFileName)
'Opens the destination document 
Dim destinationDocument As New WordDocument(targetFileName)
'Sets the break-code of first section of source document as NoBreak to avoid imported from a new page
sourceDocument.Sections(0).BreakCode = SectionBreakCode.NoBreak
'Imports the contents of source document at the end of destination document
destinationDocument.ImportContent(sourceDocument, ImportOptions.UseDestinationStyles)
'Saves the destination document
destinationDocument.Save(outputFileName, FormatType.Docx)
'Closes the document instances
sourceDocument.Close()
destinationDocument.Close()
{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Word-document/Merge-documents-in-same-page).

## Maintain Imported List style information

The following code example shows how to maintain information about imported list styles in a Word document while cloning and merging multiple Word documents.

{% tabs %}

{% highlight c# tabtitle="C# (.NET Cross platform)" %}
//Opens the source document
FileStream SourceFileStream = new FileStream("Source.docx", FileMode.Open);
WordDocument sourceDocument = new WordDocument(SourceFileStream, FormatType.Docx);
//Opens the destination document  
FileStream DestinationFileStream = new FileStream("Destination.docx", FileMode.Open);
WordDocument destinationDocument = new WordDocument(DestinationFileStream, FormatType.Docx);
//Sets true value to maintain imported list style cache to destination document
destinationDocument.Settings.MaintainImportedListCache = true;
//Processes the body contents for each section in the Word document
foreach (WSection section in sourceDocument.Sections)
{
    //Accesses the body of section where all the contents in document are apart
    foreach (TextBodyItem bodyItem in section.Body.ChildEntities)
    {
        destinationDocument.LastSection.Body.ChildEntities.Add(bodyItem.Clone());
    }
}
//Closes the source document
sourceDocument.Close();
//Sets false value to exclude imported list style cache to destination document
destinationDocument.Settings.MaintainImportedListCache = false;
//Saves the destination document
MemoryStream outputStream = new MemoryStream();
destinationDocument.Save(outputStream, FormatType.Docx);
//Closes the destination document
destinationDocument.Close();
{% endhighlight %}

{% highlight c# tabtitle="C# (.NET Windows-specific)" %}
//Opens the source document
WordDocument sourceDocument = new WordDocument(sourceFileName);
//Opens the destination document  
WordDocument destinationDocument = new WordDocument(targetFileName);
//Sets true value to maintain imported list style cache to destination document
destinationDocument.Settings.MaintainImportedListCache = true;
//Processes the body contents for each section in the Word document
foreach (WSection section in sourceDocument.Sections)
{
    //Accesses the body of section where all the contents in document are apart
    foreach (TextBodyItem bodyItem in section.Body.ChildEntities)
    {
        destinationDocument.LastSection.Body.ChildEntities.Add(bodyItem.Clone());
    }
}
//Closes the source document
sourceDocument.Close();
//Sets false value to exclude imported list style cache to destination document
destinationDocument.Settings.MaintainImportedListCache = false;
//Saves the destination document
destinationDocument.Save(outputFileName, FormatType.Docx);
//Closes the destination document
destinationDocument.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB. NET (.NET Windows-specific)" %}
'Opens the source document
Dim sourceDocument As New WordDocument(sourceFileName)
'Opens the destination document
Dim destinationDocument As New WordDocument(targetFileName)
'Sets true value to maintain imported list style cache to destination document
destinationDocument.Settings.MaintainImportedListCache = True
'Processes the body contents for each section in the Word document
For Each section As WSection In sourceDocument.Sections
    'Accesses the body of section where all the contents in document are apart     
    For Each bodyItem As TextBodyItem In section.Body.ChildEntities
        destinationDocument.LastSection.Body.ChildEntities.Add(bodyItem.Clone())
    Next
Next
'Closes the source document
sourceDocument.Close()
'Sets false value to exclude imported list style cache to destination document
destinationDocument.Settings.MaintainImportedListCache = False
'Saves the destination document
destinationDocument.Save(outputFileName, FormatType.Docx)
'Closes the destination document
destinationDocument.Close()
{% endhighlight %}

{% endtabs %}

## See Also

* [How to merge multiple Word documents in C#, VB.NET](https://www.syncfusion.com/kb/12998/how-to-merge-multiple-word-documents-in-c-vb-net)
* [How to remove Section Break when merging documents using ImportContent API](https://www.syncfusion.com/kb/12952/how-to-remove-section-break-when-merging-documents-using-importcontent-api)