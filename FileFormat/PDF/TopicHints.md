* Overview

Key Features of Essential PDF

* Getting Started
  * Creating a simple PDF document with basic elements
  * Creating and filling forms
  * Converting HTML contents to PDF document
  * Merge PDF documents 
* Concepts and Features
* Essential PDF Document Object Model
* Working with Document
  * Adding the Page settings
  * Creating sections in a PDF
  * Printing PDF document
  * Manipulating document properties
  * Choosing the viewer preferences
* Working with Pages
  * Adding a new page to the document
  * Importing pages from an existing document.
  * Inserting pages in a document
  * Removing pages from a document
  * Splitting a PDF file to individual pages
* Working with text
    * Drawing text in the PDF page
    * Drawing Right-To-Left text 
    * Adding a HTML Styled Text
    * Creating a multicolumn PDF document
    * Inserting Rich Text Format contents 
    * Adding an Ordered List 
    * Adding an Unordered List 
    * Replace Fonts in an existing document
    * Search and get the bounds of a text in a document
  * Working with Images
    * Inserting a raster image 
    * Inserting a vector image 
    * Working with Image Masking
    * Replacing images in an existing document.
  * Working with Tables
    * Creating a simple table
    * Support for cell customizations
    * Support for row and column customizations
    * Choosing between a PdfLightTable and a PdfGrid
  * Working with Forms
    * Creating a new PDF form
    * Modifying the location and properties of an existing form field
    * Filling form fields of an existing PDF 
    * Flattening Form Fields of a PDF document
* Merge Documents
    * Merging multiple documents from disk and stream
    * Merging two documents using Append method
    * Importing and rearranging pages from multiple documents
    * Best practices
* Working with Text Extraction
  * Working with basic text extraction
  * Working with layout based text extraction
* Working with Image Extraction
* Working with Document Conversions
    * HTML To PDF
      * Conversion by using IE Rendering
        * Prerequisites and setting up the conversion for IE9 and later
        * Converting the URL to a PDF document
        * Converting the HTML string to PDF document
        * Converting the Windows Authenticated website to PDF document
        * Converting the webpages to PDFA conformance
        * Troubleshooting
      * Conversion by using WebKit Rendering
        * Prerequisites and setting up the WebKit engine for conversion
        * Converting the URL to a PDF document
        * Converting the HTML string to PDF document
        * Converting an SVG to PDF
        * Troubleshooting
    * Working with Word to PDF
    * Working with Tiff to PDF
    * Working with RTF to PDF
    * Working with XPS to PDF
    * Working with HTML to Image
    * Working with PDF to Image
  * Working with Optical Character Recognition(OCR)
    * Prerequisites and setting up the Tesseract Engine
    * Performing OCR for an entire document
    * Performing OCR for a region of the document
    * Best Practices
    * Troubleshooting
* Working with Hyperlinks
* Working with PDF Templates
* Working with Pagination
    * Paginating a text element
    * Paginating an embedded image
    * Paginating a large table
* Working with Headers and Footers
    * Adding an automatic field in header and footer
  * Working with Shapes
  * Working with Bookmarks
    * Adding Bookmarks in a PDF
    * Inserting Bookmarks in an existing PDF
    * Removing Bookmarks from an existing PDF 
  * Working with Annotations
    * Adding annotations to a PDF document
    * Supported annotation types
    * Removing annotations from an existing PDF 
  * Working with Attachments
    * Adding attachment in a PDF
    * Removing attachment from an existing PDF 
    * Extracting and saving an attachment to the disk.
* Security
  * Working with RC4 Encryption 
  * Working with AES Encryption 
* Working with Digitally Signature
  * Adding a timestamp in digital signature
* Working with Barcode
  * Adding a barcode to the PDF document
  * Supported barcode types
* Working with Actions
  * Adding an action to the PDF
  * Supported action types
  * Adding an action to the form field
  * Adding an action to the bookmarks
* Working with Stamps, Watermarks and Overlay
* Working with Portfolio
* Working with Layers
  * Adding multiple layers in PDF page
  * Toggling the visibility of layers
  * Merging multiple layers in an existing PDF document.
  * Working with Tagged PDF
  * Working with Compression
    * Working with content compression
    * Working with image compression
* PDF Conformance
  * Adding support for PDF/A-1b conformance.
  * Adding support for PDF/X-1a conformance.
* Metadata (XMP)
  * Working with the XMP metadata
  * Supported Schema types
* Adding Custom Metadata to the PDF document
    * Working with colorspace
      * Supported colorspaces

**Getting** **Started**

**Creating** **a** **simple** **PDF** **document** **with** **basic** **elements**

1. Adding assembly reference in an application (Compression.Base & Pdf.Base)
      a. Describe about the dependent assembly, namespace details required for using the Essential PDF
2. Creating new instance for PDF document by using Essential PDF.
3. Essential PDF has a set of APIs similar to the .NET GDI plus that helps to draw elements to the PDF page just like 2D drawing in .NET
4. Unlike System.Drawing APIs all the units are measured in Point instead of pixel. The Essential PDF’s unit converter API helps to convert the value in pixel to point and vice versa.
5. In PDF, all the elements are placed in absolute positions and the layout result of each element provides the rendered bounds that can be used to avoid content overlapping.
6. The Drawstring method of the page graphics helps add the text to the page. The code example adds the necessary text create a basic invoice application.

<<<Code for adding text>>

7. The DrawImage method helps add image in a PDF page. Essential PDF supports a variety of scalar images such as bitmap, jpeg, gif, Tiff etc., and Metafile vector image.

<<Code for adding invoice logo>>

8. Essential PDF provides two types of table models. 
      a. PdfLightTable – used to create table with complex customizations support
      b. PdfGrid – table that provides simple cell customizations.

Since the invoice document requires only a simple customization, the given code example explains how to create a simple invoice table

<<Code for adding invoice table>>

**Creating** **and** **filling** **forms**

1. How to add form fields to pdf page.
2. Setting various properties to the form field.
3. Making the form field readonly. 
4. Loading an existing form document.
5. Enumerating the form fields in the PDF document.
6. Filling the form fields
7. Flattening the form fields.

**Converting** **HTML** **contents** **to** **PDF**

1. Converting simple HTML content by using PdfHTMLTextElement
2. Use cases and when to choose PdfHTMLTextElement
3. Converting URL / complex HTML content to PDF by using HTMLConverter class.
4. When to choose IE rendering engine and when to choose WebKit converter.
5. Prerequisites for WebKit converter.
6. Converting an URL to PDF by using WebKit converter.
7. Converting a HTML string to PDF 
8. Converting authenticated HTML page to PDF.

**Merge** **PDF** **Documents**

1. Combining two documents by using Append method
2. Combining multiple documents from disk.
3. Combining multiple documents from stream.

**Concepts** **and** **Features**

**Essential** **PDF** **Document** **Object** **Model**

* Essential PDF represents the PDF document as a DOM
* The DOM can be accessed and manipulated to read and modify documents.

This object model can be used to manipulate the PDF document as required

**Working** **with** **Document**

**Adding** **the** **Page** **settings**

Essential PDF supports various page setting options to control the page display, 

1. You can choose the standard or custom page size when you add a page to the PDF document

This example illustrates how to create a PDF document with standard page size,

