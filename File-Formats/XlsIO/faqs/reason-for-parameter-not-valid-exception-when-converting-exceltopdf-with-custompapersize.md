---
title: How to overcome Parameter Not valid exception | XlsIO | Syncfusion
description: This page tells the reason for parameter not valid exception in Excel to PDF with Custom Papar Size in Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# How to overcome Parameter Not valid exception?

**ParameterNotValid** exception occurs while trying to convert Excel document to PDF with large [CustomPaperSize](https://help.syncfusion.com/cr/file-formats/Syncfusion.ExcelToPdfConverter.ExcelToPdfConverterSettings.html#Syncfusion_ExcelToPdfConverter_ExcelToPdfConverterSettings_CustomPaperSize). Syncfusion XlsIO cannot handle such large values. Also, the values are considered in inches. Using height and width below 200 would resolve the issue.
