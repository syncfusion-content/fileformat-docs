---
title: Excel to PDF Conversion
description: In this section, you can learn how to convert Excel Workbook to PDF & Worksheet to PDF file; how to print Excel file and how to convert Excel chart to image
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
XlsIO supports Excel To PDF conversion in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms. To achieve Excel to PDF conversion in other platforms like UWP, Xamarin, ASP.NET Core it is recommended to use web service.

The following code illustrates how to convert an Excel workbook to PDF.

{% tabs %}  

{% highlight c# %}
using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

  //Open the Excel document to Convert
  ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);

  //Initialize PDF document
  PdfDocument pdfDocument = new PdfDocument();

  //Convert Excel document into PDF document
  pdfDocument = converter.Convert();

  //Save the PDF file
  pdfDocument.Save("ExcelToPDF.pdf");
}

{% endhighlight %}

{% highlight vb %}
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

{% highlight UWP %}

#region Excel To PDF
//Gets assembly
Assembly assembly = typeof(App).GetTypeInfo().Assembly;

//Gets input Excel document from an embedded resource collection
Stream inputStream = assembly.GetManifestResourceStream("ExcelToPDF.Data.ExcelToPDF.xlsx");

//Output stream to save PDF
MemoryStream outputStream = null;

//Creates new instance of HttpClient to access service
HttpClient client = new HttpClient();

//Web service URI 
string requestUri = "http://js.syncfusion.com/demos/ioservices/api/excel/converttopdf";

//Posts input Excel document to service and gets resultant PDF as content of HttpResponseMessage
HttpResponseMessage response = null;
try
{
  response = await client.PostAsync(requestUri, new StreamContent(inputStream));

  //Dispose the input stream and client instances
  inputStream.Dispose();
  client.Dispose();
}
catch (Exception ex)
{
  return;
}

//Gets PDF from content stream if the service get success
if (response.IsSuccessStatusCode)
{
  var responseHeaders = response.Headers;
  outputStream = new MemoryStream(await response.Content.ReadAsByteArrayAsync());

  //Dispose the response instance
  response.Dispose();
}

else
{
  return;
}
#endregion

//Save the workbook stream as a file.

#region Setting output location
StorageFile storageFile;
if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
{
  FileSavePicker savePicker = new FileSavePicker();
  savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
  savePicker.SuggestedFileName = "ExcelToPDF";
  savePicker.FileTypeChoices.Add("PDF File", new List<string>() { ".pdf", });
  storageFile = await savePicker.PickSaveFileAsync();
}
else
{
  StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
  storageFile = await local.CreateFileAsync("ExcelToPDF.xlsx", CreationCollisionOption.ReplaceExisting);
}

if (storageFile == null)
  return;

using (Stream storageStream = await storageFile.OpenStreamForWriteAsync())
{
    if (storageStream.CanSeek)
      storageStream.SetLength(0);
    storageStream.Write(outputStream.ToArray(), 0, (int)outputStream.Length);
    outputStream.Dispose();
}
#endregion
{% endhighlight %}

{% highlight ASP.NET Core %}

//Gets assembly
Assembly assembly = typeof(Program).GetTypeInfo().Assembly;

//Gets input Excel document from an embedded resource collection
Stream inputStream = assembly.GetManifestResourceStream("ExcelToPDF.Spreadsheet.xlsx");

//Creates new instance of HttpClient to access the service
HttpClient client = new HttpClient();

//Web service URI 
string requestUri = "http://js.syncfusion.com/demos/ioservices/api/excel/converttopdf";

//Posts input Excel document to service and gets resultant PDF as content of HttpResponseMessage
HttpResponseMessage response = null;
try
{
    response = await client.PostAsync(requestUri, new StreamContent(inputStream));

    //Dispose the input stream and client instances
    inputStream.Dispose();
    client.Dispose();
}
catch (Exception ex)
{
    return;
}

MemoryStream outputStream = null;

//Gets PDF from content stream if the service get success
if (response.IsSuccessStatusCode)
{
    var responseHeaders = response.Headers;
    outputStream = new MemoryStream(await response.Content.ReadAsByteArrayAsync());
    //Dispose the response instance.
    response.Dispose();
}
else
{
    return;
}

//Saving the workbook as stream
FileStream stream = new FileStream("Output.pdf", FileMode.Create, FileAccess.ReadWrite);
outputStream.CopyTo(stream);

outputStream.Close();
outputStream.Dispose();

