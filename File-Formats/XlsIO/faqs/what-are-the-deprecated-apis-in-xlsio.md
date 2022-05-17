---
title: What are the deprecated APIs in XlsIO | Syncfusion
description: description: This page lists the deprecated APIs of Syncfusion .NET Excel library (XlsIO) and their respective new APIs.
platform: File-formats
control: XlsIO
documentation: UG
---

# What are the deprecated APIs in XlsIO?

[FillBackgroundRGB](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IExtendedFormat.html#Syncfusion_XlsIO_IExtendedFormat_FillBackgroundRGB), [FillBackground](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IExtendedFormat.html#Syncfusion_XlsIO_IExtendedFormat_FillBackground), [FillForegroundRGB](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IExtendedFormat.html#Syncfusion_XlsIO_IExtendedFormat_FillForegroundRGB), and [FillForeground](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IExtendedFormat.html#Syncfusion_XlsIO_IExtendedFormat_FillForeground) APIs that were available under **CellStyle** are now deprecated, and Syncfusion XlsIO have now come up with new APIS called [Color](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IExtendedFormat.html#Syncfusion_XlsIO_IExtendedFormat_Color), [ColorIndex](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IExtendedFormat.html#Syncfusion_XlsIO_IExtendedFormat_ColorIndex), [PatternColor](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IExtendedFormat.html#Syncfusion_XlsIO_IExtendedFormat_PatternColor), and [PatternColorIndex](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IExtendedFormat.html#Syncfusion_XlsIO_IExtendedFormat_PatternColorIndex). Please find the list below.

<table>
<tr>
<th>Old API<br/><br/></th>
<th>New API<br/><br/></th>
</tr>
<tbody>
<tr>
<td>worksheet.Range["A1"].CellStyle.FillBackgroundRGB<br/><br/></td>
<td>worksheet.Range["A1"].CellStyle.Color<br/><br/></td>
</tr>
<tr>
<td>worksheet.Range["A1"].CellStyle.FillBackground<br/><br/></td>
<td>worksheet.Range["A1"].CellStyle.ColorIndex<br/><br/></td>
</tr>
<tr>
<td>worksheet.Range["A1"].CellStyle.FillForegroundRGB<br/><br/></td>
<td>worksheet.Range["A1"].CellStyle.PatternColor<br/><br/></td>
</tr>
<tr>
<td>worksheet.Range["A1"].CellStyle.FillForeground<br/><br/></td>
<td>worksheet.Range["A1"].CellStyle.PatternColorIndex<br/><br/></td>
</tr>
</tbody>
</table>
