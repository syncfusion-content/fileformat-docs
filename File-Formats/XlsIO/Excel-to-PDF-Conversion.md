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
using(ExcelEngine excelEngine = new ExcelEngine())
{
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
}

{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
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
End Using
{% endhighlight %}

{% highlight UWP %}
//XlsIO supports excel to pdf conversion in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms alone.This below code shows how to achieve excel to pdf conversion using a web service.

#region Excel to PDF
//Gets assembly
Assembly assembly = typeof(App).GetTypeInfo().Assembly;

//Gets input Excel document from embedded resource collection
Stream inputStream = assembly.GetManifestResourceStream("ExcelToPDF.Data.ExceltoPDF.xlsx");

//Output stream to save PDF
MemoryStream outputStream = null;

//Creates new instance of HttpClient to access service
HttpClient client = new HttpClient();

//Gets Uri 
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
  error.Text = ex.Message.ToString();
  return;
}

//Gets PDF from content stream if service got success
if (response.IsSuccessStatusCode)
{
  var responseHeaders = response.Headers;
  outputStream = new MemoryStream(await response.Content.ReadAsByteArrayAsync());

  //Dispose the response instance
  response.Dispose();
}

//Pop ups the result of service failure with details
else
{
  error.Text = "The input document could not be processed, Could you please email the document to support@syncfusion.com for troubleshooting";
  return;
}
#endregion

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
//XlsIO supports excel to pdf conversion in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms alone.This below code shows how to achieve excel to pdf conversion using a web service.
//.cshtml file for excel to pdf conversion

@using Syncfusion.JavaScript.DataVisualization

@section SampleHeading{<span class="sampleName">XlsIO / ExcelToPDF</span>}

 @section ControlsSection{                                
          @{ViewBag.Title = "    Essential XlsIO (Excel) :Excel To PDF Conversion : Syncfusion";}

<form name="form1" method="post" action="https://js.syncfusion.com/ejservices/api/xlsio/converttopdf" enctype="multipart/form-data">
    <div class="Common">
        <div class="tablediv">
            <div class="rowdiv">
                <label>
                    Clicking the button below will result in a PDF document being converted from Excel document using Essential XlsIO and Essential PDF.
                    Please note that you need to have a PDF viewer installed in order to view the generated PDF file.
                </label>
                <br />
                <br />
                <label>Select Document</label>
                <br />
                 @Html.TextBox("file", "", new { type = "file", accept = ".xlsx,.xls,.xlsm,.xltx", @style = "display:inline"})
                <input class="buttonStyle" type="submit" value="Convert to PDF" name="button" style="width:150px" />
            </div>
            <br />
        </div>
    </div>
</form>
     }
{% endhighlight %}

{% highlight Xamarin %}
//XlsIO supports excel to pdf conversion in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms alone.This below code shows how to achieve excel to pdf conversion using a web service.

//Gets assembly
Assembly assembly = typeof(App).GetTypeInfo().Assembly;

//Gets input Excel document from embedded resource collection
Stream inputStream = assembly.GetManifestResourceStream("ExcelToPDF.ExceltoPDF.xlsx");

//Creates new instance of HttpClient to access service
HttpClient client = new HttpClient();

//Gets Uri 
string requestUri = "http://js.syncfusion.com/demos/ioservices/api/excel/converttopdf";

//Posts input Excel document to service and gets resultant PDF as content of HttpResponseMessage
HttpResponseMessage response = null;
response = await client.PostAsync(requestUri, new StreamContent(inputStream));

//Dispose the input stream and client instances
inputStream.Dispose();
client.Dispose();

MemoryStream outputStream = null;

//Gets PDF from content stream if service got success
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

//The operation in SaveAndView under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer xlsio/xamarin section for respective code samples.

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

## Web Service

