---
title: Syncfusion Excel to PDF Converter Settings
description: In this section, you can learn how to use Excel to PDF converter settings while convert Excel Workbook to PDF & Worksheet to PDF file;
platform: File-formats
control: XlsIO
documentation: UG
---

# Excel to PDF Converter Settings

XlsIO allows you to convert an entire workbook or a single worksheet into PDF document with Excel to PDF converter settings. Refer to the following links for assemblies/nuget packages required based on platforms to convert Excel document into PDF.

* [Assemblies Information](https://help.syncfusion.com/file-formats/xlsio/assemblies-required#converting-excel-document-to-pdf) 
* [NuGet Information](https://help.syncfusion.com/file-formats/xlsio/nuget-packages-required#converting-excel-document-into-pdf)

## PDF Conformance Level

Excel to PDF converter settings allows you to set the PDF conformance level. There are two conformance levels Pdf_A1B and Pdf_X1A2001.
N> 1. To know more details about PDF conformance refer [https://help.syncfusion.com/file-formats/pdf/working-with-pdf-conformance](https://help.syncfusion.com/file-formats/pdf/working-with-pdf-conformance)
N> 2. Pdf_X1A2001 is not supported for NETStandard.

The following code illustrates  how to set the PdfConformanceLevel while converting  Excel workbook to PDF.

{% tabs %}  

{% highlight c# %}
using(ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

  //Open the Excel document to Convert
  ExcelToPdfConverter converter = new ExcelToPdfConverter(workbook);

  //Initialize Excel to PDF converter settings
  ExcelToPdfConverterSettings settings = new ExcelToPdfConverterSettings();
  
  // Set the conformance for PDF/A-1b conversion
  settings.PdfConformanceLevel = PdfConformanceLevel.Pdf_A1B;

  //Convert Excel document into PDF document
  PdfDocument pdfDocument = converter.Convert(settings);

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

  'Initialize Excel to PDF converter settings
  Dim settings As ExcelToPdfConverterSettings = New ExcelToPdfConverterSettings()
  
  'Set the conformance for PDF/A-1b conversion
  settings.PdfConformanceLevel = PdfConformanceLevel.Pdf_A1B

  'Convert Excel document into PDF document
  Dim pdfDocument As PdfDocument = converter.Convert(settings)

  'Save the PDF file
  pdfDocument.Save("ExcelToPDF.pdf")
End Using
{% endhighlight %}

{% highlight UWP %}
//Excel To PDF conversion can be performed by referring .NET Standard assemblies in UWP platform

#region Excel To PDF
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    
    //Gets assembly
    Assembly assembly = typeof(App).GetTypeInfo().Assembly;

    //Gets input Excel document from an embedded resource collection
    Stream excelStream = assembly.GetManifestResourceStream("ExcelToPDF.xlsx");
	
    IWorkbook workbook = await application.Workbooks.OpenAsync(excelStream);

    //Initialize XlsIO renderer.
    XlsIORenderer renderer = new XlsIORenderer();
	
	//Initialize XlsIO renderer settings
	XlsIORendererSettings settings = new XlsIORendererSettings();

    // Set the conformance for PDF/A-1b conversion
    settings.PdfConformanceLevel = PdfConformanceLevel.Pdf_A1B;
  
    //Convert Excel document into PDF document 
    PdfDocument pdfDocument = renderer.ConvertToPDF(workbook, settings);

    //Save the PDF document to stream.
    MemoryStream stream = new MemoryStream();

    await doc.SaveAsync(stream);
    Save(stream, "ExcelToPDF.pdf");

    excelStream.Dispose();
    stream.Dispose();
}
#endregion

//Save the workbook stream as a file.

#region Setting output location
async void Save(Stream stream, string filename)
{
    stream.Position = 0;

    StorageFile stFile;
    if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
    {
        FileSavePicker savePicker = new FileSavePicker();
        savePicker.DefaultFileExtension = ".pdf";
        savePicker.SuggestedFileName = "Sample";
        savePicker.FileTypeChoices.Add("Adobe PDF Document", new List<string>() { ".pdf" });
        stFile = await savePicker.PickSaveFileAsync();
    }
    else
    {
        StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
        stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
    }
    if (stFile != null)
    {
        Windows.Storage.Streams.IRandomAccessStream fileStream = await stFile.OpenAsync(FileAccessMode.ReadWrite);
        Stream st = fileStream.AsStreamForWrite();
        st.Write((stream as MemoryStream).ToArray(), 0, (int)stream.Length);
        st.Flush();
        st.Dispose();
        fileStream.Dispose();
    }
}
#endregion
{% endhighlight %}

{% highlight ASP.NET Core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
   IApplication application = excelEngine.Excel;
   FileStream excelStream = new FileStream("ExcelToPDF.xlsx", FileMode.Open, FileAccess.Read);
   IWorkbook workbook = application.Workbooks.Open(excelStream);

    //Initialize XlsIO renderer.
    XlsIORenderer renderer = new XlsIORenderer();
	
	//Initialize XlsIO renderer settings
	XlsIORendererSettings settings = new XlsIORendererSettings();

    // Set the conformance for PDF/A-1b conversion
    settings.PdfConformanceLevel = PdfConformanceLevel.Pdf_A1B;
  
    //Convert Excel document into PDF document 
    PdfDocument pdfDocument = renderer.ConvertToPDF(workbook, settings);

   Stream stream = new FileStream("ExcelToPDF.pdf", FileMode.Create, FileAccess.ReadWrite);
   pdfDocument.Save(stream);

   excelStream.Dispose();
   stream.Dispose();
}
{% endhighlight %}

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
   
    //Gets assembly
    Assembly assembly = typeof(App).GetTypeInfo().Assembly;

    //Gets input Excel document from an embedded resource collection
    Stream excelStream = assembly.GetManifestResourceStream("ExcelToPDF.xlsx");

    IWorkbook workbook = application.Workbooks.Open(excelStream);

    //Initialize XlsIO renderer.
    XlsIORenderer renderer = new XlsIORenderer();
	
	//Initialize XlsIO renderer settings
	XlsIORendererSettings settings = new XlsIORendererSettings();

    // Set the conformance for PDF/A-1b conversion
    settings.PdfConformanceLevel = PdfConformanceLevel.Pdf_A1B;
  
    //Convert Excel document into PDF document 
    PdfDocument pdfDocument = renderer.ConvertToPDF(workbook, settings);

    //Save the PDF document to stream.
    MemoryStream stream = new MemoryStream();
    pdfDocument.Save(stream);

    stream.Position = 0;

    //Save the stream into pdf file
    if (Device.OS == TargetPlatform.WinPhone || Device.OS == TargetPlatform.Windows)
    {
        Xamarin.Forms.DependencyService.Get<ISaveWindowsPhone>().Save("ExcelToPDF.pdf", "application/pdf", stream);
    }
    else
    {
        Xamarin.Forms.DependencyService.Get<ISave>().Save("ExcelToPDF.pdf", "application/pdf", stream);
    }

    excelStream.Dispose();
    stream.Dispose();
}
{% endhighlight %}

{% endtabs %}
