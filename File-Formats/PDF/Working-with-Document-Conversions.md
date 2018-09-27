---
title: Working with Document Conversion
description: This section explains converting other document Types into PDF
platform: file-formats
control: PDF
documentation: UG
---
# Working with Document Conversions

## Converting Word documents to PDF

Essential PDF allows you to convert a Word document into PDF. For converting a Word document to PDF, the following assemblies need to be referenced in your application

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

For UWP, ASP.NET Core and Xamarin applications 
* using Syncfusion.DocIO
* using Syncfusion.DocIO.DLS
* using Syncfusion.DocIORenderer
* using Syncfusion.Pdf

DocToPDFConverter class is responsible for converting a Word document into PDF. The following code snippet illustrates how to convert a Word document into PDF document.

{% tabs %}

{% highlight c# %}


//Load an existing Word document

WordDocument wordDocument = new WordDocument("Template.docx", FormatType.Docx);

//Initialize chart to image converter for converting charts during Word to pdf conversion

wordDocument.ChartToImageConverter = new ChartToImageConverter();

//Create an instance of DocToPDFConverter

DocToPDFConverter converter = new DocToPDFConverter();

//Convert Word document into PDF document

PdfDocument pdfDocument = converter.ConvertToPDF(wordDocument);

//Save the PDF file

pdfDocument.Save("WordtoPDF.pdf");

//Close the instance of document objects

pdfDocument.Close(true);

wordDocument.Close();



{% endhighlight %}

{% highlight vb.net %}


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

{% highlight UWP %}

//Create the file open picker

FileOpenPicker fileOpenPicker = new FileOpenPicker()
{
    ViewMode = PickerViewMode.Thumbnail,

    SuggestedStartLocation = PickerLocationId.PicturesLibrary
};

fileOpenPicker.FileTypeFilter.Add(".doc");

fileOpenPicker.FileTypeFilter.Add(".docx");

StorageFile file = await fileOpenPicker.PickSingleFileAsync();

//Opens storage file.

var stream = await file.OpenReadAsync();

//Clears the text block

TextBlockView.Text = "";

//Loads document from stream

WordDocument document = new WordDocument(stream.AsStream(), FormatType.Automatic);

//Instantiation of DocIORenderer for Word to PDF conversion

DocIORenderer renderer = new DocIORenderer();

//Converts Word document into PDF

PdfDocument pdf = renderer.ConvertToPDF(document);

//Releases all resources used by the Word document and DocIO Renderer objects

renderer.Dispose(); 

document.Close();

//Output stream to save PDF

MemoryStream outputStream = new MemoryStream();

pdf.Save(outputStream);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(outputStream,"WordtoPDF.pdf");

pdf.Close();

{% endhighlight %}

{% highlight ASP.NET Core %}

// Open the file as Stream

FileStream docStream = new FileStream(@"Template.docx", FileMode.Open, FileAccess.Read);

//Loads file stream into Word document

WordDocument wordDocument = new WordDocument(docStream, Syncfusion.DocIO.FormatType.Automatic);

//Instantiation of DocIORenderer for Word to PDF conversion

DocIORenderer render = new DocIORenderer();

//Converts Word document into PDF document

PdfDocument pdfDocument = render.ConvertToPDF(wordDocument);

//Releases all resources used by the Word document and DocIO Renderer objects

render.Dispose();

wordDocument.Dispose();

//Save the document into stream.

MemoryStream stream = new MemoryStream();

pdfDocument.Save(stream);

stream.Position = 0;

//Close the documents.

pdfDocument.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = " WordtoPDF.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Load the Word document as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Template.docx");

//Load the stream into word document

WordDocument wordDocument = new WordDocument(docStream, Syncfusion.DocIO.FormatType.Automatic);

//Instantiation of DocIORenderer for Word to PDF conversion

DocIORenderer render = new DocIORenderer();

//Converts Word document into PDF document

PdfDocument pdfDocument = render.ConvertToPDF(wordDocument);

//Releases all resources used by the Word document and DocIO Renderer objects

render.Dispose();

wordDocument.Dispose();

//Save the document into memory stream

MemoryStream stream = new MemoryStream();

pdfDocument.Save(stream);

stream.Position = 0;

//Close the document 

pdfDocument.Close();

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("WordtoPDF.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("WordtoPDF.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}

Note:

* Word to PDF conversion is not supported in Silverlight, Windows Phone, WinRT, Universal, Xamarin and UWP applications
* Initializing the ChartToImageConverter is mandatory to convert the charts present in the Word document to PDF. Otherwise the charts will not be exported to the converted PDF
* ChartToImageConverter is supported from .NET Framework 4.0 onwards
* Total number of pages may vary  based on unsupported elements in the converted PDF document when compare to Word document


### Customizing the Word document to PDF conversion

Essential DocIO allows you to customize the Word to PDF conversion with the below options:

* Allows to determine the quality of the charts in the converted PDF
* Allows to determine the quality of the JPEG images in the converted PDF
* Allows to reduce the Main Memory usage in Word to PDF conversion by reusing the identical images.

{% tabs %}

