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

<table>
<tr>
<thead>
<th>Missing classes</th>
<th>Alternate classes</th>
</thead>
</tr>
<tr>
<td>
[PdfLoadedDocument(String)](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html#Syncfusion_Pdf_Parsing_PdfLoadedDocument__ctor_System_String_)
</td>
<td> 
You can open the document as stream from the system file using [PdfLoadedDocument(Stream)](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html#Syncfusion_Pdf_Parsing_PdfLoadedDocument__ctor_System_IO_Stream_) API.  
</td>
</tr>
<tr>
<td>
[PdfLoadedDocument(String, String)](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html#Syncfusion_Pdf_Parsing_PdfLoadedDocument__ctor_System_String_System_String_)
</td>
<td> 
You can open the encrypted document as stream or byte array with password from system file using [PdfLoadedDocument(Stream, String)](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html#Syncfusion_Pdf_Parsing_PdfLoadedDocument__ctor_System_IO_Stream_System_String_) or [PdfLoadedDocument(Byte[], String)](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html#Syncfusion_Pdf_Parsing_PdfLoadedDocument__ctor_System_Byte___System_String_) API. 
</td>
</tr>
<tr>
<td>
[PdfLoadedDocument(String, Boolean)](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html#Syncfusion_Pdf_Parsing_PdfLoadedDocument__ctor_System_String_System_Boolean_)
</td>
<td> 
You can open the corrupted PDF document as stream or byte array with Boolean from system file using [PdfLoadedDocument(Stream, Boolean)](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html#Syncfusion_Pdf_Parsing_PdfLoadedDocument__ctor_System_IO_Stream_System_Boolean_) or [PdfLoadedDocument(Byte[], Boolean)](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfLoadedDocument.html#Syncfusion_Pdf_Parsing_PdfLoadedDocument__ctor_System_Byte___System_Boolean_) API. 
</td>
</tr>
<tr>
<td>
[PdfBitmap(String)](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfBitmap.html#Syncfusion_Pdf_Graphics_PdfBitmap__ctor_System_String_)
</td>
<td> 
[PdfBitmap(Stream)](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfBitmap.html#Syncfusion_Pdf_Graphics_PdfBitmap__ctor_System_IO_Stream_)
</td>
</tr>
<tr>
<td>
[PdfBitmap(String, Boolean)](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfBitmap.html#Syncfusion_Pdf_Graphics_PdfBitmap__ctor_System_String_System_Boolean_)
</td>
<td> 
[PdfBitmap(Steam, Boolean)](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfBitmap.html#Syncfusion_Pdf_Graphics_PdfBitmap__ctor_System_IO_Stream_System_Boolean_)
</td>
</tr>
<tr>
<td>
[TextLines](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.TextLines.html#constructors) 
</td>
<td> 
TextLineCollection <br/> *Sample link:* <br/> [https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Text%20Extraction/Extract-each-lines-from-an-existing-PDF-document](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Text%20Extraction/Extract-each-lines-from-an-existing-PDF-document) 
</td>
</tr>
<tr>
<td>
[PdfBitmap](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfBitmap.html)
</td>
<td> 
PdfTiffImage <br/> *Sample link:* <br/> [https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Document%20conversion/TIFF-to-PDF/Converting-multipage-TIFF-to-PDF-document](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Document%20conversion/TIFF-to-PDF/Converting-multipage-TIFF-to-PDF-document)   
</td>
</tr>
<tr>
<td>
[XPSToPdfConverter](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Base~Syncfusion.XPS.XPSToPdfConverter.html) 
</td>
<td> 
XPSToPdfConverter <br/> *Sample link:* <br/> [https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Document%20conversion/Converting-XPS-to-PDF-document](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Document%20conversion/Converting-XPS-to-PDF-document)
</td>
</tr>
<tr>
<td>
[PdfCompressionOptions](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfCompressionOptions.html)    
</td>
<td> 
PdfCompressionOptions <br/> *Sample link:* <br/> [https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Compression/Compress-the-images-in-an-existing-PDF-document](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Compression/Compress-the-images-in-an-existing-PDF-document)
</td>
</tr>
<tr>
<td>
[PdfFileLinkAnnotation](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfFileLinkAnnotation.html)
</td>
<td> 
Not supported 
</td>
</tr>
<tr>
<td>
[PdfLauchAction](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfLaunchAction.html)
</td>
<td> 
Not supported  
</td>
</tr>
<tr>
<td>
[PdfJavaScriptAction](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfJavaScriptAction.html) - Add/modify Javascript actions on existing PDF document 
</td>
<td> 
Not supported 
</td>
</tr>
<tr>
<td>
[PdfDocumentAnalyzer(String)](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfDocumentAnalyzer.html#Syncfusion_Pdf_Parsing_PdfDocumentAnalyzer__ctor_System_String_)
</td>
<td> 
You can check whether the existing PDF document is corrupted or not using [PdfDocumentAnalyzer(Stream)](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.PdfDocumentAnalyzer.html#Syncfusion_Pdf_Parsing_PdfDocumentAnalyzer__ctor_System_IO_Stream_).  
</td>
</tr>
<tr>
<td>
[PdfUsedFont](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.Fonts.PdfUsedFont.html)
</td>
<td> 
Not supported 
</td>
</tr>
<tr>
<td>
[ImageExportSettings](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.ImageExportSettings.html)
</td>
<td> 
Not supported  
</td>
</tr>
<tr>
<td>
[PdfBarcodeException](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Barcode.PdfBarcodeException.html)
</td>
<td> 
BarcodeException 
</td>
</tr>
<tr>
<td>
[ImageExportSettings](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.ImageExportSettings.html)
</td>
<td> 
Not supported  
</td>
</tr>
<tr>
<td>
[HtmlToPdfResult](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.HtmlToPdf.HtmlToPdfResult.html)
</td>
<td> 
Not supported  
</td>
</tr>
<tr>
<td>
[PdfRichMediaContent(String, PdfRichMediaContentType)](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfRichMediaContent.html#Syncfusion_Pdf_Interactive_PdfRichMediaContent__ctor_System_String_Syncfusion_Pdf_Interactive_PdfRichMediaContentType_)
</td>
<td> 
[PdfRichMediaContent(String, Stream, String, PdfRichMediaContentType)](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfRichMediaContent.html#Syncfusion_Pdf_Interactive_PdfRichMediaContent__ctor_System_String_System_IO_Stream_System_String_Syncfusion_Pdf_Interactive_PdfRichMediaContentType_)
</td>
</tr>
<tr>
<td>
[PdfAngleMeasurementAnnotation(PointF[])](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfAngleMeasurementAnnotation.html#Syncfusion_Pdf_Interactive_PdfAngleMeasurementAnnotation__ctor_System_Drawing_PointF___)
</td>
<td> 
Not supported
</td>
</tr>
<tr>
<td>
[PdfCertificateDistinguishedName](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Security.PdfCertificateDistinguishedName.html)
</td>
<td> 
Not supported  
</td>
</tr>
<tr>
<td>
[GraphicsStateData](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.GraphicsStateData.html)
</td>
<td> 
Not supported 
</td>
</tr>
<tr>
<td>
[PdfConfig](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.PdfConfig.html)
</td>
<td> 
Not supported 
</td>
</tr>
<tr>
<td>
[TextData](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.TextData.html)
</td>
<td> 
Not supported  
</td>
</tr>
<tr>
<td>
[TextLines](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.TextLines.html)
</td>
<td> 
TextLineCollection <br/> *Sample link:* <br/> [https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Text%20Extraction/Extract-each-lines-from-an-existing-PDF-document](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Text%20Extraction/Extract-each-lines-from-an-existing-PDF-document)
</td>
</tr>
<tr>
<td>
[PdfMetafile](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfMetafile.html)
</td>
<td> 
Not supported
</td>
</tr>
<tr>
<td>
[PdfMetafileLayoutFormat](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfMetafileLayoutFormat.html)
</td>
<td> 
PdfLayoutFormat <br/> *Sample link:* <br/> [https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Text/Adding-HTML-styled-text-to-PDF-document/](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Text/Adding-HTML-styled-text-to-PDF-document/)
</td>
</tr>
<tr>
<td>
[XFdfDocument](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Parsing.XFdfDocument.html)
</td>
<td> 
Not supported
</td>
</tr>
<tr>
<td>
[HtmlToPdfResult](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.HtmlToPdf.HtmlToPdfResult.html)
</td>
<td> 
Not supported 
</td>
</tr>
<tr>
<td>
[PdfAngleMeasurementAnnotation](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Interactive.PdfAngleMeasurementAnnotation.html)
</td>
<td> 
Not supported  
</td>
</tr>
</table>