---
title: Working with Asp.Net MVC
description: Creating a ASP.NET MVC application and save the document
platform: file-formats
control: PDF
documentation: UG
---
# Working with Asp.Net MVC

## Save the document 

The following code example illustrates how to save the PDF document in ASP.NET MVC.

{% highlight c# %}
C#:

// Create a new PdfDocument

PdfDocument document = new PdfDocument();

// Add a page to the document

PdfPage page = document.Pages.Add();

// Create Pdf graphics for the page

PdfGraphics graphics = page.Graphics;

// Create a solid brush

PdfBrush brush = new PdfSolidBrush(Color.Black);

// Set the font

PdfFont font = new PdfStandardFont(PdfFontFamily.Helvetica, 20f);

// Draw the text

graphics.DrawString("Hello world!", font, brush, new PointF(20, 20));

//Export the document after saving

return document.ExportAsActionResult("output.pdf", HttpContext.ApplicationInstance.Response, HttpReadType.Save);

public static class PdfExtension

{

public static PdfResult ExportAsActionResult(this PdfDocument PdfDoc, string filename, HttpResponse response, HttpReadType type)

{

return new PdfResult(PdfDoc, filename, response, type);

}

public static PdfResult ExportAsActionResult(this PdfLoadedDocument pdfdoc, string filename, HttpResponse response, HttpReadType type)

{

return new PdfResult(pdfdoc, filename, response, type);

}

}

public class PdfResult : ActionResult

{

private string m_filename;

private PdfDocument m_pdfDocument;

private PdfLoadedDocument m_pdfLoadedDocument;

private HttpResponse m_response;

private HttpReadType m_readType;

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

public PdfDocument PdfDoc

{

get

{

if (m_pdfDocument != null)

return m_pdfDocument;

return null;

}

}

public PdfLoadedDocument pdfLoadedDoc

{

get

{

if (m_pdfLoadedDocument != null)

return m_pdfLoadedDocument;

return null;

}

}

public HttpResponse Response

{

get

{

return m_response;

}

}

public HttpReadType ReadType

{

get

{

return m_readType;

}

set

{

m_readType = value;

}

}

public PdfResult(PdfDocument pdfDocument, string filename, HttpResponse respone, HttpReadType type)

{

this.m_pdfDocument = pdfDocument;

this.m_pdfLoadedDocument = null;

this.FileName = filename;

this.m_response = respone;

this.ReadType = type;

}

public PdfResult(PdfLoadedDocument pdfLoadedDocument, string filename, HttpResponse respone, HttpReadType type)

{

this.m_pdfDocument = null;

this.m_pdfLoadedDocument = pdfLoadedDocument;

this.FileName = filename;

this.m_response = respone;

this.ReadType = type;

}

public  override void ExecuteResult(ControllerContext context)

{

if (context == null)

return;

if (pdfLoadedDoc != null)

this.pdfLoadedDoc.Save(FileName, Response, ReadType);

if (PdfDoc != null)

{

this.PdfDoc.Save(FileName, Response, ReadType);

this.PdfDoc.Close(true);

}

}



{% endhighlight %}

{% highlight vb.net %}
VB:

' Create a new PdfDocument

Dim document As New PdfDocument()

' Add a page to the document

Dim page As PdfPage = document.Pages.Add()

' Create Pdf graphics for the page

Dim graphics As PdfGraphics = page.Graphics

' Create a solid brush

Dim brush As PdfBrush = New PdfSolidBrush(Color.Black)

' Set the font

Dim font As PdfFont = New PdfStandardFont(PdfFontFamily.Helvetica, 20f)

' Draw the text

graphics.DrawString("Hello world!", font, brush, New PointF(20, 20))

'Export the document after saving

Return document.ExportAsActionResult("output.pdf", HttpContext.ApplicationInstance.Response, HttpReadType.Save)

Public Module PdfExtension

<System.Runtime.CompilerServices.Extension> _

Public Function ExportAsActionResult(ByVal PdfDoc As PdfDocument, ByVal filename As String, ByVal response As HttpResponse, ByVal type As HttpReadType) As PdfResult

Return New PdfResult(PdfDoc, filename, response, type)

End Function

<System.Runtime.CompilerServices.Extension> _

Public Function ExportAsActionResult(ByVal pdfdoc As PdfLoadedDocument, ByVal filename As String, ByVal response As HttpResponse, ByVal type As HttpReadType) As PdfResult

Return New PdfResult(pdfdoc, filename, response, type)

End Function

End Module

Public Class PdfResult

Inherits ActionResult

Private m_filename As String

Private m_pdfDocument As PdfDocument

Private m_pdfLoadedDocument As PdfLoadedDocument

Private m_response As HttpResponse

Private m_readType As HttpReadType

Public Property FileName() As String

Get

Return m_filename

End Get

Set(ByVal value As String)

m_filename = value

End Set

End Property

Public ReadOnly Property PdfDoc() As PdfDocument

Get

If m_pdfDocument IsNot Nothing Then

Return m_pdfDocument

End If

Return Nothing

End Get

End Property

Public ReadOnly Property pdfLoadedDoc() As PdfLoadedDocument

Get

If m_pdfLoadedDocument IsNot Nothing Then

Return m_pdfLoadedDocument

End If

Return Nothing

End Get

End Property

Public ReadOnly Property Response() As HttpResponse

Get

Return m_response

End Get

End Property

Public Property ReadType() As HttpReadType

Get

Return m_readType

End Get

Set(ByVal value As HttpReadType)

m_readType = value

End Set

End Property

Public Sub New(ByVal pdfDocument As PdfDocument, ByVal filename As String, ByVal respone As HttpResponse, ByVal type As HttpReadType)

Me.m_pdfDocument = pdfDocument

Me.m_pdfLoadedDocument = Nothing

Me.FileName = filename

Me.m_response = respone

Me.ReadType = type

End Sub

Public Sub New(ByVal pdfLoadedDocument As PdfLoadedDocument, ByVal filename As String, ByVal respone As HttpResponse, ByVal type As HttpReadType)

Me.m_pdfDocument = Nothing

Me.m_pdfLoadedDocument = pdfLoadedDocument

Me.FileName = filename

Me.m_response = respone

Me.ReadType = type

End Sub

Public Overrides Sub ExecuteResult(ByVal context As ControllerContext)

If context Is Nothing Then

Return

End If

If pdfLoadedDoc IsNot Nothing Then

Me.pdfLoadedDoc.Save(FileName, Response, ReadType)

End If

If PdfDoc IsNot Nothing Then

Me.PdfDoc.Save(FileName, Response, ReadType)

Me.PdfDoc.Close(True)

End If

End Sub

End Class





{% endhighlight %}

