---
title: How to read filtered rows in Excel? |Syncfusion
description: This page shows how to read the filtered data from the Excel file using Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# How to read filtered rows in Excel?

The filtered rows in an Excel document can be read through [RowHeight](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IRange.html#Syncfusion_XlsIO_IRange_RowHeight) property. The filtered rows, also called as hidden rows, will have the row height as 0. The following code explains this.

{% tabs %}  

{% highlight c# tabtitle="C#" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  //Open an existing Excel file
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
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

{% highlight vb.net tabtitle="VB.NET" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
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

{% highlight c# tabtitle="UWP" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2016;    
  //Instantiates the File Picker
  FileOpenPicker openPicker = new FileOpenPicker();
  openPicker.SuggestedStartLocation = PickerLocationId.Desktop;
  openPicker.FileTypeFilter.Add(".xlsx");
  openPicker.FileTypeFilter.Add(".xls");

  //Creates a storage file from FileOpenPicker
  StorageFile inputStorageFile = await openPicker.PickSingleFileAsync();
  //Loads or open an existing workbook
  IWorkbook workbook = await application.Workbooks.OpenAsync(inputStorageFile);
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

{% highlight c# tabtitle="ASP.NET Core" %}
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

{% highlight c# tabtitle="Xamarin" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  string resourcePath = "GettingStarted.Sample.xlsx";
  //"App" is the class of Portable project.
  Assembly assembly = typeof(App).GetTypeInfo().Assembly;
  Stream fileStream = assembly.GetManifestResourceStream(resourcePath);

  //Opens the workbook 
  IWorkbook workbook = application.Workbooks.Open(fileStream);                        
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

