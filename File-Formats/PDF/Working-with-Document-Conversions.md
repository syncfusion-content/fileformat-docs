---
title: Working with Document Conversion in .NET PDF Library | Syncfusion
description: This section explains converting other document types such as Word, Excel, RTF, TIFF, XPS, and HTML to PDF.
platform: file-formats
control: PDF
documentation: UG
---
# Working with Document Conversions in File Formats PDF 

## Converting Word documents to PDF

Essential PDF allows you to convert a Word document into PDF. For converting a Word document to PDF, the following assemblies need to be referenced in your application.

<table>
<thead>
<tr>
<th>
Assembly Name<br/><br/></th><th>
Description<br/><br/></th></tr>
</thead>
<tbody>
<tr>
<td>
Syncfusion.DocIO.Base<br/><br/></td><td>
This assembly has the core features for creating and manipulating Word documents.<br/><br/></td></tr>
<tr>
<td>
Syncfusion.Compression.Base<br/><br/></td><td>
This assembly is used to package the Word documents<br/><br/></td></tr>
<tr>
<td>
Syncfusion.DocToPdfConverter.Base<br/><br/></td><td>
This assembly is needed for converting the Word document to PDF.<br/><br/></td></tr>
<tr>
<td>
Syncfusion.Pdf.Base<br/><br/></td><td>
This assembly has the core features for creating PDF file.<br/><br/></td></tr>
<tr>
<td>
Syncfusion.OfficeChart.Base<br/><br/></td><td>
This assembly has features to work with chart in Word document.<br/><br/></td></tr>
</tbody>
</table>

The following assemblies are need to be referred in addition to the above mentioned assemblies for converting the chart present in the Word document into PDF.

<table>
<thead>
<tr>
<th>
Assembly Name<br/><br/></th><th>
Description<br/><br/></th></tr>
</thead>
<tbody>
<tr>
<td>
Syncfusion.OfficeChartToImageConverter.WPF<br/><br/></td><td>
This assembly is used to convert the chart to image.<br/><br/></td></tr>
<tr>
<td>
Syncfusion.SfChart.WPF<br/><br/></td><td>
This is supporting assembly for Syncfusion.OfficeChartToImageConverter.WPF<br/><br/></td></tr>
<tr>
<td>
Syncfusion.Shared.WPF<br/><br/></td><td>
This is supporting assembly for Syncfusion.OfficeChartToImageConverter.WPF<br/><br/></td></tr>
</tbody>
</table>

The following namespaces are required to compile the code in this topic.

For Windows Forms, WPF, ASP.NET and ASP.NET MVC applications
* using Syncfusion.OfficeChart
* using Syncfusion.DocIO
* using Syncfusion.DocIO.DLS
* using Syncfusion.DocToPDFConverter
* using Syncfusion.Pdf
* using Syncfusion.OfficeChartToImageConverter

For ASP.NET Core and Xamarin applications 
* using Syncfusion.DocIO
* using Syncfusion.DocIO.DLS
* using Syncfusion.DocIORenderer
* using Syncfusion.Pdf

[DocToPDFConverter](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocToPDFConverter.DocToPDFConverter.html) class is responsible for converting a Word document into PDF. The following code snippet illustrates how to convert a Word document into PDF document.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

// Open the file as Stream.
FileStream docStream = new FileStream(@"Template.docx", FileMode.Open, FileAccess.Read);
//Loads file stream into Word document.
WordDocument wordDocument = new WordDocument(docStream, Syncfusion.DocIO.FormatType.Automatic);
//Instantiation of DocIORenderer for Word to PDF conversion.
DocIORenderer render = new DocIORenderer();
//Converts Word document into PDF document.
PdfDocument pdfDocument = render.ConvertToPDF(wordDocument);
//Releases all resources used by the Word document and DocIO Renderer objects.
render.Dispose();
wordDocument.Dispose();

//Save the document into stream.
MemoryStream stream = new MemoryStream();
pdfDocument.Save(stream);
//Close the document.
pdfDocument.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Load an existing Word document.
WordDocument wordDocument = new WordDocument("Template.docx", FormatType.Docx);
//Initialize chart to image converter for converting charts during Word to pdf conversion.
wordDocument.ChartToImageConverter = new ChartToImageConverter();
//Create an instance of DocToPDFConverter.
DocToPDFConverter converter = new DocToPDFConverter();
//Convert Word document into PDF document.
PdfDocument pdfDocument = converter.ConvertToPDF(wordDocument);

//Save the PDF file.
pdfDocument.Save("WordtoPDF.pdf");
//Close the instance of document objects.
pdfDocument.Close(true);
wordDocument.Close();

{% endhighlight %}


{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Load an existing Word document
Dim wordDocument As New WordDocument("Template.docx", FormatType.Docx)
'Initialize chart to image converter for converting charts during Word to pdf conversion
wordDocument.ChartToImageConverter = New ChartToImageConverter()
'Create an instance of DocToPDFConverter
Dim converter As New DocToPDFConverter()
'Convert Word document into PDF document
Dim pdfDocument As PdfDocument = converter.ConvertToPDF(wordDocument)

'Save the PDF file
pdfDocument.Save("WordtoPDF.pdf")
'Close the instance of document objects
pdfDocument.Close(True)
wordDocument.Close()

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Document%20conversion/Word-to-PDF/Converting-Word-to-PDF-document).

