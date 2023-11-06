---
title: Merge Excel files from multiple workbooks into single file |Syncfusion
description: Code example to merge several Excel files from more than one workbook to a single file using Suncfusion's XlsIO.
platform: file-formats
control: XlsIO
documentation: UG
---

# How to merge Excel files from more than one workbook to a single file?

You can merge several Excel files from more than one workbook to a single file. The following code snippet illustrates this.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Loads all the template documents from Data folder
string[] files = Directory.GetFiles("Data/");

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

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Loads all the template documents from Data folder
string[] files = Directory.GetFiles("../../Data/");

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

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
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
{% endtabs %}  

## See Also

* [How to open an existing XLSX workbook and save it as XLS?](how-to-open-an-existing-xlsx-workbook-and-save-it-as-xls)
* [How to create and open Excel Template files by using XlsIO?](how-to-create-and-open-excel-template-files-by-using-xlsio)
* [How to copy a range from one workbook to another?](how-to-copy-a-range-from-one-workbook-to-another)
* [Does XlsIO support Excel files with macros that are digitally signed?](does-xlsio-support-excel-files-with-macros-that-are-digitally-signed)
* [How does Excel file with uninstalled fonts is converted to PDF/Image?](how-does-excel-file-with-uninstalled-fonts-is-converted-to-pdf-image)
* [How to sort two or more columns in a pivot table?](how-to-sort-two-or-more-columns-in-a-pivot-table)
* [How to move or copy a worksheet?](https://help.syncfusion.com/file-formats/xlsio/working-with-excel-worksheet#move-or-copy-a-worksheet)