{% highlight c# %}



//Loads an existing Word document

WordDocument wordDocument = new WordDocument("Sample_Image.docx", FormatType.Docx);

//Initialize chart to image converter for converting charts during Word to pdf conversion

wordDocument.ChartToImageConverter = new ChartToImageConverter();

//Set the scaling mode for charts

wordDocument.ChartToImageConverter.ScalingMode = ScalingMode.Normal;

//create an instance of DocToPDFConverter - responsible for Word to PDF conversion

DocToPDFConverter converter = new DocToPDFConverter();

//Set the image quality

converter.Settings.ImageQuality = 100;

//Set the image resolution

converter.Settings.ImageResolution = 640;

//Set true to optimize the memory usage for identical images

converter.Settings.OptimizeIdenticalImages = true;

//Convert Word document into PDF document

PdfDocument pdfDocument = converter.ConvertToPDF(wordDocument);

//Save the PDF file to file system

pdfDocument.Save("WordtoPDF.pdf");

//close the instance of document objects

pdfDocument.Close(true);

wordDocument.Close();



{% endhighlight %}

{% highlight vb.net %}


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

{% highlight UWP %}

//Essential PDF supports customizing the Word document to PDF conversion only in Windows Forms, WPF, ASP.NET and ASP.NET MVC Platforms.

{% endhighlight %}

{% highlight ASP.NET Core %}

//Essential PDF supports customizing the Word document to PDF conversion only in Windows Forms, WPF, ASP.NET and ASP.NET MVC Platforms.

{% endhighlight %}

{% highlight Xamarin %}

//Essential PDF supports customizing the Word document to PDF conversion only in Windows Forms, WPF, ASP.NET and ASP.NET MVC Platforms.

{% endhighlight %}

{% endtabs %}



## Converting Excel documents to PDF

Essential PDF allows you to convert an entire workbook or a single worksheet into PDF document. For converting an Excel document to PDF, the following assemblies need to be referenced in your application

* Syncfusion.XlsIO.Base.dll
* Syncfusion.Compression.Base.dll
* Syncfusion.ExcelToPDFConverter.Base.dll
* Syncfusion.ExcelChartToImageConverter.Wpf.dll
* Syncfusion.SfChart.Wpf.dll
* Syncfusion.Shared.Wpf.dll
* Syncfusion.Pdf.Base.dll

### Converting  a Workbook to PDF

Essential PDF supports Excel to PDF conversion in Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms. To achieve Excel to PDF conversion in other platforms like UWP, Xamarin, ASP.NET Core it is recommended to use web service.

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

//Save the pdf file

pdfDocument.Save("ExcelToPDF.pdf");

//Dispose the objects

pdfDocument.Close();

converter.Dispose();

workbook.Close();

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb.net %}


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

'Save the pdf file

pdfDocument.Save("ExcelToPDF.pdf")

'Dispose the objects

pdfDocument.Close()

converter.Dispose()

workbook.Close()

excelEngine.Dispose()

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
FileStream stream = new FileStream("ExcelToPDF.pdf", FileMode.Create, FileAccess.ReadWrite);
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

To know more about ExcelToPdf conversion settings, please refer ExcelToPdfConverterSettings – LINK API reference


### Converting a Worksheet to PDF

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

pdfDocument.Save("ExcelToPDF.pdf");

pdfDocument.Close();

converter.Dispose();

workbook.Close();
excelEngine.Dispose();



{% endhighlight %}

{% highlight vb.net %}


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

pdfDocument.Save("ExcelToPDF.pdf")

'Dispose the objects

pdfDocument.Close()

converter.Dispose()

workbook.Close()

excelEngine.Dispose()

{% endhighlight %}

{% highlight UWP %}

//Essential PDF supports Excel to PDF conversion only in Windows Forms, WPF, ASP.NET, ASP.NET MVC platforms. Refer to the Workbook to PDF section to convert using web service.

{% endhighlight %}

{% highlight ASP.NET Core %}

//Essential PDF supports Excel to PDF conversion only in Windows Forms, WPF, ASP.NET, ASP.NET MVC platforms. Refer to the Workbook to PDF section to convert using web service.

{% endhighlight %}

{% highlight Xamarin %}

//Essential PDF supports Excel to PDF conversion only in Windows Forms, WPF, ASP.NET, ASP.NET MVC platforms. Refer to the Workbook to PDF section to convert using web service.

{% endhighlight %}

{% endtabs %}



### Creating individual PDF document for each worksheet

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

{% highlight vb.net %}


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

{% highlight UWP %}

//Essential PDF supports Excel to PDF conversion only in Windows Forms, WPF, ASP.NET, ASP.NET MVC platforms. Refer to the Workbook to PDF section to convert using web service.

{% endhighlight %}

{% highlight ASP.NET Core %}

//Essential PDF supports Excel to PDF conversion only in Windows Forms, WPF, ASP.NET, ASP.NET MVC platforms. Refer to the Workbook to PDF section to convert using web service.

{% endhighlight %}

{% highlight Xamarin %}

//Essential PDF supports Excel to PDF conversion only in Windows Forms, WPF, ASP.NET, ASP.NET MVC platforms. Refer to the Workbook to PDF section to convert using web service.

{% endhighlight %}

{% endtabs %}

### Excel with Chart to PDF