Note:
* Initializing the [ChartToImageConverter](https://help.syncfusion.com/cr/file-formats/Syncfusion.OfficeChartToImageConverter.ChartToImageConverter.html) is mandatory to convert the charts present in the Word document to PDF. Otherwise the charts will not be exported to the converted PDF.
* [ChartToImageConverter](https://help.syncfusion.com/cr/file-formats/Syncfusion.OfficeChartToImageConverter.ChartToImageConverter.html) is supported from .NET Framework 4.0 onwards.
* Total number of pages may vary  based on unsupported elements in the converted PDF document when compare to Word document.

### Customizing the Word document to PDF conversion

Essential DocIO allows you to customize the Word to PDF conversion using [DocToPDFConverter](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocToPDFConverter.DocToPDFConverter.html) class with the below options:

* Allows to determine the quality of the charts in the converted PDF.
* Allows to determine the quality of the JPEG images in the converted PDF.
* Allows to reduce the Main Memory usage in Word to PDF conversion by reusing the identical images.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

//PDF doesn't support customizing the Word document C#.NET Cross platforms.

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Loads an existing Word document.
WordDocument wordDocument = new WordDocument("Sample_Image.docx", FormatType.Docx);
//Initialize chart to image converter for converting charts during Word to pdf conversion.
wordDocument.ChartToImageConverter = new ChartToImageConverter();
//Set the scaling mode for charts.
wordDocument.ChartToImageConverter.ScalingMode = ScalingMode.Normal;

//create an instance of DocToPDFConverter - responsible for Word to PDF conversion.
DocToPDFConverter converter = new DocToPDFConverter();
//Set the image quality.
converter.Settings.ImageQuality = 100;
//Set the image resolution.
converter.Settings.ImageResolution = 640;
//Set true to optimize the memory usage for identical images.
converter.Settings.OptimizeIdenticalImages = true;
//Convert Word document into PDF document.
PdfDocument pdfDocument = converter.ConvertToPDF(wordDocument);

//Save the PDF file to file system.
pdfDocument.Save("WordtoPDF.pdf");
//close the instance of document objects.
pdfDocument.Close(true);
wordDocument.Close();

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Loads an existing Word document
Dim wordDocument As New WordDocument("Sample_Image.docx", FormatType.Docx)
'Initialize chart to image converter for converting charts during Word to pdf conversion
wordDocument.ChartToImageConverter = New ChartToImageConverter()
'Set the scaling mode for charts
wordDocument.ChartToImageConverter.ScalingMode = ScalingMode.Normal

'create an instance of DocToPDFConverter - responsible for Word to PDF conversion
Dim converter As New DocToPDFConverter()
'Set the image quality
converter.Settings.ImageQuality = 100
'Set the image resolution
converter.Settings.ImageResolution = 640
'Set true to optimize the memory usage for identical images
converter.Settings.OptimizeIdenticalImages = True
'Convert Word document into PDF document
Dim pdfDocument As PdfDocument = converter.ConvertToPDF(wordDocument)

'Save the PDF file to file system
pdfDocument.Save("WordtoPDF.pdf")
'close the instance of document objects
pdfDocument.Close(True)
wordDocument.Close()

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Document%20conversion/Word-to-PDF/Customizing-the-Word-to-PDF-conversion).

## Converting Excel documents to PDF

[ExcelToPdfConverter](https://help.syncfusion.com/cr/file-formats/Syncfusion.ExcelToPDFConverter.Base~Syncfusion.ExcelToPdfConverter.ExcelToPdfConverter.html) is responsible for converting an Excel document into PDF. Essential PDF allows you to convert an entire workbook or a single worksheet into PDF document. Refer to the following links for assemblies/nuget packages required based on platforms to convert Excel document into PDF. 

* [Assemblies Information](https://help.syncfusion.com/file-formats/pdf/assemblies-required#converting-excel-document-to-pdf)
* [NuGet Information](https://help.syncfusion.com/file-formats/pdf/nuget-packages-required#converting-excel-document-to-pdf)

N> Excel to PDF conversion works proper in Blazor server-side alone and not in client-side.

### Converting a Workbook to PDF

The following code illustrates how to convert a workbook to PDF Document using [IWorkbook](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbook.html) type in [ExcelToPdfConverter](https://help.syncfusion.com/cr/file-formats/Syncfusion.ExcelToPdfConverter.ExcelToPdfConverter.html#Syncfusion_ExcelToPdfConverter_ExcelToPdfConverter__ctor_Syncfusion_XlsIO_IWorkbook_) class.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  //Load the document.
  FileStream excelStream = new FileStream("ExcelToPDF.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(excelStream);
  //Initialize XlsIO renderer.
  XlsIORenderer renderer = new XlsIORenderer();
  //Convert Excel document into PDF document.
  PdfDocument pdfDocument = renderer.ConvertToPDF(workbook);

  //Save the PDF document to stream.
  Stream stream = new FileStream("ExcelToPDF.pdf", FileMode.Create, FileAccess.ReadWrite);
  pdfDocument.Save(stream);
  //Dispose the stream.
  excelStream.Dispose();
  stream.Dispose();
}

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);
  //Open the Excel document to Convert.
  ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);
  //Initialize PDF document.
  PdfDocument pdfDocument = new PdfDocument();
  //Convert Excel document into PDF document.
  pdfDocument = converter.Convert();

  //Save the PDF file.
  pdfDocument.Save("ExcelToPDF.pdf");
}

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)
  'Open the Excel document to convert
  Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(workbook)
  'Initialize the PDF document
  Dim pdfDocument As PdfDocument = New PdfDocument()
  'Convert Excel document into PDF document
  pdfDocument = converter.Convert()

  'Save the PDF file
  pdfDocument.Save("ExcelToPDF.pdf")
End Using

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Document%20conversion/Excel-to-PDF/Convert-workbook-to-PDF-document).

### Converting a Worksheet to PDF

The following code shows how to convert a particular sheet to PDF Document using [IWorksheet](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorksheet.html) type in [ExcelToPdfConverter](https://help.syncfusion.com/cr/file-formats/Syncfusion.ExcelToPdfConverter.ExcelToPdfConverter.html#Syncfusion_ExcelToPdfConverter_ExcelToPdfConverter__ctor_Syncfusion_XlsIO_IWorksheet_) class.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream excelStream = new FileStream("ExcelToPDF.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(excelStream);
  IWorksheet worksheet = workbook.Worksheets[0];
   
  //Initialize XlsIO renderer.
  XlsIORenderer renderer = new XlsIORenderer();
  //Convert Excel document into PDF document. 
  PdfDocument pdfDocument = renderer.ConvertToPDF(worksheet);

  //Saving the PDF to the MemoryStream.
  Stream stream = new FileStream("ExcelToPDF.pdf", FileMode.Create, FileAccess.ReadWrite);
  pdfDocument.Save(stream);
  //Dispose the stream.
  excelStream.Dispose();
  stream.Dispose();
}

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

Using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);
  IWorksheet sheet = workbook.Worksheets[0];

  //convert the sheet to PDF.
  ExcelToPdfConverter converter = new ExcelToPdfConverter(sheet);
  //Initialize PDF document.
  PdfDocument pdfDocument= new PdfDocument();
  //Convert Excel document into PDF document.
  pdfDocument = converter.Convert();

  //Save the PDF file.
  pdfDocument.Save("ExcelToPDF.pdf");       
}

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Converts the particular sheet. 
  Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(sheet)
  'Initialize PDF document.
  Dim pdfDocument As PdfDocument = New PdfDocument()
  'Convert Excel document into PDF document.
  pdfDocument = converter.Convert()

  'Save the PDF file.
  pdfDocument.Save("ExcelToPDF.pdf")
End Using

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Document%20conversion/Excel-to-PDF/Converting-a-worksheet-to-PDF-document).

### Creating individual PDF document for each worksheet

