---
title: How to detect merged cells in Excel | XlsIO | Syncfusion
description: This page explains how to detect merged cells in an Excel document using Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# How to detect merged cells in Excel?

The merged cells in an Excel worksheet can be detected through [MergedCells](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorksheet.html#Syncfusion_XlsIO_IWorksheet_MergedCells) of IWorksheet. The following complete code snippet explains this.

{% tabs %} 
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  FileStream fileStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);
  IWorkbook workbook = application.Workbooks.Open(fileStream);
  IWorksheet worksheet = workbook.Worksheets[0];

  //Create a new worksheet
  IWorksheet mergedCells = workbook.Worksheets.Create("MergedCells");

  //Get the list of merged cells
  for (int pos = 0; pos < worksheet.MergedCells.Length; pos++)
  {
    mergedCells.Range["A" + (pos + 1).ToString()].Text = (pos + 1).ToString() + "th Merged region = " + worksheet.MergedCells[pos].Address;
  }

  //Autofit the used range
  mergedCells.UsedRange.AutofitColumns();

  //Saving the workbook as stream
  FileStream stream = new FileStream("Output.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(stream);
  stream.Dispose();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  IApplication application = excelEngine.Excel;
  application.DefaultVersion = ExcelVersion.Xlsx;
  IWorkbook workbook = application.Workbooks.Open("Sample.xlsx");
  IWorksheet worksheet = workbook.Worksheets[0];

  //Create a new worksheet
  IWorksheet mergedCells = workbook.Worksheets.Create("MergedCells");

  //Get the list of merged cells
  for (int pos = 0; pos < worksheet.MergedCells.Length; pos++)
  {
    mergedCells.Range["A" + (pos+1).ToString()].Text = (pos+1).ToString()+"th Merged region = "+ worksheet.MergedCells[pos].Address;
  }

  //Autofit the used range
  mergedCells.UsedRange.AutofitColumns();

  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  Dim application As IApplication = ExcelEngine.Excel
  application.DefaultVersion = ExcelVersion.Xlsx
  Dim workbook As IWorkbook = application.Workbooks.Open("Sample.xlsx")
  Dim worksheet As IWorksheet = workbook.Worksheets(0)

  'Create a new worksheet
  Dim mergedCells As IWorksheet = workbook.Worksheets.Create("MergedCells")

  'Get the list of merged cells
  For pos As Integer = 0 To worksheet.MergedCells.Length - 1 Step 1
    mergedCells.Range("A" + (pos + 1).ToString()).Text = (pos + 1).ToString() + "th Merged region = " + worksheet.MergedCells(pos).Address
  Next

  'Autofit the used range
  mergedCells.UsedRange.AutofitColumns()

  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}
{% endtabs %}
