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

//Initialize PDF Document

PdfDocument pdfDocument = new PdfDocument();

//Convert Excel Document into PDF document

pdfDocument = converter.Convert();

//Save the PDF file

pdfDocument.Save("ExcelToPDF.pdf");

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

'Initialize the PDF Document

Dim pdfDocument As PdfDocument = New PdfDocument()

'Convert Excel Document into PDF document

pdfDocument = converter.Convert()

'Save the PDF file

pdfDocument.Save("ExcelToPDF.pdf")

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

//convert the sheet to PDF

ExcelToPdfConverter converter = new ExcelToPdfConverter(sheet);

PdfDocument pdfDocument= new PdfDocument();

pdfDocument = converter.Convert();

pdfDocument.Save("ExcelToPDF.pdf");

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

'Save the PDF file

pdfDocument.Save("ExcelToPDF.pdf")

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

	//Save the PDF file
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

	'Save the PDF file
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

pdfDocument.Save("ExcelToPDF.pdf");

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

pdfDocument.Save("ExcelToPDF.pdf")

converter.Dispose()

pdfDocument.Close()

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  


## Print Excel Document

XlsIO supports Excel printing option by converting Excel to PDF and then print that PDF document. The Excel can be print with specified page setup and printer settings in XlsIO.

The following printer settings can be applied to print Excel in XlsIO. 

![](Excel-to-PDF-Conversion_images/Excel-to-PDF-Conversion_img1.jpg)

 
### Print Excel Document 

The following code snippet illustrates how to print the Excel document in XlsIO.

{% tabs %}  
{% highlight c# %}

ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
IWorkbook workbook = application.Workbooks.Open("Excel.xlsx"));

// Convert the workbook.
ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);
           
// Print the converted PDF document.
converter.Print();

converter.Dispose();
workbook.Close();
excelEngine.Dispose();

{% endhighlight %}
{% highlight vb %}

Dim excelEngine As ExcelEngine = New ExcelEngine
Dim application As IApplication = excelEngine.Excel
Dim workbook As IWorkbook = application.Workbooks.Open("Excel.xlsx")

' Convert the workbook.
Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(workbook)

' Print the converted PDF document.
converter.Print()
converter.Dispose()
workbook.Close()
excelEngine.Dispose()

{% endhighlight %}
{% endtabs %}

### Print with printer settings.

The following code snippet illustrates how to print the Excel document with printer settings in XlsIO.

{% tabs %}  
{% highlight c# %}

ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
IWorkbook workbook = application.Workbooks.Open("Excel.xlsx"));

// Convert the workbook.
ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);

// Initialize the printer settings.
PrinterSettings printerSettings = new PrinterSettings();

// customizing the printer settings.
printerSettings.PrinterName = "HP LaserJet Pro MFP M127-M128 PCLmS";
printerSettings.Copies = 2;
printerSettings.FromPage = 2;
printerSettings.ToPage = 3;
printerSettings.DefaultPageSettings.Color = false;
printerSettings.Duplex = Duplex.Vertical;

// Print the converted PDF document with printer settings.
converter.Print(printerSettings);

converter.Dispose();
workbook.Close();
excelEngine.Dispose();

{% endhighlight %}
{% highlight vb %}

Dim excelEngine As ExcelEngine = New ExcelEngine
Dim application As IApplication = excelEngine.Excel
Dim workbook As IWorkbook = application.Workbooks.Open("Excel.xlsx")

' Convert the workbook.
Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(workbook)

' Initialize the printer settings.
Dim printerSettings As PrinterSettings = New PrinterSettings

' customizing the printer settings.
printerSettings.PrinterName = "HP LaserJet Pro MFP M127-M128 PCLmS"
printerSettings.Copies = 2
printerSettings.FromPage = 2
printerSettings.ToPage = 3
printerSettings.DefaultPageSettings.Color = false
printerSettings.Duplex = Duplex.Vertical

' Print the converted PDF document with printer settings.
converter.Print(printerSettings)

converter.Dispose()
workbook.Close()
excelEngine.Dispose()

{% endhighlight %}
{% endtabs %}

### Print with Excel to PDF converter settings.

The following code snippet illustrates how to print the Excel document with Excel to PDF converter settings in XlsIO.

{% tabs %}  
{% highlight c# %}

ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
IWorkbook workbook = application.Workbooks.Open("Excel.xlsx");

// Convert the workbook.
ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);

// Initializes the Excel to PDF converter setting class.
ExcelToPdfConverterSettings converterSettings = new ExcelToPdfConverterSettings();

// Layout the page using FitAllColumnsOnOnePage options.
converterSettings.DisplayGridLines = GridLinesDisplayStyle.Visible;
converterSettings.LayoutOptions = LayoutOptions.FitAllColumnsOnOnePage;

