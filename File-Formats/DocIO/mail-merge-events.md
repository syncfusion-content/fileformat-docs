---
title: Mail merge events | Word library (DocIO) | Syncfusion
description: This section illustrates how to format or customize the merged text and image, clear or retain unmerged fields during mail merge using events.
platform: file-formats
control: DocIO
documentation: UG
---

# Event support for Mail merge

The MailMerge class provides event support to customize the document contents and merging image data during the Mail merge process. The following events are supported by Essential DocIO in Mail merge process:

* `MergeField`- occurs during Mail merge when a Mail merge field except image Mail merge field is encountered in the document.
* `MergeImageField`- occurs during Mail merge when an image Mail merge field is encountered in the document.
* `BeforeClearField`- occurs during Mail merge when an unmerged field is encountered in the document.
* `BeforeClearGroupField`- occurs during Mail merge when an unmerged group field is encountered in the document.

## MergeField Event

The following code example shows how to use the MergeField event during Mail merge process.

{% tabs %}  

{% highlight c# %}
//Opens the template document 
WordDocument document = new WordDocument("Template.docx");    
//Uses the mail merge events to perform the conditional formatting during runtime
document.MailMerge.MergeField += new MergeFieldEventHandler(ApplyAlternateRecordsTextColor);
//Executes Mail Merge with groups
document.MailMerge.ExecuteGroup(GetDataTable());
//Saves and closes the Word document instance
document.Save("Sample.docx");
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Opens the template document 
Dim document As New WordDocument("Template.docx")
'Uses the mail merge events to perform the conditional formatting during runtime
AddHandler document.MailMerge.MergeField, AddressOf ApplyAlternateRecordsTextColor
'Executes Mail Merge with groups
document.MailMerge.ExecuteGroup(GetDataTable())
'Saves and closes the Word document instance
document.Save("Sample.docx")
document.Close()
{% endhighlight %}

{% highlight UWP %}
//DocIO supports performing mail merge with ADO.NET objects in Windows Forms, WPF, ASP.NET, ASP.NET MVC, ASP.NET Core, and Xamarin platforms alone.
{% endhighlight %}

{% highlight ASP.NET CORE %}
//Opens the template document 
FileStream fileStreamPath = new FileStream("Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);  
//Uses the mail merge events to perform the conditional formatting during runtime
document.MailMerge.MergeField += new MergeFieldEventHandler(ApplyAlternateRecordsTextColor);
//Executes Mail Merge with groups
document.MailMerge.ExecuteGroup(GetDataTable());
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Sample.docx");
{% endhighlight %}

{% highlight XAMARIN %}
//Opens the template document
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Docx);
//Uses the mail merge events to perform the conditional formatting during runtime
document.MailMerge.MergeField += new MergeFieldEventHandler(ApplyAlternateRecordsTextColor);
//Executes Mail Merge with groups
document.MailMerge.ExecuteGroup(GetDataTable());
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Template.docx", "application/msword", stream);
//Closes the document 
document.Close();
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %} 

{% endtabs %}  

The following code example shows how to set text color to the alternate Mail merge record by using MergeFieldEventHandler.

{% tabs %} 