The following code snippet shows how to create an individual PDF document for each worksheet in a workbook using [ExcelToPdfConverter](https://help.syncfusion.com/cr/file-formats/Syncfusion.ExcelToPdfConverter.ExcelToPdfConverter.html#Syncfusion_ExcelToPdfConverter_ExcelToPdfConverter__ctor_Syncfusion_XlsIO_IWorksheet_) class.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream excelStream = new FileStream("ExcelToPDF.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(excelStream);
   
  //Initialize XlsIO renderer.
  XlsIORenderer renderer = new XlsIORenderer();
  //Create a new PDF document.
  PdfDocument pdfDocument = new PdfDocument();         	
  foreach (IWorksheet sheet in workbook.Worksheets)
  {
    pdfDocument = renderer.ConvertToPDF(sheet);
   
    //Save the PDF file.
    Stream stream = new FileStream(sheet.Name+".pdf", FileMode.Create, FileAccess.ReadWrite);
    pdfDocument.Save(stream);
    stream.Dispose();
  }
  excelStream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

Using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

  //Create a new PDF document.
  PdfDocument pdfDocument = new PdfDocument();     
  foreach (IWorksheet sheet in workbook.Worksheets)
  {
    //Open the Excel document to Convert.
    ExcelToPdfConverter converter = new ExcelToPdfConverter(sheet);
    pdfDocument = converter.Convert();

    //Save the PDF file.
    pdfDocument.Save(sheet.Name +".pdf");
    converter.Dispose();
  }
}

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")

  'Create a new PDF document.
  Dim pdfDocument As New PdfDocument()
  For Each sheet As IWorksheet In workbook.Worksheets
    'Open the Excel document to Convert.
    Dim converter As New ExcelToPdfConverter(sheet)
    PdfDocument = converter.Convert()

    'Save the PDF file.
    PdfDocument.Save(sheet.Name + ".pdf")
    converter.Dispose()
  Next
End Using

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Document%20conversion/Excel-to-PDF/Creating-individual-PDF-document-for-each-worksheet).

### Excel with Chart to PDF

To preserve the charts during Excel to PDF conversion, you should initialize the [ChartToImageConverter](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IApplication.html#Syncfusion_XlsIO_IApplication_ChartToImageConverter) of [IApplication](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.Base~Syncfusion.XlsIO.IApplication.html) interface, otherwise the charts present in worksheet will get skipped. The following code illustrate how to convert an Excel with chart to PDF document.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;   
  //Initialize XlsIO renderer.
  XlsIORenderer renderer = new XlsIORenderer();
  //Load the document as stream.
  FileStream excelStream = new FileStream("chart.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(excelStream);

  //Convert Excel document with charts into PDF document. 
  PdfDocument pdfDocument = renderer.ConvertToPDF(workbook);

  //Save the PDF document.
  Stream stream = new FileStream("ExcelToPDF.pdf", FileMode.Create, FileAccess.ReadWrite);
  pdfDocument.Save(stream);
  //Dispose the stream.
  excelStream.Dispose();
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

Using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  //Instantiating the ChartToImageConverter and assigning the ChartToImageConverter instance of XlsIO application.
  application.ChartToImageConverter = new ChartToImageConverter();
  //Tuning chart image quality.
  application.ChartToImageConverter.ScalingMode = ScalingMode.Best;
  IWorkbook workbook = application.Workbooks.Open("chart.xlsx");
  IWorksheet worksheet = workbook.Worksheets[0];

  //Open the Excel document to Convert.
  ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);

  //Initialize PDF document.
  PdfDocument pdfDocument = new PdfDocument();
  //Convert Excel document into PDF document.
  pdfDocument = converter.Convert();
  //Save the PDF file.
  pdfDocument.Save("ExcelToPDF.pdf");
}

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  'Instantiating the ChartToImageConverter and assigning the ChartToImageConverter instance of XlsIO application.
  application.ChartToImageConverter = New ChartToImageConverter()
  'Tuning chart image quality.
  application.ChartToImageConverter.ScalingMode = ScalingMode.Best
  Dim workbook As IWorkbook = application.Workbooks.Open("chart.xlsx")
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Open the Excel document to Convert.
  Dim converter As New ExcelToPdfConverter(workbook)
  
  'Initialize PDF document.
  Dim pdfDocument As New PdfDocument()
  'Convert Excel document into PDF document.
  pdfDocument = converter.Convert()
  'Save the PDF file.
  pdfDocument.Save("ExcelToPDF.pdf")
End Using

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Document%20conversion/Excel-to-PDF/Converting-Excel-with-chart-to-PDF-document).

### Supported Elements

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

### Unsupported Elements

The following list contains unsupported elements that presently will not be preserved in the generated PDF document.

* Grouping columns
* OLE Objects
* Text rotations
* Background images

## Converting RTF documents to PDF

Essential PDF allows you to convert a RTF to PDF document. For converting a RTF to PDF, the following assemblies need to be referenced in your application.

<table>
<thead>
<tr>
<th>
Assembly Name<br/><br/></th><th>
Description<br/><br/></th></tr>
</thead>
<tbody>
<tr>
<td>
Syncfusion.DocIO.Base<br/><br/></td><td>
This assembly has the core features for creating and manipulating RTF documents.<br/><br/></td></tr>
<tr>
<td>
Syncfusion.Compression.Base<br/><br/></td><td>
This assembly is used to package the RTF documents<br/><br/></td></tr>
<tr>
<td>
Syncfusion.DocToPdfConverter.Base<br/><br/></td><td>
This assembly is needed for converting the RTF to PDF.<br/><br/></td></tr>
<tr>
<td>
Syncfusion.Pdf.Base<br/><br/></td><td>
This assembly has the core features for creating PDF file.<br/><br/></td></tr>
</tbody>
</table>

The following namespaces are required to compile the code in this topic.

For Windows Forms, WPF, ASP.NET and ASP.NET MVC applications
* using Syncfusion.DocIO
* using Syncfusion.DocIO.DLS
* using Syncfusion.DocToPDFConverter
* using Syncfusion.Pdf

For ASP.NET Core and Xamarin applications 
* using Syncfusion.DocIO
* using Syncfusion.DocIO.DLS
* using Syncfusion.DocIORenderer
* using Syncfusion.Pdf

[DocToPDFConverter](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocToPDFConverter.Base~Syncfusion.DocToPDFConverter.DocToPDFConverter.html) class is responsible for converting a RTF to PDF. The following code snippet illustrates how to convert a RTF to PDF document.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Open the file as Stream
FileStream docStream = new FileStream(@"Input.rtf", FileMode.Open, FileAccess.Read);
//Loads file stream into Word document
WordDocument wordDocument = new WordDocument(docStream, Syncfusion.DocIO.FormatType.Automatic);
//Instantiation of DocIORenderer for Word to PDF conversion
DocIORenderer render = new DocIORenderer();
//Converts Word document into PDF document
PdfDocument pdfDocument = render.ConvertToPDF(wordDocument);

