---
title: Group Mail merge | Syncfusion
description: This section illustrates how to perform Mail merge in the specific region with data source in a Word document
platform: file-formats
control: DocIO
documentation: UG
---

# Performing Mail merge for a group

You can perform Mail merge and append multiple records from data source within a specified region to a template document. The region between start and end groups merge fields. It gets repeated for every record from the data source. The region where the Mail merge operations are to be performed must be marked by two MergeFields with the following names.

  * «TableStart:TableName» and «BeginGroup:GroupName» - For the entry point of the region
  * «TableEnd:TableName» and «EndGroup:GroupName» - For the end point of the region
  
  1.TableStart and TableEnd region is preferred for performing Mail merge inside the table cell
  
  2.BeginGroup and EndGroup region is preferred for performing Mail merge inside the document body contents.
  
For example – Consider that you have a template document as shown.

![Mail merge for a group](MailMerge_images/MailMerge_img4.jpeg)

In this template, Employees is the group name and the same name should be used while performing Mail merge through code. There are two special merge fields “TableStart:Employees” and “TableEnd:Employees”, to denote the start and end of the Mail merge group.

The MailMerge class provides various overloads for ExecuteGroup method to perform Mail merge within a group from various data sources. The following code example shows how to perform Mail merge in the specific region with data source retrieved from SQL connection.

{% tabs %}