<table>
<tr>
<td>
**[****C****#]**<br/><br/>//Creates a new PDF document.<br/><br/>PdfDocument document = new PdfDocument();<br/><br/>// Sets the page size.<br/><br/>document.PageSettings.Size = PdfPageSize.A4;<br/><br/>//Adds a page to the document.<br/><br/>PdfPage page = document.Pages.Add();<br/><br/>//Creates PDF graphics for the page.<br/><br/>PdfGraphics graphics = page.Graphics;<br/><br/>//Sets the font.<br/><br/>PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);<br/><br/>//Draws the text.<br/><br/>graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));<br/><br/>//Saves the document.<br/><br/>document.Save("Output.pdf");<br/><br/>//Closes the document.<br/><br/>document.Close(true);<br/><br/></td></tr>
</table>
This example illustrates how to create a PDF document with custom page size

<table>
<tr>
<td>
**[****C****#]**<br/><br/>//Creates a new PDF document.<br/><br/>PdfDocument document = new PdfDocument();<br/><br/>// Sets the custom page size.<br/><br/>document.PageSettings.Size = new SizeF(200,300);<br/><br/>//Adds a page to the document.<br/><br/>PdfPage page = document.Pages.Add();<br/><br/>//Creates PDF graphics for the page.<br/><br/>PdfGraphics graphics = page.Graphics;<br/><br/>//Sets the font.<br/><br/>PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);<br/><br/>//Draws the text.<br/><br/>graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));<br/><br/>//Saves the document.<br/><br/>document.Save("Output.pdf");<br/><br/>//Closes the document.<br/><br/>document.Close(true);<br/><br/></td></tr>
</table>
2. You can change page orientation from portrait to landscape and vice versa.
<table>
<tr>
<td>
<br/>**[****C****#]**<br/><br/>//Creates a new PDF document.<br/><br/>PdfDocument document = new PdfDocument();<br/><br/>// Sets the page size.<br/><br/>document.PageSettings.Size = PdfPageSize.A4;<br/><br/>//Change the page orientation to landscape<br/><br/>document.PageSettings.Orientation = PdfPageOrientation.Landscape;<br/><br/>//Adds a page to the document.<br/><br/>PdfPage page = document.Pages.Add();<br/><br/>//Creates PDF graphics for the page.<br/><br/>PdfGraphics graphics = page.Graphics;<br/><br/>//Sets the font.<br/><br/>PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);<br/><br/>//Draws the text.<br/><br/>graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));<br/><br/>//Saves the document.<br/><br/>document.Save("Output.pdf");<br/><br/>//Closes the document.<br/><br/>document.Close(true);<br/><br/></td></tr>
</table>
3. You can also change orientation by setting the rotation angle with PdfPageRotateAngle Enum
<table>
<tr>
<td>
<br/>**[****C****#]**<br/><br/>//Creates a new PDF document.<br/><br/>PdfDocument document = new PdfDocument();<br/><br/>// Sets the page size.<br/><br/>document.PageSettings.Size = PdfPageSize.A4;<br/><br/>//Change the page orientation to 90°<br/><br/>document.PageSettings.Rotate = PdfPageRotateAngle.RotateAngle90;<br/><br/>//Adds a page to the document.<br/><br/>PdfPage page = document.Pages.Add();<br/><br/>//Creates PDF graphics for the page.<br/><br/>PdfGraphics graphics = page.Graphics;<br/><br/>//Sets the font.<br/><br/>PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);<br/><br/>//Draws the text.<br/><br/>graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));<br/><br/>//Saves the document.<br/><br/>document.Save("Output.pdf");<br/><br/>//Closes the document.<br/><br/>document.Close(true);<br/><br/></td></tr>
</table>
**Creating** **sections** **in** **a** **PDF**

PDF sections are similar to PDF pages, you can add multiple pages into the sections to group the pages.

<table>
<tr>
<td>
**[****C****#]**<br/><br/>//Creates a new PDF document.<br/><br/>PdfDocument document = new PdfDocument();<br/><br/>//Adding a section to PDF document.<br/><br/>PdfSection section = document.Sections.Add();<br/><br/>//Adding pages to the section<br/><br/>PdfPage page = section.Pages.Add();<br/><br/>//Creates PDF graphics for the page//Creates PDF graphics for the page.<br/><br/>PdfGraphics graphics = page.Graphics;<br/><br/>//Sets the font.<br/><br/>PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);<br/><br/>//Draws the text.<br/><br/>graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));<br/><br/>//Saves the document.<br/><br/>document.Save("Output.pdf");<br/><br/>//Closes the document.<br/><br/>document.Close(true);<br/><br/></td></tr>
</table>
**Printing** **PDF** **document**

**Manipulating** **document** **properties**

Essential PDF allows you to set and read a file or document information of a PDF like Author, CreationDate, Subject, Title, Producer etc. The document information property of the PdfDocument or PdfLoadedDocument provides access to this information.

The following code example shows you how to set PDF document information.

<table>
<tr>
<td>
**[****C****#]**<br/><br/>//Creates a new PDF document.<br/><br/>PdfDocument document = new PdfDocument();<br/><br/>//Sets document information.<br/><br/>document.DocumentInformation.Author = "Syncfusion";<br/><br/>document.DocumentInformation.CreationDate = DateTime.Now;<br/><br/>document.DocumentInformation.Creator = "Essential PDF";<br/><br/>document.DocumentInformation.Keywords = "PDF";<br/><br/>document.DocumentInformation.Subject = "Document information DEMO";<br/><br/>document.DocumentInformation.Title = "Essential PDF Sample";<br/><br/>//Adds a page to the document.<br/><br/>PdfPage page = document.Pages.Add();<br/><br/>//Creates PDF graphics for the page.<br/><br/>PdfGraphics graphics = page.Graphics;<br/><br/>//Sets the font.<br/><br/>PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);<br/><br/>//Draws the text.<br/><br/>graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));<br/><br/>//Saves the document.<br/><br/>document.Save("Output.pdf");<br/><br/>//Closes the document.<br/><br/>document.Close(true);<br/><br/></td></tr>
</table>
The following code example shows you how to get PDF document information.

<table>
<tr>
<td>
**[****C****#]**<br/><br/>PdfLoadedDocument document = new PdfLoadedDocument("Input.pdf");<br/><br/>//Access the document information.       <br/><br/>Console.WriteLine(document.DocumentInformation.Author);<br/><br/>Console.WriteLine(document.DocumentInformation.Title);<br/><br/>Console.WriteLine(document.DocumentInformation.Subject);<br/><br/>Console.WriteLine(document.DocumentInformation.Keywords);<br/><br/>Console.WriteLine(document.DocumentInformation.Creator);<br/><br/>Console.WriteLine(document.DocumentInformation.Producer);<br/><br/></td></tr>
</table>
**Choosing** **the** **viewer** **preferences**

Essential PDF allows you to set various PDF viewer preferences to be used when the generated PDF document is displayed in a PDF viewer.

1. You can hide the viewer menu and toolbar.

<table>
<tr>
<td>
**[****C****#]**<br/><br/>//Creates a new PDF document.<br/><br/>PdfDocument document = new PdfDocument();<br/><br/>//Adds a page to the document.<br/><br/>PdfPage page = document.Pages.Add();<br/><br/>//Creates PDF graphics for the page.<br/><br/>PdfGraphics graphics = page.Graphics;<br/><br/>//Sets the font.<br/><br/>PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);<br/><br/>//Draws the text.<br/><br/>graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));<br/><br/>//Hides viewer application's menu bar.<br/><br/>document.ViewerPreferences.HideMenubar = true;<br/><br/>//Hides viewer application's toolbar.<br/><br/>document.ViewerPreferences.HideToolbar = true;<br/><br/>//Shows user interface elements in the document's window (such as scroll bars and navigation controls).<br/><br/>document.ViewerPreferences.HideWindowUI = false;<br/><br/><br/><br/>//Saves the document.<br/><br/>document.Save("Sample.pdf");<br/><br/>//Closes the document.<br/><br/>document.Close(true);<br/><br/></td></tr>
</table>
2. You can instruct the viewer to initially display the bookmarks, thumbnails or attachments by using  PdfPageMode ENUM
<table>
<tr>
<td>
<br/>**[****C****#]**<br/><br/>//Creates a new PDF document.<br/><br/>PdfDocument document = new PdfDocument();<br/><br/>//Adds a page to the document.<br/><br/>PdfPage page = document.Pages.Add();<br/><br/>//Creates PDF graphics for the page.<br/><br/>PdfGraphics graphics = page.Graphics;<br/><br/>//Sets the font.<br/><br/>PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20);<br/><br/>//Draws the text.<br/><br/>graphics.DrawString("Hello World!!!", font, PdfBrushes.Black, new PointF(0, 0));<br/><br/>//Shows the attachments panel.<br/><br/>document.ViewerPreferences.PageMode = PdfPageMode.UseAttachments;<br/><br/>//Saves the document.<br/><br/>document.Save("Sample.pdf");<br/><br/>//Closes the document.<br/><br/>document.Close(true);<br/><br/></td></tr>
</table>
3. You can select the page layout to one column, single page, two column left, two column right by using the PdfPageLayout ENUM

<<Code example>>

**Working** **with** **Pages**

**Adding** **a** **new** **page** **to** **the** **document**

The following code example explains how to add a page in a PDF document. The Add() method of the PdfPageCollection class adds the page at the end.

<<Code example>>

**Importing** **pages** **from** **an** **existing** **document****.**

Essential PDF allows you to import a page or import a range of pages from one document to the other. The following code example illustrates how to import a page to the existing document.

**Inserting** **pages** **in** **a** **document**

You can insert an empty page at any location of the document location, in the front, in the middle or at the end of the existing PDF document.

<<Code example>>

**Removing** **pages** **from** **a** **document**

You can remove the pages from the existing PDF document by using the PdfPageBase or index,

<<Code example>>

**Splitting** **a** **PDF** **file** **to** **individual** **pages**

Essential PDF allows to split existing PDF document into multiple individual pages into PDF document. 

<<Code example>>

**Working** **with** **text**

**Drawing** **text** **in** **the** **PDF** **page**

Essential PDF allows you to add text with various fonts to a PDF document,

1) You can add text by using the fonts installed in the system.

<<Code example>>

2) You can add text by using the font from local file system

<<Code example>>

3) You can add text by using the standard PDF fonts

<<Code example>>

4) You can add Unicode text in the PDF document by using the font with Unicode rendering capability

<<Code example>>

**Drawing** **Right****-****To****-****Left** **text** 

Essential PDF allows you to add RTL text in the PDF document by using the RightToLeft property in the PdfStringFormat class. The following code example shows you how to add RTL text in the PDF document.

<<Code example>>

**Adding** **a** **HTML** **Styled** **Text**

Essential PDF provides you support to render the HTML string in a PDF document that can flow to multiple pages by using the PdfHTMLTextElement class.

1) The PdfHTMLTextElement class provides you support for a basic set of HTML tags, to render HTML format text in the PDF document.
2) The PdfMetafileLayoutFormat class enables to break the HTML text into multiple pages.
3) Complex HTML CSS does not support using this class.

The following code example illustrates how to render the HTML string in a PDF document.

<<Code example>>

**Creating** **a** **multicolumn** **PDF** **document**

Essential PDF allows you to flow the text on multiple pages by using PdfLayoutFormat class. The following code example explains how to render the text in multi-column format. 

<<Code example>>

**Inserting** **Rich** **Text** **Format** **contents** 

Essential PDF allows you to insert a RTF text into a PDF document by using the FromRtf method in PdfImage. 

The following code example illustrate how to insert RTF text in PDF document,

<<Code example>>

**Adding** **an** **Ordered** **List** 

Essential PDF allows you to create an ordered list in the document. Ordered List is represented by the PdfOrderedList class and can be numerical or alphabetical.

<<Code example>>

**Adding** **an** **Unordered** **List** 

Essential Pdf also provides support to create an unordered List that is represented by the PdfUnorderedList class. An Unordered list can be bullets, circle or an image.

<<Code example>>

**Replace** **Fonts** **in** **an** **existing** **document**

Essential PDF allows you to replace the fonts from the existing PDF document by using the Replace method of the used font’s collections.

<<Code example>>

**Search** **and** **get** **the** **bounds** **of** **a** **text** **in** **a** **document**

**Working** **with** **Images**

**Inserting** **a** **raster** **image**

Essential PDF supports to insert a raster image such as JPEG, PNG, TIFF, BMP and GIF. You can load images from stream, file on disk and system Bitmap object.

1) You can draw unscaled images into PDF document 

<<Code example>>

2) You can scale images to fit a given rectangle in the PDF document,

