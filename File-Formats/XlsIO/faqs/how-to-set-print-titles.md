---
title: How to set print titles | XlsIO | Syncfusion
description: This page demonstrates with an example to set print titles using Syncfusion .NET Excel library (XlsIO).
platform: File-formats
control: XlsIO
documentation: UG
---

# How to set print titles?

**Printing** **Title** **Rows**

XlsIO allows to designate row header to repeat on all pages of a printed workbook using **PrintTitleRows** property. The following code snippet illustrates this.

{% tabs %}  

{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Excel2013;

    IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

    IWorksheet worksheet = workbook.Worksheets[0];

    //Print Rows 1 to 3 on every printed page

    worksheet.PageSetup.PrintTitleRows = "$A$1:$IV$3";

    workbook.SaveAs("TitleRows.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Excel2013

    Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

    Dim worksheet As IWorksheet = workbook.Worksheets(0)

    'Print Rows 1 to 3 on every printed page

    worksheet.PageSetup.PrintTitleRows = "$A$1:$IV$3"

    workbook.SaveAs("TitleRows.xlsx")
End Using
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    Stream inputStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
    IWorkbook workbook = await application.Workbooks.OpenAsync(inputStream, ExcelOpenType.Automatic);

    IWorksheet worksheet = workbook.Worksheets[0];

    //Print Rows 1 to 3 on every printed page
    worksheet.PageSetup.PrintTitleRows = "$A$1:$IV$3";

    //Initializes FileSavePicker
    FileSavePicker savePicker = new FileSavePicker();
    savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
    savePicker.SuggestedFileName = "TitleRows";
    savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

    //Creates a storage file from FileSavePicker
    StorageFile storageFile = await savePicker.PickSaveFileAsync();

    //Saves changes to the specified storage file
    await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    FileStream inputStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
    IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelOpenType.Automatic);

    IWorksheet worksheet = workbook.Worksheets[0];

    //Print Rows 1 to 3 on every printed page
    worksheet.PageSetup.PrintTitleRows = "$A$1:$IV$3";

    FileStream stream = new FileStream("TitleRows.xlsx", FileMode.OpenOrCreate, FileAccess.ReadWrite);
    workbook.SaveAs(stream);

    workbook.Close();
    excelEngine.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    Assembly assembly = typeof(App).GetTypeInfo().Assembly;
    Stream fileStream = assembly.GetManifestResourceStream("App.Sample.xlsx");
    IWorkbook workbook = application.Workbooks.Open(fileStream);

    IWorksheet worksheet = workbook.Worksheets[0];

    //Print Rows 1 to 3 on every printed page
    worksheet.PageSetup.PrintTitleRows = "$A$1:$IV$3";

    MemoryStream stream = new MemoryStream();
    workbook.SaveAs(stream);

    stream.Position = 0;

    //Save the stream as a file in the device and invoke it for viewing
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("TitleRows.xlsx", "application/msexcel", stream);
}
{% endhighlight %}

  {% endtabs %}  

**Printing** **Title** **Columns**

XlsIO allows to designate column header to repeat on all pages of a printed workbook using **PrintTitleColumns** property. The following code illustrates printing Title Columns.

{% tabs %}  

{% highlight c# tabtitle="C#" %}
ExcelEngine excelEngine = new ExcelEngine();            

IApplication application = excelEngine.Excel;

application.DefaultVersion = ExcelVersion.Excel2013;

IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

IWorksheet worksheet = workbook.Worksheets[0];

//Print Columns 1 to 3 on every printed page

worksheet.PageSetup.PrintTitleColumns = "$A$1:$C$65536";

workbook.SaveAs("TitleColumns.xlsx");

workbook.Close();

excelEngine.Dispose();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

application.DefaultVersion = ExcelVersion.Excel2013

Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

Dim worksheet As IWorksheet = workbook.Worksheets(0)

'Print Columns 1 to 3 on every printed page

worksheet.PageSetup.PrintTitleColumns = "$A$1:$C$65536"

workbook.SaveAs("TitleColumns.xlsx")

workbook.Close()

excelEngine.Dispose()
{% endhighlight %}

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    Stream inputStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
    IWorkbook workbook = await application.Workbooks.OpenAsync(inputStream, ExcelOpenType.Automatic);

    IWorksheet worksheet = workbook.Worksheets[0];

    //Print Columns 1 to 3 on every printed page
    worksheet.PageSetup.PrintTitleColumns = "$A$1:$C$65536";

    //Initializes FileSavePicker
    FileSavePicker savePicker = new FileSavePicker();
    savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
    savePicker.SuggestedFileName = "TitleColumns";
    savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

    //Creates a storage file from FileSavePicker
    StorageFile storageFile = await savePicker.PickSaveFileAsync();

    //Saves changes to the specified storage file
    await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight c# tabtitle="ASP.NET Core" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    FileStream inputStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
    IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelOpenType.Automatic);

    IWorksheet worksheet = workbook.Worksheets[0];

    //Print Columns 1 to 3 on every printed page
    worksheet.PageSetup.PrintTitleColumns = "$A$1:$C$65536";

    FileStream stream = new FileStream("TitleColumns.xlsx", FileMode.OpenOrCreate, FileAccess.ReadWrite);
    workbook.SaveAs(stream);

    workbook.Close();
    excelEngine.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    Assembly assembly = typeof(App).GetTypeInfo().Assembly;
    Stream fileStream = assembly.GetManifestResourceStream("App.Sample.xlsx");
    IWorkbook workbook = application.Workbooks.Open(fileStream);

    IWorksheet worksheet = workbook.Worksheets[0];

    //Print Columns 1 to 3 on every printed page
    worksheet.PageSetup.PrintTitleColumns = "$A$1:$C$65536";

    MemoryStream stream = new MemoryStream();
    workbook.SaveAs(stream);

    stream.Position = 0;

    //Save the stream as a file in the device and invoke it for viewing
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("TitleColumns.xlsx", "application/msexcel", stream);
}
{% endhighlight %}

  {% endtabs %}  

For information on Print settings, refer to section [Page Setup Settings](/file-formats/xlsio/working-with-excel-worksheet#page-setup-settings).

## See Also

* [How to ignore print areas set in a worksheet?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-ignore-print-areas-set-in-a-worksheet)
* [How to set a line break inside a cell?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-set-a-line-break-inside-a-cell)
* [How to set or format a Header/Footer?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-set-or-format-a-header-footer)
* [How to print Excel document?](https://help.syncfusion.com/file-formats/xlsio/excel-to-pdf-conversion#print-excel-document)
* [What are page setup settings?](https://help.syncfusion.com/file-formats/xlsio/working-with-excel-worksheet#page-setup-settings)
