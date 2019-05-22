---
title: Word file format conversions | DocIO | Syncfusion
description: Word file format conversions supported in DocIO
platform: file-formats
control: DocIO
documentation: UG
---


## Word File Formats

The [Microsoft Word's](https://en.wikipedia.org/wiki/Microsoft_Word#) native file formats are DOC, DOCX, RTF, DOT, DOTX, DOCM, and DOTM. The Essential DocIO supports the following major native file formats.

1. Word Open XML formats (2007 & later)
2. Word Processing XML (.xml)
3. Word Binary (97-2003) format (classic)

## Word Open XML formats (2007 & later)

[Office Open XML](http://en.wikipedia.org/wiki/Office_Open_XML#) (OOXML or Microsoft Open XML (MOX)) is a zipped, new XML-based file format introduced by Microsoft in Office 2007 applications. WordprocessingML is the markup language used by Microsoft Office Word to store its DOCX documents.

DocIO supports the following WordprocessingML:

* Microsoft Word 2007
* Microsoft Word 2010
* Microsoft Word 2013
* Microsoft Word 2016

The following code example explains how to create a new Word document with few lines of code.

{% tabs %}
{% highlight c# %}
//Creates an instance of WordDocument Instance (Empty Word Document)

WordDocument document = new WordDocument();

//Add a section & a paragraph in the empty document

document.EnsureMinimal();

//Append text to the last paragraph of the document

document.LastParagraph.AppendText("Hello World");

//Save and close the Word document

document.Save("Result.docx");

document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Creates an instance of WordDocument Instance (Empty Word Document)

Dim document As New WordDocument()

'Add a section & a paragraph in the empty document

document.EnsureMinimal()

'Append text to the last paragraph of the document

document.LastParagraph.AppendText("Hello World")

'Save and close the Word document

document.Save("Result.docx")

document.Close()
{% endhighlight %}

{% highlight ASP.NET CORE %}

//Creates a new instance of WordDocument (Empty Word Document)

using (WordDocument document = new WordDocument())

{

//Adds a section and a paragraph to the document

document.EnsureMinimal();

//Appends text to the last paragraph of the document

document.LastParagraph.AppendText("Hello World");

MemoryStream stream = new MemoryStream();

//Saves and closes the destination document to  MemoryStream

document.Save(stream, FormatType.Docx);

document.Close();

stream.Position = 0;

//Download Word document in the browser

return File(stream, "application/msword", "Result.docx");

}

{% endhighlight %}

{% highlight UWP %}

using (WordDocument document = new WordDocument())

{

//Adds a section and a paragraph to the document

document.EnsureMinimal();
 
//Appends text to the last paragraph of the document

document.LastParagraph.AppendText("Hello World");
 
MemoryStream stream = new MemoryStream();

//Saves the Word file to MemoryStream

await document.SaveAsync(stream, FormatType.Docx);

//Saves the stream as Word file in local machine

Save(stream, "Result.docx");

document.Close();

}

// Saves the Word document
async void Save(MemoryStream streams, string filename)

{

streams.Position = 0;

StorageFile stFile;

if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))

{

FileSavePicker savePicker = new FileSavePicker();

savePicker.DefaultFileExtension = ".docx";

savePicker.SuggestedFileName = filename;

savePicker.FileTypeChoices.Add("Word Documents", new List<string>() {".docx"});

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

{% highlight Xamarin %}

//Creates a new instance of WordDocument (Empty Word Document)

using (WordDocument document = new WordDocument())

{

//Adds a section and a paragraph to the document

document.EnsureMinimal();
 
//Appends text to the last paragraph of the document

document.LastParagraph.AppendText("Hello World");

MemoryStream stream = new MemoryStream();

document.Save(stream, FormatType.Docx);
                
//Save the stream as a file in the device and invoke it for viewing
                
Xamarin.Forms.DependencyService.Get<ISave>()
                    .SaveAndView("Result.docx", "application/msword", stream);

//Closes the document              

document.Close();

}

{% endhighlight %}

{% endtabs %}

### Templates

DOTX is a Word document template. The following code snippet shows how to create the Word document template with few lines of code.

{% tabs %}
{% highlight c# %}
//Creates an instance of WordDocument Instance (Empty Word Document)

WordDocument document = new WordDocument();

//Add a section & a paragraph in the empty document

document.EnsureMinimal();

//Append text to the last paragraph of the document

document.LastParagraph.AppendText("Hello World");

//Save and close the Word document

document.Save("Result.dotx");

document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Creates an instance of WordDocument Instance (Empty Word Document)

Dim document As New WordDocument()

'Add a section & a paragraph in the empty document

document.EnsureMinimal()

'Append text to the last paragraph of the document

document.LastParagraph.AppendText("Hello World")

'Save and close the Word document

document.Save("Result.dotx")

document.Close()
{% endhighlight %}

{% highlight ASP.NET CORE %}

//Creates a new instance of WordDocument (Empty Word Document)

using (WordDocument document = new WordDocument())

{

//Adds a section and a paragraph to the document

document.EnsureMinimal();

//Appends text to the last paragraph of the document

document.LastParagraph.AppendText("Hello World");

MemoryStream stream = new MemoryStream();

//Saves and closes the destination document to  MemoryStream

document.Save(stream, FormatType.Dotx);

document.Close();

stream.Position = 0;

//Download Word document in the browser

return File(stream, "application/msword", "Result.dotx");

}

{% endhighlight %}

{% highlight UWP %}

using (WordDocument document = new WordDocument())

{

//Adds a section and a paragraph to the document

document.EnsureMinimal();
 
//Appends text to the last paragraph of the document

document.LastParagraph.AppendText("Hello World");
 
MemoryStream stream = new MemoryStream();

//Saves the Word file to MemoryStream

await document.SaveAsync(stream, FormatType.Docx);

//Saves the stream as Word file in local machine

Save(stream, "Result.dotx");

document.Close();

}

// Saves the Word document
async void Save(MemoryStream streams, string filename)

{

streams.Position = 0;

StorageFile stFile;

if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))

{

FileSavePicker savePicker = new FileSavePicker();

savePicker.DefaultFileExtension = ".dotx";

savePicker.SuggestedFileName = filename;

savePicker.FileTypeChoices.Add("Word Documents", new List<string>() {".dotx"});

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

{% highlight Xamarin %}

//Creates a new instance of WordDocument (Empty Word Document)

using (WordDocument document = new WordDocument())

{

//Adds a section and a paragraph to the document

document.EnsureMinimal();
 
//Appends text to the last paragraph of the document

document.LastParagraph.AppendText("Hello World");

MemoryStream stream = new MemoryStream();

document.Save(stream, FormatType.Dotx);
                
//Save the stream as a file in the device and invoke it for viewing
                
Xamarin.Forms.DependencyService.Get<ISave>()
                    .SaveAndView("Result.dotx", "application/msword", stream);

//Closes the document              

document.Close();

}

{% endhighlight %}

{% endtabs %}

### Macros

DOCM is a macro enabled Word document. It is same as DOCX document contains macros and scripts. The DocIO provides only preservation support for macros. The following code illustrates how to load and save a macro enabled document using the DocIO library.

{% tabs %}
{% highlight c# %}
// Loads the macro-enabled template.

WordDocument document = new WordDocument("Template.dotm");

// Gets the table

DataTable table = GetDataTable();

// Executes Mail Merge with groups.

document.MailMerge.ExecuteGroup(table);

//Saves and closes the document

document.Save("Sample.docm", FormatType.Word2013Docm);

document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Loads the macro-enabled template.

Dim document As New WordDocument("Template.dotm")

'Gets the table

Dim table As DataTable = GetDataTable()

'Executes Mail Merge with groups.

document.MailMerge.ExecuteGroup(table)

'Saves and closes the document

document.Save("Sample.docm", FormatType.Word2013Docm)

document.Close()
{% endhighlight %}

{% highlight ASP.NET CORE %}

FileStream fileStreamPath = new FileStream(@"Data/Template.dotm", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);

//Opens an existing document from file system through constructor of WordDocument class

using (WordDocument document = new WordDocument(fileStreamPath, FormatType.Dotm))

{
// Gets the table

DataTable table = GetDataTable();

// Executes Mail Merge with groups.

document.MailMerge.ExecuteGroup(table);

MemoryStream stream = new MemoryStream();

document.Save(stream, FormatType.Word2013Docm);

//Closes the Word document

document.Close();

stream.Position = 0;

//Download Word document in the browser

return File(stream, "application/msword", "Result.docm");

}


{% endhighlight %}

{% highlight UWP %}

//"App" is the class of Portable project.

Assembly assembly = typeof(App).GetTypeInfo().Assembly;

//Opens an existing document from file system through constructor of WordDocument class

using (WordDocument document = new WordDocument((assembly.GetManifestResourceStream("CreateWordSample.Assets.Test.dotm")),
              FormatType.Dotm))
{

// Gets the table

DataTable table = GetDataTable();

// Executes Mail Merge with groups.

document.MailMerge.ExecuteGroup(table);

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream, FormatType.Word2013Docm);

//Saves the stream as Word file in local machine

Save(stream, "Result.docm");
                
//Closes the Word document

document.Close();

}

// Saves the Word document

async void Save(MemoryStream streams, string filename)

{

streams.Position = 0;

StorageFile stFile;

if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))

{

FileSavePicker savePicker = new FileSavePicker();

savePicker.DefaultFileExtension = ".docm";

savePicker.SuggestedFileName = filename;

savePicker.FileTypeChoices.Add("Word Documents", new List<string>() {".docm"});

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

}

}

{% endhighlight %}

{% highlight Xamarin %}

Assembly assembly = typeof(App).GetTypeInfo().Assembly;

//Opens an existing document from file system through constructor of WordDocument class

using (WordDocument document = new WordDocument((assembly.GetManifestResourceStream("XamarinFormsApp1.Assets.Hello World.dotm")),
              FormatType.Automatic))
{

// Gets the table

DataTable table = GetDataTable();

// Executes Mail Merge with groups.

document.MailMerge.ExecuteGroup(table);

MemoryStream stream = new MemoryStream();

document.Save(stream, FormatType.Word2013Docm);

//Save the stream as a file in the device and invoke it for viewing

Xamarin.Forms.DependencyService.Get<ISave>()
                    .SaveAndView("Result.docm", "application/msword", stream);

//Closes the Word document

document.Close();

}

{% endhighlight %}

{% endtabs %}



## Word Processing XML (.xml)

The XML format introduced in Microsoft Word 2003 was a simple, XML-based format called WordprocessingML or WordML.
The Essential DocIO supports converting the Word document into Word Processing XML document and vice versa.

N> 1. Importing and exporting the Word Processing 2007 XML documents is supported.
N> 2. Exporting the Word Processing 2003 XML document is not supported. Whereas you can import the Word Processing 2003 XML documents and export it to other supported file formats.
N> 3. The custom XML elements present in the Word Processing 2003 XML documents will be removed automatically while importing, like latest Microsoft Word. The custom XML element is a depreciated feature in latest Microsoft Word.

The following code example shows how to convert the Word document into Word Processing XML document.

{% tabs %}
{% highlight c# %}
//Loads an existing Word document

WordDocument document = new WordDocument("Template.docx");

//Saves the document as Word Processing ML document

document.Save("WordToWordML.xml", FormatType.WordML);

//Closes the document

document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Loads an existing Word document 

Dim document As New WordDocument("Template.docx")

'Saves the document as Word Processing ML document

document.Save("WordToWordML.xml", FormatType.WordML)

'Closes the document

document.Close()
{% endhighlight %}

{% highlight ASP.NET CORE %}

FileStream fileStreamPath = new FileStream(@"Data/Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);

//Opens an existing document from file system through constructor of WordDocument class

using (WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx))

{

MemoryStream stream = new MemoryStream();

document.Save(stream, FormatType.WordML);

//Closes the Word document

document.Close();

stream.Position = 0;

//Download Word document in the browser

return File(stream, "application/msword", "WordToWordML.xml");

}

{% endhighlight %}

{% highlight UWP %}

//"App" is the class of Portable project.

Assembly assembly = typeof(App).GetTypeInfo().Assembly;

//Opens an existing document from file system through constructor of WordDocument class

using (WordDocument document = new WordDocument((assembly.GetManifestResourceStream("CreateWordSample.Assets.Test.docx")),
              FormatType.Docx))
{

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream, FormatType.WordML);

//Saves the stream as Word file in local machine

Save(stream, "WordToWrodML.xml");
                
//Closes the Word document

document.Close();

}

// Saves the Word document

async void Save(MemoryStream streams, string filename)

{

streams.Position = 0;

StorageFile stFile;

if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))

{

FileSavePicker savePicker = new FileSavePicker();

savePicker.DefaultFileExtension = ".xml";

savePicker.SuggestedFileName = filename;

savePicker.FileTypeChoices.Add("Word Documents", new List<string>() {".xml"});

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

}

}