To preserve the charts during Excel to PDF conversion, you should initialize the ChartToImageConverter of IApplication interface, otherwise the charts present in worksheet will get skipped. The following code illustrate how to convert an Excel with chart to PDF document.

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

{% highlight vb.net %}


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

{% highlight UWP %}

//Essential PDF supports Excel to PDF conversion only in Windows Forms, WPF, ASP.NET, ASP.NET MVC platforms. Refer to the Workbook to PDF section to convert using web service.

{% endhighlight %}

{% highlight ASP.NET Core %}

//Essential PDF supports Excel to PDF conversion only in Windows Forms, WPF, ASP.NET, ASP.NET MVC platforms. Refer to the Workbook to PDF section to convert using web service.

{% endhighlight %}

{% highlight Xamarin %}

//Essential PDF supports Excel to PDF conversion only in Windows Forms, WPF, ASP.NET, ASP.NET MVC platforms. Refer to the Workbook to PDF section to convert using web service.

{% endhighlight %}

{% endtabs %}

N> This section is applicable only to the Windows Forms, ASP.NET, MVC and WPF platforms.



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

​

### Unsupported Elements

The following list contains unsupported elements that presently will not be preserved in the generated PDF document.

* Grouping columns
* OLE Objects
* Text rotations
* Background images

## Converting RTF documents to PDF

Essential PDF allows you to convert a RTF to PDF document. For converting a RTF to PDF, the following assemblies need to be referenced in your application

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

* using Syncfusion.DocIO
* using Syncfusion.DocIO.DLS
* using Syncfusion.DocToPDFConverter
* using Syncfusion.Pdf

DocToPDFConverter class is responsible for converting a RTF to PDF. The following code snippet illustrates how to convert a RTF to PDF document.

{% tabs %}

