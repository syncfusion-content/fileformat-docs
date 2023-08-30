---
title: Working with Word comparisson in .NET Word library | Syncfusion
description: Learn how to compare Word documents using the .NET Word (DocIO) library without Microsoft Word.
platform: file-formats
control: DocIO
documentation: UG
---

# Compare Word documents 


N> You can use compare only in documents that are saved in the Open XML Format and cannot be used in the Word 97-2003 document (.doc) format.

## Compare two Word documents 

The following code example illustrates how to compare two Word documents in c#.

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


## Detect Formattings


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

## Supported Word document elements 

The following table shows the list of Word document elements supported in Word comparison. 

**Body items** 

<table>
<thead>
<tr>
<th>Element in Word document<br/><br/></th>
<th>Notes<br/><br/></th>
</tr>
</thead>
<tbody>  
<tr>
<td>
Paragraph<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
Table <br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
Block Content Control<br/><br/></td><td>
-<br/><br/></td></tr>
</tbody>
</table>


**Paragraph items**

<table>
<thead>
<tr>
<th>Element in Word document<br/><br/></th>
<th>Notes<br/><br/></th>
</tr>
</thead>
<tbody>  
<tr>
<td>
Field<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
Form Field <br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
Hyperlink<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
Image<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
Horizontal Rule<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
Content Control<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
Breaks<br/><br/></td><td>
-<br/><br/></td></tr>
</tbody>
</table>

**Formatting** 

<table>
<thead>
<tr>
<th>Element in Word document<br/><br/></th>
<th>Notes<br/><br/></th>
</tr>
</thead>
<tbody>  
<tr>
<td>
Bold<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
Italic <br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
StrikeThrough<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
Subscript and Superscript<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
Hidden<br/><br/></td><td>
-<br/><br/></td></tr>
<tr>
<td>
List<br/><br/></td><td>
-<br/><br/></td></tr>

</tbody>
</table>

## Limitation 

* Field - As default DocIO compares the result based on file level only, if need to compare with proper results, we suggest you to update the fields before start comparison.

* Comment - Comments will be maintain as it is in original document and doesn't perform comparison for comments.
