---
title: Working with Text
description: This section explains how to add text to the PDF document using different type of fonts, TrueType fonts and standard fonts
platform: file-formats
control: PDF
documentation: UG
---
# Working with Text

## Drawing text in a new document

You can add text in the new PDF document by using the following code sample,

{% tabs %}

{% highlight c# %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Set the standard font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

//Save the document.

document.Save("Output.pdf");

//Close the document.

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim document As New PdfDocument()

'Add a page to the document.

Dim page As PdfPage = document.Pages.Add()

'Create PDF graphics for the page.

Dim graphics As PdfGraphics = page.Graphics

'Set the standard font.

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 20)

'Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, New PointF(0, 0))

'Save the document.

document.Save("Output.pdf")

'Close the document.

document.Close(True)

{% endhighlight %}

{% endtabs %}

## Drawing text in an existing document

You can add text in the existing PDF document by using the following code sample,

{% tabs %}

{% highlight c# %}

//Load a PDF document.
PdfLoadedDocument doc = new PdfLoadedDocument("input.pdf");

//Get first page from document
PdfLoadedPage page = doc.Pages[0] as PdfLoadedPage;

//Create PDF graphics for the page
PdfGraphics graphics = page.Graphics;

//Set the standard font.
PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.
graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

//Save the document.
doc.Save("Output.pdf");

//Close the document.
doc.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Load a PDF document.
Dim doc As New PdfLoadedDocument("input.pdf")

'Get first page from document
Dim page As PdfLoadedPage = TryCast(doc.Pages(0), PdfLoadedPage)

'Create PDF graphics for the page
Dim graphics As PdfGraphics = page.Graphics

'Set the standard font.
Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 20)

'Draw the text.
graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, New PointF(0, 0))

'Save the document.
doc.Save("Output.pdf")

'Close the document.
doc.Close(True)

{% endhighlight %}

{% endtabs %}

## Drawing text using different fonts

Essential PDF allows you to add text to the PDF document using the following types of fonts.

1. Standard fonts
2. TrueType fonts
3. Chinese, Japanese and Korean (CJK) fonts

### Draw text using standard fonts

PDF has fourteen base fonts, also known as standard fonts which has special significance. The details can be referred from the link below.