{% highlight c# %}


//Load an existing RTF document

WordDocument rtfDocument = new WordDocument(inputFileName);

//Create an instance of DocToPDFConverter

DocToPDFConverter converter = new DocToPDFConverter();

//Convert Word document into PDF document

PdfDocument pdfDocument = converter.ConvertToPDF(rtfDocument);

//Save the PDF file

pdfDocument.Save("RTFToPDF.pdf");

//Close the instance of document objects

pdfDocument.Close(true);

rtfDocument.Close();



{% endhighlight %}

{% highlight vb.net %}


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

{% highlight UWP %}

//Create the file open picker

FileOpenPicker fileOpenPicker = new FileOpenPicker()
{
    ViewMode = PickerViewMode.Thumbnail,

    SuggestedStartLocation = PickerLocationId.PicturesLibrary
};

fileOpenPicker.FileTypeFilter.Add(".rtf");

//fileOpenPicker.FileTypeFilter.Add(".docx");

StorageFile file = await fileOpenPicker.PickSingleFileAsync();

//Opens storage file.

var stream = await file.OpenReadAsync();

//Clears the text block

TextBlockView.Text = "";

//Loads document from stream

WordDocument document = new WordDocument(stream.AsStream(), FormatType.Automatic);

//Instantiation of DocIORenderer for Word to PDF conversion

DocIORenderer renderer = new DocIORenderer();

//Converts Word document into PDf

PdfDocument pdf = renderer.ConvertToPDF(document);

//Releases all resources used by the Word document and DocIO Renderer objects

renderer.Dispose(); 

document.Close();

//Output stream to save PDF

MemoryStream outputStream = new MemoryStream();

pdf.Save(outputStream);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples

Save(outputStream,"RTFToPDF.pdf");

pdf.Close();

{% endhighlight %}

{% highlight ASP.NET Core %}

// Open the file as Stream

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

//Save the document into stream.

MemoryStream stream = new MemoryStream();

pdfDocument.Save(stream);

stream.Position = 0;

//Close the documents.

pdfDocument.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = " RTFToPDF.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Load the Word document as stream

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Input.rtf");

//Load an existing Word document

WordDocument rtfDocument = new WordDocument(docStream, Syncfusion.DocIO.FormatType.Automatic);

//Instantiation of DocIORenderer for Word to PDF conversion

DocIORenderer render = new DocIORenderer();

//Converts Word document into PDF document

PdfDocument pdfDocument = render.ConvertToPDF(rtfDocument);

//Releases all resources used by the Word document and DocIO Renderer objects

render.Dispose();

rtfDocument.Dispose();

//Save the document into memory stream

MemoryStream stream = new MemoryStream();

pdfDocument.Save(stream);

stream.Position = 0;

//Close the document 

pdfDocument.Close();

//Save the stream into pdf file

//The operation in Save under Xamarin varies between Windows Phone, Android and iOS platforms. Please refer PDF/Xamarin section for respective code samples.

if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
{
    Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("RTFToPDF.pdf", "application/pdf", stream);
}
else
{
    Xamarin.Forms.DependencyService.Get<ISave>().Save("RTFToPDF.pdf", "application/pdf", stream);
}

{% endhighlight %}

{% endtabs %}


N> 1. RTF to PDF conversion is not supported in Silverlight, Windows Phone, WinRT, Universal, Xamarin and UWP applications.
N> 2. Total number of pages may vary  based on unsupported elements in the converted PDF document when compare to RTF document.


### Customizing the RTF to PDF conversion

Essential DocIO allows you to customize the RTF to PDF conversion with the below options:

* Allows to determine the quality of the JPEG images in the converted PDF
* Allows to reduce the Main Memory usage in RTF to PDF conversion by reusing the identical images.


{% tabs %}

{% highlight c# %}



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

{% highlight vb.net %}


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

{% highlight UWP %}

//Essential PDF supports customizing the RTF to PDF conversion only Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

{% endhighlight %}

{% highlight ASP.NET Core %}

//Essential PDF supports customizing the RTF to PDF conversion only Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

{% endhighlight %}

{% highlight Xamarin %}

//Essential PDF supports customizing the RTF to PDF conversion only Windows Forms, WPF, ASP.NET and ASP.NET MVC platforms.

{% endhighlight %}

{% endtabs %}



## Converting TIFF to PDF

### Converting multi page TIFF to PDF

Multi frame TIFF image can be converted to PDF document. This can be done by accessing each frame of the multi frame TIFF image and rendering it in each page of the PDF document.

The code snippet to illustrate the same is given below.

{% tabs %}

{% highlight c# %}


//Create a PDF document

PdfDocument pdfDocument = new PdfDocument();

//Add a section to the PDF document

PdfSection section = pdfDocument.Sections.Add();

//Declare the PDF page

PdfPage page;

//Declare PDF page graphics

PdfGraphics graphics;

//Load multi frame TIFF image

PdfBitmap tiffImage = new PdfBitmap("image.tiff");

//Get the frame count

int frameCount = tiffImage.FrameCount;

//Access each frame draw into the page

for (int i = 0; i < frameCount; i++)

{

page = section.Pages.Add();

section.PageSettings.Margins.All = 0;

graphics = page.Graphics;

tiffImage.ActiveFrame = i;

graphics.DrawImage(tiffImage, 0, 0, page.GetClientSize().Width, page.GetClientSize().Height);

}

//Save and close the document

pdfDocument.Save("Sample.pdf");

pdfDocument.Close(true);



{% endhighlight %}



{% highlight vb.net %}


'Create a PDF document

Dim pdfDocument As New PdfDocument()

'Add a section to the PDF document

Dim section As PdfSection = pdfDocument.Sections.Add()

'Declare the PDF page

Dim page As PdfPage

'Declare PDF page graphics

Dim graphics As PdfGraphics

'Load multi frame TIFF image

Dim tiffImage As New PdfBitmap("image.tiff")

'Get the frame count

Dim frameCount As Integer = tiffImage.FrameCount

'Access each frame draw into the page

For i As Integer = 0 To frameCount - 1

page = section.Pages.Add()

section.PageSettings.Margins.All = 0

graphics = page.Graphics

tiffImage.ActiveFrame = i

graphics.DrawImage(tiffImage, 0, 0, page.GetClientSize().Width, page.GetClientSize().Height)

Next

'Save and close the document

pdfDocument.Save("Sample.pdf")

pdfDocument.Close(True)

{% endhighlight %}

{% highlight UWP %}

//Create a PDF document

PdfDocument pdfDocument = new PdfDocument();

//Add a section to the PDF document

PdfSection section = pdfDocument.Sections.Add();

//Declare the PDF page

PdfPage page;

//Declare PDF page graphics

PdfGraphics graphics;

//Load multi frame TIFF image

Stream imageStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.image.tiff");

PdfBitmap tiffImage = new PdfBitmap(imageStream);

//Get the frame count

int frameCount = tiffImage.FrameCount;

//Access each frame draw into the page

for (int i = 0; i < frameCount; i++)

{

    page = section.Pages.Add();

    section.PageSettings.Margins.All = 0;

    graphics = page.Graphics;

    tiffImage.ActiveFrame = i;

    graphics.DrawImage(tiffImage, 0, 0, page.GetClientSize().Width, page.GetClientSize().Height);

}

MemoryStream memoryStream = new MemoryStream();

//Save the document.

await pdfDocument.SaveAsync(memoryStream);

//Close the documents.

pdfDocument.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(memoryStream, "Sample.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Essential PDF supports converting multi page TIFF to PDF only in Windows Forms, WPF, ASP.NET, ASP.NET MVC and UWP platforms.

{% endhighlight %}

{% highlight Xamarin %}

//Essential PDF supports converting multi page TIFF to PDF only in Windows Forms, WPF, ASP.NET, ASP.NET MVC and UWP platforms.

{% endhighlight %}

{% endtabs %}


### Compression in monochrome images

Essential PDF supports JBIG2 compression for best compression of monochrome images.

Refer the below code snippet to draw a single frame monochrome TIFF image with JBIG2 compression

{% tabs %}

{% highlight c# %}


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



{% highlight vb.net %}


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

{% highlight UWP %}

//Essential PDF supports compressing monochrome images only in Windows Forms, WPF, ASP.NET, ASP.NET MVC and UWP platforms.

{% endhighlight %}

{% highlight ASP.NET Core %}

//Essential PDF supports compressing monochrome images only in Windows Forms, WPF, ASP.NET, ASP.NET MVC and UWP platforms.

{% endhighlight %}

{% highlight Xamarin %}

//Essential PDF supports compressing monochrome images only in Windows Forms, WPF, ASP.NET, ASP.NET MVC and UWP platforms.

{% endhighlight %}

{% endtabs %}

N> 1. Currently the JBIG2Decode compression is supported only in lossy mode and also only single frame TIFF images are supported.
N> 2. By default, all monochrome images will be compressed in CITTT4 compression.


## Converting XPS document to PDF

The XPS (XML Paper Specification) document format is a fixed document format which consists of structured XML markup that defines the layout of a document and the visual appearance of each page, along with rendering rules for distributing, archiving, rendering, processing and printing the documents.

Essential PDF provides support for converting XPS to PDF using XPSToPdfConverter class.

The below code illustrates how to convert XPS to PDF.

{% tabs %}

{% highlight c# %}


//Create converter class.

XPSToPdfConverter converter = new XPSToPdfConverter();

//Convert the XPS to PDF.

PdfDocument document = converter.Convert(xpsFileName);

//Save and close the document.

document.Save("Sample.pdf");

document.Close(true);



{% endhighlight %}

{% highlight vb.net %}

'Create converter class.

Dim converter As New XPSToPdfConverter()

'Convert the XPS to PDF.

Dim document As PdfDocument = converter.Convert(xpsFileName)

'Save and close the document.

document.Save("Sample.pdf")

document.Close(True)

{% endhighlight %}

{% highlight UWP %}

//Create converter class.

XPSToPdfConverter converter = new XPSToPdfConverter();

//Load the XPS file

Stream fileStream = typeof(MainPage).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.input.xps");

//Convert the XPS to PDF.

PdfDocument document = converter.Convert(fileStream);

MemoryStream memoryStream = new MemoryStream();

//Save the document.

await document.SaveAsync(memoryStream);

//Close the documents.

document.Close(true);

//Save the stream as PDF document file in local machine. Refer to PDF/UWP section for respected code samples.

Save(memoryStream, "Sample.pdf");

{% endhighlight %}

{% highlight ASP.NET Core %}

//Essential PDF supports converting XPS document to PDF only in Windows Forms, WPF, ASP.NET, ASP.NET MVC and UWP platforms.

{% endhighlight %}

{% highlight Xamarin %}

//Essential PDF supports converting XPS document to PDF only in Windows Forms, WPF, ASP.NET, ASP.NET MVC and UWP platforms.

{% endhighlight %}

{% endtabs %}

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

PDF pages can be converted to images. To add PDF to image functionality in an application, you need to add the below mentioned assemblies as reference to the project.

1. Syncfusion.Compression.Base.dll
2. Syncfusion.Pdf.Base.dll
3. Syncfusion.PdfViewer.Windows.dll

The following code snippet illustrates how to convert PDF page into image.

{% tabs %}

{% highlight c# %}


PdfDocumentView documentViewer = new PdfDocumentView();

//Load the PDF document

documentViewer.Load("Input.pdf");

//Export PDF page to image

Bitmap image = documentViewer.ExportAsImage(0);

//Save the image.

image.Save("Output.png", ImageFormat.Png);

documentViewer.Dispose();



{% endhighlight %}

{% highlight vb.net %}


Dim documentViewer As New PdfDocumentView()

'Load the PDF document

documentViewer.Load("Input.pdf")

'Export PDF page to image

Dim image As Bitmap = documentViewer.ExportAsImage(0)

'Save the image.

image.Save("Sample.png", ImageFormat.Png)

documentViewer.Dispose()



{% endhighlight %}

{% endtabs %}


## MHTML to PDF

The MHTML file can be converted to PDF using WebKit rendering engine. Please refer the below code snippet,


Prerequisites - [https://help.syncfusion.com/file-formats/pdf/converting-html-to-pdf#prerequisites-for-windows](https://help.syncfusion.com/file-formats/pdf/converting-html-to-pdf#prerequisites-for-windows)
    
Troubleshooting - [https://help.syncfusion.com/file-formats/pdf/converting-html-to-pdf#troubleshooting](https://help.syncfusion.com/file-formats/pdf/converting-html-to-pdf#troubleshooting)

{% tabs %}

{% highlight c# %}

//Initialize HTML converter with WebKit rendering engine
HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter(HtmlRenderingEngine.WebKit);

WebKitConverterSettings webKitSettings = new WebKitConverterSettings();

//Set WebKit path
webKitSettings.WebKitPath = @"/QtBinaries/"; 
           
//Assign WebKit settings to HTML converter
htmlConverter.ConverterSettings = webKitSettings;

//Convert MHTML to PDF
PdfDocument document = htmlConverter.Convert("input.mhtml");  
    
//Save the document.
document.Save("Sample.pdf");

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Initialize HTML converter with WebKit rendering engine
Dim htmlConverter As New HtmlToPdfConverter(HtmlRenderingEngine.WebKit)

Dim webKitSettings As New WebKitConverterSettings()

'Set WebKit path
webKitSettings.WebKitPath = "/QtBinaries/"

'Assign WebKit settings to HTML converter
htmlConverter.ConverterSettings = webKitSettings

'Convert MHTML to PDF
Dim document As PdfDocument = htmlConverter.Convert("input.mhtml")

'Save the document.
document.Save("Sample.pdf")

document.Close()

{% endhighlight %}

{% highlight UWP %}

//Essential PDF supports converting MHTML to PDF only in Windows Forms, WPF, ASP.NET, ASP.NET MVC and ASP.NET Core platforms. 

{% endhighlight %}

{% highlight ASP.NET Core %}

//Initialize HTML to PDF converter 

HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter();

WebKitConverterSettings webKitSettings = new WebKitConverterSettings();

//Set WebKit path

webKitSettings.WebKitPath = @"/QtBinaries/";

//Assign WebKit settings to HTML converter

htmlConverter.ConverterSettings = webKitSettings;

//Convert MHTML to PDF

PdfDocument document = htmlConverter.Convert(@"input.mhtml");

//Save the document into stream.

MemoryStream stream = new MemoryStream();

document.Save(stream);

stream.Position = 0;

//Close the documents.

document.Close(true);

//Defining the ContentType for pdf file.

string contentType = "application/pdf";

//Define the file name.

string fileName = " Sample.pdf";

//Creates a FileContentResult object by using the file contents, content type, and file name.

return File(stream, contentType, fileName);

{% endhighlight %}

{% highlight Xamarin %}

//Essential PDF supports converting MHTML to PDF only in Windows Forms, WPF, ASP.NET, ASP.NET MVC and ASP.NET Core platforms. 

{% endhighlight %}

{% endtabs %}


## HTML to MHTML

The WebKit HTML Converter provides support for converting the webpage to MHTML. Please refer the below code snippet,

Prerequisites - [https://help.syncfusion.com/file-formats/pdf/converting-html-to-pdf#prerequisites-for-windows](https://help.syncfusion.com/file-formats/pdf/converting-html-to-pdf#prerequisites-for-windows)
    
Troubleshooting - [https://help.syncfusion.com/file-formats/pdf/converting-html-to-pdf#troubleshooting](https://help.syncfusion.com/file-formats/pdf/converting-html-to-pdf#troubleshooting)

{% tabs %}

{% highlight c# %}

//Initialize HTML converter with WebKit rendering engine
HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter(HtmlRenderingEngine.WebKit);

WebKitConverterSettings webKitSettings = new WebKitConverterSettings();

//Set WebKit path
webKitSettings.WebKitPath = @"/QtBinaries/";

//Assign WebKit settings to HTML converter
htmlConverter.ConverterSettings = webKitSettings;

//Convert URL to MHTML
htmlConverter.ConvertToMhtml("http://www.syncfusion.com", "sample.mhtml");

{% endhighlight %}

{% highlight vb.net %}

'Initialize HTML converter with WebKit rendering engine
Dim htmlConverter As New HtmlToPdfConverter(HtmlRenderingEngine.WebKit)      
  
Dim webKitSettings As New WebKitConverterSettings()

'Set WebKit path
webKitSettings.WebKitPath = "/QtBinaries/"

'Assign WebKit settings to HTML converter
htmlConverter.ConverterSettings = webKitSettings

'Convert URL to MHTML
htmlConverter.ConvertToMhtml("http://www.syncfusion.com", "sample.mhtml")

{% endhighlight %}

{% highlight UWP %}

//Essential PDF supports converting HTML to MHTML only in Windows Forms, WPF, ASP.NET, ASP.NET MVC platforms.

{% endhighlight %}

{% highlight ASP.NET Core %}

//Essential PDF supports converting HTML to MHTML only in Windows Forms, WPF, ASP.NET, ASP.NET MVC platforms.

{% endhighlight %}

{% highlight Xamarin %}

//Essential PDF supports converting HTML to MHTML only in Windows Forms, WPF, ASP.NET, ASP.NET MVC platforms.

{% endhighlight %}

{% endtabs %}


## HTML to Raster Image

The WebKit HTML Converter provides support for converting webpage to Image. Please refer the below code snippet,

Prerequisites - [https://help.syncfusion.com/file-formats/pdf/converting-html-to-pdf#prerequisites-for-windows](https://help.syncfusion.com/file-formats/pdf/converting-html-to-pdf#prerequisites-for-windows)
    
Troubleshooting - [https://help.syncfusion.com/file-formats/pdf/converting-html-to-pdf#troubleshooting](https://help.syncfusion.com/file-formats/pdf/converting-html-to-pdf#troubleshooting)

{% tabs %}

{% highlight c# %}

//Initialize HTML converter with WebKit rendering engine
HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter(HtmlRenderingEngine.WebKit);

WebKitConverterSettings webKitSettings = new WebKitConverterSettings();

//Set WebKit path
webKitSettings.WebKitPath = @"/QtBinaries/";

//Assign WebKit settings to HTML converter
htmlConverter.ConverterSettings = webKitSettings;

//Convert URL to Image
Image[] image = htmlConverter.ConvertToImage("http://www.syncfusion.com");

//Save the image.
image[0].Save("Sample.jpg");

{% endhighlight %}

{% highlight vb.net %}

'Initialize HTML converter with WebKit rendering engine
Dim htmlConverter As New HtmlToPdfConverter(HtmlRenderingEngine.WebKit)

Dim webKitSettings As New WebKitConverterSettings()

'Set WebKit path
webKitSettings.WebKitPath = "/QtBinaries/"

'Assign WebKit settings to HTML converter
htmlConverter.ConverterSettings = webKitSettings

'Convert URL to Image
Dim image As Image() = htmlConverter.ConvertToImage("http://www.syncfusion.com ")

'Save the image.
image(0).Save("Sample.jpg")

{% endhighlight %}

{% highlight UWP %}

//Essential PDF supports converting HTML to raster image only in Windows Forms, WPF, ASP.NET, ASP.NET MVC platforms.

{% endhighlight %}

{% highlight ASP.NET Core %}

//Essential PDF supports converting HTML to raster image only in Windows Forms, WPF, ASP.NET, ASP.NET MVC platforms.

{% endhighlight %}

{% highlight Xamarin %}

//Essential PDF supports converting HTML to raster image only in Windows Forms, WPF, ASP.NET, ASP.NET MVC platforms.

{% endhighlight %}

{% endtabs %}


## HTML string to Raster Image

The WebKit HTML Converter provides support for converting HTML string to Image. Please refer the below code snippet,

Prerequisites - [https://help.syncfusion.com/file-formats/pdf/converting-html-to-pdf#prerequisites-for-windows](https://help.syncfusion.com/file-formats/pdf/converting-html-to-pdf#prerequisites-for-windows)
    
Troubleshooting - [https://help.syncfusion.com/file-formats/pdf/converting-html-to-pdf#troubleshooting](https://help.syncfusion.com/file-formats/pdf/converting-html-to-pdf#troubleshooting)

{% tabs %}

{% highlight c# %}

string htmlString = "<html><body>Hello World!!!</body></html>";
string baseURL = "";

//Initialize HTML converter with WebKit rendering engine
HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter(HtmlRenderingEngine.WebKit);

WebKitConverterSettings webKitSettings = new WebKitConverterSettings();

//Set WebKit path
webKitSettings.WebKitPath = @"/QtBinaries/";

//Assign WebKit settings to HTML converter
htmlConverter.ConverterSettings = webKitSettings;

//Convert HTML string to Image
Image[] image = htmlConverter.ConvertToImage(htmlString, baseURL);

//Save the image.
image[0].Save("Sample.jpg");

{% endhighlight %}

{% highlight vb.net %}

Dim htmlString As String = "<html><body>Hello World!!!</body></html>"
Dim baseURL As String = ""

'Initialize HTML converter with WebKit rendering engine
Dim htmlConverter As New HtmlToPdfConverter(HtmlRenderingEngine.WebKit)

Dim webKitSettings As New WebKitConverterSettings()

'Set WebKit path
webKitSettings.WebKitPath = "/QtBinaries/"

'Assign WebKit settings to HTML converter
htmlConverter.ConverterSettings = webKitSettings

'Convert HTML string to Image
Dim image As Image() = htmlConverter.ConvertToImage(htmlString, baseURL)

'Save the image.
image(0).Save("Sample.jpg")

{% endhighlight %}

{% highlight UWP %}

//Essential PDF supports converting HTML string to raster image only in Windows Forms, WPF, ASP.NET, ASP.NET MVC platforms.

{% endhighlight %}

{% highlight ASP.NET Core %}

//Essential PDF supports converting HTML string to raster image only in Windows Forms, WPF, ASP.NET, ASP.NET MVC platforms.

{% endhighlight %}

{% highlight Xamarin %}

//Essential PDF supports converting HTML string to raster image only in Windows Forms, WPF, ASP.NET, ASP.NET MVC platforms.

{% endhighlight %}

{% endtabs %}


## Partial webpage to Raster Image

The WebKit HTML Converter provides support for converting partial webpage to Image. Please refer the below code snippet,

Prerequisites - [https://help.syncfusion.com/file-formats/pdf/converting-html-to-pdf#prerequisites-for-windows](https://help.syncfusion.com/file-formats/pdf/converting-html-to-pdf#prerequisites-for-windows)
    
Troubleshooting - [https://help.syncfusion.com/file-formats/pdf/converting-html-to-pdf#troubleshooting](https://help.syncfusion.com/file-formats/pdf/converting-html-to-pdf#troubleshooting)

{% tabs %}

{% highlight c# %}

//Initialize HTML converter 

HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter(HtmlRenderingEngine.WebKit);

// WebKit converter settings

WebKitConverterSettings webKitSettings = new WebKitConverterSettings();

//Assign the WebKit binaries path

webKitSettings.WebKitPath = @"/QtBinaries/";

//Assign the WebKit settings

htmlConverter.ConverterSettings = webKitSettings;

//Convert Partial HTML to Image

Image[] image = htmlConverter.ConvertPartialHtmlToImage("input.html", "pic");

//Save Image

image[0].Save("Output.jpg");

{% endhighlight %}

{% highlight vb.net %}

'Initialize HTML converter 

Dim htmlConverter As New HtmlToPdfConverter(HtmlRenderingEngine.WebKit)

' WebKit converter settings

Dim webKitSettings As New WebKitConverterSettings()

'Assign the WebKit binaries path

webKitSettings.WebKitPath = "/QtBinaries/"

'Assign the WebKit settings

htmlConverter.ConverterSettings = webKitSettings

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

{% highlight UWP %}

//Essential PDF supports converting partial webpage to raster image only in Windows Forms, WPF, ASP.NET, ASP.NET MVC platforms.

{% endhighlight %}

{% highlight ASP.NET Core %}

//Essential PDF supports converting partial webpage to raster image only in Windows Forms, WPF, ASP.NET, ASP.NET MVC platforms.

{% endhighlight %}

{% highlight Xamarin %}

//Essential PDF supports converting partial webpage to raster image only in Windows Forms, WPF, ASP.NET, ASP.NET MVC platforms.

{% endhighlight %}

{% endtabs %}



## HTML to SVG

The WebKit HTML Converter provides support for converting HTML to SVG. Please refer the below code snippet,

Prerequisites - [https://help.syncfusion.com/file-formats/pdf/converting-html-to-pdf#prerequisites-for-windows](https://help.syncfusion.com/file-formats/pdf/converting-html-to-pdf#prerequisites-for-windows)
    
Troubleshooting - [https://help.syncfusion.com/file-formats/pdf/converting-html-to-pdf#troubleshooting](https://help.syncfusion.com/file-formats/pdf/converting-html-to-pdf#troubleshooting)

{% tabs %}

{% highlight c# %}

//Initialize HTML converter with WebKit rendering engine
HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter(HtmlRenderingEngine.WebKit);

WebKitConverterSettings webKitSettings = new WebKitConverterSettings();

//Set WebKit path
webKitSettings.WebKitPath = @"/QtBinaries/";

//Assign WebKit settings to HTML converter
htmlConverter.ConverterSettings = webKitSettings;

//Convert URL to SVG
htmlConverter.ConvertToSvg("http://www.syncfusion.com", "sample.svg");

{% endhighlight %}

{% highlight vb.net %}

'Initialize HTML converter with WebKit rendering engine
Dim htmlConverter As New HtmlToPdfConverter(HtmlRenderingEngine.WebKit)

Dim webKitSettings As New WebKitConverterSettings()

'Set WebKit path
webKitSettings.WebKitPath = "/QtBinaries/"

'Assign WebKit settings to HTML converter
htmlConverter.ConverterSettings = webKitSettings

'Convert URL to SVG
htmlConverter.ConvertToSvg("http://www.syncfusion.com", "sample.svg")

{% endhighlight %}

{% highlight UWP %}

//Essential PDF supports converting HTML to SVG only in Windows Forms, WPF, ASP.NET, ASP.NET MVC platforms.

{% endhighlight %}

{% highlight ASP.NET Core %}

//Essential PDF supports converting HTML to SVG only in Windows Forms, WPF, ASP.NET, ASP.NET MVC platforms.

{% endhighlight %}

{% highlight Xamarin %}

//Essential PDF supports converting HTML to SVG only in Windows Forms, WPF, ASP.NET, ASP.NET MVC platforms.

{% endhighlight %}

{% endtabs %}


## Partial webpage to SVG

The WebKit HTML Converter provides support for converting partial webpage to SVG. Please refer the below code snippet,

Prerequisites - [https://help.syncfusion.com/file-formats/pdf/converting-html-to-pdf#prerequisites-for-windows](https://help.syncfusion.com/file-formats/pdf/converting-html-to-pdf#prerequisites-for-windows)
    
Troubleshooting - [https://help.syncfusion.com/file-formats/pdf/converting-html-to-pdf#troubleshooting](https://help.syncfusion.com/file-formats/pdf/converting-html-to-pdf#troubleshooting)

{% tabs %}

{% highlight c# %}

//Initialize HTML converter 

HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter(HtmlRenderingEngine.WebKit);

// WebKit converter settings

WebKitConverterSettings webKitSettings = new WebKitConverterSettings();

//Assign the WebKit binaries path

webKitSettings.WebKitPath = @"/QtBinaries/";

//Assign the WebKit settings

htmlConverter.ConverterSettings = webKitSettings;

//Convert Partial HTML to SVG

htmlConverter.ConvertPartialHtmlToSvg("input.html", "pic", "Output.svg");

{% endhighlight %}

{% highlight vb.net %}

'Initialize HTML converter 

Dim htmlConverter As New HtmlToPdfConverter(HtmlRenderingEngine.WebKit)

' WebKit converter settings

Dim webKitSettings As New WebKitConverterSettings()

'Assign the WebKit binaries path

webKitSettings.WebKitPath = "/QtBinaries/"

'Assign the WebKit settings

htmlConverter.ConverterSettings = webKitSettings

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

{% highlight UWP %}

//Essential PDF supports converting partial webpage to SVG only in Windows Forms, WPF, ASP.NET, ASP.NET MVC platforms.

{% endhighlight %}

{% highlight ASP.NET Core %}

//Essential PDF supports converting partial webpage to SVG only in Windows Forms, WPF, ASP.NET, ASP.NET MVC platforms.

{% endhighlight %}

{% highlight Xamarin %}

//Essential PDF supports converting partial webpage to SVG only in Windows Forms, WPF, ASP.NET, ASP.NET MVC platforms.

{% endhighlight %}

{% endtabs %}
