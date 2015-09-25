---
layout: Post
title: Loading and saving the PowerPoint presentation
description: Loading and saving the presentation; Modifying the presnetation
platform: FileFormats
control: Presentation
documentation: UG
---
# Loading & saving the presentation

## Opening an existing presentation from file system

You can open an existing PowerPoint presentation by using the file name and its physical path.

{% highlight c# %}
[C#]

//Open an existing presentation from file system 

IPresentation presentation = Presentation.Open(fileName);



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Open an existing presentation from file system 

Dim presentation_1 As IPresentation = Presentation.Open(fileName)



{% endhighlight %}

## Opening an existing presentation from stream

You can open an existing PowerPoint presentation from stream using the overloads of Open method.

{% highlight c# %}
[C#]

//Opens an existing presentation from stream 

IPresentation presentation = Presentation.Open(presentationStream);



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Opens an existing presentation from stream 

Dim presentation_1 As IPresentation = Presentation.Open(presentationStream)



{% endhighlight %}

## Opening an encrypted presentation

You can open an encrypted PowerPoint presentation from either file path or stream using the following overloads of Open method as shown below

{% highlight c# %}
[C#]

//Open an existing encrypted presentation from stream 

IPresentation presentation = Presentation.Open(presentationStream, password);



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Open an existing encrypted presentation from stream 

Dim presentation_1 As IPresentation = Presentation.Open(presentationStream, password)



{% endhighlight %}

{% highlight c# %}
[C#]

//Open an existing encrypted presentation from file system 

IPresentation presentation = Presentation.Open(fileName, password);



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Open an existing encrypted presentation from file system 

Dim presentation As IPresentation = Presentation.Open(fileName, password)



{% endhighlight %}

## Saving a PowerPoint presentation to file system

You can save the created or manipulated PowerPoint presentation to file system using Save() method of **IPresentation** interface. Default format type is *.pptx.

{% highlight c# %}
[C#]

//Open an existing PowerPoint presentation 

IPresentation presentation = Presentation.Open(fileName);

//To-Do some manipulation

//To-Do some manipulation

//Save the presentation in file system

presentation.Save("Output.pptx");



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Open an existing PowerPoint presentation

Dim presentation_1 As IPresentation = Presentation.Open(fileName)

'To-Do some manipulation

'To-Do some manipulation

'Save the presentation in file system

Presentation_1.Save("Output.pptx")



{% endhighlight %}

## Saving a PowerPoint presentation to stream

You can save the created or manipulated PowerPoint presentation to stream using overloads of Save method.

{% highlight c# %}
[C#]

//open an existing PowerPoint presentation 

IPresentation presentation = Presentation.Open(fileName);

//To-Do some manipulation

//To-Do some manipulation

//Create an instance of memory stream

MemoryStream stream = new MemoryStream();

//Save the presentation to stream

presentation.Save(stream);



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'open an existing PowerPoint presentation 

Dim presentation_1 As IPresentation = Presentation.Open(fileName)

'To-Do some manipulation

'To-Do some manipulation

'Create an instance of memory stream

Dim stream As New MemoryStream()

'Save the presentation to stream

Presentation_1.Save(stream)



{% endhighlight %}

## Sending to a client browser

You can save and send the presentation to a client browser from a website or web application by invoking the overload of Save method. This method explicitly make use of an instance of HttpResponse as its parameter in order to stream the presentation to client browser. So this overload is suitable for web application which references [System.Web](https://msdn.microsoft.com/en-us/library/gg145018(v=vs.110).aspx# "") assembly.

{% highlight c# %}
[C#]

//Open an existing PowerPoint presentation 

IPresentation presentation = Presentation.Open(fileName);

//To-Do some manipulation

//To-Do some manipulation

//Save the presentation to the client browser

presentation.Save("Output.pptx", FormatType.Pptx, Response);



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Open an existing PowerPoint presentation 

Dim presentation_1 As IPresentation = Presentation.Open(fileName)

'To-Do some manipulation

'To-Do some manipulation

'Save the presentation to the client browser

Presentation_1.Save("Output.pptx", FormatType.Pptx, Response)



{% endhighlight %}

## Closing a PowerPoint presentation

Once we are done with the presentation instance, we should close the instance of **IPresentation**, in order to release the memory consumed by Essential Presentation library. The following code snippet illustrates how to close an IPresentation instance.

{% highlight c# %}
[C#]

//Open an existing presentation from file system 

IPresentation presentation = Presentation.Open(fileName);

//To-Do some manipulation

//To-Do some manipulation

//Creates an instance of memory stream

MemoryStream stream = new MemoryStream();

//Save the presentation to stream

presentation.Save(stream);

//Close the presentation instance & free the memory consumed.

presentation.Close();



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Open an existing presentation from file system 

Dim presentation_1 As IPresentation = Presentation.Open(fileName)

'To-Do some manipulation

'To-Do some manipulation

'Creates an instance of memory stream

Dim stream As New MemoryStream()

'Save the presentation to stream

presentation_1.Save(stream)

'Close the presentation instance & free the memory consumed.

presentation_1.Close()



{% endhighlight %}

