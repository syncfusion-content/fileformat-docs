---
title: Split PDF Documents | Syncfusion
description:  Split a PDF file into single-page or multiple-page PDFs using the Syncfusion .NET PDF library.
platform: file-formats
control: PDF
documentation: UG
---

# Split PDF Documents using .NET PDF Library

The Syncfusion .NET PDF library supports [Splitting PDF file](https://www.syncfusion.com/document-processing/pdf-framework/net/pdf-library/split-pdf) into single-page or multiple-page PDF documents.

## Splitting a PDF file into individual pages

The Syncfusion .NET PDF library allows splitting the pages of an existing PDF document into multiple individual PDF documents using [Split](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html#Syncfusion_Pdf_Parsing_PdfLoadedDocument_Split_System_String_) method of the [PdfLoadedDocument](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html) class.

Refer to the following code example to split a PDF into individual pages.

{% tabs %}  

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Due to platform limitations, Essential PDF supports splitting a PDF file into individual pages only in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms. However this can be achieved by using the following code snippet. 

//Load the PDF document
FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);
for (int i=0;i<loadedDocument.PageCount;i++)
{
//Creates a new document
PdfDocument document = new PdfDocument();
//Imports the pages from the loaded document
document.ImportPage(loadedDocument, i);

//Create a memory stream 
MemoryStream stream = new MemoryStream();
//Save the document to stream
document.Save(stream);
//Close the document
document.Close(true);
}

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Load the PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");
//Set a output path
const string destinationFilePattern = "Output" + "{0}.pdf";
//Split the pages into separate documents
loadedDocument.Split(destinationFilePattern);
//Close the document
loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Load the PDF document
Dim loadedDocument As New PdfLoadedDocument("Input.pdf")
'Set a output path
Const destinationFilePattern As String = "Output" + "{0}.pdf"
'Split the pages into separate documents
loadedDocument.Split(destinationFilePattern)
'Close the document
loadedDocument.Close(True)

{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Pages/Splitting-PDF-file-into-individual-pages/). 

## Split a range of pages into a separate PDF document

The Syncfusion .NET PDF library allows splitting a certain range of pages into a separate PDF document using the [SplitByRanges](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html#Syncfusion_Pdf_Parsing_PdfLoadedDocument_SplitByRanges_System_String_System_Int32_0__0___) method of the [PdfLoadedDocument](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html) class. 

Refer to the following code example to split a range of pages.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Due to platform limitations, Essential PDF supports splitting a range of pages into separate PDF document only in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms. However this can be achieved by using the following code snippet. 
//Load the PDF document
FileStream docStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read);
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);
//Import the range of pages from the existing PDF
loadedDocument.ImportPageRange(loadedDocument, 2, 8);

//Create a memory stream 
MemoryStream stream = new MemoryStream();
//Save the document to stream
loadedDocument.Save(stream);
//Close the document
loadedDocument.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

int[,] values = new int[,] { { 2, 5 }, { 8, 10 } };
//Load the PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");
//Set a output path
const string destinationFilePattern = "Output" + "{0}.pdf";
//Split the pages into fixed number
loadedDocument.SplitByRanges(destinationFilePattern, values);
//close the document
loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Load the PDF document.
Dim loadedDocument As New PdfLoadedDocument("Input.pdf")
'Set a output path
Const destinationFilePattern As String = "Output" + "{0}.pdf"
'Split the pages into fixed number.
loadedDocument.SplitByRanges(destinationFilePattern, values)
'Close the document.
loadedDocument.Close(True)

{% endhighlight %}

{% endtabs %}  

Download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Split%20PDFs/Split-a-Range-of-Pages/.NET%20Framework).

## Split by a fixed number of pages into a PDF document

