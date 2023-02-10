---
title: Migrate DocIO library from .NET Framework to .NET Core | DocIO | Syncfusion
description: This section illustrates Migrate from net framework to net core
control: DocIO
documentation: UG
---
# Migrate DocIO library from .NET Framework to .NET Core

## Namespace changes 

<table>
<tr>
<thead>
<th>.NET Framework</th>	
<th>.NET Core</th>
</thead>
</tr>
<tr>
<td>Syncfusion.DocToPDFConverter</td>
<td>Syncfusion.DocIORenderer</td>
</tr>
<tr>
<td>Syncfusion.OfficeChartToImageConverter</td>
<td>Not applicable – Classes are moved within Syncfusion.DocIORenderer namespace </td>
</tr>
</table>

# API Changes

## Type Changes 

<table>
<tr>
<thead>
<th>Missing Types</th>	
<th>Alternate Types</th>
</thead>
</tr>
<tr>
<td>[DocToPDFConverter] (https://help.syncfusion.com/cr/file-formats/Syncfusion.DocToPDFConverter.DocToPDFConverter.html)</td>
<td>DocIORenderer</td>
</tr>
<tr>
<td>[ChartToImageConverter] (https://help.syncfusion.com/cr/file-formats/Syncfusion.OfficeChartToImageConverter.ChartToImageConverter.html)</td>
<td>Not applicable</td>
</tr>
<tr>
<td>[DocToPDFConverterSettings] (https://help.syncfusion.com/cr/file-formats/Syncfusion.DocToPDFConverter.DocToPDFConverterSettings.html)</td>
<td>Not applicable</td>
</tr>
</table>

## Property Changes
<table>
<tr>
<thead>
<th>Missing Properties</th>	
<th>Alternate Properties</th>
</thead>
</tr>
<tr>
<td>[DocToPDFConverterSettings.EnableFastRendering] (https://help.syncfusion.com/cr/file-formats/Syncfusion.DocToPDFConverter.DocToPDFConverterSettings.html#Syncfusion_DocToPDFConverter_DocToPDFConverterSettings_EnableFastRendering)</td>
<td>Not applicable</td>
</tr>
<tr>
<td>[DocToPDFConverterSettings.RecreateNestedMetaFile] (https://help.syncfusion.com/cr/file-formats/Syncfusion.DocToPDFConverter.DocToPDFConverterSettings.html#Syncfusion_DocToPDFConverter_DocToPDFConverterSettings_RecreateNestedMetafile)</td>
<td>Not supported due to .NET Core framework limitations.</td>
</tr>
<tr>
<td>[DocToPDFConverterSettings.ImageQuality] (https://help.syncfusion.com/cr/file-formats/Syncfusion.DocToPDFConverter.DocToPDFConverterSettings.html#Syncfusion_DocToPDFConverter_DocToPDFConverterSettings_ImageQuality)</td>
<td>Not supported</td>
</tr>
<tr>
<td>[DocToPDFConverterSettings.ImageResolution] (https://help.syncfusion.com/cr/file-formats/Syncfusion.DocToPDFConverter.DocToPDFConverterSettings.html#Syncfusion_DocToPDFConverter_DocToPDFConverterSettings_ImageResolution)</td>
<td>Not supported</td>
</tr>
<tr>
<td>[DocToPDFConverterSettings.PreserveOleEquationAsBitmap] (https://help.syncfusion.com/cr/file-formats/Syncfusion.DocToPDFConverter.DocToPDFConverterSettings.html#Syncfusion_DocToPDFConverter_DocToPDFConverterSettings_PreserveOleEquationAsBitmap)</td>
<td>Not supported due to .NET Core framework limitations.</td>
</tr>
<tr>
<td>[SaveOptions.HtmlExportImagesFolder] (https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.SaveOptions.html#Syncfusion_DocIO_DLS_SaveOptions_HtmlExportImagesFolder)</td>
<td>Not applicable.</td>
</tr>
<tr>
<td>[SaveOptions.HtmlExportCssStyleSheetFileName] (https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.SaveOptions.html#Syncfusion_DocIO_DLS_SaveOptions_HtmlExportCssStyleSheetFileName)</td>
<td>Not applicable</td>
</tr>
<tr>
<td>[SaveOption.HTMLExportImageAsBase64] (https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.SaveOptions.html#Syncfusion_DocIO_DLS_SaveOptions_HTMLExportImageAsBase64)</td>
<td>Not applicable</td>
</tr>
<tr>
<td>[CssStyleSheetType.External] (https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.CssStyleSheetType.html)</td>
<td>Not applicable</td>
</tr>
</table>

## Method Changes 

<table>
<tr>
<thead>
<th>Missing methods</th>	
<th>Alternate methods</th>
</thead>
</tr>
<tr>
<td>[Open(String)] (https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WordDocument.html#Syncfusion_DocIO_DLS_WordDocument_Open_System_String_)</td>
<td>You can open the document as stream from the file system using [Open(Stream, FormatType)] (https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WordDocument.html#Syncfusion_DocIO_DLS_WordDocument_Open_System_IO_Stream_Syncfusion_DocIO_FormatType_) API</td>
</tr>
<tr>
<td>[Save(String)] (https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WordDocument.html#Syncfusion_DocIO_DLS_WordDocument_Save_System_String_)</td>
<td>You can save the document as stream to the file system using [Save(Stream, FormatType)] (https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WordDocument.html#Syncfusion_DocIO_DLS_WordDocument_Save_System_IO_Stream_Syncfusion_DocIO_FormatType_) API</td>
</tr>
<tr>
<td>[Save(string fileName, FormatType formatType, HttpResponse response)] (https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WordDocument.html#Syncfusion_DocIO_DLS_WordDocument_Save_System_String_Syncfusion_DocIO_FormatType_System_Web_HttpResponse_Syncfusion_DocIO_HttpContentDisposition_)</td>	
<td>You can save the document as stream and then download from browser.</td>
</tr>
<tr>
<td>[Execute(OleDbDataReader)] (https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.MailMerge.html#Syncfusion_DocIO_DLS_MailMerge_Execute_System_Data_OleDb_OleDbDataReader_)</td>	
<td>Not supported due to .NET Core framework limitations.</td>
</tr>
<tr>
<td>[Execute(IDataReader)] (https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.MailMerge.html#Syncfusion_DocIO_DLS_MailMerge_Execute_System_Data_IDataReader_)</td>	
<td>Not supported due to .NET Core framework limitations.</td>
</tr>
<tr>
<td>[ExecuteGroup(IDataReader)] (https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.MailMerge.html#Syncfusion_DocIO_DLS_MailMerge_ExecuteGroup_System_Data_IDataReader_)</td>	
<td>Not supported due to .NET Core framework limitations.</td>
</tr>
<tr>
<td>[ExecuteNestedGroup(DbConnection, ArrayList)] (https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.MailMerge.html#Syncfusion_DocIO_DLS_MailMerge_ExecuteNestedGroup_System_Data_Common_DbConnection_System_Collections_ArrayList_)</td>	
<td>Not supported due to .NET Core framework limitations.</td>
</tr>
<tr>
<td>[ExecuteNestedGroup(DbConnection, ArrayList, Boolean)] (https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.MailMerge.html#Syncfusion_DocIO_DLS_MailMerge_ExecuteNestedGroup_System_Data_Common_DbConnection_System_Collections_ArrayList_System_Boolean_)</td>	
<td>Not supported due to .NET Core framework limitations.</td>
</tr>
<tr>
<td>[SaveAsImage(IOfficeChart, Stream)] (https://help.syncfusion.com/cr/file-formats/Syncfusion.OfficeChartToImageConverter.ChartToImageConverter.html#Syncfusion_OfficeChartToImageConverter_ChartToImageConverter_SaveAsImage_Syncfusion_OfficeChart_IOfficeChart_System_IO_Stream_)</td>	
<td>Not supported due to .NET Core framework limitations.</td>
</tr>
</table>

## Advantages

* Supports Windows, macOS, Linux, docker, Azure, and AWS environments.

## Known limitations

* EMF and WMF images are not supported in .NET Core platforms.

## Notable changes

* Drawing library: In .NET Framework, our library makes use of System.Drawing for any text measuring and graphics-related operations. Whereas in .NET Core, our library uses the SkiaSharp graphics library to provide the same type of graphics operations in all the supported platforms.
* The below features are make use of SkiaSharp graphics library, which are separated into a separate package, [Syncfusion.DocIORenderer.Net.Core] (https://www.nuget.org/packages/Syncfusion.DocIORenderer.Net.Core).
* During Word to PDF/Image conversion, if you are facing font-related problems (like accessing font from the environment), you can pass the fonts as streams using our [font substitution approach] (https://help.syncfusion.com/file-formats/docio/word-to-pdf#font-substitution). 

Note: 

If you want to migrate without any code changes from [“Syncfusion.DocIO.ASP.NET”] (https://www.nuget.org/packages/Syncfusion.DocIO.AspNet) NuGet in application targeting .NET Framework, you can consider to use anyone of the packages 

* Syncfusion.DocIO.WinForms 
* Syncfusion.DocIO.Wpf 
* Syncfusion.DocIO.AspNet.Mcv4 

This is not a recommended approach. 