//Releases all resources used by the Word document and DocIO Renderer objects
render.Dispose();
wordDocument.Dispose();

//Save the document into stream
MemoryStream stream = new MemoryStream();
pdfDocument.Save(stream);
//Close the document
pdfDocument.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Load an existing RTF document.
WordDocument rtfDocument = new WordDocument(inputFileName);
//Create an instance of DocToPDFConverter.
DocToPDFConverter converter = new DocToPDFConverter();
//Convert Word document into PDF document.
PdfDocument pdfDocument = converter.ConvertToPDF(rtfDocument);

//Save the PDF file.
pdfDocument.Save("RTFToPDF.pdf");
//Close the instance of document objects.
pdfDocument.Close(true);
rtfDocument.Close();

{% endhighlight %}


{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Load an existing Word document
Dim rtfDocument As New WordDocument(inputFileName)
'Create an instance of DocToPDFConverter
Dim converter As New DocToPDFConverter()
'Convert Word document into PDF document
Dim pdfDocument As PdfDocument = converter.ConvertToPDF(rtfDocument)

'Save the PDF file
pdfDocument.Save("RTFToPDF.pdf")
'Close the instance of document objects
pdfDocument.Close(True)
rtfDocument.Close()

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Document%20conversion/RTF-to-PDF/Convert-RTF-to-PDF-document).

N> Total number of pages may vary  based on unsupported elements in the converted PDF document when compare to RTF document.

### Customizing the RTF to PDF conversion

Essential DocIO allows you to customize the RTF to PDF conversion using [DocToPDFConverter](https://help.syncfusion.com/cr/file-formats/Syncfusion.DocToPDFConverter.DocToPDFConverter.html) class with the below options:

* Allows to determine the quality of the JPEG images in the converted PDF.
* Allows to reduce the Main Memory usage in RTF to PDF conversion by reusing the identical images.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

//PDF doesn't support customizing the RTF to PDF conversion C#.NET Cross platforms.

{% endhighlight %}
{% highlight c# tabtitle="C# [Windows-specific]" %}

//Loads an existing Word document
WordDocument rtfDocument = new WordDocument(inputFileName);
//create an instance of DocToPDFConverter - responsible for Word to PDF conversion
DocToPDFConverter converter = new DocToPDFConverter();
//Set the image quality
converter.Settings.ImageQuality = 100;
//Set the image resolution
converter.Settings.ImageResolution = 640;
//Set true to optimize the memory usage for identical images
converter.Settings.OptimizeIdenticalImages = true;
//Convert Word document into PDF document
PdfDocument pdfDocument = converter.ConvertToPDF(rtfDocument);

//Save the PDF file to file system
pdfDocument.Save("RTFToPDF.pdf");
//close the instance of document objects
pdfDocument.Close(true);
rtfDocument.Close();

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Loads an existing Word document
Dim rtfDocument As New WordDocument(inputFileName)
'create an instance of DocToPDFConverter - responsible for Word to PDF conversion
Dim converter As New DocToPDFConverter()
'Set the image quality
converter.Settings.ImageQuality = 100
'Set the image resolution
converter.Settings.ImageResolution = 640
'Set true to optimize the memory usage for identical images
converter.Settings.OptimizeIdenticalImages = True
'Convert Word document into PDF document
Dim pdfDocument As PdfDocument = converter.ConvertToPDF(rtfDocument)

'Save the PDF file to file system
pdfDocument.Save("RTFToPDF.pdf")
'close the instance of document objects
pdfDocument.Close(True)
rtfDocument.Close()

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Document%20conversion/RTF-to-PDF/Customizing-the-RTF-to-PDF-document).

## Converting TIFF to PDF

### Converting multi page TIFF to PDF

Multi frame TIFF image can be converted to PDF document using [PdfBitmap](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.PdfBitmap.html) class. This can be done by accessing each frame of the multi frame TIFF image and rendering it in each page of the PDF document.

The code snippet to illustrate the same is given below.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Create a new PDF document
PdfDocument document = new PdfDocument();

//Load the multi frame TIFF image from the disk
FileStream imageStream = new FileStream("image.tiff", FileMode.Open, FileAccess.Read);
PdfTiffImage tiffImage = new PdfTiffImage(imageStream);
//Get the frame count
int frameCount = tiffImage.FrameCount;
//Access each frame and draw into the page
for (int i = 0; i < frameCount; i++)
{
	//Add a section to the PDF document
	PdfSection section = document.Sections.Add();
	//Set page margins
	section.PageSettings.Margins.All = 0;
	tiffImage.ActiveFrame = i;
	//Create a PDF unit converter instance
	PdfUnitConvertor converter = new PdfUnitConvertor();
	//Convert to point
	Syncfusion.Drawing.SizeF size = converter.ConvertFromPixels(tiffImage.PhysicalDimension, PdfGraphicsUnit.Point);
	//Set page orientation
	section.PageSettings.Orientation = (size.Width > size.Height) ? PdfPageOrientation.Landscape : PdfPageOrientation.Portrait;
	//Set page size
	section.PageSettings.Size = size;
	//Add a page to the section
	PdfPage page = section.Pages.Add();
	//Draw TIFF image into the PDF page
	page.Graphics.DrawImage(tiffImage, Syncfusion.Drawing.PointF.Empty, size);
}

//Creating the stream object
MemoryStream stream = new MemoryStream();
//Save the document as stream
document.Save(stream);
//Close the document
document.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Create a PDF document
PdfDocument pdfDocument = new PdfDocument();

//Load multi frame TIFF image
PdfBitmap tiffImage = new PdfBitmap("image.tiff");
//Get the frame count
int frameCount = tiffImage.FrameCount;
//Access each frame and draw into the page
for (int i = 0; i < frameCount; i++)
{
	tiffImage.ActiveFrame = i;
	//Add a section to the PDF document
	PdfSection section = pdfDocument.Sections.Add();
	//Set page margins
	section.PageSettings.Margins.All = 0;
	//Create a PDF unit converter instance
	PdfUnitConvertor converter = new PdfUnitConvertor();
	//Convert to point
	SizeF size = converter.ConvertFromPixels(tiffImage.PhysicalDimension, PdfGraphicsUnit.Point);
	//Set page orientation
	section.PageSettings.Orientation = (size.Width > size.Height) ? PdfPageOrientation.Landscape : PdfPageOrientation.Portrait;
	//Set page size
	section.PageSettings.Size = size;
	//Add a page to the section
	PdfPage page = section.Pages.Add();
	//Draw TIFF image into the PDF page
	page.Graphics.DrawImage(tiffImage, PointF.Empty, size);
}

//Save and close the document
pdfDocument.Save("Sample.pdf");
pdfDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Create a PDF document
Dim pdfDocument As New PdfDocument()

'Load multi frame TIFF image
Dim tiffImage As New PdfBitmap("image.tiff")
'Get the frame count
Dim frameCount As Integer = tiffImage.FrameCount
'Access each frame and draw into the page
For i As Integer = 0 To frameCount - 1
  tiffImage.ActiveFrame = i
  'Add a section to the PDF document
  Dim section As PdfSection = pdfDocument.Sections.Add()
  'Set page margins
  section.PageSettings.Margins.All = 0
  'Create a PDF unit converter instance
  Dim converter As New PdfUnitConvertor()
  'Convert to point
  Dim size As SizeF = converter.ConvertFromPixels(tiffImage.PhysicalDimension, PdfGraphicsUnit.Point)
  'Set page orientation
  If size.Width > size.Height Then section.PageSettings.Orientation = PdfPageOrientation.Landscape
  'Set page size
  section.PageSettings.Size = size
  'Add a page to the section
  Dim page As PdfPage = section.Pages.Add()
  'Draw TIFF image into the PDF page
  page.Graphics.DrawImage(tiffImage, PointF.Empty, size)
Next

'Save and close the document
pdfDocument.Save("Sample.pdf")
pdfDocument.Close(True)

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Document%20conversion/TIFF-to-PDF/Converting-multipage-TIFF-to-PDF-document).

