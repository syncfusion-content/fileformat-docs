---
title: Simple Mail merge in C# | DocIO | Syncfusion
description: Learn how to Mail merge - replace all merge fields with data, by repeating whole document for each record in data source using the .NET Word (DocIO) library.
platform: file-formats
control: DocIO
documentation: UG
---

# Simple Mail merge in Word document

You can create a Word document template using Microsoft Word application or by adding merge fields in the Word document programmatically. For further information, click [here](https://help.syncfusion.com/file-formats/docio/working-with-mail-merge#create-word-document-template).

## Mail merge with string arrays

The [MailMerge](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.MailMerge.html) class provides various overloads for [Execute](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.MailMerge.html#Syncfusion_DocIO_DLS_MailMerge_Execute_System_String___System_String___) method to perform Mail merge from various data sources. The Mail merge operation replaces the matching merge fields with the respective data.

### Create Word document template

The following code example shows how to create a Word template document with merge fields.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Creates an instance of a WordDocument 
WordDocument document = new WordDocument();
//Adds one section and one paragraph to the document
document.EnsureMinimal();
//Sets page margins to the last section of the document
document.LastSection.PageSetup.Margins.All = 72;
//Appends text to the last paragraph.
document.LastParagraph.AppendText("EmployeeId: ");
//Appends merge field to the last paragraph.
document.LastParagraph.AppendField("EmployeeId", FieldType.FieldMergeField);
document.LastParagraph.AppendText("\nName: ");
document.LastParagraph.AppendField("Name", FieldType.FieldMergeField);
document.LastParagraph.AppendText("\nPhone: ");
document.LastParagraph.AppendField("Phone", FieldType.FieldMergeField);
document.LastParagraph.AppendText("\nCity: ");
document.LastParagraph.AppendField("City", FieldType.FieldMergeField);
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the Word document
document.Close();
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Creates an instance of a WordDocument 
WordDocument document = new WordDocument();
//Adds one section and one paragraph to the document
document.EnsureMinimal();
//Sets page margins to the last section of the document
document.LastSection.PageSetup.Margins.All = 72;
//Appends text to the last paragraph.
document.LastParagraph.AppendText("EmployeeId: ");
//Appends merge field to the last paragraph.
document.LastParagraph.AppendField("EmployeeId", FieldType.FieldMergeField);
document.LastParagraph.AppendText("\nName: ");
document.LastParagraph.AppendField("Name", FieldType.FieldMergeField);
document.LastParagraph.AppendText("\nPhone: ");
document.LastParagraph.AppendField("Phone", FieldType.FieldMergeField);
document.LastParagraph.AppendText("\nCity: ");
document.LastParagraph.AppendField("City", FieldType.FieldMergeField);
//Saves and closes the WordDocument instance.
document.Save("Template.docx", FormatType.Docx);
document.Close();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
'Creates an instance of a WordDocument 
Dim document As New WordDocument()
'Adds one section and one paragraph to the document
document.EnsureMinimal()
'Sets page margins to the last section of the document
document.LastSection.PageSetup.Margins.All = 72
'Appends text to the last paragraph.
document.LastParagraph.AppendText("EmployeeId: ")
'Appends merge field to the last paragraph.
document.LastParagraph.AppendField("EmployeeId", FieldType.FieldMergeField)
document.LastParagraph.AppendText(vbLf & "Name: ")
document.LastParagraph.AppendField("Name", FieldType.FieldMergeField)
document.LastParagraph.AppendText(vbLf & "Phone: ")
document.LastParagraph.AppendField("Phone", FieldType.FieldMergeField)
document.LastParagraph.AppendText(vbLf & "City: ")
document.LastParagraph.AppendField("City", FieldType.FieldMergeField)
'Saves and closes the WordDocument instance.
document.Save("Template.docx", FormatType.Docx)
document.Close()
{% endhighlight %}

{% endtabs %}  

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Mail-Merge/Create-Word-document-template).

The generated template document looks as follows.

![Word document template](../MailMerge_images/Simple_mail_merge_template.png)

### Execute mail merge

The following code example shows how to perform a simple Mail merge in the generated template document with string array as data source.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Opens the template document
FileStream fileStreamPath = new FileStream("Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);
string[] fieldNames = new string[] { "EmployeeId", "Name", "Phone", "City" };
string[] fieldValues = new string[] { "1001", "Peter", "+122-2222222", "London" };
//Performs the mail merge
document.MailMerge.Execute(fieldNames, fieldValues);
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Closes the Word document
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Sample.docx");
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Mail-Merge/Mail-merge-with-string-arrays).

The resultant document looks as follows.

![Mail merged Word document](../MailMerge_images/Simple_mail_merge_output.png)

## See Also

The following table illustrates the supported mail merge overloads for Execute method.

<table>
<tr>
<th>Overloads<br/><br/></th>
<th>Examples<br/><br/></th>
</tr>
<tbody>
<tr>
<td>{{'[Execute(IEnumerable)](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.MailMerge.html#Syncfusion_DocIO_DLS_MailMerge_Execute_System_Collections_IEnumerable_)'| markdownify }}</td>
<td>{{'[Create Envelopes for mailings](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Mail-Merge/Create-Envelopes-for-mailing)'| markdownify }}</td>
</tr>
<tr>
<td>{{'[Execute(DataRow)](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.MailMerge.html#Syncfusion_DocIO_DLS_MailMerge_Execute_System_Data_DataRow_)'| markdownify }}</td>
<td>{{'[Generate multiple Word documents](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Mail-Merge/Generate-multiple-Word-documents)'| markdownify }}</td>
</tr>
<tr>
<td>{{'[Execute(DataTable)](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.MailMerge.html#Syncfusion_DocIO_DLS_MailMerge_Execute_System_Data_DataTable_)'| markdownify }}</td>
<td>{{'[Generate notice to renew lease](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Mail-Merge/Generate-notice-to-renew-lease)'| markdownify }}</td>
</tr>
<tr>
<td>{{'[Execute(DataView)](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.MailMerge.html#Syncfusion_DocIO_DLS_MailMerge_Execute_System_Data_DataView_)'| markdownify }}</td>
<td>{{'[Generate letter for candidates in sorted order](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Mail-Merge/Generate-letter-for-candidates-in-sorted-order)'| markdownify }}</td>
</tr>
<tr>
<td>{{'[Execute(OleDbDataReader)](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.MailMerge.html#Syncfusion_DocIO_DLS_MailMerge_Execute_System_Data_OleDb_OleDbDataReader_)'| markdownify }}</td>
<td>{{'[Generate certificates for employees](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Mail-Merge/Generate-certificate-for-employees)'| markdownify }}</td>
</tr>
<tr>
<td>{{'[Execute(IDataReader)](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.MailMerge.html#Syncfusion_DocIO_DLS_MailMerge_Execute_System_Data_IDataReader_)'| markdownify }}</td>
<td>{{'[Generate payroll for employees](https://github.com/SyncfusionExamples/DocIO-Examples/tree/main/Mail-Merge/Generate-payroll-for-employees)'| markdownify }}</td>
</tr>
</tbody>
</table>