---
title: Maximum characters count in an Excel cell | XlsIO | Syncfusion
description: This page has information of maximum characters count in an Excel cell in Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# Information about maximum characters count in an Excel cell

An Excel cell accepts only maximum 32767 characters. ArgumentOutOfRangeException is thrown when you try to set the text with length greater that 32767 characters, into an Excel cell. This is the behavior of Microsoft Excel and Syncfusion XlsIO also does the same. Please go through [Excel Specifications and Limits](https://support.microsoft.com/en-us/office/excel-specifications-and-limits-1672b34d-7043-467e-8e27-269d656771c3).
