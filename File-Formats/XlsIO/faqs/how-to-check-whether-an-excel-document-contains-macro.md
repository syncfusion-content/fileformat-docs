---
title: How to check whether an Excel document contains macro | Syncfusion
description: Code example to check whether an Excel document contains macro using Syncfusion .NET Excel library (XlsIO).
platform: File-formats
control: XlsIO
documentation: UG
---

# How to check whether an Excel document contains macro?
You can check whether the Excel document contains macro using **IWorkbook.HasMacro** property. The value true indicates that the Excel document has a Vba project.

The following code illustrate how to check whether an Excel document contains macro using XlsIO.
{% tabs %}  
{% highlight c# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    // Instantiate the excel application object.
    IApplication application = excelEngine.Excel;

    // Opening a workbook
    IWorkbook workbook = application.Workbooks.Open("Test.xls");

    IWorksheet sheet = workbook.Worksheets[0];

    //Check macro exist
    bool IsMacroEnabled = workbook.HasMacros;        
     
   //Save the workbook
    workbook.SaveAs("Output.xls");
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()
    'Instantiate the excel application object.
    Dim application As IApplication = excelEngine.Excel

    'Opening a Workbook
    Dim workbook As IWorkbook = application.Workbooks.Open("Test.xls")
    Dim sheet As IWorksheet = workbook.Worksheets(0)

    'Check macro exist
    Dim IsMacroEnabled As Boolean = workbook.HasMacros            
   
    ‘Save the workbook 
    workbook.SaveAs("Output.xls")
End Using
{% endhighlight %}

{% highlight UWP %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;

    //Instantiates the File Picker
    FileOpenPicker openPicker = new FileOpenPicker();
    openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
    openPicker.FileTypeFilter.Add(".xlsm");
    openPicker.FileTypeFilter.Add(".xltm");
    openPicker.FileTypeFilter.Add(".xls");
    StorageFile file = await openPicker.PickSingleFileAsync();

    //Opening a workbook with a worksheet
    IWorkbook workbook = await application.Workbooks.OpenAsync(file, ExcelOpenType.Automatic);

    IWorksheet worksheet = workbook.Worksheets[0];

    //Check macro exist
    bool IsMacroEnabled = workbook.HasMacros;     
     

    // Save the Workbook
    StorageFile storageFile;
    if (!(Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons")))
    {
        FileSavePicker savePicker = new FileSavePicker();
        savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
        savePicker.SuggestedFileName = "Output";
        savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xls" });
        storageFile = await savePicker.PickSaveFileAsync();
    }
    else
    {
        StorageFolder local = Windows.Storage.ApplicationData.Current.LocalFolder;
        storageFile = await local.CreateFileAsync("Output.xls", CreationCollisionOption.ReplaceExisting);
    }
    //Saving the workbook
    await workbook.SaveAsAsync(storageFile);

    // Launch the saved file
    await Windows.System.Launcher.LaunchFileAsync(storageFile);
}
{% endhighlight %}

{% highlight ASP.NET Core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{

    //Instantiate the excel application object.
    IApplication application = excelEngine.Excel;

    //Opening form module existing workbook
    FileStream input = new FileStream(DataPathBase + "Test.xls", FileMode.Open, FileAccess.ReadWrite);
    IWorkbook workbook = application.Workbooks.Open(input);

    IWorksheet sheet = workbook.Worksheets[0];

    //Check macro exist
    bool IsMacroEnabled = workbook.HasMacros;     
             
    // Save the workbook
    FileStream output = new FileStream("Output.xls", FileMode.Create, FileAccess.ReadWrite);
    workbook.SaveAs(output);

    input.Close();
    output.Close();
}

{% endhighlight %}

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;

    //"App" is the class of Portable project
    Assembly assembly = typeof(App).GetTypeInfo().Assembly;
    Stream inputStream = assembly.GetManifestResourceStream("App.Test.xls");

    //Opening the workbook
    IWorkbook workbook = application.Workbooks.Open(inputStream);

    IWorksheet worksheet = workbook.Worksheets[0];

    //Check macro exist
    bool IsMacroEnabled = workbook.HasMacros;     
                
    //Saving as Excel without macros
    MemoryStream stream = new MemoryStream();
    workbook.SaveAs(stream);

    //Save the stream into XLSX file
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("sample.xls", "application/msexcel", stream);
}
{% endhighlight %}
{% endtabs %}   

## See Also

* [How to open an Excel 2013 Macro Enabled Template?](how-to-open-an-excel-2013-macro-enabled-template)
* [Does XlsIO support Excel files with macros that are digitally signed?](does-xlsio-support-excel-files-with-macros-that-are-digitally-signed)
* [Does XlsIO support password protected macro in the Excel documents?](does-xlsio-support-password-protected-macro-in-the-excel-documents)
* [How to create a macro?](https://help.syncfusion.com/file-formats/xlsio/working-with-macros#creating-a-macro)
* [How to edit a macro?](https://help.syncfusion.com/file-formats/xlsio/working-with-macros#editing-a-macro)
* [How to remove macros?](https://help.syncfusion.com/file-formats/xlsio/working-with-macros#removing-macros)
