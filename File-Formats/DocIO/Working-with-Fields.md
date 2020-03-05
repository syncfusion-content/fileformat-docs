---
title: Working with Fields | Syncfusion
description: This section illustrates how to add dynamic information like title, time, page number, etc., in the Word document that updates automatically
platform: file-formats
control: DocIO
documentation: UG
---
# Working with Fields

Fields in Word document are placeholders for data that might change on field update. Fields are represented by `WField`, `WFieldMark` instance in DocIO. A field in Word document contains field codes, field separator, field result, and field end.

To know various types of Microsoft Word supported fields and its syntax,refer [MSDN article](https://support.office.com/en-US/article/Field-codes-in-Word-1ad6d91a-55a7-4a8d-b535-cf7888659a51#)

From v16.1.0.24, the entire field code is included in Document Object Model(DOM). Hence the adding a field will automatically include below elements in DOM,

1. `WField` -- represents the starting of Field.

2. `ParagraphItem` – represents the Field code.

3. `WFieldMark` –represents the Field separator.

4. `ParagraphItem` – represents the Field result.

5. `WFieldMark` – represents the end of Field.

Find more information about migration changes from [here](https://help.syncfusion.com/file-formats/release-notes/migratingtov16.1.0.24#). 

## Adding fields

You can add a field in a Word document by using `AppendField` method of `WParagraph` class.

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
//Adds the new Date field in Word document with field name and its type
WField field = paragraph.AppendField("Date", FieldType.FieldDate) as WField;
//Field code used to describe how to display the date
field.FieldCode = @"DATE  \@" + "\"MMMM d, yyyy\""; 
//Saves the document in the given name and format
document.Save("Sample.docx", FormatType.Docx);
//Releases the resources occupied by WordDocument instance
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Creates an instance of WordDocument class (Empty Word Document)
Dim document As New WordDocument()
'Adds a new section into the Word Document
Dim section As IWSection = document.AddSection()
'Adds a new paragraph into Word document and appends text into paragraph
Dim paragraph As IWParagraph = section.AddParagraph()
paragraph.AppendText("Today's Date: ")
'Adds the new Date field in Word document with field name and its type
Dim field As WField = TryCast(paragraph.AppendField("Date", FieldType.FieldDate), WField)
'Field code used to describe how to display the date
field.FieldCode = "DATE  \@" + """MMMM d, yyyy"""
'Saves the document in the given name and format
document.Save("Sample.docx", FormatType.Docx)
'Releases the resources occupied by WordDocument instance
document.Close()
{% endhighlight %}

{% highlight UWP %}
//Creates an instance of WordDocument class (Empty Word Document)
WordDocument document = new WordDocument();
//Adds a new section into the Word Document
IWSection section = document.AddSection();
//Adds a new paragraph into Word document and appends text into paragraph
IWParagraph paragraph = section.AddParagraph();
paragraph.AppendText("Today's Date: ");
//Adds the new Date field in Word document with field name and its type
WField field = paragraph.AppendField("Date", FieldType.FieldDate) as WField;
//Field code used to describe how to display the date
field.FieldCode = @"DATE  \@" + "\"MMMM d, yyyy\""; 
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word file in local machine
Save(stream, "Sample.docx");
//Closes the document
document.Close();
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight ASP.NET Core %}
//Creates an instance of WordDocument class (Empty Word Document)
WordDocument document = new WordDocument();
//Adds a new section into the Word Document
IWSection section = document.AddSection();
//Adds a new paragraph into Word document and appends text into paragraph
IWParagraph paragraph = section.AddParagraph();
paragraph.AppendText("Today's Date: ");
//Adds the new Date field in Word document with field name and its type
WField field = paragraph.AppendField("Date", FieldType.FieldDate) as WField;
//Field code used to describe how to display the date
field.FieldCode = @"DATE  \@" + "\"MMMM d, yyyy\""; 
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Sample.docx");
{% endhighlight %}

{% highlight Xamarin %}
//Creates an instance of WordDocument class (Empty Word Document)
WordDocument document = new WordDocument();
//Adds a new section into the Word Document
IWSection section = document.AddSection();
//Adds a new paragraph into Word document and appends text into paragraph
IWParagraph paragraph = section.AddParagraph();
paragraph.AppendText("Today's Date: ");
//Adds the new Date field in Word document with field name and its type
WField field = paragraph.AppendField("Date", FieldType.FieldDate) as WField;
//Field code used to describe how to display the date
field.FieldCode = @"DATE  \@" + "\"MMMM d, yyyy\""; 
//Saves the Word document to  MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.docx", "application/msword", stream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}  

## Formatting Fields

You can format the field instances added to the Word document, by iterating items from field start to end.

The following code example illustrates how to format the field in Word document.

{% tabs %}

{% highlight c# %}
//Creates an instance of a WordDocument 
WordDocument document = new WordDocument();
//Adds one section and one paragraph to the document
document.EnsureMinimal();
//Adds the new Page field in Word document with field name and its type
IWField field = document.LastParagraph.AppendField("Page", FieldType.FieldPage);
IEntity entity = field;
//Iterates to sibling items until Field End 
while (entity.NextSibling != null)
{
	if (entity is WTextRange)
		//Sets character format for text ranges
		(entity as WTextRange).CharacterFormat.FontSize = 6;
	else if ((entity is WFieldMark) && (entity as WFieldMark).Type == FieldMarkType.FieldEnd)
		break;
	//Gets next sibling item
	entity = entity.NextSibling;
}
//Saves and closes the WordDocument instance
document.Save("Template.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight VB.NET %}
'Creates an instance of a WordDocument
Dim document As WordDocument = New WordDocument
'Adds one section and one paragraph to the document
document.EnsureMinimal()
'Adds the new Page field in Word document with field name and its type
Dim field As IWField = document.LastParagraph.AppendField("Page", FieldType.FieldPage)
Dim entity As IEntity = field
'Iterates to sibling items until Field End 
While (Not (entity.NextSibling) Is Nothing)
	'Sets character format for text ranges
	If (TypeOf entity Is WTextRange) Then
		CType(entity, WTextRange).CharacterFormat.FontSize = 6
	ElseIf ((TypeOf entity Is WFieldMark) AndAlso (CType(entity, WFieldMark).Type = FieldMarkType.FieldEnd)) Then
		Exit While
	End If
	'Gets next sibling item
	entity = entity.NextSibling
End While
'Saves and closes the WordDocument instance
document.Save("Template.docx", FormatType.Docx)
document.Close
{% endhighlight %}

{% highlight UWP %}
//Creates an instance of a WordDocument 
WordDocument document = new WordDocument();
//Adds one section and one paragraph to the document
document.EnsureMinimal();
//Adds the new Page field in Word document with field name and its type
IWField field = document.LastParagraph.AppendField("Page", FieldType.FieldPage);
IEntity entity = field;
//Iterates to sibling items until Field End 
while (entity.NextSibling != null)
{
	if (entity is WTextRange)
		//Sets character format for text ranges
		(entity as WTextRange).CharacterFormat.FontSize = 6;
	else if ((entity is WFieldMark) && (entity as WFieldMark).Type == FieldMarkType.FieldEnd)
		break;
	//Gets next sibling item.
	entity = entity.NextSibling;
}
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word file in local machine
Save(stream, "Template.docx");
//Closes the document
document.Close();
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight ASP.NET Core %}
//Creates an instance of a WordDocument 
WordDocument document = new WordDocument();
//Adds one section and one paragraph to the document
document.EnsureMinimal();
//Adds the new Page field in Word document with field name and its type
IWField field = document.LastParagraph.AppendField("Page", FieldType.FieldPage);
IEntity entity = field;
//Iterates to sibling items until Field End 
while (entity.NextSibling != null)
{
	if (entity is WTextRange)
		//Sets character format for text ranges 
		(entity as WTextRange).CharacterFormat.FontSize = 6;
	else if ((entity is WFieldMark) && (entity as WFieldMark).Type == FieldMarkType.FieldEnd)
		break;
	//Gets next sibling item.
	entity = entity.NextSibling;
}
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Template.docx");
{% endhighlight %}

{% highlight Xamarin %}
//Creates an instance of a WordDocument 
WordDocument document = new WordDocument();
//Adds one section and one paragraph to the document
document.EnsureMinimal();
//Adds the new Page field in Word document with field name and its type
IWField field = document.LastParagraph.AppendField("Page", FieldType.FieldPage);
IEntity entity = field;
//Iterates to sibling items until Field End 
while (entity.NextSibling != null)
{
	if (entity is WTextRange)
		//Sets character format for text ranges
		(entity as WTextRange).CharacterFormat.FontSize = 6;
	else if ((entity is WFieldMark) && (entity as WFieldMark).Type == FieldMarkType.FieldEnd)
		break;
	//Gets next sibling item
	entity = entity.NextSibling;
}
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Template.docx", "application/msword", stream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
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
//Updates the fields present in a document
document.UpdateDocumentFields();
document.Save("Result.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Loads an existing Word document into DocIO instance 
Dim document As New WordDocument("Input.docx", FormatType.Docx)
'Updates the fields present in a document
document.UpdateDocumentFields()
document.Save("Result.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight UWP %}
//Loads an existing Word document into DocIO instance 
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Input.docx"), FormatType.Docx);
//Updates the fields present in a document
document.UpdateDocumentFields();
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Closes the document
document.Close();
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight ASP.NET Core %}
//Loads an existing Word document into DocIO instance 
FileStream fileStreamPath = new FileStream("Input.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);
//Updates the fields present in a document
document.UpdateDocumentFields();
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %}

{% highlight Xamarin %}
//Loads an existing Word document into DocIO instance 
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("GettingStarted.Data.Input.docx"), FormatType.Docx);
//Updates the fields present in a document
document.UpdateDocumentFields();
//Saves the Word document to  MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}  

## IF Field

If field compares two values and updates the field result with true text, when comparison succeeds otherwise false text.

To know more about If field and its syntax in Microsoft Word, refer [MSDN article](https://support.office.com/en-au/article/Field-codes-IF-field-9f79e82f-e53b-4ff5-9d2c-ae3b22b7eb5e#)

The following code example illustrates how to add an If field in Word document.

{% tabs %}  

{% highlight c# %}
//Creates an instance of a WordDocument 
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

{% highlight vb.net %}
'Creates an instance of a WordDocument 
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
'Specify the expression, true and false statement in field code
field.FieldCode = "IF 100 >= 1000 ""The given statement is Correct"" ""The given statement is Wrong"""
'Updates the document fields
document.UpdateDocumentFields()
document.Save("Sample.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% highlight UWP %}
//Creates an instance of a WordDocument
WordDocument document = new WordDocument();
//Adds a new section into the Word Document
IWSection section = document.AddSection();
//Adds a new paragraph into Word document and appends text into paragraph
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
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word file in local machine
Save(stream, "Sample.docx");
//Closes the document
document.Close();
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight ASP.NET Core %}
//Creates an instance of a WordDocument
WordDocument document = new WordDocument();
//Adds a new section into the Word Document
IWSection section = document.AddSection();
//Adds a new paragraph into Word document and appends text into paragraph
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
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Sample.docx");
{% endhighlight %}

{% highlight Xamarin %}
//Creates an instance of a WordDocument
WordDocument document = new WordDocument();
//Adds a new section into the Word Document
IWSection section = document.AddSection();
//Adds a new paragraph into Word document and appends text into paragraph
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
//Saves the Word document to  MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.docx", "application/msword", stream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %} 
  
## Document Variables

The DocVariable field displays the value of a specified document variable in the Word document. The document variables can be added or modified using `Variables` property of `WordDocument` class.

The following code example illustrate how to add a DocVariable field in Word document.

{% tabs %}  

{% highlight c# %}
//Creates an instance of a WordDocument 
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

{% highlight vb.net %}
'Creates an instance of a WordDocument 
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

{% highlight UWP %}
//Creates an instance of a WordDocument
WordDocument document = new WordDocument();
//Adds a new section into the Word Document
IWSection section = document.AddSection();
//Adds a new paragraph into Word document and appends text into paragraph
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
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word file in local machine
Save(stream, "Sample.docx");
//Closes the document
document.Close();
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight ASP.NET Core %}
//Creates an instance of a WordDocument
WordDocument document = new WordDocument();
//Adds a new section into the Word Document
IWSection section = document.AddSection();
//Adds a new paragraph into Word document and appends text into paragraph
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
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Sample.docx");
{% endhighlight %}

{% highlight Xamarin %}
//Creates an instance of a WordDocument
WordDocument document = new WordDocument();
//Adds a new section into the Word Document
IWSection section = document.AddSection();
//Adds a new paragraph into Word document and appends text into paragraph
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
//Saves the Word document to  MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.docx", "application/msword", stream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}
  
## Cross Reference

A cross-reference refers to an item that appears in another location in a document. You can create cross-reference to bookmarks in a document by using `AppendCrossReference` method of `WParagraph` class.

N>  Essential DocIO supports to create and update cross-reference fields only for bookmarks in a document

The following code example illustrate how to append cross reference for bookmark in Word document.

{% tabs %}  

{% highlight c# %}
//Creates an instance of a WordDocument 
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

{% highlight vb.net %}
'Creates an instance of a WordDocument 
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

{% highlight UWP %}
//Creates an instance of a WordDocument
WordDocument document = new WordDocument();
//Adds a new section into the Word Document
IWSection section = document.AddSection();
//Adds a new paragraph into Word document
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
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word file in local machine
Save(stream, "Sample.docx");
//Closes the document
document.Close();
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight ASP.NET Core %}
//Creates an instance of a WordDocument
WordDocument document = new WordDocument();
//Adds a new section into the Word Document
IWSection section = document.AddSection();
//Adds a new paragraph into Word document
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
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Sample.docx");
{% endhighlight %}

{% highlight Xamarin %}
//Creates an instance of a WordDocument
WordDocument document = new WordDocument();
//Adds a new section into the Word Document
IWSection section = document.AddSection();
//Adds a new paragraph into Word document
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
//Saves the Word document to  MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.docx", "application/msword", stream);
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}  

## Unlink fields

You can replace the field with its most recent result in the Word document by unlinking the field using `Unlink` API. When you unlink a field, its current result is converted to text or a graphic and can no longer be updated automatically.


The following code example shows how to unlink the fields in Word document.

{% tabs %}  

{% highlight C# %}
//Creates an instance of WordDocument class
WordDocument document = new WordDocument();
//Adds a new section into the Word Document
IWSection section = document.AddSection();
//Adds a new paragraph into Word document and appends text into paragraph
IWParagraph paragraph = section.AddParagraph();
paragraph.AppendText("Today's Date: ");
//Adds the new Date field in Word document with field name and its type
WField field = paragraph.AppendField("Date", FieldType.FieldDate) as WField;
//Updates the field
field.Update();
//Unlink the field
field.Unlink();
//Saves the document in the given name and format
document.Save("Sample.docx", FormatType.Docx);
//Releases the resources occupied by WordDocument instance
document.Close();
{% endhighlight %}

{% highlight VB.NET %}
'Creates an instance of WordDocument class
Dim document As WordDocument = New WordDocument()
'Adds a new section into the Word Document
Dim section As IWSection = document.AddSection()
'Adds a new paragraph into Word document and appends text into paragraph
Dim paragraph As IWParagraph = section.AddParagraph()
paragraph.AppendText("Today's Date: ")
'Adds the new Date field in Word document with field name and its type
Dim field As WField = CType(paragraph.AppendField("Date", FieldType.FieldDate), WField)
'Updates the field
field.Update()
'Unlink the field
field.Unlink()
'Saves the document in the given name and format
document.Save("Sample.docx", FormatType.Docx)
'Releases the resources occupied by WordDocument instance
document.Close()
{% endhighlight %}

{% highlight UWP %}
//Creates an instance of WordDocument class
WordDocument document = new WordDocument();
//Adds a new section into the Word Document
IWSection section = document.AddSection();
//Adds a new paragraph into Word document and appends text into paragraph
IWParagraph paragraph = section.AddParagraph();
paragraph.AppendText("Today's Date: ");
//Adds the new Date field in Word document with field name and its type
WField field = paragraph.AppendField("Date", FieldType.FieldDate) as WField;
//Updates the field
field.Update();
//Unlink the field
field.Unlink();
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
document.Close();
//Saves the stream as Word file in local machine
Save(stream, "Sample.docx");

//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight ASP.NET CORE %}
//Creates an instance of WordDocument class
WordDocument document = new WordDocument();
//Adds a new section into the Word Document
IWSection section = document.AddSection();
//Adds a new paragraph into Word document and appends text into paragraph
IWParagraph paragraph = section.AddParagraph();
paragraph.AppendText("Today's Date: ");
//Adds the new Date field in Word document with field name and its type
WField field = paragraph.AppendField("Date", FieldType.FieldDate) as WField;
//Updates the field
field.Update();
//Unlink the field
field.Unlink();
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
//Closes the Word document instance
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Sample.docx");
{% endhighlight %}

{% highlight XAMARIN %}
//Creates an instance of WordDocument class
WordDocument document = new WordDocument();
//Adds a new section into the Word Document
IWSection section = document.AddSection();
//Adds a new paragraph into Word document and appends text into paragraph
IWParagraph paragraph = section.AddParagraph();
paragraph.AppendText("Today's Date: ");
//Adds the new Date field in Word document with field name and its type
WField field = paragraph.AppendField("Date", FieldType.FieldDate) as WField;
//Updates the field
field.Update();
//Unlink the field
field.Unlink();
//Saves and closes the Word document instance
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.docx", "application/msword", stream);

//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}

N>  Fields such as XE (Index Entry) fields and SEQ (Sequence) fields cannot be unlinked.