<<Code example>>

3) You can draw the images into the existing PDF document

<<Code example>>

4) You can change the image quality and draw into the PDF document, image quality is 100 by default, which increases the resultant file size and quality. Reducing the quality will reduce the file size. 

<<Code example>>

**Inserting** **a** **vector** **image** 

Essential PDF supports to insert a vector image such as EMF, EMF Plus and EMF Plus Dual.

You can insert the vector images into the PDF document by using PdfMetafile class,

<<Code example>>

You can avoid text or image splitting across the pages by using the SplitImages and SplitTextLines properties in the PdfMetafileLayoutFormat class.

<<Code example>>

**Working** **with** **Image** **Masking**

You can mask the images into the PDF document by using PdfImageMask class

**Replacing** **images** **in** **an** **existing** **document****.**

Essential PDF allows you to replace the images in the existing PDF document by using the ReplaceImage method of the Page collection. 

The following code example shows you how to replace an image in the existing PDF document.

<<Code example>>

You can control the quality of an image that’s being replaced in the existing PDF document,

<<Code example>>

**Tables** 

**Creating** **a** **simple** **table** **using** **PdfLightTable** **model**

**PdfLightTable** is a table consisting of rows and columns that can be filled with data and rendered into the Page of the **PDF** Document. 

The following code example demonstrates how to create the PdfLightTable :

<<code example>>

**Creating** **a** **simple** **table** **using** **PdfGrid** **model**

**PdfGrid** is based on cell model that offers rich API for formatting and layout options that can be used to enter the data manually or from an external data source.

The following code example demonstrates how to create the PdfGrid:

<<code example>>

**Support** **for** **cell** **customizations** **using** **PdfLightTable** **model**

You can customize the cell by using the following properties.

**DefaultStyle**

You can specify the default cell style by using the DefaultStyle property

<<code example>>

**HeaderStyle**

You can set the style for the header cell by using the HeaderStyle property

<<code example>>

**AlternateStyle**

An alternate style can also be specified by using the AlternateStyle property. It is used to customize the appearance of the cells in the odd rows.

<<code example>>

**BackgroundBrush**

BackgroundBrush is the brush that draws the background of the cell.

<<code example>>

**Border**

Border is the pen with which the border of the cell is drawn.

<<code example>>

**Font**

Font is used to Get or set the font from where the text content of the cell is drawn.

<<code example>>

**StringFormat**

StringFormat is used to get or set the string format of the text.

<<code example>>

**TextBrush**

TextBrush is the brush with which the text is rendered.

<<code example>>

**TextPen**

TextPen is the pen that is used to draw text outlines.

<<code example>>

**Support** **for** **cell** **customizations** **using** **PdfGrid** **model**

You can customize the cell by using following properties.

**Columnspan** 

It is used to span the columns.

<<code example>>

**Height**

Height is used to  get the height of the particular cell.

<<code example>>

**ImagePosition**

Gets or sets the image alignment type of the background image.

<<code example>>

**Rowspan**

It is used to span the columns.

<<code example>>

**Stringformat**

StringFormat gets or sets the string format of the text.

<<code example>>

**Style** 

Style property is used to customize the cell content, text color, background color.

<<code example>>

**Value** 

Value property is used to specify  the value for individual cell and also to specify value of the another PdfGrid to make the nested table.

<<code example>>

**Width** 

Width is used to  get the width of the particular cell.

<<code example>>

**BackgroundBrush**

BackgroundBrush with that draws the background of the cell.

<<code example>>

**Borders**

Borders is the pen with which the border of the particular cell is drawn at the specified position.

<<code example>>

**Font**

It gets or sets the font with which the text content of the cell is drawn.

<<code example>>

**StringFormat**

StringFormat gets or sets the string format of the text.

<<code example>>

**TextBrush**

TextBrush is the brush with which the text is rendered.

<<code example>>

**TextPen**

TextPen is the pen that is used to draw text outlines.

<<code example>>

**BackgroundImage**

BackgroundImage is the image used to set the background image of the particular cell.

<<code example>>

**Shapes** 

Shape is the form of an object or its external boundary, outline, or external surface. It has the following varieties 

