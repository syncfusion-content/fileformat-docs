---
title: Convert the required range in Excel to PDF | Syncfusion
description: This page shows how to convert the required range of Excel to PDF using the Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# How to convert the required range in Excel to PDF?

A specific range of an Excel worksheet can be converted to PDF by applying page breaks to that particular range and copying it to a new worksheet for conversion. The following code snippet explains this.

{% tabs %}  

{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;
    IWorkbook workbook = application.Workbooks.Open("ExceltoPDF.xlsx");              
    IWorksheet sheet = workbook.Worksheets[0];

    //Initialize ExcelToPdfConverterSettings
    ExcelToPdfConverterSettings settings = new ExcelToPdfConverterSettings();
    settings.LayoutOptions = LayoutOptions.FitAllColumnsOnOnePage;
                             
     //Set Horizontal Page Breaks
    sheet.HPageBreaks.Add(sheet.Range["A40"]);
    //Set Vertical Page Breaks
    sheet.VPageBreaks.Add(sheet.Range["R11"]);

    IWorksheet tempWorksheet = workbook.Worksheets.Create();
    sheet.Range[1, 1, sheet.HPageBreaks[0].Location.Row, sheet.VPageBreaks[0].Location.Column].CopyTo(tempWorksheet.Range[1, 1]);

    //Load the Excel document into ExcelToPdfConverter
    ExcelToPdfConverter converter = new ExcelToPdfConverter(tempWorksheet);
    //Convert the Excel document to PDF with converter settings
    PdfDocument document = converter.Convert(settings);
    //Save the PDF document
    document.Save("ExceltoPDF.pdf");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Xlsx
    Dim workbook As IWorkbook = application.Workbooks.Open("ExceltoPDF.xlsx")
    Dim sheet As IWorksheet = workbook.Worksheets(0)

    'Initialize ExcelToPdfConverterSettings
    Dim settings As ExcelToPdfConverterSettings = New ExcelToPdfConverterSettings()
    'Set layout option as FitAllColumnsOnOnePage
    settings.LayoutOptions = LayoutOptions.FitAllColumnsOnOnePage

    'Set Horizontal Page Breaks
    sheet.HPageBreaks.Add(sheet.Range("A40"))
    'Set Vertical Page Breaks
    sheet.VPageBreaks.Add(sheet.Range("R11"))

    Dim tempWorksheet As IWorksheet = workbook.Worksheets.Create()
    sheet.Range(1, 1, sheet.HPageBreaks(0).Location.Row, sheet.VPageBreaks(0).Location.Column).CopyTo(tempWorksheet.Range(1, 1))

    'Load the Excel document into ExcelToPdfConverter
    Dim converter As ExcelToPdfConverter = New ExcelToPdfConverter(tempWorksheet)
    'Convert the Excel document to PDF with converter settings
    Dim document As PdfDocument = converter.Convert(settings)
    'Save the PDF document
    document.Save("ExceltoPDF.pdf")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
//Excel To PDF conversion can be performed by referring .NET Standard assemblies in UWP platform
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;
	
    //Get assembly
    Assembly assembly = typeof(App).GetTypeInfo().Assembly;
    //Get input Excel document from an embedded resource collection
    Stream excelStream = assembly.GetManifestResourceStream("GettingStarted.ExceltoPDF.xlsx");              
    IWorkbook workbook = application.Workbooks.Open(excelStream);
    IWorksheet sheet = workbook.Worksheets[0];

    //Initialize XlsIORendererSettings
    XlsIORendererSettings settings = new XlsIORendererSettings();
    //Set layout option as FitAllColumnsOnOnePage
    settings.LayoutOptions = LayoutOptions.FitAllColumnsOnOnePage;

    //Set Horizontal Page Breaks
    sheet.HPageBreaks.Add(sheet.Range["A40"]);
    //Set Vertical Page Breaks
    sheet.VPageBreaks.Add(sheet.Range["R11"]);

    IWorksheet tempWorksheet = workbook.Worksheets.Create();
    sheet.Range[1, 1, sheet.HPageBreaks[0].Location.Row, sheet.VPageBreaks[0].Location.Column].CopyTo(tempWorksheet.Range[1, 1]);

    //Initialize XlsIORenderer
    XlsIORenderer renderer = new XlsIORenderer();
    //Convert the Excel document to PDF with renderer settings
    PdfDocument document = renderer.ConvertToPDF(tempWorksheet, settings);

    //Save the PDF document
    MemoryStream stream = new MemoryStream();
    document.Save(stream);
    Save(stream, "ExceltoPDF.pdf");
    excelStream.Dispose();
}

