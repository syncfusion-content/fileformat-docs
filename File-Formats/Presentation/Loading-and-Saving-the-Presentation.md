---
title: Loading and saving the PowerPoint presentation
description: Loading and saving the presentation; Modifying the presnetation
platform: file-formats
control: Presentation
documentation: UG
---
# Load and save the presentation

## Opening an existing presentation from file system

You can open an existing PowerPoint presentation by using the file name and its physical path.

{% tabs %}

{% highlight c# %}

//Opens an existing presentation from file system 

IPresentation presentation = Presentation.Open(fileName);

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing presentation from file system 

Dim presentationDocument As IPresentation = Presentation.Open(fileName)

{% endhighlight %}

{% endtabs %}

## Opening an existing presentation from stream

You can open an existing PowerPoint presentation from stream by using the overloads of Open method.

{% tabs %}

{% highlight c# %}

//Opens an existing presentation from stream 

IPresentation presentation = Presentation.Open(presentationStream);

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing presentation from stream 

Dim presentationDocument As IPresentation = Presentation.Open(presentationStream)

{% endhighlight %}

{% endtabs %}

## Opening an encrypted presentation

You can open an encrypted PowerPoint presentation from either file path or stream by using the following overloads of Open method as follows.

{% tabs %}

{% highlight c# %}

//Opens an existing encrypted presentation from stream 

IPresentation presentation = Presentation.Open(presentationStream, password);

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing encrypted presentation from stream 

Dim presentationDocument As IPresentation = Presentation.Open(presentationStream, password)

{% endhighlight %}

{% endtabs %}

{% tabs %}

{% highlight c# %}

//Opens an existing encrypted presentation from file system 

IPresentation presentation = Presentation.Open(fileName, password);

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing encrypted presentation from file system 

Dim presentation As IPresentation = Presentation.Open(fileName, password)

{% endhighlight %}

{% endtabs %}

## Saving a PowerPoint presentation to file system

You can save the created or manipulated PowerPoint presentation to file system by using Save() method of **IPresentation** interface. Default format type is *.pptx.

{% tabs %}

{% highlight c# %}

//Opens an existing PowerPoint presentation 

IPresentation presentation = Presentation.Open(fileName);

//To-Do some manipulation

//To-Do some manipulation

//Saves the presentation in file system

presentation.Save("Output.pptx");

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing PowerPoint presentation

Dim presentationDocument As IPresentation = Presentation.Open(fileName)

'To-Do some manipulation

'To-Do some manipulation

'Saves the presentation in file system

Presentation_1.Save("Output.pptx")

{% endhighlight %}

{% endtabs %}

## Saving a PowerPoint presentation to stream

You can save the created or manipulated PowerPoint presentation to stream by using overloads of Save method.

{% tabs %}

{% highlight c# %}

//Opens an existing PowerPoint presentation 

IPresentation presentation = Presentation.Open(fileName);

//To-Do some manipulation

//To-Do some manipulation

//Creates an instance of memory stream

MemoryStream stream = new MemoryStream();

//Saves the presentation to stream

presentation.Save(stream);

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing PowerPoint presentation 

Dim presentationDocument As IPresentation = Presentation.Open(fileName)

'To-Do some manipulation

'To-Do some manipulation

'Creates an instance of memory stream

Dim stream As New MemoryStream()

'Saves the presentation to stream

Presentation_1.Save(stream)

{% endhighlight %}

{% endtabs %}

## Sending to a client browser

You can save and send the presentation to a client browser from a website or web application by invoking the overload of Save method. This method explicitly make use of an instance of HttpResponse as its parameter in order to stream the presentation to client browser. So, this overload is suitable for web application that refer to [System.Web](https://msdn.microsoft.com/en-us/library/gg145018(v=vs.110).aspx) assembly.

{% tabs %}

{% highlight c# %}

//Opens an existing PowerPoint presentation 

IPresentation presentation = Presentation.Open(fileName);

//To-Do some manipulation

//To-Do some manipulation

//Saves the presentation to the client browser

presentation.Save("Output.pptx", FormatType.Pptx, Response);

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing PowerPoint presentation 

Dim presentationDocument As IPresentation = Presentation.Open(fileName)

'To-Do some manipulation

'To-Do some manipulation

'Saves the presentation to the client browser

Presentation_1.Save("Output.pptx", FormatType.Pptx, Response)

{% endhighlight %}

{% endtabs %}

## Closing a PowerPoint presentation

When you are done with the presentation instance, you should close the instance of **IPresentation** in order to release the memory consumed by Essential Presentation library. The following code example illustrates how to close an IPresentation instance.

{% tabs %}

{% highlight c# %}

//Opens an existing presentation from file system 

IPresentation presentation = Presentation.Open(fileName);

//To-Do some manipulation

//To-Do some manipulation

//Creates an instance of memory stream

MemoryStream stream = new MemoryStream();

//Saves the presentation to stream

presentation.Save(stream);

//Closes the presentation instance and free the memory consumed.

presentation.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens an existing presentation from file system 

Dim presentationDocument As IPresentation = Presentation.Open(fileName)

'To-Do some manipulation

'To-Do some manipulation

'Creates an instance of memory stream

Dim stream As New MemoryStream()

'Saves the presentation to stream

presentationDocument.Save(stream)

'Closes the presentation instance and free the memory consumed.

presentationDocument.Close()

{% endhighlight %}

{% endtabs %}
