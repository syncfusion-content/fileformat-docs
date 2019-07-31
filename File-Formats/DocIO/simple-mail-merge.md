---
title: Simple Mail merge | Word library (DocIO) | Syncfusion
description: This section illustrates how to Mail merge - replace all merge fields in a document with data, by repeating whole document for each record in data source.
platform: file-formats
control: DocIO
documentation: UG
---

# Simple Mail merge

The `MailMerge` class provides various overloads for `Execute` method to perform Mail merge from various data sources. The Mail merge operation replaces the matching merge fields with the respective data.

The following code example shows how to create a Word template document with merge fields.

{% tabs %}  

{% highlight c# %}

//Creates an instance of a WordDocument
 
WordDocument document = new WordDocument();

//Adds one section and one paragraph to the document

document.EnsureMinimal();

//Sets page margins to the last section of the document

document.LastSection.PageSetup.Margins.All = 72;

//Appends text to the last paragraph

document.LastParagraph.AppendText("EmployeeId: ");

//Appends merge field to the last paragraph

document.LastParagraph.AppendField("EmployeeId", FieldType.FieldMergeField);

document.LastParagraph.AppendText("\nName: ");

document.LastParagraph.AppendField("Name", FieldType.FieldMergeField);

document.LastParagraph.AppendText("\nPhone: ");

document.LastParagraph.AppendField("Phone", FieldType.FieldMergeField);

document.LastParagraph.AppendText("\nCity: ");

document.LastParagraph.AppendField("City", FieldType.FieldMergeField);

//Saves and closes the WordDocument instance

document.Save("Template.docx", FormatType.Docx);

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates an instance of a WordDocument 

Dim document As New WordDocument()

'Adds one section and one paragraph to the document

document.EnsureMinimal()

'Sets page margins to the last section of the document

document.LastSection.PageSetup.Margins.All = 72

'Appends text to the last paragraph

document.LastParagraph.AppendText("EmployeeId: ")

'Appends merge field to the last paragraph

document.LastParagraph.AppendField("EmployeeId", FieldType.FieldMergeField)

document.LastParagraph.AppendText(vbLf & "Name: ")

document.LastParagraph.AppendField("Name", FieldType.FieldMergeField)

document.LastParagraph.AppendText(vbLf & "Phone: ")

document.LastParagraph.AppendField("Phone", FieldType.FieldMergeField)

document.LastParagraph.AppendText(vbLf & "City: ")

document.LastParagraph.AppendField("City", FieldType.FieldMergeField)

'Saves and closes the WordDocument instance

document.Save("Template.docx", FormatType.Docx)

document.Close()

{% endhighlight %}

{% endtabs %}

The generated template document looks as follows.

![Template document](MailMerge_images/MailMerge_img2.jpeg)

The following code example shows how to perform a simple Mail merge in the generated template document with string array as data source.

{% tabs %}  

{% highlight c# %}

//Opens the template document

WordDocument document = new WordDocument("Template.docx");

string[] fieldNames = new string[] { "EmployeeId", "Name", "Phone", "City" };

string[] fieldValues = new string[] { "1001", "Peter", "+122-2222222", "London" };

//Performs the mail merge

document.MailMerge.Execute(fieldNames, fieldValues);

//Saves and closes the WordDocument instance

document.Save("Sample.docx", FormatType.Docx);

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens the template document

Dim document As New WordDocument("Template.docx")

Dim fieldNames As String() = New String() {"EmployeeId", "Name", "Phone", "City"}

Dim fieldValues As String() = New String() {"1001", "Peter", "+122-2222222", "London"}

'Performs the mail merge

document.MailMerge.Execute(fieldNames, fieldValues)

'Saves and closes the WordDocument instance

document.Save("Sample.docx", FormatType.Docx)

document.Close()

{% endhighlight %}

{% endtabs %}

The resultant document looks as follows.

![Resultant document](MailMerge_images/MailMerge_img3.jpeg)

You can find more examples about various overloads of the `Execute` method from the following table:

<table>
<thead>
<tr>
<td><b>Overloads</b></td>
<td><b>Examples</b></td>
</tr>
</thead>
<tr>
<td>Execute(IEnumerable)</td>
<td>
<a href="http://www.syncfusion.com/downloads/support/directtrac/general/ze/MAAA1B~11635160515.zip">Create envelopes for mailings</a>
</td>
</tr>
<tr>
<td>Execute(DataRow)</td>
<td>
<a href="http://www.syncfusion.com/downloads/support/directtrac/general/ze/MAAA1B~11635160515.zip">Generate multiple Word documents</a>
</td>
</tr>
<tr>
<td>Execute(DataTable)</td>
<td>
<a href="http://www.syncfusion.com/downloads/support/directtrac/general/ze/MAAA1B~11635160515.zip">Generate notice to renew lease</a>
</td>
</tr>
<tr>
<td>Execute(DataView)</td>
<td>
<a href="http://www.syncfusion.com/downloads/support/directtrac/general/ze/MAAA1B~11635160515.zip">Generate letter for candidates in sorted order</a>
</td>
</tr>
<tr>
<td>Execute(OleDbDataReader)</td>
<td>
<a href="http://www.syncfusion.com/downloads/support/directtrac/general/ze/MAAA1B~11635160515.zip">Generate certificates for employees</a>
</td>
</tr>
<tr>
<td>Execute(IDataReader)</td>
<td>
<a href="http://www.syncfusion.com/downloads/support/directtrac/general/ze/MAAA1B~11635160515.zip">Generate payroll for multiple employees</a>
</td>
</tr>
</table>