N> 1. Essential PDF supports converting TIFF to PDF with [Syncfusion.Pdf.Imaging.Portable](https://www.nuget.org/packages/Syncfusion.Pdf.Imaging.Net.Core) assembly reference in ASP.NET Core.

### Compression in monochrome images

Essential PDF supports JBIG2 compression for best compression of monochrome images.

Refer the below code snippet to draw a single frame monochrome TIFF image with JBIG2 compression using [EncodingType](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Graphics.EncodingType.html) Enum.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

//PDF doesn't support compressing monochrome images C#.NET Cross platforms.

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Create a PDF document
PdfDocument pdfDocument = new PdfDocument();
//Add a page
PdfPage page = pdfDocument.Pages.Add();

//Load single frame TIFF image
PdfBitmap tiffImage = PdfImage.FromFile("image.tiff") as PdfBitmap;
//Set encode type
tiffImage.Encoding = EncodingType.JBIG2;
//Draw an image
page.Graphics.DrawImage(tiffImage, 0, 0, page.GetClientSize().Width, page.GetClientSize().Height);

//Save and close the document
pdfDocument.Save("Sample.pdf");
pdfDocument.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Create a PDF document
Dim pdfDocument As New PdfDocument()
'Add a page
Dim page As PdfPage = pdfDocument.Pages.Add()

'Load single frame TIFF image
Dim tiffImage As PdfBitmap = TryCast(PdfImage.FromFile("image.tiff"), PdfBitmap)
'Set encode type
tiffImage.Encoding = EncodingType.JBIG2
'Draw an image
page.Graphics.DrawImage(tiffImage, 0, 0, page.GetClientSize().Width, page.GetClientSize().Height)

'Save and close the document
pdfDocument.Save("Sample.pdf")
pdfDocument.Close(True)

{% endhighlight %}
{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Document%20conversion/TIFF-to-PDF/Compression-in-monochrome-images).

N> 1. Currently the JBIG2Decode compression is supported only in lossy mode and also only single frame TIFF images are supported.
N> 2. By default, all monochrome images will be compressed in CITTT4 compression.

## Converting XPS document to PDF

The XPS (XML Paper Specification) document format is a fixed document format which consists of structured XML markup that defines the layout of a document and the visual appearance of each page, along with rendering rules for distributing, archiving, rendering, processing and printing the documents.

Essential PDF provides support for converting XPS to PDF using [XPSToPdfConverter](https://help.syncfusion.com/cr/file-formats/Syncfusion.Pdf.Base~Syncfusion.XPS.XPSToPdfConverter.html) class.

The below code illustrates how to convert XPS to PDF.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Initialize XPS to PDF converter.
XPSToPdfConverter converter = new XPSToPdfConverter();
//Open the XPS file as stream.
FileStream fileStream = new FileStream("Input.xps", FileMode.Open, FileAccess.ReadWrite);
//Convert the XPS to PDF.
PdfDocument document = converter.Convert(fileStream);

//Creating the stream object.
MemoryStream stream = new MemoryStream(); 
//Save the document into stream.
document.Save(stream); 
//Close the documents.
document.Close(true); 

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Create converter class
XPSToPdfConverter converter = new XPSToPdfConverter();
//Convert the XPS to PDF
PdfDocument document = converter.Convert(xpsFileName);

//Save and close the document
document.Save("Sample.pdf");
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Create converter class
Dim converter As New XPSToPdfConverter()
'Convert the XPS to PDF
Dim document As PdfDocument = converter.Convert(xpsFileName)

'Save and close the document
document.Save("Sample.pdf")
document.Close(True)

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Document%20conversion/Converting-XPS-to-PDF-document).

N> Essential PDF supports converting XPS to PDF with [Syncfusion.XpsToPdfConverter.Net.Core](https://www.nuget.org/packages/Syncfusion.XpsToPdfConverter.Net.Core) package reference in .NET Core application.

### Supported Elements

The below table shows the list of elements supported in XPS during the conversion.

<table>
<thead>
<tr>
<th>
Element<br/><br/></th><th>
Convert to PDF<br/><br/></th></tr>
</thead>
<tbody>
<tr>
<td>
ArcSegment<br/><br/></td><td>
Yes<br/><br/></td></tr>
<tr>
<td>
Canvas<br/><br/></td><td>
Yes<br/><br/></td></tr>
<tr>
<td>
DocumentOutline<br/><br/></td><td>
No<br/><br/></td></tr>
<tr>
<td>
DocumentReference<br/><br/></td><td>
No<br/><br/></td></tr>
<tr>
<td>
FigureStructure<br/><br/></td><td>
No<br/><br/></td></tr>
<tr>
<td>
FixedPageResources<br/><br/></td><td>
Yes<br/><br/></td></tr>
<tr>
<td>
Glyphs<br/><br/></td><td>
Yes<br/><br/></td></tr>
<tr>
<td>
Gradient<br/><br/></td><td>
Yes<br/><br/></td></tr>
<tr>
<td>
ImageBrush<br/>(JPG, BMP, GIF, TIFF)<br/></td><td>
Yes<br/><br/></td></tr>
<tr>
<td>
Intent<br/><br/></td><td>
Yes<br/><br/></td></tr>
<tr>
<td>
LinkTarget<br/><br/></td><td>
Yes<br/><br/></td></tr>
<tr>
<td>
ListItemStructure<br/><br/></td><td>
Yes<br/><br/></td></tr>
<tr>
<td>
ListStructure<br/><br/></td><td>
Yes<br/><br/></td></tr>
<tr>
<td>
MatrixTransform<br/><br/></td><td>
Yes<br/><br/></td></tr>
<tr>
<td>
NamedElement<br/><br/></td><td>
No<br/><br/></td></tr>
<tr>
<td>
OutlineEntry<br/><br/></td><td>
No<br/><br/></td></tr>
<tr>
<td>
PageContent<br/><br/></td><td>
Yes<br/><br/></td></tr>
<tr>
<td>
PageContentLinkTargets<br/><br/></td><td>
No<br/><br/></td></tr>
<tr>
<td>
ParagraphStructure<br/><br/></td><td>
No<br/><br/></td></tr>
<tr>
<td>
Path<br/><br/></td><td>
Yes<br/><br/></td></tr>
<tr>
<td>
PolyBezierSegment<br/><br/></td><td>
Yes<br/><br/></td></tr>
<tr>
<td>
PolyLineSegment<br/><br/></td><td>
Yes<br/><br/></td></tr>
<tr>
<td>
PolyQuadraticBezierSegment<br/><br/></td><td>
Yes<br/><br/></td></tr>
<tr>
<td>
ResourceDictionary<br/><br/></td><td>
Yes<br/><br/></td></tr>
<tr>
<td>
SectionStructure<br/><br/></td><td>
No<br/><br/></td></tr>
<tr>
<td>
SignBy<br/><br/></td><td>
No<br/><br/></td></tr>
<tr>
<td>
SignatureDefinition<br/><br/></td><td>
No<br/><br/></td></tr>
<tr>
<td>
SignatureDefinitions<br/><br/></td><td>
No<br/><br/></td></tr>
<tr>
<td>
SigningLocation<br/><br/></td><td>
No<br/><br/></td></tr>
<tr>
<td>
SolidColorBrush<br/><br/></td><td>
Yes<br/><br/></td></tr>
<tr>
<td>
SpotLocation<br/><br/></td><td>
No<br/><br/></td></tr>
<tr>
<td>
Story<br/><br/></td><td>
No<br/><br/></td></tr>
<tr>
<td>
TableStructure<br/><br/></td><td>
No<br/><br/></td></tr>
<tr>
<td>
VisualBrush<br/><br/></td><td>
No<br/><br/></td></tr>
</tbody>
</table>

## Converting PDF to Image

This PDF to image converter library allows converting PDF documents to images without opening the document in the PDF Viewer control. It allows you to selectively export pages as a stream by utilizing the 'Convert' method, facilitating the transformation of PDF files into images.

<b>NuGet</b>

<table>
<tr>
<thead>
<th><b>Platform(s)</b></th>
<th><b>NuGet Package</b></th>
</thead>
</tr>
<tr>
<td>
Windows Forms
</td>
<td>
{{'[Syncfusion.PdfToImageConverter.WinForms.nupkg](https://www.nuget.org/packages/Syncfusion.PdfToImageConverter.WinForms/)'| markdownify }}
</td>
</tr>
<tr>
<td>
WPF
</td>
<td>
{{'[Syncfusion.PdfToImageConverter.WPF.nupkg](https://www.nuget.org/packages/Syncfusion.PdfToImageConverter.WPF/)'| markdownify }}
</td>
</tr>
<tr>
<td>
ASP.NET Core Windows
</td>
<td>
{{'[Syncfusion.PdfToImageConverter.Net.nupkg](https://www.nuget.org/packages/Syncfusion.PdfToImageConverter.Net/)'| markdownify }}
</td>
</tr>
<tr>
<td>
ASP.NET MVC Windows
</td>
<td>
{{'[Syncfusion.PdfToImageConverter.AspNet.Mvc4.nupkg](https://www.nuget.org/packages/Syncfusion.PdfToImageConverter.AspNet.Mvc4/)'| markdownify }}<br/>
{{'[Syncfusion.PdfToImageConverter.AspNet.Mvc5.nupkg](https://www.nuget.org/packages/Syncfusion.PdfToImageConverter.AspNet.Mvc5/)'| markdownify }}
</td>
</tr>
</table>

N> The above mentioned NuGet packages are available in [nuget.org](https://www.nuget.org/).

The following code snippet illustrates how to convert PDF page into image using Convert method in PdfToImageConverter.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//Initialize PDF to Image converter.
PdfToImageConverter imageConverter = new PdfToImageConverter();
//Load the PDF document as a stream
FileStream inputStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.ReadWrite);
imageConverter.Load(inputStream);
//Convert PDF to Image.
Stream outputStream = imageConverter.Convert(0, false, false);
MemoryStream stream = outputStream as MemoryStream;
return File(stream.ToArray(), System.Net.Mime.MediaTypeNames.Image.Jpeg, "sample.jpeg");

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Initialize PDF to Image converter.
PdfToImageConverter imageConverter = new PdfToImageConverter();
//Load the PDF document as a stream
FileStream inputStream = new FileStream("Input.pdf", FileMode.Open, FileAccess.ReadWrite);
imageConverter.Load(inputStream);
//Convert PDF to Image.
Stream outputStream = imageConverter.Convert(0, false, false);
Bitmap image = new Bitmap(outputStream);
image.Save("sample.png");


{% endhighlight %}
{% highlight vb tabtitle="VB.NET [Windows-specific]" %}

'Initialize PDF to Image converter.
Dim imageConverter As PdfToImageConverter = New PdfToImageConverter()
'Load the PDF document as a stream
Dim inputStream As FileStream = New FileStream("Input.pdf", FileMode.Open, FileAccess.ReadWrite)
imageConverter.Load(inputStream)
'Convert PDF to Image.
Dim outputStream As Stream = imageConverter.Convert(0, False, False)
Dim image As Bitmap = New Bitmap(outputStream)
image.Save("sample.png")

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/WPF-PDFViewer-Examples/tree/master/PDF-to-image).

N> To know more about PdfToImageConverter and features it provides, please refer to [PdfToImageConverter](https://help.syncfusion.com/file-formats/pdf-to-image)

## MHTML to PDF

The [HTML to PDF converter library](https://www.syncfusion.com/document-processing/pdf-framework/net/html-to-pdf) supports converting the MHTML file to PDF document. Please refer to the following code example. 

*HTML to PDF Features:* [https://help.syncfusion.com/file-formats/pdf/convert-html-to-pdf/features](https://help.syncfusion.com/file-formats/pdf/convert-html-to-pdf/features) 
    
*Troubleshooting:* [https://help.syncfusion.com/file-formats/pdf/convert-html-to-pdf/troubleshooting](https://help.syncfusion.com/file-formats/pdf/convert-html-to-pdf/troubleshooting)

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//Initialize HTML to PDF converter 
HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter();
//Convert MHTML to PDF
PdfDocument document = htmlConverter.Convert(@"input.mhtml");
//Save the document into stream
MemoryStream stream = new MemoryStream();
//Close the document
document.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Initialize HTML to PDF converter
HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter();
//Convert MHTML to PDF
PdfDocument document = htmlConverter.Convert("input.mhtml");  
//Save the document
document.Save("Sample.pdf");
document.Close();

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Initialize HTML to PDF converter
Dim htmlConverter As New HtmlToPdfConverter()
'Convert MHTML to PDF
Dim document As PdfDocument = htmlConverter.Convert("input.mhtml")
'Save and close the document
document.Save("Sample.pdf")
document.Close()

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Document%20conversion/Convert-MHTML-to-PDF-document).

## HTML to MHTML

The [HTML to PDF converter library](https://www.syncfusion.com/document-processing/pdf-framework/net/html-to-pdf) supports converting the webpage to an MHTML file. Please refer to the following code example. 

*HTML to PDF Features:* [https://help.syncfusion.com/file-formats/pdf/convert-html-to-pdf/features](https://help.syncfusion.com/file-formats/pdf/convert-html-to-pdf/features) 
    
*Troubleshooting:* [https://help.syncfusion.com/file-formats/pdf/convert-html-to-pdf/troubleshooting](https://help.syncfusion.com/file-formats/pdf/convert-html-to-pdf/troubleshooting)

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

//PDF doesn't support converting HTML to MHTML C#.NET Cross platforms.

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Initialize HTML to PDF converter
HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter();
//Convert URL to MHTML
htmlConverter.ConvertToMhtml("http://www.syncfusion.com", "sample.mhtml");

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Initialize HTML to PDF converter
Dim htmlConverter As New HtmlToPdfConverter()      
'Convert URL to MHTML
htmlConverter.ConvertToMhtml("http://www.syncfusion.com", "sample.mhtml")

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Document%20conversion/Convert-HTML-to-MHTML).

## HTML to Raster Image

The [HTML to PDF converter library](https://www.syncfusion.com/document-processing/pdf-framework/net/html-to-pdf) supports converting the webpage to an image. Please refer to the following code example. 

*HTML to PDF Features:* [https://help.syncfusion.com/file-formats/pdf/convert-html-to-pdf/features](https://help.syncfusion.com/file-formats/pdf/convert-html-to-pdf/features) 
    
*Troubleshooting:* [https://help.syncfusion.com/file-formats/pdf/convert-html-to-pdf/troubleshooting](https://help.syncfusion.com/file-formats/pdf/convert-html-to-pdf/troubleshooting)

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}

//Initialize HTML to PDF converter
HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter();
//Convert URL to Image
Image image = htmlConverter.ConvertToImage("http://www.google.com");
byte[] imageByte = image.ImageData;
//Save the image
File.WriteAllBytes("Sample.jpg", imageByte);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Initialize HTML to PDF converter
HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter();
//Convert URL to Image
Image[] image = htmlConverter.ConvertToImage("http://www.syncfusion.com");
//Save the image
image[0].Save("Sample.jpg");

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Initialize HTML to PDF converter
Dim htmlConverter As New HtmlToPdfConverter()
'Convert URL to Image
Dim image As Image() = htmlConverter.ConvertToImage("http://www.syncfusion.com")
'Save the image
image(0).Save("Sample.jpg")

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Document%20conversion/Convert-HTML-to-raster-image).

## HTML string to Raster Image

The [HTML to PDF converter library](https://www.syncfusion.com/document-processing/pdf-framework/net/html-to-pdf) supports converting the HTML string to an image. Please refer to the following code example. 

*HTML to PDF Features:* [https://help.syncfusion.com/file-formats/pdf/convert-html-to-pdf/features](https://help.syncfusion.com/file-formats/pdf/convert-html-to-pdf/features) 
    
*Troubleshooting:* [https://help.syncfusion.com/file-formats/pdf/convert-html-to-pdf/troubleshooting](https://help.syncfusion.com/file-formats/pdf/convert-html-to-pdf/troubleshooting)

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}
//Initialize HTML to PDF converter
HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter();
//HTML string and Base URL
string htmlString = "<html><body>Hello World!!!</body></html>";
string baseURL = "";
//Convert HTML string to Image
Image image = htmlConverter.ConvertToImage(htmlString, baseURL);
byte[] imageByte = image.ImageData;
//Save the image
File.WriteAllBytes("Output.jpg", imageByte);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

string htmlString = "<html><body>Hello World!!!</body></html>";
string baseURL = "";
//Initialize HTML to PDF converter
HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter();
//Convert HTML string to Image
Image[] image = htmlConverter.ConvertToImage(htmlString, baseURL);
//Save the image
image[0].Save("Sample.jpg");

{% endhighlight %}
{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

Dim htmlString As String = "<html><body>Hello World!!!</body></html>"
Dim baseURL As String = ""
'Initialize HTML to PDF converter
Dim htmlConverter As New HtmlToPdfConverter()
'Convert HTML string to Image
Dim image As Image() = htmlConverter.ConvertToImage(htmlString, baseURL)
'Save the image
image(0).Save("Sample.jpg")

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Document%20conversion/HTML-string-to-raster-image/.NET-Standard).

## Partial webpage to Raster Image

The [HTML to PDF converter library](https://www.syncfusion.com/document-processing/pdf-framework/net/html-to-pdf) supports converting the partial webpage to an image. Please refer to the following code example. 

*HTML to PDF Features:* [https://help.syncfusion.com/file-formats/pdf/convert-html-to-pdf/features](https://help.syncfusion.com/file-formats/pdf/convert-html-to-pdf/features) 
    
*Troubleshooting:* [https://help.syncfusion.com/file-formats/pdf/convert-html-to-pdf/troubleshooting](https://help.syncfusion.com/file-formats/pdf/convert-html-to-pdf/troubleshooting)

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Initialize HTML to PDF converter
HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter();
//Convert Partial HTML to Image
Image image = htmlConverter.ConvertPartialHtmlToImage("http://www.google.com", "lga");
byte[] imageByte = image.ImageData;
//Save the image
File.WriteAllBytes("Output.jpg", imageByte);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Initialize HTML to PDF converter
HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter();
//Convert Partial HTML to Image
Image[] image = htmlConverter.ConvertPartialHtmlToImage("input.html", "pic");
//Save Image
image[0].Save("Output.jpg");

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Initialize HTML to PDF converter
Dim htmlConverter As New HtmlToPdfConverter()
'Convert Partial HTML to Image
Dim image As Image() = htmlConverter.ConvertPartialHtmlToImage("input.html", "pic")
'Save Image
image(0).Save("Output.jpg")

{% endhighlight %}

{% highlight html %}

<html>
<head>
</head>
<body>
Hello world
	<div id="pic">
		<img src=" syncfusion_logo.gif" alt="Smiley face" width="42" height="42"><br>
		This is a Syncfusion Logo
	</div>
	<div>
		Hello world
	</div>
</body>
</html>

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Document%20conversion/Convert-partial-webpage-to-raster-image).

## HTML to SVG

The [HTML to PDF converter library](https://www.syncfusion.com/document-processing/pdf-framework/net/html-to-pdf) supports converting the HTML to SVG file. Please refer to the following code example. 

*HTML to PDF Features:* [https://help.syncfusion.com/file-formats/pdf/convert-html-to-pdf/features](https://help.syncfusion.com/file-formats/pdf/convert-html-to-pdf/features) 
    
*Troubleshooting:* [https://help.syncfusion.com/file-formats/pdf/convert-html-to-pdf/troubleshooting](https://help.syncfusion.com/file-formats/pdf/convert-html-to-pdf/troubleshooting)

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Initialize HTML to PDF converter
HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter(HtmlRenderingEngine.WebKit);
//Initialize the memory stream
MemoryStream stream = new MemoryStream();
//Convert URL to SVG
htmlConverter.ConvertToSvg("http://www.syncfusion.com", stream);
//Save the document
using (FileStream output = new FileStream("Sample.svg", FileMode.Create))
{
    stream.CopyTo(output);
}

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Initialize HTML to PDF converter
HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter(HtmlRenderingEngine.WebKit);
//Convert URL to SVG
htmlConverter.ConvertToSvg("http://www.syncfusion.com", "sample.svg");

{% endhighlight %}


{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Initialize HTML to PDF converter
Dim htmlConverter As New HtmlToPdfConverter(HtmlRenderingEngine.WebKit)
'Convert URL to SVG
htmlConverter.ConvertToSvg("http://www.syncfusion.com", "sample.svg")

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Document%20conversion).

N> 1. Syncfusion PDF supports converting HTML to SVG with  [Syncfusion.HtmlToPdfConverter.QtWebKit.Net.Core](https://www.nuget.org/packages/Syncfusion.HtmlToPdfConverter.QtWebKit.Net.Core) package reference in the .NET Core application.
N> 2. HTML to SVG conversion is not supported on Mac platforms.

## Partial webpage to SVG

The [HTML to PDF converter library](https://www.syncfusion.com/document-processing/pdf-framework/net/html-to-pdf) supports converting the partial webpage to SVG. Please refer to the following code example.

*HTML to PDF Features:* [https://help.syncfusion.com/file-formats/pdf/convert-html-to-pdf/features](https://help.syncfusion.com/file-formats/pdf/convert-html-to-pdf/features) 
    
*Troubleshooting:* [https://help.syncfusion.com/file-formats/pdf/convert-html-to-pdf/troubleshooting](https://help.syncfusion.com/file-formats/pdf/convert-html-to-pdf/troubleshooting)

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Initialize HTML to PDF converter
HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter(HtmlRenderingEngine.WebKit);
//Initialize the memory stream
MemoryStream stream = new MemoryStream();
//Convert a partial HTML to SVG
htmlConverter.ConvertPartialHtmlToSvg("input.html", "pic", stream);
//Save the document
using (FileStream output = new FileStream("Sample.svg", FileMode.Create))
{
    stream.CopyTo(output);
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Initialize HTML to PDF converter
HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter(HtmlRenderingEngine.WebKit);
//Convert Partial HTML to SVG
htmlConverter.ConvertPartialHtmlToSvg("input.html", "pic", "Output.svg");

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Initialize HTML to PDF converter
Dim htmlConverter As New HtmlToPdfConverter(HtmlRenderingEngine.WebKit)
'Convert Partial HTML to SVG
htmlConverter.ConvertPartialHtmlToSvg("input.html", "pic", "Output.svg")

{% endhighlight %}

{% highlight html %}

<html>
<head>
</head>
<body>
Hello world
	<div id="pic">
		<img src=" syncfusion_logo.gif" alt="Smiley face" width="42" height="42"><br>
		This is a Syncfusion Logo
	</div>
	<div>
		Hello world
	</div>
</body>
</html>

{% endhighlight %}

{% endtabs %}

You can download a complete working sample from [GitHub](https://github.com/SyncfusionExamples/PDF-Examples/tree/master/Document%20conversion/Convert-partial-webpage-to-SVG/.NET-Standard).

N> 1. Syncfusion PDF supports Partial HTML to SVG conversion with [Syncfusion.HtmlToPdfConverter.QtWebKit.Net.Core](https://www.nuget.org/packages/Syncfusion.HtmlToPdfConverter.QtWebKit.Net.Core) package reference in the .NET Core application.
N> 2. Partial HTML to SVG conversion is not supported on Mac platforms.

## SVG to PDF 

The [HTML to PDF converter library](https://www.syncfusion.com/document-processing/pdf-framework/net/html-to-pdf) supports converting the SVG to PDF document. Please refer to the following code example.

{% tabs %}

{% highlight c# tabtitle="C# [Cross-platform]" %}

//Initialize HTML to PDF converter
HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter();
//Convert URL to PDF document. 
PdfDocument document = htmlConverter.Convert("inputSVG.svg");
//Save the document into stream
MemoryStream stream = new MemoryStream();
document.Save(stream);
//Close the document
document.Close(true);

{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}

//Initialize HTML to PDF converter
HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter();
//Convert a SVG file to PDF with HTML converter
PdfDocument document = htmlConverter.Convert("inputSVG.svg");
//Save and close the PDF document
document.Save("SVGToPDF.pdf");
document.Close(true);

{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}

'Initialize HTML to PDF converter 
Dim htmlConverter As HtmlToPdfConverter = New HtmlToPdfConverter()
'Convert a SVG file to PDF with HTML converter 
Dim document As PdfDocument = htmlConverter.Convert("inputSVG.svg")
'Save and close the PDF document
document.Save("SVGToPDF.pdf")
document.Close(True)

{% endhighlight %}

{% endtabs %}