[Standard type 1 fonts](https://en.wikipedia.org/wiki/Portable_Document_Format#Standard_Type_1_Fonts_.28Standard_14_Fonts.29)

You can add text using the standard PDF fonts by using the following code snippet. 

{% tabs %}

{% highlight c# %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Set the standard font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

//Save the document.

document.Save("Output.pdf");

//Close the document.

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim document As New PdfDocument()

'Add a page to the document.

Dim page As PdfPage = document.Pages.Add()

'Create PDF graphics for the page.

Dim graphics As PdfGraphics = page.Graphics

'Set the standard font.

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 20)

'Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, New PointF(0, 0))

'Save the document.

document.Save("Output.pdf")

'Close the document.

document.Close(True)

{% endhighlight %}

{% endtabs %}

### Draw text using TrueType fonts

You can add text using the TrueType fonts installed in the system by using the following code snippet.

{% tabs %}

{% highlight c# %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Use the font installed in the machine

PdfFont font = new PdfTrueTypeFont(new Font("Arial", 14));

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

//Save the document.

document.Save("Output.pdf");

//Close the document.

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim document As New PdfDocument()

'Add a page to the document.

Dim page As PdfPage = document.Pages.Add()

'Create PDF graphics for the page.

Dim graphics As PdfGraphics = page.Graphics

'Use the font installed in the machine

Dim font As PdfFont = New PdfTrueTypeFont(New Font("Arial", 14))

'Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, New PointF(0, 0))

'Save the document.

document.Save("Output.pdf")

'Close the document.

document.Close(True)

{% endhighlight %}

You can add text using the font file from local file system by providing the path of the TrueType font location. The following code snippet explains the same.

{% highlight c# %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Provide the path of the local *.ttf file

PdfFont font = new PdfTrueTypeFont(new Font("Arial.ttf", 14));

//Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));

//Save the document.

document.Save("Output.pdf");

//Close the document.

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim document As New PdfDocument()

'Add a page to the document.

Dim page As PdfPage = document.Pages.Add()

'Create PDF graphics for the page.

Dim graphics As PdfGraphics = page.Graphics

' Provide the path of the local *.ttf file

Dim font As PdfFont = New PdfTrueTypeFont(New Font("Arial.ttf", 14))

'Draw the text.

graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, New PointF(0, 0))

'Save the document.

document.Save("Output.pdf")

'Close the document.

document.Close(True)

{% endhighlight %}

{% endtabs %}

### Draw text using CJK fonts

You can add text using CJK fonts by using the following code sample,

{% tabs %}

{% highlight c# %}

//Create a new PDF document.
PdfDocument document = new PdfDocument();

//Add a page to the document.
PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.
PdfGraphics graphics = page.Graphics;

//Set the standard font.
PdfFont font = new PdfCjkStandardFont(PdfCjkFontFamily.HeiseiMinchoW3, 20);

//Draw the text.
graphics.DrawString("こんにちは世界", font, PdfBrushes.Black, new PointF(0, 0));

//Save the document.
document.Save("Output.pdf");

//Close the document.
document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document.
Dim document As New PdfDocument()

'Add a page to the document.
Dim page As PdfPage = document.Pages.Add()

'Create PDF graphics for the page.
Dim graphics As PdfGraphics = page.Graphics

'Set the standard font.
Dim font As PdfFont = New PdfCjkStandardFont(PdfCjkFontFamily.HeiseiMinchoW3, 20)

'Draw the text.
graphics.DrawString("こんにちは世界", font, PdfBrushes.Black, New PointF(0, 0))

'Save the document.
document.Save("Output.pdf")

'Close the document.
document.Close(True)

{% endhighlight %}

{% endtabs %}

## Embedding fonts and working with Unicode text

To embed a font or display Unicode text in the document, the ‘Unicode’ Boolean parameter of the PdfTrueTypeFont constructor has to be set to true. The following code illustrates the same.

N> To render a Unicode text in the PDF document the chosen font should have the Unicode rendering capability.

{% tabs %}

{% highlight c# %}

//Create a new PDF document.

PdfDocument document = new PdfDocument();

//Add a page to the document.

PdfPage page = document.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//use the system installed font

PdfFont font = new PdfTrueTypeFont(new Font("Arial Unicode MS", 14), true);

//Read the unicode text from the text file.

StreamReader reader = new StreamReader(@"input.txt", Encoding.Unicode);

string text = reader.ReadToEnd();

reader.Close();

//Draw the text.

graphics.DrawString(text, font, PdfBrushes.Black, new PointF(0, 0));

//Save the document.

document.Save("Output.pdf");

//Close the document.

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim document As New PdfDocument()

'Add a page to the document.

Dim page As PdfPage = document.Pages.Add()

'Create PDF graphics for the page.

Dim graphics As PdfGraphics = page.Graphics

'use the system installed font

Dim font As PdfFont = New PdfTrueTypeFont(New Font("Arial Unicode MS", 14), True)

'Read the unicode text from the text file.

Dim reader As New StreamReader("input.txt", Encoding.Unicode)

Dim text As String = reader.ReadToEnd()

reader.Close()

'Draw the text.

graphics.DrawString(text, font, PdfBrushes.Black, New PointF(0, 0))

'Save the document.

document.Save("Output.pdf")

'Close the document.

document.Close(True)

{% endhighlight %}

{% endtabs %}

## Drawing Right-To-Left text 

Essential PDF allows you to add RTL text in the PDF document by using the RightToLeft property in the PdfStringFormat class, the following code snippet illustrates how to add RTL text in the PDF document.

{% tabs %}

{% highlight c# %}

//Create a new PDF document.

PdfDocument doc = new PdfDocument();

//Add a page to the document.

PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page

PdfGraphics graphics = page.Graphics;

//Set the font with Unicode option.

Font font = new Font("Arial", 14);

PdfFont pdfFont = new PdfTrueTypeFont(font, true);

//Set the format for string.

PdfStringFormat format = new PdfStringFormat();

//Set the format as RTL type.

format.RightToLeft = true;

//Set the alignment.

format.Alignment = PdfTextAlignment.Right;

//Read the RTL text from the text file.

StreamReader reader = new StreamReader(@"input.txt", Encoding.Unicode);

string textWithHebrew = reader.ReadToEnd();

reader.Close();

graphics.DrawString(textWithHebrew, pdfFont, PdfBrushes.Black, new RectangleF(0, 0, page.GetClientSize().Width, page.GetClientSize().Height), format);

//Save the document.

doc.Save("Output.pdf");

//Close the document.

doc.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim doc As New PdfDocument()

'Add a page to the document.

Dim page As PdfPage = doc.Pages.Add()

'Create PDF graphics for the page

Dim graphics As PdfGraphics = page.Graphics

'Set the font with Unicode option.

Dim font As New Font("Arial", 14)

Dim pdfFont As PdfFont = New PdfTrueTypeFont(font, True)

'Set the format for string.

Dim format As New PdfStringFormat()

'Set the format as RTL type.

format.RightToLeft = True

'Set the alignment.

format.Alignment = PdfTextAlignment.Right

'Read the RTL text from the text file.

Dim reader As New StreamReader("input.txt", Encoding.Unicode)

Dim textWithHebrew As String = reader.ReadToEnd()

reader.Close()

graphics.DrawString(textWithHebrew, pdfFont, PdfBrushes.Black, New RectangleF(0, 0, page.GetClientSize().Width, page.GetClientSize().Height), format)

'Save the document.

doc.Save("Output.pdf")

'Close the document.

doc.Close(True)

{% endhighlight %}

{% endtabs %}

## Adding a HTML Styled Text

Essential PDF provides support to render simple HTML string in a PDF document that can flow through multiple pages. This can be done by using the PdfHTMLTextElement class.

1. The PdfHTMLTextElement class provides support for a basic set of HTML tags, to render HTML format text in the PDF document.

   Supported tags (Should be XHTML-compliant)

   * Font
   * B
   * I
   * U
   * Sub
   * Sup
   * BR
   
2. The PdfMetafileLayoutFormat class enables to break the HTML text into multiple pages.
3. Complex HTML with CSS are not supported in this class. Please use [HTML to PDF](/file-formats/pdf/working-with-document-conversions#converting-html-documents-to-pdf "Converting HTML documents To PDF") section for complex HTML with CSS and URL's

The following code example illustrates how to render the HTML string in a PDF document.   

{% tabs %}

{% highlight c# %}

//Create a new PDF document.

PdfDocument doc = new PdfDocument();

//Add a page to the document.

PdfPage page = doc.Pages.Add();

//Create PDF graphics for the page.

PdfGraphics graphics = page.Graphics;

//Set the font.

PdfFont font = new PdfStandardFont(PdfFontFamily.Courier, 14);

//Simple HTML content

string htmlText = "<font color='#0000F8'>Essential PDF</font> is a <u><i>.NET</i></u> " +

"library with the capability to produce Adobe PDF files ";

//Render HtmlText.

PdfHTMLTextElement richTextElement = new PdfHTMLTextElement(htmlText, font, PdfBrushes.Black);

richTextElement.TextAlign = TextAlign.Left;

//Format Layout.

PdfMetafileLayoutFormat format = new PdfMetafileLayoutFormat();

format.Layout = PdfLayoutType.Paginate;

format.Break = PdfLayoutBreakType.FitPage;



//Draw htmlString.

richTextElement.Draw(page, new RectangleF(0, 20, page.GetClientSize().Width, page.GetClientSize().Height), format);

//Save the document.

doc.Save("Output.pdf");

//Close the document.

doc.Close(true);



{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim doc As New PdfDocument()

'Add a page to the document.

Dim page As PdfPage = doc.Pages.Add()

'Create PDF graphics for the page.

Dim graphics As PdfGraphics = page.Graphics

'Set the font.

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Courier, 14)

'Simple HTML content

Dim htmlText As String = "<font color='#0000F8'>Essential PDF</font> is a <u><i>.NET</i></u> " + "library with the capability to produce Adobe PDF files "

'Render HtmlText.

Dim richTextElement As New PdfHTMLTextElement(htmlText, font, PdfBrushes.Black)

richTextElement.TextAlign = TextAlign.Left

'Format Layout.

Dim format As New PdfMetafileLayoutFormat()

format.Layout = PdfLayoutType.Paginate

format.Break = PdfLayoutBreakType.FitPage

'Draw htmlString.

richTextElement.Draw(page, New RectangleF(0, 20, page.GetClientSize().Width, page.GetClientSize().Height), format)

'Save the document.

doc.Save("Output.pdf")

'Close the document.

doc.Close(True)

{% endhighlight %}

{% endtabs %}

## Creating a multicolumn PDF document

Essential PDF allows you to create multi-column text in PDF document by using PdfTextElement class. The following code example illustrates the same.

{% tabs %}

{% highlight c# %}

//Create a PDF document instance

PdfDocument document = new PdfDocument();

//Add page to the document

PdfPage page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

string text = "Adventure Works Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company. The company manufactures and sells metal and composite bicycles to North American, European and Asian commercial markets. While its base operation is located in Washington with 290 employees, several regional sales teams are located throughout their market base.";

//Create a text element with the text and font

PdfTextElement textElement = new PdfTextElement(text, new PdfStandardFont(PdfFontFamily.TimesRoman, 14));

//Draw the text in the first column

textElement.Draw(page, new RectangleF(0, 0, page.GetClientSize().Width / 2, page.GetClientSize().Height));

textElement = new PdfTextElement(text, new PdfStandardFont(PdfFontFamily.TimesRoman, 14));

//Draw the text in the second column

textElement.Draw(page, new RectangleF(page.GetClientSize().Width / 2, 0, page.GetClientSize().Width / 2, page.GetClientSize().Height));

document.Save("Output.pdf");

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a PDF document instance

Dim document As New PdfDocument()

'Add page to the document

Dim page As PdfPage = document.Pages.Add()

Dim graphics As PdfGraphics = page.Graphics

Dim text As String = "Adventure Works Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company. The company manufactures and sells metal and composite bicycles to North American, European and Asian commercial markets. While its base operation is located in Washington with 290 employees, several regional sales teams are located throughout their market base."

'Create a text element with the text and font

Dim textElement As New PdfTextElement(text, New PdfStandardFont(PdfFontFamily.TimesRoman, 14))

'Draw the text in the first column

textElement.Draw(page, New RectangleF(0, 0, page.GetClientSize().Width / 2, page.GetClientSize().Height))

textElement = New PdfTextElement(text, New PdfStandardFont(PdfFontFamily.TimesRoman, 14))

'Draw the text in the second column

textElement.Draw(page, New RectangleF(page.GetClientSize().Width / 2, 0, page.GetClientSize().Width / 2, page.GetClientSize().Height))

document.Save("Output.pdf")

document.Close(True)

{% endhighlight %}

{% endtabs %}

The PdfLayoutFormat class helps to allow the text to flow across pages. The PdfLayoutResult class provides the rendered bounds of the previously added text which can be used to place successive elements without overlapping.

The following code snippet illustrates how to add elements relatively and also allow the text to flow across multiple pages.

{% tabs %}

{% highlight c# %}

//Create a PDF document instance

PdfDocument document = new PdfDocument();

//Add page to the document

PdfPage page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

//Read the long text from the text file.

StreamReader reader = new StreamReader(@"input.txt", Encoding.ASCII);

string text = reader.ReadToEnd();

reader.Close();



const int paragraphGap = 10;



//Create a text element with the text and font

PdfTextElement textElement = new PdfTextElement(text, new PdfStandardFont(PdfFontFamily.TimesRoman, 14));

PdfLayoutFormat layoutFormat = new PdfLayoutFormat();

layoutFormat.Layout = PdfLayoutType.Paginate;

layoutFormat.Break = PdfLayoutBreakType.FitPage;



//Draw the first paragraph

PdfLayoutResult result = textElement.Draw(page, new RectangleF(0, 0, page.GetClientSize().Width / 2, page.GetClientSize().Height), layoutFormat);

//Draw the second paragraph from the first paragraph end position

result = textElement.Draw(page, new RectangleF(0, result.Bounds.Bottom + paragraphGap, page.GetClientSize().Width / 2, page.GetClientSize().Height), layoutFormat);

document.Save("Output.pdf");

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a PDF document instance

Dim document As New PdfDocument()

'Add page to the document

Dim page As PdfPage = document.Pages.Add()

Dim graphics As PdfGraphics = page.Graphics

'Read the RTL text from the text file.

Dim reader As New StreamReader("input.txt", Encoding.ASCII)

Dim text As String = reader.ReadToEnd()

reader.Close()

Const paragraphGap As Integer = 10

'Create a text element with the text and font

Dim textElement As New PdfTextElement(text, New PdfStandardFont(PdfFontFamily.TimesRoman, 14))

Dim layoutFormat As New PdfLayoutFormat()

layoutFormat.Layout = PdfLayoutType.Paginate

layoutFormat.Break = PdfLayoutBreakType.FitPage

'Draw the first paragraph

Dim result As PdfLayoutResult = textElement.Draw(page, New RectangleF(0, 0, page.GetClientSize().Width / 2, page.GetClientSize().Height), layoutFormat)

'Draw the second paragraph from the first paragraph end position

result = textElement.Draw(page, New RectangleF(0, result.Bounds.Bottom + paragraphGap, page.GetClientSize().Width / 2, page.GetClientSize().Height), layoutFormat)

document.Save("Output.pdf")

document.Close(True)

{% endhighlight %}

{% endtabs %}

## Inserting Rich Text Format contents 

Essential PDF allows you to insert a RTF text into a PDF document.

The following code example illustrates how to insert RTF text in PDF document.

{% tabs %}

{% highlight c# %}

//Create a new PDF document.

PdfDocument doc = new PdfDocument();

//Add a page.

PdfPage page = doc.Pages.Add();

SizeF bounds = page.GetClientSize();

//Read RTF document.

StreamReader reader = new StreamReader(@"input.rtf", Encoding.ASCII);

string text = reader.ReadToEnd();

reader.Close();

//Convert it to Metafile.

PdfMetafile imageMetafile = (PdfMetafile)PdfImage.FromRtf(text, bounds.Width, PdfImageType.Metafile);

PdfMetafileLayoutFormat format = new PdfMetafileLayoutFormat();

//Allow text to flow multiple pages without any break.

format.SplitTextLines = true;

//Draws image.

imageMetafile.Draw(page, 0, 0, format);

//Save the document.

doc.Save("Output.pdf");

doc.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a new PDF document.

Dim doc As New PdfDocument()

'Add a page.

Dim page As PdfPage = doc.Pages.Add()

Dim bounds As SizeF = page.GetClientSize()

'Read RTF document.

Dim reader As New StreamReader("input.rtf", Encoding.ASCII)

Dim text As String = reader.ReadToEnd()

reader.Close()

'Convert it to Metafile.

Dim imageMetafile As PdfMetafile = DirectCast(PdfImage.FromRtf(text, bounds.Width, PdfImageType.Metafile), PdfMetafile)

Dim format As New PdfMetafileLayoutFormat()

'Allow text to flow multiple pages without any break.

format.SplitTextLines = True

'Draws image.

imageMetafile.Draw(page, 0, 0, format)

'Save the document.

doc.Save("Output.pdf")

doc.Close(True)

{% endhighlight %}

{% endtabs %}


N> For converting complex RTF content to PDF, refer the [RTF to PDF](/file-formats/pdf/working-with-document-conversions#converting-rtf-documents-to-pdf "Working with document conversions") section.

## Adding an Ordered List 


Essential PDF allows you to create an ordered list in the document. Ordered List is represented by the PdfOrderedList class and can be numerical or alphabetical. The following code snippet illustrates the same.

{% tabs %}

{% highlight c# %}

//Create a new instance of PdfDocument class.

PdfDocument document = new PdfDocument();

//Add a new page to the document.

PdfPage page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

SizeF size = page.Graphics.ClientSize;

//Create font 

PdfFont font = new PdfStandardFont(PdfFontFamily.TimesRoman, 10, PdfFontStyle.Italic);

string[] products = { "Tools", "Grid", "Chart", "Edit", "Diagram", "XlsIO", "Grouping", "Calculate", "PDF", "HTMLUI", "DocIO" };

//Create string format

PdfStringFormat format = new PdfStringFormat();

format.LineSpacing = 10f;

//Create Ordered list

PdfOrderedList pdfList = new PdfOrderedList();

pdfList.Marker.Brush = PdfBrushes.Black;

pdfList.Indent = 20;

//Set format for sub list

pdfList.Font = font;

pdfList.StringFormat = format;

foreach (string s in products)

{

//Add items

pdfList.Items.Add(string.Concat("Essential ", s));

}

pdfList.Draw(page, new RectangleF(0, 20, size.Width, size.Height));  

// Save and close the document.

document.Save("Output.pdf");

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}

'Create a new instance of PdfDocument class.

Dim document As New PdfDocument()

'Add a new page to the document.

Dim page As PdfPage = document.Pages.Add()

Dim graphics As PdfGraphics = page.Graphics

Dim size As SizeF = page.Graphics.ClientSize

'Create font 

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.TimesRoman, 10, PdfFontStyle.Italic)

Dim products As String() = {"Tools", "Grid", "Chart", "Edit", "Diagram", "XlsIO", _

"Grouping", "Calculate", "PDF", "HTMLUI", "DocIO"}

'Create string format

Dim format As New PdfStringFormat()

format.LineSpacing = 10.0F

'Create Ordered list

Dim pdfList As New PdfOrderedList()

pdfList.Marker.Brush = PdfBrushes.Black

pdfList.Indent = 20

'Set format for sub list

pdfList.Font = font

pdfList.StringFormat = format

For Each s As String In products

'Add items

pdfList.Items.Add(String.Concat("Essential ", s))

Next

pdfList.Draw(page, New RectangleF(0, 20, size.Width, size.Height))

' Save and close the document.

document.Save("Output.pdf")

document.Close(True)

{% endhighlight %}

{% endtabs %}

## Adding an Unordered List 

Essential PDF also provides support to create an unordered List that is represented by the PdfUnorderedList class. An Unordered list can be bullets, circle or an image. The following code snippet illustrates the same.

{% tabs %}

{% highlight c# %}

//Create a new instance of PdfDocument class.

PdfDocument document = new PdfDocument();

//Add a new page to the document.

PdfPage page = document.Pages.Add();

PdfGraphics graphics = page.Graphics;

SizeF size = page.Graphics.ClientSize;

//Create an unordered list

PdfUnorderedList list = new PdfUnorderedList();

//Set the marker style

list.Marker.Style = PdfUnorderedMarkerStyle.Disk;

//Create font and write title

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 12, PdfFontStyle.Regular);

//Create string format

PdfStringFormat format = new PdfStringFormat();

format.LineSpacing = 10f;

// Format list

list.Font = font;

list.StringFormat = format;

//Set list indent

list.Indent = 10;

//Add items to the list

list.Items.Add("PDF");

list.Items.Add("XlsIO");

list.Items.Add("DocIO");

list.Items.Add("PPT");

//Set text indent

list.TextIndent = 10;

//Draw list

list.Draw(page, new RectangleF(0, 10, size.Width, size.Height));

// Save and close the document.

document.Save("Output.pdf");

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Create a new instance of PdfDocument class.

Dim document As New PdfDocument()

'Add a new page to the document.

Dim page As PdfPage = document.Pages.Add()

Dim graphics As PdfGraphics = page.Graphics

Dim size As SizeF = page.Graphics.ClientSize

'Create an unordered list

Dim list As New PdfUnorderedList()

'Set the marker style

list.Marker.Style = PdfUnorderedMarkerStyle.Disk

'Create font and write title

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 12, PdfFontStyle.Regular)

'Create string format

Dim format As New PdfStringFormat()

format.LineSpacing = 10.0F

' Format list

list.Font = font

list.StringFormat = format

'Set list indent

list.Indent = 10

'Add items to the list

list.Items.Add("PDF")

list.Items.Add("XlsIO")

list.Items.Add("DocIO")

list.Items.Add("PPT")

'Set text indent

list.TextIndent = 10

'Draw list

list.Draw(page, New RectangleF(0, 10, size.Width, size.Height))

'Save and close the document.

document.Save("Output.pdf")

document.Close(True)

{% endhighlight %}

{% endtabs %}

## Replace Fonts in an existing document

Essential PDF allows you to replace the fonts in an existing PDF document by using the Replace method. The following code snippets illustrates the same.

{% tabs %}

{% highlight c# %}

//Creates a new PDF document.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");

//Replace font 
loadedDocument.UsedFonts[0].Replace(new PdfStandardFont(PdfFontFamily.TimesRoman, 12));

//Save the document
loadedDocument.Save("Output.pdf");

loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Creates a new PDF document.

Dim loadedDocument As New PdfLoadedDocument("Input.pdf")

'Replace font

loadedDocument.UsedFonts(0).Replace(New PdfStandardFont(PdfFontFamily.TimesRoman, 12))

'Save the document

loadedDocument.Save("Output.pdf")

loadedDocument.Close(True)

{% endhighlight %}

{% endtabs %}

## Search and get the bounds of a text in a document

You can search for a particular text in a document and get the bounds. To include this functionality, you need to add the below mentioned assemblies as reference to the project.

1. Syncfusion.Compression.Base.dll
2. Syncfusion.Pdf.Base.dll
3. Syncfusion.PdfViewer.Windows.dll 

The following code snippet illustrates how to get the bound of a text from PDF document.

{% tabs %}

{% highlight c# %}

PdfViewerControl documentViewer = new PdfViewerControl();

//Load the PDF document

documentViewer.Load("Input.pdf");

//Get the occurrences of the target text and location.

Dictionary<int, List<RectangleF>> textSearch = new Dictionary<int, List<RectangleF>>();

bool IsMatchFound = documentViewer.FindText("hello", out textSearch);

documentViewer.Dispose();

{% endhighlight %}

{% highlight vb.net %}

Dim documentViewer As New PdfViewerControl()

'Load the PDF document

documentViewer.Load("Input.pdf")

'Get the occurrences of the target text and location.

Dim textSearch As New Dictionary(Of Integer, List(Of RectangleF))()

Dim IsMatchFound As Boolean = documentViewer.FindText("hello", textSearch)

documentViewer.Dispose()

{% endhighlight %}

{% endtabs %}