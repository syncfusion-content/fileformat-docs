---
title: Loading and saving document
description: This secion explains loading and saving a PDF document
platform: file-formats
control: PDF
documentation: UG
---
# Loading & saving document

## Opening an existing PDF document

You can open an existing PDF document by using the PdfLoadedDocument class. The following example shows how to load an existing document from physical path.
{% tabs %}
{% highlight c# %}

//Open an existing document from file system 
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");

{% endhighlight %}

{% highlight vb.net %}

'Open an existing document from file system 
Dim loadedDocument As New PdfLoadedDocument("Input.pdf")

{% endhighlight %}
{% endtabs %}
## Opening an existing PDF document from Stream

You can open an existing document from stream by using PdfLoadedDocument class as shown below
{% tabs %} 
{% highlight c# %}

//Opens an existing document from stream 
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(stream); 

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing document from stream 
Dim loadedDocument As New PdfLoadedDocument(stream)

{% endhighlight %}
{% endtabs %}
## Opening an existing PDF document from byte array

You can open an existing document from byte array by using PdfLoadedDocument class as shown in the below code snippet.
{% tabs %} 
{% highlight c# %}

//Open an existing document from byte array 
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(byteArray); 

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing document from byte array 
Dim loadedDocument As New PdfLoadedDocument(byteArray)

{% endhighlight %}
{% endtabs %}
## Opening an Encrypted PDF document

You can open an existing encrypted PDF document from either the file system or the stream or the byte array using the following overloads as shown below

{% tabs %}
{% highlight c# %}

//Open an existing encrypted document from disk.
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf", "password");

{% endhighlight %}

{% highlight vb.net %}

'Open an existing encrypted document from disk. 
Dim loadedDocument As New PdfLoadedDocument("Input.pdf","password")

{% endhighlight %}
{% endtabs %}

{% tabs %} 
{% highlight c# %}


//Open an existing encrypted document from stream.

PdfLoadedDocument loadedDocument = new PdfLoadedDocument(stream, "password");



{% endhighlight %}

{% highlight vb.net %}

'Open an existing encrypted document from stream.
Dim loadedDocument As New PdfLoadedDocument(stream,"password")

{% endhighlight %}
{% endtabs %}

{% tabs %} 
{% highlight c# %}

//Open an existing encrypted document from byte array. 
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(byteArray, "password");

{% endhighlight %}

{% highlight vb.net %}

'Open an existing encrypted document from byte array. 
Dim loadedDocument As New PdfLoadedDocument(byteArray,"password")

{% endhighlight %}
{% endtabs %}
## Opening a corrupted PDF document

You can open a corrupted PDF document from either the file system or the stream or the byte array using the following overloads as shown below
{% tabs %}
{% highlight c# %}

//Open an existing corrupted document from disk. 
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf", true);

{% endhighlight %}

{% highlight vb.net %}

'Open an existing corrupted document from disk. 
Dim loadedDocument As New PdfLoadedDocument("Input.pdf", True)

{% endhighlight %}
{% endtabs %}

{% tabs %}
{% highlight c# %}

//Open an existing corrupted document from stream. 
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(stream, true);

{% endhighlight %}

{% highlight vb.net %}

'Open an existing corrupted document from stream. 
Dim loadedDocument As New PdfLoadedDocument(stream, True)

{% endhighlight %}
{% endtabs %}

{% tabs %}
{% highlight c# %}

//Open an existing corrupted document from byte array. 
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(byteArray, true);

{% endhighlight %}

{% highlight vb.net %}

'Open an existing corrupted document from byte array. 
Dim loadedDocument As New PdfLoadedDocument(byteArray, True)

{% endhighlight %}
{% endtabs %}
N> Note:

N> 1. The OpenAndRepair overload is capable of resolving basic cross reference offset issues and cannot repair complex document corruption.

N> 2.  Using this overload may cause performance delay when compared with other overloads, due to the repairing process.

## Saving a PDF document to file system

You can save the manipulated PDF document to file system using Save method of PdfLoadedDocument class.

{% tabs %}
{% highlight c# %}

//Load an existing PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");
//To-Do some manipulation
//To-Do some manipulation
//Save the document in file system
loadedDocument.Save("Output.pdf"); 

{% endhighlight %}

{% highlight vb.net %}

' Load an existing PDF document
Dim loadedDocument As New PdfLoadedDocument("Input.pdf")
'To-Do some manipulation
'To-Do some manipulation
'Save the document in file system
loadedDocument.Save("Output.pdf")

{% endhighlight %}
{% endtabs %}

## Saving a PDF document to stream

You can also save the manipulated PDF document to stream using overloads of Save method

{% tabs %}
{% highlight c# %}

//Load an existing PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");
//To-Do some manipulation
//To-Do some manipulation
//Creates an instance of memory stream
MemoryStream stream = new MemoryStream();
//Save the document stream
loadedDocument.Save(stream) ;

{% endhighlight %}

{% highlight vb.net %}

' Load an existing PDF document
Dim loadedDocument As New PdfLoadedDocument("Input.pdf")
'To-Do some manipulation
'To-Do some manipulation
'Creates an instance of memory stream
Dim stream As New MemoryStream()
'Save the document to stream
loadedDocument.Save(stream)

{% endhighlight %}
{% endtabs %}

## Saving a PDF document into the same file or stream

You can also resave the manipulated PDF document to the same file using overloads of Save method

{% tabs %}
{% highlight c# %}

//Load an existing PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");
//To-Do some manipulation
//To-Do some manipulation
//Resave the document to the same file 
loadedDocument.Save() ;


{% endhighlight %}

{% highlight vb.net %}

' Load an existing PDF document
Dim loadedDocument As New PdfLoadedDocument("Input.pdf")
'To-Do some manipulation
'To-Do some manipulation
'Resave the document to the same file 
loadedDocument.Save()

{% endhighlight %}
{% endtabs %}

{% tabs %}
{% highlight c# %}

//Load an existing PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument(stream);
//To-Do some manipulation
//To-Do some manipulation
//Resave the document to the same stream
loadedDocument.Save();

{% endhighlight %}

{% highlight vb.net %}

' Load an existing PDF document
Dim loadedDocument As New PdfLoadedDocument(stream)
'To-Do some manipulation
'To-Do some manipulation
'Resave the document to the same stream
loadedDocument.Save()

{% endhighlight %}
{% endtabs %}
## Closing a document

After the document manipulation and save operation are completed, you should close the instance of PdfLoadedDocument, in order to release all the memory consumed by PDF DOM. The following code snippet illustrates how to close a PdfLoadedDocument instance.

{% tabs %}
{% highlight c# %}

//Load an existing PDF document
PdfLoadedDocument loadedDocument = new PdfLoadedDocument("Input.pdf");
//To-Do some manipulation
//To-Do some manipulation
//Save the document in file system
loadedDocument.Save("Output.pdf"); 
//Close the document
loadedDocument.Close(true);

{% endhighlight %}

{% highlight vb.net %}

' Load an existing PDF document
Dim loadedDocument As New PdfLoadedDocument("Input.pdf")
'To-Do some manipulation
'To-Do some manipulation
'Save the document in file system
loadedDocument.Save("Output.pdf")
'Close the document
loadedDocument.Close(True)

{% endhighlight %}
{% endtabs %}

N> Note: 

N> Close() method will dispose all the memory consumed by PDF DOM.

N> Close(true) method will dispose all the memory consumed by PDF DOM as well as disposes its document stream

