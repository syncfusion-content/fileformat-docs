---
title: Migrate from .NET Framework to .NET core | DocIO | Syncfusion
description: This section illustrates Migrating DocIO library from .NET Framework to .NET core
control: DocIO
documentation: UG
---
# Migrate DocIO library from .NET Framework to .NET Core

In this section, we will see about the changes which need to be considered while migrating Syncfusion .NET Word (DocIO) library from .NET Framework to .NET Core.  

## NuGet packages 

<table>
<tr>
<thead>
<th>Packages targeting .NET Framework</th>	
<th>Packages targeting .NET Standard 2.0/.NET Core</th>
</thead>
</tr>
<tr>
<td>[Syncfusion.DocIO.WinForms] (https://www.nuget.org/packages/Syncfusion.DocIO.WinForms<br/>[Syncfusion.DocIO.Wpf] (https://www.nuget.org/packages/Syncfusion.DocIO.Wpf)<br/>[Syncfusion.DocIO.AspNet](https://www.nuget.org/packages/Syncfusion.DocIO.AspNet)<br/>[Syncfusion.DocIO.AspNet.Mvc4](https://www.nuget.org/packages/Syncfusion.DocIO.AspNet.Mvc4)<br/>[Syncfusion.DocIO.AspNet.Mvc5] (https://www.nuget.org/packages/Syncfusion.DocIO.AspNet.Mvc5)</td>
<td>[Syncfusion.DocIO.Net.Core] (https://www.nuget.org/packages/Syncfusion.DocIO.Net.Core)</td>
</tr>
<tr>
<td>[Syncfusion.DocToPDFConverter.WinForms] (https://www.nuget.org/packages/Syncfusion.DocToPDFConverter.WinForms)<br/> [Syncfusion.DocToPDFConverter.Wpf] (https://www.nuget.org/packages/Syncfusion.DocToPDFConverter.Wpf)<br/>[Syncfusion.DocToPDFConverter.AspNet] (https://www.nuget.org/packages/Syncfusion.DocToPDFConverter.AspNet)<br/>[https://www.nuget.org/packages/Syncfusion.DocToPdfConverter.AspNet.Mvc4] (https://www.nuget.org/packages/Syncfusion.DocToPdfConverter.AspNet.Mvc4)<br/>[Syncfusion.DocIToPDFConverter.AspNet.Mvc5] (https://www.nuget.org/packages/Syncfusion.DocToPdfConverter.AspNet.Mvc5) (https://www.nuget.org/packages/Syncfusion.DocToPdfConverter.AspNet.Mvc5)</td>
<td>[Syncfusion.DocIORenderer.Net.Core] (https://www.nuget.org/packages/Syncfusion.DocIORenderer.Net.Core)</td>
</tr>
</table>

## Namespace changes 

<table>
<tr>
<thead>
<th>.NET Framework</th>	
<th>Alternate Namespace in .NET Core</th>
</thead>
</tr>
<tr>
<td>Syncfusion.DocToPDFConverter</td>
<td>Syncfusion.DocIORenderer</td>
</tr>
<tr>
<td>Syncfusion.OfficeChartToImageConverter</td>
<td>Not applicable – Classes are moved within Syncfusion.DocIORenderer namespace</td>
</tr>
</table>

## Type changes 

<table>
<tr>
<thead>
<th>Missing Types</th>	
<th>Alternate Types in .NET Core</th>
</thead>
</tr>
<tr>
<td>[DocToPDFConverter] (https://help.syncfusion.com/cr/file-formats/Syncfusion.DocToPDFConverter.DocToPDFConverter.html)</td>
<td>DocIORenderer</td>
</tr>
<tr>
<td>[ChartToImageConverter] (https://help.syncfusion.com/cr/file-formats/Syncfusion.OfficeChartToImageConverter.ChartToImageConverter.html)</td>
<td>Not applicable – It is handled internally.</td>
</tr>
<tr>
<td>[DocToPDFConverterSettings] (https://help.syncfusion.com/cr/file-formats/Syncfusion.DocToPDFConverter.DocToPDFConverterSettings.html)</td>
<td>DocIORendererSettings</td>
</tr>
</table>

## Property changes
<table>
<tr>
<thead>
<th>Missing properties</th>	
<th>Alternate properties in .NET Core </th>
</thead>
</tr>
<tr>
<td>[IWordDocument.ChartToImageConverter]  (https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.IWordDocument.html#Syncfusion_DocIO_DLS_IWordDocument_ChartToImageConverter)</td>
<td>Not applicable – It is handled internally.</td>
</tr>
<tr>
<td>[WordDocument.ChartToImageConverter]  (https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WordDocument.html#Syncfusion_DocIO_DLS_WordDocument_ChartToImageConverter)</td>
<td>Not applicable – It is handled internally.</td>
</tr>
<tr>
<td>[DocToPDFConverterSettings.EnableFastRendering] (https://help.syncfusion.com/cr/file-formats/Syncfusion.DocToPDFConverter.DocToPDFConverterSettings.html#Syncfusion_DocToPDFConverter_DocToPDFConverterSettings_EnableFastRendering)</td>
<td>This is the default approach in .NET Core and handled internally.</td>
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
<td>Not applicable – You can save the images to folder using [SaveOptions.ImageNodeVisited] (https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.SaveOptions.html#Syncfusion_DocIO_DLS_SaveOptions_ImageNodeVisited) event in the application level.</td>
</tr>
<tr>
<td>[SaveOptions.HtmlExportCssStyleSheetFileName] (https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.SaveOptions.html#Syncfusion_DocIO_DLS_SaveOptions_HtmlExportCssStyleSheetFileName)</td>
<td>Not supported</td>
</tr>
<tr>
<td>[SaveOption.HTMLExportImageAsBase64] (https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.SaveOptions.html#Syncfusion_DocIO_DLS_SaveOptions_HTMLExportImageAsBase64)</td>
<td>This is the default approach in .NET Core and handled internally.</td>
</tr>
<tr>
<td>[CssStyleSheetType.External] (https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.CssStyleSheetType.html)</td>
<td>Not supported</td>
</tr>
</table>

## Method Changes 

<table>
<tr>
<thead>
<th>Missing methods</th>	
<th>Alternate methods in .NET Core</th>
</thead>
</tr>
<tr>
<td>[WordDocument.Open(String)] (https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WordDocument.html#Syncfusion_DocIO_DLS_WordDocument_Open_System_String_)<br/>[WordDocument.Open(String, FormatType)](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WordDocument.html#Syncfusion_DocIO_DLS_WordDocument_Open_System_String_Syncfusion_DocIO_FormatType_)</td>
<td>You can open the document as stream from the file system using [WordDocument.Open(Stream, FormatType)] (https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WordDocument.html#Syncfusion_DocIO_DLS_WordDocument_Open_System_IO_Stream_Syncfusion_DocIO_FormatType_) API</td>
</tr>
<tr>
<td>[WordDocument.Save(String)] (https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WordDocument.html#Syncfusion_DocIO_DLS_WordDocument_Save_System_String_)<br/>[WordDocumentSave(String, FormatType)] (https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WordDocument.html#Syncfusion_DocIO_DLS_WordDocument_Save_System_String_Syncfusion_DocIO_FormatType_)</td>
<td>You can save the document as stream to the file system using [WordDocument.Save(Stream, FormatType)] (https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WordDocument.html#Syncfusion_DocIO_DLS_WordDocument_Save_System_IO_Stream_Syncfusion_DocIO_FormatType_) API</td>
</tr>
<tr>
<td>[WordDocument.Save(string fileName, FormatType formatType, HttpResponse response)] (https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.WordDocument.html#Syncfusion_DocIO_DLS_WordDocument_Save_System_String_Syncfusion_DocIO_FormatType_System_Web_HttpResponse_Syncfusion_DocIO_HttpContentDisposition_)</td>	
<td>You can save the document as stream and then download from browser.</td>
</tr>
<tr>
<td>[WParagraph.AppendPicture(Image)] (https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.IWParagraph.html#Syncfusion_DocIO_DLS_IWParagraph_AppendPicture_System_Drawing_Image_)</td>	
<td>You can open the image as stream and append in paragraph using AppendPicture(Stream imageStream) API.</td>
</tr>
<tr>
<td>[MailMerge.Execute(OleDbDataReader)] (https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.MailMerge.html#Syncfusion_DocIO_DLS_MailMerge_Execute_System_Data_OleDb_OleDbDataReader_)</td>	
<td>Not supported due to .NET Core limitations.</td>
</tr>
<tr>
<td>[MailMerge.Execute(IDataReader)] (https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.MailMerge.html#Syncfusion_DocIO_DLS_MailMerge_Execute_System_Data_IDataReader_)</td>	
<td>Not supported due to .NET Core limitations.</td>
</tr>
<tr>
<td>[MailMerge.ExecuteGroup(IDataReader)] (https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.MailMerge.html#Syncfusion_DocIO_DLS_MailMerge_ExecuteGroup_System_Data_IDataReader_)</td>	
<td>Not supported due to .NET Core limitations.</td>
</tr>
<tr>
<td>[MailMerge.ExecuteNestedGroup(DbConnection, ArrayList)] (https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.MailMerge.html#Syncfusion_DocIO_DLS_MailMerge_ExecuteNestedGroup_System_Data_Common_DbConnection_System_Collections_ArrayList_)</td>	
<td>Not supported due to .NET Core limitations.</td>
</tr>
<tr>
<td>[MailMerge.ExecuteNestedGroup(DbConnection, ArrayList, Boolean)] (https://help.syncfusion.com/cr/file-formats/Syncfusion.DocIO.DLS.MailMerge.html#Syncfusion_DocIO_DLS_MailMerge_ExecuteNestedGroup_System_Data_Common_DbConnection_System_Collections_ArrayList_System_Boolean_)</td>	
<td>Not supported due to .NET Core limitations.</td>
</tr>
<tr>
<td>[ChartToImageConverter.SaveAsImage(IOfficeChart, Stream)] (https://help.syncfusion.com/cr/file-formats/Syncfusion.OfficeChartToImageConverter.ChartToImageConverter.html#Syncfusion_OfficeChartToImageConverter_ChartToImageConverter_SaveAsImage_Syncfusion_OfficeChart_IOfficeChart_System_IO_Stream_)</td>	
<td>WChart.SaveAsImage()</td>
</tr>
</table>

## Advantages

* Supports Windows, macOS, Linux, docker, Azure, and AWS environments.

## Known limitations

* EMF and WMF images are not supported in .NET Core platforms.

## Notable changes

* Graphics library: In .NET Framework, our library makes use of System.Drawing.Common for any text measuring and graphics-related operations. Whereas in .NET Core, our library uses the SkiaSharp graphics library to provide the same type of graphics operations in all the supported environments.
* The below features are make use of SkiaSharp graphics library, which are separated into a separate package, [Syncfusion.DocIORenderer.Net.Core] (https://www.nuget.org/packages/Syncfusion.DocIORenderer.Net.Core).
	* [Word document to PDF] (https://help.syncfusion.com/file-formats/docio/word-to-pdf)
	* [Word document to Image] (https://help.syncfusion.com/file-formats/docio/word-to-image)
	* [Updating table of contents] (https://help.syncfusion.com/file-formats/docio/working-with-table-of-contents#updating-table-of-contents)
	* [Convert chart to image] (https://help.syncfusion.com/file-formats/docio/working-with-charts#convert-chart-to-image)
* During Word to PDF/Image conversion, if you are facing font-related problems (like accessing font from the environment), you can pass the fonts as streams using our [font substitution approach] (https://help.syncfusion.com/file-formats/docio/word-to-pdf#font-substitution).

N> If you want to migrate without any code changes from [“Syncfusion.DocIO.ASP.NET”] (https://www.nuget.org/packages/Syncfusion.DocIO.AspNet) NuGet in application targeting .NET Framework, you can consider to use anyone of the packages 

* Syncfusion.DocIO.WinForms 
* Syncfusion.DocIO.Wpf 
* Syncfusion.DocIO.AspNet.Mcv4 

But, this is not a recommended approach. 