---
title: How to unfreeze the rows and columns in XlsIO? | XlsIO | Syncfusion
description: This page demonstrates with an example to unfreeze the rows and columns using Syncfusion .NET Excel library (XlsIO).
platform: File-formats
control: XlsIO
documentation: UG
---

# How to unfreeze the rows and columns in XlsIO?

You can unfreeze rows and columns in XlsIO by using the RemovePanes method. The following code snippet illustrates this.

{% tabs %}  

{% highlight c# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Excel2013;

    IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);

    IWorksheet worksheet = workbook.Worksheets[0];

    //Freeze the panes
    worksheet.Range[8, 1].FreezePanes();

    //Unfreeze the panes
    worksheet.RemovePanes();

    workbook.SaveAs("Unfreeze.xlsx");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Excel2013

    Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)

    Dim worksheet As IWorksheet = workbook.Worksheets(0)

    'Freeze the panes
    worksheet.Range(8, 1).FreezePanes()

    'Unfreeze the panes
    worksheet.RemovePanes()

    workbook.SaveAs("Unfreeze.xlsx")
End Using
{% endhighlight %}

{% highlight UWP %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    Stream inputStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
    IWorkbook workbook = await application.Workbooks.OpenAsync(inputStream, ExcelOpenType.Automatic);

    IWorksheet worksheet = workbook.Worksheets[0];

    //Freeze the panes
    worksheet.Range[8, 1].FreezePanes();

    //Unfreeze the panes
    worksheet.RemovePanes();

    //Initializes FileSavePicker
    FileSavePicker savePicker = new FileSavePicker();
    savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
    savePicker.SuggestedFileName = "Unfreeze";
    savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

    //Creates a storage file from FileSavePicker
    StorageFile storageFile = await savePicker.PickSaveFileAsync();

    //Saves changes to the specified storage file
    await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight ASP.NET Core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    FileStream inputStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
    IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelOpenType.Automatic);

    IWorksheet worksheet = workbook.Worksheets[0];

    //Freeze the panes
    worksheet.Range[8, 1].FreezePanes();

    //Unfreeze the panes
    worksheet.RemovePanes();

    FileStream stream = new FileStream("Unfreeze.xlsx", FileMode.OpenOrCreate, FileAccess.ReadWrite);
    workbook.SaveAs(stream);

    workbook.Close();
    excelEngine.Dispose();
}
{% endhighlight %}

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    Assembly assembly = typeof(App).GetTypeInfo().Assembly;
    Stream fileStream = assembly.GetManifestResourceStream("App.Sample.xlsx");
    IWorkbook workbook = application.Workbooks.Open(fileStream);

    IWorksheet worksheet = workbook.Worksheets[0];

    //Freeze the panes
    worksheet.Range[8, 1].FreezePanes();

    //Unfreeze the panes
    worksheet.RemovePanes();

    MemoryStream stream = new MemoryStream();
    workbook.SaveAs(stream);

    stream.Position = 0;

    //Save the stream as a file in the device and invoke it for viewing
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Unfreeze.xlsx", "application/msexcel", stream);
}
{% endhighlight %}

  {% endtabs %}  

## See Also

* [What is the maximum range of Rows and Columns?](faqs/what-is-the-maximum-range-of-rows-and-columns)
* [How to hide the summary rows and columns using XlsIO?](faqs/how-to-hide-the-summary-rows-and-columns-using-xlsio)
* [How to sort two or more columns in a pivot table?](faqs/how-to-sort-two-or-more-columns-in-a-pivot-table)
* [How to freeze panes?](https://help.syncfusion.com/file-formats/xlsio/working-with-excel-worksheet#freeze-panes)
* [How to unfreeze panes?](https://help.syncfusion.com/file-formats/xlsio/working-with-excel-worksheet#unfreeze-panes)
* [How to split panes?](https://help.syncfusion.com/file-formats/xlsio/working-with-excel-worksheet#split-panes)
