---
title: Unhide Excel Worksheets | Syncfusion
description: Explains with an example on how to unhide Excel worksheets which are in hidden state using Interop and XlsIO.
platform: file-formats
control: XlsIO
documentation: UG
---

# Unhide Excel Worksheets

Hidden sheets can be unhidden. The following code shows how to unhide Excel worksheets with Interop and XlsIO for .NET.

## Interop

{% tabs %}
{% highlight c# tabtitle="C#" %}
private void UnhideWorksheet()
{
  //Instantiate the application object
  var excelApp = new Microsoft.Office.Interop.Excel.Application();

  //Open the workbook with hidden worksheets
  Workbook workbook = excelApp.Workbooks.Open("InteropOutput_HiddenWorksheet.xlsx");

  //Get the first sheet
  Worksheet worksheet = (Worksheet)workbook.Sheets["Sheet1"];

  //Unhide the worksheet
  worksheet.Visible = XlSheetVisibility.xlSheetVisible;

  //Save the file
  workbook.SaveCopyAs("InteropOutput_UnhiddenWorksheet.xlsx");

  //Quit the application
  excelApp.Quit();
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Private Sub UnhideWorksheet()
  'Instantiate the application object
  Dim excelApp = New Microsoft.Office.Interop.Excel.Application()

  'Open the workbook with hidden worksheets
  Dim workbook As Workbook = excelApp.Workbooks.Open("InteropOutput_HiddenWorksheet.xlsx")

  'Get the first sheet
  Dim worksheet As Worksheet = workbook.Sheets("Sheet1")

  'Unhide the worksheet
  worksheet.Visible = XlSheetVisibility.xlSheetVisible

  'Save the file
  workbook.SaveCopyAs("InteropOutput_UnhiddenWorksheet.xlsx")

  'Quit the application
  excelApp.Quit()
End Sub
{% endhighlight %}
{% endtabs %}

## XlsIO

{% tabs %}
{% highlight c# tabtitle="C#" %}
private void UnhideWorksheet()
{
  using (ExcelEngine excelEngine = new ExcelEngine())
  {
    //Instantiate the application object
    IApplication application = excelEngine.Excel;

    //Open the workbook with hidden worksheets
    IWorkbook workbook = application.Workbooks.Open("XlsIOOutput_HiddenWorksheet.xlsx");

    //Get the first sheet
    IWorksheet worksheet = workbook.Worksheets[0];

    //Unhide the worksheet
    worksheet.Visibility = WorksheetVisibility.Visible;

    //Save the workbook
    workbook.SaveAs("XlsIOOutput_UnhiddenWorksheet.xlsx");
  }
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Private Sub UnhideWorksheet()
  Using excelEngine As ExcelEngine = New ExcelEngine()
    'Instantiate the application object
    Dim application As IApplication = excelEngine.Excel

    'Open the Excel file
    Dim workbook As IWorkbook = application.Workbooks.Open("XlsIOOutput_HiddenWorksheet.xlsx")

    'Get the first sheet
    Dim worksheet As IWorksheet = workbook.Worksheets(0)

    'Unhide the worksheet
    worksheet.Visibility = WorksheetVisibility.Visible

    'Save as Excel file
    workbook.SaveAs("XlsIOOutput_UnhiddenWorksheet.xlsx")
  End Using
End Sub
{% endhighlight %}
{% endtabs %}
