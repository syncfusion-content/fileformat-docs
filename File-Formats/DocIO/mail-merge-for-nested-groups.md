---
title: Mail merge for nested groups | Word library (DocIO) | Syncfusion
description: This section illustrates how to Mail merge for nested groups - replace merge fields in nested regions of document with relational data.
platform: file-formats
control: DocIO
documentation: UG
---

# Performing Nested Mail merge for group

You can perform nested Mail merge with relational or hierarchical data source and independent data tables in a template document.

You need to define the commands with table name and expression for linking the independent data tables during nested Mail merge process. You can use the “%TableName.ColumnName%” expression for getting the current value of specified column in a table.

Nested Mail merge operation automatically replaces the merge field with immediate group data. You can also predefine the group data that is populated to a merge field. You need to add a corresponding group name as a prefix to the merge field name for merging a specific group data to the merge field.

For example:
  * The merge field name should be like “TableName:Id” (<<TableName:MergeFieldName>>)
  * The merge field name should be like “Image:TableName:Photo” (<<Image:TableName:MergeFieldName>>)

The following code example shows how to perform a nested Mail merge.


{% tabs %}  

{% highlight c# %}
//Opens the template document
WordDocument document = new WordDocument(@"Template.docx");
//Gets the employee details as “IEnumerable” collection
List<Employees> employeeList = GetEmployees();
//Creates an instance of “MailMergeDataTable” by specifying mail merge group name and “IEnumerable” collection
MailMergeDataTable dataTable = new MailMergeDataTable("Employees", employeeList);
//Performs Mail merge
document.MailMerge.ExecuteNestedGroup(dataTable);
//Saves and closes the WordDocument instance
document.Save("Result.docx");
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Opens the template document 
Dim document As New WordDocument("Template.docx")
'Gets the employee details as “IEnumerable” collection
Dim employeeList As List(Of Employees) = GetEmployees()
'Creates an instance of “MailMergeDataTable” by specifying mail merge group name and “IEnumerable” collection
Dim dataTable As New MailMergeDataTable("Employees", employeeList)
'Performs Mail merge
document.MailMerge.ExecuteNestedGroup(dataTable)
'Saves and closes the WordDocument instance
document.Save("Result.docx")
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
	//Performs Mail merge
	document.MailMerge.ExecuteNestedGroup(dataTable);
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
FileStream fileStreamPath = new FileStream(@"Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);
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
{% endhighlight %}

{% endtabs %}  

The following code example provides supporting methods for the above code.

{% tabs %}  
{% highlight c# %}
public static List<Employees> GetEmployees()
{
	List<OrderDetails> orders = new List<OrderDetails>();
	orders.Add(new OrderDetails("10835", new DateTime(2015, 1, 5), new DateTime(2015, 1, 12), new DateTime(2015, 1, 21)));
	orders.Add(new OrderDetails("10952", new DateTime(2015, 2, 5), new DateTime(2015, 2, 12), new DateTime(2015, 2, 21)));
	CustomerDetails customers = new CustomerDetails("Maria Anders", "Maria Anders", "Berlin", "Germany", orders);
	List<Employees> employees = new List<Employees>();
	employees.Add(new Employees("Nancy", "Smith", "1", "505 - 20th Ave. E. Apt. 2A,", "Seattle", "USA", customers));
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
	public CustomerDetails Customers { get; set; }
	
	public Employees(string firstName, string lastName, string employeeId, string address, string city, string country, CustomerDetails customers)
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
Public Function GetEmployees() As List(Of Employees)
	Dim orders As New List(Of OrderDetails)()
	orders.Add(New OrderDetails("10835", New DateTime(2015, 1, 5), New DateTime(2015, 1, 12), New DateTime(2015, 1, 21)))
	orders.Add(New OrderDetails("10952", New DateTime(2015, 2, 5), New DateTime(2015, 2, 12), New DateTime(2015, 2, 21)))
	Dim customers As New CustomerDetails("Maria Anders", "Maria Anders", "Berlin", "Germany", orders)
	Dim employees As New List(Of Employees)()
	employees.Add(New Employees("Nancy", "Smith", "1", "505 - 20th Ave. E. Apt. 2A,", "Seattle", "USA", customers))
	Return employees
End Function

Public Class Employees
	Public Property FirstName() As String
		Get
			Return m_FirstName
		End Get
		Set(value As String)
			m_FirstName = value
		End Set
	End Property
	Private m_FirstName As String

	Public Property LastName() As String
		Get
			Return m_LastName
		End Get
		Set(value As String)
			m_LastName = value
		End Set
	End Property
	Private m_LastName As String

	Public Property EmployeeID() As String
		Get
			Return m_EmployeeID
		End Get
		Set(value As String)
			m_EmployeeID = value
		End Set
	End Property
	Private m_EmployeeID As String

	Public Property Address() As String
		Get
			Return m_Address
		End Get	
		Set(value As String)
			m_Address = value
		End Set
	End Property
	Private m_Address As String

	Public Property City() As String
		Get
			Return m_City
		End Get
		Set(value As String)
			m_City = value
		End Set
	End Property
	Private m_City As String

	Public Property Country() As String
		Get
			Return m_Country
		End Get
		Set(value As String)
			m_Country = value
		End Set
	End Property
	Private m_Country As String

	Public Property Customers() As CustomerDetails
		Get
			Return m_Customers
		End Get
		Set(value As CustomerDetails)
			m_Customers = value
		End Set
	End Property
	Private m_Customers As CustomerDetails

	Public Sub New(firstName As String, lastName As String, employeeId As String, address As String, city As String, country As String, _customers As CustomerDetails)
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
		Get
			Return m_ContactName
		End Get
		Set(value As String)
			m_ContactName = value
		End Set
	End Property
	Private m_ContactName As String

	Public Property CompanyName() As String
		Get
			Return m_CompanyName
		End Get
		Set(value As String)
			m_CompanyName = value
		End Set
	End Property
	Private m_CompanyName As String

	Public Property City() As String
		Get
			Return m_City
		End Get
		Set(value As String)
			m_City = value
		End Set
	End Property
	Private m_City As String

	Public Property Country() As String
		Get
			Return m_Country
		End Get
		Set(value As String)
			m_Country = value
		End Set
	End Property
	Private m_Country As String

	Public Property Orders() As List(Of OrderDetails)
		Get
			Return m_Orders
		End Get
		Set(value As List(Of OrderDetails))
			m_Orders = value
		End Set
	End Property
	Private m_Orders As List(Of OrderDetails)

	Public Sub New(contactName As String, companyName As String, city As String, country As String, orders As List(Of OrderDetails))
		Me.ContactName = contactName
		Me.CompanyName = companyName
		Me.City = city
		Me.Country = country
		Me.Orders = orders
	End Sub
End Class

Public Class OrderDetails
	Public Property OrderID() As String
		Get
			Return m_OrderID
		End Get
		Set(value As String)
			m_OrderID = value
		End Set
	End Property
	Private m_OrderID As String

	Public Property OrderDate() As DateTime
		Get
			Return m_OrderDate
		End Get
		Set(value As DateTime)
			m_OrderDate = value
		End Set
	End Property
	Private m_OrderDate As DateTime

	Public Property ShippedDate() As DateTime
		Get
			Return m_ShippedDate
		End Get
		Set(value As DateTime)
			m_ShippedDate = value
		End Set
	End Property
	Private m_ShippedDate As DateTime

	Public Property RequiredDate() As DateTime
		Get
			Return m_RequiredDate
		End Get
		Set(value As DateTime)
			m_RequiredDate = value
		End Set
	End Property
	Private m_RequiredDate As DateTime

	Public Sub New(orderId As String, orderDate As DateTime, shippedDate As DateTime, requiredDate As DateTime)
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
	orders.Add(new OrderDetails("10952", new DateTime(2015, 2, 5), new DateTime(2015, 2, 12), new DateTime(2015, 2, 21)));
	CustomerDetails customers = new CustomerDetails("Maria Anders", "Maria Anders", "Berlin", "Germany", orders);
	List<Employees> employees = new List<Employees>();
	employees.Add(new Employees("Nancy", "Smith", "1", "505 - 20th Ave. E. Apt. 2A,", "Seattle", "USA", customers));
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
	public CustomerDetails Customers { get; set; }
	
	public Employees(string firstName, string lastName, string employeeId, string address, string city, string country, CustomerDetails customers)
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
	orders.Add(new OrderDetails("10952", new DateTime(2015, 2, 5), new DateTime(2015, 2, 12), new DateTime(2015, 2, 21)));
	CustomerDetails customers = new CustomerDetails("Maria Anders", "Maria Anders", "Berlin", "Germany", orders);
	List<Employees> employees = new List<Employees>();
	employees.Add(new Employees("Nancy", "Smith", "1", "505 - 20th Ave. E. Apt. 2A,", "Seattle", "USA", customers));
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
	public CustomerDetails Customers { get; set; }

	public Employees(string firstName, string lastName, string employeeId, string address, string city, string country, CustomerDetails customers)
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
	orders.Add(new OrderDetails("10952", new DateTime(2015, 2, 5), new DateTime(2015, 2, 12), new DateTime(2015, 2, 21)));
	CustomerDetails customers = new CustomerDetails("Maria Anders", "Maria Anders", "Berlin", "Germany", orders);
	List<Employees> employees = new List<Employees>();
	employees.Add(new Employees("Nancy", "Smith", "1", "505 - 20th Ave. E. Apt. 2A,", "Seattle", "USA", customers));
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
	public CustomerDetails Customers { get; set; }
	
	public Employees(string firstName, string lastName, string employeeId, string address, string city, string country, CustomerDetails customers)
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

The resultant document looks as follows.

![Nested Mail merge resultant document](MailMerge_images/MailMerge_img7.jpeg)