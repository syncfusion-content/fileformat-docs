---
title: Excel to PDF Conversion
description: Briefs about Excel to PDF conversion in XlsIO
platform: File-formats
control: XlsIO
documentation: UG
---

# Excel to PDF Conversion

XlsIO allows you to convert an entire workbook or a single worksheet into PDF document. For converting an Excel document to PDF, the following assemblies need to be referenced in your application

* Syncfusion.XlsIO.Base.dll
* Syncfusion.Compression.Base.dll
* Syncfusion.ExcelToPDFConverter.Base.dll
* Syncfusion.ExcelChartToImageConverter.Wpf.dll
* Syncfusion.SfChart.Wpf.dll
* Syncfusion.Pdf.Base.dll

## Workbook to PDF

The following code illustrates how to convert a workbook to PDF Document.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
application.DefaultVersion = ExcelVersion.Excel2013;
IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

//Open the Excel Document to Convert

ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);

//Intialize PDF Document

PdfDocument pdfDocument = new PdfDocument();

//Convert Excel Document into PDF document

pdfDocument = converter.Convert();

//Save the pdf file

pdfDocument.Save("ExceltoPDF.pdf");

//Dispose the objects

pdfDocument.Close();

converter.Dispose();

workbook.Close();

excelEngine.Dispose();         



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

'Open the Excel Document to Convert

Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(workbook)

'Intialize the PDF Document

Dim pdfDocument As PdfDocument = New PdfDocument()

'Convert Excel Document into PDF document

pdfDocument = converter.Convert()

'Save the pdf file

pdfDocument.Save("ExceltoPDF.pdf")

'Dispose the objects

pdfDocument.Close()

converter.Dispose()

workbook.Close()

excelEngine.Dispose()       





{% endhighlight %}

  {% endtabs %}  

To know more about different conversion settings in Excel to PDF conversion, please refer ExcelToPdfConverterSettings in API section.

## Worksheet to PDF

The following code shows how to convert a particular sheet to PDF Document.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

IWorksheet sheet = workbook.Worksheets[0];

//convert the sheet to pdf

ExcelToPdfConverter converter = new ExcelToPdfConverter(sheet);

PdfDocument pdfDocument= new PdfDocument();

pdfDocument = converter.Convert();

pdfDocument.Save("ExceltoPDF.pdf");

pdfDocument.Close();

converter.Dispose();

workbook.Close();
excelEngine.Dispose();         



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

Dim sheet As IWorksheet = workbook.Worksheets(0)

'Converts the particular sheet 

Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(sheet)

Dim pdfDocument As PdfDocument = New PdfDocument()

pdfDocument = converter.Convert()

'Save the pdf file

pdfDocument.Save("ExceltoPDF.pdf")

'Dispose the objects

pdfDocument.Close()

converter.Dispose()

workbook.Close()

excelEngine.Dispose()    





{% endhighlight %}

  {% endtabs %}  

**Creating** **individual** **PDF** **document** **for** **each** **worksheet**

The following code snippet shows how to create an individual PDF document for each worksheet in a workbook.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

PdfDocument pdfDocument = new PdfDocument();     

foreach (IWorksheet sheet in workbook.Worksheets)

{

ExcelToPdfConverter converter = new ExcelToPdfConverter(sheet);

pdfDocument = converter.Convert();

//Save the pdf file

pdfDocument.Save(sheet.Name+".pdf");

converter.Dispose();

}

//Dispose the objects

pdfDocument.Close();

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")

Dim pdfDocument As New PdfDocument()

For Each sheet As IWorksheet In workbook.Worksheets

Dim converter As New ExcelToPdfConverter(sheet)

PdfDocument = converter.Convert()

'Save the pdf file

PdfDocument.Save(sheet.Name + ".pdf")

converter.Dispose()

Next

pdfDocument.Close()

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}
  
## Excel with Chart to PDF

To preserve the charts during Excel to PDF conversion, you should initialize the ChartToImageConverter of **IApplication** interface, otherwise the charts present in worksheet will get skipped. The following code illustrate how to convert an Excel with chart to PDF document.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

// Instantiating the ChartToImageConverter and 

//Assigning the ChartToImageConverter instance of XlsIO application

application.ChartToImageConverter = new ChartToImageConverter();

// Tuning Chart Image Quality.

application.ChartToImageConverter.ScalingMode = ScalingMode.Best;

IWorkbook workbook = application.Workbooks.Open("chart.xlsx");

IWorksheet worksheet = workbook.Worksheets[0];

ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);

PdfDocument pdfDocument = new PdfDocument();

pdfDocument = converter.Convert();

pdfDocument.Save("ExceltoPDF.pdf");

converter.Dispose();

pdfDocument.Close();

workbook.Close();

excelEngine.Dispose();         



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

' Instantiating the ChartToImageConverter and

'Assigning the ChartToImageConverter instance of XlsIO application

application.ChartToImageConverter = New ChartToImageConverter()

' Tuning Chart Image Quality.

application.ChartToImageConverter.ScalingMode = ScalingMode.Best

Dim workbook As IWorkbook = application.Workbooks.Open("chart.xlsx")

Dim worksheet As IWorksheet = workbook.Worksheets(0)

Dim converter As New ExcelToPdfConverter(workbook)

Dim pdfDocument As New PdfDocument()

pdfDocument = converter.Convert()

pdfDocument.Save("ExceltoPDF.pdf")

converter.Dispose()

pdfDocument.Close()

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

N> This section is applicable only to the Windows Forms, ASP.NET, ASP.NET MVC and WPF platforms.

**Supported** **Elements**

This feature provides support for the following elements:

* Styles
* Character formatting
* Headers  and footers
* Images
* Text box
* Hyperlinks
* Document properties
* Comments
* Encryption
* Table Style Support
* Text Rotations
* Excel Page Setup Options
* Unicode Support
* Printing Titles when Converting the Excel to PDF
* Page Break Support
* Print Area Support
* Print Order Support
* Unicode in Headers and Footers
* 2D Charts
* 3D Charts

​

**Unsupported** **Elements** 

The following list contains unsupported elements that presently will not be preserved in the generated PDF document. 

* Gradient Fill
* Sparklines
* Pivot Chart
* SmartArt
* Different First Page
* Different Odd and Even Pages
* Conditional Formats
	* Data Bars
	* Color Scales
	* Icon Sets
* Table
	* Custom Style
* Heading
* Form Controls
* ActiveX Controls
* Grouping Columns
* OLE Objects
* Background images
* AutoShapes