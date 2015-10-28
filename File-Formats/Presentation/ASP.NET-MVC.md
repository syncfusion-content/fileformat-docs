---
layout: Post
title: Loading and Saving the presentation in ASP.NET MVC platform
description: Loading and Saving the presentation in ASP.NET MVC platform
platform: ASP.NET MVC
control: Presentation
documentation: FileFormats
---
## ASP.NET MVC 

The below code snippet demonstrates how to load and save a PowerPoint presentation in ASP.NET MVC platform:

{% highlight c# %}
[C#]

//Create a PowerPoint presentation

IPresentation presentationDocument = Presentation.Create();

//Add slide to the presentation

ISlide slide = presentationDocument.Slides.Add(SlideLayoutType.Blank);

//Add paragraph to the text box

IParagraph paragraph = slide.Shapes.AddTextBox(100, 120, 300, 200).TextBody.AddParagraph("Sample Text");

//Save the presentation

return new PresentationResult(presentationDocument, "Output.pptx", HttpContext.ApplicationInstance.Response);



{% endhighlight %}

The following code snippet demonstrates the class “PresentationResult” used in the above code snippet.

{% highlight c# %}
[C#]

public class PresentationResult : ActionResult

{

//private members

private IPresentation m_source;

private string m_filename;

private HttpResponse m_response;

//Get/Set the filename of presentation

public string FileName

{

get

{

return m_filename;

}

set

{

m_filename = value;

}

}

//Get the presentation

public IPresentation Source

{

get

{

return m_source as IPresentation;

}

}

//Get the http response

public HttpResponse Response

{

get

{

return m_response;

}

}

public PresentationResult(IPresentation source, string fileName, HttpResponse response)

{

//Assign values using the constructor

this.FileName = fileName;

this.m_source = source;

m_response = response;

}

public override void ExecuteResult(ControllerContext context)

{

//Throw exception if context is null

if (context == null)

throw new ArgumentNullException("Context");

//Save the presentation to the client browser

this.m_source.Save(FileName, FormatType.Pptx, Response);

}

}



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

'Create a PowerPoint presentation

Dim presentationDocument As IPresentation = Presentation.Create()

'Add slide to the presentation

Dim slide As ISlide = presentationDocument.Slides.Add(SlideLayoutType.Blank)

'Add paragraph to the text box

Dim paragraph As IParagraph = slide.Shapes.AddTextBox(100, 120, 300, 200).TextBody.AddParagraph("Sample Text")

'Save the presentation

Return New PresentationResult(presentationDocument, "Output.pptx", HttpContext.ApplicationInstance.Response)



{% endhighlight %}

{% highlight vb.net %}
[VB.NET]

Public Class PresentationResult

Inherits ActionResult

'private members

Private m_source As IPresentation

Private m_filename As String

Private m_response As HttpResponse

'Get/Set the filename of presentation

Public Property FileName() As String

Get

Return m_filename

End Get

Set(value As String)

m_filename = value

End Set

End Property

'Get the presentation

Public ReadOnly Property Source() As IPresentation

Get

Return TryCast(m_source, IPresentation)

End Get

End Property

'Get the http response information

Public ReadOnly Property Response() As HttpResponse

Get

Return m_response

End Get

End Property

Public Sub New(source As IPresentation, fileName As String, response As HttpResponse)

'Assign variables/property using the constructor

Me.FileName = fileName

Me.m_source = source

m_response = response

End Sub

Public Overrides Sub ExecuteResult(context As ControllerContext)

'Throw exception if context is null

If context Is Nothing Then

Throw New ArgumentNullException("Context")

End If

'Save the presentation to the client browser

Me.m_source.Save(FileName, FormatType.Pptx, Response)

End Sub

End Class



{% endhighlight %}

## 