{% highlight C# %}
private void ApplyAlternateRecordsTextColor (object sender, MergeFieldEventArgs args)
{
	//Sets text color to the alternate mail merge record
	if (args.RowIndex % 2 == 0)
	{
		args.TextRange.CharacterFormat.TextColor = Color.FromArgb(255, 102, 0);
	}
}
{% endhighlight %}

{% highlight vb.net %}
Private Sub ApplyAlternateRecordsTextColor(ByVal sender As Object, ByVal args As MergeFieldEventArgs)
	'Sets text color to the alternate mail merge record
	If ((args.RowIndex Mod 2) = 0) Then
		args.TextRange.CharacterFormat.TextColor = Color.FromArgb(255, 102, 0)
	End If
End Sub
{% endhighlight %}

{% highlight UWP %}
//DocIO supports performing mail merge with ADO.NET objects in Windows Forms, WPF, ASP.NET, ASP.NET MVC, ASP.NET Core, and Xamarin platforms alone.
{% endhighlight %}

{% highlight ASP.NET CORE %}
private void ApplyAlternateRecordsTextColor (object sender, MergeFieldEventArgs args)
{
	//Sets text color to the alternate mail merge record
	if (args.RowIndex % 2 == 0)
	{
		args.TextRange.CharacterFormat.TextColor = Color.FromArgb(255, 102, 0);
	}
}
{% endhighlight %}

{% highlight XAMARIN %}
private void ApplyAlternateRecordsTextColor (object sender, MergeFieldEventArgs args)
{
	//Sets text color to the alternate mail merge record
	if (args.RowIndex % 2 == 0)
	{
		args.TextRange.CharacterFormat.TextColor = Syncfusion.Drawing.Color.FromArgb(255, 102, 0);
	}
}
{% endhighlight %}

{% endtabs %}  

The following code example provides supporting methods

{% tabs %} 

{% highlight C# %}
private static DataTable GetDataTable()
{
	DataTable dataTable = new DataTable("Employee");
	dataTable.Columns.Add("EmployeeName");
	dataTable.Columns.Add("EmployeeNumber");
	for (int i = 0; i < 20; i++)
	{
		DataRow datarow = dataTable.NewRow();
		dataTable.Rows.Add(datarow);
		datarow[0] = "Employee" + i.ToString();
		datarow[1] = "EMP" + i.ToString();
	}
	return dataTable;
}
{% endhighlight %}

{% highlight vb.net %}
Private Function GetDataTable() As DataTable
	Dim dataTable As New DataTable("Employee")
	dataTable.Columns.Add("EmployeeName")
	dataTable.Columns.Add("EmployeeNumber")
	For i As Integer = 0 To 19
		Dim datarow As DataRow = dataTable.NewRow()
		dataTable.Rows.Add(datarow)
		datarow(0) = "Employee" + i.ToString()
		datarow(1) = "EMP" + i.ToString()
	Next
	Return dataTable
End Function
{% endhighlight %}

{% highlight UWP %}
//DocIO supports performing mail merge with ADO.NET objects in Windows Forms, WPF, ASP.NET, ASP.NET MVC, ASP.NET Core, and Xamarin platforms alone.
{% endhighlight %}

{% highlight ASP.NET CORE %}
private static DataTable GetDataTable()
{
	DataTable dataTable = new DataTable("Employee");
	dataTable.Columns.Add("EmployeeName");
	dataTable.Columns.Add("EmployeeNumber");
	for (int i = 0; i < 20; i++)
	{
		DataRow datarow = dataTable.NewRow();
		dataTable.Rows.Add(datarow);
		datarow[0] = "Employee" + i.ToString();
		datarow[1] = "EMP" + i.ToString();
	}
	return dataTable;
}
{% endhighlight %} 

{% highlight XAMARIN %}
private static DataTable GetDataTable()
{
	DataTable dataTable = new DataTable("Employee");
	dataTable.Columns.Add("EmployeeName");
	dataTable.Columns.Add("EmployeeNumber");
	for (int i = 0; i < 20; i++)
	{
		DataRow datarow = dataTable.NewRow();
		dataTable.Rows.Add(datarow);
		datarow[0] = "Employee" + i.ToString();
		datarow[1] = "EMP" + i.ToString();
	}
	return dataTable;
}
{% endhighlight %}

{% endtabs %} 

## MergeImageField Event

The following code example shows how to use the MergeImageField event during Mail merge process.

{% tabs %}  

{% highlight c# %}
//Opens the template document
WordDocument document = new WordDocument("Template.docx");
//Uses the mail merge events handler for image fields
document.MailMerge.MergeImageField += new MergeImageFieldEventHandler(MergeField_ProductImage);
//Specifies the field names and field values
string[] fieldNames = new string[] { "Logo"};
string[] fieldValues = new string[] { "Logo.png"};
//Executes the mail merge with groups
document.MailMerge.Execute(fieldNames, fieldValues);
//Saves and closes WordDocument instance
document.Save("Sample.docx");
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Opens the template document
Dim document As New WordDocument("Template.docx")
'Uses the mail merge events handler for image fields
AddHandler document.MailMerge.MergeImageField, AddressOf MergeField_ProductImage
'Specifies the field names and field values
Dim fieldNames As String() = New String() {"Logo"}
Dim fieldValues As String() = New String() {"Logo.png"}
'Executes the mail merge with groups
document.MailMerge.Execute(fieldNames, fieldValues)
'Saves and closes WordDocument instance
document.Save("Sample.docx")
document.Close()
{% endhighlight %}

{% highlight UWP %}
//Creates an instance of a WordDocument
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
WordDocument document = new WordDocument();
document.Open(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Docx);
//Uses the mail merge events handler for image fields
document.MailMerge.MergeImageField += new MergeImageFieldEventHandler(MergeField_ProductImage);
//Specifies the field names and field values
string[] fieldNames = new string[] { "Logo"};
string[] fieldValues = new string[] { "Sample.Assets.Logo.png"};
//Executes the mail merge with groups
document.MailMerge.Execute(fieldNames, fieldValues);
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word file in local machine
Save(stream, "Sample.docx");
document.Close();
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight ASP.NET CORE %}
//Opens the template document
FileStream fileStreamPath = new FileStream("Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);
//Uses the mail merge events handler for image fields
document.MailMerge.MergeImageField += new MergeImageFieldEventHandler(MergeField_ProductImage);
//Specifies the field names and field values
string[] fieldNames = new string[] { "Logo"};
string[] fieldValues = new string[] { "Logo.png"};
//Executes the mail merge with groups
document.MailMerge.Execute(fieldNames, fieldValues);
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Sample.docx");
{% endhighlight %}

{% highlight XAMARIN %}
//Opens the template document
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Docx);
//Uses the mail merge events handler for image fields
document.MailMerge.MergeImageField += new MergeImageFieldEventHandler(MergeField_ProductImage);
//Specifies the field names and field values
string[] fieldNames = new string[] { "Logo"};
string[] fieldValues = new string[] { "Sample.Assets.Logo.png"};
//Executes the mail merge with groups
document.MailMerge.Execute(fieldNames, fieldValues);
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Template.docx", "application/msword", stream);
//Closes the document 
document.Close();
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}  
  
The following code example shows how to bind the image from file system during Mail merge process by using MergeImageFieldEventHandler.

{% tabs %}  

{% highlight c# %}
private void MergeField_ProductImage(object sender, MergeImageFieldEventArgs args)
{ 
	//Binds image from file system during mail merge
	if (args.FieldName == "Logo")
	{
		string ProductFileName = args.FieldValue.ToString();
		//Gets the image from file system
		args.Image = Image.FromFile(ProductFileName);
		//Gets the picture, to be merged for image merge field
		WPicture picture = args.Picture;
		//Resizes the picture
		picture.Height = 50;
		picture.Width = 150;
	}
}
{% endhighlight %}

{% highlight vb.net %}
Private Sub MergeField_ProductImage(ByVal sender As Object, ByVal args As MergeImageFieldEventArgs)
	'Binds image from file system during mail merge
	If args.FieldName = "Logo" Then
		Dim ProductFileName As String = args.FieldValue.ToString()
		'Gets the image from file system
		args.Image = Image.FromFile(ProductFileName)
		'Gets the picture, to be merged for image merge field
		Dim picture As WPicture = args.Picture
		'Resizes the picture
		picture.Height = 50
		picture.Width = 150
	End If
End Sub
{% endhighlight %}

{% highlight UWP %}
private void MergeField_ProductImage(object sender, MergeImageFieldEventArgs args)
{ 
	//Binds image from file system during mail merge
	if (args.FieldName == "Logo")
	{
		string ProductFileName = args.FieldValue.ToString();
		//Gets the image from file system
		Assembly assembly = typeof(App).GetTypeInfo().Assembly;
		args.ImageStream = assembly.GetManifestResourceStream(ProductFileName);
		//Gets the picture, to be merged for image merge field
		WPicture picture = args.Picture;
		//Resizes the picture
		picture.Height = 50;
		picture.Width = 150;
	}
}
{% endhighlight %}

{% highlight ASP.NET CORE %}
private void MergeField_ProductImage(object sender, MergeImageFieldEventArgs args)
{ 
	//Binds image from file system during mail merge
	if (args.FieldName == "Logo")
	{
		string ProductFileName = args.FieldValue.ToString();
		//Gets the image from file system
		FileStream imageStream = new FileStream(ProductFileName, FileMode.Open, FileAccess.Read);
		args.ImageStream = imageStream;
		//Gets the picture, to be merged for image merge field
		WPicture picture = args.Picture;
		//Resizes the picture
		picture.Height = 50;
		picture.Width = 150;
	}
}
{% endhighlight %}

{% highlight XAMARIN %}
private void MergeField_ProductImage(object sender, MergeImageFieldEventArgs args)
{ 
	//Binds image from file system during mail merge
	if (args.FieldName == "Logo")
	{
		string ProductFileName = args.FieldValue.ToString();
		//Gets the image from file system
		Assembly assembly = typeof(App).GetTypeInfo().Assembly;
		args.ImageStream = assembly.GetManifestResourceStream(ProductFileName);
		//Gets the picture, to be merged for image merge field
		WPicture picture = args.Picture;
		//Resizes the picture
		picture.Height = 50;
		picture.Width = 150;
	}
}
{% endhighlight %}

{% endtabs %} 

## BeforeClearField Event

The following code example shows how to use the BeforeClearField event during Mail merge process.

{% tabs %}  

{% highlight c# %}
//Opens the template document 
WordDocument document = new WordDocument("Template.docx");
//Sets “ClearFields” to true to remove empty mail merge fields from document
document.MailMerge.ClearFields = false;
//Uses the mail merge event to clear the unmerged field while perform mail merge execution
document.MailMerge.BeforeClearField += new BeforeClearFieldEventHandler(BeforeClearFieldEvent);
//Execute mail merge
document.MailMerge.ExecuteGroup(GetDataTable());
//Saves and closes the WordDocument instance
document.Save("Sample.docx");
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Opens the template document 
Dim document As WordDocument = New WordDocument("Template.docx")
'Sets “ClearFields” to true to remove empty mail merge fields from document
document.MailMerge.ClearFields = False
'Uses the mail merge event to clear the unmerged field while perform mail merge execution
document.MailMerge.BeforeClearField += New BeforeClearFieldEventHandler(AddressOf BeforeClearField)
'Execute mail merge
document.MailMerge.ExecuteGroup(GetDataTable())
'Saves and closes the WordDocument instance
document.Save("Sample.docx")
document.Close()
{% endhighlight %}

{% highlight UWP %}
//DocIO supports performing mail merge in BeforeClearField Event in Windows Forms, WPF, ASP.NET, ASP.NET MVC, ASP.NET Core and Xamarin platforms alone.
{% endhighlight %}

{% highlight ASP.NET CORE %}
//Opens the template document 
FileStream fileStreamPath = new FileStream("Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
WordDocument document = new WordDocument(fileStreamPath);
//Sets “ClearFields” to true to remove empty mail merge fields from document
document.MailMerge.ClearFields = false;
//Uses the mail merge event to clear the unmerged field while perform mail merge execution
document.MailMerge.BeforeClearField += new BeforeClearFieldEventHandler(BeforeClearFieldEvent);
//Execute mail merge
document.MailMerge.ExecuteGroup(GetDataTable());
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Sample.docx");
{% endhighlight %}

{% highlight XAMARIN %}
//Opens the template document
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Docx);
//Sets “ClearFields” to true to remove empty mail merge fields from document
document.MailMerge.ClearFields = false;
//Uses the mail merge event to clear the unmerged field while perform mail merge execution
document.MailMerge.BeforeClearField += new BeforeClearFieldEventHandler(BeforeClearFieldEvent);
//Execute mail merge
document.MailMerge.ExecuteGroup(GetDataTable());
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.docx", "application/msword", stream);
//Closes the document 
document.Close();
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %} 

The following code example shows how to bind the data to unmerged fields during Mail merge process by using BeforeClearFieldEventHandler.

{% tabs %}  

{% highlight c# %}
private void BeforeClearFieldEvent (object sender, BeforeClearFieldEventArgs args)
{
	if (args.HasMappedFieldInDataSource)
	{
		//To check whether the mapped field has null value
		if (args.FieldValue == null || args.FieldValue == DBNull.Value)
		{
			//Gets the unmnerged field name
			string unmergedFieldName = args.FieldName;
			string ownerGroup = args.GroupName;
			//Sets error message for unmerged fields
			args.FieldValue = "Error! The value of MergeField " + unmergedFieldName + " of owner group " + ownerGroup + " is defined as Null in the data source.";
		}
		else
			//If field value is empty, you can set whether the unmerged merge field can be clear or not
			args.ClearField = true;
	}
	else
	{
		string unmergedFieldName = args.FieldName;
		//Sets error message for unmerged fields, which is not found in data source
		args.FieldValue = "Error! The value of MergeField " + unmergedFieldName + " is not found in the data source.";
	}
}
{% endhighlight %}

{% highlight vb.net %}
Private Sub BeforeClearField(ByVal sender As Object, ByVal args As BeforeClearFieldEventArgs)
	If args.HasMappedFieldInDataSource Then
		'To check whether the mapped field has null value
		If args.FieldValue Is Nothing OrElse args.FieldValue = DBNull.Value Then
			'Gets the unmnerged field name
			Dim unmergedFieldName As String = args.FieldName
			Dim ownerGroup As String = args.GroupName
			'Sets error message for unmerged fields
			args.FieldValue = "Error! The value of MergeField " & unmergedFieldName & " of owner group " & ownerGroup & " is defined as Null in the data source."
		Else
			'If field value is empty, you can set whether the unmerged merge field can be clear or not
			args.ClearField = True
	End If
	Else
		Dim unmergedFieldName As String = args.FieldName
		'Sets error message for unmerged fields, which is not found in data source
		args.FieldValue = "Error! The value of MergeField " & unmergedFieldName & " is not found in the data source."
	End If
End Sub
{% endhighlight %}

{% highlight UWP %}
//DocIO supports performing mail merge in BeforeClearField Event in Windows Forms, WPF, ASP.NET, ASP.NET MVC, ASP.NET Core and Xamarin platforms alone.
{% endhighlight %}

{% highlight ASP.NET CORE %}
private void BeforeClearFieldEvent (object sender, BeforeClearFieldEventArgs args)
{
	if (args.HasMappedFieldInDataSource)
	{
		//To check whether the mapped field has null value
		if (args.FieldValue == null || args.FieldValue == DBNull.Value)
		{
			//Gets the unmnerged field name.
			string unmergedFieldName = args.FieldName;
			string ownerGroup = args.GroupName;
			//Sets error message for unmerged fields.
			args.FieldValue = "Error! The value of MergeField " + unmergedFieldName + " of owner group " + ownerGroup + " is defined as Null in the data source.";
		}
		else
			//If field value is empty, you can set whether the unmerged merge field can be clear or not.
			args.ClearField = true;
	}
	else
	{
		string unmergedFieldName = args.FieldName;
		//Sets error message for unmerged fields, which is not found in data source.
		args.FieldValue = "Error! The value of MergeField " + unmergedFieldName + " is not found in the data source.";
	}
}
{% endhighlight %}

{% highlight XAMARIN %}
private void BeforeClearFieldEvent (object sender, BeforeClearFieldEventArgs args)
{
	if (args.HasMappedFieldInDataSource)
	{
		//To check whether the mapped field has null value
		if (args.FieldValue == null || args.FieldValue == DBNull.Value)
		{
			//Gets the unmnerged field name
			string unmergedFieldName = args.FieldName;
			string ownerGroup = args.GroupName;
			//Sets error message for unmerged fields
			args.FieldValue = "Error! The value of MergeField " + unmergedFieldName + " of owner group " + ownerGroup + " is defined as Null in the data source.";
		}
		else
			//If field value is empty, you can set whether the unmerged merge field can be clear or not
			args.ClearField = true;
	}
	else
	{
		string unmergedFieldName = args.FieldName;
		//Sets error message for unmerged fields, which is not found in data source
		args.FieldValue = "Error! The value of MergeField " + unmergedFieldName + " is not found in the data source.";
	}
}
{% endhighlight %}

{% endtabs %} 

The following code example provides supporting methods

{% tabs %} 

{% highlight C# %}
private DataTable GetDataTable()
{
	//Create an instance of DataTable
	DataTable dataTable = new DataTable("Employee");
	//Add columns
	dataTable.Columns.Add("EmployeeId");
	dataTable.Columns.Add("City");
	//Add records
	DataRow row;
	row = dataTable.NewRow();
	row["EmployeeId"] = "1001";
	row["City"] = null;
	dataTable.Rows.Add(row);
	row = dataTable.NewRow();
	row["EmployeeId"] = "1002";
	row["City"] = "";
	dataTable.Rows.Add(row);
	row = dataTable.NewRow();
	row["EmployeeId"] = "1003";
	row["City"] = "London";
	dataTable.Rows.Add(row);
	return dataTable;
}
{% endhighlight %}

{% highlight vb.net %}
Private Function GetDataTable() As DataTable
	'Create an instance of DataTable
	Dim dataTable As DataTable = New DataTable("Employee")
	'Add columns
	dataTable.Columns.Add("EmployeeId")
	dataTable.Columns.Add("City")
	'Add records
	Dim row As DataRow
	row = dataTable.NewRow()
	row("EmployeeId") = "1001"
	row("City") = Nothing
	dataTable.Rows.Add(row)
	row = dataTable.NewRow()
	row("EmployeeId") = "1002"
	row("City") = ""
	dataTable.Rows.Add(row)
	row = dataTable.NewRow()
	row("EmployeeId") = "1003"
	row("City") = "London"
	dataTable.Rows.Add(row)
	Return dataTable
End Function
{% endhighlight %}

{% highlight UWP %}
//DocIO supports performing mail merge in BeforeClearField Event in Windows Forms, WPF, ASP.NET, ASP.NET MVC, ASP.NET Core and Xamarin platforms alone.
{% endhighlight %}

{% highlight ASP.NET CORE %}
private DataTable GetDataTable()
{
	//Create an instance of DataTable
	DataTable dataTable = new DataTable("Employee");
	//Add columns
	dataTable.Columns.Add("EmployeeId");
	dataTable.Columns.Add("City");
	//Add records
	DataRow row;
	row = dataTable.NewRow();
	row["EmployeeId"] = "1001";
	row["City"] = null;
	dataTable.Rows.Add(row);
	row = dataTable.NewRow();
	row["EmployeeId"] = "1002";
	row["City"] = "";
	dataTable.Rows.Add(row);
	row = dataTable.NewRow();
	row["EmployeeId"] = "1003";
	row["City"] = "London";
	dataTable.Rows.Add(row);
	return dataTable;
}
{% endhighlight %} 

{% highlight XAMARIN %}
private DataTable GetDataTable()
{
	//Create an instance of DataTable
	DataTable dataTable = new DataTable("Employee");
	//Add columns
	dataTable.Columns.Add("EmployeeId");
	dataTable.Columns.Add("City");
	//Add records
	DataRow row;
	row = dataTable.NewRow();
	row["EmployeeId"] = "1001";
	row["City"] = null;
	dataTable.Rows.Add(row);
	row = dataTable.NewRow();
	row["EmployeeId"] = "1002";
	row["City"] = "";
	dataTable.Rows.Add(row);
	row = dataTable.NewRow();
	row["EmployeeId"] = "1003";
	row["City"] = "London";
	dataTable.Rows.Add(row);
	return dataTable;
}
{% endhighlight %} 
{% endtabs %}

## BeforeClearGroupField Event

The following code example shows how to use the BeforeClearGroupField event during Mail merge process.

{% tabs %}  

{% highlight C# %}
//Opens the template document 
WordDocument document = new WordDocument(@"Sample.docx");
//Sets “ClearFields” to true to remove empty mail merge fields from document
document.MailMerge.ClearFields = false;
//Uses the mail merge event to clear the unmerged group field while perform mail merge execution
document.MailMerge.BeforeClearGroupField += new BeforeClearGroupFieldEventHandler(BeforeClearFields);
//Gets the employee details as “IEnumerable” collection
List<Employees> employeeList = GetEmployees();
//Creates an instance of “MailMergeDataTable” by specifying mail merge group name and “IEnumerable” collection
MailMergeDataTable dataTable = new MailMergeDataTable("Employees", employeeList);
//Performs Mail merge
document.MailMerge.ExecuteNestedGroup(dataTable);
//Saves and closes the WordDocument instance
document.Save("Sample.docx");
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Opens the template document 
Dim document As WordDocument = New WordDocument("Sample.docx")
'Sets “ClearFields” to true to remove empty mail merge fields from document
document.MailMerge.ClearFields = False
'Uses the mail merge event to clear the unmerged field while perform mail merge execution
AddHandler document.MailMerge.BeforeClearGroupField, AddressOf BeforeClearFields
'Gets the employee details as “IEnumerable” collection
Dim employeeList As List(Of Employees) = GetEmployees()
'Creates an instance of MailMergeDataTableby specifying mail merge group name and “IEnumerable” collection
Dim dataTable As MailMergeDataTable = New MailMergeDataTable("Employees", employeeList)
'Performs Mail merge
document.MailMerge.ExecuteNestedGroup(dataTable)
'Saves and closes the WordDocument instance
document.Save("Sample.docx")
document.Close()
{% endhighlight %}

{% highlight UWP %}
//Creates an instance of a WordDocument
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
WordDocument document = new WordDocument();
document.Open(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Docx);
//Sets “ClearFields” to true to remove empty mail merge fields from document
document.MailMerge.ClearFields = false;
//Uses the mail merge event to clear the unmerged group field while perform mail merge execution
document.MailMerge.BeforeClearGroupField += new BeforeClearGroupFieldEventHandler(BeforeClearFields);
//Gets the employee details as “IEnumerable” collection
List<Employees> employeeList = GetEmployees();
//Creates an instance of “MailMergeDataTable” by specifying mail merge group name and “IEnumerable” collection
MailMergeDataTable dataTable = new MailMergeDataTable("Employees", employeeList);
//Performs Mail merge
document.MailMerge.ExecuteNestedGroup(dataTable);
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word file in local machine
Save(stream, "Sample.docx");
document.Close();
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp 
{% endhighlight %}

{% highlight ASP.NET CORE %}
//Opens the template document
FileStream fileStreamPath = new FileStream(@"Sample.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);
//Sets “ClearFields” to true to remove empty mail merge fields from document
document.MailMerge.ClearFields = false;
//Uses the mail merge event to clear the unmerged group field while perform mail merge execution
document.MailMerge.BeforeClearGroupField += new BeforeClearGroupFieldEventHandler(BeforeClearFields);
//Gets the employee details as “IEnumerable” collection
List<Employees> employeeList = GetEmployees();
//Creates an instance of “MailMergeDataTable” by specifying mail merge group name and “IEnumerable” collection
MailMergeDataTable dataTable = new MailMergeDataTable("Employees", employeeList);
//Performs Mail merge
document.MailMerge.ExecuteNestedGroup(dataTable);
//Saves the Word document to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Sample.docx");
{% endhighlight %}

{% highlight XAMARIN %}
//Opens the template document
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Docx);
//Sets “ClearFields” to true to remove empty mail merge fields from document
document.MailMerge.ClearFields = false;
//Uses the mail merge event to clear the unmerged group field while perform mail merge execution
document.MailMerge.BeforeClearGroupField += new BeforeClearGroupFieldEventHandler(BeforeClearFields);
//Gets the employee details as “IEnumerable” collection
List<Employees> employeeList = GetEmployees();
//Creates an instance of “MailMergeDataTable” by specifying mail merge group name and “IEnumerable” collection
MailMergeDataTable dataTable = new MailMergeDataTable("Employees", employeeList);
//Performs Mail merge
document.MailMerge.ExecuteNestedGroup(dataTable);
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.docx", "application/msword", stream);
//Closes the document 
document.Close();
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin
{% endhighlight %}

{% endtabs %}

The following code example shows how to bind the data to unmerged group fields during Mail merge process by using BeforeClearGroupFieldEventHandler.

{% tabs %}  

{% highlight C# %}
private static void BeforeClearFields(object sender, BeforeClearGroupFieldEventArgs args)
{
	if (!args.HasMappedGroupInDataSource)
	{
		//Gets the Current unmerged group name from the event argument
		string[] groupName = args.GroupName.Split(':');
		if (groupName[groupName.Length - 1] == "Orders")
		{
			//Gets the field names in the group
			string[] fields = args.FieldNames;
			List<OrderDetails> orderList = GetOrders();
			//Binds the data to the unmerged fields in group as alternative values
			args.AlternateValues = orderList;
		}
		else
			//If group value is empty, you can set whether the unmerged merge group field can be clear or not
			args.ClearGroup = true;
	}
}
{% endhighlight %}

{% highlight vb.net %}
Private Sub BeforeClearFields(ByVal sender As Object, ByVal args As BeforeClearGroupFieldEventArgs)
	If Not args.HasMappedGroupInDataSource Then
		‘Gets the Current unmerged group name from the event argument
		Dim groupName As String() = args.GroupName.Split(":"c)
		If groupName(groupName.Length - 1) = "Orders" Then
			'Gets the field names in the group
			Dim fields As String() = args.FieldNames
			Dim orderList As List(Of OrderDetails) = GetOrders()
			‘Binds the data to the unmerged fields in group as alternative values
			args.AlternateValues = orderList
		Else
			‘If group value is empty, you can set whether the unmerged merge group field can be clear or not
			args.ClearGroup = True
		End If
	End If
End Sub
{% endhighlight %}

{% highlight UWP %}
private static void BeforeClearFields(object sender, BeforeClearGroupFieldEventArgs args)
{
	if (!args.HasMappedGroupInDataSource)
	{
		//Gets the Current unmerged group name from the event argument
		string[] groupName = args.GroupName.Split(':');
		if (groupName[groupName.Length - 1] == "Orders")
		{
			string[] fields = args.FieldNames;
			List<OrderDetails> orderList = GetOrders();
			//Binds the data to the unmerged fields in group as alternative values
			args.AlternateValues = orderList;
		}
		else
			//If group value is empty, you can set whether the unmerged merge group field can be clear or not.
			args.ClearGroup = true;
	}
}
{% endhighlight %}

{% highlight ASP.NET CORE %}
private static void BeforeClearFields(object sender, BeforeClearGroupFieldEventArgs args)
{
	if (!args.HasMappedGroupInDataSource)
	{
		//Gets the Current unmerged group name from the event argument
		string[] groupName = args.GroupName.Split(':');
		if (groupName[groupName.Length - 1] == "Orders")
		{
			string[] fields = args.FieldNames;
			List<OrderDetails> orderList = GetOrders();
			//Binds the data to the unmerged fields in group as alternative values
			args.AlternateValues = orderList;
		}
		else
			//If group value is empty, you can set whether the unmerged merge group field can be clear or not.
			args.ClearGroup = true;
	}
}
{% endhighlight %}

{% highlight XAMARIN %}
private static void BeforeClearFields(object sender, BeforeClearGroupFieldEventArgs args)
{
	if (!args.HasMappedGroupInDataSource)
	{
		//Gets the Current unmerged group name from the event argument
		string[] groupName = args.GroupName.Split(':');
		if (groupName[groupName.Length - 1] == "Orders")
		{
			string[] fields = args.FieldNames;
			List<OrderDetails> orderList = GetOrders();
			//Binds the data to the unmerged fields in group as alternative values
			args.AlternateValues = orderList;
		}
		else
			//If group value is empty, you can set whether the unmerged merge group field can be clear or not.
			args.ClearGroup = true;
	}
}
{% endhighlight %}

{% endtabs %} 

The following code example provides supporting methods

{% tabs %} 

{% highlight C# %}
//Gets order list
private static List<OrderDetails> GetOrders()
{
	List<OrderDetails> orders = new List<OrderDetails>();
	orders.Add(new OrderDetails("10952", new DateTime(2015, 2, 5), new DateTime(2015, 2, 12), new DateTime(2015, 2, 21)));
	return orders;
}

//Gets employee list
public static List<Employees> GetEmployees()
{
	List<OrderDetails> orders = new List<OrderDetails>();
	orders.Add(new OrderDetails("10835", new DateTime(2015, 1, 5), new DateTime(2015, 1, 12), new DateTime(2015, 1, 21)));
	List<CustomerDetails> customerDetails = new List<CustomerDetails>();
	customerDetails.Add(new CustomerDetails("Maria Anders", "Maria Anders", "Berlin", "Germany", orders));
	customerDetails.Add(new CustomerDetails("Andy", "Bernard", "Berlin", "Germany", null));
	List<Employees> employees = new List<Employees>();
	employees.Add(new Employees("Nancy", "Smith", "1", "505 - 20th Ave. E. Apt. 2A,", "Seattle", "USA", customerDetails));
	return employees;
}

public class Employees
{
	public string FirstName { get; set; }
	public string LastName { get; set; }
	public string EmployeeID { get; set; }
	public string Address { get; set; }
	public string City { get; set; }
	public string Country { get; set; }
	public List<CustomerDetails> Customers { get; set; }
	
	public Employees(string firstName, string lastName, string employeeId, string address, string city, string country, List<CustomerDetails> customers)
	{
		FirstName = firstName;
		LastName = lastName;
		Address = address;
		EmployeeID = employeeId;
		City = city;
		Country = country;
		Customers = customers;
	}
}

public class CustomerDetails
{
	public string ContactName { get; set; }
	public string CompanyName { get; set; }
	public string City { get; set; }
	public string Country { get; set; }
	public List<OrderDetails> Orders { get; set; }

	public CustomerDetails(string contactName, string companyName, string city, string country, List<OrderDetails> orders)
	{
		ContactName = contactName;
		CompanyName = companyName;
		City = city;
		Country = country;
		Orders = orders;
	}
}

public class OrderDetails
{
	public string OrderID { get; set; }
	public DateTime OrderDate { get; set; }
	public DateTime ShippedDate { get; set; }
	public DateTime RequiredDate { get; set; }

	public OrderDetails(string orderId, DateTime orderDate, DateTime shippedDate, DateTime requiredDate)
	{
		OrderID = orderId;
		OrderDate = orderDate;
		ShippedDate = shippedDate;
		RequiredDate = requiredDate;
	}
}
{% endhighlight %}

{% highlight vb.net %}
'Gets orders list
Private Shared Function GetOrders() As List(Of OrderDetails)
	Dim orders As List(Of OrderDetails) = New List(Of OrderDetails)()
	orders.Add(New OrderDetails("10835", New DateTime(2015, 1, 5), New DateTime(2015, 1, 12), New DateTime(2015, 1, 21)))
	Return orders
End Function

'Gets employee list
Public Shared Function GetEmployees() As List(Of Employees)
	Dim orders As List(Of OrderDetails) = New List(Of OrderDetails)()
	orders.Add(New OrderDetails("10835", New DateTime(2015, 1, 5), New DateTime(2015, 1, 12), New DateTime(2015, 1, 21)))
	Dim customerDetails As List(Of CustomerDetails) = New List(Of CustomerDetails)()
	customerDetails.Add(New CustomerDetails("Maria Anders", "Maria Anders", "Berlin", "Germany", orders))
	customerDetails.Add(New CustomerDetails("Andy", "Bernard", "Berlin", "Germany", Nothing))
	Dim employees As List(Of Employees) = New List(Of Employees)()
	employees.Add(New Employees("Nancy", "Smith", "1", "505 - 20th Ave. E. Apt. 2A,", "Seattle", "USA", customerDetails))
	Return employees
End Function

Public Class Employees
	Public Property FirstName As String
	Public Property LastName As String
	Public Property EmployeeID As String
	Public Property Address As String
	Public Property City As String
	Public Property Country As String
	Public Property Customers As List(Of CustomerDetails)

	Public Sub New(ByVal firstName As String, ByVal lastName As String, ByVal employeeId As String, ByVal address As String, ByVal city As String, ByVal country As String, ByVal customers As List(Of CustomerDetails))
		Me.FirstName = firstName
		Me.LastName = lastName
		Me.Address = address
		Me.EmployeeID = employeeId
		Me.City = city
		Me.Country = country
		Me.Customers = customers
	End Sub
End Class

Public Class CustomerDetails
	Public Property ContactName As String
	Public Property CompanyName As String
	Public Property City As String
	Public Property Country As String
	Public Property Orders As List(Of OrderDetails)

	Public Sub New(ByVal contactName As String, ByVal companyName As String, ByVal city As String, ByVal country As String, ByVal orders As List(Of OrderDetails))
		Me.ContactName = contactName
		Me.CompanyName = companyName
		Me.City = city
		Me.Country = country
		Me.Orders = orders
	End Sub
End Class

Public Class OrderDetails
	Public Property OrderID As String
	Public Property OrderDate As DateTime
	Public Property ShippedDate As DateTime
	Public Property RequiredDate As DateTime
	
	Public Sub New(ByVal orderId As String, ByVal orderDate As DateTime, ByVal shippedDate As DateTime, ByVal requiredDate As DateTime)
		Me.OrderID = orderId
		Me.OrderDate = orderDate
		Me.ShippedDate = shippedDate
		Me.RequiredDate = requiredDate
	End Sub
End Class
{% endhighlight %}

{% highlight UWP %}
//Gets order list
private static List<OrderDetails> GetOrders()
{
	List<OrderDetails> orders = new List<OrderDetails>();
	orders.Add(new OrderDetails("10952", new DateTime(2015, 2, 5), new DateTime(2015, 2, 12), new DateTime(2015, 2, 21)));
	return orders;
}

//Gets employee list
public static List<Employees> GetEmployees()
{
	List<OrderDetails> orders = new List<OrderDetails>();
	orders.Add(new OrderDetails("10835", new DateTime(2015, 1, 5), new DateTime(2015, 1, 12), new DateTime(2015, 1, 21)));
	List<CustomerDetails> customerDetails = new List<CustomerDetails>();
	customerDetails.Add(new CustomerDetails("Maria Anders", "Maria Anders", "Berlin", "Germany", orders));
	customerDetails.Add(new CustomerDetails("Andy", "Bernard", "Berlin", "Germany", null));
	List<Employees> employees = new List<Employees>();
	employees.Add(new Employees("Nancy", "Smith", "1", "505 - 20th Ave. E. Apt. 2A,", "Seattle", "USA", customerDetails));
	return employees;
}

public class Employees
{
	public string FirstName { get; set; }
	public string LastName { get; set; }
	public string EmployeeID { get; set; }
	public string Address { get; set; }
	public string City { get; set; }
	public string Country { get; set; }
	public List<CustomerDetails> Customers { get; set; }
	
	public Employees(string firstName, string lastName, string employeeId, string address, string city, string country, List<CustomerDetails> customers)
	{
		FirstName = firstName;
		LastName = lastName;
		Address = address;
		EmployeeID = employeeId;
		City = city;
		Country = country;
		Customers = customers;
	}
}

public class CustomerDetails
{
	public string ContactName { get; set; }
	public string CompanyName { get; set; }
	public string City { get; set; }
	public string Country { get; set; }
	public List<OrderDetails> Orders { get; set; }

	public CustomerDetails(string contactName, string companyName, string city, string country, List<OrderDetails> orders)
	{
		ContactName = contactName;
		CompanyName = companyName;
		City = city;
		Country = country;
		Orders = orders;
	}
}

public class OrderDetails
{
	public string OrderID { get; set; }
	public DateTime OrderDate { get; set; }
	public DateTime ShippedDate { get; set; }
	public DateTime RequiredDate { get; set; }

	public OrderDetails(string orderId, DateTime orderDate, DateTime shippedDate, DateTime requiredDate)
	{
		OrderID = orderId;
		OrderDate = orderDate;
		ShippedDate = shippedDate;
		RequiredDate = requiredDate;
	}
}
{% endhighlight %}

{% highlight ASP.NET CORE %}
//Gets order list
private static List<OrderDetails> GetOrders()
{
	List<OrderDetails> orders = new List<OrderDetails>();
	orders.Add(new OrderDetails("10952", new DateTime(2015, 2, 5), new DateTime(2015, 2, 12), new DateTime(2015, 2, 21)));
	return orders;
}

//Gets employee list
public static List<Employees> GetEmployees()
{
	List<OrderDetails> orders = new List<OrderDetails>();
	orders.Add(new OrderDetails("10835", new DateTime(2015, 1, 5), new DateTime(2015, 1, 12), new DateTime(2015, 1, 21)));
	List<CustomerDetails> customerDetails = new List<CustomerDetails>();
	customerDetails.Add(new CustomerDetails("Maria Anders", "Maria Anders", "Berlin", "Germany", orders));
	customerDetails.Add(new CustomerDetails("Andy", "Bernard", "Berlin", "Germany", null));
	List<Employees> employees = new List<Employees>();
	employees.Add(new Employees("Nancy", "Smith", "1", "505 - 20th Ave. E. Apt. 2A,", "Seattle", "USA", customerDetails));
	return employees;
}

public class Employees
{
	public string FirstName { get; set; }
	public string LastName { get; set; }
	public string EmployeeID { get; set; }
	public string Address { get; set; }
	public string City { get; set; }
	public string Country { get; set; }
	public List<CustomerDetails> Customers { get; set; }

	public Employees(string firstName, string lastName, string employeeId, string address, string city, string country, List<CustomerDetails> customers)
	{
		FirstName = firstName;
		LastName = lastName;
		Address = address;
		EmployeeID = employeeId;
		City = city;
		Country = country;
		Customers = customers;
	}
}

public class CustomerDetails
{
	public string ContactName { get; set; }
	public string CompanyName { get; set; }
	public string City { get; set; }
	public string Country { get; set; }
	public List<OrderDetails> Orders { get; set; }

	public CustomerDetails(string contactName, string companyName, string city, string country, List<OrderDetails> orders)
	{
		ContactName = contactName;
		CompanyName = companyName;
		City = city;
		Country = country;
		Orders = orders;
	}
}

public class OrderDetails
{
	public string OrderID { get; set; }
	public DateTime OrderDate { get; set; }
	public DateTime ShippedDate { get; set; }
	public DateTime RequiredDate { get; set; }
	
	public OrderDetails(string orderId, DateTime orderDate, DateTime shippedDate, DateTime requiredDate)
	{
		OrderID = orderId;
		OrderDate = orderDate;
		ShippedDate = shippedDate;
		RequiredDate = requiredDate;
	}
}
{% endhighlight %}

{% highlight XAMARIN %}
//Gets order list
private static List<OrderDetails> GetOrders()
{
	List<OrderDetails> orders = new List<OrderDetails>();
	orders.Add(new OrderDetails("10952", new DateTime(2015, 2, 5), new DateTime(2015, 2, 12), new DateTime(2015, 2, 21)));
	return orders;
}

//Gets employee list
public static List<Employees> GetEmployees()
{
	List<OrderDetails> orders = new List<OrderDetails>();
	orders.Add(new OrderDetails("10835", new DateTime(2015, 1, 5), new DateTime(2015, 1, 12), new DateTime(2015, 1, 21)));
	List<CustomerDetails> customerDetails = new List<CustomerDetails>();
	customerDetails.Add(new CustomerDetails("Maria Anders", "Maria Anders", "Berlin", "Germany", orders));
	customerDetails.Add(new CustomerDetails("Andy", "Bernard", "Berlin", "Germany", null));
	List<Employees> employees = new List<Employees>();
	employees.Add(new Employees("Nancy", "Smith", "1", "505 - 20th Ave. E. Apt. 2A,", "Seattle", "USA", customerDetails));
	return employees;
}

public class Employees
{
	public string FirstName { get; set; }
	public string LastName { get; set; }
	public string EmployeeID { get; set; }
	public string Address { get; set; }
	public string City { get; set; }
	public string Country { get; set; }
	public List<CustomerDetails> Customers { get; set; }
	
	public Employees(string firstName, string lastName, string employeeId, string address, string city, string country, List<CustomerDetails> customers)
	{
		FirstName = firstName;
		LastName = lastName;
		Address = address;
		EmployeeID = employeeId;
		City = city;
		Country = country;
		Customers = customers;
	}
}

public class CustomerDetails
{
	public string ContactName { get; set; }
	public string CompanyName { get; set; }
	public string City { get; set; }
	public string Country { get; set; }
	public List<OrderDetails> Orders { get; set; }

	public CustomerDetails(string contactName, string companyName, string city, string country, List<OrderDetails> orders)
	{
		ContactName = contactName;
		CompanyName = companyName;
		City = city;
		Country = country;
		Orders = orders;
	}
}

public class OrderDetails
{
	public string OrderID { get; set; }
	public DateTime OrderDate { get; set; }
	public DateTime ShippedDate { get; set; }
	public DateTime RequiredDate { get; set; }

	public OrderDetails(string orderId, DateTime orderDate, DateTime shippedDate, DateTime requiredDate)
	{
		OrderID = orderId;
		OrderDate = orderDate;
		ShippedDate = shippedDate;
		RequiredDate = requiredDate;
	}
}
{% endhighlight %}

{% endtabs %} 