* Rectangle 
* Line
* Curve 
* Circle
* Arc
* Text and so on.

Shapes are filled by using different types of brushes like gradient brush, Tiling brush, and so on. **Essential** **PDF** supports drawing shapes with different color spaces and also allows to set the Transparency for shapes. 

<<code example>>

**Working** **with** **Forms** 

An interactive form, sometimes referred to as an AcroForm is a collection of fields for gathering information.

**PDF** document can contain any number of fields appearing in any combination of pages, all of that make a single, globally interactive form spanning the entire document

**Creating** **a** **new** **PDF** **form**

**Essential** **PDF** allows you to create forms in the **PDF**.

The **PdfForm** class provides a collection of named **Fields** that helps in managing form fields in **PDF** document.

**Adding** **TextBox** **field**

Text field is a box or space where you can enter text through the keyboard.

**PdfTextBoxField** class is used to create a textbox field in PDF forms. This class also provides support to create password and multiline text boxes. 

The following code example illustrates this.

<<Code example>>

**Adding** **Button** **field**

A button field represents an interactive control on the screen that you can manipulate by using the mouse. **PdfButtonField** class is used to create Buttons fields. 

<<Code example>>

**Adding** **Check** **Box** **field**

**PdfCheckBoxField** class is used to create a check box in **PDF** forms. You can customize the check box style by using properties such as **BorderStyle**, **HighlightMode**, **BorderWidth****,** etc.

<<Code example>>

**Adding** **Combo** **box** **field** 

**PdfComboBoxField** class is used to create a combo box field in **PDF** forms. You can add a list of items to the combo box by using the **PdfListFieldItem** class.

<<Code example>>

**Adding** **List** **box** **field**

**PdfListBoxField** is used to create the ListBox field in **PDF** forms.

<<Code example>>

**Adding** **Radio** **button** **field**

**PdfRadioButtonListField** class is used to create a radio button in the **PDF** Forms. You can create the radio button list items by using the **PdfRadioButtonListItem** class.

<<Code example>>

**Adding** **Signature** **Field**

**PdfSignatureField** class is used to create signature fields in **PDF** forms. **PdfSignature** class enables you to sign the signature field with the given certificate.

<<Code example>>

**Filling** **form** **fields** **of** **an** **existing** **PDF** 

**Essential** **PDF** provides you support to fill AcroForm fields. You can fill the form field value by using its field name or field index.