The Syncfusion .NET PDF library allows splitting by fixed number of pages of an existing PDF document using the [SplitByFixedNumber](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html#Syncfusion_Pdf_Parsing_PdfLoadedDocument_SplitByFixedNumber_System_String_System_Int32_) method of the [PdfLoadedDocument](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html) class.
Refer to the following code example to split by a fixed number of pages.

{% tabs %}  

{% highlight c# tabtitle="C# [Cross-platform]" %}

//PDF doesn't support split by fixed number on the C#.NET Cross platforms.

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Load the PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");
//Set a output path
const string destinationFilePattern = "Output" + "{0}.pdf";
//Split the pages into fixed number
loadedDocument.SplitByFixedNumber(destinationFilePattern, 4);

//close the document
loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Load the PDF document.
Dim loadedDocument As New PdfLoadedDocument("Input.pdf")
'Set a output path
Const destinationFilePattern As String = "Output" + "{0}.pdf"
'Split the pages into fixed number
loadedDocument.SplitByFixedNumber(destinationFilePattern, 4)
'Close the document.
loadedDocument.Close(True)

{% endhighlight %}

{% endtabs %}

Download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Split%20PDFs/Split-by-FixedNumber/.NET%20Framework).

## Split a PDF document based on PDF bookmarks

A PDF document may contain bookmarks that indicate different sections.The Syncfusion .NET PDF library allows splitting a PDF document into sections using the [PdfBookmark](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfBookmark.html) class.

Refer to the following code example to split a PDF using bookmarks.

{% tabs %}  

{% highlight c# tabtitle="C# [Cross-platform]" %}

// Load the PDF document 
using (FileStream fileStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.Read)) 
using (PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileStream)) 
{ 
    PdfBookmarkBase bookmarks = loadedDocument.Bookmarks; 
    // Iterate all the bookmarks and their page ranges 
    foreach (PdfBookmark bookmark in bookmarks) 
    { 
        if (bookmark.Destination != null) 
        { 
            if (bookmark.Destination.Page != null) 
            { 
                int endIndex = bookmark.Destination.PageIndex; 
                // Create a new PDF document
                using (PdfDocument document = new PdfDocument()) 
                { 
                    foreach (PdfLoadedBookmark childBookmark in bookmark) 
                    { 
                        endIndex = childBookmark.Destination.PageIndex; 
                    } 
                    // Import the pages to the new PDF document 
                    document.ImportPageRange(loadedDocument, bookmark.Destination.PageIndex, endIndex); 
                    //Save the document as stream
                    using (MemoryStream stream = new MemoryStream()) 
                    { 
                        document.Save(stream); 
                    } 
                } 
            } 
        } 
    } 
} 

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

// Load the PDF document 
using (PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf"))
{
     PdfBookmarkBase bookmarks = loadedDocument.Bookmarks;
     // Iterate all the bookmarks and their page ranges 
     foreach (PdfBookmark bookmark in bookmarks)
    {
        if (bookmark.Destination != null)
        {
           if (bookmark.Destination.Page != null)
            {
              int endIndex = bookmark.Destination.PageIndex;
              // Create a new PDF document
              using (PdfDocument document = new PdfDocument())
                {
                    foreach (PdfLoadedBookmark childBookmark in bookmark)
                    {
                        endIndex = childBookmark.Destination.PageIndex;
                    }
                    // Import the pages to the new PDF document 
                    document.ImportPageRange(loadedDocument, bookmark.Destination.PageIndex, endIndex);
                    //Save the document as stream
                    document.Save("Output.pdf");
                }
            }
        }
    }
} 

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

Using loadedDocument As PdfLoadedDocument = New PdfLoadedDocument("Input.pdf")
Dim bookmarks As PdfBookmarkBase = loadedDocument.Bookmarks
For Each bookmark As PdfBookmark In bookmarks
If bookmark.Destination IsNot Nothing Then
If bookmark.Destination.Page IsNot Nothing Then
Dim endIndex As Integer = bookmark.Destination.PageIndex
Using document As PdfDocument = New PdfDocument()
For Each childBookmark As PdfLoadedBookmark In bookmark
endIndex = childBookmark.Destination.PageIndex
Next
document.ImportPageRange(loadedDocument, bookmark.Destination.PageIndex, endIndex)
document.Save("Output.pdf")
End Using
End If
End If
Next
End Using

{% endhighlight %}

{% endtabs %}

Download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Split%20PDFs/Split-PDF-based-Bookmarks/.NET).