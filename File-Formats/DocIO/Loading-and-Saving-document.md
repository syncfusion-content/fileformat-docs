---
title: Loading & Saving document | DocIO | Syncfusion
description: This section illustrates how to load and save the Word document using Syncfusion Word library (Essential DocIO)
platform: file-formats
control: DocIO
documentation: UG
---
# Loading & saving document

## Namespaces required

The following namespaces of Essential DocIO need to be included in your application to load and save the Word document.

{% tabs %}  

{% highlight c# %}
using Syncfusion.DocIO;
using Syncfusion.DocIO.DLS;
{% endhighlight %}

{% highlight vb.net %}
using Syncfusion.DocIO;
using Syncfusion.DocIO.DLS;
{% endhighlight %}

{% highlight UWP %}
using Syncfusion.DocIO;
using Syncfusion.DocIO.DLS;
{% endhighlight %}

{% highlight ASP.NET CORE %}
using Syncfusion.DocIO;
using Syncfusion.DocIO.DLS;
{% endhighlight %}

{% highlight XAMARIN %}
using Syncfusion.DocIO;
using Syncfusion.DocIO.DLS;
{% endhighlight %}

{% endtabs %}

## Opening an existing document

You can open an existing Word document by using either the `Open` method or the constructor of `WordDocument` class

{% tabs %}  

{% highlight c# %}
//Opens an existing document from file system through constructor of WordDocument class
WordDocument document = new WordDocument(fileName);
{% endhighlight %}

{% highlight vb.net %}
'Opens an existing document from file system through constructor of WordDocument class
Dim document As New WordDocument(fileName)
{% endhighlight %}

{% highlight UWP %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing document through constructor of `WordDocument` class
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("CreateWordSample.Assets.Test.docx"),FormatType.Docx);
{% endhighlight %}

{% highlight ASP.NET CORE %}
//Opens an existing document from stream through constructor of `WordDocument` class
FileStream fileStreamPath = new FileStream(@"Data/Hello World.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
WordDocument document = new WordDocument(fileStreamPath, FormatType.Automatic);
{% endhighlight %}

{% highlight XAMARIN %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Opens an existing document through constructor of `WordDocument` class
WordDocument document = new WordDocument(assembly.GetManifestResourceStream("XamarinFormsApp1.Assets.Test.docx"),FormatType.Automatic);
{% endhighlight %}

{% endtabs %}

{% tabs %} 
 
{% highlight c# %}
//Creates an empty Word document instance
WordDocument document = new WordDocument();
//Loads or opens an existing word document through Open method of WordDocument class
document.Open(fileName);
{% endhighlight %}

{% highlight vb.net %}
'Creates an empty Word document instance
Dim document As New WordDocument()
'Loads or opens an existing word document through Open method of WordDocument class
document.Open(fileName)
{% endhighlight %}

{% highlight UWP %}
//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".docx");
//Creates a storage file from FileOpenPicker
StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();
WordDocument document = new WordDocument();
await document.OpenAsync(inputStorageFile);
{% endhighlight %}

{% highlight ASP.NET CORE %}
//Opens an existing document from stream through constructor of `WordDocument` class
FileStream fileStreamPath = new FileStream(@"Data/Hello World.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
//Creates an empty Word document instance
WordDocument document = new WordDocument();
//Loads or opens an existing word document through Open method of WordDocument class
document.Open(fileStreamPath, FormatType.Automatic);
{% endhighlight %}

{% highlight XAMARIN %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Creates an empty Word document instance
WordDocument document = new WordDocument();
//Loads or opens an existing word document through Open method of WordDocument class
document.Open(assembly.GetManifestResourceStream("XamarinFormsApp1.Assets.Test.docx"),FormatType.Automatic);
{% endhighlight %}

{% endtabs %}  

## Opening an existing document from Stream

You can open an existing document from stream by using either the overloads of `Open` methods or the constructor of `WordDocument` class

{% tabs %}  

{% highlight c# %}
//Opens an existing document from stream through constructor of WordDocument class
WordDocument document = new WordDocument(wordDocumentStream, FormatType.Automatic);
{% endhighlight %}

{% highlight vb.net %}
'Opens an existing document from stream through constructor of WordDocument class
Dim document As New WordDocument(wordDocumentStream, FormatType.Automatic)
{% endhighlight %}

{% highlight UWP %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Loads or opens an existing Word document from stream
Stream inputStream = assembly.GetManifestResourceStream("CreateWordSample.Assets.Test.docx");
//Opens an existing document through constructor of `WordDocument` class
WordDocument document = new WordDocument(inputStream, FormatType.Docx);
{% endhighlight %}

{% highlight ASP.NET CORE %}
//Opens an existing document from stream through constructor of `WordDocument` class
FileStream fileStreamPath = new FileStream(@"Data/Hello World.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
//Opens an existing document from stream through constructor of WordDocument class
WordDocument document = new WordDocument(fileStreamPath, FormatType.Automatic);
{% endhighlight %}

{% highlight XAMARIN %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Loads or opens an existing Word document from stream
Stream inputStream = assembly.GetManifestResourceStream("XamarinFormsApp1.Assets.Hello World.docx");
//Opens an existing document through constructor of `WordDocument` class
WordDocument document = new WordDocument(inputStream, FormatType.Automatic);
{% endhighlight %}

{% endtabs %}  

{% tabs %}   

{% highlight c# %}
//Creates an empty WordDocument instance
WordDocument document = new WordDocument();
//Loads or opens an existing Word document through Open method of WordDocument class
document.Open(wordDocumentStream, FormatType.Automatic);
{% endhighlight %}

{% highlight vb.net %}
'Creates an empty WordDocument instance
Dim document As New WordDocument()
'Loads or opens an existing word document through Open method of WordDocument class
document.Open(wordDocumentStream, FormatType.Automatic)
{% endhighlight %}

{% highlight UWP %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Creates an empty WordDocument instance
using (WordDocument document = new WordDocument())
{
	//Loads or opens an existing Word document from stream
	Stream inputStream = assembly.GetManifestResourceStream("CreateWordSample.Assets.Test.docx");
	//Loads or opens an existing Word document through Open method of WordDocument class
	document.Open(inputStream, FormatType.Docx);
}
{% endhighlight %}

{% highlight ASP.NET CORE %}
//Creates an empty WordDocument instance
using (WordDocument document = new WordDocument())
{
	//Loads or opens an existing Word document from stream
	FileStream fileStreamPath = new FileStream(@"Data/Hello World.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
	//Loads or opens an existing Word document through Open method of WordDocument class 
	document.Open(fileStreamPath, FormatType.Automatic);
}
{% endhighlight %}

{% highlight XAMARIN %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Creates an empty WordDocument instance
using (WordDocument document = new WordDocument())
{
	//Loads or opens an existing Word document from stream
	Stream inputStream = assembly.GetManifestResourceStream("XamarinFormsApp1.Assets.Hello World.docx");
	//Loads or opens an existing Word document through Open method of WordDocument class
	document.Open(inputStream, FormatType.Automatic);
}
{% endhighlight %}

{% endtabs %} 

## Opening an Encrypted Word document

You can open an existing encrypted Word document from either the file system or the stream by using the following overloads as shown. 

{% tabs %} 

{% highlight c# %}
//Opens an existing encrypted document through constructor of WordDocument class
WordDocument document = new WordDocument(fileName, FormatType.Automatic, "password");
{% endhighlight %}

{% highlight vb.net %}
'Opens an existing encrypted document through constructor of WordDocument class
Dim document As New WordDocument(fileName, FormatType.Automatic, "password")
{% endhighlight %}

{% highlight UWP %}
//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".docx");
//Creates a storage file from FileOpenPicker
StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();
WordDocument document = new WordDocument();
await document.OpenAsync(inputStorageFile, FormatType.Docx, "password");
{% endhighlight %}

{% highlight ASP.NET CORE %}
//DocIO supports Encryption in Windows Forms, WPF, ASP.NET, ASP.NET MVC and UWP platforms alone.
{% endhighlight %}

{% highlight XAMARIN %}
//DocIO supports Encryption in Windows Forms, WPF, ASP.NET, ASP.NET MVC and UWP platforms alone.
{% endhighlight %} 

{% endtabs %}  

{% tabs %}  
  
{% highlight c# %}
//Creates an empty Word document instance
WordDocument document = new WordDocument();
//Loads or opens an existing encrypted Word document through Open method of WordDocument class
document.Open(wordDocumentStream, FormatType.Automatic, "password");
{% endhighlight %}

{% highlight vb.net %}
'Creates an empty Word document instance
Dim document As New WordDocument()
'Loads or opens an existing encrypted Word document through Open method of WordDocument class
document.Open(wordDocumentStream, FormatType.Automatic, "password")
{% endhighlight %}

{% highlight UWP %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Creates an empty WordDocument instance
using (WordDocument document = new WordDocument())
{
	//Loads or opens an existing Word document from stream
	Stream inputStream = assembly.GetManifestResourceStream("CreateWordSample.Assets.Test.docx");
	//Loads or opens an existing encrypted Word document through Open method of WordDocument class
	document.Open(inputStream, FormatType.Docx, "password");
}
{% endhighlight %}

{% highlight ASP.NET CORE %}
//DocIO supports Encryption in Windows Forms, WPF, ASP.NET, ASP.NET MVC and UWP platforms alone.
{% endhighlight %}

{% highlight XAMARIN %}
//DocIO supports Encryption in Windows Forms, WPF, ASP.NET, ASP.NET MVC and UWP platforms alone.
{% endhighlight %} 

{% endtabs %}

## Opening the read only Word document

You can open the ready only documents or read only streams using the OpenReadOnly method. If the Word document for reading is opened by any other application such as Microsoft Word, then the same document can be opened using DocIO in ReadOnly mode. The following code sample demonstrates the same.

{% tabs %}  
  
{% highlight c# %}
//Creates an empty WordDocument instance
WordDocument document = new WordDocument();
//Loads or opens an existing word document using read only stream
document.OpenReadOnly("Template.docx", Syncfusion.DocIO.FormatType.Docx);
{% endhighlight %}

{% highlight vb.net %}
'Creates an empty WordDocument instance 
Dim document As WordDocument = New WordDocument
'Loads or opens an existing word document using read only stream
document.OpenReadOnly("Template.docx", Syncfusion.DocIO.FormatType.Docx)
{% endhighlight %}

{% highlight UWP %}
//DocIO supports OpenReadOnly Word documents in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms alone.
{% endhighlight %}

{% highlight ASP.NET CORE %}
//DocIO supports OpenReadOnly Word documents in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms alone.
{% endhighlight %}

{% highlight XAMARIN %}
//DocIO supports OpenReadOnly Word documents in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms alone.
{% endhighlight %} 

{% endtabs %}

You can also open an existing encrypted document in read only mode using the overloads as mentioned below.

{% tabs %}  
  
{% highlight c# %}
//Creates an empty WordDocument instance
WordDocument document = new WordDocument();
//Loads or opens an existing encrypted word document using read only stream
document.OpenReadOnly("Template.docx", Syncfusion.DocIO.FormatType.Docx , "password");
{% endhighlight %}

{% highlight vb.net %}
'Creates an empty WordDocument instance 
Dim document As WordDocument = New WordDocument
'Loads or opens an existing encrypted word document using read only stream
document.OpenReadOnly("Template.docx", Syncfusion.DocIO.FormatType.Docx, "password")
{% endhighlight %}

{% highlight UWP %}
//DocIO supports OpenReadOnly Word documents in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms alone.
{% endhighlight %}

{% highlight ASP.NET CORE %}
//DocIO supports OpenReadOnly Word documents in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms alone.
{% endhighlight %}

{% highlight XAMARIN %}
//DocIO supports OpenReadOnly Word documents in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms alone.
{% endhighlight %} 

{% endtabs %} 

## Saving a Word document to file system

You can save the created or manipulated Word document to file system using `Save` method of `WordDocument` class. When you do not provide the format type, then the document is saved in Word 97-2003 (*.doc) format.

{% tabs %}  

{% highlight c# %}
//Creates an empty WordDocument instance
WordDocument document = new WordDocument();
//opens an existing Word document through Open method of WordDocument class
document.Open(fileName);
//To-Do some manipulation
//To-Do some manipulation
//Saves the document in file system
document.Save(outputFileName, FormatType.Docx);
{% endhighlight %}

{% highlight vb.net %}
'Creates an empty WordDocument instance
Dim document As New WordDocument()
'opens an existing Word document through Open method of WordDocument class
document.Open(fileName)
'To-Do some manipulation
'To-Do some manipulation
'Saves the document in file system
document.Save(outputFileName, FormatType.Docx)
{% endhighlight %}

{% highlight UWP %}
//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".docx");
//Creates a storage file from FileOpenPicker
StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();
WordDocument document = new WordDocument();
await document.OpenAsync(inputStorageFile);
//To-Do some manipulation
//To-Do some manipulation
//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = OutputFileName;
savePicker.FileTypeChoices.Add("Word Documents", new List<string>() { ".docx" });
//Creates a storage file from FileSavePicker
StorageFile outputStorageFile = await savePicker.PickSaveFileAsync();
//Saves changes to the specified storage file
await document.SaveAsAsync(outputStorageFile, FormatType.Docx);
{% endhighlight %}

{% highlight ASP.NET CORE %}
//Open an existing WordDocument
FileStream inputStream = new FileStream(inputFileName, FileMode.Open);
WordDocument document = new WordDocument(inputStream, FormatType.Docx);
//To-Do some manipulation
//To-Do some manipulation
//Saving the Word document
FileStream outputStream = new FileStream("Sample.docx", FileMode.Create, FileAccess.ReadWrite, FileShare.ReadWrite);
document.Save(outputStream, FormatType.Docx);
document.Close();
outputStream.Flush();
outputStream.Dispose();
{% endhighlight %}

{% highlight XAMARIN %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = assembly.GetManifestResourceStream(inputFilePath);
WordDocument document = new WordDocument(inputStream, FormatType.Docx);
//To-Do some manipulation
//To-Do some manipulation
//Saving the Word document
MemoryStream stream = new MemoryStream();
document.Save(stream, FormatType.Docx);
stream.Position = 0;
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
//Closes the document
document.Close();
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin 
{% endhighlight %}

{% endtabs %} 

## Saving a Word document to Stream

You can also save the created or manipulated word document to stream by using overloads of `Save` methods

{% tabs %} 

{% highlight c# %}
//Creates an empty WordDocument instance
WordDocument document = new WordDocument();
//Opens an existing Word document through Open method of WordDocument class
document.Open(fileName);
//To-Do some manipulation
//To-Do some manipulation
//Creates an instance of memory stream
MemoryStream stream = new MemoryStream();
//Saves the document to stream
document.Save(stream, FormatType.Docx);
{% endhighlight %}

{% highlight vb.net %}
'Creates an empty WordDocument instance
Dim document As New WordDocument()
'Opens an existing Word document through Open method of WordDocument class
document.Open(fileName)
'To-Do some manipulation
'To-Do some manipulation
'Creates an instance of memory stream
Dim stream As New MemoryStream()
'Saves the document to stream
document.Save(stream, FormatType.Docx)
{% endhighlight %}

{% highlight UWP %}
//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".docx");
//Creates a storage file from FileOpenPicker
StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();
WordDocument document = new WordDocument();
await document.OpenAsync(inputStorageFile);
//To-Do some manipulation
//To-Do some manipulation
//Creates an instance of memory stream
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight ASP.NET CORE %}
//Creates an empty WordDocument instance
using (WordDocument document = new WordDocument())
{
	//Loads or opens an existing Word document from stream
	FileStream fileStreamPath = new FileStream(@"Data/Hello World.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
	//Loads or opens an existing Word document through Open method of WordDocument class 
	document.Open(fileStreamPath, FormatType.Automatic);
	//To-Do some manipulation
	//To-Do some manipulation
	//Creates an instance of memory stream
	MemoryStream stream = new MemoryStream();
	//Saves the document to stream
	document.Save(stream, FormatType.Docx);
	//Closes the document
	document.Close();
	stream.Position = 0;
	//Download Word document in the browser
	return File(stream, "application/msword", "Result.docx");
}
{% endhighlight %}

{% highlight XAMARIN %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Creates an empty WordDocument instance
using (WordDocument document = new WordDocument())
{
	//Loads or opens an existing Word document from stream
	Stream inputStream = assembly.GetManifestResourceStream("XamarinFormsApp1.Assets.Hello World.docx");
	//Loads or opens an existing Word document through Open method of WordDocument class
	document.Open(inputStream, FormatType.Automatic);
	//To-Do some manipulation
	//To-Do some manipulation
	//Creates an instance of memory stream
	MemoryStream stream = new MemoryStream();
	//Saves the document to stream
	document.Save(stream, FormatType.Docx);
	//Closes the document
	document.Close();
	//Save the stream as a file in the device and invoke it for viewing
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
}
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin 
{% endhighlight %}

{% endtabs %}  

## Sending to a client browser

You can save and send the document to a client browser from a web site or web application by invoking the following shown overload of `Save` method.  This method explicitly makes use of an instance of [HttpResponse](https://msdn.microsoft.com/en-us/library/system.web.httpresponse(v=vs.110).aspx#) as its parameter in order to stream the document to client browser. So this overload is suitable for web application that references System.Web assembly.

{% tabs %}  

{% highlight c# %}
//Creates an empty WordDocument instance
WordDocument document = new WordDocument();
//Opens an existing Word document through Open method of WordDocument class
document.Open(fileName);
//To-Do some manipulation
//To-Do some manipulation
//Creates an instance of memory stream
MemoryStream stream = new MemoryStream();
//Saves the document to stream
document.Save(outputFileName, FormatType.Docx, Response, HttpContentDisposition.Attachment);
{% endhighlight %}

{% highlight vb.net %}
'Creates an empty WordDocument instance
Dim document As New WordDocument()     
'Opens an existing Word document through Open method of WordDocument class
document.Open(fileName)
'To-Do some manipulation
'To-Do some manipulation
'Creates an instance of memory stream
Dim stream As New MemoryStream()
'Saves the document to stream
document.Save(outputFileName, FormatType.Docx, Response, HttpContentDisposition.Attachment)
{% endhighlight %} 

{% highlight UWP %}
//Saving and sending the Word document to a client browser from a web site is suitable for web applications alone.
{% endhighlight %}

{% highlight ASP.NET CORE %}
//Creates a new instance of WordDocument (Empty Word Document)
WordDocument document = new WordDocument();
//Adds new section to the document
IWSection section = document.AddSection();
//Adds new paragraph to the section
IWParagraph paragraph = section.AddParagraph();
//Appends the text to the created paragraph
paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");
MemoryStream stream = new MemoryStream();
//Saves the Word document to  MemoryStream
document.Save(stream, FormatType.Docx);
document.Close();
stream.Position = 0;
//Download Word document in the browser
return File(stream, "application/msword", "Result.docx");
{% endhighlight %}

{% highlight XAMARIN %}
//Saving and sending the Word document to a client browser from a web site is suitable for web applications alone.
{% endhighlight %}

{% endtabs %}  

## Closing a document

Once the document manipulation and save operation are completed, you should close the instance of `WordDocument`, in order to release all the memory consumed by DocIO’s DOM. The following code example illustrates how to close a WordDocument instance.

{% tabs %}  

{% highlight c# %}
//Creates an empty WordDocument instance
WordDocument document = new WordDocument();
//opens an existing word document through Open method of WordDocument class
document.Open(fileName);
//To-Do some manipulation
//To-Do some manipulation
//Creates an instance of memory stream
MemoryStream stream = new MemoryStream();
//Saves the document to stream
document.Save(stream, FormatType.Docx);
//Closes the document
document.Close();
{% endhighlight %}

{% highlight vb.net %}
'creates an empty WordDocument instance
Dim document As New WordDocument()
'opens an existing word document through Open method of WordDocument class
document.Open(fileName)
'To-Do some manipulation
'To-Do some manipulation
'Creates an instance of memory stream
Dim stream As New MemoryStream()
'Saves the document to stream
document.Save(stream, FormatType.Docx)
'Closes the document
document.Close()
{% endhighlight %}

{% highlight UWP %}
//Instantiates the File Picker
FileOpenPicker openPicker = new FileOpenPicker();
openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
openPicker.FileTypeFilter.Add(".docx");
//Creates a storage file from FileOpenPicker
StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();
WordDocument document = new WordDocument();
await document.OpenAsync(inputStorageFile);
//To-Do some manipulation
//To-Do some manipulation
//Creates an instance of memory stream
MemoryStream stream = new MemoryStream();
//Saves the Word file to MemoryStream
await document.SaveAsync(stream, FormatType.Docx);
//Saves the stream as Word file in local machine
Save(stream, "Result.docx");
//Closes the document
document.Close();
//Please refer the below link to save Word document in UWP platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-uwp#save-word-document-in-uwp
{% endhighlight %}

{% highlight ASP.NET CORE %}
//Creates an empty WordDocument instance
using (WordDocument document = new WordDocument())
{
	//Loads or opens an existing Word document from stream
	FileStream fileStreamPath = new FileStream(@"Data/Hello World.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
	//Loads or opens an existing Word document through Open method of WordDocument class 
	document.Open(fileStreamPath, FormatType.Automatic);
	//To-Do some manipulation
	//To-Do some manipulation
	//Creates an instance of memory stream
	MemoryStream stream = new MemoryStream();
	//Saves the document to stream
	document.Save(stream, FormatType.Docx);
	//Closes the document
	document.Close()
	stream.Position = 0;
	//Download Word document in the browser
	return File(stream, "application/msword", "Result.docx");
}
{% endhighlight %}

{% highlight XAMARIN %}
//"App" is the class of Portable project
Assembly assembly = typeof(App).GetTypeInfo().Assembly;
//Creates an empty WordDocument instance
using (WordDocument document = new WordDocument())
{
	//Loads or opens an existing Word document from stream
	Stream inputStream = assembly.GetManifestResourceStream("XamarinFormsApp1.Assets.Hello World.docx");
	//Loads or opens an existing Word document through Open method of WordDocument class
	document.Open(inputStream, FormatType.Automatic);
	//To-Do some manipulation
	//To-Do some manipulation
	//Creates an instance of memory stream
	MemoryStream stream = new MemoryStream();
	//Saves the document to stream
	document.Save(stream, FormatType.Docx);
	//Save the stream as a file in the device and invoke it for viewing
	Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Result.docx", "application/msword", stream);
	//Closes the document
	document.Close();
}
//Please download the helper files from the below link to save the stream as file and open the file for viewing in Xamarin platform
//https://help.syncfusion.com/file-formats/docio/create-word-document-in-xamarin#helper-files-for-xamarin 
{% endhighlight %}

{% endtabs %}