{% endhighlight %}

{% highlight Xamarin %}

Assembly assembly = typeof(App).GetTypeInfo().Assembly;

//Opens an existing document from file system through constructor of WordDocument class

using (WordDocument document = new WordDocument((assembly.GetManifestResourceStream("XamarinFormsApp1.Assets.Hello World.docx")),
              FormatType.Docx))
{

MemoryStream stream = new MemoryStream();

document.Save(stream, FormatType.WordML);

//Save the stream as a file in the device and invoke it for viewing

Xamarin.Forms.DependencyService.Get<ISave>()
                    .SaveAndView("WordToWordML.xml", "application/msword", stream);

//Closes the Word document

document.Close();

}

{% endhighlight %}

{% endtabs %}

The following code example shows how to convert the Word Processing XML document into Word document.

{% tabs %}
{% highlight c# %}
// Loads an existing Word document 

WordDocument document = new WordDocument("Template.xml");

//Saves the Word Processing ML document as docx

document.Save("WordMLToWord.docx", FormatType.Docx);

//Closes the document

document.Close();
{% endhighlight %}

{% highlight vb.net %}
' Loads an existing Word document 

Dim document As New WordDocument("Template.xml")

'Saves the Word Processing ML document as docx 

document.Save("WordMLToWord.docx", FormatType.Docx)

'Closes the document

document.Close()
{% endhighlight %}

{% highlight ASP.NET CORE %}

FileStream fileStreamPath = new FileStream(@"Data/Template.xml", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);

//Opens an existing document from file system through constructor of WordDocument class

using (WordDocument document = new WordDocument(fileStreamPath, FormatType.WordML))

{

MemoryStream stream = new MemoryStream();

document.Save(stream, FormatType.Docx);

//Closes the Word document

document.Close();

stream.Position = 0;

//Download Word document in the browser

return File(stream, "application/msword", "WordMLToWord.docx");

}



{% endhighlight %}

{% highlight UWP %}

//"App" is the class of Portable project.

Assembly assembly = typeof(App).GetTypeInfo().Assembly;

//Opens an existing document from file system through constructor of WordDocument class

using (WordDocument document = new WordDocument((assembly.GetManifestResourceStream("CreateWordSample.Assets.Test.xml")),
              FormatType.WordML))
{

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream, FormatType.Docx);

//Saves the stream as Word file in local machine

Save(stream, "WordMLToWord.docx");
                
//Closes the Word document

document.Close();

}