**[Filling the text box field](http://help.syncfusion.com/ug/windows forms/Documents/fillingthetextboxfield.htm# "")**

<<Code example>>

**[Filling the combo box field](http://help.syncfusion.com/ug/windows forms/Documents/fillingthecomboboxfield.htm# "")**

<<Code example>>

**[Filling the Radio button field](http://help.syncfusion.com/ug/windows forms/Documents/fillingtheradiobuttonfield.htm# "")**

<<Code example>>

**[Filling list box field](http://help.syncfusion.com/ug/windows forms/Documents/fillinglistboxfield.htm# "")**

<<Code example>>

**[Filling the check Box field](http://help.syncfusion.com/ug/windows forms/Documents/fillingthecheckboxfield.htm# "")**

<<Code example>>

**[Filling the signature field](http://help.syncfusion.com/ug/windows forms/Documents/fillingthesignaturefield.htm# "")**

<<Code example>>

**[Enumerate the form fields](http://help.syncfusion.com/ug/windows forms/Documents/enumeratetheformfields.htm# "")**

<<Code example>>

**Flattening** **Form** **Fields** **of** **a** **PDF** **document**

You can flatten the loaded field by using the **Flatten** property of the **PdfLoadedField** class. A particular field or the whole form can be flattened using this class.

<<Code example>>

**Merge** **Documents**

Essential PDF supports to merge the multiple PDF documents.

**Merging** **multiple** **documents** **from** **disk** **and** **stream**

You can merge the multiple PDF document by specifying the path of the documents in a string array.

Refer to the following code example to merge multiple documents from disk.

<<Code example>>

You can merge the documents by using the stream of the PDF documents. Refer to the following code example.

<<Code example>>

**Merging** **two** **documents** **using** **Append** **method**

Two files can also be merged by appending one file after another by using append method in the **PdfDocumentBase** class. The following code example illustrates this.

<<Code example>>

**Importing** **and** **rearranging** **pages** **from** **multiple** **documents**

You can import the pages from multiple documents by using ImportPageRange method. The following code example illustrates this.

<<Code example>>

**Best** **practices**

Merging multiple large **PDF** documents can lead to high memory usage. To optimize memory usage, you can use the following code example.

<<Code example>>

**Working** **with** **Text** **Extraction**

Essential PDF provides support to extract text from an existing PDF document. By using the ExtractText method, you can extract the text, page by page.

**Working** **with** **basic** **text** **extraction**

The extracted content is in the order of how the text is encoded in the PDF document.

Refer to the following code example for basic text extraction. 

<<Code example>>

**Working** **with** **layout** **based** **text** **extraction**

The extracted content is in the order of how it is viewed in the reader application.

Refer to the following code example for layout based text extraction

<<Code example>>

**Working** **with** **Image** **Extraction**

Essential PDF provides support to extract images from an existing PDF document. You can extract images by using the **ExtractImages** method in the **PdfLoadedPage** class.

The following code example illustrates how to extract images from a PDF document.

<<Code example>>

**HTML** **To** **PDF**

Essential PDF allows you to convert HTML page to PDF document. The converter has support for HTML5, CSS3, SVG, Web Fonts and JavaScript. This is done by using two different rendering engines. They are

* IE Rendering 
* WebKit Rendering 

**Conversion** **using** **IE** **Rendering**

**Prerequisites**

Use the following assemblies to convert HTML strings or URL’s to PDF document

1) Syncfusion.Compression.Base.dll
2) Syncfusion.Pdf.Base.dll
3) Syncfusion.HtmlConverter.Base.dll

**Converting** **the** **URL** **to** **a** **PDF** **document**

You can convert the http or https website to non-searchable PDF (bitmapped output) by using the following the code example.

<table>
<tr>
<td>
**[****C****#]**<br/><br/>//Creates a new PDF document.<br/><br/>PdfDocument pdfDocument = new PdfDocument();<br/><br/>pdfDocument.PageSettings.Margins.All = 0;<br/><br/>//Adds a page to the PDF document.<br/><br/>PdfPage page = pdfDocument.Pages.Add();<br/><br/>SizeF pageSize = page.GetClientSize().ToSize();<br/><br/>AspectRatio dimension = AspectRatio.KeepWidth;<br/><br/>HtmlConverter html = new HtmlConverter();<br/><br/>//Converts to Bitmap.<br/><br/>PdfUnitConvertor convertor = new PdfUnitConvertor();<br/><br/><br/><br/>float width = convertor.ConvertToPixels(pageSize.Width, PdfGraphicsUnit.Point);<br/><br/>float height = convertor.ConvertToPixels(pageSize.Height, PdfGraphicsUnit.Point);<br/><br/>Image img = html.ConvertToImage("http://www.google.com", ImageType.Bitmap, (int)width, (int)height, dimension);<br/><br/>PdfImage image = new PdfBitmap(img);<br/><br/>image.Draw(page, new RectangleF(0, 0, pageSize.Width, -1));<br/><br/>//Saves the document.<br/><br/>pdfDocument.Save("Output.pdf");<br/><br/>pdfDocument.Close(true);<br/><br/><br/><br/></td></tr>
</table>
You can convert the http or https website to searchable PDF (vector) by using the following code example.

<table>
<tr>
<td>
**[****C****#]**<br/><br/>//Creates a new PDF document.<br/><br/>PdfDocument pdfDocument = new PdfDocument();<br/><br/>pdfDocument.PageSettings.Margins.All = 0;<br/><br/>//Adds a page to the PDF document.<br/><br/>PdfPage page = pdfDocument.Pages.Add();<br/><br/>SizeF pageSize = page.GetClientSize().ToSize();<br/><br/>AspectRatio dimension = AspectRatio.KeepWidth;<br/><br/>HtmlConverter html = new HtmlConverter();<br/><br/>//Converts to Bitmap.<br/><br/>PdfUnitConvertor convertor = new PdfUnitConvertor();<br/><br/><br/><br/>float width = convertor.ConvertToPixels(pageSize.Width, PdfGraphicsUnit.Point);<br/><br/>float height = convertor.ConvertToPixels(pageSize.Height, PdfGraphicsUnit.Point);<br/><br/>Image img = html.ConvertToImage("http://www.google.com", ImageType.Bitmap, (int)width, (int)height, dimension);<br/><br/>PdfImage image = new PdfBitmap(img);<br/><br/>image.Draw(page, new RectangleF(0, 0, pageSize.Width, -1));<br/><br/>//Saves the document.<br/><br/>pdfDocument.Save("Output.pdf");<br/><br/>pdfDocument.Close(true);<br/><br/><br/><br/></td></tr>
</table>
**Converting** **the** **HTML** **string** **to** **PDF** **document**

You can convert the HTML string to PDF document. The following code example illustrates the same.

<table>
<tr>
<td>
**[****C****#]**<br/><br/>//Creates a new PDF document.<br/><br/>PdfDocument pdfDocument = new PdfDocument();<br/><br/>pdfDocument.PageSettings.Margins.All = 0;<br/><br/>//Adds a page to the PDF document.<br/><br/>PdfPage page = pdfDocument.Pages.Add();<br/><br/>SizeF pageSize = page.GetClientSize().ToSize();<br/><br/>AspectRatio dimension = AspectRatio.KeepWidth;<br/><br/>HtmlConverter html = new HtmlConverter();<br/><br/>//Converts to Bitmap.<br/><br/>PdfUnitConvertor convertor = new PdfUnitConvertor();<br/><br/>// Layout format for Metafile.<br/><br/>PdfMetafileLayoutFormat metafileFormat = new PdfMetafileLayoutFormat();<br/><br/>metafileFormat.Break = PdfLayoutBreakType.FitPage;<br/><br/>metafileFormat.Layout = PdfLayoutType.Paginate;<br/><br/>metafileFormat.SplitTextLines = false;<br/><br/>metafileFormat.SplitImages = false;<br/><br/>float width = convertor.ConvertToPixels(**pageSizhttp****://****msdn****.****microsoft****.****com****/****en****-****us****/****library****/****ee330732****(****v****=****vs****.****85****).****aspx****#****iviewobject****_****drawe**.Width, PdfGraphicsUnit.Point);<br/><br/>float height = convertor.ConvertToPixels(pageSize.Height, PdfGraphicsUnit.Point);<br/><br/>string htmlText = @"<html><head><title></title></head><body><dhttp://files2.syncfusion.com/dtsupport/directtrac/91655/IE9_RegistryEdit1127686967.zipiv>Hello World!!!&lt;/div&gt;&lt;/body&gt;&lt;/html&gt;";<br/><br/>HtmlToPdfResult result = html.Convert(htmlText,"", ImageType.Bitmap, (int)width, (int)height, dimension);<br/><br/>result.Render(page, metafileFormat);<br/><br/>pdfDocument.Save("Output.pdf");<br/><br/>pdfDocument.Close(true);<br/><br/></td></tr>
</table>
**Converting** **Windows** **Authenticated** **website** **to** **PDF** **document**

You can convert the Windows Authenticated websites to PDF document by providing the username and password. The following code example explains the same.

{% highlight c# %}
[C#]

//Creates a new PDF document.

PdfDocument pdfDocument = new PdfDocument();

pdfDocument.PageSettings.Margins.All = 0;

//Adds a page to the PDF document.

PdfPage page = pdfDocument.Pages.Add();

SizeF pageSize = page.GetClientSize().ToSize();

AspectRatio dimension = AspectRatio.KeepWidth;

HtmlConverter html = new HtmlConverter();

//Converts to Bitmap.

PdfUnitConvertor convertor = new PdfUnitConvertor();

// Layout format for Metafile.

PdfMetafileLayoutFormat metafileFormat = new PdfMetafileLayoutFormat();

metafileFormat.Break = PdfLayoutBreakType.FitPage;

metafileFormat.Layout = PdfLayoutType.Paginate;

metafileFormat.SplitTextLines = false;

metafileFormat.SplitImages = false;

float width = convertor.ConvertToPixels(pageSize.Width, PdfGraphicsUnit.Point);

float height = convertor.ConvertToPixels(pageSize.Height, PdfGraphicsUnit.Point);



//Windows authentication by providing username and password

HtmlToPdfResult result = html.Convert("http://www.example.com", ImageType.Bitmap, (int)width, (int)height, dimension, "xxx", "yyy");

result.Render(page, metafileFormat);

pdfDocument.Save("Output.pdf");

pdfDocument.Close(true);



{% endhighlight %}

**Converting** **the** **webpages** **to** **PDFA** **conformance**

You can convert the webpages to PDFA1B conformance and also you can embed all the fonts into the PDF document.

The following code snippet illustrate, how to embed fonts while converting webpage into PDF document and how to convert the webpage into PDF conformance

{% highlight c# %}
[C#]

//Creates a new PDFA1B document.

PdfDocument pdfDocument = new PdfDocument(PdfConformanceLevel.Pdf_A1B);

pdfDocument.PageSettings.Margins.All = 0;

//Adds a page to the PDF document.

PdfPage page = pdfDocument.Pages.Add();

SizeF pageSize = page.GetClientSize().ToSize();

AspectRatio dimension = AspectRatio.KeepWidth;

HtmlConverter html = new HtmlConverter();

//Converts to Bitmap.

PdfUnitConvertor convertor = new PdfUnitConvertor();

// Layout format for Metafile.

PdfMetafileLayoutFormat metafileFormat = new PdfMetafileLayoutFormat();

metafileFormat.Break = PdfLayoutBreakType.FitPage;

metafileFormat.Layout = PdfLayoutType.Paginate;

metafileFormat.SplitTextLines = false;

metafileFormat.SplitImages = false;

float width = convertor.ConvertToPixels(pageSize.Width, PdfGraphicsUnit.Point);

float height = convertor.ConvertToPixels(pageSize.Height, PdfGraphicsUnit.Point);



//Windows authentication by providing username and password

HtmlToPdfResult result = html.Convert("http://www.google.com", ImageType.Bitmap, (int)width, (int)height, dimension);

result.Render(page, metafileFormat);

pdfDocument.Save("Output.pdf");

pdfDocument.Close(true);



{% endhighlight %}

**Troubleshooting**

The following conditions may occur while converting HTML to PDF by using the IE rendering engine.

* Converted PDF document contains content as a Bitmap.
* Page break may not be applied in the resultant PDF document.
* Text cannot be selectable in the PDF document
* Converted PDF is blurry.

Most probably the above issue occurs due to the IE9 or above version of rendering engine and it is a known issue that generates only raster image. You can get more information on this from the following link,

[http://msdn.microsoft.com/en-us/library/ee330732(v=vs.85).aspx#iviewobject_draw](http://msdn.microsoft.com/en-us/library/ee330732(v=vs.85).aspx#iviewobject_draw "")

To overcome this issue, the key **FEATURE****_****IVIEWOBJECTDRAW****_****DMLT9****_****WITH****_****GDI** should be updated in the registry. This registry change should be updated in the machine where the HTML to PDF conversion takes place.

* You can add the key manually by following video link,

[http://files2.syncfusion.com/dtsupport/directtrac/91655/IE9_RegistryEdit1127686967.zip](http://files2.syncfusion.com/dtsupport/directtrac/91655/IE9_RegistryEdit1127686967.zip# "")

* You can run the utility placed in the following location to perform the above changes automatically.

$system drive:\Program Files\Syncfusion\Essential Studio\$Version # \Utilities\PDF\Legacy Drawing

When the issue still occurs, run the Legacy tool with elevated permission and make sure that the **FEATURE****_****IVIEWOBJECTDRAW****_****DMLT9****_****WITH****_****GDI** at both **HKEY****_****LOCAL****_****MACHINE** and **HKEY****_****CURRENT****_****USER** is set as follows.

<table>
<tr>
<td>
**Name**<br/><br/></td><td>
**Type**<br/><br/></td><td>
**Data**<br/><br/></td></tr>
<tr>
<td>
*<br/><br/></td><td>
REG_DWORD<br/><br/></td><td>
0x00000001<br/><br/></td></tr>
</table>
**Conversion** **using** **WebKit** **Rendering**

Syncfusion Essential PDF now supports HTML to PDF conversion by using the WebKit rendering engine in addition to the existing Internet Explorer.

**Prerequisites** **and** **setting** **up** **the** **WebKit** **engine** **for** **conversion**

As the QT WebKit Converter requires msvcp100.dll, msvcr100.dll, libeay32.dll, libssl32.dll, ssleay32.dll for converting Webpages to PDF, these assemblies should be available in the machine. For 64 bit machines, it should be placed in C:\Windows\SysWOW64 and for 32 bit machines, it should be placed in C:\Windows\System32 locations.

**Converting** **the** **URL** **to** **a** **PDF** **document**

You can convert HTML page to PDF by using WebKitHtmlConverter. Refer to the following code example.

<<Code example>>

**Converting** **the** **HTML** **string** **to** **PDF** **document**

You can convert HTML string to pdf by using the following code example.

<<Code example>>

**Converting** **an** **SVG** **to** **PDF**

You can convert SVG files to PDF by using the following code example.

<<Code example>>

**Troubleshooting**

WebKit Converter may create blank page PDF under the following cases.

* When the **webpaghttps****://****code****.****google****.****com****/****p****/****tesseract****-****ocr****/****wiki****/****ImproveQualitye** (html) is not available/accessible.
* When msvcp.dll, msvcr.dll, libeay32.dll, libssl32.dll, ssleay32.dll are not present in SysWOW64 location.
* When any QT Binary is not present in the mentioned location.
* When the size of the webpage is high, to overcome this Additional Delay should be increased.

**Working** **with** **Word** **to** **PDF**

Essential DocIO enables to export the Word document into a PDF document by using the ConvertToPDF method of the DocToPDFConverter class

**Assembly** **Dependency** **for** **this** **Conversion**

  * Syncfusion.DocToPDFConverter.Base.dll
  * Syncfusion.DocIO.Base.dll
  * Syncfusion.Pdf.Base.dll
  * Syncfusion.Compression.Base.dll

Refer to the following code example for conversion of Word document to PDF

<<Code example>>

**Working** **with** **Tiff** **to** **PDF**

TIFF image can be converted into PDF document. This can be done by accessing each frame of the multiframe TIFF image and rendering it in each page of the PDF document.

The following code example illustrates the same.

<<Code example>>

**Working** **with** **RTF** **to** **PDF**

Essential PDF supports adding RTF contents in PDF. Essential PDF makes use of DocIO’s RTF engine to convert RTF to word and then it can be converted to PDF. 

The code example illustrates the conversion of RTF to PDF is as follows.

<<Code example>>

**Working** **with** **XPS** **to** **PDF**

XPS documents can be converted to PDF by using the Convert method of the XPSToPdfConverter class.

__**Note**____**:**__ __**You**__ __**need**__ __**to**__ __**add**__ __**the**__ __**Syncfusion**____**.**____**XPS**__ __**namespace**__ __**to**__ __**work**__ __**with**__ __**the**__ __**XPSToPdfConverter**__ __**class**____**.**__

An XPS document can be converted to PDF by using the following code example:

<<Code example>>

**Working** **with** **HTML** **to** **Image**

You can convert HTML page to Images by using HtmlConverter class. Refer to the following code example.

<<Code example>>

**Working** **with** **PDF** **to** **Image**

You can convert all Pages to Images of Pdf document by using Essential PDF. Refer to the following code example.

Essential PDF Viewer assemblies are required for this conversion.

<< Code example>>

**Working** **with** **Tagged** **PDF**

HTML documents can be converted to tagged PDFs by using the **ConvertToTaggedPDF** method. It returns **PdfLayoutResult** that provides the end rectangle bounds and PDF page after the conversion.

A tagged PDF can be converted from a Web page or HTML string by using the following code example:

<<Code example>>

**Working** **with** **Optical** **Character** **Recognition** **(****OCR****)**

Essential PDF provided support for **Optical** **Character** **Recognition** with the help of Google’s Tesseract optical character recognition engine.

**Prerequisites** **and** **setting** **up** **the** **Tesseract** **Engine**

To use a component in your application, you need to add a reference to it

1.   Add the following assemblies as references in the application.

* Syncfusion.Compression.Base.dll
* Syncfusion.Pdf.Base.dll
* Syncfusion.OCRProcessor.Base.dll

2. Place the **SyncfusionTesseract****.****dll** and **liblept168****.****dll** Tesseract assemblies in the local system and provide an assembly path to the OCR processor.

3. Place the Tesseract language data **{****E****.****g** **eng****.****traineddata****}** in the local system and provide a path to the OCR processor

**Performing** **OCR** **for** **an** **entire** **document**

You can perform OCR on PDF document with the help of OCRProcessor and PdfLoadedDocument Class. Refer to the following code example.

<<Code example>>

**Performing** **OCR** **for** **a** **region** **of** **the** **document**

You can perform OCR on particular region of a PDF document with the help of PageRegion class. Refer to the following code example.

<<Code example>>

**Best** **Practices**

You can improve the accuracy of the OCR process by choosing the correct compression method when converting the scanned paper to a TIFF image and then to a PDF document.

1. Tesseract works best with text when at least 300 dots per inch (DPI) are used, so it is beneficial to resize images.

2. Compression:

* Use (zip) lossless compression for color or gray-scale images.
* Use CCITT Group 4 or JBIG2 (lossless) compression for monochrome images. This ensures that optical character recognition works on the highest-quality image, thereby improving the OCR accuracy. This is especially useful in low-resolution scans.

3. In addition, rotated images and skewed images can also affect the accuracy and readability of the OCR process.

For more details regarding quality improvement, refer to the following link:

[https://code.google.com/p/tesseract-ocr/wiki/ImproveQuality](https://code.google.com/p/tesseract-ocr/wiki/ImproveQuality# "")

Troubleshooting

1. You can get the exception “Tesseract has not been initialized”, make sure the path of the Tesseract binaries and Tesseract data.

**Working** **with** **Hyperlinks**

Essential PDF allows you to create a hyperlinks in the PDF document by using DrawTextWebLink method in the PdfTextWebLink class

<<Code example>>

**Working** **with** **PDF** **Templates**

**Working** **with** **Pagination**

**Paginating** **a** **text** **element**

You can flow the text on multiple pages by using the PdfLayoutFormat class

<<Code example>>

**Paginating** **an** **embedded** **image**

You can flow the image on multiple pages by using the PdfLayoutFormat class

<<Code example>>

**Paginating** **a** **large** **table**

You can flow the table across multiple pages. The following code example illustrates how to flow the large content table on multiple pages.

<<Code example>>

**Headers** **and** **Footers** 

**Adding** **an** **automatic** **field** **in** **header** **and** **footer**

The **Header** can be placed at the top margin area of the PdfPage and **Footer** can be placed at the bottom margin area of the PdfPage.

You can draw the header and footer in PDF document by using the PdfPageTemplateElement class.

Refer to the following procedure to draw the header:

1) Create the template object for header by using the PdfPageTemplateElement class.
2) Assign the created header template into PDF document template at top.

The same procedure can be followed to draw the footer. The page numbers can be drawn in footer by using automatic fields.

Refer to the following code example to draw the page numbers in footer by using automatic fields:

<<code example>>

**Shapes** 

Shape is the form of an object or its external boundary, outline, or external surface. It has the following varieties 

* Rectangle 
* Line
* Curve 
* Circle
* Arc
* Text and so on.

Shapes are filled by using different types of brushes like gradient brush, Tiling brush, and so on. **Essential** **PDF** supports drawing shapes with different color spaces and also allows to set the Transparency for shapes. 

<<code example>>

  * Working with Forms
    * Creating a new PDF form
    * Modifying the location and properties of an existing form field
    * Filling form fields of an existing PDF 
    * Flattening Form Fields of a PDF document

**Working** **with** **Bookmarks**

To ease navigation in large documents, **PDF** files can display a document outline in the viewer, allowing you to navigate from one page to another.

The document outline consists of a tree like hierarchy of bookmark items. This tree serves as a visual table of content displaying the structure of the document.

**Adding** **Bookmarks** **in** **a** **PDF**

**Essential** **PDF** allows you to add bookmarks to the newly created **PDF** document and also to the existing **PDF** documents.

The Add () method of PdfBookmarkBase collection class adds the bookmark to the document.

<<Code example>>

**Inserting** **Bookmarks** **in** **an** **existing** **PDF**

When loading an existing document, the **Essential** **PDF** loads all bookmarks of the document. Each loaded bookmark is represented by the **PdfLoadedBookmark** class, inherited from the **PdfBookmark** class.

The following code example illustrates how to insert new bookmarks in the existing **PDF** document,

<<Code example>>

**Removing** **Bookmarks** **from** **an** **existing** **PDF** 

You can also remove bookmarks from the existing PDF document by using the following methods of the **PdfBookmarkBase** class.

**Remove** - This method allows you to remove the specified bookmark.

**RemoveAt** - This method allows you to remove the bookmark at a specified index.

<<Code example>>

**Working** **with** **Annotations**

An annotation associates an object such as a note, sound, or a movie with location on the page of a **PDF** document, or provides a way to interact with you by means of mouse and keyboard.

**Adding** **annotations** **to** **a** **PDF** **document**

<table>
<tr>
<td>
In order to add an annotation in a particular page, you need to add it to the PdfAnnotationCollection of that page by using Add method. <br/><br/></td></tr>
</table>
* Create a particular annotation that you want to add to the PDF.
* Add the annotation to the PdfPage's PdfAnnotationCollection.

<<Code example>>

**Supported** **annotation** **types**

**3D** **Annotation**

3D Annotations are by means where the 3D artwork is represented in a PDF document. Essential PDF can embed 3D files (u3d) in PDF files. 

3D annotation is handled by the **Pdf3DAnnotation** class. The following example illustrates how to embed a 3D file.

<<Code example>>

**File** **Link** **Annotation** 

External files can be hyperlinked in a pdf document by using the file link annotation.

An annotation can associate objects such as note, sound or a movie by specifying the corresponding object location in the document.

**PdfFileLinkAnnotation** class of the Essential PDF can be used to associate an external file to the document as follows

<<Code example>>

**Free** **Text** **Annotation**

Free text annotation enables you to display text directly on the page.

Free Text Annotations can be included anywhere in the PDF Document by specifying the location and CallOutLine points.

**PdfFreeTextAnnotation** calss is used to create the free text annotation.

<<Code example>>

**Line** **Annotation** 

Line annotation displays a single straight line on the page. When you open it, it displays a pop-up window containing text of the associated note.

PdfLineAnnotation is used to create and set the properties to the Line annotation.

**Working** **with** **Attachments**

**Adding** **attachment** **in** **a** **PDF**

Essential PDF allows you to add attachments in the PDF document by using the PdfAttachment class.

<<Code example>>

**Removing** **attachment** **from** **an** **existing** **PDF** 

You can remove an attachment from an existing PDF document by using remove method of the PdfAttachmentCollection class.

**Extracting** **and** **saving** **an** **attachment** **to** **the** **disk****.**

Essential PDF allows you to extract the attachment from the existing PDF document. 

<<Code example>>

**Security**

PDF Security is used to protect PDF documents from unauthorized use and misuse.

**Working** **with** **RC4** **Encryption** 

**Essential** **PDF** allows you to encrypt your document in RC4 encryption.

<<Code example>>

**Working** **with** **AES** **Encryption** 

**Essential** **PDF** allows you to create an AES encrypted PDF document.

<<Code example>>

**Working** **with** **Digitally** **Signature**

**Essential** **PDF** allows you to put signature in an existing **PDF** document as in a newly created **PDF**.

<<Code example>>

**Adding** **a** **timestamp** **in** **digital** **signature**

**Essential** **PDF** supports addition of timestamp in digital signatures. The date and time where the document is signed can be added as part of the signature.

To apply timestamp using **Essential** **PDF**, the TimeStampServer property of the PdfSignature class has to be used. The parameters for the TimeStampMethod are the URI of digital server, username, and password.

<<Code example>>

**Barcode** 

**Adding** **a** **barcode** **to** **the** **PDF** **document**

Refer to JS

**Supported** **barcode** **types** – refer JS

**Working** **with** **Actions**

**Essential** **PDF** supports different actions triggered by different events and user interactions

**Adding** **an** **action** **to** **the** **PDF**

You can add the action to the PDF document. Refer to the following code example.

<<Code example>>

**Supported** **action** **types**

Essential PDF supports the following types of actions.

* **PdfSoundAction** that plays the specified music file.
* **PdfJavaScriptAction** that executes specified PDF JavaScript code.
* **PdfUriAction** that launches the specified URI.
* **PdfGoToAction** that goes to the specified page of the document.
* **PdfLaunchAction** that launches the application or opens the document.
* **PdfNamedAction** that goes to the named destination: next, previous, first or last page.
* **PdfSubmitAction** that submits the data entered into the PDF form.
* **PdfResetAction** that resets the fields of the PDF form.
1. Following are the events of a Document object where an action can be added:
* **AfterOpen** action to be performed after the document is opened.
* **AfterPrint** action to be performed after the document is printed.
* **AfterSave** action to be performed after the document is saved.
* **BeforeClose** action to be performed before the document is closed.
* **BeforePrint** action to be performed before the document is printed.
* **BeforeSave** action to be performed before the document is saved.
2. Following are the events of an annotation where an action can be added:
* **GotFocus** action to be performed when the annotation gets focus.
* **LostFocus** action to be performed when the annotation loses focus.
* **MouseEnter** action to be performed when the cursor enters the active area of the annotation.
* **MouseLeave** action to be performed when the cursor leaves the active area of the annotation.
* **MouseDown** action to be performed when the mouse button is pressed inside the active area of the annotation.
* **MouseUp** action to be performed when the mouse button is released inside the active area of the annotation.
3. Following are the events of a form field where an action can be added 
  * **Calculate** JavaScript action to be performed to recalculate the value of the field.
  * **Format** JavaScript action to be performed before the field is formatted to display the value.
  * **Validate** JavaScript action to be performed when the value of the field is changed.
  * **KeyPressed** JavaScript action to be performed when you type, key-stroke into a text field or combo box, or modifies the selection in a scrollable list box.

**Sound** **Action**

Sound action plays a specified music file in the **PDF** document. Volume and repeat can be specified for the sound action.

<<Code example>>

**Javascript** **Action**

A JavaScript action allows execution of **JavaScript** code embedded in the **PDF** document

<<Code example>>

**URI** **Action**

URI action allows you displaying a hypertext link in a web browser.

**<<****Code** **example****>>**

**GoTo** **Action**

GoTo action displays the specified page in the current document. The location can be specified for the destination page.

<<Code example>>

**Launch** **Action**

Launch action allows execution of an external application or file.

<<Code example>>

**Named** **Action**

Named action allows execution of predefined **PDF** actions. 

The following predefined **PDF** actions are available: go to next page, go to prev page, go to first page, and go to last page

<<Code example>>

**Submit** **Action**

Submit action allows submission of data that is entered into the PDF form.

<<Code example>>

**Reset** **Action**

Reset action allows resetting of all form fields in the PDF document

<<Code example>>

**Adding** **an** **action** **to** **the** **form** **field**

Essential PDF provides you support to add the various actions to form fields.

The following code example illustrates this. 

<<Code example>>

**Adding** **an** **action** **to** **the** **bookmarks**

Essential PDF allows you to add action to the specific bookmarks. You can perform action by clicking the bookmarks at the run time.

<<Code example>>

**Working** **with** **Stamps****,** **Watermarks** **and** **Overlay**

Essential PDF supports stamps, watermarks and overlay the pdf documents.

**Stamp** **Documents**

Essential PDF provides you support to stamp over newly created document as well as an existing PDF document.

* Adding Text Stamp into the PDF document
* Adding Image Stamp into the PDF document

**Adding** **Text** **Stamp** **into** **the** **PDF** **document**

You can add text stamp in to the PDF document. Refer to the following code example.

<<Code example>>

**Adding** **Image** **Stamp** **into** **the** **PDF** **document**

You can add image as stamp into the PDF document. Refer to the following code example.

<<Code example>>

**Watermarks**

You can add watermarks into the PDF document. Refer to the following code example.

<<Code example>>

**Overlay** **Documents**

PDF pages can be overlayed one above the other by importing pages from existing document and converting them to templates.

Refer to the following code example to overlay the documents.

<<Code example>>

**Working** **with** **Layers**

Layers are collection of graphics and when the viewer application is used, you can make the layers visible or invisible dynamically. The graphics belonging to such a group can reside anywhere in the document.

**Adding** **multiple** **layers** **in** **PDF** **page**

**PdfPageLayer** used to create the layers in the **PdfDocument** that allows creating unlimited levels of layers and sub-layers in a parent-child relationship. Refer to the following code example for adding multiple layers.

<<Code example>>

**Toggling** **the** **visibility** **of** **layers**

You can toggle the visibility of the **PdfLayer** when printing the PDF document by using the **PdfPrintState** class and it has the following three options.

* Print when visible – Prints the layer when it is visible on the page.
* Never print – This option never prints Layer on the page.
* Always print – This option always prints the Layer on the page.

<<Code example>>

**Merging** **multiple** **layers** **in** **an** **existing** **PDF** **document****.**

You can merge the multiple layers from an existing PDF document. Refer to the following code example.

<<Code example>>

**Working** **with** **Tagged** **PDF**

HTML documents can be converted to tagged PDFs by using the **ConvertToTaggedPDF** method. It returns **PdfLayoutResult** that provides the end rectangle bounds and PDF page after the conversion.

A tagged PDF can be converted from a Web page or HTML string by using the following code example:

<<Code example>>

**Working** **with** **Compression**

**Working** **with** **content** **compression**

Essential PDF allows you to compress the content of the PDF document to reduce the file size.

<<Code example>>

**Working** **with** **image** **compression**

Essential PDF allows you to compress the image in the PDF document to reduce the file size by changing the image quality in the PdfBitmap class

<<Code example>>

**PDF** **Conformance**

PDF elements are standardized under ISO for several constituencies. This section deals with the following standards that are supported by Essential PDF.

* PDF/A-This topic demonstrates PDF/A-1b standard that is used for archiving in environments like corporate, government, and library.
* PDF/X-This topic discusses the PDF/X-1a standard that is mainly available for standardizing printing and graphics.

**Adding** **support** **for** **PDF****/****A****-****1b** **conformance****.**

The PDF/A formats specified in the ISO 19005 standards strive to provide a mechanism for representing electronic documents.

These documents are represented in a manner that preserves their visual appearance over time, independent of the tools and systems used for creating, storing, or rendering the files. 

A key element to this reproducibility is the requirement for PDF/A documents to be 100 percent self-contained.

PDF/A standard imposes some restrictions regarding the usage of color, fonts, annotations, and other elements. These restrictions are:

* The use of JavaScript is forbidden.
* Attaching any file to a PDF document is forbidden.
* Hyperlinking to a non-PDF file is forbidden.
* Security features are forbidden.
* Use of Form Fields is forbidden.
* Text containing HTML tags is forbidden.
* Supports the use of TrueType fonts only, does not support Type1 font.
* Supports the use of RGB color, does not support CMYK color.

**Validating** **PDF****/****A1****-****b**

Adobe Acrobat Preflight tool is used to verify the compliance of a PDF document with the PDF/A standard.

You can verify the compliance of a PDF file by using the Preflight tool. By using the menu options select Advanced > Preflight > PDF/A compliance > Verify compliance with PDF/A-1b.

The following code example illustrates how to create PDF/A-1b compliant output:

<<Code example>>

**Adding** **support** **for** **PDF****/****X****-****1a** **conformance****.**

PDF/X-1a restricts the content in the PDF document that does not directly serve the purpose of high-quality print production output, such as annotations, Java Actions, and embedded multimedia.

PDF/X-1a also eliminates the most common errors in file preparation. Sending the document as a PDF/X-1a file guarantees that font errors do not occur. This is because a file declared as complying with the PDF/X-1a standard meets the following requirements:

•      All fonts and images must be embedded.

•      All elements must be encoded as CMYK.

The following code example illustrates how to create PDF/A-1b compliant output:

<<Code example>>

**Metadata** **(****XMP****)**

**Metadata** is a data that describes the characteristics or properties of a document

Metadata includes document information properties such as author, modification date, and copyright status.

**Working** **with** **the** **XMP** **metadata**

In order to work multiple applications effectively with metadata, there must be a common standard that they understand. XMP-the Extensible Metadata Platform is designed to provide such a standard.

XMP standardizes the definition, creation, and processing of metadata

**Supported** **Schema** **types**

XMP is provided with the following schemas:

* Basic Schema 
* Dublin Core Schema 
* Rights Management Schema 
* Basic Job Ticket Schema 
* Paged-Text Schema 
* PDF Schema 

**Basic** **Schema**

Basic Schema contains properties that provide basic descriptive information such as, 

* Base URL
* Creation date
* Creator tool
* Label
* Modified date.
* Meta data date
* Nickname
* Rating

BasicSchema class is used to create the basic schema properties.

Refer to the following code example to create XMP basic schema

<<Code example>>

**Dublin** **Core** **Schema**

The Dublin Core schema provides a set of commonly used properties such as,

* Contributor
* Coverage
* Creator
* Date
* Description
* Format
* Language
* Publisher
* Title

DublinCoreSchema class is used to create the Dublincore schema properties

<<Code example>>

**Rights** **Management** **Schema**

This schema includes properties related to rights management. These properties provide information regarding the legal restrictions associated with a resource.

* Certificate
* Marked
* Owner
* UsageTerm
* WebStatement

<<Code example>>

**Basic** **Job** **Ticket** **Schema**

This schema describes very simple workflow or job information.

* JobRef

<<Code example>>

**Paged****-****Text** **Schema**

The Paged-Text schema is used for text appearence on page in a document.

* MaxPageSize
* NPages
* Colorants
* PlateNames

<<Code example>>

**PDF** **Schema**

This schema specifies properties used with Adobe PDF documents.

PDFSchema class is used to create the PDF Schema. It has the following set of properties.

<<Code example>

**Custom** **Schema**

A custom schema defines the structure of the customized information records. You can use the CustomSchema class to: 

* Define custom metadata files and, 
* Add them to the PDF document 

Add the following code to define a custom schema. 

<<Code example>>

**Adding** **Custom** **Metadata** **to** **the** **PDF** **document**

**Essential** **PDF** allows you to add required metadata (custom metadata) to a PDF document

**How** **to** **add** **a** **custom** **Metadata** **Field**

To add a custom metadata field, 

* Create an XML document container 
* Create a custom schema 

**Create** **an** **XML** **Document** **container**

The custom metadata to be created has to be stored and linked to the PDF document in use. Here, XML document is used as a container to save the custom metadata fields for the PDF document. 

You can add the following code to create an XML document to store custom metadata fields.

<<Code example>>

**Create** **custom** **schema**

Custom schema defines the structure of the customized information records. 

You can use the CustomSchema class to: 

* Define custom metadata files
* Add them to the PDF document 

<<Code example>>

**Full** **Code**

Full code is used to create a custom meatadata field as illustrated in the following code

<<Code example>>

**Working** **with** **Color** **Space**

Essential PDF allows you to add color space into the PDF document.

**Supported** **color** **spaces**

* Device ColorSpace
* CIE-based Color Spaces
* ICC-based Color Spaces
* Graphics Level
