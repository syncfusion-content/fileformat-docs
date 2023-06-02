---
title: Create and open Excel Template files by using XlsIO | Syncfusion
description: This page shows how to create and open Excel Template files using Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# How to create and open Excel Template files by using XlsIO?

**Creating** **Excel** **Template** **Files**

Excel template files (XLT or XLTX) can be created in XlsIO by saving a file as **Template** using [ExcelSaveType](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelSaveType.html) enumeration. The following code snippet illustrates this.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Save as XLT
  workbook.Version = ExcelVersion.Excel97to2003;
  FileStream stream = new FileStream("XLTFile.xlt", FileMode.OpenOrCreate, FileAccess.ReadWrite);
  workbook.SaveAs(stream, ExcelSaveType.SaveAsTemplate);

  //Save as XLTX
  workbook.Version = ExcelVersion.Excel2007;
  FileStream stream1 = new FileStream("XLTXFile.xltx", FileMode.OpenOrCreate, FileAccess.ReadWrite);
  workbook.SaveAs(stream1, ExcelSaveType.SaveAsTemplate);
  workbook.Close();
  excelEngine.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Save as XLT
  workbook.Version = ExcelVersion.Excel97to2003;
  workbook.SaveAs("XLTFile.xlt", ExcelSaveType.SaveAsTemplate);

  //Save as XLTX
  workbook.Version = ExcelVersion.Excel2007;
  workbook.SaveAs("XLTXFile.xltx", ExcelSaveType.SaveAsTemplate);
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Save as XLT
  workbook.Version = ExcelVersion.Excel97to2003
  workbook.SaveAs("XLTFile.xlt", ExcelSaveType.SaveAsTemplate)

  'Save as XLTX
  workbook.Version = ExcelVersion.Excel2007
  workbook.SaveAs("XLTXFile.xltx", ExcelSaveType.SaveAsTemplate)
End Using
{% endhighlight %}
{% endtabs %}  

**Opening** **Excel** **Template** **Files**

In XlsIO, an Excel template file is opened in the same way, as excel workbook (.xls and .xlsx) is opened. The following code snippet illustrates this.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream inputStream = new FileStream("Sample.xltx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelOpenType.Automatic);

  FileStream stream = new FileStream("Output.xlsx", FileMode.OpenOrCreate, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  workbook.Close();
  excelEngine.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
ExcelEngine excelEngine = new ExcelEngine();
IApplication application = excelEngine.Excel;
application.DefaultVersion = ExcelVersion.Excel2013;

//Open Excel Template.
IWorkbook workbook = application.Workbooks.Open("Sample.xltx", ExcelOpenType.Automatic);
workbook.SaveAs("Output.xlsx");
workbook.Close();
excelEngine.Dispose();
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Dim excelEngine As New ExcelEngine()
Dim application As IApplication = excelEngine.Excel
application.DefaultVersion = ExcelVersion.Excel2013

'Open Excel Template.
Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xltx", ExcelOpenType.Automatic)
workbook.SaveAs("Output.xlsx")
workbook.Close()
excelEngine.Dispose()
{% endhighlight %}
{% endtabs %}  

## See Also

* [How to create a Chart with a discontinuous range?](how-to-create-a-chart-with-a-discontinuous-range)
* [How to create a sparkline from a named range?](how-to-create-a-sparkline-from-a-named-range)
* [How to open an Excel 2013 Macro Enabled Template?](how-to-open-an-excel-2013-macro-enabled-template)
* [How to open an Excel file from stream?](how-to-open-an-excel-file-from-stream)
* [How to open an existing XLSX workbook and save it as XLS?](how-to-open-an-existing-xlsx-workbook-and-save-it-as-xls)
* [Does XlsIO support Excel files with macros that are digitally signed?](does-xlsio-support-excel-files-with-macros-that-are-digitally-signed)
* [How to create a simple Excel file?](https://help.syncfusion.com/file-formats/xlsio/getting-started-create-excel-file-csharp-vbnet#create-a-simple-excel-file)
* [How to fill template based data Template Markers](https://help.syncfusion.com/file-formats/xlsio/getting-started-create-excel-file-csharp-vbnet#template-based-data-filling-using-template-markers)
* [How to open an existing workbook?](https://help.syncfusion.com/file-formats/xlsio/loading-and-saving-workbook#opening-an-existing-workbook)
* [How to open a CSV file?](https://help.syncfusion.com/file-formats/xlsio/working-with-excel-worksheet#open-a-csv-file)