// Saves the Word document

async void Save(MemoryStream streams, string filename)

{

streams.Position = 0;

StorageFile stFile;

if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))

{

FileSavePicker savePicker = new FileSavePicker();

savePicker.DefaultFileExtension = ".docx";

savePicker.SuggestedFileName = filename;

savePicker.FileTypeChoices.Add("Word Documents", new List<string>() {".docx"});

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

}

}

{% endhighlight %}

{% highlight Xamarin %}

Assembly assembly = typeof(App).GetTypeInfo().Assembly;

//Opens an existing document from file system through constructor of WordDocument class

using (WordDocument document = new WordDocument((assembly.GetManifestResourceStream("XamarinFormsApp1.Assets.Hello World.xml")),
              FormatType.WordML))
{

MemoryStream stream = new MemoryStream();

document.Save(stream, FormatType.Docx);

//Save the stream as a file in the device and invoke it for viewing

Xamarin.Forms.DependencyService.Get<ISave>()
                    .SaveAndView("WordMLToWord.docx", "application/msword", stream);

//Closes the Word document

document.Close();

}

{% endhighlight %}

{% endtabs %}

### Unsupported elements in Word to Word Processing XML conversion:

The following table contains list of unsupported elements in Word to Word Processing XML conversion.

<table>
<thead> 
<tr>
<th>Element</th>
<th>Limitations or Unsupported elements</th>
</tr>
</thead>
<tr>
<td>
Custom Shapes and Grouped Shapes<br/><br/></td>
<td>
Not supported<br/><br/></td>
</tr>
<tr>
<td>
Embedded fonts<br/><br/></td>
<td>
Not supported<br/><br/></td>
</tr>
<tr>
<td>
Equation<br/><br/></td>
<td>
Not supported<br/><br/></td>
</tr>
<tr>
<td>
SmartArt<br/><br/></td>
<td>
Not supported<br/><br/></td>
</tr>
<tr>
<td>
WordArt<br/><br/></td>
<td>
Not supported<br/><br/></td>
</tr>
<tr>
<td>
Form Fields
</td>
<td>
Unparsed in Word Processing 2003 XML document.
</td>
</tr>
<tr>
<td>
Ole Object
</td>
<td>
Unparsed in Word Processing 2003 XML document.
</td>
</tr>
</table>