//Save the PDF stream as a file
#region Setting output location
async void Save(Stream stream, string filename)
{
    stream.Position = 0;
    StorageFile stFile;
    if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
    {
         FileSavePicker savePicker = new FileSavePicker();
         savePicker.DefaultFileExtension = ".pdf";
         savePicker.SuggestedFileName = "ExceltoPDF";
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
    stream.Dispose();
}
#endregion
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
	application.DefaultVersion = ExcelVersion.Xlsx;
    FileStream excelStream = new FileStream("ExceltoPDF.xlsx", FileMode.Open, FileAccess.Read);
    IWorkbook workbook = application.Workbooks.Open(excelStream);
    IWorksheet sheet = workbook.Worksheets[0];

    XlsIORendererSettings settings = new XlsIORendererSettings();
    settings.LayoutOptions = LayoutOptions.FitAllColumnsOnOnePage;

    //Set Horizontal Page Breaks
    sheet.HPageBreaks.Add(sheet.Range["A40"]);
    //Set Vertical Page Breaks
    sheet.VPageBreaks.Add(sheet.Range["R11"]);

    IWorksheet tempWorksheet = workbook.Worksheets.Create();
    sheet.Range[1, 1, sheet.HPageBreaks[0].Location.Row, sheet.VPageBreaks[0].Location.Column].CopyTo(tempWorksheet.Range[1, 1]);

    //Initialize XlsIO renderer.
    XlsIORenderer renderer = new XlsIORenderer();
    //Convert Excel document into PDF document
    PdfDocument pdfDocument = renderer.ConvertToPDF(tempWorksheet, settings);
    Stream stream = new FileStream("ExcelToPDF.pdf", FileMode.Create, FileAccess.ReadWrite);
    pdfDocument.Save(stream);
    excelStream.Dispose();
    stream.Dispose();

}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;
    //Gets assembly
    Assembly assembly = typeof(App).GetTypeInfo().Assembly;
    //Gets input Excel document from an embedded resource collection
    Stream excelStream = assembly.GetManifestResourceStream("GettingStarted.ExceltoPDF.xlsx");
    IWorkbook workbook = application.Workbooks.Open(excelStream);
    IWorksheet sheet = workbook.Worksheets[0];

    //Initialize XlsIORendererSettings
    XlsIORendererSettings settings = new XlsIORendererSettings();
    //Set layout option as FitAllColumnsOnOnePage
    settings.LayoutOptions = LayoutOptions.FitAllColumnsOnOnePage;

    //Set Horizontal Page Breaks
    sheet.HPageBreaks.Add(sheet.Range["A40"]);
    //Set Vertical Page Breaks
    sheet.VPageBreaks.Add(sheet.Range["R11"]);

    IWorksheet tempWorksheet = workbook.Worksheets.Create();
    sheet.Range[1, 1, sheet.HPageBreaks[0].Location.Row, sheet.VPageBreaks[0].Location.Column].CopyTo(tempWorksheet.Range[1, 1]);

    //Initialize XlsIORenderer
    XlsIORenderer renderer = new XlsIORenderer();
    //Convert the Excel document to PDF with renderer settings
    PdfDocument document = renderer.ConvertToPDF(tempWorksheet, settings);
    //Save the PDF document to stream
    MemoryStream stream = new MemoryStream();
    document.Save(stream);
    stream.Position = 0;

    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("ExceltoPDF.pdf", "application/pdf", stream);
}
{% endhighlight %}
{% endtabs %}  

## See Also

* [How to overcome Parameter Not valid exception?](reason-for-parameter-not-valid-exception-when-converting-exceltopdf-with-custompapersize)
* [How to open an existing XLSX workbook and save it as XLS?](how-to-open-an-existing-xlsx-workbook-and-save-it-as-xls)
* [How to create and open Excel Template files by using XlsIO?](how-to-create-and-open-excel-template-files-by-using-xlsio)
* [How to copy a range from one workbook to another?](how-to-copy-a-range-from-one-workbook-to-another)
* [Does XlsIO support Excel files with macros that are digitally signed?](does-xlsio-support-excel-files-with-macros-that-are-digitally-signed)
* [How does Excel file with uninstalled fonts is converted to PDF/Image?](how-does-excel-file-with-uninstalled-fonts-is-converted-to-pdf-image)
* [How to sort two or more columns in a pivot table?](how-to-sort-two-or-more-columns-in-a-pivot-table)
* [How to move or copy a worksheet?](https://help.syncfusion.com/file-formats/xlsio/working-with-excel-worksheet#move-or-copy-a-worksheet)

