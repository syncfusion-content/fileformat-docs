---
title: Conversions
description: Briefs about conversions supported in XlsIO
platform: File-formats
control: XlsIO
documentation: UG
---

# Conversions

## Excel to PDF Conversion

XlsIO allows you to convert an entire workbook or a single worksheet into PDF document. For converting an Excel document to PDF, the following assemblies need to be referenced in your application

* Syncfusion.XlsIO.Base.dll
* Syncfusion.Compression.Base.dll
* Syncfusion.ExcelToPDFConverter.Base.dll
* Syncfusion.ExcelChartToImageConverter.Wpf.dll
* Syncfusion.SfChart.Wpf.dll
* Syncfusion.Shared.Wpf.dll
* Syncfusion.Pdf.Base.dll

### Workbook to PDF

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

To know more about ExcelToPdf conversion settings, please refer ExcelToPdfConverterSettings – LINK API reference

### Worksheet to PDF

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

### Excel with Chart to PDF

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

I> This section is applicable only to the Windows Forms, ASP.Net, MVC and WPF platforms.

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
* Background Images
* Printing Titles when Converting the Excel to PDF
* Page Break Support
* Print Area Support
* Print Order Support
* Unicode in Headers and Footers

​

**Unsupported** **Elements** 

The following list contains unsupported elements that presently will not be preserved in the generated PDF document. 

* Grouping columns
* OLE Objects
* Text rotations
* Background images

## Convert Worksheet to Image 

### Convert as Bitmap

The following code shows how to convert the specified range of rows and columns in the worksheet to bitmap.

{% tabs %}  

{% highlight c# %}
// Convert as bitmap.

Image img = sheet.ConvertToImage(1, 1, 10, 20);

img.Save("Sample.png", ImageFormat.Png);





{% endhighlight %}

{% highlight vb %}
'Convert as bitmap.

Dim img As Image = sheet.ConvertToImage(1, 1, 10, 20)

img.Save("Sample.png", ImageFormat.Png)



{% endhighlight %}

  {% endtabs %}  

### Save as Stream

The following code snippet shows how to save a sheet as stream.

{% tabs %}  

{% highlight c# %}
// Converts and save as stream.

MemoryStream stream = new MemoryStream();

sheet.ConvertToImage(1, 1, 10, 20, ImageType.Metafile, stream);





{% endhighlight %}

{% highlight vb %}
'Converts and save as stream.

Dim stream As MemoryStream = New MemoryStream()

sheet.ConvertToImage(1, 1, 10, 20, ImageType.Metafile, stream)



{% endhighlight %}

  {% endtabs %}  

The complete code snippet of the above options is shown below.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

IWorksheet sheet = workbook.Worksheets[0];

// Convert as bitmap.

Image img = sheet.ConvertToImage(1, 1, 10, 20);

img.Save("Sample.png", ImageFormat.Png);

// Converts and save as stream.

MemoryStream stream = new MemoryStream();

sheet.ConvertToImage(1, 1, 10, 20, ImageType.Metafile, stream);

//Save the workbook to disk.
workbook.SaveAs("Sample.xlsx");

//Close the workbook.
workbook.Close();

//No exception will be thrown if there are unsaved workbooks.
excelEngine.ThrowNotSavedOnDestroy = false;

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As ExcelEngine = New ExcelEngine

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("sample.xlsx", ExcelOpenType.Automatic)

Dim worksheet As IWorksheet = workbook.Worksheets(0)

'Convert as bitmap.

Dim img As Image = sheet.ConvertToImage(1, 1, 10, 20)

img.Save("Sample.png", ImageFormat.Png)

'Converts and save as stream.

Dim stream As MemoryStream = New MemoryStream()

sheet.ConvertToImage(1, 1, 10, 20, ImageType.Metafile, stream)

'Save the workbook to disk.
workbook.SaveAs("Sample.xlsx")

'Close the workbook.
workbook.Close()

'No exception will be thrown if there are unsaved workbooks.
excelEngine.ThrowNotSavedOnDestroy = False

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

**Non****-****Supported** **Features****:**

* Subscript/Superscript
* RTF
* Shrink to fit
* Shapes (except TextBox shape and Image)
* Charts and Chart Worksheet
* Complex conditional formatting
* Gradient fill is partially supported

## Convert Chart to Image 

The following code snippets shows how to converting an Excel Chart to an image using the **ExcelChartToImageConverter** class.

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

application.ChartToImageConverter = new ChartToImageConverter();

application.ChartToImageConverter.ScalingMode = ScalingMode.Best;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");

IWorksheet worksheet = workbook.Worksheets[0];

IChart chart = worksheet.Charts[0];

//Creating the memory stream for chart image.

MemoryStream stream = new MemoryStream();

//Saving the chart as image.

chart.SaveAsImage(stream);

Image image = Image.FromStream(stream);

//Saving image stream to file.

image.Save("Output.png");

//Closing the workbook and disposing the Excel Engine.

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim ChartToImageConverter As chartToImageConverter = New ChartToImageConverter()

application.ChartToImageConverter = chartToImageConverter

application.ChartToImageConverter.ScalingMode = ScalingMode.Best

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")

Dim worksheet As IWorksheet = workbook.Worksheets(0)

Dim chart As IChart = worksheet.Charts(0)

'Creating the memory stream for chart image.

Dim stream As New MemoryStream()

'Saving the chart as image.

chart.SaveAsImage(stream)

Dim image As Image = Image.FromStream(stream)

'Saving image stream to file.

image.Save("Output.png")

'Closing the workbook and disposing the Excel Engine.

workbook.Close()

excelEngine.Dispose()



{% endhighlight %}

  {% endtabs %}  

# 

