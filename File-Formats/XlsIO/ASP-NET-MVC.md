---
title: ASP.NET MVC
description: Briefs about saving an Excel document in ASP.NET MVC platform.
platform: file-formats
control: XlsIO
documentation: UG
---
# ASP.NET MVC

In order to use XlsIO in your ASP.NET MVC application, please add the required assemblies in your ASP.NET MVC application. Refer [Assemblies Required](/File-Formats/XlsIO/Assemblies-Required).

## Saving the document

The following code snippet illustrates how to save an Excel document in ASP.NET MVC.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

IWorkbook workbook = application.Workbooks.Create(1);

IWorksheet sheet = workbook.Worksheets[0];

sheet.Range["A3"].Text ="Hello World";

workbook.Version = ExcelVersion.Excel2013;

return excelEngine.SaveAsActionResult(workbook, "output.xlsx", HttpContext.ApplicationInstance.Response, ExcelDownloadType.PromptDialog, ExcelHttpContentType.Excel2013);

public static class XlsIOExtension

{

public static ExcelResult SaveAsActionResult(this ExcelEngine _engine, IWorkbook _workbook, string filename, HttpResponse response)

{

ExcelHttpContentType contentType = ExcelHttpContentType.Excel2007;

if (_workbook.Version == ExcelVersion.Excel2007)

contentType = ExcelHttpContentType.Excel2007;

else if (_workbook.Version == ExcelVersion.Excel97to2003)

contentType = ExcelHttpContentType.Excel2000;

return new ExcelResult(_engine, _workbook, filename, response, ExcelDownloadType.PromptDialog, contentType);

}



public static ExcelResult SaveAsActionResult(this ExcelEngine _engine, IWorkbook _workbook, string filename, HttpResponse response, ExcelDownloadType DownloadType)

{

ExcelHttpContentType contentType = ExcelHttpContentType.Excel2007;

if (_workbook.Version == ExcelVersion.Excel2007)

contentType = ExcelHttpContentType.Excel2007;

else if (_workbook.Version == ExcelVersion.Excel97to2003)

contentType = ExcelHttpContentType.Excel2000;

return new ExcelResult(_engine, _workbook, filename, response, DownloadType, contentType);

}

public static ExcelResult SaveAsActionResult(this ExcelEngine _engine, IWorkbook _workbook, string filename, HttpResponse response, ExcelHttpContentType contentType)

{

return new ExcelResult(_engine, _workbook, filename, response, ExcelDownloadType.PromptDialog, contentType);

}

public static ExcelResult SaveAsActionResult(this ExcelEngine _engine, IWorkbook _workbook, string filename, HttpResponse response, ExcelDownloadType DownloadType, ExcelHttpContentType contentType)

{

return new ExcelResult(_engine, _workbook, filename, response, DownloadType, contentType);

}

public static ExcelResult SaveAsActionResult(this ExcelEngine _engine, IWorkbook _workbook, string filename, ExcelSaveType saveType, HttpResponse response, ExcelDownloadType DownloadType, ExcelHttpContentType contentType)

{

return new ExcelResult(_engine, _workbook, filename, response, DownloadType, contentType);

}



public static ExcelResult SaveAsActionResult(this ExcelEngine _engine, IWorkbook _workbook, string filename, string separator, HttpResponse response, ExcelDownloadType DownloadType, ExcelHttpContentType contentType)

{

return new ExcelResult(_engine, _workbook, filename, separator, response, DownloadType, contentType);

}

}

public class ExcelResult : ActionResult