{% highlight c# %}

WordDocument document = new WordDocument("EmployeesTemplate.docx");

//Gets the data table. 

DataTable table = GetDataTable();

// Executes Mail Merge with groups. 

document.MailMerge.ExecuteGroup(table);

//Saves and closes the WordDocument instance

document.Save("Result.docx");

document.Close();

{% endhighlight %}

{% highlight vb.net %}

Dim document As New WordDocument("EmployeesTemplate.docx")

'Gets the data table. 

Dim table As DataTable = GetDataTable()

' Executes Mail Merge with groups. 

document.MailMerge.ExecuteGroup(table)

'Saves and closes the WordDocument instance

document.Save("Result.docx")

document.Close()

{% endhighlight %}

{% endtabs %}

The following code example provides supporting methods for the above code.

{% tabs %}

{% highlight c# %}

private DataTable GetDataTable()

{

SqlCeConnection conn = new SqlCeConnection("Data Source = " + datasourceName);

conn.Open();

SqlCeDataAdapter adapter = new SqlCeDataAdapter("Select TOP(5) * from EmployeesReport", conn);

adapter.Fill(dataset);

adapter.Dispose();

conn.Close();

System.Data.DataTable table = dataset.Tables[0];

// Sets table name as Employees for template merge field reference.

table.TableName = "Employees";

return table;

}

{% endhighlight %}

{% highlight vb.net %}

Private Function GetDataTable() As DataTable

Dim conn As New SqlCeConnection ("Data Source = " + datasourceName)

conn.Open()

Dim adapter As New SqlCeDataAdapter ("Select TOP(5) * from EmployeesReport", conn)

adapter.Fill(dataset)

adapter.Dispose()

conn.Close()

Dim table As System.Data.DataTable = dataset.Tables(0)

' Sets table name as Employees for template merge field reference.

table.TableName = "Employees"

Return table

End Function

{% endhighlight %}

{% endtabs %}

The resultant document looks as follows.

![Group resultant document](MailMerge_images/MailMerge_img5.jpeg)

## Performing Mail merge with business objects

You can perform Mail merge with business objects in a template document. The following code snippet shows how to perform Mail merge with business objects

{% tabs %}

{% highlight c# %}

//Opens the template document. 

WordDocument document = new WordDocument(@"Template.docx");

//Gets the employee details as “IEnumerable” collection

List<Employee> employeeList = GetEmployees();

//Creates an instance of “MailMergeDataTable” by specifying mail merge group name and “IEnumerable” collection.

MailMergeDataTable dataTable = new MailMergeDataTable("Employees", employeeList);

//Performs Mail merge

document.MailMerge.ExecuteGroup(dataTable);

//Saves and closes the Word document instance

document.Save("Result.docx");

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens the template document. 

Dim document As New WordDocument("Template.docx")

'Gets the employee details as “IEnumerable” collection

Dim employeeList As List(Of Employee) = GetEmployees()

'Creates an instance of “MailMergeDataTable” by specifying mail merge group name and “IEnumerable” collection.

Dim dataTable As New MailMergeDataTable("Employees", employeeList)

'Performs Mail merge

document.MailMerge.ExecuteGroup(dataTable)

'Saves and closes the Word document instance

document.Save("Result.docx")

document.Close()

{% endhighlight %}

{% endtabs %}

The following code example provides supporting methods and class for the above code

{% tabs %}

{% highlight c# %}

public List<Employee> GetEmployees()

{

List<Employee> employees = new List<Employee>();

employees.Add(new Employee("Andy", "Bernard", "Sales Representative", "505 - 20th Ave. E. Apt. 2A,", "Seattle", "WA", "USA", "Andy.png"));

employees.Add(new Employee("Andrew", "Fuller", "Vice President, Sales", "908 W. Capital Way", "Tacoma", "WA", "USA", "Andrew.png"));

employees.Add(new Employee("Stanley", "Hudson", "Sales Representative", "722 Moss Bay Blvd.", "Kirkland", "WA", "USA", "Stanley.png"));

employees.Add(new Employee("Margaret", "Peacock", "Sales Representative", "4110 Old Redmond Rd.", "Redmond", "WA", "USA", "Margaret.png"));

employees.Add(new Employee("Steven", "Buchanan", "Sales Manager", "14 Garrett Hill", "London", string.Empty, "UK", "Steven.png"));

return employees;

}

public class Employee

{

public string FirstName { get; set; }

public string LastName { get; set; }

public string Address { get; set; }

public string City { get; set; }

public string Region { get; set; }

public string Country { get; set; }

public string Title { get; set; }

public Image Photo { get; set; }

public Employee(string firstName, string lastName, string title, string address, string city, string region, string country, string photoFilePath)

{

FirstName = firstName;

LastName = lastName;

Title = title;

Address = address;

City = city;

Region = region;

Country = country;

Photo = Image.FromFile(photoFilePath);

}

}

{% endhighlight %}

{% highlight vb.net %}

Public Function GetEmployees() As List(Of Employee)

Dim employees As New List(Of Employee)()

employees.Add(New Employee("Andy", "Bernard", "Sales Representative", "505 - 20th Ave. E. Apt. 2A,", "Seattle", "WA", "USA", "Andy.png"))

employees.Add(New Employee("Andrew", "Fuller", "Vice President, Sales", "908 W. Capital Way", "Tacoma", "WA", "USA", "Andrew.png"))

employees.Add(New Employee("Stanley", "Hudson", "Sales Representative", "722 Moss Bay Blvd.", "Kirkland", "WA", "USA", "Stanley.png"))

employees.Add(New Employee("Margaret", "Peacock", "Sales Representative", "4110 Old Redmond Rd.", "Redmond", "WA", "USA", "Margaret.png"))

employees.Add(New Employee("Steven", "Buchanan", "Sales Manager", "14 Garrett Hill", "London", string.Empty, "UK", "Steven.png"))

Return employees

End Function

Public Class Employee

Public Property FirstName() As String

Get

Return m_FirstName

End Get

Set(value As String)

m_FirstName = Value

End Set

End Property

Private m_FirstName As String

Public Property LastName() As String

Get

Return m_LastName

End Get

Set(value As String)

m_LastName = Value

End Set

End Property

Private m_LastName As String

Public Property Address() As String

Get

Return m_Address

End Get

Set(value As String)

m_Address = Value

End Set

End Property

Private m_Address As String

Public Property City() As String

Get

Return m_City

End Get

Set(value As String)

m_City = Value

End Set

End Property

Private m_City As String

Public Property Region() As String

Get

Return m_Region

End Get

Set(value As String)

m_Region = Value

End Set

End Property

Private m_Region As String

Public Property Country() As String

Get

Return m_Country

End Get

Set(value As String)

m_Country = Value

End Set

End Property

Private m_Country As String

Public Property Title() As String

Get

Return m_Title

End Get

Set(value As String)

m_Title = Value

End Set

End Property

Private m_Title As String

Public Property Photo() As Image

Get

Return m_Photo

End Get

Set(value As Image)

m_Photo = Value

End Set

End Property

Private m_Photo As Image

Public Sub New(firstName As String, lastName As String, title As String, address As String, city As String, region As String, country As String, photoFilePath As String)

FirstName = firstName

LastName = lastName

Title = title

Address = address

City = city

Region = region

Country = country

Photo = Image.FromFile(photoFilePath)

End Sub

End Class

{% endhighlight %}

{% endtabs %}

You can find an example about overloads of the ExecuteGroup method from the Following table:

<table>
<thead>
<tr>
<td><b>Overloads</b></td>
<td><b>Examples</b></td>
</tr>
</thead>
<tr>
<td>ExecuteGroup(DataView)</td>
<td>
<a href="http://www.syncfusion.com/downloads/support/directtrac/general/ze/MAAA1B~11635160515.zip">Generate letter for filtered contacts</a>
</td>
</tr>
</table>