## Word Binary (97-2003) format

DOC is one of the classic file format of Word processing document. It is a proprietary binary format of Microsoft used in all the Microsoft Word versions.

The DocIO library supports importing or exporting of DOC format and refer to the following code sample.

{% tabs %}
{% highlight c# %}
//Creates an instance of WordDocument Instance (Empty Word Document)

WordDocument document = new WordDocument();

//Add a section & a paragraph in the empty document

document.EnsureMinimal();

//Append text to the last paragraph of the document

document.LastParagraph.AppendText("Hello World");

//Save and close the Word document

document.Save("BinaryDocument.doc");

document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Creates an instance of WordDocument Instance (Empty Word Document)

Dim document As New WordDocument()

'Add a section & a paragraph in the empty document

document.EnsureMinimal()

'Append text to the last paragraph of the document

document.LastParagraph.AppendText("Hello World")

'Save and close the Word document

document.Save("BinaryDocument.doc ")

document.Close()
{% endhighlight %}

{% highlight ASP.NET CORE %}

//Creates a new instance of WordDocument (Empty Word Document)

using (WordDocument document = new WordDocument())

{

//Adds a section and a paragraph to the document

document.EnsureMinimal();

//Appends text to the last paragraph of the document

document.LastParagraph.AppendText("Hello World");

MemoryStream stream = new MemoryStream();

//Saves and closes the destination document to  MemoryStream

document.Save(stream, FormatType.Doc);

document.Close();

stream.Position = 0;

//Download Word document in the browser

return File(stream, "application/msword", "Result.doc");

}

{% endhighlight %}

{% highlight UWP %}

using (WordDocument document = new WordDocument())

{

//Adds a section and a paragraph to the document

document.EnsureMinimal();
 
//Appends text to the last paragraph of the document

document.LastParagraph.AppendText("Hello World");
 
MemoryStream stream = new MemoryStream();

//Saves the Word file to MemoryStream

await document.SaveAsync(stream, FormatType.Doc);

//Saves the stream as Word file in local machine

Save(stream, "Result.doc");

document.Close();

}

// Saves the Word document
async void Save(MemoryStream streams, string filename)

{

streams.Position = 0;

StorageFile stFile;

if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))

