---
title: Mail merge options | Word library (DocIO) | Syncfusion
description: This section illustrates the mail merge options used to customize field mapping, remove unmerged fields, unmerged mail merge groups, empty paragraphs and more.
platform: file-formats
control: DocIO
documentation: UG
---

# Mail merge options

The `MailMerge` class allows you to customize the Mail merge process with the following options.

## Field Mapping

The `MailMerge` class can automatically maps the merge field names with data source column names during Mail merge process. You can also customize the field mapping when the merge field names in the template document varies with the column names in the data source by using `MappedFields` collection.

The following code example shows how to add mapping when a merge field name in a document and column name in data source have different names.

{% tabs %}  

{% highlight C# %}
//Opens the template document 
WordDocument document = new WordDocument("Template.docx");
//Creates data source
string[] fieldNames = new string[] { "Employee_Id_InDataSource", "Name_InDataSource",
    "Phone_InDataSource", "City_InDataSource" };
string[] fieldValues = new string[] { "101", "John", "+122-2000466", "Houston" };
//Mapping the required merge field names with data source column names
document.MailMerge.MappedFields.Add("Employee_Id_InDocument", "Employee_Id_InDataSource");
document.MailMerge.MappedFields.Add("Name_InDocument", "Name_InDataSource");
document.MailMerge.MappedFields.Add("Phone_InDocument", "Phone_InDataSource");
document.MailMerge.MappedFields.Add("City_InDocument", "City_InDataSource");
//Performs the mail merge
document.MailMerge.Execute(fieldNames, fieldValues);
//Saves and closes the Word document instance
document.Save("Sample.docx");
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Opens the template document 
Dim document As New WordDocument("Template.docx")
'Creates data source
Dim fieldNames As String() = New String() {"Employee_Id_InDataSource", "Name_InDataSource", 
    "Phone_InDataSource", "City_InDataSource"}
Dim fieldValues As String() = New String() {"101", "John", "+122-2000466", "Houston"}
'Mapping the required merge field names with data source column names
document.MailMerge.MappedFields.Add("Employee_Id_InDocument", "Employee_Id_InDataSource")
document.MailMerge.MappedFields.Add("Name_InDocument", "Name_InDataSource")
document.MailMerge.MappedFields.Add("Phone_InDocument", "Phone_InDataSource")
document.MailMerge.MappedFields.Add("City_InDocument", "City_InDataSource")
'Performs the mail merge
document.MailMerge.Execute(fieldNames, fieldValues)
'Saves and closes the Word document instance
document.Save("Sample.docx")
document.Close()
{% endhighlight %}

{% highlight UWP %}
private async void OnButtonClicked(object sender, RoutedEventArgs e)
{
	//Creates an instance of a WordDocument
	Assembly assembly = typeof(App).GetTypeInfo().Assembly;
	WordDocument document = new WordDocument();
	document.Open(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Docx);
	//Creates data source
	string[] fieldNames = new string[] { "Employee_Id_InDataSource", "Name_InDataSource", 
	    "Phone_InDataSource", "City_InDataSource" };
	string[] fieldValues = new string[] { "101", "John", "+122-2000466", "Houston" };
	//Mapping the required merge field names with data source column names
	document.MailMerge.MappedFields.Add("Employee_Id_InDocument", "Employee_Id_InDataSource");
	document.MailMerge.MappedFields.Add("Name_InDocument", "Name_InDataSource");
	document.MailMerge.MappedFields.Add("Phone_InDocument", "Phone_InDataSource");
	document.MailMerge.MappedFields.Add("City_InDocument", "City_InDataSource");
	//Performs the mail merge
	document.MailMerge.Execute(fieldNames, fieldValues);
	//Saves the Word file to MemoryStream
	MemoryStream stream = new MemoryStream();
	await document.SaveAsync(stream, FormatType.Docx);
	//Saves the stream as Word file in local machine
	Save(stream, "Sample.docx");
	document.Close();
}

//Saves the Word document
async void Save(MemoryStream streams, string filename)
{
	streams.Position = 0;
	StorageFile stFile;
	if(!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
	{
		FileSavePicker savePicker = new FileSavePicker();
		savePicker.DefaultFileExtension = ".docx";
		savePicker.SuggestedFileName = filename;
		savePicker.FileTypeChoices.Add("Word Documents", new List<string>() { ".docx" });
		stFile = await savePicker.PickSaveFileAsync();
	}
	else
	{
		StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
		stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
	}
	if (stFile != null)
	{
		using (IRandomAccessStream zipStream = await stFile.OpenAsync(FileAccessMode.ReadWrite))
		{
			//Write compressed data from memory to file
			using (Stream outstream = zipStream.AsStreamForWrite())
			{
				byte[] buffer = streams.ToArray();
				outstream.Write(buffer, 0, buffer.Length);
				outstream.Flush();
			}
		}
	}
	//Launch the saved Word file
	await Windows.System.Launcher.LaunchFileAsync(stFile);
}
{% endhighlight %}

{% highlight ASP.NET CORE %}
//Opens the template document. 
FileStream fileStreamPath = new FileStream("Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);
//Creates data source
string[] fieldNames = new string[] { "Employee_Id_InDataSource", "Name_InDataSource", 
    "Phone_InDataSource", "City_InDataSource" };
string[] fieldValues = new string[] { "101", "John", "+122-2000466", "Houston" };
//Mapping the required merge field names with data source column names
document.MailMerge.MappedFields.Add("Employee_Id_InDocument", "Employee_Id_InDataSource");
document.MailMerge.MappedFields.Add("Name_InDocument", "Name_InDataSource");
document.MailMerge.MappedFields.Add("Phone_InDocument", "Phone_InDataSource");
document.MailMerge.MappedFields.Add("City_InDocument", "City_InDataSource");
//Performs the mail merge
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
//Creates data source
string[] fieldNames = new string[] { "Employee_Id_InDataSource", "Name_InDataSource", 
    "Phone_InDataSource", "City_InDataSource" };
string[] fieldValues = new string[] { "101", "John", "+122-2000466", "Houston" };
//Mapping the required merge field names with data source column names
document.MailMerge.MappedFields.Add("Employee_Id_InDocument", "Employee_Id_InDataSource");
document.MailMerge.MappedFields.Add("Name_InDocument", "Name_InDataSource");
document.MailMerge.MappedFields.Add("Phone_InDocument", "Phone_InDataSource");
document.MailMerge.MappedFields.Add("City_InDocument", "City_InDataSource");
//Performs the mail merge
document.MailMerge.Execute(fieldNames, fieldValues);
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.docx", "application/msword", stream);
//Closes the document 
document.Close();
{% endhighlight %}

{% endtabs %} 

## Retrieve the merge field names

The following code example shows how to retrieve the merge field names in the Word document.

{% tabs %}  

{% highlight C# %}
//Gets the merge field names from the document
string[] fieldNames = document.MailMerge.GetMergeFieldNames();
{% endhighlight %}

{% highlight vb.net %}
'Gets the merge field names from the document
Dim fieldNames As String() = document.MailMerge.GetMergeFieldNames()
{% endhighlight %}

{% highlight UWP %}
//Gets the merge field names from the document.
string[] fieldNames = document.MailMerge.GetMergeFieldNames();
{% endhighlight %} 

{% highlight ASP.NET CORE %}
//Gets the merge field names from the document.
string[] fieldNames = document.MailMerge.GetMergeFieldNames();
{% endhighlight %} 

{% highlight XAMARIN %}
//Gets the merge field names from the document.
string[] fieldNames = document.MailMerge.GetMergeFieldNames();
{% endhighlight %} 

{% endtabs %}  
 
The following code example shows how to retrieve the merge field group names in the Word document

{% tabs %}  

{% highlight C# %}
//Gets the merge field group names from the document
string[] groupNames = document.MailMerge.GetMergeGroupNames();
{% endhighlight %}

{% highlight vb.net %}
'Gets the merge field group names from the document
Dim groupNames As String() = document.MailMerge.GetMergeGroupNames()
{% endhighlight %}

{% highlight UWP %}
//Gets the merge field group names from the document.
string[] groupNames = document.MailMerge.GetMergeGroupNames();
{% endhighlight %}

{% highlight ASP.NET CORE %}
//Gets the merge field group names from the document.
string[] groupNames = document.MailMerge.GetMergeGroupNames();
{% endhighlight %}

{% highlight XAMARIN %}
//Gets the merge field group names from the document.
string[] groupNames = document.MailMerge.GetMergeGroupNames();
{% endhighlight %}

{% endtabs %}  

The following code example shows how to retrieve the merge field names for a specific group in the Word document

{% tabs %}  

{% highlight C# %}
//Gets the fields from the specified groups 
string[] fieldNames = document.MailMerge.GetMergeFieldNames(groupName);
{% endhighlight %}

{% highlight vb.net %}
'Gets the fields from the specified groups 
Dim fieldNames As String() = document.MailMerge.GetMergeFieldNames(groupName)
{% endhighlight %}

{% highlight UWP %}
//Gets the fields from the specified groups. 
string[] fieldNames = document.MailMerge.GetMergeFieldNames(groupName);
{% endhighlight %}

{% highlight ASP.NET CORE %}
//Gets the fields from the specified groups. 
string[] fieldNames = document.MailMerge.GetMergeFieldNames(groupName);
{% endhighlight %}

{% highlight XAMARIN %}
//Gets the fields from the specified groups. 
string[] fieldNames = document.MailMerge.GetMergeFieldNames(groupName);
{% endhighlight %}

{% endtabs %}  

## Remove empty paragraphs

The following code example shows how to remove the empty paragraphs when the paragraph has a merge field item without any data during Mail merge process.

{% tabs %} 

{% highlight C# %}
//Opens the template document 
WordDocument document = new WordDocument("Template.docx");
//Removes paragraph that contains only empty fields 
document.MailMerge.RemoveEmptyParagraphs = true;
string[] fieldNames = new string[] { "EmployeeId", "Phone", "City" };
string[] fieldValues = new string[] { "1001", "+91-9999999999", "London" };
//Performs the mail merge
document.MailMerge.Execute(fieldNames, fieldValues);
//Saves and closes the Word document instance
document.Save("Sample.docx");
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Opens the template document 
Dim document As New WordDocument("Template.docx")
'Removes paragraph that contains only empty fields 
document.MailMerge.RemoveEmptyParagraphs = True
Dim fieldNames As String() = New String() {"EmployeeId", "Phone", "City"}
Dim fieldValues As String() = New String() {"1001", "+91-9999999999", "London"}
'Performs the mail merge
document.MailMerge.Execute(fieldNames, fieldValues)
'Saves and closes the Word document instance
document.Save("Sample.docx")
document.Close()
{% endhighlight %}

{% highlight UWP %}
private async void OnButtonClicked(object sender, RoutedEventArgs e)
{
	//Creates an instance of a WordDocument
	Assembly assembly = typeof(App).GetTypeInfo().Assembly;
	WordDocument document = new WordDocument();
	document.Open(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Docx);
	//Removes paragraph that contains only empty fields 
	document.MailMerge.RemoveEmptyParagraphs = true;
	string[] fieldNames = new string[] { "EmployeeId", "Phone", "City" };
	string[] fieldValues = new string[] { "1001", "+91-9999999999", "London" };
	//Performs the mail merge
	document.MailMerge.Execute(fieldNames, fieldValues);
	//Saves the Word file to MemoryStream
	MemoryStream stream = new MemoryStream();
	await document.SaveAsync(stream, FormatType.Docx);
	//Saves the stream as Word file in local machine
	Save(stream, "Sample.docx");
	document.Close();
}

//Saves the Word document
async void Save(MemoryStream streams, string filename)
{
	streams.Position = 0;
	StorageFile stFile;
	if(!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
	{
		FileSavePicker savePicker = new FileSavePicker();
		savePicker.DefaultFileExtension = ".docx";
		savePicker.SuggestedFileName = filename;
		savePicker.FileTypeChoices.Add("Word Documents", new List<string>() { ".docx" });
		stFile = await savePicker.PickSaveFileAsync();
	}
	else
	{
		StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
		stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
	}
	if (stFile != null)
	{
		using (IRandomAccessStream zipStream = await stFile.OpenAsync(FileAccessMode.ReadWrite))
		{
			//Write compressed data from memory to file
			using (Stream outstream = zipStream.AsStreamForWrite())
			{
				byte[] buffer = streams.ToArray();
				outstream.Write(buffer, 0, buffer.Length);
				outstream.Flush();
			}
		}
	}
	//Launch the saved Word file
	await Windows.System.Launcher.LaunchFileAsync(stFile);
}
{% endhighlight %}

{% highlight ASP.NET CORE %}
//Opens the template document. 
FileStream fileStreamPath = new FileStream("Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);
//Removes paragraph that contains only empty fields. 
document.MailMerge.RemoveEmptyParagraphs = true;
string[] fieldNames = new string[] { "EmployeeId", "Phone", "City" };
string[] fieldValues = new string[] { "1001", "+91-9999999999", "London" };
//Performs the mail merge.
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
//Removes paragraph that contains only empty fields 
document.MailMerge.RemoveEmptyParagraphs = true;
string[] fieldNames = new string[] { "EmployeeId", "Phone", "City" };
string[] fieldValues = new string[] { "1001", "+91-9999999999", "London" };
//Performs the mail merge
document.MailMerge.Execute(fieldNames, fieldValues);
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.docx", "application/msword", stream);
//Closes the document 
document.Close();
{% endhighlight %}

{% endtabs %}  

N>If any white space or line break exists in the merge field's parent paragraph, then it will not be considered as empty paragraph and not removed during mail merge process.

## Remove empty merge fields

Essential DocIO removes or keeps the unmerged merge fields in the output document based on the ClearFields property on each mail merge execution.

When a merge field is considered as unmerged during mail merge process?

1.The merge field doesn't have mapping field in data source.

2.The merge field has mapping field in data source, but the data is null or string.Empty.

Mail merge operation automatically removes the unmerged merge fields since the default value of ClearFields property is true.

T> 1.Set ClearFields property to false before the mail merge execution statement if your requirement is to keep the unmerged merge fields in the output document.
T> 2.Modify the ClearFields property before each mail merge execution statement while performing multiple mail merge executions if your requirement is to remove the unmerged merge fields in one mail merge execution and keep the unmerged merge fields in another mail merge execution.
T> 3.Order the mail merge executions with the ClearFields property false as first to avoid removal merge fields that are required for next mail merge execution in the same document.

The following code example shows how to keep the unmerged merge fields in the generated Word document.
 
{% tabs %}  

{% highlight c# %}
//Opens the template document 
WordDocument document = new WordDocument("Template.docx");
//Sets “ClearFields” to true to remove empty mail merge fields from document 
document.MailMerge.ClearFields = false;
string[] fieldNames = new string[] { "EmployeeId", "Phone", "City" };
string[] fieldValues = new string[] { "1001", "+91-9999999999", "London" };
//Performs the mail merge
document.MailMerge.Execute(fieldNames, fieldValues);
//Saves and closes the Word document instance
document.Save("Sample.docx");
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Opens the template document 
Dim document As New WordDocument("Template.docx")
'Sets “ClearFields” to true to remove empty mail merge fields from document 
document.MailMerge.ClearFields = False
Dim fieldNames As String() = New String() {"EmployeeId", "Phone", "City"}
Dim fieldValues As String() = New String() {"1001", "+91-9999999999", "London"}
'Performs the mail merge
document.MailMerge.Execute(fieldNames, fieldValues)
'Saves and closes the Word document instance
document.Save("Sample.docx")
document.Close()
{% endhighlight %}

{% highlight UWP %}
private async void OnButtonClicked(object sender, RoutedEventArgs e)
{
	//Creates an instance of a WordDocument
	Assembly assembly = typeof(App).GetTypeInfo().Assembly;
	WordDocument document = new WordDocument();
	document.Open(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Docx);
	//Sets “ClearFields” to true to remove empty mail merge fields from document 
	document.MailMerge.ClearFields = false;
	string[] fieldNames = new string[] { "EmployeeId", "Phone", "City" };
	string[] fieldValues = new string[] { "1001", "+91-9999999999", "London" };
	//Performs the mail merge
	document.MailMerge.Execute(fieldNames, fieldValues);
	//Saves the Word file to MemoryStream
	MemoryStream stream = new MemoryStream();
	await document.SaveAsync(stream, FormatType.Docx);
	//Saves the stream as Word file in local machine
	Save(stream, "Sample.docx");
	document.Close();
}

//Saves the Word document
async void Save(MemoryStream streams, string filename)
{
	streams.Position = 0;
	StorageFile stFile;
	if(!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
	{
		FileSavePicker savePicker = new FileSavePicker();
		savePicker.DefaultFileExtension = ".docx";
		savePicker.SuggestedFileName = filename;
		savePicker.FileTypeChoices.Add("Word Documents", new List<string>() { ".docx" });
		stFile = await savePicker.PickSaveFileAsync();
	}
	else
	{
		StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
		stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
	}
	if (stFile != null)
	{
		using (IRandomAccessStream zipStream = await stFile.OpenAsync(FileAccessMode.ReadWrite))
		{
			//Write compressed data from memory to file
			using (Stream outstream = zipStream.AsStreamForWrite())
			{
				byte[] buffer = streams.ToArray();
				outstream.Write(buffer, 0, buffer.Length);
				outstream.Flush();
			}
		}
	}
	//Launch the saved Word file
	await Windows.System.Launcher.LaunchFileAsync(stFile);
}
{% endhighlight %}

{% highlight ASP.NET CORE %}
//Opens the template document 
FileStream fileStreamPath = new FileStream("Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);
//Sets “ClearFields” to true to remove empty mail merge fields from document 
document.MailMerge.ClearFields = false;
string[] fieldNames = new string[] { "EmployeeId", "Phone", "City" };
string[] fieldValues = new string[] { "1001", "+91-9999999999", "London" };
//Performs the mail merge
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
//Sets “ClearFields” to true to remove empty mail merge fields from document 
document.MailMerge.ClearFields = false;
string[] fieldNames = new string[] { "EmployeeId", "Phone", "City" };
string[] fieldValues = new string[] { "1001", "+91-9999999999", "London" };
//Performs the mail merge
document.MailMerge.Execute(fieldNames, fieldValues);
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.docx", "application/msword", stream);
//Closes the document 
document.Close();
{% endhighlight %}
{% endtabs %} 

## Remove empty group

The following code example shows how to remove groups which contain empty merge fields after executing mail merge in a Word document.

{% tabs %}  

{% highlight C# %}

//Opens the template document 
WordDocument document = new WordDocument(@"Template.docx");
//Gets the employee details as “IEnumerable” collection
List<Employees> employeeList = GetEmployees();
//Creates an instance of “MailMergeDataTable” by specifying mail merge group name and “IEnumerable” collection
MailMergeDataTable dataTable = new MailMergeDataTable("Employees", employeeList);
//Enable the flag to remove empty group which contain empty merge fields
document.MailMerge.RemoveEmptyGroup = true;
//Performs Mail merge
document.MailMerge.ExecuteNestedGroup(dataTable);
//Saves and closes the WordDocument instance
document.Save("Sample.docx");
document.Close();

{% endhighlight %}

{% highlight VB.NET %}

'Opens the template document
Dim document As WordDocument =  New WordDocument("Template.docx")
'Gets the employee details as “IEnumerable” collection
Dim employeeList As List(Of Employees) =  GetEmployees() 
'Creates an instance of “MailMergeDataTable” by specifying mail merge group name and “IEnumerable” collection
Dim dataTable As MailMergeDataTable =  New MailMergeDataTable("Employees",employeeList) 
'Enable the flag to remove empty group which contain empty merge fields
document.MailMerge.RemoveEmptyGroup = True
'Performs Mail merge
document.MailMerge.ExecuteNestedGroup(dataTable)
'Saves and closes the WordDocument instance
document.Save("Sample.docx")
document.Close() 

{% endhighlight %}

{% highlight UWP %}

private async void OnButtonClicked(object sender, RoutedEventArgs e)
{
	//Creates an instance of a WordDocument
	Assembly assembly = typeof(App).GetTypeInfo().Assembly;
	WordDocument document = new WordDocument();
	document.Open(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Docx);
	//Gets the employee details as “IEnumerable” collection
	List<Employees> employeeList = GetEmployees();
	//Creates an instance of “MailMergeDataTable” by specifying mail merge group name and “IEnumerable” collection
	MailMergeDataTable dataTable = new MailMergeDataTable("Employees", employeeList);
	//Enable the flag to remove empty group which contain empty merge fields
	document.MailMerge.RemoveEmptyGroup = true;
	//Performs Mail merge
	document.MailMerge.ExecuteNestedGroup(dataTable);
	//Saves the Word file to MemoryStream
	MemoryStream stream = new MemoryStream();
	await document.SaveAsync(stream, FormatType.Docx);
	//Saves the stream as Word file in local machine
	Save(stream, "Sample.docx");
	document.Close();
}

// Saves the Word document
async void Save(MemoryStream streams, string filename)
{
	streams.Position = 0;
	StorageFile stFile;
	if(!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
	{
		FileSavePicker savePicker = new FileSavePicker();
		savePicker.DefaultFileExtension = ".docx";
		savePicker.SuggestedFileName = filename;
		savePicker.FileTypeChoices.Add("Word Documents", new List<string>() { ".docx" });
		stFile = await savePicker.PickSaveFileAsync();
	}
	else
	{
		StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
		stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
	}
	if (stFile != null)
	{
		using (IRandomAccessStream zipStream = await stFile.OpenAsync(FileAccessMode.ReadWrite))
		{
			// Write compressed data from memory to file
			using (Stream outstream = zipStream.AsStreamForWrite())
			{
				byte[] buffer = streams.ToArray();
				outstream.Write(buffer, 0, buffer.Length);
				outstream.Flush();
			}
		}
	}
	// Launch the saved Word file
	await Windows.System.Launcher.LaunchFileAsync(stFile);
}

{% endhighlight %}

{% highlight ASP.NET CORE %}

//Opens the template document 
FileStream fileStreamPath = new FileStream(@"Data\Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);
//Gets the employee details as “IEnumerable” collection
List<Employees> employeeList = GetEmployees();
//Creates an instance of “MailMergeDataTable” by specifying mail merge group name and “IEnumerable” collection.
MailMergeDataTable dataTable = new MailMergeDataTable("Employees", employeeList);
//Enable the flag to remove empty group which contain empty merge fields
document.MailMerge.RemoveEmptyGroup = true;
//Performs Mail merge
document.MailMerge.ExecuteNestedGroup(dataTable);
MemoryStream stream = new MemoryStream();
//Saves the Word document to MemoryStream
document.Save(stream, FormatType.Docx);
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Sample.docx");

{% endhighlight %}

{% highlight XAMARIN %}

//Opens the template document
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Docx);
//Gets the employee details as “IEnumerable” collection
List<Employees> employeeList = GetEmployees();
//Creates an instance of “MailMergeDataTable” by specifying mail merge group name and “IEnumerable” collection
MailMergeDataTable dataTable = new MailMergeDataTable("Employees", employeeList);
//Enable the flag to remove empty group which contain empty merge fields
document.MailMerge.RemoveEmptyGroup = true;
//Performs Mail merge
document.MailMerge.ExecuteNestedGroup(dataTable);
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.docx", "application/msword", stream);
//Closes the document 
document.Close();

{% endhighlight %}

{% endtabs %}

The following code example provides supporting methods

{% tabs %}  

{% highlight C# %}
  
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

{% highlight VB.NET %}

Public Function GetEmployees() As List(Of Employees)
	Dim orders As List(Of OrderDetails) = New List(Of OrderDetails)
	orders.Add(New OrderDetails("10835", New DateTime(2015, 1, 5), New DateTime(2015, 1, 12), New DateTime(2015, 1, 21)))
	Dim customers As List(Of CustomerDetails) = New List(Of CustomerDetails) 
	customers.Add(New CustomerDetails("Maria Anders", "Maria Anders", "Berlin", "Germany", orders))
	customers.Add(New CustomerDetails("Andy", "Bernard", "Berlin", "Germany", Nothing))
	Dim employees As List(Of Employees) = New List(Of Employees) 
	employees.Add(New Employees("Nancy", "Smith", "1", "505 - 20th Ave. E. Apt. 2A,", "Seattle", "USA", customers))
	Return employees
End Function
 
Public Class Employees
	Public Property FirstName() As String
	Public Property LastName() As String
	Public Property EmployeeID() As String
	Public Property Address() As String
	Public Property City() As String
	Public Property Country() As String
	Public Property Customers() As List(Of CustomerDetails)
	 
	Public Sub New(firstName As String, lastName As String, employeeId As String, address As String, city As String, country As String, customers As List(Of CustomerDetails))
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
	Public Property ContactName() As String
	Public Property CompanyName() As String
	Public Property City() As String
	Public Property Country() As String
	Public Property Orders() As List(Of OrderDetails)
	 
	Public Sub New(contactName As String, companyName As String, city As String, country As String, orders As List(Of OrderDetails))
		Me.ContactName = contactName
		Me.CompanyName = companyName
		Me.City = city
		Me.Country = counTry
		Me.Orders = orders
	End Sub
End Class
 
Public Class OrderDetails
	Public Property OrderID() As String
	Public Property OrderDate() As DateTime
	Public Property ShippedDate() As DateTime	 
	Public Property RequiredDate() As DateTime
	
	Public Sub New(ByVal orderId As String, ByVal orderDate As DateTime, ByVal shippedDate As DateTime, ByVal requiredDate As DateTime)
		Me.OrderID = orderId
		Me.OrderDate = orderDate
		Me.ShippedDate = shippedDate
		Me.RequiredDate = requiredDate
	End Sub
End Class

{% endhighlight %}

{% highlight UWP %}
  
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

## Restart numbering in lists

The following code example shows how to restart the list numbering in a Word documents while performing mail merge and merging multiple Word documents.

{% tabs %}  

{% highlight C# %}
//Loads an existing Word document
WordDocument wordDocument = new WordDocument("Template.docx");
//Sets ImportOptions to restart the list numbering
wordDocument.ImportOptions = ImportOptions.ListRestartNumbering;
//Creates the employee details as “IEnumerable” collection
List<Employee> employeeList = new List<Employee>();
employeeList.Add(new Employee("101", "Nancy Davolio", "Seattle, WA, USA"));
employeeList.Add(new Employee("102", "Andrew Fuller", "Tacoma, WA, USA"));
employeeList.Add(new Employee("103", "Janet Leverling", "Kirkland, WA, USA"));
//Creates an instance of “MailMergeDataTable” by specifying mail merge group name and “IEnumerable” collection
MailMergeDataTable dataTable = new MailMergeDataTable("Employee", employeeList);
//Performs mail merge
wordDocument.MailMerge.ExecuteGroup(dataTable);
//Saves the Word document
wordDocument.Save("Sample.docx");
//Closes the instance of Word document object
wordDocument.Close();

/// <summary>
/// Represents the helper class to perform mail merge
/// </summary>
public class Employee
{
    public string EmployeeID { get; set; }
    public string EmployeeName { get; set; }
    public string Location { get; set; }
    /// <summary>
	/// Represents a constructor to create value for merge fields
	/// </summary>    
	public Employee(string employeeId, string employeeName, string location)
    {
        EmployeeID = employeeId;
        EmployeeName = employeeName;
        Location = location;
	}
}
{% endhighlight %}

{% highlight vb.net %}
'Loads an existing Word document
Dim wordDocument As WordDocument = New WordDocument("Template.docx")
'Sets ImportOptions to restart the list numbering
wordDocument.ImportOptions = ImportOptions.ListRestartNumbering
'Creates the employee details as “IEnumerable” collection
Dim employeeList As List(Of Employee) = New List(Of Employee)()
employeeList.Add(New Employee("101", "Nancy Davolio", "Seattle, WA, USA"))
employeeList.Add(New Employee("102", "Andrew Fuller", "Tacoma, WA, USA"))
employeeList.Add(New Employee("103", "Janet Leverling", "Kirkland, WA, USA"))
'Creates an instance of “MailMergeDataTable” by specifying mail merge group name and “IEnumerable” collection
Dim dataTable As MailMergeDataTable = New MailMergeDataTable("Employee", employeeList)
'Performs mail merge
wordDocument.MailMerge.ExecuteGroup(dataTable)
'Saves the Word document
wordDocument.Save("Sample.docx")
'Closes the instance of Word document object
wordDocument.Close()

'Represents the helper class to perform mail merge
Public Class Employee
    Public Property EmployeeID() As String
        Get
            Return m_EmployeeID
        End Get
        Set(value As String)
            m_EmployeeID = value
        End Set
    End Property
    Private m_EmployeeID As String

    Public Property EmployeeName() As String
        Get
            Return m_EmployeeName
        End Get
        Set(value As String)
            m_EmployeeName = value
        End Set
    End Property
    Private m_EmployeeName As String

    Public Property Location() As String
        Get
            Return m_Location
        End Get
        Set(value As String)
            m_Location = value
        End Set
    End Property
    Private m_Location As String

    'Represents a constructor to create value for merge fields
    Public Sub New(employeeId As String, employeeName As String, location As String)
        m_EmployeeID = employeeId
        m_EmployeeName = employeeName
        m_Location = location
	End Sub
End Class
{% endhighlight %}

{% highlight UWP %}
private async void OnButtonClicked(object sender, RoutedEventArgs e)
{
	//Creates an instance of a WordDocument
	Assembly assembly = typeof(App).GetTypeInfo().Assembly;
	WordDocument document = new WordDocument();
	document.Open(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Docx);
	//Sets ImportOptions to restart the list numbering
	wordDocument.ImportOptions = ImportOptions.ListRestartNumbering;
	//Creates the employee details as “IEnumerable” collection
	List<Employee> employeeList = new List<Employee>();
	employeeList.Add(new Employee("101", "Nancy Davolio", "Seattle, WA, USA"));
	employeeList.Add(new Employee("102", "Andrew Fuller", "Tacoma, WA, USA"));
	employeeList.Add(new Employee("103", "Janet Leverling", "Kirkland, WA, USA"));
	//Creates an instance of “MailMergeDataTable” by specifying mail merge group name and “IEnumerable” collection
	MailMergeDataTable dataTable = new MailMergeDataTable("Employee", employeeList);
	//Performs mail merge
	wordDocument.MailMerge.ExecuteGroup(dataTable);
	//Saves the Word file to MemoryStream
	MemoryStream stream = new MemoryStream();
	await document.SaveAsync(stream, FormatType.Docx);
	//Saves the stream as Word file in local machine
	Save(stream, "Sample.docx");
	document.Close();
}

/// <summary>
/// Represents the helper class to perform mail merge
/// </summary>
public class Employee
{
    public string EmployeeID { get; set; }
    public string EmployeeName { get; set; }
    public string Location { get; set; }
    /// <summary>
	/// Represents a constructor to create value for merge fields
	/// </summary>    
	public Employee(string employeeId, string employeeName, string location)
    {
        EmployeeID = employeeId;
        EmployeeName = employeeName;
        Location = location;
	}
}

//Saves the Word document
async void Save(MemoryStream streams, string filename)
{
	streams.Position = 0;
	StorageFile stFile;
	if(!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
	{
		FileSavePicker savePicker = new FileSavePicker();
		savePicker.DefaultFileExtension = ".docx";
		savePicker.SuggestedFileName = filename;
		savePicker.FileTypeChoices.Add("Word Documents", new List<string>() { ".docx" });
		stFile = await savePicker.PickSaveFileAsync();
	}
	else
	{
		StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
		stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
	}
	if (stFile != null)
	{
		using (IRandomAccessStream zipStream = await stFile.OpenAsync(FileAccessMode.ReadWrite))
		{
			//Write compressed data from memory to file
			using (Stream outstream = zipStream.AsStreamForWrite())
			{
				byte[] buffer = streams.ToArray();
				outstream.Write(buffer, 0, buffer.Length);
				outstream.Flush();
			}
		}
	}
	//Launch the saved Word file
	await Windows.System.Launcher.LaunchFileAsync(stFile);
}
{% endhighlight %}

{% highlight ASP.NET CORE %}
//Loads an existing Word document
FileStream fileStream = new FileStream("Template.docx", FileMode.Open);
WordDocument wordDocument = new WordDocument(fileStream, FormatType.Docx);
//Sets ImportOptions to restart the list numbering
wordDocument.ImportOptions = ImportOptions.ListRestartNumbering;
//Creates the employee details as “IEnumerable” collection
List<Employee> employeeList = new List<Employee>();
employeeList.Add(new Employee("101", "Nancy Davolio", "Seattle, WA, USA"));
employeeList.Add(new Employee("102", "Andrew Fuller", "Tacoma, WA, USA"));
employeeList.Add(new Employee("103", "Janet Leverling", "Kirkland, WA, USA"));
//Creates an instance of “MailMergeDataTable” by specifying mail merge group name and “IEnumerable” collection
MailMergeDataTable dataTable = new MailMergeDataTable("Employees", employeeList);
//Performs mail merge
wordDocument.MailMerge.ExecuteGroup(dataTable);
//Saves the Word document
MemoryStream outputStream = new MemoryStream();
wordDocument.Save(outputStream, FormatType.Docx);
//Closes the instance of Word document object
wordDocument.Close();

/// <summary>
/// Represents the helper class to perform mail merge
/// </summary>
public class Employee
{
    public string EmployeeID { get; set; }
    public string EmployeeName { get; set; }
    public string Location { get; set; }
    /// <summary>
	/// Represents a constructor to create value for merge fields
	/// </summary>    
	public Employee(string employeeId, string employeeName, string location)
    {
        EmployeeID = employeeId;
        EmployeeName = employeeName;
        Location = location;
	}
}
{% endhighlight %}

{% highlight XAMARIN %}
//Load the Word document as stream 
Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample.docx");
// Loads the stream into Word Document
WordDocument wordDocument = new WordDocument(docStream, Syncfusion.DocIO.FormatType.Automatic);
//Sets ImportOptions to restart the list numbering
wordDocument.ImportOptions = ImportOptions.ListRestartNumbering;
//Creates the employee details as “IEnumerable” collection
List<Employee> employeeList = new List<Employee>();
employeeList.Add(new Employee("101", "Nancy Davolio", "Seattle, WA, USA"));
employeeList.Add(new Employee("102", "Andrew Fuller", "Tacoma, WA, USA"));
employeeList.Add(new Employee("103", "Janet Leverling", "Kirkland, WA, USA"));
//Creates an instance of “MailMergeDataTable” by specifying mail merge group name and “IEnumerable” collection
MailMergeDataTable dataTable = new MailMergeDataTable("Employees", employeeList);
//Performs mail merge
wordDocument.MailMerge.ExecuteGroup(dataTable);
//Saves the Word document
MemoryStream outputStream = new MemoryStream();
wordDocument.Save(outputStream, FormatType.Docx);
//Closes the instance of Word document object
wordDocument.Close();

/// <summary>
/// Represents the helper class to perform mail merge
/// </summary>
public class Employee
{
	public string EmployeeID { get; set; }	
	public string EmployeeName { get; set; }	
	public string Location { get; set; }	
	/// <summary>	
	/// Represents a constructor to create value for merge fields	
	/// </summary>    	
	public Employee(string employeeId, string employeeName, string location)	
	{
		EmployeeID = employeeId;	
		EmployeeName = employeeName;	
		Location = location;
	}
}
{% endhighlight %}

{% endtabs %}

## Insert as new row

The following code example shows how to add each record as new row inside table when the row group contains only one cell, which means, the merge fields denoting group start and end present inside the same cell.

{% tabs %}  

{% highlight C# %}

//Opens the template document 
WordDocument document = new WordDocument(@"Data/Template.docx");
//Creates a data table
DataTable table = new DataTable("CompatibleVersions");
table.Columns.Add("WordVersion");
//Creates a new data row
DataRow row = table.NewRow();
row["WordVersion"] = "Microsoft Word 97-2003";
table.Rows.Add(row);
row = table.NewRow();
row["WordVersion"] = "Microsoft Word 2007";
table.Rows.Add(row);
row = table.NewRow();
row["WordVersion"] = "Microsoft Word 2010";
table.Rows.Add(row);
row = table.NewRow();
row["WordVersion"] = "Microsoft Word 2013";
table.Rows.Add(row);
row = table.NewRow();
row["WordVersion"] = "Microsoft Word 2019";
table.Rows.Add(row);
//Enable the flag to insert a new row for every group in a table
document.MailMerge.InsertAsNewRow = true;
//Execute mail merge
document.MailMerge.ExecuteGroup(table);
//Saves and closes the WordDocument instance
document.Save("Sample.docx");
document.Close();

{% endhighlight %}

{% highlight VB.NET %}

'Opens the template document 
Dim document As WordDocument = New WordDocument("Data/Template.docx")
'Creates a data table
Dim table As DataTable = New DataTable("CompatibleVersions")
table.Columns.Add("WordVersion")
'Creates a new data row
Dim row As DataRow = table.NewRow()
row("WordVersion") = "Microsoft Word 97-2003"
table.Rows.Add(row)
row = table.NewRow()
row("WordVersion") = "Microsoft Word 2007"
table.Rows.Add(row)
row = table.NewRow()
row("WordVersion") = "Microsoft Word 2010"
table.Rows.Add(row)
row = table.NewRow()
row("WordVersion") = "Microsoft Word 2013"
table.Rows.Add(row)
row = table.NewRow()
row("WordVersion") = "Microsoft Word 2019"
table.Rows.Add(row)		
'Enable the flag to insert a new row for every group in a table
document.MailMerge.InsertAsNewRow = True		
'Execute mail merge
document.MailMerge.ExecuteGroup(table)		
'Saves and closes the WordDocument instance
document.Save("Sample.docx")
document.Close()

{% endhighlight %}

{% highlight UWP %}

// Not working

{% endhighlight %}

{% highlight ASP.NET CORE %}

//Opens the template document 
FileStream fileStreamPath = new FileStream(@"Data\Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);
//Creates a data table 
DataTable table = new DataTable("CompatibleVersions");
table.Columns.Add("WordVersion");
//Creates a new data row 
DataRow row = table.NewRow();
row["WordVersion"] = "Microsoft Word 97-2003";
table.Rows.Add(row);
row = table.NewRow();
row["WordVersion"] = "Microsoft Word 2007";
table.Rows.Add(row);
row = table.NewRow();
row["WordVersion"] = "Microsoft Word 2010";
table.Rows.Add(row);
row = table.NewRow();
row["WordVersion"] = "Microsoft Word 2013";
table.Rows.Add(row);
row = table.NewRow();
row["WordVersion"] = "Microsoft Word 2019";
table.Rows.Add(row);			
//Enable the flag to insert a new row for every group in a table
document.MailMerge.InsertAsNewRow = true;			
//Execute mail merge
document.MailMerge.ExecuteGroup(table);
MemoryStream stream = new MemoryStream();
//Saves the Word document to MemoryStream
document.Save(stream, FormatType.Docx);
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Sample.docx");

{% endhighlight %}

{% highlight XAMARIN %}

//Opens the template document
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Docx);
//Creates a data table
DataTable table = new DataTable("CompatibleVersions");
table.Columns.Add("WordVersion");
//Creates a new data row
DataRow row = table.NewRow();
row["WordVersion"] = "Microsoft Word 97-2003";
table.Rows.Add(row);
row = table.NewRow();
row["WordVersion"] = "Microsoft Word 2007";
table.Rows.Add(row);
row = table.NewRow();
row["WordVersion"] = "Microsoft Word 2010";
table.Rows.Add(row);
row = table.NewRow();
row["WordVersion"] = "Microsoft Word 2013";
table.Rows.Add(row);
row = table.NewRow();
row["WordVersion"] = "Microsoft Word 2019";
table.Rows.Add(row);
//Enable the flag to insert a new row for every group in a table
document.MailMerge.InsertAsNewRow = true;
//Execute mail merge
document.MailMerge.ExecuteGroup(table);
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.docx", "application/msword", stream);
//Closes the document 
document.Close();

{% endhighlight %}

{% endtabs %}

## Skip to merge image

The following code example shows how to skip merging particular image while performing mail merge in Word document.

{% tabs %}  

{% highlight C# %}

//Opens the template document 
WordDocument document = new WordDocument(@"Template.docx");
//Uses the mail merge events to perform the conditional formatting during runtime
document.MailMerge.MergeImageField += new MergeImageFieldEventHandler(MergeEmployeePhoto);
//Executes Mail Merge with groups
string[] fieldNames = { "Nancy", "Andrew", "Steven" };
string[] fieldValues = { "Nancy.png", "Andrew.png", "Steven.png" };
//Execute mail merge
document.MailMerge.Execute(fieldNames, fieldValues);
//Saves and closes the Word document instance
document.Save("Sample.docx");
document.Close();

{% endhighlight %}

{% highlight VB.NET %}

'Opens the template document  
Dim document As WordDocument =  New WordDocument("Template.docx")  
'Uses the mail merge events to perform the conditional formatting during runtime 
AddHandler document.MailMerge.MergeImageField, AddressOf MergeEmployeePhoto 
'Executes Mail Merge with groups 
Dim fieldNames() As String = {"Nancy", "Andrew", "Steven"}
Dim fieldValues() As String = {"Nancy.png", "Andrew.png", "Steven.png"} 
'Execute mail merge 
document.MailMerge.Execute(fieldNames, fieldValues) 
'Saves and closes the Word document instance 
document.Save("Sample.docx") 
document.Close()

{% endhighlight %}

{% highlight UWP %}

private async void OnButtonClicked(object sender, RoutedEventArgs e)
{
	//Creates an instance of a WordDocument
	Assembly assembly = typeof(App).GetTypeInfo().Assembly;
	WordDocument document = new WordDocument();
	document.Open(assembly.GetManifestResourceStream("Sample.Assets.Template.docx"), FormatType.Docx);
	//Uses the mail merge events to perform the conditional formatting during runtime
	document.MailMerge.MergeImageField += new MergeImageFieldEventHandler(MergeEmployeePhoto);
	//Executes Mail Merge with groups
	string[] fieldNames = { "Nancy", "Andrew", "Steven" };
	string[] fieldValues = { "Sample.Assets.Nancy.png", "Sample.Assets.Andrew.png", "Sample.Assets.Steven.png" };
	//Execute mail merge
	document.MailMerge.Execute(fieldNames, fieldValues);
	//Saves the Word file to MemoryStream
	MemoryStream stream = new MemoryStream();
	await document.SaveAsync(stream, FormatType.Docx);
	//Saves the stream as Word file in local machine
	Save(stream, "Sample.docx");
	document.Close();
}

// Saves the Word document
async void Save(MemoryStream streams, string filename)
{
	streams.Position = 0;
	StorageFile stFile;
	if(!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
	{
		FileSavePicker savePicker = new FileSavePicker();
		savePicker.DefaultFileExtension = ".docx";
		savePicker.SuggestedFileName = filename;
		savePicker.FileTypeChoices.Add("Word Documents", new List<string>() { ".docx" });
		stFile = await savePicker.PickSaveFileAsync();
	}
	else
	{
		StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
		stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
	}
	if (stFile != null)
	{
		using (IRandomAccessStream zipStream = await stFile.OpenAsync(FileAccessMode.ReadWrite))
		{
			// Write compressed data from memory to file
			using (Stream outstream = zipStream.AsStreamForWrite())
			{
				byte[] buffer = streams.ToArray();
				outstream.Write(buffer, 0, buffer.Length);
				outstream.Flush();
			}
		}
	}
	// Launch the saved Word file
	await Windows.System.Launcher.LaunchFileAsync(stFile);
}

{% endhighlight %}

{% highlight ASP.NET CORE %}

//Opens the template document 
FileStream fileStreamPath = new FileStream(@"Data\Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);
//Uses the mail merge events to perform the conditional formatting during runtime
document.MailMerge.MergeImageField += new MergeImageFieldEventHandler(MergeEmployeePhoto);
//Executes Mail Merge with groups
string[] fieldNames = { "Nancy", "Andrew", "Steven" };
string[] fieldValues = { "Nancy.png", "Andrew.png", "Steven.png" };
//Execute mail merge
document.MailMerge.Execute(fieldNames, fieldValues);
MemoryStream stream = new MemoryStream();
//Saves the Word document to MemoryStream
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
document.MailMerge.MergeImageField += new MergeImageFieldEventHandler(MergeEmployeePhoto);
//Executes Mail Merge with groups
string[] fieldNames = { "Nancy", "Andrew", "Steven" };
string[] fieldValues = { "Nancy.png", "Andrew.png", "Steven.png" };
//Execute mail merge
document.MailMerge.Execute(fieldNames, fieldValues);
//Saves the Word file to MemoryStream
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.docx", "application/msword", stream);
//Closes the document 
document.Close();

{% endhighlight %}

{% endtabs %}

The following code example provides supporting methods.

{% tabs %}  

{% highlight C# %}

private void MergeEmployeePhoto(object sender, MergeImageFieldEventArgs args)
{
	//Skip to merge particular image
	if (args.FieldName == "Andrew")
		args.Skip = true;
	//Sets image
	args.ImageFileName = args.FieldValue.ToString();
}  

{% endhighlight %}

{% highlight VB.NET %}

Private Sub MergeEmployeePhoto(ByVal sender As Object, ByVal args As MergeImageFieldEventArgs) 
	'Skip to merge particular image 
	If args.FieldName = "Andrew" Then 
		args.Skip = True
	End If 
	'Sets image 
	Dim ProductFileName As String = args.FieldValue.ToString()	
	args.Image = Image.FromFile("Data/" + ProductFileName) 
End Sub

{% endhighlight %}

{% highlight UWP %}

private void MergeEmployeePhoto(object sender, MergeImageFieldEventArgs args)
{
	//Skip to merge particular image
	if (args.FieldName == "Andrew")
		args.Skip = true;
	//Sets image
	args.ImageFileName = args.FieldValue.ToString();
}  

{% endhighlight %}

{% highlight ASP.NET CORE %}

private void MergeEmployeePhoto(object sender, MergeImageFieldEventArgs args)
{
	//Skip to merge particular image
	if (args.FieldName == "Andrew")
		args.Skip = true;
	//Sets image
	string ProductFileName = args.FieldValue.ToString();	
	FileStream imageStream = new FileStream(ProductFileName, FileMode.Open, FileAccess.Read);	
	args.ImageStream = imageStream;
	WPicture picture = args.Picture;	
	picture.Height = 100;	
	picture.Width = 100;
}  

{% endhighlight %}

{% highlight XAMARIN %}

private void MergeEmployeePhoto(object sender, MergeImageFieldEventArgs args)
{
	//Skip to merge particular image
	if (args.FieldName == "Andrew")
		args.Skip = true;
	//Sets image
	Assembly assembly = typeof(App).GetTypeInfo().Assembly;
	Stream imageStream = assembly.GetManifestResourceStream(args.FieldValue.ToString());
	args.ImageStream = imageStream;
	WPicture picture = args.Picture;
	picture.Height = 100;
	picture.Width = 100;
}  

{% endhighlight %}

{% endtabs %}