---
title: How to overcome Parameter Not valid exception | XlsIO | Syncfusion
description: This page tells the reason for parameter not valid exception in Excel to PDF with Custom Papar Size in Syncfusion .NET Excel library (XlsIO).
platform: File-formats
control: XlsIO
documentation: UG
---

# How to overcome Parameter Not valid exception?

ParameterNotValid exception occurs while trying to convert Excel document to PDF with large CustomPaperSize. Syncfusion XlsIO cannot handle such large values. Also, the values are considered in inches. Using height and width below 200 would resolve the issue.
