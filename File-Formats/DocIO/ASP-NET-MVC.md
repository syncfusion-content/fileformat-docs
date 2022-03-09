---
title: Working with Word document in ASP.NET MVC using Syncfusion Word library
description: Creating a Word document in ASP.NET MVC application and save the document with Syncfusion Word library
platform: file-formats
control: DocIO
documentation: UG
---
# Working with ASP.NET MVC

In your ASP.NET MVC application, please add the required assemblies in order to use DocIO. [Refer here for assemblies required](/File-Formats/DocIO/Assemblies-Required).

## Save the document 

The following code example illustrates how to save the Word document in ASP.NET MVC.

{% tabs %}  

{% highlight c# tabtile="C#" %}

//Creates an empty Word document instance

WordDocument document = new WordDocument();

//Adds new section to the document

IWSection section = document.AddSection();

//Adds new paragraph to the section

IWParagraph paragraph = section.AddParagraph();

//Appends the text to the created paragraph

paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.");

//Export the document after saving

return document.ExportAsActionResult("Sample.docx", FormatType.Docx, HttpContext.ApplicationInstance.Response, HttpContentDisposition.Attachment);

{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


'Creates an empty Word document instance

Dim document As New WordDocument()

'Adds new section to the document

Dim section As IWSection = document.AddSection()

'Adds new paragraph to the section

Dim paragraph As IWParagraph = section.AddParagraph()

'Appends the text to the created paragraph

paragraph.AppendText("AdventureWorks Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company.")

'Export the document after saving

Return document.ExportAsActionResult("Sample.docx", FormatType.Docx, HttpContext.ApplicationInstance.Response, HttpContentDisposition.Attachment)

{% endhighlight %}

{% endtabs %}  

Following extension class will help you to download the Word document.

{% tabs %}  

{% highlight c# tabtile="C#" %}

public static class DocIOExtension
{

public static DocumentResult ExportAsActionResult(this IWordDocument document, string filename, FormatType formattype, HttpResponse response, HttpContentDisposition contentDisposition)

{

return new DocumentResult(document, filename, formattype, response, contentDisposition);

}

}

public class DocumentResult : ActionResult
 
{

#region Fields

private string m_filename;

private IWordDocument m_document;

private FormatType m_formatType;

private HttpResponse m_response;

private HttpContentDisposition m_contentDisposition;

#endregion Fields

#region Properties

public string FileName

{

get { return m_filename; }

set { m_filename = value; }

}

public IWordDocument Document

{

get { return (m_document != null) ?  m_document: null; }

}

public FormatType formatType

{

get { return m_formatType; }

set { m_formatType = value; }

}

public HttpContentDisposition ContentDisposition

{

get { return m_contentDisposition; }

set { m_contentDisposition = value;}

}

public HttpResponse Response

{

get { return m_response; }

}

#endregion Properties

#region Constructor

public DocumentResult(IWordDocument document, string filename, FormatType formattype, HttpResponse response, HttpContentDisposition contentDisposition)

{

FileName = filename;

m_document = document;

this.formatType = formattype;

m_response = response;

this.ContentDisposition = contentDisposition;

}

public override void ExecuteResult(ControllerContext context)

{

if (context == null)

throw new ArgumentNullException("Context");

this.Document.Save(FileName, formatType, Response, ContentDisposition);

}        

}

{% endhighlight %}

{% highlight vb.net tabtile="VB.NET" %}


Public Module Class DocIOExtension

<System.Runtime.CompilerServices.Extension> _
	
Public Shared Function ExportAsActionResult(ByVal document As IWordDocument, ByVal filename As String, ByVal formattype As FormatType, ByVal response As HttpResponse, ByVal contentDisposition As HttpContentDisposition) As DocumentResult

Return New DocumentResult(document, filename, formattype, response, contentDisposition)

End Function

End Module

Public Class DocumentResult

Inherits ActionResult

#Region "Fields"

Private m_filename As String

Private m_document As IWordDocument

Private m_formatType As FormatType

Private m_response As HttpResponse

Private m_contentDisposition As HttpContentDisposition

#End Region

#Region "Properties"

Public Property FileName() As String

Get
Return m_filename
End Get

Set
m_filename = value
End Set
End Property

Public ReadOnly Property Document() As IWordDocument

Get
			
Return If((m_document IsNot Nothing), m_document, Nothing)

End Get

End Property

Public Property formatType() As FormatType

Get

Return m_formatType

End Get

Set

m_formatType = value

End Set

End Property

Public Property ContentDisposition() As HttpContentDisposition

Get

Return m_contentDisposition

End Get

Set

m_contentDisposition = value

End Set

End Property


Public ReadOnly Property Response() As HttpResponse

Get

Return m_response

End Get

End Property


#End Region

#Region "Constructor"

Public Sub New(document As IWordDocument, filename__1 As String, formattype As FormatType, response As HttpResponse, contentDisposition As HttpContentDisposition)

FileName = filename__1

m_document = document

Me.formatType = formattype

m_response = response


Me.ContentDisposition = contentDisposition

End Sub

Public Overrides Sub ExecuteResult(context As ControllerContext)

If context Is Nothing Then

Throw New ArgumentNullException("Context")

End If

Me.Document.Save(FileName, formatType, Response, ContentDisposition)

End Sub

End Class

{% endhighlight %}

{% endtabs %}

## Online Examples

1. You can visit our ASP.NET MVC (JavaScript) online examples for [more examples of Essential DocIO](https://ej2.syncfusion.com/aspnetmvc/DocIO/UpdateFields#/material).

2. You can visit our ASP.NET MVC (jQuery) online examples for [more examples of Essential DocIO](https://mvc.syncfusion.com/demos/web/docio/default).