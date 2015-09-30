---
layout: Post
title: Loading & Saving document
description: This section illustrate how to load and save the Word document
platform: FileFormat
control: DocIO
documentation: UG
---
# Loading & saving document

## Opening an existing document

You can open an existing Word document by using either the Open method or the constructor of WordDocument class

{% highlight c# %}
[C#]

//Open an existing document from file system through constructor of WordDocument class

WordDocument document = new WordDocument(fileName);





{% endhighlight %}

{% highlight vbnet %}
[VB]

'Open an existing document from file system through constructor of WordDocument class

Dim document As New WordDocument(fileName)



{% endhighlight %}

{% highlight c# %}
[C#]

//Create an empty Word document instance

WordDocument document = new WordDocument();

//Load or open an existing word document through open method of WordDocument class

document.Open(fileName);





{% endhighlight %}

{% highlight vbnet %}
[VB]

'Create an empty Word document instance

Dim document As New WordDocument()

'Load or open an existing word document through Open method of WordDocument class

document.Open(fileName)



{% endhighlight %}

## Opening an existing document from Stream

You can open an existing document from stream by either using either the overloads of Open methods or the constructor of WordDocument class

{% highlight c# %}
[C#]

//Open an existing document from stream through constructor of WordDocument class

WordDocument document = new WordDocument(wordDocumentStream, FormatType.Automatic);





{% endhighlight %}

{% highlight vbnet %}
[VB]

'Opens an existing document from stream through constructor of WordDocument class

Dim document As New WordDocument(wordDocumentStream, FormatType.Automatic)





{% endhighlight %}

{% highlight c# %}
[C#]

//Create an empty WordDocument instance

WordDocument document = new WordDocument();

//Load or open an existing word document through Open method of WordDocument class

document.Open(wordDocumentStream, FormatType.Automatic);





{% endhighlight %}

{% highlight vbnet %}
[VB]

'Create an empty Wordocument instance

Dim document As New WordDocument()

'Load or open an existing word document through Open method of WordDocument class

document.Open(wordDocumentStream, FormatType.Automatic)





{% endhighlight %}

## Opening an Encrypted Word document

You can open an existing encrypted word document from either the file system or the stream using the following overloads as shown below

{% highlight c# %}
[C#]

//Open an existing encrypted document through constructor of WordDocument class

WordDocument document = new WordDocument(fileName, FormatType.Automatic, "password");



{% endhighlight %}

{% highlight vbnet %}
[VB]

'Open an existing encrypted document through constructor of WordDocument class

Dim document As New WordDocument(fileName, FormatType.Automatic, "password")



{% endhighlight %}

{% highlight c# %}
[C#]

//Create an empty Word document instance

WordDocument document = new WordDocument();

//Load or open an existing encrypted word document through Open method of WordDocument class

document.Open(wordDocumentStream, FormatType.Automatic, "password");





{% endhighlight %}

{% highlight vbnet %}
[VB]

'Create an empty Word document instance

Dim document As New WordDocument()

'Load or open an existing encrypted word document through Open method of WordDocument class

document.Open(wordDocumentStream, FormatType.Automatic, "password")



{% endhighlight %}

## Saving a Word document to file system

You can save the created or manipulated word document to file system using Save method of WordDocument class. If the user does not provide the format type, then the document will be saved in Word 97-2003 (*.doc) format.

{% highlight c# %}
[C#]

//Create an empty WordDocument instance

WordDocument document = new WordDocument();

//open an existing word document through Open method of WordDocument class

document.Open(fileName);

//To-Do some manipulation

//To-Do some manipulation

//Save the document in file system

document.Save(outputFileName, FormatType.Docx);





{% endhighlight %}

{% highlight vbnet %}
[VB]

'Create an empty WordDocument instance

Dim document As New WordDocument()

'open an existing word document through Open method of WordDocument class

document.Open(fileName)

'To-Do some manipulation

'To-Do some manipulation

'Save the document in file system

document.Save(outputFileName, FormatType.Docx)





{% endhighlight %}

## Saving a Word document to Stream

You can also save the created or manipulated word document to stream using overloads of Save methods

{% highlight c# %}
[C#]

//Create an empty WordDocument instance

WordDocument document = new WordDocument();

//Open an existing Word document through Open method of WordDocument class

document.Open(fileName);

//To-Do some manipulation

//To-Do some manipulation

//Creates an instance of memory stream

MemoryStream stream = new MemoryStream();

//Save the document to stream

document.Save(stream, FormatType.Docx);





{% endhighlight %}

{% highlight vbnet %}
[VB]

'Create an empty WordDocument instance

Dim document As New WordDocument()

'Open an existing Word document through Open method of WordDocument class

document.Open(fileName)

'To-Do some manipulation

'To-Do some manipulation

'Creates an instance of memory stream

Dim stream As New MemoryStream()

'Save the document to stream

document.Save(stream, FormatType.Docx)



{% endhighlight %}

## Sending to a client browser

You can save & send the document to a client browser from a web site or web application by invoking the below shown overload of Save method.  This method explicitly make use of an instance of [HttpResponse](https://msdn.microsoft.com/en-us/library/system.web.httpresponse(v=vs.110).aspx# "") as its parameter in order to stream the document to client browser. So this overload is suitable for web application which references System.Web assembly.

{% highlight c# %}
[C#]

//Create an empty WordDocument instance

WordDocument document = new WordDocument();

//Open an existing Word document through Open method of WordDocument class

document.Open(fileName);

//To-Do some manipulation

//To-Do some manipulation

//Creates an instance of memory stream

MemoryStream stream = new MemoryStream();

//Save the document to stream

document.Save(outputFileName, FormatType.Docx, Response, HttpContentDisposition.Attachment);





{% endhighlight %}

{% highlight vbnet %}
[VB]

'Create an empty WordDocument instance

Dim document As New WordDocument()     

'Opens an existing Word document through Open method of WordDocument class

document.Open(fileName)

'To-Do some manipulation

'To-Do some manipulation

'Create an instance of memory stream

Dim stream As New MemoryStream()

'Save the document to stream

document.Save(outputFileName, FormatType.Docx, Response, HttpContentDisposition.Attachment)





{% endhighlight %}

## Closing a document

Once after the document manipulation and save operation are completed, yoou should close the instance of WordDocument, in order to release all the memory consumed by DocIO’s DOM. The following code snippet illustrates how to close a WordDocument instance.

{% highlight c# %}
[C#]

//Create an empty WordDocument instance

WordDocument document = new WordDocument();

//opens an existing word document through Open method of WordDocument class

document.Open(fileName);

//To-Do some manipulation

//To-Do some manipulation

//Create an instance of memory stream

MemoryStream stream = new MemoryStream();

//Save the document to stream

document.Save(stream, FormatType.Docx);

//Close the document

document.Close();





{% endhighlight %}

{% highlight vbnet %}
[VB]

'creates an empty WordDocument instance

Dim document As New WordDocument()

'opens an existing word document through Open method of WordDocument class

document.Open(fileName)

'To-Do some manipulation

'To-Do some manipulation

'Creates an instance of memory stream

Dim stream As New MemoryStream()

'Save the document to stream

document.Save(stream, FormatType.Docx)

'Closes the document

document.Close()



{% endhighlight %}