{% endhighlight %}

{% highlight Xamarin %}

//Gets assembly
Assembly assembly = typeof(App).GetTypeInfo().Assembly;

//Gets input Excel document from an embedded resource collection
Stream inputStream = assembly.GetManifestResourceStream("ExcelToPDF.ExcelToPDF.xlsx");

//Creates new instance of HttpClient to access service
HttpClient client = new HttpClient();

//Web service URI 
string requestUri = "http://js.syncfusion.com/demos/ioservices/api/excel/converttopdf";

//Posts input Excel document to service and gets resultant PDF as content of HttpResponseMessage
HttpResponseMessage response = null;
response = await client.PostAsync(requestUri, new StreamContent(inputStream));

//Dispose the input stream and client instances
inputStream.Dispose();
client.Dispose();

MemoryStream outputStream = null;

//Gets PDF from content stream if the service get success
if (response.IsSuccessStatusCode)
{
  var responseHeaders = response.Headers;
  outputStream = new MemoryStream(await response.Content.ReadAsByteArrayAsync());
  //Dispose the response instance.
  response.Dispose();
}
else
{
  return;
}

//Save the stream as Excel document and view the saved document

//The operation in SaveAndView under Xamarin varies among Windows Phone, Android, and iOS platforms. Refer to the xlsio/xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
  await DependencyService.Get<ISaveWindowsPhone>().Save("ExcelToPDF.pdf", "application/pdf", outputStream);
}
else
{
  DependencyService.Get<ISave>().Save("ExcelToPDF.pdf", "application/pdf", outputStream);
}

//Dispose the output stream instance
outputStream.Dispose();
{% endhighlight %}

{% endtabs %}

**Web Service**

The web service code that converts Excel document at server-side and returns the resultant PDF document as content of HttpResponseMessage at client-side.

> The following server-side code can be invoked from client-side using web service URI.

{% tabs %}
{% highlight c# %}
HttpFileCollection files = HttpContext.Current.Request.Files;

if (files.Count == 0)
    return;
    
//Loads an existing Excel document stream	
using (Stream stream = files[0].InputStream)
{
  using (ExcelEngine engine = new ExcelEngine())
  {
    IApplication application = engine.Excel;
	
    //Initializes the ChartToImageConverter for converting charts during Excel To PDF conversion
    application.ChartToImageConverter = new ChartToImageConverter();
    application.ChartToImageConverter.ScalingMode = ScalingMode.Normal;
	
    //Creates an instance of the ExcelToPDFConverter
    using (ExcelToPdfConverter excelToPDFConverter = new ExcelToPdfConverter(stream))
    {
      //Converts Excel document into PDF document
      using (PdfDocument pdfDocument = excelToPDFConverter.Convert())
      {
        //Saves the PDF document to response stream
        pdfDocument.Save("ExcelToPDF.pdf", HttpContext.Current.Response, HttpReadType.Save);
        pdfDocument.Close(true);
      }
    } 
  }
}
{% endhighlight %}
{% highlight vb %}
Dim files As HttpFileCollection = HttpContext.Current.Request.Files

If files.Count = 0 Then Return

'Loads an existing Excel document stream
Using stream As Stream = files(0).InputStream
      Using engine As ExcelEngine = New ExcelEngine()
          Dim application As IApplication = engine.Excel
          
          'Initializes the ChartToImageConverter for converting charts during Excel To PDF conversion
          application.ChartToImageConverter = New ChartToImageConverter()
          application.ChartToImageConverter.ScalingMode = ScalingMode.Normal
          
          'Creates an instance of the ExcelToPDFConverter
          Using excelToPDFConverter As ExcelToPdfConverter = New ExcelToPdfConverter(stream)
          
             'Converts Excel document into PDF document
              Using pdfDocument As PdfDocument = excelToPDFConverter.Convert()
              
                 'Saves the PDF document to response stream
                  pdfDocument.Save("ExcelToPDF.pdf", HttpContext.Current.Response, HttpReadType.Save)
                  pdfDocument.Close(True)
                  
              End Using
          End Using
      End Using
End Using
{% endhighlight %}
{% endtabs %}

To learn more about different conversion settings in Excel To PDF conversion, refer to the ExcelToPdfConverterSettings in API section.

## Worksheet to PDF

The following code shows how to convert a particular sheet to PDF document.

{% tabs %}
{% highlight c# %}
Using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);
  IWorksheet sheet = workbook.Worksheets[0];

  //convert the sheet to PDF
  ExcelToPdfConverter converter = new ExcelToPdfConverter(sheet);

  PdfDocument pdfDocument= new PdfDocument();
  pdfDocument = converter.Convert();
  pdfDocument.Save("ExcelToPDF.pdf");       
}

