---
title: Loading and Saving the Presentation in ASP.NET MVC platform
description: Loading and Saving the Presentation in ASP.NET MVC platform
platform: file-formats
control: Presentation
documentation: ug
---
# ASP.NET MVC 

The below code snippet demonstrates how to load and save a PowerPoint Presentation in ASP.NET MVC platform:

{% tabs %}

{% highlight c# %}

//Create a PowerPoint Presentation

IPresentation presentationDocument = Presentation.Create();

//Add slide to the Presentation

ISlide slide = presentationDocument.Slides.Add(SlideLayoutType.Blank);

//Add paragraph to the text box

IParagraph paragraph = slide.Shapes.AddTextBox(100, 120, 300, 200).TextBody.AddParagraph("Sample Text");

//Save the Presentation

return new PresentationResult(presentationDocument, "Output.pptx", HttpContext.ApplicationInstance.Response);

{% endhighlight %}

{% highlight vb.net %}

'Create a PowerPoint Presentation

Dim presentationDocument As IPresentation = Presentation.Create()

'Add slide to the Presentation

Dim slide As ISlide = presentationDocument.Slides.Add(SlideLayoutType.Blank)

'Add paragraph to the text box

Dim paragraph As IParagraph = slide.Shapes.AddTextBox(100, 120, 300, 200).TextBody.AddParagraph("Sample Text")

'Save the Presentation

Return New PresentationResult(presentationDocument, "Output.pptx", HttpContext.ApplicationInstance.Response)

{% endhighlight %}

{% endtabs %} 

The following code snippet demonstrates the class “PresentationResult” used in the above code snippet.

{% tabs %}

{% highlight c# %}

public class PresentationResult : ActionResult

{

//private members

private IPresentation m_source;

private string m_filename;

private HttpResponse m_response;

//Get/Set the filename of Presentation

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

//Get the Presentation

public IPresentation Source

{

get

{

return m_source as IPresentation;

}

}

//Get the HTTP response

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

//Save the Presentation to the client browser

this.m_source.Save(FileName, FormatType.Pptx, Response);

}

}



{% endhighlight %}

{% highlight vb.net %}

Public Class PresentationResult

Inherits ActionResult

'private members

Private m_source As IPresentation

Private m_filename As String

Private m_response As HttpResponse

'Get/Set the filename of Presentation

Public Property FileName() As String

Get

Return m_filename

End Get

Set(value As String)

m_filename = value

End Set

End Property

'Get the Presentation

Public ReadOnly Property Source() As IPresentation

Get

Return TryCast(m_source, IPresentation)

End Get

End Property

'Get the HTTP response information

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

'Save the Presentation to the client browser

Me.m_source.Save(FileName, FormatType.Pptx, Response)

End Sub

End Class



{% endhighlight %}

{% endtabs %} 

