---
layout: Post
title: Working with Macros
description: This section illustrates how to load and save a macro enabled documents
platform: FileFormat
control: DocIO
documentation: UG
---
# Working with Macros

Macro is a way to automate the tasks that you perform repeatedly. It is a saved sequence of commands or keyboard strokes that can be recalled with a single command or keyboard stroke. 

The following link shows how to create a macro in the Word document.

[https://support.office.com/en-in/article/Create-or-run-a-macro-c6b99036-905c-49a6-818a-dfb98b7c3c9c](https://support.office.com/en-in/article/Create-or-run-a-macro-c6b99036-905c-49a6-818a-dfb98b7c3c9c# "")

The following code illustrates snippet how to load and save a macro enabled document.

{% highlight c# %}
[C#]

// Load the macro-enabled template.

WordDocument document = new WordDocument("Template.dotm");

// Get the table

DataTable table = GetDataTable();

// Execute Mail Merge with groups.

document.MailMerge.ExecuteGroup(table);

//Save and close the document

document.Save("Sample.docm", FormatType.Word2013Docm);

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB]

'Load the macro-enabled template.

Dim document As New WordDocument("Template.dotm")

'Get the table

Dim table As DataTable = GetDataTable()

'Execute Mail Merge with groups.

document.MailMerge.ExecuteGroup(table)

'Save and close the document

document.Save("Sample.docm", FormatType.Word2013Docm)

document.Close()



{% endhighlight %}

The following code snippet illustrates the method used to get the tables from data set.

{% highlight c# %}
[C#]

private DataTable GetDataTable()

{

// List of syncfusion products name.

string[] products = { "DocIO", "PDF", "XlsIO" };

// Add new Tables to the data set.

DataRow row;

DataTable table = new DataTable();

// Add fields to the Products table.

table.TableName = "Products";

table.Columns.Add("ProductName");

table.Columns.Add("Binary");

table.Columns.Add("Source");

// Inserting values to the tables.

foreach (string product in products)

{

row = table.NewRow();

row["ProductName"] = string.Concat("Essential ", product);

row["Binary"] = "$895.00";

row["Source"] = "$1,295.00";

table.Rows.Add(row);

}

return table;

}



{% endhighlight %}

{% highlight vbnet %}
[VB]

Private Function GetDataTable() As DataTable

'List of syncfusion products name.

Dim products As String() = {"DocIO", "PDF", "XlsIO"}

'Add new Tables to the data set.

Dim row As DataRow

Dim table As New DataTable()

'Add fields to the Products table.

table.TableName = "Products"

table.Columns.Add("ProductName")

table.Columns.Add("Binary")

table.Columns.Add("Source")

'Inserting values to the tables.

For Each product As String In products

row = table.NewRow()

row("ProductName") = String.Concat("Essential ", product)

row("Binary") = "$895.00"

row("Source") = "$1,295.00"

table.Rows.Add(row)

Next

Return table

End Function 



{% endhighlight %}

The following code snippet illustrates how to remove the macros present in the document using RemoveMacros method.

{% highlight c# %}
[C#]

//Load the document with macros

WordDocument document = new WordDocument("Sample.docm");

//Check whether the document has macros and remove them

if (document.HasMacros)

document.RemoveMacros();

//Save the document

document.Save("Sample.docx", FormatType.Docx);

//Close the document

document.Close();



{% endhighlight %}

{% highlight vbnet %}
[VB]

'Load the document with macros

Dim document As New WordDocument("Sample.docm")

'Check whether the document has macros and remove them

If document.HasMacros Then

document.RemoveMacros()

End If

'Save the document

document.Save("Sample.docx", FormatType.Docx)

'Close the document

document.Close()





{% endhighlight %}

