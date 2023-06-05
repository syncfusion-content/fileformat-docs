---
title: How to protect certain cells in a worksheet | XlsIO | Syncfusion
description: This page demonstrates with an example to protect certain cells in a worksheet using Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# How to protect certain cells in a worksheet?

All the cells in an Excel worksheet have a **Locked** property, which determines if the cell will be editable. When a worksheet is protected, all the cells in the worksheet get locked, by default.

However, there is often a need to protect only certain cells in a worksheet. In this scenario, you need to protect a worksheet, and set the [Locked](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IExtendedFormat.html#Syncfusion_XlsIO_IExtendedFormat_Locked) property as false for the cells that need to be made editable. 

The following code snippet illustrate this.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  FileStream inputStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(inputStream, ExcelOpenType.Automatic);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Sample data
  worksheet.Range["A1:K20"].Text = "Locked";

  //A1:A10 will not be protected, hence it is editable.
  worksheet.Range["A1:A10"].CellStyle.Locked = false;
  worksheet.Range["A1:A10"].Text = "UnLocked";
  worksheet.Protect("syncfusion", ExcelSheetProtection.All);

  FileStream stream = new FileStream("ProtectCells.xlsx", FileMode.OpenOrCreate, FileAccess.ReadWrite);
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

  //Sample data
  worksheet.Range["A1:K20"].Text = "Locked";

  //A1:A10 will not be protected, hence it is editable.
  worksheet.Range["A1:A10"].CellStyle.Locked = false;
  worksheet.Range["A1:A10"].Text = "UnLocked";
  worksheet.Protect("syncfusion", ExcelSheetProtection.All);
  workbook.SaveAs("ProtectCells.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx", ExcelOpenType.Automatic)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Sample data
  worksheet.Range("A1:K20").Text = "Locked"

  'A1:A10 will not be protected.
  worksheet.Range("A1:A10").CellStyle.Locked = False
  worksheet.Range("A1:A10").Text = "UnLocked"
  worksheet.Protect("syncfusion", ExcelSheetProtection.All)
  workbook.SaveAs("ProtectCells.xlsx")
End Using
{% endhighlight %}
{% endtabs %}  

N> Locking/Unlocking cells in an unprotected worksheet has no effect.

## See Also

* [How to protect Excel workbook?](https://help.syncfusion.com/file-formats/xlsio/migrate-from-office-automation-to-syncfusion-xlsio/protect-excel-workbook)
* [How to protect worksheet?](https://help.syncfusion.com/file-formats/xlsio/security#protect-worksheet)
* [How to protect the zip files using Syncfusion.Compression.Base?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-protect-the-zip-files-using-syncfusion-compression-base)
* [How to un-protect the zip files using Syncfusion.Compression.Base?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-un-protect-the-zip-files-using-syncfusion-compression-base)