{

FileSavePicker savePicker = new FileSavePicker();

savePicker.DefaultFileExtension = ".doc";

savePicker.SuggestedFileName = filename;

savePicker.FileTypeChoices.Add("Word Documents", new List<string>() {".doc"});

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

{% highlight Xamarin %}

//Creates a new instance of WordDocument (Empty Word Document)

using (WordDocument document = new WordDocument())

{

//Adds a section and a paragraph to the document

document.EnsureMinimal();
 
//Appends text to the last paragraph of the document

document.LastParagraph.AppendText("Hello World");

MemoryStream stream = new MemoryStream();

document.Save(stream, FormatType.Doc);
                
//Save the stream as a file in the device and invoke it for viewing
                
Xamarin.Forms.DependencyService.Get<ISave>()
                    .SaveAndView("Result.doc", "application/msword", stream);

//Closes the document              

document.Close();

}

{% endhighlight %}
{% endtabs %}

### DOC to DOCX and DOCX to DOC
The following code shows, how to convert the DOC file into DOCX file format using DocIO

{% tabs %}
{% highlight c# %}
//Loads an existing document

WordDocument document = new WordDocument("Sample.doc", FormatType.Doc);

//Saves the binary document(.doc) as Word Document(.docx) file

document.Save("DocToWord.docx", FormatType.Docx);

//Closes the document

document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Loads an existing document

Dim document As New WordDocument("Sample.doc", FormatType.Doc)

' Saves the binary document(.doc) as Word Document(.docx) file

document.Save("DocToWord.docx", FormatType.Docx)

'Closes the document

document.Close()
{% endhighlight %}
{% highlight ASP.NET CORE %}

FileStream fileStreamPath = new FileStream(@"Data/Template.doc", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);

//Opens an existing document from file system through constructor of WordDocument class

using (WordDocument document = new WordDocument(fileStreamPath, FormatType.Doc))

{

MemoryStream stream = new MemoryStream();

document.Save(stream, FormatType.Docx);

//Closes the Word document

document.Close();

stream.Position = 0;

//Download Word document in the browser

return File(stream, "application/msword", "DocToWord.docx");

}



{% endhighlight %}

{% highlight UWP %}

//"App" is the class of Portable project.

Assembly assembly = typeof(App).GetTypeInfo().Assembly;

//Opens an existing document from file system through constructor of WordDocument class

using (WordDocument document = new WordDocument((assembly.GetManifestResourceStream("CreateWordSample.Assets.Test.doc")),
              FormatType.Doc))
{

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream, FormatType.Docx);

//Saves the stream as Word file in local machine

Save(stream, "DocToWord.docx");
                
//Closes the Word document

document.Close();

}

// Saves the Word document

async void Save(MemoryStream streams, string filename)

{

streams.Position = 0;

StorageFile stFile;

if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))