{

private IWorkbook m_source;

private ExcelEngine m_engine;

private string m_filename;

private HttpResponse m_response;

private ExcelDownloadType m_downloadType;

private ExcelHttpContentType m_contentType;

private string m_separator;

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

public IWorkbook Source

{

get

{

return m_source as IWorkbook;

}

}

public ExcelEngine Engine

{

get

{

return m_engine as ExcelEngine;

}

}

public HttpResponse Response

{

get

{

return m_response;

}

}

public ExcelDownloadType DownloadType

{

set

{

m_downloadType = value;

}

get

{

return m_downloadType;

}

}

public ExcelHttpContentType ContentType

{

set

{

m_contentType = value;

}

get

{

return m_contentType;

}

}

public string Separator

{

set

{

m_separator = value;

}

get

{

return m_separator;

}

}

public ExcelResult(ExcelEngine engine, IWorkbook source, string fileName, HttpResponse response, ExcelDownloadType downloadType, ExcelHttpContentType contentType)

{

this.FileName = fileName;

this.m_source = source;

this.m_engine = engine;

m_response = response;

DownloadType = downloadType;

ContentType = contentType;

}

public ExcelResult(ExcelEngine engine, IWorkbook source, string fileName, string separator, HttpResponse response, ExcelDownloadType downloadType, ExcelHttpContentType contentType)

{

this.FileName = fileName;

this.m_source = source;

this.m_engine = engine;

m_response = response;

DownloadType = downloadType;

ContentType = contentType;

Separator = separator;

}

public override void ExecuteResult(ControllerContext context)

{

if (context == null)

throw new ArgumentNullException("Context");

if (m_contentType == ExcelHttpContentType.CSV)

{

this.m_source.SaveAs(FileName, Separator, Response, DownloadType, ContentType);

this.m_source.Close();

this.m_engine.Dispose();

}

else

{

this.m_source.SaveAs(FileName, Response, DownloadType, ContentType);

this.m_source.Close();

this.m_engine.Dispose();

}

}

}

public override void ExecuteResult(ControllerContext context)

{

if (context == null)

throw new ArgumentNullException("Context");

if (m_contentType == ExcelHttpContentType.CSV)

{

this.m_source.SaveAs(FileName, Separator, Response, DownloadType, ContentType);

this.m_source.Close();

this.m_engine.Dispose();

}

else

{

this.m_source.SaveAs(FileName, Response, DownloadType, ContentType);

this.m_source.Close();

this.m_engine.Dispose();

}

}



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

Dim workbook As IWorkbook = application.Workbooks.Create(1)

Dim sheet As IWorksheet = workbook.Worksheets(0)

sheet.Range("A3").Text = "Hello World"

workbook.Version = ExcelVersion.Excel2013

Return excelEngine.SaveAsActionResult(workbook, "output.xlsx", HttpContext.ApplicationInstance.Response, ExcelDownloadType.PromptDialog, ExcelHttpContentType.Excel2013)

Public static Class XlsIOExtension

Public Shared Function SaveAsActionResult(ByVal ExcelEngine As Me, ByVal _workbook As IWorkbook, ByVal filename As String, ByVal response As HttpResponse) As ExcelResult

Dim contentType As ExcelHttpContentType = ExcelHttpContentType.Excel2007

If _workbook.Version = ExcelVersion.Excel2007 Then

contentType = ExcelHttpContentType.Excel2007

ElseIf _workbook.Version = ExcelVersion.Excel97to2003 Then

contentType = ExcelHttpContentType.Excel2000

End If

Return New ExcelResult(_engine, _workbook, filename, response, ExcelDownloadType.PromptDialog, contentType)

End Function

Public Shared Function SaveAsActionResult(ByVal ExcelEngine As Me, ByVal _workbook As IWorkbook, ByVal filename As String, ByVal response As HttpResponse, ByVal DownloadType As ExcelDownloadType) As ExcelResult

Dim contentType As ExcelHttpContentType = ExcelHttpContentType.Excel2007

If _workbook.Version = ExcelVersion.Excel2007 Then

contentType = ExcelHttpContentType.Excel2007

ElseIf _workbook.Version = ExcelVersion.Excel97to2003 Then

contentType = ExcelHttpContentType.Excel2000

End If

Return New ExcelResult(_engine, _workbook, filename, response, DownloadType, contentType)

End Function

Public Shared Function SaveAsActionResult(ByVal ExcelEngine As Me, ByVal _workbook As IWorkbook, ByVal filename As String, ByVal response As HttpResponse, ByVal contentType As ExcelHttpContentType) As ExcelResult

Return New ExcelResult(_engine, _workbook, filename, response, ExcelDownloadType.PromptDialog, contentType)

End Function

Public Shared Function SaveAsActionResult(ByVal ExcelEngine As Me, ByVal _workbook As IWorkbook, ByVal filename As String, ByVal response As HttpResponse, ByVal DownloadType As ExcelDownloadType, ByVal contentType As ExcelHttpContentType) As ExcelResult