{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
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
End Using
{% endhighlight %}

{% highlight UWP %}
//XlsIO supports Excel To PDF conversion in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms. Refer to the Workbook to PDF section to convert using web service.
{% endhighlight %}

{% highlight ASP.NET Core %}
//XlsIO supports Excel To PDF conversion in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms. Refer to the Workbook to PDF section to convert using web service.
{% endhighlight %}

{% highlight Xamarin %}
//XlsIO supports Excel To PDF conversion in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms. Refer to the Workbook to PDF section to convert using web service.
{% endhighlight %}
{% endtabs %}  

**Creating** **individual** **PDF** **document** **for** **each** **worksheet**

The following code snippet shows how to create an individual PDF document for each worksheet in a workbook.

{% tabs %}
{% highlight c# %}
Using(ExcelEngine excelEngine = new ExcelEngine())
{
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
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
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
End Using
{% endhighlight %}

{% highlight UWP %}
//XlsIO supports Excel To PDF conversion in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms. Refer to the Workbook to PDF section to convert using web service.
{% endhighlight %}

{% highlight ASP.NET Core %}
//XlsIO supports Excel To PDF conversion in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms. Refer to the Workbook to PDF section to convert using web service.
{% endhighlight %}

{% highlight Xamarin %}
//XlsIO supports Excel To PDF conversion in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms. Refer to the Workbook to PDF section to convert using web service.
{% endhighlight %}
{% endtabs %}
  
## Excel with chart to PDF

To preserve the charts during Excel To PDF conversion, initialize the ChartToImageConverter of **IApplication** interface otherwise the charts present in worksheet gets skipped. The following code illustrates how to convert an Excel with chart to PDF document.

{% tabs %}
{% highlight c# %}
Using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  //Instantiating the ChartToImageConverter and assigning the ChartToImageConverter instance of XlsIO application
  application.ChartToImageConverter = new ChartToImageConverter();

  //Tuning chart image quality
  application.ChartToImageConverter.ScalingMode = ScalingMode.Best;

  IWorkbook workbook = application.Workbooks.Open("chart.xlsx");
  IWorksheet worksheet = workbook.Worksheets[0];

  ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);

  PdfDocument pdfDocument = new PdfDocument();
  pdfDocument = converter.Convert();
  pdfDocument.Save("ExcelToPDF.pdf");
}

{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013

  'Instantiating the ChartToImageConverter and assigning the ChartToImageConverter instance of XlsIO application
  application.ChartToImageConverter = New ChartToImageConverter()

  'Tuning chart image quality
  application.ChartToImageConverter.ScalingMode = ScalingMode.Best

  Dim workbook As IWorkbook = application.Workbooks.Open("chart.xlsx")
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  Dim converter As New ExcelToPdfConverter(workbook)
  
  Dim pdfDocument As New PdfDocument()
  pdfDocument = converter.Convert()
  pdfDocument.Save("ExcelToPDF.pdf")
End Using
{% endhighlight %}

{% highlight UWP %}
//XlsIO supports Excel To PDF conversion in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms. Refer to the Workbook to PDF section to convert using web service.
{% endhighlight %}

{% highlight ASP.NET Core %}
//XlsIO supports Excel To PDF conversion in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms. Refer to the Workbook to PDF section to convert using web service.
{% endhighlight %}

{% highlight Xamarin %}
//XlsIO supports Excel To PDF conversion in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms. Refer to the Workbook to PDF section to convert using web service.
{% endhighlight %}
{% endtabs %}  

## Print Excel document

XlsIO supports Excel printing option by converting Excel To PDF and printing that PDF document. The Excel can be printed with specified page setup and printer settings in XlsIO.

The following printer settings can be applied to print Excel in XlsIO. 

![](Excel-to-PDF-Conversion_images/Excel-to-PDF-Conversion_img1.jpg)
 
### Print Excel document 

The following code snippet illustrates how to print the Excel document in XlsIO.

{% tabs %}
{% highlight c# %}
Using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  IWorkbook workbook = application.Workbooks.Open("Excel.xlsx"));

  // Convert the workbook
  ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);

  // Print the converted PDF document
  converter.Print();
}
{% endhighlight %}

{% highlight vb %}

Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  Dim workbook As IWorkbook = application.Workbooks.Open("Excel.xlsx")

  'Convert the workbook
  Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(workbook)

  'Print the converted PDF document
  converter.Print()
End Using
{% endhighlight %}

{% highlight UWP %}
//XlsIO supports Excel To PDF conversion in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms. Refer to the Workbook to PDF section to convert using web service.
{% endhighlight %}

{% highlight ASP.NET Core %}
//XlsIO supports Excel To PDF conversion in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms. Refer to the Workbook to PDF section to convert using web service.
{% endhighlight %}

{% highlight Xamarin %}
//XlsIO supports Excel To PDF conversion in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms. Refer to the Workbook to PDF section to convert using web service.
{% endhighlight %}
{% endtabs %}

### Print with printer settings

The following code snippet illustrates how to print the Excel document with printer settings in XlsIO.

{% tabs %}
{% highlight c# %}
Using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  IWorkbook workbook = application.Workbooks.Open("Excel.xlsx"));

  //Convert the workbook
  ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);

  //Initialize the printer settings
  PrinterSettings printerSettings = new PrinterSettings();

  //customizing the printer settings
  printerSettings.PrinterName = "HP LaserJet Pro MFP M127-M128 PCLmS";
  printerSettings.Copies = 2;
  printerSettings.FromPage = 2;
  printerSettings.ToPage = 3;
  printerSettings.DefaultPageSettings.Color = false;
  printerSettings.Duplex = Duplex.Vertical;

  //Print the converted PDF document with printer settings
  converter.Print(printerSettings);
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  Dim workbook As IWorkbook = application.Workbooks.Open("Excel.xlsx")

  'Convert the workbook
  Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(workbook)

  'Initialize the printer settings
  Dim printerSettings As PrinterSettings = New PrinterSettings

  'customizing the printer settings
  printerSettings.PrinterName = "HP LaserJet Pro MFP M127-M128 PCLmS"
  printerSettings.Copies = 2
  printerSettings.FromPage = 2
  printerSettings.ToPage = 3
  printerSettings.DefaultPageSettings.Color = false
  printerSettings.Duplex = Duplex.Vertical

  'Print the converted PDF document with printer settings
  converter.Print(printerSettings)