{

FileSavePicker savePicker = new FileSavePicker();

savePicker.DefaultFileExtension = ".docx";

savePicker.SuggestedFileName = filename;

savePicker.FileTypeChoices.Add("Word Documents", new List<string>() {".docx"});

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

}

}

{% endhighlight %}

{% highlight Xamarin %}

Assembly assembly = typeof(App).GetTypeInfo().Assembly;

//Opens an existing document from file system through constructor of WordDocument class

using (WordDocument document = new WordDocument((assembly.GetManifestResourceStream("XamarinFormsApp1.Assets.Hello World.doc")),
              FormatType.Doc))
{

MemoryStream stream = new MemoryStream();

document.Save(stream, FormatType.Docx);

//Save the stream as a file in the device and invoke it for viewing

Xamarin.Forms.DependencyService.Get<ISave>()
                    .SaveAndView("DocToWord.docx", "application/msword", stream);

//Closes the Word document

document.Close();

}

{% endhighlight %}

{% endtabs %}
The following code shows, how to convert the DOCX file into DOC file format using DocIO

{% tabs %}
{% highlight c# %}
//Loads an existing document

WordDocument document = new WordDocument("Sample.docx", FormatType.Docx);

//Saves the Word Document(.docx) as binary document(.doc) file

document.Save("DocxToBinary.doc", FormatType.Doc);

//Closes the document

document.Close();
{% endhighlight %}

{% highlight vb.net %}
'Loads an existing document

Dim document As New WordDocument("Sample.docx", FormatType.Docx)

' Saves the Word Document(.docx) as binary document(.doc) file 

document.Save("DocxToBinary.doc", FormatType.Doc)

'Closes the document

document.Close()
{% endhighlight %}

{% highlight ASP.NET CORE %}

FileStream fileStreamPath = new FileStream(@"Data/Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);

//Opens an existing document from file system through constructor of WordDocument class

using (WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx))

{

MemoryStream stream = new MemoryStream();

document.Save(stream, FormatType.Doc);

//Closes the Word document

document.Close();

stream.Position = 0;

//Download Word document in the browser

return File(stream, "application/msword", "DocxToBinary.doc");

}



{% endhighlight %}

{% highlight UWP %}

//"App" is the class of Portable project.

Assembly assembly = typeof(App).GetTypeInfo().Assembly;

//Opens an existing document from file system through constructor of WordDocument class

using (WordDocument document = new WordDocument((assembly.GetManifestResourceStream("CreateWordSample.Assets.Test.docx")),
              FormatType.Docx))
{

MemoryStream stream = new MemoryStream();

await document.SaveAsync(stream, FormatType.Doc);

//Saves the stream as Word file in local machine

Save(stream, "DocxToBinary.doc");
                
//Closes the Word document

document.Close();

}

// Saves the Word document

async void Save(MemoryStream streams, string filename)

{

streams.Position = 0;

StorageFile stFile;

if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))

