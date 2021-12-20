---
title: FAQ Section| XlsIO | Syncfusion
description: This page shows how to resolve "Excel cannot open the file because the file format is not valid..." using XlsIO.
platform: File-formats
control: XlsIO
documentation: UG
---

# How to resolve "Excel cannot open the file 'filename.xlsx'..." error?

This error "Excel cannot open the file 'filename.xlsx' because the file format for the file extension is not valid. Verify that the file has not been corrupted and that the file extension matches the format of the file" occurs when there is a mismatch between the file format and its extension. The default workbook creation version in XlsIO is Excel97-2003 (.xls). The application version set to the required version should match its file format during save, as in the below code. 

{% tabs %}  

{% highlight c# %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

//Set application version

application.DefaultVersion = ExcelVersion.Excel2013;

//Do some manipulation

//Do some manipulation

//Workbook is saved in Excel2013 format

workbook.SaveAs("Sample.xlsx");

{% endhighlight %}

{% highlight vb %}
Dim excelEngine As New ExcelEngine()

Dim application As IApplication = excelEngine.Excel

'Set application version

application.DefaultVersion = ExcelVersion.Excel2013

'Do some manipulation

'Do some manipulation

'Workbook is saved in Excel2013 format

workbook.SaveAs("Sample.xlsx")

{% endhighlight %}

{% highlight UWP %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

//Set application version

application.DefaultVersion = ExcelVersion.Excel2013;

//Do some manipulation

//Do some manipulation

//Workbook is saved in Excel2013 format

//Initializes FileSavePicker
FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Sample";
savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

//Creates a storage file from FileSavePicker
StorageFile storageFile = await savePicker.PickSaveFileAsync();

//Saves changes to the specified storage file
await workbook.SaveAsAsync(storageFile);
{% endhighlight %}

{% highlight ASP.NET Core %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

//Set application version

application.DefaultVersion = ExcelVersion.Excel2013;

//Do some manipulation

//Do some manipulation

//Workbook is saved in Excel2013 format

 FileStream stream = new FileStream("Sample.xlsx", FileMode.OpenOrCreate, FileAccess.ReadWrite);
workbook.SaveAs(stream);
{% endhighlight %}

{% highlight Xamarin %}
ExcelEngine excelEngine = new ExcelEngine();

IApplication application = excelEngine.Excel;

//Set application version

application.DefaultVersion = ExcelVersion.Excel2013;

//Do some manipulation

//Do some manipulation

//Workbook is saved in Excel2013 format

MemoryStream stream = new MemoryStream();
workbook.SaveAs(stream);

stream.Position = 0;

//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.xlsx", "application/msexcel", stream);
{% endhighlight %}

{% endtabs %}  

If the application version is ignored, then the workbook version should be set properly during creation and save.

* To save a workbook in Excel2003 format, set the workbook version to Excel97to2003 and save the file with extension ‘.xls’ i.e. binary file format.

* To save a workbook in Excel 2007 and above formats, set the workbook version to Excel2007 and above and save the file with extension __‘.____xlsx’__ i.e. open XML file format.

These are represented in the below code snippet.

{% tabs %}  

{% highlight c# %}
workbook.Version = ExcelVersion.Excel97to2003;

workbook.SaveAs("Sample.xls");

workbook.Version = ExcelVersion.Excel2013;

workbook.SaveAs("Sample.xlsx");

{% endhighlight %}

{% highlight vb %}
workbook.Version = ExcelVersion.Excel97to2003

workbook.SaveAs("Sample.xls")

workbook.Version = ExcelVersion.Excel2013

workbook.SaveAs("Sample.xlsx")

{% endhighlight %}

{% highlight UWP %}
workbook.Version = ExcelVersion.Excel97to2003;

FileSavePicker savePicker = new FileSavePicker();
savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker.SuggestedFileName = "Sample";
savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xls" });
StorageFile storageFile = await savePicker.PickSaveFileAsync();
await workbook.SaveAsAsync(storageFile);

workbook.Version = ExcelVersion.Excel2013;

FileSavePicker savePicker1 = new FileSavePicker();
savePicker1.SuggestedStartLocation = PickerLocationId.Desktop;
savePicker1.SuggestedFileName = "Sample";
savePicker1.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });
StorageFile storageFile1 = await savePicker1.PickSaveFileAsync();
await workbook.SaveAsAsync(storageFile1); 
{% endhighlight %}

{% highlight ASP.NET Core %}
workbook.Version = ExcelVersion.Excel97to2003;
FileStream stream = new FileStream("Sample.xls", FileMode.OpenOrCreate, FileAccess.ReadWrite);
workbook.SaveAs(stream);

workbook.Version = ExcelVersion.Excel2013;
FileStream stream1 = new FileStream("Sample.xlsx", FileMode.OpenOrCreate, FileAccess.ReadWrite);
workbook.SaveAs(stream1); 
{% endhighlight %}

{% highlight Xamarin %}
workbook.Version = ExcelVersion.Excel97to2003;

//SaveAndView method is not implemented to save and open .xls files. Hence, saving it as stream.
MemoryStream stream = new MemoryStream();
workbook.SaveAs(stream);
stream.Position = 0;
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xls", "application/vnd.ms-excel", stream);

workbook.Version = ExcelVersion.Excel2013;

MemoryStream stream1 = new MemoryStream();
workbook.SaveAs(stream1);
stream1.Position = 0;
//Save the stream as a file in the device and invoke it for viewing
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Sample.xlsx", "application/msexcel", stream1);
{% endhighlight %}

{% endtabs %}  
  
## See Also

* [How to resolve the File does not contain workbook stream error in Syncfusion.XlsIO.Base.dll?](how-to-resolve-the-file-does-not-contain-workbook-stream-error-in-syncfusion-xlsio-base-dll)
* [What are the known exceptions of XlsIO?](https://help.syncfusion.com/file-formats/xlsio/known-exceptions)
* [What are the supported features by file formats?](https://help.syncfusion.com/file-formats/xlsio/supported-features-by-file-formats)
