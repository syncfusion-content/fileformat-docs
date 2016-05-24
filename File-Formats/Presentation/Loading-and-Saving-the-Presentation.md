---
title: Loading and saving the PowerPoint Presentation
description: Loading and saving the Presentation; Modifying the Presentation
platform: file-formats
control: Presentation
documentation: UG
---
# Load and save the Presentation

## Opening an existing Presentation from file system

You can open an existing PowerPoint Presentation by using the file name and its physical path.

{% tabs %}

{% highlight c# %}

//Opens an existing Presentation from file system 

IPresentation presentation = Presentation.Open(fileName);

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing Presentation from file system 

Dim presentationDocument As IPresentation = Presentation.Open(fileName)

{% endhighlight %}

{% endtabs %}

## Opening an existing Presentation from stream

You can open an existing PowerPoint Presentation from stream by using the overloads of Open method.

{% tabs %}

{% highlight c# %}

//Opens an existing Presentation from stream 

IPresentation presentation = Presentation.Open(presentationStream);

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing Presentation from stream 

Dim presentationDocument As IPresentation = Presentation.Open(presentationStream)

{% endhighlight %}

{% endtabs %}

## Opening an encrypted Presentation

You can open an encrypted PowerPoint presentation from either file path or stream by using the following overloads of Open method as follows.

{% tabs %}

{% highlight c# %}

//Opens an existing encrypted Presentation from stream 

IPresentation presentation = Presentation.Open(presentationStream, password);

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing encrypted Presentation from stream 

Dim presentationDocument As IPresentation = Presentation.Open(presentationStream, password)

{% endhighlight %}

{% endtabs %}

{% tabs %}

{% highlight c# %}

//Opens an existing encrypted Presentation from file system 

IPresentation presentation = Presentation.Open(fileName, password);

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing encrypted Presentation from file system 

Dim presentation As IPresentation = Presentation.Open(fileName, password)

{% endhighlight %}

{% endtabs %}

## Saving a PowerPoint Presentation to file system

You can save the created or manipulated PowerPoint Presentation to file system by using Save() method of **IPresentation** interface. Default format type is *.PPTX.

{% tabs %}

{% highlight c# %}

//Opens an existing PowerPoint Presentation 

IPresentation presentation = Presentation.Open(fileName);

//To-Do some manipulation

//To-Do some manipulation

//Saves the Presentation in file system

presentation.Save("Output.pptx");

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing PowerPoint Presentation

Dim presentationDocument As IPresentation = Presentation.Open(fileName)

'To-Do some manipulation

'To-Do some manipulation

'Saves the Presentation in file system

Presentation_1.Save("Output.pptx")

{% endhighlight %}

{% endtabs %}

## Saving a PowerPoint Presentation to stream

You can save the created or manipulated PowerPoint Presentation to stream by using overloads of Save method.

{% tabs %}

{% highlight c# %}

//Opens an existing PowerPoint Presentation 

IPresentation presentation = Presentation.Open(fileName);

//To-Do some manipulation

//To-Do some manipulation

//Creates an instance of memory stream

MemoryStream stream = new MemoryStream();

//Saves the Presentation to stream

presentation.Save(stream);

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing PowerPoint Presentation 

Dim presentationDocument As IPresentation = Presentation.Open(fileName)

'To-Do some manipulation

'To-Do some manipulation

'Creates an instance of memory stream

Dim stream As New MemoryStream()

'Saves the Presentation to stream

Presentation_1.Save(stream)

{% endhighlight %}

{% endtabs %}

## Sending to a client browser

You can save and send the Presentation to a client browser from a website or web application by invoking the overload of Save method. This method explicitly make use of an instance of HttpResponse as its parameter in order to stream the presentation to client browser. So, this overload is suitable for web application that refer to [System.Web](https://msdn.microsoft.com/en-us/library/gg145018(v=vs.110).aspx) assembly.

{% tabs %}

{% highlight c# %}

//Opens an existing PowerPoint Presentation 

IPresentation presentation = Presentation.Open(fileName);

//To-Do some manipulation

//To-Do some manipulation

//Saves the Presentation to the client browser

presentation.Save("Output.pptx", FormatType.Pptx, Response);

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing PowerPoint Presentation 

Dim presentationDocument As IPresentation = Presentation.Open(fileName)

'To-Do some manipulation

'To-Do some manipulation

'Saves the Presentation to the client browser

Presentation_1.Save("Output.pptx", FormatType.Pptx, Response)

{% endhighlight %}

{% endtabs %}

## Closing a PowerPoint Presentation

When you are done with the Presentation instance, you should close the instance of **IPresentation** in order to release the memory consumed by Essential Presentation library. The following code example illustrates how to close an IPresentation instance.

{% tabs %}

{% highlight c# %}

//Opens an existing Presentation from file system 

IPresentation presentation = Presentation.Open(fileName);

//To-Do some manipulation

//To-Do some manipulation

//Creates an instance of memory stream

MemoryStream stream = new MemoryStream();

//Saves the Presentation to stream

presentation.Save(stream);

//Closes the Presentation instance and free the memory consumed.

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing Presentation from file system 

Dim presentationDocument As IPresentation = Presentation.Open(fileName)

'To-Do some manipulation

'To-Do some manipulation

'Creates an instance of memory stream

Dim stream As New MemoryStream()

'Saves the Presentation to stream

presentationDocument.Save(stream)

'Closes the Presentation instance and free the memory consumed.

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}