End Using
{% endhighlight %}

{% highlight UWP %}
//XlsIO supports Excel To PDF conversion in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms. Refer to the Workbook to PDF section to convert using web service.
{% endhighlight %}

{% highlight ASP.NET Core %}
//XlsIO supports Excel To PDF conversion in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms. Refer to the Workbook to PDF section to convert using web service.
{% endhighlight %}

{% highlight Xamarin %}
//XlsIO supports Excel To PDF conversion in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms. Refer to the Workbook to PDF section to convert using web service.
{% endhighlight %}
{% endtabs %}

### Print with Excel To PDF converter settings

The following code snippet illustrates how to print the Excel document with Excel To PDF converter settings in XlsIO.

{% tabs %}  
{% highlight c# %}
Using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  IWorkbook workbook = application.Workbooks.Open("Excel.xlsx");

  //Convert the workbook
  ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);

  //Initializes the Excel To PDF converter setting class
  ExcelToPdfConverterSettings converterSettings = new ExcelToPdfConverterSettings();

  //Layout the page using FitAllColumnsOnOnePage options
  converterSettings.DisplayGridLines = GridLinesDisplayStyle.Visible;
  converterSettings.LayoutOptions = LayoutOptions.FitAllColumnsOnOnePage;

  //Print the converted PDF document with converter settings
  converter.Print(converterSettings);
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  Dim workbook As IWorkbook = application.Workbooks.Open("Excel.xlsx")

  'Convert the workbook
  Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(workbook)

  'Initialize the Excel To PDF converter setting class
  Dim converterSettings As ExcelToPdfConverterSettings = New ExcelToPdfConverterSettings

  'Layout the page using FitAllColumnsOnOnePage options
  converterSettings.DisplayGridLines = GridLinesDisplayStyle.Visible
  converterSettings.LayoutOptions = LayoutOptions.FitAllColumnsOnOnePage

  'Print the converted PDF document with converter settings
  converter.Print(converterSettings)
End Using
{% endhighlight %}

{% highlight UWP %}
//XlsIO supports Excel To PDF conversion in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms. Refer to the Workbook to PDF section to convert using web service.
{% endhighlight %}

