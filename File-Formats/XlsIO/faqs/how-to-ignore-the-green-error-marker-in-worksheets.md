---
title: Ignore green error marker in worksheets | XlsIo | Syncfusion
description: This page demonstrates how to ignore the green error marker in worksheets using Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# How to ignore the green error marker in worksheets?

When there exists data that are of different formats, the error marker appears in cells. In XlsIO You can ignore this by using [IgnoreErrorOptions](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IRange.html#Syncfusion_XlsIO_IRange_IgnoreErrorOptions) property. The following code snippet illustrate this.

{% tabs %} 
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream inputStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelOpenType.Automatic);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Ignore Error Options
  worksheet.Range["B3"].IgnoreErrorOptions = ExcelIgnoreError.All;

  FileStream stream = new FileStream("IgnoreGreenError.xlsx", FileMode.OpenOrCreate, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  workbook.Close();
  excelEngine.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Ignore Error Options
  worksheet.Range["B3"].IgnoreErrorOptions = ExcelIgnoreError.All;

  workbook.SaveAs("IgnoreGreenError.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Ignore Error Options
  worksheet.Range("B3").IgnoreErrorOptions = ExcelIgnoreError.All

  workbook.SaveAs("IgnoreGreenError.xlsx")
End Using
{% endhighlight %}
{% endtabs %}  

## See Also

* [How to ignore print areas set in a worksheet?](how-to-ignore-print-areas-set-in-a-worksheet)
* [How to resolve Excel cannot open the file filename.xlsx... error?](how-to-resolve-excel-cannot-open-the-file-because-the-file-format-for-the-file-extension-is-not-valid)
* [How to resolve the File does not contain workbook stream error in Syncfusion.XlsIO.Base.dll?](how-to-resolve-the-file-does-not-contain-workbook-stream-error)