// Print the converted PDF document with converter settings.
converter.Print(converterSettings);

converter.Dispose();
workbook.Close();
excelEngine.Dispose();

{% endhighlight %}
{% highlight vb %}

Dim excelEngine As ExcelEngine = New ExcelEngine
Dim application As IApplication = excelEngine.Excel
Dim workbook As IWorkbook = application.Workbooks.Open("Excel.xlsx")

' Convert the workbook.
Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(workbook)

' Initialize the Excel to PDF converter setting class.
Dim converterSettings As ExcelToPdfConverterSettings = New ExcelToPdfConverterSettings

' Layout the page using FitAllColumnsOnOnePage options.
converterSettings.DisplayGridLines = GridLinesDisplayStyle.Visible
converterSettings.LayoutOptions = LayoutOptions.FitAllColumnsOnOnePage

' Print the converted PDF document with converter settings.
converter.Print(converterSettings)

converter.Dispose()
workbook.Close()
excelEngine.Dispose()

{% endhighlight %}
{% endtabs %}

### Print with printer settings and Excel to PDF converter settings.

The following code snippet illustrates how to print the Excel document with Excel to PDF converter settings and printer settings in XlsIO.

{% tabs %}  
{% highlight c# %}

ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
IWorkbook workbook = application.Workbooks.Open("Excel.xlsx"));

ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);

// Initialize the printer settings.
PrinterSettings printerSettings = new PrinterSettings();

// customizing the printer settings.
printerSettings.PrinterName = "HP LaserJet Pro MFP M127-M128 PCLmS";
printerSettings.Copies = 2;
printerSettings.FromPage = 2;
printerSettings.ToPage = 3;
printerSettings.DefaultPageSettings.Color = true;
printerSettings.Duplex = Duplex.Vertical;
printerSettings.Collate = true;

// Initializes the Excel to PDF converter setting class.
ExcelToPdfConverterSettings converterSettings = new ExcelToPdfConverterSettings();

// Layout the page using FitAllColumnsOnOnePage options.
converterSettings.DisplayGridLines = GridLinesDisplayStyle.Visible;
converterSettings.LayoutOptions = LayoutOptions.FitAllColumnsOnOnePage;

// Print the converted PDF document with printer settings and converter settings.
converter.Print(printerSettings, converterSettings);

converter.Dispose();
workbook.Close();
excelEngine.Dispose();

{% endhighlight %}
{% highlight vb %}

Dim excelEngine As ExcelEngine = New ExcelEngine
Dim application As IApplication = excelEngine.Excel
Dim workbook As IWorkbook = application.Workbooks.Open("Excel.xlsx")
Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(workbook)

' Initialize the printer settings.
Dim printerSettings As PrinterSettings = New PrinterSettings

' customizing the printer settings.
printerSettings.PrinterName = "HP LaserJet Pro MFP M127-M128 PCLmS"
printerSettings.Copies = 2
printerSettings.FromPage = 2
printerSettings.ToPage = 3
printerSettings.DefaultPageSettings.Color = true
printerSettings.Duplex = Duplex.Vertical
printerSettings.Collate = true

' Initialize the Excel to PDF converter setting class.
Dim converterSettings As ExcelToPdfConverterSettings = New ExcelToPdfConverterSettings

' Layout the page using FitAllColumnsOnOnePage options.
converterSettings.DisplayGridLines = GridLinesDisplayStyle.Visible
converterSettings.LayoutOptions = LayoutOptions.FitAllColumnsOnOnePage

' Print the converted PDF document with printer settings and converter settings.
converter.Print(printerSettings, converterSettings)

converter.Dispose()
workbook.Close()
excelEngine.Dispose()

{% endhighlight %}
{% endtabs %}

  
N> This section is applicable only to the Windows Forms and WPF platforms.

## Supported Elements

This feature provides support for the following elements:

* Styles
* Rich-Text Formatting
* Headers and Footers
* Images
* Text Boxes
* Hyperlinks
* Document Properties
* Table Styles
* Text Rotations
* Excel Page Setup Options
* Unicode
* Print Titles
* Page Breaks
* Print Area
* Print Order
* 2D Charts
* 3D Charts
* AutoShapes
​

## Unsupported Elements

The following list contains unsupported elements that presently will not be preserved in the generated PDF document. 

* Gradient Fill
* Comments
* Sparklines
* Pivot Charts
* SmartArt Graphics
* Different First Page Headers
* Different Odd and Even Pages
* Conditional Formats
	* Data Bars
	* Color Scales
	* Icon Sets
* Tables
	* Custom Styles
* Row and Column Headings
* Form Controls
* ActiveX Controls
* OLE Objects
