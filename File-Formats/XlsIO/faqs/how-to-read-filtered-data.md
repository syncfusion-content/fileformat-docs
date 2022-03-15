---
title: Read the filtered data |Syncfusion
description: This page shows how to read the filtered data from the Excel file using Syncfusion .NET Excel library (XlsIO).
platform: File-formats
control: XlsIO
documentation: UG
---

# How to read filtered data?

You can access the filtered rows in the Excel file using the row height property. The hidden rows will have their row height as zero '0'. So based on this, you can loop the filtered rows. The following code snippet illustrates this.

{% tabs %}  

{% highlight c# %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;

    //Open an existing Excel file
    IWorkbook workbook = excelEngine.Excel.Workbooks.Open("../../Sample.xlsx");
    IWorksheet worksheet = workbook.Worksheets[0];
    IRange usedRange = worksheet.UsedRange;

    string[] rowValues = new string[usedRange.Columns.Length];

    for (int row = usedRange.Row; row <= usedRange.LastRow; row++)
    {
         //Validated the row is filtered or not
         if (worksheet.Rows[row-1].RowHeight != 0)
         {
              for (int column = usedRange.Column; column <= usedRange.LastColumn; column++)
              {
                   rowValues.SetValue(worksheet.Range[row , column].Value, column-1);
              }
         }
    }
}
{% endhighlight %}

{% highlight vb %}
Using excelEngine As ExcelEngine = New ExcelEngine()

    Dim application As IApplication = excelEngine.Excel
    application.DefaultVersion = ExcelVersion.Xlsx
    Dim workbook As IWorkbook = application.Workbooks.Open("../../Sample.xlsx")
    Dim worksheet As IWorksheet = workbook.Worksheets(0)
    Dim usedRange As IRange = worksheet.UsedRange

    Dim rowValues(3) As String
    Dim row As Integer
    Dim column As Integer

    For row = usedRange.Row To usedRange.LastRow Step row + 1
         If worksheet.Rows(row - 1).RowHeight <> 0 Then
              For column = usedRange.Column To usedRange.LastColumn
                   rowValues(column - 1) = worksheet.Range(row, column).Value
              Next
         End If
    Next

End Using
{% endhighlight %}

{% highlight UWP %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    //Set the default application version as Excel 2016.
    excelEngine.Excel.DefaultVersion = ExcelVersion.Excel2016;

    //Instantiates the File Picker
    FileOpenPicker openPicker = new FileOpenPicker();
    openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
    openPicker.FileTypeFilter.Add(".xlsx");
    openPicker.FileTypeFilter.Add(".xls");

    //Creates a storage file from FileOpenPicker
    StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();

    //Loads or open an existing workbook
    IWorkbook workbook = await excelEngine.Excel.Workbooks.OpenAsync(inputStorageFile);

    //Access first worksheet from the workbook instance.
    IWorksheet worksheet = workbook.Worksheets[0];

    IRange usedRange = worksheet.UsedRange;

    string[] rowValues = new string[usedRange.Columns.Length];

    for (int row = usedRange.Row; row <= usedRange.LastRow; row++)
    {
         //Validated the row is filtered or not
         if (worksheet.Rows[row-1].RowHeight != 0)
         {
              for (int column = usedRange.Column; column <= usedRange.LastColumn; column++)
              {
                   rowValues.SetValue(worksheet.Range[row , column ].Value, column-1);
              }
         }
    }
}
{% endhighlight %}

{% highlight ASP.NET Core %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;

    FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
    IWorkbook workbook = application.Workbooks.Open(fileStream, ExcelOpenType.Automatic);
    IWorksheet worksheet = workbook.Worksheets[0];
    IRange usedRange = worksheet.UsedRange;

    string[] rowValues = new string[usedRange.Columns.Length];

    for (int row = usedRange.Row; row <= usedRange.LastRow; row++)
    {
         //Validated the row is filtered or not
         if (worksheet.Rows[row-1].RowHeight != 0)
         {
              for (int column = usedRange.Column; column <= usedRange.LastColumn; column++)
              {
                   rowValues.SetValue(worksheet.Range[row, column].Value, column-1);
              }
         }
    }
}
{% endhighlight %}

{% highlight Xamarin %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
    //Set the default application version as Excel 2013.
    excelEngine.Excel.DefaultVersion = ExcelVersion.Excel2013;

    string resourcePath = "GettingStarted.Sample.xlsx";
    //"App" is the class of Portable project.
    Assembly assembly = typeof(App).GetTypeInfo().Assembly;
    Stream fileStream = assembly.GetManifestResourceStream(resourcePath);

    //Opens the workbook 
    IWorkbook workbook = excelEngine.Excel.Workbooks.Open(fileStream);                          

    //Access first worksheet from the workbook instance.
    IWorksheet worksheet = workbook.Worksheets[0];

    IRange usedRange = worksheet.UsedRange;

    string[] rowValues = new string[usedRange.Columns.Length];

    for (int row = usedRange.Row; row <= usedRange.LastRow; row++)
         {
              //Validated the row is filtered or not
              if (worksheet.Rows[row-1].RowHeight != 0)
              {
                   for (int column = usedRange.Column; column <= usedRange.LastColumn; column++)
                   {
                        rowValues.SetValue(worksheet.Range[row, column].Value, column-1);                        
                   }
              }
         }

    //Save the workbook to stream in xlsx format. 
    MemoryStream stream = new MemoryStream();
    workbook.SaveAs(stream);

    workbook.Close();

    //Save the stream as a file in the device and invoke it for viewing
    Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("GettingStared.xlsx", "application/msexcel", stream);

}
{% endhighlight %}

  {% endtabs %}  

## See Also

* [How to open an existing XLSX workbook and save it as XLS?](how-to-open-an-existing-xlsx-workbook-and-save-it-as-xls)
* [How to create and open Excel Template files by using XlsIO?](how-to-create-and-open-excel-template-files-by-using-xlsio)
* [How to copy a range from one workbook to another?](how-to-copy-a-range-from-one-workbook-to-another)
* [Does XlsIO support Excel files with macros that are digitally signed?](does-xlsio-support-excel-files-with-macros-that-are-digitally-signed)
* [How does Excel file with uninstalled fonts is converted to PDF/Image?](how-does-excel-file-with-uninstalled-fonts-is-converted-to-pdf-image)
* [How to sort two or more columns in a pivot table?](how-to-sort-two-or-more-columns-in-a-pivot-table)
* [How to move or copy a worksheet?](https://help.syncfusion.com/file-formats/xlsio/working-with-excel-worksheet#move-or-copy-a-worksheet)

