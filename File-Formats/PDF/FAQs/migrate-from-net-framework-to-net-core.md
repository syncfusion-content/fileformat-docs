---
title: Migrate from .NET Framework to .NET Core | Syncfusion 
description: This section explains the process of migrating from .NET Framework to .NET Core for classes, methods, properties and events. 
platform: file-formats
control: PDF
documentation: UG
---

# Migrate PDF library from .NET Framework to .NET Core 

The Syncfusion ASP.NET Web Forms components will no longer be actively developed and will be marked as end of support after the 2023 Volume 2 release. However, ASP.NET Web Forms related NuGet’s will be updated until then. If you want to use the Syncfusion ASP.NET Web Forms components in the future, you may continue to use till version 2023 Volume 2 release, and bug fixes will be provided as patches as long as Microsoft supports it, even after the 2023 Volume 2 release. It is recommended to use the latest Blazor or ASP.NET Core for new web applications development. For more details, please refer the below link,
https://learn.microsoft.com/en-us/dotnet/architecture/blazor-for-web-forms-developers/introduction. 

You can also visit the Blazor documentation and demo links provided for more information.
* [Blazor documentation](https://blazor.syncfusion.com/documentation/introduction)
* [Blazor demo](https://blazor.syncfusion.com/demos/)

This section explains the modification required while migrating the Syncfusion .NET PDF library from .NET Framework to .NET Core.

## NuGet packages 

<table>
<tr>
<thead>
<th>Packages targeting .NET Framework</th>
<th>Packages targeting .NET Standard 2.0/.NET Core</th>
</thead>
</tr>
<tr>
<td>
<ul>
<li>[Syncfusion.Pdf.WinForms](https://www.nuget.org/packages/Syncfusion.Pdf.WinForms)</li>
<li>[Syncfusion.Pdf.Wpf](https://www.nuget.org/packages/Syncfusion.Pdf.Wpf)</li>
<li>[Syncfusion.Pdf.AspNet](https://www.nuget.org/packages/Syncfusion.Pdf.AspNet)</li>
<li>[Syncfusion.Pdf.AspNet.Mvc4](https://www.nuget.org/packages/Syncfusion.Pdf.AspNet.Mvc4)</li>
<li>[Syncfusion.Pdf.AspNet.Mvc5](https://www.nuget.org/packages/Syncfusion.Pdf.AspNet.Mvc5)</li>
</ul>
</td>
<td> 
[Syncfusion.Pdf.Net.Core](https://www.nuget.org/packages/Syncfusion.Pdf.Net.Core) 
</td>
</tr>
</table>

## Class changes 

Missing classes | Alternate classes 
[PdfLoadedDocument(String)](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html#Syncfusion_Pdf_Parsing_PdfLoadedDocument__ctor_System_String_) | You can open the document as stream from the system file using [PdfLoadedDocument(Stream)](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html#Syncfusion_Pdf_Parsing_PdfLoadedDocument__ctor_System_IO_Stream_) API.  

[PdfLoadedDocument(String, String)](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html#Syncfusion_Pdf_Parsing_PdfLoadedDocument__ctor_System_String_System_String_) | You can open the encrypted document as stream or byte array with password from system file using [PdfLoadedDocument(Stream, String)](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html#Syncfusion_Pdf_Parsing_PdfLoadedDocument__ctor_System_IO_Stream_System_String_) or [PdfLoadedDocument(Byte[], String)](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html#Syncfusion_Pdf_Parsing_PdfLoadedDocument__ctor_System_Byte___System_String_) API. 

[PdfLoadedDocument(String, Boolean)](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html#Syncfusion_Pdf_Parsing_PdfLoadedDocument__ctor_System_String_System_Boolean_) | You can open the corrupted PDF document as stream or byte array with Boolean from system file using [PdfLoadedDocument(Stream, Boolean)](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html#Syncfusion_Pdf_Parsing_PdfLoadedDocument__ctor_System_IO_Stream_System_Boolean_) or [PdfLoadedDocument(Byte[], Boolean)](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html#Syncfusion_Pdf_Parsing_PdfLoadedDocument__ctor_System_Byte___System_Boolean_) API. 

[PdfBitmap(String)](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfBitmap.html#Syncfusion_Pdf_Graphics_PdfBitmap__ctor_System_String_) | [PdfBitmap(Stream)](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfBitmap.html#Syncfusion_Pdf_Graphics_PdfBitmap__ctor_System_IO_Stream_)

[PdfBitmap(String, Boolean)](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfBitmap.html#Syncfusion_Pdf_Graphics_PdfBitmap__ctor_System_String_System_Boolean_) | [PdfBitmap(Steam, Boolean)](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfBitmap.html#Syncfusion_Pdf_Graphics_PdfBitmap__ctor_System_IO_Stream_System_Boolean_)

[TextLines](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.TextLines.html#constructors) | TextLineCollection <br/> *Sample link:* <br/> https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Text%20Extraction/Extract-each-lines-from-an-existing-PDF-document 

[PdfBitmap](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfBitmap.html) | PdfTiffImage <br/> *Sample link:* <br/> https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Document%20conversion/TIFF-to-PDF/Converting-multipage-TIFF-to-PDF-document   

