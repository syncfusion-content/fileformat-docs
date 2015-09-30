---
layout: Post
title: Fields
description: This section illustrates to add and update the fields in the Word document
platform: FileFormat
control: DocIO
documentation: UG
---
# Fields

Fields in Word document are placeholders for data that might change on field update. Fields are represented by **WField****,** **WFieldMark** instance in DocIO. A field in Word document contains field codes, field separator, field result, and field end.

To know various types of Microsoft Word supported fields and its syntax refer the below MSDN article:

[https://support.office.com/en-US/article/Field-codes-in-Word-1ad6d91a-55a7-4a8d-b535-cf7888659a51](https://support.office.com/en-US/article/Field-codes-in-Word-1ad6d91a-55a7-4a8d-b535-cf7888659a51# "")

## Adding fields

You can add a field in a Word document using **AppendField** method of **WParagraph** class.

The following code snippet illustrate how to add a field in Word document.

{% highlight c# %}
C#

//Create an instance of WordDocument class (Empty Word Document)

WordDocument document = new WordDocument();

//Add a new section into the Word Document

IWSection section = document.AddSection();

//Add a new paragraph into Word document and append text into paragraph

IWParagraph paragraph = section.AddParagraph();

paragraph.AppendText("Today's Date: ");

//Add the new Date field in Word document with field name and its type.

WField field = paragraph.AppendField("Date", FieldType.FieldDate) as WField;

//Field code used to describe how to display the date

field.FieldCode = @"DATE  \@" + "\"MMMM d, yyyy\""; 

//Save the document in the given name and format

document.Save("Sample.docx", FormatType.Docx);

//Release the resources occupied by WordDocument instance

document.Close();



{% endhighlight %}

{% highlight vbnet %}
VB

'Create an instance of WordDocument class (Empty Word Document)

Dim document As New WordDocument()

'Add a new section into the Word Document

Dim section As IWSection = document.AddSection()

'Add a new paragraph into Word document and append text into paragraph

Dim paragraph As IWParagraph = section.AddParagraph()

paragraph.AppendText("Today's Date: ")

'Add the new Date field in Word document with field name and its type.

Dim field As WField = TryCast(paragraph.AppendField("Date", FieldType.FieldDate), WField)

'Field code used to describe how to display the date

field.FieldCode = "DATE  \@" + """MMMM d, yyyy"""

'Save the document in the given name and format

document.Save("Sample.docx", FormatType.Docx)

'Release the resources occupied by WordDocument instance

document.Close()



{% endhighlight %}

## Updating fields

Field updating engine calculates the resultant value based on the field code information and updates the field result with the new value. You can update the following fields using DocIO:

* = (formula field)
* DATE
* TIME
* DOCVARIABLE 
* DOCPROPERTY
* COMPARE
* IF
* NEXTIF
* MERGEREC
* MERGESEQ
* SECTION
* NUMPAGES
* TITLE
* Cross-Reference

The following are the known limitations:

* Updating of NUMPAGES field and Cross Reference field with Page number and Paragraph number options are not supported in Silverlight, WinRT, Universal, Windows Phone and Xamarin applications.
* Currently group shapes, drawing canvas, and table auto resizing are not supported in Word to PDF lay outing, and this may lead to update incorrect page number and total number of pages.

The following code snippet illustrate how to update the fields present in Word document.

{% highlight c# %}
C#

//Load an existing Word document into DocIO instance 

WordDocument document = new WordDocument("Input.docx", FormatType.Docx);

//Updates the fields present in a document.

document.UpdateDocumentFields();

document.Save("Result.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
VB

'Load an existing Word document into DocIO instance 

Dim document As New WordDocument("Input.docx", FormatType.Docx)

'Updates the fields present in a document.

document.UpdateDocumentFields()

document.Save("Result.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

## IF Field

If field compares two values and updates the field result with true text, if comparison succeeds otherwise false text.

To know more about If field and its syntax in Microsoft Word refer the below MSDN article:

[https://support.office.com/en-au/article/Field-codes-IF-field-9f79e82f-e53b-4ff5-9d2c-ae3b22b7eb5e](https://support.office.com/en-au/article/Field-codes-IF-field-9f79e82f-e53b-4ff5-9d2c-ae3b22b7eb5e# "")

The following code snippet illustrate how to add an If field in Word document.

{% highlight c# %}
C#

WordDocument document = new WordDocument();

IWSection section = document.AddSection();

IWParagraph paragraph = section.AddParagraph();

paragraph.AppendText("If field which uses string of characters in expression");

paragraph = section.AddParagraph();

//Create the new instance of IF field

WIfField field = paragraph.AppendField("If", FieldType.FieldIf) as WIfField;

//Specify the expression, true and false statement in field code

field.FieldCode = "IF \"True\" = \"True\" \"The given statement is Correct\" \"The given statement is Wrong\"";

paragraph = section.AddParagraph();

paragraph.AppendText("If field which uses numbers in expression");

paragraph = section.AddParagraph();

//Create the new instance of IF field

field = paragraph.AppendField("If", FieldType.FieldIf) as WIfField;

//Specify the expession, true and false statement in field code

field.FieldCode = "IF 100 >= 1000 \"The given statement is Correct\" \"The given statement is Wrong\"";

//Update the document fields

document.UpdateDocumentFields();

document.Save("Sample.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
VB

Dim document As New WordDocument()

Dim section As IWSection = document.AddSection()

Dim paragraph As IWParagraph = section.AddParagraph()

paragraph.AppendText("If field which uses string of characters in expression")

paragraph = section.AddParagraph()

'Create the new instance of IF field

Dim field As WIfField = TryCast(paragraph.AppendField("If", FieldType.FieldIf), WIfField)

'Specify the expression, true and false statement in field code

field.FieldCode = "IF ""True"" = ""True"" ""The given statement is Correct"" ""The given statement is Wrong"""

paragraph = section.AddParagraph()

paragraph.AppendText("If field which uses numbers in expression")

paragraph = section.AddParagraph()

'Create the new instance of IF field

field = TryCast(paragraph.AppendField("If", FieldType.FieldIf), WIfField)

'Specify the expession, true and false statement in field code

field.FieldCode = "IF 100 >= 1000 ""The given statement is Correct"" ""The given statement is Wrong"""

'Update the document fields

document.UpdateDocumentFields()

document.Save("Sample.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

## Document Variables

The DocVariable field displays the value of a specified document variable in the Word document. The document variables can be added or modified using **Variables** property of **WordDocument** class.

The following code snippet illustrate how to add a DocVariable field in Word document.

{% highlight c# %}
C#

WordDocument document = new WordDocument();

IWSection section = document.AddSection();

IWParagraph paragraph = section.AddParagraph();

paragraph.AppendText("First Name of the customer: ");

//Add the DocVariable field with Variable name and its type

paragraph.AppendField("FirstName", FieldType.FieldDocVariable);

paragraph = section.AddParagraph();

paragraph.AppendText("Last Name of the customer: ");

//Add the DocVariable field with Variable name and its type

paragraph.AppendField("LastName", FieldType.FieldDocVariable);

//Add the value for variable in WordDocument.Variable collection

document.Variables.Add("FirstName", "Jeff");

document.Variables.Add("LastName", "Smith");

//Update the document fields

document.UpdateDocumentFields();

document.Save("Sample.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
VB

Dim document As New WordDocument()

Dim section As IWSection = document.AddSection()

Dim paragraph As IWParagraph = section.AddParagraph()

paragraph.AppendText("First Name of the customer: ")

'Add the DocVariable field with Variable name and its type

paragraph.AppendField("FirstName", FieldType.FieldDocVariable)

paragraph = section.AddParagraph()

paragraph.AppendText("Last Name of the customer: ")

'Add the DocVariable field with Variable name and its type

paragraph.AppendField("LastName", FieldType.FieldDocVariable)

'Add the value for variable in WordDocument.Variable collection

document.Variables.Add("FirstName", "Jeff")

document.Variables.Add("LastName", "Smith")

'Update the document fields

document.UpdateDocumentFields()

document.Save("Sample.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

## Cross Reference

A cross-reference refers to an item that appears in another location in a document. You can create cross-reference to bookmarks in a document using **AppendCrossReference** method of **WParagraph** class.

I> Note: Essential DocIO supports to create and update cross-reference fields only for bookmarks in a document

The following code snippet illustrate how to how to append cross reference for bookmark in Word document.

{% highlight c# %}
C#

WordDocument document = new WordDocument();

IWSection section = document.AddSection();

IWParagraph paragraph = section.AddParagraph();

//Add text, bookmark start and end in the paragraph

paragraph.AppendBookmarkStart("Title");

paragraph.AppendText("Northwind Database");

paragraph.AppendBookmarkEnd("Title");

paragraph = section.AddParagraph();

paragraph.AppendText("The Northwind sample database (Northwind.mdb) is included with all versions of Access. It provides data you can experiment with and database objects that demonstrate features you might want to implement in your own databases.");

section = document.AddSection();

section.AddParagraph();

paragraph = section.AddParagraph() as WParagraph;

//Get the collection of bookmark start in the word document

List<Entity> items = document.GetCrossReferenceItems(ReferenceType.Bookmark);

paragraph.AppendText("Bookmark Cross Reference starts here ");

//Append the cross reference for bookmark “Title” with ContentText as reference kind

paragraph.AppendCrossReference(ReferenceType.Bookmark, ReferenceKind.ContentText, items[0], true, false, false, string.Empty);

//Update the document Fields

document.UpdateDocumentFields();

document.Save("Sample.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
VB

Dim document As New WordDocument()

Dim section As IWSection = document.AddSection()

Dim paragraph As IWParagraph = section.AddParagraph()

'Add text, bookmark start and end in the paragraph

paragraph.AppendBookmarkStart("Title")

paragraph.AppendText("Northwind Database")

paragraph.AppendBookmarkEnd("Title")

paragraph = section.AddParagraph()

paragraph.AppendText("The Northwind sample database (Northwind.mdb) is included with all versions of Access. It provides data you can experiment with and database objects that demonstrate features you might want to implement in your own databases.")

section = document.AddSection()

section.AddParagraph()

paragraph = TryCast(section.AddParagraph(), WParagraph)

'Get the collection of bookmark start in the word document

Dim items As List(Of Entity) = document.GetCrossReferenceItems(ReferenceType.Bookmark)

paragraph.AppendText("Bookmark Cross Reference starts here ")

'Append the cross reference for bookmark “Title” with ContentText as reference kind

paragraph.AppendCrossReference(ReferenceType.Bookmark, ReferenceKind.ContentText, items(0), True, False, False, String.Empty)

'Update the document Fields

document.UpdateDocumentFields()

document.Save("Sample.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