{

FileSavePicker savePicker = new FileSavePicker();

savePicker.DefaultFileExtension = ".doc";

savePicker.SuggestedFileName = filename;

savePicker.FileTypeChoices.Add("Word Documents", new List<string>() {".doc"});

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

}

}

{% endhighlight %}

{% highlight Xamarin %}

Assembly assembly = typeof(App).GetTypeInfo().Assembly;

//Opens an existing document from file system through constructor of WordDocument class

using (WordDocument document = new WordDocument((assembly.GetManifestResourceStream("XamarinFormsApp1.Assets.Hello World.docx")),
              FormatType.Docx))
{

MemoryStream stream = new MemoryStream();

document.Save(stream, FormatType.Doc);

//Save the stream as a file in the device and invoke it for viewing

Xamarin.Forms.DependencyService.Get<ISave>()
                    .SaveAndView("DocxToBinary.doc", "application/msword", stream);

//Closes the Word document

document.Close();

}

{% endhighlight %}

{% endtabs %}

### Open a Word (*.doc) document containing incremental save information

Essential DocIO process the content that are preserved in the last complete save operation alone from a Word (.doc) document and it doesn't process the incremental save information. 
Hence it throws "Complex format is not supported" exception when attempting to open a Word (.doc) document containing incremental save information.

You can open the Word (*.doc) documents containing incremental save information without exception by setting SkipIncrementalSaveValidation property of Settings class as true. 
Whereas the recent changes saved as incremental save information using older Microsoft Word application can't be preserved.

