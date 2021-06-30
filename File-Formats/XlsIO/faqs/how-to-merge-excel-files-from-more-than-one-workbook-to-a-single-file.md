---
title: FAQ Section| XlsIO | Syncfusion
description: Code example to merge several Excel files from more than one workbook to a single file using Suncfusion's XlsIO.
platform: File-formats
control: XlsIO
documentation: UG
---

# How to merge Excel files from more than one workbook to a single file?

You can merge several Excel files from more than one workbook to a single file. The following code snippet illustrates this.

{% tabs %}  

{% highlight c# %}
//Loads all the template documents from Data folder
string[] files = Directory.GetFiles(@"../../Data/");

using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Excel2013;

    //Create empty Excel workbook instance with one empty worksheet
    IWorkbook workbook = application.Workbooks.Create(1);

    //Enumerates all the workbook files from the data folder and clone and merge it into new workbook
    foreach (string file in files)
    {
		//Loads the all template document from data folder
		FileStream inputStream = new FileStream(file, FileMode.Open, FileAccess.Read);

		//Opens the template workbook from stream
		IWorkbook tempWorkbook = application.Workbooks.Open(inputStream);

		//Disposes the stream
		inputStream.Dispose();

		//Cloning all workbook's worksheets
		workbook.Worksheets.AddCopy(tempWorkbook.Worksheets);
	}
	
	//Removing the first empty worksheet
	workbook.Worksheets.Remove(0);

	workbook.SaveAs("MergingFiles.xlsx");
}
{% endhighlight %}

{% highlight vb %}
'Loads the all template document from data folder
Dim files As String() = Directory.GetFiles("../../Data/")

Using excelEngine As ExcelEngine = New ExcelEngine()
    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Excel2013

    'Create empty Excel workbook instance with one empty worksheet 
    Dim workbook As IWorkbook = application.Workbooks.Create(1)

    'Enumerates all the workbook files from the data folder and clone and merge it into new workbook
    For Each file As String In files
        'Loads the all template document from data folder
        Dim inputStream As New FileStream(file, FileMode.Open, FileAccess.Read)

        'Opens the template workbook from stream
        Dim tempWorkbook As IWorkbook = application.Workbooks.Open(inputStream)

        'Disposes the stream
        inputStream.Dispose()

        'Cloning all workbook's worksheets
        workbook.Worksheets.AddCopy(tempWorkbook.Worksheets)
    Next

    'Removing the first empty worksheet
    workbook.Worksheets.Remove(0)

    workbook.SaveAs("MergingFiles.xlsx")
End Using
{% endhighlight %}

{% highlight UWP %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Excel2013;

    //Create empty Excel workbook instance with one empty worksheet
    IWorkbook workbook = application.Workbooks.Create(1);

    //Instantiates the File Picker
    FileOpenPicker openPicker = new FileOpenPicker();
    openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
    openPicker.FileTypeFilter.Add(".xlsx");
    openPicker.FileTypeFilter.Add(".xls");
    IReadOnlyList<StorageFile> files = await openPicker.PickMultipleFilesAsync();

    //Enumerates all the workbook files from the data folder and clone and merge it into new workbook
    foreach (StorageFile file in files)
    {
        //Opens the template workbook from stream
        IWorkbook tempWorkbook = await application.Workbooks.OpenAsync(file);

        //Cloning all workbook's worksheets
        workbook.Worksheets.AddCopy(tempWorkbook.Worksheets);
    }

    //Removing the first empty worksheet
    workbook.Worksheets.Remove(0);

    //Initializes FileSavePicker
    FileSavePicker savePicker = new FileSavePicker();
    savePicker.SuggestedStartLocation = PickerLocationId.Desktop;
    savePicker.SuggestedFileName = "MergingFiles";
    savePicker.FileTypeChoices.Add("Excel Files", new List<string>() { ".xlsx" });

    //Creates a storage file from FileSavePicker
    StorageFile storageFile = await savePicker.PickSaveFileAsync();

    //Saves changes to the specified storage file
    await workbook.SaveAsAsync(storageFile);
}
{% endhighlight %}

{% highlight ASP.NET Core %}
//Loads all the template documents from Data folder
string[] files = Directory.GetFiles(@"Data/");

using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Excel2013;

    //Create empty Excel workbook instance with one empty worksheet
    IWorkbook workbook = application.Workbooks.Create(1);

    //Enumerates all the workbook files from the data folder and clone and merge it into new workbook
    foreach (string file in files)
    {
        //Loads a template document from data folder
        FileStream inputStream = new FileStream(file, FileMode.Open, FileAccess.Read);

        //Opens the template workbook from stream
        IWorkbook tempWorkbook = application.Workbooks.Open(inputStream);

        //Disposes the stream
        inputStream.Dispose();

        //Cloning all workbook's worksheets
        workbook.Worksheets.AddCopy(tempWorkbook.Worksheets);
    }

    //Removing the first empty worksheet
    workbook.Worksheets.Remove(0);

    FileStream outputStream = new FileStream("MergingFiles.xlsx", FileMode.OpenOrCreate, FileAccess.ReadWrite);
    workbook.SaveAs(outputStream);

    workbook.Close();
    excelEngine.Dispose();
}
{% endhighlight %}

{% highlight Xamarin %}
//Get the path with files to merge
string path = Path.Combine(Environment.CurrentDirectory);
string[] files = Directory.GetFiles(path, "Sample*");

using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Excel2013;

    //Create empty Excel workbook instance with one empty worksheet
    IWorkbook workbook = application.Workbooks.Create(1);

    //Enumerates all the workbook files from the folder and clone and merge it into new workbook
    foreach (string file in files)
    {        
        //Loads a template document from the folder
        FileStream inputStream = new FileStream(file, FileMode.Open, FileAccess.Read);

        //Opens the template workbook from stream
        IWorkbook tempWorkbook = application.Workbooks.Open(inputStream);

        //Disposes the stream
        inputStream.Dispose();

        //Cloning all workbook's worksheets
        workbook.Worksheets.AddCopy(tempWorkbook.Worksheets);
    }

    //Removing the first empty worksheet
    workbook.Worksheets.Remove(0);
     
    MemoryStream stream = new MemoryStream();
    workbook.SaveAs(stream);

    stream.Position = 0;

    //Save the stream as a file in the device and invoke it for viewing
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("MergingFiles.xlsx", "application/msexcel", stream);
}
{% endhighlight %}

  {% endtabs %}  

## See Also

* [How to open an existing XLSX workbook and save it as XLS?](faqs/how-to-open-an-existing-xlsx-workbook-and-save-it-as-xls)
* [How to create and open Excel Template files by using XlsIO?](faqs/how-to-create-and-open-excel-template-files-by-using-xlsio)
* [How to copy a range from one workbook to another?](faqs/how-to-copy-a-range-from-one-workbook-to-another)
* [Does XlsIO support Excel files with macros that are digitally signed?](faqs/does-xlsio-support-excel-files-with-macros-that-are-digitally-signed)
* [How does Excel file with uninstalled fonts is converted to PDF/Image?](faqs/how-does-excel-file-with-uninstalled-fonts-is-converted-to-pdf-image)
* [How to sort two or more columns in a pivot table?](faqs/how-to-sort-two-or-more-columns-in-a-pivot-table)
* [How to move or copy a worksheet?](https://help.syncfusion.com/file-formats/xlsio/working-with-excel-worksheet#move-or-copy-a-worksheet)

