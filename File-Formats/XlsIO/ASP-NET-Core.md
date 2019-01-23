---
title: ASP.NET Core | Syncfusion
description: Briefs about loading and saving an Excel document in ASP.NET Core platform.
platform: aspnet-core
control: XlsIO
documentation: UG
---

# ASP.NET Core

To use XlsIO in your ASP.NET Core application, please add the required assemblies in the application by referring to [Getting Started](https://help.syncfusion.com/aspnet-core/xlsio/getting-started) section.

## Loading the document

The below code snippet illustrates how to load an Excel file in ASP.NET Core.

{% highlight c# %}
//New instance of ExcelEngine is created 

//Equivalent to launching Microsoft Excel with no workbooks open

//Instantiate the spreadsheet creation engine

ExcelEngine excelEngine = new ExcelEngine();

//Instantiate the Excel application object

IApplication application = excelEngine.Excel;

//Assigns default application version

application.DefaultVersion = ExcelVersion.Excel2013;

//A existing workbook is opened.              

string basePath = _hostingEnvironment.WebRootPath + @"\XlsIO\Sample.xlsx";              

FileStream sampleFile = new FileStream(basePath, FileMode.Open);

IWorkbook workbook = application.Workbooks.Open(sampleFile);

//Access first worksheet from the workbook.

IWorksheet worksheet = workbook.Worksheets[0];             

//Defining the ContentType for excel file.

string ContentType = "Application/msexcel";

//Define the file name.

string fileName = "Output.xlsx";

//Creating stream object.

MemoryStream stream = new MemoryStream();

//Saving the workbook to stream in XLSX format

workbook.SaveAs(stream);

stream.Position = 0;

//Closing the workbook.

workbook.Close();

//Dispose the Excel engine

excelEngine.Dispose();

//Creates a FileContentResult object by using the file contents, content type, and file name.
return File(stream, ContentType, fileName);
{% endhighlight %}

N> _hostingEnvironment is the base path for input files of type IHostingEnvironment.

## Saving the document

The following code snippet illustrates how to save an Excel document in ASP.NET Core.

{% highlight c# %}
//New instance of ExcelEngine is created 

//Equivalent to launching Microsoft Excel with no workbooks open

//Instantiate the spreadsheet creation engine

ExcelEngine excelEngine = new ExcelEngine();

//Instantiate the Excel application object

IApplication application = excelEngine.Excel;

//Assigns default application version

application.DefaultVersion = ExcelVersion.Excel2013;

//A new workbook is created.              

IWorkbook workbook = application.Workbooks.Create(1);

//Access first worksheet from the workbook.

IWorksheet worksheet = workbook.Worksheets[0];             

//Defining the ContentType for excel file.

string ContentType = "Application/msexcel";

//Define the file name.

string fileName = "Output.xlsx";

//Creating stream object.

MemoryStream stream = new MemoryStream();

//Saving the workbook to stream in XLSX format

workbook.SaveAs(stream);

stream.Position = 0;

//Closing the workbook.

workbook.Close();

//Dispose the Excel engine

excelEngine.Dispose();

//Creates a FileContentResult object by using the file contents, content type, and file name.
return File(stream, ContentType, fileName);
{% endhighlight %}