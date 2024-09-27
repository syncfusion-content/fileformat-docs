---
title: How to overcome UnauthorizedAccessException | XlsIO | Syncfusion
description: This page shows how to overcome UnauthorizedAccessException using Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# How to overcome UnauthorizedAccessException?

The [UnauthorizedAccessException](https://learn.microsoft.com/en-us/dotnet/api/system.unauthorizedaccessexception?view=netcore-3.1) occurs when you are trying to write in a read-only/hidden file or if you don’t have access to the particular folder that contains the file or the folder might be locked currently. 

First, check whether you can access the folder and the file directly. Then, right-click the input file and check whether the Read-only/Hidden checkbox is checked. If it is checked, kindly uncheck the Read-only/Hidden checkbox and try running the project as an administrator or an authorized user to access the file folder.

## See Also

* [How to overcome StackOverflow exception with IWorksheet Calculate()?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-overcome-stackoverflow-exception-with-iworksheet-calculate)
* [How to avoid exception when adding worksheets with same name?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-avoid-exception-when-adding-worksheets-with-same-name)
* [What are the known exceptions of XlsIO?](https://help.syncfusion.com/file-formats/xlsio/known-exceptions)
* [How to secure Excel documents?](https://help.syncfusion.com/file-formats/xlsio/security)
