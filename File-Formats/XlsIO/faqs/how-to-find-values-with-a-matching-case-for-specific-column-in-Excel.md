---
title: Values with matching case for specific column in an Excel |Syncfusion
description: This page shows how to find values with matching case for specific column in an Excel worksheet using Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# How to find values with a matching case for specific column in Excel?
XlsIO allows finding values with matching case for specific column in Excel worksheet using **MatchCase** option of [ExcelFindOptions](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelFindOptions.html) enumeration through [Find](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.Implementation.WorksheetImpl.html#Syncfusion_XlsIO_Implementation_WorksheetImpl_Find_Syncfusion_XlsIO_IRange_System_String_Syncfusion_XlsIO_ExcelFindType_Syncfusion_XlsIO_ExcelFindOptions_System_Boolean_) method of [WorksheetImpl](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.Implementation.WorksheetImpl.html). The following code illustrates this.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream, ExcelOpenType.Automatic);
  IWorksheet worksheet = workbook.Worksheets[0];

  IRange[] range1 = (worksheet as WorksheetImpl).Find(worksheet.Range["C1"].EntireColumn, "90", ExcelFindType.Number, ExcelFindOptions.MatchCase, false);
  IRange[] range2 = (worksheet as WorksheetImpl).Find(worksheet.Range["Q1"].EntireColumn, "90", ExcelFindType.Number, ExcelFindOptions.MatchCase, false);
  IRange[] range3 = (worksheet as WorksheetImpl).Find(worksheet.Range["AA1"].EntireColumn, "90", ExcelFindType.Number, ExcelFindOptions.MatchCase, false);
  IRanges ranges = worksheet.CreateRangesCollection();

  for (int range = 0; range < range1.Length; range++)
    ranges.Add(range1[range]);
  for (int range = 0; range < range2.Length; range++)
    ranges.Add(range2[range]);
  for (int range = 0; range < range3.Length; range++)
    ranges.Add(range3[range]);
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
  IWorksheet worksheet = workbook.Worksheets[0];                             

  IRange[] range1 = (worksheet as WorksheetImpl).Find(worksheet.Range["C1"].EntireColumn, "90", ExcelFindType.Number, ExcelFindOptions.MatchCase, false);
  IRange[] range2 = (worksheet as WorksheetImpl).Find(worksheet.Range["Q1"].EntireColumn, "90", ExcelFindType.Number, ExcelFindOptions.MatchCase, false);
  IRange[] range3 = (worksheet as WorksheetImpl).Find(worksheet.Range["AA1"].EntireColumn, "90", ExcelFindType.Number, ExcelFindOptions.MatchCase, false);
  IRanges ranges = worksheet.CreateRangesCollection();

  for (int range = 0; range < range1.Length; range++)
    ranges.Add(range1[range]);
  for (int range = 0; range < range2.Length; range++)
    ranges.Add(range2[range]);
  for (int range = 0; range < range3.Length; range++)
    ranges.Add(range3[range]);   
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx    
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
  'Access first worksheet from the workbook instance
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  Dim range1 As IRange() = (TryCast(sheet, WorksheetImpl)).Find(sheet.Range("C1").EntireColumn, "90", ExcelFindType.Number, ExcelFindOptions.MatchCase, False)
  Dim range2 As IRange() = (TryCast(sheet, WorksheetImpl)).Find(sheet.Range("Q1").EntireColumn, "90", ExcelFindType.Number, ExcelFindOptions.MatchCase, False)
  Dim range3 As IRange() = (TryCast(sheet, WorksheetImpl)).Find(sheet.Range("AA1").EntireColumn, "90", ExcelFindType.Number, ExcelFindOptions.MatchCase, False)
  Dim ranges As IRanges = sheet.CreateRangesCollection()

  For range As Integer = 0 To range1.Length - 1 Step range + 1
    ranges.Add(range1(range))
  Next
  For range As Integer = 0 To range2.Length - 1 Step range + 1
    ranges.Add(range2(range))
  Next
  For range As Integer = 0 To range3.Length - 1 Step range + 1
    ranges.Add(range3(range))
  Next
End Using
{% endhighlight %}
{% endtabs %}  

## See Also

* [How to opening an existing workbook?](https://help.syncfusion.com/file-formats/xlsio/loading-and-saving-workbook#opening-an-existing-workbook)
* [How to perform Find and Replace?](https://help.syncfusion.com/file-formats/xlsio/worksheet-cells-manipulation#find-and-replace)
* [How to get entire column of the particular range?](https://help.syncfusion.com/file-formats/xlsio/worksheet-cells-manipulation#entire-column)
* [How to define discontinuous ranges?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-define-discontinuous-ranges)
* [How to create and open Excel Template files by using XlsIO?](how-to-create-and-open-excel-template-files-by-using-xlsio)
* [How to copy a range from one workbook to another?](how-to-copy-a-range-from-one-workbook-to-another)
* [How to sort two or more columns in a pivot table?](how-to-sort-two-or-more-columns-in-a-pivot-table)
* [How to move or copy a worksheet?](https://help.syncfusion.com/file-formats/xlsio/working-with-excel-worksheet#move-or-copy-a-worksheet)
