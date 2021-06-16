---
title: FAQ Section| XlsIO | Syncfusion
description: Code example to open an Excel 2013 Macro Enabled Template using Syncfusion .NET Excel library (XlsIO).
platform: File-formats
control: XlsIO
documentation: UG
---

# How to open an Excel 2013 Macro Enabled Template?

You can open and save an Excel 2013 Macro Enabled Template to XLSM (Excel 2013 Macro Enabled Document) format. The following code snippet illustrates this.

{% tabs %}  

{% highlight c# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Excel2013;

    //Open an existing XLTM file
    IWorkbook workbook = application.Workbooks.Open("Sample.xltm", ExcelOpenType.Automatic);

    //Save the file as XLSM
    workbook.SaveAs("Output.xlsm");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Excel2013

    'Open an existing XLTM file
    Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xltm", ExcelOpenType.Automatic)

    'Save the file as XLSM
    workbook.SaveAs("Output.xlsm")
End Using
{% endhighlight %}

{% highlight UWP %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    
    //Open an existing XLTM file
    Stream inputStream = new FileStream("Sample.xltm", FileMode.Open, FileAccess.Read);
    IWorkbook workbook = await application.Workbooks.OpenAsync(inputStream, ExcelOpenType.Automatic);

    //Save the file as XLSM
    FileSavePicker savePicker = new FileSavePicker();
    savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
    savePicker.SuggestedFileName = "Output";
    savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsm" });
    StorageFile storageFile = await savePicker.PickSaveFileAsync();
    await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight ASP.NET Core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;

    //Open an existing XLTM file
    FileStream inputStream = new FileStream("Sample.xltm", FileMode.Open, FileAccess.Read);
    IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelOpenType.Automatic);

    //Save the file as XLSM
    FileStream outputStream = new FileStream("Output.xlsm", FileMode.OpenOrCreate, FileAccess.ReadWrite);
    workbook.SaveAs(outputStream);

    workbook.Close();
    excelEngine.Dispose();
}
{% endhighlight %}

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;

    //Open an existing XLTM file
    Assembly assembly = typeof(App).GetTypeInfo().Assembly;
    Stream fileStream = assembly.GetManifestResourceStream("App.Sample.xltm");
    IWorkbook workbook = application.Workbooks.Open(fileStream);

    //Save the file as XLSM
    MemoryStream stream = new MemoryStream();
    workbook.SaveAs(stream);

    stream.Position = 0;

    //Save the stream as a file in the device and invoke it for viewing
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsm", "application/vnd.ms-excel.sheet.macroEnabled.12", stream);
}
{% endhighlight %}

  {% endtabs %}  

## See Also

How to check whether an Excel document contains macro?
Does XlsIO support Excel files with macros that are digitally signed?
Does XlsIO support password protected macro in the Excel documents?
[Creating a Macro](https://help.syncfusion.com/file-formats/xlsio/working-with-macros#creating-a-macro)
[Editing a Macro](https://help.syncfusion.com/file-formats/xlsio/working-with-macros#editing-a-macro)
[Removing Macros](https://help.syncfusion.com/file-formats/xlsio/working-with-macros#removing-macros)
