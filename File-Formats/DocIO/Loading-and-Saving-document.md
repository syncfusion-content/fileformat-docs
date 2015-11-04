---
title: Loading & Saving document
description: This section illustrate how to load and save the Word document
platform: file-formats
control: DocIO
documentation: UG
---
# Loading & saving document

## Opening an existing document

You can open an existing Word document by using either the Open method or the constructor of WordDocument class

{% tabs %}  

{% highlight c# %}


//Opens an existing document from file system through constructor of WordDocument class

WordDocument document = new WordDocument(fileName);





{% endhighlight %}

{% highlight vb.net %}


'Opens an existing document from file system through constructor of WordDocument class

Dim document As New WordDocument(fileName)



{% endhighlight %}

 {% endtabs %} 

 {% tabs %}  
 
{% highlight c# %}


//Creates an empty Word document instance

WordDocument document = new WordDocument();

//Loads or opens an existing word document through open method of WordDocument class

document.Open(fileName);





{% endhighlight %}

{% highlight vb.net %}


'Creates an empty Word document instance

Dim document As New WordDocument()

'Loads or opens an existing word document through Open method of WordDocument class

document.Open(fileName)

{% endhighlight %}



{% endtabs %}  



## Opening an existing document from Stream

You can open an existing document from stream by using either the overloads of Open methods or the constructor of WordDocument class

{% tabs %}  

{% highlight c# %}


//Opens an existing document from stream through constructor of WordDocument class

WordDocument document = new WordDocument(wordDocumentStream, FormatType.Automatic);


{% endhighlight %}

{% highlight vb.net %}


'Opens an existing document from stream through constructor of WordDocument class

Dim document As New WordDocument(wordDocumentStream, FormatType.Automatic)



{% endhighlight %}

{% endtabs %}  

{% tabs %}   

{% highlight c# %}


//Creates an empty WordDocument instance

WordDocument document = new WordDocument();

//Loads or opens an existing word document through Open method of WordDocument class

document.Open(wordDocumentStream, FormatType.Automatic);





{% endhighlight %}

{% highlight vb.net %}


'Creates an empty Wordocument instance

Dim document As New WordDocument()

'Loads or opens an existing word document through Open method of WordDocument class

document.Open(wordDocumentStream, FormatType.Automatic)


{% endhighlight %}


{% endtabs %} 


## Opening an Encrypted Word document

You can open an existing encrypted word document from either the file system or the stream by using the following overloads as shown. 

{% tabs %} 

{% highlight c# %}


//Opens an existing encrypted document through constructor of WordDocument class

WordDocument document = new WordDocument(fileName, FormatType.Automatic, "password");



{% endhighlight %}

{% highlight vb.net %}


'Opens an existing encrypted document through constructor of WordDocument class

Dim document As New WordDocument(fileName, FormatType.Automatic, "password")

{% endhighlight %} 

  {% endtabs %}  

  {% tabs %}  
  
{% highlight c# %}


//Creates an empty Word document instance

WordDocument document = new WordDocument();

//Loads or opens an existing encrypted word document through Open method of WordDocument class

document.Open(wordDocumentStream, FormatType.Automatic, "password");





{% endhighlight %}

{% highlight vb.net %}


'Creates an empty Word document instance

Dim document As New WordDocument()

'Loads or opens an existing encrypted word document through Open method of WordDocument class

document.Open(wordDocumentStream, FormatType.Automatic, "password")

{% endhighlight %} 

 {% endtabs %}  

## Saving a Word document to file system

You can save the created or manipulated word document to file system using Save method of WordDocument class. When you do not provide the format type, then the document is saved in Word 97-2003 (*.doc) format.

{% tabs %}  

{% highlight c# %}


//Creates an empty WordDocument instance

WordDocument document = new WordDocument();

//opens an existing word document through Open method of WordDocument class

document.Open(fileName);

//To-Do some manipulation

//To-Do some manipulation

//Saves the document in file system

document.Save(outputFileName, FormatType.Docx);





{% endhighlight %}

{% highlight vb.net %}


'Creates an empty WordDocument instance

Dim document As New WordDocument()

'opens an existing word document through Open method of WordDocument class

document.Open(fileName)

'To-Do some manipulation

'To-Do some manipulation

'Saves the document in file system

document.Save(outputFileName, FormatType.Docx)


{% endhighlight %}


   {% endtabs %} 

   
   
## Saving a Word document to Stream

You can also save the created or manipulated word document to stream by using overloads of Save methods

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

 {% endtabs %}  

## Sending to a client browser

You can save and send the document to a client browser from a web site or web application by invoking the following shown overload of Save method.  This method explicitly makes use of an instance of [HttpResponse](https://msdn.microsoft.com/en-us/library/system.web.httpresponse(v=vs.110).aspx#) as its parameter in order to stream the document to client browser. So this overload is suitable for web application that references System.Web assembly.

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


 {% endtabs %}  

 
 
## Closing a document

Once the document manipulation and save operation are completed, you should close the instance of WordDocument, in order to release all the memory consumed by DocIO’s DOM. The following code example illustrates how to close a WordDocument instance.

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

{% endtabs %}  