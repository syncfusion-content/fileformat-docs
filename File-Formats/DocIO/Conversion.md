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

### XHTML 1.0

XHTML syntax is very similar to HTML syntax and almost all the valid HTML elements are valid in XHTML as well. But when you write an XHTML document, need to pay a bit extra attention to make the HTML document compliant to XHTML.
Here are the important points to remember while writing a new XHTML document or converting existing HTML document into XHTML document:

* Write a DOCTYPE declaration at the start of the XHTML document.
* Write all XHTML tags and attributes in lower case only.
* Close all XHTML tags properly.
* Nest all the tags properly.
* Quote all the attribute values.
* Replace the name attribute with the id attribute.

In Word library (DocIO) we use XML reader for parsing the content from input HTML. So, the input HTML should meet XML standard (should have proper open and close tags), even if you specify XHTMLValidationType parameter as XHTMLValidationType.None.

#### What is meant by XHTMLValidation

Every HTML document is validated against a Document Type Declaration (DTD).

A `Document Type Declaration (DTD)` is a set of mark-up declarations that define a document type for a SGML-family mark-up language (GML, SGML, XML, HTML). A DTD defines the valid building blocks of an XML document. It defines the document structure with a list of validated elements and attributes.

#### Difference between XHTML validation types

** XHTMLValidationType.Strict: ** Checks whether the given HTML content is in accordance with rules or standards of XHTML 1.0 strict DTD that is, XHTML 1.0 strict DTD not allows the attributes inside the tag. 

** XHTMLValidationType.Transitional: ** Checks whether the given HTML content is in accordance with rules or standards of XHTML 1.0 Transitional DTD that is, XHTML 1.0 Transitional DTD allows several attributes within the tags, which are not allowed when using the strict DTD.

If you created the HTML document based on the transitional DTD, but used XHTMLValidationType.Strict, then the "DocIO support only welformatted xhtml " exception will be thrown in the DocIO. But not in vice-versa because, in transitional DTD approach, we may use attributes within the tags.

** XHTMLValidationType.None: ** Checks only the HTML content against the XHTML format and does not perform any schema validation. So, the given HTML content must compliant with the XHTML 1.0 format.

** Example 1:** 

This example uses the strict DTD, meaning that every single tag must be closed properly, all attributes assigned values, and more.

<table>
<tr>
<td>

  <?xml version="1.0" encoding="UTF-8"?>
  <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "DTD/xhtml1-strict.dtd">
  <html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en">
  <head>
    <title> Strict DTD XHTML Example </title>
  </head>
  <body>
    <p> Please Choose a Day:
    <br /><br />
     <select name="day">
       <option selected="selected">Monday</option>
       <option>Tuesday</option>
       <option>Wednesday</option>
     </select>
    </p>
  </body>
  </html>

</td>
</tr>
</table>

** Example 2: **

This example uses the transitional DTD, it uses several attributes within the <body> tag, which are not allowed when using the strict DTD.

<table>
<tr>
<td>

  <?xml version="1.0" encoding="UTF-8"?>
  <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "DTD/xhtml1-transitional.dtd">
  <html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en">
   <head>
     <title> Transitional DTD XHTML Example </title>
   </head>
   <body bgcolor="#FFFFFF" link="#000000" text="red">
     <p>This is a transitional XHTML example</p>
   </body>
  </html>

</td>
</tr>
</table>

## Text file

Essential DocIO supports to convert the Word document into Text file and vice versa. For further information kindly refer [here](https://help.syncfusion.com/file-formats/docio/text#).

  
## Word to EPUB

Essential DocIO supports to convert the Word document into EPUB v2.0. It only supports in Windows Forms, UWP, WPF, ASP.NET Web and MVC platforms. For further information kindly refer [here](https://help.syncfusion.com/file-formats/docio/word-to-epub#).
