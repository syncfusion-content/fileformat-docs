---
title: Conversion
description: This section illustrates how to convert a Word document into other supported file formats
platform: file-formats
control: DocIO
documentation: UG
---

# Conversion

## Working with Document Conversions

The Essential DocIO converts documents from one format to another format. Each file format document can be categorized as flow layout document or fixed layout document.

**Flow layout document**

* A flow document is designed to "reflow content" depending on the application.
* Does not contain any information about the position of its content.
* Dynamically renders the content by application at run time.
* Example: DOC, DOCX, HTML, EPUB, RTF, and TEXT file formats.

**Fixed layout document**

* This format of fixed document is like "what you see is what you get".
* Maintains the fixed position for each content.
* Statically preserves the content in specified position.
* Example: Image and PDF.


Essential DocIO can convert various flow document as fixed document by using our layout engine. Following conversions are supported by Essential DocIO.

* Microsoft Word file format Conversions
* Word document to PDF
* Word document to Image
* RTF Conversions
* Text Conversions
* HTML Conversions
* Word document to ODT
* Word document to EPUB

## Converting Word document to PDF

Essential DocIO allows you to convert a Word document into PDF with a few lines of code. For further information kindly refer [here](https://help.syncfusion.com/file-formats/docio/word-to-pdf#).


### Customizing the Word document to PDF conversion

Essential DocIO allows you to customize the Word to PDF conversion with the following options:

* Allows to embed the TrueType fonts used in the converted PDF
* Allows to determine the quality of the charts in the converted PDF 
* Allows to determine the quality of the JPEG images in the converted PDF
* Allows to reduce the Main Memory usage in Word to PDF conversion by reusing the identical images.

For further information kindly refer [here](https://help.syncfusion.com/file-formats/docio/word-to-pdf#customization-settings#).
 
 
### Unsupported elements in Word to PDF conversion

Kindly refer the [here](https://help.syncfusion.com/file-formats/docio/word-to-pdf#unsupported-elements-in-word-to-pdf-conversion#) for list of Unsupported elements in Word to PDF conversion


## Rendering / Converting Word document to Image

Essential DocIO supports to convert the Word document to images using `RenderAsImages` method. For further information kindly refer [here](https://help.syncfusion.com/file-formats/docio/word-to-image#).


## RTF conversion 

Essential DocIO supports to convert the RTF document into Word document and vice versa. For further information kindly refer [here](https://help.syncfusion.com/file-formats/docio/rtf#).


## HTML conversion

Essential DocIO supports converting the HTML file into Word document and vice versa. It supports only the HTML files that meet the validation either against XHTML 1.0 strict or XHTML 1.0 Transitional schema. 

For further information kindly refer [here](https://help.syncfusion.com/file-formats/docio/html#).


### Customizing the HTML to Word conversion

You can customize the HTML to Word conversion with the following options:

* Validate the HTML string against XHTML 1.0 Strict and Transitional schema
* Insert the HTML string at the specified position of the document body contents
* Append HTML string to the specified paragraph

For further information kindly refer [here](https://help.syncfusion.com/file-formats/docio/html#customization-settings#).

### Customizing the Word to HTML conversion

You can customize the Word to HTML conversion with the following options:

* Extract the images used in the HTML document at the specified file directory 
* Specify to export the header and footer of the Word document in the HTML 
* Specify to consider Text Input field as a editable fields or text 
* Specify the CSS style sheet type and its name

N> 
While exporting header and footer, DocIO exports the first section header content at the top of the HTML file and first section footer content at the end of the HTML file

For further information kindly refer [here](https://help.syncfusion.com/file-formats/docio/html#customization-settings#).

### Supported Document elements

Kindly refer the [here](https://help.syncfusion.com/file-formats/docio/html#supported-and-unsupported-items#) for the document elements and attributes are supported by DocIO in Word to HTML and HTML to Word conversions.

## Text file

Essential DocIO supports to convert the Word document into Text file and vice versa. For further information kindly refer [here](https://help.syncfusion.com/file-formats/docio/text#).

  
## Word to EPUB

Essential DocIO supports to convert the Word document into EPUB v2.0. It only supports in Windows Forms, UWP, WPF, ASP.NET Web and MVC platforms. For further information kindly refer [here](https://help.syncfusion.com/file-formats/docio/word-to-epub#).
