---
title: How to use Named Ranges with XlsIO | Syncfusion
description: This page demonstrates with an example on how to use named ranges in Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# How to use Named Ranges with XlsIO?

A named range can be added to worksheet or workbook based on the required scope, the following code snippet illustrate this. For more information, see [Named Range](https://support.microsoft.com/en-us/office/define-and-use-names-in-formulas-4d0f13ac-53b7-422e-afd2-abd7ff379c64?ui=en-us&rs=en-us&ad=us)

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Excel2013;
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Adding named range to the workbook
  IName workBookName = workbook.Names.Add("WorkBookName");
  workBookName.RefersToRange = worksheet.Range["I8"];

  //Looping through the Named Ranges in a workbook
  foreach (IName workbookName in workbook.Names)
  {
    MessageBox.Show(workbookName.Name.ToString());
  }

  //Adding named range to the worksheet
  IName worksheetName = worksheet.Names.Add("WorkSheetName");
  worksheetName.RefersToRange = worksheet.Range["J8"];

  //Looping through the Named Ranges in a worksheet
  foreach (IName name in worksheet.Names)
  {
    MessageBox.Show(name.Name.ToString());
  }

  FileStream stream = new FileStream("NamedRange.xlsx", FileMode.OpenOrCreate, FileAccess.ReadWrite);
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
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Adding named range to the workbook            
  IName workBookName = workbook.Names.Add("WorkBookName");
  workBookName.RefersToRange = worksheet.Range["I8"];

  //Looping through the Named Ranges in a workbook.
  foreach (IName workbookName in workbook.Names)
  {
    MessageBox.Show(workbookName.Name.ToString());
  }

  //Adding named range to the worksheet
  IName worksheetName = worksheet.Names.Add("WorkSheetName");
  worksheetName.RefersToRange = worksheet.Range["J8"];

  //Looping through the Named Ranges in a worksheet.
  foreach (IName name in worksheet.Names)
  {
    MessageBox.Show(name.Name.ToString());
  }
  workbook.SaveAs("NamedRange.Xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = excelEngine.Excel
  application.DefaultVersion = ExcelVersion.Excel2013
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Adding named range to the workbook
  Dim workBookName__1 As IName = workbook.Names.Add("WorkBookName")
  workBookName__1.RefersToRange = worksheet.Range("I8")

 'Looping through the Named Ranges in a workbook.
  For Each workbookName__2 As IName In workbook.Names
    MessageBox.Show(workbookName__2.Name.ToString())
  Next

  'Adding named range to the worksheet
  Dim worksheetName__3 As IName = worksheet.Names.Add("WorkSheetName")
  worksheetName__3.RefersToRange = worksheet.Range("J8")

  'Looping through the Named Ranges in a worksheet.
  For Each worksheetName__4 As IName In worksheet.Names
    MessageBox.Show(worksheetName__4.Name.ToString())
  Next

  workbook.SaveAs("NamedRange.Xlsx")
End Using
{% endhighlight %}
{% endtabs %}  

## See Also

* [How to avoid exception when adding worksheets with same name?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-avoid-exception-when-adding-worksheets-with-same-name)
* [How to create named range in Excel?](https://help.syncfusion.com/file-formats/xlsio/migrate-from-office-automation-to-syncfusion-xlsio/create-named-range-in-excel)
* [How to create a sparkline from a named range?](https://help.syncfusion.com/file-formats/xlsio/faqs/how-to-create-a-sparkline-from-a-named-range)
* [How to define names?](https://help.syncfusion.com/file-formats/xlsio/working-with-formulas#defined-names)
* [How to use named ranges in formulas?](https://help.syncfusion.com/file-formats/xlsio/working-with-formulas#named-ranges-in-formulas)
* [In which situation we use AutoDetectComplexScript converter property?](https://help.syncfusion.com/file-formats/xlsio/faqs/in-which-situation-we-use-autodetectcomplexscript-converter-property)
