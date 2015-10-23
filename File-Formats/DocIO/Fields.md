---
title: Fields
description: This section illustrates how to add and update the fields in the Word document
platform: file-formats
control: DocIO
documentation: UG
---
# Fields

Fields in Word document are placeholders for data that might change on field update. Fields are represented by WField,WFieldMarkinstance in DocIO. A field in Word document contains field codes, field separator, field result, and field end.

To know various types of Microsoft Word supported fields and its syntax refer to the following MSDN article:

[https://support.office.com/en-US/article/Field-codes-in-Word-1ad6d91a-55a7-4a8d-b535-cf7888659a51](https://support.office.com/en-US/article/Field-codes-in-Word-1ad6d91a-55a7-4a8d-b535-cf7888659a51#)

## Adding fields

You can add a field in a Word document by using AppendFieldmethod of WParagraphclass.

The following code example illustrates how to add a field in Word document.

{% tabs %} 

{% highlight c# %}


//Creates an instance of WordDocument class (Empty Word Document)

WordDocument document = new WordDocument();

//Adds a new section into the Word Document

IWSection section = document.AddSection();

//Adds a new paragraph into Word document and appends text into paragraph

IWParagraph paragraph = section.AddParagraph();

paragraph.AppendText("Today's Date: ");

//Adds the new Date field in Word document with field name and its type.

WField field = paragraph.AppendField("Date", FieldType.FieldDate) as WField;

//Field code used to describe how to display the date

field.FieldCode = @"DATE  \@" + "\"MMMM d, yyyy\""; 

//Saves the document in the given name and format

document.Save("Sample.docx", FormatType.Docx);

//Releases the resources occupied by WordDocument instance

document.Close();



{% endhighlight %}

{% highlight vbnet %}


'Creates an instance of WordDocument class (Empty Word Document)

Dim document As New WordDocument()

'Adds a new section into the Word Document

Dim section As IWSection = document.AddSection()

'Adds a new paragraph into Word document and appends text into paragraph

Dim paragraph As IWParagraph = section.AddParagraph()

paragraph.AppendText("Today's Date: ")

'Adds the new Date field in Word document with field name and its type.

Dim field As WField = TryCast(paragraph.AppendField("Date", FieldType.FieldDate), WField)

'Field code used to describe how to display the date

field.FieldCode = "DATE  \@" + """MMMM d, yyyy"""

'Saves the document in the given name and format

document.Save("Sample.docx", FormatType.Docx)

'Releases the resources occupied by WordDocument instance

document.Close()

{% endhighlight %}

   {% endtabs %}  

   
   
## Updating fields

Field updating engine calculates the resultant value based on the field code information and updates the field result with the new value. You can update the following fields by using DocIO:

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

The following code example illustrate how to update the fields present in Word document.

{% tabs %} 

{% highlight c# %}


//Loads an existing Word document into DocIO instance 

WordDocument document = new WordDocument("Input.docx", FormatType.Docx);

//Updates the fields present in a document.

document.UpdateDocumentFields();

document.Save("Result.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}

'Loads an existing Word document into DocIO instance 

Dim document As New WordDocument("Input.docx", FormatType.Docx)

'Updates the fields present in a document.

document.UpdateDocumentFields()

document.Save("Result.docx", FormatType.Docx)

document.Close()

{% endhighlight %}

 {% endtabs %}  

 
## IF Field

If field compares two values and updates the field result with true text, when comparison succeeds otherwise false text.

To know more about If field and its syntax in Microsoft Word, refer to the following MSDN article:

[https://support.office.com/en-au/article/Field-codes-IF-field-9f79e82f-e53b-4ff5-9d2c-ae3b22b7eb5e](https://support.office.com/en-au/article/Field-codes-IF-field-9f79e82f-e53b-4ff5-9d2c-ae3b22b7eb5e#)

The following code example illustrates how to add an If field in Word document.

{% tabs %}  

{% highlight c# %}


WordDocument document = new WordDocument();

IWSection section = document.AddSection();

IWParagraph paragraph = section.AddParagraph();

paragraph.AppendText("If field which uses string of characters in expression");

paragraph = section.AddParagraph();

//Creates the new instance of IF field

WIfField field = paragraph.AppendField("If", FieldType.FieldIf) as WIfField;

//Specifies the expression, true and false statement in field code

field.FieldCode = "IF \"True\" = \"True\" \"The given statement is Correct\" \"The given statement is Wrong\"";

paragraph = section.AddParagraph();

paragraph.AppendText("If field which uses numbers in expression");

paragraph = section.AddParagraph();

//Creates the new instance of IF field

field = paragraph.AppendField("If", FieldType.FieldIf) as WIfField;

//Specifies the expression, true and false statement in field code

field.FieldCode = "IF 100 >= 1000 \"The given statement is Correct\" \"The given statement is Wrong\"";

//Updates the document fields

document.UpdateDocumentFields();

document.Save("Sample.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}

Dim document As New WordDocument()

Dim section As IWSection = document.AddSection()

Dim paragraph As IWParagraph = section.AddParagraph()

paragraph.AppendText("If field which uses string of characters in expression")

paragraph = section.AddParagraph()

'Creates the new instance of IF field

Dim field As WIfField = TryCast(paragraph.AppendField("If", FieldType.FieldIf), WIfField)

'Specifies the expression, true and false statement in field code

field.FieldCode = "IF ""True"" = ""True"" ""The given statement is Correct"" ""The given statement is Wrong"""

paragraph = section.AddParagraph()

paragraph.AppendText("If field which uses numbers in expression")

paragraph = section.AddParagraph()

'Creates the new instance of IF field

field = TryCast(paragraph.AppendField("If", FieldType.FieldIf), WIfField)

'Specify the expession, true and false statement in field code

field.FieldCode = "IF 100 >= 1000 ""The given statement is Correct"" ""The given statement is Wrong"""

'Updates the document fields

document.UpdateDocumentFields()

document.Save("Sample.docx", FormatType.Docx)

document.Close()

{% endhighlight %}

  {% endtabs %}  

  
  
## Document Variables

The DocVariable field displays the value of a specified document variable in the Word document. The document variables can be added or modified using Variablesproperty of WordDocumentclass.

The following code example illustrate how to add a DocVariable field in Word document.

{% tabs %}  

{% highlight c# %}


WordDocument document = new WordDocument();

IWSection section = document.AddSection();

IWParagraph paragraph = section.AddParagraph();

paragraph.AppendText("First Name of the customer: ");

//Adds the DocVariable field with Variable name and its type

paragraph.AppendField("FirstName", FieldType.FieldDocVariable);

paragraph = section.AddParagraph();

paragraph.AppendText("Last Name of the customer: ");

//Adds the DocVariable field with Variable name and its type

paragraph.AppendField("LastName", FieldType.FieldDocVariable);

//Adds the value for variable in WordDocument.Variable collection

document.Variables.Add("FirstName", "Jeff");

document.Variables.Add("LastName", "Smith");

//Updates the document fields

document.UpdateDocumentFields();

document.Save("Sample.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}

Dim document As New WordDocument()

Dim section As IWSection = document.AddSection()

Dim paragraph As IWParagraph = section.AddParagraph()

paragraph.AppendText("First Name of the customer: ")

'Adds the DocVariable field with Variable name and its type

paragraph.AppendField("FirstName", FieldType.FieldDocVariable)

paragraph = section.AddParagraph()

paragraph.AppendText("Last Name of the customer: ")

'Adds the DocVariable field with Variable name and its type

paragraph.AppendField("LastName", FieldType.FieldDocVariable)

'Adds the value for variable in WordDocument.Variable collection

document.Variables.Add("FirstName", "Jeff")

document.Variables.Add("LastName", "Smith")

'Updates the document fields

document.UpdateDocumentFields()

document.Save("Sample.docx", FormatType.Docx)

document.Close()

{% endhighlight %}

  {% endtabs %}  

  
  
## Cross Reference

A cross-reference refers to an item that appears in another location in a document. You can create cross-reference to bookmarks in a document by using AppendCrossReferencemethod of WParagraphclass.

N>  Essential DocIO supports to create and update cross-reference fields only for bookmarks in a document

The following code example illustrate how to append cross reference for bookmark in Word document.

{% tabs %}  

{% highlight c# %}


WordDocument document = new WordDocument();

IWSection section = document.AddSection();

IWParagraph paragraph = section.AddParagraph();

//Adds text, bookmark start and end in the paragraph

paragraph.AppendBookmarkStart("Title");

paragraph.AppendText("Northwind Database");

paragraph.AppendBookmarkEnd("Title");

paragraph = section.AddParagraph();

paragraph.AppendText("The Northwind sample database (Northwind.mdb) is included with all versions of Access. It provides data you can experiment with and database objects that demonstrate features you might want to implement in your own databases.");

section = document.AddSection();

section.AddParagraph();

paragraph = section.AddParagraph() as WParagraph;

//Gets the collection of bookmark start in the word document

List<Entity> items = document.GetCrossReferenceItems(ReferenceType.Bookmark);

paragraph.AppendText("Bookmark Cross Reference starts here ");

//Appends the cross reference for bookmark “Title” with ContentText as reference kind

paragraph.AppendCrossReference(ReferenceType.Bookmark, ReferenceKind.ContentText, items[0], true, false, false, string.Empty);

//Updates the document Fields

document.UpdateDocumentFields();

document.Save("Sample.docx", FormatType.Docx);

document.Close();



{% endhighlight %}

{% highlight vbnet %}


Dim document As New WordDocument()

Dim section As IWSection = document.AddSection()

Dim paragraph As IWParagraph = section.AddParagraph()

'Adds text, bookmark start and end in the paragraph

paragraph.AppendBookmarkStart("Title")

paragraph.AppendText("Northwind Database")

paragraph.AppendBookmarkEnd("Title")

paragraph = section.AddParagraph()

paragraph.AppendText("The Northwind sample database (Northwind.mdb) is included with all versions of Access. It provides data you can experiment with and database objects that demonstrate features you might want to implement in your own databases.")

section = document.AddSection()

section.AddParagraph()

paragraph = TryCast(section.AddParagraph(), WParagraph)

'Gets the collection of bookmark start in the word document

Dim items As List(Of Entity) = document.GetCrossReferenceItems(ReferenceType.Bookmark)

paragraph.AppendText("Bookmark Cross Reference starts here ")

'Appends the cross reference for bookmark “Title” with ContentText as reference kind

paragraph.AppendCrossReference(ReferenceType.Bookmark, ReferenceKind.ContentText, items(0), True, False, False, String.Empty)

'Updates the document Fields

document.UpdateDocumentFields()

document.Save("Sample.docx", FormatType.Docx)

document.Close()



{% endhighlight %}

{% endtabs %}  