{% highlight ASP.NET Core %}
//XlsIO supports Excel To PDF conversion in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms. Refer to the Workbook to PDF section to convert using web service.
{% endhighlight %}

{% highlight Xamarin %}
//XlsIO supports Excel To PDF conversion in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms. Refer to the Workbook to PDF section to convert using web service.
{% endhighlight %}
{% endtabs %}

### Print with Excel To PDF converter and printer settings

The following code snippet illustrates how to print the Excel document with Excel To PDF converter settings and printer settings in XlsIO.

{% tabs %}  
{% highlight c# %}
Using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  IWorkbook workbook = application.Workbooks.Open("Excel.xlsx"));

  ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);

  //Initialize the printer settings
  PrinterSettings printerSettings = new PrinterSettings();

  //customizing the printer settings
  printerSettings.PrinterName = "HP LaserJet Pro MFP M127-M128 PCLmS";
  printerSettings.Copies = 2;
  printerSettings.FromPage = 2;
  printerSettings.ToPage = 3;
  printerSettings.DefaultPageSettings.Color = true;
  printerSettings.Duplex = Duplex.Vertical;
  printerSettings.Collate = true;

  //Initializes the Excel To PDF converter setting class
  ExcelToPdfConverterSettings converterSettings = new ExcelToPdfConverterSettings();

  //Layout the page using FitAllColumnsOnOnePage options
  converterSettings.DisplayGridLines = GridLinesDisplayStyle.Visible;
  converterSettings.LayoutOptions = LayoutOptions.FitAllColumnsOnOnePage;

  //Print the converted PDF document with printer settings and converter settings
  converter.Print(printerSettings, converterSettings);
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  Dim workbook As IWorkbook = application.Workbooks.Open("Excel.xlsx")
  Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(workbook)

  'Initialize the printer settings
  Dim printerSettings As PrinterSettings = New PrinterSettings

  'customizing the printer settings
  printerSettings.PrinterName = "HP LaserJet Pro MFP M127-M128 PCLmS"
  printerSettings.Copies = 2
  printerSettings.FromPage = 2
  printerSettings.ToPage = 3
  printerSettings.DefaultPageSettings.Color = true
  printerSettings.Duplex = Duplex.Vertical
  printerSettings.Collate = true

  'Initialize the Excel To PDF converter setting class
  Dim converterSettings As ExcelToPdfConverterSettings = New ExcelToPdfConverterSettings

  'Layout the page using FitAllColumnsOnOnePage options
  converterSettings.DisplayGridLines = GridLinesDisplayStyle.Visible
  converterSettings.LayoutOptions = LayoutOptions.FitAllColumnsOnOnePage

  'Print the converted PDF document with printer settings and converter settings
  converter.Print(printerSettings, converterSettings)
End Using
{% endhighlight %}

{% highlight UWP %}
//XlsIO supports Excel To PDF conversion in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms. Refer to the Workbook to PDF section to convert using web service.
{% endhighlight %}

{% highlight ASP.NET Core %}
//XlsIO supports Excel To PDF conversion in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms. Refer to the Workbook to PDF section to convert using web service.
{% endhighlight %}

{% highlight Xamarin %}
//XlsIO supports Excel To PDF conversion in Windows Forms, WPF, ASP.NET, and ASP.NET MVC platforms. Refer to the Workbook to PDF section to convert using web service.
{% endhighlight %}
{% endtabs %}

  
N> This section is applicable only to the Windows Forms and WPF platforms.

## Supported elements

This feature supports the following elements:

* Styles
* Rich-text formatting
* Headers and footers
* Images
* Picture recolor
	* Black and white
	* Color change
	* DuoTone
	* Gray scale
* Text boxes
* Hyperlinks
* Document properties
* Table styles
* Text rotations
* Excel page setup options
* Unicode
* Print titles
* Page breaks
* Print area
* Print order
* 2D charts
* 3D charts
* AutoShapes
* Group shapes
* Conditional formats
* Pivot tables

## Unsupported elements

The following list contains unsupported elements that presently not preserved in the generated PDF document: 

* Gradient fill
* Comments
* Sparklines
* Pivot charts
* SmartArt graphics
* Different first page headers
* Different odd and even pages
* Conditional formats
	* Data bars
	* Color scales
* Tables
	* Custom styles
* Row and column headings
* Form controls
* ActiveX controls
* OLE objects
