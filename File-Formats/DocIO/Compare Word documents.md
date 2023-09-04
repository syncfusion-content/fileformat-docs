---
title: Compare Word documents in C# | DocIO | Syncfusion
description: Learn how to compare two Word documents in C# using .NET Word (DocIO) library without Microsoft Word or interop dependencies.
platform: file-formats
control: DocIO
documentation: UG
---

# Compare Word documents in C#

Comparing two documents allows you to identify differences and similarities between them. The .NET Word library (DocIO) allows you to compare two Word documents and highlight the following changes as tracked changes
*	Insertions
*	Deletions
*	Formatting

N> Comparing two Word documents supported in DOCX format only.

## Compare two Word documents 

Compare the existing Word documents or document that is created from scratch using Compare method in .NET Word library (DocIO).

The following code example illustrates how to compare two Word documents.


{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

string originalFilePath = Path.GetFullPath("Data/OriginalDocument.docx");
string revisedFilePath = Path.GetFullPath("Data/RevisedDocument.docx");
string resultFilePath = Path.GetFullPath("Result.docx");

using (FileStream orgDocStream = new FileStream(originalFilePath, FileMode.Open, FileAccess.Read))
using (FileStream revisedStream = new FileStream(revisedFilePath, FileMode.Open, FileAccess.Read))
//Open the original Word document.
using (WordDocument originalDocument = new WordDocument(orgDocStream, FormatType.Docx))
//Open the revised Word document.
using (WordDocument revisedDocument = new WordDocument(revisedStream, FormatType.Docx))
{
    //Compare original document with revised document.
    originalDocument.Compare(revisedDocument);

    //Save the output Word document.
    using (FileStream resultStream = new FileStream(resultFilePath, FileMode.Create, FileAccess.ReadWrite))
    {
        originalDocument.Save(resultStream, FormatType.Docx);
    }
}

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

string originalFilePath = Path.GetFullPath("Data/OriginalDocument.docx");
string revisedFilePath = Path.GetFullPath("Data/RevisedDocument.docx");
string resultFilePath = Path.GetFullPath("Result.docx");

//Open the original Word document.
using (WordDocument originalDocument = new WordDocument(originalFilePath, FormatType.Docx))
//Open the revised Word document.
using (WordDocument revisedDocument = new WordDocument(revisedFilePath, FormatType.Docx))
{
    //Compare original document with revised document.
    originalDocument.Compare(revisedDocument);
    //Save the Word document.
    originalDocument.Save(resultFilePath);          
}

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

Dim originalFilePath As String = Path.GetFullPath("Data/OriginalDocument.docx")
Dim revisedFilePath As String = Path.GetFullPath("Data/RevisedDocument.docx")
Dim resultFilePath As String = Path.GetFullPath("Result.docx")

' Open the original Word document.
Using originalDocument As New WordDocument(originalFilePath, FormatType.Docx)
    ' Open the revised Word document.
    Using revisedDocument As New WordDocument(revisedFilePath, FormatType.Docx)
        ' Compare original document with revised document.
        originalDocument.Compare(revisedDocument)
        ' Save the Word document.
        originalDocument.Save(resultFilePath)
    End Using
End Using

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub]().

![Compare Word documents in C#]()

## Set Author and Date 

Compare two Word documents by setting author and date for revisions to identify the changes clearly.

The following code example shows how to set author and date for revision while comparing two Word documents.

## Comparison options

You can customize the Word comparison using our ComparisonOptions in DocIO.

### Ignore format changes

In the .NET Word library (DocIO), document comparison includes formatting changes by default. However, you can configure DocIO to ignore formatting differences using DetectFormatChanges API to concentrate solely on content modifications.

The following code example illustrates how to compare two Word documents by ignoring the format changes.


{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//Loads the original document
using (FileStream originalDocumentStreamPath = new FileStream("OriginalDocument.docx", FileMode.Open, FileAccess.Read))
{
    using (WordDocument originalDocument = new WordDocument(originalDocumentStreamPath, FormatType.Docx))
    {
        //Loads the revised document
        using (FileStream revisedDocumentStreamPath = new FileStream("RevisedDocument.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite))
        {
            using (WordDocument revisedDocument = new WordDocument(revisedDocumentStreamPath, FormatType.Automatic))
            {
                //Sets the Comparison option detect format changes, whether to detect format changes while comparing two Word documents
                ComparisonOptions compareOptions = new ComparisonOptions();
                compareOptions.DetectFormatChanges = false;
                //Compares the original document with revised document
                originalDocument.Compare(revisedDocument, "Syncfusion", DateTime.Now, compareOptions);
                //Saves the Word document to MemoryStream
                using (MemoryStream stream = new MemoryStream())
                {
                    originalDocument.Save(stream, FormatType.Docx);
                }
            }
        }
    }
}

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

//Loads the original document 
using (WordDocument originalDocument = new WordDocument("OriginalDocument.docx"))
{
    //Loads the revised document
    using (WordDocument revisedDocument = new WordDocument("RevisedDocument.docx"))
    {
        //Sets the Comparison option detect format changes, whether to detect format changes while comparing two Word documents
        ComparisonOptions compareOptions = new ComparisonOptions();
        compareOptions.DetectFormatChanges = false;
        //Compare the original document with revised document
        originalDocument.Compare(revisedDocument, "Syncfusion", DateTime.Now, compareOptions);
        //Save the Word document
        originalDocument.Save(output);
    }                 
} 

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Loads the original document
Using originalDocument As New WordDocument("OriginalDocument.docx")
    'Loads the revised document
    Using revisedDocument As New WordDocument("RevisedDocument.docx")
        'Sets the Comparison option to detect format changes
        Dim compareOptions As New ComparisonOptions()
        compareOptions.DetectFormatChanges = False
        'Compares the original document with the revised document
        originalDocument.Compare(revisedDocument, "Syncfusion", DateTime.Now, compareOptions)
        'Saves the Word document
        originalDocument.Save(output)
    End Using
End Using

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub]().

![Compare Word documents by ignoring format changes]()