---
title: Extract Text From PDF File | PDF | File Formats | Syncfusion
description: This section explains how to extract text from the particular page of the PDF document based on bounds and layout.
platform: file-formats
control: PDF
documentation: UG
---
# Working with Text Extraction

Essential PDF allows you to extract the text from a particular page or the entire PDF document. 

## Working with basic text extraction

You can extract the text from a page using [ExtractText](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Base~Syncfusion.Pdf.PdfPageBase~ExtractText().html) method in [PdfPageBase](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Base~Syncfusion.Pdf.PdfPageBase.html) class.

The following code snippet explains how to extract the texts from a page.

{% tabs %}

{% highlight c# %}

//Load an existing PDF.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);

//Load the first page.

PdfPageBase page = loadedDocument.Pages[0];

//Extract text from first page.

string extractedText = page.ExtractText();

//Close the document

loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Load an existing PDF.

Dim loadedDocument As New PdfLoadedDocument(fileName)

'Load the first page.

Dim page As PdfPageBase = loadedDocument.Pages(0)

'Extract the text from first page.

Dim extractedText As String = page.ExtractText()

'close the document.

loadedDocument.Close(True)

{% endhighlight %}

{% highlight UWP %}

//Create the file open picker

var picker = new FileOpenPicker();

picker.FileTypeFilter.Add(".pdf");

//Browse and chose the file

StorageFile file = await picker.PickSingleFileAsync();

//Creates an empty PDF loaded document instance

PdfLoadedDocument loadedDocument = new PdfLoadedDocument();

//Loads or opens an existing PDF document through Open method of PdfLoadedDocument class

await loadedDocument.OpenAsync(file);

//Load the first page.

PdfPageBase page = loadedDocument.Pages[0];

//Extract text from first page.

string extractedText = page.ExtractText();

//Close the document.

loadedDocument.Close(true);

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document.

FileStream docStream = new FileStream("Sample.pdf", FileMode.Open, FileAccess.Read);

//Load the PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Load the first page.

PdfPageBase page = loadedDocument.Pages[0];

//Extract text from first page.

string extractedText = page.ExtractText();

//Close the document.

loadedDocument.Close(true);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Load the first page.

PdfPageBase page = loadedDocument.Pages[0];

//Extract text from first page.

TextLineCollection lineCollection =  new TextLineCollection();

string extractedText = page.ExtractText(out lineCollection);

//Close the document

loadedDocument.Close(true);

{% endhighlight %}

{% endtabs %}

N> In this method, the text is extracted in the order in which it is written in the document stream and it may not be in the order in which it is viewed in the PDF reader application.

N> Extracting text from the PDF document pages will not load the entire document content into memory.

The below code illustrates how to extract the text from entire PDF document:

{% tabs %}

{% highlight c# %}

// Load an existing PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);

// Loading page collections

PdfLoadedPageCollection loadedPages = loadedDocument.Pages;

string extractedText = string.Empty;

// Extract text from existing PDF document pages

foreach (PdfLoadedPage loadedPage in loadedPages)

{

extractedText += loadedPage.ExtractText();

}

// Close the document.

loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net %}

' Load an existing PDF document.

Dim loadedDocument As New PdfLoadedDocument(fileName)

' Loading page collections

Dim loadedPages As PdfLoadedPageCollection = loadedDocument.Pages

Dim extractedText As String = String.Empty

' Extract text from existing PDF document pages

For Each loadedPage As PdfLoadedPage In loadedPages

extractedText &= loadedPage.ExtractText()

Next loadedPage

' Close the document.

loadedDocument.Close(True)

{% endhighlight %}

{% highlight UWP %}

//Create the file open picker

var picker = new FileOpenPicker();

picker.FileTypeFilter.Add(".pdf");

//Browse and chose the file

StorageFile file = await picker.PickSingleFileAsync();

//Creates an empty PDF loaded document instance

PdfLoadedDocument loadedDocument = new PdfLoadedDocument();

//Loads or opens an existing PDF document through Open method of PdfLoadedDocument class

await loadedDocument.OpenAsync(file);

// Loading page collections

PdfLoadedPageCollection loadedPages = loadedDocument.Pages;

string extractedText = string.Empty;

// Extract text from existing PDF document pages

foreach (PdfLoadedPage loadedPage in loadedPages)

{

    extractedText += loadedPage.ExtractText();

}

//Close the document.

loadedDocument.Close(true);


{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document.

FileStream docStream = new FileStream("Sample.pdf", FileMode.Open, FileAccess.Read);

//Load the PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

// Loading page collections

PdfLoadedPageCollection loadedPages = loadedDocument.Pages;

string extractedText = string.Empty;

// Extract text from existing PDF document pages

foreach (PdfLoadedPage loadedPage in loadedPages)

{

    extractedText += loadedPage.ExtractText();

}

//Close the document.

loadedDocument.Close(true);

{% endhighlight %}

{% highlight Xamarin %}

//Load the file as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample.pdf");

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

// Loading page collections

PdfLoadedPageCollection loadedPages = loadedDocument.Pages;

TextLineCollection lineCollection =  new TextLineCollection();

string extractedText = string.Empty;

// Extract text from existing PDF document pages

foreach (PdfLoadedPage loadedPage in loadedPages)

{

    extractedText += loadedPage.ExtractText(out lineCollection);

}

//Close the document

loadedDocument.Close(true);

{% endhighlight %}

{% endtabs %}

## Working with layout based text extraction

You can extract text from the given PDF page based on its layout using [ExtractText(bool)](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Base~Syncfusion.Pdf.PdfPageBase~ExtractText(Boolean).html) overload. In this method, the text is extracted in the layout as it is viewed in the reader application.

Please refer the following code snippet to extract the text with layout.

{% tabs %}

{% highlight c# %}

//Load an existing PDF.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);

//Load first page.

PdfPageBase page = loadedDocument.Pages[0];

//Extract text from first page.

string extractedTexts = page.ExtractText(true);

//close the document

loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net %}

//Load an existing PDF.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(fileName);

//Load first page.

PdfPageBase page = loadedDocument.Pages[0];

//Extract text from first page.

string extractedTexts = page.ExtractText(true);

//close the document

loadedDocument.Close(true);

{% endhighlight %}

{% highlight UWP %}

//Create the file open picker

var picker = new FileOpenPicker();

picker.FileTypeFilter.Add(".pdf");

//Browse and chose the file

StorageFile file = await picker.PickSingleFileAsync();

//Creates an empty PDF loaded document instance

PdfLoadedDocument loadedDocument = new PdfLoadedDocument();

//Loads or opens an existing PDF document through Open method of PdfLoadedDocument class

await loadedDocument.OpenAsync(file);

//Load first page.

PdfPageBase page = loadedDocument.Pages[0];

//Extract text from first page.

string extractedTexts = page.ExtractText(true);

//Close the document.

loadedDocument.Close(true);

{% endhighlight %}

{% highlight ASP.NET Core %}

//Load the PDF document.

FileStream docStream = new FileStream("Sample.pdf", FileMode.Open, FileAccess.Read);

//Load the PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(docStream);

//Load first page.

PdfPageBase page = loadedDocument.Pages[0];

//Extract text from first page.

string extractedTexts = page.ExtractText(true);

//Close the document.

loadedDocument.Close(true);

//Save the document into stream

MemoryStream stream = new MemoryStream();

loadedDocument.Save(stream);

stream.Position = 0;

//Closes the document

loadedDocument.Close(true);

{% endhighlight %}

{% highlight Xamarin %}

//PDF supports extract text from the given PDF page based on its layout using ExtractText(bool) overload only in Windows Forms, WPF, ASP.NET, ASP.NET MVC, ASP.NET Core and UWP platforms.

{% endhighlight %}

{% endtabs %}

N> Layout based text extraction may take additional processing time when compared to the normal extraction mode.

## Text Extraction with Bounds

### Working with Lines

You can get the line and its properties that contains texts by using [TextLine](https://help.syncfusion.com/cr/xamarin/Syncfusion.Pdf.Portable~Syncfusion.Pdf.TextLine.html). Refer to the following code sample.

{% tabs %}

{% highlight C# %}

//PDF supports getting the lines and its properties using TextLine only in Xamarin platform.

{% endhighlight %}

{% highlight vb.net %}

//PDF supports getting the lines and its properties using TextLine only in Xamarin platform.

{% endhighlight %}

{% highlight UWP %}

//PDF supports getting the lines and its properties using TextLine only in Xamarin platform.

{% endhighlight %}

{% highlight ASP.NET Core %}

//PDF supports getting the lines and its properties using TextLine only in Xamarin platform.

{% endhighlight %}

{% highlight Xamarin %}

//Load the existing PDF document
PdfLoadedDocument m_loadedDocument = new PdfLoadedDocument(stream);

//Get the first page of the loaded PDF document
PdfPageBase page = m_loadedDocument.Pages[0];

TextLineCollection lineCollection = new TextLineCollection();

//Extract text from the first page
string m_extractedText = page.ExtractText(out lineCollection);

//Gets specific line from the collection
TextLine line = lineCollection.TextLine[0];

//Gets bounds of the line
RectangleF lineBounds = line.Bounds;

//Gets the font of the text
string fontName = line.FontName;

//Gets the size of the text
float fontSize = line.FontSize;

//Gets font style of the text
FontStyle fontStyle = line.FontStyle;

//Gets text in the line
string text = line.Text;
//Gets collection of the words in the line
List<TextWord> textWordCollection = line.WordCollection;

{% endhighlight %}

{% endtabs %}

### Working with words
 
You can get the single word and its properties by using [TextWord](https://help.syncfusion.com/cr/xamarin/Syncfusion.Pdf.Portable~Syncfusion.Pdf.TextWord.html). Refer to the following code sample.

{% tabs %}

{% highlight C# %}

//PDF supports getting the word and its properties using TextWord only in Xamarin platform. 

{% endhighlight %}

{% highlight vb.net %}

//PDF supports getting the word and its properties using TextWord only in Xamarin platform.

{% endhighlight %}

{% highlight UWP %}

//PDF supports getting the word and its properties using TextWord only in Xamarin platform.

{% endhighlight %}

{% highlight ASP.NET Core %}

//PDF supports getting the word and its properties using TextWord only in Xamarin platform.

{% endhighlight %}

{% highlight Xamarin %}

//Load the existing PDF document
PdfLoadedDocument m_loadedDocument = new PdfLoadedDocument(stream);

//Get the first page of the loaded PDF document
PdfPageBase page = m_loadedDocument.Pages[0];

TextLineCollection lineCollection = new TextLineCollection();

//Extract text from the first page
string m_extractedText = page.ExtractText(out lineCollection);

//Gets specific line from the collection
TextLine line = lineCollection.TextLine[0];

//Gets collection of the words in the line
List<TextWord> textWordCollection = line.WordCollection;

//Gets word from the collection using index
TextWord textWord = textWordCollection[0];

//Gets bounds of the word
RectangleF WordBounds = textWord.Bounds;

//Gets font name of the word
string wordFontName = textWord.FontName;

//Gets size of the word
float wordFontSize = textWord.FontSize;

//Gets font style of the word
FontStyle wordFontStyle = textWord.FontStyle;

// Gets the word
string wordText = textWord.Text;

// Gets Glyph details of the word
List<TextGlyph> textGlyphCollection = textWord.Glyphs;

{% endhighlight %}

{% endtabs %}

### Working with characters

You can get single character and its properties by using [TextGlyph](https://help.syncfusion.com/cr/xamarin/Syncfusion.Pdf.Portable~Syncfusion.Pdf.TextGlyph.html). Refer to the following code sample. 

{% tabs %}

{% highlight C# %}

//PDF supports getting the single character and its properties using TextGlyph only in Xamarin platform. 

{% endhighlight %}

{% highlight vb.net %}

//PDF supports getting the single character and its properties using TextGlyph only in Xamarin platform.

{% endhighlight %}

{% highlight UWP %}

//PDF supports getting the single character and its properties using TextGlyph only in Xamarin platform.

{% endhighlight %}

{% highlight ASP.NET Core %}

//PDF supports getting the single character and its properties using TextGlyph only in Xamarin platform.

{% endhighlight %}

{% highlight Xamarin %}

//Load the existing PDF document
PdfLoadedDocument m_loadedDocument = new PdfLoadedDocument(stream);

//Get the first page of the loaded PDF document
PdfPageBase page = m_loadedDocument.Pages[0];

TextLineCollection lineCollection = new TextLineCollection();

//Extract text from the first page
string m_extractedText = page.ExtractText(out lineCollection);

//Gets specific line from the collection
TextLine line = lineCollection.TextLine[0];

//Gets collection of the words in the line
List<TextWord> textWordCollection = line.WordCollection;

//Gets word from the collection using index
TextWord textWord = textWordCollection[0];

// Gets Glyph details of the word
List<TextGlyph> textGlyphCollection = textWord.Glyphs;

//Gets character of the word
TextGlyph textGlyph = textGlyphCollection[0];

//Gets bounds of the character
RectangleF glyphBounds = textGlyph.Bounds;

//Gets font name of the character
string GlyphFontName = textGlyph.FontName;

//Gets font size of the character
float GlyphFontSize = textGlyph.FontSize;

//Gets font style of the character
FontStyle GlyphFontStyle = textGlyph.FontStyle;

//Gets character in the word
char GlyphText = textGlyph.Text;

{% endhighlight %}

{% endtabs %}