{% tabs %}
{% highlight c# %}
HttpFileCollection files = HttpContext.Current.Request.Files;
if (files.Count == 0)
    return;
	
using (Stream stream = files[0].InputStream)
{
  //Loads an existing Excel document stream
  using (ExcelEngine engine = new ExcelEngine())
  {
    IApplication application = engine.Excel;
	
    //Initializes the ChartToImageConverter for converting charts during Excel to PDF conversion
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
Using stream As Stream = files(0).InputStream
      Using engine As ExcelEngine = New ExcelEngine()
          Dim application As IApplication = engine.Excel
          application.ChartToImageConverter = New ChartToImageConverter()
          application.ChartToImageConverter.ScalingMode = ScalingMode.Normal
          Using excelToPDFConverter As ExcelToPdfConverter = New ExcelToPdfConverter(stream)
              Using pdfDocument As PdfDocument = excelToPDFConverter.Convert()
                  pdfDocument.Save("ExcelToPDF.pdf", HttpContext.Current.Response, HttpReadType.Save)
                  pdfDocument.Close(True)
              End Using
          End Using
      End Using
End Using
{% endhighlight %}
{% endtabs %}

To know more about different conversion settings in Excel to PDF conversion, please refer ExcelToPdfConverterSettings in API section.

## Worksheet to PDF

The following code shows how to convert a particular sheet to PDF Document.

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
//XlsIO supports excel to pdf conversion in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms alone.Please refer the Workbook to PDF section to use a web service for Excel to PDF conversion.
{% endhighlight %}

{% highlight ASP.NET Core %}
//XlsIO supports excel to pdf conversion in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms alone.Please refer the Workbook to PDF section to use a web service for Excel to PDF conversion.
{% endhighlight %}

{% highlight Xamarin %}
//XlsIO supports excel to pdf conversion in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms alone.Please refer the Workbook to PDF section to use a web service for Excel to PDF conversion.
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
//XlsIO supports excel to pdf conversion in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms alone.Please refer the Workbook to PDF section to use a web service for Excel to PDF conversion.
{% endhighlight %}

{% highlight ASP.NET Core %}
//XlsIO supports excel to pdf conversion in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms alone.Please refer the Workbook to PDF section to use a web service for Excel to PDF conversion.
{% endhighlight %}

{% highlight Xamarin %}
//XlsIO supports excel to pdf conversion in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms alone.Please refer the Workbook to PDF section to use a web service for Excel to PDF conversion.
{% endhighlight %}
{% endtabs %}
  
## Excel with Chart to PDF

To preserve the charts during Excel to PDF conversion, you should initialize the ChartToImageConverter of **IApplication** interface, otherwise the charts present in worksheet will get skipped. The following code illustrate how to convert an Excel with chart to PDF document.

{% tabs %}
{% highlight c# %}
Using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;

  //Instantiating the ChartToImageConverter and assigning the ChartToImageConverter instance of XlsIO application
  application.ChartToImageConverter = new ChartToImageConverter();

  //Tuning Chart Image Quality
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

  'Tuning Chart Image Quality
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
//XlsIO supports excel to pdf conversion in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms alone.Please refer the Workbook to PDF section to use a web service for Excel to PDF conversion.
{% endhighlight %}

{% highlight ASP.NET Core %}
//XlsIO supports excel to pdf conversion in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms alone.Please refer the Workbook to PDF section to use a web service for Excel to PDF conversion.
{% endhighlight %}

{% highlight Xamarin %}
//XlsIO supports excel to pdf conversion in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms alone.Please refer the Workbook to PDF section to use a web service for Excel to PDF conversion.
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
Using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  IWorkbook workbook = application.Workbooks.Open("Excel.xlsx"));

  // Convert the workbook.
  ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);

  // Print the converted PDF document.
  converter.Print();
}
{% endhighlight %}

{% highlight vb %}

Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  Dim workbook As IWorkbook = application.Workbooks.Open("Excel.xlsx")

  'Convert the workbook.
  Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(workbook)

  'Print the converted PDF document.
  converter.Print()
End Using
{% endhighlight %}

{% highlight UWP %}
//XlsIO supports excel to pdf conversion in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms alone.Please refer the Workbook to PDF section to use a web service for Excel to PDF conversion.
{% endhighlight %}

{% highlight ASP.NET Core %}
//XlsIO supports excel to pdf conversion in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms alone.Please refer the Workbook to PDF section to use a web service for Excel to PDF conversion.
{% endhighlight %}

{% highlight Xamarin %}
//XlsIO supports excel to pdf conversion in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms alone.Please refer the Workbook to PDF section to use a web service for Excel to PDF conversion.
{% endhighlight %}
{% endtabs %}

### Print with printer settings.

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

  //Print the converted PDF document with printer settings.
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
//XlsIO supports excel to pdf conversion in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms alone.Please refer the Workbook to PDF section to use a web service for Excel to PDF conversion.
{% endhighlight %}

{% highlight ASP.NET Core %}
//XlsIO supports excel to pdf conversion in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms alone.Please refer the Workbook to PDF section to use a web service for Excel to PDF conversion.
{% endhighlight %}

{% highlight Xamarin %}
//XlsIO supports excel to pdf conversion in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms alone.Please refer the Workbook to PDF section to use a web service for Excel to PDF conversion.
{% endhighlight %}
{% endtabs %}

### Print with Excel to PDF converter settings.

The following code snippet illustrates how to print the Excel document with Excel to PDF converter settings in XlsIO.

{% tabs %}  
{% highlight c# %}
Using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  IWorkbook workbook = application.Workbooks.Open("Excel.xlsx");

  //Convert the workbook
  ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);

  //Initializes the Excel to PDF converter setting class
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

  'Initialize the Excel to PDF converter setting class
  Dim converterSettings As ExcelToPdfConverterSettings = New ExcelToPdfConverterSettings

  'Layout the page using FitAllColumnsOnOnePage options
  converterSettings.DisplayGridLines = GridLinesDisplayStyle.Visible
  converterSettings.LayoutOptions = LayoutOptions.FitAllColumnsOnOnePage

  'Print the converted PDF document with converter settings
  converter.Print(converterSettings)
End Using
{% endhighlight %}

{% highlight UWP %}
//XlsIO supports excel to pdf conversion in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms alone.Please refer the Workbook to PDF section to use a web service for Excel to PDF conversion.
{% endhighlight %}

{% highlight ASP.NET Core %}
//XlsIO supports excel to pdf conversion in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms alone.Please refer the Workbook to PDF section to use a web service for Excel to PDF conversion.
{% endhighlight %}

{% highlight Xamarin %}
//XlsIO supports excel to pdf conversion in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms alone.Please refer the Workbook to PDF section to use a web service for Excel to PDF conversion.
{% endhighlight %}
{% endtabs %}

### Print with printer settings and Excel to PDF converter settings.

The following code snippet illustrates how to print the Excel document with Excel to PDF converter settings and printer settings in XlsIO.

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

  //Initializes the Excel to PDF converter setting class
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

  'Initialize the Excel to PDF converter setting class
  Dim converterSettings As ExcelToPdfConverterSettings = New ExcelToPdfConverterSettings

  'Layout the page using FitAllColumnsOnOnePage options
  converterSettings.DisplayGridLines = GridLinesDisplayStyle.Visible
  converterSettings.LayoutOptions = LayoutOptions.FitAllColumnsOnOnePage

  'Print the converted PDF document with printer settings and converter settings
  converter.Print(printerSettings, converterSettings)
End Using
{% endhighlight %}

{% highlight UWP %}
//XlsIO supports excel to pdf conversion in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms alone.Please refer the Workbook to PDF section to use a web service for Excel to PDF conversion.
{% endhighlight %}

{% highlight ASP.NET Core %}
//XlsIO supports excel to pdf conversion in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms alone.Please refer the Workbook to PDF section to use a web service for Excel to PDF conversion.
{% endhighlight %}

{% highlight Xamarin %}
//XlsIO supports excel to pdf conversion in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms alone.Please refer the Workbook to PDF section to use a web service for Excel to PDF conversion.
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

​## Unsupported Elements

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
* AutoShapes