Return New ExcelResult(_engine, _workbook, filename, response, DownloadType, contentType)

End Function

Public Shared Function SaveAsActionResult(ByVal ExcelEngine As Me, ByVal _workbook As IWorkbook, ByVal filename As String, ByVal saveType As ExcelSaveType, ByVal response As HttpResponse, ByVal DownloadType As ExcelDownloadType, ByVal contentType As ExcelHttpContentType) As ExcelResult

Return New ExcelResult(_engine, _workbook, filename, response, DownloadType, contentType)

End Function

Public Shared Function SaveAsActionResult(ByVal ExcelEngine As Me, ByVal _workbook As IWorkbook, ByVal filename As String, ByVal separator As String, ByVal response As HttpResponse, ByVal DownloadType As ExcelDownloadType, ByVal contentType As ExcelHttpContentType) As ExcelResult

Return New ExcelResult(_engine, _workbook, filename, separator, response, DownloadType, contentType)

End Function

End Class

Public Class ExcelResult

Inherits ActionResult

Private m_source As IWorkbook

Private m_engine As ExcelEngine

Private m_filename As String

Private m_response As HttpResponse

Private m_downloadType As ExcelDownloadType

Private m_contentType As ExcelHttpContentType

Private m_separator As String

Public Property FileName() As String

Get

Return m_filename

End Get

Set(ByVal Value As String)

m_filename = value

End Set

End Property

Public ReadOnly Property Source() As IWorkbook

Get

Return m_source as IWorkbook

End Get

End Property

Public ReadOnly Property Engine() As ExcelEngine

Get

Return m_engine as ExcelEngine

End Get

End Property

Public ReadOnly Property Response() As HttpResponse

Get

Return m_response

End Get

End Property

Public Property DownloadType() As ExcelDownloadType

Get

Return m_downloadType

End Get

Set(ByVal Value As ExcelDownloadType)

m_downloadType = value

End Set

End Property

Public Property ContentType() As ExcelHttpContentType

Get

Return m_contentType

End Get

Set(ByVal Value As ExcelHttpContentType)

m_contentType = value

End Set

End Property

Public Property Separator() As String

Get

Return m_separator

End Get

Set(ByVal Value As String)

m_separator = value

End Set

End Property

Public Sub New(ByVal engine As ExcelEngine, ByVal source As IWorkbook, ByVal fileName As String, ByVal response As HttpResponse, ByVal downloadType As ExcelDownloadType, ByVal contentType As ExcelHttpContentType)

Me.FileName = fileName

Me.m_source = source

Me.m_engine = engine

m_response = response

DownloadType = downloadType

ContentType = contentType

End Sub

Public Sub New(ByVal engine As ExcelEngine, ByVal source As IWorkbook, ByVal fileName As String, ByVal separator As String, ByVal response As HttpResponse, ByVal downloadType As ExcelDownloadType, ByVal contentType As ExcelHttpContentType)

Me.FileName = fileName

Me.m_source = source

Me.m_engine = engine

m_response = response

DownloadType = downloadType

ContentType = contentType

Separator = separator

End Sub

Public Overrides Sub ExecuteResult(ByVal context As ControllerContext)

If context Is Nothing Then

Throw New ArgumentNullException("Context")

End If

If m_contentType = ExcelHttpContentType.CSV Then

Me.m_source.SaveAs(FileName, Separator, Response, DownloadType, ContentType)

Me.m_source.Close()

Me.m_engine.Dispose()

Else

Me.m_source.SaveAs(FileName, Response, DownloadType, ContentType)

Me.m_source.Close()

Me.m_engine.Dispose()

End If

End Sub

End Class

Public Overrides Sub ExecuteResult(ByVal context As ControllerContext)

If context Is Nothing Then

Throw New ArgumentNullException("Context")

End If

If m_contentType = ExcelHttpContentType.CSV Then

Me.m_source.SaveAs(FileName, Separator, Response, DownloadType, ContentType)

Me.m_source.Close()

Me.m_engine.Dispose()

Else

Me.m_source.SaveAs(FileName, Response, DownloadType, ContentType)

Me.m_source.Close()

Me.m_engine.Dispose()

End If

End Sub



{% endhighlight %}

  {% endtabs %}  