The following code example shows how to open a Word (*.doc) document containing incremental save information without exception.

{% tabs %}  

{% highlight c# %}

//Creates an empty Word document instance

WordDocument document = new WordDocument();

//Sets flag to skip old file format exception while opening document

document.Settings.SkipIncrementalSaveValidation = true;

//Loads or opens an existing incrementally saved DOC format through Open method of WordDocument class

document.Open(fileName);

//Saves the Word Document

document.Save("Result.doc", FormatType.Doc);

//Closes the document

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Creates an empty Word document instance

Dim document As New WordDocument()

'Sets flag to skip old file format exception while opening document

document.Settings.SkipIncrementalSaveValidation = True

'Loads or opens an existing incrementally saved DOC format through Open method of WordDocument class

document.Open(fileName)

' Saves the Word Document

document.Save("Result.doc", FormatType.Doc)

'Closes the document

document.Close()

{% endhighlight %}

{% highlight ASP.NET CORE %}

//Creates a new instance of WordDocument (Empty Word Document)

using (WordDocument document = new WordDocument())

{
//Loads or opens an existing Word document from stream

FileStream fileStreamPath = new FileStream(@"Data/Hello World.doc", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);

//Sets flag to skip old file format exception while opening document

document.Settings.SkipIncrementalSaveValidation = true;

//Loads or opens an existing Word document through Open method of WordDocument class 

document.Open(fileStreamPath, FormatType.Automatic);

MemoryStream stream = new MemoryStream();

//Saves and closes the destination document to  MemoryStream

document.Save(stream, FormatType.Doc);

document.Close();

stream.Position = 0;

//Download Word document in the browser

return File(stream, "application/msword", "Result.doc");

}

{% endhighlight %}

{% highlight UWP %}

//"App" is the class of Portable project.

Assembly assembly = typeof(App).GetTypeInfo().Assembly;

using (WordDocument document = new WordDocument())

{

/Loads or opens an existing Word document from stream

Stream inputStream = assembly.GetManifestResourceStream("CreateWordSample.Assets.Test.doc");

//Sets flag to skip old file format exception while opening document

document.Settings.SkipIncrementalSaveValidation = true;

//Loads or opens an existing Word document through Open method of WordDocument class

document.Open(inputStream, FormatType.Automatic);
 
MemoryStream stream = new MemoryStream();

//Saves the Word file to MemoryStream

await document.SaveAsync(stream, FormatType.Doc);

//Saves the stream as Word file in local machine

Save(stream, "Result.doc");

document.Close();

}

// Saves the Word document
async void Save(MemoryStream streams, string filename)

{

streams.Position = 0;

StorageFile stFile;

if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))

{

FileSavePicker savePicker = new FileSavePicker();

savePicker.DefaultFileExtension = ".doc";

savePicker.SuggestedFileName = filename;

savePicker.FileTypeChoices.Add("Word Documents", new List<string>() {".doc"});

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

{% highlight Xamarin %}

//"App" is the class of Portable project.

Assembly assembly = typeof(App).GetTypeInfo().Assembly;

//Creates a new instance of WordDocument (Empty Word Document)

using (WordDocument document = new WordDocument())

{

//Loads or opens an existing Word document from stream

Stream inputStream = assembly.GetManifestResourceStream("XamarinFormsApp1.Assets.Hello World.doc");

//Sets flag to skip old file format exception while opening document

document.Settings.SkipIncrementalSaveValidation = true;

//Loads or opens an existing Word document through Open method of WordDocument class

document.Open(inputStream, FormatType.Automatic);

MemoryStream stream = new MemoryStream();

document.Save(stream, FormatType.Doc);
                
//Save the stream as a file in the device and invoke it for viewing
                
Xamarin.Forms.DependencyService.Get<ISave>()
                    .SaveAndView("Result.doc", "application/msword", stream);

//Closes the document              

document.Close();

}

{% endhighlight %}

{% endtabs %}  