---
title: Create, read, edit, convert PDF files in .NET | Syncfusion
description: Essential PDF is a .NET PDF library to convert PDF files in Windows Forms, WPF, UWP, ASP.NET Core, ASP.NET MVC, Xamarin, Flutter applications
platform: file-formats
control: PDF
documentation: UG
---
# Overview of PDF Framework

The PDF framework is a feature rich [.NET PDF class library](https://www.syncfusion.com/document-processing/pdf-framework/net) developed with 100% managed C# code that can be used to create, read and write PDF. The library can be used in [Windows Forms](https://www.syncfusion.com/document-processing/pdf-framework/net), [WPF](https://www.syncfusion.com/document-processing/pdf-framework/net), [ASP.NET Web Forms](https://www.syncfusion.com/document-processing/pdf-framework/net), [ASP.NET MVC](https://www.syncfusion.com/document-processing/pdf-framework/net), [ASP.NET Core](https://www.syncfusion.com/document-processing/pdf-framework/net-core), [Blazor](https://www.syncfusion.com/document-processing/pdf-framework/blazor), [UWP](https://www.syncfusion.com/document-processing/pdf-framework/uwp), [Xamarin](https://www.syncfusion.com/document-processing/pdf-framework/xamarin), [Flutter](https://www.syncfusion.com/document-processing/pdf-framework/flutter) applications and Unity platform without the dependency of Adobe Acrobat. The creation of PDF follows the most popular PDF 1.7 (ISO 32000-1) and latest PDF 2.0 (ISO 32000-2) specifications.

## Key Features of Essential PDF

The following list shows the key features available in the Essential PDF.

* Support to [create PDF files](https://help.syncfusion.com/file-formats/pdf/create-pdf-file-in-c-sharp-vb-net) from scratch.
* Support to add [text](https://help.syncfusion.com/file-formats/pdf/working-with-text), various formats of [images](https://help.syncfusion.com/file-formats/pdf/working-with-images), [tables](https://help.syncfusion.com/file-formats/pdf/working-with-tables) and [shapes](https://help.syncfusion.com/file-formats/pdf/working-with-shapes).
* Support for [creation](https://help.syncfusion.com/file-formats/pdf/working-with-forms#creating-a-new-pdf-form), [filling](https://help.syncfusion.com/file-formats/pdf/working-with-forms#filling-form-fields-in-an-existing-pdf-document) and [flattening](https://help.syncfusion.com/file-formats/pdf/working-with-forms#removing-editing-capability-of-form-fields) forms (AcroForms and XFA).  
* Open, modify and save existing PDF files.
* Support to [compress](https://help.syncfusion.com/file-formats/pdf/working-with-compression) existing PDF files.
* Ability to [merge](https://help.syncfusion.com/file-formats/pdf/merge-documents) and split PDF files.
* Support for [Optical Character Recognition](https://help.syncfusion.com/file-formats/pdf/working-with-ocr/dot-net-framework) by using Tesseract engine. 
* Ability to convert [HTML](https://help.syncfusion.com/file-formats/pdf/working-with-document-conversions#mhtml-to-pdf), [RTF](https://help.syncfusion.com/file-formats/pdf/working-with-document-conversions#converting-rtf-documents-to-pdf), [Word](https://help.syncfusion.com/file-formats/pdf/working-with-document-conversions#converting-word-documents-to-pdf), [Excel](https://help.syncfusion.com/file-formats/pdf/working-with-document-conversions#converting-excel-documents-to-pdf), [PowerPoint](https://help.syncfusion.com/file-formats/presentation/presentation-to-pdf) and [XPS](https://help.syncfusion.com/file-formats/pdf/working-with-document-conversions#converting-xps-document-to-pdf) to PDF.
* Ability to [encrypt and decrypt PDF](https://help.syncfusion.com/file-formats/pdf/working-with-security) files with advanced standards.
* Support to add, modify and remove interactive elements such as [bookmarks](https://help.syncfusion.com/file-formats/pdf/working-with-bookmarks), [annotations](https://help.syncfusion.com/file-formats/pdf/working-with-annotations) and [attachments](https://help.syncfusion.com/file-formats/pdf/working-with-attachments).
* Support to add [barcode](https://help.syncfusion.com/file-formats/pdf/working-with-barcode) in the PDF files.
* Support to convert [PDF to PDF/A-1B](https://help.syncfusion.com/file-formats/pdf/working-with-pdf-conformance#converting-pdf-to-pdfa-1b) conformance.
* Support for [PDF/X1-A](https://help.syncfusion.com/file-formats/pdf/working-with-pdf-conformance#adding-support-for-pdfx-1a-conformance),[PDF/A1-B](https://help.syncfusion.com/file-formats/pdf/working-with-pdf-conformance#adding-support-for-pdfa-1b-conformance),[PDF/A3-B](https://help.syncfusion.com/file-formats/pdf/working-with-pdf-conformance#adding-support-for-pdfa-2b-conformance) and [PDF/A1-B](https://help.syncfusion.com/file-formats/pdf/working-with-pdf-conformance#adding-support-for-pdfa-3b-conformance) conformances. 
* Support to create [accessible PDF or tagged PDF (PDF/UA)](https://help.syncfusion.com/file-formats/pdf/working-with-tagged-pdf) with section 508 compliant. 
* Support to [redact text and images](https://help.syncfusion.com/file-formats/pdf/working-with-redaction) in the PDF files.  
* Support to digitally [sign](https://help.syncfusion.com/file-formats/pdf/working-with-digitalsignature) and [validate](https://help.syncfusion.com/file-formats/pdf/working-with-digitalsignature) signature in PDF document. 
* Support to [find the corrupted PDF document](https://help.syncfusion.com/file-formats/pdf/working-with-document#find-corrupted-pdf-document). 
* Support for .NET Standard 1.2 onwards. 
* PDF library is compatible with .NET Core 3.0 WPF and Windows Forms.
* PDF library is supported in Blazor, Xamarin and Flutter platforms.
* PDF library is compatible with .NET 5.0 applications.

N> 1. Starting with v20.1.0.x, if you reference Syncfusion HTML converter or OCR processor assemblies from trial setup or from the NuGet feed, you also have to include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/overview) to know about registering Syncfusion license key in your application to use our components.
N> 2. The Syncfusion ASP.NET Web Forms components will no longer be actively developed and will be marked as end of support after the 2023 Volume 2 release. However, ASP.NET Web Forms related NuGet's will be updated until then. If you want to use the Syncfusion ASP.NET Web Forms components in the future, you may continue to use till version 2023 Volume 2 release, and bug fixes will be provided as patches as long as Microsoft supports it, even after the 2023 Volume 2 release. It is recommended to use the latest Blazor or ASP.NET Core for new web applications development.
For more details, please refer to this link:https://learn.microsoft.com/en-us/dotnet/architecture/blazor-for-web-forms-developers/introduction. You can also visit the Blazor documentation and demo links provided for more information.
* [Blazor documentation](https://blazor.syncfusion.com/documentation/introduction)
* [Blazor demo](https://blazor.syncfusion.com/demos/)